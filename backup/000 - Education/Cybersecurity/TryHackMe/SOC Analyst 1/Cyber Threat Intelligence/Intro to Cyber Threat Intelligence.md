### Introduction

> This room will introduce you to cyber threat intelligence (CTI) and various frameworks used to share intelligence. 
> 
> 	As security analysts, CTI is vital for investigating and reporting against adversary attacks with organizational stakeholders and external communities.

### Learning Objectives

- The basics of CTI and its various classifications
- The lifecycle followed to deploy and use intelligence during threat investigations.
- Frameworks and standards used in distributing intelligence.

### Cyber Threat Intelligence Module

﻿This is the first room in a new Cyber Threat Intelligence module. The module will also contain:

- [Threat Intelligence Tools](https://tryhackme.com/room/threatinteltools)
- [YARA](https://tryhackme.com/room/yara)
- [OpenCTI](https://tryhackme.com/room/opencti)
- [MISP](https://tryhackme.com/room/misp)
# Cyber Threat Intelligence

> Cyber Threat Intelligence can be defined as evidence-based knowledge about adversaries, including their indicators, tactics, motivations, and actionable advice against them. 
> 
> 	These can be utilized to protect critical assets and inform cyber security teams and management business decisions.

It would be typical to use the terms "data", "information" and "intelligence" interchangeably.

However, let us distinguish between them to understand better how CTI comes into play.

**Data**: Discrete indicators associated with an adversary, such as IP addresses, URLs or hashes.

**Information**: A combination of multiple data points that answer questions such as "How many times have employees accessed tryhackme.com in the last month?"

**Intelligence**: The correlation of data and information to extract patterns of action based on contextual analysis.

The primary goal of CTI is to understand the relationship between your operational environment and your adversary and how to defend your environment against any attacks.

You would seek this goal by developing your cyber threat context by trying to answer the following questions:

- Who's attacking you?
- What are their motivations?
- What are their capabilities?
- What artefacts and indicators of compromise (IOCs) should you look out for?

With these questions, threat intelligence would be gathered from different sources under the following categories:

- **Internal**:
	- Corporate security events such as vulnerability assessments and incident response reports.
	- Cyber awareness training reports.
	- System logs and events.
- **Community**:
	- Open web forums.
	- Dark web communities for cybercriminals.
- **External**:
	- Threat intel feeds (Commercial and Open-Source)
	- Online marketplaces
	- Public sources including government data, publications, social media, financial and industrial assessments.
### Threat Intelligence Classifications

**Threat Intel** is geared towards understanding the relationship between your *operational environment and your adversary.*

With this in mind, we can break down threat intel into the following classifications:
- **Strategic Intel**: High-level intel that looks into the organization's threat landscape and maps out the risk areas based on trends, patterns and emerging threats that may impact business decisions.
- **Technical Intel**: Looks into evidence and artefacts of attack uses by an adversary. Incident Response teams can use this intel to create a baseline attack surface to analyze and develop defence mechanisms.
- **Tactical Intel**: Assesses adversaries' tactics, techniques and procedures (TTPs). This intel can strengthen security controls and address vulnerabilities through real-time investigations.
- **Operational Intel**: Looks into an adversary's specific motive and intent to perform an attack. Security teams may use this intel to understand the critical assets available to the organization (people, processes and technologies) that may be targeted.

# CTI Lifecycle

> Threat intel is obtained from a data-churning process that transforms raw data into contextualized and action-oriented insights geared towards triaging security incidents. 

The transformational process follows a six-cycle phase:
### 1. Direction

> Every threat intel program requires to have objectives and goals defined, involving identifying the following parameters:

- Information assets and business processes that require defending.
- Potential impact to be experienced on losing the assets or through process interruptions.
- Sources of data and intel to be used towards protection.
- Tools and resources that are required to defend the assets.

This phase also allows security analysts to pose questions related to investigating incidents.

### 2. Collection

> Once objectives have been defined, security analysts will gather the required data to address them.
> 
> 	Analysts will do this by using commercial, private and open-source resources available.
> 		Due to the volume of data analysts usually face, it is recommended to **automate this phase to provide time for triaging incidents.** 

### 3. Processing

> Raw logs, vulnerability information, malware and network traffic usually come in different formats and may be disconnected when used to investigate an incident.

This phase ensures that the data is *extracted, sorted, organized, and correlated with appropriate tags and presented visually in a useable and understandable format to the analysts.*

**SIEMS** are valuable tools for achieving this and allow quick parsing of data. 

### 4. Analysis

> Once the information aggregation is complete, security analysts must derive insights.

Decisions to be made involve:

- Investigating a potential threat through uncovering indicators and attack patterns.
- Defining an action plan to avert an attack and defend the infrastructure.
- Strengthening security controls or justifying investment for additional resources.

### 5. Dissemination

> Different organizational stakeholders will consume the intelligence in varying languages and formats. 

For example, C-suite members will require a concise report covering trends in adversary activities, financial implications and strategic recommendations. 

At the same time, analysts will more likely inform the technical team about the threat IOCs, adversary TTPs and tactical action plans.

### 6. Feedback

> This phase covers the most crucial part, as analysts rely on the responses provided by stakeholders to improve the threat intelligence process and implementation of security controls. 

Feedback should be a *regular interaction between teams* to keep the lifecycle working.

# CTI Standards and Frameworks

> **Standards and Frameworks** provide structures to rationalize the distribution and use of threat intel across industries. 

They also allow for common terminology, which helps in collaboration and communication. 

Here, we briefly look at some essential standards and frameworks that are commonly used.
### MITRE ATT&CK

The [ATT&CK framework](https://tryhackme.com/room/mitre) is a knowledge base of adversary behaviour, focusing on the indicators and tactics. Security analysts can use the information to be thorough while investigating and tracking adversarial behaviour.
### TAXII

[The Trusted Automated eXchange of Indicator Information (TAXII)](https://oasis-open.github.io/cti-documentation/taxii/intro) defines protocols for securely exchanging threat intel to have near real-time detection, prevention and mitigation of threats.

The protocol supports two sharing models:

- **Collection**: Threat intel is collected and hosted by a producer upon request by users using a *request-response model.*
- **Channel**: Threat intel is pushed to users from a central server through a *publish-subscribe model*
### STIX

[Structured Threat Information Expression (STIX)](https://oasis-open.github.io/cti-documentation/stix/intro) is a language developed for the "specification, capture, characterization and communication of standardized cyber threat information". 

It provides defined relationships between sets of threat info such as observables, indicators, adversary TTPs, attack campaigns and more. 
### Cyber Kill Chain

Developed by Lockheed Martin, the Cyber Kill Chain breaks down adversary actions into steps. This breakdown helps analysts and defenders identify which stage-specific activities occurred when investigating an attack. The phases defined are shown in the image below.

|Technique|Purpose|Examples|
|---|---|---|
|Reconnaissance|Obtain information about the victim and the tactics used for the attack.|Harvesting emails, OSINT, and social media, network scans|
|Weaponisation|Malware is engineered based on the needs and intentions of the attack.|Exploit with a backdoor, malicious office document|
|Delivery|Covers how the malware would be delivered to the victim's system.|Email, weblinks, USB|
|Exploitation|Breach the victim's system vulnerabilities to execute code and create scheduled jobs to establish persistence.|EternalBlue, Zero-Logon, etc.|
|Installation|Install malware and other tools to gain access to the victim's system.|Password dumping, backdoors, remote access trojans|
|Command & Control|Remotely control the compromised system, deliver additional malware, move across valuable assets and elevate privileges.|Empire, Cobalt Strike, etc.|
|Actions on Objectives|Fulfil the intended goals for the attack: financial gain, corporate espionage, and data exfiltration.|Data encryption, ransomware, public defacement|
### The Diamond Model

> The Diamond Model looks at intrusion analysis and tracking attack groups over time. 
> 
> 	It focuses on four key areas, each representing a different point on the diamond. These are:

- **Adversary**: The focus here is on the threat actor behind an attack and allows analysts to identify the motive behind the attack.
- **Victim**: The opposite end of adversary looks at an individual, group or organization affected by an attack.
- **Infrastructure**: The adversaries' tools, systems and software to conduct their attack are the main focus. Additionally, the victim's systems would be crucial to providing information about the compromise.
- **Capabilities**: The focus here is on the adverary's approach to reaching it's goal. This looks at the means of exploitation and the TTPs implemented across the attack timeline.

> An example of the diamond model in play would involve an adversary targeting a victim using phishing attacks to obtain sensitive information and compromise the system, as displayed on the diagram.
> 
> 	As a threat intelligence analyst, the model allows you to pivot along its properties to produce a complete picture of an attack and correlate indicators.

