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
### Without DISTINCT
```sql
SELECT AVG(salary)
FROM employees;
```
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
# Part 2: Filtering & Operators
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

## Key Points
EXISTS is used only with subqueries.
It returns TRUE if the subquery returns one or more rows.
NOT EXISTS returns rows where the subquery returns no rows.
SELECT 1 and SELECT * behave the same inside an EXISTS subquery, but SELECT 1 is the preferred convention.
EXISTS is often more efficient than IN for large correlated subqueries because it stops searching as soon as it finds the first matching row.

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
```sql
SELECT departmentname
FROM "Departments" d
WHERE EXISTS (
    SELECT 1
    FROM employees e
    WHERE e.department = d.departmentname
)
ORDER BY departmentname;
```

## LIKE & Wildcards

The LIKE operator is used to search for a pattern in text (string) values.

It is commonly used with the WHERE clause to filter rows based on partial matches.

### Syntax:
```sql
SELECT column1, column2
FROM table_name
WHERE column_name LIKE 'pattern';
```
### Example 1: Starts With
```sql
SELECT name
FROM employees
WHERE name LIKE 'A%';
```
### Example 2: Ends With

```sql
SELECT name
FROM employees
WHERE name LIKE '%e';
```
Example 3: Contains
```sql
SELECT name
FROM employees
WHERE name LIKE '%ar%';
```
### One Character After A:
```sql
SELECT name
FROM employees
WHERE name LIKE 'A_';
```
Because _ matches exactly one character.

### Exactly Five Letters
```sql
SELECT name
FROM employees
WHERE name LIKE '_____';
```

### LIKE Wildcard Summary
>Pattern	Meaning	Example Match
>'A%'	Starts with A	Alice, Andrew
>'%e'	Ends with e	Alice, Charlie
>'%ar%'	Contains "ar"	Charlie
>'A_'	A + exactly one character	Al
>'_____'	Exactly 5 characters	Alice, David
>'__r%'	Third letter is r	Charlie

### Key Points
>LIKE is used for pattern matching in text columns.
>% matches zero or more characters.
>_ matches exactly one character.
>Use NOT LIKE to exclude matching patterns.
>LIKE is commonly used with WHERE, AND, OR, ORDER BY, and JOIN.
>Use = for exact matches and LIKE for pattern-based matches.


## ANY

The ANY operator is used to compare a value with any one of the values returned by a subquery.

A condition is TRUE if it matches at least one value returned by the subquery.

Note: ANY is always used with a comparison operator (=, >, <, >=, <=, <>) and a subquery.

### Key Points
>ANY is always used with a subquery.
>It works with comparison operators such as =, >, <, >=, <=, and <>.
>The condition is TRUE if at least one comparison succeeds.
>= ANY (subquery) is equivalent to IN (subquery).
>ANY is commonly used when comparing a value against a dynamic set of values returned by another query.

### Syntax:
```sql
SELECT column1, column2
FROM table_name
WHERE column_name comparison_operator ANY (
    subquery
);
```
### = ANY

```sql
SELECT name,
       department
FROM employees
WHERE department = ANY (
    SELECT departmentname
    FROM "Departments"
);
```
This is similar to:
```sql
SELECT name,
       department
FROM employees
WHERE department IN (
    SELECT departmentname
    FROM "Departments"
);
```

ANY: The condition must be true for at least one value returned by the subquery.
ALL: The condition must be true for every value returned by the subquery.

## Operators

### Arithmetic-Operators

### Key Points
>Arithmetic operators perform mathematical calculations on numeric data.
>They can be used in SELECT, WHERE, ORDER BY, HAVING, and aggregate functions.
>Parentheses () control the order of evaluation.
>Arithmetic operations involving NULL return NULL; use COALESCE() when appropriate.
>Integer division returns an integer result. Use decimal values or CAST() to get fractional results.

| Operator | Description         | Example         |
| -------- | ------------------- | --------------- |
| `+`      | Addition            | `salary + 5000` |
| `-`      | Subtraction         | `salary - 5000` |
| `*`      | Multiplication      | `salary * 12`   |
| `/`      | Division            | `salary / 2`    |
| `%`      | Modulus (Remainder) | `salary % 1000` |

### 1. Addition (+)
```sql
SELECT name,
       salary,
       salary + 5000 AS NewSalary
FROM employees;
```
### 2. Subtraction (-)

