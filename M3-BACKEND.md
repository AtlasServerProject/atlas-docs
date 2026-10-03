# M3 — Catálogo e promoções reais

API `0.3.0`, migrations V3/V4; marco comercial sem liberação de vendas. Conta e emails do M2 permanecem integrados ao Netlify por HTTPS gratuito. Nenhuma alteração no Core ou banco Minecraft.

## Funcionamento

Os três VIPs têm seeds versionados: 2500, 3500 e 5000 centavos, duração de 30 dias, destino Emerald. Categorias únicas: VIPs, Chaves, Pacotes e Cosméticos. Catálogo público inclui somente produto/oferta/servidor ativos. Produtos podem aparecer como prévia, mas `purchasable=false` é obrigatório no banco neste marco. O site não permite compra simulada pelo catálogo real.

CRUD administrativo cria/edita/desativa produtos e a oferta Emerald. Não apaga registros históricos. Toda alteração usa revisão otimista, transação, versão do produto e auditoria com UUID do ator, requestId gerado no backend, antes/depois e horário. Slug duplicado, promoção sobreposta e revisão desatualizada recebem 409. USER não pode alterar catálogo, mesmo com modo ADMIN ou dados adulterados no navegador.

Preço em BRL é inteiro em centavos, entre 1 e 100000000. Promoção recebe preço final **ou** desconto em pontos-base (100 = 1%). O backend calcula o resultado com HALF_UP no centavo, exige preço positivo inferior ao base e usa um snapshot do preço base na promoção. Preço base não pode cair abaixo de uma promoção ainda válida: encerrá-la ou ajustá-la primeiro. Mudança de preço base posterior não recalcula o valor final da promoção já cadastrada.

Promoções usam intervalo `[startsAt, endsAt)` e relógio UTC da API. O começo é inclusivo e o término exclusivo. CANCELLED/FINISHED manual prevalece; promoções encerradas não são reabertas. Estados efetivos e preço final são calculados na leitura, sem depender de cron/job ou de navegador aberto. Um trigger PostgreSQL bloqueia a linha do produto e rejeita sobreposição inclusive em gravações concorrentes ou SQL direto. Intervalos adjacentes são permitidos.

Resposta pública inclui serverTime, revisão global, revisões individuais, preços base/final e promoção vigente. A leitura transacional REPEATABLE READ mantém o snapshot coerente. Sem cache de preços ou autorização; respostas no-store.

## Angular

ProductService e PromotionService usam HttpClient; armazenamento local não decide catálogo. Apenas conteúdo visual dos kits continua estático. Estados de atualização, erro e retry são exibidos. Após salvar, a API é reconsultada. Em 409, o formulário permanece aberto com seus valores e pede atualização explícita da revisão antes de tentar novamente.

Countdown usa diferença entre relógio do navegador e serverTime, compensando aproximadamente latência de rede. Reconsulta no início/término e ao voltar à aba; há atualização periódica de 15 segundos. O cronômetro apenas exibe tempo: a vigência e os preços continuam determinados pela API. Página administrativa cria/edita produtos, ativa/desativa Emerald, edita preços e cria/edita/encerra/cancela promoções.

## Contrato

[OpenAPI M3](api/openapi-m3.json). GET `/api/v1/catalog` é público. Todas as rotas `/api/v1/admin/*` exigem ADMIN; POST/PATCH exigem sessão e CSRF obtido por GET `/api/v1/auth/csrf`.

| Rota | Uso |
| --- | --- |
| GET `/admin/catalog` | Catálogo completo, incluindo inativos e promoções encerradas |
| POST `/admin/products` | Criar produto e oferta Emerald, revisão zero |
| PATCH `/admin/products/{id}` | Editar metadados/preço e visibilidade com revisão |
| PATCH `/admin/products/{id}/price` | Editar preço com revisão |
| PATCH `/admin/products/{id}/offer` | Ativar/desativar visibilidade Emerald com revisão |
| POST `/admin/promotions` | Criar promoção, revisão zero e productRevision atual |
| PATCH `/admin/promotions/{id}` | Editar com revisão da promoção e do produto |
| PATCH `/admin/promotions/{id}/status` | CANCELLED ou FINISHED com revisão |

IDs comerciais são inteiros restritos ao intervalo seguro do JavaScript. Não há checkout, cobrança, entrega ou alteração automática de conta Minecraft neste marco. Oferta vendável requer migration e marcos posteriores.

## ADMIN e operação

Primeiro ADMIN solicitado: nickname VFSomente, email vfsomente@gmail.com. Conceder somente depois de encontrar a conta confirmada correspondente e registrar concessão pelo script operacional do M2. Não criar senha nem conceder ADMIN ao amigo cadastrado.

Antes de aplicar migrations ao ambiente persistente, preservar dump privado e JAR anterior. Executar `python3 scripts/verify-local.py --web-tests` em banco descartável. Publicar frontend após a atualização da API e verificar catálogo/saúde no endereço público. Segredos e backups ficam fora do Git.

Referências: [locks de linhas PostgreSQL](https://www.postgresql.org/docs/current/explicit-locking.html) e [visibilidade em triggers](https://www.postgresql.org/docs/current/trigger-datachanges.html).

Validação: 26 testes Java/PostgreSQL e 34 testes Playwright aprovados. A migração V3 de um build intermediário havia sido aplicada durante teste operacional de reinício; seu conteúdo foi preservado, e a correção de duração exclusiva de VIP entrou em V4 incremental, sem repair do histórico e sem apagar contas.
