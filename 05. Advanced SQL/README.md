## Chapter 05. Advanced SQL

# Lesson 1. GROUP BY

https://academy.zerotomastery.io/courses/1073491/lectures/23648637

N: Get in-depth information by group

Ex:
SELECT dept_no, COUNT(emp_no)
FROM "public"."dept_emp"
GROUP BY dept_no;

- groups all the department number (dept_no) in a single cel and then count all the employees for that department.

<GROUP BY> splits data into groups or chuck of data so we can apply functions against the group rather than the entire table! It used to get a count, sum, max or min (aggregated functions). We apply the functin per group

# Lesson 2. Group By Exercises

https://academy.zerotomastery.io/courses/1073491/lectures/23659456

1. Exercise:
   How many people were hired on any given hire date?
   Database: Employees
   Table: Employ

Answer:
SELECT hire_date, COUNT(emp_no) as "amount"
FROM employees
GROUP BY hire_date
ORDER BY "amount" DESC;

2. Exercise:
   Show me all the employees, hired after 1991 and count the amount of positions they've had
   Database: Employees

Answer:
SELECT e.emp_no, count(t.title) as "amount of titles"
FROM employees as e
JOIN titles as t USING(emp_no)
WHERE EXTRACT (YEAR FROM e.hire_date) > 1991
GROUP BY e.emp_no
ORDER BY e.emp_no;

3. Exercise:
   Show me all the employees that work in the department development and the from and to date.
   Database: Employees

Answer:
SELECT e.emp_no, de.from_date, de.to_date
FROM employees as e
JOIN dept_emp AS de USING(emp_no)
WHERE de.dept_no = 'd005'
GROUP BY e.emp_no, de.from_date, de.to_date
ORDER BY e.emp_no, de.to_date;

- WHERE de.dept_no = 'd005' to satisfied the condiction to only show workers from 'development deparment'. Table 'departments' show the the corresponde number for each department. I think this is not really useful in real life but practical as exercise coz over complicate the SQL

# Lesson 3. HAVING Keyword

https://academy.zerotomastery.io/courses/1073491/lectures/23610053

<HAVING Keyword> apply filters in a group as a whole

Ex:
SELECT d.dept_name, COUNT(e.emp_no) AS "# of employees"
from employees AS e
INNER JOIN dept_emp AS de ON de.emp_no = e.emp_no
INNER JOIN departments as d ON de.dept_no = d.dept_no
WHERE e.gender = 'F'
GROUP by d.dept_name
HAVING count(e.emp_no) > 25000

- If I try to do a aggregate function in the WHERE clause, it will give me an error. That is why we use HAVING

# LESSON 4. Having Exercises

https://academy.zerotomastery.io/courses/1073491/lectures/25317819

1. Exercise:
   Show me all the employees, hired after 1991, that have had more than 2 titles
   Database: Employees

Answer:
SELECT e.emp_no, count(t.title) as "amount of titles"
FROM employees as e
JOIN titles as t USING(emp_no)
WHERE EXTRACT (YEAR FROM e.hire_date) > 1991
GROUP BY e.emp_no
HAVING count(t.title) > 2
ORDER BY e.emp_no;

2. Exercise:
   Show me all the employees that have had more than 15 salary changes that work in the department development
   Database: Employees

Answer:
SELECT e.emp_no, count(s.from_date) as "amount of raises"
FROM employees as e
JOIN salaries as s USING(emp_no)
JOIN dept_emp AS de USING(emp_no)
WHERE de.dept_no = 'd005'
GROUP BY e.emp_no
HAVING count(s.from_date) > 15
ORDER BY e.emp_no;

3. Exercise:
   Show me all the employees that have worked for multiple departments
   Database: Employees

Answer:
SELECT e.emp_no, e.first_name, count(de.dept_no) as "worked for # departments"
FROM employees as e
JOIN dept_emp AS de USING(emp_no)
GROUP BY e.emp_no
HAVING count(de.dept_no) > 1
ORDER BY e.emp_no;

# Lesson 5. Ordering Grouped Data

https://academy.zerotomastery.io/courses/1073491/lectures/23610048

# Lesson 5. Group By Mental Model

https://academy.zerotomastery.io/courses/1073491/lectures/23610043

# Lesson 6. Grouping Sets

https://academy.zerotomastery.io/courses/1073491/lectures/23610041

