# Environmental Project

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


