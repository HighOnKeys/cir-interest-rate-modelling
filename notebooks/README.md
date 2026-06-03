# Notebooks

## Main Notebook
`CIR_Interest_Rate_Modelling.ipynb` — Full implementation, calibration, extension, and analysis.

## How to Run
1. Open in Google Colab: [Click here](https://colab.research.google.com/)
2. Upload the three CSV files from the `data/` folder when prompted
3. Run all cells top to bottom (Runtime → Run All)

## Structure
| Section | Description |
|---|---|
| A. Data Preprocessing | Loading, cleaning, outlier detection, viability checks |
| B. CIR Implementation | SDE, bond pricing formula, OLS calibration |
| C. Prediction Challenge | Yield curve reconstruction from 3M rate alone |
| D. Extensions | CIR++ flat shift and maturity-specific shift |
| E. Critical Analysis | Model limitations, failure modes, regime analysis |
