# Cloudflare — migração do Atlas

03/10/2026. Frontend publicado em `https://atlas-cobblemon.pages.dev`, com integração GitHub ativa; domínio e API pública aguardam propagação DNS. Domínio comprado pelo dono: `atlascobblemon.com.br`. DNS configurado no Registro.br para `brady.ns.cloudflare.com` e `faye.ns.cloudflare.com`; aguardar status Active na Cloudflare. Não substituir esses nameservers por IPs do servidor.

## Arquitetura preparada

- Frontend Angular no Cloudflare Pages, com o repositório `AtlasServerProject/atlas-web`.
- API e PostgreSQL continuam na VM. Nenhuma conta, vínculo Minecraft, pedido ou senha é transferido para Pages.
- Domínio principal e `www` apontam para o projeto Pages. `api.atlascobblemon.com.br` usa um túnel permanente com aplicação publicada para `http://127.0.0.1:4201`.
- O gateway 4201 expõe somente `/api/v1/`; não usar 8080 como destino público. Core proofs/internal e actuator não são expostos pelo gateway.
- O frontend continua usando `/api/v1/` no mesmo domínio. Um Pages Worker encaminha apenas essas chamadas ao hostname fixo da API e preserva cookies de sessão, CSRF e assinaturas de webhook. Credenciais não ficam no frontend.
- Assets estáticos não invocam Functions; rotas API têm cache desativado. API indisponível retorna erro recuperável, enquanto loja e páginas estáticas permanecem disponíveis.
- A VM ligada e com internet continua sendo requisito para cadastro/login/pagamentos. Não há promessa de hospedagem gratuita irrestrita: Pages/Functions têm limites próprios.

## Build e validação prontos

```bash
cd /home/somente/dev/atlas/atlas-web
npm ci
npm run test:hosting
npm run build:pages
```

Saída: `dist/atlas-web/browser`. Build Pages gera `_worker.js` e `_routes.json`, remove o `_redirects` específico do Netlify somente da saída e usa o fallback SPA padrão de Pages. O arquivo fonte Netlify é preservado para a versão anterior. O Node recomendado é 24.21.0. `wrangler.jsonc` fixa a configuração e `wrangler` está versionado em 4.147.0.

O workflow hosting-check verifica o proxy e compila a saída em pushes/PRs. Os testes cobrem sessão/Set-Cookie, corpo, CSRF, assinatura do Mercado Pago, ausência de cache, destino fixo, redirects externos, limite de tamanho e indisponibilidade. Prévia real do Wrangler também deve confirmar rotas Angular e assets antes de publicar.

## Acesso à conta autorizado

A conta foi autorizada pelo dono via OAuth Device Grant em 03/10/2026. O acesso da VM está confirmado; não reenviar credenciais nem repetir login enquanto a sessão for válida. Para renovar a autorização pelo navegador quando necessário:

```bash
cd /home/somente/dev/atlas/atlas-web
npx wrangler login
```

Se o navegador estiver fora da VM, encaminhar a porta local 8976 pelo VS Code/SSH para que o retorno OAuth alcance o terminal que iniciou o login. Não enviar senha/token pelo chat. Os arquivos de credenciais do Wrangler não devem entrar no Git.

## Criar Pages com publicação automática

No painel Cloudflare: Workers & Pages → criar aplicação → Pages → conectar GitHub. Autorizar acesso ao repositório `AtlasServerProject/atlas-web` e selecionar:

- Nome do projeto: `atlas-cobblemon`, se disponível; se mudar, ajustar `name` em `wrangler.jsonc`.
- Branch de produção: `main`.
- Diretório raiz: raiz do repositório atlas-web.
- Build: `npm run build:pages`.
- Saída: `dist/atlas-web/browser`.
- Variável de build `NODE_VERSION`: `24.21.0`.

Escolher integração Git desde a criação para publicação automática. Projetos criados por Direct Upload não podem ser convertidos para a integração Git nativa. Depois da primeira publicação, associar `atlascobblemon.com.br` e `www.atlascobblemon.com.br` em Custom domains do Pages, antes de criar CNAME manualmente.

## Túnel permanente e início com a VM

Criar um túnel gerenciado remotamente na mesma conta Cloudflare. Publicar o hostname `api.atlascobblemon.com.br` com destino HTTP `127.0.0.1:4201`. Copiar somente o token para o arquivo privado abaixo, sem colocá-lo em documentação, comandos de shell ou conversa:

`/home/somente/dev/atlas/atlas-api/.runtime/cloudflare-tunnel.token`

