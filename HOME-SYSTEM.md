# Home System

O sistema de homes do Atlas foi inspirado nas funções centrais do Ultra SetHome, adaptadas ao Fabric, PostgreSQL e cargos próprios do servidor.

## Comandos

- `/sethome <nome>` cria ou atualiza uma home no Survival Emerald.
- `/home` teleporta para a home principal, inicialmente a primeira criada.
- `/home <nome>` teleporta para uma home específica.
- `/delhome <nome>` remove uma home.
- `/homes` abre o menu visual de homes, com limite e paginação.
- `/back` retorna para a última localização salva antes de teleportes manuais.

Os nomes aceitam de 1 a 16 caracteres: letras, números, `_` e `-`.

## Limites e cooldowns

| Cargo | Homes | Cooldown |
|---|---:|---:|
| Dono / ADM | 100 | Sem cooldown |
| MOD / SUP | 25 | Sem cooldown |
| VIP++ | 12 | 5 segundos |
| VIP+ | 8 | 10 segundos |
| VIP | 5 | 15 segundos |
| Player | 2 | 30 segundos |

## Segurança

- Homes só podem ser criadas no Survival Emerald.
- O chunk de destino é carregado antes do teleporte.
- O sistema procura espaço seguro próximo da posição salva.
- Locais obstruídos não teleportam o jogador e não aplicam cooldown.
- O teleporte possui aquecimento de três segundos.
- Movimento cancela sem aplicar cooldown; girar a câmera é permitido.
- `/back` salva a posição anterior antes de teleportes como `/lobby emerald`, `/spawn`, `/home`, `/claimtp` e `/rtp`.
- Usar `/back` troca a posição atual pela anterior, permitindo voltar e retornar novamente.

## GUI — v1.29.16

`/homes` abre **Homes do Atlas**, um container de seis linhas no servidor.
Não exige mod adicional no cliente. Disponível após autenticação, fora do Auth Hub.

- 28 posições por página, com navegação para acomodar até 100 homes.
- Cama verde: principal; cama azul: demais homes.
- Clique esquerdo: inicia o mesmo teleporte seguro de `/home`.
- Shift + clique esquerdo: define a principal no PostgreSQL.
- Clique direito: confirma atualização da posição no Survival Emerald.
- Modo excluir: clique na home e confirme a exclusão; cancelar não altera dados.
- Mapa vazio ou bússola: confirma criação na posição atual do Survival Emerald.
- Criações pelo menu usam o primeiro nome disponível `home1`, `home2`, etc.
  Para nomes personalizados, usar `/sethome <nome>`.
- Vidro vermelho: posição bloqueada pelo limite do cargo, com limites no texto de ajuda.
- Relógio: tempo restante do cooldown, atualizado enquanto o menu está aberto.
- Barreira: fecha o menu; vidro cinza preenche os espaços sem ação.

O inventário visual bloqueia coleta de ícones, hotbar swap, arraste, descarte,
clone e clique duplo. Limites, mundo e existência da home são conferidos nas ações.
Após excluir a principal, uma home restante assume esse papel.
`/home` e `/home <nome>` mantêm o comportamento anterior.

## Validação em jogo

GUI testada e aprovada pelo usuário em 2026-09-27. Checklist de regressão:

- Criar, atualizar, cancelar e excluir pelo menu.
- Escolher principal e conferir `/home` após reconectar.
- Navegar páginas com Staff e conferir limites com Player/VIP.
- Tentar retirar ícones com Shift, teclas numéricas, arraste e clique duplo.
- Conferir cooldown, movimento durante aquecimento e destino obstruído.
