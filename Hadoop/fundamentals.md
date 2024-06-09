**Hadoop:** Apache Hadoop is a framework which provides us various services or tools to store and process Big Data. It helps in analyzing Big Data and making business decisions out of it, which can’t be done efficiently and effectively using traditional systems.

**Distributed FileSystem**: filesystem that allow store data in multiple machines or nodes in a cluster and allow multiple users to access data.

**HDFS:** In hadoop framework HDFS is the primary data storage system.

**Components:**

1. **Namenode(RAM):** is the master node, stores the metadata and slave configuration. There is one active namenode and one or more standby namenode(secondary). Active name node serves client requests, standby name node handles high availability configuration.
   **WORK:**
   1. Manage filesystem namespaces and the single hadoop cluster failure point
   2. keep track of all blocks with there location details
   3. manage request of clients actual data files
   4. metadata of actual data is also stored here like file information, block information, permission.
2. **Data Node:** worker node of HDFS, can be n in number, responsible for serving actual read and write request to clients. Actual data stores here.
   WORK:
   1. stores actual data.
   2. instructed by name node, data node is responsible for storing and deleting blocks and replicating these blocks.
   3. Handles the client's read and writes requests
   4. datanodes synchronized to communicate and ensure the data is balanced accross the cluster starting from copying to moving.

**Secondary Namenode:** maintains the edit log and namespace image information in sync with the namenode server. At times the namespace images from the namenode server are not updated therefore, you can not totaly rely on the secondary namenode server for the recovery process.

**FS Image:** file stored on the os filesystem that contains the complete directory structure with details about the location of the data on the data blocks and which are stored on which node.

**EditLogs:** is the transaction log that record the changes in the HDFS filesystem or any action performed on the HDFS cluster such as addition of new block, replication, deletion etc.

**CheckPointing:** is the process of merging the content of the most recent fsimage, with all edits applied after that fsimage is merged, to create a new fsimage. it triggered automatically by configuration policies or manually by HDFS administration commands.

**File System:** expose a file system namespace and allows user data to be stored in files. It has hierarchical file system with directories and files.

**Blocks:** unit of stored data in hdfs by default is 128MB, EX: file size : 512mb divided into 4 block storing 128mb each.

**Rack:** collection of 30-40 data nodes or machines in a hadoop cluster located in a single data center or location. These datanodes in a rack are connected to the namenode throgh traditional network design via a network switch.

**HDFS Read Operations:**

1. Client call -> open() method on the filesystem object.
2. filesystem calls -> namenode using RPC -> get the location of the blocks of a file -> return the address of close datanodes
3. filesystem -> return the FSDataInputStream to the client.
4. client-> calls read() method on FSDataInputStream object.
5. DFSInputStream(wraped in FSDataInputStream) contain the address of blocks of the file -> connects to the closet data nodes-> read the first block of the file.
6. after reaching end of the file -> DFSInputStream close the connection with that data node -> finds the next nearest block.
7. client reading completed -> it calls close() on FSDataInputStream.

**HDFS Write Operations:**

1. client calls -> create() method-> on filesystem to create a file.
2. filesystem -> interacts with namenode throgh RPC -> call create a new file in the filesystem namespace with (file-size,dest_path..)
3. namnode make sure that file doesn't already exists and permission to create a file.
4. filesystem -> returns FSDataOutputStream to start writing data to datanode.
5. as clients start writing the data -> DFSOutputStream(wrapped) splits the clients data into packets and writes it to an internal queue callled data queue.
6. Datastreamer responsible for telling the namenode to allocate new blocks by choosing the list of suitable data nodes to store the replicas.
7. client -> close() method on the stream when it finishes writing data.
8. FSDataOutputStream -> sends acknowledgment to Namenode.

**Replication Factor:** HDFS creates replicas of block based on the replication factor (a number that defines the total copies of a block of a file.) be default 3.means 3 copies of each block are created and stored accross multiple nodes.

**DataNode Failure:** data node send hearbeat to namenode in every 3 second("I AM ALIVE"). If namenode does not get hearbeat from any particular datanode for more that 10 minutes then consider it as dead and start creating a replica of block that were available on that data node.

**Benefits of HDFS:**

