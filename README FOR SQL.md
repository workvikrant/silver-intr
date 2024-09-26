
# Silver space internship

Solving the questions using SQL 


## SQL Query

Q1. How many tweets were posted containing the term on each day?


```bash
SELECT DATE(created_at) AS tweet_date,
    COUNT(*) AS tweet_count
FROM 
    tweets
WHERE 
    text LIKE '%music%'
GROUP BY 
    DATE(created_at)
ORDER BY 
    tweet_count;

```

Q2. How many unique users posted a tweet containing the term?

```bash
SELECT 
    COUNT(DISTINCT user_id) AS unique_users
FROM 
    tweets
WHERE 
    text LIKE '%music%';

```
Q3. How many likes did tweets containing the term get, on average?

```bash
SELECT 
    AVG(likes) AS average_likes
FROM 
    tweets
WHERE 
    text LIKE '%music%';

```
Q4. Where (in terms of place IDs) did the tweets come from?

```bash
SELECT 
    place_id,
    COUNT(*) AS tweet_count
FROM 
    tweets
WHERE 
    text LIKE '%music%'
GROUP BY 
    place_id
ORDER BY 
    tweet_count DESC;

```
Q5. What times of day were the tweets posted at?

```bash
SELECT 
    EXTRACT(HOUR FROM created_at) AS tweet_hour,
    COUNT(*) AS tweet_count
FROM 
    tweets
WHERE 
    text LIKE '%music%'
GROUP BY 
    tweet_hour
ORDER BY 
    tweet_count DESC;


```
Q6. Which user posted the most tweets containing the term?


```bash
SELECT 
    user_id,
    COUNT(*) AS tweet_count
FROM 
    tweets
WHERE 
    text LIKE '%music%'
GROUP BY 
    user_id
ORDER BY 
    tweet_count DESC
LIMIT 1;
```