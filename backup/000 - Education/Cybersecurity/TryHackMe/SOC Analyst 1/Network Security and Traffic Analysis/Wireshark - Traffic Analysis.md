# Introduction

In this room, we will cover the techniques and key points of traffic analysis with Wireshark and detect suspicious activities. Note that this is the third and last room of the Wireshark trio.

In the first two rooms, we have covered how to use Wireshark and do packet-level searches. Now, it is time to investigate and correlate the packet-level information to see the big picture in the network traffic, like detecting anomalies and malicious activities. For a security analyst, it is vital to stop and understand pieces of information spread in packets by applying the analyst's knowledge and tool functionality. This room will cover investigating packet-level details by synthesising the analyst knowledge and  Wireshark functionality for detecting anomalies and odd situations for a given case.
## Nmap Scans

**Nmap** is an industry-standard tool for mapping networks, identifying live hosts and discovering the services. As it is one of the most used network scanner tools, a security analyst should identify the network patterns created with it. This section will cover identifying the most common Nmap scan types.

- TCP connect scans
- SYN scans
- UDP scans

It is essential to know how Nmap scans work to spot scan activity on the network. However, it is impossible to understand the scan details without using the correct filters. Below are the base filters to probe Nmap scan behavior on the network.

**TCP flags in a Nutshell**.

| Notes                                                                                        | Wireshark Filters                                                              |
| -------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| Global Search                                                                                | > `tcp`<br><br>> `udp`                                                         |
| > Only SYN flag<br><br>> SYN Flag is set. The rest of the bits are not important.            | > `tcp.flags == 2`<br><br>> `tcp.flags.syn == 1`                               |
| > Only ACK flag.<br><br>> ACK flag is set. The rest of the bits are not important.           | > `tcp.flags == 16`<br><br>> `tcp.flags.ack == 1`                              |
| > Only SYN, ACK flags.<br><br>> SYN and ACK are set. The rest of the bits are not important. | > `tcp.flags == 18`<br><br>> `(tcp.flags.syn == 1) and (tcp.flags.ack == 1)`   |
| > Only RST flag.<br><br>> RST Flag is set. The rest of the bits are not important.           | > `tcp.flags == 4`<br><br>> `tcp.flags.reset == 1`                             |
| > Only RST, ACK flags.<br><br>> RST and ACK flags are set, rest of the bits not important.   | > `tcp.flags == 20`<br><br>> `(tcp.flags.reset == 1) and (tcp.flags.ack == 1)` |
| > Only FIN flag<br><br>> FIN flag is set. The rest of the bits are not important.            | > `tcp.flags == 1`<br><br>> `tcp.flags.fin == 1`                               |
### TCP Connect Scans

**TCP Connect Scan in a Nutshell**:

- Relies on the three-way handshake (needs to finish handshake process)
- Usually conducted with `nmap -sT` command.
- Used by non-privileged users (only option for a non-root user)
- Usually has a windows size larger than 1024 bytes as the request expects some data due to the nature of the protocol.

| **Open TCP Port**                        | **Open TCP Port  <br>**                                    | **Closed TCP Port** |
| ---------------------------------------- | ---------------------------------------------------------- | ------------------- |
| - SYN --><br>- <-- SYN, ACK<br>- ACK --> | - SYN --><br>- <-- SYN, ACK<br>- ACK --><br>- RST, ACK --> | - SYN --><br>- <--  |
The images below show the three-way handshake process of the open and close TCP ports. Images and pcap samples are split to make the investigation easier and understand each case's details.
#### Open TCP Port (Connect)

#### Closed TCP Port (Connect)

> The above images provide the patterns in isolated traffic. However, it is not always easy to spot the given patterns in  big capture files. Therefore analysts need to use a generic filter to view the initial anomaly patterns, and then it will be easier to focus on a specific traffic point. The given filter shows the TCP Connect scan patterns in a capture file. 

```
tcp.flags.syn==1 and tcp.flags.ack==0 and tcp.window_size > 1024
```
### SYN Scans

**SYN Scans in a Nutshell**: 

- Doesn't rely on the three-way handshake (no need to finish handshake process)
- Usually conducted with `nmap -sS` command.
- Used by privileged users.
- Usually has a size less than or equal to 1024 bytes as the request *is not finished* and it doesn't expect to receive data.

|   |   |
|---|---|
|**Open TCP Port**|**Close TCP Port**|
|- SYN --><br>- <-- SYN,ACK<br>- RST-->|- SYN --><br>- <-- RST,ACK|#
#### Open TCP Port (SYN)

#### Closed TCP Port (SYN)

