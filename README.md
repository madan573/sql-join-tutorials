**Prerequisites & Basics of SQL**, perfect for beginners who want to learn SQL from scratch — especially focusing on foundations needed for understanding **SQL JOINs** later.

---

## **Module 1: Prerequisites & Basics of SQL**

---
### **1. What is a Database and RDBMS?**

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
### **2. Introduction to SQL & Its Command Categories**
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

### **3. Creating Tables and Inserting Data**
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
##  **Module 2: Introduction to SQL JOINs**
---
### **1. What is a JOIN?**

A **JOIN** in SQL is used to **combine rows from two or more tables** based on a related column between them.
Think of it as **connecting tables** like puzzle pieces using a common field (e.g., `dept_id` in both `departments` and `employees`).

---
### **2. Why JOIN is Used?**
Databases are **normalized** — data is split across multiple tables to reduce redundancy.
**JOINs are used to:**
* Fetch **complete information** by combining related data.
* Run **powerful queries** across multiple tables.
* Maintain **data integrity** without repeating data.

####  Example:
Two tables:
**employees**

| emp\_id | emp\_name | dept\_id |
| ------- | --------- | -------- |
| 101     | Madan     | 1        |
| 102     | Sam       | 2        |

**departments**

| dept\_id | dept\_name |
| -------- | ---------- |
| 1        | IT         |
| 2        | HR         |

 A JOIN lets you combine them to see:
```sql
emp_name | dept_name
---------|----------
madan    | IT
bhandari | HR
```
---

###  **3. Syntax of JOINs**
####  General JOIN Syntax:
```sql
SELECT columns
FROM table1
JOIN table2
ON table1.common_field = table2.common_field;
```
##### Example:

```sql
SELECT e.emp_name, d.dept_name
FROM employees e
JOIN departments d
ON e.dept_id = d.dept_id;
```
Here, `dept_id` is the **foreign key** in `employees` and **primary key** in `departments`.

---
### **4. Types of Relationships in Tables**
#### **One-to-One (1:1)**
Each row in Table A is related to **one and only one** row in Table B.
→ Rare in practice.

#### **One-to-Many (1\:N)**
One row in Table A relates to **many rows** in Table B.
→ Most common relationship.
**Example:** One department has many employees.

#### **Many-to-Many (M\:N)**
Many rows in Table A relate to many rows in Table B.
→ Requires a **junction table**.
**Example:** Students and Courses (a student can take many courses, a course has many students)

---
##  **Module 3: INNER JOIN**

---
###  **1. Concept of INNER JOIN**
**INNER JOIN** returns **only the matching rows** from two or more tables based on a given condition.
It **excludes** rows that don’t have a match in both tables.

---
#### Example Use Case:
You want to list employees **with their department names** — but only those who are **assigned to a department**.

---
### **2. Syntax and Usage**
#### Basic INNER JOIN Syntax:
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```
#### Aliased Version (often used):
```sql
SELECT e.emp_name, d.dept_name
FROM employees e
INNER JOIN departments d
ON e.dept_id = d.dept_id;
```

---
### **3. Examples with Two Tables**
#### Example Tables:
**employees**

| emp\_id | emp\_name | dept\_id |
| ------- | --------- | -------- |
| 101     | Madan     | 1        |
| 102     | Sam       | 2        |
| 103     | Bhandari  | NULL     |

**departments**

| dept\_id | dept\_name |
| -------- | ---------- |
| 1        | IT         |
| 2        | HR         |

### Query:
```sql
SELECT e.emp_name, d.dept_name
FROM employees e
INNER JOIN departments d
ON e.dept_id = d.dept_id;
```
#### Result:
| emp\_name | dept\_name |
| --------- | ---------- |
| Madan     | IT         |
| Sam       | HR         |

Note: **bhandari** is not shown because her `dept_id` is `NULL`.

---
### **4. Filtering with WHERE Clause**
You can add conditions after the JOIN using `WHERE`:
```sql
SELECT e.emp_name, d.dept_name
FROM employees e
INNER JOIN departments d ON e.dept_id = d.dept_id
WHERE d.dept_name = 'IT';
```
Result:
| emp\_name | dept\_name |
| --------- | ---------- |
| Madan     | IT         |

---
### **5. INNER JOIN with More than Two Tables**
You can **chain INNER JOINs** to combine 3 or more tables.
#### Tables:
* `employees`
* `departments`
* `locations`

```sql
SELECT e.emp_name, d.dept_name, l.city
FROM employees e
INNER JOIN departments d ON e.dept_id = d.dept_id
INNER JOIN locations l ON d.location_id = l.location_id;
```
## **Practice Set: INNER JOIN**

---
### **1. Employees & Departments**
#### Tables:
##### **departments**

```sql
CREATE TABLE departments (
  dept_id INT PRIMARY KEY,
  dept_name VARCHAR(50)
);
```
##### **employees**
```sql
CREATE TABLE employees (
  emp_id INT PRIMARY KEY,
  emp_name VARCHAR(50),
  dept_id INT,
  FOREIGN KEY (dept_id) REFERENCES departments(dept_id)
);
```
#### Sample Data:
```sql
INSERT INTO departments VALUES
(1, 'IT'),
(2, 'HR'),
(3, 'Finance');

