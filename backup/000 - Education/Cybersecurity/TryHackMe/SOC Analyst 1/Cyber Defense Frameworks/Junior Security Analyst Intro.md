---
up: "[[SOC Analyst 1]]"
tags:
  - "#tryhackme/socanalyst1/jrsecurityanalystintro"
prev:
---

# A Career as a Junior (Associate) Security Analyst

> As a Junior Security Analyst, you will be a triage specialist. You will spend a lot of time triaging or monitoring the event logs and alerts.

Responsibilities for this role include:

- Monitor and investigate the alerts, (most of the time, in a 24x7 SOC environment)
- Configure and manage the security tools
- Develop and implement basic IDS (Intrusion Detection Systems) signatures
- Participate in SOC working groups, meetings
- Create tickets and escalate the security incidents to the Tier 2 and Team lead if needed.

Required Qualifications:

- 0-2 years of experience with Security Operations
- Basic understanding of networking (OSI Mode, TCP/IP model), Operating Systems (Windows, Linux), Web applications.
- Scripting/programming skills are a plus


| Job Role                             | Responsibilities                                            |
| ------------------------------------ | ----------------------------------------------------------- |
| Junior SOC (Tier 1)                  | Monitor network traffic logs and events                     |
|                                      | Works on the tickets, closes the alerts                     |
|                                      | Performs basic investigations and mitigations               |
| Security Operations Analyst (Tier 2) | Focuses on deeper investigations, analysis and remediation. |
|                                      | Proactively hunts for adversaries                           |
|                                      | Monitors and resolves more complex alerts                   |
| SOC Tier 3 (Threat Hunter)           | Works on more advanced investigations                       |
|                                      | Performs advanced threat hunting and adversary research     |
|                                      | Malware reversing                                           |
# Security Operations Center

## Preparation and Prevention

As a Junior Security Analyst, you should stay informed of the current cybersecurity threats (Twitter and Feedly are great resources to keep up with the news related to CySec). 

It's crucial to work on a security roadmap to protect the organization, and be ready for worst-case scenarios.

> Prevention methods include gathering intelligence data on the latest threats, threat actors, and their **TTPS (Tactics, Techniques and Procedures)**.
> 	It also includes the maintenance procedures like updating the firewall signatures, patching the vulnerabilities in the existing systems, block-listing and safe-listing applications, email-addresses and IPs.

To better understand TTPs, look at one of CISA's alerts on APT40 (Chinese Advanced Persistent Threat) at https://us-cert.cisa.gov/ncas/alerts/aa21-200a

## Monitoring and Investigation

A SOC team proactively uses **SIEM (Security Information and Event Management)** and **EDR (Endpoint Detection and Response)** tools to monitor suspicious and malicious network activities. 
- Imagine being a firefighter and having a multi-alarm fire - one-alarm fires, two-alarm fires, three-alarm fires; the categories classify the seriousness of the fire, which is a threat in our case.
- As a security analyst, you will learn how to prioritize the alerts based on their level: Low, Medium, High, and Critical.
- You start from the highest level and work towards the bottom
- Properly configured tools are the best chance at preventing more serious threats

> Junior Analysts play a critical role in the investigation procedure. They perform triaging on the ongoing alerts by exploring and understanding how a certain attack works and preventing bad things from happening if they can. 

During the investigation, it's important to raise the question "How?, When, and why?". Security Analysts find the answers by drilling down on the data logs and alerts in combination with using open-source tools, which we will explore later in this path.
##### Response

After the investigation, the SOC team coordinates and takes action on the compromised hosts, which involves isolating the hosts from the network, terminating the malicious processes, deleting files and more.

### A Day in the Life of a Junior SOC

> One of the most rewarding and exciting things is when you are finished working on an incident and have managed to remediate the threat. Incident Response might take hours, days, or weeks; it all depends on the scale of the attack:
> 	Did the attacker manage to exfiltrate the data?
> 	How much data does the attacker manage to exfiltrate?
> 	Did the attacker attempt to pivot into other hosts?

There are many questions to ask and a lot of detection, containment and remediation to do. 

# The Pyramid of Pain

> This well renowned concept is being applied to cybersecurity solutions like Cisco Security, SentinelOne, and SOCRadar. 

Cisco Security: https://gblogs.cisco.com/ca/2020/08/26/the-canadian-bacon-cisco-security-and-the-pyramid-of-pain/
SentinelOne: https://www.sentinelone.com/blog/revisiting-the-pyramid-of-pain-leveraging-edr-data-to-improve-cyber-threat-intelligence/
SOCRadar: https://socradar.io/re-examining-the-pyramid-of-pain-to-use-cyber-threat-intelligence-more-effectively/

Understanding the Pyramid of Pain concept as a Threat Hunter, Incident Responder, or SOC Analyst is important.

### Hash Values (Trivial)

> As per Microsoft, the hash value is a numeric value of a fixed length that uniquely identifies data. A hash value is the result of a hashing algorithm. The following are some of the most common hashing algorithms.