> The given filter shows the TCP SYN scan patterns in a capture file.

```
`tcp.flags.syn==1 and tcp.flags.ack==0 and tcp.window_size <= 1024`
```
### UDP Scans

**UDP Scans in a Nutshell**:

- Doesn't require a handshake process
- No prompt for open ports
- ICMP error message for closed ports
- Usually conducted with `nmap -sU` command

| Open UDP Port    | Closed UDP Port                                                                                |
| ---------------- | ---------------------------------------------------------------------------------------------- |
| - UDP packet --> | - UDP packet --><br>- ICMP Type 3, Code 3 message. (Destination unreachable, port unreachable) |

The above image shows that the closed port returns an ICMP error packet. No further information is provided about the error at first glance, so how can an analyst decide where this error message belongs? The ICMP error message uses the original request as encapsulated data to show the source/reason of the packet. Once you expand the ICMP section in the packet details pane, you will see the encapsulated data and the original request, as shown in the below image.

> The given filter shows the UDP scan patterns in a capture file.

```
icmp.type==3 and icmp.code==3
```

Detecting suspicious activities in chunked files is easy and a great way to learn how to focus on the details. Now use the exercise files to put your skills into practice against a single capture file and answer the questions below!

# Arp Poisoning | Man in the Middle

**ARP** protocol, or **Address Resolution Protocol** is the technology responsible for allowing devices to identify themselves on a network. Address Resolution Protocol Poisoning (also known as ARP Spoofing or Man in the Middle) is a type of attack that involves network jamming/manipulating by sending malicious ARP packets to the default gateway. 

> The ultimate aim is to manipulate the **IP to MAC Address table** and sniff the traffic of the target host.

There are a variety of tools available to conduct ARP attacks. However, the mindset of the attack is static, so it is easy to detect such an attack by knowing the ARP protocol workflow and Wireshark skills. 

**ARP Analysis in a Nutshell**

- Works on the local network
- Enables the communication between MAC addresses
- Not a secure protocol
- Not a routable protocol
- It doesn't have an authentication function
- Common patterns are request & response, announcement and gratuitous packets.

Before investigating the traffic, let's review some legitimate and suspicious ARP packets. The legitimate requests are similar to the shown picture: a broadcast request that asks if any of the available hosts use an IP address and a reply from the host that uses the requested IP address.

| Notes                                           | Wireshark Filter                                                       |
| ----------------------------------------------- | ---------------------------------------------------------------------- |
| Global Search                                   | `arp`                                                                  |
| Opcode 1: Arp Requests                          | `arp.opcode == 1`                                                      |
| Opcode 2: Arp Responses                         | `arp.opcode == 2`                                                      |
| **Hunt**: ARP scanning                          | `arp.dst.hw_mac == 00:00:00:00:00:00`                                  |
| **Hunt:** Possible ARP Poisoning                | `arp.duplicate-address-detected or arp.dupiclicate-address-frame`      |
| **Hunt**: Possible ARP flooding from detection. | `((arp)) && (op.code == 1)) && (arp.src.hw_mac == target-mac-address)` |

> A suspicious situation means having two different ARP responses (conflict) for a particular IP address. In that case, Wireshark's expert info tab warns the analyst. However, it only shows the second occurrence of the duplicate value to highlight the conflict. Therefore, identifying the malicious packet from the legitimate one is the analyst's challenge. A possible spoofing case is shown in the picture below:

Here, knowing the network architecture and inspecting the traffic for a specific time frame can help detect the anomaly. As an analyst, you should take notes of your findings before going further. This will help you be organized and make it easier to correlate the further findings. 

Look at the given picture; there is a conflict, the MAC address that ends with `b4` crafted an ARP request with the `192.168.1.25` IP address, then claimed to have the `192.168.1.1` IP address.

| Notes                         | Detection Notes                                                                                                           | Findings                                                |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| Possible IP address match     | 1 IP address announced from a MAC Address                                                                                 | - MAC: 00:0c:29:e2:18:b4<br>- IP: 192.168.1.25          |
| Possible ARP spoofing attempt | 2 MAC addresses claimed the same IP address (192.168.1.1) <br>The `192.168.1.1` IP address is a possible gateway address. | - MAC1: 50:78:b3:f3:cd:f4<br>- MAC 2: 00:0c:29:e2:18:b4 |
| Possible ARP Flooding attempt | The MAC address that ends with `b4` claims to have a different/new IP address                                             | - MAC: 00:0c:29:e2:18:b4<br>- IP: 192.168.1.1           |
Let's keep an eye on the traffic to spot any other anomalies. Note that the case is split into multiple capture files to make the investigation easier.

