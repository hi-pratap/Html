# Sql Queries

Created: June 24, 2023 5:20 PM
Date: July 1, 2023 5:20 PM
Select: SQL

---

Certainly! Here are the 50 SQL queries categorized into different categories:

# Basic Queries:

### 1. Write a query to retrieve all records from a table.

- Description: This query retrieves all the records from a specified table.
- Query: `SELECT * FROM table_name;`
1. Write a query to retrieve specific columns from a table.
    - Description: This query retrieves specific columns from a specified table.
    - Query: `SELECT column1, column2 FROM table_name;`
2. Write a query to retrieve distinct values from a column.
    - Description: This query retrieves unique/distinct values from a specified column in a table.
    - Query: `SELECT DISTINCT column_name FROM table_name;`
3. Write a query to filter records based on a condition.
    - Description: This query retrieves records from a table based on a specified condition.
    - Query: `SELECT * FROM table_name WHERE condition;`
4. Write a query to sort records in ascending order.
    - Description: This query retrieves records from a table and sorts them in ascending order based on a specified column.
    - Query: `SELECT * FROM table_name ORDER BY column_name ASC;`
5. Write a query to sort records in descending order.
    - Description: This query retrieves records from a table and sorts them in descending order based on a specified column.
    - Query: `SELECT * FROM table_name ORDER BY column_name DESC;`

### Advanced Queries:

1. Write a query to retrieve records with NULL values in a column.
    - Description: This query retrieves records from a table where a specified column has NULL values.
    - Query: `SELECT * FROM table_name WHERE column_name IS NULL;`
2. Write a query to retrieve records between a specific range of values.
    - Description: This query retrieves records from a table where a specified column's value falls within a range.
    - Query: `SELECT * FROM table_name WHERE column_name BETWEEN value1 AND value2;`
3. Write a query to count the number of records in a table.
    - Description: This query calculates the total count of records in a specified table.
    - Query: `SELECT COUNT(*) FROM table_name;`
4. Write a query to calculate the average of a column.
    - Description: This query calculates the average value of a specified column in a table.
    - Query: `SELECT AVG(column_name) FROM table_name;`
5. Write a query to calculate the sum of a column.
    - Description: This query calculates the sum of values in a specified column of a table.
    - Query: `SELECT SUM(column_name) FROM table_name;`

### Conditional Queries:

1. Write a query to find the minimum value in a column.
    - Description: This query retrieves the minimum value from a specified column in a table.
    - Query: `SELECT MIN(column_name) FROM table_name;`
2. Write a query to find the maximum value in a column.
    - Description: This query retrieves the maximum value from a specified column in a table.
    - Query: `SELECT MAX(column_name) FROM table_name;`
3. Write a query to retrieve records based on multiple conditions using AND.
    - Description: This query retrieves records from a table based on multiple conditions using the logical operator AND.
    - Query:
    
    ```
    SELECT * FROM table_name WHERE condition1 AND condition2;
    
    ```
    
4. Write a query to retrieve records based on multiple conditions using OR.
    - Description: This query retrieves records from a table based on multiple conditions using the logical operator OR.
    - Query:
    
    ```
    SELECT * FROM table_name WHERE condition1 OR condition2;
    
    ```
    
5. Write a query to retrieve records that match a specific pattern using LIKE.
    - Description: This query retrieves records from a table where a specified column matches a specific pattern using the LIKE operator.
    - Query:
    
    ```
    SELECT * FROM table_name WHERE column_name LIKE 'pattern';
    
    ```
    

### Join Queries:

1. Write a query to join two tables based on a common column.
    - Description: This query joins two tables based on a common column and retrieves the combined records.
    - Query:
    
    ```
    SELECT * FROM table1 JOIN table2 ON table1.column = table2.column;
    
    ```
    
2. Write a query to retrieve records from one table that have no matching records in another table.
    - Description: This query retrieves records from one table that do not have any matching records in another table.
    - Query:
    
    ```
    SELECT * FROM table1 WHERE column NOT IN (SELECT column FROM table2);
    
    ```
    
3. Write a query to retrieve records from two tables with a one-to-many relationship.
    - Description: This query retrieves records from two tables that have a one-to-many relationship based on a common column.
    - Query:
    
    ```
    SELECT * FROM table1 JOIN table2 ON table1.column = table2.column;
    
    ```
    
4. Write a query to retrieve records from two tables with a many-to-many relationship.
    - Description: This query retrieves records from two tables that have a many-to-many relationship based on a junction table.
    - Query:
    
    ```
    SELECT * FROM table1 JOIN junction_table ON table1.column = junction_table.column JOIN table2 ON junction_table.column = table2.column;
    
    ```
    

