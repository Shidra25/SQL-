# 📚 SQL Learning Roadmap

## 📑 Table of Contents

### Part 1: SQL Basics
- [SELECT](#select)
- [FROM](#from)
- [WHERE](#where)
- [DISTINCT](#distinct)
- [ORDER BY](#order-by)
- [TOP / LIMIT](#top--limit)
- [Aliases](#aliases)
- [Comments](#comments)
- [Execution Order](#SQl--Logically--Process)

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

### 1. Select all columns
 ```sql

SELECT *
FROM Employees;
```
### 2. Select specific columns
```sql
SELECT Name, Salary
FROM Employees;
```
### 3. Using FROM with WHERE
```sql
SELECT Name, Department
FROM Employees
WHERE Salary > 55000;

```
### 4. Using Table Alias
```sql
SELECT e.Name, e.Salary
FROM Employees AS e;
```
>Here, e is an alias (short name) for the Employees table.

### 5. Multiple Tables (JOIN)
```sql
SELECT e.Name, d.DepartmentName
FROM Employees e
JOIN Departments d
ON e.DepartmentID = d.DepartmentID;
```
> This works but is not recommended. Always use explicit JOIN syntax.

### 6. Multiple Tables (JOIN)

```sql
SELECT e.Name, d.DepartmentName
FROM Employees e, Departments d
WHERE e.DepartmentID = d.DepartmentID;
```

### 7. FROM with a Subquery
```sql
SELECT Name, Salary
FROM (
    SELECT Name, Salary
    FROM Employees
    WHERE Department = 'IT'
) AS IT_Employees;
```

### 8. FROM with a Common Table Expression (CTE)
```sql
WITH HighSalary AS (
    SELECT *
    FROM Employees
    WHERE Salary > 60000
)
SELECT Name, Salary
FROM HighSalary;
```
### 9. FROM with Multiple Joins
```sql
SELECT e.Name,
       d.DepartmentName,
       m.Name AS Manager
FROM Employees e
JOIN Departments d
    ON e.DepartmentID = d.DepartmentID
JOIN Employees m
    ON e.ManagerID = m.EmployeeID;
```
---

## WHERE

...

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
