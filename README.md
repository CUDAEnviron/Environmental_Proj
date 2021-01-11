

# Selected topic – Climate Change

Climate refers to the long-term regional or even global average of temperature, humidity and rainfall patterns over seasons, years or decades. 
Reason for Selection of topic

Climate change has become a huge problem that affects the very existence of life on the planet and a majority of climate change in the recent years in our industrial age is caused due to human activity. Global warming is the long-term heating of Earth’s climate system observed since the pre-industrial period (between 1850 and 1900) due to human activities, primarily fossil fuel burning, which increases heat-trapping greenhouse gas levels in Earth’s atmosphere. This has caused a dramatic increase of temperatures on both land and water surfaces, meltdown of ice caps, rise in sea levels, increase in the magnitude and frequency of hurricanes, and extinction of many species. These adverse effects can be slowed down or reversed with changes in human activity and proper education. 
Gross domestic product (GDP) is the total monetary or market value of all the finished goods and services produced within a country's borders in a specific time period.

This project’s goal is to show the correlation between the rise in temperatures due to rise in atmospheric greenhouse gases (CO2) caused by human activity and to conclude that controlling the CO2 emissions can regulate climate change phenomenon. In addition, using historical GDP, and CO22 emissions data, we aim to identify the current and long-term impact of climate change on economic activity across countries, and ultimately recognize economic gains from reducing carbon footprint. 

## Applicability

This analysis is applicable to the general public as well as many companies in various industries like automobile, fossil fuel extraction, food processing, chemicals, etc. that cause an increase in atmospheric greenhouse gases. It provides and overview of how rise in CO2 levels is causing a rise in average temperatures by country, which is the reason for all the adverse effects on various life forms including humans on Earth.

In addition, our analysis will show the projected impact of climate change on GDP per capital between now and 2100 for a select group of countries. 
Data Source 

1.	Temperature - All the temperature data necessary for the study is downloaded from Kaggle 
2.	The dataset is a global metric dataset from Jan 1949 to Oct 2018. The dataset includes Country Name, Year, CO2 level, CO2 Growth, Consumption, CO2 from Trade, CO2 Per Capita, % of Global CO2, CO2 from Cement, CO2 from Coal, CO2 from Oil, CO2 from Gas, Population, and Total GDP.

## Methodology 

1.	The aim of the project is to show the trends in temperature increase and the 
prime factor is the increase in CO2 levels due to human activity in the industrial 
age. 
2.	Since the cause has many factors and the data is available to show the 
correlation between factors and effects, this study will be a supervised learning. 
3.	This supervised learning model is going to be regression and time series 
forecast model to show the correlation, recent trends and future trends 
4.	The variable this project is aiming to predict is temperature - average, min, and 
max by Country

5.	The training data will be the raise of CO2 levels. The idea is to build a forecast model with varying levels of CO2 data once the relationship is established and show the sensitivity analysis by changing the trend in factor variables (e.g. CO2 from cement, CO2 from gas, etc..), increasing trend, prediction trend, decreasing trend in CO2, and also show how CO2 is changed in the atmosphere by varying the tree cover predictors. 

## Description of the communication protocols 

Majority of the communication will take place during classroom sessions, however as the project progresses, frequent meetings outside of those sessions will be necessary. Group members will be cognizant of information in the group slack channel and will attend group zoom meetings as necessary.  

## Potential Outputs

The deliverable will be a presentation with associated visualizations of sensitivity analysis, and an explanation of the approach. 

## How does GDP rates respond to temperature?

Determining this response is one of the main exercises of our project. As described in the paper, we use 70 year of  historical data for more than 174 countries to arrive at this estimate. 

# Charts

## The below charts show summary data of our analysis of the Co2 data as it relates to GDP. 


