
# Predicting Dielectric Properties with Machine Learning

This project builds and evaluates machine learning models to predict the dielectric response of crystalline materials using the [`matbench_dielectric`](https://matbench.materialsproject.org) dataset from MatBench.

The work was completed as part of the *Machine Learning for Materials* course and focuses on feature engineering for crystal structures, model comparison, and benchmarking against state-of-the-art approaches on the MatBench leaderboard.

---

## Project structure

- `matbench_dielectric_project.ipynb`  
  Main Jupyter notebook containing the full workflow: data loading, feature engineering, model training, evaluation, and benchmarking.

- `requirements.txt`  
  Python dependencies used in the notebook.

---

## Dataset

- **Name:** `matbench_dielectric`
- **Source:** MatBench (materials ML benchmark suite)
- **Task:** Regression – predict components of the dielectric tensor of inorganic crystals from their atomic structure.
- **Access:** The dataset is loaded programmatically using `matminer.datasets.load_dataset` (no raw data files are stored in this repository).

---

## Methods

### Feature engineering

Feature engineering is performed using [`matminer`](https://hackingmaterials.lbl.gov/matminer/):

- **Composition-based features**
  - `ElementProperty` featuriser (statistics over elemental properties for each composition).

- **Structure-based features**
  - `SineCoulombMatrix` featuriser to encode inter-atomic interactions within the crystal structure.
    
Features are scaled using `MinMaxScaler` from `scikit-learn`.  
Additional checks and plots are used to investigate feature distributions and potential issues with data leakage or target leakage.

### Models

Several regression models from `scikit-learn` and `xgboost` are explored:

- **Support Vector Regression (SVR)**
- **Random Forest Regressor**
- **XGBoost Regressor**

Hyperparameters are tuned using `GridSearchCV` with cross-validation. The notebook records the best hyperparameters for each model and compares them.

---

## Evaluation

Model performance is evaluated using:

- Mean Absolute Error (MAE)
- Root Mean Squared Error (RMSE)
- Coefficient of determination (R²)

A 10-fold cross-validation scheme is used to estimate generalisation performance. The final chosen model (an SVR with a polynomial kernel) is trained on the full training set and evaluated on a held-out test set.

A comparison is also made with published MatBench leaderboard entries for `matbench_dielectric` to see where this workflow stands in relation to state-of-the-art models such as MODNet, GNNs, and other baselines.

---

## How to run
### How to Run
1. Clone the repo:
   ```bash
   git clone https://github.com/Suleyman040/Perovskite-ML-Classifier.git
