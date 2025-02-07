# Incident Detection, Analysis and Response

  > By the end of this course, you will have an in-depth understanding of incident response.

- Incident response lifecycle
    
- Monitor and analyze network traffic
    
- Processes and procedures during incident response
    
- Interpret logs and alerts


# Module 1: The Incident Response Lifecycle

>> Revisit NIST CSF with a focus on the:

- Incident response lifecycle
    
- Incident handlers journal
    
- Incident response teams
    
- Documentation, detection and management tools
    

Introduction to the Incident Response Lifecycle

>> Incident lifecycle frameworks provide a structure to support incident response operations. Frameworks help organizations develop a standardized approach to their incident response process, so that incidents are managed in an effective and consistent way.

  

>> In this course, we'll focus on the NIST CSF.

- Phases of the incident response lifecycle. 
    
- The five core functions of the NIST CSF are: identify, protect, detect, respond and recover. 
    

>> The NIST incident response lifecycle is another NIST framework with additional substeps dedicated to incident response. 

- Preparation
    

- Quarterly employee training
    
- Proactive environment where employees feel comfortable asking questions
    

- Detection and Analysis
    

- Identify signs of an incident
    
- Filter external emails to flag messages containing attachments such as voicemails
    
- Have incident response plan to reference
    

- Eradication and Recovery
    

- Communicate with sender to confirm the origin of the source message
    
- Provide employees with an easy way to report and contain suspicious messages
    

- Post-incident activity
    

- Update the playbook to highlight additional red flags employees should know
    
- Review processes and workflows related to permissions and adjust oversight of those permissions
    

>> The incident lifecycle isn’t a linear process. It’s a cycle, which means that steps can overlap as new discoveries are made. 

What is an Incident?

- According to NIST, an incident is an occurrence that actually or imminently jeopardizes, without lawful integrity, the confidentiality, integrity or availability of information or an information system; or constitutes a violation or imminent threat of violation of law, security policies, security procedures, or acceptable use policies. 
    

What are Events?

- An observable occurrence on a network, system or device
    
- For example, a password reset request
    

>> All security incidents are events, but not all events are incidents.

>> The Five W’s of an Incident:

- Who triggered the incident
    
- What happened
    
- When the incident took place
    
- Where the incident took place
    
- Why the incident occurred
    

Incident Handler’s Journals - journal for documentation of incidents and response

Incident Response Teams

>> A successful response to security incidents doesn’t happen in isolation. It requires a team of both security and non-security professionals working together with defined roles. 

>> Computer security incident response teams, or CSIRTs, are a specialized group of security professionals that are trained in incident management and response. 

- The goal of CSIRTs are to effectively and efficiently manage incidents, provide services and resources for response and recovery, and prevent future incidents from occurring.
    

>> CSIRTs must work cross functionally with other departments to share relevant information.

- For example, if an incident resulted in the breach of sensitive data, like financial PII, then the legal team must be consulted.
    
- Some regulatory compliance measures may require organizations to publicly disclose a security incident within a certain timeframe.
    

Roles in CSIRT:

- Security analyst
    
- Technical lead
    
- Incident coordinator
    

Roles in Response

>> National Institute of Standards and Technology (NIST) Incident Response Lifecycle consists of four phases:

- Preparation
    
- Detection and analysis
    
- Containment, Eradication and Recovery
    
- Post-incident activity
    

>> Understanding the composition of incident response teams will help you navigate an organization’s hierarchy, openly collaborate and communicate with others, and work cohesively to respond to incidents. 

Command, Control and Communication

>> A computer security incident response team is a specialized group of security professionals that are trained in incident management and response. For incident response to be effective and efficient, there must be clear command, control and communication of the situation to achieve the desired goal.

- Command refers to having the appropriate leadership and direction to oversee the response.
    
- Control refers to the ability to manage technical aspects during incident response, like coordinating resources and assigning tasks.
    
- Communication refers to the ability to keep stakeholders informed.
    

Roles in CSIRT

1. Security Analyst
    
2. Technical Lead
    
3. Incident Coordinator
    

Security Analyst

- The job of the security analyst is to continuously monitor an environment for any security threats. 
    

- Analyzing and triaging alerts
    
- Performing root-cause investigations
    
- Escalating or resolving alerts
    

- If a critical threat is identified, then analysts escalate it to the appropriate team lead, such as the technical lead. 
    

Technical Lead

- Job of the technical lead is to manage all of the technical aspects of the incident response process, such as applying software patches or updates. 
    
- They do this by first determining the root cause of the incident. Then, they create and implement the strategies for containing, eradicating and recovering from the incident. 
    
- Technical leads often collaborate with other teams to ensure their incident response priorities, such as reducing disruptions for customers or returning. 
    

  

Incident Coordinator

- Responding to an incident also requires cross-collaboration with non security personnel.
    
- CSIRTS will often consult with and leverage the expertise of members from external departments. 
    
- The job of incident coordinator is to coordinate with the relevant departments during a security incident. 
    

- By doing so, lines of communication are open and clear, and all personnel are made aware of the incident status
    

Other Roles

>> Depending on the organization, many other roles can be found in a CSIRT, including a dedicated communications lead, a legal lead, a planning lead and more.

- Teams, roles and responsibilities vary from company to company
    

Security Operations Center

>> A security operations center is an organizational unit dedicated to monitoring networks, systems and devices for security threats or attacks. Structurally, a SOC often exists as its own separate unit or within a CSIRT. 

SOC Organization

>> Composed of SOC analysts, SOC leads and SOC managers. Each role has it’s own respective responsibilities. 

>> SOC analysts are grouped into different tiers:

Tier 1 SOC Analyst

- Least experienced SOCs are known as level 1’s. They are responsible for:
    

- Monitoring, reviewing and prioritizing alerts based on criticality or severity
    
- Creating and closing alerts using ticketing systems
    
- Escalating alert tickets to Tier 2 or Tier 3
    

Tier 2 SOC Analyst

- More experienced SOC analysts, or level 2’s. Responsible for:
    

- Receiving escalated tickets from L1 and conducting deeper investigations
    
- Configuring and refining security tools
    
- Reporting to the SOC lead
    

Tier 3 SOC Analyst

- Highly experienced professionals are responsible for:
    

- Managing the operations of the team
    
- Exploring methods of detection by performing advanced detection techniques, such as malware and forensics analysis
    
- Reporting to SOC manager
    

SOC Manager

- Top of the pyramid and is responsible for:
    

- Hiring, training and evaluating the SOC team members
    
- Creating performance metrics and managing the performance of the SOC team
    
- Developing reports related to incidents
    

Other Roles

- Forensic Investigators: Commonly L2s and L3s who collect, preserve and analyze digital evidence related to security incidents to determine what happened.
    
- Threat Hunters: Threat hunters are typically L3’s who work to detect, analyze and defend against new and advanced cybersecurity threats using threat intelligence.
    

Incident Response Plans

>> When an incident occurs, incident response teams must be prepared to respond quickly, efficiently and effectively. 

Security Plans consist of three basic elements:

- Policies
    
- Standards
    
- Procedures
    

>> An incident response plan is a document that outlines the procedures to take in each step of incident response.

Elements of Incident Plans

- Incident response procedures
    
- System information
    

- Network diagrams, data flow diagrams, logging, asset inventory
    

- Other documents
    

- Contact lists, forms and templates
    

Incident Response Tools

>> As a security analyst, you won’t be using a single tool to monitor, detect and analyze events.

- Detection and management tools
    
- Documentation tools
    
- Investigative tools
    

>> Continuously expand your security toolbox to become an effective cybersecurity professional.

The Value of Documentation

Documentation is any form of recorded content that is used for a specific purpose.

- Playbooks
    
- Incident Handler Journals
    
- Policies
    
- Plans
    
- Final reports
    

Playbook is a manual that provides details about any operational action

>> As a security professional, you’ll be using and creating documentation regularly. 

- It’s essential that the documentation you use and produce is clear, consistent and accurate.
    

Word Processors are a common way to document. A few common tools are:

- Google Docs
    
- OneNote
    
- Evernote
    
- Notepad++
    

Ticketing systems like Jira are also commonly used for tracking and documenting.

Intrusion Detection Systems

>> Application that monitors system and network activity and produces alerts on possible intrusions (IDS)

  

Intrusion Prevention System

>> An application that monitors system activity for intrusions and take action to stop the activity (IPS)

IDS and IPS tools

- Snort
    
- Zeek
    
- Kismet
    
- Sagan
    
- Suricata
    

Overview of Detection Tools

>> Compare and contrast IDS and IPS systems, as well as learn about endpoint detection and response (EDR)

Why you need detection tools

>> Cybersecurity tools help organizations protect their networks and systems against unwanted and unauthorized access. 

- In order to defend against threats, you will need to know when they occur.
    

Detection Tools

>> As a security analyst, you’ll likely encounter IDS, IPS and EDR detection tools at some point, but it’s important to understand the differences between them. 

  

|   |   |   |   |
|---|---|---|---|
|Capability|IDS|IPS|EDR|
|Detects malicious activity|✔️|✔️|✔️|
|Prevents intrusions|❌|✔️|✔️|
|Logs activity|✔️|✔️|✔️|
|Generates alerts|✔️|✔️|✔️|
|Performs behavioral analysis|❌|❌|✔️|

  
  

Overview of IDS Tools

An intrusion detection system (IDS) in an application that monitors system activity and alerts on possible intrusions. An IDS provides continuous monitoring of the network events to help protect against security threats or attacks. 

