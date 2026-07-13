# Moderação do Atlas

O sistema de moderação do Atlas é próprio e registra punições no PostgreSQL.

## Comandos

| Comando | Uso |
| --- | --- |
| `/warn` | `/warn <jogador> <motivo>` |
| `/kick` | `/kick <jogador> <motivo>` |
| `/mute` | `/mute <jogador> <tempo\|perma> <motivo>` |
| `/unmute` | `/unmute <jogador> <motivo>` |
| `/ban` | `/ban <jogador> <motivo>` |
| `/unban` | `/unban <jogador> <motivo>` |
| `/atlasban` | `/atlasban <jogador> <motivo>` |
| `/atlasunban` | `/atlasunban <jogador> <motivo>` |
| `/banip` | `/banip <ip\|jogadorOnline> <motivo>` |
| `/unbanip` | `/unbanip <ip> <motivo>` |
| `/punishments` | `/punishments <jogador>` |

## Tempo

`/mute` aceita:

- `s`: segundos;
- `m`: minutos;
- `h`: horas;
- `d`: dias;
- `perma`: permanente.

Exemplos:

- `/mute Steve 10m spam`
- `/mute Steve 2h ofensa`
- `/mute Steve perma abuso grave`

## Hierarquia

Jogadores da staff podem punir apenas jogadores com prioridade de cargo menor.

O console não sofre essa limitação.

## Comportamento

- Mute bloqueia chat.
- Ban bloqueia entrada.
- BanIP bloqueia entrada pelo IP.
- Warn é privado.
- Kick desconecta imediatamente.

## Observação sobre `/ban`

O Minecraft possui um comando vanilla chamado `/ban`. Por isso o Atlas também fornece:

- `/atlasban`
- `/atlasunban`

Esses aliases evitam ambiguidade e usam diretamente o sistema de punições do Atlas.

O `/unban` do Atlas também remove banimentos vanilla quando encontra um jogador banido fora do histórico do Atlas.
