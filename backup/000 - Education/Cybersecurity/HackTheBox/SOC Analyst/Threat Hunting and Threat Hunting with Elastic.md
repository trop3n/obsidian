#hackthebox #socanalyst #threathunting #threatmodeling #blueteam 

---
> [[HTB]] | [[001 - Organization/Cheatsheets and Resources/Newsletters/Cybersecurity/Tools/Blue Team|Blue Team]] | [[Cyber Threat Intelligence]] | [[Elasticstack]] 
---
# Threat Hunting Fundamentals

The median between and actual security breach and its detection, otherwise termed ***dwell time***, is usually several weeks, if not months. This implies a potential adversarial presence within a network for a span approaching three weeks, a duration that can be significantly impactful. 

This alarming fact underscores the growing inefficacy of traditional, defense-oriented cybersecurity tactics. In response, we advocate for  a *paradigm shift* towards a **proactive, offensive strategy** -- the initiation of ***threat hunting***. 

`Threat Hunting` is an active, human-led, and often hypothesis-driven practice that systematically combs through network data to identify stealthy, advanced threats that evade existing security solutions. This strategic evolution from a conventionally reactive posture allows us to uncover insidious threats that automated detection systems or external entities such as law enforcement might not discern.

The principal objective of threat hunting is to substantially reduce dwell time by recognizing malicious entities at the *earliest stage* of the cyber kill chain. This proactive stance has the potential to prevent threat actors from entrenching themselves deeply within our infrastructure and to swiftly neutralize them.

The threat hunting process commences with the identification of assets -- systems or data -- that could be high-value targets for threat actors. Next, we analyze the TTPs (**Tactics, Techniques**
and **Procedures**) these adversaries are likely to employ, based on current threat intelligence. We subsequently strive to proactively detect, isolate, and validate any artifacts related to the abovementioned TTPs and any anomalous activity that deviates from established baseline norms. 

During the hunting endeavor, we regularly employ Threat Intelligence, a vital component that aids in formulating hunting hypotheses, developing counter-tactics, and executing protective measures to prevent system compromise. 

Key facets of **threat hunting** include:

- An offensive, `proactive` strategy that prioritizes *threat anticipation* over reaction, based on hypotheses, attacker TTPs, and intelligence. 
- An offensive, `reactive` response that searches across the network for artifacts related to a `verified` incident, based on evidence and intelligence.
- A solid, practical comprehension of threat landscape, cyber threats, adversarial TTPs, and the cyber kill chain.
- Cognitive empathy with the attacker, fostering an understanding of the adversarial mindset.
- A profound knowledge of the organization's IT environment, network topology, digital assets, and normal activity. 
- Utilization of high-fidelity data and tactical analysis, and leveraging advanced threat hunting tools and platforms.
## The Relationship Between Incident Handling & Threat Hunting

So, how does threat hunting intersect with the various phases of Incident Handling?

- In the `Preparation` phase of incident handling, a threat hunting team must set up robust, clear rules of engagement. Operational protocols must be established, outlining when and how to intervene, the course of action in specific scenarios, and so forth. Organizations must choose to weave threat hunting into their existing incident handling policies and procedures, obviating the need for separate threat hunting policies and procedures. 

- During the `Detection & Analysis` phase of incident handling, a threat hunter's acumen is indispensable. They can augment investigations, ascertain whether the observed indicators of compromise (IoCs) truly signify an incident, and further, their adversarial mindset can help uncover additional artifacts or IoCs that might have been missed initially.

- In the `Containment, Eradication and Recovery` phase, some organizations might expect hunters to perform tasks within the **Containment**, **Eradication**, and **Recovery** stages. However, this is not a universally accepted practice. The specific roles and responsibilities of the hunting team will be stipulated in the procedural documents and security policies. 

- Regarding the `Post-Incident Activity` phase of incident handling, hunters, with their extensive expertise spanning various IT domains and IT Security, can contribute significantly. They can proffer recommendations to fortify the organization's overall security posture.

We tried to shed light on the symbiotic relationship between incident handling and threat hunting. Whether these processes should be integrated or function independently is a strategic decision, contingent upon each organization's unique threat landscape, risk, etc.

---
## A Threat Hunting Team's Structure

The construction of a threat hunting team is a strategic and meticulously planned process that requires a diverse range of skills, expertise, and perspectives. It is crucial that each member of the team offers a unique set of competencies that, when combined, provide a holistic and comprehensive approach to *identifying, mitigating* and *eliminating threats*.

The ideal threat hunting team composition typically includes the following roles:

- `Threat Hunter`: The core role within the team, threat hunters are cybersecurity professionals with a deep understanding of the threat landscape, cyber adversaries' Tactics, Techniques and Procedures (TTPs), and sophisticated threat detection methodologies. They proactively search for Indicators of Compromise (IoCs) and are proficient in using a variety of threat hunting tools and platforms.

- `Threat Intelligence Analyst`: These individuals are responsible for gathering and analyzing data from a variety of sources, including:
	- Open-Source Intelligence
	- Dark Web Intelligence
	- Industry Reports
	- Threat Feeds
		Their job is to understand the current threat landscape and predict future trends, providing valuable insights to threat hunters.

- `Incident Responders`: When threat hunters identify potential threats, incidents responders step in to manage the situation. They investigate the incident thoroughly and they are also responsible for containment, eradication, and recovery actions, and they ensure that the organization can quickly resume normal operations.

- `Forensics Experts`: These are team members who delve deep into the technical details of an incident. They are proficient in digital forensics and incident response, capable of reverse engineering malware, analyzing malware, and providing detailed incident reports.

- `Data Analysts/Scientists`: They play a pivotal role in examining large datasets, using statistical models, machine learning algorithms, and data mining techniques to uncover patterns, correlations, and trends that can lead to actionable insights for threat hunters.

- `Security Engineers/Architects`: Security engineers are responsible for the overall design of the organization's security infrastructure. They ensure that all systems, applications and networks are designed with *security in mind*, and they often work closely with threat hunters to develop and implement tools and techniques that facilitate threat hunting, as well as **kill-chain** defenses.

- `Network Security Analyst`: These professionals specialize in network behavior and traffic patterns. They understand the normal ebb and flow of network activity and can quickly identify anomalies indicative of a potential breach. 

