> Zeek is an open-source and commercial network monitoring tool. 

[The official description;](https://docs.zeek.org/en/master/about.html) "Zeek (formerly Bro) is the world's leading platform for network security monitoring. Flexible, open-source, and powered by defenders." "Zeek is a passive, open-source network traffic analyser. Many operators use Zeek as a network security monitor (NSM) to support suspicious or malicious activity investigations. Zeek also supports a wide range of traffic analysis tasks beyond the security domain, including performance measurement and troubleshooting."
# Introduction to Network Monitoring Approaches

> Network monitoring is a set of management actions to watch/continuously overview and optionally save the network traffic for further investigation. This action aims to detect and reduce network problems, improve performance, increase overall productivity. 

It is a main part of the daily IT/SOC operations and *differs from Network Security Monitoring* and it's purpose.
### Network Monitoring

> Network monitoring is highyl focused on IT assets like uptime (availability), device health and connection quality (performance), and network traffic balance and management (configuration).

Monitoring and visualizing the network traffic, troubleshooting, and root cause analysis are also part of the *Network Monitoring Process*.

This model is helpful for network administrators and usually doesn't cover identifying non-asset in depth vulnerabilities and significant security concerns like internal threats and zero-day vulnerabilities. 

Usually, network monitoring is not within the SOC scope. It is linked to the enterprise IT/Network management team.
### Network Security Monitoring

> Network security monitoring is focused on network anomalies like ***rogue hosts, encrypted traffic, suspicious service and port usage, and malicious/suspicious traffic patterns*** in an intrusion/anomaly detection and response action. 

Monitoring and visualizing the network traffic and investigating suspicious events is a core part of Network Security Monitoring. 

- This model is helpful for security analysts/incident responders, security engineers and threat hunters and covers *identifying threats, vulnerabilities and security issues* with a set of rules, signatures and patterns. 

Network Security Monitoring is part of the SOC, and the actions are separated between tier 1-2-3 analyst levels.
### What is ZEEK?

> **Zeek** is an open-source and commercial passive Network Monitoring tool (traffic analysis framework) developed by Lawrence Berkeley Labs. 

Today, Zeek is supported by several developers, and Corelight provides and enterprise-ready fork of Zeek. 

Therefore, this tool is called both open-source and commercial. The differences between the open-source version and the commercial version are detailed [here](https://corelight.com/products/compare-to-open-source-zeek?hsLang=en).

Zeek differs from known monitoring and IDS/IPS tools by providing a wide range of detailed logs ready to investigate both for forensics and data analysis actions. Currently, Zeek provides 50+ logs in 7 categories.
### Zeek vs. Snort

> While both are called IDS/IPS, it is good to know the cons and pros of each tool and use them in a specific manner. While there are some overlapping functionalities, they have different purposes for usage.

| Tool             | Zeek                                                                                                                                                                               | Snort                                                                                                                                                   |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Capabilities     | NSM and IDS framework. It is heavily focused on network analysis. It is more focused on specific threats to trigger alerts. The detection mechanism is focused more on events.     | An IDS/IPS system. It is heavily focused on signatures to detect vulnerabilities. The detection mechanism is focused on signature patterns and packets. |
| Cons             | Hard to use. The analysis is done out of the Zeek, manually or by automation.                                                                                                      | Hard to detect complex threats.                                                                                                                         |
| Pros             | Provides in-depth traffic visibility. Useful for threat hunting. Ability to detect complex threats. Is has a scripting language and supports event correlation. Easy to read logs. | Easy to write rules. Cisco supported rules. Community rules.                                                                                            |
| Common Use Cases | Network monitoring, in-depth traffic investigation, Intrusion detecting in chained events.                                                                                         | Intrusion detection and prevention. Stop known attacks/threats.                                                                                         |
### Zeek Architecture

> Zeek has two primary layers: ***Event Engine*** and ***Policy Script Interpreter***. 

The event engine layer is where the packets are processed; it is called the event core and is responsible for describing the event without focusing on event details. 

It is where packages are divided into parts such as:

- Source and destination addresses
- Protocol identification
- Session analysis
- File Extraction

The **Policy Script Interpreter** layer is where the semantic analysis is conducted. It is responsible for describing the event correlations by using Zeek scripts.
### Zeek Frameworks

> Zeek has several frameworks to provide extended functionality in the scripting layer. These frameworks enhance Zeek's flexibility and compatibility with other network components. Each framework focuses on the specific use case and easily runs with Zeek installation.

For instance, we will be using the "Logging Framework" for all cases. 

Having ide on each framework's functionality can help users quickly identify an event of interest. 
#### Available Frameworks
|   |   |   |   |   |
|---|---|---|---|---|
|Logging|Notice|Input|Configuration|Intelligence|
|Cluster|Broker Communication|Supervisor|GeoLocation|File Analysis|
|Signature|Summary|NetControl|Packet Analysis|TLS Decryption|
### Zeek Outputs

> As mentioned before, Zeek provides 50+ log files under seven different categories, which are helpful in various areas such as:

- Traffic monitoring
- Intrusion detection
- Threat hunting
- Web analytics

This section is not intended to discuss the logs in depth, which will be covered in Task 3.

Once you run Zeek, it will automatically start investigating the traffic or given pcap file and generate logs automatically. Once you process a pcap with Zeek, it will create the logs int he working directory. If you run Zeek as a service, your logs will be located in the default log path. 

- The default log path is `/opt/zeek/logs`
### Working with Zeek

> There are two operation options for Zeek. The first one is ***running it as a service***, and the second option is ***running Zeek against a pcap***. 

Before starting working with Zeek, let's check the version of the Zeek instance with the following command: `zeek -v`.

Now we are sure that we have Zeek installed. Let's start the Zeek as a service! To do this, we need to use the "ZeekControl" module, as shown below. 

The **Zeek Control** module requires superuser permissions to use. You can elevate the session privileges and switch to the superuser account to examine the generated log files with the following command: `sudo su`

Here we can manage the Zeek service and view that status of the service. Primary management of the Zeek service is done with three commands:

- `status`
- `start`
- `stop`

> You can also use the "ZeekControl" mode with the following commands as well:

- `zeekctl status`
- `zeekctl start`
- `zeekctl stop`

The only way to listen to the live network traffic is using Zeek as a service. Apart from using the Zeek as a network monitoring tool, we can also use it as a packet investigator. To do so, we need to process the pcap files with Zeek, as shown below. 

Once you process a pcap file, Zeek automatically creates log files according to the traffic.

In pcap processing mode, logs are saved in the working directory. You can view the generated logs using the `ls -l` command.

```bash

root@ubuntu$ -C -r sample.pcap

root@ubuntu$ ls -l
-rw-r--r-- 1 ubuntu ubuntu  11366 Mar 13 20:45 conn.log
-rw-r--r-- 1 ubuntu ubuntu    763 Mar 13 20:45 dhcp.log

```

| Parameter | Description                              |
| --------- | ---------------------------------------- |
| `-r`      | Reading option, read/process a pcap file |
| `-C`      | Ignoring checksum errors                 |
| `-v`      | Version information                      |
| `zeekctl` | ZeekControl module                       |
> Investigating the generated logs will require command-line tools like `cat`,`cut`, `grep`, `uniq` and additional tools (zeek-cut). We will cover them in the following tasks. 
# Zeek Logs

> Zeek generates log files according to the traffic data. You will have logs for every connection in the wire, including the application level protocols and fields. 

Zeek is capable of identifying 50+ logs and categorizing them into seven categories. 

Zeek logs are well structured and tab-separated ASCII files, so reading and processing them is easy but requires effort. 

- You should be familiar with networking and protocols to correlate the logs in an investigation, know where to focus, and find a specific piece of evidence. 

Each log consists of multiple fields, and each field holds a different pattern part of the traffic data. Correlation is done through a unique value called **UID**. The **UID** represents the unique identifier assigned to each session. 
### Zeek Logs in a Nutshell

| Category             | Description                                                             | Log Files                                                                                                                                                                                                                                                                                                                          |
| -------------------- | ----------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Network              | Network Protocol Logs                                                   | _conn.log, dce_rpc.log, dhcp.log, dnp3.log, dns.log, ftp.log, http.log, irc.log, kerberos.log, modbus.log, modbus_register_change.log, mysql.log, ntlm.log, ntp.log, radius.log, rdp.log, rfb.log, sip.log, smb_cmd.log, smb_files.log, smb_mapping.log, smtp.log, snmp.log, socks.log, ssh.log, ssl.log, syslog.log, tunnel.log._ |
| Files                | File analysis result logs                                               | *files.log*, *oscp.log*, *pe.log*, *x509.log*                                                                                                                                                                                                                                                                                      |
| NetControl           | Network control and flow logs                                           | *netcontrol.log*, *netcontrol_drop.log*, *netcontrol_shunt.log*, *netcontrol_catch_release.log*, *openflow.log*                                                                                                                                                                                                                    |
| Detection            | Detection and possible indicator log                                    | *intel.log*, *notice.log*, *notice_alarm.log*, *signatures.log*, *traceroute.log*                                                                                                                                                                                                                                                  |
| Network Observations | Network flow logs                                                       | *known_certs.log*, *known_hosts.log*, *known_modbus.log*, *known_services.log*, *software.log*                                                                                                                                                                                                                                     |
| Miscellaneous        | Additional logs cover external alerts, inputs and failures              | _barnyard2.log, dpd.log, unified2.log, unknown_protocols.log, weird.log, weird_stats.log._                                                                                                                                                                                                                                         |
| Zeek Diagnostic      | Zeek diagnostic logs cover system messages, actions and some statistics | _broker.log, capture_loss.log, cluster.log, config.log, loaded_scripts.log, packet_filter.log, print.log, prof.log, reporter.log, stats.log, stderr.log, stdout.log._                                                                                                                                                              |
> Please refer to [Zeek's official documentation](https://docs.zeek.org/en/current/script-reference/log-files.html) and [Corelight log cheat sheet](https://corelight.com/about-zeek/zeek-data) for more information. 

Although there are multiple log files, some log files are updated daily, and some are updated in each session. Some of the most commonly used logs are explained in the given table.

| Update Frequency | Log Name             | Description                                    |
| ---------------- | -------------------- | ---------------------------------------------- |
| Daily            | *known_hosts.log*    | List of host that completed TCP handshake.     |
| Daily            | *known_services.log* | List of services used by hosts.                |
| Daily            | *known_certs.log*    | List of SSL certificates                       |
| Daily            | *software.log*       | List of software used on the network.          |
| Per Session      | *notice.log*         | Anomalies detected by Zeek.                    |
| Per Session      | *intel.log*          | Traffic contains malicious patterns/indicators |
| Per Session      | *signatures.log*     | List of triggered signatures                   |
> A difficulty of working with Zeek is having the required network knowledge and investigative mindset. 
### Brief Log Usage Primer Table

| **Overall Info**     | **Protocol Based** | **Detection**    | **Observation**      |
| -------------------- | ------------------ | ---------------- | -------------------- |
| _conn.log_           | _http.log_         | _notice.log_     | _known_host.log_     |
| _files.log_          | _dns.log_          | _signatures.log_ | _known_services.log_ |
| _intel.log_          | _ftp.log_          | _pe.log_         | _software.log_       |
| _loaded_scripts.log_ | _ssh.log_          | _traceroute.log_ | _weird.log_          |
> You can categorize the logs before starting an investigation. Thus, finding the evidence/anomaly you are looking for will be easier.

The given table is a brief example of using multiple log files. You can create your working model or customize the given one. Make sure you read each log description and understand the purpose to know what to expect from the corresponding log file. 

Note that these are not the only ones to focus on. Investigated logs are highly associated with the investigation case type and hypothesis, so do not just rely on the logs given in the example table.

> The table shows us how to use multiple logs to identify anomalies and run an investigatio by correlating across available logs. 

- **Overall Info**: The aim is to review the overall connections, shared files, loaded scripts and indicators at once. This is the first step of the investigation.
- **Protocol Based**: Once you review the overall traffic and find suspicious indicators or want to conduct a more in-depth investigation, you focus on a specific protocol. 
- **Detection**: Use the prebuild or custom scripts and signature outcomes to support your findings by having additional indicators or linked actions.
- **Observation**: The summary of the hosts, services, software and unexpected activity statistics will help you discover possible missing points and conclude the investigation.

> Remember, we mentioned the pros and cons of Zeek logs at the beginning of this task. Now, let's demonstrate the log viewing and identify the differences between them. 

**Recall 1**: Zeek logs are well structured and tab-separated ASCII files, so reading and processign them is easy but requires effort. 
**Recall 2**: Investigating the generated logs will require command line tools (cat, cut, grep sort, and uniq) and additional tools (zeek cut)

> The above image shows that reading the logs with tools is not enough to spot an anomaly quickly. Logs provide a ***vast amount of information*** and data to investigate and correlate. You will need to have technical knowledge and event correlation ability to carry out an investigation.

It is possible to use external visualization and correlation tools such as ELK and Splunk. 
- We will focus on using and processing the logs with a hands on approach.

In addition to Linux command-line tools, one auxiliary program called `zeek-cut` reduces the effort of extracting specific columns from log files. 

- Each log file provides "field names" in the beginning. This information will help you while using `zeek-cut`. Make sure that you use the "fields" and not the "types".

|   |   |
|---|---|
|**Tool/Auxilary Name**|**Purpose**|
|**Zeek-cut**|Cut specific columns from zeek logs.|
> Let's use `zeek-cut` in action.

Let's extract the UID, protocol, source and destination hosts, and source and destination ports from the conn.log.

We will first read the logs with the cat command and then extract the event of interest fields with `zeek-cut` auxiliary to compare the difference.
# CLI Kung-Fu Recall: Processing Zeek Logs

> **Graphical User Interfaces** are handy and good for accomplishing tasks and processing information quickly. 

There are multiple advantages of GUIs, especially when processing the information visually. However, when processing massive amounts of data, GUIs are not stable and as effective as the CLI (Command Line Tools) tools.

The critical point is: *what if there is no "function/button/feature" for what you want to find/view/extract?*

Having the power to manipulate the data at the command line is a crucial skill for analysts. Not only in this room but each time you deal with packets, you will need to use command-line tools, Berkeley Packet Filters and regular expressions to find/view/extract the data you are looking for.

| Category      | Command Purpose and Usage                                        | Category  | Command Purpose and Usage                                                            |
| ------------- | ---------------------------------------------------------------- | --------- | ------------------------------------------------------------------------------------ |
| Basics        | View command history: `ubuntu@ubuntu$ history`                   | Read File | Read sample.txt file: `ubuntu@ubuntu$ cat sample.txt`                                |
|               | Execute the 10th command in history: `ubuntu@ubuntu$ !10`        |           | Read the first 10 lines of the file: `ubuntu@ubuntu$ head sample.txt`                |
|               | Execute the previous command: `ubuntu@ubntu$ !!`                 |           | Read the last 10 lines of the file: `ubuntu@ubuntu$ tail sample.txt`                 |
| Find & Filter | Cut the first field: `ubuntu@buntu$ cat test.txt \| cut -f 1`    | Advanced  | Print line 11: `ubuntu@ubuntu$ cat test.txt \| sed -n '11p'`                         |
|               | Cut the first column: `ubuntu@ubuntu$ cat test.txt \| cut -c1`   |           | Print lines between 10-15: `ubuntu@ubuntu$ cat test.txt \| awk 'NR < 11 {porint $0}` |
|               | Filter specific keywords: `cat test.txt \| grep 'keyword'`       |           | Print lines below 11: `ubuntu@ubuntu$ cat test.txt \| awk 'NR < 11 {print $0}`       |
|               | Sort outputs alphabetically: `cat test.txt \| sort`              |           | Print line 11: `ubuntu@ubuntu$ cat test.txt \| awk 'NR == 11 {print $0}`             |
|               | Sort outputs numerically `cat test.txt \| sort -n`               |           |                                                                                      |
|               | Eliminate duplicate lines: `ubuntu@ubuntu$ cat test.txt \| uniq` |           |                                                                                      |
|               | Count line numbers: `ubuntu@ubuntu$ cat test.txt \| wc -1`       |           |                                                                                      |
|               | Show line numbers: `ubuntu@ubuntu$ cat test.txt \| n1`           |           |                                                                                      |

| Special | Filter Specific fields of Zeek logs:                                  |
| ------- | --------------------------------------------------------------------- |
|         | `ubuntu@ubuntu$ cat signatures.log \| zeek-cut uid src_addr dst_addr` |

| Use Case                                         | Description                                                                                      |
| ------------------------------------------------ | ------------------------------------------------------------------------------------------------ |
| `sort \| uniq`                                   | Remove duplicate values                                                                          |
| `sort \| uniq -c`                                | Remove duplicates and count the number of occurences for each value                              |
| `sort -nr`                                       | Sort values numerically and recursively                                                          |
| `rev`                                            | Reverse string characters                                                                        |
| `cut -f 1`                                       | Cut field 1                                                                                      |
| `cut -d '.' -f 1-2`                              | Split the string on every dot and print keep the first two fields                                |
| `grep -v 'test'`                                 | Display lines that don't match the "test" string                                                 |
| `grep -v -e 'test1' -e 'test2'`                  | Display lines that don't match one or both "test1" and "test2" strings.                          |
| `file`                                           | View file information                                                                            |
| `grep -rin Testvalue1 * \| column -t \| less -S` | Search the "testvalue1" string everywhere, organize column spaces and view the output with less. |
# Zeek Signatures

> Zeek supports signatures to have rules and event correlations to find noteworthy activities on the network. Zeek signatures use low-level pattern matching and cover conditions similar to Snort rules. 

Unlike Snort Rules, Zeek rules are not the primary event detection point. Zeek has a scripting language and can chain multiple events to find an event of interest. 

We focus on the signatures in this task, and then we will focus on Zeek scripting in the following task.

The signature breakdown is shown in the table below;

- **Signature ID**: **Unique** signature name. 
- **Conditions**: 
	- **Header**: Filtering the packet headers for specific source and destination addresses, protocol and port numbers.
	- **Content**: Filtering the packet payload for specific value/pattern.
- **Action**:
	- **Default Action**: Create the "signatures.log" file in case of a signature match.
	- **Additional Action**: Trigger a Zeek script.

> Let's dig more into Zeek signatures. The below table provides the most common conditions and filters for the Zeek signatures.

| Condition Field      | Available Filters                                                               |
| -------------------- | ------------------------------------------------------------------------------- |
| Header               | `src-ip`: Source IP                                                             |
|                      | `dst-ip`: Destination IP                                                        |
|                      | `src-port`: Source Port                                                         |
|                      | `dst-port`: Destination Port                                                    |
|                      | `ip-proto`: Target protocol. Supported protocols: TCP, UDP, ICMP ICMP6, IP, IP6 |
| Content              | `payload`: Packet payload                                                       |
|                      | `http-request`: Decoded HTTP requests                                           |
|                      | `http-request-header`: Client-side HTTP headers.                                |
|                      | `http-request-body`: Client-side HTTP body requests.                            |
|                      | `http-reply-header`: Server-side HTTP headers.                                  |
|                      | `http-reply-body`: Server-side HTTP request bodies.                             |
|                      | `ftp`: Command line input of FTP sessions                                       |
| Context              | `same-ip`: Filtering the source and destination addresses for duplication.      |
| Action               | `event`: Signature match message.                                               |
| Comparison Operators | `==, !=, <, <=, >, >=`                                                          |
| Note!                | Filters accept string, numeric and regex values.                                |
```Bash
ubuntu@ubuntu$ zeek -C -r sample.pcap -s sample.sig
```

> Zeek signatures use the ".sig" extension.
> 	- `-C`: Ignore checksum errors.
> 	- `-r`: Read pcap file.
> 	- `-s`: Use signature file
### Example | Cleartext Submission of Password

> Let's create a simple signature to detect HTTP cleartext passwords.

```Bash
signature http-password {
     ip-proto == tcp
     dst-port == 80
     payload /.*password.*/
     event "Cleartext Password Found!"
}

# signature: Signature name.
# ip-proto: Filtering TCP connection.
# dst-port: Filtering destination port 80.
# payload: Filtering the "password" phrase.
# event: Signature match message.
```

Remember, Zeek signatures accept regex. Regex * matches any character zero or more times.

The rule will match when a "password" phrase is detected in the packet payload. 

Once the match occurs, Zeek will generate an alert and create additional log files (signatures.log and notice.log).

```Bash
ubuntu@ubuntu$ zeek -C -r http.pcap -s http-password.sig 
ubuntu@ubuntu$ ls
clear-logs.sh  conn.log  files.log  http-password.sig  http.log  http.pcap  notice.log  packet_filter.log  signatures.log

ubuntu@ubuntu$ cat notice.log  | zeek-cut id.orig_h id.resp_h msg 
10.10.57.178	44.228.249.3	10.10.57.178: Cleartext Password Found!
10.10.57.178	44.228.249.3	10.10.57.178: Cleartext Password Found!

ubuntu@ubuntu$ cat signatures.log | zeek-cut src_addr dest_addr sig_id event_msg 
10.10.57.178		http-password	10.10.57.178: Cleartext Password Found!
10.10.57.178		http-password	10.10.57.178: Cleartext Password Found!
```

> As shown in the above terminal output, the signatures.log and notice.log provide basic details and the signature message. Both of the logs also have the application banner field. So it is possible to know where the signature match occurs.

Let's look at the application banner.

```bash
ubuntu@ubuntu$ cat signatures.log | zeek-cut sub_msg
POST /userinfo.php HTTP/1.1\x0d\x0aHost: testphp.vulnweb.com\x0d\x0aUser-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:98.0) Gecko/20100101 Firefox/...

ubuntu@ubuntu$ cat notice.log  | zeek-cut sub
POST /userinfo.php HTTP/1.1\x0d\x0aHost: testphp.vulnweb.com\x0d\x0aUser-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:98.0) Gecko/20100101 Firefox/...
```

> We will demonstrate only one log file output to avoid duplication after this point. You can practice discovering the event of interest by analyzing notice.log and signatures.log.
### Example | FTP Brute Force

> Let's create another rule to filter FTP traffic. 

This time, we will use the FTP content filter to investigate command-line inputs of the FTP traffic. The aim is to detect FTP "admin" login attempts. 

This basic signature will help us identify the admin login attempts and have an idea of possible admin account abuse or compromise events.

```markdown
signature ftp-admin {
     ip-proto == tcp
     ftp /.*USER.*dmin.*/
     event "FTP Admin Login Attempt!"
}
```

> Let's run the Zeek with the signature and investigate the signatures.log and notice.log

```Bash
ubuntu@ubuntu$ zeek -C -r ftp.pcap -s ftp-admin.sig
ubuntu@ubuntu$ cat signatures.log | zeek-cut src_addr dst_addr event_msg sub_msg | sort -r| uniq
10.234.125.254	10.121.70.151	10.234.125.254: FTP Admin Login Attempt!	USER administrator
10.234.125.254	10.121.70.151	10.234.125.254: FTP Admin Login Attempt!	USER admin 
```

> Our rule shows us that there are multiple logging attempts with account names containing the "admin" phrase. The output gives us great information to notice if there is a brute-force attempt for an admin account. 

This signature can be considered a **case signature**. While it is accurate and works fine, we need global signatures to detect the "known threats/anomalies". We will need those case-based signatures for significant and sophistical anomalies like zero days and insider attacks in real-life environments. 

- Having individual rules for each case will create dozens of logs and alerts and cause missing the real anomaly.
- The critical point is *logging logically, not logging everything.*

We can improve our signature by not limiting the focus only to an admin account. In that case, we need to know how the FTP protocol works and the default response codes. If you don't know these details, please refer to [RFC documentation](https://datatracker.ietf.org/doc/html/rfc765).

**Let's optimise our rule and make it detect all possible FTP brute-force attempts.**

> This signature will create logs for each event containing "FTP 530 response", which allows us to track the login failure events regardless of username. 

```markdown
signature ftp-brute {
     ip-proto == tcp
     payload /.*530.*Login.*incorrect.*/
     event "FTP Brute-force Attempt"
}
```

> Zeek signature files can consist of multiple signatures. Therefore we can have one file for each protocol/situation/threat type. Let's demonstrate this feature in our global rule.

```markdown
signature ftp-username {
    ip-proto == tcp
    ftp /.*USER.*/
    event "FTP Username Input Found!"
}

signature ftp-brute {
    ip-proto == tcp
     payload /.*530.*Login.*incorrect.*/
    event "FTP Brute-force Attempt!"
}
```

> Let's merge both of these signatures into a single file. We will have two different signatures, and they will generate alerts according to **match status.**

The result will show us how we benefit from this action. Again, we need the "CLI-Kung-Fu" skills to extract the event of interest. 

> This rule should show us two types of alerts and help us to correlate the events by having "FTP Username Input" and "FTP Brute-Force Attempt" event messages. Let's investigate the logs. We're grepping the logs in range 1001-1004 to demonstrate that the first rule matches two different accounts (admin and administrator)

```Bash
ubuntu@ubuntu$ zeek -C -r ftp.pcap -s ftp-admin.sig
ubuntu@ubuntu$ cat notice.log | zeek-cut uid id.orig_h id.resp_h msg sub | sort -r| nl | uniq | sed -n '1001,1004p'
  1001	CeMYiaHA6AkfhSnd	10.234.125.254	10.121.70.151	10.234.125.254: FTP Username Input Found!	USER admin
  1002	CeMYiaHA6AkfhSnd	10.234.125.254	10.121.70.151	10.121.70.151: FTP Brute-force Attempt!	530 Login incorrect.
  1003	CeDTDZ2erDNF5w7dyf	10.234.125.254	10.121.70.151	10.234.125.254: FTP Username Input Found!	USER administrator
  1004	CeDTDZ2erDNF5w7dyf	10.234.125.254	10.121.70.151	10.121.70.151: FTP Brute-force Attempt!	530 Login incorrect.
```
### Snort Rules in Zeek?

> While Zeek was known as Bro, it supported Snort rules with a script called **Snort2Bro**, which converted Snort rules to Bro signatures. 

However, after the rebranding, workflows between the two platforms have changed. [The official Zeek document](https://docs.zeek.org/en/master/frameworks/signatures.html) mentions that the script is no longer supported and is not a part of the Zeek distribution.
# Zeek Scripts

> Zeek has its own event-driven scripting language, which is as powerful as high-level languages and allows us to investigate and correlate the detected events. 

Since it is as capable as high-level programming languages, you will need to spend time on Zeek scripting language in order to become proficient. 

In this room, we will cover the basics of Zeek scripting to help understand, modify and create basic scripts. 

Note that scripts can be used to apply a policy and in this case, they are called **policy scripts**.

|                                                                                                                                                                                                          |                                                                              |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| Zeek has base scripts installed by default, and these are not intended to be modified.                                                                                                                   | These scripts are located in "/opt/zeek/share/zeek/base".                    |
| User-generated or modified scripts should be located in a specific path.                                                                                                                                 | These scripts are located in  <br>**"/opt/zeek/share/zeek/site".**           |
| Policy scripts are located in a specific path.                                                                                                                                                           | These scripts are located in **"/opt/zeek/share/zeek/policy"**.              |
| Like Snort, to automatically load/use a script in live sniffing mode, you must identify the script in the Zeek configuration file. You can also use a script for a single run, just like the signatures. | The configuration file is located in "/opt/zeek/share/zeek/site/local.zeek". |
- Zeek scripts use the **.zeek** extension.
- Do not modify anything under the "zeek/base" directory. User-generated and modified scripts should be in the "zeek/site" directory. 
- You can call scripts in live monitoring mode by loading them with the command `load @/script/path` or `load @script-name` in local.zeek file.
- Zeek is event-oriented, not packet-oriented. We need to use/write scripts to handle the event of interest. 

```markdown
ubuntu@ubuntu$ zeek -C -r sample.pcap -s sample.sig
```
### GUI vs. Scripts

> Have you ever thought about automating tasks in Wireshark, tshark or tcpdump? Zeek provides that chance to use with its scripting power. Let's say we need to extract all available DHCP hostnames from a pcap file. In that case, we have several options like using tcpdump, Wireshark, tshark or Zeek.

Let's see Wireshark on the stage first. You can have the same information with Wireshark. However, while this information can be extracted using Wireshark it is not easy to transfer the data to another tool for processing.

tcpdump and tshark are command-line tools, and it is easy to extract and transfer data to another tool for processing and correlating.

##### extracting hostnames with tcpdump and tshark

```markdown
ubuntu@ubuntu$ sudo tcpdump -ntr smallFlows.pcap port 67 or port 68 -e -vv | grep 'Hostname Option' | awk -F: '{print $2}' | sort -nr | uniq | nl
     1	 "vinlap01"
     2	 "student01-PC"
ubuntu@ubuntu$ tshark -V -r smallFlows.pcap -Y "udp.port==67 or udp.port==68" -T fields -e dhcp.option.hostname | nl | awk NF
     1	student01-PC
     2	vinlap01
```

> Now let's see Zeek scripts in action. First, let's look at the components of the Zeek script. Here the first, second and fourth lines are predefined syntaxes of the scripting language. The only part we created is the third line which tells Zeek to extract DHCP hostnames. 

Now compare this automation ease with the rest of the methods. Obviously, this four-line script is easier to create and use. 

While tcpdump and tshark can provide similar results, transferring uncontrolled data through multiple pipelines is not much preferred.

```markdown
event dhcp_message (c: connection, is_orig: bool, msg: DHCP::Msg, options: DHCP::Options)
{
print options$host_name;
}
```

> Now let's use the Zeek script and see the output.

```markdown
ubuntu@ubuntu$ zeek -C -r smallFlows.pcap dhcp-hostname.zeek 
student01-PC
vinlap01
```

> The provided outputs show that our script works fine and can extract the requested information. This should show why Zeek is helpful in data extraction and correlation. 

Note that Zeek scripting is a programming language itself, and we are not covering the fundamentals of Zeek scripting. In this room, we will cover the logic of Zeek scripting and how to use Zeek scripts. 

You can learn and practice Zeek scripting language by using [Zeek's official training platform](https://try.bro.org/#/?example=hello) for free.

There are multiple options to trigger conditions in Zeek. Zeek can use "Built-In Function" (Bif) and protocols to extract information from traffic data. You can find supported protocols and Bif either by looking in your setup or visiting the [Zeek repo](https://docs.zeek.org/en/master/script-reference/scripts.html).

*/opt/zeek/share/zeek/base/bif*
*/opt/zeek/share/zeek/base/bif/plugins*
*/opt/zeek/share/zeek/base/protocols*

# Zeek Scripts | Scripts and Signatures

### Scripts 101 | Write Basic Scripts

> Scripts contain operators, types, attributes, declarations and statements, and directives.

Let's look at a simple event called "zeek_init" and "zeek_done".

These events work once the Zeek process starts and stops. Note that these events don't have parameters, and some events will require parameters. 

```markdown
event zeek_init()
    {
     print ("Started Zeek!");
    }
event zeek_done()
    {
    print ("Stopped Zeek!");
    }

# zeek_init: Do actions once Zeek starts its process.
# zeek_done: Do activities once Zeek finishes its process.
# print: Prompt a message on the terminal.
```

> Run Zeek with a script:

```markdown
ubuntu@ubuntu$ zeek -C -r sample.pcap 101.zeek 
Started Zeek!
Stopped Zeek!
```

> The above output shows how the script works and provides messages on the terminal. Zeek will create logs in the working directory separately from the scripts tasks.

Let's print the packet data to the terminal and see the raw data. In this script, we are requesting details of a connection and extracting them without filtering or sorting of the data. To accomplish this, we are using the `"new_connection"` event. This event is *automatically generated for each new connection*.  This script provides bulk information on the terminal.

We need to get familiar with Zeek's data structure to reduce the amount of information and focus on the event of interest. To do so, we need to investigate the bulk data.

```shell
event new_connection(c: connection)
{
	print c;
}
```

Run Zeek with the script:

```markdown
ubuntu@ubuntu$ zeek -C -r sample.pcap 102.zeek 
[id=[orig_h=192.168.121.40, orig_p=123/udp, resp_h=212.227.54.68, resp_p=123/udp], orig=[size=48, state=1, num_pkts=0, num_bytes_ip=0, flow_label=0, l2_addr=00:16:47:df:e7:c1], resp=[size=0, state=0, num_pkts=0, num_bytes_ip=0, flow_label=0, l2_addr=00:00:0c:9f:f0:79], start_time=1488571365.706238, duration=0 secs, service={}, history=D, uid=CajwDY2vSUtLkztAc, tunnel=, vlan=121, inner_vlan=, dpd=, dpd_state=, removal_hooks=, conn=, extract_orig=F, extract_resp=F, thresholds=, dce_rpc=, dce_rpc_state=, dce_rpc_backing=, dhcp=, dnp3=, dns=, dns_state=, ftp=, ftp_data_reuse=F, ssl=, http=, http_state=, irc=, krb=, modbus=, mysql=, ntlm=, ntp=, radius=, rdp=, rfb=, sip=, sip_state=, snmp=, smb_state=, smtp=, smtp_state=, socks=, ssh=, syslog=]
```

The above terminal provides bulk data for each connection. This style is not the best usage, and in real life, we will need to filter the information for specific purposes. If you look closely at the output, you can see an ID and field value for each part. 

To filter the event of interest, we will use the primary tag (in this case, it is c --coms from "c:connection"--), id value (id=) and field name. You should notice that the fields are the same as the fields in the log files. 

```shell
event new_connection(c: connection)
{
	print ("###########################################################");
	print ("");
	print ("New Connection Found!");
	print ("");
	print fmt ("Source Host: %s # %s --->", c$id$orig_h, c$id$orig_p);
	print fmt ("Destination Host: resp: %s # %s <---", c$id$resp_h, c$id$resp_p);
	print ("");
}

# %s: Identifies string output for the source.
# c$id: Source reference field for the identifier.
```

Now that we have a general idea of running a script and following the provided output on the console, let's look closer to another script that extends information from packets. The script above creates logs and prompts each source and destination address for each connection.

Let's see this script in action:

```markdown
ubuntu@ubuntu$ zeek -C -r sample.pcap 103.zeek 
###########################################################
New Connection Found! Source Host: 192.168.121.2 # 58304/udp ---> 
Destination Host: resp: 192.168.120.22 # 53/udp <--- 
###########################################################
```

> The above output shows that we successfully extract specific information from the events. Remember that this script extracts the event of interest (in this example, a new connection), and we still have logs in *the working directory*. We can always modify and optimize the scripts at any time.

## Scripts 201 | Use Scripts and Signatures Together

Up to here, we have covered the basics of Zeek scripts. Now it is time to use scripts collaboratively with other scripts and signatures to get one step closer to event correlation. Zeek scripts can refer to signatures and other Zeek scripts as well. This flexibility provides a massive advantage in event correlation. 

Let's demonstrate this concept with an example. We will create a script that detects if our previously created **"ftp-admin** rule has a hit.

```markdown
event signature_match (state: signature_state, msg: string, data: string)
{
if (state$sig_id == "ftp-admin")
    {
    print ("Signature hit! --> #FTP-Admin ");
    }
}
```

> This basic script quickly checks if there is a signature hit and provides terminal output to notify us. We are using the `"signature_match"` event to accomplish this. 

You can read more about events [here](https://docs.zeek.org/en/master/scripts/base/bif/event.bif.zeek.html?highlight=signature_match). Note that we are looking only for "ftp-admin" signature hits. The signature is shown below. 

```markdown
signature ftp-admin {
    ip-proto == tcp
    ftp /.*USER.*admin.*/
    event "FTP Username Input Found!"
}
```

**Let's see this script in action.**

```markdown
ubuntu@ubuntu$ zeek -C -r ftp.pcap -s ftp-admin.sig 201.zeek 
Signature hit! --> #FTP-Admin Signature hit! --> #FTP-Admin
Signature hit! --> #FTP-Admin Signature hit! --> #FTP-Admin
```

> The above outputs show that we successfully combined the signature and script. Zeek processed the signature and logs then the script controlled the outputs and provided a terminal output for each rule hit.

## Scripts 202 | Load Local Scripts

We mentioned Zeek has base scripts located in `/opt/zeek/share/zeek/base`. You can load all local scripts identified in your "local.zeek" file. 

Not that base scripts cover multiple framework functionalities. You can load all base scripts by easily running the `local` command. 

```markdown
ubuntu@ubuntu$ zeek -C -r ftp.pcap local 
ubuntu@ubuntu$ ls
101.zeek  103.zeek          clear-logs.sh  ftp.pcap            packet_filter.log  stats.log
102.zeek  capture_loss.log  conn.log       loaded_scripts.log  sample.pcap        weird.log 
```

The above output demonstrates how to run all base scripts using the "local" command. Look at the above terminal output; Zeek provided additional log files this time. Loaded scripts generated `loaded_scripts.log`, `capture_loss.log`, `stats.log` files.

Note that, in our instance, 465 scripts loaded and used by using the "local" command. However, Zeek doesn't provide log files the scripts that don't have hits or results.

#### Load Specific Scripts

Another way to load scripts is by identifying the script path. In that case, you have the opportunity of loading a specific script or framework. Let's go back to FTP brute-forcing case. We created a script that detects multiple admin login failures in previous steps. Zeek has an FTP brute-force detection script as well. Now let's use the default script and identify the differences.

```markdown
ubuntu@ubuntu$ zeek -C -r ftp.pcap /opt/zeek/share/zeek/policy/protocols/ftp/detect-bruteforcing.zeek 

ubuntu@ubuntu$ cat notice.log | zeek-cut ts note msg 
1024380732.223481	FTP::Bruteforcing	10.234.125.254 had 20 failed logins on 1 FTP server in 0m1s
```

The above output shows how to load a specific script. This script provides much more information than the one we created. It provides one single line output and a connection summary for the suspicious incident. You can find and read more on the prebuilt scripts and frameworks by visiting Zeek's online book https://docs.zeek.org/en/master/frameworks/index.html 

# Zeek Scripts | Frameworks

## Scripts 203 | Load Frameworks

Zeek has ***15+ Frameworks*** that help analysts to discover the different events of interest. In this task, we will cover the common frameworks and functions. You can find and read more on the prebuilt scripts and frameworks by visiting Zeek's online book [here](https://docs.zeek.org/en/master/frameworks/index.html).

### File Framework | Hashes

Not all framework functionalities are intended to be used in CLI mode. The majority of them are used in scripting. You can easily see the usage of frameworks in scripts by calling a specific framework as `load @ $PATH/base/frameworks/framework-name`.

Now, let's use a prebuilt function of the file framework to have MD5, SHA1 and SHA256 hashes of the detected files. We will call the `File Analysis` frameworks's "hash-all-files" script to accomplish this. Before loading the scripts, let's look at how it works. 

```markdown
ubuntu@ubuntu$ cat hash-demo.zeek 
# Enable MD5, SHA1 and SHA256 hashing for all files.
@load /opt/zeek/share/zeek/policy/frameworks/files/hash-all-files.zeek
```

The above output shows how frameworks are loaded. In earlier tasks, we mentioned that Zeek highly relies on scripts, and the frameworks depend on scripts. Let's have a closer look at the file hash framework and see the script behind it. 

```markdown
ubuntu@ubuntu$ cat /opt/zeek/share/zeek/policy/frameworks/files/hash-all-files.zeek 
# Enable MD5, SHA1 and SHA256 hashing for all files.

@load base/files/hash
event file_new(f: fa_file)
	{
	Files::add_analyzer(f, Files::ANALYZER_MD5);
	Files::add_analyzer(f, Files::ANALYZER_SHA1);
	Files::add_analyzer(f, Files::ANALYZER_SHA256);
	}
```

Now let's execute the script and investigate the log file.

```markdown
ubuntu@ubuntu$ zeek -C -r case1.pcap hash-demo.zeek
ubuntu@ubuntu$ zeek -C -r case1.pcap /opt/zeek/share/zeek/policy/frameworks/files/hash-all-files.zeek 

ubuntu@ubuntu$ cat files.log | zeek-cut md5 sha1 sha256
cd5a4d3fdd5bffc16bf959ef75cf37bc	33bf88d5b82df3723d5863c7d23445e345828904	6137f8db2192e638e13610f75e73b9247c05f4706f0afd1fdb132d86de6b4012
b5243ec1df7d1d5304189e7db2744128	a66bd2557016377dfb95a87c21180e52b23d2e4e	f808229aa516ba134889f81cd699b8d246d46d796b55e13bee87435889a054fb
cc28e40b46237ab6d5282199ef78c464	0d5c820002cf93384016bd4a2628dcc5101211f4	749e161661290e8a2d190b1a66469744127bc25bf46e5d0c6f2e835f4b92db18
```

Look at the above terminal outputs. Both of the scripts provided the same result. Here the preference is up to the suer. Both of the usage formats are true. Prebuilt frameworks are commonly used in scripting's with the `@load` method. Specific scripts are sued as practical scripts for particular use cases.

### File Framework | Extract Files

The file framework can extract the files transferred. Let's see this feature in action.

```markdown
ubuntu@ubuntu$ zeek -C -r case1.pcap /opt/zeek/share/zeek/policy/frameworks/files/extract-all-files.zeek

ubuntu@ubuntu$ ls
101.zeek  102.zeek  103.zeek  case1.pcap  clear-logs.sh  conn.log  dhcp.log  dns.log  extract_files  files.log  ftp.pcap  http.log  packet_filter.log  pe.log
```

We successfully extracted files from the pcap. A new folder called `extract_files` is automatically created, and all detected files are located in it. First, we will list the contents of the folder, and then we will use the `file` command to determine the file type of the extracted files.

```markdown
ubuntu@ubuntu$ ls extract_files | nl
     1	extract-1561667874.743959-HTTP-Fpgan59p6uvNzLFja
     2	extract-1561667889.703239-HTTP-FB5o2Hcauv7vpQ8y3
     3	extract-1561667899.060086-HTTP-FOghls3WpIjKpvXaEl

ubuntu@ubuntu$ cd extract_files

ubuntu@ubuntu$ file *| nl
     1	extract-1561667874.743959-HTTP-Fpgan59p6uvNzLFja:  ASCII text, with no line terminators
     2	extract-1561667889.703239-HTTP-FB5o2Hcauv7vpQ8y3:  Composite Document File V2 Document, Little Endian, Os: Windows, Version 6.3, Code page: 1252, Template: Normal.dotm, Last Saved By: Administrator, Revision Number: 2, Name of Creating Application: Microsoft Office Word, Create Time/Date: Thu Jun 27 18:24:00 2019, Last Saved Time/Date: Thu Jun 27 18:24:00 2019, Number of Pages: 1, Number of Words: 0, Number of Characters: 1, Security: 0
     3	extract-1561667899.060086-HTTP-FOghls3WpIjKpvXaEl: PE32 executable (GUI) Intel 80386, for MS Windows
```

Zeek extracted three files. The `file` command shows us one .txt file, one .doc/,docx file and one .exe file. Zeek renames extracted files. The name format consists of four values that come from `conn.log` and `files.log`; default `extract` keyword, `timestamp` value, `protocol` (source), and connection id (conn_uids).

Let's look at the files.log to understand possible anomalies better and verify the findings. Look at the below output; files.log provides the same results with additional details. Let's focus on the .exe and correlate this finding by searching its connection id (conn_uids).

> The given terminal output shows us that there are three files extracted from the traffic capture. Let's look at the file.log and correlate the findings with the rest of the log files. 

```markdown
ubuntu@ubuntu$ cat files.log | zeek-cut fuid conn_uids tx_hosts rx_hosts mime_type extracted | nl
     1	Fpgan59p6uvNzLFja	CaeNgL1QzYGxxZPwpk	23.63.254.163	10.6.27.102	text/plain	extract-1561667874.743959-HTTP-Fpgan59p6uvNzLFja
     2	FB5o2Hcauv7vpQ8y3	CCwdoX1SU0fF3BGBCe	107.180.50.162	10.6.27.102	application/msword	extract-1561667889.703239-HTTP-FB5o2Hcauv7vpQ8y3
     3	FOghls3WpIjKpvXaEl	CZruIO2cqspVhLuAO9	107.180.50.162	10.6.27.102	application/x-dosexec	extract-1561667899.060086-HTTP-FOghls3WpIjKpvXaEl

ubuntu@ubuntu$ grep -rin CZruIO2cqspVhLuAO9 * | column -t | nl | less -S
#NOTE: The full output is not shown here!. Redo the same actions in the attached VM!
     1	conn.log:43:1561667898.852600   CZruIO2cqspVhLuAO9  10.6.27.102     49162        107.180.50.162      80    tcp  http        
     2	files.log:11:1561667899.060086  FOghls3WpIjKpvXaEl  107.180.50.162  10.6.27.102  CZruIO2cqspVhLuAO9  HTTP  0    EXTRACT,PE  
     3	http.log:11:1561667898.911759   CZruIO2cqspVhLuAO9  10.6.27.102     49162        107.180.50.162      80    1    GET      
```

The `grep` tool helps us investigate the particular value across all available logs. The above terminal output shows us that the connection id linked with `.exe` appears in `conn.log`, `files.log`, and `http.log` files. 

Given example demonstrates how to filter some fields and correlate the findings with the rest of the logs. We've lsited the source and destination addresses, file and connection id numbers, MIME types, and file names. Up to now, provided outputs and findings show that record number three is a `.exe` file, and other log files provide additional information.

### Notice Framework | Intelligence

The *intelligence framework* can work with data feeds to process and correlate events and identify anomalies. The intelligence framework requires a feed to match and creates alerts from the network traffic. Let's demonstrate a single user-generated treat intel file and let Zeek use it as the primary intelligence source.

Intel source location: `/opt/zeek/intel/zeek_intel.txt`

There are two critical points you should never forget. First, the source file has to be tab-delimited. Second, you can manually update the source and adding extra lines doesn't require any re-deployment. However, if you delete a line from the file, you will need to deploy the Zeek instance.

Let's add the suspicious URL gathered from the case1.pcap file as a source intel and see this feature in action. Before executing the script, let's look at the intelligence file and the script contents.

```markdown
ubuntu@ubuntu$ cat /opt/zeek/intel/zeek_intel.txt 
#fields	indicator	indicator_type	meta.source	meta.desc
smart-fax.com	Intel::DOMAIN	zeek-intel-test	Zeek-Intelligence-Framework-Test

ubuntu@ubuntu$ cat intelligence-demo.zeek 
# Load intelligence framework!
@load policy/frameworks/intel/seen
@load policy/frameworks/intel/do_notice
redef Intel::read_files += { "/opt/zeek/intel/zeek_intel.txt" }; 
```

> The above output shows the contents of the intel file and script contents. There is one intelligence input, and it is focused on a domain name, so when this domain name appears in the network traffic, Zeek will create the `intel.log` file and provide the available details. 

```markdown
ubuntu@ubuntu$ zeek -C -r case1.pcap intelligence-demo.zeek 

ubuntu@ubuntu$ cat intel.log | zeek-cut uid id.orig_h id.resp_h seen.indicator matched
CZ1jLe2nHENdGQX377	10.6.27.102	10.6.27.1	smart-fax.com	Intel::DOMAIN	
C044Ot1OxBt8qCk7f2	10.6.27.102	107.180.50.162	smart-fax.com	Intel::DOMAIN 
```

> The above output shows that Zeek detected the listed domain and created the `intel.log` file. This is one of the easiest ways of using the intelligence framework. You can read more on the intelligence framework [here](https://docs.zeek.org/en/master/frameworks/intel.html) and [here](https://docs.zeek.org/en/current/scripts/base/frameworks/intel/main.zeek.html#type-Intel::Type).

**Investigate the case1.pcap file with hash-demo.zeek script. Investigate the files.log file. What is the MD5 hash of the downloaded .exe file?**

**Ans: cc28e40b46237ab6d5282199ef78c464**

zeek -C -r case1.pcap hash-demo.zeek  
cat files.log | head  
cat files.log | zeek-cut mime_type md5

![](https://miro.medium.com/v2/resize:fit:700/1*mcpl4MwJc1Gvli8s6CmsOg.png)

We know that it is an executable file so it should be the third md5 value.

![](https://miro.medium.com/v2/resize:fit:700/1*JyKxsnwfPinCIeryTfWCUg.png)

We can also find the correlation of the “.exe” file with the other log files.

First we need a common value of the “.exe” file.

cat files.log | zeek-cut fuid conn_uids tx_hosts rx_hosts mime_type extracted | nl

![](https://miro.medium.com/v2/resize:fit:700/1*jWP8n0gorUX6OlkqWgjKbg.png)

We will choose the value of the field “conn_uids”.

So we got the “conn_uids” value of the “.exe” file. Now we will extract all values in the current directory that correlates to the “.exe” file.

grep -rin CVsnuagu2ZhLnXy91 * | column -t | nl | less -S

- `grep -rin CVsnuagu2ZhLnXy91 *`: This searches for the pattern "CVsnuagu2ZhLnXy91" recursively (`-r`) in all files (`*`) within the current directory. The `-i` option is used for case-insensitive matching, and the `-n` option displays line numbers.
- `column -t`: This formats the output into multiple columns for better readability. It assumes tabular data with whitespace as the delimiter.
- `nl`: This adds line numbers to the output.
- `less -S`: This command opens the output in the `less` pager, which allows scrolling through the content. The `-S` option disables line wrapping for better readability.

From the result, the “.exe” file is found in three logs. We see other information that relates to the file, and in “files.log” we see its MD5 value.

![](https://miro.medium.com/v2/resize:fit:700/1*RhpxFAefjzLwlUINXwjIMA.png)

**Investigate the case1.pcap file with file-extract-demo.zeek script. Investigate the “extract_files” folder. Review the contents of the text file. What is written in the file?**

**Ans: Microsoft NCSI**

zeek -C -r case1.pcap  file-extract-demo.zeek  
file * | nl  
cat extract-1561667874.743959-HTTP-Fpgan59p6uvNzLFja

![](https://miro.medium.com/v2/resize:fit:700/1*eDrZXSVUVPOPfwzFDNiVhw.png)

# Zeek Scripts | Packages

## Scripts 204 | Package Manager

Zeek Package Manager helps users install third-party scripts and plugins to extend Zeek functionalities with ease. The package manager is installed with Zeek and available with the `zkg` command. Users can install, load, remove, update and create packages with the `zkg` tool. 

We can read more on and view available packages [here](https://packages.zeek.org/) and [here](https://github.com/zeek/packages). Please note that you need root privileges to use the "zkg" tool.  

### Basic Usage of `zkg`

|   |   |
|---|---|
|**Command**|**Description**|
|`zkg install package_path`|Install a package. Example (zkg install zeek/j-gras/zeek-af_packet-plugin).|
|`zkg install git_url`|Install package. Example (zkg install https://github.com/corelight/ztest).|
|`zkg list`|List installed package.|
|`zkg remove`|Remove installed package.|
|`zkg refresh`|Check version updates for installed packages.|
|`zkg upgrade`|Update installed packages.|

> There are multiple ways to use packages. The first approach is using them as frameworks and calling specific package path/directory per usage. The second and most common approach is calling packages from a script with the `@load` method.
> 
> The third and final approach to using packages is calling their package names; note that this method works only for packages installed with the `zkg` install method.

### Packages | Clear Submission of Password

Let's install a package first and then demonstrate the usage in different approaches.

```markdown
ubuntu@ubuntu$ zkg install zeek/cybera/zeek-sniffpass
The following packages will be INSTALLED:
  zeek/cybera/zeek-sniffpass (master)
Proceed? [Y/n] Y
Installing "zeek/cybera/zeek-sniffpass"
Installed "zeek/cybera/zeek-sniffpass" (master)
Loaded "zeek/cybera/zeek-sniffpass"

ubuntu@ubuntu$ zkg list
zeek/cybera/zeek-sniffpass (installed: master) - Sniffpass will alert on cleartext passwords discovered in HTTP POST requests
```

The above output shows how to install and list the installed packages. Now we successfully installed a package. As the description mentions on the above terminal, this package creates alerts for cleartext passwords found in HTTP traffic. 

Let's use this package in three different ways.

```shell
### Calling with script
ubuntu@ubuntu$ zeek -Cr http.pcap sniff-demo.zeek 

### View script contents
ubuntu@ubuntu$ cat sniff-demo.zeek 
@load /opt/zeek/share/zeek/site/zeek-sniffpass

### Calling from path
ubuntu@ubuntu$ zeek -Cr http.pcap /opt/zeek/share/zeek/site/zeek-sniffpass

### Calling with package name
ubuntu@ubuntu$ zeek -Cr http.pcap zeek-sniffpass 
```

The above output demonstrates how to execute/load packages against a pcap. You can use the best one for your case. 

The `zeek-sniffpass` package provides additional information in the notice.log file. Now let's review the logs and discover the obtained data using the specific package.

```markdown
ubuntu@ubuntu$ cat notice.log | zeek-cut id.orig_h id.resp_h proto note msg
10.10.57.178	44.228.249.3	tcp	SNIFFPASS::HTTP_POST_Password_Seen	Password found for user BroZeek
10.10.57.178	44.228.249.3	tcp	SNIFFPASS::HTTP_POST_Password_Seen	Password found for user ZeekBro
```

The above output shows that the package found cleartext password submissions, provided notice, and grabbed the usernames. Remember, in **TASK-5** we created a signature to do the same action. 

Now we can do the same activity without using a signature file. This is a simple demonstration of the benefit and flexibility of the Zeek scripts.

### Packages | Geolocation Data

Let's use another helpful package called `geoip-conn`. This package provides geolocation information for the IP addresses in the conn.log file. It depends on `GeoLite2-City.mmdb` database created by MaxMind.

This package provides location information for only matched IP addresses from the internal database. 

```markdown
ubuntu@ubuntu$ zeek -Cr case1.pcap geoip-conn

ubuntu@ubuntu$ cat conn.log | zeek-cut uid id.orig_h id.resp_h geo.orig.country_code geo.orig.region geo.orig.city geo.orig.latitude geo.orig.longitude geo.resp.country_code geo.resp.region geo.resp.city                                                  
Cbk46G2zXi2i73FOU6	10.6.27.102	23.63.254.163	-	-	-	-	-	US	CA	Los Angeles
```

> Up to now, we've covered what the Zeek packages are and how to use them. There are many more packages and scripts available for Zeek in the wild. You can try ready or third party packages and scripts or learn Zeek scripting language and create new ones.


