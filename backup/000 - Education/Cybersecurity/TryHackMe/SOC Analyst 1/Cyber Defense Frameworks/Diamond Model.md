**The Diamond Model of Intrusion Analysis** was developed by cybersecurity professionals - Sergio Caltagirone, Andrew Pentergast, and Christopher Betz in 2013.

[As described by its creators](https://www.activeresponse.org/wp-content/uploads/2013/07/diamond.pdf), the Diamond Model is composed of four core features: adversary, infrastructure, capability, and victim, and establishes the fundamental atomic element of any intrusion activity.

Why is it called a "Diamond Model"? The four core features are edge-connected, representing their underlying relationships and arranged in the shape of a diamond.

> The Diamond Model carries the essential concepts of intrusion analysis and adversary operations while allowing the flexibility to expand and encompass new ideas and concepts.
> 
> 	The model provides various opportunities to integrate intelligence in real-time for network defense, automating correlation across events, classifying events with confidence into adversary campaigns, and forecasting adversary operations while planning and gaming mitigation strategies.

### Adversary

> An **adversary** is also known as an attacker, enemy, cyber threat actor, or hacker. 
> 
> The adversary is the person who stands behind the cyberattack.
> 	Cyber attacks can be an intrusion or a breach.

According to the creators of the Diamond Model, an adversary is an actor or organization responsible for utilizing a capability against the victim to achieve their intent. 

- Adversary knowledge can generally be mysterious, and this core feature is likely to be empty for most events -- at least at the time of discovery.

It is essential to know the difference between **adversary operator** and **adversary customer** because it will help you understand *intent, attribution, adaptability, and persistence* by helping to frame the relationship between and adversary and victim pair.

It is difficult to identify an adversary during the first stages of a cyberattack. Utilizing data collected from an incident or breach, signatures, and other relevant information can help you determine who the adversary target might be.

**Adversary Operator** is the "hacker" or persons conducting the intrusion activity

**Adversary Customer** is the entity that stands to benefit from the activity conducted in the intrusion. It may be the same person who stands behind the adversary operator, or it may be separate person or group. 

### Victim

**Victim** - is the target of an adversary. 

- A victim can be an organization, person, target email address, IP address, domain, etc.
- It's essential to understand the *difference between the victim persona and the victim assets because they serve different analytical functions.* 

> A victim can be an opportunity for attackers to get a foothold on the organization they are trying to attack. 
> 
> 	There is always a victim in every cyberattack.
> 	For example, the spearphishing email (a well-crafted email targeting a specific person of interest) was sent to the company, and someone (victim) clicked on the link.
> 		In this case, the victim is the selected target of interest for an adversary.

**Victim Personae** are the people and organizations being targeted and whose assets are being attacked and exploited. 
	These can be organization names, people's names, industries, job roles, interests, etc.

**Victim Assets** are the attack surface and include:

- Sets of systems
- Networks
- Email Addresses
- Hosts
- IP addresses
- Social Networking Accounts

### Capability

**Capability** - also know as the skill, tools and techniques used by the adversary in the event. The capability highlights the adversary's tactics, techniques and procedures (TTPs).

- The capability can include all techniques used to attack the victims, from the less sophisticated methods, such as manual password guessing, to the most sophisticated techniques, like developing malware or a malicious tool.

**Capability Capacity** is all of the vulnerabilities and exposures that the individual capability can use.

An **Adversary Arsenal** is a set of capabilities that belong to an adversary. The combined capacities of an adversary's capabilities make it the adversary's arsenal.

- An adversary must have the required capabilities. The capabilities can be malware and phishing email development skills or, at least, access to capabilities, such as acquiring malware or ransomware as a service.

### Infrastructure

**Infrastructure** - also known as software or hardware. Infrastructure us the physical or logical interconnections that the adversary uses to deliver a capability or maintain control of capabilities.

- For example, a command and control centre (C2) and the results from the victim (data exfiltration)

**Type 1 Infrastructure** is the infrastructure controlled or owned by the adversary

**Type 2 Infrastructure** is the infrastructure controlled by an intermediary. Sometimes the intermediary might not be aware of it. 
- This is the infrastructure that a victim will see as the adversary. 
- Type 2 infrastructure has the purpose of obfuscating the source of the activity. 
- Type 2 infrastructure includes:
	- Malware staging servers
	- Malicious domain names
	- Compromised email accounts

**Service Providers** are organizations that provide services considered critical for the adversary availability of Type 1 and Type 2 infrastructure, for example, Internet Service Providers, domain registrars, and webmail providers.

### Event Meta Features

> Six possible features can be added to the Diamond Model. Meta-features are not required, but they can add some valuable information or intelligence to the diamond model.

- **Timestamp** - date and time of the event. Each event can be recorded with a date and time that it occured, such as 2021-09-12 02:10:12:136.
	- The timestamp can include when the event started and stopped.
	- Timestamps are essential to help determine the patterns and group the malicious activity.
	- For example, if an attack happened at 3am in the United States, it might be possible that the attack was carried out from a specific country with a different time zone and standard business hours.
- **Phase** - these are the phases of an intrusion, attack or breach. According to the diamond model creators and Axiom 4 *"Every malicious activity contains two or more phases which must be successfully executed in succession to achieve the desired result."* 
	- Malicious activities do not occur as single events, but rather as a sequence of events. 
	- See the ***Cyber Kill Chain*** developed by Lockheed Martin for details on each phase.
- **Result** - While the results and post-conditions of an adversary's operations will not always be known or have a high confidence value when they are known, they are helpful to capture. 
	- It is crucial to capture the results and post-conditions of an adversary's operations, but sometimes they might not always be known.
	- The events can be labelled as "success", "failure", or "unknown". 
	- The event results can also be related to the CIA triad, such as *Confidentiality Compromised*, *Integrity Compromised,* and *Integrity Compromised*. 
	- Another approach can also be documenting all of the post-conditions resulting from the event, for example, information gathered in the reconnaissance stage or successful passwords/sensitive data exfiltration.
- **Direction** - This meta-feature helps describe host-based and network-based events and represents the direction of the intrusion attack. 
	- The Diamond Model of Intrusion Analysis defines seven potential values for this meta-feature: 
		1. *Victim-to-Infrastructure*
		2. *Infrastructure-to-Victim*
		3. *Infrastructure-to-Infrastructure*
		4. *Adversary-to-Infrastructure*
		5. *Infrastructure-to-Adversary*
		6. *Bidirectional* 
		7. *Unknown.*
- **Methodology** - This meta-feature will allow an analyst to describe the general classification of intrusion, for example, phishing, DDoS, breach, port scan, etc.
- **Resources** - According to the diamond model, every intrusion event needs one or more external resources to be satisfied to succeed. 
	- Examples of resources include the following:
		- *Software* (Operating systems, virtualization software, Metasploit framework)
		- *Knowledge* (How to use Metasploit to execute the attack and run the exploit)
		- *Information* (a username/password to masquerade)
		- *Hardware* (servers, workstations, routers)
		- *Funds* (money to purchase domains)
		- *Facilities* (electricity, shelter)
		- *Access* (network path from the source host to the victim and vice versa, network access from an ISP)
# Social Political Component

> The **Social-Political Component** describes the needs and intent of the adversary, for example, financial gain, gaining acceptance in the hacker community, hacktivism, or espionage.

The scenario can be that the victim provides a "product", for example, computing resources and bandwidth as a zombie in a botnet for crypto mining purposes, while the adversary consumes their product or gets financial gain.
# Technology Component

> **Technology** - the technology meta-feature or component highlights the relationship between the core features: capability and infrastructure. 

The capability and infrastructure describe how the adversary operates and communicates. A scenario can be a watering-hole attack which is a methodology where the adversary compromises legitimate websites that they believe their targeted victims will visit.


