# Backend gratuito durante a construção

O site continua em https://atlas-cobblemon.netlify.app. As chamadas `/api/v1/` passam pelo proxy do Netlify, pelo HTTPS do Cloudflare Quick Tunnel e chegam à API da VM. O PostgreSQL permanece em `127.0.0.1:55432`; a API em `127.0.0.1:8080`. O gateway em `127.0.0.1:4201` aceita apenas rotas da API, sem publicar Actuator ou arquivos da VM.

Não foi contratado plano nem domínio. Esta configuração é para desenvolvimento: depende da VM ligada e conectada à internet. Quick Tunnel não garante disponibilidade, permite até 200 requisições simultâneas e troca o endereço ao iniciar um novo processo. Referência: https://developers.cloudflare.com/tunnel/get-started/quick-tunnels/.

## Serviços

- `atlas-api`: API e PostgreSQL dedicado persistente.
- `atlas-api-preview`: gateway restrito à API.
- `atlas-api-tunnel`: `cloudflared` com HTTPS público, transporte HTTP/2 e reinício em caso de falha.
- `atlas-api-tunnel-sync.timer`: verifica a cada minuto se o endereço mudou. Quando muda, publica novamente o frontend já compilado com o novo proxy. Usa a autenticação local existente do Netlify CLI. Não publica commits no GitHub automaticamente.

Templates ficam em `infra/templates/atlas-api-*.service` e `atlas-api-tunnel-sync.timer`. O checkout utilizado é `~/dev/atlas`; o binário Cloudflare é `~/.local/bin/cloudflared`. É necessário instalar o Netlify CLI, autenticar a conta e vincular `atlas-web` ao site Atlas. A sincronização depende do build em `atlas-web/dist/atlas-web/browser`. Mudanças de endereço consomem publicações/créditos do plano gratuito do Netlify; não habilitar upgrade automático pago.

## Configuração privada

No `atlas-api/.env`, os valores públicos são `SPRING_PROFILES_ACTIVE=local,preview`, `ATLAS_WEB_URL=https://atlas-cobblemon.netlify.app` e `ATLAS_MAIL_MODE=smtp`. O perfil `preview` ativa cookie Secure e permite apenas a origem HTTPS do site. Senhas SMTP, senhas de banco e chave de criptografia permanecem no arquivo ignorado, com permissão `0600`.

Emails de confirmação e recuperação usam o Gmail configurado e links para o Netlify. O banco do jogo não participa desta configuração. Os limites atuais de autenticação são conservadores e compartilham o IP do proxy; revisar identificação de clientes e limites antes de abrir para tráfego amplo.

## Operação

```bash
systemctl --user status atlas-api atlas-api-preview atlas-api-tunnel atlas-api-tunnel-sync.timer
python3 ~/dev/atlas/infra/scripts/sync-api-tunnel.py
journalctl --user -u atlas-api-tunnel-sync.service --no-pager -n 20
```

Se o túnel reiniciar, pode haver uma breve indisponibilidade até a republicação do Netlify. Falha de autenticação do CLI ou limite do plano gratuito exige correção; o último frontend publicado é preservado. Não é uma instalação com garantia de produção. Ao concluir a construção, escolher domínio e hospedagem com endereço estável, backup e disponibilidade adequados.

## Validação em 02/10/2026

Teste Playwright no endereço público validou cadastro, confirmação, login, recuperação, revogação da sessão antiga e rejeição de link já usado. Durante esse teste os emails ficaram em arquivos privados locais; depois foi ativado SMTP. As duas contas temporárias foram removidas. A saúde da API e o bloqueio externo do Actuator também foram verificados.
