# Basic SQL Commands

## Table of Contents
- [SELECT Statement](#select-statement)
- [WHERE Clause](#where-clause)
- [ORDER BY Clause](#order-by-clause)
- [LIMIT Clause](#limit-clause)
- [GROUP BY Clause](#group-by-clause)
- [INSERT Statement](#insert-statement)
- [UPDATE Statement](#update-statement)
- [DELETE Statement](#delete-statement)
- [Common Interview Questions](#common-interview-questions)

## SELECT Statement

The `SELECT` statement is used to retrieve data from a database.

```sql
-- Basic SELECT syntax
SELECT column1, column2, ...
FROM table_name;

-- Select all columns
SELECT * FROM employees;

-- Select specific columns
SELECT employee_id, first_name, last_name
FROM employees;

-- Using column aliases
SELECT first_name AS name, salary AS annual_pay
FROM employees;
```

### Key Points
- Use `*` to select all columns (not recommended in production code for performance reasons)
- Column aliases are defined with the `AS` keyword (the `AS` keyword is optional but recommended for clarity)
- SQL keywords are not case-sensitive, but it's common practice to write them in uppercase

## WHERE Clause

The `WHERE` clause is used to filter records based on a specified condition.

```sql
-- Basic WHERE syntax
SELECT column1, column2, ...
FROM table_name
WHERE condition;

-- Examples
SELECT * FROM employees WHERE department_id = 10;
SELECT * FROM employees WHERE salary > 50000;
SELECT * FROM employees WHERE hire_date < '2020-01-01';
```

### Comparison Operators
- Equal (`=`)
- Not Equal (`<>` or `!=`)
- Greater Than (`>`)
- Less Than (`<`)
- Greater Than or Equal To (`>=`)
- Less Than or Equal To (`<=`)

### Logical Operators
- `AND` - Returns true if both conditions are true
- `OR` - Returns true if either condition is true
- `NOT` - Returns true if the condition is false

```sql
-- Using logical operators
SELECT * FROM employees
WHERE department_id = 10 AND salary > 50000;

SELECT * FROM employees
WHERE department_id = 10 OR department_id = 20;

SELECT * FROM employees
WHERE NOT department_id = 10;
```

### Special Operators
- `IN` - Checks if a value matches any value in a list
- `BETWEEN` - Checks if a value is within a range
- `LIKE` - Searches for a pattern
- `IS NULL` / `IS NOT NULL` - Checks for NULL values

```sql
-- IN operator
SELECT * FROM employees
WHERE department_id IN (10, 20, 30);

-- BETWEEN operator
SELECT * FROM employees
WHERE salary BETWEEN 50000 AND 70000;

-- LIKE operator
SELECT * FROM employees
WHERE last_name LIKE 'S%';  -- Names starting with S
SELECT * FROM employees 
WHERE email LIKE '%@example.com';  -- Emails ending with @example.com

-- NULL checks
SELECT * FROM employees
WHERE manager_id IS NULL;
```

## ORDER BY Clause

The `ORDER BY` clause is used to sort the result set.

```sql
-- Basic ORDER BY syntax
SELECT column1, column2, ...
FROM table_name
ORDER BY column1 [ASC|DESC], column2 [ASC|DESC], ...;

-- Examples
SELECT * FROM employees
ORDER BY last_name ASC;  -- Ascending order (default)

SELECT * FROM employees
ORDER BY salary DESC;  -- Descending order

-- Multiple columns
SELECT * FROM employees
ORDER BY department_id ASC, salary DESC;
```

## LIMIT Clause

The `LIMIT` clause is used to restrict the number of rows returned.

```sql
-- MySQL/PostgreSQL/SQLite syntax
SELECT * FROM employees
LIMIT 10;

-- Skip first 5 records, return next 10
SELECT * FROM employees
LIMIT 10 OFFSET 5;

-- SQL Server/Oracle syntax
SELECT TOP 10 * FROM employees;  -- SQL Server
SELECT * FROM employees WHERE ROWNUM <= 10;  -- Oracle
```

## GROUP BY Clause

The `GROUP BY` clause is used with aggregate functions to group the result set by one or more columns.

```sql
-- Basic GROUP BY syntax
SELECT column1, aggregate_function(column2)
FROM table_name
GROUP BY column1;

-- Examples
SELECT department_id, COUNT(*) as employee_count
FROM employees
GROUP BY department_id;

SELECT department_id, AVG(salary) as avg_salary
FROM employees
GROUP BY department_id;
```

### Common Aggregate Functions
- `COUNT()` - Returns the number of rows
- `SUM()` - Returns the sum of all values
- `AVG()` - Returns the average of the values
- `MIN()` - Returns the minimum value
- `MAX()` - Returns the maximum value

## INSERT Statement

The `INSERT` statement is used to insert new records in a table.

```sql
-- Basic INSERT syntax
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);

-- Example
INSERT INTO employees (employee_id, first_name, last_name, email, hire_date, job_id, salary)
VALUES (207, 'John', 'Smith', 'jsmith@example.com', '2023-05-15', 'IT_PROG', 60000);

-- Insert multiple rows
INSERT INTO employees (employee_id, first_name, last_name, email)
VALUES 
    (208, 'Jane', 'Doe', 'jdoe@example.com'),
    (209, 'Mike', 'Johnson', 'mjohnson@example.com');
```

## UPDATE Statement

The `UPDATE` statement is used to modify existing records in a table.

```sql
-- Basic UPDATE syntax
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;

-- Example
UPDATE employees
SET salary = 65000, department_id = 20
WHERE employee_id = 207;
```

### Important!
Always use a `WHERE` clause with `UPDATE` statements unless you want to update all rows.

## DELETE Statement

The `DELETE` statement is used to delete records from a table.

```sql
-- Basic DELETE syntax
DELETE FROM table_name
WHERE condition;

-- Example
DELETE FROM employees
WHERE employee_id = 207;
```

### Important!
Always use a `WHERE` clause with `DELETE` statements unless you want to delete all rows.

## Common Interview Questions

1. **What's the difference between `DELETE` and `TRUNCATE`?**
   
   - `DELETE` is a DML (Data Manipulation Language) command that can be used with a `WHERE` clause to remove specific rows.
   - `TRUNCATE` is a DDL (Data Definition Language) command that removes all rows from a table and typically cannot be rolled back.
   - `DELETE` logs individual row deletions, while `TRUNCATE` logs only the page deallocation.
   - `TRUNCATE` is typically faster than `DELETE` when removing all rows.

2. **How do you select distinct values from a column?**

   ```sql
   SELECT DISTINCT department_id FROM employees;
   ```

3. **How would you find the second highest salary in the employees table?**

   ```sql
   -- Using subquery
   SELECT MAX(salary) FROM employees
   WHERE salary < (SELECT MAX(salary) FROM employees);
   
   -- Using ORDER BY and LIMIT
   SELECT salary FROM employees
   ORDER BY salary DESC
   LIMIT 1 OFFSET 1;
   ```

4. **What are wildcards in SQL and how do you use them?**

   Wildcards are used with the `LIKE` operator:
   - `%` - Represents zero or more characters
   - `_` - Represents a single character
   
   ```sql
   -- Find all employees whose last name starts with 'S'
   SELECT * FROM employees WHERE last_name LIKE 'S%';
   
   -- Find all employees whose last name is exactly 5 characters long
   SELECT * FROM employees WHERE last_name LIKE '_____';
   ```

5. **How do you count the number of rows in a table?**

   ```sql
   SELECT COUNT(*) FROM employees;
   ```

---

[Back to SQL & Database Main Page](./README.md)
