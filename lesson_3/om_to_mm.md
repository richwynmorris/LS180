### Exercise 1

```SQL
om-to-mm=# CREATE TABLE directors_films (
id serial PRIMARY KEY,
director_id int REFERENCES directors(id),
film_id int REFERENCES films(id)
);
CREATE TABLE
```

### Exercise 2

```SQL
om-to-mm=# INSERT INTO directors_films (director_id, film_id)
VALUES (1, 1), 
(2,2),
(3,3),
(4,4),
(5,5),
(6,6),
(3, 7),
(7, 8),
(8, 9),
(4, 10);
INSERT 0 10
```

### Exercise 3

```SQL
om-to-mm=# ALTER TABLE films
om-to-mm-# DROP COLUMN director_id;
ALTER TABLE
om-to-mm=# SELECT * FROM films;
 id |           title           | year |   genre   | duration 
----+---------------------------+------+-----------+----------
  1 | Die Hard                  | 1988 | action    |      132
  2 | Casablanca                | 1942 | drama     |      102
  3 | The Conversation          | 1974 | thriller  |      113
  4 | 1984                      | 1956 | scifi     |       90
  5 | Tinker Tailor Soldier Spy | 2011 | espionage |      127
  6 | The Birdcage              | 1996 | comedy    |      118
  7 | The Godfather             | 1972 | crime     |      175
  8 | 12 Angry Men              | 1957 | drama     |       96
  9 | Wayne''s World             | 1992 | comedy    |       95
 10 | Let the Right One In      | 2008 | horror    |      114
(10 rows)
```

### Exercsise 4

```SQL
om-to-mm=# SELECT films.title, directors.name
FROM films
INNER JOIN directors_films
ON films.id = directors_films.film_id
INNER JOIN directors
ON directors.id = directors_films.director_id
om-to-mm-# ORDER BY films.title;
           title           |         name         
---------------------------+----------------------
 12 Angry Men              | Sidney Lumet
 1984                      | Michael Anderson
 Casablanca                | Michael Curtiz
 Die Hard                  | John McTiernan
 Let the Right One In      | Michael Anderson
 The Birdcage              | Mike Nichols
 The Conversation          | Francis Ford Coppola
 The Godfather             | Francis Ford Coppola
 Tinker Tailor Soldier Spy | Tomas Alfredson
 Wayne''s World             | Penelope Spheeris
(10 rows)
```

### Exercise 5

```SQL
om-to-mm=# INSERT INTO films (title, year, genre, duration)
VALUES ('Fargo', 1996, 'comedy', 98),
('No Country for Old Men', 2007, 'western', 122),
('Sin City', 2005, 'crime', 124),
('Spy Kids', 2001, 'scifi', 88);
INSERT 0 4


om-to-mm=# INSERT INTO directors (name)
om-to-mm-# VALUES ('Joel Coen')
om-to-mm-# , ('Ethan Coen')
om-to-mm-# , ('Frank Miller')
om-to-mm-# , ('Robert Rodriguez');
INSERT 0 4



om-to-mm=# INSERT INTO directors_films (director_id, film_id)
om-to-mm-# VALUES (9, 11),
om-to-mm-# (9, 12),
om-to-mm-# (10, 12),
om-to-mm-# (11, 13),
om-to-mm-# (12, 13),
om-to-mm-# (12, 14);
INSERT 0 6
```

### Exercise 6

```SQL
om-to-mm=# SELECT directors.name, COUNT(directors_films.director_id) AS number_of_films
FROM directors
LEFT JOIN directors_films
ON directors.id = directors_films.director_id
LEFT JOIN films
ON films.id = directors_films.film_id
GROUP BY directors.name
ORDER BY number_of_films DESC, directors.name;
         name         | number_of_films 
----------------------+-----------------
 Francis Ford Coppola |               2
 Joel Coen            |               2
 Michael Anderson     |               2
 Robert Rodriguez     |               2
 Ethan Coen           |               1
 Frank Miller         |               1
 John McTiernan       |               1
 Michael Curtiz       |               1
 Mike Nichols         |               1
 Penelope Spheeris    |               1
 Sidney Lumet         |               1
 Tomas Alfredson      |               1
(12 rows)
```

