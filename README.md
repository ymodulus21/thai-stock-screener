# 🇹🇭 Thai Stock Screener — Multi-Factor Quantitative Model

> A systematic, data-driven stock screening framework for the Thai SET market.
> Combines fundamental quality filters with quantitative factor scoring to select high-conviction portfolios.

[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)](https://jupyter.org)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

---

## Performance Summary (Out-of-Sample)

| Metric | Thai Quant Model | SET TRI Index | vs Benchmark |
|---|---|---|---|
| **Sharpe Ratio** | **0.837** | ~0.32 | **+162%** better |
| **Max Drawdown** | **-12.5%** | -45%+ | **3.6x** less risk |
| **CAGR** | **16.4%** | ~8-10% | +6-8% alpha/yr |
| **WFT Beat Rate** | **67%** | — | OOS validated |
| **Backtest Period** | 10 years (2014–2024) | — | Full market cycles |
| **Live Paper Trade** | +0.41% (Mar 2026) | -4.99% | **+5.4% alpha** |

> ✅ **Live paper trading since March 27, 2026** — Month 1 outperformed SPY by +5.40%

---

## What This Project Does

This screener identifies high-quality Thai stocks using a **4-factor scoring system**:

```
Universe: Thai SET Market (~500+ stocks, survivorship-bias corrected)
     │
     ▼
[Factor Scoring]
  ├── Quality    — ROE, Debt/Equity, Current Ratio
  ├── Value      — P/E, P/B, EV/EBITDA (Point-In-Time)
  ├── Growth     — Revenue YoY, EPS YoY, Earnings momentum
  └── Momentum   — Price momentum 3M, 6M, 12M
     │
     ▼
[Risk Filters]
  ├── Volatility filter — removes high-vol outliers
  ├── Liquidity filter  — minimum avg daily volume
  └── Sector constraint — max 3 stocks per sector
     │
     ▼
[Portfolio: Top 10-15 stocks, rebalanced monthly]
```

---

## Key Features

### ✅ Point-In-Time (PIT) Fundamentals
No look-ahead bias. Financial data is only used **after** it would have been publicly available (filing date + 60-day SEC delay), preventing the most common backtest inflation error.

### ✅ Walk-Forward Optimization
```
Training:   IS  70% (in-sample)
Validation: OOS 30% (out-of-sample)
Method:     Rolling 18-month IS / 6-month OOS windows
```
Results are validated on data the model **never saw during training**.

### ✅ 7-Layer Risk Management System
```
L1: Regime Filter      — SPY vs SMA200 → BULL/SIDEWAYS/BEAR exposure
L2: Volatility Target  — Scale position to 15% annual vol target
L3: Circuit Breaker    — Auto-reduce exposure at -10/-15/-20% drawdown
```

### ✅ Survivorship-Bias Corrected
Uses full historical SET universe — not just current listed stocks — to avoid inflating backtest results with companies that only survived because they performed well.

---

## Factor Details

### Quality Score
```python
quality_score = (
    0.35 * roe_score +          # Return on Equity
    0.35 * debt_equity_score +  # Financial leverage
    0.30 * current_ratio_score  # Short-term liquidity
)
```

### Value Score (Point-In-Time)
```python
value_score = (
    0.40 * pe_score +     # Price-to-Earnings (PIT)
    0.35 * pb_score +     # Price-to-Book (PIT)
    0.25 * ev_score       # EV/EBITDA
)
```

### Growth Score (TTM — Trailing Twelve Months)
```python
growth_score = (
    0.40 * revenue_yoy +  # Revenue growth YoY
    0.35 * eps_yoy +      # EPS growth YoY
    0.25 * gp_margin      # Gross profit margin trend
)
```

### Momentum Score
```python
momentum_score = (
    0.20 * mom_3m +   # 3-month price momentum
    0.40 * mom_6m +   # 6-month price momentum
    0.40 * mom_12m    # 12-month price momentum
)
```

---

## Results — Equity Curve

```
Portfolio Value (Normalized to 100, 2014–2024)

400 ┤                                              ╭────
    │                                         ╭───╯
300 ┤                                    ╭────╯
    │                              ╭─────╯
200 ┤                    ╭─────────╯
    │          ╭─────────╯
100 ┤──────────╯
    └──────────────────────────────────────────────────
    2014  2015  2016  2017  2018  2019  2020  2021  2022  2023  2024

Thai Quant Model ───  CAGR 16.4% | Sharpe 0.837
SET TRI Index    - -  CAGR ~9%   | Sharpe ~0.32
```

---

## Backtesting Methodology

| Parameter | Value |
|---|---|
| Backtest Period | Jan 2014 – Dec 2024 (10 years) |
| Rebalancing | Monthly (1st trading day) |
| Transaction Costs | 0.25% per trade (buy + sell) |
| Portfolio Size | 10–15 stocks |
| Universe | SET market, survivorship-bias corrected |
| Data Source | Fundamental + price data, PIT-adjusted |
| Walk-Forward | 18-month IS / 6-month OOS rolling |

---

## Live Paper Trading

| Month | Portfolio | SPY | Alpha |
|---|---|---|---|
| **Mar 2026** | **+0.41%** | **-4.99%** | **+5.40%** ✅ |
| Apr 2026 | In progress | — | — |

> Paper trading started: March 27, 2026
> Next evaluation: May 2, 2026

---

## Project Structure

```
thai-stock-screener/
│
├── screener/
│   ├── factor_scoring.py      # Quality, Value, Growth, Momentum
│   ├── pit_fundamentals.py    # Point-In-Time data handling
│   └── universe_builder.py   # SET universe construction
│
├── backtest/
│   ├── engine.py              # Portfolio simulation engine
│   ├── walk_forward.py        # WFT implementation
│   └── risk_system.py         # 7-layer risk management
│
├── notebooks/
│   ├── 01_screening.ipynb     # Factor screening walkthrough
│   ├── 02_backtest.ipynb      # Full backtest analysis
│   └── 03_results.ipynb       # Performance visualization
│
└── README.md
```

---

## Requirements

```bash
pip install pandas numpy matplotlib seaborn scipy yfinance jupyter
```

---

## Related Projects

| Project | Description |
|---|---|
| [thai-portfolio-backtester](https://github.com/ymodulus21/thai-portfolio-backtester) | Full portfolio backtesting engine with walk-forward optimization |
| [thai-stock-backtestv2](https://github.com/ymodulus21/thai-stock-backtestv2) | Enhanced backtest v2 with PIT data and bias corrections |
| [thai-stock-screener-app](https://github.com/ymodulus21/thai-stock-screener-app) | Full pipeline application combining all components |

---

## Author

**Kittipong Mahaheng (Bass)**
Business Administration | Quantitative Finance Enthusiast
5+ years trading experience — Forex, BTC, Gold, SET & S&P500

[![GitHub](https://img.shields.io/badge/GitHub-ymodulus21-181717?style=flat&logo=github)](https://github.com/ymodulus21)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=flat&logo=linkedin)](https://linkedin.com)

---

<div align="center">

*Built with systematic thinking, not gut feeling.*

</div>
