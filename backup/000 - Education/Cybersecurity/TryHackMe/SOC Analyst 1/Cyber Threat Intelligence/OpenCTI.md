> **OpenCTI** is an open-source threat intelligence platform. The room will help you understand and answer the following questions:

- What is OpenCTI and how is it used?
- How would I navigate through the platform?
- What functionalities will be important during a security threat analysis?
# Introduction to OpenCTI

> Cyber Threat Intelligence is typically a managerial mystery to handle, with organizations battling out who to input, digest, analyze and present threat data in a way that will make sense.

For the rooms that have been linked on the overview, it is clear that there are numerous platforms that have been developed to tackle the juggernaut that is Threat Intelligence.
### OpenCTI

> [OpenCTI](https://github.com/OpenCTI-Platform/opencti) is another open-sourced platform designed to provide organisations with the means to manage CTI through the storage, analysis, visualisation and presentation of threat campaigns, malware and IOCs.
### Objective

> Developed by the collaboration of the [French National cybersecurity agency (ANSSI)](https://www.ssi.gouv.fr/) the platforms main objective is to create a comprehensive tool that allows users to capitalize on technical and non-technical information while developing relationships between each piece of information and it's primary source.

The platform can used the [MITRE ATT&CK framework](https://tryhackme.com/room/mitre) to secure the data. Additonally, it can be integrated with other threat intel tools such as MISP and TheHive. Rooms to these tools have been linked in the overview.
# OpenCTI Data Model

> OpenCTI uses a variety of knowledge schemas in structing data, the main one being the Structured Threat Information Expression ([STIX2](https://oasis-open.github.io/cti-documentation/stix/intro)) standards. 
> 
> 	***STIX is a serialized and standardized language format used in threat intelligence.*** 

- It allows for the data to be implemented as entities and relationships, effectively tracing the origin of the provided information.

This data model is supported by how the platform's architecture has been laid out. The image below gives and architectural structure for your know-how:

> The highlight services include:

- **GraphQL API**: The API connects clients to the database and the messaging system.
- **Write Workers**: Python processes utilized to write queries asynchronously from teh RabbitMQ messaging system
- **Connectors**: Another set of Python processes used to ingest, enrich or export data on the platform. These connectors provide the application with a robust network in integrated systems and frameworks to create threat intelligence relations and allow users to improve their defense tactics.

According to OpenCTI, connectors fall under the following classes:

| Class                          | Description                                                  | Examples                  |
| ------------------------------ | ------------------------------------------------------------ | ------------------------- |
| **External Input Connector**   | Ingests information from external sources                    | CVE, MISP, TheHive, MITRE |
| **Stream Connector**           | Consumes platform data stream                                | History, Tanium           |
| **Internal Enrichment Connector**  | Takes in new OpenCTI entities from user requests             | Observables enrichment    |
| **Internal Import File Connector** | Extracts information from uploaded reports                   | PDFs, STIX2 Import        |
| **Internal Export File Connector** | Exports information from OpenCTI into different file formats | CSV, STIX2 export, PDF    |
> Refer to the [connectors](https://github.com/OpenCTI-Platform/connectors) and [data model](https://luatix.notion.site/Data-model-4427344d93a74fe194d5a52ce4a41a8d) documentation for more details on configuring connectors and the data schema.
# OpenCTI Dashboard 1

### OpenCTI Dashboard

> Once connected to the platform, the opening dashboard showcases various visual widgets summarising the threat data ingested into OpenCTI.

- Widgets on the dashboard showcase the current state of entities ingested on the platform via the total number of entities, relationships, reports and observables ingested, and changes to these properties noted within 24 hours.
### Activities & Knowledge

> The OpenCTI categorizes and presents entities under the **Activities & Knowledge** groups on the left side panel.

The activities section cover security incidents ingested onto the platform in the form of reports. It makes it easy for analysts to investigate these incidents. In contrast, the Knowledge section provides linked data related to the tools adversaries use, targeted victims and the type of threat actors and campaigns used.
#### Analysis

> The **Analysis** tab contains the input entities in reports analyzed and associated external references. 

Reports are central to OpenCTI as knowledge on threats and events are extracted and processed. They allow for easier identification of the source of information by analysts. 

Additionally, analysts can add their investigation notes and other external resources for knowledge enrichment. As displayed below, we can look at the **Triton** software report published by MITRE attack and observe or add to the details provided. 
#### Events

> Security analysts investigate and hunt for events involving suspicious and malicious activities across their organizational network. Within the Events tab, analysts can record their findings and enrich their threat intel by creating associated for their incidents.
#### Observations

> Technical elements, detection rules and artefacts identified during a cyber attack are listed under this tab: one or several identifiable makeup indicators.

These elements assist analysts in mapping out threat events during a hunt and perform correlations between what they observe in their environments against the intel feeds.
#### Threats

> All information classified as threatening to an organization or information would be classified under threats. These will include:

- **Threat Actors**: An individual or group of attackers seeking to propagate malicious actions against a target.
- **Intrusion Sets**: An array of TTPs, tools, malware and infrastructure used by a threat actor against targets who share some attributes. APTs and threat groups are listed under this category on the platform due to their known pattern of actions.
- **Campaigns**: Series of attacks taking place within a given period and against victims initiated by advanced persistent threat actors who employ various TTPs. 
	- Campaigns usually have specified objectives and are orchestrated by threat actors from a nation-state, crime syndicate or other disreputable organization.
#### Arsenal

> This tab lists all items related to an attack and any legitimate tools identified from the entities.

- **Malware**: Known and active malware and trojan are listed with details of their identification and mapping based on the knowledge ingested into the platform. In our example, we analyze the **4H RAT** malware and we can extract information and associations made about the malware.
- **Attack Patterns**: Adversaries implement and use different TTPs to target, compromise, and achieve their objectives. 
	- Here, we can look at the details of the ***Command-Line Interface and make decisions based on the relationships established on the platform and navigate through an investigation associated with the technique.***
- **Courses of Action**: MITRE maps out concepts and technologies that can be used to prevent an attack technique from being employed successfully. These are represented as Courses of Action (CoA)  against the TTPs.
- **Tools**: Lists all legitimate tools and services developed for network maintenance, monitoring and management. Adversaries may also use these tools to achieve their objectives. 
	- For example, for the Command-Line Interface attack pattern, it is possible to narrow down that **CMD** would be used as an execution tool. 
	- As an analyst, one can investigate reports and instances associated with the use of the tool.
- **Vulnerabilities**: Known software bugs, system weaknesses and exposures are listed to provide enrichment for what attackers may use to exploit and gain access to systems. 
	- The **Common Vulnerabilities and Exposures (CVE)** list is maintained by MITRE is used and imported via connector.
#### Entities

> This tab categorizes all entities based on operational sectors, countries, organizations and individuals. This information allows for knowledge enrichment on attacks, organizations or intrusion sets.
# OpenCTI Dashboard 2

> The day-to-day usage of OpenCTI would involve navigating through different entities within the platform to understand and utilize the information for any threat analysis. We will be looking at **Cobalt Strike** malware for entity walkthrough, mainly found under the Arsenal Tab we've covered previously. 

When you select an intelligence entity, the details are presented to the user through: 

- **Overview Tab**: Provides the general information about an entity being analyzed and investigated. In our case, the dashboard will present you with the entity ID, confidence level, description, relations created based on threats, intrusion sets and attack patterns, reports mentioning the entity and any external references. 
- **Knowledge Tab**: Presents linked information associated with the entity selected. This tab will include the associated reports, indicators, relations and attacker pattern timeline of the entity. 
- **Analysis Tab**: Provides the reports where the identified entry has been seen. The analysis provides useable information about a threat and guides investigation tasks.
- **Indicators Tab:** Provides information on IOC identified for all the threats and entities
- **Data Tab**: Contains the files uploaded for export that are related to the entity. These assist in communicating information about threats being investigated in either technical or non-technical formats.
- **History Tab**: Changes made to the element, attributes, and relations are tracked by the platform worker and this tab will outline the changes.




