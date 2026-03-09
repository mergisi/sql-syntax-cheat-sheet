# SQL Syntax Cheat Sheet

[![Stars](https://img.shields.io/github/stars/mergisi/sql-syntax-cheat-sheet?style=social)](https://github.com/mergisi/sql-syntax-cheat-sheet)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> A comprehensive SQL syntax reference covering commands, functions, operators, and concepts across MySQL, PostgreSQL, SQL Server, SQLite, and Oracle.

<div align="center">

**Don't want to memorize SQL syntax?** Describe what you need in plain English and get the query instantly.

**[Try AI2SQL - Generate SQL from English →](https://ai2sql.io)**

</div>

---

## Table of Contents

1. [Data Definition Language (DDL)](#1-data-definition-language-ddl)
   - [CREATE](#create)
   - [ALTER](#alter)
   - [DROP](#drop)
2. [Data Manipulation Language (DML)](#2-data-manipulation-language-dml)
   - [SELECT](#select)
   - [INSERT](#insert)
   - [UPDATE](#update)
   - [DELETE](#delete)
3. [Data Control Language (DCL)](#3-data-control-language-dcl)
   - [GRANT](#grant)
   - [REVOKE](#revoke)
4. [Transaction Control Language (TCL)](#4-transaction-control-language-tcl)
   - [COMMIT](#commit)
   - [ROLLBACK](#rollback)
   - [SAVEPOINT](#savepoint)
5. [Constraints](#5-constraints)
6. [Operators](#6-operators)
7. [Functions](#7-functions)
   - [Aggregate Functions](#aggregate-functions)
   - [String Functions](#string-functions)
   - [Date and Time Functions](#date-and-time-functions)
8. [Joins](#8-joins)
   - [INNER JOIN](#inner-join)
   - [LEFT JOIN](#left-join)
   - [RIGHT JOIN](#right-join)
   - [FULL OUTER JOIN](#full-outer-join)
9. [Subqueries](#9-subqueries)
10. [Views](#10-views)
11. [Indexes](#11-indexes)
12. [Stored Procedures and Functions](#12-stored-procedures-and-functions)
13. [Common Clauses](#13-common-clauses)
    - [WHERE](#where)
    - [GROUP BY](#group-by)
    - [HAVING](#having)
    - [ORDER BY](#order-by)
    - [LIMIT / TOP / FETCH](#limit--top--fetch)
14. [Data Types](#14-data-types)
15. [Window Functions](#15-window-functions)
16. [Common Table Expressions (CTEs)](#16-common-table-expressions-ctes)
17. [Database-Specific Syntax](#17-database-specific-syntax)
18. [Performance and Optimization](#18-performance-and-optimization)
19. [Common Mistakes and Fixes](#19-common-mistakes-and-fixes)
20. [Additional Resources](#20-additional-resources)

---

## 1. Data Definition Language (DDL)

### CREATE

**Create a Database**

```sql
CREATE DATABASE database_name;
```

**Create a Table**

```sql
CREATE TABLE table_name (
    column1 datatype [constraints],
    column2 datatype [constraints],
    ...
);
```

*Example:*

```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    FirstName VARCHAR(50) NOT NULL,
    LastName VARCHAR(50) NOT NULL,
    Email VARCHAR(100) UNIQUE,
    CreatedDate DATE DEFAULT CURRENT_DATE
);
```

### ALTER

**Add a Column**

```sql
ALTER TABLE table_name
ADD column_name datatype [constraints];
```

**Modify a Column**

```sql
ALTER TABLE table_name
MODIFY COLUMN column_name new_datatype;
```

**Drop a Column**

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

### DROP

**Drop a Table**

```sql
DROP TABLE table_name;
```

**Drop a Database**

```sql
DROP DATABASE database_name;
```

---

## 2. Data Manipulation Language (DML)

### SELECT

**Basic Syntax**

```sql
SELECT column1, column2, ...
FROM table_name
[WHERE condition]
[GROUP BY column1, column2, ...]
[HAVING condition]
[ORDER BY column1 [ASC|DESC], column2 [ASC|DESC], ...];
```

*Example:*

```sql
SELECT FirstName, LastName
FROM Customers
WHERE CreatedDate > '2023-01-01'
ORDER BY LastName ASC;
```

### INSERT

**Insert Into All Columns**

```sql
INSERT INTO table_name
VALUES (value1, value2, ...);
```

**Insert Into Specific Columns**

```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```

*Example:*

```sql
INSERT INTO Customers (FirstName, LastName, Email)
VALUES ('Alice', 'Smith', 'alice@example.com');
```

### UPDATE

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

*Example:*

```sql
UPDATE Customers
SET Email = 'newemail@example.com'
WHERE CustomerID = 1;
```

### DELETE

```sql
DELETE FROM table_name
WHERE condition;
```

*Example:*

```sql
DELETE FROM Customers
WHERE CustomerID = 1;
```

---

## 3. Data Control Language (DCL)

### GRANT

```sql
GRANT privilege_type ON object_name TO user [WITH GRANT OPTION];
```

*Example:*

```sql
GRANT SELECT, INSERT ON Customers TO 'db_user';
```

### REVOKE

```sql
REVOKE privilege_type ON object_name FROM user;
```

*Example:*

```sql
REVOKE INSERT ON Customers FROM 'db_user';
```

---

## 4. Transaction Control Language (TCL)

### COMMIT

```sql
COMMIT;
```

### ROLLBACK

```sql
ROLLBACK;
```

### SAVEPOINT

```sql
SAVEPOINT savepoint_name;
```

**Rollback to Savepoint**

```sql
ROLLBACK TO SAVEPOINT savepoint_name;
```

---

## 5. Constraints

- **NOT NULL**: Ensures a column cannot have a NULL value.
- **UNIQUE**: Ensures all values in a column are unique.
- **PRIMARY KEY**: Uniquely identifies each record in a table.
- **FOREIGN KEY**: Ensures referential integrity between tables.
- **CHECK**: Ensures that all values in a column satisfy a specific condition.
- **DEFAULT**: Sets a default value for a column if none is specified.

*Example:*

```sql
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    OrderDate DATE NOT NULL,
    CustomerID INT,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```

---

## 6. Operators

- **Arithmetic Operators**: `+`, `-`, `*`, `/`, `%`
- **Comparison Operators**: `=`, `<>` or `!=`, `>`, `<`, `>=`, `<=`
- **Logical Operators**: `AND`, `OR`, `NOT`
- **Other Operators**: `BETWEEN`, `IN`, `LIKE`, `IS NULL`, `EXISTS`

*Example:*

```sql
SELECT * FROM Products
WHERE Price BETWEEN 10 AND 50;

SELECT * FROM Customers
WHERE Email LIKE '%@example.com';
```

---

## 7. Functions

### Aggregate Functions

- **COUNT()**: Counts the number of rows.
- **SUM()**: Calculates the sum of a numeric column.
- **AVG()**: Calculates the average value.
- **MIN()**: Finds the minimum value.
- **MAX()**: Finds the maximum value.

*Example:*

```sql
SELECT COUNT(*) FROM Orders;

SELECT CustomerID, SUM(TotalAmount) as TotalSpent
FROM Orders
GROUP BY CustomerID;
```

### String Functions

- **UPPER(string)**: Converts to uppercase.
- **LOWER(string)**: Converts to lowercase.
- **SUBSTRING(string, start, length)**: Extracts a substring.
- **TRIM(string)**: Removes whitespace.
- **CONCAT(string1, string2, ...)**: Concatenates strings.

*Example:*

```sql
SELECT UPPER(FirstName), LOWER(LastName)
FROM Customers;
```

### Date and Time Functions

- **NOW()**: Returns current date and time.
- **CURDATE()**: Returns current date.
- **DATE_ADD(date, INTERVAL value unit)**: Adds a time interval to a date.
- **DATEDIFF(date1, date2)**: Returns the difference between two dates.

*Example:*

```sql
SELECT NOW();

SELECT DATE_ADD(CURDATE(), INTERVAL 7 DAY);
```

---

## 8. Joins

### INNER JOIN

Returns records with matching values in both tables.

```sql
SELECT columns
FROM table1
INNER JOIN table2 ON table1.column = table2.column;
```

*Example:*

```sql
SELECT Orders.OrderID, Customers.FirstName, Customers.LastName
FROM Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID;
```

### LEFT JOIN

Returns all records from the left table, and matched records from the right table.

```sql
SELECT columns
FROM table1
LEFT JOIN table2 ON table1.column = table2.column;
```

### RIGHT JOIN

Returns all records from the right table, and matched records from the left table.

```sql
SELECT columns
FROM table1
RIGHT JOIN table2 ON table1.column = table2.column;
```

### FULL OUTER JOIN

Returns all records when there is a match in either left or right table.

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2 ON table1.column = table2.column;
```

> **Writing complex JOINs is error-prone.** Describe your tables and relationships in English, and [AI2SQL](https://ai2sql.io) generates the correct JOIN for you.

---

## 9. Subqueries

A query nested inside another query.

```sql
SELECT column1
FROM table1
WHERE column2 = (SELECT column FROM table2 WHERE condition);
```

*Example:*

```sql
SELECT FirstName, LastName
FROM Customers
WHERE CustomerID IN (SELECT CustomerID FROM Orders WHERE TotalAmount > 1000);
```

> **Nested subqueries getting complicated?** Just describe what data you need. [AI2SQL](https://ai2sql.io) handles the nesting automatically.

---

## 10. Views

A virtual table based on the result set of an SQL statement.

**Create a View**

```sql
CREATE VIEW view_name AS
SELECT columns
FROM table
WHERE condition;
```

*Example:*

```sql
CREATE VIEW HighValueOrders AS
SELECT OrderID, CustomerID, TotalAmount
FROM Orders
WHERE TotalAmount > 1000;
```

---

## 11. Indexes

Used to speed up the retrieval of data.

**Create an Index**

```sql
CREATE INDEX index_name
ON table_name (column1, column2, ...);
```

**Create a Unique Index**

```sql
CREATE UNIQUE INDEX index_name
ON table_name (column);
```

---

## 12. Stored Procedures and Functions

### Stored Procedure

A set of SQL statements that can be stored and executed on the database server.

**Create a Stored Procedure**

```sql
CREATE PROCEDURE procedure_name (parameters)
BEGIN
    -- SQL statements
END;
```

*Example:*

```sql
CREATE PROCEDURE GetCustomerOrders(IN custID INT)
BEGIN
    SELECT * FROM Orders WHERE CustomerID = custID;
END;
```

### User-Defined Function

A function that returns a single value.

**Create a Function**

```sql
CREATE FUNCTION function_name (parameters)
RETURNS datatype
BEGIN
    DECLARE variable datatype;
    -- SQL statements
    RETURN variable;
END;
```

> **Skip the boilerplate.** Describe your procedure's logic in plain English and [AI2SQL](https://ai2sql.io) writes the full stored procedure.

---

## 13. Common Clauses

### WHERE

Filters records that meet specific conditions.

```sql
SELECT * FROM table_name
WHERE condition;
```

### GROUP BY

Groups rows that have the same values in specified columns.

```sql
SELECT column1, AGG_FUNC(column2)
FROM table_name
GROUP BY column1;
```

### HAVING

Filters groups according to specified conditions.

```sql
SELECT column1, AGG_FUNC(column2)
FROM table_name
GROUP BY column1
HAVING condition;
```

### ORDER BY

Sorts the result set.

```sql
SELECT * FROM table_name
ORDER BY column1 [ASC|DESC], column2 [ASC|DESC];
```

### LIMIT / TOP / FETCH

Limits the number of records returned.

- **MySQL, PostgreSQL, SQLite**

  ```sql
  SELECT * FROM table_name
  LIMIT number OFFSET offset;
  ```

- **SQL Server**

  ```sql
  SELECT TOP number * FROM table_name;
  ```

- **Oracle**

  ```sql
  SELECT * FROM table_name
  FETCH FIRST number ROWS ONLY;
  ```

> **Tired of looking up syntax differences between databases?** [AI2SQL](https://ai2sql.io) generates the right syntax for your specific database.

---

## 14. Data Types

### Numeric

- `INT`
- `DECIMAL(p, s)`
- `FLOAT`
- `DOUBLE`

### String

- `CHAR(n)`
- `VARCHAR(n)`
- `TEXT`

### Date and Time

- `DATE`
- `TIME`
- `DATETIME`
- `TIMESTAMP`

### Binary

- `BINARY`
- `VARBINARY`
- `BLOB`

### Boolean

- `BOOLEAN` or `BIT`

---

## 15. Window Functions

```sql
-- ROW_NUMBER
SELECT name, department, salary,
       ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) as rank
FROM employees;

-- RANK and DENSE_RANK
SELECT name, salary,
       RANK() OVER (ORDER BY salary DESC) as rank,
       DENSE_RANK() OVER (ORDER BY salary DESC) as dense_rank
FROM employees;

-- Running total
SELECT date, amount,
       SUM(amount) OVER (ORDER BY date) as running_total
FROM transactions;

-- LAG and LEAD
SELECT date, revenue,
       LAG(revenue, 1) OVER (ORDER BY date) as prev_day,
       revenue - LAG(revenue, 1) OVER (ORDER BY date) as daily_change
FROM daily_sales;
```

---

## 16. Common Table Expressions (CTEs)

```sql
-- Basic CTE
WITH active_customers AS (
    SELECT CustomerID, FirstName, LastName
    FROM Customers
    WHERE LastOrderDate > DATE_SUB(NOW(), INTERVAL 90 DAY)
)
SELECT * FROM active_customers;

-- Recursive CTE (org chart)
WITH RECURSIVE org_chart AS (
    SELECT id, name, manager_id, 1 as level
    FROM employees WHERE manager_id IS NULL
    UNION ALL
    SELECT e.id, e.name, e.manager_id, oc.level + 1
    FROM employees e
    JOIN org_chart oc ON e.manager_id = oc.id
)
SELECT * FROM org_chart ORDER BY level;
```

---

## 17. Database-Specific Syntax

### PostgreSQL

```sql
-- UPSERT
INSERT INTO users (email, name) VALUES ('a@b.com', 'Alice')
ON CONFLICT (email) DO UPDATE SET name = EXCLUDED.name;

-- JSON queries
SELECT data->>'name' as name FROM events WHERE data->>'type' = 'signup';

-- Array operations
SELECT * FROM posts WHERE tags @> ARRAY['sql', 'tutorial'];
```

### MySQL

```sql
-- UPSERT
INSERT INTO users (email, name) VALUES ('a@b.com', 'Alice')
ON DUPLICATE KEY UPDATE name = VALUES(name);

-- JSON queries
SELECT JSON_EXTRACT(data, '$.name') FROM events;

-- Full-text search
SELECT * FROM articles WHERE MATCH(title, body) AGAINST('sql tutorial');
```

### SQL Server

```sql
-- MERGE (UPSERT)
MERGE INTO users AS target
USING (VALUES ('a@b.com', 'Alice')) AS source (email, name)
ON target.email = source.email
WHEN MATCHED THEN UPDATE SET name = source.name
WHEN NOT MATCHED THEN INSERT (email, name) VALUES (source.email, source.name);

-- STRING_AGG
SELECT department, STRING_AGG(name, ', ') as team
FROM employees GROUP BY department;
```

---

## 18. Performance and Optimization

```sql
-- EXPLAIN query plan
EXPLAIN ANALYZE SELECT * FROM orders WHERE customer_id = 42;

-- Index hints (MySQL)
SELECT * FROM orders USE INDEX (idx_customer) WHERE customer_id = 42;

-- Avoid SELECT *
SELECT id, name, email FROM users WHERE active = 1;  -- faster than SELECT *

-- Use EXISTS instead of IN for large datasets
SELECT * FROM customers c
WHERE EXISTS (SELECT 1 FROM orders o WHERE o.customer_id = c.id);
```

---

## 19. Common Mistakes and Fixes

```sql
-- WRONG: NULL comparison
SELECT * FROM users WHERE status = NULL;
-- CORRECT:
SELECT * FROM users WHERE status IS NULL;

-- WRONG: GROUP BY with non-aggregated columns
SELECT name, department, COUNT(*) FROM employees GROUP BY department;
-- CORRECT:
SELECT department, COUNT(*) FROM employees GROUP BY department;

-- WRONG: Using HAVING instead of WHERE
SELECT * FROM orders HAVING total > 100;
-- CORRECT:
SELECT * FROM orders WHERE total > 100;

-- WRONG: Cartesian join (missing JOIN condition)
SELECT * FROM orders, customers;
-- CORRECT:
SELECT * FROM orders JOIN customers ON orders.customer_id = customers.id;
```

---

## 20. Additional Resources

### AI-Powered SQL Tools

- **[AI2SQL](https://ai2sql.io)** - Generate SQL queries from plain English descriptions. Supports MySQL, PostgreSQL, SQL Server, SQLite, and Oracle. No SQL knowledge required.

### Official Documentation
- [MySQL Documentation](https://dev.mysql.com/doc/)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [SQL Server Documentation](https://docs.microsoft.com/en-us/sql/sql-server/)
- [SQLite Documentation](https://www.sqlite.org/docs.html)

### Online Tutorials
- [W3Schools SQL Tutorial](https://www.w3schools.com/sql/)
- [TutorialsPoint SQL Tutorial](https://www.tutorialspoint.com/sql/index.htm)

### Practice Platforms
- [SQLBolt](https://sqlbolt.com/)
- [HackerRank SQL Challenges](https://www.hackerrank.com/domains/sql)
- [LeetCode Database Problems](https://leetcode.com/problemset/database/)

---

## How to Use This Cheat Sheet

- **Learning**: Use this guide as a starting point to learn SQL syntax and concepts.
- **Reference**: Quickly look up syntax for SQL commands and functions.
- **Contribution**: Feel free to contribute by suggesting improvements or adding new sections.

## License

This cheat sheet is released under the [MIT License](LICENSE).

---

**Note:** SQL syntax may vary slightly between different database systems (e.g., MySQL, PostgreSQL, SQL Server, Oracle). Always refer to the official documentation of the database you are using for exact syntax and additional features.

---

<div align="center">

**Writing SQL by hand?** Describe what you need in English and get the query instantly.

**[Try AI2SQL →](https://ai2sql.io)**

</div>
