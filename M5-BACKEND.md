# M5 — Pagamentos Mercado Pago

03/10/2026. API 0.5.0, schema 7. Implementação local de Checkout Pro via Preferences API; homologação externa pendente de credenciais. Vendas permanecem desativadas na VM; processamento de pagamentos habilitado somente em modo test após validação das credenciais. Entrega de VIP depende do M6.

O dono confirmou o vínculo Minecraft de VFSomente, Principelothric e Pablix026 em jogo. Isso fecha a validação manual do comando prevista no M4; não altera permissões dessas contas.

## Fluxo implementado

1. O M4 cria um pedido com cotação e destinatário imutáveis. O usuário inicia o pagamento em Minhas compras por POST `/api/v1/orders/{id}/payment`, com sessão, CSRF e limite de tentativas.
2. Uma tentativa única por pedido é gravada e confirmada no banco antes da chamada externa. O preço e a referência vêm do pedido persistido. PIX e cartão são oferecidos pelo checkout hospedado; boleto é excluído e cartão fica limitado a uma parcela. A disponibilidade efetiva de PIX deve ser homologada na conta brasileira escolhida.
3. O backend cria a preferência no Mercado Pago e entrega somente a URL HTTPS autorizada, usando sandbox_init_point em teste e init_point em produção. Cartão, CPF e credenciais do comprador não são coletados pelo Atlas.
4. O retorno ao site mostra o estado consultado na API. Parâmetros de URL nunca aprovam um pedido. O usuário pode atualizar o status e retomar a mesma preferência dentro do prazo do pedido.
5. POST `/api/v1/webhooks/mercadopago?data.id=ID&type=payment` recebe notificações públicas. HMAC-SHA256 de x-signature, x-request-id e data.id é verificado em tempo constante. Essa rota tem exceção específica de CSRF, não há exceção para pagamentos autenticados.
6. Apenas o identificador de pagamento autenticado entra na fila; o corpo externo não determina o valor ou a aprovação. O recebimento e a deduplicação são transacionais antes do HTTP 200. Falha de armazenamento não confirma recebimento. Não é aplicado limite de idade à assinatura, pois retries do gateway podem chegar dias depois; repetir uma assinatura só solicita a consulta autenticada ao provedor.
7. Workers usam lease, SKIP LOCKED, geração e token para processar com retry. Notificações que chegam durante processamento continuam pendentes. O pagamento é consultado fora da transação; referência, recebedor, ambiente, valor inteiro em centavos, moeda e aprovação são conferidos antes de qualquer entrega.
8. Aprovação válida muda o pedido para PAID/PROCESSING e insere uma obrigação única em delivery_outbox na mesma transação. Rollback/retry não duplicam essa obrigação. A fila ainda não aplica VIP no Core.

## Incerteza, reconciliação e compensação

- Timeout ou falha ao persistir a preferência deixa CREATING/UNKNOWN. O sistema não faz outro POST de criação automaticamente, mesmo enviando X-Idempotency-Key: não depende de uma garantia de idempotência de preferências não homologada. O usuário consulta o mesmo pedido; uma tentativa sem preferência recuperada exige análise operacional. Não orientar a criar outro pedido enquanto houver resultado incerto.
- A reconciliação pesquisa pagamentos pela external_reference a cada minuto, inclusive pagamentos aprovados para detectar estorno/contestação posterior. As 20 tentativas menos recentemente verificadas são processadas por ciclo. Resultados encontrados voltam à consulta individual autenticada. Pesquisa com mais de 100 resultados falha para análise, sem conceder benefícios.
- Webhook tardio com aprovação dentro do prazo do pedido pode confirmar a compra mesmo após a expiração local. Aprovação após o prazo, data ausente ou inválida registra PAID/REVIEW, sem criar entrega automática.
- Estorno total, parcial ou chargeback registra análise de compensação e segura qualquer obrigação ainda aguardando entrega. Entrega realizada permanece registrada. Remoção/compensação de benefícios exige M6 e operação M7.
- Segundo pagamento aprovado do mesmo pedido entra em revisão; continua existindo uma única obrigação. Estorno do segundo pagamento não regride a compra original.
- Eventos antigos e estados pending/rejected/cancelled não regridem PAID, REFUNDED ou CHARGEBACK. Uma tentativa recusada não encerra a preferência: o cliente pode tentar novamente no checkout; o pedido permanece aguardando pagamento até aprovação ou expiração.
- Os registros operacionais ficam em payment_reviews, payment_observations e order_events. Painel de atendimento e alertas são M7.

