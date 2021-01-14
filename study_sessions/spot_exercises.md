1)  Return a table that contains first name and last name of all employees

Extension: change the column names so they read a more human friendly manner.

```SQL
SELECT first_name, last_name FROM employees;
```

2) Return a table to the console that returns the first name and last name of each
employee aswell as the the department that they belong to.


Output:

 first_name | last_name | Department  
------------+-----------+-------------
 John       | Smith     | Reporting
 Ian        | Peterson  | Engineering
 Mike       | Peterson  | Engineering
 Cailin     | Ninson    | Engineering
 John       | Mills     | Marketing
 Ava        | Muffinson | Silly Walks

Extension: Can you show only the employees that belong to the 'engineering' department?

```SQL
SELECT first_name, last_name, departments.name AS "Department" FROM employees
INNER JOIN departments
ON employees.department_id = departments.id;
```

3) Return a table where you group the employees, in a single column, by their department using their first name. 
   Sort the departments by alphabetical order.

   Extension: can you output both first name and last name of the employee to 'Employees' column? 

   Output:

        Employees     | Department  
   -------------------+-------------
    Ian, Mike, Cailin | Engineering
    John              | Marketing
    John              | Reporting
    Ava               | Silly Walks

```SQL
SELECT string_agg(employees.first_name, ', ') AS "Employees", departments.name AS "Department" FROM employees
INNER JOIN departments
ON employees.department_id = departments.id
GROUP BY departments.name
ORDER BY "Department" 
```

4) It looks quite busy using both the first name and last name in the employees column. 

   Let's just the initial of the employees first name and their last name. 

   https://www.postgresql.org/docs/12/functions-string.html

   Output:
               Employees             | Department  
   ----------------------------------+-------------
    I Peterson, M Peterson, C Ninson | Engineering
    J Mills                          | Marketing
    J Smith                          | Reporting
    A Muffinson                      | Silly Walks


  ```SQL
  SELECT string_agg(concat(left(employees.first_name, 1), ' ', employees.last_name), ', ') AS "Employees", departments.name AS "Department" FROM employees
  INNER JOIN departments
  ON employees.department_id = departments.id
  GROUP BY departments.name
  ORDER BY "Department" 
```
 
5) Add a 'Total employees' column with the number of employees in each department. Order this in descending order. 

  Output: 

            Employees             | Department  | Total Employees 
----------------------------------+-------------+-----------------
 I Peterson, M Peterson, C Ninson | Engineering |               3
 J Smith                          | Reporting   |               1
 J Mills                          | Marketing   |               1
 A Muffinson                      | Silly Walks |               1

  ```SQL
  SELECT string_agg(concat(left(employees.first_name, 1), ' ', employees.last_name), ', ') AS "Employees", departments.name AS "Department", count(employees.department_id) as "Total Employees" FROM employees
  INNER JOIN departments
  ON employees.department_id = departments.id
  GROUP BY departments.name
  ORDER BY "Total Employees" DESC
  ```

6) Return a table that contains 'Employees', 'Department', 'Total Projects', and 'Total Budget' columns. 

You will need to use the many-to-many relationship between employees and projects using a join table.

You should organise the 'Total Projects' column in descending order. 

Output:

             Employee             | Total Projects | Total Budget 
----------------------------------+----------------+--------------
 C Ninson, M Peterson, I Peterson |              3 |      3000000
 A Muffinson                      |              1 |          100
 J Smith                          |              1 |       100000
 J Mills                          |              0 |             
(4 rows)

Extension: there's data in the system which could potentially cause issues. Can you find it and fix it?

```SQL
SELECT string_agg(concat(left(employees.first_name, 1), ' ', employees.last_name), ', ') AS "Employee", count(employee_id) AS "Total Projects", SUM(projects.budget) AS "Total Budget" FROM employees
FULL JOIN employees_projects
ON employees.id = employees_projects.employee_id
FULL JOIN projects
ON employees_projects.project_id = projects.id
GROUP BY projects.title
ORDER BY "Total Projects" DESC
``` 
