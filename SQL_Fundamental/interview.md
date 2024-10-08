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

1. 𝐔𝐧𝐢𝐪𝐮𝐞 𝐊𝐞𝐲 - ensures that all values in a column (or a set of columns) are uniqueacross the table. Unlike a primary key, a unique key allows one NULLvalue. Use: It prevents duplicate values in the column, but unlike the primary key, it is not necessarily used for identifying rows.
2. Super Key: is any set of columns that can uniquely identify a row in a table. It can contain additional columns besides the minimum required to uniquely identify rows (i.e., it might include non-essential columns along with the primary key). Use: It's a superset of the primary key, often used conceptually in database design.
   Example: In a table, both (EmployeeID, Name) and (EmployeeID) could be super keys if EmployeeID is the primary key.
3. Candidate Keys(minimum super key): is any column (or set of columns) that can potentially become a primary key. A table can have multiple candidate keys, but only one can be chosen as the primary key. Use: It serves as a potential unique identifier for the table. Example: In a table of employees, both EmployeeID and SSN might be candidate keys, but only one will be chosen as the primary key.
4. Primary Key: is a column (or a set of columns) that uniquely identifies each row in a table. It ensures that no duplicate or NULL values are present in the specified column. Use: It helps in identifying records uniquely and is usually indexed for fast retrieval.
5. Alternate Key: different from primary key, if necessary primary key can be selected from any of the alternate keys, sometimes to improve search speed, alternate keys are used for indexing.
6. Foreign Key: is a column (or a set of columns) in one table that links to the primary key of another table. It enforces referential integrity between the two tables.Use: It establishes a relationship between tables and ensures that the value in the foreign key column exists in the primary key column of the referenced table.
7. Composite Key: is a combination of two or more columns that together uniquely identify a row in the table. Neither of the columns alone can act as a primary key. Use: It is useful when no single column can uniquely identify a record, so multiple columns are combined.
8. Surrogate Key: allow under certain conditions like main PK is very large, challenging PK, lack of key, when not natural choice. EX: student Table {student_id}

| Key Type      | Definition                                          | Uniqueness   | Null Values | Purpose                                     | Index                   | Usage             | Alteration                           |
| ------------- | --------------------------------------------------- | ------------ | ----------- | ------------------------------------------- | ----------------------- | ----------------- | ------------------------------------ |
| Primary Key   | Uniquely identifies each record in a table.         | Required     | Not Allowed | Data integrity, record identification.      | Creates Unique Index    | Within same table | May be complex, impact other tables. |
| Foreign Key   | Establishes a relationship between tables.          | Not Required | Allowed     | Data consistency, relationship maintenance. | May create Index        | Between tables    | More flexible for maintenance.       |
| Candidate Key | Alternative unique keys that could be primary keys. | Required     | Not Allowed | Backup primary key options.                 | May create Index        | Within same table | May become primary key.              |
| Super Key     | Combination of attributes that uniquely identify.   | Required     | Allowed     | Conceptual, not enforced.                   | May create Index        | Conceptual use    | N/A                                  |
| Composite Key | Combined attributes used as a single key.           | Required     | Not Allowed | Specialized unique identification.          | Creates Composite Index | Within same table | May be complex, impact performance.  |
| Unique Key    | Ensures column(s) have unique values.               | Required     | Allowed     | Enforce uniqueness, no primary key.         | Creates Unique Index    | Within same table | May be used as primary key.          |
| Surrogate Key | Artificial keys assigned for record identification. | Required     | Not Allowed | Enhanced data privacy, data warehousing.    | Creates Unique Index    | Within same table | Generally static, non-changing.      |

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

syntax:

```sql
create procedure GetAllEmployee    --Create stored procedure syntax
as 
begin
select * from Employee;
end
```

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

 **Use Cases** :

* **View** : Suitable for dynamic, frequently changing data where real-time accuracy is important.
* **Materialized View** : Suitable for scenarios where query performance is critical and the data does not need to be real-time, or can be refreshed periodically.

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

Joins : combines data from two tables.

1. LEFT JOIN : LEFT JOIN returns all rows from the left table with matching rows from the right table. Rows without a match are filled
   with NULLs. LEFT JOIN is also called LEFT OUTER JOIN.
2. RIGHT JOIN: RIGHT JOIN returns all rows from the right table with matching rows from the left table. Rows without a match are
   filled with NULLs. RIGHT JOIN is also called RIGHT OUTER JOIN.
3. FULL JOIN: FULL JOIN returns all rows from the left table and all rows from the right table. It fills the non-matching rows with
   NULLs. FULL JOIN is also called FULL OUTER JOIN.
4. CROSS JOIN: CROSS JOIN returns all possible combinations of rows from the left and right tables.cartesian product of the two tables included in the join.
5. SELF JOIN: You can join a table to itself.
6. NATURAL JOIN: If the tables have columns with the same name, you can use NATURAL JOIN instead of JOIN.

Difference:

| **INNER JOIN**                                    | **LEFT JOIN**                                                                          | **RIGHT JOIN**                                                                        | **FULL JOIN**                                            | **SELF JOIN**                                                                                                                    | CARTESIAN JOIN                                                                                      |
| ------------------------------------------------------- | -------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| returns rows when there<br />is a match in both tables. | returns all rows from the left table, even<br /> if there are no matches in the right table. | returns all rows from the right table,<br />even if there are no matches in the left table. | combines the results of both<br /> left and right outer joins. | joins a table to itself as<br />if the table were two tables,<br />temporarily renaming at least <br />one table in the SQL statement. | returns the Cartesian product of the<br />sets of records from the two or more<br /> joined tables. |

**Products Table:**

| ProductID | ProductName | SupplierID |
| --------- | ----------- | ---------- |
| 1         | Apples      | 100        |
| 2         | Oranges     | 101        |
| 3         | Bananas     | NULL       |
| 4         | Grapes      | 102        |
| 5         | Pineapples  | 103        |

**Suppliers Table:**

| SupplierID | SupplierName   |
| ---------- | -------------- |
| 100        | Fresh Farms    |
| 101        | Citrus World   |
| 102        | Vine Vineyards |
| 104        | Tropical Goods |

Inner Join:

SELECT Products.ProductName, Suppliers.SupplierName
FROM Products
INNER JOIN Suppliers
ON Products.SupplierID = Suppliers.SupplierID;

| ProductName | SupplierName   |
| ----------- | -------------- |
| Apples      | Fresh Farms    |
| Oranges     | Citrus World   |
| Grapes      | Vine Vineyards |

Self Join:

SELECT p1.ProductName AS Product1, p2.ProductName AS Product2, p1.SupplierID
FROM Products p1
JOIN Products p2
ON p1.SupplierID = p2.SupplierID
AND p1.ProductID < p2.ProductID;

| Product1 | Product2   | SupplierID |
| -------- | ---------- | ---------- |
| Apples   | Oranges    | 100        |
| Grapes   | Pineapples | 102        |

LEFT JOIN (LEFT OUTER JOIN):

SELECT Products.ProductName, Suppliers.SupplierName
FROM Products
LEFT JOIN Suppliers
ON Products.SupplierID = Suppliers.SupplierID;

| ProductName | SupplierName   |
| ----------- | -------------- |
| Apples      | Fresh Farms    |
| Oranges     | Citrus World   |
| Bananas     | NULL           |
| Grapes      | Vine Vineyards |
| Pineapples  | NULL           |

RIGHT JOIN (RIGHT OUTER JOIN):

SELECT Products.ProductName, Suppliers.SupplierName
FROM Products
RIGHT JOIN Suppliers
ON Products.SupplierID = Suppliers.SupplierID;

| ProductName | SupplierName   |
| ----------- | -------------- |
| Apples      | Fresh Farms    |
| Oranges     | Citrus World   |
| Grapes      | Vine Vineyards |
| NULL        | Tropical Goods |

FULL OUTER JOIN:

| ProductName | SupplierName   |
| ----------- | -------------- |
| Apples      | Fresh Farms    |
| Oranges     | Citrus World   |
| Bananas     | NULL           |
| Grapes      | Vine Vineyards |
| Pineapples  | NULL           |
| NULL        | Tropical Goods |

Natural Join:

SELECT *
FROM Products
NATURAL JOIN Suppliers;

| ProductID | ProductName | SupplierID | SupplierName   |
| --------- | ----------- | ---------- | -------------- |
| 1         | Apples      | 100        | Fresh Farms    |
| 2         | Oranges     | 101        | Citrus World   |
| 4         | Grapes      | 102        | Vine Vineyards |

---

SUBQUERIES: A subquery is a query that is nested inside another query, or inside another subquery. There are different types of subqueries.

* SINGLE VALUE: The simplest subquery returns exactly one column and exactly one row. It can be used with comparison operators =, <, <=, >, or >=. Appear in SELECT statements, clause like where and having or from.

  ```sql
  SELECT name FROM city
  WHERE rating = (
  SELECT rating
  FROM city
  WHERE name = 'Paris'
  ```
* MULTIPLE VALUES: A subquery can also return multiple columns or multiple rows. Such subqueries can be used with operators IN, EXISTS, ALL, or ANY.Appear in SELECT statements, clause like where and having or from.

  ```sql
  SELECT name
  FROM city
  WHERE country_id IN (
  SELECT country_id
  FROM country
  WHERE population > 20000000
  );
  ```
* CORRELATED: A correlated subquery refers to the tables introduced in the outer query. A correlated subquery depends on the outer query. It cannot be run independently from the outer query.

  ```sql
  SELECT *
  FROM city main_city
  WHERE population > (
  SELECT AVG(population)
  FROM city average_city
  WHERE average_city.country_id = main_city.country_id
  );
  ```

Key differences

