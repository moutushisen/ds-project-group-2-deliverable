# Predicting Inter-Basin Exchange in Lake Mälaren
### Data Science Project – Group 2

This repository contains the final deliverable for the **Data Science** course project at **Uppsala University**.

The project predicts inter-basin water exchange in Lake Mälaren using data-driven models based on river inflow and meteorological data. The goal is to provide a faster and more interpretable alternative to physics-based hydrodynamic simulations used in the **MEWS** (Managing Events and Extremes in Water Supplies) project.

## 🎯 Objectives
* **Predict discharge** across basin interfaces A, B, and C.
* **Utilize multivariate inputs**, including river inflow and meteorological variables.
* **Compare model performance** between interpretable linear models and complex non-linear methods.
* **Ensure reproducibility** through a structured pipeline and preserved time-series data.

## 📁 Repository Structure
```text
.
├── Meteo_csv/              # Meteorological input data
├── Rivers_csv/             # River inflow data
├── Rivers_csv_old/         # Older / unused data
├── Python_csv/             # Intermediate processed CSVs
│
├── model.py                # Main Python pipeline (Command Line Interface)
├── _model.py               # Training, evaluation, and prediction logic
├── utils.py                # Data preprocessing and cleaning
├── const.py                # File paths and constants
├── requirements.txt        # Python dependencies
│
├── linear_regression_*.R   # Interface-specific R models
├── decision_tree_A.py      # Decision tree implementation (Interface A)
├── neural_network_A.py     # Neural network implementation (Interface A)
├── xgboost_C.R             # XGBoost implementation (Interface C)
│
└── README.md
