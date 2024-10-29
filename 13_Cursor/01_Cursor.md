### Cursors in MySQL

A **cursor** in MySQL is a database object that allows you to retrieve and manipulate data row by row, rather than processing a set of rows all at once. Cursors are particularly useful when you need to perform complex operations on a result set that requires multiple steps or when you want to manage the data incrementally.

### Key Features of Cursors

1. **Row-by-Row Processing**: Cursors enable you to process each row returned by a query individually.
2. **Control Over Data**: They provide greater control over data processing and allow for complex operations that cannot be easily handled in a single SQL statement.
3. **Read and Modify Data**: Cursors can be used to read data, and with the appropriate permissions, they can also be used to update or delete rows.

### Types of Cursors

1. **Implicit Cursors**: Automatically created by MySQL for single SQL statements. No explicit declaration is needed, and they are used internally.
2. **Explicit Cursors**: Explicitly defined by the user for a specific SQL statement and allow for more control over the data retrieval process.

### Syntax for Creating and Using Cursors

Here’s a step-by-step guide on how to create and use explicit cursors in MySQL.

#### 1. Declaring a Cursor

```sql
DECLARE cursor_name CURSOR FOR select_statement;
```

#### 2. Opening the Cursor

```sql
OPEN cursor_name;
```

#### 3. Fetching Data from the Cursor

```sql
FETCH cursor_name INTO variable1, variable2, ...;
```

#### 4. Closing the Cursor

```sql
CLOSE cursor_name;
```

#### 5. Deallocating the Cursor

```sql
DEALLOCATE PREPARE cursor_name;
```

### Example: Using Cursors

#### Use Case: Process Employee Salaries

Let’s create a stored procedure that uses a cursor to process employee salaries and give a raise to each employee.

Your stored procedure `RaiseEmployeeSalaries()` is well-structured for processing employee salary updates using a cursor. Let's walk through the entire process, including creating the `employees` table, inserting records, and executing the procedure.

### Step 1: Create the Employees Table

First, we will create the `employees` table:

```sql
CREATE TABLE employees (
    employee_id INT AUTO_INCREMENT PRIMARY KEY,
    employee_name VARCHAR(100),
    salary DECIMAL(10, 2)
);
```

### Step 2: Insert Records into the Table

Next, let's insert some sample records into the `employees` table:

```sql
INSERT INTO employees (employee_name, salary) VALUES
('Alice', 50000),
('Bob', 60000),
('Charlie', 70000),
('Diana', 80000);
```

### Step 3: Create the RaiseEmployeeSalaries Procedure

Now, we can use your cursor-based procedure to raise employee salaries by 10%. You've already provided the procedure code, but just for clarity, here it is again:

```sql
DELIMITER //

CREATE PROCEDURE RaiseEmployeeSalaries()
BEGIN
    DECLARE done INT DEFAULT FALSE;
    DECLARE emp_id INT;
    DECLARE emp_salary DECIMAL(10,2);
    
    -- Declare the cursor
    DECLARE employee_cursor CURSOR FOR 
        SELECT employee_id, salary FROM employees;

    -- Declare a handler for the end of the cursor
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = TRUE;

    -- Open the cursor
    OPEN employee_cursor;

    -- Loop through the cursor
    read_loop: LOOP
        -- Fetch data into variables
        FETCH employee_cursor INTO emp_id, emp_salary;
        
        IF done THEN
            LEAVE read_loop;
        END IF;

        -- Give a 10% raise
        UPDATE employees
        SET salary = emp_salary * 1.10
        WHERE employee_id = emp_id;
    END LOOP;

    -- Close the cursor
    CLOSE employee_cursor;
END //

DELIMITER ;
```

### Step 4: Execute the Procedure

Now, you can call the procedure to apply the salary raises:

```sql
CALL RaiseEmployeeSalaries();
```

### Step 5: Verify the Salary Updates

To verify that the salaries have been updated, you can run a simple `SELECT` query:

```sql
SELECT * FROM employees;
```

This should show the updated salaries, reflecting the 10% increase.

### Complete Example

Putting it all together, here’s the complete SQL script:

```sql
-- Step 1: Create the employees table
CREATE TABLE employees (
    employee_id INT AUTO_INCREMENT PRIMARY KEY,
    employee_name VARCHAR(100),
    salary DECIMAL(10, 2)
);

-- Step 2: Insert records into the table
INSERT INTO employees (employee_name, salary) VALUES
('Alice', 50000),
('Bob', 60000),
('Charlie', 70000),
('Diana', 80000);

-- Step 3: Create the RaiseEmployeeSalaries procedure
DELIMITER //

CREATE PROCEDURE RaiseEmployeeSalaries()
BEGIN
    DECLARE done INT DEFAULT FALSE;
    DECLARE emp_id INT;
    DECLARE emp_salary DECIMAL(10,2);
    
    -- Declare the cursor
    DECLARE employee_cursor CURSOR FOR 
        SELECT employee_id, salary FROM employees;

    -- Declare a handler for the end of the cursor
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = TRUE;

    -- Open the cursor
    OPEN employee_cursor;

    -- Loop through the cursor
    read_loop: LOOP
        -- Fetch data into variables
        FETCH employee_cursor INTO emp_id, emp_salary;
        
        IF done THEN
            LEAVE read_loop;
        END IF;

        -- Give a 10% raise
        UPDATE employees
        SET salary = emp_salary * 1.10
        WHERE employee_id = emp_id;
    END LOOP;

    -- Close the cursor
    CLOSE employee_cursor;
END //

DELIMITER ;

-- Step 4: Execute the procedure to raise salaries
CALL RaiseEmployeeSalaries();

-- Step 5: Verify the salary updates
SELECT * FROM employees;
```

### Conclusion

This complete example shows how to create a table, insert records, define a stored procedure with a cursor, and execute it to update employee salaries. Feel free to modify the procedure or data as needed for your specific requirements!
### Advantages of Using Cursors

1. **Fine-Grained Control**: Cursors provide the ability to handle data one row at a time, which can be essential for complex logic.
2. **Flexibility**: They allow for complex operations that may not be feasible with set-based operations alone.
3. **Iterative Processing**: Useful for scenarios where operations need to be performed on each row independently.

### Disadvantages of Using Cursors

1. **Performance**: Cursors can be slower than set-based operations, especially with large data sets, due to their row-by-row processing.
2. **Resource Consumption**: They consume more server resources, which can impact performance in high-concurrency environments.

### Conclusion

Cursors are a powerful feature in MySQL for processing data row by row, allowing for complex data manipulation and control. While they provide flexibility and fine-grained control, they should be used judiciously due to potential performance implications. Understanding when and how to use cursors effectively can greatly enhance your database programming capabilities.
