# Uber Data Engineering End-to-End Project

## Objective

In this project, I designed and implemented an end-to-end data pipeline that consists of several stages:
1. Extracted data from NYC Trip Record Data website and loaded into Google Cloud Storage for further processing.
3. Transformed and modeled the data using fact and dimensional data modeling concepts using Python on Jupyter Notebook.
4. Using ETL concept, I orchestrated the data pipeline on Mage AI and loaded the transformed data into Google BigQuery.
5. Developed a dashboard on Looker Studio.

As this is a data engineering project, my emphasis is primarily on the engineering aspect with a lesser emphasis on analytics and dashboard development.

The sections below will explain additional details on the technologies and files utilized.

## Table of Content

- [Dataset Used](#dataset-used)
- [Technologies](technologies)
- [Data Pipeline Architecture](#data-pipeline-architecture)
- [Date Modeling](#data-modeling)
- [Step 1: Cleaning and Transformation](#step-1-cleaning-and-transformation)
- [Step 2: Storage](#step-2-storage)
- [Step 3: ETL / Orchestration](#step-3-etl--orchestration)
- [Step 4: Analytics](#step-4-analytics)

## Dataset Used

This project uses the TLC Trip Record Data which include fields capturing pick-up and drop-off dates/times, pick-up and drop-off locations, trip distances, itemized fares, rate types, payment types, and driver-reported passenger counts.

More info about dataset can be found in the following links:
- Website: https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page
- Data Dictionary: https://www.nyc.gov/assets/tlc/downloads/pdf/data_dictionary_trip_records_yellow.pdf
- Raw Data (CSV): https://github.com/kdr47101/data-engineering/blob/main/Uber%20Project/uber_data.csv

## Technologies

The following technologies are used to build this project:
- Language: Python, SQL
- Extraction and transformation: Jupyter Notebook, Google BigQuery
- Storage: Google Cloud Storage
- Orchestration: [Mage AI](https://www.mage.ai)
- Dashboard: [Looker Studio](https://lookerstudio.google.com)

## Data Pipeline Architecture

<img width="897" alt="Screenshot 2023-05-08 at 11 49 09 AM" src="https://user-images.githubusercontent.com/81607668/236729698-65e193bc-75ee-4ea6-9040-f33f5f2958cb.png">

Files in the following stages:
- Step 1: Cleaning and transformation - [Uber Data Engineering.ipynb](https://github.com/kdr47101/data-engineering/blob/main/Uber%20Project/Uber%20Data%20Engineering.ipynb)
- Step 2: Storage
- Step 3: ETL, Orchestration - Mage: [Extract](https://github.com/kdr47101/data-engineering/blob/main/Uber%20Project/Mage/uber_load_data.py), [Transform](https://github.com/kdr47101/data-engineering/blob/main/Uber%20Project/Mage/uber_transformation.py), [Load](https://github.com/katiehuangx/data-engineering/blob/main/Uber%20Project/Mage/uber_gbq_load.py)
- Step 4: Analytics - [SQL script](https://github.com/kdr47101/data-engineering/blob/main/Uber%20Project/sql_script.sql)
- Step 5: [Dashboard](https://github.com/kdr47101/data-engineering/blob/main/Uber%20Project/Uber_Dashboard.pdf)

## Data Modeling

The datasets are designed using the principles of fact and dim data modeling concepts. 

![Data Model](https://user-images.githubusercontent.com/81607668/236725688-995b6049-26c1-440f-b523-7c6c10d507ba.png)

## Step 1: Cleaning and Transformation

In this step, I loaded the CSV file into Jupyter Notebook and carried out data cleaning and transformation activities prior to organizing them into fact and dim tables.

Here's the specific cleaning and transformation tasks that were performed:
1. Converted `tpep_pickup_datetime` and `tpep_dropoff_datetime` columns into datetime format.
2. Removed duplicates and reset the index.

## Step 2: Storage

## Step 3: ETL / Orchestration

1. Begin by launching the SSH instance and running the following commands below to install the required libraries.

```python
# Install python and pip 
sudo apt-get install update

sudo apt-get install python3-distutils

sudo apt-get install python3-apt

sudo apt-get install wget

wget https://bootstrap.pypa.io/get-pip.py

sudo python3 get-pip.py

# Install Google Cloud Library
sudo pip3 install google-cloud

sudo pip3 install google-cloud-bigquery

# Install Pandas
sudo pip3 install pandas
```

2. After that, I install the Mage AI library from the [Mage AI GitHub](https://github.com/mage-ai/mage-ai#using-pip-or-conda). Then, I create a new project called "uber_de_project".

```python 
# Install Mage library
sudo pip3 install mage-ai

# Create new project
mage start demo_project
```

3. Next, I conduct orchestration in Mage by accessing the external IP address through a new tab. The link format is: `<external IP address>:<port number>`.

After that, I create a new pipeline with the following stages:
- Extract: [load_uber_data](https://github.com/kdr47101/data-engineering/blob/main/Uber%20Project/Mage/uber_load_data.py)
- Transform: [transform_uber](https://github.com/kdr47101/data-engineering/blob/main/Uber%20Project/Mage/uber_transformation.py)
- Load: [load_gbq](https://github.com/kdr47101/data-engineering/blob/main/Uber%20Project/Mage/uber_load_data.py)

Before executing the Load pipeline, I download credentials from Google API & Credentials and then update them accordingly in the `io_config.yaml` file within the same pipeline. This step is essential for granting authorization to access and load data into Google BigQuery.

## Step 4: Analytics

After running the Load pipeline in Mage, the fact and dim tables are generated in Google BigQuery.

***