INSERT INTO employees VALUES
(101, 'Alice', 1),
(102, 'Bob', 1),
(103, 'Carol', 2),
(104, 'David', NULL);
```

####  Practice Queries:
1. **List employee names and their department names**:
```sql
SELECT e.emp_name, d.dept_name
FROM employees e
INNER JOIN departments d ON e.dept_id = d.dept_id;
```

2. **List employees working in the 'IT' department**:
```sql
SELECT e.emp_name
FROM employees e
INNER JOIN departments d ON e.dept_id = d.dept_id
WHERE d.dept_name = 'IT';
```
3. **Count how many employees are in each department**:
```sql
SELECT d.dept_name, COUNT(e.emp_id) AS total_employees
FROM employees e
INNER JOIN departments d ON e.dept_id = d.dept_id
GROUP BY d.dept_name;
```

---

### **2. Students & Courses**
#### Tables:
##### **courses**
```sql
CREATE TABLE courses (
  course_id INT PRIMARY KEY,
  course_name VARCHAR(100)
);
```
##### **students**
```sql
CREATE TABLE students (
  student_id INT PRIMARY KEY,
  student_name VARCHAR(100)
);
```
##### **enrollments** (junction table for many-to-many)
```sql
CREATE TABLE enrollments (
  student_id INT,
  course_id INT,
  FOREIGN KEY (student_id) REFERENCES students(student_id),
  FOREIGN KEY (course_id) REFERENCES courses(course_id)
);
```
#### Sample Data:
```sql
INSERT INTO students VALUES
(1, 'Aarav'),
(2, 'Sita'),
(3, 'Ram');

INSERT INTO courses VALUES
(101, 'Math'),
(102, 'Science'),
(103, 'English');

INSERT INTO enrollments VALUES
(1, 101),
(1, 102),
(2, 103),
(3, 101);
```
#### Practice Queries:
1. **List all students with the courses they are enrolled in**:
```sql
SELECT s.student_name, c.course_name
FROM enrollments e
INNER JOIN students s ON e.student_id = s.student_id
INNER JOIN courses c ON e.course_id = c.course_id;
```
2. **List students who are enrolled in ‘Math’**:
```sql
SELECT s.student_name
FROM enrollments e
INNER JOIN students s ON e.student_id = s.student_id
INNER JOIN courses c ON e.course_id = c.course_id
WHERE c.course_name = 'Math';
```
3. **Count how many students are in each course**:
```sql
SELECT c.course_name, COUNT(e.student_id) AS student_count
FROM enrollments e
INNER JOIN courses c ON e.course_id = c.course_id
GROUP BY c.course_name;
```
## **Module 4: LEFT JOIN (or LEFT OUTER JOIN)**

---
### **1. Understanding LEFT JOIN Logic**

A **LEFT JOIN** returns:
* All records from the **left table**
* Matching records from the **right table**
* If there's **no match**, NULLs are returned for right table columns.

#### Visualize:
```
LEFT TABLE:  ✔️✔️✔️✔️
RIGHT TABLE:    ✔️  ✔️