```sql
SELECT name,
       salary,
       salary - 2000 AS ReducedSalary
FROM employees;
```
### 3. Multiplication (*)
```sql
SELECT name,
       salary,
       salary * 12 AS AnnualSalary
FROM employees;
```
### 4. Division (/)
```sql
SELECT name,
       salary,
       salary / 2 AS HalfSalary
FROM employees;
```
### 5. Modulus (%)
```sql
SELECT name,
       salary,
       salary % 1000 AS Remainder
FROM employees;
```
## Comparison-Operators

>Comparison operators are used to compare two values.

>They are most commonly used in the WHERE clause to filter rows, but they can also be used in CASE, HAVING, and other SQL expressions.

| Operator     | Description              | Example              |
| ------------ | ------------------------ | -------------------- |
| `=`          | Equal to                 | `salary = 70000`     |
| `<>` or `!=` | Not equal to             | `department <> 'HR'` |
| `>`          | Greater than             | `salary > 80000`     |
| `<`          | Less than                | `salary < 50000`     |
| `>=`         | Greater than or equal to | `salary >= 70000`    |
| `<=`         | Less than or equal to    | `salary <= 60000`    |

>Note: PostgreSQL supports both <> and !=, but <> is the SQL standard.

### 1. Equal To (=)
```sql
SELECT name,
       department
FROM employees
WHERE department = 'Engineering';
```
### 2. Not Equal To (<>)
```sql
SELECT name,
       department
FROM employees
WHERE department <> 'HR';
```
Equivalent:
```sql
SELECT name,
       department
FROM employees
WHERE department != 'HR';
```
### 3. Greater Than (>)
```sql
SELECT name,
       salary
FROM employees
WHERE salary > 80000;
```
### 4. Less Than (<)
```sql
SELECT name,
       salary
FROM employees
WHERE salary < 50000;
```
### 5. Greater Than or Equal To (>=)
```sql
SELECT name,
       salary
FROM employees
WHERE salary >= 70000;
```
### 6. Less Than or Equal To (<=)
```sql
SELECT name,
       salary
FROM employees
WHERE salary <= 60000;
```
# Part 3: Functions
>String functions are built-in SQL functions used to manipulate, format, search, and analyze text values.

| Function       | Description                          | Example                           |
| -------------- | ------------------------------------ | --------------------------------- |
| `UPPER()`      | Convert to uppercase                 | `UPPER(name)`                     |
| `LOWER()`      | Convert to lowercase                 | `LOWER(name)`                     |
| `INITCAP()`    | Capitalize first letter of each word | `INITCAP(name)`                   |
| `LENGTH()`     | Returns string length                | `LENGTH(name)`                    |
| `CONCAT()`     | Concatenates strings                 | `CONCAT(name, ' - ', department)` |
| `\|\|`         | String concatenation operator        | `name \|\| ' - ' \|\| department` |
| `TRIM()`       | Removes leading and trailing spaces  | `TRIM(name)`                      |
| `LTRIM()`      | Removes left spaces                  | `LTRIM(name)`                     |
| `RTRIM()`      | Removes right spaces                 | `RTRIM(name)`                     |
| `SUBSTRING()`  | Extracts part of a string            | `SUBSTRING(name,1,3)`             |
| `LEFT()`       | Leftmost characters                  | `LEFT(name,3)`                    |
| `RIGHT()`      | Rightmost characters                 | `RIGHT(name,2)`                   |
| `POSITION()`   | Finds character position             | `POSITION('a' IN name)`           |
| `REPLACE()`    | Replaces text                        | `REPLACE(city,'York','Delhi')`    |
| `REVERSE()`    | Reverses string                      | `REVERSE(name)`                   |
| `LPAD()`       | Left padding                         | `LPAD(name,10,'*')`               |
| `RPAD()`       | Right padding                        | `RPAD(name,10,'*')`               |
| `SPLIT_PART()` | Splits text by delimiter             | `SPLIT_PART(email,'@',1)`         |
| `ASCII()`      | ASCII value of first character       | `ASCII(name)`                     |
| `CHR()`        | Character from ASCII code            | `CHR(65)`                         |


### 1. UPPER()
Converts text to uppercase.
```sql
SELECT name,
       UPPER(name) AS UpperName
FROM employees;
```
### 2. LOWER()
Converts text to lowercase.
```sql
SELECT name,
       LOWER(name) AS LowerName
FROM employees;
```
### 3. INITCAP()
Capitalizes the first letter of each word.
```sql
SELECT INITCAP('john smith');
```

### 4. LENGTH()
Returns the number of characters.
```sql
SELECT name,
       LENGTH(name) AS Characters
FROM employees;
```

