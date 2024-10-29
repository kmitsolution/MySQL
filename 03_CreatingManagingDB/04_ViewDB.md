### Viewing Existing Databases in MySQL

To view existing databases in MySQL, you use the `SHOW DATABASES;` command. This command lists all databases available on the MySQL server, helping you to identify which databases are available for your operations.

#### Step 1: Connect to MySQL

First, connect to your MySQL server using a client like MySQL Workbench or the command line:

```bash
mysql -u root -p
```

Enter your password when prompted.

#### Step 2: Show Existing Databases

To view all existing databases, execute the following command:

```sql
SHOW DATABASES;
```

This command will return a list of all databases available on the server.

**Example Output**:
```
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| school             |
| library            |
| events             |
+--------------------+
```

### Use Case: Managing a School Management System

#### Scenario

Imagine you are managing a school management system that uses multiple databases for different functionalities: one for student records, another for library management, and another for school events.

#### Example Steps

1. **Connect to MySQL**:
   Start by connecting to your MySQL server:

   ```bash
   mysql -u root -p
   ```

2. **View Existing Databases**:
   After connecting, you can check which databases are available:

   ```sql
   SHOW DATABASES;
   ```

3. **Identify the Relevant Databases**:
   From the output, you may see:
   - `school`: Contains student and course data.
   - `library`: Manages book records.
   - `events`: Stores information about school events.

4. **Select a Database to Work With**:
   If you want to manage student data, you would select the `school` database:

   ```sql
   USE school;
   ```

5. **Perform Operations**:
   After selecting the `school` database, you can run queries to view student records, add new students, or update existing information:

   ```sql
   SELECT * FROM students;  -- View all student records
   ```

### Conclusion

Viewing existing databases in MySQL is a fundamental step in database management. By using the `SHOW DATABASES;` command, you can easily identify and navigate through different databases available on your server. This capability is especially useful in environments with multiple databases, allowing you to manage various functionalities efficiently, such as in a school management system.
