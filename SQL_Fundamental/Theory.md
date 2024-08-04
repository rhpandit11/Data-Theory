**Database:**  A database is collection of data that is set up for easy access, management and updating.

**DBMS:** software systems used to store, retrieve, and run queries on stored data.

**Relational Database:** A database consiting of data organized among various tables in rows and columns format.

**RDBMS:** is a system used to create, update and manage relational databases.

**SQL:** is a standard database language that is used to create, maintain and retrieve the relational database.

---

**Types of SQL:**

1. DDL : Data Defination Language - Handle database schema and used to construct and modify the structure of database objects {CREATE, ALTER, DROP, TRUNCATE}
2. DML: Data Manipulation Language - used to make changes to the database such as: CRUD {SELECT, INSERT, UPDATE, DELETE}
3. DCL: Data Control Language - Used to control access to data stored in database {GRANT, REVOKE}
4. DQL: Data Query Language - allow you to get and organise data from database {SELECT}
5. TCL: Transaction Control Language - used to manage database transaction(squence of one or more sql operations that are treated as a unit.) {COMMIT, ROLLBACK}

Difference Between DROP and TRUNCATE:

| DROP                                                                                                               | TRUNCATE                                                                                    |
| ------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------- |
| In the drop table data and its defination is deleted<br />with their full structure                                | it preserves the structure of the table for further<br />use exist but deletes all the data |
| Drop is used to eliminate existing complications and fewer complications<br />in the whole database form the table | used to eliminate the tuple from the table                                                  |
| Integrity constraints get removed in the DROP command                                                              | Integrity commands exists in the truncate command                                           |
| since the structure does not exist, the view of the table does not exist<br />in the drop command                  | since the structure exists the view of the table exists in the<br />truncate command        |
| free the memory                                                                                                    | does not free the table space from the memory                                               |
| it slow as compare to truncate                                                                                     | it is fast                                                                                  |

---

**Constraints:** are rules that we can apply on the type of data in a table to store data in specific manner or order.

* NOT NULL - Restricts NULL value from being inserted into a column.
* UNIQUE  - Ensures unique values to be inserted into the field.
* PRIMARY KEY - Uniquely identifies each record in a table.
* FOREIGN KEY - Ensures referential integrity for a record in another table.
* CHECK - Verifies that all values in a field satisfy a condition.
* DEFAULT - Automatically assigns a default value if no value has been specified for the field.
* **INDEX** - Indexes a field providing faster retrieval of records.

---

**ACID Properties:**

* ATOMOCITY: ensure that a transaction need to completely successful or completely unsuccessful.
* CONSISTENCY: Transcation move in a database one valid state to another.
* ISOLATION: Multiple transactions independetally happen without interfare.
* DURABILITY: After one transaction committed, it can't be modified even after system failure.

Example:

* **Atomicity:** Consider a fund transfer between two bank accounts. If the debiting of one account succeeds but the crediting of the other account fails due to a technical glitch, the entire transaction is rolled back to maintain the atomicity of the operation.
* **Consistency:** In an e-commerce platform, when a user places an order, the inventory of the purchased items is decremented to reflect the items’ availability accurately.
* **Isolation:** In a reservation system for flight tickets, two users attempting to book the same seat simultaneously are isolated from each other. Only one user's reservation is accepted, preventing double bookings.
* **Durability:** After a user confirms an edit to a document in a word processing application, the changes are permanently stored in the document file, even if the application crashes before the document is closed.

---

**Keys and Why we need it:** basice requirement of relational database model, used to identify the tuples(row) uniquely in the table and also used for setup relations amongst various columns and tables.

**Keys of DBMS:**

* Super Key: To uniquely identify each tuple in the table, it might be single or a combination of many attributes. EX: booking(Passenger ID + Reservation Number) Bank(customer Id + account number)
* Candidate Keys(minimum super key): simple collection of characetricstics that can be used to identify a tuple, can contain null value, but must always be unique. EX: Account No, Voter Id
* Primary Key: most suitable candidate key, cannot have null values, it must unique and non-null. EX: email_id, Name, DOB.
* Alternate Key: different from primary key, if necessary primary key can be selected from any of the alternate keys, sometimes to improve search speed, alternate keys are used for indexing.
* Foreign Key: supports for creation of associations between tables, EX: course_id
* Composite Key: unique method two identifying rows in a table by combining two or more characteristics to create composite key. EX: (AP 19 CB 2005) AP -> state_id, 19->sectore_id
* Surrogate Key: allow under certain conditions like main PK is very large, challenging PK, lack of key, when not natural choice. EX: student Table {student_id}

---

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

