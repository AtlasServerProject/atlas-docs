v0.0.1

Primeiro bootstrap.

---

v0.0.2

Player System.

---

v0.0.3

Economy.

---

v0.0.4

Ranks.

---

O histórico detalhado dos builds do mod está em `atlas-docs/versions/`.

---

v1.8.0

Autenticação híbrida segura para contas Premium e Offline, com migração de UUID e dados.

---

v1.9.0

Console administrativo próprio por socket Unix e remoção do RCON.

---

v1.10.0

Bloqueio de chat e comandos para jogadores não autenticados.

---

v1.11.0

Logout manual e expiração ativa das sessões de autenticação.

---

v1.12.0

Primeira entrega do Auth Lobby, com mapa dedicado e saudação individual no login.

---

v1.12.1

Título de entrada compacto e definição do spawn global do Auth Lobby.

---

v1.12.2

Spawn exato obrigatório no Auth Lobby para todas as conexões.

---

v1.13.0

Proteção de construção do Auth Lobby com exceção exclusiva para Dono e Admin.

---

v1.14.0

Primeira integração com eventos de spawn do Cobblemon; substituída após o teste revelar que comandos ignoravam o cancelamento.

---

v1.14.1

Bloqueio absoluto de entidades Pokémon no Auth Lobby, validado contra spawn por comando.

---

Documentação operacional

Adicionada a referência dos comandos `sudo playit status` e `sudo playit attach`, incluindo a consulta do endereço externo e a validação dos serviços necessários.

---

v1.14.2

Proteção total contra dano antes da autenticação e bloqueio de dano de queda no Auth Lobby. Os chunks existentes do mapa também foram convertidos para o bioma `minecraft:the_void`.

---

v1.14.3

Ordenação determinística do TAB pela prioridade dos cargos, mantendo Dono, ADM, MOD e SUP acima de VIPs e Players.

---

v1.14.4

Bloqueio autoritativo da escolha de Pokémon inicial no Auth Lobby antes que o Cobblemon grave a escolha ou entregue o Pokémon.

---

v1.15.0

Adicionado `/spawn` para jogadores autenticados retornarem ao Hub central e ao seletor de servidores.

---

v1.16.0

Bloqueados cliques de inventário, receitas, inventário criativo e interações com blocos, itens e entidades antes da autenticação.

---

v1.16.1

Adicionado bloqueio de cinco minutos após cinco senhas inválidas, sem registrar senha, hash ou IP nos logs de segurança.

---

v1.16.2

Refinado o limitador para considerar cinco falhas dentro de uma janela móvel de dez minutos, evitando acúmulo indefinido de erros antigos.

---

v1.17.0

Instalado o Lobby Emerald como `atlas:emerald` e adicionado o seletor por bússola com entrega pós-login, proteção do item, menu exclusivo do Emerald e restauração automática no Auth Lobby.

---

v1.17.1

Corrigido o destino do Lobby Emerald para `975.5 179 1573.5`, orientado para leste.

---

v1.18.0

Primeira implementação da proteção de queda e whitelist de Pokémon no Lobby Emerald; substituída após o teste revelar resolução incorreta do mundo durante eventos de spawn.

---

v1.18.1

Corrigida a resolução da dimensão nos eventos do Cobblemon. O Lobby Emerald permite a escolha do inicial, bloqueia dano de queda e aceita somente espécies fracas explicitamente aprovadas.

---

v1.18.2

Renomeada a mensagem de proteção para Hub e estendido o bloqueio de quebra e colocação ao Lobby Emerald.

---

v1.19.0

Criado o Survival Emerald com área de 6000 × 6000 blocos, pré-geração dos 375 × 375 chunks e comando `/lobby` para retornar ao Lobby Emerald.

---

v1.19.1

Reforçado o limite do Survival Emerald com reposicionamento automático de jogadores que tentarem ultrapassar a área definida.

---

v1.20.0

Adicionado `/rtp` seguro no Survival Emerald, com cooldown progressivo por cargo e validação do terreno de destino.

---

v1.20.1

Corrigido o fluxo do `/rtp`: o comando agora é usado no Lobby Emerald e envia o jogador para um local seguro no Survival Emerald.

