# Protótipo funcional — RF-032 Forçar Indexação Maven (eTCE Web)

Protótipo navegável com dados simulados do fluxo principal do RF-032 (Fluxo 01 — Reindexar
processo) e das demais áreas da Tela 01: Lotes, Resultados e Acompanhamento.

- Artefato publicado: https://claude.ai/artifact/MySLubB3dNxaqUfx1pQ2ef
- `Main.dc.html` — fonte do artboard (formato Design Component do canvas de design)
- `canvas.json` — índice do canvas

Tweaks disponíveis no artefato: perfil (com a função · SERV-SISTEMAS, com a função · outro
setor, sem a função), falha do Maven Docs (nenhuma, falha em um item, HTTP 503, tempo
esgotado), falha ao registrar o pedido, lotes vazios e lote em execução por outro usuário.

Entrada pela listagem: em "Listagem de processos" (menu lateral), selecionar processos habilita a
ação "Forçar indexação Maven" (vermelha, na barra de ações), que abre a tela com os processos
selecionados; ali é possível removê-los ou incluir outros pelo campo com autocompletar. Pelo menu
lateral, a tela abre sem processos: é preciso buscá-los para incluí-los.

Processos simulados (botões abaixo do campo): 202600047000118 (erro e não processados),
202500047001842 (todos publicados), 202600047000233 (pendente em retomada — RN18),
202500047002010 (retomada esgotada), 202600047000301 (falha no modo ausentes),
202600047000412 (sem documentos no sumário) e 20260004700011 (trecho de número — CA10).

## Decisões tomadas onde o PRD é ambíguo

1. Layout padrão do eTCE Web ([`../PADRAO_LAYOUT.md`](../PADRAO_LAYOUT.md)), com fonte Poppins no lugar de Product Sans (indisponível na web).
2. Menu (dúvida 03): "Forçar Indexação Maven" como item de primeiro nível do menu lateral, depois de "Distribuir processos"; rota `/forcar-indexacao-maven`.
3. Layout (dúvida 12): cartões empilhados — título, "Reindexar processo", "Lotes", "Resultados" e "Acompanhamento da indexação". "Consultar situação" fica junto de "Reindexar Processo", pois usa o mesmo campo.
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
16. Usuário sem a função: o item não aparece no menu e a tela exibe "Acesso negado" (simulando acesso direto pelo endereço).
17. Listagem: a ação "Forçar indexação Maven" é um botão de ícone vermelho (`#C62828`, o vermelho de alerta do padrão) ao fim da barra de ações, com dica de texto; fica desabilitada sem seleção e só aparece para quem tem a função `funReindexarProcessoMaven` (RN01). As demais ações da barra são ilustrativas (fora do escopo).
18. Ao acionar a ação, a lista da tela é substituída pelos processos selecionados, e a seleção da listagem é limpa. A trilha mostra "Listagem de processos" como nível anterior.
19. "Processo a ser reindexado" vira autocompletar: sugere a partir de 3 dígitos (até 6 processos, com o assunto); escolher uma sugestão ou teclar Enter inclui o processo na lista e limpa o campo. Número digitado e não incluído não entra no pedido: "Reindexar Processo" pede que seja incluído antes; número inexistente recebe "Processo inválido ou não existe!".
20. "Reindexar Processo" pede a reindexação de todos os processos da lista, uma execução com um item por processo (o PRD prevê um processo por vez; a lista é extensão desta demanda). A falha de um processo não interrompe os demais.
21. Modo "Todos os documentos" com processo da lista em retomada (RN18): o pedido inteiro é recusado, com a mensagem indicando o processo a remover; nada é registrado.
22. "Consultar situação" usa o número digitado ou, com o campo vazio, o primeiro processo da lista; cada processo da lista também tem um botão de consulta próprio. Processo consultado que não está na lista pode ser incluído pelo botão "Incluir na reindexação" do acompanhamento.
23. Entrada pelo menu lateral: a lista começa vazia (com orientação para buscar o processo); a lista vinda da listagem também é descartada ao reabrir a tela pelo menu. Os processos simulados abaixo do campo apenas preenchem a busca.
24. Os botões de remover ficam desabilitados durante a execução.
25. Dados, nomes de usuários, números de processo, ids e mensagens de erro técnicas (ORA-, HTTP) são fictícios.
