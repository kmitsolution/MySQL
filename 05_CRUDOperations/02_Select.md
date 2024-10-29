### Querying Data in MySQL

Querying data is essential for retrieving information from a database. In MySQL, the primary tool for querying data is the `SELECT` statement, which allows you to specify the data you want to retrieve. You can refine your queries using various clauses, such as `WHERE`, `ORDER BY`, and `LIMIT`.

#### Step 1: Connect to MySQL

First, connect to your MySQL server:

```bash
mysql -u root -p
```

Enter your password when prompted.

#### Step 2: Select the Database

Select the database you want to work with:

```sql
USE school;
```

### 1. **SELECT Statement**

The `SELECT` statement is used to specify which columns you want to retrieve from a table.

**Syntax**:
```sql
SELECT column1, column2, ...
FROM table_name;
```

**Example**:
To select all students from the `students` table:

```sql
SELECT * FROM students;  -- Selects all columns
```

To select specific columns (e.g., `student_name` and `email`):

```sql
SELECT student_name, email FROM students;
```

### 2. **WHERE Clause**

The `WHERE` clause is used to filter records based on specific conditions.

**Syntax**:
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

**Example**:
To select students older than 18:

```sql
SELECT * FROM students
WHERE age > 18;
```

To find a specific student by name:

```sql
SELECT * FROM students
WHERE student_name = 'Alice';
```

### 3. **ORDER BY Clause**

The `ORDER BY` clause is used to sort the result set based on one or more columns.

**Syntax**:
```sql
SELECT column1, column2, ...
FROM table_name
ORDER BY column1 [ASC|DESC], column2 [ASC|DESC];
```

**Example**:
To sort students by age in ascending order:

```sql
SELECT * FROM students
ORDER BY age ASC;
```

To sort by name in descending order:

```sql
SELECT * FROM students
ORDER BY student_name DESC;
```

### 4. **LIMIT Clause**

The `LIMIT` clause is used to specify the maximum number of records to return.

**Syntax**:
```sql
SELECT column1, column2, ...
FROM table_name
LIMIT number;
```

**Example**:
To retrieve only the first 3 students:

```sql
SELECT * FROM students
LIMIT 3;
```

### 5. **Combining Clauses**

You can combine the `WHERE`, `ORDER BY`, and `LIMIT` clauses to refine your queries further.

**Example**:
To select the top 5 oldest students:

```sql
SELECT * FROM students
WHERE age > 18
ORDER BY age DESC
LIMIT 5;
```

### 6. **SELECT INTO Statement**

The `SELECT INTO` statement allows you to select data from one table and insert it into another table.

**Syntax**:
```sql
CREATE TABLE new_table AS
SELECT column1, column2, ...
FROM source_table
WHERE condition;
```

**Example**:
Suppose you want to create a new table, `adult_students`, that contains all students older than 18:

```sql
CREATE TABLE adult_students AS
SELECT student_id, student_name, age, email
FROM students
WHERE age > 18;
```

### Complete Example

Here’s a complete example that combines various aspects of querying data:

1. **Creating the `students` Table** (if it doesn't already exist):

```sql
CREATE TABLE students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    student_name VARCHAR(100) NOT NULL,
    age INT,
    email VARCHAR(100) UNIQUE
);
```

2. **Inserting Sample Data**:

```sql
INSERT INTO students (student_name, age, email) VALUES
('Alice', 20, 'alice@example.com'),
('Bob', 17, 'bob@example.com'),
('Charlie', 19, 'charlie@example.com'),
('David', 21, 'david@example.com'),
('Eva', 22, 'eva@example.com');
```

3. **Querying Data**:

- Select all students:
    ```sql
    SELECT * FROM students;
    ```

- Select students older than 18:
    ```sql
    SELECT * FROM students WHERE age > 18;
    ```

- Order students by name in descending order:
    ```sql
    SELECT * FROM students ORDER BY student_name DESC;
    ```

- Limit results to the first 3 students:
    ```sql
    SELECT * FROM students LIMIT 3;
    ```

- Select the top 3 oldest students:
    ```sql
    SELECT * FROM students WHERE age > 18 ORDER BY age DESC LIMIT 3;
    ```

- Create a new table for students older than 18:
    ```sql
    CREATE TABLE adult_students AS SELECT * FROM students WHERE age > 18;
    ```

### Conclusion

Querying data in MySQL using the `SELECT` statement, along with clauses like `WHERE`, `ORDER BY`, and `LIMIT`, enables you to retrieve and manage your data effectively. By understanding how to combine these features, you can perform complex queries and create new tables based on your selection criteria, enhancing your database management capabilities.
