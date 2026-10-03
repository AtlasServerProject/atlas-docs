# Backend gratuito durante a construção

O site continua em https://atlas-cobblemon.netlify.app. As chamadas `/api/v1/` passam pelo proxy do Netlify, pelo HTTPS do Cloudflare Quick Tunnel e chegam à API da VM. O PostgreSQL permanece em `127.0.0.1:55432`; a API em `127.0.0.1:8080`. O gateway em `127.0.0.1:4201` aceita apenas rotas da API, sem publicar Actuator ou arquivos da VM.

Não foi contratado plano nem domínio. Esta configuração é para desenvolvimento: depende da VM ligada e conectada à internet. Quick Tunnel não garante disponibilidade, permite até 200 requisições simultâneas e troca o endereço ao iniciar um novo processo. Referência: https://developers.cloudflare.com/tunnel/get-started/quick-tunnels/.

## Serviços

- `atlas-api`: API e PostgreSQL dedicado persistente.
- `atlas-api-preview`: gateway restrito à API.
- `atlas-api-tunnel`: `cloudflared` com HTTPS público, transporte HTTP/2 e reinício em caso de falha.
- `atlas-api-tunnel-sync.timer`: verifica a cada 30 segundos se o endereço mudou. Se o túnel expira mesmo com o processo ativo, recria a conexão. Depois de três falhas de saúde com a API local saudável, também recria o túnel. Quando muda, publica novamente a última versão validada do frontend com o novo proxy. Usa a autenticação local existente do Netlify CLI. Não publica commits no GitHub automaticamente.

Templates ficam em `infra/templates/atlas-api-*.service` e `atlas-api-tunnel-sync.timer`. O checkout utilizado é `~/dev/atlas`; o binário Cloudflare é `~/.local/bin/cloudflared`. É necessário instalar o Netlify CLI, autenticar a conta e vincular `atlas-web` ao site Atlas. A sincronização usa a cópia validada em `atlas-api/.runtime/published-web`, evitando publicar trabalho ainda em construção. O Node é acessado por `~/.local/bin/node`, inclusive sem ambiente de terminal. Mudanças de endereço consomem publicações/créditos do plano gratuito do Netlify; não habilitar upgrade automático pago.

## Configuração privada

No `atlas-api/.env`, os valores públicos são `SPRING_PROFILES_ACTIVE=local,preview`, `ATLAS_WEB_URL=https://atlas-cobblemon.netlify.app` e `ATLAS_MAIL_MODE=smtp`. O perfil `preview` ativa cookie Secure e permite apenas a origem HTTPS do site. Senhas SMTP, senhas de banco e chave de criptografia permanecem no arquivo ignorado, com permissão `0600`.

Emails de confirmação e recuperação usam o Gmail configurado e links para o Netlify. O banco do jogo não participa desta configuração. Os limites atuais de autenticação são conservadores e compartilham o IP do proxy; revisar identificação de clientes e limites antes de abrir para tráfego amplo.

## Operação

```bash
systemctl --user status atlas-api atlas-api-preview atlas-api-tunnel atlas-api-tunnel-sync.timer
python3 ~/dev/atlas/infra/scripts/sync-api-tunnel.py
journalctl --user -u atlas-api-tunnel-sync.service --no-pager -n 20
```

Se o túnel reiniciar, pode haver uma breve indisponibilidade até a republicação do Netlify. A verificação inicial ocorre aproximadamente 15 segundos após o início; rede, DNS e publicação podem acrescentar tempo. Serviços habilitados e linger garantem início sem abrir sessão no terminal. Falha de autenticação do CLI ou limite do plano gratuito exige correção; o último frontend publicado é preservado. Não é uma instalação com garantia de produção. Ao concluir a construção, escolher domínio e hospedagem com endereço estável, backup e disponibilidade adequados.

## Validação em 02/10/2026

Teste Playwright no endereço público validou cadastro, confirmação, login, recuperação, revogação da sessão antiga e rejeição de link já usado. Durante esse teste os emails ficaram em arquivos privados locais; depois foi ativado SMTP. As duas contas temporárias foram removidas. A saúde da API e o bloqueio externo do Actuator também foram verificados.

Correção operacional: Cloudflare retornou “Unauthorized: Tunnel not found” com processo ainda ativo. O teste reiniciou API/gateway/túnel e validou a republicação pelo systemd, com `Result=success`, e o formulário de login público. A versão da API usada em operação é fixada por `ATLAS_API_JAR` em `.runtime/releases`, sem depender de um build em andamento.
