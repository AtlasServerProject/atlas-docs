# M6 — Entrega e ciclo comercial de VIP

03/10/2026. API 0.6.0/schema 8 e Core 1.30.0 instalados. Frontend publicado no Cloudflare Pages pelo GitHub. Vendas continuam fechadas; pagamentos externos continuam em test. Implementação e testes isolados concluídos, homologação final em jogo e abertura comercial pendentes.

## Fluxo de entrega

Pagamento validado pelo M5 cria uma única delivery_outbox. O Core consulta a API por HTTPS de saída, recebe uma tentativa com lease de 120 segundos e aplica somente planos conhecidos: vip-1 → VIP, vip-2 → VIPPLUS, vip-3 → VIPPLUSPLUS, sempre 30 dias/Emerald. Não recebe comandos, RCON ou identificadores de ranks arbitrários.

O recebedor vem do snapshot imutável do pedido: subject estável + players.id. O Core confirma ambos em site_identities, sem confiar em nickname nem exigir jogador online. Promoção de identidade Premium preserva players.id/subject. Recibo único por delivery_id e saldo são gravados na mesma transação PostgreSQL, com bloqueio do jogador. A repetição usa o mesmo identificador e fingerprint e devolve o recibo original; payload diferente é recusado. A ativação começa no instante registrado pelo Core, inclusive para jogador offline.

O ACK exige a tentativa vigente, recibo compatível e pagamento PAID. Status de entrega, recibo, espelho VIP, evento e auditoria são confirmados em uma transação na API. Se a resposta se perde depois do commit Core ou API, a repetição não concede prazo novamente. ACK antigo não vence uma nova lease. Tentativas têm backoff e seguem para revisão após oito claims; administração reprocessa com justificativa, preservando delivery_id. Uma compensação/reembolso entre claim e concessão requer análise operacional: não existe transação distribuída entre os dois bancos.

## Tempo, pausa e retomada

Saldos comerciais ficam separados por jogador/Emerald/nível. Somente o maior nível com saldo positivo consome tempo. Recompra soma 30 dias no nível comprado, mesmo se pausado. Comprar VIP 3 durante VIP 1 preserva o saldo restante do VIP 1; ao terminar o VIP 3, o VIP 1 retoma desse saldo. VIP 2 pode entrar entre eles. Reconciliação atravessa múltiplas expirações durante indisponibilidade/offline, com precisão de milissegundos e sem ganhar tempo por relógio retroceder.

RankService une o nível comercial vigente aos ranks manuais existentes. Staff e atribuições manuais não são rebaixados nem reescritos pelo ledger. Kits, homes, claims, RTP, ec, fly e apresentação que usam RankService recebem o benefício vigente. Cache comercial tem validade de cinco segundos, calcula expiração a cada consulta, é invalidado na concessão/login e não conserva nível expirado. Um serviço remove voo comercial sem permissão em até um segundo, preservando Creative/Spectator e permissões de staff/manuais. Apresentação usa sincronização de ranks existente. Nenhum cooldown, home ou claim é apagado; limites existentes passam a bloquear novos excedentes.

## Transporte e separação de ambientes

Canal de entrega: https://127.0.0.1:4202, serviço de usuário atlas-api-core-tls. Somente caminhos internos tipados são encaminhados ao backend loopback 8080. Certificado com SAN 127.0.0.1 é confiado explicitamente pelo HttpClient Core; redirects não são seguidos. Chave existente do Core é enviada no header, comparada em tempo constante, e rotas exigem origem loopback. Arquivos privados ficam fora do Git. Certificado tem validade de 365 dias e precisa de renovação operacional antes de vencer.

O gateway público 4201 continua expondo somente /api/v1; /internal retorna 404 na internet. Não existe DNS/túnel público para 4202. O serviço HTTPS é habilitado para iniciar com a VM. Vinculação /site mantém seu transporte loopback anterior, sem alterar essa integração.

ATLAS_DELIVERY_ENABLED=true, ATLAS_DELIVERY_MODE=production; ATLAS_SALES_ENABLED=false. Claim filtra o ambiente da tentativa de pagamento. Core instalado também recusa mode=test. Os pagamentos e fixtures fictícias de homologação não concedem VIP aos jogadores reais. Habilitar pagamentos de teste não habilita vendas nem altera o ambiente do consumidor de entrega.

## Contratos