![Wireshark - arp flood](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/e02a42c9d4e3f17a94acbae4cacb6b65.png)

At this point, it is evident that there is an anomaly. A security analyst *cannot ignore a flood of ARP requests*. This could be malicious activity, scan or network problems. There is a new anomaly; the MAC address that ends with `b4` crafted multiple ARP requests with the `192.168.1.25` IP address. Let's focus on the source of this anomaly and extend the taken notes. 

| Notes                         | Detection Notes                                                                                                           | Findings                                                |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| Possible IP address match     | 1 IP address announced from a MAC Address                                                                                 | - MAC: 00:0c:29:e2:18:b4<br>- IP: 192.168.1.25          |
| Possible ARP spoofing attempt | 2 MAC addresses claimed the same IP address (192.168.1.1) <br>The `192.168.1.1` IP address is a possible gateway address. | - MAC1: 50:78:b3:f3:cd:f4<br>- MAC 2: 00:0c:29:e2:18:b4 |
| Possible ARP Flooding attempt | The MAC address that ends with `b4` claims to have a different/new IP address                                             | - MAC: 00:0c:29:e2:18:b4<br>- IP: 192.168.1.1           |
| Possible ARP flooding attempt | The MAC address that ends with `b4` crafted multiple ARP requests against a range of IP addresses                         | - MAC: 00:0c:29:e2:18:b4<br>- IP: 192.168.1.xxx         |
Up to this point, it is evident that the MAC address that ends with `b4` owns the `192.168.1.25` IP address and crafted suspicious ARP requests against a range of IP addresses. It also claimed to have the possible gateway address as well. Let's focus on other protocols and spot the reflection of this anomaly in the following sections of the time frame.

![Wireshark - arp spoof mitm http view-1](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/f55ebc1632f6776e074dc29842221b48.png)

There is HTTP traffic, and everything looks normal at the IP level, so there is no linked information with our previous findings. Let's add the MAC addresses as columns in the packet list pane to reveal the communication behind the IP addresses.

![Wireshark - arp spoof mitm http view-2](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/f885817e77449e6898ba3ede164723c4.png)

One more anomaly. The MAC address that ends with `b4` is the destination of all HTTP packets. It is evident that there is a MITM attack, and the attacker is the host with the MAC address ending in `b4`. All traffic linked to `192.168.1.12` IP addresses is forwarded to the malicious host. Let's summarize the findings before concluding the investigation.

| Detection Notes   | Findings                                       |                                                                                                                                         |
| ----------------- | ---------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| IP to MAC matches | 3 IP to MAC address matches                    | - MAC: 00:0c:29:e2:18:b4 = IP: 192.168.1.25<br>- MAC: 50:78:b3:f3:cd:f4 = IP: 192.1681.1<br>- MAC: 00:0c:29:98:c7:a8 = IP: 192.168.1.12 |
| Attacker          | The attacker created noise with ARP Packets    | MAC: 00:0c:29:e2:18:b4 = IP: 192.168.1.25                                                                                               |
| Router/gateway    | Gateway Address                                | MAC: 50:78:b3:f3:cd:f4 = IP: 192.1681.1                                                                                                 |
| Victim            | The attacker sniffed all traffic of the victim | MAC: 50:78:b3:f3:cd:f4 = IP: 192.1681.12                                                                                                |
Detecting these bits and pieces of information in a big capture file is challenging. However, in real-life cases, you will not have **tailored data** ready for investigation. Therefore you need to have the analyst mindset, knowledge and tool skills to filter and detect the anomalies.

> [!NOTE] Note
> In traffic analysis, there are always alternative solutions available. The solution type and the approach depend on the analyst's knowledge and skill level and the available data sources.
>

Detecting suspicious activities in chunked files is easy and a great way to learn how to focus on the details.

# Identifying Hosts | DHCP, NetBIOS and Kerberos

When investigating a compromise or malware infection activity, a security analyst should know how to identify the hosts on the network apart from IP to MAC address match. One of the best methods is identifying the hosts and users on the network to decide the investigation's starting point and list the hosts and users associated with the malicious traffic/activity.

Usually, enterprise networks use a predefined pattern to name users and hosts. While this makes knowing and following the inventory easier, it has good and bad sides. The good side is that it will be easy to identify a user or host by looking at the name. The bad side is that it will be easy to clone that pattern and live in the enterprise network for adversaries. *There are multiple solutions to avoid these kinds of activities, but for a security analyst, it is still essential to have host and user identification skills.* 
Protocols that can be used in Host and User Identification:

- Dynamic Host Configuration Protocol (DHCP)
- NetBIOS (NBNS) traffic
- Kerberos traffic

## DHCP Analysis

**DHCP** protocol is the technology responsible for managing automatic IP address and required communication parameters assignment.

**DHCP Analysis In a Nutshell**

| Notes                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Wireshark Filter                                                                                                                                                                                                                        |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Global Search                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | `dhcp` or `bootp`                                                                                                                                                                                                                       |
| Filtering the proper DHCP packet options is vital to finding an event of interest.   <br>  <br><br>- **"DHCP Request"** packets contain the hostname information<br>- **"DHCP ACK"** packets represent the accepted requests<br>- **"DHCP NAK"** packets represent denied requests<br><br>Due to the nature of the protocol, only "Option 53" ( request type) has predefined static values. You should filter the packet type first, and then you can filter the rest of the options by "applying as column" or use the advanced filters like "contains" and "matches". | Request: `dhcp.option.dhcp==3`<br>ACK: `dhcp.option.dhcp ==5`<br>NAK: `dhcp.option.dhcp==6`                                                                                                                                             |
| **"DHCP Request"** options for grabbing the low-hanging fruits:<br><br>- **Option 12:** Hostname.<br>- **Option 50:** Requested IP address.<br>- **Option 51:** Requested IP lease time.<br>- **Option 61:** Client's MAC address.                                                                                                                                                                                                                                                                                                                                      | `dhcp.option.hostname contains "keyword"`                                                                                                                                                                                               |
| **"DHCP ACK"** options for grabbing the low-hanging fruits:<br><br>- **Option 15:** Domain name.<br>- **Option 51:** Assigned IP lease time.                                                                                                                                                                                                                                                                                                                                                                                                                            | `dhcp.option.domain_name contains "keyword"`                                                                                                                                                                                            |
| **"DHCP NAK"** options for grabbing the low-hanging fruits:<br><br>- **Option 56:** Message (rejection details/reason).                                                                                                                                                                                                                                                                                                                                                                                                                                                 | As the message could be unique according to the case/situation, it is suggested to read the message instead of filtering it. Thus, the analyst could create a more reliable hypothesis/result by understanding the event circumstances. |
## NetBIOS Analysis

**NetBIOS** or **Network Basic Input/Output System** is the technology responsible for allowing applications on different hosts to communicate with each other.

**NBNS** investigation in a nutshell:

| Notes                                                             | Wireshark Filter               |
| ----------------------------------------------------------------- | ------------------------------ |
| Global Search                                                     | `nbns`                         |
| **NBNS** options for grabbing the low-hanging fruits:             | `nbns.name contains "keyword"` |
| Queries: query details                                            |                                |
| Query details could contain **name, TTL and IP address details**. |                                |
## Kerberos Analysis

**Kerberos** is the default authentication service for Microsoft Windows domains. It is responsible for authenticating service requests between two or more computers over the untrusted network. The ultimate aim is to prove identity securely. 

**Kerberos investigation in a nutshell**:

| **Notes**                                                                                                                                                                                                                                                                                                                                                                           | **Wireshark Filter**                                                                                               |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| Global search.                                                                                                                                                                                                                                                                                                                                                                      | - `kerberos`                                                                                                       |
| User account search:<br><br>- **CNameString:** The username.<br><br>**Note:** Some packets could provide hostname information in this field. To avoid this confusion, filter the **"$"** value. The values end with **"$"** are hostnames, and the ones without it are user names.                                                                                                  | - `kerberos.CNameString contains "keyword"` <br>- `kerberos.CNameString and !(kerberos.CNameString contains "$" )` |
| "Kerberos" options for grabbing the low-hanging fruits:<br><br>- **pvno:** Protocol version.<br>- **realm:** Domain name for the generated ticket.  <br>    <br>- **sname:** Service and domain name for the generated ticket.<br>- **addresses:** Client IP address and NetBIOS name.  <br>    <br><br>**Note:** the "addresses" information is only available in request packets. | - `kerberos.pvno == 5`<br><br>- `kerberos.realm contains ".org"` <br><br>- `kerberos.SNameStrin`                   |

> Detecting suspicious activities in chunked files is easy and a great way to learn how to focus on the details. 

# Tunnelling Traffic: DNS and ICMP

Traffic Tunnelling is (also known as **Port Forwarding**) transferring the data/resources in a secure method to network segments and zones. It cna be used for "internet to private networks" and "private networks to internet" flow/direction. There is an encapsulation process to hide the data, so the transferred data appear natural for the case, but it contains private data packets and transfers them to the final destination securely. 

