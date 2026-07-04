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

O proprietário sempre possui controle total. Dono e ADM terão bypass administrativo, com auditoria prevista antes da conclusão da Sprint.

## Comandos planejados

- `/trust <jogador>`
- `/containertrust <jogador>`
- `/accesstrust <jogador>`
- `/untrust <jogador>`
- `/abandonclaim`
- `/claimslist`

## Entregas posteriores

Proteções contra explosões, pistões, fluidos indiretos, fogo, entidades e Pokémon serão adicionadas em etapas e validadas separadamente.