Result:         ✔️✔️❌✔️ (NULLs shown where no match)
```

---
### **2. Difference Between INNER JOIN and LEFT JOIN**

| Feature       | INNER JOIN                        | LEFT JOIN (LEFT OUTER JOIN)       |
| ------------- | --------------------------------- | --------------------------------- |
| Returns rows  | Only matching rows in both tables | All rows from left + matched rows |
| Missing match | Row is **excluded**               | Row is **included with NULLs**    |
| Use case      | When both sides must have data    | When left-side data is primary    |

---
#### Example
##### **Tables:**
**departments**
| dept\_id | dept\_name |
| -------- | ---------- |
| 1        | IT         |
| 2        | HR         |
| 3        | Finance    |
| 4        | Admin      |

**employees**
| emp\_id | emp\_name | dept\_id |
| ------- | --------- | -------- |
| 101     | Alice     | 1        |
| 102     | Bob       | 2        |
| 103     | Carol     | NULL     |

---
#### INNER JOIN:
```sql
SELECT e.emp_name, d.dept_name
FROM employees e
INNER JOIN departments d ON e.dept_id = d.dept_id;
```
**Result**:
| emp\_name | dept\_name |
| --------- | ---------- |
| Alice     | IT         |
| Bob       | HR         |

Carol is **not shown** (no matching dept)
---
#### LEFT JOIN:
```sql
SELECT e.emp_name, d.dept_name
FROM employees e
LEFT JOIN departments d ON e.dept_id = d.dept_id;
```
**Result**:
| emp\_name | dept\_name |
| --------- | ---------- |
| Alice     | IT         |
| Bob       | HR         |
| Carol     | NULL       |

Carol is included — `dept_name` is NULL since there’s no matching department.
---

### **3. Handling NULL Values**
When using LEFT JOIN, you often get `NULL` values for non-matching right table data.
#### Common techniques:
* Use `IS NULL` to **filter unmatched**:

  ```sql
  SELECT e.emp_name
  FROM employees e
  LEFT JOIN departments d ON e.dept_id = d.dept_id
  WHERE d.dept_id IS NULL;
  ```
This finds employees **without any department**.
* Use `COALESCE()` to **replace NULLs**:
  ```sql
  SELECT e.emp_name, COALESCE(d.dept_name, 'No Department') AS dept
  FROM employees e
  LEFT JOIN departments d ON e.dept_id = d.dept_id;
  ```

---
### **4. Real-World Examples of LEFT JOIN**
#### Example 1: Students with or without enrollment
```sql
SELECT s.student_name, c.course_name
FROM students s
LEFT JOIN enrollments e ON s.student_id = e.student_id
LEFT JOIN courses c ON e.course_id = c.course_id;
```
* This shows **all students**, even those **not enrolled** in any course.

---
#### Example 2: Orders with or without shipping details
```sql
SELECT o.order_id, s.ship_date
FROM orders o
LEFT JOIN shipping s ON o.order_id = s.order_id;
```
* View all orders, including ones that are **not yet shipped**.

---
## **Practice Set: LEFT JOIN**

---
### **1. Customers & Orders**
#### Tables:
##### **customers**
```sql
CREATE TABLE customers (
  customer_id INT PRIMARY KEY,
  customer_name VARCHAR(100)
);
```
##### **orders**
```sql
CREATE TABLE orders (
  order_id INT PRIMARY KEY,
  customer_id INT,
  order_date DATE,
  FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);
```
#### Sample Data:
```sql
INSERT INTO customers VALUES
(1, 'John'),
(2, 'Emma'),
(3, 'Ravi'),
(4, 'Laxmi');

