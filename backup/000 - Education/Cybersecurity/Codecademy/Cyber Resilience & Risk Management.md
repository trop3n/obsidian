
# Cyber Resilience 

> The capability of an organization to continue to perform it’s operations, tasks, missions and objectives despite experiencing impacts from security incidents.

Why is it important?

> a cybersecurity strategy is developed with business objectives in mind. Cyber attacks are continuously rising, and CISOs can struggle to stay ahead of attackers. 

> being the target of successful cyberattacks is expensive and not sustainable. 

How to Achieve Cyber Resilience

- Redundancy of Geography, Disk, Network and Power
    
- Replication of Data through Backups
    
- Non-Persistence
    
- High Availability
    
- Restoration Order
    
- Diversity
    

  

Redundancy

> Refers to have alternate ways to maintain the availability of a resource.

> one of the ways we can achieve redundancy is by following the concept of geographic dispersal. In Cybersecurity, geographical dispersal refers to placing physical distances between the duplicate systems so the organization can avoid damages to both the primary and alternate resources from the same disaster. 

  

- Disk

- RAID: A redundant array of independent disks achieves redundancy by implementing multiple hard drives in a single resource volume. 
- Multipath: A fault-torrent implementation that provides multiple routes between CPU and storage devices.

- Network

- Load balancers distribute network traffic across multiple segments
- NIC teaming is used to increase network bandwidth by bonding two or more NICs into one.
- Power

- Uninterruptible power supply - provides non-fluctuating power to the computing devices
- A generator is temporary alternate means of power while the main power is getting restored
- Dual Power Supply means to source power from two different sources (e.g. one source could be local power supply company and a second sources could be solar)
- Managed power distribution units (PDUs) manages utilization of power remotely by the rack equipment

Replication

> having multiple copies of the same data available in multiple locations

> High availability is a concept of replication that helps us achieve Cyber Resilience.High availability refers to the assurance that a system will be available to respond to requests and complete requested operations in a timely manner. 

  

Following considerations could also assist us in increasing cyber resilience:

- SAN
    
- VM
    
- On-premises vs. Cloud
    
- Back-Up Types
    

  

Non-Persistence

> ability to maintain a systems integrity despite multiple attempts of changes by the users or attackers.

> for example, the search engine company enables theri call center employees to utilize non-persistence virtual desktop infrastructure, so every morning when they log in, a non-persistent VDI spins up a fresh VDI image.

  

Restoration Order

> refers to the sequence of mission-critical business processes that should be restored. For example, imagine your search engine company has a data center that was recently damaged by the hurricane. This data center contains chemical, mechanical, and electrical safety hazards. Thus, the first missions-critical business process of the restoration order could be to ensure the environmental health and safety of the data center. 

  

Diversity

> refers to the multilayered security mechanisms of having different types of access control provided by different entities/products.This supports cyber resiliency. Another term for this is “defense in depth”. For example, your company may want to avoid the pitfalls of only have a single security feature provided by a single brand. Instead, they use different brands of routers to establish connections among different data center sites located in different parts of the country. 

Cybersecurity Policies & Procedures

  

> In cybersecurity, Policies and Procedures refer to the documentation that define how employees should accomplish their tasks in compliance with the security policy. It often includes specific plans and procedures defining how to install and configure security components, respond to incidents and avoid incidents. 

  

Importance of Policies to Organizational Security

  

> How employees should accomplish their tasks and compliance with the security policy

> Standard operating procedures specifying how, what and where technology should be installed and configured

  

Policies are dependant on specific organizations.

  

Personnel Policies

> to build an organizational culture that values cybersecurity, it is of the utmost imprtoance that its people comply with strong personnel policies. Personnel policies are policies that mandate appropriate modification of user behaviors in order to implement proper security. The following topics could be part of the overall personnel policies. 

- Acceptable Use Policy
    
- Principle of Least Privilege
    
- Background Checks
    
- Social Media Analysis
    
- Nondisclosure Agreements (NDA)
    
- Innovate User Training
    

  

Incident Response Policy

  

> a policy that is prepared to respond to cybersecurity incidents so the organization can:

- Protect it’s systems and data
    
- Prevent disruption of its services
    

  

> done by implementing proper controls for incidents handling, reporting and monitoring, as well as incident response training, testing and assistance.

  

> standardized response process for confirmed malicious attacks. These playbooks describe the process through the IR phases defined in the National Institute of Standards and Technology (NIST) Special Publication (SP) 800-61 Rev 2 [1] Including:

- Preparation
    
- Detection and analysis
    
- Containment
    
- Eradication and recovery
    
- Post incident activities
    

