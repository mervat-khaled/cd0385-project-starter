# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### Mervat Khaled

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
As Kaggle doesn't accept negative values in submission files according to the evaluation metrics "RSMLE": which can be used if actual or predicted have zero-valued elements, but this function is not appropriate if either is negative valued. 
So I had to set those values to equal zero, fortunately, all values were positive, except one value in the last submission file.

Also, I couldn't run the commend line in the notebook to submit my submission files because I have different operating system!. so I took screen shots from kaggle submission page.

### What was the top ranked model that performed?
The top ranked model was: WeightedEnsemble_L3 without "hyperparameter tuning", with adding new features ["hour","day","year"], transforming skewed features ["humidity","windspeed"], and dropping highly correlated features ["atemp",month]. 
And the error "RMSE" in validation set = 39.88 and in the test set: the Error "RSMLE" = 0.46397.

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?

 #### Basic EDA:
 * Histograms:
Histograms depict that there are two features that look nearly normally distributed ["actual temp","temp"], whereas the target variable "count" is right skewed, also ["humidity and windspeed] are left and right-skewed. And skewed features should be transformed to be near to normal distribution before modeling because that affects on prediction.
 
* Some features were binary such as [holiday, working day]
* some features were categorical such as [season, weather].

 #### Additional EDA:
 
#### Heatmap to check correlation:

The heatmap graph illustrates that most of the features have poor correlation with each other and with the target value "count", although there are some features have highly correlated with each other such as ["atemp" and "temp", "month" and "season"], and we should drop one of them before modeling because that will cause multicollinearity which affects on the prediction. So I will drop the column "temp" because the column "atemp"\actual temperature gives us the same info, and also drop "month" because "season" has the same info.

Count and Hour have a moderate correlation. 

#### Lag plots to check the randomness and outliers on some features:

lag plots above show a linear pattern which means the data ["count","hour", "day", "month", "temp"] are strongly non-random which is not good for most of the statistical models because randomness is an underlying assumption for most statistical estimation and testing techniques.
there are some outliers, and they should be handeled. 

** Resources:

[1](https://www.itl.nist.gov/div898/handbook/eda/section3/eda33f.htm)
[2](https://www.itl.nist.gov/div898/handbook/eda/section3/lagplot2.htm)
[3](https://www.itl.nist.gov/div898/handbook/eda/section3/lagplot3.htm)

#### FacetGrid graphs:

* Facet grid graphs with classes in weather and season columns show how weather condition has a strong effect on rental bikes, therefore bikes rent most of the time in good weather whereas no rents in bad weather/class 4: "Heavy Rain + Ice Pallets + Thunderstorm + Mist, Snow + Fog" because logically people wouldn't sacrifice their lives and rent a bike in bad weather.

#### Line plot graphs:

* The line plot graphs with ["month", "season"] columns emphasize, what we have already observed with facet grid graphs, that weather has a huge effect on total rents, thus, bikes rent more in summer and fall.

*  With the "hour" column,  The line graph highlights that over time of the day, total rents are nonconstant, with 2 peaks around 8 am and between 5 pm and 6 pm.

#### Count of rows that have a zero value in the wind speed column:

* there are 1313 rows in train data and 867 in test data that have a zero value in the windspeed column, and maybe that occurs because of  = missing values or there is something wrong with acquiring data from the system. 

 
### How much better did your model preform after adding additional features and why do you think that is?

In the first submission without adding any features, the model was suffering from high bias, so the error "RMSE" was 0.52 in validation data and 1.7989 with (RSMLE) error in test data. But after adding new features, extracted from DateTime info, ["hour", "day", "month", "year"] the error was minimized in both validation and test data: with (RMSE) = 0.30 and (RSMLE) = 0.77367, which is a huge improvement.

Also, I retrained the data after adding the same features but deleted the highly correlated features and transformed the skewed data with log transformation, and the error was minimized more in test data whereas slightly higher in validation data:
with (RMSE) = 0.39 and (RSMLE) = 0.46397, even though the error increased in the validation data the model generalized well in test data.

## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?

The model performed much better than the initial model and a little bit better than the improvement with just adding new features, 
but a little bit worse than the improvement with transformed skewed features.

rmse decresed from 39.88 to 37.20 for the best model. However, the model's test error icreased from 0.46397 to 0.51801. This gives an indication that the model with hyperparameter has a bit higher variance.

### If you were given more time with this dataset, where do you think you would spend more time?

I would spend more time detecting and handling outliers and doing more robust feature transformations to fix skewed data. 

### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.
|model|hpo1|hpo2|score|
|--|--|--|--|
|initial|defult|defult|1.7989|
|add_features|defult|defult|0.77367|
|add_features_transform_skewedfeatures_no_hpo| defult|defult|0.46397
|hpo|CAT|GMB|0.51801|
### Create a line plot showing the top model score for the three (or more) training runs during the project.

![model_train_score.png](img/model_train_score.png)

### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.


![model_test_score.png](img/model_test_score.png)

## Summary

The project showed how important doing EDA (exploratory data analysis) for knowing your data well and taking the right steps with feature engineering before modeling. also hyper parameter optimization is curcial step in machine learning process, which will make a huge improvment for choosing a robust model. 
