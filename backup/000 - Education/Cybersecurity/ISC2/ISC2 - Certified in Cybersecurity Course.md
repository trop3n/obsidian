# Domain 1: Security Principles

**Privacy**

> Privacy is the right of an individual to control the distribution of information about themselves.
-  While security and privacy both focus on the protection of personal and sensitive data, there is a difference between them.
-  With the increasing rate at which data is collected and digitally stored across all industries, the push for privacy legislation and compliance with existing policies steadily grows.


> Global privacy is an especially crucial issue when considering requirements regarding the collection and security of personal information. 

> There are several laws that define privacy and data protection, which periodically change. 

#### General Data Protection Regulation

> Applies to all organizations, foreign or domestic, doing business in the EU or any persons in the EU. 

#### Risk Management Terminology

> Security professionals use their knowledge and skills to examine operational risk management, determine how to use risk data effectively, work cross functionally, and report actionable information findings to the stakeholders concerned. 

**An Asset**:
-  Something in need of protection

**A Vulnerability**:
-  A gap or weakness in those protection efforts

**A Threat**:
-  something or someone that aims to exploit a vulnerability to thwart protection efforts

#### Decision Making Based on Risk Properties

> When making decisions based on risk priorities, organizations must evaluate the likelihood and impact of the risk as well as their tolerance for different sorts of risk. 

#### Code of Ethics

> States that information security professionals must act honorably, honestly, justly, responsibly and legally.

Using privilege or status to behave in a way that is unbecoming of a security professional can have severe career consequences. 
-  It also opens up your organization to legal consequences in certain contexts

#### Authentication

**Confidentiality**
> When users have stated their identity, it is necessary to validate that they are the rightful owners of that identity. 

> This process of verifying or proving the user's identification in known as **authentication.**
> Simply put, authentication is a process to prove the identity of the requestor.

There are some common methods of authentication:

- **Something you know:** Passwords or passphrases
- **Something you have:** Tokens, memory cards, smart cards
- **Something you are:** Biometrics, measurable characteristics

#### Professional Code of Conduct

> Every ISC2 member is required to commit to fully support the ISC2 Code of Ethics

**ISC2 Code of Ethics Canons**
> The Canons represent the important beliefs held in common by the members of ISC2. Cybersecurity professionals who are members of ISC2 have a duty to the following four entities in the Canons:

- Protect society, the common good, necessary public trust and confidence, and the infrastructure.
- Act honorably, honestly, justly, responsibly, and legally.
- Provide diligent and competent service to principles
- Advance and protect the profession

#### Governance Elements

> Any business or organization exists to fulfill a purpose, whether it is to provide raw materials to an industry, manufacture equipment to build computer hardware, develop software applications, construct buildings, or provide goods and services.
> To complete the objective requires that decisions are made, rules and practices are defined, and policies and procedures are in place to guide the organization in its pursuit of achieving it's goals and mission.

When leaders and management implement the systems and structures that the organization will use to acheive it's goals, they are guided by laws and regulations created by governments to enact public policy. *Laws and regulations guide the development of standards, which cultivate policies, which result in procedures*

- *Procedures* are the detailed steps to complete a task that support departmental or organizational activities.
- *Policies* are put in place by organizational governance, such as executive management, to provide guidance in all activities to ensure that the organization supports industry standards and regulations.
- *Standards* are often used by governance teams to provide a framework to introduce policies and procedures in support of regulations.
- *Regulations* are commonly issued in the form of laws, usually from government and typically carry financial penalties for non-compliance

##### **Regulations and Laws**

> Regulations and associated fines and penalties can be imposed by governments at the national, regional or local level. 

Because regulations and laws can be imposed and enforced differently in different parts of the world, here are a few examples to connect to concepts to actual regulations:

- **Health Insurance Portability and Accountability Act**: 1996 law that governs the use of protected health information (PHI) in the United States
	- Violation of HIPAA carries the possibility of fines for both individuals and companies
- **General Data Protection Regulation**: EU regulation to control the use of Personally Identifiable Information (PII) of its citizens and those in the EU.
	- Includes provisions that apply financial penalties to companies who handle the data of EU citizens and those living in the EU even if the company does not have a physical presence in the EU. 

Organizations need to consider the regulations that apply to their business at all levels, national, regional and local, and ensure they are in compliance with the most restrictive regulation

##### **Standards**

> Organizations use multiple standards as part of their information systems security programs, both as compliance documents and as advisories or guidelines.

Standards cover a broad range of issues and ideas and may provide assurance that an organization is operating with policies and procedures that support regulations and widely accepted best practices. 

**International Organization for Standardization (ISO)**

> Develops and publishes international standards on a variety of technical subjects, including information systems and information security, as well as encryption standards.

ISO solicits input from the international community of experts to provide input on its standards prior to publishing.

**National Institute of Standards and Technology**

> Unites States government agency under the department of commerce and publishes a variety of technical standards in addition to information technology and information security standards.

Many of these standards are mandatory for US government agencies and are considered recommended standards by industries worldwide. 

NIST standards solicit and integrate input from the industry and are free to download from the NIST website.

**Internet Engineering Task Force (IETF)**

> Creators of standards in communications protocols that ensure all computers can connect with each other across borders, even when the operators do not speak the same language.

**Institute of Electrical and Electronics Engineers (IEEE)**

> Set standards for telecommunications, computer engineering and similar disciplines.

##### **Policies**

> Policy is informed by applicable laws and specifies which standards and guidelines the organization will follow. 
> Policy is broad but not detailed, it establishes context and sets out strategic direction and priorities. 

Governance policies are used to moderate and control decision-making, to ensure compliance when necessary, and to guide the creation and implementation of other policies.

Policies are implemented, or carried out, by people; for that, someone must expand the policies from statements of intent and direction into step-by-step instructions or procedures.

##### **Procedures**

> Procedures define the explicit, repeatable activities necessary to accomplish a specific task or set of tasks.
> They provide supporting data, decision criteria, or other explicit knowledge needed to perform each task. 
> Procedures can address one-time or infrequent actions or common, regular occurrences.

In addition, procedures establish the measurement criteria and methods to use to determine whether a task has been successfully completed. Properly documenting procedures and training personnel on how to locate and follow them is necessary for deriving the maximum organizational benefits from procedures.

#### Non-Repudiation

> The ability to deny taking an action such as creating information, approving information, or sending or receiving a message.

Non-repudiation is a legal term defined as the protection against an individual falsely denying having performed a particular action. 
- It provides the capability to determine whether a given individual took a particular action, such as created information, approved information or sent or received a message.

In today's world of e-commerce and electronic transactions, there are opportunities for impersonation of others or denial of an action (e.g. making a purchase online and later denying it)

It is important that all participants trust online transactions.
- Non-repudiation methodologies ensure that people are held responsible for transactions they conducted. 

***Non-repudiation methodologies ensure that people are held responsible for transactions they conducted.***

#### CIA In the Real World

> Security professionals are tasked with security the information of large corporations or multiple individuals.

**Confidentiality** means that no information has been improperly disclosed to unauthorized individuals.
- Ensuring that PII is protected.
- Goal is protect the information from unauthorized access.

**Integrity** ensures that the information is not being corrupted or changed without the data owner's permission.
- It confirms that the information being maintained is complete and accurate and consistent with the legitimate use of that information
- Interfering with the integrity of information can have serious consequences

**Availability** is crucial because it verifies that people have access to the information in a timely manner.
- Cyberattacks that target availability are trying to prevent access to information, like DDoS or Ransomware

#### Methods of Authentication

> There are two types of authentication:
> 	Using only one method of authentication is known as **single factor authentication**
> 	Granting users access after successfully demonstrating or displaying two or more of these methods is known as **multi-factor authentication**

**Single Factor Authentication**
> Use of just one of the three available factors (something you know, something you are, something you have) to carry out an authentication request

**Multi-Factor Authentication**
> Use of two or more distinct instances of the three factors of authentication for identity verification

Common best practice is to implement at least two of the three common techniques for authentication:
- Knowledge-based
- Token-based
- Characteristic-based

**Knowledge based Authentication** uses a passphrase or password to differentiate between an authorized and unauthorized user. 
- If you have selected a personal identification number (PIN), created a password, or entered some other secret value that only you know, then you have experienced knowledge based authentication

The problem with knowledge based authentication alone is that it is often vulnerable to a variety of attacks.
-  Calls to reset user passwords
- The challenge is ensuring that the request is only being made by the correct user and not someone impersonating the user.

#### Risk Priorities

> When risks have been identified, it is time to prioritize and analyze core risks through **qualitative risk analysis** and/or **quantitative risk analysis**

This is necessary to determine the root cause and narrow down apparent risks and core risks.

Understanding the organization's overall mission and the functions that support the mission helps to place risks in context, determine the root causes, and prioritize the assessment and analysis of these items. 

- In most cases, management will provide direction for using the findings of the risk assessment to determine a prioritized set of risk-response actions.

One effective method to prioritize risk is to use a risk matrix, which helps identify priority as the intersection of likelihood of occurrence and impact.

- It also gives the team a common language to use with management when determining the final priorities. For example, a low likelihood and low impact might result in a low priority, while an incident with a high likelihood and high impact will result in a high-priority. Assignment of priority may relate to business priorities, the cost of mitigating risk, or the potential for loss if an incident occurs.

#### Risk Treatment

**Risk Treatment** involves making decisions about the best actions to take regarding the identified and prioritized risk.
	- The decisions are dependent on the attitude of management toward risk and the availability--and cost-- of risk mitigation.

**Common Risk Treatment Options Are:**

> **Risk Avoidance** is the attempt to eliminate the risk entirely. 
> 	This could include ceasing operation for some or all of the activities of the organization that leave it exposed to a particular risk. 
> 	Leadership may choose risk avoidance if the potential impact of a given risk is too high or the likelihood of the risk being realized is simply to great.

> **Risk Acceptance** is taking no action to reduce the likelihood of a risk occurring. Management may opt to conduct the business function associated with the risk without any further action on the part of the organization, either because the impact or likelihood of the occurrence is negligible or because the benefit is more than enough to offset that risk. 

> **Risk Mitigation** is the most common type of risk management and includes taking actions to prevent or reduce the possibility of a risk event or its impact. 
> 	Mitigation can involve remediation measures such as security controls, policies, procedures and standards to minimize adverse risk. 
> 	Risk cannot always be mitigated, but mitigations such as safety measures should always be in place.

> **Risk Transfer** is the practice of passing the risk to another party who will accept the financial impact of the harm resulting from a risk being realized in exchange for payment. 
> 	This is typically an insurance policy.

#### Risk Tolerance

> The perception management takes toward risk is often likened to the entity's appetite for risk. 
> How much risk are they willing to take? Does management welcome risk or want to avoid it?

Different departments may have different attitudes towards acceptable and unacceptable risk.
	- Understanding an organization and senior management's attitude toward risk is usually the starting point for getting management to take action regarding risks.

> Executive management and/or the Board of Directors determines what is an acceptable level of risk for the organization. Security professionals aim to maintain the levels or risk within management's limit of risk tolerance.

***A company with an even lower tolerance for downtime will invest in multiple generators with multiple fuel sources to provide a higher level assurance that the power will not fail.***

#### Risk Assessment

> **The analysis performed as part of risk management.**
> A risk assessment incorporates threat and vulnerability analyses and considers mitigations provided by security controls planned or in place.

**Risk Assessment is defined as the process of identifying, estimating and prioritizing risks to an organization's operations, assets, individuals, other organizations and even teh nation.**
	- Risk assessment should result in aligning (or associating) each identified risk resulting from the operation of an information system with the goals, objective, assets or processes that the organization uses, which it in turn aligns with or directly supports the organization's goals and objectives.

**In some cases, management may indicate a need for a more in-depth risk assessment to be performed by internal or external parties.**

#### Security Controls

> **Physical Controls**
> **Administrative Controls
> Technical Controls**

**Security Controls**
> Pertain to the physical, technical and administrative mechanisms that act as safeguards or countermeasures to protect the confidentiality, integrity and availability of the system and its information

*The implementation of controls should reduce risk to an acceptable level.* 

**Physical Controls**

> Address the security needs using physical hardware devices, such as badge readers, architectural features of buildings and facilities, and specific security actions taken by staff.

They typically provide ways of controlling, directing, or preventing the movement of people and equipment throughout a specific physical location, such as an office suite, factory or other facility.

Physical controls also provide protection and control over entry onto the land surrounding the buildings, parking lots and other areas within the organization's control.

-  In most cases, physical controls are supported by technical controls as a means of incorporating them into an overall security system.

