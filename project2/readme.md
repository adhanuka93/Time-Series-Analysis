# Project 02 — Cointegration and Statistical Arbitrage

## Motivation
Two assets that share a common economic driver may be cointegrated — their 
prices drift together in the long run even though each individually is a 
random walk. When the spread between them deviates from equilibrium, it 
creates a mean-reversion trading opportunity.

## Data
- Synthetic cointegrated pair (Part A) — known ground truth for validation
- GLD (Gold ETF) and GDX (Gold Miners ETF) 2010–2026 (Part B)
- Source: yfinance, daily adjusted close prices

## Part A — Static Hedge Ratio (Synthetic Data)

### Methodology
- Generated synthetic cointegrated pair with true β = 1.5
- Estimated hedge ratio via OLS
- Tested spread stationarity via ADF 
- Fit OU process to spread via AR(1) regression — extracted half-life
- Constructed z-score trading signal — entry at ±2σ, exit at 0.5σ

### Results
- OLS accurately recovered the true hedge ratio
- ADF confirmed stationarity — spread is mean reverting
- OU half-life consistent with fast mean reversion in synthetic data

## Part B — Dynamic Hedge Ratio (Real Data: GLD/GDX)

### Motivation
Static OLS hedge ratio fails over the full 2010–2026 sample:
- Spread drifts between −0.65 and +0.65
- ADF p-value = 0.33 — spread is not stationary
- The relationship between GLD and GDX is time-varying

### Methodology
- Implemented Kalman filter from scratch in NumPy
- State equation: β_t = β_{t-1} + η_t (random walk hedge ratio)
- Observation equation: log(GDX)_t = β_t · log(GLD)_t + ε_t
- Fixed hyperparameters: Q = 1e-5, R = var(log GDX)
- Proper estimation of Q and R via Kalman likelihood MLE is left as extension


### Key Finding
The hedge ratio between GLD and GDX drifted significantly over 15 years — 
from 0.80 in 2010 to 0.55 in 2016 and back to 0.75 in 2026. A static hedge 
ratio cannot cancel the common stochastic trend at all time points. The Kalman 
filter tracks this drift dynamically — producing a stationary spread where the 
static approach fails.

## What Did Not Work
- Static cointegration fails over the full sample — the relationship is not stable
- Large spike in dynamic spread during COVID 2020 — extreme market dislocation 
  breaks even the dynamic hedge ratio temporarily

## Limitations
- Q and R are fixed by hand — proper MLE estimation would be more rigorous
- No transaction costs modeled — spread trades frequently, costs matter
- Walk-forward validation not implemented — in-sample result only

## Physics Connection
- OU process = Langevin equation — same mathematics, different domain
- Kalman filter = state-space model used in experimental physics
- Half-life = same formula as GARCH variance mean reversion
