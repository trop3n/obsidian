#DFIR #endpointmonitoring #tryhackme #soclevel1 

# Velociraptor

In this room, we will explore Rapid7's newly acquired tool known as [Velociraptor](https://www.rapid7.com/blog/post/2021/04/21/rapid7-and-velociraptor-join-forces/). 

Per the official Velociraptor [documentation](https://docs.velociraptor.app/docs/overview/), "_Velociraptor is a unique, advanced open-source endpoint monitoring, digital forensic and cyber response platform._ _It was developed by Digital Forensic and Incident Response (DFIR) professionals who needed a powerful and efficient way to hunt for specific artifacts and monitor activities across fleets of endpoints. Velociraptor provides you with the ability to more effectively respond to a wide range of digital forensic and cyber incident response investigations and data breaches_".

This tool was created by Mike Cohen, a former Google employee who worked on tools such as [GRR](https://github.com/google/grr) (GRR Rapid Response) and [Rekall](https://github.com/google/rekall) (Rekall Memory Forensic Framework). Mike joined Rapid7's Detection and Response Team and continues to work on improving Velociraptor. At the date of this entry, the latest release for Velociraptor is [0.6.3](https://www.rapid7.com/blog/post/2022/02/03/velociraptor-version-0-6-3-dig-deeper-with-more-speed-and-scalability/).

**Learning Objectives**

- Learn what is Velociraptor
- Learn how to interact with agents and create collections
- Learn how to interact with the virtual file system
- Learn what is VQL and how to create basic queries
- Use Velociraptor to perform a basic hunt

**Prerequisites**

- [Windows Forensics 1](https://tryhackme.com/room/windowsforensics1)
- [Windows Forensics 2](https://tryhackme.com/room/windowsforensics2)
- [KAPE](https://tryhackme.com/room/kape)

# Deploying Velociraptor

Velociraptor is unique because the Velociraptor executable can act as a **server** or a **client** and it can run on **Windows, Linux or MacOS**. Velociraptor is also compatible with cloud file systems, such as **Amazon EFS** and **Google Filestore**. 

Velociraptor can be deployed across thousands, even tens of thousands, client endpoints and runs surprisingly well for an open-source product. 

In this task, we will **NOT** go into detail about how to deploy Velociraptor as a server and agent architecture in an environment. Rather, in the attached VM, you will run the commands to start the first Velociraptor executable as a server and execute a second Velociraptor executable to run as an agent. 

This is possible thanks to WSL ([Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/about)). This will simulate Velociraptor running as a server in Linux (Ubuntu) and as a client running Windows. WSL (Windows Subsystem For Linux) allows to run a Linux environment in a Windows machine without the need for a virtual machine. 

Let's start Velociraptor as a server. If you haven't done so, deploy the attached virtual machine. 

After fully loading, the virtual machine will appear in split view in your web browser. If you don't see the VM, click **Show Split View**.

![](https://i.imgur.com/FOYg5cq.png)

There is a text file on the desktop called commands.txt. Open the Ubuntu terminal and run the command for `Start the Velociraptor Server (Ubuntu Terminal)`and **proceed to follow the instructions listed in command.txt.**

Below is an example of the terminal input and output.

```shell-session
[INFO] 2024-05-26T11:44:45Z  _    __     __           _                  __
[INFO] 2024-05-26T11:44:45Z | |  / /__  / /___  _____(_)________ _____  / /_____  _____
[INFO] 2024-05-26T11:44:45Z | | / / _ \/ / __ \/ ___/ / ___/ __ `/ __ \/ __/ __ \/ ___/
[INFO] 2024-05-26T11:44:45Z | |/ /  __/ / /_/ / /__/ / /  / /_/ / /_/ / /_/ /_/ / /
[INFO] 2024-05-26T11:44:45Z |___/\___/_/\____/\___/_/_/   \__,_/ .___/\__/\____/_/
[INFO] 2024-05-26T11:44:45Z                                   /_/
[INFO] 2024-05-26T11:44:45Z Digging deeper!                  https://www.velocidex.com
[INFO] 2024-05-26T11:44:45Z This is Velociraptor 0.5.8 built on 2021-04-11T22:09:54Z (e468f54c)
[INFO] 2024-05-26T11:44:45Z Loading config from file server.config.yaml
[INFO] 2024-05-26T11:44:45Z Starting Frontend. {"build_time":"2021-04-11T22:09:54Z","commit":"e468f54c","version":"0.5.8"}
[INFO] 2024-05-26T11:44:45Z Error increasing limit invalid argument. This might work better as root.
[INFO] 2024-05-26T11:44:45Z Starting Journal service.
[INFO] 2024-05-26T11:44:45Z Starting the notification service.
[INFO] 2024-05-26T11:44:45Z Starting Inventory Service
[INFO] 2024-05-26T11:44:45Z Loaded 250 built in artifacts in 88.9704ms
[INFO] 2024-05-26T11:44:45Z Starting Label service.
[INFO] 2024-05-26T11:44:45Z Selected frontend configuration localhost:8000
[INFO] 2024-05-26T11:44:45Z Starting Client Monitoring Service
[INFO] 2024-05-26T11:44:45Z Reloading client monitoring tables from datastore
[INFO] 2024-05-26T11:44:45Z Starting the hunt manager service.
[INFO] 2024-05-26T11:44:45Z Starting Hunt Dispatcher Service.
[INFO] 2024-05-26T11:44:45Z Starting Enrollment service.
[INFO] 2024-05-26T11:44:45Z server_monitoring: Starting Server Monitoring Service
[INFO] 2024-05-26T11:44:45Z Closing Server Monitoring Event table
[INFO] 2024-05-26T11:44:45Z server_monitoring: Updating monitoring table
[INFO] 2024-05-26T11:44:45Z server_monitoring: Collecting Server.Monitor.Health/Prometheus
[INFO] 2024-05-26T11:44:45Z Starting VFS writing service.
[INFO] 2024-05-26T11:44:45Z Starting Server Artifact Runner Service
[INFO] 2024-05-26T11:44:45Z Starting gRPC API server on 127.0.0.1:8001
[INFO] 2024-05-26T11:44:45Z Launched Prometheus monitoring server on 127.0.0.1:8003
[INFO] 2024-05-26T11:44:45Z GUI is ready to handle TLS requests on https://127.0.0.1:8889/
[INFO] 2024-05-26T11:44:45Z server_monitoring: Finished collecting Server.Monitor.Health/Prometheus
[INFO] 2024-05-26T11:44:45Z Query Stats: {"RowsScanned":1,"PluginsCalled":1,"FunctionsCalled":0,"ProtocolSearch":0,"ScopeCopy":5}
[INFO] 2024-05-26T11:44:45Z Frontend is ready to handle client TLS requests at https://localhost:8000/
[INFO] 2024-05-26T11:44:46Z Compiled all artifacts.
```

> It's worth noting that the version of Velociraptor running in the attached VM is **0.5.8**. Now launch Google Chrome and click the Velociraptor shortcut.

Chrome is likely to show "Your Connection is not private errors", this is expected and you can proceed to 127.0.0.1 via the advanced option.

The credentials for the Velociraptor server are:

- Username: `thmadmin`
- Password: `tryhackme`

If all goes well, you should see the Velociraptor [Welcome screen](https://docs.velociraptor.app/docs/gui/#the-welcome-screen).

![](https://i.imgur.com/AFcjL8H.png)

If you wish to interact and deploy Velociraptor locally in your lab, then **[Instant Velociraptor](https://docs.velociraptor.app/docs/deployment/#instant-velociraptor)** is for you. Instant Velociraptor is a fully functional Velociraptor system that is deployed only to your local machine.

Refer to the official [documentation](https://docs.velociraptor.app/docs/deployment/) for more information on deploying Velociraptor as a server/client infrastructure or as Instant Velociraptor.
# Interacting with Client Machines

If you didn't notice, some links are greyed out when you first log into Velociraptor. See below.

![](https://i.imgur.com/f5h1i8K.png)

These links are specific to client endpoints and will become active once the analyst interacts with these endpoint within the Velociraptor UI. 

Let's add a client to Velociraptor. Remember, since the attached VM is running WSL, the Velociraptor server is running in Ubuntu, but the client will be Windows. 

Run the commands for 'Add Windows as a client (CMD)' from the `commands.txt` on the destkop. 

```shell-session
INFO] 2022-03-31T05:47:36-07:00  _    __     __           _                  __
[INFO] 2022-03-31T05:47:36-07:00 | |  / /__  / /___  _____(_)________ _____  / /_____  _____
[INFO] 2022-03-31T05:47:36-07:00 | | / / _ \/ / __ \/ ___/ / ___/ __ `/ __ \/ __/ __ \/ ___/
[INFO] 2022-03-31T05:47:36-07:00 | |/ /  __/ / /_/ / /__/ / /  / /_/ / /_/ / /_/ /_/ / /
[INFO] 2022-03-31T05:47:36-07:00 |___/\___/_/\____/\___/_/_/   \__,_/ .___/\__/\____/_/
[INFO] 2022-03-31T05:47:36-07:00                                   /_/
[INFO] 2022-03-31T05:47:36-07:00 Digging deeper!                  https://www.velocidex.com
[INFO] 2022-03-31T05:47:36-07:00 This is Velociraptor 0.5.8 built on 2021-04-11T22:11:10Z (e468f54c)
[INFO] 2022-03-31T05:47:36-07:00 Loading config from file velociraptor.config.yaml
Generating new private key....
[INFO] 2022-03-31T05:47:36-07:00 Setting temp directory to C:\Program Files\Velociraptor\Tools
[...]
```

> To see the client and interact with it, click on the `magnifying glass` with an empty search query (no text in the search bar) or click `Show All`.

Below is a brief explanation of each column

|   |   |
|---|---|
|**Online State**|A green dot indicates the endpoint is online and communicating with the Velociraptor server. A yellow dot means the server hasn't received any communication from the endpoint within a 24-hour time frame. A red dot means it's been more than 24 hours since the server last heard from the endpoint.|
|**Client ID**|This is a unique ID assigned to the client by the Velociraptor server, and the server will use this client ID to identify the endpoint. A client ID always starts with the letter **C**.|
|**Hostname**|This is the hostname the client identifies itself to the Velociraptor server. Remember that hostnames can change, hence why Velociraptor uses the Client ID instead of identifying a client machine.|
|**Operating System Version**|The Velociraptor client can run on Windows, Linux, or MacOS. The details regarding the client operating system are displayed in this column.|
|**Labels**|Client machines may have multiple labels attached to them. This is useful to identify multiple clients as a group.|
Click on the agent to bring you to a semi-detailed view. By default, the view shown is the overview for the client.
## Overview

In this view, the analyst (you) will see additional information about the client. The additional details are listed below:

- **Client ID**
- **Agent Version**
- **Agent Name**
- **Last Seen At**
- **Last Seen IP**
- **Operating System**
- **Hostname**
- **Release**
- **Architecture**
- **Client Metadata**
## VQL Drilldown

In this view, there is additional information about the client, such as Memory and CPU usage over 24 hours timespan, the Active Directory domain if the client is a domain-joined machine and the active local accounts for the client.

The data is represented in two colors in the Memory and CPU footprint over the past 24 hours.

- **Orange** - Memory Usage
- **Blue** - CPU Usage
## Shell

With the shell, commands can be executed remotely on the client machine. Commands can be run in **PowerShell**, **CMD**, **Bash** or **VQL**. Depending on the target operating system will determine which the analyst will pick. For example, CMD will not be a viable option if the client machine is running Linux. 

It's straightforward, choose one of the options to run the command in and click `Launch`.

In the example below, the command `whoami` was executed with PowerShell. The command results are not immediately visible, and the **eyeball** icon needs to be toggled to see the command results. 
## Collected

Here the analyst will see the results from the commands executed previously from the Shell. Other actions, such as interacting with the **VFS (Virtual File System)**, will appear here in Collected. VFS will be discussed later in upcoming tasks. 

Across the top pane are brief details of the 'collected' artifact. See below.

![](https://i.imgur.com/KaZLog9.png)

Clicking on any FlowID will populate the bottom pan with additional details regarding the information collected for that artifact or collection.

![](https://i.imgur.com/Pdajq3s.png)

This section is very busy, and I'll leave you to acquaint yourself with the information displayed here for each collected artifact. 

The questions in this task will help nudge you to navigate throughout the output returned for each shell execution (i.e. `whoami`).

In the next task, we'll explore how to create a collection and review the results in Collected. 
## Interrogate

Per the [documentation](https://docs.velociraptor.app/docs/gui/clients/), "Interrogate operation. Interrogation normally occurs when the client first enrolls, but you can interrogate any client by clicking the Interrogate button".

To confirm this, click `Interrogate`. Now navigate back to Collected. You will notice that the **Artifact Collection** is **Generic. Client.Info**, which is an additional collection on the list. The first artifact collection in the list is indeed **Generic.Client.Info**. This is the same information displayed under **VQL Drilldown**.  

Refer to the official Velociraptor documentation titled [Inspecting Clients](https://docs.velociraptor.app/docs/gui/clients/) for additional information.
# Creating a New Collection

We will take advantage of the WSL set-up in the attached VM and choose an artifact specific to Ubuntu. 

There will be 5 stages in this process.

- **Select Artifacts**
- **Configure Parameters**
- **Specify Resources**
- **Review**
- **Launch**
## Select Artifacts

In the search bar, type `Windows.KapeFiles.Targets`. If you're not familiar with KAPE, please visit the KAPE Room.

In short, `KapeFiles` are community-created targets and modules for use with KAPE. But as you can see, other tools use these KapeFiles as well. 

When you select the artifact, a brief description of the collector will be displayed on the right, along with a rundown of the parameters. 

![](https://i.imgur.com/ZLnj4iL.png)
## Configure Parameters

![](https://i.imgur.com/oUkNRG4.png)
## Specify Resources

You can't leave this untouched. See the below screenshot.

![](https://i.imgur.com/JaEXvgS.png)
## Review

The output will display in JSON format and it's pretty straightforward. Only one setting was enabled to collect, which was Ubuntu.

![](https://i.imgur.com/TuqboAt.png)
## Launch

Everything should now be in order. Now it's time to launch the collection to gather the artifacts.

When you click **Launch**, you will be directed to the Collected view. Notice that there should be a new entry with the newly created collection. In particular, notice the State. It should show an hourglass which indicates the artifacts are actively being gathered for that collection. 

![](https://i.imgur.com/XfAvjD3.png)

Once the artifacts have been gathered, the state will change from an hourglass to checkmark like the others.

![](https://i.imgur.com/UYipUak.png)

As the list of collections grows, you can search for specific collections using the textfield at the top of the column. See the above screenshot. Sweet, now that we got that covered, let's look at VFS. Refer to the Velociraptor documentation to learn more about [Artifacts](https://docs.velociraptor.app/docs/gui/artifacts/).
# VFS (Virtual File System)

Per the [documentation](https://docs.velociraptor.app/docs/gui/vfs/), "_The VFS is simply a server side cache of the files on the endpoint. It is merely a familiar GUI to allow inspection of the client’s filesystem_".

This can prove useful in an incident response scenario where you, the analyst, need to inspect artifacts in a client. 

Refer to the official documentation for a complete overview of the VFS. In this task, we're going to focus on getting hands-on with VFS.

Below is what you should see when you first access the VFS for a client.

![](https://i.imgur.com/AMgBAOb.png)

In the left pane, along with the middle pane, there are 4 folders (or accessors, filesystem access drivers): 

- **file**: uses operating system APIs to access files
- **ntfs**: uses raw NFTS parsing to access low level files
- **registry**: uses operating system APIs to access the Windows registry
- **artifacts**: previously run commands

Three buttons are highlighted in the above image. Below is a brief explanation for each.

![](https://i.imgur.com/J8UnZKZ.png)

1. Refresh the current directory (sync it's listing from the client)
2. Recursively refresh this directory (sync its listing from the client)
3. Recursively download this directory from the client

Let's continue interacting with VFS.

When any folder is clicked  in the left pane, additional details are displayed in the middle pane. For example, if the file folder is clicked, a subfolder will appear, which is **C:**. Now the details in the middle pane change to reflect C:.
# VQL (Velociraptor Query Language)

Per the official [documentation](https://docs.velociraptor.app/docs/overview/#vql---the-velociraptor-difference), "_Velociraptor’s power and flexibility comes from the Velociraptor Query Language (VQL). VQL is a framework for creating highly customized artifacts, which allow you to collect, query, and monitor almost any aspect of an endpoint, groups of endpoints, or an entire network. It can also be used to create continuous monitoring rules on the endpoint, as well as automate tasks on the server_".

With many tools that you will encounter in your SOC career, some tools may have their own query language. For example, in Splunk its SPL ([Search Processing Language](https://docs.splunk.com/Splexicon:SPL#:~:text=abbreviation,functions%2C%20arguments%2C%20and%20clauses.)), Elastic has KQL ([Kibana Query Language](https://www.elastic.co/guide/en/kibana/current/kuery-query.html)), Microsoft Sentinel has KQL [too] ([Kusto Query Language](https://docs.microsoft.com/en-us/azure/sentinel/kusto-overview)), etc.

VQL is the meat and potatoes of Velociraptor. Throughout each task thus far, unbeknownst to you, you have been interacting with VQL.

To jog your memory, navigate back to **Collected** and inspect **Generic.Client.Info**. Click the requests tab in the bottom pane. See below image.

```SQL
"VQL": "Let Generic_Client_Info_User_0_0=SELECT Name, Description, Mtime AS LastLogin FROM Artifact.Windows.Sys.Users()"
```

If you are familiar with SQL (Structured Query Language) then you should notice the similarities, for example: **SELECT**, **FROM** and **WHERE**.

To execute a simple VQL on your own, first create a **[Notebook](https://docs.velociraptor.app/docs/vql/notebooks)**.

Navigate to the **Notebooks** tab. In Velociraptor, **Notebooks** are *containers* that we can use to execute our queries and commands, as demonstrated below.

![](https://i.imgur.com/HM3Gz2f.gif)

Notebooks consist of two languages - **[Markdown](https://www.markdownguide.org/getting-started/)** and (of course) **VQL**. If you are familiar with [Jupyter Notebooks](https://jupyter.org/) they function in a very similar fashion!

Let's create our first notebook and enter some simple markdown. We'll circle back to VQL shortly. 

![](https://i.imgur.com/1UW8BVS.gif)

Sweet! Now let's set our notebook to use VQL instead & query basic information from current agent, we can use `SELECT * FROM info()`.

> [!NOTE]
> **Note**: click into the lower box to display the options for this, then select the pencil to edit. 

![](https://i.imgur.com/Sgbc1HF.png)

Let's save this notebook and run it against the agent as demonstrated below.

![](https://i.imgur.com/reh5ZYs.gif)

VQL can also be run via the command line. See the example below.

For this example, VQL is run from the command line querying an agent for details such as its hostname.

![](https://i.imgur.com/QQz5K3V.gif)
## Artifacts

Before wrapping up this task, let's touch on **Artifacts** (or VQL Modules).

Per the [documentation](https://docs.velociraptor.app/docs/vql/artifacts/), "_Velociraptor allows packaging VQL queries inside mini-programs called Artifacts. An artifact is simply a structured YAML file containing a query, with a name attached to it. This allows Velociraptor users to search for the query by name or description and simply run the query on the endpoint without necessarily needing to understand or type the query into the UI_".

This was a **BRIEF** intro to VQL. It is recommended to review the official [documentation](https://docs.velociraptor.app/docs/vql/) thoroughly to fully understand it and how you can wield its power to execute advanced queries. Also, reference the [VQL Reference](https://docs.velociraptor.app/vql_reference/) and [Extending VQL](https://docs.velociraptor.app/docs/extending_vql/) for further information on VQL.
# Forensic Analysis

Per the [documentation](https://docs.velociraptor.app/docs/forensic/), "_VQL is not useful without a good set of plugins that make DFIR work possible. Velociraptor’s strength lies in the wide array of VQL plugins and functions that are geared towards making DFIR investigations and detections effective_".

There is a lot of information to cover here regarding VQL plugins. This task aims to give you enough information regarding these plugins so you can construct your VQL query to hunt for artifacts of a popular exploit known as Printnightmare. 

At the date of the entry of this content, below are the categories surrounding forensic analysis:

- **Searching Filenames**
- **Searching Content**
- **NTFS Analysis**
- **Binary Parsing**
- **Evidence of Execution**
- **Event Logs**
- **Volatile Machine State**

Have a skim through **Searching Filenames** and **NTFS Analysis** to provide a solid brain dump to prep you for the questions below and for the next task.


