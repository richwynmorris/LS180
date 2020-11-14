# RB180 - Study Guide

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
    DELETE table_name
    WHERE column_name = data;
    ```

    This statement will delete the data contained within the table at the row that matches the expression in the `WHERE` column. 

    ```sql
    DELETE table_name;
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
    ORDER BY ASC # or DESC
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

    A sub-query is a nested query that is performed within an outer outer query. The result of his nested query is then used the operation of the outer query. This can remove the need to JOIN two separate tables and may have some performance benefits. However, JOIN statements are generally more efficient. 

- What are the sub query expressions that can be used in combination with a nested query?
    - `IN` - compares the evaluated expression of the outer query to the rows in the nested subquery. If the evalutated expression is in the contained within the nested sub query's rows, it returns true the row is selected.
    - `NOT IN` - compares the evaluated expression of the outer query to the rows in the nested sub query. If the evaluated expression is NOT in the row, it returns true and the row is selected.
    - `ALL`  - checks if all of the rows selected by evaluated expression of outer query are in the nested sub query. If they are, the statement returns true and the specified rows are selected.
    - `SOME/ANY`  - checks if any of the rows selected by the evaluated expression of the outer query are contained within in the nested sub query. If they are, the statement returns true and all the specified rows are selected.
    - `EXISTS`  - checks to see the row selected by the evaluated expression of the outer query exists within the nested sub query. If it does, it returns true and the specified rows are selected.
- Provide an example of sub query

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

### PostgreSQL

- Describe what a sequence is and what they are used for.
- Create an auto-incrementing column.
- Define a default value for a column.
- Be able to describe what primary, foreign, natural, and surrogate keys are.
- Create and remove CHECK constraints from a column.
- Create and remove foreign key constraints from a column.

### Database Diagrams

- Talk about the different levels of schema.
- Define cardinality and modality.
- Be able to draw database diagrams using crow's foot notation.