- The goal of an IDS is to detect potential malicious activity and generate an alert once such activity is detected. An IDS does not stop or prevent the activity. Instead, security professionals will investigate the alert and act to stop it, if necessary. 
    

Detection Categories

>> There are four types of detection categories you should be familiar with:

1. A true positive is an alert that correctly detects the presence of an attack
    
2. A true negative is a state where there is no detection of malicious activity. This is when no malicious activity exists and no alert is triggered
    
3. A false positive is an alert that incorrectly detects the presence of a threat. This is when an IDS identifies an activity as malicious, but it isn’t. 
    

1. False positives are an inconvenience for security teams because they spend time and resources investigating an illegitimate alert.
    

5. A false negative is a state where the presence of a threat is not detected. This is when malicious activity happens but an IDS fails to detect it. 
    

1. False negatives can be dangerous because security teams are left unaware of legitimate attacks that they can be vulnerable to. 
    

Overview of IPS tools

>> Intrusion prevention systems are applications that monitor system activity for intrusive activity and take action to stop the activity.

- IPS differs from IDS because an IPS can monitor system activity to detect and alert analysts, but also takes action to prevent the activity and minimize it’s effects.
    
- Suricata, Snort, and Sagan have both IDS and IPS capabilities
    

Overview of EDR tools

>> Endpoint detection and response (EDR) is an application that monitors an endpoint for malicious activity. EDR tools are installed on endpoints. 

- Endpoints are any device connected to a network.
    

- End-user devices, like computers, smart phones, tablets etc.
    

- EDR tools monitor, record and analyze endpoint system activity to identify, alert and respond to suspicious activity. Unlike IDS and IPS, EDRs collect endpoint activity data and perform behavioral analysis to identify threat patterns happening on an endpoint. 
    
- Behavioral Analysis uses the power of machine learning and artificial intelligence to analyze system behavior to identify malicious or unusual activity. 
    
- Tools like Open EDR, Bitdefender Endpoint Detection and Response and FortiEDR are examples of EDR tools. 
    

Alert and Event Management with SIEM and SOAR tools

>> a SIEM looks at data flows between all the different systems in the network and analyzes them to provide a real-time picture of any potential threats to the network.

- It does this by ingesting a massive amount of data and categorizes this data, so that it’s easily accessible through a centralized platform.
    

SIEM Process

1. Collect and aggregate data
    

1. Data gets centralized in one place
    
2. Not all data collected by a SIEM is relevant
    

3. Normalize data
    

1. Creates consistency in log records
    

5. Analyze data
    

1. Analyze the normalized data against a ruleset to detect any possible security incidents, which then get categorized or reported as alerts for security analysts to review.
    

Security Orchestration, Automation and Response (SOAR)

>> A collection of applications, tools and workflows that uses automation to respond to security events 

- SOAR automates analysis and response to security events and incidents. SOAR can also be used to track and manage cases. 
    
- Multiple incidents form a case, and SOAR offers a way to view all of these incidents in one centralized place. 
    

Overview of SIEM Technology

>> Security Information and Event Management

- Log analysis, the process of examining logs to identify events of interest
    

SIEM Advantages

>> Tools that collect and manage security relevant data that can be used during investigations.

- SIEM tools provide awareness about the activity that occurs between devices on a network
    
- SIEM Tools have many advantages that can hello security teams effectively respond to and manage incidents:
    

- Access to event data: SIEM tools provide access to the event and activity data that happens on a network, including real-time activity. SIEM ingest all of the data on a network so that it can be accessed
    
- Monitoring, detecting and alerting: SIEM tools continuously monitor systems and networks in real-time. They then analyze the collected data using detection rules to detect malicious activity. If an activity matches the rule, an alert is generated and sent out for security teams to assess. 
    
- Log storage: act as a system for data retention, which can provide access to historical data.
    

The SIEM Process

- SIEM process consists of three critical steps:
    

1. Collect and aggregate data
    
2. Normalize data
    
3. Analyze data
    

Collect and Aggregate data

- SIEM collects data from various sources like firewalls, servers, routers and more. 
    

- This data, known as logs, contains event details like timestamps, IP addresses, and more. Logs are records of events that occur within a system. 
    

- After logs and data are collected, it gets aggregated in one centralized place. 
    

- Eliminates the need for manually reviewing and analyzing event data by accessing individual data sources. 
    

- Parsing maps data according to their fields and their corresponding values. 
    

- For example, the following log example contains fields with values. At first, it might be difficult to interpret information from this log based on its format:
    

April 3 11:01:21 server sshd[1088]: Failed password for user nuhara from 218.124.14.105 port 5023

In a parsed format, the fields and values are extracted and paired making them easier to read and interpret:

- Host = server
    
- process = sshd
    
- source_user = nuhara
    
- source_ip = 218.124.14.105
    
- source port = 5023
    

Normalize Data

>> SIEM tools collect data from many different sources. 

- This data must be transformed into a single format so that it can be easily processed by the SIEM. However, each data source is different and data can be formatted in many different ways.
    
- Normalization converts data into a standard, structured format that is easily searchable.
    

Analyze Data

>> After log data has been collected, aggregated and normalized, the SIEM must do something useful with all of the data to enable security teams to investigate threats. 

- During the final stage of the process, SIEM tools analyze the data. 
    
- Analysis is usually done with some form of detection logic such as a set of rules and conditions. 
    
- SIEMs apply these rules to the data, and if any of the log activity matches a rule, alerts are sent out to cybersecurity teams
    

SIEM Tools

>> There are many SIEM tools. These are ones commonly used in the cybersecurity industry:

- AlienVault OSSIM
    
- Chronicle
    
- Elastic
    
- Exabeam
    
- IBM QRadar Security Intelligence Platform
    
- LogRhythm
    
- Splunk
    

Module 2: Understand Network Traffic 

>> Data can get unintentionally sent and stored in insecure places, like personal email inboxes or cloud storage platforms.

- Users trust that their data is safely and securely stored, and it’s the job of cybersecurity professionals to help protect these communications in transit and at rest. 
    

Network Traffic:

- The amount of data that moves across a network
    

Network Data:

- The data that’s transmitted between devices on a network
    

>> Depending on the size of a network, there can be a huge volume of network traffic at any given moment. 

- In a large multinational organization, there may be thousands of employees sending and receiving traffic and emails at any given time. 
    
- How do you know what’s normal, what’s unusual and requires investigation as a potential security incident?
    

- By knowing what’s normal, you can immediately detect what is abnormal. 
    

Data Exfiltration

- Unauthorized transmission of data from a system
    

- Attackers use data exfiltration to steal or leak data such as usernames, passwords and intellectual property
    
- By observing network traffic, we can determine if there’s any indicators of compromise, such as large volumes of outbound traffic leaving a host
    

Maintain Awareness with Network Monitoring

>> Network monitoring is essential in maintaining situational awareness of any activity on a network. By collecting and analyzing network traffic, organizations can detect suspicious network activity. 

- Before networks can be monitored, you must know what to monitor.
    

Know Your Network

>> Network information like destination IPs, amount of data transferred, date and time etc. can be valuable for security professionals when developing a baseline of normal or expected behavior.

- A Baseline is a reference point that’s used for comparison. 
    

- By knowing the baseline of normal network behavior, you’ll be better able to identify abnormal network behavior
    

Monitor Your Network

>> Network components that can be monitored to detect malicious activity:

Flow Analysis

- Flow refers to the movement of the network comms and included info related to packets, protocols and ports. 
    

- Packets travel to ports, which receive and transmit communications.
    
- Ports are often, but not always associated with network protocols.
    

- Malicious actors can use protocols and ports that are not commonly associated to maintain communications between the compromised system and their own machine.
    

- Known as command and control (C2), techniques used by malicious actors to maintain communications with compromised systems.
    

Temporal Patterns

- Network packets contain information relating to time, which is useful in understanding time patterns. 
    
- Companies in North America experience bulk traffic flows between 0900 and 1700, which is the baseline for normal network activity. 
    

- Large amounts of traffic suddenly outside of normal hours should be investigated. 
    

Packet Payload Information

- Network packets contain components related to the transmission of the packet. This includes details like source and destination IP address, packet payload info, which is the actual data being transmitted.
    
- Organizations can monitor the payload information of packets to uncover unusual activity, such as time sensitive data transmitting outside of the network, which could indicate a possible network infiltration attack.
    

Protect Your Network

>> Organizations may deploy a network operations center (NOC), which is an organizational unit that monitors the performance of a network and responds to any network disruption, such as network outage. 

- SOC is focused on security, NOC is focused on network performance, stability and uptime.
    

>> Security analysts and network analysts monitor networks to identify any signs of potential security incidents known as indicators of compromise (IoC). 

- To protect against attacks, they must understand the environment that network communications travel through so that they can identify deviations. 
    

Network Monitoring Tools

>> Network monitoring can be automated or performed manually. Some common network monitoring tools are:

- Intrusion detection system: monitor system activity and alert on possible intrusions. IDS tools will monitor the content of packet payload to detect patterns associated with threats such as malware or phishing attempts.
    
- Network protocol analyzers: also known as packet sniffers, these tools are designed to capture and analyze data traffic within a network.
    

- Tcpdump and wireshark
    

Data Exfiltration Attacks

>> Before attackers can perform data exfiltration, they’ll need to gain initial access into a network and computer system.

- This can be done through phishing or more advanced and technical methods.
    