- `SOC Manager`: The Security Operations Center (SOC) manager oversees the operations of the threat hunting team, ensuring smooth coordination among team members and effective communication with the rest of the organization.
## When Should We Hunt?

In the realm of cybersecurity, threat hunting should not be seen as sporadic or reactionary practice, but rather as a sustained, forward-thinking activity. Nevertheless, there are specific instances that call for an immediate and intense threat hunting operation. Here's a more intricate breakdown of these instances:

- `When NEw Information or an Adversary Comes to Light`: The cybersecurity landscape is always evolving, with fresh intel on potential threats and system vulnerabilities being uncovered regularly. If there's a newly discovered adversary or a vulnerability associated with an application that our network utilizes, this calls for an immediate threat hunting session. It's imperative to decipher the adversary's modus operandi and scrutinize the vulnerability to evaluate the possible risk to our systems. 
	- For instance, if we stumble on a previously unknown vulnerability in a widely utilized application, we'd promptly kickstart a threat hunting initiative to seek out any signs of exploitation. 

- `When New Indicators are Associated with a Known Adversary`: Often, cybersecurity intelligence sources release new indicators of compromise tied to specific adversaries. If these indicators are associated with an adversary known for targeting networks akin to ours or if we've been a past target of the same adversary, we need to launch a threat hunting initiative. This aids in detecting any traces of the adversary's activities within our system, allowing us to ward off potential breaches.

- `When Multiple Network Anomalies are Detected`: Network anomalies might sometimes be harmless, caused by system glitches or valid alterations. However, several anomalies appearing concurrently or within a short period might hint at a systemic issue or an orchestrated attack. In such cases, it's crucial to carry out threat hunting to pinpoint the root cause of these anomalies and address any possible threats. For instance, if we observe odd network traffic behavior or unexpected system activities, we'd initiate threat hunting to probe these anomalies.

- `During an Incident Response Activity`: Upon the detection of a confirmed security incident, our Incident Response (IR) team will concentrate on containment, eradication, and recovery. Yet, while the IR process is in motion, it's vital to simultaneously conduct threat hunting across the network. This enables us to expose any connected threats that might not be readily visible, understand the full extent of the compromise, and avert further harm. For example, during a confirmed malware infiltration, while the IR team is dealing with the infected system, threat hunting can assist in identifying other potentially compromised systems.

- `Periodic Proactive Actions`: Beyond the scenarios mentioned above, it's crucial to note that threat hunting should not simply be a reactive task. Regular, proactive threat hunting exercises are key to discovering latent threats that may have slipped past our security defenses. This guarantees a continual monitoring strategy, bolstering out overall security stance and minimizing the prospective impact of an attack.

In a nutshell, the ideal time for threat hunting is always the present. A proactive stance on threat hunting lets us detect and neutralize threats before they can inflict substantial damage.

---
## The Relationship Between Risk Assessment & Threat Hunting

Risk assessment, as an essential facet of cybersecurity, enables a comprehensive understanding of the potential vulnerabilities and threat vectors within an organization. In the context of threat hunting, risk assessment serves as a key enabler, allowing us to prioritize our hunting activities and focus our efforts on the areas of **greatest potential impact**.

To begin with, risk assessment entails a systematic process of identifying and evaluating risks based on potential threat sources, existing vulnerabilities, and the potential impact should these vulnerabilities be exploited. It involves a series of steps including *asset identification*, *threat* 
*identification*, *vulnerability identification*, *risk determination*, and finally, *risk mitigation strategy formulation*.

In the threat hunting process, the information gleaned from a thorough risk assessment can guide our activities in several ways:

- `Prioritizing Hunting Efforts`: By recognizing the most critical assets (often referred to as "crown jewels") and their associated risks, we can prioritize out threat hunting efforts on these areas. Assets could include sensitive data repositories, mission-critical applications, or key network infrastructure.

- `Understanding Threat Landscape`: The threat identification step of the risk assessment allows us to understand the threat landscape better, including TTPs used by potential threat actors. This understanding assists us in developing our hunting hypotheses, which are *essential* in proactive threat hunting.

- `Highlighting Vulnerabilities`: Risk assessment helps to highlight vulnerabilities in our systems, applications and processes. Knowing these weaknesses enables us to look for exploitation indicators in these areas. For instance, if we know a particular application has a vulnerability that allows for privilege escalation, we can look for anomalies in user privilege levels.

- `Informing the Use of Threat Intelligence`: Threat intelligence is often used in threat hunting to identify malicious behavior. Risk assessment helps inform the application of threat intelligence by identifying the most likely threat actors and their preferred method of attack.

- `Refining Incident Response Plans`: Risk assessment also plays a critical role in refining Incident Response plans. Understanding the likely risks helps us anticipate and plan for potential breaches, ensuring a swift and effective response.

- `Enhancing Cybersecurity Controls`: Lastly, the risk mitigation strategies derived from risk assessment can directly feed into enhancing existing cybersecurity controls and defenses, further strengthening the organization's security posture.

The technicalities of employing risk assessment for threat hunting include the use of advanced tools and techniques. These range from automated vulnerability scanners and penetration testing tools to sophisticated threat intelligence platforms. For instance, SIEM (Security Information and Event Management) systems can be used to aggregate and correlate events from various sources, providing a holistic view of the organization's security status and aiding in threat hunting.

In essence, risk assessment and threat hunting are deeply intertwined, each augmenting the other to create a more robust and resilient cybersecurity posture. By regularly conducting comprehensive risk assessments, we can better focus our threat hunting activities, thereby reducing dwell time, mitigating potential damage, and enhancing our overall cybersecurity defense.
# Threat Hunting Process

Below is a brief description of the threat hunting process.

- `Setting the Stage`: The initial phase is all about planning and preparation. It includes laying out clear targets based on a deep understanding of the threat landscape, our business's critical requirements, and our threat intelligence insights. The preparation phase also encompasses making certain environment is ready for effective threat hunting, which might involve enabling extensive logging across our systems and ensuring threat hunting tools, such as SIEM, EDR, IDS are correctly set up. Additionally, we stay informed about the most recent cyber threats and familiarize ourselves with threat actor profiles. 