***These require technical controls to integrate the badge or token readers, door release mechanisms, and identity management and access control systems into a more seamless security system.***

**Technical Controls**

> Security controls that computer systems and networks directly implement.
> These controls provide automated protection from unauthorized access or misuse, facilitate detection of security violations, and support security requirements for applications and data.

Technical controls can be configuration settings or parameters stored as data, managed through a software GUI, or they can be hardware settings done with switches, jumper plugs or other means.

The implementation of technical controls always requires a significant operational consideration and should be consistent with the management of security within the organization.

**Administrative Controls**

> Are directives, guidelines or advisories aimed at the people within an organization. They provide frameworks, constraints, and standards for human behavior and should cover the entire scope of the organization's activities and its interactions with external parties and stakeholders.

Admin controls can and should be powerful, effective tools for achieving information security.
	- Even the simplest security awareness policy can be an effective control if it is implemented through systematic training and practice. 

> Providing admin controls as task-level activities and operational decision practices that the workforce uses throughout their day is an effective way to improve the overall security posture.
> 	This can be done by providing them as in-context ready references and advisory resources or by linking them directly into training activities.

#### CIA Triad Deep Dive

**Confidentiality** is a difficult balance to achieve when many system users are guests or customers and it is not known whether they are accessing the system from a compromised machine or vulnerable mobile application.
	- The security professional's obligation is to regulate access -- protect the data that needs protection, yet permit access to authorized individuals.

**Sensitivity** is a measure of the importance assigned to information by its owner, or the purpose of denoting its need for protection. Sensitive information is information that if improperly disclosed (confidentiality) or modified (integrity) would harm an organization or individual.

**Integrity** measures the degree to which something is whole and complete, internally consistent, and correct. 

The concept of integrity applies to information or data:

- Systems and processes for business operations
- Organizations
- People and their actions

**Data Integrity** is the assurance that data has not been altered in an unauthorized manner. This requires the protection of the data in systems and during processing to ensure that it is free from improper modification, errors or loss of information and is recorded, used and maintained in a way that ensure it's completeness.
	- Consistency, as part of data integrity, requires that all instances of the data be identical in form, content and meaning.

**System Integrity** refers to the maintenance of a known good configuration and expected operational function as the system processes the information. Ensuring integrity begins with an awareness of **state**, which is the current condition of the system
	- Specifically, this awareness concerns the ability to document and understand the state of data or a system at a certain point, creating a **baseline**
	- The baseline is used to compare against the current state, to determine if any discrepancies have occurred that are out of the realm of normalcy

***The need to safeguard information and system integrity may be dictated by laws and regulations. Often, it is dictated by the needs of the organization to access and use reliable, accurate information.***

**Availability** can be defined as (1) timely and reliable access to information and the ability to use it, and (2) for authorized users, timely and reliable access to data and information services.
	- The core concept of availability is that data is accessible to authorized users when and where it is needed and in the form and format required.

Some systems and data are far more critical than others, so the security professional must ensure that the appropriate levels of availability are provided. 
- This requires consultation with the involved business to ensure that critical systems are identified and available. 
- Availability is often associated with the term **criticality** because it represents the importance an organization gives to data or an information system in performing its operations or achieving its mission. 

# Domain 2: Incident Response, Business Continuity and Disaster Recovery Concepts

> The incident response plan responds to unexpected changes in operating conditions to keep the business operating
> The Business Continuity plan enables the business to continue operating throughout the crisis
> If both the Incident Response and Business Continuity Plans fail, the Disaster Recovery Plan is activated to help the business return to normal operations as quickly as possible

Security professionals spend their days ensuring the confidentiality, integrity and availability of data and systems, but in addition to safeguarding networks and securing the exchange of data and shared resources, it's important to realize that cybersecurity goes beyond the technical aspects. Its scope encompasses the protection of people and their personal information.

**Learning Objectives**

- Explain how organizations respond to, recover from and continue to operate during unplanned disruptions
- Recall the terms and components of incident response
- Summarize the components of a business continuity plan
- Identify the components of disaster recovery
- Practice the terminology of and review incident response, business continuity and disaster recovery concepts

#### Incident Terminology

> Inevitably, things go wrong in cybersecurity.
> For this reason, cybersecurity professionals also play the role of first responders. An understanding of incident response starts with knowing the terms used to describe various cyberattacks.

**Breach**

>The loss of control, compromise, unauthorized disclosure, unauthorized acquisition or any similar occurrence where:
>	a person other than an authorized user access or potentially accesses personally identifiable information (PII)
>	an authorized user accesses personally identifiable information for other than an authorized purpose
>**NIST SP 800-53 Rev. 5**


**Event**

> Any observable occurrence in a network or system.

**Exploit**

> A particular attack. It is named this way because these attacks exploit system vulnerabilities

**Incident**

> An event that actually or potentially jeaporadizes the confidentiality, integrity or availability of an information system or the information the system processes, stores or transmits

**Intrusion**

> A security event, or combination of events, that constitutes a deliberate security incident in which an intruder gains, or attempts to gain, access to a system or system resource without authorization
> 	**IETF RFC 4949 Ver 2**

**Threat**

> Any circumstance or even with the potential to adversely impact organizational operations, organizational assets, individuals, other organizations, or the nation through an information system via unauthorized access, destruction, disclosure, modification of information, and/or denial of service attacks.
> 	**NIST SP 800-30 Rev 1**

**Vulnerability**

> Weakness in an information system, system security procedures, internal controls, or implementation that could be exploited by a threat source.
> 	**NIST SP 800-53 Rev 1**

**Zero Day**

> An previously unknown system vulnerability with the potential of exploitation without risk of detection or prevention because it does not, in general, fit recognized patterns, signatures, or methods.

#### The Goal of Incident Response

Every organization must be prepared for incidents. Despite the best efforts of an organization's management and security teams to avoid or prevent problems, it is inevitable that adverse events will happen that have the potential to affect the business mission or objectives.

**The priority of any incident response is to protect life, health and safety. When any decision related to priorities is to be made, always choose safety first.**

The primary goal of incident management is to be prepared. Preparation requires having a policy and response plan that will lead the organization through the crisis.

The incident response process is aimed at reducing the impact of an incident so the organization can resume the interrupted operations as soon as possible. Incident response planning is a subset of the greater discipline of business continuity management (BCM)

#### Components of a Business Continuity Plan

> Business continuity planning (BCP) is the proactive development of procedures to restore business operations after a disaster or other significant disruption to the organization.

Members from across the organization should participate in creating the BCP to ensure all systems, processes and operations are accounted for in the plan.

- In order to safeguard the confidentiality, integrity and availability of information, the technology must align with the business needs. 

**Here are some common components of a comprehensive business continuity plan:**

- List of the BCP team members, including multiple contact methods and backup members.
- Immediate response procedures and checklists (security and safety procedures, fire suppression procedures, notification of appropriate emergency response agencies, etc.)
- Notification systems and call trees for alerting personnel that the BCP is being enacted
- Guidance for management, including designation of authority for specific managers
- How/when to enact the plan
- Contact numbers for critical members of the supply chain (vendors, customers, possible external emergency providers, third-party partners)

#### Business Continuity in Action

**What does business continuity look like in action?**

> a **Business Impact Analysis** is an analysis procedure that determines the impact of emergencies that occur and their effect on other areas of the business
>> The document will identify the dependencies of the particular department and develop a plan of action to restore them or cover the duties until the department can be operational again

Ideally, this pre-planning will result in a minimal loss to the company and it's ability to provide service to customers.

#### The Importance of Business Continuity

> The intent of a business continuity plan is to sustain business operations while recovering from a significant disruption. An event has created a disturbance in the environment, and now you need to know how to maintain the business.

**A key part of the plan is communication, including multiple contact methodologies and backup numbers in case of a disruption of power or communications.**

Many companies will establish a phone tree, so if one person is not available, they know who else to call. 
	- Organizations will go through their procedures and checklists to make sure they know exactly who is responsible for which action. 
	- Individuals with proper authority must be there the execute operations, for instance, if there are critical areas that need to be shut down.

#### Components of the Incident Response Plan

The incident response policy should reference an incident response plan that all employees will follow, depending on their role in the process. The plan may contain several procedures and standards related to incident response.
- It's a living representation of an organization's incident response policy.

Procedures to implement the plan should define the technical processes, techniques, checklists and other tools that teams will use when responding to an incident.

**Here are the components commonly found in an incident response plan:**

1. Preparation
2. Detection & Analysis
3. Containment, Eradication & Recovery
4. Post-Incident Activity

**Preparation**

- Develop a policy approved by management
- Identify critical data and systems and any single points of failure
- Train staff on incident response
- Implement an incident response team
- Practice *Incident Identification*
- Identify roles & responsibilities
- Plan the coordination of communication between stakeholders
- Consider the possibility that a primary method of communication may not be available

**Detection & Analysis**

- Monitor all possible *attack vectors*
- Analyze the incident using known data and threat intelligence
- Prioritize incident response
- Standardize incident documentation

**Containment**

- Gather evidence
- Choose an appropriate containment strategy
- Identify the attacker
- Isolate the attack

**Post-Incident Activity**

- Identify evidence that may need to be retained
- Document lessons learned

Conduct a retrospective of:

- Preparation
- Detection and analysis
- Containment, Eradication and Recovery
- Post-Incident Activity

#### Incident Response Team

> A properly staffed and trained incident response team can be leveraged, dedicated or a combination of the two, depending on the requirements of the organization.

**Many IT professionals are classified as first responders for incidents. They are the first ones on the scene and know how to differentiate typical IT problems from security incidents.**

Similar to medical first responders, IT professionals need specific training so they can determine the difference between a typical problem that needs troubleshooting and a security incident that they need to report and address at a higher level.

> A typical incident response team is a cross-functional group of individuals who represent the managerial, technical and functional areas of responsibility most directly impacted by a security incident. 
> Potential team members include the following:
> 	Representatives of senior management
> 	Information security professionals
> 	Legal representatives
> 	Public affairs/communications representatives
> 	Engineering representatives (systems and network)

Many organizations now have dedicated teams responsibile for investigating any computer security incidents that take place. These teams are commonly known as computer incident response teams (**CIRTS**). 

These teams have four primary responsibilities when an incident occurs:

- *Determine the amount and scope of damage caused by the incident*
- *Determine whether any confidential information was compromised during the incident*
- *Implement any necessary recovery procedures to restore security and recover from incident-related damage*
- *Supervise the implementation of any additional security measures necessary to improve security and prevent recurrence of the incident*

#### The Goal of Disaster Recovery

> **Disaster Recovery steps in where business continuity leaves off.**

When a disaster strikes or an interruption of business activities occurs, the **disaster recovery plan (DRP)** guides the actions of emergency response personnel until the end goal is reached -- which is to see the business restored to full last-known reliable operations.

Disaster recovery refers specifically to restoring the information technology and communications services and systems needed by an organization, both during the period of disruption caused by any event and during restoration of normal services.

> Whereas business continuity planning is about maintaining critical business functions, disaster recovery planning is about restoring IT and communications back to full operations after a disruption.

#### Components of a Disaster Recovery Plan

**Depending on the size of the organization and number of people involved in the DRP effort, organizations often maintain multiple types of plan documents, intended for different audiences.**

The following list includes various types of documents worth considering:

- Executive summary providing a high-level overview of the plan
- Department specific plans
- Technical guides for IT personnel responsible for implementing and maintaining critical backup systems
- Full copies of the plan for critical disaster recovery team members
- Checklists for certain individuals:
	- Critical disaster recovery team members will have checklists to help guide their actions amid the chaotic atmosphere of a disaster
	- IT personnel will have technical guides helping them get the alternate sites up and running
	- Managers and public relations personnel will have simple-to-follow, high-level documents to help them communicate the issue accurately without requiring input from team members who are busy working on recovery.

#### Disaster Recovery in the Real World

**It is vital to ensure that an organization's critical systems are formally identified and have backups that are regularly tested. Sometimes an incident is not recognized or detected until days or months later.**

Complex systems can often store valuable information across several servers. While at its most basic level, disaster recovery plans include backing up data at a server level, it is also necessary to consider the database itself, as well as any dependencies on other systems.

> It is important to understand the flow of data and the intricate dependencies of one system on another to properly document and implement a disaster recovery plan that will be successful when it is needed.

# Domain 3: Access Control Concepts

**Learning Objectives:**

- Select access controls that are appropriate in a given scenario. 
- Relate access control concepts and processes to given scenarios
- Compare various physical access controls
- Describe logical access controls
- Practice the terminology of access controls and review concepts of access controls.

**Key Topics:**

- Security Control Protocols
- Access Control Strategies
- User Privilege Administration

