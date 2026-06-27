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
### 10: WHERE with IN
```sql
SELECT name,
       department
FROM employees
WHERE department IN ('Engineering', 'HR', 'Finance');
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

---

## ORDER BY

...

---

## TOP / LIMIT

'''

---
