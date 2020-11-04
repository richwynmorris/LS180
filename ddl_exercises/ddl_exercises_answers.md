### Exercise 1

```SQL
extrasolar=# CREATE TABLE stars (
id serial PRIMARY KEY,
name varchar(25) UNIQUE NOT NULL,
distance int NOT NULL CHECK (distance > 0),
spectral_type char(1),
companions int NOT NULL CHECK (companions > 0));
CREATE TABLE
extrasolar=# CREATE TABLE planets (
extrasolar(# id serial PRIMARY KEY,
extrasolar(# designation char(1),
extrasolar(# mass int);
CREATE TABLE
```

### Exercise 2 

```SQL
extrasolar=# ALTER TABLE planets
ADD COLUMN star_id int NOT NULL REFERENCES stars (id);
ALTER TABLE
extrasolar=# 
```

### Exercise 3

```SQL
extrasolar=# ALTER TABLE stars
ALTER COLUMN name TYPE varchar(50);
ALTER TABLE
```

### Exercise 4

```SQL
extrasolar=# ALTER TABLE stars
ALTER COLUMN distance TYPE real;
ALTER TABLE
```

### Exercise 5

```SQL
extrasolar=# ALTER TABLE stars
ALTER COLUMN spectral_type SET NOT NULL,
ADD CHECK (spectral_type IN ('O', 'B', 'A', 'F', 'G', 'K', 'm'));
```

OR

```SQL
extrasolar=# ALTER TABLE stars
ADD CHECK (spectral_type ~ '[OBAFGKM]'),
ALTER COLUMN spectral_type SET NOT NULL;
ALTER TABLE
```

### Exercise 6

```SQL
extrasolar=# CREATE TYPE spect_type_val AS ENUM ('O', 'B', 'A', 'F', 'G', 'K', 'M');
CREATE TYPE


extrasolar=# ALTER TABLE stars
ALTER COLUMN spectral_type TYPE spect_type_val
USING spectral_type::spect_type_val;
ALTER TABLE
```

### Exercise 7

```
extrasolar=# ALTER TABLE planets
extrasolar-# ALTER COLUMN mass TYPE numeric;
ALTER TABLE

extrasolar=# ALTER TABLE planets
extrasolar-# ADD CHECK (mass >= 0.0);
ALTER TABLE

extrasolar=# ALTER TABLE planets
ALTER COLUMN designation SET NOT NULL;
ALTER TABLE

extrasolar=# ALTER TABLE planets
extrasolar-# ALTER COLUMN mass SET NOT NULL;
ALTER TABLE
```

### Exercise 8

```SQL
extrasolar=# ALTER TABLE planets
extrasolar-# ALTER COLUMN mass SET NOT NULL;
ALTER TABLE
```


### Exercise 9

```SQL
extrasolar=# CREATE TABLE moons (
id serial PRIMARY KEY,
designation int NOT NULL CHECK (designation > 0),
semi_major_axis numeric CHECK (semi_major_axis > 0.0),
mass numeric CHECK (mass > 0.0),
planets_id int NOT NULL REFERENCES planets(id));
CREATE TABLE
```

### Exercise 10 

```SQL
dropdb extrasolar 
```

OR

```SQL
\c other_database
DROP DATABASE extrasolar
```