---

v1.20.2

O `/rtp` agora mantém uma busca persistente e assíncrona até encontrar um destino seguro, sem exigir novas tentativas do jogador.

---

v1.20.3

Adicionada uma fila antecipada de destinos seguros inspirada no BetterRTP, tornando o `/rtp` praticamente imediato.

---

v1.20.4

Adicionado aquecimento de três segundos ao `/rtp`, cancelado sem cooldown caso o jogador se mova.

---

v1.20.5

Liberado o uso de `/rtp` tanto no Lobby Emerald quanto dentro do Survival Emerald.

---

v1.21.0

Adicionada persistência da última posição no Survival Emerald, restauração após autenticação e retorno ao lobby somente por morte ou `/lobby emerald`.

---

v1.22.0

Primeira entrega do Home System, com homes nomeadas, home principal, limites e cooldowns por cargo e teleporte seguro.

---

v1.22.1

Bloqueados todos os comandos no Auth Hub, inclusive após autenticação, mantendo somente `/login` e `/register`.

---

v1.23.0

Primeira entrega funcional de Claims & Protection no Survival Emerald, com seleção por pá dourada, inspeção por graveto, confiança cumulativa, limites por cargo e persistência PostgreSQL.

---

v1.23.1

Conclusão da Sprint 7 com proteção de entidades e Pokémon, bloqueios contra explosões, pistões, fluidos e fogo, auditoria administrativa e bordas visuais por partículas.

---

v1.23.2

Demarcação visual das claims com blocos de ouro falsos durante a seleção e inspeção, sem modificar o mapa.

---

v1.23.3

Adicionado teleporte seguro e clicável para claims próprias diretamente pelo `/claimslist`.

---

v1.23.4

Corrigida a numeração do `/claimslist`: claims apagadas deixam de aparecer e as restantes são renumeradas sequencialmente sem expor IDs internos.

---

v1.23.5

Corrigida a gamerule `doTileDrops` do Survival Emerald e adicionada garantia automática de drops a cada inicialização.

---

v1.24.0

Primeira entrega da Sprint 8 com monitoramento de TPS/MSPT e limpeza segura, automática e manual de drops antigos e Pokémon selvagens distantes.

---

v1.24.1

Conclusão da Sprint 8 com `/lixeira`, `/dropados`, recuperação persistente no PostgreSQL, expiração automática e logs.

---

v1.24.2

Adicionado `/endbattle`, tema sonoro por mundo, liberação controlada de Pokémon fracos no Lobby Emerald, respawn do Survival para o Lobby Emerald e documentação do pacote de addons Cobblemon.

---

v1.24.3

Survival Emerald resetado com a mesma seed `27594263`, estruturas/worldgen dos addons habilitados, limite ampliado para 12000 × 12000 blocos e pré-geração atualizada para 750 × 750 chunks.

---

Ferramentas administrativas

Instalado WorldEdit `7.3.8` para Fabric 1.21.1 como ferramenta de construção e manutenção de mapas. A Sprint 12 — Atlas Events foi iniciada com documentação do fluxo, filosofia, componentes e comandos previstos.

---

Runtime do servidor

Corrigido o runtime do Atlas para `-Xms1G -Xmx4G`, compatível com a RAM atual da máquina. O Chunky deixou de continuar automaticamente após reinício e o `atlas-cli pregenerate-survival` sem argumento agora consulta status em vez de iniciar pré-geração.

---

v1.24.4

Liberado o machado de madeira do WorldEdit no Auth Hub para Dono/OWNER e ADM/ADMIN, mantendo a limpeza de inventário para jogadores comuns e preservando a bússola do seletor.

---

v1.24.5

Comandos do WorldEdit restritos a Dono/OWNER e ADM/ADMIN em todos os mundos, incluindo Auth Hub, Lobby Emerald e Survival Emerald.

---

v1.24.6

Auth Lobby fechado com barreiras invisíveis nas laterais e no teto, preservando blocos existentes do mapa e mantendo chunks descarregados após a operação.

---

v1.24.7