![](https://github.com/CUDAEnviron/Environmental_Proj/blob/Kam_branch/Images/Co2%20GDP%20Bar%20Chart.png)This Chart shows Co2 Per GDP by country.

![](https://github.com/CUDAEnviron/Environmental_Proj/blob/Kam_branch/Images/Co2%20GDP%20Bar%20Chart%20Desc.png)This Chart shows Co2 Per GDP by country in Descending Order. 

![](https://github.com/CUDAEnviron/Environmental_Proj/blob/Kam_branch/Images/Co2%20GDP%20Bar%20Chart_Top10.png)This Chart shows Co2 Per GDP by country (Top 10 Countries)

![](https://github.com/CUDAEnviron/Environmental_Proj/blob/Kam_branch/Images/Co2%20GDP%20Grid.png)This Chart shows Co2 Per GDP by country in Grid view. 


![](https://github.com/CUDAEnviron/Environmental_Proj/blob/Kam_branch/Images/Co2%20GDP%20Historical.png)This Chart shows a historical view of Co2 Per GDP by country.


![](https://github.com/CUDAEnviron/Environmental_Proj/blob/Kam_branch/Images/Co2%20GDP%20Map.png)This Chart shows Co2 Per GDP by country in a map view.


![](https://github.com/CUDAEnviron/Environmental_Proj/blob/Kam_branch/Images/Dashboard.png)This Chart shows a dashboard of Co2 Per GDP by country.


## Technology use for Climate Change project

### Overview 

For this project we will utilize various forms of technology to accomplish the task of showing 
that there is a direct correlation between global temperature increase and an abundance of CO2 
levels. To do so, we will analyze the data from csv datasets that include: an extensive collection of global temperature data and Carbon Dioxide (CO2) emissions on Gross Domestic Product (GDP) by country and/or region. We will use pythondata to detect and correct any discrepancy in the data before fitting it into our machine learning model. 

### Python -- Jupyter Notebook 

We have combined the temperature csv with the CO2 emissions/GDP csv dataset. Using PythonData, we have imported the pandas library to delete empty columns and filter the country's column to include only countries that exist (posses a country code and excluding regions and continents). After cleaning the data, we combined the remaining columns and rows into a more concise dataframe. 
We further analyed the data to categorize the GDP per capita and CO2 outputs. 

### SQL Database

We have used a Postgres SQL database hosted by Heroku. Our original file currently cotains 24016 rows and 38 columns. We will continue to use Postgres SQL database to process our data as the project progresses.

### Machine Learning Model 

We are currently using a balanced random forest model to make predictions on emissions outcomes based on the data that includes the variables: temperature, CO2 emissions, population size and GDP. The model is trained using the train_test_split model from the scikit learn library. Thus far, we have measured an accuracy of approximately 99% (result = 0.9945) using the balanced_accuracy_score method.

### Tableau 

We have used Tableau to connect to our data sources, extract data into the sources and make visualizations of the data. 

## Database Storage

- We are using a Postgres SQL database hosted by Heroku for our project.

- Our first base data file is Resources/<b>owid-co2-data.csv</b> and has 24016 rows and 38 columns.

- This file has been uploaded to the <b>co2_data</b> table in the Postgres database.<br><br>
<img src=Resources/co2_data_db.png></img><br>

- The <b>CO2_Data_to_Database.ipynb</b> Jupyter Notebook shows how the connection is made to the Postgres database and how the data is uploaded to the co2_data table.

- Our second base data file is Resources/<b>clean_Global_temps_1901_to_2016.csv</b> and has 22736 rows and 4 columns.

- This file has been uploaded to the <b>temperature_data</b> table in the Postgres database.<br><br>
<img src=Resources/temperature_data_db.png></img><br>

- Here is the ERD of our database:<br><br>
<img src=Resources/ERD.png></img><br>

- The database tables will be read into the machine learning model for analysis.



## Machine Learning Model
For this segment of the final project, we found a new temperature dataset than the one used in Deliverable 1.  The old dataset only went until 2103, and this new one has entries until 2016.  This dataset was cleaned and then uploaded to the database into the ‘temperature_data’ table,
### Preliminary Data Preprocessing
After importing both tables from the database and converting them to dataframes in the ML_model notebook, each dataframe was cleaned before being merged for initial analysis. In the Co2 data, the NAs were dropped, as well as any entries in the ‘country’ column that didn’t represent an actual country.  A new clean Co2 dataframe was created with only the most relevant columns.  The temperature data was cleaned as well, and then merged with the clean co2 data.  This combined dataset was then examined to establish if there is a correlation between co2 emissions and a country’s gdp output.  To determine a baseline for whether a country is a disproportionate polluter, we broke out the data for 2016, the most recent year in the dataset. We exported it as a csv to get a full look at the data and pick a baseline for "bad" ratio of gdp to co2 per capita.  After looking at the 2016 data in Excel, a new column is created to indicate co2 production per unit of gdp, by dividing 'co2 per capita' by 'gdp per capita' (multiplied by 100000 to make the result more readable). A baseline of 300 is chosen, as a cursory analysis shows that numbers between the max and 300 encapsulate countries with economies known to pollute, as well as some countries that are a surprise, so it seems like a good place to begin our analysis. So, countries with a ratio of co2 to gdp over 300, will be labeled as 'high' and those below 300 will be labeled as 'low’ in the  ‘emission_ratio’ column.
To ready the data for a machine learning model, that categorical data was encoded. I used the Label Encoder method from the scikit learn library to encode any features where the data was a string, the 'country' and 'emission_ratio' columns. The data was changed from a string to a number for each unique entry.
### Feature Selection
The X variable, or independent variable, holds all the features that effect the y variable, or dependent variable, 'emission_ratio.' The X features include 'Country', 'Year', 'CO2', 'Population', 'GDP', 'Temperature', 'GDP_per_Capita', 'CO2_per_Capita', and 'CO2_per_unit_GDP'. The Emission_Ratio indicates the relationship for each country between GDP output and CO2 emissions per person. The Emission_Ratio is effected for each country by each feature held in the X variable.
### Splitting into Training/Testing
The data was split into training and testing sets using the train_test_split method from the scikit learn library. It was trained using the Balanced Random Forest Classifier from the imbalanced-learn package.
### Model Choice
We chose a balanced random forest model classifier for this analysis. A BRM was chosen because random forest models are efficient, are not prone to overfitting, and are able to rank feature importance. However, a BRM is something of a black box algorithm, so there is little control over what the model does.
A BRM is an ensemble classifier that works by combining multiple decision tree algorithms to improve accuracy. A random forest model randomly selects a subset of features from the training set and fits a decision tree to each one. By choosing different features for each tree, each tree is independent and improves the ensemble prediction. The Balanced RF works by performing a random undersampling of the majority class to correct any imbalance between classes. In this case, there was not an extreme imbalance between classes to begin with, but every little bit helps to improve accuracy.  
### Model Validation
Using the test data to validate the model shows that this model performs with 99% accuracy. The classification report, furthermore, shows that there is high accuracy for both the high and low classes, for a well-balanced model.

