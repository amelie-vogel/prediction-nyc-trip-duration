# Prediction Of A Trip Duration - NYC Taxi Trip


## Dataset 

### Description 
This dataset is based on the 2016 NYC Yellow Cab trip record data made available in Big Query on Google Cloud Platform. The data was originally published by the NYC Taxi and Limousine Commission (TLC). The data was sampled and cleaned for the purposes of a Kaggle competition: https://www.kaggle.com/c/nyc-taxi-trip-duration/data

The data contains important features like pickup and dropoff dates and times, as well as geographical coordinates of the trip, and passenger counts. 



### Addendum: Weather data
Thanks to the following dataset made available on Kaggle (https://www.kaggle.com/mathijs/weather-data-in-new-york-city-2016), I added weather features to check if weather conditions influence traffic.

Weather data has been collected by the National Weather Service. It contains weather conditions of the first six months of 2016, from a weather station in Central Park. For each day, the features are: minimum temperature, maximum temperature, average temperature, precipitation, snow fall, and current snow depth. The temperature is measured in Fahrenheit and the depth is measured in inches. T means that there is traces of precipitation.

## Cleaning the data

Before merging the two datasets, I worked on the main one and cleaned it up.

As important tasks, I calculated the distance driven by a NYC taxi thanks to the coordinates, and calculated the duration of each trip based on the precise times of pickup and dropoff. 

I then dropped the trips that exceeded 2 hours, and those shorter than 1 minute, since there were obvious outliers (mean of a trip : 14 minutes ; median : 11 minutes). 

# Modelling

## Feature engineering with K-Means clustering

I tried to add clusters as features. 

Using the elbow method, I've been told to choose either 5 clusters after PCA, or 6 clusters without PCA. 

I decided to use K-Means with both, and finally added the 6 clusters that had been found without PCA (less costly).

I then built new train and test sets, using those clusters as new features.

## Supervised Learning

I tried 4 models of regression and evaluated them using 3-fold cross-validation. 

Here are the results:

### Linear Regression with OLS

##### 1) With clusters as features 

Using linear regression (with sklearn), I got a R-squared of 40% on the train set, and 41% on the test set. 


##### 2) Without clusters 

The results here being close to those with clusters (40% and 41% on train and test sets), we decide to drop the clusters for the following models. 

##### 3) K-fold cross-validation results

After cross-validation (3 folds), the scores of linear regression are:

- Score of R-squared on the train set is 0.41
- Score of R-squared on the test set is 0.39

We can thus conclude that 39-41% of the variation in trip duration can be explained by the variation of the variables: it's a relativeliy strong relationship.

### Ridge Regression 

After cross-validation (3 folds), the scores of Ridge regression are:

![image](https://user-images.githubusercontent.com/63364114/92381000-5c603f80-f10a-11ea-9363-ee0883d1d563.png)


### Lasso Regression


After cross-validation (3 folds), the scores of Lasso regression are:

![image](https://user-images.githubusercontent.com/63364114/92381023-62eeb700-f10a-11ea-8433-c83eeb703d23.png)



### Random Forest Regression

After cross-validation (3 folds), the scores of Random Forest regression are:


##### Depth of the model:

![image](https://user-images.githubusercontent.com/63364114/92381073-76018700-f10a-11ea-8834-7b3490d2f08a.png)

##### Number ot estimators:

![image](https://user-images.githubusercontent.com/63364114/92381049-6f730f80-f10a-11ea-857b-61cfebcac843.png)


### Selected model 

Based on the previous results, we opt for the Random Forest Regression model with parameters: depth of 15 and 35 estimators. 

## Contact me
[LinkedIn](https://linkedin.com/in/amelie-vogel-/)

[GitHub](https://https://github.com/amelie-vogel/)
