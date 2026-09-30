# NPCs do Atlas

O visual do NPC de navegação do Auth Lobby é fornecido pelo Easy NPC
(`easy_npc:humanoid`). O Atlas Core trata o clique pela tag
`atlas_npc_auth_emerald` e encaminha jogadores autenticados ao Lobby Emerald,
no mesmo fluxo da bússola, preservando o inventário.

- O Auth Lobby permite apenas NPCs oficiais de navegação, sem economia ou gameplay.
- Easy NPC precisa estar no pacote do cliente.
- Não recriar os protótipos antigos de Villager, FakePlayer ou ArmorStand.
- Detalhes da integração e instalação original: [v1.26.8](versions/v1.26.8.md).
- Coordenadas históricas devem ser conferidas no mapa atual antes de reutilização.

Pendências: gestão configurável de NPCs e conteúdo do Lobby Emerald
(tutorial, crates, rankings, RTP e informações).

## Projeto — NPC de acesso ao Survival

Planejado em 30/09/2026. Mapa do Lobby Emerald declarado concluído pelo usuário.
**Ainda não implementado nem posicionado**; coordenadas e orientação serão fornecidas depois.

### Apresentação proposta

- Nome: **Survival Emerald**.
- Indicação: **Clique para explorar**.
- Corpo `easy_npc:humanoid`, seguindo a integração já utilizada no Auth Lobby.
- Visual sugerido: guia/explorador; skin ainda a definir.
- NPC fixo, persistente, sem caminhada e protegido contra dano e empurrões.
- Dimensão exclusiva: `atlas:emerald`; tag proposta: `atlas_npc_emerald_survival`.

### Fluxo proposto

1. Jogador autenticado clica com a mão principal no NPC.
2. Atlas valida dimensão, identidade do NPC e estado do jogador; freeze, StaffMode, batalha e teleporte pendente não podem ser contornados pelo clique.
3. Abre o menu existente **RTP — Survival Emerald**, com Overworld, Nether e End. O Overworld é o próprio Survival Emerald.
4. A escolha usa `RandomTeleportService`, mantendo busca segura, aquecimento de 3 segundos, cancelamento por movimento e cooldown por cargo.
5. O jogador chega ao destino sem alteração de inventário ou Pokémon. Mundo indisponível e falha na busca retornam uma mensagem, sem teleporte inseguro.

A primeira entrega proposta é acesso por RTP. Não restaurar silenciosamente a última posição salva: uma opção de retorno será uma decisão separada, considerando que `/lobby` atualmente limpa essa posição.

### Implementação prevista

- Estender o roteamento de interação de `LobbyNpcService` para reconhecer a tag do Survival somente no Emerald; preservar o comportamento do NPC de navegação do Auth Lobby.
- Manter as validações em serviço, inclusive no momento de confirmar o menu; listeners apenas encaminham a interação.
- Reutilizar o menu e o serviço de RTP, sem executar comandos com permissão elevada nem duplicar sua lógica.
- Consumir o clique do NPC oficial para não abrir simultaneamente diálogos do Easy NPC; ignorar mão secundária e impedir acionamentos repetidos.
- Verificar como o Easy NPC persiste entidade, skin e proteção antes de escolher a instalação definitiva. Garantir que reinícios não criem cópias.
- Não criar tabela ou migration apenas para esse NPC se a persistência existente do Easy NPC for suficiente.

### Pendências para instalação

- [ ] Receber X, Y, Z, yaw e pitch do local desejado.
- [ ] Definir skin; conferir espaço e chão no local.
- [ ] Implementar interação, validações e proteção do NPC.
- [ ] Testar menu, destinos, cooldown, movimento, cliques repetidos e bloqueios de moderação.
- [ ] Validar que NPC do Auth Lobby continua funcionando.
- [ ] Reiniciar e confirmar persistência, ausência de duplicatas e proteção contra a limpeza global.
- [ ] Registrar versão, compilar e implantar conforme o fluxo de release.
