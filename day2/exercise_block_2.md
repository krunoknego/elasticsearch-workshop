# Exercise Block #2: Search Basics

## Exercise 1:Perform a term query to find movies directed by "Christopher Nolan".

```json
GET /movies/_search
{
  "query": {
    "term": {
      "director": "Christopher Nolan"
    }
  }
}
```

What is the result of this query? How many movies were found?

How could you modify the query to make it work?

## Exercise 2:Perform a range query to find movies released between 2010 and 2020.

```json
GET /movies/_search
{
  "query": {
    "range": {
      "year": {
        "gte": 2010,
        "lte": 2020
      }
    }
  }
}
```

## Exercise 3:Use a match query to search for movies with "ACTION" in their genre.
  
  ```json
  GET /movies/_search
  {
    "query": {
      "match": {
        "genre": "ACTION"
      }
    }
  }
  ```
  What is the result of this query? Can you explain why it returned those results?

## Exercise 4:Write a bool query to:
✅ Match genre containing "Sci-Fi" and "Action"
✅ Filter for year 2010

⚠️ You have to use the `bool` query to combine the two conditions.
