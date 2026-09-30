# Arquitetura dos Lobbys do Atlas

## Fluxo inicial

```text
Entrada
  ↓
Auth Lobby
  ↓
Login, registro ou autenticação Premium
  ↓
Bússola de servidores
  ↓
Lobby Emerald
  ↓
Survival Emerald
```

O Auth Lobby não envia o jogador automaticamente ao Emerald. Após autenticar, o
jogador permanece no mesmo lobby e recebe acesso ao seletor de servidores.

## Auth Lobby

Responsável exclusivamente pela entrada e autenticação. Antes do login, o Atlas
bloqueia movimentação, chat e comandos, exceto `/login` e `/register`. O jogador
não pode receber nenhum tipo de dano enquanto ainda não estiver autenticado.
As demais proteções previstas incluem inventário, blocos e interações.

Nos lobbys, jogadores autenticados também não devem receber dano de queda. Essa
regra evita mortes acidentais em mapas grandes e verticais sem interferir no
dano normal dos servidores de gameplay.

O Auth Lobby não oferece a seleção de Pokémon inicial. Conta, autenticação e
seleção de servidor são as únicas experiências permitidas nesse ambiente.

O mapa `Lobby Hub` foi adotado como Auth Lobby. Antes da implantação, foram
removidos dados legados de jogadores, inventários, Pokémon, Pokédex, estatísticas
e advancements. Mensagens promocionais e links externos também foram removidos.

Spawn global inicial:

```text
X: 642.215
Y: 126
Z: 3534.426
Orientação: oeste (`yaw 91.8`, `pitch -3.4`)
```

O raio aleatório do spawn está desativado. Toda conexão é teleportada para o
posição exata (`642.215 126 3534.426`), inclusive quando o jogador já possui uma
posição anterior salva.

Na versão `v1.26.4`, o `minecraft:overworld` do Auth Lobby foi resetado para
um mundo void/superflat próprio do Atlas, removendo o uso do mapa externo
anterior. A build atual é uma plataforma autoral inicial com spawn, NPC de
navegação e barreiras invisíveis.

## Seletor

Depois da autenticação, uma bússola abrirá o menu de servidores. A primeira opção
será o Emerald. O seletor será a fronteira entre a autenticação global e os
servidores de gameplay, permitindo substituir o transporte local por uma conexão
via proxy no futuro.

## Lobby Emerald

O Lobby Emerald será o hub do primeiro servidor do Atlas. Ele concentrará acesso
ao Survival Emerald, NPCs, crates, rankings, tutorial, loja, eventos, scoreboard
e navegação.

O mapa está instalado como a dimensão `atlas:emerald`. O seletor envia o jogador
para a posição configurada no novo mapa (v1.29.20):

```text
X: 918.5302583016859
Y: 71.0
Z: 3838.5058040626927
Yaw: 179.39441° (quase norte)
Pitch: -1.7545054°
```

Fora dos chunks existentes, a dimensão utiliza geração vazia para impedir a
criação de terreno aleatório ao redor do lobby. A antiga base media 129 × 129 blocos
(X 911–1039, Z 1509–1637, topo em Y 178) e era protegida por barreiras
invisíveis laterais e superiores.

Em 14/07/2026, a plataforma de quartzo e os elementos decorativos antigos foram
removidos. Naquela etapa, o lobby recebeu uma ilha flutuante autoral completa: a superfície é
de grama, seguida por terra, pedra e deepslate em camadas progressivamente
menores, terminando em um núcleo pontudo de dripstone próximo de Y 145. O topo
ficou livre para a construção dos NPCs, tutorial, rankings, crates e demais
elementos do hub.

Em 29/09/2026, todos os blocos de `atlas:emerald` foram removidos a pedido do usuário,
incluindo ilha e barreiras. A limpeza ocorreu com o servidor ligado, sem mover o
jogador e sem reinício. Foram limpos 90 chunks; após salvar, a leitura dos 3.736
chunks existentes confirmou nenhuma seção com blocos diferentes de ar. Os chunks
carregados temporariamente para manutenção foram liberados.

Após outras limpezas solicitadas, o usuário instalou um novo mapa e confirmou o término da colagem. Na v1.29.20, a posição e a rotação de chegada foram capturadas diretamente do personagem no portal do novo lobby. O seletor, `/lobby emerald` e os retornos ao Emerald pelo serviço de viagem usam esse destino. Auth Lobby e Survival não foram alterados.

Backup anterior à limpeza:
`/opt/atlas/server/backups/emerald-before-clear-20260929T173530Z.tar.gz`.

Após autenticar no Auth Lobby, o jogador recebe uma bússola protegida no slot
central da barra rápida. Ela abre um menu de nove slots que, no lançamento,
contém apenas o Lobby Emerald. A bússola não pode ser movida ou descartada, é
removida ao entrar no Emerald e restaurada automaticamente ao retornar ao Auth
Lobby.

Jogadores não recebem dano de queda no Lobby Emerald. Diferente do Auth Lobby,
o Emerald permite que cada jogador escolha seu Pokémon inicial.

Os Pokémon selvagens do lobby seguem uma whitelist de espécies fracas de rotas
iniciais. Atualmente são permitidos:

```text
Bidoof, Bunnelby, Caterpie, Fletchling, Goldeen, Hoothoot, Lechonk,
Lillipup, Magikarp, Patrat, Pidgey, Pidove, Pikipek, Rattata,
Rookidee, Sentret, Skwovet, Starly, Tarountula, Weedle, Wurmple,
Yungoos e Zigzagoon.
```

Qualquer espécie fora da lista é cancelada antes do spawn e removida caso seja
carregada de dados persistidos. Com isso, lendários, míticos, Ultra Beasts,
Paradoxos e demais Pokémon especiais não podem permanecer no Lobby Emerald.

O comando `/spawn` levará o jogador autenticado de volta ao Hub central do
Atlas. No lançamento, esse destino é o spawn do Auth Lobby, onde fica o seletor
de servidores. Assim, um jogador que estiver no Emerald poderá retornar ao Hub
e escolher novamente seu destino. O comando nunca ignora a autenticação.

## Hierarquia no TAB

A lista de jogadores deve obedecer à hierarquia visual abaixo, sem depender do
nome do jogador ou do ID interno do cargo no banco:

```text
Dono > ADM > MOD > SUP > VIPs > Players
```

Nenhum Player ou VIP pode aparecer acima de um membro da Staff.

## Evolução para Atlas Network

O lançamento terá somente o Emerald. Uma expansão futura poderá adicionar outros
servidores mantendo globais conta, autenticação, UUID, Premium, VIP, ranks,
amigos e Discord. Economia, Pokémon, GTS, crates, eventos e progressão continuarão
isolados por servidor.
