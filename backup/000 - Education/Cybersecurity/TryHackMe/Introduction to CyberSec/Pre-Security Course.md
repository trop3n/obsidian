### Intro to Offensive Security

>In short, offensive security is the process of breaking into computer systems, exploiting software bugs, and finding loopholes in applications to gain unauthorized access to them.

> To beat a hacker, you need to behave like a hacker, finding vulnerabilities and recommending patches before a cybercriminal does, as you'll do in this room.

> On the flip side, there is defensive security, which is the process of protecting an organization's network and computer systems by analyzing and securing any potential digital threats; learn more in the digital forensics room.
> 	In a defensive cyber role, you could be investigating infected computers or devices to understand how it was hacked, tracking down cybercriminals, or monitoring infrastructure for malicious activity. 

Entering the following command 
`gobuster -u http://fakebank.com -w wordlist.txt dir` will run and display an output like the one below:

```shell-session
```markup
ubuntu@tryhackme:~/Desktop$ gobuster -u http://fakebank.com -w wordlist.txt dir
=====================================================
Gobuster v2.0.1
=====================================================
[+] Mode         : dir
[+] Url/Domain   : http://fakebank.com/
[+] Threads      : 10
[+] Wordlist     : wordlist.txt
[+] Status codes : 200,204,301,302,307,403
[+] Timeout      : 10s
=====================================================
2022/04/11 18:23:28 Starting gobuster
=====================================================
/images (Status: 301)
/DIRECTORY_NAME_OUTPUT (Status: 200)
=====================================================
2022/04/11 18:23:38 Finished
=====================================================
```

In this command, the `-u` is used to state the website we're scanning, `-w` takes a list of words to iterate through to find hidden pages.

You will see that GoBuster scans the website with each word in the list, finding pages that exist on the site. GoBuster will have told you the pages it found in the list of page/directory names (indicated by Status: 301)
### Introduction to Defensive Security

> Offensive security focuses on one thing: breaking into systems. Breaking into systems might be achieved by exploiting bugs, abusing insecure setups, and taking advantage of unenforced access control policies, among other things. 

Defensive security is somewhat the opposite of offensive security, as it is concerned with two main tasks: 

1. Preventing intrusions from occuring
2. Detecting intrusions when they occur and responding properly

Some tasks related to defensive security include:

- User cyber security awareness: Training users about cybersecurity helps protect against various attacks that target their systems. 
- Documenting and managing assets: We need to know the types of systems and devices that we have to manage and protect properly.
- Updating and patching systems: Ensuring that computers, servers, and network devices are correctly updated and patched against any known vulnerability
- Setting up preventative security devices: firewall and intrusion prevention systems (IPS) are critical components of preventative security. Firewalls control what network traffic can enter and leave a network. IPS blocks any network traffic that matches present rules and attack signatures.
- Setting up logging and monitoring devices. Without proper logging and monitoring of the network, it won't be possible to detect malicious activities and intrusions. If a new unauthorized device appears on our network, we should be able to know. 

There is much more to defensive security, and the list above only covers a few topics. 

In this room, we cover:

- *Security Operations Center (SOC)*
- *Threat Intelligence*
- *Digital Forensics and Incident Response (DFIR)*
- *Malware Analysis*

#### Areas of Defensive Security

In this task, we will cover two main topics related to defensive security:
- Security Operations Center, where we cover Threat Intelligence
- Digital Forensics and Incident Response (DFIR), where we also cover Malware Analysis
##### Security Operations Center

> A *SOC* is a team of cybersecurity professionals that monitors the network and its systems to detect malicious cybersecurity events. Some main areas of interest for the SOC are:

- *Vulnerabilities*: Whenever a system vulnerability (weakness) is discovered, it is essential to fix it by installing proper updates or patches. When a fix is not available, the necessary measures should be taken to prevent an attacker from exploiting it. 
	- Although remediating vulnerabilities is of vital interest to a SOC, it is not necessarily assigned to them.
- *Policy Violations*: We can think of a security policy as a set of rules required for the protection of the network and systems. 
	- For example, it might be a policy violation if users start uploading confidential company information to an online storage device.
- *Unauthorized Activity*: Consider the case where a user's login name and password are stolen, and the attacker uses them to log into the network. A SOC needs to detect such an event and block it as soon as possible before further damage is done. 
- *Network Intrusions*: No matter how good your security is, there is always a change for an intrusion. An intrusion can occur when a user clicks on a malicious link or when an attacker exploits a public server. Either way, when an intrusion occurs, we must detect it as soon as possible to prevent further damage.

##### Threat Intelligence

> In this context, *Intelligence* refers to information you gather about actual and potential enemies. 

> A *Threat* is any action that can distrupt or adversely affect a system. Threat intelligence aims to gather information to help the company better prepare against potential adversaries.

The purpose would be to achieve a *threat-informed defense*. DIfferent companies have different adversaries. Some adversaries might seek to steal customer information from a mobile operator; however, other adversaries are interested in halting the production in a petroleum refinery. 

Example adversaries include a nation state cyberarmy working for political reasons and ransomware group acting for financial purposes. Based on the company (target), we can expect adversaries.

Intelligence needs data. Data has to be collected, processed and analyzed. Data collection is done from local sources such as network logs and public sources such as forums. 

Processing of data aims to arrange them in a format suitable for analysis. The analysis phase seeks to find more information about the attackers and their motives; moreover, it aims to create a list of recommendations and actionable steps.

As a result of threat intelligence, we identify the threat actor, predict their activity, and consequently, we will be able to mitigate their attacks and prepare a response strategy.

##### Digital Forensics and Incident Response (DFIR)

- Digital Forensics
- Incident Response
- Malware Analysis

**Digital Forensics**

 >Forensics is the application of science to investigate crimes and establish facts. With the use and spread of digital systems, such as computers and smartphones, a new branch of forensics was born to investigate related crimes: computer forensics, which later evolved into, *digital forensics*. 
 
 In defensive security, the focus of digital forensics shifts to analyzing evidence of an attack and its perpetrators and other areas such as intellectual property theft, cyber espionage, and possession of unauthorized content. 

Consequently, digital forensics will focus on different areas such as:

- *File System*: Analyzing a digital forensics image (low-level copy) of a system's storage reveals much information, such as installed programs, created files, partially overwritten files, and deleted files. 
- *System Memory*: If the attacker is running their malicious program in memory without saving it to the disk, taking a forensic image (low-level copy) of the system memory is the best way to analyze its contents and learn about the attack.
- *System Logs*: Each client and server computer maintains different log files about what is happening. Log files provide plenty of information about what happened on a system. Some traces will be left even if the attacker tries to clear their traces.
- *Network Logs:* Logs of the network packets that have traversed the network would help answer more questions about whether an attack is occurring and what it entails. 

**Incident Response**

> An *incident* usually refers to a data breach or cyber attack; however, in some cases, it can be something less critical, such as a misconfiguration, an intrusion attempt, or a policy violation.

Examples of a cyberattack include an attacker making our network or systems inaccessible, defacing (changing) the public website, and data breach (stealing company data). How would you *respond* to a cyberattack? Incident response specifies the methodology that should be followed to handle such a case. The aim is to reduce damage and recover in the shortest time possible. Ideally, you would develop a plan ready for incident response.

The four major phases of the incident response process are:

1. *Preparation*: This requires a team trained and ready to handle incidents. Ideally, various measures are put in place to prevent incidents from happening in the first place. 
2. *Detection and Analysis*: The team has the necessary resources to detect any incident; moreover, it is essential to further analyze any detected incident to learn about it's severity.
3. *Containment, Eradication and Recovery*:  Once an incident is detected, it is crucial to stop it from affecting other systems, eliminate it, and recover the affected systems. For instance, when we notice that a system is infected with a computer virus, we would like to stop (contain) the virus from spreading to other systems, clean (eradicate) the virus, and ensure proper system recovery.
4. *Post-Incident Activity*: After a successful recovery, a report is produced, and the learned lesson is shared to prevent similar future incidents.

**Malware Analysis**

Malware stands for malicious software. *Software* refers to programs, documents, files that you can save on a disk or send over the network. Malware includes many types, such as: 

- *Virus*: a piece of code that attaches itself to a program. It is designed to spread from one computer to another; moreover, it works by altering, overwriting, and deleting files once it infects a computer. The result ranges from the computer becoming slow to unstable. 
- *Trojan Horse*: a program that shows one desirable function but hides a malicious function underneath. For example, a victim might download a video player from a shady website that gives the attacker complete control over their system. 
- *Ransomware*: malicious program that encrypts the users files. Encryption makes the files unreadable without a key. The attacker offers the user the encryption key if the user is willing to pay a ransom, usually in the form of cryptocurrency.

*Malware analysis* aims to learn about such malicious programs using various means:

1. Static analysis works by inspecting the malicious program without running it. Usually, this requires solid knowledge of assembly language (processor's instruction set, i.e., computer's fundamental instructions)
2. Dynamic analysis works by running the malware in a controlled environment and monitoring it's activities. It lets you observe how the malware behaves when running.

### Practical Example of Defensive Security

143.110.250.149

> There are many open source websites out there, like AbuseIPDB, and CISCO Talos Intelligence, where you can perform a reputation and location check for the IP address. 

# Careers in Cyber

> Cyber careers are becoming more in demand and offer high salaries. There are many different jobs to choose from in the cyber industry, from offensive pentesting, to defensive security.

### Security Analysts

> Security Analysts are integral to constructing security measures across organizations to protect the company from attacks. Analysts explore and evaluate company networks to uncover actionable data and recommendations for engineers to develop preventative measures.

This job roles requires working with various stakeholders to gain an understanding of security requirements and the security landscape.

**Responsibilities**

- Working with various stakeholders to analyze the cybersecurity throughout the company
- Compile ongoing reports about the safety of networks, documenting security issues and measures taken in response. 
- Develop security plans, incorporating research on new attack tools and trends, and measures needed across teams to maintain data security.

### Security Engineer

> Security engineers develop and implement security solutions using threats and vulnerability data - often sourced from members of the security workforce. Security engineers work across circumventing a breadth of attacks, network threats, and evolving trends and tactics. 

The ultimate goal is to retain and adopt security measures to mitigate the risks of attack and data loss.

**Responsibilities**

- Testing and screening security measures across software.
- Monitor networks and reports to update systems and mitigate vulnerabilities.
- Identify and implement systems needed for optimal security

### Incident Responder

> Incident responders respond productively and efficiently to security breaches. Responsibilities include creating plans, policies and protocols for organizations to enact during and following incidents. 

This is often a highly pressurized position with assessments and responses required in real-time, as attacks are unfolding. Incident response metrics include MTTD, MTTA and MTTR - the meantime to detect, acknowledge and recover (from attacks). 

The aim is to achieve a swift and effective response, retain financial standing and avoid negative breach implications. Ultimately, incident responders protect the company's data, reputation and financial standing from cyberattacks. 

**Responsibilities**

- Developing and adopting a thorough, actionable incident response plan.
- Maintaining strong security best practices and supporting incident response measures.
- Post-incident reporting and preparation for future attacks, considering learning and adaptations to take from incidents

### Digital Forensics Examiner

> If you like to play detective, this might be the perfect job. If you are working as part of a law-enforcement department, you would be focused on collecting and analysing evidence to help solve crimes: charging the guilty and exonerating the innocent. On the other hand, if your work falls under defending a company's network, you will be using your forensic skills to analyse incidents, such as policy violations.

**Responsibilities**

- Collect digital evidence while observing legal proceedings
- Analyse digital evidence to find answers related to the case
- Document your findings and report on the case

### Malware Analyst

> A malware analysts work involves analysing suspicious programs, discovering what they do and writing reports about their findings. A malware analyst sometimes is called a reverse-engineer as their core task revolves around converting compiled programs from machine language to readable-code, usually in a low-level language.

This work requires the malware analyst to have a strong programming background, especially in low-level languages such as Assembly and C. The ultimate goal is to learn about all the activities that a malicious program carries out, find out how to detect it and report it.

**Responsibilities**

- Carry out static analysis of malicious programs, which entails reverse-engineering
- Conduct dynamic analysis of malware samples by observing their activities in a controlled environment
- Document and report all the findings

### Penetration Tester

You may see penetration referred to as ethical hacking. A pentesters job role is to test the security of the systems and software within a company - this is achieved through attempts to uncover flaws and vulnerabilities through systemized hacking.

Pentesters exploit these vulnerabilities to evaluate risk in each instance. The company then can take these insights to rectify issues to prevent a real-world cyberattack.

**Responsibilities**

- Conduct tests on computer systems, networks and web-based applications
- Perform security assessments, audits and analyse policies
- Evaluate and report on insights, recommending actions for attack prevention

### Red Teamer

> Red teamers share similarities to pentesters, with a more targeted job role. Penetration testers look to uncover many vulnerabilities across systems to keep cyber-defense in good standing, whilst red teamers are enacted to test the company detection and response capabilities. 

This role requires imitating the cyber criminals actions, emulating malicious attacks, retaining access, and avoiding detection. Red team assessments can run for up to a month, typically by a team external to the company. They are often best suited to organizations with mature security programs in place.

**Responsibilities**

- Emulate the role of a threat actor to uncover exploitable vulnerabilities, maintain access and avoid detection
- Assess organizations' security controls, threat intelligence, and incident response procedures
- Evaluate and report on insights, with actionable data for companies to avoid real-world instances

# What is Networking?

> Networks are simply things connected. For example, your friendship circle: you are all connected because of similar interests, hobbies, skills and sorts.

Networks can be found in all walks of life:

- City transportation grid
- National power grid
- Meeting and greeting your neighbors
- Postal systems for sending letters and projects

More specifically for computing, networks are the same idea, just dispersed to technological devices.

Take your phone as an example, the reason that you have it is to access things. 

### What is the Internet?

> One giant network that consists of many, many small networks within itself. 

The first iteration of the internet was with ARPANET in the late 1960's. This project was funded by the US DoD and was the first documented network in action.

It wasn't until 1989 when the internet as we know it was born when Tim Berners-Lee created the World Wide Web.
###### The internet is made up of many small networks joined together. These small networks are called **private networks**, where networks connecting these small networks are called **public networks**, or the Internet.

### Identifying Devices on a Network

To communicate and maintain order, devices must be both identifying and identifiable on a network. 

Devices on the network are vert similar to humans in the fact that we have two ways of being identified: 

- Our name
- Fingerprints

Devices have the same thing: two means of identification, with one being permeable. These are:

- IP Address
- Media Access Control Address (MAC)

#### IP Addresses

> Briefly, an IP address (or **I**nternet **P**rotocol) address can be used as a way of identifying a host on a network for a period of time, where that IP address can then be associated with another device without the IP address changing.

An IP Address is a set of numbers that are divided into four octets. The value of each octet will summarize to be the IP address of the device on the network.

This number is calculated through a technique known as IP addressing & Subnetting. 
- IP addresses can change from device to device but cannot be active simultaneously more than once within the same network.

IP Addresses follow a set of standards known as *protocols*. These protocols are the backbone of networking and force many devices to communicate in the same language. 

Devices can be on both a public and private network. Depending on where they are will determine what type of IP address they have: public or private. 

A **public IP address** is used to identify a device on the internet, whereas a private IP address is used to identify a device amongst other devices. 

> IPv6 is the new iteration of Internet Protocol addressing scheme to help tackle the issue of *IP exhaustion*. 

It seems more daunting, but it hosts a few key benefits:
- Supports up to 2^128 of IP addresses (340 trillion plus), resolving the exhaustion issue.
- More efficient due to new methodologies

#### MAC Addresses

> Devices on a network will all have a physical network interface, which is a microchip found on the device's motherboard. The network interface is assigned a unique address at the factory it was built at, called a **Media Access Control Address.** 

The MAC address is a **twelve-character** hexadecimal number (a base sixteen numbering system used in computing to represent numbers) split into two's by a colon.

These colons are considered separators. 
>For example, _a4:c3:f0:85:ac:2d_. The first six characters represent the company that made the network interface, and the last six is a unique number.

An interesting thing about MAC addresses is that they can be faked or *spoofed* in a process known as *spoofing*. 
- This spoofing occurs when a networked device pretends to identify as another using its MAC address. 
- When this occurs, it can often break poorly implemented security designs that assume the device talking on a network is trustworthy. 

> Places such as cafes, coffee shops, and hotels alike often use MAC address control when using their "Guest "or "Public" Wi-Fi. This configuration could offer better services, i.e. a faster connection for a price if you are willing to pay the fee per device.

### Ping (ICMP)

> Ping is one of the most fundamental network tools available to us. Ping uses **ICMP** (Internet Control Message Protocol) packets to determine the performance of a connection between devices, for example, if the connections exists or is reliable.

The time taken for ICMP packets travelling between devices is measured by ping. This measuring is done by using ICMP's echo packet and then ICMP's echo reply from the target device.

> Pings can be performed against devices on a network, such as your home network or resources like websites. This tool can be easily used and comes installed on Operating Systems (OSs) such as Linux and Windows. The syntax to do a simple ping is `ping IP address or website URL`. Let's see this in action in the screenshot below.

# Introduction to LAN

> Over the years, there has been experimentation and implementation of various network designs. In reference to networking, when we refer to the term **topology**, we are actually referring to the design or look of the network at hand. 

### Star Topology

> The main premise of a star topology is that devices are individually connected via a central networking device such as a switch or hub. 
> 	This topology is commonly found today because of it's reliability and scalability - despite it's cost. 

Any information send to a device in this topology is sent via the central device to which it connects. 

Because more cabling and the purchase of dedicated networking equipment is required for this topology, it is more expensive than any of the other topologies. However, despite this added cost, this does provide some significant advantages. 

- For example, this topology is much more scalable in nature, which measn that it is very easy to add more devices as the demand for the network increases.

Unfortunately, the more the networking scales, the more maintenance is required to keep the network functional. This increased dependence on maintenance can also make troubleshooting faults much harder. 

- Furthermore, the star topology is still prone to failure, albeit reduced. 
- For example, if the centralized hardware that connects the devices fails, these devices will no longer be able to send or receive data. Thankfully, these centralized hardware devices are often robust.

### Bus Topology

> This type of connection relies upon a single connection which is known as a backbone cable. This type of topology is similar to the leaf off of a tree in the sense that devices (leaves) stem from where the branches on this cable are. 

Because all data destined for each device travels along the same cable, it is very quickly prone to becoming slow and bottlenecked if devices within the topology are simultaneously requesting data.

- This bottleneck also results in very difficult troubleshooting because it quickly becomes difficult to identify which device is experiencing issues with data all travelling along the same route.

However, bus topologies are one of the easier and more cost-effective topologies to setup because of their expenses, such as cabling or dedicated networking equipment used to connect these devices.

Lastly, another disadvantage of the bus topology is that there is little redundancy in place in case of failures. This disadvantage is because there is *single point of failure* along the backbone cable. 
- If this cable were to break, devices can no longer receive or transmit data along the bus.

### Ring Topology

> Also known as a **token topology**. Devices such as computers are connected directly to each other to form a loop, meaning that there is little cabling required and less dependence on dedicated hardware such as within a star topology.

A ring topology works by sending data across a loop until it reaches the destined device, using other devices along the loop to forward the data. Interestingly, a device will only send received data from another device in this topology if it does not have any to send itself.
- If the device happens to have data to send, it will send its own data first before sending data from another source.

Because data only goes in one direction in this topology, it is fairly easy to troubleshoot any faults that arise. However, this is a double-edged sword because is isn't an efficient way of sending data across a network, as it may have to visit many multiple devices before reaching the intended device.

Lastly, ring topologies are less prone to bottlenecks, such as within a bus topology, as large amounts of traffic are not travelling across the network and any one time. 

- This design does mean that a fault such as a cut cable, or broken device will result in the entire networking breaking.

### What is a Switch?

> Switches are dedicated devices within a network that are designed to aggregate multiple other devices such as computers, printers or any other networking-capable device using ethernet. 

These various device plug into a switch's port. Switches are usually found in larger networks such as businesses, schools, or similar sized networks, where there are many devices to connect to the network.

- Switches can connect a large number of devices by having ports of 4,8,16,24,32 and 64 for devices to plug into.

Switches are much more efficient than their lesser counterpart (hubs/repeaters). 
- Switches keep track of what device is connected to which port. This way, when they receive a packet, instead of repeating that packet to every port like a hub would do, it just sends it to the intended target, thus reducing network traffic. 

Both switches and routers can be connected to one another. The ability to do this increases the redundancy, or reliability, of a network by adding multiple paths for data to take. If one path goes down, another can be used. Whilst this may reduce the overall performance of a network because packets have to take longer to travel, there is no downtime -- a small price to pay considering the alternative.

### What is a Router?

> It's a router's job to connect networks and pass data between them. It does this by routing.

Routing is the label given to the process of data travelling across networks. Routing involves creating a path between networks so that this data can be successfully delivered. 

Routing is useful when devices are connected by many paths, such as in the example diagram below.

# A Primer on Subnetting

> **Subnetting** is the term given to splitting up a network into smaller, miniature networks within itself. 
> 	Think of it as slicing up a cake for your friends. 
> 	There's only so much cake to go around, and everyone wants a piece. 

Subnetting is you deciding who gets what slice & reserving such a slice of this metaphorical cake.

Organizations typically have departments, like finance, HR and accounting. 

Whilst you know where to send information in real life to the correct department, networks need to know as well. Network administrators use subnetting to categorize and assign specific parts of a network to reflect this.

> Subnetting is achieved by splitting up the number of hosts that can fit within the network, represented by a number called a subnet mask. 

As you recall about IP addresses, they are divided into four octets. The same goes for a subnet mask which is also represented as a number of four bytes (32 bits), ranging from 0 to 255. 

Subnets use IP addresses in three different ways:

1. Identify the network address
2. Identify the host address
3. Identify the default gateway

| Type            | Purpose                                                                                                                                        | Explanation                                                                                                                                                                                                                                          | Example       |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- |
| Network Address | This address identifies the start of the actual network and is used to identify a network's existence.                                         | For example, a device with the IP address of 192.168.1.100 will be on the network identified by 192.168.1.0                                                                                                                                          | 192.168.1.0   |
| Host Address    | An IP address here is used to identify a device on the subnet                                                                                  | For example, a device will have the network address of 192.168.1.1                                                                                                                                                                                   | 192.168.1.100 |
| Default Gateway | The default gateway address is a special address assigned to a device on the network that is capable of sending information to another network | Any data that needs to go to a device that isn't on the same network (i.e. isn't on 192.168.1.0) will be sent to this device. These devices can use any host address but usually use either the first or last host address in a network (.1 or .254) | 192.168.1.254 |
You typically won't need to subnet a home network, because there is a low chance of having 254 devices on a single home network.

In businesses and office, there are typically many more devices (PCs, Printers, cameras and sensors), where subnetting takes place.

Subnetting provides a range of benefits, including:
- Efficiency
- Security
- Full Control

### The ARP Protocol

> The Address Resolution Protocol, or ARP for short, is the technology that is responsible for allowing devices to identify themselves on a network. 

Simply, the ARP protocol allows a device to associate its MAC address with an IP address on the network. Each device on a network will keep a log of the MAC address associated with other devices. 

When devices wish to communicate with another, they will send a broadcast to the entire network searching for the specific device. Devices can use the ARP protocol to find the MAC address (and therefore the physical identifier) of a device for communication. 

**How Does ARP Work?**

Each device within a network has a ledger to store information on, which is called a cache. In the context of the ARP protocol, the cache stores the identifiers of the other devices on the network.

In order to map these two identifiers together, (IP and MAC address), the ARP protocol sends two kinds of messages:

1. **ARP Request**
2. **ARP Reply**

When an **ARP Request** is sent, a message is broadcasted to every other device found on a network by the device, asking whether or not the device's MAC address matches the requested IP address.

If the device does have the requested IP address, an **ARP Reply** is returned to the initial device to acknowledge this. The initial device will now remember this and store it within its cache (an ARP entry).

### The DHCP Protocol

> IP Addresses can be assigned either manually, by entering them physically into a device, or automatically and most commonly by using DHCP (**Dynamic Host Configuration Protocol**) server.

When a device connects to a network, if it has not already been manually assigned an IP address, it sends out a request (**DHCP Discover**) to see if any DHCP servers are on the network. The DHCP server then replies back with an IP Address the device could use (**DHCP Offer**) 
- The device then sends a reply confirming it wants the offered IP Address (**DHCP Request**), and then lastly, the DHCP server sends a reply acknowledging this has been completed, and the device can start using the IP Address (**DHCP Ack**)

- **DHCP Discover**: Hey I'm new here, is there anyone who can give me an IP address?
- **DHCP Offer**: Hey! Sure thing, you can have 192.168.1.0.
- **DHCP Request**: Yes, that would be brilliant! I'll start using 192.168.1.0.
- **DHCP ACK**: Okay, great. You can use that IP address for the next 24 hours. 

# The OSI Model

### What is the OSI Model?

> The OSI model, or **Open Systems Interconnection Model**, is an absolute fundamental model used in networking. 

This critical model provides a framework dictating how all networked devices will send, receive and interpret data.

One of the main benefits of the OSI model is that devices can have different functions and designs on a network while communicating with other devices. Data sent across a network that follows the uniformity of the OSI model can be understood by other devices.

The OSI Model consists of 7 layers. Each layer has a different set of responsibilities and is arranged from layer 7 to 1.

> At every individual layer that data travels through, specific processes take place, and pieces of information are added to this data. 
> 	For now, all we need to understand is that this process is called **encapsulation** and what the OSI model looks like in the diagram above.

#### Layer 7: Application

The application layer of the OSI model is the layer that you will be most familiar with. 

This familiarity is because the application layer is the layer in which protocols and rules are in place to determine how the user should interact with data sent or received. 

Everyday applications such as email clients, browsers or file server browsers such as FileZilla provide a friendly, GUI for users to interact with data sent or received.

- Other protocols include **DNS**, which is how website addresses are translated into IP Addresses.

#### Layer 6: Presentation

> Layer 6 of the OSI model is the layer in which standardization starts to take place. Because software developers can develop any software such as an email client differently, the data still needs to be handled in the same way -- no matter how the software works.

This layer acts a a *translator for data to and from the application layer*. The receiving computer will also understand data sent to a computer in one format destined for in another format. For example, when you send an email, the other user may have another email client for you, but the contents of the email still need to display the same.

Security features such as data encryption (like HTTPS when visiting a secure site) occur at this layer.

#### Layer 5: Session

> Once data has been correctly translated or formatted from the presentation layer (layer 6), the session layer will begin to create a connection to the other computer that the data is destined for.
> 	When a communication is established, a session is created. Whilst this connection is active, so is the session.

The session layer synchronizes the two computers to ensure that they are on the same page before data is sent and received. Once these checks are in place, the session layer will begin to divide up the data sent into smaller chunks (packets) one at a time. 

- This dividing up is beneficial because if the connection is lost, only the chunks that weren't yet sent will have to be sent again -- not the entire piece of data (think of it like loading a save file in a videogame).

What is worthy of noting is that sessions are unique -- meaning that data cannot travel over different sessions, but in face, only across each session instead.

#### Layer 4: Transport

> Layer 4 of the OSI model plays a vital part in transmitting data across a network and can be a little bit difficult to grasp.
> 	When data is sent between devices, it follows one of two different protocols that are decided based on several factors:

- TCP
- UDP

The **Transmission Control Protocol** is designed with reliability and guarantee in mind. This protocol reserves a constant connection between the two devices for the amount of time it takes for the data to be sent and received. 

- Not only this, but TCP incorporates error checking into its design. Error checking is how TCP can guarantee that data sent from the small chunks in the session layer has then been received and reassembled in the same order.

| Advantages of TCP                                                                        | Disadvantages of TCP                                                                                                                          |
| ---------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Guarantees the accuracy of data/                                                         | Requires a reliable connection between two devices. If one small chunk of data is not received, then the entire chunk of data cannot be used. |
| Capable of synchronizing two devices to prevent each other from being flooded with data. | A slow connection can bottleneck another device as the connection will be reserved on the receiving computer the whole time.                  |
| Performs a lot more processes for reliability.                                           | TCP is significantly slower than UDP because more work has to be done by the devices using this protocol.                                     |
> TCP is used for functions such as file sharing, internet browsing or sending an email. This usage is because these services require the data the be accurate and complete (no good having half a file.)

 The **User Datagram Protocol** is not nearly advanced as its brother - the TCP protocol. 

- It doesn't boast the many features offered by TCP, such as error checking and reliability. In fact, any data that gets sent via UDP is sent to the computer whether it gets there or not. 
- There is no synchronization between the two devices or guarantee; just hope for the best, and fingers crossed. 

Whilst this sounds disadvantageous, it does have it's merits, which we'll layout in the table below:

| Advantages of UDP                                                                                                     | Disadvantages of UDP                                                               |
| --------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| UDP leaves the application layer (user software) to decide if there is any control over how quickly packets are sent. | UDP doesn't care if the data is received.                                          |
| UDP does not reserve a continuous connection on a device as TCP does.                                                 | It is quite flexible to software developers in this case.                          |
| UDP does not reserve a continuous connection on a device as TCP does.                                                 | This means that unstable connections result in a terrible experience for the user. |
> UDP is useful in situations where there are small pieces of data being sent. For example, protocols used for discovering devices (ARP and DHCP) or larger files such as video streaming, where it is okay if some part of the video becomes pixelated. Pixels are just lost pieces of data. 

#### Layer 3: Network

> Where the magic of routing and re-assembly of data takes place (from these small chunks to the larger chunk)
> 	Firstly, routing simply determines there most optimal path in which these chunks of data should be sent. 

Whilst some protocols at this layer determine exactly what is the optimal path that data should take to reach a device, we should only know about their existence at this stage of the networking module. 

- Briefly, these protocols include **OSPF (Open Shortest Path First)** and **RIP (Routing Information Protocol)**. The factors that decide what route is taken is decided by the following:

	- What path is the shortest? (The least amount of device the packet needs to travel across)
	- What path is the most reliable (Have packets been lost on that path before?)
	- Which path has the faster physical connection (Is one path using a copper connection or a fiber connection?)

>At this layer, everything is dealt with via IP addresses such as 192.168.1.100. Devices such as routers capable of delivering packets using IP addresses are known as layer 3 devices -- because they are capable of working at the third layer of the OSI model.

#### Layer 2: Data Link

> The data link layer focuses on the physical addressing of the transmission.

It receives a packet from the network layer (including the IP address for the remote computer) and adds in the physical **MAC** address of the receiving endpoint. 

Inside every network enabled computer is a network interface card (NIC) which comes with a unique MAC address to identify it.

MAC addresses are set by the manufacturer and literally burnt into the card, they can't be changed, although they can be spoofed. 
- When information is sent across a networks it's actually the physical address that is used to identify where exactly to send the information. 

#### Layer 1: Physical

> This layer is one of the easiest to grasp. Put simply, this layer refers to the physical components of the hardware used in networking and is the lowest layer that you will find. 
> 	Devices uses electrical signals to transfer data between each other in a binary number system.

# Packets and Frames

> Packets and frames are small pieces of data that, when forming together, make a larger piece of information or message. 

However, they are two different things in the OSI model. A frame is at layer 2, the data link layer, meaning there is no such information as IP addresses. 

Think of it as putting an envelope within an envelope within an envelope and sending it away.
- The first envelope will be that packet that you mail, but once it is opened, the envelope still exists and contains data (this is a **frame**)

This process is called **encapsulation**. 

At this stage, its safe to say that if we are talking about anything regarding IP addresses, we are talking about packets. 

- When encapsulating information is stripped away, we're talking about the frame itself.

*Packets are an efficient way of communicating data across networked devices*. 
Because this data is exchanged in small pieces, there is less chance of bottlenecking occurring across a network than large messages all being sent at once.

Packets have different structures that are dependent upon the type of packet that is being sent. As we'll come on to discuss, networking is full of standards and protocols that act as a set of rules for how the packet is handled on a device. 
- With the Internet predicted to have approx. 50 billion devices connected by the end of 2020, things quickly get out of hand if there is no standardisation.

A packet using the Internet Protocol will have a set of headers that contain additional pieces of information to the data that is being sent across the network.

| Header              | Description                                                                                                                                                  |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Time to Live        | This field sets an expiry timer for the packet to not clog up the network if it never manages to reach a host or escapes.                                    |
| Checksum            | Provides integrity checking for protocols such as TCP/IP. If any data is changed, this value will be different from what was expected and therefore corrupt. |
| Source Address      | The IP address of the device that the packet is being sent **from** so that data knows where to **return to**.                                               |
| Destination Address | The device's IP address that the packet is being sent so that data knows where to travel next.                                                               |
### TCP/IP (Three-Way Handshake)

**Transmission Control Protocol (TCP)** is another one of these rules used for networking. 

The protocol is very similar to the OSI model that we have previously discussed in room three of this module so far. 

The TCP/IP protocol consists of four layers and is arguably just a summarized version of the OSI model.

- Application
- Transport
- Internet
- Network Interface

One defining feature of TCP is that it is **connection-based** , which means that TCP must establish a connection between both a client and da device acting as a server before data is sent. 

Because of this, TCP guarantees that any data sent will be received on the other end. This process is named the three-way handshake. 

TCP Packets contain various sections of information known as headers that are added from encapsulation. Let's explain some of the crucial headers in the table below:

| Header                 | Description                                                                                                                                                                                                                                         |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Source Port            | This value is the port opened by the sender to send the TCP packet from. This value is chosen randomly from the ports 0-65535 that aren't already in use at the time.                                                                               |
| Destination Port       | This value is the port number that an application or service is running on the remote host (the one receiving data); for example, a webserver running on port 80. Unlike the source port, this value is not chosen at random.                       |
| Source IP              | This is the IP address that is sending the packet.                                                                                                                                                                                                  |
| Destination IP         | This is the IP address of the device that the packet is destined for.                                                                                                                                                                               |
| Sequence Number        | When a connection occurs, the first piece of data transmitted is given a random number. We'll explain this more in-depth further on.                                                                                                                |
| Acknowledgement Number | After a piece of data has been given as sequence number, the number for the next piece of data will have the sequence number +1.                                                                                                                    |
| Checksum               | This value is what gives TCP integrity. A mathematical calculation is made where the output is remembered. When the receiving device performs the mathematical calculation, the data must be corrupt if the output is different from what was sent. |
| Data                   | This header is where the data, i.e. bytes of a file that is being transmitted, is stored.                                                                                                                                                           |
| Flag                   | This header determines how the packet should be handled by either device during the handshake process. Specific flags will determine specific behaviours, which is what we'll come on to explain below.                                             |
> Next, we come to the *three way handshake*, a term given for the process used to establish a connection between two devices. The Three-Way handshake communicates using a few special messages -- the table below highlights the main ones. 

| Step | Message | Description                                                                                                                                                                                                                                        |
| ---- | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1    | SYN     | A SYN message is the initial packet sent by a client during the handshake. This packet is used to initiate a connection and synchronize the two devices together                                                                                   |
| 2    | SYN/ACK | This packet is sent by the receiving device (server) to acknowledge the synchronization attempt from the client                                                                                                                                    |
| 3    | ACK     | The acknowledgment packet can be used by either the client or server to acknowledge that a series of messages/packets have been successfully received.                                                                                             |
| 4    | DATA    | Once a connection has been established, data is sent via the DATA message                                                                                                                                                                          |
| 5    | FIN     | This packet is used to cleanly close the connection after is has been complete                                                                                                                                                                     |
| #    | RST     | This packet abruptly ends all communication. This is the last resort and indicates there was some problem during the process. For example, if the service or application is not working correctly, or the system has faults such as low resources. |
Any data sent is given a random number sequence and is reconstructed using this number sequence and incrementing by 1. Both computers must agree on the same number sequence for data to be sent in the correct order. This order is agreed upon during three steps.

1. **SYN**-Client: Here's my Initial Sequence Number (ISN) to **SYN**chronize with (0)
2. **SYN/ACK**-Server: Here's my Initial Sequence Number (ISN) to **SYN**chronise with (5,000), and I **ACK**knowledge your initial number sequence.
3. **ACK**-Client: I **ACK**nowledge your Initial Sequence Number (ISN) of (5,000), here is some data that is my ISN+1 (0+1)

**TCP Closing a Connection**

Let's quickly explain the process behind TCP closing a connection. 

First, TCP will close a connection once a device has determined that the other device has successfully received all of its data.

Because TCP reserves system resources on a device, it is best practice to close TCP connections as soon as possible.
- To initiate the closure of a TCP connection, the device will send a "**FIN**" packet to the other device. 
- Of course, with TCP, the other device will also have to acknowledge this packet. 

### UDP/IP

The **User Datagram Protocol** is another protocol that is used to communicate data between devices. 

Unlike its brother TCP, UDP is a **stateless** protocol that doesn't require a constant connection between two devices for data to be sent. 

- For example, the Three-Way handshake does not occur, nor is there any synchronization between the two devices. 

Recall some of the comparisons made about these two protocols in Room 3: "OSI Model". Namely UDP is used in situations where applications can tolerate data being lost (such as video streaming or voice chat) or in scenarios where applications can tolerate data being lost (such as video streaming or voice chat) or in scenarios where an unstable connection is not the end-all.

As mentioned, no process takes place in setting up a connection between two devices. Meaning that there is no regard for whether or not data is received, and there are no safeguards such as those offered by TCP, such as data integrity. 

UDP Packets are much simpler than TCP packets and have fewer headers.
- However, both protocols share some standard headers, which are annotated below:

| Header              | Description                                                                                                                                                                                                                       |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Time to Live (TTL)  | This field sets an expiry timer for the packet, so it doesn't clog up your network if it never manages to reach a host or escape.                                                                                                 |
| Source Address      | The IP address of the device that the packet is being sent from, so that data knows where to return to.                                                                                                                           |
| Destination Address | The device's IP address the packet is being sent to so that data knows where to travel next.                                                                                                                                      |
| Source Port         | This value is the port that is opened by the sender to send the UDP packet from. This value is randomly chosen (out of the ports from 0-65355 that aren't already in use at the time.)                                            |
| Destination Port    | This value is the port number that an application or service is running on the remote host (the one receiving the data); for example, a webserver running on port 80. Unlike the source port, this value is not chosen at random. |
| Data                | This header is where data, i.e. bytes of a file that is being transmitted, is stored.                                                                                                                                             |
### Ports 101

> Ports are an essential point in which data can be exchanged. Think of a harbor and a port. 
> 	Ships wanting to dock at the harbor will have to go to a port compatible with the dimensions and facilities located on the ship.
> 	When the ship lines up, it will connect to the **ports** at the harbor.

A cruise ship cannot dock at a port made for a fishing vessel, and so on.

*Ports enforce what can park and where, if it isn't compatible, it can't park there.*

Networking devices also use ports to enforce strict rules when communicating with one another. When a connection has been established (recalling from the OSI Model's room), any data sent or received by a device will be sent through these ports. In computing, ports are a numerical value between 0 and 65355.

Because ports can use a range of anywhere between 0-65355, there quickly runs the risk of losing track of what application is using what port. 

- Thankfully, we associate applications, software and behaviors with a standard set of rules. 
- For example, by enforcing that any web browser data is sent over port 80, software developers can design a web browser such as Chrome or Firefox to interpret the data the same way as one another.

> While the standard rule for web data is port 80, a few other protocols have been allocated a standard rule. Any port that is within 0 and 1024 is known as a common port. Let's explore some of these other protocols below.

| Protocol                           | Port Number | Description                                                                                                                 |
| ---------------------------------- | ----------- | --------------------------------------------------------------------------------------------------------------------------- |
| File Transfer Protocol             | 21          | Used by a file-sharing application built on a client server model, meaning you can download files from a central location.  |
| Secure Shell                       | 22          | Used to securely login to systems via a text based interface for management.                                                |
| Hypertext Transfer Protocol        | 80          | Powers the world wide web, your browser uses this to download text, images and videos of web pages.                         |
| Hypertext Transfer Protocol Secure | 443         | Does the exact same thing as HTTP, this time using encryption.                                                              |
| Server Message Block               | 445         | Similar to FTP, but as well as files, you can share devices like printers.                                                  |
| Remote Desktop Protocol            | 3389        | Secure means of logging in to a system using a visual desktop interface (as opposed to SSH and it's text based limitations) |
> It is worth noting that these protocols only follow the standards. I.e. you can administer applications that interact with these protocols on a different port other than what is the standard. 
> 	Note, however, applications will presume that the standard is being followed, so you will have to provide a **colon (:)** along with the port number.

# Introduction to Port Forwarding

Port forwarding is an essential component in connecting applications and services to the internet. 

>Without port forwarding, applications and services such as web servers are only available to devices within the same direct network.

It is easy to confuse port forwarding with the behaviors of a firewall. 
- However, at this stage, just understand that port forwarding opens specific ports. 
- In comparison, firewalls determine if traffic can travel across these ports (even if they are opened via port forwarding.)

### Firewalls 101

> A firewall is a device within a network responsible for determining what traffic is allowed to enter and exit.

Think of a firewall as border security for a network.

An administrator can configure a firewall to **permit** or **deny** traffic from entering or exiting a network based on numerous factors such as:

- Where is the traffic coming from? Has the firewall been told to accept/deny traffic from a specific network?
- Where is the traffic going to? Has the firewall been told to accept/deny traffic destined for a specific network?
- What port is the traffic for? Has the firewall been told to accept/deny traffic destined for port 80 only?
- What protocol is the traffic using? Has the firewall been told to accept/deny traffic that is UDP, TCP or both?

> Firewalls perform packet inspection to determine the answers to these questions.

Two Primary categories of firewalls:

| Firewall Category | Description                                                                                                                                                                                                                     |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Stateful          | This type of firewall uses the entire information from a connection; rather than inspecting an individual packet, this firewall determines the behavior of a device **based upon the entire connection**.                       |
|                   | This firewall type consumes many resources in comparison to stateless as the decision making is dynamic. For example, a firewall could allow the first parts of a TCP handshake that would later fail.                          |
|                   | If a connection from a host is bad, it will block the entire device.                                                                                                                                                            |
| Stateless         | Firewall type that uses a static set of rules to determine whether or not individual packets are acceptable or not. For example, a device sending a bad packet will not necessarily mean that the entire device is blocked.     |
|                   | While these firewalls use much fewer resources than alternatives, they are much dumber. These firewalls are only as effective as the rules that are defining them. If a rule is not exactly matched, it is effectively useless. |
|                   | However, these firewalls are great when receiving large amounts of traffic from a set of hosts, such as a DDoS attack.                                                                                                          |
### VPN Basics

> A **Virtual Private Network** is a technology that allows devices on separate networks to communicate securely by creating a dedicated path between each other over the Internet (known as a **tunnel**).

Devices connected within this tunnel form their own private network.

A VPN could allow to offices to be connected. 

There are three networks in this image:

1. Network 1 (Office 1)
2. Network 2 (Office 2)
3. Network 3 (Two devices connected via VPN)

The devices connected on Network #3 are still a part of Network #1 and Network #2 but also form together to create a private network (Network #3) that only devices that are connected via this VPN can communicate over.

| Benefit                                                              | Description                                                                                                                                                                                                                 |
| -------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Allows networks in different geographical locations to be connected. | A business with multiple offices will find VPNs beneficial, as it means that resources like servers/infrastructure can be accessed from another office.                                                                     |
| Offers privacy                                                       | VPN technology uses encryption to protect data. This means it can only be understood between the devices it was being sent from and is destined for, meaning the data isn't vulnerable to sniffing.                         |
| Offers anonymity                                                     | Journalists and activists depend upon VPNs to safely report on global issues in countries where freedom of speech is controlled.                                                                                            |
|                                                                      | Usually, your traffic can be viewed by your ISP and other intermediaries and, therefore, tracked.                                                                                                                           |
|                                                                      | The level of anonymity a VPN provides is only as much as how other devices on the network respect privacy. For example, a VPN that logs all of your data/history is essentially the same as not using a VPN in this regard. |
> Some existing VPN technologies:

| VPN   | Description                                                                                                                                                                                                                                                               |
| ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| PPP   | Used to allow authentication and provide encyption of data. VPNs work by using a private key and public certificate (similar to SSH). a private key and certificate must match for you to connect. This tech is not capable of leaving a network by itself (non-routable) |
| PPTP  | The **Point to Point Tunnel Protocol** is the technology that allows the data from PPP to travel and leave a network. PPTP is very easy to set up and is supported by most devices. It is, however, weakly encrypted in comparison to alternatives.                       |
| IPSec | **Internet Protocol Security** encrypts data using the existing IP framework. IPSec is difficult to set up in comparison, however, if successful, it boasts strong encryption and is also supported on many devices.                                                      |

### LAN Network Devices

**What is a Router?**

> It's a routers job to connect networks and pass data between them.
> 	It does this by using routing. 

Routing is the label given to the process of data travelling across networks. Routing involves creating a path between networks so that this data can be successfully delivered. 

Routers operate at level 3 of the OSI model. They often feature an interactive interface (such as a website or a console) that allows an administrator to configure various rules such as port forwarding or firewalling.

Routers are dedicated devices and do not perform the same functions as switches. 

Different protocols determine the path for data to be taken, but factors include:

- What path is the shortest?
- What path is the most reliable?
- Which path has the faster medium? Copper of fiber?

**What is a Switch?**

>A switch is a dedicated networking device responsible for providing a means of connecting to multiple devices. Switches can facilitate many devices (from 3 to 63) using Ethernet cables. 

Switches can operate at both layer one and layer two of the OSI model. However, these are exclusive in the sense that Layer 2 switches cannot operate at layer 3.

Take, for example, a layer 2 switch in the diagram below. These switches will forward frames (remember these are no longer packets as the IP protocol has been stripped) onto the connected devices using their MAC address.

**Layer 3 Switches** 

> These switches are more sophisticated than Layer 2, as they can perform some of the responsibilities of a router. 
> 	Namely, these switches will send frames to devices (as layer 2 does) and route packets to other devices using the IP protocol.

A technology called **VLAN** or **Virtual Local Area Network** allows specific devices within a network to be virtually split up. 

This split means they can all benefit from things such as an Internet connection but are treated separately. This network separation provides security because it means that rules in place determine how specific devices communicate with each other. This segregation is illustrated in the diagram above:

> The Sales Department and Accounting Department will be able to access the internet but not be able to access each other.

# How the Web Works

### DNS in Detail

> **DNS (Domain Name System)** provides a simple way for us to communicate with devices on the internet without remembering complex numbers. 

Much like every house has a unique address for sending mail directly to it, every computer on the internet has its own unique address to communicate with it called an IP address. 

When accessing a website, it's not exactly optimal to have to remember the whole IP address, and that's where DNS can help. Instead of tryhackme's IP address, you just remember tryhackme.com

### Domain Hierarchy

**TLD (Top Level Domain)**

> A TLD is the most righthand part of a domain name. So, for example, the tryhackme.com TLD is **.com**. There are two types of TLD, gTLD (Generic Top Level) and ccTLD (Country Code Top Level Domain).

Historically a gTLD was meant to tell the user the domain name's purpose; for example, a .com would be for commercial purposes, .org for an organization, .edu for education and .gov for government.

A ccTLD was used for geographical purposes, for example, .ca for sites based in Canada, .co.uk for sites based in the United Kingdom, and so on.
- Due to so much demand, there is an influx of new gTLDs ranging from .online, .club, .website, . biz and so many more. 

**Second-Level Domain**

Taking tryhackme.com as an example, the .com part is the TLD, and tryhackme is the *Second Level Domain*.

When registering a domain name, the second-level domain is limited to 63 characters + the TLD and can only use a-z 0-9 and hyphens (cannot start or end with hyphens or have consecutive hyphens)

**Subdomain**

A subdomain sits on the left-hand side of the Second-Level Domain using a period to separate it; for example, in the name admin.tryhackme.com the **admin** part is the *subdomain*. 

A subdomain has the same creation restrictions as a Second-Level Domain, being limited to 63 characters and can only use a-z 0-9 and hyphens (and cannot start or end with hyphens or have consecutive hyphens)

You can use multiple subdomains split with periods to create longer names, such as jupiter.server.tryhackme.com
- But the length must be kept to 253 characters or less
- There is no limit to the number of subdomains you can create for your domain name.

### DNS Record Types

>DNS isn't just for websites though, and multiple types of DNS record exist. 

**A Record**

> These records resolve to IPv4 addresses.

**AAAA Record**

>These records resolves to IPv6 addresses

**CNAME Record** 

> These records resolve to another domain name, for example TryHackMe's online shop has the subdomain name store.tryhackme.com which returns a CNAME record shops.shopify.com
> 	Another DNS request would then be made to shops.shopify.com to work out the IP address.

**MX Record**

>These records resolves to the address of the servers that handle the email for the domain you are querying, for example an MX record response for tryhackme.com would look something like alt1.aspmx.l.google.com. 
>	These records also come with a priority flag. 
>	This tells the client in which order to try the servers, this is perfect for if the main server goes down and email needs to be sent to a backup server.

**TXT Record**

>TXT Records are free text fields where any text-based data can be stored. TXT records have multiple uses, but some common ones can be to list servers that have the authority to send an email on behalf of the domain (this can help in the battle against spoofed email). They can also be used to verify ownership of the domain name when signing up for third party services.

### Making a Request

1. When you request a domain name, your computer first checks its local cache to see if you've previously looked up the address recently; if not, a request to your Recursive DNS server will be made.
2. A Recursive DNS server is usually provided by your ISP, but you can choose your own. This server also has a local cache of recently looked up domain names. If a result is found locally, this is sent back to your computer, and your request ends here. 
		If the request cannot be found locally, a journey begins to find the correct answer, starting with internet's root DNS servers.
3. The root servers act as the DNS backbone of the internet; their job is to redirect you to the correct Top Level Domain Server, depending on your request. If, for example, you request www.tryhackme.com, the root server will recognize the Top Level Domain of .com and refer you to the correct TLD server that deals with .com addresses.
4. The TLD server holds records for where to find the authoritative server to answer the DNS request. The authoritative server is often known as the **nameserver** for the domain. 
		For example, the name server for tryhackme.com is kip.ns.cloudflare.com and uma.ns.cloudflare.com. 
		You'll often find multiple nameservers for a domain name to act as a backup in case one goes down.
5. An authoritative DNS server is the server that is responsible for storing the DNS records for a particular domain name and where any updates to your domain name DNS records would be made. Depending on the record type, the DNS record is then sent back to the Recursive DNS Server, where a local copy will be cached for future requests and then relayed back to the original client that made the request. DNS records all come with a TTL (time to live) value.
		This value is a number represented in seconds that the response should be saved for locally until you have to look it back up again. 
		Caching saves on having to make a DNS request every time you communicate with a server.

## HTTP In Detail

**What is HTTP?**

> HTTP is what's used whenever you view a website, developed by Tim Burners-Lee and his team between 1989-1991. 
> 	HTTP is the set of rules used for communicating with web servers for the transmitting of webpage data, whether that is HTML, Images, Videos, etc.

**What is HTTPS**

> HTTPS is the secure version of HTTP. HTTPS data is encrypted so it not only stops people from seeing the data you are receiving and sending, but it also gives you assurances that you're talking to the correct web server and not something impersonating it.

### Requests and Responses

> When we access a website, your browser will need to make request to a web server for assets such as HTML, Images and download the responses. Before that, you need to tell the browser specifically how and where to access these resources, this where URLs will help.

**What is a URL?**

> If you've used the internet, you've used a URL before. A **Uniform Resource Locator** is predominantly an instruction on how to access a resource on the internet. 

**Scheme**: This instructs on what protocol to use for accessing the resource such as HTTP, HTTPS, FTP (File Transfer Protocol)
**User**: Some services require authentication to log in, you can put a username and password into the URL to log in. 
**Host**: The domain name or IP address of the server you wish to choose.
**Port**: The Port that you are going to connect to, usually 80 for HTTP and 443 for HTTPS, but this can be hosted on any port between 1-65355. 
**Path**: The file name or location of the resource you are trying to access.
**Query String**: Extra bits of information that can be sent to the requested path. For example, /blog**id=1** would tell the blog path that you wish to receive the blog article with the id of 1.
**Fragment**: This is a reference to a location on the actual page requested. This is commonly used for pages with long content and can have a certain part of the page directly linked to it, so it is viewable to the user as soon as they access the page.

**Making a Request**

It's possible to make a request to a web server using just one line "`get/http/1.1`"

But for a much richer experience, you'll need to send other data as well. This other data is sent in what is called headers, where headers contain extra information to give to the web server you're communicating with, but we'll go more into this in the Header task.

**Example Request**:

```http
GET / HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0 Firefox/87.0
Referer: https://tryhackme.com/
 
