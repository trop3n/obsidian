### The Scanning Phase

> In the cybersecurity industry, it is common practice for an organization to hire a team of authorized cybersecurity professionals skilled in penetration testing and other offensive tactics. These professionals use common intrusion and ethical hacking tactics to engage the organization's defenses. 

The process they use to compromise a target system is called **The Hacking Process**. 

**The Hacking Process** consists of *reconaissance*, *scanning*, *enumeration*, *system hacking*, *escalation of privilege*, *planting backdoors* and *covering tracks*

### What is Nmap?

> Network Mapper, is a port scanner/network mapping tool. It is the most used scanning tool by ethical and unethical hackers. Nmap is an open-source command-line tool designed to run on the Linux operating system. 

The tool is designed to scan systems/networks for IP addresses, system ports, OS details and applications/services installed.

**Nmap** was released in 1997 as a Linux OS port scanning tool. Since then, the open-source development of Nmap has added many new features! Development of the tool continues today, and new capabilities are continuously added to Nmap. Soon, Nmap will have new capabilities that allow scanning of websites directly, and allow scanning systems and networks across the internet.

### Why Use Nmap?

> Nmap can perform highly sophisticated mapping functions that go undetected by **IDS/IPS**, but it can also perform simple network commands. Additionally, Nmap offers complex scripting capabilities through its Nmap Scripting Engine (NSE). Some of the most beneficial features of Nmap include:

- Ability to identify specific services running on systems such as: *DNS, web, email, SSH, etc.*
- The ability to gather OS-specific details of the target system
- The Zenmap's Graphical User Interface (GUI) helps build visualizations of the scan results of the target network/systems
- The ability to identify and distinguish between different networked devices such as: *routers, servers, switches, mobile devices, etc.*
- The NSE. It allows for complex and sophisticated automated scanning that exponentially increases Nmap's power. The NSE uses the Lua language for scripting.
- Access to reusable attack scripts from the NSE repository

### How to Use Nmap?

**Scenario**: A penetration tester is targeting an organization’s network to identify systems that may present vulnerabilities. Before scanning individual systems, the tester would like to sweep the network to identify all active devices on the network. To perform this “ping sweep” the penetration tester performs the following command in Nmap:

```
$ nmap -sP 192.168.0.0
```

This command will scan all IP addresses in the `192.168.0.0` network. The results of the command will list each IP address that is “up” or active on the network sweeped, as well as the system’s MAC address.

Once the penetration tester has the list of active systems on the network, a more targeted scanning approach may be executed on each system.
# Introduction to Linux

### Open Source Software

> Open-source software is software with source code that anyone can look at or contribute to and distribute based on the terms of the license. 

It grew out of the *free software movement* which guarantees certain freedoms to software users. 

These two movements overlap significantly and the terms are often used interchaneably, but they are respectfully defined by the non-profit organizations, **Open-Source Initiative** and the **Free Software Foundation**.

The Free Software Foundation first published the GNU Public License (GPL) in 1989. The GPL is a copyleft (as opposed to copyright) license, which means that any derivative software must be distributed under the same or equivalent license terms.

### OS vs. Linux Kernel vs. Shell

> The *kernel* is the most important part of the OS. It performs a variety of tasks:

- Process management
- Managing hardware devices
- Task scheduling

> The kernel controls all the major functions of the hardware, whether it's a phone, laptop, or *server.*

When we talked about Linus Torvalds and what he published in 1991, it was the Linux kernel.

Most Linux distributions utilize the command line extensively, using the *bash command language*

### What is a Linux Distribution?

> A Linux distribution is made from a software collection including the Linux kernel, GNU tools and default software.

Here are a short list of the most popular distributions:

