# Housing Price Prediction

**Tools:** Python · Scikit-learn · Pandas · Matplotlib · Seaborn  
**Domain:** Real Estate · Regression Modeling  
**Type:** Supervised machine learning — regression

---

## Overview

This project predicts real estate prices in Sindian District, New Taipei City, Taiwan using historical transaction data. The dataset contains 414 property records with features covering location, age, proximity to transport, and nearby amenities.

The project follows a structured modeling approach — start with linear regression as a baseline, evaluate performance against a threshold (R² ≥ 0.85), and move to tree-based models if the linear model falls short. It also includes a deliberate step to handle outliers, which had a significant impact on test set performance.

---

## Dataset

| Property | Detail |
|---|---|
| Source | UCI ML Repository — Real Estate Valuation Dataset |
| Records | 414 |
| Target | House price per unit area |
| Features | 6 |

**Features:**
| Feature | Description |
|---|---|
| Transaction date | Year and month of sale |
| House age | Age of the property in years |
| Distance to nearest MRT | Distance in meters |
| Number of convenience stores | Count within walking distance |
| Latitude | Geographic coordinate |
| Longitude | Geographic coordinate |

---

## Methodology

### 1. Exploratory Data Analysis
- Correlation analysis revealed that distance to MRT has the strongest negative correlation with price — the further from public transport, the lower the price
- Number of convenience stores and latitude showed positive correlations
- House age and transaction date had minimal predictive value
- Target variable was roughly bell-shaped with a few high-price outliers

### 2. Baseline — Linear Regression

| Metric | Training | Test |
|---|---|---|
| R² | 0.565 | 0.657 |
| MSE | 81.57 | 59.52 |

Performance fell well below the 0.85 threshold, indicating the price-feature relationships are non-linear. This justified moving to ensemble methods.

### 3. Random Forest Regressor

| Metric | Training | Test (original) |
|---|---|---|
| R² | 0.955 | 0.720 |
| MSE | 8.40 | 48.59 |

Strong training performance but a notable gap to test — suggesting the model was being affected by outliers in the test data.

### 4. Gradient Boosting Regressor

| Metric | Training | Test (original) |
|---|---|---|
| R² | 0.934 | 0.675 |
| MSE | 12.46 | 56.55 |

Similar pattern — good training, moderate test performance.

### 5. Outlier Removal

Properties with prices above the 3rd quartile threshold were identified and removed from the training set. The cleaned dataset was then used to retrain both models.

**Impact on Random Forest (cleaned data):**

| Metric | Training | Test |
|---|---|---|
| R² | 0.952 | **0.835** |
| MSE | 8.34 | **28** |

This was the decisive improvement — test R² jumped from 0.720 to 0.835 after outlier removal.

---

## Results

**Best model: Random Forest on cleaned dataset**

| Metric | Value |
|---|---|
| Test R² | 0.835 |
| Test MSE | 24.42 |

**Sample predictions on 5 random test cases:**

| Actual Price | Predicted Price | % Error |
|---|---|---|
| 56.8 | 52.99 | 6.71% |
| 25.6 | 24.90 | 2.75% |
| 40.6 | 38.84 | 4.35% |
| 39.3 | 40.53 | 3.12% |
| 51.7 | 42.09 | 18.60% |

4 out of 5 predictions fell within a 7% error margin. The one outlier (18.6% error) was a high-value property — edge cases like these still present a challenge.

---

## Key Findings

1. MRT proximity is the strongest price driver — this is consistent with urban real estate behavior globally, not just Taiwan.
2. Linear models are insufficient for real estate pricing — the non-linear relationships between location features and price require ensemble approaches.
3. Outlier removal had a bigger impact than model selection — going from 0.720 to 0.835 R² was almost entirely due to cleaning the training data, not switching algorithms.
4. Feature importance from Random Forest confirmed that distance to MRT, latitude, and number of convenience stores were the top three predictors.

---

## Limitations

- 414 records is a small dataset — predictions on edge cases (very high or very low price properties) are less reliable
- The dataset is geographically limited to one district in New Taipei City
- Transaction date was dropped but could carry useful seasonality information
- Cross-validation was not applied to the final model — should be added for more robust evaluation
