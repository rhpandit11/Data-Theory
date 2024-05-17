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
6. Streaming read are made possible throgh HDFS
