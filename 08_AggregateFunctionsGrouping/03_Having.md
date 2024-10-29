### HAVING Clause in MySQL

The `HAVING` clause in SQL is used to filter records after aggregation has been performed, allowing you to specify conditions on groups created by the `GROUP BY` clause. While the `WHERE` clause filters rows before aggregation, `HAVING` filters groups after the aggregation has taken place.

### Syntax

The basic syntax for using the `HAVING` clause is:

```sql
SELECT column1, aggregate_function(column2)
FROM table_name
GROUP BY column1
HAVING condition;
```

### Example of Using HAVING

Assuming you have the following `employees` table:

**employees**:
| employee_id | employee_name | department_id | salary |
|-------------|---------------|---------------|--------|
| 1           | Alice         | 1             | 70000  |
| 2           | Bob           | 2             | 80000  |
| 3           | Charlie       | 1             | 75000  |
| 4           | David         | 3             | 60000  |
| 5           | Eva           | 2             | 72000  |

#### Example Queries

1. **Count Employees by Department with a Condition**:

To count the number of employees in each department but only show departments with more than one employee:

```sql
SELECT department_id, COUNT(*) AS EmployeeCount
FROM employees
GROUP BY department_id
HAVING COUNT(*) > 1;
```

**Result**:
| department_id | EmployeeCount |
|---------------|---------------|
| 2             | 2             |
| 1             | 2             |

2. **Total Salary by Department with a Condition**:

To calculate the total salary of employees in each department but only display departments where the total salary exceeds $140,000:

```sql
SELECT department_id, SUM(salary) AS TotalSalaries
FROM employees
GROUP BY department_id
HAVING SUM(salary) > 140000;
```

**Result**:
| department_id | TotalSalaries |
|---------------|---------------|
| 2             | 152000        |

3. **Average Salary with a Condition**:

To find departments where the average salary of employees is greater than $70,000:

```sql
SELECT department_id, AVG(salary) AS AverageSalary
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 70000;
```

**Result**:
| department_id | AverageSalary |
|---------------|---------------|
| 1             | 72500         |
| 2             | 76000         |

### Key Points to Remember

- **HAVING vs. WHERE**: Use `WHERE` to filter records before grouping and `HAVING` to filter groups after aggregation.
- **Aggregate Functions**: The `HAVING` clause is often used with aggregate functions like `COUNT`, `SUM`, `AVG`, `MAX`, and `MIN`.
- **Order of Execution**: The SQL execution order is important: `FROM` -> `WHERE` -> `GROUP BY` -> `HAVING` -> `SELECT`.

### Conclusion

The `HAVING` clause is a powerful feature in SQL that allows you to apply conditions to aggregated results. It is particularly useful for filtering groups created by the `GROUP BY` clause based on aggregate calculations. Mastering the use of `HAVING` will enhance your ability to perform complex data analysis in MySQL.
