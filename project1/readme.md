# Project 01 — Volatility Forecasting (SPY)

## Motivation
ARIMA adequately models the conditional mean of SPY log returns — residuals 
are white noise. But ACF of squared residuals shows strong autocorrelation 
up to 20+ lags. Variance is predictable even when the mean is not. GARCH 
models this time-varying conditional variance explicitly.

## Data
- SPY (S&P 500 ETF) daily log returns 2010–2026
- Source: yfinance, adjusted close prices

## Models Implemented
1. **Realized volatility** — rolling std (naive baseline, equal weights)
2. **EWMA** — exponential weighted moving average (RiskMetrics)
3. **GARCH(1,1)** — from scratch via MLE (main contribution)

## Methodology

### ARIMA motivation
- Fitted ARIMA candidates to SPY log returns, compared via AIC/BIC
- ACF of residuals: flat — conditional mean adequately modeled
- ACF of squared residuals: significant autocorrelation up to 20+ lags
- Conclusion: variance has memory that ARIMA cannot capture → GARCH needed

### GARCH(1,1)
- Variance equation: σ²_t = ω + α·r²_{t-1} + β·σ²_{t-1}
- Zero mean assumption — justified since ARIMA conditional mean is negligible
- MLE via sequential loop + scipy.optimize.minimize (L-BFGS-B)
- Constraints: ω > 0, α ≥ 0, β ≥ 0, α + β < 1 (stationarity)
- Initialized at sample variance to ensure numerical stability

## Key Finding
All three models track each other closely. GARCH is theoretically superior 
because it has a finite long-run variance it reverts to — EWMA does not. 
Fitted α+β confirms SPY volatility is highly persistent but stationary — 
close to but below the EWMA boundary of 1.

## What Did Not Work
- ARIMA completely misses variance structure — adequate for mean, blind to risk
- All three models look visually similar — differences only apparent over 
  long horizons where GARCH mean-reverts and EWMA drifts

## Limitations
- Gaussian innovations assumed — SPY returns have fat tails, Student-t 
  GARCH would be more appropriate
- No formal forecast evaluation — QLIKE loss and Mincer-Zarnowitz regression 
  left as extension
- In-sample fit only — walk-forward validation not implemented

