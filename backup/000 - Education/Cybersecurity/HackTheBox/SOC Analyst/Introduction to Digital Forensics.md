---
title: Introduction to Digital Forensics
author:
  - HackTheBox
source: https://academy.hackthebox.com/module/237/section/2608
---
# Introduction

> [!NOTE]
> It is essential to clarify that this module does not claim to be an all-encompassing or exhaustive program on Digital Forensics. This module provides a robust foundation for SOC analysts, enabling them to confidently tackle key Digital Forensics tasks. The primary focus of the module will be the analysis of malicious activity within Windows-based environments.

`Digital Forensics`, often referred to as computer forensics or cyber forensics, is a specialized branch of cybersecurity that involves the collection, preservation, analysis, and presentation of digital evidence to investigate cyber incidents, criminal activities, and security breaches. It applies forensic techniques to digital artifacts, including computers, servers, mobile devices, networks and storage media, to uncover the truth behind cyber-related events. Digital forensics aims to:

- **reconstruct timelines**
- **identify malicious activities**
- **assess the impact of incidents**
- **provide evidence for legal and regulatory proceedings**

Digital forensics is an integral part of the incident response process, contributing crucial insights and support at various stages.
## Key Concepts:

- `Electronic Evidence`: Digital forensics deals with electronic evidence, which can include files, emails, logs, databases, network traffic, and more. This evidence is collected from computers, mobile devices, servers, cloud services, and other digital sources.
- `Preservation of Evidence`: Ensuring the integrity and authenticity of digital evidence is crucial. Proper procedures are followed to preserve evidence, establish a chain of custody, and prevent any unintentional alterations.
- `Forensic Process`: The digital forensics process typically involves several stages:
	- `Identification`: Determining potential sources of evidence.
	- `Collection`: Gathering data using forensically sound methods.
	- `Examination`: Analyzing the collected data for relevant information.
	- `Analysis`: Interpreting the data to draw conclusions about the incident. 
	- `Presentation`: Presenting findings in a clear and comprehensible manner.
- `Types of Cases`: Digital forensics is applied in a variety of cases, including:
	- Cybercrime investigations (hacking, fraud, data theft).
	- Intellectual property theft.
	- Employee misconduct investigations.
	- Data breaches and incidents affecting organizations.
	- Litigation support in legal proceedings.

The basic steps for performing a forensic investigation are as follows:

1. `Create a Forensic Image`
2. `Document the System's State`
3. `Identify and Preserve Evidence`
4. `Analyze the Evidence`
5. `Timeline Analysis`
6. `Identify Indicators of Compromise`
7. `Report and Documentation`
## Digital Forensics and SOC Analysts

When we talk about the Security Operations Center (SOC), we're discussing the frontline defense against cyber threats. But what happens when a breach occurs, or when an anomaly is detected? That's where digital forensics comes into play.

First and foremost, digital forensics provides us with a `detailed post-mortem of security incidents`. By analyzing digital evidence, we can trace back the steps of an attacker, understanding their methods, motives and possibly even their identity. This retrospective is crucial for improving our defenses and understanding our vulnerabilties. 

Moreover, in the heart of a security incident, *time is of the essence*. Digital forensics tools can `rapidly sift through vast amounts of data, pinpointing the exact moment of compromise, the affected systems, and the nature of the malware attack or technique used`. This swift identification allows us to contain the threat faster, minimizing potential damage.

Let's not forget about the legal implications. In the event of a significant breach, especially one that affects customers or stakeholders, there's a high likelihood of *legal repercussions*. Digital forensics not only helps us in identifying the culprits but also `provides legally admissible evidence` that can be used in court. This evidence is **meticulously logged**, **hashed**, and **timestamped** to ensure its integrity and authenticity. 

Furthermore, the insights gained from digital forensics empower our SOC teams to `proactively hunt for threats`. Instead of merely reacting to alerts, we can actively search our environments for signs of compromise, leveraging indicators of compromise and tactics, techniques and procedures identified from past incidents. 

Another critical aspect is the `enhancement of our incident response strategies`. By understanding the full scope of an attack, we can better tailor our response, ensuring that every compromised system is addressed and that no stone is left unturned. This comprehensive approach reduces the risk of attackers lingering in our environment or using the same attack vector twice. 

Lastly, digital forensics `fosters a culture of continuous learning within our SOC teams`. Every incident, no matter how small, provides a learning opportunity. By dissecting these incidents, our analysts can stay ahead of the curve, anticipating new attack techniques and bolstering our defenses accordingly. 

In conclusion, `digital forensics isn't just a reactive measure, it's a proactive tool that amplifies the capabilities of our SOC analysts`, ensuring our organization remains resilient in the face of ever-evolving cyber threats.
# Windows Forensics Overview

> [!Important] Links
>  [[Windows Forensics 1]] | [[Windows Forensics 2]] | [[KAPE]] | [[Autopsy]] | [[Velociraptor]]

In this section, we will provide a concise overview of the key Windows artifacts and forensic procedures.
## NTFS

NTFS (New Technology File System) is a proprietary file system developed by Microsoft as part of its Windows NT operating system family. It was introduced with the release of Windows NT 3.1 and it has since become the default and most widely used filesystem in modern Windows operating systems, including Windows XP, Windows 7, Windows 8, Windows 10, and their server counterparts.

NTFS was designed to address several limitations of its predecessor, the FAT (File Allocation Table) file system. It introduced numerous features and enhancements that improved the reliability, performance, security and storage capabilities of the file system.

Here are some of the key forensic artifacts that digital investigators often analyze when working with NTFS file systems:

- `File Metadata`: NTFS stores extensive metadata for each file, including:
	- Creation Time
	- Modification Time
	- Access Time
	- Attribute information (read-only, hidden, or system file attributes).
		Analyzing these timestamps can help establish timelines and reconstruct user activities. 

- `MFT Entries`: The Master File Table (MFT) is a crucial component of NTFS that stores metadata for all files and directories on a volume. Examining MFT entries provides insights into file names, sizes, timestamps, and data storage locations. When files are deleted, their MFT entries are marked as available, but the data may remain on the disk until overwritten.

- `File Slack and Unallocated Space`: Unallocated space on an NTFS volume may contain remnants of deleted files or fragments of data. File slack refers to the unused portion of a cluster that may contain data from a previous file. Digital forensics tools can help recover and analyze data from these areas.

- `File Signatures`: File headers and signatures can be useful in identifying file types and even when file extensions have been changed or obscured. This information is critical for reconstructing the types of files present on a system.

- `USN Journal`: The Update Sequence Number (USN) Journal is a log maintained by NTFS to record changes made to files and directories. Forensic Investigators can analyze the USN Journal to track file modifications, deletions, and renames.

- `LNK Files`: Windows Shortcut Files (LNK) files, contain information about the target file or program, as well as timestamps and metadata. These files can provide insights into recently accessed files or executed programs.

- `Prefetch Files`: Prefetch files are generated by Windows to improve the startup performance of applications. These files can indicate which programs have been run on the system and when they were last executed. 

- `Registry Hives`: While not directly related to the file system, Windows Registry hives contain important configuration and system information. Malicious activities or unauthorized changes can leave traces in the registry, which forensic investigators analyze to understand system modifications. 

- `Shellbags`: Shellbags are registry entries that store folder view settings, such as *window positions* and *sorting preferences*. Analyzing shellbags can reveal user navigation patterns and potentially identify accessed folders.

- `Thumbnail Cache`: Thumbnail caches store miniature previews of images and documents. These caches can reveal files that were recently viewed, even if the original files have been deleted.

- `Recycle Bin`: The Recycle Bin contains files that have been deleted from the filesystem. Analyzing the Recycle Bin can help recover deleted files and provide insights into user actions.

- `Alternate Data Streams (ADS)`: ADS are additional streams of data associated with files. Malicious actors may use ADS to hide data, and forensic investigators need to examine these streams to ensure a comprehensive analysis. 

- `Volume Shadow Copies`: NTFS supports **Volume Shadow Copies**, which are snapshots of the file system at different points in time. These copies can be valuable for data recovery and analysis of changes made over time.

- `Security Descriptors and ACLs`: **Access Control Lists** (ACLs) and security descriptors determine file and folder permissions. Analyzing these artifacts helps understand user access rights and potential security breaches. 
## Windows Event Logs

`Windows Event Logs` are an intrinsic part of the Windows Operating System, storing logs from different components of the system including the system itself, applications running on it, ETW providers, services, and others. 

Windows event logging offers comprehensive logging capabilities for application errors, security events, and diagnostic information. As cybersecurity professionals, we leverage these logs extensively for analysis and intrusion detection.

Adversarial tactics from initial compromise using malware or other exploits, to credential accessing, privilege elevation and lateral movement using Windows operating system's internal tools are often captured via Windows event logs.

By viewing the available Windows event logs, investigators can get a good sense of what is being logged and even search for specific log entries. To access the logs directly for offline analysis, investigators should navigate to the default file path for log storage at `C:\Windows\System32\winevt\logs`.

The analysis of Windows Event Logs has been addressed int he modules titled `Windows Event Logs & Finding Evil` and `YARA & Sigma for SOC Analysts`.
## Execution Artifacts

`Windows Execution Artifacts` refer to the *traces and evidence left behind on a Windows operating*
*system when programs and processes are executed*. These artifacts provide valuable insights into the execution of applications, scripts, and other software components, which can be crucial in digital forensics investigations, incident response, and cybersecurity analysis. By examining execution artifacts, investigators can:

- `Reconstruct Timelines`
- `Identify Malicious Activities`
- `Establish patterms of behavior`

Here are some of the common types of Windows execution artifacts:

- `Prefetch Files`: Windows maintains a prefetch folder that contains metadata about the execution of various applications. Prefetch files record information such as file paths, execution counts, and timestamps of when applications were run. Analyzing prefetch files can reveal a history of executed programs and the order in which they were run.

- `Shimcache`: Shimcache is a Windows mechanism that logs information about program execution to assist with compatibility and performance optimizations. It records details such as file paths, execution timestamps, and flags indicating whether a program was executed. Shimcache can help investigators identify recently executed programs and their associated files. 

- `Amcache`: Amcache is a database introduced in Windows 8 that stores information about installed applications and executables. It includes details like file paths, sizes, digital signatures, and timestamps of when applications were last executed. Analyzing the Amcache can provide insights into program execution history and identify potentially suspicious or unauthorized software.

- `UserAssist`: UserAssist is a registry key that *maintains information about programs executed by* users. It records details such as:
	- Application Names
	- Execution Counts
	- Timestamps
		Analyzing UserAssist artifacts can reveal a history of executed applications and user activity.

- `RunMRU Lists`: The RunMRU (Most Recently Used) lists in the Windows Registry store information about recently executed programs from various locations, such as the `Run` and `RunOnce` keys. These lists can indicate which programs were run, when they were executed, and potentially reveal user activity.

- `Jump Lists`: Jump lists stored *information about recently accessed files, folders and tasks* associated with specific applications. They can provide insights into user activities and recently used files. 

- `Shortcut (LNK) Files`: Shortcut files can contain information about the target executable, file paths, timestamps, and user interactions. Analyzing LNK files can reveal details about executed programs and the context in which they were run. 

- `Recent Items`: The Recent Items folder maintains a list of recently opened files. It can provide information about recently accessed documents and user activity.

- `Windows Event Logs`: Various Windows event logs, such as the **Security**, **Application**, and **System Logs**, record events *related to program execution*, including process creation and termination, application crashes, and more.

| Artifact             | Location/Registry Key                                                                        | Data Stored                                                                    |
| -------------------- | -------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| Prefetch Files       | C:\Windows\Prefetch                                                                          | Metadata about executed applications (file paths, timestamps, execution count) |
| Shimcache            | Registry: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache | Program execution details (file paths, timestamps, flags)                      |
| Amcache              | C:\Windows\AppCompat\Programs\Amcache.hve (Binary Registry Hive)                             | Application details (file paths, sizes, digital signatures, timestamps)        |
| UserAssist           | Registry: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist    | Executed program details (application names, execution counts, timestamps)     |
| RunMRU Lists         | Registry: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU        | Recently executed programs and their command lines                             |
| Jump Lists           | User-specific folders (e.g., %AppData%\Microsoft\Windows\Recent)                             | Recently accessed files, folders, and tasks associated with applications       |
| Shortcut (LNK) Files | Various locations (e.g., Desktop, Start Menu)                                                | Target executable, file paths, timestamps, user interactions                   |
| Recent Items         | User-specific folders (e.g., %AppData%\Microsoft\Windows\Recent)                             | Recently accessed files                                                        |
| Windows Event Logs   | C:\Windows\System32\winevt\Logs                                                              | Various event logs containing process creation, termination, and other events  |
## Windows Persistence Artifacts

Windows persistence refers to the *techniques and mechanisms used by attackers to ensure their* 
*unauthorized presence and control over a compromised system*, allowing them to maintain access and control even after initial intrusion. These persistence methods exploit various system components, such as registry keys, startup processes, scheduled tasks, and services, enabling malicious actors to withstand reboots and security measures while continuing to carry out their objectives undetected.,
### Registry

The Windows `Registry` acts as a **crucial database**, storing critical system settings for the Windows OS. This encompasses:
- `Configurations for devices`
- `Security`
- `Services`
- `Storage of User Account Security Configurations`

in the **Security Accounts Manager** (SAM). Given its significance, it's no surprise that adversaries often target the Windows Registry for establishing persistence. Therefore, it's essential to routinely inspect Registry autorun keys.

Example of `Autorun` keys used for persistence:

- **`Run/RunOnce Keys`**
    - HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run
    - HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce
    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce
    - HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\
- **`Keys used by WinLogon Process`**
    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon
    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Shell
- **`Startup Keys`**
    - HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders
    - HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders
    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders
    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\User
### Schtasks

Windows provides a feature allowing programs to schedule specific tasks. These tasks reside in `C:\Windows\System32\Tasks`, with each one saved as an XML file. This file details the creator, the task's timing or trigger, and the path to the command or program set to run. To scrutinize scheduled tasks, we should navigate to `C:\Windows\System32\Tasks` and examine the XML file's contents.
### Services

`Services` in Windows are **pivotal** for maintaining processes on a system, enabling software components to operate in the background without user intervention. Malicious actors often tamper with or craft *rogue services* to ensure persistence and retain unauthorized access. the registry location to keep an eye on is: `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services`
## Web Browser Forensics

Diving into web browser forensics, it's a discipline centered on **analyzing remnants left by web** 
**browsers**. These remnants can shed light on user actions, online engagements, and potentially harmful behaviors. Some of the pivotal browser forensic artifacts include:

- `Browsing History`: Records of websites visited, including URLs, titles, timestamps, and visit frequency.
- `Cookies`: Small data files stored by websites on a user's device, containing information such as session details, preferences, and authentication tokens.
- `Cache`: Cached copies of web pages, images, and other content visited by the user. Can reveal websites accessed even if the history is cleared.
- `Bookmarks/Favorites`: Saved links to frequently visited websites or pages of interest.
- `Download History`: Records of downloaded files, including source URLs, filenames, and timestamps.
- `Autofill Data`: Information automatically entered into forms, such as names, addresses, and passwords.
- `Search History`: Queries entered into search engines, along with search terms and timestamps.
- `Session Data`: Information about active browsing sessions, tabs, and windows.
- `Typed URLs`: URLs entered directly into the address bar.
- `Form Data`: Information entered into web forms, such as login credentials and search queries.
- `Passwords`: Saved or autofilled passwords for websites.
- `Web Storage`: Local storage data used by websites for various purposes.
- `Favicons`: Small icons associated with websites, which can reveal visited sites.
- `Tab Recovery Data`: Information about open tabs and sessions that can be restored after a browser crash.
- `Extensions and Add-ons`: Installed browser extensions and their configurations.
## SRUM

Switching gears to `SRUM` (System Resource Usage Monitor), it's a feature introduced in Windows 8 and subsequent versions. SRUM meticulously tracks resource utilization and application usage patterns. The data is housed in a database file named `sru.db` found in the `C:\Windows\System32\sru` directory. This SQLite formatted database allows for structured data storage and efficient data retrieval. SRUM's records, organized by time intervals, can help reconstruct application and resource usage over specific durations. 

Key facets of SRUM Forensics encompass:

- `Application Profiling`: SRUM can provide a comprehensive view of the applications and processes that have been executed on a Windows System. It records details such as executable names, file paths, timestamps, and resource usage metrics. This information is crucial for understanding the software landscape on a system, identifying potentially malicious or unauthorized applications, and reconstructing user activities.

- `Resource Consumption`: SRUM captures data on CPU time, network usage and memory consumption for each application and process. This data is invaluable for investigating resource-intensive activities, identifying unusual patterns of resource consumption, and detecting potential performance issues caused by specific applications.

- `Timeline Reconstruction`: By analyzing SRUM data, digital forensics experts can create timelines of application and process execution, resource usage, and system activities. This timeline reconstruction is instrumental in understanding the sequence of events, identifying suspicious behaviors, and establishing a clear picture of user interactions and actions.

- `User and System Context`: SRUM data includes user identifiers, which helps in attributing activities to specific users. This can aid in user behavior analysis and determining whether certain actions were performed by legitimate users or potential threat actors.

