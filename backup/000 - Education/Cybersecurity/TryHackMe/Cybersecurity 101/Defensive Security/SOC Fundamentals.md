#tryhackme #socanalyst #cybersecurity #cybersecurity101 
# Introduction to SOC

Technology has made our lives more efficient, but with this efficiency comes more responsibility. Modern-day fears have come a long way from the exploitaiton of physical assets. The critical data, called secrets, are no longer stored in physical files. Organizations carry tons of confidential data in their network and systems. Any unauthorized disruption, loss, or modification to this data may cause them huge damage. 

Threat actors discover and exploit new vulnerabilities in these networks and systems daily, becoming a major concern in cyber security. Traditional security practices may not be enough to prevent many of these threats. Dedicating a whole team to managing your organization's security is important. 

A **SOC**, or **Security Operations Center** is a dedicated facility operated by a specialized security team. This team aims to continuously monitor an organization's network and resources and identify suspicious activity to prevent damage. This team works 24 hours a day, seven days a week. 

This room will delve into some key concepts of SOC, one of the most important fields in defensive security.

## Learning Objectives

- Building a baseline for SOC (Security Operations Center)
- Detection and response in SOC
- The role of People, Processes, and Technology
- Practical exercise
# Purpose and Components

The main focus of the SOC team is to keep **Detection** and **Response** intact. The SOC team has some resources in the form of security solutions that help them achieve this. These solutions integrate the whole company's network and all the systems to monitor them from one centralized location. Continuous monitoring is required to detect and respond to any security incident. 

