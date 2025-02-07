#cybersecurity #educativeio 
# Introduction: Simplify Security Practices

> Learn to improve an organization's security by focusing on best practices.

"You can't build a great building on a weak foundation. You must have a solid foundation if you're going to have a strong superstructure" - Gordon B. Hinckley

## Demystify IT Security

Demystifying IT security allows us to bridge the gap between security and non-security groups so that everyone can work together to improve the organization's security posture. Focusing on easy to understand best practices can help us do this.

## Focus On Best Practices

Technical details shouldn't get in the way of practicing good security. Security doesn't need to be overly complicated. If best practices are followed, most security weaknesses can be mitigated. Most security breaches we see in the news could've been prevented with simple solutions.

# Use a Risk-Based Approach

## Overview

A risk-based approach may be the best way to clarify our goals as we move forward. Focus first on the risks to the organization. Once we come up with a list of risks, we can organize it by prioritizing different levels of severity, which helps us determine what we should focus on first.

## Risk Gathering

Some questions to ask during the risk gathering process include:

- What are the biggest threats?
- What does the organization value most?
- What kind of attack would be the most damaging to the organization?

By answering these questions, we can focus our resources on the highest priority items.

## Identify High Priority Items

If everything’s a priority, then nothing’s a priority. There’s a concept called the **defender’s dilemma**. This means that the defender has to protect all points of a system, yet an attacker only has to find one exploitable weakness to be successful. Because not all possible points of attack can be completely protected, risk management can help determine the most critical points that need to be defended. Due to resource constraints, it’s nearly impossible to fortify every aspect of an organization. Therefore, a more suitable approach is to approximate and apply controls to areas where we can gain the most benefits.

## Residual Risk

Another concept to be aware of is **residual risk**. When security controls are applied, the risk is reduced. The risk that remains after applying these controls is what we call residual risk. We should continually work to reduce residual risk.

# General Security Concepts

Learn to secure an organization by carefully introducting security measures.

## Maintain an Organization's Security Posture

Each security decision should address at least one of the following concepts in this section. If it doesn't, challenge its value. Implementing a new control means making a change to the production environment. Any change runs the risk of breaking something that was working before or even increasing the attack surface. **Changes shouldn't be taken lightly**. Any change should maintain, if not improve, an organization's security posture. Therefore, if we decide to implement a security control, the net benefit should be mapped back to a *core security concept*.

## Security Theater

**Security theater** means implementing a security control only to say that a security control has been implemented without actually improving security. Since changes like this don’t make the organization any safer, we want to avoid them.

## An Increase in an Organization's Complexity

Changes also run the risk of increasing an organization’s complexity. There’s a general rule that the more complex something is, the greater the chance that something will go wrong. In a security context, complexity increases the likelihood of vulnerabilities and bugs being exploited. In addition to their contribution to security, proposed changes should also be evaluated for complexity. Changes that increase complexity should be considered carefully because they can adversely impact the organization’s overall security.

# Least Privilege

Learn how to manage the access rights to an organization's resources.

## Limit Access

Objects can be protected by limiting access to them. Permissions, otherwise known as privileges or rights, can be assigned to objects. An object can be a protected resource like:

- Documents
- Databases
- Systems

Hardening applies best security practices to an object to make it more resilient to attacks. Restricting how a subject can interact with an object is an example of hardening.

## An Access Control Solution

Access permissions can be enforced and managed by an access control solution. By following the principle of **least privilege**, permissions are explicitly defined based on the rights that a subject needs. Permissions assigned to objects shouldn't exceed what's required. Least privilege is also known as **need to know**.

## Use a Ticket System for Permission Changes

A ticket system can be utilized to effectively manage access for all subjects and objects. This lets permission changes get the appropriate approvals and documentation. Access is ideally tied to human resources so that permissions are based on the employee's role, so those same permission are revoked if that employee separates from the organization.

## Permissions Snowball

A **permissions snowball** is a phenomenon where the amount of access someone has directly reflects their time with the organization. Privileges are granted to the user as they change roles, but they're never revoked. This is due to poor access management processes. Effective access management can help ensure that users only have the permissions they need to perform their specific jobs. When someone changes roles, access rights for the previous role should be revoked and the required rights for the new role should be granted.

