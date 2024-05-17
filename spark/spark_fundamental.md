**Spark:**  spark is a open-source unified analytics engine for large scale data processing.

**Spark Architecture:**

1. **Liabrary Layer** - spark sql,spark streaming, spark Mllib, spark graphx
2. **Api Layer** - Python, Java, Scala, R
3. **Spark Core Layer** -Provides  RDD API for distributed data processing, task schedular for parallelism, an in-memory memory management system.
4. **Cluster Manager** - mesos, yarn, kubernets, standalone.
5. **Storage Layer** - HDFS, S3, ADLS GEN2, Local Storage

**Spark Execution Model:**

1. **Driver** - brain of spark framework
2. **Executor** - worker node responsible for executing the given task.

**Driver Works:**

* sparkcontext/session initialization
* compute the application requirement resoures and also manage dynamic allocation lifecycle
* works/Tasks distributor
* react on node/executor failure
* progress/monitor the executor
* send response to user
* through the metadata job it powers the spark WEBUI

**Executor  Works:** execute the task assigned by driver, report the progress back to driver

**Spark Programming Model:**

1. **Job** - an action encountered in the application
2. **Stage** - Jobs are divide into stages or A suffle dependency in the application
3. **Task** - smaller unit of execution because one task is launched per partition

---

**Spark Internally Working:**

1. user submit job using "sparkSubmit()"
2. "sparkSubmit()" -> driver program  -> execute main() method
3. Driver -> contact cluster manager -> request for resources to launch the executors
4. cluster manager -> launch executors on behalf of driver
5. Executors -> established direct connection with driver.
6. Driver -> determined total number of tasks -> by checking the lineage.
7. Driver -> creates logical and physical plan
8. Physical plan granted -> Spark allocates the task to the executors
9. Task run on executors -> after completion return to driver
10. All Task completed -> main() method -> invokes sparkContextStop().
11. Spark release all resources from cluster manager.

---

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

Dataset prefered over dataframe when data is strongly typed meaning schema is known ahead of time and data is not necessarily homogeneous. Because in dataset type errors will be caught at compile time rather than at runtime. In addition, Datasets can take advantage of the Catalyst optimizer, which can lead to more efficient execution.

---

**2. DAG:** DAG is a more general concept that represents the logical execution plan for a set of stages in a Spark job.It is a combination of vertices as well as edges where vertices represents RDDs and edges represents operation to be applied on RDD.

Components: Stages | DAG Scheduler

* Stages: set of tasks execute together in a single wave of computation.
* DAG Scheduler: High - level scheduling layer implements stage-oriented scheduling.

  Works:

1. computes the stages of each job and schdule it, 2.subimt Task set to TaskScheduler 3. convert Logical Execution Plan to Physical Execution Plan. 4. React on fault tolerance

Step1: DAG Creation: set of Transformation of rdd generated through Lazy Evoluation

Step2: DAG optimization: Logical to Physical

Step3: DAG Execution: Action Triggering -> Stages breaks into Tasks -> DAG Scheduler to Task Scheduler .

---

**Lineage Graph:** Lineage Graph is a historical record of transformations, tracing back to the original data. It is the representation of dependencies in between RDDs rather than the actual data.

**Use:**

1. It's the basis for Spark's lazy evaluation strategy, only executing transformations when an action is invoked.
2. Allows Spark to recover lost data by re-computing it from the lineage graph.

**DAG VS Lineage Graph:**

|                | DAG                                                                     | Lineage                                                                                |
| -------------- | ----------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| Representation | dependencies between tasks or events                                    | history of data transformations or processing steps                                    |
| Cycle          | A DAG does not contain cycles                                           | lineage graph can contain cycles.                                                      |
| Direction      | direction of edges represent the flow of dependencies between tasks     | the direction of edges represent the flow of data transformations or processing steps. |
| Use            | used in task scheduling, workflow management, and distributed computing | used in data lineage and data quality analysis.                                        |

Note: Because dag represent dependencies between task that must be executed in particular order while lineage Represent history of data transformations that may be repeated or looped over.

---

Catalyst Optimizer: It is a robust query optimization framework, responsible for transforming and optimizing Logical and Physical query plans.

How It Works:

1. Parsing: parsing the dataframe to create an AST(abstract syntax tree) represent logical structure of query.
2. Analysis: Sementic Analysis perform on AST resolve/check column or table names, check for syntax errors and type checking to check query is valid or not. Additionaly, collect metadata of columns and tables involved in it.
3. Logical optimization: apply set of logical optimization, it simply or rewrite the query operations without changing overall behaviour or results.
4. Logical Plan: Then it produce logical plan, it is like tree-like representation of queries operations and their dependencies. It captures high level operations like filter, joins, aggregation and projection.
5. Physical Planing: based on logical plan it generates many alternative physical plans, and explore different execution strategies and physical operators for the specific data source involved in the query.
6. Cost-Based Optimization: It checks each physical plan factors like, distribution, network latency, disk I/o, CPU Usage, and memory consumption after that select one physical execution plan which cost is lowest estimated.
7. Code-Generation: After that it generate efficient java bytes code or optimized sql code for executing the query which further optimized by underlying execution engine.
8. Execution: Finally spark sql execuets the optimized physical plan to get the desired results.

