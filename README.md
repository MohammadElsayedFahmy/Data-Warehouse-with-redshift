# Song Play Analysis with S3 and Redshift
-------------------------


### Introduction
In this project, i'll apply what i've learned on data warehouses and AWS to build an ETL pipeline for a database hosted on Redshift. To complete the project, i will need to load data from S3 to staging tables on Redshift and execute SQL statements that create the analytics tables from these staging tables.

### Datasets

I'll be working with two datasets that reside in S3. Here are the S3 links for each:

+ **Song data: s3://udacity-dend/song_data**
+ **Log data: s3://udacity-dend/log_data**
+ **Log data json path: s3://udacity-dend/log_json_path.json**

### Song Dataset
The first dataset is a subset of real data from the **Million Song Dataset**. Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. For example, here are file paths to two files in this dataset.


+ **song_data/A/B/C/TRABCEI128F424C983.json**
+ **song_data/A/A/B/TRAABJL12903CDCF1A.json**

And below is an example of what a single song file, TRAABJL12903CDCF1A.json, looks like.

+ **{"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}**



### Log Dataset
The second dataset consists of log files in JSON format generated by this event simulator based on the songs in the dataset above. These simulate app activity logs from an imaginary music streaming app based on configuration settings.

The log files in the dataset you'll be working with are partitioned by year and month. For example, here are file paths to two files in this dataset.

+ **log_data/2018/11/2018-11-12-events.json**
+ **log_data/2018/11/2018-11-13-events.json**

### Database Schema
Star schema that contains 1 fact table (songplays) and 4 dimension tables (users, songs, artists and time).

**songplays**
+ **records in log data associated with song plays i.e. records with page NextSong**

**users**
+ **users in the app**

**songs**
+ **songs in music database**

**artists**
+ **artists in music database**

**time**
+ **timestamps of records in songplays broken down into specific units**

### How to Run

1. Create tables by running `create_tables.py`.

2. Execute ETL process by running `etl.py`.
