---
up: "[[000 - Education/Cybersecurity/Red Team/Red Team|Red Team]]"
tags:
  - "#education/books/cybersecurity/redteam/grayhathacking"
source: "[[Gray Hat Hacking 6th Edition1.pdf]]"
---

---
# Chapter 1: Gray Hat Hacking

In this chapter, we cover the following topics: 
- Gray hat hacking
- Vulnerability disclosure
- Advanced persistent threats
- Cyber Kill Chain
- MITRE ATT&CK Framework

What is a gray hat hacker? Why should you care? In this chapter, we attempt to define what a gray hat hacker is and why they are so vital to the cybersecurity field. In short, they stand in the gap between white hat hackers and black hat hackers and serve as ethical hackers, never breaking the law, but instead making the world a better place through applying their skills for good. Now, this concept is controversial, and good people may disagree on this topic. So, in this chapter, we try to set the record straight and give a call to action—that you join us as gray hat hackers and practice ethical hacking in a responsible manner. We also lay the foundation of other critical topics discussed throughout the book.
## Gray Hat Hacking Overview

The phrase "gray hat hacker" has been quite controversial. To some, it means a hacker who occasionally breaks the law or does something unethical to reach a desired end. We, as gray hack hackers, reject that notion. 
## History of Hacking

Ethical hacking has not always been accepted as a legal profession. There was a time when any form of hacking, regardless of intent, was regarded as a *purely criminal exercise*. As technology has evolved and become more pervasive in our lives, so have the understanding of hacking and the laws that govern its use. For many of the readers of this book, these are concepts that are simply lost to history. 

However, it is important to understand this history and give credit to the hard work of the founders of the field who made it possible to pursue this career. 

There was a time when fewer rules governed the use of computers because the skills and knowledge of lawmakers and law enforcement lagged during the rapid evolution of networked systems. Hackers who might attack systems out of curiosity or even mischief, however, had found a new world of opportunity. 

Not everyone indulging their curiosity did so with harm. However, the resulting clash with authority figures who were unable to understand the systems meant many benevolent, bright and intelligent hackers were labelled as criminals by much of the world's software vendors and governments.
### Computer Fraud and Abuse Act

Passed in 1986, was intended to shore up existing computer fraud laws. This expressly prohibited access to computer systems without authorization, or in excess of authorization, and was designed to protect *critical government systems*.
### Digital Millennium Copyright Act

