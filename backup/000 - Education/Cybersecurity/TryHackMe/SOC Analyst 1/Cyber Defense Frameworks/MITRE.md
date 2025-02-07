> **MITRE** researches in many areas, outside of cybersecurity for the *safety, stability and well-being of our nation.*

- These areas include threat intelligence, artificial intelligence, health informatics, and space security.

From [**Mitre.org**](https://www.mitre.org/about/corporate-overview): "_At MITRE, we solve problems for a safer world. Through our federally funded R&D centers and public-private partnerships, we work across government to tackle challenges to the safety, stability, and well-being of our nation._"

In this room, we will focus on other projects/research that the US-based non-profit MITRE corporation has created for the cybersecurity community, specifically:

- ATT&CK (Adversarial Techniques, Tactics and Common Knowledge)
- CAR (Cyber Analytics Repository)
- ENGAGE
- D3FEND (Detection, Denial and Disruption Framework Empowering Network Defense)
- AEP (ATT&CK Emulation Plans)

# Basic Terminology

**APT** is an acronym for **Advanced Persistent Threat**. 

- This can be considered a team/group (*threat group*) or even a country (*nation-state group*), that engages in long term attacks against organizations and/or countries.
- The term "advanced" can be misleading as it will tend to cause us to believe that each APT group all have some super-weapon, i.e. a zero-day exploit, that they will use.
- The techniques APT groups use are often quite common and can be detected with the right implementations in place.

**TTP** is an acronym for **Tactics, Techniques and Procedures**

- The *tactic* is the adversary's goal or objective
- The *technique* is how the adversary achieves it's goal or objective
- The *procedure* is how the technique is used.

# ATT&CK Framework

> What is the ATT&CK framework?
> 
> According to the [website](https://attack.mitre.org/), "MITRE ATT&CK® is a globally-accessible knowledge base of adversary tactics and techniques based on real-world observations."

In 2013, MITRE began to address the need to record and document common TTPs (Tactics, Techniques, and Procedures) that APT (Advanced Persistent Threat) groups used against enterprise Windows networks. This started with an internal project known as FMX (Fort Meade Experiment)

- Within this project, selected security professionals were tasked to emulate adversarial TTPs against a network, and data was collected from the attacks on this network.
- The gathered data helped construct the beginning pieces of what we know today as the ATT&CK framework.

> The ATT&CK framework has grown and expanded over the years.
> 
> One notable extension was that the framework focused solely on the Windows platform but has expanded to cover other platforms, such as macOS and Linux.

The framework is heavily contributed to by many sources, such as security researchers and threat intelligence reports. 

*ATT&CK* is not only a blue team tool, it is also a tool for red teamers.
# CAR Knowledge Base

> The official definition of CAR is "_The MITRE Cyber Analytics Repository (CAR) is a knowledge base of analytics developed by MITRE based on the MITRE ATT&CK_® _adversary model. CAR defines a data model that is leveraged in its pseudocode representations but also includes implementations directly targeted at specific tools (e.g., Splunk, EQL) in its analytics. With respect to coverage, CAR is focused on providing a set of validated and well-explained analytics, in particular with regards to their operating theory and rationale._"

Let's begin our journey by reviewing [CAR-2020-09-001: Scheduled Task - File Access](https://car.mitre.org/analytics/CAR-2020-09-001/).

-  We're provided with psuedocode here and a query on how to search for this specific analysis within Splunk. 
- A **psuedocode** is a plain, human-readable way to describe a set of instructions or algorithms that a program or system will perform.

To take full advantage of CAR, we can view the [Full Analytic List](https://car.mitre.org/analytics) or the [CAR ATT&CK® Navigator layer](https://mitre-attack.github.io/attack-navigator/#layerURL=https://raw.githubusercontent.com/mitre-attack/car/master/docs/coverage/car_analytic_coverage_04_05_2022.json) to view all the analytics.

Let's look at another analytic to see a different implementation, [CAR-2014-11-004: Remote PowerShell Sessions](https://car.mitre.org/analytics/CAR-2014-11-004/).

Under Implementations, a pseudocode is provided and an EQL version of the pseudocode. EQL (pronounced as 'equal'), and it's an acronym for Event Query Language. EQL can be utilized to query, parse, and organize Sysmon event data. You can read more about this [here](https://eql.readthedocs.io/en/latest/).

> To summarize, CAR is a great place for finding analytics that takes us further than the Mitigation and Detection summaries in the ATT&CK® framework. 
> 	This tool is not a replacement for ATT&CK® but an added resource.

# MITRE Engage

> Per the website, "_MITRE Engage is a framework for planning and discussing adversary engagement operations that empowers you to engage your adversaries and achieve your cybersecurity goals._"

MITRE Engage is considered an **Adversary Engagement Approach**. This is accomplished by the implementation of **Cyber Denial** and **Cyber Deception**.

The Engage website provides a [starter kit](https://engage.mitre.org/starter-kit/) to get you 'started' with the Adversary Engagement Approach. The starter kit is a collection of whitepapers and PDFs explaining various checklists, methodologies, and processes to get you started.

Let's look at each of these categories based on the information on the Engage website.

- **Prepare** the set of operational actions that will lead to your desired outcome
- **Expose** adversaries when they trigger your deployed deception activities
- **Affect** adversaries by performing actions that will have a negative impact on their operations
- **Elicit** information by observing the adversary and learn more about their modus operandi (TTPs)
- **Understand** the outcomes of the operational actions

Refer to the [Engage Handbook](https://engage.mitre.org/wp-content/uploads/2022/04/EngageHandbook-v1.0.pdf) to learn more. 

You can interact with the [Engage Matrix Explorer](https://engage.mitre.org/matrix). We can filter by information from [MITRE ATT&CK](https://attack.mitre.org/). 

Note that by default the matrix focuses on Operate, which entails Expose, Affect, and Elicit.
# MITRE D3FEND

> What is this MITRE resource? Per the [D3FEND](https://d3fend.mitre.org/) website, this resource is "_A knowledge graph of cybersecurity countermeasures._"

- D3FEND is still in beta and is funded by the Cybersecurity Directorate of the NSA.

D3FEND stands for ***Detection, Denial, and Disruption Framework Empowering Network Defense.***

Let's take a look at one of the D3FEND's artifacts, such as **Decoy File**.

> As you can see, you're provided with information on what is the technique (**definition**), how the technique works (**how it works**), things to consider during implementation (**considerations**), and how to utilize the utility (**example**).

Note, as with other MITRE resources, you can filter based on the ATT&CK matrix. 

Since this resource is in beta and will change significantly in future releases, we won't spend that much time on D3FEND. 

The objective of this task is to make you aware of this MITRE resource and hopefully you'll keep an eye on it as it matures in the future. 

We will still encourage you to navigate the website a bit by answering the questions below.

# ATT&CK Emulation Plans

> If these tools provided to us by MITRE are not enough, under [MITRE ENGENUITY](https://mitre-engenuity.org/), we have CTID, the Adversary Emulation Library, and ATT&CK® Emulation Plans.

MITRE formed an organization named the **Center of Threat-Informed Defense** (CTID). This organization consists of various companies and vendors from around the globe. 

- Their objective is to conduct research on cyber-threats and their TTPs and share this research to improve cyber defense for all.

Some of the companies and vendors who are participants of CTID:

- *AttackIQ (founder)*
- *Verizon*
- *Microsoft (founder)*
- *Red Canary (founder)*
- *Splunk*

> Per the website, "_Together with Participant organizations, we cultivate solutions for a safer world and advance threat-informed defense with open-source software, methodologies, and frameworks. By expanding upon the MITRE ATT&CK knowledge base, our work expands the global understanding of cyber adversaries and their tradecraft with the public release of data sets critical to better understanding adversarial behavior and their movements._"

### Adversary Emulation Library & ATT&CK Emulation Plans

> The [Adversary Emulation Library](https://medium.com/mitre-engenuity/introducing-the-all-new-adversary-emulation-plan-library-234b1d543f6b) is a public library making adversary emulation plans a free resource for blue/red teamers. 
> 
> 	The library and the emulations are a contribution from CTID. There are several [ATT&CK® Emulation Plans](https://github.com/center-for-threat-informed-defense/adversary_emulation_library) currently available: [APT3](https://attack.mitre.org/resources/adversary-emulation-plans/), [APT29](https://github.com/center-for-threat-informed-defense/adversary_emulation_library/tree/master/apt29), and [FIN6](https://github.com/center-for-threat-informed-defense/adversary_emulation_library/tree/master/fin6). 
> 	The emulation plans are a step-by-step guide on how to mimic the specific threat group. If any of the C-Suite were to ask, "how would we fare if APT29 hits us?" This can easily be answered by referring to the results of the execution of the emulation plan.

# ATT&CK and Threat Intelligence

> **Threat Intelligence** or **Cyber Threat Intelligence** is the information, or TTPs, attributed to the adversary. 
> 
> 	By using threat intelligence, as defenders, we can make better decisions regarding the defensive strategy.

Large corporations might have an in-house team whose primary objective is to gather threat intelligence for other teams in the organization, aside from using threat intel already readily available.

- Some of this threat intel can be from open source or through a subscription with a vendor, such as CrowdStrike.
- In contrast, many defenders wear multiple hats (roles) within an organization, and they need to take time from their other tasks to focus on threat intelligence. 
- To cater to the latter, we'll work a scenario of using ATT&CK for threat intelligence. 

**Scenario**: You are a security analyst who works in the aviation sector. Your organization is moving their infrastructure to the cloud. Your goal is to use the ATT&CK® Matrix to gather threat intelligence on APT groups who might target this particular sector and use techniques targeting your areas of concern. You are checking to see if there are any gaps in coverage. After selecting a group, look over the selected group's information and their tactics, techniques, etc.

# Conclusion

> ***The more information we have as defenders, the better we are equipped to fight back.***

If we're seeking to transition into a role as a SOC Analyst, detection engineer, cyber threat analyst, etc. these tools are a *must know*.

As mentioned before, these tools are not only for blue teamers.

Red teamers, these tools/resources are useful as well.

- Your objective is to mimic the adversary and attempt to bypass all the controls in place within the environment. 
- With these resources, as the red teamer, you can effectively mimic a true adversary and communicate your findings in a common language that both sides can understand.

In a nutshell, this is known as **purple teaming**.

