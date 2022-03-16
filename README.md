# AmExpert-2021-Machine-Learning-Hackathon 

## Rank 23 solution AmExpert 2021 – Machine Learning Hackathon
## Leadeboard link (user: xeeman)
https://datahack.analyticsvidhya.com/contest/amexpert-2021-machine-learning-hackathon/#LeaderBoard

XYZ Bank is a mid-sized private bank that includes a variety of banking products, such as savings accounts, current accounts, investment products, credit products, and home loans.

The Bank wants to predict the next set of products for a set of customers to optimize their marketing and communication campaigns.

The data available in this problem contains the following information:

* User Demographic Details : Gender, Age, Vintage, Customer Category etc.

* Current Product Holdings

* Product Holding in Next 6 Months (only for Train dataset)

Here, our task is to predict the next set of products (upto 3 products) for a set of customers (Test data) based on their demographics and current product holdings.
 
### Dataset Description
### Train.csv

Variable|Definition
|---|---|
Customer_ID|Unique ID for the customer 
Gender|Gender of the Customer
Age|Age of the Customer (in Years)
Vintage|Vintage for the Customer (In Months)
Is_Active|Activity Index, 0 :  Less frequent customer, 1 : More frequent customer
City_Category|Encoded Category of customer's city
Customer_Category|Encoded Category of the customer
Product_Holding_B1|Current Product Holding (Encoded)
Product_Holding_B2 |Product Holding in next six months (Encoded) - Target Column
 
### Test.csv

Variable|Definition
|---|---|
Customer_ID|Unique ID for the customer
Gender|Gender of the Customer
Age|Age of the Customer (in Years)
Vintage|Vintage for the Customer (In Months)
Is_Active|Activity Index, 0 :  Less frequent customer, 1 : More frequent customer
City_Category|Encoded Category of customer's city
Customer_Category|Encoded Category of the customer
Product_Holding_B1|Current Product Holding (Encoded)
 
### Evaluation Metric

The evaluation metric is Mean Average Precision (MAP) at K (K = 3). MAP is a well-known metric used to evaluate ranked retrieval results. E.g. Let’s say for a given customer, we recommended 3 products and only 1st and 3rd products are correct. So, the result would look like — 1, 0, 1

In this case, The precision at 1 will be: 1*1/1 = 1 The precision at 2 will be: 0*1/2 The precision at 3 will be: 1*2/3 = 0.67 Average Precision will be: (1 + 0 + 0.67)/3 = 0.556. The formula is:

Mean average precision is the mean of average precision calculated across all users
 
Where n = number of customers
 
### Public and Private split

Note that the test data is further randomly divided into Public (30%) and Private (70%) data. Your initial responses will be checked and scored on the Public data.
The final rankings would be based on your private score which will be published once the competition is over.

### Guidelines for Final Submission
Please ensure that your final submission includes the following:

* Solution file containing the predictions for next 3 products (format is given in sample submission csv)
Note : Format of your submission should be as mentioned in the sample submission file.

* Code file for reproducing the submission, note that it is mandatory to submit your code for a valid final submission
 
## Rank 23 Solution Description
The main challenge in this competition is how to tackle multiple product recommendations. We are also asked not to use customerID features as part of this competition. This would mean that we cannot use matrix factorization based features which provide significant perfromance improvement. Following are salient features of this solution:

* This solution converts the problem into a multi-label classification problem where multiple label can be correct at once.
* It applies MultilabelStratifiedKFold to get train and validation sets (using the library iterstrat. source: https://github.com/trent-b/iterative-stratification)
* The prediction is made over 5-fold MultilabelStratifiedKFold and aggregated probablities from the 5 folds are used for prediction.
* Top three predictions with highest probability is used for recommendation.
