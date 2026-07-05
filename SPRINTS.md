# Sprints do Atlas

## Próximas prioridades

1. Acompanhar e concluir a pré-geração integral do Survival Emerald.
2. Concluir as regras essenciais da Sprint 5: PvP, fome, dano de queda, Void e exceções para arenas.
3. Validar morte no Survival, retorno ao Lobby Emerald e limpeza de posição com `/lobby emerald`.
4. Validar e concluir a GUI da Sprint 6 — Home System.
5. Retomar o conteúdo visual do Lobby Emerald: NPCs, tutorial, rankings, crates, BossBar e scoreboard.

---

## Sprint 1 — Core Foundation

Status: ✅ Concluída

- [x] PostgreSQL
- [x] Migrations
- [x] Module Manager
- [x] Player System
- [x] Economy
- [x] Rank
- [x] Permission
- [x] Cache

---

## Sprint 2 — Visual Identity & Ranks

Status: ✅ Concluída

- [x] Rank Formatter
- [x] Tags visuais de cargos
- [x] Chat Formatter
- [x] Nametag
- [x] TAB
- [x] Sincronização de ranks em tempo real
- [x] Administração completa por `/rank`
- [x] Integração de permissões vanilla sem OP
- [x] Feedback privado de comandos administrativos

Versão final: `v1.4.0`

---

## Sprint 3 — Authentication

Status: ✅ Concluída

### Fundação

- [x] Migration `auth_accounts`
- [x] Migration `player_sessions`
- [x] AuthModule
- [x] AuthRepository
- [x] AuthService
- [x] AuthSessionCache

### Registro e login

- [x] `/register <senha> <confirmacao>`
- [x] Hash seguro de senha com BCrypt
- [x] `/login <senha>`
- [x] `/logout`
- [x] Sessão persistente por jogador
- [x] Expiração e encerramento de sessões

### Proteção

- [x] Bloquear movimentação antes do login
- [x] Bloquear chat e comandos antes do login
- [x] Bloquear inventário e interações antes do login
- [x] Bloquear dano antes do login
- [x] Limitar tentativas e aplicar cooldown
- [x] Ocultar mensagens sensíveis dos logs

### Premium

- [x] Identificar contas Premium com prova oficial de sessão
- [x] Login automático para Premium
- [x] Manter `/register` e `/login` para jogadores Offline

### Entrega

- [x] Testes de registro, login e reconexão
- [x] Documentação da versão
- [x] Build e implantação da v1.8.0
- [x] Validação Premium e Offline em jogo

---

## Sprint 4 — Lobbys & Server Selector

Status: 🚧 Base funcional concluída; pendências visuais e expansão futura

### Arquitetura

- [x] Definir fluxo `Auth Lobby → seletor → Lobby Emerald`
- [x] Impedir teleporte automático após autenticação
- [x] Preparar arquitetura inicial com mundos separados
- [ ] Criar abstração compatível com futura Atlas Network — futuro

### Mapas

- [x] Receber e validar o mapa do Auth Lobby (`Lobby Hub`)
- [x] Receber e validar o mapa do Lobby Emerald
- [x] Confirmar compatibilidade com Minecraft 1.21.1
- [x] Remover mensagens promocionais e links externos
- [x] Criar mensagens de boas-vindas do Atlas Cobblemon
- [x] Verificar mensagens e command blocks nos chunks
- [x] Limpar dados legados de jogadores e Cobblemon
- [x] Converter os biomas dos chunks existentes do Auth Lobby para `minecraft:the_void`
- [x] Instalar o Auth Lobby como mundo inicial
- [x] Instalar o Lobby Emerald como mundo selecionável
- [x] Definir o spawn global do Auth Lobby
- [x] Forçar o spawn exato em toda conexão
- [x] Validar o spawn do Auth Lobby em jogo

### Auth Lobby

- [x] Enviar jogadores sem posição persistente ao Auth Lobby ao entrar
- [x] Impedir restauração automática do Survival após autenticação
- [x] Manter o jogador no Auth Lobby após autenticar
- [x] Bloquear quebra e colocação de blocos para jogadores comuns
- [x] Liberar construção somente para Dono/Owner/Admin/ADM
- [x] Bloquear inventário antes do login
- [x] Bloquear interações com blocos, itens e entidades antes do login
- [x] Bloquear todo dano antes do login
- [x] Bloquear dano de queda de jogadores dentro do Auth Lobby
- [x] Impedir spawn e carregamento de Pokémon no Auth Lobby
- [x] Impedir escolha e recebimento de Pokémon inicial no Auth Lobby
- [x] Fechar o Auth Lobby com paredes e teto de barreira invisível
- [x] Validar em jogo a tentativa de escolher um inicial no Auth Lobby