- *Debian*: one of the oldest distros, first developed in 1993. It is a stable Linux OS, and software updates are frequent but small.
- *Ubuntu*: The most popular distro based on Debian Linux. It's widely used and supported and looks most like other operating systems like OSX and Windows in terms of usability.
- *Mint*: a distribution that is based of Ubuntu that comes with less pre-installed software than Ubuntu.
- *Red Hat Enterprise Linux*: also known as RHEL, is a distribution developed by Red Hat. It has strict rules around its trademark which prevents free distribution, but it mostly used in enterprise environments or servers.
- *Fedora*: open-source and community driven distro that is backed by Red Hat. Think of it as the Ubuntu equivalent to Red Hat.
- *Arch Linux*: Is a rolling release distribution of Linux that is 100% developed by its community. It has a steeper learning curve but is a great lightweight distribution of Linux. 
# Manipulation

> The `ls` command lists all files and directories in the working directory.

We can use `ls` as is or attach an *option*. Options modify the behavior of commands.

For example: 

```bash
ls -a
```

> The command above displays the contents of the working directory in more detail.
> 
> This command displays all the files and directories, including those starting with a dot (`.`). Files starting with a dot are normally hidden, and don't appear when using `ls` alone.

The `-a` is called an *option*. Options modify the behavior of commands.

In additional to `-a`, the `ls` command has several more options.

Here are three common ones:

- `-a` lists all contents, including hidden files and directories
- `-l` lists all contents of a directory in long format, as well as with file permissions
- `-t` orders files and directories by the time they were last modified
### `ls` and Combining Options

```bash
$ ls -l
drwxr-xr-x 5  cc  eng  4096 Jun 24 16:51  actiond
rwxr-xr-x 4  cc  eng  4096 Jun 24 16:51  comedy
drwxr-xr-x 6  cc  eng  4096 Jun 24 16:51  drama
-rw-r--r-- 1  cc  eng     0 Jun 24 16:51  genres.txt
```

> The `-l` option lists files and directories as a *table*. Here there are four rows, with seven columns separated by spaces. Here's what each column means:

1. Access Rights. These indicate the read, write and execute permissions on the file or directory allowed to the owner, the group, and all users. 
2. Number of hard links. This represents the number of hard links to the file or directory. This number includes the parent directory link (`..`) and current directory link (`.`).
3. The username of the file's owner. Here the username is `cc`.
4. The name of the group that owns the file. Here the group nam is `eng`.
5. The size of the file in bytes.
6. The date and time that the file was last modified.
7. The name of the file or directory.

> In addition to using each option separately, like `ls -a` or `ls -l`, multiple options can be used together, like `ls - alt`.

We can group letter options for other commands in the same way.

`ls -alt` lists all contents, including hidden files and directories, in long format, ordered by the date and time they were last modified.
### `cat`

> How do we view the contents of an individual file in our terminal? We can use `cat`.

The `cat` command outputs the contents of a specified file. For example, running the following inside the **movies/** directory.

```bash
cat genres.txt
```

^^ Will output all the text from genres.txt

This is a useful command for peeking at files without opening them, and confirming the result of other commands that change the contents of files.

We can also get output using paths to a specified file. To output the contents of `batman.txt` within the action directory, we can run:

```bash
cat action/batman.txt
```

This will output the contents of `batman.txt` within the `action/` directory.
# `cp` Part 1

> Let's move on to copying, moving and removing files and directories from the command line. 

The `cp` command copies files or directories. Below, we copy the contents of a source file into a destination file:

```bash
cap source.txt destination.txt
```

For example, if we are in the `scifi/` directory and want to make a backup of `terminator.txt` file we would run:

```
cp terminator.txt terminator.bak
```

> This will make a copy of `terminator.txt` and save it as `terminator.bak`.

**Note**: The `.bak` file extension is commonly used to notate a file as a backup of a file with the same name.

We could also a file to a destination directory:

```
cp source.txt directory
```

If we are in the `comedy/` directory and wanted to put a copy of the `the-office.txt` in the `slapstick/` directory we would run:

```
cp the-office.txt slapstick
```

The above example will put an exact copy named `the-office.txt` in the `slapstick/` directory.

If we wanted to rename the file as well, we would include the name in the path of the second argument.
# `cp` Part II