Lobby Emerald fechado com barreiras invisíveis nas laterais e no teto, usando carregamento temporário de chunks na dimensão `atlas:emerald`.

---

v1.24.8

Corrigido o fluxo de autenticação para manter o jogador no Auth Hub após login/autologin e preservar o inventário real ao usar a bússola para entrar no Lobby Emerald.

---

v1.24.9

Corrigida a ponte de permissões vanilla para que Dono/OWNER e ADM/ADMIN possam usar comandos do WorldEdit, incluindo `//wand`, sem precisar de OP.

---

v1.24.10

Schema temporário de Pokébola aplicado no Auth Lobby e fechado com barreira invisível própria ao redor, sem alterar o Lobby Emerald ou o Survival Emerald.

---

v1.25.0

Integrada a economia do Atlas ao CobbleDollars. `/saldo` e `/addmoney` agora usam o saldo CobbleDollars como fonte oficial, mantendo o banco antigo apenas como legado.

---

v1.25.1

Adicionado `/pay <player> <valor>` para transferir CobbleDollars entre jogadores online, com validação de saldo, bloqueio de autopagamento e confirmação para os dois lados.

---

v1.26.0

Adicionado o primeiro NPC oficial do Atlas no Auth Lobby. O NPC `Lobby Emerald` é persistente, sem IA, invulnerável e envia jogadores autenticados ao Lobby Emerald, mantendo o Auth Lobby sem gameplay externo.

---

v1.26.1

Ajustado o spawn do Auth Lobby para o novo ponto do mapa atual e movido o NPC `Lobby Emerald` para a posição definida no lobby.

---

v1.26.2

Adicionado alias Atlas `/wand` para entregar o machado de seleção do WorldEdit a Dono/ADM, evitando erro de comando desconhecido com a barra dupla do WorldEdit.

---

v1.26.3

Adicionado `/dev` para Dono/ADM ativarem OP vanilla e acesso administrativo ao `/op`/`/deop`, inclusive no Auth Hub.

---

v1.26.4

Auth Lobby resetado para um `minecraft:overworld` void/superflat próprio do Atlas, sem uso de mapa externo. Criada plataforma inicial autoral com spawn, NPC `Lobby Emerald` e barreiras invisíveis.

---

v1.26.5

Schema do Auth Lobby aplicado no novo mundo void próprio, mantendo spawn, NPC `Lobby Emerald` e barreira invisível ao redor da construção.

---

v1.26.6

NPC `Lobby Emerald` do Auth Lobby substituído de Villager para FakePlayer nativo do Fabric, inspirado no modelo de NPC player do ZNPCs.

---

v1.26.7

Hotfix temporário com `ArmorStand` para recuperar visibilidade do NPC após o teste com FakePlayer; supersedido pela integração com Easy NPC.

---

v1.26.8

NPC visual do Auth Lobby migrado para Easy NPC `easy_npc:humanoid`, mantendo no Atlas Core apenas o clique por tag `atlas_npc_auth_emerald` para enviar jogadores autenticados ao Lobby Emerald.

---

v1.26.9

Atualizado o modpack cliente com SimpleTMs, Xaero's Minimap, CobbleSounds, Cobblemon Interface e ícones Cobblemon para Xaero. `SimpleTMs` foi instalado no servidor e validado; CobbleTowns ficou pendente por incompatibilidade com Minecraft 1.21.1.

---

v1.27.0

Aplicadas regras globais PvE: PvP desativado, fome desativada, dano de queda bloqueado nos mundos gerenciados e proteção contra Void. A pré-geração do Survival Emerald foi retomada e a GUI futura das homes foi projetada com ícones e fluxo de uso.

---

v1.27.1

Gerado o modpack cliente `v3-lite`, reduzindo o pacote de `657 MB` para `258 MB`. O `CobbleSounds[Complete]` foi substituído por uma versão BattleOnly do Atlas, mantendo sons de batalha e removendo músicas pesadas de mundo/bioma.

---

v1.27.2

Gerado o modpack cliente `v4-nosounds`, removendo completamente o CobbleSounds para diagnosticar os timeouts em `Entrando no mundo...`. O pacote caiu para `168 MB` e mantém apenas Cobblemon Interface e ícones Cobblemon do Xaero como resource packs.

