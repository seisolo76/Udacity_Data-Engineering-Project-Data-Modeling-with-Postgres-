# Project: Data Modeling with Postgres

##### by Kelly Joseph 5-20-2020

## Introduction
A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.
They'd like a data engineer to create a Postgres database with tables designed to optimize queries on song play analysis, and bring you on the project. Your role is to create a database schema and ETL pipeline for this analysis. You'll be able to test your database and ETL pipeline by running queries given to you by the analytics team from Sparkify and compare your results with their expected results.
## Project Description
In this project, I have applied what I learned on data modeling with Postgres and built an ETL pipeline using Python. To complete the project, I needed to define fact and dimension tables for a star schema for a particular analytic focus, and write an ETL pipeline that transfers data from files in two local directories into these tables in Postgres using Python and SQL.
## Datasets
### Song Dataset
The first dataset is a subset of real data from the Million Song Dataset. Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. For example, here are filepaths to two files in this dataset.
```
song_data/A/B/C/TRABCEI128F424C983.json
song_data/A/A/B/TRAABJL12903CDCF1A.json
```
And below is an example of what a single song file, TRAABJL12903CDCF1A.json, looks like.
```python
{"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}
```
## Log Dataset
The second dataset consists of log files in JSON format generated by this event simulator based on the songs in the dataset above. These simulate activity logs from a music streaming app based on specified configurations.
The log files in the dataset you'll be working with are partitioned by year and month. For example, here are filepaths to two files in this dataset.
```
log_data/2018/11/2018-11-12-events.json
log_data/2018/11/2018-11-13-events.json
```
And below is an example of what the data in a log file, 2018-11-12-events.json, looks like.

![Alt text](https://github.com/seisolo76/Udacity_Data-Engineering-Project-Data-Modeling-with-Postgres-/blob/master/pics/log-data.png)
 
## Database Schema for Song Play Analysis
Using the song and log datasets, I created a star schema optimized for queries on song play analysis. This includes the following tables.
### Fact Table
     1.	songplays - records in log data associated with song plays i.e. records with page NextSong

          •	songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent
   
### Dimension Tables
      2.	users - users in the app  
           • user_id, first_name, last_name, gender, level
   
      3.	songs - songs in music database  
           • song_id, title, artist_id, year, duration
   
      4.	artists - artists in music database  
           • artist_id, name, location, latitude, longitude
   
      5.	time - timestamps of records in songplays broken down into specific units  
           • start_time, hour, day, week, month, year, weekday
## Visual Representation of the Table Structure

![Alt text](https://github.com/seisolo76/Udacity_Data-Engineering-Project-Data-Modeling-with-Postgres-/blob/master/pics/songplays%20schema.png)
 
## Files
### In addition to the data files, the project workspace includes six files:
#### • test.ipynb displays the first few rows of each table to let you check your database.
#### • create_tables.py drops and creates your tables. You run this file to reset your tables before each time you run your ETL scripts.
#### • etl.ipynb reads and processes a single file from song_data and log_data and loads the data into your tables. This notebook contains detailed instructions on the ETL process for each of the tables.
#### • etl.py reads and processes files from song_data and log_data and loads them into your tables. You can fill this out based on your work in the ETL notebook.
#### • sql_queries.py contains all your sql queries, and is imported into the last three files above.
#### • README.md provides discussion on your project.
## ETL Pipeline
Extract, transform, load (ETL) is the process of extracting data from one or more sources, manipulating the data and then inserting it into a database.
## Extracting the Data 
The data will be extracted from files in two directories 
•	/data/log_data and
•	/data/song_data.

I used the function pd.read_json to extract and move the data in a data frame. 
## Transform the Data
 In the data frame I am able to use only the columns that I want of the data. I can also break apart the time data into components (hour, day, week, month, year) . I also filtered the data by “Next Song”.
## Load the Data
Using the insert queries in the sql_queries.py I insert the data into the tables created by create_tables.py script. 
The test.ipynb was used to test the creation of tables and imported data.
The etl.ipynb was used to develop the ETL process and prepare the datasets for each table. I used that code to complete the etl.py which reads and processes all the files from the song_data and log_data directories and loads that into the sparkifydb database tables.
To run the ETL pipeline do the following:  
#### 1.	Run the create_table.py python script to create/reset the tables in the sparkifydb database.  
#### 2.	Run the etl.py python script to extract, transform, and load the data into the sparkifydb database.
Most of this Read Me is taken from the indroduction, Project Datasets, and Project Instructions of the this Project. 