- `Malware Analysis and Detection`: SRUM data can be used to identify unusual or unauthorized applications that may be indicative of malware or malicious activities. Sudden spikes in resource usage, abnormal application patterns, or unauthorized software installations can be all be detected through SRUM analysis.

- `Incident Response`: During incident response, SRUM can provide rapid insights into recent application and process activities, enabling analysis to quickly identify potential threats and respond effectively. 
# Evidence Acquisition Techniques and Tools

`Evidence Acquisition` is a critical phase in digital forensics, involving the collection of digital artifacts and data from various sources to preserve potential evidence for analysis. This process requires specialized tools and techniques to ensure the integrity, authenticity, and admissibility of the collected evidence. 

Here's an overview of evidence acquisition techniques commonly used in digital forensics:

- Forensic Imaging
- Extracting Host-based Evidence & Rapid Triage
- Extracting Network Evidence
## Forensic Imaging

Forensic Imaging is a fundamental process in digital forensics that involves creating an exact, bit-by-bit copy of digital storage media, such as hard drives, solid state drives, USB drives and memory cards. This process is crucial for preserving the original state of the data, ensuring data integrity, and maintaining the admissibilty of evidence in legal proceedings. Forensic imaging plays a critical role in investigations by allowing analysts to examine evidence without altering or compromising the original data. 

Below are some forensic imaging tools and solutions:

