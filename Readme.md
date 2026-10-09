# Airline Passenger ARIMA Forecasting

ARIMA forecasting of airline passenger demand on the AirPassengers dataset (monthly airline passengers, 1949-1960): log transformation and differencing, ACF/PACF analysis, ARIMA(2,1,2) fitting with AIC/BIC, a 12-month forecast, and MAE/RMSE evaluation.

## Scenario
The goal is to build a forecasting model for airline passenger trends. Accurate demand forecasts help airlines optimize scheduling, pricing and resource allocation. This project builds on an earlier exploratory analysis of the same dataset, which found a trend and seasonality and showed the data was non-stationary, and uses the transformed data to fit an ARIMA model.

## Contents

| File | Description |
|---|---|
| `CG_C09_M04.ipynb` | Jupyter notebook with the full modeling workflow |
| `AirPassengers.csv` | Monthly passenger counts (`time`, `value`) |

## Workflow

0. Load the dataset and import libraries
1. Convert the data to a time series: monthly start (`MS`) datetime index, `value` renamed to `Passengers`
2. Apply a log transformation and first-order differencing, then plot ACF and PACF to guide the ARIMA parameters
3. Fit an ARIMA(2,1,2) model on the log-transformed series, compute AIC and BIC, and plot residual diagnostics
4. Forecast the next 12 months and convert the forecast back to the original scale
5. Evaluate in-sample performance with MAE and RMSE

## Results

| Metric | Value |
|---|---|
| AIC | -247.8 |
| BIC | -233.0 |
| MAE (original scale) | 24.3217 |
| RMSE (original scale) | 31.407 |

- The model is fit on log passengers, so the `d = 1` in ARIMA(2,1,2) handles the differencing, and forecasts are converted back with `np.exp()`.
- MAE and RMSE are computed on the original passenger scale. The first in-sample prediction is kept, and because the model has no history at that point it is far off and raises both errors.
- The series has strong yearly seasonality that a non-seasonal ARIMA does not capture. A seasonal model such as SARIMA would be the natural next step.

## Notes

- The `time` column is kept in the DataFrame after setting `Month` as the index