### 5. CONCAT()
Combines multiple strings.
```sql
SELECT CONCAT(name,' - ',department) AS EmployeeInfo
FROM employees;
```
### 6. Concatenation Operator (||)
```sql
SELECT name || ' works in ' || department AS EmployeeInfo
FROM employees;
```
### 7. TRIM()
Removes spaces from both ends.
```sql
Removes spaces from both ends.
```
### 8. LTRIM()

Removes left spaces.
```sql
SELECT LTRIM('   Alice');
```
### 9. RTRIM()

Removes right spaces.
```sql
SELECT RTRIM('Alice   ');
```
### 10. SUBSTRING()

Extracts part of a string
```sql
SELECT name,
       SUBSTRING(name,1,3) AS FirstThreeLetters
FROM employees;
```
### 11. LEFT()

Returns leftmost characters.
```sql
SELECT LEFT(name,2)
FROM employees;
```
### 12. RIGHT()

Returns rightmost characters.
```sql
SELECT RIGHT(name,2)
FROM employees;
```
### 13. POSITION()

Finds the position of a substring.
```sql
SELECT POSITION('a' IN name)
FROM employees;
```
### 14. REPLACE()

Replace one string with another.

```sql
SELECT REPLACE(city,'New','Old')
FROM employees;
```
### 15. REVERSE()
```sql
SELECT REVERSE(name)
FROM employees;
```
### 16. LPAD()

Pads characters on the left.
```sql
SELECT LPAD(name,10,'*')
FROM employees;
```
### 17. RPAD()

Pads characters on the right.
```sql
SELECT RPAD(name,10,'*')
FROM employees;
```
### 18. SPLIT_PART()

Extracts a part of a delimited string.
```sql
SELECT SPLIT_PART('alice@gmail.com','@',1);
```
### 19. ASCII()

Returns the ASCII code of the first character.
```sql
SELECT ASCII('A');
```
### 20. CHR()

Returns a character from an ASCII code.
```sql
SELECT CHR(65);
```

# Date & Time Functions
>Date & Time Functions are built-in SQL functions used to retrieve, manipulate, format, calculate, and compare DATE, TIME, TIMESTAMP, and INTERVAL values.

| Function            | Description                             | Example                                                       |
| ------------------- | --------------------------------------- | ------------------------------------------------------------- |
| `CURRENT_DATE`      | Returns the current date                | `CURRENT_DATE`                                                |
| `CURRENT_TIME`      | Returns the current time                | `CURRENT_TIME`                                                |
| `CURRENT_TIMESTAMP` | Returns the current date and time       | `CURRENT_TIMESTAMP`                                           |
| `NOW()`             | Returns the current timestamp           | `NOW()`                                                       |
| `LOCALTIME`         | Returns the local time                  | `LOCALTIME`                                                   |
| `LOCALTIMESTAMP`    | Returns the local timestamp             | `LOCALTIMESTAMP`                                              |
| `AGE()`             | Calculates the difference between dates | `AGE(CURRENT_DATE, hiredate)`                                 |
| `EXTRACT()`         | Extracts a part of a date or time       | `EXTRACT(YEAR FROM hiredate)`                                 |
| `DATE_PART()`       | Returns a specific part of a date       | `DATE_PART('year', hiredate)`                                 |
| `DATE_TRUNC()`      | Truncates a date/time                   | `DATE_TRUNC('month', CURRENT_TIMESTAMP)`                      |
| `TO_CHAR()`         | Formats a date/time as text             | `TO_CHAR(hiredate,'DD-MM-YYYY')`                              |
| `TO_DATE()`         | Converts text to a date                 | `TO_DATE('25-12-2025','DD-MM-YYYY')`                          |
| `TO_TIMESTAMP()`    | Converts text to a timestamp            | `TO_TIMESTAMP('2025-12-25 10:30:00','YYYY-MM-DD HH24:MI:SS')` |
| `INTERVAL`          | Represents a duration of time           | `CURRENT_DATE + INTERVAL '10 days'`                           |
| `AT TIME ZONE`      | Converts timestamps between time zones  | `CURRENT_TIMESTAMP AT TIME ZONE 'UTC'`                        |


### CURRENT_DATE
>CURRENT_DATE is a built-in PostgreSQL function that returns today's current date according to the database server.

>It returns only the date.
>It does not include the time.
>It does not require parentheses.

```sql
SELECT CURRENT_DATE;
```

### 2. CURRENT_TIME

