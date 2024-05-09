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
   2. Salting Concept: Add a random value to the key to distribute the data more evenly across partitions.key1 == key1, it should also get satisfied by key1_`<salt>` = key1_`<salt>`
   3. Bucketing: In this, we group/bucket specific attributes of values into fixed-size so that data can evenly distribute.
   4. Custom Partioning: Implement a custom partitioner that distributes the data based on specific characteristics.
   5. AQE
   6. Repartition or Coalesce: Use repartition or coalesce to redistribute the data among partitions.

Salting Work: When certain keys(hot keys) data have high number of occurences, which result in Skewness, now we add random number/string(salt) to the key

so that the record with the same key is now spread accross multiple keys.

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

Checkpoint: used for fault-tolerance and to cut down the lineage of RDDs/dataframes especially in long and complex computations. It breaks the lineage and

stores data to a reliable Storage(HDFS), used in scenario where lineage graph is too long or when you want to recover from failures efficiently.

Note: use cache() -> for optimization purpose Checkpoint() -> for fault tolerance purpose, and reduce the lineage length in complex computations.

---

coalesce and repartition:

coalesce: is used to decrease the number of partitions without invoking Shuffling. It used in when output partitions is less than the input.

repartition: helps to increase or decrease the number of partitions by doing Shuffling of data.

---
