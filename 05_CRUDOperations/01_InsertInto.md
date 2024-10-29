### Inserting Data into MySQL Tables

Inserting data into MySQL tables is done using the `INSERT` statement. This allows you to add new records to a table. Here’s how to do it effectively, along with examples.

#### Step 1: Connect to MySQL

First, connect to your MySQL server:

```bash
mysql -u root -p
```

Enter your password when prompted.

#### Step 2: Select the Database

Select the database that contains the table you want to insert data into:

```sql
USE school;
```

### Inserting Data

#### 1. **Inserting a Single Row**

To insert a single row of data into a table, use the `INSERT INTO` statement with the column names and the corresponding values.

**Syntax**:
```sql
INSERT INTO table_name (column1, column2, column3, ...) VALUES (value1, value2, value3, ...);
```

**Example**:
Let’s insert a new student into the `students` table:

```sql
INSERT INTO students (student_id, student_name, age, email) VALUES (1, 'Alice', 20, 'alice@example.com');
```

#### 2. **Inserting Multiple Rows**

You can also insert multiple rows in a single `INSERT` statement by separating each set of values with a comma.

**Syntax**:
```sql
INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...), (value3, value4, ...);
```

**Example**:
Let’s insert multiple students at once:

```sql
INSERT INTO students (student_id, student_name, age, email) VALUES 
(2, 'Bob', 22, 'bob@example.com'),
(3, 'Charlie', 19, 'charlie@example.com');
```

#### 3. **Inserting Data with Auto-Increment**

If a table has an auto-increment primary key, you can omit the primary key column in your `INSERT` statement. MySQL will automatically generate the next value.

**Example**:
Assuming `student_id` is auto-incremented, you can insert a new student like this:

```sql
INSERT INTO students (student_name, age, email) VALUES ('David', 21, 'david@example.com');
```

#### 4. **Inserting Data with Default Values**

If you have columns with default values, you can omit those columns in your `INSERT` statement, and MySQL will use the default value.

**Example**:
Let’s say the `enrollment_date` column has a default value of the current date. You can insert a student without specifying this column:

```sql
INSERT INTO students (student_name, age, email) VALUES ('Eva', 20, 'eva@example.com');
```

### Example: Complete Data Insertion

Here’s a complete example of inserting data into the `students` table:

```sql
-- Insert a single student
INSERT INTO students (student_name, age, email) VALUES ('Alice', 20, 'alice@example.com');

-- Insert multiple students
INSERT INTO students (student_name, age, email) VALUES 
('Bob', 22, 'bob@example.com'),
('Charlie', 19, 'charlie@example.com'),
('David', 21, 'david@example.com');

-- Insert with auto-increment (assuming student_id is auto-incremented)
INSERT INTO students (student_name, age, email) VALUES ('Eva', 20, 'eva@example.com');
```

### Inserting Data from One Table to Another in MySQL

You can insert data into a table from another table using the `INSERT INTO ... SELECT` statement. This method allows you to copy rows from one table and insert them into another, which is particularly useful for data migration or consolidation.

#### Step 1: Connect to MySQL

First, connect to your MySQL server:

```bash
mysql -u root -p
```

Enter your password when prompted.

#### Step 2: Select the Database

Select the database that contains the tables you want to work with:

```sql
USE school;
```

### Inserting Data from One Table to Another

#### Syntax

The syntax for inserting data from one table to another is:

```sql
INSERT INTO target_table (column1, column2, ...)
SELECT column1, column2, ...
FROM source_table
WHERE condition;  -- Optional
```

- **`target_table`**: The table where you want to insert the data.
- **`source_table`**: The table from which you are selecting data.
- **`condition`**: Optional. You can specify a condition to filter which rows to copy.

#### Example

Assuming you have two tables: `students` and `new_students`, and you want to copy students from `new_students` to `students`.

**Table Structure**:
- **`students`**: `student_id`, `student_name`, `age`, `email`
- **`new_students`**: `student_name`, `age`, `email` (no `student_id` since it is auto-incremented)

**Example SQL Statement**:

```sql
INSERT INTO students (student_name, age, email)
SELECT student_name, age, email
FROM new_students;
```

### Inserting with Conditions

You can also add a `WHERE` clause to filter which records to insert. For example, if you only want to insert students older than 18:

```sql
INSERT INTO students (student_name, age, email)
SELECT student_name, age, email
FROM new_students
WHERE age > 18;
```

### Complete Example

Here's a complete flow of inserting data from one table to another:

1. **Creating the Tables** (if they don't already exist):

```sql
CREATE TABLE students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    student_name VARCHAR(100) NOT NULL,
    age INT,
    email VARCHAR(100) UNIQUE
);

CREATE TABLE new_students (
    student_name VARCHAR(100) NOT NULL,
    age INT,
    email VARCHAR(100) UNIQUE
);
```

2. **Inserting Data into `new_students`**:

```sql
INSERT INTO new_students (student_name, age, email) VALUES
('Alice', 20, 'alice@example.com'),
('Bob', 17, 'bob@example.com'),
('Charlie', 19, 'charlie@example.com');
```

3. **Inserting Data from `new_students` to `students`**:

```sql
INSERT INTO students (student_name, age, email)
SELECT student_name, age, email
FROM new_students;
```

### Conclusion

Using the `INSERT INTO ... SELECT` statement allows you to efficiently copy data between tables in MySQL. This approach is useful for migrating data, consolidating records, or transferring data based on specific conditions. By leveraging this functionality, you can streamline data management tasks and maintain an organized database structure.
