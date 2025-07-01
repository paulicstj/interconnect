# 📡 Interconnect – Churn Prediction Project

## 🧠 Project Overview
Customer churn is a major challenge in the telecommunications industry. **Interconnect**, a telecom operator, aims to reduce churn by identifying at-risk customers early using machine learning.

This project focuses on building a classification model to **predict customer churn**, with **AUC-ROC** as the main evaluation metric. The model will allow the company to implement retention strategies like personalized plans or promotions.

---

## 🎯 Objective
Develop a machine learning model that predicts the probability of customer churn with high performance (minimum AUC-ROC > 0.75). The best-performing model will be considered for deployment in a real-world retention system.

---

## 🗺️ Project Plan

### 1. Data Exploration & Preprocessing
- Loaded and merged four datasets: `contract_df`, `internet_df`, `personal_df`, and `phone_df`, using `customer_id` as the key.
- Cleaned data:
  - Converted columns to `snake_case`.
  - Handled missing values (e.g., replaced missing services with `"No"`).
  - Created a new binary target variable `active_customer`.
- Final dataset: 7,043 rows × 21 columns.

---

### 2. Exploratory Data Analysis (EDA)
- **Churn distribution**: Clear class imbalance (most customers are active).
- **Contract type**: Month-to-month contracts have the highest churn rate.
- **Monthly Charges vs. Tenure**:
  - Customers with **high charges and short tenure** are more likely to churn.
- **EDA visuals**:
  - Bar plots for churn by contract/payment method.
  - Boxplots comparing charges across active vs. inactive users.

---

### 3. Data Preparation
- One-hot encoding for categorical variables.
- `customer_id`, `total_charges`, and `end_date` were removed to reduce noise.
- Dataset split into training/test sets (70:30).
- Class imbalance addressed using **SMOTE**.
- Scale-sensitive models used **StandardScaler**.

---

### 4. Model Training & Evaluation

| Model               | AUC-ROC | F1-Score (Churn) |
|---------------------|---------|------------------|
| Dummy Classifier    | 0.50    | 0.00             |
| Logistic Regression | 0.8001  | 0.57             |
| Random Forest       | 0.8178  | 0.60             |
| LightGBM            | 0.8250  | 0.60             |
| XGBoost             | 0.8205  | 0.58             |
| **CatBoost**        | **0.8332**  | **0.61**             |

📌 *CatBoost (with default parameters) was the top performer.*

---

## ✅ Final Conclusion

After extensive experimentation, **CatBoost** emerged as the best model for predicting customer churn at Interconnect. It achieved an **AUC-ROC of 0.8332** and an **F1 score of 0.61** for churned customers — exceeding the required threshold and outperforming other models.

Its ability to handle categorical features and deliver strong results without intensive tuning makes it ideal for practical deployment.

### 🔄 Recommendations
- Implement CatBoost in production as the core model for churn prediction.
- Integrate it with a system that:
  - Monitors churn probability scores.
  - Automatically triggers **retention offers or promotions** for high-risk customers.
- Continuously monitor model performance and retrain periodically to reflect evolving user behavior.

---
