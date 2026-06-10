RegimeAI: Machine Learning-Based Market Regime Detection and Forecasting
Overview

Financial markets exhibit distinct behavioral patterns such as bull markets, corrections, recoveries, and crashes. Identifying these hidden market states and forecasting future transitions is a fundamental challenge in quantitative finance.

This project develops an end-to-end machine learning framework to:

Discover hidden market regimes using unsupervised learning
Forecast future market regimes using supervised learning
Analyze regime transitions and persistence
Evaluate regime-aware portfolio allocation strategies

The framework combines Gaussian Mixture Models (GMM) for regime discovery and XGBoost for regime forecasting on 15 years of ETF market data.

Research Objective

The project aims to answer two key questions:

1. Can machine learning discover hidden market regimes?

Using engineered market features, an unsupervised learning model identifies distinct market states without predefined labels.

2. Can future market regimes be predicted?

Using historical market characteristics, supervised machine learning models forecast next-day market regimes.

Dataset

Historical daily adjusted prices were collected using Yahoo Finance.

Assets used:

Asset	Description
SPY	S&P 500 ETF
QQQ	Nasdaq-100 ETF
TLT	20+ Year Treasury Bond ETF
GLD	Gold ETF

Time Period:

2010 – Present
Feature Engineering

Twelve market features were engineered from raw price data:

Return Features
SPY Daily Return
QQQ Daily Return
TLT Daily Return
GLD Daily Return
Volatility Features
20-Day Rolling Volatility
60-Day Rolling Volatility
Volatility Ratio
Momentum Features
30-Day Momentum
90-Day Momentum
Trend Features
Price / 50-Day Moving Average
Price / 200-Day Moving Average
Cross-Asset Features
60-Day Rolling Correlation (SPY vs QQQ)
Methodology
Phase 1: Market Regime Discovery

Gaussian Mixture Models (GMM) were used to identify hidden market regimes.

Model selection was performed using the Bayesian Information Criterion (BIC).

Result:

7 Distinct Market Regimes Identified

Example regimes:

Stable Bull Market
Momentum Bull Market
Recovery Rally
Correction
Transition
Late Bull Market
Crash Regime
Phase 2: Market Regime Forecasting

A next-day regime prediction problem was formulated.

Target:

Today's Features
        ↓
Tomorrow's Market Regime

Models evaluated:

Random Forest
XGBoost

Training Procedure:

Chronological Train/Test Split (80/20)
No Data Shuffling
Out-of-Sample Evaluation
Results
Regime Forecasting Performance
Model	Accuracy
Random Forest	76.2%
XGBoost	77.8%

XGBoost achieved the highest out-of-sample accuracy in forecasting future market regimes.

Portfolio Evaluation

A regime-aware asset allocation strategy was constructed using predicted market regimes.

Performance Metrics:

Strategy	Sharpe Ratio	Max Drawdown
Regime Strategy	0.716	-23.8%
SPY Buy & Hold	0.733	-23.5%

While the machine learning framework successfully identified and forecasted market regimes, manually designed allocation rules did not outperform a simple SPY benchmark, highlighting the difficulty of converting predictive signals into investment alpha.

Key Findings
Market behavior can be segmented into economically meaningful hidden states.
Volatility, momentum, and trend indicators are strong predictors of regime transitions.
Gaussian Mixture Models effectively identify latent market structures.
XGBoost achieved 77.8% multiclass out-of-sample accuracy.
Accurate regime prediction alone does not guarantee superior portfolio performance.
Technology Stack
Programming Language
Python
Libraries
pandas
numpy
yfinance
scikit-learn
xgboost
matplotlib
Machine Learning
Gaussian Mixture Models (GMM)
Random Forest
XGBoost
Future Improvements

Potential extensions include:

Walk-forward validation
SHAP explainability analysis
Regime-specific portfolio optimization
Hidden Markov Models (HMM)
Reinforcement learning for dynamic allocation
Multi-asset portfolio construction
Repository Structure
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
│
└── requirements.txt
Author

Developed as a quantitative finance and machine learning research project exploring market regime discovery, forecasting, and portfolio applications.

Resume Title

Use this exact title on your resume:

RegimeAI: Market Regime Detection and Forecasting using Gaussian Mixture Models and XGBoost

It's concise, technical, and immediately signals both finance and ML to recruiters.
