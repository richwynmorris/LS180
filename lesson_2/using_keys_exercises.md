### Exercise 1

Write a SQL statement that makes a new sequence called "counter".

```SQL
CREATE SEQUENCE counter;
CREATE SEQUENCE
```

## Exercise 2
Write a SQL statement to retrieve the next value from the sequence created in #1.

```SQL
examples=# SELECT nextval('counter');
 nextval 
---------
       1
(1 row)
```

### Exercise 3
Write a SQL statement that removes a sequence called "counter".

```SQL
examples=# DROP SEQUENCE counter;
DROP SEQUENCE
```

### Exercise 4
Is it possible to create a sequence that returns only even numbers? The documentation for sequence might be useful.

```SQL
examples=# CREATE SEQUENCE even_counter INCREMENT BY 2 START WITH 2;
CREATE SEQUENCE
examples=# SELECT nextval('even_counter');
 nextval 
---------
       2
(1 row)

examples=# SELECT nextval('even_counter');
 nextval 
---------
       4
(1 row)

examples=# SELECT nextval('even_counter');
 nextval 
---------
       6
(1 row)
```


### Exercise 5
What will the name of the sequence created by the following SQL statement be?

```SQL
CREATE TABLE regions (id serial PRIMARY KEY, name text, area integer);
```

* regions_id_seq

### Exercise 6
Write a SQL statement to add an auto-incrementing integer primary key column to the films table.

```SQL
examples=# ALTER TABLE films
ADD COLUMN id serial PRIMARY KEY;
ALTER TABLE
```

### Exercise 7
What error do you receive if you attempt to update a row to have a value for id that is used by another row?

```SQL
examples=# UPDATE films SET id=1 WHERE title='Casablanca';
ERROR:  duplicate key value violates unique constraint "id"
DETAIL:  Key (id)=(1) already exists.
```

### Exercise 8
What error do you receive if you attempt to add another primary key column to the films table?

```SQL
examples=# ALTER TABLE films
ADD CONSTRAINT id PRIMARY KEY (genre);
ERROR:  multiple primary keys for table "films" are not allowed
```

### Exercise 9
Write a SQL statement that modifies the table films to remove its primary key while preserving the id column and the values it contains.

```SQL
examples=# ALTER TABLE films
DROP CONSTRAINT id;
ALTER TABLE
```

