# Complex Question
### Question:

You have two tables, employees and departments. The employees table contains the following columns: employee_id, employee_name, department_id, and salary. The departments table contains the columns: department_id and department_name.

Write a SQL query to find the highest-paid employee in each department, along with their department name and salary.

### Answer:
```sql
SELECT d.department_name, e.employee_name, e.salary
FROM employees e
JOIN departments d ON e.department_id = d.department_id
WHERE e.salary = (
    SELECT MAX(salary)
    FROM employees
    WHERE department_id = e.department_id
);
```

## Explanation
- Inner Query (Subquery):

    - The inner query selects the maximum salary for each department.

    - SELECT MAX(salary) FROM employees WHERE department_id = e.department_id fetches the highest salary for the department of the current employee (e.department_id).

- Outer Query:

    - The outer query joins the employees and departments tables on the department_id.

    - It selects the department_name from the departments table, and the employee_name and salary from the employees table.

    - The WHERE clause ensures that only the employees with the maximum salary in their respective departments are selected by matching the employee’s salary with the result of the inner query.