
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

Created a new server on MongoDB compass and imported the data using shell or Atlas


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

# Part 3
 -- Question:  
 
 Explain to me how I can use your system. I should be able to run this system and query it on my own computer using your instructions. Please explain and justify any important design choices you make.

 -- Answer:

 
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
