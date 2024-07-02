BigQuery: BigQuery is a cloud-native data warehouse that handles petabyte-scale analysis using standard SQL. It enables analysts, data scientists, and developers to run fast SQL queries on vast amounts of data.

Key features include:

* Serverless architecture — no infrastructure to manage
* Real-time analysis of streaming data
* In-memory BI Engine for interactive analysis
* Integrated machine learning for predictive insights
* Geospatial analytics and visualization
* Granular access controls and encryption

Architecture:

1. Capacitor - columnar format: store data in columnar storage format called capacitor allows BQ to store and efficiently uery semi-structured data with neseted and repeated fields.
2. colossus - storage: distributed file system is designed to be reliable and fault-tolerant.replaced GFS and capable of handling cluster-wide replication recovery from disk crashes and distributed management.
3. Dremel - execution engine: scalable, interactive ad-hoc query system for analysis of large scale read only nested data.

* Root Node:
  * reads metadata from tables
  * The root server is responsible for communication between the client and mixers
* Inetrmediate Nodes(mixer):
  * performs query optimization and re-writes the query to include horizontal partitions of the table(shards), partial aggregation and filtering.
* Leaf Nodes
  * perform the heavy lifting of reading the data from colossus and performing filters and final aggregeation
  * in a typical dremel tree, there are hundreds or thousands of leaf nodes.
  * each node provides execution threads(slots), which BQ automatically calculates for each query based on its size and complexity.

Execution:

1. user submits a query to BQ ex: SELECT count(*) from mytable where timestamp > '2021-01-01';
2. query received by root node of dremel serving tree, which is starting point of query execution.
3. root nodes route the query to intermediate nodes(mixers) of the serving tree.These nodes perform query optimization and rewrite the query to include horizontal partitions of the table and partial aggregations and filtering.
4. In this ex, query optimizer might decide to pation the table based on timestamp and include partitions that have timestamp greate than '2021-01-01'
5. intermediate nodes than send ther rewritten query to leaf nodes for execution.Leaf node read the relevant partitions of the table from colossus and perform the filters and final aggregation specified in the query.
6. in this ex, leaf node would count the number of rows in the partitions that have timestap greate than and return the result to intermediate nodes.
7. Intermediate nodes than pass the result back up to serving tree to the root node which result final query such as "count(*) = 1000000" to the user.

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

**What is fail-safe?**

What is your critical data deleted before 7 days and now you want to restore it???? Again here Google came to our rescue , BigQuery provides a **fail-safe** period.During the fail-safe period, deleted data is automatically retained for an additional seven days after the time travel window, so that the data is available for emergency recovery. Data is recoverable at the table level. The fail-safe period is not configurable. You can’t query or directly recover data in fail-safe storage. To recover data from fail-safe storage, contact Cloud customer support.

**How to work with Arrays and Structs in Google BigQuery:**

Arrays: ike in any other language, are a collection of elements of the same data type. **address_history: [“current”, “previous”, “birth”]**

Structs and how are they used in BigQuery: A struct is a data type that has attributes in key-value pairs, just like a dictionary in Python.

Within each record, multiple attributes have their own values. These attributes can either be referred to as keys or *Struct* columns.

> id:”1",
> name:”abc”,
> age:”20",
> **address_history: {
> “status”:”current”,
> “address”:”London”,
> “postcode”:”ABC123D”
> }  **

What are Array of Structs and how can we use them in BigQuery: if we want to store multiple *Structs* against each key/ID, *Array of Structs* is the option.

For example: Address_history is an *Array* column having 3 {} *Structs* inside [] .

> id:”1",
> name:”abc”,
> age:”20",
> **address_history: [
> { “status”:”current”, “address”:”London”, “postcode”:”ABC123D” },
> { “status”:”previous”, “address”:”New Delhi”, “postcode”:”738497" },
> { “status”:”birth”, “address”:”New York”, “postcode”:”SHI747H” }
> ]**

How do I know by looking at the schema if it is Array/Struct/Array of Structs:

Array -> REPEATED (schema)

Struct -> RECORD (for selecting one value we use dot) with Nullable mode

Array of Structs ->RECORD | REPEATED (mode)

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