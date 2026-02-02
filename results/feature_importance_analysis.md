
# Feature Importance Analysis: Random Forest vs Boosting (CatBoost)

This section addresses **Part 4 of the assignment**, which requires a deeper analysis of two non-linear models:
- **Random Forest (RF)**
- **A boosting model (CatBoost)**

The goal is to:
1. Show feature importance for each model
2. Compare the 10 most important features
3. Discuss similarities, differences, and economic interpretation

---

## 1. Feature Importance – Random Forest

Random Forest feature importance is based on **mean decrease in impurity**, reflecting how much each feature contributes to reducing prediction error across trees.

### Top 10 Random Forest Features

| Rank | Feature | Interpretation |
|----|-------------------------------|--------------------------------------------|
| 1 | estimated_revenue_l365d | Proxy for historical demand and pricing power |
| 2 | bedrooms*bathrooms | Capacity interaction effect |
| 3 | amenities_score*bathrooms | Quality–size interaction |
| 4 | distance_to_center | Location premium |
| 5 | amenities_score*bedrooms | Amenities scale with size |
| 6 | bedrooms*accommodates | Non-linear capacity effect |
| 7 | bathrooms | Core size attribute |
| 8 | maximum_nights | Pricing / regulatory constraint |
| 9 | distance_to_center*amenities_score | Amenities matter more in central locations |
|10 | distance_to_center*bathrooms | Size premium varies by location |

**Key insight:**  
Random Forest relies heavily on **explicitly engineered interaction terms**, indicating that non-linear relationships between size, amenities, and location are crucial for accurate pricing.

---

## 2. Feature Importance – CatBoost (Boosting Model)

CatBoost feature importance reflects the contribution of each feature to reducing the loss function during boosting iterations. Unlike Random Forest, CatBoost naturally handles categorical variables and captures interactions implicitly.

### Top 10 CatBoost Features

| Rank | Feature | Interpretation |
|----|-------------------------------|--------------------------------------------|
| 1 | estimated_revenue_l365d | Strongest indicator of demand persistence |
| 2 | estimated_occupancy_l365d | Utilization and market tightness |
| 3 | bedrooms*bathrooms | Capacity interaction |
| 4 | distance_to_center | Centrality premium |
| 5 | days_since_last_review | Listing activity and recency |
| 6 | maximum_nights | Stay constraints affecting price |
| 7 | beds*bedrooms | Size composition |
| 8 | neighbourhood_cleansed | Location heterogeneity |
| 9 | maximum_minimum_nights | Regulatory or host constraints |
|10 | reviews_per_month | Demand intensity signal |

**Key insight:**  
CatBoost assigns substantial importance to **demand dynamics, temporal activity, and categorical location effects**, reflecting its strength in modeling complex, structured data.

---

## 3. Comparison of Top Features

### Overlapping Important Features (Robust Drivers)

Both models consistently identify the following as key predictors:

- **estimated_revenue_l365d**
- **Capacity interactions** (e.g. bedrooms*bathrooms)
- **distance_to_center**
- **maximum_nights**

These variables represent **fundamental economic drivers** of Airbnb pricing: demand history, size, location, and booking constraints. Their importance across models suggests stable and robust effects.

### Differences in Emphasis

| Random Forest | CatBoost |
|--------------|----------|
| Emphasizes manual interaction terms | Emphasizes demand and activity variables |
| Importance spread across many features | Importance concentrated on fewer high-signal features |
| Limited role for review dynamics | Strong role for review timing and frequency |
| Requires explicit feature engineering | Learns interactions implicitly |

---

## 4. Discussion and Interpretation

The comparison reveals that while both models capture similar core pricing drivers, they do so in different ways. Random Forest benefits significantly from **explicit interaction terms**, whereas CatBoost captures complex patterns automatically, particularly in categorical and temporal dimensions.

This difference aligns with the horserace results: CatBoost achieves lower out-of-sample error, suggesting better generalization. The findings confirm that Airbnb prices are driven by a combination of **location, capacity, amenities, and demand persistence**, and that boosting models provide a more flexible representation of these relationships.

---

## 5. Conclusion

Feature importance analysis highlights strong agreement between Random Forest and CatBoost on the main economic drivers of Airbnb prices, while also revealing meaningful differences in how these models capture complexity. Boosting models appear better suited for this task due to their ability to handle non-linearities, interactions, and categorical structure more efficiently.
