# Introduction

> Understanding the behaviors, objectives and methodologies of a cyber threat is a vital step to establishing a strong cybersecurity defense (posture)

**Learning Objectives**:

- Understanding why frameworks such as the UKC are important and helpful in establishing a good cybersecurity posture
- Using the UKC to understand an attacker's motivation, methodologies and tactics
- Understanding the various phases of the UKC
- Discover that the UKC is a framework that is used to complement other frameworks such as MITRE.

# What is a "Kill Chain"?

> A **kill chain** is a term used to explain the various stages of an attack. 
> In the realm of cybersecurity, a Kill Chain is used to describe the methodology/path attackers such as hackers or APTs use to approach and intrude a target.

The objective is to understand an attacker's “Kill Chain” so that defensive measures can be put in place to either pre-emptively protect a system or disrupt an attacker's attempt.

# What is "Threat Modeling"?

> **Threat Modelling,** in a cybersecurity context, is a series of steps to ultimately improve the security of a system. Threat modelling is about identifying risk and essentially boils down to:

1. Identifying what systems and applications need to be secured and what function they serve in the environment.
	1. For example, is the system critical to normal operations, and is a system holding sensitive information like payment information or addresses?
2. Assessing what vulnerabilities and weaknesses these systems and applications may have and how they could be potentially exploited.
3. Creating a plan of action to secure these systems and applications from the vulnerabilities highlighted.
4. Putting in policies to prevent these vulnerabilities from occurring again where possible (for example, implementing a software development life cycle (SDLC) for an application or training employees on phishing awareness.)

> ***Threat modelling is important in reducing risk within a system or application.*** 

- It creates a high-level overview of an organization's IT assets (an asset in IT is a piece of software or hardware) and the procedures to resolve vulnerabilities.

The UKC can encourage threat modelling as the UKC framework helps identify potential attack surfaces and how these systems may be exploited.

