# Mods Cobblemon Addons

Este documento registra o pacote de mods extras adicionado ao servidor de testes do Atlas.

## Objetivo

Complementar o Cobblemon com recursos de gameplay, decoração, batalhas, raids, navegação e qualidade de vida, mantendo o servidor validado antes de liberar testes com amigos.

## Mods adicionados da pasta `modsadd`

Origem local:

```text
/home/somente/dev/modsadd
```

Mods instalados:

- `CobbleDollars-fabric-2.0.0+Beta-5.1+1.21.1.jar`
- `CobbleFurnies-fabric-1.0.jar`
- `CobbleverseBadges-1.3.jar`
- `Cobbreeding-fabric-2.2.0.jar`
- `MoreCobblemonTweaks-fabric-1.3.3.jar`
- `Only Bottle Caps-1.3.0.jar`
- `cobblecuisine-2.0.1-1.7-rc1.jar`
- `cobblemon-additions-4.1.6.jar`
- `cobblemon-battle-extras-fabric-1.12.42.jar`
- `cobblemon-battle-positions-1.1.3.jar`
- `cobblemonraiddens-fabric-0.10.0+1.21.1.jar`
- `cobblenav-fabric-2.3.2.jar`
- `mega_showdown-fabric-1.7.3+1.7.3+1.21.1.jar`
- `sophisticatedbackpacks-1.21.1-3.23.4.3.106.jar`
- `sophisticatedcore-1.21.1-1.2.9.21.168.jar`
- `sophisticatedstorage-1.21.1-1.3.7.9.139.jar`

## Dependências adicionadas

Dependências baixadas e instaladas para permitir o boot do servidor:

- `architectury-13.0.8-fabric.jar`
- `cloth-config-15.0.140-fabric.jar`
- `athena-fabric-1.21.1-4.0.6.jar`
- `rctapi-fabric-1.21.1-0.15.2-beta.jar`
- `geckolib-fabric-1.21.1-4.9.2.jar`
- `accessories-fabric-1.1.0-beta.53+1.21.1.jar`
- `owo-lib-0.13.0-alpha.15+1.21.jar`
- `ForgeConfigAPIPort-v21.1.6-1.21.1-Fabric.jar`
- `energy-4.1.0.jar`

## Backup antes da instalação

Antes de instalar os addons, a pasta de mods do servidor foi arquivada em:

```text
/opt/atlas/server/backups/mod-versions/mods-pre-cobblemon-addons-2026-07-04.tar.gz
```

## Validação realizada

Validações concluídas:

- dependências principais conferidas por `fabric.mod.json`;
- hashes dos downloads do Modrinth conferidos contra a API;
- servidor reiniciado com o novo pacote;
- boot concluído sem erro fatal;
- serviço `atlas` ficou `active`;
- comando `/atlas tps` respondeu corretamente;
- servidor iniciou com 33 JARs na pasta `mods`.

## Observações importantes

### Pacote do cliente obrigatório

Com esses addons, os jogadores precisam instalar o mesmo pacote de mods no cliente.

Se o jogador tentar entrar sem o pacote correto, pode acontecer:

- queda ao conectar;
- erro de registro de itens/blocos;
- itens invisíveis;
- recipes/crafts demorando ou não sincronizando corretamente;
- diferença entre conteúdo do servidor e do cliente.

### Crafts demorando para aparecer

Após adicionar muitos mods, o primeiro carregamento de receitas pode demorar mais no cliente. Isso tende a ser mais perceptível:

- no primeiro login após instalar o pacote;
- em computadores mais fracos;
- quando o cliente ainda está indexando recipes novas.

Se o problema persistir depois de alguns minutos, validar:

- se o cliente está usando exatamente os mesmos mods;
- se não há versão duplicada de dependência;
- se o log do cliente mostra erro de recipe ou datapack.

### CobbleDollars e economia Atlas

O `CobbleDollars` foi adotado como fonte oficial da economia Atlas.

Atlas Coins e CobbleDollars passam a representar a mesma moeda em jogo. Os comandos do Atlas devem usar a ponte documentada em `ECONOMY.md`, evitando moedas paralelas ou saldos divergentes.

### Worldgen e chunks já gerados

Mods que adicionam estruturas ou geração de mundo podem não aparecer em chunks já pré-gerados.

Para validar conteúdo de worldgen:

- testar em chunks novos;
- revisar configurações do mod;
- evitar regenerar mapa de produção sem backup.

## Pacote para amigos

Sempre que atualizar os mods do servidor, gerar um novo pacote de cliente e enviar aos testadores.

O pacote deve conter:

- Fabric API;
- Cobblemon;
- todos os addons acima;
- todas as dependências acima.

O pacote não precisa conter mods exclusivamente de servidor, como o Atlas Core.

