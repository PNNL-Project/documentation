# Devops Documentation

#### This documentation holds information about the following deployments:

AWS RDS
AWS EC2 Services + Health Checks
Grafana on EC2
Airflow in Docker on EC2
Influx DB on EC2
Predictions API + Redis on EC2
AWS Amplify
Deployment Costs

## AWS RDS
### Summary: 
RDS was used to host the MySQL database on AWS. Data was imported from a .csv file (found on the PNNL website)

### Relationship With Other Services: 
RDS was used to serve MySQL data for:
The react-app-redis-backend API
Supplying data to the airflow-data-pipeline
stores the machine learning outcomes by the airflow-data-pipeline.


### Additional Notes: 
Option 1: Directly import the .csv file into any MySQL server and name the database and table as indicated here. Use the default port 3306.  
Option 2: MySQL dump files can be found here 

## Services in Docker Containers

### Grafana on EC2
#### Summary: 
#### Relationship With Other Services:
#### Directions:
#### Additional Notes:

### Airflow in Docker on EC2
#### Summary:
#### Relationship With Other Services:
#### Directions:
#### Additional Notes:

InfluxDB (Docker)
#### Summary: 
A highly-optimized time-series database directly handing queries from the Grafana. Since AWS does not provide InfluxDB directly, we are running an InfluxDB docker container on a EC2 instance
#### Relationship With Other Services: 
It only serves the Grafana Dashboard
#### Directions:
#### Additional Notes: 
There is a simple bash shell script that will import the data into influxDB. The data source is consistent with MySQL database.

### Predictions API + Redis + cron (Docker)
#### Summary: 
A NodeJS express server handling two GET requests (query on a single day/a range of days) by reading data from Redis. The data in Redis is periodically supplied by the MySQL database by a cron job.
#### Relationship With Other Services: 
This server focus on providing data for the frontend react app
#### Directions:
#### Additional Notes: 
These three components are all containerized and are launched via docker compose; The cron job has been set to refresh the data every 3 hours while the duration of the data in Redis is 24 hours.

### Frontend React App (Docker)
#### Summary: The front end app is running on Docker as
#### Relationship With Other Services:
#### Directions:
#### Additional Notes:

### Deployment Costs
#### Summary:
#### Relationship With Other Services:
#### Directions:
#### Additional Notes:
