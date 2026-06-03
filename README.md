# Stochastic Interest Rate Modelling: CIR Model
### Finance Club, IIT Roorkee — Open Projects 2026

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![Status](https://img.shields.io/badge/Status-Complete-green)
![R2](https://img.shields.io/badge/Out--of--Sample%20R²-0.893-brightgreen)

---

## Overview

This project implements, calibrates, and extends the **Cox-Ingersoll-Ross (CIR)**
stochastic short-rate model on real yield curve data. The core objective is to
reconstruct the full yield curve using only the 3-Month rate as input.

The CIR model describes the evolution of the instantaneous short rate via:
dr_t = κ(θ − r_t)dt + σ√r_t dW_t

where κ is mean reversion speed, θ is the long-run mean, σ is volatility,
and W_t is a standard Brownian motion.

---

## Results

| Model | Overall R² | R² 0.5Y | R² 0.75Y | R² 1.0Y | R² 2.0Y |
|---|---|---|---|---|---|
| Base CIR | **0.893** | 0.994 | 0.968 | 0.910 | 0.389 |
| CIR++ Flat Shift | 0.879 | 0.992 | 0.959 | 0.894 | 0.331 |
| CIR++ Maturity Shift | 0.836 | 0.978 | 0.908 | 0.775 | 0.372 |

**Key finding:** Base CIR generalises better out-of-sample than both extensions.
Shift corrections learned in a low-rate regime overcorrect in the high-rate inverted
curve environment of the test period — textbook regime-dependent overfitting.

---

## Calibrated Parameters

| Parameter | Value | Interpretation |
|---|---|---|
| κ (kappa) | 0.1658 | Mean reversion speed — half-life ≈ 4.2 years |
| θ (theta) | 0.0244 | Long-run mean rate ≈ 2.44% |
| σ (sigma) | 0.0006 | Low volatility — smooth curve fitting |
| Feller condition | ✓ Satisfied | Rates guaranteed strictly positive |

---

## Project Structure

cir-interest-rate-modelling/
│
├── data/
│   ├── train_data.csv          # 1,976 daily observations (2016-2024)
│   ├── test_data.csv           # 495 daily observations (2024+)
│   └── test_data_3M.csv        # 3M rate only — model input for prediction
│
├── notebooks/
│   └── CIR_Interest_Rate_Modelling.ipynb   # Full implementation
│
└── README.md

---

## Methodology

### A. Data Preprocessing
- 0 missing values, 0 outliers (3x IQR), 0 non-positive yields
- No cleaning interventions required — dataset mathematically viable as-is

### B. CIR Implementation and Calibration
- Closed-form bond pricing via A(t,T) and B(t,T) functions
- OLS calibration minimising squared errors across all maturities and dates
- Feller condition enforced as hard constraint during optimisation

### C. Prediction Challenge
- Only the 3M yield ingested per test day as proxy for instantaneous short rate
- Full yield curve (0.5Y–2Y) reconstructed from this single input
- Out-of-sample R² = 0.893 on held-out test set

### D. Extensions
- **CIR++ Flat Shift**: Daily φ calibrated to anchor model to observed 3M rate
- **CIR++ Maturity Shift**: Training residuals used as per-maturity correction terms
- Both extensions underperformed base CIR out-of-sample

### E. Critical Analysis
- 2Y maturity R² = 0.39: single-factor model cannot capture inverted curve dynamics
- κ = 0.167 implies 4.2-year shock half-life — highly persistent rate environment
- Extensions overfit to training regime, failing in structurally different test period

---

## How to Run

1. Clone this repository
2. Open `notebooks/CIR_Interest_Rate_Modelling.ipynb` in Google Colab
3. Upload the three CSV files from `data/` when prompted
4. Runtime → Run All

---

## Dependencies

pandas
numpy
matplotlib
scipy
scikit-learn

---

## References

- Cox, J.C., Ingersoll, J.E., Ross, S.A. (1985). *A Theory of the Term Structure of Interest Rates*. Econometrica.
- Brigo, D., Mercurio, F. (2006). *Interest Rate Models — Theory and Practice*. Springer.
- Longstaff, F.A., Schwartz, E.S. (1992). *Interest Rate Volatility and the Term Structure*. Journal of Finance.
- Duffie, D., Pan, J., Singleton, K. (2000). *Transform Analysis and Asset Pricing for Affine Jump-Diffusions*. Econometrica.
