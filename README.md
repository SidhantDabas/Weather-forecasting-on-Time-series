# Weather Forecasting with Foundational Models and XGBoost

## Abstract
Accurate weather forecasting is a critical component in various applications, from disaster preparedness to energy management. The growing interest in pre-trained foundational models, initially developed for language tasks, has led to the emergence of models such as TimesFM, a decoder-only time series foundational model. Designed for zero-shot forecasting, TimesFM promises faster results than traditional methods. This research investigates a private dataset provided by MetService New Zealand, comprising weather data from various stations across the country, to forecast wind speed at multiple temporal frequencies. XGBoost, a proven model for forecasting time series, serves as a baseline to create a comparative analysis between TimesFM and XGBoost. The study emphasizes adapting TimesFM to optimize its performance for meteorological forecasting, exploring what configurations work best for each data type. The findings highlight the potential and limitations of foundational models in weather prediction applications.

---

## Repository Structure

### Root Directory
- **`README.md`**: This file, providing an overview of the project.
- **`environment_darts.yml`**: An Anaconda environment file containing dependencies for XGBoost metrics calculation using Darts.
- **`environment_timesfm.yml`**: An Anaconda environment file containing dependencies for TimeSFM metrics calculation.

### Directories


#### 1. `notebooks/`
Contains modular Jupyter notebooks for each stage of the research.
- **`1_Data_Preprocessing_Sample.ipynb`**: Sample notebook for data cleaning, merging, and preprocessing steps using a subset of the dataset.
- **`2_Feature_Selection_Sample.ipynb`**: Sample notebook demonstrating feature selection techniques such as correlation analysis and feature importance.
- **`3_XGB_10Min.ipynb`**: Training and evaluation of XGBoost on data with frequency 10min.
- **`4_XGB_Hour.ipynb`**: Training and evaluation of XGBoost on data with frequency Hour.
- **`5_XGB_3Hour.ipynb`**: Training and evaluation of XGBoost on data with frequency 3hour.
- **`6_TFM_10Min.ipynb`**: Training and evaluation of TimesFM on data with frequency 10min.
- **`7_TFM_Hour.ipynb`**: Training and evaluation of TimesFM on data with frequency Hour.
- **`8_TFM_3Hour.ipynb`**: Training and evaluation of TimesFM on data with frequency 3hour.
- **`9_plots.ipynb`**: Generation of plots, including feature rankings, ALE/PDP plots, and model comparison visualizations.

#### 2. `Dataset`
Directory for dataset storage (not included). The dataset utilized in this study was provided by MetService, New Zealand. It contains meteorological data for five weather stations across New Zealand, listed in the table below:

| Station ID | ICAO Code | Station Name       | Location               |
|------------|-----------|--------------------|------------------------|
| 93439      | NZWNA     | Wellington Aero    | Wellington, New Zealand |
| 93110      | NZAAA     | Auckland Aero      | Auckland, New Zealand   |
| 93831      | NZQNA     | Queenstown Aero    | Queenstown, New Zealand |
| 93781      | NZCHA     | Christchurch Aero  | Christchurch, New Zealand |
| 93245      | NZAPA     | Taupo Airport Aws  | Taupo, New Zealand      |

#### 3. `outputs/`
- **`plots/`**: Generated plots (e.g., ALE/PDP plots, feature rankings, and performance visualizations).
- **`metrics/`**: Raw metrics files for each model and frequency, detailing RMSE, MAE, etc.

---

## Setup Instructions

Set up the environment:
   - For XGBoost:
     ```bash
     conda env create -f environment_darts.yml
     conda activate weather_forecasting
     ```
   - For TimesFM:
     ```bash
     conda env create -f environment_timesfm.yml
     conda activate Timesfm_clone
     ```

3. Open the notebooks:
   ```bash
   jupyter notebook
   ```

4. Follow the notebooks sequentially to reproduce the preprocessing, modeling, and results generation.

---

## Outputs
- **Feature Rankings**: Rankings of features based on importance scores.
- **ALE/PDP Plots**: Visualizations demonstrating the effect of specific features on predictions.
- **Model Comparison**: Plots and raw metrics comparing XGBoost and TimesFM performance.

---
