# In Progress - CONTACT FOR COLLOBORATION 

## Data Card and Dataset Information

### Dataset Source
Our dataset source is the [OpenMeteo API](https://archive-api.open-meteo.com/v1/archive), which provides comprehensive historical weather data. We have utilized both hourly and daily weather data, covering data from the present date back to the year 2000. The data is used to capture a variety of weather conditions at different resolutions for robust prediction and analysis.

### Data Card - Daily
| Variable Name             | Role     | Type   | Description                                     | Units | Missing Values |
|---------------------------|----------|--------|-------------------------------------------------|-------|----------------|
| date                      | Feature  | Date   | Date of observation                             | -     | No             |
| temperature_2m_max        | Feature  | Float  | Daily maximum temperature                       | °C    | No             |
| temperature_2m_min        | Feature  | Float  | Daily minimum temperature                       | °C    | No             |
| daylight_duration         | Feature  | Float  | Duration of daylight                            | Hours | Yes            |
| sunshine_duration         | Feature  | Float  | Duration of sunshine                            | Hours | Yes            |
| precipitation_sum         | Feature  | Float  | Total precipitation                             | mm    | No             |
| rain_sum                  | Feature  | Float  | Total rainfall                                  | mm    | No             |
| showers_sum               | Feature  | Float  | Total showers amount                            | mm    | Yes            |
| sunshine_ratio            | Feature  | Float  | Ratio of sunshine hours to daylight hours       | -     | Yes            |
| is_weekend                | Feature  | Binary | Whether the date falls on a weekend (0 = No, 1 = Yes) | -     | No             |
| is_hot_day                | Feature  | Binary | Whether it was a hot day (0 = No, 1 = Yes)      | -     | No             |
| is_cold_day               | Feature  | Binary | Whether it was a cold day (0 = No, 1 = Yes)     | -     | No             |
| is_rainy_day              | Feature  | Binary | Whether it was a rainy day (0 = No, 1 = Yes)    | -     | No             |
| is_heavy_precipitation    | Feature  | Binary | Whether there was heavy precipitation (0 = No, 1 = Yes) | -     | No             |

### Data Card - Hourly
| Variable Name             | Role     | Type       | Description                                     | Units  | Missing Values |
|---------------------------|----------|------------|-------------------------------------------------|--------|----------------|
| datetime                  | Feature  | DateTime   | Date and time of observation                    | -      | No             |
| temperature_2m            | Feature  | Float      | Hourly temperature at 2 meters                  | °C     | No             |
| relative_humidity_2m      | Feature  | Float      | Hourly relative humidity at 2 meters            | %      | No             |
| dew_point_2m              | Feature  | Float      | Hourly dew point temperature at 2 meters        | °C     | No             |
| precipitation             | Feature  | Float      | Hourly precipitation                            | mm     | No             |
| rain                      | Feature  | Float      | Hourly rainfall                                 | mm     | No             |
| snowfall                  | Feature  | Float      | Hourly snowfall                                 | mm     | No             |
| cloud_cover               | Feature  | Float      | Cloud cover percentage                          | %      | No             |
| wind_speed_10m            | Feature  | Float      | Wind speed at 10 meters                         | m/s    | No             |
| wind_direction_10m        | Feature  | Float      | Wind direction at 10 meters                     | Degrees| No             |
| is_day                    | Feature  | Binary     | Whether it is day (0 = No, 1 = Yes)             | -      | No             |
| is_freezing               | Feature  | Binary     | Whether it is freezing (0 = No, 1 = Yes)        | -      | No             |
| is_raining                | Feature  | Binary     | Whether it is raining (0 = No, 1 = Yes)         | -      | No             |
| is_snowing                | Feature  | Binary     | Whether it is snowing (0 = No, 1 = Yes)         | -      | No             |
| temp_rolling_mean_24h     | Feature  | Float      | 24-hour rolling mean temperature                | °C     | Yes            |
| precip_rolling_sum_24h    | Feature  | Float      | 24-hour rolling sum of precipitation            | mm     | Yes            |
| wind_category             | Feature  | Categorical| Wind category based on speed                    | -      | Yes            |

## Project Scope
[Project Scope Document](reports/Project_Scoping_Group_8.pdf)

## Git Repository Structure

```
├── LICENSE                <- Open-source license if one is chosen
├── Makefile               <- Makefile with convenience commands
├── pyproject.toml         <- Project configuration and package metadata
├── README.md              <- The top-level README for developers using this project
├── assets                 <- Contains subfolders for weather data, data plots, and data validation assets
│   ├── weather_data
│   │   ├── weather_data_daily_weather_data.csv
│   │   ├── weather_data_engineered_daily_data.csv
│   │   ├── weather_data_engineered_hourly_data.csv
│   │   ├── weather_data_hourly_weather_data.csv
│   │   ├── weather_data_preprocessed_daily_data.csv
│   │   └── weather_data_preprocessed_hourly_data.csv
│   ├── weather_data_plots
│   │   ├── Correlation Heatmap - Hourly Data.jpeg
│   │   ├── Correlation Heatmap - Daily Data.jpeg
│   │   ├── Distribution of Daily Maximum Temperature.jpeg
│   │   ├── Precipitation by Season.jpeg
│   │   └── Temperature and Precipitation Over Time.jpeg
│   └── weather_data_validation
│       ├── weather_data_validation_daily_schema.pkl
│       ├── weather_data_validation_daily_stats.pkl
│       ├── weather_data_validation_hourly_schema.pkl
│       └── weather_data_validation_hourly_stats.pkl
│
├── clima_smart            <- Core source code for the ClimaSmart project
│   ├── __init__.py
│   ├── config.py          <- Configuration variables
│   ├── dataset.py         <- Script for data loading and generation
│   ├── features.py        <- Script for feature engineering
│   ├── modeling
│   │   ├── __init__.py
│   │   ├── predict.py     <- Model prediction script
│   │   └── train.py       <- Model training script
│   └── plots.py           <- Script for data visualization
│
├── config                 <- Configuration files, including credentials
│   └── key.json           <- JSON key file for authentication (e.g., Google Cloud)
│
├── dags                   <- Directory for Airflow DAGs and utility scripts
│   ├── constants.py                          <- Defines constants used across DAGs
│   ├── daily_model_analysis.py               <- Daily model analysis script
│   ├── daily_model_development_dag.py        <- DAG for daily model development
│   ├── daily_model_training_v2.py            <- Daily model training script (version 2)
│   ├── daily_weather_data_collection_dag.py  <- DAG for daily weather data collection
│   ├── feature_engineering.py                <- Feature engineering script
│   ├── hourly_model_analysis.py              <- Hourly model analysis script
│   ├── hourly_model_development_dag.py       <- DAG for hourly model development
│   ├── hourly_model_training_v2.py           <- Hourly model training script (version 2)
│   ├── hourly_weather_data_collection_dag.py <- DAG for hourly weather data collection
│   ├── utils.py                              <- Utility functions for the DAGs
│   ├── weather_data_collection.py            <- Script to collect weather data
│   ├── weather_data_preprocessing.py         <- Script for data preprocessing
│   ├── weather_data_validation.py            <- Script for validating weather data
│   └── weather_forecasting_dag.py            <- DAG for weather forecasting
│
├── data                   <- Data folders for various stages (raw, processed, interim, external)
│   ├── external           <- Data from third-party sources
│   ├── interim            <- Intermediate data that has been transformed
│   ├── processed          <- The final, canonical data sets for modeling
│   ├── raw                <- The original, immutable data dump
│   └── daily_weather_data.csv.dvc <- Data Version Control file for tracking raw daily data
│
├── docs                   <- Documentation files
├── k8s-deployment.yaml <- Kubernetes deployment configuration
| ── k8s-service.yaml    <- Kubernetes service configuration
│
├── logs                   <- Logs generated by Airflow or other processes
│   ├── dag_id=daily_weather_data_pipeline
│   ├── dag_id=daily_weather_model_development_pipeline_v2
│   ├── dag_id=hourly_weather_data_pipeline
│   ├── dag_id=hourly_weather_model_development_pipeline_v2
│   ├── dag_id=weather_forecasting_pipeline
│   ├── dag_processor_manager
│   └── scheduler
│
├── mlruns                 <- MLflow tracking server and artifacts
│   ├── artifacts          <- Directory for MLflow artifacts
│   └── mlflow.db          <- SQLite database for MLflow metadata
│
├── models                 <- Serialized models and model-related files
│
├── notebooks              <- Jupyter notebooks for data exploration and prototyping
│
├── plugins                <- Custom Airflow plugins
│
├── references             <- Reference files or related documentation
│
├── reports                <- Generated analysis and visualizations for reporting
│   ├── figures            <- Figures used in reports
│   ├── data_collection_Group_8.pdf
│   ├── Data_Pipeline_Group8.pdf
│   ├── errors_failure_Group_8.pdf
│   ├── Project_Scoping_Group_8.pdf
│   └── user_needs_Group_8.pdf
│
├── scripts                <- Custom scripts for the project
│
├── streamlit              <- Streamlit web application for predictions
│   ├── app.py             <- Main Streamlit app
│   ├── app1.py            <- Additional Streamlit app version
│   ├── app_test.py        <- Test script for Streamlit app
│   ├── Dockerfile         <- Dockerfile for deploying Streamlit
│   └── requirements.txt   <- Dependencies for Streamlit
│
├── tests                  <- Unit and integration tests
│   ├── test_feature_engineering.py
│   ├── test_utils.py
│   ├── test_weather_data_collection.py
│   ├── test_weather_data_processing.py
│   └── test_weather_data_validation.py
│
├── weather_data           <- Weather data files
│
├── docker-compose.yaml    <- Docker configuration for containerized environments
├── Dockerfile.airflow     <- Dockerfile for Airflow deployment
├── Dockerfile.mlflow      <- Dockerfile for MLflow deployment
├── requirements.txt       <- List of dependencies for the environment
└── setup.cfg              <- Configuration for code style enforcement (flake8, etc.)
```

---

## Installation

This project requires **Python 3.8 or higher**. Please ensure that the correct version of Python is installed on your device. This project is compatible with Windows, Linux, and macOS.

### Prerequisites

- **Git**
- **Python** >= 3.8
- **Docker Daemon/Desktop** (Docker must be running)
---

# **Weather Forecasting Workflow**

This repository contains an end-to-end automated pipeline for weather forecasting using daily and hourly weather data. The workflow incorporates data collection, preprocessing, feature engineering, validation, model training, and analysis to provide robust predictions while ensuring data quality. The pipeline is orchestrated using **Apache Airflow** and relies on **Google Cloud Storage** for storing processed data, models, and analysis reports.

---

## **1. Data Collection**
### Overview
Our pipeline begins by fetching weather data from the Open-Meteo API. Both daily and hourly datasets are collected and stored in structured formats. 

We use **Airflow DAGs** to automate data collection, ensuring efficient scheduling and monitoring.

### Key Modules
- **`weather_data_collection.py`**:
  - `setup_session`: Configures a session with caching and retries for API robustness.
  - `fetch_daily_weather_data`: Fetches daily weather data.
  - `fetch_hourly_weather_data`: Fetches hourly weather data.
  - `process_daily_weather_data` and `process_hourly_weather_data`: Convert raw API responses into structured pandas DataFrames.

### Features Extracted
- **Daily Data**: Includes variables such as maximum and minimum temperatures, precipitation sums, sunshine duration, wind speeds, and evapotranspiration.
- **Hourly Data**: Includes temperature, humidity, precipitation, wind characteristics, and solar radiation metrics.

---

## **2. Data Cleaning and Preprocessing**
### Overview
High-quality data is crucial for accurate predictions. The preprocessing pipeline ensures the data is clean, consistent, and ready for feature engineering and modeling.

### Key Modules
- **`weather_data_preprocessing.py`**:
  - Handles missing values (e.g., interpolation for continuous variables, zero-filling for precipitation).
  - Removes outliers using the IQR method to prevent distorted model outputs.
  - Normalizes numerical columns for compatibility with machine learning models.
  - Adds time-based features like `season` and `is_weekend`.

---

## **3. Feature Engineering**
### Overview
Feature engineering enhances the predictive power of our models by transforming raw data into meaningful features.

### Key Modules
- **`feature_engineering.py`**:
  - **Daily Features**:
    - **Temperature Range**: Difference between max and min temperatures.
    - **Diurnal Temperature Range**: Captures daily temperature fluctuations.
    - **Sunshine Ratio**: Proportion of sunshine duration to total daylight duration.
    - **Precipitation Intensity**: Average precipitation per hour.
    - Binary flags for hot, cold, and rainy days.
  - **Hourly Features**:
    - **Rolling Averages**: Calculates rolling means for temperature and precipitation over 24 hours.
    - **Extreme Weather Flags**: Binary indicators for freezing, rain, and snow.
    - **Wind Chill and Heat Index**: Quantifies human-perceived temperature based on weather conditions.
    - Time-based features such as `hour` and `is_holiday`.

---

## **4. Data Validation**
### Overview
To ensure data reliability, custom validation checks are applied to the datasets. Validation ensures the data adheres to predefined quality standards and schemas.

### Key Modules
- **`weather_data_validation.py`**:
  - **Validation Checks**:
    - `test_no_nulls`: Ensures no missing values.
    - `test_positive_temperatures`: Validates temperature ranges.
    - `test_precipitation_non_negative`: Ensures precipitation values are non-negative.
  - **Schema Validation**: Compares schemas between daily and hourly datasets to ensure consistency.

---

## **5. Model Training**
### Overview
The pipeline uses **XGBoost** for training regression models on both daily and hourly datasets. The trained models are stored in `.json` format for easy deployment.

### Key Modules
- **Daily Model Training (`daily_model_training.py`)**:
  - Trains models using features such as `month`, `day_of_year`, and `week_of_year`.
  - Targets: `apparent_temperature_max`, `precipitation_sum`, etc.
  - Evaluates model performance using RMSE.
- **Hourly Model Training (`hourly_model_training.py`)**:
  - Trains models using hourly features such as `hour`, `month`, and `day_of_year`.
  - Targets: `apparent_temperature`, `precipitation`, etc.
  - Monitors model performance and triggers retraining if thresholds are exceeded.

---

## **6. Model Analysis**
### Overview
Comprehensive analysis ensures the models are unbiased and sensitive to feature variations.

### Key Modules
- **`daily_model_analysis.py` & `hourly_model_analysis.py`**:
  - **Bias Analysis**:
    - Compares predicted vs. actual values.
    - Computes MAE, RMSE, R², and average bias.
    - Saves scatter plots for bias visualization.
    ### Daily Bias Amalysis for Apparent Temperature Max and Precipitation Sum

    ### Hourly Bias Analysis for Apparent Temperature Max and Precipitation Sum


  - **Sensitivity Analysis**:
    - Perturbs key features (e.g., `month`, `hour`) to observe changes in predictions.
    - Outputs sensitivity metrics and visualizations as `.csv` and plots.

---

## **7 Working on Model-Deployment Pipelines (AIRFLOW) 
