# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
Write a SQL query that retrieve all the columns from the table "Grades", where the grade is equal to the maximum grade achieved in each subject. Sample table: GRADES (attributes: student_id, student_name, subject, grade)

```sql
SELECT *
FROM GRADES g
WHERE grade = (
    SELECT MAX(grade)
    FROM GRADES
    WHERE subject = g.subject
);

```

**Output:**

<img width="1136" height="335" alt="438736610-d3d3c6be-b5b9-40e7-aed4-091d3c825e63" src="https://github.com/user-attachments/assets/9f73ff18-116b-4afb-85ef-5540282802a4" />


**Question 2**
---
Write a SQL query to Identify customers whose city is different from the city of the customer with the highest ID

SAMPLE TABLE: customer
```
name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
```

```sql
SELECT *
FROM customer
WHERE city <> (
    SELECT city
    FROM customer
    WHERE id = (SELECT MAX(id) FROM customer)
);

```

**Output:**

<img width="1118" height="367" alt="438736907-91ff9e98-1f8d-4a62-877a-5cf34ee18ee4" src="https://github.com/user-attachments/assets/df4fc97e-0d92-4e16-b12b-a5ae31e621e2" />


**Question 3**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is LESS than $2500.

Sample table: CUSTOMERS
```
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000
```

```sql
SELECT *
FROM CUSTOMERS
WHERE SALARY < 2500;

```

**Output:**

<img width="1000" height="352" alt="438737441-5368fd05-45e9-44ce-98b9-755023b20def" src="https://github.com/user-attachments/assets/7d558797-9100-4ed4-a2d1-78633d37fe31" />


**Question 4**
---
From the following tables write a SQL query to count the number of customers with grades above the average in New York City. Return grade and count.

customer table
```
name         type
-----------  ----------
customer_id  int
cust_name    text
city         text
grade        int
salesman_id  int
```

```sql
SELECT grade, COUNT(*)
FROM customer
WHERE  grade > (SELECT AVG(grade) FROM customer WHERE city = 'New York')
GROUP BY grade;
```

**Output:**

<img width="493" height="257" alt="438737770-5ee3faa5-16e7-4f66-aa1d-3be574da237b" src="https://github.com/user-attachments/assets/04820172-34f1-4c3f-bdb4-d18f23b37286" />


**Question 5**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi

Sample table: CUSTOMERS
```
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000
```

```sql
SELECT *
FROM CUSTOMERS
WHERE ADDRESS = 'Delhi';

```

**Output:**

<img width="1005" height="250" alt="438738204-80f9f243-907d-4aea-a337-6c50af79ea3f" src="https://github.com/user-attachments/assets/126873dc-d4e8-464f-a625-126c12021666" />


**Question 6**
---
From the following tables write a SQL query to find the order values greater than the average order value of 10th October 2012. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

Note: date should be yyyy-mm-dd format

ORDERS TABLE
```
name            type
----------     ----------
ord_no          int
purch_amt    real
ord_date       text
customer_id  int
salesman_id  int
```

```sql
SELECT ord_no, purch_amt, ord_date, customer_id, salesman_id
FROM ORDERS
WHERE purch_amt > (
    SELECT AVG(purch_amt)
    FROM ORDERS
    WHERE ord_date = '2012-10-10'
);
```

**Output:**

<img width="1015" height="348" alt="438738727-c430c51e-9b78-4f93-8466-421008a9ef22" src="https://github.com/user-attachments/assets/11b29a9c-1f6f-4202-ac40-c55100e5e109" />


**Question 7**
---
From the following tables write a SQL query to find all orders generated by New York-based salespeople. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

salesman table
```
name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)
```
orders table
```
name             type
---------------  --------
order_no         int
purch_amt        real
order_date       text
customer_id      int
salesman_id      int
```

```sql
SELECT o.ord_no, o.purch_amt, o.ord_date, o.customer_id, o.salesman_id
FROM orders o
JOIN salesman s ON o.salesman_id = s.salesman_id
WHERE s.city = 'New York';

```

**Output:**

<img width="998" height="353" alt="438739345-2fc61d66-a2cb-4187-aae4-096d234335ec" src="https://github.com/user-attachments/assets/ace615c0-5c61-4972-8e38-dbeedd2bf287" />


**Question 8**
---
From the following tables, write a SQL query to find those salespeople who earned the maximum commission. Return ord_no, purch_amt, ord_date, and salesman_id.

salesman table
```
name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)
```
orders table
```
name             type
---------------  --------
order_no         int
purch_amt        real
order_date       text
customer_id      int
salesman_id      int
```

```sql
SELECT o.ord_no, o.purch_amt, o.ord_date, o.salesman_id
FROM orders o
JOIN salesman s ON o.salesman_id = s.salesman_id
WHERE s.commission = (
    SELECT MAX(commission)
    FROM salesman
);

```

**Output:**
<img width="826" height="357" alt="438739795-d34c06f4-4485-45aa-a1df-f7d9401eec2b" src="https://github.com/user-attachments/assets/d1eb188b-9c00-44b0-ac51-c9a4df477c04" />


**Question 9**
---
From the following tables, write a SQL query to find all the orders generated in New York city. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

SALESMAN TABLE
```
name               type
-----------        ----------
salesman_id  numeric(5)
name             varchar(30)
city                 varchar(15)
commission   decimal(5,2)
```
ORDERS TABLE
```
name            type
----------      ----------
ord_no          int
purch_amt    real
ord_date       text
customer_id  int
salesman_id  int
```

```sql
SELECT o.ord_no, o.purch_amt, o.ord_date, o.customer_id, o.salesman_id
FROM orders o
JOIN salesman s ON o.salesman_id = s.salesman_id
WHERE s.city = 'New York';

```

**Output:**

<img width="981" height="371" alt="438740256-52f55304-0cfd-4b75-bdb5-f6fe19e13f0b" src="https://github.com/user-attachments/assets/0ac6c275-66e4-4839-9717-3bb566275374" />


**Question 10**
---
Write a SQL query that retrieves the all the columns from the Table Grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)


```sql
SELECT student_id, student_name, subject, grade
FROM Grades g
WHERE grade = (
    SELECT MIN(grade)
    FROM Grades
    WHERE subject = g.subject
);

```

**Output:**

<img width="1087" height="330" alt="438740732-d16e38c0-ec16-448e-b45b-fbb95ba9cba7" src="https://github.com/user-attachments/assets/65f8c295-8b7d-436b-bfd6-db96e0f9b3d5" />

## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
