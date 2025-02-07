> In this room, we will introduce the fundamentals of endpoint security monitoring, essential tools, and high-level methodology.
> 
> This room gives an overview of determining a malicious activity from an endpoint and mapping it's related events.

To start with, we will take the following topics to build a stepping stone on how to deal with Endpoint Security Monitoring.

- Endpoint Security Fundamentals
- Endpoint Logging and Analysis
- Endpoint Log Analysis

At the end of this room, we will have a threat simulation wherein you need to investigate and remediate the infected machines. 

### Endpoint Security Fundamentals

> Before we deal with learning how to deep-dive into endpoint logs, we need first to learn the fundamentals of how the Windows OS works.

- Without prior knowledge, differentiating an outlier from a haystack of events could be problematic.

To learn more about Core Windows Processes, a built-in Windows tool called **Task Manager** may aid us in understanding the underlying processes inside a Windows machine.

**Task Manager** is a built-in GUI-based Windows utility that allows users to *see what is running on the Windows System*. 

- It also provides information on resource usage, such as how much each process utilizes CPU and Memory. 
- When a program is not responding, the Task Manager can be used to terminate the process.

Task Manager provides some of the core processes that are running in the background. Below is a summary of running processes that are considered *normal behavior*:

- `System`
- `System > smss.exe`
- `csrss.exe`
- `wininit.exe`
- `wininit.exe > services.exe`
- `wininit.exe > services.exe > svchost.exe`
- `lsass.exe`
- `winlogon.exe`
- `explorer.exe`

In addition, the processes with no depiction of a parent-child relationship should not have a Parent Process under normal circumstances, except for the system process, which should only have **System Idle Process (0)** as it's parent process.

