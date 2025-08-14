# Realistic Opening Range Breakout Backtesting

This repository implements a realistic backtesting framework for the Opening Range Breakout (ORB) day‑trading strategy. It is inspired by the paper *“Can Day Trading Really Be Profitable? Evidence of Sustainable Long‑term Profits from Opening Range Breakout (ORB) Day Trading Strategy vs. Benchmark in the US Stock Market”* by Carlo Zarattini and Andrew Aziz.

## Background
Day trading has become very popular, especially among retail investors. Many studies have shown that most day traders lose money.  The ORB strategy enters long or short when a stock breaks out from its initial range.  The paper claims that using leverage or leveraged ETFs with ORB can generate significant returns, including an annualised alpha of 33 % and a cumulative return of 1 ,484 % from 2016–2023 compared with 169 % for passive QQQ.

## Goals
This project aims to:

- Recreate and extend the results of the referenced paper with transparent, reproducible code.
- Model realistic trading frictions including commissions, slippage, margin requirements and borrow fees.
- Compare the ORB strategy against passive buy‑and‑hold benchmarks.
- Test both cash‑based leverage and leveraged ETFs to see if leverage truly improves results.
- Provide configurable parameters (range duration, position sizing, stop‑loss rules) to explore sensitivity.

## Contents
- **Notebooks and scripts** to download intraday QQQ/TQQQ data and execute n‑minute ORB strategies.
- **Backtesting engine** that simulates trades with realistic constraints.
- **Performance metrics** including CAGR, Sharpe ratio, alpha versus benchmark and drawdown.

- **Examples** illustrating how to run the pipeline and interpret the results.


## Code overview

This project includes a Jupyter notebook, `ORB_phased_research_pipeline_plots.ipynb`, that implements a phased research pipeline to evaluate the Opening Range Breakout strategy.  Key components include:

- **Signal construction** – A helper function `build_orb_signals()` identifies the n‑minute opening range from intraday data and creates long/short signals when price breaks above or below that range.
- **Fast backtesting** – `simulate_vectorbt()` wraps vectorbt to backtest these signals quickly with realistic trading frictions (spreads, slippage, commissions, borrow fees) and supports both cash‑based leverage and leveraged ETFs.
- **Hyper‑parameter tuning** – A function `search_orb_parameters()` uses Optuna to search over parameters such as opening range duration, stop‑loss size and entry timing, optimizing metrics like alpha and Sharpe ratio.
- **Helper utilities** – Additional functions load intraday data (using environment variables for API keys), generate monthly walk‑forward windows and compute performance metrics (CAGR, alpha, Sharpe ratio, drawdown).
- **Phased workflow** – The notebook is divided into phases: `FAST R&D` runs vectorbt backtests and parameter search; `CONFIRMATION` (commented out) sketches a deterministic backtest using zipline‑reloaded; `ROBUSTNESS` (commented out) proposes using mlfinlab’s Purged Walk‑Forward cross‑validation for out‑of‑sample testing.

No API keys or secrets are embedded in this notebook; data is accessed via environment variables (e.g., `POLYGON_API_KEY`, `ALPHA_VANTAGE_API_KEY`), so please set these locally before running.- **Examples** illustrating how to run the pipeline and interpret the results.

## Disclaimer
This project is for educational and research purposes.  Past performance does not guarantee future results, and high leverage can magnify losses as well as gains.  Always do your own due diligence before trading or investing.
