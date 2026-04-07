# Coffee Shop Revenue Analysis using Multiple Linear Regression

`Predict Revenue based on time, product category, and business drivers`

---

# Overview

> This is a Multiple Linear Regression Project with the goal to make model predictions that accurately will predict revenue based on factors like time period, product category, location of the store, and the day of the week. With also try to identify which factors that affects the model the most.

# Dataset

- **Source**: https://www.kaggle.com/datasets/ahmedabbas757/coffee-sales
- **Size**: 149116 Rows and 11 Columns
- **Target Variable**: "revenue" **($\text{transaction\_qty} \times \text{unit\_price}$)**
- **Features Variables**: "time_period" (morning, afternoon, nigth), "product_category", "store_location", "day_of_week"

# Tech Stack

- **Language**: Python
  - **Libraries**:
    - `pandas` (Dataframe and Dummy Variables)
    - `matplotlib` & `seaborn` (Visualization)
    - `scikit-learn` (Model Building & Evaluation)
    - `statsmodels` (Statistical & OLS Analysis)

# Workflow

1. **Exploratory Data Analysis (EDA)**: Check Statistics, Missing Values, and Info
2. **Feature Engineering**:
   - Create new "revenue" column **($\text{unit\_price} \times \text{qty}$)**
   - Split transaction time into period (morning, afternoon, and night)
   - Getting the day of the week from transaction date
3. **Aggregated Data**: Groups sales by time of day, product category, store location, and day of the week. Then calculates the total revenue for each group.
4. **Apply Base Model**:
   - Create Dummy Variables for the features
   - Use Multiple Linear Regression
   - 80/20 Split Data Training and Test
5. **Evaluation Metrics**:
   - $R^2$ Score
   - Adjusted $R^2$ Score
   - Coefficients
   - Variance Inflation Factor (VIF)

6. **Visualization**:
   - Actual vs Predicted
   - Residual Plot
7. **Apply Log Transformation Model**

# Key Results

## $R^2$ and $\text{Adjusted} \space R^2$

- **Base Model**:
  `R2:  0.7810559825110095 Adjusted R2: 0.7386797210615275`
- **Log Transformation Model**:
  `R2: 0.8648369528840075 Adjusted R2: 0.8386763631196219`

> In base model, **78%** of the Variance in Revenue is explain by the Features for the base and **86%** in Log Transformation Model. Adjusted $R^2$ for both model decreases, this indicates some of the features are statistically insignificant.

## Coefficients

- **Base Model**:
  - `product_category_Coffee` and `product_category_Tea` has the highest positive coefficient, meaning it contributes most to revenue
  - `morning` period is the time period that generates more revenue
  - `monday` and `wednesday` are the days of the week that generates more revenue
  - Rest of the features, have a negative coefficients which indicates they are associated with a decrease in revenue, holding other variables constant
- **Log Transformation Model**:
  - `product_category_Coffee` has the highest positive coefficient ($1.275$), implying approximately a 258% increase in (1 + revenue) per transaction
  - `product_category_Packaged Chocolate` has the largest negative coefficient ($−2.94$), suggesting that transactions in this category generate roughly 95% lower revenue per transaction, all else equal.

## Variance Inflation Factor (VIF)

> Low VIF values indicate that the features have little linear correlation with each other
> and do not violate the multicollinearity assumption in linear regression.

# OLS Assumptions

- Linearity: The model assumes a straight-line relationship between the features (like time period, product category, store location, and day) and revenue. Since we used one-hot encoding, this works fine.
- Exogeneity:
- Homoscedasticity: The base model violates homoscedasticity. After applying a log transformation, this improved, though there’s still a bit of unevenness for higher revenue values.
- No Autocorrelation: Each row represents a unique combination of factors, so they’re treated as independent. But because the data comes from time-based transactions, there might still be some hidden time-related patterns.
- No Multicollinearity: Low Variance Influence Factor (VIF) indicates that all features have low correlation score
