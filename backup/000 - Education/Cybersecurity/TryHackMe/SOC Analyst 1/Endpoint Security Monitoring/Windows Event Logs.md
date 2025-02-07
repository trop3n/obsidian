# What are Event Logs?

> Per Wikipedia, "**Event logs** record events taking place in the execution of a system to provide an audit that can be used to understand the activity of the system and to diagnose problems. They are essential to understand the activities of complex systems, particularly in applications with little user interaction (such as server applications)".

This definition would apply to system administrators, IT technicians, desktop engineers, etc. 

- If the endpoint is experiencing and issue, the event logs can be queried to see clues about what led to the problem. 
- The operating system, by default, writes message to these logs. 

As defenders (blue teamers), there is another use case for event logs. "*Combining log file entries from multiple sources can also be useful. This approach, in combination with statistical analysis, may yield correlations between seemingly unrelated events on different servers.*"

This is where SIEMs (**Security Information and Event Management**) such as Splunk and Elastic come into play.

If you don't know exactly what a SIEM is sued for, below is a visual overview of it's capabilities:

> Even though accessing a remote machine's logs is possible, this will not be feasible in a large enterprise environment. Instead, one can view the logs from all the endpoints, appliances, etc. in a SIEM. 

- This will allow you to query the logs from multiple devices instead of manually connecting to a single device to view it's logs. 

Windows is not the only operating system that uses a logging system. Linux and macOS do as well.

- For example, the logging system on Linux systems is known as **Syslog.** In this room though, we're only focusing on the Windows logging system, Windows Event Logs.

# Event Viewer

> The Windows Event Logs are not text files that can be viewed using a text editor. However, the raw data can be translated into XML using the Windows API. The events in these log files are stored in a proprietary binary format with a `.evt` or `evtx` extension. 

- The log files with the `.evtx` extension typically reside in `C:\Windows\System32\winevt\Logs`. 
### Elements of a Windows Event Log

> Event logs are *crucial for troubleshooting any computer incident and help understand the situation and how to remediate the incident.*

To get this picture well, you must first understand the format in which the information will be presented. Windows offers a standardized means of relaying this system information.

First, we need to know what elements form event logs in Windows Systems. These elements are:

- **System Logs**: Records events associated with the Operating System segments. They may include information about hardware changes, device drivers, system changes, and other activities related to the device. 
- **Security Logs**: Records events connected to logon and logoff activities on a device. The system's audit policy specifies the events. The logs are an excellent source for analysts to investigate attempted or successful unauthorized entry. 
- **Application Logs**: Records events related to applications installed on a system. The main pieces of information include application errors, events and warnings.
- **Directory Service Events**: Active Directory changes and activities are recorded in these logs, mainly on domain controllers. 
- **File Replication Service Events**: Records events associated with Windows Servers during the sharing of Group Policies and logon scripts to domain controller, from where they may be accessed by the users through the client servers. 
- **DNS Event Logs**: DNS servers use these logs to record domain events and to map out.
- **Custom Logs**: Events are logged by applications that require custom data storage. This allows applications to control the log size or attach other parameters, such as ACLs, for security purposes.

