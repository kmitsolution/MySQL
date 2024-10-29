### Comparison Operators in MySQL

Comparison operators are used in SQL to compare two values. They are often used in `WHERE` clauses to filter records based on certain conditions. The result of a comparison is a Boolean value (true or false). 

Here’s a list of the most commonly used comparison operators in MySQL:

#### 1. **Equal to (`=`)**

Checks if two values are equal.

**Example**:
Select students with the name "Alice":

```sql
SELECT * FROM students
WHERE student_name = 'Alice';
```

#### 2. **Not Equal to (`<>` or `!=`)**

Checks if two values are not equal.

**Example**:
Select students who are not named "Bob":

```sql
SELECT * FROM students
WHERE student_name <> 'Bob';
```

or

```sql
SELECT * FROM students
WHERE student_name != 'Bob';
```

#### 3. **Greater than (`>`)**

Checks if the left value is greater than the right value.

**Example**:
Select students older than 20:

```sql
SELECT * FROM students
WHERE age > 20;
```

#### 4. **Less than (`<`)**

Checks if the left value is less than the right value.

**Example**:
Select students younger than 18:

```sql
SELECT * FROM students
WHERE age < 18;
```

#### 5. **Greater than or Equal to (`>=`)**

Checks if the left value is greater than or equal to the right value.

**Example**:
Select students who are 18 years old or older:

```sql
SELECT * FROM students
WHERE age >= 18;
```

#### 6. **Less than or Equal to (`<=`)**

Checks if the left value is less than or equal to the right value.

**Example**:
Select students who are 22 years old or younger:

```sql
SELECT * FROM students
WHERE age <= 22;
```

#### 7. **IS NULL**

Checks if a value is NULL (i.e., no value).

**Example**:
Select students who do not have an email address:

```sql
SELECT * FROM students
WHERE email IS NULL;
```

#### 8. **IS NOT NULL**

Checks if a value is not NULL.

**Example**:
Select students who have an email address:

```sql
SELECT * FROM students
WHERE email IS NOT NULL;
```

### Complete Example Using Comparison Operators

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

### Using Comparison Operators

1. **Select students with the name "Alice"**:

    ```sql
    SELECT * FROM students
    WHERE student_name = 'Alice';
    ```

2. **Select students not named "Bob"**:

    ```sql
    SELECT * FROM students
    WHERE student_name <> 'Bob';
    ```

3. **Select students older than 20**:

    ```sql
    SELECT * FROM students
    WHERE age > 20;
    ```

4. **Select students younger than 18**:

    ```sql
    SELECT * FROM students
    WHERE age < 18;
    ```

5. **Select students who are 18 years old or older**:

    ```sql
    SELECT * FROM students
    WHERE age >= 18;
    ```

6. **Select students who are 22 years old or younger**:

    ```sql
    SELECT * FROM students
    WHERE age <= 22;
    ```

7. **Select students who do not have an email address**:

    ```sql
    SELECT * FROM students
    WHERE email IS NULL;
    ```

8. **Select students who have an email address**:

    ```sql
    SELECT * FROM students
    WHERE email IS NOT NULL;
    ```

### Conclusion

Comparison operators are fundamental in SQL for filtering records based on specific conditions. By using operators like `=`, `<>`, `>`, `<`, `>=`, `<=`, `IS NULL`, and `IS NOT NULL`, you can create effective queries to retrieve or manipulate data based on various criteria. Mastering these operators will greatly enhance your ability to work with MySQL and perform complex data retrieval and management tasks.
