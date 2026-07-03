# Sprints do Atlas

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

Status: 🚧 Em andamento

### Arquitetura

- [x] Definir fluxo `Auth Lobby → seletor → Lobby Emerald`
- [x] Impedir teleporte automático após autenticação
- [x] Preparar arquitetura inicial com mundos separados
- [ ] Criar abstração compatível com futura Atlas Network

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

- [x] Enviar todo jogador ao Auth Lobby ao entrar
- [x] Manter o jogador no Auth Lobby após autenticar
- [x] Bloquear quebra e colocação de blocos para jogadores comuns
- [x] Liberar construção somente para Dono/Owner/Admin/ADM
- [x] Bloquear inventário antes do login
- [x] Bloquear interações com blocos, itens e entidades antes do login
- [x] Bloquear todo dano antes do login
- [x] Bloquear dano de queda de jogadores dentro do Auth Lobby
- [x] Impedir spawn e carregamento de Pokémon no Auth Lobby
- [x] Impedir escolha e recebimento de Pokémon inicial no Auth Lobby
- [x] Validar em jogo a tentativa de escolher um inicial no Auth Lobby

### Gameplay do Auth Lobby

- [ ] Desativar NPCs
- [ ] Desativar economia
- [ ] Desativar demais gameplays

### Seletor de servidores

- [x] Entregar a bússola somente após autenticação
- [x] Impedir que a bússola seja movida, descartada ou perdida
- [x] Abrir o menu de servidores ao usar a bússola
- [x] Exibir inicialmente apenas o servidor Emerald
- [x] Teleportar para o Lobby Emerald após a seleção
- [x] Restaurar a bússola ao retornar ao Auth Lobby
- [ ] Preparar arquitetura para Sword
- [ ] Preparar arquitetura para Shield
- [x] Restaurar a bússola ao retornar ao Auth Lobby
- [x] Validar visualmente a bússola e o menu com um jogador autenticado

### Lobby Emerald

- [x] Proteger o mapa contra alterações não autorizadas
- [x] Bloquear dano de queda no Lobby Emerald
- [x] Permitir escolha do Pokémon inicial no Lobby Emerald
- [x] Restringir spawns a Pokémon fracos de rotas iniciais
- [x] Bloquear Pokémon especiais por whitelist de espécies
- [x] Validar em jogo o spawn natural de espécies permitidas
- [x] Implementar `/spawn` para retornar ao Hub central do Atlas
- [x] Restringir `/spawn` a jogadores autenticados
- [x] Validar em jogo o retorno do Emerald ao Hub com `/spawn`
- [ ] Preparar acesso ao Survival Emerald
- [ ] Implementar NPCs
- [ ] Implementar tutorial
- [ ] Implementar rankings
- [ ] Implementar crates
- [ ] Implementar BossBar
- [ ] Implementar scoreboard

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

---

## Sprint 5 — Gameplay Rules

Status: ⏳ Planejada

Objetivo: padronizar toda a experiência PvE.

- [ ] Desativar PvP
- [ ] Desativar fome
- [ ] Desativar dano de queda
- [ ] Implementar regras por mundo
- [ ] Proteger os lobbys
- [ ] Definir limites automáticos dos mapas
- [ ] Teleportar automaticamente ao sair da área
- [ ] Proteger contra o Void
- [ ] Preparar exceções para arenas futuras

---

## Sprint 6 — Home System

Status: ⏳ Planejada

- [x] Migration `homes`
- [ ] HomeModule
- [ ] HomeRepository
- [ ] HomeService
- [ ] `/home`
- [ ] `/sethome`
- [ ] `/delhome`
- [ ] Cooldowns
- [ ] Limites por cargo
- [ ] Teleporte seguro

---

## Sprint 7 — Anti Lag & Recovery

Status: ⏳ Planejada

### Anti Lag

- [ ] Limpeza de drops
- [ ] Limpeza de Pokémon
- [ ] Monitoramento de TPS
- [ ] `/atlas cleanup`

### Item Recovery

- [ ] `/lixeira`
- [ ] `/dropados`
- [ ] Recuperação de itens
- [ ] Expiração
- [ ] Logs

---

## Sprint 8 — Moderation & Staff

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

## Sprint 9 — Economy Expansion

Status: ⏳ Planejada

### Economia

- [ ] Pesquisa Pokémon
- [ ] Contratos
- [ ] Mercado
- [ ] Profissões
- [ ] Oferta e demanda
- [ ] Ginásios
- [ ] Login diário

### Filosofia

- Coins apenas jogando
- Sem venda infinita de blocos
- Sem economia Pay-to-Win

---

## Sprint 10 — Quest Module

Status: ⏳ Planejada

- [ ] Quest principal
- [ ] Quest diária
- [ ] Quest semanal
- [ ] Quest de evento
- [ ] NPCs Professores

---

## Sprint 11 — Atlas Events

Status: ⏳ Planejada

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

## Sprint 12 — Tournament Module

Status: ⏳ Planejada

- [ ] Inscrição
- [ ] Chaveamento
- [ ] Arenas
- [ ] Ranking
- [ ] Temporadas

---

## Sprint 13 — Gym Module

Status: ⏳ Planejada

- [ ] Ginásios
- [ ] Puzzles
- [ ] Líderes
- [ ] Insígnias
- [ ] Elite Four

---

## Sprint 14 — Pokédex Progression

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

## Sprint 15 — Achievement Module

Status: ⏳ Planejada

- [ ] Conquistas
- [ ] Títulos
- [ ] Partículas
- [ ] Cosméticos

---

## Sprint 16 — Atlas Seasons

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

## Sprint 17 — VIP System

Status: ⏳ Planejada

### Qualidade de vida

- [ ] Homes extras
- [ ] Backpack
- [ ] PVs
- [ ] Fly somente nos lobbys
- [ ] Back
- [ ] Spawn
- [ ] RTP

### Cosméticos

- [ ] Tags
- [ ] Partículas
- [ ] Emotes
- [ ] Bicicletas
- [ ] Mochilas

---

## Sprint 18 — Staff Academy

Status: ⏳ Planejada

- [ ] Manual da Staff
- [ ] Código de Conduta
- [ ] Casos práticos
- [ ] Guia dos comandos
- [ ] Fluxo de atendimento
- [ ] Centro de Treinamento

---

## Sprint 19 — API & Painel

Status: ⏳ Planejada

- [ ] REST API
- [ ] Website
- [ ] Loja
- [ ] Painel administrativo
- [ ] Discord
- [ ] CLI

---

## Sprint 20 — Atlas Network

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
- [x] Restaurar a bússola ao retornar ao Auth Lobby
