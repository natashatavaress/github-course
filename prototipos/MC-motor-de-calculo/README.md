# Protótipo funcional — Motor de Cálculo (SIMEX/AP)

Protótipo navegável, com dados simulados, do cálculo do ICMS por item da DUIMP descrito em
[SIMEX1 — Motor de Cálculo](../../docs/requisitos/SIMEX1-motor-de-calculo.md). Usa o layout do
SIMEX/AP (cabeçalho, menu lateral, rodapé do menu, fonte, títulos e cores) da tela "Editar Regra do
Artigo 139", que serviu apenas de referência visual.

- Artefato publicado: https://claude.ai/artifact/4dD7VZMnoEDZWbubbM88x6
- `Main.dc.html` — fonte do artboard (formato Design Component do canvas de design)
- `canvas.json` — índice do canvas

## Telas

| Tela | O que faz | Requisitos |
| --- | --- | --- |
| Cálculo do ICMS da DUIMP | Dados da DUIMP, totais (ICMS, antecipação, FCP, total, diferido), alertas do cálculo e tabela de itens com código CAL e valores; aviso e botão "Recalcular DUIMP" quando há regime alterado | MC-RF14, MC-RF15, MC-FL06 |
| Cálculo do item | Dados do item (MC-TL01); regime especial com candidatos, RTI001/RTI002 e motivo de cada regime do CNPJ, seleção e "Recalcular" (MC-TL02); resultado (MC-TL03); memorial fase a fase com status, valores e referências (MC-TL04); alertas | MC-RF01 a MC-RF13, MC-FL01 a MC-FL05 |

O motor do protótipo executa as fases 1 a 8 da seção 1.3 do documento, com os filtros de candidato
(Base RN002), Corredor, ALCMS/ZF (art. 142 e crédito presumido), efeitos de regime, busca ST,
busca Art. 139 por prioridade, Situação A, FCP e código CAL.

## Alternativas

O canvas tem duas propostas para a mesma funcionalidade, com os mesmos dados e o mesmo motor.

| | Alternativa A (`Main.dc.html`) | Alternativa B (`Alternativa-B.dc.html`) |
| --- | --- | --- |
| Navegação | Duas telas: DUIMP e detalhe do item | Uma tela: lista de itens à esquerda e item à direita |
| Memorial | Lista das fases 1 a 8 com texto | Trilha visual das fases; a fase escolhida mostra o detalhe |
| Regime especial | Seleção + "Recalcular" (item fica pendente) | Tabela comparando cada candidato (código, ICMS, antecipação, total e diferença) e "Aplicar regime ao item" |
| Resultado | Tabela de valores | Composição passo a passo, de b0 até o total |
| Regimes não candidatos | Sempre visíveis, com motivo | Recolhidos, com motivo ao expandir |
| Melhor para | Revisar a DUIMP inteira e conferir item a item | Decidir o regime de cada item comparando o efeito antes de aplicar |

## Itens de exemplo

| Item | Caso demonstrado | Código |
| --- | --- | --- |
| 1 | Revenda sem ALCMS com regra ST (autopeças, MVA 71,78%); candidatos de crédito presumido e redução do imposto | CAL002 |
| 2 | ALCMS 17% (cosméticos), Art. 139 ART139-C | CAL003 |
| 3 | ALCMS 12% com crédito presumido de 8%, Art. 139 regra geral; Corredor não é candidato (modalidade) | CAL003 |
| 4 | Corredor de Importação 4%: ICMS diferido, prazo de 60 dias e alerta da MAL-SIMEX-008 | CAL008 |
| 5 | Redução do imposto 40%; Art. 139 sem ALCMS gera alerta da Situação A | CAL001 |
| 6 | Ativo imobilizado, sem candidatos (RTI002) | CAL006 |
| 7 | Industrialização sem antecipação; candidato de diferimento disponível para escolha | CAL001 |

## Premissas para pontos em aberto (MC seção 9)

1. Antecipação = base do ICMS × (1 + MVA) × alíquota do item − ICMS bruto, nunca negativa. Fórmula provisória, indicada na tela.
2. Itens ALCMS/ZF: as fases 4 a 6 não são executadas; a fase 7 (ST/Art. 139) e o FCP são executados, para que CAL004 e o Art. 139 façam sentido.
3. Alíquota do Corredor = `percentual` do Ato; prazo = `prazoRecolhimentoDias` do Ato ou 60 dias, contados do registro da DUIMP.
4. Redução de base aplicada sobre b0.
5. Arredondamento a 2 casas no fim de cada cálculo.
6. Alterar o regime não recalcula sozinho: o item fica marcado e o analista usa "Recalcular" (MC-TL02).
7. Dados de DUIMP, regimes e itens são fictícios; ST e Art. 139 usam as regras de exemplo do documento.