#### What is Security Control?

**A control is a safeguard or countermeasure designed to preserve Confidentiality, Integrity and Availability of Data.**

Access control involves limiting what objects can be available to what subjects according to what rules.

A firewall is an example of a control, which are included in a system or network to prevent something from the outside from getting in and disturbing or compromising the environment.

#### Controls Overview

> It can be argued that access controls are the heart of an information security program.
> But in the end, security all comes down to who can get access to organizational assets (buildings, data, systems, etc.) and what they can do when they get access.

Access controls are not just about restricting access to information systems and data, but also about allowing access.

**Access is Based on Three Elements:**

- Subjects
- Objects
- Rules

**Subjects**

> A subject can be defined as any entity that requests access to assets.

The entity requesting access may be a user, a client, a process or a program, for example. A subject is the initiator of a request for service; therefore, a subject is referred to as "active."

A subject:

- Is a user, a process, a procedure, a client (or a server), a program, or a device such as an endpoint, workstation, smartphone or removable storage device with onboard firmware.
- Is active: It initiates a request for access to resources or services.
- Requests a service from an object.
- Should have a level of clearance (permissions) that relates to its ability to successfully access services or resources.

**Objects**

>By definition, anything that a subject attempts to access in referred to as an object.

An object is a device, process, person, user, program, server, client or other entity that responds to a request for service.

Whereas a subject is active in that it initiates a request for service, an object is passive in that it takes no action until called upon by request from a subject.

>By definition, objects do not contain their own access control logic. Objects are passive, not active (in access control terms), and must be protected from unauthorized access by some other layers of functionality in the system, such as the integrated identity and access management system.
>	Quite often, the rules of access for an object are stored in a rule base or access control list.

**An Object:**

- Is a building, computer, file, database, printer or scanner, server, comms resource, a block of memory, an I/O port, a person, a software task, a thread or a process.
- Is anything that provides service to a user
- Is passive
- Responds to a request
- May have a classification

**Rules**

> An access rule is an instruction developed to allow or deny access to an object by comparing the validated identity of the subject to an access control list.

One example of a rule is a firewall access control list. By default, firewalls deny access from any address to any address, on any port. For a firewall to be useful, however, it needs more rules.

A rule can: 

- Compare multiple attributes to determine appropriate access
- Allow access to an object
- Define how much access is allowed
- Deny access to an object
- Apply time based access

#### Defense in Depth

> All-access permissions includes access to buildings, server rooms, networks, applications and utilities. These are all implementations of access control and are part of a layered defense strategy, also known as defense in depth, developed by an organization.

**Defense in Depth** describes an information security strategy that integrates people, technology, and operations capabilities to establish variable barriers across multiple layers and missions of the organization.
	- It applies multiple countermeasures in a layered fashion to fulfill security objectives. Defense in depth should be implemented to prevent or deter a cyberattack, but it cannot guarantee that an attack will not occur.

**When a company has information at multiple sensitivity levels, it might require the network traffic to be validated by rules on more than one firewall, with the most sensitive information being stored behind multiple firewalls.**

 #### What are Logical Access Controls?

Whereas physical access controls are tangible methods or mechanisms that limit someone from getting access to an area or asset, logical access controls are electronic methods that limit someone from getting access to systems, and sometimes even tangible assets or areas.

**Types of Logical Access Controls include:**

- Passwords
- Biometrics (implemented on a system, such as a smartphone or laptop)
- Badge/token readers connected to a system

*These types of electronic tools limit who get logical access to an asset, even if the person already has physical access.*

#### Controls and Risks

> A control serves to reduce the risk according to where it falls within the risk tolerance of the individual or organization.

*A physical control would be a seatbelt*

*An administrative control would be a law requiring the use of a seatbelt.*

These controls together serve to reduce the risk of driving to a degree that is acceptable to the driver and society.

#### Control Assessments

> Risk reduction depends on the effectiveness of the control. It must apply to the current situation and adapt to a changing environment.

*Consider a scenario where part of an office building is being re-purposed for use as a secure storage facility. Due to the previous use of the area, there are 5 doors which must be secured before confidential files can be stored there. When securing a physical location, there are several things to consider.*

To keep the information the most secure, it might be recommended to install biometric scanners on all doors. A site assessment will determine if all five doors need biometric scanners, or if only one or two doors need scanners. 

The remaining doors could be permanently secured, or if the budget permits, the doors could be removed and replaced with a permanent wall. 

#### Role-Based Access Control in the Workplace

*Role-based access control provides each worker privileges based on what role they have in the organization.*

> Only HR has access to personnel files, only Finance has access to bank accounts; each manager has access to their own direct reports and their own department.

**Privilege Creep** is when junior roles inherit access and permissions from previous personnel when those permissions are not critical for their job duties.

Upon hiring or changing roles, it is recommended to not copy user profiles to new users. It is recommended that once standard roles are established, and new users are created based on those standards rather than an actual user.

#### Privileged Accounts

> Privileged Accounts are those with permissions beyond those of normal users, such as managers and administrators.

Broadly speaking, these accounts have elevated privileges and are used by many different classes of users, including:

- Sysadmins, who have the principal responsibilities for operating systems, applications deployment, and performance management.
- Help desk or IT support staff, who often need to view or manipulate endpoints, server, and applications platforms by using privileged or restricted operations.
- Security analysts, who may require rapid access to the entire IT infrastructure, systems, endpoints and data environment of the organization. 

*The delegation of authority and responsibility should be contingent on trustworthiness, since misuse or abuse of these privileges could lead to harm for the organization or it's stakeholders.*

>Typical measures used for moderating the potential for elevated risks from misuse or abuse of privileged accounts include the following:

- *More extensive and detailed logging than regular user accounts.* 
	- Acts as both a deterrent and as an administrative control
- *More stringent access control that regular user accounts*
	- Users with higher privileges should be required to go through more rigorous or additional authentication prior to gaining those privileges. 
	- Just-in-time identity should also be considered a way to restrict the use of these privileges to specific tasks and the times at which the user is executing them. 
- *Deeper trust verification than regular user accounts*
	- Privileged account holders should be subject to more detailed background checks, stricter non-disclosure agreements and acceptable use policies
- *More auditing than regular user accounts*
	- Privileged account activity should be monitored and audited at a greater rate and extent than regular usage.

##### Explore Privileged Access Management Further

Consider the Help Desk role. In order to provide the level of service customers demand, it may be necessary for Help Desk personnel to reset passwords and unlock user accounts. In a Windows environment, this typically requires "domain admin" privileges. 
	Those two permissions can be granted alone, giving the Help Desk personnel a way to reset passwords without giving them access to everything in the Windows domain, such as adding new users or changing a user's information.

#### Monitoring

The use of physical access controls, monitoring personnel and equipment entering and leaving, and auditing and logging all physical events are primary elements in maintaining overall organizational security. 

**Monitoring Examples**

**Cameras**

Cameras are normally integrated into the overall security program and centrally monitored. Cameras provide a flexible method of surveillance and monitoring. They can be a deterrent to criminal activity, can detect activities if combined with other sensors and, if recorded, can provide evidence after the activity. 
	They are often used in locations where access is difficult or there is a need for a forensic record. 

**Logs**

A log is a record of events that have occurred. Physical security logs are essential to support business requirements. They should capture and retain information as along as necessary for legal or business reasons. 

Because logs may be needed to prove compliance with regulations and assist in a forensic investigation, the logs must be protected from manipulation. 
	Logs may also contain sensitive data about customers or users and should be protected from unauthorized disclosure. 

A **log anomaly** is anything out of the ordinary. Identifying log anomalies is often the first step in identifying security-related issues, both during an audit and during routine monitoring. 

Some anomalies will be glaringly obvious: for example, gaps in date/time stamps or account lockouts. 

Others will be harder to detect, such as someone trying to write data to a protected directory. Although it may seems that logging everything to avoid missing any important data is the best approach, most organizations would soon drown under the amount of data collected. 

Some businesses are mandated by their industry standards to retain log data for a certain amount of time. **Payment Card Industry Data Security Standard (PCI DSS)** requires that businesses retain one year of log data in support of PCI. Some federal regulations include requirements for data retention as well.

**Alarm Systems**

Alarm systems are commonly found on doors and windows in homes and office buildings. In their simplest form, they are designed to alert the appropriate personnel when a door or window is opened unexpectedly. 

For example, an employee may enter a code and/or swipe a badge to open a door, and that action would not trigger an alarm.
	Alternatively, if that same door was opened by brute force without someone entering the correct code or using an authorized badge, an alarm would be activated.

#### Examples of Least Privilege

> To preserve the confidentiality of information and ensure that it is only available to personnel who are authorized to see it, we use privileged access management, which is based on the principle of least privilege. 
> 	That means each user is granted access to only the items they need and nothing further. 

**For example, only individuals working in billing will be allowed to view consumer financial data, and even fewer individuals will have the authority to change or delete that data.**

This maintains confidentiality and integrity while also allowing availability by providing administrative access with an appropriate password or sign-on that proves the user has the appropriate permissions to access that data.

Sometimes it is necessary to allow users to access the information via a temporary or limited access, for instance, for a specific time period or just within normal business hours.

>Or, access rules can limit the fields that the individuals can have access to.
>	One example of this would be a healthcare environment. Some worked might have access to patient data but not their medical data. Individual doctors might have access only to data related to their own patients. In some cases, this is regulated by law, such as HIPAA.

Systems often monitor access to private information, and if logs indicate that someone has attempted to access a database without the proper permissions, that will automatically trigger an alarm.

**The more critical information a person has access to, the greater the security should be around that access. They should definitely have multi-factor authentication, for example.**

#### Mandatory Access Control (MAC) in the Workplace

>Mandatory access control is determined by the owner of the assets, on an across-the-board basis, with little individual decision making about who gets access.

For example, at certain government agencies, personnel must have a certain type of security clearance to get access to certain areas. In general, this level of access is set by government policy and not by an individual giving permission based on their own judgment.

**Often this is accompanied by separation of duties, where the scope of work is limited and users do not have access to information that does not concern them. This separation of duties is also facilitated by role-based access control. **

#### Mandatory Access Control

> A **Mandatory Access Control (MAC)** policy is one that is uniformly enforced across all subjects and objects within the boundary of an information system. 

In the simplest terms, this means that only properly designated security administrators, as trusted subjects, can modify any of the security rules that are established for subjects and objects within the system. 

This also means that for all subjects defined by the organization (that is, known to its integrated identity management and access control system), the organization assigns a subset of total privileges for a subset of objects, such that the subject is constrained from doing any of the following:

- Passing the information to unauthorized subjects or objects
- Granting its privileges to other subjects
- Changing one or more security attributes on subjects, objects, the information systems or system components
- Choosing the security attributes to be associated with newly created or modified objects
- Changing the rules governing access control

**Although MAC sounds very similar to DAC, the primary difference is who can control access. With Mandatory Access Control, it is mandatory for security administrators to assign access rights or permissions; with Discretionary Access Control, it is up to the object owner's discretion.**

#### What are Physical Security Controls?

> Physical security controls are items you can physically touch. They include physical mechanisms deployed to prevent, monitor or detect direct contact with systems or areas within a facility. 

Examples of physical access controls include security guards, fences, motion detectors, locked doors/gates, sealed windows, lights, cable protection, laptop locks, badges, swipe cards, guard dogs, cameras, mantraps/turnstiles, and alarms.

Physical controls are necessary to protect the assets of a company, including its most important asset: people. When considering access controls, the security of the personnel always comes first, followed by securing other physical assets. 

**Why Have Physical Security Controls?**

Physical access controls prevent unauthorized individuals from entering a physical site, such as a workplace.

This is not only to protect physical assets like computers and hardware, but also the health and safety of the personnel inside. 

#### Privileged Access Management

> **Privileged Access Management** provides the first and perhaps most familiar use case. Consider a human user identity that is granted various create, read, update and delete privileges on a database. 
> 	Without privileged access management, the system's access control would have those privileges assigned to the administrative user in a static way, effectively "on 24/7". 

Security would be dependent upon the login process to prevent misuse of that identity. 

Just-in-time privileged access management, by contrast, includes role-based specific subsets of privileges that only become active in real time when the identity is requesting the use of a resource or service. 

#### Separation of Duties

> **Separation of Duties is based on the security practice that no one person should control and entire high-risk transaction from start to finish.**

Separation of duties breaks the transaction into separate parts and requires a different person to execute each part of the transaction. For example, an employee may submit an invoice for payment to a vendor (or for reimbursement to themselves). but it must be approved by a manager prior to payment; in another instance, almost anyone may submit a proposal for a change to a system configuration, but the request must go through technical and management review and gain approval before it can be implemented. 

