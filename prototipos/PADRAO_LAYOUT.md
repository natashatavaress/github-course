# Padrão de layout dos protótipos — eTCE Web

Todo protótipo funcional de requisito do eTCE Web segue este layout. Ponto de partida obrigatório:
[`_modelo/Main.dc.html`](./_modelo/Main.dc.html) (casca pronta + exemplo de filtros e lista) e
[`_modelo/canvas.json`](./_modelo/canvas.json). Referências já no padrão: `RF-028-pendencias`
(branch `claude/tce-web-functional-prototype-36w3z7`) e [`RF-032-indexacao-maven`](./RF-032-indexacao-maven/).

## Como criar um protótipo novo

1. Copiar `_modelo/` para `prototipos/RF-NNN-<nome-curto>/` e trocar os marcadores `[...]`.
2. Manter **sem alterar** o bloco `<style>` da casca, o cabeçalho, o menu lateral e a trilha.
   Acrescentar CSS próprio só no fim do `<style>`, em uma seção `/* ---------- RF-NNN ---------- */`.
3. Incluir no menu lateral o item da funcionalidade (rótulo + ícone de traço) e marcá-lo como ativo
   (`nav on`, `aria-current="page"`); item exibido só a quem tem a permissão do requisito.
4. Publicar como artefato Design (um artboard `Main.dc.html`, 1440×1000, `expand: "fill"`,
   `is_interactive: true`, `launch` focado) e registrar o link no `README.md` da pasta, com a
   lista de **decisões tomadas onde o PRD é ambíguo**.

## Casca (igual em todas as telas)

| Parte | Especificação |
|---|---|
| Cabeçalho | Branco, 82 px, borda inferior `#DDE1E4`. Da esquerda para a direita: botão hambúrguer (cinza `#DADDE0`, recolhe o menu), logotipo (olho + "TRIBUNAL DE CONTAS / DO ESTADO DE GOIÁS"), busca "Buscar processo..." (500 px, 50 px de altura), chip "Protótipo · dados simulados", sino vermelho com badge de pendências, "Usuário:" e "Órgão/Setor:" com seta, avatar circular cinza com as iniciais |
| Menu lateral | Branco, 250 px (58 px recolhido). Itens: Dashboard (azul), Listagem de processos (verde) com Com Anotações e Com Pendências (laranja, badge vermelho), Pauta (roxo, seta), Distribuir processos (vermelho, seta) e o item da funcionalidade. Ativo: fundo `#E8F1FA`, peso 500 |
| Trilha | Faixa branca de 50 px: ícone de início › níveis › página atual, fonte 16 px |
| Conteúdo | Fundo `#ECEFF1`, padding 24 px, cartões empilhados com 12 px de espaço |

## Cartões e componentes

- **Cartão** (`.card`): branco, raio 4 px, sombra leve. Título `.card-t` Poppins 400 22 px `#3D4448`;
  subtítulo `.phint` 14 px `#5E676D`. Ordem típica: cartão de título → cartão "Filtros"
  (recolhível pela seta) → cartão da lista/ação.
- **Campos** (`.field` + `.input`): rótulo acima, 15 px `#5E676D`; entrada de 42 px, borda `#A7AEB3`,
  raio 4 px. Filtros em grade de 3 colunas, "Limpar filtros" (contornado) alinhado à direita.
- **Botões**: primário `.btn` azul `#1E78BE`; secundário `.btn-o` contornado azul; link `.lnk`
  (ex.: "⟳ Atualizar", "✎ Alterar…"). Ações finais do cartão em grade de colunas iguais, largura
  total (`.btn-w`), com a ação principal (preenchida) à direita — ex.: Fechar · Negar · Autorizar.
- **Tabela** (`.tbl` + `.tr` + `.g-<nome>`): bordas `#A7AEB3` em todas as células, linhas de 64 px,
  cabeçalho 15 px com seta de ordenação (`.nf` remove a seta), células em caixa alta (`.nu` desliga),
  número do processo sublinhado (`.num`), faixa cinza à esquerda da coluna de processo
  (`.strip-gray`), seleção por checkbox na primeira coluna, rolagem horizontal na própria tabela e
  rodapé `.tfoot` com a contagem ("3 processos aguardando autorização").
- **Chips** (`.chip` + `.c-primary|c-success|c-warn|c-error|c-info|c-neutral`): raio 13 px, 12 px, 500.
- **Avisos** (`.alert` + `.a-error|a-warn|a-info|a-success`), **Snackbar** (`.toast` + `.t-*`)
  no canto inferior esquerdo, **carregamento** (`.skel`, `.spin`).

## Tokens

| Token | Valor |
|---|---|
| Fonte | Poppins 300–600 (Google Fonts) — substitui a Product Sans do sistema |
| Texto | `#3D4448`; secundário `#5E676D`; escuro `#2F3437` |
| Primária | `#1E78BE` (hover `#155A90`) |
| Fundo da página | `#ECEFF1` |
| Bordas | tabela/campos `#A7AEB3`; divisórias `#DDE1E4` |
| Alerta/badge | `#C62828` |
| Sucesso | `#13855E` |

## Regras gerais

- Dados sempre fictícios; o chip "Protótipo · dados simulados" fica visível.
- Simulações de perfil, cenário e falha vão em *tweaks* (`data-props`, seção "Simulação"),
  nunca em controles da tela. Atalhos de teste dentro da tela, quando úteis, ficam em caixa
  tracejada amarela identificada como simulação.
- Telas fora do escopo levam a uma página "fora do escopo" que preserva o estado da tela principal.
- Acessibilidade: botões reais, `aria-label` em botões só com ícone, `role="table"` nas tabelas.
