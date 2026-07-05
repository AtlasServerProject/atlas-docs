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

## Próximos cuidados

- Migrar comandos futuros de economia para a mesma ponte.
- Validar lojas, banco e recompensas do CobbleDollars antes de liberar economia avançada.
- Decidir se o banco legado `economy_accounts` será removido, migrado ou mantido apenas para auditoria.
