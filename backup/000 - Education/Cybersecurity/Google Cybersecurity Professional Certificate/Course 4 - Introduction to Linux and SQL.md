Course 4: Tools of the Trade: Linux and SQL

Module 1: Computing Basics for Security Professionals 

> Operating systems and how they relate to applications and hardware

> The Linux operating system

> The Linux command line

> Using SQL to query databases

Module 1:

> Common operating systems

> Main functions of an operating system

> Relationship between operating systems, applications and hardware

> Graphical user interfaces and command-line interfaces

Introduction to Operating Systems

- Operating system
    

- The interface between computer hardware and the user
    
- Responsible for making the computer run efficiently while also making it easy to use
    
- Help computers and humans interface with each other
    

- OS security is critical for cybersecurity professionals
    

- Knowing how OSs work is critical for security tasks
    

Compare Operating Systems

Common Operating Systems

Windows and macOS

> Windows was introduced in 1985, and macOS was introduced in 1984, and both are used in personal and enterprise computers

- Windows is closed-source, meaning the code is not shared openly with the public
    
- macOS is partially open-source, meaning some code is shared with the public, such as the macOS kernel
    

Linux

- First released in 1991
    
- Completely open-source OS
    
- Some Linux distributions are specifically designed for cybersecurity
    

ChromeOS

- Launched in 2011
    
- Partially open-source and derived from the Chromium OS
    
- Frequently used in the education field
    

Android and iOS

- Mobile operating systems
    
- Android was introduced in 2008
    
- iOS introduced in 2007
    

Operating Systems and Vulnerabilities

- Security issues are inevitable with all operating systems
    
- Keeping all of them up to date is a critical part of security for organizations 
    

Legacy Operating Systems

> operating system that is outdated but still being used. 

- Some organization still use legacy operating systems because software they rely on is not compatible with newer operating systems
    
- Most common in industries that use a lot of embedded software, software that’s placed inside components of the equipment itself
    
- Vulnerable to attacks because they’re no longer supported or updated
    

Other Vulnerabilities

- Even up-to-date operating systems are vulnerable to attack
    
- Important for security professionals to be knowledgeable about legacy operating systems and the risks they can create
    

Inside the Operating System

> What happens when you use an operating system?

- Application: a program that performs a specific task
    

Requests to the Operating System

> Explore the complex process of the connections between applications and hardware to allow users to perform tasks.

Booting the Computer

- When you boot a computer, either a BIOS or UEFI chip is activated
    

- These programs contain loading instructions for the computer
    
- UEFI has replaced BIOS in most modern operating systems
    

- The bootloader is a software program that boots the operating system. Once the operating system has finished booting, your computer is ready to use
    

Completing a Task

- User
    

- The user initiates the process by having something they want to accomplish on the computer 
    

- Application
    

- The software program that users want to interact with to complete a task
    

- Operating System
    

- Receives user’s request from the application
    
- OS interprets the request and directs its flow
    

- Hardware
    

- Where all of the processing is done to complete tasks initiated by the user.
    

OS at work Behind the Scenes

- There are processes that someone won’t directly observe when operating a car, but they do feel it and move forward when they press the gas pedal. 
    
- The kitchen in a restaurant is like an OS, you don’t know what happens inside, but the process is conducted for you to receive the food you ordered.
    

  

Example: Downloading a file from an internet browser

- How an OS completes the task of downloading a file from the internet
    

1. The user decides they want to download a file they found online
    
2. The internet browser communicates this action to the OS
    
3. The OS sends the request to download the file to the appropriate hardware for processing
    
4. The hardware begins the file download, and the OS sends this information to the internet browser application, then informs the user when the download is complete
    

Resource Allocation via the OS

> Using a task manager or other resource allocation application to see what resources are being used where is helpful for cybersecurity analysts. You may see that system resources are being directed towards malware.

Virtualization Technology

> Explore how virtual machines work and the benefits of using them

What is a Virtual Machine?

- A virtual machine is a virtual version of a physical computer. Virtual machines are one example of virtualization. Virtualization is the process of using software to create virtual representations of various physical machines.
    
- Software simulates physical hardware
    
- Virtual Systems are just code, no hardware
    

> You can run multiple virtual machines using the physical hardware of a single computer

- Involves dividing the resources of the host computer to be shared across all physical and virtual components. 
    

- RAM  is hardware component for short-term memory. If a computer has 16GB of RAM, it can host three virtual machines with 4GB of RAM each
    

Benefits of Virtual Machines

- Can increase security for many tasks and can also increase efficiency
    

Security

- Virtualization can provide an isolated environment, or a sandbox. When a computer has multiple virtual machines, these virtual machines are “guests” of the computer
    
- These VMs are isolated from the host computer, providing a layer of security.
    

- If the VMs become infected with malware, it can be dealt with more securely because it’s isolated from the other machines.
    
- There are still some risks, as advanced malware authors can spoof this VM system to trick it into behaving like normal software until on the host machine.
    

Efficiency

- You can open multiple virtual machines at once and switch easily between them, allowing you to streamline security tasks, such as testing and exploring various applications.
    
- Separate physical machines aren’t necessary to perform certain tasks.
    

Managing Virtual Machines

- Managed by a software called a hypervisor. Hypervisors help manage multiple virtual machines and connect the virtual and physical hardware.
    

- Also help with allocating shared resources from the host machine
    

- One hypervisor that is useful to be familiar with is the Kernel-based Virtual Machine (KVM)
    

- Open-source hypervisor that is supported by most major Linux distributions
    
- Built into Linux kernel
    

Other Forms of Virtualization

- Some other forms of virtualization do not use operating systems.
    
- Multiple virtual servers can be created from a single physical server. 
    

Graphical User Interface vs. Command Line Interface

> Interfaces are the programs that allow a user to interface with the operating system.

- User Interface 
    

- A program that allows the user to control the functions of the operating system
    

Graphical User Interface: A user interface that uses icons on a screen to manage different tasks on a computer

- Basic GUI components:
    

- Start menu
    
- Task bar
    
- Desktop with icons and shortcuts
    

Command Line Interface: text-based user interface that uses commands to interact with the computer.