* Execution: Non-correlated runs once, correlated runs for each row in the outer query.
* Dependency: Non-correlated is independent, correlated needs data from the outer query.
* Performance: Non-correlated can be faster due to fewer executions.
* Complexity: Correlated queries can be more complex and harder to read.

**Best Practices:**

* Prefer non-correlated subqueries whenever possible: If the required information can be obtained independently of the outer query, use a non-correlated subquery for potential performance benefits.
* Optimize correlated subqueries carefully: If correlated subqueries are necessary, consider techniques like using indexes and optimizing the subquery logic to minimize execution time.
* Test and measure: Always test and measure the performance of different query approaches with your specific data and workload to determine the most efficient solution for your use case.

---

CTE: SQL CTEs or Common Table Expressions are nothing but temporary tables that you can use within a query.They can be referenced within a SELECT, INSERT, UPDATE, or DELETE statement.

Recursive CTEs: CTEs can be used for recursive queries, which are queries that refer to themselves to generate a result. For example, you can use a recursive CTE to generate a list of numbers or dates.

```sql
WITH recursive numbers (n) AS (
    SELECT 1
    UNION ALL
    SELECT n + 1
    FROM numbers
    WHERE n < 10
)
SELECT n
FROM numbers;
```

When to Use:

* CTE can help you to avoid repeated sub queries.
* A CTE can be used multiple times within your statement, e.g. within a `JOIN` with a dynamic behavior depending on the actual row-count.
* You can use multiple CTEs within one statement and you can use the result of one CTE within a later CTE.
* There are recursive (or better  *iterative* ) CTEs.

Advantages:

* useable in  *ad-hoc* -queries (functions, views)
* no unexpected side effects (most narrow scope)

Disadvantages:

* You cannot use the CTE's result in different statements
* You cannot use indexes, statistics to optimize your CTE's set (although it will implicitly use existing indexes and statistics of the targeted objects - if appropriate).

difference between Subquery and CTE

1. cte's are defined using the "with" keyword followed by the CTE name and columns list(optional).Where as subqueries are enclosed within parentheses and can be used in various parts of a query such as the SELECT,FROM,WHERE or HAVING clauses.
2. CTE's are used to create temporary result sets that can be referenced multiple times within a larger query hence improve code readability and maintainability.Subqueries are used to retrieve data based on the result of an outer query.Commonly used for data filtering,joining related tables or performing calculations on subsets of data.
3. CTEs can improve performance by making queries run faster, but it depends on how complicated the query is and how much data it involves.Subqueries can sometimes result in poor performance, particularly when dealing with large datasets or complex join conditions.
4. CTEs make queries easier to read and maintain by breaking them into smaller, managable parts.Subqueries can make queries more complicated, especially when they are deeply nested**,** which makes them harder to understand and update.
5. CTEs have a **limited scope** and exist temporarily during a single query, not accessible outside it.Subqueries are embedded within a query and have a **limited scope,** retrieving data based on the outer query.
6. CTE's act as a named temporary result set whreas subquery is a part of a larger query.
7. CTE's can be used for recursive queries where subquery used for filtering or retrieving specific values.
8. Cte's can be referenced by multiple queries within a single query block, subquery cannot be referenced outside the query where it is defined.
9. Use CTEs to make complex queries easier to read and organize, especially when dealing with repeated subqueries.Use subqueries sparingly, avoiding excessive nesting for better code readability and performance.

---

Window Functions: SQL function where the input values are taken from a "window" of one or more rows in the results set of a SELECT statement.

AGGREGATE FUNCTIONS VS. WINDOW FUNCTIONS: unlike aggregate functions, window functions do not collapse rows.

PARTITION BY: divides rows into multiple groups, called partitions, to which the window function is applied.

1. Aggregate Functions
   * avg() - average value for rows within the window frame
   * count() - count of values for rows within the window frame
   * max() - maximum value within the window frame
   * min() - minimum value within the window frame
   * sum() - sum of values within the window frame
2. Ranking Functions
   * row_number() - unique number for each row within partition, with different numbers for tied values (give unique value for duplicates values also)
   * rank() - ranking within partition, with gaps and same ranking for tied values - (give samevalue for duplicates values and skip next digits)
   * dense_rank() - ranking within partition, with no gaps and same ranking for tied values - (give samevalue for duplicates values and not skip digits)
3. Distribution Functions
   * percent_rank() - he percentile ranking number of a row—a value in [0, 1] interval: (rank - 1) / (total number of rows - 1)
   * cume_dist()  - the cumulative distribution of a value within a group of values, i.e., the number of rows with values less than or equal to the current row’s value divided by the total number of rows; a value in (0, 1] interval
4. Analytic Functions
   * lead(expr, offset, default)
   * lag(expr, offset, default)
   * ntile(n) - divide rows within a partition as equally as possible into n groups, and assign each row its group number.
   * first_value(expr) - the value for the first row within the window frame
   * last_value(expr) - the value for the last row within the window frame
   * nth_value(expr,n) - the value for the n-th row within the window frame; n must be an integer

---
