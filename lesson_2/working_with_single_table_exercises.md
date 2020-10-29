### Exercise 1
Write a SQL statement that will create the following table, people:
name 	age 	occupation
Abby 	34 	biologist
Mu'nisah 	26 	NULL
Mirabelle 	40 	contractor

```SQL
CREATE TABLE people (
name text,
age int,
occupation text DEFAULT NULL);
CREATE TABLE
```

## Exercise 2
Write SQL statements to insert the data shown in #1 into the table.

```SQL
INSERT INTO people
VALUES ('Abby', 34, 'biologist'),
('Mu''nisah', 26, DEFAULT),
('Mirabelle', 40, 'contractor');
INSERT 0 3
```

### Exercise 3
Write 3 SQL queries that can be used to retrieve the second row of the table shown in #1 and #2.

```SQL
SELECT * FROM people
WHERE name='Mu''nisah';
   name   | age | occupation 
----------+-----+------------
 Mu'nisah |  26 | 
(1 row)

SELECT * FROM people
WHERE age=26;
   name   | age | occupation 
----------+-----+------------
 Mu'nisah |  26 | 
(1 row)

SELECT * FROM people
WHERE occupation IS NULL;
   name   | age | occupation 
----------+-----+------------
 Mu'nisah |  26 | 
(1 row)

```

### Exercise 4
Write a SQL statement that will create a table named birds that can hold the following values:
name 	length 	wingspan 	family 	extinct
Spotted Towhee 	21.6 	26.7 	Emberizidae 	f
American Robin 	25.5 	36.0 	Turdidae 	f
Greater Koa Finch 	19.0 	24.0 	Fringillidae 	t
Carolina Parakeet 	33.0 	55.8 	Psittacidae 	t
Common Kestrel 	35.5 	73.5 	Falconidae 	f


```SQL
CREATE TABLE birds (
examples(# name text,
examples(# length numeric(3,1),
examples(# wingspan numeric(3,1),
examples(# family text,
examples(# extinct boolean);
CREATE TABLE
```

### Exercise 5
Using the table created in #4, write the SQL statements to insert the data as shown in the listing.

```SQL
INSERT INTO birds
VALUES ('Spotted Towhee', 21.6, 26.7, 'Emberizidae', false),
('American Robin', 25.5, 36.0, 'Turdidae', false),
('Greater Koa Finch', 19.0, 24.0, 'Fringillidae', true),
('Carolina Parakeet', 33.0, 55.8, 'Psittacidae', true),
('Common Kestrel', 35.5, 73.5, 'Falconidae', false);
INSERT 0 5
```

### Exercise 6
Write a SQL statement that finds the names and families for all birds that are not extinct, in order from longest to shortest (based on the length column's value).

```SQL
SELECT name, family FROM birds
WHERE extinct=false
ORDER BY length DESC;
      name      |   family    
----------------+-------------
 Common Kestrel | Falconidae
 American Robin | Turdidae
 Spotted Towhee | Emberizidae
(3 rows)
```

### Exercise 7
Use SQL to determine the average, minimum, and maximum wingspan for the birds shown in the table.


```SQL
SELECT round(avg(wingspan),1), min(wingspan), max(wingspan) FROM birds;
 round | min  | max  
-------+------+------
  43.2 | 24.0 | 73.5
(1 row)

SELECT round(avg(wingspan),1), min(wingspan), max(wingspan) FROM birds;
 round | min  | max  
-------+------+------
  43.2 | 24.0 | 73.5
(1 row)
```



### Exercise 8
Write a SQL statement to create the table shown below, menu_items:
item 	prep_time 	ingredient_cost 	sales 	menu_price
omelette 	10 	1.50 	182 	7.99
tacos 	5 	2.00 	254 	8.99
oatmeal 	1 	0.50 	79 	5.99

```SQL
CREATE TABLE menu_items
examples-# ( item text,
examples(# prep_time int,
examples(# ingredient_cost numeric (4,2),
examples(# sales int,
examples(# menu_price numeric(4,2));
CREATE TABLE
```

### Exercise 9
Write SQL statements to insert the data shown in #8 into the table.

```SQL
INSERT INTO menu_items
examples-# VALUES ('omelette', 10, 1.50, 182, 7.99),
examples-# ('tacos', 5, 2.00, 254, 8.99),
examples-# ('oatmeal', 1, 0.50, 79, 5.99);
INSERT 0 3
```

### Exercise 10
Using the table and data from #8 and #9, write a SQL query to determine which menu item is the most profitable based on the cost of its ingredients, returning the name of the item and its profit.

```SQL
SELECT item, menu_price - ingredient_cost AS profit 
examples-# FROM menu_items
examples-# ORDER BY profit
examples-# DESC LIMIT 1;
 item  | profit 
-------+--------
 tacos |   6.99
(1 row)
```


### Exercise 11
Write a SQL query to determine how profitable each item on the menu is based on the amount of time it takes to prepare. Assume that whoever is preparing the food is being paid $13 an hour. List the most profitable items first. Keep in mind that prep_time is represented in minutes and ingredient_cost and menu_price are in dollars and cents):

```SQL
SELECT item, menu_price, ingredient_cost,
round(prep_time/60.0 * 13.0, 2) AS labour, 
menu_price - round(prep_time/60.0 * 13.0, 2) - ingredient_cost AS profit
FROM menu_items```
ORDER BY profit
DESC;
   item   | menu_price | ingredient_cost | labour | profit 
----------+------------+-----------------+--------+--------
 tacos    |       8.99 |            2.00 |   1.08 |   5.91
 oatmeal  |       5.99 |            0.50 |   0.22 |   5.27
 omelette |       7.99 |            1.50 |   2.17 |   4.32
(3 rows)
```