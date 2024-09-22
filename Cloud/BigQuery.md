    BigQuery: BigQuery is a cloud-native data warehouse that handles petabyte-scale analysis using standard SQL. It enables analysts, data scientists, and developers to run fast SQL queries on vast amounts of data.

Key features include:

* Serverless architecture — no infrastructure to manage
* Real-time analysis of streaming data
* In-memory BI Engine for interactive analysis
* Integrated machine learning for predictive insights
* Geospatial analytics and visualization
* Granular access controls and encryption

Architecture:

1. Capacitor — The Storage Format - bigquery's columnar storage format
   * columnar Storage - data is stored in columns because it is more efficient for read-heavy tasks because it allows bq to read only desired output columns saving time and resources.
   * High Compression - Capacitor compress data efficiently which reduces storage costs and speeds up data retrieval.
   * Nested Data - BQ supports complex nested data structures capacitor handles this by storing each column in separate files.
2. Colossus - The Distributed Storage System - provides reliability,fault tolerance scalability and geo-replication(data is copied accross diff geographic regions).
3. Dremel - The Query Execution Engine - process query in BQ. Queries are executed through multi-level tree structure that includes root, intermediate and leaf nodes.Provides parallel processing and automatically optimizes queries to ensure they run as efficiently as possible(make use of index and data partitions).

* Root Node: reads metadata from tables and responsible for communication between the client and mixers
* Inetrmediate Nodes(mixers): optimize and distribute these tasks.
* Leaf Nodes: perform the actual data reading and computition

4. Borg - The Compute Manager - is google's cluster management system that allocates computational resources for BQ.It ensures : Resource Allocation, Fault Tolerance, Job Scheduling
5. Jupiter - The Network Backbone - Google's high-speed network that connects all parts of the BQ Architecture.It provides: High bandwith with low latency.

Execution:

1. Query Submission : You submit a query, like `SELECT COUNT(*) FROM mytable WHERE date > ‘2023–01–01’`.
2. Root Node Processing : The root node of Dremel receives the query and reads metadata to understand the table structure.
3. Task Distribution : The query is divided into smaller tasks, which are sent to intermediate nodes.
4. Optimization : Intermediate nodes optimize the tasks, determining the best way to execute them (e.g., which data partitions to read).
5. Data Retrieval and Computation : Leaf nodes read the necessary data from Colossus, apply filters, and perform calculations.
6. Aggregation : Results are aggregated by intermediate nodes and sent back to the root node.
7. Final Result : The root node compiles the final result and returns it to you.

---

Google BigQuery data types:

* NUMERIC (including INT64, NUMERIC, BIGNUMERIC, and FLOAT64)

  * Integer type (INT64) - The values can't contain decimals or fractional components.
  * Numeric type (NUMERIC DECIMAL) - Stores exact, high-precision decimal numbers with up to 38 digits of precision.use for storing large financial data,currency values and precise calculations.
  * Bignumeric type (BIGNUMERIC BIGDECIMAL) - similar as numeric but allows even larger numbers with more digits of precision.
  * Floating point type (FLOAT64) - stores 64-bit floating point number use for store decimal precision numbers.
* BOOLEAN - store logical valuse of either TRUE or FALSE use for flags, binary condition or toggles in data.
* STRING - stores text data operates on Unicode characters use for storing names,description and text fields.
* BYTES - stores binary data as a sequence of bytes rather than Unicode characters useful for storing images,files, encoded data etc.
* TIME (including DATE, TIME, DATETIME, and TIMESTAMP)

  * DATE - stores calendar dates without time.
  * TIME - stores time-of-day values without date.
  * DATETIME - stores both the date and time(without time zone information)
  * TIMESTAMP - stores an exact point in time, including the date and time(with time zone).
