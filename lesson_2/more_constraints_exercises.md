### Exercise 1
Import this file into a PostgreSQL database.

**Answer**

```SQL
\i path/to/my/file/films2.sql
```

### Exercise 2 
Modify all of the columns to be NOT NULL.

```SQL
ALTER TABLE films
ALTER COLUMN title SET NOT NULL;
ALTER TABLE
examples=# ALTER TABLE films
ALTER COLUMN year SET NOT NULL;
ALTER TABLE
examples=# ALTER TABLE films
ALTER COLUMN genre SET NOT NULL;
ALTER TABLE
examples=# ALTER TABLE films
ALTER COLUMN director SET NOT NULL;
ALTER TABLE
examples=# ALTER TABLE films
ALTER COLUMN duration SET NOT NULL;
ALTER TABLE
```

### Exercise 3
How does modifying a column to be NOT NULL affect how it is displayed by \d films?

```SQL
examples=# \d films
                        Table "public.films"
  Column  |          Type          | Collation | Nullable | Default 
----------+------------------------+-----------+----------+---------
 title    | character varying(255) |           | not null | 
 year     | integer                |           | not null | 
 genre    | character varying(100) |           | not null | 
 director | character varying(255) |           | not null | 
 duration | integer                |           | not null |
 ```

### Exercise 4
Add a constraint to the table films that ensures that all films have a unique title.

```SQL
ALTER TABLE films
ADD CONSTRAINT unique_title UNIQUE(title);
ALTER TABLE
```

### Exercise 5
How is the constraint added in #4 displayed by \d films?

```
Indexes:
    "unique_title" UNIQUE CONSTRAINT, btree (title)
```

### Exercises 6
Write a SQL statement to remove the constraint added in #4.

```SQL
ALTER TABLE films
DROP CONSTRAINT unique_title;
ALTER TABLE
```

### Exericse 7
Add a constraint to films that requires all rows to have a value for title that is at least 1 character long.

```SQL
ALTER TABLE films
ADD CHECK (length(title) >= 1);
ALTER TABLE
```

### Exercise 8
What error is shown if the constraint created in #7 is violated? Write a SQL INSERT statement that demonstrates this.

```SQL
INSERT INTO films
VALUES ('', 1998, 'scifi', 'mr.director', 120);

ERROR:  new row for relation "films" violates check constraint "films_title_check"
DETAIL:  Failing row contains (, 1998, scifi, mr.director, 120).
```

### Exercise 9
How is the constraint added in #7 displayed by \d films?

```SQL
Check constraints:
    "films_title_check" CHECK (length(title::text) >= 1)
```

### Exercise 10
Write a SQL statement to remove the constraint added in #7.

```SQL
ALTER TABLE films
examples-# DROP CONSTRAINT films_title_check;
ALTER TABLE
```

### Exercise 11
Add a constraint to the table films that ensures that all films have a year between 1900 and 2100.

```SQL
ALTER TABLE films
ADD CONSTRAINT correct_year CHECK (year > 1900 AND year < 2100);
ALTER TABLE
```

### Exercise 12
How is the constraint added in #11 displayed by \d films?

```SQL
Check constraints:
    "correct_year" CHECK (year > 1900 AND year < 2100)
```

### Exercise 13
Add a constraint to films that requires all rows to have a value for director that is at least 3 characters long and contains at least one space character ().

```SQL
ALTER TABLE films
examples-# ADD CONSTRAINT full_name CHECK (length(director) > 3 AND director LIKE '% %'); 
ALTER TABLE
```
## Exercise 14
How does the constraint created in #13 appear in \d films?

```SQL
Check constraints:
    "correct_year" CHECK (year > 1900 AND year < 2100)
    "full_name" CHECK (length(director::text) > 3 AND director::text ~~ '% %'::text)
```

### Exercise 15

Write an UPDATE statement that attempts to change the director for "Die Hard" to "Johnny". Show the error that occurs when this statement is executed.

```SQL
UPDATE films
examples-# SET director='Johnny';
ERROR:  new row for relation "films" violates check constraint "full_name"
DETAIL:  Failing row contains (Die Hard, 1988, action, Johnny, 132).
```

### Exercise 16
List three ways to use the schema to restrict what values can be stored in a column.

* Add a data type constraint
* Add NOT NULL
* Add constraint check


### Exercise 17
How can you see a list of all of the constraints on a table?

Use **\d** followed by the table name. The list of constraints are at the bottom. 