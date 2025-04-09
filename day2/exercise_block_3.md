# Exercise Block #3: Advanced Search

## Exercise Block #1: Using bulk API add more movies to the index

```json
POST /movies/_bulk
{ "index": {} }
{ "title": "Blade Runner", "director": "Ridley Scott", "year": 1982, "genre": ["Sci-Fi", "Drama"] }
{ "index": {} }
{ "title": "The Fifth Element", "director": "Luc Besson", "year": 1997, "genre": ["Sci-Fi", "Action"] }
{ "index": {} }
{ "title": "Eternal Sunshine of the Spotless Mind", "director": "Michel Gondry", "year": 2004, "genre": ["Sci-Fi", "Romance"] }
{ "index": {} }
{ "title": "The Prestige", "director": "Christopher Nolan", "year": 2006, "genre": ["Drama", "Mystery"] }
```

## Exercise 2:Use `match_phrase` query to find movies with the exact phrase "sunshine of the spotless".
```json
GET /movies/_search
{
  "query": {
    "match_phrase": {
      "title": "sunshine of the spotless"
    }
  }
}
```

What would happen if you used a term query instead of a `match_phrase` query? Why would you use `match_phrase` instead of term?

```json
GET /movies/_search
{
  "query": {
    "term": {
      "title": "sunshine of the spotless"
    }
  }
}
```

How would you modify the term query to make it work?


## Exercise 3:Perform a fuzzy search on movie titles to match misspelled terms.

```json
GET /movies/_search
{
  "query": {
    "fuzzy": {
      "title": {
        "value": "Inception",
        "fuzziness": "AUTO"
      }
    }
  }
}
```

What is the result of this query? Can you explain why it returned those results? What is the purpose of using `fuzziness` in this context?

## Exercise 4:Sort search results by year in descending order.

```json
GET /movies/_search
{
  "sort": [
    {
      "year": {
        "order": "desc"
      }
    }
  ]
}

```

## Exercise 5:Implement pagination using from and size.

```json
GET /movies/_search
{
  "from": 0,
  "size": 3
}
```
