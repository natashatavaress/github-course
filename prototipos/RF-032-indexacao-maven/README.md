# Protótipo funcional — RF-032 Forçar Indexação Maven (eTCE Web)

Protótipo navegável com dados simulados do fluxo principal do RF-032 (Fluxo 01 — Reindexar
processo) e das demais áreas da Tela 01: Resultados e Acompanhamento (com as ações de reprocessamento abaixo da tabela).

- Artefato publicado: https://claude.ai/artifact/MySLubB3dNxaqUfx1pQ2ef
- `Main.dc.html` — fonte do artboard (formato Design Component do canvas de design)
- `canvas.json` — índice do canvas

Tweaks disponíveis no artefato: perfil (com a função · SERV-SISTEMAS, com a função · outro
setor, sem a função), falha do Maven Docs (nenhuma, falha em um item, HTTP 503, tempo
esgotado), falha ao registrar o pedido, lotes vazios e lote em execução por outro usuário.

Acesso somente pelo menu lateral ("Forçar Indexação Maven"); a tela abre com o campo
"Processo a ser reindexado" vazio, com autocompletar.

Processos simulados (digite no campo de busca): 202600047000118 (erro e não processados),
202500047001842 (todos publicados), 202600047000233 (pendente em retomada — RN18),
202500047002010 (retomada esgotada), 202600047000301 (falha no modo ausentes),
202600047000412 (sem documentos no sumário) e 20260004700011 (trecho de número — CA10).

## Decisões tomadas onde o PRD é ambíguo

1. Layout padrão do eTCE Web ([`../PADRAO_LAYOUT.md`](../PADRAO_LAYOUT.md)), com fonte Poppins no lugar de Product Sans (indisponível na web).
2. Menu (dúvida 03): "Forçar Indexação Maven" como item de primeiro nível do menu lateral, depois de "Distribuir processos"; rota `/forcar-indexacao-maven`.
3. Layout (dúvida 12): cartões empilhados — título, "Reindexar processo", "Resultados" e "Acompanhamento da indexação". Não há área "Lotes": "Reprocessar Todas Autuações Em Andamento" e "Reindexar Documentos com Erro" ficam no fim do cartão "Acompanhamento da indexação", abaixo da tabela, visíveis só ao setor autorizado (RN11). "Consultar situação" fica junto de "Reindexar Processo", pois usa o mesmo campo.
4. Resultados mostram só a execução mais recente; um novo disparo substitui a lista (no legado o texto acumulava).
5. "Consultar situação" continua habilitado durante uma execução (a RN12 só desabilita os três botões de reindexação); durante a consulta, todos os botões de ação ficam desabilitados.
6. Recusas (RN17, RN18) e falha ao registrar (RN13) aparecem como alerta abaixo das ações; mensagem final e lote vazio aparecem em Snackbar.
7. Erros de validação (RN03, RN04) aparecem junto ao campo, também para "Consultar situação".
8. Situação "Pendente" só existe no modo "Todos os documentos"; o modo "Só documentos ausentes" usa a procedure e não chama o Maven, por isso não é afetado pela simulação de falha do Maven.
9. Documento que deixou o índice (RL14) aparece como "Pedido registrado" com a mensagem do legado, pois a gravação é confirmada.
10. Processo sem documentos no sumário (dúvida 14): lista vazia, chip "Sem documentos no sumário" e "Situação do processo" não exibida.
11. A coluna "Documento" do acompanhamento mostra o nome, com o id de origem e o id Maven em linha secundária.
12. Lote de autuações: as autuações excluídas por pendência em retomada (RN09/CA47) são informadas no resumo da execução.
13. "Atualizar" simula o avanço da indexação externa (fila → conversão → pronto → publicado) para demonstrar o CA37; sem o acionamento, a lista não muda.
14. Retomada automática (Fluxo 06, passo 04) não é simulada: é processamento do back-end, sem tela. A pendência gerada aparece no acompanhamento, com 1 tentativa e próxima tentativa em 15 min (RN19).
15. Execução em segundo plano (RN12/CA49–CA50) simulada pela troca de tela: ao ir para "Processos" e voltar, a execução continua e mostra os itens concluídos; o item do menu lateral mostra um indicador de execução.
16. Usuário sem a função `funReindexarProcessoMaven`: o item "Forçar Indexação Maven" não aparece no menu lateral e o protótipo abre na Listagem de processos; um botão de simulação (caixa tracejada) reproduz o acesso direto pelo endereço, que exibe "Acesso negado" (Fluxo 08, CA02–CA03).
17. "Processo a ser reindexado" é autocompletar: sugere a partir de 3 dígitos (até 6 processos, com o assunto); escolher a sugestão ou teclar Enter preenche o campo. A validação continua a das RN03/RN04 sobre o número do campo.
18. Ao registrar o pedido de "Reindexar Processo", o campo "Processo a ser reindexado" é limpo (e o aviso de origem na listagem some), deixando a tela pronta para o próximo processo; o processo pedido continua nos Resultados. Recusas e erros de validação mantêm o número no campo para correção.
19. "Reindexar Processo" usa a opção marcada em "Quais documentos reindexar?" no momento do clique. Resultados ganham a coluna "Documentos reindexados" com o modo aplicado ao item, e a mensagem do item registrado descreve o efeito: no modo ausentes, quantos documentos ausentes foram para a fila; no modo todos, a exclusão do processo do índice e a quantidade de documentos do sumário enfileirados (o PRD previa mensagem só em falha).
20. Acesso à funcionalidade somente pela ação "Forçar Indexação Maven" do menu lateral (RN01, D13); a Listagem de processos não tem ação de reindexação.
21. Dados, nomes de usuários, números de processo, ids e mensagens de erro técnicas (ORA-, HTTP) são fictícios.
