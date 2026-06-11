# DataScience_MachineLearning----Forecasting----Sales-market-forecasting_project
# Multivariate Sales Forecasting using ARIMAX & SARIMAX

This repository contains an advanced time-series forecasting case study designed to predict monthly **Sales** performance by utilizing **Marketing Expense** as an exogenous regressor. Moving beyond simple univariate configurations, this project leverages **ARIMAX** (Autoregressive Integrated Moving Average with Exogenous Regressors) and **SARIMAX** (Seasonal ARIMAX) models to analyze how promotional spending behaviors directly impact future sales velocities over time.

---

## 📂 Dataset Repository & Properties

The model consumes historical monthly records linking commercial revenue outcomes with cross-channel marketing investments.

### Dataset Profile (`Sales-and-Marketing.csv`)
* **Attributes:**
  - `Time Period`: Monthly date identifier formatted as `Mon-YY` (e.g., `Jan-11`, `Feb-11`), mapped as the primary Datetime index.
  - `Sales`: Target dependent variable representing generated monthly unit revenue.
  - `Marketing Expense`: Independent exogenous variable tracking marketing investments.
* **Core Characteristics:** The dataset exhibits a strong linear relationship between marketing adjustments and sales output, paired with cyclic seasonal patterns that dictate non-stationary shifts across quarters.

---

## 🛠️ Data Engineering & Statistical Preprocessing

The exploratory and stabilization workflow built inside `Sales-and-Marketing_ARIMAX,SARIMAX.ipynb` includes:

1. **Classical Decomposition:** Decomposing the `Sales` series into explicit Trend, Seasonal, and Residual components via `statsmodels` to map annual recurring peaks.
2. **Stationarity Testing:** Running the **Augmented Dickey-Fuller (ADF)** test to check for unit roots. Transformations (Log/Square Root) and first-order regular differencing ($d=1$) are applied to stabilize baseline variance.
3. **Exogenous Feature Alignment:** Organizing and lagging `Marketing Expense` values to feed the regression matrix. This helps the model map delayed or compounding consumer reactions to marketing campaigns.

---

## 🤖 Modeling Framework & Architecture

The forecasting pipeline separates models based on seasonality configurations and the presence of external variables:

### 1. Baseline ARIMA (No Seasonality / No Exogenous Features)
* Utilizes regular differencing and autoregressive lags purely on historical sales. It serves as a benchmark but drops important marketing trends and seasonal cycles.

### 2. ARIMAX Model (With Exogenous Regressors)
* Combines classical ARIMA framework with an external regression component ($X$). Sales forecasts are calculated as a function of past errors, past sales values, and current marketing spend metrics.

### 3. SARIMAX Model (Seasonal + Exogenous Regressors)
* **Configuration:** The ultimate model deployed in this study. It introduces seasonal order components `(P, D, Q)s
