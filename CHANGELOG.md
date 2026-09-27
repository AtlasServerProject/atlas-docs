# Histórico de mudanças

Detalhes e validações ficam em [versions/](versions/README.md).
Registros históricos descrevem a época da entrega; o estado atual está em [STATUS.md](STATUS.md).

- [v0.0.1](versions/v0.0.1.md) — Primeiro bootstrap.
- [v0.0.2](versions/v0.0.2.md) — Player System.
- [v0.0.3](versions/v0.0.3.md) — Economy.
- [v0.0.4](versions/v0.0.4.md) — Ranks.
- [v1.8.0](versions/v1.8.0.md) — Autenticação híbrida segura para contas Premium e Offline, com migração de UUID e dados.
- [v1.9.0](versions/v1.9.0.md) — Console administrativo próprio por socket Unix e remoção do RCON.
- [v1.10.0](versions/v1.10.0.md) — Bloqueio de chat e comandos para jogadores não autenticados.
- [v1.11.0](versions/v1.11.0.md) — Logout manual e expiração ativa das sessões de autenticação.
- [v1.12.0](versions/v1.12.0.md) — Primeira entrega do Auth Lobby, com mapa dedicado e saudação individual no login.
- [v1.12.1](versions/v1.12.1.md) — Título de entrada compacto e definição do spawn global do Auth Lobby.
- [v1.12.2](versions/v1.12.2.md) — Spawn exato obrigatório no Auth Lobby para todas as conexões.
- [v1.13.0](versions/v1.13.0.md) — Proteção de construção do Auth Lobby com exceção exclusiva para Dono e Admin.
- [v1.14.0](versions/v1.14.0.md) — Primeira integração com eventos de spawn do Cobblemon; substituída após o teste revelar que comandos ignoravam o cancelamento.
- [v1.14.1](versions/v1.14.1.md) — Bloqueio absoluto de entidades Pokémon no Auth Lobby, validado contra spawn por comando.
- [v1.14.2](versions/v1.14.2.md) — Proteção total contra dano antes da autenticação e bloqueio de dano de queda no Auth Lobby. Os chunks existentes do mapa também foram convertidos para o bioma `minecraft:the_void`.
- [v1.14.3](versions/v1.14.3.md) — Ordenação determinística do TAB pela prioridade dos cargos, mantendo Dono, ADM, MOD e SUP acima de VIPs e Players.
- [v1.14.4](versions/v1.14.4.md) — Bloqueio autoritativo da escolha de Pokémon inicial no Auth Lobby antes que o Cobblemon grave a escolha ou entregue o Pokémon.
- [v1.15.0](versions/v1.15.0.md) — Adicionado `/spawn` para jogadores autenticados retornarem ao Hub central e ao seletor de servidores.
- [v1.16.0](versions/v1.16.0.md) — Bloqueados cliques de inventário, receitas, inventário criativo e interações com blocos, itens e entidades antes da autenticação.
- [v1.16.1](versions/v1.16.1.md) — Adicionado bloqueio de cinco minutos após cinco senhas inválidas, sem registrar senha, hash ou IP nos logs de segurança.
- [v1.16.2](versions/v1.16.2.md) — Refinado o limitador para considerar cinco falhas dentro de uma janela móvel de dez minutos, evitando acúmulo indefinido de erros antigos.
- [v1.17.0](versions/v1.17.0.md) — Instalado o Lobby Emerald como `atlas:emerald` e adicionado o seletor por bússola com entrega pós-login, proteção do item, menu exclusivo do Emerald e restauração automática no Auth Lobby.
- [v1.17.1](versions/v1.17.1.md) — Corrigido o destino do Lobby Emerald para `975.5 179 1573.5`, orientado para leste.
- [v1.18.0](versions/v1.18.0.md) — Primeira implementação da proteção de queda e whitelist de Pokémon no Lobby Emerald; substituída após o teste revelar resolução incorreta do mundo durante eventos de spawn.
- [v1.18.1](versions/v1.18.1.md) — Corrigida a resolução da dimensão nos eventos do Cobblemon. O Lobby Emerald permite a escolha do inicial, bloqueia dano de queda e aceita somente espécies fracas explicitamente aprovadas.
- [v1.18.2](versions/v1.18.2.md) — Renomeada a mensagem de proteção para Hub e estendido o bloqueio de quebra e colocação ao Lobby Emerald.
- [v1.19.0](versions/v1.19.0.md) — Criado o Survival Emerald com área de 6000 × 6000 blocos, pré-geração dos 375 × 375 chunks e comando `/lobby` para retornar ao Lobby Emerald.
- [v1.19.1](versions/v1.19.1.md) — Reforçado o limite do Survival Emerald com reposicionamento automático de jogadores que tentarem ultrapassar a área definida.
- [v1.20.0](versions/v1.20.0.md) — Adicionado `/rtp` seguro no Survival Emerald, com cooldown progressivo por cargo e validação do terreno de destino.
- [v1.20.1](versions/v1.20.1.md) — Corrigido o fluxo do `/rtp`: o comando agora é usado no Lobby Emerald e envia o jogador para um local seguro no Survival Emerald.
- [v1.20.2](versions/v1.20.2.md) — O `/rtp` agora mantém uma busca persistente e assíncrona até encontrar um destino seguro, sem exigir novas tentativas do jogador.
- [v1.20.3](versions/v1.20.3.md) — Adicionada uma fila antecipada de destinos seguros inspirada no BetterRTP, tornando o `/rtp` praticamente imediato.
- [v1.20.4](versions/v1.20.4.md) — Adicionado aquecimento de três segundos ao `/rtp`, cancelado sem cooldown caso o jogador se mova.
- [v1.20.5](versions/v1.20.5.md) — Liberado o uso de `/rtp` tanto no Lobby Emerald quanto dentro do Survival Emerald.
- [v1.21.0](versions/v1.21.0.md) — Adicionada persistência da última posição no Survival Emerald, restauração após autenticação e retorno ao lobby somente por morte ou `/lobby emerald`.
- [v1.22.0](versions/v1.22.0.md) — Primeira entrega do Home System, com homes nomeadas, home principal, limites e cooldowns por cargo e teleporte seguro.
- [v1.22.1](versions/v1.22.1.md) — Bloqueados todos os comandos no Auth Hub, inclusive após autenticação, mantendo somente `/login` e `/register`.
- [v1.23.0](versions/v1.23.0.md) — Primeira entrega funcional de Claims & Protection no Survival Emerald, com seleção por pá dourada, inspeção por graveto, confiança cumulativa, limites por cargo e persistência PostgreSQL.
- [v1.23.1](versions/v1.23.1.md) — Conclusão da Sprint 7 com proteção de entidades e Pokémon, bloqueios contra explosões, pistões, fluidos e fogo, auditoria administrativa e bordas visuais por partículas.
- [v1.23.2](versions/v1.23.2.md) — Demarcação visual das claims com blocos de ouro falsos durante a seleção e inspeção, sem modificar o mapa.
- [v1.23.3](versions/v1.23.3.md) — Adicionado teleporte seguro e clicável para claims próprias diretamente pelo `/claimslist`.
- [v1.23.4](versions/v1.23.4.md) — Corrigida a numeração do `/claimslist`: claims apagadas deixam de aparecer e as restantes são renumeradas sequencialmente sem expor IDs internos.
- [v1.23.5](versions/v1.23.5.md) — Corrigida a gamerule `doTileDrops` do Survival Emerald e adicionada garantia automática de drops a cada inicialização.
- [v1.24.0](versions/v1.24.0.md) — Primeira entrega da Sprint 8 com monitoramento de TPS/MSPT e limpeza segura, automática e manual de drops antigos e Pokémon selvagens distantes.
- [v1.24.1](versions/v1.24.1.md) — Conclusão da Sprint 8 com `/lixeira`, `/dropados`, recuperação persistente no PostgreSQL, expiração automática e logs.
- [v1.24.2](versions/v1.24.2.md) — Adicionado `/endbattle`, tema sonoro por mundo, liberação controlada de Pokémon fracos no Lobby Emerald, respawn do Survival para o Lobby Emerald e documentação do pacote de addons Cobblemon.
- [v1.24.3](versions/v1.24.3.md) — Survival Emerald resetado com a mesma seed `27594263`, estruturas/worldgen dos addons habilitados, limite ampliado para 12000 × 12000 blocos e pré-geração atualizada para 750 × 750 chunks.
- [v1.24.4](versions/v1.24.4.md) — Liberado o machado de madeira do WorldEdit no Auth Hub para Dono/OWNER e ADM/ADMIN, mantendo a limpeza de inventário para jogadores comuns e preservando a bússola do seletor.
- [v1.24.5](versions/v1.24.5.md) — Comandos do WorldEdit restritos a Dono/OWNER e ADM/ADMIN em todos os mundos, incluindo Auth Hub, Lobby Emerald e Survival Emerald.
- [v1.24.6](versions/v1.24.6.md) — Auth Lobby fechado com barreiras invisíveis nas laterais e no teto, preservando blocos existentes do mapa e mantendo chunks descarregados após a operação.
- [v1.24.7](versions/v1.24.7.md) — Lobby Emerald fechado com barreiras invisíveis nas laterais e no teto, usando carregamento temporário de chunks na dimensão `atlas:emerald`.
- [v1.24.8](versions/v1.24.8.md) — Corrigido o fluxo de autenticação para manter o jogador no Auth Hub após login/autologin e preservar o inventário real ao usar a bússola para entrar no Lobby Emerald.
- [v1.24.9](versions/v1.24.9.md) — Corrigida a ponte de permissões vanilla para que Dono/OWNER e ADM/ADMIN possam usar comandos do WorldEdit, incluindo `//wand`, sem precisar de OP.
- [v1.24.10](versions/v1.24.10.md) — Schema temporário de Pokébola aplicado no Auth Lobby e fechado com barreira invisível própria ao redor, sem alterar o Lobby Emerald ou o Survival Emerald.
- [v1.25.0](versions/v1.25.0.md) — Integrada a economia do Atlas ao CobbleDollars. `/saldo` e `/addmoney` agora usam o saldo CobbleDollars como fonte oficial, mantendo o banco antigo apenas como legado.
- [v1.25.1](versions/v1.25.1.md) — Adicionado `/pay <player> <valor>` para transferir CobbleDollars entre jogadores online, com validação de saldo, bloqueio de autopagamento e confirmação para os dois lados.
- [v1.26.0](versions/v1.26.0.md) — Adicionado o primeiro NPC oficial do Atlas no Auth Lobby. O NPC `Lobby Emerald` é persistente, sem IA, invulnerável e envia jogadores autenticados ao Lobby Emerald, mantendo o Auth Lobby sem gameplay externo.
- [v1.26.1](versions/v1.26.1.md) — Ajustado o spawn do Auth Lobby para o novo ponto do mapa atual e movido o NPC `Lobby Emerald` para a posição definida no lobby.
- [v1.26.2](versions/v1.26.2.md) — Adicionado alias Atlas `/wand` para entregar o machado de seleção do WorldEdit a Dono/ADM, evitando erro de comando desconhecido com a barra dupla do WorldEdit.
- [v1.26.3](versions/v1.26.3.md) — Adicionado `/dev` para Dono/ADM ativarem OP vanilla e acesso administrativo ao `/op`/`/deop`, inclusive no Auth Hub.
- [v1.26.4](versions/v1.26.4.md) — Auth Lobby resetado para um `minecraft:overworld` void/superflat próprio do Atlas, sem uso de mapa externo. Criada plataforma inicial autoral com spawn, NPC `Lobby Emerald` e barreiras invisíveis.
- [v1.26.5](versions/v1.26.5.md) — Schema do Auth Lobby aplicado no novo mundo void próprio, mantendo spawn, NPC `Lobby Emerald` e barreira invisível ao redor da construção.
- [v1.26.6](versions/v1.26.6.md) — NPC `Lobby Emerald` do Auth Lobby substituído de Villager para FakePlayer nativo do Fabric, inspirado no modelo de NPC player do ZNPCs.
- [v1.26.7](versions/v1.26.7.md) — Hotfix temporário com `ArmorStand` para recuperar visibilidade do NPC após o teste com FakePlayer; supersedido pela integração com Easy NPC.
- [v1.26.8](versions/v1.26.8.md) — NPC visual do Auth Lobby migrado para Easy NPC `easy_npc:humanoid`, mantendo no Atlas Core apenas o clique por tag `atlas_npc_auth_emerald` para enviar jogadores autenticados ao Lobby Emerald.
- [v1.26.9](versions/v1.26.9.md) — Atualizado o modpack cliente com SimpleTMs, Xaero's Minimap, CobbleSounds, Cobblemon Interface e ícones Cobblemon para Xaero. `SimpleTMs` foi instalado no servidor e validado; CobbleTowns ficou pendente por incompatibilidade com Minecraft 1.21.1.
- [v1.27.0](versions/v1.27.0.md) — Aplicadas regras globais PvE: PvP desativado, fome desativada, dano de queda bloqueado nos mundos gerenciados e proteção contra Void. A pré-geração do Survival Emerald foi retomada e a GUI futura das homes foi projetada com ícones e fluxo de uso.
- [v1.27.1](versions/v1.27.1.md) — Gerado o modpack cliente `v3-lite`, reduzindo o pacote de `657 MB` para `258 MB`. O `CobbleSounds[Complete]` foi substituído por uma versão BattleOnly do Atlas, mantendo sons de batalha e removendo músicas pesadas de mundo/bioma.
- [v1.27.2](versions/v1.27.2.md) — Gerado o modpack cliente `v4-nosounds`, removendo completamente o CobbleSounds para diagnosticar os timeouts em `Entrando no mundo...`. O pacote caiu para `168 MB` e mantém apenas Cobblemon Interface e ícones Cobblemon do Xaero como resource packs.
- [v1.27.3](versions/v1.27.3.md) — Gerado o modpack cliente `v7-current` com `144 MB`, alinhado à pasta de mods atual do servidor de testes. Os pacotes antigos `v3-lite`, `v4-nosounds`, `v5-minconnect` e `v6-coreconnect` foram removidos da raiz do projeto para evitar confusão.
- [v1.27.4](versions/v1.27.4.md) — Criado o resource pack `Atlas-CobbleSongs-Lite-v1.0.0.zip` com 12 faixas selecionadas do `CobbleSounds[Complete]`, reduzindo a trilha sonora para aproximadamente `25 MB`.
- [v1.27.5](versions/v1.27.5.md) — Removidos `Sophisticated Backpacks`, `Sophisticated Core` e `Sophisticated Storage` do servidor após o cliente não carregar corretamente o mapa. Criado o modpack `v9-nosophisticated-cobblesongs-lite` com `165 MB`, mantendo o `Atlas CobbleSongs Lite` e removendo completamente o trio Sophisticated do pacote do cliente.
- [v1.27.6](versions/v1.27.6.md) — Confirmado que o problema de carregamento do mapa era causado pelo trio Sophisticated. O servidor permanece sem `Sophisticated Backpacks`, `Sophisticated Core` e `Sophisticated Storage`.
- [v1.27.7](versions/v1.27.7.md) — Hotfix do login no Auth Lobby: o teleporte para o spawn deixou de ocorrer diretamente no evento `JOIN` e passou a ser executado no tick seguinte do servidor.
- [v1.27.8](versions/v1.27.8.md) — Temas musicais do Atlas conectados ao `CobbleSounds[AtlasLite]`: o Auth Lobby/Hub agora toca `cobblesounds:rustboro_city_hoenn2`, o Lobby Emerald toca `cobblesounds:introductions_hoenn` e o Survival Emerald usa `cobblesounds:route1_sinnoh`.
- [v1.27.9](versions/v1.27.9.md) — Sistema de música evoluído para prioridade por contexto. O Survival/RTP agora varia o tema entre rota base, rotas alternativas, água/mar e caverna, em vez de tocar uma única faixa fixa.
- [v1.27.10](versions/v1.27.10.md) — A limpeza automática do Survival Emerald agora remove Pokémon selvagens elegíveis independentemente do tempo de spawn. As proteções continuam ativas para Pokémon de jogadores, Pokémon em batalha, ocupados, vinculados a pastures/tethering ou próximos de jogadores.
- [v1.28.0](versions/v1.28.0.md) — Primeira entrega da Sprint 9 com sistema de moderação e punições persistentes.
- [v1.28.1](versions/v1.28.1.md) — Hotfix da Sprint 9: `/unban` agora também remove banimentos vanilla aplicados por engano com o comando `/ban` do Minecraft. Adicionados aliases seguros `/atlasban` e `/atlasunban` para evitar ambiguidade com o comando vanilla.
- [v1.28.2](versions/v1.28.2.md) — Atualização do modpack cliente para `v13-e19-minimap-icons`. O resource pack antigo `Xaeros Cobblemon Icons v2.1.zip` foi substituído por `E19 Cobblemon Minimap Icons.zip`, extraído do pacote Cobbleverse analisado localmente.
- [v1.28.3](versions/v1.28.3.md) — Criado o pacote manual `mods-qol-2026-07-13` com mods de qualidade de vida para o cliente: MouseTweaks, Controlling, BetterF3, Zoomify, BetterThirdPerson, NotEnoughAnimations, EntityCulling, ImmediatelyFast, ModernFix, FerriteCore, Lithium, Krypton, PacketFixer, CatchIndicator e CatchRate Display.
- [v1.28.4](versions/v1.28.4.md) — Criado o pacote manual `mods-phase3-cobblemon-2026-07-13`, contendo a fase 3 de gameplay Cobblemon sem `fightorflight`.
- [v1.28.5](versions/v1.28.5.md) — Hotfix do Anti Lag: a limpeza automática do Survival Emerald agora remove Pokémon selvagens elegíveis mesmo quando estão próximos de jogadores. Isso corrige o acúmulo de Pokémon comuns ao redor de players, bases e áreas movimentadas.
- [v1.28.6](versions/v1.28.6.md) — Hotfix de compatibilidade das mega pedras: adicionado `zamega-fabric-1.7.1.jar` ao servidor.
- [v1.28.7](versions/v1.28.7.md) — Hotfix de alinhamento de registry entre cliente e servidor.
- [v1.28.8](versions/v1.28.8.md) — Evolução do `/rtp`: o comando sem argumentos agora abre uma interface com três destinos do Survival Emerald: Overworld, Nether e The End.
- [v1.28.9](versions/v1.28.9.md) — Chunky reinstalado no servidor com `Chunky-Fabric-1.4.23.jar` para pré-gerar Nether e The End após a liberação do `/rtp` multidimensional.
- [v1.29.0](versions/v1.29.0.md) — Primeira entrega prática da Sprint 10 com sistema de kits.
- [v1.29.1](versions/v1.29.1.md) — Expansão do sistema de kits.
- [v1.29.2](versions/v1.29.2.md) — Adicionado `/back` para retornar à última localização salva antes de teleportes manuais.
- [v1.29.3](versions/v1.29.3.md) — Adicionado `/fly` para alternar voo.
- [v1.29.4](versions/v1.29.4.md) — Adicionados kits VIP ao `/kits`.
- [v1.29.5](versions/v1.29.5.md) — Kits VIP reformulados conforme a tabela final de benefícios.
- [v1.29.6](versions/v1.29.6.md) — Adicionado `/ec` com alias `/enderchest`.
- [v1.29.7](versions/v1.29.7.md) — Adicionadas as variações visuais de VIP.
- [v1.29.8](versions/v1.29.8.md) — Adicionado chat colorido para VIPs e Staff.
- [v1.29.9 (atualização de mundo)](versions/v1.29.9.md) — O Lobby Emerald foi preparado em um mundo void/superflat autoral, removendo o terreno legado e mantendo a base de construção de 129 × 129 blocos no spawn `975.5 179 1573.5`. Foi criada uma ilha flutuante sob a base, com camadas reduzidas de pedra, terra e deepslate e pontas de dripstone. As barreiras invisíveis e as regras do lobby foram preservadas. Esta atualização é operacional; o jar do Atlas Core permanece na versão `1.29.8`.
- [v1.29.10 (atualização de mundo)](versions/v1.29.10.md) — Correção visual do Lobby Emerald: a antiga plataforma de quartzo, blocos brancos e detalhes de esmeralda foram removidos completamente. A base foi reconstruída como uma ilha flutuante natural, com superfície de grama, camadas de terra, pedra e deepslate e cone inferior de dripstone. As barreiras invisíveis de proteção foram restauradas após a reconstrução.
- [v1.29.11](versions/v1.29.11.md) — Corrigida a autorização do WorldEdit para a sintaxe de dupla barra (`//set`, `//pos1`, `//pos2`, `//wand` e demais comandos). Dono/OWNER e ADM/ADMIN são reconhecidos pelo filtro global e continuam sendo os únicos cargos permitidos; jogadores comuns permanecem bloqueados.
- [v1.29.12](versions/v1.29.12.md) — Corrigido o `/wand`: o machado entregue agora é uma stack vanilla de `minecraft:wooden_axe`, exatamente igual ao item configurado pelo WorldEdit, sem nome ou componentes customizados que pudessem impedir o reconhecimento.
- [v1.29.13](versions/v1.29.13.md) — Adicionado bypass total de comandos para `OWNER/DONO` após a autenticação. O Dono agora pode executar todos os comandos registrados pelo servidor, inclusive no Auth Hub, enquanto a proteção antes do login permanece ativa.

- [v1.29.14](versions/v1.29.14.md) — Corrigidos pacotes Java e avisos do editor.

## Registros operacionais

Documentação operacional

Adicionada a referência dos comandos `sudo playit status` e `sudo playit attach`, incluindo a consulta do endereço externo e a validação dos serviços necessários.

Ferramentas administrativas

Instalado WorldEdit `7.3.8` para Fabric 1.21.1 como ferramenta de construção e manutenção de mapas. A Sprint 12 — Atlas Events foi iniciada com documentação do fluxo, filosofia, componentes e comandos previstos.

Runtime do servidor

Corrigido o runtime do Atlas para `-Xms1G -Xmx4G`, compatível com a RAM atual da máquina. O Chunky deixou de continuar automaticamente após reinício e o `atlas-cli pregenerate-survival` sem argumento agora consulta status em vez de iniciar pré-geração.
