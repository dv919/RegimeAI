<div align="center">

# 📈 RegimeAI

### Machine Learning-Based Market Regime Detection and Forecasting

*Discovering hidden market states with unsupervised learning, and forecasting their transitions with gradient boosting.*

![Python](https://img.shields.io/badge/Python-3.9+-3776AB?style=flat&logo=python&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-77.8%25_Accuracy-FF6F00?style=flat)
![scikit-learn](https://img.shields.io/badge/scikit--learn-GMM-F7931E?style=flat&logo=scikit-learn&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=flat)
![Status](https://img.shields.io/badge/Status-Complete-success?style=flat)

</div>

---

## 🧭 Overview

Financial markets move through distinct behavioral regimes — **bull runs, corrections, recoveries, and crashes.** Spotting these hidden states as they form, and forecasting when they'll shift, is one of the foundational problems in quantitative finance.

**RegimeAI** is an end-to-end ML framework that tackles this problem in four stages:

| Stage | What it does |
|:---|:---|
| 🔍 **Discover** | Uncover hidden market regimes using unsupervised learning |
| 🔮 **Forecast** | Predict next-day market regimes using supervised learning |
| 🔄 **Analyze** | Study regime transitions, persistence, and stability |
| 💰 **Evaluate** | Test regime-aware portfolio allocation strategies |

The pipeline pairs **Gaussian Mixture Models (GMM)** for regime discovery with **XGBoost** for regime forecasting, trained on 15 years of multi-asset ETF market data.

---

## ❓ Research Questions

> **1. Can machine learning discover hidden market regimes?**
> Using engineered market features, an unsupervised model identifies distinct market states — with no predefined labels.

> **2. Can future market regimes be predicted?**
> Using historical market characteristics, supervised models forecast tomorrow's regime, today.

---

## 📊 Dataset

Daily adjusted prices sourced via **Yahoo Finance**, spanning **2010 → Present** (15 years).

| Ticker | Asset Class |
|:---:|:---|
| 🟦 `SPY` | S&P 500 ETF |
| 🟩 `QQQ` | Nasdaq-100 ETF |
| 🟨 `TLT` | 20+ Year Treasury Bond ETF |
| 🟧 `GLD` | Gold ETF |

---

## 🧩 Feature Engineering

**12 engineered features**, spanning four categories of market behavior:

<table>
<tr>
<td valign="top" width="25%">

**📉 Returns**
- SPY Daily Return
- QQQ Daily Return
- TLT Daily Return
- GLD Daily Return

</td>
<td valign="top" width="25%">

**⚡ Volatility**
- 20-Day Rolling Volatility
- 60-Day Rolling Volatility
- Volatility Ratio

</td>
<td valign="top" width="25%">

**🚀 Momentum**
- 30-Day Momentum
- 90-Day Momentum

</td>
<td valign="top" width="25%">

**📐 Trend & Cross-Asset**
- Price / 50-Day MA
- Price / 200-Day MA
- 60-Day SPY–QQQ Correlation

</td>
</tr>
</table>

---

## ⚙️ Methodology

### Phase 1 — Market Regime Discovery 🔍

Gaussian Mixture Models cluster the engineered feature space into latent market states. Model complexity (number of regimes) is chosen via the **Bayesian Information Criterion (BIC)**.

<div align="center">

### 🏆 Result: 7 Distinct Market Regimes Identified

| 🟢 Stable Bull | 🔵 Momentum Bull | 🟣 Recovery Rally | 🟡 Late Bull |
|:---:|:---:|:---:|:---:|
| **🟠 Transition** | **🔴 Correction** | **⚫ Crash Regime** | |

</div>

### Phase 2 — Market Regime Forecasting 🔮

```
   Today's Features  ──────▶  Tomorrow's Market Regime
```

Two models were benchmarked head-to-head on a **chronological 80/20 split** — no shuffling, fully out-of-sample:

- ✅ Random Forest
- ✅ XGBoost

---

## 🏁 Results

### Regime Forecasting Performance

<div align="center">

| Model | Accuracy |
|:---|:---:|
| Random Forest | 76.2% |
| 🥇 **XGBoost** | **77.8%** |

</div>

> **XGBoost wins** with the highest out-of-sample multiclass accuracy for next-day regime prediction.

### Portfolio Evaluation 💼

A regime-aware allocation strategy was built on top of the predicted regimes and benchmarked against buy-and-hold:

<div align="center">

| Strategy | Sharpe Ratio | Max Drawdown |
|:---|:---:|:---:|
| Regime Strategy | 0.716 | −23.8% |
| SPY Buy & Hold | **0.733** | −23.5% |

</div>

> 🔎 **Key insight:** the ML framework discovered and forecasted regimes successfully — but hand-designed allocation rules *didn't* beat a simple SPY benchmark. A sharp reminder that **predictive accuracy ≠ investable alpha.**

---

## 🔑 Key Findings

- ✅ Market behavior segments cleanly into **economically meaningful hidden states**
- ✅ **Volatility, momentum, and trend** indicators are strong predictors of regime shifts
- ✅ **GMM** effectively recovers latent market structure without supervision
- ✅ **XGBoost** reaches **77.8%** out-of-sample multiclass accuracy
- ⚠️ Accurate regime prediction alone **does not guarantee** superior portfolio performance

---

## 🛠️ Tech Stack

<div align="center">

![Python](https://img.shields.io/badge/-Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/-Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/-NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![scikit-learn](https://img.shields.io/badge/-scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![XGBoost](https://img.shields.io/badge/-XGBoost-FF6F00?style=for-the-badge)
![Matplotlib](https://img.shields.io/badge/-Matplotlib-11557C?style=for-the-badge)

</div>

**Machine Learning:** Gaussian Mixture Models (GMM) · Random Forest · XGBoost
**Data Source:** `yfinance`

---

## 🚧 Future Improvements

- [ ] Walk-forward validation
- [ ] SHAP explainability analysis
- [ ] Regime-specific portfolio optimization
- [ ] Hidden Markov Models (HMM)
- [ ] Reinforcement learning for dynamic allocation
- [ ] Multi-asset portfolio construction

---

## 📁 Repository Structure

```
RegimeAI/
│
├── data/
│   └── market_data.csv
│
├── notebooks/
│   └── regime_forecasting.ipynb
│
├── figures/
│   ├── bic_selection.png
│   ├── regime_visualization.png
│   └── equity_curve.png
│
├── README.md
└── requirements.txt
```

---

<div align="center">

### 👤 Author
DEEKSHA V(ED23B015)

</div>