| Rota | Acesso | Comportamento |
|---|---|---|
| POST /internal/v1/deliveries/claim | Chave Core + loopback | Body server=emerald; até dez entregas por lease |
| POST /internal/v1/deliveries/{id}/ack | Chave Core + loopback | Lease token, recibo imutável e saldo/checkpoint |
| POST /internal/v1/deliveries/{id}/failed | Chave Core + loopback | Falha transitória ou divergência para revisão |
| POST /internal/v1/vip/statuses | Chave Core + loopback | Até cem espelhos; checkpoint antigo não regride estado |
| GET /api/v1/users/me/vip | Sessão própria | Nível comercial atual, activeUntil, saldos pausados e vínculo |
| GET /api/v1/admin/deliveries?page=0 | ADMIN | Tentativas, prazo, falha e próxima execução; paginação |
| POST /api/v1/admin/deliveries/{id}/retry | ADMIN + CSRF | Justificativa de 10–500 caracteres; mesmo delivery_id |

Minha conta mostra VIP atual e saldos pausados e atualiza a cada 30 segundos. Administração mostra tentativas e justificativa para reprocessar. Status da compra DELIVERED depende do ACK persistido; voltar do checkout não entrega VIP. Espelho do site não é autoridade de permissões no Minecraft.

## Migrações, validação e instalação

V8__vip_deliveries.sql amplia somente o banco dedicado da API. database/migrations/034_commercial_vip_ledger.sql cria duas tabelas Core e permissões, sem converter/apagar registros históricos de VIP, ranks ou jogadores.

Validações realizadas:

- 77 testes API/PostgreSQL, incluindo concorrência de claims, lease expirada, ACK divergente, pagamento reembolsado, ambiente diferente, limite/reprocessamento auditado, espelho monotônico e rollback do ACK com replay.
- 38 testes Playwright, incluindo nível atual/saldo pausado, retomada na tela e reprocessamento administrativo com justificativa.
- Gradle build do Core e teste determinístico de pausa, retomada, recompra, múltiplas expirações offline e limite exato de prazo.
- Repositório Core real em cluster descartável: dois workers, commit antes de ACK, jogador offline, identidade/payload divergentes e falha de recibo com rollback.
- API pública respondeu 0.6.0/schema 8; HTTPS privado autenticado respondeu e rotas internas públicas retornaram 404.

Scripts: verify-local.py, verify-vip-core.py e deploy-m6-local.py em atlas-api/scripts. Backup privado de env, JARs e ambos os bancos preservado em .runtime/backups/before-m6-*. Código Core foi compilado em worktree isolado para não incluir alterações locais de NPC/RTP alheias ao M6. Há exatamente um atlas-core JAR ativo na pasta de mods.

O comando systemctl restart exigiu autenticação interativa. Como o Java Minecraft pertence ao usuário e Restart=always já estava configurado, a reinicialização foi realizada com SIGTERM normal, preservando o salvamento dos mundos. Novo PID ativo, Done no startup, atlas-core 1.30.0 carregado e consumidor HTTPS de produção iniciado. Logs de mods externos contêm avisos/erros; não foram detectadas falhas do novo módulo VIP.

Frontend commit 5701fd2 publicado automaticamente, deploy Pages ccf2d587-dc71-4e63-b7ed-6e49442e20a7 concluído. Nenhum plano pago foi contratado.

## Pendências antes de abrir vendas

Concluir cenários externos M5 (cartão recusado, PIX, expiração e compensação), confirmar regras/benefícios em jogo e validar autostart em reinício integral da VM. M7 deve completar monitoramento, restauração, incidentes e operação. Não alterar ATLAS_SALES_ENABLED nem credenciais para produção somente porque M6 foi instalado.

## Homologação em jogo — 04/10/2026

VFSomente teve DONO retirado para verificar permissões. Sem cargos, o jogador confirmou bloqueio de kit VIP e fly. Com VIP 1 manual, resgatou kit VIP, teve kit VIP 2 negado e ativou fly. Com VIP 3 manual, resgatou kits dos níveis 2/3 e manteve cooldown do nível 1. Cargos temporários foram removidos; o jogador confirmou bloqueio de kit VIP e fly. Após instalar 1.30.1, /clear também ficou indisponível à conta sem cargos. Esses testes de ranks manuais não comprovam entrega comercial, pausa/retomada ou expiração de saldo.

Core 1.30.1 restringe /clear a ADM/ADMIN e DONO/OWNER, inclusive para jogadores OP. Core 1.30.2 adiciona /vip para consultar somente o próprio saldo comercial, nível ativo, término e níveis pausados. O comando não considera ranks manuais como compra. ADMIN do site não foi alterado durante os testes.
