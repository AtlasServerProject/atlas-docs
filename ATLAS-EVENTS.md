# Atlas Events

Sprint responsável por eventos especiais de Pokémon no Atlas.

## Objetivo

Criar uma base controlada para eventos de Lendários, Ultra Beasts, Paradox e Míticos, com anúncio, acompanhamento em BossBar, desfecho claro e integração futura com Discord.

## Filosofia

Eventos devem gerar movimento no servidor sem virar bagunça ou pay-to-win.

Princípios:

- eventos são globais e anunciados;
- spawn precisa ser controlado pelo Atlas;
- o jogador deve entender onde procurar;
- o evento precisa ter começo, estado atual e fim;
- logs são obrigatórios para auditoria;
- recompensas especiais não devem quebrar economia nem progressão.

## Fluxo inicial planejado

```text
Evento agendado/manual
        ↓
Escolhe categoria
        ↓
Escolhe mundo/bioma elegível
        ↓
Anuncia no chat
        ↓
Exibe BossBar com tempo restante
        ↓
Pokémon aparece
        ↓
Monitora estado
        ↓
Capturado / derrotado / expirou / desapareceu
        ↓
Anuncia desfecho
        ↓
Registra log
```

## Categorias

- Lendários
- Ultra Beasts
- Paradox
- Míticos

## Componentes técnicos previstos

- `EventModule`
- `PokemonEventService`
- `PokemonEventRepository`
- `ActivePokemonEvent`
- `EventBossBarService`
- `EventAnnouncementService`
- `DiscordWebhookService`

## Comandos previstos

Comandos administrativos:

- `/atlas event start <categoria>`
- `/atlas event stop`
- `/atlas event status`
- `/atlas event reload`

Comandos públicos:

- `/evento`

## Dados que precisam ser registrados

- tipo do evento;
- espécie;
- mundo;
- bioma;
- coordenadas aproximadas ou região;
- horário de início;
- horário de término;
- responsável por iniciar, quando manual;
- jogador que capturou, se houver;
- motivo do encerramento.

## Desfechos

- capturado;
- derrotado;
- desapareceu;
- tempo expirado;
- cancelado pela staff.

## Primeira entrega sugerida

Para a primeira versão funcional, o menor corte seguro é:

- comando staff para iniciar evento manual;
- anúncio no chat;
- BossBar com tempo restante;
- spawn controlado de uma espécie configurada;
- encerramento por tempo;
- log no banco.

Depois disso entram captura, Discord, rotação automática e categorias avançadas.