1. HDFS is not only for storing big data but also for facilitating the processing of big data.
2. HDFS is cost-effective because it can be run on cheap hardware does not require powerful machine.
3. HDFS is high-fault tolerance because of replica of the data may be available from different node through replication.
4. HDFS is famous for rack awareness to avoid data loss which result in increased latency.
5. HDFS is scalable, includes vertical and horizontal scalability mechanism by adjusting the resources according to size of your file system.
6. Streaming read are made possible throgh HDFS.

---

Inetrview Question:

###### What are active and passive “NameNodes”?

* Active “NameNode” is the “NameNode” which works and runs in the cluster.
* Passive “NameNode” is a standby “NameNode”, which has similar data as active “NameNode”.

When the active “NameNode” fails, the passive “NameNode” replaces the active“NameNode” in the cluster. Hence, the cluster is never without a“NameNode” and so it never fails.

###### What happens when two clients try to access the same file in the HDFS?

HDFS supports exclusive writes only.

When the first client contacts the “NameNode” to open the file for writing, the “NameNode” grants a lease to the client to create this file. When the second client tries to open the same file for writing, the "NameNode” will notice that the lease for the file is already granted to
 another client, and will reject the open request for the second client.

###### How does NameNode tackle DataNode failures?

NameNode periodically receives a Heartbeat (signal) from each of the DataNode in the cluster, which implies DataNode is functioning properly.A block report contains a list of all the blocks on a DataNode. If a DataNode fails to send a heartbeat message, after a specific period of time it is marked dead.

The NameNode replicates the blocks of dead node to another DataNode using the replicas created earlier.

###### What will you do when NameNode is down?

The NameNode recovery process involves the following steps to make the Hadoop cluster up and running:

1. Use the file system metadata replica (FsImage) to start a new NameNode.
2. Then, configure the DataNodes and clients so that they can acknowledge this new NameNode, that is started.
3. Now the new NameNode will start serving the client after it has completed loading the last checkpoint FsImage (for metadata information) and received enough block reports from the DataNodes.
   Whereas, on large Hadoop clusters this NameNode recovery process may consume a lot of time and this becomes even a greater challenge in the case of the routine maintenance.

###### What is a checkpoint?

In brief, “Checkpointing” is a process that takes an FsImage, edit log and compacts them into a new FsImage. Thus, instead of replaying an edit log, the NameNode can load the final in-memory state directly from the FsImage. This is a far more efficient operation and reduces NameNode startup time. Checkpointing is performed by Secondary NameNode.

###### How is HDFS fault tolerant?

When data is stored over HDFS, NameNode replicates the data to several DataNode. The default replication factor is 3. You can change the
configuration factor as per your need. If a DataNode goes down, the NameNode will automatically copy the data to another node from the
replicas and make the data available. This provides fault tolerance in HDFS.

###### Can NameNode and DataNode be a commodity hardware?

The smart answer to this question would be, DataNodes are commodity hardware like personal computers and laptops as it stores data and are required in a large number. But from your experience, you can tell that, NameNode is the master node and it stores metadata about all the blocks stored in HDFS. It requires high memory (RAM) space, so NameNode needs to be a high-end machine with good memory space.

###### Why do we use HDFS for applications having large data sets and not when there are a lot of small files?

HDFS is more suitable for large amounts of data sets in a single file as compared to small amount of data spread across multiple files. As you
know, the NameNode stores the metadata information regarding the file system in the RAM. Therefore, the amount of memory produces a limit to the number of files in my HDFS file system. In other words, too many files will lead to the generation of too much metadata. And, storing these metadata in the RAM will become a challenge. As a thumb rule,metadata for a file, block or directory takes 150 bytes.

###### How do you define “Rack Awareness” in Hadoop?

**Rack Awareness** is the algorithm in which the “NameNode” decides how blocks and their replicas are placed, based on rack definitions to minimize network traffic between “DataNodes” within the same rack. Let's say we consider replication factor 3 (default), the policy is that“for every block of data, two copies will exist in one rack, third copy in a different rack. This rule is known as the “Replica Placement Policy.

###### What is “speculative execution” in Hadoop?

If a node appears to be executing a task slower, the master node can redundantly execute another instance of the same task on another node.
Then, the task which finishes first will be accepted and the other one is killed. This process is called “speculative execution.

###### How can I restart “NameNode” or all the daemons in Hadoop?

This question can have two answers, we will discuss both the answers. We can restart NameNode by following methods:

