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






