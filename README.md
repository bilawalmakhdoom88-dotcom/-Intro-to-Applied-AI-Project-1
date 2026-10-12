# Introduction to Applied AI — Project 1

A practical machine learning project focused on **customer churn prediction, model optimization, unsupervised learning, and interactive application development** using the Telco Customer Churn dataset.

This repository documents the work completed during **Week 3 and Week 4**, progressing from machine learning experimentation to an interactive customer churn risk prediction application.

## 📌 Project Overview

Customer churn occurs when customers discontinue a company's services. Predicting churn can help businesses identify customers who may be at risk and make informed customer-retention decisions.

This project uses machine learning to predict customer churn, evaluate and optimize predictive models, explore customer segments, and integrate a trained model into a Streamlit application.

## 🎯 Project Objectives

- Analyze customer data and identify patterns associated with churn.
- Compare machine learning algorithms using cross-validation.
- Optimize model performance through hyperparameter tuning.
- Apply K-Means clustering and Principal Component Analysis (PCA).
- Select and evaluate a final predictive model.
- Save the trained model for reuse.
- Develop an interactive application for individual and batch churn-risk prediction.

---

# 📘 Week 3 — Model Optimization and Unsupervised Learning

## Overview

Week 3 focuses on improving machine learning models and exploring customer data using both supervised and unsupervised learning techniques.

The Telco Customer Churn dataset was used to compare predictive models, investigate performance variations, optimize hyperparameters, and identify customer segments.

## Key Activities

### 1. Data Preprocessing

- Converted `TotalCharges` into numeric format.
- Handled missing values.
- Converted the target variable into binary form: `0` for no churn and `1` for churn.
- Applied one-hot encoding to categorical features.
- Removed `customerID` because it does not provide useful predictive information.

### 2. Train-Test Split and Split Noise Analysis

The dataset was split into training and testing sets using stratification to preserve the approximate churn-class proportions.

Different random seeds were evaluated to examine the effect of data splitting on model performance.

**Observed Results:**

- Minimum accuracy: 0.780
- Maximum accuracy: 0.828
- Standard deviation: 0.0104

This experiment demonstrated why evaluating a model using only one random split can produce an incomplete picture of its performance.

### 3. Cross-Validation

Stratified 5-Fold Cross-Validation was used to obtain more reliable model-performance estimates.

Evaluation metrics included:

- ROC-AUC
- Accuracy
- Precision
- Recall
- F1-score

Cross-validation helped compare models more consistently while reducing reliance on a single validation split.

### 4. Model Comparison and Hyperparameter Tuning

The following algorithms and optimization methods were explored:

- **Logistic Regression:** Used as a baseline classifier, with the regularization parameter tuned.
- **Random Forest:** Optimized using randomized hyperparameter search.
- **XGBoost:** Tuned using randomized search, with early stopping used during experimentation to help control overfitting.

### 5. Model Comparison Results

| Model | Mean CV AUC | CV Standard Deviation |
|---|---:|---:|
| Tuned Logistic Regression | 0.8464 | 0.0129 |
| Random Forest — Random Search | 0.8464 | 0.0114 |
| Tuned XGBoost | 0.8502 | 0.0117 |

**Selected Model: XGBoost**

XGBoost achieved the highest mean cross-validation AUC of **0.8502** among the models listed above.

The model was selected using cross-validation results rather than the test-set score.

### 6. K-Means Customer Segmentation

K-Means clustering was applied to explore groups of customers with similar characteristics.

Selected features included tenure, monthly charges, total charges, and number of services. Feature standardization was used to account for differences in feature scales.

The Elbow Method and Silhouette Score were considered when selecting the number of clusters.

### 7. Principal Component Analysis (PCA)

PCA was applied to reduce the dimensionality of the dataset while retaining important information.

The dataset contained 30 features, and **15 principal components were required to explain at least 90% of the total variance**.

### Week 3 Key Learnings

- Why a single train-test split can be unreliable.
- How Stratified K-Fold Cross-Validation works.
- How to compare classification models using ROC-AUC.
- How hyperparameter tuning can improve model performance.
- How XGBoost and Random Forest approach classification.
- How K-Means can support customer segmentation.
- How PCA reduces dimensionality.
- Why the test set should remain separate from model selection.

---

# 🚀 Week 4 — Model Deployment and Interactive Churn Risk Prediction

## Overview

Week 4 focuses on putting a trained machine learning model into practical use through a Streamlit application.

The saved model is integrated with a user interface that allows users to enter customer information, estimate churn probability, adjust the decision threshold, and score multiple customers from a CSV file.

## Key Activities

### 1. Saving and Loading the Model

The trained model is stored in `churn_model.joblib` and loaded by the application using Joblib.

Model information and prediction settings are stored in `model_meta.json`, allowing the application to access the model's metadata and expected feature columns.

