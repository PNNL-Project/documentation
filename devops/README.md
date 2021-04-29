# Devops Documentation

#### This documentation holds information about the following deployments and information:

- AWS RDS
- Airflow in Docker on EC2
- Predictions API + Redis on EC2
- AWS Amplify
- Grafana
- Influx DB
- AWS Deployment Costs

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
Option 2: MySQL information and dump files can be found [here](https://github.com/PNNL-Project/mysql-files)

## Services in Docker Containers

### Grafana on EC2

#### Summary:

Grafana is used by the front end react app to show dashboards and visualizations.

#### Relationship With Other Services:

Grafana is used by the front end react app to show dashboards and capitalization
Grafana talks to influxdb to get the cost

#### Additional Notes:

If the mailing address of grafana has to changed please change the grafana.ini file in <grafana-docker-link>

### Airflow in Docker on EC2

#### Summary:

Airflow is an open-source work load management problem.

#### Relationship With Other Services:

Airflow queries the MySQL database to create prediction labels that are stored back into the MySQL database.

#### Deployment Directions:

Please refer to the readme located in the airflow-data-pipeline repo [here](https://github.com/PNNL-Project/airflow-data-pipeline/blob/master/airflow/Readme.md)

### InfluxDB (Docker)

#### Summary:

A highly-optimized time-series database directly handing queries from the Grafana. Since AWS does not provide InfluxDB directly, we are running an InfluxDB docker container on a EC2 instance

#### Relationship With Other Services:

It only serves the Grafana Dashboard

#### Additional Notes:

There is a simple bash shell script that will import the data into influxDB. The data source is consistent with MySQL database.

### Predictions API + Redis + cron (Docker)

#### Summary:

A NodeJS express server handling two GET requests (query on a single day/a range of days) by reading data from Redis. The data in Redis is periodically supplied by the MySQL database by a cron job.

#### Relationship With Other Services:

This server focus on providing data for the frontend react app

#### Additional Notes:

These three components are all containerized and are launched via docker compose; The cron job has been set to refresh the data every 3 hours while the duration of the data in Redis is 24 hours. For the detailed implementation & usage, please see [here](https://github.com/PNNL-Project/react-app)

### Alert Service (Docker)

### Summary:

Alert service is used to create alerts by the front end

### Relationship With Other Services:

Alert service is used by the front end react app to create visualize hunting events found within the data.


### Deployment Costs

Summarized Devops Cost Report for all the AWS Services

The estimates are provided for each month for services with recommended resources


![image](https://user-images.githubusercontent.com/56701482/115756361-222b7180-a36c-11eb-8498-6cccbbfb0a23.png)




More detailed Cost Report can be found at 

https://docs.google.com/presentation/d/1bXRQjJtvxacumiZao05njhjTySpyTQK3g5xDYKVkU2w/edit#slide=id.gaf43eba715_0_0







Cost for deploying Docker Images


We have created Docker images for all the services and have deployed them in EC2. We recommend to use a instance with 16GB RAM and 200 GB space. The cost of running the instance for a month is

https://calculator.aws/#/estimate?id=12ff3ee39c622bcc1e0686151a43e3ccd39366e1


 
### AWS Deployment Costs

Please see `DevOps Cost Report.pdf`

