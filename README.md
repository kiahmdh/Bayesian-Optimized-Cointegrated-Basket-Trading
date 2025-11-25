# Bayesian-Optimized Cointegrated Basket Trading

Full, end-to-end quantitative trading pipeline for building and testing **cointegrated mean-reversion baskets**.  
The project combines **Johansen cointegration**, **Bayesian hyperparameter optimization**, and **OU / AR(1) diagnostics** with transaction-cost-aware backtesting and rich visualizations.

* * *

## Features

- **Cointegration-Based Basket Construction**
  - Uses Johansen test to extract the cointegration vector.
  - Supports both `Adj Close` and `Close` prices.
  - Handles new yfinance **MultiIndex** format robustly.
  - Optional **log-price** transformation for better cointegration behavior.

- **Mean-Reversion Trading Strategy**
  - Z-score based entry/exit rules:
    - Enter short when spread is high (positive z).
    - Enter long when spread is low (negative z).
    - Exit to flat inside a neutral band.
  - Supports **rolling** or **EMA-based** z-scores.

- **Bayesian Hyperparameter Optimization**
  - Optimizes on training data:
    - Lookback window length.
    - Entry Z-score threshold.
    - Exit Z-score threshold.
  - Uses `bayesian-optimization` package (Gaussian Process based).
  - Penalizes invalid parameter regions to keep the search stable.

- **Realistic Backtesting**
  - Daily frequency with configurable **transaction costs** per position change.
  - Computes:
    - Sharpe ratio
    - Total return
    - Volatility
    - Maximum drawdown
    - Win rate
  - Runs on train and test splits to check for overfitting.

- **OU / AR(1) Diagnostics**
  - Fits AR(1) model on the spread and maps it to OU parameters:
    - Mean reversion speed (κ)
    - Long-run mean (μ)
    - Half-life of mean reversion
  - Helps identify whether the spread is actually tradeable.

- **Visualization Suite**
  - Spread plot with **train/test split**.
  - Z-score + thresholds + position shading (long/short regimes).
  - Equity curve with **drawdown overlay**.
  - OU **forecast bands** (68% and 95% confidence) on future spread.
  - Residual histogram vs normal distribution to check model fit.

- **Trade Log & Analysis**
  - Builds per-trade records:
    - Entry/exit dates
    - Long/short direction
    - PnL per trade
    - Holding period
  - Reports:
    - Trade count
    - Win rate
    - Average PnL
    - Average holding duration

* * *

## Project Structure

- `main.py` – main script containing:
  - data download and split
  - cointegration estimation
  - strategy and backtest logic
  - Bayesian optimization
  - plots and diagnostics
- `requirements.txt` – Python dependencies (yfinance, bayesian-optimization, statsmodels, numpy, pandas, matplotlib).
- `README.md` – this document.
- (optional) `notebooks/` – Jupyter or Colab notebooks for experiments.
- (optional) `figures/` – saved plots (spread, equity, forecast, etc.).

* * *

## How to Run

It is recommended to start in a **virtual environment** or **Google Colab**.
