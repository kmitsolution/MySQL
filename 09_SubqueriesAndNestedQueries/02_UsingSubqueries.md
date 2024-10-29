### Using Subqueries in MySQL

Subqueries can be utilized in various SQL statements such as `SELECT`, `INSERT`, `UPDATE`, and `DELETE`. They provide a powerful way to perform operations based on the results of another query. Below are examples of how to use subqueries in each of these contexts.

### 1. Subqueries in SELECT

**Use Case**: Find employees who earn more than the average salary.

```sql
SELECT employee_name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

**Explanation**: This subquery calculates the average salary from the `employees` table and the outer query retrieves employee names and salaries that exceed this average.

### 2. Subqueries in INSERT

**Use Case**: Insert a new employee with a salary higher than the average salary.

```sql
INSERT INTO employees (employee_name, department_id, salary)
VALUES ('New Employee', 1, 
    (SELECT AVG(salary) + 5000 FROM employees));
```

**Explanation**: This subquery calculates the average salary and adds $5,000, which is then used as the salary for the new employee being inserted.

### 3. Subqueries in UPDATE

**Use Case**: Increase the salary of employees in the HR department by 10% if their salary is less than the average salary of all employees.

```sql
UPDATE employees
SET salary = salary * 1.10
WHERE department_id = (SELECT department_id FROM departments WHERE department_name = 'HR')
AND salary < (SELECT AVG(salary) FROM employees);
```

**Explanation**: The subquery retrieves the department ID for HR, and another subquery calculates the average salary. The outer query updates the salaries of employees in the HR department who earn less than the average.

### 4. Subqueries in DELETE

**Use Case**: Delete employees who earn less than the average salary.

```sql
DELETE FROM employees
WHERE salary < (SELECT AVG(salary) FROM employees);
```

**Explanation**: This subquery calculates the average salary, and the outer query deletes employees whose salaries fall below this average.

### Conclusion

Subqueries enhance the flexibility and power of SQL queries, enabling complex data manipulations and retrievals across different statements. By effectively utilizing subqueries in `SELECT`, `INSERT`, `UPDATE`, and `DELETE`, you can perform sophisticated operations in MySQL that are crucial for robust data management and analysis.
