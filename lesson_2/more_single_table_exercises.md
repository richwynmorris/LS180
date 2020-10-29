### Exercise 1
Create a new database called residents using the PostgreSQL command line tools.

```SQL
createdb residents
```

### Exercise 2
Load this file into the database created in #1.

```SQL
residents= \i Documents/SQL/lesson_2/residents_with_data.sql
```

### Exercise 3
Write a SQL query to list the ten states with the most rows in the people table in descending order.

```SQL
SELECT state, count(state) AS count FROM people
GROUP BY state
ORDER BY count DESC
LIMIT 10;
```

### Exercise 4
Write a SQL query that lists each domain used in an email address in the people table and how many people in the database have an email address containing that domain. Domains should be listed with the most popular first.

### Exercise 5

```SQL
SELECT substr(email, strpos(email, '@') + 1) AS domain, # returns the string from  the index position of '@' to the end of the string. The index position of '@' is found using the 'strpos' method which returns an interger with the position of given string arguement. 

residents-# COUNT(id) as count
residents-# FROM people
residents-# GROUP BY domain
residents-# ORDER BY count;
     domain     | count 
----------------+-------
 fleckens.hu    |   958
 einrot.com     |   965
 dayrep.com     |   966
 teleworm.us    |   998
 jourrapide.com |  1000
 armyspy.com    |  1006
 superrito.com  |  1018
 rhyta.com      |  1024
 gustr.com      |  1029
 cuvox.de       |  1036
(10 rows)
```

### Exercise 6
Write a SQL statement that will delete the person with ID 3399 from the people table.

```SQL
DELETE FROM people WHERE id=3399;
DELETE 1
```
### Exercise 7
Write a SQL statement that will delete all users that are located in the state of California (CA).

```SQL
DELETE FROM people WHERE state='CA';
DELETE 1064
```

### Exercise 8
Write a SQL statement that will update the given_name values to be all uppercase for all users with an email address that contains teleworm.us.

```SQL
UPDATE people SET given_name = UPPER(given_name)
residents-# WHERE email LIKE '%teleworm.us';
UPDATE 889
```

### Exercise 9
Write a SQL statement that will delete all rows from the people table.

```SQL
DELETE FROM people
DELETE 8935
```
