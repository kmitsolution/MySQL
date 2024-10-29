### User-Defined Functions (UDFs) in MySQL

A **User-Defined Function (UDF)** in MySQL is a stored function that allows you to create reusable code blocks to perform calculations, manipulate data, or encapsulate complex logic. UDFs can be used in SQL statements just like built-in MySQL functions.

### Key Features of User-Defined Functions

1. **Reusability**: Functions can be reused across multiple queries and applications, promoting code efficiency.
2. **Encapsulation**: Encapsulate complex logic into a single callable unit, making your SQL queries cleaner and more manageable.
3. **Return Values**: Unlike stored procedures, UDFs always return a single value and can be used in expressions.

### Syntax for Creating a User-Defined Function

```sql
CREATE FUNCTION function_name(parameter1 datatype, parameter2 datatype, ...)
RETURNS return_datatype
BEGIN
    -- SQL statements
    RETURN value;  -- Return a value
END;
```

### Example: Creating a User-Defined Function

#### Use Case: Calculate Yearly Salary

Let's create a UDF to calculate the yearly salary based on an employee's monthly salary.

1. **Creating the Function**:

```sql
DELIMITER //

CREATE FUNCTION CalculateYearlySalary(monthly_salary DECIMAL(10,2))
RETURNS DECIMAL(10,2)
BEGIN
    RETURN monthly_salary * 12;  -- Calculate and return yearly salary
END //

DELIMITER ;
```

**Explanation**:
- The function `CalculateYearlySalary` takes one parameter, `monthly_salary`, and returns the annual salary by multiplying the monthly salary by 12.

2. **Using the Function**:

To use the function in a query, you would call it like any other SQL function:

```sql
SELECT employee_name, CalculateYearlySalary(salary) AS YearlySalary
FROM employees;
```

### Example: Using UDF with Conditional Logic

#### Use Case: Determine Employee Status

Let’s create a UDF to determine if an employee is eligible for a bonus based on their salary.

1. **Creating the Function**:

```sql
DELIMITER //

CREATE FUNCTION IsEligibleForBonus(salary DECIMAL(10,2))
RETURNS VARCHAR(10)
BEGIN
    IF salary >= 80000 THEN
        RETURN 'Yes';
    ELSE
        RETURN 'No';
    END IF;
END //

DELIMITER ;
```

**Explanation**:
- The function `IsEligibleForBonus` checks if the salary is above or equal to $80,000 and returns 'Yes' or 'No'.

2. **Using the Function**:

You can then call this function in a SELECT statement:

```sql
SELECT employee_name, IsEligibleForBonus(salary) AS BonusEligibility
FROM employees;
```

### Dropping a User-Defined Function

If you need to modify or remove a UDF, you can drop it using:

```sql
DROP FUNCTION IF EXISTS function_name;
```

### Conclusion

User-Defined Functions in MySQL are powerful tools for encapsulating logic and performing calculations. They improve code reusability and can simplify complex SQL statements. By understanding how to create and use UDFs, you can enhance your SQL programming capabilities and make your database operations more efficient and organized.
