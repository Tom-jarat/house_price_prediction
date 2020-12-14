# Executive summary

This project provides a linear regression analysis to find the potential characteristics of residential houses. The project aims to estimate the sale price and the cost-effectiveness of doing renovations. Methods of analysis include Exploratory Data analysis, Feature Engineering, Modelling and Model selection of Ames housing data from Kaggle. All the process can be used to determine the best features both fixed and changeable. Based on the result, the best model among all is Ridge and Lasso regression indicated by R square and Mean square error. The best fixed feature is ground living area. For the changeable feature, the overall rating of property’s material and finish of the house is the best characteristic among all. The report finds the potential investment of the company to purchase undervalued property or renovate the property and resell it to the market.  



# Introduction

The project uses the Ames housing data recently made available on Kaggle to determine the best characteristics of the property that will affect the sale price. Based on the data provided, I used a supervised learning technique and regression analysis to identify the potential house that company can buy to make a profit from the renovation and reselling the property to the real estate market. The project consists of two parts. First is to estimate the sale price of properties based on the fixed characteristic of properties. The features such as neighbourhood, lot size, number of stories will assess to define the property price. After evaluating the fix characteristics, I used the estimation of the value of possible changes and renovations to properties from the variation in sale price not explained by the unchangeable features. The goal is to estimate the potential return on investment when making specific improvements to properties. Lastly, I determined the features in the housing data that best predict "abnormal" sales (foreclosures, etc.).

# Objective

The project aims to identify the characteristics of residential houses that estimate the sale price and the cost-effectiveness of doing renovations.

# Data Background

The Ames housing data is from Kaggle. The data consists of 1460 rows and 81 columns. The target variable is SalePrice columns that will use all the 80 features to predict the sale price of the properties. 

# Methodology

In this project, I used regression analysis which is the selection of 3 models (Linear regression, Ridge regression, and Lasso regression). Before modelling, understanding the data is an important aspect. I started analysis with the Exploratory Data analysis to understand the data. Then, the application of feature engineering is used to deal with independent and dependent variables including dealing with missing value before feeding the data into the model.

# Exploratory Data Analysis

## Data

Exploratory Data Analysis is the initial investigations process on the data to find a pattern and test the hypothesis and check the assumption of the project.  
 
 

After going through the data description to understand the raw data and information, I check the shape of the raw data including getting the information of data. The first point that is the data has a column named Id which is unnecessary. I can drop the Id columns or set it as the index column. As the result, the data dimension reduces from 81 columns to 80 columns. Secondly, a figure above shows that some columns contain the missing value. This topic will be covered in the later section.


## Dependant variable

The target variable of this project is the sale price. To be more understanding in the target variable, data visualization is a tool to make data more easily to interpret. I used the distribution plot and Q-Q plot to understand the target variable of regression analysis. 

According to the graph above, the distribution of the dependant variable is right-skewed. As you see from the SalePrice Distribution, the price is positive-skew distribution. The data may violate the assumption of linear regression as it assumes that the error terms will follow the normal distribution when we used the skewed target, the error or residual will usually be skewed. Secondly, the Quatile-Quatile plot shows that the target variable does not follow normal distribution which I will need to handle. The solution of this problem can use log transformation which converts the target variable to be normally distributed. On the other hand, the value of the house price will stay positive as it should be. According to the goal is dollar value estimation, I will not transform the data and let it as it be.

## Top 10 correlated features to target variable
 
The Top 10 correlated features to target variable describe the movement of property price based on the change of the value of the individual feature by 1 unit. For example, the overall quality of the property is positively correlated to the SalePrice. It means that when the OverallQual value change by 1 unit. The SalePrice value will change in the same direction with OverallQual by 1 unit and vice versa. The figure below shows the relation between 10 features in the correlation aspect.


 
According to the table above, there are two points concerns about the correlation table. First of all, the higher correlation to the SalePrice will have a higher chance that this feature will be important in the regression analysis. It means that all these features in the table above will be important in the model later. Second is multicollinearity. GarageArea and GarageCars are highly correlated with the value of 0.88. As a Rule of Thumb, the area of the garage will result in the higher car space in the property. That is the reason why GarageArea and GarageCars is a high correlation. To prevent multicollinearity, I will drop the GarageArea Column because the GarageCars has a higher correlation to the target variable.