### 2. Building the Streamlit Application

The application is developed in Python using Streamlit and provides an interactive interface for customer churn analysis.

### 3. Individual Customer Prediction

Users can enter customer details, including:

- Tenure
- Contract type
- Monthly charges
- Internet service
- Additional services
- Payment method
- Billing preferences
- Customer demographics

The application processes the selected information and estimates the customer's churn probability.

### 4. Churn Risk Assessment

The application converts the predicted probability into a risk category:

- **HIGH:** Probability meets or exceeds the selected threshold.
- **WATCH:** Probability is below the threshold but remains relatively close to it.
- **LOW:** Probability is below the watch range.

Users can adjust the decision threshold according to their analysis needs.

These categories are decision-support indicators, not guarantees of future customer behavior.

### 5. What-If Analysis

The application allows users to compare predicted churn probabilities under alternative customer settings.

Examples include changing the contract type, payment method, or technical-support status.

This helps users explore how the model's predictions change when customer attributes are modified. These comparisons represent learned associations, not guaranteed causal effects.

### 6. Batch Customer Scoring

The application also supports batch prediction:

1. Upload a CSV file containing the required Telco customer columns.
2. Validate the input columns.
3. Calculate churn probabilities for the provided customers.
4. Identify records above the selected contact threshold.
5. View the highest-risk customers.
6. Download the scored customer data as a CSV file.

### 7. Technologies Used in Week 4

- Python
- Streamlit
- Pandas
- NumPy
- Joblib
- Scikit-learn
- XGBoost

### Week 4 Key Learnings

- How to save and reuse a trained machine learning model.
- How to integrate model inference with a web interface.
- How to prepare input data in the correct feature format.
- How to display probability-based predictions.
- How to support batch prediction with CSV files.
- How to make machine learning results more accessible to users.
- Why model predictions should be interpreted with appropriate limitations.

---

## 🗂️ Repository Structure

```text
-Intro-to-Applied-AI-Project-1/
│
├── app.py
├── churn_model.joblib
├── model_meta.json
├── sample_customers.csv
├── week-3-model-optimization.ipynb
├── requirements.txt
├── .gitignore
└── README.md
```

### File Descriptions

- `app.py` — Streamlit interface for individual and batch churn-risk prediction.
- `churn_model.joblib` — Saved machine learning model.
- `model_meta.json` — Model metadata, feature-column definitions, and prediction settings.
- `sample_customers.csv` — Sample customer data for testing batch predictions.
- `week-3-model-optimization.ipynb` — Notebook documenting Week 3 experiments.
- `requirements.txt` — Python package dependencies.
- `README.md` — Project documentation.

## 🛠️ Installation and Usage

### Prerequisites

Install Python and Git before running the project.

### 1. Clone the Repository

```bash
git clone https://github.com/bilawalmakhdoom88-dotcom/-Intro-to-Applied-AI-Project-1.git
```

### 2. Navigate to the Project Directory

```bash
cd -Intro-to-Applied-AI-Project-1
```

### 3. Create a Virtual Environment

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

On macOS or Linux:

```bash
source venv/bin/activate
```

### 4. Install Dependencies

```bash
pip install -r requirements.txt
```

### 5. Launch the Application

```bash
streamlit run app.py
```

Open the local URL displayed in the terminal to use the application.

**Note:** Keep `app.py`, `churn_model.joblib`, and `model_meta.json` available in the expected locations. The application also requires the packages specified in `requirements.txt`.

## 📊 Model Information

The model metadata included in the repository reports the following evaluation values:

- Model: XGBoost Classifier
- Cross-validation AUC: 0.850
- Cross-validation AUC standard deviation: 0.014
- Test AUC: 0.848
- Dataset: IBM Telco Customer Churn, 7,043 customers

ROC-AUC measures how well a model distinguishes between customers who churn and those who do not. These values describe the stored model's reported evaluation and should not be interpreted as a guarantee of future performance.

## 🔮 Future Improvements

- Deploy the Streamlit application to a public hosting platform.
- Add visualizations for churn patterns and customer segments.
- Improve input validation and error handling.
- Add model explainability and feature-importance analysis.
- Monitor prediction performance on new customer data.
- Evaluate the model on different customer populations before applying it in other markets.

## 👨‍💻 Author

**Bilawal Makhdoom**

**Course:** Introduction to Applied AI  
**Project:** Project 1  
**Topics:** Machine Learning, Model Optimization, Unsupervised Learning, and Application Development

## 📄 Conclusion

This project demonstrates the progression from machine learning experimentation to a usable prediction application.

**Week 3** focuses on cross-validation, model optimization, customer segmentation, and dimensionality reduction. **Week 4** focuses on integrating a trained model into a Streamlit interface for individual and batch churn-risk predictions.

Together, these activities demonstrate practical applications of machine learning, model evaluation, and interactive AI development.