* GEOGRAPHY - stores latitude/longitude co-ordinates, geometric shapes points, lines, and polygons.
* ARRAY - stores a collections of  ordered list of items of a single data type. useful for store list of related data such as user tags or items in an order.Note that none of these elements can be of an ARRAY type themselves.
* STRUCT - stores a collection of key-value pairs, where each key is associated with a value of a specific data type.userful for storing ex. user profile with multiple attributes. EX: STRUCT<name STRING, age INT64>('John Doe', 30)

GEOGRAPHY, ARRAY,STRUCT will not work on orderby, groupby, distinct, partitionby, compare to others.

---

Big Query Time Travel:(ex: avenger endgame)

In bigquery time travel is used to access historical data for analysis and troubleshooting.This means that you can query data that was stored, updated, or deleted in the past.

You can set the duration of the time travel window, from a **minimum of two** days to a  **maximum of seven days** . Seven days is the  **default** .You can query a table’s historical data from any point in time within the time travel window by using a clause SYSTEM_TIMEASOF TIMESTAMP_SUB.

**Note:** To restore data from a deleted table, you need to have the admin role on the corresponding table.

How to Enable:

1. In the **Explorer** panel, expand your project and select a dataset.
2. Expand the **Actions** option and click  **Open** .
3. In the **Details** panel, click  **Edit details** .
4. Expand  **Advanced options** , then select the **Time travel window** to use.
5. Click  **Save** .

benefits:

* Troubleshoot problems with historical data.
* Recover data that was accidentally deleted.
* Analyze data trends over time.
* Compare data from different points in time.

---

**What is fail-safe?**

What is your critical data deleted before 7 days and now you want to restore it???? Again here Google came to our rescue , BigQuery provides a **fail-safe** period.During the fail-safe period, deleted data is automatically retained for an additional seven days after the time travel window, so that the data is available for emergency recovery. Data is recoverable at the table level. The fail-safe period is not configurable. You can’t query or directly recover data in fail-safe storage. To recover data from fail-safe storage, contact Cloud customer support.

---

**What are partitions and clusters?**

Partitioning and clustering are two very effective techniques to minimize query costs and increase performance (using fewer resources while improving speed).

The idea behind these techniques is to limit the amount of data that needs to be read when running a query.

**Partitions:** **Table partitioning** is a technique for splitting large tables into smaller ones.BigQuery will store separately the different partitions at a physical level (meaning the data will be stored on different servers).

You can create a partitioned table based on a column, also known as a  **partitioning key** . In BigQuery, you can partition your table using different keys:

* **Time-unit column** : Tables are partitioned based on a time value such as timestamps or dates.
* **Ingestion time** : Tables are partitioned based on the timestamp when BigQuery ingests the data.
* **Integer range** : Tables are partitioned based on a number.

BigQuery has  **a limit of 4,000 partitions per table** .

**Clusters:** Clusters will allow BigQuery to keep data that is similar closer together, allowing a query to scan fewer data. Based on the values in the column you chose for clustering, BigQuery will automatically sort these values and also decide on how to store them in optimal storage blocks.

BigQuery has  **a limit of 4 cluster columns per table** .

**Clustering Benefits:**

* Clustering provides granularity beyond what partitioning can offer.
* Ideal for situations where the number of values in a column or group of columns is large (cardinality) and exceeds partitioning limitations.
* Useful when the partitioning strategy results in an excessive number of partitions beyond the 4000 limit.
* Appropriate when the partitioning strategy leads to frequent modifications of partitions, which can be costly.

**Partitioning Benefits:**

* Partitioning offers known cost benefits upfront, making it suitable for managing query costs effectively.
* Excellent when you need to aggregate or filter data based on a single column.
* Allows for partition-level management, including creating, deleting, and moving partitions, which is not feasible with clustering.

Slot : A BigQuery slot is  **a virtual CPU used by BigQuery to execute SQL queries** .

---

In  **BigQuery** , **clustering** and **partitioning** are optimization techniques used to organize and manage large datasets for faster and more efficient query performance.

Partitioning: Partitioning divides table into smaller, managable segments(partitions) based on certain column typically a timestamp or an integer.Queries that only need data from specific partitons can skip over irrelevant partitions, improving query performance and reducing cost by scanning less data.