>> After gaining initial access into the system, an attacker won’t stop there. The goal for attackers is to maintain access in the environment for as long as possible without being detected. 

- To do this, they’ll perform a tactic called lateral movement or pivoting.
    

- They’ll spend time exploring the network with the goal of expanding and maintaining access to other systems on the network
    

- As an attacker pivots in the network, they’ll scope out valuable assets, such as sensitive data like proprietary code, personally identifiable information like names and addresses, or financial records. 
    
- Search locations like network file shares, intranet sites, code repositories and more.
    

>> After assets of value are identified, the hacker will need to collect, package and prepare the data for exfiltration outside of the organization’s network and into the attacker’s systems. 

- Attackers will often reduce the size of the data, helping them hide stolen data and bypass security controls. 
    

Defensive Measures

1. Prevent attacker access
    

1. MFA
    

3. Monitor network activity
    

1. Multiple user logins from external IP addresses
    

5. Protect assets
    

1. Asset inventory, security controls between assets
    

7. Detect and stop exfiltration
    

1. Large external uploads, file transfers etc.
    
2. Investigate and prevent: block the IP address associated with the attacker
    

Packets and Packet Captures

>> Actions performed on a network can be identified through examining network traffic flows.

Components of a Packet

1. Header
    

1. Network protocol and port
    
2. Source IP and Destination IP
    

3. Payload
    

1. Actual data being delivered
    

5. Footer
    

1. Signifies end of packet
    

Packet Capture (P-Cap)

- A file containing data packets intercepted from an interface or network
    
- Incredibly useful during an investigation
    
- Observe network interactions and start to build a storyline to determine what exactly happened. 
    

Learn More About Packet Captures

>> Three main aspects of network analysis: packets, network protocol analyzers and packet captures

  

Packets

- A data packet a basic unit of information that travels from one device to another within a network. Detecting network intrusions begins at the packet level.
    
- In cybersecurity, packets provide valuable information that helps add context to events during investigations. 
    

>> Understanding the transfer of information through packets will not only help you develop insight on network activity, it will also help you identify abnormalities and better defend networks.

- Packets contain three components: the header, payload and the footer.
    

Header

>> Packets can have several headers depending on the protocols used such as an Ethernet header, and IP header a TCP header, and more. 

- Headers provide information that’s used to route packets to their destination. 
    
- This includes information about the source and destination IP addresses, packet length, protocol, packet identification numbers, and more. 
    

Payload

>> The payload directly follows the header and contains the actual data being delivered. Think back to the example of uploading an image to a website; the payload of this packet would be the image itself.

Footer

>> Located at the end of the packet. The Ethernet protocol uses footers to provide error-checking information to determine if data has been corrupted. 

Note: most protocols, such as the Internet Protocol (IP) do not use footers.

Network Protocol Analyzers

>> Also known as packet sniffers are tools designed to capture and analyze data traffic within a network. 

Common network protocol analyzers:

- Tcpdump
    
- Wireshark
    
- TShark
    

>> Network protocol analyzers can also be used for malicious purposes, malicious actors can use network protocol analyzers to capture packets containing sensitive data, such as account login information.

How Network Protocol Analyzers Work

>> Use both software and hardware capabilities to capture network traffic and display it for security analysts to examine and analyze.

1. First, packets must be collected from the network via the network interface card (NIC). NICs, by default only listen to network traffic that’s addressed to them. 
    

1. To capture all network traffic that is sent over the network, a NIC must be switched to a mode that has access to all visible network data packets. 
    
2. In wireless setups this is often called monitoring mode, and in other systems it may be called promiscuous mode. 
    
3. A network protocol analyzer must be positioned in an appropriate network segment to access all traffic between different hosts
    

3. Network protocol analyzers collect network traffic in raw binary format. Binary format consists of 0s and 1s and is not as easy for humans to intercept. 
    

1. Packet sniffer takes the binary and converts it so that it’s displayed in a human-readable format, so analysts can easily read and understand it. 
    

Capturing packets

Packet sniffing is the practice of capturing and inspecting data packets across a network. 

A Packet Capture is a file containing data packets intercepted from an interface or network. 

- Can be viewed and further analyzed using network protocol analyzers. 
    

Note: it is often illegal to use network protocol analyzers to intercept and examine private network communications without permission.

>> P-cap files can come in many formats depending on the packet capture library that’s used. Each format has different uses and network tools may use or support specific packet capture file formats by default.

- Libpcap is a packet capture library designed to be used by Unix-like systems, like Linux and macOS. 
    
- WinPcap is an open-source packet capture library designed for devices running Windows operating systems. 
    
- Npcap is a library designed by the port scanning tool Nmap that is commonly used in Windows operating systems
    
- PCAPng is a modern file format that can simultaneously capture packets and store data. Its ability to do both explains the “ng” which stands for “next generation”
    

Reexamine the Fields of a Packet Header

>> Examination of important packet component: IP Headers

- Two different versions of IP: IPv4 and IPv6
    

Version: 

- Specifies which version of IP is being used
    

Internet Header Length (IHL)

- Specifies the length of the IP header
    

Type of Service (ToS)

- Tells us if certain packets should be treated with different care. 
    

Total Length Field 

- Identifies the length of the entire packet, including the headers and data
    

Identification, Flags and Fragmentation

- All three deal with fragmentation
    
- Fragmentation is when an IP packet gets broken up into chunks, which then get transmitted over the wire and reassembled when they arrive at their destination. These three fields specify if fragmentation has been used and how to reassemble the broken packets in the correct order. 
    

Time to Live (TTL)

- Determines how long a packet can live before it gets dropped
    
- Without this, packets could flow through routers endlessly
    

Protocol

- Specifies the protocol used by providing a value which corresponds to a protocol.
    
- TCP is represented by 6, for example
    

Header Checksum

- Stores a value called a checksum, which is used to determine if any errors have occurred in the header
    

Source Address

- Specified the source IP address and the Destination Address specified the destination IP address
    

Options

- Not required and is commonly used for network troubleshooting rather than common traffic
    
- If it’s used, the header length increases
    

End of Packet Header

- Where the packet’s data resides
    

Investigate Packet Details

>> Examine IPv4 and IPv6 headers, then explore how to use Wireshark to investigate the details of packet capture files.

Internet Protocol

>> Packets form the foundation of data exchange over a network, which means that detection begins at the packet level.

- Internet Protocol (IP) includes a set of standards use for routing and addressing data packets as they travel between devices on a network.
    

IPv4

>> Most commonly used version of IP. 

IPv6

>> IPv6 adoption has been increasing because of its large address space. There are eight fields in the header:

- Version: indicates the IP version. For Ipv6, IPv6 is used.
    
- Traffic Class: Similar to the IPv4 Type of Service field. Provides information about the packet’s priority or class to help with packet delivery
    
- Flow Label: Identifies the packets of a flow. A flow is a sequence of packets sent from a specific source.
    
- Payload Strength: this field specifies the length of the data portion of the packet.
    
- Next Header: this field indicates the type of header that follows the IPv6 header, such as TCP.
    
- Hop Limit: similar to IPv4 Time to Live. Limits how long a packet can travel in a network before it is discarded.
    
- Source Address: specifies the source address of a header.
    
- Destination Address: specifies the destination address of the receiver
    

>> Header fields contain valuable information for investigations and tools like Wireshark help to display these fields in a human-readable format.

Wireshark

>> Wireshark is an open-source network protocol analyzer. It uses a graphical user interface (GUI), which makes it easier to visualize network communications for packet analysis purposes. 

- Wireshark has many features to explore that are beyond the scope of this course. 
    
- You’ll focus on how to use basic filtering to isolate network packets so that you can find what you need.
    

Displays Filters

>> Let you apply filters to packet capture files. This is helpful when inspecting packet captures with large volumes of information.

- Display filters will help you find specific information that’s most relevant to your investigation.
    
- You can filter packets based on information such as protocols, IP addresses, ports, and virtually any other property found in a packet. 
    

Comparison Operators

>> Comparison operators can be expressed using either abbreviations or symbols. 

>> This table summarizes the different types of comparison operators you can use for display filtering.

  

|   |   |   |
|---|---|---|
|Operator Type|Symbol|Abbreviation|
|Equal|==|eq|
|Not equal|!=|ne|
|Greater than|>|gt|
|Less than|<|lt|
|Greater than or equal to|>=|ge|
|Less than or equal to|<=|le|

Pro tip: you can use comparison operators with boolean logical operators like and and or to create complex display filters. Parenthesis can also be used to group expressions to prioritize search terms.

Contains Operator

>> The contains operator is used to filter packets that contain an exact match of a string of text. 

Matches Operator

>> The matches operator is used to filter packets based on the regular expression (regex) that’s specified. Regular expression is a sequence of characters that form a pattern

Filter Toolbar

>> You can apply filters to a packet capture using Wireshark’s filter toolbar. For example, dns is the applied filter, which means Wireshark will only display packets containing the DNS protocol. 

  

Filter for Protocols

>> Protocol filtering is one of the simplest ways you can use display filters. You can simply enter the name of the protocol to filter. For example, to filter for DNS packets simply type dns in the filter toolbar. 

- dns
    
- http 
    
- ftp 
    
- ssh 
    
- arp 
    
- telnet 
    
- icmp 
    

Filter for an IP Address

>> You can use display filters to locate packets with a specific IP address.

>> Here is an example of a display filter that filters for the IP address 172.21.224.2:

ip.addr == 172.21.224.2

>> Example of filtering an IP address for source IP:

