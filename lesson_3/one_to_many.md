### Exercise 1

```SQL
INSERT INTO calls ("when", duration, contact_id)
examples-# VALUES ('2016-01-18 14:47:00', 632, 6);
INSERT 0 1
```

### Exercise 2

```SQL
SELECT calls.when, calls.duration, contacts.first_name FROM calls
INNER JOIN contacts
ON calls.contact_id = contacts.id
examples-# WHERE contacts.id <> 6;
        when         | duration | first_name 
---------------------+----------+------------
 2016-01-08 15:30:00 |      350 | Yuan
 2016-01-11 11:06:00 |      111 | Tamila
 2016-01-13 18:13:00 |     2521 | Tamila
 2016-01-17 09:43:00 |      982 | Yuan
(4 rows)
```

### Exercise 3
```SQL
INSERT INTO contacts (first_name, last_name, number)
examples-# VALUES ('Merve', 'Elk', 6343511126),
examples-# ('Sawa', 'Fyodorov', 6125594874);
INSERT 0 2
examples=# SELECT * FROM contacts;
 id | first_name | last_name |   number   
----+------------+-----------+------------
  6 | William    | Swift     | 7204890809
 17 | Yuan       | Ku        | 2195677796
 25 | Tamila     | Chichigov | 5702700921
 26 | Merve      | Elk       | 6343511126
 27 | Sawa       | Fyodorov  | 6125594874
(5 rows)

examples=# INSERT INTO calls ("when", duration, contact_id)
VALUES ('2016-01-17 11:52:00', 175, 26),
examples-# ('2016-01-18 21:22:00', 79, 27);
INSERT 0 2
```

### Exercise 4

```SQL
examples=# ALTER TABLE contacts
ADD CONSTRAINT unique_number UNIQUE (number);
ALTER TABLE
```

### Exercise 5

```SQL
INSERT INTO contacts (first_name, last_name, number)
VALUES ('Different', 'Person', 6343511126);
ERROR:  duplicate key value violates unique constraint "unique_number"
DETAIL:  Key (number)=(6343511126) already exists.
```

### Exercise 6
When as an column identifier needs to be in quotation marks as it is also an SQL keyword. By placing it in quotations marks, we're able to indicate to postgres that the it's not a declaration but a unique identifier. 

