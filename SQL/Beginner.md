# Basic Questions

## What is SQL?
SQL is a language for querying databases. It is a standard language for accessing databases and it is supported
by all the major database systems such as Oracle, MS SQL Server, MySQL, PostgreSQL, etc.

## What is a database?
A database is an organized collection of data stored and accessed electronically. It can be managed by a Database Management System (DBMS).

## What is a table in a database?
A table is a collection of related data entries organized in rows and columns. Each column represents a field, and each row represents a record.

## What is a primary key?
A primary key is a unique identifier for each record in a table. It must contain unique values and cannot contain NULL values.

## What is a foreign key?
A foreign key is a column or group of columns in one table that provides a link between data in two tables. It is a field (or collection of fields) in one table that uniquely identifies a row of another table.

# Query Questions

## How do you retrieve all the records from a table?
```sql
SELECT * FROM table_name;
```

## How do you retrieve specific columns from a table?
```sql
SELECT column1, column2 FROM table_name;
```

## How do you filter records in SQL?
```sql
SELECT * FROM table_name WHERE condition;
```

## How do you sort records in SQL?
```sql
SELECT * FROM table_name ORDER BY column_name [ASC|DESC];
```

## How do you insert a new record into a table?
```sql
INSERT INTO table_name (column1, column2) VALUES (value1, value2);
```

# Join Questions

## What is a join in SQL?
A join is a SQL operation that combines rows from two or more tables based on a related column between them.

## What are the different types of joins?
- INNER JOIN: Returns records that have matching values in both tables.
- LEFT (OUTER) JOIN: Returns all records from the left table and matched records from the right table.
- RIGHT (OUTER) JOIN: Returns all records from the right table and matched records from the left table.
- FULL (OUTER) JOIN: Returns all records when there is a match in either left or right table.

## How do you perform an inner join?
```sql
SELECT columns
FROM table1
INNER JOIN table2 ON table1.common_column = table2.common_column;
```

# Aggregate Functions

## What are aggregate functions?
 Aggregate functions perform a calculation on a set of values and return a single value. Common aggregate functions include SUM(), AVG(), COUNT(), MIN(), and MAX().

## How do you count the number of records in a table?
```sql
SELECT COUNT(*) FROM table_name;
```

## How do you find the average value of a column?
```sql
SELECT AVG(column_name) FROM table_name;
```

# Advanced Beginner Questions

## What is a subquery?
A subquery is a query nested inside another query. It can be used in SELECT, INSERT, UPDATE, or DELETE statements or inside another subquery.

## What is a view in SQL?
A view is a virtual table based on the result set of an SQL statement. It contains rows and columns just like a real table and can be queried like a regular table.

## How do you update existing records in a table?
```sql
UPDATE table_name
SET column1 = value1, column2 = value2
WHERE condition;
```

## How do you delete records from a table?
```sql
DELETE FROM table_name WHERE condition;
```