## Configuração privada pendente

No `.env` ignorado da API foram preparados os campos abaixo; preencher somente os três valores privados após identificar corretamente a conta de teste:

```dotenv
ATLAS_PAYMENT_ENABLED=false
ATLAS_MP_MODE=test
ATLAS_MP_ACCESS_TOKEN=
ATLAS_MP_WEBHOOK_SECRET=
ATLAS_MP_COLLECTOR_ID=
ATLAS_MP_NOTIFICATION_URL=https://www.atlascobblemon.com.br/api/v1/webhooks/mercadopago
ATLAS_SALES_ENABLED=false
```

- ACCESS_TOKEN: credencial da integração/conta de teste compatível com Checkout Pro.
- WEBHOOK_SECRET: assinatura secreta mostrada na configuração de Webhooks da aplicação.
- COLLECTOR_ID: User ID do recebedor associado ao token, não o número da aplicação nem o comprador.
- No painel de Webhooks, cadastrar a URL acima em teste e selecionar pagamentos. O hostname do túnel gratuito não é usado nessa configuração; o proxy Cloudflare Pages usa o domínio definitivo.
- Public Key não é necessária para este redirecionamento hospedado sem SDK de cartão no frontend.
- Nunca enviar esses valores pelo chat, colocar no frontend ou versionar `.env`. Credenciais de produção e teste precisam de ambientes separados. O flag mode não converte uma credencial real em credencial de teste; confirmar origem antes de habilitar.

## Homologação externa para fechar M5

- [ ] Identificar credenciais e recebedor de teste; validar resposta de conta e ambiente com o provedor.
- [ ] Abrir preferência de cartão e PIX usando comprador de teste, em janela anônima.
- [ ] Validar cartão aprovado, recusado e pendente; PIX pendente e expiração.
- [ ] Simular notificações pelo painel e conferir assinatura, retries e fila persistente. A documentação informa que pagamentos com credenciais de teste podem não emitir webhooks; nesses casos testar o receiver pelo painel e a confirmação por reconciliação.
- [ ] Confirmar um pagamento de teste sem evento e depois após reinício da API.
- [ ] Conferir compensação após reembolso/contestação no ambiente suportado.
- [ ] Verificar método PIX habilitado e comportamento do prazo antes de abrir vendas.
- [ ] Completar M6/M7; liberar produção apenas com entrega e operação homologadas.

## Validação e instalação

Testes usam PostgreSQL descartável e um provedor substituído por fixtures: nenhuma cobrança ou email de usuário real. A suite cobre assinatura inválida/deduplicação, valores/recebedor/ambiente divergentes, eventos fora de ordem, timeout, webhook perdido, retorno manipulado, lease, concorrência, falha transacional na outbox e URLs de redirect. O adaptador HTTP também é exercitado com respostas compatíveis com a API, parsing de valores/datas e erros sem exposição de token.

Executar `python3 atlas-api/scripts/verify-local.py --web-tests`; o frontend inclui um teste M5 com checkout externo interceptado, estados consultados e retorno manipulado. `scripts/deploy-m5-local.py` preserva backup privado de banco/env/JAR, instala uma cópia versionada e aplica V7. Essa instalação não reinicia o Minecraft nem habilita vendas/pagamentos. Publicar no Netlify a cópia do build validado e atualizar o snapshot congelado usado pelo timer do túnel.

## Fontes oficiais consultadas

