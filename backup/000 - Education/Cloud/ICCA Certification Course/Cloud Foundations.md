# Cloud Basics
#### Topics

> Introduction
> Cloud Management
> Cloud Services
> Cloud Providers

#### Learning Objectives

-  Define what is meant by the "cloud"
-  Explain why organizations are moving workloads to the cloud
-  Identify services that are provided in the cloud
-  List the major cloud providers

#### What is the Cloud?
* Cloud Architecture
* Types of Cloud Services
*  Accessing Cloud Services
*  Demo: Why I love the Cloud

**On-Premises Information Systems Architecture**
1. Workload
2. Services - MongoDB, MySQL
3. Virtual Machine - Windows, Linux Variants
4. Virtualization
	1. Platform Maintenance Licensing
5. Physical Infrastructure
	1. Power, Network, Racks, Storage
6. Physical Facility 
	1.  Cost of Space, Physical Security, Personnel

**Cloud Architecture**
> 'There is no cloud, you're just using someone else's computer'

Cloud Architecture looks the same, except it removes:
4. Virtualization
5. Physical Infrastructure
6. Physical Facility

It does this by offloading the cost and equipment of this onto the cloud provider.

Cloud Architecture adds a **management plane**
> this is the interface that the client interacts with the cloud service

**Types of Cloud Services**

> Workload
> Services
> Virtual Machine

**Infrastructure as a Service** - Virtual Machine - Most Control, Harder Admin
> Managing your own virtual machines
> Using the cloud as a virtual machine host

**Platform as a Service** - Services - Medium Control, Medium Admin
> Hosting a database or web server
> Allows code to be deployed directly to the cloud
> Give me the platform, and I'll put the workload on it

**Software as a Service** - Workload - Least Control, Easiest Admin
> The cloud provider manages the entire workload
> Google GSuite (Docs, Sheets, etc. ), Microsoft 365, Salesforce

The lines between all of these cloud service types are often blurred, and often used together or interchangeably. 
-  Lines between them are not as solid as they seem.

#### Accessing Cloud Services

> To access the cloud from on-prem devices:
> 	-  Public endpoints, over the internet
> 		-  Not as secure
> 	 - VPN Tunnels
> 	 - Private circuit communication
> 	 	- Costs more, but more privacy

Treat the cloud just like another Wide Area Network (WAN)

#### Who are the Cloud Providers?

> Cloud Market
> AWS
> Azure
> Google Cloud Platform
> Other Cloud Providers

Amazon Web Services is the #1 Cloud Platform currently
Microsoft Azure is the #2
Google Cloud Platform is #3
Alibaba and Tencent are also large cloud providers, especially in China

-  Cloud platform will grow significantly in the future. ~823 billion dollar (US)

**Amazon Web Services**

> First and biggest cloud project and service
> 18 global regions
> 175 products and services
> 190 countries

**Microsoft Azure**

> Available since 2010
> 169 services
> 300k customers
> 31 geographies
> 57 regions

**Google Cloud Platform**

> Launched in 2010
> Over 90 services
> Unknown userbase
> Heavy investment from Google into the future

**Other Cloud Providers**

> 20% of the market
> Tencent and Alibaba in China
> IBM and Oracle
> Digital Ocean - developers like this one
> Private Cloud providers

#### Why Choose the Cloud?

> Cloud Economics
> CapEx vs. OpEx
> Consumption-based Spending
> Functional Advantages
> Also, Maybe Not

**Cloud Economics**

> Eventually, on-prem or proprietary data centers will physically run out of room for more storage disks
> 	-  Storage is often the driving factor for companies moving to cloud infrastructure

> Compute is a lot more variable than storage, typically undergoing a surge then relief
> 	- Cloud services allow for additional computing power on demand, on a need basis
> 	- If your demand goes up, the cloud has elasticity to handle it
> 	- If your computing demands go down, the cloud will scale along with it, meaning expensive computing power is not underutilized

**Capital Expense vs. Operational Expense**

> up-front infrastructure cost vs. long term monthly expenditure

-  On-premises capacity extension = capital expense
	-  purchase equipment and licensing up front
	-  depreciate and replace equipment
	-  renew licenses
-  Cloud-base capacity expansion = operational expense
	- billed monthly for what is used
	- no equipment purchase
	- may or may not require license purchase
		- cloud does not eliminate license purchases
		- web server software, accounting software, database software
