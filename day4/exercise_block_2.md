# Exercise Block #2: Product Catalog

Context:

You are building a product search backend for an e-commerce application. Start by setting up a basic product catalog and enable users to search across product names and descriptions.

## Exercise 1: Define Index Mapping


Define a **products** index with fields:

- name (text + keyword)

- description (text)

- category (keyword)

- price (float)


## Exercise 2: Index Sample Data

```json
{
  "name": "Wireless Headphones",
  "description": "Over-ear Bluetooth headphones with noise canceling.",
  "category": "electronics",
  "price": 99.99
}
{
  "name": "Wireless Mouse",
  "description": "Ergonomic wireless mouse with customizable buttons.",
  "category": "electronics",
  "price": 49.99
}
{
  "name": "Running Shoes",
  "description": "Lightweight running shoes for all terrains.",
  "category": "footwear",
  "price": 79.99
}
{
  "name": "Smartphone",
  "description": "Latest model with high-resolution camera.",
  "category": "electronics",
  "price": 699.99
}
{
  "name": "Yoga Mat",
  "description": "Eco-friendly yoga mat with non-slip surface.",
  "category": "fitness",
  "price": 29.99
}
```


## Exercise 3: Search Products

Write a search query to find products that match the term "wireless" in either the name or description. The search should be case-insensitive and return results sorted by price in ascending order.


## Exercise 4: Filter by Category

Write a query to filter products by category "electronics" and sort the results by price in descending order.

## Exercise 5: Aggregation

Write a query to get the average price of products in each category. The result should include the category name and the average price.
