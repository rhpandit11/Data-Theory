**Spark:**  spark is an open-source unified analytics engine for large scale data processing.

* Fault tolerance - spark is designed to handle worker node failures.
* Dynamic In Nature -
* Lazy Evaluation - All the transformations are lazily ecaluated.
* Real-Time Stream Processing - we can write streaming jobs the same way like batch jobs.
* Speed - spark achieves faster speed by minimizing disk read/write operations for intermediate results.
* Reusability - spark code can be used for batch-processing, stream-processing, ad-hoc queries
* In Memory Computing - Apache Spark is capable of processing tasks in memory and it is not required to write back intermediate results to the disk.
* Supporting Multiple languages - JAVA, SCALA, PYTHON, R, SparkSQL
* Integrated with Hadoop - integrates very well with Hadoop file system HDFS and support multiple file formats like parquet, json, csv, ORC, Avro etc.

**Spark Architecture:**

1. Programming Layer (Java, Scala, R, Python)
2. Liabrary Layer - (MLlib, SparkSQL, Graphx, Streaming)
3. Spark core engine - (Apache Spark)
4. Spark Management or cluseter layer - (Kubernetes, Apache Hadoop YARN, Mesos, Apache Spark)
5. Storage layer - (Local FS, s3, blob storage, HDFS)

**Difference between mapreduce and spark:**

| MapReduce                                                                             | Spark                                                                  |
| ------------------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| read/write data to a disk                                                             | spark can do it in-memory make it faster.                              |
| developed in java                                                                     | developed in scala                                                     |
| Fault tolerance is done through replication                                           | done throgh rdd                                                        |
| Hard to work with real-time data                                                      | Easy                                                                   |
| Less costly comparison to spark                                                       | more costly                                                            |
| Hadoop can work or process far larger datasets than spark                             | Less compare to hadoop                                                 |
| MapReduce requires an external scheduler for jobs.                                    | Spark has its own job scheduler due to the in-memory data computation. |
| A program written using map reduce has more lines of code<br />when compared to spark | A program written using spark has less lines of code                   |
| Linear - Run steps one by one                                                         | Lazy evolution                                                         |
| Operation run step by step                                                            | Till the Action is triggered none of the Transaction will work.       |

**Spark Execution Model:**

* **Driver** - brain of spark framework that runs the main() function of the application and also creates the SparkContext/session. Also host bunch of process which are part of application like (SparkEnv,DagScheduler, TaskScheduler, SparkUI)
* **Executor** - worker node responsible for executing the given task by driver.

**Driver Works:**

* creating the sparkcontext/session which serves as a entry point for spark functionality
* compute the application requirement resoures and also manage dynamic allocation lifecycle
* Tasks distributor among the executors
* react on executor failure
* monitor the executor progress
* send response to user
* Converting transformations into a logical Directed Acyclic Graph (DAG)
* through the metadata job it powers the spark WEBUI

**Executor  Works:** execute the task assigned by driver, report the progress back to driver, Storing data for the application in memory or disk storage.

Spark Programming Model:

* **Application:** When we submit the Spark code to a cluster it creates a Spark Application.
* **Job:** The Job is the top-level execution for any Spark application. A Job corresponds to an Action in a Spark application.
* **Stage:** A stage represents a set of tasks that can be executed in parallel. There are two types of stages in Spark: shuffle stages and non-shuffle stages. Shuffle stages involve the exchange of data between nodes, while non-shuffle stages do not.(groupByKey, sortByKey).
* **Task:** Stages will be further divided into various tasks. Each stage is divided into task.A task is a unit of execution that runs on a single machine.

**Spark Internally Working:**

* User submits a Spark application.
* Driver process starts and sets up the SparkContext.
* The SparkContext connects to the cluster manager to negotiate resources.
* The cluster manager launches executors on worker nodes.
* Executors register with the driver.
* Driver creates a logical plan (DAG) and converts it into a physical plan (tasks).
* Tasks are sent to executors by the driver.
* Executors execute tasks, process data, and store intermediate results.
* Executors return results to the driver.
* Driver compiles the results and completes the job.

SparkContext: was the primary entry point for interacting with spark, represent the connection to the spark cluster and was responsible for co-ordinating task execution.

SparkSession: spark2.0 introduced as unified entry point that encapsulates sparkcontext while offering much more.Provides user-friendly API for working with structured data in the form of dataframes and datasets.