- Much different structure than GUI
    
- No icons or graphics
    
- Similar to lines of code 
    
- More flexible and powerful than a GUI
    
- Control / Customization
    

> Allows users to complete multiple tasks simultaneously

Command Line in Use

> Advantages of CLI in cybersecurity:

- Efficiency
    

- It can be used more quickly when you know how to manage the interface
    
- More powerful when needing to do multiple tasks simultaneously and efficiently
    

- History File
    

- The Linux CLI records a history file of all the commands and actions in the CLI
    
- This history file can be used to verify that all commands that are required were successfully used
    
- Can also trace a hacker using this history fie
    

Module 2: Linux

> Linux is the most common OS in the security world

> Architecture of Linux

> Different Linux Distros

> The Shell

Introduction to Linux

> Open-source operating systems

- Created in two parts:
    

- Linus Torvalds took the Unix OS which was already established and improved it, making it open-source
    
- He was revolutionary in the introduction of the Linux kernel
    

- Richard Stallman was working on GNU, another OS based on Unix.
    

- Combined Torvald’s kernel and made what is commonly known today as Linux.
    

Linux Architecture

> Operating systems also have an architecture, just like buildings.

- Linux is a multi-user system
    
- Nano is a text editor native to Linux
    
- Shell is a command line interpreter, used to interface with Linux
    
- Filesystem Hierarchy Standard (FHS)
    

- The component of the Linux OS that organizes data
    
- Filing cabinet of data
    

- Kernel 
    

- Component of the Linux OS that manages processes and memory
    
- Communicates with hardware to execute commands sent by the shell
    
- The kernel uses drivers to enable applications to execute tasks
    
- Linux kernel helps ensure that the system allocates resources more efficiently and makes the system work faster
    

- Hardware
    

- Physical components of a computer
    
- CPU, Mouse and Keyboard
    

Linux Architecture Explained

> Understanding how the system is organized makes it easier to understand how it functions.

- User
    

- Person interacting with the computer
    
- They initiate and manage computer tasks
    
- Multi-user system
    

- Applications
    

- Program that performs a specific task
    
- A package manager is a tool that helps users install, manage and remove packages or applications
    
- A package is a piece of software that can be combined with other packages to form an application
    

- Shell 
    

- Command-line interpreter
    
- Everything entering into the shell is text-based
    
- Allows users to give commands to the kernel and receive responses from it
    
- Translator between you and computer
    

- Filesystem Heirarchy Standard (FHS)
    

- Component of the Linux OS that organizes data
    
- Directory is a file that organizes where other files are stored.
    
- FHS defines how directories, directory contents and other storage is organized so the operating system knows where to find data
    

- Kernel
    

- Component of the Linux OS that manages processes and memory
    
- Communicates with the applications to route commands
    
- Linux kernel is unique to the Linux OS and is critical for allocating resources to the system
    

- Hardware
    

- Physical components of a computer
    
- Hard drives, CPU, etc.
    
- Peripheral Drives
    

- Attached and controlled by the computer system
    
- Not core components needed to run the computer system
    

- Monitors, printers, keyboards and mice
    

- Internal Hardware
    

- Required to run the computer
    
- Main circuit board and all components attached to it
    

- Central Processing Unit: computer’s main processor, which is used to perform general computing tasks on a computer
    
- Random Access Memory (RAM): hardware component used for short-term memory
    

- Data is stored there temporarily
    

- Hard drive: component used for long term memory
    

- Programs and files are stored here
    
- Can be accessed even when a computer has been turned off
    

Linux Distributions

> Linux is a very customizable operating system

> Unlike other OS, there are different versions available for you to use, called distributions.

- Debian is a different distribution than Ubuntu, and has a different toolset.
    

> The kernel is the most important component of the Linux OS.

> Different distributions are used for different reasons.

Parent Distributions

- RedHat Enterprise Linux (CentOS)
    
- Slackware (SUSE)
    
- Debian (Ubuntu and KALI LINUX)
    

Kali Linux

> Trademark of Offensive Security and is Debian derived

> Kali Linux should be used in a virtual machine to prevent damage to your system i the tools are used improperly

- VMs also give you the ability to revert to a previous state
    

Penetration Test

- Simulated attack that helps identify vulnerabilities in systems, networks, websites, applications and processes
    

Penetration Testing Tools in KALI LINUX

- Metasploit
    
- Burp suite
    
- John the Ripper
    

Digital Forensics

- The practice of collecting and analyzing data to determine what has happened after and attack
    

Digital Forensics Tools in KALI LINUX

- Tcpdump
    
- Wireshark
    
- Autopsy
    

More Linux Distributions

KALI LINUX

- Open-source distribution of Linux that is widely used in the security industry
    
- Pre-installed with many useful tools for penetration testing and digital forensics
    

Ubuntu

- Open-source, user friendly distribution that is widely used in security and other industries
    
- Has both a CLI and GUI 
    
- Debian-derived and includes common applications by default
    
- Large number of community support and resources
    

Parrot

- Open-source distro that is commonly used for security
    
- Comes with pre-installed security tools related to pen testing and digital forensics
    
- Based on Debian 
    
- Considered user-friendly
    

RedHat Enterprise Linux

- Subscription based version of Linux built for enterprise use. 
    
- Dedicated support team for customers to call about issues.
    

CentOS

- Open-source distribution that is closely related to Red Hat.
    
- Uses source-code published by Red Hat to provide a similar platform
    
- Doesn’t offer the same enterprise support that Red hat does
    

Package Managers for Installing Applications

> Apply knowledge to learn more about package managers

Introduction to Package Managers

- A package is a piece of software that can be combined with other packages to aform and application
    

- Contains necessary files for an application to be installed
    
- Includes dependencies, which are supplemental files used to run an application
    

- Package managers can help resolve any issues with dependencies and perform other managerial tasks
    

- Package managers are tools that help users install, manage and remove packages or applications
    

Types of Package Managers

- Many commonly used Linux distributions are derived from the same parent distribution. 
    
- KALI, Ubuntu and Parrot all come from Debian. CentOS comes from Redhat
    

> Certain package managers work with certain distributions

