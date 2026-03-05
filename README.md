# Quantitative Risk Management: Stylized Facts & Dependence Modeling

This repository provides a rigorous statistical framework for analyzing financial time series and modeling multivariate risk dependencies. Using a portfolio of **Apple (AAPL)**, **Meta (META)**, and **JPMorgan Chase (JPM)**, the project implements advanced econometrics to capture the "fat tails" and non-linear correlations inherent in equity markets.

## Project Overview
The project investigates the empirical failure of standard Normal distribution assumptions in risk management. By identifying stylized facts—such as volatility clustering and leptokurtosis—we implement a robust approach using **GARCH-filtered residuals** and **Copula-based dependence modeling** to accurately estimate extreme risk measures.

### Key Technical Features:
* **Automated Data Ingestion**: Historical adjusted closing prices are pulled directly from **Yahoo Finance** for all analyzed tickers.
* **Stylized Facts Analysis**: Empirical verification of heavy tails (leptokurtosis), gain/loss asymmetry, and the absence of linear autocorrelation in returns.
* **Marginal Modeling**: Returns are filtered using **GARCH(1,1)** models with Student-$t$ innovations to address volatility clustering and produce i.e. i.i.d. residuals.
* **Risk Measure Estimation**: Comparative analysis of **Value-at-Risk (VaR)** and **Expected Shortfall (ES)** using Parametric (Normal/Student-$t$), Non-Parametric (Historical Simulation), and Semi-Parametric (EVT) methods.
* **Multivariate Modeling**: Implementation of **Gaussian, Student-t, Clayton, and Gumbel Copulas** to model joint distributions and capture tail dependencies.

## Repository Structure

```text
├── analysis.ipynb    # Full Python implementation: data fetching, GARCH, and Copulas
├── report.pdf              # Theoretical report: derivations, proofs, and results analysis
├── requirements.txt        # Environment dependencies (arch, copulas, scipy, yfinance)
└── README.md               # Project documentation and summary
```
## Methodology

The analysis follows a structured pipeline to move from raw market data to multivariate risk assessment:

### 1. Exploratory Data Analysis (EDA)
* **Log-Return Analysis**: Quantitative analysis of log-returns to identify non-normal characteristics such as high kurtosis and negative skewness.
* **Aggregational Gaussianity**: Verification of "Aggregational Gaussianity," observing how return distributions approach normality as the time horizon increases.

### 2. Univariate Filtering
* **GARCH(1,1) Modeling**: Application of **GARCH(1,1)** models to account for conditional heteroskedasticity and remove temporal dependencies in volatility.
* **Residual Extraction**: Extraction of standardized residuals to ensure the data is independent and identically distributed (i.i.d.) before dependence modeling.

### 3. Probability Integral Transform (PIT)
* **Uniform Mapping**: Mapping the standardized residuals to uniform margins $U[0,1]$ using the cumulative distribution function (CDF).
* **Isolation of Structure**: This step isolates the dependency structure of the assets from their individual marginal distributions.

### 4. Dependence Modeling (Copulas)
* **Copula Fitting**: Fitting multiple Copula families (Gaussian, Student-$t$, and Archimedean) to the uniform margins.
* **Model Selection**: Selecting the optimal model based on **Log-Likelihood**, **AIC**, and **BIC** criteria to determine which structure best captures joint tail risks.

### 5. Risk Evaluation & Simulation
* **Portfolio Simulation**: Simulating joint portfolio returns to calculate 95% and 99% **VaR** and **Expected Shortfall**.
* **Comparative Analysis**: Comparing the accuracy of these risk metrics across different distributional assumptions to highlight the necessity of non-Gaussian models.



---

## Summary of Results

The analysis confirms that equity returns exhibit significant tail dependence that linear correlation fails to capture. Our findings show that **Archimedean copulas** (like Clayton) and the **Student-$t$ copula** provide a superior fit for this portfolio, as they account for the simultaneous extreme losses observed in historical data during "black swan" events.

---

**Authors:** Mahe Velay, Adélaïde Robert, Timothée POTTIÉ
**Date:** Fall 2025
