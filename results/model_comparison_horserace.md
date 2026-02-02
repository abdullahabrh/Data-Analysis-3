
# Model Comparison and Horserace Results

This section presents a **horserace comparison** of five predictive models used to estimate Airbnb nightly prices:
- OLS (Linear Regression)
- LASSO
- Random Forest
- CatBoost
- XGBoost

Models are compared along two dimensions:
1. **Predictive performance** (fit)
2. **Computational cost** (training time)

The evaluation metrics are:
- **Train RMSE**
- **CV RMSE (5-fold cross-validation)**
- **Holdout RMSE** (out-of-sample performance)
- **Train R²**
- **Holdout R²**
- **Training Time (seconds)**

The holdout RMSE is the primary criterion for ranking models.

---

## Horserace Summary

| Model        | Train RMSE | CV RMSE | Holdout RMSE | Train R² | Holdout R² | Training Time (s) |
|-------------|-----------:|--------:|-------------:|---------:|-----------:|------------------:|
| XGBoost     | 10.16      | 48.97   | 56.18        | 0.99     | 0.62       | 35.36             |
| CatBoost    | 21.65      | 47.71   | 56.65        | 0.94     | 0.62       | 467.79            |
| RandomForest| 21.52      | 58.39   | 66.00        | 0.94     | 0.48       | 76.67             |
| OLS         | 59.31      | 61.43   | 72.69        | 0.52     | 0.37       | 0.14              |
| LASSO       | 59.53      | 61.37   | 73.04        | 0.51     | 0.36       | 97.74             |

Models are ranked by **Holdout RMSE (ascending)**.

---

## Performance Discussion

### Predictive Accuracy
Boosting-based models (XGBoost and CatBoost) clearly outperform all other approaches in terms of holdout RMSE. This indicates that Airbnb prices are driven by **non-linear relationships and complex feature interactions** that linear models struggle to capture.

- **XGBoost** achieves the lowest holdout RMSE (56.18), making it the best-performing model overall.
- **CatBoost** performs almost identically in terms of predictive accuracy, confirming the strength of boosting methods, especially when handling categorical variables.
- **Random Forest** performs reasonably well but is noticeably worse than boosting models, suggesting that boosting provides superior bias–variance trade-offs in this setting.

### Linear Benchmarks
- **OLS** serves as a baseline linear model and shows substantially higher holdout RMSE.
- **LASSO** performs similarly to OLS, indicating that regularization alone is insufficient to match the performance of non-linear models, despite mitigating multicollinearity.

These results suggest that linear structure is too restrictive for modeling Airbnb pricing dynamics.

### Overfitting and Generalization
- All tree-based models exhibit very low training RMSE relative to CV and holdout RMSE, indicating strong in-sample fit.
- The closeness of **CV RMSE and holdout RMSE** for XGBoost and CatBoost suggests good generalization and limited overfitting.
- Random Forest shows a larger gap between CV and holdout RMSE, consistent with mild overfitting.

### Computational Cost
- **OLS** is extremely fast to train but provides the weakest predictive performance.
- **XGBoost** achieves the best accuracy with moderate training time.
- **CatBoost**, while highly accurate, is significantly more computationally expensive, making it less attractive if frequent retraining is required.

This highlights a clear **trade-off between accuracy and computational efficiency**.

---

## Conclusion

Overall, boosting models dominate the horserace in terms of predictive accuracy. XGBoost offers the best balance between performance and training time, making it the preferred choice for a production pricing model. OLS and LASSO remain useful as interpretable benchmarks, but they are clearly outperformed by modern machine learning approaches in this application.