<UNION ALL> does not remove duplicate records
<UNION> remove duplicate data
<GROUPING SET> is a subclause that allows you to define multiple groupings

# Lesson 7. Rollup

https://academy.zerotomastery.io/courses/1073491/lectures/23610051

Ex:
SELECT EXTRACT(YEAR from orderdate) as "year",
EXTRACT(MONTH from orderdate) as "month",
EXTRACT(DAY from orderdate) as "day",
sum(ol.quantity)
From orderlines as ol
GROUP BY
ROLLUP(
EXTRACT(YEAR from orderdate),
EXTRACT(MONTH from orderdate),
EXTRACT(DAY from orderdate)
)
ORDER BY
EXTRACT(YEAR from orderdate),
EXTRACT(MONTH from orderdate),
EXTRACT(DAY from orderdate)

N: This query returns the sum of all the day, the months, years and total sum

# Lesson 8. Window What?

https://academy.zerotomastery.io/courses/1073491/lectures/23633823

# Lesson 9. Looking Through The Window

https://academy.zerotomastery.io/courses/1073491/lectures/23610050

<Window functions> create a new column based on functions perfomanced or a bubset or a window of the data

Ex:
SELECT
\*,
max(salary) over()
from salaries
where salary < 70000

N: This query returns all the data from table <salaries> and create a column with the max salary. It could be use to compare individual salary with the maximum salary.

- In this case the max salary function willbe use in the range we selected (salary < 70000).

# Lesson 10. PARTITION BY

https://academy.zerotomastery.io/courses/1073491/lectures/23610057

Ex:
SELECT
\*,
max(salary) over(
PARTITION by d.dept_name
)
from salaries
join dept_emp AS de USING(emp_no)
join departments as d USING(dept_no)

N: This will return all the data from salaries table and CREATE w columns. One column with the departnment name and the other with the salary of that specific department

# Lesson 11. Order By Acting Strange

https://academy.zerotomastery.io/courses/1073491/lectures/23610039

# Lesson 12. Using Framing In Window Function

https://academy.zerotomastery.io/courses/1073491/lectures/23610054

When we use <FRAME CLAUS> in a window function we can create a sub range or frame

<With ORDER BY> by defaultthe framing is everything before the row and the current row

1. Ex:
   SELECT emp_no,
   salary,
   COUNT(salary) over(
   PARTITION by emp_no
   ORDER BY emp_no
   )
   from salaries

- Set a column with the amount of the salaries

2. Ex:
   SELECT emp_no,
   salary,
   COUNT(salary) over(
   PARTITION by emp_no
   ORDER BY salary
   )
   from salaries

- Set a column with a count down of the salary

3. Ex:
   SELECT emp_no,
   salary,
   COUNT(salary) over(
   PARTITION by emp_no
   ORDER BY salary
   range BETWEEN UNBOUNDED PRECEDING and UNBOUNDED FOLLOWING
   )
   from salaries

- Same result as the first example

# Lesson 13. Solving For Current Salary

https://academy.zerotomastery.io/courses/1073491/lectures/23610047

1. EX:
   SELECT
   DISTINCT emp_no,
   LAST_VALUE(s.from_date) over(
   PARTITION by s.emp_no
   ORDER BY s.from_date
   range BETWEEN UNBOUNDED PRECEDING and UNBOUNDED FOLLOWING
   ),
   LAST_VALUE(salary) over(
   PARTITION by s.emp_no
   ORDER BY s.from_date
   range BETWEEN UNBOUNDED PRECEDING and UNBOUNDED FOLLOWING
   )
   from salaries AS s
   JOIN dept_emp AS de USING (emp_no)

2. Ex:
   SELECT
   DISTINCT emp_no,
   e.first_name,
   LAST_VALUE(salary) over(
   PARTITION by e.emp_no
   ORDER BY s.from_date
   range BETWEEN UNBOUNDED PRECEDING and UNBOUNDED FOLLOWING
   ) AS "current salary"
   from salaries AS s
   JOIN employees AS e USING (emp_no)
   JOIN dept_emp AS de USING (emp_no)
   JOIN departments AS d USING (dept_no)

# Lesson 14. FIRST_VALUE

https://academy.zerotomastery.io/courses/1073491/lectures/23610052

