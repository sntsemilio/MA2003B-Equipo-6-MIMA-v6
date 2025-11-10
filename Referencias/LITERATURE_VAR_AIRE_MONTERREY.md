# Literature Review: Applications of Value-at-Risk (VaR) and Expected Shortfall (ES/CVaR) to Urban Air Pollution

## Overview

We conducted a targeted literature search for applications of **Value at Risk (VaR)**, **Expected Shortfall (ES/CVaR)**, and related quantile- and volatility-based risk models to urban air-pollution time series. Evidence includes direct VaR/CAViaR applications to PM10, and complementary volatility and extreme-value approaches used to characterize tail risk in pollutant series.

No study explicitly applying VaR/ES to air quality in **Latin America, Mexico, or Monterrey** was found in the retrieved evidence; however, the methodologies identified are transferable to these contexts.

---

## Key Evidence on VaR/CAViaR for Urban Air Pollution

### PM10 in Madrid (Spain)
An **extended CAViaR (quantile regression–based VaR)** model is proposed as an early-warning system for exceedances of legal standards.  
- Forecasts low-probability quantiles of next-day PM10 “returns.”  
- Incorporates meteorology via a covariate index.  
- Evaluated with out-of-sample backtesting.  
- **Extended CAViaR** outperformed standard CAViaR, EWMA (RiskMetrics), Gaussian GARCH(1,1), and hybrid GARCH + block-maxima EVT benchmark models.  
- A spatial extension coupling CAViaR with kriging was also proposed to map exceedance risk across Madrid.

### PM10 in Seoul (Korea)
A master’s thesis develops **one-step-ahead conditional VaR forecasts** for daily PM10 using ARMA models with both parametric (e.g., skew-t residuals) and semiparametric (CAViaR-style) quantile-regression approaches.  
- Backtesting includes unconditional and conditional coverage tests.  
- Empirical exceedance rates are reported in the original thesis.

---

## Complementary Risk-Modelling Approaches Relevant to Tail Events

### AQI Risk Transfer (Xi’an, China)
An actuarial framework for AQI options uses an expanded Ornstein–Uhlenbeck trend with AR–GARCH volatility and Esscher transform pricing.  
While not a VaR/ES application, it demonstrates integrating time-series volatility modelling for **air-quality risk management** and evaluation on hold-out data.

### PM10 Volatility and Forecasting
Seasonal long-memory models with GARCH volatility improve forecasts of daily PM10 and provide calibrated predictive intervals, evidencing heteroscedasticity and non-normality typical of air-pollution series. These serve as **building blocks for parametric VaR or ES estimation**.

---

## Implications for Latin America / Mexico / Monterrey

No urban Latin American or Mexican case studies explicitly applying VaR/ES/CAViaR to air pollution were found.  
However, frameworks from **Madrid** and **Seoul** provide **transferable templates** for future research in **Monterrey**:

1. Direct quantile regression (CAViaR) for exceedance-risk forecasting.  
2. Parametric/semiparametric VaR using ARMA(GARCH) residuals.  
3. Formal backtesting of VaR forecasts.  
4. Spatial extensions to map exceedance risk across cities.

### Recommended Workflow for a Monterrey Application

1. Build baseline ARIMA/SARIMA or SARFIMA models; test for heteroscedasticity.  
2. Fit GARCH/EGARCH models where volatility clustering is present.  
3. Implement CAViaR (e.g., SAV-CAViaR) with meteorological covariates to forecast next-day pollutant VaR.  
4. Backtest forecasts using UC/CC tests and compare to parametric VaR (GARCH+EVT) and EWMA benchmarks.  
5. Optionally, include spatial kriging for exceedance-risk mapping.

---

## Summary of Studies

| Study | Context ID(s) | City / Region | Pollutant(s) | Model | Key Findings |
|-------|----------------|----------------|----------------|----------------|----------------|
| **Sanchis-Marco et al. (2022)** | (1.1–1.3) | Madrid, Spain | PM10 | Extended CAViaR (SAV-CAViaR + meteorological index; spatial kriging) | Outperformed CAViaR, EWMA, GARCH, and hybrid GARCH+EVT models in backtesting. |
| **Heo (2016)** | (2.1–2.2) | Seoul, Korea | PM10 | ARMA residual-based VaR (skew-t) and quantile-regression (CAViaR-style) | Conditional VaR forecasts evaluated with UC/CC backtests; empirical exceedance rates reported. |
| **Liu et al. (2019)** | (3.1) | Xi’an, China | AQI | AR–GARCH volatility + Esscher transform | Used for actuarial AQI option pricing; validated on 2018 data. |
| **Reisen et al. (2013)** | (4.1) | Urban PM10 | PM10 | SARFIMA + GARCH(1,1) | Improved PM10 forecasts; predictive interval coverage ~93–94%. |
| **Wu & Kuo (2020)** | (1.4) | Kaohsiung–Pingtung, Taiwan | PM10, O3, NO2 | VARMA–EGARCH | Captured pollutant interdependence and asymmetric volatility. |

---

## Key Takeaways

- **Quantile-based VaR approaches (CAViaR)** effectively model air pollution exceedance risk.  
- **Volatility models (GARCH/EGARCH)** remain foundational for capturing heteroscedasticity in pollutant series.  
- **Hybrid GARCH+EVT** and **CAViaR** can complement each other for extreme pollution events.  
- **Empirical backtesting** (UC/CC) remains crucial for validating VaR forecast reliability.  
- The identified methods are **directly transferable** to Monterrey’s monitoring data for PM2.5/PM10/ozone.

---

## References

1. **Sanchis-Marco, L., Montero, J.-M., & Fernández-Avilés, G. (2022).** *An extended CAViaR model for early-warning of exceedances of the air pollution standards: The case of PM10 in the city of Madrid.* Atmospheric Pollution Research.  
2. **Heo, Y. (2016).** *VaR forecasting for PM10 data using time series models.* Master’s Thesis.  
3. **Liu, Z., Zhao, L., Wang, C., Yang, Y., Xue, J., Bo, X., Li, D., & Liu, D. (2019).** *An Actuarial Pricing Method for Air Quality Index Options.* International Journal of Environmental Research and Public Health.  
4. **Reisen, V. A., Sarnaglia, A. J. Q., Reis, N. C., Lévy-Leduc, C., & Santos, J. M. (2013).** *Modeling and forecasting daily average PM10 concentrations by a seasonal long-memory model with volatility.* Environmental Modelling & Software.

---

