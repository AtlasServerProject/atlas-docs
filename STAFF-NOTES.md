# Staff Notes e Histórico

Entregue no Atlas Core **1.29.19**. Registros internos persistidos no PostgreSQL.

## Comandos

| Comando | Função |
| --- | --- |
| `/staffnotes add <jogador> <texto>` | Adiciona uma nota interna e retorna o ID. |
| `/staffnotes list <jogador> [pagina]` | Lista notas não arquivadas, cinco por página. |
| `/staffnotes archive <jogador> <id> <motivo>` | Arquiva uma nota, preservando conteúdo, autoria e motivo. |
| `/history <jogador> [pagina]` | Reúne notas, arquivamentos, punições e revogações, do mais recente ao mais antigo. |

Exemplo: `/staffnotes add Jogador Cooperou durante a análise da denúncia.`
Para corrigir uma nota, arquive-a com motivo e adicione outra; não há edição nem exclusão definitiva por comando.

## Acesso e privacidade

- Staff autenticada pode consultar e registrar informações somente sobre jogadores de cargo inferior ao seu. Isso também bloqueia consulta sobre si mesmo e cargos iguais.
- Console administrativo com permissão 4 pode acessar todos os jogadores cadastrados.
- Funciona com jogadores offline já registrados no banco, por nome atual e sem diferenciar maiúsculas/minúsculas.
- Respostas são privadas ao executor; não há broadcast nem notificação ao alvo.
- Os novos comandos são permitidos no StaffMode. Freeze continua bloqueando comandos de quem está congelado.
- Texto e motivo aceitam de 1 a 500 caracteres após remover espaços nas extremidades, sem controles ou códigos de formatação `§`.
- Qualquer staff autorizada sobre o alvo pode arquivar uma nota, independentemente de quem a escreveu. A identidade do responsável fica registrada.

## Histórico e persistência

As notas são vinculadas ao ID persistente do jogador, preservando o vínculo quando o nome muda.
Cada entrada mostra tipo, ID, autor, data em UTC, conteúdo e estado atual. Um arquivamento ou revogação aparece como evento próprio, com responsável e motivo. IDs pertencem a seus respectivos tipos; nota #1 e punição #1 podem coexistir.

Avisos e kicks aparecem como registros; bans e mutes indicam se estão ativos, expirados ou revogados. O histórico consulta também punições anteriores a esta versão que tenham vínculo com o jogador.

O escopo é **notas e punições do Atlas**, não um registro de todos os comandos da equipe. Banimentos somente por IP, bans vanilla e logs de freeze/inspeção/StaffMode não são incluídos nesta consulta. `/punishments` continua disponível com seu comportamento anterior.

Migration: `database/migrations/032_staff_notes.sql`. Cria `staff_notes` e índices de consulta. O arquivamento é atômico: uma segunda tentativa não sobrescreve o primeiro motivo. Consultas não usam cache para refletir imediatamente alterações feitas por outros membros da equipe. A paginação pode deslocar itens se houver novos registros entre consultas.

## Validação

- Build Java/Fabric aprovado; v1.29.19 instalada e inicialização do servidor confirmada.
- Registro dos comandos e consultas somente leitura validados pelo console administrativo.
- `python3 infra/tests/test_staff_notes.py`: PostgreSQL temporário; aplicação repetida da migration, persistência em nova conexão, isolamento entre jogadores, arquivamento, ordenação/paginação, alteração de nome, punições e revogações, política de acesso e validação de texto aprovados.
- O teste executa o repositório e as políticas reais; não simula cliente Minecraft nem substitui testes em jogo.

### Checklist em jogo — pendente

- [ ] Player comum e staff sem login não acessam os comandos.
- [ ] Cargo igual/superior e consulta ao próprio jogador são bloqueados.
- [ ] Staff autorizada adiciona, consulta e arquiva nota de jogador online e offline.
- [ ] Jogador alvo não recebe a nota no chat.
- [ ] Histórico mostra punição, revogação e arquivamento com autoria correta.
- [ ] Paginação e consulta durante StaffMode funcionam.
- [ ] Registros continuam disponíveis após reconexão e reinício.
