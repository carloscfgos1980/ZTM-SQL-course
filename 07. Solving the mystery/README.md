## 07. Solving the mystery

# Lesson 1. Clue #1 and #2

https://academy.zerotomastery.io/courses/1073491/lectures/23503499

# Lesson 2. Getting ready to solve the mystery!

https://academy.zerotomastery.io/courses/1073491/lectures/23659734

1. Create <Movr> database and restore the data
   psql -U postgres postgres
   CREATE DATABASE Movr;
   \q
   psql -U postgres movr
   \i ~/Documents/schema.sql
   \i ~/Documents/data.sql
   \q

2. Create <movr_employees> database and restore the data
   psql -U postgres postgres
   CREATE DATABASE Movr_Employees;
   \q
   psql -U postgres movr_employees
   \i ~/Documents/movr_employees.sql
   \q

# Lesson 3. Clue #3

https://academy.zerotomastery.io/courses/1073491/lectures/23482540

**problem:**
Keiko employees and their family travel for free with the Movr platform and since Keiko is located in the heart of Downtown New York, he's thinking they may have used the platform to get around.

With what we know now, we should be able to deduce some information from the Movr database. Let's try to figure out what vehicles were at the location of Keiko Corp, and let's not forget our very first clue!

Date of incident: 2020-06-23
Keiko Corp Longitude: -74.997 to -74.9968
Keiko Corp Latitude: 40.5 to 40.6

1. With this information, we should be able to figure out which Movr rides happened that day around the office.

Try to sift through the database and figure out what table we need to query and what our query would be.

2. Once you figure out what rides occurred around the office that day, Bruno asks you to find the vehicle and owner info linked to those rides. Make sure you don't have duplicates! (see image below for expected columns)

**Answer:**

1. Create a vew that will select the suspected rides attending to the given criteria:

CREATE VIEW suspected_rides as
SELECT \*
from vehicle_location_histories as vlh
where
vlh.city = 'new york'
and
(
vlh.long BETWEEN 40.5 and 40.6
)
and (
vlh.lat BETWEEN -74.997 and -74.9968
)
and (
vlh."timestamp"::DATE = '2020-06-23'::DATE
)
ORDER by long;

2. Join rides, vehicles and users table to the created viw (suspected_rides) in order to visualize the name of the riders, address and status

SELECT DISTINCT r.vehicle_id, "u"."name" as "owner name", u.address, v.status, v.current_location
from suspected_rides as sr
join rides as r on r.id = sr.ride_id
join vehicles as v on v.id = r.vehicle_id
join users as u on u.id = v.owner_id

N: This is a bit complicated coz I can not use <USING> to join the tables since the join clomuns do not have the same name.

N: All this query was to find oit who are the drivers!

# Lesson 4. Clue #4

https://academy.zerotomastery.io/courses/1073491/lectures/23482531

# Lesson 5. Exercise: Clue #4

https://academy.zerotomastery.io/courses/1073491/lectures/23659852

DARN! All the work and the interrogation of the drivers has come up flat! Interestingly enough, we should have been looking at the riders all along. It was staring us right in the face.

So with our current setup, we go ahead and filter out all of the unique riders that were on those suspected rides on that horrible day of the theft.

Make sure to rename the column to "rider name"

# Lesson 6. Solution: Clue #4

https://academy.zerotomastery.io/courses/1073491/lectures/23599819

Answer:
SELECT DISTINCT r.vehicle_id, "u"."name" as "rider name", u.address
from suspected_rides as sr
join rides as r on r.id = sr.ride_id
join users as u on u.id = r.rider_id

N: Get all the riders

# Lesson 7. Clue #5 and #6

https://academy.zerotomastery.io/courses/1073491/lectures/23482543

run this to run queries across databases:
psql -U postgres movr
create extension dblink;
\q
psql -U postgres movr_employees
create extension dblink;
\q

# Lesson 8. Solution: Clue #5 and #6

https://academy.zerotomastery.io/courses/1073491/lectures/23599820

1. Step
   create VIEW suspected_riders_name as
   SELECT DISTINCT
   split_part( u.name, ' ', 1) as "first_name",
   split_part( u.name, ' ', 2) as "last_name"
   from suspected_rides as vhl
   join rides as r on r.id = vhl.ride_id
   join users as u on u.id = r.rider_id

N: Create a view with the name and last name of the riders. I need to use <split_part> function

2. Step
   SELECT DISTINCT
   CONCAT(t1.first_name, ' ', t1.last_name) as "employee",
   CONCAT(u.first_name, ' ', u.last_name) AS "rider"
   from dblink ('host=localhost user=postgres password=postgres dbname=movr_employees',
   'select first_name, last_name from employees;')
   as t1(first_name NAME, last_name NAME)

JOIN suspected_riders_name as u on t1.last_name = u.last_name
ORDer by "rider"

N: Cross information between databases

# Lesson 9. Solving The Mystery

https://academy.zerotomastery.io/courses/1073491/lectures/23482536
