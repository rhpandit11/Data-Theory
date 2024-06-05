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
