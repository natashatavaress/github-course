# Protótipo funcional — RF-028 Processos com Pendências (eTCE Web)

Protótipo navegável com dados simulados do fluxo principal do RF-028: Painel de Pendências
(Tela 01), lista filtrada por pendência (Tela 02) e telas de trabalho (autuação, aceite,
juntada, autorização de prazo e avocação).

Baseado no **PRD v1.9** do RF-028. Ajustes da v1.5 a v1.9 aplicados, nos pontos em que o PRD prevalece sobre o protótipo (seção 6):

- P01 conta as solicitações em `S` e, para o chefe de setor, também em `A`; `E` não conta (`RN22`, CA110–CA112).
- Marcação da fila de autuação por perfil e situação, sem "selecionar todas" (`RN27`). `C`, `X` e `R` não são marcáveis; `A` só para o chefe ou o criador da solicitação. Exceção mantida: `E` continua marcável, porque "Prosseguir com Autuação" exige `E` (`RN29`) — contradição a resolver no PRD.
- "Habilitar sigilo" desabilitado quando o andamento é de outro setor e o usuário não tem a permissão de sigilo (`RN33`).
- P11 conta toda a base da avocação (`RN69`).
- Gravar a decisão de juntada não altera a situação; a linha recebe o chip "Decisão salva" (`RN53`, `RN54`).
- Tela 12 (v1.9) virou o cadastro completo da solicitação de autuação (`RN89`–`RN102`):
  - linha de identificação (nº, situação, criador e sigla do setor) e mensagem por situação;
  - Título/Resumo com "N caracteres restantes" e Histórico obrigatórios;
  - grade de arquivos com assinatura (Novo, Será excluído, Na Central), descrição, nome, data, tipo, nº, ano, origem e "Visualizar";
  - "Adicionar arquivos" (seletor real, validações da RN91), "Incluir arquivos de exemplo" e "Remover arquivo";
  - "Informações do arquivo" com "Aplicar ao arquivo"; com mais de um arquivo marcado, vira edição em massa (RN93);
  - "Salvar" confirma inclusões, exclusões e atualizações e mantém o diálogo aberto em modo de edição (RN96);
  - botões por situação (RN101): N → Salvar; A → Excluir, Enviar à Central/Cancelar envio, Salvar; S → Excluir, Salvar, Enviar Solicitação; E (Protocolo) → Rejeitar, Prosseguir com Autuação; R → Motivo da rejeição, Excluir. Fechar e Nova sempre aparecem; fechar com alterações pede confirmação.
- O envio à Central de Assinatura aceita só o criador da solicitação ou o chefe de setor e envia apenas os PDFs marcados; a permissão "assinar" (questão 03) não foi simulada.
- A passagem de `A` para `S` acontece no Portal de Assinatura; no protótipo, o botão "Simular assinatura concluída no Portal" faz essa transição.

- Artefato publicado: https://claude.ai/artifact/KUDM1VHPeChCHSJVm2DzfV
- `Main.dc.html` — fonte do artboard (formato Design Component do canvas de design)
- `canvas.json` — índice do canvas

Layout conforme o padrão visual do projeto ([`../PADRAO_VISUAL.md`](../PADRAO_VISUAL.md)); este arquivo é a implementação de referência desse padrão.

Tweaks disponíveis no artefato: perfil (chefe, analista, gabinete, Protocolo/Setor 41), cenário (padrão, sem
pendências, volume 99+) e simulação de falha.

## Cobertura das telas do PRD

| Tela do PRD | Onde está no protótipo |
|---|---|
| 01 — Painel de Pendências | Página **Com Pendências** (sino do cabeçalho ou submenu): seleção de tipo e de item, com contagens, horário da última atualização e "Atualizar" |
| 02 — Lista filtrada por pendência | Itens P02–P07 e P12: tabela de processos filtrada, com apensados. Em "Aguardando assinatura" (P02), a única ação acima da tabela é "Assinar", habilitada ao selecionar processos, que redireciona para Gerenciar assinatura (RF-014) com os selecionados. Em "Pendentes de envio" (P03), "Assinados por mim" (P04) e "Assinados por outros" (P05), a única ação é "Enviar", que redireciona para Enviar processo (RF-012). Em "Enviados para Revisão Oficial" (P06), as ações são "Tramitar" (verde-claro, RF-013) e "Assinar" (laranja, RF-014). "Enviado para Assinatura (REVISADO)" (P07) não tem ações acima da tabela. Em "Revisado" (P12), a única ação é "Assinar" (laranja, RF-014). Na listagem, Tramitar, Assinar e Enviar fazem os mesmos redirecionamentos |
| 03 — Solicitações de Autuação Pendentes | Item "Autuação" (P01), com filtros iniciais da RN25, "Filtros Exclusivos do Protocolo" só para o Setor 41 (RN78), marcação "Todas p/ Envio · Todas p/ Assinatura" e ação de linha por origem (RN79) |
| 04 — Autuação de Processo Eletrônico | Diálogo aberto por "Prosseguir com Autuação" |
| 05 — Aguardando Aceite de Processos | Item "Aguardando aceite" (P08): "Aceite eletrônico — Recebimento de Processos", com as colunas do PRD, marcação em cascata dos apensados (RN41), "Aceitar TODOS", "Devolver Selecionados" e "Fechar" (RN81) |
| 06 — Juntada de Documentos: solicitações | Item "Juntada" (P09) |
| 07 — Decisão de Juntada | Diálogo aberto por "Decidir juntada", "Ver decisão" ou "Consultar": documentos a juntar com visualizador ao lado (RN80), descrição da solicitação em somente leitura, decisão, "Ver Termo de deferimento" e "Consultar Processo" |
| 08 — Autorizar Prorrogação/Suspensão | Item "Prorrogação/Suspensão" (P10), só para o chefe de setor, com ação de linha "Abrir" e filtro de analista com pesquisa |
| 09 — Prorrogar / Suspender | Diálogo "Prorrogar/Suspender", aberto pela ação de linha ou por "Alterar Prorrogação/Suspensão concedida": dias úteis e justificativa obrigatórios (contador de restantes) e "Excluir" por lançamento (RN61) |
| 10 — Avocação de Processo | Item "A serem avocados" (P11): campos com pesquisa, colunas do PRD, título "Processos (N)", ação de linha "Abrir" e "Redistribuir Selecionados" que redireciona para Distribuição Manual (RF-022) com os selecionados (RN83) |
| 11 — Visualização de arquivos da solicitação | Diálogo aberto pela ação de linha "Visualizar arquivos" (origens SEI, Atos de Pessoal, LRF e Tomada de Contas), com "Visualizar" e "Rejeitar Solicitação" (só Atos de Pessoal e LRF, RN76) |
| 12 — Solicitação de Autuação | Diálogo aberto por "Abrir solicitação" ou "Nova Solicitação": cadastro completo (RN89–RN102) com identificação, título com contador, histórico, grade de arquivos com metadados, edição em massa, Central de Assinatura, envio ao Protocolo, exclusão e rejeição |

