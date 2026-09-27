# Roadmap do Atlas

Atualizado em 2026-09-27. Referência: Atlas Core `1.29.14`.

O detalhamento e os critérios de conclusão estão em [SPRINTS.md](SPRINTS.md).
O estado consolidado está em [STATUS.md](STATUS.md).

## Entregas concluídas

- Sprint 1: fundação modular, PostgreSQL, migrations, players, economia, ranks e permissões.
- Sprint 2: identidade visual de cargos, TAB, chat, nametags e administração de ranks.
- Sprint 3: autenticação Offline/Premium, sessões e proteções antes do login.
- Sprint 7: claims, proteção, confiança, gestão e auditoria administrativa.
- Sprint 8: limpeza de entidades, monitoramento e recuperação persistente de itens.

Concluído indica o escopo registrado da sprint; validações de alterações posteriores
podem permanecer abertas.

## Finalizar sistemas existentes

| Sprint | Entregue | Falta |
| --- | --- | --- |
| 4 — Lobbys | Auth Hub, seletor, NPC de navegação, proteção e base autoral Emerald | Conteúdo visual, NPCs do Emerald, tutorial, rankings, crates, BossBar e scoreboard |
| 5 — Gameplay | PvE, Survival, RTP multidimensional, respawn e músicas contextuais | Retorno opcional à posição salva, validações e exceções futuras para arenas |
| 6 — Homes | Comandos, limites, segurança e `/back` | GUI das homes |
| 9 — Moderação | Punições persistentes e hierarquia | Validação em jogo, ferramentas de staff, regras e aceite |
| 10 — Economia | CobbleDollars, transferências e kits comuns | Pesquisa, contratos, mercado/GTS, profissões, oferta/demanda e login diário |
| 12 — Eventos | Planejamento documentado | Implementação de eventos Pokémon, anúncios, desfechos e Discord |
| 18 — VIP | Kits, cargos, chat colorido, `/fly`, `/ec` e benefícios de teleporte | Assinatura/expiração, validação e revisão dos benefícios, armazenamento e cosméticos |

## Conteúdo planejado

- Sprint 11: missões principais, diárias, semanais e de eventos.
- Sprint 13: torneios, arenas, chaveamento, ranking e temporadas.
- Sprint 14: ginásios, puzzles, líderes, insígnias e Elite Four.
- Sprint 15: progressão da Pokédex, Academia Atlas e Hall dos Professores.
- Sprint 16: conquistas, títulos, partículas e cosméticos.
- Sprint 17: Jornada Atlas, passes, XP e desafios.
- Sprint 19: manual, conduta, atendimento e treinamento da staff.
- Sprint 20: API REST, website, loja, painel e Discord. A CLI operacional já existe.
- Sprint 21: expansão futura para Sword, Shield, Ruby e Sapphire, com sistemas compartilhados.

## Ordem de continuidade

Pendência operacional prioritária: implementar backup/restauração reais e testar recuperação; os scripts atuais são placeholders.

1. Validar os fluxos essenciais e as entregas recentes em jogo; confirmar pré-geração do Nether/End.
2. Finalizar GUI das homes e conteúdo do Lobby Emerald.
3. Completar ferramentas de staff e regras.
4. Desenvolver economia, missões e eventos.
5. Construir API, website e loja após definir benefícios e monetização.
6. Expandir a rede conforme a maturidade do Emerald.
