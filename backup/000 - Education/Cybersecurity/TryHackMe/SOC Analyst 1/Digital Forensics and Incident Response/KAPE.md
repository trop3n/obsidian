#soclevel1 #tryhackme #cybersecurity #DFIR 

In the [Windows Forensics 1](https://tryhackme.com/room/windowsforensics1) and [Windows Forensics 2](https://tryhackme.com/room/windowsforensics2) rooms, we learned about the different artifacts which store information about a user's activity on a system. We also learned where those artifacts are located and how they can be accessed and interpreted. However, we did all that manually. In many cases, a forensic investigator doesn't have the luxury to perform manual analysis, which can be time-consuming. In such scenarios, it is helpful to have some tools help in automating the evidence collection, sanitization, and processing part.

## **Learning Objectives:**

In this room, we will:

- Learn about KAPE
- How KAPE works
- The different targets and modules used by KAPE
- Collection and analysis of forensic data using KAPE
# Introduction to KAPE

Kroll Artifact Parser and Extractor (KAPE) parses and extracts Windows forensics artifacts. It is a tool that can significantly reduce the time needed to respond to an incident by providing forensic artifacts from a live system or a storage device much earlier than the imaging process completes.

KAPE serves two primary purposes, 1) collect files and 2) process the collected files as per the provided options. For achieving these purposes, KAPE uses the concept of targets and modules. Targets can be defined as the forensic artifacts that need to be collected. Modules are programs that process the collected artifacts and extract information from them. We will learn about them in the upcoming tasks. 
## How it Works

KAPE is extensible and highly configurable. In essence, the KAPE binary collects files and processes them as per the provided configuration. 

The collection of files (targets) KAPE adds the files to a queue and copies them into two passes. In the first pass, it copies the files that it can. This works for files that the OS has not locked. The rest of the files are passed to a secondary queue. The secondary queue is processed using a different technique that uses raw disk reads to bypass the OS locks and copy the files. The copied files are saved with original timestamps and metadata and stored in a similar directory structure.

Once the data is collected, KAPE can process it using modules. The modules can be independent binaries that run on the collected data and process them to extract information. For example, KAPE will collect and copy the Prefetch file to our target destination during the target collection. Running a Prefetch Parser (PECmd) module on this target will extract the prefetch file and save it in a CSV file. 

