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

Durante testes com jogadores, a geração pode ser pausada e retomada sem perder progresso:

```bash
infra/scripts/atlas-cli pregenerate-survival pause
infra/scripts/atlas-cli pregenerate-survival continue
```

## Retorno ao Lobby Emerald

Jogadores autenticados dentro do Survival Emerald podem executar `/lobby emerald`. O comando os leva ao spawn do Lobby Emerald em `975.5 179 1573.5` e remove a posição de retorno salva.

## Persistência da posição

A posição no Survival Emerald é salva no PostgreSQL a cada 30 segundos e ao desconectar. Ao reconectar ou após um reinício, o jogador autentica normalmente e retorna ao mesmo ponto, mesmo que ainda não tenha criado uma home.

A posição persistente é removida somente quando:

- o jogador morre no Survival Emerald e retorna ao Lobby Emerald;
- o jogador escolhe sair com `/lobby emerald`.

## Teleporte aleatório

No Lobby Emerald, o comando `/rtp` envia o jogador para um terreno seguro do Survival Emerald, entre 500 e 2850 blocos do centro. O mesmo comando pode ser usado novamente dentro do Survival para trocar de região. Água, lava, blocos de magma, espaços obstruídos e posições fora da borda são rejeitados. Dentro do Survival, `/lobby emerald` realiza o caminho de volta.

A busca continua em segundo plano até encontrar um destino válido. Ela não é encerrada por falta de um local nas primeiras tentativas, não consome o cooldown antes do teleporte e não cria solicitações duplicadas quando o jogador repete o comando.

Para reduzir o tempo de espera, o servidor mantém uma fila de 32 destinos previamente carregados e validados. Cada uso consome um destino e a reserva é reabastecida gradualmente, seguindo a estratégia de fila usada pelo BetterRTP sem bloquear o tick do servidor.

Após executar `/rtp`, o jogador deve permanecer parado durante três segundos. Qualquer deslocamento cancela a solicitação, devolve o destino reservado à fila e não aplica cooldown. Olhar ao redor continua permitido.

Cooldown entre usos:

| Cargo | Tempo |
|---|---:|
| Dono / ADM | Instantâneo |
| MOD / SUP | 1 minuto |
| VIP++ | 1 minuto |
| VIP+ | 1 minuto e 50 segundos |
| VIP | 2 minutos e 30 segundos |
| Player | 3 minutos |