* First normal Form (1NF): It removes all duplicate columns from the table. Creates table for related data and identifies unique column values
* First Normal Form (2NF): Follows 1NF and creates and places data subsets in an individual table and defines relationship between tables using primary key
* Third Normal Form (3NF): Follows 2NF and removes those columns which are not related through primary key
* Fourth Normal Form (4NF): Follows 3NF and do not define multi-valued dependencies. 4NF also known as BCNF

**Denormalization:** database optimization technique in which we add redundant data to one or more tables. (OLAP).

reasons for denormalizing the data: We de-normalize data when we need better performance. Sometimes there are many joins in a query due to highly normalized data. In that case, for faster data retrieval it becomes essential to de-normalize data.

---

**Relationship in SQL:**

1. One-to-one Relationship
2. One-to-many Relationship
3. Many-to-many Relationship
4. Many-to-one Relationship
5. Self-referencing Relationship

---

**Trigger:** is a stored procedure that can be executed in response to one of three conditions 1. An UPDATE, 2.An INSERT, 3. A DELETE. automatically invokes whenever a special event in the database occurs.

**Types of Triggers: 1.** DDL Triggers, 2. DML Triggers, 3. TCL Triggers

* ***Create Trigger***
  These two keywords are used to specify that a trigger block is going to be declared.
* ***Trigger_Name***
  It specifies the name of the trigger. Trigger name has to be unique and shouldn’t repeat.