- Different package managers use different file extensions
    

- Redhat has the .rpm file extension
    
- Debian derived package managers use .deb file extension
    

Package Management Tools 

-  There are also package management tools that allow you to easily work with packages through the shell.
    
- Advanced Package Tool (APT)
    

- Used with Debian-derived distributions. It is run from the command-line interface to manage, search and install packages.
    

- Yellowdog Updater Modified (YUM)
    

- Used with Redhat derived distributions. 
    
- Run from the command line to manage, search and install packages, works with .rpm files
    

Resources for Completing Linux Labs

> Use a platform like QwikLabs to complete lab assignments

How to Use Qwiklabs

> Launch app, new tab will open that contains lab instructions

Start Lab Button

> Start lab opens a temporary terminal. Instructions will move to the right side of the screen

Lab Control Dialog Box

> After Start Lab, a lab control dialog box opens. It contains the End Lab button, the timer and the Open Linux Console button

The Timer

> Starts when the terminal has loaded, and keeps track of the amount of time you have left to complete a lab.

> When the timer reaches zero, your temporary terminal and resources are deleted. 

Open Linux Console

> Opens a new browser window with the console

Check Progress

> Allows you to check your progress by clicking check my progress at the end of each task.

> Allows user to receive a hint

Using copy/paste commands

> Using Crtl+C will open a dialog box asking the user to allow the use of those shortcuts in the lab

Code Block

Certain steps may include a code block. Click the copy button to copy the code provided and then paste it into the terminal

> Terminal is active when the cursor in the terminal changes from a static empty outline to a flashing solid block.

Scrolling

> In certain situations, you may want to scroll within the terminal window. Use the scroll wheel on your mouse or touchpad

End Lab Button

> Ends the lab, make sure you have completed the tasks in the lab

Introduction to the Shell

- Command: instruction sent to the computer telling it to do something
    

- Shell interacts with the kernel to execute these commands
    

- Think of the shell as a language interpreter between the computer and yourself
    

Different Types of Shells

> Review shells and introduce you to different types, including the one that you’ll use in this course

Communicate Through a Shell

- Shell allows you to give commands to the computer and receive responses from it.
    
- When entering a command into the shell, it executes many internal processes to interpret your command, send it to the kernel, and return the results
    

Types of Shells

- Bourne-again Shell (bash)
    
- C Shell (csh)
    
- Korn shell (ksh)
    
- Enhanced C Shell (tcsh)
    
- Z shell (zsh)
    

Bash

- The default shell in most Linux distributions. It’s considered a user friendly shell
    
- Can be used for basic Linux commands or for larger projects
    
- Most popular shell in cybersecurity profession
    

  
  

Input and Output from the Shell

- Standard input consists of information received by the OS via the command line.
    
- If the shell can interpret your request, it asks the kernel for the resources it needs to execute the related task
    

> echo - a Linux command that outputs a specific string of text

> string data - data consisting of an ordered sequence of characters

- Standard Output is the information returned by the OS through the Shell
    
- Standard Errors are messages returned by the OS through the shell
    

Module 3: More Advanced Linux Operations

Linux Commands via the Bash Shell

Essential Command Line Tasks for Security Analysts:

> Work with server logs

> Navigate, manage and analyze files remotely

> Verify and configure users and group access

> Give authorization and set file permissions

Bash is the default shell in most Linux distributions

- The key Linux commands that you’ll be learning in this lesson are the same across shells. 
    

> An argument (linux) is specific information needed by a command

- All commands and arguments are case-sensitive
    

Core Command for Navigation and Reading Files

- Imagine a tree. The roots, branches and trunk are all similar to how we think about a Linux operating system.
    
- The Filesystem Hierarchy Standard, or FHS, is the component of the Linux OS that organizes data.
    

- The file system in Linux is very important because everything we do in Linux is considered a file somewhere in the system’s directory
    

- The root directory in Linux is the highest-level directory
    
- Sub-directories branch out from the root directory, going further and further into more subdirectories.
    

Common Commands for Navigating the Filesystem

- Pwd - present working directory - displays the working directory to the screen
    
- Ls - displays the names of files and directories in the current working directory
    
- Cd - change directory - place in from of a directory to change to that directory
    
- Cat - displays the content of a file
    
- Head - displays just the beginning of a file by the first 10 lines
    

Navigate Linux and Read File Content

> Explore the organization of the Linux Filesystem Hierarchy Standard (FHS), review several common Linux commands for navigation and reading file content, and learn a couple of new commands

Filesystem Hierarchy Standard (FHS)

- Component of Linux that organizes data. 
    
- Defines how directories, directory contents and other storage is organized in the operating system
    
-  A file path is the location of a file or directory. In the file path, the different levels of the hierarchy are separated by a forward slash (/).
    

Root directory

- Highest level directory in Linux, and always represented with a  forward slash(/). All subdirectories branch off the root directory.
    

Standard FHS Directories

- Directly below the root directory, you’ll find standard FHS directories. In the diagram, home, bin and  etc are standard FHS directories.
    
- Here are a few examples of what standard directories contain:
    

- /home: each user in the system gets their own directory
    
- /bin: this directory stands for “binary” and contains binary files and other executables. Executables are fuels that contain a series of commands a computer needs to follow to run programs and perform other functions
    
- /etc: this directory stores the system’s configuration files
    
- /tmp: this directory stores many temporary files. The /tcp directory is commonly used by attackers because anyone in the system can modify data in these files
    
- /mnt: directory stands for “mount” and stores media, such as a USB drive and hard drives
    

User-specific subdirectories

Under home are subdirectories for specific users. In the diagram, these users are analyst and analyst2. Each user has their own personal subdirectories, such as projects, logs or reports.

Note: when a subdirectory leads below the user’s home directory, the user’s home directory can be represented as the tilde (~).

> The absolute file path is the full file path, which starts from the root. 

> the relative file path is the file path that starts from a user’s current directory

Key Commands for Navigating the File System

The following Linux commands can be used to navigate the file system: pwd, ls and cd.

Pwd: prints the working directory to the screen, meaning it returns the directory that you’re currently using.