INSERT INTO orders VALUES
(101, 1, '2024-01-15'),
(102, 2, '2024-02-10'),
(103, 1, '2024-03-05');
```

---
#### Practice Queries:
##### 1. **List all customers with their orders (if any):**

```sql
SELECT c.customer_name, o.order_id, o.order_date
FROM customers c
LEFT JOIN orders o ON c.customer_id = o.customer_id;
```
You will see that **Ravi and Laxmi** are shown with **NULL** for `order_id` and `order_date`.

---

##### 2. **List customers who have NOT placed any orders:**
```sql
SELECT c.customer_name
FROM customers c
LEFT JOIN orders o ON c.customer_id = o.customer_id
WHERE o.order_id IS NULL;
```
This filters only customers **without** orders.

---
### **2. Teachers & Classes**
#### Tables:
##### **teachers**
```sql
CREATE TABLE teachers (
  teacher_id INT PRIMARY KEY,
  teacher_name VARCHAR(100)
);
```
##### **classes**
```sql
CREATE TABLE classes (
  class_id INT PRIMARY KEY,
  class_name VARCHAR(100),
  teacher_id INT,
  FOREIGN KEY (teacher_id) REFERENCES teachers(teacher_id)
);
```
#### Sample Data:
```sql
INSERT INTO teachers VALUES
(1, 'Mr. Sharma'),
(2, 'Ms. Rai'),
(3, 'Mr. Joshi');

INSERT INTO classes VALUES
(201, 'Math', 1),
(202, 'English', 2);
```

---
#### Practice Queries:
##### 1. **List all teachers with their assigned classes:**
```sql
SELECT t.teacher_name, c.class_name
FROM teachers t
LEFT JOIN classes c ON t.teacher_id = c.teacher_id;
```
This includes **Mr. Joshi** even though he has no class assigned.

---
##### 2. **Find teachers without any class assigned:**
```sql
SELECT t.teacher_name
FROM teachers t
LEFT JOIN classes c ON t.teacher_id = c.teacher_id
WHERE c.class_id IS NULL;
```
Shows teachers **not currently teaching** any class.

---
## **Module 5: RIGHT JOIN (or RIGHT OUTER JOIN)**

---
### **1. RIGHT JOIN Logic and Comparison with LEFT JOIN**

A **RIGHT JOIN** returns:
* All rows from the **right table**
* Matching rows from the **left table**
* If no match, returns **NULLs** for left table columns

---
#### **Comparison Table:**
| Feature                | LEFT JOIN                           | RIGHT JOIN                  |
| ---------------------- | ----------------------------------- | --------------------------- |
| Includes all rows from | Left table                          | Right table                 |
| Non-matching rows      | Right table rows = NULL             | Left table rows = NULL      |
| Usage                  | When left table is primary          | When right table is primary |
| Same result?           | Yes, if you reverse the table order |                             |

---
#### Example Logic:
```sql
SELECT ...
FROM A
RIGHT JOIN B ON A.id = B.id;
```
This returns all rows from `B`, and matching rows from `A`.

---
### **2. When and Why to Use RIGHT JOIN**
#### Use RIGHT JOIN when:
* The **right table is the focus** (e.g., you want to show **all managers**, even if they don’t have employees).
* You want to highlight **unmatched rows** from the right table.
* Your JOIN conditions or logic feel more **natural** reading left-to-right with the right table being dominant.

---
### **Practice: Employees & Managers**

---
#### Sample Schema:
##### **managers**
```sql
CREATE TABLE managers (
  manager_id INT PRIMARY KEY,
  manager_name VARCHAR(100)
);
```
##### **employees**
```sql
CREATE TABLE employees (
  emp_id INT PRIMARY KEY,
  emp_name VARCHAR(100),
  manager_id INT,
  FOREIGN KEY (manager_id) REFERENCES managers(manager_id)
);
```

---
#### Sample Data:
```sql
INSERT INTO managers VALUES
(1, 'Mr. Sharma'),
(2, 'Ms. Rai'),
(3, 'Mr. Joshi');

