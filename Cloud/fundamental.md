Cloud computing is the delivery of computing services like servers, storage, databases, networking tools and storage over the internet.

characteristics:

* On-demand self service - Access from any where
* Broad Network Access - Access from any devices
* Resource Pooling -  EX: car pooling, micro sd card in phone use as external or internal
* Rapid Elasticity - pay as you go
* Measured Services - billing of resources user uesed

Types Of Cloud Computing Services:

1. IaaS (Infrastructure as a Service) - Networking, Storage, Servers, Virtualisation EX: VM,EC2
2. PaaS (Platform as a Service) - Networking, Storage, Servers, Virtualisation, OS, Middleware, Runtime EX: Cloud App Engine
3. SaaS (Software as a Service) - Networking, Storage, Servers, Virtualisation, OS, Middleware, Runtime, Application EX: Mail
4. Serverless Computing

Types Of Cloud:

1. Public Cloud - Any one can access - EX: GCP,ACURE,AWS
2. Private Cloud - Openstack
3. Hybrid Cloud - Public + Private

---

Regions: are independent geographic areas that consist of zones. They affect pricing, reliablity, networking and performance.

EX: VM

Zone: A zone is a deployment area for google cloud resources within a region. Zones should be considered a single failure within a region.

To deploy fault tolerant application with high availability and help to protect against unexpected failures deploy your application across multiple zones in a region.

EX: app engine

Multi-Regional: service are designed to be able to function following the loss of a single machine region.

EX: BigQuery, BigTable, CloudStorage, Spanner, DataStore, Firestore, ArtifactRegistry

Note: if a single region fails only customers solely in that region are impacetd. customer who have multi-region products are not imapcated.

**Regions ends with - 1,2,3 Zones ends with a,b,c

 When Selecting a zone yourself here are something to keep in mind:

* communication within end across regions will increase different cost.
* design important system with redundancy across multiple zones or regions at same point in time, your instance migh experience an unexpected failure. To mitigate the effect of these possible events you should duplicate important systems in multiple zones and regions.

---

Resource Hierarchy in GCP:

Organization - contains all billing account

 Folders - in folders there may be subfolders of subfolders(optional)

Projects - associated with one billing account - in prject there is no subprojects

Resources - belongs to one project only

VM - Storage

**billing start from bottom to top

The purpose of the google cloud resource hierarchy:

* provide a hierarchy of ownership, which binds the lifecycle of a resource to its immediate parent in the hierarchy.
* provide attach points and inheritance for access control and organisation policies.

GCP resources hierarchy resembles the file system found in traditional OS as a way of organising and managing entities hierarchically. Each resource has exactly one parent.

Benefits of the organisation Resources:

* with an organization resource, projects belongs to your organization instead of the employee who created the project. This means that the projects are no longer deleted when an employee leaves the company.
* You can grant roles at the organization level, which are inherited by all projects and folders under the organization resource. for eg. you can grant the network admin role to your networking team at the organization level allowing them to manage all the networks in all projects in your company instead of granting them the role for all individual projects.

Folders: provides an additional grouping mechanism and isolation boundries between projects can contain other subfolders and alos it is optional means if you can directly create a project without creating a folder.

---

Projects:

* All gcp resources you use are associated to one specific project.
* You can track resources and quota usage
* Enable billing and set budget
* Manage permission and credentials
* Project is a global entity
* Enable services and API
* Equivalent to account in AWS and Subscription in MicrosoftAzure

| ProjectId       | ProjectName         | Project Number  |
| --------------- | ------------------- | --------------- |
| Globally Unique | Uniqueness not req. | Globally Unique |
| choosen by user | choosen by you      | Assigned by gcp |
| Immutable       | Mutable             | Immutable       |

---

Cloud Storage

Types:

1. Cloud Storage - in aws(S3)
2. Persistent Disk - in aws(EBS)
3. FileStore - in aws (EFS - Elastic filestore)

Google Cloud Database Store:

