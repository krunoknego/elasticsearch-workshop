# Exercise Block #4: Blog Post and Comments

Context:

You are building a blog platform where users can create posts and leave comments. You need to setup an index for blog posts.
Each blog post can have multiple comments.

## Exercise 1: Define Index Mapping

Define a **blog** index with fields:

- title (text + keyword)
- content (text)
- author (keyword)
- tags (keyword)
- comments (nested object with fields: user (keyword), comment (text), date (date))

```json
PUT /blog
{
  "mappings": {
    "properties": {
      "title": {
        "type": "text",
        "fields": {
          "keyword": {
            "type": "keyword"
          }
        }
      },
      "content": {
        "type": "text"
      },
      "author": {
        "type": "keyword"
      },
      "tags": {
        "type": "keyword"
      },
      "comments": {
        "type": "nested",
        "properties": {
          "user": {
            "type": "keyword"
          },
          "comment": {
            "type": "text"
          },
          "date": {
            "type": "date"
          }
        }
      }
    }
  }
}
```

## Exercise 2: Index Sample Data

```json
POST /blog/_doc
{
  "title": "Understanding Elasticsearch",
  "content": "Elasticsearch is a distributed, RESTful search and analytics engine capable of solving a growing number of use cases.",
  "author": "John Doe",
  "tags": ["elasticsearch", "search", "analytics"],
  "comments": [
    {
      "user": "Jane Smith",
      "comment": "Great article!",
      "date": "2023-10-01"
    },
    {
      "user": "Alice Johnson",
      "comment": "Very informative.",
      "date": "2023-10-02"
    }
  ]
}

POST /blog/_doc
{
  "title": "Getting Started with Kibana",
  "content": "Kibana is a data visualization and exploration tool for Elasticsearch.",
  "author": "Alice Johnson",
  "tags": ["kibana", "visualization"],
  "comments": [
    {
      "user": "Bob Brown",
      "comment": "I love using Kibana!",
      "date": "2023-10-03"
    }
  ]
}

POST /blog/_doc
{
  "title": "Advanced Elasticsearch Queries",
  "content": "Learn how to write complex queries in Elasticsearch.",
  "author": "John Doe",
  "tags": ["elasticsearch", "queries"],
  "comments": []
}
```

## Exercise 3: Search Blog Posts

Write a search query to find blog posts that contain the term "elasticsearch" in the title or content.

```json
GET /blog/_search
{
  "query": {
    "multi_match": {
      "query": "elasticsearch",
      "fields": ["title", "content"]
    }
  }
}
```

## Exercise 4: Blog Posts with Comments by User

Write a query to find blog posts where the user "Jane Smith" made a comment.

```json
GET /blog/_search
{
  "query": {
    "nested": {
      "path": "comments",
      "query": {
        "term": {
          "comments.user": "Jane Smith"
        }
      }
    }
  }
}
```


## Exercise 5: Find Posts by Tag

Write a query to find all blog posts that have the tag "elasticsearch".

```json
GET /blog/_search
{
  "query": {
    "term": {
      "tags": "elasticsearch"
    }
  }
}
```
