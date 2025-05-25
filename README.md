# Spotify_Data_Analysis_using_SQL

**Database:** Spotify_db

**SQL Queries:** DDL, DML, Aggregations, Joins, Subqueries, Window Functions

**Tool using:** pgAdmin 4

![Spotify](https://github.com/Issita/Spotify_Data_Analysis_using_SQL/blob/main/spotify.png)

## Overview

In this project, I work with a Spotify dataset that includes various track, album, and artist attributes. The process involves converting a denormalized dataset into a normalized structure, writing SQL queries of increasing complexity (from basic to advanced), and optimizing query performance. The key aims are to enhance my SQL expertise and uncover valuable trends in the dataset.


## Data Exploration

Before diving into SQL, it’s important to understand the dataset thoroughly. The dataset contains attributes such as:

- **Artist:** The performer of the track.
- **Track:** The name of the song.
- **Album:** The album to which the track belongs.
- **Album_type:** The type of album (e.g., single or album).
- Various metrics such as **danceability, energy, loudness, tempo,** and more.

## Queries
**1. Retrieve the names of all tracks that have more than 1 billion streams.**
```sql
SELECT * FROM spotify
WHERE Stream > 1000000000;
```
**2. List all albums along with their respective artists.**
```sql
SELECT 
DISTINCT artist, album
FROM spotify
ORDER BY 1;
```
**3. Get the total number of comments for tracks where licensed = TRUE**
```sql
SELECT SUM(comments) AS Total_Comments
FROM spotify
WHERE licensed = 'TRUE';
```
**4. Find all tracks that belong to the album type single.**
```sql
SELECT track FROM spotify
WHERE Album_type = 'single';
```
**5. Count the total number of tracks by each artist.**

```sql
select artist, count(track) as number_of_track
from spotify
group by artist;
```

**6. Calculate the average danceability of tracks in each album.**
```sql
select
album,
avg(danceability) as avg_danceability
from spotify
group by album
order by avg(danceability) desc;
```

**7. Find the top 5 tracks with the highest energy values.**
```sql
select 
track,
max(energy) as desc_energy
from spotify
group by track
order by max(energy)
limit 5;
```

**8. List all tracks along with their views and likes where official_video = TRUE.**
```sql
select 
track,
sum(views) as total_view,
sum(likes) as total_likes
from spotify
where official_video = 'TRUE'
group by track
order by sum(views) desc;
```

**9. For each album, calculate the total views of all associated tracks.**
```sql
select 
album,
track,
sum(views) as total_views
from spotify
group by album,track
order by sum(views) desc;

```

**10. Retrieve the track names that have been streamed on Spotify more than YouTube.**
```sql
select * from 
(
select 
track,
-- most_playedon,
coalesce(sum(case when most_playedon = 'Youtube' then stream end),0) as streamed_on_youtube,
coalesce(sum(case when most_playedon = 'Spotify' then stream end),0) as streamed_on_spotify
from spotify
group by track
) as t1
where streamed_on_spotify > streamed_on_youtube
	  and
	  streamed_on_youtube<> 0; 

```


```sql

```