Permissões 0600; pasta runtime 0700. O template `infra/templates/atlas-api-cloudflare.service` usa `--token-file`, requer o gateway da API e reinicia em falhas. Não armazena token no comando ExecStart nem em arquivo versionado. Não há mudança no Core/Minecraft nem no Playit nesta migração.

Depois de Pages/DNS/token prontos:

```bash
cd /home/somente/dev/atlas
python3 infra/scripts/activate-cloudflare.py
```

O script verifica precondições, preserva backup privado de `.env`/config, configura links de email e CORS por arquivo Spring externo e atualiza a URL de webhook para o novo domínio. Preserva flags de vendas/pagamentos, tokens e banco. Instala/habilita o novo serviço e consulta a API pelo frontend público. Somente após validação positiva desativa o túnel temporário e o timer que republicava no Netlify.

Se a validação falhar, o túnel anterior permanece ativo e o backup fica em `.runtime/backups/before-cloudflare-*`. A configuração da API pode já ter sido alterada: revisar DNS/túnel/Pages ou restaurar o `.env` privado e reiniciar `atlas-api`. Não alterar migrations para desfazer uma configuração de hospedagem.

## Teste público após ativação

- Abrir loja, login e Minha conta no domínio com HTTPS.
- Login de conta existente, geração/comprovação do código Minecraft e histórico de compras.
- Recuperação/novo cadastro: email deve apontar ao novo domínio. Links antigos já enviados continuam apontando ao hostname anterior; reenviar quando necessário.
- Reiniciar túnel e API, confirmar o mesmo endereço público e os mesmos dados.
- Validar autostart em reinício integral da VM antes de declarar operação homologada.
- Atualizar a configuração de Webhooks no painel Mercado Pago; homologação M5 e entrega M6 continuam pendentes.

## Fontes oficiais

- [Pages: Angular](https://developers.cloudflare.com/pages/framework-guides/deploy-an-angular-site/)
- [Worker em modo avançado](https://developers.cloudflare.com/pages/functions/advanced-mode/)
- [Roteamento de Functions](https://developers.cloudflare.com/pages/functions/routing/)
- [Integração Git](https://developers.cloudflare.com/pages/configuration/git-integration/)
- [Domínios personalizados](https://developers.cloudflare.com/pages/configuration/custom-domains/)
- [Token e parâmetros do túnel](https://developers.cloudflare.com/tunnel/reference/run-parameters/)

Validação local concluída: sete testes do proxy aprovados, build Angular/Pages aprovado e prévia real do Wrangler conferida com Playwright (rotas diretas, JavaScript servido corretamente, layout móvel e API indisponível retornando 503). A consulta DNS desta execução ainda retornou os nameservers anteriores do Registro.br. Nenhum serviço permanente foi ativado sem token/autorização.

## Avanço após autorização da conta

Túnel remoto `atlas-api` criado e configurado para `api.atlascobblemon.com.br` → `http://127.0.0.1:4201`. Token salvo somente no arquivo privado de runtime (0600). Serviço `atlas-api-cloudflare` instalado, ativo e habilitado para iniciar com a VM. O túnel temporário anterior e sua configuração foram preservados até validação pública.

Após autorização GitHub, o projeto Pages `atlas-cobblemon` foi criado com integração nativa ao repositório e branch main. O projeto Workers `atlas-web` criado inicialmente foi preservado. Primeira publicação de produção concluída com sucesso: `86d5206c-66d9-4a5a-a0b7-196d4b74fadd`. Home e /login retornaram HTTP 200; API retornou 503 enquanto seu hostname não resolve publicamente.

DNS da API criado pelo dono e confirmado no servidor autoritativo Cloudflare: CNAME `api` → `ff6c623c-1ce6-4051-a734-104e58c7ce39.cfargotunnel.com`. A delegação pública ainda aponta aos nameservers antigos do Registro.br. OAuth da VM não permite editar DNS (HTTP 403).

Domínios principal e www já associados ao Pages. Ainda precisam dos registros CNAME `@` → `atlas-cobblemon.pages.dev` e `www` → `atlas-cobblemon.pages.dev`, com proxy ativado e TTL automático. Configuração de emails/CORS e desativação do túnel anterior aguardam validação pública.

O primeiro build automático usou Node 22.16.0, incompatível com Angular. Arquivo `.node-version` fixa Node 24.21.0 para os próximos builds.

Deploy automático pelo GitHub validado com sucesso após fixar Node: `f09b91e3-aa9d-4c07-b38a-71c88073bf8b`, commit `370a21c`. Home, loja e login públicos também conferidos em navegador móvel (HTTP 200, renderização Angular e sem overflow horizontal).
