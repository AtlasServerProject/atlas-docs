# Loja Atlas — catálogo e condições em definição

Atualização: 30/09/2026. Vitrine: https://atlas-cobblemon.netlify.app/store.

## Decisões do dono

- VIP 1 (rank VIP), VIP 2 (VIP ✦) e VIP 3 (VIP ✦✦).
- Duração comercial planejada: 30 dias, sem renovação automática.
- Kits são benefícios dos planos, sem cobrança adicional e sem venda avulsa.
- Caixas serão produtos separados em etapa futura. Nenhuma caixa/chave está incluída nos planos apresentados.
- Preços aprovados pelo dono: VIP 1 R$ 25,00; VIP 2 R$ 35,00; VIP 3 R$ 50,00. Valores totais por 30 dias, com kits incluídos. Preços de pré-lançamento, sujeitos a alteração até a abertura das vendas, conforme orientação do dono.

| Plano | Preço total / 30 dias | Kits próprios | Acesso herdado |
| --- | --- | --- | --- |
| VIP 1 | R$ 25,00 | Diário, semanal e mensal VIP 1 | Nenhum nível VIP anterior |
| VIP 2 | R$ 35,00 | Diário, semanal e mensal VIP 2 | Kits VIP 1 |
| VIP 3 | R$ 50,00 | Diário, semanal e mensal VIP 3 | Kits VIP 1 e VIP 2 |

## Apresentação ao cliente

Cards separam preço total, duração, disponibilidade e acesso aos kits. Tabela compara planos. Seleção de plano apresenta prints originais ampliáveis e lista textual com quantidades por resgate, não totais mensais. Benefícios de outros níveis são acessíveis separadamente pelo menu /kits.

Os prints ilustram resgates: Mints, pedras e Bottle Caps aleatórios não garantem a variante mostrada. Mints à escolha abrem menu próprio. VIP 2 mensal contém 5 Bottle Caps OBC, conforme execução atual (1+4 do mesmo item).

## Regras verificadas no servidor

Fonte: atlas-core/src/main/java/io/atlas/modules/kit/service/DailyKitService.java. Cooldowns individuais após resgate: diário 24 horas, semanal 7 dias, mensal 30 dias. Não há entrega automática. O acesso depende do rank. Não prometer número fixo de resgates nem dois kits mensais em uma ativação de 30 dias. A expiração comercial automática do VIP ainda precisa ser implementada.

## Pendências antes de vender

1. Preços confirmados; vendas ainda não habilitadas.
2. Aprovar catálogo final e revisão de equilíbrio dos benefícios.
3. Definir início da validade, prazo de ativação, renovação manual, upgrades e tratamento dos cooldowns entre ativações.
4. Implementar pagamento, identificação segura do jogador, entrega auditável e expiração.
5. Definir atendimento e condições aplicáveis a cancelamentos, reembolsos e indisponibilidade, com revisão apropriada antes de publicar termos definitivos.
6. Validar compra/ativação/resgate/expiração de ponta a ponta.

Não inventar regras de reembolso, prazo de entrega ou garantias. Vendas permanecem fechadas. A documentação é especificação do produto em elaboração, não termos finais de compra.
