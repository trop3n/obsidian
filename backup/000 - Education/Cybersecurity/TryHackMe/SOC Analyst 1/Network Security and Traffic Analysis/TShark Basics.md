> TShark is an open-source command-line network traffic analyzer. It is created by the Wireshark developers and has most of the features of Wireshark. It is commonly used as a command-line alternative to Wireshark. However, it can also be used like `tcpdump`. Therefore it is preferred for comprehensive packet assessments.
### Learning Objectives

- Filtering the traffic with TShark
- Implementing Wireshark filters in TShark
- Expanding and automating packet filtering with TShark

# Command Line Packet Analysis Hints

TShark is a text-based tool, and it is suitable for data carving, in depth packet analysis, and automation with scripts. This strength and flexibility come out of the nature of the CLI tools, as the producted/processed data can be pipelined to additional tools. The most common tools used in packet analysis are listed below:

| Tool/Utility | Purpose and Benefit                                                                                                                                    |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `capinfos`   | A program that provides details of a specified capture file. It is suggested to view the summary of the capture file before starting an investigation. |
| `grep`       | Helps search plain-text data                                                                                                                           |
| `cut`        | Helps cut parts of lines from a specified data source.                                                                                                 |
| `uniq`       | Filters repeated lines/values.                                                                                                                         |
| `nl`         | Views the number of shown lines.                                                                                                                       |
| `sed`        | A stream editor.                                                                                                                                       |
| `awk`        | Scripting language that helps pattern search and processing.                                                                                           |

> [!NOTE] Note
> Sample usage of these tools is covered in the Zeek room.

Open the terminal and follow the given instructions. You can follow along with the interactive materials by switching to the following directory

`cd Desktop/exercise-files`

```
user@ubuntu$ capinfos demo.pcapng  
File name:           demo.pcapng 
File type:           Wireshark/tcpdump/... - pcap 
File encapsulation:  Ethernet 
File timestamp precision:  microseconds (6) 
Packet size limit:   file hdr: 65535 bytes 
Number of packets:   4... 
File size:           25 kB Data size:           25 kB 
Capture duration:    30.393704 seconds 
First packet time:   2004-05-13 10:17:07.311224 
Last packet time:    2004-05-13 10:17:37.704928 Data byte rate:      825 bytes/s Data bit rate:       6604 bits/s 
Average packet size: 583.51 bytes 
Average packet rate: 1 packets/s 
SHA256:              25a72bdf10339... RIPEMD160:           6ef5f0c165a1d... 
SHA1:                3aac91181c3b7... 
Strict time order:   
True Number of interfaces in file: 1 
Interface #0 info:                      
		Encapsulation = Ethernet (1 - ether)                      
		Capture length = 65535                      
		Time precision = microseconds (6)                      
		Time ticks per second = 1000000                      
		Number of stat entries = 0                      
		Number of packets = 4... ..`
```

# TShark Fundamentals | Main Parameters I

TShark is a text-based command line tool. Therefore, conducting an in-depth and consecutive analysis of the obtained results is easy. Multiple built-in options are ready to use to help analysts conduct such investigations. However, learning the parameters is essential; you will need the built-in options and associated parameters to keep control of the output and not be flooded with the detailed output of TShark. The most common parameters are explained in the given table below. Note that TShark requires superuser privileges to sniff the live traffic and list all available features.

| Parameter      | Purpose                                                                      |
| -------------- | ---------------------------------------------------------------------------- |
| `-h`           | Display the help page with the most common features `tshark -h`              |
| `-v`           | Show version info `tshark -v`                                                |
| `-D`           | List available sniffing interfaces `tshark -D`                               |
| `-i`           | Choose an interface to capture live traffic `tshark -i 1`, `tshark -i ens55` |
| `No Parameter` | Sniff the traffic like tcpdump `tshark`                                      |
## Sniffing

Sniffing is one of the *essential functionalities of TShark*. A computer node can have multiple network interfaces that allow the host to communicate and sniff the traffic through the network. Specific interfaces might be associated with particular tasks/jobs. Therefore, the ability to choose a sniffing interface helps users decide and set the proper interface for sniffing.

```shell
user@ubuntu$ sudo tshark -D 
1. ens5 
2. lo (Loopback) 
3. any 4
4. . bluetooth-monitor 
5. nflog ..
```

Sniffing can be done with and without selecting a specific interface. When a particular interface is selected, TShark uses that interface to sniff the traffic. TShark will use the first available interface when no interface is selected, usually listed as 1 in the terminal. Having no interface argument is an alias for `-i 1`. You can also set different sniffing interfaces by using the parameter `-i`. TShark always echoes the used interface name at the beginning of the sniffing.

```shell
# Sniffing with the default interface.
user@ubuntu$ tshark                           
Capturing on 'ens5'
    1   0.000000 aaa.aaa.aaa.aaa ? bbb.bbb.bbb.bbb TCP 3372 ? 80 [SYN] Seq=0 Win=8760 Len=0 MSS=1460 SACK_PERM=1 
    2   0.911310 aaa.aaa.aaa.aaa ? bbb.bbb.bbb.bbb TCP 80 ? 3372 [SYN, ACK] Seq=0 Ack=1 Win=5840 Len=0 MSS=1380 SACK_PERM=1 
    3   0.911310 aaa.aaa.aaa.aaa ? bbb.bbb.bbb.bbb TCP 3372 ? 80 [ACK] Seq=1 Ack=1 Win=9660 Len=0 