- **MDS (Message Digest, defined by RFC 1321)** - was designed Ron Rivest in 1992 and is a widely used cryptographic hash function with a 128-bit hash value. MDS hashes are **NOT** considered to be **cryptographically secure**. In 2011, the IETF published RFC 6151, ["Updated Security Considerations for the MD5 Message-Digest and the HMAC-MD5 Algorithms](https://datatracker.ietf.org/doc/html/rfc6151)," which mentioned a number of attacks against MD5 hashes, including the hash collision.

- **SHA-1 (Secure Hash Algorithm 1, defined by [RFC 3174](https://tools.ietf.org/html/rfc3174))** - invented by United States National Security Agency in 1995. When data is fed to SHA-1 Hashing Algorithm, SHA-1 takes an input and produces a 160-bit hash value string as a 40 digit hexadecimal number. [NIST deprecated the use of SHA-1 in 2011](https://csrc.nist.gov/news/2017/research-results-on-sha-1-collisions) and banned its use for digital signatures at the end of 2013 based on it being susceptible to brute-force attacks.
	- NIST recommends migrating from SHA-1 to stronger hash algorithms in the SHA-2 and SHA-3 families

- **The SHA-2 (Secure Hash Algorithm 2)** - SHA-2 Hashing Algorithm was designed by the National Institute of Standards and Technology (NIST) and the National Security Agency (NSA) in 2001 to replace SHA-1. SHA-2 has many variants, and arguably the most common is SHA-256. The SHA-256 algorithm returns a hash value of 256-bits as a 64 digit hexadecimal number.

> A hash is not considered to by cryptographically secure if two files have the same hash value or digest. 

Security professionals usually use the hash values to gain insight into a specific malware sample, a malicious or suspicious file, and as a way to uniquely identify and reference the malicious artifact. 

Online tools for doing hash lookups:

Metadefender Cloud - OPSWAT: https://metadefender.opswat.com/?lang=en

VirusTotal: https://www.virustotal.com/gui/home/upload

---

It's fairly easy to spot a malicious file if we have the hash in our arsenal. However, as an attacker, modifying the file by even a little bit is trivial, which would produce a different hash value. With so many variations and instances of known malware or ransomware, threat hunting using file hashes as the IOC (Indicators of Compromise) can become difficult.

### IP Addess (Easy)

> You may have learned the importance of an IP address from the Networking rooms. An IP address is used to identify any device connected to a network.

- We rely on IP addresses to send and receive information over a network. 

In the Pyramid of Pain, we will evaluate how IP addresses are used as an indicator.

> In the Pyramid of Pain, IP addresses are associated with the color green. You might be asking why and what you can associate the color green with?

- From a defensive standpoint, knowledge of the IP addresses an adversary uses can be valuable. A common defense tactic is to block, drop or deny inbound requests from IP addresses on your parameter or external firewall. 
- This tactic if often not bulletproof as it's trivial for an experienced adversary to recover simply by using a new public IP address.

One of the fastest ways an adversary can make it challenging to successfully carry out IP blocking is by using **Fast Flux**.

According to Akamai, **Fast Flux** is a DNS technique used by botnets to hide fishing, web proxying, malware delivery, and malware communication activities behind compromised hosts acting as proxies. 

- The purpose of using the Fast Flux network is to make the communication between malware and command and control servers challenging to be discovered by security professionals.

*The primary concept of a Fast Flux network is to have multiple IP addresses associated with a domain name, which is constantly changing.*

- Palo Alto created a great fictional scenarios to explain fast flux: ["](https://unit42.paloaltonetworks.com/fast-flux-101/)[Fast Flux 101: How Cybercriminals Improve the Resilience of Their Infrastructure to Evade Detection and Law Enforcement Takedowns"](https://unit42.paloaltonetworks.com/fast-flux-101/)

### Domain Names (Simple)

> Domain names can be thought as simply mapping an IP address to a string of text. A domain name can contain a domain and a top-level domain (evilcorp.com) or a subdomain (tryhackme.evilcorp.com). 
> 	But we will not go into the details of the the Domain Name System (DNS) works. 

Domain names can be a little more of a pain for the attacker to change as they would most likely need to purchase the domain, register it and modify DNS records. Unfortunately for defenders, many DNS providers have loose standards and provide APIs to make it even easier for the attacker to change the domain. 

A **Punycode** attack is used by hackers to redirect users to a malicious domain that seems legit at first glance. 

What is **Punycode**? "Punycode is a way of converting words that cannot be written in ASCII, into a Unicode ASCII encoding."

> To detect malicious domains, proxy logs or web server logs can be used. 

Attackers usually hide the malicious domains under *URL shorteners*. A URL shortener is a tool that creates a short and unique URL that will redirect to the specific website specified during the initial step of setting up the URL shortener link. 

- According to Cofense, attackers use the following URL shortening services to generate malicious links:
	- bit.ly
	- goo.gl
	- ow.ly
	- s.id
	- smarturl.it
	- tiny.pl
	- tinyurl.com
	- x.co

##### Viewing Connections in Any.run:

Because Any.run is a sandboxing service that executes the sample, we can review any connections such as HTTP requests, DNS requests or processes communicating with an IP address. To do so, we can look at the "networking" tab located just below the snapshot of the machine.

*Please Note:* you should be extremely cautious about visiting any of the IP addresses or HTTP requests made in a report. After all, these are behaviors from the malware sample, so they're probably doing something dangerous. 

### Host Artifacts (Annoying)

> On the yellow level of the Pyramid of Pain, the attacker will feel a little more annoyed and frustrated if you can detect the attack.

The attacker would need to circle back at this detection level and change his attack tools and methodologies.

- This is very time-consuming for the attacker, and probably, he will need to spend more resources on his adversary tools.
- Host artifacts are the traces of observables that attackers leave on the system, such as registry values, suspicious process execution, attack patterns or IOCs (*Indicators of Compromise*), files dropped by malicious applications, or anything exclusive to the current threat.


### Network Artifacts (Annoying)

> **Network Artifacts** also belong to the yellow zone in the Pyramid of Pain. 
> This means if you can detect and respond to the threat, the attacker would need more time to go back and change his tactics or modify the tools, which gives you more time to respond and detect the upcoming threats or remediate the existing ones.

A network artifact can be a user-agent string, C2 information, or URI patterns followed by the HTTP POST Requests. 

An attacker might use a User-Agent string that hasn't been observed in your environment before or seems out of the ordinary. The **User-Agent** is defined by [RFC2616](https://datatracker.ietf.org/doc/html/rfc2616#page-145) as the request-header field that contains the information about the user agent originating the request.

Network artifacts can be detected in Wireshark PCAPs (the file that contains the packet of data of a network) by sing a network protocol analyzer such as [TShark](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html) or exploring IDS (Intrusion Detection System) logging from a source such as [Snort](https://www.snort.org/).

> If you can detect the user-agent strings that the attacker is using, you might be able to block them, creating more obstacles and making their attempt to compromise the network more annoying.

### Tools (Challenging)

> At this stage, we have levelled up our detection capabilities against the artifacts. The attacker would most likely give up trying to break into your network or go back and try to create a new tools that serves the same purpose. 

It will be game over for the attackers as they would need to invest some money into building a new tool (if they are capable of doing so). find the tool that has the same potential, or even get some training to learn how to be proficient in a certain tool.

Attackers would use the utilities to create malicious macro documents (**maldocs**) for spearphishing attempts, a backdoor that can be used to establish C2 (**command and control infrastructure**), any custom .EXE, and .DLL files, payloads or password crackers.

> ***Antivirus signatures, detection rules and YARA rules*** can be great weapons for you to use against attackers at this stage. 

- [MalwareBazaar](https://bazaar.abuse.ch/) and [Malshare](https://malshare.com/) are good resources to provide you with access to the samples, malicious feeds, and YARA results - these all can be very helpful when it comes to threat hunting and incident response.
- For detection rules, [SOC Prime Threat Detection Marketplace](https://tdm.socprime.com/) is a great platform, where security professionals share their detection rules for different kinds of threats including the latest CVE's that are being exploited in the wild by adversaries.
- Fuzzy hashing is also a strong weapon against the attacker's tools. Fuzzy hashing helps you to perform similarity analysis - match two files with minor differences based on the fuzzy hash values. One of the examples of fuzzy hashing is the usage of [SSDeep](https://ssdeep-project.github.io/ssdeep/index.html); on the SSDeep official website, you can also find the complete explanation for fuzzy hashing.

### TTPs (Tough)

> TTPS stands for ***Tactics, Techniques and Procedures.*** 

This includes the whole [MITRE](https://attack.mitre.org/) [ATT&CK Matrix](https://attack.mitre.org/), which means all the steps taken by an adversary to achieve his goal, starting from phishing attempts to persistence and data exfiltration.

If you can detect and respond to the TTPs quickly, you leave the adversaries almost no chance at fighting back. 

- For example, if you could detect a Pass-The-Hash attack using Windows Event Log Monitoring and remediate it, you would be able to find the compromised host very quickly and stop the lateral movement inside your network.
- At this point, the attacker would have two options:

1. Go back, do more research and training, reconfigure their custom tools
2. Give up and find another target

### Conclusion

Now you have learned the concept of the Pyramid of Pain. Maybe it is time to apply this in practice. Please, navigate to the Static Site to perform the exercise.   

You can pick any APT (Advanced Persistent Threat Groups) as another exercise. A good place to look at would be [FireEye Advanced Persistent Threat Groups](https://www.fireeye.com/current-threats/apt-groups.html). When you have determined the APT Group you want to research - find their indicators and ask yourself: " What can I do or what detection rules and approach can I create to detect the adversary's activity?", and "Where does this activity or detection fall on the Pyramid of Pain?”

As David Blanco states, "_**the amount of pain you cause an adversary depends on the types of indicators you are able to make use of**_".


