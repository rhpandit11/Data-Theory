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

| EXTERNAL  | REGIONAL INTERNAL | REGIONAL EXTERNAL |
| --------- | ----------------- | ----------------- |
| HTTP(s)   | TCP/UDP LB        | TCP/UDP Network   |
| Classic   | HTTP(s) LB        | HTTP(s)           |
| TCP Proxy | TCP Proxy         |                   |
| SSL Proxy |                   |                   |