![](https://i.imgur.com/PxdAZ9r.png)

As the above image shows, KAPE can extract targets from a live system, a mounted image, or the [F-response](https://www.f-response.com/) utility. KAPE does not need to be installed. It is portable and can be used from network locations or USB drives. To proceed further, click the Start Machine button on the top-right corner to start the attached VM in split-screen mode. Alternatively, you can log in to the machine using the following credentials:

**Username**: thm-4n6
**Password**: 123

In the attached VM, you will find KAPE on the Desktop in the folder titled KAPE.In this folder, you will find the following files and directories:

You can see two binaries in this directory, kape.exe and gkape.exe. The first is the CLI version of KAPE, and the second is a GUI version (symbolized by the 'g' prefix). 

gkape.settings stores the default settings of the GUI version. 

Get-KAPEupdate.ps1, as the name suggests, is a Powershell script that checks and download updates. 

ChangeLog.txt and Documentation are self-explanatory. We will explore Targets and Modules in the following tasks. 
# Target Options

In KAPE's lexicon, `Targets` are the artifacts that need to be collected from a system or image and copied to our provided destination. For example, as we learned in the last room, Windows Prefetch is a forensic artifact for evidence of execution so that we can create a `Target` for it. Similarly, we can also create `Targets` for the registry hives. In short, `Targets` copy files from one place to another. 

> When we open the `Targets` directory, this is what we see:

![](https://i.imgur.com/xOxEuu3.png)

The last four files at the bottom are guides and templates to create `Targets` and `Compound Targets` of our own. We will discuss `Compound Targets` later in this task. As you can see, the targets are grouped into different directories. Let's check out the `Windows` directory to see what we have:  

![](https://i.imgur.com/3lekynm.png)

We can see different .tkape extension files. This is how a `Target` is defined for KAPE. A TKAPE file contains information about the artifact that we want to collect, such as the path, category, and file masks to collect. As an example, below is how the Prefetch `Target` is defined. 

![](https://i.imgur.com/AFGXNCp.png)

This TKAPE file tells KAPE to collect files with the file mask `*.pf` from the path `C:\Windows\Prefetch` and `C:\Windows.old\prefetch`.

Notice that we have the `C:\Windows.old` path listed here as well. This path contains files retained after Windows has updated to a new version. For forensic analysis, we can also find interesting historical artifacts from this directory.
## Compound Targets

KAPE also supports `Compound Targets`. These are `Targets` that are compounds of multiple other targets. As mentioned in the previous tasks, KAPE is often used for quick triage collection and analysis. The purpose of KAPE will not be fulfilled if we have to collect each artifact individually. Therefore, `Compound Targets` help us collect multiple targets by giving a single command. 

Examples of `Compound Targets` include `!BasicCollection`, `!SANS_triage` and `KAPEtriage`. We can view the `Compound Targets` on the path `KAPE\Targets\Compound`. The following image shows what a `Compound Target` for evidence of execution looks like:

![](https://i.imgur.com/ZZKLHkq.png)

> The above `Compound Target` will collect evidence from Prefetch, RecentFileCache, AmCache, and Syscache `Targets`. 
## !Disabled

This directory contains `Targets` that you want to keep in the KAPE instance, but you don't want them to appear in the active Targets list.
## !Local

If you have created some `Targets` that you don't want to sync with the KAPE Github repository, you can place them in this directory. These can be `Targets` that are specific to your environment. Similarly, anything not present in the Github repository when we update KAPE will be moved to the `!Local` directory.
# Module Options

`Modules`, in KAPE's lexicon, run specific tools against the provided set of files. Their goal is not to copy files from one place to another but rather run some command and store the output. Generally, the output is in the form of CSV or TXT files. 

This is what the `Modules` directory looks like in KAPE:

![](https://i.imgur.com/w16X5Zt.png)

Similar to the previous task, we see guides and templates for creating `Modules` and `Compound Modules`. We also see the `!Disabled`, `!Local` and `Compound` directories, which are similar to what we saw in the previous task. We will not discuss these again, as we discussed them in the last task. We see that most of the `Modules` are grouped together in different directories. One thing we find different is the `bin` directory. We will discuss that in a bit. For now, let's open the Windows directory and see what we have there:

![](https://i.imgur.com/Oasv9Vh.png)

> Here we see files with the `.mkape` extension. These are understood as `Modules` by KAPE. Let's open an MKAPE file and see how it is structured. The following image shows the Windows_IPConfig MKAPE file. 
> 
![](https://i.imgur.com/fvFdpWb.png)

Notice that MKAPE file tells KAPE about the executable that has to be run, the command line parameters of the executable file, the output export format, and the filename to export to. But what if the executable that we want to run is not present on the system. This brings us to the `bin` directory.
## The `bin` Directory

The `bin` directory contains executables that we want to run on the system but are not natively present on most systems. KAPE will run executables either from the `bin` directory or the complete file path. An example of files to be kept in the `bin` directory are Eric Zimmerman's tools, which are generally not present on a Windows system. We used them extensively in the Windows Forensics rooms.

![](https://i.imgur.com/jeRUVin.png)

Notice that most of the binaries present here are from Eric Zimmerman's Tools.
# KAPE GUI

Now that we have learned about how the different components of KAPE work let's take it for a test drive. 

![](https://i.imgur.com/mnn6mDn.png)

> Here you can see that there are different options, but most are disabled. To collect `Targets` we will go ahead by enabling the `Use Target Options` checkbox. This will enable the options present in the left half of the Window:

![](https://i.imgur.com/o468N7A.png)

If we want to perform forensics on the same machine on which KAPE is running, we will provide `C:\` for the target source. We can select the target destination of our choice. All the triage files will be copied to the Target destination that we provide.

![](https://i.imgur.com/W88mIAM.png)

> Here, the `Flush` checkbox will delete all the contents of the Target destination, so we *have to be careful when using that*. We have disabled the `Flush` checkbox so that it does not delete data already present in the directories. `Add %d` will append date info to the directory name where the collected data is saved. Similarly, `Add %m` will append machine info to the Target destination directory. We can select our desired Target from the list shown above. The Search bar helps us search for the names of the desired Targets quickly.

![](https://i.imgur.com/Kp5EWm4.png)

We can select if we want to process Volume Shadow Copies by enabling `Process VSCs`. We can select the `transfer` checkbox if we want to transfer the collected artifacts through an SFTP server or an S3 bucket. For transfer, the files must be enclosed in a container, which can be Zip, VHD, or VHDX. Similarly, we can provide exclusions based on SHA-1, and KAPE will not copy the excluded files. When enclosing in a container, we will need to give a `Base Name` that will be used for all the created files. It is not required if we are not transferring files or enclosing them in a container.

![](https://i.imgur.com/h5WnHeZ.png)

In the `current command line` tab, we see the command line options being added or removed while configuring the UI. This Window will show more options in the command line as we add options. Please note that the destination path in your case will be different from the one shown in the image. Notice the `--tflush` flag here. It means that when this command line was created, the `Flush` checkbox was still checked.

![](https://i.imgur.com/qrDXNns.png)

> By clicking the **Use Module Options** checkbox, the right side of the KAPE Window will also be enabled. 

![](https://i.imgur.com/skrL9qr.png)

The rest of the options for modules are similar to the ones for targets, so we won't go into details for them. Below you will see what the configuration looks like when we have KAPE all set up for collecting targets and processing them using Modules.

![](https://i.imgur.com/FBRHVH1.png)

We have selected the `KapeTriage` compound target and `!EZParser` Compound Module. The command line below shows the CLI command that will be run. The `Execute!` button is the bottom right corner will execute the command. The `Disable flush warnings` checkbox underneath it will not warn use when we are using the `Flush` flags. When we press `Execute!` We will see a command line window open and show us the logs as KAPE performs its tasks. It will take a few minutes to execute since it will be collecting all the data and then running the module processes on it. Once it completes, it will show us the total execution time, and we can press any key to terminate the command window.

```shell-session
KAPE version 1.1.0.1 Author: Eric Zimmerman (kape@kroll.com)

KAPE directory: D:\KAPE
Command line: --tsource C: --tdest C:\Users\Umair\Desktop\kape --target KapeTriage --mdest C:\Users\Umair\Desktop\4n6-2 --module !EZParser --gui

System info: Machine name: UMAIR-THINKBOOK, 64-bit: True, User: Umair OS: Windows10 (10.0.22000)

Using Target operations
Found 14 targets. Expanding targets to file list...
Target 'ApplicationEvents' with Id '2da16dbf-ea47-448e-a00f-fc442c3109ba' already processed. Skipping!
Target 'ApplicationEvents' with Id '2da16dbf-ea47-448e-a00f-fc442c3109ba' already processed. Skipping!
Target 'ApplicationEvents' with Id '2da16dbf-ea47-448e-a00f-fc442c3109ba' already processed. Skipping!
Target 'ApplicationEvents' with Id '2da16dbf-ea47-448e-a00f-fc442c3109ba' already processed. Skipping!
Target 'ApplicationEvents' with Id '2da16dbf-ea47-448e-a00f-fc442c3109ba' already processed. Skipping!
Found 3,059 files in 4.257 seconds. Beginning copy...
        Deferring 'C:\Windows\System32\winevt\logs\Application.evtx' due to IOException...
        Deferring 'C:\Windows\System32\winevt\Logs\Microsoft-Windows-Windows Defender%4Operational.evtx' due to IOException...
        Deferring 'C:\Windows\System32\winevt\Logs\Microsoft-Windows-Windows Defender%4WHC.evtx' due to IOException...
        Deferring 'C:\ProgramData\Microsoft\Windows Defender\Support\MPDetection-20220126-183133.log' due to IOException...
        Deferring 'C:\ProgramData\Microsoft\Windows Defender\Support\MPDeviceControl-20211016-164735.log' due to IOException...
        Deferring 'C:\ProgramData\Microsoft\Windows Defender\Support\MPLog-10172021-040927.log' due to IOException...
        Deferring 'C:\ProgramData\Microsoft\Windows Defender\Support\MpWppTracing-20220210-070038-00000003-ffffffff.bin' due to IOException...
        Deferring 'C:\Windows\System32\winevt\logs\HardwareEvents.evtx' due to IOException...
        Deferring 'C:\Windows\System32\winevt\logs\IntelAudioServiceLog.evtx' due to IOException...
        Deferring 'C:\Windows\System32\winevt\logs\Internet Explorer.evtx' due to IOException...
.
.
.
.
Executing remaining modules...
        Running 'EvtxECmd\EvtxECmd.exe': -d C:\Users\Umair\Desktop\kape --csv C:\Users\Umair\Desktop\4n6-2\EventLogs
        Running 'JLECmd.exe': -d C:\Users\Umair\Desktop\kape --csv C:\Users\Umair\Desktop\4n6-2\FileFolderAccess -q
        Running 'LECmd.exe': -d C:\Users\Umair\Desktop\kape --csv C:\Users\Umair\Desktop\4n6-2\FileFolderAccess -q
        Running 'PECmd.exe': -d C:\Users\Umair\Desktop\kape --csv C:\Users\Umair\Desktop\4n6-2\ProgramExecution -q
        Running 'RBCmd.exe': -d C:\Users\Umair\Desktop\kape --csv C:\Users\Umair\Desktop\4n6-2\FileDeletion -q
        Running 'RECmd\RECmd.exe': -d C:\Users\Umair\Desktop\kape --bn BatchExamples\Kroll_Batch.reb --nl false --csv C:\Users\Umair\Desktop\4n6-2\Registry -q
        Running 'SBECmd.exe': -d C:\Users\Umair\Desktop\kape --csv C:\Users\Umair\Desktop\4n6-2\FileFolderAccess -q
        Running 'SQLECmd\SQLECmd.exe': -d C:\Users\Umair\Desktop\kape --csv C:\Users\Umair\Desktop\4n6-2\SQLDatabases
        Running 'SrumECmd.exe': -d C:\Users\Umair\Desktop\kape -k --csv C:\Users\Umair\Desktop\4n6-2\SystemActivity
        Running 'SumECmd.exe': -d C:\Users\Umair\Desktop\kape\Windows\System32\LogFiles\SUM --csv C:\Users\Umair\Desktop\4n6-2\SUMDatabase
Executed 18 processors in 192.2738 seconds

Total execution time: 258.1812 seconds


Press any key to exit
```

Notice that at the backend, KAPE is running the `kape.exe` in a command line. We can check out the files created by KAPE once it completes processing them. The below snapshot shows our `Module destination`. Notice how KAPE has processed the files according to different categories.

![](https://i.imgur.com/xio5FPx.png)

Let's collect triage data using the `KAPETriage` package, process it using `!EZParser` module, and answer the questions below. Then we can proceed to learn about the KAPE CLI in the next task.
# KAPE CLI

Though we used the GUI in the previous task, KAPE is a command-line tool. Therefore, it is pertinent to know how to use KAPE through the command line to make full use of it.

For a list of all the different switches that can be used with KAPE, open an elevated PowerShell (Run As Administrator), go to the path where the KAPE binary is located, and try `KAPE.exe`. you will see something like this as an output.

```shell-session
D:\KAPE>kape.exe

KAPE version 1.1.0.1 Author: Eric Zimmerman (kape@kroll.com)

        tsource         Target source drive to copy files from (C, D:, or F:\ for example)
        target          Target configuration to use
        tdest           Destination directory to copy files to. If --vhdx, --vhd or --zip is set, files will end up in VHD(X) container or zip file
        tlist           List available Targets. Use . for Targets directory or name of subdirectory under Targets.
        tdetail         Dump Target file details
        tflush          Delete all files in 'tdest' prior to collection
        tvars           Provide a list of key:value pairs to be used for variable replacement in Targets. Ex: --tvars user:eric would allow for using %user% in a Target which is replaced with eric at runtime. Multiple pairs should be separated by ^
        tdd             Deduplicate files from --tsource (and VSCs, if enabled) based on SHA-1. First file found wins. Default is TRUE

        msource         Directory containing files to process. If using Targets and this is left blank, it will be set to --tdest automatically
        module          Module configuration to use
        mdest           Destination directory to save output to
        mlist           List available Modules. Use . for Modules directory or name of subdirectory under Modules.
        mdetail         Dump Module processors details
        mflush          Delete all files in 'mdest' prior to running Modules
        mvars           Provide a list of key:value pairs to be used for variable replacement in Modules. Ex: --mvars foo:bar would allow for using %foo% in a module which is replaced with bar at runtime. Multiple pairs should be separated by ^
        mef             Export format (csv, html, json, etc.). Overrides what is in Module config

        sim             Do not actually copy files to --tdest. Default is FALSE
        vss             Process all Volume Shadow Copies that exist on --tsource. Default is FALSE

        vhdx            The base name of the VHDX file to create from --tdest. This should be an identifier, NOT a filename. Use this or --vhd or --zip
        vhd             The base name of the VHD file to create from --tdest. This should be an identifier, NOT a filename. Use this or --vhdx or --zip
        zip             The base name of the ZIP file to create from --tdest. This should be an identifier, NOT a filename. Use this or --vhdx or --vhd

        scs             SFTP server host/IP for transferring *compressed VHD(X)* container
        scp             SFTP server port. Default is 22
        scu             SFTP server username. Required when using --scs
        scpw            SFTP server password
        scd             SFTP default directory to upload to. Will be created if it does not exist
        scc             Comment to include with transfer. Useful to include where a transfer came from. Defaults to the name of the machine where KAPE is running

        s3p             S3 provider name. Example: spAmazonS3 or spGoogleStorage. See 'https://bit.ly/34s9nS6' for list of providers. Default is 'spAmazonS3'
        s3r             S3 region name. Example: us-west-1 or ap-southeast-2. See 'https://bit.ly/3aNxXhc' for list of regions by provider
        s3b             S3 bucket name
        s3k             S3 Access key
        s3s             S3 Access secret
        s3st            S3 Session token
        s3kp            S3 Key prefix. When set, this value is used as the beginning of the key. Example: 'US1012/KapeData'
        s3o             When using 'spOracle' provider, , set this to the 'Object Storage Namespace' to use
        s3c             Comment to include with transfer. Useful to include where a transfer came from. Defaults to the name of the machine where KAPE is running

        s3url           S3 Presigned URL. Must be a PUT request vs. a GET request

        asu             Azure Storage SAS Uri
        asc             Comment to include with transfer. Useful to include where a transfer came from. Defaults to the name of the machine where KAPE is running

        zv              If true, the VHD(X) container will be zipped after creation. Default is TRUE
        zm              If true, directories in --mdest will be zipped. Default is FALSE
        zpw             If set, use this password when creating zip files (--zv | --zm | --zip)

        hex             Path to file containing SHA-1 hashes to exclude. Only files with hashes not found will be copied

        debug           Show debug information during processing
        trace           Show trace information during processing

        gui             If true, KAPE will not close the window it executes in when run from gkape. Default is FALSE

        ul              When using _kape.cli, when true, KAPE will execute entries in _kape.cli one at a time vs. in parallel. Default is FALSE

        cu              When using _kape.cli, if true, KAPE will delete _kape.cli and both Target/Module directories upon exiting. Default is FALSE

        sftpc           Path to config file defining SFTP server parameters, including port, users, etc. See documentation for examples
        sftpu           When true, show passwords in KAPE switches for connection when using --sftpc. Default is TRUE

        rlc             If true, local copy of transferred files will NOT be deleted after upload. Default is FALSE
        guids           KAPE will generate 10 GUIDs and exit. Useful when creating new Targets/Modules. Default is FALSE
        sync            If true, KAPE will download the latest Targets and Modules from specified URL prior to running. Default is https://github.com/EricZimmerman/KapeFiles/archive/master.zip

        ifw             If false, KAPE will warn if a process related to FTK is found, then exit. Set to true to ignore this warning and attempt to proceed. Default is FALSE


        Variables: %d = Timestamp (yyyyMMddTHHmmss)
                   %s = System drive letter
                   %m = Machine name

Examples: kape.exe --tsource L: --target RegistryHives --tdest "c:\temp\RegistryOnly"
          kape.exe --tsource H --target EvidenceOfExecution --tdest "c:\temp\default" --debug
          kape.exe --tsource \\server\directory\subdir --target Windows --tdest "c:\temp\default_%d" --vhdx LocalHost
          kape.exe --msource "c:\temp\default" --module LECmd --mdest "c:\temp\modulesOut" --trace --debug

          Short options (single letter) are prefixed with a single dash. Long commands are prefixed with two dashes

          Full documentation: https://ericzimmerman.github.io/KapeDocs/


D:\KAPE>
```

We can see from the above screenshot that while collecting targets, the switches `tsource`, `target` and `tdest` are required. Similarly, when processing files using Modules, `module` and `mdest` are required switches. The other switches are optional as per the requirements of the collection.

With this information, let's build a command to perform the same task we performed in the previous task i.e. collect triage data using the `KapeTriage` Compound Target and process it using the `!EZParser` Compound Module. Since we are not using the GUI version, we will start with typing:

`kape.exe`

To add a Target source, let's append `--tsource` and that Target path:

`kape.exe --tsource C:`

The `--target` flag will be used for selecting the Target the `--tdest` flag for the Target destination. For the sake of simpicity, we will set the Target destination to a directory named target on the Desktop. KAPE will create a new directory if it doesn't already exist. Our command line will now look like this:

`kape.exe --tsource C: --target KapeTriage --tdest C:\Users\thm-4n6\Desktop\Target`

Running the above command will collect triage data defined in the KapeTriage Target and save it to the provided destination. However, it will not process it or perform any other activity on the data.

If we want to flush the Target destination, we can add `--tflush` to do that. For now, let's move on to adding the Module options. If we were using a Module source, we would have used a >`--msource` flag in a similar manner to the `--tsource` flag. But in this case, let's use the Target destination as the Module source. By doing this, we will not need to add it explicitly, and we can move on to adding the Module destination using the `--mdest` flag:

`kape.exe --tsource C: --target KapeTriage --tdest C:\Users\thm-4n6\Desktop\Target --mdest C:\Users\thm-4n6\Desktop\module`

We have just used a directory named module for the Module destination.

To process the Target destination using a Module, we need to provide the Module name using the `--module` flag. To process it using the `!EZParser` Module, we will append `--module !EZParser`, making our command look like this:

`kape.exe --tsource C: --target KapeTriage --tdest C:\Users\thm-4n6\Desktop\Target --mdest C:\Users\thm-4n6\Desktop\module -- !EZParser`

Please note that we will need to run this command in an elevated shell (with Administrator privileges) for KAPE to collect the data.

We can modify the command as per our needs and the switches provided by KAPE. When we run this command, we will see a similar window as in the previous task. You can check out he files collected by KAPE Targets and Modules once it completes.
## Batch Mode:

KAPE can also be run in batch mode. What this means is that we can provide a list of commands for KAPE to run in a file named `_kape.cli`. Then we keep this file in the directory containing the KAPE binary. When `kape.exe` is executed as an administrator, it checks if there is `_kape.cli` file present in the directory. If so, it executes the commands mentioned in the cli file. This mode can be used if you need someone to run KAPE for you, you will keep all the commands in a single line, and all you need is for the person to right-click and run kape.exe as administrator. For example, if we have to perform the same task as we did earlier in this task using batch mode, we will have to create a kape.cli file with the following content:

`--tsource C: --target KapeTriage --tdest C:\Users\thm-4n6\Desktop\Target --mdest C:\Users\thm-4n6\Desktop\module --module !EZParser`

When we run `kape.exe`, it will perform the same tasks as when we ran it through CLI above.

Let's answer the questions below and get ready to put our newly learned skills to use in the next task.

