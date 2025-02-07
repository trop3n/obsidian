### MISP - Malware Information Sharing Platform

> This room explores the MISP Malware & Threat Sharing Platform through its core objective to foster sharing of structured threat information among security analysts, malware researchers and IT professionals. 
### Room Objectives

> We will be covering the following areas within the room:
- Introduction to MISP and why it was developed
- Use cases MISP can be applied to
- Core features and terminologies
- Dashboard Navigation
- Event Creation and Management
- Feeds and Taxonomies
# What is MISP?

> [MISP (Malware Information Sharing Platform)](https://www.misp-project.org/) is an open-source threat information platform that facilitates the collection, storage and distribution of threat intelligence and Indicators of Compromise related to malware, cyberattacks, financial fraud or any intelligence within a community of trusted members.

Information sharing follows a distributed model, with supported closed, semi-private, and open communities (public). 

Additionally, the threat information can be distributed and consumed by **Network Intrusion Detection Systems** (NIDS), log analysis tools and **Security Information and Event Management Systems.** 

MISP is effectively useful for the following use cases:

- **Malware Reverse Engineering**: Sharing of malware indicators to understand how different malware families function. 
- **Security Investigations**: Searching, validating and using indicators in investigating security breaches. 
- **Intelligence Analysis**: Gathering information and using indicators in investigating security breaches.
- **Law Enforcement**: Using Indicators to support forensic investigations.
- **Risk Analysis**: Researching new threats, their likelihood and occurrences.
- **Fraud Analysis**: Sharing of financial indicators to detect financial fraud.
### What doe MISP support?

MISP provides the following core functionalities:

- **IOC Database**: This allows for the storage of technical and non-technical information about malware samples, incidents, attackers and intelligence.
- **Automatic Correlation**: Identification of relationships between attributes and indicators from malware, attack campaigns or analysis.
- **Data Sharing**: This allows for sharing of information using different models of distributions and among different MISP instances. 
- **Import & Export Features**: This allows the import and export of events in different formats to integrate other systems such as NIDS, HIDS and OpenIOC.
- **Event Graph**: Showcases the relationships between objects and attributes identified from events.
- **API Support**: Supports integration with own systems to fetch and export events and intelligence.

> The following terms are commonly used within MISP and are related to the functionalities described above and the general usage of the platform:

- **Events**: Collection of contextually linked information
- **Attributes**: Individual data points associated with an event, such as network or system indicators
- **Objects**: Custom attribute compositions
- **Object References**: Relationships between different objects
- **Sightings**: Time-specific occurrences of a given data point or attribute detected to provide more credibility.
- **Tags**: Labels attached to events/attributes
- **Taxonomies**: Classification libraries are used to tag, classify and organize information
- **Galaxies**: Knowledge base items used to label events/attributes
- **Indicators**: Pieces of information that can detect suspicious or malicious cyber activity
# Using the System

### Dashboard

> The analyst's view of MISP provides you with the functionalities to track, share and correlate events and IOCs identified during your investigation. The dashboard's menu contains the following options, and we shall look into them further:

- **Home Button**: Returns you to the application's start screen, the event index page or the page set as a custom home page using the star in the top bar.
- **Event Actions**: All the malware data entered into MISP comprises an event object described by its connected attributes. The event actions menu gives access to all the functionality related to the creation, modification, deletion, publishing, searching and listing of events and attributes.
- **Dashboard**: This allows you to create a custom dashboard using widgets.
- **Galaxies**: Shortcut to the list of  [MISP Galaxies](https://github.com/MISP/misp-book/blob/main/galaxy) on the MISP instance.
- **Input Filters**: Input Filters alter how users enter data into this instance. Apart from the basic validation of attribute entry by type, the site administrators can define regular expression in replacements and blocklists for specific values and block certain values from being exportable. Users can view these replacement and blocklist rules here, while and admin can alter them.
- **Global Actions**: Access to information about MISP and this instance. You can view and edit your profile, view the manual, read the news or terms of use again, see a list of the active organizations on this instance and a histogram of their contributions by attribute type.
- **MISP**: Simple Link to your baseurl.
- **Name**: Name (Auto-generated from mail address) of currently logged in user.
- **Envelope**: Link to User Dashboard to consult some of your notifications and changes since the last visit, like some proposals received for your organization.
- **Log Out**: The log out button to end your session immediately.
### Event Management

> The **Event Actions** tab is where you, as an analyst, will create all malware investigation correlations by providing descriptions and attributes associated with the investigation.

Splitting resources into three significant phases, we have:

- **Event Creation**
- **Populating events with attributes and attachments**
- **Publishing**
#### Event Creation

> In the beginning, events are a storage of general information about an incident or investigation. We add the description, time, and risk level deemed appropriate for the incident by clicking the **Add Event** button.

- Additionally, we specify the distribution level we would like our event to have on the MISP network and community. 
- According to MISP, the following distribution options are available:

	- **Your Organization Only**: This only allows members of your organization to see the event.
	- **This community only**: Users that are part of your MISP community will be able to see the event. This includes your organization, organizations on this MISP server and organizations running MISP servers that synchronize with this server.
	- **Connected communities**: Users who are part of your MISP community will see the event, including all organizations on this MISP server, all organizations on MISP servers synchronizing with this server, and the hosting organizations of servers that are two hops away from this one.
	- **All communities**: This will share the event with all MISP communities, allowing the event to be freely propagated from one server to the next.
	-

> Additionally, MISP provides a means to add a sharing group, where an analyst can define a predefined list of organizations to share events.

Event details can also be populated by filling our predefined fields on a defined template, including adding attributes to the event. 
	We can use the emails details of the CobaltStrike investigation to populate details of our event. 
	We will be using the **Phishing Email** category from the templates.
### Attributes and Attachments

> Attributes can bee added manually or imported through other formats such as ***OpenIOC and ThreatConnect.*** 
> 
> 	To add them manually, click the **Add Attribute** and populate the form fields. 

Some essential options to note are:

- **For Intrusion Detection System**: This allows the attribute to be used as an IDS signature when exporting the NIDS data unless it overrides the permitted list. If not set, the attribute is considered contextual information and not used for automatic detection. 
- **Batch Import**: If there are several attributes of the same type to enter (such as a list of IP addresses) it is possible to join them all into the same value field, separated by a line break between each line. This will allow the system to create separate lines for each attribute.

> The analyst can also add file attachments to the event. These may include malware, report files from external analysis or simply artefact dropped by the malware. 

We have added the CobaltStrike EXE binary file to our event in the example. You also have to check the malware checkbox to mark the file as malware. This will ensure that it is zipped and passworded to protect users from accidentally downloading and executing the file.

**Publish Event**

> Once the analysts have created events, the *organizational admin* will review and publish those events to add them to the pool of events. 

This will also share the events to the distribution channels set during the creation of the events.
# Feeds and Taxonomies

> **Feeds** are resources that contain indicators that can be imported into MISP and provide attributed information about security events. 

These feeds provide analysts and organizations with continuously updated information on threats and adversaries and aid in their proactive defence against attacks.

MISP Feeds provide a way to:

- Exchange threat information
- Preview events along with associated attributes and objects
- Select and import events to your instance
- Correlate attributes identified between events and feeds

Feeds are enabled and managed by the **Site Admin** for the analysts to obtain information on events and indicators.
### Taxonomies

> A **taxonomy** is a means of classifying information based on standard features or attributes. On MISP, taxonomies are used to categorize events, indicators and threat actors based on tags that identify them. 
![[taxonomy-explanation.png]]

> Analysts can use taxonomies to:

- Set events for further processing by external tools such as VirusTotal.
- Ensure events are classified appropriately before the Organizational Admin publishes them.
- Enrich intrusion detection systems' export values with tags that fit specific deployments.

> Taxonomies are expressed in machine tags, which comprise three vital parts:

- **Namespace**: Defines the tag's property to be used
- **Predicate**: Specifies the property attached to the data
- **Value**: Numerical or text details to map the property
### Tagging

> Information from feeds and taxonomies, tags can be placed on events and attributers to identify them based on the indicators or threats identified correctly. 

Tagging allows for effective sharing of threat information between users, communities and other organizations using MISP to identify various threats.

In our CobaltStrike event example, we can add tags by clocking on the buttons in the **Tags** section and searching from the available options appropriate to the case.

- The buttons represent *global* tags and *local* tags, respectively.
- It is also important to note that you can add your unique tags to your MISP instance as an analyst or organization that would allow you to ingest, navigate through and share information quickly within the organization.
### Tagging Best Practices

#### Tagging at Event Level vs. Attribute Level

> Tags can be added to an event and attributes. Tags are also inheritable when set. It is recommended to set tags on the entire event and only include tags on attributes when they are an exception from what the event indicates.

- This will provide a more fine-grained analysis. 

#### The Minimal Subset of Tags

The following tags can be considered a must-have to provide a well-defined event for distribution:

- **Traffic Light Protocol**: Provides a color schema to guide how intelligence can be shared.
- **Confidence**: Provides and indication as to whether or not the data being shared is of high quality and has been vetted so that it can be trusted to be good for immediate usage.
- **Origin**: Describes the source of information and whether it was from automation or manual investigation.
- **Permissible Actions Protocol**: An advanced classification that indicates how the data can be used to search for compromises with the organization.




