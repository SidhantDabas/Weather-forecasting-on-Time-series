# Weather Forecasting with TimesFM and XGBoost

Applied machine learning research project benchmarking Google's TimesFM foundation model against XGBoost for multi-scale wind speed forecasting using proprietary meteorological data from MetService New Zealand.

This work was completed as part of a research collaboration between the University of Waikato and MetService New Zealand from May 2024 to January 2025. A paper based on this work was accepted as a PRICAI poster.

## Project Summary

This project evaluates whether a zero-shot time-series foundation model, TimesFM, can perform competitively against a trained XGBoost baseline for operational weather forecasting.

The forecasting target was wind speed. Models were evaluated across three temporal frequencies:

| Frequency | Dataset Size | Forecasting Task |
|---|---:|---|
| 10-minute | 797,135 rows | Short-horizon high-resolution wind forecasting |
| Hourly | 130,798 rows | Medium-horizon wind forecasting |
| 3-hourly | 43,595 rows | Longer-horizon wind forecasting |

The study used meteorological data from five New Zealand weather stations:

| Station ID | ICAO Code | Station Name | Location |
|---|---|---|---|
| 93439 | NZWNA | Wellington Aero | Wellington, New Zealand |
| 93110 | NZAAA | Auckland Aero | Auckland, New Zealand |
| 93831 | NZQNA | Queenstown Aero | Queenstown, New Zealand |
| 93781 | NZCHA | Christchurch Aero | Christchurch, New Zealand |
| 93245 | NZAPA | Taupo Airport AWS | Taupo, New Zealand |

## Key Results

TimesFM outperformed XGBoost in the evaluated experiments, especially for higher-resolution and longer-horizon forecasting.

| Model | Frequency | Horizon | MAE | MSE | R² | Runtime |
|---|---|---:|---:|---:|---:|---:|
| TimesFM | 10-min | 3 hrs | 1.74 | 5.35 | 0.75 | 96.76s |
| XGBoost | 10-min | 3 hrs | 2.63 | 13.14 | 0.74 | 786.48s |
| TimesFM | Hourly | 18 hrs | 1.96 | 7.01 | 0.70 | 11.82s |
| XGBoost | Hourly | 18 hrs | 2.88 | 13.96 | 0.71 | 240.70s |
| TimesFM | 3-Hourly | 18 hrs | 1.94 | 6.32 | 0.69 | 13.05s |
| XGBoost | 3-Hourly | 18 hrs | 3.72 | 23.34 | 0.58 | 46.41s |

Note: XGBoost timing includes training and inference. TimesFM timing is inference-only due to its zero-shot setup.

## Technical Workflow

### 1. Data Preprocessing

- Loaded NWP data from NetCDF files using `xarray`
- Merged observational and forecast datasets using a unified `valid_time` index
- Removed duplicate timestamps
- Retained latest WRF model runs
- Interpolated gaps under four hours
- Aligned data across 10-minute, hourly, and 3-hourly frequencies

### 2. Feature Engineering

- Converted temperature features to Kelvin
- Added topographic attributes including latitude, longitude, and elevation
- Added temporal features including hour-of-day and month
- Selected top 40 features using Random Forest importance, ALE plots, and PDP analysis

### 3. Modelling

Two modelling approaches were compared:

#### XGBoost Baseline

- Implemented using the Darts library
- Trained separately for each temporal frequency
- Used a context length of 30
- Evaluated using MAE, MSE, and R²

#### TimesFM Foundation Model

- Used Google's pretrained decoder-only time-series foundation model
- Evaluated in zero-shot mode
- Used context length of 512 and batch size of 64
- Tested hybrid configurations involving external regressors

### 4. Evaluation

Models were evaluated across:

- Temporal frequencies: 10-minute, hourly, 3-hourly
- Forecast horizons: up to 36 hours
- Error metrics: MAE, MSE, R²
- Runtime comparison
- Forecast-horizon stability

## Repository Structure

```text
.
├── README.md
├── environment_darts.yml
├── environment_timesfm.yml
├── notebooks/
│   ├── 1_Data_Preprocessing_Sample.ipynb
│   ├── 2_Feature_Selection_Sample.ipynb
│   ├── 3_XGB_10Min.ipynb
│   ├── 4_XGB_Hour.ipynb
│   ├── 5_XGB_3Hour.ipynb
│   ├── 6_TFM_10Min.ipynb
│   ├── 7_TFM_Hour.ipynb
│   ├── 8_TFM_3Hour.ipynb
│   └── 9_plots.ipynb
├── outputs/
│   ├── plots/
│   └── metrics/
└── paper/
    └── PRICAI_poster_paper.pdf
