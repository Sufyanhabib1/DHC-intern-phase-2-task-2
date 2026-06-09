# DHC-intern-phase-2-task-2
Customer Churn Prediction Using Machine Learning
Project Overview

This project builds a machine learning model to predict whether a customer is likely to leave (churn) or stay with a company. The model uses customer information from a dataset and applies data preprocessing, feature engineering, hyperparameter tuning, and classification techniques to achieve accurate predictions.

The final trained model is saved as a reusable .pkl file for future deployment and predictions.

Objective

Predict customer churn using customer demographic and service-related information.

Target Variable:

Churn
Yes → Customer leaves
No → Customer stays
Technologies Used
Python
Pandas
Scikit-Learn
Joblib
Google Colab
Dataset Requirements

The dataset should be a CSV file containing customer information and must include:

Required Columns
Column	Description
customerID	Unique customer identifier
Churn	Target variable (Yes/No)

The dataset may also contain additional numerical and categorical features such as:

Gender
SeniorCitizen
Partner
Dependents
Tenure
InternetService
Contract
MonthlyCharges
TotalCharges
Machine Learning Workflow
1. Data Loading

The user uploads a CSV file through Google Colab.

uploaded = files.upload()
df = pd.read_csv(list(uploaded.keys())[0])
2. Target Encoding

The target variable is converted into binary values:

Original	Encoded
Yes	1
No	0
y = df["Churn"].map({"Yes": 1, "No": 0})
3. Feature Selection

The following columns are removed:

Churn (target variable)
customerID (identifier)
X = df.drop(["Churn", "customerID"], axis=1)
4. Train-Test Split

The dataset is divided into:

80% Training Data
20% Testing Data
train_test_split(
    X, y,
    test_size=0.2,
    random_state=42
)
5. Data Preprocessing

The dataset may contain:

Numerical Features

Examples:

Tenure
MonthlyCharges
TotalCharges

These features are standardized using:

StandardScaler()
Categorical Features

Examples:

Gender
Contract
InternetService

These features are encoded using:

OneHotEncoder()

Both transformations are combined using:

ColumnTransformer()
6. Model Building

A Random Forest Classifier is used for classification.

RandomForestClassifier()

Reasons for choosing Random Forest:

Handles categorical and numerical data well
Robust to overfitting
Good performance on churn prediction problems
Works well with mixed feature types
7. Hyperparameter Tuning

Grid Search with 3-fold Cross Validation is used to find the best model parameters.

Parameters tested:

{
    "model__n_estimators": [50, 100],
    "model__max_depth": [5, 10]
}

Cross-validation:

GridSearchCV(cv=3)
8. Model Evaluation

Performance metrics used:

Accuracy

Measures overall prediction correctness.

accuracy_score()
Classification Report

Provides:

Precision
Recall
F1-Score
Support
classification_report()
9. Model Saving

The best trained model is saved using Joblib.

joblib.dump(
    grid.best_estimator_,
    "churn_model.pkl"
)

Generated file:

churn_model.pkl
10. Model Download

The trained model is automatically downloaded in Google Colab.

files.download("churn_model.pkl")
Project Structure
Customer-Churn-Prediction/
│
├── customer_data.csv
├── churn_model.pkl
├── churn_prediction.ipynb
└── README.md
Output

The program displays:

Best hyperparameters
Model accuracy
Classification report

Example:

Best Parameters:
{'model__max_depth': 10,
 'model__n_estimators': 100}

Accuracy:
0.85

Classification Report:
              precision    recall    f1-score
Future Improvements
Handle class imbalance using SMOTE.
Try advanced models such as:
XGBoost
LightGBM
CatBoost
Add feature selection techniques.
Deploy the model using:
Flask
FastAPI
Streamlit
Build a web-based churn prediction dashboard.
