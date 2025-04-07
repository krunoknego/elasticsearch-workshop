# Exercise Block #5: Custom Routing

## Exercise 1:Index 2 documents into the products index using a custom routing key.

```json
POST /products/_doc?routing=custom_key
{
  "name": "Product 2",
  "category": "Category B",
  "price": 29.99
}
```

```json

POST /products/_doc?routing=custom_key
{
  "name": "Product 3",
  "category": "Category A",
  "price": 39.99
}
```

## Exercise 2: Index 1 document into products index without using a custom routing key.

```json
POST /products/_doc
{
  "name": "Product 4",
  "category": "Category C",
  "price": 49.99
}
```

## Exercise 3:Retrieve the documents using the custom routing key.

```json
GET /products/_search?routing=custom_key
{
  "query": {
    "match_all": {}
  }
}
```

How many documents are returned?


## Exercise 4: Check which shard the documents are stored in.
  
```json
GET /products/_search?routing=custom_key
{
  "profile": true,
  "_source": false,
  "query": {
    "match_all": {}
  }
}
```

The response will include shard information in the `shards` field.

It should look something like this:

```json
  "profile": {
    "shards": [
      {
        "id": "[cBUcWWujQJmgUgxyka2pdQ][products][1]",
        "node_id": "cBUcWWujQJmgUgxyka2pdQ",
        "shard_id": 1,
        "index": "products",
        "cluster": "(local)",
        "searches": [
```
The`shard_id` indicates which shard the document is stored in. The `index` field shows the index name, and the `node_id` indicates which node the shard is on.
