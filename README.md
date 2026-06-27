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

...

---

## WHERE

...

---

## DISTINCT

...

---

## ORDER BY

...
