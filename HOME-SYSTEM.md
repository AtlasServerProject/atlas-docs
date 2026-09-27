# Home System

O sistema de homes do Atlas foi inspirado nas funções centrais do Ultra SetHome, adaptadas ao Fabric, PostgreSQL e cargos próprios do servidor.

## Comandos

- `/sethome <nome>` cria ou atualiza uma home no Survival Emerald.
- `/home` teleporta para a home principal, inicialmente a primeira criada.
- `/home <nome>` teleporta para uma home específica.
- `/delhome <nome>` remove uma home.
- `/homes` lista as homes e o limite atual.
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

## GUI planejada

O comando `/homes` deve evoluir de lista em texto para um menu visual simples, inspirado no fluxo do Ultra SetHome, mas com identidade própria do Atlas.

### Menu principal

Título:

```text
Homes do Atlas
```

Layout previsto:

- 6 linhas.
- Slots centrais para homes existentes.
- Linha inferior reservada para ações.
- Slots vazios preenchidos com vidro cinza para reduzir clique acidental.

### Ícones

| Função | Ícone sugerido | Ação |
|---|---|---|
| Home principal | Cama verde ou esmeralda | Clique teleporta para a home principal |
| Home comum | Cama colorida | Clique teleporta para a home escolhida |
| Slot disponível | Mapa vazio | Clique cria home na posição atual, quando permitido |
| Slot bloqueado por limite | Vidro vermelho ou barreira | Mostra o cargo necessário para liberar mais homes |
| Cooldown ativo | Relógio | Mostra tempo restante antes de teleportar |
| Criar/atualizar home | Bússola | Abre confirmação para salvar a posição atual |
| Modo deletar | Corante vermelho | Alterna exclusão segura de homes |
| Fechar | Barreira | Fecha o menu |

### Comportamento esperado

- Clique esquerdo em uma home: iniciar teleporte.
- Shift + clique em uma home: definir como home principal.
- Clique com modo deletar ativo: pedir confirmação antes de remover.
- Homes obstruídas devem mostrar aviso no chat e não aplicar cooldown.
- Jogadores comuns não devem ver opções que não podem usar; quando fizer sentido, o menu mostra o motivo do bloqueio.

### Próxima implementação

A implementação deve usar container server-side do Fabric, sem depender de plugin Bukkit. A GUI será apenas uma camada visual sobre o `HomeService`, mantendo PostgreSQL, limites, cooldowns e validações atuais como fonte oficial.