Third-Party Risk Management

  

> organizations must establish a third-party risk management plan to address the cybersecurity risk involved when interacting with external entities

  

The third party risk management plan should include:

> business partners

> service-level agreements (SLA)

> memorandums of understanding (MOU) 

> business partnership agreements (BPA)

  

Business Partners

  

> must interoperability agreement: a contract that defines the terms where two entities agree to work with each other while exchanging or sharing resources. This agreement could be a preamble to an SLA or BPA.

  

Service Level Agreement 

  

> defines the service provided for a specific cost and compensation between a supplier and a customer. The SLA specifies the customer’s options for compensation in case the supplier does not fulfill their obligations or vice versa, penalties where payment is late or not made. 

  

Memorandum of Understanding (MOU)

  

> Specifies or aligns two entities’ intent to work on a common goal without legally binding them to the parameters of the memorandum. MOU is also known as a letter of intent.

  

Business Partnership Agreement (BPA)

  

> A business partnership agreement clearly define the expectations and obligations of two entities to achieve a common goal. BPA should detail dispute resolution; the decision-making process; distribution of business capital, salary or benefits and the addition or deletion of any partners. 

  

Data Policies

  

> covers the classification, governance and retention of an organization’s data.

- Classification protects data based on the need for secrecy, sensitivity or confidentiality during storing, processing or in transit. 
    
- Data governance is a collection of best practices to support the security efforts of an organization’s data. 
    
- Data retention defines a specific time frame to store, delete, destroy and/or sanitize data.
    

  

Credential Policies

  

> define the requirements for subjects to receive authentication, authorization and accounting (AAA) in order to be fully operational in an organization. Various subjects and requirements could be Personnel using Multifactor authentication; Service accounts credentials with a set expiration date; devices with unique service accounts.

  

Organizational Policies

  

> dictate security methods and requirements for the organization. These could include the following: 

- Change management
    
- Change control process
    
- Asset inventory management 
    

  

What are Security Frameworks?

  

> Provide organizations with a structure to implement their security program to keep the organizational assets safe. Some important security frameworks are:

  

> Why use the NCF Framework

- NCF provides a common language and systematic methodology
    
- NCF provides an opportunity to identify security gaps by creating profiles and implementing plans
    
- NCF’s tiers-based approach allows the individual organization to tailor their cybersecurity programs based on their mission priority, risk appetite, and budget.
    
- NCF is cost-effective not only because it is open source, but also for it’s flexibility to be customized to any security program’s needs. 
    

  

Components of the NIST Framework

  

The cybersecurity framework has 3 components: 

- Framework Core
    
- Implementation Tiers
    
- Profiles
    

  

Framework Core

  

The framework core provides desired cybersecurity activities and outcomes that are organized into functions categories, subcategories and informative references. The core could be altered to better match the business environment and needs of the organization. 

  
  
  

> The core has five functions that aid in expressing cybersecurity risk at the management level and enables decision making. 

- The identify function helps and organization prioritize its efforts based on understanding the business context, required resources to support critical functions, and related cybersecurity risks. 
    
- The Protect function provides safeguards to ensure the rendering of critical services despite cybersecurity events. 
    
- The Detect function delineates appropriate activities so we discover cybersecurity events quickly.
    
- The Respond function is comprised of actions after detecting a cybersecurity incident. 
    
- The Recover function includes acitivites that help establish normal operations after a cybersecurity incident.
    

  

Implementation Tiers

  

> measures how well-integrated cybersecurity risk decisions are into the organizations broader risk decisions. Based on their business needs, organizations can select the desired tiers. 

  

> tiers range from 1-4:

  

1. Partial
    

- Prioritization of cybersecurity efforts is not based on organizational risk objectives, business requirements, or the threat environment
    
- Organization has limited awareness of cybersecurity risk
    

  

2. Risk-Informed
    

- Priotitization of cybersecurity efforts is updated based on organizational risk objectives, business requirements or the threat environment
    
- Org has awareness of cybersecurity risk
    

3. Repeatable
    

- Prioritization of cybersecurity efforts is updated based on changes in the organizational risk objectives, business requirements, or the threat environment
    
- Org takes actions against cyber risks in the supply chain
    

4. Adaptive

-    Utilize lessons learned and predictive indicators to adapt to present cybersecurity needs
    

  

Profiles

> used to align organizational objectives, risk appetite, and resources against desired outcomes to identify gaps between the current and target operating state. Profiling allows organizations to create a prioritized implementation plan that helps them plan and budget cybersecurity improvement activities.

What is Risk?

  

> we define risk as the possibility or likelihood that a threat will pose harm or damage to an asset. 

