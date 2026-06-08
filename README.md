# Time Series Analysis: Construction Values & Food Industrial Production

A comprehensive time series analysis project applying the Box-Jenkins methodology to two monthly economic indicators.

---

## Project Overview

This project conducts a complete statistical analysis and modeling of two monthly economic time series:

- **Series 1**: Value of Real Estate Constructions (February 1982 – January 2015, 396 observations)
- **Series 2**: Industrial Production Index for Food Manufacturing (IPG311A2N) (January 1972 – March 2024, 627 observations) — sourced from the Federal Reserve Economic Data (FRED)

**Author:** Hajer Abdelkef  
**Date:** April 2026

---

## Objectives

For each time series, the analysis follows a rigorous three-phase methodology:

1. **Statistical & Graphical Analysis** — Descriptive statistics, visualizations, ACF/PACF, lag plots, and decomposition
2. **Trend & Seasonality Adjustment** — Polynomial regression and harmonic modeling (Fourier series)
3. **ARIMA Residual Modeling** — Stationarity tests (ADF, KPSS), differencing, ARIMA/SARIMA identification, and diagnostics
4. **Cross-Correlation Analysis (CCF)** — Relationship between the two series before and after removing deterministic components

---

## Data Sources

| Series | Source | Period | Frequency | Observations |
|--------|--------|--------|-----------|--------------|
| Construction Values | Internal dataset | Feb 1982 – Jan 2015 | Monthly | 396 |
| Food Industrial Production (IPG311A2N) | FRED (Federal Reserve) | Jan 1972 – Mar 2024 | Monthly | 627 |

---

## Methodology & Key Results

### Series 1: Real Estate Construction Values
- **Pattern**: Multiplicative model with a major structural break around 2002–2008 (Global Financial Crisis)
- **Trend**: Non-linear with sharp decline, recovery, crash, and slow rebound
- **Seasonality**: Strong annual seasonality (peak March–July, trough November–February)
- **Harmonic Model**: Reduced harmonic model with quadratic trend  
  `R² adjusted = 35.6%`
- **Residual Model**: `ARIMA(1,1,1)(0,1,1)[12]` — validated via Ljung-Box test (p=0.162)
- **Forecast**: 12-month ahead predictions with widening confidence intervals

### Series 2: Food Industrial Production
- **Pattern**: Additive model with stable, continuous upward trend (no structural break)
- **Trend**: Quadratic growth with slight deceleration post-2000
- **Seasonality**: Moderate but regular annual seasonality
- **Harmonic Model**: Reduced harmonic model with quadratic trend  
  `R² adjusted = 97.84%`
- **Residual Model**: `ARIMA(1,0,1)(1,0,1)[12]` — validated via Ljung-Box test (p=0.367)
- **COVID-19 Impact**: Notable outlier detected around 2020 in residuals

### Cross-Correlation Analysis
- **Raw Series**: Significant negative cross-correlation — the two sectors tend to move in opposite directions
- **Residuals (detrended & deseasonalized)**: Weak correlation, suggesting the observed inverse relationship is mostly driven by differing long-term trends rather than short-term interdependence
- **Exogenous Variable Test**: Adding Series 2 as an external regressor to Series 1's ARIMA model showed a non-significant coefficient (|t| &lt; 1.96), confirming weak direct predictive power

---

## Technologies & R Packages

The analysis is implemented in **R** and relies on the following packages:

```r
library(readxl)    # Excel data import
library(tidyverse) # Data manipulation & visualization
library(forecast)  # ARIMA modeling & forecasting
library(tseries)   # Stationarity tests (ADF, KPSS)
library(zoo)       # Irregular time series handling
library(xts)       # Extensible time series
library(ggplot2)   # Advanced plotting
library(gridExtra) # Multi-plot layouts
library(knitr)     # Formatted tables
```
## Repository structure
├── data/
│   ├── construction_values.xlsx          # Series 1 raw data
│   └── industrial_production_food.xlsx   # Series 2 raw data (FRED)
├── modelisation/
│   └── ProjectST.rmd                       # Main R analysis script
│   └── projetST.pdf                      # Full project report (French)
└── README.md                             # This file
## How to Run
1.Clone the repository and ensure R (>= 4.0) is installed
2.Install dependencies:
install.packages(c("readxl", "tidyverse", "forecast", "tseries", 
                   "zoo", "xts", "ggplot2", "gridExtra", "knitr"))
 3.Open modelisation/ProjectST.rmd and run sequentially:
Data import & ts/zoo/xts object creation
Phase 1: Exploratory analysis (plots, ACF, boxplots)
Phase 2: Harmonic regression & trend modeling
Phase 3: ARIMA residual modeling & forecasting
Phase 4: Cross-correlation analysis (CCF)
## Key Takeways 
| Aspect                     | Series 1 (Construction)     | Series 2 (Food Production) |
| -------------------------- | --------------------------- | -------------------------- |
| **Model Type**             | Multiplicative              | Additive                   |
| **Structural Break**       | Yes (2008 Crisis)           | No                         |
| **Trend**                  | Quadratic + Harmonic        | Quadratic + Harmonic       |
| **Explanatory Power (R²)** | 35.6%                       | 97.84%                     |
| **Residual Model**         | ARIMA(1,1,1)(0,1,1)\[12]    | ARIMA(1,0,1)(1,0,1)\[12]   |
| **Stationarity**           | Requires differencing (d=1) | Stationary residuals (d=0) |
## Citation
If you use this work, please reference:
Abdelkef, H. (2026). Analyse et Modélisation de Séries Temporelles : Valeur des Constructions Immobilières et Production Industrielle Alimentaire. Time Series Analysis Course Project.
## License
This project is provided for academic and educational purposes.
                  
                   
