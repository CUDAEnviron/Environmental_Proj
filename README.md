# Climate Change and GDP

Climate change has become a significant problem that affects the very existence of life on the planet. Climate change is caused by human activity and the growth of industry over the last century. Global warming is the long-term heating of Earth’s climate system observed since the pre-industrial period. It’s causes are primarily fossil fuel burning, which increases heat-trapping greenhouse gas levels in Earth’s atmosphere. This has caused a dramatic increase of temperatures on both land and water surfaces, meltdown of ice caps, rise in sea levels, increase in the magnitude and frequency of hurricanes, and extinction of many species. It is hoped that these adverse effects can be slowed down or reversed with changes in human activity and proper education. 

The impact of human industry on the world climate has been obvious for a generation, but response to correct the issues have been met with slow action by world governments.  The reason often cited is the economic impact of changing the ways things have always been done.  Gross Domestic Product is the total value of goods and services produced within a country and it functions as scorecard of a country’s economic health.  GDP can be used as an indicator of a country’s economic growth.

This project’s goal is to show, using historical GDP and CO2 emissions data, the correlation between economic growth and CO2 emissions.  We aim to identify the current and long-term connection between greenhouse gas emissions and economic activity across countries, and ultimately recognize economic gains from reducing carbon footprint. 

## The Question
Can a country make gains in terms of GDP without correlating gains in CO2 emissions?  In other words, is it possible to succeed economically without destroying the planet?

## Project Dashboard
Please use the links below to view our project presentation slides, visualization dashboard on Tableau, or to browse our data:

