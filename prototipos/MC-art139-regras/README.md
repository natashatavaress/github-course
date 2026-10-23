# Protótipo funcional — Regras do Artigo 139 (SIMEX/AP)

Protótipo navegável, com dados simulados, da manutenção das regras do Art. 139 e da forma como o
Motor de Cálculo as aplica. Segue o layout da tela "Editar Regra do Artigo 139" do SIMEX/AP.

- Artefato publicado: https://claude.ai/artifact/2oBFBskmWyirSCZ4TVqKBG
- `Main.dc.html` — fonte do artboard (formato Design Component do canvas de design)
- `canvas.json` — índice do canvas
- Requisitos: [SIMEX1 — Motor de Cálculo](../../docs/requisitos/SIMEX1-motor-de-calculo.md) e
  [SIMEX1 — Tabelas de Parâmetros](../../docs/requisitos/SIMEX1-tabelas-de-parametros.md)

## Telas

| Tela | O que faz | Requisitos |
| --- | --- | --- |
| Lista de regras | Busca por código ou prefixo, filtro por situação, ordenação por prioridade, situação calculada (Ativa, Inativa, Vencida, Agendada), aviso de empate de prioridade com prefixos sobrepostos, log de auditoria | Base RF015, RN015, RN035, TL04 |
| Nova / Editar regra | Campos do layout: código, situação, NCM ("*" ou prefixos de 2 a 8 dígitos), MVA, prioridade, vigência e fundamento legal; validações e avisos de prioridade | Base RF015, RN015, RN031 · MC-RN16, MC-RN21 |
| Excluir | Confirmação com opção de inativar em vez de excluir; registra `SIMEX_REGRA_ART139_REMOVIDA` | Base RN035, FL04 (log) |
| Simular aplicação | Reproduz a fase 7 do motor para um item: portão de finalidade, precedência da ST, chave do painel, escolha por prioridade, empate e exigência de ALCMS/ZF (Situação A) | MC-FL04, MC-RN02, MC-RN15–MC-RN19, MC-RN24 |

## Dados de exemplo

As regras padrão ART139-A, ART139-B, ART139-C e ART139-E vêm do documento do Motor de Cálculo
(MC-RN21). A ART139-VESTUARIO reproduz a tela de referência. Data de análise padrão: 23/10/2026.

## Decisões tomadas onde os requisitos são ambíguos

1. Código não pode ser alterado na edição (campo bloqueado, como no layout); é único e aceita letras, números, "-" e "_".
2. Prefixo de NCM com 2 a 8 dígitos, como indica o layout; pontos digitados são removidos.
3. MVA exibida com 4 casas decimais e vírgula; precisa ser maior que zero.
4. Situação "Ativa/Inativa" corresponde ao campo `ativo` da tabela; "Vencida" e "Agendada" são só exibição, calculadas pela vigência.
5. Empate de prioridade e regra específica com prioridade maior ou igual à da regra geral geram aviso, sem bloquear o salvamento.
6. O simulador mostra a MVA que seria usada, mas não calcula o valor da antecipação, porque a fórmula está em aberto (MC seção 9).
7. A regra ST é simulada por uma caixa de seleção; o protótipo não lê a tabela ICMS-ST.
8. Fora do protótipo: persistência real, perfis de acesso e importação de JSON (Base RF022). Dados são fictícios.
