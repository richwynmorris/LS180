### Exercise 1
What is the result of using an operator on a NULL value?

**Answer**: AS NULL is representative of 'nothing' and when it is used in an expression it returns `NULL`. `NULL` is automatically is considered the greatest value when being sorted against other values. 

### Exercise 2
Set the default value of column department to "unassigned". Then set the value of the department column to "unassigned" for any rows where it has a NULL value. Finally, add a NOT NULL constraint to the department column.

**Answer**:

```SQL
ALTER TABLE employees
ALTER COLUMN department SET DEFAULT 'unassigned';
ALTER TABLE
```

```SQL
UPDATE employees SET department='unassigned'
WHERE department IS NULL;
UPDATE 1
```

```SQL
ALTER TABLE employees
ALTER COLUMN department
SET NOT NULL;
ALTER TABLE
```

### Exercise 3

Write the SQL statement to create a table called temperatures to hold the following data:

    date    | low | high
------------+-----+------
 2016-03-01 | 34  | 43
 2016-03-02 | 32  | 44
 2016-03-03 | 31  | 47
 2016-03-04 | 33  | 42
 2016-03-05 | 39  | 46
 2016-03-06 | 32  | 43
 2016-03-07 | 29  | 32
 2016-03-08 | 23  | 31
 2016-03-09 | 17  | 28

Keep in mind that all rows in the table should always contain all three values.

**Answer**:

```SQL
CREATE TABLE temperatures (
residents(# date date NOT NULL,
residents(# low int NOT NULL,
residents(# high int NOT NULL);
CREATE TABLE
```

### Exercise 4

Write the SQL statements needed to insert the data shown in #3 into the temperatures table.

**Answer**:

```SQL
INSERT INTO tempreatures
VALUES ('2016-03-01', 34, 43);
INSERT 0 1
residents=# INSERT INTO temperatures
VALUES ('2016-03-02', 32, 44);
INSERT 0 1
residents=# INSERT INTO temperatures
VALUES ('2016-03-03', 31, 47);
INSERT 0 1
residents=# INSERT INTO temperatures
VALUES ('2016-03-04', 33, 42);
INSERT 0 1
residents=# INSERT INTO temperatures
VALUES ('2016-03-05', 39, 46);
INSERT 0 1
residents=# INSERT INTO temperatures
VALUES ('2016-03-06', 32, 44);
INSERT 0 1
residents=# INSERT INTO temperatures
VALUES ('2016-03-07', 29, 32);
INSERT 0 1
residents=# INSERT INTO temperatures
VALUES ('2016-03-08', 23, 31);
INSERT 0 1
residents=# INSERT INTO temperatures
VALUES ('2016-03-09', 17, 28);
INSERT 0 1
```

### Exercise 5
Write a SQL statement to determine the average (mean) temperature -- divide the sum of the high and low temperatures by two) for each day from March 2, 2016 through March 8, 2016. Make sure to round each average value to one decimal place.

```SQL
SELECT date, round(((high + low) / 2), 1) AS mean_temperature FROM temperatures
WHERE EXTRACT (day FROM date) >= 02 AND EXTRACT (day FROM date) <= 08; 
    date    | mean_temperature 
------------+------------------
 2016-03-02 |             38.0
 2016-03-03 |             39.0
 2016-03-04 |             37.0
 2016-03-05 |             42.0
 2016-03-06 |             38.0
 2016-03-07 |             30.0
 2016-03-08 |             27.0
(7 rows)
```

### Exercise 6
Write a SQL statement to add a new column, rainfall, to the temperatures table. It should store millimeters of rain as integers and have a default value of 0.

```SQL
ALTER TABLE temperatures
ADD COLUMN rainfall int DEFAULT 0;
ALTER TABLE
```

### Exercise 7

Each day, it rains one millimeter for every degree the average temperature goes above 35. Write a SQL statement to update the data in the table temperatures to reflect this.

```SQL
ALTER TABLE temperatures
ALTER COLUMN rainfall TYPE numeric (6,4);
ALTER TABLE
residents=# SELECT * FROM temperatures;
    date    | low | high | rainfall 
------------+-----+------+----------
 2016-03-07 |  29 |   32 |   0.0000
 2016-03-08 |  23 |   31 |   0.0000
 2016-03-09 |  17 |   28 |   0.0000
 2016-03-01 |  34 |   43 |   3.0000
 2016-03-02 |  32 |   44 |   3.0000
 2016-03-03 |  31 |   47 |   4.0000
 2016-03-04 |  33 |   42 |   2.0000
 2016-03-05 |  39 |   46 |   7.0000
 2016-03-06 |  32 |   44 |   3.0000
(9 rows)
```

### Exercise 8
A decision has been made to store rainfall data in inches. Write the SQL statements required to modify the rainfall column to reflect these new requirements.

```SQL
residents=# UPDATE temperatures SET rainfall = rainfall * 0.039;
UPDATE 9
residents=# SELECT * FROM temperatures;
    date    | low | high | rainfall 
------------+-----+------+----------
 2016-03-07 |  29 |   32 |   0.0000
 2016-03-08 |  23 |   31 |   0.0000
 2016-03-09 |  17 |   28 |   0.0000
 2016-03-01 |  34 |   43 |   0.1170
 2016-03-02 |  32 |   44 |   0.1170
 2016-03-03 |  31 |   47 |   0.1560
 2016-03-04 |  33 |   42 |   0.0780
 2016-03-05 |  39 |   46 |   0.2730
 2016-03-06 |  32 |   44 |   0.1170
(9 rows)
```

### Exercise 9
Write a SQL statement that renames the temperatures table to weather.

```SQL
ALTER TABLE temperatures RENAME TO weather;
ALTER TABLE
```

### Exercise 10
What psql meta command shows the structure of a table? Use it to describe the structure of weather.

```SQL
\d weather
```

### Exercise 11

What PostgreSQL program can be used to create a SQL file that contains the SQL commands needed to recreate the current structure and data of the weather table?

```SQL

pg_dump -d residents -t weather --inserts > weather_tb.sql

```
* `pg_dump` - *pg_dump is a utility for backing up a PostgreSQL database. Dumps can be output in script or archive file formats. Script dumps are plain-text files containing the SQL commands required to reconstruct the database to the state it was in at the time it was saved. To restore from such a script, feed it to psql. Script files can be used to reconstruct the database even on other machines and other architectures; with some modifications, even on other SQL database products.*
* `-d` - database
* `-t` - table
* `--inserts` - Makes sure the database can be run on other non-POSTgresSQL databases. However, can be very slow. 
* `weather_tb.sql` - Name of the sql file containing the the data and scheme for the weather table. 