- The output gives you the absolute path to the directory
    
- You can use whoami to return the username of the current user.
    

Ls: displays the names of the files and directories in the current working directory. 

Cd: navigates between directories.

- When you need to change directories, you should use this command
    

Common Commands for Reading File Content

The following Linux commands are useful for reading file content: cat, head, tail and less.

Cat

> the cat command displays the content of a file. Entering cat updates.txt returns everything in the updates.txt file

Head

> the head command displays just the beginning of a file, by default 10 lines. The head command can be useful when you want to know the basic contents of a file but don’t need the full contents. 

Pro-tip: you can change the number of lines returned by head, you can specify the number of lines by including -n. E.g. “head -n 5”

tail 

> the tail command does the opposite of head. This command can be used to display just the end of a file, by default 10 lines.

Less

> the less command returns the content of a file page one page at a time. 

> For example, entering less updates.txt changes the terminal window to display the contents of updates.txt one page at a time. This allows you to easily move forward and backward through the content.

> Once you’ve accessed your content with the less command, you can use several keyboard controls to move through the file: 

- Space bar: move forward one page
    
- B: move back one page
    
- Down Arrow: move forward one line
    
- Up arrow: move back one line
    
- Q: quit and return to the previous terminal window
    

Find What You Need with Linux

> As a security analyst, your work will likely involve filtering for the information you need. 

- Filtering means searching  your system for specific information that can help you solve complex problems
    

Grep

- The grep command searches a specified file and returns all lines in the file containing a specified string. Here’s an example of this. Let’s say we have a file called updates.txt, and we’re currently looking for lines that contain the word: OS.
    
- The grep command is followed by two arguments
    

- The first argument is the string we’re searching for
    
- The second argument is the name of the file we’re searching through, updates.txt
    

Piping

- Piping is a Linux command that can be used for a variety of purposes. 
    
- The piping command sends a standard output of one command as standard input into another command for further processing
    

- Represented by the vertical bar character
    
- Linux piping involves redirection just like physical piping
    
- Output from one command is sent through the pipe, then comes out on the other end of the pipe.
    

Filtering Content in Linux

> Learn a new Linux command, find, which can help you search files and directories for specific information

Filtering for Information

- Filtering is selecting data that match a certain condition
    
- For example, if you had a virus that old  affected the .txt files, you could use filtering to find these files quickly
    
- Filtering allows you to search based on specific criteria, such as file extension or a string of text.
    

Grep

- The grep command searches a specified file and returns all lines in the file containing a specified string or text. 
    
- The grep command commonly takes two arguments: a specific string to search for and a specific file to search through
    

Piping

- Accessed by using the pipe character: “|” 
    
- Piping sends the standard output of one command as standard input to another command for further processing.
    

- Standard output is the information returned by the OS through the shell
    
- Standard input is information received by the OS via the command line
    

Note: you can think of piping as a general tool that you can use whenever you want the output of one command to become the input of another command.

Find

- The find command searches for directories and files that meet specified criteria. There’s a wide range of criteria that can be specified with find. For example, you can search for files and directories that: 
    

- Contain a specific string in the name
    
- Are a certain file size
    
- Were last modified within a certain time frame
    

- When using find, the first argument after find indicates where to start searching. For example, entering find /home/analyst/projects searches for everything starting at the projects directory
    
- After this first argument, you need to indicate your criteria for the search. If you don’t include a specific search criteria with your second argument, your search will likely return a lot of directories and files.
    

-name and -iname 

One key criteria analysts might use with find  is to find file or directory names that contain a specific string.

- The specific string you’re looking for must be entered in quotes after the -name or -iname options
    
- -name is case sensitive, -iname is not
    

-mtime 

- Security analysts might also use find to find files or directories last modified within a certain time frame. The -mtime option can be used for this search. For example, entering find /home/analyst/projects -mtime -3 returns all files and directories in the projects directory that have been modified with the past three days
    

Create and Modify Directories and Files

> When working with data in security, organization is key. 

- Let’s take a look at some essential commands for creating and removing directories.
    
- For example, within a directory for reports an analyst may need to create two subdirectories: one for drafts and one for final reports.
    

Commands for Creating and Removing Directories

> mkdir command creates a new directory

- You can either provide the new directory as the absolute file path, which starts from the root, or as a relative file path, which starts from your directory
    
- Use the ls command to confirm the new directory was added
    

  

> rmdir removes or deletes a directory

- Contains a built in warning that lets you know a directory is not empty
    
- This warning saves you from accidentally deleting files
    

Creating and Modifying Files

Touch 

- Creates a new file
    

- This file won’t have any content inside
    
- Entering touch permissions.txt creates a new file in the reports subdirectory called permissions.txt
    

Rm 

- Removes or deletes a file
    
- Should be used carefully because it’s not easy to recover files deleted with rm. To remove the permissions file you just created, enter rm permissions.txt 
    

Mv and cp

- You can use mv and cp when working with files. The mv command moves a file or directory to a new location, and the cp command copies a file or directory into a new location
    
- The first argument after mv or cp is the file or directory you want to move or copy, and the second argument is the location you want to move or copy it to.
    

Nano Text Editor

- Nano is a command line file editor that is available by default in many Linux distributions.
    
- Many beginners find it easy to use, and it’s widely used in the security profession
    
- Multiple basic tasks can be performed in nano 
    

- Creating new files
    
- Modifying file contents
    

- To open an existing file in nano form the directory that contains it, enter nano followed by the filename.
    

Standard output redirection

- In addition to piping, you can also use the right angle bracket (>) and the double right angle bracket (>>) operators to redirect standard output
    

- The difference between the two is that > overwrites your existing file, and >> adds your content to the end of the existing file instead of overwriting it. 
    
- The > should be used carefully, as it is not easy to recover overwritten files
    

File Permissions and Ownership

> Permissions

- The type of access granted for a file or directory
    
- Permissions are related to authorization
    

- Authorization allows you to limit access to specified files or directories
    
- Allows you to limit access to specified files or directories
    

Permissions in Linux

- Read
    

- Means that contents of the file can be read
    

- Write
    

- Allows modifications of contents of the file
    
