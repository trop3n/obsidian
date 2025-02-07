In our first room, [TShark: The Basics](https://tryhackme.com/room/tsharkthebasics), we covered the fundamentals of TShark by focusing on how it operates and how to use it to investigate traffic captures. In this room, we will cover advanced features of TShark by focusing on translating Wireshark GUI features to the TShark CLI and investigate events of interest.

To start the VM, press the green **Start Machine** button attached to this task. The machine will start in split view. In case it is not showing up, you can press the blue **Show Split View** button at the top of the page.

The task files for this room are located in the following directory:

- `~/Desktop/exercise-files`

# Command-Line Wireshark Features I | Statistics

At the beginning of the module, we mentioned that TShark is considered a command line version of Wireshark. In addition to sharing the same display filters, TShark can accomplish several features of Wireshark explained below:

Three important points when using Wireshark-like features:

- These options are applied to all packets in scope unless a display filter is provided.
- Most of the commands shown below are CLI versions of the Wireshark features discussed in [Wireshark: Packet Operations](https://tryhackme.com/room/wiresharkpacketoperations) (Task 2).
- TShark explains the parameters used at the beginning of the output line.
	- For example, you will use the `phs` option to view the protocol hierarchy.

| **Parameter** | **Purpose**                                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| --color       | - Wireshark-like colourised output.<br>- `tshark --color`                                                                                                                                                                                                                                                                                                                                                      |
| -z            | - Statistics<br>- There are multiple options available under this parameter. You can view the available filters under this parameter with:<br><br>- `tshark -z help`<br><br>- Sample usage.<br><br>- `tshark -z filter`<br><br>- Each time you filter the statistics, packets are shown first, then the statistics provided. You can suppress packets and focus on the statistics by using the `-q` parameter. |
## Colorized Output

TShark can provide colorized outputs to help analysts speed up the analysis and spot anomalies quickly. If you are more of a Wireshark person and feel the need for a Wireshark-style packet highlighting option does that. The color option is activated with the `--color` parameter, as shown below.

```
user@ubuntu$ tshark -r colour.pcap --color
```
![](https://i.imgur.com/3FP2w9I.png)

## Statistics | Protocol Hierarchy

Protocol hierarchy helps analysts to see the protocols used, frame numbers, and size of packets in a tree view based on packet numbers. As it provide a summary of the capture, it can help analysts decide the focus point for an event of interest. Use the `-z io,phs -q` parameters to view the protocol hierarchy.

```
user@ubuntu$ tshark -r demo.pcapng -z io,phs -q =================================================================== 
Protocol Hierarchy Statistics 
Filter:     
eth                                    frames:43 bytes:25091     
  ip                                   frames:43 bytes:25091       
    tcp                                frames:41 bytes:24814         
      http                             frames:4 bytes:2000           
        data-text-lines                frames:1 bytes:214             
          tcp.segments                 frames:1 bytes:214           
        xml                            frames:1 bytes:478             
          tcp.segments                 frames:1 bytes:478       
    udp                                frames:2 bytes:277         
      dns                              frames:2 bytes:277 ===================================================================`
```

> After viewing the entire packet tree, you can focus on a specific protocol as shown below. Add the `udp` keyword to the filter to focus on the UDP protocol.

```
user@ubuntu$ tshark -r demo.pcapng -z io,phs,udp -q =================================================================== 
Protocol Hierarchy Statistics 
Filter: udp    
eth                                    frames:2 bytes:277     
  ip                                   frames:2 bytes:277        
    udp                                frames:2 bytes:277         
      dns                              frames:2 bytes:277 ===================================================================`
```

## Statistics | Packet Lengths Tree

The packet lengths tree view helps analysts to overview the general distribution of packets by size in a tree view. It allows analysts to detect anomalously big and small packets at a glance! Use the `-z plen,tree -q` parameters to view the packet lengths tree.


```shell-session
user@ubuntu$ tshark -r demo.pcapng -z plen,tree -q

=========================================================================================================================
Packet Lengths:
Topic / Item       Count     Average       Min val       Max val     Rate (ms)     Percent     Burst rate    Burst start  
-------------------------------------------------------------------------------------------------------------------------
Packet Lengths     43        583.51        54            1484        0.0014        100         0.0400        2.554        
 0-19              0         -             -             -           0.0000        0.00        -             -            
 20-39             0         -             -             -           0.0000        0.00        -             -            
 40-79             22        54.73         54            62          0.0007        51.16       0.0200        0.911        
 80-159            1         89.00         89            89          0.0000        2.33        0.0100        2.554        
 160-319           2         201.00        188           214         0.0001        4.65        0.0100        2.914        
 320-639           2         505.50        478           533         0.0001        4.65        0.0100        0.911        
 640-1279          1         775.00        775           775         0.0000        2.33        0.0100        2.984        
 1280-2559         15        1440.67       1434          1484        0.0005        34.88       0.0200        2.554        
 2560-5119         0         -             -             -           0.0000        0.00        -             -            
 5120 and greater  0         -             -             -           0.0000        0.00        -             -            
-------------------------------------------------------------------------------------------------------------------------
```

## Statistics | Endpoints

The endpoint statistics view helps analysts to overview the unique endpoints. It also shows the number of packets associated with each endpoint. If you are familiar with Wireshark, you should know that endpoints can be viewed in multiple formats. Similar to Wireshark, TShark supports multiple source filtering options for endpoint identification. Use `-z endpoints,ip -q` parameters to view IP endpoints.

Filter for the most common viewing options are explained below:

| Filter | Purpose                                    |
| ------ | ------------------------------------------ |
| `eth`  | Ethernet address                           |
| `ip`   | IPv4 Address                               |
| `ipv6` | IPv6 address                               |
| `tcp`  | TCP Address, valid for both IPv4 and IPv6. |
| `udp`  | UDP address, valid for both IPv4 and IPv6  |
| `wlan` | IEEE 802.11 addresses                      |
```
user@ubuntu$ tshark -r demo.pcapng -z endpoints,ip -q 
```

## Statistics | Conversions

The conversions view helps analysts to overview the traffic flow between two particular connection points. Similar to endpoint filtering, conversations can be viewed in multiple formats. This filter uses the same parameters as the "Endpoints" option. Use `-z conv,ip -q` parameters to view IP conversations.

```shell-session
user@ubuntu$ tshark -r demo.pcapng -z conv,ip -q  
```

## Statistics | Expert Info

The expert info view helps analysts to view the automatic comments provided by Wireshark. If you are unfamiliar with the "Wireshark Expert Info", visit Task 4 in the [Wireshark: The Basics](https://tryhackme.com/room/wiresharkthebasics) room of the [Wireshark module](https://tryhackme.com/module/wireshark). Use the `-z expert -q` parameters to view the expert information.

```shell-session
user@ubuntu$ tshark -r demo.pcapng -z expert -q
```

# Command Line Wireshark Features II | Statistics II

There are plenty of filters designed for multiple protocols. The common filtering options for specific protocols are explained below. Note that most of the commands below are CLI versions of the Wireshark features discussed in [Wireshark: Packet Operations](https://tryhackme.com/room/wiresharkpacketoperations) (Task 3)

## Statistics | IPv4 and IPv6

This option provides statistics on IPv4 and IPv6 packets, as shown below. Having the protocol statistics helps analysts to overview packet distribution according to the protocol type. You can filter the available protocol types and view the details using the `-z ptype,tree -q` parameters.

```
user@ubuntu$ tshark -r demo.pcapng -z ptype,tree -q
```
![](https://i.imgur.com/vJ6csgC.png)

> Having the summary of the hosts in a single view is useful as well. Especially when you are working with large captures, viewing all hosts with a single command can help you detect an anomalous host at a glance. You can filter all IP addresses using the parameters given below:

- IPv4: `-z ip_hosts,tree -q`
- IPv6: `-z ipv6_hosts,tree -q`

```shell-session
user@ubuntu$ tshark -r demo.pcapng -z ip_hosts,tree -q
```
![](https://i.imgur.com/RtzGQnz.png)

> For complex cases and in-depth analysis, you will need to correlate the finding by focusing on the source and destination addresses. You can filter all source and destination addresses using the parameters given below.

- IPv4: `-z ip_srcdst,tree -q`
- IPv6: `-z ipv6_srcdst,tree -q`

```shell-session
user@ubuntu$ tshark -r demo.pcapng -z ip_srcdst,tree -q
```
![](https://i.imgur.com/peOS4dK.png)

> In some cases, you will need to focus on the outgoing traffic to spot the used services and ports. You can filter all outgoing traffic by using the parameters given below.

IPv4: `-z dests,tree -q`
IPv6: `-z ipv6_dests,tree -q`

```shell-session
user@ubuntu$ tshark -r demo.pcapng -z dests,tree -q
```
![](https://i.imgur.com/pUvSJNT.png)

## Statistics | DNS

This option provides statistics on DNS packets by summarizing the available info. You can filter the packets and view the details using the `-z dns,tree -q` parameters.

```shell-session
user@ubuntu$ tshark -r demo.pcapng -z dns,tree -q
```
![](https://i.imgur.com/VwJc05t.png)

## Statistics | HTTP

This option provides statistics on HTTP packets by summarizing the load distribution, requests, packets, and status info. You can filter the packets and view the details using the parameters given below:

- Packet and Status counter for HTTP: `-z http,tree -q`
- Packet and status counter for HTTP2: `-z http2,tree -q`
- Load distribution: `-z http_srv,tree -q`
- Requests: `-z http_req,tree -q`
- Requests and responses: `-z http_seq,tree -q`

```shell-session
user@ubuntu$ tshark -r demo.pcapng -z http,tree -q
```
![](https://i.imgur.com/C8yRWqn.png)

# Command Line Wireshark Features III | Streams, Objects and Credentials

There are plenty of filters designed for multiple purposes. The common filtering options for specific operations are explained below. Note that most of the commands shown below are CLI versions of the Wireshark features discussed in the **[Wireshark module](https://tryhackme.com/module/wireshark)**.

## Follow Stream

This option helps analysts to follow traffic streams similar to Wireshark. The query structure is explained in the table given below.

| **Main Parameter** | **Protocol**                        | **View Mode**    | **Stream Number**    | **Additional Parameter** |
| ------------------ | ----------------------------------- | ---------------- | -------------------- | ------------------------ |
| -z follow          | - TCP<br>- UDP<br>- HTTP<br>- HTTP2 | - HEX<br>- ASCII | 0 \| 1 \| 2 \| 3 ... | -q                       |

> [!NOTE] Note
> Streams start from '0'. You can filter the packets and follow the streams by using the parameters given below.

- **TCP Streams**: `-z follow,tcp,ascii,0 -q`
- **UDP Streams**: `-z follow,udp,ascii,0 -q`
- **HTTP Streams**: `-z follow,http,ascii,0 -q`

```shell
user@ubuntu$ tshark -r demo.pcapng -z follow,tcp,ascii,1 -q
```
![](https://i.imgur.com/T9dc23Z.png)

## Export Objects

This option helps analysts to extract files from DICOM, HTTP, IMF, SMB and TFTP. The query structure is explained in the table below.

| **Main Parameter** | **Protocol**                                  | **Target Folder**                | **Additional Parameter** |
| ------------------ | --------------------------------------------- | -------------------------------- | ------------------------ |
| --export-objects   | - DICOM<br>- HTTP<br>- IMF<br>- SMB<br>- TFTP | Target folder to save the files. | -q                       |
> You can filter the packets and follow the streams by using the parameters given below:

- `--export-objects http,/home/ubuntu/Desktop/extracted-by-tshark -q`

```
# Extract the files from HTTP traffic. 
user@ubuntu$ tshark -r demo.pcapng --export-objects http,/home/ubuntu/Desktop/extracted-by-tshark -q  

# view the target folder content. 
user@ubuntu$ ls -l 
/home/ubuntu/Desktop/extracted-by-tshark/ total 24 
-rw-r--r-- 1 ubuntu ubuntu  'ads%3fclient=ca-pub-2309191948673629&random=1084443430285&lmt=1082467020&format=468x60_as&o 
-rw-r--r-- 1 ubuntu ubuntu download.html`
```

## Credentials

This option helps analysts to detect and collect cleartext credentials from FTP, HTTP, IMAP, POP and SMTP. You can filter packets and find the cleartext credentials using the parameters below.

- `-z credentials -q`

```
user@ubuntu$ tshark -r credentials.pcap -z credentials -q =================================================================== 
Packet     Protocol         Username         Info             
------     --------         --------         -------- 
72         FTP              admin            Username in packet: 37 
80         FTP              admin            Username in packet: 47 
83         FTP              admin            Username in packet: 54 
118        FTP              admin            Username in packet: 93 
123        FTP              admin            Username in packet: 97 
167        FTP              administrator    Username in packet: 133 
207        FTP              administrator    Username in packet: 170 
220        FTP              administrator    Username in packet: 184 
230        FTP              administrator    Username in packet: 193 .... ===================================================================`
```

# Advanced Filtering Options | Contains, Matches and Extract Fields

Accomplishing in-depth packet analysis sometimes ends up with a special filtering requirement that cannot be covered with default filters. TShark supports Wireshark's **contains** and **matches** operators, which are the key to advanced filtering options. You can visit the **Wireshark: Packet Operations room** (Task 6) if you are unfamiliar with these filters.

A quick recap from the [Wireshark: Packet Operations](https://tryhackme.com/room/wiresharkpacketoperations) room:

| **Filter**   | **Details**                                                                                                                 |
| ------------ | --------------------------------------------------------------------------------------------------------------------------- |
| **Contains** | - Search a value inside packets.<br>- Case sensitive.<br>- Similar to Wireshark's "find" option.                            |
| **Matches**  | - Search a pattern inside packets.<br>- Supports regex.<br>- Case insensitive.<br>- Complex queries have a margin of error. |

> [!NOTE] Note
> The **contains** and **matches** operators cannot be used with fields consisting of **integer** values

> [!tip] Tip
> Using HEX and regex values instead of ASCII always has a better chance of a match.

## Extract Fields

This option helps analysts to extract specific parts of data from the packets. In this way, analysts have the opportunity to collect and correlate various fields from the packets. It also helps analysts manage the query output of the terminal. The query structure is explained in the table given below.

| Main Filter | Target Field        | Show Field Name |
| ----------- | ------------------- | --------------- |
| `-T` fields | `-e` `<field name>` | `-e` header=y   |

> [!NOTE] Note
> You need to use the `-e` parameter for each field you want to display.

You can filter any files by using the field names as shown below:

- `-T fields -e ip.src -e ip.dst -E header=y`

```
user@ubuntu$ tshark -r demo.pcapng -T fields -e ip.src -e ip.dst -E header=y -c 5 

ip.src	        ip.dst 
145.254.160.237	65.208.228.223 
65.208.228.223	145.254.160.237 
145.254.160.237	65.208.228.223 
145.254.160.237	65.208.228.223 
65.208.228.223	145.254.160.237
```

## Filter: `contains`

| Filter      | contains                                                                                                                                     |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| Type        | Comparison operator                                                                                                                          |
| Description | Search a value inside packets. It is case-sensitive and provides similar functionality to the "Find" option by focusing on a specific field. |
| Example     | Find all "Apache" servers.                                                                                                                   |
| Workflow    | List all HTTP packets where the "server" field contains the "Apache" keyword                                                                 |
| Usage       | `http.server contains Apache`                                                                                                                |
```
user@ubuntu$ tshark -r demo.pcapng -Y 'http.server contains "Apache"'                  38   4.846969 65.208.228.223 ? 145.254.160.237 HTTP/XML HTTP/1.1 200 OK   

user@ubuntu$ tshark -r demo.pcapng -Y 'http.server contains "Apache"' -T fields -e ip.src -e ip.dst -e http.server -E header=y 
ip.src	ip.dst	http.server 
65.208.228.223	145.254.160.237	Apache`
```
## Filter: `matches`

| Filter      | matches                                                                                                     |
| ----------- | ----------------------------------------------------------------------------------------------------------- |
| Type        | Comparison operator                                                                                         |
| Description | Search a pattern of a regular expression. It is case-sensitive, and complex queries have a margin of error. |
| Example     | Find all `.php` and `.html` packages                                                                        |
| Workflow    | List all HTTP packets where the "request method" field matches the keywords "GET" or "POST"                 |
| Usage       | `http.request.method matches (GET\|POST)`                                                                   |
```
user@ubuntu$ tshark -r demo.pcapng -Y 'http.request.method matches "(GET|POST)"'        4   0.911310 145.254.160.237 ? 65.208.228.223 HTTP GET /download.html HTTP/1.1     18   2.984291 145.254.160.237 ? 216.239.59.99 HTTP GET /pagead/ads?client=ca-pub-2309191948673629&random=1084443430285&  

user@ubuntu$ tshark -r demo.pcapng -Y 'http.request.method matches "(GET|POST)"' -T fields -e ip.src -e ip.dst -e http.request.method 
-E header=y 
ip.src	ip.dst	http.request.method 
145.254.160.237	65.208.228.223	GET 
145.254.160.237	216.239.59.99	GET
```

# Use Cases | Information

When investigating a case, a security analyst should know how to extract hostnames, DNS queries, and user agents to hunt low-hanging fruits after viewing the statistics and creating an investigation plan. The most common four use cases for every security analyst are demonstrated below. 

If you want to learn more about the mentioned protocols and benefits of the extracted info, please refer to the [Wireshark Traffic Analysis](https://tryhackme.com/room/wiresharktrafficanalysis) room.

## Extract Hostnames

```
user@ubuntu$ tshark -r hostnames.pcapng -T fields -e dhcp.option.hostname      
92-rkd 9
2-rkd 
T3400  

T3400  
60-alfb-sec2 
60-alfb-sec2  

aminott ...
```

> The above example shows how to extract hostnames from DHCP packets with TShark. However, the output is hard to manage when multiple duplicate values exist. A skilled analyst should know how to use native Linux tools/utilities to manage and organize the command line output, as shown below.

```
user@ubuntu$ tshark -r hostnames.pcapng -T fields -e dhcp.option.hostname | awk NF | sort -r | uniq -c | sort -r      
    26 202-ac      
    18 92-rkd      
    14 93-sts-sec ...`
```

Now the output is organized and ready to process/use. The logic of the query is explained below. 

| Query                                                          | Purpose                                                                            |
| -------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| `tshark -r hostnames.pcapng -T fields -e dhcp.option.hostname` | Main query. Extract the DHCP hostname value.                                       |
| `awk NF`                                                       | Remove empty lines.                                                                |
| `sort -r`                                                      | Sort recursively before handling the values.                                       |
| `uniq -c`                                                      | Show unique values, but calculate and show the number of occurrences.              |
| `sort -r`                                                      | The final sort process. <br>Show the output/results from high occurrences to less. |
## Extract DNS Queries

```
user@ubuntu$ tshark -r dns-queries.pcap -T fields -e dns.qry.name | awk NF | sort -r | uniq -c | sort -r      
    96 connectivity-check.ubuntu.com.rhodes.edu      
    94 connectivity-check.ubuntu.com       
    8 3.57.20.10.in-addr.arpa       
    4 e.9.d.b.c.9.d.7.1.b.0.f.a.2.0.2.0.0.0.0.0.0.0.0.0.0.0.0.0.8.e.f.ip6.arpa          4 0.f.2.5.6.b.e.f.f.f.b.7.2.4.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.8.e.f.ip6.arpa          2 _ipps._tcp.local,_ipp._tcp.local       
    2 84.170.224.35.in-addr.arpa       
    2 22.2.10.10.in-addr.arpa`
```

## Extract User Agents

```
user@ubuntu$ tshark -r user-agents.pcap -T fields -e http.user_agent | awk NF | sort -r | uniq -c | sort -r       
    6 Mozilla/5.0 (Windows; U; Windows NT 6.4; en-US) AppleWebKit/534.10 (KHTML, like Gecko) Chrome/8.0.552.237 Safari/534.10       
    5 Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:100.0) Gecko/20100101 Firefox/100.0  
    5 Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.32 Safari/537.36       
    4 sqlmap/1.4#stable (http://sqlmap.org)       
    3 Wfuzz/2.7       
    3 Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)`
```

```
tshark -r hostnames.pcapng -T fields -e dhcp.option.hostname | awk NF | sort -r | uniq -c | sort -r | nl
```

`awk` is a scripting language used for manipulating data and generating records. The awk command programming language requires *no compiling* and allows the user to use variables, numeric functions, string functions, and logical operators.

- `awk NF`: finds the number of fields in the current record.
- `sort -r`: arranges the record in a specific order according to the option used. 
	- `-b`: ignore blanks at the start of a line
	- `-r`: reverse the sorting order
	- `-o`: specify the output file
	- `-n`: use the numerical value to sort
	- `-M`: sort as per the calender month specified
	- `-u`: suppress lines that repeat an earlier key
	- `- sort -k POS1, POS2`: Specify a key to do the sorting. POS1 and POS2 are optional parameters and are used to indicate the starting field and the ending field indices. Without POS2, only the field specified by POS1 is used. Each POS is specified as “F.C” where F represents the field index, and C represents the character index from the start of the field.
    - `sort -t SEP`: Use the provided separator to identify the fields.
- 