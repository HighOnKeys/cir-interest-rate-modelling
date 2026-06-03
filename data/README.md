# Data

The dataset used in this project contains daily zero-coupon bond yields
across 9 maturities: 3M, 6M, 9M, 1Y, 2Y, 5Y, 10Y, 20Y, 30Y.

## Files
- `train_data.csv` — Training set: 1,976 daily observations (May 2016 — early 2024)
- `test_data.csv` — Test set: 495 daily observations (April 2024 onwards)
- `test_data_3M.csv` — Test set 3M rate only (model input for prediction challenge)

## Notes
- Yields are in decimal form (e.g. 0.05 = 5%)
- The underlying market/geography is intentionally undisclosed per project requirements
- Data was verified clean: no missing values, no outliers, no non-trading day anomalies