- Capacity reduction
	- On-premises - possibly sell excess equipment
	- Cloud - reduce monthly cost

**Computation-Based Spending**

-  Capacity-based spending
	- On-premises resources
	- Some cloud resources = virtual machines
-  Consumption-based spending
	- Pay only for what is used
	- Functions, Lambda
	- Services
	- Storage

**Functional Advantages**

-  Provision environments in minutes rather than days, weeks or months
	- No capital equipment purchases
	- Streamlined provisioning process
- Built-in access and allocation management
- Reduced administrative overhead

**Also, Maybe Not**

-  Existing investment
	- Moving millions of dollar of invested on prem equipment doesn't always make sense
- On-going operational expenses
	- Not properly accounting for storage costs
- Data fencing
	- Data sovereignty, keeping the data in your own environment
- Regulatory compliance
	- Sensitive data needs to be protected, cloud service security is often out of the organization's control

# Cloud Management

#### Managing Cloud Resources
> Cloud management tools
> Web-based Cloud Management
> Command Line Cloud Management
> Cloud API
> Demo: Managing Clouds

**Cloud Management Tools**

-  Web Based Tools
-  Command Line Interface
	- Linux way of doing things
	- PowerShell command line options
- Rest API
	- Standard interface allows you to have your own applications to interact with the cloud services
	- Google is very adamant about having this option
	- Third parties can create their own management tools

**Web-based Cloud Management**

-  Azure calls them portals
-  AWS and GCP call them consoles

> Idea is to make the web interfaces easy to use

**Command Line Interface**

> write and save scripts to use for management

-  AWS 
	- AWS CLI
	- PowerShell
- Azure
	- Azure CLI
	- Azure PowerShell
- Google Cloud
	- Google Cloud SDK
	- Component Management (kubectl)
	- Cloud Tools for PowerShell
- Cloud Shell
	 Command Line tools can be installed on local machines
	 Can also be managed in the cloud

**Cloud API (REST API)**
> if you're a developer or looking for lowest amount of interaction with cloud providers, this is the option to choose and develop

#### Demo: Managing Clouds

> Use web manager to control access
> Use CLI to list available virtual machines

#### Cloud Cost Management

> Cloud Pricing Models
> Demo: Calculate Resource Costs
> Cloud Billing
> Cost Monitoring
> Cost Optimization
> Demo: Optimize Storage Cost

**Capacity vs. Consumption**

-  I want this much storage, CPU and memory
	-  Pay a cost per/hour for the service
- Storage is consumption based

> It can be a lot easier to budget for capacity based billing
> Here's the capacity I want, this is how much I will pay for it.

> Capacity can be harder to budget for since there is slightly less controlled compared to Consumption

The highest level of monitoring and auditing that's available typically comes with an additional charge
-  Per instance basis for an EC2 in cloudwatch, for example

**Data Transfer**

> Egress costs

If you want to exfiltrate data from the cloud, you will have to pay a cost for that data transfer

**Cloud Billing**

-  Billing Entity
-  Billing Cycle
-  Billing management
-  Billing rate
-  Marketplace billing
	-  In addition to standard billing, using a partner service provided by the cloud provider (like a Linux distro, for example), you may have to pay that 3rd party in addition to the normal monthly rate

**Cost Monitoring**

-  Budgets
	- Providers allow you to set budgets and come with alerts before billing cycles
-  Alerts
	- Alerts can be set up to notify organization before billing commences
-  Monitoring Tools
-  3rd Party

**Cost Optimization**

-  Agents
	- Azure advisors
	- AWS cost anomaly detection
	- Google recommender
- Sizing
	- hundreds of different sizes of virtual machines
	- pick the right one you need
- Autoscale
	- react to the conditions, like heavy load and scale up
	- scale back down when it returns to normal load
- "Serverless" options
	- requires rearchitecting your applications
- Long-term commitments
	- Bulk discounts
	- committing to services for certain time periods can significantly lower the costs

### Cloud Support & SLAs

> One of the most critical considerations when moving to the cloud is that you are putting your entire workload and majority of resources onto the cloud, in someone else's hands.

- **Cloud Resource Responsibility**
- **Cloud SLAs**
- **Demo: Cloud SLAs**
- **Cloud Support**
- **Demo: Cloud Support**

