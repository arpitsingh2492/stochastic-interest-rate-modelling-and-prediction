# Stochastic Interest Rate Modelling and Prediction

This repository contains an executable Jupyter Notebook implementation of the **Cox-Ingersoll-Ross (CIR)** stochastic interest rate model, calibrated to a real-world macroeconomic dataset of US Treasury yields.

The project demonstrates the end-to-end pipeline of quantitative finance modeling: from data engineering and regime filtering to model calibration, yield curve reconstruction, and critical analysis. It also extends the base model to the **CIR++ framework** using a deterministic shift, achieving an out-of-sample $R^2$ of over 92% across all maturities.

## 🚀 Key Features

1. **Robust Data Engineering Pipeline:**
   - Pre-processing of historical yield data, handling missing values via forward/backward filling.
   - Macroeconomic regime filtering (post-2021 hiking cycle).
   - Outlier detection and clipping using the Interquartile Range (IQR) method. Includes synthetic outlier injection to demonstrate the pipeline's robustness against data corruption (e.g., fat-finger errors).

2. **Base CIR Model Implementation (Object-Oriented):**
   - Formulation of the mean-reverting square-root diffusion process: $dr_t = \kappa(\theta - r_t)dt + \sigma\sqrt{r_t}dW_t$.
   - Mathematical viability verification (positivity, realistic bounds, mean-reversion, Feller condition).
   - Analytical closed-form zero-coupon bond pricing using Affine Term Structure theory.

3. **Global OLS Calibration:**
   - Optimisation using L-BFGS-B across the entire cross-sectional yield curve simultaneously to avoid localized overfitting.
   - Calibration sensitivity analysis using multiple random restarts.

4. **Yield Curve Reconstruction & Prediction:**
   - Reconstructing the entire unobserved yield curve (6M through 30Y) using strictly the 3-Month short rate proxy ($r_t$).
   - Rigorous out-of-sample residual analysis (heatmaps, Mean Absolute Error, systematically over/under-predicted tenors).

5. **CIR++ Extension (Brigo-Mercurio):**
   - Implementation of the CIR++ deterministic shift $\varphi(t)$ to perfectly fit the initial term structure.
   - Anchoring the shift to the most recent training observation to maximize predictive power in the current macroeconomic regime, resulting in a global out-of-sample $R^2$ of > 92%.

6. **Critical Analysis & Key Questions:**
   - The notebook embeds detailed answers to 9 critical quantitative modeling questions, covering Feller condition breakdowns, persistence of shocks, structural limitations, and comparisons with jump-diffusion and two-factor models.
   - Concludes with real-world trading implications (yield curve risk, hedging failures).

## 📂 Repository Structure

- `main.ipynb`: The primary executable Jupyter Notebook containing all code, analysis, and visualizations.
- `dataset/`: Contains the raw and pre-processed CSV datasets (Training Data, Test Data, and Test 3M short-rate proxy).

## ⚙️ How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/arpitsingh2492/stochastic-interest-rate-modelling-and-prediction.git
   ```
2. Install the required Python dependencies:
   ```bash
   pip install numpy pandas matplotlib scipy
   ```
3. Open and run the Jupyter Notebook:
   ```bash
   jupyter notebook main.ipynb
   ```

## 📊 Results Summary

- **Base CIR Out-of-Sample $R^2$:** ~91.36%
- **CIR++ Out-of-Sample $R^2$:** ~92.13%
- Both models successfully exceed the strict >85% evaluation criterion, with CIR++ structurally correcting persistent bias at the long end of the curve.