***Stride, Dread and CVSS*** are all frameworks specifically used in threat modelling. If you are interested to learn more, check out the “[Principles of Security](https://tryhackme.com/room/principlesofsecurity)” room on TryHackMe.

# Introducing the Unified Kill Chain

> The [Unified Kill Chain](https://www.unifiedkillchain.com/assets/The-Unified-Kill-Chain.pdf), aims to complement (**not compete**) with other cybersecurity kill chain frameworks such as Lockheed Martin's and MITRE's ATT&CK.

The UKC states that there are 18 phases to an attack: Everything from reconnaissance to data exfiltration and understanding an attacker's motive. These phases have been grouped together in this room into a few areas of focus for brevity, which will be detailed in the remaining tasks.

Some large benefits of the UKC over traditional cybersecurity kill chain frameworks include the fact that it is modern and extremely detailed.

#### The Unified Kill Chain

| Number | Stage                | Description                                                                                          |
| ------ | -------------------- | ---------------------------------------------------------------------------------------------------- |
| 1      | Reconnaissance       | Researching, identifying and selecting targets using active or passive reconnaissance methods.       |
| 2      | Weaponization        | Preparatory activities aimed at setting up the infrastructure required for the attack.               |
| 3      | Delivery             | Techniques resulting in the transmission of a weaponized object to the targeted environment.         |
| 4      | Social Engineering   | Techniques aimed at the manipulation of people to perform unsafe actions.                            |
| 5      | Exploitation         | Techniques to exploit vulnerabilities in systems that may, amongst others, result in code execution. |
| 6      | Persistence          | Any access, action or change to a system that give an attacker persistent presence on the system.    |
| 7      | Defense Evasion      | Techniques an attacker may specifically use for evading detection or avoiding other defenses         |
| 8      | Command & Control    | Techniques that allow attackers to communicate with controlled systems within a target network       |
| 9      | Pivoting             | Tunnelling traffic through a controlled system to other systems that are not directly accessible.    |
| 10     | Discovery            | Techniques that allow an attacker to gain knowledge about a system and its network environment.      |
| 11     | Privilege Escalation | The result of techniques that provide an attacker with higher permissions on a system or network.    |
| 12     | Execution            | Techniques that result in execution of attacker-controlled code on a local or remote system.         |
| 13     | Credential Access    | Techniques resulting in the access of, or control over, system, service or domain credentials.       |
| 14     | Lateral Movement     | Techniques that enable an adversary to horizontally access and control other remote systems.         |
| 15     | Collection           | Techniques used to identify and gather data from a target network prior to exfiltration.             |
| 16     | Exfiltration         | Techniques that result or aid in an attacker removing data from a target network.                    |
| 17     | Impact               | Techniques aimed at manipulating, interrupting or destroying the target system or data.              |
| 18     | Objectives           | Socio-technical objectives of an attack that are intended to achieve a strategic goal.               |
#### Framework Comparison

| Benefits of UKC Framework                                         | How do Other Frameworks Compare?                                                                                                  |
| ----------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| Modern (released in 2017, updated in 2022)                        | Some frameworks, such as MITRE's was released in 2013, when the cybersecurity landscape was very different.                       |
| The UKC is extremely detailed.                                    | Other frameworks often have a small handful of phases.                                                                            |
| The UKC covers an entire attack - from recon to post-exploitation | Other frameworks have a limited amount of phases.                                                                                 |
| The UKC highlights a much more realistic attack scenario.         | Other frameworks do not account for the fact that an attacker will go back and forth between the various phases during an attack. |
# Phase: In (Initial Foothold)

> An attacker will employ numerous tactics to investigate the system for potential vulnerabilities that can be exploited to gain a foothold in the system. For example, a common tactic is the use of reconnaissance against a system to discover potential attack vectors (such as applications and services).

This series of phases also accommodates for an attacker creating a form of persistence (such as files or a process that allows the attacker to connect to the machine at any time).

Finally, the UKC accounts for the fact that attackers will often use a combination of the tactics listed above.

#### Reconnaissance **([MITRE Tactic TA0043](https://attack.mitre.org/tactics/TA0043/))**

> This phase of the UKC describes techniques that an adversary employs to gather information relating to their target. 

This can be achieved through means of passive and active reconnaissance. The information gathered during this phase is used throughout the later stages of the UKC (such as the initital foothold)

Information gathered from this phase can include:

- Discovering what systems and services are running on the target, this is beneficial information in the weaponization and exploitation phases of this section.
- Finding contact lists or lists of employees that can be impersonated or used in either a social engineering or phishing attack.
- Looking for potential credentials that may be of use in later stages, such as pivoting or initial access.
- Understanding the network topology and other networked systems can be used to pivot to. 

#### Weaponization ([MITRE Tactic TA0001](https://attack.mitre.org/tactics/TA0001/))

> This phase of the UKC describes the adversary setting up the necessary infrastructure to perform the attack. For example, this could be setting up a command and control server, or a system capable of catching reverse shells and delivering payloads to the system.

#### Social Engineering ([MITRE Tactic TA0001](https://attack.mitre.org/tactics/TA0001/))

> This phase of the UKC describes techniques that an adversary may employ to manipulate employess to perform actions that will aid in the adversaries attack.
> 	For example, a social engineering attack could include:

- Getting a user to open a malicious attachment
- Impersonating a web page and having the user enter their credentials.
- Calling or visiting the target and impersonation a user (for example, requesting a password reset) or being able to gain access to areas of a site that the attacker would not previously be capable of (impersonating a utility engineer).
#### Exploitation ([MITRE Tactic TA0002](https://attack.mitre.org/tactics/TA0002/))

> This phase of the UKC is rather short and simple. Specifically, this phase of the UKC describes the techniques an adversary uses to maintain access to a system they have gained an initial foothold in.

For example:

- Creating a service on the target system that will allow the attacker to regain access.
- Adding the target system to a Command & Control server where commands can be executed remotely at any time.
- Leaving other forms of backdoors that execute when a certain action occurs on the system (i.e. a reverse shell with execute when a system admin logs in).
#### Defense Evasion ([MITRE Tactic TA0005](https://attack.mitre.org/tactics/TA0005/))

> The "Defence Evasion" section of the UKC is one of the more valuable phases of the UKC. This phase specifically is used to understand the techniques an adversary uses to evade defensive measures put in place in the system or network. For example, this could be:

- Web application firewalls
- Network firewalls
- Anti-virus systems on the target machine
- Intrusion detection systems

This phase is valuable when analysing an attack as it helps form a response and better yet - gives the defensive team information on how they can improve their defense systems in the future.
#### Command & Control ([MITRE Tactic TA0011](https://attack.mitre.org/tactics/TA0011/))

> The **Command and Control** phase of the UKC combines the efforts an adversary made during the "Weaponization" stage of the UKC to establish communications between the adversary and target system.

An adversary can establish command and control of a target system to achieve its action on objectives. For example:

- Execute Commands
- Steal data, credentials and other information
- Use the controlled server to pivot to other systems on the network.

#### Pivoting ([MITRE Tactic TA0008](https://attack.mitre.org/tactics/TA0008/))

> **Pivoting** is the technique an adversary uses to reach other systems within a network that are not otherwise accessible (for example, they are not exposed to the internet). 
> 
> There are often many systems in a network that are not directly reachable and often contain valuable data or have weaker security.

For example, an adversary can gain access to a web server that is publicly accessible to attack other systems that are within the same network (but not accessible via the internet.)

# Phase: Through (Network Propogation)

> This phase follows a successful foothold being established on the target network. An attacker would seek to gain additional access and privileges to systems and data to fulfill their goals.
> 
> The attacker would set up a base on one of the systems to act as their pivot point and use it to gather information about the internal network.

### Pivoting ([MITRE Tactic TA0008](https://attack.mitre.org/tactics/TA0008/))

> Once the attacker has access to the system, they would use it as their **staging ground** and a tunnel between their command operations and the victim's network. 
> 	Would also be used as the **distribution point for malware and backdoors at later stages.**
#### Discovery ([MITRE Tactic TA0007](https://attack.mitre.org/tactics/TA0007/))

> The adversary would uncover information about the system and the network it is connected to. Within this stage, the knowledge base would be built from the active user accounts, the permissions granted, applications and software in use, web browser activity, files, directories and network shares, and system configurations.
#### Privilege Escalation ([MITRE Tactic TA0004](https://attack.mitre.org/tactics/TA0004/))

> Following the knowledge-gathering, the adversary would try to gain more prominent permissions with the pivot system. They would leverage the information on the accounts present with vulnerabilities and misconfigurations found to elevate their access to one of the following superior leves:

- *SYSTEM/ROOT*
- *Local Administrator*
- *User account with Admin-like access*
- *User account with specific access functions*
#### Execution ([MITRE Tactic TA0002](https://attack.mitre.org/tactics/TA0002/))

> Recall when the adversary set up their attack infrastructure. Once the attacker has access to the system, they would use it as their staging site and a tunnel between their command operations and the victim's network. 
> 
> The system would also be used as the distribution point for all malware and backdoors. 

Weaponized payloads? This is where they deploy their malicious code using the pivot system as their host. 

- Remote trojans, C2 scripts, malicious links and scheduled tasks are deployed and created to facilitate a recurring presence on the system and uphold their persistence. 
#### Credential Access ([MITRE Tactic TA0006](https://attack.mitre.org/tactics/TA0006/))

> Working hand in hand with privilege escalation stage, the adversary would attempt to steal account names and passwords through various methods, including keylogging and credential dumping. 

This makes them *harder to detect* during their attack as they would be using legitimate credentials.
### Lateral Movement ([MITRE Tactic TA0008](https://attack.mitre.org/tactics/TA0008/))

> With the credentials and elevated privileges, the adversary would seek to move through the network and jump through the network and jump onto other targeted systems to achieve their primary objective.
> 
> The stealthier the technique, the better.
# Phase: Out (Action on Objectives)

> This phase wraps up the journey of an adversary’s attack on an environment, where they have critical asset access and can fulfil their attack goals. 
> 
> These goals are usually geared toward compromising the confidentiality, integrity and availability (CIA) triad.

### Collection [MITRE Tactic (TA0009)](https://attack.mitre.org/tactics/TA0009/)

> After all the hunting for access and assets, the adversary will be seeking to gather all the valuable data of interest. 
> 
> This, in turn, compromises the confidentiality of the data and would lead to the next attack stage -- **Exfiltration**. 
> 	The main target sources include drives, browsers, audio, video and email.
#### Exfiltration ([MITRE Tactic TA0010](https://attack.mitre.org/tactics/TA0010/))

> To elevate the compromise, the adversary would seek to steal data, which would be packages using encryption measures and compression to avoid any detection. 
> 
> The C2 channel and tunnel deployed in the earlier phases will come in handy during this process.
#### Impact ([MITRE Tactic TA0040](https://attack.mitre.org/tactics/TA0040/))

> If the adversary seeks to compromise the intergrity and availability of the data assets, they would manipulate, interrupt or destroy these assets. 
> 
> 	The goal would be to disrupt business and operational processes and may involve removing account access, disk wipes and data encryption such as ransomware, defacement and denial of service (DoS) attacks.

### Objectives

> With all the power and access to the systems and network, the adversary would seek to achieve their strategic goal for the attack. 

For example, if the attack was financially motivated, they may seek to encrypt the files and systems with ransomware and ask for payment to release the data. 

In other instances, the attacker may seek to damage the reputation of the business, and they would release private and confidential information to the public.



