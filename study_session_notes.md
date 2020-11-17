* Areas To Work On 
* Constraints
- Foreign Key references Primary Key
- The constraint means the that the table it is referencing must have the value exist for it to be added.
- You must first remove the foreign key constraint to be able to drop the table it is referencing. 
- To escape keywords you need to use quotation marks. 
- `string_agg` to concatanate the items in the group by clause. Uses two arguments.
-  If you use a aggregate function in the SELECT clause you must reference any other columns in the SELECT clause in the GROUP BY clause.

```SQL
employees                             projects
+---------------+---------+           +---------------+---------+
| id            | int     |<----+  +->| id            | int     |
| first_name    | varchar |     |  |  | title         | varchar |
| last_name     | varchar |     |  |  | start_date    | date    |
| salary        | int     |     |  |  | end_date      | date    |
| department_id | int     |--+  |  |  | budget        | int     |
+---------------+---------+  |  |  |  +---------------+---------+
                             |  |  |
departments                  |  |  |  employees_projects
+---------------+---------+  |  |  |  +---------------+---------+
| id            | int     |<-+  |  +--| project_id    | int     |
| name          | varchar |     +-----| employee_id   | int     |
+---------------+---------+           +---------------+---------+


-- SELECT e.first_name, e.last_name, e.salary,
--   d.name as department_name
-- FROM employees   AS e
-- JOIN departments AS d ON e.department_id = d.id;


/*

employee name | all projects
_____________________________
   Richard     |  Database Design, Deploy Web App
   
 */

-- Richard:
SELECT employees.first_name as "employee name", string_agg(projects.title, ', ') AS "all projects"
FROM employees
INNER JOIN employees_projects
ON employees.id = employees_projects.employee_id
INNER JOIN projects
ON employees_projects.project_id = projects.id
GROUP BY employees.first_name; 



-- SELECT employees.first_name, String_AGG(projects.title, ',') FROM employees
-- JOIN employees_projects 
-- ON employees_projects.employee_id = employees.id
-- JOIN projects 
-- ON projects.id = employees_projects.project_id
-- GROUP BY employees.first_name;



-- -- Erik
-- SELECT e.first_name AS employee_name, String_AGG(proj.title, ', ') AS all_projects
-- FROM employees AS e 
-- INNER JOIN employees_projects AS ep 
-- ON e.id = ep.employee_id
-- INNER JOIN projects AS proj
-- ON proj.id = ep.project_id
-- GROUP BY e.first_name;
```