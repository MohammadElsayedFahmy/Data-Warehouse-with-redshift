# Song Play Analysis with S3 and Redshift
-------------------------


### Introduction
In this project, i'll apply what i've learned on data warehouses and AWS to build an ETL pipeline for a database hosted on Redshift. To complete the project, i will need to load data from S3 to staging tables on Redshift and execute SQL statements that create the analytics tables from these staging tables.

### Datasets

You'll be working with two datasets that reside in S3. Here are the S3 links for each:

Song data: **s3://udacity-dend/song_data**
Log data: **s3://udacity-dend/log_data**
Log data **json path: s3://udacity-dend/log_json_path.json**

### Song Dataset
The first dataset is a subset of real data from the **Million Song Dataset**. Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. For example, here are file paths to two files in this dataset.


+ **song_data/A/B/C/TRABCEI128F424C983.json**
+ **song_data/A/A/B/TRAABJL12903CDCF1A.json**

And below is an example of what a single song file, TRAABJL12903CDCF1A.json, looks like.

+ **{"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}**


The **Redshift** service is where data will be ingested and transformed, in fact though `COPY` command we will access to the JSON files inside the buckets and copy their content on our *staging tables*.

### Database Schema
We have two staging tables which *copy* the JSON file inside the  **S3 buckets**.
#### Staging Table
+ **staging_songs** - info about songs and artists
+ **staging_events** - actions done by users (which song are listening, etc.. )


I createa a star schema optimized for queries on song play analysis. This includes the following tables.

#### Fact Table
+ **songplays** - records in event data associated with song plays i.e. records with page `NextSong`

#### Dimension Tables
+ **users** - users in the app
+ **songs** - songs in music database
+ **artists** - artists in music database
+ **time** - timestamps of records in **songplays** broken down into specific units



### Data Warehouse Configurations and Setup
* Create a new `IAM user` in your AWS account
* Give it AdministratorAccess and Attach policies
* Use access key and secret key to create clients for `EC2`, `S3`, `IAM`, and `Redshift`.
* Create an `IAM Role` that makes `Redshift` able to access `S3 bucket` (ReadOnly)
* Create a `RedShift Cluster` and get the `DWH_ENDPOIN(Host address)` and `DWH_ROLE_ARN` and fill the config file.

### ETL Pipeline
+ Created tables to store the data from `S3 buckets`.
+ Loading the data from `S3 buckets` to staging tables in the `Redshift Cluster`.
+ Inserted data into fact and dimension tables from the staging tables.

### Project Structure

+ `create_tables.py` - This script will drop old tables (if exist) ad re-create new tables.
+ `etl.py` - This script executes the queries that extract `JSON` data from the `S3 bucket` and ingest them to `Redshift`.
+ `sql_queries.py` - This file contains variables with SQL statement in String formats, partitioned by `CREATE`, `DROP`, `COPY` and `INSERT` statement.
+ `dhw.cfg` - Configuration file used that contains info about `Redshift`, `IAM` and `S3`

### How to Run

1. Create tables by running `create_tables.py`.

2. Execute ETL process by running `etl.py`.
