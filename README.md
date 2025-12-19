# Applied Linear Regression Analysis of Global Mean Sea Level and Temperature Anomalies

This repository contains the full code and outputs for the STAT 5205 final project at Columbia University.
The project analyzes the relationship between **monthly Global Mean Sea Level (GMSL)** and **global temperature anomalies**, with a focus on robustness, seasonality, decade heterogeneity, and multicollinearity.


## Project Overview

We study the association between temperature anomalies and sea-level changes using multiple linear regression models on monthly climate data.
To ensure valid inference and robustness, the analysis incorporates:

* Long-run time trends
* Seasonal fixed effects (monthly dummies)
* Decade indicators and temperature–decade interaction terms
* HAC (Newey–West) standard errors to address serial correlation
* Ridge regression as a regularization-based robustness check under multicollinearity

All regression results and figures reported in the final paper are fully reproducible using this repository.


## Repository Structure

```
5205_final_proj/
├── data/
│   ├── co2_mm_mlo.csv                     # Monthly atmospheric CO2 concentration
│   ├── GLEAM_global_monthly_evaporation.csv
│   ├── Global_TAVG_monthly.txt            # Global temperature anomalies
│   ├── GMSL_TPJAOS_5.2.txt                # Global Mean Sea Level (altimetry)
│   └── data_process_eva.ipynb             # Evaporation data processing (NetCDF → monthly)
│
├── out/
│   ├── desc_stats_panelA.csv              # Descriptive statistics (Panel A)
│   ├── desc_stats_panelB.csv              # Descriptive statistics (Panel B)
│   ├── reg_A1_temp_hac.csv
│   ├── reg_A2_temp_trend_hac.csv
│   ├── reg_B1_temp_evap_hac.csv
│   ├── reg_B2_temp_evap_trend_hac.csv
│   ├── reg_B3_temp_evap_trend_monthFE_hac.csv
│   └── reg_B4_tempXdecade_evap_trend_monthFE_hac.csv
│
├── pic/
│   ├── fig1_gmsl_ts.png                   # GMSL time series
│   ├── fig2_temp_ts.png                   # Temperature anomaly time series
│   ├── fig3_evap_ts.png                   # Evaporation time series
│   ├── fig4_scatter_gmsl_temp.png         # GMSL vs temperature scatter
│   └── fig5_bubble_3vars.png              # Bubble plot by decade
│
├── main.ipynb                             # Main analysis notebook (EDA + regressions)
├── README.md
└── .gitignore
```

---

## Data Sources

All datasets are publicly available:

* **Global Mean Sea Level (GMSL)**
  NASA GSFC / PO.DAAC, TP/Jason v5.2 altimetry (GIA-corrected)

* **Global Temperature Anomalies**
  Berkeley Earth Global Land–Ocean Temperature Dataset

* **Atmospheric CO₂ Concentration**
  NOAA Global Monitoring Laboratory (monthly mean CO₂, Mauna Loa)

* **Global Evaporation**
  GLEAM v4.2b global land evaporation dataset
  (processed into a global monthly series in `data_process_eva.ipynb`)


## Methodology

### Regression Models

* Ordinary Least Squares (OLS)
* HAC / Newey–West standard errors (lag = 12)
* Progressive specifications:

  * Baseline temperature–GMSL regression
  * Addition of time trends
  * Seasonal fixed effects (monthly dummies)
  * Decade indicators
  * Temperature × decade interaction terms

### Hypothesis Testing

* Individual coefficient significance (HAC p-values)
* Joint Wald tests (HAC covariance) for:

  * Seasonal effects
  * Decade main effects
  * Temperature–decade interactions

### Diagnostics

Standard regression diagnostics are produced, including:

* Residuals vs fitted values
* Normal Q–Q plots
* Scale–location plots
* Leverage and Cook’s distance
* Residual autocorrelation (ACF)
* Added-variable plots

### Multicollinearity & Regularization

* Correlation matrix
* Variance Inflation Factors (VIF)
* Ridge regression with:

  * Standardized covariates
  * 5-fold cross-validation
  * Bootstrap stability analysis


## How to Run the Analysis

1. **Process evaporation data** (if needed):

   * Run `data/data_process_eva.ipynb`

2. **Run main analysis**:

   * Open and run `main.ipynb`
   * This notebook performs:

     * Data merging
     * EDA and figures
     * Regression estimation
     * HAC inference
     * Diagnostics
     * Ridge regression

3. **Outputs**:

   * Regression tables → `out/`
   * Figures → `pic/`


## Authors

* **Cheng Zhang**
* **Xinai Lu**
* **Jiawei Lu**
* **Guichen Zheng**

Department of Statistics, Columbia University


## Notes

This project is for **educational purposes only**.

Data sources retain their original licenses.
