# Exercise Block #6: Search Template

## Exercise 1:Create a search template to search for movies by title.

```json
POST /_scripts/movie_search_template
{
  "script": {
    "lang": "mustache",
    "source": {
      "query": {
        "match": {
          "title": "{{title}}"
        }
      }
    }
  }
}
```

## Exercise 2:Execute the template with parameterized input.

```json
POST /_search/template
{
  "id": "movie_search_template",
  "params": {
    "title": "Inception"
  }
}
```