Returns the current time.
```sql
SELECT CURRENT_TIME;
```
### 3. CURRENT_TIMESTAMP

Returns the current date and time.
```sql
SELECT CURRENT_TIMESTAMP;
```
### 4. NOW()

Returns the current timestamp with the session time zone.
```sql
SELECT NOW();
```
### 5. LOCALTIME

Returns the current local time (without time zone).
```sql
SELECT LOCALTIME;
```
### 6. LOCALTIMESTAMP

Returns the current local date and time (without time zone).
```sql
SELECT LOCALTIMESTAMP;
```
### 7. AGE()

Calculates the difference between two dates.
```sql
SELECT name,
       AGE(CURRENT_DATE, hiredate) AS experience
FROM employees;
```
### 8. EXTRACT()

>Extracts a specific part of a date or timestamp.
#### Extract the hire year.
```sql
SELECT name,
       EXTRACT(YEAR FROM hiredate) AS hire_year
FROM employees;
```
#### Extract the current month.
```sql
SELECT EXTRACT(MONTH FROM CURRENT_DATE);
```
#### Extract the current day.
```sql
Extract the current day.
```
#### Extract the current hour.
```sql
SELECT EXTRACT(HOUR FROM CURRENT_TIMESTAMP);
```
### 9. DATE_PART()
>Returns a specific part of a date or timestamp.
#### Extract the hire year.
```sql
SELECT name,
       DATE_PART('year', hiredate) AS hire_year
FROM employees;
```
#### Extract the current month.
```sql
SELECT DATE_PART('month', CURRENT_DATE);
```

### 10. DATE_TRUNC()
>Truncates a date or timestamp to a specified precision.
Beginning of the current month.
```sql
SELECT DATE_TRUNC('month', CURRENT_TIMESTAMP);
```
Beginning of the current year.
```sql
SELECT DATE_TRUNC('year', CURRENT_TIMESTAMP);
```
Beginning of the current day.
```sql
SELECT DATE_TRUNC('day', CURRENT_TIMESTAMP);
```
### 11. TO_CHAR()

>Formats a date or timestamp as text.
```sql
SELECT TO_CHAR(CURRENT_DATE, 'DD-MM-YYYY');
```
Format employee hire dates.
```sql
SELECT name,
       TO_CHAR(hiredate, 'DD Mon YYYY')
FROM employees;
```
Format timestamp.
```sql
SELECT TO_CHAR(CURRENT_TIMESTAMP,
               'DD-MM-YYYY HH24:MI:SS');
```
### 12. TO_DATE()

>Converts a string into a DATE value.

```sql
SELECT TO_DATE('25-12-2025', 'DD-MM-YYYY');
```

```sql
SELECT TO_DATE('2025/12/25',
               'YYYY/MM/DD');
```
### 13. TO_TIMESTAMP()

Converts a string into a TIMESTAMP.

```sql
SELECT TO_TIMESTAMP(
'2025-12-25 10:30:00',
'YYYY-MM-DD HH24:MI:SS'
);
```
### 14. INTERVAL

>Represents a duration of time.

Add 10 days.
```sql
SELECT CURRENT_DATE + INTERVAL '10 days';
```
Subtract 2 months.
```sql
SELECT CURRENT_DATE - INTERVAL '2 months';
```
Employee's first work anniversary.
```sql
SELECT name,
       hiredate + INTERVAL '1 year'
FROM employees;
```
### 15. AT TIME ZONE

>Converts timestamps between time zones.

>Convert the current timestamp to UTC.
```sql
SELECT CURRENT_TIMESTAMP
AT TIME ZONE 'UTC';
```
Convert the current timestamp to India Standard Time.
```sql
SELECT CURRENT_TIMESTAMP
AT TIME ZONE 'Asia/Kolkata';
```
## Numeric Functions
>Numeric functions are built-in SQL functions used to perform mathematical calculations, rounding, absolute values, powers, square roots, random number generation, >logarithms, and other numeric operations.

