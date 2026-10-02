# Padrão visual dos protótipos — eTCE Web

Fonte de verdade de layout para **todo protótipo** deste projeto. Todo protótipo novo segue este
padrão, salvo pedido explícito em contrário.

- **Referências visuais:** [`_referencias/layout-listagem-processos.png`](_referencias/layout-listagem-processos.png),
  [`_referencias/layout-gerenciar-assinatura.png`](_referencias/layout-gerenciar-assinatura.png) e
  [`_referencias/layout-menu-com-anotacoes.png`](_referencias/layout-menu-com-anotacoes.png) (menu lateral).
- **Implementação de referência:** [`RF-028-pendencias/Main.dc.html`](RF-028-pendencias/Main.dc.html).
  O bloco `<helmet><style>` desse arquivo é a folha de estilos canônica. Copie-o inteiro para o
  protótipo novo, junto com a casca (cabeçalho, menu lateral e trilha), e ajuste apenas o conteúdo
  da área `<main>`.

## 1. Casca da aplicação

| Região | Regra |
|---|---|
| Cabeçalho | Branco, 82 px de altura, borda inferior `#DDE1E4`. Da esquerda para a direita: botão hambúrguer (quadrado cinza `#DADDE0`, 40 px, recolhe o menu), marca "TRIBUNAL DE CONTAS / DO ESTADO DE GOIÁS", campo "Buscar processo..." (500 px, 50 px de altura, lupa à direita), espaço livre, sino de **pendências** (azul `#1E78BE` sem pendência, vermelho `#C62828` com pendência, badge vermelho com a contagem até `99+`; leva à página **Com Pendências**, com o submenu correspondente selecionado), bloco **Usuário:** / **Órgão/Setor:** (rótulo em negrito, valor truncado com reticências, seta ▾) e avatar circular de 50 px. |
| Menu lateral | Branco, 250 px expandido ou 58 px recolhido (só ícones). Itens de 48 px com ícone colorido + rótulo cinza `#5A6268` 14 px. Ordem: **Dashboard**; **Listagem de processos**, com os subitens fixos **Com Anotações** (RF-027) e **Com Pendências** (RF-028), recuados, com ícone laranja `#F2A33A` e badge vermelho de contagem à direita; **Pauta** e **Distribuir processos**, grupos que começam recolhidos, com chevron ⌄ à direita. Item ativo: fundo `#E8F1FA`, raio 4 px, rótulo em peso 500 (pode quebrar em duas linhas). Cores dos ícones: Dashboard azul `#1E78BE`, Listagem verde `#13855E`, Pauta roxo `#8E44AD`, Distribuir vermelho `#E74C3C`. Avatar do cabeçalho: círculo cinza `#E3E6E8` com as iniciais. |
| Trilha (breadcrumb) | Faixa branca de 50 px sob o cabeçalho. Ícone de casa e itens separados por `›`, 16 px, cor `#3D4448`. O último item não é clicável. |
| Área de conteúdo | Fundo `#ECEFF1`, padding de 24 px, cartões empilhados com 12 px de espaço entre si. |

## 2. Cartões (seções)

- Branco, raio de 4 px, sombra `0 1px 3px rgba(30,40,50,.16)`.
- Cabeçalho do cartão: título 22 px, peso 400, `#3D4448`, e chevron ^ à direita para recolher.
- Subtítulo de seção (ex.: "Processos" dentro de um cartão): 15 px, peso 600, `#6B7378`.
- Cartão **Filtros**: título "Filtros", divisor vertical e o indicador de filtro aplicado (funil laranja `#F57C00`). Ações de filtro ficam no corpo do cartão; pendências não ficam aqui, e sim no sino do cabeçalho. Começa recolhido.
- Telas de trabalho: um cartão "Filtros" e, abaixo, um cartão com o título da tela, contendo a tabela e as ações.

### 2.1 Página de seleção em dois níveis: tipo → item (ex.: Com Pendências, Com Anotações)

- Cartão de topo com título, subtítulo de contexto à esquerda e, à direita, o horário da última atualização mais o link de ação "Atualizar".
- **1º nível, tipos:** uma linha de botões de tipo em grade `repeat(auto-fit, minmax(180px, 1fr))`. Cada botão tem 56 px de altura, borda `#D5DADE`, raio 4 px, rótulo de 15 px (peso 500) à esquerda e pílula com o total do tipo à direita. O tipo selecionado fica com fundo azul `#1E78BE`, texto branco e pílula branca. A pílula fica vermelha `#C62828` quando o tipo contém prazo vencido.
- **2º nível, itens:** os itens só aparecem **depois de clicar num tipo**, numa faixa cinza-clara `#F6F8F9` logo abaixo, como chips arredondados de 40 px com rótulo curto e contagem (o rótulo completo fica no `title`). O item selecionado fica com borda azul, fundo `#EEF5FB` e contagem azul. Itens com zero ficam esmaecidos.
- **Orientação:** sem tipo selecionado, a página mostra "Selecione um tipo de pendência para ver os itens."; com tipo e sem item, mostra "Selecione uma pendência para exibir os processos.". O conteúdo do item (tabela ou tela de trabalho) aparece abaixo, em cartões próprios.
- **Responsividade:** os tipos quebram de linha sozinhos (um por linha no celular) e os chips fluem com `flex-wrap`, sem rolagem horizontal.
- O sino do cabeçalho e o submenu levam à mesma página. Na sessão, ela preserva o último tipo e item escolhidos. Clicar em "Com Pendências" na trilha limpa a seleção.

## 3. Tabela

