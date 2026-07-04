# Claims do Atlas

O sistema de claims será inspirado no fluxo de uso do GriefPrevention, mas implementado diretamente no Atlas Core para Fabric e PostgreSQL.

## Escopo inicial

- Claims disponíveis somente em `atlas:survival_emerald`.
- Seleção de dois cantos com pá dourada.
- Inspeção da área com graveto.
- Proteção 2D cobrindo toda a altura do mundo.
- Tamanho mínimo de 10 × 10 blocos.
- Proibição de sobreposição.
- Limite total de área definido pelo maior cargo do jogador.

## Confiança

Os níveis são cumulativos:

1. `ACCESS`: portas, botões e interações simples.
2. `CONTAINER`: nível anterior mais baús e contêineres.
3. `BUILD`: níveis anteriores mais quebra e colocação de blocos.

O proprietário sempre possui controle total. Dono e ADM possuem bypass administrativo, e cada uso é auditado no PostgreSQL com jogador, ação, claim, mundo, coordenadas e horário.

## Comandos disponíveis

- `/trust <jogador>`
- `/containertrust <jogador>`
- `/accesstrust <jogador>`
- `/untrust <jogador>`
- `/abandonclaim`
- `/claimslist`

O `/claimslist` exibe cada claim como uma linha clicável. O botão `[TELEPORTAR]` procura um ponto seguro dentro da claim e permite acesso somente ao proprietário.

## Proteções indiretas

- Explosões não destroem blocos protegidos.
- Pistões não movem nem empurram blocos para dentro ou para fora de claims.
- Fluidos não avançam sobre áreas protegidas.
- Fogo não se espalha nem consome blocos dentro de claims.
- Ataques e interações de terceiros com entidades e Pokémon são bloqueados.

Ao selecionar ou inspecionar uma claim, blocos de ouro falsos exibem temporariamente seu perímetro. Esses blocos existem apenas para o cliente do jogador, não alteram o mapa e são restaurados automaticamente.

## Limites de área

- Player: 10.000 blocos.
- VIP: 20.000 blocos.
- VIP+: 30.000 blocos.
- VIP++: 50.000 blocos.
- MOD e SUP: 100.000 blocos.
- Dono e ADM: 1.000.000 de blocos.

O limite é a soma da área de todas as claims do jogador. Cada claim precisa medir ao menos 10 × 10 blocos.
