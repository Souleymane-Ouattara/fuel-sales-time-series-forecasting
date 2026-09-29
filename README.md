# Fuel Sales Forecasting with Time Series Models

This project develops and compares time-series forecasting approaches for monthly gasoline and diesel sales in France.

The analysis covers more than forty years of monthly observations and applies logarithmic transformations, seasonal decomposition, stationarity tests, ARMA and SARIMA modelling, residual diagnostics and twelve-month forecasting.

## Project objectives

The project aims to:

- identify the trend and seasonal structure of fuel sales;
- model the remaining temporal dependence;
- compare alternative forecasting specifications;
- validate the selected models against historical observations;
- produce twelve-month forecasts with uncertainty intervals;
- discuss the relevance of the results for energy-demand forecasting and commodity markets.

## Methodology

The monthly sales series are treated as multiplicative processes. A logarithmic transformation is therefore applied to stabilise their variance:

$$
Y_t = \log(X_t).
$$

The transformed series is represented using an additive decomposition:

$$
Y_t = T_t + S_t + R_t,
$$

where:

- $T_t$ is the trend component;
- $S_t$ is the seasonal component;
- $R_t$ is the residual component.

The modelling process includes:

1. logarithmic variance stabilisation;
2. trend and seasonal decomposition;
3. ACF and PACF analysis;
4. ADF, Phillips-Perron and KPSS stationarity tests;
5. ARMA and SARIMA estimation;
6. model comparison using AIC, BIC, MAE and RMSE;
7. residual diagnostics using Box-Pierce and Ljung-Box tests;
8. historical reconstruction and twelve-month forecasting.

## Gasoline sales

For gasoline sales, the logarithmic series is decomposed using STL.

The residual component is modelled with an ARMA(5,3) process:

$$
R_t
=
\sum_{i=1}^{5}\phi_i R_{t-i}
+
\sum_{j=1}^{3}\theta_j\varepsilon_{t-j}
+
\varepsilon_t.
$$

The reconstructed historical series achieves:

| Metric | Value |
|---|---:|
| MAE | 26.61 |
| RMSE | 37.71 |
| MAPE | 2.82% |
| $R^2$ | 0.989 |
| Mean bias | 2.47 |

The model reproduces the historical trend and seasonal behaviour while accounting for the disruption observed around 2020. It is subsequently used to generate twelve-month forecasts with 95% confidence intervals.

## Diesel sales

Two approaches are compared for diesel sales:

1. decomposition of the logarithmic series followed by an ARMA model fitted to the residual component;
2. direct modelling of the logarithmic series using a seasonal ARIMA specification.

The principal candidate models are:

- ARMA(4,4);
- SARIMA(2,1,4)(0,1,1)[12].

Based on historical reconstruction metrics, the decomposition and ARMA(4,4) approach provides the best empirical fit:

| Metric | ARMA(4,4) | SARIMA |
|---|---:|---:|
| MAE | 51.86 | 67.35 |
| RMSE | 84.47 | 112.22 |
| MAPE | 2.56% | 3.34% |
| $R^2$ | 0.9854 | 0.9749 |
| Mean bias | -2.10 | -9.73 |

The selected model is then used to produce a twelve-month forecast for diesel sales.

## Main findings

- Both fuel-sales series exhibit strong annual seasonality.
- A logarithmic transformation substantially stabilises their variance.
- Decomposition followed by ARMA modelling provides accurate historical reconstructions.
- The models capture the principal dynamics surrounding the disruption observed in 2020.
- Gasoline sales are reconstructed with a MAPE below 3%.
- For diesel sales, the decomposition and ARMA approach outperforms the selected SARIMA model on the reported historical-fit metrics.
- The resulting forecasts retain the seasonal patterns observed in the historical data.

## Market relevance

Fuel-demand forecasting is relevant to several operational and financial applications, including:

- inventory and supply planning;
- energy-demand monitoring;
- commodity-market analysis;
- risk management;
- short-term hedging decisions;
- scenario analysis for energy-sector exposures.

## Report and source code

The complete report is available here:

[Read the full report](report/fuel_sales_time_series_forecasting_report.pdf)

The R implementations are included directly in the report:

- Appendix A: gasoline-sales modelling;
- Appendix B: diesel-sales modelling.

No separate source-code files are provided in this repository.

## Technologies and statistical methods

- R
- `forecast`
- `tseries`
- `ggplot2`
- `dplyr`
- `lubridate`
- `zoo`
- STL decomposition
- ARMA and SARIMA models
- ACF and PACF analysis
- ADF, Phillips-Perron and KPSS tests
- Ljung-Box and Box-Pierce diagnostics

## Reproducibility note

The report contains the complete R scripts used for the analysis. However, the original dataset is not distributed in this repository, and some file paths in the appendices refer to the authors' local environments.

Users wishing to reproduce the analysis must obtain the corresponding monthly fuel-sales data and adapt the local file paths in the R scripts.

## Repository structure

```text
.
├── README.md
└── report/
    └── fuel_sales_time_series_forecasting_report.pdf
```

## Authors

- Salimata Diouf
- Christ Ange Dylan Kouame
- Aboubakar Ouattara
- Souleymane Ouattara

Academic time-series project completed at ISFA.

Supervisor: Prof. Christian Robert.

## Disclaimer

This repository presents an academic forecasting exercise. The forecasts should not be interpreted as investment recommendations, official market projections or operational advice.
