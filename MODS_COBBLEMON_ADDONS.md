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
