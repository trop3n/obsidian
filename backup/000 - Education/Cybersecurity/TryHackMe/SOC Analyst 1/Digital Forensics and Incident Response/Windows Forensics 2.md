#windows #DFIR #forensics

# Introduction

We learned about Windows Forensics in the previous room and practiced forensic artifacts from the Windows Registry. We learned about gathering system information, user information, files and folders accessed, programs run, and external devices connected to the system, all from the Windows registry.

However, the registry is not the only place where forensic artifacts are present. In this room, we will learn about forensic artifacts in other places. We will learn about the different file systems commonly used by Windows and where to look in these file systems when looking for artifacts. We will identify locations and artifacts to prove evidence of execution, file/folder usage or knowledge, and external device usage. We will also cover the basics of recovering deleted files. We will use [Eric Zimmerman's tools](https://ericzimmerman.github.io/#!index.md) to parse information present in the artifacts for most of this room. We already used Registry Explorer and ShellBags Explorer in the previous room. For some of the tasks, we will use Autopsy. 

# The FAT File Systems

A storage device in a computer system, for example, a hard disk drive or a USB device, is just a collection of bits. To convert these bits into meaningful information, they need to be organized. For this purpose, computer scientists and engineers have created different file systems that organize the bits in a hard drive as per a standard, so that information stored in these bits can be interpreted easily. 

## The File Allocation Table (FAT):

The File Allocation Table (FAT) is one of these file systems. It has been the default file system for Microsoft Operating Systems since at least the late 1970's and is till in use, though not the default anymore. 

As the name suggests, the File Allocation Table creates a table that indexed the location of bits that are allocated to different files. If you are interested in the history of the FAT file system, you can head to the [Wikipedia page](https://en.wikipedia.org/wiki/File_Allocation_Table) for it.

## Data Structures of the FAT File System:

The FAT file system supports the following Data Structures:

### Clusters

> A **cluster** is a basic storage unit of the FAT file system. Each file stored on a storage device can be considered a group of clusters containing bits of information.

### Directory

> A directory contains information about file identification, like file name, starting cluster, and filename length.

### File Allocation Table

The File Allocation Table is a linked list of all the clusters. It contains the status of the cluster and the pointer to the next cluster in the chain.

In summary, the bits that mkae up a file are stored in clusters. All the filenames on a file system, their starting clusters, and their lengths are stored in directories. And the location of each cluster on the disk is stored in the File Allocation Table. We can see that we started with a raw disk composed of bits and organized it to define what group of bits refers to what file stored on the disk.

## FAT12, FAT16, and FAT32

The FAT file format divides the available disk space into clusters for more straightforward addressing. The number of these clusters depends on the number of bits used to address the cluster. Hence the different variations of the FAT file system. FAT was initially developed with 8-bit cluster addressing, and it was called the FAT Structure. Later, as the storage needed to be increased, FAT12, FAT16 and FAT32 were introduced. The last one of them was introduced in 1996.

Theoretically, FAT12 used 12-bit cluster addressing for a maximum of 4096 clusters (2^12). FAT16 used 16-bit cluster addressing for a maximum of 65,536 clusters (2^16). In the case of FAT32, the actual bits used to address clusters are 28, so the maximum number of clusters is actually 268,435,456 or 2^28.

However, not all of these clusters are used for file storage. Some are used for administrative purposes, e.g. to store the end of a chain of clusters, the unusable parts of the disk, or other such purposes. 

The following table summarizes the information as mentioned earlier and how it impacts the maximum volume and sizes.

The following table summarizes the information as mentioned earlier and how it impacts the maximum volume and file sizes:

| **Attribute**                  | **FAT12**  | **FAT16**  | **FAT32**   |
| ------------------------------ | ---------- | ---------- | ----------- |
| **Addressable bits**           | 12         | 16         | 28          |
| **Max number of clusters**     | 4,096      | 65,536     | 268,435,456 |
| **Supported size of clusters** | 512B - 8KB | 2KB - 32KB | 4KB - 32KB  |
| **Maximum Volume size**        | 32MB       | 2GB        | 2TB         |
Even though the maximum volume size for FAT32 is 2TB, Windows limits formatting to only 32GB. However, volume sizes formatted on the other OS with larger volume sizes are supported by Windows. 

The chances of coming across a FAT12 filesystem are rare nowadays. FAT16 and FAT32 are still used in some places, like USB drives, SD cards or Digital Cameras. However, the maximum volume size and the maximum file size (4GB - 1 file size for both FAT16 and FAT32) are limiting factors that have reduced their usage. 

## The exFAT File System

As the file sizes have grown, especially with higher resolution images and vides being supported by the newer digital cameras, the maximum file size limit of FAT32 became a substantial limiting factor for camera manufacturers. Though Microsoft had moved on to the NTFS file system, it was not suitable for digital media devices as they did not need the added security features and the overhead that came with it. Therefore, these manufacturers lobbied Microsoft to create the exFAT file system.

The exFAT file system is now the default for SD cards larger than 32GB. It has also been adopted widely by most manufacturers of digital devices. The exFAT file system supports a cluster size of 4KB to 32MB. It has a maximum file size and a maximum volume size of 128PB (Petabytes). It also reduces some of the overheads of the FAT file system to make it lighter and more efficient. It can have a maximum of 2,796,202 files per directory.

# The NTFS File System

As observed in the previous task, the FAT file system is a very basic file system. It does the job when it comes to organizing our data, but it offers little more in terms of security, reliability and recovery capabilities. It also has certain limitations when it comes to file and volume sizes. Hence, Microsoft developed a newer file system called the New Technology File System (NTFS) to add these features. This file system was introduced in 1993 with the Windows NT 3.1. However it became mainstream since Windows XP. The NTFS file system resolves many issues present in the FAT file system and introduces a lot of new features. We will discuss some of the features below.

## Journaling

The NTFS file system keeps a log of changes to the metadata in the volume. This feature helps the system recover from a crash or data movement due to defragmentation. This log is stored in $LOGFILE in the volume's root directory. Hence, the NTFS file system is called a journaling file system.

## Access Controls

The FAT file system did not have access controls based on the user. The NTFS file system has access controls that define the owner of a file/directory and permissions for each users.

## Volume Shadow Copy

The NTFS file system keeps track of changes made to a file using a feature called Volume Shadow Copies. Using this feature, a user can restore previous file versions for recovery or system restore. In recent ransomware attacks, ransomware actors have been noted to delete the shadow copies on a victim's file systems to prevent them from recovering their data. 

## Alternate Data Streams

A file is a stream of data organized in a file system, Alternate Data Streams (ADS) is a feature in NTFS that allows files to have multiple streams of data stored in a single file. Internet Explorer and other browsers use Alternate Data Streams to identify files downloaded from the internet (using the ADS Zone Identifier). Malware has also been observed to hide their code in ADS.

## **Master File Table**

Like the File Allocation Table, there is a Master File Table in NTFS. However, the Master File Table, or MFT, is much more extensive than the File Allocation Table. It is a structured database that tracks the objects stored in a volume. Therefore, we can say that the NTFS file system data is organized in the Master file Table. From a forensics perspective, the following are some of the critical files in the MFT:

### $MFT

The $MFT is the first record in the volume. The **Volume Boot Record (VBR)** points to the cluster where it is located. $MFT stores information about the clusters where all other objects present on the volume are located. This file contains a directory of all the files present on the volume. 

### $LOGFILE

The $LOFGILE stores the *transactional logging of the file system*. It helps maintain the integrity of the file system in the event of a crash.

### $UsnJrnl

It stands for the Update Sequence Number (USN) Journal. It is present in the $Extend record. It contains information about all the files that *were changed* in the file system and the reason for the change. It is also the change journal.

### MFT Explorer

MFT Explorer is one of Eric Zimmerman's tools used to explore MFT files. It is available on both the command line and GUI versions. We will be using the CLI version for this task. 

> Open an elevated command prompt and click `Run as Administrator`. Navigate to the directory `C:\Users\THM-4n6\Desktop\Eztools` and run the command `MFTECmd.exe`. You will see the following options:

![](https://i.imgur.com/TQeBlBC.png)

MFTECmd parses data from the different files created by the NTFS file system like $MFT, $Boot, etc. The above screenshot shows the available options for parsing MFT files. For parsing the $MFT file, we can use the following command:

`MFTECmd.exe -f <path-to$MFT-file> --csv <path-to-save-results-in csv>`

You can then use the EZviewer tool inside the EZtools folder to view the output of MFTECmd, or to view CSV files in the next tasks as well. You will see that it lists information about all the files present on the volume. You can similarly parse the $Boot file, which will provide information about the boot sector of the volume. MFTECmd doesn't support $LOGFILE as of now.

Let's parse the MFT files present on the location `C:\users\THM-4n6\Desktop\triage\C\` in the attached VM and answer the questions below. Currently, MFTECmd.exe doesn't support $Logfile.

# Recovering Deleted Files

Understanding the file systems makes it easier to know how files are deleted, recovered, and wiped. As we learned in the previous two tasks, a file system stores the location of a file on the disk in a table or a database. When we delete a file from the file system, the file system deletes the entries that store the file's location on the disk. For the file system, the location where the file existed is now available for writing or unallocated. However, the file contents on disk are still there, as long as they are are not overwritten by the file system while copying another file or by the disk firmware while performing maintenance on the disk.

Similarly, there is data on the disk in different unallocated clusters, which can possibly be recovered. To recover this data, we have to understand the file structure of different file types to identify the specific file through the data we see in a hex editor. However, we will not cover that in this room. What we will do, is to use a tool that does this work for us and identifies deleted files in a disk image file. But what is a disk image file?

## Data Image

A  disk image file is a file that contains a bit-by-bit copy of a disk drive. A bit-by-bit copy saves all the data in a disk image file, including the metadata, in a single file. Thus, while performing forensics, one can make several copies of the physical evidence, i.e. the disk, and use them for investigation. This helps in two ways. 

1. The original evidence is not contaminated while performing forensics, and
2. The disk image file can be copied to another disk and analyzed without specialized hardware.

## Recovering Files with Autopsy

With that out of the way, let's see how we can recover deleted files from a disk. We will use Autopsy for recovering deleted files. For a room dedicated to Autopsy, you can go [here](https://tryhackme.com/room/btautopsye0). 

On the attached VM, you will find an icon for Autopsy on the Desktop. Double-click it to run Autopsy. You will be greeted with the following screen:

![](https://i.imgur.com/vlkqbwC.png)

> Click on the 'New Case' option. You will find a window similar to the following:

![](https://i.imgur.com/uSRBSYG.png)

> Enter a name to save your case by, and click Next. 

![](https://i.imgur.com/kUkpIqJ.png)

> You can add the required details here. For now, we can click finish to move forward. Autopsy will perform some processing and then show the following screen. Click Next to move forward.

![](https://i.imgur.com/bRp5Py5.png)

![Uploading file...2vuvv]()

> You will see this screen. Since we will be performing analysis on a disk image, select the topmost option, Disk Image or VM File.

![](https://i.imgur.com/977LOwZ.png)

> It will ask you for the location of the data source.

![](https://i.imgur.com/TwNLZkP.png)

> Provide the location of the data source. You will find a disk image named 'usb.001' on the Desktop. Provide the path to that file in the above window and click next. You will see the following window:

![](https://i.imgur.com/St0nuj1.png)

> Here, click Deselect All. These are different modules that Autopsy runs on the data for processing. For this task, we don't need any of these. If enabled, they take a lot of time to run. Click Next after clicking Deselect All. Autopsy will load the disk image. You will see the following in the left panel.

![](https://i.imgur.com/2ecidBp.png)

> The Data Sources show the data sources that we have added to Autopsy. We can add more sources as well. The File Views and Tags menus show what Autopsy has found after processing the data. Expand the Data Sources, and lick on the usb.001 device. Autopsy will show the contents of the disk image in the following way:

![](https://i.imgur.com/6If2GFF.png)

The contents of the disk are shown on the right side. All the files and folders present in the disk are listed in the upper tab. In the lower tab, details about the selected files are shown. There are different options to see the details here. You can check them out to find interesting information.

Notice the X mark on the last file in the screenshot above, named New Microsoft Excel Worksheet.xlsx-RFcd07702.TMP. This indicates that this is a deleted file. Deleted files will have this X mark on them. To recover a deleted file, right-click on it, and select the Extract File(s) option.

![](https://i.imgur.com/ianyEJg.png)

> Provide the path to save the extracted file, and you will have your deleted file recovered. Now let's see what other deleted files you can find on this disk image and answer the following questions.

# Evidence of Execution

Now that we have learned about the File system, let's learn where to find artifacts present in the file system to perform forensic analysis. In this task, we will look into the artifacts that provide us evidence of execution. 

## Windows Prefetch Files

When a program is run in Windows, it stores its information for future use. This stored information is used to load the program quickly in case of frequent use. This information is stored in prefetch files which are located in the `C:\Windows\Prefetch` directory.

Prefetch files have an extension of `.pf`. Prefetch files contain *the last run times of the application, the number of times the application was run, and any files and device handles used by the file*. Thus it forms an excellent source of information about the last executed programs and files.

We can use Prefetch Parset (PECmd.exe) from Eric Zimmerman's tools for parsing Prefetch files and extracting data. When we run PECmd.exe in an elevated command prompt, we get this output:

![](https://i.imgur.com/ouLOE4A.png)

> To run Prefetch Parser on a file and save the results in a CSV, we can use the following command:

`PMCmd.exe -f <path-to-Prefetch-files> --csv <path-to-save-csv>`

Similarly, for parsing a while directory, we can use the following command:

`PECmd.exe -d <path-to-Prefetch-directionary> --csv <path-to-save-csv>`

We can use this information to answer the questions at the end.

## Windows 10 Timeline

Windows 10 stores recently used applications and files in an SQLite database called the Windows 10 timeline. This data can be a source of information about the last executed programs. It contains the application that was executed and the focus time of the application. The Windows 10 timeline can be found at the following location:

```
C:\Users\<username>\AppData\Local\ConnectedDevicesPlatform\{randomfolder}\ActivitiesCache.db
```

We can use Eric Zimmerman's WxTCmd.exe for parsing Windows 10 Timeline. We get the following options when we run it:

```shell-session
user@machine$ WxTCmd.exe

WxTCmd version 0.6.0.0

Author: Eric Zimmerman (saericzimmerman@gmail.com)
https://github.com/EricZimmerman/WxTCmd

        f               File to process. Required
        csv             Directory to save CSV formatted results to. Be sure to include the full path in double quotes
        dt              The custom date/time format to use when displaying timestamps. See https://goo.gl/CNVq0k for options. Default is: yyyy-MM-dd HH:mm:ss

Examples: WxTCmd.exe -f "C:\Users\eric\AppData\Local\ConnectedDevicesPlatform\L.eric\ActivitiesCache.db" --csv c:\temp

          Database files are typically found at 'C:\Users\\AppData\Local\ConnectedDevicesPlatform\L.\ActivitiesCache.db'

          Short options (single letter) are prefixed with a single dash. Long commands are prefixed with two dashes

-f is required. Exiting
```

We can use the following command to run WxTCmd:

`WxTCmd.exe -f <path-to-timeline-file> --csv <path-to-save-csv>`

## Windows Jump Lists

Windows introduced **Jump Lists** to help users go directly to their recently used files from the taskbar. We can view jumplists by right-clicking an application's icon in the taskbar, and it will show us the recently opened files in that application. This data is stored in the following directory:

```
C:\Users\<username>\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations
```

Jumplists include information about the applications executed, first time of execution, and last time of execution of the application against an AppID.

> We can use Eric Zimmerman's JLECmd.exe to parse Jump Lists. We get the following options when we run it:

```shell-session

user@machine$ JLECmd.exe

JLECmd version 1.4.00


Author: Eric Zimmerman (saericzimmerman@gmail.com)
https://github.com/EricZimmerman/JLECmd

        d               Directory to recursively process. Either this or -f is required
        f               File to process. Either this or -d is required
        q               Only show the filename being processed vs all output. Useful to speed up exporting to json and/or csv. Default is FALSE

        all             Process all files in directory vs. only files matching *.automaticDestinations-ms or *.customDestinations-ms. Default is FALSE

        csv             Directory to save CSV formatted results to. Be sure to include the full path in double quotes
        csvf            File name to save CSV formatted results to. When present, overrides default name

        html            Directory to save xhtml formatted results to. Be sure to include the full path in double quotes
        json            Directory to save json representation to. Use --pretty for a more human readable layout
        pretty          When exporting to json, use a more human readable layout. Default is FALSE

        ld              Include more information about lnk files. Default is FALSE
        fd              Include full information about lnk files (Alternatively, dump lnk files using --dumpTo and process with LECmd). Default is FALSE

        appIds          Path to file containing AppIDs and descriptions (appid|description format). New appIds are added to the built-in list, existing appIds will have their descriptions updated
        dumpTo          Directory to save exported lnk files
        withDir         When true, show contents of Directory not accounted for in DestList entries
        Debug           Debug mode

        dt              The custom date/time format to use when displaying timestamps. See https://goo.gl/CNVq0k for options. Default is: yyyy-MM-dd HH:mm:ss
        mp              Display higher precision for timestamps. Default is FALSE

Examples: JLECmd.exe -f "C:\Temp\f01b4d95cf55d32a.customDestinations-ms" --mp
          JLECmd.exe -f "C:\Temp\f01b4d95cf55d32a.automaticDestinations-ms" --json "D:\jsonOutput" --jsonpretty
          JLECmd.exe -d "C:\CustomDestinations" --csv "c:\temp" --html "c:\temp" -q
          JLECmd.exe -d "C:\Users\e\AppData\Roaming\Microsoft\Windows\Recent" --dt "ddd yyyy MM dd HH:mm:ss.fff"

          Short options (single letter) are prefixed with a single dash. Long commands are prefixed with two dashes

Either -f or -d is required. Exiting
```

> We can use the following command to parse jumplists using JLECmd.exe:

`JLECmd.exe -f <path-to-Jumplist-file> --csv <path-to-save-csv>`

In the folder named `triage`, present on the Desktop of the attached machine, we have extracted the Windows directory of a system we want to investigate. It retains the directory structure of the original Windows directory, that is, `C:\Windows` directory from the system is mapped on to `C:\users\thm-4n6\Desktop\Triage\C\Windows`. Now let's use the information we have learned to perform analysis on the data saved in the folder named `triage` on the Desktop in the attached VM and answer the following questions.

# File/Folder Knowledge

## Shortcut Files

Windows creates a shortcut file for each file opened either locally or remotely. The shortcut files contain information about the first and last opened times of the file and the path of the opened file, along with some other data. Shortcut files can be found in the following locations:

```
C:\Users\<username>\AppData\Roaming\Microsoft\Windows\Recent\
C:\Users\<username>\AppData\Roaming\Microsoft\Office\Recent\
```

We can use Eric Zimmerman's LECmd.exe (Lnk Explorer) to parse shortcut files. When we run LECmd.exe, we see the following options:

```shell-session

Author: Eric Zimmerman (saericzimmerman@gmail.com)
https://github.com/EricZimmerman/LECmd

        d               Directory to recursively process. Either this or -f is required
        f               File to process. Either this or -d is required
        q               Only show the filename being processed vs all output. Useful to speed up exporting to json and/or csv. Default is FALSE

        r               Only process lnk files pointing to removable drives. Default is FALSE
        all             Process all files in directory vs. only files matching *.lnk. Default is FALSE

        csv             Directory to save CSV formatted results to. Be sure to include the full path in double quotes
        csvf            File name to save CSV formatted results to. When present, overrides default name

        xml             Directory to save XML formatted results to. Be sure to include the full path in double quotes
        html            Directory to save xhtml formatted results to. Be sure to include the full path in double quotes
        json            Directory to save json representation to. Use --pretty for a more human readable layout
        pretty          When exporting to json, use a more human readable layout. Default is FALSE

        nid             Suppress Target ID list details from being displayed. Default is FALSE
        neb             Suppress Extra blocks information from being displayed. Default is FALSE

        dt              The custom date/time format to use when displaying time stamps. See https://goo.gl/CNVq0k for options. Default is: yyyy-MM-dd HH:mm:ss
        mp              Display higher precision for time stamps. Default is FALSE

Examples: LECmd.exe -f "C:\Temp\foobar.lnk"
          LECmd.exe -f "C:\Temp\somelink.lnk" --json "D:\jsonOutput" --jsonpretty
          LECmd.exe -d "C:\Temp" --csv "c:\temp" --html c:\temp --xml c:\temp\xml -q
          LECmd.exe -f "C:\Temp\some other link.lnk" --nid --neb
          LECmd.exe -d "C:\Temp" --all

          Short options (single letter) are prefixed with a single dash. Long commands are prefixed with two dashes

Either -f or -d is required. Exiting
```

> We can use the following command to parse shortcut files using LECmd.exe:

```
LECmd.exe -f <path-to-shortcut-files> --csv <path-to-save-csv>
```

The creation data of the shortcut file points to the date/time when the file was first opened. The date/time of modification of the shortcut file points to the last time the file was accessed.

## IE/Edge History

An interesting thing about the IE/Edge browsing history is that it includes files opened in the system as well, whether those files were opened using the browser or not. Hence, a valuable source of information on opened files in a system is the IE/Edge history. We can access the history in the following location:

```
C:\Users\<username>\AppData\Local\Microsoft\Windows\WebCache\WebCacheV*.dat
```

The files/folders accessed appear with a `file:///*` prefix in the IE/Edge history. Though several tools can be used to analyze Web cache data, you can use Autopsy to do so in the attached VM. For doing that, select Logical Files as a data source. 

![](https://i.imgur.com/QQCjMnT.png)

> it will then ask you to select the path from which you want files to be analyzed. You can provide the path to the triage folder. 

![](https://i.imgur.com/aedrsiZ.png)

> In the Window where Autopsy asks about ingest modules to process data, check the box in front of "Recent Activity" and uncheck everything else.

![](https://i.imgur.com/MWdac64.png)

> You will be able to view local files accessed in the Web history option in the left panel. 

![](https://i.imgur.com/g6b1nSX.png)

This is what it will look like in the right panel.

![](https://i.imgur.com/jA3FbZb.png)

> As shown above, the 'Data Artifacts' tab displays information about the file accessed.

## Jump Lists

As we already learned in the last task, Jump Lists create a list of the last opened files. This information can be used to identify both the last executed programs and the last opened files in a system. Remembering from the last task, Jump Lists are present at the following location:

```
C:\Users\<username>\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations
```

We have already learned about parsing jump lists in the previous task, so it won't be gone over again. 

# External Devices | USB Device Forensics

## Setupapi Dev Logs for USB Devices

When any new device is attached to a system, information related to the setup of that device is stored in the `setupapi.dev.log`. This log is present at the following location:

```
C:\Windows\inf\setupapi.dev.log
```

This log contains the device serial number and the first/last times when the device was connected.

![](https://i.imgur.com/tKpQUwj.png)

> Here is what it looks like when opened in Notepad.exe. Notice the first line where we can see the device ID and Serial Number.

## Shortcut Files

As we learned in the previous task, shortcut files are created automatically by Windows for files opened locally or remotely. These shortcut files can sometimes provide us with information about connected USB devices. It can provide us with information about the volume name, type and serial number. Recalling from the previous task, this information can be found at:

```
C:\Users\<username>\AppData\Roaming\Microsoft\Windows\Recent
C:\Users\<username>\AppData\Roaming\Microsoft\Office\Recent
```

As we have already learned about parsing Shortcut files using Eric Zimmerman's LECmd.exe in a previous task, we will not go over it again.

