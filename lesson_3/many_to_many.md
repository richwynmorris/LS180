### Exercise 1

```SQL
examples=# SELECT books.id, books.author, string_agg(categories.name, ', ') AS categories
FROM books
LEFT JOIN books_categories
ON books.id = books_categories.book_id
LEFT JOIN categories
ON categories.id = books_categories.category_id
GROUP BY books.id
examples-# ORDER BY books.id;
 id |     author      |           categories           
----+-----------------+--------------------------------
  1 | Charles Dickens | Fiction, Classics
  2 | J. K. Rowling   | Fiction, Fantasy
  3 | Walter Isaacson | Nonfiction, Biography, Physics
```


### Exercise 2

Step 1:

```SQL
examples=# ALTER TABLE books
examples-# ALTER COLUMN title TYPE text;
ALTER TABLE
```

Step 2:

```SQL
examples=# INSERT INTO books (title, author)
VALUES ('Sally Ride: America''s First Woman in Space', 'Lynn Sherr'),
('Jane Eyre', 'Charlotte Bronte'),
('Vij''s: Elegant and Inspired Indian Cuisine', 'Meeru Dhalwala and Vikram Vij');
INSERT 0 3
```

Step 3:

```SQL
examples=# INSERT INTO categories (name)
VALUES ('Space Exploration'),
('Cookbook'),
examples-# ('South Asia');
INSERT 0 3
```


Step 4:

```SQL
examples=# INSERT INTO books_categories (book_id, category_id)
examples-# VALUES (4, 5);
INSERT 0 1
examples=# INSERT INTO books_categories (book_id, category_id)
VALUES (4, 1);
INSERT 0 1
examples=# INSERT INTO books_categories (book_id, category_id)
VALUES (4, 7);
INSERT 0 1
examples=# INSERT INTO books_categories (book_id, category_id)
VALUES (5, 2);
INSERT 0 1
examples=# INSERT INTO books_categories (book_id, category_id)
VALUES (5, 4);
INSERT 0 1
examples=# INSERT INTO books_categories (book_id, category_id)
VALUES (6, 8);
INSERT 0 1
examples=# INSERT INTO books_categories (book_id, category_id)
VALUES (6, 1);
INSERT 0 1
examples=# INSERT INTO books_categories (book_id, category_id)
VALUES (6, 9);
INSERT 0 1
```

Step 4:

```SQL
examples=# SELECT books.id, books.author, string_agg(categories.name, ', ') AS categories
FROM books
LEFT JOIN books_categories
ON books.id = books_categories.book_id
LEFT JOIN categories
ON categories.id = books_categories.category_id
GROUP BY books.id
ORDER BY books.id, categories;
 id |            author             |                categories                
----+-------------------------------+------------------------------------------
  1 | Charles Dickens               | Fiction, Classics
  2 | J. K. Rowling                 | Fiction, Fantasy
  3 | Walter Isaacson               | Nonfiction, Biography, Physics
  4 | Lynn Sherr                    | Biography, Nonfiction, Space Exploration
  5 | Charlotte Bronte              | Fiction, Classics
  6 | Meeru Dhalwala and Vikram Vij | Cookbook, Nonfiction, South Asia
(6 rows)
```

### Exercise 3

```SQL
examples=# ALTER TABLE books_categories
examples-# ADD CONSTRAINT unique_values UNIQUE (book_id, category_id); 
ALTER TABLE
```


### Exercise 4

```SQL
examples=# SELECT categories.name, COUNT(books_categories.category_id) AS book_count, string_agg(books.title, ', ') FROM books 
INNER JOIN books_categories
ON books.id = books_categories.book_id
INNER JOIN categories
ON categories.id = books_categories.category_id
GROUP BY categories.name
examples-# ORDER BY categories.name;
```