**Cloud Resource Responsibility**

-  Data vs. Management 

	-   Workload, Services and Virtual Machine are on the client to manage responsibility for
	-   Management Plane, Physical Infrastructure, and Physical Facility are maintained by the cloud provider

**Cloud SLAs**

-  AWS
	-  Baseline EC2 - 99.99% uptime
	-  AWS Service Level Agreements
-  Azure
	- Baseline virtual environment - 99.99% uptime
	- Service Level Agreements - Home | Microsoft Azure
- Google Cloud Platform
	- Baseline virtual machine - 99.99% uptime
	- Google Cloud Platform Service Level Agreements

> **Service Credits**
> Each provider has a credit system that will provide a refund if the cloud platform become unavailable for a certain percentage of uptime.

**Cloud Support**
> Priced packages for customer support from the cloud provider, with more support options based on the size of the organization and their needs
-  AWS
	- Basic
	- Developer
	- Business
	- Enterprise
- Azure
	- Basic
	- Developer
	- Standard
	- Professional Direct
- Google
	- Basic
	- Developer
	- Business
	- Enterprise
# Cloud Infrastructure Services

> Companies that are new to the cloud or have recently moved into the cloud are often only using a fraction of the fundamental services offered by the big three cloud providers.

- It's consistent with what they already know, concepts remain consistent

**In this Section:**
- *Infrastructure as a Service*
- *Cloud Networking*
- *Cloud Compute*
- *Cloud Storage*
- **Demo: Iaas**

#### Infrastructure as a Service

Provider offers Virtualization, Physical Infrastructure and Physical Facility

Client uses the Infrastructure for Virtual Machines, Services and Workload

**Virtual Networks (Cloud Networking)**

>Within the virtual network are typically subnets
>	Within the subnets are IP address ranges
>	Access Control, Network Security Groups and Access Control Lists (ACL)
>	Routing
>	DNS Settings
>	Certain Security Settings

In Azure and AWS you set the IP range at the VNet/VPC level. 
In Google Cloud, you set it at the subnet level.

> Gateways are set up at the VNet/VPC level as VPN gateways or Private Circuit Gateways

> Load Balancers can be set up at the VNet/VPC level as well

> Basic firewalls are available for the VNet/VPC as well

On-premises networking is must more involved and demanding than setting up a cloud network.

**Virtual Machines/EC2 (Cloud Compute)**

***Two Key Characteristics:***
> Size of the instance
> 	Series & a Size
> 	Typically defined in *number of CPUs* and *amount of memory*
> Image that the VM is based on
> 	IAM - Image in AWS
> 	Contains the OS (Windows or Linux)
> 	Additional software 
> 		(LAMP Stack)
> 	Custom Images 
> 		Useful for having to install a large number of instances
> 		Create new instances based on the custom image
> 		Useful for large enterprises

*Security and Access* can be defined on the VM
- Main user accounts
- Passwords
- Key pairs for access
- Networking rules to allow access

*Burstable* virtual machines allow you to build up credits when the machine is running at a lower level, then spend those accrued credits when the demand and level increases.
- This results in more performance

**Cloud Storage**

> If you have infrastructure, you have storage

There is the ability to use storage outside of the Virtual Machines

*AWS*
- S3 Buckets
	- Pure storage
- Elastic File Services (EFS)
	- File server without a server
- Elastic Block Services (EBS)
	- Used for storing virtual drives for EC2
*Azure*
- Storage Account
- Managed Disks
	- Used by VMs
*Google Cloud*
- Storage Buckets
- Compute Engine Disks and Images
	- Used by VMs

# Cloud Platform Services

> When moving to a cloud environment, a few things are the key factors:
	1. Cost
	2. Security
	3. Availability
	4. Ease

In this section:

- **Platform as A Service**
- **Application Hosting**
- **Data Hosting**
- **Other Services**
- Demo: Application Hosting

*Platform as a Service* really means that the provider is offering everything except the workload that will be placed onto the platform
- The workload is at the client's discretion

So, that means that the cloud provider is covering:

- Services
- Virtual machines
- Management Plane
- Virtualization
- Physical Infrastructure
- Physical Facility

> Allows the client to focus solely on the workload that will be placed on the cloud, the cloud provider handles the rest.

