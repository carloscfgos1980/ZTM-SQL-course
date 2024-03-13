## Chapter 06. Database management

# Lesson 01. Time To Create Some Stuff!

https://academy.zerotomastery.io/courses/1073491/lectures/23648638

**What we'll be learning in this sectio:**

- Different types of data
- How to create database
- Hot to create tables
- How to Insert/Update/... Data

# Lesson 2. Types Of Databases In A RDBMS

https://academy.zerotomastery.io/courses/1073491/lectures/23459395

# Lesson 3. Default PostgreSQL Database

https://academy.zerotomastery.io/courses/1073491/lectures/23459394

# Lesson 4. Template Databases

https://academy.zerotomastery.io/courses/1073491/lectures/23459392

- template0 is like a safety. Never change it!
- Template01 is the one we use to create database. The changes we do to this template won't affect the already created database but it will affect all the future databases

# Lesson 5. Creating A Database

https://academy.zerotomastery.io/courses/1073491/lectures/23459397

I had a huge bug here! I missed this in the installation and configuration:
sudo mkdir -p /etc/paths.d &&
echo /Applications/Postgres.app/Contents/Versions/latest/bin | sudo tee /etc/paths.d/postgresapp
Now it works!

**Create database**
psql -U postgres postgres
CREATE DATABASE ztm;

**Delete database**
DROP DATABASE ztm;

# Lesson 6. Database Organization

https://academy.zerotomastery.io/courses/1073491/lectures/23486770

- Postgress offers the concept of <schemas>, Think it like a box in which you can organize tables, views, indexes, etc

- By default each database gets a "public" schema. Eg:

SELECT \* FROM employees

-- is the same as

SELECT \* FROM public.employees

# Lesson 7. Roles In Postgres

https://academy.zerotomastery.io/courses/1073491/lectures/23486765

<A role> can be an individual user or a group.

# Lesson 8. Role Attributes And Creation

https://academy.zerotomastery.io/courses/1073491/lectures/23486764

The privileges of a role are determineed in part by its attributes

**command to check the roles**
psql -U postgres postgres
\du

# Lesson 9. Creating Users And Configuring Login

https://academy.zerotomastery.io/courses/1073491/lectures/23486768

psql -U postgres postgres
CREATE role test_role_with_login WITH LOGIN ENCRYPTED PASSWORD 'password';

- You can alter the role, like this:
  ALTER ROLE test_role_with_login WITH LOGIN ENCRYPTED PASSWORD 'password2';

The follow commands show two files need to change the default local login for the database:
show hba_file;
/Users/carlosinfante/Library/Application Support/Postgres/var-16/pg_hba.conf

show config_file;
/Users/carlosinfante/Library/Application Support/Postgres/var-16/postgresql.conf

In this video explain how to do it. This siles controls the configuration of postgres. I didn't change anything!

# Lesson 10. Privileges

https://academy.zerotomastery.io/courses/1073491/lectures/23486763

- By default objects are only available to the one who creates them.
- Privileges need to be granted for new roles and users to have access to certain data

# Lesson 11. Granting Privileges and Role Management

https://academy.zerotomastery.io/courses/1073491/lectures/23542649

Create a user with no privileges interactive. CLI:
createuser --interactive
Enter name of role to add: privilegetest
Shall the new role be a superuser? (y/n) n
Shall the new role be allowed to create databases? (y/n) n
Shall the new role be allowed to create more new roles? (y/n) n

- Open a different terminal and login into Employees database with the new user that has not privileges:

psql -U privilegetest Employees

- Try to access a table and I get permission denied:

Employees=> SELECT \* FROM titles;
ERROR: permission denied for table titles

- Grant priviliges to the the user to access "titles" table. This has to be done by the superuser:
  psql -U postgres Employees
  \conninfo
  GRANT SELECT ON titles TO privilegetest;

- Revoke permission:
  REVOKE SELECT ON titles FROM privilegetest;

- Grant all permissions:
  GRANT ALL ON ALL TABLES IN SCHEMA public TO privilegetest;

- Revoke all permissions:
  REVOKE ALL PRIVILEGES ON ALL TABLES IN SCHEMA public FROM privilegetest;

- Create a ready only role:
  CREATE ROLE employess_read;

- Grant read only permission:
  GRANT SELECT ON ALL TABLES IN SCHEMA public TO employess_read;

- We can gran read only role to another role, likes this:
  GRANT employess_read TO privilegetest;

# Lesson 12. Best Practices For Role Management

https://academy.zerotomastery.io/courses/1073491/lectures/23486767

# Lesson 13. Data Types & Boolean Type

https://academy.zerotomastery.io/courses/1073491/lectures/23486769

# Lesson 14. Storing Text

https://academy.zerotomastery.io/courses/1073491/lectures/23542653

CHAR(N)