ip.src == 10.10.10.10

>> example of filtering an IP address for destination IP:

Ip.dst == 4.4.4.4

Filter for a MAC Address

>> You can also filter packets according to the Media Access Control (MAC) Address. As a refresher, a MAC address is a unique alphanumeric identifier that is assigned to each physical device on a network

eth.addr == 00:0:f4:23:18:c4

Filter for ports

>> Port filtering is used to filter packets based on port numbers. This is helpful when you want to isolate specific types of traffic. DNS traffic uses TCP or UDP port 53 so this will list traffic related to DNS queries and responses only.

udp.port == 53

tcp.port == 25

Follow Streams

>> Wireshark provides a feature that lets you filter for packets specific to a protocol and view streams. A stream or conversation is the exchange of data between devices using a protocol. Wireshark reassembles the data

Packet Inspection

>> With tcpdump, you can apply options and flags to your commands to easily filter network traffic so that you can find exactly what you’re looking for.

- You can filter for a specific IP address, protocol, or port number.
    

Overview of tcpdump

>> tcpdump is another type of network protocol analyzer (packet sniffer) that runs using a command line interface. 

What is tcpdump?

>> tcpdump is used to capture network traffic. This traffic can be saved as a packet capture (p-cap), which is a file containing data packets intercepted from an interface or network. 

- Analysts use tcpdump for a variety of reasons, from troubleshooting network issues to identifying malicious activity. 
    

Note: its common for network traffic to be encrypted, which means data is encoded and unreadable. Inspecting the network packets might require decrypting the data using the appropriate private keys. 

Capturing Packets with tcpdump

>> a Linux root user (or superuser) has elevated privileges to modify the system. You also learned that the sudo command temporarily grants elevated permissions to specific users in Linux. 

- Like many other packet sniffing tools, you’ll need administrator access to capture network traffic using tcpdump. 
    
- This means you’ll either be logged in as the root user or have the ability to use the sudo command. 
    

>> Breakdown of the tcpdump syntax for capturing packets:

sudo tcpdump [-i interface] [option(s)] [expression(s)]

- The sudo tcpdump command begins running tcpdump using elevated permissions as sudo.
    
- The -i parameter specifies the network interface to capture network traffic. You must specify a network interface to capture from to begin capturing packets. If you use -i any you’ll sniff traffic from all network interfaces on the system.
    
- The option(s) are optional and provide you with the ability to alter the execution of the command. The expression(s) are a way to further filter network traffic packets so that you can isolate network traffic. 
    

Options

>> with tcpdump, you can apply options, also known as flags, to the end of commands to filter network traffic. Short optionsa re abbreviated by a hyphen and a single character like -i. Long options are spelled out using a double hyphen like –interface. 

Note: options are case sensitive. 

Note: tcpdump options that are written using short options can be written with or without a space between the option and it’s value. For example, sudo tcpdump -i any -c 3 and sudo tcpdump -iany -c3 are equivalent commands. 

-w

>> using the -w flag, you can write or save the sniffed network packets to a packet capture file instead of just printing it out in the terminal. This is useful for referring to the saved file for further analysis. In this command, tcpdump is capturing network traffic from all network interfaces and saving it to a packet capture file named packetcapture.pcap 

sudo tcpdump -i any -w packetcapture.pcap

-r 

>> using the -r flag, you can read a packet capture file by specifying the file name as a parameter. Here is an example of a tcpdump command that reads a file called packetcapture.pcap

sudo tcpdump -r packetcapture.pcap

-v

>> this option, which stands for verbose, lets you control how much packet information you want tcpdump to print out

>> there are three levels of verbosity you can use depending on how much packet information you want tcpdump to print out. The levels are -v, -vv, -vvv. The level of verbosity increases with each added v. 

- The verbose option can be helpful if you’re looking for packet information like the details of a packet’s IP header fields. Here’s an example of a tcpdump command that reads the packetcapture.pcap file with verbosity:
    

sudo tcpdump -r packetcapture.pcap -v

  
  

-c

>> the -c option stands for count. The option lets you control how many packets tcpdump will capture. For example, specifying -c 1 will only print out one single packet, whereas -c 10 prints out 10 packets. This example using tcpdump to only capture the first three packets it sniffs from any network interface

sudo tcpdump -i any -c 3

-n

>> by default, tcpdump will perform name resolution. This means that tcpdump automatically converts IP addresses to names. It will also resolve ports to commonly associated services that use these ports. This can be problematic because tcpdump isn’t always accurate in name resolution. 

- For example, tcpdump can capture traffic from port 80 and automatically translates port 80 to HTTP in the output. This is misleading because port 80 isn’t always going to be using HTTP; it could be using a different protocol. 
    
- Name resolution uses what’s called a reverse DNS lookup. A reverse DNS lookup is a query that looks for the domain name associated with an IP address. If you perform a reverse DNS lookup on an attacker’s system, they might be alerted that you are investigating them through DNS records.
    
- Using the -n flag disables this automatic mapping of numbers to names and is considered to be best practice when sniffing or analyzing traffic. Using -n will not resolve hostnames, whereas -nn will not resolve both hostnames or ports. 
    

>> Here’s an example of a tcpdump command that reads the packetcapture.pcap file with verbosity and disables name resolution:

sudo tcpdump -r packetcapture.pcap -v -n

>> You can combine options together, like -vn. If an option accepts a parameter right after it, like -c 1, then you can’t combine other options to it.

Expressions

>> Using filter expressions in tcpdump commands is also optional, but knowing how and when to use filter expressions can be helpful during packet analysis. 

- If you want to specifically search for network traffic by protocol, you can use filter expressions to isolate network packets. You can find only IPv6 traffic using the filter ip6
    

>> you can use boolean operators like and, or or not to further filter network traffic for specific IP addresses, ports and more. 

Sudo tcpdump -r packetcapture.pcap -n ‘ip and port 80’ 

Pro tip: you can use single or double quotes to ensure that tcpdump executes all of the expressions. You can also use parenthesis to group and prioritize different expressions. Grouping expressions is helpful for complex or lengthy commands. 

Interpreting Output

>> Once you run a command to capture packets, tcpdump will print the output of the command as the sniffed packets. In the output, tcpdump prints one line of text for each packet with each line beginning with a timestamp. 

>> Here’s an example of a command and output for a single TCP packet:

sudo tcpdump -i any -v -c 1

- This command tells tcpdump to capture packets on -i any network interface. The option -v prints out the packet with detailed information and the option -c 1 prints out only one packet. 
    

1. Timestamp: the output begins with the timestamp, which starts with hours, minutes, seconds and fractions of a second
    
2. Source IP: the packet’s origin is provided by its source IP address
    
3. Source Port: this port number is where the packet originated
    
4. Destination IP: the destination IP address is where the packet is being transmitted to
    
5. Destination Port: this port number is where the packet is being transmitted to. 
    

Module 3: Incident Detection and Verification

- Investigate and verify an incident
    
- Plans and processes behind incident response
    
- Post-incident actions
    

Detection and Analysis Phase of the Lifecycle

>> Detection enables the prompt discovery of security events

- Not all events are incidents but all incidents are events
    

>> Analysis involves the investigation and validation of alerts

- Analysts must apply critical thinking and incident analysis skills to investigate and validate alerts
    

>> Challenges

- It’s impossible to detect everything
    
- Even the best monitoring and analysis tools have limitations
    
- Automated tools may not always be deployed across an entire organization due to resource restraints
    
- High volume of alerts per shift
    

- Misconfigured alert settings
    
- Too broad of configurations can lead to high number of alerts
    

Cybersecurity Incident Detection Methods

>> Introduction to different detection methods that organizations can employ to discover threats.

Methods of Detection

- Intrusion Detection Systems can detect possible intrusions and send out alerts to security analysts to investigate the suspicious activity. 
    
- Detection tools can only detect what security teams configure them to monitor. 
    

- If they aren’t properly configured, they can fail to detect suspicious activity, leaving systems vulnerable to attack.
    

Threat Hunting

- Threats evolve and attackers advance their tactics and techniques. 
    
- Automated, technology driven detection can be limited in keeping up to date with the evolving threat landscape. 
    
- Human-driven detection like threat hunting combines the power of technology with a human element to discover hidden threats left undetected by detection tools.
    

>> Threat Hunting is the proactive search for threats on a network. Security professionals use threat hunting to uncover malicious activity that was not identified by detection tools and as a way to do further analysis on detections.

- Also used to detect threats before they cause damage. 
    
- Fileless malware is difficult for detection tools to identify. 
    

- Uses sophisticated evasion techniques such as hiding in memory instead of using files or applications, allowing it to bypass traditional methods of detection like signature analysis. 
    

Threat Intelligence

>> Organizations can improve their detection capabilities by staying updated on the evolving threat landscape and understanding the relationship between their environment and malicious actors. 

- Threat intelligence is evidence based threat information that provides context about existing or emerging threats.
    

>> Threat Intelligence is gained from private or public sources like:

- Industry reports: these often include details about attacker’s tactics, techniques and procedures
    
- Government advisories: similar to industry reports, government advisories include details about attacker’s TTP. 
    
- Threat data feeds: Threat data feed provide a stream of threat-related data that can be used to protect against sophisticated attackers like advanced persistent threats. APTs are instances when a threat actor maintains unauthorized access to a system for an extended period of time. 
    

- The data is usually a list of indicators like IP addresses, domains, and file hashes. 
    

