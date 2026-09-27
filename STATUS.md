# Estado atual do Atlas

Consolidação documental: 2026-09-27.

## Referência técnica

- Versão declarada em `atlas-core/gradle.properties`: **1.29.13**.
- O JAR instalado em `/opt/atlas/server/fabric/mods/atlas-core.jar` declara **1.29.13**.
- O serviço `atlas` estava ativo na consulta desta consolidação. Isso não substitui testes em jogo.
- `atlas-api/` e `atlas-web/` estão vazias no workspace: API e frontend ainda são planejados.
- A CLI operacional está em `infra/scripts/atlas-cli`.
- Migrations existentes para funcionalidades futuras não comprovam implementação dessas funcionalidades.

## Implementado

- Core modular, PostgreSQL, migrations, players e cache.
- Ranks, permissões, TAB, nametags e chat; variantes VIP e chat colorido.
- Registro/login Offline, autenticação automática Premium e proteção de sessões.
- Auth Hub, bússola seletora, NPC de acesso ao Emerald e preservação do inventário.
- Lobbys autorais, Survival Emerald, regras PvE, RTP para Overworld/Nether/End e músicas contextuais.
- Homes por comandos, `/back`, claims, confiança e proteções auditáveis.
- CobbleDollars como fonte oficial de saldo, `/saldo`, `/addmoney` e `/pay`.
- Kits comuns e VIP, cooldowns, GUI de kits e seleção de mints; `/fly` e `/ec`.
- Punições persistentes e histórico, respeitando hierarquia da staff.
- Limpeza de entidades, TPS/MSPT e recuperação persistente de itens.
- Scripts operacionais, backup/restauração e comandos de pré-geração.

## Últimas entregas consolidadas

As versões 1.28.5 a 1.29.13 registram ajustes de limpeza e compatibilidade de mods,
RTP multidimensional, pré-geração, kits, benefícios VIP, reconstrução do Lobby Emerald
e correções de WorldEdit. A 1.29.13 libera todos os comandos para Dono autenticado,
inclusive no Auth Hub, mantendo as proteções antes do login.

As versões 1.29.9 e 1.29.10 descrevem intervenções no mundo; não são, por si só,
novas versões do JAR. Consulte [CHANGELOG.md](CHANGELOG.md) e [versions/](versions/README.md).

## Pendências imediatas

- GUI das homes e conteúdo final do Lobby Emerald.
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
[CONTEXT.md](CONTEXT.md) preserva a visão e decisões originais; descrições históricas
não devem substituir o comportamento documentado nas versões mais recentes.
Por exemplo, a economia atual usa CobbleDollars, embora o desenho inicial previsse
saldo próprio no PostgreSQL.

Esta consolidação organiza alterações locais existentes e documentação. Não representa
uma nova release, novo deploy ou uma nova rodada de validação dentro do Minecraft.
