# GRANTOP – Sistema de Calibração (Estação Total)

Este kit cria um **sistema em Google Sheets + Apps Script** para registrar leituras (EDM, ângulos HZ/V), calcular parâmetros de calibração (d₀ e k do EDM; descolimação C e índice vertical i) e **gerar o relatório automaticamente** (Google Docs com link de PDF).

## Como usar

1. Crie uma planilha no Google Sheets (vazia).
2. Abra **Extensões → Apps Script** e crie um projeto.
3. Crie um arquivo `code.gs` e cole o conteúdo deste repositório.
4. Crie um arquivo HTML chamado `index` e cole o conteúdo de `index.html`.
5. Salve. Volte à planilha e recarregue.
6. Use o menu **Calibração → 1) Preparar estrutura** para criar as abas.
7. Use **Calibração → 2) Abrir painel (Sidebar)** para abrir a interface.
8. Cadastre a **Nova calibração**, depois lance **Leituras EDM** e **Ângulos**.
9. Em **Processar e Relatar**, informe o `calibId` e clique em **Calcular resultados**.
10. Em seguida, clique em **Gerar relatório** para criar o **Google Docs** (com link de **PDF**).

> OBS:
> - O cálculo de EDM é feito por **regressão linear** do erro (mm) vs. distância nominal (m), produzindo `d0_mm` (intercepto) e `k_ppm` (slope × 1000).
> - Os modelos de ângulos adotam relações usuais de leituras diretas/reversas em graus e resultados em arcsegundos.
> - Ajuste os critérios, arredondamentos e incertezas conforme seu procedimento interno.
> - Se quiser usar um **template** pré-existente do Google Docs, informe o `Doc Template ID` na aba **Config** e adapte a função `generateReport`.

## Campos principais

- **Calibracoes**: `calibId, data, cliente, cnpj, instrumento, fabricante, modelo, ns, res_ang_arcsec, obs`
- **EDM_Dados**: `calibId, ponto, dist_nom_m, dist_lida_m, face, rep, temp_C, UR_%, press_hPa, obs, erro_mm, usar?`
- **Angulos_HZ**: `calibId, conjunto, alvo, ang_nom_deg, F1_deg, F2_deg, obs, erro_arcsec, C_arcsec, usar?`
- **Angulos_V**: `calibId, conjunto, alvo, ang_nom_deg, F1_deg, F2_deg, obs, erro_arcsec, i_arcsec, usar?`
- **Resultados**: `d0_mm, k_ppm, U_d0_mm, U_k_ppm, C_arcsec, i_arcsec, ...`
- **Relatorio**: links gerados e status

## Personalização

- Ajuste as fórmulas de C e i conforme o padrão do seu laboratório (graus, gons, etc.).
- Inclua correções ambientais do EDM se aplicável (p.ex., temperatura/pressão/umidade).
- Expanda a geração do **Docs** para incluir seu **brasão/logo**, assinaturas e anexos.

---

**Suporte rápido:** Cole sua dúvida/erro e o conteúdo da aba **Resultados** aqui que eu te ajudo a ajustar.
