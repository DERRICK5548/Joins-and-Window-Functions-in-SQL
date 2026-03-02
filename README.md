# Joins-and-Window-Functions-in-SQL
##<u>Introduction</u>
In data analysis, SQL plays a vital role for querying and transforming data. Inbuilt features like joins and window functions enable analysts to combine datasets into important and meaningful views as well as perform basic and complex calculations. In this article, we will discuss how joins and window functions work and their importance in analytics.

##<u>Joins</u> 
Joins are used to combine rows from two or more tables based on a common column.
Usually, the common column its the primary key and a foreign key.

**What is the Importance Of Joins?**

1. Relational Data Connection: Joins allow easy connection of tables.   For Example: You can match a customer_id in sales table with a customers table.
1. Normalization: Joins can help to normalize data i.e. eliminate duplicates therefore improving data storage, by storing data into different tables rather than repeating data which brings inconsistencies.
1. Performance Optimization: Using joins like the (inner join) improves data retrieval and enhances fast filtering also.

##<u>Types of Joins Include:</u>
**INNER JOIN**
The INNER JOIN returns only matching records from both tables.
Excludes non-matching data from the result
For Example: Matching employees from employees table with departments table the common column being the department_id.
```
SELECT e.name, d.department_name
FROM Employees e
INNER JOIN Departments d
ON e.department_id = d.department_id;
```
**Visual Representation:**

![INNER JOIN](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/m1teq8idv3dsikani8cw.png)


**LEFT JOIN**
Also known as left outer join.
Returns all records from the left table, and matched records from the right.

```
SELECT e.name, d.department_name
FROM Employees e
LEFT JOIN Departments d
ON e.department_id = d.department_id;
```
**Visual Representation:**
![LEFT JOIN](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/f7dgygxkj9ewnz911x0u.png)


**RIGHT JOIN**
Also known as right outer join
Returns all records from the right table, and matched records from the left
```
SELECT e.name, d.department_name
FROM Employees e
RIGHT JOIN Departments d
ON e.department_id = d.department_id;
```
**Visual Representation:**

![RIGHT JOIN](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/s6oa4r4bxnvobzlpat9d.png)


**FULL JOIN**
Also known as full outer join. 
Returns all records when a match exists in either table.

```
SELECT e.name, d.department_name
FROM Employees e
FULL JOIN Departments d
ON e.department_id = d.department_id;
```
**Visual Representation:**

![FULL JOIN](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/cr6wdu6ccf1bad70n6ut.png)

##<u>WINDOW FUNCTIONS IN SQL</u>
Window functions allow you to perform calculations across a defined set of rows (window), without collapsing the result into a single value.

**Common uses for Window Functions:**
1. Aggregates->calculates sum, averages, count across a partition of rows.
1. Rankings->They assign ranks to rows. Very useful when performing N-queries or ordered comparisons.
1. Running totals->they generate cumulative totals over a period of time.

To define a window for calculation, you use the `OVER()` clause.
Through this you can:
- PARTITION BY->it divides data into groups but doesn't collapse the rows.

- ORDER BY->order by specifies the order of the rows.

**General syntax for a window function:**
`SELECT column_name1, 
       window_function(column_name2) 
       OVER ([PARTITION BY column_name3] [ORDER BY column_name4]) AS new_column
FROM table_name;`

##Types of window functions in SQL

<u>**A. AGGREGATE FUNCTIONS**</u>
Aggregate functions perform aggregates over a window of rows.
They include:

- SUM(): Sums values within a window.

Sample Query: Total salary by department.
```
SELECT name,department,salary,
SUM(salary) OVER (PARTITION BY department) AS dept_total
FROM employees;
```

- AVG(): Calculates the average value within a window.

Sample Query: Calculating the average salary within each department.


```
SELECT Name, Age, Department, Salary, 
AVG(Salary) OVER( PARTITION BY Department) AS Avg_Salary
FROM employee
```
- COUNT(): Counts the rows within a window.

Sample Query: Counting rows within a specific group.
```
SELECT OrderID,CustomerID,OrderDate,
COUNT(OrderID) OVER (PARTITION BY CustomerID) AS OrdersPerCustomer
FROM Orders;
```
- MAX(): Returns the maximum value in the window.

Sample Query: Finding the maximum salary within each department
```
SELECT  employee_id, department, salary,
MAX(salary) OVER(PARTITION BY department) AS dep_maximum_salary
FROM employee;
```
- MIN(): Returns the minimum value in the window.

Sample Query: finding the minimum salary within each department and displaying each employee's individual details. 
```
SELECT department, employee_name, salary,
MIN(salary) OVER (PARTITION BY department) AS min_department_salary
FROM employees;
```

**<u>B. RANKING FUNCTIONS<U/>**

They assign ranks to rows within a specified area.
They include:
- ROW_NUNMBER()->Assigns a unique number to each row in the result set.
It automatically increments by 1 for every row.

Sample Query:
``` 
SELECT name, salary,
ROW_NUMBER() OVER (ORDER BY salary DESC) AS row_num
FROM employees;
```
- RANK()->They assign ranks rows, when they find a duplicate they skip.
Simply, they organize data and analyze data.

Sample Query: Ranking employees by salary, as well as skipping where salary is equal.
```
SELECT Name, Department, Salary,
RANK() OVER(PARTITION BY Department ORDER BY Salary DESC) AS emp_rank
FROM employee;
```
-DENSE_RANK()->Assigns ranks to rows without skipping rank numbers for duplicates.
Its usually the same as Rank() but doesn't skip
Sample Query: Ranking employees by salary without skipping ranks
```
SELECT Name, Department, Salary,
DENSE_RANK() OVER(PARTITION BY Department ORDER BY Salary DESC) AS emp_dense_rank
FROM employee;
```

- PERCENT_RANK()->shows where a row stands compared to others in the same group.  
Sample Query: finding the relative salary position of each employee within a department.

```
SELECT Name, Department, Salary,
PERCENT_RANK() OVER(PARTITION BY Department ORDER BY Salary DESC) AS emp_percent_rank
FROM employee;
```
##Conclusion
Joins and window functions are very important in SQL. As they make data analysis easier and effective. Therefore, learning and practicing these topics is essential for any data analyst.
