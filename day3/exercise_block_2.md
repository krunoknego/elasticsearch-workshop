# Exercise Block #2: Advanced Language & Result Tuning

## Exercise 1: Create a flat object index that causes cross-matching

```json
PUT /movies_not_nested
{
  "mappings": {
    "properties": {
      "title": { "type": "text" },
      "actors": {
        "properties": {
          "name": { "type": "text" },
          "role": { "type": "text" }
        }
      }
    }
  }
}
```

Index flat actor documents:

```json
POST /movies_not_nested/_doc
{
  "title": "Fake Match Movie",
  "actors": [
    {
      "name": "Leonardo DiCaprio",
      "role": "Joker"
    },
    {
      "name": "Heath Ledger",
      "role": "Cobb"
    }
  ]
}
```

Search for an actor with the name "Leonardo" and role "Cobb":

```json
GET /movies_not_nested/_search
{
  "query": {
    "bool": {
      "must": [
        { "match": { "actors.name": "Leonardo DiCaprio" } },
        { "match": { "actors.role": "Cobb" } }
      ]
    }
  }
}
```

What happens? Why does it return a match?


## Exercise 2: Create a proper index with nested actors

```json
PUT /movies_nested
{
  "mappings": {
    "properties": {
      "title": { "type": "text" },
      "actors": {
        "type": "nested",
        "properties": {
          "name": { "type": "text" },
          "role": { "type": "text" }
        }
      }
    }
  }
}
```

## Exercise 3:Index sample movie document with nested actors.
```json
POST /movies_nested/_doc
{
  "title": "Real Match Movie",
  "actors": [
    {
      "name": "Leonardo DiCaprio",
      "role": "Cobb"
    },
    {
      "name": "Heath Ledger",
      "role": "Joker"
    }
  ]
}
```

## Exercise 4: Use a nested query to avoid cross-matching

```json
GET /movies_nested/_search
{
  "query": {
    "nested": {
      "path": "actors",
      "query": {
        "bool": {
          "must": [
            { "match": { "actors.name": "Leonardo DiCaprio" } },
            { "match": { "actors.role": "Cobb" } }
          ]
        }
      }
    }
  }
}
```

What could happen if you used a normal query instead of a nested query?
