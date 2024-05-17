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

    MapReduce

---

MapReduce: is the processing layer in hadoop, designed for processing huge volumes of data in parallel by dividing the task into the set of independent task.

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