- Fill the empty spaces with pad
  CHAR(10)

- It will only fill the spaces with the text
  VARCHAR(10)

- Infinite amount of text
  TEXT

# Lesson 15. Storing Numbers

https://academy.zerotomastery.io/courses/1073491/lectures/23542642

- SMALLINT. There can be from negative to positive numbers:
  -500 TO 1000.

- INT. Storage number in milliions

-2,500,999 TO -2,500,999

- BIGINT. Storage very large numbers
  -4,333,444,666 TO 4,333,444,666

- FLOAT4/FLOAT8. Floating numbers. FLOAT4 you can go 6 digits after the point and FLOAT8 till 15 digits after the point.

- DECIMAL/NUMERIC. Up to 131072 digits before the decimal point and up to 16383 after the decimal point.

# Lesson 16. Storing Arrays

https://academy.zerotomastery.io/courses/1073491/lectures/23542644

# Lesson 17. Data Models And Naming Conventions

https://academy.zerotomastery.io/courses/1073491/lectures/23542645

- Check the image of Data models

# Lesson 18. CREATE TABLE

https://academy.zerotomastery.io/courses/1073491/lectures/23542647

- Create a table:
  CREATE TABLE student(
  student_id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  first_name VARCHAR(255) NOT NULL,
  last_name VARCHAR(255) NOT NULL,
  email VARCHAR(255) NOT NULL,
  date_of_birth DATE NOT NULL
  );

- Run this command so uuid_generate_v4() works:
  create extension if not exists "uuid-ossp";

- Check tables in database:
  \dt

- Check data model of a table:
  \d student

# Lesson 19. Column Constraints

https://academy.zerotomastery.io/courses/1073491/lectures/23640935

# Lesson 20. Table Constraints

https://academy.zerotomastery.io/courses/1073491/lectures/23640933

- You can write the contrains at column level or table level. It works either way

# Lesson 21. Regexes!

https://academy.zerotomastery.io/courses/1073491/lectures/23659587

Regexes stands for regular exprexions. It is used to check (validate) the value before storage in database.

# Lesson 22. UUID Explained

https://academy.zerotomastery.io/courses/1073491/lectures/23640932

UUID stands for Universal Unique Identifier

# Lesson 23. Custom Data Types And Domains

https://academy.zerotomastery.io/courses/1073491/lectures/23640934

- We can create our custom data, like we do with "rating" column:

  CREATE DOMAIN Rating SMALLINT
  CHECK (VALUE > 0 AND VALUE <= 5);

CREATE TYPE Feeback as (
student_id UUID,
rating Rating,
feedback TEXT
);

# Lesson 24. Creating The Tables For ZTM

https://academy.zerotomastery.io/courses/1073491/lectures/23542643

- Create <student> table:
  CREATE TABLE student(
  student_id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  first_name VARCHAR(255) NOT NULL,
  last_name VARCHAR(255) NOT NULL,
  email VARCHAR(255) NOT NULL,
  date_of_birth DATE NOT NULL
  );

- Create <subject> table:
  CREATE Table subject (
  subject_id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  subjetc TEXT NOT NULL,
  description TEXT NOT NULL
  );

- Create <teacher> table:
  CREATE TABLE teacher(
  teacher_id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  first_name VARCHAR(255) NOT NULL,
  last_name VARCHAR(255) NOT NULL,
  email VARCHAR(255) NOT NULL,
  date_of_birth DATE NOT NULL
  );

- Add a colum to a table:
  ALTER TABLE student
  ADD COLUMN email VARCHAR(255) NOT NULL;

- Create <course> table:
  CREATE TABLE course(
  course_id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  "name" TEXT NOT NULL,
  description TEXT,
  subject_id UUID REFERENCES subject(subject_id),
  teacher_id UUID REFERENCES teacher(teacher_id),
  feedback feedback[]
  );

N: name is in double quote cos is a reserved key,
subject_id UUID REFERENCES subject(subject_id) => This is a way we create a foreign key
feeback feeback[] => This is the way we create array values.

- Create <enrollment> table:
  CREATE TABLE enrollment (
  course_id UUID REFERENCES course(course_id),
  student_id UUID REFERENCES student(student_id),
  enrollment_date DATE NOT NULL,
  CONSTRAINT pk_enrollment PRIMARY KEY (course_id, student_id)
  );

N: CONSTRAINT pk_enrollment PRIMARY KEY (course_id, student_id) => Make couser_id and student_id the primary keys of this table.

# Lesson 25. Adding Students And Teachers

https://academy.zerotomastery.io/courses/1073491/lectures/23542646

- Inserting data into student table:
  INSERT INTO student (
  first_name,
  last_name,
  email,
  date_of_birth
  ) VALUES (
  'Carlos',
  'Infante',
  'kuva5008@gmail.com',
  '1980-01-31'::DATE
  );

