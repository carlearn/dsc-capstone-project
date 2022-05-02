# Capstone Project

This is the final project of Flatiron Decision Science bootcamp program. 


## Project Overview: Predicting the Market Value of FIFA Soccer Players

### Overview

As a soccer fan, I am very excited for the rating release every year and have a strong interest in understanding what factors determine the market value of soccer players. According to FIFA's description of its' Ratings Collective, the overall ratings are based on the attributes. Therefore, for this project, we will focus on the prediction of players' market value using these attributes.

We will leverage the data source Kaggle FIFA 22 complete player dataset, which covers the players data (with 100+ attributes) for the Career Mode from FIFA 15 to FIFA 22, and allows multiple comparisons for the same players across the last 8 version of the videogame. We will focus on the FIFA 2022 data sets.

Our **objective** is to build a regression model to predict the market value of soccer players and understand what key factors determine the market value of soccer players by what amount. 

Our **approach** is to establish multiple regression models with linear regression and machine learning regressors (i.e., Decision Tree, Random Forest, XGBoost and Support Vector Regressor) to get the best prediction of players' market value. 


### Exploratory Data Analysis

#### Data Cleaning

We removed the players who do not have market value in 2022, replaced the missing values with zero, and selected the players who are in level 1 league.

We also conducted One-Hot Encoding on categorical data for further analysis. 


#### Data Visualization 

We visualized the data for attributes analysis to check the relationship between market value and each single attributes. 

Here are some highlighted attributes which are also in the Top 10 Feature Importance of Selected Regression Model.

![](https://github.com/carlearn/dsc-capstone-project/blob/main/charts/Relationship%20between%20Market%20Value%20and%20Release%20Clause%20Value%20(in%20Million%20euros).png)

![](https://github.com/carlearn/dsc-capstone-project/blob/main/charts/Relationship%20between%20Market%20Value%20and%20Weekly%20Wage.png)

![](https://github.com/carlearn/dsc-capstone-project/blob/main/charts/Relationship%20between%20Market%20Value%20and%20International%20Reputation.png)

![](https://github.com/carlearn/dsc-capstone-project/blob/main/charts/Relationship%20between%20Market%20Value%20and%20Different%20Body%20Types.png)

![](https://github.com/carlearn/dsc-capstone-project/blob/main/charts/Relationship%20between%20Market%20Value%20and%20Club%20Positions.png)



### Modeling - Linear Regression

We conducted train-test-split and established 3 Linear Regression Models: baseline model, refined baseline model by removing uninfluential features by stepwise selection with p-values, and refined baseline model by transforming the data with MinMaxScaler. 

The selected linear regression model is the refined baseline model by removing uninfluential features by stepwise selection with p-values. There are 38 attributes. The most important features (except nationality-related features which also matter) that are determining the market value of the soccer players are:

(1) Body type is Unique
(2) Club position is Attacking Midfielder (Right, Left and Center as ranked in order)
(3) High international reputation

In respect of the model validation perspective, the selected Linear Regression Model performs well: Adjusted R-squared: 99.3%, RMSE for train data: 0.73, and RMSE for test data: 0.80.


### Modeling - Machine Learning Regression

We used the MinMaxScaler to transform the data and conducted train-test-split. We applied Decision Tree Regressor, Random Forest Regressor, XGBoost Regressor and Support Vector Regressor to run a regression model. 

The best model is XGBRegressor() with the lowest test RMSE, better than that of Linear Regression.


### Tuning XGBoost Regression with GridSearchCV 

We applied GridSearchCV to tune XGBRegressor() in order to get a better result. Best parameters are {'colsample_bytree': 1, 'learning_rate': 0.1, 'max_depth': 3, 'n_estimators': 100}. The results are the same as the original parameters selection in the XGBRegressor().


### Feature Importance 

We leveraged XGBRegressor().feature_importances_ to obtain the top 10 attributes that have higher importance in determining the market value of soccer players.

![](https://github.com/carlearn/dsc-capstone-project/blob/main/charts/Feature%20Importance%20-%20Top%2010%20primary%20attributes%20of%20the%20Market%20Value%20of%20soccer%20players.png) 

### Conclusion

In consideration of the adjusted R-squared and lowest Root Mean Square Error (RMSE), we selected **XGBoost Regressor** (i.e., XGBRegressor()) as our best regression model to predict the market value of the soccer players. 

We summariezed them into three categories: 
    (1) release clause value on contract and their weekly wages with the club, 
    (2) specific physical attributes and skillsets, and 
    (3) international reputation.

#### Next steps

1. Improve the parameter selection to tune the regression models:
    
    Given the limitation of the computation power, we did not take a deep dive into the tuning the parameters of GridSearchCV. In order to get a better result (more accurate prediction), it's important to spend more efforts to obtain the best parameters. We could leverage RandomizedSearchCV or HalvingGridSearchCV to increase the efficiency of parameters selection.

2. Recategorize the original attributes:
    
    We notice that the large number of attributes results in the higher R-squared. Among them, nationality after one-hot encoding created many new attributes. A better way to solve the problem is to map the country into region (e.g., Europe, Asia, North America, South America, Africa and others).

3. Incorporate FIFA ratings into the prediction of market value:
    
    We did not consider FIFA ratings in our current analysis given the FIFA ratings are derived from the attributes. However, there should be some relationship between FIFA ratings and market value. It could be another interesting topic to further discuss.
    

## The Deliverables


* [GitHub repository](https://github.com/carlearn/dsc-capstone-project)
* [Jupyter Notebook](https://github.com/carlearn/dsc-capstone-project/blob/main/student_notebook.ipynb)
* [non-technical presentation](https://github.com/carlearn/dsc-capstone-project/blob/main/capstone_presentation.pptx)
* [Blog](https://medium.com/@carrielearn/predicting-the-market-value-of-fifa-soccer-players-db0df4e4a651)