Ex:
I want to know how my prices compares to the item with the lowest price in the same category

1.  SELECT
    prod_id,
    price,
    category,
    first_value( price )OVER(
    PARTITION BY category
    ORDER by price
    range BETWEEN UNBOUNDED PRECEDING and UNBOUNDED FOLLOWING
    ) as "cheapest in category"
    From "public"."products"

2.  SELECT
    prod_id,
    price,
    category,
    min( price )OVER(
    PARTITION BY category
    ) as "cheapest in category"
    From "public"."products"

N: Using aggregate function <min> is as using <first value> but simplier.

# Lesson 15. LAST_VALUE

https://academy.zerotomastery.io/courses/1073491/lectures/23610049

Ex:
I want to know how my prices compares to the item with the highest price in the same category

1.  SELECT
    prod_id,
    price,
    category,
    last_value( price )OVER(
    PARTITION BY category
    ORDER by price
    range BETWEEN UNBOUNDED PRECEDING and UNBOUNDED FOLLOWING
    ) as "most expensive in category"
    From "public"."products"

2.  SELECT
    prod_id,
    price,
    category,
    max( price )OVER(
    PARTITION BY category
    ) as "cheapest in category"
    From "public"."products"

# Lesson 16. SUM

https://academy.zerotomastery.io/courses/1073491/lectures/23610045

Getting the sum in a group depending on the framing. I want to see cumulately a customer has order in our store

SELECT
o.orderid,
o.customerid,
o.netamount,
sum(o.netamount) over (
PARTITION BY o.customerid
order by o.orderid
)
FROM orders AS o
order by o.customerid

# Lesson 17. ROW_NUMBER

https://academy.zerotomastery.io/courses/1073491/lectures/23610042

Number the current rawwithin the partition starting from 1 regarless of framing
I want to know where my product is potitioned in the category by price

# Lesson 17. Window Function Exercises

https://academy.zerotomastery.io/courses/1073491/lectures/23659466

1. Show the population per continent
   Database: World
   Table: Country

SELECT
DISTINCT continent,
SUM(population) OVER w1 as"continent population"
FROM country
WINDOW w1 AS( PARTITION BY continent );

2.  To the previous query add on the ability to calculate the percentage of the world population
    What that means is that you will divide the population of that continent by the total population and multiply by 100 to get a percentage.
    Make sure you convert the population numbers to float using `population::float` otherwise you may see zero pop up

Database: World
Table: Country

SELECT
DISTINCT continent,
SUM(population) OVER w1 as"continent population",
CONCAT(
ROUND(
(
SUM( population::float4 ) OVER w1 /
SUM( population::float4 ) OVER()
) \* 100  
 ),'%' ) as "percentage of population"
FROM country
WINDOW w1 AS( PARTITION BY continent );

3.  Count the number of towns per region

Database: France
Table: Regions (Join + Window function)

SELECT
DISTINCT r.id,
r."name",
COUNT(t.id) OVER (
PARTITION BY r.id
ORDER BY r."name"
) AS "# of towns"
FROM regions AS r
JOIN departments AS d ON r.code = d.region
JOIN towns AS t ON d.code = t.department
ORDER BY r.id;

# Lesson 18. Conditional Statements

https://academy.zerotomastery.io/courses/1073491/lectures/23173279

# Lesson 19. Conditional Statement Exercise

Database: Store
Table: products
Create a case statement that's named "price class" where if a product is over 20 dollars you show 'expensive'
if it's between 10 and 20 you show 'average'
and of is lower than or equal to 10 you show 'cheap'.

SELECT prod_id, title, price,
CASE  
 WHEN price > 20 THEN 'expensive'
WHEN price <= 10 THEN 'cheap'
WHEN price BETWEEN 10 and 20 THEN 'average'
END AS "price class"
FROM products

# Lesson 20. NULLIF

https://academy.zerotomastery.io/courses/1073491/lectures/23173280

# Lesson 21. NULLIF Exercise

https://academy.zerotomastery.io/courses/1073491/lectures/25317958

- DB: Store
- Table: products
- Question: Show NULL when the product is not on special (0)

SELECT prod_id, title, price, NULLIF(special, 0) as "special"
FROM products

# Lesson 22. Views...What Are They Good For?

https://academy.zerotomastery.io/courses/1073491/lectures/23610040