- Indicates that new files can be created in that directory
    

- Execute
    

- Means that files can be executed if it’s an executable file
    
- Allows users to enter into a directory and access it’s files
    

Types of Owners

- User
    

- Owner of the file
    
- When a file is created, the user becomes the owner, but ownership can be transferred
    

- Group
    

- Consists of several users
    

- Other
    

- Considered all other users on a system
    
- Anyone else with access to the system belongs to this group
    

> File permissions in Linux are represented in a 10-character string.

- For a directory with full permissions for the user group, this string would be: drwxrwxrwx
    

World-writable files pose a significant security risk, because there are no access permissions for the file

How to Check Permissions?

Ls -l

- Displays permissions to files and directories.
    

Ls -a

- Displays hidden files. You can combine these two options (ls -l & ls -a)
    

Ls -la

- Displays permissions to files and directories, including hidden files
    

Change Permissions in Linux File Hierarchy

> Permission changes are necessary in order to protect system files from being accidentally or deliberately altered or deleted.

chmod changes permissions on files and directories

- Stands for change mode
    

> There are two modes for changing permissions, but we’ll focus on symbolic. The best way to learn about how chmod works is through an example. I know this is a lot of details, but we’ll break this down. 

> with chmod. You need to identify which file or directory you want to adjust permissions for. 

- This is the final argument, in this case. 
    

Types of Owners

- User = u
    
- Group = g
    
- Other = o
    

Reading Permissions

>> In Linux, permissions are represented with a 10-character string. Permissions include:

- read: for files, this is the ability to read the file contents; for directories, this is the ability to read all contents in the directory including both files and subdirectories
    
- write: for files, this is the ability to make modifications on the file contents; for directories, this is the ability to create new files in the directory
    
- execute: for files, this is the ability to execute the file if it’s a program; for directories, this is the ability to enter the directory and access it’s files
    

The permissions are given to these types of owners:

- user: the owner of the file
    
- group: a larger group that the owner is a part of
    
- other: all other users on the system 
    

Each character in the 10-character string conveys different information about these permissions. The following table describes the purpose of each character:

  

|   |   |   |
|---|---|---|
|Character|Example|Meaning|
|1st|drwxrwxrwx|File type<br><br>- D for directory<br>    <br>- - for a regular file|
|2nd|drwxrwxrwx|Read permissions for the user<br><br>- R if the user has read permissions<br>    <br>- - if the user lacks read permissions|
|3rd|drwxrwxrwx|Write permissions for the user<br><br>- W if the user has write permissions<br>    <br>- - if the user lacks write permissions|
|4th|drwxrwxrwx|Execute permissions for the user<br><br>- X if the user has execute permissions<br>    <br>- - if the user lacks execute permissions|
|5th|drwxrwxrwx|Read permissions for the group<br><br>- R if the group has read permissions<br>    <br>- - if the group lacks read permissions|
|6th|drwxrwxrwx|Write permissions for the group<br><br>- W if the group has write permissions<br>    <br>- - if the group lacks write permissions|
|7th|drwxrwxrwx|Execute permissions for the group<br><br>- X if the group has execute permissions<br>    <br>- - if the group lacks execute permissions|
|8th|drwxrwxrwx|Read permissions for other<br><br>- R if the other owner type has read permissions<br>    <br>- - if the other owner type lacks read permissions|
|9th|drwxrwxrwx|Write permissions for other<br><br>- W if the other owner type has write permissions<br>    <br>- - if the other owner type lacks write permissions|
|10th|drwxrwxrwx|Execute permissions<br><br>- X if the other owner type has execute permissions<br>    <br>- - if the other owner type lacks execute permissions|

Exploring Existing Permissions

> You can use the ls command to investigate who has permissions on files and directories

Additional Options with ls Command:

- ls -a: displays hidden files. Hidden files start with a . at the beginning
    
- ls -l: displays permissions to files and directories. Also displays other additional information, including owner name, group, file size and the time of last modification
    
- ls -la: displays permissions to files and directories, including hidden files. This is a combination of the above options
    

Changing Permissions

>> The principle of least privilege is the concept of granting only the minimal access and authorization required to complete a task or function. 

- Users should not have privileges that are beyond what is necessary
    
- Not following the principle of least privilege can lead to security risks
    

>> the chmod command can help you manage this authorization. 

- chmod changes permissions on files and directories
    

Using chmod

- The chmod command requires two arguments. The first argument indicates how to change permissions, and the second argument indicates the file or directory that you want to change permissions for. 
    
- You can also use an = (equals sign) in the first argument. This assigns the permissions exactly as specified
    
- The equals sign method overwrites and existing permissions
    

  

|   |   |
|---|---|
|Character|Description|
|u|Indicates changes will be made to user permissions|
|g|Indicates changes will be made to group permissions|
|o|Indicates changes will be made to other permissions|
|+|Adds permissions to the user, group or other|
|-|Removes permissions from the user, group or other|
|=|Assigns permissions for the user, group or other|

Note: when there are permission changes to more than one owner type, commas are needed to separate changes for each owner type

Adding and Deleting Users

> Adding and deleting users is related to the concept of authentication.

> Authentication is the process of a user proving that they are who they say they are in the system.

- Root User: a user with elevated privileges to modify a system
    

- Root user does not have limitations, like regular users
    
- Running commands as the root user is considered bad practice when using Linux
    

Problems with Logging in as Root

- Security risks
    

- Hackers will try to breach the root account, since it has the most privileges
    
- To stay safe, the root account should have logins disabled
    

- Irreversible mistakes
    

- Easy to make the wrong command in the CLI, and if you’re running as the root user, you run a higher risk of making a mistake that cannot be reverted, like permanently deleting a directory
    

- Accountability
    

- You cannot track commands input by the root user
    

sudo - a command that temporarily grants elevated permissions to specific users

- This provides a more controlled approach compared to root
    
- Solves most problems associated with running commands as root
    

> running sudo will prompt you to enter the password for the user you’re currently logged in as

- Users must be granted sudo access through a configuration file called the sudoers file.
    

> useradd: adds a user to the system

- Only root or sudo privilege users can use the useradd command
    

