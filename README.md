**Module 1: Prerequisites & Basics of SQL**, perfect for beginners who want to learn SQL from scratch — especially focusing on foundations needed for understanding **SQL JOINs** later.

---

 **Module 1: Prerequisites & Basics of SQL**

---

**1. What is a Database and RDBMS?**

**Database**:

A database is an organized collection of data that is stored and accessed electronically.

**RDBMS (Relational Database Management System)**:

An RDBMS is a system for managing **relational databases** where data is stored in **tables** (rows and columns) with relationships between them.

**Examples of RDBMS**:

* MySQL
* PostgreSQL
* Oracle
* SQL Server

---

**2. Introduction to SQL & Its Command Categories**

SQL (Structured Query Language) is used to communicate with databases.

**Main SQL Command Types:**

| Category | Name                         | Examples                     |
| -------- | ---------------------------- | ---------------------------- |
| **DDL**  | Data Definition Language     | `CREATE`, `ALTER`, `DROP`    |
| **DML**  | Data Manipulation Language   | `INSERT`, `UPDATE`, `DELETE` |
| **DQL**  | Data Query Language          | `SELECT`                     |
| **DCL**  | Data Control Language        | `GRANT`, `REVOKE`            |
| **TCL**  | Transaction Control Language | `COMMIT`, `ROLLBACK`         |

**For JOINs**, focus on DDL (table creation) and DQL (`SELECT`).

---

**3. Creating Tables and Inserting Data**

Example: Create two tables

```sql
CREATE TABLE departments (
  dept_id INT PRIMARY KEY,
  dept_name VARCHAR(100)
);

CREATE TABLE employees (
  emp_id INT PRIMARY KEY,
  emp_name VARCHAR(100),
  dept_id INT,
  FOREIGN KEY (dept_id) REFERENCES departments(dept_id)
);
```

#### Inserting sample data:

```sql
INSERT INTO departments VALUES (1, 'IT'), (2, 'HR');

INSERT INTO employees VALUES
(101, 'Alice', 1),
(102, 'Bob', 1),
(103, 'Carol', 2);
```

---

### **4. Basic SELECT Queries**

```sql
-- Select all columns
SELECT * FROM employees;

-- Select specific columns
SELECT emp_name FROM employees;

-- Use WHERE clause
SELECT * FROM employees WHERE dept_id = 1;
```

---

### **5. Primary and Foreign Keys (Important for JOINs)**

#### **Primary Key**:

* Uniquely identifies each row in a table.
* Example: `emp_id` in `employees`

#### **Foreign Key**:

* Creates a link between two tables.
* Example: `dept_id` in `employees` links to `departments`.

This connection between tables is **what enables JOINs**.

---