> Under this categorization, event logs can be further classified into types. Here, types describe the activity that resulted in the event being logged. There are 5 types that can be logged, as described in the table below from [docs.microsoft.com](https://docs.microsoft.com/en-us/windows/win32/eventlog/event-types).

There are three main ways off accessing these event logs on a Windows System:

1. ***Event Viewer*** (GUI-based application)
2. ***Wevtutil.exe*** (command-line tool)
3. ***Get-WinEvent*** (PowerShell cmdlet)
### Event Viewer

> In any Windows system, the Event Viewer, a **Microsoft Management Console (MMC)** snap-in, can be launched by simply right clicking the Windows icon in the taskbar and selecting **Event Viewer**. 

For the savvy sysadmins that use the CLI much of their day, Event Viewer can be launched by typing `eventvwr.msc`. It is a GUI-based application that allows you to interact quickly with and analyze logs.

Event Viewer has three panes:

1. The pane on the left provides a *hierarchical tree listing of the event log providers*
2. The pane in the middle will display a *general overview and summary of the events specific to a selected provider*.
3. The pane on the right is the *actions pane*.

The standard logs we had earlier defined on the left pane are visible under **Windows Logs**.

The following section is the **Applications and Services Logs**. Expand this section and drill down on `Microsoft > Windows > PowerShell > Operational`.

Right-lick on **Operational** then **Properties**

> Within properties, you see the log location, log size and when it was created, modified and last accessed. Within the properties window, you can also see the maximum set log size and what action to take once the criteria are met. 

This concept is known as ***log rotation***.

- These are discussion held with corporations of various sizes. *How long does it take to keep logs, and when it's permissible to overwrite them with new data.* 

Lastly, notice the **Clear Log** button at the bottom right. There are legitimate reasons to use this button, such as during security maintenance, but adversaries will likely attempt to clear the logs to go undetected. 

**Note**: This is not the only method to remove the event logs for any given event provider. 

> Focus your attention on the middle pane. Remember from previous descriptions that this pane will display the event specific to a selected provider. In this case, **PowerShell/Operational**.


From the above image, notice the event provider's name and the number of events logged. In this case there are 44 events logged. You might see a different number. No worries, though. Each column of the pane presents a particular type of information as described below: 

- ***Level***: Highlights the log recorded by type based on the identified event types specified earlier. In this case, the log is labelled as *information*.
- ***Date and Time***: The name of the software that logs the event is identified. From the above image, the source is PowerShell. 
- ***Source***: The name of the software that logs the event is identified. From the above image, the source is PowerShell.
- ***Event ID***: This is a predefined numerical value that maps to a specific operation or event based on the log source. This makes Event IDs not unique, so `Event ID 4103` in the above image is related to Executing Pipeline but will have an entirely different meaning in another event log. 
- ***Task Category***: Highlights the Event Category. This entry will help you organize events so the Event Viewer can filter them. The event source defines this column.

The middle pane has a split view. More information is displayed in the bottom half of the middle pane for any event you click on.

This section has two tabs: **General and Details**.

- General is the default view, and the rendered data is displayed.
- The details view has two options: Friendly view and XML view.

Below is a snipper of the General view:


> Lastly, take a look at the **Actions** pane. Several options are available, but we'll only focus on a few. Please examine all the actions that can be performed at your leisure if you're unfamiliar with MMC snap-ins.

As you should have noticed, you can open a saved log within the Actions pane. This is useful if the remote machine can't be accessed. The logs can be provided to the analyst. You will perform this action a little later. 

> The **Create Custom View** and **Filter Current Log** are nearly identical. The only difference between the 2 is that the `By log` and `By source` radio buttons are greyed out in **Filter Current Log**.

- What is the reason for that? The filter you can make with this specific action only relates to the current log. Hence no reason for 'by log' or 'by source' to be enabled.


Why are these actions beneficial? Say, for instance, you don't want all the events associated with PowerShell/Operational cluttering all the real estate in the pane. Maybe you're interested in 4104 events. That is possible with these two actions.

To view event logs from another computer, right-click `Event Viewer (Local) > Connect to Another Computer...`

# wevtutil.exe 

> Imagine you have to sit and manually sift through hundreds or event thousands of events (even after filtering the log). Not fun. It would be nice if you could write scripts to do this work for you. We will explore some tools that will allow you to query event logs via the command line and/or PowerShell.

Let's look at `wevtutil.exe` first. Per Microsoft, the wevtutil.exe tool "enables you to retrieve information about event logs and publishers. You can use this command to install and uninstall event manifests, to run queries, and to export, archive and clear logs."

As with any tool, access its help files to find out how to run the tool. An example of a command to do this is `wevtutil.exe /?`.

```Powershell
PS> C:\Users\Administrator> wevtutil.exe /?
Windows Events Commandline Utility.
Enables you to retrieve information about event logs and publishers, install and uninstall event manifests, run queries, and export, archive and clear logs.

Usage:

You can use either the short (for example, ep /uni) or long (for example, enum-publishers /unicode) version of the command and option names. Commands, options and option values are not case-sensitive.

Variables are noted in all upper-case.

wevtutil COMMAND [ARGUMENT [ARGUMENT] ...] [/OPTION:VALUE [/OPTION:VALUE] ...]

Commands:

el  | enum-logs              List log names.
gl  | get-log                Get log configuration information.
sl  | set-log                Modify configuration of a log.
ep  | enum-publishers        List event publishers.
gp  | get-publisher          Get publisher configuration information.
im  | install-manifest       Install event publishers and logs from manifest.
um  | uninstall-manifest     Uninstall event publishers and logs from manifest.
qe  | query-events           Query events from a log or log file.
gli | get-log-info           Get log status information.
epl | export-log             Export a log.
al  | archive-log            Archive an exported log.
cl  | clear-log              Clear a log.
```

> From the above screenshot, under **Usage**, you are provided a brief example of how to use the tool. In this example, `ep` (enum-publishers) is used. This is a **command** for wevtutil.exe.

Below, we can find the **Common Options** that can be used with Windows Event Utility.

```Powershell
Common Options:

/{r | remote}:VALUE
If specified, run the command on a remote computer. VALUE is the remote computer name. Options /im and /um do not support remote operations.

/{u |username}:VALUE
Specify a different user to log on to the remote computer. VALUE is a user name in the form of domain\user or user. Only applicable when option /r is specified.

/{p | password}:VALUE
Password for the specified user. If not specified, or if VALUE is "*", the user will be prompted to enter a password. Only applicable when the /u option is specified.

/{a | authentication}:[Default|Negotiate|Kerberos|NTLM]
Authentication type for connecting to remote computer. The default is Negotiate.

/uni | unicode}:[true|false]
Display output in Unicode. If true, then output is in Unicode.

To learn more about a specific command, type the following:

wevtutil COMMAND /?
```

> Notice at the bottom of the above snapshot, `wevtutil COMMAND /?`. This will provide additional information specific to a command. We can use it to get more information on the command `qe` (*query-events*).

```PowerShell
PS> C:\Users\Administrator> wevtutil qe /?
Read events from an event log, log file or using a structured query.

Usage:

wevtutil {qe | query-events}  [/OPTION:VALUE [/OPTION:VALUE]...]
```

# Get-WinEvent

> This is a PowerShell cmdlet called ***Get-WinEvent***. Per Microsoft, the Get-WinEvent cmdlet "gets events from event logs and event tracing log files on local and remote computers."

- It provides information on event logs and event log providers. 
- Additionally, you can combine numerous events from multiple sources into a single command and filter using `XPath` queries, `structured XML queries`, and `hash table` queries.

> **Note**: The **Get-WinEvent** cmdlet replaces the Get-EventLog cmdlet.

As with any new tool, it's good practice to read the Get-Help documentation to become acquainted with its capabilities. Please refer to the Get-Help information online at [docs.microsoft.com](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.diagnostics/get-winevent?view=powershell-5.1).

> Let us look at a couple of examples of how to use `Get-WinEvent`, as supported by the documentation. Some tasks might require some PowerShell-fu, while others don't. Even if your PowerShell-fu is not up to par, fear not; each example has a detailed explanation of the commands cmdlets used.

### Example 1: Get All Logs from a Computer

Here, we are obtaining all event logs locally, and the list starts with classic logs first, followed by new Windows Event logs. It is possible to have a log's **RecordCount** be null or zero.

```PowerShell
Get-WinEvent -ListLog *

LogMode   MaximumSizeInBytes RecordCount LogName
-------   ------------------ ----------- -------
Circular            15532032       14500 Application
Circular             1052672         117 Azure Information Protection
Circular             1052672        3015 CxAudioSvcLog
Circular            20971520             ForwardedEvents
Circular            20971520           0 HardwareEvents
```

- The `Get-WinEvent` cmdlet gets log information from the computer.
- The `ListLog` parameter uses the `*` asterisk wildcard to display information about each log.

### Example 2: Get Event Log Providers and Log Names

> This command gets the event log providers and the logs to which they write.

```Powershell
Get-WinEvent -ListProvider *

Name     : .NET Runtime
LogLinks : {Application}
Opcodes  : {}
Tasks    : {}

Name     : .NET Runtime Optimization Service
LogLinks : {Application}
Opcodes  : {}
Tasks    : {}
```

- The `Get-WinEvent` cmdlet gets log information from the computer.
- The `ListProvider` parameter uses the asterisk `*` wildcard to display information about each provider.
- In the output, the `Name` is the provider and `LogLinks` is the log that the provider writes to.

### Example 3: Log Filtering

> Log filtering allows you to select events from an event log. We can filter event logs using the `Where-Object` cmdlet as follows:

```PowerShell
PS C:\Users\Administrator> Get-WinEvent -LogName Application | Where-Object { $_.ProviderName -Match 'WLMS' }

   ProviderName: WLMS

TimeCreated                     Id LevelDisplayName Message
-----------                     -- ---------------- -------
12/21/2020 4:23:47 AM          100 Information
12/18/2020 3:18:57 PM          100 Information
12/15/2020 8:50:22 AM          100 Information
12/15/2020 8:18:34 AM          100 Information
12/15/2020 7:48:34 AM          100 Information
12/14/2020 6:42:18 PM          100 Information
12/14/2020 6:12:18 PM          100 Information
12/14/2020 5:39:08 PM          100 Information
12/14/2020 5:09:08 PM          100 Information
```

**Tip**: if you are working on a Windows evaluation virtual machine that is cut off from the internet eventually, it will shut down every hour.

When working with large event logs, per Microsoft, it's inefficient to send objects down the pipeline to a `Where-Object` command. 

- The use of the `Get-WinEvent` cmdlet's `FilterHashTable` parameter is recommended to filter event logs. We can achieve the same results as above by running the following command:

```Powershell
Get-WinEvent -FilterHashtable @{
  LogName='Application' 
  ProviderName='WLMS' 
}
```

> The syntax of a hashtable is as follows:

```Powershell
@{ <name> = <value>; [<name> = <value> ] ...}
```

Guidelines for defining a hast table are:

- Begin the hash table with an `@` sign.
- Enclose the hash table is curly braces `{}`
- Enter one or more key-value pairs for the content of the hast table.
- Use an equal sign (`=`) to separate each key from it's value.

**Note:** You don't need to use a semicolon if you separate each key/value with a new line, as in the screenshot above for the `-FilterHashTable` for `ProviderName='WLMS`.

Below is a table that displays the accepted key/value pairs for the Get-WinEvent FilterHashTable parameter.

| Key Name       | Value Data Type | Accepts Wildcard? |
| -------------- | --------------- | ----------------- |
| LogName        | `<String[]>`    | Yes               |
| ProviderName   | `<String[]>`    | Yes               |
| Path           | `<String[]>`    | No                |
| Keywords       | `<Long[]>`      | No                |
| ID             | `<Int32[]>`     | No                |
| Level          | `<Int32[]>`     | No                |
| StartTime      | `<DateTime>`    | No                |
| EndTime        | `<DateTime>`    | No                |
| UserID         | `<SID>`         | No                |
| Data           | `<String[]>`    | No                |
| `<named-data>` | `<String[]>`    | No                |
> When building a query with a hash table, Microsoft recommends making the hash table one key-value pair at a time. 

Event viewer can provide quick information on what you need to build your hash table.


> Based on this information, the hash table will look as follows:


For more information on creating `Get-WinEvent` queries with FilterHastable, check the official Microsoft documentation: [docs.microsoft.com](https://docs.microsoft.com/en-us/powershell/scripting/samples/Creating-Get-WinEvent-queries-with-FilterHashtable?view=powershell-7.1).

Since we're on the topic of Get-WinEvent and FilterHashTable, here is a command that you might find helpful (shared by @mubix):

```Powershell
Get-WinEvent -FilterHashtable @{LogName='Microsoft-Windows-PowerShell/Operational'; ID=4104} | Select-Object -Property Message | Select-String -Pattern 'SecureString'
```

You can read more about creating hash tables in general [docs.microsoft.com](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_hash_tables?view=powershell-7.1).

# XPath Queries

> Now we will examine filtering with ***XPath***. The **W3C** created XPath, or the ***XML Path Language*** in full, to provide a standard syntax and semantics for addressing parts of an XML document and manipulating strings, numbers and booleans. 

The Windows Event Log supports a subset of [XPath 1.0](https://www.w3.org/TR/1999/REC-xpath-19991116/). 

Below is an example XPath query along with it's explanation:

```shell
// The following query selects all events from the channel or log file where the severity level is less than or equal to 3 and the event occurred in the last 24 hour period. 
XPath Query: *[System[(Level <= 3) and TimeCreated[timediff(@SystemTime) <= 86400000]]]
```

Based on [docs.microsoft.com](https://docs.microsoft.com/en-us/windows/win32/wes/consuming-events#xpath-10-limitations), an XPath query starts with `*` or `Event`. The above code block confirms this. 

But how do we construct the rest of the query? Luckily the Event Viewer can help us with that. 

Let's create an XPath query for the same event from the previous section. *Note that both `wevtutil` and `Get-WinEvent` support XPath queries as event filters.* 


> Draw your attention to the bottom half of the middle pane. In the Event Viewer section, the Details tab was briefly touched on. Now you'll see how the information in this bottom half can be useful.

Click on the `Details` tab and select the `XML View` radio button. Don't worry if the log details you are viewing are slightly different. The point is understanding how to use the XML view to construct aa valid XPath query. 


The first tag is the *starting point*. This can either be a `*` or the word `Event`. 

The command so far looks like `Get-WinEvent -LogName Application -FilterXPath '*'`


Now we work our way down the XML tree. The next tag is `System`.

Let's add that. Now our command is: `Get-WinEvent -LogName Application -FilterPath '*/System'`.

**Note**: It is best practice to explicitly use the keyword `System` but you can use an `*` instead as with the `Event` keyword. The query `-FilterXPath '*/*'` is still valid. 

The **Event ID** is **100**. Let's plug that into the command. 


Our command is now `Get-WinEvent -LogName Application -FilterXPath '*/System/EventID=100'`.

```Powershell
PS C:\Users\Administrator> Get-WinEvent -LogName Application -FilterXPath '*/System/EventID=100'

   ProviderName: WLMS

TimeCreated                     Id LevelDisplayName Message
-----------                     -- ---------------- -------
12/21/2020 4:23:47 AM          100 Information
12/18/2020 3:18:57 PM          100 Information
12/15/2020 8:50:22 AM          100 Information
12/15/2020 8:18:34 AM          100 Information
12/15/2020 7:48:34 AM          100 Information
12/14/2020 6:42:18 PM          100 Information
12/14/2020 6:12:18 PM          100 Information
12/14/2020 5:39:08 PM          100 Information
12/14/2020 5:09:08 PM          100 Information
```

> When using `wevtutil.exe` and XPath to query for the same event log and ID, this is our result:

```PowerShell
C:\Users\Administrator>wevtutil.exe qe Application /q:*/System[EventID=100] /f:text /c:1
Event[0]:
  Log Name: Application
  Source: WLMS
  Date: 2020-12-14T17:09:08.940
  Event ID: 100
  Task: None
  Level: Information
  Opcode: Info
  Keyword: Classic
  User: N/A
  User Name: N/A
  Computer: WIN-1O0UJBNP9G7
  Description:
N/A
```

**Note**: 2 additional parameters were used in the above command. This was done to retrieve just one event and for it not to contain any XML tags. 

If you want to query a different element, such as `Provider Name`, the syntax will be different. To filter on the provider, we need to use the `Name` attribute of `Provider`.

```PowerShell
PS C:\Users\Administrator> Get-WinEvent -LogName Application -FilterXPath '*/System/Provider[@Name="WLMS"]'

   ProviderName: WLMS

TimeCreated                     Id LevelDisplayName Message
-----------                     -- ---------------- -------
12/21/2020 4:23:47 AM          100 Information
12/18/2020 3:18:57 PM          100 Information
12/15/2020 8:50:22 AM          100 Information
12/15/2020 8:48:34 AM          101 Information
12/15/2020 8:18:34 AM          100 Information
12/15/2020 7:48:34 AM          100 Information
12/14/2020 7:12:18 PM          101 Information
12/14/2020 6:42:18 PM          100 Information
12/14/2020 6:12:18 PM          100 Information
12/14/2020 6:09:09 PM          101 Information
12/14/2020 5:39:08 PM          100 Information
12/14/2020 5:09:08 PM          100 Information
```

> What if you combine two queries? Is that even possible? 
> The answer is Yes.

Let's build this query based on the screenshot above. The Provider Name is `WLMS`, and based on the output, there are **2 Event IDs**. 

This time we only want to query for events with **Event ID 101**.

The XPath query would be `Get-WinEvent -LogName Application -FilterXPath '*/System/EventID=101 and */System/Provider[@Name="WLMS"]'`

```PowerShell
PS C:\Users\Administrator> Get-WinEvent -LogName Application -FilterXPath '*/System/Provider[@Name="WLMS"]'

   ProviderName: WLMS

TimeCreated                     Id LevelDisplayName Message
-----------                     -- ---------------- -------
12/15/2020 8:48:34 AM          101 Information
12/14/2020 7:12:18 PM          101 Information
12/14/2020 6:09:09 PM          101 Information
```

> Lastly, let's discuss how to create XPath queries for elements within `EventData`. The query will be slightly different. 

**Note**: The EventData element doesn't always contain information.

Below is the XML View of the event for which we will build our XPath Query.


> We will build the query for `TargetUserName`. In this case, that will be System. The XPath query would be `Get-WinEvent -LogName Security -FilterXPath '*/EventData/Data[@Name="TargetUserName']="System"'`

