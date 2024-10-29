### Subqueries in MySQL

A **subquery** is a query nested inside another query. It allows you to use the result of one query as an input for another. Subqueries can be used in various clauses, such as `SELECT`, `FROM`, `WHERE`, and `HAVATE`.

### Types of Subqueries

1. **Single-Row Subquery**: Returns a single value (one row, one column).
2. **Multiple-Row Subquery**: Returns multiple rows.
3. **Multiple-Column Subquery**: Returns multiple columns.

### Example Tables

Consider the following two tables: `employees` and `departments`.

**employees**:
| employee_id | employee_name | department_id | salary |
|-------------|---------------|---------------|--------|
| 1           | Alice         | 1             | 70000  |
| 2           | Bob           | 2             | 80000  |
| 3           | Charlie       | 1             | 75000  |
| 4           | David         | 3             | 60000  |
| 5           | Eva           | 2             | 72000  |

**departments**:
| department_id | department_name |
|---------------|------------------|
| 1             | HR               |
| 2             | IT               |
| 3             | Sales            |

### Examples of Subqueries

#### 1. Single-Row Subquery

**Use Case**: Find the salary of the employee with the highest salary.

```sql
SELECT employee_name, salary
FROM employees
WHERE salary = (SELECT MAX(salary) FROM employees);
```

**Result**:
| employee_name | salary |
|---------------|--------|
| Bob           | 80000  |

#### 2. Multiple-Row Subquery

**Use Case**: Find employees who earn more than the average salary.

```sql
SELECT employee_name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

**Result**:
| employee_name | salary |
|---------------|--------|
| Bob           | 80000  |
| Charlie       | 75000  |

#### 3. Subquery in the FROM Clause

**Use Case**: List departments and the average salary of employees in each department.

```sql
SELECT d.department_name, avg_salaries.avg_salary
FROM departments AS d
JOIN (SELECT department_id, AVG(salary) AS avg_salary
      FROM employees
      GROUP BY department_id) AS avg_salaries
ON d.department_id = avg_salaries.department_id;
```

**Result**:
| department_name | avg_salary |
|------------------|------------|
| HR               | 72500      |
| IT               | 76000      |
| Sales            | 60000      |

### 4. Subquery in the HAVING Clause

**Use Case**: Find departments where the total salary exceeds $130,000.

```sql
SELECT department_id, SUM(salary) AS TotalSalaries
FROM employees
GROUP BY department_id
HAVING SUM(salary) > (SELECT 130000);
```

**Result**:
| department_id | TotalSalaries |
|---------------|---------------|
| 2             | 152000        |

### Conclusion

Subqueries are a powerful tool in MySQL that allow for complex data retrieval and manipulation. By using subqueries, you can achieve results that would be difficult or impossible with simple queries. Understanding how to effectively use subqueries will enhance your ability to perform advanced data analysis in MySQL.
