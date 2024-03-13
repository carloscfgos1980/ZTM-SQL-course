## SQL Course

# Chapter 1. History and Story of Data

**Concepts:**
<Database Management System>: It is a software that is used to manage the database.
<Relatational Database Management system>: It is a subset of Database Management System
<Structure Query Language>: It is a way for us to interact with a Database Management System

**5 are the most populars:**

- Relational (ProgressSQL)
- Document (MongoDB)
- Key Value
- Graph (social network. Very rare)
- Wide Columnar (Apache, Cassandra)

**What is a database**
Database is a system, hardware and software that allows the user to store, organize and use data

# Chapter 2. Database SQL Fundamentals

- Playground to understand SQL
- Explanation of tablesm rows, columns foreign key and primary key

**OLTP vs OLAP**

- OLTP: Online Transaccion Processes. Day to day transaccion ex: Sales. Store the data in the relatinal models.

* OLAP: Online analytical process. Take the data and put it in a warehouse and then all kind of analytical process on that data to figure it out what is valuable about that data to make decistions about new products, new interaction with the customers

# Chapter 3. Environment setups

- Installing Postgres and Valentina. Valentina was a pain in the ass the installation due the serial, nevertheless it's done!

- loading data into database

# Chapter 4. SQL Deep Dive

- Changing Column Names in a SELECT Query
- Concat Function
- Aggregate Functions
- Commenting Your Queries
- Filtering Data
- Comparison Operators
- Checking For NULL Values
- IS Keyword
- NULL Coalescing
- BETWEEN + AND
- IN Keyword
- LIKE
- Dates And Timezones
- Setting Up Timezones (This took me busy a whole weekend!)
- Date Functions
- Date Difference And Casting
- Age Calculation
- Extracting Information
- Intervals
- Exercise: Date and Timestamp
- DISTINCT
- Sorting Data
- Multi Table SELECT
- Inner Join
- Self Join
- Outer Join
- Less Common Joins
- USING Keyword

# Chapter 5. Advanced SQL

- GROUP BY
- HAVING Keyword
- Ordering Grouped Data
- Grouping Sets
- Rollup
- Window functions
- Window PARTITION BY
- Using Framing In Window Function
- Solving For Current Salary (window function)
- FIRST_VALUE
- LAST_VALUE
- SUM
- ROW_NUMBER
- Conditional Statements
- NULLIF
- Views
- Indexes
- Subqueries
- Getting The Latest Salaries
- Subquery Operators

# Chapter 6. Database management

- Conceptualization of databases
- Create a database
- Roles and permissions
- Type of data
- Storing data
- Data Models And Naming Conventions
- CREATE TABLE
- Column Constraints
- Table Constraints
- UUID Explained
- Custom Data Types And Domains
- Backing Up In Postgres
- Restoring A Database
- Transactions

# Chapter 7. Solving the mystery

- Restore database
- Filter information and create a view (suspected_rides)
- Get the onwner name and address of the suspected_rides by join 3 tables (rides, vehicle, users). I need to use the ON syntax instead of USING coz this motherfuckers had a different name for the primary and foreign key.
- filter the name of the riders instead of the owners.
- create dblink extension so I could cross data between two different databases
- from <movr> database create a view with a list of first_name and last_name. I need to use a function to split name (a column that contains both name and last name)
- SQl to cross data between <movr> and <movr_employees>, matching suspected riders last name with employees last name. This provide a list of eleven people. That is the end of the exercise
- No entendi mucho esta mierda pero al final se como usar las putas herramientas. Esto es pa nerds!

# Chapter 8. Database design

- System Design And SDLC
- SDLC Phases
- Top Down Design
- DRIVEME academy as example of Top Down Design
- Button up design
