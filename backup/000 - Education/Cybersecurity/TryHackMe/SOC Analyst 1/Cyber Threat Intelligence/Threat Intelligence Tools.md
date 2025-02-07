> This room will cover the concepts of Threat Intelligence and various open-source tools that are useful.

The learning objectives include:

- Understanding the basics of threat intelligence & it's classifications.
- Using *UrlScan.io* to scan for malicious URLs. 
- Using *Abuse.ch* to track malware and botnet indicators.
- Investigate phish emails using *PhishTool*
- Using Cisco's Talos Intelligence platform for gathering intel

# Threat Intelligence

> **Threat intelligence is the analysis of data and information using tools and techniques to generate meaningful patterns on how to mitigate against potential risks associated with existing or emerging threats targeting organizations, industries, sectors or governments.**

To mitigate against risks, we can start by trying to answer a few simple questions:

- Who is attacking?
- What's their motivation?
- What are their capabilities?
- What artefacts and indicators of compromise should you look out for?

### Threat Intelligence Classifications:

Threat Intel is geared towards understanding the relationship between your operational environment and your adversary. With this in mind, we can break down threat intel into the following classifications: 

- **Strategic Intel:** High-level intel that looks into the organisation's threat landscape and maps out the risk areas based on trends, patterns and emerging threats that may impact business decisions.
- **Technical Intel:** Looks into evidence and artefacts of attack used by an adversary. Incident Response teams can use this intel to create a baseline attack surface to analyse and develop defence mechanisms.
- **Tactical Intel:** Assesses adversaries' tactics, techniques, and procedures (TTPs). This intel can strengthen security controls and address vulnerabilities through real-time investigations.
- **Operational Intel:** Looks into an adversary's specific motives and intent to perform an attack. Security teams may use this intel to understand the critical assets available in the organisation (people, processes, and technologies) that may be targeted.
### URLScan.io

