# Ecommerce Customer Churn

## Introduction

We have a dataset from a leaning E-Commerce company which does online retailing. Customers register to the site and do online shopping. Dataset is the sales/purchases done by online customers of the company. Various quantitative and qualitative factors that give us information about the customer behaviour is given. Using this information we are asked to present a model that gives the company an overall idea about what factors are influencing the customer churn and what measures can be taken to reduce the same. 

Customer churn is a concern for the company because potential sales from that customer is lost forever. In this project we study customer behaviour to try and understand why they churn. Then, understand and implement a strategy to reduce customer churn. 

Business opportunity here is to try and stop customer churn. E-Commerce customer may churn because of several reasons. Unavailability of products, cost of the product, fulfilment and delivery issues, customer support, etc. 

We analyse why the churn is happening, engage with the customer, give incentives/lucrative offers, define the target customer and see how we can keep the target customer.  

## Problem 

The main aim of the project is to determine the factors influencing customer churn and thereby coming up with efficient strategies to reduce the same. 
Customer churn is a concern for the company because potential sales from that customer is lost forever. In this project we study customer behaviour to try and understand why they churn. Then, understand and implement a strategy to reduce customer churn. 
Business opportunity here is to try and stop customer churn. E-Commerce customer may churn because of several reasons. Unavailability of products, cost of the product, fulfilment and delivery issues, customer support, etc. 
We analyse why the churn is happening, engage with the customer, give incentives/lucrative offers, define the target customer and see how we can keep the target customer.  

## Exploratory Data Analysis and Business Implication 
### a.	Understanding how data was collected in terms of time, frequency and methodology
Data seems to have been collected from a few different places technically. There is CustomerID, Tenure column which suggests that the data is taken from the database of web application. There we have how long the user was on the site. This seems to be taken from the web application session information. Then there is information on mobile app so that seems to be taken from the logs of Mobile application. 

Tenure is a number between 0 and 61. Tenue is how long the user is with the organization. With the assumption that E Commerce has not been around for 61 years now. It seems fair to assume that this is in months. 

WarehouseToHome is a number between 5 and 127. There is no mention of the units of this field. From data science analysis perspective of this data, the unit of this field does not matter much. It could be either Mile or Kms. We assume this data to be in Kms. 

Number of records in dataset is the same as unique count of CustomerID. This tells us that the data is per customer. There are columns in the dataset that talk about counts of last month and values since last year. This tells us that the data is not per month or year, but is a data snapshot taken at a particular point in time. At the time the data snapshot was taken, what were the various counts/values last year, last month, etc. 

### b.	Visual inspection of data (rows, columns, descriptive details)
We have 5630 rows of data and 20 columns. CustomerID field is not useful for our modelling. So, we can drop that. Churn is the dependent variable. 

Numeric fields are: 'Tenure', 'WarehouseToHome', 'HourSpendOnApp', 'NumberOfDeviceRegistered', 'SatisfactionScore', 'NumberOfAddress', 'Complain', 'OrderAmountHikeFromlastYear', 'CouponUsed', 'OrderCount', 'DaySinceLastOrder', 'CashbackAmount'

Categorical fields are: 'PreferredLoginDevice', 'CityTier', 'PreferredPaymentMode', 'Gender', 'PreferedOrderCat', 'MaritalStatus'


### c.	Understanding of attributes (variable info, renaming if required)
From data info, we see the list of fields that are objects and the list that are numeric. We also see that there are several null values in various fields



### d.	Univariate analysis (distribution and spread for every continuous attribute, distribution of data in categories for categorical ones)
Below table gives a detailed information on each continuous field. 