These steps can prevent fraud or detect an error in the process before implementation. 
It could be that the same employee might be authorized to originally submit invoices regarding one set of activities but not approve them, and yet also have approval authority but not the right to submit invoices on another. 
	It is possible, of course, that two individuals can willfully work together to bypass the separation of duties to jointly commit fraud. This is called collusion. 

Another implementation of separation of duties is dual control.  
	This would apply at a bank where there are two separate combination locks on the door of the vault. Some personnel know one of the combinations and some know the other, but no one person knows both combinations. 

**Two-Person Integrity**

> The two person rule is a security strategy that requires a minimum of two people to be in an area together, making it impossible for a person to be in the area alone. 
> 	Many access control systems prevent an individual cardholder from entering a selected high-security area unless accompanied by at least one other person. 

#### Discretionary Access Control

> **Discretionary Access Control (DAC) is a specific type of access control policy that is enforced over all subjects and objects in an information system.**

In DAC, the policy specifies that a subject who has been granted access to information can do one or more of the following: 

- Pass the information to other subjects or objects
- Grant its privileges to other subjects
- Change security attributes on subjects, objects, information systems, or system components
- Choose the security attributes to be associated with newly created or revised objects
- Change rules governing access control, mandatory access controls restrict this capability

**DAC Example**

Discretionary access control systems allow users to establish or change these permissions on files they create or otherwise have ownership of. 

Many operating systems, such as Windows and the whole Unix family tree (including Linux) and iOS, use this type of data structure to make fast, accurate decisions about authorizing or denying an access request. Note that this data can be viewed as either rows or columns. 

- An object's access control list shows the total set of subjects who have any permissions at all for that specific object
- A subject's capabilities list shows each object in the system that said subject has any permissions for. 

> This methodology relies on the discretion of the owner of the access control object to determine the access control subject's specific rights. 
> 	Hence, security of the object is literally up to the discretion of the object owner.

DACs are not very scalable, they rely on the access control decisions made by each individual object owner, and it can be difficult to find the source of access control issues when problems occur.

**DAC in the Workplace**

Most information systems are DAC systems. In a DAC system, a user who has access to a file is able to share that file with or pass it to someone else. It is at the discretion of the asset owner whether to grant or revoke access to the user. For access to computer files, this can be shared files or password protections.

#### Authorized vs. Unauthorized Personnel

> Subjects are given authorized access to objects after they have been authenticated. Authentication is confirming the identity of the subject. Once a subject has been authenticated, the system checks its authorization to see if it is allowed to complete the action it is attempting.

This is usually done via a security matric access by the system controlling the access, based on pre-approved levels. For example, when a person presents an ID badge to the data center door, the system checks the ID number, compares that to a security matrix within the system, and unlocks the door if the ID is authorized.
	IF the ID is not authorized to unlock the door, it will remain locked. In another example, a user attempts to delete a file.
		- The file system checks the permissions to see if the user is authorized to delete the file. If the user is authorized, the file is deleted. If the user is not authorized, the file is left untouched.

**How Users are Provisioned**

> Other situations that call for provisioning new user accounts or changing privileges include:

- **A New Employee**:
	- When a new employee is hired, the hiring manager sends a request to the security administrator to create a new user ID. This request authorizes creation of the new ID and provides instructions on appropriate access levels.
- **Change of Position**
	- When an employee has been promoted, their permissions and access rights might change as defined by the new role, which will dictate any added privileges and updates to access. At the same time, any access that is no longer needed in the new job will be removed.
- **Separation of Employment**
	- When employees leave the company, depending on company policy and procedures, their accounts must be disabled for a period before they are deleted to preserve the integrity of any audit trails or files that may be owned by the user. 
	- Since the account will no longer be used, it should be removed from any security roles or additional access profiles.

#### Types of Physical Access Controls

> Control, monitor and manage access to a facility.

- These range from deterrents to detection mechanisms. Each area requires unique and focused physical access controls, monitoring and detection mechanisms. 

**Badge Systems and Gate Entry**

> Technologies such as turnstiles, mantraps, and remotely or system controlled door locks. 

Most often, a badge is produced and issued with the employee's identifiers, with the entrollment station giving the employee specific areas that will be accessible. 

In high-security environments, enrollment may also include biometric characteristics. In general, an access control system compares an individuals badge against a verified database.

**A range of card types allow the system to be used in a variety of environments. These cards include:**

- Bar Code
- Magnetic stripe
- Proximity
- Smart
- Hybrid

**Environmental Design**

**Crime Prevention through Environmental Design** approaches the challenge of creating workspaces through passive design elements. This has great applicability for the information security community as security professionals design, operate and assess the organizational security environment. 

Other practices, such as standards for building construction and data centers, also affect how we implement controls over our physical environment. Security professionals should be familiar with these concepts so they can successfully advocate for functional and effective physical spaces where information is created, processed and stored.

**Biometrics**

> To authenticate a user's identity, biometrics use characteristics unique to the individual seeking access. A biometric authentication solution entails two processes:

- Enrollment. During the enrollment process, the user's registered biometric code is stored either in a system or on a smart card that is kept by the user.
- Verification. During the verification process, the user presents their biometric data to the system so that the biometric data can be compared with the stored biometric code.

> Biometric data constitutes PII, so it should not be revealed without the user's consent.

**Physiological**

Physiological biometric systems measure the characteristics of a person such as a fingerprint, iris scan, retinal scan, palm scan and venous scans that look for the flow of blood through the veins in a palm.

**Behavioral**

Behavioral systems measure how a person acts by measuring voiceprints, signature dynamics, and keystroke dynamics. 

**Biometrics** are considered highly accurate, but can be very expensive to implement and maintain. 
- Users are often uncomfortable with the use of biometrics, considering them to be an invasion of privacy.

# Domain 4: Network Security

**A network is simply two or more computers linked together to share data, information and resources.**

To properly establish secure data communications, it is important to explore all of the technologies involved in computer communications.

From hardware to software to protocols and encryption and beyond, there are many details, standards and procedures to be familiar with. 

**Types of Networks**

Local Area Network (LAN)
- A local area network (LAN) is a network typically spanning a single floor or building. This is commonly a limited geographical area.
Wide Area Network (WAN)
- Wide Area Network is the term usually assigned to the long-distance connections between geographically remote networks.

#### Network Devices

**Hubs**

Hubs are used to connect multiple devices in a network. They're less likely to be seen in business or corporate networks than in home networks. 
Hubs are wired devices that are not as smart as switches or routers.

**Firewall**

Firewalls are essential tools in managing and controlling network traffic and protecting the network. A firewall is a network device used to filter traffic. It is typically deployed between a private network and the internet, but it can also be deployed between departments. (segmented networks) within an organization.

Firewalls filter traffic based on a defined set of rules, also called filters or access control lists.

**Switch**

Rather than using a hub, you might consider a switch, or what is also known as an intelligent hub. Switches are wired devices that know the addresses of the devices connected to them and route traffic to that port/device rather than retransmitting to all devices. 

Offering greater efficiency for traffic delivery and improving the overall throughput of data, switches are smarter than hubs, but not as smart as routers.

Switches can also create separate broadcast domains when used to create VLANs.

**Server**

A server is a computer that provides information to other computers on a network. Some common servers are web servers, email servers and file servers. All of these are, by design, networked and accessed in some way by a client computer. 

Servers are usually secured differently than workstations to protect the information they contain.

**Router**

Routers are used to control traffic flow on networks and are often used to connect similar networks and control traffic flow between them. Routers can be wired or wireless and can connect multiple switches. 

Smarter than hubs and switches, routers determine the most efficient "route" for the traffic to flow across a network. 

**Endpoint**

Endpoints are the ends of a network communication link. One end is often at a server where a resource resides, and the other end if often a client making a request to use a network resource.

An endpoint can be another server, desktop workstation, laptop, tablet, mobile phone, or any other end user device.

#### Other Networking Terms

**Ethernet**

Ethernet (IEEE 802.3) is a standard that defines wired connections of networked devices. 

The standard defines the way data is formatted over the wire to ensure disparate devices can communicate over the same cables.

**Media Access Control Address (MAC)**

Every network device is assigned a Media Access Control (MAC) address. An example is 00-13-02-1F-58-F5.

The first three bytes (24 bits) of the address denote the vendor or manufacturer of the physical network interface. No two devices can have the same MAC address in the same local network; otherwise and address conflict occurs. 

**Internet Protocol (IP) Address**

While MAC addresses are generally assigned in the firmware of the interface, IP hosts associate that address with a unique logical address. This logical IP address represents the network interface within the network and can be useful to maintain communications when a physical device is swapped with new hardware.

#### What is Wi-Fi

>Wireless networking is a popular method of connecting corporate and home systems because of the ease of deployment and relatively low cost. 

**It has made networking more versatile than ever before. Workstations and portable systems are no longer tied to a cable but can roam freely within the signal range of the deployed wireless access points. However, with this freedom comes additional vulnerabilities.**

WiFi range is generally wide enough for most homes or small offices, and range extenders may be placed strategically to extend the signal for larger campuses or homes. Over time the Wi-Fi standard has evolved, with each updated version faster than the last. 

In a LAN, threat actors need to enter the physical space or immediate vicinity of the physical media itself. 

For wired networks, this can be done by placing sniffer taps onto cables, plugging in USB devices, or using other tools that require physical access to the network. 

#### Microsegmentation

> The toolsets of current adversaries are polymorphic in nature and allow threats to bypass static security protocols

Modern cyber attacks take advantage of traditional security models to move easily between systems within a data center. Microsegmentation aids in protecting against these threats. 

A fundamental design requirement of microsegmentation is to understand the protection requirements for traffic within a data center and traffic and from the internet traffic flows.
- When organizations avoid infrastructure-centric design paradigms, they are more likely to become more efficent at service delivery in the data center and become apt at detecting and preventing advanced persistent threats (APTs)

**Micro-segmentation Characteristics**

- Micro-segmentation allows for granular restrictions within the IT environment, to the point where rules can be applied to individual machines and/or users, and these rules can be as detailed and complex as desired. 
	- For instance, it can limit which IP addresses can communicate to a given machine, at which time of day, with which credentials, and which services those connections use.

- Micro-segmentation uses logical rules, not physical rules, and does not require additional hardware or manual interaction with the device (that is, the administrator can apply the rules to various machines without having to physically touch each device or the cables connecting it to the networked environment.)

- Microsegmentation is the ultimate end state of the defense-in-depth philosophy; no single point of access within the IT environment can lead to broader compromise.

- Microsegmentation is crucial in shared environments, such as the cloud, where more than one customer's data and functionality might reside on the same device(s), and where third-party personnel (admins, technicians who work for the cloud provider, not the customer) might have physical access to the devices. 

- Allows the organization to limit which business functions, units, offices, or departments can communicate with others, to enforce the concept of least privilege. 

- In modern environments, microsegmentation is available because of virtualization and software-defined networking (SDN) technologies. In the cloud, the tools for applying this strategy are often called "virtual private networks (VPNs)" or "Security groups"

- Even in your home, microsegmentation can be used to separate computers from smart TVs, air conditioning and smart appliances, which can be connected and have vulnerabilities.

#### Intrusion Detection Systems

> An intrusion occurs when an attacker is able to bypass or thwart security mechanisms and gain access to an organization's resources.

**Intrusion Detection is a specific form of monitoring that monitors recorded information and real-time events to detect abnormal activity indicating a potential incident or instrusion.**

An *Intrusion Detection System* automates the inspection of logs and real-time system events to detect intrusion attempts and system failures.
- An IDS is intended as part of a defense-in-depth security plan. It will work with, and complement, other security mechanisms such as firewalls, but it does not replace them.

IDSs recognize attacks that come from external connections, such as an attack from the internet, and attacks that spread internally, such as a malicious worm. 
- Once a suspicious event is detected, they respond by sending alerts or raising alarms. A primary goal of an IDS is to provide a means for a timely and accurate response to intrusions.

IDS types are commonly classified as **host-based** and **network-based**. A host-based IDS (HIDS) monitors a single computer or host.

A Network-based IDS (NIDS) monitors a network by observing network traffic patterns.

**Host-based Intrusion Detection System**

- Monitors activity on a single computer, including process calls and information recorded in a system, application, security and host-based firewall logs. 
- Can often examine events in more detail than a NIDS can. 
- Can pinpoint specific files compromised in an attack.
	- Also can track processes used by an attacker. 

**Network Intrusion Detection System**

A NIDS monitors and evaluates network activity to detect attacks or event anomalies.