Passed in 1988, and criminalized attacks against access control or digital rights management (DRM). Legitimate researchers in the hacking community were now left to fear that finding vulnerabilities and reporting them could result in legal action or even jail time, according to one or both of these acts, given the argument that code was copyrighted and reverse engineering was therefore illegal, or that unauthorized access to any system (not only government systems) must be criminal (refer to Edelman v. N2H2, Felton et al. v. RIAA, and https://klevchen.ece.illinois.edu/pubs/gsls-ccs17.pdf).

---
Increased pressure for hackers to distinguish themselves from criminals led many researchers to define for themselves a set of ethics that could bring no legal question, while others questioned the chilling effect of the law and the overall reaction to security research. Those in the first camp became known as “white hat hackers,” choosing to discuss known weaknesses with only the minimum amount of detail possible in order to try to get things fixed. These hackers also chose to eschew techniques that might possibly cause harm during their research and to only perform actions that involved full permission. This left the rest to be marked as “black hat hackers,” for anyone who might question the goodness of the law.

Yet, a third group emerged. Hackers who desired not to do harm but to make things better found themselves frustrated by the inability to make positive change in the face of these limitations. Where were the laws to hold software makers accountable for security decisions that negatively impacted consumers?

Discovery of vulnerabilities had not stopped, it had simply been forced underground, while white hat techniques had remained hampered in what they were able to discover by legal limitations on their methods. 
### Gray Hat Hacking

> “First off, being grey does not mean you engage in any criminal activity or condone it. We certainly do not. Each individual is responsible for his or her actions. Being grey means you recognize that the world is not black or white.”
> 
> - L0pht

L0pht and other pioneers in the field used their knowledge to educate authority figures, including testifying in front of congress. This education has helped evolve attitudes toward hacking and security research so that legitimate practitioners today can conduct work that makes computer security better, with less fear of prosecution due to misunderstanding. However, it is a delicate balance, and the battle to maintain that balance continues with every new case, with every new technology, and with every new hacker.
## Ethics and Hacking

"Ethical Hacker" is another term referring to hackers who use their skills for ethical reasons. The problem is, morals, ethics and laws vary among individuals, social groups and governments. In most contexts, the term is designed to differentiate between criminality and lawful behavior -- to differentiate between someone who hacks for the *greater good* and in support of professional pursuits from someone who pursues *personal gain*, *active criminality*, or *harm* with their skills. 

- Guidelines for Ethical Hackers are often codified for certification holders and members of some security organizations that use codes of conduct.
## Definition of Gray Hat Hacking

As you can see, the term “gray hat” comes from an early recognition that there are more “shades of gray,” so to speak, than the polar terms of black and white. Of course, the terms black and white in reference to hackers comes from the old television westerns in the US, where cowboys wearing white hats were the good guys, and the bad guys always wore black hats.

***Gray Hat Hackers***, therefore, are those who operate in between. We choose to operate within the law and ethically, using research and adversarial knowledge to better the world by improving defenses surrounding technology.

There are enough black hat hackers out there; we need more gray hats, stepping in the gap, to protect others. If you enjoy this book, we hope you join us in clearing up the confusion on this topic. Speak up when you hear someone mischaracterize a gray hat hacker. Let’s protect our field, standing up for what is right and good and calling out those who cross the line.
## History of Ethical Hacking

Topics: vulnerability disclosure and bug bounties. 

This will lay the foundation of later topics in this chapters, like APTs, Lockheed Martin Cyber Kill Chain, MITRE ATT&CK, penetration testing, threat intel, threat hunting, and security engineering.
### History of Vulnerability Disclosure

Software vulnerabilities are as old as software itself. Simply put, software vulnerabilities are weaknesses in either the design or implementation of software that may be exploited by an attacker. 

- Not all bugs are vulnerabilities
- Bugs are distinguished from vulnerabilities by using the ***exploitability factor***.
- 1-5% of software defects turn out to be vulnerabilities

As long as humans are developing software, we will have vulnerabilities. As long as there are vulnerabilities, users are at risk.

> [!Important]
> Therefore, it is incumbent on security professionals and researchers to prevent, find, and fix these vulnerabilities before an attacker takes advantage of them, harming the user. This is the ultimate mission of the gray hat hacker.

Many considerations arise during vulnerability disclosure:

- Who to contact
- How to contact them
- What information to provide
- How to assert accountability among all parties in the disclosure

For the vendor, this includes details such as:

- Tracking vulnerability reports
- Performing risk analysis
- Getting the right information for a fix
- Performing cost-benefit analysis for the programming effort to make the fix
- Managing communication with consumers and the person who disclosed the vuln.

> When goals surrounding these considerations do not align between the hacker and the vendor, there is an *opportunity for friction*.

**Key questions arise**:

- How long is enough time for a vendor to make the fix?
- Do the hacker and vendor agree that the fix is important?
- Should someone who reports a vulnerability in good faith be compensated or recognized?
- How long should customers have to make themselves safe by patching before the hacker or vendor releases details about the weakness?
- How much detail is appropriate?
- Will customers apply the patch if they don't understand the danger of not patching?

Some researchers may find non-disclosure untenable if a vendor chooses not to take action on a vulnerability. Lingering danger to consumers in face of the ongoing vulnerability can be frustrating when there is no other authority to hold a vendor responsible for security.

**There is no formal consensus for these matters**.
#### Common Methods of Disclosure:

- Full vendor disclosure
- Coordinated disclosure

In the spirit of ethical hacking, we lean towards the concept of coordinated disclosure.

> [!NOTE]
> These terms are controversial, and some may prefer “partial vendor disclosure” as an option to handle cases when proof of concept (POC) code is withheld and when other parties are involved in the disclosure process. To keep it simple, in this book we will stick with the aforementioned terms
#### Full Vendor Disclosure

Starting around the year 2000, some researchers were more likely to cooperate with vendors and perform full vendor disclosure, whereby the researcher would disclose the vulnerability to the vendor fully and would not disclose it to any other parties. This was due, in part, to the growing openness of vendors to accept public feedback without resorting to legal action. However, the concept of computer security had begun to more thoroughly permeate the vendor space, meaning more companies had begun to adopt formal channels for disclosure.

**Most of these disclosures would require non-disclosure to the public** on the part of the researcher, or the researcher would choose not to publicly disclose details out of a white hat ethos. However, with no formal means for handling these reports, and no source of external accountability, this often led to an unlimited period of time to patch a vuln. The perception that vendors have a lack of incentive to patch a vulnerability led to researcher disenfranchisement that sometimes led hackers to prefer full disclosure.

**Software vendors**, on the other hand, not only had to figure out new processes to address these vulnerabilities, but they struggled with how to manage distribution of updates to their customers. 

- Too many changes in a short time could lead to loss of consumer confidence in the product. 
- Not revealing details about what was fixed might lead consumers not to patch.
- Some consumers had large logistical problems that made patching difficult. 
- How long would it take to reverse-engineer a patch and create a new exploit, and would that be more or less than the time it would take for all consumers to protect themselves?
#### Full Public Disclosure

Many zines, mailing lists, and Usenet groups discussing vulnerabilities were created before a viable disclosure method was created. 

- Hackers used these to build their rep. 
- Others stemmed from the frustration born out of a desire to see things fixed with no formal channel to communicate them,
- Some system owners and vendors didn't understand security; some had no legal reason to care.

However, over the years, frustration built in the hacker community as vendors were not seen as playing fairly or taking the researchers seriously. In 2001, Rain Forest Puppy, a security consultant, made a stand and said that he would only give a vendor one week to respond before he would publish fully and publicly a vulnerability. In 2002, the infamous Full Disclosure mailing list was born and served as a vehicle for more than a decade, where researchers freely posted vulnerability details, with or without vendor notification.

> The full disclosure approach also means that vendors may not fix the actual problem appropriately in their rush to meet arbitrary deadlines.

**Other difficulties arise when a software vendor is dealing with a vulnerability in a library they did not develop.**

For example, when OpenSSL had issues with Heartbleed, thousands of websites, applications and operating system distributions became vulnerable. Each of those software developers had to quickly absorb that information and incorporate fixed upstream version of the library in their application. 
	This takes time, and some vendors move faster than others, leaving many users less safe in the meantime as attackers began exploiting the vuln within days of release. 

Another advantage of full public disclosure is to warn the public so that people may take mitigating steps prior to a fix being released. This notion is based on the premise that *black hats likely know of the issue already*, so arming the public is a good thing and levels the playing field, somewhat, between attackers and defenders.
##### Public Harm

- Is the public safer with or without full disclosure?

Attackers conduct their own research and may know about an issue and be using it already to attack users prior to the vulnerability disclosure. 
#### Coordinated Disclosure

Many hackers have argued that the name "responsible disclosure" implies that attempts to assert vendor accountability are, therefore, "irresponsible". 

The hallmark of coordinated disclosure is using threat of disclosure after a reasonable period of time to hold vendors accountable. The ***Computer Emergency Response Team*** (CERT) coordination center was established in 1988 in response to the **Morris Worm** and has served for nearly 30 years as a facilitator of vulnerability and patch information.

The CERT/CC has established a 45-day grace period when handling vulnerability reports, in that the CERT/CC will publish vulnerability data after 45 days, unless there are extenuating circumstances. Security researchers may submit vulnerabilities to the CERT/CC or one of its delegated entities, and the CERT/CC will handle coordination with the vendor and will publish the vulnerability when the patch is available or after the 45-day grace period. See the “For Further Reading” section for information on the DHS Cybersecurity and Infrastructure Security Agency’s stance on coordinated vulnerability disclosure.
## No More Free Bugs

So far, we have discussed full vendor disclosure, full public disclosure, and responsible disclosure. All of these methods of vulnerability disclosure are **free**, whereby the security researcher spends countless hours finding security vulnerabilities and, for various reasons not directly tied to financial compensation, discloses the vulnerability for the public good. In fact, it is often difficult for a researcher to be paid under these circumstances without being construed as shaking down the vendor.

In 2009, the game changed. At the annual CanSecWest conference, three famous hackers, Charlie Miller, Dino Dai Zovi, and Alex Sotirov, made a stand.19 In a presentation led by Miller, Dai Zovi and Sotirov held up a cardboard sign that read **“NO MORE FREE BUGS.”** 

It was only a matter of time before researchers became more vocal about the disproportionate number of hours required to research and discover vulnerabilities versus the amount of compensation received by researchers. Not everyone in the security field agreed, and some flamed the idea publicly. Others, taking a more pragmatic approach, noted that although these three researchers had already established enough “social capital” to demand high consultant rates, others would continue to disclose vulnerabilities for free to build up their status.Regardless, this new sentiment sent a shockwave through the security field. It was empowering to some, scary to others. No doubt, the security field was shifting toward researchers over vendors.
### Bug Bounty Programs

The concept of bug bounties is an attempt by software vendors to respond to the problem of vulnerabilities in a responsible manner. After all, the security researchers, in the best case, are saving the companies lots of time and money in finding vulnerabilities.

On the other hand, in the worst case, the reports of security researchers, if not handled correctly, may be *prematurely exposed*, thus costing companies lots of time and money due to damage control. 

Therefore, an interesting and fragile economy has emerged as both vendors and researchers have interest and incentives to play well together. 
### Incentives

Bug bounty programs offer many unofficial and official incentives. In the early days, rewards included letters, T- shirts, gift cards, and simply bragging rights. Then, in 2013, Yahoo! was shamed into giving more than swag to researchers. The community began to flame Yahoo! for being cheap with rewards, giving T-shirts or nominal gift cards for vulnerability reports. In an open letter to the community, Ramses Martinez, the director of bug finding at Yahoo!, explained that he had been funding the effort out of his own pocket. 

From that point onward, Yahoo! increased its rewards to $150 to $15,000 per validated report.From 2011 to 2014, Facebook offered an exclusive “White Hat Bug Bounty Program” Visa debit card.27 The rechargeable black card was coveted and, when flashed at a security conference, allowed the researcher to be recognized and perhaps invited to a party. Nowadays, bug bounty programs still offer an array of rewards, including Kudos (points that allow researchers to be ranked and recognized), swag, and financial compensation.
### Controversy Surrounding Bug Bounties

Vendors may use the platforms to rank researchers, but researchers cannot normally rank vendors. Some bug bounty programs are set up to collect reports, but the vendor might not properly communicate with the researcher. Also, there might be no way to tell whether a response of a "duplicate" is indeed accurate.

What's more, the scoring system might be *arbitrary* and not accurately reflect the value of the vulnerability disclosure, given the value of the report on the black market. Therefore, each researcher will need to decide if a bug bounty program is for them and whether the benefits outweigh the downsides.
## Knowing the Enemy: Black Hat Hacking

The famous ancient Chinese general Sun Tzu said it best more than 2,500 years ago: “If you know the enemy and know yourself, you need not fear the result of a hundred battles. If you know yourself but not the enemy, for every victory gained you will also suffer a defeat.”
### Advanced Persistent Threats

Not all black hat hackers are APTs, and not all APTs can be attributed to black hat hackers. Further, this term has become stretched over time to include even more basic forms of attack, which is unfortunate.

That said, it has become a useful description of an advanced adversary that may be used to bring light to their activities and focus attention on the adversary.

As the name implies, APTs:

- Use advanced forms of attack
- Persistent in nature
- Significant threat to the enterprise.

An adversary does not need to drop a zero-day on the front end of their APT attack. There are two reasons for this:

1. Zero days are hard to come by and are *perishable*
2. Zero days are often *not needed* to get into an enterprise

Zero days are typically only dropped *when absolutely needed*, and often as a **secondary attack**, after already gaining a foothold in the enterprise network.
### Lockheed Martin Cyber Kill Chain

The key idea is that adversaries often have *repeatable processes*, which, if discovered early, could be countered in a number of ways. The sooner you discover IoCs and break the kill chain, the cheaper the recovery. The inverse is also true.
#### Reconnaissance

Steps taken by adversaries prior to the attack. Involves both passive and active techniques. Passive techniques are performed without even sending a packet to the target of the attack, instead meta data is gathered indirectly, through public documents, public sources, search engines, and cached web archives. 

Active recon on the other hand involves interacting with the target's website, open interfaces, and may even involve port and serve and API scanning (enumeration) and vulnerability scanning.
#### Weaponization

Weaponization involves the crafting of, or selection of, existing exploits to take advantage of the vulnerabilities found during the reconnaissance phase. Normally, an APT does not have to do anything fancy or use a 0-day at this stage of the attack. 

There are normally unpatched publicly available known vulns that may be used. However, in rate cases, an adversary may craft a special exploit to a custom payload, containing a trojan or other back door, that provides command and control and further functionality. 
#### Delivery

During this phase of the attack, the attacker sends the exploit and payload to the target to take advantage of a discovered vulnerability. This may involve exploits in email or the web, or be as simple as a simple phishing email. 
#### Exploitation

During this phase, the cyber weapon is detonated and is executed in some fashion, either by that "helpful" user or automatically by an application such as an email client or web browser plugin. At this point, the attacker's code is executing on the target host. 
#### Installation

During this stage, the attacker usually performs two actions:

1. ***Gain Persistence***
2. ***Downloads and Executes a Secondary Payload***

When it comes to persistence, the worst thing that can happen to an attacker at this phase is the user closes the application that is running the malicious code or even worse, reboots the computer, severing all connections. Therefore, the first intention of the adversary is to quickly gain some form of persistence. 

The secondary payload is normally required, as the primary payload must be small, evade anti-virus, and must often fit within the confines of a carrier document or file. However, this secondary payload may be larger in size, may execute entirely in memory, further evading many antivirus technologies. 
#### Command and Control (C2)

Adversaries will then set up some command and control server to direct the activities of the remote access tool or attack framework. This C2 may leverage a more sophisticated scheme of tunneling through common traffic, custom encryption, or communication protocols. 
#### Actions on Objectives

Finally, after all that effort, which may only take seconds to complete, the adversary will perform actions on objectives, which is also a military phrase, complete the task you came to do. Often this involves moving laterally across the organization, discovering sensitive information, gaining enterprise admin privilege, establishing more forms of persistence and access, and ultimately exfiltration of the sensitive data, extortion through ransomware, bitcoin mining, or some other profit motive.
### Courses of Action for the Cyber Kill Chain

There are methods for breaking the chain and dealing with an active attack at every step of the kill chain.
#### Detect

During each phase, you may detect the attacker, but it is often more feasible to detect the attack in its early phases. The further the attacker digs into the network, the more they begin to look like a normal user and the harder it is to detect them. 
#### Deny

An effective method to deal with an attacker is to "deny" them access to sensitive resources. However, that turns out to be harder than it sounds. Again, if an attacker is simply taking an advantage of a discovered vulnerability that, for example, bypasses the built-in access control mechanisms, it may not be possible to deny access to that system, particularly if it is *internet-facing*. 

However, for secondary systems, further network segmentation and access controls should be deployed to deny the attacker. 

On the extreme end of this is **Zero Trust**, which is becoming popular, and if properly deployed, would greatly improve this method. 
#### Disrupt

The act of disrupting the attacker involves *increasing their cost*, either through new forms of antivirus or operating system updates that bring new forms of memory protection, such as:

- **Data Execution Prevention (DEP)**
- **Address Space Layout Randomization (ASLR)**
- **Stack Canaries**.

As the attacker evolves, we as defenders should evolve too. This is particularly important on *external-facing systems*, but we cannot stop there: all systems and internal segments of the network should be *considered vulnerable* and employ methods to disrupt the attacker.
#### Degrade

To degrade an attacker means to limit their ability to be successful. For example, you may throttle outbound data over a certain threshold, to limit exfiltration. 

Further, you may *block all outbound traffic*, except through approved and authenticated proxies, which may buy time to detect those attempts before the attacker figures out what is happening.
#### Deceive

To deceive an enemy is as old as warfare itself. It is a basic element of cyber operations and is most effective for an attacker who has made it past all other defenses but is lurking and poking around the internal network. The hope is that the attacker steps on one of the "digital mouse traps" (honeypots) that have been deployed for detecting that very act.
#### Destroy

Unless you happen to work for a nation-state-level cyber force, you probably won't be able to "hack back". However, you may destroy an attacker's foothold in your own network when it's discovered. 

A word of caution here: you will need to perform careful planning and ensure that you pull the attacker out by the roots; otherwise, you may start a dangerous game of hide-and-seek, angering the attacker, who may be in deeper than you originally thought. 
### MITRE ATT&CK Framework

This framework goes deeper than the Cyber Kill Chain and allows us to get to the underlying tactics, techniques and procedures of the attacker, and thereby have a finer-grained approach to thwarting the attacker at the TTP level. 

The MITRE Framework is "a knowledgebase of attacker behavior." The framework is organized with tactics across the top, which you may notice contain some of the Cyber Kill Chain steps, but many more. 

Techniques are presented under each tactic and have been truncated for brevity in the illustration shown here.

![](https://i.imgur.com/rp8W9YZ.png)

> [!NOTE]
> Although sample procedures are linked to sub-techniques, the ATT&CK framework does not contain a comprehensive list of procedures, nor is it intended to. 

**Procedures** show the variations of the techniques that APTs are known for and are linked to the techniques pages. 
#### Tactics

The MITRE ATT&CK framework contains a mountain of useful information that may be applied across the cybersecurity field. 
#### Cyber Threat Intel

The MITRE framework may be used to *describe attacker behavior in a common language and*
*lexicon*. By it's nature, cyber threat intel has a **short shelf life**, so it is critical to correctly and fully identify the activity (indicators) and then to share (disseminate) that information (intel) in a timely manner, so others may look for those indicators in their own network. 

The framework allows that to happen, on a global scale. Thankfully, the framework has been incorporated into the **Structured Threat Information Expression** (STIX) language and may be distributed on **Trusted Automated Exchange of Intelligence** Information servers. This allows the framework data to be ingested and used by machines, in real time.

| Tactic               | Description                                                                                                                                                                                              |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Reconnaissance       | Similar to the Cyber Kill Chain.                                                                                                                                                                         |
| Resource Development | Involves developing the infrastructure required for the attack, including compromised accounts, development of capabilities, and systems for launching attack.                                           |
| Initial Access       | Similar to delivery phase of the Cyber Kill Chain; describes techniques to gain initial access within a network.                                                                                         |
| Execution            | Similar to exploitation phase of Cyber Kill Chain; describes techniques to get the initial exploit running.                                                                                              |
| Persistence          | Similar to the installation phase of the Cyber Kill Chain; describes techniques to gain and retain persistence on the network.                                                                           |
| Privilege Escalation | Describes the known techniques to be used by attackers to escalate their privileges in a network.                                                                                                        |
| Defense Evasions     | Describes the known techniques used for evasion. This tactic has the deepest list of techniques, as attackers spend a lot of effort evading.                                                             |
| Credential Access    | Describes techniques used to steal account names and passwords.                                                                                                                                          |
| Discovery            | Describes those techniques used by attackers to discover sensitive information and resources within the network. This phase and the next one are particularly vulnerable to detection through deception. |
| Lateral Movement     | Describes techniques used to move across an organization, attacking and gaining access to new systems, often through previously obtained privileged access.                                              |
| Collection           | Describes the techniques used by attackers to collect and stage sensitive information.                                                                                                                   |
| Command and Control  | Similar to the C2 phase of the Cyber Kill Chain, describes those techniques used to communicate between the attacker and the malware.                                                                    |
| Exfiltration         | Techniques used by attackers to remove sensitive information from the network. This may be a few files, but is often gigabytes of information.                                                           |
| Impact               | Similar to Actions on Objectives, describes the techniques used to manipulate, interrupt or destroy systems or data.                                                                                     |
#### Cyber Threat Emulation

Once you know how an adversary acts, you can emulate their TTP and determine if:

1. Your sensors are aligned properly and detecting what they should detect.
2. If your incident monitoring capability is "awake" and if the response procedures are adequate.

For example, if you determine that APT28 is a threat to your organization, due to their interest in your industry, then you may use the procedures identified for that APT and run a controlled exercise to assess your organization's ability to prevent, detect and withstand an attack from that APT. 

One effective tool in this regard is **Red Canary's Atomic Red Team tool**. 

> [!Caution]
> Be sure to coordiante cyber threat exercises with your boss *before* you do them. If you have a SOC, you may want to coordinate with the leader of that organization as well, but it is recommended that the analysts *not* know the exercise is taking place, as their response is part of the test.
#### Threat Hunting

Threat hunting is a new trend in the cybersecurity field. Using the ATT&CK framework, the threat hunter may select a set of APTs in a similar manner to the CTE exercise, but in this case to develop multiple hypotheses of attack. 

Then the threat hunter may fold in cyber threat intelligence, along with situational awareness of the network environment, to prove or disprove their hypotheses. We have long known that the best defenders are attackers (that is, gray hat hackers). Now we have a tool to methodically pursue attackers by using the knowledgebase contained in the framework to systematically hunt them down post-breach.
#### Security Engineering

As a security engineer, you may develop a threat model based on the MITRE ATT&CK Navigator. The Navigator can be used to select a particular set of APTs, which you may download as a spreadsheet. You may then use that spreadsheet to perform a gap assessment, leveraging the results from the CTE exercise and using colors for particular techniques to record your level of coverage in relation to that APT.

That threat model and associated coverage may could be used to design future controls to close those gaps. 
### Summary

This chapter provides you with an overview of the topic of gray hat hacking, which we define as ethical hacking—using offense for defensive purposes. We started with some background and history on the phrase. Then we covered the history of vulnerability disclosure and how that is tied to ethical hacking. Finally, we shifted our focus to the adversary, the black hat hacker, and learned how to discuss, describe, share, and hunt for their activities using the MITRE ATT&CK framework.
### Further Reading

-  CISA Coordinated Vulnerability Disclosure Process (CVD) www.cisa.gov/coordinated-vulnerability-disclosure- process 
- Red Canary Atomic Red Team github.com/redcanaryco/atomic-red-team 
- MITRE ATT&CK Navigator mitre-attack.github.io/attack- navigator/ 
- Threat Hunting with MITRE ATT&CK www.threathunting.se/2020/05/24/threat-detection-with- mitre-attck-and-atomic-redteam/ 
# Chapter 2: Programming Survival Skills

In this chapter, we cover the following topics:

- The C Programming Language
- Computer memory
- Intel processors
- Assembly language basics
- Debugging with `gdb`
- Python survival skills

Why study programming? Ethical hackers should study programming and learn as much about the subject as possible in order to find vulnerabilities in programs and get them fixed before unethical ahckers and black hats take advantage of them. Many security professionals come at programming from a *nontraditional perspective*, often having no programming experience prior to their career. Bug hunting is very much a foot race: if a vulnerability exists, who will find it first?

The purpose of this chapter is to give you the survival skills necessary to understand upcoming chapters and then later to find the holes in software before blackhats do.
## C Programming Language
[[Introduction to C]] | [[Learn C]] 

The C programming language was developed in 1972 by Dennis Ritchie from AT&T Bell Labs. The language was heavily used in ***Unix*** and is therefore ubiquitous. In fact, many of the staple networking programs and operating systems, as well as large applications such as Microsoft Office Suite, Adobe Reader, browsers, are written in combinations of C, C++, Objective-C, assembly and a couple of other low level languages.
### Basic C Language Constructs

Although each C program is unique, some common structures can be found in most programs. We'll discuss these in the next few sections. 
#### `main()`

All C programs "should" contain a `main()` function that follows the format

```
<optional return value type> main(<optional argument>) {
  <optional procedure statements or function calls>;
}
```

where both the return value type and arguments are optional. If no return value type is specified, a return type of `int` is used; however, some compilers may throw warnings if you fail to specify its return value as `int` or attempt to use `void`. If you use command line arguments for `main()`, you could use the format:

```
<optional return value type> main(int argc, char * argv[]) {
```

among others, where the `argc` integer holds the number of arguments (strings). The name of the program is always stored at offset `argv[0]`. The parentheses and brackets are mandatory. The brackets are used to denote the beginning and end of a block of code.

Although *procedure and function calls are optional*, the program would **do nothing without them**. A ***procedure statement*** is simply a series of commands that performs operations on data or variables and normally ends with a semicolon.
### Functions

*Functions* are self-contained bundles of code that can be called for execution by `main()` and other functions. They are **nonpersistent** and can be called as many times as needed, thus preventing us from having to repeat the same code throughout a program.

The format is as follows:

```C
<optional return value type> function name (<optional function argument>) {
}
```

The function name and optional argument list comprise the *signature*. By looking at it, you can tell if the function requires arguments that will be used in processing the procedures of the function. Also notice the optional return value; this tells you if the function returns a value after executing and, if so, what type of data that is. 

The call to the function may look like this:

```C
<optional variable to store the returned value> = function name (arguments if called for by the function signature);
```

The following is a simple example:

```C
#include <stdio.h>
#include <stdlib.h>
int foo() {                                            // 4
	return 8;                                         // 7
}
int main(void) {                                      // 3
	int val_x;                                       // 5
	val_x = foo();                                   // 6
	printf("The value returned is: %d\n", val_x);    // 2, 8
	exit(0);                                         // 1
}
```

Here, we are including the appropriate header files, which include the functions declarations for `exit` and `printf`. The `exit` functions is defined in `stdlib.h`, and `printf` if defined in `stdio.h`.

> If you do not know what header files are required based on the dynamically linked functions you are using in a program, you can simply look at the manual entry, such as `man sscanf`, and refer to the synopsis at the top. We then define the `main` function with a `return` value of `int`.

We specify `void` in the arguments location between the parenthesis because we do not want to allow arguments passed to the `main` function. We then create a variable called `x` with a data type of `int`. Next, we call the function `foo` and assign the return value to `x`. The `foo` function simply returns the value of `8`. This value is then printed onto the screen using the `printf` function, using the format string `%d` to treat `x` as a decimal value..

> Function calls modify the **flow of a program**. When a call to a function is made, the execution of the program temporarily jumps to the function. After execution of the called function has completed, control returns to the calling function at the virtual memory address directly below the call instruction. This process will make more sense during our discussion of stack operations in Chapter 10.
### Variables

***Variables*** are used in programs to *store pieces of information that may change and may be used to *
*dynamically influence the program*. 

When the program is compiled, most variables are pre-allocated memory of a fixed size according to system-specific definitions of size. Sizes in the table below are considered **typical**; there is no guarantee you will get those exact sizes. It is left up to the hardware implementation to define the size. However, the function `sizeof()` is used in C to ensure that the correct sizes are allocated by the compiler. 

Variables are typically defined near the top of a block of code. As the compiler chews up the code and builds a *symbol* table, it must be aware of a variable before that variable is used in the code later. The word "symbol" is simply a name or identifier. This formal declaration of variables is done in the following manner:

```
<variable type> <variable name> <optional initialization starting with "=">;
```

| Variable Type | Use                                                  | Typical Size                                                                             |
| ------------- | ---------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `int`         | Stores a signed integer value such as 314 or -314    | 8 bytes for 64-bit machines<br>4 bytes for 32-bit machines<br>2 bytes of 16-bit machines |
| `float`       | Stores a signed floating point number such as -3.234 | 4 bytes                                                                                  |
| `double`      | Stores a large floating point number                 | 8 bytes                                                                                  |
| `char`        | Stores a single character such as "d"                | 1 byte                                                                                   |
For example, an integer (normally 4 bytes) is declared in memory with a symbol of `a` and an initial value of `0`. 

Once a variable is declared, the assignment construct is used to change the value of the variable. 
	For example, the statement `x=x+1` is an assignment statement that changes the value of the variable `x`. The new value of `x` is the current value of `x` modified by the `+` operator. It is common to use the format `destination = source <with optional operators>` where `destination` is the location in which the final outcome is stored.
### `printf`

The C language comes with many useful constructs bundled into the libc library. One of many commonly used constructs is the `printf` command, generally used to print output to the console.

There are two forms of the `printf` command:

```C
printf(<string>);
printf(<format string>), <list of variables/values);
```

The first format is straightforward and is used to display a simple string to the screen. The second format allows for more flexibility through the use of a format type that can be composed of normal characters and special symbols that act as placeholders for the list of variables following the comma. Commonly used format symbols are listed and described in Table 2-2.

These format types allow the programmer to indicate how they want data displayed to the screen, written to a file, or other possibilities through the use of the `printf` family of functions. As an example, say you know a variable to be a `float` and you want to ensure that it is printed out as such, and you also want to limit it's width, both before and after the floating point. In this case, you could use the code in the following lab in Kali, where we first change our shell to Bash and then get the code from GitHub using `git clone`.

| Format Type | Meaning       | Example                     |
| ----------- | ------------- | --------------------------- |
| `%n`        | Print nothing | `printf("test%n");`         |
| `%d`        | Decimal value | `printf("test%d",123);`     |
| `%s`        | String value  | `printf("test %s","123");`  |
| `%x`        | Hex value     | `printf("test %x", 0x123);` |
| `%f`        | Float         | `printf("test %f", 1.308);` |
## Lab 2-1: Format Strings

Once the repo is cloned from Github, enter that directory and then run `cat fmt_str.c` to open the C file. 

```C
#include <stdio.h>

int main(void) {
  double x = 23.5644;
  printf("The value of x is %5.2f\n", x);
  printf("The value of x is %4.1f\n", x);

  return 0;
}
```

1. In the first `printf` call, we use a total width of `5`, with `2` values after the floating point. 
2. In the second call to `printf`, we use a total width of `4`, with `1` value after the floating point.

Now, let's compile it with `gcc` and run it:

```
jason@nixos~> gcc fmt.str.c -o fmt.str
jason@nixos~> ./fmt.str
The value of x is 23.56
The value of x is 23.6
```
### `scanf`

The `scanf` command complements the `printf` command and is generally used to get input from the user. The format is:

```
scanf(<format string>, <list of variables/values>);
```

where the format string can contain format symbols such as those shown for `printf` in Table 2.2.
	For example, the following code will read an integer from the user and store it in a variable called `number`:

```C
scanf("%d", &number);
```

Actually, the `&` symbol means we are storing the value in the memory location *pointed to* by `number`. This will make more sense when we talk about pointers later in the chapter in the "Pointers" section. For now, realize that you must use the `&` symbol *before* any variable name with `scanf`. The command is smart enough to change types on the fly, so if you were to enter a character in the previous command prompt, the command would convert the character into the decimal (ASCII) value automatically. Bounds checking is not done in regard to string size, which may lead to problems, as discussed later in Chapter 10.
### `strcpy/strncpy`

The `strcpy` command is one of the most **dangerous functions used in C**. The format of the command is as follows:

```
strcpy(<destination>, <source>);
```

The purpose of the command is to copy each character in the source string (a series of characters ending with a null character, `\0`) into the destination string. This is particularly dangerous because *there is no checking of the source's size before it is copied over to the destination*. In reality, we are talking about overwriting memory locations here, which is something that we will explain later in this chapter. Suffice it to say, *when the source is larger than the space allocated for the*
*destination*, overflow conditions are likely present, which could result in the control of program execution. 

When used properly, a safer alternative function is the `strncpy` command. Here is the format of that command.

```
strncpy(<destination>, <source>, <width>)
```

The `<width>` field is used to:

- Ensure that only a *certain number of characters are copied* from the source string to the destination string.
- This allows for greater control by the programmer.

The `width` parameter should be based on the size of the destination, such as an allocated buffer. Another alternative with the ability to control the size and handle errors is `snprintf`. Overall, the C programming language's handling of strings has always been debated and highly scrutinized due to the *requirement of the develop to handle memory allocation*.

> [!caution]
> Using unbounded functions like strcpy is unsafe; however, many traditional programming courses do not cover the dangers posed by these functions in enough detail. In fact, if programmers would simply properly use the safer alternatives, such as snprintf, then the entire class of buffer overflow attacks would be less prevalent. Many programmers clearly continue to use these dangerous functions because buffer overflows are still commonly discovered. Legacy code containing bad functions is another common problem. Luckily, most compilers and operating systems support various exploit-mitigation protections that help to prevent exploitation of these types of vulnerabilities. That said, even bounded functions can suffer from incorrect buffer size calculations.
## Lab 2-2: Loops

Loops are used in programming languages to iterate through a series of command multiple times. The two common types are:

- `for` loops
- `while` loops
### `for` Loops

`for` loops start counting at a beginning value, test the value for some condition, execute the statement, and increment the value for the next iteration. 

The format is as follows:

```
for(<beginning value>; <test value>; <change value>) {
<statement>;
}
```

Therefore, a `for` loop like:

```C
for(i=0; i<10; i++) {
printf("%d", i);
}
```

will print the numbers 0-9 on the same line (since `\n` is not used), like this:

```
0123456789
```

With `for` loops, the condition is checked *prior to the iteration of the statements in the loop*, so it is possible that even the first iteration will not be executed. When the condition is not met, the flow of the program continues after the loop. 

> [!NOTE] 
> It is important to note the use of the less-than operator (`<`) in place of the less-than-or-equal-to operator (`<=`), which allows the loop to proceed one more time until `i = 10`. This is an important concept that can lead to **off-by-one** errors. Also, note that the count is started with 0. This is common in C and worth getting used to.
### `while` Loops

The `while` loop is used to iterate through a series of statements **until** a condition is met. A basic example is as follows:

```C
#include <stdio.h>

int main(void){
  int x = 0;

  while (x<10) {
    printf("x = %d\n", x);
    x++;
  }
  return 0;
}
```

```
~/Dev/C/GHHv6/ch02 on  main [?] via C v13.3.0-gcc via 🐍 v3.12.7 via ❄  impure (nix-shell-env) ❯  gcc while_ex.c -o while_ex
~/Dev/C/GHHv6/ch02 on  main [?] via C v13.3.0-gcc via 🐍 v3.12.7 via ❄  impure (nix-shell-env) ❯  ./while_ex            nix-shell-env
x = 0
x = 1
x = 2
x = 3
x = 4
x = 5
x = 6
x = 7
x = 8
x = 9
```

Loops may also be nested within each other. 
## Lab 2-3: `if/else`

The `if/else` construct is used to *execute a series of statements if a certain condition is met*; otherwise, the optional `else` block will be executed. If there is no `else` block of statements, the flow of the program will continue after the end of the closing `if` block bracket (`}`).

The following is an example of an `if/else` construct nested within a `for` loop:

```C
#include <stdio.h>

int main(void){
  int x = 0;
  while(1){                         // 1
    if (x == 0) {                   // 2
	  printf("x = %d\n", x);
	  x++;
	  continue;
	}
	else {                          // 3
	  printf("x != 0\n");
	  break;                        // 4
	}
	return 0;
  }
}
```

```
~/Dev/C/GHHv6/ch02 on  main [?] via C v13.3.0-gcc via 🐍 v3.12.7 via ❄  impure (nix-shell-env) ❯  gcc ifelse.c -o ifelsenix-shell-env
~/Dev/C/GHHv6/ch02 on  main [?] via C v13.3.0-gcc via 🐍 v3.12.7 via ❄  impure (nix-shell-env) ❯  ./ifelse              nix-shell-env

x = 0
x != 0
```

In this example:

1. We use a `while` loop to loop through the `if/else` statements. 
2. Before we go into the loop, we set the variable `x` to `0`. Because `x` is equal to 0, we meet the condition in the `if` statement.
3. Then we call the `printf` function, increment `x` by `1`, and then `continue`. Since `x` is now 1, we don't meet the condition for the if statement during the second iteration through the loop. Therefore, we move on to the `else` statement.
4. The `else` statement calls the `printf` function and then breaks out of the the loop.

The braces may be omitted for single statements.
### Comments

To assist in the readability and sharing of our code, programmers include comments in the code. You can use one of two ways to place comments in code: `//` or `/*` and `*/`.

The `//` comment type indicates that any characters on the rest of that line are to be treated as comments and not acted on by the computer when the program executes. 

The `/*` and `*/` pair starts and stops a block of comments that may span multiple lines. In this case, `/*` is used to start the comment, and `*/` is used to indicate the end of the comment.
## Lab 2-4: `hello.c`

We will start by showing the program with `//` comments included and will follow up with a discussion of the program.

```C
~$ cat hello.c                
hello.c                         / / customary comment of program name
#include <stdio.h>
int main(){
	printf("Hello haxor!\n")
}
```

This simple program prints "Hello Haxor!" to the screen using the `printf` function, included in the stdio.h library. 
## Lab 2-5: `meet.c`

Now for something a little more complex. This program will take input, store it, then print it:

```C
~$ cat meet.c
// meet.c
#include <stdio.h>                             // needed for screen printing
#include <string.h>                            // needed for strcpy

void greeting(char *temp1,char *temp2){        // greeting function to say hello
	char name[400];                           // string variable to hold name
	strcpy(name, temp2);                      // copy argument to name
	printf("Hello %s %s\n", temp1, name);     // print out the greeting
}
int main(int argc, char * argv[]){             // note the format for arguments
	greeting(argv[1], argv[2]);               // call function, pass title & name
	printf("Bye %s %s\n", argv[1], argv[2])   // say bye
}                                              // exit program
```

1. This program takes two command line arguments.
2. Calls the greeting function
3. The greeting function prints "Hello" and the name given, followed by a carriage return
4. When the `greeting()` function finishes, control is returned to `main()`, which prints out "Bye" and the name given.
5. Finally, the program exits.
### Compiling with `gcc`

***Compiling*** is the process of turning *human readable source code into machine-readable binary files* that can be digested by the computer and executed. More specifically, a compiler takes source code and translates it into an immediate set of files called *object code*. These files are nearly ready to execute by may contain unresolved references to symbols and functions not included in the original source code file. 

The symbols and references are resolved through a process called ***linking***, as each object file is **linked together into an executable binary file**. We have simplified the process for you here, but these are the main steps. 

When programming with C on UNIX systems, most programmers prefer to use the **GNU C Compiler** (`gcc`). `gcc` offers plenty of options when compiling. The most commonly used flags are listed and described in the table below:

| Option                         | Description                                                                                                                                           |
| ------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-o <filename>`                | Saves the compiled binary with this name. The default is to save to output as `a.out`.                                                                |
| `-S`                           | Produces a file containing assembly instructions; saved with an `.s` extension.                                                                       |
| `-ggdb`                        | Produces extra debugging information; useful when using the GNU debugger (`gdb`)                                                                      |
| `-c`                           | Compiles without linking; produces object files with an `.o` extension.                                                                               |
| `-mpreferred-stack-boundary=2` | Compiles the program using a DWORD size stack, simplifying the debugging process while you learn.                                                     |
| `-fno-stack-protector`         | Disables the stack protection; introduced with GCC 4.1. This option is useful when you're learning about buffer overflows, as you will in Chapter 11. |
| `-z execstack`                 | Enables and executable stack. This option is useful when you're learning about buffer overflows, as you will in Chapter 11.                           |
## Lab 2-6: Compiling `meet.c`

```
(kali@kali) - [~/GHHv6/ch02]
~$ gcc -o meet meet.c
```

To execute, you type:

```
(kali@kali) - [~/GHHv6/ch02]
~$ ./meet Leet Haxor
Hello 1337 Haxor
Bye 1337 Haxor
```

You will use various compiler options to compile programs in this book and beyond; see the "For Further Reading" for more info on using `gcc`.
### Computer Memory

In the simplest terms, ***computer memory*** is an electronic mechanism that has the ability to **store and retrieve data**. The smallest amount of data that can be stored is `1 bit`, which can be represented by either a 1 or 0 in memory. 

When you put 4 bits together, it is called a *nibble*, which can represent values from `0000` to `-1111`. There are exactly 16 binary values, ranging from 0 to 15, in decimal format. 

When you put two nibbles, or 8 bits, together, you get a **byte**, which can represent values from 0 to $(2^8 -1)$, or 0 to get 255 in decimal. 

When you put two bytes together, you get a **word**, which can represent values from 0 to $(2^16 -1)$, or 0 to 65,535 in decimal. 

Continuing to piece data together, if you put **two words** together, you get a **double word**, or **DWORD**, which can represent values from 0 to $(2^32 - 1)$, or 0 to 4,294,967,295 in decimal. Two DWORDs together is a **quadruple word**, which can represent values from $(2^64 - 1)$, or 0 to 18,446,744,073,709,551,615 in decimal.

In terms of memory addressing on 64-bit AMD and Intel processors, only the lower 48 bits are used, which offers 256 Terabytes of addressable memory. This is well documented in countless online resources.

There are many types of computer memory; we will focus on **random access memory**, and **registers**. Registers are special forms of memory *embedded within processors*, which will be discussed later in this chapter in the "Registers" section.
### Random Access Memory

In RAM, any piece of stored data can be retrieved at any time, thus, the term *random access*. However, RAM is *volatile*, meaning that when the computer is turned off, all data is lost from RAM. When we're discussing modern Intel and AMD-based products (x86 and x64), the memory is 32-bit or 48-bit addressable, respectively, meaning that the address bus the processor uses to select a particular memory address is 32 or 48 bits wide. Therefore, the most memory that can be addressed in an x86 processor is 4,294,967,295 bytes or 281,474,976,710,655 bytes (256 Terabytes). On an x64 64-bit processor, addressing can be expanded in the future by adding more transistors, but $2^48$ is plenty for current systems.
### Endian

In Internet Experiment Note (IEN) 137, "On Holy Wars and a Plea for Peace" from 1980, Danny Cohen summarized Swift's *Gulliver's Travels*, in part, as follows in his discussion of byte order:
	Gulliver finds out that there is a law, proclaimed by the grandfather of the present ruler, requiring all citizens of Lilliput to break their eggs only at the little ends. Of course, all those citizens who broke their eggs at the big ends were angered by the proclamation. Civil war broke out between the Little-Endians and Big-Endians, resulting in the Big-Endians taking refuge on a nearby island, the kingdom of Blefuscu.

The point of Cohen's paper was to describe the two schools of thought when writing data into memory. Some feel that the "low orders" bytes should be written first (called Little Endians by Cohen), whereas others think that the high-order bytes should be written first (Big Endians).

The difference really depends on the hardware you are using. For example, Intel-based processors use the little-endian method, whereas Motorola-based processors use big-endian.
### Segmentation of Memory

The subject of segmentation could easily consume a chapter itself. However, the basic concept is simple.

Each process (oversimplified as an executing program) needs to have access to it's **own areas** in memory. After all, you would not want one process overwriting another process's data. Therefore, memory is broken down into small segments and handed out to processes as needed. 

**Registers**, discussed later in the chapter, are *used to store and keep track of the current segments a*
*process maintains*.  Offset registers are used to keep track of where in the segment the critical pieces of data are kept. Segmentation also describes the memory layout within a process's virtual address space. Segments such as the code segment, data segment, and stack segment are intentionally allocated in different regions of the virtual address space within a process to prevent collisions and allow for the ability to set permissions accordingly. Each running process gets its own virtual address space, and the amount of space depends on the **architecture** (32-bit vs 64-bit), system settings, and the OS. A basic 32-bit Windows process by default gets 4GB, where 2GB is assigned to the **kernel-mode** side of the process. Only a small portion of this virtual space within each process is mapped to physical memory, and depending on the architecture, there are various ways of performing virtual-to-physical memory mapping through the use of paging and address translation.
### Programs in Memory

When process are loaded into memory, they are basically *broken into many small sections*. We are only concerned with six main sections, which we discuss in the following subsections.
#### `.text` Section

The `.text` section, also known as the ***code segment***, basically corresponds to the `.text` portion of the binary executable file. It contains the machine instructions to get the task done. This section is marked as readable and executable and will cause an access violation if a write attempt is made. The size is fixed at runtime when the process is first loaded. 
#### `.data` Section

The `.data` section is used to store global initialized variables, such as:

```C
int a = 0;
```

The size of this section is fixed at run time. It should only be marked as readable.
#### `.bss` Section

The *below stack section (.bss)* is used to store certain types of global uninitialized variables, such as:

```C
int a;
```

The size of this section is fixed at runtime. This segment needs to be readable and writable but should not be executable.
#### Heap Section

The *heap* section is used to store dynamically allocated variables and grows from the lower-addressed memory to the higher-addressed memory. The allocation of memory is controlled through the `malloc()`, `realloc()` and `free()` functions.
	For example, to declare an integer and have the memory allocated at runtime, you would use something like this:

```C
int = malloc (sizeof (int)); // dynamically allocated an integer, contains the
                        // preexisting value of that memory
```

The heap section **should be readable and writable** but should **not be executable** because an attacker who gains control of a process could easily perform ***shellcode execution*** in regions such as the stack and heap.
#### Stack Sectionn

The *stack* section is used to keep track of **function calls** (recursively) and grows from the higher-addressed memory to the lower-addressed memory on most systems. If the process is multi-threaded, each thread will have a unique stack. As you will see, the fact that the stack grows from high memory toward low memory allows the subject of buffer overflows to exist. Local variables exist in the stack section. The stack segment if further explained in Chapter 10.
#### Environment/Arguments Section

The *environments/arguments* section is used to store a copy of system-level variables that may be required by the process during runtime. 
	For example, among other things, the path, shell name, and hostname are made available to the running process. This section is writable, allowing it's use in format string and buffer overflow exploits. Additionally, the command-line arguments are stored in this area. The sections of memory reside in the order presented. The memory space of a process looks like this:

![](https://i.imgur.com/Oo82JVY.png)
#### Buffers

The term *buffer* refers to a storage place used to receive and hold data until it can be handled by a process.

Since each process might have it's own set of buffers, it is critical to **keep them straight**; this is done by **allocating the memory within the `.data` or `.bss` section** of the process's memory.

Remember, once allocated, the buffer is of **fixed length**. The buffer may hold any predefined type of data; however, for our purpose, we will focus on *string-based buffers*, which are used to store **user input and text-based variables**.
#### Strings In Memory

Simply put, *strings* are just continuous arrays of character data in memory. The string is referenced in memory by the address of the first character. The string is terminated or ended by a null character (`\0` in C). The `\0` is an example of an **escape sequence**.

**Escape Sequences** enable the developer to specify a *special operation*, such as a newline with `\n` or a carriage return with `\r`. The backslash ensures that the subsequent character is not treated as part of the string. If a backslash is needed, one can simply use the escape sequence `\\`, which will show only a single `\`. Tables of various escape sequences can be found online.
#### Pointers

**Pointers** are *special pieces of memory* that hold the **address of other pieces of memory**. Moving data around inside of memory is a relatively slow operation. It turns out that instead of moving data, keeping track of the location of items in memory through pointers and simply changing the pointers is much easier. 

Pointers are saved in `4` or `8` bytes of *contiguous memory*, depending on whether the application is 32-bit or 64-bit. 
	For example, as mentioned, strings are referenced by the address of the first character in the array. That address value is called a *pointer*. The variable declaration of a string in C is written as follows:

```C
char * str; // This is read. Give me 4 or 8 bytes called str which is a 
          // pointer to a Character variable (the first byte of the array).
```

Note that even though the size of the pointer is set at 4 or 8 bytes, depending on the architecture, the size of the string has not been set with the preceding command; therefore, this data is considered uninitialized and will be placed in the `.bss` section of the process memory.

Here is another example; if you wanted to store a pointer to an integer in memory, you would issue the following command in your C program:

```C
int * point1; // this is read, give me 4 or 8 bytes called point1, which is a
		    // pointer to an integer variable
```

To read the value of the memory address pointed to by the pointer, you dereference the pointer with with `*` symbol. Therefore, if you want to print the value of the integer pointed to by `point1` in the preceding code, you would use the command:

```C
printf("%d", *point1);
```

where `*` is used to dereference the pointer called `point1` and display the value of the integer using the `printf()` function.
## Lab 2.7: `memory.c`

