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

Status: 🚧 Em andamento

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
- [ ] Instalar o Lobby Emerald como mundo selecionável
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
- [ ] Validar em jogo a tentativa de escolher um inicial no Auth Lobby
- [ ] Desativar NPCs, economia e demais gameplays no Auth Lobby

### Seletor de servidores

- [ ] Entregar a bússola somente após autenticação
- [ ] Impedir que a bússola seja movida, descartada ou perdida
- [ ] Abrir o menu de servidores ao usar a bússola
- [ ] Exibir inicialmente apenas o servidor Emerald
- [ ] Teleportar para o Lobby Emerald após a seleção
- [ ] Restaurar a bússola ao retornar ao Auth Lobby

### Lobby Emerald

- [ ] Proteger o mapa contra alterações não autorizadas
- [x] Implementar `/spawn` para retornar ao Hub central do Atlas
- [x] Restringir `/spawn` a jogadores autenticados
- [ ] Validar o retorno do Emerald ao Hub após a instalação do Lobby Emerald
- [ ] Preparar acesso ao Survival Emerald
- [ ] Reservar integração para NPCs, crates, rankings e tutorial
- [ ] Reservar integração para scoreboard e BossBar

### Hierarquia visual

- [x] Ordenar o TAB por `Dono > ADM > MOD > SUP > VIPs > Players`
- [x] Garantir por prioridade que nenhum Player ou VIP apareça acima da Staff
- [ ] Validar visualmente a ordenação do TAB com jogadores de cargos diferentes

### Entrega

- [x] Documentar a arquitetura dos lobbys
- [x] Build e implantação da v1.12.0
- [ ] Testar fluxo com conta Premium
- [ ] Testar fluxo com conta Offline
- [ ] Validar reconexão, logout e expiração de sessão

---

## Sprint 5 — Homes

Status: ⏳ Planejada

- [x] Migration `homes`
- [ ] HomeModule
- [ ] HomeRepository
- [ ] HomeService
- [ ] `/home`
- [ ] `/sethome`
- [ ] `/delhome`
- [ ] Limites por cargo e VIP
- [ ] Teleporte seguro
- [ ] Cooldown de teleporte

---

## Backlog

- Claims
- VIP
- Crates
- GTS
- Missões
- Eventos
- API REST
- Website e loja
- CLI administrativa
- Integração com Discord
