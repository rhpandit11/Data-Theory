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
| Productivity        | Improves the efficiency of business analysts.                                                                                   | Enhances the user's productivity.                                                                                                                       |

Framework: A framework is a pre-built foundation for application development, offering tools and templates to speed up the process and avoid starting from scratch.

Purpose of Serialization and Deserialization: we store data in data structures like string, list, dict format but transporting them in the same data structure is inefficient.So in order to transfer data accross network we need to transform(serialize) the data into byte stream with enough information in a way that it can be retransformed (deserialized) back into its original format at its destination.

Database: A database is a collection of data or information.

Datawarehouse: A datawarehouse is a system that stores highly structured information from various sources. Typically  store current and hiostorical data from one or more systems.The goal is to utilize it to analyze the data, look for insights and create BI in the form of reports and dashboards.

DataLake: A datalake is a repository of data from disparate sources that is stored in its orginal/raw format.what sets data lake apart is their ability to store data in varity of formats including JSON, BSON, CSV, TSV, AVRO, ORC and parquet.

Difference:

* A database stores the current data required to power an application.
* A datawarehouse store current and historical data from one or more systems in a predefined and fixed schema which allows to easily analze the data.
* A datalake stores current and historical data from one or more systems in its raw format.

Different File Formats:

File Should:

1. Faster read times
2. Faster write times
3. Splittable files
4. Schema evolution support
5. Advanced compression support

Text Files(csv,tsv):

* Behaviour: Each line is a record/data, and lines are terminated by a newline character(\n).
* Read/Write: Good write perrformance but slow reads
* compression: Do not support block compression
* splitable: Text-files are inherently splittable on \n character
* Schema Evolution: Limited schema evolution(New fields can only be appended to existing fields while old fields can never be deleted).

Sequence File:

* Behaviour: Each record is stored as a key value pair in binary format
* Read/Write: Good write performance than text files
* compression: support block compression
* Splitable: sequence files are splittable
* Schema Evolution: Limited schema evolution(New fields can only be appended to existing fields while old fields can never be deleted).

Avro File:

* Behaviour: It is a file format plus a serialization and deserialization framework. Avro uses JSON for defining data types and serializes data in compact binary format.
* Read/Write: Average read/write performance
* compression: support block compression
* Splitable: Avro files are splittable
* Schema Evolution: was mainly designed for schema evolution. Fields can renamed, added, deleted while old files can still be read with the new schema.

Columnar File Formats:

* In columnar file format instead of just storing rows of data adjacent to one another we also store column values adjacent to each other.
* So datasets are partitioned both horizontally and vertically

RC(Record Columnar) File:

* Behaviour: These are flat files consisting of binary key/value pairs and it shares much similarity with sequnce file.
* Read/Write: was developed for faster reads but with a compromise with write peformance
* compression: provides significant block compression, can be compressed with high compression ratios.
* Splitable: RC files are splittable
* Schema Evolution: Was mainly designed for Faster reads so No schema evolution.

ORC File:

* Behaviour: A better version fot RC file
* Read/Write: was developed for faster reads but with a compromise with write peformance(better than RC file)
* compression: provides significant block compression, can be compressed with high compression ratios.(better than RC file)
* Splitable: ORC files are splittable
* Schema Evolution: Was mainly designed for Faster reads so No schema evolution.

Parquet File:

* Behaviour: It is a columnar file format, similar to RC and ORC. Parquet stores nested data structures in a flat columnar format.
* Read/Write: Faster reads with slow writes
* compression: Support compression mostly with snappy algorithm
* Splitable: parquet files are conditionally splittable
* Schema Evolution: Limited schema evolution(New Fields can only be appended to existing fields while old fields can never be deleted).

- Use **CSV** for simple and small datasets.
- Use **JSON** for semi-structured data and ease of readability.
- Use **Avro** for efficient data serialization with schema evolution.
- Use **Parquet** or **ORC** for high-performance analytics on large datasets.
- Use *SequenceFile* for key-value pair data storage in Hadoop.
- Use *RCFile* for efficient columnar storage in Hadoop environments.