- It cannot monitor the content of encrypted traffic but can monitor other packet details. 
- A single NIDS can monitor a large network by using remote sensors to collect data at key network locations that send data to a central management console.
	- These sensors can monitor traffic at routers, firewalls, network switches that support port mirroring, and other types of network taps.
- A NIDS has very little negative effect on the overall network performance, and when it is deployed on a single-purpose system, it doesn't adversely affect performance on any other computer.

**Security Information and Event Management (SIEM)**

> Security management involves the use of tools that collect information about IT environments from many disparate sources to better examine the overall security of the organization and streamline security efforts. 

- The idea of a SIEM solution is to gather log data from various sources across the enterprise to better understand potential security concerns and apportion resources accordingly. 

#### Preventing Threats

> While there is no single step you can take to protect against all threats, there are some basic steps you can take that help reduce the risk of many types of threat: 

- **Keep systems and applications up to date.** Vendors regularly release patches to correct bugs and security flaws, but these only help when they are applied. Patch management ensures that systems and applications are kept up to date with relevant patches. 
- **Remove or disable unneeded services and protocols**. If a system doesn't need a service or protocol, it should not be running. Attackers cannot exploit a vulnerability in a service or protocol that isn't running on a system. 
- **Use intrusion detection and prevention systems.** Intrusion detection and prevention systems observe activity, attempt to detect threats, and provide alerts. They can often block or stop attacks.
- **Use firewalls.** Firewalls can prevent many different types of threats. Network-based firewalls protect entire networks, and host-based firewalls protect individual systems.
- **Use up-to-date anti-malware software.** A primary countermeasure.
#### Antivirus

> The use of antivirus products is strongly encouraged as a security best practice and is a requirement for compliance with the PCI DSS.

There are several antivirus products available, and many can be deployed as part of an enterprise solution that integrates with several other security products.

Antivirus systems try to identify malware based on the signature of known malware or by detecting abnormal activity on a system. 
- Identification is done with various types of scanners, pattern recognition, and advanced machine learning algorithms.

Many endpoint antivirus products include firewalls, IDS and IPS systems.
#### Scans

> Here is an example scan from Zenmap showing open ports on a host.

Regular vulnerability and port scans are a good way to evaluate the effectiveness of security controls used within an organization.

They may reveal areas where patches or security settings are insufficient, where new vulnerabilities have developed or become exposed, and where security policies are either ineffective or not being followed. 
#### Firewalls

> In building construction or vehicle design, a firewall is a specially built physical barrier that prevents the spread of fire from one area of the structure to another or from one compartment of a vehicle to another.

Early computer security engineers borrowed that name for the devices and services that isolate network segments from each other, as a security measure. 

As a result, firewalling refers to the process of designing, using or operating different processes in ways that isolate high-risk activities from lower-risk ones. 

- Firewalls enforce policies by filtering network traffic based on a set of rules. While a firewall should always be placed at internet gateways, other internal network considerations and conditions determine where a firewall would be employed, such as network zoning or segregation of different levels of sensitivity. 

Firewalls have rapidly evolved over time to provide enhanced security capabilities. This growth in capabilities can be seen in the graphic below, which contrasts an oversimplified view of traditional and next-generation firewalls.

It integrates a variety of threat management capabilities into a single framework, including proxy services, intrusion prevention services (IPS) and tight integration with the identity and access management (IAM) environment to ensure only authorized users are permitted to pass traffic across the infrastructure.
- While firewalls can manage traffic at Layers 2 (MAC addresses), 3 (IP ranges) and 7 (application firewalls), the traditional implementation has been to control traffic Layer 4. 

#### Intrusion Prevention System

> An intrusion prevention system (IPS) is a special type of active IDS that automatically attempts to detect and block attacks before they reach target systems.

A distinguishing difference between an IDS and IPS is that the IPS is placed in line with the traffic.

In other words, all traffic must pass through the IPS and the IPS can choose what traffic to forward and what traffic to block after analyzing it. 
- This allows the IPS to prevent an attack from reaching a target.

#### Redundancy

> The concept of redundancy is to design systems with duplicate components so that if a failure were to occur there would be a backup. 

This can apply to the data center as well. Risk assessments pertaining to the data center should identify when multiple separate utility service entrances are necessary for redundant communication channels and/or mechanisms. 

If the organization requires full redundancy, devices should have two power supplies connected to diverse power sources.

#### Network Segmentation (Demilitarized Zone)

**Network segmentation is an effective way to achieve defense in depth for distributed or multitiered applications. The use of a demilitarized zone (DMZ), for example, is a common practice in security architecture.**

With a DMZ, host systems that are accessible through the firewall are physically separated from the internal network by means of secured switches or by using an additional firewall to control traffic between the web server and the internal network. Application DMZs (or semi-trusted networks) are frequently used today to limit access to application servers to those networks or systems that have a legitimate need to connect.

> For example, in a hospital or doctor's office, you would have a segregated network for the patient information and billing, and on the other side would be the electronic medical records. 

**Web-Application Firewall**

The WAF has an internal and an external connection like a traditional firewall, with the external traffic being filtered by the traditional or next generation firewall first. It monitors all traffic, encrypted or not, from the outside for malicious behavior before passing commands to a web server that may be internal to the network. 

#### Virtual Private Network (VPN)

**A virtual private network is not necessarily an encrypted tunnel. It is simply a point-to-point connection between two hosts that allows them to communicate.**

Secure communications can, of course, be provided by the VPN, but only if the security protocols have been selected and correctly configured to provide a trusted path over an untrusted network, such as the internet. 

Remote users employ VPNs to access their organization's network, and depending on the VPN's implementation, they may have most of the same resources available to them as if they were physically at the office.

> Having water overhead in a data center is not advised, because eventually water pipes will fail and leak on equipment. The risk can be reduced somewhat by using a dry-pipe system that keeps the water out of the pipes over the data center.

#### Virtual Local Area Network

**Virtual Local Area Networks (VLANs)** allow network administrators to use switches to create a software-based LAN segments, which can segregate or consolidate traffic across multiple switch ports.

Devices that share a VLN communicate through switches as if they were on the same Layer 2 network. The image below shows different VLANs --red, green and blue, connecting separate sets of ports together, while sharing the same network segment consisting of the two switches and their connection. 

Since VLANs act as discrete networks, communications between VLANs must be enabled. Broadcast traffic is limited to the VLAN, reducing congestion and reducing the effectiveness of some attacks.

Administration of the environment is simplified, as the VLANs can be reconfigured when individuals change their physical location or need access to different services. VLANs can be configured based on switch port, IP subnet, MAC address and protocols. 

VLANs do not guarantee a network's security. At first glance, it may seem that traffic cannot be intercepted because communication within a VLAN is restricted to member devices. 
- However, there are attacks that allow a malicious user to see traffic from other VLANs (so-called "VLAN hopping"). THE VLAN technology is only one tool that can improve the overall security of the network environment. 

#### Security of the Network

>TCP/IP's vulnerabilities are numerous. Improperly implemented TCP/IP stacks in various operating systems are vulnerable to various DoS/DDoS attacks, fragment attacks, oversized packet attacks, spoofing attacks, and man-in-the middle attacks. 

TCP/IP (as well as most protocols) is also subject to passive attacks via monitoring or sniffing. Network monitoring, or sniffing, is the act of monitoring traffic patterns to obtain information about a network. 

#### Service Model

Some cloud-based services only provide data storage and access. When storing data in the cloud, organizations must ensure that security controls are in place to prevent unauthorized access to the data.

There are varying levels of responsibility for assets depending on service model. This includes maintaining the assets, ensuring they remain functional, and keeping the systems and applications up to date with current patches.

In some cases, the cloud service provider is responsible for these steps, in other cases, the consumer is responsible. 
- Types of cloud computing service models include Software as a Service (SaaS), Platform as a Service (PaaS), Infrastructure as a Service (IaaS)

#### Managed Service Providers

> Managed service providers are companies that manage information technology assets for another company. 

Small and medium sized businesses commonly outsource part or all of their information technology functions to an MSP to manage day to day operations or to provide expertise in areas the company does not have.

**Managed Detection and Response** a service where a vendor monitors firewall and other security tools to provide expertise in triaging events. 

#### Cloud Characteristics

Cloud-based assets include any resources that an organization accesses using cloud computing. Cloud computing refers to on-demand access to computing resources available from almost anywhere, and cloud computing resources are highly available and easily scalable. 

**Cloud Computing has many benefits for organizations, which include but are not limited to:**

- Usage is metered and priced according to units (or instances) consumed. This can also be billed back to specific departments or functions.
- Reduced cost of ownership. There is no need to buy any assets for everyday use, no loss of asset value over time and a reduction of other related costs of maintenance and support.
- Reduced energy and cooling costs, along with "green IT" environment with optimum use of IT resources and systems
- Allows an enterprise to scale up new software or data-based services/solutions through cloud systems quickly and without having to install massive hardware locally.

#### Cloud Computing

**Cloud computing is usually associated with an internet based set of computing resources, any typically sold as a service provided by a CSP.**

> Cloud computing is similar to the electrical or power grid. It is provisioned in a geographic location and is sourced using an electrical means this is not necessarily obvious to the consumer. 
- Cloud computing is scalable, elastic, and easy-to-use for the provisioning and deployment of IT services.

NIST defines cloud computing as:

*A model for enabling ubiquitous, convenient, on-demand network access to a shared pool of configurable computing resources (such as networks, servers, storage, applications, and services) that can be rapidly provisioned and released with minimal management effort or service provider interaction.*

#### Service-Level Agreement

The cloud computing service level agreement is an agreement between a cloud service provider and a cloud service customer based on a taxonomy of cloud computing specific terms to set the quality of cloud computing specific terms to set the quality of the cloud services delivered. 

Think of a rule book and legal contract, that combination is what you have in a service level agreement. 
- Let us not downplay the importance of this document/agreement. In it, the minimum level of service, availability, security, controls, processes, comms, support and many other crucial business elements. 

The purpose of an SLA is to document specific parameters, minimum service levels, and remedies for any failure to meet the specified requirements. It should also affirm data ownership and specify data return and destruction details.

>Other SLA points to consider:

- Cloud system infrastructure details and security standards
- Customer right to audit legal and regulatory compliance by the CSP
- Rights and costs associated with continuing and discontinuing service use
- Service availability
- Service performance
- Data security and privacy
- Disaster recovery processes 
- Data location
- Data access
- Data portability
- Problem identification and resolution expectations
- Change management processes
- Dispute mediation processes
- Exit strategy

#### Memorandum of Understanding (MOU) Memorandum of Agreement (MOA)

Some organizations seeking to minimize downtime to enhance BC (business continuity) and DR (disaster recovery) capabilities will create agreements with other, similar organizations. They agree that if one of the parties experiences and emergency and cannot operate within their own facility, the other party will share its resources and let them operate within their own facility, the other party will share it's resources and let them operate within theirs to maintain critical functions. 

These agreements often include competitors, because their facilities and resources meet the needs of their particular industry. 

> The difference between an MOA or MOU and an SLA is that an MOU is more directly related to what can be done with a system or information. 
- A service-level agreement goes down to the granular level. For example, if you are outsourcing the new IT services, then you will need two full-time technicians readily available, at least from Monday though Friday during business hours.

**We must be cautious when outsourcing cloud-based services, because we must understand exactly what we are agreeing to.**

- If the SLA promises 100% accessibility to information, is the access directly to you at the moment, or is it access to their website through their portal when they open on Monday?

#### Network Design

The objective of network design is to satisfy data communication requirements and achieve the result of efficient overall performance. 

**Network Segmentation**

- Network segmentation involves controlling traffic among networked devices. Complete or physical network segmentation occurs when a network is isolated form all outside communications, so transactions can only occur between devices within the segmented network. 

**Demilitarized Zone**

- A DMZ is a network area that is designed to be accessed by outside visitors but is still isolated from the private network of the organization. The DMZ is often the host of public web, email, file and other resource servers. 

**Virtual Local Area Network**

- VLANS are created by switches to logically segment a network without altering its physical topology.

**Virtual Private Network**

- A virtual private network (VPN) is a communication tunnel that provides a point-to-point transmission of both authentication and data traffic over an untrusted network.

**Defense in Depth**

- Defense in depth uses multiple types of access control in literal or theoretical layers to help an organization avoid a monolithic security stance.

**Network Access Control (NAC)**

- Network access control (NAC) is a concept of controlling access to an environment through strict adherence to an implementation of security policy.

#### Types of Threats

**There are many types of cyber threats to organizations. Below, we look at several of the most common types.**

**Spoofing**

> This is an attack with the goal of gaining access to a target system through the use of a falsified identity.
- Spoofing can be used against IP addresses, MAC addresses, usernames, system names, wireless network SSIDs, email addresses and many other types of logical identification.

