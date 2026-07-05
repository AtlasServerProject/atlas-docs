# NPCs do Atlas

## Referência de design

O sistema de NPCs do Atlas segue a ideia central de plugins como Citizens:

- NPC persistente;
- nome visível;
- sem IA;
- invulnerável;
- ação ao clicar;
- controle total pelo servidor.

Como o Atlas roda em Fabric, a implementação é nativa no `atlas-core`, sem depender de plugin Bukkit.

## Decisão para o Auth Lobby

O Auth Lobby continua sendo um ambiente sem gameplay.

A exceção permitida é NPC oficial de navegação do Atlas.

Isso significa:

- NPCs promocionais, externos ou de mapa baixado devem ser removidos;
- NPCs de economia, crates, loja ou gameplay não devem existir no Auth Lobby;
- NPCs oficiais podem existir apenas para guiar o jogador após autenticação.

## NPC inicial

### Lobby Emerald

NPC criado no Auth Lobby:

```text
Nome: Lobby Emerald (clique)
Tipo: Villager vanilla
Mundo: minecraft:overworld
X: 628.622
Y: 123.0
Z: 3535.462
Yaw: -90.0
```

Comportamento:

- antes do login: avisa que o jogador precisa autenticar;
- após login/autologin: envia o jogador para o Lobby Emerald;
- usa o mesmo fluxo da bússola, preservando o inventário real do jogador.

## Próximos passos

- Permitir configurar NPCs em arquivo ou banco.
- Criar comando administrativo para mover/criar/remover NPCs.
- Adicionar NPCs do Lobby Emerald:
  - tutorial;
  - crates;
  - rankings;
  - RTP para Survival Emerald;
  - informações do servidor.