1. Bigtable
2. Firestore
3. CloudSQL
4. CloudDatabase
5. CloudSpanner
6. MemoryStore

---

Cloud Storage: is a service for storing your objects in google cloud. An object is an immutable piece of data consisting a file of any size and format.

You stores objects in containers called buckets.

ways to access:

* console
* gsutil - cloudshell
* client libraries
* Rest Api's

Cloud Storage Classes:

1. standard storage  - hot storage - for present data access
2. Nearline Storage - warm storage - for 1months data access
3. Coldline Storage -  cold storage - for 3 months data access
4. Achive Storage - for 1 year data access

*cost reduce from up to down *data retrieval time increase from up to down.

**Characteristics:**

* A storage classes is a peice of metadata that is used by every object.
* The storage class set for an object offsets the object availability and pricing model.
* You can change the storage class of an existing object either by rewriting the object or by using object lifecycle management.
* when you create a bucket you can specify a default storage class for the bucket if you don't specfy then default storage in standard.

All storage Class provides the following:

* Unlimited storage with no minimum object size
* worldwide accessibility and worldwide storage location
* low latency
* High Durability (99.999999999)
* Geo redundancy, if the data is stored in a multi-region or dual region.
* A uniform experience with cloud storage features, security, toold and APIs.
* Object written to cloud storage must be redundantly stored in at least two different availabilty zones before the write as acknowledged is successful.
* Max size of an object stored in cloud bucket is 5TB.
* There is a 100 ACl limits per object.
* A multiple upload can have upto 10,000 parts. An individual part has max size limit of 5GB. Object assembled from a multipart upload are subject to the overall 5TB size limit.

---

**Standard Storage:** is best for data that is frequently accessed (hot data) or stored for only brief periods of time.

* when used in a region, standard storage is appropriate for storing data in the same location as GKE cluster or compute engine instances that use the data.
* Regional storage is redundant within a region
* when used in dual-region, improved availability.
* when used in multi-region, ideal for storing data that is accessed around the world such as serving website content, streaming videos, executing interactive workloads or serving gaming data or apps.
* Multi-regional is Geo-redundant stored accross 2 or more regions which are 500 miles apart.

Availablity of standard storage data is:

| Location Type | Availability Service<br /> Level Agrement(SLA) |
| ------------- | ---------------------------------------------- |
| Multi-region  | 99.95%                                         |
| Dula-region   | 99.95%                                         |
| Regional      | 99.90%                                         |

---

**Nearline Storage:** is a low-cost, highly durable storage service for storing infrequently accessed data.

* Nearline storage is better choice than standard storage in scenarios where slightly lower availability, a 30-day minimum storage duration and cost for data access are acceptable trade-offs for lowered at rest storage costs.
* Nearline storage is ideal for data you plan to read or modify on average once per month.

Availablity of Nearline storage data is:

| Location Type | Availability Service<br /> Level Agrement(SLA) |
| ------------- | ---------------------------------------------- |
| Multi-region  | 99.99%                                         |
| Dula-region   | 99.9%                                          |
| Regional      | 99.90%                                         |

---

**Coldline Storage:** coldline storage provides very low-cost highly durable storage service for storing infrequently accessed data(cold data).

* coldline storage is ideal for data you plan to read or modify at most once a quarter.

Availablity is same as nearline.

---

**Archive Storage:** storage is cheapest highly durable storage service for data archiving online backup and disaster recovery.

* unlike the 'coldest' storage service offer by other cloud provides your data is available within miliseconds not hours or days.
* Archive storage has higher cost for data access as well as 365 day min. storage duration.
* Archive storage is the best choice for data that you plan to access less than a year.

Availablity is same as nearline or coldline.

To Maximize the availability of your data:

* consider storing your data in multi-regional or dual-regional bucket location if high availability is a top requirement.
* All data is stored geo-redundantly in these locations, which means your data is stored in at least two geographically separated regions.In the unliked event like region wide  outage, buckets in geo-redundant location remains available with no need to change storage path.
* You cannot change bucket location or project after creation.

---

Cloud Storage Pricing:

pricing based on:

* Data Storage: the amount of data stored in your buckets. Storage rates vary depending on storage class of your data and location of your buckets.
* Data Processing: The processing done by cloud storage, which includes operations charges any applicable retrieval fees and inter-region replication.
* Netwrok usage: The amount of data read from or moved between your buckets

---

Bucket: bucket is like a folder for your objects.

* using buckets you can organise and maintain access permissions
* you cannot create nested buckets
* buckets has name, default storage class, geographic locations.
* Named and location can only be changed by deleting and recreating.
* There is only one google coloud storage namespaces, which means every bucket must have a unique name accross the entire google cloud storage namespace.
* objects names must be unique only within a given bucket.

Object:

* object is file that you want to store.
* can be upto 5TB
* object has data & metadata
* no limit on number of objects in buckets
* objects are immutable and you can overwrite onjects

Turbo Replication: is a cloud storage premium features degined to asynchronously replicate newly written cloud storage objects associated with any insert, rewrite, copy or compose operation-regardless of object size to a separate region within a target of 15 minutes.

---

Load Balancers: A load balancer distributes user traffic across multiple instances of your application by sending the load, load balancing reduces the risk that your applications experience performance issues.

Cloud load balancer is built on the same frontend-serving infrastructure that powers google. It supports 1 million+ queries per second with consist high performance and low latency. Traffic enters cloud load balancing throgh 80+ distinct global load balancing locations, mazimizing the distance traveled on googles fast private network backbone.

Features:

* single anycast IP address
* software - defined low balancing
* seamless autoscaling No prewarming
* layer-4(tcp/udp) and layer-7(application(http,https)) LB
* External and inetrnal LB
* Global(has only External LB) and regional LB
* Enable cloud CDN for HTTP(s) load balancing to optimize application delievery for your users with a single checkbox
* Manage ssl certification and decryption

Load Balancer can be opted on the basis of your requirement.

various aspect:

1. External vs internal LB
2. Global VS Regional
3. Premium Vs Standard Tier
4. Peoxy Vs Pass-through
5. Traffic Type
6. DDoS(distributed denial of services) protector

Types:

| EXTERNAL  | REGIONAL INTERNAL       | REGIONAL EXTERNAL            |
| --------- | ----------------------- | ---------------------------- |
| HTTP(s)   | TCP/UDP LB(pass-throgh) | TCP/UDP Network(pass-throgh) |
| Classic   | HTTP(s) LB              | HTTP(s)                      |
| TCP Proxy | TCP Proxy               |                              |
| SSL Proxy |                         |                              |

* Global Load Balancing when your backends are distributed accross multiple regions.
* Regional Load balancing when your backends are in one region or when you have juridictional compliance requirements for traffic to stay in a praticular region.
* External load balancers distribute traffic from the internet to your google cloud vpc.
* Premium tier delivers traffic on google's premium backbone. It gives high performance and low latency.
* Standard tier uses regular ISP network. It is low cost alternative for apps that don't have stric requirement. for latency & performance.
* Proxy Load Balancers terminate incoming client connections and open new connection from the LB to backends.
* Pass-throgh LB do not terminate client connections instead load-balanced packets are received by backends VMS with the packet source, destination, and if applicable port information. Unchanged connections are terminated by the backends VM's go directly to the client's not back throgh the load balancer. The term for this is direct server return.

Underlying Technology of Google Cloud Load Balancers:

1. Google Front Ends (GFES) are software defined, distributed system that are located in google points of presence(Pops) and perform global load balancing in conjuction with other systems and control plane.
2. Androme is google cloud's SDN virtualisation stack.
3. Maglev is a distributed system for network load balancing.
4. Envoy Proxy is and open-source edge and service proxy designed for cloud-native applications.

---

**IAM - Identity(user/person) Access(Role) Management(Resources)**

