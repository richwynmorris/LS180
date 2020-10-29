### Exercise 1

Load this file into your database.

* What does the file do?
* What is the output of the command? What does each line in this output mean?
* Open up the file and look at its contents. What does the first line do?

**Answer:**
* This files drops any preexisting table that is called `films` and is contained within the `public` area of the database. It then creates a new table called `films` with 3 columns; title, year and genre. Finally, it inserts data into the table to be referenced later.

* The output of the command is:

```SQL
DROP TABLE # This drops any prexisting table called 'films'
CREATE TABLE # This creates a new table to structure any incoming data with columns 
INSERT 0 1 # a new row is added
INSERT 0 1 # a new row is added
INSERT 0 1 # a new row is added
``` 

### Exercise 2
Write a SQL statement that returns all rows in the films table.

```SQL
SELECT * FROM films;
      title       | year |  genre   
------------------+------+----------
 Die Hard         | 1988 | action
 Casablanca       | 1942 | drama
 The Conversation | 1974 | thriller
(3 rows)
```

### Exercise 3
Write a SQL statement that returns all rows in the films table with a title shorter than 12 letters.

```SQL
SELECT * FROM films
examples-# WHERE length(title) < 12;
   title    | year | genre  
------------+------+--------
 Die Hard   | 1988 | action
 Casablanca | 1942 | drama
```

### Exercise 4
Write the SQL statements needed to add two additional columns to the films table: director, which will hold a director's full name, and duration, which will hold the length of the film in minutes.

```SQL
ALTER TABLE films
ADD COLUMN director text,
ADD COLUMN duration int;
```

### Exercise 5
Write SQL statements to update the existing rows in the database with values for the new columns:
title 	director 	duration
Die Hard 	John McTiernan 	132
Casablanca 	Michael Curtiz 	102
The Conversation 	Francis Ford Coppola 	113


```SQL
UPDATE films
SET director='John McTiernan', duration=132
WHERE title='Die Hard'
;
UPDATE 1

UPDATE films
SET director='Michael Curtiz', duration=102
WHERE title='Casablanca'
;
UPDATE 1

UPDATE films
SET director='Francis Ford Coppola', duration=113
WHERE title='The Conversation'
;
UPDATE 1
```

### Exercicse 6
Write SQL statements to insert the following data into the films table:
title 	year 	genre 	director 	duration
1984 	1956 	scifi 	Michael Anderson 	90
Tinker Tailor Soldier Spy 	2011 	espionage 	Tomas Alfredson 	127
The Birdcage 	1996 	comedy 	Mike Nichols 	118

```SQL
INSERT INTO films (title, year, genre, director, duration)
VALUES ('1984', 1956, 'scifi', 'Michael Anderson', 90),
('Tinker Tailor Soldier Spy', 2011, 'espionage', 'Tomas Alfredson', 127),
('The Birdcage', 1996, 'Comedy', 'Mike Nichols', 118);
INSERT 0 3
```

### Exercise 7
Write a SQL statement that will return the title and age in years of each movie, with newest movies listed first:


```SQL
SELECT title, EXTRACT(YEAR FROM CURRENT_DATE) - year AS age FROM films
ORDER BY age; 
           title           | age 
---------------------------+-----
 Tinker Tailor Soldier Spy |   9
 The Birdcage              |  24
 Die Hard                  |  32
 The Conversation          |  46
 1984                      |  64
 Casablanca                |  78
(6 rows)
```

### Exercise 8
Write a SQL statement that will return the title and duration of each movie longer than two hours, with the longest movies first.

```SQL
SELECT title, duration FROM films                                     
WHERE duration > 120
ORDER BY duration DESC;
           title           | duration 
---------------------------+----------
 Die Hard                  |      132
 Tinker Tailor Soldier Spy |      127
(2 rows)
```



### Exercise 9
Write a SQL statement that returns the title of the longest film.

```SQL
SELECT title AS longest_film FROM films
examples-# ORDER BY duration DESC
examples-# LIMIT 1;
 longest_film 
--------------
 Die Hard
(1 row)
```