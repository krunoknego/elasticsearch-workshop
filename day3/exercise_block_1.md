# Exercise Block #1: Language Processing

## Exercise 1:Analyze the text "The quick brown fox jumps over the lazy dog" using the standard analyzer.

```json
POST /_analyze
{
  "analyzer": "standard",
  "text": "The quick brown fox jumps over the lazy dog"
}
```

How many tokens were generated? 

## Exercise 2:Create a custom analyzer with:
✅ Whitespace tokenizer
✅ Lowercase filter
✅ English stopword filter

```json
PUT /custom_english
{
  "settings": {
    "analysis": {
      "analyzer": {
        "my_custom_english": {
          "type": "custom",
          "tokenizer": "whitespace",
          "filter": ["lowercase", "stop"]
        }
      }
    }
  }
}
```

Test it with the text "The quick brown fox jumps over the lazy dog".

```json
POST /custom_english/_analyze
{
  "analyzer": "my_custom_english",
  "text": "The quick brown fox jumps over the lazy dog"
}
```

Look at the output. How many tokens were generated? Which ones were removed?


## Exercise 3:Implement a synonym filter for the words: "movie, film".

- Create index with synonym filter

```json
PUT /movies_synonym
{
  "settings": {
    "analysis": {
      "filter": {
        "synonym_filter": {
          "type": "synonym",
          "synonyms": ["movie, film"]
        }
      },
      "analyzer": {
        "movie_synonym_analyzer": {
          "tokenizer": "standard",
          "filter": ["lowercase", "synonym_filter"]
        }
      }
    }
  },
  "mappings": {
    "properties": {
      "title": {
        "type": "text",
        "analyzer": "movie_synonym_analyzer"
      }
    }
  }
}
```

You can test the synonym filter with the text "film".

```json
POST /movies_synonym/_analyze
{
  "analyzer": "movie_synonym_analyzer",
  "text": "film"
}
```

What tokens were generated? Did the synonym filter work as expected?

