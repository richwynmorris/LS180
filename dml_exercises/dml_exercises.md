### Exercise 1

```SQL
workshop=# CREATE TABLE devices (
workshop(# id serial PRIMARY KEY,
workshop(# name text NOT NULL,
workshop(# created_at timestamp DEFAULT current_timestamp);
CREATE TABLE

workshop=# CREATE TABLE parts (
id serial PRIMARY KEY,
part_number int UNIQUE NOT NULL,
device_id int REFERENCES devices(id));
CREATE TABLE
```


### Exercise 2

```SQL
workshop=# INSERT INTO devices (name)
workshop-# VALUES ('Accelerometer');
INSERT 0 1
workshop=# INSERT INTO devices (name)
VALUES ('Gyroscope');
INSERT 0 1
workshop=# SELECT * FROM devices;
 id |     name      |         created_at         
----+---------------+----------------------------
  1 | Accelerometer | 2020-11-05 20:21:04.809933
  2 | Gyroscope     | 2020-11-05 20:21:19.271768
(2 rows)

        ^
workshop=# INSERT INTO parts (part_number, device_id)
workshop-# VALUES (101, 1),
workshop-# (102, 1),
workshop-# (103, 1);
INSERT 0 3


workshop=# INSERT INTO parts (part_number, device_id)
VALUES (201, 2),
(202, 2),
(203, 2),
(204, 2),
(205, 2);
INSERT 0 5

workshop=# INSERT INTO parts (part_number)
VALUES (301),
(302),
(303);
INSERT 0 3
```

### Exercise 3

```SQL
workshop=# SELECT devices.name, parts.part_number FROM devices
workshop-# INNER JOIN parts
workshop-# ON devices.id = parts.device_id;
     name      | part_number 
---------------+-------------
 Accelerometer |         101
 Accelerometer |         102
 Accelerometer |         103
 Gyroscope     |         201
 Gyroscope     |         202
 Gyroscope     |         203
 Gyroscope     |         204
 Gyroscope     |         205
(8 rows)

```

### Exercise 4

```SQL
workshop=# SELECT parts.part_number FROM parts
WHERE CAST (parts.part_number AS text) ~ '^3';
 part_number 
-------------
         301
         302
         303
(3 rows)
```

### Exercise 5

```SQL
workshop=# SELECT devices.name, COUNT(parts.device_id) AS number_of_parts FROM devices 
INNER JOIN parts
ON devices.id = parts.device_id
GROUP BY devices.name;
     name      | number_of_parts 
---------------+-----------------
 Accelerometer |               3
 Gyroscope     |               5
(2 rows)
```

### Exercise 6

```SQL
workshop=# SELECT devices.name, COUNT(parts.device_id) AS number_of_parts FROM devices 
LEFT JOIN parts                                                            
ON devices.id = parts.device_id
GROUP BY devices.name
workshop-# ORDER BY devices.name DESC;
     name      | number_of_parts 
---------------+-----------------
 Gyroscope     |               5
 Accelerometer |               3
(2 rows)

```

### Exercise 7

```SQL
workshop=# SELECT parts.part_number, parts.device_id FROM parts
workshop-# WHERE parts.device_ID IS NOT NULL;
 part_number | device_id 
-------------+-----------
         101 |         1
         102 |         1
         103 |         1
         201 |         2
         202 |         2
         203 |         2
         204 |         2
         205 |         2
(8 rows)

workshop=# SELECT parts.part_number, parts.device_id FROM parts
WHERE parts.device_ID IS NULL;
 part_number | device_id 
-------------+-----------
         301 |          
         302 |          
         303 |          
(3 rows)
```

### Exercise 8

```SQL
workshop=# SELECT name FROM devices
ORDER BY created_at ASC 
LIMIT 1;
     name      
---------------
 Accelerometer
(1 row)
```

### Exercise 9

```SQL
workshop=# UPDATE parts
workshop-# SET device_id = 1
workshop-# WHERE id = 5 or id = 6;
UPDATE 2
workshop=# SELECT * FROM parts;
 id | part_number | device_id 
----+-------------+-----------
  1 |         101 |         1
  2 |         102 |         1
  3 |         103 |         1
  4 |         201 |         2
  7 |         204 |         2
  8 |         205 |         2
  9 |         301 |          
 10 |         302 |          
 11 |         303 |          
 12 |          42 |         3
  5 |         202 |         1
  6 |         203 |         1

workshop=# UPDATE parts
SET device_id = 2
WHERE part_number = (SELECT MIN(part_number) FROM parts);
UPDATE 1

```

### Exercise 10

```SQL
workshop=# DELETE FROM parts WHERE device_id = 1;
DELETE 5
workshop=# DELETE FROM devices WHERE id = 1;
DELETE 1
workshop=# SELECT * FROM devices;
 id |     name     |         created_at         
----+--------------+----------------------------
  2 | Gyroscope    | 2020-11-05 20:21:19.271768
  3 | Magnetometer | 2020-11-05 20:57:43.351406
(2 rows)

```