> a threat can be defined as any potential occurence that may cause an undesirable outcome for an organization or a specific asset.

> a vulnerability is the weakness in an asset or the absence of a safeguard.

  

> risk = threat * vulnerability

  

Examples of Risk 

  

- Viruses
    
- Malicious Hackers
    
- Disgruntled employees
    
- User errors
    
- Physical damage
    
- Personnel privilege abuse
    
- Loss of data
    
- IP Theft
    
- Change or compromises to data classification or security protocols
    
- Intentional attacks
    

  

Different Types of Risk

  

- Natural disasters
    
- Physical security breaches
    
- Physical theft
    
- Equipment failure
    
- Government, political or military instrusions
    

  

Risk Management & Risk Analysis

  

> Risk management is the detailed process of identifying, analyzing, evaluating and addressing your organization's cybersecurity threats. Risk management is a key requirement of many information security standards, frameworks and laws. 

  

> At it’s core, risk assessments involve developing a list of threats, and then individual evaluating each threat and its related risk. 

  
  
  

Quantitative vs. Qualitative Risk Assessment

  

> The quantitative method generates concrete probabilities of risk. It assigns a quantity to a risk. This is not always sufficient because oftentimes risks are subjective and intangible. 

  

> Important terms in Quantitative Risk:

- Asset value: appraisal value of an org’s assets.
    
- Exposure factor: percentage of loss an organization would experience if a specific asset were violated by a realized risk.
    
- Single Loss Expectancy: cost associated with a single realized risk against a specific asset. 
    
- Annual Rate of Occurence: expected frequency with which a specific risk or threat will occur
    
- Annualized Loss Expectancy: possible yearly cost of all instances of a specific realized threat against a specific asset
    

  

Qualitative Risk analysis is more scenario based. Rather than assigning numbers and dollar figures, risks are ranked on a scale to evaluate their overall effect. The process for performing this type of analysis is often based on professional judgment, best practice and experience.

  

Regulations, Risk and Compliance

  

> Cyber Risk is interconnected with the world of legal and regulatory compliance. National, state and local governments have all passed overlapping laws regulating different components of cybersecurity. Professionals must be aware of a growing patchwork of regulations to stay ahead of threats. 

  

Laws

  

General Data Protection Regulation (GDPR)

  

California Consumer Privacy Act (CCPA)

  

Health Insurance Portability and Accountability Act (HIPAA)

  

Regulations and Frameworks

  

National Institute of Standards and Technology (NIST) Cybersecurity Framework

  

International Organization for Standardization (ISO)

  

Federal Financial Institutions Examination Council Cybersecurity Assessment Tool

  

Control Objectives for Information and Related Technology (COBIT)

Payment Card Industry Data Security Standard (PCI DSS)

  

Third Party Risk Management

  

> Many orgs outsource various aspects of their business operations. This can include security, tech support, accounting services, consulting and more. 

> Third parties need to stay in compliance with the primary organizations security posture otherwise they will present additional risks and vulnerabilities.

  

> Third Party Risk is the potential threat presented to organizations employee and customer data, financial information, operations and more from external vendors.Third parties are frequent targets for cybercriminals to conduct various attacks such as ransomware, spear-phishing and business email compromise.

  

> Some types of cybersecurity risks that occur as a result of third party risk:

- Intellectual property theft
    
- Credential theft
    
- Spear phishing
    
- Data exfiltration
    
- Network intrusion
    
- Fileless malware
    

  

Secure Configurations: User Machine Security

  

> as a cybersecurity analyst, we’ll often be considered the “last line of defense” for malicious attacks, but with proper foresight and planning, we can mitigate a majority of vulnerabilities before they become an actual risk to your IT environment.

  

Secure Configuration: No environment is completely “secure”. Attackers are always evolving to overcome your best defenses. A secure configuration follows the requirements and secure practices that we, and our IT organization, put in place, while also continuing to monitor and update over these the life of our environment. 

  

> cybersecurity analysts are in the business of risk management, and configuration management is a large part of that task.

  

> guarding against worst-case scenarios at every level of infrastructure while balancing the cost of time, effort, funding and technical availability of protection.

  
  
  
  

User Machine Security

  

> Almost everyone in your organization is going to have a desktop, laptop tablet or mobile device that can access company resources. 

  

Operating Systems

  

> Each operating system has it’s own vulnerabilities, patches and patch procedures and risk level. 

  

Automatic Patching, Updates and Application Management

> Automated patching tools like WIndows Update can force push updates to user machines, but we may need to consider implementing a process users to update their OS before accessing resources. 

  