* **( *Before | After ***This specifies when the trigger will be executed. It tells us the time at which the trigger is initiated, i.e, either before the ongoing event or after.
* *Before Triggers* are used to update or validate record values before they’re saved to the database.
* *After Triggers* are used to access field values that are set by the system and to effect changes in other records. The records that activate the after trigger are read-only. We cannot use the After trigger if we want to update a record because it will lead to a read-only error.
* **[ * Insert | Update | Delete * ]**
  These are the DML operations and we can use either of them in a given trigger.
* ** *on * [ *Table_Name ***We need to mention the table name on which the trigger is being applied. Don’t forget to use **on **keyword and also make sure the selected table is present in the database.
* **[ for each row | for each column ]**

1. Row-level trigger gets executed before or after *any column value of a row *changes
2. Column Level Trigger gets executed before or after the *specified column *changes

```sql
CREATE TRIGGER calculate
before INSERT
ON student
FOR EACH ROW
SET new.marks = new.marks+100;
```

**Advantages:**

1. maintain integrity constrainsts when primary key and foreign key constrain are not defined.
2. SQL code short
3. give alternative way to run scheduled tasks.

**Disadvantages:**

1. Triggers can only provide extended  **validations** , i.e, not all kinds of validations. For simple validations, you can use the NOT NULL, UNIQUE, CHECK, and FOREIGN KEY constraints
2. increase overhead
3. difficult to troubleshoot because they execute automatically

---

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

---

**VIEW:** kind of virtual table not stored in database and give query result through real tables. ex.

CREATE VIEW *view_name* AS
SELECT  *column1* ,  *column2* , ...
FROM *table_name*
WHERE  *condition* ;

****Materialized Views:**** When the results of a view expression are stored in a database system, they are called materialized views.

| Views                                                                                                                                                                                 | Materialized Views                                                                                                                                                                             |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Query expression are stored in the databases system,<br />and not the resulting tuples of the query expression.                                                                       | Resulting tuples of the query expression are stored in the databases<br />system.                                                                                                              |
| Views needs not to be updated every time the relation<br />on which view is defined is updated, as the tuples of the views<br /> are computed every time when the view is accessed. | Materialized views are updated as the tuples are stored in the database<br />system. It can be updated in one of three ways depending on the <br />databases <br />system as mentioned above. |
| It does not have any storage cost associated with it.                                                                                                                                 | It does have a storage cost associated with it.                                                                                                                                                |
| It does not have any updation cost associated with it.                                                                                                                                | It does have updation cost associated with it.                                                                                                                                                 |
| There is an SQL standard of defining a view.                                                                                                                                          | There is no SQL standard for defining a materialized view, and the<br /> functionality is provided by some databases systems as an extension.                                                 |
| Views are useful when the view is accessed infrequently.                                                                                                                              | Materialized views are efficient when the view is accessed frequently<br />as it<br />saves the computation time by storing the results before hand.                                           |

**Advantages:**

1. not store data in a physical location
2. used to hide some of the column from table
3. provide access restriction, since data insertion, delete, update not possible.

**Disadvantages:**

1. when physical table drop associated view irrelevant.
2. when views are created for large tables it occupy more memory.

---

**Index:** is like organized catalog for your database. It's a data structure that help's you quickly locate specific rows in a table.Just like the index at the back of a book.

**Benefits:**

* Improved search performance
* Efficient data retrieval
* Enhanced query performance
* sorting and ordering

**Types:**

1. Clustered Index: Index which have primary key define.You can create only one clustered index in a table.In this index contain a pointer to block but not direct data.If  we create a table with primary key then automatically clustered index created.If you have one clustered index on multiple columns, and that type of index is called a composite index. ex:

   ```sql
   CREATE INDEX idx_LastName ON Employees (LastName);
   ```

   * The data or file, that you are moving into secondary memory should be in sequential or sorted order.
   * There should be a key value, meaning it can not have repeated values.
2. Non-Clustered Index: The non-Clustered Index is similar to the index of a book. The index of a book consists of a chapter name and page number, if you want to read any topic or chapter then you can directly go to that page by using the index of that book. No need to go through each and every page of a book. The data is stored in one place, and the index is stored in another place. Since the data and non-clustered index is stored separately, then you can have multiple non-clustered indexes in a table.

   ```sql
   Create table Student
   ( Roll_No int primary key, 
   Name varchar(50), 
   Gender varchar(30), 
   Mob_No bigint );

   insert into Student 
   values (4, 'afzal', 'male', 9876543210 );

   insert into Student 
   values (3, 'sudhir', 'male', 9675432890 );

   insert into Student 
   values (5, 'zoya', 'female', 8976453201 );

   create nonclustered index NIX_FTE_Name
   on Student (Name ASC);
   ```

Difference Between Clustered and Non-Clustered Index :

| CLUSTERED INDEX                                                                                                | NON-CLUSTERED INDEX                                                                                                                                                      |
| -------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| A clustered index is faster.                                                                                   | A non-clustered index is slower.                                                                                                                                         |
| The clustered index requires less memory for operations.                                                       | A non-Clustered index requires more memory for operations.                                                                                                               |
| In a clustered index, the clustered index is the main data.                                                    | In the Non-Clustered index, the index is the copy of data.                                                                                                               |
| A table can have only one clustered index.                                                                     | A table can have multiple non-clustered indexes.                                                                                                                         |
| The clustered index has the inherent ability to store data on the disk.                                        | A non-Clustered index does not have the inherent ability to store<br />data<br />on the disk.                                                                            |
| Clustered index store pointers to block not data.                                                              | The non-clustered index stores both the value and a pointer to the<br />actual<br /> row that holds the data                                                             |
| In Clustered index leaf nodes are actual data itself.                                                          | In Non-Clustered index leaf nodes are not the actual data itself<br />rather<br /> they only contain included columns.                                                   |
| In a Clustered index, Clustered key defines the order<br />of data within a table.                             | In a Non-Clustered index, the index key defines the order of data<br />within the index.                                                                                 |
| A Clustered index is a type of index in which table records<br /> are physically reordered to match the index. | A Non-Clustered index is a special type of index in which the logical<br />order of the index does not match the physical stored order of the <br />rows on the disk. |
| The size of The primary clustered index is large.                                                              | The size of the non-clustered index is compared relativelyThe composite<br />is smaller.                                                                                 |
| Primary Keys of the table by default are clustered indexes.                                                    | The[composite key](https://www.geeksforgeeks.org/composite-key-in-sql/) when used with unique constraints of the table act <br />as the non-clustered index.                |

Use:

****Index Clustering****

* Perfect for tables where range queries, in particular, place a high value on data retrieval efficiency.
* Ideal for tables with few updates or relatively static data because moving data around can slow down insert and update operations.

****Non-Clustered index****

* allows for the optimization of various query types without changing the data’s physical order on disk.
* Ideal for tables where data changes often since inserts and updates are typically quicker than with clustered indexes.

---

**Correlated subquery:** n Correlated Query,  Outer query executes first and for every Outer query row Inner query is executed. Hence, the Inner query uses values from the Outer query.

**Non-Correlated subquery** - In non-correlated query inner query does not dependent on the outer query. They both can run separately.

| Sr. No.     | Key                            | Correlated subquery                                                                 | Non-Correlated subquery                                                                   |
| ----------- | ------------------------------ | ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| **1** | **Basic**                | **In correlated subquery, inner query is <br />dependent on the outer query** | **In non-correlated query inner query does not dependent <br />on the outer query** |
| **2** | **IN and NOT In clause** | **It does not use IN and NOT In clause**                                      | **Non-Correlated subquery are used along-with IN and<br /> NOT IN clause**          |
| **3** | **Run Separately**       | **Inner query can not run alone**                                             | Inner query can not run alone and it's not depended on<br />outer quer**y** ``      |
| **4** | **Performance**          | correlated subqueries are slower queries                                            | **They are faster than correlated subqueries**                                      |

---

Can you explain the difference between a CTE (Common Table Expression) and a subquery in SQL, and give an example of when to use each type?

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
12. LIMIT/FETCH/TOP