![Picture1](https://user-images.githubusercontent.com/50361336/105450769-31cde800-5ca1-11eb-81c4-5069af4ab0c7.png)

Distribution plots of all continuous variables in dataset: 

![Picture2](https://user-images.githubusercontent.com/50361336/105451265-41016580-5ca2-11eb-9f89-c5a76a7776ac.png)
![Picture3](https://user-images.githubusercontent.com/50361336/105451272-42cb2900-5ca2-11eb-8e11-fd9efd312b5f.png) 

The following represents Distribution percentage of Categorical Variables 

<img width="803" alt="Screenshot 2021-01-22 at 11 05 50 AM" src="https://user-images.githubusercontent.com/50361336/105451475-a2c1cf80-5ca2-11eb-8259-fdc3a43c4a11.png">  

### e.	Bivariate analysis (relationship between different variables, correlations) 

<img width="818" alt="Screenshot 2021-01-22 at 11 06 10 AM" src="https://user-images.githubusercontent.com/50361336/105451503-ac4b3780-5ca2-11eb-9950-6be790234833.png"> 

### f.	Business Insights derived from the EDA 

- We are able to understand the scope of this dataset, that is , data is provided for a limited time period (time range constraint ) and thus might reduce the efficiency of the predicted model 
- Nothing about the E-commerce company (It is anonymous) is known. Thereby making personalised suggestions and data explorations limited
- Thus we move ahead to model building, where we try and find the top predictors influencing churn and from the insights derived, make recommendations for customer incentives, company policies, product pricing and payment methods. 

## Data Cleaning and Pre-Processing 

### a.  Removal of unwanted variables (if applicable)	 
CustomerID is a variable that will not be useful for our analysis. Have checked to see if each record is a unique CustomerID and made sure it is. So, we can safely remove CustomerID variable. 

From an initial look into the dataset, we don’t see any other variable that are unwanted. 

### b.	Missing Value treatment (if applicable)	
In categorical variables there are no NULL/NaN values. 
Missing values for each continuous variable is as given below. From this we see that days since last order has maximum null values at 307. This accounts to be about 5.5 %. So, we can impute null values with the median value for each variable.   

Now the null counts of variables is given as: 

![Picture4](https://user-images.githubusercontent.com/50361336/105451282-452d8300-5ca2-11eb-8c4a-99e8fe3eb9c5.png)  

We can see that variables that have missing values are 'Tenure', 'WareHousetoHome', 'HourSpendOnApp', 'OrderAmountHikeFromlastYear' , 'CouponUsed' , 'OrderCount', 'DaySinceLastOrder'. 

We treat missing values with median value for each variable. 


### c.	Outlier treatment (if required)
We see that there are no outliers in the categorical variables. The maximum number of outliers is found out to be 703 which accounts for 13%, so we go ahead and treat it for outliers and replace them with their medians. We first treat for values that are above the third quartile, Q3, observe the impact on the number of outliers recorded and then treat for outliers which are below the first quartile, i.e. Q1.However, to prevent the problem of overfitting, the same is not done for the variable “Cashbackamount”.

Outlier count of variables is given by: 

![Picture5](https://user-images.githubusercontent.com/50361336/105451925-6773d080-5ca3-11eb-9f1a-e68e853d4cdf.png) 

Now, Outlier count after treatment is: 

![Picture6](https://user-images.githubusercontent.com/50361336/105451930-68a4fd80-5ca3-11eb-88a5-fb23f28d6b93.png) 

Thus reducing the maximum number of outliers to 344 ( about 6.4% and we thus neglect it). 

### d.	Variable transformation (if applicable)
Variable transformation needs to be done for the following categorical variables : 
-	Preferred login device
-	Preferred Payment Method
-	Gender
-	Preferred order Category 
-	Marital Status 
We use one hot encoding as none of the variables has any inert order (not ordinal , variables are nominal)

### e.	Addition of new variables (if required)
Dummy variables have been introduced for qualitative variables mentioned above in order to get meaningful insights from them. The problem of dummy variable trap has also been prevented by the use of one less dummy variables than the given number of classes in a particular qualitative variable. For example, for the variable gender, we use only one dummy variable which takes the value of 1 if male and since 0 automatically implies that it is female, we do not introduce another dunny variable column for it. 


## Model building and interpretation	
### a.	Build various models (You can choose to build models for either or all of descriptive, predictive or prescriptive purposes)
	 
**LOGISTIC REGRESSION**  

Logistic Regression has been used as it is an algorithm that is extremely simple, easy to understand and implement. It is also very efficient to train the dataset using this model. The “l1” and “l2” regularization techniques prevent the model from over fitting, which also acts as an added benefit. 

Now, we run a logistic regression model on the given dataset and derive the following conclusions: 

Accuracy: Accuracy of the Logistic Regression Classifier on the test set if 88 %


**RANDOM FOREST CLASSIFIER**

The ensemble model, random forest classifier has been used as it produces a highly accurate result even without hyper parameter tuning. And since we have a significant number of explanatory variables, random forest classifier has proved to have a higher true and false positive rate. Thus increasing the model efficiency. 
 
Now, we run a Random Forest Classifier model on the given dataset and derive the following conclusions: 

Accuracy: Accuracy of the Logistic Regression Classifier on the test set if 96.21 %


**XGBoost CLASSIFIER** 

The ensemble model, XGBoost, has is the combination of all the significantly good features of random forest and gradient boosting thus is being used to predict the customer churn. 

Now, we run a XGBoost Classifier model on the given dataset and derive the following conclusions: 

Accuracy: Accuracy of the Logistic Regression Classifier on the test set if 90.29 %

**KNN Classifier**

K- Nearest Neighbour algorithm has been used because of its simplicity and its feature which will be most useful in predicting if a customer will churn or not. That is, when a new customer is presented in this algorithm, it runs through its given database of customers, looks for the ones that are more similar to the given customer and thereby predicts if this new customer would churn or not – based on what the similar customers did. 

Now, we run a KNN Classifier model on the given dataset and derive the following conclusions: 

Accuracy: Accuracy of the Logistic Regression Classifier on the test set if 86.09 %

**SVM Classifier**

The main reason behind using this algorithm is its usage of risk minimalization principal and its focus on training the data points on the separating hyper planes – as compared to other supervised learning models. 

Now, we run an SVM Classifier model on the given dataset and derive the following conclusions: 

Accuracy: Accuracy of the Logistic Regression Classifier on the test set if 88.63 %


**Naive Bayes Classifier**

This model has been used with the aim of achieving high accuracy in lieu of a significantly large data and high number of dimensions with casual heuristics. 
Now, we run a Naïve Bayes Classifier model on the given dataset and derive the following conclusions: 

Accuracy: Accuracy of the Logistic Regression Classifier on the test set if 80.46 %

### b.	 Test your predictive model against the test set using various appropriate performance metrics

Statistics Comparison Table: 
Now, calculating the Precision, Recall, Accuracy, Support, ROC AUC Value and F1- Score For the train and the test dataset: 

Train, Test – dataset (the values are in the order of Train, Test for each column heading) 

Test and Train Model Parameters (without gridsearch): 

<img width="548" alt="Screenshot 2021-01-22 at 11 16 54 AM" src="https://user-images.githubusercontent.com/50361336/105451968-79ee0a00-5ca3-11eb-8385-8ffeee0c60e1.png"> 

Note: An accuracy of 1 implies that the sample chosen is not random.  

**MODELLING WITH GRID SEARCH** 

<img width="498" alt="Screenshot 2021-01-22 at 11 16 47 AM" src="https://user-images.githubusercontent.com/50361336/105451954-75c1ec80-5ca3-11eb-8589-e9de3c745fca.png">  

### c.	Interpretation of the model(s)	

Firstly, we note that from Table 1, none of the estimators of the train and the test value differ significantly.  Thus, showing us that there is no problem of overfitting. 
Now, from Table1, we see that the model with the highest accuracy produced is Random Forest classifier, followed by XGBoost Classifier. 

Now, on running these models through GridSearch CV with their best hyperparameters, we see that the estimators of the random forest classifier decrease drastically, while that of XGBoost remains more consistent. 

## Model Validation  
The model has been validated using the following:

1.	Train – Test Split: From Table 1, we can see that, none of the estimators of the train and the test value differ significantly.  We can thus see from the train-test split that all the models used are good models for the given dataset. 
2.	Hyperparameter tuning using GridSearchCV: GridSearch is one of the best methods for hyper parameter tuning. It performs exhaustive search over specified parameter values for the model. Using components like ‘best_params_’ ( for best parameter), ‘best_score_’ and ‘best_estimator’ we were able to derive the model that gives the most consistent result amongst all the selected models. 
So overall, the model validation was done on two parts, first with the train-test split to check if the selected models are a good fit for the given data and later on, GridSearchCV was employed to check which model showed the most consistent results. 

## 	Model Tuning and business implication	
### a.	Ensemble modelling, wherever applicable 

 The ensemble models, random forest classifier and XGBoost has been used with the aim of achieving an optimum model and also as the characteristics of these two models are very much in line with the given dataset and the problem statement of predicting if a customer will churn. 


### b.	Other model tuning measures used

Model Hyperparameter tuning has been done and Grid Search CV had been used to obtain a better understanding of the best suited model. The model and the respective hyperparameters tuned are as follows: 
1.	Logistic Regression- The Hyperparameters tuned are: Penalty and C 
2.	Random Forest Classifier - The Hyperparameters tuned are: n_estimators, max_depth, max_features, criterion 
3.	XGBoost Classifier - The Hyperparameters tuned are: gamma, subsample, colsample_bytree, max_depth 
4.	KNN Classifier - The Hyperparameters tuned are: n_neighbors, weights, algorithm 
5.	SVM Classifier - The Hyperparameters tuned are: C, gamma, kernel 
6.	Naïve Bayes Classifier - The Hyperparameters tuned are: var_smoothing
	
### c.	Interpretation of the most optimum model and its implication on the business
	
In lieu of the results obtained in Table 2 and their corresponding value in Table 1, we can conclude that XG Boost Classifier is the most optimum model for this given dataset. The initial reason for choosing the model, which is, it having all the significantly good features of random forest and gradient boosting thus is being used to predict the customer churn pays off with its estimators being consistent even after the application of Grid Search CV shows that this model is best suited. 

Now, we see that the precision of the model increases from 0.83 to 0.90 , the accuracy of the model also shows the same pattern with an increase from 0.90 to 0.95, the recall value also increases from 0.58 to 0.81, thus giving us a model with high precision and high recall as compared to other models, which is the best suited. It’s F1 score is also high at 0.85. And due to these reasons, it is the best model to determine the customer churn.  


## Final Interpretation/ recommendations 

### a.	Top Predictors 
We thus observe that the top predictors are, 
- Tenure
- Complaints
- Relationship Status 
- Type of Items Purchased 
which determine if a given customer will churn 


### b.	Recommendations 

1.	Tenure: It has been observed that the longer the tenure of the customer, the less likely they are to leave the platform. Thus, incentives like loyalty points, based on the duration they have used the platform should be given, to make use of this.
2.	Complaints: The fact the customer is taking out time register a complaint shows that they are disappointed with the service. Especially with reference to the given company, the customers who complain are more prone to churn.  And thus, extra attention should be given to such customers. Some things that can be done to take care of this is;
- Expedite Complaint Resolution
- Engage with Complainant to see if their gradience resolution was satisfactory
- Improve Complaint Management in system
3.	Marital Status: It has been seen that single/unmarried customers are less likely to churn. This might be because 
- It is generally the younger population that is unmarried and understandably, they tend to have lesser finances at their disposal, so giving them options like the purchasing a product on instalment will attract them to the platform
- Work also need to be done to ensure that the platform is more youth friendly by having the latest gadgets that is popular and savvy.

4.	Type of Products Purchased: It is noticed that customers buying more expensive products such as electronic gadgets and accessories, tend to churn. This might be because they use the platform for a one time buy. Now, to prevent this from happening we can do the following:
- Since they are buying expensive commodities through the ecommerce platform, this shows that they already trust the company. So by directing personalised advertisements that for say, if the customer buys a laptop, then other accessories that go with it, and that they will have to buy will help keep them on the platform and prevent them from leaving. 


So overall effort needs to be put in to ensure the already existing loyal (longer tenure) customer base doesn’t churn and also ensuring that the newly acquitted customers have a smooth initiation with the platform.  






