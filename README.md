# Project Documentation

This course project was developed for Northeastern University's course, Advance Software Development, in collaboration with Pacific Northwest National Laboratory. The project's goal was to increase awareness in building data. The project's mainly focused its efforts with analyzing, transforming, and visualizing metrics within the System's Engineering Building (SEB). [The PNNL Project Organization](https://github.com/PNNL-Project/) contains all the files and links required to get the PNNL Project running.

## PNNL Organization Components

The components within PNNL Project include:  

* **airflow-data-pipeline**: The ML data pipeline that queries MySQL daily to create predictions and store back in MySQL.
* **data-importers**: Software programs utilized to import data into the MySQL and Influx Databases.
* **documentation**: Overall documentation including instructions to setup the projects [(located in the devops folder)].(https://github.com/PNNL-Project/documentation/tree/main/devops)
* **grafana-services**: The Grafana dashboard files and instructions along with the Influx DB files.
* **ml-models**: ML models and the code used to develop them.
* **mysql-files**: Documentation and links for the database structures and the content of the tables (using mysqldump).
* **react-app**: The 3 components that create the visualization and alerts: Hunting service, PNNL-Frontend-React, React-App-Redis-Backend (Predictions API).



