# StaffMode — v1.29.18

Primeira entrega de fiscalização baseada no modo espectador nativo do Minecraft.
Disponível apenas para staff autenticada, fora do Auth Hub e sem freeze.

## Comandos

- `/staffmode` ou `/staff`: alterna o modo.
- `/staffmode on` e `/staffmode off`: ativação/desativação explícita.
- `/staffmode tp <jogador>`: aproximação de jogador online autenticado, fora do
  Auth Hub e com cargo inferior. Consulta própria segue a regra dos comandos da staff.

## Funcionamento

Antes de ativar, salva no PostgreSQL o modo de jogo, a posição, orientação,
permissões e velocidades de voo/movimento. O jogador entra em espectador,
podendo voar e atravessar blocos. O inventário não é trocado nem esvaziado;
não são entregues ferramentas temporárias. Uma mensagem na barra de ação
identifica o modo ativo.

A visibilidade segue o espectador vanilla: esta entrega não implementa vanish
com remoção do TAB ou ocultação de outros espectadores. A navegação nativa do
espectador continua disponível; o teleporte pelo comando Atlas verifica hierarquia.

No modo, permanecem disponíveis moderação, `/invsee`, `/endersee`, `/freeze`,
mensagens privadas (`/msg`, `/tell`, `/w`), ajuda e autenticação. Comandos de
inventário/economia/gameplay, como `/kits`, `/pay`, `/give`, `/fly`, `/home` e
`/gamemode`, são bloqueados até sair. Variantes com namespace e `/execute` não
contornam essa lista. Interações com blocos, itens, entidades e alterações de
inventário também são bloqueadas; os menus de inspeção permanecem somente leitura.

A ativação é recusada durante batalha Cobblemon, aquecimento de home/RTP,
sono ou montaria. Os locais visitados durante fiscalização não substituem a
posição de Survival salva pelo Atlas. Ações são registradas no log.

## Saída e recuperação

- Saída manual: retorna à posição e ao modo/habilidades anteriores, inclusive
  voo que já estava habilitado. Fecha câmera de espectador e menus antes da restauração.
- Congelamento pela staff: encerra StaffMode antes de registrar a posição do freeze.
- Perda do cargo ou autenticação: encerra automaticamente o modo.
- Desconexão: restaura habilidades e mantém o registro de recuperação até o próximo login.
- Reconexão/quebra do processo: recupera o modo/habilidades pelo banco, respeitando
  o fluxo normal de autenticação no Auth Hub; não retorna diretamente ao Survival.
- Parada normal: tenta restaurar jogadores antes de salvar e encerrar o servidor.
- Falha do banco: não ativa sem salvar o estado; recuperação malsucedida no login
  recusa a conexão e mantém o registro para nova tentativa.

O estado vanilla é salvo antes de marcar a restauração como concluída no banco.
A migration `031_staff_mode_sessions.sql` mantém um registro por jogador e impede
sobrescrever uma sessão ainda ativa. O registro é marcado inativo após recuperação,
sem apagar o jogador ou seu inventário. Reativar cria um novo ponto de retorno.

## Validação

Teste automatizado: `python3 infra/tests/test_staff_mode.py`.
Executa o repositório Java e a política de comandos em PostgreSQL descartável;
verifica todos os campos, isolamento de jogadores, recuperação em nova conexão,
ativação repetida, encerramento idempotente e bloqueio de comandos/aliases.
Não utiliza nem altera o banco de produção.

Testes em jogo **pendentes**, pois o usuário não pode executá-los nesta etapa:

- Ativar/desativar em Survival, Creative e com `/fly` previamente habilitado.
- Conferir inventário, armadura, mão secundária, XP e posição antes/depois.
- Usar `/staffmode tp`, `/invsee`, `/endersee` e `/freeze` respeitando hierarquia.
- Tentar coletar, mover ou descartar itens e executar comandos de gameplay.
- Desconectar/reconectar e reiniciar o servidor durante o modo.
- Perder cargo/autenticação e conferir recuperação sem privilégios temporários.
- Conferir câmera de espectador e passagem para o Auth Hub.
