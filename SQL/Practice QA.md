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
---------------------------------------------------------

### Question:

Given the tables employees and departments:

`employees`(employee_id, employee_name, department_id, salary, join_date)
`departments`(department_id, department_name)

Write a SQL query to find the average salary of employees who have joined within the last year for each department, and include the department name. Additionally, include departments with no employees who joined in the last year with an average salary of 0.

### Answer:

```sql
SELECT d.department_name, COALESCE(AVG(e.salary), 0) AS average_salary
FROM departments d
LEFT JOIN employees e ON d.department_id = e.department_id AND e.join_date >= DATEADD(year, -1, GETDATE())
GROUP BY d.department_name;
```

### Explanation
- LEFT JOIN:

    - We perform a LEFT JOIN to include all departments, even those without employees who joined in the last year.
    - The condition e.join_date >= DATEADD(year, -1, GETDATE()) filters employees who have joined within the last year.
- COALESCE:

    - The COALESCE function is used to return 0 when there are no employees who joined in the last year in a department (i.e., when AVG(e.salary) is NULL).
- GROUP BY:

    - The GROUP BY d.department_name groups the results by department, allowing us to calculate the average salary for each department.

-----------------------------------
### Question:
You have three tables: employees, departments, and projects.

- employees(employee_id, employee_name, department_id, salary)
- departments(department_id, department_name)
- projects(project_id, project_name, budget)

Each employee can be assigned to multiple projects through the employee_projects table:

- employee_projects(employee_id, project_id)

Write a SQL query to find the total salary of employees assigned to each project, along with the project name and budget. Include projects with no employees assigned, showing a total salary of 0 for those projects.

### Answer:
```SQL
SELECT p.project_name, p.budget, COALESCE(SUM(e.salary), 0) AS total_salary
FROM projects p
LEFT JOIN employee_projects ep ON p.project_id = ep.project_id
LEFT JOIN employees e ON ep.employee_id = e.employee_id
GROUP BY p.project_name, p.budget;
```

### Explanation
- LEFT JOIN:

    - The first LEFT JOIN between projects (p) and employee_projects (ep) ensures that all projects are included, even those without assigned employees.
    - The second LEFT JOIN between employee_projects (ep) and employees (e) brings in employee details, including their salary.
- COALESCE:

    - The COALESCE function is used to return 0 when there are no employees assigned to a project (i.e., when SUM(e.salary) is NULL).
- GROUP BY:

    - The GROUP BY p.project_name, p.budget groups the results by project name and budget, allowing us to calculate the total salary for each project.

----------------------------
### Question:

Given the tables employees, departments, and projects:

- employees(employee_id, employee_name, department_id, salary)
- departments(department_id, department_name)
- projects(project_id, project_name, budget)

Each employee can be assigned to multiple projects through the employee_projects table:

- employee_projects(employee_id, project_id)

Write a SQL query to find the highest-paid employee in each project, along with their project name, project budget, and the average salary of employees in the same department as the highest-paid employee for that project.

### Answer:

```sql
WITH ProjectSalaries AS (
    SELECT 
        ep.project_id,
        e.employee_id,
        e.salary,
        ROW_NUMBER() OVER (PARTITION BY ep.project_id ORDER BY e.salary DESC) AS rank
    FROM 
        employee_projects ep
    JOIN 
        employees e ON ep.employee_id = e.employee_id
),
HighestPaidEmployees AS (
    SELECT 
        ps.project_id,
        ps.employee_id,
        ps.salary AS highest_salary
    FROM 
        ProjectSalaries ps
    WHERE 
        ps.rank = 1
),
DepartmentAverageSalaries AS (
    SELECT
        e.department_id,
        AVG(e.salary) AS avg_department_salary
    FROM
        employees e
    GROUP BY
        e.department_id
)
SELECT 
    p.project_name,
    p.budget,
    e.employee_name AS highest_paid_employee,
    hpe.highest_salary,
    das.avg_department_salary
FROM 
    HighestPaidEmployees hpe
JOIN 
    employees e ON hpe.employee_id = e.employee_id
JOIN 
    projects p ON hpe.project_id = p.project_id
JOIN 
    DepartmentAverageSalaries das ON e.department_id = das.department_id;
```

### Explanation:
- CTE: ProjectSalaries:

    - This common table expression (CTE) calculates the salary for each employee assigned to each project and ranks them by salary within each project using ROW_NUMBER().
- CTE: HighestPaidEmployees:

    - This CTE selects the highest-paid employee for each project by filtering where rank = 1.
- CTE: DepartmentAverageSalaries:

    - This CTE calculates the average salary for each department.
- Final SELECT Statement:

    - Joins the highest-paid employees with the employees, projects, and DepartmentAverageSalaries tables to get the required details:
    - project_name and budget from projects.
    - employee_name and highest_salary from employees and HighestPaidEmployees.
    - avg_department_salary from DepartmentAverageSalaries.