| Function               | Description                                       | Example                    |
| ---------------------- | ------------------------------------------------- | -------------------------- |
| `ABS()`                | Returns the absolute (positive) value             | `ABS(-25)`                 |
| `CEIL()` / `CEILING()` | Rounds up to the nearest integer                  | `CEIL(12.3)`               |
| `FLOOR()`              | Rounds down to the nearest integer                | `FLOOR(12.9)`              |
| `ROUND()`              | Rounds a number                                   | `ROUND(12.567,2)`          |
| `TRUNC()`              | Removes decimal places without rounding           | `TRUNC(12.987,2)`          |
| `MOD()`                | Returns the remainder                             | `MOD(10,3)`                |
| `POWER()`              | Raises a number to a power                        | `POWER(2,5)`               |
| `SQRT()`               | Returns the square root                           | `SQRT(64)`                 |
| `CBRT()`               | Returns the cube root                             | `CBRT(27)`                 |
| `RANDOM()`             | Returns a random number between 0 and 1           | `RANDOM()`                 |
| `SIGN()`               | Returns the sign of a number                      | `SIGN(-15)`                |
| `PI()`                 | Returns the value of π                            | `PI()`                     |
| `EXP()`                | Returns e raised to a power                       | `EXP(2)`                   |
| `LN()`                 | Returns the natural logarithm                     | `LN(10)`                   |
| `LOG()`                | Returns the logarithm (base 10 or specified base) | `LOG(100)`                 |
| `LOG(base, value)`     | Returns logarithm with a specified base           | `LOG(2,8)`                 |
| `GREATEST()`           | Returns the largest value                         | `GREATEST(10,20,30)`       |
| `LEAST()`              | Returns the smallest value                        | `LEAST(10,20,30)`          |
| `WIDTH_BUCKET()`       | Places a value into a histogram bucket            | `WIDTH_BUCKET(65,0,100,5)` |

### 1. ABS()

Returns the absolute (positive) value of a number.
```sql
SELECT ABS(-250);
```
### 2. CEIL() / CEILING()

Rounds a number up to the nearest integer.
```sql
SELECT CEIL(25.2);
```
3. FLOOR()

Rounds a number down to the nearest integer.
```sql
SELECT FLOOR(25.9);
```
### 4. ROUND()

Rounds a number to the specified decimal places.
```sql
SELECT ROUND(25.6789);
```
Round to 2 decimal places.
```sql
SELECT ROUND(25.6789,2);
```
Round employee salary after dividing by 12.
```sql
SELECT name,
       ROUND(salary/12.0,2) AS monthly_salary
FROM employees;
```
### 5. TRUNC()

Removes decimal places without rounding.
```sql
SELECT TRUNC(25.9876);
```
Keep two decimal places.
```sql
SELECT TRUNC(25.9876,2);
```
### 6. MOD()

Returns the remainder after division.
```sql
SELECT MOD(15,4);
```
Determine whether employee IDs are even or odd.
```sql
SELECT employeesid,
       MOD(employeesid,2) AS remainder
FROM employees;
```
### 7. POWER()

Raises a number to the specified power.

```sql
SELECT POWER(2,5);
```
Calculate salary squared.
```
SELECT name,
       POWER(salary,2)
FROM employees;
```
### 8. SQRT()

Returns the square root.
```sql
SELECT SQRT(81);
```
### 9. CBRT()

Returns the cube root.
```sql
SELECT CBRT(125);
```
### 10. RANDOM()

Returns a random number between 0 and 1.
```sql
SELECT RANDOM();
```
### 11. SIGN()

Returns the sign of a number.

1 → Positive
0 → Zero
-1 → Negative

```sql
SELECT SIGN(-250);
```
```sql
SELECT SIGN(0);
```
```sql
SELECT SIGN(250);
```


### 12. PI()

Returns the value of π (3.141592653589793).
```sql
SELECT PI();
```

```sql
SELECT PI() * POWER(10,2) AS area;
```
### 13. EXP()

Returns e raised to the specified power.
```sql
SELECT EXP(2);
```
### 14. LN()

Returns the natural logarithm.
```sql
SELECT LN(100);
```
### 15. LOG()

Returns the logarithm.
```sql
SELECT LOG(1000);
```
### 16. GREATEST()

Returns the largest value.

```sql
SELECT GREATEST(50,80,65,90);
```
```sql
SELECT e.name,
       GREATEST(e.salary,d.budget)
FROM employees e
JOIN "Departments" d
ON e.department=d.departmentname;
```
### 17. LEAST()

Returns the smallest value.
```sql
SELECT LEAST(50,80,65,90);
```
```sql
SELECT e.name,
       LEAST(e.salary,d.budget)
FROM employees e
JOIN "Departments" d
ON e.department=d.departmentname;
```
### 18. WIDTH_BUCKET()

Assigns a value to a bucket (histogram).

```sql
SELECT WIDTH_BUCKET(75,0,100,5);
```
```SELECT name,
       salary,
       WIDTH_BUCKET(salary,30000,100000,5) AS salary_bucket
FROM employees;
```
