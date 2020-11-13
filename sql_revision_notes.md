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

- What is the syntax for an `INSERT` statement?

    ```SQL
    INSERT INTO table_name (col_1, col_2, col_3 ...)
    VALUES (val_1, val_2, val_3 ..),
    (val_1, val_2, val_3, ...);
    ```    


- Understand how to use GROUP BY, ORDER BY, WHERE, and HAVING.
- Be familiar with using subqueries

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
