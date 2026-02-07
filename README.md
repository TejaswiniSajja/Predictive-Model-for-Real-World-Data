# 📈 Retail Sales Prediction Using Machine Learning

## 🧠 Problem Understanding

The objective of this project is to **predict daily retail sales** using historical transaction data. Accurate sales forecasting helps retail businesses plan inventory, manage staffing, and evaluate overall business performance.

The original dataset contains **order-level records**, where each row represents an individual purchase. Since predicting sales at the order level is noisy and unnecessary for this task, the data is **aggregated to a daily level**. This allows the model to focus on overall sales trends rather than individual customer behavior.

The problem is framed as a **supervised regression task**, where:

- **Target variable**: total sales per day  
- **Input features**: calendar information, order statistics, and recent sales history  

Retail sales often show **temporal patterns** such as weekday vs weekend effects and short-term dependence on previous days’ sales. To capture this behavior, **time-based features and lag variables** are used.

A **time-aware train-test split** is applied to ensure that future data is never used to predict the past, preventing data leakage and better simulating real-world forecasting conditions.

The emphasis of this project is on **machine learning fundamentals**—clean data handling, appropriate feature engineering, correct validation strategy, and clear model reasoning—rather than achieving maximum prediction accuracy.

## 🔧 Model Pipeline Description

### Dataset Preparation
The dataset consists of **order-level retail transactions**, with one row per order containing order date, sales value, and customer/shipping details.  
To reduce noise and make the data suitable for forecasting, transactions are **aggregated to a daily level**, producing:

- **Total daily sales** (target variable)
- **Number of orders per day**
- **Average order value per day**

This aggregation enables stable, time-based modeling.

---

### Data Preprocessing
- The order date is converted to **datetime format**
- Data is **sorted chronologically** to preserve temporal order  

This prevents **data leakage**, ensuring future information does not influence past predictions.

---

### Feature Engineering
To capture sales behavior, the following features are created:

- **Day of the week** – captures weekly seasonality  
- **Weekend indicator** – distinguishes weekday vs weekend patterns  
- **Previous day’s sales (lag feature)** – captures short-term sales momentum  

Rows with missing lag values (initial days) are removed since they lack historical context.

---

### Train–Test Split
A **time-based split** is used instead of a random split:
- Earlier data is used for training
- Most recent data is used for testing  

This setup reflects real-world forecasting conditions.

---

### Model Selection
Two regression models are used for comparison:

- **Linear Regression**
  - Serves as a baseline model
  - Assumes linear relationships
  - Simple and interpretable

- **Random Forest Regressor**
  - Captures non-linear relationships
  - Uses an ensemble of decision trees
  - More flexible than Linear Regression

Both models are trained using the same features and data split.

---

### Evaluation Metrics
Model performance is evaluated using:

- **MAE (Mean Absolute Error)** – average daily prediction error (USD)
- **RMSE (Root Mean Squared Error)** – penalizes larger errors
- **R² Score** – proportion of variance in sales explained by the model

---

### Results & Interpretation

**Linear Regression**
- MAE: **$388.67**
- RMSE: **$613.90**
- R²: **0.659**

On average, Linear Regression predictions are off by approximately **$389 per day**, explaining about **66% of the variability** in daily sales.

**Random Forest Regressor**
- MAE: **$240.69**
- RMSE: **$500.26**
- R²: **0.774**

Random Forest reduces the average error to **~$241 per day** and explains about **77% of the variance**, indicating that retail sales exhibit **non-linear patterns** better captured by ensemble models.

---

### Key Observation
While Linear Regression provides a strong and interpretable baseline, Random Forest achieves better performance, suggesting that incorporating non-linear relationships improves sales prediction accuracy.
