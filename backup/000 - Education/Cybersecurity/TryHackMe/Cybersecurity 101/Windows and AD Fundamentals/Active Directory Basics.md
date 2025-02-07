#tryhackme #cybersecurity101 #infosec #beginner #windows #activedirectory
# Introduction

Microsoft's Active Directory is the backbone of the corporate world. It simplifies the management of devices and users within a corporate environment. In this room, we'll take a deep dive into the essential components of Active Directory.
## Room Objectives

In this room, we will learn about Active Directory and will become familiar with the following topics:

- What Active Directory is
- What an Active Directory Domain is
- What components go into an Active Directory Domain
- Forests and Domain Trust
- Much more!

### Room Prerequisites

- General familiarity with Windows. Check the [Windows Fundamentals module](https://tryhackme.com/module/windows-fundamentals) for more information on this.
# Windows Domains

Picture yourself administering a small business network with only five computers and five employees. In such a tiny network, you will probably be able to configure each computer separately without a problem. You will manually log into each computer, create users for whoever will use them, and make specific configurations for each employee's accounts. If a user's computer stops working, you will probably go to their place and fix the computer on site.

While this sounds like a very relaxed lifestyle, let's suppose your business suddenly grows and now has 157 computers and 320 different user located across four different offices. Would you still be able to manage each computer as a separate entity, manually configure policies for each of the users across the network and provide on-site support for everyone? The answer is most likely no. 

To overcome these limitations, we can use a Windows domain. Simply put, a **Windows Domain** is a group of users and computers under the administration of a given business. The main idea behind a domain is the centralize the administration of common components of a Windows computer network in a single repository called **Active Directory (AD)**. The server that runs the Active Directory services is know as a **Domain Controller (DC)**.

![](https://i.imgur.com/ftJ6akB.png)

The main advantages of having a configured Windows domain are:

- ***Centralized Identity Management***: All users across the network can be configured from Active Directory with minimum effort.
- ***Managing Security Policies***: You can configure security policies directly from AD and apply them to users an computers across the network as needed.

## A Real-World Example

If this sounds a bit confusing, chances are that you have already interacted with a Windows domain at some point in your school, university or work. 

In school/university networks, you will often be provided with a username and password that you can use on any of the computers available on campus. Your credentials are valid for all machines because whenever you input them on a machine, it will forward the authentication process back to the Active Directory, where your credentials will be checked. Thanks to AD, your credentials don't need to exist in each machine and are available through the network.

Active Directory is also the component that allows your school/university to restrict you from accessing the control panel on your school/university machines. Policies will usually be deployed throughout the network so that you don't have administrative privileges over those computers.
## Welcome to THM Inc.

During this task, we'll assume the role of the new IT admin at THM Inc. As our first task, we have been asked to review the current domain "THM.local" and do some additional configurations. You will have administrative credentials over a pre-configured Domain Controller to do the tasks.
# Active Directory

The core of any Windows Domain is the **Active Directory Domain Service (AD DS)**. This service acts aas a catalogue that holds the information of all the "objects" that exist on your network. Amongst the many objects supported by AD, we have users, groups, machines, printers, shares and many others. Let's look at some of them.
## Users

Users are one of the most ocmmon object types in Active Directory. Users are one of the objects known as **security principals**, meaning they can be authenticated by the domain and can be assigned privileges over *resources* like files or printers. You could say that a security principal is an object that can act upon resources in the network.

Users can be used to represent two types of entities:

- **People**: users will generally represent persons in your organization that need to access the network, like employees.
- **Services**: you can also define users to be used by services like IIS or MSSQL. Every single service requires a user to run, but service users are different from regular users as they will only have the privileges needed to run their specific service. 
## Machines

Machines are another type of object within Active Directory; for every computer that joins the Active Directory domain, a machine object will be created. Machines are also considered "security principals" and are assigned an account just as any regular user. This account has somewhat limited rights within the domain itself. 

The machine accounts themeselves are local adminstrators on the assigned computer, they are generally not supposed to be accessed by anyone except the computer itself, but as with any other account, if you have the password, you can use it to log in.

> [!NOTE]
> **Note**: Machine Account passwords are automatically rotated out and are generally comprised of 120 random characters. 

Identifying machine accounts is relatively easy. They follow a specific naming scheme. The machine account name is the computer's name followed by a dollar sign. For example, a machine named `DC01` will have a machine account called `DC01$`.
## Security Groups

If you are familiar with Windows, you probably know that you can define user groups to assign access rights or other resources to entire groups instead of single users. This allows for better manageability as you can dd users to an existing group, and they will automatically inherit all of the group's privileges. Security groups are also considered security principals and, therefore, can have privileges over resources on the network. 

Groups can have both users and machines as members. If needed, groups can include other groups as well. 

Several groups are created by default in a domain that can be used to grant specific privileges to users. As an example, here are some of the most important groups in a domain:

| Security Group     | Description                                                                                                                                               |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Domain Admins      | Users of this group have administrative privileges over the entire domain. By default, they can administer any computer on the domain, including the DCs. |
| Server Operators   | Users in this group can administer Domain Controllers. They cannot change any administrative group memberships.                                           |
| Backup Operators   | Users in this group are allowed to access any file, ignoring their permissions. They are used to perform backups of data on computers.                    |
| Account Operators  | Users in this group can create or modify other accounts in the domain.                                                                                    |
| Domain Users       | Includes all existing user accounts in the domain.                                                                                                        |
| Domain Computers   | Includes all existing computers in the domain.                                                                                                            |
| Domain Controllers | Includes all existing DCs on the domain.                                                                                                                  |
## Active Directory Users and Computers

To configure users, groups or machines in Active Directory, we need to log in to the Domain Controller and run "Active Directory Users and Computers" from the start menu:

![](https://i.imgur.com/yyDSdDP.png)

This will open up a window where you can see the hierarchy of users, computers and groups that exist in the domain. These objects are organized in **Organizational Units (OUs)** which are container objects that allow you to classify users and machines. OUs are mainly used to define sets of users with similar policy requirements. The people in the Sales department of your organization are likely to have a different set of policies applied than the people in IT, for example. Keep in mind that a user can only be a part of a single OU at a time. 

Checking our machine, we can see that there is already an OU called `THM` with four child OUs for the IT, Management, Marketing and Sales departments. It is very typical to see the OUs mimic the business' structure, as it allows for efficiently deploying baseline policies that apply to entire departments. Remember that while this would be the expected model most of the time, you can define OUs arbitrarily.  Feel free to right-click the `THM` OU and create a new OU under it called `Students` just for the fun of it. 

![](https://i.imgur.com/llSYVKr.png)

If you open any OUs, you can see the users they contain and perform simple tasks like creating, deleting or modifying them as needed. You can also reset passwords if needed (pretty useful for the helpdesk):

![](https://i.imgur.com/Va50f0l.png)

You probably noticed already that there are other default containers apart from the THM OU. These containers are created by Windows automatically and contain the following:

- **Built-In**: Contains default groups available to any Windows host
- **Computers**: Any machine joining the network will be put here by default. You can move them if needed.
- **Domain Controllers**: Default OU that contains the DCs in your network.
- **Users**: Default users and groups that apply to a domain-wide context.
- **Managed Service Accounts**: Holds accounts used by services in your Windows domain.
## Security Groups vs. OUs

You are probably wondering why we have both groups and OUs. While both are used to classify users and computers, their purposes are entirely different.

- **OUs** are hand for *applying policies* to users and computers, which include specific configurations that pertain to sets of users depending on their particular role in the enterprise. Remember, a user can only be a member of a single OU at a time, as it wouldn't make sens to try to apply two different sets of policies to a single user.
- **Security Groups**: on the other hand, are used to **grant permissions over resources**. For example, you will use groups if you want to allow some users to access a shared folder or network printer. A user can be a part of many groups, which is needed to grant access to multiple resources. 
# Managing Users in AD

Your first task as the new domain administrator is to check the existing AD OUs and users, as some recent changes have happened to the business. You have been given the following organizational chart and are expected to make changes to the AD to match it:

![](https://i.imgur.com/f72P97x.png)

## Deleting Extra OUs and Users

The first thing you should notice is that there is an additional department OU in your current AD configuration that doesn't appear in the chart. We've been told it was closed due to budget cuts and should be removed from the domain. If you try to right-click and delete the OU, you will get the following error:

![](https://i.imgur.com/IHKy9w0.png)

By default, OUs are protected against accidental deletion. To delete the OU, we need to enable the **Advanced Features** in the view menu:

![](https://i.imgur.com/8uNniN7.png)

This will show you some additional containers and enable you to disable deletion protection. To do so, right-click the OU and go to Properties. You will find a checkbox in the Object tab to disable the protection:

![](https://i.imgur.com/M0gQpT2.png)
Be sure to uncheck the box and try deleting the OU again. You will be prompted to confirm that you want to delete the OU, and as a result, any users, groups or OUs under it will also be deleted:

After deleting the extra OU, you should notice that for some of the departments, the users in the AD don't match the ones in our organizational chart. Create and delete users as needed to match them.
## Delegation

One of the nice things you can do in AD is to give specific users some control over some OUs. This process is known as **delegation** and allows you to grant users specific privileges to perform advanced tasks on OUs without needing a Domain Administrator to step in.

One of the most common use cases for this is granting `IT Support` the privileges to reset other low-privilege users' passwords. According to our organizational chart, Philip is in charge of IT support, so we'd probably want to delete the control of resetting passwords over the Sales, Marketing, and Management OUs to him.

For this example, we will delegate control over the Sales OU to Philip. To delegate control over an OU, you can right-click it and select **Delegate Control**:

![](https://i.imgur.com/ebUCIZb.png)

This should open a new window where you will first be asked to whom you want to delegate control:

> [!NOTE]
> **Note**: To avoid mistyping the user's name, write "phillip" and click the check names button. Windows will autocomplete users for you.

![](https://i.imgur.com/AXrjaSX.png)

Click OK, and on the next step, select the following option:

![](https://i.imgur.com/lL26j5A.png)

Click a couple of times, and now Philip should be able to reset passwords for any user in the sale department. While you'd probably want to repeat these steps to delegate the password resets of the Marketing and Management departments, we'll leave it here for this task. You are free continue to configure the rest of the OUs if you so desire.

While you may be tempted to go to **Active Directory Users and Computers** to try and test Phillip's new powers, he doesn't really have the privileges to pen it, so you'll have to use other methods to do password resets. In this case, we will be using PowerShell to do so:

```shell-session
PS C:\Users\phillip> Set-ADAccountPassword sophie -Reset -NewPassword (Read-Host -AsSecureString -Prompt 'New Password') -Verbose

New Password: *********

VERBOSE: Performing the operation "Set-ADAccountPassword" on target "CN=Sophie,OU=Sales,OU=THM,DC=thm,DC=local".
```

Since we wouldn;t want Sophie to keep on using a password we know, we can also force a password reset at the next logon with the following command:

```shell-session
PS C:\Users\phillip> Set-ADAccountPassword sophie -Reset -NewPassword (Read-Host -AsSecureString -Prompt 'New Password') -Verbose

New Password: *********

VERBOSE: Performing the operation "Set-ADAccountPassword" on target "CN=Sophie,OU=Sales,OU=THM,DC=thm,DC=local".
```
# Managing Computers in AD

By default, all the machines that join a domain (except for the DCs) will be put in the container called "Computers". If we check our DC, we will see that some devices are already there:

![](https://i.imgur.com/FlGgYQe.png)

We can see some servers, some laptops and some PCs corresponding to the users in our network. Having all of our devices there is not the best idea *since it's very likely that you want different policies for your servers and the machines that regular users use on a daily basis*.

While there is no golden rule on how to organize your machines, an excellent starting point is segregating devices according to their use. In general, you'd expect to see devices divided into at least three following categories:
## 1. Workstations

Workstations are one of the most common devices within an Active Directory domain. Each user in the domain will likely be logging into a workstation. This is the device they will use to do their work or normal browsing activities. These devices should never have a privileged user signed into them.

## 2. Servers

Servers are the second most common device within an Active Directory Domain. Servers are generally used to provide access to users or other services. 

## 3. Domain Controllers

Domain Controllers are the third most common device within an Active Directory domain. Domain Controllers allow you to manage the Active Directory Domain. These devices are ofteen deemed the most sensitive devices within the network as they contain hashed passwords for all user accounts within the environment.

Since we are tidying up our AD, let's create two separate OUs for `Workstations` and `Servers` (Domain Controllers are already in an OU created by Windows). We will be creating them directly under the `thm.local` domain controller. In the end, you should have the following OU structure:

![](https://i.imgur.com/8kJyK9n.png)

Now, move the personal computers and laptops to the Workstations OU and the servers to the Servers OU from the Computers container. Doing so will allow us to configure policies for each OU later. 
# Group Policies

So far, we have organized users and computers in OUs just for the sake of it, but the main idea behind this is to be able to deploy different policies for each OU individually. That way, we can push different configurations and security baselines to users depending on their department.

Windows manages such policies through **Group Policy Objects (GPO)**. GPOs are simply a collection of settings that can be applied to OUs. GPOs can contain policies aimed at either users or computers, allowing you to set a baseline on specific machines and identities.

To configure GPOs, you can use the **Group Policy Management** tool, available from the start menu:

![](https://i.imgur.com/ywIT366.png)

The first thing you will see when opening it is your complete OU hierarchy, as defined before. To configure group policies, you can first create a GPO under **Group Policy Objects** and then link it to the OU where you want the policies to apply. As an example, you can see there are some already existing GPOs in your machine:

![](https://i.imgur.com/GgICgdH.png)

We can see in the image above that 3 GPOs have been created. From those, the `Default Domain Policy` and `RDP Policy` are linked to the `thm.local` domain as a whole, and the `Default Domain Controllers Policy` is linked to the `Domain Controllers` OU only. Something important to have in mind is that any GPO will apply to the linked OU and any sub-OUs under it. For example, the `Sales` OU will still be affected by the `Default Domain Policy`.

Let's examine the `Default Domain Policy` to see what's inside a GPO. The first tab you'll see when selecting a GPO shows its **scope**, which is where the GPO is linked in the AD. For the current policy, we can see that it has only been linked to the `thm.local` domain:

![](https://i.imgur.com/4L9V7tV.png)

As you can see, you can also apply **Security Filtering** to GPOs so that they are only applied to specific users/computers under and OU. By default, they will apply to the **Authenticated Users** group, which includes all users/PCs.

The **Settings** tab includes the actual contents of the GPO and lets us know what specific configurations it applies. As stated before, each GPO has configurations that apply to computers only and configurations that apply to users only. In this case, the `Default Domain Policy` only contains Computer Configurations:

![](https://i.imgur.com/sEvEnLO.png)

Feel free to explore the GPO and expand on the available items using the "show" links on the right side of each configuration. In this case, the `Default Domain Policy` indicates really basic configurations that should apply to most domains, including password and account lockout policies:

![](https://i.imgur.com/CgrYVtH.png)

Since this GPO applies to the whole domain, any change to it would affect all computers. Let's change the minimum password length policy to have at least 10 characters in their passwords. To do this, right-click the GPO and select **Edit**:

![](https://i.imgur.com/yrLYRSs.png)

This will open a new window where we can navigate and edit all the available configurations. To change the minimum password length, go to `Computer Configurations -> Policies -> Windows Setting -> Security Settings -> Account Policies -> Password Policy` and changes the required policy value:

![](https://i.imgur.com/Q9ETMGn.png)

As you can see, plenty of policies can be established in a GPO. While explaining every single one of them would be impossible in a single room, do feel free to explore a bit, as some of the policies are straightforward. If more information on any of the policies is needed, you can double-click them and read the **Explain** tab on each of them:

![](https://i.imgur.com/jBzZTZ3.png)
## GPO Distribution

GPOs are distributed to the network via a network share called `SYSVOL`, which is stored in the DC. All users in a domain should typically have access to this share over the network to sync their GPOs periodically. The SYSVOL share points by default to the `C:\Windows\SYSVOL\sysvol\` directory on each of the DCs in our network.

Once a change has been made to any GPOs, it might take up to 2 hours for computers to catch up. If you want to force any particular computer to sync its GPOs immediately, you can always run the following command on the desired computer:

```shell-session
PS C:\> gpupdate /force
```
## Creating Some GPOs for THM Inc.

As part of our new job, we have been tasked with implementing some GPOs to allow us to:

1. Block non-IT users from accessing the Control Panel
2. Make workstations and servers lock their screen automatically after 5 minutes of user inactivity to avoid people leaving their sessions exposed.

Let's focus on each of those and define what policies we should enable in each GPO and where they should be linked.
### Restrict Access to Control Panel

We want to restrict access to the Control Panel across all machines to only th users that are part of the IT department. Users of other departments shouldn't be able to change the system's preferences.

Let's create a new GPO called `Restrict Control Panel Access` and open it for editing. Since we want this GPO to apply to specific users, we will look under `User Configuration` for the following policy:

![](https://i.imgur.com/jxnnlnD.png)

Notice we have enabled the **Prohibit Access to Control Panel and PC Settings** policy.

Once the GPO is configured, we will need to link it to all of the OUs corresponding to users who shouldn't have access to the Control Panel of their PCs. In this case, we will link the `Marketing`, `Management` and `Sales` OUs by dragging the GPO to each of them.

![](https://i.imgur.com/zowDkb4.png)
### Auto Lock Screen GPO

For the first GPO, regarding screen locking for workstations and servers, we could directly apply it over the `Workstations`, `Servers` and `Domain Controllers` OUs we have created previously. 

While this solution should work, an alternative consists of simply applying the GPO to the root domain, as we want the GPO to affect all of our computers. Since the `Workstations`, `Servers` and `Domain Controllers` OUs are all child OUs of the root domain, they will inherit its policies.

> [!NOTE]
> **Note**: You might notice that if your GPO is applied to the root domain, it will also be inherited by other OUs like `Sales` or `Marketing`. Since these OUs contain users only, any Computer Configuration in our GPO will be ignored by them.

Let's create a new GPO, call it `Auto Lock Screen`, and edit it. The policy to achieve what we want is located in the following route:

![](https://i.imgur.com/YLuD3DN.png)

We will set the inactivity limit to 5 minutes so that computers get locked automatically if any user leaves their session open. After closing the GPO editor, we will link the GPO to the root domain by dragging the GPO to it:

![](https://i.imgur.com/p1CHk1S.png)

Once the GPOs have been applied to the correct OUs, we can log in as any users in either Marketing, Sales or Management for verification. For this task, let's connect via RDP using Mark's credentials:
# Authentication Methods

When using Windows domains, all credentials are stored in the Domain Controllers. Whenever a user tries to authenticate to a service using domain credentials, the service will need to ask the Domain Controller to verify if they are correct. Two protocols can be used for network Authentication in Windows domains:

- `Kerberos`: Used by any recent version of Windows. This is the default protocol in any recent domain.
- `NetNTLM`: Legacy authentication protocol kept for compatibility purposes.

While NetNTLM should be considered obsolete, most networks will have both protocols enabled. Let's take a deeper look at how each of these protocols works:
## Kerberos Authentication

Kerberos authentication is the default authentication protocol for any recent version of Windows. Users who log into a service using Kerberos will be assigned tickets. Think of tickets as *proof of a previous authentication*. Users with tickets can present them to a service to demonstrate they have already authenticated into the network before and are therefore enabled to use it.

---

Kerberos is a computer network authentication protocol that operates based on tickets, allowing nodes to securely prove their identity to one another over a non-secure network. It primarily aims at a client-server model and provides mutual authentication, where the user and the server verify each other's identity. The Kerberos protocol messages are protected against eavesdropping and replay attacks, and it builds on symmetric-key cryptography, requiring a trusted third party.

---

When Kerberos is used for authentication, the following process happens:

1. The user sends their username and a timestamp encrypted using a key derived from their password to the `Key Distribution Center (KDC)`, a service usually installed on the Domain Controller in charge of creating Kerberos tickets on the network. The KDC will create and send back a `Ticket Granting Ticket (TGT)`, which will allow the user to request additional tickets to access specific services. The need for a ticket to get more tickets may sound a bit weird, but it allows users to request service tickets without passing their credentials every time they want to connect to a service. Along with TGT, a `Session Key` is given to the user, which they will need to generate the following requests. Notice the TGT is encrypted using `krbtgt` account's password hash, and therefore the user can't access its contents. It is essential to know that the encrypted TGT includes a copy of the Session Key as part of its contents, and the KDC has no need to store the Session Key as it can recover a copy by decrypting the TGT if needed. 

![](https://i.imgur.com/MVSGRhC.png)

2. When a user wants to connect to a service on the network like a share, website or database, they will use their TGT to ask the KDC for a **Ticket Granting Service (TGS)**. TGS are tickets that allow connection only to the specific service they were created for. To request a TGS, the user will send their username and a timestamp encrypted using the Session Key, along with the TGT and a `Service Principal Name (SPN)`, which indicates the service and server name we intend to access. As a result, the KDC will send us a TGS along with a `Service Session Key`, which we will need to authenticate to the service we want to access. The TGS is encrypted using a key derived from the `Service Owner Hash`. The Service Owner is the user or machine account that the service runs under. TH TGS contains a copy of the Service Session Key on its encrypted contents so that the Service Owner can access it by decrypting the TGS.

![](https://i.imgur.com/Zjmn1n4.png)

3. The TGS can then be sent to the desired service to authenticate and establish a connection. The service will use its configured account's password hash to decrypt the TGS and validate the Service Session Key.

![](https://i.imgur.com/qqEooyd.png)

## NetNTLM Authentication

NetNTLM works using a *challenge-response mechanism*. The entire process is as follows:

![](https://i.imgur.com/NGdag2T.png)

1. The client sends an authentication request to the server they want to access.
2. The server generates a random number and sends it as a challenge to the client.
3. The client combines their NTLM password hash with the challenge (and other known data) to generate a response to the challenge and sends it back to the server for verification.
4. The server forwards the challenge and the response to the Domain Controller for verification.
5. The domain controller uses the challenge to recalculate the response and compares it to the original response sent by the client. If they both match, the client is authenticated; otherwise, access is denied. The authentication is sent back to the server.
6. The server forwards the authentication result to the client.

Note that the user's password (or hash) is never transmitted through the network for security.

> [!NOTE]
> **Note:** The described process applies when using a domain account. If a local account is used, the server can verify the response to the challenge itself without requiring interaction with the domain controller since it has the password hash stored locally on its SAM.
# Trees, Forests and Trusts

So far, we have discussed how to manage a single domain, the role of a Domain Controller and how it joins computers, servers and users. 

![](https://i.imgur.com/2kFwtEa.png)

As companies grow, so do their networks. Having a single domain for a company is good enough to start, but in time some additional needs might push you into having more than one. 
## Trees

Imagine, for example, that suddenly your company expands to a new country. The new country has different laws and regulations that require you to update your GPOs to comply. In addition, you now have IT people in both countries, and each IT team needs to manage the resources that correspond to each country without interfering with the other team. While you could create a complex OU structure and use delegations to achieve this, having a huge AD infrastructure might be hard to manage and prone to human errors. 

Luckily for us, Active Directory supports integrating multiple domains so that you can partition your network into units that can be managed independently. If you have two domains that share the same namespace (`thm.local`) for example, those domains can be joined into a **Tree**.

If our `thm.local` domain was split into two subdomains for UK and US branches, you could build a tree with a root domain of `thm.local` and two subdomains called `uk.thm.local` and `us.thm.local`, each with its AD, computers, and users:

![](https://i.imgur.com/pmhR1KO.png)

This partitioned structure gives us better control over who can access what in the domain. The IT people from the UK will have their own DC that manages the UK resources only. For example, a UK user would not be able to manage US users. In that way, the Domain Administrators of each branch will have compete control over their respective DCs, but not other branches' DCs. Policies can also be configured independently for each domain in the tree.

A new security group needs to be introduced when talking about trees and forests. The **Enterprise Admins** group will grant a user administrative privileges over all of an enterprise's domains. Each domain would still have its Domain Admins with administrator privileges over their single domains and the Enterprise Admins who can control everything in the enterprise. 
## Forests

The domains you manage can also be configured in different namespaces. Suppose your company continues growing and eventually acquires another company called `MHT Inc.`. When both companies merge, you will probably have different domain trees for each company, each managed by its own IT department. The union of several trees with different namespaces into the same network is known as a **forest**.

![](https://i.imgur.com/FY8JojZ.png)

## Trust Relationships

Having multiple domains organized in trees and forest allows you to have a nice compartmentalized network in terms of management and resources. But at a certain point, a user at THM UK might need to access a shared file in one of MHT ASIA servers. For this to happen, domains arranged in trees and forest are joined together by **trust relationships**. 

In simple terms, having a trust relationship between domains allows you to authorize a user from domain `THM UK` to access resources from domain `MHT EU`.

The simplest trust relationship that can be established is a **one-way trust relationhip**. In a one-way trust, if `Domain AAA` trusts `Domain BBB`, this means a user on BBB can be authorized to access resources on AAA:

![](https://i.imgur.com/AO30NVm.png)

The direction of the one way trust relationship is contrary to that of the access direction. 

**Two-Way Trust Relationships** can also be made to allow both domains to mutually authorize users from the other. By default, joining several domains together under a tree or forest will form a two-way trust relationship. 

It is important to note that having a trust relationship between two domains doesn't automatically grant access to all resources on other domains. Once a trust relationship is established, you have the chance to authorize users across different domains, but it's up to you what is actually authorized or not.

# Conclusion

In this room, we have shown the basic components and concepts related to Active Directories and Windows Domains. Keep in mind that this room should only serve as an introduction to the basic concepts, as there's quite a bit more to explore to implement a production-ready Active Directory environment.

If you are interested in learning how to secure an Active Directory installation, be sure to check out the Active Directory Hardening Room (To be released soon). If, on the other hand, you'd like to know how attackers can take advantage of common AD misconfigurations and other AD hacking techniques, the [Compromising Active Directory module](https://tryhackme.com/module/hacking-active-directory) is the way to go.

