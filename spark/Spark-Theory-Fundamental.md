**Spark:**  spark is an open-source unified analytics engine for large scale data processing.

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

**Features:**

* Speed → Due to in-memory processing
* Caching → Spark has a caching layer to cache the data which makes the processing even faster
* Deployment → Can be deployed in a Hadoop cluster or its own Spark cluster
* Polyglot → Code can be written in Python, Java, Scala and R
* Real-time → It was developed to support ‘real-time’ use cases.

**Spark Architecture:**

1. Programming Layer (Java, Scala, R, Python)
2. Liabrary Layer - (MLlib, SparkSQL, Graphx, Streaming)
3. Spark core engine - (Apache Spark)
4. Spark Management or cluseter layer - (Kubernetes, Apache Hadoop YARN, Mesos, Apache Spark)
5. Storage layer - (Local FS, s3, blob storage, HDFS)

* Engine — Spark Core: It is the basic core component of Spark ecosystem on top of which the entire ecosystem is built. It performs the tasks of scheduling/monitoring and basic IO functionality
* Management — Spark cluster can be managed by Hadoop YARN, Mesos or Spark cluster manager.
* Library — Spark ecosystem comprises of Spark SQL (for running SQL like queries on RDD or data from external sources), Spark Mlib (for ML),Spark Graph X (for constructing graphs for better visualisation of data), Spark streaming (for batch processing and streaming of data in the same application)
* Programming can be done in Python, Java, Scala and R
* Storage — Data can be stored in HDFS, S3, local storage and it supports both SQL and NoSQL databases.

---

**Spark Execution Model:**

1. **Driver** - brain of spark framework
2. **Executor** - worker node responsible for executing the given task.

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

**Spark Programming Model:**

1. **Job** - in spark refers to a sequence of transformations on data.whenever an action like count(), first() and save is called on RDD  a job is created.collect(), saveAsTextFile(), or count()
2. **Stage** - A stage represents a set of tasks that can be executed in parallel. There are two types of stages in Spark: shuffle stages and non-shuffle stages. Shuffle stages involve the exchange of data between nodes, while non-shuffle stages do not.(groupByKey, sortByKey).
3. **Task** - in spark is the samallest unit of work that can be scheduled. Each stage is divided into task.A task is a unit of execution that runs on a single machine.

---

**Spark Internally Working:**

1. **Job Submission:** The user submits a Spark application using the SparkContext/session in the driver program.
2. **DAG Construction:** The driver builds a logical Directed Acyclic Graph (DAG) of stages representing transformations and actions.
3. **Task Scheduling:** The DAG is divided into smaller sets of tasks, which are then submitted to the cluster manager.
4. **Task Execution:** The cluster manager allocates resources and schedules the tasks on available executors.

- Executors perform the tasks assigned to them, which may involve reading data from a data source, performing computations, and storing
  intermediate results.

5. **Result Collection:**

- Executors send the results of their computations back to the driver.
- The driver program consolidates these results and performs any final actions required.


1.  User submits a Spark application.

2. Driver process starts and sets up the SparkContext.
3. The SparkContext connects to the cluster manager to negotiate resources.
4. The cluster manager launches executors on worker nodes.
5. Executors register with the driver.
6. Driver creates a logical plan (DAG) and converts it into a physical plan (tasks).
7. Tasks are sent to executors by the driver.
8. Executors execute tasks, process data, and store intermediate results.
9. Executors return results to the driver.
10. Driver compiles the results and completes the job.

---

SparkContext: was the primary entry point for interacting with spark, represent the connection to the spark cluster and was responsible for co-ordinating task execution.

SparkSession: spark2.0 introduced as unified entry point that encapsulates sparkcontext while offering much more.Provides user-friendly API for working with structured data in the form of dataframes and datasets.

| SparkContext                                                                                                               | SparkSession                                                                                                    |
| -------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| preferred way to work with the lower-level API like RDD,<br />Accumulator and broadcast variable                           | prefered way when to work with data structure like<br />dataframe and datasets as it provides simpler interface |
| can be created only once in spark application at any time                                                                  | can be created multiple times                                                                                   |
| provides method for creating RDD's accumulator and broadcasting variable<br />as well as method to start task on executors | provides method for creating dataframe and datasets<br />as well as methods for reading and writting data.      |

---

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
5. In RDDs, *garbage collection (GC) impacts performance, but in DataFrames and Datasets, GC impact is resolved.

*GC - Garbage Collector: When memory is full in RDD, GC will start scanning entire memory and it will start removing the data which is old and obselete.

