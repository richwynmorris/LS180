## Exercise 1

SQL consists of 3 different sublanguages. For example, one of these sublanguages is called the Data Control Language (DCL) component of SQL. It is used to control access to a database; it is responsible for defining the rights and roles granted to individual users. Common SQL DCL statements include:

`GRANT`
`REVOKE`

Name and define the remaining 2 sublanguages, and give at least 2 examples of each.

### Answer

**DDL - Data Definition Language** = `CREATE`,`DROP`, `ALTER`.
**DML - Data Manipulation Language** = `SELECT`, `DELETE`, `UPDATE`, `INSERT`. 

## Exercise 2

Does the following statement use the Data Definition Language (DDL) or the Data Manipulation Language (DML) component of SQL?

```SQL
SELECT column_name FROM my_table;
```

### Answer
This is using the **DML** language to retrieve data from the relational database.

## Exercise 3

Does the following statement use the DDL or DML component of SQL?

```SQL
CREATE TABLE things (
  id serial PRIMARY KEY,
  item text NOT NULL UNIQUE,
  material text NOT NULL
);
```

### Answer
This uses the DDL component of SQL as it is defining the schema and the data definitions stored in relational database. 


## Exercise 4

Does the following statement use the DDL or DML component of SQL?

```SQL
ALTER TABLE things
DROP CONSTRAINT things_item_key;
```
### Answer
This uses the DDL component of SQL as we are manipulating the way data can be stored within the schema. This does not modify the data directly only the data definitions.


## Exercise 5

Does the following statement use the DDL or DML component of SQL?

```SQL
INSERT INTO things VALUES (3, 'Scissors', 'Metal');
```

### Answer
This uses the DML component of SQL as we are directly modfiying the data that is stored within the schema of the database by adding values to the database.


## Exercise 6

Does the following statement use the DDL or DML component of SQL?

```SQL
UPDATE things
SET material = 'plastic'
WHERE item = 'Cup';
```

## Answer 
This uses the DML component of SQL as it is directly modifying the data by changing the preexisting values with new ones using a conditional WHERE keyword. 


## Exercise 7

Does the following statement use the DDL, DML, or DCL component of SQL?

```SQL
\d things
```

### Original Answer - WRONG
~~This statement uses the DCL component of SQL as it relates to viewing the data associated with the table `things`. Dependent on whether the user making the request has the correct permissions will determine whether they can view the data contained within the table.~~

### Correct Answer
It relates to non of these as it is a `psql` console command and has nothing directly to do with SQL. It acts similarly to a DDL command `DESRIBE` as it displays the schema of the named table. 


## Exercise 8

Does the following statement use the DDL or DML component of SQL?

```SQL
DELETE FROM things WHERE item = 'Cup';
```

## Answer
This uses the DML component of SQL as it is removing data contained withing the database. As it is concerned with manipulation of the data directly and not the structure of the data it is related to DML. 

## Exercise 9 

Does the following statement use the DDL or DML component of SQL?

```SQL
DROP DATABASE xyzzy;
```

## Answer
This is related to the DDL component of SQL as we are deleting the structure, and it's data entirely. This declaration can only be made from a database that isn't the one that's being dropped. 

## Exercise 10

Does the following statement use the DDL or DML component of SQL?

```SQL
CREATE SEQUENCE part_number_sequence;
```

## Answer

As a `SEQUENCE` is related to the creation of tables and tables help us to structure our data within a database, I think this is a component of DDL. 

*notes* - CREATE SEQUENCE statements modify the characteristics and attributes of a database by adding a sequence object to the database structure. 