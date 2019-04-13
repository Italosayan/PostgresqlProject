### Sparkify: Give a spark to your playlist.

##### Purpose

The purpose of this project is to provide tables to analyze the songs played by users. It is going to be queried by the analytics team. The data is not designed for transactional workloads.

##### Schema

The schema is star and the fact table is songplay table. The key information is available there. The dimension tables have characteristics of the rest of the entities the company always works with. Users, songs, artists, and time.
Other decisions in the schema are:
songplay_id as a serial variable
On conflict clauses in the user, song, artists, and time tables to avoid duplication.
In the case of the user table if the user_id is duplicated we make sure to store level updates in the database.

##### ETL Pipeline:

The ETL Pipeline in its current version processes one row at a time. We have a lot of insert calls that can be optimized. Also, it is heavily relliant on pandas.

##### How to run the files:

The first part of the process is to create the tables. Hopefully the analytics team doesn't have to run this file. In the '/home/workspace' directory run the following command.

```python
python create_tables.py
```

The script creates the songplays, users, songs, artist, and time tables. The SQL queries that are executed by the create_tables script are located in the *sql_queries.py* file.
Next, in order to input all the json files to the database we need to run the etl file.

```python
python etl.py
```

The script connects to the **sparkifydb** locally and processes the *song_data* and *log_data* directories. It also executes files in the *sql_queries.py* script.

##### Dependencies:

1. Pandas, os, glob ,psycopg2
2. Postgresql, jupyter
