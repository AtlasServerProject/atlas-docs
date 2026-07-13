# Soundtrack do Atlas

Este documento guarda a curadoria de músicas do Atlas usando faixas selecionadas do pacote completo do CobbleSongs/CobbleSounds.

## Decisão

O Atlas não deve voltar a usar o pacote completo como obrigatório para todos os jogadores. O pacote completo ficou pesado demais e já foi removido do modpack padrão durante os testes de conexão.

A abordagem correta é criar um pacote leve contendo apenas as faixas aprovadas abaixo, mas mantendo os IDs originais do CobbleSounds. O primeiro teste com IDs customizados `atlas.music.*` não tocou no cliente; o formato funcional é o mesmo do CobbleSounds original.

Nome do pacote atual:

```text
CobbleSounds[AtlasLite]_v1.4.1.zip
```

## Músicas por contexto

| Contexto | Faixas |
| --- | --- |
| Perto do mar, navegando de bote ou voando perto do mar | `sea_mauville_unova.ogg`, `surfing_hoenn2.ogg` |
| Rotas/cidades iniciais de exploração | `route1_sinnoh.ogg`, `accumula_town_unova.ogg`, `driftveil_city_unova2.ogg` |
| Shopping | `azalea_town_sinnoh.ogg` |
| Cavernas | `pettleburg_woods-granite_cave.ogg` |
| Templos lendários | `dragonspiral_tower.ogg` |
| Batalhas contra Regis | `battle_regis_hoenn.ogg` |
| Lobby Hub/Auth Lobby | `rustboro_city_hoenn2.ogg` |
| The End | `distortion_world_sinnoh.ogg` |
| Lobby Emerald | `introductions_hoenn.ogg` |

## Regras de implementação

- As músicas devem tocar apenas para o jogador que entrou no contexto.
- O sistema deve evitar reiniciar a mesma música a cada tick.
- Ao trocar de mundo ou região, o tema anterior deve ser interrompido antes do novo tema.
- Música de batalha tem prioridade sobre música de área.
- Ao terminar/fugir/encerrar uma batalha, o tema da área atual deve voltar automaticamente.
- As músicas futuras de shopping, templos lendários e batalhas de Regis ficam guardadas até os respectivos sistemas existirem.
- O pacote de áudio deve conter somente as faixas usadas pelo Atlas para evitar travamentos em `Entrando no mundo...`.
- O Atlas Core toca diretamente os temas principais por ID `cobblesounds:*`, sem depender da rotação vanilla do Minecraft.

## Pendências

- [x] Receber ou localizar o pacote que contém os arquivos `.ogg`.
- [x] Criar resource pack leve com `sounds.json` próprio do Atlas.
- [x] Trocar os temas vanilla atuais do `WorldThemeService` por IDs de som do resource pack.
- [x] Dar prioridade à música de batalha sobre os temas de área.
- [x] Variar o tema do Survival/RTP por contexto simples.
- Definir detecção de região para mar, cavernas, shopping e templos.
- Definir gatilho futuro de batalha para Regis.

## Resource pack gerado

Arquivo separado:

```text
/home/somente/dev/atlas/CobbleSounds[AtlasLite]_v1.4.1.zip
```

Incluído no modpack:

```text
/home/somente/dev/atlas/atlas-client-modpack-2026-07-07-v10-cobblesounds-atlaslite.tar.gz
```

Versão atual do modpack com correção dos temas:

```text
/home/somente/dev/atlas/atlas-client-modpack-2026-07-09-v11-cobblesounds-themefix.tar.gz
```

Tamanho aproximado do pack separado:

```text
25 MB
```

IDs de som disponíveis no padrão original do CobbleSounds:

- `cobblesounds:sea_mauville_unova`
- `cobblesounds:surfing_hoenn`
- `cobblesounds:surfing_hoenn2`
- `cobblesounds:route1_sinnoh`
- `cobblesounds:accumula_town_unova`
- `cobblesounds:driftveil_city_unova2`
- `cobblesounds:azalea_town_sinnoh`
- `cobblesounds:pettleburg_woods-granite_cave`
- `cobblesounds:dragonspiral_tower`
- `cobblesounds:battle_regis_hoenn`
- `cobblesounds:rustboro_city_hoenn2`
- `cobblesounds:distortion_world_sinnoh`
- `cobblesounds:introductions_hoenn`

Temas ativos no Atlas Core:

| Mundo | ID tocado pelo servidor |
| --- | --- |
| Auth Lobby / Lobby Hub | `cobblesounds:rustboro_city_hoenn2` |
| Lobby Emerald | `cobblesounds:introductions_hoenn` |
| Survival Emerald — rota base | `cobblesounds:route1_sinnoh` |
| Survival Emerald — rota/cidade alternativa | `cobblesounds:accumula_town_unova`, `cobblesounds:driftveil_city_unova2` |
| Survival Emerald — água/mar | `cobblesounds:sea_mauville_unova`, `cobblesounds:surfing_hoenn2` |
| Survival Emerald — caverna | `cobblesounds:pettleburg_woods-granite_cave` |
| Batalha temporária | `cobblesounds:battle_regis_hoenn` |

Observação: `battle_regis_hoenn` está sendo usado temporariamente como tema geral de batalha porque já está no pacote Lite. Quando a trilha de batalha comum for escolhida, ela substituirá essa faixa sem mudar a arquitetura.
