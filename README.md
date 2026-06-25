# 📊 Telco Customer Churn Prediction & Customer Segmentation

> An end-to-end Machine Learning project that predicts customer churn using a Random Forest Classifier and segments customers into actionable groups using K-Means Clustering.


## 📌 Project Overview

Customer churn is one of the biggest challenges faced by telecommunications companies. Acquiring a new customer is significantly more expensive than retaining an existing one, making churn prediction an essential business problem.

This project combines **Supervised Machine Learning** and **Unsupervised Learning** to:

- Predict whether a customer is likely to churn.
- Identify the most influential factors contributing to churn.
- Segment customers based on their behavior and churn probability.
- Generate meaningful business insights for targeted customer retention strategies.


## 🎯 Objectives

The primary objectives of this project are:

- Perform comprehensive Exploratory Data Analysis (EDA)
- Clean and preprocess raw telecom customer data
- Build a Random Forest Classification model for churn prediction
- Improve model performance using hyperparameter tuning
- Evaluate the model using multiple performance metrics
- Segment customers into meaningful clusters using K-Means Clustering
- Visualize insights that can support business decision-making


# 📂 Dataset

**Dataset:** `Telco_customer_churn.xlsx`

The dataset contains customer information such as:

- Customer demographics
- Subscription details
- Internet services
- Billing information
- Contract type
- Payment methods
- Customer tenure
- Monthly and total charges
- Customer Lifetime Value (CLTV)
- Churn information


# 📚 Project Workflow


Raw Dataset
      │
      ▼
Exploratory Data Analysis
      │
      ▼
Data Cleaning
      │
      ▼
Feature Engineering
      │
      ▼
One-Hot Encoding
      │
      ▼
Train-Test Split
      │
      ▼
Random Forest Model
      │
      ▼
Hyperparameter Tuning
      │
      ▼
Model Evaluation
      │
      ▼
Predict Churn Probability
      │
      ▼
Feature Scaling
      │
      ▼
K-Means Clustering
      │
      ▼
Customer Segmentation


# 🔍 Step 1: Exploratory Data Analysis (EDA)

Before building the model, extensive exploratory data analysis was performed to understand customer behavior and identify patterns.

## Data Inspection

The following checks were performed:

- Dataset shape
- Data types
- Missing values
- Duplicate records
- Statistical summary
- Target distribution

Example:

python
df.info()
df.describe()
df.isnull().sum()




## Distribution Analysis

Histograms were plotted for important numerical features such as:

- Tenure Months
- Monthly Charges

These helped understand:

- Customer distribution
- Skewness
- Outliers
- Spending behavior



## Box Plot Analysis

Box plots were used to compare churned and non-churned customers.

Features analyzed:

- Tenure Months
- Monthly Charges

Insights:

- Customers with lower tenure churn more frequently.
- Customers paying higher monthly charges are more likely to churn.


## Count Plot Analysis

Categorical variables were analyzed against churn.

Examples:

- Contract Type
- Internet Service
- Tech Support
- Online Security
- Payment Method

These plots revealed which customer groups have higher churn rates.


## Correlation Analysis

A correlation heatmap was generated for numerical variables.

Features included:

- Tenure Months
- Monthly Charges
- Total Charges
- Churn Value
- Churn Score
- CLTV

This helped identify relationships among numerical features.


## Bivariate Analysis

Cross-tabulation was performed using:

python
pd.crosstab()


Example:

- Contract vs Churn

This helped understand churn percentages for each contract type.


# 🧹 Step 2: Data Cleaning & Preprocessing

Proper preprocessing is crucial for improving model performance.


## Total Charges Conversion

The **Total Charges** column was originally stored as a string.

It was converted into numeric format:

`python
pd.to_numeric()


Rows with empty values occurred only for customers with zero tenure.

Instead of removing these records, missing values were replaced with **0**.



## Removing Irrelevant Columns

Several columns were removed because they either:

- did not contribute to prediction,
- caused data leakage,
- or contained unnecessary geographical information.

Dropped columns include:

- CustomerID
- Country
- State
- City
- Zip Code
- Latitude
- Longitude
- Lat Long
- Churn Label
- Churn Score
- CLTV
- Churn Reason

Removing leakage features ensures the model learns genuine customer behavior.


## One-Hot Encoding

Machine learning algorithms require numerical input.

Categorical columns were converted using:

python
pd.get_dummies()

with
python
drop_first=True

to avoid multicollinearity.


# 🤖 Step 3: Machine Learning Model

A **Random Forest Classifier** was selected because it:

- Handles nonlinear relationships
- Works well with mixed data
- Handles high-dimensional datasets
- Is robust against overfitting
- Provides feature importance


## Train-Test Split

The dataset was divided into:

- **80% Training**
- **20% Testing**

using

python
train_test_split()


This allows unbiased evaluation on unseen data.


## Initial Model Training

The Random Forest model was trained on the training dataset.

Example:

python
RandomForestClassifier()


Predictions were then generated for the testing dataset.



# ⚙ Step 4: Hyperparameter Tuning

To improve model performance, multiple combinations of parameters were tested.

Parameters tuned included:

- Number of Trees (`n_estimators`)
- Maximum Tree Depth (`max_depth`)

Each combination was evaluated using:

- Accuracy
- Precision
- Recall
- F1 Score

The best-performing configuration was selected.



## Handling Class Imbalance

Since churn datasets are often imbalanced, the model used:
python
class_weight='balanced'


This forces the model to pay equal attention to both churned and retained customers.


# 📈 Step 5: Model Evaluation

The final model was evaluated using multiple performance metrics.

## Accuracy

Measures overall prediction correctness.


## Precision

Measures how many predicted churn customers actually churned.


## Recall

Measures how many actual churn customers were successfully identified.


## F1 Score

Balances Precision and Recall.

Useful when dealing with imbalanced datasets.


## ROC-AUC Score

The Receiver Operating Characteristic (ROC) Curve evaluates the classifier across multiple thresholds.

The Area Under the Curve (AUC) measures how well the model distinguishes between churned and retained customers.

Higher AUC indicates better performance.


## Cross Validation

To ensure model generalization:

- 5-Fold Cross Validation was performed.

This provides a more reliable estimate of model performance compared to a single train-test split.

# 📊 Step 6: Customer Segmentation

After predicting churn probability, customers were grouped into meaningful business segments.


## Feature Selection

The following features were selected:

- Tenure Months
- Monthly Charges
- Total Charges
- Predicted Churn Probability

These variables capture both customer value and churn risk.

## Feature Scaling

Since K-Means relies on Euclidean distance, all features were standardized using:

python
StandardScaler()

This prevents variables with larger ranges from dominating clustering.

## Choosing the Number of Clusters

The **Elbow Method** was used.

Within Cluster Sum of Squares (WCSS) was plotted against different values of **K**.

The elbow appeared at:

K = 3


Hence, three customer segments were created.


## K-Means Clustering

K-Means clustering was applied using:

python
KMeans(n_clusters=3)


Each customer was assigned to one of the three clusters.


## Cluster Interpretation

Clusters were interpreted using their average values.

### 🟢 Budget Loyal Customers

Characteristics:

- Long tenure
- Low monthly charges
- Low churn probability

Business Strategy:

- Reward loyalty
- Upsell premium services


### 🔴 High Risk New Customers

Characteristics:

- Low tenure
- High churn probability
- Moderate spending

Business Strategy:

- Retention campaigns
- Welcome offers
- Personalized discounts


### 🔵 Loyal Premium Customers

Characteristics:

- High monthly charges
- Long tenure
- High customer value

Business Strategy:

- VIP support
- Premium plans
- Exclusive rewards


# 📉 Visualizations

The project includes several visualizations to better understand customer behavior.

### Exploratory Analysis

- Histograms
- Count Plots
- Box Plots
- Correlation Heatmap

### Model Evaluation

- ROC Curve
- Performance Metrics

### Customer Segmentation

Scatter Plot:

- Tenure vs Monthly Charges

Scatter Plot:

- Total Charges vs Churn Probability

Clusters are color-coded for easy interpretation.


# 🛠 Technologies Used

| Category | Tools |
|----------|-------|
| Programming Language | Python |
| Data Processing | Pandas, NumPy |
| Visualization | Matplotlib, Seaborn |
| Machine Learning | Scikit-learn |
| Model | Random Forest Classifier |
| Clustering | K-Means |
| Model Evaluation | Accuracy, Precision, Recall, F1 Score, ROC-AUC, Cross Validation |
| Notebook | Google Colab / Jupyter Notebook |



# 📁 Project Structure


Telco-Customer-Churn/
│
├── Telco_customer_churn.xlsx
├── Customer_Churn_Prediction.ipynb
├── README.md
└── images/
      ├── churn_distribution.png
      ├── boxplot.png
      ├── correlation_heatmap.png
      ├── roc_curve.png
      ├── elbow_method.png
      └── customer_segments.png



# 🚀 Future Improvements

- Compare multiple machine learning models (XGBoost, LightGBM, CatBoost)
- Deploy the model using Streamlit or Flask
- Integrate SHAP for explainable AI
- Perform automated hyperparameter tuning using GridSearchCV
- Build a real-time churn prediction dashboard
- Add feature importance and business recommendation engine


# 💡 Business Impact

This project helps telecom companies:

- Identify customers at high risk of leaving
- Reduce customer churn
- Improve customer retention strategies
- Increase customer lifetime value
- Design personalized marketing campaigns
- Optimize business decision-making using data-driven insights

# 👩‍💻 Author

**Nagasri Karumuri**

If you found this project helpful, feel free to ⭐ the repository!
