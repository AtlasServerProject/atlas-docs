# Anti Lag do Atlas

O Atlas complementa Lithium, FerriteCore e ModernFix controlando acúmulo de entidades no Survival Emerald.

## Limpeza automática

- Executada a cada 15 minutos.
- Avisos globais com 60, 30 e 10 segundos de antecedência.
- Remove somente drops com pelo menos 5 minutos no chão.
- Remove somente Pokémon selvagens com pelo menos 5 minutos de existência e a mais de 64 blocos de todos os jogadores.

Nunca são removidos Pokémon:

- pertencentes a jogadores;
- em batalha ou ocupados;
- vinculados a pastures;
- próximos de jogadores;
- existentes nos lobbys.

## Comandos

- `/atlas tps`: mostra TPS, MSPT e quantidades de entidades, drops e Pokémon no Survival Emerald.
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
