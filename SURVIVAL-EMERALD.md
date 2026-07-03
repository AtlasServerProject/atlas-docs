# Survival Emerald

O primeiro mundo de gameplay do Atlas é a dimensão `atlas:survival_emerald`.

## Dimensões

- Centro: `0, 0`.
- Tamanho: 6000 × 6000 blocos.
- Grade: 375 × 375 chunks.
- Limites: de aproximadamente `-3000` a `+3000` nos eixos X e Z.

Esse tamanho oferece espaço suficiente para uma comunidade inicial sem criar um mundo excessivamente pesado. A expansão poderá ser feita de forma planejada quando houver necessidade.

## Pré-geração

O Chunky renderiza todo o mundo antecipadamente. Isso evita que a exploração gere muitos chunks em tempo real e provoque travamentos.

```bash
infra/scripts/atlas-cli pregenerate-survival start
infra/scripts/atlas-cli pregenerate-survival status
```

A configuração `continueOnRestart` mantém a tarefa após reinicializações.

## Retorno ao Lobby Emerald

Jogadores autenticados dentro do Survival Emerald podem executar `/lobby`. O comando os leva ao spawn do Lobby Emerald em `975.5 179 1573.5`.