>> Organizations can leverage a threat intelligence platform (TIP) which is an application that collects, centralizes, and analyzes threat intelligence from different sources. 

Note: Threat intelligence data feeds are best used to add context to detections, and should not drive detections completely and should be assessed before applied to an organization.

Cyber Deception

>> Involves techniques that deliberately deceive malicious actors with the goal of increasing detection and improving defensive strategies. 

- Honeypots are an example of an active cyber defense mechanism that uses deception technology. Honeypots are systems or resources that are created as decoys vulnerable to attacks with the purpose of attracting potential intruders. 
    

Indicators of Compromise

>> Improve defenses and reduce the damage an incident can cause by understanding different types of indicators of compromise

- Indicators of Compromise (IoCs) are observable evidence that suggests signs of a potential security incident. IoCs chart specific pieces of evidence that are associated with an attack, like a file name associated with a type of malware. 
    

- Evidence that points to something that’s already happened, like noticing that a valuable has been stolen from a car. 
    

- Indicators of Attack (IoA) are the series of observed events that indicate a real-time incident. 
    

- IoAs focus on identifying the behavioral evidence of an attacker, including methods and intentions.
    

- Essentially, IoCs help identify the who or what of an attack after it’s taken place, while IoAs focus on finding the why and how of an ongoing or unknown attack. 
    

Note: indicators of compromise are not always a confirmation that a security incident has happened. IoCs may be the result of human error, system malfunctions, and other reasons not related to security. 

Pyramid of Pain 

>> Not all indicators of compromise are equal in the value they provide to security teams. It’s important for security professionals to understand the different types of indicators of compromise so that they can quickly and effectively detect and respond to them. 

>> The Pyramid of Pain captures the relationship between indicators of compromise and the level of difficulty that malicious actors experience when indicators of compromise are blocked by security teams. 

- Lists the different types of indicators of compromise that security professionals use to identify malicious threats. 
    

>> Each type of indicator of compromise is separated into levels of difficulty.

- These represent the “pain” levels that an attacker faces when security teams block the activity associated with the indicator of compromise. 
    

  

1. Hash values: hashes that correspond to known malicious files. These are often used to provide unique references to specific samples of malware or to files involved in an intrusion.
    
2. IP addresses: an internet protocol like 192.168.1.1
    