<Views> allows us to store and query prviously run queries

**type of views:**

- Materialized
- Non-materialized

# Lesson 23. View Syntax

https://academy.zerotomastery.io/courses/1073491/lectures/23173281

<Views> are the output of the query we ran
<Non-materialized Views> take very little space to store. We only store de definition of a view not all the data that it returns. Most of the time we will work this this type of views.

# Lesson 24. Using Views

https://academy.zerotomastery.io/courses/1073491/lectures/23173283

**STEPS:**

1. Run query to select the last date the salary changed:

SELECT
e.emp_no,
max(s.from_date)

from salaries AS s

JOIN employees AS e USING (emp_no)
JOIN dept_emp AS de USING (emp_no)
JOIN departments AS d USING (dept_no)

GROUP BY e.emp_no
ORDER BY e.emp_no

2. Create a View of the query:

CREATE or REPLACE view last_salary_change AS
SELECT
e.emp_no,
max(s.from_date)

from salaries AS s

JOIN employees AS e USING (emp_no)
JOIN dept_emp AS de USING (emp_no)
JOIN departments AS d USING (dept_no)

GROUP BY e.emp_no
ORDER BY e.emp_no

3. Check the view. Run previous query:
   SELECT \* FROM last_salary_change

4. Solve the last salary change problem using <views>:

SELECT s.emp_no, d.dept_name, s.from_date, s.salary
FROM last_salary_change

JOIN salaries AS s USING (emp_no)
JOIN dept_emp AS de USING (emp_no)
JOIN departments AS d USING (dept_no)

where max = s.from_date

N: max is the name of the column we create we ran the first query in order to dinf the last date our salary changed. So we match that to from_date column in salary table and we are goint to filter all the data me need to check who is the employee, the department and the salary

**PROS:**

- Join sintax withfiltering is easier to read.
- It is easier to reason about

**DRAWBACK:**

- You have to create a view.

# Lesson 25. Views Exercises

1. Exercise:

- Create a view "90-95" that:
- Shows me all the employees, hired between 1990 and 1995
- Database: Employees

Answer:
CREATE VIEW "90-95" AS
SELECT \*
FROM employees as e
WHERE EXTRACT (YEAR FROM e.hire_date) BETWEEN 1990 AND 1995
ORDER BY e.emp_no;

2. Exercise

- Create a view "bigbucks" that:
- Shows me all employees that have ever had a salary over 80000
- Database: Employees

Answer:
CREATE VIEW "bigbucks" AS
SELECT e.emp_no, s.salary
FROM employees as e
JOIN salaries as s USING(emp_no)
WHERE s.salary > 80000
ORDER BY s.salary;

# Lesson 26. Indexes

https://academy.zerotomastery.io/courses/1073491/lectures/23173282

<INDEX> is a construct to improve query performance

**Types of indexes:**

- Single-column
- Multi-column
- Unique
- Partial
- Implicit indexes

**When to use index:**

- Index foreign key
- Index primary key and unique columns
- Index on a column that end up in the order by/where clause often

**When NOT to use index:**

- Don't add an index just to add an index
- Don't use index in small tables
- Dont't use on thable that are updated frequently
- Don't use in columns that can contain null values
- Don't use in columns that have large values

# Lesson 27. Index Types

https://academy.zerotomastery.io/courses/1073491/lectures/23547534

# Lesson 28. Index Algorithms

https://academy.zerotomastery.io/courses/1073491/lectures/23547533

# Lesson 29. What Are Subqueries?

https://academy.zerotomastery.io/courses/1073491/lectures/23610044

<Subquerie> It is a query within another SQL query, most often in the WHERE clause

# Lesson 30. Subqueries vs Joins

https://academy.zerotomastery.io/courses/1073491/lectures/23547532

- Both Subqueries and joins combines data from different tables.
- Subqueries are queries that could stand alone.
- Joins combines rows from one or more tables based on a match condiction.
- Subqueries can return a single result or a row set.
- Joins only return a row set.
- A joined table can be used in a outer query

# Lesson 31. Subquery Guidelines As Types

https://academy.zerotomastery.io/courses/1073491/lectures/23547536

- Subquery must be enclosed in parentheses
- Most be placed on the right side of the comparison operator.
- Can not manipulate the results internally.
- Use single row operators with single row subqueries.
- Subqueries that returns null might not return any result.