* IAM lets you grant granular access to specific google cloud resources and helps to prevent access to other resources.
* IAM lets you adopt the security principle of least priviledged which states that nobody should have more permissions than they actually need.
* With IAM, you manage access control by defining who('Identity') has what access(role) for which resources.
* IAM permission to access a resource is n9it granted directly to the end user. Instead permissions are grouped into roles, and roles are granted to authenticated principles(members).
* Policy defines and enforces what roles are granted to which principles.Each allow policy is attached to a resource.(Member+role)
* When an authenticated principla attempts to access a resource IAM checks the resource's allow policy to determine whether the action is permitted.

Features:

* Lets you authrozie who can take specific action on resources to give you full control and visibilty on your google cloud service centrally.
* Permissions are represnetd in the form of service.resources.verb
* can map job functions into groups and roles.
* with IAM users only get access to what they need to get the job done.
* Cloud IAM enables you to grant access to cloud resources at fine-grined levels, well beyond project level access.

PARTS of IAM:

1. Principals/Members: A pricinple can be
   * google account
   * service account
   * google group
   * google workspace
   * cloud identity domain
   * authenticated users
   * all user
2. Role: A role is a collection of permissions. Permission is determine what operations are allowed on a resource.When you grant a role to a principal, you grant all the permissions that the role contains.
3. Policy: Policy is a collection of role bindings that bind one or more principals to individual roles.When you want to define who has what type of access on a resource you create allow policy and attach resource.

* Google Account: Any email address that's associated with a google account can be an identity, including gmail.com ot other domains.
* Service Account: A service account is an account for an application or compute workload instead of an individual end user.
* Google Group: is a collection of google accounts and service accounts. Every google group has a unique email address that's associated with the group. You can grant and change access controls for a whole group at once instead of granting or changing access controls. One at a time for individual users or service accounts.
* Google workspace account: Google workspace accounts are associated with your organisation internet domain name, such as example.com.When you create a google account for a new user such as username@gmail.com, that google account is added to the virtual group for your google workspace account.
* Cloud Identity Domain: is like a google workspace account becaus it represents a virtual group of all google accounts in an organization.However cloud identity domain users don't have access to google workspace applications and features.
* All Authenticated User: The value all authtucated users is a special identifier the represent all service accounts and all users on the internet who have authenticated with a google account.This identifier includes accounts that are not connected to google workspace. Account or cloud identity domain such as personal gmail accounts. User who are not authenticated such as anonymous visitors are not included.
* All Users: The value all users is a special identifier that represents anyone who is on the internet including authenticated and unauthenticated users.

Roles:

* A role contains a set of permissions that allows you to perform specific actions on google cloud resources.
* you don't directly grat users permissions in IAM. Instead you grant them roles, which bundle one or more permissions.
* To make permissions available to member including users, group and service accounts you grant roles to the members.

Types of roles:

1. Basic/Primitive Roles:

| Owner                            | Editor             | Viewer    | Billing Admin                | Browser                           |
| -------------------------------- | ------------------ | --------- | ---------------------------- | --------------------------------- |
| Super user at<br />project level | Modify codes       | Read only | Manage Billing               | kind of viwer with limited access |
| Add or remove<br />members       | Deploy apps        |           | Add or remove administartors |                                   |
| Delete & create projects         | Configure service  |           |                              |                                   |
| Setup Billing for project        | Stop start service |           |                              |                                   |

2. Predifined Roles:
   * Provides granular access for a specific service and is managed and defined by google cloud.
   * Prevents unwanted access to othe resources
   * Google is responsible for updating and adding permissions as necessary
   * You can grant multiple roles to the same user
3. Custome Roles
   * provide granular access according to a user defined list of permissions.
   * you can create a custom IAM role with one or more permissions and then grant that custom role to users or groups
   * custom roles are not maintained by google
   * You can grant multiple roles to a user or a group

**Policy(principle+role+condition) :** You cant grant roles to users by creating an allow policy which is a collection of statements that define who has what tyep of access.

* A policy is a collection of bindings audit configuration and metadata.
* A binding associates one or more members with a single role and any context-specific conditions that change how and when the role is granted.
* Each binding includes that following fields
* A member known as an identity or principla can be a
  * user account
  * service account
  * google group
  * domain
