> **Network Security** is a set of operations for *protecting data, applications, devices and systems on a connected network*. 
> 
> 	It is accepted as one of the significant domains of cybersecurity. 
> 	It focuses on system design, operation and management of the architecture/infrastructure to provide network accessibility, integrity, continuity and reliability. 

**Traffic Analysis** is a subdomain of the Network Security domain, and its primary focus is investigating the network data to identify problems and anomalies.
# Network Security and Network Data

> The essential concern of Network Security focuses on two core concepts:
> 
> **Authentication**
> **Authorization**

There are a variety of tools, technologies and approaches to ensure and measure implementations of these two key concepts and go beyond to provide continuity and reliability. 

Network security operations contain three base control levels to ensure the maximum available security management.

**Base Network Security Control Levels**:

| Physical                                                                                                                              | Technical                                                                                                                     | Administrative                                                                                                                         |
| ------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| Physical security controls prevent unauthorized physical access to networking devices, cable boards, locks and all linked components. | Data security controls prevent unauthorized access to network data, like installing tunnels and implementing security layers. | Administrative controls provide consistency in security operations like creating policies, access levels and authentication processes. |
> There are two main approaches and multiple elements under these control levels. The most common elements used in Network Security Operations are explained below.

**The Main Approaches**:

| Access Control                                                                                              | Threat Control                                                                                                                                |
| ----------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| The starting point of Network Security. It is a set of controls to ensure authentication and authorization. | Detecting and preventing anomalous/malicious activities on the network. It contains both internal (trusted) and external traffic data probes. |
##### Key Elements of Access Control

| Type                               | Description                                                                                                                                                                                                           |
| ---------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Firewall Protection**            | Controls incoming and outgoing network traffic with predetermined security rules. Designed to block suspicious/malicious traffic and application-layer threats while allowing legitimate and expected traffic.        |
| **Network Access Control (NAC)**   | Controls the devices' suitability before access to the network. Designed to verify device specifications and conditions are compliant with the predetermined profile connecting to the network.                       |
| **Identity and Access Management** | Controls and manages the asset identities and user access to data systems and resources over the network.                                                                                                             |
| **Load Balancing**                 | Controls the resource usage to distribute (based on metrics) tasks over a set of resources and improve overall data processing flow.                                                                                  |
| **Network Segmentation**           | Creates and controls network ranges and segmentation to isolate the user's access levels, group assets with common functionalities, and improve the protection of sensitive/internal devices/data in a safer network. |
| **Virtual Private Networks (VPN)** | Creates and controls encrypted communication between devices (typically for secure remote access) over the network (including communications over the internet)                                                       |
| **Zero Trust Model**               | Suggests configuring and implementing the access and permissions at a minimum level (providing access required to fulfill the assigned role). The mindset is focused on: **never trust, always verify**               |
##### Key Elements of Threat Control

| Type                                                          | Description                                                                                                                                                                                                                                                    |
| ------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Intrusion Detection and Prevention System (IDS/IPS)**       | Inspects the traffic and creates alerts (IDS) or resets the connection (IPS) when detecting an anomaly or threat.                                                                                                                                              |
| **Data Loss Prevention**                                      | Inspects the traffic (performs content inspection and contextual analysis of the data on the wire) and blocks the extraction of sensitive data.                                                                                                                |
| **Endpoint Protection**                                       | Protecting all kinds of endpoints and appliances that connect to the network by using a multi-layered approach like encryption, antivirus, antimalware, DLP, and IDS/IPS.                                                                                      |
| **Security Information and Event Management (SIEM)**          | Technology that helps threat detection, compliance, and security incident management, through available data (logs and traffic statistics) by using event and context analysis to identify anomalies, threats and vulnerabilities.                             |
| **Security Orchestration Automation and Response (SOAR)**     | Technology that helps coordinate and automates tasks between various people, tools and data within a single platform to identify anomalies, threats and vulnerabilities. It also supports vulnerability management, incident response and security operations. |
| **Network Traffic Analysis & Network Detection and Response** | Inspecting network traffic or traffic capture to identify anomalies and threats.                                                                                                                                                                               |
##### Typical Network Security Management Operation 


