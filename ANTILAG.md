# Anti Lag do Atlas

O Atlas complementa Lithium, FerriteCore e ModernFix controlando acúmulo de entidades em todos os mundos carregados, incluindo Auth Lobby, Lobby Emerald, Survival, Nether e End.

## Limpeza automática

- Executada a cada 15 minutos.
- Avisos globais com 60, 30 e 10 segundos de antecedência.
- Remove todos os itens dropados carregados, sem idade mínima, inclusive recém-jogados.
- Remove Pokémon selvagens elegíveis independente do tempo de existência, mesmo que estejam perto de jogadores.

Nunca são removidos Pokémon:

- pertencentes a jogadores;
- em batalha ou ocupados;
- vinculados a pastures;
- lendários ou míticos da lista protegida do Atlas.


A lista protegida usa os IDs internos do Cobblemon e cobre lendários/míticos de Kanto até Paldea, incluindo variações com nomes compostos como `typenull`, `tapukoko`, `gougingfire`, `ironboulder`, `ironcrown`, `wochien`, `chienpao`, `tinglu` e `chiyu`.

## Comandos

- `/atlas tps`: mostra TPS, MSPT e quantidades de entidades, drops e Pokémon em todos os mundos carregados, incluindo Auth Lobby, Lobby Emerald, Survival, Nether e End.
- `/atlas cleanup`: força a mesma limpeza segura; disponível somente para Dono, ADM e console.

Todas as execuções são registradas no log do servidor com as quantidades verificadas e removidas.

## Recuperação de itens

- `/lixeira` abre um baú virtual de 54 espaços.
- Os itens deixados nele ficam recuperáveis por 15 minutos.
- `/dropados` abre os itens disponíveis para o jogador.
- Retirar um item do menu confirma sua recuperação.
- Itens que permanecem no menu ao fechar continuam disponíveis pelo prazo restante renovado.
- Drops removidos pela limpeza automática são armazenados quando o servidor consegue identificar seu jogador proprietário.
- Os dados usam SNBT completo, preservando quantidade, nome, encantamentos e componentes.
- A tabela PostgreSQL `item_recovery_entries` mantém os itens durante reinícios.
- Entradas expiradas são removidas automaticamente e registradas no log.

## Escopo a partir da v1.29.21

A execução manual e o ciclo automático percorrem todas as dimensões na mesma execução. Pokémon selvagens elegíveis dos lobbys também são removidos; as proteções acima continuam valendo. Inventários, baús, blocos e outras entidades não são limpos. Chunks descarregados não são forçados a carregar: seus itens e Pokémon só poderão ser verificados quando estiverem carregados em um próximo ciclo.