---

v1.27.3

Gerado o modpack cliente `v7-current` com `144 MB`, alinhado à pasta de mods atual do servidor de testes. Os pacotes antigos `v3-lite`, `v4-nosounds`, `v5-minconnect` e `v6-coreconnect` foram removidos da raiz do projeto para evitar confusão.

O pacote mantém Cobblemon, Easy NPC, Sophisticated Backpacks/Core/Storage, dependências necessárias, Xaero Minimap e os resource packs Cobblemon Interface + Xaero Cobblemon Icons. O `atlas-core.jar` continua fora do cliente por ser exclusivo do servidor.

---

v1.27.4

Criado o resource pack `Atlas-CobbleSongs-Lite-v1.0.0.zip` com 12 faixas selecionadas do `CobbleSounds[Complete]`, reduzindo a trilha sonora para aproximadamente `25 MB`.

Gerado o modpack cliente `v8-cobblesongs-lite` com `169 MB`, incluindo o pack de músicas leve junto do conjunto atual de mods e resource packs do Atlas.

---

v1.27.5

Removidos `Sophisticated Backpacks`, `Sophisticated Core` e `Sophisticated Storage` do servidor após o cliente não carregar corretamente o mapa. Criado o modpack `v9-nosophisticated-cobblesongs-lite` com `165 MB`, mantendo o `Atlas CobbleSongs Lite` e removendo completamente o trio Sophisticated do pacote do cliente.

---

v1.27.6

Confirmado que o problema de carregamento do mapa era causado pelo trio Sophisticated. O servidor permanece sem `Sophisticated Backpacks`, `Sophisticated Core` e `Sophisticated Storage`.

O resource pack de música foi refeito como `CobbleSounds[AtlasLite]_v1.4.1.zip`, preservando os IDs originais do CobbleSounds em vez de IDs customizados `atlas.music.*`. Gerado o modpack cliente `v10-cobblesounds-atlaslite` com `165 MB`, sem Sophisticated e com o CobbleSounds AtlasLite incluído.

---

v1.27.7

Hotfix do login no Auth Lobby: o teleporte para o spawn deixou de ocorrer diretamente no evento `JOIN` e passou a ser executado no tick seguinte do servidor.

Esse ajuste evita conflito com o rastreamento interno de chunks do Minecraft, que estava gerando `Force-added player with duplicate UUID` e podia deixar o jogador preso no limbo mesmo com os arquivos do mapa intactos.

---

v1.27.8

Temas musicais do Atlas conectados ao `CobbleSounds[AtlasLite]`: o Auth Lobby/Hub agora toca `cobblesounds:rustboro_city_hoenn2`, o Lobby Emerald toca `cobblesounds:introductions_hoenn` e o Survival Emerald usa `cobblesounds:route1_sinnoh`.

O resource pack Lite foi refeito com aliases mínimos em `assets/minecraft/sounds.json` e correção do `surfing_hoenn2`, permitindo que o pacote leve funcione sem depender do CobbleSounds Complete. Gerado o modpack cliente `v11-cobblesounds-themefix`.

---

v1.27.9

Sistema de música evoluído para prioridade por contexto. O Survival/RTP agora varia o tema entre rota base, rotas alternativas, água/mar e caverna, em vez de tocar uma única faixa fixa.

Batalhas do Cobblemon agora têm prioridade sobre temas de área: ao iniciar uma batalha, o Atlas para a música atual e toca um tema de batalha; ao vencer, fugir ou usar `/endbattle`, a música de área volta automaticamente.

---

v1.27.10

A limpeza automática do Survival Emerald agora remove Pokémon selvagens elegíveis independentemente do tempo de spawn. As proteções continuam ativas para Pokémon de jogadores, Pokémon em batalha, ocupados, vinculados a pastures/tethering ou próximos de jogadores.

Drops continuam exigindo pelo menos 5 minutos no chão antes de serem removidos.

---

v1.28.0

Primeira entrega da Sprint 9 com sistema de moderação e punições persistentes.