## Atualização de modpack — 2026-07-05 v2

Novo pacote gerado:

```text
/home/somente/dev/atlas/atlas-client-modpack-2026-07-05-v2.tar.gz
```

Tamanho aproximado:

```text
657 MB
```

O crescimento de tamanho veio principalmente do resource pack `CobbleSounds[Complete]`, que possui muitos arquivos de áudio.

### Adicionado ao servidor

Instalado e validado no servidor:

- `SimpleTMs-fabric-2.3.3.jar`

Motivo:

- adiciona TMs e TRs para Cobblemon;
- compatível com Minecraft `1.21.1`;
- compatível com Cobblemon `>=1.7.1`;
- o Atlas usa Cobblemon `1.7.3`.

Backup antes da instalação:

```text
/opt/atlas/server/backups/mod-versions/mods-pre-simpletms-20260705-233538.tar.gz
```

### Adicionado ao pacote do cliente

Mods adicionados ao pacote de cliente:

- `SimpleTMs-fabric-2.3.3.jar`
- `easy_npc-fabric-1.21.1-6.0.21.jar`
- `easy_npc_config_ui-fabric-1.21.1-6.0.21.jar`
- `xaerominimap-fabric-1.21.1-26.1.0.jar`

Resource packs adicionados ao pacote de cliente:

- `CobbleSounds[Complete]_v1.4.1.zip`
- `Cobblemon Interface v1.6.0.zip`
- `Xaeros Cobblemon Icons v2.1.zip`

## Atualização de modpack — 2026-07-07 v3-lite

Novo pacote recomendado para testes:

```text
/home/somente/dev/atlas/atlas-client-modpack-2026-07-07-v3-lite.tar.gz
```

Tamanho aproximado:

```text
258 MB
```

Motivo da revisão:

- o pacote v2 tinha `657 MB`;
- o `CobbleSounds[Complete]` sozinho tinha aproximadamente `488 MB`;
- a maior parte do peso vinha de músicas de bioma/mundo;
- isso poderia travar clientes mais fracos durante o carregamento em `Entrando no mundo...`.

Alterações:

- removido `CobbleSounds[Complete]_v1.4.1.zip` do pacote padrão;
- criado `CobbleSounds[BattleOnly]_v1.4.1-atlas-lite.zip`;
- mantidos os sons de batalha do Cobblemon;
- removidas músicas globais de mundo/bioma do CobbleSounds;
- removido `easy_npc_config_ui-fabric-1.21.1-6.0.21.jar` do pacote padrão dos jogadores.

Validação:

- arquivo `.tar.gz` listado com sucesso;
- resource pack BattleOnly validado com `ZipFile.testzip`;
- 66 arquivos `.ogg` de batalha preservados;
- 0 músicas de mundo/bioma preservadas;
- `assets/minecraft/sounds.json` removido para evitar referências quebradas às músicas excluídas.

Decisão:

O v3-lite passa a ser o pacote recomendado para jogadores. O CobbleSounds completo deve ficar opcional para quem tiver máquina melhor e quiser a experiência musical completa.

## Atualização de modpack — 2026-07-07 v4-nosounds

Pacote de diagnóstico sem CobbleSounds:

```text
/home/somente/dev/atlas/atlas-client-modpack-2026-07-07-v4-nosounds.tar.gz
```

Tamanho aproximado:

```text
168 MB
```

Motivo:

- o cliente continuou desconectando durante `Entrando no mundo...`;
- para isolar completamente a camada de áudio, removemos qualquer versão do CobbleSounds do pacote;
- esse pacote deve ser usado como teste principal de conexão.

Resource packs mantidos:

- `Cobblemon Interface v1.6.0.zip`
- `Xaeros Cobblemon Icons v2.1.zip`

Resource packs removidos:

- `CobbleSounds[Complete]_v1.4.1.zip`
- `CobbleSounds[BattleOnly]_v1.4.1-atlas-lite.zip`

Validação:

- `.tar.gz` aberto e listado com sucesso;
- nenhuma entrada contendo `CobbleSounds` ou `cobblesounds`;
- `easy_npc_config_ui` permanece fora do pacote padrão dos jogadores;
- servidor validado com `20.00 TPS`.

Decisão histórica:

O `v4-nosounds` foi usado para diagnosticar os timeouts em `Entrando no mundo...`, mas foi substituído nos testes seguintes.

## Atualização de modpack — 2026-07-07 v7-current

Pacote histórico:

```text
/home/somente/dev/atlas/atlas-client-modpack-2026-07-07-v7-current.tar.gz
```

Tamanho aproximado:

```text
144 MB
```

Motivo:

