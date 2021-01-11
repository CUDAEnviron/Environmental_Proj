# Environmental Project

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