6) RDD and Datasets provide strong type safety that is at the time of you writing the code it'll give the error if something is wrong and thus they provide run-time compilation error. But, in the case of, DataFrames there's no type safety, so error will be known only once the code is executed and thus, they provides error at compile team.

Use Cases of RDD:

* Handling unstructured data or requiring low-level transformations and actions in a distributed computing environment.
* When fine-grained transformations and actions are needed for a distributed computing environment.
* For performance optimization and fine-tuning in scenarios where the schema is not defined in a distributed computing environment.

Use DataFrames:

Use DataFrames when dealing with structured data, similar to an SQL table, to improve performance through optimized execution plans and built-in optimizations.

Use Datasets:

* Grouping data: Utilize Datasets when you need strong typing for a group of data and when you want to benefit from the features like grouping, aggregation, and windowing functions.
* Language support: Datasets are the go-to choice when language-specific encoders for objects are required, ensuring type safety at compile time.
* **Schema support** : Datasets should be used when a structured and typed API with the benefits of Spark SQLs optimized execution engine is necessary.

---

Transformation: are operations on RDD/Dataframes/Dataset that produce a new distributed dataset from existing one.They are generally lazy meaning they are not executed immediately.EX: map, filter, groupby,join.

* Narrow: each partition of the input rdd contributes to only one partition of the output rdd.ex: map,filter
* Wide: each partition of the input rdd may contribute to multiple partition of the output rdd(ex: groupby,reducebykey,join)

Action: are operations that trigger the execution of transformation and return value to the driver program or write data to external storage system.ex: collect,count,first,saveAsTextFile.

| Features     | Transformation                             | Action                                                |
| ------------ | ------------------------------------------ | ----------------------------------------------------- |
| output       | New Dataset(RDD or Dataframe)              | value, side effect(e.g writting data)                 |
| execution    | Lazy only planned                          | Triggered by an action, immediate computation         |
| Optimization | spark optimized the overall execution plan | spark optimized the overall execution plan            |
| Use case     | Defining data manipulation pipeline        | Retrieving results, interacting with external systems |

---

**2. DAG:**  represents the logical execution plan for a set of stages in a Spark job.It is a combination of vertices as well as edges where vertices represents RDDs and edges represents operation to be applied on RDD.

**DAG Execution:**