INSERT INTO employees VALUES
(101, 'Alice', 1),
(102, 'Bob', 1),
(103, 'Carol', 2);
```
Mr. Joshi has **no employees under him**.

---
#### Practice Queries:
##### 1. **List all managers and their employees (if any):**
```sql
SELECT e.emp_name, m.manager_name
FROM employees e
RIGHT JOIN managers m ON e.manager_id = m.manager_id;
```
Result:
| emp\_name | manager\_name |
| --------- | ------------- |
| Alice     | Mr. Sharma    |
| Bob       | Mr. Sharma    |
| Carol     | Ms. Rai       |
| NULL      | Mr. Joshi     |

Mr. Joshi is shown even though he has **no employee** — his `emp_name` is NULL.

---
##### 2. **Find managers without any employees:**
```sql
SELECT m.manager_name
FROM employees e
RIGHT JOIN managers m ON e.manager_id = m.manager_id
WHERE e.emp_id IS NULL;
```
Output: `Mr. Joshi`

---
## **Module 6: FULL JOIN (or FULL OUTER JOIN)**

---
### **1. Understanding FULL JOIN Behavior**

A **FULL JOIN** (also called **FULL OUTER JOIN**) returns:
* All matching rows from both tables
* **Unmatched rows** from **left table** (with NULLs from right)
* **Unmatched rows** from **right table** (with NULLs from left)
In simple terms:
```
FULL JOIN = LEFT JOIN + RIGHT JOIN
```

---
#### Example:
You want to compare **sales from 2023 and 2024**, and show:
* Products sold **only in 2023**
* Products sold **only in 2024**
* Products sold in **both years**

---
### 2. MySQL Does **Not Natively Support FULL JOIN**
Since **MySQL does not support FULL JOIN directly**, you can **simulate** it using:
```sql
SELECT ...
FROM table1
LEFT JOIN table2 ON ...
UNION
SELECT ...
FROM table1
RIGHT JOIN table2 ON ...
```

---
### 3. Practice: Sales Data from Two Years

---
#### Tables:
##### **sales\_2023**
```sql
CREATE TABLE sales_2023 (
  product_id INT PRIMARY KEY,
  product_name VARCHAR(100),
  sales_amount INT
);
```
##### **sales\_2024**
```sql
CREATE TABLE sales_2024 (
  product_id INT PRIMARY KEY,
  product_name VARCHAR(100),
  sales_amount INT
);
```

---
#### Sample Data:
```sql
-- 2023 Sales
INSERT INTO sales_2023 VALUES
(1, 'Laptop', 1000),
(2, 'Tablet', 500),
(3, 'Mouse', 200);

-- 2024 Sales
INSERT INTO sales_2024 VALUES
(1, 'Laptop', 1200),
(3, 'Mouse', 150),
(4, 'Keyboard', 300);
```

---
#### Simulated FULL JOIN in MySQL
```sql
-- FULL JOIN using UNION of LEFT and RIGHT JOIN
SELECT
  s23.product_id,
  COALESCE(s23.product_name, s24.product_name) AS product_name,
  s23.sales_amount AS sales_2023,
  s24.sales_amount AS sales_2024
FROM sales_2023 s23
LEFT JOIN sales_2024 s24 ON s23.product_id = s24.product_id

UNION

SELECT
  s24.product_id,
  COALESCE(s23.product_name, s24.product_name) AS product_name,
  s23.sales_amount AS sales_2023,
  s24.sales_amount AS sales_2024
FROM sales_2023 s23
RIGHT JOIN sales_2024 s24 ON s23.product_id = s24.product_id;
```

---
#### Output:
| product\_id | product\_name | sales\_2023 | sales\_2024 |
| ----------- | ------------- | ----------- | ----------- |
| 1           | Laptop        | 1000        | 1200        |
| 2           | Tablet        | 500         | NULL        |
| 3           | Mouse         | 200         | 150         |
| 4           | Keyboard      | NULL        | 300         |

---
## **Module 7: CROSS JOIN**

---
### **1. What is a CROSS JOIN?**

A **CROSS JOIN** returns the **Cartesian product** of two tables:
Every row from the first table is **combined with every row** from the second table.
#### Example:
If Table A has 3 rows and Table B has 2 rows, a CROSS JOIN will return:
```
3 × 2 = 6 rows
```
**No ON condition** is used in a CROSS JOIN.

---
### **2. Cartesian Product**
A **Cartesian product** is the **complete pairing** of all rows from two tables.
#### Syntax:
```sql
SELECT *
FROM table1
CROSS JOIN table2;
```
Or simply:
```sql
SELECT *
FROM table1, table2;
```

---
### **3. When to Use and Avoid CROSS JOIN**
#### Use CROSS JOIN When:
* You want to **generate combinations** (e.g., color × size).
* You are doing **testing**, **permutations**, or **simulations**.
* You want **every possible pair** between two lists.
#### Avoid When:
* Tables have large number of rows → can cause **performance issues**.
* You mistakenly forget the `ON` condition in a normal JOIN — this **accidentally becomes a CROSS JOIN**.

---
### **Practice: Combining Colors & Sizes**

---
#### Tables:
##### **colors**
```sql
CREATE TABLE colors (
  color_name VARCHAR(20)
);
```
##### **sizes**
```sql
CREATE TABLE sizes (
  size_label VARCHAR(10)
);
```

---
#### Sample Data:
```sql
INSERT INTO colors VALUES
('Red'),
('Blue'),
('Green');

