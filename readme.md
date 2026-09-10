# Quant Research Portfolio — Time Series & Volatility Modeling

Two projects implementing quantitative finance models from scratch,
emphasizing mathematical depth and honest out-of-sample validation.

**Methods:** GARCH, EWMA, ARIMA, Kalman filter, cointegration,
Ornstein-Uhlenbeck process, MLE, stationarity testing, pairs trading,
mean reversion, volatility forecasting, statistical arbitrage

---

## Projects

### [Project 01 — Volatility Forecasting (SPY)](./project1/)
Realized volatility, EWMA, and GARCH(1,1) from scratch via MLE on SPY 
daily returns 2010–2026.

**Key finding:** ARIMA residuals have autocorrelated squares — variance is 
predictable even when returns are not. GARCH captures this with three 
parameters estimated via maximum likelihood.

### [Project 02 — Cointegration and Statistical Arbitrage](./project2/)
Static OLS cointegration on synthetic data, then Kalman filter from scratch 
on real GLD/GDX data 2010–2026.

**Key finding:** Static hedge ratio fails over 15 years — relationship is 
time-varying. Kalman filter tracks β_t dynamically, producing a stationary 
spread where the static approach fails.

---

## Technical Stack
- Python — NumPy, Pandas, SciPy, Matplotlib, statsmodels
- Models from scratch: GARCH(1,1) via MLE, Kalman filter, OU process, ACF/PACF
- Data: yfinance (SPY, GLD, GDX, TLT)
