## Chapter 04. SQL Deep Dive

# Lesson 1. Starting With Query

https://academy.zerotomastery.io/courses/1073491/lectures/23648641

- Check SQL Commands image

# Lesson 2. Exercise: Simple Queries

https://academy.zerotomastery.io/courses/1073491/lectures/23176812

# lesson 3. Changing Column Names in a SELECT Query

https://academy.zerotomastery.io/courses/1073491/lectures/25322256

Ex:
SELECT emp_no AS "Employee #" FROM "public"."employees"

# Lesson 4. Concat Function

https://academy.zerotomastery.io/courses/1073491/lectures/23176802

- Put columns together in a single column

  EX:
  SELECT CONCAT (emp_no, ' ', title) from "public"."titles"
  SELECT CONCAT (emp_no, ' is a ', title) from "public"."titles"

* With single quote we can insert something between the concated columns

SELECT CONCAT (emp_no, ' is a ', title) AS "Employee title" from "public"."titles"

- We need to rename the column

Exercise:
SELECT CONCAT(first_name , ' ', last_name) AS "Name and Lastname" FROM "public"."employees"

- This is only query the data but it does not change the data.

# Lesson 5. What Is A Function In SQL?

https://academy.zerotomastery.io/courses/1073491/lectures/23176805

# Lesson 6. Aggregate Functions

https://academy.zerotomastery.io/courses/1073491/lectures/23176798

This are high level functions that allows us to change the data we retrieve from the database in a query, just like the exmaple in Lesson 4. There are many functions. This website shows them:
https://www.postgresql.org/docs/12/functions-aggregate.html

# Lesson 7. Exercise: Aggregate Functions

https://academy.zerotomastery.io/courses/1073491/lectures/23658992

--
/\*

- What database should I use for these exercises?
- Name: Employees
  \*/
  --

-- Question 1: What is the average salary for the company?
-- Table: Salaries
-- Result: 63810.744836143706
select avg(salary) from salaries;

-- Question 2: What year was the youngest person born in the company?
-- Table: employees
-- Result: 1965-02-01
select max(birth_date) from employees;

--
/\*

- What database should I use for these exercises?
- Name: France
  \*/
  --

-- Question 1: How many towns are there in france?
-- Table: Towns
-- Result: 36684
select count(id) from towns;

--
/\*

- What database should I use for these exercises?
- Name: World
  \*/
  --

-- Question 1: How many official languages are there?
-- Table: countrylanguage
-- Result: 238
select count(countrycode) from countrylanguage
where isofficial = true;

-- Question 2: What is the average life expectancy in the world?
-- Table: country
-- Result: 66.48603611164265
select avg(lifeexpectancy) from country;

-- Question 3: What is the average population for cities in the netherlands?
-- Table: city
-- Result: 185001
select AVG(population) from city
where countrycode = 'NLD';

# Lesson 8. Commenting Your Queries

https://academy.zerotomastery.io/courses/1073491/lectures/23176807

EX:
SELECT first_name, last_name FROM "public"."employees" where first_name = 'Mayumi' AND last_name = 'Schueller'

- First Select the columns, then table (FROM) and then filter the result (where first_name = 'Mayumi' AND last_name = 'Schueller'). By using AND we can look in different tables.

* Example of query with comments:

-- Select statement to Filter Mayumi Schueller
SELECT first*name, last_name FROM "public"."employees"
/*
Filter on first name and last name to limit the amoung of data returned
and focus the filtering on a single person
\_/

where first_name = 'Mayumi' AND last_name = 'Schueller';--filtering here on Mayumo Schueller

# Lesson 9. Common SELECT Mistakes

https://academy.zerotomastery.io/courses/1073491/lectures/24413385

# Lesson 10. Filtering Data

https://academy.zerotomastery.io/courses/1073491/lectures/23176811

- Get just a subset of the data, just the one we need

# Lesson 11. AND and OR

https://academy.zerotomastery.io/courses/1073491/lectures/23176808

AND used in filtering we can chain multiple criteria to be met in a single row of data

Example of using AND to select a single row of data:

SELECT first_name, last_name, hire_date FROM "public"."employees"
Where first_name = 'Georgi' AND last_name = 'Facello' AND hire_date = '1986-06-26';

AND and OR Example:

SELECT first_name, last_name, hire_date FROM "public"."employees"
Where (first_name = 'Georgi' AND last_name = 'Facello' AND hire_date = '1986-06-26')
OR (first_name = 'Bezalel' and last_name = 'Simmel');

- Order of opearation is important. After the WHERE SQL will change all the AND condictions until it hits OR. With OR SQL start looking a different condictions (filter). The parenthesis helps to see what is happening and in what order

# Lesson 12. Exercise: Filtering Data

https://academy.zerotomastery.io/courses/1073491/lectures/23176804

Question:
How many female customers do we have from the state of Oregon (OR) and New York (NY)?

Answer:
Result:200
SQL:
long version:
SELECT count(customerid) FROM "public"."customers"
WHERE (state = 'OR' AND gender = 'F')
OR (state = 'NY' AND gender = 'F');

short version:
SELECT count(customerid) FROM "public"."customers"
WHERE (state = 'OR' OR state = 'NY')
AND gender = 'F';

- The parenthesis goes into boolean algebra. the AND After this parenthesis will be applied for both used cases!

# Lesson 13. The NOT Keyword

https://academy.zerotomastery.io/courses/1073491/lectures/23176803

- NOT keyword remove results

Exercise:
How many customers aren't 55

SQL:
SELECT count(customerid) FROM "public"."customers"
WHERE NOT age = 55;

# Lesson 14. Comparison Operators

https://academy.zerotomastery.io/courses/1073491/lectures/24413386

N: This are just operators as I learned in python and javascript!

# Lesson 15. Exercise: Comparison Operators

https://academy.zerotomastery.io/courses/1073491/lectures/23660925

Questions:

1. How many female customers do we have from the state of Oregon (OR)?
2. Who over the age of 44 has an income of 100 000 or more?
3. Who between the ages of 30 and 50 has an income of less than 50 000?
4. What is the average income between the ages of 20 and 50?

Answer:

- All the Query are done in Store database and table customers

1.  SELECT count(customerid) FROM "public"."customers"
    WHERE state = 'OR' AND gender = 'F';

2.  SELECT count(customerid) FROM "public"."customers"
    WHERE age > 44 AND income >=100000;

3.  SELECT firstname FROM "public"."customers"
    WHERE (age > 30 AND age < 50) AND income < 50000;

SELECT avg(income) FROM "public"."customers"
WHERE (age > 20 AND age < 50);

# Lesson 16. Logical Operators

https://academy.zerotomastery.io/courses/1073491/lectures/23176797

- Check out image of operators precedence

Check this website for logical operators:
https://www.postgresql.org/docs/12/sql-syntax-lexical.html#SQL-PRECEDENCE

# Lesson 17. Operator Precedence 2

https://academy.zerotomastery.io/courses/1073491/lectures/23176801

# Lesson 18. Exercise: Operator Precedence

https://academy.zerotomastery.io/courses/1073491/lectures/23659131

Exercises:

1. Select people either under 30 or over 50 with an income above 50000 that are from either Japan or Australia
2. What was our total sales in June of 2004 for orders over 100 dollars?

Answers:

1.  SELECT firstname, country, age, income FROM "public"."customers"
    WHERE (age < 30 OR age > 50)
    AND (country = 'Japan' OR country = 'Australia')
    AND income > 50000;

2.  SELECT SUM(totalamount) from "public"."orders"
    WHERE (orderdate >= '2004-06-01' AND orderdate <= '2004-06-30')
    AND totalamount > 100

# Lesson 19. Checking For NULL Values

https://academy.zerotomastery.io/courses/1073491/lectures/23267547

NULL is represent empty or missing values

# Lesson 20. IS Keyword

https://academy.zerotomastery.io/courses/1073491/lectures/23267543

IS operator allows to filter on values that are NULL, NOT NULL, TRUE OR FALSE

EX:
SELECT \* FROM Users
WHERE age = 20 is FALSE;

SELECT name FROM Students
WHERE name IS NOT NULL;

# Lesson 21. NULL Coalescing

https://academy.zerotomastery.io/courses/1073491/lectures/23267544

N: Clean up your data. Replace NULL values

Ex: SELECT coalesce (<column>, 'Empty') AS column_alias FROM <table>

# Lesson 22. Exercise: Null Value Coalescing

https://academy.zerotomastery.io/courses/1073491/lectures/23659158

DB: https://www.db-fiddle.com/f/PnGNcaPYfGoEDvfexzEUA/0

Question:

1. Assuming a students minimum age for the class is 15, what is the average age of a student?

Answer:
SELECT avg(coalesce(age, 15)) FROM "Student";

2. Question:
   Replace all empty first or last names with a default?

Answer:
SELECT id, coalesce(name, 'fallback'), coalesce(lastName, 'lastName'), age FROM "Student";

- This query gives us back a substitute value for NULL in the selected columns

# Lesson 23. 3 Valued Logic

https://academy.zerotomastery.io/courses/1073491/lectures/23267545

N: Besides TRUE or FALSE, the result of logical expressions can also be unknown (NULL). in programing usually NULL is equal to FALSE but is SQL there is slighty different.
NULL could be anything that is why we use IS NULL check

EX:
SELECT \* FROM "Student"
WHERE (age is null) OR (age IS NOT null);

- Here all the data is return

# Lesson 24. Exercise: 3 Valued Logic

https://academy.zerotomastery.io/courses/1073491/lectures/23659286

1. DB: Store
   Table: customers
   Question: adjust the following query to display the null values as "No Address"

Answer:
SELECT COALESCE(address2, 'No Address') FROM "public"."customers"

2. DB: Store
   Table: customers
   Question: Fix the following query to apply proper 3VL

SELECT \*
FROM customers
WHERE COALESCE(address2, null) IS NOT null;

Answer:
SELECT \*
FROM "public"."customers"
WHERE address2 IS NOT null;

3. DB: Store
   Table: customers
   Question: Fix the following query to apply proper 3VL

SELECT coalesce(lastName, 'Empty'), \* from customers
where (age = null);

Answer:

SELECT coalesce(lastname, 'Empty'), \* from "public"."customers"
where (age IS null);

# Lesson 25. BETWEEN + AND

https://academy.zerotomastery.io/courses/1073491/lectures/23267546

N: It is more readable and maintabable to select range of data

# Lesson 26. Exercise: BETWEEN + AND

https://academy.zerotomastery.io/courses/1073491/lectures/24603302

1. Exercise. Question:
   Who between the ages of 30 and 50 has an income less than 50 000?

Answer:
SELECT \*
FROM "public"."customers"
WHERE (age BETWEEN 30 AND 50)
AND income < 50000;

2. Exercise. Question
   What is the average income between the ages of 20 and 50? (Including 20 and 50)

Answer:
SELECT avg(income)
FROM "public"."customers"
WHERE (age BETWEEN 20 AND 50);

# Lesson 27. IN Keyword

https://academy.zerotomastery.io/courses/1073491/lectures/23421019

IN keyword is used to check if a value match any value in a list of values

SQL structure
SELECT \*
FROM <table>
WHERE <column> IN (value1, value2,...)

Ex:
SELECT \* FROM "public"."employees"
WHERE emp_no IN (100001, 100006, 11008);

# Lesson 28. Exercise: IN Keyword

https://academy.zerotomastery.io/courses/1073491/lectures/23659329

1. Exercise:
   DB: Store
   Table: orders
   Question: How many orders were made by customer 7888, 1082, 12808, 9623

Answer:
SELECT count(orderid)
FROM "public"."orders"
WHERE customerid IN (7888, 1082, 12808, 9623);

2. Exercise:
   DB: World
   Table: city
   Question: How many cities are in the district of Zuid-Holland, Noord-Brabant and Utrecht?

Answer:
select count(id) from "public"."city"
where district IN ('Zuid-Holland', 'Noord-Brabant', 'Utrecht');

# Lesson 29. LIKE

https://academy.zerotomastery.io/courses/1073491/lectures/23334911

N: Select something based in partial reference

Ex:
SELECT firstname
FROM "employee"
WHERE firstname LIKE 'M%'

- This will select start with M

N: This is called _pattern matching_

Ex:
SELECT \* FROM "public"."employees"
WHERE first_name LIKE 'G%';

We need to build the patterns:
% means everything
\_ means just one character

- Check the image of pattern maching

Ex:
SELECT \* FROM "public"."employees"
WHERE first_name LIKE 'G%er';

Postgres LIKE only does text comparison so we must cast whatever we use to text

There are two way to make it text:
CAST(salary AS text)
salary::text

ILIKE is a insensitive keyword. It match the character regarless is capital letters or small letters

Ex:
SELECT \* FROM "public"."employees"
WHERE first_name ILIKE 'G%ER';

# Lesson 30. Exercise: Like Keyword

https://academy.zerotomastery.io/courses/1073491/lectures/23659337

1. Exercise:
   DB: Employees
   Table: employees
   Question: Find the age of all employees who's name starts with M.
   Sample output: https://imgur.com/vXs4093
   Use EXTRACT (YEAR FROM AGE(birth_date)) we will learn about this in later parts of the course

SELECT ..., EXTRACT (YEAR FROM AGE(birth_date)) as "age" FROM employees;

Answer:
SELECT \*, EXTRACT (YEAR FROM AGE(birth_date)) as "age" FROM "public"."employees"
WHERE first_name LIKE 'M%';

2. Exercise:
   DB: Employees
   Table: employees
   Question: How many people's name start with A and end with R?
   Expected output: 1846

Answer:
SELECT count(emp_no) FROM "public"."employees"
WHERE first_name ILIKE 'A%R';

3. Exercise:
   DB: Store
   Table: customers
   Question: How many people's zipcode have a 2 in it?.
   Expected output: 4211

Answer:
SELECT count(customerid) FROM "public"."customers"
WHERE zip::text LIKE '%2%';

4. Exercise:
   DB: Store
   Table: customers
   Question: How many people's zipcode start with 2 with the 3rd character being a 1.
   Expected output: 109

Answer:
SELECT count(customerid) FROM "public"."customers"
WHERE zip::text LIKE '2_1%';

5. Exercise:
   DB: Store
   Table: customers
   Question: Which states have phone numbers starting with 302?
   Replace null values with "No State"
   Expected output: https://imgur.com/AVe6G4c

Answer:
SELECT COALESCE(state, 'No State') as "State", phone FROM "public"."customers"
WHERE phone::text LIKE '302%';

# Lesson 31. Dates And Timezones

https://academy.zerotomastery.io/courses/1073491/lectures/23334913

UTC stands for Universal Coordinate Time. There is no territory, country that uses UTC. It is a global time

# Lesson 32. Setting Up Timezones

https://academy.zerotomastery.io/courses/1073491/lectures/23334918

N: What a pain in the ass to set the time zone in Valentina to UTC. It didn't work as the tutorial:
ALTER USER carlosinfante SET timezone TO 'UTC';

- carlosinfante is the user in my mac but it didn't work. Instead I had to use <postgres> as a user:

ALTER USER postgres SET timezone TO 'UTC';

- This bug kept me busy the whole weekend!

# Lesson 33. How Do We Format Date And Time?

https://academy.zerotomastery.io/courses/1073491/lectures/23457694

N: Postgres uses ISO-8601 as a norm for the dates:

YYYY-MM-DDTHH:MM:SS
2017-06-15T12:45:15+02:00

+02:00 means 2 hours more of the UTC, the timezome where the persone is located. This is optional, if it is not given then it will assume that is in UTC.

- FORMAT is a way to represent date and time.

# Lesson 34. Timestamps

https://academy.zerotomastery.io/courses/1073491/lectures/23334914

TIMESTANDS is a date with a time and potentially TIMEZONE information

SQL to create a table with time stand in Employees database
CREATE TABLE timezones (
ts TIMESTAND WITHOUT TIME ZONE,
tz TIMESTAND WITH TIME ZONE
)

SQL to insert values in a table. This values are time stands:

INSERT into timezones values (
TIMESTAND WITHOUT TIME ZONE '2020-08-10 10:00:00-05',
TIMESTAND WITH TIME ZONE '2020-08-10 10:00:00-05',
);

- I got an error when I tried to create the table, at this point is not really important. What I need to know is that the time stand could be store with or without time zone. It depends of what need need.

# Lesson 36. Date Functions

https://academy.zerotomastery.io/courses/1073491/lectures/23334917

CURRENT DATE. There are two way:

SELECT NOW()::date;
SELECT CURRENT_DATE;

FORMAT:
SELECT TO_CHAR(CURRENT_DATE, 'dd/mm/yyyy');

In This website we cand find the functions and the identifiers:
https://www.postgresql.org/docs/16/functions-formatting.html

# Lesson 37. Date Difference And Casting

https://academy.zerotomastery.io/courses/1073491/lectures/23334910

SUNSTRACTIN DATES:

SELECT NOW() - '1800-01-01'

N: This return the amount of days and time

CASTING DATE (converting the date into a ISO-8601):

SELECT date '2002/01/31'

# Lesson 38. Age Calculation

https://academy.zerotomastery.io/courses/1073491/lectures/23334916

- age function returns the amoung of date, there is no time included in the respond.

Example to calculate age
SELECT age(date '1800-01-01');

- <age> is the keyword for the calculation
- We need always to cast the date (using date) to avoid errors

Example to calculate difference between two dates:
SELECT age(date '2021-01-01', date '1800-01-01');

# Lesson 39. Extracting Information

https://academy.zerotomastery.io/courses/1073491/lectures/23334909

Examples:

SELECT EXTRACT (DAY from date '2020/01/13') AS DAY;

SELECT EXTRACT (MONTH from date '2020/01/13') AS MONTH;

SELECT EXTRACT (YEAR from date '2020/01/13') AS YEAR;

Trunc the year:
SELECT date_trunc('YEAR', date '2024/02/19');

- This will set the date to the lower possible value, which means it will return Janueary 1rst 2023 (2024-01-01)

# Lesson 40. Intervals

https://academy.zerotomastery.io/courses/1073491/lectures/23334919

INTERVALS allow us to write queries in a ny that mirrow language

Ex:
SELECT \*
FROM orders
WHERE purchaseDate <= now() - interval '30 days';

- Extract Intervals:
  SELECT
  EXTRACT (
  year FROM
  interval '5 years 5 monts'
  )

# Lesson 41. Exercise: Date and Timestamp

1. Exercise:
   DB: Employees
   Table: employees
   Question: Get me all the employees above 60, use the appropriate date functions

Answer:

SELECT AGE(birth_date), \* FROM employees
WHERE (
EXTRACT (YEAR FROM AGE(birth_date))
) > 64;

2. Exercise:
   DB: Employees
   Table: employees
   Question: How many employees where hired in February?

Answer:
SELECT count( emp_no ) FROM "public"."employees"
where EXTRACT (MONTH FROM hire_date) = 2;

3. Exercise:
   DB: Employees
   Table: employees
   Question: How many employees were born in november?

Answer:
SELECT count( emp_no ) FROM "public"."employees"
where EXTRACT (MONTH FROM birth_date) = 11;

4. Exercise:
   DB: Employees
   Table: employees
   Question: Who is the oldest employee? (Use the analytical function MAX)

Answer:
SELECT MAX(AGE(birth_date)) FROM employees;

- The SQL above returns the age of the older person but it does not tell who is the older person. For that prpose, it is needed the following SQL:

SELECT \*
FROM "public"."employees"
WHERE birth_date = (
SELECT MAX(birth_date)
FROM "public"."employees"
);

5. Exercise:
   DB: Store
   Table: orders
   Question: How many orders were made in January 2004?

Answer:
SELECT COUNT(orderid)
FROM orders
WHERE DATE_TRUNC('month', orderdate) = date '2004-01-01';

# Lesson 42. DISTINCT

https://academy.zerotomastery.io/courses/1073491/lectures/23334912

DISTINCT removes duplicates

# Lesson 43. Exercise: Distinct Keyword

https://academy.zerotomastery.io/courses/1073491/lectures/23659394

1. Exercise:
   DB: Employees
   Table: titles
   Question: What unique titles do we have?

Answer:
SELECT DISTINCT title FROM "public"."titles"

2. Exercise:
   DB: Employees
   Table: employees
   Question: How many unique birth dates are there?

Answer:
SELECT count(DISTINCT birth_date) FROM "public"."employees"

3. Exercise:
   DB: World
   Table: country
   Question: Can I get a list of distinct life expectancy ages
   Make sure there are no nulls

Answer:
SELECT DISTINCT lifeexpectancy FROM "public"."country"
WHERE lifeexpectancy IS NOT NULL
ORDER BY lifeexpectancy;

# Lesson 44. Sorting Data

https://academy.zerotomastery.io/courses/1073491/lectures/23334915

Ex:
SELECT \* FROM customers
ORDER BY name ASC

SELECT \* FROM customers
ORDER BY name DESC

N: In ORDER BY if ASC by default!

# Lesson 45. Exercise Sorting Data

https://academy.zerotomastery.io/courses/1073491/lectures/24696445

1. Exercise:
   DB: Employees
   Table: employees
   Question: Sort employees by first name ascending and last name descending

Answer:
SELECT \* FROM "public"."employees"
ORDER BY first_name, last_name DESC;

2. Exercise:
   DB: Employees
   Table: employees
   Question: Sort employees by age

Answer:
SELECT \* FROM "public"."employees"
ORDER BY birth_date;

3. Exercise:
   DB: Employees
   Table: employees
   Question: Sort employees who's name starts with a "k" by hire_date

Answer:
SELECT \* FROM "public"."employees"
where first_name ILIKE 'k%'
ORDER BY hire_date;

# Lesson 46. Multi Table SELECT

https://academy.zerotomastery.io/courses/1073491/lectures/23421020

Ex:
SELECT a.emp_no, b.salary, b.from_date
FROM "public"."employees" AS a, "public"."salaries" AS b
WHERE a.emp_no = b.emp_no
order by a.emp_no;

# Lesson 47. Inner Join

https://academy.zerotomastery.io/courses/1073491/lectures/23544274

- Check image of Inner Join

* Inner Join is a more readable syntax that join table using WHERE like in the previous lesson.

Ex:
SELECT a.emp_no,
CONCAT(a.first_name, ' ', a.last_name) AS "name",
b.salary
FROM "public"."employees" AS a
INNER JOIN "public"."salaries" AS b ON b.emp_no = a.emp_no
ORDER BY a.emp_no

When we do join, the results is not order so we have to do that our selves in the query

# Lesson 48. Self Join

https://academy.zerotomastery.io/courses/1073491/lectures/23544272

It is not so common. It is join a table to itself

# Lesson 49. Outer Join

https://academy.zerotomastery.io/courses/1073491/lectures/23544275

N: Outer Join add the data that does not match

# Lesson 50. Less Common Joins

https://academy.zerotomastery.io/courses/1073491/lectures/23544276

# Lesson 51. Exercise: Inner-Join

https://academy.zerotomastery.io/courses/1073491/lectures/23659435

1. Exercise:
   DB: Store
   Table: orders
   Question: Get all orders from customers who live in Ohio (OH), New York (NY) or Oregon (OR) state
   ordered by orderid

Answer:
SELECT c.firstname, c.lastname, o.orderid
FROM orders AS o
INNER JOIN customers AS c ON o.customerid = c.customerid
WHERE c.state IN ('NY', 'OH', 'OR')
ORDER BY o.orderid;

2. Exercise:
   DB: Store
   Table: products
   Question: Show me the inventory for each product

Answer:
SELECT p.prod_id, i.quan_in_stock
FROM products as p
INNER JOIN inventory AS i ON p.prod_id = i.prod_id

3. Exercise:
   DB: Employees
   Table: employees
   Question: Show me for each employee which department they work in

Answer:
SELECT e.first_name, dp.dept_name
FROM employees AS e
INNER JOIN dept_emp AS de ON de.emp_no = e.emp_no
INNER JOIN departments AS dp ON dp.dept_no = de.dept_no;

N: Last one s more comple coz I need to join 3 tables!

# Lesson 52. USING Keyword

https://academy.zerotomastery.io/courses/1073491/lectures/23544273

N: Simplying Join syntax. Comparing a primary Key to foreign key
Ex:
SELECT e.emp_no, e.first_name, de.dept_no
From employees AS e
INNER JOIN dept_emp AS de USING(emp_no);