> userdel: deletes a user from the system

- Requires sudo privileges, just like useradd
    

Responsible use of Sudo

> the sudo command is important for security analysts because it allows users to have elevated permissions without risking the system by running commands as the root user

- The sudo command temporarily grants super user access to an account for specific users. 
    

- Command derives it’s name from “super user do”
    

- Although using sudo is preferable to using the root, it’s important to be aware that users with the elevated permissions to use sudo might be more at risk in the event of an attack
    
- You should be careful using sudo and only use it for the commands you need, and nothing more. 
    
- Running commands as sudo allows users to bypass the normal security controls that are in place to prevent elevated access to an attacker.
    

Authentication and Authorization with Sudo

> Authentication is the process of verifying who someone is

> Authorization is the concept of granting access to specific resources in a system

useradd: adds a user to a system

- To add the user with username fgarcia, enter sudo useradd fgarcia. 
    

- -g sets the user’s default group, also called their primary group
    
- -G adds the user to additional groups, also called supplemental or secondary groups
    

  

usermod: modifies existing user accounts. 

- The same -g and -G commands from the useradd command can be used with usermod if a user already exists
    
- -a option appends the user to an existing group and is only used with the -G option
    

Note: if you don’t include the -a option, -G will replace any existing supplemental groups with the groups specified after usermod

Other Commands that can be used with usermod:

- -d changes the user’s home directory
    
- -l changes the user’s login name
    
- -L locks the account so the user can’t login
    

userdel: command deletes a user from the system. For example, sudo userdel fgarcia deletes fgarcia as a user. Be careful before you delete a user using this command.

- Userdel doesn’t delete the files in the user’s home directory unless you use the -r option.
    
- Before deleting any files, you should make sure backups have been made in case you need them later.
    
- Using usermod -L is sometimes more beneficial, since it locks the account, allowing you to transfer files and ownership to other users without deleting everything.
    

chown: command changes the ownership of a file or directory.

- You can use chown to change user or group ownership.
    

Get Help in Linux

>> Resources available directly through the bash shell

- man: displays information on other commands and how they work
    

- Comes from the word “manual”
    

- whatis: displays a description of a command on a single line
    
- apropos: searches the manual page descriptions for a specified string
    

Linux Resources

>> When you’re aware of the resources available to you, you can continue to use Linux independently

>> You can also discover even more ways that Linux can support your work as a security analyst

Linux Community

>> Linux has a large online community, and this is a huge resource for Linux users of all levels. You can find the answers to your questions with a simple online search

>> the UNIX and Linux Stack Exchange is a trusted resource for troubleshooting Linux issues. 

Integrated Linux Support

>> Linux has several commands that can be used for support

- Man
    
- Whatis
    
- Apropos
    

Module 4: SQL

>> In this section, we will explore SQL

- Relational databases
    
- SQL queries
    
- SQL filters
    
- SQL joins
    

Introduction to Databases

>> When working with large amounts of data, we need to know how to store it, so it’s organized and quick to access

- The solution is through databases
    

Database: an organized collection of information or data

- Often compared to spreadsheets
    

- Spreadsheets are often designed for a single user or small group
    

- Databases can be accessed by multiple people simultaneously
    
- Store massive amounts of data
    
- Perform complex tasks while accessing data
    

  

Databases for Security Analysts:

- You’ll often need to access databases containing useful information
    
- Databases can store:
    

- Info on login attempts
    
- Software and software updates
    
- Machines and their owners
    

How Databases are Organized:

- Relational Database:
    

- Structured database containing tables that are related to each other
    
- Each table contains fields of information
    

- Tables contain rows called “records”
    
- Rows are filled with specific data related to the columns in the table
    

- Primary Key:
    

- A column where every row has a unique entry
    
- The primary key must not have any duplicate values, or any null or empty values
    

- Foreign Key:
    

- A column in a table that is a primary key in another table
    
- Allows us to connect two tables together
    

- A table can have only one Primary Key, but multiple Foreign Keys
    

Query Databases with SQL

>> SQL (Structured Query Language)

- A programming language used to create, interact with, and request information from a database
    

Query:

- A request for data from a database table or a combination of tables
    

>> Nearly all relational databases rely on SQL to query data

- Different variations of SQL only have slight differences in their structure, like where to place quotation marks.
    

Log: 

- A record of events that occur within an organization’s systems
    
- Some logs might contain details on machines used in a company
    

- You will need to locate the machines that weren’t configured properly
    

- Other logs may contain info describing visitors to your website or web app and the tasks they performed
    

- You might be looking for unusual patterns that may point to malicious activity
    

- Security logs are often very large and hard to process
    

SQL Filtering vs Linux Filtering

>> Explore the differences between Linux and SQL 

>> One way to access SQL is through the Linux command line

Accessing SQL

- To access SQL from Linux, you need to type in a common for the version of SQL that you want to use. 
    

- e.g. if you want to access SQLite, you can enter the command sqlite3
    

- Commands typed after sqlite3 will be directed to SQL instead of Linux
    

Differences Between Linux and SQL Filtering

- Purpose:
    

- Linux filters data in the context of files and directories on a computer system
    
- Used for tasks like:
    

- Searching for specific files
    
- Manipulating file permissions
    
- Managing processes
    

- SQL is used to filter data within a database management system
    

- Used for querying and manipulating data stored in tables and retrieving specific information based on defined criteria
    

- Syntax:
    

- Linux uses various commands and command-line options specific to each filtering tool
    

- Syntax varies depending on the tool and purpose
    

- SQL uses the Structured Query Language, a standardized language with specific keywords and clauses for filtering data across different SQL databases
    

- WHERE, SELECT, JOIN
    

- Structure:
    

- SQL offers a lot more structure than Linux, which is more free-form and not as tidy
    
- SQL provides results that are more easily readable and that can be adjusted more quickly than when using Linux
    

- Joining Tables
    

- SQL allows the analyst to join multiple tables together when returning data
    
- Linux doesn’t have the same functionality, and doesn’t allow the information to be connected to other information on your computer
    

- Best Uses
    

- As a security analyst, it’s important to understand when you can use each tool.
    