> [**Urlscan.io**](https://urlscan.io) is a free service developed to assist in scanning and analyzing websites. It is used to automate the process of browsing and crawling through websites to record activities and interactions. 

When a URL is submitted, the information recorded includes the domains and IP addresses contacted, resources requested from the domains, a snapshot of the web page, technologies utilized and other metadata about the website.

The site provides two views, the first one showing the most recent scans performed and the second one showing current live scans.

#### Scan Results

URL scan results provide ample information, with the following key areas being essential to look at:

- **Summary**: Provides general information about the URL, ranging from the identified IP address, domain registration details, page history and a screenshot of the site. 
- **HTTP**: Provides information on the HTTP connections made by the scanner to the site, with details about the data fetched and the file types received.
- **Redirects**: Shows information on any identified HTTP and client-side redirects on the site.
- **Links**: Shows all identified links outgoing from the site's homepage.
- **Behavior**: Provides details of the variables and cookies found on the site. These may be useful in identifying the frameworks used in developing the site.
- **Indicators**: Lists all IPs, domains and hashes associated with the site. These indicators do not imply malicious activity related to the site.
### Abuse.sh

> [Abuse.ch](https://abuse.ch) is a research project hosted by the Institute for Cybersecurity and Engineering at the Bern University of Applied Sciences in Switzerland.
> 
> 	It was developed to identify and track malware and botnets through several operational platforms developed under the project. 

These platforms are:

- **Malware Bazaar**: A resource for sharing malware samples.
- **Feodo Tracker**: A resource used to track botnet command and control (C2) infrastructure linked with Emotet, Dridex and TrickBot.
- **SSL Blacklist**: A resource for collecting and providing a blocklist for malicious SSL certificates and JA3/JA3s fingerprints.
- **URL Haus**: A resource for sharing malware distribution sites.
- **Threat Fox**: A resource for sharing indicators of compromise.
#### [MalwareBazaar](https://bazaar.abuse.ch)

> As the name suggests, this project is an all in one malware and analysis database. The project supports the following features:

- **Malware Samples Upload**: Security analysts can upload their malware samples for analysi and build the intelligence database. This can be done through the browser on an API.
- **Malware Hunting**: Hunting for malware samples is possible through setting up alerts to match various elements such as tags, signatures, YARA rules, ClamAV signatures and vendor detection.
#### [FeodoTracker](https://feodotracker.abuse.ch)

> With this project, Abuse.ch is targeting to share intelligence on botnet Command & Control servers associated with Dridex, Emotet (aka Heodo), TrickBot, QakBot and BazarLoader/BazarBackdoor.

This is achieved by providing a database of the C&C servers that security analysts can search through and investigate any suspicious IP addresses they have come across.

- Additionally, they provide various IP and IOC blocklists and mitigation information to be used to prevent botnet infections.
#### [SSL Blacklist](https://sslbl.abuse.ch)

> Abuse.ch developed this tool to identify and detect malicious SSL connections. From these connections SSL certificates used by botnet C2 servers would be identified and updated on a denylist that is provided for use. 

The denylist is also used to identify JA3 fingerprints that would help detect and block malware botnet C2 communications on the TCP layer.

*You can browse through the SSL certificates and JA3 fingerprints lists or download them to add to your deny list or threat hunting rulesets.*
#### [URLhaus](https://urlhaus.abuse.ch)

> As the name points out, this tool focuses on sharing malicious URLs used for malware distribution. As a security analyst, you can search through the database for domains, URLs, hashes and filetypes that are suspected to be malicious and validate your investigations.

The tool also provides feeds associated with country, AS number and Top Level Domain that an analyst can generate based on specific search needs. 
#### [ThreatFox](https://threatfox.abuse.ch)

> With ThreatFox, security analysts can search for, share and export indicators of compromise associated with malware. IOCs can be exported in ***various formats such as MISP events, Suricata IDS ruleset, Domain Host files, DNS Response Policy Zone, JSON files and CSV files.*** 
# PhishTool

### Email Phishing

> Email phishing is one of the main precursors of any cyber attack. Unsuspecting user get duped into opening and accessing malicious files and links sent to them by email, as they appear to be legitimate.

- As a result, adversaries infect their victim's systems with malware, harvesting their credentials and personal data and performing other actions such as financial fraud or conducting ransomware attacks.

[PhishTool](https://www.phishtool.com) seeks to elevate the perception of phishing as a server form of attack and provide a responsive means of email security. 

Through email analysis, security analysts can *uncover email IOCs, prevent breaches and provide forensic reports that could be used in phishing containment and training engagements.*

PhishTool has two accessible versions: **Community** and **Enterprise**. We shall mainly focus on the community version and the core features in this task.

The core features include:

- **Perform email analysis**: PhishTool retrieves metadata from phishing emails and provides analysts with the relevant explanations and capabilities to follow the emails actions, attachments and URLs to triage the situation.
- **Heuristic Intelligence**: OSINT is baked into the tool to provide analysts with the intelligence needed to stay ahead of persistent attacks and understand what TTPs were used to evade security controls and allow the adversary to social engineer a target.
- **Classification and Reporting**: Phishing email classifications are conducted to allow analysts to take action quickly. Additionally, reports can be generated to provide a forensic record that can be shared.

Additional features are available on the Enterprise version:

- Manage user-reported phishing events
- Report phishing email findings back to users and keep them engaged in the process
- Email stack integration with Microsoft 365 and Google Workspace

### Analysis Tab

Once uploaded, we are presented with the details of our email for a more in-depth look. Here, we have the following tabs:

- **Headers**: Provides the routing information of the email, such as source and destination email addresses, originating IP and DNS addresses and Timestamp.
- **Received Lines**: Details on the email traversal process across various SMTP servers for tracing purposes.
- **X-Headers**: These are extension headers added by the recipient mailbox to provide additional information about the email. 
- **Security**: Details on email security frameworks and policies such as *Sender Policy Framework (SPF), DomainKeys Identified Mail (DKIM) and Domain-Based Message Authentication, Reporting and Conformance (DMARC)*
- **Attachments**: Lists any file attachments found in the email.
- **Message URLs**: Associated external URLs found in the email will be found here.

We can further perform lookups and flag indicators as malicious from these options. On the right-hand side of the screen, we are presented with the Plaintext and Source details of the email.

> Above the `plaintext` section, we have a `Resolve` checkmark. Here, we get to perform the resolution of our analysis by classifying the email, setting up flagged artefacts and setting the classification codes.
> 
> 	Once the email has been classified, the details will appear on the `Resolution` tab on the analysis of the email.
# Cisco Talos Intelligence

> IT and Cybersecurity companies collect massive amounts of information that could be used for threat analysis and intelligence. 

Being one of those companies, Cisco assembled a large team of security practitioners called Cisco Talos to provide actionable intelligence, visibility on indicators, and protection against emerging threats through data collected from their products. 

The solution is accessible as [Talos Intelligence](https://talosintelligence.com).

Cisco Talos encompasses six key teams:

- **Threat Intelligence & Interdiction**: Quick correlation and tracking of threats provide a means to turn simple IOCs into context-rich intel.
- **Detection Research**: Vulnerability and malware analysis is performed to create rules and content for threat detection.
- **Engineering & Development**: Provides the maintenance support for the inspection engines and keeps them up to date to identify and triage emerging threats.
- **Vulnerability Research & Discovery**: Working with service and software vendors to devleop repeatable means of identifying and reporting security vulnerabilities.
- **Communities**: Maintains the image of the team and the open-source solutions.
- **Global Outreach**: Disseminates intelligence to customers and the security community through publications.

> More information about Cisco Talos can be found on their [White Paper](https://www.talosintelligence.com/docs/Talos_WhitePaper.pdf)

### Talos Dashboard

>Accessing the open-source solution, we are first presented with a reputation lookup dashboard with a world map. 
>	This map shows an overview of email traffic with indicators of whether the emails are legitimate, spam or malware across numerous countries. 
>		Clicking on any marker, we see more information associated with IP and hostname addresses, volume on the day and the type.

At the top, we have several tabs that provide different types of intelligence resources. The primary tabs that an analyst would interact with are:

- **Vulnerability Information**: Disclosed and zero-day vulnerability reports marked with CVE numbers and CVSS scores. Details of the vulnerabilities reported are provided when you select a specific report, including the timeline taken to get the report published. Microsoft vulnerability advisories are also provided, with the applicable snort rules that can be used.

- **Reputation Center**: Provides access to searchable threat data related to IPs and files using their SHA256 hashes. Analysts would rely on these options to conduct their investigations. Additional email and spam data can be found under the `Email & Spam Data tab`.

