### Logical Operators in MySQL

Logical operators are used in SQL to combine multiple conditions in `WHERE` clauses, allowing for more complex queries. The most common logical operators in MySQL are `AND`, `OR`, and `NOT`.

#### 1. **AND Operator**

The `AND` operator is used to combine two or more conditions. All conditions combined with `AND` must be true for the overall expression to be true.

**Syntax**:
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition1 AND condition2;
```

**Example**:
Select students who are older than 18 and have the name "David":

```sql
SELECT * FROM students
WHERE age > 18 AND student_name = 'David';
```

#### 2. **OR Operator**

The `OR` operator is used to combine two or more conditions, where at least one of the conditions must be true for the overall expression to be true.

**Syntax**:
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition1 OR condition2;
```

**Example**:
Select students who are either named "Bob" or younger than 19:

```sql
SELECT * FROM students
WHERE student_name = 'Bob' OR age < 19;
```

#### 3. **NOT Operator**

The `NOT` operator is used to negate a condition. It will return true if the condition is false.

**Syntax**:
```sql
SELECT column1, column2, ...
FROM table_name
WHERE NOT condition;
```

**Example**:
Select students who are not named "Alice":

```sql
SELECT * FROM students
WHERE NOT student_name = 'Alice';
```

#### 4. **Combining Logical Operators**

You can combine multiple logical operators in a single query. When doing so, use parentheses to group conditions and clarify the order of evaluation.

**Example**:
Select students who are either older than 20 or younger than 18, but not named "Bob":

```sql
SELECT * FROM students
WHERE (age > 20 OR age < 18) AND NOT student_name = 'Bob';
```

### Complete Example Using Logical Operators

Assuming you have a `students` table structured as follows:

```sql
CREATE TABLE students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    student_name VARCHAR(100) NOT NULL,
    age INT,
    email VARCHAR(100) UNIQUE
);
```

#### Inserting Sample Data:

```sql
INSERT INTO students (student_name, age, email) VALUES
('Alice', 20, 'alice@example.com'),
('Bob', 17, 'bob@example.com'),
('Charlie', 19, 'charlie@example.com'),
('David', 21, NULL),
('Eva', 22, 'eva@example.com');
```

### Using Logical Operators

1. **Select students older than 18 and named "David"**:

    ```sql
    SELECT * FROM students
    WHERE age > 18 AND student_name = 'David';
    ```

2. **Select students either named "Bob" or younger than 20**:

    ```sql
    SELECT * FROM students
    WHERE student_name = 'Bob' OR age < 20;
    ```

3. **Select students who are not 19 years old**:

    ```sql
    SELECT * FROM students
    WHERE NOT age = 19;
    ```

4. **Select students who are older than 18 but not named "Alice"**:

    ```sql
    SELECT * FROM students
    WHERE age > 18 AND NOT student_name = 'Alice';
    ```

5. **Select students who are either older than 20 or younger than 18, but not named "Bob"**:

    ```sql
    SELECT * FROM students
    WHERE (age > 20 OR age < 18) AND NOT student_name = 'Bob';
    ```

### Conclusion

Logical operators are essential for building complex queries in MySQL. By understanding how to use `AND`, `OR`, and `NOT`, you can refine your data retrieval and manipulation, making your SQL queries more powerful and versatile. Combining these operators effectively will enable you to handle a wide range of scenarios in database operations.
