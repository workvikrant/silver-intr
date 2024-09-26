# Silver Space Internship

In this project we are going to use MongoDB and docker to create a database and run querries.



# Part 1
The database will be hosted on a cloud platform known as codespace which can be accessed from anywhere.

To install the container we have to run the following commands


### Deployment

To deploy this project run

```bash
  docker run -d --name mongo-intr \
  > -e MONGO_INITDB_ROOT_USERNAME=mongoadmin \
  > -e MONGO_INITDB_ROOT_PASSWORD=admin \
  > -p27017:27017 -v mongointr:/data/twitter \
  > mongo:latest
```

This will install latest version of MongoDB with a volume name mongointr 

### Connect to MongoDB

Connect your docker image to MongoDB in codespace using extension.

```bash
  mongodb://<ip of codespace>:27017/
```
Change <ip of codespace> to your ip


### OR

Created a new server using MongoDB Atlas for free and imported the data using shell or Compass


## Part 2
Executing the queries

Q1.How many tweets were posted containing the term on each day


### Screenshots

![Query with result Screenshot](https://github.com/workvikrant/silver-intr/blob/main/Screenshot%20(1930).png)

Q2. How many unique users posted a tweet containing the term?

### Screenshots

![Query with result Screenshot](https://github.com/workvikrant/silver-intr/blob/main/Screenshot%20(1925).png)

Q3. How many likes did tweets containing the term get, on average?

### Screenshots

![Query with result Screenshot](https://github.com/workvikrant/silver-intr/blob/main/Screenshot%20(1926).png)

Q4. Where (in terms of place IDs) did the tweets come from?

### Screenshots

![Query with result Screenshot](https://github.com/workvikrant/silver-intr/blob/main/Screenshot%20(1927).png)

Q5. What times of day were the tweets posted at? 

### Screenshots

![Query with result Screenshot](https://github.com/workvikrant/silver-intr/blob/main/Screenshot%20(1928).png)

Q6. Which user posted the most tweets containing the term?

### Screenshots

![Query with result Screenshot](https://github.com/workvikrant/silver-intr/blob/main/Screenshot%20(1929).png)

# Part 2 ( Using SQL )


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
    id AS user_id,
    COUNT(DISTINCT id) AS unique_users
FROM 
    tweets
WHERE 
    text LIKE '%music%'
GROUP BY
    user_id;

```
Q3. How many likes did tweets containing the term get, on average?

```bash
SELECT 
    AVG(like_count) AS average_likes
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
    id AS user_id,
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

# Part 3
 -- Question:  
 
 Explain to me how I can use your system. I should be able to run this system and query it on my own computer using your instructions. Please explain and justify any important design choices you make.

 -- Answer:

1. To use the same system as I have, you can simply just create a codespace on the main branch, install 'docker' extension and 'MongoDB for VS code' extension.
2. Open the terminal and run the above command given in part 1.
3. Create a connection string and using that connection string connect to MongoDB
4. Import the data and run the queries using playground

OR 

1. Open MongoDB Atlas
2. Connect to the server using the connection string shown at the time of creation of the server (Remember the password)
3. Run the queries using MongoDB Compass
4. Create a view for further reference


* The design which I have choose for this project is creating a codespace on main branch of GitHub project or using MongoDB server, So 
  that I do not have to install any of the application/software/dependencies on my personal computer, things can be shared easily and 
  multiple people can collaborate at once.




#### I could have shared the server details with you but I have forgot the password shown at the time of creation :(

 
# Changes made:

Converted the .tsv file to .json file Using the following Python code

```bash
import csv
import json

def tsv_to_json(tsv_file, json_file):
    with open(tsv_file, 'r') as f:
        reader = csv.DictReader(f, delimiter='\t')
        data = list(reader)

    with open(json_file, 'w') as f:
        json.dump(data, f, indent=4)

if __name__ == '__main__':
    tsv_file = 'correct_twitter_201904.tsv'  
    json_file = 'output_twitter.json' 
    tsv_to_json(tsv_file, json_file)
```
