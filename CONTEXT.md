# Contexto do Atlas

Atlas é uma plataforma para uma comunidade brasileira de Minecraft Cobblemon.
O servidor Emerald é a primeira entrega; API, website, loja e expansão da rede
fazem parte do planejamento em [ROADMAP.MD](ROADMAP.MD).

## Princípios

- Priorizar módulos próprios quando trouxerem controle e manutenção viável.
- Aceitar contas Premium com prova oficial de sessão e contas Offline com registro/login.
- Não vender dinheiro ou vantagens competitivas; revisar os benefícios VIP atuais à luz dessa diretriz.
- Preservar dados de jogadores e histórico de operações relevantes.
- Nunca guardar senhas em código, scripts ou documentação.

## Arquitetura

Stack atual: Java 21, Minecraft 1.21.1, Fabric e PostgreSQL.
Spring Boot e Angular são escolhas planejadas; API e frontend ainda não estão implementados.

| Diretório | Responsabilidade |
| --- | --- |
| `atlas-core/` | Módulos e regras do servidor Minecraft |
| `database/migrations/` | Evolução versionada do banco |
| `infra/` | CLI, scripts e templates operacionais |
| `minecraft/` | Recursos locais do servidor, mapas e schemas |
| `atlas-docs/` | Estado, operação e histórico de versões |
| `atlas-api/`, `atlas-web/` | Espaços reservados para API e frontend |

Fluxo: comando/listener → serviço → repositório → banco.
Commands validam argumentos e permissões; Services concentram regras; Repositories
concentram SQL; Listeners delegam aos Services. O bootstrap registra módulos com
ciclo de vida `enable`/`disable`. Cache reduz consultas, sem substituir persistência.
As regras de desenvolvimento e release estão em [AGENTS.md](AGENTS.md).

## Persistência e integrações

- PostgreSQL mantém jogadores, autenticação, sessões, ranks/permissões, homes,
  claims, punições, resgates de kits e recuperação de itens.
- Toda alteração de schema exige migration. Os arquivos SQL são a referência dos campos e índices.
- UUID identifica jogadores; a autenticação Premium inclui migração de identidade e dados.
- CobbleDollars é a fonte oficial de saldo; `economy_accounts` é legado.
- Dados completos de Pokémon continuam sob responsabilidade do Cobblemon.
- Migrations para recursos futuros não significam que esses recursos estejam implementados.
- Ranks podem ser combinados; a prioridade define apresentação e as permissões são reunidas.
- A administração usa console local por socket Unix; o RCON foi substituído.

Estado implementado: [STATUS.md](STATUS.md). Critérios e pendências: [SPRINTS.md](SPRINTS.md).