## Scatter plot of SalePrice and GrLivArea

According to data description, the GrLivArea column is the living area above ground in square feet which is highly correlated to the price of the property. The scatter plot is a type of visualization using coordinates to display values of two variables for a set of data. The graph below shows the scatter plot of SalePrice and GrLivArea column.
 

The figure above shows the pattern between SalePrice and GrLivArea are moving in the same direction as the correlation value described. As you can see from the graph, there are two obvious points of data which can identify as the outliers. The outliers display on the bottom right of the graph which may reflect the negative result in the regression model. So, I decided to drop the 2 rows of data as the outliers.

## Boxplot of SalePrice and GarageCars

Based on the top 10 correlation matrix, the OverallQual and GarageCars columns are the two of the highest correlated values to the property price. Boxplot is a standardized way of displaying the distribution of data based on five descriptive statistic values. The values included minimum, first quartile, median, third quartile and maximum. This graph can detect the outlier based on these five values and also identify the skewness of data.
  

The graph above shows that the higher the overall quality of the property will result in a higher price. On the other hands, the Garage Cars graph shows that the price will be rise based on the number of parking spot available in the house with only one condition. It seems that four parking spots are unnecessary in the property because it does not reflect in the house price risen. Besides, the median value of the property with 4 parking spots is higher than the median of the property with 2 parking spots. Besides, there are outliers based on the graphs above. The outlier shows above is a point that out of the range of 1.5 times of interquartile range (Q1 – 1.5 * IQR or Q3 + 1.5*IQR) or whiskers. I decided to drop all the value that can classify as an outlier from the graph above to get a more accurate result.


# Missing Value

The missing value in the data is the important aspect that data scientist needs to handle. According to Ames housing data, there are 19 features that contain null values. The table below shows the name of the feature, missing percentage, description of the feature, filled value, and meaning of imputed data.

 

According to the table above, the most missing features are PoolQC, MiscFeature, Alley, and Fence respectively. I decided to use the description of data and data characteristic to define the missing value of each feature. For example, the PoolQC column uses the input as the indicator of the quality of the pool. I classify this column as the categorical value. So, the imputation of this column is ‘None’ which means the column does not have a pool in the property. The missing value can handle in various ways. In this project, I define the imputation of this data in 3 categories  

1. If the feature is categorical data, I will impute it as None which mean there do not have these features in the property.
2. If the feature is numeric data, I will impute it with 0 as there do not have these features in the property.
3. If the feature is suitable to impute statistical value, I will impute it with a statistical value such as mean or median.


# Feature Engineering 

As Features are important attributes to predictive models and 

Feature engineering is the process of using domain knowledge to extract features from raw data via data mining techniques. These features can be used to improve the performance of machine learning algorithms. 


## Data Types

Based on Ames housing data, there are 2 types of data. One is numeric data such as Area of Basement, Living area, and Pool Area. Another is categorical data. This data tells the condition or other characteristic of property including Condition of the house, Fireplace Quality.  


 

According to the figure above, the conversion of data type is applied to the columns that should not be in the data type. The characteristic of year should not count as number because it will affect to the model as the magnitude of number result in the importance of the features. Therefore, I convert it into string to be classify as categorical value. The MSSubClass also identify the type of dwelling involved in sale in numeric value. As it does not measure the as the continuous value. So, I decided to convert it into string to classify as categorical value.


## Skewness data

The skewed data does not harm a regression analysis as skewed residual does. The skewed data may result in skewed residual. So, I decided to use log transformation to transform data to be normally distributed. The log transformation only applies to the numeric data. The pictures below show the skewness of each numeric variable before and after transformation of each independent variable.

  

