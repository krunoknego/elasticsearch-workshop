# Exercise Block #1: Cluster Setup

## Exercise 1:Set up a 3-node Elasticsearch cluster using Docker Compose.

- Execute `make start` to start the cluster.

## Exercise 2: Open Kibana

- Open your web browser and navigate to `http://localhost:5601` to access Kibana. (u: elastic, p: helloworld)


## Exercise 3:Verify cluster health and node information:

```json
GET /_cluster/health
```

```json
GET /_cat/nodes?v
```

## Exercise 4: Create an index for movies andadd sample data

- Execute the following query and create an index named movies with the following settings/mappings:
  ``` json
  PUT /movies
  {
    "settings": {
      "number_of_shards": 3,
      "number_of_replicas": 1
    }
  }
  ```
- Add movies to the index, execute
  ``` json
  POST /movies/_doc/1
  {
    "title": "Inception",
    "director": "Christopher Nolan",
    "year": 2010,
    "genre": ["Action", "Sci-Fi"]
  }
  ```
  
  ``` json
  POST /movies/_doc/2
  {
    "title": "The Matrix",
    "director": "Lana Wachowski, Lilly Wachowski",
    "year": 1999,
    "genre": ["Action", "Sci-Fi"]
  }
  ```
  
  ``` json
  POST /movies/_doc/3
  {
    "title": "Interstellar",
    "director": "Christopher Nolan",
    "year": 2014,
    "genre": ["Adventure", "Drama", "Sci-Fi"]
  }
  ```
