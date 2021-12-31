# Campaign Response Model
[![](https://img.shields.io/badge/-Classification-orange)](#) [![](https://img.shields.io/badge/-RFM-blue)](#) [![](https://img.shields.io/badge/-Python-green)](#) [![](https://img.shields.io/badge/-Logistic--Regression-orange)](#) [![](https://img.shields.io/badge/-XGBoost-orange)](#) [![](https://img.shields.io/badge/-SMOTE-blue)](#) [![](https://img.shields.io/badge/-GridsearchCV-orange)](#) [![](https://img.shields.io/badge/-Google--Colab-blue)](#)  
  
**Notebooks:** [Customers Segmentation](./03_Product_Recommendation.ipynb)  
**Google Colab:** [![Open In Collab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/KodchakornL/BADS7105-CRM-Analytics-Intelligence/blob/main/04%20Campaign%20Response%20Model/04_Campaign_Response_Model_Evaluate_by_Auctrain_Auctest.ipynb) 

## Dataset
A Retail-like dataset.There are 2 datasets: 
1. Retail_Data_Response dataset consisting of customer_id, response => Customer level 
2. Retail_Data_Transactions dataset consisting of customer_id, trans_date, tran_amount => Transaction level. The table doesn't have trans_id, so we use tran_date as an identifier instead. If we want these 2 tables to join together, we can't do it at different levels. We have to make it a Customer level so that we can combine them to get into the model.


# Step of Campaign Response Model
  
### 1.Explore data  
  
**1.1 EDA**  
  
![EDA](./01_EDA.png)  
  
  
  
**2.2 Cohort Analysis**  
  
![cohort](./02_cohort.png)  
  
  
  
## 2 Feature Engineering  
**2.1. Features**
  
* `recency` : the range from the last day that the customer arrived with the current day, representing *Recency* in RFM analysis.  
* `Frequency` : total distinct transactions over all 'active' , representing *Frequency* in RFM analysis.  
* `TotalSpend` : total spending over all 'active', representing *Monetary* in RFM analysis.  
* `Ticket_size` : total spending over all transactions, representing *Monetary* in RFM analysis.  
* `AOU` : See how long this customer has been a customer., representing *Tenure*.  
* `Conversion_rate` : percentage of visitors to your channel that complete a desired goal (a conversion) out of the total number of visitors., representing *conversion*.  
  
**Correlation**  
  
![corr](./03_corr.png)
  
**2. Evaluate models (1st Round)**

**2.1 Creating train and test dataset**
  
![split_train_test_dataset](./06_split_train_test_dataset.png)
  
  
  
**2.2 Use 'SMOTE' fix SMOTE (synthetic minority oversampling technique) is one of the most commonly used oversampling methods to solve the imbalance problem. It aims to balance class distribution by randomly increasing minority class examples by replicating them.**
  
![unbalanced](./04_unbalanced.png)  
  
![unbalanced](./05_unbalanced.png)  
  
![SMOTE](./07_SMOTE.png)  
  
  
  
**2.3  Model Selection**  
Comparison Model by **Accuracy score**  
    - LogisticRegression  
    - DecisionTreeClassifier  
    - KNeighborsClassifier  
    - RandomForestClassifier  
    - GradientBoostingClassifier  
    - XGBClassifier  
  
![model-selection](./08_model_selection.png)  
  
#### **RFM Dataset** 
  
![model-selection](./09_model_selection_rfm.png)  
  
  
![roc_rfm](./11_roc_rfm.png)  
  
  
#### **CLV Dataset** 
  
![model-selection](./10_model_selection_clv.png)

  
![roc_clv](./12_roc_clv.png)
  

  
##  3.Model XGBoost
#### **1. Before hyper parameter tunning**  
  
**RFM Dataset**  
AUC score training set = 0.7276  
AUC score test set = 0.7043  
  
![confusion_metrix_rfm](./13_confusion_metrix_rfm.png)  
  
**CLV Dataset**  
AUC score training set = 0.7276  
AUC score test set = 0.7043  
![confusion_metrix_clv](./14_confusion_metrix_clv.png)  
  
  
#### **2. Hyperparameter Tunning Model**  
Use GridSearchCV()  
  
#### **RFM  Dataset**  
AUC score training set = 0.7807
AUC score test set = 0.7201  
  
![Hyperparameter Tunning Model](./15_GridseachCV_rfm.png)  
  
![Hyperparameter Tunning Model](./16_GridseachCV_confusion_rfm.png)  
  
![Hyperparameter Tunning Model](./17_GridseachCV_roc_rfm.png)  
  
  
  
#### **CLV  Dataset**  
AUC score training set = 0.7886  
AUC score test set = 0.7436  
  
![Hyperparameter Tunning Model](./18_GridseachCV_clv.png)  
  
![Hyperparameter Tunning Model](./19_GridseachCV_confusion_clv.png)  
  
![Hyperparameter Tunning Model](./20_GridseachCV_roc_clv.png)  
  
  
## 4.Result
From the campaign response data, the results were obtained after the run model. Better results were obtained after using model selection and hyperparameter tuning to determine the best parameters and the AUC score was greatly improved.  
  
Targeting the most potential customers will help to maximize campaign’s ROI. To put it in numerical terms, if targeting the wrong customers can have a negative impact on reputation.
However, what is more interesting about this kind of problem is the imbalance between the positive responses versus the negative responses.in this problem, driving the models towards negative predictions, as a naive guess of all responses are negative will have a low error score. This is called the “imbalance class” problem.

  
  