```PowerShell
PS C:\Users\Administrator> Get-WinEvent -LogName Security -FilterXPath '*/EventData/Data[@Name="TargetUserName"]="System"' -MaxEvents 1

   ProviderName: Microsoft-Windows-Security-Auditing

TimeCreated                     Id LevelDisplayName Message
-----------                     -- ---------------- -------
12/21/2020 10:50:26 AM         4624 Information     An account was successfully logged on...
```

**Note**: The `-MaxEvents` parameter was used, and it was set to 1. This will return just 1 event.

At this point, you have enough knowledge to create XPath queries for **wevtutil.exe** or **Get-WinEvent**. To further this knowledge, I suggest reading the official Microsoft XPath Reference [docs.microsoft.com](https://docs.microsoft.com/en-us/previous-versions/dotnet/netframework-4.0/ms256115(v=vs.100)).

### Questions

1. Using the knowledge gained on **Get-WinEvent** and **XPath**, what is the query to find **WLMS** events with a System Time of **2020-12-15T01:09:08.940277500Z**?

We know how to filter by WLMS provider events by just looking at this example. For Time/Date let's look check the XML View of an event.


This is the field we want to capture, so let's craft our query like so:

```PowerShell
*/System/TimeCreated[@SystemTime="2020-12-15T01:09:08.940277500Z
```

> **Answer:** Get-WinEvent -LogName Application -FilterXPath ‘*/System/Provider[@Name=”WLMS”] and */System/TimeCreated[@SystemTime=”2020–12–15T01:09:08.940277500Z”]’

2. Using **Get-WinEvent** and **XPath**, what is the query to find a user named Sam with an Logon Event ID of 4720?

This one is kind of a doozy but luckily, the syntax to filter by username is provided in the task:

So put that together with the eventid filter and we get…

> **Answer:** Get-WinEvent -LogName Security -FilterXPath ‘*/EventData/Data[@Name=”TargetUserName”]=”Sam” and */System/EventID=”4720"’

3. Based on the previous query, how many results are returned?

```PowerShell
PS C:\Users\Administrator> Get-WinEvent -Logname Security -FilterXPath '*/EventData/Data[@Name="TargetUserName"]="Sam" and */System/EventID="4720"'


   ProviderName: Microsoft-Windows-Security-Auditing

TimeCreated                     Id LevelDisplayName Message
-----------                     -- ---------------- -------
12/17/2020 1:57:14 PM         4720 Information      A user account was created....
12/17/2020 1:56:58 PM         4720 Information      A user account was created....
```

> **Answer**: 2

4. Based on the output from question #2, what is Message?

> **Answer**: A user account was created

5. Still working with Sam as the user, what time was Event ID 4724 recorded?

We can simply add the query to find that particular event ID to the end of the previous query.

```PowerShell
PS C:\Users\Administrator> Get-WinEvent -LogName Security -FilterXPath '*/EventData/Data[@Name="TargetUserName"]="Sam" and */System/EventID="4724"'


   ProviderName: Microsoft-Windows-Security-Auditing

TimeCreated                     Id LevelDisplayName Message
-----------                     -- ---------------- -------
12/17/2020 1:57:14 PM         4724 Information      An attempt was made to reset an account's password....
```

> **Answer**: 12/17/2020 1:57:14 PM

6. What is the Provider Name?

This can be found from looking at the output of the previous query:

> **Answer**: Microsoft-Windows-Security-Auditing

# Event IDs

> When it comes to monitoring and hunting, you need to know what you are looking for. There are a large number of event IDs in use. This section is aimed at assisting you with this task. There are plenty of blogs, writeups etc. on this topic. 

A few resources will be shared in this section. Please note this is not an exhaustive list.

First on the list is [The Windows Logging Cheat Sheet (Windows 7 - Windows 2012)](https://static1.squarespace.com/static/552092d5e4b0661088167e5c/t/580595db9f745688bc7477f6/1476761074992/Windows+Logging+Cheat+Sheet_ver_Oct_2016.pdf). The last version update is October 2016, but it's still a good resource. The document covers a few things that need to be enabled and configured and what event IDs to look for based on different categories, such as Accounts, Processes, Log Clear, etc.


Above is a snippet from the cheatsheet. Want to detect if a new service was installed? Look for **Event ID 7045** within the **System Log**. 

> Next is [Spotting the Adversary with Windows Event Log Monitoring](https://web.archive.org/web/20190115215749/https://apps.nsa.gov/iaarchive/customcf/openAttachment.cfm?FilePath=/iad/library/ia-guidance/security-configuration/applications/assets/public/upload/Spotting-the-Adversary-with-Windows-Event-Log-Monitoring.pdf&WpKes=aF6woL7fQp3dJiqyJL2LenrLxuHC7ztGtVNK3x). This NSA resource is also a bit outdated but good enough to build upon your foundation. The document covers some concepts touched on in this room and beyond. You must click on `Get File` to download the resource.


> Above is a snippet from the document. Maybe you want to monitor if a firewall rule was deleted from the host. That is **Event ID 2066/2033**. 

Where else can we get a list of Event IDs to monitor/hunt for? [MITRE ATT&CK](https://attack.mitre.org/)!

Let's look for ATT&CK ID [T1098](https://attack.mitre.org/techniques/T1098/) (Account Manipulation). Each ATT&CK ID will contain a section sharing tips to mitigate the technique and detection tips.


The last two resources are from Microsoft. 

- [Events to Monitor](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/plan/appendix-l--events-to-monitor) (Best Practices for Securing Active Directory)
- [The Windows 10 and Windows Server 2016 Security Auditing and Monitoring Reference](https://www.microsoft.com/en-us/download/confirmation.aspx?id=52630) (a comprehensive list [**over 700 pages**])

**Note**: Some events will not be generated by default, and certain features will need to be enabled/configured on the endpoint, such as PowerShell logging. This feature can be enabled via the **Group Policy** or the **Registry**.

`Local Computer Policy > Computer Configuration > Administrative Templates > Windows Components > Windows PowerShell`. 


Some resources to provide more information about enabling this feature, along with its associated event IDs:

- [About Logging Windows](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_logging_windows?view=powershell-7.1)
- [Greater Visibility Through PowerShell Logging](https://www.fireeye.com/blog/threat-research/2016/02/greater_visibilityt.html)
- [Configure PowerShell logging to see PowerShell anomalies in Splunk UBA](https://docs.splunk.com/Documentation/UBA/5.0.4/GetDataIn/AddPowerShell)


> Another feature to enable/configure is ***Audit Process Creation***, which will generate **event ID 4688**. This will allow **command-line process auditing**. This setting is NOT enabled in the virtual machine but feel free to enable it and observe the events generated after executing some commands. 

`Local Computer Policy > Computer Configuration > Administrative Templates > System > Audit Process Creation`


out this feature, refer to [docs.microsoft.com](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/manage/component-updates/command-line-process-auditing#try-this-explore-command-line-process-auditing). The steps to test the configuration are at the bottom of the document.



> To conclude this section, it will be reiterated that this is not an exhaustive list. There are countless blogs, writeups, threat intel reports, etc. on this topic. 

To effectively monitor and detect, you need to know what to look for (as mentioned earlier).

# Putting Theory Into Practice

> Scenario 1 (Questions 1 & 2): The server admins have made numerous complaints to Management regarding PowerShell being blocked in the environment. Management finally approved the usage of PowerShell within the environment. Visibility is now needed to ensure there are no gaps in coverage. You researched this topic: what logs to look at, what event IDs to monitor, etc. You enabled PowerShell logging on a test machine and had a colleague execute various commands.

From MITRE ATT&CK: Adversaries may downgrade or use a version of system features that may be outdated, vulnerable, and/or does not support updated security controls. Downgrade attacks take advantage of a system's *backwards compatibility* to force it into less secure modes of operation.

Adversaries may downgrade and use various less-secure versions of features of a system, such as [Command and Scripting Interpreter](https://attack.mitre.org/techniques/T1059)s or even network protocols that can be abused to enable [Adversary-in-the-Middle](https://attack.mitre.org/techniques/T1557) or [Network Sniffing](https://attack.mitre.org/techniques/T1040). For example, PowerShell versions 5+ includes Script Block Logging (SBL) which can record executed script content. However, adversaries may attempt to execute a previous version of PowerShell that does not support SBL with the intent to [Impair Defenses](https://attack.mitre.org/techniques/T1562) while running malicious scripts that may have otherwise been detected.(https://www.crowdstrike.com/blog/how-falcon-complete-stopped-a-big-game-hunting-ransomware-attack/)(https://www.mandiant.com/resources/bring-your-own-land-novel-red-teaming-technique)(https://nsfocusglobal.com/attack-and-defense-around-powershell-event-logging/) 

> Scenario 2 (Questions 3 & 4): The Security Team is using Event Logs more. They want to ensure they can monitor if event logs are cleared. You assigned a colleague to execute this action.

> Scenario 3 (Questions 5, 6 & 7): The threat intel team shared its research on **Emotet**. They advised searching for event ID 4104 and the text "ScriptBlockText" within the EventData element. Find the encoded PowerShell payload.

> Scenario 4 (Questions 8 & 9): A report came in that an intern was suspected of running unusual commands on her machine, such as enumerating members of the Administrators group. A senior analyst suggested searching for "`C:\Windows\System32\net1.exe`". Confirm the suspicion.

### Conclusion

In this room, we covered Windows Event Logs, what they are, and how to query them using various tools and techniques. 

We also briefly discussed various features within Windows that you need to enable/configure to log additional events to gain visibility into those processes/features that are turned off by default. 

The information covered in this room will serve as a primer for other rooms covering [Windows Internals](https://tryhackme.com/jr/windowsinternals), [Sysmon](https://tryhackme.com/jr/sysmon), and various [SIEM](https://tryhackme.com/jr/splunk101) tools.

I'll end this room by providing additional reading material:

- [EVTX Attack Samples](https://github.com/sbousseaden/EVTX-ATTACK-SAMPLES) (a few were used in this room)
- [PowerShell <3 the Blue Team](https://devblogs.microsoft.com/powershell/powershell-the-blue-team/)
- [Tampering with Windows Event Tracing: Background, Offense, and Defense](https://medium.com/palantir/tampering-with-windows-event-tracing-background-offense-and-defense-4be7ac62ac63)