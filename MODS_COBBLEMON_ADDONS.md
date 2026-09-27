# Mods e compatibilidade

Referência do pacote documentado para Minecraft `1.21.1`, Fabric Loader `0.17.3`
e Cobblemon `1.7.3`. Antes de distribuir um cliente, conferir os JARs ativos em
`/opt/atlas/server/fabric/mods/` e os mods efetivamente carregados no último boot.

## Componentes registrados

| Grupo | Mods |
| --- | --- |
| Economia e itens | CobbleDollars, Only Bottle Caps, SimpleTMs, TM Craft |
| Gameplay | Cobbreeding, SafePastures, PastureLoot, CobbleCuisine, PokéBlocks, MoreCobblemonTweaks |
| Batalhas e progressão | Raid Dens, Additions, Battle Extras, Battle Positions, Mega Showdown, Z-A Mega, Cobbleverse Badges |
| Navegação e decoração | CobbleNav, CobbleFurnies, Easy NPC |
| Operação | WorldEdit e Chunky |
| Performance do servidor | ModernFix, FerriteCore, Lithium, Krypton, PacketFixer |
| Cliente | Xaero Minimap, MouseTweaks, Controlling, BetterF3, Zoomify, BetterThirdPerson, NotEnoughAnimations, EntityCulling, ImmediatelyFast, CatchIndicator e CatchRate Display |
| Resource packs | Cobblemon Interface, E19 Cobblemon Minimap Icons e CobbleSounds AtlasLite |

As dependências devem acompanhar as versões escolhidas dos mods. Não copiar mods
exclusivos do cliente para o servidor. `atlas-core.jar` é exclusivo do servidor.
Easy NPC e mods que adicionam itens/registros precisam de versões compatíveis no cliente.

## Decisões preservadas

- Sophisticated Backpacks/Core/Storage foram removidos após problemas de carregamento do mapa.
- CobbleSounds Complete foi substituído pelo AtlasLite; detalhes em [SOUNDTRACK.md](SOUNDTRACK.md).
- Fight or Flight foi excluído por decisão de gameplay.
- Tim's TMs avaliado exigia Cobblemon anterior a 1.7.0; não foi instalado.
- CobbleTowns avaliado era para Minecraft 1.20.1; permanece pendente de versão compatível.
- O pacote v13 atualizou ícones para E19; pacotes QoL e gameplay foram distribuídos separadamente depois dele.

## Atualização e diagnóstico

1. Preservar uma cópia dos mods antes de substituir JARs.
2. Conferir versões, dependências e lado cliente/servidor no `fabric.mod.json`.
3. Reiniciar o servidor e conferir o boot: copiar JARs não os carrega no processo ativo.
4. Testar entrada, inventário, itens novos e receitas com cliente alinhado.
5. Validar worldgen em chunks novos; não regenerar produção sem backup.

O erro `Failed to decode packet 'serverbound/minecraft:set_creative_mode_slot'`
foi associado a registros diferentes entre cliente e servidor. O alinhamento da
[v1.28.7](versions/v1.28.7.md) documenta a correção; o teste dos itens em jogo
continua necessário após mudanças no pacote.

O histórico resumido está no [CHANGELOG.md](CHANGELOG.md). Listas antigas de
pacotes de diagnóstico e caminhos temporários podem ser recuperados pelo Git.