1. You can stop the NameNode individually using ***/sbin /hadoop-daemon.sh stop namenode ***command and then start the NameNode using*.* ***/sbin/hadoop-daemon.sh start namenode ***command.
2. To stop and start all the daemons, use**.**  ***/sbin/stop-all.*** and then use .***/sbin/start-all.sh*** command which will stop all the daemons first and then start all the daemons.

These script files reside in the sbin directory inside the Hadoop directory.

###### What is the difference between an “HDFS Block” and an “Input Split”?

The“HDFS Block” is the physical division of the data while “Input Split”is the logical division of the data. HDFS divides data in blocks for
storing the blocks together, whereas for processing, MapReduce divides the data into the input split and assign it to mapper function.

###### Name the three modes in which Hadoop can run.

The three modes in which Hadoop can run are as follows:

1. ***Standalone (local) mode*** : This is the default mode if we don’t configure anything. In this mode, all the components of Hadoop, such NameNode, DataNode, ResourceManager, and NodeManager, run as a single Java process. This uses the local filesystem.
2. ***Pseudo-distributed mode*** :
   A single-node Hadoop deployment is considered as running Hadoop system in pseudo-distributed mode. In this mode, all the Hadoop services, including both the master and the slave services, were executed on a single compute node.
3. ***Fully distributed mode*** :
   A Hadoop deployments in which the Hadoop master and slave services run on separate nodes, are stated as fully distributed mode.

**What is Job History Server**

It maintains information about MapReduce jobs after the Application Master terminates.

**How does NameNode tackles data node failures?**

NameNode periodically receives a Heartbeat (signal) from each of the DataNode in the cluster, which implies DataNode is functioning properly.

**What will you do when NameNode is down?**

Use the file system metadata replica (FsImage) to start a new NameNode. Then, configure the DataNodes and clients so that they can acknowledge this new NameNode, that is started.

**What is checkpoint?**

Checkpointing” is a process that takes an FsImage, edit log and compacts them into anew FsImage. Thus, instead of replaying an edit log, the NameNode can load the final in-memory state directly from the FsImage.

---

    MapReduce

---

MapReduce: is the processing layer in hadoop, designed for processing huge volumes of data in parallel by dividing the task into the set of independent task.

Components of MapReduce

1. Map Phase:

- Input: The input data is divided into smaller, manageable chunks, typically using an input format such as key-value pairs.
- Processing: Each chunk is processed by a mapper function that performs a specific task, such as filtering, sorting, or transforming the data.
- Output: The mapper function generates intermediate key-value pairs.

2. Shuffle and Sort Phase:

- Intermediate Data: The intermediate key-value pairs produced by the mappers are shuffled and sorted based on the keys. This phase ensures that all values associated with the same key are grouped together.
- Distribution: The sorted key-value pairs are distributed to reducers based on the key.

3. Reduce Phase:

- Input: Each reducer receives a set of intermediate key-value pairs grouped by the key.
- Processing: The reducer function processes these groups, typically aggregating or summarizing the data.
- Output: The reducer generates the final output key-value pairs.

Steps in MapReduce

1. Splitting: The input data is split into chunks, each of which will be processed by a separate mapper.
2. Mapping: The mapper processes each chunk independently, producing intermediate key-value pairs.
3. Shuffling and Sorting: The framework shuffles and sorts the intermediate data by key, ensuring that all values associated with a
   given key are sent to the same reducer.
4. Reducing: The reducer processes the grouped intermediate key-value pairs to produce the final output.

Advantages of MapReduce

- Scalability: Can handle very large datasets by distributing the workload across many machines.
- Fault Tolerance: Can recover from failures of individual nodes in the cluster.
- Simplicity: Provides a simple programming model that abstracts the complexity of parallel processing and data distribution.

Disadvantages of MapReduce

- Latency: Not suitable for real-time processing due to the batch-oriented nature of the framework.
- Complexity: Requires careful design of the map and reduce functions, and understanding of data distribution.
- Resource Intensive: Can require significant computational and storage resources, particularly for large datasets.

MapReduce Works: Mapreduce work in two phase 1.Map(write complex logic) 2.Reduce(light-weight processing like aggregation)

Flow Chart:

1. Input FIles: data stored in HDFS it can be any type of file.
2. Input Format: defines how input files are split and read generally use TextInputFormat
3. InputSplits: created by input format logically represent the data which will be further processed by and individual mapper.
4. RecordReader: communicates with InputSplit and converts data into key,value pairs suitable for reading by the mapper.
5. Mapper: process each input record from record reader and generates new key,value pair, and this key,value pair generated by mapper is completely different from the input pair. output of mapper is also known as intermediate output which is written in local disk not stored in HDFS because it will create unnecessary copies.
6. combiner: also called as mini reducer done local aggregation of mappers output which helps to minimize the data transfer between mapper and reducer.
7. Partitioner: used when we working with more than one reducer(for one reducer not required).each combiner output is partioned and a record having the same key,value pair goes into the same partition and then each partition sent to a reducer allows even distribution of map output over the reducer.
8. Shuffling and Sorting: physical movement of the data which is done over the network. mappers are finished and their output is shuffled on the reducer nodes, then this intermediate output is merged and sorted which is then provided as input to reduce phase.
9. Reducer: takes inetrmediate key-value pairs produced by mappers as the input and runs a reducer function on each of them to generate the output.Reducer output is final output that is stored in HDFS
10. RecordWriter: writes the output key-value pair from the reducer phase to the output files.
11. OutputFormat: the way these key-value pairs are written on HDFS by Record writer is determined by outputformat.

Dear Bear River   (deer,Beer,River)           (deer,1) (beer,1) (River,1)       Bear (1,1)   Bear,2

Car Car River       (Car,Car,River)               (car,1) (car,1) (River,1)            car (1,1,1)   car,3

Deer Car Bear     (Dear,car,Bear)               (dear,1) (car,1) (bear,1)          Deer (1,1)   Deer,2

Advantages:

* Scalability: mapreduce is designed for scale horizontally allowing it to process massive datasets accross thousands of nodes.
* Faul Tolerance: If a node fails during processing the framework can reassign the task to another node, ensuring job continues.
* Flexibility: can process structured and unstructured data and also supports various programming languages.
* Cost-Effectivnes: mapreduce can be run on commodity hardware reducing the overall costs of processing the large datasets.

Limitations:

* Latency: not well suited for real-time data processing primarly designed for batch processing.
* complexity: writting efficient map and reduce functions can be challenging particularly for complex data processing tasks.

---

YARN

---

Yarn allows different data processing engines like graph processing, interactive processing, stream processing as well as batch processing to run and process data stored in HDFS. Apart from resource management yarn also does job scheduling.

Components/Daemons:

1. Client: It submits map-reduce job
2. Global Resource Manager: main purpose of resource manager is to disribute resources among various applications in the system. It has two functionalities.

   1. Scheduler: decides allocation of resources to various running applications. Pure scheduler does not monitor or track the status of application.
   2. Application Manager: accept the job submissions, Negotiating resources(containers) for executing the application master, Restarting the Application master in case of failure
3. Application Master: process that runs the main function/entry point of an application, such as spark driver. several responsibilities: Requesting resources, Running the master/driver program
4. Node Manager: Java process that run on slave/worker nodes in a hadoop cluster. responsible for managing containers and resources on each worker node.
5. Container: unit of resource allocation such as CPU, memory, disk space allowing the task to run in a controlled and isolated environment.

Flow Chart:

1. client submits an application to RM
2. RM -> allocates container -> to start the application manager
3. AM -> resgister itself with RM
4. AM -> negotiates containers from the RM
5. AM -> notify the node manager to launch containers
6. Application code is executed in the container
7. client contact -> RM/AM to monitor application's status
8. After task completed -> AM un-registered with RM

Advantages:

1. Flexibility: run various distributed processing systems such as Apache spark, Apache flink, Apache storm and others, also in a single hadoop cluster it allows multiple processing engines run simultaneously
2. Resource Management: allows administartors to allocate and monitor the resources required by each application in a cluster.
3. Scalability: highly scalable handle thousands of nodes in a cluster, it can scale up or down based on the applications.
4. Security: offer kerberos authentication

Disadvantages:

1. Complexity: requires additionla configurations and settings which can be difficult for user who are not familiar with YARN
2. Overhead: Increase overhead because of required managing resources and scheduling applications
3. Single Point of Failure: yarn can be single point failure if it falls the entire cluster to go down need to configure backup yarn
4. Limited Support: YARN has limited support for non-java programming languages.
