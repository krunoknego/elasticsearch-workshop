# Exercise Block #5: Search Profiling & Pagination

## Exercise 1: Implement `search_after` for deep pagination.

First query to get the first page of results:
```json
GET /movies/_search
{
  "size": 2,
  "sort": [
    {
      "year": {
        "order": "desc"
      }
    }
  ]
}
```

Take the last sort value from the first page of results and use it in the next query:

⚠️ Use the same sort order as the first query to ensure consistent pagination.
⚠️ The `search_after` parameter should be an array containing the last sort value from the previous page (e.g., the last year value).


```json
GET /movies/_search
{
  "size": 2,
  "sort": [
    {
      "year": {
        "order": "desc"
      }
    }
  ],
  "search_after": [<last_sort_value>] // replace this
}
```

What is the purpose of using `search_after` in this context? How does it differ from using `from` and `size` for pagination?

## Exercise 2:Profile a query. Identify slow parts of the query.

```json
GET /movies/_search
{
  "profile": true,
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "title": "Inception"
          }
        }
      ]
    }
  }
}
```

Check theresponse for the `profile` section. It will show you the time taken for each phase of the query execution.

The `breakdown` section will provide detailed information about the time spent in different parts of the query execution process.

## Exercise 3:Implement Scroll API to fetch all documents in the movies index.

Create the scroll context:
```json
POST /movies/_search?scroll=10m
{
  "size": 2,
  "query": {
    "match_all": {}
  },
  "sort": ["_doc"]
}
```

The response will include a `scroll_id` and the first batch of results. 

⚠️ Remember to use the `scroll_id` in subsequent requests to fetch the next batch of results.

```json
GET /_search/scroll
{
    "scroll": "10m",
    "scroll_id": "<scroll_id>" // replace this with the actual scroll_id
}
```

What is the purpose of using the Scroll API? How does it differ from using a regular search query with pagination?

⚠️ It's important to note that you need to manage the scroll context and clear it after use to avoid resource leaks.

```json
DELETE /_search/scroll
{
  "scroll_id": "<scroll_id>"
}
```