...
100 packets captured

# Choosing an interface
user@ubuntu$ tshark -i 2
Capturing on 'Loopback: lo'
...
```

# TShark Fundamentals | Main Parameters II

Let's continue discovering main parameters of TShark.

| Parameter | Purpose                                                                                                                                                        |
| --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-r`      | Read/input information. Read a capture file. `tshark -r demo.pcapng`                                                                                           |
| `-c`      | Packet count. Stop after capturing a specified number of packets.<br>E.g. stop capturing/filtering/reading 10 packets<br>`tshark -c 10`                        |
| `-w`      | Write/output function. Write the sniffed traffic to a file.<br>`tshark -w sample-capture.pcap`                                                                 |
| `-V`      | Verbose. <br>Provide detailed information **for each packet**. This option will provide similar details to Wireshark's **Packet Details Pane**.<br>`tshark -V` |
| `-q`      | Silent mode. <br>Suppress the packet outputs on the terminal.<br>`tshark -q`                                                                                   |
| `-x`      | Display packet bytes.<br>Show packet details in hex and ASCII dump for each packet.<br>`tshark -x`                                                             |
## Read Capture Files

TShark can also process PCAP files. You can use the `-r` parameter to process the file and investigate the packets. You can limit the number of shown packets using the `-c` parameter.

```shell
user@ubuntu$ tshark -r demo.pcapng     
1   0.000000 145.254.160.237 ? 65.208.228.223 TCP 3372 ? 80 [SYN] Seq=0 Win=8760 Len=0 MSS=1460 SACK_PERM=1      
2   0.911310 65.208.228.223 ? 145.254.160.237 TCP 80 ? 3372 [SYN, ACK] Seq=0 Ack=1 Win=5840 Len=0 MSS=1380 SACK_PERM=1      
3   0.911310 145.254.160.237 ? 65.208.228.223 TCP 3372 ? 80 [ACK] Seq=1 Ack=1 Win=9660 Len=0   
..
# Read by count, show only the first 2 packets. 
user@ubuntu$ tshark -r demo.pcapng -c 2 
1   0.000000 145.254.160.237 ? 65.208.228.223 TCP 3372 ? 80 [SYN] Seq=0 Win=8760 Len=0 MSS=1460 SACK_PERM=1      
2   0.911310 65.208.228.223 ? 145.254.160.237 TCP 80 ? 3372 [SYN, ACK] Seq=0 Ack=1 Win=5840 Len=0 MSS=1380 SACK_PERM=1`
```

## Write Data

TShark can also write the sniffed or filtered packets to a file. You can save the sniffed traffic to a file using the `-w` parameter. This option helps analysts to separate specific packets from the file/traffic and save them for further analysis. It also allows analysts to share only suspicious packets/scope with higher-level investigators.

```
# Read the first packet of the demo.pcapng, create write-demo.pcap and save the first packet there. 
user@ubuntu$ tshark -r demo.pcapng -c 1 -w write-demo.pcap  

# List the contents of the current folder. 
user@ubuntu$ ls demo.pcapng  write-demo.pcap  

# Read the write-demo.pcap and show the packet bytes/details. 
user@ubuntu$ tshark -r write-demo.pcap      
1   0.000000 145.254.160.237 ? 65.208.228.223 TCP 3372 ? 80 [SYN] Seq=0 Win=8760 Len=0 MSS=1460 SACK_PERM=1`
```

