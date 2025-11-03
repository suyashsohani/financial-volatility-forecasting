# Volatility Forecasting and Regime Detection in Financial Time Series

**Authors:** Suyash Sohani, Sayantan Banerjee\
**Date:** August 8, 2025

## Overview

This project investigates volatility forecasting and regime detection in
financial markets using **GARCH-family models** and **Markov Switching
Autoregression (MS-AR)**. It provides a unified framework for
understanding market volatility, structural shifts, and crisis-period
dynamics across major global indices.

## Objectives

1.  **Forecast Volatility** --- Evaluate GARCH and its extensions
    (EGARCH, GJR-GARCH) in predicting volatility of equity indices.\
2.  **Detect Market Regimes** --- Identify hidden high- and
    low-volatility states using Markov Switching models.\
3.  **Assess Model Robustness** --- Analyze model behavior during crises
    like the **2008 Global Financial Crisis** and the **2020 COVID-19
    Crash**.

##  Data Description

-   **Sources:** Yahoo Finance (via `yfinance` API)\
-   **Indices:** S&P 500 (USA), NASDAQ Composite (USA), Nifty 50
    (India)\
-   **Time Period:** January 1, 2000 -- July 20, 2025\
-   **Data Type:** Daily adjusted close prices, transformed into
    log-returns for stationarity.

Tests used:\
- **ADF test** --- confirms no unit root.\
- **KPSS test** --- fails to reject stationarity.

Result: all series are **stationary**, suitable for ARIMA/GARCH
modeling.

##  Methodology

### 1. Preprocessing

-   Convert prices to **log returns**.
-   Conduct **ACF** and **PACF** analyses for lag structure.
-   Test for **stationarity** using ADF and KPSS.

### 2. Modeling

-   Fit **ARIMA(p,d,q)** for mean dynamics (selected by AIC).
-   Model volatility using:
    -   **GARCH(p,q)**
    -   **EGARCH(p,q)** --- captures asymmetry and clustering.
    -   **GJR-GARCH(p,q,1)** --- tests for leverage effects.
-   Perform **Markov Switching Autoregression** to capture hidden
    regimes (2 states: high/low volatility).

### 3. Evaluation

-   **Rolling Forecasts** using 80% training, 20% testing.
-   Metrics:
    -   Mean Squared Error (MSE)
    -   QLIKE Loss
    -   Value-at-Risk (VaR) exceedance rate

Best performance was consistently achieved by **EGARCH** and
**GJR-GARCH** models.

##  Key Results

  Index      Model                MSE        QLIKE   VaR Exceedance
  ---------- ----------- ------------ ------------ ----------------
  S&P 500    GJR-GARCH     **0.6858**   **1.0538**           0.0649
  NASDAQ     GJR-GARCH     **1.1001**   **1.6814**           0.0700
  Nifty 50   EGARCH        **0.4396**   **0.6640**           0.0535

-   Asymmetric models (EGARCH, GJR-GARCH) outperform symmetric GARCH.
-   Regime probabilities from MS-AR align with market stress periods.

##  Insights

-   **Leverage effects** confirmed: negative shocks amplify volatility
    more than positive ones.\
-   **Crisis Detection:** Regime-switching probabilities surged during
    2008--2009 and 2020 crises.\
-   **Complementary Modeling:** Combining GARCH-family and MS-AR
    provides a robust framework for identifying market stress regimes.

##  Conclusion

The study demonstrates that **asymmetric GARCH models** and **Markov
Switching** approaches together effectively forecast volatility and
detect market stress regimes. These tools can enhance risk management,
asset allocation, and regulatory monitoring.

##  Tools & Libraries

-   **Python 3.x**
-   Libraries: `pandas`, `numpy`, `yfinance`, `statsmodels`, `arch`,
    `matplotlib`, `seaborn`

##  Repository Structure

    FinanceProject/
    |
    |--- FinanceProjectReport.pdf        # Full technical report
    |--- FinanceProject.ipynb             # Project notebook
    |--- README.md                       # Project overview (this file)

##  Future Work

-   Extend regime detection to multi-state models (>3 regimes).\
-   Explore machine learning volatility forecasters (e.g., LSTM-GARCH
    hybrids).\
-   Apply framework to sectoral or cryptocurrency indices.