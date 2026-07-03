# Home System

O sistema de homes do Atlas foi inspirado nas funções centrais do Ultra SetHome, adaptadas ao Fabric, PostgreSQL e cargos próprios do servidor.

## Comandos

- `/sethome <nome>` cria ou atualiza uma home no Survival Emerald.
- `/home` teleporta para a home principal, inicialmente a primeira criada.
- `/home <nome>` teleporta para uma home específica.
- `/delhome <nome>` remove uma home.
- `/homes` lista as homes e o limite atual.

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