### Gameplay do Auth Lobby

- [ ] Desativar NPCs
- [ ] Desativar economia
- [ ] Desativar demais gameplays
- [x] Bloquear todos os comandos no Hub mesmo após autenticação
- [x] Permitir exclusivamente `/login` e `/register` no Hub

### Seletor de servidores

- [x] Entregar a bússola somente após autenticação
- [x] Impedir que a bússola seja movida, descartada ou perdida
- [x] Abrir o menu de servidores ao usar a bússola
- [x] Exibir inicialmente apenas o servidor Emerald
- [x] Teleportar para o Lobby Emerald após a seleção
- [x] Manter o jogador no Auth Hub após login/autologin até escolher pela bússola
- [x] Preservar o inventário real ao sair do Auth Hub pelo seletor
- [x] Restaurar a bússola ao retornar ao Auth Lobby
- [ ] Preparar arquitetura para Sword — futuro
- [ ] Preparar arquitetura para Shield — futuro
- [x] Validar visualmente a bússola e o menu com um jogador autenticado

### Lobby Emerald

- [x] Proteger o mapa contra alterações não autorizadas
- [x] Bloquear dano de queda no Lobby Emerald
- [x] Permitir escolha do Pokémon inicial no Lobby Emerald
- [x] Restringir spawns a Pokémon fracos de rotas iniciais
- [x] Bloquear Pokémon especiais por whitelist de espécies
- [x] Manter Pokémon de jogadores liberados no Lobby Emerald
- [x] Fechar o Lobby Emerald com paredes e teto de barreira invisível
- [x] Validar em jogo o spawn natural de espécies permitidas
- [x] Implementar `/spawn` para retornar ao Hub central do Atlas
- [x] Restringir `/spawn` a jogadores autenticados
- [x] Validar em jogo o retorno do Emerald ao Hub com `/spawn`
- [x] Preparar acesso ao Survival Emerald
- [x] Criar o mundo `atlas:survival_emerald`
- [x] Implementar `/lobby emerald` para retornar do Survival ao Lobby Emerald
- [x] Iniciar pré-geração integral do Survival Emerald
- [ ] Concluir pré-geração integral do Survival Emerald
- [ ] Implementar NPCs
- [ ] Implementar tutorial
- [ ] Implementar rankings
- [ ] Implementar crates
- [ ] Implementar BossBar
- [ ] Implementar scoreboard
- [x] Adicionar tema sonoro de entrada por mundo

### Hierarquia visual

- [x] Ordenar o TAB por `Dono > ADM > MOD > SUP > VIPs > Players`
- [x] Garantir por prioridade que nenhum Player ou VIP apareça acima da Staff
- [x] Validar visualmente a ordenação do TAB com jogadores de cargos diferentes

### Entrega

- [x] Documentar a arquitetura dos lobbys
- [x] Build e implantação da v1.12.0
- [x] Testar fluxo com conta Premium
- [x] Testar fluxo com conta Offline
- [x] Validar reconexão, logout e expiração de sessão
- [x] Build e implantação da v1.21.0

---

## Sprint 5 — Gameplay Rules

Status: 🚧 Em andamento

- [x] Garantir drops de blocos e plantas no Survival Emerald

Objetivo: padronizar toda a experiência PvE.

- [ ] Desativar PvP
- [ ] Desativar fome
- [ ] Desativar dano de queda
- [x] Implementar regras por mundo
- [x] Proteger os lobbys
- [x] Definir limite de 12000 × 12000 blocos para o Survival Emerald
- [x] Reposicionar jogadores que ultrapassarem o limite
- [x] Iniciar pré-geração automática dos 750 × 750 chunks do Survival Emerald
- [ ] Concluir pré-geração automática dos 750 × 750 chunks do Survival Emerald
- [x] Resetar o Survival Emerald com a mesma seed e estruturas/worldgen dos addons
- [x] Implementar `/rtp` seguro no Lobby e Survival Emerald
- [x] Aplicar cooldown de `/rtp` por cargo
- [x] Manter fila rápida de destinos seguros
- [x] Cancelar `/rtp` por movimento sem aplicar cooldown
- [x] Salvar a última posição no Survival entre reconexões e reinícios
- [ ] Definir fluxo de retorno opcional ao Survival salvo sem pular o seletor
- [x] Retornar ao Lobby Emerald após morte no Survival
- [x] Implementar saída voluntária com `/lobby emerald`
- [x] Adicionar `/endbattle` para jogadores encerrarem batalhas travadas
- [ ] Proteger contra o Void
- [ ] Preparar exceções para arenas futuras

