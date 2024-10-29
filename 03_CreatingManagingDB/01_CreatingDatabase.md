### Creating Databases in MySQL

Creating a database in MySQL is a straightforward process that involves using the `CREATE DATABASE` statement. Here’s a step-by-step guide along with an example and a use case.

#### Step 1: Connect to MySQL

Before creating a database, you need to connect to your MySQL server using a client like MySQL Workbench or the command line.

```bash
mysql -u root -p
```

You'll be prompted to enter your password.

#### Step 2: Create a Database

To create a new database, use the `CREATE DATABASE` command followed by the name of the database. 

**Syntax**:
```sql
CREATE DATABASE database_name;
```

**Example**:
Let's create a database named `school`.

```sql
CREATE DATABASE school;
```

#### Step 3: Verify the Database Creation

To confirm that the database was created, you can list all databases with the following command:

```sql
SHOW DATABASES;
```

You should see `school` in the list of databases.

#### Step 4: Use the Database

To start using the new database, use the `USE` command:

```sql
USE school;
```

### Use Case: School Management System

#### Scenario

Consider a school management system that needs to manage data related to students, courses, and enrollments. Here’s how you might use the `school` database:

1. **Tables Needed**:
   - **Students**: To store student information.
   - **Courses**: To store course details.
   - **Enrollments**: To track which students are enrolled in which courses.

#### Step 5: Creating Tables

After creating the `school` database, you can create tables to hold the necessary data.

**Creating the Students Table**:
```sql
CREATE TABLE students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    age INT,
    email VARCHAR(100)
);
```

**Creating the Courses Table**:
```sql
CREATE TABLE courses (
    course_id INT AUTO_INCREMENT PRIMARY KEY,
    course_name VARCHAR(100) NOT NULL,
    credits INT
);
```

**Creating the Enrollments Table**:
```sql
CREATE TABLE enrollments (
    enrollment_id INT AUTO_INCREMENT PRIMARY KEY,
    student_id INT,
    course_id INT,
    FOREIGN KEY (student_id) REFERENCES students(student_id),
    FOREIGN KEY (course_id) REFERENCES courses(course_id)
);
```

### Example Queries

1. **Inserting Data**:
   Insert some students and courses into the tables.

   ```sql
   INSERT INTO students (name, age, email) VALUES ('Alice', 20, 'alice@example.com');
   INSERT INTO students (name, age, email) VALUES ('Bob', 22, 'bob@example.com');

   INSERT INTO courses (course_name, credits) VALUES ('Mathematics', 3);
   INSERT INTO courses (course_name, credits) VALUES ('Physics', 4);
   ```

2. **Enrolling Students in Courses**:
   Enroll students in courses using the `enrollments` table.

   ```sql
   INSERT INTO enrollments (student_id, course_id) VALUES (1, 1);  -- Alice enrolls in Mathematics
   INSERT INTO enrollments (student_id, course_id) VALUES (2, 2);  -- Bob enrolls in Physics
   ```

### Conclusion

By creating a database like `school`, you can effectively manage student and course information in a structured manner. This use case illustrates how to set up a database, define relationships among tables, and perform basic operations. Creating databases is foundational in building applications that require data management, making it a critical skill for developers and database administrators.
