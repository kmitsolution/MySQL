### Creating and Executing Stored Procedures in MySQL

Stored procedures are essential for encapsulating business logic and simplifying complex SQL operations. Below, we’ll walk through the process of creating, executing, and managing stored procedures in MySQL.

### Creating a Stored Procedure

#### Basic Syntax

The syntax for creating a stored procedure is as follows:

```sql
DELIMITER //

CREATE PROCEDURE procedure_name (IN parameter_name datatype, ...)
BEGIN
    -- SQL statements
END //

DELIMITER ;
```

**Key Components**:
- **DELIMITER**: Changes the statement delimiter to allow for multi-statement blocks.
- **CREATE PROCEDURE**: Begins the definition of the stored procedure.
- **IN**: Indicates that the parameter is an input parameter.

### Example: Creating a Stored Procedure

#### Use Case: Insert a New Employee

Let's create a stored procedure to insert a new employee into the `employees` table.

1. **Table Structure**:

Assuming you have the following `employees` table:

**employees**:
| employee_id | employee_name | department_id | salary |
|-------------|---------------|---------------|--------|
| 1           | Alice         | 1             | 70000  |
| 2           | Bob           | 2             | 80000  |

2. **Creating the Stored Procedure**:

```sql
DELIMITER //

CREATE PROCEDURE AddEmployee(
    IN emp_name VARCHAR(50),
    IN dept_id INT,
    IN emp_salary DECIMAL(10, 2)
)
BEGIN
    INSERT INTO employees (employee_name, department_id, salary)
    VALUES (emp_name, dept_id, emp_salary);
END //

DELIMITER ;
```

**Explanation**:
- This procedure, `AddEmployee`, takes three parameters: `emp_name`, `dept_id`, and `emp_salary`.
- It inserts a new employee into the `employees` table using these parameters.

### Executing a Stored Procedure

To execute a stored procedure, you use the `CALL` statement:

```sql
CALL AddEmployee('Charlie', 1, 75000);
```

**Explanation**: This command adds a new employee named Charlie in department 1 with a salary of $75,000.

### Viewing Stored Procedures

To see the stored procedures in your database, you can use:

```sql
SHOW PROCEDURE STATUS;
```

### Updating a Stored Procedure

If you need to modify an existing stored procedure, you cannot directly alter it. Instead, you should drop it and create it again:

1. **Dropping the Procedure**:

```sql
DROP PROCEDURE IF EXISTS AddEmployee;
```

2. **Recreating the Procedure** (with changes, if necessary):

```sql
DELIMITER //

CREATE PROCEDURE AddEmployee(
    IN emp_name VARCHAR(50),
    IN dept_id INT,
    IN emp_salary DECIMAL(10, 2)
)
BEGIN
    INSERT INTO employees (employee_name, department_id, salary)
    VALUES (emp_name, dept_id, emp_salary);
END //

DELIMITER ;
```

### Error Handling

You can add error handling within stored procedures using `DECLARE` and `HANDLER` statements:

```sql
DELIMITER //

CREATE PROCEDURE AddEmployeeWithErrorHandling(
    IN emp_name VARCHAR(50),
    IN dept_id INT,
    IN emp_salary DECIMAL(10, 2)
)
BEGIN
    DECLARE CONTINUE HANDLER FOR SQLEXCEPTION
    BEGIN
        -- Handle the error (e.g., log it or return an error message)
        SELECT 'Error occurred while inserting employee.' AS ErrorMessage;
    END;

    INSERT INTO employees (employee_name, department_id, salary)
    VALUES (emp_name, dept_id, emp_salary);
END //

DELIMITER ;
```

### Conclusion

Creating and executing stored procedures in MySQL allows for encapsulated logic, improved performance, and better maintainability of database operations. By understanding how to create, execute, and manage stored procedures, you can significantly enhance your database application development.
