# New York City Taxi Ride Data Engineering Project
## Navigation / Quick Access
Quickly move to section you are interested in by clicking on appropriate link:
- [Overview](https://github.com/Jucodez/Jucodez-Taxi-ride-data-engineering-project/tree/main#overview)
- [Project Objective](https://github.com/Jucodez/Jucodez-Taxi-ride-data-engineering-project/tree/main#project-objective)
- [Project Architecture](https://github.com/Jucodez/Jucodez-Taxi-ride-data-engineering-project/tree/main#project-architecture)
- [Dataset](https://github.com/Jucodez/Jucodez-Taxi-ride-data-engineering-project/tree/main#dataset)
- [Technologies](https://github.com/Jucodez/Jucodez-Taxi-ride-data-engineering-project/tree/main#technologies)
- [Reproducing Project](https://github.com/Jucodez/Jucodez-Taxi-ride-data-engineering-project/tree/main#reproducing-project) (long section)
- [Dashboard](https://github.com/Jucodez/Jucodez-Taxi-ride-data-engineering-project/tree/main#dashboard)

---
## Overview
This project extracts, transforms, loads and analyzes data from the [NYC Taxi and Limousine Commission](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page).

Relevant data is collected, and transformations are carried out to support the analysis of revenue generation by the commission through taxi rides.

---
## Project Objective
Successfully move data from Source, transform, and Visualize in a dashboard.
Key Deliverables:
- Create a data pipeline to process data in batches from the [NYC Taxi and Limousine Commission](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page) data records to a data warehouse.
- Create an analytical engineering model to transform the data for analysis.
- Create a dashboard to present key revenue insights to stakeholders.

---
## Project Architecture
![DAG](https://github.com/user-attachments/assets/33af18d8-a345-4d99-829e-09a5263986cf)


The data architecture is an overview of the data pipeline. Key points are:
- A mage ETL pipeline from the [NYC Taxi and Limousine Commission](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page) data records to a GCS bucket
- A mage ETL pipeline from the GCS bucket to the Big Query data warehouse.
- An analytical engineering model built on top of the Big Query data warehouse using DBT to further transform the data
- A dashboard built with Power BI for Analysis
---
## Dataset
The project's data source can be accessed [here](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page)

Two months of data, June and July 2024, were collected from the [NYC Taxi and Limousine Commission](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page) data records for green and yellow service taxis.

This data was then analyzed to present insights into the revenue of the commission for these two months


Yellow Taxi Dataset:

Field name description
- VendorID - A code indicating the TPEP provider that provided the record
- tpep_pickup_datetime - The date and time when the meter was engaged.
- tpep_dropoff_datetime - The date and time when the meter was disengaged.
- Passenger_count - The number of passengers in the vehicle (this is a driver-entered value).
- Trip_distance - The elapsed trip distance in miles reported by the taximeter.
- PULocationID - TLC Taxi Zone in which the taximeter was engaged.
- DOLocationID - TLC Taxi Zone in which the taximeter was disengaged.
- RateCodeID - The final rate code in effect at the end of the trip.
- Store_and_fwd_flag - Indicates whether the trip record was held in vehicle memory before sending to the vendor (“store and forward”) due to no connection to the server.
- Payment_type - A numeric code signifying how the passenger paid for the trip.
- Fare_amount - The time-and-distance fare calculated by the meter.
- Extra - Miscellaneous extras and surcharges, including the $0.50 and $1 rush hour and overnight charges.
- MTA_tax - $0.50 MTA tax automatically triggered based on the metered rate in use.
- Improvement_surcharge - $0.30 improvement surcharge assessed for trips at the flag drop. The surcharge began being levied in 2015.
- Tip_amount - Tip amount – this field is automatically populated for credit card tips. Cash tips are not included.
- Tolls_amount - Total amount of all tolls paid during the trip.
- Total_amount - The total amount charged to passengers (does not include cash tips).
- Congestion_Surcharge - Total amount collected for NYS congestion surcharge during the trip.
- Airport_fee - $1.25 for pickups only at LaGuardia and John F. Kennedy Airports.


Green Taxi Dataset:

Field name description

- VendorID - A code indicating the LPEP provider that provided the record.
- lpep_pickup_datetime - The date and time when the meter was engaged.
- lpep_dropoff_datetime - The date and time when the meter was disengaged.
- Passenger_count - The number of passengers in the vehicle (this is a driver-entered value).
- Trip_distance - The elapsed trip distance in miles reported by the taximeter.
- PULocationID - TLC Taxi Zone in which the taximeter was engaged.
- DOLocationID - TLC Taxi Zone in which the taximeter was disengaged.
- RateCodeID - The final rate code in effect at the end of the trip.
- Store_and_fwd_flag - Indicates whether the trip record was held in vehicle memory before sending to the vendor (“store and forward”) due to no connection to the server.
- Payment_type - A numeric code signifying how the passenger paid for the trip.
- Fare_amount - The time-and-distance fare calculated by the meter.
- Extra - Miscellaneous extras and surcharges, including the $0.50 and $1 rush hour and overnight charges.
- MTA_tax - $0.50 MTA tax automatically triggered based on the metered rate in use.
- Improvement_surcharge - $0.30 improvement surcharge assessed on hailed trips at the flag drop. The surcharge began being levied in 2015.
- Tip_amount - Tip amount – this field is automatically populated for credit card tips. Cash tips are not included.
- Tolls_amount - Total amount of all tolls paid during the trip.
- Total_amount - The total amount charged to passengers (does not include cash tips).
- Trip_type - A code indicating whether the trip was a street-hail or a dispatch. It is automatically assigned based on the metered rate in use but can be altered by the driver.



---
## Technologies
- [Docker](https://www.docker.com/):- Containerization of applications -- build, share, run, and verify applications anywhere — without tedious environment configuration or management.
- [Google Cloud Storage](https://cloud.google.com/storage) GCS - Data Lake for storage
- [Google Cloud BigQuery](https://cloud.google.com/bigquery) - Data warehouse for analytical purposes
- [Mage](https://docs.mage.ai/introduction/overview) -  Data and workflow orchestration 
- [Dbt](https://www.getdbt.com/)- For analytics engineering via data transformation
- [Power BI]([https://lookerstudio.google.com/](https://www.microsoft.com/en-us/power-platform/products/power-bi)) - Data Visualization

---
## Project Overview
This section will give a thorough breakdown of how to reproduce this project

### 1) Mage
Two Mage ETL pipeline were built to load data from the [NYC Taxi and Limousine Commission](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page) data records to a GCS Bucket. One for the green taxi records and another for the yellow taxi records. These pipeline collected data for two months for their respective service concatenated it and loaded it to the GCS Bucket

Yellow taxi records ingestion pipeline

![Screenshot (1003)](https://github.com/user-attachments/assets/a3eb6306-6973-482e-a235-c609cdaa9270)

Green taxi records ingestion pipeline

![Screenshot (1004)](https://github.com/user-attachments/assets/ce6e53c9-17c1-427c-ace2-d0ec7c33e56b)

Two more Mage EL pipelines were built to load the data from the GCS Bucket to Big Query. One for the green taxi records and another for the yellow taxi records. 

Yellow taxi records staging pipeline

![Screenshot (1005)](https://github.com/user-attachments/assets/e41c886d-47b8-4b6a-8cdd-b932d905e812)

Green taxi records staging pipeline

![Screenshot (1006)](https://github.com/user-attachments/assets/f922f12d-a364-48f2-9e0c-c9771ebab210)

### 2) Data Build Tool (DBT)

DBT was used to build and deploy an analytical model to transform the data.

In addition to the dataset gotten from [NYC Taxi and Limousine Commission](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page) data records, the comission also provides a taxi zone lookup table to correctly identify boroughs. This was added as a seed in the dbt model

![Screenshot (1007)](https://github.com/user-attachments/assets/7190b0a1-c81a-47e8-a4e1-3e251934a8a2)

### 4) Analytics

Using power BI, the following dashboard was built

![Screenshot (1008)](https://github.com/user-attachments/assets/b7df12de-01d8-4ec3-8e90-978e15300f1d)






