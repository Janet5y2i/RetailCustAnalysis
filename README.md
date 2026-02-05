🛒 iFood Marketing Campaign Response Prediction
📌 Project Overview
This project aims to optimize the success rate of marketing campaigns for iFood, one of the leading food delivery platforms. By analyzing customer socio-demographic data and historical purchase behaviors, we built a classification model to predict whether a customer will respond to a new marketing offer.

Business Objective: Maximize the number of identified responders (maximizing Recall) to ensure that marketing efforts reach as many potential customers as possible under an ample budget scenario.

For the detail report, you can download the "iFood Marketing Prediction Model_Report.ppt" for your reference.


📂 Repository Structure
Plaintext
├── 01EDA.ipynb                     # Exploratory Data Analysis & Feature Engineering
├── 02Model_Catboost.ipynb           # Baseline CatBoost implementation
├── 02Model_Catboost_Ensemble.ipynb  # Final optimized Ensemble Undersampling approach
├── 02Model_RandomForest.ipynb       # Benchmarking with Random Forest
├── 02Model_XGBoost.ipynb            # Benchmarking with XGBoost
├── dataset/
│   ├── ifood_df.csv                # Original dataset
│   └── ifood_selected_columns.csv  # Cleaned & selected feature set
└── README.md
🛠️ Execution Process
1. Data Pre-processing (EDA)

Data Cleaning: Handled missing values (NaN) and infinity values (Inf) to ensure mathematical stability.

Feature Selection: Identified and removed highly correlated variables (e.g., redundant product spend categories) to address Multicollinearity.

Feature Engineering: Retained key drivers like Recency, MntWines, and AcceptedCmpOverall.

Transformations: Applied Log-transformation to skewed numerical features (e.g., Income) and performed Z-score normalization for scale consistency.

2. Model Selection

We compared multiple state-of-the-art algorithms:

Random Forest: Provided a solid baseline for tree-based performance.

XGBoost: Strong precision, but conservative in predicting the minority class.

CatBoost (Selected): Excelled in handling categorical features and provided the best Recall rate for our imbalanced dataset.

3. Optimization: Ensemble Undersampling

To tackle the class imbalance (approx. 1:6 ratio):

Strategy: The majority class (non-responders) was split into three distinct sets.

Training: Each set was paired with all minority samples (responders) to train three sub-models.

Aggregation: Final output was based on the averaged probability of these models, resulting in a more robust and stable prediction.

📊 Key Results
Metric    Score
AUC-ROC    above 0.9
Recall (Primary)    Highest among all models
F1-Score    Balanced for marketing outreach
Key Insights:

AcceptedCmpOverall: The strongest predictor; historical loyalty strongly correlates with future responses.

Recency: Customers with recent interactions are significantly more likely to engage.

Wines & Meat Spending: High spenders in specific categories show higher sensitivity to marketing campaigns.

🚀 How to Run
Clone this repository:

Bash
git clone https://github.com/your-username/retailcustanalysis.git
Install dependencies:

Bash
pip install catboost pandas numpy matplotlib seaborn scikit-learn
Run the notebooks in the following order:

01EDA.ipynb

02Model_Catboost_EnsebleUndersampling.ipynb

📈 Conclusion & Suggestions
For high-budget campaigns, we recommend using the CatBoost Ensemble model with a slightly lowered probability threshold to capture nearly all potential responders. This "high-sensitivity" approach ensures that iFood captures every possible conversion opportunity.