[Presentation](https://docs.google.com/presentation/d/1QSeTHzu5lJcCZ3nt-1JJPHDhVycquPNRZLXf4xkHaJw/edit?ts=5fff77e5#slide=id.p)

[Visualization Dashboard](https://public.tableau.com/profile/kamrul7767#!/?newProfile=&activeTab=0)

[Data Browser Dashboard](https://cudaenviron.github.io/Environmental_Proj/)

Or continue reading for a project overview.  The Tableau charts are also shown at the bottom of this document.

## Project Overview
### Data Source 
We used two main sources of data for this project:

 - OWID-co2-data.csv 
   - A dataset on CO2 and greenhouse gas emissions compiled by Hannah Ritchie, Max Roser and Edouard Mathieu for Our World in Data, a website that compiles research and data “to make progress against the world’s largest problems.”  [Our World in Data](https://ourworldindata.org/co2-and-other-greenhouse-gas-emissions)
   
- clean_Global_temps_1901_to_2016.csv
  - A dataset on that tracks the average yearly temperature in Celsius for each country over the last 115 years.  Downloaded from the Climate Change Knowledge Portal of the World Bank Group.  [World Bank Group](https://climateknowledgeportal.worldbank.org/download-data)

### Database
We are using a multi-user Postgres SQL database hosted by Heroku for our project.

Here is the ERD of our database:
![ERD.png](https://github.com/CUDAEnviron/Environmental_Proj/blob/main/Updated%20Images/ERD.png)

- Our first base data file is Resources/<b>owid-co2-data.csv</b> and has 24016 rows and 38 columns.

- This file has been uploaded to the <b>co2_data</b> table in the Postgres database.

- The <b>CO2_Data_to_Database.ipynb</b> Jupyter Notebook shows how the connection is made to the Postgres database and how the data is uploaded to the co2_data table.

- Our second base data file is Resources/<b>clean_Global_temps_1901_to_2016.csv</b> and has 22736 rows and 4 columns.

- This file has been uploaded to the <b>temperature_data</b> table in the Postgres database.

- The database tables will be read into <b>ML_model.ipynb</b> for analysis.

### Data Exploration and Machine Learning Model

#### Preliminary Data Cleaning and Preprocessing
After importing both tables from the database and converting them to dataframes in the ML_model notebook, each dataframe was cleaned before being merged for initial analysis. In the CO2 data, the NAs were dropped, as well as any entries in the ‘country’ column that didn’t represent an actual country.  A new clean CO2 dataframe was created with only the most relevant columns.  The temperature data was cleaned as well, and then merged with the clean CO2 data.  This combined dataset was then examined to establish if there is a correlation between CO2 emissions and a country’s GDP output.  

To determine a baseline for whether a country is a disproportionate polluter, we broke out the data for 2016, the most recent year in the dataset. We exported it as a CSV to get a full look at the data and pick a baseline for "bad" ratio of GDP to CO2 per capita.  After looking at the 2016 data in Excel, a new column is created to indicate CO2 production per unit of GDP, by dividing 'co2' by 'gdp per capita' (multiplied by 100000 to make the result more readable). By calculating the CO2 produced for each unit of GDP_per_Capita, it establishes a ratio of pollution to production.  A high ratio means that pollution is outstripping production, which shows that while an economy may be economically robust, it can be environmentally destructive.  

A baseline of 300 is chosen, as a cursory analysis shows that numbers between the max and 300 encapsulate countries with economies known to pollute, as well as some countries that are a surprise, so it seems like a good place to begin our analysis. So, countries with a ratio of CO2 to GDP over 300, will be labeled as 'High' and those below 300 will be labeled as 'Low’ in the ‘emission_ratio’ column.

![emissionsratio.PNG](https://github.com/CUDAEnviron/Environmental_Proj/blob/main/Updated%20Images/emissionsratio.PNG)

To ready the data for a machine learning model, that categorical data was encoded. The Label Encoder method from the scikit learn library was used to encode any features where the data was a string, the 'country' and 'emission_ratio' columns. The data was changed from a string to a number for each unique entry.

#### Feature Selection
The X variable, or independent variable, holds all the features that effect the y variable, or dependent variable, 'emission_ratio.' The X features include 'Country', 'Year', 'CO2', 'Population', 'GDP', 'Temperature', 'GDP_per_Capita', 'CO2_per_Capita', and 'CO2_per_unit_GDP'. The Emission_Ratio indicates the relationship for each country between GDP output and CO2 emissions per person. The Emission_Ratio is effected for each country by each feature held in the X variable.

#### Splitting into Training/Testing
The data was split into training and testing sets using the train_test_split method from the scikit learn library. It was trained using the Balanced Random Forest Classifier from the imbalanced-learn package.

#### Model Choice
We chose a balanced random forest model classifier for this analysis. A BRM was chosen because random forest models are efficient, are not prone to overfitting, and are able to rank feature importance. However, a BRM is something of a black box algorithm, so there is little control over what the model does.
A BRM is an ensemble classifier that works by combining multiple decision tree algorithms to improve accuracy. A random forest model randomly selects a subset of features from the training set and fits a decision tree to each one. By choosing different features for each tree, each tree is independent and improves the ensemble prediction. The Balanced RF works by performing a random under-sampling of the majority class to correct any imbalance between classes. In this case, there was not an extreme imbalance between classes to begin with, but every little bit helps to improve accuracy.  

#### Model Validation
Using the test data to validate the model shows that this model performs with 99% accuracy. The confusion matrix shows that all of the countries classified as ‘High’ were classified correctly and all but one of the countries classified as ‘Low’ were classified correctly.

![ml4.PNG](https://github.com/CUDAEnviron/Environmental_Proj/blob/main/Updated%20Images/ml4.PNG)

### Final Analysis and Results

In the <b>High_Low_analysis.ipynb</b> notebook, final analysis is done to answer the question of whether a country could grow their economy without disproportionately polluting the earth.  This code performs and analysis on the High and Low groups that were established in the data exploration phase.  A for-loop is written that will loop through each country, and determine the GDP per Capita, Emission Ratio, CO2, and the Temperature for the first and last year available in the dataset.  A calculation is then done to determine the change over time for each of these indicators.  This code will separate all the countries in the dataset into groups depending on how their Emission Ratio changed over time.  Either Low to Low, High to Low, Low to High, or High to High.   It will also show how much GDP has increased or decreased, the change in CO2 output, and how the temperature has fluctuated over the time span given for each country.

The result is 4 dataframes.  The Low to Low and High to Low dataframes are merged into a new dataframe called good_job, because these countries have either maintained a low ratio or improved their ratio over the time span available.  These countries have done a good job.  The Low to High and High to High dataframes are merged into a new dataframe called bad_job, because these countries have either shown deteriorating emissions ratios or just maintained a high ratio over time.  These two dataframes can then be used to find the countries that performed the worst and best over time.

The worst polluters were determined by sorting the bad_job dataframe by CO2 change from highest to lowest. These countries have increased CO2 emissions the most over the time span of the dataframe.

To find the countries that had both poor emissions ratios and decreased GDP over time, the bad_job dataframe was sorted by GDP change from least to most.  These countries made the least gains in GDP, while either increasing CO2 output or not decreasing it enough to improve their emission ratio over time.

To find the countries that performed the best, the good job dataframe was filtered to only include those countries that have increased GDP per Capita AND decreased CO2 output.  This was determined by only including countries with a positive GDP change over time, and a negative CO2 change over time. The result was a dataframe with 12 countries.

### Conclusions

Saudi Arabia is determined to be the country that has increased emissions the MOST over time.  Saudi Arabia’s CO2 emissions have increased by 178 million tons from 1950 to 2016.  Even though their GDP increased by over 40,000, they had the most significant increase in emissions in this dataset over time.

![co2%20chart.PNG](https://github.com/CUDAEnviron/Environmental_Proj/blob/main/Updated%20Images/co2%20chart.PNG)

Afghanistan is determined to be the only country that has both decreased GDP output over time AND increased co2 emissions over time.  Afghanistan made negative gains in GDP over time at -697 and increased CO2 emissions by 2 million tons.  This CO2 increase is certainly not as significant as Saudi Arabia’s increase, but it is significant that Afghanistan has also decreased economic output while increasing emissions.

![gdp%20change.PNG](https://github.com/CUDAEnviron/Environmental_Proj/blob/main/Updated%20Images/gdp%20change.PNG)

12 countries were able to increase GDP output AND decrease CO2 output over the time span of this dataset.  Luxembourg performed the best out of these.

![winners.PNG](https://github.com/CUDAEnviron/Environmental_Proj/blob/main/Updated%20Images/winners.PNG)

In answer to our overall question of whether a country could experience economic growth while decreasing emissions, the answer is yes.  Out of the 156 countries represented in this dataset, 12 countries have been shown to have achieved this metric.  Luxembourg has decreased CO2 emissions the most by shedding 94 million tons since 1950, and increased GDP by over 50,000.  Luxembourg is a very small country, with a population of only about 600,000, so making economic gains while improving environmental metrics is a more achievable task than the same would be for other countries, but the accomplishment still cannot be ignored.

### Future Analysis

With more time we would like to perform another analysis that includes some of the factors within the countries that have performed the worst and best over time, such as the systems of government in each country, primary types of industry, and any environmental treaties or pledges made.  Factors such as these would help explain how some countries have been able to increase economic growth while decreasing emissions while others have failed in either or both metric.  It is encouraging to have data proving it is possible to both grow an economy and decrease emissions, but it would be beneficial to understand how, and to provide other countries with some actionable guidelines.

### Technologies Used
We used Jupyter Notebook to compose code written in Python, utilizing the Pandas software library for analysis.

Our data was stored in two tables on a PostgreSQL database hosted by Heroku.

A Balanced Random Forest classification model from the Scikit Learn library was used to analyze the data.

Tableau and Flourish were used to create visualizations and host the dashboard.

<b>Requirements.txt</b> shows the required packages and libraries needed to run this code.

## The below charts show summary data of our analysis of the Co2 data as it relates to GDP. 

![](https://github.com/CUDAEnviron/Environmental_Proj/blob/main/Updated%20Images/Co2%20Per%20GDP%20Bar%20Chart_2016.png)This Chart shows Co2 Per GDP by country.

![](https://github.com/CUDAEnviron/Environmental_Proj/blob/main/Updated%20Images/Co2%20Per%20GDP%20Bar%20Chart_2016_Desc.png)This Chart shows Co2 Per GDP by country in Descending Order. 

![](https://github.com/CUDAEnviron/Environmental_Proj/blob/main/Updated%20Images/Co2%20Per%20GDP%20Bar%20Chart_Top10_2016.png)This Chart shows Co2 Per GDP by country (Top 10 Countries)

![](https://github.com/CUDAEnviron/Environmental_Proj/blob/main/Updated%20Images/Co2%20Per%20GDP%20Box%20Grid_2016.png)This Chart shows Co2 Per GDP by country in Grid view. 

![](https://github.com/CUDAEnviron/Environmental_Proj/blob/main/Updated%20Images/Co2%20Per%20GDP%20Bar%20Chart_Historical.png)This Chart shows a historical view of Co2 Per GDP by country.

![](https://github.com/CUDAEnviron/Environmental_Proj/blob/main/Updated%20Images/Co2%20Per%20GDP%20Bar%20Chart_Map_2016.png)This Chart shows Co2 Per GDP by country in a map view.

![](https://github.com/CUDAEnviron/Environmental_Proj/blob/main/Updated%20Images/Dashboard.png)This Chart shows a dashboard of Co2 Per GDP by country.
