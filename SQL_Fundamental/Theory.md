**Database:**  A database is collection of data that is set up for easy access, management and updating.

**DBMS:** software systems used to store, retrieve, and run queries on stored data.

**Relational Database:** A database consiting of data organized among various tables in rows and columns format.

**RDBMS:** is a system used to create, update and manage relational databases.

**SQL:** is a standard database language that is used to create, maintain and retrieve the relational database.

**Types of SQL:**

1. DDL : Data Defination Language - Handle database schema and used to construct and modify the structure of database objects {CREATE, ALTER, DROP, TRUNCATE}
2. DML: Data Manipulation Language - used to make changes to the database such as: CRUD {SELECT, INSERT, UPDATE, DELETE}
3. DCL: Data Control Language - Used to control access to data stored in database {GRANT, REVOKE}
4. DQL: Data Query Language - allow you to get and organise data from database {SELECT}
5. TCL: Transaction Control Language - used to manage database transaction(squence of one or more sql operations that are treated as a unit.) {COMMIT, ROLLBACK}

**Constraints:** are rules that we can apply on the type of data in a table to store data in specific manner or order.

* NOT NULL
* UNIQUE
* PRIMARY KEY
* FOREIGN KEY
* CHECK
* DEFAULT

**ACID Properties:**

* ATOMOCITY: ensure that a transaction need to completely successful or completely unsuccessful.
* CONSISTENCY: Transcation move in a database one valid state to another.
* ISOLATION: Multiple transactions independetally happen without interfare.
* DURABILITY: After one transaction committed, it can't be modified even after system failure.

**Keys and Why we need it:** basice requirement of relational database model, used to identify the tuples(row) uniquely in the table and also used for setup relations amongst various columns and tables.

**Keys of DBMS:**

* Super Key: To uniquely identify each tuple in the table, it might be single or a combination of many attributes. EX: booking(Passenger ID + Reservation Number) Bank(customer Id + account number)
* Candidate Keys(minimum super key): simple collection of characetricstics that can be used to identify a tuple, can contain null value, but must always be unique. EX: Account No, Voter Id
* Primary Key: most suitable candidate key, cannot have null values, it must unique and non-null. EX: email_id, Name, DOB.
* Alternate Key: different from primary key, if necessary primary key can be selected from any of the alternate keys, sometimes to improve search speed, alternate keys are used for indexing.
* Foreign Key: supports for creation of associations between tables, EX: course_id
* Composite Key: unique method two identifying rows in a table by combining two or more characteristics to create composite key. EX: (AP 19 CB 2005) AP -> state_id, 19->sectore_id
* Surrogate Key: allow under certain conditions like main PK is very large, challenging PK, lack of key, when not natural choice. EX: student Table {student_id}

**Dependency:** it is a constraint defines relationship between attributes, also define relationship knowing that one attribute is enough to tell you the value of another attribute in the same table.

1. **Functional Dependency:** fundamental concept describe the relationship between attributes in a table, shows how the values in one or more attributes determine the value in another.
2. **Fully Functional Dependency:** type of dependency that exists between two sets of attributes in a database table.

**Types of Functional Dependency:**

1. Partial Dependency: exists when a non-primary column depends upon a single column that is a part of a composite primary key.
2. Transitive Functional Dependecy: It occurs when one attribute's value determines another's value through an intermediary(a third) attribute.

**Normalization:** is the process of minimizing redundancy and correcting table structure in a relational table.

**Why we need?**

* eliminating redundant data, so we can handle data integrity, because of repeated data data inconsitent chances increases.
* breaking down large tables into smaller tables with relationship, so it makes database structure more scalable and adaptable.
* ensuring data stored logically.

**Normal Forms:**

1. **1NF:** A relation is in 1NF if all its attributes have an atomic value.
2. **2NF:** A relation is in 2NF if it is in 1NF and all non-key attributes are fully functional dependent on the candidate key.
3. **3NF:** A relation is in 3NF if it is in 2NF and there is no transitive dependency.
4. **BCNF:** A relation is in BCNF if it is in 3NF and for every Functional Dependency, LHS is the super key.

**Denormalization:** database optimization technique in which we add redundant data to one or more tables. (OLAP).

**Relationship in SQL:**

1. One-to-one Relationship
2. One-to-many Relationship
3. Many-to-many Relationship
4. Many-to-one Relationship
5. Self-referencing Relationship

**Trigger:** is a stored procedure that can be executed in response to one of three conditions 1. An UPDATE, 2.An INSERT, 3. A DELETE. automatically invokes whenever a special event in the database occurs.

**Types of Triggers: 1.** DDL Triggers, 2. DML Triggers, 3. TCL Triggers

**Advantages:**

1. maintain integrity constrainsts when primary key and foreign key constrain are not defined.
2. SQL code short
3. give alternative way to run scheduled tasks.

**Disadvantages:**

1. Only provide extended validators
2. increase overhead
3. difficult to troubleshoot because they execute automatically

**Store Procedures:** group of sql statements stored together in a database, based on procedure and parameters you pass, it can perform one or multiiple DML operations, allow to pass same statement multiple times, thereby enabling reusability.

**Advantages:**

* Reusable: multiple user and applications can easly reuse store procedure by calling it.
* Easy to Modify: with the help of alter command we can change the store procedure statement.
* Security: store procedure enhance the security by restricting the user from direct access the table.
* Low Network Traffic: server only passes the procedue name not the whole statement reducing network traffic

**Drawbacks:**

* Increased Overhead: when we do complex operations stored procedure consume more resources than a simple sql statement.
* Limited Portability: often specific for a particular DBMS, not easy to portable to other business.
* Debugging Challeneges: if there multiple layers of code involved debugging the store procedure is challenging.

**VIEW:** kind of virtual table not stored in database and give query result through real tables.

**Advantages:**

1. not store data in a physical location
2. used to hide some of the column from table
3. provide access restriction, since data insertion, delete, update not possible.

**Disadvantages:**

1. when physical table drop associated view irrelevant.
2. when views are created for large tables it occupy more memory.

**Index:** is like organized catalog for your database. It's a data structure that help's you quickly locate specific rows in a table.Just like the index at the back of a book.

**Benefits:**

* Improved search performance
* Efficient data retrieval
* Enhanced query performance
* sorting and ordering

**Types:**

1. Clustered Index: Index which have primary key define
2. Non-Clustered Index: index which have non-primary key

**LOGICAL ORDER OF OPERATIONS IN SQL:**

1. FROM, JOIN
2. WHERE
3. GROUP BY
4. aggregate functions
5. HAVING
6. window functions
7. SELECT
8. DISTINCT
9. UNION/INTERSECT/EXCEPT
10. ORDER BY
11. OFFSET
12.  LIMIT/FETCH/TOP
