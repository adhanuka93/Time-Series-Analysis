"""
Project 01 — Volatility Forecasting
=====================================
Motivation:
- ARIMA(1,1) adequately models the conditional mean of SPY log returns
- But ACF of squared residuals shows strong autocorrelation
- Variance is predictable even when mean is not
- GARCH(1,1) models this time-varying variance

Models implemented:
1. Realized volatility — rolling std (naive baseline)
2. EWMA — exponential weighted moving average (RiskMetrics)
3. GARCH(1,1) — from scratch via MLE (main contribution)

Key findings:
- GARCH parameters: alpha=0.15, beta=0.81, alpha+beta=0.96
- Long run annualized vol: 16.3%
- All three models track each other closely
- GARCH provides most theoretically justified forecast
"""
