# Acesso externo com Playit

O túnel Minecraft Java deve apontar para `127.0.0.1:25565`.

## Iniciar e conferir

```bash
sudo systemctl start atlas
sudo systemctl start playit
systemctl is-active atlas
systemctl is-active playit
sudo playit status
```

Os dois serviços devem retornar `active`. Consulte o endereço público em
`sudo playit attach` ou no [painel de túneis](https://playit.gg/account/tunnels).
`Ctrl+C` encerra apenas a visualização do agente.

## Acesso dos jogadores

Enviar endereço público (e porta quando indicada), Minecraft `1.21.1`, Fabric
e o pacote compatível de mods do Atlas. Veja [mods e compatibilidade](MODS_COBBLEMON_ADDONS.md).

Se a conexão falhar, conferir túnel, serviços, versões do cliente e logs:

```bash
journalctl -u atlas -n 120 --no-pager
```
