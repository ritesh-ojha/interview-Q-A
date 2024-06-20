# Most Used Funtions in DAX

### 1. SUM()
- Purpose: Calculates the sum of a column.
- Syntax: SUM(ColumnName)
- Example:
    - Scenario: You have a table named Sales with a column Amount.
    - Usage: 
    ```
    Total Sales = SUM(Sales[Amount])
    ```
    - Explanation: This measure will calculate the total sales amount by summing up all the values in the Amount column of the Sales table.
### 2. AVERAGE()
- Purpose: Calculates the average of a column.
- Syntax: AVERAGE(ColumnName)
- Example:
    - Scenario: You have a table named Sales with a column Amount.
    - Usage: 
    ```
    Average Sales = AVERAGE(Sales[Amount])
    ```
    - Explanation: This measure will calculate the average sales amount by averaging all the values in the Amount column of the Sales table.
### 3. COUNT()
- Purpose: Counts the number of non-blank rows in a column.
- Syntax: COUNT(ColumnName)
- Example:
    - Scenario: You have a table named Customers with a column CustomerID.
    - Usage: 
    ```
    Customer Count = COUNT(Customers[CustomerID])
    ```
    - Explanation: This measure will count the number of non-blank customer IDs in the CustomerID column.
### 4. COUNTA()
- Purpose: Counts the number of non-blank values in a column.
- Syntax: COUNTA(ColumnName)
- Example:
    - Scenario: You have a table named Sales with a column OrderID.
    - Usage: 
    ```
    Order Count = COUNTA(Sales[OrderID])
    ```
    - Explanation: This measure will count the number of non-blank order IDs in the OrderID column.
### 5. COUNTROWS()
- Purpose: Counts the number of rows in a table.
- Syntax: COUNTROWS(TableName)
- Example:
    - Scenario: You have a table named Sales.
    - Usage: 
    ```
    Total Orders = COUNTROWS(Sales)
    ```
    - Explanation: This measure will count the number of rows in the Sales table.
### 6. IF()
- Purpose: Returns one value if a condition is true and another value if it is false.
- Syntax: IF(Condition, Result_If_True, Result_If_False)
- Example:
    - Scenario: You want to categorize sales amounts as "High" or "Low" based on a threshold.
    - Usage: 
    ```
    Sales Category = IF(Sales[Amount] > 1000, "High", "Low")
    ```
    - Explanation: This calculated column will categorize each sale as "High" if the Amount is greater than 1000, otherwise as "Low".
### 7. CALCULATE()
- Purpose: Evaluates an expression in a modified filter context.
- Syntax: CALCULATE(Expression, Filters)
- Example:
    - Scenario: You want to calculate total sales for a specific region.
    - Usage: 
    ```
    Total Sales West = CALCULATE(SUM(Sales[Amount]), Sales[Region] = "West")
    ```
    - Explanation: This measure will calculate the total sales amount for the "West" region by summing the Amount column within the context where Region is "West".
### 8. FILTER()
- Purpose: Returns a table that represents a subset of another table or expression.
- Syntax: FILTER(Table, Expression)
- Example:
    - Scenario: You want to filter sales data for a specific product.
    - Usage: 
    ```
    Filtered Sales = FILTER(Sales, Sales[ProductID] = 123)
    ```
    - Explanation: This will return a table of sales data where the ProductID is 123.
### 9. RELATED()
- Purpose: Returns a related value from another table.
- Syntax: RELATED(ColumnName)
- Example:
    - Scenario: You have a Sales table and a related Products table.
    - Usage: 
    ```
    Product Name = RELATED(Products[ProductName])
    ```
    - Explanation: This calculated column in the Sales table will return the product name from the related Products table.
### 10. ALLEXCEPT()
- Purpose: Removes all filters from a table except the ones specified.
- Syntax: ALLEXCEPT(Table, Column1, Column2, ...)
- Example:
    - Scenario: You want to calculate total sales ignoring all filters except the Region.
    - Usage: 
    ```
    Total Sales Except Region = CALCULATE(SUM(Sales[Amount]), ALLEXCEPT(Sales, Sales[Region]))
    ```
    - Explanation: This measure will calculate total sales ignoring all filters except those applied to the Region column.
### 11. DISTINCT()
- Purpose: Returns a one-column table that contains the distinct values from the specified column.
- Syntax: DISTINCT(ColumnName)
- Example:
    - Scenario: You want to count the number of distinct customers.
    - Usage:
    ```
    Distinct Customers = COUNTROWS(DISTINCT(Sales[CustomerID]))
    ```
    - Explanation: This measure will count the number of distinct customers in the CustomerID column of the Sales table.
### 12. SUMX()
- Purpose: Evaluates an expression for each row in a table and then sums the results.
- Syntax: SUMX(Table, Expression)
- Example:
    - Scenario: You want to calculate total revenue by multiplying quantity by price for each sale.
    - Usage:
    ```
    Total Revenue = SUMX(Sales, Sales[Quantity] * Sales[Price])
    ```
    - Explanation: This measure will calculate total revenue by evaluating the expression Sales[Quantity] * Sales[Price] for each row and then summing the results.
### 13. EARLIER()
- Purpose: Refers to an earlier row context in a nested calculation.
- Syntax: EARLIER(ColumnName, [N])
- Example:
    - Scenario: You want to calculate the running total of sales.
    - Usage: 
    ```
    Running Total = CALCULATE(SUM(Sales[Amount]), FILTER(ALL(Sales), Sales
    [Date] <= EARLIER(Sales[Date])))
    ```
    - Explanation: This calculated column will compute a running total of sales amounts up to the current row's date.
### 14. ALL()
- Purpose: Removes all filters from the specified table or column.
- Syntax: ALL(Table|Column)
- Example:
    - Scenario: You want to calculate total sales without any filters.
    - Usage: 
    ```
    Total Sales All = CALCULATE(SUM(Sales[Amount]), ALL(Sales))
    ```
    - Explanation: This measure will calculate the total sales amount by removing all filters from the Sales table.