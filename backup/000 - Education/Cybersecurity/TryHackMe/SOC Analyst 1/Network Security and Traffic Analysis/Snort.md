# Introduction

> SNORT is an ***open-source, rule-based*** Network Intrusion Detection and Prevention System (NIDS/NIPS). It was developed and still maintained by Martin Roesch, open-source contributors, and the Cisco Talos team.

**[The official description](https://www.snort.org/):** _"__Snort is the foremost Open Source Intrusion Prevention System (IPS) in the world. Snort IPS uses a series of rules that help define malicious network activity and uses those rules to find packets that match against them and generate alerts for users.__"_
# Introduction to IDS/IPS

> Before diving into Snort and analyzing traffic, let's have a brief overview of what an Intrusion Detection System (IDS) and Intrusion Prevention System (IPS) is.

- It is possible to configure your network infrastructure and use both of them, but before starting to use any of them, let's learn the differences. 
### Intrusion Detection System

> IDS is a ***passive monitoring solution*** for detecting possible malicious activities/patterns, abnormal incidents, and policy violations.

It is responsible for generating alerts for each suspicious event.

**There are two main types of IDS systems**;

- **Network Intrusion Detection Systems**: NIDS monitor the traffic flow from various areas of the network. The aim is to investigate the traffic on the entire subnet. If a signature is identified, **an alert is created**.
- **Host-based Intrusion Detection System**: HIDS monitors the traffic flow from a single endpoint device. The aim is to investigate the traffic on a particular device. If a signature is identified, **an alert is created.**
### Intrusion Prevention System

> IPS is an ***active protecting solution*** for preventing possible malicious activities/patterns, abnormal incidents, and policy violations. 

It is responsible for *stopping/preventing/terminating* the suspicious event as soon as the detection is performed. 

**There are four main types of IPS systems**;

- **Network Intrusion Prevention System**: NIPS monitor the traffic flow from various areas of the network. The aim is to protect the traffic on the entire subnet. If a signature is identified, **the connection is terminated.**
- **Behavior-based Intrusion Prevention System (Network Behavior Analysis - NBA)** - Behavior-based systems monitor the traffic flow from various areas of the network. The aim is to protect the traffic on the entire subnet. If a signature is detected, *the connection is terminated.*

Network Behavior Analysis Systems work similar to NIPS. The difference between NIPS and Behavior-based is that *behavior based systems require a training period* (also known as *baselining*) to learn the normal traffic and differentiate the malicious traffic and threats. This model provides more efficient rules against new threats.

The system is trained to know the "normal" to detect the "abnormal". The training period is crucual to avoid any false positives. In case of any security breach during the training period, the results will be highly problematic. Another critical point is to ensure that the system is well trained to recognize benign activities.

- **Wireless Intrusion Prevention Systems**: WIPS monitors the traffic flow from a wireless network. The aim is to protect the wireless traffic and stop possible attacks launched from there. If a signature is identified, **the connection is terminated.**
- **Host-based Intrusion Prevention System**: HIPS actively protects the traffic flow from a single endpoint device. The aim is to investigate the traffic on a particular device. If a signature is identified, **the connection is terminated.**

HIPS working mechanism is similar to HIDS. The difference between them is that *while HIDS creates alerts for threats, HIPS stops the threats by terminating the connection.*
### Detection/Prevention Techniques

> There are three main detection and prevention techniques used in IDS and IPS solutions:

| Technique           | Approach                                                                                                                                                                                                                       |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Signature-Based** | This technique relies on rules that identify the specific patterns of the known malicious behavior. This model helps detect known threats.                                                                                     |
| **Behavior-Based**  | This technique identifies new threats with new patterns that pass through signatures. The model compares the known/normal behavior with unknown/abnormal behaviors. *The model helps detect previously unknown or new threats* |
| **Policy-Based**    | This technique compares detected activities with system configuration and security policies. This model helps detect policy violations.                                                                                        |

### Summary  

**Phew!** That was a long ride and lots of information. Let's summarise the overall functions of the IDS and IPS in a nutshell.

- **IDS** can identify threats but require user assistance to stop them.
- **IPS** can identify and block the threats with less user assistance at the detection time.

### Snort Time

**Now, let's talk about Snort.**

**[Here is the rest of the official description](https://www.snort.org/) of Snort**

_"__Snort can be deployed inline to stop these packets, as well. Snort has three primary uses: As a packet sniffer like tcpdump, as a packet logger — which is useful for network traffic debugging, or it can be used as a full-blown network intrusion prevention system. Snort can be downloaded and configured for personal and business use alike."_

> SNORT is an *open-source, rule-based* Network Intrusion Detection and Prevention System (NIDS/NIPS). 
#### Capabilities of Snort

- Live traffic analysis
- Attack and probe detection
- Packet logging
- Real-time alerting
- Modules & plugins
- Pre-processors
- Cross-platform support (Linux and Windows)
#### Three Main Use Models

- **Sniffer Mode** - read IP packets and prompt them in the console application.
- **Packet Logger Mode** - Log all IP packets (inbound and outbound) that visit the network.
- **NIDS** (Network Intrusion Detection System ) and **NIPS** (Network Intrusion Prevention System) - Log/drop the packets that are deemed as malicious according the the user-defined rules.
# First Interaction With Snort

The command `snort -V` will display the instance verision:

**Before getting our hands dirty, we should ensure our configuration file is valid.**

> Here, `-T` is used for testing configuration, and `-c` is identifying the configuration file (`snort.conf`).
> 
> 	Note that it is possible to use an additional configuration file by pointing it with `-c`.

Once we use a configuration file, snort got much more powerful! The configuration file is *an all-in-one management file for Snort.*

- Rules, Plugins, Detection Mechanisms, Default Actions and Output settings are identified here. It is possible to have multiple configuration files for different purposes and cases but can only use one at runtime.

Note that every time you start Snort, it will automatically show the default banner and initial information about your setup. You can prevent this by using the `-q` parameter. 

| Parameter      | Description                                                                                            |
| -------------- | ------------------------------------------------------------------------------------------------------ |
| `-V/--version` | This parameter provides information about your instance version.                                       |
| `-c`           | Identifying the configuration file                                                                     |
| `-T`           | Snort's self-test parameter, you can test your setup with this parameter.                              |
| `-q`           | Quiet mode prevents Snort from displaying the default banner and initial information about your setup. |
# Operation Mode 1: Sniffer Mode

> Like ***tcpdump***, Snort has various flags capable of viewing various data about the packet it is ingesting.

Sniffer mode parameters are explained in the table below:

| Parameter | Description                                                                                                                                                   |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-v`      | Verbose. Display the TCP/IP output in the console.                                                                                                            |
| `-d`      | Display the packet data (payload)                                                                                                                             |
| `-e`      | Display the link-layer (TCP/IP/UDP/ICMP) headers.                                                                                                             |
| `-X`      | Display the full packet details in HEX.                                                                                                                       |
| `-i`      | This parameter helps to define a specific network interface to listen/sniff. Once you have multiple interfaces, you can choose a specific interface to sniff. |
> Let's start using each parameter and see the difference between them. Snort needs active traffic on your interface, so we need to generate traffic to see Snort in action.

To do this, use the **traffic-generator script**.
### Sniffing with the Parameter `-i`

> Start the Snort instance in `verbose mode (-v)` and use the `interface (-i)` "eth0"; `sudo snort -v -i eth0`

In case you only have one interface, Snort uses it by default. The above example demonstrates sniffing on the interface named `eth0`. Once you simulate the parameter -v, you will notice it will automatically use the `"eth0"` interface and prompt it.
### Sniffing with Parameter `-v`

> Start the Snort instance in **verbose mode**: `sudo snort -v`

Now run the traffic-generator script as sudo and start `ICMP/HTTP traffic`. Once the traffic is generated, snort will start showing the packets in verbosity mode.

> As you can see in the given output, verbosity mode provides `tcpdump`-like output information. Once we interrupt the sniffing with ctrl+c, it stops and summarizes the sniffed packets.
### Sniffing with Parameter `-d`

> Start the Snort instance in **dumping packet mode**: `sudo snort -d`

As you can see in the given output, packet data payload mode covers the verbose mode and provides more data.
### Sniffing with Parameter `-de`

> Start the Snort instance in **dump (-d)** and **link-layer header grabbing (-e)** mode; `snort -d -e`
### Sniffing with Parameter `-X`

> Start the Snort instance in **full packet dump mode (-X)**; `sudo snort -X`

Once the traffic is generated, snort will start showing the  packets in verbosity mode

**Note that you can use the parameters in combined and separated form as follows**:

- `snort -v`
- `snort -vd`
- `snort -de`
- `snort -v -d -e`
- `snort -X`
# Operation Mode 2: Packet Logger Mode

### Let's Run Snort in Logger Mode

> You can use Snort as a sniffer and log the sniffed packets via logger mode. You only need to use the packet logger mode parameters, and Snort does the rest to accomplish this.

Packet logger parameters are explained in the table below:

| Parameter  | Description                                                                                                                                                             |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-l`       | Logger mode, target **log and alert** output directory. Default output folder is `/var/log/snort`. The default action is to dump as tcpdump format in `/var/log/snort`. |
| `-K ASCII` | Log packets in ASCII format.                                                                                                                                            |
| `-r`       | Reading option, read the dumped logs in Snort.                                                                                                                          |
| `-n`       | Specify the number of packets that will process/read. Snort will stop after reading the specified number of packets.                                                    |
### Logfile Ownership

> Before generating logs and investigating them, we must remember the Linux file ownership and permissions. 

No need to deep dive into user types and permissions. 

The fundamental file ownership rule: **whoever creates a file becomes the owner of the corresponding file.**

**Snort** needs superuser (root) rights to sniff the traffic, so once you run the snort with the `sudo` command, the "root" account will own the generated log files. Therefore, you will need root rights to investigate the log files. 

There are two different approaches to investigate the generated log files:

- Elevation of privileges - You can elevate your privileges to examine the files. You can use the `sudo` command to execute your command as a superuser with the following command `sudo command`. You can also elevate the session privileges and switch to the superuser account to examine the generated log files with the following command: `sudo su`.
- Changing the ownership of the files/directories - You can also change the ownership of the file/folder to read it as your user: `sudo chown username file` or `sudo chown username -R directory`. The `-R` parameter helps recursively process the files and directories.
### Logging with Parameter `-l`

> First, start the Snort instance in packet logger mode: `sudo snort -dev -l`.

Now start ICMP/HTTP traffic with the traffic-generator script.

> Once the traffic is generated, Snort will start showing the packets and log them in the target directory. You can configure the default output directory in `snort.config` file. 

However, you can use the `-l` parameter to set a target directory. Identifying the default log directory is useful for continuous monitoring operations, and the `-l` parameter is much more useful for testing purposes.

The `-l .` part of the command creates the logs in the current directory. You will need to use this option to have the logs for each exercise in their folder.

Now, let's check the generated log file. **Note that the log file names will be different in your case.**

```bash
user@ubuntu$ ls .

snort.log.1717334955
```
### Logging with the Parameter `-K ASCII`

Start the Snort instance in packet logger mode: `sudo snort -dev -K ASCII`

Now run the traffic-generator script as sudo and start the **ICMP/HTTP traffic**. Once the traffic is generated, Snort will start showing the packets in verbosity mode. 

> The logs created with "`-K ASCII`" parameter is entirely different. There are two folders with IP address names. Let's look into them. 

```
user@ubuntu$ ls ./192.168.175.129/                               
ICMP_ECHO  UDP:36648-53  UDP:40757-53  UDP:47404-53  UDP:50624-123`
```

Once we take a closer look at the created folders, we can see that the logs are in ASCII and categorized format, so it is possible to read them without using a Snort instance. 

> In a nutshell, ASCII mode provides multiple files in human-readable format, so it is possible to read the logs easily by using a text editor. By contrast with ASCII format, binary format is not human-readable and requires analysis using Snort or an application like tcpdump.

Let's compare the ASCII format with the binary format by opening both of them up in a text editor.

The difference between the binary log file and the ASCII file is shown below. 

Right: ASCII, Left: Binary
### Reading Generated Logs with Parameter `-r`

> Start the Snort instance in packet reader mode; `sudo snort -r`

**Note that** Snort can read and handle the binary like output (tcpdump and Wireshark can also handle this log format). However, if you create logs with "-K ASCII" parameter, Snort will not read them. 

As you can see in the output, Snort read and displayed the log file just like in the sniffer mode.

*`-r`* parameter also allows users to filter the binary log files. You can filter the processed log to see specific packets with the "`-r`" parameter and Berkeley Packet Filters (BPF).

- - `sudo snort -r logname.log -X`
- `sudo snort -r logname.log icmp`
- `sudo snort -r logname.log tcp`
- `sudo snort -r logname.log 'udp and port 53'`

The output will be the same as the above, but only packets with the chosen protocol will be shown. Additionally, you can specify the number of processes with the parameter `-n`. *The following command will process only the first 10 packets.*

`snort -dvr logname.log -n 10`

Please use the following resources to understand how the BPF works and its use.

- [https://en.wikipedia.org/wiki/Berkeley_Packet_Filter](https://en.wikipedia.org/wiki/Berkeley_Packet_Filter)
- [https://biot.com/capstats/bpf.html](https://biot.com/capstats/bpf.html)
- [https://www.tcpdump.org/manpages/tcpdump.1.html](https://www.tcpdump.org/manpages/tcpdump.1.html)
# Snort in IDS/IPS Mode

> Capabilities of Snort are not limited to sniffing and logging the traffic. IDS/IPS mode helps you manage the traffic according to user-defined rules.

**Note that** (N)IDS/IPS mode depends on the rules and configuration. `TASK-10` summarizes the essential paths, files and variables. 

Also, task 3 covers configuration testing. Here, we need to understand the operating logic first, and then we will be going into rules in `TASK-9`.
### Run Snort in IDS/IPS Mode

> NIDS mode parameters are explained in the table below:

| Parameter | Description                                                                                                                                                                       |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-c`      | Defining the configuration file.                                                                                                                                                  |
| `-T`      | Testing the configuration file.                                                                                                                                                   |
| `-N`      | Disable logging.                                                                                                                                                                  |
| `-D`      | Background mode.                                                                                                                                                                  |
| `-A`      | Alert modes;                                                                                                                                                                      |
|           | `Full`: Full alert mode, providing all possible information about the alert. This one also is the default mode; once you use -A and don't specify any mode, Snort uses this mode. |
|           | `fast`: Fast mode shows the alert message, timestamp, source and destination IP, along with port numbers.                                                                         |
|           | `console`: Provides fast style alerts on the console screen.                                                                                                                      |
|           | `cmg`: CMG style, basic header details with payload in hex and text format.                                                                                                       |
|           | `none`: Disabling alerting.                                                                                                                                                       |
> Let's start using each parameter and see the difference between them. Snort needs active traffic on your interface, so we need to generate traffic to see Snort in action. 

To do this, use the **traffic-generator** script and sniff the traffic.

*Once you start running IDS/IPS mode, you need to use rules.* As we mentioned earlier, we will use a pre-defined ICMP rule as an example. The defined rule will only generate alerts in any direction of ICMP packet activity. 

`alert icmp any any <> any any (msg: "ICMP Packet Found"; sid: 100001; rev:1;)`

> The rule is located in `/etc/snort/rules/local.rules`.

Remember, in this module, we will focus only on the operating modes. The rules are covered in TASK9&10. **Snort will create an "alert" file if the traffic flow triggers an alert.** **One last note;** once you start running IPS/IDS mode, the sniffing and logging mode will be semi-passive. However, you can activate the functions using the parameters discussed in previous tasks. `**(-i, -v, -d, -e, -X, -l, -K ASCII)**` If you don't remember the purpose of these commands, please revisit TASK4.
### IDS/IPS Mode with Parameter `-c and -T`

Start the Snort instance and test the configuration file. 

`sudo snort -c /etc/snort/snort.conf -T`

This command will check your configuration file and prompt if there is any misconfiguration in your current setting. You should be familiar with this command if you covered TASK3. 
### IDS/IPS Mode with Parameter `-N`

> Start the Snort instance and *disable logging* by running the following command: `sudo snort -c /etc/snort/snort.conf -N`.

Now run the traffic-generator script as sudo and start `ICMP/HTTP traffic`. This command will disable logging mode. The rest of the other functions will still be available (if activated.)

The command-line output will provide the information requested with the parameters. So, if you activate verbosity (`-v`) or full packet dump (`-X`) you will still have the output in the console, but there will be no logs in the log folder.
### IDS/IPS mode with parameter `-D`

> Start the Snort instance in background mode with the following command: `sudo snort -c /etc/snort/snort.conf -D`

Now run the traffic-generator script as sudo and start ICMP/HTTP traffic. Once the traffic is generated, snort will start processing the packets and accomplish the given task with additional parameters.

```shell
user@ubuntu$ sudo snort -c /etc/snort/snort.conf -D

Spawning daemon child...
My daemon child 2898 lives...
Daemon parent exiting (0)
```

> The command-line output will provide the information requested with the parameters. So if you activate **verbosity `-v`** or **full packet dump `-X`** with **packet logger mode `-l`** you will still have logs in the logs folder, but there will be no output in the console. 

Once you start the background mode and want to check the process, you can use the `ps` command:

```bash
user@ubuntu$ ps -ef | grep snort

root        2898    1706  0 05:53 ?        00:00:00 snort -c /etc/snort/snort.conf -D
```

> If you want to kill the daemon, you can easily use the "kill" command to stop the process.

```shell
user@ubuntu$ sudo kill -9 2898
```

**Note that** daemon mode is mainly used to automate the Snort. This parameter is mainly used in scripts to start the Snort service in the background. *It is not recommended to use this mode unless you have a working knowledge of Snort and stable configuration.*
### IDS/IPS Mode with Parameter `-A`

**Remember that there are several alert mode available in Snort**

- `console`: Provides fast style alerts on the console screen.
- `cmg`: Provides basic header details with payload in hex and text format.
- `full`: Full alert mode, providing all possible information about the alert.
- `fast`: Fast mode, shows the alert message, timestamp, source and destination IP along with port numbers.
- `none`: disabling alerting.

In this section, only the `console` and `cmg` parameters provide alert information in the console. It is impossible to identify the difference between the rest of the alert modes via terminal. 

- Differences can be identified by looking at generated logs.

At the end of this section, we will compare the full, fast and none modules. Remember that these parameters don't provide console output, so we will continue to identify the differences through log formats.
#### IDS/IPS Mode with Parameter `-A console`

> Console mode provides fast style alerts on the console screen. 

Start the Snort instance in console alert mode with the following command: `sudo snort -c /etc/snort/snort.conf -A console`.

Now run the traffic-generator script as sudo and start ICMP/HTTP traffic. Once the traffic is generated, snort will start generating alerts according to provided ruleset defined in the configuration file.
#### IDS/IPS Mode with Parameter `-A cmg`

> Cmg mode provides basic header details with payload in hex and text format. Start the Snort instance in **cmg alert mode (-A cmg)** with the following command: `sudo snort -c /etc/snort/snort.conf -A cmg`

Now run the traffic-generator script as sudo and start ICMP/HTTP traffic. 

Once the traffic is generated, snort will start generating alerts according to provided ruleset defined in the configuration file.

> Let's compare the console and cmg outputs before moving on to other alarm types. As you can see in the outputs, `console mode` provides basic header and rule information, `cmg mode` provides full packet information along with rule information. 
#### IDS/IPS Mode with Parameter `-A fast`

> Fast mode provides alert messages, timestamps, and source and destination IP addresses. **Remember, there is no console output in this mode.** Start the Snort instance in fast alert mode (-A fast ) with the following command `sudo snort -c /etc/snort/snort.conf -A fast`

> As you can see in the given picture above, fast style alerts contain summary information on the action like direction and alert header.
#### IDS/IPS Mode with Parameter `-A full`

> Full alert mode provides all possible information about the alert. **Remember, there is no console output in this mode.** Start the Snort instance in full alert mode (-A full ) with the following command `sudo snort -c /etc/snort/snort.conf -A full`

*Full Style Alerts* contain all possible information on the action.
#### IDS/IPS Mode with Parameter `-A none`

> Disable alerting. This mode doesn't create the alert file. However, it still logs the traffic and creates a log file in binary dump format. Remember, there is no console output in this mode. Start the Snort instance in none alert mode (-A none) with the following command `sudo snort -c /etc/snort/snort.conf -A none`

#### IDS/IPS mode: "Using rule file without configuration file"

It is possible to run the Snort only with rules without a configuration file. Running the Snort in this mode will help you test the user-created rules. However, this mode will provide less performance.
#### IPS Mode and Dropping Packets

> Snort IPS mode activated with `-Q --daq afpacket` parameters. You can also activate this mode by editing snort.conf file. However, you don't need to edit snort.conf file in the scope of this room. 

Activate the Data Acquisition (DAQ) modules and use the afpacket module to use snort as an IPS: `-i eth0:eth1`
# Operation Mode 4: PCAP Investigation

### Let's Investigate PCAPs with Snort

> Capabilities of Snort are not limited to sniffing, logging and detecting/preventing the threats. PCAP read/investigate mode helps you work with pcap files. 

Once you have a pcap file and process it with Snort, you will receive default traffic statistics with alerts depending on your ruleset. 

Reading a pcap without using any additional parameters we discussed before will only overview the packets and provide statistics about the file. In most cases, this is not very handy. 

We are investigating the pcap with *Snort to benefit from the rules and speed up our investigation process by using the known patterns of threats.*

**Note that**: we are pretty close to starting to create rules. Therefore, you need to grasp the working mechanism of Snort, learn the discussed parameters and begin combining the parameters for different purposes.

PCAP Mode parameters are listed below:

| Parameter            | Description                                      |
| -------------------- | ------------------------------------------------ |
| `-r/ --pcap-single=` | Read a single pcap                               |
| `--pcap-list=""`     | Read pcaps provided in command (space separated) |
| `--pacp-show`        | Show pcap name on console during processing      |
### Investigating single PCAP with Parameter `-r`.

For test purposes, you can still test the default reading option with pcap by using the following command `snort -r icmp=test.pcap`

Let's investigate the pcap with our configuration file and see what will happen. `sudo snort -c /etc/snort/snort.conf -q -r icmp-test.pcap -A console -n 10`

Our ICMP rule got a hit! As you can see in the given output, snort identified the traffic and prompted the alerts according to our ruleset.
### Investigating Multiple PCAPs with parameter "--pcap-list"

Let's investigate multiple pcaps with our configuration file and see what will happen. `sudo snort -c /etc/snort/snort.conf -q --pcap-list="icmp-test.pcap http2.pcap" -A console -n 10`

Our ICMP rule got a hit! As you can see in the given output, snort identified the traffic and prompted the alerts according to our ruleset.

**Here is one point to notice**: we've processed two pcaps, and there are a lot of alerts, so it is impossible to match the alerts with provided pcaps without Snort's help. We need to separate the pcap process to identify the source of the alerts.
### Investigating Multiple PCAPs with Parameter `--pcap-show`

> Let's investigate multiple pcaps, distinguish each one, and see what will happen. `sudo snort -c /etc/snort/snort.conf -q --pcap-list="icmp-test.pcap http2.pcap" -A console --pcap-show`

# Snort Rule Structure

> Understanding the Snort rule structure and format is essential for any blue and purple team tester. The primary structure of the Snort rule is shown below;

> Each rule should have a type of action, protocol, source and destination IP, source and destination port and an option.

Remember, Snort is in passive mode by default. So, most of the time, you will use Snort as an IDS. 

You will need to start **`inline mode` to turn on IPS mode**. But before we start playing with inline mode, you should be familiar with Snort features and rules.

> The Snort rule structure is easy to understand but difficult to produce. You should be familiar with rule options and related details to create efficient rules. ***It is recommended to practice Snort rules and option details for different use cases.*** 

We will cover the basic rule structure in this room and help you take a step into Snort rules. You can always advance your rule creation skills with different rule options by practicing different use cases and studying rule option details in depth. 

We will focus on two actions: `alert` for IDS mode and `reject` for IPS mode.

> Rules cannot be processed without a header. Rule options are `optional` parts. ***However, it is almost impossible to detect sophisticated attacks without using the rule options.*** 

**Action**: There are several actions for rules. Make sure you understand the functionality and test it before creating rules for live systems. The most common actions are listed below:

- `alert`: Generate an alert and log the packet.
- `log`: Log the packet.
- `drop`: Block and log the packet.
- `reject`: Block the packet, log it and terminate the packet session.

**Protocol**: Protocol parameter identifies the type of the protocol that filtered for the rule.

Not that Snort2 supports only four protocol filters in the rules: *IP, TCP, UDP and ICMP*. 

However, you can detect the application flows using port numbers and options. For instance, if you want to detect FTP traffic, you cannot use the FTP keyword in the protocol field but filter the FTP traffic by investigating TCP traffic on port 21.
### IP and Port Numbers

> These parameters identify the source and destination IP addresses and associated port numbers filtered for the rule.

|   |   |
|---|---|
|IP Filtering|alert icmp 192.168.1.56 any <> any any  (msg: "ICMP Packet From "; sid: 100001; rev:1;)<br><br>This rule will create an alert for each ICMP packet originating from the 192.168.1.56 IP address.|
|Filter an IP range|alert icmp 192.168.1.0/24 any <> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;)<br><br>This rule will create an alert for each ICMP packet originating from the 192.168.1.0/24 subnet.|
|Filter multiple IP ranges|alert icmp [192.168.1.0/24, 10.1.1.0/24] any <> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;)<br><br>This rule will create an alert for each ICMP packet originating from the 192.168.1.0/24 and 10.1.1.0/24 subnets.|
|Exclude IP addresses/ranges|"negation operator" is used for excluding specific addresses and ports. Negation operator is indicated with "!"<br><br>alert icmp !192.168.1.0/24 any <> any any  (msg: "ICMP Packet Found"; sid: 100001; rev:1;)<br><br>This rule will create an alert for each ICMP packet not originating from the 192.168.1.0/24 subnet.|
|Port Filtering|alert tcp any any <> any 21  (msg: "FTP Port 21 Command Activity Detected"; sid: 100001; rev:1;)<br><br>This rule will create an alert for each TCP packet sent to port 21.|
|Exclude a specific port|alert tcp any any <> any !21  (msg: "Traffic Activity Without FTP Port 21 Command Channel"; sid: 100001; rev:1;)  <br><br>This rule will create an alert for each TCP packet not sent to port 21.|
|Filter a port range (Type 1)|alert tcp any any <> any 1:1024   (msg: "TCP 1-1024 System Port Activity"; sid: 100001; rev:1;)<br><br>This rule will create an alert for each TCP packet sent to ports between 1-1024.|
|Filter a port range (Type 2)|alert tcp any any <> any :1024   (msg: "TCP 0-1024 System Port Activity"; sid: 100001; rev:1;)  <br><br>This rule will create an alert for each TCP packet sent to ports less than or equal to 1024.|
|Filter a port range (Type 3)|alert tcp any any <> any 1025: (msg: "TCP Non-System Port Activity"; sid: 100001; rev:1;)<br><br>This rule will create an alert for each TCP packet sent to source port higher than or equal to 1025.|
|Filter a port range (Type 4)|alert tcp any any <> any [21,23] (msg: "FTP and Telnet Port 21-23 Activity Detected"; sid: 100001; rev:1;)<br><br>This rule will create an alert for each TCP packet sent to port 21 and 23.|
#### Direction