Adicionados `/warn`, `/kick`, `/mute`, `/unmute`, `/ban`, `/unban`, `/banip`, `/unbanip` e `/punishments`. Mutes bloqueiam chat, bans bloqueiam entrada no servidor e BanIP bloqueia conexões pelo IP registrado. As punições ficam salvas no PostgreSQL e respeitam a hierarquia da staff.

---

v1.28.1

Hotfix da Sprint 9: `/unban` agora também remove banimentos vanilla aplicados por engano com o comando `/ban` do Minecraft. Adicionados aliases seguros `/atlasban` e `/atlasunban` para evitar ambiguidade com o comando vanilla.

---

v1.28.2

Atualização do modpack cliente para `v13-e19-minimap-icons`. O resource pack antigo `Xaeros Cobblemon Icons v2.1.zip` foi substituído por `E19 Cobblemon Minimap Icons.zip`, extraído do pacote Cobbleverse analisado localmente.

O E19 foi validado com `9947` entradas, `9447` sprites `.png` e definição do Xaero em `assets/xaerominimap/entity/icon/definition/cobblemon/pokemon.json`. Também foi disponibilizado separadamente em `/home/somente/dev/atlas/E19 Cobblemon Minimap Icons.zip` para instalação manual.

---

v1.28.3

Criado o pacote manual `mods-qol-2026-07-13` com mods de qualidade de vida para o cliente: MouseTweaks, Controlling, BetterF3, Zoomify, BetterThirdPerson, NotEnoughAnimations, EntityCulling, ImmediatelyFast, ModernFix, FerriteCore, Lithium, Krypton, PacketFixer, CatchIndicator e CatchRate Display.

No servidor foram instalados apenas os mods seguros de lado servidor: ModernFix, FerriteCore, Lithium, Krypton e PacketFixer. Foi criado backup em `/opt/atlas/server/backups/mod-versions/mods-pre-qol-server-20260713-144049.tar.gz`. O restart ainda precisa ser executado manualmente por exigir autenticação interativa do `systemctl`.

---

v1.28.4

Criado o pacote manual `mods-phase3-cobblemon-2026-07-13`, contendo a fase 3 de gameplay Cobblemon sem `fightorflight`.

Adicionados ao pacote e copiados para o servidor: Cobblemon Raid Dens, Cobbreeding, SafePastures, PastureLoot, CobbleCuisine, PokéBlocks, Cobblemon Additions, Cobblemon Battle Extras, Cobblemon Battle Positions, Mega Showdown, Cobbleverse Badges e Fabric Language Kotlin.

`fightorflight` foi propositalmente excluído por alterar o combate/comportamento dos Pokémon de maneira agressiva. Backup criado antes da instalação em `/opt/atlas/server/backups/mod-versions/mods-pre-phase3-cobblemon-20260713-145356.tar.gz`. O restart ainda precisa ser executado manualmente para carregar os novos JARs.

---

v1.28.5

Hotfix do Anti Lag: a limpeza automática do Survival Emerald agora remove Pokémon selvagens elegíveis mesmo quando estão próximos de jogadores. Isso corrige o acúmulo de Pokémon comuns ao redor de players, bases e áreas movimentadas.

Continuam protegidos Pokémon de jogadores, Pokémon em batalha, ocupados ou vinculados a pastures. Também foi adicionada uma lista protegida de lendários e míticos de Kanto até Paldea, usando os IDs internos reais do Cobblemon para evitar remoções indevidas.

---

v1.28.6

Hotfix de compatibilidade das mega pedras: adicionado `zamega-fabric-1.7.1.jar` ao servidor.

O problema investigado desconectava o jogador ao pegar certas mega stones em modo criativo com `Failed to decode packet 'serverbound/minecraft:set_creative_mode_slot'`. A causa provável era diferença entre cliente e servidor: o cliente possuía itens do addon Z-A Mega, mas o servidor tinha apenas `mega_showdown`.

Criado backup antes da instalação em `/opt/atlas/server/backups/mod-versions/mods-pre-zamega-hotfix-20260713-152237.tar.gz` e pacote separado em `/home/somente/dev/atlas/mods-zamega-hotfix-2026-07-13.tar.gz`.

---

v1.28.7

