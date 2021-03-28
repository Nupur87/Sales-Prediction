# Sales Prediction
# Introduction and Summary of the Project
Sales are the lifeblood of a business. It's what helps business pay employees, cover operating expenses, buy more inventory, market new products and attract more investors. Sales prediction is a crucial part of the financial planning of a business. It's a self-assessment tool that uses past and current sales statistics to intelligently predict future performance.One simple sales forecast can inform every other aspect of the business.When a company constantly misses its sales forecast it can have a negative impact on its valuation over the long term. When the business cannot estimate how much revenue they will generate accurately, they can’t hire or invest to keep with the growth and that could lead to several missed opportunities. Decision makers rely on these predictions to plan for business expansion and to determine how to fuel the company’s growth. So, in many ways, sales prediction affects everyone in the organization.If a company predicts robust sales in the fourth quarter but only earns half that amount, it's a sign to stockholders that not only is the company performing poorly, but management is clueless. When attracting new investors to a private company, sales forecasts can be used to predict the potential return on investment.The overall effect of accurate sales forecasting is a business that runs more efficiently, saving money on excess inventory, increasing profit and serving its customers better.

Therefore the main objective of this project is to work on the anonymous supermarket sales dataset obtained from Kaggle and identify and visualize which factors contribute to the sales generation as well as to build a prediction model that will perform the regression task, compare the models and identify which model will provide the best sales prediction results and at last perform causal inference to understand what causes high or low sales generation for the supermarket. This dataset contains total 1000 rows and 17 attributes. The target variable is Total.

There are eight continuous variables:

-Unit price: Price of each product in $

-Quantity: Number of products purchased by customer

-Tax 5 percent tax fee for customer buying

-Total: Total price including tax

-COGS: Cost of goods sold

-Gross margin percentage: Gross margin percentage

-Gross income: Gross income

-Rating: Customer stratification rating on their overall shopping experience (On a scale of 1 to 10)

There are nine categorical variables:

-Invoice id: Computer generated sales slip invoice identification number

-Branch: Branch of supercenter (3 branches are available identified by A, B and C).

-City: Location of supercenters

-Customer type: Type of customers, recorded by Members for customers using member card and Normal for without member card.

-Gender: Gender type of customer

-Product line: General item categorization groups - Electronic accessories, Fashion accessories, Food and beverages, Health and beauty, Home and lifestyle, Sports and travel

-Date: Date of purchase (Record available from January 2019 to March 2019)

-Time: Purchase time (10am to 9pm)

-Payment: Payment used by customer for purchase (3 methods are available – Cash, Credit card and Ewallet)

The analysis have been performed in the below steps:

-Exploratory Analysis

-Data Preprocessing and Preparation

-Training,tuning and evaluating machine learning models

-Causal Inference

# Exploratory Analysis:

In order to identify patterns that can yield to total sales generation, exploratory analysis was performed on the dataset. The bar graphs, histograms and boxplots were made and some useful insights were drawn and explained in the notebook below. I created two three attributes Day,Hour,Month to identify the sales trend on a daily, monthly and hourly basis.

# Data Preprocessing and Preparation:

There was no missing data.

The variables such as Invoice ID did not have any predictive power as these were unuique to the customers and therefore was removed from the analysis. Similarly the attributes like gross margin percentage was removed since it had only one value for all the rows and Date and Time were also removed since they did not have any predictive power and I already converted date into day, hour and month tgo understand the sales trend, therefore to avoid duplicacy Date and Time attributes were removed.

The categorical variables were dummyfied using the label encoding and one hot encoding methods. The correlation matrix was formed in order to understand if there are any variables which are high colliear. From the matrix it was observed that there City was highly correlated with Branch and Tax 5 percent,cogs, gross income were highly correlated with Total sales so these variables were removed from the analysis to avoid multi collinearity issues.

The training and testing data was then standardised to ensure that each input variable has the same range so that the effect on the model is similar and the variable such as Total and Unit price that has greater ranges does not have larger influence on the model's results

After this, the feature selection process was performed using Lasso, RFE and Random forest methods to select the predictors which play a significant role in explaining the variation between X and Y better. The features that came out to be less useful for the prediction purpose were "Payment_Credit card","Product line_Food and beverages","Product line_Electronic accessories","Product line_Health and beauty" as based on their RFE rankings, Lasso cofficients(zero) and Random Forest Gini coefficients. Therefore, for the modelling purpose these useless predictors were removed from the analysis.

# Training,tuning and evaluating machine learning models:

Since this was a regression task, I tested and applied four regressions models which were Linear Regression, Random Forest Regressor, Gradient Boosting Regressor and XG Boost Regressor to analyse and comapre MSE,RMSE and MAE scores obtained by each of them.

To improve the overall performance of the model, I tuned the algorithms hyperparameters using GridSearchCV.

Models were built on the selected features and after the application of various models, it was found that Gradient Boosting Model generated the minimum RMSE of 10.64 with optimal hyperparameters as compared to other models.It also has the lowest MSE and MAE scores which makes it a perfect model for prediction of sales.

The GBT model also highlighted two most important features when it comes to sales prediction of a supermarket. Quantity plays an important role, where if people are buying large amount of quantity of the products that may lead to high generation of sales in different branches. Similarly, Unit price is the second most important feature, which may imply that the price of product plays an important role in the sales generation and people percieve any product with the low price there is a higher chance that they would buy it more and generate more sales, on the other hand it can also be possible that some premium products which have a higher unit price may be percievd as good quality products and that could lead to higher sales generation.

# Causal Inference

I made the hypothesis to check the effect of each variable (21 after dummifying) on Total sales. I created different models for each causal effect analysis with different treatments each time.

From the analysis it was observed that only three variables have the significant positive causal effect on total sales which were Quantity, Unit price and Customer type whereas Cash Payment had the significant negative causal effect on the total sales.

# Business Benefit
The Gradient Boosting Model built in this project would proof very helpful to the supermarket as they will be able to predict the supermarket sales accurately with lowest MSE (113) and RMSE(10.64) efficiently with least variation. This would ensure that the company is able to build strategies on improving the product, launching new products, increasing the payment options, increasing the quantity of the most popular and highly demanded products or manage the unit price of different types of products and offer different schemes on periodic intervals to different types of customers whether member or normal and male or female. The higher the sales are generated, means higher profitability for the firm and more customer base and better reputation of the supermarket in the retail market. The model also depicts that there is a direct causal relationship between Quantity, Unit price and Customer type, this will definitely provide a useful insight to the business where they can make strategies to improve their customer base by providing better offers and schemes as well as build pricing and supply strategies for different types of products in different branches and locations and based on customer preferences.
