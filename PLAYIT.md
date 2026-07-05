# Acesso externo com Playit

O Playit publica o servidor Minecraft na internet sem exigir abertura manual de portas no roteador.

## Passo a passo para abrir o servidor de testes para amigos

Use este fluxo sempre que quiser chamar alguém de fora da sua rede para testar o Atlas.

### 1. Ligar o servidor Atlas

```bash
sudo systemctl start atlas
```

Confirme se ele subiu:

```bash
systemctl is-active atlas
```

O retorno esperado é:

```text
active
```

Se quiser acompanhar o boot:

```bash
journalctl -u atlas -n 80 --no-pager
```

Procure uma linha parecida com:

```text
Done
```

### 2. Ligar o Playit

```bash
sudo systemctl start playit
```

Confirme se o agente está rodando:

```bash
systemctl is-active playit
```

O retorno esperado também é:

```text
active
```

### 3. Conferir o túnel

```bash
sudo playit status
```

Esse comando confirma que o agente está autenticado e conectado.

Para visualizar o túnel em tempo real:

```bash
sudo playit attach
```

O túnel do Minecraft precisa apontar para:

```text
127.0.0.1:25565
```

O endereço externo normalmente aparece no formato:

```text
algum-nome.gl.joinmc.link
```

ou:

```text
algum-nome.gl.joinmc.link:porta
```

Se o terminal ficar preso no Playit, use `Ctrl+C`. Isso fecha só a visualização; o serviço continua rodando.

### 4. Conferir no painel do Playit

Caso o endereço não apareça claro no terminal, acesse:

<https://playit.gg/account/tunnels>

No túnel do Minecraft, confirme:

- tipo/protocolo de Minecraft Java;
- destino local `127.0.0.1:25565`;
- endereço público gerado pelo Playit.

### 5. Passar o acesso para os amigos

Envie para o jogador:

- o endereço externo do Playit;
- a versão do Minecraft: `1.21.1`;
- o loader: Fabric;
- o pacote de mods atualizado do Atlas.

Com os addons do Cobblemon instalados no servidor, o jogador precisa usar o mesmo pacote de mods no cliente. Se o cliente não tiver os mods necessários, ele pode cair ao tentar entrar ou ver erros de registro/itens.

### 6. Checklist rápido antes do teste

```bash
systemctl is-active atlas
systemctl is-active playit
sudo playit status
```

Tudo certo quando:

- `atlas` está `active`;
- `playit` está `active`;
- o túnel aponta para `127.0.0.1:25565`;
- o jogador usa Minecraft `1.21.1` com Fabric e os mods do Atlas.

### 7. Problemas comuns

Se o amigo não conseguir entrar:

- verifique se o endereço do Playit está correto;
- confirme se o servidor Atlas está `active`;
- confirme se o Playit está `active`;
- confira se o amigo instalou o pacote de mods correto;
- veja os logs do servidor:

```bash
journalctl -u atlas -n 120 --no-pager
```

Se o jogador cair ao conectar logo após adicionarmos mods, quase sempre é diferença entre os mods do cliente e do servidor.

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
