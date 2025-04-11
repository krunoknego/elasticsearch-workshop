# Exercise Block #3: Product Catalog Autocomplete

Context:

Now you want to implement autocomplete for product search and improve search quality with phrase and exact matching.

## Exercise 1: Define Autocomplete Mapping

Define a **products_autocomplete** index with fields:
- name (text + keyword with tokenizer for autocomplete)

- description (text)

- category (keyword)

- price (float)

## Exercise 2: Reindex the Data from products to products_autocomplete

Reindex the data from the **products** index to the **products_autocomplete** index.

## Exercise 3: Autocomplete Search

Write a query to find products that match the term "wire" in the `name` field. 

## Exercise 4: Find Products in Electronics Category and Filter Them by Price 

Write a query to find products in the "electronics" category with a price less than 50. Sort the results by price in ascending order.