- A lot of data used in cybersecurity will be stored in a database format that works with SQL. However, other logs might be in a format that is not compatible with SQL.
    
- If the data is stored in a text file, you cannot search it through SQL
    

- In these cases, it is useful to know how to filter in Linux
    

SQL Queries

>> SQL query based on a common work task you may encounter as a security analyst

- SELECT: indicates which columns to return
    
- FROM: indicates which table to query
    

Query a Database

>> Review those basic SQL queries and learn a new keyword that will help you organize your output.

>> Also learn the Chinook database, which this course uses for queries in readings and quizzes.

Basic SQL Query

>> Two essential keywords in any SQL query: SELECT and FROM. 

- You will use these keywords any time you want to query an SQL database.
    
- Helps SQL identify what data you need from a database and the table you are returning it from.
    

SELECT

- The SELECT keyword indicates which columns to return. 
    
- You can also select multiple columns by separating them with a comma
    
- If you want to return all columns in a table, you can follow the SELECT keyword with an asterisk (SELECT *)
    

Note: using SELECT * may not be advisable when working with large databases and tables; in those cases, the final output may be difficult to understand and might be slow to run.

FROM: 

>> The SELECT keyword always comes with the FROM keyword. FROM indicates which table to query.

- To use FROM, you should write it after the SELECT keyword, often on a new line, and follow it with the name of the table you’re querying. 
    
- Use a semicolon (;) to indicate the end of the query
    

ORDER BY:

- Databases are often very complicated, and this is where other SQL keywords come in handy. ORDER BY is an important keyword for organizing the data you extract from a table.
    
- ORDER BY sequences the records returned by a query based on a specified column or columns. 
    

- This can be either in ascending or descending order.
    

>> Sort In Ascending Order

- To use the ORDER BY keyword, write it at the end of the query and specify a column to base the sort on. 
    
- The ORDER BY keyword sorts the records based on the column specified after this keyword. 
    

- By default, this will be output in ascending order.
    
- If you choose a column containing numeric data, it sorts the output from the smallest to largest.
    
- If the column contains alphabetic characters, such as in the example with the city column, it orders records from the beginning of the alphabet to the end
    

>> Sort in Descending Order

- You can also use the ORDER BY with the DESC keyword to sort in descending order. 
    
- The DESC keyword is short for “descending” and tells SQL to sort numbers from smallest to largest, or alphabetically from Z to A.
    

Sorting Based on Multiple Columns

- You can also choose multiple columns to order by.
    
- After the ORDER BY keyword, include additional modifiers separated by columns and end the query with a semicolon
    

Basic Filters in SQL

>> Filtering: selecting data that match a certain condition

- Only choosing the data we want
    

>> Operator: a symbol or keyword that represents an operation

- e.g. (=), (+), (-)
    

>> WHERE: indicates the condition for a filter

>> LIKE: operator used with WHERE to search for a pattern in a column

The WHERE Clause and Basic Operators

>> Further explore how to use the WHERE clause, the LIKE operator and the percentage (%) wildcard.

How Filtering Helps

- As a SOC analyst, you’ll often be responsible for working with very large and complicated security logs. To find the information you need, you’ll often need to use SQL to filter the logs.
    
- In a cybersecurity context, you might use filters to find the login attempts of a specific user or all login attempts made at the time of a security issue
    

- You might filter to find the devices that are running a specific version of an application
    

WHERE 

>> To create a filter in SQL, you need to use the keyword WHERE. 

- WHERE indicates the condition for a filter
    
- Rather than returning all records, the WHERE clause instructs SQL to return only those that contain a certain keyword, like “IT Staff”
    

Filtering For Patterns

- You can also filter based on a pattern, for example, you can identify entries that start or end with a certain character or character.
    
- Filtering for a pattern requires incorporating two more elements into your WHERE clause:
    

- A wildcard
    
- The LIKE operator
    

Wildcards

- A wildcard is a special character that can be substituted with any other character. Two of the most useful wildcards are the percentage sign (%) and the underscore (_):
    

- The percentage sign substitutes for any number of other characters
    
- The underscore symbol only substitutes for one other character
    

>> These wildcards can be placed after a string, before a string, or in both locations depending on the pattern you’re filtering for. 

>> The following table includes these wildcards applied to the string ‘a’ and examples of what each pattern would return.

  

|   |   |
|---|---|
|Pattern|Results that could be returned|
|‘a%’|Apple123, art, a|
|“a_’|as, an, a7|
|‘a__’|ant, add, a1c|
|‘%a’|pizza, Z6ra, a|
|‘_a’|ma, 1a, ha|
|‘%a%’|Again, back, a|
|‘_a_’|Car, ban, ea7|

LIKE

>> to apply wildcards to the filter, you need to use the LIKE operator instead of an equals sign (=). LIKE is used with WHERE to search for a pattern in a column.

Common Data Types

- String
    
- Numeric
    
- Date and time
    

  
  

String Data: Data consisting of an order sequence of characters

- Numbers, Letters, or symbols
    
- String data will be encountered in usernames, like “analyst10”
    

Numeric Data: data consisting of numbers

- Unlike strings, mathematical operators can be used on numeric data, like multiplication or addition
    

Date and Time

- Consists of data representing a date and/or time
    

Operators

- =
    
- >
    
- <
    
- <>
    
- >=
    
- <=
    

BETWEEN 

- Operator that filters for numbers or dates within a range
    

Operators for Filtering Dates and Numbers

>> New examples of using operators in filters

Numbers, dates and times in Cybersecurity

- Security analysts work with more than just string data
    
- Often frequently work with numeric data, or data consisting of numbers.
    

- The number of login attempts
    
- The count of a specific type of log entry
    
- The volume of data being sent from a source
    
- The volume of data being sent to a destination
    

You’ll also encounter date and time data, or data representing a date and/or time. As a first example, logs will generally timestamp every record. Other data and time data might include:

- Login dates
    
- Login times
    
- Dates for patches
    
- The duration of a connection
    

Comparison Operators

>> In SQL, filtering numeric and data and time data often involves operators. You can use the following operators in your filters to make sure you return only the rows you need:

  

