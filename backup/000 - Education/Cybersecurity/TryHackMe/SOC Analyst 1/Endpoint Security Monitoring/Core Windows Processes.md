# Introduction

> In this room, we will explore the core processes within a Windows system. This room aims to help you know and understand what normal behavior within a Windows operating system is. 

This foundational knowledge will help us identify malicious processes running on an endpoint.

The Windows Operating System is the most used in the word, and the majority of it's users don't fully understand its inner workings. Users are simply content that it works, like anything complex, such as a car. 

It starts, and you can drive from Point A to Point B. Now regarding computers, if they can surf the web, read/answer emails, shop, listen to music and watch movies, all is well. 

It took a long time for users to grasp the need for antivirus programs fully. Only when one of their essential computer functions is disrupted is when antivirus matters. Antivirus was enough over 5-7 years ago (estimated).

Time changes everything. Malware and attacks have evolved, and antivirus is no longer enough. Antivirus has struggled to keep up, solely based on how it is designed to catch evil.

Today antivirus is just one solution within the layered defense approach. New security tools, such as **EDR** (Endpoint Detection and Response), have been created because antivirus cannot catch every malicious binary and process running on the endpoint. 

Even with these new tools, *attackers can still bypass the defenses running on the endpoint*. This is where we come in. Whether you're a Security Analyst, SOC Analyst, Detection Engineer, or Threat Hunter, if one of the tools alerts us of a suspicious binary or process, we must investigate and decide on a course of action.

Knowing the expected behavior of the systems we have to defend, a Windows system, we can infer if the binary or process is benign or evil.
# Task Manager

**Task Manager** is a built-in Windows utility that allows users to see what is running on the Windows system. It also provides information on resource usage, such as how much each process utilizes CPU and memory. When a program is not responding, Task Manager is used to kill the process.

Processes are categorized as follows: `Apps` and `Background Processes`. 

Another category that is not visible in the above image is `Windows Processes`. 

The columns are very minimal. The columns, **Name**, **Status**, **CPU** and **Memory** are the only ones visible. To view more columns, right-click on any column header to open more options. 

Overview of each column:

- **Type**: Each process falls into 1 of 3 categories (Apps, Background Processes, or Windows Processes)
- **Publisher**: Think of this column as the name of the author of the program or file.
- **PID**: This is known as the process identifier number. Windows assigns a unique process identifier each time a program starts. If the same program as multiple running processes, each will have its unique process identifier.
- **Process Name**: This is the file name of the process. In the above image, the file name for Task Manager is `Taskmrg.exe`.
- **Command Line**: THe full command used to launch the process
- **CPU**: the amount of CPU (processing power) the process uses. 
- **Memory**: The amount of physical working memory utilized by the process.

Task manager is a utility you should be comfortable using, whether you're troubleshooting or performing analysis on the endpoint. 

Let's move to the **Details** tab. This view provides some core processes that will be discussed in this room. Sort the PID column so that the PIDS are in ascending order.

Add some additional columns to see more information about these processes. Good columns to add are `Image Path Name` and `Command Line`

These two columns can quickly alert an analyst of any outliers with a given process. In the below image, PID 384 is paired with a process named svchost.exe, a Windows process, but if the image  path name of Command line is not what it's expected to be, then we can perform a deeper analysis of this process.

> of course, you can add as many columns as you wish, but adding the columns that would be pertinent to your current task is recommended.

Task manager is a powerful built-in Windows utility but lacks certain important information when analyzing processes, such as **parent process information**. 

- It is another key column when identifying outliers. Back to svchost.exe, if the parent process for PID 384 is not services.exe, this will warrant further analysis.


> Based on the above image, the PID for services.exe is 632. But wait, one of the svchost.exe processes has a PID of 384. How did svchost.exe start before services.exe? Well, it didn't.

- Task manager doesn't show a parent child process-view. That is where other utilities, such as **Process Hacker** and **Process Explorer** come to the rescue.
### Process Hacker

### Process Explorer

