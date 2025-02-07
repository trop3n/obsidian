***Sysmon***, a tool used to monitor and log events on Windows, is commonly used by enterprises as part of their monitoring and logging solutions. Part of the Windows Sysinternals package, Sysmon is similar to Windows Event Logs with further detail and granular control.

This room uses a modified version of the [Blue](https://tryhackme.com/room/blue) and [Ice](https://tryhackme.com/room/ice) boxes, as well as Sysmon logs from the Hololive network lab.

# Sysmon Overview

> From the Microsoft Docs, "System Monitor (Sysmon)" is a Windows system service and device driver that, once installed on a system, remains resident across system reboots to monitor and log system activity to the Windows Event Log. 
> 
> It provides detailed information about process creations, network connections, and changes to file creation time. By collecting the events it generates using Windows Events Collection or SIEM agents and subsequently analyzing them, you can identify malicious or anomalous activity and understand how intruders and malware operate on your network.

Sysmon gathers detailed an high-quality logs as well as event tracing that assists in identifying anomalies in your environment. Sysmon is most commonly used in conjunction with security information and event management (SIEM) system or other log parsing solutions that aggregate, filter and visualize events. When installed on an endpoint, Sysmon will start early in the Windows boot process. 

In an ideal scenario, the events would be forwarded to a SIEM for further analysis. However, in this room, we will focus on Sysmon itself and view the events on the endpoint itself with Windows Event Viewer. 

Events in Sysmon are stored in `Applications and Services Logs/Microsoft/Windows/Sysmon/Operational`.

### Sysmon Config Overview

> Sysmon requires a config file in order to tell the binary how to analyze the events that it is receiving. You can create your own Sysmon config or you can download a config. Here is an example of a high-quality config that works well for identifying anomalies created by SwiftOnSecurity: [Sysmon-Config.](https://github.com/SwiftOnSecurity/sysmon-config)

Sysmon includes 29 different types of Event IDs, all of which can be used within the config to specify how the events should be handled and analyzed. Below we will go over a few of the most important Event IDs and show examples of how they are used within config files.

When creating or modifying configuration files you will notice that a majority of rules in sysmon-config will *exclude events rather than include events.*

This will help filter out normal activity in your environment that will in turn decrease the number of events and alerts you will have to manually audit or search through in a SIEM. On the other hand, there are rulesets like the ION-Storm sysmon config fork that takes a more proactive approach with it's ruleset by using a lot of include rules. 

You may have to modify configuration files to find out what approach you prefer. Configuration preferences will vary depending on what the SOC team wants to prepare to be flexible when monitoring. 

*Note*: as there are so many Event IDs Sysmon analyzes, we will only be going over a few of the ones that we think are most important to understand.

### Event ID 1: Process Creation

> This event will look for any processes that have been created. You can use this to look for known suspicious processes or processes with types that would be considered an anomaly. This event will use the Command Line and Image XML tags.

```
<RuleGroup name="" groupRelation="or">
	<ProcessCreate onmatch="exclude">
		<CommandLine condition="is">C:\Windows\system32\svchost.exe -k appmodel -p -s camsvc</CommandLine>
	</ProcessCreate>
</RuleGroup>
```
> The above code snippet is specifying the Event ID to pull from as well as what condition to look for. In this case, it is excluding the svchost.exe process from the event logs.

### Event ID 3: Network Connection

The network connection event will look for events that occur remotely. This will include files and sources of suspicious binaries as well as opened ports. This event will use the Image and DestinationPort XML tags.

```
<RuleGroup name="" groupRelation="or">
	<NetworkConnect onmatch="include">
		<Image condition="image">nmap.exe</Image>
					<DestinationPort name="Alert,Metasploit" condition="is">4444</DestinationPort>
</NetworkConnect>   
</RuleGroup>
```

The above code snippet includes two ways to identify suspicious activity.

The first way:

- Identifies files transmitted over open ports. In this case, we are specifically looking for nmap.exe which will then be reflected within the event logs. 

The second method:


# Malicious Activity Overview

Since most of the normal activity or "noise" seen on a network is excluded or filtered out with Sysmon we're able to focus on meaningful events. This allows us to quickly identify and investigate suspicious activity. When actively monitoring a network you will want to use multiple detections and techniques simultaneously in an effort to identify threats. 

For this room, we will only be looking at what suspicious logs will look like with both Sysmon configs and how to optimize *using only Sysmon*. We will be looking at how to detect ransomware, persistence, Mimikatz, Metasploit, and Command and Control (C2) beacons. Obviously, this is only showcasing a small handful of events that could be triggered in an environment. The methodology will largely be the same for other threats. It really comes down to using an ample and efficient configuration file as it can do a lot of the heavy lifting for us. 

## Sysmon "Best Practices"

Sysmon offers a fairly open and configurable platform for us to use. Generally speaking, there are a few best practices that we can implement to ensure we're operating efficiently and not missing any potential threats. A few common best practices are outlined and explained below:

- **Exclude -> Include**

	- When creating rules for your Sysmon configuration file it is typically best to prioritize excluding events rather than including events. This prevents you from accidentally missing *crucial events* that matter the most.

- **CLI gives further control**

	- As is common with most applications the CLI gives us the most control and filtering allowing for further granular control. You can use either `Get-WinEvent` or `wevutil.exe` to access and filter logs. You can incorporate Sysmon in your SIEM or other detection solutions these tools will become less used and needed.

- **Know your environment before implementation**

	- Knowing your environment is important *when implementing any platform or tool.* You should have a firm understanding of the network or environment you are working within to fully understand what is normal and what is suspicious in order to effectively craft our rules.

## Filtering Files with Event Viewer

Event Viewer might not be the best for filtering events and out of the box offers limited control over logs. The main filter you will be using with Event Viewer is by filtering the `EventID` and keywords. You can also choose to filter by writing XML but this is a tedious process that **doesn't scale well**.

To open the filter menu select `Filter Current Log` from the Actions menu.

![](https://i.imgur.com/wBPUGNM.png)

If you have successfully opened the filter menu it should look like the menu below/

![](https://i.imgur.com/cA2Bcgv.png)

From this menu, we can add any filters or categories we want.

## Filtering Events with PowerShell

To view and filter events with PowerShell we will be using `Get-WinEvent` along with `XPath` queries. We can use any XPath queries that can be found in the XML view of events. We will be using `wevutil.exe` to view events once filtered. The command line is typically used over the Event Viewer GUI as it allows for further granular control and filtering whereas the GUI does not. For more information about using `Get-WinEvent` and `wevutil.exe` check out the [Windows Event Log](https://tryhackme.com/room/windowseventlogs) room.

For this room, we will only be going over a few basic filters as the Windows Event Log room already extensively covers this topic. 

- **Filter By Event ID**: `*/System/EventID=<ID>`

- **Filter By XML Attribute/Name**: `*/EventData/Data[@Name="<XML Attribute/Name>"]`

- **Filter by Event Data**: `*/EventData/Data=<Data>`

We can put these filters together with various attributes and data to get the most control out of our logs. Look below for an example of using `Get-WinEvent` to look for network connections coming from port 4444.

`Get-WinEvent -Path <Path to Log> -FilterXPath '*/System/EventID=3 and */EventData/Data[@Name="DestinationPort"] and */EventData/Data=4444'`

# Hunting Metasploit

Metasploit is a commonly used exploit framework for penetration testing and red team operations. Metasploit can be used to easily run exploits on a machine and connect back to a meterpreter shell. We will be hunting the meterpreter shell itself and the functionality it uses. 

To begin hunting we will look for network connections that originate from suspicious ports such as `4444` and `5555`. By default, Metasploit uses port 4444. If there is a connection to any IP known or unknown it should be investigated. To start an investigation you can look at packet captures from the data of the log to begin looking for further information about the adversary. We can also look for further information about the adversary. We can also look for suspicious processes created. This method of hunting can be applied to other various RAT and C2 beacons. 

For more information about this technique and tools used check out [MITRE ATT&CK Software](https://attack.mitre.org/software/).

For more information about how malware and payloads interact with the network check out the [Malware Common Ports Spreadsheet](https://docs.google.com/spreadsheets/d/17pSTDNpa0sf6pHeRhusvWG6rThciE8CsXTSlDUAZDyo). This will be covered in further depth in the Hunting Malware task.

You can download the event logs used in this room from this task or you can open them in the Practice folder on the provided machine.

## Hunting Network Connections

We will first be looking at a modified Ion-Security configuration to detect the creation of new network connections. The code snippet below will use event ID 3 along with the destination port to identify active connections specifically connections on port `4444` and `5555`. 

```XML
<RuleGroup name="" groupRelation="or">
	<NetworkConnect onmatch="include">
		<DestinationPort condition="is">4444</DestinationPort>
		<DestinationPort condition="is">5555</DestinationPort>
	</NetworkConnect>
</RuleGroup>
```

Open `C:\Users\THM-Analyst\Desktop\Scenarios\Practice\Hunting_Metasploit.evtx` in Event Viewer to view a basic Metasploit payload being dropped onto the machine.

