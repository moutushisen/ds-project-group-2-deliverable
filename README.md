Predicting Inter-Basin Exchange in Lake Mälaren
This repository contains the code and data used for the Data Science course project, which involves predicting inter-basin water exchange in Lake Mälaren using data-driven models.
The project is part of the broader MEWS (Managing Events and Extremes in Water Supplies) initiative, aiming to provide a faster and more interpretable alternative to computationally expensive hydrodynamic simulations.


Project Motivation
Lake Mälaren is Sweden’s third-largest lake and provides drinking water for over 2 million people.
Understanding how water flows between different basins is crucial, as some basins receive polluted inflows while others serve as drinking water reservoirs.
While a physics-based hydrodynamic model exists, it is:

Computationally expensive
Hard to interpret in terms of driving factors
This project instead uses statistical and machine-learning models to:
Predict flow across selected basin interfaces
Identify how river inflow and meteorological conditions influence transport
Enable faster and more interpretable analysis

Objectives
Predict discharge across selected interfaces (A, B, C) between lake basins
Use river inflow and meteorological data as input features
Compare interpretable models (linear regression, decision trees) with more complex models
Preserve time-series structure and reproducibility

.
├── Meteo_csv/              # Meteorological input data (CSV)
├── Rivers_csv/             # River inflow input data (CSV)
├── Rivers_csv_old/         # Older / unused river CSV files
├── Python_csv/             # Intermediate CSVs used by Python models
│
├── model.py                # Main command-line entry point
├── _model.py               # Training, evaluation, and prediction logic
├── utils.py                # Data loading and preprocessing
├── const.py                # Global constants (paths, filenames)
├── requirements.txt        # Python dependencies
│
├── decision_tree_A.py      # Decision tree model (interface A)
├── neural_network_A.py     # Neural network model (interface A)
│
├── linear_regression_A.R   # Linear regression model (interface A)
├── linear_regression_B.R   # Linear regression model (interface B)
├── linear_regression_C.R   # Linear regression model (interface C)
├── xgboost_C.R             # XGBoost model (interface C)
│
├── time_series_model.R     # Time-series baseline models
├── meteo_average.R        # Meteorological data aggregation
├── river_average.R        # River inflow aggregation
├── flow_at_interface.R    # Flow extraction at basin interfaces
├── flow_at_coordinate.R   # Flow extraction at spatial coordinates
├── flux_interface.R       # Flux calculations across interfaces
│
└── README.md

Data Description
Hydrodynamic Target Data
Generated from a physics-based hydrodynamic model
Weekly averages from 2000–2024
Flow extracted across 9 interfaces grouped into A, B, and C

Meteorological Data (Meteo_csv/)
Variables such as wind speed, wind direction, precipitation, and temperature
Aggregated to weekly resolution
A month feature is automatically extracted for seasonality

River Inflow Data (Rivers_csv/)
Daily inflow data aggregated to weekly values
Used to capture basin-specific forcing

Modeling Approach
Linear Regression (final selected model)
Decision Trees (interpretable comparison)
Neural Networks (performance comparison)
XGBoost (R-based comparison)

Key design choices:
Ordered 80/20 train–test split (no shuffling)
Multi-output regression for multiple interfaces
Lagged precipitation features
Focus on interpretability vs. performance trade-off

Python Pipeline Usage
pip install -r requirements.txt

Training and Evaluation
python model.py \
  -d Rivers_csv \
  -m Meteo_csv \
  -s 0.8 \
  -i A, B, C
  
Trains a linear regression model
Evaluates on held-out test data
Saves model, predictions, and figures automatically

Prediction Only
python model.py \
  -m Meteo_csv \
  -r Rivers_csv \
  -s 0
Uses a previously trained model to generate predictions.

Outputs

models/
└── linear_regression/
    ├── linear_regression.joblib
    └── colnames.txt
Figures
figures/
├── linear_regression_evaluation.png
└── linear_regression_prediction.png
Predictions
predictions/
└── linear_regression_predictions.csv

Results Summary

Linear regression achieved the best balance between performance and interpretability
River inflow is the strongest predictor of inter-basin exchange
Meteorological variables contribute additional explanatory power
More complex models did not outperform linear regression, given the dataset size

Course Context

This repository accompanies the project report:
“Predicting Inter-Basin Exchange in Lake Mälaren”
Uppsala University – Data Science
Authors: Alberto Fernández Comesaña, Henrik Jonasson, Moutushi Sen

License
For academic and educational use only.