| SparkContext                                                                                                               | SparkSession                                                                                                    |
| -------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| preferred way to work with the lower-level API like RDD,<br />Accumulator and broadcast variable                           | prefered way when to work with data structure like<br />dataframe and datasets as it provides simpler interface |
| can be created only once in spark application at any time                                                                  | can be created multiple times                                                                                   |
| provides method for creating RDD's accumulator and broadcasting variable<br />as well as method to start task on executors | provides method for creating dataframe and datasets<br />as well as methods for reading and writting data.      |

Data abstraction refers to the difference between how the data is stored and how it's used (or access) within the software that's consuming it.

**Two Main Abstraction of Spark:**

1. **RDD**(Low Level Abstraction):  **fault-tolerant and Immuatble collection of data elements partitioned across the cluster nodes** that can be operated on in parallel using Sparks APIs.

   **Spark Dataframe**(High Level Abstraction): A DataFrame is a dataset organized into  **named columns** . At a conceptual level, it is equivalent to a table in a relational database or to a Pandas dataframe in Python.

   **Spark Dataset**(High Level Abstraction): A Dataset is a distributed collection of data which  **combines the benefits of RDDs and the power of Spark SQL engine** .

**Difference:**

1. Both RDDs and Datasets provide an OOP-style API, while DataFrames provide a SQL-style API.
2. In RDDs, we specify to the Spark engine how to achieve a certain task, whereas with DataFrames and Datasets, we specify what to do, and the Spark Engine takes care of the rest. This is why DataFrames and Datasets inherently have optimization techniques.
3. In RDDs, only on-heap objects are used, while in DataFrames and Datasets, both on-heap and off-heap memory can be utilized. Off-heap objects are employed when there is additional data in memory.
4. Since RDDs use only on-heap objects, serialization is unavoidable because additional data needs to be transferred from RAM to disk. This is avoidable in DataFrames and Datasets due to the presence of off-heap space.
5. In RDDs, *garbage collection (GC) impacts performance, but in DataFrames and Datasets, GC impact is resolved because it constructs individual objects for each row in the dataset.

*GC - Garbage Collector: When memory is full in RDD, GC will start scanning entire memory and it will start removing the data which is old and obselete.

6) RDD and Datasets provide strong type safety that is at the time of you writing the code it'll give the error if something is wrong and thus they provide run-time compilation error. But, in the case of, DataFrames there's no type safety, so error will be known only once the code is executed and thus, they provides error at compile team.
7) RDD can process structured and unstructured data but does not infer the schema of the ingested data, where dataframe can process structured and semi-structured data allow spark to manage schema, and datasets can also process structured and unstructured data.
8) In RDD no inbuilt optimization engine is available, where as in dataframe and dataset optimization takes place using catalyst optimizer.

RDD Use cases:

* When we are working with unstructured data like media streams, texts, logs, etc
* When we want low-level transformation and actions and control on our data
* When we do not care about the schema of the data and don’t want to represent in a columnar fashion
* When we want to use functional programming constructs and domain-specific expressions
* When we can ignore some performance, optimizations and memory size

**DataFrame** Use cases:

* When we are dealing with structured and semi-structured data
* When performance and memory is the key to our application
* When we want to represent our data in tabular format and think of SQL like processing and querying

**Dataset** Use cases:

* When we want to work with semi-structured and structured data
* When we want type safety and it is quite important in our application
* When we want to catch type errors at the development stage with compile-time errors
* When we want to have a tabular view of our data with type information
* When performance and memory are of utmost importance.

Transformation: are operations on RDD/Dataframes/Dataset that produce a new distributed dataset from existing one.They are generally lazy meaning they are not executed immediately.EX: map, filter, groupby,join.

* Narrow: each partition of the input rdd contributes to only one partition of the output rdd.ex: map,filter
* Wide: each partition of the input rdd may contribute to multiple partition of the output rdd(ex: groupby,reducebykey,join)

Action: are operations that trigger the execution of transformation and return value to the driver program or write data to external storage system.ex: collect,count,first,saveAsTextFile.

Diff: If a function returns a `DataFrame`, `Dataset`, or `RDD`, it is a transformation. If it returns anything else or does not return a
 value at all (or returns Unit in the case of Scala API), it is an action.

**2. DAG:**  represents the logical execution plan for a set of stages in a Spark job.It is a combination of vertices as well as edges where vertices represents RDDs and edges represents operation to be applied on RDD.

**DAG Execution:**