**Phishing**

>An attack that attempts to misdirect legitimate users to malicious websites through the abuse of URLs or hyperlinks in emails could be considered phishing.

**DoS/DDoS**

> A denial of service (DoS) attack is a network resource consumption attack that has the primary goal of preventing legitimate activity on a victimized system. Attacks involving numerous unsuspecting secondary victim systems are known as distributed denial-of-service attacks. (DDoS)

**Virus**

> The computer virus is perhaps the earliest form of malicious code to plague security administrators. As with biological viruses, computer viruses have two main functions -- propagation and destruction.

- A virus is a self-replicating piece of code that spreads without the consent of the user, but frequently with their assistance.

**Worm**

> Worms pose a significant risk to network security. They contain the same destructive potential as other malicious code objects with an added twist -- they propagate themselves without requiring any human intervention. 

**Trojan**

> Software program that appears benevolent but carries a malicious, behind the scenes payload that has the potential to wreak havoc on a system or network. 

**On-Path Attack**

> Attackers place themselves between two devices, often between a web browser and a web server, to intercept or modify information that is intended for one or both of the endpoints. 

- On-path attacks are also known as man-in-the-middle attacks.

**Side-Channel**

> A side channel attack is a passive, non-invasive attack to observe the operation of a device. Methods include power monitoring, timing and fault analysis attacks.

**Advanced Persistent Threat**

> APTs refer to threats that demonstrate an unusually high level of technical and operational sophistication spanning months or even years. 

- APT attacks are often conducted by highly organized groups of hackers. 

**Insider Threat**

> Insider threats are threats that arise from individuals who are trusted by the organization. These could be disgruntled employees or employees involved in espionage. 

- Insider threats are not always willing participants. 
- A trusted user who falls victim to a scam could be an unwilling insider threat.

**Malware**

>A program that is inserted into a system, usually covertly, with the intent of compromising the confidentiality, integrity or availability of the victim's data, applications or operating system or otherwise annoying or disrupting the victim.

**Ransomware**

> Malware used for the purpose of facilitating a ransom attack. Ransomware attacks often use the cryptography to "lock" the files on an affected computer and require the payment of a ransom fee in return for the "unlock" code.

#### Network Access Control

> At it's simplest form, Network Access Control (NAC) is a way to prevent unwanted devices from connecting to a network.
> 	Some NAC systems allow for the installation of required software on the end user's device to enforce device compliance to policy prior to connecting.

These systems use VLANs to control whether devices connect to the corporate network or to a guest network. Even though a wireless access control may attach to a single port on a physical network switch, the VLAN associated with the device connection on the wireless access controller determines the VLAN that the device operates on and to which networks it is allowed to connect. 

#### Ports and Protocols

**There are physical ports that you connect wires to and logical ports that determine where the data/traffic goes.**

**Physical Ports**

> Physical ports are ports on the routers, switches, servers, computers, etc. to which you connect the wires (e.g. fiber-optic cables, Cat5 cables) to create a network.

**Logical Ports**

> When a communication connect is established between two systems, it is done using ports. A logical port (also called a socket) is little more than an address number that both ends of the communication link agree to use when transferring data.

- Ports allow a single IP address to support multiple simultaneous network connections, each using a different port number. In the application layer of the TCP/IP model, which includes the sessions, presentation and application layers of the OSI Model, resides numerous application - or service - specific protocols. Data types are mapped using port numbers associated with services. 

For example, web traffic (or HTTP) is Port 80. Secure Web Traffic (HTTPS) is port 443.

*Well-Known Ports (0-1023)*
- These ports are related to the common protocols that are at the core of the Transport Control Protocol/Internet Protocol, DNS, SMTP, etc.
*Registered Ports(1014-49151)*
- These ports are often associated with proprietary applications from vendors and developers.
*Dynamic or Private Ports (49152-65535)*
- Whenever a service is requested that is associated with well-known or registered ports, those services will respond with a dynamic port that is used for that session and then released.

#### Networking Models

> Using different models, architectures and standards exist that provide ways to interconnect different hardware and software systems with each other for the purposes of sharing information, coordinating their activities, and accomplishing joint or shared tasks.

**Computers and networks emerge from the integration of communication devices, storage devices, processing devices, security devices, input devices, output devices, operating systems, software, services and people.**

The purpose of all communications is to exchange information and ideas between people and organizations so that they can get work done. 

Those goals can be re-expressed in network and security terms:

- Provide reliable, managed communications between hosts and users
- Isolate functions in layers
- Use packets as the basis of communication
- Standardize routing, addressing and control.
- Allow layers beyond internetworking to add functionality.
- Be vendor-agnostic, scalable and resilient.

Network Model:

1. Physical
2. Data Link
3. Network
4. Transport
5. Session
6. Presentation
7. Application

**Upper Layer:**

Known as the host or application layer. 
- Responsible for managing the integrity of a connection and controlling the session as well as establishing, maintaining and terminating communication sessions between two computers. 

**Lower Layer:**

Referred to as the media or transport layer and is responsible for receiving bits from the physical connection medium and converting them into a frame.
- Frames are grouped into standardized sizes.
- Think of frames as a bucket and the bits as water.

#### Transmission Control Protocol/Internet Protocol

> The OSI Model wasn't the first or only attempt to streamline networking protocols or establish a common communications standard. 

- In fact, the most widely used today, TCP/IP, was developed in the early 1970s. The OSI Model was not developed until the late 1970s. 
- The TCP/IP protocol stack focuses on the core function of networking.

| TCP/IP Protocol Architecture Layers |                                                |
| ----------------------------------- | ---------------------------------------------- |
| Application Layer                   | Defines the protocols for the transport layer. |
| Transport Layer                     | Permits data to move among devices             |
| Internet Layer                      | Creates/Inserts packets                        |
| Network Interface Layer             | How data moves through the network             |
> TCP/IP is a platform independent protocol based on open standards.

*TCP/IP is available in just about every operating system, but it consumes a significant amount of resources and is relatively easy to hack into because it was designed for ease of use rather than for security.*

#### Segmentation for Embedded Systems and IoT

> An embedded system is a computer implemented as part of a larger system. The embedded system is typically designed around a limited set of specific functions in relation to the larger product of which it is a component.

* Examples of embedded systems include network attached printers, smart TVs, HVAC controls, smart appliances, smart thermostats and medical devices.
* Network enabled devices are any type of portable or non-portable device that has native network capabilities. This generally assumes the network in question is a wireless type of network typically provides by a mobile telecommunications company.

*The Internet of Things* is the collection of devices that can communicate over the internet with one another or with a control console to affect and monitor the real world. 

- IoT devices might be labeled as smart devices or smart-home equipment. Many of the ideas of industrial environmental control found in office buildings are finding their way into more consumer-available solutions for small offices or personal homes.

- Network segmentation can be used to isolate IoT devices from the broader internet

#### On-Premises Data Centers

> When it comes to data centers, there are two primary options: organizations can outsource the data center or own the data center. 
> 	If the data center is owned, it will likely be built on premises. A place, like a building for the data center is needed, along with power, HVAC, fire suppression, and redundancy.

1. **Data Center/Closets**
		The facility wiring infrastructure is integral to overall information system security and reliability.
		Protecting access to the physical layer of the network is important in minimizing intentional or unintentional damage. Proper protection of the physical suite must address these sorts of security challenges. 

2. **Heating, Ventilation and Air Conditioning (HVAC) / Environmental**
		High-density equipment and equipment within enclosed spaces requires adequate cooling and airflow. Well-established standards for the operation of computer equipment exist, and equipment is tested against these standards. 
		For example, the recommended range for optimized maximum uptime and hardware life is from 64 to 81 degrees and it is recommended that a rack have three temperature sensors, positioned at the top, middle and bottom of the rack, to measure the actual operating temperature of the environment. 
		Monitoring for dust, noxious fumes, water or gas leaks, sewer overflow or HVAC failure should be built into the building control environment.

3. **Power**
		Data centers and information systems in general consume a tremendous amount of power, which needs to be delivered both constantly and consistently.
			Fluctuations in power quality affect the system lifespan
		Backup generators must be sized to provide for the critical load (the computing resources) and the supporting infrastructure. 
		
1. **Fire Suppression**
		For server rooms, appropriate fire suppression/detection must be considered based on the size of the room, typical human occupation, egress routes, and risk of damage to equipment.
		Water used for fire suppression would cause more harm to servers and other electronic components. 
		Gas-based fire suppression systems are better for the equipment, but harmful to humans. 

#### Open Systems Interconnected Model

> *The OSI Model was developed to establish a common way to describe the communication structure for interconnected computer systems.*

**The OSI model serves as an abstract framework, or theoretical model, for how protocols should function in an ideal world, on ideal hardware.**

- Thus, the OSI model has become a common conceptual reference that is used to understand the communication of various hierarchical components from software interfaces to physical hardware.

OSI Model divides networking tasks into seven distinct layers. Each layer is responsible for performing specific tasks or operations with the goal of supporting data exchange (in other words, network communication) between two computers. The layers are interchangeably referenced by name or layer number.

- Each layer communicates directly with the layer above it and the layer below it.
- Each layer has the ability to perform **encapsulation.**

**Encapsulation** is the addition of header and possibly footer data by a protocol used at that layer of the OSI Model. 
- Encapsulation is particularly important when discussing transport, network and data link layers.

*When someone references an image file like a JPEG or PNG, they are talking about the presentation layer.*

*When discussing logical ports such as NetBIOS, we are discussing the session layer.*

*When discussing TCP/UDP, we are discussing the transport layer*

*When discussing routers that are sending packets, we are discussing the network layer*

*When discussing switches, bridges, or WAPs sending frames, we are discussing the data link layer.*

> Encapsulation occurs as the data moves down the OSI Model from application to physical. As data is encapsulated at each descending layer, the previous layer's header, payload and footer are all treated as the next layer's payload. 

The data unit size increases as we move down the conceptual model and the contents continue to encapsulate.

> The inverse occurs as data moves up the OSI model layers from physical to application. This process is known as **de-encapsulation** or decapsulation. The header and footer are used to properly interrupt the data payload and are then discarded. As we move up the OSI model, the data unit becomes smaller.

#### Network Access Control

> An organization's network is perhaps one of its most critical assets. As such, it is vital that you both know and control access to it, both from insiders (e.g. employees, contractors) and outsiders (customers, corporate partners, vendors). You must see who and what is attempting to make a network connection.

**At one time, network access was limited to internal devices. Gradually, that was extended to remote connections, although initially those were the exceptions rather than the norm. This started to change with the concepts of bring your own device (BYOD) and Internet of Things (IoT)**

*The organization's access control policies and associated security policies should be enforced via the NAC devices.*
- An access control device only enforces a policy, it doesn't create one.

>The NAC device will provide the network visibility needed for access security and may later be used for incident response. Aside from identifying connections, it should also provide isolation for noncompliant devices within a quarantined network and provide a mechanism to "fix" the noncompliant elements, such as turning on endpoint protection. 

**Some possible use cases for NAC deployment:**
- Medical devices
- IoT devices
- BYOD/mobile devices
- Guest users and contractors

All mobile devices, regardless of owner, should go through an onboarding process, ideally each time a network connection is made, and that the device is identified and interrogated to ensure the organization's policies are met.

#### Deployment Models

**The four cloud deployment models are *public, private, hybrid and community.***

**Public**

Public clouds are commonly referred to as cloud for the public user. It is easy to access a public cloud.

There is no real mechanism, other than applying for and paying for the cloud service.

A public cloud model includes assets available for any consumers to rent or lease and is hosted by an external cloud service provider.

**Private**

Generally are developed and deployed for a private organization that builds its own cloud.

Includes cloud based assets for a single organization, meaning that organization is responsible for all maintenance.

Private clouds provide organizations and their departments private access to the computing, storage, networking and software assets that are available in the private cloud.

**Hybrid**

A hybrid cloud deployment model is created by combining two forms of cloud computing deployment models, typically a public and private cloud. Hybrid cloud computing is gaining popularity with organizations by providing them with the ability to retain control of their IT environments, conventiely allowing them to use public cloud service to fill non-mission critical workloads, and taking advantage of flexibility, scalability and cost savings.

**Community**

Can either be public or private. 

What makes them unique is that they are generally developed for a particular community. An example could be a public community focused primarily on organic food, or maybe a community cloud focused on financial services.

#### Zero Trust

> Zero trust networks are often microsegmented networks, with firewalls at nearly every connecting point. Zero Trust encapsulates information assets, the services that apply to them, and their security properties.