- [FTK Imager](https://www.exterro.com/ftk-imager): Developed by AccessData (now acquired by Exterro), FTK Imager is one of the most widely used disk imaging tools in the cybersecurity field. It allows us to create perfect copies (or images) of computer disks for analysis, preserving the integrity of the evidence. It also lets us view and analyze the contents of data storage devices without altering the data.
- [AFF4 Imager](https://github.com/Velocidex/c-aff4): A free, open-source tool crafted for creating and duplicating forensic disk images. It's user-friendly and compatible with numerous file systems. A benefit of the AFF4 Imager is its capability to extract files based on their creation time, segment volumes, and reduce the time taken for imaging through compression.
- `DD and DCFLDD`: Both are command-line utilities available on Unix-based systems (including Linux and MacOS). DD is a versatile tool included in most Unix-based systems by default, while DCFLDD is an enhanced version of DD with features specifically useful for forensics, such as hashing.
- `Virtualization Tools`: Given the prevalent use of virtualization in modern systems, incident responders will often need to collect evidence from virtual environments. Depending on the specific virtualization solution, evidence can be gathered by temporarily halting the system and transferring the directory that houses it. Another method is to utilize the snapshot capability present in numerous virtualization software tools.
### Example 1: Forensic Imaging with FTK Imager

Let's now see a demonstration of utilizing `FTK Imager` to craft a disk image. Be mindful that you'll require an auxiliary storage medium, like an external hard drive or USB flash drive to save the resultant disk image:

- Select `File` -> `Create Disk Image`:

![](https://i.imgur.com/6iEIXNg.png)

- Next, select the media source. Typically, it's either `Physical Drive` or `Logical Drive`.

![](https://i.imgur.com/1PY4ADD.png)

- Choose the drive from which you wish to create your image.

![](https://i.imgur.com/0UggTx7.png)

- Specify the destination for the image.

![](https://i.imgur.com/2WlzEAm.png)

- Select the desired image type.

![](https://i.imgur.com/pb9yxJv.png)

- Input evidence details

![](https://i.imgur.com/YJcLwts.png)

- Choose the destination folder and filename for the image. At this step, you can also adjust settings for image fragmentation and compression.

![](https://i.imgur.com/aPf5JWc.png)

- Once all the settings are confirmed, click `start`.

![](https://i.imgur.com/vZFAvi2.png)

- You'll observe the progress of the imaging.

![](https://i.imgur.com/l8wTpdq.png)

- If you opted to verify the image, you'll also see the verification progress.

![](https://i.imgur.com/cvk5xNX.png)

- After the image has been verified, you'll receive an imaging summary. Now, you're prepared to analyze this dump.

![](https://i.imgur.com/MtQTDTq.png)
### Example 2: Mounting a Disk Image with Arsenal Image Mounter

Let's now see another demonstration of utilizing [Arsenal Image Mounter](https://arsenalrecon.com/downloads) to mount a disk image we have previously created (not the one mentioned above) from a compromised Virtual Machine (VM) running on VMWare. The virtual hard disk of the VM has been stored as `HTBVM01-000003.vmdk`.

After we've installed Arsenal Image Mounter, let's ensure we launch it with `administrative rights`. In the main window of Arsenal Image Mounter, let's click on the `Mount Disk Image` button. From there, we'll navigate to the location of our `.VMDK` file and select it.

![](https://i.imgur.com/Qw8lNZp.png)

Arsenal Image Mounter will then start its analysis of the VMDK file. We'll also have the choice to decide if we want to mount the disk as `read-only` or `read-write`, based on our specific requirements. 

*Choosing to mount a disk image as read-only is a foundational step in digital forensics and incident response. This approach is vital for preserving the original state of evidence, ensuring it's authenticity and integrity remain intact.*

Once mounted, the image will appear as a drive, assigned to the letter `D:\`.

![](https://i.imgur.com/yTOIRlU.png)
## Extracting Host-Based Evidence & Rapid Triage
### Host-Based Evidence

Modern operating systems, with Microsoft Windows becing a prime example, generate a plethora of evidence artifacts. These can arise from application execution, file modifications, or even the creation of user accounts. Each of these actions leaves behind a trail, providing valuable insights for incident response analysts. 

Evidence on a host system varies in its nature. The term `volatility` refers to the *persistence of data on a host system*, with volatile data being information that disappears after events such as logoffs or power shutdowns. Once crucial type of volatile evidence is the **system's active memory**. During investigations, especially those concerning malware infections, this live system memory becomes **indispensible**. Malware often leaves traces within system memory, and losing this evidence can hinder an analyst's investigation. To capture memory, tools like [FTK Imager](https://www.exterro.com/ftk-imager) are commonly employed.

Some other memory acquisition solutions are:

- [WinPmem](https://github.com/Velocidex/WinPmem): WinPmem has been the default open source memory acquisition driver for windows for a long time. It used to live in the Rekall project, but has recently been separated into its own repository.
- [DumpIt](https://www.magnetforensics.com/resources/magnet-dumpit-for-windows/): A simplistic utility that generates a physical memory dump of Windows and Linux machines. On Windows, it concatenates 32-bit and 64-bit system physical memory into a single output file, making it extremely easy to use.
- [MemDump](http://www.nirsoft.net/utils/nircmd.html): MemDump is a free, straightforward command-line utility that enables us to capture the contents of a system's RAM. It’s quite beneficial in forensics investigations or when analyzing a system for malicious activity. Its simplicity and ease of use make it a popular choice for memory acquisition.
- [Belkasoft RAM Capturer](https://belkasoft.com/ram-capturer): This is another powerful tool we can use for memory acquisition, provided free of charge by Belkasoft. It can capture the RAM of a running Windows computer, even if there's active anti-debugging or anti-dumping protection. This makes it a highly effective tool for extracting as much data as possible during a live forensics investigation.
- [Magnet RAM Capture](https://www.magnetforensics.com/resources/magnet-ram-capture/): Developed by Magnet Forensics, this tool provides a free and simple way to capture the volatile memory of a system.
- [LiME (Linux Memory Extractor)](https://github.com/504ensicsLabs/LiME): LiME is a Loadable Kernel Module (LKM) which allows the acquisition of volatile memory. LiME is unique in that it's designed to be transparent to the target system, evading many common anti-forensic measures.
### Example 1: Acquiring Memory with WinPmem

Let's now see a demonstration using `WinPmem` for memory acquisition.

To generate a memory dump, simple execute the command below with Administrator privileges.

```cmd
C:\Users\X\Downloads> winpmem_mini_x64_rc2.exe memdump.raw
```

![](https://i.imgur.com/bC8gr7y.png)
### Example 2: Acquiring VM Memory

Here are some steps to acquire memory from a Virtual Machine (VM).

1. Open the running VM's options
2. Suspend the running VM
3. Locate the `.vmem` file inside of the VM's directory.

![](https://i.imgur.com/Gau9m6T.png)
![](https://i.imgur.com/W5shmem.png)

On the other hand, non-volatile data remains on the hard drive, typically persisting through shutdowns. This category includes artifacts such as:

- Registry
- Windows Event Log
- System-related artifacts (e.g. Prefetch, Amache)
- Application-specific artifacts (e.g. IIS logs, Browser history)
### Rapid Triage

This approach emphasizes collecting data from potentially compromised systems. The goal is to centralize high-value data, streamlining its indexing and analysis. By centralizing this data, analysts can more effectively deploy tools and techniques, honing in on systems with the most evidentiary value. This targeted approach allows for a deeper dive into digital forensics, offering a clearer picture of the adversary's actions. 

One of the best, if not the best, rapid artifact parsing and extraction solutions is [KAPE (Kroll Artifact Parser and Extractor)](https://www.kroll.com/en/services/cyber-risk/incident-response-litigation-support/kroll-artifact-parser-extractor-kape). Let's see how we can employ `KAPE` to retrieve valuable forensic data from the image we previously mounted with the help of Arsenal Image Mounter (`D:\`).

`KAPE` is powerful tool in the realm of digital forensics and incident response. Designed to aid forensic experts and investigators, KAPE facilitates the collection and analysis of digital evidence from Windows-based systems. Developed and maintained by `Kroll` (previously known as `Magnet Forensics`), KAPE is celebrated for its comphensive collections features, adaptability, and intuitive interface. The diagram below illustrates KAPE's operational flow. 

![](https://i.imgur.com/K1uFjas.png)

Image reference: [https://ericzimmerman.github.io/KapeDocs/#!index.md](https://ericzimmerman.github.io/KapeDocs/#!index.md)

KAPE operates based on the principles of `Targets` and `Modules`. These elements guide the tool in processing data and extracting forensic artifacts. When we feed a source to KAPE, it duplicates specific forensic-related files to a designated output directory, all while maintaining the metadata of each file.

![](https://i.imgur.com/bTLbmG4.png)

After downloading, let's unzip the file and launch KAPE. Within the KAPE directory, we'll notice two executable files: `gkape.exe` and `kape.exe`. KAPE provides users with two modes: CLI (`kape.exe`) and GUI (`gkape.exe`).

![](https://i.imgur.com/0tBVOxn.png)

Let's opt for the GUI version to explore the available options more visually.

![](https://i.imgur.com/oFFVSGR.png)

The crux of the process lies in selecting the appropriate target configurations.

![](https://i.imgur.com/F7zfOPh.png)

In `KAPE`'s terminology, `Targets` refer to the specific artifacts we aim to extract from an image or system. These are then duplicated to the output directory. 

KAPE's target files have a `.tkape` extension and reside in the `<path to kape>\KAPE\Targets` directory. For instance, the target `RegistryHivesSystem.tkape` in the screenshot below specifies the locations and file masks associated with system-related registry hives. In this target configuration, `RegistryHiveSystem.tkape` contains information to collect the files with file mask `SAM.LOG*` from the `C:\Windows\System32\config` directory.

![](https://i.imgur.com/Eb4VTKw.png)

KAPE also offers `Compound Targets`, which are essentially amalgamations of multiple targets. This feature accelerates the collection process by gathering multiple files defined across various targets in a single run. The `Compound` directory's `KapeTriage` file provides an overview of the contents of this compound target. 

![](https://i.imgur.com/cZKWbuh.png)

Let's specify our source (in our scenario, it's `D:\`) and designate a location to store the harvested data. We can also determine an output folder to house the processed data from KAPE. 

After configuring our options, let's hit the `Execute` button to initiate the data collection.

![](https://i.imgur.com/CJ8D3wb.png)

Upon execution, KAPE will commence the collection, storing the results in the predetermined destination.

```shell-session
KAPE version 1.3.0.2, Author: Eric Zimmerman, Contact: https://www.kroll.com/kape (kape@kroll.com)

KAPE directory: C:\htb\dfir_module\data\kape\KAPE
Command line:   --tsource D: --tdest C:\htb\dfir_module\data\investigation\image --target !SANS_Triage --gui

System info: Machine name: REDACTED, 64-bit: True, User: REDACTED OS: Windows10 (10.0.22621)

Using Target operations
Found 18 targets. Expanding targets to file list...
Target ApplicationEvents with Id 2da16dbf-ea47-448e-a00f-fc442c3109ba already processed. Skipping!
Target ApplicationEvents with Id 2da16dbf-ea47-448e-a00f-fc442c3109ba already processed. Skipping!
Target ApplicationEvents with Id 2da16dbf-ea47-448e-a00f-fc442c3109ba already processed. Skipping!
Target ApplicationEvents with Id 2da16dbf-ea47-448e-a00f-fc442c3109ba already processed. Skipping!
Target ApplicationEvents with Id 2da16dbf-ea47-448e-a00f-fc442c3109ba already processed. Skipping!
Found 639 files in 4.032 seconds. Beginning copy...
  Deferring D:\Windows\System32\LogFiles\WMI\RtBackup\EtwRTDefenderApiLogger.etl due to UnauthorizedAccessException...
  Deferring D:\Windows\System32\LogFiles\WMI\RtBackup\EtwRTDefenderAuditLogger.etl due to UnauthorizedAccessException...
  Deferring D:\Windows\System32\LogFiles\WMI\RtBackup\EtwRTDiagLog.etl due to UnauthorizedAccessException...
  Deferring D:\Windows\System32\LogFiles\WMI\RtBackup\EtwRTDiagtrack-Listener.etl due to UnauthorizedAccessException...
  Deferring D:\Windows\System32\LogFiles\WMI\RtBackup\EtwRTEventLog-Application.etl due to UnauthorizedAccessException...
  Deferring D:\Windows\System32\LogFiles\WMI\RtBackup\EtwRTEventlog-Security.etl due to UnauthorizedAccessException...
  Deferring D:\Windows\System32\LogFiles\WMI\RtBackup\EtwRTEventLog-System.etl due to UnauthorizedAccessException...
  Deferring D:\Windows\System32\LogFiles\WMI\RtBackup\EtwRTSgrmEtwSession.etl due to UnauthorizedAccessException...
  Deferring D:\Windows\System32\LogFiles\WMI\RtBackup\EtwRTUBPM.etl due to UnauthorizedAccessException...
  Deferring D:\Windows\System32\LogFiles\WMI\RtBackup\EtwRTWFP-IPsec Diagnostics.etl due to UnauthorizedAccessException...
  Deferring D:\$MFT due to UnauthorizedAccessException...
  Deferring D:\$LogFile due to UnauthorizedAccessException...
  Deferring D:\$Extend\$UsnJrnl:$J due to NotSupportedException...
  Deferring D:\$Extend\$UsnJrnl:$Max due to NotSupportedException...
  Deferring D:\$Secure:$SDS due to NotSupportedException...
  Deferring D:\$Boot due to UnauthorizedAccessException...
  Deferring D:\$Extend\$RmMetadata\$TxfLog\$Tops:$T due to NotSupportedException...
Deferred file count: 17. Copying locked files...
  Copied deferred file D:\Windows\System32\LogFiles\WMI\RtBackup\EtwRTDefenderApiLogger.etl to C:\htb\dfir_module\data\investigation\image\D\Windows\System32\LogFiles\WMI\RtBackup\EtwRTDefenderApiLogger.etl. Hashing source file...
  Copied deferred file D:\Windows\System32\LogFiles\WMI\RtBackup\EtwRTDiagLog.etl to C:\htb\dfir_module\data\investigation\image\D\Windows\System32\LogFiles\WMI\RtBackup\EtwRTDiagLog.etl. Hashing source file...
  Copied deferred file D:\Windows\System32\LogFiles\WMI\RtBackup\EtwRTDiagtrack-Listener.etl to C:\htb\dfir_module\data\investigation\image\D\Windows\System32\LogFiles\WMI\RtBackup\EtwRTDiagtrack-Listener.etl. Hashing source file...
  Copied deferred file D:\Windows\System32\LogFiles\WMI\RtBackup\EtwRTEventLog-Application.etl to C:\htb\dfir_module\data\investigation\image\D\Windows\System32\LogFiles\WMI\RtBackup\EtwRTEventLog-Application.etl. Hashing source file...
  Copied deferred file D:\Windows\System32\LogFiles\WMI\RtBackup\EtwRTEventLog-System.etl to C:\htb\dfir_module\data\investigation\image\D\Windows\System32\LogFiles\WMI\RtBackup\EtwRTEventLog-System.etl. Hashing source file...
  Copied deferred file D:\$MFT to C:\htb\dfir_module\data\investigation\image\D\$MFT. Hashing source file...
  Copied deferred file D:\$LogFile to C:\htb\dfir_module\data\investigation\image\D\$LogFile. Hashing source file...
  Copied deferred file D:\$Extend\$UsnJrnl:$J to C:\htb\dfir_module\data\investigation\image\D\$Extend\$J. Hashing source file...
  Copied deferred file D:\$Extend\$UsnJrnl:$Max to C:\htb\dfir_module\data\investigation\image\D\$Extend\$Max. Hashing source file...
  Copied deferred file D:\$Secure:$SDS to C:\htb\dfir_module\data\investigation\image\D\$Secure_$SDS. Hashing source file...
  Copied deferred file D:\$Boot to C:\htb\dfir_module\data\investigation\image\D\$Boot. Hashing source file...
```

The output directory of KAPE houses the fruits of the artifact collection and processing. The exact contents of this directory can differ based on the artifacts and the configurations set. In our demonstration, we opted for the `!SANS_Triage` configuration. Let's navigate the KAPE's output directory to inspect the harvested data.

![](https://i.imgur.com/tMYMIaL.png)

From the displayed results. it's evident that the `$MFT` file has been collected, along with the `Users` and `Windows` directories.

It's worth noting that KAPE has also harvested the `Windows event logs`, which are nestled within the Windows directory sub-folders.

![](https://i.imgur.com/AF8oJdk.png)

What if we wanted to perform artifact collection remotely and en masse? This is where EDR solutions and [Velociraptor](https://github.com/Velocidex/velociraptor) come into play.

**Endpoint Detection and Response (EDR)** platforms offer a significant advantage for incident response analysts. They enable acquisition of digital evidence. For instance, EDR can display *recently executed binaries* or *newly added files*. Instead of sifting through individual systems, analysts can search for such indicators across the entire network. Another benefit is the capability to gather evidence, be it specific files or comprehensive forensic packages. This functionality expedites evidence collection and facilitates large-scale searching and collection.

[Velociraptor](https://github.com/Velocidex/velociraptor) is a potent tool for gathering host-based information using Velociraptor Query Language (VQL) queries. Beyond this, Velociraptor can execute `Hunts` to amass various artifacts. A frequently utilized artifact is the `Windows.KapeFiles.Targets`. While KAPE (Kroll Artifact Parser and Extractor) itself isn't open-source, its file collection logic, encoded in YAML, is accessible via the [KapeFiles project](https://github.com/EricZimmerman/KapeFiles). This approach is a staple in Rapid Triage.

To utilize Velociraptor for KapeFiles artifacts:

- Initiate a new Hunt.

![](https://i.imgur.com/ONYzJxW.png)

- Choose `Windows.KapeFiles.Targets` as the artifacts for collection.

![](https://i.imgur.com/zi8CQFE.png)

- Specify the collection to use.

![](https://i.imgur.com/OuqjpPa.png)

![](https://i.imgur.com/BqhATYi.png)

> - Click on `Launch` to start the hunt.

![](https://i.imgur.com/vjD5sYS.png)

> - Once completed, download the results.

![](https://i.imgur.com/Se6FfrB.png)

Extracting the archive will reveal files related to the collected artifacts and all gathered files.

![](https://i.imgur.com/LRi2SJn.png)

![](https://i.imgur.com/OPhFU9O.png)

For remote memory dump collection using Velociraptor:

> - Start a new hunt, but this time, select the `Windows.Memory.Acquisition` artifact.

![](https://i.imgur.com/EMLzzES.png)

> - After the hunt concludes, download the resulting archive, Within, you'll find a file named `PhysicalMemory.raw`, containing the memory dump. 

![](https://i.imgur.com/oKcUIpe.png)
## Extracting Network Evidence

Throughout our exploration of the modules in the `SOC Analyst` path, we've delved extensively into the realm of network evidence, a fundamental aspect for any SOC Analyst. 

- First up, our `Intro to Network Traffic Analysis` and `Intermediate Network Traffic Analysis` modules covered `traffic capture analysis`. Think if traffic capture as a **snapshot of all the digital conversations happening in our network.** Tools like `Wireshark` and `tcpdump` allow us to capture and dissect these packets, giving us a granular view of data in transit.

- Then, our `Working with IDS/IPS` and `Detecting Windows Attacks with Splunk` modules covered the usage of IDS/IPS-derived data. `Intrusion Detection Systems (IDS)` are our watchful sentinels, constantly monitoring network traffic for signs of malicious activity. When they spot something amiss, they alert us. On the other hand, `Intrusion Detection Systems (IPS)` take it a step further. Not only do they detect, but they also take pre-defined actions to block or prevent those malicious activities. 

- `Traffic Flow` data, often sourced from tools like `NetFlow` or `sFlow`, provides us with a broader view of our network's behavior. While it might not give us the nitty-gritty details of each packet, it offers a high level overview of traffic patterns. 

- Lastly, our trusty `firewalls`. These are not just barriers that block or allow traffic based on predefined rules. Modern firewalls are *intelligent beasts*. They can identify applications, users and even detect and block threats. By analyzing firewall logs, we can uncover attempts to exploit vulnerabilities, unauthorized access attempts, and other malicious activities.
# Memory Forensics
## Memory Forensics Definition & Process

`Memory Forensics`, also known as volatile memory analysis, is a specialized branch of digital forensics that focuses on the **examination and analysis of the volatile memory (RAM)** of a computer or digital device. Unlike traditional digital forensics, which involves analyzing data stored on non-volatile storage media like hard drives or solid-state drives, memory forensics deals with the live state of a system at a particular moment in time.

Here are some types of data found in RAM that are valuable for incident investigation.

- `Network Connections`
- `File Handles and Open Files`
- `Open Registry Keys`
- `Running Processes on the system`
- `Loaded Modules`
- `Loaded Device Drivers`
- `Command History and Console Sessions`
- `Kernel Data Structures`
- `User and Credential Information`
- `Malware Artifacts`
- `System Configuration`
- `Process Memory Regions`

As we discussed both in the previous section and in the `YARA & Sigma for SOC Analysts` module, when malware operates, it often leaves traces or footprints in a system's active memory. By analyzing this memory, investigators can uncover malicious processes, identify indicators of compromise, and reconstruct the malware's actions.

It should be noted that in some cases, important data or encryption keys may reside in memory. Memory forensics can help recover this data, which may be crucial for an investigation.

The following outlines a *systematic approach to memory forensics*, formulated to aid in in-memory investigations and drawing inspiration from [SANS](https://www.sans.org/)'s six-step memory forensics methodology.

1. `Process Identification and Verification`: Let's begin by identifying all active processes. Malicious software often masquerades as legitimate processes, sometimes with subtle name variations to avoid detection. We need to:

	- Enumerate all running processes.
	- Determine their origin within the operating system.
	- Cross-reference with known legitimate processes.
	- Highlight any discrepancies or suspicious naming conventions.

2. `Deep Dive into Process Components`: Once we've flagged potentially rogue processes, our next step is to scrutinize the associated Dynamic Link Libraries (DLLs) and handles. Malware often exploits DLLs to conceal it's activities. We should:

	- Examine DLLs linked to the suspicious activity. 
	- Check for unauthorized or malicious DLLs.
	- Investigate any signs of DLL injection or hijacking.

3. `Network Activity Analysis`: Many malware strains, especially those that operate in stages, necessitate internet connectivity. They might beacon to Command and Control (C2) servers or exfiltrate data. To uncover these:

	- Review active and passive network connections in the system's memory. 
	- Identify and document external IP addresses and associated domains.
	- Determine the nature and purpose of the communication.
		- Validate the process' legitimacy
		- Assess if the process typically requires network communication
		- Trace back to the parent process
		- Evaluate its behavior and necessity

4. `Code Injection Detection`: Advanced adversaries often employ techniques like process hollowing or utilize unmapped memory sections. To counter this, we could:

	- Use memory analysis tools to detect anomalies or signs of these techniques.
	- Identify any processes that seem to occupy unusual memory spaces or exhibit unexpected behaviors.

5. `Rootkit Discovery`: Achieving stealth and persistence is a common goal for adversaries. Rootkits, which embed deep within the OS, grant threat actors continuous, often elevated, system access while evading detection. To tackle this:

	- Scan for signs of rootkit activity or deep OS alterations.
	- Identify any processes or drivers operating at unusually high privileges or exhibiting stealth behaviors.

6. `Extraction of Suspicious Elements`: After pinpointing suspicious processes, drivers, or executables, we need to isolate them for in-depth analysis. This involves:

	- Dumping the suspicious components from memory.
	- Storing them securely for subsequent examination using specialized forensic tools.

---
## The Volatility Framework

> [!Important] Links
>  [[Volatility]]

The preferred tool for conducting memory forensics is [Volatility](https://www.volatilityfoundation.org/releases). Volatility is a leading open-soure memory forensics framework. At the heart of this framework lies the Volatility Python Script. This script harnesses a plethora of plugins, enabling it to dissect memory images with precision. 

Given it's Python foundation, we can execute Volatility on any platform that's Python compatible. Moreover, our team can leverage Volatility to scrutinize memory image files from a broad spectrum of widely-used operating systems. This includes Windows, spanning from Windows XP to Windows Server 2016, macOS, and of course, prevalent Linux distributions. 

Volatility modules or plugins are extensions or add-ons that enhance the functionality of the Volatility Framework by extracting specific information or perform specific analysis on memory images.

Some commonly used modules are:

- `pslist`: List the running processes
- `cmdline`: Displays the process command-line arguments
- `netscan`: Scans for network connections and open ports
- `malfind`: Scans for potentially malicious code injected into processes.
- `handles`: Scans for open handles
- `svcscan`: Lists Windows services
- `dlllist`: Lists loaded DLLs (Dynamic Link Libraries) in a process.
- `hivelist`: Lists the registry hives in memory.

Volatility offers extensive documentation. You can find modules and their associated documentation using the following links:

- **Volatility v2**: [https://github.com/volatilityfoundation/volatility/wiki/Command-Reference](https://github.com/volatilityfoundation/volatility/wiki/Command-Reference)
- **Volatility v3**: [https://volatility3.readthedocs.io/en/latest/index.html](https://volatility3.readthedocs.io/en/latest/index.html)

A useful Volatility (v2 & v3) cheatsheet can be found here: [https://blog.onfvp.com/post/volatility-cheatsheet/](https://blog.onfvp.com/post/volatility-cheatsheet/)

---
### Volatility v2 Fundamentals

> [!NOTE]
> Let's now navigate to the bottom of this section and click on "Click here to spawn the target system!". Then, let's SSH into the Target IP using the provided credentials. The vast majority of the actions/commands covered from this point up to end of this section can be replicated inside the target, offering a more comprehensive grasp of the topics presented.

Let's now see a demonstration of utilizing `Volatility v2` to analyze a memory dump saved as `Win7-2515534d.vmem` inside the `/home/htb/student/MemoryDumps` directory of this target.

Volatility's `help` section and `available plugins` can be seen as follows.

```shell-session
trop3n@htb[/htb]$ vol.py --help
Volatility Foundation Volatility Framework 2.6.1
/usr/local/lib/python2.7/dist-packages/volatility/plugins/community/YingLi/ssh_agent_key.py:12: CryptographyDeprecationWarning: Python 2 is no longer supported by the Python core team. Support for it is now deprecated in cryptography, and will be removed in the next release.
  from cryptography.hazmat.backends.openssl import backend
Usage: Volatility - A memory forensics analysis platform.

Options:
  -h, --help            list all available options and their default values.
                        Default values may be set in the configuration file
                        (/etc/volatilityrc)
  --conf-file=/home/htb-student/.volatilityrc
                        User based configuration file
  -d, --debug           Debug volatility
  --plugins=PLUGINS     Additional plugin directories to use (colon separated)
  --info                Print information about all registered objects
  --cache-directory=/home/htb-student/.cache/volatility
                        Directory where cache files are stored
  --cache               Use caching
  --tz=TZ               Sets the (Olson) timezone for displaying timestamps
                        using pytz (if installed) or tzset
  -C 190000, --confsize=190000
                        Config data size
  -Y YARAOFFSET, --yaraoffset=YARAOFFSET
                        YARA start offset
  -f FILENAME, --filename=FILENAME
                        Filename to use when opening an image
  --profile=WinXPSP2x86
                        Name of the profile to load (use --info to see a list
                        of supported profiles)
  -l LOCATION, --location=LOCATION
                        A URN location from which to load an address space
  -w, --write           Enable write support
  --dtb=DTB             DTB Address
  --physical_shift=PHYSICAL_SHIFT
                        Linux kernel physical shift address
  --virtual_shift=VIRTUAL_SHIFT
                        Linux kernel virtual shift address
  --shift=SHIFT         Mac KASLR shift address
  --output=text         Output in this format (support is module specific, see
                        the Module Output Options below)
  --output-file=OUTPUT_FILE
                        Write output in this file
  -v, --verbose         Verbose information
  -g KDBG, --kdbg=KDBG  Specify a KDBG virtual address (Note: for 64-bit
                        Windows 8 and above this is the address of
                        KdCopyDataBlock)
  --force               Force utilization of suspect profile
  -k KPCR, --kpcr=KPCR  Specify a specific KPCR address
  --cookie=COOKIE       Specify the address of nt!ObHeaderCookie (valid for
                        Windows 10 only)

        Supported Plugin Commands:

                agtidconfig     Parse the Agtid configuration
                amcache         Print AmCache information
                antianalysis
                apifinder
                apihooks        Detect API hooks in process and kernel memory
                apihooksdeep    Detect API hooks in process and kernel memory, with ssdeep for whitelisting
                apt17scan       Detect processes infected with APT17 malware
                atoms           Print session and window station atom tables
                atomscan        Pool scanner for atom tables
                attributeht     Find Hacking Team implants and attempt to attribute them using a watermark.
                auditpol        Prints out the Audit Policies from HKLM\SECURITY\Policy\PolAdtEv
                autoruns        Searches the registry and memory space for applications running at system startup and maps them to running processes
                bigpools        Dump the big page pools using BigPagePoolScanner
                bioskbd         Reads the keyboard buffer from Real Mode memory
                bitlocker       Extract Bitlocker FVEK. Supports Windows 7 - 10.
                cachedump       Dumps cached domain hashes from memory
                callbacks       Print system-wide notification routines
                callstacks      this is the plugin class for callstacks
                chromecookies   Scans for and parses potential Chrome cookie data
                chromedownloadchains    Scans for and parses potential Chrome download chain records
                chromedownloads Scans for and parses potential Chrome download records
                chromehistory   Scans for and parses potential Chrome url history
                chromesearchterms       Scans for and parses potential Chrome keyword search terms
                chromevisits    Scans for and parses potential Chrome url visits data -- VERY SLOW, see -Q option
                clipboard       Extract the contents of the windows clipboard
                cmdline         Display process command-line arguments
                cmdscan         Extract command history by scanning for _COMMAND_HISTORY
                connections     Print list of open connections [Windows XP and 2003 Only]
                connscan        Pool scanner for tcp connections
                consoles        Extract command history by scanning for _CONSOLE_INFORMATION
                crashinfo       Dump crash-dump information
                derusbiconfig   Parse the Derusbi configuration
                deskscan        Poolscaner for tagDESKTOP (desktops)
                devicetree      Show device tree
                directoryenumerator     Enumerates all unique directories from FileScan
                dlldump         Dump DLLs from a process address space
                dlllist         Print list of loaded dlls for each process
                driverbl        Scans memory for driver objects and compares the results with the baseline image
                driverirp       Driver IRP hook detection
                driveritem
                drivermodule    Associate driver objects to kernel modules
                driverscan      Pool scanner for driver objects
                dumpcerts       Dump RSA private and public SSL keys
                dumpfiles       Extract memory mapped and cached files
                dumpregistry    Dumps registry files out to disk
                dyrescan        Extract Dyre Configuration from processes
                editbox         Displays information about Edit controls. (Listbox experimental.)
                envars          Display process environment variables
                eventhooks      Print details on windows event hooks
                evtlogs         Extract Windows Event Logs (XP/2003 only)
                facebook        Retrieve facebook artifacts from a memory image
                facebookcontacts        Finds possible Facebook contacts
                facebookgrabinfo        Carves the memory dump for Owner's personal info JSON struct.
                facebookmessages        Carves the memory for every message exchanged between the Owner and another contact
                fileitem
                filescan        Pool scanner for file objects
                firefoxcookies  Scans for and parses potential Firefox cookies (cookies.sqlite moz_cookies table
                firefoxdownloads        Scans for and parses potential Firefox download records -- downloads.sqlite moz_downloads table pre FF26 only
                firefoxhistory  Scans for and parses potential Firefox url history (places.sqlite moz_places table)
                fwhooks         Enumerates modules which are using Firewall Hook Drivers on Windows 2000/XP/2003
                gahti           Dump the USER handle type information
                gditimers       Print installed GDI timers and callbacks
                gdt             Display Global Descriptor Table
                getservicesids  Get the names of services in the Registry and return Calculated SID
                getsids         Print the SIDs owning each process
                ghostrat        Detects and decrypts Gh0stRat communication
                handles         Print list of open handles for each process
                hashdump        Dumps passwords hashes (LM/NTLM) from memory
                hibinfo         Dump hibernation file information
                hikitconfig     Parse the Hikit configuration
                hivedump        Prints out a hive
                hivelist        Print list of registry hives.
                hivescan        Pool scanner for registry hives
                hollowfind      Detects different types of Process Hollowing
                hookitem
                hpakextract     Extract physical memory from an HPAK file
                hpakinfo        Info on an HPAK file
                hpv_clipboard   Dump Virtual Machine Clipboard data
                hpv_vmconnect   Virtual Machine Console data
                hpv_vmwp        Display the Virtual Machine Process GUID for each running vm
                idt             Display Interrupt Descriptor Table
                idxparser       Scans for and parses Java IDX files
                iehistory       Reconstruct Internet Explorer cache / history
                imagecopy       Copies a physical address space out as a raw DD image
                imageinfo       Identify information for the image
                impscan         Scan for calls to imported functions
                indx            Scans for and parses potential INDX entries
                joblinks        Print process job link information
                kdbgscan        Search for and dump potential KDBG values
                kpcrscan        Search for and dump potential KPCR values
                lastpass        Extract lastpass data from process.
                ldrmodules      Detect unlinked DLLs
                linuxgetprofile Scan to try to determine the Linux profile
                logfile         Scans for and parses potential $Logfile entries
                lsadump         Dump (decrypted) LSA secrets from the registry
                machoinfo       Dump Mach-O file format information
                malfind         Find hidden and injected code
                malfinddeep     Find hidden and injected code, whitelist with ssdeep hashes
                malfofind       Find indications of process hollowing/RunPE injections
                malprocfind     Finds malicious processes based on discrepancies from observed, normal behavior and properties
                malthfind       Find malicious threads by analyzing their callstack
                mbrparser       Scans for and parses potential Master Boot Records (MBRs)
                memdump         Dump the addressable memory for a process
                memmap          Print the memory map
                messagehooks    List desktop and thread window message hooks
                mftparser       Scans for and parses potential MFT entries
                mimikatz        mimikatz offline
                moddump         Dump a kernel driver to an executable file sample
                modscan         Pool scanner for kernel modules
                modules         Print list of loaded modules
                msdecompress    Carves and dumps Lznt1, Xpress and Xpress huffman Compressioned data blocks in a processes pagespace
                multiscan       Scan for various objects at once
                mutantscan      Pool scanner for mutex objects
                ndispktscan     Extract the packets from memory
                networkpackets  Carve and analyze ARP/IPv4 network packets from memory
                notepad         List currently displayed notepad text
                objtypescan     Scan for Windows object type objects
                openioc_scan    Scan OpenIOC 1.1 based indicators
                openvpn         Extract OpenVPN client credentials (username, password) cached in memory.
                osint           Check Url/ip extracted from memory against opensource intelligence platforms
                patcher         Patches memory based on page scans
                plugxconfig     Locate and parse the PlugX configuration
                plugxscan       Detect processes infected with PlugX
                poolpeek        Configurable pool scanner plugin
                prefetchparser  Scans for and parses potential Prefetch files
                printkey        Print a registry key, and its subkeys and values
                privs           Display process privileges
                procdump        Dump a process to an executable file sample
                processbl       Scans memory for processes and loaded DLLs and compares the results with the baseline
                profilescan     Scan for executables to try to determine the underlying OS
                psinfo          Displays process related information and suspicious memory regions
                pslist          Print all running processes by following the EPROCESS lists
                psscan          Pool scanner for process objects
                pstotal         Combination of pslist,psscan & pstree --output=dot gives graphical representation
                pstree          Print process list as a tree
                psxview         Find hidden processes with various process listings
                qemuinfo        Dump Qemu information
                raw2dmp         Converts a physical memory sample to a windbg crash dump
                registryitem
                rsakey          Extract base64/PEM encoded private RSA keys from physical memory.
                screenshot      Save a pseudo-screenshot based on GDI windows
                servicebl       Scans memory for service objects and compares the results with the baseline image
                servicediff     List Windows services (ala Plugx)
                serviceitem
                sessions        List details on _MM_SESSION_SPACE (user logon sessions)
                shellbags       Prints ShellBags info
                shimcache       Parses the Application Compatibility Shim Cache registry key
                shimcachemem    Parses the Application Compatibility Shim Cache stored in kernel memory
                shutdowntime    Print ShutdownTime of machine from registry
                sockets         Print list of open sockets
                sockscan        Pool scanner for tcp socket objects
                ssdeepscan      Scan process or kernel memory with SSDeep signatures
                ssdt            Display SSDT entries
                strings         Match physical offsets to virtual addresses (may take a while, VERY verbose)
                svcscan         Scan for Windows services
                symlinkscan     Pool scanner for symlink objects
                systeminfo      Print common system details of machine from registry
                thrdscan        Pool scanner for thread objects
                threads         Investigate _ETHREAD and _KTHREADs
                timeliner       Creates a timeline from various artifacts in memory
                timers          Print kernel timers and associated module DPCs
                truecryptmaster Recover TrueCrypt 7.1a Master Keys
                truecryptpassphrase     TrueCrypt Cached Passphrase Finder
                truecryptsummary        TrueCrypt Summary
                trustrecords    Extract MS Office TrustRecords from the Registry
                twitter         Retrieve twitter artifacts from a memory image
                uninstallinfo   Extract installed software info from Uninstall registry key
                unloadedmodules Print list of unloaded modules
                usbstor         Parse USB Data from the Registry
                userassist      Print userassist registry keys and information
                userhandles     Dump the USER handle tables
                usnjrnl         Scans for and parses potential USNJRNL entries
                usnparser       Scans for and parses USN journal records
                vaddump         Dumps out the vad sections to a file
                vadinfo         Dump the VAD info
                vadtree         Walk the VAD tree and display in tree format
                vadwalk         Walk the VAD tree
                vboxinfo        Dump virtualbox information
                verinfo         Prints out the version information from PE images
                vmwareinfo      Dump VMware VMSS/VMSN information
                volshell        Shell in the memory image
                windows         Print Desktop Windows (verbose details)
                wintree         Print Z-Order Desktop Windows Tree
                wndscan         Pool scanner for window stations
                yarascan        Scan process or kernel memory with Yara signatures 
```
### Identifying the Profile

Profiles are essential for Volatility v2 to interpret the memory data correctly (profile identification has been enhanced in v3). To determine the profile that matches the operating system of the memory dump we can use the `imageinfo` plugin as follows.

```shell-session
trop3n@htb[/htb]$ vol.py -f /home/htb-student/MemoryDumps/Win7-2515534d.vmem imageinfo                                                                   Volatility Foundation Volatility Framework 2.6.1
/usr/local/lib/python2.7/dist-packages/volatility/plugins/community/YingLi/ssh_agent_key.py:12: CryptographyDeprecationWarning: Python 2 is no longer supported by the Python core team. Support for it is now deprecated in cryptography, and will be removed in the next release.
  from cryptography.hazmat.backends.openssl import backend
INFO    : volatility.debug    : Determining profile based on KDBG search...
         Suggested Profile(s) : Win7SP1x64, Win7SP0x64, Win2008R2SP0x64, Win2008R2SP1x64_24000, Win2008R2SP1x64_23418, Win2008R2SP1x64, Win7SP1x64_24000, Win7SP1x64_23418
                     AS Layer1 : WindowsAMD64PagedMemory (Kernel AS)
                     AS Layer2 : FileAddressSpace (/home/htb-student/MemoryDumps/Win7-2515534d.vmem)
                      PAE type : No PAE
                           DTB : 0x187000L
                          KDBG : 0xf80002be9120L
          Number of Processors : 1
     Image Type (Service Pack) : 1
                KPCR for CPU 0 : 0xfffff80002beb000L
             KUSER_SHARED_DATA : 0xfffff78000000000L
           Image date and time : 2023-06-22 12:34:03 UTC+0000
     Image local date and time : 2023-06-22 18:04:03 +0530
```
### Identifying Running Processes

Let's see if the suggested `Win7SP1x64` profile is correct by trying to list running processes via the `pslist` plugin.

```shell-session
trop3n@htb[/htb]$ vol.py -f /home/htb-student/MemoryDumps/Win7-2515534d.vmem --profile=Win7SP1x64 pslist
Volatility Foundation Volatility Framework 2.6.1
/usr/local/lib/python2.7/dist-packages/volatility/plugins/community/YingLi/ssh_agent_key.py:12: CryptographyDeprecationWarning: Python 2 is no longer supported by the Python core team. Support for it is now deprecated in cryptography, and will be removed in the next release.
  from cryptography.hazmat.backends.openssl import backend
Offset(V)          Name                    PID   PPID   Thds     Hnds   Sess  Wow64 Start                          Exit
------------------ -------------------- ------ ------ ------ -------- ------ ------ ------------------------------ ------------------------------
0xfffffa8000ca8860 System                    4      0     97      446 ------      0 2023-06-22 12:04:39 UTC+0000
0xfffffa8001a64920 smss.exe                264      4      2       29 ------      0 2023-06-22 12:04:39 UTC+0000
0xfffffa80028a39a0 csrss.exe               352    344      8      626      0      0 2023-06-22 12:04:40 UTC+0000
0xfffffa8002a51730 wininit.exe             404    344      3       76      0      0 2023-06-22 12:04:41 UTC+0000
0xfffffa800291eb00 csrss.exe               416    396      9      307      1      0 2023-06-22 12:04:41 UTC+0000
0xfffffa8002a86340 winlogon.exe            464    396      3      113      1      0 2023-06-22 12:04:41 UTC+0000
0xfffffa8002ad8b00 services.exe            508    404      8      226      0      0 2023-06-22 12:04:41 UTC+0000
0xfffffa8002adbb00 lsass.exe               516    404      6      585      0      0 2023-06-22 12:04:41 UTC+0000
0xfffffa8002ae6b00 lsm.exe                 524    404      9      149      0      0 2023-06-22 12:04:41 UTC+0000
0xfffffa8002b4f720 svchost.exe             628    508     10      366      0      0 2023-06-22 12:04:42 UTC+0000
0xfffffa8002b7bb00 svchost.exe             696    508      7      288      0      0 2023-06-22 12:04:42 UTC+0000
0xfffffa8002ba0b00 svchost.exe             744    508     18      455      0      0 2023-06-22 12:04:42 UTC+0000
0xfffffa8002c00280 svchost.exe             868    508     19      443      0      0 2023-06-22 12:04:43 UTC+0000
0xfffffa8002c52710 svchost.exe             920    508     17      599      0      0 2023-06-22 12:04:43 UTC+0000
0xfffffa8002c5c680 svchost.exe             964    508     28      838      0      0 2023-06-22 12:04:43 UTC+0000
0xfffffa80022679b0 svchost.exe            1000    508     13      365      0      0 2023-06-22 12:04:44 UTC+0000
0xfffffa8002d15b00 spoolsv.exe            1120    508     13      273      0      0 2023-06-22 12:04:45 UTC+0000
0xfffffa8002d4f9b0 svchost.exe            1156    508     18      308      0      0 2023-06-22 12:04:45 UTC+0000
0xfffffa8002d2f060 svchost.exe            1268    508     11      165      0      0 2023-06-22 12:04:45 UTC+0000
0xfffffa8002d2d060 svchost.exe            1348    508     15      258      0      0 2023-06-22 12:04:45 UTC+0000
0xfffffa8000d78b00 VGAuthService.         1412    508      4       96      0      0 2023-06-22 12:04:45 UTC+0000
0xfffffa8002db6b00 vm3dservice.ex         1440    508      4       61      0      0 2023-06-22 12:04:46 UTC+0000
0xfffffa8002e2e9b0 vmtoolsd.exe           1468    508     13      299      0      0 2023-06-22 12:04:46 UTC+0000
0xfffffa8002e45a70 vm3dservice.ex         1488   1440      2       45      1      0 2023-06-22 12:04:46 UTC+0000
0xfffffa8002f58b00 svchost.exe            1724    508      6       92      0      0 2023-06-22 12:04:47 UTC+0000
0xfffffa8002fa2b00 WmiPrvSE.exe           1908    628      9      197      0      0 2023-06-22 12:04:47 UTC+0000
0xfffffa8002f8fb00 dllhost.exe            1968    508     13      190      0      0 2023-06-22 12:04:47 UTC+0000
0xfffffa8003007b00 msdtc.exe              1960    508     12      145      0      0 2023-06-22 12:04:51 UTC+0000
0xfffffa8001bfbb00 taskhost.exe           2432    508      9      241      1      0 2023-06-22 12:05:13 UTC+0000
0xfffffa80027ca970 dwm.exe                2484    868      5      152      1      0 2023-06-22 12:05:13 UTC+0000
0xfffffa8001d27b00 explorer.exe           2508   2472     24      843      1      0 2023-06-22 12:05:13 UTC+0000
0xfffffa80123fc590 vmtoolsd.exe           2600   2508      8      182      1      0 2023-06-22 12:05:14 UTC+0000
0xfffffa80027edb00 SearchIndexer.         2756    508     17      800      0      0 2023-06-22 12:05:22 UTC+0000
0xfffffa80023e7750 cmd.exe                3040   2508      1       21      1      0 2023-06-22 12:05:39 UTC+0000
0xfffffa8001d19060 conhost.exe            3048    416      2       53      1      0 2023-06-22 12:05:39 UTC+0000
0xfffffa8002d95870 taskmgr.exe            2648    464      6      113      1      0 2023-06-22 12:05:59 UTC+0000
0xfffffa8000e0fb00 ProcessHacker.          716   2508      9      476      1      0 2023-06-22 12:06:29 UTC+0000
0xfffffa8000eee060 sppsvc.exe             1080    508      4      146      0      0 2023-06-22 12:06:47 UTC+0000
0xfffffa8000ea6a00 svchost.exe             608    508     15      431      0      0 2023-06-22 12:06:47 UTC+0000
0xfffffa8000e2e620 wmpnetwk.exe           2968    508     18      442      0      0 2023-06-22 12:06:48 UTC+0000
0xfffffa80022af430 ida64.exe              2248   2508      7      340      1      0 2023-06-22 12:16:18 UTC+0000
0xfffffa8001420300 x32dbg.exe             2820   2508     20      480      1      1 2023-06-22 12:23:34 UTC+0000
0xfffffa8000ee96d0 Ransomware.wan         1512   2820     11      167      1      1 2023-06-22 12:23:41 UTC+0000
0xfffffa8002ca4240 Ransomware.wan         2320    508    117      497      0      1 2023-06-22 12:30:19 UTC+0000
0xfffffa8002ad9560 dllhost.exe            1876    628      4       79      1      0 2023-06-22 12:30:20 UTC+0000
0xfffffa8001d0f8b0 tasksche.exe           2972   1512      0 --------      1      0 2023-06-22 12:31:13 UTC+0000   2023-06-22 12:31:43 UTC+0000
0xfffffa8001d22b00 tasksche.exe           1792   1044      8       82      0      1 2023-06-22 12:31:13 UTC+0000
0xfffffa8002fa3060 SearchProtocol          852   2756      8      289      0      0 2023-06-22 12:31:15 UTC+0000
0xfffffa8002572060 @WanaDecryptor         1060   1792      2       71      0      1 2023-06-22 12:31:27 UTC+0000
0xfffffa8001568060 taskhsvc.exe           3012   1060      4      101      0      1 2023-06-22 12:31:29 UTC+0000
0xfffffa8001ddb060 conhost.exe            2348    352      1       32      0      0 2023-06-22 12:31:29 UTC+0000
0xfffffa8000df81b0 VSSVC.exe               288    508      6      116      0      0 2023-06-22 12:31:43 UTC+0000
0xfffffa800141e9a0 @WanaDecryptor         3252   3212      1       75      1      1 2023-06-22 12:31:45 UTC+0000
0xfffffa80014e4a70 MpCmdRun.exe           3436   3412      5      116      0      0 2023-06-22 12:32:12 UTC+0000
0xfffffa80014c12c0 SearchFilterHo         3904   2756      6      109      0      0 2023-06-22 12:33:18 UTC+0000
0xfffffa8000f2f1c0 audiodg.exe            4048    744      6      128      0      0 2023-06-22 12:33:33 UTC+0000
0xfffffa8000dbc5a0 cmd.exe                2080   1468      0 --------      0      0 2023-06-22 12:34:03 UTC+0000   2023-06-22 12:34:03 UTC+0000
0xfffffa8000f90b00 conhost.exe            3292    352      0 --------      0      0 2023-06-22 12:34:03 UTC+0000   2023-06-22 12:34:03 UTC+0000
0xfffffa8000f7b790 ipconfig.exe           2360   2080      0 --------      0      0 2023-06-22 12:34:03 UTC+0000   2023-06-22 12:34:03 UTC+0000
```

It should be noted that even if we specify another profile from the suggested list Volatility may still provide us with the correct output.
### Identifying Network Artifacts

The `netscan` plugin can be used to scan for network artifacts as follows:

```shell-session
trop3n@htb[/htb]$ vol.py -f /home/htb-student/MemoryDumps/Win7-2515534d.vmem --profile=Win7SP1x64 netscan
Volatility Foundation Volatility Framework 2.6.1
/usr/local/lib/python2.7/dist-packages/volatility/plugins/community/YingLi/ssh_agent_key.py:12: CryptographyDeprecationWarning: Python 2 is no longer supported by the Python core team. Support for it is now deprecated in cryptography, and will be removed in the next release.
  from cryptography.hazmat.backends.openssl import backend
Offset(P)          Proto    Local Address                  Foreign Address      State            Pid      Owner          Created
0x1a15caa0         UDPv4    0.0.0.0:3702                   *:*                                   1348     svchost.exe    2023-06-22 12:05:10 UTC+0000
0x1a15caa0         UDPv6    :::3702                        *:*                                   1348     svchost.exe    2023-06-22 12:05:10 UTC+0000
0x1fd7cac0         TCPv4    0.0.0.0:49155                  0.0.0.0:0            LISTENING        508      services.exe
0x1fd7cac0         TCPv6    :::49155                       :::0                 LISTENING        508      services.exe
0x3da01a70         UDPv4    0.0.0.0:3702                   *:*                                   1348     svchost.exe    2023-06-22 12:05:10 UTC+0000
0x3da0b130         UDPv4    0.0.0.0:0                      *:*                                   1000     svchost.exe    2023-06-22 12:05:02 UTC+0000
0x3da0b130         UDPv6    :::0                           *:*                                   1000     svchost.exe    2023-06-22 12:05:02 UTC+0000
0x3dcf1010         UDPv4    0.0.0.0:62718                  *:*                                   1348     svchost.exe    2023-06-22 12:04:46 UTC+0000
0x3dcf15b0         UDPv4    0.0.0.0:62719                  *:*                                   1348     svchost.exe    2023-06-22 12:04:46 UTC+0000
0x3dcf15b0         UDPv6    :::62719                       *:*                                   1348     svchost.exe    2023-06-22 12:04:46 UTC+0000
0x3da15010         TCPv4    0.0.0.0:49156                  0.0.0.0:0            LISTENING        516      lsass.exe
0x3da15010         TCPv6    :::49156                       :::0                 LISTENING        516      lsass.exe
0x3dc69860         TCPv4    0.0.0.0:5357                   0.0.0.0:0            LISTENING        4        System
0x3dc69860         TCPv6    :::5357                        :::0                 LISTENING        4        System
0x3dca3ee0         TCPv4    0.0.0.0:49154                  0.0.0.0:0            LISTENING        964      svchost.exe
0x3dca3ee0         TCPv6    :::49154                       :::0                 LISTENING        964      svchost.exe
0x3dcf7280         TCPv4    0.0.0.0:49155                  0.0.0.0:0            LISTENING        508      services.exe
0x3dd07540         TCPv4    0.0.0.0:445                    0.0.0.0:0            LISTENING        4        System
0x3dd07540         TCPv6    :::445                         :::0                 LISTENING        4        System
0x3e5f7cd0         UDPv4    0.0.0.0:3702                   *:*                                   1348     svchost.exe    2023-06-22 12:05:10 UTC+0000
0x3e5f7cd0         UDPv6    :::3702                        *:*                                   1348     svchost.exe    2023-06-22 12:05:10 UTC+0000
0x3deff8d0         TCPv4    0.0.0.0:10243                  0.0.0.0:0            LISTENING        4        System
0x3deff8d0         TCPv6    :::10243                       :::0                 LISTENING        4        System
0x3df01ba0         TCPv4    0.0.0.0:49154                  0.0.0.0:0            LISTENING        964      svchost.exe
0x3e194410         TCPv4    0.0.0.0:135                    0.0.0.0:0            LISTENING        696      svchost.exe
0x3e195840         TCPv4    0.0.0.0:135                    0.0.0.0:0            LISTENING        696      svchost.exe
0x3e195840         TCPv6    :::135                         :::0                 LISTENING        696      svchost.exe
0x3e1ab8f0         TCPv4    0.0.0.0:49152                  0.0.0.0:0            LISTENING        404      wininit.exe
0x3e1fe300         TCPv4    0.0.0.0:49153                  0.0.0.0:0            LISTENING        744      svchost.exe
0x3e1fe300         TCPv6    :::49153                       :::0                 LISTENING        744      svchost.exe
0x3e1fecd0         TCPv4    0.0.0.0:49153                  0.0.0.0:0            LISTENING        744      svchost.exe
0x3e963ad0         TCPv4    127.0.0.1:9050                 0.0.0.0:0            LISTENING        3012     taskhsvc.exe
0x3ec4f620         TCPv4    0.0.0.0:49152                  0.0.0.0:0            LISTENING        404      wininit.exe
0x3ec4f620         TCPv6    :::49152                       :::0                 LISTENING        404      wininit.exe
0x3f1fd6f0         TCPv4    0.0.0.0:554                    0.0.0.0:0            LISTENING        2968     wmpnetwk.exe
0x3f1fd6f0         TCPv6    :::554                         :::0                 LISTENING        2968     wmpnetwk.exe
0x3ec2d010         TCPv4    127.0.0.1:50313                127.0.0.1:50314      ESTABLISHED      -1
0x3ecb1220         TCPv4    127.0.0.1:50314                127.0.0.1:50313      ESTABLISHED      -1
0x3f3ced90         UDPv4    0.0.0.0:3702                   *:*                                   1348     svchost.exe    2023-06-22 12:05:10 UTC+0000
0x3f2284c0         TCPv4    0.0.0.0:49156                  0.0.0.0:0            LISTENING        516      lsass.exe
0x3fcfd930         UDPv4    127.0.0.1:1900                 *:*                                   1348     svchost.exe    2023-06-22 12:06:48 UTC+0000
0x3fd1bbf0         UDPv6    ::1:61543                      *:*                                   1348     svchost.exe    2023-06-22 12:06:48 UTC+0000
0x3fd28310         UDPv4    127.0.0.1:61544                *:*                                   1348     svchost.exe    2023-06-22 12:06:48 UTC+0000
0x3fd2b420         UDPv6    ::1:1900                       *:*                                   1348     svchost.exe    2023-06-22 12:06:48 UTC+0000
0x3fd4a4a0         UDPv4    0.0.0.0:5004                   *:*                                   2968     wmpnetwk.exe   2023-06-22 12:06:48 UTC+0000
0x3fd4a4a0         UDPv6    :::5004                        *:*                                   2968     wmpnetwk.exe   2023-06-22 12:06:48 UTC+0000
0x3fd4aa90         UDPv4    0.0.0.0:5005                   *:*                                   2968     wmpnetwk.exe   2023-06-22 12:06:48 UTC+0000
0x3fd4adb0         UDPv4    0.0.0.0:5004                   *:*                                   2968     wmpnetwk.exe   2023-06-22 12:06:48 UTC+0000
0x3fd5fec0         UDPv4    0.0.0.0:5005                   *:*                                   2968     wmpnetwk.exe   2023-06-22 12:06:48 UTC+0000
0x3fd5fec0         UDPv6    :::5005                        *:*                                   2968     wmpnetwk.exe   2023-06-22 12:06:48 UTC+0000
0x3fc02ca0         TCPv4    0.0.0.0:554                    0.0.0.0:0            LISTENING        2968     wmpnetwk.exe
0x3fca6010         TCPv4    0.0.0.0:2869                   0.0.0.0:0            LISTENING        4        System
0x3fca6010         TCPv6    :::2869                        :::0                 LISTENING        4        System
0x3fc4f600         TCPv4    127.0.0.1:55206                127.0.0.1:9050       ESTABLISHED      -1
0x3fe604f0         TCPv4    127.0.0.1:9050                 127.0.0.1:55206      ESTABLISHED      -1
```

To find `_TCPT_OBJECT` structures using pool tag scanning, use the `connscan` instead. This can find artifacts from previous connections that have since been terminated, in addition to active ones. 
### Identifying Injected Code

The `malfind` plugin can be used to identify and extract injected code and malicious payloads from the memory of a running process as follows.

```shell-session
trop3n@htb[/htb]$ vol.py -f /home/htb-student/MemoryDumps/Win7-2515534d.vmem --profile=Win7SP1x64 malfind --pid=608
Volatility Foundation Volatility Framework 2.6.1
/usr/local/lib/python2.7/dist-packages/volatility/plugins/community/YingLi/ssh_agent_key.py:12: CryptographyDeprecationWarning: Python 2 is no longer supported by the Python core team. Support for it is now deprecated in cryptography, and will be removed in the next release.
  from cryptography.hazmat.backends.openssl import backend
Process: svchost.exe Pid: 608 Address: 0x12350000
Vad Tag: VadS Protection: PAGE_EXECUTE_READWRITE
Flags: CommitCharge: 128, MemCommit: 1, PrivateMemory: 1, Protection: 6

0x0000000012350000  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
0x0000000012350010  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
0x0000000012350020  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
0x0000000012350030  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................

0x0000000012350000 0000             ADD [EAX], AL
0x0000000012350002 0000             ADD [EAX], AL
0x0000000012350004 0000             ADD [EAX], AL
0x0000000012350006 0000             ADD [EAX], AL
0x0000000012350008 0000             ADD [EAX], AL
0x000000001235000a 0000             ADD [EAX], AL
0x000000001235000c 0000             ADD [EAX], AL
0x000000001235000e 0000             ADD [EAX], AL
0x0000000012350010 0000             ADD [EAX], AL
0x0000000012350012 0000             ADD [EAX], AL
0x0000000012350014 0000             ADD [EAX], AL
0x0000000012350016 0000             ADD [EAX], AL
0x0000000012350018 0000             ADD [EAX], AL
0x000000001235001a 0000             ADD [EAX], AL
0x000000001235001c 0000             ADD [EAX], AL
0x000000001235001e 0000             ADD [EAX], AL
0x0000000012350020 0000             ADD [EAX], AL
0x0000000012350022 0000             ADD [EAX], AL
0x0000000012350024 0000             ADD [EAX], AL
0x0000000012350026 0000             ADD [EAX], AL
0x0000000012350028 0000             ADD [EAX], AL
0x000000001235002a 0000             ADD [EAX], AL
0x000000001235002c 0000             ADD [EAX], AL
0x000000001235002e 0000             ADD [EAX], AL
0x0000000012350030 0000             ADD [EAX], AL
0x0000000012350032 0000             ADD [EAX], AL
0x0000000012350034 0000             ADD [EAX], AL
0x0000000012350036 0000             ADD [EAX], AL
0x0000000012350038 0000             ADD [EAX], AL
0x000000001235003a 0000             ADD [EAX], AL
0x000000001235003c 0000             ADD [EAX], AL
0x000000001235003e 0000             ADD [EAX], AL
```
### Identifying Handles

The `handles` plugin in Volatility is used for analyzing the handles (file and object references) held by a specific process within a memory dump. Understanding the handles associated with a process can provide valuable insights during incident response and digital forensics investigations, as it reveals the resources and objects a process is interacting with. Here's how to use the handles plugin.

```shell-session
trop3n@htb[/htb]$ vol.py -f /home/htb-student/MemoryDumps/Win7-2515534d.vmem --profile=Win7SP1x64 handles -p 1512 --object-type=Key
Volatility Foundation Volatility Framework 2.6.1
/usr/local/lib/python2.7/dist-packages/volatility/plugins/community/YingLi/ssh_agent_key.py:12: CryptographyDeprecationWarning: Python 2 is no longer supported by the Python core team. Support for it is now deprecated in cryptography, and will be removed in the next release.
  from cryptography.hazmat.backends.openssl import backend
Offset(V)             Pid             Handle             Access Type             Details
------------------ ------ ------------------ ------------------ ---------------- -------
0xfffff8a001628ee0   1512                0x4                0x9 Key              MACHINE\SOFTWARE\MICROSOFT\WINDOWS NT\CURRENTVERSION\IMAGE FILE EXECUTION OPTIONS
0xfffff8a00221e7e0   1512               0x14                0x9 Key              MACHINE\SOFTWARE\MICROSOFT\WINDOWS NT\CURRENTVERSION\IMAGE FILE EXECUTION OPTIONS
0xfffff8a0023b3490   1512               0x20            0x20019 Key              MACHINE\SYSTEM\CONTROLSET001\CONTROL\NLS\SORTING\VERSIONS
0xfffff8a001f1e300   1512               0x38            0xf003f Key              MACHINE
0xfffff8a001f3b410   1512               0x40                0x1 Key              MACHINE\SYSTEM\CONTROLSET001\CONTROL\SESSION MANAGER
0xfffff8a001f35280   1512               0x58                0x1 Key              MACHINE\SYSTEM\CONTROLSET001\CONTROL\NLS\CUSTOMLOCALE
0xfffff8a001f18440   1512               0x9c            0xf003f Key              USER\S-1-5-21-3232251811-3497904625-37069028-1001
0xfffff8a001d4e1f0   1512               0xa0            0x2001f Key              USER\S-1-5-21-3232251811-3497904625-37069028-1001\SOFTWARE\MICROSOFT\WINDOWS\CURRENTVERSION\INTERNET SETTINGS
0xfffff8a00080e8a0   1512               0xc0            0xf003f Key              USER
0xfffff8a00237dc10   1512               0xe0                0x1 Key              USER\S-1-5-21-3232251811-3497904625-37069028-1001\SOFTWARE\MICROSOFT\WINDOWS\CURRENTVERSION\EXPLORER
0xfffff8a001f63a80   1512              0x120                0x1 Key              MACHINE\SOFTWARE\WOW6432NODE\MICROSOFT\INTERNET EXPLORER\MAIN\FEATURECONTROL
0xfffff8a00208b750   1512              0x124            0x20019 Key              MACHINE\SOFTWARE\POLICIES\MICROSOFT\WINDOWS\CURRENTVERSION\INTERNET SETTINGS
0xfffff8a0022b6850   1512              0x128            0x20019 Key              USER\S-1-5-21-3232251811-3497904625-37069028-1001\SOFTWARE\POLICIES\MICROSOFT\WINDOWS\CURRENTVERSION\INTERNET SETTINGS
0xfffff8a000d807b0   1512              0x12c            0x20019 Key              USER\S-1-5-21-3232251811-3497904625-37069028-1001\SOFTWARE\MICROSOFT\WINDOWS\CURRENTVERSION\INTERNET SETTINGS
0xfffff8a0013b2920   1512              0x130            0x20019 Key              MACHINE\SOFTWARE\POLICIES
0xfffff8a001f7b610   1512              0x134            0x20019 Key              USER\S-1-5-21-3232251811-3497904625-37069028-1001\SOFTWARE\POLICIES
0xfffff8a0022f8ad0   1512              0x138            0x20019 Key              USER\S-1-5-21-3232251811-3497904625-37069028-1001\SOFTWARE
0xfffff8a0026778a0   1512              0x13c            0x20019 Key              MACHINE\SOFTWARE\WOW6432NODE
0xfffff8a000f4fb00   1512              0x140            0x20019 Key              MACHINE\SOFTWARE\WOW6432NODE\MICROSOFT\WINDOWS\CURRENTVERSION\INTERNET SETTINGS
0xfffff8a001efb870   1512              0x154            0xf003f Key              MACHINE\SYSTEM\CONTROLSET001\SERVICES\WINSOCK2\PARAMETERS\PROTOCOL_CATALOG9
0xfffff8a001f683c0   1512              0x15c            0xf003f Key              MACHINE\SYSTEM\CONTROLSET001\SERVICES\WINSOCK2\PARAMETERS\NAMESPACE_CATALOG5
0xfffff8a001f17660   1512              0x164            0x20019 Key              USER\S-1-5-21-3232251811-3497904625-37069028-1001\SOFTWARE\MICROSOFT\INTERNET EXPLORER\MAIN
0xfffff8a0012cbe90   1512              0x168            0x20019 Key              MACHINE\SOFTWARE\WOW6432NODE\MICROSOFT\INTERNET EXPLORER\MAIN
0xfffff8a00000c610   1512              0x1b8            0x2001f Key              USER\S-1-5-21-3232251811-3497904625-37069028-1001\SOFTWARE\MICROSOFT\WINDOWS\CURRENTVERSION\INTERNET SETTINGS\ZONEMAP
0xfffff8a0025cf4c0   1512              0x1bc            0x20019 Key              MACHINE\SOFTWARE\WOW6432NODE\MICROSOFT\WINDOWS\CURRENTVERSION\INTERNET SETTINGS\ZONEMAP
0xfffff8a00125d610   1512              0x1d0                0xf Key              USER\S-1-5-21-3232251811-3497904625-37069028-1001\SOFTWARE\MICROSOFT\WINDOWS\CURRENTVERSION\INTERNET SETTINGS\5.0\CACHE
0xfffff8a0023dcdd0   1512              0x22c            0xf003f Key              MACHINE\SOFTWARE\CLASSES
```

```shell-session
trop3n@htb[/htb]$ vol.py -f /home/htb-student/MemoryDumps/Win7-2515534d.vmem --profile=Win7SP1x64 handles -p 1512 --object-type=File
Volatility Foundation Volatility Framework 2.6.1
/usr/local/lib/python2.7/dist-packages/volatility/plugins/community/YingLi/ssh_agent_key.py:12: CryptographyDeprecationWarning: Python 2 is no longer supported by the Python core team. Support for it is now deprecated in cryptography, and will be removed in the next release.
  from cryptography.hazmat.backends.openssl import backend
Offset(V)             Pid             Handle             Access Type             Details
------------------ ------ ------------------ ------------------ ---------------- -------
0xfffffa8001d162e0   1512               0x10           0x100020 File             \Device\HarddiskVolume2\Windows
0xfffffa800228adc0   1512               0x1c           0x100020 File             \Device\HarddiskVolume2\Users\Analyst\Desktop\Samples
0xfffffa8000df8070   1512              0x110           0x12019f File             \Device\HarddiskVolume2\Users\Analyst\AppData\Local\Microsoft\Windows\Temporary Internet Files\counters.dat
0xfffffa8002210cd0   1512              0x170           0x100080 File             \Device\Nsi
0xfffffa8000dedf20   1512              0x1e4           0x100001 File             \Device\KsecDD
0xfffffa8002f70700   1512              0x23c           0x120089 File             \Device\HarddiskVolume2\Windows\Registration\R000000000006.clb
```

```shell-session
trop3n@htb[/htb]$ vol.py -f /home/htb-student/MemoryDumps/Win7-2515534d.vmem --profile=Win7SP1x64 handles -p 1512 --object-type=Process
Volatility Foundation Volatility Framework 2.6.1
/usr/local/lib/python2.7/dist-packages/volatility/plugins/community/YingLi/ssh_agent_key.py:12: CryptographyDeprecationWarning: Python 2 is no longer supported by the Python core team. Support for it is now deprecated in cryptography, and will be removed in the next release.
  from cryptography.hazmat.backends.openssl import backend
Offset(V)             Pid             Handle             Access Type             Details
------------------ ------ ------------------ ------------------ ---------------- -------
0xfffffa8001d0f8b0   1512              0x29c           0x1fffff Process          tasksche.exe(2972)
```
### Identifying Windows Services

The `svcscan` plugin in Volatility is used for listing and analyzing Windows services running on a system within a memory dump. Here's how to use the `svcscan` plugin.

```shell-session
trop3n@htb[/htb]$ vol.py -f /home/htb-student/MemoryDumps/Win7-2515534d.vmem --profile=Win7SP1x64 svcscan | more
Volatility Foundation Volatility Framework 2.6.1
/usr/local/lib/python2.7/dist-packages/volatility/plugins/community/YingLi/ssh_agent_key.py:12: CryptographyDeprecationWarning: Python 2 is no longer supported by the Python core team. Support for it is now deprecated in cryptography, and will be removed in the next release.
  from cryptography.hazmat.backends.openssl import backend
Offset: 0xb755a0
Order: 71
Start: SERVICE_AUTO_START
Process ID: 628
Service Name: DcomLaunch
Display Name: DCOM Server Process Launcher
Service Type: SERVICE_WIN32_SHARE_PROCESS
Service State: SERVICE_RUNNING
Binary Path: C:\Windows\system32\svchost.exe -k DcomLaunch

Offset: 0xb754b0
Order: 70
Start: SERVICE_DEMAND_START
Process ID: -
Service Name: dc21x4vm
Display Name: dc21x4vm
Service Type: SERVICE_KERNEL_DRIVER
Service State: SERVICE_STOPPED
Binary Path: -

Offset: 0xb753c0
Order: 69
Start: SERVICE_AUTO_START
Process ID: 868
Service Name: CscService
Display Name: Offline Files
Service Type: SERVICE_WIN32_SHARE_PROCESS
Service State: SERVICE_RUNNING
Binary Path: C:\Windows\System32\svchost.exe -k LocalSystemNetworkRestricted

Offset: 0xb770d0
Order: 68
Start: SERVICE_SYSTEM_START
Process ID: -
Service Name: CSC
Display Name: Offline Files Driver
Service Type: SERVICE_KERNEL_DRIVER
Service State: SERVICE_RUNNING
Binary Path: \Driver\CSC
---SNIP---
```
### Identifying Loaded DLLs

The `dlllist` plugin in Volatility is used for listing the dynamic link libraries (DLLs) loaded into the address process within a memory dump. Here's how to use the `dlllist` plugin.

```shell-session
trop3n@htb[/htb]$ vol.py -f /home/htb-student/MemoryDumps/Win7-2515534d.vmem --profile=Win7SP1x64 dlllist -p 1512
Volatility Foundation Volatility Framework 2.6.1
/usr/local/lib/python2.7/dist-packages/volatility/plugins/community/YingLi/ssh_agent_key.py:12: CryptographyDeprecationWarning: Python 2 is no longer supported by the Python core team. Support for it is now deprecated in cryptography, and will be removed in the next release.
  from cryptography.hazmat.backends.openssl import backend
************************************************************************
Ransomware.wan pid:   1512
Command line : "C:\Users\Analyst\Desktop\Samples\Ransomware.wannacry.exe"


Base                             Size          LoadCount LoadTime                       Path
------------------ ------------------ ------------------ ------------------------------ ----
0x0000000000400000           0x66b000             0xffff 1970-01-01 00:00:00 UTC+0000   C:\Users\Analyst\Desktop\Samples\Ransomware.wannacry.exe
0x00000000773f0000           0x19f000             0xffff 1970-01-01 00:00:00 UTC+0000   C:\Windows\SYSTEM32\ntdll.dll
0x00000000739d0000            0x3f000                0x3 2023-06-22 12:23:42 UTC+0000   C:\Windows\SYSTEM32\wow64.dll
0x0000000073970000            0x5c000                0x1 2023-06-22 12:23:42 UTC+0000   C:\Windows\SYSTEM32\wow64win.dll
0x0000000073960000             0x8000                0x1 2023-06-22 12:23:42 UTC+0000   C:\Windows\SYSTEM32\wow64cpu.dll
0x0000000000400000           0x66b000             0xffff 1970-01-01 00:00:00 UTC+0000   C:\Users\Analyst\Desktop\Samples\Ransomware.wannacry.exe
0x00000000775b0000           0x180000             0xffff 1970-01-01 00:00:00 UTC+0000   C:\Windows\SysWOW64\ntdll.dll
0x0000000075b50000           0x110000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\syswow64\kernel32.dll
0x00000000770c0000            0x47000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\syswow64\KERNELBASE.dll
0x0000000074d30000            0xa1000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\syswow64\ADVAPI32.dll
0x0000000077110000            0xac000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\syswow64\msvcrt.dll
0x0000000075b30000            0x19000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\SysWOW64\sechost.dll
0x0000000074de0000            0xf0000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\syswow64\RPCRT4.dll
0x0000000074cd0000            0x60000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\syswow64\SspiCli.dll
0x0000000074cc0000             0xc000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\syswow64\CRYPTBASE.dll
0x00000000755f0000            0x35000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\syswow64\WS2_32.dll
0x0000000074f70000             0x6000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\syswow64\NSI.dll
0x000000006bb70000            0x66000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\system32\MSVCP60.dll
0x00000000738f0000            0x1c000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\system32\iphlpapi.dll
0x00000000737c0000             0x7000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\system32\WINNSI.DLL
0x0000000075160000           0x437000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\syswow64\WININET.dll
0x0000000076050000             0x4000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\syswow64\api-ms-win-downlevel-user32-l1-1-0.dll
0x0000000075e60000           0x100000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\syswow64\user32.DLL
0x0000000074ee0000            0x90000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\syswow64\GDI32.dll
0x00000000770a0000             0xa000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\syswow64\LPK.dll
0x00000000750c0000            0x9d000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\syswow64\USP10.dll
0x00000000770b0000             0x4000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\syswow64\api-ms-win-downlevel-shlwapi-l1-1-0.dll
0x0000000075c60000            0x57000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\syswow64\shlwapi.DLL
0x0000000074f80000             0x4000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\syswow64\api-ms-win-downlevel-version-l1-1-0.dll
0x00000000737b0000             0x9000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\system32\version.DLL
0x0000000075f60000             0x3000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\syswow64\api-ms-win-downlevel-normaliz-l1-1-0.dll
0x0000000075630000             0x3000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\syswow64\normaliz.DLL
0x0000000076210000           0x236000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\syswow64\iertutil.dll
0x0000000075fa0000             0x5000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\syswow64\api-ms-win-downlevel-advapi32-l1-1-0.dll
0x00000000756d0000            0x17000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\syswow64\USERENV.dll
0x0000000075fb0000             0xb000             0xffff 2023-06-22 12:23:42 UTC+0000   C:\Windows\syswow64\profapi.dll
0x0000000075ad0000            0x60000                0x2 2023-06-22 12:28:02 UTC+0000   C:\Windows\system32\IMM32.DLL
0x00000000760b0000            0xcd000                0x1 2023-06-22 12:28:02 UTC+0000   C:\Windows\syswow64\MSCTF.dll
0x000000006cd90000             0x8000                0x2 2023-06-22 12:28:06 UTC+0000   C:\Windows\system32\Secur32.dll
0x0000000076450000           0xc4c000                0x1 2023-06-22 12:28:06 UTC+0000   C:\Windows\syswow64\SHELL32.dll
0x0000000075850000           0x15f000               0x22 2023-06-22 12:28:06 UTC+0000   C:\Windows\syswow64\ole32.dll
0x000000006cc30000             0x4000                0x1 2023-06-22 12:28:06 UTC+0000   C:\Windows\system32\api-ms-win-downlevel-advapi32-l2-1-0.dll
0x00000000771c0000             0x4000                0x2 2023-06-22 12:28:06 UTC+0000   C:\Windows\syswow64\api-ms-win-downlevel-ole32-l1-1-0.dll
0x000000006cc10000            0x12000                0x1 2023-06-22 12:28:06 UTC+0000   C:\Windows\system32\dhcpcsvc.DLL
0x000000006cc00000             0xd000                0x1 2023-06-22 12:28:06 UTC+0000   C:\Windows\system32\dhcpcsvc6.DLL
0x000000006cbc0000            0x3c000                0x4 2023-06-22 12:28:06 UTC+0000   C:\Windows\system32\mswsock.dll
0x000000006cbb0000             0x6000                0x1 2023-06-22 12:28:06 UTC+0000   C:\Windows\System32\wship6.dll
0x000000006cd80000             0x4000                0x1 2023-06-22 12:28:06 UTC+0000   C:\Windows\system32\api-ms-win-downlevel-shlwapi-l2-1-0.dll
0x00000000737d0000            0x44000                0x2 2023-06-22 12:28:06 UTC+0000   C:\Windows\system32\DNSAPI.dll
0x00000000756f0000           0x150000                0x1 2023-06-22 12:28:06 UTC+0000   C:\Windows\syswow64\urlmon.dll
0x0000000075a30000            0x91000                0x4 2023-06-22 12:28:06 UTC+0000   C:\Windows\syswow64\OLEAUT32.dll
0x000000006cba0000             0x5000                0x1 2023-06-22 12:28:06 UTC+0000   C:\Windows\System32\wshtcpip.dll
0x0000000075640000            0x83000                0x1 2023-06-22 12:28:06 UTC+0000   C:\Windows\syswow64\CLBCatQ.DLL
0x000000006bb10000            0x5a000                0x1 2023-06-22 12:28:06 UTC+0000   C:\Windows\System32\netprofm.dll
0x000000006bb00000            0x10000                0x1 2023-06-22 12:28:06 UTC+0000   C:\Windows\System32\nlaapi.dll
0x000000006baf0000             0x6000                0x1 2023-06-22 12:28:06 UTC+0000   C:\Windows\system32\rasadhlp.dll
0x0000000071ac0000            0x17000                0x1 2023-06-22 12:30:20 UTC+0000   C:\Windows\system32\CRYPTSP.dll
0x000000006d420000            0x3b000                0x1 2023-06-22 12:30:20 UTC+0000   C:\Windows\system32\rsaenh.dll
0x0000000071ab0000             0xe000                0x1 2023-06-22 12:30:20 UTC+0000   C:\Windows\system32\RpcRtRemote.dll
0x000000006bae0000             0x8000                0x1 2023-06-22 12:30:20 UTC+0000   C:\Windows\System32\npmproxy.dll
0x000000006ced0000            0x4c000             0xffff 2023-06-22 12:31:13 UTC+0000   C:\Windows\system32\apphelp.dll
```
### Identifying Hives

The `hivelist` plugin in Volatility is used for listing the hives (registry files) present in the memory dump of a Windows system. Here's how to use the hivelist plugin.

```shell-session
trop3n@htb[/htb]$ vol.py -f /home/htb-student/MemoryDumps/Win7-2515534d.vmem --profile=Win7SP1x64 hivelist
Volatility Foundation Volatility Framework 2.6.1
/usr/local/lib/python2.7/dist-packages/volatility/plugins/community/YingLi/ssh_agent_key.py:12: CryptographyDeprecationWarning: Python 2 is no longer supported by the Python core team. Support for it is now deprecated in cryptography, and will be removed in the next release.
  from cryptography.hazmat.backends.openssl import backend
Virtual            Physical           Name
------------------ ------------------ ----
0xfffff8a001710010 0x000000002c2e4010 \??\C:\Users\Analyst\AppData\Local\Microsoft\Windows\UsrClass.dat
0xfffff8a001d4b410 0x000000001651f410 \??\C:\System Volume Information\Syscache.hve
0xfffff8a00000f010 0x0000000026de8010 [no name]
0xfffff8a000024010 0x00000000273f3010 \REGISTRY\MACHINE\SYSTEM
0xfffff8a000058010 0x0000000026727010 \REGISTRY\MACHINE\HARDWARE
0xfffff8a0000f7410 0x0000000019824410 \SystemRoot\System32\Config\DEFAULT
0xfffff8a000844010 0x000000001a979010 \Device\HarddiskVolume1\Boot\BCD
0xfffff8a0009d6010 0x000000001998d010 \SystemRoot\System32\Config\SOFTWARE
0xfffff8a000e0a010 0x000000000724e010 \SystemRoot\System32\Config\SAM
0xfffff8a000e36010 0x0000000012f0e010 \SystemRoot\System32\Config\SECURITY
0xfffff8a000f7e010 0x0000000012f7b010 \??\C:\Windows\ServiceProfiles\NetworkService\NTUSER.DAT
0xfffff8a00100c410 0x0000000006de7410 \??\C:\Windows\ServiceProfiles\LocalService\NTUSER.DAT
0xfffff8a0016a8010 0x000000002aecd010 \??\C:\Users\Analyst\ntuser.dat
```
## Rootkit Analysis with Volatility v2

Let's now see a demonstration of utilizing `Volatility v2` to analyze a memory dump saved as `rootkit.vmem` inside the `/home/htb-student/MemoryDumps` directory of this section's target.
### Understanding the EPROCESS Structure

[EPROCESS](https://www.nirsoft.net/kernel_struct/vista/EPROCESS.html) is a data structure in the Windows kernel that represents a process. Each running process in the Windows operating system has a corresponding `EPROCESS` block in kernel memory. During memory analysis, the examination of `EPROCESS` structures is crucial for understanding the running processes on a system, identifying parent-child relationships, and determining which active processes were active at the time of the memory capture.

![](https://i.imgur.com/JfCt94N.png)
### FLINK and BLINK

A doubly-linked list is a fundamental data structure in computer science and programming. It is a type of linked list where each node (record) contains two references or pointers:

- **Next Pointer**: This points to the next node in the list, allowing us to traverse the list in a forward direction.
- **Previous Pointer**: This points to the previous node in the list, allowing us to traverse the list in a backward direction.

Within the `EPROCESS` structure, we have `ActiveProcessLinks` as the doubly-linked list which contains the `flink` field and the `blink` field.

- `flink`: Is a forward pointer that points to the `ActiveProcessLinks` list entry of the `_next_ EPROCESS` structure in the list of active processes.
- `blink`: Is a backward pointer within the `EPROCESS` structure that points to the `ActiveProcessLinks` list entry of the `_previous_ EPROCESS` structure in the list of active processes.

These linked lists of EPROCESS structures are used by the Windows kernel to quickly iterate through all running processes on the system. The below diagram shows how this linked list looks.

![](https://i.imgur.com/JKBGiIF.png)
### Identifying Rootkit Signs

`Direct Kernel Object Manipulation (DKOM)` is a *sophisticated technique used by rootkits* and advanced malware to **manipulate the Windows operating system's kernel data structures** in order to ***hide malicious processes, drivers, files and other artifacts*** from detection by security tools and utilities running in userland.

If, for example, a monitoring tool is dependent on the `EPROCESS` structure for the enumeration of the running processes, and there's a rootkit running on the system which manipulates the `EPROCESS` structure directly in kernel memory by altering the `EPROCESS` structure or unlinking
a process from lists, the monitoring tool will not be able to get the hidden process in the currently running processes list.

The below screenshot shows a graphical representation of how this unlinking actually works.

![](https://i.imgur.com/uj1uYTA.png)

The `psscan` plugin is used to enumerate running processes. It scans the memory pool tags associated with each process's `EPROCESS` structure. This technique can help identify processes that may have been hidden or unlinked by rootkits, as well as processes that have been terminated but have no been removed from memory yet. This plugin can be used as follows.

```shell-session
trop3n@htb[/htb]$ vol.py -f /home/htb-student/MemoryDumps/rootkit.vmem psscan
Volatility Foundation Volatility Framework 2.6.1
/usr/local/lib/python2.7/dist-packages/volatility/plugins/community/YingLi/ssh_agent_key.py:12: CryptographyDeprecationWarning: Python 2 is no longer supported by the Python core team. Support for it is now deprecated in cryptography, and will be removed in the next release.
  from cryptography.hazmat.backends.openssl import backend
Offset(P)          Name                PID   PPID PDB        Time created                   Time exited
------------------ ---------------- ------ ------ ---------- ------------------------------ ------------------------------
0x0000000001a404b8 ipconfig.exe       2988   2980 0x091403c0 2023-06-24 07:31:16 UTC+0000   2023-06-24 07:31:17 UTC+0000
0x0000000001a63138 cmd.exe            2980   2004 0x091401c0 2023-06-24 07:31:16 UTC+0000   2023-06-24 07:31:17 UTC+0000
0x0000000001b24888 explorer.exe       1444    624 0x09140320 2023-06-23 16:34:38 UTC+0000
0x0000000001bc62a8 tasksche.exe       1084   1684 0x091403e0 2023-06-24 07:28:16 UTC+0000
0x0000000001c3d2d8 @WanaDecryptor@    2248   1084 0x091403a0 2023-06-24 07:29:20 UTC+0000
0x0000000001c4e020 cmd.exe            1932   1444 0x09140380 2023-06-24 07:27:16 UTC+0000
0x0000000001c54da0 cmd.exe            2396   2264 0x091401c0 2023-06-24 07:29:30 UTC+0000   2023-06-24 07:29:37 UTC+0000
0x0000000001c8a020 @WanaDecryptor@    2324   2284 0x09140440 2023-06-24 07:29:20 UTC+0000
0x0000000001cb7628 test.exe           1344    668 0x09140360 2023-06-24 07:28:15 UTC+0000
0x0000000002063ab8 svchost.exe        1220    668 0x09140160 2023-06-23 16:14:54 UTC+0000
0x0000000002093020 services.exe        668    624 0x09140080 2023-06-23 16:14:53 UTC+0000
0x0000000002094da0 ctfmon.exe          564    232 0x09140240 2023-06-23 16:15:09 UTC+0000
0x0000000002095020 csrss.exe           600    368 0x09140040 2023-06-23 16:14:51 UTC+0000
0x000000000209fa78 vmtoolsd.exe       2004    668 0x091402a0 2023-06-23 16:15:24 UTC+0000
0x00000000020a2a90 spoolsv.exe        1556    668 0x091401a0 2023-06-23 16:14:59 UTC+0000
0x00000000020ceb40 alg.exe            1520    668 0x091402c0 2023-06-23 16:15:26 UTC+0000
0x00000000020ff870 wmiprvse.exe        560    880 0x09140300 2023-06-23 16:15:26 UTC+0000
0x000000000216a650 taskhsvc.exe       2340   2248 0x09140340 2023-06-24 07:29:22 UTC+0000
0x0000000002172da0 winlogon.exe        624    368 0x09140060 2023-06-23 16:14:52 UTC+0000
0x00000000021adda0 msmsgs.exe          548    232 0x09140220 2023-06-23 16:15:09 UTC+0000
0x000000000224b128 svchost.exe         992    668 0x09140100 2023-06-23 16:14:53 UTC+0000
0x000000000225cda0 VGAuthService.e    1832    668 0x09140280 2023-06-23 16:15:16 UTC+0000
0x0000000002269490 vmacthlp.exe        848    668 0x091400c0 2023-06-23 16:14:53 UTC+0000
0x0000000002288770 wmic.exe           2416   2396 0x09140400 2023-06-24 07:29:30 UTC+0000   2023-06-24 07:29:37 UTC+0000
0x00000000022ee020 cmd.exe            1628   1444 0x091402e0 2023-06-24 07:25:01 UTC+0000
0x0000000002346990 svchost.exe         880    668 0x091400e0 2023-06-23 16:14:53 UTC+0000
0x00000000023c7618 taskmgr.exe         260   1444 0x091401e0 2023-06-24 07:27:55 UTC+0000
0x0000000002419850 svchost.exe        1136    668 0x09140120 2023-06-23 16:14:53 UTC+0000
0x000000000248c020 smss.exe            368      4 0x09140020 2023-06-23 16:14:49 UTC+0000
0x000000000248f020 svchost.exe        1176    668 0x09140140 2023-06-23 16:14:53 UTC+0000
0x000000000249fda0 vmtoolsd.exe        540    232 0x09140180 2023-06-23 16:15:09 UTC+0000
0x00000000024a57a8 lsass.exe           680    624 0x091400a0 2023-06-23 16:14:53 UTC+0000
0x00000000024cb928 svchost.exe        1708    668 0x09140260 2023-06-23 16:15:16 UTC+0000
0x000000000250e020 rundll32.exe        532    232 0x09140200 2023-06-23 16:15:09 UTC+0000
0x00000000025c8830 System                4      0 0x0031c000
```

In the output below, we can see that the `pslist` plugin could not find `test.exe` which was hidden by the rootkit, but the `psscan` plugin was able to find it.

```shell-session
trop3n@htb[/htb]$ vol.py -f /home/htb-student/MemoryDumps/rootkit.vmem pslist
Volatility Foundation Volatility Framework 2.6.1
/usr/local/lib/python2.7/dist-packages/volatility/plugins/community/YingLi/ssh_agent_key.py:12: CryptographyDeprecationWarning: Python 2 is no longer supported by the Python core team. Support for it is now deprecated in cryptography, and will be removed in the next release.
  from cryptography.hazmat.backends.openssl import backend
Offset(V)  Name                    PID   PPID   Thds     Hnds   Sess  Wow64 Start                          Exit
---------- -------------------- ------ ------ ------ -------- ------ ------ ------------------------------ ------------------------------
0x823c8830 System                    4      0     58      476 ------      0     
0x8228c020 smss.exe                368      4      3       19 ------      0 2023-06-23 16:14:49 UTC+0000
0x81e95020 csrss.exe               600    368     14      544      0      0 2023-06-23 16:14:51 UTC+0000
0x81f72da0 winlogon.exe            624    368     19      514      0      0 2023-06-23 16:14:52 UTC+0000
0x81e93020 services.exe            668    624     16      277      0      0 2023-06-23 16:14:53 UTC+0000
0x822a57a8 lsass.exe               680    624     23      358      0      0 2023-06-23 16:14:53 UTC+0000
0x82069490 vmacthlp.exe            848    668      1       25      0      0 2023-06-23 16:14:53 UTC+0000
0x82146990 svchost.exe             880    668     18      202      0      0 2023-06-23 16:14:53 UTC+0000
0x8204b128 svchost.exe             992    668     11      272      0      0 2023-06-23 16:14:53 UTC+0000
0x82219850 svchost.exe            1136    668     84     1614      0      0 2023-06-23 16:14:53 UTC+0000
0x8228f020 svchost.exe            1176    668      5       77      0      0 2023-06-23 16:14:53 UTC+0000
0x81e63ab8 svchost.exe            1220    668     15      218      0      0 2023-06-23 16:14:54 UTC+0000
0x81ea2a90 spoolsv.exe            1556    668     11      129      0      0 2023-06-23 16:14:59 UTC+0000
0x8230e020 rundll32.exe            532    232      4       78      0      0 2023-06-23 16:15:09 UTC+0000
0x8229fda0 vmtoolsd.exe            540    232      6      247      0      0 2023-06-23 16:15:09 UTC+0000
0x81fadda0 msmsgs.exe              548    232      2      190      0      0 2023-06-23 16:15:09 UTC+0000
0x81e94da0 ctfmon.exe              564    232      1       75      0      0 2023-06-23 16:15:09 UTC+0000
0x822cb928 svchost.exe            1708    668      5       87      0      0 2023-06-23 16:15:16 UTC+0000
0x8205cda0 VGAuthService.e        1832    668      2       60      0      0 2023-06-23 16:15:16 UTC+0000
0x81e9fa78 vmtoolsd.exe           2004    668      7      278      0      0 2023-06-23 16:15:24 UTC+0000
0x81eff870 wmiprvse.exe            560    880     12      236      0      0 2023-06-23 16:15:26 UTC+0000
0x81eceb40 alg.exe                1520    668      6      107      0      0 2023-06-23 16:15:26 UTC+0000
0x81924888 explorer.exe           1444    624     17      524      0      0 2023-06-23 16:34:38 UTC+0000
0x821c7618 taskmgr.exe             260   1444      3       75      0      0 2023-06-24 07:27:55 UTC+0000
0x81a3d2d8 @WanaDecryptor@        2248   1084      3       57      0      0 2023-06-24 07:29:20 UTC+0000
0x81a8a020 @WanaDecryptor@        2324   2284      2       56      0      0 2023-06-24 07:29:20 UTC+0000
0x81f6a650 taskhsvc.exe           2340   2248      2       60      0      0 2023-06-24 07:29:22 UTC+0000
0x81863138 cmd.exe                2980   2004      0 --------      0      0 2023-06-24 07:31:16 UTC+0000   2023-06-24 07:31:17 UTC+0000
0x818404b8 ipconfig.exe           2988   2980      0 --------      0      0 2023-06-24 07:31:16 UTC+0000   2023-06-24 07:31:17 UTC+0000
```

---
## Memory Analysis using Strings

Analyzing strings in memory dumps is a **valuable technique** in memory forensics and incident response. Strings often contain human-readable information, such as text messages, file paths, IP addresses, and even passwords.

We can either use the [Strings](https://learn.microsoft.com/en-us/sysinternals/downloads/strings) tool from Sysinternals suite if our system is Windows-based, or the `strings` command from `Binutils`, if our system is Linux-based.

Let's see some examples against a memory dump named `Win7-2515534d.vmem` that resides in the `/home/htb-student/MemoryDumps` directory of this section's target. 
### Identifying IPv4 Addresses

```shell-session
trop3n@htb[/htb]$ strings /home/htb-student/MemoryDumps/Win7-2515534d.vmem | grep -E "\b([0-9]{1,3}\.){3}[0-9]{1,3}\b"
---SNIP---
127.192.0.0/10
212.83.154.33
directory server at 10.10.10.1:52860
127.192.0.0/10
0.0.0.0
192.168.182.254
---SNIP---
```
### Identifying Email Addresses

```shell-session
trop3n@htb[/htb]$ strings /home/htb-student/MemoryDumps/Win7-2515534d.vmem | grep -oE "\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,4}\b"
CPS-requests@verisign.com
silver-certs@saunalahti.fi
joe@freebsd.org
info@netlock.net
UtV@UtV.UtT
acrse@economia.gob
acrse@economia.gob
CPS-requests@verisign.com
dl@comres.dll
info@globaltrust.info
info@globaltrust.info
info@globaltrust.info
ll@tzres.dll
am@tzres.dll
sy@tzres.dll
d@tzres.dll
5@tzres.dll
ic@tzres.dll
ll@tzres.dll
oo@tzres.dll
N@tzres.dll
1@tzres.dll
Mi@tzres.dll
le@tzres.dll
UtV@UtV.UtT
ssupport@hex-rays.com
ssupport@hex-rays.com
CPS-requests@verisign.com
info@aadobetech.com
CPS-requests@verisign.com
noreply@vmware.com
noreply@vmware.com
noreply@vmware.com
appro@openssl.org
appro@openssl.org
support@hex-rays.com
WanaDecryptor@.exe.lnk
1istrstream@stayer.exe
iVq0xhg@p.yRg
appro@openssl.org
appro@openssl.org
support@hex-rays.com
T@..AA
appro@openssl.org
em@provsvc.dll
support@hex-rays.com
support@hex-rays.com
support@hex-rays.com
WanaDecryptor@.exe.lnk
appro@openssl.org
now@bitwi.se
Bram@vim.org
support@hex-rays.com
support@hex-rays.com
---SNIP---
```
### Identifying Command Prompt or PowerShell Artifacts

```shell-session
trop3n@htb[/htb]$ strings /home/htb-student/MemoryDumps/Win7-2515534d.vmem | grep -E "(cmd|powershell|bash)[^\s]+"
---SNIP---
ComSpec=C:\WINDOWS\system32\cmd.exe
ComSpec=C:\WINDOWS\system32\cmd.exe
cmd.exe
cmd.exe
cmd.exe
cmd.exe
C:\WINDOWS\system32\cmd.exe
cmd.exe /c "C:\Intel\ueqzlhmlwuxdg271\tasksche.exe"
ComSpec=C:\WINDOWS\system32\cmd.exe
cmd.exe /c "%s"
cmd.exe /c start /b @WanaDecryptor@.exe vs
cmd /c ""C:\Program Files\VMware\VMware Tools\suspend-vm-default.bat""
---SNIP---
```

These are just a few example of common string searches during memory forensics and incident response. You can adapt and customize these searches based on your specific investigation's needs and the types of information you are looking for in the memory dump. Regular expressions can be powerful tools for pattern matching and data extraction during forensic analysis.
# Disk Forensics

As we've previously highlighted, adhering to the sequence of data volatility is crucial. It's imperative that we scrutinize each byte to detect the subtle traces left by cyber adversaries. Having covered memory forensics, let's now shift our attention to the area of `disk forensics` (disk image examination and analysis).

Many disk forensic tools, both commercial and open-source, come packed with features. However, for incident response teams, certain functionalities stand out:

- `File Structure Insight`: Being able to navigate and see the disk's file hierarchy is crucial. Top-tier forensic tools should display this structure, allowing quick access to specific files, especially in known locations on a suspect system. 

- `Hex Viewer`: For those moments when you need to get up close and personal with your data, viewing files in hexadecimal is *essential*. This capability is especially handy when dealing with threats like **tailored malware** or **unique exploits**.

- `Web Artifact Analysis`:  With so much user data tied to web activities, a forensic tool must effectively sift through and present this data. It's a game-changer when you're piecing together events leading up to a user landing on a malicious website.

- `Email Carving`: Sometimes, the trail leads to internal threats. Maybe it's a rogue employee or just someone who slipped up. In such cases, emails often hold the key. A tool that can *extract and present this day streamlines the process*, making it easier to connect the dots.

- `Image Viewer`: At times, the images stored on systems can tell a story of their own. Whether it's for policy checks or deeper dives, having a built-in viewer is a boon.

- `Metadata Analysis`: Details like file creation timestamps, hashes, and disk location can be invaluable. Consider a scenario where you're trying to match the launch time of an app with a malware alert. Such correlations can be the linchpin in your investigation.

Enter [Autopsy](https://www.autopsy.com/): a user-friendly forensic platform built atop the open-source Sleuth Kit toolset. It mirrors many features you'd find in its commercial counterparts: timeline assessments, keyword hunts, web and email artifact retrievals, and the ability to sift results based on known malicious file hashes. 

Once you've loaded a forensic image and processed the data, you'll see the forensic artifacts neatly organized on the side panel. From here, you can:

![](https://i.imgur.com/juPF5e9.png)

>- Dive into `Data Sources` to explore files and directories.

![](https://i.imgur.com/qVRTAp3.png)

> - Examine `Web Artifacts`.

![](https://i.imgur.com/VfZhLqu.png)

> - Check `Attached Devices`.

![](https://i.imgur.com/iOwZKzQ.png)

> - Recover `Deleted Files`.

![](https://i.imgur.com/9D2GSMx.png)

> - Conduct `Keyword Searches`.

![](https://i.imgur.com/Aa60yUm.png)

![](https://i.imgur.com/ZE5doVY.png)

> - Use `Keyword Lists` for targeted searches.

![](https://i.imgur.com/7OnSNYH.png)

![](https://i.imgur.com/TAIpLtO.png)

> - Undertake `Timeline Analysis` to map out events.

We'll be heavily utilizing Autopsy in the forthcoming "Practical Digital Forensics Scenario" section.
# Rapid Triage Examination & Analysis Tools

When it comes to Rapid Triage analysis, the right external tools are essential for thorough examination and analysis.

`Eric Zimmerman` has curated a suite of indispensable tools tailored for this very purpose. These tools are meticulously designed to aid forensic analysts in their quest to extract vital information from digital devices and artifacts.

For a comprehensive list of these tools, check out: [https://ericzimmerman.github.io/#!index.md](https://ericzimmerman.github.io/#!index.md)

> [!NOTE]
> Let's now navigate to the bottom of this section and click on "Click here to spawn the target system!". Then, let's RDP into the Target IP using the provided credentials. The vast majority of the actions/commands covered from this point up to end of this section can be replicated inside the target, offering a more comprehensive grasp of the topics presented.

To streamline the download process, we can visit the official website and select either the `.net 4` or `.net 6` link. This action will initiate the download of all the tools in a compressed format. 

![](https://i.imgur.com/K56icyZ.png)

We can also leverage the provided PowerShell script, as outlined in Step 2 of the screenshot above, to download all the tools. 

```powershell
PS C:\Users\johndoe\Desktop\Get-ZimmermanTools> .\Get-ZimmermanTools.ps1

This script will discover and download all available programs
from https://ericzimmerman.github.io and download them to C:\htb\dfir_module\tools

A file will also be created in C:\Users\johndoe\Desktop\Get-ZimmermanTools that tracks the SHA-1 of each file,
so rerunning the script will only download new versions.

To redownload, remove lines from or delete the CSV file created under C:\htb\dfir_module\tools and rerun. Enjoy!

Use -NetVersion to control which version of the software you get (4 or 6). Default is 6. Use 0 to get both

* Getting available programs...
* Files to download: 27
* Downloaded Get-ZimmermanTools.zip (Size: 10,396)
* C:\htb\dfir_module\tools\net6 does not exist. Creating...
* Downloaded AmcacheParser.zip (Size: 23,60,293) (net 6)
* Downloaded AppCompatCacheParser.zip (Size: 22,62,497) (net 6)
* Downloaded bstrings.zip (Size: 14,73,298) (net 6)
* Downloaded EvtxECmd.zip (Size: 40,36,022) (net 6)
* Downloaded EZViewer.zip (Size: 8,25,80,608) (net 6)
* Downloaded JLECmd.zip (Size: 27,79,229) (net 6)
* Downloaded JumpListExplorer.zip (Size: 8,66,96,361) (net 6)
* Downloaded LECmd.zip (Size: 32,38,911) (net 6)
* Downloaded MFTECmd.zip (Size: 22,26,605) (net 6)
* Downloaded MFTExplorer.zip (Size: 8,27,54,162) (net 6)
* Downloaded PECmd.zip (Size: 20,13,672) (net 6)
* Downloaded RBCmd.zip (Size: 18,19,172) (net 6)
* Downloaded RecentFileCacheParser.zip (Size: 17,22,133) (net 6)
* Downloaded RECmd.zip (Size: 36,89,345) (net 6)
* Downloaded RegistryExplorer.zip (Size: 9,66,96,169) (net 6)
* Downloaded rla.zip (Size: 21,55,515) (net 6)
* Downloaded SDBExplorer.zip (Size: 8,24,54,727) (net 6)
* Downloaded SBECmd.zip (Size: 21,90,158) (net 6)
* Downloaded ShellBagsExplorer.zip (Size: 8,80,06,168) (net 6)
* Downloaded SQLECmd.zip (Size: 52,83,482) (net 6)
* Downloaded SrumECmd.zip (Size: 24,00,622) (net 6)
* Downloaded SumECmd.zip (Size: 20,23,009) (net 6)
* Downloaded TimelineExplorer.zip (Size: 8,77,50,507) (net 6)
* Downloaded VSCMount.zip (Size: 15,46,539) (net 6)
* Downloaded WxTCmd.zip (Size: 36,98,112) (net 6)
* Downloaded iisGeolocate.zip (Size: 3,66,76,319) (net 6)

* Saving downloaded version information to C:\Users\johndoe\Desktop\Get-ZimmermanTools\!!!RemoteFileDetails.csv
```

While we'll be using a subset of these tools to analyze the KAPE output data, it's prudent for us to familiarize ourselves with the entire tooljit. Understanding the full capabilities of each too can significantly enhance our investigative prowess.

---
In this section we will be working with certain tools and evidence that reside in the following directories of this section's target.

- Evidence Location: `C:\Users\johndoe\Desktop\forensic_data`
	- KAPE's output location: `C:\Users\johndoe\Desktop\forensic_data\kape_output`
- Eric Zimmerman's tools location: `C:\Users\johndoe\Desktop\Get-ZimmermanTools`
- Active@ Disk Editor's Location: `C:\Program Files\LSoft Technologies\Active@ Disk Editor`
- RegRipper's location: `C:\Users\johndoe\Desktop\RegRipper3.0-master`

---
### MAC(b) Times in NTFS

The term `MAC(b) times` denotes a series of timestamps linked to files or objects. These timestamps are pivotal as they shed light on the chronology of events or actions on a file system. The acronym `MAC(b)` is an abbreviation for `Modified, Accessed, Changed and (b) Birth` times. The inclusion of `b` signifies the `Birth timestamp`, which isn't universally present across all file systems or easily accessible via standard Windows API functions. Let's delve deeper into the nuances of `MACB` timestamps.

- `Modified Time (M)`: This timestamp captures the last instance when the content within the file underwent modifications. Any alterations to the file's data, such as content edits, trigger an update to this timestamp.

- `Accessed Time (A)`: This timestamp reflects the last occasion when the file was accessed or read, updating whenever the file is opened or otherwise engaged.

- `Changed [Change in MFT Record] (c)`: This timestamp signifies changes to the MFT record. It captures the moment when the file was initially created. However, it's worth noting that certain file systems, like NTFS, might update this timestamp if the file undergoes *movement* or *copying*.

- `Birth Time (b)`: Often referred to as the Birth or Born timestamp, this represents the precise moment when the file or object was instantiated on the file system. Its significance in forensic investigation cannot be overstated, especially when determining the file's original creation time.
### DeepSeek Output for `MAC(b)`:

Ah, in the context of **NTFS (New Technology File System)** and **Windows**, **MAC(b) times** refer to the **timestamps** associated with files and directories. These timestamps are used to track when specific events occur for a file or directory. The "MAC" in this case stands for **Modified, Accessed, and Created**, and the "(b)" typically refers to the fact that these timestamps are stored in the **$STANDARD_INFORMATION attribute** of the NTFS file system.

Here’s a breakdown of the MAC(b) times:

1. **Modified Time (M)**:
    
    - This timestamp indicates the last time the **content of the file or directory was modified**. For example, if you edit a text file and save it, the modified time will be updated.
    
2. **Accessed Time (A)**:
    
    - This timestamp shows the last time the file or directory was **accessed or read**. For example, if you open a file to view its contents, the accessed time will be updated. Note that on modern Windows systems, accessed time updates may be disabled by default for performance reasons.
    
3. **Created Time (C)**:
    
    - This timestamp records when the file or directory was **originally created**. This value does not change unless the file is moved or copied, in which case the creation time may be updated depending on the operation.
    
4. **Birth Time (b)**:
    
    - The "(b)" in MAC(b) refers to the **birth time**, which is the time when the file or directory was **first created on the file system**. This is distinct from the "Created Time" in some cases, as the birth time is more specific to the NTFS file system and is not always available or used in other file systems.
### Key Points:

- These timestamps are stored in the **$STANDARD_INFORMATION** attribute of the NTFS file system.
- They are used for tracking file activity and are often important for forensic analysis, file management, and system auditing.
- In some cases, the `**FILENAME∗∗attributeinNTFSalsostoresitsownsetoftimestamps,whichmaydifferslightlyfromthoseinFILENAME∗∗attributeinNTFSalsostoresitsownsetoftimestamps,whichmaydifferslightlyfromthoseinSTANDARD_INFORMATION.`
### Example:

If you right-click a file in Windows, go to **Properties**, and check the **Details** tab, you’ll see these timestamps listed as:

- **Date created** (Created Time)
- **Date modified** (Modified Time)
- **Date accessed** (Accessed Time)

These timestamps are crucial for understanding file activity and are often used in digital forensics to reconstruct events on a system.
### Why It's Important to DFIR

In **digital forensics**, **MAC(b) times** (Modified, Accessed, Created, and Birth times) are critically important because they provide a timeline of file activity, which can help investigators reconstruct events, identify suspicious behavior, and establish evidence. Here's how each timestamp plays a role in forensic investigations:

---

#### 1. **Modified Time (M)**
   - **What it indicates**: The last time the file's **content was changed**.
   - **Forensic significance**:
     - Helps determine when a file was last edited or tampered with.
     - Useful for identifying when malicious files (e.g., malware, scripts) were modified or when evidence was altered.
     - Can reveal patterns of activity, such as when a suspect was actively working on a document.

---

#### 2. **Accessed Time (A)**
   - **What it indicates**: The last time the file was **accessed or read**.
   - **Forensic significance**:
     - Shows when a file was opened or viewed, which can help establish a suspect's interaction with specific data.
     - Can be used to correlate user activity with other events (e.g., accessing a file before deleting it).
     - Note: On modern systems, accessed time updates may be disabled by default for performance reasons, so this timestamp may not always be reliable.

---

#### 3. **Created Time (C)**
   - **What it indicates**: The time the file was **created on the system**.
   - **Forensic significance**:
     - Helps determine when a file first appeared on the system, which can be useful for identifying when malware or evidence was introduced.
     - Can reveal if a file was copied or moved, as the creation time may change depending on the operation.

---
#### 4. **Birth Time (b)**
   - **What it indicates**: The time the file was **originally created** (specific to NTFS).
   - **Forensic significance**:
     - Provides the most accurate record of when a file was first created, even if it was later moved or copied.
     - Helps distinguish between the original creation time and the time it was copied to a new location.
     - Useful for tracking the origin of files, especially in cases involving data exfiltration or file tampering.

---
### **Key Uses in Digital Forensics**

1. **Timeline Analysis**:
   - Investigators use MAC(b) times to build a timeline of file activity, which can help reconstruct events leading up to an incident (e.g., a cyberattack, data breach, or unauthorized access).

2. **Identifying Tampering**:
   - Discrepancies between MAC(b) times can indicate file tampering. For example, if the modified time is earlier than the created time, it may suggest that the timestamps were manually altered.

3. **Correlating User Activity**:
   - MAC(b) times can be cross-referenced with other evidence, such as log files, user accounts, and network activity, to establish a suspect's actions.

4. **Malware Analysis**:
   - MAC(b) times can reveal when malicious files were created, modified, or executed, helping investigators understand the timeline of an attack.

5. **Data Recovery and Deletion Analysis**:
   - When files are deleted, their MAC(b) times may still be recoverable from the file system metadata, providing clues about when the files were created, accessed, or modified before deletion.

6. **Provenance of Evidence**:
   - MAC(b) times help establish the authenticity and integrity of digital evidence, which is critical for legal proceedings.

---
#### **Challenges and Considerations**

- **Timestamp Manipulation**: Attackers or suspects may alter MAC(b) times to hide their activities. Forensic tools can detect such tampering by analyzing inconsistencies in the metadata.
- **Time Zone Differences**: Timestamps are often recorded in UTC, so investigators must account for local time zones when interpreting them.
- **File System Differences**: Not all file systems support birth time (e.g., FAT32), so investigators must be aware of the file system in use.
- **System Clock Changes**: If the system clock was altered, MAC(b) times may be inaccurate. Investigators may need to cross-reference with external logs to verify timestamps.

---
#### **Tools for Analyzing MAC(b) Times**

Forensic investigators use specialized tools to extract and analyze MAC(b) times, such as:

- **Autopsy**: A digital forensics platform that can parse NTFS metadata.
- **FTK Imager**: A tool for imaging and analyzing file systems.
- **EnCase**: A comprehensive forensic tool for analyzing file metadata.
- **The Sleuth Kit (TSK)**: An open-source toolkit for file system analysis.

---
#### **Example Scenario**

Imagine a suspect is accused of stealing sensitive documents. Investigators analyze the MAC(b) times of the files in question:
- The **Created Time** shows when the files were first placed on the suspect's system.
- The **Modified Time** indicates when the files were last edited, possibly to remove incriminating content.
- The **Accessed Time** reveals when the suspect last opened the files.
- The **Birth Time** confirms the original creation date, which may differ if the files were copied from another source.

By correlating these timestamps with other evidence (e.g., login logs, network activity), investigators can build a compelling case.

In summary, MAC(b) times are a cornerstone of digital forensics, providing critical insights into file activity and helping investigators uncover the truth behind digital incidents.

---
### General Rules for Timestamps in the Windows NTFS File System

The table below delineates the general rules governing how various file operations influence the timestamps within the Windows NTFS (New Technology File System).

| Opeartion   | Modified       | Accessed | Birth (Created) |
| ----------- | -------------- | -------- | --------------- |
| File Create | Yes            | Yes      | Yes             |
| File Modify | Yes            | No       | No              |
| File Copy   | No (Inherited) | Yes      | Yes             |
| File Access | No             | No*      | No              |
1. **File Create**:

	- `Modified Timestamp (M)`: The modified timestamp is updated to reflect the time of file creation.
	- `Accessed Timestamp (A)`: The Accessed timestamp is updated to reflect that the file was accessed at the time of creation.
	- `Birth (Created) Timestamp (b)`: The Birth timestamp is set to the time of file creation.

2. **File Modify**:

	- `Modified Timestamp (M)`: The Modified timestamp is updated to reflect the time when the file's content or attributes were last modified.
	- `Accessed Timestamp (A)`: The Accessed timestamp is not updated when the file is modified.
	- `Birth (Created) Timestamp (b)`: The Birth timestamp is not updated when the file is modified.

3. **File Copy**: 

	- `Modified Timestamp (M)`: The Modified timestamp is typically not updated when a file is copied. It usually inherits the timestamp from the source file. 
	- `Accessed Timestamp (A)`: The Accessed timestamp is updated to reflect that the file was accessed at the time of copying.
	- `Birth (Created) Timestamp (b)`: The Birth timestamp is updated to the time of copying, indicating when the copy was created.

4. **File Access**:

	- `Modified Timestamp (M)`: The Modified timestamp is not updated when the file is accessed. 
	- `Accessed Timestamp (A)`: The Accessed timestamp is updated to reflect the time of access.
	- `Birth (Created) Timestamp (b)`: The Birth timestamp is not updated when the file is accessed.

All these timestamps reside in the `$MFT` file, located at the root of the system drive. While the `$MFT` file will be covered in greater depth later, our current focus remains on understanding these timestamps.

These timestamps are housed within the `$MFT` across two distinct attributes:

- `$STANDARD_INFORMATION`
- `$FILE_NAME`

The timestamps visible in the Windows file explore are derived from the `$STANDARD_INFORMATION` attribute.
### Timestomping Investigation

Identifying instances of timestamp manipulation, commonly referred to as **timestomping** ([T1070.006](https://attack.mitre.org/techniques/T1070/006/)),presents a formidable challenge in digital forensics. Timestomping entails the *alteration of file timestamps to **obfuscate** the sequence of file activities*. This tactic is frequently employed by various tools, as illustrated in the MITRE ATT&CK's timestomp technique.

![](https://i.imgur.com/rPcNSbC.png)

When adversaries manipulate file creation times or deploy tools for such purposes, the timestamp displayed in the file explorer *undergoes modification*.

For instance, if we load `C:\Users\johndoe\Desktop\forensic_data\kape_output\$MFT` into `MFT Explorer` (available at `C:\Users\johndoe\Desktop\Get-ZimmermanTools\net6\MFTExplorer`) we will notice that the creation time of the file `ChangedFileTime.txt` has been tampered with, displaying `03-01-2022` in the file explorer, which deviates from the actual creation time. 

**Note**: `MFT Explorer` will take 15-25 minutes to load the file. 

![](https://i.imgur.com/2tkDpwH.png)

However, given our knowledge that the timestamps in the file explorer originate from the `$STANDARD_INFORMATION` attribute, we can cross-verify this data with the timestamps from the `$FILE_NAME` attribute through `MFTEcmd` as follows:

```powershell
PS C:\Users\johndoe\Desktop\Get-ZimmermanTools\net6> .\MFTECmd.exe -f 'C:\Users\johndoe\Desktop\forensic_data\kape_output\D\$MFT' --de 0x16169
MFTECmd version 1.2.2.1

Author: Eric Zimmerman (saericzimmerman@gmail.com)
https://github.com/EricZimmerman/MFTECmd

Command line: -f C:\Users\johndoe\Desktop\forensic_data\kape_output\D\$MFT --de 0x16169

Warning: Administrator privileges not found!

File type: Mft

Processed C:\Users\johndoe\Desktop\forensic_data\kape_output\D\$MFT in 3.4924 seconds

C:\Users\johndoe\Desktop\forensic_data\kape_output\D\$MFT: FILE records found: 93,615 (Free records: 287) File size: 91.8MB


Dumping details for file record with key 00016169-00000004

Entry-seq #: 0x16169-0x4, Offset: 0x585A400, Flags: InUse, Log seq #: 0xCC5FB25, Base Record entry-seq: 0x0-0x0
Reference count: 0x2, FixUp Data Expected: 04-00, FixUp Data Actual: 00-00 | 00-00 (FixUp OK: True)

**** STANDARD INFO ****
  Attribute #: 0x0, Size: 0x60, Content size: 0x48, Name size: 0x0, ContentOffset 0x18. Resident: True
  Flags: Archive, Max Version: 0x0, Flags 2: None, Class Id: 0x0, Owner Id: 0x0, Security Id: 0x557, Quota charged: 0x0, Update sequence #: 0x8B71F8

  Created On:         2022-01-03 16:54:25.2726453
  Modified On:        2023-09-07 08:30:12.4258743
  Record Modified On: 2023-09-07 08:30:12.4565632
  Last Accessed On:   2023-09-07 08:30:12.4258743

**** FILE NAME ****
  Attribute #: 0x3, Size: 0x78, Content size: 0x5A, Name size: 0x0, ContentOffset 0x18. Resident: True

  File name: CHANGE~1.TXT
  Flags: Archive, Name Type: Dos, Reparse Value: 0x0, Physical Size: 0x0, Logical Size: 0x0
  Parent Entry-seq #: 0x16947-0x2

  Created On:         2023-09-07 08:30:12.4258743
  Modified On:        2023-09-07 08:30:12.4258743
  Record Modified On: 2023-09-07 08:30:12.4258743
  Last Accessed On:   2023-09-07 08:30:12.4258743

**** FILE NAME ****
  Attribute #: 0x2, Size: 0x80, Content size: 0x68, Name size: 0x0, ContentOffset 0x18. Resident: True

  File name: ChangedFileTime.txt
  Flags: Archive, Name Type: Windows, Reparse Value: 0x0, Physical Size: 0x0, Logical Size: 0x0
  Parent Entry-seq #: 0x16947-0x2

  Created On:         2023-09-07 08:30:12.4258743
  Modified On:        2023-09-07 08:30:12.4258743
  Record Modified On: 2023-09-07 08:30:12.4258743
  Last Accessed On:   2023-09-07 08:30:12.4258743

**** DATA ****
  Attribute #: 0x1, Size: 0x18, Content size: 0x0, Name size: 0x0, ContentOffset 0x18. Resident: True

  Resident Data

  Data:

    ASCII:
    UNICODE:
```

![](https://i.imgur.com/ewfIaZY.png)

![](https://i.imgur.com/daRkvaY.png)

In standard Windows file systems like NTFS, regular users typically lack the permissions to directly modify the timestamps of filenames in `$FILE_NAME`. Such modifications are exclusively within the purview of the system kernel.

To kickstart our exploration, let's first acquaint ourselves with filesystem-based artifacts. We'll commence with the `$MFT` file, nestled in the root directory of the KAPE output.
### MFT File

The `$MFT` file, commonly referred to as the [Master File Table](https://learn.microsoft.com/en-us/windows/win32/fileio/master-file-table), is an integral part of the NTFS (New Technology File System) used by contemporary Windows operating systems. 