> The direction operator indicates the traffic flow to be filtered by Snort. The left side of the rule shows the source, and the right side shows the destination.

- `->` Source to the destination
- `<>` Bi-directional flow

*There s no `<-`* *operator in Snort.* 

### There are Three Main Rule Operators in Snort

- **General Rule Options** - Fundamental rule options for Snort.
- **Payload Rule Options** - Rule options that help to investigate the payload data. These options are helpful to detect specific payload patterns.
- **Non-payload Rule Options** - Rule options that focus on non-payload data. These options will help create specific patterns and identify network issues.
### General Rule Options

|             |                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Msg         | The message field is a basic prompt and quick identifier of the rule. Once the rule is triggered, the message filed with appear in the console or log. Usually, the message part is a one-liner that summarizes the event.                                                                                                                                                                                                                   |
| Sid         | Snort rule IDs (SID) come with a pre-defined scope, and each rule must have a SID in a proper format. There are three different scopes for SIDs shown below.                                                                                                                                                                                                                                                                                 |
| Reference   | Each rule can have additional information or reference to explain the purpose of the rule or threat pattern. That could be a Common Vulnerabilities and Exposures (CVE) id or external information. *Having references for the rules will always help analysts during the alert and incident investigation.*                                                                                                                                 |
| Rev         | Snort rules can be modified and updated for performance and efficiency issues. Rev option help analysts to have the revision information of each rule. Therefore, it will be easy to understand rule improvements. Each rule has its unique rev number, and there is no auto-backup feature on the rule history. Analysts should keep the rule history themselves. Rev option is only an indicator of how many times the rule had revisions. |
| Rev Example | alert icmp any any <> any any (msg: "ICMP Packet Found"; sid: 100001; reference:cve,CVE-XXXX; rev:1;)                                                                                                                                                                                                                                                                                                                                        |
### Payload Detection Rule Options

