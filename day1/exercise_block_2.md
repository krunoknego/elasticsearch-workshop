# Exercise Block #2: Cluster Configuration & Metadata

## Exercise 1:Inspect your cluster configuration using:

- Check the cluster settings, execute the following query:
  ```json
  GET /_cluster/settings
  ```
  
  Changes like disabling shard allocation (e.g., cluster.routing.allocation.enable: none) would show up here.
  
- Check the index settings, execute the following query:
  ```json
  GET /_cat/indices?v
  ```
  
  This shows each index’s health, number of primary & replica shards, and storage size.
  Look for movies index and verify it's using 3 primaries and 1 replica.
  
- Check the index settings, execute the following query:
  ```json
  GET /movies/_settings
  ```
  
  Confirm with how many primary shards and replicas the movie index was created.
  
## Exercise 2:Retrieve and review cluster state metadata:

- Check the cluster state, execute the following query:
  ```json
  GET /_cluster/state
  ```
  
  What you’ll see: This is a very large JSON object. Key parts to explore:
  - "cluster_name" → name of the cluster, the same name is defined in `.env`, this is important when dealing with multiple clusters
  - "nodes" → lists all nodes in the cluster, check their roles

## Exercise 3:Add a new node to your cluster and observe:

- Add a new node to your cluster by modifying the Docker Compose file.
  ```yaml
  es04:
    image: docker.elastic.co/elasticsearch/elasticsearch:${STACK_VERSION}
    volumes:
      - esdata04:/usr/share/elasticsearch/data
      - ./elasticsearch.yml:/usr/share/elasticsearch/config/elasticsearch.yml
      - ./my_backups:/usr/share/elasticsearch/my_backups
    environment:
      - node.name=es04
      - cluster.name=${CLUSTER_NAME}
      - cluster.initial_master_nodes=es01,es02,es03
      - discovery.seed_hosts=es01,es02,es03
      - ELASTIC_PASSWORD=${ELASTIC_PASSWORD}
      - bootstrap.memory_lock=true
      - xpack.security.enabled=false
      - xpack.license.self_generated.type=${LICENSE}
      - xpack.ml.use_auto_machine_memory_percent=true
    mem_limit: ${MEM_LIMIT}
    ulimits:
      memlock:
        soft: -1
        hard: -1
    healthcheck:
      test:
        [
          "CMD-SHELL",
          "curl -s http://localhost:9200 | grep -q 'You Know, for Search'",
        ]
      interval: 10s
      timeout: 10s
      retries: 120
  ```
  
- Start your newly added node `docker compose up -d es04`. Wait for the node to start, it could take a minute
  
- Execute
  ```json
  GET /_cat/nodes?v
  ```
  
  You should see now 4 nodes, including es04

- Execute
  ```json
  GET _cat/shards/movies
  ```
  Some shards might be on es04
  
- Execute
  ```json
  GET /_cluster/health
  ```
  Cluster health should remain green or briefly yellow during shard relocation.
  
- Master will stay the same unless it fails. You can check it with:
  ```json
  GET /_cat/master?v
  ```
  