1. Action Triggering: When an [action](https://medium.com/@think-data/dont-overlook-this-pyspark-foundation-f835d528ca7f) is called (e.g., `collect()`, `count()`), Spark triggers the execution. This action causes the DAG to be executed.
2. Job and Stage Creation: Spark breaks the DAG into smaller units called stages. Each stage contains tasks that can be executed in parallel.
3. Task Scheduling and Execution: Spark's scheduler assigns tasks to individual executors across the cluster. Tasks within a stage can run concurrently whenever possible.
4. Result Collection: The final results of the computation are collected back to the driver node (in the case of actions like `collect()`).

* Spark creates DAG.

- Once action is triggered on the RDD, DAG is submitted to the DAGScheduler.
- DAGScheduler looks at RDD lineage and comes up with the best execution plan by dividing it into stages of the task
- Stages set is given to TaskScheduler and TaskScheduler will launch tasks through Cluster manager.
- TaskScheduler with help of cluster manager will check the data/resources availability in different nodes to execute the tasks. It will distribute the tasks to different executors.

Components: Stages | DAG Scheduler

* Stages: set of tasks execute together in a single wave of computation.
* DAG Scheduler: High - level scheduling layer implements stage-oriented scheduling.

  Works: 1.computes the stages of each job and schdule it, 2.subimt Task set to TaskScheduler 3. convert Logical Execution Plan to Physical Execution Plan. 4. React on fault tolerance

The number of tasks for a job is = ( no of your stages * no of your partitions ) -- number of stages creation.

**Lineage Graph:** Lineage Graph is a historical record of transformations, tracing back to the original data. It represent the dependency in between rdds.

**Use:**

1. It's the basis for Spark's lazy evaluation strategy, only executing transformations when an action is invoked.
2. Allows Spark to recover lost data by re-computing it from the lineage graph.

**DAG VS Lineage Graph:**

|                | DAG                                                                           | Lineage                                                                                      |
| -------------- | ----------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| Representation | dependencies between tasks or events                                          | history of data transformations or processing steps                                          |
| Cycle          | A DAG does not contain cycles                                                 | lineage graph can contain cycles.                                                            |
| Direction      | direction of edges represent the flow``of<br />dependencies between tasks     | the direction of edges represent the flow of data<br />transformations``or processing steps. |
| Use            | used in task scheduling, workflow``management,<br />and distributed computing |                                                                                              |


What is a DAG?

DAG stands for **Directed Acyclic Graph**. In Spark, a DAG is a sequence of computations, or tasks, that are connected together in a way that forms a graph. The "directed" part means that the tasks flow in onedirection, and "acyclic" means that the graph has no cycles or loops. In simple terms, a DAG is a roadmap that Spark follows to process data.

Why is DAG Important in Spark?

When you write a Spark job, like performing transformations on a DataFrame or RDD, Spark doesn't immediately execute your code. Instead, it builds a DAG that outlines all the transformations you want to perform. Spark then uses this DAG to determine the most efficient way to execute the job.

How DAG Works in Spark


1. Stage Creation : Spark divides the DAG into smaller stages. Each stage is a set of tasks that can be executed without any dependencies on other stages. Stages are created based on the transformations you've applied, especially when there's a *shuffle* involved (like with `groupBy` or  `join` operations).
2. Task Execution : Once the stages are defined, Spark schedules tasks within each stage. Tasks are units of work that are executed on the worker nodes of the Spark cluster. Each task processes a partition of the data.

Data Flow : The DAG ensures that the data flows from one stage to the next in a controlled manner, without going back or creating loops. This
flow is crucial for maintaining efficiency and preventing errors.

Example of DAG in Spark

Let's say you have a simple Spark job where you want to:

1. Load data from a file.
2. Filter out certain rows.
3. Group the data by a specific column.
4. Calculate the sum for each group.
5. Save the result to another file.

Here’s how Spark would handle it:

Step 1: Load data : Spark starts by creating a DAG node for loading the data.
Step 2: Filter : Spark adds another node to the DAG for the filter operation.
Step 3: Group by : This operation might require a shuffle, so Spark adds a new stage in the DAG.
Step 4: Sum : The sum calculation happens after the shuffle, so it’s part of the same stage as the group by.
Step 5: Save: Finally, Spark adds a node to the DAG for saving the result.


Lazy Evoluation: In spark it's a powerful concept that allows the optimization of data processing tasks by postponing the execution of transformations until an action is called.

work: When we apply a transformations, spark records it but doesn't executes it immediately, meaning it builds dag of transformations and the execution occurs only when an action is triggered.

Benefits:

1. Optimization: Spark can optimize the entire computation plan by evaluating only the required transformations, skipping unnecessary work.
2. Fault tolerance: Lazy evaluation allows Spark to recompute only the lost or incomplete data, ensuring fault tolerance.
3. Performance: It enables pipelining of tasks, reducing the need to write intermediate results to disk.

What if Mapreduce has lazy evoluation: 1. On-demand processing 2. Resource Optimization 3.Pipeline Fusion 4. Reducing Redundant computations

What if spark does not have lazy evoluation: Without lazy evaluation, Spark would need to execute transformations immediately, leading to unnecessary computations and increased memory usage. This could result in performance degradation, especially for complex data processing tasks involving multiple transformations.

Advantagaes: 1. Optimization 2. **Reduced Disk I/O and Memory Usage** 3. **Integration with External Systems**

**Spark handle fault tolerance:**

1. RDDs:  When node fails, spark can reconstruct lost RDD partitions using lineage information, which represents the sequence of transformations applied to create the RDD. The lineage allow spark to recompute the lost data without needing to store the entire dataset.
2. Lineage and Transformations: spark maintains a DAG of transformations applied to RDD if a node fails, Spark can recompute only the lost partitions by tracing back the lineage graph this minimize the amount of data that needs to be recalculated.
3. Data Replication: By default, data is replicated at least once across different nodes. This replication ensures that there are redundant copies of data available, reducing the risk of data loss due to node failures.
4. Checkpointing:  Checkpointing is a mechanism that allows you to save the state of an RDD to a reliable distributed file system like HDFS. This helps in faster recovery in case of failures since Spark can use the checkpointed data instead of recomputing the entire lineage.
5. Task Re-execution: When a worker node fails, Spark can reschedule the failed tasks on other available nodes. The data needed for those tasks is recomputed using the lineage information.
6. Persistent Storage: Intermediate data generated during transformations can be stored in memory or on disk. This allows Spark to use persisted data in case of node failures instead of recomputing it.
7. Driver Recovery: If the driver node fails, the driver's state can be recovered by restarting the application and re-executing the driver code.
8. Dynamic Resource Allocation: Spark supports dynamic allocation of cluster resources. This means that if a node fails, its resources can be reclaimed and reallocated to other tasks, ensuring efficient resource utilization.

Catalyst optimizer: It is a robust query optimization framework, It's main goal is to reduce the time of query execution, enabling spark to analyze, organize and execute jobs more efficiently.

Four Primary Phase:

1. Parsing: In this phase it converts df into an abstract syntax tree(AST) which represents the structure of the query in a way that is easier for computer to understand.
2. Analysis: Next, it verifies the AST for semantic correctness. It resolves attributes by looking at catalog information and also resolves functions. The output of this phase is a "resolved logical plan".
3. Logical Optimization: Here it applies a series of rule based optimization to resolved logical plan. Techniques include predicate pushdown, projection pushdown and boolean simplifications.
4. Physical Planning: Logical is now converted into one or more physical plan. Then it selects the most optimal physical plan using code-based optimization where the cost of each plan is estimated based on the sizes of its inputs.
5. Code Generation: Finally generates JVM bytecodes to run the selected physical plan.

**Logical Plan:** Logical plan is a high-level description of what needs to be done, but not how to do it. It has relational operators (Filter / Join) with respective expressions (column transformations, filter / join conditions)

**Physical Plan:** •The physical plan represents the actual execution steps that Spark will perform to execute the job on the cluster. •It is derived from the logical plan and takes into account the characteristics of the input data, available resources, and optimization strategies. •The physical plan specifies how the data will be read, processed, and transformed across the distributed Spark cluster. •It includes details such as data partitioning, shuffle operations, join strategies, and optimization techniques. •The physical plan is optimized for performance and resource utilization based on Spark's Catalyst optimizer and execution engine.

Optimization Techniques:

1. Predicate Pushdown: data need to filter out in source level before entering in the Processing pipeline, it push filter condition as close  to the data sources as possible.
2. Column Purining / projection Pushdown: It reads only necessary columns and load it.
3. Broadcast Join: In this small tables copy send to every worker nodes during join with large tables.
4. Join ReOrdering: It re-orders the join's condition to minize the data Shuffle through that it enhance the parallelism and reduce overall execution time.
5. Constant Folding: During query Analysis it evaluates Constant expressions through that reducing the computational overhead.

What are the different types of Cluster manager available in Spark:

**Apache YARN** — YARN is the cluster manager for Hadoop. As of date, YARN is the most widely used cluster manager for Apache Spark.

**Apache Mesos** — Apache Mesos is another general-purpose cluster manager. If you are not using Hadoop, you might be using Mesos for your Spark cluster.

 **Kubernetes** — it's a general purpose container orchestration platform from Google.

 **Standalone** — Finally, the standalone. The Standalone is a simple and basic cluster manager that comes with Apache Spark and makes it easy to set up a Spark cluster very quickly. This is basically used during development.

**Deployment Mode:**

1. Local Mode: Execution not done in distributed manner, means single JVM process is used to produce both driver and executor.
2. Client Mode: Driver is present in Client machine, means driver is not the part of cluster and on the other side executors run within the cluster.
3. Cluster Mode: Driver and executor both run inside the cluster. Spark job submitted from local to cluster machine.

Client mode Vs Cluster mode:

| Client                                                                | Cluster                                                                               |
| --------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| Logs are generated on client machine.It is easy to debug.             | Logs are generated in std out or std err file. It is suitable for production-workload |
| Network latency is high                                               | Network latency is low                                                                |
| Driver OOM can be there                                               | Driver can go into oom but chances are less.                                          |
| Driver goes away once the edge node server is disconnected or closed. | Even if edge server closed process stil                                               |

---

PySpark is the Python API to Apache Spark, meaning that we can write Python code that calls Spark automatically.

Features:

* **Python API** : enabling Python developers to leverage Spark’s distributed computing capabilities.
* **Distributed Computing** : PySpark utilizes Spark’s distributed computing framework to process large-scale data across a cluster of machines, enabling parallel execution of tasks.
* **Fault Tolerance** :
* **Lazy Evaluation** :
* **Machine Learning** :
* **Streaming Processing** :
* **SQL Support** :

Advantages:

* **Scalability**
* **Performance**
* **Ease of Use**
* **Fault Tolerance**
* **Unified Platform**
* **Real-time Processing**
* **Machine Learning Capabilities**

**PySpark Modules & Packages:**

* RDD (pyspark.RDD)
* DataFrame and SQL (pyspark.sql)
* Streaming (pyspark.streaming)
* MLib (pyspark.ml, pyspark.mllib)
* GraphFrames (GraphFrames)
* Resource (pyspark.resource) It’s new in PySpark 3.0

**Spark Web UI:** The Spark Web UI is a user interface provided to monitor and debug Spark applications. It displays information about job progress, task execution, resource utilization, and system metrics, allowing users to optimize performance, diagnose issues, and gain insights into their Spark jobs.

**Access Spark History Server:** The Spark History Server stores information about completed Spark applications [(spark-submit](https://sparkbyexamples.com/spark/spark-submit-command/), spark-shell), including logs, metrics, and event timelines. It allows users to view detailed information about past job executions, such as tasks, stages, and configurations, through a web-based user interface.

how to read file in pyspark:

```python
spark.read.format('csv') \
	  .option('header','true') \
          .option('inferSchema','false') \
	  .option('skipRows',1) \
	  .schema(my_schema ) \
          .option('mode','FAILFAST') \
          .load('c:\user\download\data.csv')
```

Read Json File:

```python
df = spark.read.format("json") \
    .option("multiLine", "true") \
    .option("mode", "PERMISSIVE") \
    .option("columnNameOfCorruptRecord", "_corrupt_record") \
    .load("/path/to/your/jsonfile.json")
```

mode:

* **FAILFAST**- fail execution if malformed record in dataset
* **DROPMALFORMED**- drop the corrupted record
* PERMISSIVE (Default) - set null value to all corrupted fields

How to write data to disk:

```python
df.write.format("csv") \ 
	.option("header","true") \
	.option("mode","overwrite") \
        .partitionBy("column_name","column_name") \ 
	.option("path", "/Filestore/tables/csv_write") \
	.save()
```

write data with partition:

```python
df.repartition(3).write.format("csv") \ 
	.option("header","true") \
	.option("mode","overwrite") \
	.option("path", "/Filestore/tables/csv_write") \
	.save()  ## it will store data in 3 files

```

Modes in Dataframe writer API:

* Append - This mode appends the data to the file, preserving any existing data in the file. If the file does not exist, it will be created.
* Overwrite - This mode overwrites any existing data in the file. If the file does not exist, it will be created.
* errorIfExists - This mode raises an error if the file already exists.
* ignore - This mode writes the data to the file only if the file does not already exist. If the file already exists, the write operation is ignored.

Using PySpark to read PostgreSQL DB remotely:

To query a database table using jdbc() method, you would need the following.

* Server IP or Host name and Port,
* Database name,
* Table name,
* User and Password.

JDBC (Java Database Connectivity) is an API (Application Programming Interface) that enables Java applications to interact with databases. It provides a standard way for Java applications to connect to various types of databases (such as MySQL, Oracle, PostgreSQL, SQL Server, etc.)

* Initialize Spark Session

```python
spark = SparkSession\
    .builder\
    .appName("Connecting to JDBC")\
    .config("spark.driver.extraClassPath", "/path/to/postgresql-<version>.jar")\
    .getOrCreate()
```

* Define JDBC connection properties

```python
driver = "org.postgresql.Driver"
url = "jdbc:postgresql://<ip_address>:5432/<name_of_db>:emp"
user = "my_unique_user_name"
password = "my_unique_password"
```

* read data

```python
spark.read\
    .format("jdbc")\
    .option("driver", driver)\
    .option("query", "select id,age from employee where gender='M'") \ # to query specific columns 
    .option("url", url)\
    .option("user", user)\
    .option("password", password)\
    .option("dbtable", "table_name")\
    .load()
```

* write data

```python
url = "jdbc:postgresql://<ip_address>:5432/<name_of_db>:emp"
properties = {
    "user": "<username>",
    "password": "<password>",
    "driver": "org.postgresql.Driver"
}
table_name = "<table_name>"
mode = "overwrite"
df.write.jdbc(url=url, table=table_name, mode=mode, properties=properties)
```

**create SparkSession:** sparkSession class from the pyspark.sql liabrary has the getOrCreate() method which creates new sparkSession.

```python-
import pyspark
from pyspark.sql import SparkSession
spark = SparkSession.builder.master("local[1]") 
                   .appName('InterviewBitSparkSession') 
                   .getOrCreate()
```

builder -> The `builder` method initializes a `SparkSession.Builder` object, which provides methods for configuring the SparkSession, such as setting the master URL, application name, configuration options, and more. It provides methods : 1.master(), 2. appName(), 3. config(), 4.enableHiveSupport() 5. getOrCreate(), 6. newSession().

master() -> setting up the mode where application run clustermode/standalone mode for standalone mode we use local[x] value where x represents partition count to be created in RDD,dataframe,dataset.ideally x is CPU numbers of cores available.

appName() -> setting the application name

getOrCreate() -> returning sparkSession object. creates new one if it does not exists

for creating new sparkSession every time we use spark_session = SparkSession.newSession

---

Dataframe Transformation:

schema = column Name + Column Data type

Dataframe = column + rows

Operations:

* **Viewing DataFrames**
  * `show() - Displays the top rows of the DataFrame.`
  * `printSchema() - Prints the schema of the DataFrame, including column names and data types.`
  * `head() - Returns the first row as a Row object.`
  * `columns - Returns a list of column names.`
  * `dtypes - Returns a list of tuples with column names and their data types.`
  * `describe() - Computes basic statistics like count, mean, stddev, min, and max for numeric columns.`

### 2. **Data Manipulation**

* **Selecting Data**
  * `select() - Selects one or more columns from the DataFrame.`
  * `selectExpr() - Selects using SQL expressions.`
  * `withColumn() - Adds a new column or replaces an existing column.`
  * `drop() - Removes one or more columns from the DataFrame. `
  * `filter()` / `where() - Filters rows based on a condition.`
  * `distinct() - Removes duplicate rows from the DataFrame.`
* **Grouping and Aggregating**
  * `groupBy() - Groups rows by one or more columns.`
  * `agg() - Applies aggregate functions on grouped data.`
  * `count() - Counts the number of rows in each group.is action as well as transformation.`
  * `sum() - Computes the sum for each group. `
  * `avg() - Computes the average for each group.`
  * `max() - Finds the maximum value in each group.`
  * `min() - Finds the minimum value in each group.`
* **Sorting and Ordering**
  * `orderBy() - Sorts the DataFrame by one or more columns.`
  * `sort() - An alias for orderBy().`
* **Joins**
  * `join() - oins two DataFrames on a specified column(s).`
* **Handling Missing Data**
  * `na.drop() - Drops rows with missing data.`
  * `na.fill() - Fills missing data with specified values.`
  * `na.replace() - Replaces specified values in a DataFrame.`
* **Modifying Columns**
  * `withColumnRenamed() - Renames a column.`
  * `alias() - Assigns a temporary name to a column, often used in SQL expressions.`

### 3. **Window Functions**

* **Window Specifications**
  * `Window.partitionBy() - Partitions data into groups for window functions.`
  * `Window.orderBy() - Orders data within each partition.`
  * `Window.rowsBetween() - Defines the range of rows for each window.`
  * `Window.rangeBetween() - Defines the range of values for each window.`
* **Window Functions**
  * `row_number() - Assigns a unique row number to each row within a window partition.`
  * `rank() - Assigns a rank to each row within a partition, with gaps.`
  * `dense_rank() - Assigns a rank without gaps.`
  * `lag() - Accesses data from a previous row within the window.`
  * `lead() - Accesses data from a subsequent row within the window.`
  * `cumsum() - Computes the cumulative sum.`
  * `ntile() - Divides rows into n buckets based on rank.`

### 4. **SQL Functions**

* **Basic SQL Functions**
  * `lit() - Creates a Column object for a literal value.`
  * `col() - Returns a Column object for a DataFrame column.`
  * `asc() - Sorts the data in ascending order.`
  * `desc() - Sorts the data in descending order.`
  * `expr() - Parses the expression string into a column.`
* **String Functions**
  * `concat() - Concatenates multiple string columns.`
  * `substr() - Extracts a substring from a string column.`
  * `lower() - Converts strings to lowercase.`
  * `upper() - Converts strings to uppercase.`
  * `trim() - Removes leading and trailing spaces from strings.`
  * `split() - Splits strings around a specified separator.`
* **Date and Time Functions**
  * `current_date() - Returns the current date.`
  * `current_timestamp() - Returns the current timestamp.`
  * `date_format() - Formats date into a specified pattern.`
  * `datediff() - Computes the difference in days between two dates.`
  * `add_months() - Adds a specified number of months to a date.`
  * `year()`, `month()`, `dayofmonth() - Extracts the year, month, or day from a date.`
* **Mathematical Functions**
  * `abs() - Computes the absolute value.`
  * `round() - Rounds a number to a specified number of decimal places.`
  * `sqrt() - Computes the square root.`
  * `sin()`, `cos()`, `tan() - Trigonometric functions for sine, cosine, and tangent.`

### 5. **Aggregations and Statistics**

* **Aggregation Functions**
  * `count() - Counts the number of rows.`
  * `sum() - Sums values in a column.`
  * `avg() - Calculates the average of a column.`
  * `max() - Finds the maximum value in a column.`
  * `min() - Finds the minimum value in a column.`
* **Statistical Functions**
  * `corr() - Calculates the correlation between two columns.`
  * `cov() - Calculates the covariance between two columns.`
  * `approxQuantile() - Calculates approximate quantiles.`
  * `describe() - Provides summary statistics for columns.`

### 6. **User-Defined Functions (UDFs)**

* **Creating UDFs**
  * `udf() - Creates a user-defined function (UDF) for use in DataFrames.`
* **Using UDFs**
  * `withColumn() - Applies a UDF to create or modify columns.`
  * `select() - Applies a UDF in a select statement.`

### 7. **DataFrames Actions**

* **Actions**

  * `collect() - Returns all rows as a list of Row objects.`
  * `count() - Returns the number of rows in the DataFrame.`
  * `take() - Returns the first n rows as a list.`
  * `first() - Returns the first row as a Row object.`
  * `foreach() - Applies a function to each row.`
  * `foreachPartition() - Applies a function to each partition.`

### **RDD Functions**

1. **Basic RDD Operations**
   * `getNumPartitions()`: Returns the number of partitions in the RDD.
   * `collect()`: Returns all the elements of the RDD as an array.
   * `count()`: Returns the number of elements in the RDD.
   * `first()`: Returns the first element of the RDD.
   * `take(n)`: Returns the first n elements of the RDD.
   * `top(n)`: Returns the top n elements in the RDD.
   * `takeSample(withReplacement, num, [seed])`: Returns a sample of num elements from the RDD.
   * `reduce(func)`: Aggregates the elements of the RDD using the given function.
   * `foreach(func)`: Applies the function to each element of the RDD.
2. **RDD Transformations**
   * `map(func)`: Returns a new RDD by applying a function to each element.
   * `flatMap(func)`: Similar to `map`, but each input item can be mapped to 0 or more output items (flattening the results).
   * `filter(func)`: Returns a new RDD containing only the elements that satisfy a condition.
   * `distinct()`: Returns a new RDD containing distinct elements.
   * `union(otherRDD)`: Returns the union of this RDD and another RDD.
   * `intersection(otherRDD)`: Returns the intersection of this RDD and another RDD.
   * `join(otherRDD)`: Joins two RDDs by their keys.
   * `groupByKey()`: Groups the values for each key in the RDD.
   * `reduceByKey(func)`: Merges the values for each key using an associative function.
   * `sortByKey(ascending=True)`: Returns an RDD sorted by the key.
3. **Persistence**
   * `cache()`: Caches the RDD in memory.
   * `persist()`: Persist the RDD with a specified storage level.
   * `unpersist()`: Removes the RDD from memory.
4. **Partitioning**
   * `repartition(numPartitions)`: Reshuffles the data into the specified number of partitions.
   * `coalesce(numPartitions)`: Reduces the number of partitions in the RDD, useful for optimization.

JOIN:

Types of joins:

* Inner join
* full outer join
* Left join
* Right join
* Left semi join
* Left anti join
* Cross join

union VS unionAll

**If we are using union or unionAll in df then both will provide same output.

** but in spark sql union will give only distinct records while unionAll will give all records including duplicates.

**unionByName - it will check both dataframes column name if they are same then only it gives result.

---

Shared Variables: There are two different types of Shared Variables in spark -Broadcast Variable and Accumulator

1. Broadcast Variables: are read-only Variables distributed across worker nodes in-memory. The data Broadcasted this way is cached in serialized form and deserialized before running each task. Used for cache a value in memory on all nodes generally small datasets only Broadcasted.
2. Accumulator: Which are used to update the variables in parallel during execution/runtime and share results from worker to driver.similar to counters in Mapreduce. used for aggregating information across all tasks in a Spark job.

coalesce and repartition:

coalesce: is used to decrease the number of partitions without invoking Shuffling. It used in when output partitions is less than the input.

repartition: helps to increase or decrease the number of partitions by doing Shuffling of data.

difference between Persist and Cache: are optimization techniques for both iterative and interactive Spark applications to improve the performance of the jobs or applications.

iterative -> Reuse intermediate results

interactive  -> allowing a two-way flow of information

cache() -> MEMORY_ONLY

Persist(level) -> MEMORY_ONLY, MEMORY_AND_DISK, MEMORY_ONLY_SER, MEMORY_AND_DISK_SER, DISK_ONLY (disk, or off-heap memory)

unpersist() can be used to Freeing up space from the Storage memory.

Checkpoint: used for fault-tolerance and to cut down the lineage of RDDs/dataframes especially in long and complex computations. It breaks the lineage and stores data to a reliable Storage(HDFS), used in scenario where lineage graph is too long or when you want to recover from failures efficiently.

Note: use cache() -> for optimization purpose Checkpoint() -> for fault tolerance purpose, and reduce the lineage length in complex computations.

Bucketing and Partitioning in Spark:

Partitioning: Partitioning splits data into separate folders on disk based on one or more multiple columns.This enables efficient parallelism and partition pruning, which optimizes queries by skipping unnecessary data.

syntax: df.write.partitionBy("date").format("parquet").save("path")

Note: The number of resulting files is controlled by the spark.sql.shuffle.partitions setting

Bucketing: bucketing assigns rows to specific buckets and collects them on disk, which is useful for wide operations like joins and agg.Bucketing reduces the need for shuffling data across partitions.

Syntax:

df.write.bucketBy(10,"id").sortBy("id").format("parquet").save("path") #bucket the dataset by the "id" column into 10 buckets

No of bucket = Total dataset size/default block size

default block size = 128 mb

Total data size  = total no. of records * variable * datatype

variable = no of columns

When to use Partitioning and Bucketing:

* Partitioning: use partitioning when you frequently filters on a column with low cardinality. This helps in skipping unnecessary data and speeds up query performance. Ex: partitioning data by date is common when you need to analyze daily logs.
* Bucketing: Use bucketing for complex operations like joins, groupBy and windowing on columns with high cardinality. Bucketing helps in reducing shuffling and sorting costs.
* Partitioning is more about pruning data for faster reads, while bucketing is more about optimizing joins and reducing data shuffle.