You may refer to the [Core Windows Processes Room](https://tryhackme.com/room/btwindowsinternals) to learn more about this topic. 
### Sysinternals

With the prior knowledge of Core Windows Processes, we can ow proceed to discuss the available toolset for analyzing running artefacts in the backend of a Windows machine.

The **sysinternals** tools are a compilation of over 70+ WIndows-based tool. Each of these tools falls into one of the following categories:

- *File and Disk Utilities*
- *Networking Utilities*
- *Process Utilites*
- *Security Utilities*
- *System Information*
- *Miscellaneous*

We will introduce two of the most used Sysinternals tools for endpoint investigation for this task:

- **TCPView** - Network Utility tool.
- **Process Explorer** - Process Utility tool. 
### TCPView

**TCPView** is a Windows program that will show you detailed listings of TCP and UDP endpoints on your system, including the local and remote addresses and state of TCP connections. On Windows Server 2008, Vista and XP, TCPView also reports the name and process that owns the endpoint. TCPView provides a more informative and conveniently presented subset of the Netstat program that ships with Windows. 

- TCPView download includes TCPvcon, a command-line version with the same functionality.

> As shown above, every connection initiated by a process is listed by the tool, which may aid in correlating the network events executed concurrently. 
### Process Explorer

**Process Explorer** display consists of two-sub windows. The top window always shows a list of the currently active processes, including the names of their owning accounts, whereas the information displayed in the bottom window depends on the mode that process explorer is in: if it is in handle mode, you'll see the handles that the process selected in the top window has opened; if process explorer is in DLL mode you'll see the DLLs and memory-mapped files that the process had loaded. 

Process Explorer enables you to inspect the details of a running process such as:

- Associated services
- Invoked network traffic
- Handles such as files or directories
- Handles such as files or directories opened
- DLLs and memory-mapped files loaded 
# Endpoint Logging and Monitoring

> From the previous task, we have learned basic knowledge about the Windows Operating system in terms of baseline processes and essential tools to analyze events and artefacts running on the machine. However, this only limits us from observing real-time events. With this, we will introduce the importance of **endpoint-logging**, which enables us to audit significant events across different endpoints, collect and aggregate them for searching capabilities, and better automate the detection of anomalies. 
### Windows Event Logs

> The **Windows Event Logs** are not text files that can be viewed using a text editor. However, the raw data can be translated into `XML` using the Windows API. 

The events in these log files are stored in a proprietary binary format with a `.evt` or `.evtx` extension.

The log files with the `.evtx` extension typically reside in `C:\Windows\System32\winevt\Logs`

There are three main ways of accessing these event logs within a Windows System:
- **Event Viewer** (GUI-based application)
- **Wevtutil.exe** (command-line tool)
- **Get-WinEvent** (PowerShell cmdlet)

An example image of logs viewed using the event viewer is shown below: 

 > The [Windows Event Logs Room](https://tryhackme.com/room/windowseventlogs)  can be referred to to learn more about Windows Event Logs.
### Sysmon

> **Sysmon** refers to System Monitor, which is a Windows system service and device driver developed by Microsoft that is designed to monitor and log various events happening within a Windows system.

Sysmon is a tool used to monitor and log events in Windows, is commonly used by enterprises as part of their monitoring and logging solutions. As part of the Windows Sysinternals package, Sysmon is similar to Windows Event Logs with further detail and granular control. 

Sysmon gathers detailed information and high-quality logs as well as event tracing that assists in identifying anomalies in your environment. It is commonly used with a *security information and event management (SIEM)* system or other log parsing solution that aggregates, filters and visualizes events.

Lastly, Sysmon includes 27 types of Event IDs, all of which can be used within the required configuraion file to specify how the events should be handled and analyzed. 

- An excellent example of a configuration file auditing different Event IDs created by SwiftOnSecurity is linked [here](https://github.com/SwiftOnSecurity/sysmon-config).

To learn more about Sysmon, you may refer to the [Sysmon Room](https://tryhackme.com/room/sysmon).
### OSQuery

**OSQuery** is an open-source tool created by Facebook. With Osquery, Security Analysts, Incident Responders, and Threat Hunters can query an endpoint (or multiple endpoints) using SQL syntax. 

OSQuery can be installed on various platforms, Windows, Linux, macOS and FreeBSD.

To interact with Osquery interactive/console shell, open CMD (or PowerShell), and run `osqueryi`. You'll know that you've successfully entered into the interactive shell by the new command prompt. 

```shell
C:\Users\Administrator\> osqueryi
Using a virtual database. Need help, type 'help'
osquery> 
```

A sample use case for using OSQuery is to list important process information by its process name. 

```shell
osquery> select pid,name,path from processes where name='lsass.exe';
+-----+-----------+-------------------------------+
| pid | name      | path                          |
+-----+-----------+-------------------------------+
| 748 | lsass.exe | C:\Windows\System32\lsass.exe |
+-----+-----------+-------------------------------+
osquery> 
```

> OSQuery only allows you to query events inside the machine. But with Kolide Fleet, you can query multiple endpoints from the Kolide Fleet UI instead of using Osquery locally to query an endpoint. 

A sample of Kolide Fleet in action below shows a result of a query listing with the `lsass` process running. 

﻿To learn more about OSQuery, you may refer to the [OSQuery Room](https://tryhackme.com/room/osqueryf8).
### Wazuh

> Wazuh is an open-source, freely available and extensive EDR solution, which Security Engineers can deploy in all scales of environments. 

Wazuh operates on a management and agent model where a dedicated manager device is responsible for managing agents installed on the devices you'd like to monitor. 

As mentioned, Wazuh is an EDR: **Endpoint Detection and Response** are tools and applications that monitor devices for any activity that could indicate a threat or security breach. These tools and applications have features that include:

- Auditing a device for common vulnerabilities
- Proactively monitoring a device for suspicious activity such as unauthorized logins, brute-force attacks, or privilege escalations.
- Visualizing complex data and events into neat and trendy graphs.
- Recording a device's normal operating behavior to help with detecting anomalies
# Endpoint Log Analysis

> Event correlation identifies significant relationships from multiple log sources such as application logs, endpoint logs, and network logs. 

Event correlation deals with identifying significant artefacts co-existing from different log sources and connecting each related artefact. 

- For example, a network connection log may exist in various log sources such as Sysmon logs (Event ID 3: Network Connection) and Firewall Logs. 
- The Firewall log may provide the source and destination IP, source and destination port, protocol and the action taken. 
	- In contrast, Sysmon logs may give the process that invoked the network connection and the user running the process. 

With this information, we can connect the dots of each artefact from the two data sources:

- *Source and Destination IP*
- *Source and Destination Port*
- *Action Taken*
- *Protocol*
- *Process Name*
- *User Account*
- *Machine Name*

Event correlation can build the puzzle pieces to complete the exact scenario from an investigation.
### Baselining

> **Baselining** is the process of knowing what is expected to be normal. In terms of endpoint security monitoring, it requires a vast amount of data gathering to establish the standard behavior of user activities, network traffic across infrastructure, and process running on all machines owned by the organization.

Using the baseline as a reference, we can quickly determine the outliers that could threaten the organization. 

Below is a sample list of baseline and unusual activities to show the importance of knowing what to expect in your network. 

| Baseline                                                                                                                              | Unusual Activity                                                                         |
| ------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| The organization's employees are in London, and the regular working hours are between 9AM and 6PM.                                    | A user has authenticated via VPN connecting from Singapore at 3AM.                       |
| A single workstation is assigned to each employee.                                                                                    | A user has attempted to authenticate multiple workstations.                              |
| Employees can only access selected websites on their workstations, such as OneDrive, SharePoint, and other 0365 applications.         | A user has uploaded a 3GB file on Google Drive.                                          |
| Only selected applications are installed on workstations, mainly Microsoft Applications such as Word, Excel, Teams and Google Chrome. | A process named firefox.exe has been observed running on multiple employee workstations. |
Any event could be a needle in a haystack without a good overview of regular activity. 
### Investigation Activity

> We have tackled the foundations of Endpoint Security Monitoring from previous tasks. Now, we will wear our Blue Team hat and apply the concepts we discussed by investigating a suspicious activity detected on a workstation owned by one of your colleages. 

# Task Manager 



