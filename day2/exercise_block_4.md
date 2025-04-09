# Exercise Block #4: Multifield & Relevance

## Exercise 1:Create a multi_match query searching across title and description fields.Boost the title field.

```json
GET /movies/_search
{
  "query": {
    "multi_match": {
      "query": "Inception",
      "fields": [
        "title^2",
        "description"
      ]
    }
  }
}
```

What is the result of this query?
How does boosting the title field affect the search results?
How would you modify the query to boost the description field instead?

## Exercise 2:Use a bool query to:
✅ Match description containing "thriller"
✅ Filter for movies released after 2015

```json
GET /movies/_search
{
  "query": {
    "bool": {
      "must": {
        "match": {
          "description": "thriller"
        }
      },
      "filter": {
        "range": {
          "year": {
            "gt": 2015
          }
        }
      }
    }
  }
}
```

## Exercise 3: Search for all movies released after 2000. Implement field collapsing by director

```json
GET /movies/_search
{
  "query": {
    "range": {
      "year": {
        "gt": 2000
      }
    }
  },
  "collapse": {
    "field": "director.keyword"
  }
}
```

How does field collapsing work in this context?
How would you modify the query to collapse by genre instead?