| Deployment                       | Configuration                        | Management                     | Monitoring                       | Maintenance           |
| -------------------------------- | ------------------------------------ | ------------------------------ | -------------------------------- | --------------------- |
| Device and Software installation | Feature Configuration                | Security Policy Implementation | System Monitoring                | Upgrades              |
| Initial Configuration            | Initial Network Access Configuration | NAT and VPN implementation     | User Activity Monitoring         | Security Upgrades     |
| Automation                       |                                      | Threat Mitigation              | Threat Monitoring                | Rule Adjustments      |
|                                  |                                      |                                | Log and Traffic Sample Capturing | License Management    |
|                                  |                                      |                                |                                  | Configuration Updates |
### Managed Security Services

> Not every organization has enough resources to create dedicated groups for specific security domains. 
> 
> There are plenty of reasons for this:
> 	- Budget
> 	- Employee Skillset
> 	- Organization size

**Managed Security Services** come up to fulfill the required effort to ensure/enhance security needs. MSS are services that have been outsourced to service providers. 

These service providers are called **Managed Security Service Providers (MSSP)**

Today, most MSSPs are time and cost effective, can be conducted in-house or outsourced, are easy to engage, and ease the management process. 

There are various elements of MSS, and the most common ones are explained below:

| Type                            | Description                                                                                                                                                                             |
| ------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Network Penetration Testing** | Assessing network security by simulating external/internal attacker techniques to breach the network.                                                                                   |
| **Vulnerability Assessment**    | Assessing network security by discovering and analysing vulnerabilities in the environment.                                                                                             |
| **Incident Response**           | An organized approach to addressing and managing a security breach. It contains a set of actions to identify, contain, and eliminate incidents.                                         |
| **Behavioral Analysis**         | An organized approach to addressing system and user behaviors, creating baselines and traffic profiles for specific patterns to detect anomalies, threats, vulnerabilities and attacks. |
# Traffic Analysis / Network Traffic Analysis

> Traffic Analysis is a method of intercepting, recording/monitoring, and analyzing network data and communication patterns to detect and respond to system health issues, network anomalies, and threats. 

The network is a *rich data source*, so traffic analysis is useful for security and operational matters.

The operational issues cover system availability checks and measuring performance, and the security issues cover anomaly and suspicious activity detection on the network.

Traffic analysis is one of the essential approaches used in network security, and it is part of multiple disciplines of network security operations listed below:

- *Network Sniffing and Packet Analysis*
- *Network Monitoring*
- *Intrusion Detection and Prevention*
- *Network Forensics*
- *Threat Hunting*

> There are two main techniques used in Traffic Analysis:

| Flow Analysis                                                                                                                                                                                  | Packet Analysis                                                                                                                                                                       |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Collecting data/evidence from the networking devices. This type of analysis aims to provide statistical results through the data summary without applying in-depth packet-level investigation. | Collecting all available network data. Applying in depth packet-level investigation (often called *Deep Packet Inspection (DPI)* to detect and block anomalous and malicious packets) |
| **Advantage:** Easy to collect and analyze.                                                                                                                                                    | **Advantage**: Provides full packet details to get the root cause of a case.                                                                                                          |
| **Challenge:** Doesn't provide full packet details to get the root cause of a case.                                                                                                            | **Challenge**: Requires time and skillset to analyze.                                                                                                                                 |
> Benefits of Traffic Analysis:

- Provides full network visibility
- Helps comprehensive baselining for asset tracking
- Helps to detect/respond to anomalies and threats

### Does the Traffic Analysis Still Matter?

> The widespread usage of security tools/services and an increasing shift to cloud computing force attackers to modify their tactics and techniques to avoid detection. 

Network data is a pure and rich data source. Even if it is encoded/encrypted, it still provides a value by pointing to an odd, weird or unexpected pattern/situation. 

Therefore, traffic analysis is still a must-have skill for any security analyst who wants to detect and responds to advanced threats.









