> The shared responsibility model is a **framework for establishing who is responsible for securing different aspects of the cloud-computing environment between the cloud service provider and the customer.**

The CSP is generally tasked with the security of the underlying infrastructure, while it is on the customer to secure cloud-hosted data and applications.

CSPs are **responsible for securing data centers and all networking equipment**. 
- They also handle tasks such as patching and updating operating systems as well as ensuring the availability and reliability of the cloud services. This is known as the "security of the cloud" responsibility.

**Customer responsibilities include:**

- Setting up secure access controls
- *encrypting data in transit and at rest*
- managing user accounts and credentials
- implementing application-specific security measures

> "Security In the Cloud Responsibility"

Many organizations erroneously rely on their CSPs for data protection and application security. 
- Closing this knowledge gap is an essential step toward fulfilling cloud security obligations.

### How Shared Responsibility Varies by Service Type

> The level of a customer's shared responsibility depends on the service type: software as a service (SaaS), platform as a service (PaaS), and infrastructure as a service (IaaS)

**In the SaaS model,** CPS bear most security responsibilities. They secure the software application, including infrastructure and networks, and they are responsible for application-level security. 

- Customer's responsibilities often include *managing user access and ensuring data is protected and accounts are secure.*

**In the PaaS model**, CSPs manage infrastructure and underlying platform components, such as run-time, libraries and operating systems. 

- Customers are responsible for developing, maintaining and managing data and user access within their applications.

Of the three models, **IaaS customers** have the highest level of responsibility. The CSP secures the foundational infrastructure, including virtual machines, storage and networks - while customers secure everything built on the infrastructure, such as the operating system, runtime, applications and data.

### Customer's Cloud-Security Responsibilities

> Customers, rather than CSPs, often bear responsibility for most cloud-security incidents.


| Customer Responsibility   | Description                                                                                                                                                                                                                            |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Data protection           | Ensuring data confidentiality, integrity and availability is the customer's purview. Best practices involve implementing proper access controls, encryption and backups.                                                               |
| User Access Management    | Implement appropriate controls, enforce strong passwords, and adopt multi-factor authentication to keep user access secure                                                                                                             |
| Application Security      | Customers are accountable for securing cloud-hosted applications. Follow secure coding practices, conduct regular vulnerability assessments, and implement appropriate security controls to reduce application-level security threats. |
| Network Controls          | Firewalls, Virtual Private Networks, security groups, and other network-control configurations are essential customer responsibilities that protect cloud resources from unauthorized access.                                          |
| Compliance and Governance | Meeting regulatory requirements and implementing appropriate governance controls are also customer responsibilities. Rach industry has unique regulations and frameworks.                                                              |

### CSP's Typical Cloud Security Responsibilities

> CSP's share of responsibilities usually includes the security of infrastructure and attendant dependencies.


| CSP Responsibility              | Description                                                                                                                                                                                                                                                                                      |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Physical Security               | CSPs are responsible for securing physical access to their data centers, using tools like surveillance systems, restricted-access areas, and environmental controls.                                                                                                                             |
| Network-Infrastructure Security | Each provider is responsible for securing cloud-network infrastructure, including routers, switches and load balancers by implementing appropriate controls, such as intrusion detection and prevention systems.                                                                                 |
| Host-infrastructure security    | CSPs secure underlying host infrastructures, including servers, virtualization layers, and storage systems. They implement proper configuration, patching and security controls on these resources, update operating systems, and ensure overall availability and reliability of cloud services. |
| Compliance Certifications       | CSPs often undergo independent audits and attain certifications to demonstrate compliance with industry standards and regulations. These measures provide customers with assurances regarding their security practices.                                                                          |
### Overlapping Responsibilities

Some responsibilities are shared by both parties based on service type.

- For instance, Azure's shared responsibility model, CSPs and SaaS and PaaS customers share responsibility for securing identity and directory infrastructure.

CSPs clearly define the boundaries of responsibilities through service level agreements.

Overlaps typically exist in the following areas:

##### Operating Systems

The responsibility of choosing the appropriate OS to meet an organization's needs lies with the user. 

- If the user chooses the CSP's operating system, then they are responsible for it's security.
- If a customer brings their own OS, their organization is responsible for it's security.

##### Native vs. Third Party Tools

Providers are responsible for deploying, managing, maintaining and updating services.

Though, when deploying a third-party tool or application as a workload, the customer is charged with securing the application and its data, while the CSP's responsibility is limited to the infrastructure and virtualization layer.

##### Server-based vs. Serverless Computing

In server-based computing, the user is responsible for choosing the operating system, deploying the workload, and configuring the necessary security settings.

On the other hand, serverless or event-based computing means the user is accountable for the deployed code and user-defined security or configuration options provided by the cloud vendor.

##### Network Controls

Whether deploying their own firewall or using the provider's, customers are responsible for configuring firewall rules and ensuring proper security-standard configuration.

### Examples of Shared Responsibility Model

> Major CSPs like AWS, Azure and GCP have established their own shared responsibility models, which outline provider-customer security responsibilities.

##### AWS Shared Responsibility Model

> AWS takes responsibility for both hardware and software, including physical data centers, networks, edge locations and virtualization layers. 

- AWS also secures their managed services, such as AWS DynamoDB, RDS, Redshift, Elastic and EMR. 
- However, customers are still responsible for securing their own applications and data, and managing access controls and configurations within their AWS accounts.

##### GCP Shared Responsibility Model

> Follows a **shared responsibility and shared fate model**.
> 	GCP introduced 'shared fate' to address the challenges where they believe the shared responsibility model fell short.

- GCP secures underlying cloud infrastructures and provides add-on options that customers can leverage to discharge responsibility for securing applications and data, managing user access and permissions, configuring security settings, and implementing appropriate security measures with their projects.

##### Azure's Shared Responsibility Model

> Similar to GCP's model. Although Azure secures managed services, customers own and secure the whole stack if operating an on=premises data center.

### Challenges of the Shared Responsibility Model

Despite it's several benefits, the shared responsibility model also presents the following challenges:

|Challenge|Description|
|---|---|
|Access control|Organizations must always protect customer data. However, the shared responsibility model requires that CSPs have unguarded access to sensitive infrastructure to evaluate security posture, contradicting an organization’s exclusive access to customer data. This has pushed many organizations into implementing role-based access control (RBAC) to ensure that authorized individuals have access to perform only pre-specified duties.|
|Vagueness|There are important areas of cloud security where the model does not clearly spell out the security responsibilities of each party. For instance, cloud middleware—which sits between organizations and CSPs for cloud security posture management—requires regular updates as new vulnerabilities continue to surface and attack surfaces expand. However, many organizations are barely aware of the required frequency of updates, and this exposes them to preventable attacks. Automating the software patching process is a viable solution to combat this issue.|
|Incident management|When cyberattacks occur, identifying which party is responsible for investigation and remediation is critical. Unfortunately, the shared responsibility model does not clearly spell out the delegation of responsibility. Additionally, cyberattacks can be targeted at anyone at either party (customer or CSP), so managing the attack is often slowed down by pinpointing the source and establishing who is responsible for remediation.|
|Complexity|Organizations offering multiple services often require multiple CSPs and unifying them into a single system may be cumbersome. Moreover, the multi-tiered nature of cloud deployments often necessitates the intervention of multiple departments, adding complexity to the question of who is responsible for what. Even when CSP versus customer responsibilities are clearly spelled out, identifying departments that are responsible for securing specific aspects of the cloud may be difficult.|
### A New Vision of Shared Responsibility to Cloud Vulns

