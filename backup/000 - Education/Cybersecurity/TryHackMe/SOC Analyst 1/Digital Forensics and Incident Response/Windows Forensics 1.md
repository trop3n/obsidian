#DFIR #tryhacke #Windows #cybersecurity 
# Introduction to Computer Forensics for Windows:

Computer forensics is an essential field of cybersecurity that involves gathering evidence of activities performed on computers. It is part of the wider **Digital Forensics** field, which deals with forensic analysis of all types of digital devices, including recovering, examining, and analyzing data found in digital devices. The applications of digital and computer forensics are wide-ranging, from the legal sphere, where it is used to support or refute a hypothesis in a civil or criminal case, to the private sphere, where it helps in internal corporate investigations and incident and intrusion analysis.

A perfect example of Digital Forensics solving a criminal case is the [BTK serial killer](https://en.wikipedia.org/wiki/Dennis_Rader) case. This case had gone cold for more than a decade when the killer started taunting the police by sending letters. The case took a major turn when he sent a floppy disk to a local news station that was later taken into evidence by the police. The police were able to recover a deleted word document on the drive, and using the metadata and some other evidence, they pinpointed and arrested him.

Microsoft Windows is by large the most used Desktop Operating System right now. Private users and Enterprises prefer it, and it currently holds roughly 80% of the Desktop market share. This means that it is important to know how to perform forensic analysis on Microsoft Windows for someone interested in Digital Forensics. In this module, we will learn about the different ways we can gather forensic data from the Windows Registry and make conclusions about the activity performed on a Windows system based on this data. 

## Forensic Artifacts:

When performing forensic analysis, you will often hear the word 'artifact'. Forensic artifacts are essential pieces of information evidence of human activity.

- For example, during the investigation of a crime scene, fingerprints, a broken button of a shirt or coat, the tools used to perform the crime are all considered forensic artifacts. All of these artifacts are combined to recreate the story of how the crime was committed.

In computer forensics, forensic artifacts can be small footprints of activity left on the computer system. On a Windows system, a person's actions can be traced back quite accurately using computer forensics because of the various artifacts a Windows system creates for a given activity. These artifacts often reside in locations 'normal' users won't typically venture to. For our purposes, these artifacts can be analyzed to provide the trial of activity for an investigation.

## So, Is My Computer Spying on Me?

What do you think?

A Windows system keeps track of a lot of activity performed by a user. But is all that tracking for malicious purposes, or is there another reason for that? As we'll see in this room, the filesystem components that forensic experts deem artifacts primarily originated from Microsoft's effort to improve the user's experience. \

Assuming the same build of Windows is installed on a system, excluding the actions taken during installation, the out-of-the-box experience is similar for all users. However, this time, each user personalizes their computer according to their preferences. These preferences include the Desktop layout and icons, the bookmarks in the internet browser, the name of the user, installing of different applications, and logging in to different accounts for each of these applications and other accounts using the internet browser. 

Windows saves these preferences to make your computer more personalized. However, forensic investigators use these preferences as artifacts to identify the activity performed on a system. So while your computer might be spying on you, it is not for the explicit reason of spying, instead to make it more pleasant to use the computer according to your taste. But that same information is used by forensic investigators to perform forensic analysis. As we move through this room, we'll see that Windows stores these artifacts in different locations throughout the file system such as in the registry, a user's profile directory, in application-specific files, etc.

# Windows Registry and Forensics

The Windows Registry is a collection of databases that contain the system's configuration data. This configuration data can be about the hardware, the software, or the user's information. It also includes data about the recently used files, programs used, or devices connected to the system. As you can understand, this data is beneficial from a forensics standpoint. Throughout the room, we will learn ways to read this data to identify the required information about the system. You can view the registry using `regedit.exe`, a built-in Windows utility to view and edit the registry. We'll explore other tools to learn about the registry in the upcoming tasks.

The Windows Registry consists of **Keys** and **Values**. When you open the regedit.exe utility to view the registry, the folders you see are Registry Keys. Registry Values are the data stored in these Registry keys. A [Registry Hive](https://docs.microsoft.com/en-us/windows/win32/sysinfo/registry-hives#:~:text=Registry%20Hives.%20A%20hive%20is%20a%20logical%20group,with%20a%20separate%20file%20for%20the%20user%20profile.) is a group of Keys, subkeys, and values stored in a single file on the disk.

## Structure of the Registry

> The registry on any Windows system contains the following five root keys:

1. HKEY_CURRENT_USER
2. HKEY_USERS
3. HKEY_LOCAL_MACHINE
4. HKEY_CLASSES_ROOT
5. HKEY_CURRENT_CONFIG

You can view these keys when you open the `regedit.exe` utility. To open the registry editor, press the Windows key and the R key simultaneously. It will open a `run` prompt that looks like this:

![](https://i.imgur.com/kiInH7z.png)

> In this prompt, type `regedit.exe`, and you will be greeted by the registry editor window.

![](https://i.imgur.com/8cU7thk.png)

Here you can see the root keys in the left pane in a tree view that shows the included registry keys, and the values in the selected key are shown in the right place. You can click on the value shown in the right pane and select properties to view the properties of this value.

Here is how Microsoft defines each of these root keys. For more detail and information about the following Windows registry keys, please visit [Microsoft's documentation](https://docs.microsoft.com/en-US/troubleshoot/windows-server/performance/windows-registry-advanced-users).

| Folder/Predefined Key   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **HKEY_CURRENT_USER**   | Contains the root of the configuration information for the user who is currently logged on. The user's folders, screen colors, and Control Panel settings are stored here. This information is associated with the user's profile. This key is sometimes abbreviated as `HKCU`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| **HKEY_USERS**          | Contains all the actively loaded user profiles on the computer. HKEY_CURRENT_USER is a subkey of HKEY_USERS. HKEY_USERS is sometimes abbreviated as HKU.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| **HKEY_LOCAL_MACHINE**  | Contains configuration information particular to the computer (for any user). This key is sometimes abbreviated as HKLM.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| **HKEY_CLASSES_ROOT**   | Is a subkey of `HKEY_LOCAL_MACHINE\Software`. The information that is stored here makes sure that the correct program opens when you open a file by using Windows Explorer. This key is sometimes abbreviated as HKCR.<br><br>Starting with Windows 2000, this information is stored under both the HKEY_LOCAL_MACHINE and HKEY_CURRENT_USER keys. The `HKEY_LOCAL_MACHINE\Software\Classes` key contains default settings that can apply to all users on the local computer. The `HKEY_CURRENT_USER\Software\Classes` key has settings that override the default settings and apply only to the interactive user.<br><br>The HKEY_CLASSES_ROOT key provides a view of the registry that merges the information from these two sources. HKEY_CLASSES_ROOT also provides this merged view for programs that are designed for earlier versions of Windows. To change the settings for the interactive user, changes must be made under `HKEY_CURRENT_USER\Software\Classes` instead of under HKEY_CLASSES_ROOT.<br><br>To change the default settings, changes must be made under `HKEY_LOCAL_MACHINE\Software\Classes` .If you write keys to a key under HKEY_CLASSES_ROOT, the system stores the information under `HKEY_LOCAL_MACHINE\Software\Classes`.<br><br>If you write values to a key under HKEY_CLASSES_ROOT, and the key already exists under `HKEY_CURRENT_USER\Software\Classes`, the system will store the information there instead of under `HKEY_LOCAL_MACHINE\Software\Classes`. |
| **HKEY_CURRENT_CONFIG** | Contains information about the hardware profile that is used by the local computer at system startup.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
# Accessing Registry Hives Offline

If you are accessing a live system, you will be able to access the registry using regedit.exe, and you will be greeted with all of the standard root keys we learned about in the previous task. However, if you only have access to a disk image, you must know where the registry hives are located on the disk. The majority of these hives are located in the `C:\Windows\System32\Config` directory and are:

1. **DEFAULT** (mounted on `HKEY_USERS\DEFAULT`)
2. - **SAM** (mounted on `HKEY_LOCAL_MACHINE\SAM`)
3. **SECURITY** (mounted on `HKEY_LOCAL_MACHINE\Security`)
4. **SOFTWARE** (mounted on `HKEY_LOCAL_MACHINE\Software`)
5. **SYSTEM** (mounted on `HKEY_LOCAL_MACHINE\System`)

### Hives Containing User Information:

Apart from these hives, two other hives containing user information can be found in the User profile directory. For Windows 7 and above, a user's profile directory is located in `C:\Users\<username>` where the hives are:

1. **NTUSER.DAT** (mounted on HKEY_CURRENT_USER when a user logs in)
2. **USRCLASS.DAT** (mounted on HKEY_CURRENT_USER\Software\CLASSES)

The USRCLASS.DAT hive is located in the directory `C:\Users\<username>\AppData\Local\Microsoft\Windows`

![](https://i.imgur.com/Wk7KGo3.png)

> The **NTUSER.DAT** hive is located in the directory `C:\Users\<username>`

![](https://i.imgur.com/EExTkNA.png)

> Remember that NTUSER.DAT and USRCLASS.DAT are hidden files.

### The Amcache Hive:

Apart from these files, there is another very important hive called the AmCache hive. This hive is located in `C:\Windows\AppCompat\Programs\Amcache.hve`. Windows creates this hive to save information on programs that were recently run on the system.

## Transaction Logs and Backups:

Some other very viral sources of forensic data are the registry transaction logs and backups. The transaction logs can be considered as the journal of the changelog of the registry hive. Windows often uses transaction logs when writing data to registry hives. This means that the transaction logs can often have the latest changes in the registry that haven't made their way to the registry hives themselves. The transaction log for each hive is stored as a .LOG file in the same directory as the hive itself. It has the same name as the registry hive, but the extension is .LOG. For example, the transaction log for the SAM hive will be located `C:\Windows\System32\Config` in the same filename SAM.LOG. Sometimes there can be multiple transaction logs as well. In that case, they will have .LOG1, .LOG2 etc, as their extension. It is prudent to look at the transaction logs as well when performing registry forensics. 

Registry backups are the opposite of Transaction logs. These are the backups of the registry hives located in the `C:\Windows\System32\Config` directory. These hives are copied to the `C:\Windows\Ssytem32\Config\RegBack` directory every ten days. It might be an excellent place to look if you suspect that some registry keys might have been deleted/modified recently. 

# Data Acquisition

When performing forensics, we will either encounter a live system or an image taken of the system. For the sake of accuracy, it was recommended practice to image the system or make a copy of the required data and perform forensics on it. This process is called data acquisition. Below we discuss different ways to acquire registry data from a live system or a disk image:

Though we can view the registry editor, the forensically correct method is to acquire a copy of this data and perform analysis on that. However, when we go to copy the registry hive from `%WINDR%\System32\Config`, we cannot because it is a restricted file. So, what to do now?

For acquiring these files, we can use one of the following tools:

### KAPE:

[KAPE](https://www.kroll.com/en/services/cyber-risk/incident-response-litigation-support/kroll-artifact-parser-extractor-kape) is a live data acquisition and analysis tool which can be used to acquire registry data. It is primarily a command-line tool but also comes with a GUI. The below screenshot shows what a KAPE GUI looks like. We have already selected all the settings to extract the registry data using KAPE in this screenshot. We will learn more about collecting forensics artifacts using KAPE in a dedicated KAPE room.

![](https://i.imgur.com/4seykqf.png)

### Autopsy:

[Autopsy](https://www.autopsy.com/): gives you the opinion to acquire data from both live systems or from a disk image. After adding your data source, navigate to the location of the files you want to extract, then right-click and select the Extract File(s) option. It will look similar to what you see in the screenshot below.

![](https://i.imgur.com/AM6NcMO.png)

### FTK Imager:

[FTK Imager](https://www.exterro.com/ftk-imager) is similar to Autopsy and allows you to extract files from a disk image or a live system by mounting the said disk image or drive in FTK Imager. Below you can see the option to Export files as highlighted in the screenshot. 

![](https://i.imgur.com/Ku99ekB.png)

> Another way you can extract Registry files from FTK Imager is through the Obtain Protected Files option. This option is only available for live systems and is highlighted in the screenshot below. This option allows you to extract all registry hives to a location of your choosing. However, it will not copy the `Amcache.hve` file, which is often necessary to investigate evidence of programs that were last executed. 

![](https://i.imgur.com/XRZNzQS.png)

> For the purpose of this room, we will not be acquiring data ourselves, but instead, we will work with the attached VM that already has data.

# Exploring Windows Registry

Once we have extracted the registry hives, we need a tool to view these files as we would in the registry editor. Since the registry editor only works with live systems and can't load exported hives, we can use the following tools:

## Registry Viewer:

As we can see in the screenshot below, [AccessData's Registry Viewer](https://accessdata.com/product-download/registry-viewer-2-0-0) has a similar user interfce to the Windows Registry Editor. There are a couple of limitations, though. It only loads one hive at a time, and it can't take the transaction logs into account.

![](https://i.imgur.com/uB0nbu5.png)

## Zimmerman's Registry Explorer:

Eric Zimmerman has developed a handful of [tools](https://ericzimmerman.github.io/#!index.md) that are very useful for performing Digital Forensics and Incident Response. One of them is the Registry Explorer. It looks like the below screenshot. It can load multiple hives simultaneously and add data from transaction logs into the hive to make a more 'cleaner' hive with more up-to-date data. It also has a handy 'Bookmarks' option containing forensically important registry keys often sought by forensics investigators. Investigators can go straight to the interesting registry keys and values with the bookmarks menu items. We will explore these is more detail in the upcoming tasks. 

![](https://i.imgur.com/H7Ldd8h.png)

## RegRipper:

[RegRipper](https://github.com/keydet89/RegRipper3.0) is a utility that takes a registry hive as input and outputs a report that extracts data from some of the forensically important keys and values in that hive. The output report is in a text file and shows all the results in sequential order. 

RegRipper is available in both a CLI and GUI form which is shown in the screenshot below.

![](https://i.imgur.com/4QqgAnY.png)

One shortcoming of RegRipper is that it does not take the transaction logs into account. We must use Registry Editor to merge transaction logs with the respective registry hives before sending output to RegRipper for a more accurate result. 

Even though we have discussed these different tools, for the purpose of this room, we will only be using Registry Explorer and some of Eric Zimmermain's tools. The other tools mentioned here will be covered in separate rooms.

# System Information and System Accounts

Now that we have learned how to read registry data, let's find out where to look in the registry to perform our forensic analysis.

When we start performing forensic analysis, the first step is to find out about the system information. This task will cover gathering information related to a machine's System and Account Information.

## OS Version:

If we only have triage data to perform forensics, we can determine the OS version from which this data was pulled through the registry. To find the OS version, we can use the following registry key:

`SOFTWARE\Microsoft\Windows NT\CurrentVersion`

This is how Registry Explorer shows this registry key. Take a look and answer Question #1.

![](https://i.imgur.com/4rB8qGs.png)

## Current Control Set:

The hives containing the machine's configuration data used for controlling system startup are called Control Sets. Commonly, we will see two Control Sets, ControlSet001 and ControlSet002, in the **SYSTEM** hive on a machine.

In most cases (but not always), ControlSet001 will point to the Control Set that the machine booted with, and ControlSet002 will be the `last known good` configuration. Their locations will be:

`SYSTEM\ControlSet001`
`SYSTEM\ControlSet002`

Windows creates a volatile Control Set when the machine is live, called the Current Control Set (`HKLM\SYSTEM\CurrentControlSet`). For getting the most accurate system information, this is the hive that we will refer to. We can find out which Control Set is being used as the CurrentControlSet by looking at the following registry value:

`SYSTEM\Select\Current`

Similarly, the `last known good` configuration can be found using the following registry value:

`SYSTEM\Select\LastKnownGood`

This is how it looks like in Registry Explorer. Take a look and answer Question #2.

![](https://i.imgur.com/jQy26Gl.png)

> It is **vital** to establish this information before moving forward with the analysis. As we will see, many forensic artifacts we collect will be collected from the Control Sets.

## Computer Name:

It is crucial to establish the **Computer Name** while performing forensic analysis to ensure that we are working on the machine we are supposed to work on. We can find the Computer Name from the following location:

`SYSTEM\CurrentControlSet\Control\ComputerName\ComputerName`

Registry Explorer shows it like this. Take a look and answer question #3.

![](https://i.imgur.com/wJnrPtT.png)

## Time Zone Information:

For accuracy, it is important to establish what timezone the computer is located in. This will help us understand the chronology of the events as they happened. For finding the Time Zone Information, we can look at the following location:

`SYSTEM\CurrentControlSet\Control\TimeZoneInformation`

Here's how it looks in Registry Explorer. Take a look and answer Question #4.

![](https://i.imgur.com/Epa03Ms.png)

Time Zone information is important because *some data in the computer will have their timestamps in UTC/GMT* and others in the local time zone. Knowledge of the local time zone helps in establishing a timeline when merging data from all the sources. 

## Network Interfaces and Past Networks:

The following registry key will give a list of network interfaces on the machine we are investigating:

`SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces`

Take a look at this registry as shown in Registry Explorer and answer Question #5.

![](https://i.imgur.com/2rTuQ8z.png)

> Each interface is represented with a unique identifier (GUID) subkey, which contains values relating to the interface's TCP/IP configuration. This key will provide us with the information like IP addresses, DHCP IP address and Subnet Mask, DNS Servers, and more. This information is significant because it helps you make sure that you are performing forensics on the machine that you are supposed to perform it on.

The past networks a given machine was connected to can be found in the following locations:

`SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Signatures\Unmanaged`

`SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Signatures\Managed`

![](https://i.imgur.com/BYDtd8f.png)

> These registry keys contain past networks as well as the last time they were connected. The last write time of the registry key points to the last time these networks were connected.

## Autostart Programs (Autoruns):

The following registry keys include information about programs or commands that run when a user logs on. 

```
`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Run`

`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\RunOnce`

`SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce`

`SOFTWARE\Microsoft\Windows\CurrentVersion\policies\Explorer\Run`

`SOFTWARE\Microsoft\Windows\CurrentVersion\Run`
```

![](https://i.imgur.com/strRNa4.png)

The following registry key contains information about services:

`SYSTEM\CurrentControlSet\Services`

Notice the Value of the Start key in the screenshot below.

![](https://i.imgur.com/Wgk5EnO.png)

> In this registry key, if the `start` key is set to 0x02, this means that this service will *start at boot*.

## SAM Hive and User Information:

The SAM hive contains user account information, login information, and group information. This information is mainly located in the following location:

`SAM\Domains\Account\Users`

Take a look at the below screenshot and answer Question #6

![](https://i.imgur.com/IigIkoQ.png)

> The information contained here includes the relative identifier (RID) of the user, number of times the user logged in, last login time, last failed login, last password change, password expiry, password policy and password hint, and any groups the user is apart of.

# Usage or Knowledge of Files/Folders

## Recent Files

Windows maintains a list of recently opened files for each user. As we might have seen when using Windows Explorer, it shows us a list of recently used files. This information is stored in the NTUSER hive and can be found in the following location: 

```
NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs
```

![](https://i.imgur.com/ezouTbf.png)

Registry Explorer allows us to sort data contained in registry keys quickly. For example, the Recent documents tab arranges the Most Recently Used (MRU) file at the top of the list and the older ones later.

Another interesting piece of information in this registry key is that there are different keys with file extensions, such as `.pdf`, `.jpg`, `.docx` etc. These keys provide us with information about the last used files of a specific file extension. So if we are looking specifically for the last used PDF files, we can look at the following registry key:

```
NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs\.pdf
```

Registry Explorer also list the Last Opened time of the files.

## Office Recent Files:

Similar to the Recent Docs maintained by Windows Explorer, Microsoft Office also maintains a list of recently opened documents. This list is also located in the NTUSER hive. It can be found in the following location:

```
NTUSER.DAT\Software\Microsoft\Office\VERSION
```

The version number for each Microsoft Office release is different. An example registry key would look like this:

```
NTUSER.DAT\Software\Microsoft\Office\15.0\Word
```

In such a scenario, the recent files can be found at the following location. This location also saves the complete path of the most recently used files.

## Shellbags:

When any user opens a folder, it opens in a specific layout. Users can change this layout according to their preferences. These layouts can be different for different folders. This information about the Windows '*shell*' is stored and can identify the Most Recently Used files and folders. Since this setting is different for each user, it is located in the user hives. We can find this information on the following locations:

```
`USRCLASS.DAT\Local Settings\Software\Microsoft\Windows\Shell\Bags`

`USRCLASS.DAT\Local Settings\Software\Microsoft\Windows\Shell\BagMRU`

`NTUSER.DAT\Software\Microsoft\Windows\Shell\BagMRU`

`NTUSER.DAT\Software\Microsoft\Windows\Shell\Bags`
```

Registry Explorer doesn't give us much information about Shellbags. However, another tool from Eric Zimmerman's tools called the **ShellBag Explorer** shows us the information in an easy-to-use format. We just have to point to the hive file we have extracted, and it parses the data and shows us the results. An example is shown below. Take a look and answer Question #2.

![](https://i.imgur.com/YiZTLc0.png)

## Open/Save and LastVisited Dialog MRUs:

When we open or save a file, a dialog box appears asking us where to save or open that file from. It might be noticed that once we open/save a file at a specific location, Windows remembers that location. This implies that we can find out recently used files if we get our hands on this information. We can do so by examining the following registry keys:

```
NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSavePIDlMRU

NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\LastVisitedPidlMRU
```

This is how Registry Explorer shows this registry key. Take a look and answer questions #3 and #4.

![](https://i.imgur.com/tMlrdAI.png)

## Windows Explorer Address/Search Bars:

Another way to identify a user's recent activity is by looking at the paths typed in the Windows Explorer address bar or searches performed using the following registry keys, respectively. 

```
NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\TypedPaths

NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\WordWheelQuery
```

> Here is how the TypedPaths key looks like in Registry Explorer:

![](https://i.imgur.com/9XLPCYo.png)

# Evidence of Execution

## UserAssist:

Windows keeps track of applications launched by the user using Windows Explorer for statistical purposes int he User Assist registry keys. These keys contain information about the programs launched, the time of their launch, and the number of times they were executed. However, programs that were run using the command line *can't be found in the User Assist keys*. The User Assist key is present in the NTUSER hive, mapped to each user's GUID. We can find it at the following location:

`NTUSER.DAT\Software\Microsoft\Windows\Currentversion\Explorer\UserAssist\{GUID}\Count`

Take a look at the below screenshot from Registry Explorer and Answer Question #1:

![](https://i.imgur.com/Re8N8PT.png)

## ShimCache

ShimCache is a mechanism used to keep track of application compatibility with the OS and tracks all applications launched on the machine. Its main purpose is to ensure *backwards compatibility* of applications. It is also called **Application Compatibility Cache** (AppCompatCache). It is located in the following location in the SYSTEM hive:

`SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache`

ShimCache stores file name, file size, and last modified time of the executables.

Our goto tool, the Registry Explorer, doesn't parse ShimCache data in a human-readable format, so we go to another tool called AppCompatCache Parser, also a part of Eric Zimmerman's tools. It takes the SYSTEM hive as input, parses the data, and outputs a CSV file that looks like this:

![](https://i.imgur.com/6VaMSZB.png)

> We can use the following command to run the AppCompatCache Parser utiility:

`AppCompatCacheParser.exe --csv <path to save output> -f <path to SYSTEM give for data parsing> -c <control set to parse>`

The output can be viewed using EZviewer, another one of Eric Zimmerman's tools.

## AmCache

The AmCache hive is an artifact related to ShimCache. This performs a similar funciton to ShimCache, and stores additional data related to program executions. This data includes execution path, installation, execution and deletion times, and SHA1 hashes of the executed programs. This hive is located in the file system at:

`C:\Windows\appcompat\Programs\Amcache.hve`

Information about the last executed programs can be found at the following location in the hive:

`Amcache.hve\Root\File\{Volume GUID}\`

This is how Registry Explorer parses the AmCache hive:

![](https://i.imgur.com/Fmy8Wgw.png)

## BAM/DAM

**Background Activity Monitor** or BAM keeps a tab on the activity of background applications. Similar Desktop Activity Moderator or DAM is a part of Microsoft Windows that optimizes the power consumption of the device.

In the Windows registry, the following locations contain information related to BAM and DAM. This location contains information about last run programs, their full paths, and last execution time.

`SYSTEM\CurrentControlSet\Services\bam\UserSettings\{SID}`

`SYSTEM\CurrentControlSet\Services\dam\UserSettings\{SID}`

Below you can see how Registry Explorer parses data from BAM:

![](https://i.imgur.com/y1exryA.png)

# External Devices/USB Device Forensics

When performing forensics on a machine, often the need arises to identify if any USB or removable drives were attached to the machine. If so, any information related to those devices is important for a forensic investigator. In this task, we will go through the different ways to find information on connected devices and the drives on a system using the registry. 

## Device Identification

The following locations keep track of USB keys plugged into a system. These locations store the vendor id, product id, and version of the USB device plugged in and can be used to identify unique devices. These locations also stores the time the devices were plugged into the system.

`SYSTEM\CurrentControlSet\Enum\USBSTOR`

`SYSTEM\CurrentControlSet\Enum\USB`

Registry Explorer shows this information in a nice and easy-to-understand way. Take a look at this and answer question 1 and 2.

![](https://i.imgur.com/BrpFKzY.png)

## First/Last Times

Similarly, the following registry key tracks the first time the device was connected, the last time it was connected an the last time the device was removed from the system.

`SYSTEM\CurrentControlSet\Enum\USBSTOR\Ven_Prod_Version\USBSerial#\Properties\{83da6326-97a6-4088-9453-a19231573b29}\####`

In this key, the #### sign can be replaced by the following digits to get the required information:

| Value | Information           |
| ----- | --------------------- |
| 0064  | First Connection time |
| 0066  | Last connection time  |
| 0067  | Last removal time     |
> Although we can check this value manually, as we have seen above, Registry Explorer already parses this data and shows us if we select the USBSTOR key.

## USB Device Volume Name:

The device name of the connected drive can be found at the following location:

`SOFTWARE\Microsoft\Windows Portable Devices\Devices`

![](https://i.imgur.com/rOTDGZ4.png)

We can compare the GUID we see here in this registry key and compare it with the Disk ID we see on keys mentioned in device identification to correlate the names with unique devices. Take a look at these two screenshots and answer question #3.

Combining all of this information, we can create a fair picture of any USB devices that were connected to the machine we're investigating.

