**Introduction:
-
A music streaming startup, Sparkify, has grown their user base and song database and want to move their processes and data onto the cloud. Their data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

**This projects applies:
-
An ETL pipeline that extracts their data from S3, stages them in Redshift, and transforms data into a set of dimensional tables for their analytics team to continue finding insights into what songs their users are listening to with ETL pipeline for a database hosted on Redshift while loading the data from S3 to staging tables on Redshift and execute SQL statements that create the analytics tables from these staging tables.

### Data Schema
#### Fact Table
* **songplays** - records in log data associated with song plays i.e. records with page `NextSong`
    * `songplay_id`, `start_time`, `user_id`, `level`, `song_id`, `artist_id`, `session_id`, `location`, `user_agent`

#### Dimension Tables
* **users** - users in the app
    * `user_id`, `first_name`, `last_name`, `gender`, `level`
* **songs** - songs in music database
    * `song_id`, `title`, `artist_id`, `year`, `duration`
* **artists** - artists in music database
    * `artist_id`, `name`, `location`, `lattitude`, `longitude`
* **time** - timestamps of records in <b>songplays</b> broken down into specific units
    * `start_time`, `hour`, `day`, `week`, `month`, `year`, `weekday`
    
### ETL pipeline:
1- Loads the data both from S3 buckets.
2- Stage the loaded data.
3- Transform the data into the above described data schema.

### Project Repository
1-Create_tables.py runs the DROP statements to drop tables if the tables already exist. This way, you can run create_tables.py whenever you want to reset your database and test your ETL pipeline.SQL and also runs the CREATE statement for the required fact and dimension tables.
2-Running etl.py extract the data from S3 to staging tables on Redshift and then load data from staging tables to analytics tables on Redshift.
3-sql_queries.py where SQL statements are defined, which are then used by etl.py, create_table.py.
4-dwh.cfg contains redshift database and IAM role info to connect the project with the Redshift cluster, IAM role and the S3 bucket.
5-Finally, this file is the README.md for the project documentation.

### Setup:
1- Setup a redshift cluster on AWS and input the connection fields in `dwh.cfg`.
2- Create the required database structure by running `create_tables.py`.
3- Process the data from the S3 data sources by running `etl.py`.