- Grade com bordas em todas as células: 1 px `#A7AEB3`, contorno externo e divisórias verticais.
- Linhas com no mínimo 64 px e padding de 12 × 16 px.
- Cabeçalho: texto 15 px, peso 400, com ícone de funil à direita em colunas filtráveis (classe `nf` remove o funil).
- Primeira coluna: checkbox de seleção. O cabeçalho dessa coluna seleciona todos os itens da página.
- Coluna do processo: número sublinhado (aparência de link), com faixa de status de 6 px à esquerda da célula (quando a tabela tem uma coluna de **Situação** antes do processo, como no aceite e na avocação, a faixa fica na célula da Situação): cinza `#8E979C` no normal, vermelha `#C62828` quando há alerta (sigiloso, bloqueado, vencido, devolvido, rejeitado). Ícones de cadeado (sigilo) e estrela (favorito) ao lado do número.
- Linha em alerta: fundo rosado `#FDECEC`. Linha selecionada: `#EEF5FB`. Linha apensada: `#F6F8F9` com `↳`.
- Valores das células em **CAIXA ALTA**. Botões, chips e números de processo ficam fora dessa regra.
- Acima da tabela: barra de ações com botões quadrados de 40 px e ícone branco, e, à direita, o link verde "Exportar para excel". As ações que atuam sobre processos ficam **desabilitadas** (cinza `#BFC4C8`) até haver processo selecionado e, com seleção, ficam **habilitadas** em verde `#13855E` (hover `#0E6B4B`); exceção: o ícone Assinar da pendência "Aguardando assinatura" fica laranja `#C2570C` (hover `#9A4509`) quando habilitado; ações gerais, como "Atualizar lista", ficam sempre habilitadas. Ao clicar, a ação leva o usuário à funcionalidade dona (ex.: Assinar → RF-014) com os processos selecionados. Listas de pendência exibem só as ações pertinentes (ex.: "Aguardando assinatura" mostra só Assinar).
- Rodapé da tabela: botão azul "Início da tabela" (ícone de casa), "Linhas por página" com seletor, setas ‹ › e o intervalo "1-10 de N". Somente a **tabela de listagem de processos** (RF-010) tem também o botão verde "Configurar tabela" (engrenagem), entre "Início da tabela" e "Linhas por página"; as demais tabelas não o exibem. Tabelas de trabalho sem paginação mostram só a contagem no rodapé.

## 4. Botões e ações

| Tipo | Uso | Estilo |
|---|---|---|
| Primário | Ação principal | Fundo `#1E78BE`, texto branco, 40 px, raio 4 px, peso 500 |
| Contorno | Ação secundária ou cancelar | Fundo branco, borda e texto `#1E78BE` |
| Desabilitado | — | Fundo `#C2C7CB`, texto branco |
| Sucesso | "Configurar tabela" (só na listagem de processos) | Fundo `#13855E` |
| Perigo | Devolver, negar, excluir | Fundo `#C62828` |
| Link de ação | Ações auxiliares no alto do cartão (ex.: "Central de assinatura", "Remover assinatura") | Texto 14 px peso 500 com ícone; azul `#1E78BE` ou vermelho `#C62828` |

- Ações finais de formulário ou de tela ficam no rodapé do cartão em **grade de colunas de largura igual**, cada botão ocupando a coluna toda: contorno à esquerda (Cancelar ou Fechar) e primário à direita.
- Diálogos seguem o mesmo padrão de rodapé.

## 5. Formulários

- Rótulo acima do campo, 15 px, `#5E676D`.
- Campo com 42 px de altura, borda `#A7AEB3`, raio 4 px, texto `#3D4448`.
- Checkbox de 20 px com `accent-color #3D4448`. O rótulo fica ao lado, em cinza.
- Notação de campos conforme `CONTEXT.md` §6.1 (`TextField`, `Select`, `Checkbox`, `DatePicker` do MUI).

## 6. Tokens

| Token | Valor | Uso |
|---|---|---|
| Fonte | Poppins 300/400/500/600 (Google Fonts) | Substituta web da Product Sans |
| Texto | `#3D4448` | Texto principal |
| Texto secundário | `#5E676D` / `#6B7378` | Rótulos, subtítulos |
| Fundo da página | `#ECEFF1` | Área de conteúdo |
| Superfície | `#FFFFFF` | Cabeçalho, menu, trilha, cartões |
| Linha de tabela | `#A7AEB3` | Bordas da grade e dos campos |
| Primária | `#1E78BE` (hover `#155A90`) | Botões, links, foco |
| Sucesso | `#13855E` | Excel, configurar tabela, situação positiva |
| Erro/alerta | `#C62828`, fundo `#FDECEC` | Faixa, linha em alerta, badge |
| Atenção | `#F57C00` | Funil de filtro aplicado |

As cores das imagens de referência foram escurecidas levemente (azul, verde) para garantir contraste
de 4,5:1 com texto branco.

## 7. Estados obrigatórios

Toda tabela ou lista implementa os estados de **carregando** (skeleton nas linhas), **vazio**
(mensagem centralizada e ação para limpar o filtro), **erro** (`Alert` com o motivo) e **sucesso**
(toast escuro no canto inferior esquerdo), conforme `CONTEXT.md` §6.

## 8. Convenções do protótipo

- Dados sempre simulados e identificados pelo chip "Protótipo · dados simulados" no cabeçalho.
- Itens de menu fora do escopo do requisito não navegam: mostram um aviso de que não fazem parte do protótipo.
- Tweaks de simulação (perfil, cenário, falha) ficam no painel de Tweaks do artefato, nunca na tela.
- Cada protótipo fica em `prototipos/RF-NNN-<nome>/`, com `Main.dc.html`, `canvas.json` e `README.md`. O README traz o link do artefato e as decisões tomadas sobre ambiguidades do PRD.
