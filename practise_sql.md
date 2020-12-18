## Exercise 1 

Write a SQL query to get the second highest salary from the Employee table.

+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+

For example, given the above Employee table, the query should return 200 as the second highest salary. If there is no second highest salary, then the query should return null.

+---------------------+
| SecondHighestSalary |
+---------------------+
| 200                 |
+---------------------+

### Answer

```SQL
SELECT MAX(Salary) AS SecondHighestSalary
FROM Employee
WHERE salary < (SELECT MAX(salary) FROM Employee);
```

## Exercise 2

Deep within the fair realm of Lothlórien, you have been asked to create a shortlist of candidates for a recently vacated position on the council.

Of so many worthy elves, who to choose for such a lofty position? After much thought you decide to select candidates by name, which are often closely aligned to an elf's skill and temperament.

Choose those with tegil appearing anywhere in their first name, as they are likely to be good calligraphers, OR those with astar anywhere in their last name, who will be faithful to the role.

Elves table:

    firstname
    lastname

all names are in lowercase

To aid the scribes, return the firstname and lastname column concatenated, separated by a space, into a single shortlist column, and capitalise the first letter of each name.


```SQL

SELECT Concat_ws(' ', initcap(firstname), initcap(lastname)) AS shortlist FROM Elves
WHERE firstname LIKE '%tegil%' OR lastname LIKE '%astar%';
```

## Exercise 3 (working)

Task

Given the information about sales in a store, calculate the total revenue for each day, month, year, and product.
Notes

    Order the result by the product_name, year, month, day columns
    We're interested only in the product-specific data, so you shouldn't return the total revenue from all sales

Input tables

----------------------------------------
|    Table      |   Column   |  Type   |
|---------------+------------+---------|
| products      | id         | int     |
|               | name       | text    |
|               | price      | numeric |
|---------------+------------+---------|
| sales         | id         | int     |
|               | date       | date    |
|---------------+------------+---------|
| sales_details | id         | int     |
|               | sale_id    | int     |
|               | product_id | int     |
|               | count      | int     |
-----------------------------------------

Output table

--------------------------
|    Column    |  Type   |
|--------------+---------|
| product_name | text    |
| year         | int     |
| month        | int     |
| day          | int     |
| total        | numeric |
--------------------------

Example output

product_name | year | month | day | total
-------------+------+-------+-----+------
 milk        | 2019 | 01    | 01  | 200
 milk        | 2019 | 01    | 02  | 190
 milk        | 2019 | 01    |     | 390
 milk        | 2019 | 02    | 01  | 240
 milk        | 2019 | 02    |     | 240
 milk        | 2019 |       |     | 630
 milk        |      |       |     | 630

 ```SQL
 SELECT products.name AS product_name, date_part('year', sales.date) AS "year", date_part('month', sales.date) AS "month", date_part('day', sales.date) AS "day", SUM(products.price) FROM products
LEFT JOIN sales_details
ON products.id = sales_details.product_id
LEFT JOIN sales
ON sales_details.sale_id = sales.id
```
