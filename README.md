# TÜRKİYE ELECTRICITY DEMAND FORECASTING
This repository contains the full analytical workflow developed for a comprehensive electricity demand analysis and forecasting study for Türkiye. The project combines econometric modeling, time-series analysis, and diagnostic tools to examine demand dynamics at daily and hourly frequencies.

The analyses cover the years **2022, 2023, and 2024**. For reporting clarity and readability, **2022 is treated as the pilot year in the written report**, while the complete analyses for **2023 and 2024** are fully implemented and documented in this repository.

---

## Project Objectives

The main objectives of this study are:
- To analyze electricity demand behavior across different temporal resolutions (daily and hourly),
- To quantify calendar effects, particularly public holidays, on electricity consumption,
- To evaluate the robustness of econometric inference under heteroskedasticity and serial correlation,
- To assess the impact of extraordinary exogenous shocks (6 February 2023 earthquake) using Interrupted Time Series (ITS) analysis,
- To construct a reliable short-term forecasting framework using SARIMA models.

---

## Data Description

The project relies on official and institutional data sources, including:
- Hourly and daily electricity consumption data obtained from EPİAŞ and TEİAŞ,
- Calendar information (weekdays, weekends, public and religious holidays),
- Macroeconomic and industrial indicators (used in regression-based specifications),
- Time-indexed hourly series constructed by merging date and hour variables.

All datasets are processed to ensure temporal consistency, correct frequency alignment, and numerical stability.

---

## Methodological Framework

### 1. Exploratory Demand Analysis (2022–2024)

- Descriptive analysis of electricity demand by season (winter, spring, summer, autumn),
- Identification of weekday–weekend asymmetries,
- Examination of public holiday and religious festival effects,
- Visualization of demand patterns at daily and hourly frequencies.

Although all years are analyzed, **2022 is used as the illustrative year in the report** to preserve readability. Detailed outputs for **2023 and 2024** are provided in this repository.

---

### 2. Fixed Effects Regression – Holiday Effects (2022)

A fixed effects regression model is estimated to quantify the impact of public holidays on daily electricity consumption:
- Month fixed effects control for seasonal variation,
- Day-of-week fixed effects capture systematic weekly patterns,
- A continuous holiday intensity variable (`holiday_weight`) measures the magnitude of holiday effects.

To ensure valid inference:
- **HC1 heteroskedasticity-robust standard errors** are applied,
- The model is re-estimated using **Newey–West HAC standard errors** to account for serial correlation.

Residual diagnostics (ACF plots and residual time paths) provide empirical justification for the use of HAC estimators.

---

### 3. Interrupted Time Series (ITS) Analysis – 6 February 2023 Earthquake

An Interrupted Time Series (ITS) framework is used to assess whether the 6 February 2023 Kahramanmaraş earthquake introduced a detectable structural break in national electricity demand:
- Daily electricity consumption for 2023 is modeled,
- The intervention date is defined as 6 February 2023,
- The specification includes a linear time trend, an immediate level-shift indicator, and a post-event trend interaction.

The ITS analysis serves as a diagnostic tool to test for persistent aggregate-level impacts of a major exogenous shock.

---

### 4. Stationarity Diagnostics and SARIMA Modeling (Hourly Data – 2022)

For short-term forecasting, hourly electricity demand is modeled using SARIMA:

- Log-transformation is applied to stabilize variance,
- Stationarity is tested using the Augmented Dickey–Fuller (ADF) test,
- Seasonal differencing at a 24-hour period (D = 1, s = 24) is employed to remove daily cycles,
- ACF and PACF diagnostics guide AR and MA order selection,
- Seasonal orders (P, Q) are selected using AIC, BIC, and convergence criteria.

The final model specification is: SARIMA(1,0,q)(0,1,1)[24], where q ∈ {0,1}

### 5.  Key Results
Electricity demand in Türkiye exhibits strong and stable temporal structure.

Calendar effects, especially public holidays, have economically meaningful and statistically robust impacts.

Aggregate national demand shows high resilience to extraordinary shocks such as earthquakes.

Parsimonious SARIMA models capture hourly dynamics effectively without overfitting.

Robust and HAC standard errors are essential for valid inference in daily demand regressions.
