# Protótipo funcional — RF-028 Processos com Pendências (eTCE Web)

Protótipo navegável com dados simulados do fluxo principal do RF-028: Painel de Pendências
(Tela 01), lista filtrada por pendência (Tela 02) e telas de trabalho (autuação, aceite,
juntada, autorização de prazo e avocação).

- Artefato publicado: https://claude.ai/artifact/KUDM1VHPeChCHSJVm2DzfV
- `Main.dc.html` — fonte do artboard (formato Design Component do canvas de design)
- `canvas.json` — índice do canvas

Tweaks disponíveis no artefato: perfil (chefe, analista, gabinete), cenário (padrão, sem
pendências, volume 99+) e simulação de falha.

## Decisões tomadas onde o PRD é ambíguo

1. Fonte Figtree no lugar de Product Sans (indisponível na web).
2. Telas de trabalho como páginas internas, preservando o estado ao voltar (RN23).
3. Autuação: coluna "Sel." (prosseguir) separada de "Marc." (envio/assinatura) — RN27 × RN29.
4. Marcação: todos marcam Assinadas; só o chefe marca Sem assinatura.
5. P01 conta Enviadas + Assinadas + Sem assinatura (esta só para o chefe, RN21).
6. P09 conta apenas a fila inicial do perfil (E+N; E+S no gabinete), e não todas as situações da RN42.
7. P10 só entra no badge para o chefe; P11 conta vencidos e a vencer (≥ 20 dias no setor).
8. Juntada: salvar a decisão já muda a situação para Autorizada/Rejeitada; o envio do termo não altera a fila.
9. Avocação: gabinete vê processos de outros gabinetes (Avocar); demais perfis veem "Prazos a vencer/vencidos" do próprio setor (Redistribuir) — RN67 × RN69.
10. "Processo com menos de 10 dias" = vence em menos de 10 dias (20–30 dias no setor, RN68).
11. Claims simulados: chefe (chefia, distribuir); gabinete (avocar, autorizar juntada); analista (nenhum).
12. Aceite com ações por linha, sem marcação em lote (RN41 não representada).
13. Fora do protótipo: Tela 11, "Nova Solicitação" (RF-025/RF-024) e exclusão de prorrogação (Fluxo 09). Dados são fictícios.
