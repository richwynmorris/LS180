### Exercise 1

Update the orders table so that referential integrity will be preserved for the data between orders and products.

```SQL
examples=# ALTER TABLE orders
examples-# ADD CONSTRAINT orders_products_id_fkey
examples-# FOREIGN KEY (products_id)
examples-# REFERENCES products(id);
``` 

### Exercise 2

```SQL
INSERT INTO products
VALUES (DEFAULT, 'small bolt'),
(DEFAULT, 'large bolt');
INSERT 0 2
examples=# INSERT INTO orders
VALUES (DEFAULT, 1, 10),
(DEFAULT, 1, 25),
(DEFAULT, 2, 15);
INSERT 0 3
```

### Exercise 3
```SQL
examples=# SELECT orders.quantity, products.name 
FROM orders
LEFT JOIN products
examples-# ON orders.product_id = products.id;
 quantity |    name    
----------+------------
       10 | small bolt
       25 | small bolt
       15 | large bolt
(3 rows)
```

### Exercise 4
Can you insert a row into orders without a product_id? Write a SQL statement to prove your answer.

Yes, you can.

```SQL
INSERT INTO orders (id, quantity)
examples-# VALUES (DEFAULT, 10);
INSERT 0 1
```

### Exercise 5 
Write a SQL statement that will prevent NULL values from being stored in orders.product_id. What happens if you execute that statement?

It raises an error as the column already contains NULL values.

```SQL
ALTER TABLE orders ALTER COLUMN product_id SET NOT NULL;
ERROR:  column "product_id" contains null values
```

### Exercise 6
```SQL
 UPDATE orders SET product_id = 2
examples-# WHERE id = 4;
UPDATE 1
examples=# ALTER TABLE orders
examples-# ALTER COLUMN product_id
examples-# SET NOT NULL;
ALTER TABLE
```

### Exercise 7
```SQL
examples=# CREATE TABLE reviews (
 id serial PRIMARY KEY,
product_name int REFERENCES products(id),
review text);
CREATE TABLE
examples=# \d reviews
                               Table "public.reviews"
    Column    |  Type   | Collation | Nullable |               Default               
--------------+---------+-----------+----------+-------------------------------------
 id           | integer |           | not null | nextval('reviews_id_seq'::regclass)
 product_name | integer |           |          | 
 review       | text    |           |          | 
Indexes:
    "reviews_pkey" PRIMARY KEY, btree (id)
Foreign-key constraints:
    "reviews_product_name_fkey" FOREIGN KEY (product_name) REFERENCES products(id)
```

### Exercise 8
```SQL
examples=# INSERT INTO reviews (product_name, review)
examples-# VALUES (1, 'a little small'),
examples-# (1, 'very round!'),
examples-# (2, 'could have been smaller');
INSERT 0 3
examples=# SELECT * FROM reviews;
 id | product_name |         review          
----+--------------+-------------------------
  1 |            1 | a little small
  2 |            1 | very round!
  3 |            2 | could have been smaller
```

