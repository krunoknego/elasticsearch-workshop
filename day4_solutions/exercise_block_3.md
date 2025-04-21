# Exercise Block #3: Product Catalog Autocomplete

Context:

Now you want to implement autocomplete for product search and improve search quality with phrase and exact matching.

## Exercise 1: Define Autocomplete Mapping

Define a **products_autocomplete** index with fields:
- name (text + keyword with tokenizer for autocomplete)

- description (text)

- category (keyword)

- price (float)

```json
PUT /products_autocomplete
{
  "mappings": {
    "properties": {
      "name": {
        "type": "text",
        "fields": {
          "keyword": {
            "type": "keyword"
          },
          "autocomplete": {
            "type": "text",
            "analyzer": "autocomplete_analyzer"
          }
        }
      },
      "description": {
        "type": "text"
      },
      "category": {
        "type": "keyword"
      },
      "price": {
        "type": "float"
      }
    }
  },
  "settings": {
    "analysis": {
      "filter": {
        "autocomplete_filter": {
          "type": "edge_ngram",
          "min_gram": 1,
          "max_gram": 20 
        }
      },
      "analyzer": {
        "autocomplete_analyzer": {
          "tokenizer": "standard",
          "filter": [
            "lowercase",
            "autocomplete_filter"
          ]
        }
      }
    }
  }
}
```

## Exercise 2: Reindex the Data from products to products_autocomplete

Reindex the data from the **products** index to the **products_autocomplete** index.

```json
POST /_reindex
{
  "source": {
    "index": "products"
  },
  "dest": {
    "index": "products_autocomplete"
  }
}
```

## Exercise 3: Autocomplete Search

Write a query to find products that match the term "wire" in the `name` field. 

```json
GET /products_autocomplete/_search
{
  "query": {
    "match": {
      "name.autocomplete": {
        "query": "wire",
      }
    }
  }
}
```

## Exercise 4: Find Products in Electronics Category and Filter Them by Price 

Write a query to find products in the "electronics" category with a price less than 50. Sort the results by price in ascending order.

```json
GET /products_autocomplete/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "category": "electronics"
          }
        },
        {
          "range": {
            "price": {
              "lt": 50
            }
          }
        }
      ]
    }
  },
  "sort": [
    {
      "price": {
        "order": "asc"
      }
    }
  ]
}
```