> maintain an approved list of software, control downloads/patches of software and enforce that users stay current with software versions. 

  

Provisioning and Deprovisioning

> Provisioning is another way to say “make available”, while deprovisioning means to “make unavailable”. These terms can be applied to many concepts, such as baseline configurations, but these concepts can also be applied to user permissions. 

  

> users may unintentionally or intentionally download malicious software, introduce viruses into the system, or expose data in unintended ways. The most common way to prevent this is to limit the permissions users have on their own machines. Without admin or power user roles, users can’t install or make major changes to the OS, apps, databases networks or servers. 

  

> not all organizations will have this capability, therefore cybersecurity analysts must find other means to mitigate risks. These could include ensuring virus scanning software is installed on machines or managing group policy settings that restrict the potential impact of issues while still allowing users to effectively perform their jobs. 

  

Securing Coding Techniques

> There are numerous best practices for coding, and these evolve over time. 

- Input validation
    
- Normalization
    
- Output coding
    
- Safely storing procedures
    
- Obfuscation/camouflage (to prevent reverse engineering)
    
- Avoid code reuse/dead code
    
- Thoughtful memory management
    
- Risk-aware use of third party libraries and SDKs
    
- Avoid data exposure
    

  

Software Diversity

> using an array of tools in an environment can make it harder for an attacker to get in and inflict a large amount of damage. It may seem strange to use multiple types of software that have a similar purpose, using the same system for everything can allow hackers to more easily identify trends and vulnerabilities and exploit them. 

> Economics are always in play, but software diversity can create variety in how data flows, and introduce redundancy

  

Environment and Server Security

> In an orgs network, there are probably numerous servers. Even as many institutions move towards SaaS-based solutions they don’t host themselves, most orgs are still responsible for intranet nodes of some sort. 

> maintaining server security is very similar to desktop/end node security: we’ll need to think about operating systems, account access/permissions and identifying what apps are running on these servers.

  

Server Roles

> Servers perform different roles within an organization. Configured differently, they also introduce vastly different vulnerabilities to an intranet.

- Web servers are how users access data, and should be secured to ensure that vulnerabilities are not exploited (e.g. remote control execution)
    
- Database servers are often where crucial data is stored. Unplanned alteration could be disastrous! Similarly, file storage systems can be exposed if not properly protected via encryption and encoded URLs/scripts.
    
- Directory services are where all user accounts are stored. This is essential to secure, because if an attacker has access to directory services, they can easily impersonate valid credentials and access resources. 
    
- VPN (Virtual Private Network) software allows users to access their intranet. Most VPNs have configurations that allow admins to restrict who can access the network and many can allow or deny connections by connection string or port number.
    

  

Environment Roles

> part of ensuring the integrity of your production environment is through proper environments before deployment to production. Not all of the following environments are necessary in every IT solution, but we should be aware of and potentially support:

- Development
    
- Test/Integration
    
- QA/UA
    
- Staging
    

  

> with role based environments, most potential vulnerabilities can be mitigated well before production. Other tactics can be used to limit risk Sandboxing, baselining environments and defined integrity measurements

  

Security Automation & Scripting 

  

> To improve the security of an environment, there are proactive, reactive and real-time actions that a cybersecurity analyst can take. 

  

By the end of this article, we should understand the following:

  

- What a Red Team/Blue Team exercise is 
    
- What a Purple Team is
    
- What five concepts make up continuous activity that a cybersecurity analyst should focus on
    
- How Monitoring and Reporting are essential to reducing risk
    

  

Why Automation, Why Scripting? 

  

There are two main considerations for why automation and scripting is so important for a cybersecurity professional:

  

1. There is just too much data for a cybersecurity analyst to realistically and reliably monitor! Every cybersecurity analyst should employ automated tools that provide altering, logging, reporting and analytical feedback that they can utilize
    
2. By automating as much as possible, human error should theoretically be reduced, which means that dedicated efforts can be replicated without repeat work or effort. This includes test and verification processes that ensures the integrity of our environment. 
    

  

Simulated Attacks

  

One of the most effective ways to be as proactive as possible about cyber attacks is to actually conduct them. Red vs. Blue exercises let cyber analysts practice methods against each other to better protect against attacks. 

  

Automated Courses of Action

  

As IT environments grow, the amount of potential security risks increases - in some cases, exponentially! But even a small environment will be subject to more activity than human beings can watch, react to and resolve.

  
  
  
  

> Continuous really means continuous

- Whether automated or manual, addressing cybersecurity needs requires constant attention and evolution: whether security model is in place today can, and should, be improved upon for tomorrow. 
    

  