Hotfix de alinhamento de registry entre cliente e servidor.

O servidor estava em execução desde antes da instalação dos mods de gameplay, então os JARs existiam na pasta `mods`, mas não estavam carregados no processo ativo. Isso fazia o cliente enviar itens novos pelo inventário criativo enquanto o servidor ainda não conhecia aqueles registros, causando `Failed to decode packet 'serverbound/minecraft:set_creative_mode_slot'`.

O servidor foi reiniciado pelo console administrativo e passou a carregar `102 mods`, incluindo `mega_showdown`, `zamega`, CobbleDollars, CobbleFurnies, CobbleNav, TM Craft, MoreCobblemonTweaks e Only Bottle Caps.

Também foram instalados mods que estavam documentados/esperados mas ausentes na pasta ativa do servidor: `CobbleDollars`, `CobbleFurnies`, `MoreCobblemonTweaks`, `Only Bottle Caps`, `cobblenav`, `tmcraft` e as libs `supermartijn642configlib`/`supermartijn642corelib`.

Criado backup antes do alinhamento em `/opt/atlas/server/backups/mod-versions/mods-pre-registry-align-20260713-153645.tar.gz` e pacote separado em `/home/somente/dev/atlas/mods-registry-align-2026-07-13.tar.gz`.

---

v1.28.8

Evolução do `/rtp`: o comando sem argumentos agora abre uma interface com três destinos do Survival Emerald: Overworld, Nether e The End.

Também foram adicionados atalhos diretos `/rtp overworld`, `/rtp nether` e `/rtp end`. Cada dimensão possui fila própria de destinos seguros, mantendo cooldown por cargo e cancelamento por movimento sem aplicar cooldown.

Nether e The End passam a herdar regras PvE das áreas survival, incluindo fome desativada, dano de queda desativado, proteção contra Void e retorno ao Lobby Emerald após morte. The End recebeu a trilha `distortion_world_sinnoh.ogg`.

---

v1.28.9

Chunky reinstalado no servidor com `Chunky-Fabric-1.4.23.jar` para pré-gerar Nether e The End após a liberação do `/rtp` multidimensional.

Adicionados comandos ao `atlas-cli`: `pregenerate-nether` e `pregenerate-end`, ambos com `start`, `status`, `pause` e `continue`. O `pregenerate-survival start` também foi atualizado para a sintaxe nova do Chunky.

Pré-geração do Nether iniciada em `minecraft:the_nether`, formato `square`, centro `0 0`, raio `6000`. Após o Chunky ficar sem tarefas pendentes, a pré-geração do The End foi iniciada em `minecraft:the_end` com a mesma seleção.

---

v1.29.0

Primeira entrega prática da Sprint 10 com sistema de kits.

Adicionado `/kits`, que abre uma interface com os kits disponíveis. O primeiro kit liberado é o Kit Diário, com cooldown de 24 horas e entrega da `Pá de Claim do Atlas` para criação de claims no Survival Emerald. O atalho `/kit diario` continua disponível para resgate direto.

---

v1.29.1

Expansão do sistema de kits.

A interface `/kits` agora usa o `Baú do Gimmighoul` como ícone dos kits, diferenciando Diário, Semanal e Mensal pelas cores. O Kit Diário passou a entregar Poké Bolas, Super Bolas e Ultra Bolas junto da pá de claim. Foram adicionados Kit Semanal e Kit Mensal, com cooldowns separados e recompensas próprias.

---

v1.29.2

Adicionado `/back` para retornar à última localização salva antes de teleportes manuais.

O sistema registra a posição anterior antes de `/lobby emerald`, `/spawn`, `/home`, `/claimtp` e `/rtp`. Ao usar `/back`, o jogador volta para essa posição e o local atual passa a ser o novo destino de volta, permitindo alternar entre os dois pontos.

---

v1.29.3

Adicionado `/fly` para alternar voo.

O comando está disponível para VIP, VIP+, VIP++, SUP, MOD, ADM e DONO. Também aceita a permissão técnica `atlas.fly` para ajustes futuros por cargo. Ao desativar, jogadores fora do criativo/espectador perdem o estado de voo imediatamente.

---