# Separation of Duties

Learn the importance of dividing duties among an organization's employees.

## Overview

**Separation of Duties** is similar to least privilege except that the separation of duties focuses on distributing permissions among more than one person.

## The Insider Threat

To protect against the insider threat, permissions should be designed so that no individual has access to everything. Excessive privileges can give individuals the opportunity to commit end-to-end fraud. We prevent this by creating logical barriers between systems and functionality in the form of a secure permissions design.

## Example of an Insurance Company

Let's look at a hypothetical insurance company's IT systems. To reduce the change of fraud being committed by an employee, separation of duties should be used to prevent the same person from being able to create a new insurance policy and then file a claim against that policy. Being able to do both of these things would give an employee the ability to commit insurance fraud.

## Create Hypotheticals

When designing a new system or hardneing an existing one, an analysis of the subject's permissions on objects should be completed. This analysis should imagine different *negative scenarios* where insider fraud could be committed. These scenarios can then be used to identify the following:

- Permissions
- Access Controls
- The roles individuals will serve

# Confidentiality

Learn the importance of data confidentiality within an organization.

## Importance of Confidential Data

Though the popularity of social networks has made privacy difficult to maintain, data still needs to remain confidential. This needs to be driven by regulatory or legal requirements and could prevent costly data breaches. Ensuring the confidentiality of sensitive data means limiting access to these data assets to authorized individuals.

## Classify Confidential Data

The following steps should be used to identify confidential data:

- **Identify** all data that the organization uses and retains. The result of this exercise should be a data inventory or data dictionary.
- **Understand** which regulations and legal requirements the organization needs to adhere to. These requirements should include how confidential data should be defined. There may also be an organizational policy regarding data and data retention. If so, these policies should also be consulted to determine how to define confidential data correctly.
- **Review** the organization's data inventory (customer name, mailing address, and so on) and assign a confidentiality label to each data item. The labeling should follow the confidentiality recommended by relevant regulations and policies.

Take the time to identify all data transmitted and stored. All data used by production networks and systems should be covered. To be thorough, include development and test environments as well. A data classification exercise is worth the effort. 

## Protect Confidential Data

By identifying the data's confidentialty requirements, we can implement the following:

- Appropriate controls
- Processes
- Architectural Design

Encrypting data in transit and at rest, for example, is one of the best ways to ensure that this security principle is followed. Encryption by itself isn't a solution. It also needs to be appropriately implemented.

# Integrity

Learn how to maintain the integrity of an organization's data, such as system files and databases.

## Overview

Maintaining the integrity of data, systems, and software means that those objects haven't been subjected to unauthorized changes, intentional or accidental.

## Maintain the Integrity of System Files

System files are an excellent example of objects whose integrity is critical to protect. Infectious malware is often the cause of changes to these files. Integrity checks can be performed by the following:

- An agent installed on a device.
- The operating system (OS)
- The low-level BIOS that underlies and supports it all.

Because integrity controls may be available in different areas of a device, we should be familiar with the options available to help decide the best way to prevent unauthorized changes from being made on critical files.

## Maintain the Integrity of Documents and Databases

Documents and databases can also have integrity requirements. Some files should never be changed once they're created, such as **log files**. Using integrity checks on log files will let the appropriate teams know if modifications have been made or attempted. Detection of a user or process making changes to a log file could discover a malicious party trying to cover their tracks.

# Keep it Simple

Complexity is bad for security. Attackers will often attempt to exploit the obscure, less-understood details of code and networks. The more complicated something is, such as application code, network design, or firewall rules, the greater the chance that something will go wrong. These flaws could be security vulnerabilities.

## A Simplified Approach

Using the **Keep It Simple, Sir** approach whenever possible when implementing IT and security-related solutions. This principles is also know as the **economy of mechanism**. Less complexity introduces the following benefits:

- Software and systems are easier to use and support.
- Vulnerabilities are easier to find and fix.
- Troubleshooting is easier on less complex systems.

Information systems and security are *complicated enough*. Keep the KISS Principle in mind when deciding which solutions to use and how they should be implemented. If a proposed change seems to introduce more complexity but not much value, it should be reconsidered.

# Logging

