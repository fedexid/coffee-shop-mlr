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
  - `monday` and `tuesday` are the days of the week that generates more revenue
  - Rest of the features, have a negative coefficients which indicates they are associated with a decrease in revenue, holding other variables constant
- **Log Transformation Model**:
  - `product_category_Coffee` has the highest positive coefficients with the value of $1.275342$. Because of `log1p` transformation, this means we can expect an increase in revenue by 2.58 units per transaction
  - `product_category_Packaged Chocolate` has the largest negative coefficient, with a value of $-2.939795$. Because of the `log1p` transformation, this means we can expect a decrease in revenue of approximately 0.95 units per transaction.

## Variance Inflation Factor (VIF)

> Low VIF values indicate that the features have little linear correlation with each other
> and do not violate the multicollinearity assumption in linear regression.

# OLS Assumptions

- Linearity: 
- Exogeneity:
- Homoscedasticity:
- No Autocorrelation:
- No Multicollinearity: Low Variance Influence Factor (VIF) indicates that all features have low correlation score
