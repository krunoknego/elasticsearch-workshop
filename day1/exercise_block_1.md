# Exercise Block #1: Cluster & Index Basics

## Exercise 1:
Spin up a 3-node Elasticsearch cluster using the provided Docker Compose file.

- Execute `make start`
- Login to kibana http://localhost:5601 (u: elastic, p: helloworld)
- Open the menu on the left
- Navigate to Management –> Dev Tools
- Execute the following query
  ``` json
  GET _cat/nodes
  ```
- How many nodes are in the cluster? Which node is the master?


## Exercise 2:
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
- How many shards in total are created for the movies index?
  ```json
  GET /_cat/shards/movies?v
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
- Get the document by ID, execute the following query:
  ```json
  GET /movies/_doc/1
  ```
- Check the index mapping, execute the following query:
  ```json
  GET /movies/_mapping
  ```

## Exercise 3:
Check the cluster health and explain the current status.

- Execute the following query:
  ```json
  GET /_cluster/health
  ```
- Check the cluster health status
- Check the number of active shards 
- Disable the shard allocation
  ```json
  PUT _cluster/settings
  {
    "persistent": {
      "cluster.routing.allocation.enable": "none"
    }
  }
  ```
- Intentionally stop a node and observe how cluster health changes.
  `docker compose stop es02`
- Check the cluster health status again. In what state is it now? What does it mean?
- Enable the shard allocation
  ```json
  PUT _cluster/settings
  {
    "persistent": {
      "cluster.routing.allocation.enable": "all"
    }
  }
  ```
- Start the node again
  `docker compose start es02`
- Check the cluster health status again. You have to wait a bit before it is up and running
