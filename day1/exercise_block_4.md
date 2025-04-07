# Exercise Block #4: Index & Shard Management

## Exercise 1:Create an index named products with:

5 primary shards

1 replica per shard

define explicit mappings for the following fields:

name → text

category → keyword

price → float

```json
PUT /products
{
  "settings": {
    "number_of_shards": 5,
    "number_of_replicas": 1
  },
  "mappings": {
    "properties": {
      "name": {
        "type": "text"
      },
      "category": {
        "type": "keyword"
      },
      "price": {
        "type": "float"
      }
    }
  }
}
```

Add one product to the products index (that follows the schema):
```json
POST /products/_doc
{
  "name": "Product 1",
  "category": "Category A",
  "price": 19.99
}
```

## Exercise 2: Check the mapping of the products index.
```json
GET /products/_mapping
```

## Exercise 3: Index 1 document into the products index, that doesn't follow the schema.
```json
POST /products/_doc
{
  "name": "Product 5",
  "category": "Category D",
  "hello": "world"
}
```

## Exercise 4: Check the mapping of the products index.
```json
GET /products/_mapping
```

## Exercise 5: Check how the primary shards are allocated.
```json
GET /_cat/shards/products?v
```

