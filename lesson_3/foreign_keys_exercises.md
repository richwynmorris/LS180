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