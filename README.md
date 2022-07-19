# Data Modeling with Postgres

### Sparkify ETL with Postgres and Python

<br>

**Introduction**

A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

They'd like a data engineer to create a Postgres database with tables designed to optimize queries on song play analysis, and bring you on the project. We need to create a database schema and ETL pipeline for this analysis. Then we will be able to test your database and ETL pipeline by running queries given to you by the analytics team from Sparkify and compare your results with their expected results.

<br>

**Project Description**

This project is to create a SQL analytics database for a music streaming startup called Sparkify. Sparkify's analytics team want to understand what songs users are listening on the company's music app. They need an easy way to query to their data. These data are stored in raw JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app on.

<br>

**Running the Python Scripts**

At the terminal:

1. python create\_tables.py
1. python etl.py

In IPython:

1. run create\_tables.py
1. run etl.py

<br>

**Database Schema**

We will use the Star Schema: one fact table consist of the measures associated with each event *songplays*, and referencing four dimensional tables *songs*, *artists*, *users* and *time*, each with a primary key that is being referenced from the fact table.

On why to use a relational database for this case:

- The data types are structured (we know before-hand the structure of the jsons we need to analyze, and where and how to extract and transform each field)
- The amount of data we need to analyze is not big enough to require big data related solutions.
- This structure will enable the analysts to aggregate the data efficiently
- Ability to use SQL that is more than enough for this kind of analysis
- We need to use JOINS for this scenario

![ERD Diagram](Aspose.Words.d5672974-acc5-466b-a355-47d4a8b6af6b.001.png)

This design will offer flexibility with the queries being used for analysis.


**ETL Process**

**Song Dataset**

The first dataset is a subset of real data from the Million Song Dataset. Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. For example, here are filepaths to two files in this dataset.

song\_data/A/B/C/TRABCEI128F424C983.json

song\_data/A/A/B/TRAABJL12903CDCF1A.json

And below is an example of what a single song file, TRAABJL12903CDCF1A.json, looks like.

{

`    `"num\_songs": 1,

`    `"artist\_id": "ARJIE2Y1187B994AB7",

`    `"artist\_latitude": null,

`    `"artist\_longitude": null,

`    `"artist\_location": "",

`    `"artist\_name": "Line Renaud",

`    `"song\_id": "SOUPIRU12A6D4FA1E1",

`    `"title": "Der Kleine Dompfaff",

`    `"duration": 152.92036,

`    `"year": 0

}

This information is parsed to populate the Songs and Artists Dimension tables.

<br>
<br>


**Log Dataset**

The log files in the dataset are partitioned by year and month. For example, here are filepaths to two files in this dataset.

log\_data/2018/11/2018-11-12-events.json

log\_data/2018/11/2018-11-13-events.json

This data contains information of which songs Users listened to at a specific time. Information is parsed to provide data for the Songplays Fact table and the Users and Time Dimension tables. The songplays.artist\_id and songplays.song\_id columns are populated by a lookup based on the Song Title, Artist Name and song Duration.

<br>
<br>


**Description of Files**

The data files, the project includes seven files:

1. ***create\_tables.py*:** drops and creates your tables. You run this file to reset your tables before each time you run your ETL scripts.
1. ***etl.ipynb*:** reads and processes a single file from *song\_data* and *log\_data* and loads the data into your tables. This notebook contains detailed instructions on the ETL process for each of the tables.
1. ***etl.py*:** reads and processes files from *song\_data* and *log\_data* and loads them into your tables. You can fill this out based on your work in the ETL notebook.
1. ***README.md*:** provides discussion on this project.
1. ***SparkStarSchema.png*:** *ERD* for star schema of this project
1. ***sql\_queries.py*:** contains all your sql queries, and is imported into the last three files above.
1. ***test.ipynb*:** displays the first few rows of each table to let us check on the database.