### Subqueries:

1. Write a query to retrieve records that are present in both tables.
    - Description: This query retrieves records that are common to both specified tables.
    - Query:
    
    ```
    SELECT * FROM table1 INTERSECT SELECT * FROM table2;
    
    ```
    
2. Write a query to retrieve records from a table using a subquery.
    - Description: This query retrieves records from a table based on the result of a subquery.
    - Query:
    
    ```
    SELECT * FROM table_name WHERE column IN (SELECT column FROM subquery);
    
    ```
    

### Data Manipulation:

1. Write a query to update records in a table based on a condition.
    - Description: This query updates records in a table based on a specified condition.
    - Query:
    
    ```
    UPDATE table_name SET column = value WHERE condition;
    
    ```
    
2. Write a query to delete records from a table based on a condition.
    - Description: This query deletes records from a table based on a specified condition.
    - Query:
    
    ```
    DELETE FROM table_name WHERE condition;
    
    ```
    
3. Write a query to insert records into a table.
    - Description: This query inserts new records into a table with specified values.
    - Query:
    
    ```
    INSERT INTO table_name (column1, column2) VALUES (value1, value2);
    
    ```
    
4. Write a query to insert records into a table with values from another table.
    - Description: This query inserts new records into a table with values retrieved from another table.
    - Query:
    
    ```
    INSERT INTO table1 (column1, column2) SELECT column1, column2 FROM table2;
    
    ```
    

### Table Manipulation:

1. Write a query to create a new table with specific columns.
    - Description: This query creates a new table with specified columns and data types.
    - Query:

```
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    ...
);

```

1. Write a query to add a new column to an existing table.
    - Description: This query adds a new column to an existing table.
    - Query:
    
    ```
    ALTER TABLE table_name ADD column_name datatype;
    
    ```
    
2. Write a query to modify the structure of a table.
    - Description: This query modifies the data type or properties of a column in an existing table.
    - Query:
    
    ```
    ALTER TABLE table_name MODIFY column_name new_datatype;
    
    ```
    
3. Write a query to delete a table from the database.
    - Description: This query deletes a specified table from the database.
    - Query:
    
    ```
    DROP TABLE table_name;
    
    ```
    

### Miscellaneous Queries:

1. Write a query to retrieve the top N records from a table.
    - Description: This query retrieves the top N records from a table.
    - Query:
    
    ```
    SELECT * FROM table_name LIMIT N;
    
    ```
    
2. Write a query to retrieve the Nth highest value from a column.
    - Description: This query retrieves the Nth highest value from a specified column in a table.
    - Query:
    
    ```
    SELECT column_name FROM table_name ORDER BY column_name DESC LIMIT N-1, 1;
    
    ```
    
3. Write a query to calculate the total sales for each product.
    - Description: This query calculates the total sales for each product in a sales table.
    - Query:
    
    ```
    SELECT product_name, SUM(sales) FROM sales_table GROUP BY product_name;
    
    ```
    
4. Write a query to calculate the average salary by department.
    - Description: This query calculates the average salary for each department in an employee table.
    - Query:
    
    ```
    SELECT department, AVG(salary) FROM employee_table GROUP BY department;
    
    ```
    
5. Write a query to find duplicate records in a table.
    - Description: This query retrieves duplicate records based on a specified column in a table.
    - Query:
    
    ```
    SELECT column, COUNT(*) FROM table_name GROUP BY column HAVING COUNT(*) > 1;
    
    ```
    
6. Write a query to retrieve records based on multiple conditions using IN.
    - Description: This query retrieves records from a table based on multiple conditions using the IN operator.
    - Query:
    
    ```
    SELECT * FROM table_name WHERE column_name IN (value1, value2, ...);
    
    ```
    
7. Write a query to retrieve records based on a condition using BETWEEN.
    - Description: This query retrieves records from a table based on a condition using the BETWEEN operator.
    - Query:
    
    ```
    SELECT * FROM table_name WHERE column_name BETWEEN value1 AND value2;
    
    ```
    
8. Write a query to calculate the total revenue for each month.
    - Description: This query calculates the total revenue for each month in a sales table.
    - Query:
    
    ```
    SELECT MONTH(date_column), SUM(revenue) FROM sales_table GROUP BY MONTH(date_column);
    
    ```
    
9. Write a query to retrieve the most recent records from a table.
    - Description: This query retrieves the most recent records from a table based on a date column.
    - Query:
    
    ```
    SELECT * FROM table_name ORDER BY date_column DESC;
    
    ```
    

These are the 50 SQL queries categorized into different categories. Feel free to modify them according to your specific requirements.