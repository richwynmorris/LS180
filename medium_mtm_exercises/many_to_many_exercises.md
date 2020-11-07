### Exercise 1 

```SQL
billing=# CREATE TABLE customers (
id serial PRIMARY KEY,
name text NOT NULL,
payment_token varchar(8) CHECK (payment_token = upper(payment_token) AND length(payment_token) = 8));
CREATE TABLE
billing=# 

billing=# CREATE TABLE services (
billing(# id serial PRIMARY KEY,
billing(# description text NOT NULL,
billing(# price numeric(10,2) NOT NULL CHECK (price > 0.00));
CREATE TABLE

billing=# INSERT INTO customers (name, payment_token)
billing-# VALUES ('Pat Johnson', 'XHGOAHEQ'),
billing-# ('Nancy Monreal' ,'JKWQPJKL'),
billing-# ('Lynn Blake', 'KLZXWEEE'),
billing-# ('Chen Ke-Hua', 'KWETYCVX'),
billing-# ('Scott Lakso', 'UUEAPQPS'),
billing-# ('Jim Pornot', 'XKJEYAZA');
INSERT 0 6


billing=# INSERT INTO services (description, price)
VALUES ('Unix Hosting', 5.95),
('DNS', 4.95),
('Whois Registration', 1.95),
('High Bandwidth', 15.00),
billing-# ('Business Support',250.00),
billing-# ('Dedicated Hosting', 50.00),
billing-# ('Bulk Email', 250.00),
billing-# ('One-to-one Training', 999.00);
INSERT 0 8


billing=# CREATE TABLE customers_services (
id serial PRIMARY KEY,
service_id int REFERENCES services(id),
customer_id int REFERENCES customers(id) ON DELETE CASCADE,
CONSTRAINT unique_customer_service UNIQUE (service_id, customer_id) 
);
CREATE TABLE

billing=# INSERT INTO services_customers (service_id, customer_id)
VALUES (1, 1);
INSERT 0 1
billing=# INSERT INTO services_customers (service_id, customer_id)
VALUES (2, 1);
INSERT 0 1
billing=# INSERT INTO services_customers (service_id, customer_id)
VALUES (3, 1);
INSERT 0 1
billing=# INSERT INTO services_customers (service_id, customer_id)
VALUES (NULL, 2);
INSERT 0 1
billing=# INSERT INTO services_customers (service_id, customer_id)
VALUES (1, 3);
INSERT 0 1
billing=# INSERT INTO services_customers (service_id, customer_id)
VALUES (2, 3);
INSERT 0 1
billing=# INSERT INTO services_customers (service_id, customer_id)
VALUES (3, 3);
INSERT 0 1
billing=# INSERT INTO services_customers (service_id, customer_id)
VALUES (4, 3);
INSERT 0 1
billing=# INSERT INTO services_customers (service_id, customer_id)
VALUES (5, 3);
INSERT 0 1
billing=# INSERT INTO services_customers (service_id, customer_id)
VALUES (1, 4);
INSERT 0 1
billing=# INSERT INTO services_customers (service_id, customer_id)
VALUES (4, 4);
INSERT 0 1
billing=# INSERT INTO services_customers (service_id, customer_id)
VALUES (1, 5);
INSERT 0 1
billing=# INSERT INTO services_customers (service_id, customer_id)
VALUES (2, 5);
INSERT 0 1
billing=# INSERT INTO services_customers (service_id, customer_id)
VALUES (6, 5);
INSERT 0 1
billing=# INSERT INTO services_customers (service_id, customer_id)
VALUES (1, 6);
INSERT 0 1
billing=# INSERT INTO services_customers (service_id, customer_id)
VALUES (6, 6);
INSERT 0 1
billing=# INSERT INTO services_customers (service_id, customer_id)
VALUES (7, 6);
INSERT 0 1
```

### Exercise 2

```SQL
billing=# SELECT customers.name, customers.payment_token FROM customers
INNER JOIN services_customers
ON customers.id = services_customers.customer_id
billing-# GROUP BY customers.name, customers.payment_token;
```

### Exercise 3

```SQL
billing=# SELECT DISTINCT customers.name, customers.payment_token FROM customers
LEFT JOIN services_customers
ON customers.id = services_customers.customer_id
WHERE services_customers.service_id IS NULL;
     name      | payment_token 
---------------+---------------
 Nancy Monreal | JKWQPJKL
(1 row)

billing=# SELECT DISTINCT customers.*, services.* FROM customers
FULL JOIN services_customers
ON customers.id = services_customers.customer_id
FULL JOIN services
ON services.id = services_customers.service_id
WHERE service_id IS NULL or customer_id IS NULL;
```

### Exercise 4

```SQL
billing=# SELECT description
FROM services_customers
RIGHT OUTER JOIN services
ON services_customers.service_id = services.id
WHERE service_id IS NULL;
     description     
---------------------
 One-to-one Training
(1 row)
``` 

### Exercise 5

```SQL
billing=# SELECT customers.name, string_agg(services.description, ', ') FROM customers
LEFT JOIN services_customers
ON customers.id = services_customers.customer_id
LEFT JOIN services
ON services.id = services_customers.service_id
GROUP BY customers.name, customers.id
ORDER BY customers.id;
 ```



