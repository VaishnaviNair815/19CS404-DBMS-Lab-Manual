# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
sqlWhat is the average duration of insurance coverage for patients covered by each insurance company?

Sample table:Insurance Table

name               type
-----------------  ----------
InsuranceID        INTEGER
PatientID          INTEGER
InsuranceCompany   TEXT
PolicyNumber       TEXT
PolicyHolder       TEXT
StartDate          DATE
EndDate            DATE
For example:

Result
InsuranceCompany  AvgCoverageDurationDays
----------------  -----------------------
ABC Insurance     7.0
DEF Insurance     3.0
JKL Insurance     3.0
STU Insurance     3.0
VWX Insurance     3.0
XYZ Insurance     3.0
YZA Insurance     3.0
-- Paste your SQL code below for Question 1
```
SElECT InsuranceCompany,
ROUND(AVG((julianday(EndDate)-julianday(StartDate))/365.0),1) AS AvgCoverageDurationDays 
FROM Insurance
Group BY InsuranceCompany;
```

**Output:**

<img width="1385" height="967" alt="image" src="https://github.com/user-attachments/assets/b2df6fa5-1c7f-4bcd-a3a7-7053a9b369fc" />


**Question 2**
---
Sample tablePrescriptions Table



For example:

Result
Frequency      TotalPrescriptions
-------------  ------------------
Every 3 weeks  1
Every 6 hours  1
Once           1
Once daily     4
Once daily at  1
Pending        1
Twice daily    1


```sql
SELECT Frequency,
count(*)AS TotalPrescriptions
FROM Prescriptions  
group by Frequency;
```

**Output:**
<img width="1313" height="978" alt="image" src="https://github.com/user-attachments/assets/7fd7c1ad-4373-498d-a631-4eabc1d4c30a" />


**Question 3**
---
How many medical records are there for each patient?

Sample table:MedicalRecords Table


<img width="934" height="132" alt="image" src="https://github.com/user-attachments/assets/2119fdf6-5dc8-4554-806a-6851e7d15584" />

For example:

Result
PatientID   TotalRecords
----------  ------------
4           4
5           1
6           1
7           1
8           1
10          2


```sql
SELECT
PatientID,
count(RecordID) AS TotalRecords
FROM MedicalRecords  
group by PatientID
```

**Output:**

<img width="1277" height="976" alt="image" src="https://github.com/user-attachments/assets/12226051-91f7-4963-9e83-83746b7fad7b" />


**Question 4**
---
Write a SQL query to find the minimum purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

 

For example:

Result
MINIMUM
----------
65.26


```sql
SELECT MIN(purch_amt) AS MINIMUM
FROM orders;
```

**Output:**

<img width="1301" height="977" alt="image" src="https://github.com/user-attachments/assets/92d5dd87-c6f5-4776-a0b7-697d1edc806e" />

**Question 5**
---
Write a SQL query that counts the number of unique salespeople. Return number of salespeople.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

 

For example:

Result
COUNT
----------
6


```sql
SELECT COUNT(DISTINCT salesman_id) AS COUNT
FROM orders;
```

**Output:**

<img width="1290" height="970" alt="image" src="https://github.com/user-attachments/assets/15b2e6f1-d4e4-489e-8f13-68812a63f991" />


**Question 6**
---
Write a SQL query to find the Fruit with the lowest available quantity.

Note: Inventory attribute contains amount of fruits

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
 

For example:

Result
fruit_name  lowest_quantity
----------  ---------------
Watermelon  15


```sql
SELECT name AS "fruit_name" , inventory AS "lowest_quantity"
FROM fruits
order by inventory ASC
LIMIT 1
```

**Output:**

<img width="1187" height="956" alt="image" src="https://github.com/user-attachments/assets/092b3eb5-93ef-4e49-8aec-c8400ed1ee1e" />

**Question 7**
---
Write a SQL query to return the total number of rows in the 'customer' table where the city is Noida.

Sample table: customer


<img width="962" height="149" alt="image" src="https://github.com/user-attachments/assets/26055cdf-ff76-4e86-a13e-18a3a48eb499" />

 

For example:

Result
COUNT
----------
1


```sql
SELECT 
count(*) AS COUNT
FROM customer
WHERE city ='Noida';
```

**Output:**

<img width="1312" height="970" alt="image" src="https://github.com/user-attachments/assets/353bb5fe-bc63-40e1-af11-0f1919be9ca0" />

**Question 8**
---
Write the SQL query that accomplishes the selection of total number of products for each category from the "products" table, and includes only those products where the minimum category ID is less than 3.

Sample table: products
<img width="777" height="170" alt="image" src="https://github.com/user-attachments/assets/f597d8d0-361b-4364-a21a-72cd5adc48f7" />



For example:

Result
category_id  count(product_name)
-----------  -------------------
1            4
2            3

```sql
SELECT category_id,count(product_name) 
FROM products
group by category_id
HAVING MIN(category_id)<3;
```

**Output:**

<img width="1339" height="978" alt="image" src="https://github.com/user-attachments/assets/f51d7400-7127-4c05-b5b4-684fda2c5f2e" />


**Question 9**
---
Write the SQL query that accomplishes the grouping of data by age, calculates the total income for each age group, and includes only those age groups where the total income sum is greater than 1,000,000.

Sample table: employee

<img width="778" height="165" alt="image" src="https://github.com/user-attachments/assets/64c533de-be55-4aa4-b454-64b2ed3f5f96" />


For example:

Result
age         SUM(income)
----------  -----------
35          10000000
40          1350000


```sql
SELECT age,
SUM(income)
FROM employee
group by age
Having SUM(income)>1000000;
```

**Output:**

<img width="1321" height="979" alt="image" src="https://github.com/user-attachments/assets/d78cdddb-38c6-4169-8880-f1da85a9da7e" />


**Question 10**
---
Write an SQL query that groups the customer data into 5-year age intervals, calculates the minimum salary for each group, and excludes groups where the minimum salary is not less than 2000.

Table: customer1

<img width="780" height="135" alt="image" src="https://github.com/user-attachments/assets/438ccfa9-80a0-44e6-a270-b098969784d4" />

For example:

Result
age_group   MIN(salary)
----------  -----------
25          1500

```sql

SELECT  (age/5)*5 AS age_group,
MIN(salary)
FROM customer1
Group by (age/5)*5 
Having MIN(salary)< 2000;
```

**Output:**

<img width="1430" height="974" alt="image" src="https://github.com/user-attachments/assets/8822b362-0dc5-4b62-8be5-73cc3c1510b4" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
