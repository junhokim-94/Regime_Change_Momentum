# REGIME-AWARE MOMENTUM STRATEGY — Hidden Markov Model (HMM)

## Project Overview

This project implements a regime-aware momentum investing strategy using a Hidden Markov Model (HMM). The motivation stems from the limitations of static momentum strategies during regime shifts—especially after market downturns. By modeling regime dynamics explicitly, the strategy aims to reduce downside risk and improve return consistency.

While multiple regime classification models were explored in our research (Logistic Regression, Directional Change + Naive Bayes, and K-Means Clustering), this codebase implements the Hidden Markov Model (HMM).

## Authors

- Junho Kim  
- Yunjia Zhang  
- Xiaotian Wang  
- Yvonne Zhang  

## Dependencies

```bash
pandas
numpy
matplotlib
seaborn
wrds
pandas_datareader
hmmlearn
scikit-learn
statsmodels
```

## Data Files

- `data_Junho.pkl`: Main macro & decile return data (monthly)
- `data_Logistic.pkl`, `data_KNN.pkl`, `data_dc.pkl`: ML strategy return predictions (not used in HMM code)
- `F-F_Research_Data_Factors.csv`: Fama-French 3-Factor + risk-free rate (monthly)

## Model Summary

### Hidden Markov Model (Current Implementation)

- Gaussian HMM with 4 regimes
- Inputs: Macro-financial indicators + decile returns
- Inferred regimes: Neutral, Recession, Normal, Recovery
- Portfolio adjusts long/short weights on Winner (D10) and Loser (D1) portfolios based on detected regime

### Regime-Based Weighting

| Regime     | Winner Weight | Loser Weight |
|------------|---------------|--------------|
| Neutral    | -0.5          | 0.5          |
| Recession  | -0.5          | 0.0          |
| Normal     | 1.0           | -1.0         |
| Recovery   | 0.5           | -1.0         |

## Output Plots

- Cumulative log returns: HMM-based vs. raw momentum
- In-sample (1980–2013) and out-of-sample (2014–2024) comparisons
- Plots saved as `.jpg`:  
  - `Return_In-sample.jpg`  
  - `Return_Out-of-sample.jpg`

## Regression Analysis

OLS regression of strategy excess return on:
- Fama-French 3-Factors (Mkt-RF, SMB, HML)
- Momentum (WML)

Outputs include:
- Regression summary
- Annualized alpha (from intercept)

## How to Run

1. Ensure required `.pkl` and `.csv` files are in your working directory
2. Install dependencies
3. Run the script:
   ```bash
   python "REGIME-AWARE MOMENTUM STRATEGY_Hidden Markov.py"
   ```

## Columns Used

Refer to the in-code table for full descriptions of economic indicators and return series used in the model (e.g., GS10, TEDRATE, UMCSENT, D1–D10, MOM).