```
> To breakdown each line of this request:

Line 1: This request is sending the GET method, request the home page with / and telling the web server we are using HTTP protocol version 1.1.

Line 2: We tell the web server we want the website tryhackme.com

Line 3: We tell the web server we are using Firefox 87 browser.

Line 4: We are telling the web server that the web page that referred us to this one is https://tryhackme.com

Line 5: HTTP requests always end with a blank line to inform the web server that the request has finished. 

### HTTP Methods

> HTTP Methods are a way for the client to show their intended action when making an HTTP request.
> 	There are a lot of HTTP methods but we'll cover the most common ones, although mostly you'll deal with the GET and POST method.

**GET Request**

This is used for getting information from a web server

**POST Request**

This is used for submitting data to the web server and potentially creating new records

**PUT Request**

This is used for submitting data to a web server to update information.

**DELETE Request**

This is used for deleting information/records from a web server

### HTTP Status Codes

> In the previous task, you learned that when a HTTP server responds, the first line always contains a status code informing the client of the outcome of their request and also potentially how to handle it. 

These status codes can be broken down into 5 different ranges:

*100-199 - Information Response:* These are sent to tell the client the first part of their request has been accepted and they should continue sending the rest of their request. These codes are no longer very common. 

*200-299 - Success*: This range of status codes is used to tell the client their request was successful. 

*300-399 - Redirection*: These are used to redirect the client's request to another resource. This can be either to a different webpage or a different website altogether. 

*400-499 - Client Errors*: Used to inform the client that there was an error with their request.

*500-599 - Server Errors*: This is reserved for errors happening on the server-side and usually indicate quite a major problem with the server handling the request.

##### Common HTTP Status Codes

*200 - OK*: The request was completed successfully. 
*201 - Created*: A resource has been created
*301 - Moved Permanently*: This redirects the client's browser to a new webpage or tells search engines that the page has moved somewhere else and to look there instead.
*302 - Found*: Similar to the above permanent redirect, but as the name suggests, this is only a temporary change and it may change again in the near future.
*400 - Bad Request*: This tells the browser that something was either wrong or missing in their request. This could sometimes be used if the web server resource that is being requested expected a certain parameter that the client didn't send.
*401 - Not Authorized*: You are not currently allowed to view this resource until you have authorized with the web application, most commonly with a username and password.
*403 - Forbidden*: You do not have permission to view this resource whether you are logged in or not.
*405 - Method Not Allowed*: The resource does not allow this method request, for example, you sent a GET request to the resource /create-account when it was expecting a POST request instead.
*404 - Page Not Found*: The page/resource you requested does not exist. 
*500 - Internal Service Error*: The server has encountered some kind of error with your request that it doesn't know how to handle properly. 
*503 - Service Unavailable*: This server could not handle your request as it's either overloaded or down for maintenance. 

### Headers

Headers are additional bits of data you can send to the web server when making requests.

Although no headers are strictly required when making a HTTP request, you'll find it difficult to view a website properly.

##### Common Request Headers

These are headers that are sent from the client (usually your browser) to the server.

**Host**: Some web servers host multiple websites so by providing the host headers you can tell it which one you require, otherwise you'll just receive the default website for the server. 

**User-Agent**: This is your browser software and version number, telling the web server your browser software helps it format the website properly for your browser and also some elements of HTML, JavaScript and CSS are only available in certain browsers.

**Content-Length**: When sending data to a web server such as in a form, the content-length tells the web server how much data to expect in the web request. This way the server can ensure it isn't missing any data. 

**Accept-Encoding**: Tells the web server what types of compression methods the browser supports so the data can be made smaller for transmitting over the internet.

**Cookie**: Data sent to the server to help remember your information (see cookies task for more information.)

##### Common Response Headers

> These are the headers that are returned to the client from the server after a request.

**Set-Cookie**: Information to store which gets sent back to the web server on each request (see cookies task for more information)

**Cache-Control**: How long to store the content of the response in the browser's cache before it requests again. 

**Content-Type**: This tells the client what type of data is being returned, i.e. HTML, CSS, JavaScript, Images, PDF, Video, etc. Using the content type header the browser then knows how to process the data. 

**Content-Encoding**: What method has been used to compress the data to make it smaller when sending it over the internet. 

### Cookies

> You've probably heard of cookies before, they're just a small piece of data that is stored on your computer. Cookies are saved when you receive a "Set-Cookie" header from a web server. 

Then every further request you make, you'll send the cookie data back to the web server. Because HTTP is stateless (doesn't keep track of your previous requests), cookies can be used to remind the web server who you are, some personal settings for the website or whether you've been to the website before. 

Let's take a look at this as an example HTTP Request:

> Cookies can be used for many purposes but are most commonly used for website authentication. The cookie value won't usually be a clear-text string where you can see the password, but a token (unique secret code that isn't easily humanly guessable).

**Viewing Your Cookies**

> You can easily view what cookies your browser is sending to a website by using the developer tools, in your browser. 
> 	Once you have the dev tools open, click on the network tab. This tab will show you a list of all the resources your browser has requested. You can click on each one to receive a detailed breakdown of the request and response. If your browser sent a cookie, you will see these on the "Cookies" tab of the request.

## How Websites Work

> When you visit a website, your browser (like Safari or Google Chrome) makes a request to a web server asking for information about the page you're visiting. It will respond with data that your browser uses to show you the page; a web server is just a dedicated computer somewhere else in the world that handles your request. 

There are two major components that make up a website:

1. Front-end (Client-Side) - the way your browser renders a website
2. Back-end (Server-Side) - a server that processes your request and returns a response

There are many other processes involved in your browser making a request to a web server, but for now, you just need to understand that you make a request to a server, and it responds with data your browser uses to render information to you.

### HTML

Websites are primarily created using:

- HTML, to build websites and define their structure
- CSS, to make websites look pretty by adding styling options
- JavaScript, implement complex features on pages using interactivity.

**Hypertext Markup Language (HTML)** is the language websites are written in. Elements (known as tags) are the building blocks of HTML pages and tells the browser how to display content. 

The HTML Structure has the following components:

- The `<!DOCTYPE html>` defines that the page is an HTML5 document. This helps with standardization across different browsers and tells the browser to use HTML5 to interpret the page.
- The `<html>` element is the root element of the HTML page - all other elements comes after this element.
- The `<head>` element contains information about the page (such as the page title)
- The `<body>` element defines the HTML document's body; only content inside of the body is shown in the browser.
- The `<p>` element defines a paragraph
- There are many other different tags used for different purposes. For example, there are tags for `<button>`, images `<img>`, lists and much more.

Tags can contain attributes such as the class attribute which can be used to style an element (make the take a different color, e.g.) `<p class="bold-text">` or the *src* attribute which is used on images to specify the location of an image: `<img src="img/cat.jpg">`. An element can have multiple attributes each with its own unique purpose, e.g. `<p attribute1="value1" attribute2="value2">`

Elements can also have an id attribute `<p id="example">`, which is unique to the element. Unlike the class attribute, where multiple elements can use the same class, an element must have different id's to identify them uniquely. 
- Element IDs are sued for styling and to identify it by JavaScript

### JavaScript

> JavaScript is one of the most popular coding languages in the world and allows pages to become interactive. HTML is used to create the website structure and content, while JavaScript is used to control the functionality of web pages - without JavaScript, a page would not have interactive elements and would always be static. 

JS can dynamically update the page in real-time, giving functionality to change the style of a button when a particular event on the page occurs (such as when a user clicks a button) or to display moving animations. 

JavaScript is added within the page source doe and can either loaded within `<script>` tags or can be included remotely with the src attribute: <script src="/location/of/javascript_file.js"></script>

The following JS code find an HTML element on the page with the id of "demo" and changes the element's contents to "Hack the Planet"

```
: document.getElementbyId("demo").innerHTML = "Hack the Planet";
```

HTML elements can also have events, such as "onclick" or "onhover" that execute JavaScript when the event occurs. The following code changes the text of the element with the demo ID to Button Clicked: <button onclick='document.getElementById(
demo").innerHTML = "Button Clicked;"'>Click Me!</button> 

- On click events can also be defined inside the JavaScript script tags, an not on elements directly.

### Sensitive Data Exposure

> Occurs when a website doesn't properly protect (or remove) sensitive clear-text information to the end-user; usually found in a site's frontend source code. 

We now know that websites are built using many HTML elements (tags), all of which we can see simply by "viewing the page source". A website developer may have forgotten to remove login credentials, hidden links to private parts of the website or other sensitive data shown in HTML or JavaScript.

Sensitive infomation can be potentially leveraged to further an attacker's access within different parts of a web application. For example, there could be HTML comments with temporary login credentials, and if you viewed the page's source code and found this, you could use these creds to log in elsewhere on the application (or worse, used to access other backend components of the site.)

Whenever you're assessing a web application for security issues, one of the first things you should do is review the page source code to see if you can find any exposed login credentials or hidden links.

### HTML Injection

> HTML Injection is a vulnerability that occurs when unfiltered user input is displayed on the page. 

If a website fails to sanitise user inputs (filter any "malicious text" that a user inputs into a website), and that input is used on the page, an attacker can inject HTML code into a vulnerable website.

Input sanitization is very important in keeping a website secure, as information a user inputs into a website is often used in other frontend and backend functionality. A vulnerability you'll explore later is database injection. where you can manipulate a database lookup query to log in as another user by controlling the input that's directly used in the query.
- For now, we'll focus on HTML injection (which is client-side)

> When a user has control of how their input is displayed, they can submit HTML (or JavaScript) code, and the browser will use it on the page, allowing the user to control the page's appearance and functionality. 

The general rule is to *never trust user input*. To prevent malicious input, the website developer should sanitize everything the user enters before using it in the JavaScript function; in this case, the developer could remove any HTML tags.

## Putting it All Together

> To summarize, when you request a website, your computer needs to know the server's IP address it needs to talk to; for this, it uses DNS. Your computer then talks to the web server using a special set of commands called the HTTP protocol; the webserver then returns HTML, CSS, Images, etc. which your browser then uses to correctly format and display the website to you.

### Other Components

When a website's traffic starts getting quite large or is running an application that needs to have high availability, one web server might no longer do the job. 

**Load Balancers** provide two main features, ensuring high traffic websites can handle the load and providing a failover if a server becomes unresponsive.

When you request a website with a load balancer, the load balancer will receive your request first and then forward it to one of the multiple servers behind it. 
- The load balancer uses different algorithms to help it decide which server is best to deal with the request. 

A couple examples of these algorithms are **round-robin**, which sends it to each server in turn, or **weighted**, which checks how many requests a server is currently dealing with and sends it to the least busy server. 

Load Balancers also perform periodic checks with each server to ensure they are running correctly; this is called a **health check**. If a server doesn't respond appropriately or doesn't respond, the load balancer will stop sending traffic until it responds appropriately again. 

##### CDN (Content Delivery Network)

> A CDN can be an excellent resource for cutting down traffic to a busy website. It allows you to how static files from your website, such as a JavaScript, CSS, Images, Videos and host them across thousands of servers all over the world.
> 	When a user requests one of the hosted files, the CDN works out where the nearest server is physically located and sends the request there instead of potentially the other side of the world. 

##### Databases

> Often websites will need a way of storing information for their users. Webservers can communicate with databases to store and recall data from them. Databases can range from just a simple plain text file to complex clusters of multiple servers providing speed and resilience. 

You'll come across some common databases: MySQL, MSSQL, MongoDB, GraphQL, Postgres and 
more; each has specific features.

##### WAF (Web Application Firewall) 

> A WAF sits between your web request and the web server; its primary purpose is to protect the webserver from hacking or denial of service attacks. 

It analyzes the web requests for common attack techniques, whether the request is from a real browser rather than a bot. 

It also checks if an excessive amount of web requests are being sent by utilizing something called **rate limiting**, which will only allow a certain amount of requests from an IP per second. If a request is deemed a potential attack, it will be dropped and never sent to the webserver.

### How Web Servers Work

A web server is a software that listens for incoming connections and the utilizes the HTTP Protocol to deliver web content to its clients. 

The most common web server software you'll encounter is Apache, Nginx, IIS and Node.js

A web server delivers files from what's called its root directory, which is defined in the software settings. 

For example, Nginx and Apache share the same default location of /var/www/html in Linux operating systems, and IIS uses C:\inetpub\wwwroot for the Windows operating systems. So, for example, if you requested the file  [http://www.example.com/picture.jpg](http://www.example.com/picture.jpg) it would send the file /var/www/html/picture.jpg from its local hard drive.

##### Virtual Hosts

> Web servers can host multiple websites with different domain names; to achieve this, they use virtual hosts. The web server software checks the hostname being requested from the HTTP headers and matches that against its virtual hosts (virtual hosts are just text-based configuration files).
> 	If it finds a match, the correct website will be provided. If no match is found, the default website will be provided instead. 

Virtual Hosts can have their root directory mapped to different location on the hard drive. For example, one.com being mapped to /var/www/website_one, and two.com being mapped to var/www/website_two

There's no limit to the number of different websites you can host on a web server

##### Static vs. Dynamic Content

Static content, as the name suggests, is content that never changes. Common examples of this are pictures, javascript, CSS, etc., but can also include HTML that never changes. 

Furthermore, these are files that are directly served from the webserver with no changes made to them.

**Dynamic Content**, on the other hand, is content that could change with different requests. Take, for example, a blog. On the homepage of the blog, it will show you the latest entries. 
- If a new entry is created, the home page is then updated with the latest entry, or a second example might be a search page on a blog. Depending on what word you search, different results will be displayed. 

These changes to what you end up seeing are done in what is called the **backend** with the use of programming and scripting languages. It's called the Backend because what is being done is all done behind the scenes. 

- You can't view the website's HTML source and see what's happening on the backend, while the HTML is the result of the processing from the backend. 
- Everything you see in your browser is called the **frontend.**

##### Scripting and Backend Languages

There's no much of a limit to what a backend language can achieve, and these are what make a website interactive to the user. 

Some examples of these languages (in no particular order) are PHP, Python, Ruby, Node.js, Perl and many more. 

- These languages can interact with databases, call external services, process data from the user, and so much more. 
- A very basic PHP example of this would be if you requested the website [http://example.com/index.php?name=adam](http://example.com/index.php?name=adam)

If index.php was built like this:

<html><body>Hello <?php echo $_GET["name"]; ?></body></html>

It would output the following to the client:

<html><body>Hello adam</body></html>

> You notice that you don't see any PHP code because it's on the backend. This interactivity opens up a lot more security issues for web applications that haven't been created securely.

# Linux Fundamentals

## Linux Fundamentals 1

**Where is Linux Used?**

> It's fair to say that Linux is a lot more intimidating to approach than Operating Systems like Windows. Both variants have their own advantages and disadvantages.

For example, Linux is considerably much more lightweight and you'd be surprised to know that there's a good chance you've used Linux in some for or another every day!

Linux powers things such as:

- Websites that you visit
- Car entertainment/control panels
- Point of Sale systems such as checkout tills and registers in shops
- Critical infrastructure such as traffic light controllers or industrial sensors

##### Flavors of Linux

> The name "Linux" is actually an umbrella term for multiple OS's that are based on UNIX. Thanks to UNIX being open-source, variants of Linux come in all shapes and sizes - suited best for what they system is used for. 

For example, Ubuntu and Debian are some of the more commonplace distributions of Linux because it is so extensible. I.e. you can run Ubuntu as a server (such as websites & web applications) or as a fully-fledged desktop. 

For this series, we are going to be using Ubuntu.

### Running First Few Commands

> A selling point of OSs like Ubuntu is how lightweight they can be. This of course doesn't come without it's disadvantages, where for example, often there is no GUI or what is also known as a desktop environment that we can use to interact with the machine.

A large part of interacting with these systems is using the **terminal**

The **terminal** is purely text based and is intimidating at first. However, if we break down some of the commands, after some time, you quickly become familiar with using the terminal.

We need to be able to do some basic functions like navigate to files, output their contents and make files! The commands to do are self explanatory (once you know what they are, of course)

| Command | Description                                    |
| ------- | ---------------------------------------------- |
| echo    | Output an text that we provide                 |
| whoami  | Find out what use we're currently logged in as |
### Interacting with the Filesystem

>As previously stated, being able to navigate the machine that you are logged into without relying on a desktop environment is pretty important. After all, what's the point of logging in if we can't go anywhere?

| Command | Full Name               |
| ------- | ----------------------- |
| ls      | listing                 |
| cd      | change directory        |
| cat     | concatenate             |
| pwd     | print working directory |
##### Listing Files in Our Current Directory (ls)

Before we can do anything such as finding out the contents of any files or folders, we need to know what exists in the first place. 

- This can be done using the "ls" command (short for listing)

##### Changing our Current Directory

>Now that we know what folders exist, we need to use the "cd" command (short for change directory)

Say if we wanted to open "pictures" directory, we'd do `cd Pictures`. Where again, we want to find out the contents of this "Pictures" directory and to do so, we'd use "**ls**" again.

##### Outputting the Contents of a File

Whilst knowing about the existence of files is great, it's not all that useful unless we're able to view the contents of them. 

We will come on to discuss some of the tools available to us that allows us to transfer files from one machine to another in a later room. But for now, we're going to talk about simply seeing the contents of text files using a command called `cat`. 

`cat` is short for "concatenating" and is a fantastic way for us to output the contents of files (not just text files)

**Pro Tip:** you can use `cat` to output the contents of a file within directories without having to navigate to it by using `cat` and the name of the directory, i.e. `cat /home/ubuntu/Documents.todo.txt` 

Sometimes, things like usernames and passwords (yes, really) flags or configuration settings are stored within files where "cat" can be used to retrieve these.

##### Finding out the Full Path to our Current Working Directory (pwd)

> You'll notice as you progress through navigating your Linux machine, the name of the directory that you are currently working in will be listed in your terminal.

It's easy to lose track of where we are on the filesystem exactly, which is why I want to introduce "`pwd`". This stands for **print working directory**. 

### Searching for Files

> Although it doesn't seem like it so far, one of the redeeming features of Linux is truly how efficient you can be with it. 

With that said, you can only be as efficient as you are familiar with it of course. As you interact with OSs such as Ubuntu over time, essential commands like those we've already covered will start to become muscle memory.

> One fantastic way to show just how efficient you can be with systems like this is using a set of commands to quickly search for files across the entire system that our user has access to. 
> 	No need to consistently use `cd` and `ls` to find out what is where. 
> 	Instead, we can use commands such as `find` to automate things like this for us.

##### Using Find

> The `find` command is fantastic in the sense that it can be used both very simply or rather complex depending upon what it is you want to do exactly. 

However, let's stick to the fundamentals list.

Directories can contain even more directories within themselves. It becomes a headache when we're having to look through every single one just to try and look for specific files.
- We can use `find` to do just this for us.

> Let's start simple and assume that we already know the name of the file we're looking for -- but we can't remember exactly where it is. In this case, we're looking for "passwords.txt".
> If we remember the filename, we can simply use `find -name passwords.txt` where the command will look through every folder in our current directory for that specific file.

Let's say we don't know the name of the file we're looking for.

- We can simply use what's known as a wildcard (`*`) to search for anything that has .txt at the end. In our case, we want to find every .txt file that's in our current directory.

We will construct a command such as `find -name *.txt`. Where "Find" has been able to *find* every .txt file and has then given us the location of each one. 

##### Using Grep

> Another great utility that is a great one to learn about is the use of `grep`. The `grep` command allows us to search the contents of files for specific values that we are looking for.

Take, for example, the access log of a web server. In this case, the access.log of a web server has 244 entries.

Using a command like `cat` won't cut it too well here. Let's say for example if we wanted to search this log file to see the things that a certain user/IP address visited? Looking through 244 entries isn't all that efficient considering we want to find a specific value. 

We can use `grep` to search the entire contents of this file for any entires of the value that we are searching for. 
- Going with the example of a web server's access log, we want to see everything that the IP address "81.143.211.90" has visited (note that this is fictional)

### An Introduction to Shell Operators

>Linux operators are a fantastic way to power up your knowledge of working with Linux. There are a few important operators that are worth noting. We'll cover the basics and break them down accordingly to bite-sized chunks.

At an overview, I'm going to be showcasing the following operators:

| Symbol/Operator | Description                                                                                                                            |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| &               | This operator allows you to run commands in the background of your terminal.                                                           |
| &&              | This operator allows you to combine multiple commands together in one line of your terminal.                                           |
| >               | This operator is a redirector - meaning that we can take the output from a command and direct it elsewhere.                            |
| >>              | This operator does the same function of the `>` operator but appends the output rather than replacing (meaning nothing is overwritten) |
##### Operator "&"

> This operator allows us to execute commands in the background. For example, let's say we want to copy a large file. This will obviously take quite a long time and will leave us unable to do anything else until the file successfully copies.

The "&" shell operator allows us to execute a command and have it run in the background (such as this file copy) allowing us to do other things.

##### Operator "&&"

> This shell operator is a bit misleading in the sense of how familiar it is to partner "&". Unlike the "&" operator, we can use "&&" to make a list of commands to run, for example `command1 && command2`. 
> 	However, it's worth noting that `command2` will only run if `command1` was successful.

##### Operator ">"

> This operator is what's known as an output redirector. What this essentially means is that we take the output from a command we run and send that output to somewhere else. 

A great example of this is redirecting the output of `echo` command that we learned in Task 4. Of course, running something such as `echo howdy` will return "howdy" back to our terminal -- that isn't super useful. What we can do instead, is redirect "howdy" to something such as a new file. 

Let's say we want to create a file named "welcome" with the message "hey". We can run `echo hey > welcome` where we want the file created with the contents "hey".

##### Operator ">>"

> This operator is also an output redirector like in the previous operator (`>`) we discussed. However, what makes this operator different is that rather than overwriting any contents within a file, for example, it instead just puts the output at the end. 

Following our previous example where we have the file "welcome" that has the contents of "hey". If we were to use echo to add "hello" to the file using the `>` operator, the file will now only have "hello" and not "hey".

The `>>` operator allows us to append the output to the bottom of the file, rather than replacing the contents.

# Linux Fundamentals 2

### Accessing Your Linux Machine using SSH

This protocol is called **S**ecure **S**hell or **SSH** for short and is the common means of connecting to and interacting with the command line of a remote Linux machine.

##### What is Secure Shell and How Does it Work?

> Secure Shell or SSH simply is a protocol between devices in an encrypted form. Using cryptography, any input we send in a human-readable format is encrypted for travelling over a network -- where it is then unencrypted once it reaches the remote machine.

- SSH allows us to remotely execute commands on another device remotely
- Any data sent between the devices is encrypted when it is sent over a network such as the internet

##### Introduction to Flags and Switches

> A majority of commands allow for arguments to be provided. These arguments are identified by a hyphen and a certain keyword known as **flags or switches**

When using a command, unless otherwise specified, it will perform its default behavior. 
- For example, `ls` lists the contents of the working directory. However, hidden files are not shown. We can use flags and switches to extend the behaviour of commands.

Using our `ls` example, `ls` informs us that there is only one folder named "folder1" as highlighted in the screenshot.

The `--help` option used with `ls` will show a list of possible commands and explain their functions.
- This output is, in fact, a formatted output of what is called the man page (manual), which contains documentation for Linux commands and applications.

**The Man(ual) Page**

> The manual pages are a great source of information for both system commands and applications available on both a Linux machine, which is accessible on the machine itself and online.

To access this documentation, we can use the `man` command and then provide the command we want to read the documentation for. Using our ls example, we would use `man ls` to view the manual pages for `ls` like so:
##### Filesystem Interaction Continued

> We covered some of the most fundamental commands when interacting with the filesystem on the Linux machine. For example, we covered how to list and find the contents of folders using `ls` and `find` and navigating the filesystem using `cd`

In this task, we're going to learn some more commands for interacting with the filesystem to allow us to:

- create files and folders
- move files and folders
- delete files and folders

More specifically, the following commands:

| Command | Full Name      | Purpose                      |
| ------- | -------------- | ---------------------------- |
| touch   | touch          | Create file                  |
| mkdir   | make directory | Create a folder              |
| cp      | copy           | Copy a file or folder        |
| mv      | move           | Move a file or folder        |
| rm      | remove         | Remove a file or folder      |
| file    | file           | Determine the type of a file |
**Creating Files and Folders (touch, mkdir)**

> Creating files and folders on Linux is a simple process. First, we'll cover creating a file. The touch command takes exactly one argument -- the name we want to give the file we create. 

For example, we can create the file "note" by using `touch note`. 
- It's worth noting that touch simply creates a blank file. You would need to use commands like echo or text editors such as nano to add content to the blank file.

This is a similar process for creating a folder, which just involves the `mkdir` command and again providing the name that we want to assign to the directory. For example, creating the directory "mydirectory" using `mkdir mydirectory`

**Removing Files and Folders (rm)**

`rm` is extraordinary out of the commands that we've covered so far. You can simply remove files using `rm`.
- However, you need to provide the `-r` switch alongside the name of the directory you wish to remove.

**Copying and Moving Files and Folders (cp, mv)**

> copying and moving files is an important functionality on a Linux machine. Starting with `cp`, this command takes two arguments:

1. the name of the existing file
2. the name we wish to assign to the new file when copying

`cp` copies the entire contents of the existing file into the new file. In the screenshot below, we are copying "note" to "note2".

> Moving a file takes two arguments, just like the cp command. However, rather than copying and or creating a new file, `mv` will merge or modify the second file that we provide as an argument. 

Not only can you use `mv` to move a file to a new folder, but you can also use `mv` to rename a file or folder

**Determining the File Type**

> What is often misleading and often catches people out is making presumptions from files as to what their purpose or contents may be. Files usually have what's known as an extension to make this easier. For example, text files usually have an extension of ".txt"
> 	But this is not necessary.

So far, the files in our examples haven't had an extension. Without knowing the context of why the file is there -- we don't really know its purpose.

- Enter the `file` command. This command takes one argument. For example, we'll use `file` to confirm whether or not the "note" file in our examples is indeed a text file, like so `file note`.

### Permissions 101

> As you would have already found out by now, certain users cannot access certain files or folders. We've previously explored some commands that can be used to determine what access we have and where it leads us.

The ten columns in front of a file or directory are the file *permissions.*

A file or folder can have a couple of characteristics that determine both what actions are allowed and what user group has the ability to perform the given action -- such as the following.

- Read
- Write
- Execute

**The Differences Between Users & Groups**

> We briefly explored this in Linux Fundies Part 1. The great thing about Linux is that permissions can be so granular, that whilst a user technically owns a file, if the permissions have been set, the a group of users can also have either the same or a different set of permissions to the exact same file without affecting the file owner itself.

Let's put this into a real-world context; the system user that runs a web server must have permissions to read and write files for an effective web application. 

- However, companies such as web hosting companies will have to want to allow their customers to upload their own files for their website without being the webserver system user -- compromising the security of every other customer.

##### Switching Between Users

> Switching between users on a LInux install is easy work thanks to the `su` command. Unless you are the root user (or using root permissions through sudo), then you are required to know two things to facilitate this transition of user accounts:

- The user we wish to switch to
- The user's password

The `su` command takes a couple of switches that may be of relevance to you. 

- For example, executing a command once you log in or specifying a specific shell to use. I encourage you to read the man page for `su` to find out more. 
- However, I will cover the `-1` or `--login` switch.

Simply by providing the `-l` switch to `su`, we start a shell that is much more similar to the actual user logging into the system - we inherit a lot more properties of the new user, i.e. environment variables and the likes.

### Common Directories

##### /etc

>This root directory is one of the most important root directories on your system.
>	The etc folder (short for etcetera) is a commonplace location to store system files that are used by your operating system.

- For example, the sudoers file highlighted in the screenshot below contains a list of the users & groups that have permissions to run sudo or a set of commands as the root user.

The `passwd` and `shadow` files are special for Linux as they show you how your system stores the passwords for each user in encrypted formatting called *sha512*

##### /var

> The */var* directory, with "var" meaning **variable data**, is one of the main root folders found on a Linux install. 
> 	This folder stores data that is frequently accessed or written by services or applications running on the system.

For example, log files from running services and applications are written here (/var/log), or other data that is not necessarily associated with a specific user (i.e. databases and the like)

##### /root

> Unlike /home directory, the **/root** folder is actually the home for the "root" system user. There isn't anything more to this folder other than just understanding that this is home directory for the "root" user. 

But, it is worth a mention as the logical presumption is that this user would have their data in a directory such as **/home/root** by default.

##### /tmp

> This is a unique root directory found on a Linux install. Short for **temporary**, the /tmp directory is volatile and is used to store data that is only needed to be accessed once or twice.

Similar to the memory on your computer, once the computer is restarted, the contents of this folder are cleared out. 

What's useful for pentesting is that any user can write to this folder by default. Meaning once we have access to a machine, it serves as a good place to store things like our *enumeration scripts*. 

# Linux Fundamentals 3

> Showcase some useful utilities and applications that you are likely to use day-to-day.  We're also going to advance our Linux-fu skills by learning about automation, package management and service/application logging. 
### Terminal Text Editors

> Throughout the series so far, we have only stored text in files using a combination of the `echo` command and the pipe operators (`>` and `>>`). This isn't an efficient way to handle data when you're working with files with multiple lines.

**Introducing Terminal Text Editors**

- There are a few options that you can use, all with a variety of friendliness and utility. This task is going to introduce you to `nano` but also show you an alternative named `VIM`

**Nano**

> It is easy to get started with Nano. To create or edit a file using nano, we simply use `nano filename` -- replacing the name of the file you wish to edit.

Once we press enter and execute the command, `nano` will launch! Where we can just begin to start entering or modifying our text. You can navigate each line using the "up" and "down" arrow keys or start a new line using the "Enter" key on your keyboard.

Nano has a few features that are easy to remember & covers the most general things you would want out of a text editor, including:

- Searching for text
- Copying and Pasting
- Jumping to a line number
- Finding out what line number you are on

**VIM**

> VIM is a much more advanced text editor. Whilst you're not expected to know all advanced features, it's helpful to mention it for powering up your Linux skills.

Some of VIM's benefits, albeit taking a much longer time to become familiar with, includes:

- Customizable - you can modify the keyboard shortcuts to be of your choosing
- Syntax Highlighting - this is useful if you are writing or maintaining code, making it a popular choice for software developers
- VIM works on all terminals where Nano may not be installed
- There are a lot of resources such as https://vim.rtorr.com/, tutorials, and others available

### General/Useful Utilities

##### Downloading Files (Wget)

> A pretty fundamental feature of computing is the ability to transfer files. For example, you may want to download a program, a script, or even a picture.
> 	Thankfully for us, there are multiple ways in which we can retrieve these files.

We're going to cover the use of `wget`. This command allows us to download files from the web via HTTP -- as if you were accessing the file in your browser.

We simply need to provide the address of the resource that we wish to download. 

##### Transferring Files from Your Host - SCP (SSH)

Secure copy, or SCP, is just that -- a means of securely copying files. Unlike the regular cp command, this command allows you to transfer files between two computers using the SSH protocol to provide both authentication and encryption. 

Working with a model of SOURCE and DESTINATION, SCP allows you to:

- Copy files & directories from your current system to a remote system
- Copy files & directories from a remote system to your current system

Provided that we know usernames and passwords for a user on your current system and a user on the remote system. For example, let's copy an example file from our machine to a remote machine, which I have neatly laid out in the table below:

| Variable                                                    | Value           |
| ----------------------------------------------------------- | --------------- |
| The IP address of the remote system                         | 192.168.1.30    |
| User on the remote system                                   | ubuntu          |
| Name of the file on the local system                        | important.txt   |
| Name that we wish to store the file as on the remote system | transferred.txt |
> With this information, let's craft our `scp` command (remembering that the format of SCP is just SOURCE and DESTINATION)

`scp important.txt ubuntu@192.1689.1.30:/home/ubuntu/transferred.txt`

##### Serving Files From Your Web Host - WEB

Ubuntu machines come pre-packaged with python3. Python helpfully provides a lightweight and easy to use module called "HTTPServer". This module turns your computer into a quick and easy web server that you can use to serve your own files, where they can then be downloaded by another computing using commands such as `curl` and `wget`.

> Python3's "HTTPServer" will serve the files in the directory where you run the comman, but this can be changed by providing options that can be found within the manual pages. Simply, all we need to do is run `python3 -m http.server` in the terminal to start the module.
> 	Below, we are serving from a directory called "webserver", which has a single named "file"

```
tryhackme@linux3:/webserver# python3 -m http.server 
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

