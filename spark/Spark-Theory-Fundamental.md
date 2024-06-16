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

* Engine — Spark Core: It is the basic core component of Spark ecosystem on top of which the entire ecosystem is built. It performs the tasks of
  scheduling/monitoring and basic IO functionality
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
* Defining the main logic of the Spark application.
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
2. **Stage** - in spark represents a sequence of tranformations that can be executed in a single pass i.e without shuffling of data.(e.g., reduceByKey, groupByKey, sortByKey)
3. **Task** - in spark is the samallest unit of work that can be scheduled. Each stage is divided into task.A task is a unit of execution that runs on a single machine.

```python
import org.apache.spark.sql.SparkSession

// Create a Spark Session
val spark = SparkSession.builder
  .appName("Spark Job Stage Task Example")
  .getOrCreate()

// Read a CSV file - this is a transformation and doesn't trigger a job
val data = spark.read.option("header", "true").csv("path/to/your/file.csv")

// Perform a transformation to create a new DataFrame with an added column
// This also doesn't trigger a job, as it's a transformation (not an action)
val transformedData = data.withColumn("new_column", data("existing_column") * 2)

// Now, call an action - this triggers a Spark job
val result = transformedData.count() 

println(result)

spark.stop()
```

1. A Job is triggered when we call the action `count()`. This is where Spark schedules tasks to be run.
2. Stages are created based on transformations. In this example, we have two transformations (`read.csv` and `withColumn`). However, these two transformations belong to the same stage since there's no data shuffling between them.
3. Tasks are the smallest unit of work, sent to one executor. The number of tasks depends on the number of data partitions. Each task performs
   transformations on a chunk of data.

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

1. **RDD**(Low Level Abstraction):  Fundamental datastructure of spark, it is immutable distributed collection of object that can be any type.

   **Spark Dataframe**(High Level Abstraction): distributed data structure which store data in two-dimensional table with named columns and defined schema(column name, datatype).

   **Spark Dataset**(High Level Abstraction): spark rdd + dataset uses all the capabilities of both (type-safety -> through error on compilation time).

Difference Between RDD, Dataframe, Dataset:

| RDD                                | Dataframe          | Dataset                 |
| ---------------------------------- | ------------------ | ----------------------- |
| No schema                          | schema             | schema                  |
| slow on non JVM launguages         | fast               | fast                    |
| No execution optimization          | catalyst optimizer | catalyst optimizer      |
| Low Level                          | High               | High                    |
| No SQL support                     | SQL support        | SQL support             |
| Type safe                          | No Type Safe       | Type Safe               |
| Analysis error detect compile time | Runtime            | compile time            |
| High memory used                   | High               | Low because of Tungsten |

**Difference Between Dataframe, Dataset:**

| Category          | Dataframe                                                                                              | Dataset                                                           |
| ----------------- | ------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------- |
| Data Type:        | Tabular data structure with rows and columns                                                           | collection of strongly typed JVM objects<br />and it is type safe |
| performance       | faster than dataset it used code generation and build<br />on top of rdd and optimized for performance | slow because of JVM                                               |
| API               | wide variety of API's than dataset and more flexible<br />for data manipulation                        | limited API's but more concise and<br />expressive               |
| Type Safety       | Runtime Errors                                                                                         | Compile Time errors                                               |
| Memory Management | Use High Memory                                                                                        | Low memory because of Tungsten                                    |
| launguages        | Java, Python, Scala, R                                                                                 | Scala, Java                                                       |

**Use:**

◽DataFrames: Perfect for structured data and SQL-like queries. They offer excellent performance and ease of use, making them ideal for ETL operations and data analysis.
◽Datasets: Ideal when you need the optimizations of DataFrames along with the type safety of RDDs. They are great for complex transformations that benefit from compile-time type checking.

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
3. Task Scheduling and Execution: Spark’s scheduler assigns tasks to individual executors across the cluster. Tasks within a stage can run concurrently whenever possible.
4. Result Collection: The final results of the computation are collected back to the driver node (in the case of actions like `collect()`).

Components: Stages | DAG Scheduler

* Stages: set of tasks execute together in a single wave of computation.
* DAG Scheduler: High - level scheduling layer implements stage-oriented scheduling.

  Works: 1.computes the stages of each job and schdule it, 2.subimt Task set to TaskScheduler 3. convert Logical Execution Plan to Physical Execution Plan. 4. React on fault tolerance

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