## Show Packet Bytes

TShark can show packet details in hex and ASCII format. You can view the dump of the packets by using the `-x` parameter. Once you use this parameter, all packets will be shown in hex and ASCII format. Therefore, it might be hard to spot anomalies at a glance, so using this option after reducing the number of packets will be much more efficient.

```
# Read the packets from write-demo.pcap

user@ubuntu$ tshark -r write-demo.pcap 
    1   0.000000 145.254.160.237 ? 65.208.228.223 TCP 3372 ? 80 [SYN] Seq=0 Win=8760 Len=0 MSS=1460 SACK_PERM=1 
```

```shell-session
# Read the packets from write-demo.pcap and show the packet bytes/details.

user@ubuntu$ tshark -r write-demo.pcap -x
0000  fe ff 20 00 01 00 00 00 01 00 00 00 08 00 45 00   .. ...........E.
0010  00 30 0f 41 40 00 80 06 91 eb 91 fe a0 ed 41 d0   .0.A@.........A.
0020  e4 df 0d 2c 00 50 38 af fe 13 00 00 00 00 70 02   ...,.P8.......p.
0030  22 38 c3 0c 00 00 02 04 05 b4 01 01 04 02         "8............

```

## Verbosity

Default TShark packet processing and sniffing operations provide a single line of information and exclude verbosity. The default approach makes it easy to follow the number of processed/sniffed packets; however, TShark can also provide verbosity for each packet when instructed. Verbosity is provided similarly to Wireshark's **Packet Details Pane**. As verbosity offers a long list of packet details, it is suggested to use that option *for specific packets instead of a series of packets*.

```
shell-session
# Default view
user@ubuntu$ tshark -r demo.pcapng -c 1
    1   0.000000 145.254.160.237 ? 65.208.228.223 TCP 3372 ? 80 [SYN] Seq=0 Win=8760 Len=0 MSS=1460 SACK_PERM=1 
```

```
shell-session
# Verbosity
user@ubuntu$ tshark -r demo.pcapng -c 1 -V
Frame 1: 62 bytes on wire (496 bits), 62 bytes captured (496 bits)
...
Ethernet II, Src: 00:00:01:00:00:00, Dst: fe:ff:20:00:01:00
...
Internet Protocol Version 4, Src: 145.254.160.237, Dst: 65.208.228.223
    0100 .... = Version: 4
    .... 0101 = Header Length: 20 bytes (5)
    Total Length: 48
    Identification: 0x0f41 (3905)
    Flags: 0x4000, Don't fragment
    Fragment offset: 0
    Time to live: 128
    Protocol: TCP (6)
    Source: 145.254.160.237
    Destination: 65.208.228.223
Transmission Control Protocol, Src Port: 3372, Dst Port: 80, Seq: 0, Len: 0
 ...

```

> Verbosity provides a full packet details and makes it difficult to investigate (long and complex terminal output for each packet.) However, it is still helpful for in-depth packet analysis and scripting, making TShark stand out. Remember, the best utilization time of verbosity if *after filtering the packets.* You can compare the above output with the below screenshot and see the scripting, carving, and correlation opportunities we have.

