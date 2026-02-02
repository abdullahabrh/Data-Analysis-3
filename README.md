# Assignment 1 – Airbnb Price Prediction  
**Course:** Data Analysis 3  

---

## 1. Business Case

The objective of this project is to develop a **pricing model for Airbnb listings** to support a firm operating a **portfolio of short-term rental properties**.  
Accurate pricing is essential to balance occupancy and revenue, and the goal is to evaluate different predictive models and assess their **robustness over time and across cities**.

---

## 2. Data

Data is sourced from **Inside Airbnb** and stored directly in this repository to ensure full reproducibility.

### Cities and periods used:
- **Vienna – March 2024** (training and test data)
- **Vienna – September 2024** (temporal validity test)
- **Munich – 2024** (geographic validity test)
- **Berlin – 2024** (additional geographic robustness check, optional)

All raw and cleaned datasets are stored in the `data/` folder.

---

## 3. Repository Structure

Assignment_1_Airbnb_Pricing/
├── data/
│ ├── vienna_raw_march.csv
│ ├── vienna_cleaned_march.csv
│ ├── vienna_raw_september.csv
│ ├── vienna_cleaned_september.csv
│ ├── munich_raw.csv
│ ├── munich_cleaned.csv
│ ├── berlin_raw.csv
│ └── berlin_cleaned.csv
│
├── notebooks/
│ ├── data_cleaning_vienna_march.ipynb
│ ├── data_cleaning_vienna_september.ipynb
│ ├── data_cleaning_munich.ipynb
│ ├── data_cleaning_berlin.ipynb
│ ├── models.ipynb
│ ├── validity_september.ipynb
│ ├── validity_munich.ipynb
│ └── validity_berlin.ipynb
│
├── results/
│ ├── model_comparison_horserace.md
│ └── feature_importance_analysis.md
│
├── README.md
└── requirements.txt


---

## 4. Part I – Modelling

### 4.1 Data Wrangling and Feature Engineering

The following steps are applied consistently across all datasets:

- Cleaning and extraction of amenities
- Imputation of missing values
- Creation of interaction terms
- Careful variable selection to mitigate multicollinearity
- Consistent preprocessing across time periods and cities

Implemented in:
- `data_cleaning_vienna_march.ipynb`
- `data_cleaning_vienna_september.ipynb`
- `data_cleaning_munich.ipynb`
- `data_cleaning_berlin.ipynb`

---

### 4.2 Predictive Models

Five predictive models are estimated using Vienna (March) data:

1. **OLS (Linear Regression)**
2. **LASSO**
3. **Random Forest**
4. **CatBoost**
5. **XGBoost**

Model estimation, hyperparameter tuning, and evaluation are implemented in:
- `models.ipynb`

---

### 4.3 Model Comparison (Horserace)

Models are compared using:

- Train RMSE
- Cross-validation RMSE
- Holdout RMSE
- R²
- Training time

Results and performance discussion are provided in:
- `results/model_comparison_horserace.md`

---

### 4.4 Model Interpretation

Feature importance is analyzed for:

- **Random Forest**
- **Boosting models (CatBoost and XGBoost)**

The top 10 most important features are compared to assess:
- nonlinear effects
- economic interpretability
- robustness of key predictors

Results and discussion are provided in:
- `results/feature_importance_analysis.md`

---

## 5. Part II – Model Validity

### 5.1 Temporal Validity

Models trained on **Vienna (March)** are evaluated on **Vienna (September)** to test stability over time.

Implemented in:
- `validity_september.ipynb`

---

### 5.2 Geographic Validity

Models trained on **Vienna** are evaluated on **Munich**, a different city in the same region, to test spatial generalization.

Implemented in:
- `validity_munich.ipynb`

An additional robustness check using **Berlin** is provided in:
- `validity_berlin.ipynb` (optional, not required for grading)

---

## 6. Reproducibility

This project is fully reproducible.

### To reproduce the analysis on a new machine:

```bash
git clone <repository_url>
cd Data-Analysis-3/Assignment_1_Airbnb_Pricing
pip install -r requirements.txt
