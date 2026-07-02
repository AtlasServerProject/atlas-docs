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
X: 646
Y: 83
Z: 3535
Orientação: oeste (90°)
```

O raio aleatório do spawn está desativado. Toda conexão é teleportada para o
centro do bloco (`646.5 83 3535.5`), inclusive quando o jogador já possui uma
posição anterior salva.

## Seletor

Depois da autenticação, uma bússola abrirá o menu de servidores. A primeira opção
será o Emerald. O seletor será a fronteira entre a autenticação global e os
servidores de gameplay, permitindo substituir o transporte local por uma conexão
via proxy no futuro.

## Lobby Emerald

O Lobby Emerald será o hub do primeiro servidor do Atlas. Ele concentrará acesso
ao Survival Emerald, NPCs, crates, rankings, tutorial, loja, eventos, scoreboard
e navegação.

O comando `/spawn` levará o jogador ao spawn do hub correspondente ao servidor
em que ele estiver. No Emerald, por exemplo, o jogador poderá sair do Survival
Emerald e retornar ao Lobby Emerald. O comando não deve ignorar a autenticação
nem transportar silenciosamente o jogador entre servidores diferentes.

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
