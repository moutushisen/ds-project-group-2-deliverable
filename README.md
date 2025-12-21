---

## Project Motivation

Lake Mälaren is Sweden’s third-largest lake and provides drinking water for over **2 million people**.
Understanding **how water flows between different basins** is critical, as some basins receive polluted inflows while others serve as drinking water reservoirs.

Although a **physics-based hydrodynamic model** exists, it is:

* Computationally expensive
* Difficult to interpret in terms of driving factors

This project instead applies **statistical and machine-learning models** to:

* Predict flow across selected basin interfaces
* Identify the influence of **river inflow** and **meteorological conditions**
* Enable faster and more interpretable analysis

---

## Objectives

* Predict discharge across **selected interfaces (A, B, C)**
* Use **river inflow** and **meteorological data** as predictors
* Compare interpretable models with more complex approaches
* Preserve **time-series structure** and reproducibility

---

## Repository Structure

```text
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
```

---

## Data Description

### Hydrodynamic Target Data

* Generated from a **physics-based hydrodynamic model**
* Weekly averages from **2000–2024**
* Flow extracted across **9 interfaces**, grouped into **A, B, and C**

### Meteorological Data (`Meteo_csv/`)

* Wind speed, wind direction, precipitation, temperature
* Aggregated to **weekly resolution**
* A `month` feature is automatically extracted to model seasonality

### River Inflow Data (`Rivers_csv/`)

* Daily inflow data aggregated to weekly values
* Captures basin-specific hydrological forcing

---

## Modeling Approach

* **Linear Regression** (final selected model)
* **Decision Trees** (interpretable comparison)
* **Neural Networks** (performance comparison)
* **XGBoost** (R-based comparison)

Key design choices:

* Ordered **80/20 train–test split** (no shuffling)
* Multi-output regression for multiple interfaces
* Lagged precipitation features
* Focus on **interpretability vs. performance trade-off**

---

## Python Pipeline Usage

### Installation

```bash
pip install -r requirements.txt
```

### Training and Evaluation

```bash
python model.py \
  -d Rivers_csv \
  -m Meteo_csv \
  -s 0.8 \
  -i A,B,C
```

This will:

* Train a linear regression model
* Evaluate it on held-out test data
* Save models, predictions, and figures automatically

### Prediction Only

```bash
python model.py \
  -m Meteo_csv \
  -r Rivers_csv \
  -s 0
```

Uses a previously trained model to generate predictions.

---

## Outputs

### Models

```text
models/
└── linear_regression/
    ├── linear_regression.joblib
    └── colnames.txt
```

### Figures

```text
figures/
├── linear_regression_evaluation.png
└── linear_regression_prediction.png
```

### Predictions

```text
predictions/
└── linear_regression_predictions.csv
```

---

## Results Summary

* **Linear regression** achieved the best balance between performance and interpretability
* River inflow is the strongest predictor of inter-basin exchange
* Meteorological variables provide additional explanatory power
* More complex models did not outperform linear regression, given the dataset size

---

## Reproducibility

* All scripts are deterministic
* No manual steps required after configuration
* File-based inputs and outputs ensure traceability

---

## Course Context

This repository accompanies the project report:

**“Predicting Inter-Basin Exchange in Lake Mälaren”**
Uppsala University – Data Science
Authors: *Alberto Fernández Comesaña,Henrik Jonasson,Moutushi Sen*

---

## License

For academic and educational use only.

---