> Now, let's use `wget` to download the file using the 10.10.52.132 address and the name of the file. 
> 	Remember, because Python3 server is running port 8000, you will need to specify this within your `wget` command. 
> 	
```
tryhackme@mymachine:~# wget http://10.10.52.132:8000/myfile
```

> Note, you will need to open a new terminal to use `wget` and leave the one you have started the Python3 web server in. This is because, once you start the Python3 web server, it will run in that terminal until you cancel it.

```
tryhackme@linux3:/tmp# wget http://MACHINE_IP:8000/file  2021-05-04 14:26:16  http://127.0.0.1:8000/file Connecting to http://127.0.0.1:8000... connected. 
HTTP request sent, awaiting response... 200 OK Length: 51095 (50K) [text] Saving to: ‘file’  file                    
100%[=================================================>]  49.90K  --.-KB/s    
in 0.04s  
2021-05-04 14:26:16 (1.31 MB/s) - ‘file’ saved [51095/51095]`
```

> Remember, you will need to run the wget command in another terminal (while keeping the terminal that is running the Python3 server active). An example of this on the TryHackMe AttackBox is below.

### Processes 101

> Processes are the programs that are running on your machine. They are managed by the kernel, where each process will have an ID associated with it, also known as its PID. The PID increments for the order in which the process starts I.e. the 60th process will have a PID of 60. 

##### Viewing Process

We can use the friendly `ps` command to provide a list of the running processes as our user's session and some additional information such as its status code, the session that is running it, how much usage time of the CPU it is using, and the name of the actual program or command that is being executed.

Note how in the screenshot above, the second process ps has a PID of 204, and then in the command below it, this is the incremented to 205. 

To see the processes run by other users and those that don't run from a session (i.e. system processes), we need to provide `aux` to the `ps` command like so: `ps aux`

> Another very useful command it the `top` command; top gives you real-time statistics about the processes running on your system instead of a one-time view. These statistics will refresh every 10 seconds, but will also refresh when you use the arrow keys to browse the various rows. 

Another great command to gain insight into your system s via the `top` command. 

##### Managing Processes

You can send signals that terminate processes; there are a variety of types of signals that correlate to exactly how "cleanly" the process is dealt with by the kernel. To kill a command, we can use the appropriately named `kill` command and the associated PID that we wish to kill. i.e. PID 1337, we'd use `kill 1337`.

Below are some of the signals that we can send to a process when it is killed.

- SIGTERM - kill the process, but allow it to do some cleanup tasks beforehand
- SIGKILL - kill the process - doesn't do any cleanup after the fact
- SIGSTOP - stop/suspend a process

##### How do Processes Start?

> Let's start off by talking about namespaces. The Operating System (OS) uses namespaces to ultimately split up the resources available on the computer to (such as CPU, RAM and priority) processes. 
> 	Think of it as splitting your computer up into slices -- similar to a cake.

Processes within that slice will always have access to a certain amount of computing power, however, it will be a small portion of what is actually available to every process overall.

Namespaces are great for security as it is a way of isolating processes from one another -- only those that are in the same namespace will be able to see each other. 

A process with an ID of 0 is a process that is started when the system boots. This process is the system's init on Ubuntu, such as **systemd**, which is used to provide a way of managing a user's processes and sits in between the operating system and the user.
- For example, once a system boots and it initializes, **systemd** is one of the first processes that are started. Any program or piece of software that we want to start will start as what's known as a child process of **systemd**. 
- This means that it is controlled by **systemd**, but will run as its own process (although sharing the resources from **systemd**) to make it easier for us to identify and the likes.

##### Getting Processes/Services to Start on Boot

> Some applications can be started on the boot of the system that we own. For example, web servers, database servers or file transfer servers. This software is often critical and is often told to start during the boot-up of the system by administrators.

- In this example, we're going to be telling the apache web server to be starting apache manually and then telling the system to launch apache2 on boot. 

Enter the use of `systemct1` -- this command allows us to interact with the **systemd** process/daemon.

Continuing on our example, **systemctl** is an easy to use command that takes the following formatting: `systemctl [option] [service]` 

For example, to tell apache to start up, we'll use `systemctl start apache2`. Seems simple enough, right? Same with if we wanted to stop apache, we'd just replace the `[option]` with stop (instead of start like we provided).

We can do four options with `systemctl`:

- Start
- Stop
- Enable
- Disable

##### An Introduction to Backgrounding and Foregrounding in Linux

Processes can run in two states: In the background and in the foreground. For example, commands that you run in your terminal such as "echo" or things of that sort will run in the foreground of your terminal as it is the only command provided that hasn't been told to run in the background.

- "Echo" is a great example as the output of echo will return to you in the foreground, but wouldn't in the background.

This is great for commands such as copying files because it means that we can run the command in the background and continue on with whatever further commands we wish to execute (without having to wait for the file copy to finish first)

We can do the exact same when executing things like scripts -- rather than relying on the & operator, we can use `Crtl + Z` on our keyboard to background a process. 
- It is also an effective way of "pausing" the execution of a script or command like in the example below. ecution of a script or command line.

**Foregrounding a Process**

> Now that we have a process running in the background, for example, our script "background.sh" which can be confirmed by using the `ps aux` command, we can back-pedal and bring this process back to the foreground to interact with.

With our process background using either `Ctrl + Z` or the `&` operator, we can use `fg` to bring this back to focus like below, where we can see the `fg` command is being used to bring the background process back into use on the terminal, where output of the script is now returned to us.

### Maintaining Your System: Automation

> Users may want to schedule a certain action or task to take place after the system has booted. Take, for example, running commands, backing up files, or launching your favorite programs on, such as Spotify or Google Chrome.

We're going to be talking about the `cron` process, but more specifically, how we can interact with it via the use of `crontabs`. Crontab is one of the processes that is started during boot, which is responsible for facilitating and managing cron jobs. 

A **crontab** is simply a special file with formatting that is recognized by the `cron` process to execute each line step-by-step. Crontabs require six specific values.

| Value | Description                              |
| ----- | ---------------------------------------- |
| MIN   | What minute to execute at                |
| HOUR  | What hour to execute at                  |
| DOM   | What day of the month to execute at      |
| MON   | What month of the year to execute        |
| DOW   | What day of the week to execute at       |
| CMD   | The actual command that will be executed |
Let's use the example of backing up files. You may wish to backup "cnmatics" "documents" every 12 hours. We would use the following formatting.

`0*/12***cp -R /home/cnmatic/Documents/var/backups`

> An interesting feature of crontabs is that these also support the wildcard or asterisk (`*`). If we do not wish to provide a value for that specific field, i.e. we don't care what month, day or year it is executed -- only that it is executed every 12 hours, we simply just place an asterisk.

This can be confusing to begin with, which is why there are some great resources such as the online https://crontab-generator.org/ that allows you to use a friendly application to generate your formatting for you.

Crontabs can be edited by using `crontab -e`, where you can select an editor (such as Nano) to edit your crontab.
### Maintaining Your System: Package Management

##### Introducing Packages and Software Repos

> When developers wish to submit software to the community, they will submit it to an "apt" repository.
> 	If approved, their programs and tools will be released into the wild.
> 	Two of the most redeeming features of Linux shine to light here: User accessibility and the merit of open source tools.

While operating system vendors will maintain their own repositories, you can also add community repositories to your list! This allows you to extend the capabilities of your OS. 

Additional repositories can be added by using the `add-apt-repository` command or by listing another provider. 
- For example, some vendors will have a repository that is closer to their geographical location.

##### Managing Your Repositories

> Normally we use the apt command to install software onto our Ubuntu system. The `apt` command is a part of the package management software also named **apt**. Apt contains a whole suite of tools that allow us to manage the packages and sources of our software, and to install or remove software at the same time.

One method of adding repositories is to use the `add-apt-repository` command we illustrated above, but we're going to walk through adding and removing a repository manually. Whilst you can install software through the use of package installers such as `dpkg`, the benefits of apt means that whatever we update our system -- the repository that contains the pieces of software that we add also gets checked for updates.

> When adding software, the integrity of what we download is guaranteed by the use of what is called GPG (Gnu Privacy Guard) keys. These keys are essentially a safety check from the developers saying "here's our software".
> 	If the keys do not match up to what your system trusts and what the developers used, then the software will not be downloaded.

1. Let's download the GPG key and use apt-key to trust it: `wget -q0 https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -`
2. Now that we have added this key to our trusted list, we can now add Sublime Text 3's repository to our apt sources list. A good practice is to have a separate file for every different community/3rd party repository that we add. 
2.1. Let's create a file named **sublime-text.list** in **/etc/apt/sources.list.d** and enter the repository information like so:
2.2. And now use Nano or a text editor of your choice to add & save Sublime Text 3 repository into this newly created file:
2.3. After we have added this entry, we need to update apt to recognize this new entry -- this is done using the `apt update` command
2.4. Once successfully updated, we can now proceed to install the software that we have trusted and added to apt using `apt install sublime-text`

> Removing packages is as easy as reversing. This process is done by using the `add-apt-repository --remove ppa:PPA_Name/ppa` command or by manually deleting the file that we previously added to. Once removed, we can just use `apt remove [software-name-here]` i.e. `apt remove sublime-text`

### Maintaining Your System: Logs

> We briefly touched upon log files and where they can be found in Linux Fundamentals Part 1. However, let's quickly recap. 

Located in the /var/log directory, these files and folders contain logging information for applications and services running on your system.
The Operating System (OS) has become pretty good at automatically managing these logs in a process that is known as "rotating". 

> Services and logs are a great way in monitoring the health of your system and protecting it. Not only that, but the logs for services such as a web server contain information about every single request - allowing developers or administrators to diagnose performance issues or investigate an intruder's activity. 
> 	For example, the two types of log files below are of interest:

- access log
- error log

# Windows Fundamentals 1

> The Windows operating system is a complex product with many system files, utilities, settings, features, etc.

This module will attempt to provide a general overview of just a handful of what makes up the Windows OS, navigate the user interface, make changes to the system, etc. The content is aimed at those who wish to understand and use the Windows OS on a more comfortable level.

### Windows Editions

> The Windows operating system has a long history dating back to 1985, and currently, it is the dominant operating system in both home use and corporate networks. Because of this, Windows has always been targeted by hackers & malware writers.

Windows XP was a popular version of Windows and had a long-running. 

Microsoft announced Windows Vista, which was a complete overhaul of the Windows operating system. There were many issues with Vista, and it was not received well by Windows users, and it was quickly phased out.

When Microsoft announced the end-of-life date for Windows XP, many customers panicked. Corporations, hospitals etc. scrambled and tested the next viable Windows version, which was Windows 7, against many other hardware and devices
- Vendors had to work against the clock to ensure their products worked with Windows 7 for their customers. 
- If they couldn't, their customers had to break their agreement and find another vendor that upgraded their products to work with Windows 7. It was a nightmare for many, and Microsoft took note of it.

Windows 7, as quickly as it was released, was marked with an end of support date. Windows 8 came out and was short lived, just like Vista.

Then came Windows 10, which is the current Windows operating system version for desktop computers. 
- Windows 10 comes in two flavors: Home and Pro. You can read the differences between them on the Windows webpage.
- Even though we didn't talk about servers, the current version of Windows operating system for servers is **Windows Server 2019**
- Many critics like to bash on Microsoft, but they have long made strides to improve the usability and security with each new version of Windows.

### The File System

> The file system used in modern versions of Windows is the **New Technology File System**, or NTFS

Before NTFS, there was **FAT16/FAT32** (File Allocation Table) and **BPFS** (High Performance File System).

You will see FAT partitions in use today. For example, you typically see FAT partitions in USB devices, MicroSD cards, but traditionally not on personal Windows computers/laptops or Windows servers

NTFS is known as a *journaling file system*. In case of a failure, the file system can automatically repair the folders/files on disk using information stored in a log file. This function is not possible with FAT.

NFTS addresses many of the limitations of the previous file systems; such as:

- Supports larger than 4GB
- Set specific permissions on folders and files
- Folder and file compression
- Encryption (Encryption File System or **EFS**)

On NFTS volumes, you can set permissions that grant or deny access to files and folders.

The permissions are:

- **Full Control**
- **Modify**
- **Read & Execute**
- **List Folder Contents**
- **Read**
- **Write**

| Permission           | Meaning for Folders                                                                                               | Meaning for Files                                                                     |
| -------------------- | ----------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| Read                 | Permits viewing and listing of files and subfolders                                                               | Permits viewing or accessing the file's contents                                      |
| Write                | Permits adding of files and subfolders                                                                            | Permits writing to a file                                                             |
| Read & Execute       | Permits viewing and listing of files and subfolders as well as executing of files: inherited by files and folders | Permits viewing and accessing of the file's contents as well as executing of the file |
| List Folder Contents | Permits viewing and listing of files and subfolders as well as executing of files: inherited by folders only      | N/A                                                                                   |
| Modify               | Permits reading and writing of files and subfolders; allows deletion of the folder                                | Permits reading and writing of the file: allows deletion of the file                  |
| Full Control         | Permits reading, writing, changing, and deleting of files and subfolders                                          | Permits reading, writing, changing and deleting of the file                           |
How can you view the permissions of a folder or file?

- Right-click the file or folder you want to check for permissions.
- From the context menu, select `Properties`
- Within Properties, click on the `Security` tab
- In the `Group or user name` list, select the user, computer or group whose permissions you want to view.

Another feature of NTFS: **Alternate Data Streams**. Alternate Data Streams are file attributes specific to Windows NTFS.

Every file has at least one data stream (`$DATA`), and ADS allows files to contain more than one stream of data. Natively Window Explorer doesn't display ADS to the user. There are 3rd party executables that can be used to view this data, but `Powershell` gives you the ability to view ADS for files. 

From a security perspective, many malware writers have used ADS to hide data.

### The Windows\System32 Folders

> The Windows folder `C:\Windows` is traditionally known as the folder which contains the Windows operating system.

The folder doesn't have to reside in the C drive necessarily. It can reside in any other device and technically can reside in a different folder.

This is where environment variables, more specifically system environment variables, come into play.
- Even though not discussed yet, the system environment variable for the Windows directory is `%windir%`

Per Microsoft: *Environment variables store information about the operating system environment. This information includes details such as the operating system path, the number of processors used by the operating system, and the location of temporary folders.*

> The *System32* folder holds the most important files that are critical for the Operating System.

You should proceed with extreme caution when interacting with this folder. Accidentally deleting any files or folders within System32 can render the Windows OS inoperational. 

### User Accounts, Profiles and Permissions

> User accounts can be one of two types on a typical Windows system: **Administrator & Standard User**.

The user account type will determine what actions the user can perform on that specific Windows system, etc.

- An administrator can make changes to the system: add users, delete users, modify groups, modify settings on the system, etc.
- A Standard User can only make changes to folders/files attributed to the user & can't perform system-level changes, such as install programs.

When a user account is created, a profile is created for that user. The location for each user profile folder will fall under is C:\Users.

- For example, the user profile folder for the user account Max will be `C:\Users\Max`

Each user profile will have the same folders; a few of them are:

- Desktop
- Documents
- Downloads
- Music
- Pictures

Another way to access this information, and then some, is using **Local User and Group Management**

Using the Run dialog box will allow you to enter `lusrmgr.msc` which opens the Local User and Group Manager.

Each group has permissions set to it, and users are assigned/added to groups by the Administrator. When a user is assigned to a group, the user inherits the permissions of that group. 
- A user can be assigned to multiple groups.

### User Account Control

> The large majority of home users are logged into their Windows systems as local administrators. Remember from the previous task any user with administrator as the account type can make changes to the system.

A user doesn't need to run with high (elevated) privileges on the system to run tasks that don't require such privileges, such as surfing the Internet, working on a Word document, etc. This elevated privilege increases the risk of system compromise because it makes it easier for malware to infect the system.
- Consequently, since the user account can make changes to the system, the malware would run in the context of the logged-in user.

To protect the local user with such privileges, Microsoft introduced **User Account Control**(UAC)
- This concept was first introduced with the short-lived Windows Vista and continued with versions of Windows that followed.

How does UAC work? When a user with an account type of administrator logs into a system, the current session doesn't run with elevated permissions. When an operation requiring higher-level privileges needs to execute, the user will be promoted to confirm if they permit the operation to run.

### Settings and the Control Panel

> On a Windows system, the primary locations to make changes are the Settings menu and the Control Panel.

For a long time, the Control Panel has been the go-to location to make system changes, such as adding a printer, uninstall a program, etc.

The settings menu was introduced in Windows 8, the first Windows operating system catered to touch screen tablets, and is still available in Windows 10. As a matter of fact, the Settings menu is now the primary location a user goes to if they are looking to change a system. 

**Control Panel** is the menu where you will access more complex settings and perform more complex actions. In some cases, you can start in Settings and end up in the Control Panel. 

### Task Manager

> The **task manager** provides information about the applications and processes currently running on the system. Other information is also available, such as how much **CPU** and **RAM** are being utilized which falls under **performance**.

# Windows Fundamentals 2

### System Configuration

> The **System Configuration** utility (MSConfig) is for advanced troubleshooting, and its main purpose is to help diagnose startup issues.

References the following document here for more information on the System Configuration utility.

There are several methods to launch System Configuration. One method is from the Start Menu.

The System Configuration utility has five tabs across the top. Below are the names for each tab. We will briefly cover each tab in this task. 

1. General
2. Boot
3. Services
4. Startup
5. Tools

In the **general** tab, we can select what drives and services for Windows to load upon boot. 
- **Normal**
- **Diagnostic**
- **Selective**

In the **boot** tab, we can define various boot options for the Operating System.

The **Services** tab lists all services configured for the system regardless of their state (running or stopped). A service is a special type of application running in the background.

In the **Startup** tab, you won't see anything interesting in the attached VM. Below is a screenshot of the Startup tab for **MSConfig** from my local machine.

In the **Tools** tab, we can run to configure the operating system further. There is a brief description of each tool to provide some insight into what the tool is for. 

- Notice the **Selected command** section. The information in this textbox will change per tool.
- To run a tool, we can use the command to launch the tool via the run prompt, command prompt, or by clicking the `Launch` button.

### Change UAC Settings

> We're continuing with Tools that are available through the **System Configuration** panel.

**User Account Control** (UAC) was covered in great detail in Windows Fundamentals 1.

The UAC settings can be changed or even turned off entirely (not recommended). 

You can move the slider to see how the setting will change the UAC settings and Microsoft's stance on the setting.

### Computer Management

> The **Computer Management** (`compmgmt`) utility has three primary sections: **System Tools, Storage** and **Services and Applications**. 

**System Tools**

> Let's start with **Task Scheduler**. Per Microsoft, with Task Scheduler, we can create and manage common tasks that our computer will carry out automatically at the times we specify. 

A task can run an application, a script, etc. and tasks can be configured to run at any point. A task can run at log in or at log off. Tasks can also be configured to run on a specific schedule, for example, every five minutes.

To create a basic task, click on `Create Basic Task` under **Actions** (right pane). 

**Event Viewer**

Event Viewer allows us to view events that have occurred on the computer. These records of events can be seen as an audit trail that can be used to understand the activity of the computer system. 
- This information is often used to diagnose problems and investigate actions executed on the system.

> There are five types of events that can be logged. Below is a table from docs.microsoft.com providing a brief description for each.


| Event Type    | Description                                                                                                                                                                                                                                                                                      |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Error         | An event that indicates a significant problem such as loss of data or loss of functionality. For example, if a service fails to load during startup, an Error event is logged.                                                                                                                   |
| Warning       | An event that is not necessarily significant but may include a possible future problem. For example, when disk space is low, Warning event is logged. If an application can recover from an event without loss of functionality or data, it can generally classify the event as a Warning event. |
| Information   | An event that describes the successful operation of an application, driver or service. For example, when a network driver loads successfully, it may be appropriate to log an information event.                                                                                                 |
| Success Audit | An event that records an audited security access attempt that is successful. For example, a user's successful attempt to log on to the system is logged as a Success Audit event.                                                                                                                |
| Failure Audit | An event that records an audited security access attempt that fails. For example, if a user tries to access a network drive and fails, the attempt is logged as a Failure Audit event.                                                                                                           |
>The standard logs are visible under **Windows Logs**. Below is a table from docs.microsoft.com providing a brief description for each:

| Log         | Description                                                                                                                                                                                                                                 |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Application | Contains events logged by applications. For example, a database application might record a file error. The application developer decides which events to record.                                                                            |
| Security    | Contains events such as valid and invalid logon attempts, as well as events related to resource use such as creating, opening or deleting files or other objects. An administrator can start auditing to record events in the security log. |
| System      | Contains events logged by system components, such as the failure of a driver or other system component to load during start up.                                                                                                             |
| *CustomLog* | Contains events logged by applications that create a custom log. Using a custom log enables an application to control the size of the log or attach ACLs for security purposes without affecting other applications.                        |
**Shared Folders** is where you will see a complete list of shares and folders shared that others can connect to.

In **Performance**, you'll see a utility called **Performance Monitor** (`perfmon`).

Perfmon is used to view performance data either in real time or from a log file. This utility is useful for troubleshooting performance issues on a computer system, whether local or remote.

**Storage**

> Under storage is **Windows Server Backup** and **Disk Management**. We'll only look at Disk Management in this room.

Note: since the virtual machine is a Windows Server operating system, there are utilities available that you will typically not see in Windows 10.

**Disk Management** is a system utility in Windows that enables you to perform advanced storage tasks. Some tasks are:

- Set up a new drive
- Extend a partition
- Shrink a partition
- Assign or change a drive letter (ex. E:)

**Services and Applications**

> A *service* is a special type of application that runs in the background. Here you can do more than enable and disable a service, such as view the Properties for the service.

WMI Control configures and controls the **Windows Management Instrumentation** (WMI) service.

Per Wikipedia, "_WMI allows scripting languages (such as VBScript or Windows PowerShell) to manage Microsoft Windows personal computers and servers, both locally and remotely. Microsoft also provides a command-line interface to WMI called Windows Management Instrumentation Command-line (WMIC)._"
### System Information

> We're continuing with Tools that are available through the **System Configuration** panel

What is the **System Information(`msinfo32`)** tool?

*This tool gathers information about your computer and displays a comprehensive view of your hardware, system components, and software environment, which you can use to diagnose computer issues*

The information in **System Summary** is divided into three sections:

- **Hardware Resources**
- **Components**
- **Software Environment**

System Summary will display general technical specifications for the computer, such as processor brand and model.

Under **Components**, you can see specific information about the hardware devices installed on the computer. Some sections don't show any information, but some sections do. Such as **Display** and **Input**.

> In the **Software Environment** section, you can see information about software baked into the operating system and software you have installed. Other details are visible in this section as well, such as the **Environment Variables** and **Network Connections**.

### Resource Monitor

What is **Resource Monitor** (`resmon`)?

Per Microsoft, "_Resource Monitor displays per-process and aggregate CPU, memory, disk, and network usage information, in addition to providing details about which processes are using individual file handles and modules. Advanced filtering allows users to isolate the data related to one or more processes (either applications or services), start, stop, pause, and resume services, and close unresponsive applications from the user interface. It also includes a process analysis feature that can help identify deadlocked processes and file locking conflicts so that the user can attempt to resolve the conflict instead of closing an application and potentially losing data._"

> This tool is geared towards advanced users who need to perform advanced troubleshooting on their computer system.

In the Overview tab, Resmon has four sections:

- **CPU**
- **Disk**
- **Network**
- **Memory**
### Command Prompt

> The command prompt (`cmd`) can seem daunting at first, but it's really not that bad once you understand how to interact with it. 

In early operating systems, the command line was the sole way to interact with the OS.

Even though GUI is the primary way to interact with the operating system, a computer can still interact via the command prompt.

In this task, we'll only cover a few commands that a computer user can run in the command prompt to obtain information about the computer system.

Let's start with a few simple commands, such as `hostname` and `whoami`

- `hostname` displays the name of the computer
- `whoami` will output the name of the logged-in user

`ipconfig` will show the network address settings for the computer.

> Each command will have a help manual to explain the expected syntax to execute the command properly, along with any additional parameters that can be added to the command to expand its execution.

- A command to retrieve the help manual for a command is `/?`

**Note:** to clear the command prompt screen, the command is `cls`

The next command is `netstat`. Per the help manual, this command will display protocol statistics and current TCP/IP network connections.

`netstat` can be run alone or with parameters, such as `-a`, `-b`, `-e`, etc.

When any of the parameters are appended to the root command, `netstat` in this case, the output changes. Play with a few to see for yourself.

The `net` command is primarily used to manage network resources. This command supports sub commands. 
- If you type **`net`** without a subcommand, the output will show the syntax for the root command showing a few of the sub-commands you can use. 
- For help with `net`, you will need to use the correct syntax, which is `net help`.

### Registry Editor

> The **Windows Registry** is a central hierarchical database used to store information necessary to configure the system for one or more users, applications and hardware devices.

The registry contains information that Windows continually references during operation, such as:

- Profiles for each user
- Applications installed on the computer and the types of documents that each can create
- Property sheet settings for folders and application icons
- What hardware exists on a system
- The ports that are being used

There are various ways to view/edit the registry. One way is to use **Registry Editor** (`regedit`)

# Windows Fundamentals 3

> Learn about the Microsoft tools that help keep the device secure, such as Windows updates, Windows Security, BitLocker and more.

### Windows Updates

> Windows update is a service provided by Microsoft to provide security updates, feature enhancements and patches for the Windows operating system and other Microsoft products, such as Microsoft Defender.

Updates are typically released on the second Tuesday of each month, in a day referred to as **Patch Tuesday**. That doesn't necessarily mean that a critical update/patch has to wait for the next Patch Tuesday to be released. 
- If the update is urgent, then Microsoft will push the update via the Windows Update to the Windows devices. 

**Tip**: Another way to access Windows Update is from the Run dialog box, or CMD, by running the command `control /name Microsoft.WindowsUpdate`.

> Throughout the years, Windows users have grown accustomed to pushing Windows Updates off to a later data or not installing the updates at all. Various reasons caused this action, one being the fact that a reboot is typically required after a Windows update.

- Microsoft addressed this issue with Windows 10. The updates can no longer be ignored, at some point they will be installed and the computer will restart.

### Windows Security

> **Windows Security** is your home to manage the tools that protect your device and your data. 

Security has four protection areas:

- **Virus and Threat Protection**
- **Firewall & Network Protection**
- **App & Browser Control**
- **Device Security**

### Virus and Threat Protection

> Divided into two parts: 
> 	**Current threats**
> 	**Virus & threat protection settings**

##### Current Threats

Scan options:

- **Quick scan** - Checks folders in your system where threats are commonly found
- **Full scan** - Checks all files and running programs on your hard disk. This scan could take longer than an hour.
- **Custom scan** - Choose which files and locations you want to check.

Threat History:

- **Last Scan** - Windows Defender Antivirus automatically scans your device for viruses and other threats to help keep it safe.
- **Quarantined threats** - Quarantined threats have been isolated and prevented from running on your device. They will be periodically removed
- **Allowed threats** - Allowed threats are items identified as threats, which you allowed to run on your device.

##### Virus & Threat Protection Settings

**Manage settings** 

- **Real-time protection** - Locates and stops malware from installing or running on your device.
- **Cloud-delivered protection** - Provides increased and faster protection with access to the latest protection data in the cloud.
- **Automatic sample submission** - Send sample files to Microsoft to help protect you and others from potential threats. 
- **Controlled folder access** - Protect files, folders, and memory areas on your device from unauthorized changes by unfriendly applications.
- **Exclusions** - Windows Defender Antivirus won't scan items that you've excluded.
- **Notifications** - Windows Defender Antivirus will send notifications with critical information about the health and security of your device.

**Ransomware protection**

- **Controlled folder access** - Ransomware protection requires this feature to be enabled, which in turn requires Real-time protection to be enabled.

### Firewall and Network Protection

What is a **firewall**?

Per Microsoft, "_Traffic flows into and out of devices via what we call ports. A firewall is what controls what is - and more importantly isn't - allowed to pass through those ports. You can think of it like a security guard standing at the door, checking the ID of everything that tries to enter or exit_".

What is the difference between the three domains? (Public, Private and Domain)

- **Domain** - the domain profile applies to networks where the host system can authenticate to a domain controller
- **Private** - The private profile is a user-assigned profile and is used to designate private or home networks
- **Public** - The default profile is the public profile, used to designate public networks such as Wi-Fi hotspots at coffee shops, airports and other locations

### App & Browser Control 

In this section, you can change the settings for the **Microsoft Defender SmartScreen**

Per Microsoft, "_Microsoft Defender SmartScreen protects against phishing or malware websites and applications, and the downloading of potentially malicious files_".

**Check apps and files**

> Windows Defender Smart Screen helps protect your device by checking for unrecognized apps and files from the web.

**Exploit Protection**

- Exploit protection is built into Windows 10 to help protect your device against attacks.

### Device Security

**Core Isolation**

**Memory Integrity**: - prevents attacks from inserting malicious code into high-security processes

What is the Trusted Platform Module?

*Trusted Platform Module technology is designed to provide hardware-based, security-related functions. A TPM chip is a secure cryptoprocessor that is designed to carry out cryptographic operations. The chip includes multiple physical security mechanisms to make it tamper resistant, and malicious software is unable to tamper with the security functions of the TPM.*

### BitLocker

> **Bitlocker Drive Encryption** is a data protection feature that integrates with the operating system and addresses the threats of data theft or exposure from lost, stolen or inappropriately decommissioned computers. 

Per Microsoft, "_BitLocker provides the most protection when used with a Trusted Platform Module (TPM) version 1.2 or later. The TPM is a hardware component installed in many newer computers by the computer manufacturers. It works with BitLocker to help protect user data and to ensure that a computer has not been tampered with while the system was offline_".

### Volume Shadow Copy Service

> The **Volume Shadow Copy Service** (VSS) coordinates the required actions to create a consistent shadow copy (also known as a snapshot or a point-in-time copy) of the data that is to be backed up.

Volume Shadow Copies are stored on the System Volume Information folder on each drive that has the protection enabled.

If VSS is enabled (**System Protection** turned on), you can perform the following tasks from within **advanced system settings**. 

- **Create a restore point**
- **Perform system restore**
- **Configure restore settings**
- **Delete restore points**

From a security perspective, malware writers know about this Windows feature and write code in their malware to look up these files and delete them. Doing so makes it impossible to recover from a ransomware attack unless you have an offline/off-site backup.