- Insert data into teacher table:
  INSERT INTO teacher (
  first_name,
  last_name,
  email,
  date_of_birth
  ) VALUES (
  'David',
  'Soler',
  'davidgmail.com',
  '1965-10-10'::DATE
  );

# Lesson 26. Creating A Course

https://academy.zerotomastery.io/courses/1073491/lectures/23542648

- Delete a row from a table:
  DELETE FROM subject WHERE subject = 'SQL zero to mastery';

- Insert data into <course> table without (forgetting) subject_id:
  INSERT INTO subject (
  subjetc,
  description
  ) VALUES (
  'SQL',
  'A database management language'
  );

- Adding a subject_id:
  UPDATE course
  set subject_id = '0e7730b5-e890-47a0-bda5-3468fb3c3986'
  where subject_id is null;

- Add restriction to a column:
  ALTER TABLE course ALTER COLUMN subject_id set not null;

- Insert data into <course> table:
  INSERT INTO course (
  "name",
  description,
  subject_id

) VALUES (
'SQL Zero to Mastery',
'The 3 1 resource for SQL mastery',
'207fe34c-59da-48e8-9aa3-2d5fd200ed3b'
);

N: It is very important to think ahead in the data model and implement the proper constrains so we don't need to change it later.

- proper sql for course:
  INSERT INTO course (
  "name",
  description,
  subject_id,
  teacher_id

) VALUES (
'SQL Zero to Mastery',
'The 3 1 resource for SQL mastery',
'0e7730b5-e890-47a0-bda5-3468fb3c3986',
'c46a2f4b-c903-44d5-9bec-e46fd6265b80'
);

# Lesson 27. Adding Feedback To A Course

https://academy.zerotomastery.io/courses/1073491/lectures/23612114

- Insert values into <enrollment> table:
  INSERT INTO enrollment (
  student_id,
  course_id,
  enrollment_date
  ) VALUES (
  '15518797-73e2-4b60-8295-896e8e66ed28',
  '3eb93164-e6fe-428c-93f7-37a222d218ba',
  now()::DATE
  );

- adding a feedback to the course
  update course
  set feedback = array_append(
  feedback,
  ROW (
  student Id
  '15518797-73e2-4b60-8295-896e8e66ed28',
  5,
  'Great course!'
  )::feeback
  )
  WHERE course_id = '3eb93164-e6fe-428c-93f7-37a222d218ba';

N: This didn't work. I looked online and I found this way to do it instead

UPDATE course
SET feedback = '{
15518797-73e2-4b60-8295-896e8e66ed28,
5,
Great course!
}'
WHERE course_id = '137009bc-81cc-4182-896c-b3d2a1ed4eb1';

# Lesson 28. A Tale Of 2 Feedbacks

https://academy.zerotomastery.io/courses/1073491/lectures/23612112

- Create table for feedback
  create TABLE feedback (
  student_id UUID not null REFERENCES student(student_id),
  course_id UUID not null REFERENCES course (course_id),
  feedback TEXT,
  rating rating,
  CONSTRAINT pk_feedback PRIMARY KEY (student_id, course_id)
  );

N: At the end create an array of values for feedback inside table <course> is not the best practice coz we can't force to have a real student and course id. That is why is better to create a different table for feedbacks

- SQL to select name of the course, description, rating and feedback:
  SELECT c.name, c.description, fe.feedback, fe.rating
  From course AS c
  JOIN feedback AS fe USING(course_id);

- SQL to select name of the course, description, rating and feedback. This is more complex that the previous coz I join 3 tables in order to get the name and last name of the student who provide the feedback.

  SELECT c.name as "course", c.description, fe.feedback, fe.rating, CONCAT (s.first_name, ' ', s.last_name) as "student"
  From course AS c
  JOIN feedback AS fe USING(course_id)
  join student as s USING(student_id);

# Lesson 29. Backups And Why They Are Important

https://academy.zerotomastery.io/courses/1073491/lectures/23612117

N: Check <Types backups>

# Lesson 30. Backing Up In Postgres

https://academy.zerotomastery.io/courses/1073491/lectures/23612113

N: Right Click on the database we want to save. Then select <dump> and follow the instructions. This will create a .sql file in the selected location with all the info

# Lesson 31. Restoring A Database

https://academy.zerotomastery.io/courses/1073491/lectures/23612115

N: Try to restore info by Valentina (Graphical User Interface) could create an error. It is recommend it to run in CLI:
psql -d postgress
\conninfo

# Lesson 32. Transactions

https://academy.zerotomastery.io/courses/1073491/lectures/23612111

- Check image <Transaction life cycle>

psql -U postgres Employees
BEGIN;
DELETE FROM employees WHERE EMP_NO BETWEEN 1000 AND 1005;
END;

N: Resources get lock while you are doing a transaction (Update, Delete, Insert)