| AWS                                                                               | Azure                                                                         | Google Cloud                                                              |
| --------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| Lightsail, Batch, Lambda, Beanstalk                                               | Web Apps, API Apps, Function Apps, Logic Apps, Batch                          | App Engine, Cloud Functions, Workflows                                    |
| Elastic Container Service, Elastic Container Registry, Elastic Kubernetes Service | Azure Container Registry, Azure Container Instances, Azure Container Services | Cloud Run, Container Registry, Kubernetes Engine, Cloud Build, Cloud Code |
> Containers represent cross cloud functionality and cloud agnostic hosting. 

**Data Hosting**

| AWS                                                                                                | Azure                                                                                                  | Google Cloud                                               |
| -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------- |
| Amazon Aurora, Amazon RDS                                                                          | Azure SQL Database, Azure Database for PostreSQL, Azure Database for MySQL, Azure Database for MariaDB | Cloud Spanner, Cloud SQL                                   |
| Amazon Redshift, DynamoDB, Amazon Elasticache, Amazon DocumentDB, Amazon Keyspaces, Amazon Neptune | Cosmos DB, Azure Synapse, Azure Redis Cache                                                            | Cloud Bigtable, Firestore, Bigquery, Firebase, Memorystore |
> Relational and Non-relational database hosting in the cloud
> 	Every single option comes with different pricing

**Other Services**

- Authentication & Identity services
- Security services
- Media services
- Migration services
	- helps you move existing workload into the cloud provider's services
- Archiving services
- Machine learning
- Cognitive services
- IoT services
- More...

# Cloud Application Services

> Most of us now use cloud applications every day.

In this section:

- *Software as a Service*
- *SalesForce*
- *Microsoft 365*
- *G Suite*
- *Collaboration*
- *Others*
- *Demo: Cloud Productivity*

*Software as a Service* encompasses:

- Workload
- Services
- Virtual Machines
- Management Plan
- Virtualization
- Physical Infrastructure
- Physical Facility

> So, pretty much the entire cloud diagram. 
> You are not building it, you are renting it. 

You can take the software as a service and use it exactly as is.
- Or you can customize it through coding or configuration

**SalesForce**

- The leader in customer relations management (CRM)
- Depending on approach, the biggest SaaS provider
- Integration through Lightning platform
- Collaboration, coaching and training management
- Online marketplace

**Microsoft 365**

- Productivity Suite
	- Email
	- Collaboration
	- File management
- Online and offline versions of cloud products
- CRM and business management through Dynamics 365
- Low-code and no-code customization

**G Suite**

- Productivity Suite
	- Email
	- Collaboration
	- File management
- Highly Integrated

**Collaboration**

- Slack
- Zoom
- Microsoft Teams
- Google
- Others

**Others**

- Customer relations management
- Enterprise resource planning
- Content management services
- Accounting
- Business continuity
- Many more

> You are paying a subscription to just go and use a service, with little to no workload on on-prem infrastructure.

# Scalability and Availability

In this section:

- *Regional Computing*
- *Cloud Scale*
- *Cloud Availability*
- Demo: Cloud Scale

> All of the major providers will allow **data fencing**, or allowing the client to choose where their resources are located.

Allows clients to deploy a workload anywhere in the world very quickly and effectively.

#### Cloud Scale

>The amount of compute, storage and networking available to the consumer is massive with all of the data centers located globally.

The cloud gives organizations the ability to seamlessly and easily add more computing power or storage or networking without having to buy the physical assets. 

Most cloud providers have a "pay for what you use" model and allow for elasticity options and scalability options

#### Cloud Availability

> Cloud providers will provide for global availability

They also allow for datacenters to pick up workloads if the main data center becomes unavailable.

If you can't access a certain region, they'll just have you go to another region.

#### Tour of Azure

Top level: **Subscription**

Inside the subscription, there are **resource groups**

VMs, Databases and Storage are the **resources**

**Azure AD**

> Active Directory for Azure platform

Users, Groups and Service Principles are assigned roles in the **resources**

#### Tour of AWS

Starting Point: **Account**, or you can create an **Organization** to manage multiple accounts.
- email address used becomes root or primary user

From there: **IAM Users**

Below the IAM Users: **Resources**
- EC2, Databases, Storage etc.
























