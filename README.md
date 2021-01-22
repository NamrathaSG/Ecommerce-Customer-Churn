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
