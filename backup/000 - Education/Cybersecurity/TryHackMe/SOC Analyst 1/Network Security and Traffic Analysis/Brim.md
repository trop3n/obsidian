# Introduction

> [BRIM](https://www.brimdata.io/) is an open-source desktop application that processes pcap files and logs files. Its primary focus is providing *search and analytics*. In this room, you will learn how to use Brim, process pcap files and investigate log files to find the needle in the haystack.

This room expects you to be familiar with basic security concepts and processing Zeek log files. We suggest completing the "Network Fundamentals" path and the Zeek Room before starting work in this room.

# What is Brim?

> Brim is an open-source desktop application that processes pcap files and logs files, with a primary focus on providing search and analytics. It uses the Zeek log processing format. It also supports Zeek signatures and Suricata rules for detection.

It can handle two types of data as an input:

- ***Packet Capture Files***: Pcap files created with tcpdump, tshark and Wireshark applications. 
- ***Log Files***: Structured log files like Zeek logs.

Brim is built on open-source platforms.

- ***Zeek***: Log generating engine.
- ***Zed Language***: Log querying language that allows performing keyword searches with filters and pipelines. 
- ***ZNG Data Format***: Data storage format that supports saving data streams.
- ***Electron and React***: Cross-platform UI.

### Why Brim?

Ever had to investigate a big pcap file? Pcap files bigger than on gigabyte are cumbersome for Wireshark. Processing big pcaps with tcpdump and Zeek is efficient but requires time and effort. Brim reduces the time and effort spent processing pcap files and investigating the log files by providing a simple and powerful GUI application. 
### Brim vs. Wireshark vs. Zeek

Each of them is powerful and useful, it is good to know the strengths and weaknesses of each tool and which one to use for the best outcome. As a traffic capture analyzer, some overlapping functionalities exist, but each one has a unique value for different situations.

**The common best practice is handling medium sized pcaps with Wireshark, creating logs and correlating events with Zeek, and processing multiple logs in Brim.**

|   |   |   |   |
|---|---|---|---|
||Brim|Wireshark|Zeek|
|Purpose|Pcap processing; event/stream and log investigation.|Traffic sniffing. Pcap processing; packet and stream investigation.|Pcap processing; event/stream and log investigation.|
|GUI|✔|✔|✖|
|Sniffing|✖|✔|✔|
|Pcap processing|✔|✔|✔|
|Log processing|✔|✖|✔|
|Packet decoding|✖|✔|✔|
|Filtering|✔|✔|✔|
|Scripting|✖|✖|✔|
|Signature Support|✔|✖|✔|
|Statistics|✔|✔|✔|
|File Extraction|✖|✔|✔|
|Handling  pcaps over 1GB|Medium performance|Low performance|Good performance|
|Ease of Management|4/5|4/5|3/5|
# The Basics

### Landing Page

> When Brim is opened, the landing page opens up. The landing page has three sections and a file importing window. It also provides quick info on supported file formats.

- ***Pools***: Data resources, investigated pcap and log files. 
- ***Queries***: List of available queries
- ***History***: List of launched queries

### Pools and Log Details

Pools represent the imported files. Once you load a pcap, Brim processes the file and creates Zeek logs, correlates them, and displays all available findings in a timeline, as shown in the image below.

The timeline provides information about capture start and end dates. Brim also provides information fields. You can hover over fields to have more details on the field. The above image shows a user hovering over Zeek's conn.log file and UID value. 

This information will help you in creating custom queries. The rest of the log details are shown in the right pane and provides details of the log file fields. Note that you can always export the results by using the export function located near the timeline. 

You can correlate each log entry by reviewing the correlation section at the log details pane (shown on the left image.) This section provides information on the source and destination addresses, duration and associated log files.

This quick information helps you answer the "Where to look next?" question and find the event of interest and linked evidence.

You can also right-click on each field to filter and accomplish a list of tasks. 

- Filtering values
- Counting fields
- Sorting (A-Z and Z-A)
- Viewing details
- Performing whois lookup on IP address
- Viewing the associated packets in Wireshark. 

The below image demonstrates how to perform whois lookup and Wireshark packet inspection.
### Queries and History

> Queries help us to correlate finding and find the event of interest. History stores executed queries.

The image below demonstrates how to browse the queries and load a specific query from the library. Queries can have names, tags and descriptions.

Query library lists the query names, and once you double-click, it passes the actual query to the search bar.

You can double click on the query and execute it with ease. Once you double click on the query, the actual query appears on the search bar and is listed under the history tab. 

The results are shown under the search bar. In this case, we listed all available log sources created by Brim. In this example, we only insert a pcap file, and it automatically creates nine types of Zeek log files.

Brim has 12 premade queries listed under the "Brim" folder. These queries help us discover the Brim query structure and accomplish quick searches from templates. You can add new queries by clicking on the "+" button near the "Queries" menu.
# Default Queries

> It was mentioned that Brim has 12 premade queries in the previous task. Let's see them in action. 

Now, open Brim, import the sample pcap and go through the walkthrough. 

### Reviewing Overall Activity

> This query provides general information on the pcap file. The provided information is valuable for accomplishing further investigation and creating custom queries. It is *impossible to create advanced or case specific* queries without knowing the available log files.

The image below shows that there are 20 logs generated for the provided pcap file.
### Windows Specific Network Activity

> This query focuses on Windows networking activity and details the source and destination addresses and named pipe, endpoint and operation detection. The provided information helps investigate and understand specific Windows events like SMB enumeration, logs and service exploiting.
### Unique Network Connections and Transferred Data

> These two queries provide information on unique connections and connection-data correlation. The provided info helps analysts detect weird and malicious connections and suspicious and beaconing activities.

The **uniq** list provides a clear list of unique connections that help identify anomalies.

The data list summarizes the data transfer rate that supports the anomaly investigation hypothesis. 
### DNS and HTTP Methods

> These queries provide the list of the DNS queries and HTTP methods. The provided information helps analysts to detect anomalous DNS and HTTP traffic. 

You can also narrow the search by viewing the "HTTP POST" requests with the available query and modifying it to view the "HTTP GET" methods.
### File Activity

> This query provides the list of the available files. It helps analysts to detect possible data leakage attempts and suspicious file activity. 

The query provides info on the detected file MIME and file name and hash values. (MD5, SHA1)
### IP Subnet Statistics

> This query provides the list of available IP subnets. It helps analysts detect possible communications outside the scope and identify out of ordinary IP addresses. 
### Suricata Alerts

> These queries provide information based on Suricate rule results. Three different queries are available to view the available logs in different formats. (category-based, source and destination-based, and subnet based).

**Note**: Suricata is an open-source threat detection engine that can act as a rule-based Intrusion Detection and Prevention System. It is developed by the Open Information Security Foundation (OISF). Suricata works and detects anomalies in a similar way to Snort and can use the same signatures.
# Use Cases

### Custom Queries and Use Cases

> There are a variety of use case example in traffic analysis. For a security analyst, it is vital to know the common patterns and indicators of anomaly or malicious traffic.

In this task, we will cover some of them. Let's review the basics of the Brim queries before focusing on the custom and advanced ones.
### Brim Query Reference

|   |   |   |
|---|---|---|
|**Purpose**|**Syntax**|**Example Query**|
|Basic search|You can search any string and numeric value.|Find logs containing an IP address or any value.<br><br>`   10.0.0.1   `|
|Logical operators|Or, And, Not.|Find logs contain three digits of an IP AND NTP keyword.<br><br>`   192 and NTP   `|
|Filter values|"field name" == "value"|Filter source IP.<br><br>`   id.orig_h==192.168.121.40   `|
|List specific log file contents|_path=="log name"|List the contents of the conn log file.<br><br>`   _path=="conn"   `|
|Count field values|count () by "field"|Count the number of the available log files.<br><br>`   count () by _path   `|
|Sort findings|sort|Count the number of the available log files and sort recursively.<br><br>`   count () by _path \| sort -r   `|
|Cut specific field from a log file|_path=="conn" \| cut "field name"|Cut the source IP, destination port and destination IP addresses from the conn log file.<br><br>`   _path=="conn" \| cut id.orig_h, id.resp_p, id.resp_h   `|
|List unique values|uniq|Show the unique network connections. <br><br>`_path=="conn" \| cut id.orig_h, id.resp_p, id.resp_h \| sort \| uniq`|
%% **Note**: It is highly suggested to use field names and filtering options and not rely on the blind/irregular search function. Brim provides great indexing of log sources, but it is not performing well in irregular search queries. The best practice is to use the field filters to search for the event of interest.  %%

|                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| --------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Communicated Hosts**            | Identifying the list of communicated hosts is the first step of an investigation. Security analysts need to know which hosts are actively communicating on the network to detect any suspicious and abnormal activity in the first place. This approach will help analysts to detect possible access violations, exploitation attempts and malware infections.<br><br>**Query**: `_path=="conn" \| cut id.orig_h, id.resp_h \| sort \| uniq`                                                                                                                                                                |
| **Frequently Communicated Hosts** | After having the list of communicated hosts, it is important to identify which hosts communicate with each other most frequently. This will help security analysts to detect possible data exfiltration, exploitation and backdooring activities.<br><br>**Query**: `_path=="conn" \| cut id.orig_h, id.resp_h \| sort \| uniq -c \| sort -r`                                                                                                                                                                                                                                                               |
| **Most Active Ports**             | Suspicious activities are not always detectable in the first place. Attackers use multiple ways of hiding and bypassing methods to avoid detection. However, since the data is evidence, it is impossible to hide the packet traces. Investigating the most active ports will help analysts to detect silent and well-hidden anomalies by focusing on the data bus and used services.<br><br>**Query**: `_path=="conn" \| cut id.resp_p, service \| sort \| uniq -c \| sort -r count`<br>**Query**: `_path=="conn" \| cut id.orig_h, id.resp_h, id.resp_p, service \| sort id.resp_p \| uniq -c \| sort -r` |
| **Long Connections**              | For security analysts, the long connections could be the first anomaly indicator. If the client is not designed to service a continuous service, investigating the connection duration between two IP addresses can reveal possible anomalies like backdoors.<br><br>**Query**: `_path=="conn"\| cut id.orig_h, id.resp_p, id.resp_h, duration \| sort -r duration`                                                                                                                                                                                                                                         |
| **Transferred Data**              | Another essential point is calculating the transferred data size. If the client is not designed to serve and receive files and act as a file server, it is important to investigate the total bytes for each connection. Thus, analysts can distinguish possible data exfiltration or suspicious file actions like malware downloading and spreading.<br><br>**Query**: `_path=="conn" \| put total_bytes := orig_bytes + resp_bytes \| sort -r total_bytes \| cut uid, id, orig_bytes, resp_bytes, total_bytes`                                                                                            |
| **DNS and HTTP Queries**          | Identifying suspicious and out of ordinary domain connections and requests is another significant point for security analysts. Abnormal connections can help detect C2 communications and possible compromised/infected hosts. Identifying the suspicious DNS queries and HTTP requests can help security analysts to detect malware C2 channels and support the investigation hypothesis.<br><br>**Query**: `_path=="dns" \| count () by query \| sort -r`<br>**Query**: `_path=="http"  \|  count () by uri  \| sort -r`                                                                                  |
|                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
# Exercise | Threat Hunting with Brim | C2 Malware Detection

It is just another malware campaign spread with CobaltStrike. We know an employee clicks on a link, downloads a file, and then network speed issues and anomalous traffic activity arises. Now, open Brim, import the sample pcap and go through the walkthrough. 

**Let's investigate the traffic sample to detect malicious C2 activities!**

![Brim - available logs](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/fcae25712f15175255e7d725ff18cccd.png)

Let's look at the available logfiles first to see what kind of data artefact we could have. The image on the left shows that we have many alternative log files we could rely on. Let's review the frequently communicated hosts before starting to investigate individual logs.

**Query**: `cut id.orig_h, id.resp_p, id.resp_h | sort | uniq -c | sort -r count`

> This query provides sufficient data that helped us decide where to focus. The IP addresses "10.22.xx" and "104.168.xx" draw attention in the first place. Let's look at the port numbers and available services before focusing on the suspicious IP address and narrowing our search.

**Query**: `_path=="conn" | cut id.resp_p, service | sort | uniq -c | sort -r count`

> Nothing extremely odd in port numbers, but there is a massive DNS record available. Let's have a closer look.

**Query**: `_path=="dns" | count() by query | sort -r`

> There are out of ordinary DNS queries. Let's enrich our findings by using VirusTotal to identify possible malicious domains.

> We have detected two additional malicious IP addresses (we have the IP 45.147.xx from the log files and gathered the 68.138.xx and 185.70.xx from VirusTotal) linked with suspicious DNS queries with the help of external research. Let's look at the HTTP requests before narrowing down our investigation with the found malicious IP addresses.

**Query**: `_path=="http" | cut id.orig_h, id.resp_h, id.resp_p, method, host, uri | uniq -c | sort value.uri`

> We detect a file download request from the IP address we assumed as malicious. Let's validate this idea with VirusTotal and validate our hypothesis.

VirusTotal results show that the IP address `104.xx` is linked with a file. Once we investigate that file, we discover that these two findings are associated with CobaltStrike. Up to here, we've followed the abnormal activity and found the malicious IP addresses. Our findings represent the C2 communication. Now let's conclude our hunt by gathering the low hanging fruits with Suricata logs.

**Query**: `event_type=="alert" | count() by alert.severity,alert.category | sort count`

Now we can see the overall malicious activities detected by Suricata. Note that you can investigate the rest of the IP addresses to identify the secondary C2 traffic anomaly without using the Suricata logs. This task demonstrates two different approaches to detecting anomalies.

Investigating each alarm category and signature to enhance the threat hunting activities and post-hunting system hardening operations is suggested. Please note, adversaries using CobaltStrike are usually skilled threats and don't rely on a single C2 channel. Common experience and use cases recommend digging and keeping the investigation by looking at additional C2 channels.

This concludes our hunt for the given case. Now, repeat this exercise in the attached VM.
### Answers | Walkthrough

https://haircutfish.com/posts/Brim-Task-6-Exercise-Threat-Hunting-With-Brim-Malware-C2-Detection/

# Threat Hunting with Brim | Crypto Mining

Cryptocurrencies are frequently on the agenda with their constantly rising value and legal aspect. The ability to obtain cryptocurrencies by mining other than purchasing is becoming one of the biggest problems in today's corporate environments.

Attackers not only compromise the systems and ask for a ransom, but sometimes they also install mining tools (cryptojacking). Other than the attackers and threat actors, sometimes internal threats and misuse of trust and privileges end up installing coin miners in the corporate environment. 

Usually, mining cases are slightly different from traditional compromising activities. Internal attacks don't typically contain major malware samples. However, this doesn't mean they aren't malicious as they are exploiting essential corporate resources like computing power, internet, and electricity. 

Also, crypto mining activities require third party applications and tool installations which could be vulnerable or create backdoors. Lastly, mining activities are causing network performance and stability problems. Due to these known facts, coin mining is become one of the most common use cases of threat hunters. 

**Let's investigate a traffic sample to detect coin mining activity.**

Let's look at the available logfiles first to see what kind of data artefact we could have. The image on the left shows that we don't have many alternative log files we could rely on. Let's review the frequently communicated hosts to see if there is an anomaly indicator.

**Query**: `cut id.orig_h, id.resp_p, id.resp_h | sort | uniq -c | sort -r`

This query provided sufficient data that helped us decide where to focus. The IP address `192.168.xx` draws attention in the first place. Let's look at the port numbers and available services before focusing on the suspicious IP address and narrowing our search. 

**Query**: `path=="conn" | cut id.resp_p, service | sort | uniq -c | sort -r count`

> There is multiple weird port usage, and this is not usual. We are one step closer to the identification of the anomaly. Let's look at the transferred data bytes to support our findings and find more indicators. 

**Query**: `_path==-"conn" | put total_bytes := orig_bytes + resp_bytes | sort -r total_bytes | cut uid, id, orig_bytes, resp_bytes, total_bytes`

> The query result proves massive traffic originating from the suspicious IP address. The detected IP address is suspicious. However, we don't have many supportive log files to correlate our findings and detect accompanying activities. 
> 
> At this point, we will hunt the low hanging fruits with the help of Suricata rules. Let's investigate the Suricata logs. 

**Query**: `event_type=="alert" | count() by alert.severity,alert.category | sort count`

> Suricata rules have helped us conclude our hunt quickly, as the alerts tell us we are investigating a "Crypto Currency Mining" activity. Let's dig deeper and discover which data pool is used for the mining activity. 
> 
> First, we will list the associated connection logs with the suspicious IP, and then we will run a VirusTotal search against the destination IP. 

**Query**: `_path=="conn" | 192.168.1.100`

We investigated the first destination IP address and successfully identified the mining server. In real-life cases, you may need to investigate multiple IP addresses to find the event of interest. 

Lastly, let's use Suricata logs to discover mapped out MITRE ATT&CK techniques.

**Query**: `event_type=="alert" | cut alert.category, alert.metadata.mitre_technique_name, alert.metadata.mitre_technique_id, alert.metadata.mitre_tactic_name | sort | uniq -c`

Now we can identify the mapped out MITRE ATT&CK details as shown in the table below.

|   |   |   |   |
|---|---|---|---|
|Suricata Category|MITRE Technique Name|MITRE Technique Id|MITRE Tactic Name|
|Crypto Currency Mining|Resource_Hijacking|T1496|Impact|