**Types of subqueries:**

- Single row
- Multiple row
- Multiple column
- Correlated
- Nested

# Lesson 32. Using Subqueries

https://academy.zerotomastery.io/courses/1073491/lectures/23547535

1. Show all the employees older than the average age

SELECT
first_name,
last_name,
birth_date,
age(birth_date) AS "age",
(SELECT AVG(age(birth_date)) FROM employees) as "average"
from employees
WHERE age(birth_date) > (SELECT AVG(age(birth_date)) FROM employees)

2. Show all the male employees older than the average age:

SELECT
first_name,
last_name,
birth_date,
age(birth_date) AS "age",
(SELECT AVG(age(birth_date)) FROM employees) as "average"
from employees
WHERE age(birth_date) > (SELECT AVG(age(birth_date)) FROM employees where gender = 'M')

3. Show me the title by salary of each employee

SELECT
emp_no,
salary,
from_date,
(SELECT title from titles as t
refering from outside - correlated subquery
where t.emp_no = s.emp_no and t.from_date = s.from_date
)
from salaries as s
Order by emp_no

- We can get the same effect using outer join and it is a simplier query:

SELECT
emp_no,
salary,
from_date,
t.title
from salaries as s
left outer JOIN titles as t using (emp_no, from_date)
Order by emp_no

- This is another way to resolve this request, in this case it will only show the current title of the employee:

SELECT
emp_no,
salary,
from_date,
t.title
from salaries as s
JOIN titles as t using (emp_no, from_date)
Order by emp_no

**Title for employees**
In the video "Using Subqueries" we see a query where we try to apply combine titles with salaries to see the salary changes per title live. In the video "Inner Join" we stated that each title change happens 2 days AFTER a salary bump.

Our query did not take this fact into account and so for each employee we would only see the initial title, but not the subsequent title changes. In order to address this we need to add the following to the query:

select emp_no, salary, from_date,
(select title from titles as t
where t.emp_no=s.emp_no and
(t.from_date = s.from_date + interval '2 days' or t.from_date=s.from_date))
from salaries as s
order by emp_no;

This will catch both the cases where the initial title was given and any salaries linked to a subsequent title change!

# Lesson 33. Getting The Latest Salaries

https://academy.zerotomastery.io/courses/1073491/lectures/23547537

1. Subquery in WHERE CLAUSE
   select
   emp_no,
   salary as "most recent salary",
   from_date
   from salaries as s
   where from_date = (
   SELECT MAX(from_date)
   from salaries as sp
   where sp.emp_no = s.emp_no
   )
   ORDER by emp_no ASC

- This is take a lot of time

2. Subquery in the join:

select
emp_no,
salary as "most recent salary",
from_date
from salaries as s
JOIN (
SELECT emp_no, MAX(from_date) as "max"
from salaries as sp
GROUP by emp_no
) as ls USING (emp_no)
where ls.max = from_date
ORDER by emp_no ASC

- This is cost less time than the previous one

# Lesson 34. Subquery Operators

https://academy.zerotomastery.io/courses/1073491/lectures/23547531

# Lesson 35. Subquery Exercises

https://academy.zerotomastery.io/courses/1073491/lectures/23659498

1. exercise

- DB: Store
- Table: orders
- Question: Get all orders from customers who live in Ohio (OH), New York (NY) or Oregon (OR) state
- ordered by orderid

Answer:
SELECT c.firstname, c.lastname, o.orderid
FROM orders AS o, (
SELECT customerid, state, firstname, lastname
FROM customers
) AS c
WHERE o.customerid = c.customerid AND
c.state IN ('NY', 'OH', 'OR')
ORDER BY o.orderid;

2. Exercise:

- DB: Employees
- Table: employees
- Question: Filter employees who have emp_no 110183 as a manager

SELECT emp_no, first_name, last_name
FROM employees
WHERE emp_no IN (
SELECT emp_no
FROM dept_emp
WHERE dept_no = (
SELECT dept_no
FROM dept_manager
WHERE emp_no = 110183
)
)
ORDER BY emp_no

-- Written with JOIN
SELECT e.emp_no, first_name, last_name
FROM employees as e
JOIN dept_emp as de USING (emp_no)
JOIN dept_manager as dm USING (dept_no)
WHERE dm.emp_no = 110183
