
# Lab 3: Model Optimization and Unsupervised Learning

**Name:** Bilawal Makhdoom  
**Week:** 3  

---

## 1. Introduction

This lab focuses on improving machine learning models using model optimization, cross-validation, hyperparameter tuning, and unsupervised learning techniques.

The **Telco Customer Churn** dataset is used in this lab. The main goal is to predict whether a customer will leave the telecom service and to find useful customer segments.

---

## 2. Dataset

The Telco Customer Churn dataset contains information about telecom customers, including:

- Customer information
- Tenure
- Monthly charges
- Total charges
- Internet services
- Online security
- Technical support
- Streaming services
- Contract information
- Payment method
- Churn status

The target variable is:

**Churn**
- `Yes` → Customer leaves
- `No` → Customer stays

---

## 3. Objectives

The main objectives of this lab are:

1. Analyze the effect of different train-test splits.
2. Apply **Stratified 5-Fold Cross-Validation**.
3. Compare Logistic Regression and Random Forest.
4. Perform hyperparameter tuning.
5. Use XGBoost with early stopping.
6. Apply K-Means clustering for customer segmentation.
7. Apply PCA for dimensionality reduction.
8. Select the final model using Cross-Validation AUC.
9. Evaluate the final model on the test set only once.
10. Save the final trained model.

---

## 4. Data Preprocessing

The dataset was cleaned and prepared before model training.

The `TotalCharges` column was converted into numeric format and missing values were handled.

The target variable was converted into binary form:

- `0` = No Churn
- `1` = Churn

Categorical features were converted into numerical features using one-hot encoding.

The `customerID` column was removed because it does not provide useful predictive information.

---

## 5. Train-Test Split

The dataset was divided into training and testing sets.

A stratified split was used so that the proportion of churn and non-churn customers remains similar in both sets.

The test set was kept untouched during model selection and tuning.

---

## 6. Split Noise Analysis

Different random seeds were used to observe how much the model performance changes with different train-validation splits.

The results were:

- **Minimum accuracy:** 0.780
- **Maximum accuracy:** 0.828
- **Standard deviation:** 0.0104

This shows that model performance can change depending on how the data is split.

Therefore, using only one random split may give an unreliable comparison between models.

---

## 7. Stratified 5-Fold Cross-Validation

Stratified 5-Fold Cross-Validation was used to obtain more reliable model performance.

The dataset was divided into five folds while maintaining the class distribution.

The models were evaluated using:

- AUC
- Accuracy
- Recall
- Precision
- F1-score

Cross-validation provides a more reliable estimate of model performance than a single train-validation split.

---

## 8. Hyperparameter Tuning

Hyperparameter tuning was performed to improve model performance.

The following methods were used:

### Logistic Regression

The `C` parameter was tuned using a validation curve.

### Random Forest

Randomized Search was used to find better hyperparameters.

### XGBoost

XGBoost was tuned using Randomized Search and early stopping was used to reduce overfitting.

---

## 9. Final Model Comparison

The models were compared using their mean Cross-Validation AUC.

| Model | CV AUC | CV Std |
|---|---:|---:|
| LR (tuned C) | 0.8464 | 0.0129 |
| RF (random search) | 0.8464 | 0.0114 |
| XGBoost (tuned) | **0.8502** | 0.0117 |

### Final Winner

**XGBoost (tuned)** was selected as the final model because it achieved the highest mean CV AUC of **0.8502**.

The test score was **not** used to select the winner. The test set was kept untouched until the final evaluation.

---

## 10. K-Means Customer Segmentation

K-Means clustering was used to divide customers into different groups based on their characteristics.

The features included:

- Tenure
- Monthly Charges
- Total Charges
- Number of Services

The features were standardized before applying K-Means because they have different scales.

The Elbow Method and Silhouette Score were used to help select the number of clusters.

Customer segments can help a telecom company understand different types of customers and design suitable retention strategies.

---

## 11. PCA Analysis

Principal Component Analysis (PCA) was applied for dimensionality reduction.

The dataset originally contained **30 features**.

The PCA results showed:

**15 components out of 30 are required to explain 90% of the variance.**

The strongest PC1 loadings included:

- InternetService_No: 0.302
- OnlineSecurity_No internet service: 0.302
- TechSupport_No internet service: 0.302
- StreamingTV_No internet service: 0.302
- DeviceProtection_No internet service: 0.302
- OnlineBackup_No internet service: 0.302

These results indicate that several features contain related information.

PCA helps reduce the number of dimensions while keeping most of the important information.

---

## 12. Final Test Evaluation

After selecting the final model using Cross-Validation AUC, the untouched test set was used for final evaluation.

The test set was evaluated only once.

This provides a more honest estimate of how the final model may perform on unseen data.

---

## 13. Key Learnings

From this lab, I learned:

- Why a single train-test split can be unreliable.
- How Stratified K-Fold Cross-Validation works.
- How to compare models using CV AUC.
- How hyperparameter tuning improves model performance.
- How Randomized Search can be used for model optimization.
- How XGBoost uses boosting to improve predictions.
- Why feature scaling is important for K-Means.
- How K-Means can be used for customer segmentation.
- How PCA reduces dimensionality.
- Why the test set should remain untouched during model selection.
- How to select a final model based on Cross-Validation instead of test performance.

---

## 14. Conclusion

In this lab, different machine learning optimization and unsupervised learning techniques were applied to the Telco Customer Churn dataset.

Three optimized models were compared using Cross-Validation AUC. **XGBoost achieved the highest CV AUC of 0.8502**, so it was selected as the final model.

K-Means was used to identify customer segments, while PCA was used to reduce the dimensionality of the dataset.

Overall, this lab demonstrated how proper cross-validation, hyperparameter tuning, model selection, clustering, and dimensionality reduction can improve the machine learning workflow.

---

## 15. Final Model

**Selected Model:** XGBoost (tuned)  
**Mean CV AUC:** 0.8502  
**CV Standard Deviation:** 0.0117  

**Model selection was based on Cross-Validation AUC, not the test score.**
