## Chapter 08. Database design

# Lesson 1. System Design And SDLC

https://academy.zerotomastery.io/courses/1073491/lectures/23621969

- Check image SLDC. Software development life cycle

1. Phase: System planning and selection.
2. Phase: System analysis.
3. Phase: System design.
4. Phase: System implementation and operation.

- The goal of SLDC is to create roboust systems that we can add up things, be able to change it!

# Lesson 2. SDLC Phases

https://academy.zerotomastery.io/courses/1073491/lectures/23621968

1. Phase: Requirement analysis. Get info that need to be done (scope).
2. Phase: System analysis. Taking the requirements and analysing is the can be done in time and on budget.
3. Phase: Designing the system architecture for all related components: dtabases, apps, etc.
4. Phase: System implementation. Building the sodtware.

- There are more phases that can be added like:
- Testing
- Maintenance

# Lesson 3. System Design Deep Dive

https://academy.zerotomastery.io/courses/1073491/lectures/23621989

- Top-Down: Start from scratch. All requirments are gasthered up front

- Bottom-up: Three is an existing system or specific data in place

- At the end we use a bit of both approach

# Lesson 4. DRIVEME Academy

https://academy.zerotomastery.io/courses/1073491/lectures/23621980

**DRIVEME Academy example:**
<Core inventory:>

1. There is a core inventory for student to rent.
2. There are employees at every branch.
3. There is a maintenance for the vehicles.
4. There is an optinal exam at the end of your lesson.
5. You can only take the exam twice, fail twice and you must take more lessons

# Lesson 5. Top Down Design

https://academy.zerotomastery.io/courses/1073491/lectures/23621978

Goal: Create a database model based on requirements

One of the methods of <Top-Down desing> is <ER Modelling>

# Lesson 6. ER Model

https://academy.zerotomastery.io/courses/1073491/lectures/23621979

ER Model stands for Entity Relationship Model or diagram.

The emptities are the tables in the database and the relationship is the type of connection we stablish among them!

# Lesson 7. Step 1: Determining Entities

https://academy.zerotomastery.io/courses/1073491/lectures/23621981

- Determine which entities are in the system

What is an emtity (table):

- A person, a place or a thing.
- Has a singular name.
- Has a identifier
- Should contain more than one instance of data.

# Lesson 10. Tooling For Diagramming

https://academy.zerotomastery.io/courses/1073491/lectures/23621987

There are many websites to create Diagrams. For this course we use Lucidcharts
https://lucid.app/documents#/documents?folder_id=recent

# Lesson 11. DRIVEME Academy Entities

https://academy.zerotomastery.io/courses/1073491/lectures/23624695

# Lesson 12. Step 2: Attributes

https://academy.zerotomastery.io/courses/1073491/lectures/23621972

Give the entities the information we store. Attributes are colums in a table

- Most be a property of the emtity
- Must be atomic (not multiple values).
- Single/Multivalue
- Keys

# Lesson 13. Relational Model Extended

https://academy.zerotomastery.io/courses/1073491/lectures/23621988

# Lesson 14. Relational Schema And Instance

https://academy.zerotomastery.io/courses/1073491/lectures/23171552

- Check <Relational instance> Diagram

# Lesson 15. Super Key and Candidate Key

https://academy.zerotomastery.io/courses/1073491/lectures/23171555

# Lesson 16. Primary Key and Foreign Key

https://academy.zerotomastery.io/courses/1073491/lectures/23171560

- Check <Primary Key> diagram.
- Orange color indicates primary key
- Purple color indicates foreign key

# Lesson 17. Compound Composite And Surrogate Key

https://academy.zerotomastery.io/courses/1073491/lectures/23171563

- Compound Key means that the primary key is a column with unique data like email, for instance. It could be also a combination of diffrent columns. This is way is not very common.

- Surrogate Key is a Primary Key thatis not connected to the rest of the data. This is the standard.

# Lesson 18. DRIVEME Attributes

https://academy.zerotomastery.io/courses/1073491/lectures/23621982

Create a document with the attributes before adding to the Diagram in Lucid Charts

# Lesson 19. Step 3: Relationships

https://academy.zerotomastery.io/courses/1073491/lectures/23621971

- Check <crowsfeet> diagram. Crowsfeet depetis the time of releationshio we have

Firt line: Relationship
Second line: Constraint

# Lesson 20. DRIVEME Relationships

https://academy.zerotomastery.io/courses/1073491/lectures/23621983

# Lesson 21. Step 4: Solving Many To Many

https://academy.zerotomastery.io/courses/1073491/lectures/23621970

- In the relational model it isn't possible to store a many to many relationship. "Technically" you can do it but you really don't want to

- Check <many to many> diagram

<INTERMEDIATE ENTITY> is used to solve the problem of many to many relationship. Check the diagram! In the DRIVEME example, the intermediate entity is <LESSON>

# Lesson 22. Step 5: Subject Areas

https://academy.zerotomastery.io/courses/1073491/lectures/23621975

- Divide entities into logical groups that are related (think schemas)

# Lesson 23. DRIVEME Subject Areas

https://academy.zerotomastery.io/courses/1073491/lectures/23621974

# Lesson 24. Exercise: Painting Reservations

https://academy.zerotomastery.io/courses/1073491/lectures/23624694

# Lesson 25. Bottom Up Design

https://academy.zerotomastery.io/courses/1073491/lectures/23621976

# Lesson 26. Anomalies

https://academy.zerotomastery.io/courses/1073491/lectures/23621985

# Lesson 27. Normalization

https://academy.zerotomastery.io/courses/1073491/lectures/23621984

- Using normalization is key to avoid anomalies!

**Normalization:**

- Functional dependencies
- normal forms

# Lesson 28. Functional Dependencies

https://academy.zerotomastery.io/courses/1073491/lectures/23621986

- A functional dependency shows a relationship beteween attributes

- Check <Functional dependency> diagram

DETERMINANT ------> DEPENDANT
student-id ------> birth_date

# Lesson 29. Functional Dependencies 2

https://academy.zerotomastery.io/courses/1073491/lectures/23621973

- check <funtional dependency_example1> image

# Lesson 30. The Normal Forms

https://academy.zerotomastery.io/courses/1073491/lectures/23621990

- Check <Normalization> diagram

ERD stands for Entity Relational Diagram

# Lesson 31. Going from 0NF to 1NF

https://academy.zerotomastery.io/courses/1073491/lectures/23633544

**Data is in 0 normal form when it is unnormalized:**

- Repeating groups or fields
- Positional dependence of dat
- Non-atomic data

# Lesson 32. Going from 1NF to 2NF

https://academy.zerotomastery.io/courses/1073491/lectures/23633539

1. It is in 1NF (normal form)
2. All non-key attributes are fully functional dependent on the primary key

# Lesson 33. Going from 2NF to 3NF

https://academy.zerotomastery.io/courses/1073491/lectures/23633542

1. It is in 2 NF
2. No transitive dependencies

# Lesson 34. Boyce-Codd Normal Form

https://academy.zerotomastery.io/courses/1073491/lectures/25322255

1. It is in 3 NF
2. For any dependency a ---> B, A should be a super key

# Lesson 35. Why 4NF And 5NF Are Not Useful

https://academy.zerotomastery.io/courses/1073491/lectures/23633540

- This are not general used!
