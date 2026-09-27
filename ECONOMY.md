# Economia Atlas

## Decisão atual

A economia oficial do Atlas passa a usar o `CobbleDollars` como fonte de saldo.

Na prática:

- Atlas Coins e CobbleDollars representam a mesma moeda no servidor;
- `/saldo` exibe o saldo atual do CobbleDollars;
- `/addmoney <valor>` adiciona CobbleDollars ao jogador que executou o comando;
- o banco antigo `economy_accounts.balance` fica preservado apenas como legado por enquanto.

## Motivo

O `CobbleDollars` já conversa naturalmente com a experiência Cobblemon, incluindo ganhos por batalha e sistemas próprios de loja/banco. Integrar o Atlas a ele evita duas moedas paralelas e reduz conflito entre comandos, recompensas e módulos futuros.

## Regra de arquitetura

O Atlas não depende diretamente da API de compilação do CobbleDollars.

A integração usa uma ponte em tempo de execução:

- se o CobbleDollars estiver instalado, o Atlas lê e grava o saldo nele;
- se o CobbleDollars estiver ausente ou mudar a API, o Atlas registra aviso no log e não derruba o servidor.

## Comandos afetados

### `/saldo`

Mostra o saldo CobbleDollars do jogador.

### `/addmoney <valor>`

Adiciona CobbleDollars ao próprio jogador.

Permissão necessária:

```text
atlas.economy.addmoney
```

### `/pay <player> <valor>`

Transfere CobbleDollars entre jogadores online.

Regras:

- o valor mínimo é `1`;
- o jogador não pode pagar a si mesmo;
- o destino precisa estar online;
- a transferência só acontece se o pagador tiver saldo suficiente.

### `/kits`

Abre a interface de kits disponíveis do Atlas.

Entrega inicial:

- Kit Diário;
- Kit Semanal;
- Kit Mensal;
- se o inventário estiver cheio, os itens são dropados aos pés do jogador.

Os kits usam o `Baú do Gimmighoul` como ícone na interface. A diferenciação visual é feita pela cor do nome/lore de cada kit.

#### Kit Diário

Cooldown: 24 horas.

Recompensas:

- 15 Poké Bolas;
- 10 Super Bolas;
- 5 Ultra Bolas;
- 1 Pá de Claim do Atlas.

#### Kit Semanal

Cooldown: 7 dias.

Recompensas:

- 16 Poké Bolas;
- 8 Super Bolas;
- 4 Ultra Bolas;
- 8 Doces Raros.

#### Kit Mensal

Cooldown: 30 dias.

Recompensas:

- Picareta inicial com Inquebrável III;
- Machado inicial com Inquebrável III;
- Pá inicial com Inquebrável III;
- Enxada inicial com Inquebrável III;
- 32 Poké Bolas;
- 16 Super Bolas;
- 8 Ultra Bolas;
- 16 Doces Raros;
- 1 Pá de Claim do Atlas.

#### Kit VIP Diário

Cooldown: 24 horas.

Requer: VIP ou superior.

Recompensas:

- 24 Poké Bolas;
- 16 Super Bolas;
- 8 Ultra Bolas;
- 2 Doces Raros;
- 2 Exp. Candy M;
- 2 Revives.

#### Kit VIP Semanal

Cooldown: 7 dias.

Requer: VIP ou superior.

Recompensas:

- 32 Poké Bolas;
- 16 Super Bolas;
- 8 Ultra Bolas;
- 12 Doces Raros;
- 8 Exp. Candy L;
- 5 Revives;
- 1 Mint aleatória;
- 1 Pedra de Evolução aleatória.

#### Kit VIP Mensal

Cooldown: 30 dias.

Requer: VIP ou superior.

Recompensas:

- 64 Poké Bolas;
- 32 Super Bolas;
- 16 Ultra Bolas;
- 32 Doces Raros;
- 16 Exp. Candy XL;
- 10 Revives;
- 2 Max Revives;
- 2 Mints aleatórias;
- 2 Pedras de Evolução aleatórias;
- 1 Lucky Egg;
- 1 Bottle Cap de status aleatório.

#### Kit VIP ✦ Diário

Cooldown: 24 horas.

Requer: VIP ✦ ou superior.

Recompensas:

- 1 Exp. Share;
- 2 Exp. Candy XL;
- 1 Max Revive.

#### Kit VIP ✦ Semanal

Cooldown: 7 dias.

Requer: VIP ✦ ou superior.

Recompensas:

- 1 Lucky Egg;
- 1 Ability Capsule;
- 2 Mints aleatórias.

#### Kit VIP ✦ Mensal

Cooldown: 30 dias.

Requer: VIP ✦ ou superior.

Recompensas:

- 1 Destiny Knot;
- 1 Everstone;
- 2 Lucky Eggs;
- 2 Ability Capsules;
- 1 Silver Bottle Cap;
- 4 Bottle Caps.

#### Kit VIP ✦✦ Diário

Cooldown: 24 horas.

Requer: VIP ✦✦ ou superior.

Recompensas:

- 2 Exp. Candy XL;
- 2 Max Revives;
- 1 Mint à escolha.

#### Kit VIP ✦✦ Semanal

Cooldown: 7 dias.

Requer: VIP ✦✦ ou superior.

Recompensas:

- 2 Silver Bottle Caps;
- 3 Ability Capsules;
- 16 Exp. Candy XL.

#### Kit VIP ✦✦ Mensal

Cooldown: 30 dias.

Requer: VIP ✦✦ ou superior.

Recompensas:

- 1 Master Ball;
- 1 Golden Bottle Cap;
- 2 Ability Patches;
- 3 Lucky Eggs;
- 2 Destiny Knot;
- 2 Everstones;
- 5 Bottle Caps de status aleatórios;
- 5 Mints à escolha.

Atalho direto:

```text
/kit diario
/kit semanal
/kit mensal
/kit vip
/kit vipdiario
/kit vipsemanal
/kit vipmensal
/kit vip+
/kit vipplus
/kit vipplusdiario
/kit vipplussemanal
/kit vipplusmensal
/kit vip++
/kit vipplusplus
/kit vipplusplusdiario
/kit vipplusplussemanal
/kit vipplusplusmensal
```

O kit diário existe para garantir que todo jogador consiga criar claims sem depender de staff entregar a pá dourada manualmente.

## Próximos cuidados

- Migrar comandos futuros de economia para a mesma ponte.
- Validar lojas, banco e recompensas do CobbleDollars antes de liberar economia avançada.
- Decidir se o banco legado `economy_accounts` será removido, migrado ou mantido apenas para auditoria.
