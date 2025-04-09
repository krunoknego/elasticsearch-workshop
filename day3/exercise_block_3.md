# Exercise Block #5: N-Grams

# Exercise 1: Create an analyzer using ngram.

```json
PUT /autocomplete
{
  "settings": {
    "index": {
      "max_ngram_diff": 8
    },
    "analysis": {
      "filter": {
        "autocomplete_filter": {
          "type": "ngram",
          "min_gram": 3,
          "max_gram": 10
        }
      },
      "analyzer": {
        "autocomplete_analyzer": {
          "type": "custom",
          "tokenizer": "standard",
          "filter": [
            "lowercase",
            "autocomplete_filter"
          ]
        }
      }
    }
  },
  "mappings": {
    "properties": {
      "title": {
        "type": "text",
        "analyzer": "autocomplete_analyzer"
      }
    }
  }
}
```

Test it with the text "The quick brown fox jumps over the lazy dog".

```json
POST /autocomplete/_analyze
{
  "analyzer": "autocomplete_analyzer",
  "text": "The quick brown fox jumps over the lazy dog"
}
```

Which tokens were generated?

# Exercise 2:Create an analyzer using edge_ngram

```json
PUT /autocomplete_edge
{
  "settings": {
    "analysis": {
      "filter": {
        "edge_ngram_filter": {
          "type": "edge_ngram",
          "min_gram": 2,
          "max_gram": 20
        }
      },
      "analyzer": {
        "autocomplete_edge_analyzer": {
          "tokenizer": "standard",
          "filter": ["lowercase", "edge_ngram_filter"]
        }
      }
    }
  },
  "mappings": {
    "properties": {
      "title": {
        "type": "text",
        "analyzer": "autocomplete_edge_analyzer"
      }
    }
  }
}
```

Test it with the text "The quick brown fox jumps over the lazy dog".

```json
POST /autocomplete_edge/_analyze
{
  "analyzer": "autocomplete_edge_analyzer",
  "text": "The quick brown fox jumps over the lazy dog"
}
```
