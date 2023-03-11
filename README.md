# Analysis of Data Jobs Market

## The goal of the project is to analize data analysis related jobs, necessary skills, as well as salaries and schedule types in order to gain some insights about current job market in the field.

### The steps of the project:
1. Using SQLAlchemy extract three data sets from AWS, convert to data frames and merge.

2. Clean and transform the data to make the most use of it.

3. Analyze the data to gain insights into the jobs market.

4. Visualize these insights in order to demonstrate trends and patterns to the individuals seeking data analyst related positions.

5. Build linear regression model in order to predict the salaries upon such independent parameters as skills,schedule types, locations, etc.



Dataset, that was extracted with the help of SQLAlchemy, was transformed differently for different purposes:
- Kept more data including missing values for EDA
- For the purpose of predicting a salary, all the missing values from "salary_standardized" column were removed , as it is the target variable.

## EDA
During the EDA it was discovered that data is not normaly distributed, a lot of missing data. There are a lot of null values in every feature and simply no data on such major cities like Los Angeles, Atlanta, New York. We see a lot of positions' locations just marked as USA. The majority locations for positions listed in the dataset are "Anywhere"(remote positions). Since we have no information on many cities we can't draw conclusions on top 5 "hottest" cities in the market. However, we can infer that remote("work_from_home") positions are prevailing at the current 'data analyst' jobs market. As for the skills we ca assume that top 5 are SQL, Python, Excel, Power BI, Tableau.
EDWARD JONES, Upwork, Cox Communications, Corporate, Talentify companies seem to hire the most for data analysts positions.

Median salary for different companies, locations and skills is approximately the same. However, it's a bit lower for "work_from_home" positions. It seems like employees settle for smaller salaries just to be able to work remotely.

## ML
First tried to build simple linear regression model with the given data(after initial clean up and transformation). The model performed terribly, and it was clear tha data needs to be transformed further.
All the skills that serve as predictors are binary values and it was clear that they have imbalanced dictribution. Majority of skills were True (1) in less than a hundred rows out of total 2229 rows. 
Another major issue with predictor variables is a huge number of them - it increases dimensionality that leads to poor linear regression model. To address the issue I removed skills attributes that have frequency of less than 100 times.

Tried to build another linear regression model with the balanced out predictors. Unfortunately, there was no sign of improvement:
r2 0.00035697773152232326
Mean Absolute Error 28278.755269058292
RMSE 38941.620380587185

One of the reason of this outcome could be that there is no statistically significant relationship between predictor variables and the target variable. I did ttest for binary variables and Anova test for categorical variables. The tests showed that statistigal significance was only found between 'schedule_type','work_from_home' and the target variable 'salary_standardized'.

The target variable is imbalanced as well. Despite the fact that it is continous, it has a low variance, meaning that it has a lot of repeated values.

Converted continous target variable into categorical - turned it into 4 categories(salary intervals).
 Built Logistic Regression model(works better with binary or categorical variables). 
 Logistic regression showed improvement - 65% of accuracy, however it's not the desired result. Besides, it only predicts 2 majority classes.

 I think in order to improve models, additional data needs to be collected. Also there are some techniques that can be helpful to balance out predictor variables, such as feature selection ( use of correlation analysis just to choose a subset of important features)
 As for target variable, oversampling technique can be used - increasing the number of instances in the minority class.

 ## General conclusion
This data set is encomplete. In order to do EDA, that can give us information representative of the entire US "analysts" jobs market, or build a machine learning model, we need to collect additional data. We have a lot null values in every feature and the target variable contains hundreds of repeated values and some of them only occur once.


