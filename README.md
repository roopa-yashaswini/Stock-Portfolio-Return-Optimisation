# 📊 S&P 500 Portfolio Optimization Using Risk-Averse Modelling

## 🧠 Project Overview

This project tackles a core challenge in modern investment: how to create a well-diversified portfolio that maximizes return while controlling for risk and maintaining sector balance. We apply **constrained optimization techniques** to construct an **optimal investment portfolio** from the S&P 500, using historical price data and sector classifications to guide allocation.

---

## 📌 Problem Statement

Traditional portfolio strategies often rely on subjective heuristics, resulting in suboptimal diversification and inconsistent yields. This project frames portfolio construction as a **quantitative optimization problem**, balancing return maximization with:

- Risk aversion
- Industry diversification
- Stock exposure limits

The model is designed to support investors in developing a data-driven, customizable portfolio strategy.

---

## 🧾 Datasets Used

1. **Historical Stock Prices** (Yahoo Finance)  
   - Fetched via `yfinance` for all S&P 500 companies (past 4 years)

2. **Sector Classification** (Wikipedia GICS)  
   - Used to enforce diversification constraints

3. **Covariance Matrix of Returns**  
   - Captures inter-stock correlations and portfolio risk exposure

---

## 🧮 Optimization Model

Built using **Gurobi**, the model maximizes expected returns while accounting for risk and enforcing business constraints.

### 🔧 Decision Variables

- `x_s`: Continuous variable for proportion of capital allocated to stock *s*
- `z_s`: Binary variable for stock inclusion
- `z_i`: Binary variable for industry sector inclusion

### 🎯 Objective Function

Maximize:

```
Sum(weighted stock returns) - RiskAversion * Sum(weighted covariances)
```

Where risk aversion is a tunable parameter (e.g., 0.7).

### 📋 Constraints

1. **Total Investment** = 100%
2. **Individual Stock Bounds**: 1% ≤ allocation ≤ 10%
3. **Minimum Stocks**: At least 25
4. **Risk Constraint**: Total risk < 10%
5. **Industry Diversification**: Minimum 10 sectors represented

---

## 📈 Results

The optimized portfolio achieved:

- ✅ **Expected Return**: 1.006 — higher than the benchmark average
- 📉 **Risk Variance**: 0.058 (Standard Deviation: 0.24) — well below traditional portfolios
- 🧩 **Diversification**: Met strict inclusion of 25+ stocks and 10+ industry sectors
- 💼 **Robustness**: Consistently avoided overexposure to volatile stocks and concentrated sectors
- 🧠 **Smart Allocation**: Capital was tactically distributed to top-performing yet less correlated equities, offering a strong trade-off between growth and stability.

🔍 These results demonstrate the power of integrating financial data with mathematical modeling. Compared to naive diversification, this optimization strategy offers **precision allocation** with quantifiable improvements in **risk-adjusted performance**.

---

## 🚀 How to Use the Prototype

### 1. Data Collection
Use the `fetch_sp500_data()` function to retrieve current prices and save them to `sp500_stock_data_new.csv`. You may customize tickers or time range.

### 2. Run the Optimization
Run the model with a default risk aversion setting of **0.7**. Adjust this parameter and constraints to reflect your own risk profile and sector preferences.

### 3. Analyze the Output
Get a list of selected stocks with their allocated investment weights for implementation or further simulation.

---

## 💼 Tools Used

- **Python**, **Gurobi**
- `yfinance`, `pandas`, `numpy`
- Sector scraping via `requests` and `BeautifulSoup`

---

## 📊 Visual Analysis 

- Sector-wise return heatmaps
- Correlation matrix
- Top/Bottom performers
- Sector contribution insights

