# Survival Emerald

O primeiro mundo de gameplay do Atlas é a dimensão `atlas:survival_emerald`.

## Dimensões

- Centro: `0, 0`.
- Seed: `27594263`.
- Tamanho: 12000 × 12000 blocos.
- Grade: 750 × 750 chunks.
- Limites: de aproximadamente `-6000` a `+6000` nos eixos X e Z.

Esse tamanho oferece o dobro da área linear planejada inicialmente e permite que os addons de worldgen e estruturas tenham mais espaço para aparecer durante a exploração.

## Pré-geração

O Chunky renderiza todo o mundo antecipadamente. Isso evita que a exploração gere muitos chunks em tempo real e provoque travamentos.

```bash
infra/scripts/atlas-cli pregenerate-survival start
infra/scripts/atlas-cli pregenerate-survival status
```

A configuração `continueOnRestart` do Chunky fica desativada no servidor de testes. Isso impede que a pré-geração volte automaticamente após reinicializações e derrube o TPS sem intenção.

Durante testes com jogadores, a geração deve permanecer pausada. Ela pode ser pausada e retomada sem perder progresso:

```bash
infra/scripts/atlas-cli pregenerate-survival pause
infra/scripts/atlas-cli pregenerate-survival continue
```

Se o servidor ficar pesado ou o console administrativo retornar `Connection refused`, pare a pré-geração e aguarde o TPS estabilizar:

```bash
infra/scripts/atlas-cli pregenerate-survival pause
infra/scripts/atlas-cli exec "atlas tps"
```

O comando sem argumento apenas consulta o status:

```bash
infra/scripts/atlas-cli pregenerate-survival
```

Pré-geração de `12000 × 12000` blocos é pesada para a máquina atual. Rodar somente quando não houver jogadores online.

## Retorno ao Lobby Emerald

Jogadores autenticados dentro do Survival Emerald podem executar `/lobby emerald`. O comando os leva ao spawn do Lobby Emerald em `975.5 179 1573.5` e remove a posição de retorno salva.

## Persistência da posição

A posição no Survival Emerald é salva no PostgreSQL a cada 30 segundos e ao desconectar. Ao reconectar ou após um reinício, o jogador autentica normalmente e retorna ao mesmo ponto, mesmo que ainda não tenha criado uma home.

A posição persistente é removida somente quando:

- o jogador morre no Survival Emerald e retorna ao Lobby Emerald;
- o jogador escolhe sair com `/lobby emerald`.

## Teleporte aleatório

No Lobby Emerald, o comando `/rtp` envia o jogador para um terreno seguro do Survival Emerald, entre 500 e 5850 blocos do centro. O mesmo comando pode ser usado novamente dentro do Survival para trocar de região. Água, lava, blocos de magma, espaços obstruídos e posições fora da borda são rejeitados. Dentro do Survival, `/lobby emerald` realiza o caminho de volta.

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
