# Estado atual do Atlas

Consolidação documental: 2026-09-29.

## Referência técnica

- Versão declarada em `atlas-core/gradle.properties`: **1.29.21**.
- O JAR instalado em `/opt/atlas/server/fabric/mods/atlas-core.jar` declara **1.29.21**.
- O serviço `atlas` estava ativo na consulta desta consolidação. Isso não substitui testes em jogo.
- `atlas-web/` foi importado como submódulo e iniciado em desenvolvimento; melhorias adiadas conforme [ATLAS-WEB.md](ATLAS-WEB.md). A API continua planejada.
- A CLI operacional está em `infra/scripts/atlas-cli`.
- Migrations existentes para funcionalidades futuras não comprovam implementação dessas funcionalidades.

## Implementado

- Core modular, PostgreSQL, migrations, players e cache.
- Ranks, permissões, TAB, nametags e chat; variantes VIP e chat colorido.
- Registro/login Offline, autenticação automática Premium e proteção de sessões.
- Auth Hub, bússola seletora, NPC de acesso ao Emerald e preservação do inventário.
- Lobbys autorais, Survival Emerald, regras PvE, RTP para Overworld/Nether/End e músicas contextuais.
- Homes por comandos e GUI, `/back`, claims, confiança e proteções auditáveis.
- CobbleDollars como fonte oficial de saldo, `/saldo`, `/addmoney` e `/pay`.
- Kits comuns e VIP, cooldowns, GUI de kits e seleção de mints; `/fly` e `/ec`.
- Punições persistentes e histórico, respeitando hierarquia da staff.
- Limpeza de entidades, TPS/MSPT e recuperação persistente de itens.
- Scripts operacionais e comandos de pré-geração. Backup/restauração implementados e testados; timer ativo e primeiro snapshot completo concluído.

## Últimas entregas consolidadas

A [v1.29.21](versions/v1.29.21.md) amplia a limpeza para todas as dimensões carregadas, sem idade mínima dos drops, preservando proteções de Pokémon. Build, inicialização e teste de drops em duas dimensões aprovados.

A [v1.29.20](versions/v1.29.20.md) atualiza o spawn do novo Lobby Emerald para `918.5302583016859 71 3838.5058040626927`, com yaw `179.39441°` e pitch `-1.7545054°`. Build e implantação aprovados; conferência visual em jogo pendente.

A [v1.29.19](versions/v1.29.19.md) adiciona notas internas e histórico paginado, com autenticação, hierarquia e arquivamento auditável. Build, testes automatizados e consultas pelo console aprovados; validação em jogo pendente. Guia: [STAFF-NOTES.md](STAFF-NOTES.md).

A [v1.29.18](versions/v1.29.18.md) adiciona StaffMode com modo espectador,
restauração persistente e bloqueios de gameplay. Testes em jogo pendentes.

A [v1.29.17](versions/v1.29.17.md) adiciona freeze temporário e consultas
de inventário/Ender Chest somente leitura, com hierarquia e logs.

A [v1.29.16](versions/v1.29.16.md) adiciona a GUI de `/homes`, com paginação,
teleporte, escolha da principal e confirmação de criação/atualização/exclusão.
GUI testada e aprovada pelo usuário em 2026-09-27.

A [v1.29.15](versions/v1.29.15.md) remove WorldEdit do servidor e as integrações do Core.

A [v1.29.14](versions/v1.29.14.md) corrige a localização de classes Java, remove
avisos de código e define UTF-8. Build e implantação foram validados em 2026-09-27.

As versões 1.28.5 a 1.29.13 registram ajustes de limpeza e compatibilidade de mods,
RTP multidimensional, pré-geração, kits, benefícios VIP, reconstrução do Lobby Emerald
e correções de WorldEdit. A 1.29.13 libera todos os comandos para Dono autenticado,
inclusive no Auth Hub, mantendo as proteções antes do login.

As versões 1.29.9 e 1.29.10 descrevem intervenções no mundo; não são, por si só,
novas versões do JAR. Consulte [CHANGELOG.md](CHANGELOG.md) e [versions/](versions/README.md).

## Pendências imediatas

- Ampliar capacidade para retenção de backups e ensaiar recuperação integral dos mundos; [guia](BACKUP.md).
- Conteúdo final do Lobby Emerald.
- Fluxo de retorno opcional ao Survival e validação de `/lobby emerald`.
- Validação em jogo da limpeza atual, punições e kits VIP/seleção de mints.
- Confirmação do término da pré-geração do Nether e End.
- Ferramentas de staff, regras e aceite obrigatório.
- Expansão econômica, mercado/GTS, missões e implementação de eventos.
- Assinatura/expiração VIP, cosméticos e revisão da coerência dos kits com a filosofia de monetização.
- API, website, loja, painel e integração Discord.

## Como interpretar a documentação

[SPRINTS.md](SPRINTS.md) contém o checklist de implementação e validação.
[ROADMAP.MD](ROADMAP.MD) organiza o trabalho restante.
[CONTEXT.md](CONTEXT.md) reúne princípios, arquitetura e persistência.
O histórico detalhado fica nas notas de versão.

As validações de build e implantação estão nas notas de versão. Os testes em jogo
ainda pendentes permanecem listados nas sprints.