|   |   |
|---|---|
|operator|use|
|<|Less than|
|>|Greater than|
|=|Equal to|
|<=|Less than or equal to|
|>=|Greater than or equal to|
|<> or !=|Not equal to|

Incorporating Operators into Filters

>> these comparison operators are used in the WHERE clause at the end of a query. 

- In other words, the > operator is exclusive and the >= operator is inclusive. An exclusive operator is an operator that does not include the value of comparison. An inclusive operator is an operator that includes the value of comparison.
    

BETWEEN

>> Another operator used for numeric data as well as date and time data is the BETWEEN operator.

- BETWEEN filters for numbers or dates within a range
    
- The BETWEEN operator is inclusive. This means records with a hiredate of January 1, 2002 or January 1, 2003 are included in the results of the previous query
    

  
  
  

Filters with AND, OR and NOT

>> When working with real security questions, we often have to filter for multiple conditions.

- Vulnerabilities might depend on more than one factor
    
- A security vulnerability might be related to machines using a specific email client on a specific operating system, so we need to find machines using both the email client and operating system.
    

AND Operator

- Specifies that both conditions must be met simultaneously
    
- To make a query with multiple conditions that must be met, we use the AND operator between two separate conditions. 
    

OR Operator

- Specifies that either condition can be met
    
- When conjoined with OR, SQL would select all rows that satisfy one of the conditions.
    

NOT Operator

- Negates a condition
    
- SQL will return every entry that does NOT match our condition
    
- Only works on a single condition
    

Logical Operators

>> AND, OR and NOT: allow you to filter your queries and return the specific information that will help you in your work as a security analyst. 

Combining Logical Operators

>> Logical operators can be combined in filters. For example, if you know that both the USA and Canada are not affected by a cybersecurity issue, you can combine operators to return customers in all countries besides the two. 

  

Join Tables in SQL

>> Having the ability to combine SQL tables

- In SQL statements that contain two columns, SQL needs to know which column we’re referring to. 
    

- The way to resolve this is by writing the name of the table first, then a period, followed by the name of a column
    
- employees.employee_id 
    
- machines.employee_id
    

- INNER JOIN
    

- Returns rows matching on a specified column that exists in more than one table
    

Types of Outer Joins

- LEFT JOIN
    
- RIGHT JOIN
    
- FULL OUTER JOIN
    

  

- LEFT JOIN: returns all of the records of the first table, but only returns rows of the second table that match on a specified column
    
- RIGHT JOIN: returns all of the records of the first table, but only returns rows of the second table that match on a specified column
    
- FULL OUTER JOIN: returns all records from both tables
    

Compare Types of Joins

>> Review concepts and more closely analyze the syntax needed for each type of join.

Inner Joins

- Returns rows matching on a specified column that exists in more than one table
    
- It only returns the rows where there is a match, but like other types of joins, it returns all specified columns from all joined tables. 
    

- For example, if the query joins two tables with SELECT *, all columns in both of the tables are returned. 
    

The Syntax of an Inner Join

>> To write a query using INNER JOIN , you can use the following syntax:

SELECT *

FROM employees

INNER JOIN machines ON employees.device_id = machines.device_id;

You must specify the two tables to join by including the first or left table after FROM and the second or right table after INNER JOIN.

- After the name of the right tables, use the ON keyword and the = operator to indicate the column you are joining the tables on. It’s important that you specify both the table and column names in this portion of the join by placing a period(.) between the table and the column.
    
- In addition to selecting all columns, you can select only certain columns. For example, if you only want the join to return the username, operating_system and device_id columns, you can write this query:
    

Outer Joins

>> Outer joins expand what is returned from a join. Each type of outer join returns all rows from either one table or both tables.

Left Joins

>> When joining two tables, LEFT JOIN returns all the records of the first table, but only returns rows of the second table that match on a specified column.

- The syntax for using LEFT JOIN is demonstrated by the following query:
    

SELECT *

FROM employees

LEFT JOIN machines ON employees.device_id = machines.device_id;

- As with all joins, you should specify the first or left table as the table that comes after FROM and the second or right table as the table that comes after LEFT JOIN.
    
- In the example query, because employees is the left table, all of its records are returned. Only records that match on the device_id column are returned from the right table, machines.
    

Right Joins

>> When joining two tables, RIGHT JOIN returns all of the records of the second table, but only returns rows from the first table that match on a specified column.

The following demonstrates the syntax for RIGHT JOIN:

SELECT *

FROM employees

RIGHT JOIN machines ON employees.device_id = machines.device_id;

RIGHT JOIN has the same syntax as LEFT JOIN, with the only difference being the keyword RIGHT JOIN instructs SQL to produce different output. The query returns all records from machines, which is the second or right table. Only matching records are returned from employees, which is the right table.

Full Outer Joins

FULL OUTER JOIN returns all records from both tables. You can think of it as a way of completely merging two tables.

Continuous Learning in SQL 

>> Explore an example of something new you can add to your SQL toolbox: aggregate functions.

>> Focus on how to continue learning about aggregate functions and other SQL topics on your own.

Aggregate Functions

- In SQL, aggregate functions are functions that perform a calculation over multiple data points and return the result of the calculation. The actual data is not returned.
    

>> There are various aggregate functions that perform different calculations:

- COUNT returns a single number that represents the number of rows returned from your query.
    
- AVG returns a single number that represents the average of the numerical data in a column
    
- SUM returns a single number that represents the sum of the numerical data in a column
    

Aggregate Function Syntax

- To use an aggregate function, place the keyword for it after the SELECT keyword, and then in parenthesis, indicate the column you want to perform the calculation on.
    
- For example, when working with the customers table, you can use aggregate functions to summarize important information about the table. If you want to find out how many customers there are in total, you can use the COUNT function on any column, and SQL will return the total number of records, excluding NULL values. 
    

Continue Learning SQL

- SQL is one of the most important tools for working with databases and analyzing data, so you’ll find a lot of support in trying to learn SQL online. First, try searching for the concepts you’ve already learned and practiced to find resources that have accurate easy-to-follow explanations. When you identify these resources, you can use them to extend your knowledge.