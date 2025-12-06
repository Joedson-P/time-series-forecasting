# Análise e Previsão de Séries Temporais (ARIMA & GARCH)

## Objetivo do Projeto

O objetivo principal deste projeto foi aplicar modelos estatísticos clássicos de **Séries Temporais** para analisar e tentar prever o preço de fechamento (`Close Price`) das ações de uma grande empresa de tecnologia, assim como modelar sua volatilidade (risco).

## Metodologia e Pipeline

O projeto seguiu uma metodologia rigorosa para Séries Temporais Financeiras:

1.  **Pré-processamento e Estacionariedade:**
    * A série original foi diagnosticada como **Não-Estacionária** devido à forte tendência (confirmado pelo Teste ADF: $P > 0.05$).
    * Foi aplicada a **Diferenciação de 1ª Ordem** ($d=1$) para tornar a série estacionária (Teste ADF: $P \approx 0.00$).

2.  **Modelagem de Preços (ARIMA):**
    * Os parâmetros $(p=1, q=1)$ foram identificados via gráficos ACF e PACF.
    * O modelo **ARIMA(1, 1, 1)** foi treinado para previsão de preço.

3.  **Modelagem de Volatilidade (GARCH):**
    * Devido à falha do ARIMA em prever a direção (previsão em linha reta) e ao diagnóstico de **Heteroscedasticidade** (volatilidade não constante, $P(H) = 0.00$), foi necessário modelar o risco.
    * O modelo **GARCH(1, 1)** foi aplicado aos retornos logarítmicos para modelar a persistência da volatilidade (*volatility clustering*).

## Resultados Chave

| Modelo/Métrica | Resultado | Insights |
| :--- | :--- | :--- |
| **ARIMA(1, 1, 1) - RMSE** | $7.0731$ | O modelo falhou na previsão de preço (linha reta), confirmando a **inadequação do ARIMA** para capturar a tendência em séries financeiras voláteis. |
| **GARCH(1, 1) - $\alpha + \beta$** | $0.9000$ | Os parâmetros $\alpha$ (choque recente) e $\beta$ (persistência) são altamente significativos, confirmando que a volatilidade é **altamente persistente** e o modelo GARCH captura a estrutura de risco da série. |

## Fonte de Dados

* **Dataset:** [Big Tech Giants Stock Price Data](https://www.kaggle.com/datasets/umerhaddii/big-tech-giants-stock-price-data) (Kaggle)

---