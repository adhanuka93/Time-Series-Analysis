# Quant Research Portfolio

Two projects implementing quantitative finance models from scratch.

## Projects

### Project 01 — Volatility Forecasting (SPY)
Implements and compares three volatility models on SPY daily returns:
realized volatility, EWMA, and GARCH(1,1) from scratch via MLE.

Key finding: ARIMA residuals have autocorrelated squares — variance is 
predictable even when returns are not. GARCH captures this with three 
parameters estimated via maximum likelihood.

→ [Project 01](./project_01/)

### Project 02 — Cointegration and Statistical Arbitrage
Demonstrates cointegration pipeline on synthetic data, then applies 
Kalman filter from scratch to GLD/GDX real data.

Key finding: Static OLS hedge ratio fails over 15 years — the GLD/GDX 
relationship is time-varying. Kalman filter tracks β_t dynamically, 
producing a stationary spread where the static approach fails.

→ [Project 02](./project_02/)

## Technical Stack
- Python — NumPy, Pandas, SciPy, Matplotlib, statsmodels
- Models implemented from scratch: GARCH(1,1) via MLE, Kalman filter,
  OU process, ACF/PACF
- Data: yfinance (SPY, GLD, GDX, TLT)