### Validação pendente

- [x] Validar que reconexão Premium permanece no Auth Hub até escolha pela bússola
- [x] Validar que `/login` Offline permanece no Auth Hub até escolha pela bússola
- [x] Validar persistência após reinício completo do servidor
- [ ] Validar morte no Survival e retorno ao Lobby Emerald
- [ ] Validar limpeza da posição com `/lobby emerald`

---

## Sprint 6 — Home System

Status: 🚧 Em andamento

- [x] Migration `homes`
- [x] Migration complementar `024_home_system.sql`
- [x] HomeModule
- [x] HomeRepository
- [x] HomeService
- [x] `/home [nome]`
- [x] `/sethome <nome>`
- [x] `/delhome <nome>`
- [x] `/homes`
- [x] Home principal automática
- [x] Cooldowns por cargo
- [x] Limites por cargo
- [x] Teleporte seguro
- [x] Aquecimento e cancelamento por movimento
- [x] Validar criação, atualização e exclusão em jogo
- [x] Validar limites com Player, VIP e Staff
- [x] Validar home obstruída e cancelamento por movimento
- [ ] Projetar GUI e ícones das homes

---

## Sprint 7 — Claims & Protection

Status: ✅ Concluída

### Fundação

- [x] Migration `claims`
- [x] Migration `claim_members`
- [x] Migration complementar e índices
- [x] ClaimModule
- [x] ClaimRepository
- [x] ClaimService

### Criação e inspeção

- [x] Selecionar dois cantos com pá dourada
- [x] Inspecionar claims com graveto
- [x] Limite total de blocos por cargo
- [x] Tamanho mínimo de claim
- [x] Impedir sobreposição
- [x] Restringir claims ao Survival Emerald

### Proteções

- [x] Bloquear quebra e colocação por terceiros
- [x] Proteger baús e demais contêineres
- [x] Proteger portas, botões e interações
- [x] Proteger entidades e Pokémon do proprietário
- [x] Proteger contra fluidos, fogo, explosões e pistões
- [x] Bypass administrativo auditável

### Confiança e gestão

- [x] `/trust <jogador>`
- [x] `/containertrust <jogador>`
- [x] `/accesstrust <jogador>`
- [x] `/untrust <jogador>`
- [x] `/abandonclaim`
- [x] `/claimslist`
- [x] Teleporte clicável para claims próprias no `/claimslist`
- [x] Visualizar limites da claim com blocos de ouro falsos

---

## Sprint 8 — Anti Lag & Recovery

Status: ✅ Concluída

### Anti Lag

- [x] Limpeza de drops antigos
- [x] Limpeza segura de Pokémon selvagens distantes
- [x] Monitoramento de TPS e MSPT
- [x] `/atlas cleanup`
- [x] `/atlas tps`
- [x] Avisos antes da limpeza automática

### Item Recovery

- [x] `/lixeira`
- [x] `/dropados`
- [x] Recuperação persistente de itens
- [x] Expiração automática em 15 minutos
- [x] Logs de armazenamento, recuperação e expiração

### Modpack de testes

- [x] Instalar addons Cobblemon da pasta `modsadd`
- [x] Instalar dependências necessárias dos addons
- [x] Validar boot do servidor com os addons
- [x] Documentar pacote de mods e exigência de client igual ao servidor
- [x] Validar entrada de jogador com o pacote de cliente atualizado

---

## Sprint 9 — Moderation & Staff

Status: ⏳ Planejada

### Punições

- [ ] Warn
- [ ] Kick
- [ ] Mute
- [ ] Ban
- [ ] BanIP

### Staff

- [ ] Freeze
- [ ] StaffMode
- [ ] InvSee
- [ ] EnderSee
- [ ] Staff Notes
- [ ] Histórico

### Broadcast

- [ ] Warn privado
- [ ] Ban global
- [ ] Configuração

### Regras

- [ ] Sistema de Rules
- [ ] Aceite obrigatório

---

## Sprint 10 — Economy Expansion

Status: 🚧 Em andamento

### Economia