- [Checkout Pro via Preferences](https://www.mercadopago.com.br/developers/pt/reference/online-payments/checkout-pro-preferences/overview)
- [Notificações, assinaturas e retries](https://www.mercadopago.com.br/developers/en/docs/checkout-pro-preferences/payment-notifications)
- [Validador oficial Java de assinatura](https://github.com/mercadopago/sdk-java/blob/master/src/main/java/com/mercadopago/webhook/WebhookSignatureValidator.java)
- [Comprador de teste](https://www.mercadopago.com.br/developers/en/docs/checkout-pro-preferences/integration-test/introduction)
- [Cartão e meios offline em teste](https://www.mercadopago.com.br/developers/en/docs/checkout-pro-preferences/integration-test/test-purchases)

## Resultado da entrega em 03/10/2026

API 0.5.0 instalada e confirmada localmente com schema 7; backup privado preservado. 66 testes API/PostgreSQL e 36 testes Playwright passaram; os dois workflows GitHub da API também passaram. Os três vínculos citados acima foram conferidos no banco ativo.

Publicação do frontend preparada, porém bloqueada pelo Netlify: a API respondeu HTTP 403 com a razão de créditos esgotados na conta gratuita. A última versão pública do frontend permanece no ar. O build M5 validado fica em `.runtime/published-web-m5-next` e `atlas-web/dist/atlas-web/browser`; o snapshot anterior foi preservado. Não foi contratada assinatura nem comprado crédito.

O hostname antigo do proxy público também está expirado: GET público `/api/v1/system` retornou HTTP 530 / Cloudflare 1016, enquanto a API local responde 0.5.0 e o túnel atual está ativo. O timer tenta publicar o endereço atual, mas recebe o mesmo bloqueio de créditos. Isso impede cadastro/login público enquanto não houver publicação do proxy atualizado. Não confundir esse problema de hospedagem com credenciais Mercado Pago: pagamentos seguem deliberadamente desativados.

Pendências para concluir a homologação: liberar publicação do Netlify dentro do orçamento autorizado ou definir outra hospedagem gratuita; publicar o frontend/proxy validado; preencher os três campos privados do Mercado Pago; testar o checkout externo. Não declarar o M5 homologado até fechar essas etapas.


## Retomada da homologação no domínio definitivo

Frontend M5 publicado no Cloudflare Pages e API permanente conectada. Os bloqueios de hospedagem Netlify descritos acima são históricos e foram resolvidos pela migração. Nesta revisão, os três campos privados Mercado Pago ainda estavam vazios; nenhuma chamada autenticada ou compra externa foi executada.

1. Em Suas integrações → Atlas Cobblemon → Credenciais de teste, salvar o Access Token somente em `atlas-api/.env`, campo `ATLAS_MP_ACCESS_TOKEN`.
2. Em Contas de teste, identificar o vendedor associado às credenciais e salvar seu User ID em `ATLAS_MP_COLLECTOR_ID`. Não usar o ID da aplicação nem o comprador. Criar/identificar uma conta comprador distinta para os testes.
3. Em Webhooks → ambiente de teste, selecionar pagamentos e cadastrar `https://www.atlascobblemon.com.br/api/v1/webhooks/mercadopago`. Salvar a assinatura secreta em `ATLAS_MP_WEBHOOK_SECRET`.
4. Manter modo test e flags de pagamento/vendas false até validar credenciais e definir a execução isolada da homologação. Não abrir vendas no banco público só para testar: a entrega VIP M6 ainda está pendente.
5. Validar recebedor/token, checkout, confirmação por webhook/reconciliação, duplicação e recuperação antes de declarar M5 homologado. PIX exige validação específica de disponibilidade no Checkout Pro e no ambiente escolhido.

Credenciais de teste Checkout Pro podem começar com APP_USR; o prefixo sozinho não comprova o ambiente. A documentação do provedor informa que o vendedor de teste e suas credenciais são criados junto à aplicação. Não publicar credenciais em screenshots, logs, Git ou chat.


## Credenciais validadas e receiver de teste ativado

03/10/2026: campos privados preenchidos pelo dono. GET autenticado /users/me no Mercado Pago aceitou o token, confirmou site MLB, tag test_user e ID igual ao recebedor configurado. Valores não foram exibidos nem versionados. Backup privado do env preservado antes de habilitar ATLAS_PAYMENT_ENABLED=true e ATLAS_MP_MODE=test; ATLAS_SALES_ENABLED=false mantido. API reiniciada e ativa.

Webhook público no domínio definitivo rejeitou POST sem assinatura com HTTP 401 / INVALID_WEBHOOK. Isso valida roteamento e rejeição de notificações não autenticadas, mas não comprova a assinatura secreta cadastrada: ainda é necessário simular evento pelo painel Mercado Pago e conferir recebimento/fila. Nenhuma compra foi feita; checkout e PIX/cartão ainda aguardam homologação externa. Não liberar vendas públicas para gerar pedido de teste: usar ambiente isolado na próxima etapa.


## Primeiro checkout externo de teste preparado

Webhook simulado pelo painel aceito com HTTP 200 e registrado no banco: payment_id 123456, uma entrada na tabela de recebimentos. Por ser identificador fictício, consulta autenticada ao provedor não confirma compra; fila permanece em retry. Isso validou assinatura e persistência do recebimento, sem validar aprovação.

`atlas-api/scripts/payment-sandbox.py` inicializa um cluster PostgreSQL próprio, porta aleatória em loopback, API 0.5.0 e fixtures fictícias de usuário/vínculo. Revalida vendedor brasileiro test_user e correspondência de collector antes de iniciar. Credenciais chegam somente pelo ambiente do processo e estado privado `.runtime/payment-sandbox` (diretório 0700, arquivos de configuração 0600); nenhum email SMTP é enviado. Vendas são habilitadas apenas neste processo isolado. O banco público permanece fechado para vendas.

Primeiro pedido VIP 1 de 2500 centavos criado pela API, e preferência real de teste criada com sucesso pelo adaptador Mercado Pago. Estado persistido READY/test, pedido PENDING/WAITING e zero obrigações de entrega. Link fornecido ao dono para pagamento manual com comprador/cartão de teste; ainda não pago nesta execução. Prazo do pedido: 03/10/2026 14:14:34 America/Fortaleza.

```bash
python3 atlas-api/scripts/payment-sandbox.py --status
python3 atlas-api/scripts/payment-sandbox.py --stop
```

O cluster/processo permanece disponível para conferir o pagamento após a ação do dono; --stop encerra somente o ambiente identificado e preserva evidências privadas. Não repetir criação enquanto existir estado privado: falha incerta precisa de inspeção, sem recriar preferência automaticamente. O retorno do checkout aponta ao site público, mas este pedido não aparecerá em Minhas compras de uma conta real porque pertence ao banco separado. A reconciliação do sandbox consulta o provedor a cada minuto; o webhook público pode receber o evento, porém não encontra este pedido em seu próprio banco e não gera entrega ali. Portanto a confirmação do pedido isolado será validada inicialmente por reconciliação, separadamente da validação do receiver público.


## Cartão aprovado e confirmação externa validada

03/10/2026: comprador concluiu o checkout com cartão fictício APRO, pagamento 181201673665 aprovado por 2500 centavos BRL. Consulta autenticada confirmou referência do pedido e recebedor. O provedor retornou live_mode=true mesmo para o vendedor autenticado com tag test_user; o bloqueio original encaminhou PAYMENT_MISMATCH para revisão.

Correção do adaptador: preservar live_mode bruto e acrescentar evidência verifiedTestCollector somente após GET autenticado /users/me confirmar tag test_user e ID correspondente simultaneamente ao collector configurado e ao pagamento. Nickname, email e corpo de webhook não são prova do ambiente. Em modo test, aceitar live_mode=false ou esse recebedor comprovadamente fictício; produção rejeita recebedor comprovadamente test_user. Falha de consulta da identidade não aprova a compra. Referência, moeda, valor, recebedor, modo da tentativa e prazo continuam validados.

67 testes API/PostgreSQL passaram, incluindo recebedor fictício com live_mode=true, recebedor real e ID divergente. Smoke tests confirmaram persistência após reinício e falha/recuperação do banco. Sandbox reiniciado com o JAR corrigido; mesma notificação assinada do pagamento verdadeiro foi enviada duas vezes ao receiver isolado (200 em ambas). Resultado: PAID/PROCESSING, exatamente uma delivery_outbox, um evento PAYMENT_CONFIRMED, fila concluída e zero falhas. A revisão inicial permanece como evidência histórica; não houve exclusão manual ou aprovação forçada no banco.

Correção instalada também na API pública em `.runtime/releases/atlas-api-0.5.0-test-collector-fix.jar`, com backup privado de env/JAR/banco, sem mudanças de schema, credenciais ou flags comerciais. Health público confirmou 0.5.0/schema 7. Vendas continuam fechadas, pagamentos somente test. Não houve alteração do frontend.

Teste comprova criação de preferência, aprovação de cartão e confirmação/outbox no banco separado. Entrega efetiva VIP no Minecraft continua pendente do M6. Cartão recusado, PIX pendente/expiração, estornos e operação ainda precisam de homologação antes de abrir vendas; este resultado não fecha sozinho todo o M5.