> Moving forward, we'll use **Process Hacker** and **Process Explorer** instead of Task Manager to obtain information about each Windows process. 

As always, it is encouraged that you inspect and familiarize yourself with all information available within Task Manager. It's a built-in utility that is available in every Windows system. You might find yourself in a situation where you can't bring your tools to the fight and rely on the tools native to the system.

Aside from Task Manager, it would be best if you also familiarize yourself with the comand-line equivalnet of obtaining information about the running processes on a Windows system: `tasklist`, `Get_Process` or `ps` (PowerShell), and `wmic`.
# System 

The first Windows process on the list is **System**. It was mentioned in a previous section that a PID for any given process is assigned at random, but that is not the case for the System process. The PID for System is always **4**. What does this process do exactly?

The official definition from Windows Internals 6th Edition:

"_The System process (process ID 4) is the home for a special kind of thread that runs only in kernel mode a kernel-mode system thread. System threads have all the attributes and contexts of regular user-mode threads (such as a hardware context, priority, and so on) but are different in that they run only in kernel-mode executing code loaded in system space, whether that is in Ntoskrnl.exe or in any other loaded device driver. In addition, system threads don't have a user process address space and hence must allocate any dynamic storage from operating system memory heaps, such as a paged or nonpaged pool._"

What is user-mode? What is Kernel-mode? Visit the following [link](https://docs.microsoft.com/en-us/windows-hardware/drivers/gettingstarted/user-mode-and-kernel-mode) to understand each of these.
# System > smss.exe

> The next process is **smss.exe (Session Manager Subsystem)**. This process, also known as the **Windows Session Manager**, is responsible for creating new sessions. It is the first user-mode process started by the kernel.

This process starts the kernel and user modes of the Windows subsystem (you can read more about NT architecture [here](https://en.wikipedia.org/wiki/Architecture_of_Windows_NT)). This subsystem includes win32k.sys (kernel mode), winsrv.dll (user mode) and csrss.exe(user mode)

Smss.exe starts csrss.exe (Windows subsystem) and wininit.exe in Session 0, *an isolated Windows session for the operating system* and csrss.exe and winlogon.exe for Session 1, *which is the user session*. 

- The first child instance creates child instances in new sessions, done by smss.exe copying itself into the new session and self-terminating. 
- You can read more about this process [here](https://en.wikipedia.org/wiki/Session_Manager_Subsystem).
### Session 0 (csrss.exe & wininit.exe)


> Any other subsystem listed in the `Required` value of `HKLM\System\CurrentControlSet\Control\Session Manager\Subsystems` is also launched.


> SMSS is also responsible for creating environment variables, virtual memory paging files and starts winlogon.exe (the Windows Logon Manager).
### What is Normal?

**Image Path**: %SystemRoot%\System32\smss.exe
**Parent Process**: System
**Number of Instances**: One master instance and child instance per session. The child instances exits after creating the session.
**User Account**: Local System
**Start Time**: Within seconds of boot time for the master instance
### What is Unusual?

- A different parent process other than System (4)
- The image path is different from `C:\Windows\System32`
- More than one running process (children self-terminate and exit after each session)
- The running User is not the SYSTEM user
- Unexpected registry entries for Subsystem
# csrss.exe

> As mentioned in the previous section, `csrss.exe` (**Client Server Runtime Process**) is the user-mode side of the Windows subsystem. This process is always running and is critical to system operation.

If this process is terminated by chance, *it will result in system failure.*

This process is responsible for the Win32 console window and process threat creation and deletion. For each instance, csrsrv.dll and winsrv.dll are loaded along with others.

This process is also responsible for making the Windows API available to other processes, mapping drive letters, and handling the Windows shut down process. You can read more about this process [here](https://en.wikipedia.org/wiki/Client/Server_Runtime_Subsystem). 

**Note**: Recall that csrss.exe and winlogon.exe are called from smss.exe at startup for Session 1.
### What is Normal?

Session 0 (PID 392)

Session 1 (PID 512)

> Notice what is shown for the parent process of these two processes. Remember, these processes are spawned by smss.exe, which self-terminates itself.

**Image Path**: %SystemRoot%\System32\csrss.exe
**Parent Process**: Created by an instance of smss.exe
**Number of Instances**: Two or more
**User Account**: Local System
**Start Time**: Within seconds of boot time for the first two instances, (for Session 0 and 1). Start times for additional instances occur as new sessions are created, although only Sessions 0 and 1 are often created. 
### What is Unusual?

- An actual parent process. (smss.exe call this process and self terminates.)
- Image file path other than `C:\Windows\System32`
- Subtle misspellings to hide rogue processes masquerading as csrss.exe in plain sight.
- The user in not the SYSTEM user
# Wininit.exe

> The **Windows Initialization Process, wininit.exe**, is responsible for launching services.exe (Service Control Manager), lsass,exe (Local Security Authority), and lsaiso.exe within Session 0.
> 
> 	It is another critical Windows process that runs in the background, along with it's child process.

**Note**: Isaiso.exe is a process associated with **Credential Guard and KeyGuard**. You will only see this process if Credential Guard is enabled.
### What is Normal?

**Image Path**: %SystemRoot%\System32\wininit.exe
**Parent Process**: Created by an instance of smss.exe
**Number of Instances**: One
**User Account**: Local System
**Start Time**: Within seconds of boot time
### What is Unusual?

- An actual parent process (smss.exe calls this process and self-terminates)
- Image file path other than C:\Windows\System32
- Subtle misspellings to hide rogue processes in plain sight.
- Multiple running instances
- Not running as SYSTEM
# wininit.exe > services.exe

> The next process is the **Service Control Manager (SCM)** or **services.exe**. Its primary responsibility is to handle system services: loading services, interacting with services and starting or ending services. It maintains a database that can be queried using a Windows built in utility, `sc.exe`.

```shell
C:\Users\Administrator> sc.exe
DESCRIPTION:
        SC is a command line program used for communicating with the
        Service Control Manager and services.
USAGE:
        sc <server> [command] [service name] <option1> <option2>...
```

> Information regarding services is stored in the registry, `HKLM\System\CurrentControlSet\Services`.

This process also loads device drivers marked as auto-start into memory. 

When a user logs into a machine successfully, this process is responsible for setting the value of the **Last Known Good** control set (Last Known Good Configuration) `HKLM\System\Select\LastKnownGood`, to that of the CurrentControlSet.

> This process is the parent to several other key processes: *svchost.exe, spoolsv.exe, msmpeng.exe, and dllhost.exe*, to name a few. 
> You can read more about this process [here](https://en.wikipedia.org/wiki/Service_Control_Manager).
### What is Normal?

**Image Path**: %SystemRoot%\System32\services.exe
**Parent Process**: wininit.exe
**Number of Instances**: Once
**User Account**: Local System
**Start Time**: Within seconds of boot time
### What is Unusual?

- A parent process other than wininit.exe
- Image file path other than C:\Windows\System32
- Subtle misspellings to hide rogue processes in plain sight
- Multiple running instances
- Not running as SYSTEM
# wininit.exe > services.exe > svchost.exe

> The **Service Host** (Host Process for Windows Services) or **svchost.exe** is responsible for hosting and managing Windows services.

The services running in this process are *Implemented as DLLs.* The DLL to implement is stored in the registry for the service under the `Parameters` subkey in `ServiceDLL`. The full path is `HKLM\SYSTEM\CurrentControlSet\Services\SERVICE NAME\Parameters`

The example below is the ServiceDLL value for the Dcomlaunch service.

> To view this information from within Process Hacker, right-click the svchost.exe process. In this case, it will be **PID 748**.

> Right click the service and select properties. Look at ServiceDLL.

> From the above screenshot, the Binary Path is listed.

Also, notice how it is structured. There is a key identifier in the binary path, and that identifier is `-k`. This is how a legitimate svchost.exe process is called. 

The `-k` parameter is for grouping similar services to share the same process. This concept was based on the OS design and implemented to reduce resource consumption. Starting from **Windows 10 Version 1703**, services grouped into host processes changed. On machines running more than 3.5GB of memory, each service will run its own process. You can read more about this process [here](https://en.wikipedia.org/wiki/Svchost.exe).

---

From **svchost.exe** on Wikipedia:

**Svchost.exe** (**Service Host**, or **SvcHost**) is a system [process](https://en.wikipedia.org/wiki/Process_(computing) "Process (computing)") that can host one or more [Windows services](https://en.wikipedia.org/wiki/Windows_service "Windows service") in the [Windows NT](https://en.wikipedia.org/wiki/Windows_NT "Windows NT") family of [operating systems](https://en.wikipedia.org/wiki/Operating_system).(https://en.wikipedia.org/wiki/Svchost.exe#cite_note-1) Svchost is essential in the implementation of _shared service processes_, where a number of services can share a process in order to reduce resource consumption. Grouping multiple services into a single process conserves computing resources, and this consideration was of particular concern to NT designers because creating Windows processes takes more time and consumes more memory than in other operating systems, e.g. in the [Unix](https://en.wikipedia.org/wiki/Unix "Unix") family.(https://en.wikipedia.org/wiki/Svchost.exe#cite_note-osterman-2) However, if one of the services causes an unhandled exception, the entire process may crash. In addition, identifying component services can be more difficult for end users. Problems with various hosted services, particularly with [Windows Update](https://en.wikipedia.org/wiki/Windows_Update "Windows Update"),(https://en.wikipedia.org/wiki/Svchost.exe#cite_note-3)(https://en.wikipedia.org/wiki/Svchost.exe#cite_note-4) get reported by users (and headlined by the press) as involving svchost.

The svchost process was introduced in [Windows 2000](https://en.wikipedia.org/wiki/Windows_2000 "Windows 2000"),(https://en.wikipedia.org/wiki/Svchost.exe#cite_note-5) although the underlying support for shared service processes has existed since [Windows NT 3.1](https://en.wikipedia.org/wiki/Windows_NT_3.1 "Windows NT 3.1").(https://en.wikipedia.org/wiki/Svchost.exe#cite_note-osterman-2)

---

> Back to the key identifier (`-k`) from the binary path, in the above screen, the `-k` value is **Dcomlaunch**. Other services are running the same binary path in the virtual machine attached to this room.

Each will have a different value for ServiceDLL. Let's take LSM as an example and inspect the value for ServiceDLL.
### LSM Properties

> Since svchost.exe will always have multiple running processes on any Windows system, this process has been a target for malicious use. 

Adversaries create malware to masquerade as this process to try and hide amongst the legitimate svchost.exe processes. They can name the malware svchost.exe or misspell it slightly, such as **scvhost.exe**.

- By doing so, the intention is to go under the radar. Another tactic is to install/call a malicious service (DLL).

Extra reading - [Hexacorn Blog](https://www.hexacorn.com/blog/2015/12/18/the-typographical-and-homomorphic-abuse-of-svchost-exe-and-other-popular-file-names/)
### What is Normal?

**Image Path**: %SystemRoot%\System32\svchost.exe
**Parent Process**: services.exe
**Number of Instances**: Many
**User Account**: Varies (SYSTEM, Network Service, Local Service) depending on the svchost.exe instance. In Windows 10, some instances ruin as the logged-in user.
**Start Time**: Typically within seconds of boot time. Other instances of svchost.exe can be started after boot. 
### What is Unusual?

- A parent process other than services.exe
- Image file path other than C:\Windows\System32
- Subtle Misspellings to hide rogue processes in plain sight
- The absence of the `-k` parameter
# lsass.exe

Per Wikipedia, "**Local Security Authority Subsystem Service**" is a process in Microsoft Windows operating systems that is responsible for enforcing the security policy on the system.

It verifies users logging on to a Windows computer or server, handles password changes, and creates access tokens. It also writes to the Windows Security Log.

It creates *security tokens* fpr SAM (Security Account Manager), AD (Active Directory) and NETLOGON. 

- It uses authentication packages specified in `HKLM\System\CurrentControlSet\Control\Lsa`.

# winlogon.exe

> The **Winodws Logon**, **winlogon.exe**, is responsible for handing the ***Secure Attention Sequence*** (SAS).

It is the ALT + CTRL + DELETE key combination users press to enter their username and password. 

This process is also responsible for loading the user profile. It loads the user's NTUSER.DAT into HKCU, and *userinit.exe* loads the user's shell. Read more about this process [here](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc939862(v=technet.10)?redirectedfrom=MSDN).

It is also responsible for *locking the screen* and *running the user's screensaver*, among other functions. You can read more about this process [here](https://en.wikipedia.org/wiki/Winlogon).

Remember from earlier sections, smss.exe launches this process along with a copy of csrss.exe within Session 1.
### What is Normal?

**Image Path**: %SystemRoot%\System32\winlogon.exe
**Parent Process**: Created by an instance of smss.exe that exits, so analysis tools usually do not provide the parent process name.
**Number of Instances**: One or more
**User Account**: Local System
**Start Time**: Within seconds of boot tome fro the first instance (Session 1). Additional instances occur as new sessions are created, typically through Remote Desktop or Fast User Switching logons.
### What is Unusual?

- An actual parent process (smss.exe calls this process and self-terminates)
- Image file path other than `C:\Windows\System32`
- Subtle misspellings to hide rogue processes in plain sight
- Not running as `SYSTEM`
- Shell value in the registry other than explorer.exe
# explorer.exe

> The last process we'll look at is **Windows Explorer**, **explorer.exe**.

This process gives the user access to their folders and files. It also provides functionality to other features, such as the *Start Menu* and *Taskbar*.

As mentioned previously, the *Winlogon* process runs *userinit.exe*, which launches the value in `HKLM\Software\Microsoft\Windows\CurrentVersion\WinLogon\Shell`. *Userinit.exe* exits after spawning *explorer.exe*.

- Because of this, the parent process is non-existent.

There will be many child processes for explorer.exe.
### What is Normal?

**Image Path**: %SystemRoot%\explorer.exe
**Parent Process**: Created by userinit.exe and exits
**Number of Instances**: One or more per interactively logged in user
**User Account**: Logged-in user(s)
**Start Time**: First instance when the first interactive user logon session begins
### What is Unusual?

- An actual parent process. (userinit.exe calls this process and exits)
- Image file path other than C:\Windows
- Running as an unknown user
- Subtle misspellings to hide rogue processes in plain sight
- Outbound TCP/IP connections

**Note**: The above image is the explorer.exe properties view from Process Explorer.
# Conclusion

Earlier it was mentioned that if Credential Guard is enabled on the endpoint, an additional process will be running, which will be a child process to wininit.exe, and that process is lsaiso.exe. This process works with lsass.exe to enhance password protection on the endpoint. 

Other processes with Windows 10 are RuntimeBroker.exe and taskhostw.exe (formerly **taskhost.exe** and **taskhostex.exe**). Please research these processes and any other processes you might be curious about to understand their purpose and their normal functionality. 

The information for this room is derived from multiple sources.

- [https://0xcybery.github.io/blog/Core-Processes-In-Windows-System](https://0xcybery.github.io/blog/Core-Processes-In-Windows-System)[](https://www.threathunting.se/tag/windows-process/)
- [https://www.sans.org/posters/hunt-evil/](https://www.sans.org/posters/hunt-evil/)[](https://www.sans.org/security-resources/posters/hunt-evil/165/download)
- [https://docs.microsoft.com/en-us/sysinternals/resources/windows-internals](https://docs.microsoft.com/en-us/sysinternals/resources/windows-internals)

Other links are provided throughout the room. Reading them at your own leisure to further your foundation and understanding of the core Windows processes is encouraged.