Tunnelling provides *anonymity* and *traffic security*. Therefore it is highly used by enterprise networks. However, as it gives a significant level of data encryption, attackers use tunnelling to bypass security permitters using the **standard and trusted protocols** used in everyday traffic like ICMP and DNS. Therefore, for a security analyst, it is crucial to have the ability to spot ICMP and DNS anomalies.
## ICMP Analysis

Internet Control Message Protocol (ICMP) is designed for diagnosing and reporting *network communication issues*. It is highly used in error reporting and testing. As it is a trusted network layer protocol, sometimes it is used for denial of service attacks, also, adversaries use it in data exfiltration and C2 tunnelling activities.

**ICMP Analysis In a Nutshell**:

Usually, ICMP tunnelling attacks are anomalies appearing/starting after a malware execution or vulnerability exploitation. As the ICMP packets can transfer an additional data payload, adversaries use this section to exfiltrate data and establish a C2 connection. It could be a **TCP, HTTP or SSH** data. As the ICMP protocols provide a great opportunity to carry extra data, it also has disadvantages. Most enterprise networks block custom packets or require administrator privileges to create custom ICMP packets. 

A large volume of ICMP packets or anomalous packet sizes are indicators of ICMP tunnelling. Still, the adversaries could create custom packets that match the regular ICMP packet size (64 bytes), so it is still cumbersome to detect these tunnelling activities. However, a security analyst should know the normal and abnormal to spot the possible anomaly and escalate it for further analysis.

| Notes                                                | Wireshark Filters        |
| ---------------------------------------------------- | ------------------------ |
| Global Search                                        | `icmp`                   |
| **IMCP** options for grabbing the low hanging fruit: | `data.len > 64 and icmp` |
| packet length                                        |                          |
| ICMP destination addess                              |                          |
| Encapsulated protocols signs in ICMP payload         |                          |

## DNS Analysis

Domain Name System (DNS) is designed to translate/convert IP domain addresses to IP addresses. It is also known as a **phonebook of the internet**. As it is essential part of the web service, it is commonly used and trusted, and therefore often ignored. Due to that, adversaries use it in data exfiltration and C2 activities.

**DNS Analysis in a Nutshell**:

Similar to ICMP tunnels, DNS attacks are anomalies appearing/starting after a malware execution or vulnerability exploitation. Adversaries create (or have created) a domain address and configures it as a C2 channel. The malware or the commands executed after exploitation sends DNS queries to the C2 server. 

However, these queries are **longer than default DNS queries and crafted for subdomain addresses**. *Unfortunately, these subdomain addresses are not actual addresses; they are encoded commands as shown below:*

`"encoded-commands.maliciousdomain.com"`

When this query is routed to the C2 server, the server sends the actual malicious commands to the host. As the DNS queries are a natural part of the networking activity, these packets have the chance of not being detected by network perimeters. A security analyst should know how to investigate the DNS packet lengths and target addresses to spot these anomalies.

| Notes                                                                                                                                                                                                                                                                                                                                                                                     | Wireshark Filter                                                     |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| Global Search                                                                                                                                                                                                                                                                                                                                                                             | `dns`                                                                |
| "DNS" options for grabbing the low-hanging fruits:<br><br>- Query length.<br>- Anomalous and non-regular names in DNS addresses.<br>- Long DNS addresses with encoded subdomain addresses.<br>- Known patterns like dnscat and dns2tcp.<br>- Statistical analysis like the anomalous volume of DNS requests for a particular target.<br><br>**!mdns:** Disable local link device queries. | - `dns contains "dnscat"`<br><br>- `dns.qry.name.len > 15 and !mdns` |

