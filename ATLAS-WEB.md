# Atlas Web — melhorias pendentes

Registro: 2026-09-29. Repositório: https://github.com/AtlasServerProject/atlas-web.

Trabalho adiado a pedido do usuário para retomar o servidor. Esta lista registra
a revisão do código e do conteúdo; a avaliação visual no navegador ainda está pendente.

## Prioridade 1 — identidade e entrada do jogador

- [ ] Padronizar a identidade para **Atlas Cobblemon**, removendo referências a Pixelmon da home e da loja.
- [ ] Concluir o fluxo **Como jogar**: download real do modpack oficial, instruções de instalação, versões necessárias, IP confirmado e botão para copiar o endereço.
- [ ] Conectar os botões de instalação e download às ações correspondentes; atualmente não têm ação.
- [ ] Substituir textos de protótipo e de desenvolvimento por informações úteis ao jogador: proposta do servidor, recursos disponíveis e primeiros passos.
- [ ] Remover ou reescrever textos como “Logo Atlas integrada”, “Base pronta para integrar o backend Spring” e notícias sobre a estrutura técnica do site.
- [ ] Revisar acentuação e consistência dos textos.

## Prioridade 2 — informações reais e funcionalidades pendentes

- [ ] Substituir o status “Offline” fixo por informação real, com estado de indisponibilidade quando não for possível consultar; enquanto não houver integração, indicar claramente que está em preparação.
- [ ] Revisar notícias, datas e informações de abertura para publicar apenas conteúdo confirmado.
- [ ] Identificar a loja como em preparação enquanto não houver compra e entrega funcionando; evitar botões “Assinar” e “Adicionar” sem resposta.
- [ ] Conferir preços, planos, benefícios VIP, regras de entrega e comandos anunciados (`/caixas` e `/chaves`) com o que está efetivamente disponível no servidor.
- [ ] Planejar compra e entrega dos produtos em uma etapa posterior ao fluxo de entrada do jogador.

## Prioridade 3 — navegação e revisão visual

- [ ] Corrigir “Equipe”, que atualmente leva à seção de novidades; criar um destino adequado ou retirar o link até existir conteúdo.
- [ ] Tornar os atalhos da home funcionais e revisar todos os destinos de navegação.
- [ ] Compartilhar cabeçalho e menu entre as páginas para evitar duplicação e diferenças de navegação.
- [ ] Avaliar o site no navegador em desktop e celular, incluindo legibilidade, navegação por teclado e comportamento dos botões.

Ordem sugerida ao retomar: **Como jogar → home com conteúdo real → navegação e revisão visual → loja e integrações**.
