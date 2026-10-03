# M4 — Identidade Minecraft e pedidos

API 0.4.1, migration V5; Core 1.29.24, migration de jogo 033. Vendas permanecem fechadas. Pagamento, entrega e contagem de VIP pertencem ao M5/M6.

## Vínculo

Conta web confirmada gera código aleatório de 256 bits, válido por 10 minutos. Somente SHA-256 persiste; o código é exibido uma vez. Gerar outro invalida desafios anteriores. O jogador autenticado executa `/site vincular <codigo>` no Emerald. O Core comprova sua identidade pela conexão interna local, e o site apresenta o nickname para confirmação explícita. Sem essa última confirmação, não há vínculo.

Conta e jogador têm política 1:1, protegida por índices únicos e locks transacionais. Código expirado, cancelado, consumido ou desconhecido não autoriza vínculo. Há limite persistente de 10 operações por conta/identidade a cada 15 minutos e intervalo de 10 segundos no comando. Código não deve ser compartilhado.

A identidade usada pelo site é `site_identities.subject`, UUID aleatório com referência única ao `players.id` canônico no banco do Core. Promoção Premium que apenas atualiza UUID preserva a referência. Na mescla com um player Premium existente, a referência acompanha o player canônico na mesma transação, antes da exclusão do Offline. Se ambos já possuem identidades de site distintas, a mescla inteira é revertida e exige revisão operacional: nenhuma conta web é fundida automaticamente. Trocar nickname não altera destinatário. `corePlayerId`, UUID Minecraft e nickname no pedido são snapshots; a entrega futura deve resolver **subject** no Core, nunca confiar no nickname ou no antigo número de player.

Desvinculação exige senha atual da conta web, mantém registro histórico e invalida desafios pendentes. O novo vínculo precisa de novo código, nova comprovação no jogo e confirmação web. Pedidos anteriores mantêm a identidade original.

## Segurança da ponte

POST `/internal/v1/minecraft/proofs` aceita somente origem loopback e chave privada de pelo menos 256 bits, comparada em tempo constante. Não usa sessão web ou CSRF; esses continuam obrigatórios nas operações do usuário. O gateway público expõe somente `/api/v1/*` e não encaminha a rota interna. A ponte desta instalação comunica-se somente com `http://127.0.0.1:8080`; não suporta Core remoto sem revisão de transporte/autenticação.

Chave compartilhada fica em `atlas-api/.env` (`ATLAS_CORE_KEY`) e no arquivo privado `config/atlas-site.properties` da instalação do servidor (`api-url` e `key`). Não vai ao Git ou ao frontend. Ausência/invalidez desativa a ponte. Comando exige sessão do jogo autenticada e dimensão Emerald/survival Emerald/Nether/End, consultando identidade no Repository. HTTP roda em executor limitado, sem bloquear tick; SQL permanece no Repository e no thread do servidor. Erros não registram chave, código ou corpo HTTP.

## Pedidos

Checkout exige usuário autenticado, email confirmado, vínculo, produto VIP ativo, oferta Emerald ativa e elegível. Quantidade fixa em 1 período de 30 dias por pedido. Preço é calculado novamente no backend, incluindo promoção efetiva no intervalo `[início,fim)`. Revisão do produto, revisão do catálogo e valor esperado devem corresponder à confirmação do usuário; divergência recebe 409 e exige revisão do preço.

Cabeçalho `Idempotency-Key` tem 16–100 caracteres alfanuméricos, `_` ou `-`. Mesma conta + chave + corpo retorna o mesmo pedido, inclusive após retry/revínculo. Corpo diferente recebe 409. Locks de conta e unicidade no banco impedem pedidos duplicados por concorrência. Snapshot registra produto, valor em centavos BRL, duração, promoção/revisões e identidade do destinatário. Prazo inicial do pedido: 30 minutos; não inicia duração do VIP. `PENDING` vencido aparece como `EXPIRED`, sem perder o histórico; confirmação de dinheiro tardio será reconciliada no M5.

Vendas precisam de **duas condições**: `ATLAS_SALES_ENABLED=true` e oferta `purchasable=true`. Ambas continuam desabilitadas na instalação pública. Não há controle administrativo para abrir vendas neste marco. Testes usam ofertas descartáveis e ativação restrita ao contexto de teste.

Listagem paginada (20 por página) e detalhe filtram pelo dono, inclusive para ADMIN. Pagamento e entrega têm estados separados. Um evento auditável é criado junto com cada pedido; criação não chama gateway nem entrega benefícios.

## Frontend

Minha conta permite gerar/copiar comando, consultar comprovação, confirmar nickname e desvincular com senha. A consulta atualiza a cada 5 segundos enquanto há desafio pendente. Sair/trocar conta limpa estado local. Minhas compras usa pedidos reais, estados separados e paginação; dados mock antigos não aparecem. Confirmação do pedido mostra preço e jogador, mantém idempotência nos retries e exige novo valor/chave ao revisar a cotação.

## Endpoints

| Método e rota | Contrato |
| --- | --- |
| GET `/api/v1/users/me/minecraft-link` | `current` + `pending`; nunca retorna código/hash |
| POST `/api/v1/users/me/minecraft-link-challenges` | Retorna `id`, `code`, `expiresAt` uma vez |
| POST `/api/v1/users/me/minecraft-link-confirmations` | `challengeId`, `subject` previamente comprovados |
| POST `/api/v1/users/me/minecraft-unlink` | Senha atual; não altera pedidos |
| POST `/internal/v1/minecraft/proofs` | Chave privada; código e identidade canônica enviados pelo Core |
| POST `/api/v1/orders/checkout` | Chave idempotente; produto, servidor, quantidade, revisões e valor esperado |
| GET `/api/v1/orders?page=0` | `items`, `page`, `size`, `hasNext` |
| GET `/api/v1/orders/{uuid}` | Pedido do dono ou 404 |

## Instalação e validação

Preservar dump privado de ambos os bancos, JARs anteriores e frontend publicado. Validar `python3 atlas-api/scripts/verify-local.py --core-tests --web-tests` e `./gradlew build` no Core. O teste de identidade usa banco descartável separado e o código real dos repositories; não acessa o banco do jogo.

Aplicar migration 033 antes de instalar o Core, pois a mescla Premium passa a participar da proteção de identidade. Instalar apenas um JAR de Core; reiniciar e revisar inicialização. API aplica V5 por Flyway, sem editar V1–V4. Voltar para API anterior mantém schema aditivo; não executar down migration ou apagar contas/pedidos.

Validação concluída: 39 testes API/PostgreSQL, testes dos repositories reais do Core (nickname, Premium, mescla e rollback) e 35 testes Playwright, incluindo comprovação interna e confirmação web reais em banco descartável. Checkout no navegador usa injeção controlada de falhas/cotação; idempotência e preços têm testes transacionais reais separados. Builds API/Angular/Core aprovados. API 0.4.1 publicada, schema 5 aplicado, frontend no Netlify, migration 033 aplicada ao Core e 1.29.24 instalado com um único JAR. Serviço ativo, inicialização concluída e ponte configurada, sem erro de Site. Teste manual do comando pelo jogador no cliente Minecraft permanece parte da homologação; nenhuma compra ou entrega foi liberada.

Patch 0.4.1: criação de pedidos normaliza horários para microssegundos antes da persistência, alinhando prazo informado e limite real armazenado pelo PostgreSQL. Evita divergência de estado na borda exata da expiração.
