# 🇹🇭 Thai Stock Screener

> A Python-based fundamental analysis tool for screening Thai SET stocks using quantitative scoring.

---

## 🚀 Overview

This project is designed to **analyze and rank Thai stocks** based on key fundamental metrics.
It applies a scoring system (0–100) to help identify **high-quality investment opportunities**.

---

## ✨ Features

* 📊 Fundamental screening across multiple financial dimensions
* 🧠 Scoring system (0–100) for easy comparison
* 📁 Export results to CSV files
* 📈 Data visualization with charts
* ⚡ Fast and scalable analysis using Python

---

## 🧮 Scoring Model

| Category            | Metrics                  | Weight |
| ------------------- | ------------------------ | ------ |
| 💰 Valuation        | P/E, P/BV                | 25%    |
| 📈 Profitability    | ROE, ROA, Net Margin     | 25%    |
| 🏦 Financial Health | D/E Ratio, Current Ratio | 20%    |
| 💸 Dividend         | Dividend Yield           | 15%    |
| 📊 Efficiency       | Asset Utilization        | 15%    |

> Final Score = Weighted sum of all categories (0–100)

---

## 📊 Sample Outputs

* `all_stocks_data.csv` → Raw financial data
* `screened_stocks.csv` → Filtered stocks
* `thai_stock_report.csv` → Final scoring report
* `thai_stock_screener.png` → Fundamental visualization
* `thai_stock_scores.png` → Score breakdown chart

---

## 🧾 Default Screening Criteria

* P/E ≤ 25
* P/BV ≤ 4
* ROE ≥ 8%
* Net Margin ≥ 3%
* Dividend Yield ≥ 1%

---

## 🛠 Tech Stack

* Python
* Pandas
* NumPy
* yFinance
* Matplotlib

---

## ⚙️ Installation & Usage

```bash
pip install yfinance pandas numpy matplotlib seaborn
```

Run the notebook:

```bash
jupyter notebook thai_stock_screener.ipynb
```

---

## 📸 Preview

> Add your generated charts here for better presentation

```
![Fundamental Chart](https://raw.githubusercontent.com/ymodulus21/thai-stock-screener/main/thai_stock_screener.png)
![Score Breakdown](https://raw.githubusercontent.com/ymodulus21/thai-stock-screener/main/thai_stock_scores.png)

```

---

## 🎯 Future Improvements

* Add more financial ratios (PEG, Free Cash Flow, etc.)
* Integrate real-time data APIs
* Build web dashboard (Streamlit / Dash)
* Add backtesting system

---

## ⚠️ Disclaimer

This project is for **educational purposes only**.
Not intended as financial advice.

---

## 👨‍💻 Author

Kittiphong Mahaheng

---

## ⭐ If you like this project

Give it a star ⭐ on GitHub!
