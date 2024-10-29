### Constraints in MySQL

Constraints are rules applied to table columns to ensure the integrity and validity of the data. They enforce specific conditions on the data within a table. Here are the most common types of constraints in MySQL, along with examples of each.

#### 1. **NOT NULL Constraint**

The `NOT NULL` constraint ensures that a column cannot have a NULL value. This is useful for fields that must contain data.

**Example**:
```sql
CREATE TABLE students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,  -- 'name' cannot be NULL
    age INT
);
```

#### 2. **UNIQUE Constraint**

The `UNIQUE` constraint ensures that all values in a column are different. It can be applied to one or more columns.

**Example**:
```sql
CREATE TABLE students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    email VARCHAR(100) UNIQUE,  -- 'email' must be unique
    name VARCHAR(100) NOT NULL
);
```

#### 3. **PRIMARY KEY Constraint**

A `PRIMARY KEY` uniquely identifies each record in a table. It cannot contain NULL values and must contain unique values. A table can have only one primary key.

**Example**:
```sql
CREATE TABLE courses (
    course_id INT AUTO_INCREMENT PRIMARY KEY,  -- 'course_id' is the primary key
    course_name VARCHAR(100) NOT NULL
);
```

#### 4. **FOREIGN KEY Constraint**

A `FOREIGN KEY` constraint is used to establish a relationship between two tables. It ensures that the value in one table matches a value in another table, maintaining referential integrity.

**Example**:
```sql
CREATE TABLE enrollments (
    enrollment_id INT AUTO_INCREMENT PRIMARY KEY,
    student_id INT,
    course_id INT,
    FOREIGN KEY (student_id) REFERENCES students(student_id),  -- 'student_id' must exist in 'students'
    FOREIGN KEY (course_id) REFERENCES courses(course_id)      -- 'course_id' must exist in 'courses'
);
```

#### 5. **CHECK Constraint**

The `CHECK` constraint ensures that all values in a column satisfy a specific condition. However, note that not all MySQL versions fully support `CHECK` constraints.

**Example**:
```sql
CREATE TABLE students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    age INT CHECK (age >= 0)  -- 'age' must be non-negative
);
```

#### 6. **DEFAULT Constraint**

The `DEFAULT` constraint provides a default value for a column when no value is specified during record insertion.

**Example**:
```sql
CREATE TABLE students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    enrollment_date DATE DEFAULT CURRENT_DATE  -- Defaults to the current date
);
```

### Summary of Constraints

| Constraint Type | Description                                                |
|------------------|------------------------------------------------------------|
| `NOT NULL`       | Ensures a column cannot have NULL values                   |
| `UNIQUE`         | Ensures all values in a column are different               |
| `PRIMARY KEY`    | Uniquely identifies each record; cannot be NULL            |
| `FOREIGN KEY`    | Ensures that a value in one table matches a value in another table |
| `CHECK`          | Ensures all values in a column satisfy a specific condition|
| `DEFAULT`        | Provides a default value for a column if none is specified  |

### Conclusion

Using constraints in MySQL is essential for maintaining data integrity and ensuring that the data stored in your tables meets specific criteria. By applying constraints appropriately, you can enforce rules on your data and prevent invalid entries, thereby improving the overall quality of your database.
