**Pyspark:** PySpark is an Apache Spark interface in Python. It is used forcollaborating with Spark using APIs written in Python. It also supports Spark’s features like Spark DataFrame, Spark SQL, Spark Streaming, Spark MLlib and Spark Core.

**advantages:**

* Simple to use: Parallelized code can be written in a simpler manner.
* Error Handling: PySpark framework easily handles errors.
* Inbuilt Algorithms: PySpark provides many of the useful algorithms in Machine Learning or Graphs.
* Library Support: Compared to Scala, Python has a huge library collection for working in the field of data science and data visualization.

**Disadvantages:**

---

**SparkContext:** PySpark SparkContext is an initial entry point of the spark functionality. It also represents Spark Cluster Connection and can be used for creating the Spark RDDs (Resilient Distributed Datasets) and broadcasting the variables on the cluster.

---

**PySpark serializers:** The serialization process is used to conduct performance tuning on Spark. The data sent or received over the network to the disk or memory should be persisted.

* **PickleSerializer:** This serializes objects using Pythons PickleSerializer (`class pyspark.PickleSerializer`). This supports almost every Python object.
* **MarshalSerializer:** This performs serialization of objects. We can use it by using `class pyspark.MarshalSerializer`. This serializer is faster than the PickleSerializer but it supports only limited types.

---

**Is PySpark faster than pandas?** PySpark supports parallel execution of statements in a distributed environment, i.e on different cores and different machines which are not present in Pandas. This is why PySpark is faster than pandas.

---

**PySpark UDF:** User Defined Function that is used to create a reusable function in Spark.After creation it can be re-used on multiple dataframes and SQL(after registering).default type is string.

```python
```python
def upperCase(str):
    return str.upper()
upperCaseUDF = udf(lambda z:upperCase(z),StringType())   

df.withColumn("Cureated Name", upperCaseUDF(col("Name"))) \
  .show(truncate=False)
```

---

**SparkConf:** used for setting the configuration and parameters required to run applications on a cluster or local system.

---

**create SparkSession:** sparkSession class from the pyspark.sql liabrary has the getOrCreate() method which creates new sparkSession.

```python-
import pyspark
from pyspark.sql import SparkSession
spark = SparkSession.builder.master("local[1]") 
                   .appName('InterviewBitSparkSession') 
                   .getOrCreate()
```

master() -> setting up the mode where application run clustermode/standalone mode for standalone mode we use local[x] value where x represents partition count to be created in RDD,dataframe,dataset.ideally x is CPU numbers of cores available.

appName() -> setting the application name

getOrCreate() -> returning sparkSession object. creates new one if it does not exists

for creating new sparkSession every time we use spark_session = SparkSession.newSession

---

Creating RDD:

* `sparkContext.parallelize() -> do not require data but require partition for creating empty RDD`
* `sparkContext.textFile() -> read .txt file and convert them into RDD`
* `sparkContext.wholeTextFiles() -> returns pairRDD(key,value)`
* `sparkContext.emptyRDD -> RDD with no data`

Creating DataFrames:

`createDataFrame()`-> spark session method

---

Pyspark's startsWith() and endsWith() methods: methods belongs to column class and are used to searching datagrames rows by checking if the column values startswith some values or endwith some value.

* **startsWith()** – returns boolean Boolean value. It is true when the value of the column starts with the specified string and False when the match is not satisfied in that column value.

* **endsWith()** – returns boolean Boolean value. It is true when the value of the column ends with the specified string and False when the match is not satisfied in that column value.