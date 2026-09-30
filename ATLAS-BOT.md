# Atlas-bot — Discord Atlas Cobblemon

Atualizado em 30/09/2026. Código e manual operacional: [atlas/atlas-bot](https://github.com/AtlasServerProject/atlas/tree/codex/configure-atlas-docs-submodule/atlas-bot).

## Entregue

- Serviço de usuário `atlas-bot.service` instalado, habilitado e conectado ao Discord.
- Node.js 24, discord.js 14.27.0; credenciais externas em `~/.config/atlas/discord-bot.env` (600), sem segredos versionados.
- Comandos `/ping`, `/ajuda`, `/servidor`, `/como-jogar`, `/online`, `/estrutura`, `/aviso` e `/dono`.
- Administração restrita ao ID do dono e ao canal privado `atlas-controle`; outros administradores não recebem acesso aos comandos administrativos.
- Criação de canais texto/voz, cargos, atribuição de cargos e ajustes explícitos de permissões. Interação por comandos de barra, sem conversa livre.
- Categorias temáticas Informações, Comunidade e Voz; canais informativos, conversa, dúvidas, sugestões, aventuras, trocas e salas de voz.
- Cargos DONO vermelho-escuro, ADM vermelho, MOD azul, SUP verde, VIP dourado, BETA roxo e Membro branco. Cores correspondem ao Minecraft, exceto BETA, sem equivalente atual. Cargos novos sem permissões administrativas adicionais. Treinador e Avisos Atlas também existem.
- Boas-vindas para novos membros humanos, com avatar, menção e links para regras/como-jogar; cargo Membro automático. Bots ignorados, sem atribuição retroativa. Server Members Intent ativado.
- Contagem Minecraft por status TCP local, sem RCON: atividade a cada 30 segundos e `/online` com cache de 10 segundos. Falha mostra indisponível em vez de zero.
- Categoria STATUS acima de Informações, contadores Discord (inclui bots) e Minecraft em canais de voz bloqueados para membros comuns. Atualização aproximadamente a cada 310 segundos; nomes mantêm última leitura se o bot parar.
- Receptor local autenticado e emissor CLI para avisos Minecraft preparados; eventos do atlas-core ainda não conectados automaticamente.

## Decisões e pendências

- Não exibir endereço/site por enquanto. Configuração vazia não cria canal de endereço. A exclusão do placeholder existente foi recusada pelo Discord com `Missing Access`; remover manualmente ou ajustar as permissões do bot nesse canal.
- Os canais STATUS existentes também negam Connect ao bot; alterações de canais de voz podem ser recusadas apesar de Manage Channels. O modelo foi corrigido para permitir Connect ao bot em canais novos, mantendo a negação aos membros. É necessário ajustar os existentes no Discord.
- Definir textos finais de regras, boas-vindas editoriais e instruções do modpack.
- Validar entrada real, atribuição Membro e comandos usando a conta do dono.
- Sem sincronização automática de ranks Minecraft/Discord, pagamentos, banimentos ou interpretação de linguagem natural.
- Linger do usuário ainda desativado: revisar inicialização sem sessão aberta.
- Biblioteca minecraft-server-util 5.4.4 não tem manutenção upstream; dependência fixada, consulta local testada.

## Validação

13 testes locais passaram: controle do dono, configuração, avisos autenticados, estrutura sem duplicação, boas-vindas, cargo automático, cache de status, falhas/recuperação e rótulos dos contadores. Consulta real ao Minecraft retornou 0/50; bot conectado após reinício. Credenciais e node_modules excluídos do Git. Nenhuma alteração do atlas-core foi necessária nesta entrega.