Types of Partitioning:

* Time-base Partitioning: this partition data by DATE, TIMESTAMP, DATETIME. Most common as data is often collected over time. e.g daily logs.
* Integer-range Partitioning: This partition data based on custom integer column range useful when the data isn't time-based but needs to be organized by sequental or meaningful numeric values.

EX: There is an e-commerce comapany that collects millions of transactions every day.Now need to analyze transactions quickly based on different date ranges(e.g. daily, weekly, or monthly). it provides benefits for queries like fetch data only for a specific month, bq will only scan partitions for that month rather than the entire dataset.

R.EX: A social media platform like Twitter or Facebook can partition user activity logs by date, ensuring that queries analyzing user activity over a specific time range (e.g., the past week) are efficient and scalable.

Clustering: Clustering is a way to automatically organize data within the partitions based on the values of certain columns. Data is physically stored based on the clustered columns, Improves performance when you run queries with where, orderBy, or groupBy clauses on the clustered columns.It works on partition level so, it's often combined with partitioning for more efficient queries.

EX: e-commerce company wants to frequently query transactions by customer_id and product_id within a certain date range.So, we can partition the table by transaction_date and cluster it by customer_id and product_id.Now, when we query to get transactions for a specific customer and product within a date range, BQ will scan only the relevant partitions and clustered data within those partitions.

REX: In healthcare system, patient records can be partitioned by admission_date and clustered by patient_id and hospital_id.This ensures that when querying records for a specific patient at a specific hospital over a time period, only relevant partitions abd clusters are scanned , leading to quicker query results.

Parttioning and Clustering Combine:

Example, netflix that stores user activity logs.Each log contains details about which movie or series a user watched, the timestamp, and the region from which they accessed the platform.

We can partition the table by DATE(activity_timestamp) since activity data comes in daily and you're likely to run queries on recent activities.

And we can cluster the table by user_id and region because most of queries will filter data based on these columns.

Benefits of Clustering and Partitioning:

1. Reduced Query Costs
2. Improved query performance
3. Efficient data organization

Key Difference:

1. partitioning divides the table into logical segments where clustering sorts data within partitions based on cloumns.
2. Partitioning used for reducing the amount of data scanned accross large datasets based on a data or range.Clustering improves query performance on specific columns using filtering, ordering or grouping.
3. Partitioning operates on the table level and clustering operates within each partition.
4. Partitioning is best for date or range-based queries (e.g querying data by day, month, year) where as clustering best for column-based queries like filtering by user_id or product_id).

---

SESSION_USER: security function in bq. Help to find out the email or principal of the user that is running the query.

ex: select SESSION_USER()

---

Tables Type:

* External Tables - External tables are stored outside out of BigQuery storage and refer to data that's stored outside of BigQuery.
* Standard Tables- Standard BigQuery tables contain structured data and are stored in BigQuery storage in a columnar format.
* Materialized Views - [Materialized views](https://cloud.google.com/bigquery/docs/materialized-views-intro), which are precomputed views that periodically cache the results of the view query. The cached
  results are stored in BigQuery storage.
* [Views](https://cloud.google.com/bigquery/docs/views-intro), which are logical tables that are defined by using SQL queries. These queries define the view that is run each time the view is queried.

---

What is a wildcard table? Typically, a wildcard table like `events_*` is just an old-fashioned version of what is called a **partitioned table** now. These `some_table_name_*` tables have the same prefix and usually end with a stringified `date`, i.e.

---

***What is smart-tuning?***

BigQuery automatically rewrites queries to use materialized views whenever possible. Automatic rewriting improves query performance and cost, and does not change query results.

Querying does not automatically trigger a materialized refresh. For a query to be rewritten, the materialized view must meet the following conditions:

* Belong to the same dataset as one of its base tables.
* Use the same set of base tables as the query.
* Include all columns being read.
* Include all rows being read.

---