INSERT INTO sizes VALUES
('S'),
('M'),
('L');
```

---
#### Query: All Color × Size Combinations
```sql
SELECT c.color_name, s.size_label
FROM colors c
CROSS JOIN sizes s;
```

---
#### Output:
| color\_name | size\_label |
| ----------- | ----------- |
| Red         | S           |
| Red         | M           |
| Red         | L           |
| Blue        | S           |
| Blue        | M           |
| Blue        | L           |
| Green       | S           |
| Green       | M           |
| Green       | L           |

You now have all **9 combinations** of color and size.

---
## **Module 8: SELF JOIN**

---
### **1. What is a SELF JOIN?**

A **SELF JOIN** is a **regular JOIN where a table is joined to itself**.
Since you are using the same table twice, you must use **aliases** to differentiate them.

---
#### Why SELF JOIN?
* To compare **rows within the same table**
* To build **hierarchies** (e.g., employees and their managers)
* To find **related data** from the same dataset

---
### **2. Syntax of SELF JOIN**
```sql
SELECT a.column, b.column
FROM table_name a
JOIN table_name b
ON a.related_column = b.related_column;
```
You treat the same table as two separate ones using **aliases**.

---
### **3. Use Case: Employee-Supervisor Relationship**

You want to list all employees **along with their managers’ names**.

#### Table: `employees`
| emp\_id | emp\_name | manager\_id |
| ------- | --------- | ----------- |
| 1       | Alice     | NULL        |
| 2       | Bob       | 1           |
| 3       | Carol     | 1           |
| 4       | David     | 2           |

Here:
* `manager_id` is a **foreign key** that points to `emp_id` in the **same table**.

---
### **4. Query: List Employee with Their Manager**
```sql
SELECT 
  e.emp_name AS employee,
  m.emp_name AS manager
FROM employees e
LEFT JOIN employees m
  ON e.manager_id = m.emp_id;
