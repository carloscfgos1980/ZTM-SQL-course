## Chapter 02. Database SQL Fundamentals

# Lesson 1. SQL Playground

https://academy.zerotomastery.io/courses/1073491/lectures/23648639

Website for SQL play ground
https://www.db-fiddle.com

# Lesson 2. What Is SQL?

https://academy.zerotomastery.io/courses/1073491/lectures/23171548

SQL: It is a programming language to talk to database.
DAtabese: Structure set of data

# Lesson 3. What Is A Query?

https://academy.zerotomastery.io/courses/1073491/lectures/24413384

Query means in English as cuestion.

Playground to understand SQL:
https://www.db-fiddle.com/f/ogAiTgZPjwvDxwVHiVK3Ek/0

**query breakdown**
SELECT "Name"
FROM "Users"
WHERE "Role" = "Manager"

SELECT is the column, FROM is the table, and WHERE is the condiction. So this query is filtering the result

SELECT is the keyword and "Name" is the identifier
"Role" = "Manager" is the condiction and "Manager" the expression

This is the SQL that I ran in fiddle.com. It took me a while to work coz it must use single quotes

Examples:
SELECT \* FROM "User"
SELECT \* FROM "User" WHERE role = 'employee'
SELECT name, lastname FROM "User" WHERE role = 'employee'

- First example select everything from table Users,
- Second one select all the columns from users but filtering role equal to employee
- Third example Select only the specific columns (name, lastname) from the table Users and filtering role equal to employee.

# Lesson 4. Imperative vs Declarative

https://academy.zerotomastery.io/courses/1073491/lectures/23171565

# Lesson 5. History of SQL

https://academy.zerotomastery.io/courses/1073491/lectures/23171554

# Lesson 6. SQL Standards

https://academy.zerotomastery.io/courses/1073491/lectures/23171564

# Lesson 7. What Is A Database? Revisited

https://academy.zerotomastery.io/courses/1073491/lectures/23171546

# Lesson 8. Exercise: SQL Starter Quiz

https://academy.zerotomastery.io/courses/1073491/lectures/23656696

# LEsson 9. Database Models

https://academy.zerotomastery.io/courses/1073491/lectures/23633824

# Lesson 10. Hierarchical And Networking Model

https://academy.zerotomastery.io/courses/1073491/lectures/23171562

N: This are outdated models

# Lesson 11. Relational Model

https://academy.zerotomastery.io/courses/1073491/lectures/23171551

N: Check the image of Relational Model!

# Lesson 12. DBMS Revisited

https://academy.zerotomastery.io/courses/1073491/lectures/23171549

DBMS stands for Database Management System. There are different companies that develop softwares to manage database. There are some difference among them but they all use SQL

# Lesson 13. Relational Model Revisited

https://academy.zerotomastery.io/courses/1073491/lectures/23171561

# Lesson 14. Tables

https://academy.zerotomastery.io/courses/1073491/lectures/23171567

Table is a Collection of Columns and rows

# Lesson 15. Columns

https://academy.zerotomastery.io/courses/1073491/lectures/23171553

Degree: Colection of columns. Each colum storage type of data
Domain or constrain or atributes: type of data that a column can store. People could use this 3 words as synonymous

# Lesson 16. Rows

https://academy.zerotomastery.io/courses/1073491/lectures/23171559

N: Another word for row is tupple. Each and every tupple has to follow the columns' contrains
Cardinality: Collection or rows (tupples).

# Lesson 17. Primary And Foreign Keys

https://academy.zerotomastery.io/courses/1073491/lectures/23171558

Primary key: Something to unique identifier of your data, each row.

- Check image: Primary and Foreign Key

* Foreign Key: It is a reference a unique identifier from a different table. With this relationship is possible to inject data to the main table.

# Lesson 18. OLTP vs OLAP

https://academy.zerotomastery.io/courses/1073491/lectures/23171550

- OLTP: Online Transaccion Processes. Day to day transaccion ex: Sales. Store the data in the relatinal models.

* OLAP: Online analytical process. Take the data and put it in a warehouse and then all kind of analytical process on that data to figure it out what is valuable about that data to make decistions about new products, new interaction with the customers.

# Lesson 19. Exercise: OLTP vs OLAP

https://academy.zerotomastery.io/courses/1073491/lectures/23171557
