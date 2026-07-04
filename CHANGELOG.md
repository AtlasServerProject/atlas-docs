v0.0.1

Primeiro bootstrap.

---

v0.0.2

Player System.

---

v0.0.3

Economy.

---

v0.0.4

Ranks.

---

O histórico detalhado dos builds do mod está em `atlas-docs/versions/`.

---

v1.8.0

Autenticação híbrida segura para contas Premium e Offline, com migração de UUID e dados.

---

v1.9.0

Console administrativo próprio por socket Unix e remoção do RCON.

---

v1.10.0

Bloqueio de chat e comandos para jogadores não autenticados.

---

v1.11.0

Logout manual e expiração ativa das sessões de autenticação.

---

v1.12.0

Primeira entrega do Auth Lobby, com mapa dedicado e saudação individual no login.

---

v1.12.1

Título de entrada compacto e definição do spawn global do Auth Lobby.

---

v1.12.2

Spawn exato obrigatório no Auth Lobby para todas as conexões.

---

v1.13.0

Proteção de construção do Auth Lobby com exceção exclusiva para Dono e Admin.

---

v1.14.0

Primeira integração com eventos de spawn do Cobblemon; substituída após o teste revelar que comandos ignoravam o cancelamento.

---

v1.14.1

Bloqueio absoluto de entidades Pokémon no Auth Lobby, validado contra spawn por comando.

---

Documentação operacional

Adicionada a referência dos comandos `sudo playit status` e `sudo playit attach`, incluindo a consulta do endereço externo e a validação dos serviços necessários.

---

v1.14.2

Proteção total contra dano antes da autenticação e bloqueio de dano de queda no Auth Lobby. Os chunks existentes do mapa também foram convertidos para o bioma `minecraft:the_void`.

---

v1.14.3

Ordenação determinística do TAB pela prioridade dos cargos, mantendo Dono, ADM, MOD e SUP acima de VIPs e Players.

---

v1.14.4

Bloqueio autoritativo da escolha de Pokémon inicial no Auth Lobby antes que o Cobblemon grave a escolha ou entregue o Pokémon.

---

v1.15.0

Adicionado `/spawn` para jogadores autenticados retornarem ao Hub central e ao seletor de servidores.

---

v1.16.0

Bloqueados cliques de inventário, receitas, inventário criativo e interações com blocos, itens e entidades antes da autenticação.

---

v1.16.1

Adicionado bloqueio de cinco minutos após cinco senhas inválidas, sem registrar senha, hash ou IP nos logs de segurança.

---

v1.16.2

Refinado o limitador para considerar cinco falhas dentro de uma janela móvel de dez minutos, evitando acúmulo indefinido de erros antigos.

---

v1.17.0

Instalado o Lobby Emerald como `atlas:emerald` e adicionado o seletor por bússola com entrega pós-login, proteção do item, menu exclusivo do Emerald e restauração automática no Auth Lobby.

---

v1.17.1

Corrigido o destino do Lobby Emerald para `975.5 179 1573.5`, orientado para leste.

---

v1.18.0

Primeira implementação da proteção de queda e whitelist de Pokémon no Lobby Emerald; substituída após o teste revelar resolução incorreta do mundo durante eventos de spawn.

---

v1.18.1

Corrigida a resolução da dimensão nos eventos do Cobblemon. O Lobby Emerald permite a escolha do inicial, bloqueia dano de queda e aceita somente espécies fracas explicitamente aprovadas.

---

v1.18.2

Renomeada a mensagem de proteção para Hub e estendido o bloqueio de quebra e colocação ao Lobby Emerald.

---

v1.19.0

Criado o Survival Emerald com área de 6000 × 6000 blocos, pré-geração dos 375 × 375 chunks e comando `/lobby` para retornar ao Lobby Emerald.

---

v1.19.1

Reforçado o limite do Survival Emerald com reposicionamento automático de jogadores que tentarem ultrapassar a área definida.

---

v1.20.0

Adicionado `/rtp` seguro no Survival Emerald, com cooldown progressivo por cargo e validação do terreno de destino.

---

v1.20.1

Corrigido o fluxo do `/rtp`: o comando agora é usado no Lobby Emerald e envia o jogador para um local seguro no Survival Emerald.

---

v1.20.2

O `/rtp` agora mantém uma busca persistente e assíncrona até encontrar um destino seguro, sem exigir novas tentativas do jogador.

---

v1.20.3

Adicionada uma fila antecipada de destinos seguros inspirada no BetterRTP, tornando o `/rtp` praticamente imediato.

---

v1.20.4

Adicionado aquecimento de três segundos ao `/rtp`, cancelado sem cooldown caso o jogador se mova.

---

v1.20.5

Liberado o uso de `/rtp` tanto no Lobby Emerald quanto dentro do Survival Emerald.

---

v1.21.0

Adicionada persistência da última posição no Survival Emerald, restauração após autenticação e retorno ao lobby somente por morte ou `/lobby emerald`.

---

v1.22.0

Primeira entrega do Home System, com homes nomeadas, home principal, limites e cooldowns por cargo e teleporte seguro.

---

v1.22.1

Bloqueados todos os comandos no Auth Hub, inclusive após autenticação, mantendo somente `/login` e `/register`.

---

v1.23.0

Primeira entrega funcional de Claims & Protection no Survival Emerald, com seleção por pá dourada, inspeção por graveto, confiança cumulativa, limites por cargo e persistência PostgreSQL.
