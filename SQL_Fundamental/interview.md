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

| Key Type      | Definition                                          | Uniqueness   | Null Values | Purpose                                     | Index                   | Usage             | Alteration                           |
| ------------- | --------------------------------------------------- | ------------ | ----------- | ------------------------------------------- | ----------------------- | ----------------- | ------------------------------------ |
| Primary Key   | Uniquely identifies each record in a table.         | Required     | Not Allowed | Data integrity, record identification.      | Creates Unique Index    | Within same table | May be complex, impact other tables. |
| Foreign Key   | Establishes a relationship between tables.          | Not Required | Allowed     | Data consistency, relationship maintenance. | May create Index        | Between tables    | More flexible for maintenance.       |
| Candidate Key | Alternative unique keys that could be primary keys. | Required     | Not Allowed | Backup primary key options.                 | May create Index        | Within same table | May become primary key.              |
| Super Key     | Combination of attributes that uniquely identify.   | Required     | Allowed     | Conceptual, not enforced.                   | May create Index        | Conceptual use    | N/A                                  |
| Composite Key | Combined attributes used as a single key.           | Required     | Not Allowed | Specialized unique identification.          | Creates Composite Index | Within same table | May be complex, impact performance.  |
| Unique Key    | Ensures column(s) have unique values.               | Required     | Allowed     | Enforce uniqueness, no primary key.         | Creates Unique Index    | Within same table | May be used as primary key.          |
| Surrogate Key | Artificial keys assigned for record identification. | Required     | Not Allowed | Enhanced data privacy, data warehousing.    | Creates Unique Index    | Within same table | Generally static, non-changing.      |
