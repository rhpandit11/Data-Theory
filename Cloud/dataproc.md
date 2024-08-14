

Dataproc is a managed service for running Hadoop and Spark data processing workloads in simpler and cost-efficient way.

While creating Dataproc cluster, you need to provide configuration details like cluster name, region, cluster mode, machine type and disk size for both master and worker nodes, network, subnetwork etc.

pre-installs some of the open source frameworks like:

1. Hadoop
2. Hive
3. Pig
4. Spark

submit different types of job on the cluster as it comes pre-installed with Hadoop and Spark libraries. Eg:

1. Hadoop MapReduce jobs
2. Spark jobs (scala version)
3. Pyspark jobs
4. SparkSQL jobs
5. Hive jobs
6. Pig jobs

Core Features of Dataproc:

**1. Managed Hadoop and Spark**

**2. Speed and Ease of use**

3.**Integration with Google Cloud Services**

**4.Custom Machine Types and Preemptible VMs**

Auto scaling

**Security and permissions**

When to choose Dataproc:

Dataproc is an idea choice , if your team is planning to use open source frameworks like Hadoop and Spark to run data processing workloads
(or)
if your workloads are currently running on Hadoop or Spark on-premises cluster and planning to migrate to GCP, then Dataproc service is a perfect option for you.

Different Use-cases of Dataproc:

1. **Cloud Storage ETL Pipeline:** The source is Google Cloud Storage and after ETL processing on Dataproc, the data is written back to the sink, which is another location in Google Cloud Storage.
2. **Real-time Processing Pipeline from Pub/Sub to Cloud Storage:** The source here is Google Cloud Pub/Sub, providing real-time or near-real-time data feeds. The data gets processed in Dataproc, and the results (the sink) are stored in Google Cloud Storage.
3. **Relational Database to BigQuery Analytics: **External relational databases (such as MySQL and PostgreSQL) serve as the source. Using Dataproc, the data is processed and subsequently, the results are loaded to the sink, Google Cloud BigQuery.
4. **On-Premises to Cloud Migration Scenario** : Data from an onsite Hadoop cluster is migrated into a Google Cloud Storage and uses Dataproc cluster to process the data and store the result in Google Cloud Storage, for disaster recovery, additional processing, or long-term storage. Can also load final processed data to Bigquery from GCS for data warehousing.

How to create Dataproc Cluster:

They are four primary ways to create a Dataproc Cluster:

1. Using Google Cloud Console
2. Using gcloud command-line tool
3. Using Dataproc Rest API
4. Client Libraries (e.g., Python, Java, Node.js, etc.)

Creating Dataproc cluster using Google Cloud Console:

Go to Google Cloud Console page and Search for Dataproc service and then click on create cluster.

fill in the configuration details.

1. **Name of your cluster**
2. **Location** — Choose the region and zone closer to your location for better performance.
3. **Cluster Type** — I have selected **Standard** for this demo. You can select **Single Node** for development purpose or **High Availability** incase you want highly available master node.
4. **Versioning** — Select the Image Type and version based on hadoop and spark version that you want to install in your cluster.
5. **Spark performance enhancements** — We have 3 enhancement options to improve the job’s performance.
   (i) **Enable advanced optimization** — This could make read and write operations more efficient or speed up data processing tasks. It’s typically recommended for most cases.
   (ii) **Enable advanced execution layer — **If you enable this setting, then PySpark jobs will execute with the Arrow-based columnar data processing, which allows for a much more efficient, parallel, and vectorized data processing pattern. This is especially useful when working with large datasets.
   (iii)  **Enable Google Cloud Storage caching ** — This is a setting that improves the performance of jobs that repeatedly read the same data from Google Cloud Storage by caching the data locally on the cluster’s virtual machines.
   **Note** : You can also enable or disable these settings while submitting your individual jobs. So it is advisable to test the performance of your job with or without these options and decide accordingly as these options may not benefit/be effective on all of your jobs.
6. **Network Configuration** — select the primary network and subnetwork that you have created for this cluster or choose default.
7. **Dataproc Metastore** — it is a managed, serverless Apache Hive metastore (HMS). it is used to store metadata about tables, their schemas, location, and other information. You can create a Dataproc metastore first and choose it here incase if you want to manage this metadata in a central and managed environment otherwise just leave it as None.
8. **Component gateway** — It provides secure access to web endpoints for Dataproc default components like Hadoop and Spark web interfaces like for example YARN resource manager.
9. **Optional components** — Choose open source technologies that you want to install on your dataproc cluster apart from the default components.
10. **Click on Configure nodes** — To select the number of nodes, machine type, disk type and size for Master node, Primary and secondary worker nodes.

Click on Customize cluster — some of the important configuration here:
12. **Internal IP Only** — If you enable this option during cluster creation then
— The VMs in your Dataproc cluster will only be assigned an internal IP address.
— The VMs will not have an external public IP address.
— The VMs won’t be reachable directly from the internet.
— The VMs can only be accessed from within the same virtual private cloud (VPC) network or via a VPN (Virtual Private Network) or Cloud Interconnect link.
13. **Initialization actions — **Provide the GCS bucket path to your scripts to install any applications, or to make other modifications to your cluster.
14. **Scheduled deletion — **There two options, either of the options to terminate your cluster.
(i) Delete on a fixed time schedule
(ii) Delete after a cluster idle time period without submitted jobs
15. **Cloud Storage staging bucket —** It is to be used for storing cluster job dependencies, job driver output, and cluster config files. If you dont provide a bucket path, it will create a bucket by default.

16. **Click on create cluster** .