Five DevOps concepts that define “Continuous Activity” within CyberSec

- Continuous Monitoring: There is an infinite amount of activity going on, so a good CySec analyst will need to rely on automated monitoring tools that both alert, given the proper triggers, and log for traceability
    
- Continuous Validation: Its essential to revisit existing preventative measures to ensure the integrity of past and present implementations. Having repeatable validation testing confirms that, given the same criteria, the environment will respond in the same secure fashion at any point in time
    
- Continuous Integration: No environment is perpetually static. Our environment will have new software and hardware added to it regularly, and the CySec team must ensure every piece integrated into the IT solution follows the security standards of the organization. The easiest way to achieve this is by having an automated process that removes the possibility of human error.
    
- Continuous Delivery: Releasing the “latest and greatest” is often the main focus of many. While that is important, ensuring that anything that is released at any level (development, test, production, etc.) adheres to security standards is an essential part of the delivery process. Automating delivery allows the team to release more quickly. 
    
- Continuous Deployment: Once everything has been vetted, there’s one final step: the push to production! This is where the organizations’s real, live data will live, so here’s where everything is put to the test. By automating this process as much as possible, we’ll reinforce the idea of reducing human error in the crucial last step. 
    

  

What Are Logging and Monitoring?

  

> Logging is the act of collecting and storing information about event in a system. Every device generates events, these lists of events are called logs. 

  

> Log monitoring is the action of categorizing those events and searching the data for abnormalities that might cause problems in the system. 

  

> Due to the large amount of data, this function is usually carried out by logging/monitoring software. 

  

Security Information Event Management Tool

  

> CySec departments utilize a tool called SIEM to monitor and log their systems.

  

Some well known SIEMs are:

- Splunk Enterprise
    
- Datadog’s Security Monitor
    
- SolarWinds Security Event Manager
    
- McAfee ESM
    
- Micro Focus ArcSight
    

  

Log Management

  

> The history of a malicious user’s activities may be lost to a company if security logs are not properly managed. 

  

The NIST’s guide to Computer Security Log Management has listed criteria and procedures to aid in establishing company’s logging needs.

  

> Log management does come with challenges, and the challenges vary depending on the company’s needs. Some of the obstacles that NIST mentioned are:

- Log generation and storage
    
- Log congestion
    
- Log protection
    
- Log analysis
    

  

Public Key Infrastructure:

  

> Before we talk about what exactly PKI is, we need to talk about public-key cryptography. Public-key cryptography is a type of cryptography that uses asymmetric encryption which is a type of encryption that uses multiple keys. Public key cryptography has a private key, and a public key. Both keys can encrypt data, but the public key can only decrypt data encrypted by the private key. The public key can also not be easily derived from the private key. 

  

> Public key cryptography can create secure channels to communication, but requires an existing secure channel to exchange keys. This is the problem that PKI aims to solve. 

> PKI’s most basic purpose is to securely distribute and manage public keys. It does this using trusted third parties who verify the authenticity of public keys and then use their own private keys to digitally sign the public keys. That way, even if the key is not encrypted and has to be sent over cleartext, we will still be able to verify that the key is trusted by the third party. 

  

How does PKI Work? 

  

> PKI takes advantage of the fact that information encrypted with a private key can be decrypted by anyone with the corresponding public key. This is used to create digital certificates vouching for the authenticity of a given public key. The third parties who verify the authenticity are known as certificate authorities.

Security Culture

  

Good security culture requires three things:

- Employees need to be aware of security risks, especially common risks. 
    
- Employees need to know how to avoid insecure behavior
    
- Employees need to consider security important
    

  

> Training and education mean nothing if people do not care about applying what they’ve learned. There’s no single right way to motivate people, and it often helps to have a variety of approaches working together. 

  

> Offering financial incentives to employees who follow good security practices, applying corrective action for those who don't and leading by example are all options for encouraging people to consider security important. 

  

Security Controls

  

> What protects the confidentiality, integrity and accessibility of an asset. Security Controls can be administrative, technical or physical in nature. 

  

- Admin controls: can be policies and procedures that outline what people are supposed to do.
    
- Technical controls can be authentication, encryption, and monitoring software.
    
- Physical controls can be locked doors, security guards and fire extinguishers
    

  

Security Controls can serve different roles: 

- Preventative controls prevent unauthorized access
    
- Deterrent controls discourage unauthorized access
    
- Detective controls identify and record attempts at success
    
- Corrective control attempt to fix and incident while it is happening, and/or prevent a recurrence
    
- Compensating controls restore the function of compromised systems. 
    

  

Design for Error

  

> Systems should be designed with human error in mind.