Placing a greater number of firewalls or other security boundary control devices throughout a network increases the number of opportunities to detect a troublemaker before harm is done.

Many enterprise architectures are pushing to this extreme of microsegmenting their internal networks, which enforces frequent reauthentication of a user ID, as depicted in this image.

> Zero trust is an evolving design approach that recognizes even the most robust access control systems have their weaknesses. It addes defenses at the user, asset and data level, rather than relying on perimeter defense.

#### Defense in Depth

> Uses a layered approach when designing the security posture of an organization.

Using many layers of defense will encourage attackers to focus on other, easier targets.

**Here are some examples that further explain the concept of defense in depth:**

**Data:** Controls that protect the actual data with technologies such as encryption, data leak prevention, identity and access management and data controls.

**Application:** Controls that protect the application with technologies such as data leak prevention, application firewalls and database monitors.

**Host:** Every control that is placed at the endpoint level, such as antivirus, endpoint firewall, configuration, and patch management.

**Internal Network:** Controls that are in place to protect uncontrolled data flow and user access across the organizational network. Relevent technologies include intrusion detection systems, intrusion prevention systems, internal firewalls and network access controls.

**Perimeter:** Controls that protect against unauthorized access to the network. This level includes the use of technologies such as gateway firewalls, honeypots, malware analysis and secure DMZs

**Physical:** Controls that provide a physical barrier, such as locks, walls or access control.

**Policies, procedures and awareness:** Administrative controls that reduce insider threats (intentional and unintentional) and identify risks as soon as they appear.

#### Secure Ports 

> Some network protocols transmit information in clear text, meaning it is not encrypted and should not be used. 
> 	Clear text information is subject to network sniffing. 
> 	This tactic uses software to inspect packets of data as they travel across the network and extract text such as usernames and passwords.

Network sniffing could also reveal the content of documents and other files if they are sent via insecure protocols. The table below shows some of the insecure protocols along with recommended secure alternatives.


| Insecure Port | Description                                                                                                                                                                                                                                                     | Protocol                              | Secure Alternative Port | Protocol                                     |
| ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------- | ----------------------- | -------------------------------------------- |
| 21-FTP        | File Transfer Protocol, sends the username and password using plaintext from the client to the server. This could be intercepted by an attacker and later used.                                                                                                 | File Transfer Protocol                | 22-SFTP                 | Secure File Transfer Protocol                |
| 23-Telnet     | Used by many Linux systems and any other systems as a basic text-based terminal. All information to and from the host on a telnet connection is sent in plaintext and can be intercepted.                                                                       | Telnet                                | 22-SSH                  | Secure Shell                                 |
| 25-SMTP       | Default unencrypted port for sending mail messages. Data contained within can be discovered via packet sniffing.                                                                                                                                                | Simple Mail Transfer Protocol         | 587-SMTP                | SMTP with TLS                                |
| 37-Time       | May be used by legacy equipment and has mostly been replaced by using port 123 for Network Time Protocol (NTP).                                                                                                                                                 | Time Protocol                         | 123-NTP                 | Network Time Protocol                        |
| 53-DNS        | Still widely used, using DNS over TLS protects DNS information from being modified in transit.                                                                                                                                                                  | Domain Name Service                   | 853-DoT                 | DNS over TLS (DoT)                           |
| 80-HTTP       | The basis for nearly all web browser traffic on the internet. Information sent via HTTP is not encrypted and is susceptible to sniffing attacks. HTTP using TLS encryption is preferred, as it protects the data in transit between the server and the browser. | HyperText Transfer Protocol           | 443-HTTPS               | HyperText Transfer Protocol (SSL/TLS)        |
| 143-IMAP      | Protocol used for retrieving emails. IMAP traffic on port 143 is not encrypted and is vulnerable to packet sniffing.                                                                                                                                            | Internet Message Access Protocol      | 993-IMAP                | IMAP for SSL/TLS                             |
| 161/162 SNMP  | Commonly used to send and receive data used for managing infrastructure devices. Since sensitive info is usually contained in these messages, it is recommended to use SNMP ver 2 or 3 to include encryption                                                    | Simple Network Management Protocol    | 161/162 SNMP            | SNMPv3                                       |
| 445-SMB       | Used by many versions of Windows for accessing files over the network. Files are transmitted unencrypted, and many vulnerabilities are well-known. Therefore, traffic on Port 445 should not be allowed to pass through a firewall at the network perimeter.    | Server Message Block                  | 2049-NFS                | Network File System                          |
| 389-LDAP      | Used to communicate directory information from servers to clients. This can be an address book for email or usernames for logins. Because it is not encrypted, it is vulnerable to packet sniffing.                                                             | Lightweight Directory Access Protocol | 636-LDAPS               | Lightweight Directory Access Protocol Secure |
# Domain 5: Security Operations

#### Data Handling

**Data goes through its own lifecycle as users create, utilize, share and modify it. Many different models of the life of a data item can be found, but they all have some basic operational steps in common.**

The data security lifecycle model is useful because it can align easily with the different roles that people and organizations perform during the evolution of data from creation to destruction (or disposal)

It also helps put the different data states of in use, at rest and in motion, into context. Let's take a closer look.

> All ideas, data, information, or knowledge can be thought of as performing six major sets of activities throughout its lifetime. Conceptually, these involve:

- **Create**
	- Creating the knowledge, which is usually tacit knowledge at this point.
- **Store**
	- Storing or recording it in some fashion that makes it explicit.
- **Use**
	- Using the knowledge, which may cause information to be modified, supplemented, or partially deleted.
- **Share**
	- Sharing the data with other users, whether as a copy or by moving the data from one location to another.
- **Archive**
	- Archiving the data when it is temporarily not needed.
- **Destroy**
	- Destroying the data when it is no longer needed.

#### Encryption Overview

> Almost every action we take in our modern digital world involves cryptography. Encryption protects our personal and business transactions; digitally signed software updates verify their creator's or supplier's claim to authenticity. 

Digitally signed contracts, binding to all parties, are routinely exchanged via email without fear of being repudiated later by the sender. 

Cryptography is used to protect information by keeping its meaning or content secret and making it unintelligible to someone who does not have a way to decrypt that protected information.

**Confidentiality**

>Cryptography provides confidentiality by hiding or obscuring a message so that it cannot be understood by anyone except the intended recipient. Confidentiality keeps information secret from those who are not authorized to have it.

**Integrity**

> Hash functions and digital signatures can provide integrity services that allow a recipient to verify that a message has not been altered by malice or error. These include simple message integrity controls. Any changes made by the sender or the recipient, either deliberate or accidental, will result in two different results.

**Plaintext**

**Plaintext** is the data or message in its normal, unencrypted form and format. Its meaning or value to an end user (a person or process) is immediately available for use.

Plaintext can be:

- Image, audio or video files in their raw or compressed forms.
- Human-readable text and numeric data, with or without markup language elements for formatting and metadata
- Database files or records and fields within a database
- Anything else that can be represented in digital form for computer processing, transmission and storage.

#### Security Awareness Training

**The purpose of awareness training is to make sure everyone knows what is expected of them, based on responsibilities and accountabilities, and to find out whether there is any carelessness or complacency that may pose a risk to the organization.**

What is security awareness training?

*Education*: The overall goal of education is to help learners improve their understanding of these ideas and their ability to relate them to their own experiences and apply that learning in useful ways.

*Training*: Focuses on building proficiency in a specific set of skills or actions, including sharpening the perception and judgment needed to make decisions as to which skill to use, when to use it and how to apply it. Training can focus on low-level skills, an entire task, or complex workflows consisting of many tasks.

*Awareness*: These are activities that attract and engage the learner's attention by acquainting them with aspects of an issue, concern, problem or need.

#### Data Security Event Example

> Information security is not something that is plugged in as needed. You can have some patching on a system that already exists, such as updates, but if you don't have a secure system, you can't just plug something in to protect it.

#### Common Security Policies Deeper Dive

> Policies will need to be set according to the needs of the organization and its vision and mission. Each of these policies should have a penalty or consequence attached in case of noncompliance.

The first time may be a warning; the next might be a forced leave of absence or suspension without pay, and critical violation could even result in an employee's termination.

All of this should be outlined clearly during onboarding, particularly for information security personnel. It should be made clear who is responsible for enforcing these policies, and the employee must sign off on them and have documentation saying they have done so.

**Any Security or Data Handling procedures should be backed up by appropriate policies.**

#### Phishing

**The use of Phishing attacks to target individuals, entire departments, and even companies is a significant threat that the security professional needs to be aware of and prepared to defend against.**

- Countless variations on the basic phishing attack have been developed in recent years, leading to a variety of attacks that are deployed relentlessly against individuals and networks in a never-ending stream of emails, phone calls, spam, instant messages, videos, file attachments, and other delivery mechanisms.
- Phishing attacks that attempt to trick highly placed officials or private individuals with sizable assets into authorizing large fund wire transfers to previously unknown entities are known as **whaling attacks.**

#### Password Protection

**We all use multiple passwords and systems. Many password managers store passwords so that a user does not have to remember all their security code for multiple systems.**

> The greatest disadvantage of these solutions is the risk of compromise of the password manager.

These password managers may be protected by a weak password or passphrase chosen by the user and easily compromised. 

Organizations should encourage the use of different passwords for different systems and should provide a recommended password management solution for its users.

**Examples of poor password protection that should be avoided are:**

- Reusing passwords for multiple systems, especially using the same password for business and personal use.
- Writing down passwords and leaving them in unsecured areas.
- Sharing a password with tech support or a coworker.

#### Hashing Deep Dive

**No matter how long the input is, the hash digest will be the same number of characters.**

Any minor change in the input, a misspelling or an upper-case or lower-case error, will create a completely different hash digest. So you can use the hash digest to confirm that the input exactly matches what is expected or required, for instance, a password.

> Before we go live with a software product provided by a third party, for instance, we have to make sure no one has changed anything since it was tested by you and the programmer.  They will usually send you the digest of their code and you compare that to the original. This is also known as a checksum.

- If you see a discrepancy, that means something has changed. THen the security coders will compare the original one and the new one, and sometimes it's very tedious, but they have software that can do it for them. 

#### Change Management Components

**The change management process includes the following components**

**Documentation**

All of the major change management practices address a common set of core activities that start with a request for change (RFC) and move through various development and test stages until the change is released to the end users. 

From first step to last, each step is subject to some form of formalized change management and decision making; each step produces accounting or log entries to document its results. 

**Approval**

These processes typically include: Evaluating the RFCs for completeness, assignment to the proper change authorization process based on risk and organizational practices, stakeholder reviews, resource identification and allocation, appropriate approvals or rejections, and documentation of approval or rejection.

**Rollback**

Depending on the nature of the change, a variety of activities may need to be completed. These generally include: scheduling the change, testing the change, verifying the rollback procedures, implementing the change, evaluating for proper and effective operation, and documenting the change in the production environment.

- Rollback authority would generally be defined in the rollback plan, which might be immediate or scheduled as a subsequent change if monitoring of the change suggests inadequate performance.

#### Logging and Monitoring Security Events

*Logging is the primary form of instrumentation that attempts to capture signals generated by events.*

> Events are any actions that take place within the systems environment and cause measurable or observable change in one or more elements or resources within the system.

Logging imposes a computational cost but is invaluable when determining accountability. Proper design of logging environments and regular log reviews remain best practices regardless of the type of computer system.

Information that may be relevant to being recorded and reviewed include, but is not limited to:

- User IDs
- System Activities
- Dates/times of key events (logon, logoff)
- Device and location identity
- Successful and rejected system and resource access attempts
- System configuration changes and system protection activation and deactivation events

> Logging and monitoring the health of the information environment is essential to identifying inefficient or improperly performing systems, detecting compromises and providing a record of how systems are used.

*Robust logging practices provide tools to effectively correlate information from diverse systems to fully understand the relationship between one activity and another.*

Log reviews are an essential function not only for security assessment and testing but also for identifying security incidents, policy violations, fraudulent activities and operation problems near the time of occurrence. 
- Log reviews support audits forensic analysis related to internal and external investigations and provide support for organizational security baselines.

Controls are implemented to protect against unauthorized changes to log information. Operational problems with the logging facility are often related to alterations to the messages that are recorded, log files being edited or deleted, and storage capacity of log file media being exceeded. 

#### Event Logging Best Practices

> Different tools are used depending on whether the risk from the attack is from traffic coming into or leaving the infrastructure

**Ingress Monitoring**

Ingress monitoring refers to surveillance and assessment of all inbound communications traffic and access attempts. Devices and tools for this include:

- Firewalls
- Gateways
- IDS/IPS tools
- SIEM Solutions
- Remote Authentication Servers
- Anti-malware solutions

