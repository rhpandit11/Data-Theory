**Spark:**  spark is an open-source unified analytics engine for large scale data processing.

**Difference between mapreduce and spark:**

| MapReduce                                                 | Spark                                                                  |
| --------------------------------------------------------- | ---------------------------------------------------------------------- |
| read/write data to a disk                                 | spark can do it in-memory make it faster.                              |
| developed in java                                         | developed in scala                                                     |
| Fault tolerance is done through replication               | done throgh rdd                                                        |
| Hard to work with real-time data                          | Easy                                                                   |
| Less costly comparison to spark                           | more costly                                                            |
| Hadoop can work or process far larger datasets than spark | Less compare to hadoop                                                 |
| MapReduce requires an external scheduler for jobs.        | Spark has its own job scheduler due to the in-memory data computation. |

**Spark Architecture:**

1. **Liabrary Layer** - spark sql,spark streaming, spark Mllib, spark graphx
2. **Api Layer** - Python, Java, Scala, R
3. **Spark Core Layer** -Provides  RDD API for distributed data processing, task schedular for parallelism, an in-memory memory management system.
4. **Cluster Manager** - mesos, yarn, kubernets, standalone.
5. **Storage Layer** - HDFS, S3, ADLS GEN2, Local Storage

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

1. **Job** - an action encountered in the application
2. **Stage** - Jobs are divide into stages or A suffle dependency in the application
3. **Task** - smaller unit of execution because one task is launched per partition

---

**Spark Internally Working:**

1. **Job Submission:** The user submits a Spark application using the SparkContext in the driver program.
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
| provides method for creating RDD's accumulator and broadcasying variable<br />as well as method to start task on executors | provides method for creating dataframe and datasets<br />as well as methods for reading and writting data.      |

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

| Category          | Dataframe                                                                                         | Dataset                                                      |
| ----------------- | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| Data Type:        | Tabular data structure with rows and columns                                                      | collection of strongly typed JVM objects and it is type safe |
| performance       | faster than dataset it used code generation and build on top of rdd and optimized for performance | slow because of JVM                                          |
| API               | wide variety of API's than dataset and more flexible for data manipulation                        | limited API's but more concise and expressive               |
| Type Safety       | Runtime Errors                                                                                    | Compile Time errors                                          |
| Memory Management | Use High Memory                                                                                   | Low memory because of Tungsten                               |
| launguages        | Java, Python, Scala, R                                                                            | Scala, Java                                                  |

**Use:**

◽DataFrames: Perfect for structured data and SQL-like queries. They offer excellent performance and ease of use, making them ideal for ETL operations and data analysis.
◽Datasets: Ideal when you need the optimizations of DataFrames along with the type safety of RDDs. They are great for complex transformations that benefit from compile-time type checking.

---

Transformation: are operations on RDD/Dataframes/Dataset that produce a new distributed dataset from existing one.They are generally lazy meaning they are not executed immediately.EX: map, filter, groupby,join.

* Narrow: each partition of the input rdd contributes to only one partition of the output rdd.ex: map,filter
* Wide: each partition of the input rdd may contribute to multiple partition of the output rdd(ex: groupby,reducebykey,join)

Action: are operations that trigger the execution of transformation and return value to the driver program or write data to external storage system.ex: collect,count,first,saveAsTextFile.

---

**2. DAG:**  represents the logical execution plan for a set of stages in a Spark job.It is a combination of vertices as well as edges where vertices represents RDDs and edges represents operation to be applied on RDD.

Components: Stages | DAG Scheduler

* Stages: set of tasks execute together in a single wave of computation.
* DAG Scheduler: High - level scheduling layer implements stage-oriented scheduling.

  Works:

1. computes the stages of each job and schdule it, 2.subimt Task set to TaskScheduler 3. convert Logical Execution Plan to Physical Execution Plan. 4. React on fault tolerance

Step1: DAG Creation: set of Transformation of rdd generated through Lazy Evoluation

Step2: DAG optimization: Logical to Physical

Step3: DAG Execution: Action Triggering -> Stages breaks into Tasks -> DAG Scheduler to Task Scheduler .

---

**Lineage Graph:** Lineage Graph is a historical record of transformations, tracing back to the original data. It represent the dependency in between rdds.

**Use:**

1. It's the basis for Spark's lazy evaluation strategy, only executing transformations when an action is invoked.
2. Allows Spark to recover lost data by re-computing it from the lineage graph.

**DAG VS Lineage Graph:**

|                | DAG                                                                          | Lineage                                                                                     |
| -------------- | ---------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| Representation | dependencies between tasks or events                                         | history of data transformations or processing steps                                         |
| Cycle          | A DAG does not contain cycles                                                | lineage graph can contain cycles.                                                           |
| Direction      | direction of edges represent the flow<br />of dependencies between tasks     | the direction of edges represent the flow of data transformations<br />or processing steps. |
| Use            | used in task scheduling, workflow<br />management, and distributed computing | used in data lineage and data quality analysis.                                             |