Based on the pictures above, the most skewed data are MiscVal, PoolArea, 3SsnPorch, and LowQualFinSF respectively.  The conversion of independent variables using log transformation do not change the distribution to normally distributed as there are too many inputs as zero such as PoolArea column. According to the column, there are many properties that does not contain pool in the area. So, the inputs are zero does not effectively reduce the skewness of the data.


# Modelling

In this project, I used 3 regression models including linear, ridge, and lasso regression. The regression analysis divided into two parts. The first one is fixed features. These features cannot be renovated as it attached to the properties to find out the most impactful feature to property price. Second is to define the best impactful feature from the residual value which left from the first regression. The second regression will describe the best characteristic that company that renovate and make profit from refurbishing the property.

## Model selection

After implementing each model as mention above, the selection of model will use the metrics including mean square error and R square to select the best model among three models. Furthermore, the selection of model also applied the characteristic of regression to help define the quality of data and model.  

## Linear regression

 

## Ridge regression
 
## Lasso regression
 


According to figures above, the result shows mean square error and R square from 3 model.
the metric is divided into test and train data. The linear regression seems to be the best model with the highest accuracy, but the model cannot deal with the test set. The result of the test set is extremely wrong with both metrics. On the other hand, the ridge and lasso performed better with 90.67 and 88.22 for train set and 87.53 and 87.33 for test set. The consistency of the lasso is better, but the average performance of the ridge is better than lasso. Therefore, I will use ridge and lasso residual to identify the best features that company can use to make profit of the property. 






# Predicted house price and Residual plot

As the predicted property price must be related to the observed house price, the first graph shows how well the model perform between 3 linear model. After I plotted the predicted price and the observed price, the second figure shows the residual of each model which both graphs are divided into test, train and whole data to validate the linear regression assumption.  




 

 

The graph above shows the relation of the predicted price to the SalePrice column identified the performance of the model. The graph above should be positively correlated. As the higher of the observed price, the predicted price should have the same value to define the accuracy of the model. According to the figure above, the ridge and lasso regression has performed more accurate compared to the linear regression. As the linear model mostly predicted the sale price as zero which do not have a homogeneity of variance. The graph will support the decision of the section above which I mentioned that I will use ridge and Lasso to predict the best feature both fixed and changeable property. 


# Potential renovation property

After the fixed features were used to identify the model that perform well with this data set, the residual values of the model were used to find the unexplained data by the first model. I used Ridge and Lasso regression to identify the potential features to find a potential investment opportunity. 

 


 

The figures above shows the result of the Ridge and Lasso model respectively. The R square of the both models are 34.06 percent and 36.92 percent for Ridge and Lasso model. For the second model, the both models perform with the same level of consistency and accuracy. The overall of the model result in the same features importance with the highest value of overall quality of the property. 


# Findings

According to the Ames housing data recently made available on Kaggle , the project aims to find the potential investment in the properties by investing in property and refurbish it to make profit from reselling the renovated property to the market. The result of the best property’s characteristics used R square and MSE (Mean Square Error) to support decision of the model. For the unchangeable features, the most importance feature that result in positive house price is ground living area in square feet. The higher of 1 unit of square feet will result in higher price of the property about $6000 dollar. Not only the area, the location of the property is also significantly related to the house price. The property located in Northridge Heights result in the higher of property price by $6000. In term of investment opportunity, the location is a factor that company need to concern. Moreover, the model values the number of Garage car that available in the property which is the sixth rank above all features. The fixed feature can be used to calculate the initial cost of investment and find the undervalued properties in the market. The next section is to identify the potential features that company can renovate to resell the property with the significant profit. The most important feature is the overall rating of property’s material and finish of the house. The higher of 1 rating will result in increasing of house price more than $6000 dollar. The second rank of all changeable feature is overall condition of the house which result in increasing property price about $6000 dollar. In the investment opportunity, the company will look at the features that result in the negative or low value of the features and find the largest gap compared to the most positive feature to property price. For example, the company can find the property with Gravel and Tar which result in negative property by $2000 and renovate it to be by using Wood shakes material. The wood shakes material will result in positive of the property price about $2000. As the result, the property price will improve by $4000 in total. The cost of investment also need to calculate to find the best potential opportunity to the company.   









