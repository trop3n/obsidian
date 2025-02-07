#tryhackme #DFIR #cybersecurity #soclevel1 
# Introduction

Many tools can aid a security analyst or incident responder in performing memory analysis on a potentially compromised endpoint. One of the most popular tools is **[Volatility](https://tryhackme.com/room/volatility)**, which will allow an analyst to dig deep into the weeds when examining memory artifacts from an endpoint. But this process can take time. Often, when an analyst is triaging, time is of the essence, and the analyst needs to perform a quick assessment to determine the nature of a security event.

That is where the FireEye tool [**Redline**](https://fireeye.market/apps/211364) comes in. Redline will essentially give an analyst a 30,000-foot view (10 kilometers high view) of a Windows, Linux, or macOS endpoint. Using Redline, you can analyze a potentially compromised endpoint through the memory dump, including various file structures. With a nice-looking GUI (Graphical User Interface) - you can easily find the signs of malicious activities. 

Here is what you can do using Redline:

- Collect registry data (Windows hosts only)
- Collect running processes
- Collect memory images (before Windows 10)
- Collect Browser History
- Look for suspicious strings
- And much more!

Installing Redline on your local machine is straightforward. Run the MSI file and follow the installation process.
# Data Collection

Now that you have the overview of Redline, let's move to the Data Collection stage.

There are three ways or options to collect data using Redline:

1. **Standard Collector**: this method configures the script to gather a minimum amount of data for the analysis. This is going to be our *preferred method* to collect data in this room. It is also usually the fastest method to collect the data you need. It takes only a few minutes to complete.
2. **Comprehensive Collector**: this method configures the script to gather the most data from your host for further analysis. This method takes up to an hour or more. You will choose this method if you prefer the full analysis of the system.
3. **IOC Search Collector (Windows Only)**: this method collects data that matches with the [Indicators of Compromise (IOCs)](https://www.crowdstrike.com/cybersecurity-101/indicators-of-compromise/) that you created with the help of [IOC Editor](https://fireeye.market/apps/S7cWpi9W). You will choose this method if you want to run the data collection against known IOCs that you have gathered either through threat intelligence (data feed or narrative report), incident response, or malware analysis. You imported them into [IOC Editor](https://fireeye.market/apps/S7cWpi9W). We'll look at the IOC Editor a bit further in the next task.

Before proceeding, launch Redline. The icon is conveniently on the taskbar.

In this task, we will be using the Standard Collector method. 

- From Redline, click on "Create a Standard Collector".
- You will have an option to choose the target platform. In our case, we will select **Windows**. 

![](https://i.imgur.com/LAisumU.png)

- Under the *Review Script Configuration*, click on "Edit Your Script", this is one of the *crucial steps* since you will be presented with the set of data to choose to collect from the host. There will be five tabs, which include **Memory, Disk, System, Network and Other**.

Let's dive into some details:
## Memory

![](https://i.imgur.com/WIlpw0G.png)

You can configure the script to collect memory data such as process listings, drivers enumeration (Windows hosts only), and hook direction (versions before Windows 10).

> [!NOTE]
> **Note**: for this exercise, uncheck **Hook Detection** and make sure **Acquire Memory Image** is also unchecked. 
## Disk

This is where you can collect the data on Disks partitions and Volumes along with File Enumeration.

![](https://i.imgur.com/rHTQ8J3.png)
## System

The System will provide you with *machine information*:

- Machine and operating system information
- Analyze system restore points (Windows versions before 10 only)
- Enumerate the registry hives (Windows only)
- Obtain user accounts
- Obtain groups (OS X only)
- Obtain the prefetch cache

![](https://i.imgur.com/JcxcpWN.png)
## Network

> Network Options supports Windows, OS X, and Linux platforms. You can configure the script to collect network information and browser history, which is essential when investigating browser activities, including malicious file downloads and inbound/outbound connections.

![](https://i.imgur.com/2kSKazC.png)
## Other

![](https://i.imgur.com/hYT9XK5.png)

With this option, you can collect the data on different services and tasks running on the system, including the hashes. 

- Now we are ready to proceed to the next important step. After choosing your data options - click OK. And then click on "Browser" under "Save Your Collector To". Why is this an important step? because you will need to create a folder where your analysis file will be saved and the script for collecting the data you need. In our case, we are saving it to the *Analysis* folder.

![](https://i.imgur.com/cLXkaa1.png)

> [!NOTE]
> **Note**: You can choose any folder you wish but make sure that the folder is empty. Complete this dialog by clicking the OK button. 

- After you choose to save the collector to the folder, you will see the Collector Instructions.

![](https://i.imgur.com/UvpW4EY.png)

- If you go into the folder, you will notice the bat file under the name "**RunRedlineAudit**". This is the executable script to collect data from the host. The script needs to be *run as Administrator* to be able to collect the data we need. 

![](https://i.imgur.com/23s91g7.png)

- Running the script will open a command prompt window; this indicates that the script is running successfully. It will close automatically when the data collection process finishes. 

![](https://i.imgur.com/8DugUxr.png)

> [!NOTE]
> **Note**: This process may take between 15-20 minutes to complete. 

- After the script is finished, you will notice a new file created - **AnalysisSession1** (in the **Sessions** folder) with the `.mans` extension. This file is what we need to be able to import into Redline for investigation. Just double-click on the file to import the audit data.

![](https://i.imgur.com/HItGGqB.png)

> [!TIP]
> **Tip**: If you run the script multiple times, the naming convention of the analysis file will increment by 1. For example, if you run the script two times, you will see **AnalysisSession1** and **AnalysisSession2**. 

Congratulations! Now you have the data you need and are ready to dive into the investigation process in the upcoming tasks.
# The Redline Interface

Let's look at the Redline interface.

You should have your first analysis file. Double-click on the *AnalysisSession1.mans* file and the data will be imported automatically into Redline. Please give up to 10 minutes for the data to be imported.

![](https://i.imgur.com/zqvBc36.png)

When the data is imported, you will be presented with this view:

![](https://i.imgur.com/rJ0HAIV.png)

On the left panel, you will see different types of *Analysis Data*; this is where you will perform information gathering and investigation processes.

- **System Information**: this is where you will see the information about the machine, BIOS (Windows Only), operating system, and user information.
- **Processes**: processes will contain different attributes such as Process Name, PID, Path, Arguments, Parent process, Username, etc. When you expand the Processes tab, there will be four sections: Handles, Memory Sections, Strings and Ports.

A **handle** is a connection from a process to an object or resource in a Windows operating system. Operating systems use handles for referencing internal objects like files, registry keys, resources, etc.

**Memory Sections** will let you investigate unsigned memory sections used by some processes. Many processes usually use legitimate dynamic link libraries (DLLs), which will be signed. This is particularly interesting because if you see any unsigned DLLs then it will be worth taking a closer look. 

**Strings**: you will see the information on the captured strings.

**Ports**: this is one of the *critical sections to pay attention to*. Most malware often initiates the outbound or inbound connections to communicate to their command and control server (C2) to do some malicious activities like exfiltrating the data or grabbing a payload to the machine. This situation is where you can review the suspicious connections from ports and IP addresses. Pay attention to the system processes as well. The threat actors like to avoid detection by hiding under system processes. For example, `explorer.exe` or `notepad.exe` shouldn't be on the list of processes with outbound connections.

Some of the other important sections you need to pay attention to are:

- File System (**not included in this analysis section**)
- Registry
- Windows Services
- Tasks (Threat actors like to create scheduled tasks for persistence)
- Event logs (this is another great place to look for the suspicious Windows PowerShell events as well as the Logon/Logoff, user creation events, and others)
- ARP and Route Entries (**not included in this analysis session**)
- Browser URL History (**not included in this analysis session**)
- File Download History

The **Timeline** will help you to better understand when the compromise happened and what steps the malicious actor took to escalate the attack. The **Timeline** will also record every action on the file if it got created, changed, modified, accessed.

If you know when the host compromise or suspicious activity occurred, you can use **TimeWrinkles™** to filter out the timeline to only the events that took place around that time.

![](https://i.imgur.com/upEjzUU.png)

**TimeCrunches** helps to reduce the excessive amount of data that is not relevant in the table view. A TimeCrunch will hide the same types of events that occured within the same minute you specified. 

![](https://i.imgur.com/Jw5150B.png)

You can find out more about each type of data analysis using the Redline User Guide: [https://fireeye.market/assets/apps/211364/documents/877936_en.pdf](https://fireeye.market/assets/apps/211364/documents/877936_en.pdf).  

Now you have learned some basics of different data types to help you during the investigation process. Let's go hunting and see if you can answer some of the questions in the next task.

# IOC Search Collector

We briefly discussed the usage of the **IOC Search Collector** in the **Data Collection** task.

Let's take a closer look at the capabilities of this collector type. But first, let's recap what an IOC is.

IOC stands for **Indicators of Compromise**; they are artifacts of the potential compromise and host intrusion on the system or network that you need to look for when conducting threat hunting or performing incident response. IOCs can be MD5, SHA1, SHA256 hashes, IP address, C2 domain, file size, filename, file path, a registry key, etc.

One of the great tools you can use is  [IOC Editor,](https://fireeye.market/apps/S7cWpi9W) created by FireEye, to create IOC files. You can refer to this link to learn how to use the IOC Editor: [https://fireeye.market/assets/apps/S7cWpi9W//9cb9857f/ug-ioc-editor.pdf](https://fireeye.market/assets/apps/S7cWpi9W//9cb9857f/ug-ioc-editor.pdf).

> [!NOTE]
> **Note**: according to the  [IOC Editor,](https://fireeye.market/apps/S7cWpi9W) download page Windows 7 is the latest operating system officially supported. It is the same version installed on the attached VM. There is another tool called [OpenIOC Editor](https://fireeye.market/apps/211404) by FireEye, which supports Windows 10 that is worth taking a look at.

> [!TIP]
> **Tip**: Before proceeding you can close Redline to free up some system resources while using IOC Editor.

You can create a text file containing IOCs, modify them, and share it with other people in the InfoSec industry. 

In this example, we will look at an IOC of a keylogger created with IOC editor. 

> [!NOTE]
> **Note**: Below, you may follow along with the screenshots and don't have to create the IOC file in this task. You will create an IOC file using IOC Editor and perform an IOC Search in the next task. 

Open IOC Editor which was conveniently placed for you in the taskbar next to Redline.

![](https://i.imgur.com/kF6UP8Z.png)

A brief explanation of the above image:

- The **Name** of the IOC file is Keylogger, Keylogger.ioc. 
- The **Author** is RussianPanda
- **GUID**, **Created**, **Modified** are fields you can **NOT** edit, and IOC Editor populates the information.
- Under **Description**, you can add a summary explaining the purpose of the IoC file.

The actual IoC will be added under, you guessed it, **Add**.

Here are the values from the image above:

- **File Strings**: `psylog.exe`
- **File Strings**: `RIDEV_INPUTSINK`
- **File MD5**: `791ca706b285b9ae3192a33128e4ecbb`
- **File Size**: `35400`

Refer to the gif below to get an idea of adding specific IOCS to the IOC file. 

![](https://i.imgur.com/m42ynWi.gif)

Once you select an item you can enter the value for the item directly. You can also add it within the **Properties**.

All the fields are read-only except for **Content** and **Comment**. To add a value to the item enter it under **Content**.

![](https://i.imgur.com/W4687eb.png)

Once you enter the value click Save to save it.

**Note**: You can right-click on an item for additional options. See below.

![](https://i.imgur.com/en4SiKW.png)

We'll leave that for you to explore on your own. 

Now that we've created and saved the IOC file, let's move on and go back to the **IOC Search Collector** in the **Redline** tool.

**Note**: If you closed Redline now is the time to relaunch the application. You can close IOC Editor, again, to free up system resources. 

**IOC Search Collector** will ignore the data that doesn't match an IOC you have gathered. Although, you can always choose to collect additional data. As the Redline User Guide states, the quality of the IOC analysis will depend on the data you have available in the analysis session.

To create an IOC Search Collector, click "Browse..." and choose the location of the .ioc file. Redline will automatically detect the .ioc file and place it in the Indicators section, as shown below.

![](https://i.imgur.com/5BGb0be.png)

**Unsupported Search Terms:** These terms will not show any successful hits in Redline, which means Redline doesn't recognize specific search terms. 

**Supported Search Terms:** The terms that Redline will recognize and search for.

After you are finished reviewing the configured IOCs, click "Next". Now click on "Edit your script" to configure what data will be collected for the analysis. For this example, Keylogger file IOC Search, the following parameters were selected.

![](https://i.imgur.com/6qrxht0.png)

**Note**: When you configure your own IOC Search, you will choose different settings for your script compared to the settings above. 

When done editing the script, click "OK". 

In the "Save Your Collector To" section, click "Browse" and choose an empty folder where your analysis file will be saved along with the **RunRedlineAudit.bat** file. 

After executing the .bat file in the same manner as before, let's now wait for the analysis to finish.

After the analysis is finished, you will see the .mans file (AnalysisSession1 in our example). Double-click the file to open it in Redline.

If Redline fails to generate the IOC report automatically, you can manually generate it by clicking "Create New IOC Report" and importing your `.ioc` file.

When the report generation completes, you should see the "Hits". You can expand the list by clicking on the entries in each row.

![](https://i.imgur.com/8Z2maOk.png)

From the screenshot, you can see that there was one hit on "chrome.dll", this is a false positive. Let's review the details below.

![](https://i.imgur.com/LpaLoes.png)

As you can see, the DLL file matched with the string "RIDEV_INPUTSINK" that we had in our .ioc file. It's important to gather granulated and accurate artifacts to add to your IOC file to avoid false positives. 

The screenshot below is of a file with the most amount of "Hits", which means it is most likely the file we are looking for.

![](https://i.imgur.com/biZOTJ5.png)

You should be ready to answer the questions below using the screenshots provided in the task and perform these similar actions in the upcoming task!

