# Project Documentation

This course project was developed for Northeastern University's course, Advance Software Development, in collaboration with Pacific Northwest National Laboratory. The project's goal was to increase awareness in building data. The project's mainly focused its efforts with analyzing, transforming, and visualizing metrics within the System's Engineering Building (SEB). [The PNNL Project Organization](https://github.com/PNNL-Project/) contains all the files and links required to get the PNNL Project running.

## PNNL Organization Components

The components within PNNL Project include:  
![](images/system-design-labels.png)

1. **airflow-data-pipeline**: The ML data pipeline that queries MySQL daily to create predictions and store back in MySQL.
2. **data-importers**: Software programs utilized to import data into the MySQL and Influx Databases.
3. **documentation**: Overall documentation including instructions to setup the projects [(located in the devops folder)](https://github.com/PNNL-Project/documentation/tree/main/devops)
4. **grafana-services**: The Grafana dashboard files and instructions along with the Influx DB files.
5. **ml-models**: ML models and the code used to develop them.
6. **mysql-files**: Documentation and links for the database structures and the content of the tables (using mysqldump).
7. **react-app**: The 3 components that create the visualization and alerts: Hunting service, PNNL-Frontend-React, React-App-Redis-Backend (Predictions API).

## Project Flows

#### What was the flow used to create the various piechart/heatmap/stacked bar visualizations?
In order to create the visualizations, there were various steps involved:

1. Processed the SEB CSV data to import into CHISSL (data was aggregated into 1 hour windows for a particular metric for each device)
2. Used CHISSL help create a trainset to create machine learning models
3. Stored the SEB CSV data into the a denormalized table in MySQL using [TablePlus](https://docs.tableplus.com/)
4. A daily job was developed using Airflow and Python Code to do the following:
     * Reprocess SEB data from MySQL in the exact same format at step 1
     * Run the data through the machine learning model to create predictions on the yesterday's data
     * Store the predictions back into MySQL
5. A chron job queried MySQL (on an hourly basis) for the prediction labels and stores this into a redis cache
6. Upon loading the frontend react app, it queried the predictions api to retrieve the data stored into the redis cache
7. The frontend then displayed the data provided from the predictions api 


#### What was the flow used to create the alert service?
In order to visualize the alerts, this also involved various steps:

1. SEB Data was imported into the MySQL database using the [DataProcessor](https://github.com/PNNL-Project/data-importers/tree/master/DataProcessor) into a normalized table
2. The alert-service queries the data from MySQL every 15 mins to find hunting events
3. Upon loading, the alerts component of the frontend-react application will visualize these alerts

#### What was the flow used to create the Grafana Dashboards?

1. SEB given was historical, so the data set was transformed (shifting the timestamp to more recent dates so the simulated data appeared to be current)
2. SEB CSV Data was parsed, processed, and imported into Influx DB
3. Queries to InfluxDB were created to be displayed into the panels
