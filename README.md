# Spotify Advanced SQL Project and Query Optimization 
[Click Here to get Dataset](https://www.kaggle.com/datasets/sanjanchaudhari/spotify-dataset)

![Spotify Logo](https://github.com/najirh/najirh-Spotify-Data-Analysis-using-SQL/blob/main/spotify_logo.jpg)

## Overview

This project focuses on analyzing a Spotify music dataset using PostgreSQL. The objective is to practice SQL concepts by exploring real-world music data and generating useful insights from tracks, albums, artists, streaming statistics, and user engagement.

The project starts by creating a database table, importing the dataset, and performing SQL queries ranging from basic data retrieval to advanced analytical queries. It also demonstrates query optimization techniques to improve database performance.

---

## 🎯 Project Objectives

- Import and manage Spotify dataset using PostgreSQL.
- Practice SQL from beginner to advanced level.
- Perform data analysis using aggregate functions.
- Learn GROUP BY, HAVING, Window Functions, CTEs, and Subqueries.
- Optimize SQL queries using indexes.
- Generate meaningful business insights from music streaming data.

---

## 📂 Dataset Information

The dataset contains details about Spotify tracks and their performance across different platforms.

### Dataset Includes

- Artist Name
- Track Name
- Album Name
- Album Type
- Danceability
- Energy
- Loudness
- Speechiness
- Acousticness
- Instrumentalness
- Liveness
- Valence
- Tempo
- Duration
- Views
- Likes
- Comments
- Streams
- Licensed Status
- Official Video
- Most Played Platform

---

## 🛠️ Technologies Used

- PostgreSQL
- pgAdmin 4
- SQL
- Git & GitHub

---

# Database Creation

sql
DROP TABLE IF EXISTS spotify;

CREATE TABLE spotify (
    artist VARCHAR(255),
    track VARCHAR(255),
    album VARCHAR(255),
    album_type VARCHAR(50),
    danceability FLOAT,
    energy FLOAT,
    loudness FLOAT,
    speechiness FLOAT,
    acousticness FLOAT,
    instrumentalness FLOAT,
    liveness FLOAT,
    valence FLOAT,
    tempo FLOAT,
    duration_min FLOAT,
    title VARCHAR(255),
    channel VARCHAR(255),
    views FLOAT,
    likes BIGINT,
    comments BIGINT,
    licensed BOOLEAN,
    official_video BOOLEAN,
    stream BIGINT,
    energy_liveness FLOAT,
    most_played_on VARCHAR(50)
);


---

# Project Workflow

### Step 1 – Data Preparation

- Download the Spotify dataset.
- Create the database table.
- Import the dataset into PostgreSQL.

---

### Step 2 – Data Exploration

Explore the dataset to understand its structure and identify important columns before writing analytical queries.

Examples include:

- Total number of tracks
- Unique artists
- Album types
- Platform distribution
- Missing values

---

### Step 3 – SQL Analysis

The project contains SQL questions categorized into three difficulty levels.
  
---

##  Questions

### Easy Level
1. Retrieve the names of all tracks that have more than 1 billion streams.
2. List all albums along with their respective artists.
3. Get the total number of comments for tracks where `licensed = TRUE`.
4. Find all tracks that belong to the album type `single`.
```sql
SELECT track
FROM spotify
WHERE album_type = 'single';
```

5. Count the total number of tracks by each artist.

### Medium Level
1. Calculate the average danceability of tracks in each album.
2. Find the top 5 tracks with the highest energy values.
```sql
SELECT track,
       artist,
       energy
FROM spotify
ORDER BY energy DESC
LIMIT 5;
```

3. List all tracks along with their views and likes where `official_video = TRUE`.
4. For each album, calculate the total views of all associated tracks.
```sql
SELECT album,
       SUM(views) AS total_views
FROM spotify
GROUP BY album
ORDER BY total_views DESC;
```

5. Retrieve the track names that have been streamed on Spotify more than YouTube.

### Advanced Level
1. Find the top 3 most-viewed tracks for each artist using window functions.
2. Write a query to find tracks where the liveness score is above the average.
3. **Use a `WITH` clause to calculate the difference between the highest and lowest energy values for tracks in each album.**
```sql
WITH cte
AS
(SELECT 
	album,
	MAX(energy) as highest_energy,
	MIN(energy) as lowest_energery
FROM spotify
GROUP BY 1
)
SELECT 
	album,
	highest_energy - lowest_energery as energy_diff
FROM cte
ORDER BY 2 DESC;
```
   
5. Find tracks where the energy-to-liveness ratio is greater than 1.2.
6. Calculate the cumulative sum of likes for tracks ordered by the number of views, using window functions.




---

## Query Optimization Technique 

To improve query performance, we carried out the following optimization process:

- **Initial Query Performance Analysis Using `EXPLAIN`**
    - We began by analyzing the performance of a query using the `EXPLAIN` function.
    - The query retrieved tracks based on the `artist` column, and the performance metrics were as follows:
        - Execution time (E.T.): **7 ms**
        - Planning time (P.T.): **0.17 ms**
    - Below is the **screenshot** of the `EXPLAIN` result before optimization:
      ![EXPLAIN Before Index](https://github.com/najirh/najirh-Spotify-Data-Analysis-using-SQL/blob/main/spotify_explain_before_index.png)

- **Index Creation on the `artist` Column**
    - To optimize the query performance, we created an index on the `artist` column. This ensures faster retrieval of rows where the artist is queried.
    - **SQL command** for creating the index:
      ```sql
      CREATE INDEX idx_artist ON spotify_tracks(artist);
      ```

- **Performance Analysis After Index Creation**
    - After creating the index, we ran the same query again and observed significant improvements in performance:
        - Execution time (E.T.): **0.153 ms**
        - Planning time (P.T.): **0.152 ms**
    - Below is the **screenshot** of the `EXPLAIN` result after index creation:
      ![EXPLAIN After Index](https://github.com/najirh/najirh-Spotify-Data-Analysis-using-SQL/blob/main/spotify_explain_after_index.png)

- **Graphical Performance Comparison**
    - A graph illustrating the comparison between the initial query execution time and the optimized query execution time after index creation.
    - **Graph view** shows the significant drop in both execution and planning times:
      ![Performance Graph](https://github.com/najirh/najirh-Spotify-Data-Analysis-using-SQL/blob/main/spotify_graphical%20view%203.png)
      ![Performance Graph](https://github.com/najirh/najirh-Spotify-Data-Analysis-using-SQL/blob/main/spotify_graphical%20view%202.png)
      ![Performance Graph](https://github.com/najirh/najirh-Spotify-Data-Analysis-using-SQL/blob/main/spotify_graphical%20view%201.png)

This optimization shows how indexing can drastically reduce query time, improving the overall performance of our database operations in the Spotify project.
---
# Skills Demonstrated

- SQL Fundamentals
- Database Design
- Data Filtering
- Aggregate Functions
- GROUP BY
- HAVING Clause
- Window Functions
- CTEs
- Ranking Functions
- Query Optimization
- Indexing
- Performance Analysis

---

# Project Structure


Spotify SQL Project
│
├── Dataset
│   └── spotify.csv
│
├── SQL Scripts
│   ├── Database Creation.sql
│   ├── Easy Queries.sql
│   ├── Medium Queries.sql
│   ├── Advanced Queries.sql
│   └── Query Optimization.sql
│
├── Screenshots
│
└── README.md


---

# How to Run the Project

1. Install PostgreSQL and pgAdmin (if not already installed).
2. Set up the database schema and tables using the provided normalization structure.
3. Insert the sample data into the respective tables.
4. Execute SQL queries to solve the listed problems.
5. Explore query optimization techniques for large datasets.

---


# Key Learning Outcomes

After completing this project, you will be able to:

- Create SQL databases and tables
- Import datasets into PostgreSQL
- Write SQL queries of different difficulty levels
- Analyze large datasets efficiently
- Use Window Functions for advanced analytics
- Improve SQL performance using indexes
- Apply SQL concepts to real-world datasets

---

# Future Improvements

Some additional enhancements that can be added to this project include:

- Interactive Power BI Dashboard
- Tableau Visualization
- Python Data Analysis
- Machine Learning for Music Prediction
- Spotify Recommendation Analysis

---

# Conclusion

This project provides practical experience in SQL using a real-world Spotify dataset. It covers everything from basic querying to advanced analytical techniques while also introducing database optimization strategies. It is an excellent project for improving SQL skills and showcasing database knowledge in a portfolio.


---

