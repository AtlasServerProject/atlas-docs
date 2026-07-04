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