|              |                                                                                                                                                                                                                                                                                                                                      |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Content      | Payload Data. It maches specific payload data by ASCII, hex, or both. It is possible to use this option multiple times in a single rule. However, the more you create specific pattern match features, the more it takes time to investigate a packet.                                                                               |
| Nocase       | Disabling case sensitivity. Used for enhancing the content searches. `alert tcp any any <> any 80 (msg: "GET Request Found";content:"GET";nocase;sid:1000001;rev:1;`                                                                                                                                                                 |
| Fast_pattern | Prioritize content search to speed up the payload search operation. By default, Snort uses the biggest content and evaluates it against the rules. "fast_pattern" option helps you select the initial packet match with the specific value for further investigation. This option is required when using multiple "content" options. |
|              | The following rule has two content options, and the fast_pattern option tells Snort to use the first content option (in this case, GET) for the initial packet match.                                                                                                                                                                |
|              | `alert tcp any any <> any 80  (msg: "GET Request Found"; content:"GET"; fast_pattern; content:"www";  sid:100001; rev:1;)`                                                                                                                                                                                                           |
### Non-Payload Detection Rule Options

> There are rule options that focus on non-payload data. These options will help create 

|        |                                                                                                                                                                                                    |
| ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ID     | Filtering the IP id field.<br><br>alert tcp any any <> any any (msg: "ID TEST"; id:123456; sid: 100001; rev:1;)                                                                                    |
| Flags  | Filtering the TCP flags.<br><br>- F - FIN<br>- S - SYN<br>- R - RST<br>- P - PSH<br>- A - ACK<br>- U - URG<br><br>`alert tcp any any <> any any (msg: "FLAG TEST"; flags:S;  sid: 100001; rev:1;)` |
| Dsize  | Filtering the packet payload size.<br><br>- dsize:min<>max;<br>- dsize:>100<br>- dsize:<100<br><br>`alert ip any any <> any any (msg: "SEQ TEST"; dsize:100<>300;  sid: 100001; rev:1;)`           |
| Sameip | Filtering the source and destination IP addresses for duplication.<br><br>`alert ip any any <> any any (msg: "SAME-IP TEST";  sameip; sid: 100001; rev:1;)`                                        |
> Remember, once you create a rule, it is a local rule and should be in your `local.rules` file. This file is located under `/etc/snort/rules/local.rules`.
> 
> 	A quick reminder on how to edit your local rules is shown below.