> [!Example] `Example`
> During the planning and preparation phase, a threat hunting team might conduct in-depth research on the latest threat intelligence reports, analyze industry specific vulnerabilities, and study the tactics, techniques and procedures employed by threat actors. They may also identify critical assets and systems within the organization that are most likely to be targeted. As part of the preparation, extensive logging mechanisms can be implemented across servers, networks devices, and endpoints to capture relevant data for analysis. Threat hunting tools like SIEM, EDR, and IDS are configured to collect and correlate logs, generate alerts, and provide visibility into potential security incidents. Additionally, the team stays updated on emerging cyber threats by monitoring threat feeds, subscribing to relevant security mailing lists, and participating in information sharing communities.

- `Formualating Hypotheses`: The next step involves making educated predictions that will guide our threat hunting journey. These hypotheses can stem from various sources, like recent threat intelligence, industry updates, alerts from security tools, or even our professional intuition. We strive to make these hypotheses testable to guide us where to search and what to look for.

> [!Example] `Example`
> A hypothesis might be that an attacker has gained access to the network by exploiting a particular vulnerability through phishing emails. This hypothesis could be derived from recent threat intelligence reports that highlight similar attack vectors. It could also be based on an alert triggered by an intrusion detection system indicating suspicious network traffic patterns. The hypothesis should be specific and testable, such as "An advanced persistent threat (APT) group is leveraging a known vulnerability in the organization's web server to establish a command-and-control (C2) channel."

- `Designing the Hunt`: Upon crafting a hypothesis, we need to develop a hunting strategy. This includes recognizing the specific data sources that need analysis, the methodologies and tools we'll use, and the particular indicators of compromise (IoCs) or patterns we'll hunt for. At this point, we might also create customs scripts or queries and utilize dedicated threat hunting tools.

> [!Example] `Example`
> The threat hunting team may decide to analyze we server logs, network traffic logs, DNS logs, or endpoint telemetry data. They define the search queries, filters, and correlation rules to extract relevant information from the collected data. The team also leverages threat intelligence feeds and open source intelligence (OSINT) to identify specific indicators of compromise (IoCs) associated with the suspected threat actor or known attack techniques. This may involve crafting custom scripts or queries to search for known attack techniques. This may involve crafting custom scripts or queries to search for IoCs or using specialized threat hunting platforms that automate the process. 

- `Data Gathering and Examination`: This phase is where the active threat hunt occurs. It involves *collecting necessary data*, such as **log files**, **network traffic data**, **endpoint data**, and then analyzing this data using the predetermined methodologies and tools. Our goal is to find evidence that either supports or refutes our original hypothesis. This phase is highly iterative, possibly involving refinement of the hypothesis or the investigation approach as we uncover new information.

> [!example] `Example`
> The threat hunting team might examine web server access logs to identify unusual or unauthorized access patterns, analyze network traffic captures to detect suspicious communications with external domains, or investigate endpoint logs to identify anomalous behavior or signs of compromise. They apply data analysis techniques such as *statistical analysis*, *behavioral analysis*, or *signature-based* detection to identify potential threats. They might employ tools like log analyzers, packet analyzers, or malware sandboxes to extract information from the collected data and uncover hidden indicators of compromise. 

- `Evaluating Findings and Testing Hypotheses`: After analyzing the data, we need to interpret the results. This could involve confirming or disproving the hypothesis, understanding the behavior of any detected threats, identifying affected systems, or determining the potential impact of the threat. This phase is crucial, as it will inform the next steps in terms of response and remediation. 

> [!Example] `Example`
> The threat hunting team might discover a series of failed login attempts from an IP address associated with a known threat actor, confirming the hypothesis of an attempted credential brute-force attack. They might also find evidence of suspicious outbound domains, supporting the hypothesis of a command-and-control (C2) communication channel. The team conducts deeper investigations to understand the behavior of the identified threats, assess the scope of the compromise, and determine the potential impact on the organization's systems and data. 

- `Mitigating Threats`: If we confirm a threat, we must undertake remediation actions. This could involve isolating affected systems, eliminating malware, patching vulnerabilities, or modifying configurations. Our goal is to eradicate the threat and limit any potential damage. 

> [!Example] `Example`
> If the threat hunting team identifies a compromised system communicating with a C@ server, they may isolate the affected system from the network to prevent further data exfiltration or damage. They may deploy endpoint protection tools to remove malware or perform forensic analysis on the compromised system to gather additional evidence and determine the extent of the breach. Vulnerabilities identified
>during the threat hunting process can be patched or mitigated to prevent future attacks. Network configurations can be adjusted to restrict unauthorized access or to strengthen security controls. 

- `After the Hunt`: Once the threat hunting cycle concludes, it's crucial to document and share the findings, methods and outcomes. This might involve *updating threat intelligence platforms*, *enhancing detection rules*, *refining incident response playbooks*, or *improving security policies*. It's also vital to learn from each threat hunting mission to enhance future efforts. 

> [!example] `Example`
> Once the threat hunting cycle concludes, the team documents the findings, methodologies, and outcomes of the investigation. They update threat intelligence platforms with newly discovered indicators of compromise (IoCs) and share relevant information with other teams or external partners to enhance the collective defense against threats. They may improve detection rules within security tools based on the observed attack patterns and refine incident response playbooks to streamline future incident handling. Lessons learned from the hunt are incorporated into security policies and procedures, and training programs are adjusted to enhance the organization's overall security posture.

- `Continous Learning and Enhancement`: Threat hunting is not a one-time task, but a continuous process of learning and refinement. Each threat hunting cycle should *feed into the next*, allow for continuous improvement of hypotheses, methodologies, and tools based on the evolving threat landscape and the organization's changing risk profile.

> [!example] `Example`
> After each threat hunting cycle, the team reviews the effectiveness of their hypotheses, methodologies, and tools. They analyze the results and adjust their approach based on lessons learned and new threat intelligence. For example they might enhance their hunting techniques by incorporating machine learning algorithms or behavioral analytics to detect more sophisticated threats. They participate in industry conferences, attend training sessions, and collaborate with other threat hunting teams to stay updated on the latest attack techniques and defensive strategies.

