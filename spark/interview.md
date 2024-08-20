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
5. In RDDs, *garbage collection (GC) impacts performance, but in DataFrames and Datasets, GC impact is resolved.

*GC - Garbage Collector: When memory is full in RDD, GC will start scanning entire memory and it will start removing the data which is old and obselete.

6) RDD and Datasets provide strong type safety that is at the time of you writing the code it'll give the error if something is wrong and thus they provide run-time compilation error. But, in the case of, DataFrames there's no type safety, so error will be known only once the code is executed and thus, they provides error at compile team.

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

Components: Stages | DAG Scheduler

* Stages: set of tasks execute together in a single wave of computation.
* DAG Scheduler: High - level scheduling layer implements stage-oriented scheduling.

  Works: 1.computes the stages of each job and schdule it, 2.subimt Task set to TaskScheduler 3. convert Logical Execution Plan to Physical Execution Plan. 4. React on fault tolerance


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
| Use            | used in task scheduling, workflow``management, and distributed computing | used in data lineage and data                                                           |

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