## Decisões tomadas onde o PRD é ambíguo

1. Fonte Poppins no lugar de Product Sans (indisponível na web).
2. Telas de trabalho como páginas internas, preservando o estado ao voltar (RN23).
3. Autuação: uma única coluna de seleção serve a todos os botões ("Prosseguir com Autuação", "Enviar Solicitações Selecionadas" e "Enviar para a Central de Assinatura"); cada botão valida a situação das solicitações selecionadas (RN27, RN29) e informa as que não se aplicam. O radio "Todas p/ Envio · Todas p/ Assinatura" preenche essa mesma seleção (RN28).
4. Marcação: escolher "Todas p/ Envio" ou "Todas p/ Assinatura" já aplica a marcação, sem botão extra; nenhuma opção vem marcada (o PRD não levantou o padrão). Todos marcam Assinadas; só o chefe marca Sem assinatura.
5. P01 conta Enviadas + Assinadas + Sem assinatura (esta só para o chefe, RN21).
6. P09 conta apenas a fila inicial do perfil (E+N; E+S no gabinete), e não todas as situações da RN42.
7. Badge (RN01, v1.3): soma de todas as pendências visíveis, inclusive Revisado (P12) e, para o chefe, Prorrogação/Suspensão (P10). P11 conta vencidos e a vencer (≥ 20 dias no setor). P06 conta só os processos do usuário (RN84).
8. Juntada: salvar a decisão não muda a situação (chip "Decisão salva", v1.5); o envio do termo não altera a fila. A justificativa/motivo ficou opcional e sem limite, pois o PRD v1.3 deixou isso em aberto (questão 16).
9. Avocação: o gabinete de conselheiro vê os processos do seu relator em outros gabinetes, com o Relator já preenchido (Avocar); os demais perfis veem "Prazos a vencer/vencido" do próprio setor (Redistribuir) — RN67 × RN69, RN77.
10. "Processo com menos de 10 dias" = vence em menos de 10 dias (20–30 dias no setor, RN68).
11. Claims simulados: chefe (chefia, distribuir); gabinete (avocar, autorizar juntada); analista (nenhum).
12. Aceite: "Aceitar TODOS" age sobre os processos marcados; sem marcação, sobre toda a lista. Fica desabilitado enquanto houver processo com documento de Atos de Pessoal sem setor de integração (RN81).
13. Fora do protótipo: a permissão "assinar" da Central (questão 03), a assinatura real no Portal, o visualizador real (RF-024), o download de anexos do TCE-HUB/SolarBPM (RN35), os modos de lançamento do analista (RN60, RN82 — questão 19) e o modelo de termo vazio (RN75). Dados são fictícios.
15. Protocolo (RN78): a "Fila de origem" mostra as solicitações criadas pelo próprio Setor 41; "Integrador SEI" limpa o campo de setor e filtra a origem SEI. Nova solicitação entra com situação "Sem assinatura".
14. O ponto de entrada não é um botão na barra de filtros de RF-010, como diz o PRD (seção 2 e Tela 01). Por decisão do negócio, o **sino do cabeçalho** e o submenu "Com Pendências" levam à página **Com Pendências**, que substitui o painel suspenso. As 12 pendências ficam em seleção de dois níveis: primeiro o tipo, entre quatro (Solicitações, Tramitação e prazo, Assinaturas, Revisão), com o total de cada um; depois de clicar no tipo, os itens dele aparecem como chips com contagem. O item selecionado mostra a lista filtrada (P02–P07, P12) ou a tela de trabalho (P01, P08–P11) na própria página. É preciso ajustar o PRD (Tela 01, Fluxo 01) e verificar a convivência com o indicador de anotações (RF-027).