> Threat hunting is a delicate balance of art and science. It demands technical prowess, creativity, and a profound understanding of both the organization's environment and the broader threat landscape. The most successful threat hunting teams are those that learn from each and constantly hone their skills and processes.

---
## The Threat Hunting Process vs. Emotet

Let's see how the abovementioned threat hunting process could have been applied to hunt for [emotet malware](https://www.cisa.gov/news-events/cybersecurity-advisories/aa20-280a) within an organization. 

- `Setting the Stage`: During the planning and preparation phase, the threat hunting team extensively researches the Emotet malware's TTPs by studying previous attack campaigns, analyzing malware samples, and reviewing threat intelligence reports specific to Emotet. They gain a deep understanding of Emotet's infection vectors, such as malicious email attachments or links, and the exploitation of vulnerabilities in software or operating systems. The team identifies critical assets and systems that are commonly targeted by Emotet, such as endpoints with administrative privileges or email servers.

- `Formulating Hypotheses`: Hypotheses in the context of Emotet threat hunting might be based on known Emotet IoCs or patterns observed in previous attacks. For example, a hypothesis could be that Emotet is using a new phishing technique to distribute malicious payloads via compromised email accounts. This hypothesis could be derived from recent threat intelligence reports highlighting similar Emotet campaigns or based on alerts triggered by email security systems detecting suspicious email attachments. The hypothesis should be specific, such as "Emotet is using compromised email accounts to send phishing emails with malicious Word documents containing macros."

- `Designing the Hunt`: In the design phase, the threat hunting team determines the relevant data sources and collection methods to validate or invalidate the Emotet-related hypotheses. They may decide to analyze email server logs, network traffic logs, endpoint logs, or sandboxed malware samples. They define search queries, filter and correlation rules to extract information related to Emotet's specific characteristics, such as email subject lines, attachment types, or network communication patterns associated with Emotet infections. They leverage threat intelligence feeds to identify Emotet-related IoCs, such as known command-and-control (C2) server addresses or file hashes associated with Emotet payloads.

- `Data Gathering and Examination`: During the active threat hunting phase, the team collects and analyzes data from various sources to detect Emotet-related activities. For example, they might examine email server logs to identify patterns of suspicious email attachments or analyze network traffic captures to detect communication with known Emotet C2 servers. They apply *data analysis* techniques, such as:
	- email header analysis
	- network traffic pattern analysis
	- behavioral analysis
- to identify potential Emotet infections. They utilize tools like:
	- email forensics software
	- network packet analyzers
	- sandbox environments
- to extract relevant information from the collected data and uncover hidden indicators of Emotet activity.

- `Evaluating Findings and Testing Hypotheses`: In this phase, the team evaluates the findings from data analysis to confirm or refute the initial Emotet-related hypotheses. For example, they might discover a series of emails with similar subject lines and attachment types associated with Emotet campaigns, confirming the hypothesis of ongoing Emotet phishing activities. They might also find evidence of network connections to known Emotet C2 servers, supporting the hypothesis of an active Emotet infection. The team conducts deeper investigations to understand the behavior of the identified Emotet infections, assess the scope of the compromise, and determine the potential impact of the organization's systems and data.

- `Mitigating Threats`: If Emotet infections are confirmed, the team takes immediate remediation actions. They isolate affected systems from the network to prevent further spread of the malware and potential data exfiltration. They deploy endpoint protection tools to detect and remove unauthorized access. They patch or mitigate vulnerabilities exploited by Emotet to prevent future infections. Network configurations are adjusted to block communication with known Emotet C2 servers or malicious domains.

- `After the Hunt`: Once the Emotet threat hunting cycle concludes, the team documents their findings, methodologies, and outcomes. They update threat intelligence platforms with new Emotet-related IoCs and share relevant information with other teams or external partners to enhance their collective defense against Emotet. They improve detection rules within security tools based on the observed Emotet attack patterns and refine incident response playbooks to streamline future incident handling. Lessons learned from the Emotet hunt are incorporated into security policies and procedures, and training programs are adjusted to enhance the organization's overall defenses against Emotet and similar malware.

- `Continous Learning and Enhancement`: Threat hunting for Emotet is an ongoing process that requires continuous learning and improvement. After each Emotet threat hunting cycle, the team reviews the effectiveness of their hypotheses, methodologies, and tools. They analyze the results and adjust their approach based on lessons learned and new Emotet-related threat intelligence. For example they might enhance their hunting techniques by incorporating advanced behavior-based detection mechanisms or machine learning algorithms specifically designed to identify Emotet's evolving TTPs. They actively participate in industry conferences, attend training sessions, and collaborate with other threat hunting teams to stay updated on the latest Emotet attack techniques and defensive strategies.
# Threat Hunting Glossary

Within the domain of cybersecurity and threat hunting, several crucial terms and concepts play a pivotal role. Here's an enriched understanding of these:

- `Adversary`: An adversary, within the realm of Cyber Threat Intelligence (CTI), refers to an entity driven by shared objectives as your organization, albeit unauthorized, seeking to infiltrate your business and satisfy their collection requirements, which may include financial gains, insider information, or valuable intellectual property. these adversaries possess varying levels of technical expertise and are motivated to circumvent your security measures.
	- Adversaries can be classified into distinct categories, including:
		- `cyber criminals`
		- `insider threats`
		- `hacktivists`
		- `state-sponsored operators`
	- Each category exhibits unique characteristics and motivations in their pursuit of unauthorized access and exploitation.

- `Advanced Persistent Threat (APT)`: APTs are typically associated with **highly organized groups** or **nation-state entities** that possess extensive resources, thereby enabling them to carry out their malicious activities over prolonged periods. While APTs target various sectors, they show a marked preference for *high-value targets*, which can include governmental organizations, healthcare infrastructures, and defense systems.

	Contrary to what the name might suggest, being labeled as an APT doesn't necessarily imply that the group utilizes technologically advanced techniques. Rather "Advanced" refers to the sophisticated strategic planning, and "Persistent" alludes to their dogged persistence in achieving their objectives, backed by substantial resources including, but not limited to, financial backing, manpower and time.