Optimization Techniques:

1. Predicate Pushdown: data need to filter out in source level before entering in the Processing pipeline, it push filter condition as close  to the data sources as possible.
2. Column Purining / projection Pushdown: It reads only necessary columns and load it.
3. Broadcast Join: In this small tables copy send to every worker nodes during join with large tables.
4. Join ReOrdering: It re-orders the join's condition to minize the data Shuffle through that it enhance the parallelism and reduce overall execution time.
5. Constant Folding: During query Analysis it evaluates Constant expressions through that reducing the computational overhead.


1. Parsing -> parsing the dataframe to create an Abstract Syntax Tree(AST) represent logical structure of query
2. Analysis -> Semantic Analysis perform on AST structure resolve/check for query is valid or not.
3. Logical Optimization -> apply set of logical optimization, it simply rewrite the query operation without changing overall result.
4. Logical Plan -> Then it produce logical plan, it is like tree like representation of queries operations.It captures high level opearations like join, aggregation etc.
5. Physical Plan -> based on logical plan it generates many alternative physical plans and explore different execution strategies.
6. Cost-based Optimization -> It checks each physical factors like distribution, network latency, disk I/o, CPU usage and memory consumption then seletct one physical plan which cost is lowest estimated.
7. Code-Generation -> After that it generates efficient JAVA byte code or optimizes sql code for executing the query.
8. Execution: Finally spark SQL executes the optimized physical plan to get the desired result.

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

Resources Allocation in Spark:

1. Static Resource Allocation:Resources will be fixed while running the spark application even if resources are free after some filter /transformation.
2. Dynamic Resource Allocation: allows Spark applications to request and release resources (memory and CPU) from the cluster manager dynamically as per need.

   How It Works:

   When enabled, Spark applications can acquire additional resources when the workload increases and release resources when the workload decreases.

   The cluster manager monitors the resource usage and makes decisions about allocating or deallocating resources based on the application's needs.

  Benefits:

    Efficient Resource Utilization: Ensures that resources are allocated based on the actual demand of the application, avoiding over-provisioning or

    under-provisioning.

    Small cluster, bigger impact : Enables sharing resources among multiple applications running on the same cluster.

  How to enable? spark-defaults.conf | spark.shuffle.service.enabled true

    spark.dynamicAllocation.enabled true

    spark.dynamicAllocation.minExecutors 1

    spark.dynamicAllocation.maxExecutors 4

    spark.dynamicAllocation.executorIdleTimeout 60s

    spark.dynamicAllocation.schedulerBacklogTimeout 60s

 Use Cases:

    Well-suited for scenarios where the workload varies over time, and the demand for resources is unpredictable.

    Commonly used in shared environments where multiple Spark applications coexist on the same cluster.

---

Resources Isolation achieved in spark:

1. Utilize resource managers like YARN, Mesos, etc. These managers allocate independent resources for each Spark application, such as memory, CPU, etc., to ensure there is no interference between different applications.
2. Spark's built-in scheduler can dynamically allocate resources based on the application's requirements, ensuring that each application receives enough resources and avoiding resource contention issues.
3. Utilize Spark’s dynamic resource allocation feature. Spark can dynamically adjust resource allocation based on the needs of the application, enabling dynamic isolation of resources to ensure each application receives sufficient resources.

---

Difference between Standalone, mesos and yarn cluster:

1. Independent cluster setup without a resource manager. | Master-slave architecture with dynamic resource allocation. | Part of the Hadoop ecosystem, follows

   master-slave architecture.
2. Resources managed manually, suitable for smaller  development/testing environments. | Fine-grained resource sharing across multiple frameworks. | Primarily

   optimized for running Hadoop MapReduce jobs.
3. Limited scalability and resource optimization compared to yarn, mesos | Supports diverse workloads including Hadoop, Spark, containers, etc. | Integrates

   tightly with Hadoop ecosystem tools and workflows.

---

**Difference between mapreduce and spark:**

| MapReduce                                                 | Spark                                     |
| --------------------------------------------------------- | ----------------------------------------- |
| read/write data to a disk                                 | spark can do it in-memory make it faster. |
| developed in java                                         | developed in scala                        |
| Fault tolerance is done through replication               | done throgh rdd                           |
| Hard to work with real-time data                          | Easy                                      |
| Less costly comparison to spark                           | more costly                               |
| Hadoop can work or process far larger datasets than spark | Less compare to hadoop                    |