```

---
#### Output:
| employee | manager |
| -------- | ------- |
| Alice    | NULL    |
| Bob      | Alice   |
| Carol    | Alice   |
| David    | Bob     |

`Alice` has no manager (top-level), others show their respective manager names.

---
### **5. Practice: SELF JOIN on Employee Table**
#### Table Setup:
```sql
CREATE TABLE employees (
  emp_id INT PRIMARY KEY,
  emp_name VARCHAR(100),
  manager_id INT
);
```
#### Sample Data:
```sql
INSERT INTO employees VALUES
(1, 'Alice', NULL),
(2, 'Bob', 1),
(3, 'Carol', 1),
(4, 'David', 2),
(5, 'Eva', 3);
```

---
#### Practice Queries:
1. **List each employee with their manager name**:
```sql
SELECT 
  e.emp_name AS employee,
  m.emp_name AS manager
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.emp_id;
```

2. **List employees who are managers**:
```sql
SELECT DISTINCT m.emp_name AS manager
FROM employees e
JOIN employees m ON e.manager_id = m.emp_id;
```

3. **Find employees who are not managing anyone**:
```sql
SELECT e.emp_name
FROM employees e
LEFT JOIN employees sub ON e.emp_id = sub.manager_id
WHERE sub.emp_id IS NULL;
```

This filters employees **who have no subordinates**.

---
## **Module 9: Advanced JOIN Techniques**

---
### **1. JOINs with Aggregate Functions (`GROUP BY`, `COUNT`, `SUM`)**
When using JOINs, you can **group** results and apply aggregate functions to get summaries.
#### Example: Count Employees per Department
```sql
SELECT d.dept_name, COUNT(e.emp_id) AS total_employees
FROM departments d
LEFT JOIN employees e ON d.dept_id = e.dept_id
GROUP BY d.dept_name;
```
Shows department name and number of employees in each.

---
#### Example: Total Sales per Customer
```sql
SELECT c.customer_name, SUM(o.order_total) AS total_spent
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.customer_name;
```

---
### **2. JOIN with Subqueries**
Subqueries allow you to **filter or calculate** something separately, then JOIN it.

#### Example: Join with a filtered subquery
```sql
SELECT e.emp_name, d.dept_name
FROM employees e
JOIN (
  SELECT * FROM departments WHERE dept_name != 'HR'
) d ON e.dept_id = d.dept_id;
```
Joins only non-HR departments.

---
#### Example: Subquery with Aggregation + JOIN
```sql
SELECT d.dept_name, stats.avg_salary
FROM departments d
JOIN (
  SELECT dept_id, AVG(salary) AS avg_salary
  FROM employees
  GROUP BY dept_id
) stats ON d.dept_id = stats.dept_id;
```

---

### **3. JOIN with CTEs (Common Table Expressions)**

CTEs (using `WITH`) make queries **cleaner and reusable**.

#### Example: CTE + JOIN

```sql
WITH department_salaries AS (
  SELECT dept_id, SUM(salary) AS total_salary
  FROM employees
  GROUP BY dept_id
)
SELECT d.dept_name, ds.total_salary
FROM departments d
JOIN department_salaries ds ON d.dept_id = ds.dept_id;
```

---

#### Why use CTEs?

* Improves readability
* Allows **multiple JOINs with the same logic**
* Works well in complex queries

---

### **4. JOIN Performance Considerations & Indexing**

JOINs can get **slow on large tables**, especially if columns being joined are **not indexed**.

#### Best Practices:

| Tip                                                   | Why it Helps                     |
| ----------------------------------------------------- | -------------------------------- |
| Use indexes on JOIN keys                              | Faster lookups and joins         |
| Avoid joining unnecessary columns                     | Reduces memory usage             |
| Use `EXPLAIN` keyword                                 | Analyze query execution plan     |
| Prefer INNER JOIN over OUTER JOIN if possible         | INNER JOINs are generally faster |
| Watch for Cartesian joins (CROSS JOINs without WHERE) | Can explode row count            |

---

#### Example: Add Index

```sql
CREATE INDEX idx_emp_dept_id ON employees(dept_id);
```

Makes JOINs on `dept_id` much faster.

---

## **Module 10: Practical Projects**

---

### **1. Build Mini-Projects Using Sample Databases**

---

#### **Project 1: HR Database**

**Tables:**

* `employees(emp_id, emp_name, dept_id, salary)`
* `departments(dept_id, dept_name)`
* `salaries(emp_id, salary, pay_date)`

---

**Sample Queries:**

* List employees with their department and current salary.
* Find average salary per department.
* Show employees earning above the department average.
* Track salary history of an employee.

---

#### **Project 2: School Database**

**Tables:**

* `students(student_id, student_name, class_id)`
* `subjects(subject_id, subject_name)`
* `teachers(teacher_id, teacher_name)`
* `results(student_id, subject_id, marks)`

---

**Sample Queries:**

* List students with their teachers for each subject.
* Find the top scorer in each subject.
* Show average marks per student.
* List students failing in any subject (marks < passing mark).

---

#### **Project 3: E-commerce Database**

**Tables:**

* `users(user_id, user_name)`
* `products(product_id, product_name, price)`
* `orders(order_id, user_id, order_date)`
* `order_items(order_id, product_id, quantity)`
* `payments(payment_id, order_id, amount, payment_date)`

---

**Sample Queries:**

* List users with their total spent amount.
* Show orders with product details and quantities.
* Find best-selling products.
* Track payment status of orders.

---

### **Tips for Project Execution**

* Design your tables with proper primary & foreign keys.
* Use **JOINs** to combine data from multiple tables.
* Apply **aggregations** (`SUM`, `COUNT`, `AVG`) for reports.
* Use **subqueries** or **CTEs** for complex filtering.
* Optimize queries with indexing.

---