![](https://i.imgur.com/kUSzl2V.png)
## Detection

- **Detect Vulnerabilities**: A vulnerability is a weakness that an attacker can exploit to carry out things beyond their permission level. A vulnerability might be discovered in any device's software (operating system and programs), such as a server or computer. For instance, the SOC might discover a set of MS Windows computers that must be patched against a specific published vulnerability. Strictly speaking, vulnerabilities are not necessarily the SOC's responsibility; however, unfixed vulnerabilities affect the security level of the entire company.
- **Detect Unauthorized Activity**: Consider the case where an attacker discovered the username and password of one of the employees and used them to log in to the company system. It is crucial to detect this kind of activity quickly before it causes any damage. Many clues, such as geographic location, can help us detect this. 
- **Detect Policy Violations**: A security policy is a set of rules and procedures created to help protect a company against security threats and ensure compliance. What is considered a violation would vary from company to company; examples include downloading pirated media files and sending confidential company files insecurely. 
- **Detect Intrusions**: Intrusions refer to unauthorized access to systems and networks. One scenario would be an attacker successfully exploiting our web application. Another would be a user visiting a malicious site and getting their computer infected. 
## Response

- **Support with Incident Response**: Once an incident is detected, certain steps are taken to respond to it. This response includes minimizing its impact and performing the root cause analysis of the incident. The SOC team also helps the incident response team carry out these steps.

There are three pillars of a SOC. With all these pillars, a SOC team becomes mature and efficiently detects and responds to different incidents. These pillars are **People**, **Process**, and **Technology**.
![](https://i.imgur.com/3lxwxsZ.png)
**People**, **Process** and **Technology** coexist in a SOC environment. A team of professional individuals working on state-of-the-art security tools in the presence of proper processes is what makes a mature SOC environment. 

In the upcoming tasks, we will discuss each of these pillars individually and examine how they are important parts of SOC.
# People

Regardless of the evolution of automating the majority of security tasks, the **People** in a SOC will always be important. A security solution can generate numerous red flags in a SOC environment, which can cause huge noise.

Imagine you are part of a fire brigade team and have centralized software where all the city's fire alarms are integrated. Suppose you get many fire notifications all at once, all for different places. When you get into those locations, your team finds out most of those were only triggers by excessive smoke from cooking. Eventually, all the efforts will be a waste of time and resources. 

In a SOC, with security solutions in place without human intervention, you'll end up focusing on more irrelevant issues. There are always the **People** who help the security solution to identify truly harmful activities and enable a prompt response. 

The **People** are known as the SOC team. This team has the following roles and responsibilities. 

![](https://i.imgur.com/WczLE51.png)

- **SOC Analyst (Level 1)**: Anything detected by the security solution would pass through these analysts first. These are the first responders to any detection. SOC Level 1 Analysts perform basic alert triage to determine if a specific detection is harmful. They also report these detections through proper channels. 
- **SOC Analyst (Level 2)**: While Level 1 does the first-level analysis, some detections may require deeper investigation. Level 2 Analysts help them dive deeper into the investigations and correlate data from multiple data sources to perform a proper analysis. 
- **SOC Analyst (Level 3):** Level 3 Analysts are experienced professionals who proactively look for any threat indicators and support in the incident response activities. The critical severity detection reported by Level 1 and Level 2 Analysts are often security incidents that need detailed responses, including containment, eradication, and recovery. This is where Level 3 analysts' experience comes in handy. 
- **Security Engineer**: All analysts work on security solutions. These solutions need deployment and configuration. Security Engineers deploy and configure these security solutions to ensure their smooth operation.
- **Detection Engineer**: Security riles are the logic built behind security solutions to detect harmful activities. Level 2 and 3 Analysts often create these rules, while the SOC team can sometimes also utilize the detection engineer role independently for this reason. 
- **SOC Manager**: The SOC Manager manages the processes the SOC team follows and provides support. The SOC manager also remains in contact with the organization's CISO (Chief Information Security Officer) to provide him with updates on the SOC team's current security posture and efforts. 

**Note**: The roles in the SOC team can increase or decrease depending on the size and criticality of the organizations.
# Process

We discussed the roles and responsibilities of different individuals working in the SOC team. Each role has its own **Processes**, just as we saw the role of Level 1 SOC analysts as the first responders to carry out alert triage and determine if it is harmful. Let's discuss some important processes involved in a SOC.
## Alert Triage

The alert triage is the basis of the SOC team. The first response to any alert is to perform the triage. The triage is focused on analyzing the specific alert. This determines the severity of the alert and helps us prioritize it. The alert triage is all about answering the 5 W's. What are these 5 Ws?

![](https://i.imgur.com/ZwmV1Yx.png)
Following are some questions that need to be answered during the triage of an alert. 

**Alert**: Malware detected on Host: GEORGE PC

| 5 Ws   | Answers                                                                                                                                                                                                                     |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| What?  | A malicious file was detected on one of the hosts inside the organization's network.                                                                                                                                        |
| When?  | The file was detected at 13:20 on June 5, 2024.                                                                                                                                                                             |
| Where? | The file was detected in the directory of the host: "George PC"                                                                                                                                                             |
| Who?   | The file was detected for the user George.                                                                                                                                                                                  |
| Why?   | After the investigation, it was found that the file was downloaded from a pirated-software-selling website. The investigation with the user revealed that they downloaded the file as they wanted to use software for free. |
## Reporting

The detected harmful alerts need to be escalated to higher-level analysts for a timely response and resolution. These alerts are escalated as tickets and assigned to the relevant people. The report should discuss all the 5 Ws along with a thorough analysis , and screenshots should be used as evidence of the activity. 
## Incident Response and Forensics

Sometimes, the reported detections point to highly malicious activities that are critical. In these scenarios, high-level teams initiate an incident response. The incident response process is discussed in detail in the [Incident Response](https://tryhackme.com/r/room/incidentresponsefundamentals) room. A few times, a detailed forensics activity also needs to be performed. This forensic activity aims to determine the incident’s root cause by analyzing the artifacts from a system or network.
# Technology

Having the right **People** and **Processes** in place would never be enough without security solutions for detection and response. The **Technology** portion in the SOC pillars refers to the security solutions. These security solutions efficiently minimize the SOC team's manual effort to detect and respond to threats.

An organization's network consists of many devices and applications. As a security team, individually detecting and responding to threats in each device or application would require significant effort and resources. Security solutions centralize all the information of the devices or applications present in the network and automate the detection and response capabilities. 

Let's get a brief understanding of some of these security solutions:

- **SIEM**: *Security Information and Event Management* (SIEM) is a popular tool used in almost every SOC environment. This tool collects logs from various network devices, referred to as log sources. Detection rules are configured in the SIEM solution, which contains logic to identify suspicious activity. The SIEM solution provides us with the detections after correlating them with multiple log sources and alerts us in case of a match with any of the rules. Modern SIEM solutions surpass this rule based detection analysis, providing us with user behavior analytics and threat intelligence capability. Machine learning algorithms support this to enhance the detection capabilities.

**Note**: The SIEM Solution only provides the **Detection** capabilities in a SOC environment.

- **EDR**: Endpoint detection and response provides the SOC team with detailed real-time and historical visibility of the device's activities. It operates on the endpoint level and can carry out automated responses. EDR has extensive detection capabilities for endpoints, allowing you to investigate them in detail and respond with a few clicks. 
- **Firewall**: A firewall functions purely for network security and acts as a barrier between your internal networks (such as the internet). It monitors incoming and outgoing network traffic and filters any unauthorized traffic. The firewall also has some detection rules deployed, which help us identify and block suspicious traffic before it reaches the internal network. 

Several other security solutions play unique roles in a SOC environment, such as Antivirus, EPP, IDS/IPS, XDR and SOAR, and more. The decision on what technology to deploy in the SOC comes after careful consideration of the threat surface and the available resources in the organization.
# Conclusion

This room helped us learn some exciting facts about the SOC team. We saw its responsibilities and the pillars, People, Process, and Technology, that mature any SOC environment. This room focused on understanding how People, Processes, and Technology play their roles in the day-to-day SOC use cases. Lastly, we got our hands on a practice lab and solved a real-world SOC alert as a level 1 Analyst.

