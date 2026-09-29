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

## Ferramentas da staff — v1.29.17

- `/freeze <jogador>`: congela/descongela jogador online. Bloqueia movimento,
  interações, inventário e comandos de gameplay; permite chat/autenticação e evita dano.
- `/invsee <jogador>`: inventário (três linhas), hotbar (quarta linha), botas,
  calças, peitoral, capacete e mão secundária (quinta linha).
- `/endersee <jogador>`: 27 espaços do Ender Chest.

Consultas são **somente leitura**, atualizadas enquanto o menu está aberto.
É necessário ser staff autenticada, fora do Auth Hub, com cargo superior ao alvo.
Consulta própria é permitida. Congelar a si mesmo não é permitido.
O console pode usar freeze; consultas precisam ser executadas por jogador.

O freeze continua após reconexão durante a mesma execução do servidor e é
removido ao repetir o comando ou reiniciar o servidor. A reconexão gera registro
no log; não causa banimento automático. As consultas e mudanças de freeze também
ficam registradas no log. Não há leitura de inventários de jogadores offline.

### Checklist de validação das ferramentas

- Player sem cargo staff não consegue executar os três comandos.
- Staff não consegue atuar sobre cargo igual ou superior.
- Freeze impede movimento, interações e comandos de gameplay; repetir libera.
- Reconectar não libera o freeze durante a mesma execução do servidor.
- InvSee/EnderSee não permitem retirar itens por clique, Shift, arraste ou hotbar.
- Consultas fecham quando o alvo desconecta ou a autorização deixa de existir.

Build e inicialização da v1.29.17 aprovados; este checklist em jogo está pendente.

## StaffMode

Implementado na v1.29.18: `/staffmode` (`/staff`) com `on`, `off` e `tp <jogador>`.
Veja [STAFFMODE.md](STAFFMODE.md) para restauração, restrições e testes pendentes.

## Notas internas e histórico unificado

A v1.29.19 adiciona `/staffnotes` e `/history`, com autenticação, hierarquia, paginação e arquivamento auditável. Consulte [Staff Notes e Histórico](STAFF-NOTES.md).
