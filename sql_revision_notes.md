# RB180 - Study Guide

### General Database Knowledge

- What is a database?

    A database is a structured set of data that's held in a computer. This structured and organized through the use of tables. Tables are a list of individual data entries (rows) each of which stores the values a set of defined, common attributes (columns). 

- What is a relational database?

    A relational database is way to organise a database based on how the each relation relates to one another. This allows us to describe the relationship between each table or entity and how they interact. This allows us to add greater depth in how we conceptualize how  each relation fits within the context of the database. Moreover this allows us to remove duplicate data that is would be needed across multiple tables. It is in essence, a structured collection of data that follows the relational model. 

- What are SQL, PostgreSQL and MySQL all examples of?

    A relational database management system. They allow us to create, interact, modify and remove tables that exist within a database.

- What does SQL stand for? What is its purpose?

    SQL stands for Structured Query Language and is the programming language that is used to interact with relational databases.

- How is SQL different in its programming language to Ruby?

    SQL is a declarative language which means we only need to explicitly state what needs to be done and not exactly how it should be done.  The query is executed by the relational database management system itself. Ruby, however, is a general purpose programming language.

- How do we interact with a RDBMS?

    To interact with a RDBMS we need to use SQL statements. These are explicit and declarative in nature and allow us to interact and and use a relational database.

- Whats the difference between an SQL query and a SQL statement?

    An SQL query is a subset of the SQL statement. However, a SQL query is more concerned with looking up data and searching through a table while a SQL statement is more concerned with updating or modifying data within a table. Ruby is a general purpose programming language.

- What are the three reasons for learning SQL?

    We interact with structured data on  a daily basis so knowing how to create an manipulate this data is a powerful skillset to develop. 

    Code generated in a general purpose language like Ruby can come and go but the database that is uses will likely far outlive any other code. Therefore, it is important to master the ability to work with relational database management systems.

    Lastly, they help you to build your application on a strong foundation as databases are to key to web applications.

- What is schema? and what is data? What's the difference?

    **Schema** refers to the structure of the database or table within a database. It is primary concerned with the how the data is organized through the use of columns, datatypes and constraints. 

    **Data** refers to the values that held within a table or database. These values are stored in rows within a table and organized by columns. 

- What are the various data types that columns use to distinguish the appropriate values for the columns?
    - **int** - This is a integer data type and only works with whole numbers.
    - **numeric/decimal** - This is a floating point number which can specify where the decimal point is placed. It takes two arguments, the first is the total length of the number and the second in the number of digits that come after the decimal point.
    - **text** - This is a string datatype which holds a string with a maximum length of 65,535 bytes.
    - **char(length) -** This is a fixed string datatype and specifies the length of the string. If the string if less characters, it pads the remaining length of the string with empty spaces.
    - **varchar**(length)  - This is a fixed string datatype and it specifies the length of the string as an argument. If the string is less characters that specified, the **varchar** function only uses the characters it needs and drops the rest.
    - **serial** - This is an autoincrementing integer datatype which works in combination with a sequences to track the last figure used. When new data is added to this column it autoincrements to the next integer. They cannot be NULL.
    - **boolean** - This is a datatype which is either **true** or **false.**
    - **Timestamp** - This datatype uses date and time. It does this through the year, month and day (YYY-MM-DD) and the hour, minute second (HH-MM-SS) format.
    - **Date** - contains the date but does not use the time feature.

### Interacting with PostgreSQL

- Provide an example of a client application in PostgreSQL? What are they?

    Client applications are essential wrappers for SQL commands that be executed through the command line interface. Examples of these could be `createdb` , `dropdb`, `pg_dump` or `pg_restore` .

- What does `psql` do?

     The `psql` command starts up a front end terminal which the user can use for interacting with a PostgreSQL database. You can issue SQL statements and queries from this terminal and see the results of those requests.  

- What are the three different commands you can issue and where do you issue them?

    **Utility functions/Command Line commands** - They are essentially wrappers for SQL statements are used at the command line.

    **PSQL** **Metacommands** - They are used to return information on database or connect to a database. They are issued from the psql console.

    **SQL statements** - These are statements that allows us to interact with a database, These are issued from a psql console. 

- What are the two different commands you can make in a psql console?

    **Metacommands** - These commands always start with a `/` and they are used for a number of different reasons. They can be used to connect to a database, to quit a database or return the structure of a database or table. 

    **SQL statements -** These are used to issues commands to a PosgreSQL database. These are always terminated in a semicolon `;`.