3. Domain Names: a web address such as [www.google.com](http://www.google.com)
    
4. Network artefacts: Observable evidence created by malicious actors on a network. 
    

1. Information found in network protocols such as User-Agent strings.
    

6. Host artefacts: observable evidence created by malicious actors on a host. A host is any device that’s connected on a network. 
    

1. The name of a file created by malware
    

8. Tools
    

1. Software that’s used by a malicious actor to achieve their goal. 
    

1. John the Ripper performing password attacks to gain access into an account
    

10. Tactics, techniques and procedures (TTPs): behavior of a malicious actor. Tactics refer to the high-level overview of their behavior. Techniques provide detailed descriptions of the behavior relating to the tactic. Procedures are highly detailed descriptions of the technique. TTPs are the hardest to detect. 
    

Analyze Indicators of Compromise with Investigative Tools

>> Explore how investigative tools can be used during an investigation to analyze suspicious indicators of compromise (IoCs) and build context around alerts.

Adding Context to Investigations

>> Identifying and blocking a single IP address associated with malicious activity does not provide a broader insight on an attack, nor does it stop a malicious actor from continuing. 

- Focusing on a single piece of evidence is like fixating on a single section of a painting: you miss out on the bigger picture
    

>> Threat Intelligence is evidence based threat information that provides context about existing or emerging threats. By accessing additional information related to IoCs, security analysts can expand their viewpoint to observe the bigger picture and construct a narrative that helps inform their response actions.

The Power of Crowdsourcing

Crowdsourcing is the practice of gathering information using public input and collaboration. Threat Intelligence platforms use crowdsourcing to collect information from the global cybersecurity community. Traditionally, an organization’s response to incidents was performed in isolation.

- A security team would receive and analyze an alert, and then work to remediate it without additional insights on how to approach it. 
    
- Without crowdsourcing, attackers can use the same attacks against multiple organizations.
    

>> Crowdsourcing allows organizations to harness the knowledge of millions of other cybersecurity professionals, including cybersecurity product vendors, government agencies, cloud providers and more. 

- Examples of information-sharing organizations include Information Sharing and Analysis Centers (ISACs) which focus on collecting and sharing sector-specific threat intelligence to companies within specific industries like energy, healthcare, and others
    
- Open-Source Intelligence (OSINT) is the collection and analysis of information from publicly available sources to generate usable intelligence. OSINT can also be used as a method to gather information related to threat actors, threats, vulnerabilities and more.
    

>> Threat intelligence data is used to improve the detection methods and techniques of security products, like detection tools or anti-virus software. 

- Once an organization detects an attack, they can immediately publish the attack details, such as malicious files, IP addresses, or URLs, to to tools like VirusTotal. 
    

VirusTotal

>> A service that allows anyone to analyze suspicious files, domains, URLs and IP addresses for malicious content. 

- Users can submit and check artifacts, like file hashes or IP addresses, to get VirusTotal reports, which provide additional information on whether an IoC is considered malicious or not, how that IoC is connected or related to IoCs in the dataset, and more. 
    

1. Detection - the detection tab provides a list of third party security vendors and their destination verdicts on an IoC. 
    

1. Vendors can list their detection verdict as malicious, suspicious, unsafe and more.
    

3. Details - the details tab provides additional information extracted from a static analysis of the IoC. 
    

1. Information like hashes, file types, file sizes, headers, creation time, and first and last submission information can be found in this tab.
    

5. Relations - Relations tab provides related IoCs that are somehow connected to an artifact, such as contacted URLs,. Domains, IP addresses and dropped files if the artifact is executable. 
    
6. Behavior - behavior tab contains information related to the observed security activity and behaviors of an artifact after executing it in a controlled or sandboxed environment. This information includes tactics and techniques detected, network communications, registry files and file system actions, processes and more.
    
7. Community - the community tab is where members of the VirusTotal community, such as security professionals or researchers, can leave comments and insights about the IoC.
    
8. Vendor’s Ratio and Community Score: the score displated at the top of the report is the vendors’ ratio. 
    

1. Ratio shows how many security vendors have flagged the IoC as malicious as well. 
    
2. Community score is below the ratio, based on input from VirusTotal community.
    

The Benefits of Documentation

>> Without documentation, a security operations team can never scale beyond one or two analysts.

- Transparency
    

- Transparent documentation is useful as a source of evidence for security insurance claims, regulatory investigations, and legal proceedings. 
    

- Standardization
    

- Established set of guidelines or standards that members of the organization can follow to complete a task or workflow. 
    
- Examples would be establishing an organization’s security policy, processes, and procedures. 
    

- Improves Clarity
    

- Effective documentation not only gives team members a clear understanding of their roles and duties, but it also provides information on how to get the job done. 
    

Document Evidence with Chain of Custody Forms

>> Chain of Custody is the process of documenting evidence possession and control during an incident lifecycle.

- As soon as evidence gets collected, chain of custody forms are introduced. The forms should be filled out with details as the evidence is handled. 
    
- Forms should be filled out with details as the evidence is collected.
    

>> Broken Chain of Custody is inconsistencies in the collection and logging of evidence in the chain of custody

>> Chain of Custody Establishes

- Integrity
    
- Reliability
    
- Accuracy
    

Best Practices for Effective Documentation

>> Documentation is any form of content that is used for a specific purpose, and it is essential in the field of security. 

Documentation Benefits

- Effective documentation has three main benefits:
    

- Transparency
    
- Standardization
    
- Clarity
    

Transparency

>> In security, transparency is critical for demonstrating compliance with regulations and internal processes, meeting insurance requirements, and for legal proceedings. Chain of custody is the process of documenting evidence possession and control during an incident lifecycle. 

Standardization

>> Standardization through repeatable processes and procedures supports continuous improvement efforts, help with knowledge transfer and facilitates the onboarding of new team members. Standards are references that inform how to set policies. 

- Incident response plans are documents that outline the procedures to take in each step of incident response. 
    
- Standardize an organization’s response process by outlining procedures in advance of an incident
    

Clarity

>> Ideally, all documentation provides clarity to its audience. Clear communication helps people quickly access the information they need so they can take necessary action.

- Security analysts are required to document the reasoning behind any action they take so that it’s clear to their team why an alert was escalated or closed.
    

Best Practices

>> As a security professional, you’ll need to apply documentation best practices in your career. Here are some general guidelines to remember:

Know Your Audience

- Before you start creating documentation, consider your audience and their needs. For instance, an incident summary written for a security operations center manager will be written differently than one that’s drafted for a chief executive officer.
    

- SOC Manager can understand technical jargon that a CEO can’t
    

Be Concise

- When documentation is too long, people can be discouraged from using it. To ensure that your documentation is useful, establish the purpose immediately. 
    
- THis helps people quickly identify the objective of the document. 
    
- Executive summaries should be brief so that it can be easily skimmed to identify the key findings. 
    

Update Regularly

- In security, new vulnerabilities are discovered and exploited constantly. Documentation must be regularly reviewed and updated to keep up with the evolving threat landscape
    
- Updating documentation, security teams will stay well informed and incident response plans stay updated. 
    

The Value of Cybersecurity Playbooks

>> Playbooks in cybersecurity are manuals that provide details about any operational action.

- Instructions on exactly what to do when an incident occurs
    
- Clear picture of their tasks during the entire incident response life cycle
    

Types of Playbooks

1. Non-automated
    

1. Step by step actions by an analyst
    

3. Automated
    

1. Help lower time to resolution for incidents
    

5. Semi-automated
    

1. Increase productivity and decrease time to resolution
    

>> For playbooks to be effective in a constantly changing landscape, they must be updated regularly.

  

The Role of Triage in Incident Response

>> Triage in medicine is the process of allocating limited resources to those who need it the more urgently during a timeframe. 

- E.g. a heart attack is more serious than a broken finger. 
    

Triage Process

1. Receive and assess
    
2. Assign priority
    
3. Collect and analyze
    

Questions to Ask?

- Is there anything out of the ordinary?
    
- Are there multiple failed login attempts?
    
- Did the login happen outside of normal working hours?
    
- Did the login happen outside of the network?
    

The Triage Process

>> Having the skills to effectively triage is important because it allows you to address and resolve security risks efficiently.

- Triage process consists of three steps:
    

- Receive and assess
    
- Assign priority
    
- Collect and analyze
    

Receive and Assess

>> During this first step of the triage process, a security analyst receives an alert from an alerting system like an intrusion detection system (IDS). You might recall that an IDS is an application that monitors system activity and alerts on possible intrusions. 

>> Here are some questions to consider when verifying the validity of an alert. 

- Is the alert a false positive? Security analysts must determine whether the alert is a genuine security concern or a false positive, or an alert that incorrectly detects the presence of a threat.
    
- Was this alert triggered in the past? If so, how was it resolved? The history of an alert can determine whether the alert is a new or recurring issue.
    
- Is the alert triggered by a known vulnerability? If an alert is triggered by a known vulnerability, security analysts can leverage existing knowledge to determine an appropriate response and minimize impact
    
- What is the severity of the alert? The severity of an alert can help determine the priority of the response so that critical issues are quickly escalated.
    

Assign Priority

>> Once the alert has been properly assessed and verified as a genuine security issue, it needs to be prioritized accordingly. Incidents differ in their impact, size and scope, which affects the response efforts. 

>> Because all incidents are not equal, some factors are to be considered when determining the priority of an incident:

- Functional impact: Security incidents that target information technology systems impact the service that these systems provide to it’s users. For example, a ransomware incident can severely impact the confidentiality, availability and integrity of systems.
    
- Information Impact: incidents can affect the confidentiality, availability and integrity of an organization's data and information. In a data exfiltration attack, malicious actors can steal sensitive data. This data can belong to a third party user or other organizations.
    
- Recoverability: How an organization recovers from an incident depends on the size and scope of the incident and the amount of resources available. In some cases, recovery might not be possible, like when data is stolen and shared publicly. 
    

- Spending time, money and resources on an incident with no recoverability can be wasteful
    

Collect and Analyze

- The final step of triage involves the security analyst performing a comprehensive analysis of the incident. The goal of this step is to gather enough information to make an informed decision to address it. 
    
- Depending on the severity of the incident, escalation to a level two analyst or a manager might be required. 
    

Benefits of Triage

>> By prioritizing incidents based on their potential impact, you can reduce the scope of impact to the organization by ensuring a timely response. 

  

- Resource Management: Triaging alerts allows security teams to focus their resources on threats that require urgent attention
    
- Standardized Approach: Triage provides a standardized approach to incident handling. Process documentation, like playbooks, help to move alerts through an iterative process to ensure that alerts are properly assessed and validated. 
    

Containment, Eradication and Recovery Phase of the Lifecycle

>> It’s important to note that these steps interrrelate.

Containment

>> After an incident has been detected, it must be contained

- Containment is the act of limiting and preventing additional damage caused by an incident
    
- A common containment strategy for a malware incident on a single computer system is to isolate the affected system by disconnecting it from the network.
    

Eradication

>> The complete removal of the incident elements from all affected systems

- Performing vulnerability tests and applying patches to vulnerabilities related to the threat
    

Recovery

>> The process of returning affected systems back to normal operations

- Reimaging affected systems, resetting passwords and adjusting network configurations
    

Business Continuity Considerations

>> Explore the importance that business continuity planning has in recovering from incidents.

Business Continuity Planning

 >> Security teams must be prepared to minimize the impact that security incidents can have on their normal business operations. When an incident occurs, organizations might experience significant disruptions to the functionality of their systems and services.

- Prolonged disruption to systems and services can have serious effects, causing legal, financial and reputational damage.
    

>> Similar to an incident response plan, a business continuity plan (BCP) is a document that outline the procedures to sustain business operations during and after a significant disruption

- A BCP helps organizations ensure that critical business functions can resume or can be quickly restored when an incident occurs
    

>> Entry level analysts aren’t typically responsible for the development and testing of a BCP. However, it’s important to understand how BCPs provide organizations with a  structured way to respond and recover from security incidents

Consider the Impacts of Ransomware to Business Continuity

>> Impacts of a security incident such as ransomware can be devastating for business operations. Ransomware attacks targeting critical infrastructure such as healthcare can have the potential to cause significant disruption

- At a larger scale, security incidents that target the assets, systems and networks of critical infrastructure can also undermine national security, economic security, and the health and safety of the public. 
    
- BCPs help to minimize interruptions to operations so that essential services can be accessed. 
    

Recovery Strategies

>> When an outage occurs due to a security incident, organizations must have some sort of a functional recovery plan set to resolve the issue and get systems fully operational. BCPs can include strategies for recovery that focus on returning to normal operations. 

Site Resilience

>> Resilience is the ability to prepare for, respond to and recover from disruptions. Organizations can design their systems to be resilient so that they can continue delivering services despite facing disruptions. An example is site resilience, which is used to ensure the availability of networks, data centers or other infrastructure when a disruption happens. 

- Hot sites: a fully operational facility that is a duplicate of an organization’s primary environment. Hot sites can be activated immediately when an organization’s primary site experiences failure or disruption.
    
- Warm sites: a facility that contains a fully updated and configured version of the hot site. Unlike hot sites, warm sites are not fully operational and available for immediate use but can quickly be made operational when a failure or disruption occurs.
    
- Cold sites: A backup facility equipped with some of the necessary infrastructure required to operate an organization’s site. When a disruption or failure occurs, cold sites might not be ready for immediate use and might need additional work to be operational. 
    

Post-Incident Activity Phase

>> The process of reviewing an incident to identify areas for improvement during incident handling

Final Report 

- Documentation that provides a comprehensive review of an incident
    
- It includes a timeline and details and all events related to the incident
    

- Recommendations for future prevention
    

Lessons Learned Meeting

- Includes all parties involved in the incident and is generally held within two weeks after the incident. 
    
- During this meeting, the incident is reviewed to determine what happened, what actions were taken and how effective they were.
    
- Some questions during a lessons learned meeting:
    

- What happened?
    
- What time did it happen?
    
- Who discovered it?
    
- How did it get contained?
    
- What were the actions taken for recovery?
    
- What could have been done differently?
    

- Incident reviews can reveal human errors before detection and during response, whether it’s a security analyst missing a step in a recovery process, or an employee clicking a link in a phishing email, resulting in the spread of malware. 
    

Post-Incident Review 

>> Provides an opportunity to learn and improve your responses for future incidents.

Lessons Learned

- Also known a post-mortem. A lessons learned meeting includes all involved parties after a major incident. Depending on the scope of an incident, multiple meetings can be scheduled to gather sufficient data. The purpose of this meeting is to evaluate the incident in its entirety, assess the response actions, and identify any areas of improvement.
    
- Not all incidents require their own lessons learned meeting, the size and severity of an incident will dictate whether the meeting is necessary. However, major incidents, such as ransomware attacks, should be reviewed in a dedicated lessons learned meeting. 
    

Recommendations

- Lessons learned meetings provide opportunities for growth and improvement. For example, security teams can identify errors in response actions, gaps in processes and procedures, or ineffective security controls. 
    

Final Report

- Throughout this course, you explored the importance that documentation has in recording details during the incident response lifecycle. 
    
- At a minimum, incident response documentation should describe the incident by covering the 5 W’s of incident investigation: who, what, when, where, why and how. 
    

- Executive Summary: a high-level summary of the report including the key findings and essential facts related to the incident
    
- Timeline: a detailed chronological timeline of the incident that includes timestamps dating the sequence of events that led to the incident.
    
- Investigation: a compilation of the actions taken during the detection and analysis of the incident. For example, analysis of a network artifact such as a packet capture reveals information about what activities happen on a network. 
    
- Recommendations: a list of suggested actions for future prevention
    

Module 4: Overview of Logs

- Read and Analyze Logs
    
- Interpret signatures
    
- Search in SIEM tools
    

The Importance of Logs

>> Devices produce data in the form of events.

- Events are observable occurrences that happen on a network system or device.
    

>> Logs are one of the key ways that security professionals use to detect unusual or malicious activity.

- A log is a record of events that occur within an organization’s systems.
    
- Almost every device or system can generate logs
    

- What where and when an event occurred on the network
    
- Date
    
- Time
    
- Location
    
- Action
    
- Names
    

>> Log analysis: the process of examining logs to identify events of interest

- Web applications generate a high volume of log data
    
- Not all of this log data may be valuable for an investigation, it actually may slow things down
    
- Excluding specific data from being logged helps reduce the time spent searching through log data.
    

>> Software known as log forwarders collect logs from various sources and automatically forward them to a centralized log repository for storage.

>> Log Types

- Network
    
- System
    
- Application
    
- Security
    
- Authentication
    

Best Practices for Log Collection and Management

>> Examine best practices related to log management, storage and protection.

- Understanding the best practices related to log collection and management will help improve log searches and better support your efforts in identifying and resolving security incidents.
    

Logs

>> Records of events that occur within an organization’s systems.

- Today, virtually all computing devices produce some form of logs that provide valuable insights beyond troubleshooting.
    
- Security teams access logs from logging receivers like SIEM tools which consolidate logs to provide a central repository for log data
    
- Security professionals use logs to perform log analysis, which is the process of examining logs to identify events of interest
    

Types of Logs

>> Depending on the data source, different log types can be produced. Here’s a list of common log types that organizations should record:

- Network: network logs are generated by network devices like firewalls, routers or switches
    
- System: system logs are generated by operating systems like Chrome OS, Windows, Linux or Mac
    
- Application: application logs are generated by software applications and contain information relating to the events occurring within the application such as a smartphone app
    
- Security: security logs are generated by various devices or systems such as antivirus software and intrusion detection systems. Security logs contain security-related information such as file deletion
    
- Authentication: authentication logs are generated whenever authentication occurs such as a successful login attempt to a computer.
    

Log Details

>> Generally, logs contain a date, time, location, action and author of the action.

- Verbose logging records additional, detailed information beyond the default log recording.
    

Log Management

>> Because all devices produce logs, it can quickly become overwhelming for organizations to keep track of all the logs that are generated. To get the most value from your logs, you need to choose exactly what to log, how to access it easily, and keep it secure using log management

- Log management is the process of collecting, storing, analyzing and disposing of log data
    

What to Log

>> The most important aspect of log management is choosing what to log. Organizations are different, and their logging requirements can differ too. It’s important to consider which log sources are most likely to contain the most useful information depending on your event of interest. 

- Some information, including but not limited to phone numbers, email addresses, and names, form personally identifiable information (PII), which requires special handing and in some jurisdictions might not be possible to be logged. 
    

The issue with Overlogging

>> From a security perspective, it can be tempting to log everything. This is the most common mistake that organizations make. Just because it can be logged, doesn’t mean it needs to be logged. 

- Overlogging can increase storage and maintenance costs
    
- Overlogging can increase the load on systems, which can cause performance issues and affect usability, making it difficult to search for and identify important events
    

Log Retention

>> Organizations might operate in industries with regulatory requirements. For example , some regulations require organizations to retain logs for set periods of time and organizations can implement log retention practices in their log management policy

>> Organizations that operate in the following industries might need to modify log management policy to meet regulatory requirements.

- Public sector industries, like Federal Information Security Modernization ACT (FIMSA)
    
- Healthcare Industires, like Health Insurance Portability and Accountability Act of 1996
    
- Financial services industries, such as the Payment Card Industry Data Security Standard (PCI DSS), the Gramm-Leach-Bliley (GLBA) and the Sarbanes-Oxley Act (SOX)
    

Log Protection

>> Along with management and retention, the protection of logs is vital in maintaining log integrity. It’s not unusual for malicious actors to modify logs in attempts to mislead security teams and to even hide their activity. 

- Storing logs in a centralized log server is a way to maintain log integrity. When logs are generated, they get sent to a dedicated server instead of being stored on a local machine.
    

  
  
  

Variations of Logs

>> Logs Contain: 

- Timestamps
    
- System Characteristics
    
- Actions
    

Commonly Used Log Formats

- Syslog
    

- Protocol and log format
    
- Transports and writes logs as a protocol
    
- As a format, it contains a header, followed by structured data, and a message
    

- Header contains timestamp, hostname, application name and message ID
    
- Structured data portion contains additional data information in key-value pairs
    
- Message component contains a detailed log message about the event
    

- JavaScriot Object Notation (JSON)
    

- Curly brackets enclose the log statement
    
- Content of the log is centered within the brackets
    

- eXtensible Markup Language (XML)
    
- Comma Separated Values (CSV)
    

Overview of Log File Formats

>> review the following formats:

- JSON
    
- Syslog
    
- XML
    
- CSV
    
- CEF
    

JavaScript Object Notation

- Lightweight, easy to read and write
    
- Used for transmitting data in web technologies
    
- Commonly used in cloud environments
    
- JSON is derived from JavaScript syntax
    

- Key-value pairs
    
- Commas
    
- Double quotes
    
- Curly brackets
    
- Square brackets
    

Key-Value Pairs

- Set of data that represents two linked items: a key and its corresponding value. A key-value pair consists of a key followed by a colon, and then followed by a value.
    

- “Alert”: “Malware”.
    

Commas

- Used to separate data
    

Double Quotes

- Are used to enclose text data, which is also known as a string. 
    
- Data that contains numbers is not enclosed in quotes
    

Curly Brackets

- Curly brackets enclose an object, which is a data type that stores data in a comma-separated list of key-value pairs.
    

Square Brackets

- Used to enclose an array, which is a data type that stores data in a comma-separated ordered list. Arrays are useful when you want to store data as an ordered collection
    

Syslog

>> Standard for logging and transmitting data. It can be used to refer to any of its three different capabilities:

- Protocol: The syslog protocol is used to transport logs to a centralized log server for log management. It uses port 514 for plaintext logs and port 6514 for encrypted logs
    
- Service: the syslog service acts as a log forwarding service that consolidates logs from multiple sources into a single location. The service works by receiving and then forwarding any syslog log entries to a remove server
    
- Log format: The syslog format is one of the most commonly used log formats that you will be focusing on. It is the native logging format used in Unix systems. It consists of three components: a header, structured-data, and a message. 
    

XML (eXtensible Markup Language)

- XML uses tags to store and identify data. Tags are pairs that must contain a start tag and an end tag.
    
- The start tag encloses data with angle brackets, for example <tag>, whereas the end of a tag encloses data with angle brackets and a forward slash like this </tag>. 
    

Elements

- XML elements include both the data contained inside of a tag and the tags itself. 
    
- All XML entries must contain at least one root element.
    

- Root elements contain other elements that sit underneath them, known as child elements
    

Attributes

- XML elements can also contain attributes. Attributes are used to provide additional information about elements. Attributes are included as the second part of the tag itself and must always be quoted using either single or double quotes.
    

CSV (Comma Separated Value)

- CSV uses commas to separate data values. In CSV logs, the position of the data corresponds to its field name, but the field names might not be included in the log. It’s critical to understand what fields the source device (like an IPS, firewall, scanner, etc.) is including in the log.
    

CEF (Common Event Format)

- Common event format is a log format that uses key-value pairs to structure data and identify fields and their corresponding values. 
    
- Fields are separated by the pipe character |. However, anything in the extension part of the CEF log entry must be written in a key-value format. Syslog is a common method used to transport logs like CEF. 
    

- When syslog used a timestamp and hostname will be prepended to the CEF message. 
    

  

Overview of Intrusion Detection Systems

>> Telemetry

- The collection and transmission of data for analysis
    
- Describes the data itself
    
- Packet captures are considered telemetry
    

>> Endpoint

- Any device connected to a network
    
- Key targets to malicious actors
    

>> Host-based intrusion detection system

- An application that monitors the activity of the host on which it’s installed
    
- A host is any device that communicates with other devices on a network
    

>> Network-based intrusion detection system

- An application that collects and monitors network traffic and network data
    
- Similar to packet sniffers
    

>> Signature Analysis

- A detection method used to find events of interest
    

Detection Tools and Techniques

>> Different types of intrusion detection systems and the alerts they produce.

>> Two common detection techniques used by detection systems

Host-based intrusion detection system

- A host-based intrusion detection system (HIDS) is an application that monitors the activity of the host on which it’s installed. A HIDS is installed as an agent on a host. A host is also known as an endpoint, which is any device connected to a network like a computer or server
    
- HIDS is usually installed on all endpoints used to monitor and detect security threats. A HIDS monitors internal activity happening on the host to identify any unathorized or abnormal behavior.
    
- HIDS has additional capabilities, such as monitoring file systems, system resource usage, user activity and more. 
    

Network-based intrusion detection system

>> a network based intrusion detection system (NIDS) is an application that collects and monitors network traffic and network data. NIDS software is installed on devices located at specific parts of the network. If any malicious network traffic is detected, the NIDS logs it and generates an alert

- Using a combination of HIDS and NIDS to monitor an environment can provide a multi-layered approach to intrusion detection and response. HIDS and NIDS tools provide a different perspective on the activity occurring on a network and the individual hosts that are connected to it. 
    

Detection Techniques

>> Signature based detection and anomaly based detection

Signature-based analysis

- Detection method that is used to find events of interest. A signature is a pattern that is associated with malicious activity. 
    
- Signatures often contain specific patterns like a sequence of binary numbers, bytes or even specific data like an IP address.
    

>> Different types of signatures can be used depending on which type of threat or attack you want to detect. For example, an anti-malware signature contains patterns associated with malware.

- This can include malicious scripts that are used by the malware
    

Advantages

- Low rate of false positives: Signature-based analysis is very efficient at detecting known threats because it is simply comparing activity to signatures, which leads to fewer false positives
    

Disadvantages

- Signatures can be evaded: signatures are unique, and attackers can modify their attack behaviors to bypass the signatures. For example, attackers can make slight modifications to malware code to alter it’s signature and avoid detection.
    
- Signatures require updates: signature-based analysis relies on a database of signatures to detect threats.
    

- Each time a new threat or exploit is discovered, new signatures must be created and added to the database
    

- Inability to detect unknown threats: sig-based analysis relies on detecting known threats through signatures. Unknown threats cannot be detected, such as new malware families or zero-day attacks.
    

Anomaly-based Analysis

- Detection method that identifies abnormal behavior. There are two phases to anomaly based analysis:
    

- A training phase
    
- Detection phase
    

- Baselines are developed by collecting data that corresponds to normal system behavior
    
- In the detection phase, the current system activity is compared against this baseline
    

Advantages

- Ability to detect new and evolving threats: anomaly-based analysis can detect previously unknown threats like zero-days
    

Disadvantages: 

- High rate of false positives: any behavior that deviates from the baseline can be flagged as abnormal, including non-malicious behaviors
    
- Pre-existing compromise: the existence of an attacker during the training phase will include malicious behavior into the baseline
    

Components of a Detection Signature

>> A signature specifies detection rules. These rules outline the types of network intrusions you want an IDS to detect. 

- E.g. suspicious traffic trying to enter a port
    

Components of a NIDS Rule

- Action
    

- Determines the action to take if the rule criteria is met
    
- Alert, pass or reject
    

- Header
    

- Source and destination IP
    
- Source and destination ports
    
- Protocols
    
- Traffic direction
    

- Rule
    

- Lets you customize signatures with additional parameters
    
- Set options to match the content of a network packet to detect malicious payloads
    

- These reside in a packet’s data and perform malicious activity like deleting or encrypting data
    

Examining Signatures with Suricata

>> Suricata is an open-source signature-based IDS.

- Think of signatures like customizable templates
    
- Starting point for writing and defining your rules
    

Suricata Format Type

- EVE JSON - Extensible Event Format JavaScript Object Notation
    

- JSON uses key-value pairs
    

Suricata Log Types

- Alert Logs
    

- The output of signatures which have triggered an alert
    

- Network Telemetry Logs
    

- Recording what’s happening on a network
    

Overview of Suricata

>> More about Suricata, and the value of writing customized signatures and configuration

Introduction to Suricata

>> Three main ways Suricata can be used:

- Intrusion detection system (IDS): As a network-based IDS, Suricata can monitor network traffic and alert on suspicious activities and intrusions. 
    

- Can also be set up as a host-based IDS to monitor the system and network activities of a single host like a computer
    

- Intrusion prevention system (IPS): Suricata can also function as an intrusion prevention system (IPS) to detect and block malicious activity and traffic
    
- Network Security Monitoring (NSM): in this mode, Suricata helps keep networks safe by producing and saving relevant network logs. Suricata can analyze live network traffic, existing packet capture files, and create and save full or conditional captures./
    

Rules

>> Rules or signatures are used to identify specific patterns, behavior or conditions of network traffic that might indicate malicious activity. The terms rule and signature are often used interchangeably in Suricata. Security analysts use signatures, or patterns associated with malicious activity, to detect and alert on specific malicious activity. 

>> Suricata uses signature analysis, which is a detection method used to find events of interest Signatures consist of three components:

- Action: the first component of a signature. It describes the action to take if network or system activity matches the signature
    
- Header: the header includes network traffic information like and destination IP addresses, source and destination ports, protocol and traffic direction
    
- Rule options: the rule options provide you with different options to customize signatures.
    

Custom Rules

>> It is highly recommended that you modify or customize the existing rules to meet your specific security requirements.

- Security teams must extensively test and modify detection signatures according to their needs
    
- Custom rules helps to tailor detection and monitor to an organization, minimize the amount of false positives
    

Configuration File 

>> Before detection tools are deployed and can begin monitoring systems and networks, you must properly configure their settings so that they know what to do

- A configuration file is a file used to configure the settings of an application
    
- Lets you customize exactly how you want your IDS to interact with the rest of your environment
    

Log Files

>> There are two log files that Suricata generates when alerts are triggered:

- eve.json: standard suricata log file. This file contains detailed information and metadata about the events and alerts generated by Suricata stored in JSON format. 
    
- fast.log: used to record minimal alert information including basic IP address and port details about the network traffic. The fast.log file is used for basic logging and alerting and is considered a legacy file format and is not suitable for incident response or threat hunting.
    

>> The main difference between the eve.json file and the fast.log file is the level of detail that is recorded in each. 

Overview of Security Information Event Management Tools

>> A SIEM is an application that collect and analyzes log data to monitor critical activities in an organization

- Splunk
    
- Chronicle
    

Log Sources and Log Ingestion

SIEM Process Overview

>> The process involved three steps:

1. Collect and aggregate data: SIEM Tools collect event data from various data sources
    
2. Normalize data: Event data that’s been collected becomes normalized. Normalization converts data into a standard format so that data is structured in a consistent way and becomes easier to read and search. 
    

1. While data normalization is a common feature in many SIEM tools, it’s important to that SIEM tools vary in their data normalization capabilities.
    

4. Analyze data: After the data is collected and normalized, SIEM tools analyze and correlate the data to identify common patterns that indicate unusual activity. 
    

Log Ingestion

>> Process of collecting and importing data from log sources into an SIEM.

- In log ingestion, SIEM creates a copy of the event data it receives and retains it within its own storage. 
    

- This copy allows the SIEM to analyze and process the data without directly modifying the original source logs. The collection of event data provides a centralized platform for security analysts to analyze the data and respond to incidents.
    

Log Forwarders

>> There are many ways SIEM tools can ingest log data. For instance, you can manually upload data or use software to help collect data for log ingestion. 

- Manually uploading data may be inefficient and time-consuming because networks can contain thousands of systems and devices. Hence, it’s easier to use software that helps collect data. 
    
- Log forwarders are software that automate the process of collecting and sending log data. Some operating systems have native log forwarders. 
    

- Allows the data to be easily searched, explored, correlated and analyzed once installed and configured. 
    

Query for Events with Splunk

>> Broad search queries like “failed login” will returns thousands and thousands of results

- Slows down the response time of search engine as well
    
- Search queries need to be specific in order to save time and resources
    

>> Splunk uses its own processing language called Search Processing Language (SPL)

>> Raw log search has a slower performance since it extracts log data fields during the search process.

Query for Events with Chronicle

>> Chronicle uses the YARA-L language to create rules for searching through ingested log data

Types of Search

1. UDM search
    
2. Raw log search
    

Search Methods with SIEM Tools

>> Understand the different types of searches you can perform using SIEM tools so that you can find relevant event data to support your security investigations.

  

Splunk Searches

>> Splunk has it’s own query language called Search Processing Language (SPL). 

- Used to search and retrieve events form indexes using Splunk’s Search & Reporting App.
    

>> Here is an example of a basic SPL search that is querying an index for a failed event:

index=main fail

- index=main: this is the beginning of the search command that tells Splunk to retrieve events from an index named main. An index stores event data that’s been collected and processed by Splunk.
    
- fail: this is the search term. This tells Splunk to return any event that contains the term fail. 
    

Pipes

>> Piping sends the output of one command as the input of another command.

- SPL also uses piping (|) to separate the individual commands in the search. It’s also used to chain commands together so that the output of one command combines into the next command.
    

>> Example of two commands piped together:

index=main fail| chart count by host

- index=main fail: the beginning of the search command that tells SPlunk to retrieve events from an index named main for events containing the search term fail. 
    
- |: the pipe character separates and chains the two commands index=main and chart count by host. This means that the output of the fist commands index=main is used as the input of the second command chart count by host. 
    
- chart count by host: this command tells Splunk to transform the search results by creating a chart according to the count or number of events
    

Wildcard

>> a wildcard is a special character that can be substituted with any other character. A wildcard is usually symbolized by an asterisk character *. Wildcards match characters in string values. 

- Wildcards are useful because they can help find events that contain data that is similar but not entirely identical. 
    

index=main fail*

- index=main: this command retrieves events from an index named main.
    
- fail*: the wildcard after fail represents any character. This tells Splunk to search for all possible endings that contain the term fail. This expands the search results to return any event that contains the term fail such as “failed” or “failure”.
    

Chronicle Searches

>> In Chronicle, you search for events using the Search field. You can also us Procedural Filtering to apply filters to a search to further refine the search results. For example, you can use Procedural Filtering to include or exclude search results that contain specific information relating to an event type or log source. 

- In Chronicle, you can use Unified Data Module (UDM) searches or raw log searches. 
    

Unified Data Model (UDM)

- The UDM Search is the default search type used in Chronicle. You can perform a UDM search by typing your search, clicking on “Search” and selecting “UDM Search”. Through a UDM search, Chronicle searches security data that has been ingested, parsed and normalized. 
    
- A UDM Search retrieves search results faster than a Raw Log Search because it searches through indexed and structured data that’s normalized in UDM. 
    

>> Know that all UDM events contain a set of common fields including:

- Entities: Also known as nouns. All UDM events must contain at least one entity. This field provides additional context about a device, user or process that’s involved in an event.
    
- Event metadata: This field provides a basic description of an event, including what type of event it is, timestamps and more. 
    
- Network metadata: this field provides information about network related events and protocol details.
    
- Security results: this field provides the security related outcome of events. An example of a security result can be an antivirus software detecting and quarantining a malicious file by reporting “virus detected and quarantined”
    

  

Raw Log Search

>> If you can’t find the information you’re looking for through the normalized data, using a Raw Log search will search through the raw, unparsed logs. You can perform a Raw Log search by typing your search, clicking on “Search” and selecting “Raw Log Search”. Because it is searching through raw logs, it takes longer than a structured search.