![](https://i.imgur.com/TcrwLLX.png)

# Cleartext Protocol Analysis | FTP

Investigating cleartext protocol traces sounds easy, but when the time comes to investigate a big network trace for incident analysis and response, the game changes. Proper analysis is more than following the stream and reading the cleartext data. For a security analyst, it is important to create statistics and key results from the investigation process. As mentioned earlier at the beginning of the Wireshark room series, the analyst should have the required network knowledge and tool skills to accomplish this. 
## FTP Analysis

**File Transfer Protocol (FTP)** is designed to transfer files with ease, so it focuses on simplicity rather than security. As a result of this, using this protocol in unsecured environments could create security issues like:

- MITM Attacks
- Credential stealing and unauthorized access
- Phishing
- Malware planting
- Data exfiltration

| Notes                                                                                                                                                                                                                                                   | Wireshark Filter                                                                                                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Global Search                                                                                                                                                                                                                                           | `ftp`                                                                                                                                                                                       |
| **"FTP"** options for grabbing the low-hanging fruits:<br><br>- **x1x series:** Information request responses.<br>- **x2x series:** Connection messages.<br>- **x3x series:** Authentication messages.<br><br>**Note:** "200" means command successful. | ---                                                                                                                                                                                         |
| "x1x" series options for grabbing the low-hanging fruits:<br><br>- **211:** System status.<br>- **212:** Directory status.<br>- **213:** File status                                                                                                    | `ftp.response.code == 211`                                                                                                                                                                  |
| "x2x" series options for grabbing the low-hanging fruits:<br><br>- **220:** Service ready.<br>- **227:** Entering passive mode.<br>- **228:** Long passive mode.<br>- **229:** Extended passive mode.                                                   | `ftp.response.code == 227`                                                                                                                                                                  |
| "x3x" series options for grabbing the low-hanging fruits:<br><br>- **230:** User login.<br>- **231:** User logout.<br>- **331:** Valid username.<br>- **430:** Invalid username or password<br>- **530:** No login, invalid password.                   | `ftp.response.code == 230`                                                                                                                                                                  |
| "FTP" commands for grabbing the low-hanging fruits:<br><br>- **USER:** Username.<br>- **PASS:** Password.<br>- **CWD:** Current work directory.<br>- **LIST:** List.                                                                                    | `ftp.request.command == "USER"`<br><br>`ftp.request.command == "PASS"`<br><br>`ftp.request.command == "password"`                                                                           |
| Advanced usages examples for grabbing low-hanging fruits:<br><br>- **Bruteforce signal:** List failed login attempts.<br>- **Bruteforce signal:** List target username.<br>- **Password spray signal:** List targets for a static password.             | `ftp.response.code == 530`<br><br>- `(ftp.response.code == 530) and (ftp.response.arg contains "username")`<br><br>- `(ftp.request.command == "PASS" ) and (ftp.request.arg == "password")` |
|                                                                                                                                                                                                                                                         |                                                                                                                                                                                             |

![](https://i.imgur.com/wXKvEDD.png)

# Cleartext Protocol Analysis | HTTP

Hypertext Transfer Protocol is a cleartext based, request-response and client-server protocol. It is the standard type of network activity to request/serve web pages, and by default, it is not blocked by any network perimeter. As a result of being unencrypted and the backbone of web traffic, **HTTP is one of the must-know protocols in traffic analysis.** 

The following attacks can be prevented with the help of HTTP analysis:

- Phishing pages
- Web attacks
- Data exfiltration
- Command and control traffic (C2)

|   |   |
|---|---|
|**Notes**|**Wireshark Filter**|
|Global search<br><br>**Note:** HTTP2 is a revision of the HTTP protocol for better performance and security. It supports binary data transfer and request&response multiplexing.|- `http`<br><br>- `http2`|
|"HTTP **Request Methods"** for grabbing the low-hanging fruits:<br><br>- GET<br>- POST<br>- Request: Listing all requests|- `http.request.method == "GET"`<br><br>- `http.request.method == "POST"`<br><br>- `http.request`|
|"HTTP Response Status Codes" for grabbing the low-hanging fruits:<br><br>- **200 OK:** Request successful.<br>- **301 Moved Permanently:** Resource is moved to a new URL/path (permanently).<br>- **302 Moved Temporarily:** Resource is moved to a new URL/path (temporarily).<br>- **400 Bad Request:** Server didn't understand the request.<br>- **401 Unauthorised:** URL needs authorisation (login, etc.).<br>- **403 Forbidden:** No access to the requested URL. <br>- **404 Not Found:** Server can't find the requested URL.<br>- **405 Method Not Allowed:** Used method is not suitable or blocked.<br>- **408 Request Timeout:**  Request look longer than server wait time.<br>- **500 Internal Server Error:** Request not completed, unexpected error.<br>- **503 Service Unavailable:** Request not completed server or service is down.|- `http.response.code == 200`<br><br>- `http.response.code == 401`<br><br>- `http.response.code == 403`<br><br>- `http.response.code == 404`<br><br>- `http.response.code == 405`<br><br>- `http.response.code == 503`|
|"HTTP Parameters" for grabbing the low-hanging fruits:<br><br>- **User agent:** Browser and operating system identification to a web server application.<br>- **Request URI:** Points the requested resource from the server.  <br>    <br>- **Full *URI:** Complete URI information.<br><br>***URI:** Uniform Resource Identifier.|- `http.user_agent contains "nmap"`<br><br>- `http.request.uri contains "admin"`<br><br>- `http.request.full_uri contains "admin"`|
|"HTTP Parameters" for grabbing the low-hanging fruits:<br><br>- **Server:** Server service name.  <br>    <br>- **Host:** Hostname of the server<br>- **Connection:** Connection status.  <br>    <br>- **Line-based text data:** Cleartext data provided by the server.<br>- **HTML Form URL Encoded:** Web form information.|- `http.server contains "apache"`<br><br>- `http.host contains "keyword"`<br><br>- `http.host == "keyword"`<br><br>- `http.connection == "Keep-Alive"`<br><br>- `data-text-lines contains "keyword"`|
## User Agent Analysis

As the adversaries use sophisticated techniques to accomplish attacks, they try to leave traces similar to natural traffic through the known and trusted protocols. For a security analyst, it is important to spot the anomaly signs on the bits and pieces of the packets. The "user-agent" field is one of the great resources for spotting anomalies in HTTP traffic. In some cases, *adversaries successfully modify the user agent data, which could look super natural.* 

A security analyst cannot rely on the user-agent field to spot an anomaly. Never whitelist a user-agent, even if it looks natural. User agent-based anomaly/threat detection/hunting is an additional data source to check and is useful when there is an obvious anomaly. If you are unsure about a value, you can conduct a web search to validate your findings with the default and normal user-agent info ([**example site**](https://developers.whatismybrowser.com/useragents/explore/)).

**User Agent analysis in a nutshell:**  

|                                                                                                                                                                                                                                                                                                                                                                                                                      |                                                                                                                                                          |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Notes**                                                                                                                                                                                                                                                                                                                                                                                                            | **Wireshark Filter**                                                                                                                                     |
| Global search.                                                                                                                                                                                                                                                                                                                                                                                                       | - `http.user_agent`                                                                                                                                      |
| Research outcomes for grabbing the low-hanging fruits:<br><br>- Different user agent information from the same host in a short time notice.<br>- Non-standard and custom user agent info.<br>- Subtle spelling differences. **("Mozilla" is not the same as  "Mozlilla" or "Mozlila")**<br>- Audit tools info like Nmap, Nikto, Wfuzz and sqlmap in the user agent field.<br>- Payload data in the user agent field. | - `(http.user_agent contains "sqlmap") or (http.user_agent contains "Nmap") or (http.user_agent contains "Wfuzz") or (http.user_agent contains "Nikto")` |

![](https://i.imgur.com/Zzf3AuN.png)

## Log4j Analysis

A proper investigation starts with prior research on threats and anomalies going to be hunted. Let's review the knowns on the `Log4j` attack before launching Wireshark.

Log4j vulnerability analysis in a nutshell:  

![](https://i.imgur.com/W8Kwxng.png)

|   |   |
|---|---|
|**Notes**|**Wireshark Filters**|
|**Research outcomes** for grabbing the low-hanging fruits:<br><br>- The attack starts with a "POST" request<br>- There are known cleartext patterns: "**jndi:ldap**" and "**Exploit.class**".|- `http.request.method == "POST"`<br><br>- `(ip contains "jndi") or ( ip contains "Exploit")`<br><br>- `(frame contains "jndi") or ( frame contains "Exploit")`<br><br>- `(http.user_agent contains "$") or (http.user_agent contains "==")`|
# Encrypted Protocol Analysis | Decrypting HTTPS

When investigating web traffic, analysts often run across encrypted traffic. This is caused by using the Hypertext Transfer Protocol Secure protocol for enhanced security against spoofing, sniffing and intercepting attacks. HTTPS uses TLS protocol to encrypt communications, so it is impossible to decrypt the traffic and view the transferred data without having the encryption/decryption key pairs. 

As this protocol provides a good level of security for transmitting sensitive data, attackers and malicious websites also use HTTPS. Therefore, a security analyst should know how to use key files to decrypt encrypted traffic and investigate the traffic activity.

The packets will appear in different colors as the HTTP traffic is encrypted. Also, protocol and info details (actual URL address and data returned from the server) will not be fully visible. The first image below shows the HTTP packets encrypted with the TLS protocol. The second and third images demonstrate filtering HTTP packets without using a key log file.

**Additional Information for HTTPS**:

|   |   |
|---|---|
|Notes|Wireshark Filter|
|"HTTPS Parameters" for grabbing the low-hanging fruits:<br><br>- **Request:** Listing all requests  <br>    <br>- **TLS:** Global TLS search<br>- TLS Client Request<br>- TLS Server response<br>- Local Simple Service Discovery Protocol (SSDP)<br><br>**Note:** SSDP is a network protocol that provides advertisement and discovery of network services.|- `http.request`<br><br>- `tls`<br><br>- `tls.handshake.type == 1`<br><br>- `tls.handshake.type == 2`<br><br>- `ssdp`|
![](https://i.imgur.com/MAiZcdP.png)

> Similar to the TCP three-way handshake process, the TLS protocol has its handshake process. The first two steps contain "Client Hello" and "Server Hello" messages. The given filters show the initial hello packets in a capture file. These filters are helpful to spot which IP addresses are involved in the TLS handshake.

- Client Hello: `(http.request or tls.handshake.type == 1) and !(ssdp)`
- Server Hello: `(http.request or tls.handshake.type == 2) and !(ssdp)`

![](https://i.imgur.com/XXT5FMf.jpeg)

An encryption key log file is a text file that contains unique key pairs to decrypt the encrypted traffic session. These key pairs are automatically created (per session) when a connection is established with an SSL/TLS-enabled webpage. As these processes are all accomplished in the browser, you need to configure your system and use a suitable browser (Chrome and Firefox support this) to save these values as a *key log file*.

To do this, you will need to set up an environment variables and create the `SSLKEYLOGFILE`, and the browser will dump the keys to this file as you browse the web. SSL/TLS key pairs are created **per session** at the connection time, *so it is important to dump the keys during the traffic capture.* 

Otherwise, it is not possible to create/generate a suitable key log file to decrypt captured traffic. You can use the **right-click** menu or **Edit -> Preferences -> Protocols -> TLS** menu to add/remove key log files.

> **Adding key log files with the "right-click" menu:**

![](https://i.imgur.com/9jEsgHY.png)

> **Adding key log files with the "Edit --> Preferences --> Protocols --> TLS" menu:**

![](https://i.imgur.com/XhlBoXa.png)

> **Viewing the Traffic With/Without Key Log Files**

![](https://i.imgur.com/PzjLNhw.png)

> The above image shows that the traffic details are visible after using the key log file. Note that the packet details and bytes pane provides the data in different formats for investigation. Decompressed header info and HTTP2 packet details are available after decrypting the traffic. Depending on the packet details, you can slo have the following data formats:

- Frame
- Decrypted TLS
- Decompressed Header
- Reassembled TCP
- Reassembled SSL

# Bonus: Hunt Cleartext Credentials

Up to here, we discussed how to inspect the packets for specific conditions and spot anomalies. As mentioned in the first room, **Wireshark is not an IDS**, but it provides suggestions for some cases under the expert info. However, sometimes anomalies replicate the legitimate traffic, so the detection becomes harder. 

For example, in a cleartext credential hunting case, it is not easy to spot the multiple credential inputs and decide if there is a brute-force attack or if it is a standard user who mistyped their credentials. 

As everything is presented *at the packet level*, it is hard to spot the multiple username/password entries at first glance. The detection time will decrease when an analyst can view the credential entries as a list. Wireshark has such a feature to help analysts who want to hunt cleartext credential entries.

Some Wireshark dissectors (FTP, HTTP, IMAP, pop and SMTP) are programmed to extract cleartext passwords from the capture file. You can view detected credentials using the **Tools -> Credentials** menu. This feature works only after specific versions of Wireshark (v3.1) and later. Since the feature works only with particular protocols, it is suggested to have manual checks and not rely entirely on this feature to decide if there is a cleartext credential in the traffic. 

Once you use the feature, it will open a new window and provide detected credentials. It will show the packet number, protocol, username and additional information. This window is clickable; clicking on the packet number wil select the packet containing the password, and clicking on the username will select the packet containing the username info. The additional part prompts the packet number that contains the username. 

![](https://i.imgur.com/x6rZkpY.png)

# Bonus | Actionable Results

You have investigated the traffic, detected anomalies and created notes for further investigation. What is next? Not every case investigation is carried out by a crowd team. As a security analyst, there will be some cases you need to spot the anomaly, identify the source and take action. Wireshark is not all about packet details; it can help you to create firewall rules ready to implement with a couple of clicks. You can create firewall rules by using the **"Tools --> Firewall ACL Rules"** menu. Once you use this feature, it will open a new window and provide a combination of rules (IP, port and MAC address-based) for different purposes. Note that these rules are generated for implementation on an outside firewall interface.  

Currently, Wireshark can create rules for:

- Netfilter (iptables)
- Cisco IOS (standard/extended)
- IP Filter (ipfilter)
- IPFirewall (ipfw)
- Packet filter (pf)
- Windows Firewall (netsh new/old format)

