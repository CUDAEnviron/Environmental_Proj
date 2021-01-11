# Technology use for Climate Change project

## Overview 

For this project we will utilize various forms of technology to accomplish the task of showing 
that there is a direct correlation between global temperature increase and an abundance of CO2 
levels. To do so, we will analyze the data from csv datasets that include: an extensive collection of global temperature data and Carbon Dioxide (CO2) emissions on Gross Domestic Product (GDP) by country and/or region. We will use pythondata to detect and correct any discrepancy in the data before fitting it into our machine learning model. 

## Python -- Jupyter Notebook 

We have combined the temperature csv with the CO2 emissions/GDP csv dataset. Using PythonData, we have imported the pandas library to delete empty columns and filter the country's column to include only countries that exist (posses a country code and excluding regions and continents). After cleaning the data, we combined the remaining columns and rows into a more concise dataframe. 
We further analyed the data to categorize the GDP per capita and CO2 outputs. 

## SQL Database

We have used a Postgres SQL database hosted by Heroku. Our original file currently cotains 24016 rows and 38 columns. We will continue to use Postgres SQL database to process our data as the project progresses.

## Machine Learning Model 

We are currently using a balanced random forest model to make predictions on emissions outcomes based on the data that includes the variables: temperature, CO2 emissions, population size and GDP. The model is trained using the train_test_split model from the scikit learn library. Thus far, we have measured an accuracy of approximately 99% (result = 0.9945) using the balanced_accuracy_score method.


## Tableau 

We may use Tableau to connect to our data sources, extract data into the sources and make visualizations of the data if needed. 