Note: Because dag represent dependencies between task that must be executed in particular order while lineage Represent history of data transformations that may be repeated or looped over.

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

Lazy Evoluation: In spark it's a powerful concept that allows the optimization of data processing tasks by postponing the execution of transformations until an action is called.

work: When we apply a transformations, spark records it but doesn't executes it immediately, meaning it builds dag of transformations and the execution occurs only when an action is triggered.

Benefits:

1. Optimization: Spark can optimize the entire computation plan by evaluating only the required transformations, skipping unnecessary work.
2. Fault tolerance: Lazy evaluation allows Spark to recompute only the lost or incomplete data, ensuring fault tolerance.
3. Performance: It enables pipelining of tasks, reducing the need to write intermediate results to disk.

What if Mapreduce has lazy evoluation:

1. On-demand processing 2. Resource Optimization 3.Pipeline Fusion 4. Reducing Redundant computations

What if spark does not have lazy evoluation:

Without lazy evaluation, Spark would need to execute transformations immediately, leading to unnecessary computations and increased memory usage.

This could result in performance degradation, especially for complex data processing tasks involving multiple transformations.

---

**Deployment Mode:**

1. Local Mode: Execution not done in distributed manner, means single JVM process is used to produce both driver and executor.
2. Client Mode: Driver is present in Client machine, means driver is not the part of cluster and on the other side executors run within the cluster.
3. Cluster Mode: Driver and executor both run inside the cluster. Spark job submitted from local to cluster machine

---

**Resource Allocation:**

1. Static Resource Allocation: resources are pre-allocated to the spark application before it starts running, amount of resources are fixed and cannot be changed during runtime.
   **Disadvantages:** 1. Inefficient Resource Utilization  2. Limited Flexibility
2. Dynamic Resource Allocation: It is a feature in spark that allows for automatic adjustment of the number of executors allocated to an application a run time.Useful for applications that have varying workloads and need to scale up or down depending on the amount of data being processed.
   **Advantages:** 1. Resource efficiency  2. Scalability  3. Cost Savings  4. Fairness
   **Disadvantages:** 1. Overhead  2. Latency  3. Configuration Complexity  4. Unpredictability  5. Increased Network Traffic.

---

Resources Isolation achieved in spark:

1. Utilize resource managers like YARN, Mesos, etc. These managers allocate independent resources for each Spark application, such as memory, CPU, etc., to ensure there is no interference between different applications.
2. Spark's built-in scheduler can dynamically allocate resources based on the application's requirements, ensuring that each application receives enough resources and avoiding resource contention issues.
3. Utilize Spark’s dynamic resource allocation feature. Spark can dynamically adjust resource allocation based on the needs of the application, enabling dynamic isolation of resources to ensure each application receives sufficient resources.

---

Difference between Standalone, mesos and yarn cluster:

1. Independent cluster setup without a resource manager. | Master-slave architecture with dynamic resource allocation. | Part of the Hadoop ecosystem, follows master-slave architecture.
2. Resources managed manually, suitable for smaller  development/testing environments. | Fine-grained resource sharing across multiple frameworks. | Primarily optimized for running Hadoop MapReduce jobs.
3. Limited scalability and resource optimization compared to yarn, mesos | Supports diverse workloads including Hadoop, Spark, containers, etc. | Integrates tightly with Hadoop ecosystem tools and workflows.

---

**Difference between mapreduce and spark:**

| MapReduce                                                 | Spark                                                                  |
| --------------------------------------------------------- | ---------------------------------------------------------------------- |
| read/write data to a disk                                 | spark can do it in-memory make it faster.                              |
| developed in java                                         | developed in scala                                                     |
| Fault tolerance is done through replication               | done throgh rdd                                                        |
| Hard to work with real-time data                          | Easy                                                                   |
| Less costly comparison to spark                           | more costly                                                            |
| Hadoop can work or process far larger datasets than spark | Less compare to hadoop                                                 |
| MapReduce requires an external scheduler for jobs.        | Spark has its own job scheduler due to the in-memory data computation. |

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

---

Shared Variables: There are two different types of Shared Variables in spark -Broadcast Variable and Accumulator

1. Broadcast Variables: are read-only Variables distributed across worker nodes in-memory. The data Broadcasted this way is cached in serialized form and deserialized before running each task. Used for cache a value in memory on all nodes generally small datasets only Broadcasted.
2. Accumulator: Which are used to update the variables in parallel during execution/runtime and share results from worker to driver.similar to counters in Mapreduce. used for performing associative and commutative operations such as counters or sums.

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

coalesce and repartition:

coalesce: is used to decrease the number of partitions without invoking Shuffling. It used in when output partitions is less than the input.

repartition: helps to increase or decrease the number of partitions by doing Shuffling of data.
