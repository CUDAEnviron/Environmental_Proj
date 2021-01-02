# Environmental Project

## Database Storage

- We are using a Postgres SQL database hosted by Heroku for our project.

- Our first base data file is Resources/<b>owid-co2-data.csv</b> and has 24016 rows and 38 columns.

- This file has been uploaded to the <b>co2_data</b> table in the Postgres database.<br><br>
<img src=Resources/co2_data_db.png></img><br>

- The <b>CO2_Data_to_Database.ipynb</b> Jupyter Notebook shows how the connection is made to the Postgres database and how the data is uploaded to the co2_data table.

- We will be processing this data and adding other sets of data as we continue to develop this project.