- alinhar o cliente exatamente com a pasta `mods` atual do servidor de testes;
- remover pacotes antigos de diagnóstico (`v3-lite`, `v4-nosounds`, `v5-minconnect`, `v6-coreconnect`);
- manter apenas os mods atualmente ativos no servidor, exceto `atlas-core.jar`, que é exclusivo do servidor;
- manter recursos client-side úteis: Xaero Minimap, ícones Cobblemon para Xaero e Cobblemon Interface;
- manter CobbleSounds fora do pacote padrão até existir o `Atlas CobbleSongs Lite`.

Mods do pacote:

- `Cobblemon-fabric-1.7.3+1.21.1.jar`
- `ForgeConfigAPIPort-v21.1.6-1.21.1-Fabric.jar`
- `accessories-fabric-1.1.0-beta.53+1.21.1.jar`
- `architectury-13.0.8-fabric.jar`
- `athena-fabric-1.21.1-4.0.6.jar`
- `cloth-config-15.0.140-fabric.jar`
- `easy_npc-fabric-1.21.1-6.0.21.jar`
- `fabric-api-0.116.12+1.21.1.jar`
- `geckolib-fabric-1.21.1-4.9.2.jar`
- `owo-lib-0.13.0-alpha.15+1.21.jar`
- `rctapi-fabric-1.21.1-0.15.2-beta.jar`
- `sophisticatedbackpacks-1.21.1-3.23.4.3.106.jar`
- `sophisticatedcore-1.21.1-1.2.9.21.168.jar`
- `sophisticatedstorage-1.21.1-1.3.7.9.139.jar`
- `xaerominimap-fabric-1.21.1-26.1.0.jar`

Resource packs:

- `Cobblemon Interface v1.6.0.zip`
- `Xaeros Cobblemon Icons v2.1.zip`

Validação:

- `.tar.gz` listado com sucesso;
- os pacotes antigos foram removidos da raiz do projeto;
- o pacote contém `README-ATLAS-MODPACK.txt`;
- o conteúdo está alinhado com o servidor atual.

Observação:

Este pacote foi substituído depois que o trio Sophisticated causou problema de carregamento de mapa no cliente.

## Plano de áudio — CobbleSounds AtlasLite

Após remover o CobbleSounds completo do pacote padrão, a decisão é reaproveitar apenas algumas faixas selecionadas em um pacote leve próprio do Atlas, mantendo os IDs originais do CobbleSounds.

A curadoria completa está documentada em `SOUNDTRACK.md`.

Regras:

- não reinstalar o CobbleSounds completo como obrigatório;
- criar um resource pack leve com apenas as faixas usadas;
- manter músicas futuras documentadas até os sistemas correspondentes existirem;
- validar conexão e carregamento do cliente antes de recomendar o pacote para jogadores.

## Atualização de modpack — 2026-07-07 v8-cobblesongs-lite

Pacote histórico com trilha leve:

```text
/home/somente/dev/atlas/atlas-client-modpack-2026-07-07-v8-cobblesongs-lite.tar.gz
```

Resource pack separado:

```text
/home/somente/dev/atlas/Atlas-CobbleSongs-Lite-v1.0.0.zip
```

Tamanho aproximado:

```text
169 MB
```

Alterações em relação ao `v7-current`:

- adicionado `Atlas-CobbleSongs-Lite-v1.0.0.zip` em `resourcepacks/`;
- mantidos os mesmos mods do servidor atual;
- mantidos `Cobblemon Interface` e `Xaeros Cobblemon Icons`;
- mantido o CobbleSounds completo fora do modpack padrão.

Validação:

- `Atlas-CobbleSongs-Lite-v1.0.0.zip` validado com `ZipFile.testzip`;
- modpack `v8-cobblesongs-lite` listado com sucesso;
- 15 JARs e 3 resource packs no pacote;
- o resource pack lite contém 12 faixas.

Resultado do teste:

O pacote customizado com IDs `atlas.music.*` não tocou corretamente no cliente. Ele foi substituído por `CobbleSounds[AtlasLite]_v1.4.1.zip`, preservando os IDs originais.

## Atualização de modpack — 2026-07-07 v9-nosophisticated-cobblesongs-lite

Pacote histórico para diagnóstico:

```text
/home/somente/dev/atlas/atlas-client-modpack-2026-07-07-v9-nosophisticated-cobblesongs-lite.tar.gz
```

Tamanho aproximado:

```text
165 MB
```

Motivo:

- o cliente não carregava corretamente o mapa após adicionar o trio Sophisticated;
- `sophisticatedbackpacks`, `sophisticatedcore` e `sophisticatedstorage` foram removidos do servidor;
- o modpack do cliente foi alinhado novamente ao servidor;
- o `Atlas CobbleSongs Lite` foi mantido para continuar o teste da trilha sonora leve.

Mods removidos:

- `sophisticatedbackpacks-1.21.1-3.23.4.3.106.jar`
- `sophisticatedcore-1.21.1-1.2.9.21.168.jar`
- `sophisticatedstorage-1.21.1-1.3.7.9.139.jar`

Backup antes da remoção:

```text
/opt/atlas/server/backups/mod-versions/mods-pre-remove-sophisticated-20260707-232837.tar.gz
```

Validação:

- servidor reiniciado sem os três mods;
- `v9` validado sem entradas contendo `sophisticated`;
- servidor estabilizou em `20.00 TPS`;
- os warnings de datapack ausente podem aparecer por histórico do mundo, mas não impediram o boot.

## Atualização de modpack — 2026-07-07 v10-cobblesounds-atlaslite

Pacote recomendado atual:

```text
/home/somente/dev/atlas/atlas-client-modpack-2026-07-07-v10-cobblesounds-atlaslite.tar.gz
```

Resource pack separado:

```text
/home/somente/dev/atlas/CobbleSounds[AtlasLite]_v1.4.1.zip
```

Tamanho aproximado:

```text
165 MB
```

Motivo:

- manter o servidor e o cliente sem `Sophisticated Backpacks/Core/Storage`, pois o mapa voltou a carregar sem eles;
- substituir o pack `Atlas-CobbleSongs-Lite-v1.0.0.zip`, que usava IDs customizados e não tocou no cliente;
- recriar o lite no mesmo padrão do CobbleSounds original, preservando os IDs como `cobblesounds:rustboro_city_hoenn2`;
- manter apenas as 12 faixas aprovadas.

Validação:

- `CobbleSounds[AtlasLite]_v1.4.1.zip` validado com `ZipFile.testzip`;
- o modpack `v10-cobblesounds-atlaslite` foi listado com sucesso;
- 12 JARs e 3 resource packs no pacote;
- nenhuma entrada contendo `sophisticated`;
- resource pack contém 12 faixas e `assets/cobblesounds/sounds.json` com IDs originais.

### Observações sobre Xaero

O `xaerominimap-fabric-1.21.1-26.1.0.jar` inclui o `XaeroLib` internamente em:

```text
META-INF/jars/xaerolib-fabric-1.21.1-1.1.15.jar
```

Por isso não foi necessário baixar um jar separado de `XaeroLib`.

## Atualização de modpack — 2026-07-09 v11-cobblesounds-themefix

Pacote atual:

```text
/home/somente/dev/atlas/atlas-client-modpack-2026-07-09-v11-cobblesounds-themefix.tar.gz
```

Motivo:

- o `CobbleSounds[Complete]` tocava músicas porque incluía aliases em `assets/minecraft/sounds.json`;
- o `CobbleSounds[AtlasLite]` anterior tinha apenas IDs diretos em `assets/cobblesounds/sounds.json`;
- o `WorldThemeService` ainda tocava discos vanilla, então os temas escolhidos não eram chamados pelo servidor.

Alterações:

- `CobbleSounds[AtlasLite]_v1.4.1.zip` foi refeito;
- adicionados aliases mínimos em `assets/minecraft/sounds.json`;
- corrigida a faixa `surfing_hoenn2`;
- o modpack v11 mantém Sophisticated removido;
- o pacote permanece com 12 JARs e 3 resource packs.

Temas esperados com `atlas-core` atualizado:

- Auth Lobby / Hub: `cobblesounds:rustboro_city_hoenn2`;
- Lobby Emerald: `cobblesounds:introductions_hoenn`;
- Survival Emerald: `cobblesounds:route1_sinnoh`.

### Não instalado: Tim's TMs

O mod `Cobblemon Tim's TMs` foi avaliado, mas não foi instalado.

Motivo:

```text
depends: cobblemon >=1.6.1 <1.7.0
```

Como o Atlas usa Cobblemon `1.7.3`, esse mod poderia impedir o servidor de iniciar.

### Não instalado: CobbleTowns

O datapack `CobbleTowns v1.0.2` foi baixado apenas para análise, mas não foi ativado no mundo.

Motivo:

- publicado para Minecraft `1.20.1`;
- `pack.mcmeta` informa `supported_formats: [18, 26]`;
- o servidor Atlas está em Minecraft `1.21.1`;
- ativar datapack de worldgen antigo pode falhar no boot ou gerar estruturas incorretas.

Decisão:

- manter CobbleTowns como pendente;
- procurar uma versão atualizada para `1.21.1`;
- ou criar/adaptar estruturas próprias do Atlas futuramente.

### Validação da atualização

Após instalar `SimpleTMs` no servidor:

- servidor reiniciou com sucesso;
- `SimpleTMs` registrou itens, blocos e datapack;
- Easy NPC persistiu o NPC `Lobby Emerald`;
- comando `/atlas tps` respondeu;
- TPS estabilizou em `20.00`.