- What is the syntax for creating a database using  a utility function?

    ```sql
    createdb name_of_database
    ```

- What is the `psql` syntax for adding a SQL file to a preexisting postgreSQL database?

    ```sql
    psql -d database_name < my_sql_file.sql 
    ```

- What is `=` used for in a SQL query?

    `=` is used as an equality operator, particularly when used within a `WHERE` clause.

- How can you see what databases exists through the psql console?

    ```sql
    \list
    ```

- What are the syntax conventions when issuing SQL statements?

    You need to use uppercase letters for SQL keywords and lowercase words for databases, tables, columns or rows. Files should be names using snake_case. 

### SQL

- **Identify the different types of JOINs and explain their differences.**
- What is a JOIN?

    A JOIN clause is used to link two tables together, usually based on their keys that define the relationship between the two tables.

- What does INNER JOIN do?

    INNER JOIN is used to return the result of the both tables included in the query at the point of intersection. If a row contains NULL data then that row is excluded from the results. An INNER JOIN is one of the most frequently used JOIN statements used in SQL. 

- What does a LEFT OUTER JOIN do?

    A LEFT OUTER JOIN is used to return the result of two tables joined at the point of intersection. The LEFT OUTER JOIN takes all the rows that are defined as the LEFT table and joins the second table to it. The LEFT tables rows are always returned even in the second table's connecting rows contain NULL values. We do not receive the second table's row if there is no matching row.

- What does RIGHT OUTER JOIN do?

    RIGHT OUTER JOIN returns the result of the two tables that are contained within the query at the point of intersection. The table defined as the RIGHT table will include all of it's rows and data. The second table's rows will still be included in the result even if they contain NULL values.  We do not receive the second table's row if there is no matching row. 

- What does CROSS JOIN do?

    A CROSS JOIN creates the Cartesion product of all the rows contained within both tables. This means we get every possible combination of rows between both tables. This JOIN does not need to specify the intersection between the two tables included in the query. This is a fairly uncommon JOIN.  

- What does a FULL JOIN do?

    A FULL JOIN will return the results of both tables being joined at the specified intersection. This is like a combination of both LEFT JOIN and RIGHT JOIN in the sense that all rows are included between both tables as long as there are matching rows. Any columns that are empty  in the row are provided with the defaulted value of NULL. 

- **Name and define the three sublanguages of SQL and be able to classify different statements by sublanguage.**
- What is DDL?

    DDL is a sub-language of SQL and stands for **Data Definition Language.** This design language is used to create, manipulate and destroy tables and their design schema. It is not concerned with the data contained within the table, only the structure and rules that govern the table itself. DDL uses the keywords **`CREATE`  , `DROP`  and `ALTER`.**   

- WHAT IS DML?

    DML stands for **Data Manipulation Language** and is primary concerned with the insertion, retrieval, manipulation and deletion of data contained within a table's schema. DML uses the `INSERT`, `SELECT` ,`UPDATE`, `DELETE` clauses to manage data within a table.  

- What is DCL?

    DCL stands for **Data Control Language** and is used primary to set authentication permissions when interacting with a database or table. DCL uses clauses like `GRANT` and `REVOKE` as part of its language. 

