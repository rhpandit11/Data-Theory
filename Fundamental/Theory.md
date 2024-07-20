OLAP

OLTP

Cluster

framework

.csv

.json

AVRO

Parquet

cloud

parallel Processing

Metadata

indexing

structured data, semi, unstructured

serialization, de serialization

---

Cluster:  refers to a collection of interconnected computers (nodes) that work together to perform tasks. These clusters are designed to store and process large volumes of data efficiently.

**OLTP:** OLTP, or Online Transaction Processing, refers to the process of managing and executing transaction-oriented tasks in real-time. Think of it as the backbone of everyday business operations, where transactions such as sales, inventory updates, and customer interactions are swiftly processed.

**Advantages:**

1. Real-time data processing enables quick decision-making.
2. Ensures data integrity and consistency.
3. Supports concurrent access by multiple users.

**Limitations:**

1. Optimized for transaction processing rather than complex analytics.
2. May face scalability challenges with a high volume of transactions.
3. Limited historical data storage capacity.

**Common OLTP systems:**

MySQL

Oracle Database

PostgreSQL

Microsoft SQL Server

IBM DB2

**OLAP:** OLAP(Online Analytical Processing), focuses on analyzing large volumes of data to extract insights and support decision-making. Unlike OLTP, which emphasizes real-time transaction processing, OLAP is geared towards aggregating and summarizing data for in-depth analysis.

**Advantages:**

1. Enables multidimensional analysis for deeper insights.
2. Supports complex queries and ad-hoc reporting.
3. Facilitates trend analysis and forecasting.

**Limitations:**

1. Typically slower in processing real-time data compared to OLTP.
2. Requires substantial computing resources for processing large datasets.
3. May struggle with handling unstructured or semi-structured data.

**Common OLAP systems:**

Amazon Redshift

Snowflake

Google BigQuery

| Category            | OLAP (Online Analytical Processing)                                                                                             | OLTP (Online Transaction Processing)                                                                                                                    |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Definition          | It is well-known as an online database<br />query management system.                                                            | It is well-known as an online database<br />modifying system.                                                                                           |
| Data source         | Consists of historical data from various Databases.                                                                             | Consists of only operational current data.                                                                                                              |
| Method used         | It makes use of a data warehouse.                                                                                               | It makes use of a standard<br />[database management system (DBMS).](https://www.geeksforgeeks.org/introduction-of-dbms-database-management-system-set-1/) |
| Application         | It is subject-oriented. Used for[Data Mining](https://www.geeksforgeeks.org/data-mining/), <br />Analytics, Decisions making, etc. | It is application-oriented. Used for business tasks.                                                                                                    |
| Normalized          | In an OLAP database, tables are not normalized.                                                                                 | In an OLTP database, tables are[normalized (3NF)](https://www.geeksforgeeks.org/third-normal-form-3nf/).                                                   |
| Usage of data       | The data is used in planning, problem-solving,<br />and decision-making.                                                        | The data is used to perform day-to-day<br />fundamental operations.                                                                                     |
| Task                | It provides a multi-dimensional<br />view of different business tasks.                                                          | It reveals a snapshot of present business tasks.                                                                                                        |
| Purpose             | It serves the purpose to extract<br /> information for analysis and decision-making.                                            | It serves the purpose to Insert, Update,<br />and Delete information from the database.                                                                 |
| Volume of data      | A large amount of data is stored typically in TB, PB                                                                            | The size of the data is relatively small as<br />the historical data is archived in MB, and GB.                                                         |
| Queries             | Relatively slow as the amount of<br />data involved is large. Queries may take hours.                                           | Very Fast as the queries operate on 5%<br />of the data.                                                                                                |
| Update              | The OLAP database is not often updated.<br />As a result, data integrity is unaffected.                                         | The data integrity constraint must<br />be maintained in an OLTP database.                                                                              |
| Backup and Recovery | It only needs backup from time<br /> to time as compared to OLTP.                                                               | The backup and recovery process is<br />maintained rigorously                                                                                           |
| Processing time     | The processing of complex queries can take a lengthy time.                                                                      | It is comparatively fast in processing because<br />of simple and straightforward queries.                                                              |
| Types of users      | This data is generally managed by CEO, MD, and GM.                                                                              | This data is managed by clerksForex and<br />managers.                                                                                                  |
| Operations          | Only read and rarely write operations.                                                                                          | Both read and write operations.                                                                                                                         |
| Updates             | With lengthy, scheduled batch operations,<br />data is refreshed on a regular basis.                                            | The user initiates data updates, which are<br />brief and quick.                                                                                        |
| Nature of audience  | The process is focused on the customer.                                                                                         | The process is focused on the market.                                                                                                                   |
| Database Design     | Design with a focus on the subject.                                                                                             | Design that is focused on the application.                                                                                                              |
| Productivity        | Improves the efficiency of business analysts.                                                                                   | Enhances the user’s productivity.                                                                                                                      |

Framework: A framework is a pre-built foundation for application development, offering tools and templates to speed up the process and avoid starting from scratch.