* A role which is name collection of permissions that grant access to perform actions on google cloud resources
* A condition which is a logical expression that further constraints the role binding based on attributes about the request such as its origin the target resource etc.

Service Accounts:

* A service account is a special kind of account used by an application or a vitual machine not a person.
* Application use service accounts to make authorized API calls, authorized as either
  * the service account itself
  * as google workspace
  * as cloud identity users through domain
  * wide delegation
* A service account is identified by its email address, which is unique to the account.
* Each service account is associated with two sets of public/private RSA key pairs used to authenticate to google.

Types of Service Accounts:

1. Default service account
2. user-managed service account

A service account is also a resource with IAM policies attached to it, which means you can define who can use the account and who can perform specific actions on the service account.0

---

BigQuery: BigQuery is a cloud-native data warehouse that handles petabyte-scale analysis using standard SQL. It enables analysts, data scientists, and developers to run fast SQL queries on vast amounts of data.

Key features include:

* Serverless architecture — no infrastructure to manage
* Real-time analysis of streaming data
* In-memory BI Engine for interactive analysis
* Integrated machine learning for predictive insights
* Geospatial analytics and visualization
* Granular access controls and encryption

Architecture:

1. Capacitor - columnar format: store data in columnar storage format called capacitor allows BQ to store and efficiently uery semi-structured data with neseted and repeated fields.
2. colossus - storage: distributed file system is designed to be reliable and fault-tolerant.replaced GFS and capable of handling cluster-wide replication recovery from disk crashes and distributed management.
3. Dremel - execution engine: scalable, interactive ad-hoc query system for analysis of large scale read only nested data.

* Root Node:
  * reads metadata from tables
  * The root server is responsible for communication between the client and mixers
* Inetrmediate Nodes(mixer):
  * performs query optimization and re-writes the query to include horizontal partitions of the table(shards), partial aggregation and filtering.
* Leaf Nodes
  * perform the heavy lifting of reading the data from colossus and performing filters and final aggregeation
  * in a typical dremel tree, there are hundreds or thousands of leaf nodes.
  * each node provides execution threads(slots), which BQ automatically calculates for each query based on its size and complexity.

Execution:

1. user submits a query to BQ ex: SELECT count(*) from mytable where timestamp > '2021-01-01';
2. query received by root node of dremel serving tree, which is starting point of query execution.
3. root nodes route the query to intermediate nodes(mixers) of the serving tree.These nodes perform query optimization and rewrite the query to include horizontal partitions of the table and partial aggregations and filtering.
4. In this ex, query optimizer might decide to pation the table based on timestamp and include partitions that have timestamp greate than '2021-01-01'
5. intermediate nodes than send ther rewritten query to leaf nodes for execution.Leaf node read the relevant partitions of the table from colossus and perform the filters and final aggregation specified in the query.
6. in this ex, leaf node would count the number of rows in the partitions that have timestap greate than and return the result to intermediate nodes.
7. Intermediate nodes than pass the result back up to serving tree to the root node which result final query such as "count(*) = 1000000" to the user.

Big Query Time Travel:(ex: avenger endgame)

In bigquery time travel is used to access historical data for analysis and troubleshooting.This means that you can query data that was stored, updated, or deleted in the past.

You can set the duration of the time travel window, from a **minimum of two** days to a  **maximum of seven days** . Seven days is the  **default** .You can query a table’s historical data from any point in time within the time travel window by using a clause SYSTEM_TIMEASOF TIMESTAMP_SUB.

**Note:** To restore data from a deleted table, you need to have the admin role on the corresponding table.

How to Enable:

1. In the **Explorer** panel, expand your project and select a dataset.
2. Expand the **Actions** option and click  **Open** .
3. In the **Details** panel, click  **Edit details** .
4. Expand  **Advanced options** , then select the **Time travel window** to use.
5. Click  **Save** .

benefits:

* Troubleshoot problems with historical data.
* Recover data that was accidentally deleted.
* Analyze data trends over time.
* Compare data from different points in time.

**What is fail-safe?**

What is your critical data deleted before 7 days and now you want to restore it???? Again here Google came to our rescue , BigQuery provides a **fail-safe** period.During the fail-safe period, deleted data is automatically retained for an additional seven days after the time travel window, so that the data is available for emergency recovery. Data is recoverable at the table level. The fail-safe period is not configurable. You can’t query or directly recover data in fail-safe storage. To recover data from fail-safe storage, contact Cloud customer support.

**How to work with Arrays and Structs in Google BigQuery:**

Arrays: ike in any other language, are a collection of elements of the same data type. **address_history: [“current”, “previous”, “birth”]**

Structs and how are they used in BigQuery: A struct is a data type that has attributes in key-value pairs, just like a dictionary in Python.

Within each record, multiple attributes have their own values. These attributes can either be referred to as keys or *Struct* columns.

> id:”1",
> name:”abc”,
> age:”20",
> **address_history: {
> “status”:”current”,
> “address”:”London”,
> “postcode”:”ABC123D”
> }  **

What are Array of Structs and how can we use them in BigQuery: if we want to store multiple *Structs* against each key/ID, *Array of Structs* is the option. 

For example: Address_history is an *Array* column having 3 {} *Structs* inside [] .

> id:”1",
> name:”abc”,
> age:”20",
> **address_history: [
> { “status”:”current”, “address”:”London”, “postcode”:”ABC123D” },
> { “status”:”previous”, “address”:”New Delhi”, “postcode”:”738497" },
> { “status”:”birth”, “address”:”New York”, “postcode”:”SHI747H” }
> ]**
>

How do I know by looking at the schema if it is Array/Struct/Array of Structs:

Array -> REPEATED (schema)

Struct -> RECORD (for selecting one value we use dot) with Nullable mode

Array of Structs ->RECORD | REPEATED (mode)

**What are partitions and clusters?**

Partitioning and clustering are two very effective techniques to minimize query costs and increase performance (using fewer resources while improving speed).

The idea behind these techniques is to limit the amount of data that needs to be read when running a query.


**Partitions:** **Table partitioning** is a technique for splitting large tables into smaller ones.BigQuery will store separately the different partitions at a physical level (meaning the data will be stored on different servers).

You can create a partitioned table based on a column, also known as a  **partitioning key** . In BigQuery, you can partition your table using different keys:

* **Time-unit column** : Tables are partitioned based on a time value such as timestamps or dates.
* **Ingestion time** : Tables are partitioned based on the timestamp when BigQuery ingests the data.
* **Integer range** : Tables are partitioned based on a number.

BigQuery has  **a limit of 4,000 partitions per table** .

**Clusters:** Clusters will allow BigQuery to keep data that is similar closer together, allowing a query to scan fewer data. Based on the values in the column you chose for clustering, BigQuery will automatically sort these values and also decide on how to store them in optimal storage blocks.

BigQuery has  **a limit of 4 cluster columns per table** .

**Clustering Benefits:**

* Clustering provides granularity beyond what partitioning can offer.
* Ideal for situations where the number of values in a column or group of columns is large (cardinality) and exceeds partitioning limitations.
* Useful when the partitioning strategy results in an excessive number of partitions beyond the 4000 limit.
* Appropriate when the partitioning strategy leads to frequent modifications of partitions, which can be costly.

**Partitioning Benefits:**

* Partitioning offers known cost benefits upfront, making it suitable for managing query costs effectively.
* Excellent when you need to aggregate or filter data based on a single column.
* Allows for partition-level management, including creating, deleting, and moving partitions, which is not feasible with clustering.

Slot : A BigQuery slot is  **a virtual CPU used by BigQuery to execute SQL queries** .

---

Big Query

Session user

16 nested views is the limit

smart tuning

materialized view

partioned by how many type

wildcard tables

structured array in big qury how to query them.

slot

clustering vs partioning

Time Travel in big query

architecture
