# Atlas Web — estado atual

Site publicado: https://atlas-cobblemon.netlify.app. Repositório: https://github.com/AtlasServerProject/atlas-web.

Atualização: 30/09/2026. Último deploy de produção: `6abd8c40e57e0de911d669ef`.

## Entregue

- Identidade Atlas Cobblemon com paleta Emerald e logo oficial na home, cabeçalho, rodapé, favicon e metadados de compartilhamento.
- Quatro páginas: início, como jogar, novidades e loja; menu/rodapé compartilhados e navegação Angular.
- Conteúdo alinhado ao servidor e links para o Discord oficial. Sem IP público inventado, status Offline fixo, launcher fictício ou ofertas de chaves não implementadas.
- Guia para testers, FAQ, recursos de Survival/claims/homes e andamento real do Emerald.
- Vitrine VIP 1/2/3 com comparação, nove prints originais ampliáveis e listas de itens por resgate.
- Valores: R$ 25,00 / R$ 35,00 / R$ 50,00 por 30 dias, sem renovação automática. Preços de pré-lançamento sujeitos a alteração até a abertura das vendas.
- Kits incluídos nos planos; caixas serão produtos separados futuramente. Detalhes em [LOJA.md](LOJA.md).
- Responsividade por CSS, foco visível, atalho para conteúdo e respeito à redução de movimento. Avaliação completa em navegador desktop/celular permanece pendente; o dono aprovou inicialmente o visual.

## Hospedagem

Netlify serve o build estático com HTTPS, independentemente da VM. `netlify.toml`: Node 24.21.0, build `npm run build`, publicação `dist/atlas-web/browser`. `public/_redirects` permite acesso direto às rotas. Deploy manual por CLI autenticada; integração automática com Git ainda não configurada. Não versionar `.netlify`, credenciais ou arquivos `.env`.

Prévia local em http://192.168.227.129:4200, via serviço de usuário `atlas-web.service`; script e template em `infra/scripts/serve-web.py` e `infra/templates/atlas-web.service` no repositório principal. Serve somente o build compilado. Atualizar o build depois de editar o frontend.

Regra do dono: Minecraft, site, bot e acesso dos testers devem iniciar com a VM. `atlas` e `playit` são serviços de sistema habilitados; `atlas-web` e `atlas-bot` são serviços do usuário habilitados, com linger ativado. Reinício integral e conexão externa de tester ainda não foram validados nesta configuração. O Netlify mantém apenas o site: Minecraft e bot continuam dependentes da VM.

## Validação

Build de produção aprovado. Quatro rotas públicas e nove PNGs testados por HTTPS. Metadados da logo e imagem pública verificados. Prints recebidos em `downloads/kits vip.zip`, incorporados sem alteração em `public/kits/`. Resgate e itens conferidos no DailyKitService; VIP 2 mensal contém cinco Bottle Caps OBC.

## Pendências

- Download público do modpack, requisitos finais e endereço Minecraft confirmado.
- Regras e instruções finais aprovadas pela equipe.
- API pública de status; o contador do bot não é uma API pública para o site.
- Compra, pagamento, ativação/expiração, atendimento e testes de entrega VIP. Vendas seguem desativadas.
- Definição e implementação das caixas como produtos separados.
- Revisão visual e acessibilidade no navegador; domínio próprio opcional e deploy automático via Git.

## Impacto nas sprints

Sprint 20: frontend e publicação entregues; API, painel, integração comercial e status público pendentes. Sprint 18: apresentação/preços VIP documentados; assinatura automática não será usada, mas ativação por 30 dias e expiração ainda precisam de implementação.
