#thehiveproject #tryhackme #dfir #soclevel1 

Welcome to TheHive Project Outline!

This room will cover the foundations of using TheHive project, a Security Incident Response Platform.

Specifically, we will be looking at: 
- What TheHive is?
- An overview of the platform's functionalities and integrations.
- Installing TheHive for yourself.
- Navigating the UI.
- Creation of a case assessment.

![](https://i.imgur.com/qOog5Q4.png)
# Introduction

TheHive Project is a scalable, open-source and freely available Security Incident Response Platform, designed to assist security analysts and practioners working in SOCs, CSIRTs and CERTs to track, investigate and act upon identified security incidents in a swift and *collaborative* manner. 

Security Analysts can collaborate on investigations simultaneously, ensuring real-time information pertaining to new or existing cases, tasks, observables and IOCs are available to all team members. 

More information about the project can be found on [https://thehive-project.org/](https://thehive-project.org/)[](https://thehive-project.org/) & their [GitHub Repo](https://github.com/TheHive-Project/TheHive). 

![](https://i.imgur.com/mTDkIKI.png)

TheHive Project operates under the guide of three core functions:

- **Collaborate**: Multiple analysts from one organization can work together on the same case simultaneously. Through it's live stream capabilities, everyone can keep an eye on the cases in real-time. 
- **Elaborate**: Investigations correspond to cases. The details of each case can be broken down into associated tasks, which can be created from scratch through a template engine. Additionally, analysts can record their progress, attach artifacts of evidence and assign tasks effortlessly.
- **Act**: a quick triaging process can be supported by allowing analysts to add observables to their cases, leveraging tags, flagging IOCs and identifying previously seen observables to feed their threat intelligence.
# TheHive Features and Integrations

TheHive allwos analysts from one organization to work together on the same case simultaneously. This is due to the platform's rich feature set and integrations that support analyst workflows. The features include:

- **Case/Task Management**: Every investigation is meant to correspond to a case that has been created. Each case can be broken down into one or more tasks for added granularity and even be turned into templates for easier management. Additionally, analysts can record their progress, attach pieces of evidence or noteworthy files, add tags and other archives to cases.
- **Alert Triage**: Cases can be imported from SIEM alerts, email reports and other security event sources. This feature allows an analyst to go through the imported alerts and decide whether or not they are to be escalated into investigations or incident response.
- **Observable Enrichment with Cortex**: One of the main feature integrations TheHive supports is Cortex, an observable analysis and active response engine. Cortex allows analysts to collect more information from threat indicators by performing correlation analysis and developing patterns from the cases. More information on [Cortex](https://github.com/TheHive-Project/Cortex/).
- **Active Response**: TheHive allows analysts to use Responders and run active actions to communicate, share information about incidents and prevent or contain a threat.
- **Custom Dashboards**: Statistics on cases, tasks, observables, metrics and more can be compiled and distributed on dashboards that can be used to generate useful KPIs within an organization.
- **Built-in MISP Integration**: Another useful integration is with [MISP](https://www.misp-project.org/index.html), a threat intelligence platform for sharing, storing and correlating Indicators of Compromise of targeted attacks and other threats. This integration allows analysts to create cases from MISP events, import IOCs or export their own identified indicators to their MISP communities.

Other notable integrations that TheHive supports are [DigitalShadows2TH](https://github.com/TheHive-Project/DigitalShadows2TH) & [ZeroFox2TH](https://github.com/TheHive-Project/Zerofox2TH), free and open-source extensions of alert feeders from [DigitalShadows](https://www.digitalshadows.com/) and [ZeroFox](https://www.zerofox.com/) respectively. These integrations ensure that alerts can be added into TheHive and transformed into new cases using pre-defined incident response templates or by adding to existing cases.
# User Profiles & Permissions

TheHive offers an administrator the ability to create an organization group to identify the analysts and assign different roles based on a list of pre-configured user profiles.

![](https://i.imgur.com/GFtoLKt.png)

The pre-configured user profiles are:

- **admin**: full administrative permissions on the platform; can't manage any cases or other data related to investigations
- **org-admin**: manage users and all organization-level configuration, can create and edit Cases, Tasks, Observables, and run Analyzers and Responders;
- **analyst**: can create and edit cases, tasks, observables and run analyzers and responders
- **read-only**: Can only read, cases,tasks and observables details.

![](https://i.imgur.com/hUrxEJC.png)

Each user profile has a pre-defined list of permissions that would allow the user to perform different tasks based on their role. When a profile has been selected, it's permissions will be listed.

![](https://i.imgur.com/4dnnsSw.png)

The full list of permissions includes:

| Permission                           | Functions                                              |
| ------------------------------------ | ------------------------------------------------------ |
| **manageOrganisation (1)  <br>**     | Create & Update an organisation                        |
| **manageConfig (1)  <br>**           | Update Configuration                                   |
| **manageProfile (1)  <br>**          | Create, update & delete Profiles                       |
| **manageTag (1)  <br>**              | Create, update & Delete Tags                           |
| **manageCustomField (1)  <br>**      | Create, update & delete Custom Fields                  |
| **manageCase  <br>**                 | Create, update & delete Cases                          |
| **manageObservable  <br>**           | Create, update & delete Observables                    |
| **manageALert  <br>**                | Create, update & import Alerts                         |
| **manageUser  <br>**                 | Create, update & delete Users                          |
| **manageCaseTemplate  <br>**         | Create, update & delete Case templates                 |
| **manageTask  <br>**                 | Create, update & delete Tasks                          |
| **manageShare**                      | Share case, task & observable with other organisations |
| **manageAnalyse (2)  <br>**          | Execute Analyse                                        |
| **manageAction (2)  <br>**           | Execute Actions                                        |
| **manageAnalyserTemplate (2)  <br>** | Create, update & delete Analyser Templates             |
*Note that (1) organizations, configuration, profiles and tags are global objects. The related permissions are effective only on the "admin" organization. (2) Actions, analysis and template are available only if the Cortex connector is enabled.*

In addition to adding new user profiles, the admin can also perform other operations such as creating case custom fields, custom observable types, custom analyzer templates and importing TTPs from the MITRE ATT&CK framework, as displayed in the image below.

![](https://i.imgur.com/pQadTQh.png)

Deploy the machine attached to follow along on the next task. Please give it a minimum of 5 minutes to boot up. It would be best if you connected to the portal via [http://10.10.124.147/index.html](http://10.10.124.147/index.html)[](http://10.10.124.147/index.html) on the AttackBox or using your VPN connection.

Log on to the _analyst_ profile using the credentials: 

_Username: analyst@tryhackme.me Password: analyst1234_
# Analyst Interface Navigation

You have captured network traffic on your network after suspicion of data exfiltration being done on the network. This traffic corresponds to FTP connections that were established. Your task is to analyse the traffic and create a case on TheHive to facilitate the progress of an investigation. If you are unfamiliar with using Wireshark, please check out [this room](https://tryhackme.com/room/wireshark) first and come back to complete this task.

Once an analyst has logged into the dashboard, they will be greeted with the screen below. At the top, various menu options are listed that allow the user to create new cases and see their tasks and alerts. A list of active cases will be populated on the centre console when analysts create them.

![](https://i.imgur.com/8BzPSco.png)

On clicking the `New Case` tab, a pop up windows opens, providing the analyst with fields to input their case details and tasks. The following options must be indicated on the case to set different categories and filter options:

- *Severity*: This showcases the level of impact the incident being investigated has on the environment from low to critical levels.
- *TLP*: The Traffic Light Protocol is a set of designations to ensure that sensitive information is shared with the appropriate audience. The range of colors represents a scale between full disclosure of information (white) and No disclosure/Restricted (Red). You can find more information about the definitions on the [CISA](https://www.cisa.gov/tlp) website.
- *PAP*: The Permissible Actions Protocol is used to indicate what an analyst can do with the information, whether an attacker can detect the current analysis state or defensive actions in place. It uses a color scheme similar to TLP and is part of the [MISP taxonomies](https://www.misp-project.org/taxonomies.html#_pap).

With this in mind, we open a new case and fill in the details of our investigation, as seen below. Additionally, we add a few tasks to the case that would guide the investigation of the event.

![](https://i.imgur.com/gmSWtKy.gif)

In the visual below, we add the corresponding tactic and technique associated with the case. The TTPs are imported from [MITRE ATT&CK](https://attack.mitre.org/tactics/enterprise/). This provides additional information that can be helpful to map out the threat. As this is an exfiltration investigation, that is the specific tactic chosen and followed by the specific T1048.003 technique for Exfiltration Over Unencrypted/Obfuscated Non-C2 Protocol.

Case observables will be added from the Observables tab and you would have to indicate the following details. 

| **Field**                          | **Description**                                                   | **Examples**              |
| ---------------------------------- | ----------------------------------------------------------------- | ------------------------- |
| _Type *:_                          | The observable dataType                                           | IP address, Hash, Domain  |
| _Value *:_                         | Your observable value                                             | 8.8.8.8, 127.0.0.1        |
| _One observable per line:_         | Create one observable per line inserted in the value field.       |                           |
| _One single multiline observable:_ | Create one observable, no matter the number of lines              | Long URLs                 |
| _TLP *:_                           | Define here the way the information should be shared.             |                           |
| _Is IOC:_                          | Check if this observable is considered an Indicator of Compromise | Emotet IP                 |
| _Has been sighted:_                | Has this observable been sighted on your information system?      |                           |
| _Ignore for similarity:_           | Do not correlate this observable with other similar observables.  |                           |
| _Tags **:_                         | Insightful information Tags.                                      | Malware IP; MITRE Tactics |
| _Description **:_                  | Description of the observable                                     |                           |
In our scenario, we are adding the IP address 192... as our observable as this IP is the source of the FTP requests. Depending on the situation of your analysis, this observable can be marked as an IOC or if it has been sighted before in a different investigation.

![](https://i.imgur.com/8wcy1sC.gif)