**Egress Monitoring**

> Egress monitoring is used to regulate data leaving the organization's IT environment.

The term is used in conjunction with this effort is data loss prevention (DLP) or data leak protection. The DLP solution should be deployed so that it can inspect all forms of data leaving the organization, including:

- Email (content and attachments)
- Copy to portable media
- File Transfer Protocol
- Posting to web pages/websites
- Applications/application programming interfaces (APIs)

#### Symmetric Encryption

> The central characteristic of a symmetrical encryption algorithm is that it uses the same key in both the encryption and decryption process. It could be said that the decryption process is a mirror image of the encryption process.

**The same key is used for both the encryption and decryption process. This means that the two parties communicating need to share knowledge of the same key.**

This type of algorithm protects data, as a person who does not have the correct key would not be able to read the encrypted message.

- If two parties suspect a specific communication path between them is compromised, they obviously can't share key material along that path. 
- Distribution of the key is difficult, because the key cannot be sent in the same channel as the encrypted message, or the man-in-the-middle would have access to the key.
- Any party with knowledge of the key can access, and therefore change, the message.
- Each individual or group of people wishing to communicate would need to use a different key for each individual or group they want to connect with. This raises the challenge of scalability. 

**Primary uses of symmetric algorithms:**

- Encrypting bulk data (hard drives, backups, portable media)
- Encrypting messages traversing communications channels (IPsec, TLS)
- Streaming large-scale, time-sensitive data (audio/video materials, gaming)
#### Asymmetric Encryption

*Asymmetric encryption uses one key to encrypt and a different key to decrypt the input plaintext. This is in stark contrast to symmetric encryption, which uses the same key to encrypt and decrypt.*

> For security professionals, the math of asymmetric encryption can be left to the cryptanalysts and cryptographers to know. 

Note that anyone can encrypt something using the recipient's public key, but only the recipient -- with their private key -- can decrypt it. 

Asymmetric key cryptography solves the problem of key distribution by allowing a message to be sent across an untrusted medium in a secure manner without the overhead of prior key exchange or key material distribution. It also allows for several other features not readily available in symmetric cryptography, such as the non-repudiation of origin and delivery, access control, and data integrity. 

> Asymmetric key cryptography also solves the problem of scalability. It does scale well as numbers increase, as each party only requires a key pair, the private and public keys. 
> 	An organization with 100,000 employees would only need a total of 200,000 keys instead. 

> The main problem with asymmetric is that it is extremely slow compared with it's symmetric counterpart, so much so that it is considered impractical for everyday use.

**This is because asymmetric key cryptography handles much larger keys and is mathematically intensive, thereby reducing speeds significantly.**

#### Social Engineering

**Social engineering is an important part of any security awareness training program for one simple reason: bad actors know that it works.**

For cyber attackers, social engineering is an inexpensive investment with a potentially high payoff. Social engineering, applied over time, can extract significant insider knowledge about almost any organization or individual.

> Social engineering works because plays on human tendencies. Education, training and awareness work best to counter or defend against social engineering because they underscore that every person in the organization plays a role in information security. 

#### Hashing

> Hashing takes an input set of data of almost arbitrary size and returns a fixed-length result called the hash value. A hash function is the algorithm used to perform this transformation. When used with cryptographically strong hash algorithms, this is the most common method of ensuring message integrity today.

**Hashes have many uses in computing and security, one of which is to create a message digest by applying such a hash function to the plaintext body of a message.**

To be useful and secure, a cryptographic hash function must demonstrate five main properties:

1. **Useful:** it is easy to compute the hash value for any given message.
2. **Nonreversible:** It is computationally infeasible to reverse the hash process or otherwise derive the original plaintext of a message from its hash value, unlike an encryption process, for which there must be a corresponding decryption process. 
3. **Content Integrity Assurance**: It is computationally infeasable to modify a message such that reapplying the hash function will produce the original hash value. 
4. **Unique**: It is computationally infeasible to find two or more different, sensible message that hash to the same hash value.
5. **Deterministic**: The same input will always generate the same hash, when using the same hashing algorithm.

> Cryptographic hash functions have many applications in information security, including digital signatures, message authentication codes, and other forms of authentication. 

- They can also be used for fingerprinting, to pinpoint duplicate data or uniquely identify files, and as checksums to detect accidental data corruption. 
- The problem with a simple hash function like this is that it does not protect against a malicious attacker who would be able to change both the message and the hash/digest by intercepting it in transit. The general idea of a cryptographic hash function can be summarized with the following formula:

`variable data input + hashing algorithm = fixed bit size data output (digest)`

#### Configuration Management Overview

> Configuration management is a process and discipline used to ensure that the only changes made to a system are those that have been authorized and validated. 

- Both a decision making process and a set of control processes.
	- Identification
	- Baseline
	- Change Control
	- Verification & Audit

**Identification**

Baseline identification of a system and all of its components, interfaces and documentation.

**Baseline**

A security baseline is a minimum level of protection that can be used as a reference point. Baselines provide a way to ensure that updates to technology and architectures are subjected to the minimum understood and acceptable level of security requirements.

**Change Control**

An update process for requesting changes to a baseline, by means of making changes to one or more components in that baseline. A review and approval process for all changes, including updates and patches.

**Verification and Audit**

A regression and validation process, which may involve testing and analysis, to verify that nothing in the system was broken by a newly applied set of changes. An audit process can validate that currently in use baseline matches the sum total of its initial baseline plus all approved changes applied in sequence.

**Inventory**

*You can't protect what you don't know you have.*

Making an inventory, catalog, or registry of all the information assets that the organization is aware of, whether they already exist, or there's a wish list or need to create or acquire them, is the first step in any asset management process.

**Baselines** 

A commercial software product, for example, might have thousands of individual modules, processes, parameter, and initialization files or other elements. If any one of them is missing, the system cannot function correctly.

The baseline is a total inventory of all the system's components, hardware, software, data, administrative controls, documentation, and user instructions.

Once controls are in place to mitigate risks, the baselines can be referenced. All further comparisons and development are measured against the baselines.

**Updates**

Repairs, maintenance actions and updates are frequently required on almost all levels of systems elements, from the basic infrastructure of the IT architecture on up through the operating systems, applications, platforms, networks and user interfaces.
- Such modifications must be acceptance tested to verify that newly installed or repaired functionality works as required. 
- They must also be regression tested to verify that the modifications did not introduce other erroneous or unexpected behaviors in the system.

**Patches**

Patch management mostly applies to software and hardware devices that are subject to regular modification. A patch is an update, upgrade or modification to a system or component. These patches may be needed to address a vulnerability or to improve functionality. 

The challenge for security professionals is to maintain all patches, since they can come at irregular intervals from many different vendors. 
- Standards such as the PCI DSS require organizations to deploy security patches within a certain timeframe. 

Organizations should test patches before rolling them out across and entire system or network.

#### Common Security Policies

**All policies must support any regulatory and contractual obligations of the organization**

Sometimes it can be challenging to ensure the policy encompasses all requirements while remaining simple enough for users to understand. 

These are six common security-related policies that exist in most organizations:

**Data Handling Policy**

The aspect of the policy defines whether data is for use within the company, is restricted for use by only certain roles, or can be made public to anyone outside the organization. 

In addition, some data has associated legal usage definitions. The organization's policy should spell out any such restrictions or refer to the legal definitions as required. Proper data classification also helps the organization comply with pertinent laws and regulations.

**Password Policy**

Every organization should have a password policy in place that defines expectations of systems and users. 

The password policy should describe senior leadership's commitment to ensuring secure access to data, outline any standards that the organization has selected for password formulation, and identify who is designated to enforce and validate the policy.

**Acceptable Use Policy**

The acceptable use policy defines acceptable use of the organization's network and compter systems and can help protect the organization from legal action.

It should detail the appropriate and approved usage of the organization's assets, including the IT environment, devices and data. 
- Each employee should be required to sign a copy of the AUP, preferably in the presence of another employee of the organization, and both parties should keep a copy of the signed AUP.

Policy aspects commonly included in AUPs:

- Data access
- System access
- Data disclosure
- Passwords
- Data retention
- Internet usage
- Company device usage

**Bring Your own Device Policy (BYOD)**

An organization may allow workers to acquire equipment of their choosing and use personally owned equipment for business use. This is sometimes called bring your own device (BYOD). 

BYOD raises a lot of security concerns for organizations, but raises overall employee morale. 

All employees should read and agree to the policy before any access to the network, systems or data is allowed.

**Privacy Policy**

It is imperative that the organization documents that the personnel understand and acknowledge the organization's policies and procedures for handling that type of information and are made aware of the legal repercussions of improper protection. 
- This is similar to the AUP but is specific to privacy-related data

The organization's privacy policy should stipulate which information is considered PII/ePHI, the appropriate handling procedures and mechanisms used by the organization, how the user is expected to perform in accordance with the stated policy and procedures, any enforcement mechanisms and punitive measures for failure to comply, as well as references to applicable regulations and legislation to which the organization is subject. 

**Change Management Policy**

Change management is the discipline of transitioning from the current state to a future state.

It consists of three major activities:

1. Deciding to change
2. Making the change
3. Confirming that the change has been correctly accomplished

Change management requires a process to implement the necessary changes so they do not adversely affect business operations.

#### Data Handling Practices

> Data has value and must be handled appropriately.

We will explore the basics of classifying and labeling data to ensure it is treated and controlled in a manner consistent with the sensitivity of the data.

**Classification**

Businesses recognize that information has value and others might steal their advantage if the information is not kept confidential, so they classify it. 

These classifications dictate rules and restrictions about how that information can be used, stored, or shared with others. All of this is done to keep the temporary value and importance of that information from leaking away. 

**This is our first definition:** Classification is the process of recognizing the organizational impacts if the information suffers any security compromises related to its characteristics of confidentiality, integrity and availability. 

> Classifications are derived from laws, regulations, contract-specific standards, or other business expectations.

**Labeling**

> Security labels are part of implementing controls to protect classified information. It is reasonable to want a simple way of assigning a level of sensitivity to a data asset, such that the higher the level, the greater the presumed harm to the organization, and thus the greater security protection the data asset requires.

Typically, two or three classifications are manageable, and more than four tend to be difficult.

- **Highly restricted:** Compromise of data with this sensitivity label could possibly put the organization's future existence at risk. Could lead to potential loss of life, injury or property damage, and litigation and claims would follow.
- **Moderately restricted:** Compromise of data with this sensitivity label could lead to loss of temporary competitive advantage, loss of revenue or disruption of planned investments or activities.
- **Low sensitivity:** compromise of data with this sensitivity label could cause minor disruptions, delays or impacts
- **Unrestricted public data:** as this data is already published, no harm can come from further dissemination or disclosure.

**Retention**

>Information and data should be kept only for as long as it is beneficial, no more and no less.
>	For various types of data, certain industry standards, laws and regulations can define retention periods.
>	When such external requirements are not set, it is an organization's responsibility to define and implement its own data retention policy. 

Security professionals should ensure that data destruction is performed when an asset has reached its retention limit. For the security professional to succeed in this assignment, an accurate inventory must be maintained, including the asset location, retention period requirement, and destruction requirements. 

Records retention policies indicate how long an organization is required to maintain information and assets. Policies should guarantee that:

- Personnel understand the various retention requirements for data of different types throughout the organization.
- The organization appropriately documents the retention requirements for each type of information
- The systems, processes and individuals of the organization retain information in accordance with the required schedule but no longer.

> A common mistake in records retention is applying the longest retention period to all types of information in an organization. This not only wastes storage but also increases risk of data exposure and adds unnecessary "noise" when searching or processing information of relevant records.

**Destruction:** 

>Data that might be left on media after deleting is known as remanence and may be a significant security concern. 

This can be removed through a series of means:

- Clearing the device or system, which usually involves writing multiple patterns of random values throughout all storage media such as main memory, registers and fixed disks. This is sometimes called *overwriting* or *zeroing* the system, although writing zeros has the risk that missed block or storage extent may still contain recoverable, sensitive information after the process is completed.
- Purging the device or system, which eliminates, or greatly reduces, the change that residual physical effects from the writing of the original data values may still be recovered, even after the system is cleared. 
	- Some magnetic disk storage technologies, for example, can still have residual "ghosts" of data on their surfaces even after being overwritten multiple times. Magnetic media, for example, can often be altered sufficiently to meet security requirements.
- Physical destruction of the device or system is the ultimate remedy to data remanence. Magnetic or optical disks and some flash drive technologies may require being mechanically shredded, chopped or broken up, etched in acid or burned; their remains may be buried in protected landfills, in some cases.