![](https://i.imgur.com/f5c2g6i.png)

# TShark Fundamentals | Capture Conditions

As a network sniffer and packet analyzer, TShark can be configured to count packets and stop at a specific point or run in a loop structure. The most common parameters are explained below.

| **Parameter** | **Purpose**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|               | Define capture conditions for a single run/loop. STOP after completing the condition. Also known as "Autostop".                                                                                                                                                                                                                                                                                                                                                                                                      |
| -a            | - **Duration:** Sniff the traffic and stop after X seconds. Create a new file and write output to it.  <br>    <br><br>- `tshark -w test.pcap -a duration:1`<br><br>- **Filesize:** Define the maximum capture file size. Stop after reaching X file size (KB).<br><br>- `tshark -w test.pcap -a filesize:10`<br><br>- **Files:** Define the maximum number of output files. Stop after X files.<br><br>- `tshark -w test.pcap -a filesize:10 -a files:3`                                                            |
|               | Ring buffer control options. Define capture conditions for multiple runs/loops. (INFINITE LOOP).                                                                                                                                                                                                                                                                                                                                                                                                                     |
| -b            | - **Duration:** Sniff the traffic for X seconds, create a new file and write output to it.   <br>    <br><br>- `tshark -w test.pcap -b duration:1`<br><br>- **Filesize:** Define the maximum capture file size. Create a new file and write output to it after reaching filesize X (KB).<br><br>- `tshark -w test.pcap -b filesize:10`<br><br>- **Files:** Define the maximum number of output files. Rewrite the first/oldest file after creating X files.<br><br>- `tshark -w test.pcap -b filesize:10 -b files:3` |
> Capture condition parameters only work in the **capturing/sniffing** mode. You will receive an error message if you try to read a pcap file and apply the capture condition parameters. The idea is to save the capture files in specific sizes for different purposes during live capturing. If you need to extract sorts of packets from a specific capture file, you will need to use the read & write options discussed in the previous task.

> [!Hint] Hint
> TShark supports combining *autostop* `-a` parameters with ring buffer control parameters `-b`. You can combine parameters according to your needs. Use the infinite loop options carefully, remember, you must use at least one autostop parameter to stop the infinite loop. 

```shell-session
# Start sniffing the traffic and stop after 2 seconds, and save the dump into 5 files, each 5kb.

user@ubuntu$ tshark -w autostop-demo.pcap -a duration:2 -a filesize:5 -a files:5
Capturing on 'ens5'
13 
```

```shell-session
# List the contents of the current folder.
user@ubuntu$ ls
-rw------- 1 ubuntu ubuntu   autostop-demo_..1_2022.pcap
-rw------- 1 ubuntu ubuntu   autostop-demo_..2_2022.pcap
-rw------- 1 ubuntu ubuntu   autostop-demo_..3_2022.pcap
-rw------- 1 ubuntu ubuntu   autostop-demo_..4_2022.pcap
-rw------- 1 ubuntu ubuntu   autostop-demo_..5_2022.pcap
```

# Packet Filtering Options: Capture vs. Display Filters

There are two dimensions of packet filtering in TShark; live (capture) and post-capture (display) filtering. 

These two dimensions can be filtered with two different approaches; using a predefined syntax or **Berkeley Packet Filters** (BPF). TShark supports both, so you can use Wireshark filters and BPF to filter traffic. As mentioned earlier, TShark is a command-line version of Wireshark, so we will need to use different filters for capturing and filtering packets. A quick recap from the [Wireshark: Packet Operations](https://tryhackme.com/r/room/wiresharkpacketoperations) room:

|                     |                                                                                                                                                                       |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Capture Filters** | Live filtering options. The purpose is to **save** only a specific part of the traffic. It is set before capturing traffic and is not changeable during live capture. |
| **Display Filters** | Post-capture filtering options. The purpose is to investigate packets by **reducing the number of visible packets**, which is changeable during the investigation.    |
Capture Filters are used to have a *specific type of traffic in the capture file* rather than having everything. Capture filters have limited filtering features, and the purpose is to implement a scope by range, protocol, and direction filtering. This might sound like bulk/raw filtering, but it still provides organized capture files with reasonable file sizes. The display filters investigate the capture files in-depth without modifying the packet. 

|   |   |
|---|---|
|**Parameter**|**Purpose**|
|-f|Capture filters. Same as BPF syntax and Wireshark's capture filters.|
|-Y|Display filters. Same as **Wireshark's display filters.**|
# Packet Filtering Options: Capture Filters

Wireshark's capture filter syntax is used here. The basic syntax for the Capture/BPF filter is shown below. You can read more on capture filter syntax [here](https://www.wireshark.org/docs/man-pages/pcap-filter.html) and [here](https://gitlab.com/wireshark/wireshark/-/wikis/CaptureFilters#useful-filters). Boolean operators can also be used in both types of filters.

|   |   |
|---|---|
|**Qualifier**|**Details and Available Options**|
|**Type**|Target match type. You can filter IP addresses, hostnames, IP ranges, and port numbers. Note that if you don't set a qualifier, the "host" qualifier will be used by default.<br><br>- host \| net \| port \| portrange<br>- Filtering a host<br><br>- `tshark -f "host 10.10.10.10"`<br><br>- Filtering a network range <br><br>- `tshark -f "net 10.10.10.0/24"`<br><br>- Filtering a Port<br><br>- `tshark -f "port 80"`<br><br>- Filtering a port range<br><br>- `tshark -f "portrange 80-100"`|
|**Direction**|Target direction/flow. Note that if you don't use the direction operator, it will be equal to "either" and cover both directions.<br><br>- src \| dst<br>- Filtering source address<br><br>- `tshark -f "src host 10.10.10.10"`<br><br>- Filtering destination address<br><br>- `tshark -f "dst host 10.10.10.10"`|
|**Protocol**|Target protocol.<br><br>- arp \| ether \| icmp \| ip \| ip6 \| tcp \| udp<br>- Filtering TCP<br><br>- `tshark -f "tcp"`<br><br>- Filtering MAC address<br><br>- `tshark -f "ether host F8:DB:C5:A2:5D:81"`<br><br>- You can also filter protocols with IP Protocol numbers assigned by IANA.<br>- Filtering IP Protocols 1 (ICMP)<br><br>- `tshark -f "ip proto 1"`<br>- [**Assigned Internet Protocol Numbers**](https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml)|W
We need to create traffic noise to test and simulate capture filters. We will use the **terminator** terminal instance to have a split=screen view in a single terminal. The **terminator** will help you craft and sniff packets using a single terminal interface. 

Now, run the `terminator` command and follow the instructions using the new terminal instance.
#### Terminal 1
```
user@ubuntu$ tshark -f "host 10.10.10.10" 
Capturing on 'ens5'     
0.000000000 YOUR-IP → 10.10.10.10  TCP 74 36150 → 80 [SYN] Seq=0 Win=62727 Len=0 MSS=8961 SACK_PERM=1 TSval=2045205701 TSecr=0 WS=128     
2 0.003452830  10.10.10.10 → YOUR-IP TCP 74 80 → 36150 [SYN, ACK] Seq=0 Ack=1 Win=62643 Len=0 MSS=8961 SACK_PERM=1 TSval=744450747 TSecr=2045205701 WS=64     
3 0.003487830 YOUR-IP → 10.10.10.10  TCP 66 36150 → 80 [ACK] Seq=1 Ack=1 Win=62848 Len=0 TSval=2045205704 TSecr=744450747     
4 0.003610800 YOUR-IP → 10.10.10.10  HTTP 141 GET / HTTP/1.1`
```

#### Terminal 2
```shell-session
user@ubuntu$ curl -v 10.10.10.10
*   Trying 10.10.10.10:80...
* TCP_NODELAY set
* Connected to 10.10.10.10 (10.10.10.10) port 80 (#0)
> GET / HTTP/1.1
> Host: 10.10.10.10
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Accept-Ranges: bytes
< Content-Length: 1220
< Content-Type: text/html; charset=utf-8

```

> Being comfortable with the command line and TShark filters requires time and practice. You can use the below table to practice TShark capture filters.

|                             |                                                                                                                                                                                                                                                                                                                                                                                      |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Capture Filter Category** | **Details**                                                                                                                                                                                                                                                                                                                                                                          |
| **Host Filtering**          | Capturing traffic to or from a specific host.<br><br>- Traffic generation with cURL. This command sends a default HTTP query to a specified address.<br><br>- `curl tryhackme.com`<br><br>- TShark capture filter for a host<br><br>- `tshark -f "host tryhackme.com"`                                                                                                               |
| **IP Filtering**            | Capturing traffic to or from a specific port. We will use the Netcat tool to create noise on specific ports.<br><br>- Traffic generation with Netcat. Here Netcat is instructed to provide details (verbosity), and timeout is set to 5 seconds.<br><br>- `nc 10.10.10.10 4444 -vw 5`<br><br>- TShark capture filter for specific IP address<br><br>- `tshark -f "host 10.10.10.10"` |
| **Port Filtering**          | Capturing traffic to or from a specific port. We will use the Netcat tool to create noise on specific ports.<br><br>- Traffic generation with Netcat. Here Netcat is instructed to provide details (verbosity), and timeout is set to 5 seconds.<br><br>- `nc 10.10.10.10 4444 -vw 5`<br><br>- TShark capture filter for port 4444<br><br>- `tshark -f "port 4444"`                  |
| **Protocol Filtering**      | Capturing traffic to or from a specific protocol. We will use the Netcat tool to create noise on specific ports.<br><br>- Traffic generation with Netcat. Here Netcat is instructed to use UDP, provide details (verbosity), and timeout is set to 5 seconds.<br><br>- `nc -u 10.10.10.10 4444 -vw 5`<br><br>- TShark capture filter for<br><br>- `tshark -f "udp"`                  |
# Packet Filtering Options: Display Filters

Wireshark's display filter syntax is used here. You can use the official [**Display Filter Reference**](https://www.wireshark.org/docs/dfref/) to find the protocol breakdown for filtering. Additionally, you can use Wireshark's built-in **Display Filter Expression** menu to break down protocols for filters. Noe that Boolean operators can also be used in both types of filters. Common filtering options are shown in the given table below. 

> [!NOTE] Note
> Using single quotes for capture filters is *recommended* to avoid space and bash expansion problems. Once again, you can check the [Wireshark: Packet Operations](https://tryhackme.com/room/wiresharkpacketoperations) room (Task 4 & 5) if you want to review the principles of packet filtering.

|   |   |
|---|---|
|**Display Filter Category**|**Details and Available Options**|
|**Protocol: IP**|- Filtering an IP without specifying a direction.  <br>    <br><br>- `tshark -Y 'ip.addr == 10.10.10.10'`<br><br>- Filtering a network range <br><br>- `tshark -Y 'ip.addr == 10.10.10.0/24'`<br><br>- Filtering a source IP<br><br>- `tshark -Y 'ip.src == 10.10.10.10'`<br><br>- Filtering a destination IP<br><br>- `tshark -Y 'ip.dst == 10.10.10.10'`|
|**Protocol: TCP**|- Filtering TCP port  <br>    <br><br>- `tshark -Y 'tcp.port == 80'`<br><br>- Filtering source TCP port<br><br>- `tshark -Y 'tcp.srcport == 80'`|
|**Protocol: HTTP**|- Filtering HTTP packets  <br>    <br><br>- `tshark -Y 'http'`<br><br>- Filtering HTTP packets with response code "200"<br><br>- `tshark -Y "http.response.code == 200"`|
|**Protocol: DNS**|- Filtering DNS packets  <br>    <br><br>- `tshark -Y 'dns'`<br><br>- Filtering all DNS "A" packets<br><br>- `tshark -Y 'dns.qry.type == 1'`|
We will use the `demo.pcapng` to test display filters. 

```
user@ubuntu$ tshark -r demo.pcapng -Y 'ip.addr == 145.253.2.203' 
13 2.55 145.254.160.237 ? 145.253.2.203 DNS Standard query 0x0023 A .. 
17 2.91 145.253.2.203 ? 145.254.160.237 DNS Standard query response 0x0023 A ..`
```

> The above terminal demonstrates using the **IP Filtering** option. TShark filters the packets and provides the output in our terminal. It is worth noting that TShark doesn't count the "total number of filtered packets"; it assigns numbers to packets according to the capture time, but only displays the packets that match our filter.

Look at the above example. There are two matched packets, but the associated numbers don't start from zero or one; "13" and "17" are assigned to these filtered packets. Keeping track of these numbers and calculating the "total number of filtered packets" can be confusing if your filter retrieves more than a handful of packets. Another example is shown below.

```
user@ubuntu$ tshark -r demo.pcapng -Y 'http'   
4   0.911 145.254.160.237 ? 65.208.228.223 HTTP GET /download.html HTTP/1.1    
18   2.984 145.254.160.237 ? 216.239.59.99 HTTP GET /pagead/ads?client...   
27   3.955 216.239.59.99 ? 145.254.160.237 HTTP HTTP/1.1 200 OK  (text/html)   
38   4.846 65.208.228.223 ? 145.254.160.237 HTTP/XML HTTP/1.1 200 OK`
```

> You can use the `nl` command to get a numbered list of the output. Therefore you can easily calculate the "total number of filtered packets" without being confused with "assigned packet numbers". The usage of the `nl` command is shown below.

```
user@ubuntu$ tshark -r demo.pcapng -Y 'http' | nl 
1    4  0.911 145.254.160.237 ? 65.208.228.223 HTTP GET /download.html HTTP/1.1   
2   18  2.984 145.254.160.237 ? 216.239.59.99 HTTP GET /pagead/ads?client...  
3   27   3.955 216.239.59.99 ? 145.254.160.237 HTTP HTTP/1.1 200 OK (text/html)  
4   38   4.846 65.208.228.223 ? 145.254.160.237 HTTP/XML HTTP/1.1 200 OK`
```