1. Action Triggering: When an [action](https://medium.com/@think-data/dont-overlook-this-pyspark-foundation-f835d528ca7f) is called (e.g., `collect()`, `count()`), Spark triggers the execution. This action causes the DAG to be executed.
2. Job and Stage Creation: Spark breaks the DAG into smaller units called stages. Each stage contains tasks that can be executed in parallel.
3. Task Scheduling and Execution: Spark's scheduler assigns tasks to individual executors across the cluster. Tasks within a stage can run concurrently whenever possible.
4. Result Collection: The final results of the computation are collected back to the driver node (in the case of actions like `collect()`).

Components: Stages | DAG Scheduler

* Stages: set of tasks execute together in a single wave of computation.
* DAG Scheduler: High - level scheduling layer implements stage-oriented scheduling.

  Works: 1.computes the stages of each job and schdule it, 2.subimt Task set to TaskScheduler 3. convert Logical Execution Plan to Physical Execution Plan. 4. React on fault tolerance

---

**Lineage Graph:** Lineage Graph is a historical record of transformations, tracing back to the original data. It represent the dependency in between rdds.

**Use:**

1. It's the basis for Spark's lazy evaluation strategy, only executing transformations when an action is invoked.
2. Allows Spark to recover lost data by re-computing it from the lineage graph.

**DAG VS Lineage Graph:**

|                | DAG                                                                      | Lineage                                                                                 |
| -------------- | ------------------------------------------------------------------------ | --------------------------------------------------------------------------------------- |
| Representation | dependencies between tasks or events                                     | history of data transformations or processing steps                                     |
| Cycle          | A DAG does not contain cycles                                            | lineage graph can contain cycles.                                                       |
| Direction      | direction of edges represent the flow``of dependencies between tasks     | the direction of edges represent the flow of data transformations``or processing steps. |
| Use            | used in task scheduling, workflow``management, and distributed computing | used in data lineage and data quality analysis.                                         |

Note: Because dag represent dependencies between task thatmust be executed in particular order while lineage Represent history of data transformations that may be repeated or looped over.

---

Lazy Evoluation: In spark it's a powerful concept that allows the optimization of data processing tasks by postponing the execution of transformations until an action is called.

work: When we apply a transformations, spark records it but doesn't executes it immediately, meaning it builds dag of transformations and the execution occurs only when an action is triggered.

Benefits:

1. Optimization: Spark can optimize the entire computation plan by evaluating only the required transformations, skipping unnecessary work.
2. Fault tolerance: Lazy evaluation allows Spark to recompute only the lost or incomplete data, ensuring fault tolerance.
3. Performance: It enables pipelining of tasks, reducing the need to write intermediate results to disk.

What if Mapreduce has lazy evoluation: 1. On-demand processing 2. Resource Optimization 3.Pipeline Fusion 4. Reducing Redundant computations

What if spark does not have lazy evoluation: Without lazy evaluation, Spark would need to execute transformations immediately, leading to unnecessary computations and increased memory usage. This could result in performance degradation, especially for complex data processing tasks involving multiple transformations.

Advantagaes: 1. Optimization 2. **Reduced Disk I/O and Memory Usage** 3. **Integration with External Systems**

---

Catalyst Optimizer: It is a robust query optimization framework, responsible for transforming and optimizing Logical and Physical query plans.

How It Works:

1. Parsing -> parsing the dataframe to create an Abstract Syntax Tree(AST) represent logical structure of query
2. Analysis -> Semantic Analysis perform on AST structure resolve/check for query is valid or not.
3. Logical Optimization -> apply set of logical optimization, it simply rewrite the query operation without changing overall result.
4. Logical Plan -> Then it produce logical plan, it is like tree like representation of queries operations.It captures high level opearations like join, aggregation etc.
5. Physical Plan -> based on logical plan it generates many alternative physical plans and explore different execution strategies.
6. Cost-based Optimization -> It checks each physical factors like distribution, network latency, disk I/o, CPU usage and memory consumption then seletct one physical plan which cost is lowest estimated.
7. Code-Generation -> After that it generates efficient JAVA byte code or optimizes sql code for executing the query.
8. Execution: Finally spark SQL executes the optimized physical plan to get the desired result.

Optimization Techniques:

1. Predicate Pushdown: data need to filter out in source level before entering in the Processing pipeline, it push filter condition as close  to the data sources as possible.
2. Column Purining / projection Pushdown: It reads only necessary columns and load it.
3. Broadcast Join: In this small tables copy send to every worker nodes during join with large tables.
4. Join ReOrdering: It re-orders the join's condition to minize the data Shuffle through that it enhance the parallelism and reduce overall execution time.
5. Constant Folding: During query Analysis it evaluates Constant expressions through that reducing the computational overhead.

---

**Deployment Mode:**

1. Local Mode: Execution not done in distributed manner, means single JVM process is used to produce both driver and executor.
2. Client Mode: Driver is present in Client machine, means driver is not the part of cluster and on the other side executors run within the cluster.
3. Cluster Mode: Driver and executor both run inside the cluster. Spark job submitted from local to cluster machine.

---

Shared Variables: There are two different types of Shared Variables in spark -Broadcast Variable and Accumulator

1. Broadcast Variables: are read-only Variables distributed across worker nodes in-memory. The data Broadcasted this way is cached in serialized form and deserialized before running each task. Used for cache a value in memory on all nodes generally small datasets only Broadcasted.
2. Accumulator: Which are used to update the variables in parallel during execution/runtime and share results from worker to driver.similar to counters in Mapreduce. used for performing associative and commutative operations such as counters or sums.

---

coalesce and repartition:

coalesce: is used to decrease the number of partitions without invoking Shuffling. It used in when output partitions is less than the input.

repartition: helps to increase or decrease the number of partitions by doing Shuffling of data.

---

difference between Persist and Cache: are optimization techniques for both iterative and interactive Spark applications to improve the performance of the jobs or applications.

iterative -> Reuse intermediate results

interactive  -> allowing a two-way flow of information

cache() -> MEMORY_ONLY

Persist(level) -> MEMORY_ONLY, MEMORY_AND_DISK, MEMORY_ONLY_SER, MEMORY_AND_DISK_SER, DISK_ONLY (disk, or off-heap memory)

unpersist() can be used to Freeing up space from the Storage memory.

Checkpoint: used for fault-tolerance and to cut down the lineage of RDDs/dataframes especially in long and complex computations. It breaks the lineage and stores data to a reliable Storage(HDFS), used in scenario where lineage graph is too long or when you want to recover from failures efficiently.

Note: use cache() -> for optimization purpose Checkpoint() -> for fault tolerance purpose, and reduce the lineage length in complex computations.

---

**Spark handle fault tolerance:**

1. RDDs:  When node fails, spark can reconstruct lost RDD partitions using lineage information, which represents the sequence of transformations applied to create the RDD. The lineage allow spark to recompute the lost data without needing to store the entire dataset.
2. Lineage and Transformations: spark maintains a DAG of transformations applied to RDD if a node fails, Spark can recompute only the lost partitions by tracing back the lineage graph this minimize the amount of data that needs to be recalculated.
3. Data Replication: By default, data is replicated at least once across different nodes. This replication ensures that there are redundant copies of data available, reducing the risk of data loss due to node failures.
4. Checkpointing:  Checkpointing is a mechanism that allows you to save the state of an RDD to a reliable distributed file system like HDFS. This helps in faster recovery in case of failures since Spark can use the checkpointed data instead of recomputing the entire lineage.
5. Task Re-execution: When a worker node fails, Spark can reschedule the failed tasks on other available nodes. The data needed for those tasks is recomputed using the lineage information.
6. Persistent Storage: Intermediate data generated during transformations can be stored in memory or on disk. This allows Spark to use persisted data in case of node failures instead of recomputing it.
7. Driver Recovery: If the driver node fails, the driver's state can be recovered by restarting the application and re-executing the driver code.
8. Dynamic Resource Allocation: Spark supports dynamic allocation of cluster resources. This means that if a node fails, its resources can be reclaimed and reallocated to other tasks, ensuring efficient resource utilization.

---

**Optimizing**

* Data Partitioning: Partitioning divides data into smaller, manageable chunks.

```python
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName("OptimizationExample").getOrCreate()
df = spark.read.csv("large_dataset.csv", header=True, inferSchema=True)
# Repartition data
df = df.repartition(100) # Repartition into 100 partitions
# Coalesce data
df = df.coalesce(50) # Coalesce into 50 partitions
```

* Caching and Persistence: Caching frequently accessed data in memory reduces the need for repeated computations.

```python
# Cache data
df.cache()
# Persist data with different storage levels
df.persist(StorageLevel.MEMORY_AND_DISK)
```

* Broadcast Variables: Broadcast variables distribute read-only data across all worker nodes, minimizing data transfer overhead. This technique is useful for joining a large dataset with a small one.

```python
# Create a small DataFrame to broadcast
small_df = spark.read.csv("small_dataset.csv", header=True, inferSchema=True)
broadcast_small_df = spark.sparkContext.broadcast(small_df.collect())
# Use broadcast variable in a join
large_df = spark.read.csv("large_dataset.csv", header=True, inferSchema=True)
joined_df = large_df.join(small_df, "key_column")
```

* Efficient Joins: Joins can be resource-intensive, especially with skewed data. Optimize joins by using broadcast joins for small datasets, or by using bucketing and sorting techniques to reduce shuffling.

  ```python
  # Broadcast join
  broadcasted_small_df = broadcast(small_df)
  joined_df = large_df.join(broadcasted_small_df, "key_column")
  # Bucketing and sorting
  large_df.write.bucketBy(10, "key_column").sortBy("key_column").saveAsTable("bucketed_table")
  bucketed_df = spark.table("bucketed_table")
  ```
* Optimized File Formats: Choosing the right file format can drastically impact performance. Parquet and ORC are columnar storage formats that offer efficient compression and faster read/write operations compared to plain text formats like CSV or JSON.

---



Data Skewness: In scenario where some of the partitioned data has more data compared to others.

How it Occurs:

1. When data get re-partitioned
2. Join/Group by operations

Disadvantages:

1. Impact on job performance
2. Execution time increase then usual time
3. Spark job resources not used in its full potential
4. most resources become idle without doing any tasks
5. distributed Processing got affected.
6. Out of memory errors

Fix Data Skewness:

1. Broadcast Join: Instead of sort-merge join we use Broadcast join because 1. Shuffle 2. Sort 3. merge. Use a broadcast join for smaller datasets to avoid shuffling large datasets.
2. Bucketing: In this, we group/bucket specific attributes of values into fixed-size so that data can evenly distribute.
3. Custom Partioning: Implement a custom partitioner that distributes the data based on specific characteristics.
4. AQE
5. Repartition or Coalesce: Use repartition or coalesce to redistribute the data among partitions.
6. Salting Technique: salting involves artificially increasing the number of distinct keys in a dataset by appending a random or unique identifier, known as salt helps to distribute data more evenly across partitions.
   Example: (A,10), (B,15), (A,5), (c,8), (B,20), (A,7)
   (A_1,10), (B_2,15), (A_3,5), (c_4,8), (B_5,20), (A_6,7) -> adding salt
