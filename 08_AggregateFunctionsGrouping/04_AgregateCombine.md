### Combining Aggregate Functions with Joins in MySQL

Combining aggregate functions with joins allows you to perform complex data analysis across multiple tables. This approach is useful when you want to summarize data while also retrieving related information from different tables.

### Scenario Example

Let's consider two tables: `employees` and `departments`.

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

### Example Queries

1. **Total Salary by Department**:

To calculate the total salary paid to employees in each department and get the department names, you can use an `INNER JOIN` with the `SUM` aggregate function:

```sql
SELECT d.department_name, SUM(e.salary) AS TotalSalaries
FROM employees AS e
INNER JOIN departments AS d ON e.department_id = d.department_id
GROUP BY d.department_name;
```

**Result**:
| department_name | TotalSalaries |
|------------------|---------------|
| HR               | 145000        |
| IT               | 152000        |
| Sales            | 60000         |

2. **Average Salary by Department**:

To find the average salary of employees in each department:

```sql
SELECT d.department_name, AVG(e.salary) AS AverageSalary
FROM employees AS e
INNER JOIN departments AS d ON e.department_id = d.department_id
GROUP BY d.department_name;
```

**Result**:
| department_name | AverageSalary |
|------------------|---------------|
| HR               | 72500         |
| IT               | 76000         |
| Sales            | 60000         |

3. **Count of Employees by Department**:

To count the number of employees in each department:

```sql
SELECT d.department_name, COUNT(e.employee_id) AS EmployeeCount
FROM employees AS e
INNER JOIN departments AS d ON e.department_id = d.department_id
GROUP BY d.department_name;
```

**Result**:
| department_name | EmployeeCount |
|------------------|---------------|
| HR               | 2             |
| IT               | 2             |
| Sales            | 1             |

### Using Aggregate Functions with LEFT JOIN

If you want to include departments that have no employees (for example, if a department exists but no employees are assigned), you can use a `LEFT JOIN`:

```sql
SELECT d.department_name, COUNT(e.employee_id) AS EmployeeCount
FROM departments AS d
LEFT JOIN employees AS e ON d.department_id = e.department_id
GROUP BY d.department_name;
```

**Result**:
| department_name | EmployeeCount |
|------------------|---------------|
| HR               | 2             |
| IT               | 2             |
| Sales            | 1             |

### Conclusion

Combining aggregate functions with joins is a powerful way to analyze and summarize data from multiple tables. By using joins, you can relate different datasets and apply aggregate functions to extract meaningful insights. Understanding how to effectively use these techniques will greatly enhance your ability to perform data analysis in MySQL.
