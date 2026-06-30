# 📚 SQL Learning Roadmap

## 📑 Table of Contents

### Part 1: SQL Basics
- [Logical Execution Order](#SQL_Process_in_Order)
- [SELECT](#select)
- [FROM](#from)
- [WHERE](#where)
- [DISTINCT](#distinct)
- [ORDER BY](#order-by)
- [TOP / LIMIT](#top--limit)
- [Aliases](#aliases)
- [Comments](#comments)

### Part 2: Filtering & Operators
- [AND](#and)
- [OR](#or)
- [NOT](#not)
- [IN](#in)
- [BETWEEN](#between)
- [LIKE](#like)
- [IS NULL](#is-null)
- [EXISTS](#exists)
- [ANY](#any)
- [ALL](#all)
- [Arithmetic Operators](#arithmetic-operators)
- [Comparison Operators](#comparison-operators)
- [Bitwise Operators](#bitwise-operators)

### Part 3: Functions
- [String Functions](#string-functions)
- [Date & Time Functions](#date--time-functions)
- [Numeric Functions](#numeric-functions)

### Part 4: Aggregate & GROUP BY
- [COUNT](#count)
- [SUM](#sum)
- [AVG](#avg)
- [MIN](#min)
- [MAX](#max)
- [GROUP BY](#group-by)
- [HAVING](#having)
- [ROLLUP](#rollup)
- [CUBE](#cube)
- [GROUPING SETS](#grouping-sets)

### Part 5: Joins & Subqueries
- [INNER JOIN](#inner-join)
- [LEFT JOIN](#left-join)
- [RIGHT JOIN](#right-join)
- [FULL JOIN](#full-join)
- [CROSS JOIN](#cross-join)
- [SELF JOIN](#self-join)
- [Scalar Subquery](#scalar-subquery)
- [Correlated Subquery](#correlated-subquery)
- [Nested Subquery](#nested-subquery)
- [EXISTS / NOT EXISTS](#exists--not-exists)

### Part 6: Set Operators & CASE
- [UNION](#union)
- [UNION ALL](#union-all)
- [INTERSECT](#intersect)
- [EXCEPT](#except)
- [CASE](#case)

### Part 7: CTE & Window Functions
- [CTE](#cte)
- [Recursive CTE](#recursive-cte)
- [ROW_NUMBER](#row_number)
- [RANK](#rank)
- [DENSE_RANK](#dense_rank)
- [NTILE](#ntile)
- [LEAD](#lead)
- [LAG](#lag)
- [FIRST_VALUE](#first_value)
- [LAST_VALUE](#last_value)
- [Window Frame Clauses](#window-frame-clauses)

### Part 8: Pivot & Temp Objects
- [PIVOT](#pivot)
- [UNPIVOT](#unpivot)
- [Temporary Tables](#temporary-tables)
- [Table Variables](#table-variables)

### Part 9: Views, Indexes & Constraints
- [Views](#views)
- [Indexes](#indexes)
- [Constraints](#constraints)

### Part 10: DDL, DML, TCL & DCL
- [DDL](#ddl)
- [DML](#dml)
- [TCL](#tcl)
- [DCL](#dcl)

### Part 11: Stored Procedures & Triggers
- [Stored Procedures](#stored-procedures)
- [Functions](#functions)
- [Triggers](#triggers)

### Part 12: Transactions & Performance
- [Transactions](#transactions)
- [Dynamic SQL](#dynamic-sql)
- [Execution Plans](#execution-plans)
- [Query Optimization](#query-optimization)

### Part 13: Advanced SQL
- [Recursive Queries](#recursive-queries)
- [Hierarchical Data](#hierarchical-data)
- [Gaps & Islands](#gaps--islands)
- [Running Totals](#running-totals)
- [Rolling Average](#rolling-average)
- [Median](#median)
- [Percentile](#percentile)
- [XML / JSON Functions](#xml--json-functions)
- [Temporal Tables](#temporal-tables)

---

# Part 1: SQL Basics

### SQL_Process_in_Order
```sql
> FROM employees
> WHERE salary > 60000
> GROUP BY (if present)
> HAVING (if present)
> SELECT
> DISTINCT (if present)
> ORDER BY salary DESC
> LIMIT / OFFSET
```
---
## SELECT

> The `SELECT` statement retrieves data from one or more database tables.

### Syntax

```sql
SELECT column1, column2, ...
FROM table_name;
```

### 1. Select all columns

```sql
SELECT *
FROM employees;
```

### 2. Select specific columns

```sql
SELECT name, salary
FROM employees;
```

### 3. Select with a condition

```sql
SELECT name, salary
FROM employees
WHERE salary > 70000;
```

### 4. Select distinct values

```sql
SELECT DISTINCT department
FROM employees;
```

### 5. Select with sorting

```sql
SELECT name, salary
FROM employees
ORDER BY salary DESC;
```

---

## FROM
>The FROM clause specifies which table (or tables) SQL should retrieve data from.
...
### Syntax
```sql
SELECT column1, column2, ...
FROM table_name;
```

> SELECT → Chooses the columns to display.
> FROM → Specifies the table containing the data.

### 1.FROM with a Single Table
 ```sql

SELECT *
FROM Employees;
```
### 2. Select specific columns
```sql
SELECT Name, Salary
FROM Employees;
```
### 3. FROM with WHERE
```sql
SELECT name, department, salary
FROM employees
WHERE salary > 60000;

```
### 4.FROM with Table Alias
```sql
SELECT e.name,
       e.department,
       e.salary
FROM employees AS e;
```
or 
```sql
SELECT e.name,
       e.department,
       e.salary
FROM employees e;
```

>Here, e is an alias (short name) for the Employees table.

### 5.FROM with JOIN
```sql
SELECT e.name,
       e.department,
       d.budget
FROM employees e
JOIN "Departments" d
ON e.department = d.departmentname;
```
> This works but is not recommended. Always use explicit JOIN syntax.

### 6. FROM with Multiple Tables

```sql
SELECT e.name,
       d.departmentname,
       d.budget
FROM employees e,
     "Departments" d
WHERE e.department = d.departmentname;
```

### 7. FROM with a Subquery
```sql
SELECT name,
       salary
FROM
(
    SELECT name,
           salary
    FROM employees
    WHERE salary > 70000
) AS HighSalaryEmployees;
```

### 8. FROM with a Common Table Expression (CTE)
```sql
WITH HighSalaryEmployees AS
(
    SELECT *
    FROM employees
    WHERE salary > 70000
)
SELECT name,
       salary,
       department
FROM HighSalaryEmployees;
```
### 9. FROM with Self Join (Employee → Manager)
```sql
SELECT e.name AS Employee,
       m.name AS Manager
FROM employees e
LEFT JOIN employees m
ON e.managerid = m.employeesid;
```
### 10. FROM with Multiple JOINs
```sql
SELECT e.name,
       d.departmentname,
       d.budget,
       m.name AS Manager
FROM employees e
JOIN "Departments" d
ON e.department = d.departmentname
LEFT JOIN employees m
ON e.managerid = m.employeesid;
```
### 11. FROM with ORDER BY
```sql
SELECT name,
       salary
FROM employees
ORDER BY salary DESC;
```
### 12. FROM with LIMIT
```sql
SELECT *
FROM employees
LIMIT 5;
```
### 13. FROM with DISTINCT
```sql
SELECT DISTINCT department
FROM employees;
```
### 14. FROM with Aggregate Function
```sql
SELECT department,
       COUNT(*) AS TotalEmployees
FROM employees
GROUP BY department;
```
### 15. FROM with Aggregate and HAVING
```sql
SELECT department,
       AVG(salary) AS AverageSalary
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```
---

## WHERE
>The WHERE clause is used to filter rows from a table. It returns only those rows that satisfy a specified condition.
...
### Syntax
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

### 1: Simple WHERE
>Retrieve employees from the Engineering department.

```sql
SELECT *
FROM employees
WHERE department = 'Engineering';
```
### 2: WHERE with Numeric Value
```sql
SELECT name, salary
FROM employees
WHERE salary > 70000;
```
### 3: WHERE with Less Than
```sql
SELECT name, salary
FROM employees
WHERE salary < 60000;
```
### 4: WHERE with Equal (=)
```sql
SELECT *
FROM employees
WHERE city = 'New York';
```
### 5: WHERE with Not Equal
```sql
SELECT *
FROM employees
WHERE department <> 'HR';
```
or
```sql
SELECT *
FROM employees
WHERE department != 'HR';
```
### 6: WHERE with AND
```sql
SELECT name,
       department,
       salary
FROM employees
WHERE department = 'Engineering'
AND salary > 80000;
```
### 7: WHERE with OR
```sql
SELECT *
FROM employees
WHERE department = 'HR'
OR department = 'Finance';
```
### 8: WHERE with NOT
```sql
SELECT *
FROM employees
WHERE NOT department = 'Marketing';
```
### 9: WHERE with BETWEEN
```sql
SELECT name,
       salary
FROM employees
WHERE salary BETWEEN 60000 AND 90000;
```
>Equivalent to:
```sql
WHERE salary >= 60000
AND salary <= 90000;
```

### 10: WHERE with IN
```sql
SELECT name,
       department
FROM employees
WHERE department IN ('Engineering', 'HR', 'Finance');
```
>Equivalent to:
```sql
WHERE department='Engineering'
OR department='HR'
OR department='Finance';
```
### 11: WHERE with NOT IN
```sql
SELECT *
FROM employees
WHERE department NOT IN ('HR', 'Marketing');
```
### 12: WHERE with LIKE
```sql
SELECT *
FROM employees
WHERE name LIKE 'A%';
```
> Names ending with 'n'.
```sql
SELECT *
FROM employees
WHERE name LIKE '%n';
```
>Names containing 'ar'.
```sql
SELECT *
FROM employees
WHERE name LIKE '%ar%';
```
>Exactly five characters.
```sql
---(_ represents one character.)
SELECT *
FROM employees
WHERE name LIKE '_____';
```
### 13: WHERE with IS NULL
```sql
SELECT *
FROM employees
WHERE managerid IS NULL;
```
### 14: WHERE with IS NOT NULL
```sql
SELECT *
FROM employees
WHERE managerid IS NOT NULL;
```
### 15: WHERE with Dates
```sql
SELECT name,
       hiredate
FROM employees
WHERE hiredate > '2022-01-01';
```
### 16: WHERE with Multiple Conditions
```sql
SELECT *
FROM employees
WHERE department='Engineering'
AND city='New York'
AND salary > 70000;
```

### 17: WHERE with Parentheses
```sql
SELECT *
FROM employees
WHERE (department='Engineering'
       OR department='HR')
AND salary > 60000;
```
### 18: WHERE with JOIN
```sql
SELECT e.name,
       e.department,
       d.budget
FROM employees e
JOIN "Departments" d
ON e.department = d.departmentname
WHERE e.department = 'Engineering';
```
### 19: WHERE with Aggregate (Incorrect)
```sql
SELECT department,
       AVG(salary)
FROM employees
WHERE AVG(salary) > 70000
GROUP BY department;
```
>Aggregate functions cannot be used in the WHERE clause.

### 20: Use HAVING Instead
```sql
SELECT department,
       AVG(salary) AS AverageSalary
FROM employees
GROUP BY department
HAVING AVG(salary) > 70000;
```
---

## DISTINCT
...
>The DISTINCT clause is used to remove duplicate rows from the result set. It returns only unique values.

### Syntax
```sql
SELECT DISTINCT column_name
FROM table_name;
```
>or 
```sql
SELECT DISTINCT column1, column2
FROM table_name;
```
### 1: DISTINCT on One Column

```sql
SELECT DISTINCT department
FROM employees;
```
### 2: Without DISTINCT
```sql
SELECT department
FROM employees;
```
### 3: DISTINCT on Multiple Columns
```sql
SELECT DISTINCT department, city
FROM employees;
```
### 4: DISTINCT with ORDER BY
```sql
SELECT DISTINCT department
FROM employees
ORDER BY department;
```
### 5: DISTINCT with WHERE
```sql
SELECT DISTINCT city
FROM employees
WHERE department = 'Engineering';
```
### 6: DISTINCT with JOIN
```sql
SELECT DISTINCT
       d.departmentname,
       d.budget
FROM employees e
JOIN "Departments" d
ON e.department = d.departmentname;
```
### 7: DISTINCT with COUNT
```sql
SELECT COUNT(DISTINCT department)
FROM employees;
```
### 8: DISTINCT with Aggregate
```sql
SELECT AVG(DISTINCT salary)
FROM employees;
```
Without DISTINCT

SELECT AVG(salary)
FROM employees;

Average:

(50000 + 50000 + 60000 + 70000) / 4
= 57,500
### 9: DISTINCT with LIMIT
```sql
SELECT DISTINCT city
FROM employees
LIMIT 3;
```
### 10: DISTINCT with GROUP BY
```sql
SELECT DISTINCT department
FROM employees
GROUP BY department;
```
---

## ORDER BY

...
The ORDER BY clause is used to sort the result set in ascending (ASC) or descending (DESC) order.

ASC (Ascending) is the default order.
DESC (Descending) sorts in reverse order.
### Syntax
```sql
SELECT column1, column2
FROM table_name
ORDER BY column_name ASC;
```
### 1: ORDER BY (Ascending)
```sql
SELECT name, salary
FROM employees
ORDER BY salary;
```
### 2: ORDER BY DESC
```sql
SELECT name, salary
FROM employees
ORDER BY salary DESC;
```
### 3: ORDER BY Text Column

Sort employees alphabetically by name.
```sql
SELECT name, department
FROM employees
ORDER BY name;
```
### 4: ORDER BY Multiple Columns

Sort first by department, then by salary.
```sql
SELECT name,
       department,
       salary
FROM employees
ORDER BY department, salary;
```
### 5: Different Sort Orders

Sort department in ascending order and salary in descending order.
```sql
SELECT name,
       department,
       salary
FROM employees
ORDER BY department ASC,
         salary DESC;
```
### 8: ORDER BY with JOIN
```sql
SELECT e.name,
       e.department,
       d.budget
FROM employees e
JOIN "Departments" d
ON e.department = d.departmentname
ORDER BY d.budget DESC;
```
### 9: ORDER BY Using Column Position
```sql
SELECT name,
       salary,
       department
FROM employees
ORDER BY 2 DESC;
```
### 10:ORDER BY with Aggregate Function
```sql
SELECT department,
       AVG(salary) AS AverageSalary
FROM employees
GROUP BY department
ORDER BY AverageSalary DESC;
```
### 11: ORDER BY with NULL Values
```sql
SELECT name,
       managerid
FROM employees
ORDER BY managerid;
```
By default in PostgreSQL:

ASC → NULL values appear last.
DESC → NULL values appear first.


---

## TOP / LIMIT

'''
TOP and LIMIT are used to restrict the number of rows returned by a query.

> LIMIT → Used in PostgreSQL, MySQL, and SQLite.
> TOP → Used in SQL Server.
> Since you're using PostgreSQL, you'll use LIMIT.

### Syntax
#### PostgreSQL

```sql
SELECT column1, column2
FROM table_name
LIMIT number;
```
#### SQL Server
```sql
SELECT TOP number column1, column2
FROM table_name;
```
### 1: LIMIT
```sql
SELECT *
FROM employees
LIMIT 5;
```
### 2: LIMIT with OFFSET
Skip the first 5 employees and return the next 5.
```sql
SELECT *
FROM employees
LIMIT 5
OFFSET 5;
```
---
## ALIASES
>An Alias is a temporary name given to a column or a table in a SQL query. It makes query results easier to read and SQL statements shorter.
'''
### Syntax
```sql
SELECT column_name AS alias_name
FROM table_name;
```
### 1: Column Alias
```sql
SELECT name,
       salary AS EmployeeSalary
FROM employees;
```
### 2: Column Alias Without AS
```sql
SELECT name,
       salary EmployeeSalary
FROM employees;
```
### 3: Multiple Column Aliases
```sql
SELECT employeesid AS EmployeeID,
       name AS EmployeeName,
       salary AS MonthlySalary
FROM employees;
```
### 4: Table Alias
```sql
SELECT e.name,
       e.department,
       e.salary
FROM employees AS e;
```
### 5: Alias with WHERE
```sql
SELECT e.name,
       e.salary
FROM employees e
WHERE e.salary > 70000;
```
### 6: Alias with ORDER BY
```sql
SELECT name,
       salary AS EmployeeSalary
FROM employees
ORDER BY EmployeeSalary DESC;
```
### 7: Alias with Aggregate Function
```sql
SELECT department,
       AVG(salary) AS AverageSalary
FROM employees
GROUP BY department;
```
### 8: Alias with HAVING
```sql
SELECT department,
       AVG(salary) AS AverageSalary
FROM employees
GROUP BY department
HAVING AVG(salary) > 70000;
```
### 9: Alias with JOIN
```sql
SELECT e.name,
       d.departmentname,
       d.budget
FROM employees e
JOIN "Departments" d
ON e.department = d.departmentname;
```
Explanation
e → Alias for employees
d → Alias for "Departments"

### 10: Alias with CONCAT
```sql
SELECT name || ' - ' || department AS EmployeeDetails
FROM employees;
```
### 11: Alias with COUNT
```sql
SELECT department,
       COUNT(*) AS TotalEmployees
FROM employees
GROUP BY department;
```
### 12: Alias with CASE
```sql
SELECT name,
       salary,
       CASE
           WHEN salary >= 80000 THEN 'High Salary'
           ELSE 'Normal Salary'
       END AS SalaryCategory
FROM employees;
```
---
## COMMENTS

> Comments are used to add notes or explanations to SQL code. They are ignored by the SQL engine and are only for humans reading the query.

### Types of Comments

There are two types of comments in SQL:
> Single-line Comment (--)
> Multi-line Comment (/* ... */)

### 1: Single-Line Comment
```sql
-- Display all employees
SELECT *
FROM employees;
```
### 2: Comment Above a Query
```sql
-- Display employees earning more than ₹70,000
SELECT name,
       salary
FROM employees
WHERE salary > 70000;
```
### 3: Inline Comment
```sql
SELECT name,
       salary -- Monthly salary
FROM employees;
```
 ## Part 2: Filtering & Operators
 ---
### AND
>The AND operator is used to combine two or more conditions in the WHERE clause.
>A row is returned only if all conditions are TRUE.

Syntax
```sql
SELECT column1, column2
FROM table_name
WHERE condition1
AND condition2;
```
### And WIth Conditions
```sql
SELECT name,
       department,
       salary
FROM employees
WHERE department = 'Engineering'
AND salary > 70000;
```
### AND with BETWEEN
```sql
SELECT name,
       department,
       salary
FROM employees
WHERE department = 'HR'
AND salary BETWEEN 50000 AND 80000;
```
## OR
>The OR operator is used to combine two or more conditions in the WHERE clause.
>A row is returned if at least one condition is TRUE.

### Syntax:
```sql
SELECT column1, column2
FROM table_name
WHERE condition1
OR condition2;
```
### OR with Two Conditions
```sql
SELECT name,
       department
FROM employees
WHERE department = 'Engineering'
OR department = 'HR';
```
## NOT
>The NOT operator is used to reverse (negate) a condition.
>If a condition is TRUE, NOT makes it FALSE.
>If a condition is FALSE, NOT makes it TRUE.

It is commonly used with WHERE to exclude rows that match a condition.

### Syntax:
```sql
SELECT column1, column2
FROM table_name
WHERE NOT condition;
```
### NOT with Equal (=)
```sql
SELECT name,
       department
FROM employees
WHERE NOT department = 'HR';
```
### NOT with BETWEEN
```sql
SELECT name,
       salary
FROM employees
WHERE salary NOT BETWEEN 50000 AND 80000;
```
### NOT with IN
```sql
SELECT name,
       department
FROM employees
WHERE department NOT IN ('Engineering', 'HR');
```

Equivalent to:
```sql
SELECT name,
       department
FROM employees
WHERE department <> 'Engineering'
AND department <> 'HR';
```
## IN
>The IN operator is used to check whether a value matches any value in a list.
>Instead of writing multiple OR conditions, you can use IN.

### Syntax
```sql
SELECT column1, column2
FROM table_name
WHERE column_name IN (value1, value2, value3, ...);
```
### Example 1:
```
SELECT name,
       department
FROM employees
WHERE department IN ('Engineering', 'HR', 'Finance');
```
### Example 2:
```sql
SELECT name,
       department
FROM employees
WHERE department = 'Engineering'
   OR department = 'HR'
   OR department = 'Finance';
```
### Example 3:
```sql
SELECT e.name,
       e.department,
       d.budget
FROM employees e
JOIN "Departments" d
ON e.department = d.departmentname
WHERE d.budget IN (200000, 500000);
```
## BETWEEN
>The BETWEEN operator is used to filter values within a specified range.
>It includes both the starting and ending values.

### Syntax
```sql
SELECT column1, column2
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```
Example 1:
```sql
SELECT name,
       salary
FROM employees
WHERE salary BETWEEN 50000 AND 80000;
```

Example 2:
```sql
SELECT name,
       hiredate
FROM employees
WHERE hiredate BETWEEN '2023-01-01' AND '2023-12-31';
```
```sql
SELECT name,
       salary
FROM employees
WHERE salary NOT BETWEEN 50000 AND 80000;
```

## IS NULL /IS NOT NULL
>In SQL, NULL represents a missing, unknown, or undefined value.

>Important: NULL is not the same as:

> "0 (zero)"
> '' (empty string)
>  "FALSE"

To check for NULL values, use:

IS NULL
IS NOT NULL

Note: You cannot use = or != with NULL.

## Syntax:

### IS NULL
```sql
SELECT column1, column2
FROM table_name
WHERE column_name IS NULL;
```
### IS NOT NULL
```sql
SELECT column1, column2
FROM table_name
WHERE column_name IS NOT NULL;
```

Example 1:
```sql
SELECT name,
       managerid
FROM employees
WHERE managerid IS NULL;
```
Example 2:
```sql
SELECT name,
       managerid
FROM employees
WHERE managerid IS NOT NULL;
```
## EXISTS

>The EXISTS operator is used to check whether a subquery returns any rows.
If the subquery returns one or more rows, EXISTS returns TRUE.
If the subquery returns no rows, EXISTS returns FALSE.

Note: EXISTS is always used with a subquery.

### Syntax:
```sql
SELECT column1, column2
FROM table_name
WHERE EXISTS (
    subquery
);
```
### Example 1: Basic EXISTS
```sql
SELECT departmentname
FROM "Departments" d
WHERE EXISTS (
    SELECT 1
    FROM employees e
    WHERE e.department = d.departmentname
);
```
>For each department:If at least one employee belongs to that department → Return the department.
>Otherwise → Skip it.

### Example 2: EXISTS with Salary
```sql
SELECT departmentname
FROM "Departments" d
WHERE EXISTS (
    SELECT 1
    FROM employees e
    WHERE e.department = d.departmentname
      AND e.salary > 80000
);
```
