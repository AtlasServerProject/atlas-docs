# M5 — Pagamentos Mercado Pago

03/10/2026. API 0.5.0, schema 7. Implementação local de Checkout Pro via Preferences API; homologação externa pendente de credenciais. Vendas e pagamentos permanecem desativados na VM. Entrega de VIP depende do M6.

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
ATLAS_MP_NOTIFICATION_URL=https://atlas-cobblemon.netlify.app/api/v1/webhooks/mercadopago
ATLAS_SALES_ENABLED=false
```

- ACCESS_TOKEN: credencial da integração/conta de teste compatível com Checkout Pro.
- WEBHOOK_SECRET: assinatura secreta mostrada na configuração de Webhooks da aplicação.
- COLLECTOR_ID: User ID do recebedor associado ao token, não o número da aplicação nem o comprador.
- No painel de Webhooks, cadastrar a URL acima em teste e selecionar pagamentos. O hostname do túnel gratuito não é usado nessa configuração; o proxy Netlify permanece estável.
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