- `Tactics, Techniques and Procedures (TTPs)`: A term borrowed from the military, TTPs symbolize the distinct operational patterns or 'signature' of an adversary.

	- `Tactics`: This term describes the strategic objectives and high-level concepts of operations employed by the adversary. Essentially, it addresses the 'why' behind their actions.
	- `Techniques`: These are the specific methods utilized by an adversary to accomplish their tactical objectives, providing the 'how' behind their actions. Techniques don't provide step-by-step instructions but rather describe the *general approach* to achieving a goal.
	- `Procedures`: These are the granular, step-by-step instructions, essentially the 'recipe' for the implementation of each technique.

	Analyzing TTPs offers deep insights into how an adversary penetrates a network, moves laterally within it, and achieves their objectives. Understanding TTPs allows for the creation of Indicators of Compromise (IoCs), which can help detect and thwart future attacks.

- `Indicator`: An indicator, when analyzed in CTI, encompasses both technical data and contextual information. Isolated technical data lacking relevant context holds limited or negligible value for network defenders. Contextual details allow for a comprehensive understanding of the indicator's significance, enabling effective threat analysis and response.

![](https://i.imgur.com/np141rs.png)

- `Threat`: A threat is a multifaceted concept, consisting of three fundamental factors, intent, capability, and opportunity.

![](https://i.imgur.com/IUXjCal.png)

1. Firstly, `intent` signifies the underlying rationale driving adversaries to target and exploit your network infrastructure. This intent can range from corporate espionage to financial gains through cybercrime, or even targeting your business relationships with other entities.

2. Secondly, `capability` denotes the tools, resources and financial backing that adversaries possess to carry out their operations successfully. Their skill level in penetrating your network and the availability of sufficient financial resources determine their capability to sustain ongoing attacks against your organization.

3. Lastly, `opportunity` refers to conditions or events that provide favorable circumstances for adversaries to execute their operations. This encompasses instances where adversaries acquire relevant emails addresses or credentials from your network, as well as their awareness of vulnerabilities in specific software systems.

- `Campaign`: A campaign refers to a collection of incidents that share similar Tactics, Techniques and Procedures (TTPs) and are believed to have comparable collection requirements. This type of intelligence necessitates substantial time and effort to aggregate and analyze, as businesses and organizations progressively report and uncover related malicious activities.

- `Indicators of Compromise (IOCs)`: IOCs are *digital traces* or *artifacts* derived from active or past intrusions. They serve as 'signposts' of a specific adversary or malicious activity. IOCs can include a wide array of elements such as the hashes of malicious files, suspicious IP addresses, URLs, domain names, and names of malicious executables or scripts. Continually tracking, cataloging, and analyzing IOCs can greatly enhance our threat detection capabilities, leading to faster and more effective responses to cyber threats.

- `Pyramid of Pain`: Pyramid of Pain is a critical visualization which presents a hierarchy of indicators that can support us in detecting adversaries. It also showcases the degree of difficulty in acquiring these specific indicators and the subsequent impact of gathering intelligence on them. The Pyramid of Pain concept was brought to life by David Bianco from FireEye in his insightful presentation, [Intel-Driven Detection and Response to Increase Your Adversary’s Cost of Operations.](https://rvasec.com/slides/2014/Bianco_Pyramid%20of%20Pain.pdf) As we ascend the Pyramid of Pain, obtaining adversary-specific Indicators of Compromise (IOCs) becomes increasingly challenging. However, the flip side is that acquiring these specific IOCs forces the adversary to alter their attack methodologies, a task that is far from simple for them.

![](https://i.imgur.com/fLbAkK3.png)

- `Hash Values`: Hash values are the **digital fingerprints of files**. They are created using algorithms like MD5, SHA-1, or SHA-256 that take an input (or 'message') and return a fixed-size string of bytes. For instance, malware binaries can be identified through their unique hash values. However, a slight change to the file, such as adding a byte or changing a single character, will dramatically alter the hash value, making it an easy-to-change and therefore, less reliable indicator.

- `IP Addresses`: IP addresses are unique identifiers for devices on a network. They can be used to track the source of network traffic or a potential attack. However, adversaries often use tactics such as IP spoofing, VPNs, proxies, or TOR networks to hide their true IP addresses, making this level of indicator easy to change and somewhat unreliable.

- `Domain Names`: Domains are used to identify one or more IP addresses. For example, the domain name `www.example.com` represents about a dozen IP addresses. Malicious actors often use domain generation algorithms to produce a large number of pseudo-random domain names to evade detection. They can also use dynamic DNS services to quickly change the IP addresses associated with a domain.

- `Network/Host Artifacts`:

	- `Network Artifacts`: These are residual traces of an attacker's activities within the network infrastructure. They can be found in network logs, packet captures, netflow data, or DNS request logs, to name a few. Examples might include certain patterns in network traffic, unique packet headers, or unusual protocol usage. Network artifacts are challenging for an attacker to modify without impacting the effectiveness or stealth of their operation.

	- `Host Artifacts`: On the other hand, host artifacts refer to remnants of malicious activity left on individual systems or endpoints. These could be found within system logs, file systems, registry keys, list of running processes, loaded DLLs, or even in volatile memory. For instance, unusual entries in the Windows Registry, unique file paths, or suspicious running processes could all be considered host artifacts. These indicators are also fairly hard for an adversary to alter without affecting their intrusion campaign or revealing their presence. 

	- Analyzing these artifacts can provide valuable insights into an adversary's tools, techniques and procedures (TTPs), and help in the detection and prevention of future attacks. However, the higher position of Network and Host Artifacts in the Pyramid of Pain indicates that they are harder to utilize for detection, and also harder for the attacker to change or obfuscate.

- `Tools`: Tools refer to the software used by adversaries to conduct their attacks. This could include malware, exploits, scripts, or command and control (C2) frameworks. Identifying the tools used by an adversary can provide valuable insight into their capabilities and intentions. However, sophisticated adversaries often use custom tools or modify existing ones to evade detection.

- `TTPs (Tactics, Techniques, and Procedures)`: This is the pinnacle of the Pyramid of Pain. TTPs refer to the specific methods used by adversaries to conduct their attacks. Tactics describe the adversary's overall objectives, techniques describe the actions taken to achieve those objectives, and procedures are the exact steps taken to execute the techniques. Identifying an adversary's TTPs can provide the most valuable insights into their operations and are the most difficult for an adversary to change without significant cost and effort. Examples might include;
	- use of spear-phishing for initial access
	- exploitation of a specific software vulnerability
	- specific steps taken to exploit that vulnerability

- `Diamond Model`: The [Diamond Model of Intrusion Analysis](https://apps.dtic.mil/sti/pdfs/ADA586960.pdf) is a conceptual framework designed to illustrate the fundamental aspects of a cyber intrusion. This model, developed by Sergio Caltagirone, Andrew Pendergast, and Christopher Betz, aims to provide a more structured approach to understand, analyze, and respond to cyber threats.

The model is structured around four key components, represented as vertices of a diamond:

![](https://i.imgur.com/ZP8oDUw.png)

- `Adversary`: This represents the individual, group or organization responsible for the cyber intrusion. It's important to understand their capabilities, motivations, and intent to effectively defend against their attacks.
- `Capability`: This represents the tools, techniques, and procedures (TTPs) that the adversary uses to carry out the intrusion. This could include malware, exploits, and other malicious tools, as well as the specific methods used to deploy these tools. 
- `Infrastructure`: This represents the physical and virtual resources that the adversary uses to facilitate the intrusion. It can include servers, domain names, IP addresses, and other network resources used to deliver malware, control compromised systems, or exfiltrate data. 
- `Victim`: This represents the target of the intrusion, which could be an individual, organization, or system. Understanding the victim's vulnerabilities, the value of their assets, and their potential exposure to threats is crucial for effective defense.

These four components are connected by bidirectional arrows, representing the dynamic relationships and interactions between them. For example, an adversary uses capabilities through an infrastructure to target a victim. This model allows for the capture of complex relationships and the construction of robust strategies for threat detection, mitigation, and predication. 

Comparing this to the Cyber Kill Chain model, we can see that the Diamond Model provides a more detailed view of the cyber intrusion ecosystem. While the Cyber Kill Chain focuses more on the stages of an attack (from recon to actions on objectives), the Diamond Model provides a more *holistic* view of the components involved in the intrusion and their relationships.

Let's consider a technical example to illustrate the Diamond Model: Suppose a financial institution (Victim) is targeted by a cybercriminal group (Adversary). The group uses spear-phishing emails (Capability) sent from a botnet (Infrastructure) to deliver a banking Trojan. When a recipient clicks on a malicious link in the email, the Trojan is installed on their system, allowing the cybercriminals to steal sensitive financial data.

In this scenario, the Diamond Model helps to highlight the interplay between the different components of the intrusion. By analyzing these components and their interactions, the financial institution can gain a deeper understanding of the threat they're facing and develop more effective strategies for mitigating this and future threats. This could involve strengthening their email security protocols, monitoring for signs of the specific banking Trojan, or implementing measures to detect and respond to unusual network activity associated with the botnet.

Overall, the Diamond Model provides a complementary perspective to the Cyber Kill Chain, offering a different lens through which to understand and respond to cyber threats. Both models can be useful tools in the arsenal of a cybersecurity professional.
# Threat Intelligence Fundamentals
## Cyber Threat Intelligence Definition

`Cyber Threat Intelligence` (CTI) represents a vital asset in our arsenal, providing essential insights to fortify our defenses again cyberattacks. The primary objective of our CTI team is to transition our defense strategies from merely reactive measures to a more proactive, anticipatory approach. They contribute crucial insights to our Security Operations Center (SOC).

Four fundamental principles make CTI an integral part of our cybersecurity strategy:

![](https://i.imgur.com/gqhl0Bh.png)

- `Relevance`: The cyber world is awash with diverse sources of information, from social media posts and security vendor reports to shared insights from similar organizations. However, the true value of this information lies in its relevance *to our organization*. 
	- For instance, if there is a reported vulnerability in a software that we, or our trusted partner organizations, do not use, the urgency to implement defensive measures is naturally diminished.

- `Timeliness`: Swift communication of intelligence to our defense team is *crucial* for the implementation of effective mitigation measures. The value of information depreciates over time -- freshly discovered data is more valuable, and 'aged' indicators lose their relevance as they might no longer be used by the adversary or may have been resolved by the affected organization.

- `Actionability`: Data under analysis by a CTI analyst should yield actionable insights for our defense team. If the intelligence doesn't offer clear directives for action, its value diminishes. Intelligence must be scrutinized until it yields *relevant*, *timely* and *actionable* insights for our network defense. Unactionable intelligence can lead to self-perpetrating cycles of non-productive analysis, often referred to as a **self-licking ice cream cone**.

- `Accuracy`: Before disseminating any intelligence, it must be verified for accuracy. Incorrect indicators, misattributions, or flawed TTPs can result in wastage of valuable time and resources. If the accuracy of any information is uncertain, it should be label with a confidence indicator, ensuring that our defense team is aware of potential inaccuracies.

When these four factors synergize, the intelligence gleaned allows us to:

- Gain insights into potential adversary operations and campaigns that might be targeting our organization.
- Enrich our data pool through analysis by CTI analysts and other network defenders.
- Uncover adversary TTPs, enabling the development of effective mitigation measures and enhancing our understanding of adversary behavior. 
- Provide decision-makers within our organization with pertinent information for informed, impactful decision-making related to business operations.

---
## The Difference Between Threat Intelligence & Threat Hunting

***Threat Intelligence*** and ***Threat Hunting*** represent two distinct, yet intrinsically linked, specialties within the realm of cybersecurity. While they serve separate functions, they both contribute significantly to the development of a comprehensive security analyst. However, it's important to note that they are not *substitutes* for each other.

**Threat Intelligence** (Predictive): The primary aim here is to anticipate the adversary's moves, ascertain their targets, and discern their methods of information acquisition. The adversary has a specific objective, and as a team involved in threat intelligence, our mission is to predict:

- The location of the attack
- The timing of the attack
- The operational strategies the adversary will employ
- The ultimate objectives of the adversary

**Threat Hunting** (Reactive and Proactive): Yes, the two terms are opposites, but they encapsulate the essence of Threat Hunting. An initiating event or incident, whether it occurs within our network or in a network of a similar industry, prompts our team to launch an operation to ascertain whether an adversary is present in the network, or if one was present and evaded detection.

Ultimately, Threat Intelligence and Threat Hunting bolster each other, strengthening our organization's overall network defense posture. As our Threat Intelligence team analyzes adversary activities and develops comprehensive adversary profiles, this information can be shared with our Threat Hunting analysts to inform their operations. Conversely, the findings from Threat Hunting can equip our Threat Intelligence analysts with additional data to refine their intelligence and enhance the accuracy of their predictions.

---
## Criteria of Cyber Threat Intelligence

What truly makes Cyber Threat Intelligence (CTI) valuable? What issues does it resolve? As discussed earlier, for CTI to be effective, it must be:

- *Actionable*
- *Timely*
- *Relevant*
- *Accurate*

These four elements form the foundation of robust CTI that ultimately provides visibility into adversary operations. Additionally, well-constructed CTI brings forth secondary benefits, such as:

- Understanding of threats to our organization and partner activities
- Potential insights into our organization's network
- Enhanced awareness of potential problems that may have gone unnoticed. 

Furthermore, from a leadership standpoint, high-quality CTI aids in fulfilling the business objective of minimizing risk as much as possible. As intelligence about an adversary targeting our business is gathered and analyzed, it empowers leadership to adequately assess the risk, formulate a contingency action plan if an incident occurs, and ultimately frame the problem and disseminate the information in a coherent and meaningful way.

![](https://i.imgur.com/WPYdjau.png)


As this information is compiled, it transforms into intelligence. This intelligence can then be classified into three different categories, each having various degrees of relevance for different teams within our organization. These categories are:

1. **Strategic Intelligence**
2. **Operational Intelligence**
3. **Tactical Intelligence**

In the diagram below, the ideal intersection is *right at the core*. At this convergence juncture, the Cyber Threat Intelligence (CTI) analyst is equipped to offer the most comprehensive and detailed portrait of the adversary and their modus operandi.

![](https://i.imgur.com/3AkJf4s.png)

`Strategic Intelligence` is characterized by:

- Being consumed by C-Suite executives, VPs and other company leaders
- Aiming to align intelligence directly with company risks to inform decisions
- Providing an overview of the adversary's operations over time
- Mapping TTPs and Modus Operandi (MO) of the adversary
- Striving to answer the **Who** and **Why**
	- `Example`: A report containing strategic intelligence might outline the threat posed by APT28 (also known as Fancy Bear), a nation-state actor linked to the Russian Government. This report could cover the group's past campaigns, its motivations (such as political espionage), targets (governments, military, and security organizations), and long-term strategies. The report might also explore how the group adapts its tactics and tools over time, based on historical data and the geopolitical context. 

`Operational Intelligence` is characterized by:

- Also including TTPs of an adversary (similar to Strategic Intelligence)
- Providing information on adversary campaigns
- Offering more detail that what's found in strategic intelligence reports
- Being produced for mid-level management personnel
- Working towards answering the **How** and **Where**
	- `Example`: A report containing operational intelligence can provide detailed analysis of a ransomware campaign conducted by the REvil Group. It would include how the group gains initial access (like through phishing or exploiting vulnerabilities), its lateral movement tactics (such as credential dumping and exploiting Windows admin tools), and its method of executing the ransomware payload (maybe after hours to maximize damage and encrypt as many systems as possible).

`Tactical Intelligence` is characterized by:

- Delivering immediate actionable information
- Being provided to network defenders for swift action
- Including technical details on attacks that have occurred or could occur in the near future
	- `Example`: A report containing tactical intelligence could include specific IP addresses, URLs, or domains linked to the REvil command and control servers, hashes of known REvil ransomware samples, specific file paths, registry keys, or mutexes associated with REvil, or even distinctive strings within the ransomware code. This type of information can be directly used by security technologies and incident responders to detect, prevent, and respond to specific threats.

It's crucial to understand that there's a degree of overlap among these three types of intelligence. That's why we represent the intelligence in a Venn diagram. Tactical intelligence contributes to forming an operational picture and a strategic overview. The converse is also true.

---
## How to Go Through a Tactical Threat Intelligence Report

Interpreting threat intelligence reports loaded with tactical intelligence and Indicators of Compromise (IOCs) is a task that requires a structured methodology to optimize our responsiveness as SOC analysts or threat hunters. Let's delve into a procedural, in-depth process using a theoretical scenario involving a threat intelligence report on an elaborate Emotet malware campaign:

- `Comprehending the Report's Scope and Narrative`: The initial phase of interpreting the report involves comprehending its broader context. Suppose our report elucidates an ongoing Emotet campaign directed towards businesses in our sector. The report may offer macro-level insights about the attacker's objectives and the types of entities in their crosshairs. By grasping the narrative, we can assess the pertinence of the threat to our business. 

- `Spotting and Classifying the IOCs`: Tactical intelligence typically encompasses a list of IOCs tied to the threat. In the context of our Emotet scenario, these might include IP addresses linked to command and control (C2) servers, file hashes of the Emotet payloads, email addresses or subject lines leveraged in phishing campaigns, URLs of deceptive websites. or distinct Registry alterations by the malware. We should partition these IOCs into categories for more comprehensible understanding and actionable results: Network-based IOCs (IPs, domains), Host-based IOCs (file hashes, registry keys), and Email-based IOCs (email addresses, subject lines). Furthermore, IOCs could also contain **Mutex** names generated by the malware, SSL certificate hashes, specific API calls enacted by the malware, or even patterns in network traffic (such as specific User-Agents, HTTP headers, or DNS request patterns). Moreover, IOCs can be augmented with supplementary data. For instance, IP addresses can be supplemented with geolocation data, WHOIS information, or associated domains.

- `Comprehending the Attack's Lifecycle`: The report will likely depict the TTPs deployed by the attackers, correspondingly mapped to the MITRE ATT&CK framework. For the Emotet campaign, it might commence with a spear-phishing email (Initial Access), proceed to execute the payload (Execution), establish persistence (Persistence), execute defense evasion tactics (Defense Evasion), and ultimately exfiltrate data or deploy secondary payloads (Command and Control). Comprehending this lifecycle aids us in forecasting the attacker's moves and formulating an effective response. 

- `Analysis and Validation of IOCs`: Not all IOCs hold the same utility or accuracy. We need to *authenticate them*, typically by cross-referencing with additional threat intelligence sources or databases such as VirusTotal or AlienVault's OTX. We also need to contemplate the age of IOCs. Older ones *may not be as pertinent* if the attacker has modified their infrastructure or tactics. Moreover, contextualizing IOCs is critical for their correct interpretation. 
	- For example, an IP address employed as a C2 server may also host legitimate websites due to IP sharing in cloud environments. Analysts should also consider the sources reliability and whether the IOC has been whitelisted in the past. Ultimately, understanding the false positive rate is crucial to avoid **alert fatigue**.

- `Incorporating the IOCs into our Security Infrastructure`: Once authenticated, we can integrate these IOCs into our security solutions. This might involve updating firewall rules with malicious IP addresses or domains, incorporating file hashes into our EDR solution, or creating new IDS/IPS signatures. For email-based IOCs, we can update our email security gateway or anti-spam solution. When implementing IOCs, we should consider the *potential impact on business operations*. 
	- For example, blocking an IP address might affect a business-critical service. In such cases, alerting rather than blocking might be more appropriate. Additionally, all changes should be documented and approved following change management procedures to maintain system integrity and avoid unintentional disruptions.

- `Proactive Threat Hunting`:  Equipped with insights from the report, we can proactively hunt for signs of the Emotet threat in our environment. This might involve searching for logs for network connections to the C2 servers, scanning endpoints for the identified file hashes, or checking email logs for the phishing email indicators. Threat hunting shouldn't be limited to searching for IOCs. We should also look for broader signs of TTPs described in the report. 
	- For instance, Emotet often employs PowerShell for execution and evasion. Therefore, we might hunt for suspicious PowerShell activity, even if it doesn't directly match an IOC. This approach aids in detecting variants of the threat not covered by the specific IOCs in the report.

- `Continuous Monitoring and Learning`: After implementing the IOCs, we must continually monitor our environment for any hits. Any detection should trigger a predefined incident response process. Furthermore, we should utilize the information gleaned from the report to enhance our security posture. This could involve user education around the phishing tactics employed by the Emotet group or improving our detection rules to catch specific evasion techniques employed by this malware. While we should unquestionably learn from each report, we should also contribute back to the threat intelligence community. If we discover new IOCs or TTPs, these should be shared with threat intelligence platforms and ISACs/ISAOs (Information Sharing Analysis Centers/Organizations) to aid other organizations in defending against the threat. 

This meticulous, step-by-step process, while tailored to our Emotet example, can be applied to any threat intelligence report containing tactical intelligence and IOCs. The secret is to be systematic, comprehensive, and proactive in our approach to maximize the value we derive from these reports.
# Hunting for Stuxbot
## Threat Intelligence Report: Stuxbot

The present Threat Intelligence report underlines the immediate menace posed by the organized cybercrime collective known as "Stuxbot". The group initiated its phishing campaigns earlier this year and operates with a broad scope, seizing upon opportunities as they arise, without any specific targeting strategy -- their motto seems to be anyone, anywhere, anytime. The primary motivation behind their actions appears to be espionage, as there have been no indications of them exfiltrating sensitive blueprints, proprietary business information, or seeking financial gain through methods such as ransomware or blackmail.

- Platforms in the Crosshairs: `Microsoft Windows`
- Threatened Entities: `Windows users`
- Potential Impact: `Complete takeover of the victim's computer / Domain escalation`
- Risk Level: `Critical`

The group primarily leverages opportunistic-phishing for initial access, exploiting data from social media, past breaches, (e.g. databases of email addresses), and corporate websites. There is scant evidence suggesting spear-phishing against specific individuals. 

The document compiles all known TTPs and IOCs linked to the group, which are currently under continuous refinement. This preliminary sketch is confidential and meant exclusively for our partners, who are strongly advised to conduct scans of their infrastructures to spot potential successful breaches at the earliest possible stage.

In summary, the attack sequence for the initially compromised device can be laid out as follows:

![](https://i.imgur.com/SMgAfsP.png)
### Initial Breach

The phishing email is relatively rudimentary, with the malware posing as an invoice file. Here's and example for an actual phishing email that includes a link leading to a OneNote file:

![](https://i.imgur.com/qaLCmh6.png)

Our forensic investigation into these attacks revealed that the link directs to a OneNote file, which has consistently been hosted on a file hosting service (e.g. Mega.io or similar platforms).

This OneNote file masquerades as an invoice featuring a 'HIDDEN' button that triggers and embedded batch file. This batch file, in turn, fetches PowerShell scripts, representing stage 0 of the malicious payload. 
### RAT Characteristics

The RAT deployed in these attacks is modular, implying that it can be augmented with an infinite range of capabilities. While only a few features are accessible once the RAT is staged, we have noted the use of tools that capture screen dumps, execute [Mimikatz](https://attack.mitre.org/software/S0002/), provide an interactive `CMD Shell` on compromised machines, and so forth. 
### Persistence

All persistence mechanisms utilized to date have involved an EXE file deposited to disk.
### Lateral Movement

So far, we have identified two distinct methods for lateral movement:

- Leveraging the original, Microsoft-signed PSExec
- Using WinRM
### Indicators of Compromise

The following provides a comprehensive inventory of all identified IOCs to this point. 
#### OneNote File:

- httpx://transfer.sh/get/kNxU7/invoice.one
- httpx://mega.io/dl9o1Dz/invoice.one
#### Staging Entity (PowerShell Script)

- httpx://pastebin.com/raw/AvHtdKb2
- httpx://pastebin.com/raw/gj58DKz
#### Command and Control (C&C) Nodes

- 91.90.213.14:443
- 103.248.70.64:443
- 141.98.6.59:443
#### Cryptographic Hashes of Involved Files (SHA256):

- `226A723FFB4A91D9950A8B266167C5B354AB0DB1DC225578494917FE53867EF2`
- `C346077DAD0342592DB753FE2AB36D2F9F1C76E55CF8556FE5CDA92897E99C7E`
- `018D37CBD3878258C29DB3BC3F2988B6AE688843801B9ABC28E6151141AB66D4`
## Hunting for Stuxbot with the Elastic Stack




























