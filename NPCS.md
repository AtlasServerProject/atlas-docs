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
