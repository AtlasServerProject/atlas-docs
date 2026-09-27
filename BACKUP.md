# Backup e restauração

## Estado

Implementação concluída e testada em ambiente isolado em 2026-09-27.
Serviço/timer instalados e primeiro backup completo concluído em 2026-09-27 às
22:40 UTC, em 3min22s. Snapshot: `atlas-20260927T223730368915Z`. Serviço de backup
com resultado `success`; Minecraft reiniciado e timer diário habilitado.

## O que é salvo

Cada snapshot contém `database.dump` (PostgreSQL, formato custom), `fabric.tar.gz`
e `manifest.json` com SHA-256 de ambos os arquivos. A pasta Fabric inclui mundos,
mods, configurações, arquivos de jogadores, bibliotecas e arquivos de inicialização.
São excluídos logs, crash-reports, caches `.fabric`/`.mixin.out`, mods desativados
e o socket administrativo. Links simbólicos e arquivos especiais são rejeitados.

A rotina verifica acesso ao banco e espaço antes de parar o serviço `atlas`.
Com o servidor parado, exporta o banco e arquiva os arquivos; publica o snapshot
somente depois de verificar sua integridade. Se o servidor estava ativo, tenta
reiniciá-lo mesmo quando o backup falha. Não usar `service: null` em produção:
esse modo é reservado a fixtures e instalações já mantidas offline pelo operador.
APIs externas que escrevam no banco também precisarão ser paradas se forem adicionadas no futuro.

Backups ficam em `/opt/atlas/server/backups/snapshots`. Permissões restritas
protegem os dados. A retenção padrão é de 30 dias, preservando pelo menos duas
cópias. Somente snapshots desta rotina entram na retenção, após novo backup
concluído. Backups manuais anteriores não são removidos.

## Instalação nesta máquina

O arquivo privado `/home/somente/.config/atlas/backup.pgpass` já foi preparado
fora do Git, com permissão 0600. Não publicar seu conteúdo.

```bash
sudo /home/somente/dev/atlas/infra/scripts/install-backup.sh /home/somente/.config/atlas/backup.pgpass
```

O instalador copia o gerenciador para `/opt/atlas/scripts`, configuração e credencial
para `/etc/atlas`, e as unidades para `/etc/systemd/system`. Executa o primeiro
backup completo antes de habilitar o timer. Essa execução causa indisponibilidade
durante a cópia dos mundos. A senha é lida pelo PostgreSQL via passfile; não aparece
nos argumentos dos processos, nos manifests ou nos arquivos versionados novos.

O timer roda diariamente às **05:00 UTC**, com `Persistent=true` para recuperar
execuções perdidas. Para mudar o horário, editar a unidade do timer e executar
`sudo systemctl daemon-reload` e `sudo systemctl restart atlas-backup.timer`.
Retenção e caminhos ficam em `/etc/atlas/backup.json`.

## Operação

```bash
sudo systemctl start atlas-backup.service
sudo systemctl status atlas-backup.service --no-pager
systemctl list-timers atlas-backup.timer
sudo journalctl -u atlas-backup.service -n 80 --no-pager
```

A CLI do workspace também aceita:

```bash
sudo /home/somente/dev/atlas/infra/scripts/atlas-cli backup
sudo /home/somente/dev/atlas/infra/scripts/atlas-cli backup-verify /opt/atlas/server/backups/snapshots/atlas-DATA
sudo /home/somente/dev/atlas/infra/scripts/atlas-cli restore /opt/atlas/server/backups/snapshots/atlas-DATA --confirm
```

Substituir `atlas-DATA` pelo diretório real do snapshot.
`ATLAS_BACKUP_CONFIG` permite selecionar outro JSON; no gerenciador Python,
`--config CAMINHO` deve vir antes de `backup`, `verify` ou `restore`.

## Restauração de produção

A restauração exige `--confirm`. Valida hashes e caminhos do arquivo antes de
alterar dados, extrai para uma pasta temporária e para o servidor. Cria um backup
de segurança do estado atual antes de restaurar o banco numa transação PostgreSQL.
Depois troca a pasta Fabric e inicia o serviço. A pasta anterior é preservada ao
lado, com sufixo `.pre-restore-*`, e não participa da retenção automática.

Uma falha após a parada mantém o servidor parado para análise, com o backup de
segurança disponível. Banco e filesystem não formam uma transação única: não
reiniciar às cegas depois de erro na troca de diretórios. O restore usa
`pg_restore --clean --if-exists`: recria os objetos presentes no dump; objetos
adicionados ao banco depois do snapshot e ausentes dele não são eliminados.

É necessário espaço para extração e backup de segurança. Não apagar as cópias
anteriores antes de confirmar login, mundos e dados restaurados.

## Recuperação isolada

Preparar um banco de teste vazio e diretório vazio fora da instalação e backups.
O usuário PostgreSQL configurado precisa poder restaurar no banco de teste.

```bash
sudo /home/somente/dev/atlas/infra/scripts/atlas-cli restore /opt/atlas/server/backups/snapshots/atlas-DATA --confirm --target /opt/atlas/recovery-test/fabric --database atlas_recovery_test
```

Esse modo não para nem inicia o serviço, rejeita o nome do banco de produção,
recusa destinos sobrepostos e recusa banco de teste com tabelas/views/sequências.
O passfile precisa conter uma entrada para o banco de teste. O comando não cria
bancos automaticamente nem inicia um segundo Minecraft.

## Testes realizados

```bash
python3 infra/tests/test_backup.py
```

Os testes criam um PostgreSQL temporário com socket privado, sem porta TCP,
e removem o cluster ao terminar. Foram validados round-trip de arquivos e banco,
checksum corrompido, isolamento de destino, trava concorrente, limpeza de execução
incompleta, tentativa de reinício após falha e retenção mínima.
Também foi restaurado um dump do banco real em cluster temporário e conferidas
as contagens de `players`, `homes`, `claims` e `ranks`, sem alterar produção.
A primeira cópia completa dos mundos foi concluída com integridade verificada
pela rotina em 2026-09-27. Recuperação integral desses mundos ainda não foi ensaiada.

## Capacidade

Na implementação, a máquina tinha cerca de 21 GB livres e 12 GB de mundos.
A rotina exige espaço livre equivalente aos arquivos descomprimidos, tamanho do
banco e margem de 512 MiB antes de parar o servidor. Não há garantia de capacidade
para 30 cópias diárias neste disco; monitorar ocupação e planejar armazenamento
externo. Esta rotina ainda não replica backups para outra máquina.

Após o primeiro snapshot, restaram cerca de 14 GB livres. Monitorar antes das
próximas execuções: a retenção de 30 dias não implica espaço disponível para
30 backups; a rotina aborta antes da parada se faltar espaço.
