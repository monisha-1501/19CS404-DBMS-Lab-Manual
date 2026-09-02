# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```

### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--Write a SQL query to add birth_date attribute as timestamp (datatype) in the table customer 

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002

```sql
ALTER TABLE customer ADD birth_date timestamp;
```

**Output:**

<img width="1236" height="441" alt="image" src="https://github.com/user-attachments/assets/872bfa32-c8a9-46b8-b6c5-60399c59fd43" />



**Question 2**
---Insert the below data into the Student_details table, allowing the Subject and MARKS columns to take their default values.

RollNo      Name          Gender      
----------  ------------  ----------  
204         Samuel Black  M          

Note: The Subject and MARKS columns will use their default values.

```sql
INSERT INTO student_details(RollNo,Name, Gender)
VALUES (204,'Samuel Black', 'M');
```

**Output:**

<img width="865" height="417" alt="image" src="https://github.com/user-attachments/assets/42728aa6-d0a3-45e6-acba-23f17a7b7c1f" />



**Question 3**
---Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.

```sql
CREATE TABLE ProjectAssignments (AssignmentID INTEGER PRIMARY KEY,EmployeeID INTEGER, ProjectID INTEGER,AssignmentDate DATA NOT NULL,FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID),
FOREIGN KEY (ProjectID) REFERENCES Projects(ProjectID));
```

**Output:**

<img width="850" height="360" alt="image" src="https://github.com/user-attachments/assets/d4581ac8-f904-40cb-b136-2b5ece70acbc" />



**Question 4**
---Create a table named Employees with the following columns:

EmployeeID as INTEGER
FirstName as TEXT
LastName as TEXT
HireDate as DATE

```sql
CREATE TABLE Employees (
EmployeeID INTEGER,
FirstName TEXT,
LastName TEXT,
HireDate DATE
);
```

**Output:**
<img width="855" height="377" alt="image" src="https://github.com/user-attachments/assets/2f3adfbe-e866-422c-ab0f-d01675651187" />





**Question 5**
---
Create a table named Department with the following constraints:
DepartmentID as INTEGER should be the primary key.
DepartmentName as TEXT should be unique and not NULL.
Location as TEXT.

```sql
CREATE TABLE Department(
DepartmentID INTEGER PRIMARY KEY,
DepartmentName TEXT UNIQUE NOT NULL,
Location TEXT);
```

**Output:**
<img width="862" height="362" alt="image" src="https://github.com/user-attachments/assets/8d1f8ecb-a9f0-4aae-871f-1d1f0bafcf16" />




**Question 6**
---
create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.

```sql
CREATE TABLE jobs(
job_id INT PRIMARY KEY,
job_title VARCHAR(100) DEFAULT '',
min_salary DECIAML (10,2) DEFAULT 8000,
max_salary DECIMAL(10,2) DEFAULT NULL);
```

**Output:**
<img width="855" height="395" alt="image" src="https://github.com/user-attachments/assets/4cfba9b8-73e4-4ce9-b90d-8287dd6258f8" />




**Question 7**
---
Write a SQL query to Add a new ParentsNumber column  as number and Adhar_Number as Number in the Student_details table.

```sql
ALTER TABLE Student_details ADD ParentsNumber number;
ALTER TABLE Student_details ADD Adhar_Number number;
```

**Output:**

<img width="858" height="463" alt="image" src="https://github.com/user-attachments/assets/9ecd4244-57ba-4660-9d95-ee4299656c7d" />



**Question 8**
---
Insert all customers from Old_customers into Customers

Table attributes are CustomerID, Name, Address, Email

```sql
INSERT INTO Customers SELECT * FROM old_customers;
```

**Output:**


<img width="861" height="361" alt="image" src="https://github.com/user-attachments/assets/1786b56f-4ad1-4c0e-91f3-41bb200bd456" />



**Question 9**
---
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should cascade updates and deletes.
item_desc and rate should not accept NULL.

```sql
CREATE TABLE item (
item_id TEXT PRIMARY KEY, 
item_desc TEXT NOT NULL,
rate INTEGER NOT NULL,
icom_id TEXT CHECK (LENGTH (icom_id) = 4),
FOREIGN KEY (icom_id) REFERENCES company (com_id)
ON UPDATE CASCADE
ON DELETE CASCADE);

```

**Output:**

<img width="851" height="427" alt="image" src="https://github.com/user-attachments/assets/ae64383c-8e50-4b47-a9b3-0a190ee9b323" />





**Question 10**
---

In the Products table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ProductID   Name              Category    Price       Stock
----------  ---------------   ----------  ----------  ----------
106         Fitness Tracker   Wearables
107         Laptop            Electronics  999.99      50
108         Wireless Earbuds  Accessories              100

```sql
INSERT INTO Products(ProductID,Name,Category,Price,Stock)
VALUES (106,'Fitness Tracker','Wearables',NULL,NULL);
INSERT INTO Products(ProductID,Name,Category,Price,Stock)
VALUES (107,'Laptop','Electronic', 999.99,50);
INSERT INTO Products(ProductID,Name,Category,Price,Stock)
VALUES (108,'Wireless Earbud','Accessorie',NULL,100);
```

**Output:**

<img width="852" height="366" alt="image" src="https://github.com/user-attachments/assets/ea51e532-29f8-48eb-8751-fb8ff910c74b" />




## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
