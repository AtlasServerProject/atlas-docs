# Acesso externo com Playit

O Playit publica o servidor Minecraft na internet sem exigir abertura manual de portas no roteador.

## Verificar o agente

```bash
sudo playit status
```

Esse comando confirma se o agente está configurado e em execução. Ele não mostra o endereço público do servidor.

## Consultar o túnel e o endereço externo

```bash
sudo playit attach
```

O comando conecta o terminal ao agente e permite visualizar os túneis configurados. O túnel do Minecraft deve encaminhar para:

```text
127.0.0.1:25565
```

O endereço entregue aos jogadores aparece no painel ou no agente, normalmente como um domínio `*.gl.joinmc.link` acompanhado de uma porta quando necessária.

Pressione `Ctrl+C` para sair da visualização. O serviço do Playit continuará funcionando em segundo plano.

O mesmo endereço também pode ser consultado no painel:

<https://playit.gg/account/tunnels>

## Verificar os serviços do Atlas

```bash
systemctl is-active atlas
systemctl is-active playit
```

Os dois comandos devem retornar `active` para que o servidor esteja disponível externamente.
