# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### Mervat Khaled

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
As Kaggle doesn't accept negative values in submission files according to the evaluation metrics "RSMLE": which can be used if actual or predicted have zero-valued elements, but this function is not appropriate if either is negative valued. 
so I had to set those values to equal zero, fortunately, all values were positive, except one value in the last submission file.

Also, I couldn't run the commend line in the notebook to submit my submission files because I have different operating system!. so I took screen shots from kaggle submission page.

### What was the top ranked model that performed?
The top ranked model was: WeightedEnsemble_L3 with adding new features and defuelt setting "no hyperparameter tuning". 
The root squared error for the model = -19.36, R2/accuracy =0.988, kaggle score= 0.77367.

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?



### How much better did your model preform after adding additional features and why do you think that is?
TODO: Add your explanation

## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?
TODO: Add your explanation

### If you were given more time with this dataset, where do you think you would spend more time?
TODO: Add your explanation

### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.
|model|hpo1|hpo2|hpo3|score|
|--|--|--|--|--|
|initial|?|?|?|?|
|add_features|?|?|?|?|
|hpo|?|?|?|?|

### Create a line plot showing the top model score for the three (or more) training runs during the project.

TODO: Replace the image below with your own.

![model_train_score.png](img/model_train_score.png)

### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.

TODO: Replace the image below with your own.

![model_test_score.png](img/model_test_score.png)

## Summary
TODO: Add your explanation
