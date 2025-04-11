# Exercise Block #1: Administration & Maintenance


## Exercise 1: Force merge an index

First add a few documents to the **products_force_merge** index:

```json
POST /products_force_merge/_bulk
{"index": {"_id": "1"}}
{"name": "Wireless Headphones", "description": "Over-ear Bluetooth headphones with noise canceling.", "category": "electronics", "price": 99.99}
{"index": {"_id": "2"}}
{"name": "Wireless Mouse", "description": "Ergonomic wireless mouse with customizable buttons.", "category": "electronics", "price": 49.99}
{"index": {"_id": "3"}}
{"name": "Running Shoes", "description": "Lightweight running shoes for all terrains.", "category": "footwear", "price": 79.99}
```

Check the number of segments in the index:

```json
GET /products_force_merge/_segments
```

If the number of segments is 1, add more documents to increase the number of segments:

```json
POST /products_force_merge/_bulk
{"index": {"_id": "4"}}
{"name": "Smartphone", "description": "Latest model with high-resolution camera.", "category": "electronics", "price": 699.99}
{"index": {"_id": "5"}}
{"name": "Yoga Mat", "description": "Eco-friendly yoga mat with non-slip surface.", "category": "fitness", "price": 29.99}
```

Then force merge the index to reduce the number of segments:

```json
POST /products_force_merge/_forcemerge?max_num_segments=1
```

Check the number of segments again:

```json
GET /products_force_merge/_segments
```


## Exercise 2:Simulate a rolling restart of a 3-node cluster.

Stop the shard allocation:

```json
PUT /_cluster/settings
{
  "persistent": {
    "cluster.routing.allocation.enable": "none"
  }
}
```

Stop the node 

`docker compose stop es01`

After doing some fictive updates on the node you can start it again:

`docker compose start es01`

Then start the shard allocation:

```json
PUT /_cluster/settings
{
  "persistent": {
    "cluster.routing.allocation.enable": null
  }
}
```
