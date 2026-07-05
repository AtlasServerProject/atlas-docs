# Runtime do servidor Atlas

## Memória Java

A máquina atual possui cerca de `5.1 GiB` de RAM. Por isso o Atlas não deve subir com `-Xmx6G`, pois o Java pode tentar reservar mais memória do que existe disponível e acionar o OOM killer do Linux.

Configuração ativa recomendada:

```bash
java -Xms1G -Xmx4G -jar fabric-server-launch.jar nogui
```

Arquivo ativo no servidor:

```text
/opt/atlas/server/fabric/start.sh
```

Template versionado:

```text
infra/templates/start.sh
```

## OOM killer

Se aparecer no status do serviço:

```text
The kernel OOM killer killed some processes in this unit
```

significa que o servidor tentou usar memória demais. Ações recomendadas:

1. pausar ou cancelar tarefas pesadas do Chunky;
2. reiniciar o Atlas;
3. validar `-Xmx4G`;
4. conferir TPS;
5. evitar testes com jogadores enquanto houver pré-geração pesada.

## Pré-geração pesada

O Survival Emerald atual possui `12000 × 12000` blocos planejados. Pré-gerar tudo com Chunky consome CPU, RAM e disco.

Use somente fora de horário de testes:

```bash
infra/scripts/atlas-cli pregenerate-survival continue
```

Pause ao terminar o período de manutenção:

```bash
infra/scripts/atlas-cli pregenerate-survival pause
```
