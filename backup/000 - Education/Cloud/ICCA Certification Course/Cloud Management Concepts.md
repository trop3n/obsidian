### Learning Objectives:

> Describe the unique aspects of managing resources in the cloud
> Identify the cloud resource management tasks
> Explain the fundamentals of cloud access control

#### Cloud Shared Responsibility Model

- Shared Responsibility
- Management Responsibility
- Security Responsibility
- Resiliency Responsibility
- Workload Responsibility

| Workload                |
| ----------------------- |
| Services                |
| Virtual Machine         |
| Management Plane        |
| Virtualization          |
| Physical Infrastructure |
| Physical Facility       |
> You are always responsible for managing your Azure AD tenant, and access your subscription (everything above the management plane)

> The cloud provider is always responsible for managing and securing the facility, infrastructure, virtualization, and cloud management plane (everything below the management plane)

#### Management Responsibility

**Infrastructure as a service**
You are responsible for managing the virtual machine (operating system) and above
- IaaS includes everything above the management plane

**Platform as a Service**
You are responsible for the workload only 

**Software as a Service**
The provider is responsible for managing the full stack. You may be responsible for managing customizations. You are still responsible for managing usage and adhering to good practices and compliance.

#### Security Responsibility

**Provider Responsibility**
- Physical security
- Infrastructure security
- Platform security
- Identity system security
- Standards compliance

**Customer Responsibility**
- Identity security
- Data security
- Application security
- Standards compliance

> **Standards Compliance** is always a *shared responsibility* between customer and provider. 

#### Resiliency Responsibility

- 99.99% uptime service level agreement (SLA)
- Build redundancy to support availability
- Build resiliency into applications

#### Workload Responsibility

- Workloads still fail in the cloud
- SaaS out of the box
	- Workload failures are responsibility of provider
	- No customization
- Good software lifecycle management practices are critical
	- Just as important in the cloud as on-premises

> The rules you have for building good software doesn't change just because you moved into the cloud.

# Managing Cloud Resources

- Provisioning Resources
- Configuring Resources
- Maintaining Resources
- Monitoring Resources
- Change Management

**REST API** is in really, an interface for services based on web standards.

#### Maintaining Resources

- Maintaining code base
- Maintaining data
- Maintaining security

> Monitoring resources is critical in the cloud

Particularly, spending is important to monitor, before the IT director gets mad at you for racking up a bill because you forgot about a service. 

#### Change Management

- It is easy to change things in the cloud
- Governance is critical in the cloud
	- Since the cloud makes it easy to do things, which means people can do the wrong things easily
	- Access rights, policies are set correctly
- Tools are available for managing change - platform specific and vendor neutral

# Monitoring and Alerts

- Cloud Monitoring
- Unified Monitoring
- Proactive Resource Management

#### Cloud Monitoring

- Resource Monitoring
- System Monitoring
	- Azure Monitor
	- AWS CloudWatch
	- Google Cloud Monitoring

> Give you a framework to view what's going on

- Disk usage
- Network usage
- Disk bytes
- CPU (average)

#### Unified Monitoring

- Nagios
- Splunk
- PRTG

> Third-party monitoring tools

**Proactive Resource Management**

- Cloud Automation
- Cloud Alerting

> What is something happens and someone doesn't happen to be monitoring?
> 	Alerting and automation come into play here
> 	Error conditions, budget conditions etc. can all trigger an alert to notify the customer
> 	Automation may autoscale for example, if certain conditions are met

You have a built in capability to monitor your applications, and you need to utilize that.

Automated monitoring and alerting will save you a lot of time and money in the long run.

# Cloud Identity and Access Management

- Cloud-Based Identity
- Access Management
- Demo: Cloud Access Management
#### Cloud-Based Identity

You start out with a **Root User**. This user exists outside of whatever subscription you're using.
- Has absolute rights.
- Use with utmost caution.

**Identity Component and Resource Component**

>Identity has:
>	Users
>	Groups

>Resource has:
>	EC2, Lightsail, S3, etc.

The users and groups are assigned permissions to use the different resources.

**Access Management - Different Cloud Providers**

>Azure:
>	Users, Groups and Roles
>	Federated users

>AWS:
>	Users, Groups and Permissions
>	Federated users
>	Policies grant permissions
>		Effect (allow/deny)
>		Action
>		Resources
>		Conditions

>GCP:
>	Users, Groups, Roles, Policies
>	Federated Users
>	Policies link users to toles on resources
>		User
>		Role
>		Resource
>		Condition

#### Cloud Management and Data Planes