- **Write SQL statements using INSERT, UPDATE, DELETE, CREATE/ALTER/DROP TABLE, ADD/ALTER/DROP COLUMN.**
- What is the syntax for an `INSERT` statement? What does it do?

    The `INSERT` statement is part of the SQL sub-language Data Manipulation Language and is used to insert data into a table or relation. 

    ```sql
        INSERT INTO table_name (col_1, col_2, col_3 ...)
        VALUES (val_1, val_2, val_3 ..),
        (val_1, val_2, val_3, ...);
        ```
    ```

    *"The order of the columns must match the order of the values to be inserted, but by specifying both the columns and the values, it is much easier to ensure that the order matches up correctly." - Launch School*

- What is the syntax for a `UPDATE` statement? What does it do?

    The `UPDATE` statement is used to modify the preexisting data within a table to a name value. The `UPDATE` statement is part of the SQL sub-language, Data manipulation language. 

    ```sql
    UPDATE table_name SET column_name = new_value
    WHERE column_name = current_value
    ```

    *"The WHERE clause in the above syntax example is optional. If omitted, PostgreSQL will update every row in the target table, so before executing such a query be sure that this is actually what you want to do. Even when using a WHERE clause care must be taken to ensure that it is restrictive or specific enough to target only the rows that you want to modify. You can always test your WHERE clause in a SELECT statement to check which rows are being targeted, before then using it in an UPDATE statement."* - Launch School

- What is the syntax for a `DELETE` statement? What does it do?

    A `DELETE` statement is part of the SQL sub-language, Data Manipulation Language, and is used to delete data contained within a table. 

    ```sql
    DELETE FROM table_name
    WHERE column_name = data;
    ```

    This statement will delete the data contained within the table at the row that matches the expression in the `WHERE` column. 

    ```sql
    DELETE FROM table_name;
    ```

    This statement will delete all the data contained within the table. 

- What is the syntax for a `CREATE` statement?  What does it do?

    The `CREATE` statement is a part of the SQL sub-language, Data Definition Language, and is used to build and design a table's schema. 

    ```sql
    CREATE table_name (
    col_name, data_type, col_constraints_or_keys
    *
    *
    *
    table_constraints
    );
    ```

    Each column in a `CREATE` statement is added on a new line and separated with a `,` . Column names and data types are a required part of the column definitions. The column constraints are optional.  A constraint can be added at the table level by adding it after the list of column definitions.

- What is the syntax for a `ALTER TABLE` statement? What does it do?

    The `ALTER TABLE` statement is used to modify an aspects of a preexisting table's schema. It is often used in conjunction with `RENAME TO` to rename table or `RENAME COLUMN` to change to a column's name. 

    It also the precursor to using the `ALTER COLUMN` syntax to modify a specific column within the table's schema. Moreover, is it also the precursor to the `ADD CONSTRAINT`, `DROP CONSTRAINT`, `ADD COLUMN` and `DROP COLUMN` statements. 

    ```sql
    ALTER TABLE table_name
    RENAME to new_table_name;
    ```

- What is the syntax for a `DROP TABLE` statement? What does it do?

    The `DROP TABLE` syntax is used to delete a table, and data contained within it, from the database. It is non reversible.

    ```sql
    DELETE TABLE table_name; 
    ```

- What is the syntax for a  `ADD COLUMN` statement? What does it do?

    The `ADD COLUMN` STATEMENT is used after the `ALTER TABLE` statement and allows the user to add an additional column to a preexisting table. This is a part of the SQL sub-language **DDL** as it alters a table's schema. The syntax used in this statement mimics that of the definition column definition syntax used in `CREATE TABLE` syntax. 

    ```sql
    ALTER TABLE table_name
    ADD COLUMN col_name data_type constraints; 
    ```

- What is the syntax for a  `ALTER COLUMN` statement? What does it do?

    An `ALTER COLUMN` statement is used after a `ALTER TABLE` statement and is the precursor to a statement which modifies a column in someway.

    This might be through adding a column constraint: 

    ```sql
    #ADD COLUMN CONSTAINT:
    ALTER TABLE table_name
    ALTER COLUMN col_name SET constraint_expression;
    ```

    It can also be used to remove a column constraint. Specifically for `NOT NULL` or `DEFAULT` constraints. 

    ```sql
    ALTER TABLE table_name
    ALTER COLUMN col_name
    DROP CONSTRAINT constraint_name;
    ```

    This could also be used to change a column's datatype 

    ```sql
    # CHANGE COLUMN DATA TYPE:
    ALTER TABLE table_name
    ALTER COLUMN col_name TYPE new_data_type; 
    ```

- What is the syntax for a `DROP COLUMN` statement? What does it do?

    `DROP COLUMN` is a **DDL** statement that is used to drop a column and it's data from a specified table. Its action is nonrecoverable.

    ```sql
    ALTER TABLE table_name
    DROP COLUMN col_name; 
    ```

- **Understand how to use GROUP BY, ORDER BY, WHERE, and HAVING.**
- What is the `GROUP BY` clause and what does it do?

    The `GROUP BY` a clause is used to group data results together to make more meaningful information. `GROUP BY` statements collate rows of the same value together into its own group. NOTE:  `SELECT` statement can only use columns that are used in an aggregate function or listed by the `GROUP BY` clause. Any additional columns that are not used in the context above will throw an error. 

    ```sql
    SELECT col_name, aggre_func(col_name)
    FROM table_name
    GROUP BY col_name; 
    ```

    To  add multiple columns to a `GROUP BY` clause, you need to use a comma to list the specific columns. 

    ```sql
    SELECT col_1, col_2, aggre_fun(col_name)
    FROM table_name
    GROUP BY col_1, col_2
    ```

- What is the `ORDER BY` clause and what does it do?

    The `ORDER BY` clause is used to sort rows in the returned results in particular order. This useful for seeing data contained within rows in a distinct sequence, either ascending or descending. 

    ```sql
    SELECT col_name
    FROM table_name
    WHERE col_name = row_data
    ORDER BY col_name ASC # or DESC
    ; 
    ```

     
    The `ASC` keyword is used to organise the results in an ascending order, starting with the lowest value and ending with the highest. `ASC` is the default when there is no keyword specified. 

    The `DESC` keyword can also be used to organise the results in a descending order. The `DESC` keyword must be specificied as it is not the default choice. 

    You can organise the results by multiple columns by including them in the a list after the `ORDER BY` keyword and organising them by priority. If the two rows have the same data, they will then be organised the secondary `ORDER BY` clause.

    ```sql
    SELECT col_1, col_2, aggr_func() 
    FROM table_name
    ORDER BY col_2 DESC, col_1;  
    ```

- What is the `WHERE` clause used for and what does it do?

    The `WHERE` clause is used as part of a `SELECT` statement to filter rows by comparing a specified expression with the data found in each row. The `WHERE` expression make use of operators to generate an expression. The `WHERE` clause filters at the row level. 

    ```sql
    SELECT col_name
    FROM table_name
    WHERE col_name = data_to_find;
    ```

    The `WHERE` clause can also use the `AND` or `OR` clauses to add greater filtering capabilities to the result returned from the table: 

    ```sql
    SELECT col_1 , col_2 
    FROM table_name
    WHERE col_1 = 1 AND col_2 = 2 # OR col_2 = 2
    ;
    ```

    Moreover, the `WHERE` clause can also use the `LIKE` operator to filter the results based on a matching string pattern expression:

    ```sql
    SELECT col_1
    FROM table_name
    WHERE col_1 LIKE 'new%'
    ```

- What is the `HAVING`  clause used for and what does it do?

    The `HAVING` clause is used in a `SELECT` statement and is used to filter groups of rows.  Therefore, the `HAVING` clause must always be used after a `GROUP BY` clause. 

    ```sql
    SELECT col_1, SUM(col_2)
    FROM table_name
    GROUP BY col_1
    HAVING SUM(col_2) > 5;
    ```

- **Be familiar with using sub**-**queries**
- What is a sub-query?

    A sub-query is a nested query that is used as a condition within an outer query. The result of his nested query is then used the operation of the outer query. This can remove the need to JOIN two separate tables together and may have some performance benefits. However, JOIN statements are generally more efficient. 

- What are the sub query expressions that can be used in combination with a nested query?
    - `IN` - compares the evaluated expression of the outer query to the rows in the virtual table returned by the nested subquery. If the evaluated expression is contained within the nested sub query's result, it returns true the row is selected.
    - `NOT IN` - compares the evaluated expression of the outer query to the rows in the virtual table returned by the nested sub query. If the evaluated expression is NOT in the nested sub query's result, it returns true and the row is selected.
    - `ALL`  - checks if all of the rows selected by evaluated expression of the outer query are in the virtual table returned by the nested sub query. If they are, the statement returns true and the specified rows are selected.  `ALL` uses operators to check for this condition. (=,>,<,)
    - `SOME/ANY`  - checks if any of the rows selected by the evaluated expression of the outer query are contained within in the virtual table returned by the nested sub query. If they are, the statement returns true and all the specified rows are selected. `ANY` of `SOME` uses operators(=,>,<,) to check for this condition.
    - `EXISTS`  - checks to see if the nested sub query returns any results. If it does, it returns true and the specified rows in the outer query are selected.
- Provide an example of sub query.

    ```sql
    CREATE TABLE pets (
    id serial PRIMARY KEY
    name text,
    age int);

    INSERT INTO pets (name, age)
    VALUES ('Torty', 55),
    ('Hudson', 4),
    ('Bongo', 14);
    INSERT 0 3

    SELECT name 
    FROM pets
    WHERE age > (SELECT AVG(age)
            FROM pets);

    name  
    -------
     Torty
    (1 row)

    ```

- What is a reason for using subquerys
    - They could be argued to be more readable and make more logical sense in certain situations.
    - They could be performance benefits to using it over a JOIN statement.

### PostgreSQL

- **Describe what a sequence is and what they are used for.**
- What is a sequence?

     A sequence is a special kind of relation that is automatically generated every time the `serial` keyword is used to define a table's schema. It remembers the last number it generated, so it will generate numbers in a predetermined sequence automatically. It does this using the `nextval` method. This is often used to keep track of, and identify, rows in a table. 

- What are the two ways you can create a sequence.

    You can create a sequence automatically by using the `serial` datatype when creating a table. Moreover, you can manually create a sequence through the use of the `CREATE SEQUENCE` statement followed by a name for the sequence. 

- **Create an auto-incrementing column.**
- What datatype do you use to create an auto incrementing column?

    To create an auto incrementing column, you need to use the `serial` datatype in a column's definition when creating a new table. 

    ```sql
    CREATE TABLE example_table (
    id serial PRIMARY KEY,
    ..
    ..
    );
    ```

- Why would you need to use an auto incrementing column?

    We primary use an auto incrementing column when we want to add a surrogate key to a row. This can be used as a unique identifier for each row. Moreover, this also provides the benefit of auto incrementing each time a new row is added.

- **Define a default value for a column.**
- How do you define a default value for a column?

    You need to add the `DEFAULT` value after the data type in the column definition when creating a table. 

    ```sql
    CREATE TABLE example_table (
    id serial PRIMARY KEY,
    age int DEFAULT 0
    ); 
    ```

    To change a columns value to contain a default value the syntax is:

    ```sql
    ALTER TABLE table_name
    ALTER COLUMN column_name SET DEFAULT 0;
    ```

    To drop a default column:

    ```sql
    ALTER TABLE table_name
    ALTER COLUMN column_name DROP DEFAULT;
    ```

    The `DEFAULT` value set for the column must be the same as the datatype defined for the column. 

- **Be able to describe what primary, foreign, natural, and surrogate keys are**.
- What is a PRIMARY KEY? What is its purpose?

    A `PRIMARY KEY` is a special type of constraint that is used primarily as a unique identifier for a row within a table. A primary key will apply the the `NOT NULL` and `UNIQUE` constraints to the column by default. This allows relationships to be created between two entities. Each table can only have one PRIMARY KEY and this column is conventionally named `id.`   

    Examples:

    ```sql
    # CREATING A TABLE WITH A PRIMARY KEY
    CREATE TABLE table_name (
    id int PRIMARY KEY,
    .,
    .
    );
    ```

    ```sql
    # ADDING A PRIMARY TO A PREEXISTING COLUMN
    ALTER TABLE
    ADD CONSTRAINT pk_column_name PRIMARY KEY (id);
    ```

    ```sql
    # REMOVING A PRIMARY KEY FROM A PREEXISTING COLUMN
    ALTER TABLE
    DROP CONSTRAINT pk_column_name;
    ```

- What constraints does a PRIMARY KEY use by default?

    `UNIQUE` and `NOT NULL`. 

- Why follow the id convention as a PRIMARY KEY?

    Following conventions in software development saves time, reduces confusion, and minimizes the amount of time needed to get up to speed on a new project.

- What is a FOREIGN KEY? What is its purpose?

    A FOREIGN KEY refers to two things: 

    Foreign key column - A foreign key column represents a relationship between two tables. It references a row in a different table using it's primary key.  

    Foreign key constraint - A foreign key constraint is the constraint that is placed on the values contained within foreign key column that it must abide by. 

    "*A Foreign Key allows us to associate a row in one table to a row in another table. This is done by setting a column in one table as a Foreign Key and having that column reference another table's Primary Key column."* - LS

- What are the two ways to add a FOREIGN KEY constraint?

    ```sql
    CREATE TABLE table_name (
    ..,
    ..,
    fk_demon int REFERENCES a_different_table(pk_id)
    ); 
    ```

    ```sql
    ALTER TABLE table_name
    ADD CONSTRAINT fk_custom_name FOREIGN KEY (column_name) REFERENCES a_different_table(pk_id);
    ```

    ```sql
    # DROP A FOREIGN KEY
    ALTER TABLE
    DROP CONSTRAINT fk_custom_name; 
    ```

- How do Foreign Keys help maintain referential integrity?

    *"One of the main benefits of using the foreign key constraints provided by a relational database is to preserve the referential integrity of the data in the database. The database does this by ensuring that every value in a foreign key column exists in the primary key column of the referenced table. Attempts to insert rows that violate the table's constraints will be rejected." - LS*

- What is a natural key?

    A natural key is a column where the data for each row is inherently unique. This can often be identified as something like a user's email address or phone number. 

- Why are natural keys not always suitable?

    Natural keys are not always suitable as they can sometimes change hands or the user may not have valid information that can be used as data. There are ways of getting around this through the use of composite keys (a combination of two natural keys) but it often more effective to use surrogate keys. 

- What is a surrogate key?

    A surrogate key is a value, integrated into the table by the designer, whose sole purpose is to act as a identifier for a specific row in table's data. 

    The most commonly used surrogate key is the `serial`  datatype which is an auto incrementing integer. 

- How can you create a surrogate key?

    To create a surrogate key, it is often best to use the `serial` datatype when defining a column. This means that every time a new row of data is added to the table, the surrogate key will be auto incremented. This means each row will have a unique integer value. 

- **Create and remove CHECK constraints from a column.**
- How do you add a CHECK constraint in a column's definition?

    To add a CHECK constraint in a column's definition you need to use the following syntax:

    ```sql
    CREATE TABLE table_name (
    id serial PRIMARY KEY,
    name text CHECK (length(name) > 0)
    );
    ```

- How do you alter a column to include a CHECK constraint?

    To alter a columns to include a CHECK constraint you need to use the following syntax;

    ```sql
    ALTER TABLE table_name
    ADD CHECK (column_name operator expression); 
    ```

- How do you drop a CHECK constraint from column?

    To drop a constraint, use the following syntax:

    ```sql
    ALTER TABLE
    DROP CONSTRAINT check_name; 
    ```

- How do you create your own custom data type to use in a CHECK constraint?

    Use the `ENUM` function. 

    First create your data type:

    ```sql
    CREATE TYPE custom_type AS ENUM (val1,val2,val3);
    ```

    Use your own custom data type in the table definition:

    ```sql
    CREATE TABLE table_name (
    name custom_type
    );
    ```

    Or change a preexisting column's data type to your custom type:

    ```sql
    ALTER TABLE table_name
    ALTER COLUMN name TYPE custom_type USING name::custom_type;
    ```

- **Create and remove foreign key constraints from a column.**
- How do you add a foreign key when creating a table?

    ```sql
    CREATE TABLE table_name (
    id serial PRIMARY KEY,
    .
    .
    table_2_id int REFERECES table_2(id)
    )
    ```

- How do you add a foreign key to a preexisting column? What factors must be taken into consideration before doing this?

    To add a foreign key to a preexisting column, the syntax is:

    ```sql
    ALTER TABLE table_name
    ADD CONSTRAINT fk_name FOREIGN KEY (column_name) REFERENCES (other_table(id));
    ```

- How do you remove a foreign key from a column?

    ```sql
    ALTER TABLE table_name
    DROP CONSTRAINT fk_name_of_constraint; 
    ```

### Database Diagrams

- What is a relational database?

    Relational databases are called relational as it persists data as a set of relations. A table made up of columns and rows can be considered a relation. If you use something from the `FROM` clause in a `SELECT` statement, it's probably a relation.

    A *relationship* is different in the sense that we use relationship to discuss how two entities (or data contained within tables) relate between one another. A *relation* is simply another way of saying 'table'.

- **Talk about the different levels of schema.**
- What are the 3 different levels of schema? What is each one concerned with?

    The 3 different levels of schema each represent a level of abstraction when designing databases. 

    - Conceptual - "*A high level design focused on entities and their relationships." - Concerned with bigger objects and higher level concepts. Not concerned with how the data will be stored in the database. This will use an entity relationship model to demonstrate the database design.*
    - Logical - This is concerned with the logical implementation of building relationships between entities. Contains attributes and data types that are specific to a particular database. Combination of physical and conceptual. Uses SQL standard column types. Not used most of the time.
    - Physical - .*"A low level database-specific design focused on implementation."- Concerned primarily with entity attributes, data types and rules between entities.*
- **Define cardinality and modality.**
- What is cardinality?

    Cardinality is the number of objects that exist on each side of the relationship.

    *'The number of objects on each side of the relationship (1:1, 1:M, M:M)'*

- What is modality?

    The modality of the relationship indicates whether the relationship between objects is required or not. 

    *'Tells us whether the relationship is required (1) or optional (0).'* 

    If it is required, there must be at least one instance of that entity. If its optional, there doesn't need to be any instances of that entity.

- **Be able to draw database diagrams using crow's foot notation.**
- Do entity relationship models reflect all tables used within a database?
- What does a one to one relationship look like using crow's foot notation?

    A one-to-one relationship looks like a straight line between entities.

- What does a one to many relationship look like using crow's foot notation?

    A one-to-many relationship looks like a straight line terminating in a crow's foot.

- What does a many to many relationship look like using crow's foot notation?

    A many-to-many relationship looks like a crows foot terminating in a crows foot.