- [x] Integrar Atlas Coins ao CobbleDollars
- [x] Usar CobbleDollars como fonte oficial de saldo
- [x] Atualizar `/saldo`
- [x] Atualizar `/addmoney`
- [ ] Pesquisa Pokémon
- [ ] Contratos
- [ ] Mercado
- [ ] Profissões
- [ ] Oferta e demanda
- [ ] Ginásios
- [ ] Login diário
- [ ] Kit diário com pá dourada para criação de claims

### Filosofia

- Coins apenas jogando
- Sem venda infinita de blocos
- Sem economia Pay-to-Win

---

## Sprint 11 — Quest Module

Status: ⏳ Planejada

- [ ] Quest principal
- [ ] Quest diária
- [ ] Quest semanal
- [ ] Quest de evento
- [ ] NPCs Professores

---

## Sprint 12 — Atlas Events

Status: 🚧 Em andamento

### Planejamento

- [x] Definir objetivo e filosofia dos eventos
- [x] Documentar fluxo inicial de evento Pokémon
- [x] Definir componentes técnicos previstos
- [x] Definir comandos administrativos e públicos previstos

### Eventos Pokémon

- [ ] Lendários
- [ ] Ultra Beasts
- [ ] Paradox
- [ ] Míticos

### Spawn

- [ ] Anunciar bioma
- [ ] BossBar

### Desfecho

- [ ] Capturado
- [ ] Derrotado
- [ ] Desapareceu
- [ ] Tempo expirado

### Discord

- [ ] Webhook

---

## Sprint 13 — Tournament Module

Status: ⏳ Planejada

- [ ] Inscrição
- [ ] Chaveamento
- [ ] Arenas
- [ ] Ranking
- [ ] Temporadas

---

## Sprint 14 — Gym Module

Status: ⏳ Planejada

- [ ] Ginásios
- [ ] Puzzles
- [ ] Líderes
- [ ] Insígnias
- [ ] Elite Four

---

## Sprint 15 — Pokédex Progression

Status: ⏳ Planejada

### Academia Atlas

- [ ] Progressão por porcentagem: 10%, 20%, 30% ... 100%

### Professor Atlas — conclusão em 100%

- [ ] Tag exclusiva
- [ ] Hall dos Professores
- [ ] `/pc`
- [ ] `/pokeheal`
- [ ] `/legendary`

### Hall

- [ ] NPCs
- [ ] Estatísticas
- [ ] Data da conquista

### Categorias

- [ ] Kanto
- [ ] Johto
- [ ] Hoenn
- [ ] Demais regiões

### Tipos

- [ ] Dragões
- [ ] Fadas
- [ ] Fantasmas
- [ ] Demais tipos

---

## Sprint 16 — Achievement Module

Status: ⏳ Planejada

- [ ] Conquistas
- [ ] Títulos
- [ ] Partículas
- [ ] Cosméticos

---

## Sprint 17 — Atlas Seasons

Status: ⏳ Planejada

### Jornada Atlas

- [ ] Passe gratuito
- [ ] Passe Premium
- [ ] XP
- [ ] Desafios
- [ ] Temporadas

### Filosofia

- Não vender Atlas Tokens
- Tokens apenas jogando
- VIP possui trilha Premium
- Nunca Pay-to-Win

---

## Sprint 18 — VIP System

Status: ⏳ Planejada

### Qualidade de vida

- [ ] Homes extras
- [ ] Backpack
- [ ] PVs
- [ ] Fly somente nos lobbys
- [ ] Back
- [x] Spawn
- [x] RTP com vantagens de cooldown por cargo

### Cosméticos

- [ ] Tags
- [ ] Partículas
- [ ] Emotes
- [ ] Bicicletas
- [ ] Mochilas

---

## Sprint 19 — Staff Academy

Status: ⏳ Planejada

- [ ] Manual da Staff
- [ ] Código de Conduta
- [ ] Casos práticos
- [ ] Guia dos comandos
- [ ] Fluxo de atendimento
- [ ] Centro de Treinamento

---

## Sprint 20 — API & Painel

Status: ⏳ Planejada

- [ ] REST API
- [ ] Website
- [ ] Loja
- [ ] Painel administrativo
- [ ] Discord
- [x] CLI

---

## Sprint 21 — Atlas Network

Status: 🔮 Futuro

### Servidores previstos

- [x] Emerald
- [ ] Sword
- [ ] Shield
- [ ] Ruby
- [ ] Sapphire

### Estrutura por servidor

- [ ] Economia própria
- [ ] Eventos próprios
- [ ] GTS própria
- [ ] Mundo próprio

### Sistemas compartilhados

- [x] Login
- [x] Conta
- [x] Premium
- [ ] Amigos
- [x] Staff global