```shell
user@ubuntu$ sudo gedit /etc/snort/rules/local.rules 
```

> That is the `local.rules` file.

> Note that there are some default rules activated with Snort instance. These rules are deactivated to manage your rules and improve your exercise experience. For further information, please refer to the TASK-10 or [Snort manual](http://manual-snort-org.s3-website-us-east-1.amazonaws.com/).

By this point, we covered the primary structure of the Snort rules. Understanding and practicing the fundamentals is suggested before created advanced rules using additional options. 
# Snort2 Operation Logic: Points to Remember

### Points to Remember

###### Main Components of Snort

- **Packet Decoder**: Packet collector component of Snort. It collects and prepares the packets for pre-processing.
- **Pre-Processors**: A component that arranges and modifies the packets for the detection engine.
- **Detection Engine**: The primary component that processes, dissect and analyze the packets by applying the rules. 
- **Logging and Alerting**: Log and alert generation component.
- **Outputs and Plugins**: Output integration modules (i.e. alerts to syslog/mysql) and additional plugin (rule management detection plugins) support is done with this component.
### There are Three Types of Rules Available for Snort

- **Community Rules** - Free ruleset under the GPLv2. Publicly accessible, no need for registration.
- **Registered Rules** - Free ruleset (requires registration). This ruleset contains subscriber rules with 30 days delay.
- **Subscriber Rules (paid)** - Paid ruleset (requires subscription). This is the main ruleset and is updated twice a week (Tuesday and Thursdays)

You can download and read more about rules [here](https://www.snort.org/downloads).

**Note:** Once you install Snort2, it automatically creates the required directories and files. However, if you want to use the community or the paid rules, you need to indicate each rule in the **snort.conf** file.

Since it is a long, all-in-one configuration file, editing it without causing misconfiguration is troublesome for some users. **That is why Snort has several rule updating modules and integration tools. To sum up, never replace your configured Snort configuration files; you must edit your configuration files manually or update your rules with additional tools and modules to not face any fail/crash or lack of feature.**

- *snort.conf*: Main configuration file.
- *local.rules*: User-generated rules file.

> **Let's start with overviewing the main configuration file (snort.conf)** `sudo gedit /etc/snort/snort.conf`

###### Navigate to the Step #1: Set the Network Variables Section

This section manages the scope of the detection and rule paths. 

| TAG NAME            | INFO                                                                                | EXAMPLE                   |
| ------------------- | ----------------------------------------------------------------------------------- | ------------------------- |
| `HOME_NET`          | That is where/what we are protecting.                                               | 'any' OR '192.168.1.1/24' |
| `EXTERNAL_NET`      | This field is the external network, so we need to keep it as 'any' or '!$HOME_NET'. | 'any' OR '!$HOME_NET'     |
| `RULE_PATH`         | Hardcoded rule path.                                                                | /etc/snort/rules          |
| `SO_RULE_PATH`      | *These rules come with registered and subscriber rules*                             | $RULE_PATH/so_rules       |
| `PREPROC_RULE_PATH` | *These rules come with registered and subscriber rules*                             | $RULE_PATH/plugin_rules   |
###### Navigate to the Step #2 Configure the Decoder Section

> In this section, you manage the IPS mode of Snort. The single-node installation model IPS works best with `afpacket` mode. You can enable this mode and run Snort in IPS.

| TAG NAME            | INFO                       | EXAMPLE         |
| ------------------- | -------------------------- | --------------- |
| `#config daq:`      | IPS mode selection         | afpacket        |
| `#config daq_mode:` | Activating the inline mode | inline          |
| `#config logdir:`   | Hardcoded default log path | /var/logs/snort |
> ***Data Acquisition Modules (DAQ)*** are specific libraries used for packet I/O, bringing flexibility to process packets. It is possible to select DAQ type and mode for different purposes.

There are six DAQ modules available in Snort:

- `pcap`: Default mode, known as *sniffer mode*
- `afpacket`: Inline mode, known as *IPS mode*
- `ipq`: Inline mode on Linux by using Netfilter. It replaces the snort_inline patch. 
- `nfq`: Inline mode on Linux.
- `ipfw`: Inline on OpenBSD and FreeBSD b using divert sockets, with the pf and ipfw firewalls.
- `dump`: testing mode of inline and normalization

> The most popular modes are the default (pcap) and inline/IPS (afpacket)
###### Navigate to the "Step #6 Configure Output Plugins" Section

This section manages the outputs of the IDS/IPS actions, such as logging and alerting format details. The default action prompts everything in the console application, so configuring this part will help you use the Snort more efficiently.
###### Navigate to the Step #7: Customize Your Ruleset Section

|                           |                                                |                                |
| ------------------------- | ---------------------------------------------- | ------------------------------ |
| **TAG NAME**              | **INFO**                                       | **EXAMPLE**                    |
| **# site specific rules** | Hardcoded local and user-generated rules path. | include $RULE_PATH/local.rules |
| **#include $RULE_PATH/**  | Hardcoded default/downloaded rules path.       | include $RULE_PATH/rulename    |

*Note that "#" is commenting operator. You should uncomment a line to activate it.*