v1.29.4

Adicionados kits VIP ao `/kits`.

O menu agora possui três linhas e exibe também Kit VIP, Kit VIP+ e Kit VIP++. Cada kit possui cooldown semanal e restrição por cargo, permitindo que cargos superiores resgatem os kits inferiores. Foram adicionados atalhos `/kit vip`, `/kit vip+`, `/kit vipplus`, `/kit vip++` e `/kit vipplusplus`.

---

v1.29.5

Kits VIP reformulados conforme a tabela final de benefícios.

VIP, VIP+ e VIP++ agora possuem kits Diário, Semanal e Mensal separados. VIP++ pode resgatar também os kits VIP e VIP+. Foram adicionados itens Cobblemon como Exp. Candy, Revive, Max Revive, Lucky Egg, Ability Capsule, Ability Patch, Destiny Knot, Everstone e Master Ball, além de Bottle Caps do mod `Only Bottle Caps`.

Mints aleatórias e Pedras de Evolução aleatórias são sorteadas automaticamente. Kits VIP++ com “Mint à escolha” agora abrem uma GUI própria para o jogador selecionar a mint desejada.

---

v1.29.6

Adicionado `/ec` com alias `/enderchest`.

O comando abre o Ender Chest remoto do jogador e está disponível para VIP, VIP+, VIP++, SUP, MOD, ADM e DONO. Também aceita a permissão técnica `atlas.ec` para ajustes futuros por cargo.

---

v1.29.7

Adicionadas as variações visuais de VIP.

O Atlas agora possui `VIP`, `VIP ✦` e `VIP ✦✦` como cargos separados, mantendo a hierarquia abaixo da Staff e acima de Player. O `/rank set` aceita aliases como `vipplus`, `vip+`, `vipestrela`, `vipplusplus`, `vip++` e `vipestrelas`, mas exibe os cargos com o símbolo `✦` no TAB, nametag, `/rank list` e menus dos kits.

---

v1.29.8

Adicionado chat colorido para VIPs e Staff.

Jogadores com VIP, VIP ✦, VIP ✦✦, SUP, MOD, ADM ou DONO podem usar códigos com `&` no chat, como `&cMensagem vermelha`, `&aMensagem verde`, `&lNegrito` e `&rReset`. Jogadores comuns continuam enviando o texto sem conversão de cores.

---

v1.29.9 (atualização de mundo)

O Lobby Emerald foi preparado em um mundo void/superflat autoral, removendo o
terreno legado e mantendo a base de construção de 129 × 129 blocos no spawn
`975.5 179 1573.5`. Foi criada uma ilha flutuante sob a base, com camadas
reduzidas de pedra, terra e deepslate e pontas de dripstone. As barreiras
invisíveis e as regras do lobby foram preservadas. Esta atualização é
operacional; o jar do Atlas Core permanece na versão `1.29.8`.

---

v1.29.10 (atualização de mundo)

Correção visual do Lobby Emerald: a antiga plataforma de quartzo, blocos
brancos e detalhes de esmeralda foram removidos completamente. A base foi
reconstruída como uma ilha flutuante natural, com superfície de grama, camadas
de terra, pedra e deepslate e cone inferior de dripstone. As barreiras
invisíveis de proteção foram restauradas após a reconstrução.

---

v1.29.11

Corrigida a autorização do WorldEdit para a sintaxe de dupla barra (`//set`,
`//pos1`, `//pos2`, `//wand` e demais comandos). Dono/OWNER e ADM/ADMIN são
reconhecidos pelo filtro global e continuam sendo os únicos cargos permitidos;
jogadores comuns permanecem bloqueados.

---

v1.29.12

Corrigido o `/wand`: o machado entregue agora é uma stack vanilla de
`minecraft:wooden_axe`, exatamente igual ao item configurado pelo WorldEdit,
sem nome ou componentes customizados que pudessem impedir o reconhecimento.

---

v1.29.13

Adicionado bypass total de comandos para `OWNER/DONO` após a autenticação. O
Dono agora pode executar todos os comandos registrados pelo servidor, inclusive
no Auth Hub, enquanto a proteção antes do login permanece ativa.
