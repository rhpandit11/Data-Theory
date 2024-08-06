**Pyspark:** PySpark is an Apache Spark interface in Python. It is used for collaborating with Spark using APIs written in Python. It also supports Spark's features like Spark DataFrame, Spark SQL, Spark Streaming, Spark MLlib and Spark Core.

**advantages:**

* Simple to use: Parallelized code can be written in a simpler manner.
* Error Handling: PySpark framework easily handles errors.
* Inbuilt Algorithms: PySpark provides many of the useful algorithms in Machine Learning or Graphs.
* Library Support: Compared to Scala, Python has a huge library collection for working in the field of data science and data visualization.

**Disadvantages:**

---

```python
df.format(....)\
  .option("key","value")\
  .schema(....)\
  .load(...)
```

format -> data file format(by default parquet)

    (csv,json,JDB/ODBC,Table,Parquet)

option -> inferschema,mode,header(optional)

schema -> manual schema you can pass (optional)

load -> path from where our data is reading

dataframe Reader API Access -> spark.read

Example:

```python
spark.read.format("csv")\
          .option("header","true")\
          .option("inferschema","true")\
          .option("mode","FAILFAST")\
          .load("c:/user\download\data.csv")
  
```

Mode:

1. FailFast -> fail execution if mailformed record
2. DropmalFormed -> drop the corrupted record
3. premissive -> default -> set nullvalue to corupted fields

Schema We can create using two method

1. structType (which defines our structure of DF),StructField(list of struct field)
2. DDL

```python
schema = structType([
		   	structField("Id",IntegerType(),True),#nullable
			structField("name",StringType(),True),
			structField("age",InetegerType(),True)
	            ])
```

DDL Method:

```
ddl_myschema = "id Integer,name string,age int"
```

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

---

PySpark is the Python API to Apache Spark, meaning that we can write Python code that calls Spark automatically.


how to read file in pyspark:

```python
spark.read.format('csv') \
	  .option('header','true') \
          .option('inferSchema','false') \
	  .option('skipRows',1) \
	  .schema(my_schema ) \
          .option('mode','FAILFAST') \
          .load('c:\user\download\data.csv')
```

mode:

* FailFast - fail execution if mailformed record in dataset
* Dropmalformed - drop the corrupted record
* Permissive(default) - set null value to all corrupted fields

How to create a schema in pyspark:

Using two methods:

* StructType - (which defines our structure of DF. collection of StructField),   StructField
* DDL

using StructType and field method:

```python
from pyspark.sql.types import StructType, StructField
my_schema = StructType ([
		   	  StructField("id", IntegerType(), True),
		          StructField("name", StringType(), True),
			  StructField("age", IntegerType(), True),
			  StructField("_corrupt_record", StringType(), True), #for handling bad records
			])
```

DDL Method:

ddl_my_schema = "id integer, name string, age integer"


Corrupted Record Handling: To handle corrupt record we will define our own schema with "_courrupt_record" filed name and make this string type.Later we can access that by loading the badRecordsPath.

```python
spark.read.format('csv') \
	  .option('header','true') \
          .option('inferSchema','false') \
	  .schema(my_schema) \
	  .option('badRecordsPath', 'c:\user\download\bad_records') \ #by default in .json format
          .load('c:\user\download\data.csv')

```


Read Json File:


Parquet: columnar based hybrid structured binary file format

by default 128mb
