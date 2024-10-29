### Input and Output Parameters in Stored Procedures

Stored procedures in MySQL can use input and output parameters to facilitate data exchange between the caller and the procedure. Understanding these parameters is crucial for developing effective stored procedures that can perform a variety of operations.

### Input Parameters

**Input parameters** are used to pass values into the stored procedure when it is called. They allow you to provide the procedure with data it needs to perform its operations.

#### Syntax for Input Parameters

```sql
CREATE PROCEDURE procedure_name(IN parameter_name datatype)
BEGIN
    -- SQL statements using parameter_name
END;
```

#### Example: Using Input Parameters

**Use Case**: Create a stored procedure to retrieve employee details based on their ID.

```sql
DELIMITER //

CREATE PROCEDURE GetEmployeeByID(IN emp_id INT)
BEGIN
    SELECT employee_name, department_id, salary
    FROM employees
    WHERE employee_id = emp_id;
END //

DELIMITER ;
```

**Executing the Procedure**:

```sql
CALL GetEmployeeByID(1);
```

**Result**: This would return the details of the employee with ID 1.

### Output Parameters

**Output parameters** are used to return values from the stored procedure back to the caller. They allow the procedure to provide information after its execution.

#### Syntax for Output Parameters

```sql
CREATE PROCEDURE procedure_name(OUT parameter_name datatype)
BEGIN
    -- SQL statements setting value to parameter_name
END;
```

#### Example: Using Output Parameters

**Use Case**: Create a stored procedure to calculate the average salary of employees in a specific department and return it.

```sql
DELIMITER //

CREATE PROCEDURE GetAverageSalary(IN dept_id INT, OUT avg_salary DECIMAL(10,2))
BEGIN
    SELECT AVG(salary) INTO avg_salary
    FROM employees
    WHERE department_id = dept_id;
END //

DELIMITER ;
```

**Executing the Procedure**:

To call the stored procedure and retrieve the output:

```sql
SET @average_salary = 0;
CALL GetAverageSalary(1, @average_salary);
SELECT @average_salary AS AverageSalary;
```

**Result**: This will return the average salary of employees in department 1.

### Using Both Input and Output Parameters

You can also create stored procedures that use both input and output parameters. 

#### Example

**Use Case**: Create a procedure to get the employee details and calculate the percentage increase in salary based on a given percentage.

```sql
DELIMITER //

CREATE PROCEDURE GetEmployeeWithSalaryIncrease(
    IN emp_id INT,
    IN increase_percent DECIMAL(5,2),
    OUT new_salary DECIMAL(10,2)
)
BEGIN
    DECLARE current_salary DECIMAL(10,2);
    
    SELECT salary INTO current_salary
    FROM employees
    WHERE employee_id = emp_id;

    SET new_salary = current_salary + (current_salary * increase_percent / 100);
END //

DELIMITER ;
```

**Executing the Procedure**:

```sql
SET @new_salary = 0;
CALL GetEmployeeWithSalaryIncrease(1, 10, @new_salary);
SELECT @new_salary AS NewSalary;
```

**Result**: This will calculate and return the new salary for the employee with ID 1 after a 10% increase.

### Conclusion

Input and output parameters are powerful features of stored procedures in MySQL that facilitate data exchange between the procedure and the calling context. By effectively using these parameters, you can create more dynamic and flexible stored procedures that cater to various business needs. Understanding how to implement and utilize them can significantly enhance your database programming capabilities.
