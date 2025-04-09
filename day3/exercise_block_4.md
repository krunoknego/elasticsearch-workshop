# Exercise Block #7: dis_max and Boosting Queries

## Exercise 1: Use a `dis_max` query to search across title and description. Adjust the tie_breaker parameter and observe how it affects the scoring.

Create the dismovies index

```json
PUT /dismovies
{
  "mappings": {
    "properties": {
      "title": {
        "type": "text"
      },
      "description": {
        "type": "text"
      },
      "genre": {
        "type": "text",
        "fields": {
          "keyword": {
            "type": "keyword"
          }
        }
      }
    }
  }
}
```

Index sample documents using bulk API

```json
POST /dismovies/_bulk
{ "index": {} }
{ "title": "The Mystery of the Blue Train", "description": "A thrilling mystery novel", "genre": "mystery" }
{ "index": {} }
{ "title": "Romantic Nights", "description": "A romantic drama", "genre": "romance" }
{ "index": {} }
{ "title": "Comedy Central", "description": "A hilarious comedy show", "genre": "comedy" }
{ "index": {} }
{ "title": "The Great Adventure", "description": "An action-packed adventure", "genre": "action" }
{ "index": {} }
{ "title": "Mystery in the Woods", "description": "A suspenseful mystery", "genre": "mystery" }
{ "index": {} }
{ "title": "Romantic Getaway", "description": "A romantic comedy", "genre": "romance" }
{ "index": {} }
{ "title": "Comedy Nights", "description": "A fun comedy show", "genre": "comedy" }
{ "index": {} }
{ "title": "The Adventure Continues", "description": "An exciting sequel", "genre": "action" }
{ "index": {} }
{ "title": "Mystery of the Lost Treasure", "description": "A thrilling treasure hunt", "genre": "mystery" }
{ "index": {} }
{ "title": "Romantic Escapade", "description": "A romantic adventure", "genre": "romance" }
{ "index": {} }
{ "title": "Comedy Extravaganza", "description": "A comedy festival", "genre": "romance comedy" }
```


```json
GET /dismovies/_search
{
  "query": {
    "dis_max": {
      "queries": [
        { "match": { "title": "mystery" } },
        { "match": { "description": "mystery" } }
      ],
      "tie_breaker": 0.2
    }
  }
}
```

Try adjusting the `tie_breaker` parameter. What happens when you set it to 0.0? What about 1.0?
Look at the score of the documents returned.

Try adding `explain: true` to the search request to see how the score is calculated.

## Exercise 2: Create a boosting query to prioritize romantic films while lowering the score for those tagged with comedy.

```json
GET /dismovies/_search
{
  "query": {
    "boosting": {
      "positive": { "match": { "genre": "romance" } },
      "negative": { "match": { "genre": "comedy" } },
      "negative_boost": 0.3
    }
  }
}
```

Try adjusting the `negative_boost` parameter. What happens when you set it to 0.0? What about 1.0?

## Exercise 3: Count how many movies are in each genre.

```json
GET /dismovies/_search
{
  "size": 0,
  "aggs": {
    "genre_count": {
      "terms": {
        "field": "genre.keyword"
      }
    }
  }
}
```

Aggregations work only on keyword fields. If you want to use aggregations on text fields, you need to create a sub-field of type keyword.
