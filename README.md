
For this first segment of the final project, I took on the triangle role, which deals with the provisional machine learning model.  To begin with, I took our dataset on co2 and combined it with another that had temperature data, to create a fuller picture.  I then did some work to make the data work better for supervised machine learning, by creating a column with a binary outcome, in this case ‘high’ and ‘low’.  This referenced whether a given country is determined to be have a high ratio of co2 emission to gdp (polluter) or a low ratio (less of a polluter).  

## Which model
For the initial, early model, I chose a logistic regression model.  I chose this model because our target variable is a binary outcome, which is ideal for logistic regression, and because we hope to make predictions on future emissions outcomes.  I hoped a logistic regression model be able to determine the relationship between our binary outcome of high/low pollution ratio and the factors contributing to it, which in this dataset are temperature, co2 emission, population, and various gdp calculations.

## Training the model
To train the model, I broke our variables into `X` and `y`, with `X` being all the features except for ‘emission_ratio’ and `y` being the ‘emission_ratio’ column with values of ‘high’ or ‘low.’  After encoding the categorical data, the model was trained using the train_test_split method from the scikit learn library.
## Model Accuracy
After running the training data through the logistic regression model, I made predictions on the test data `(X_test`) and compared it to the actual data `(y_test)` in a dataframe.  I also used the accuracy_score method from the scikit library, which showed a result of 0.9945, or 99%.
## How does this model work
This model works by analyzing the available data and then, when given new data, it determines the probability of the data belonging to one of two classes.  In this case, it used the training data to determine the factors contributing to a country being a ‘high’ or ‘low’ ratio polluter, and then when given the testing data, it was able to predict ‘high’ or ‘low’ with 99% accuracy. 
