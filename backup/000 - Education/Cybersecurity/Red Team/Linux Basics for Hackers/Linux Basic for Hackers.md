---
up: "[[000 - Education/Cybersecurity/Red Team/Red Team|Red Team]]"
source: "[[Linux Basics for Hackers- NSP.pdf]]"
tags:
  - "#education/books/cybersecurity/redteam/linuxbasicsforhackers"
---

# Introduction

Hacking is the most important skill set of the 21st century. Events in recent years seem to reaffirm this statement with every morning's headline. Nations are spying on each other to gain secrets, cyber criminals are stealing billions of dollars, adversaries are influencing each other's elections, and combatants are taking down each other's utilities.

These are all the work of hackers, and their influence over our increasingly digital world is just beginning to be felt. 

I decided to write this book after working with tens of thousands of aspiring hackers through Null-Byte, https://www.hackers-arise.com/, and nearly every branch of the US military and intelligence agencies (NSA, DIA, CIA, and FBI). These experiences have taught me that many aspiring hackers have had little or no experience with Linux, and this lack of experience is the primary barrier to their starting the journey to becoming professional hackers. Almost all the best hacker tools are written in Linux, so some basic Linux skills are a prerequisite to becoming a professional hacker. I have written this book to help aspiring hackers get over this barrier.

Hacking is an elite profession within the IT field. As such, it requires an extensive and detailed understanding of IT concepts and technologies. At the most fundamental level, Linux is a requirement. 

- One should invest a lot of time learning and using it in order to pursue a career in the information security field.

This book is intended for those who wish to get involved on the exciting path of hacking, cybersecurity and pentesting. It is also treated as a starting point in Linux and hacking overall. 

In this introduction, we’ll look at the growth of ethical hacking for infor- mation security, and I’ll take you through the process of installing a virtual machine so you can install Kali Linux on your system without disturbing the operating system you are already running.
## What is Ethical Hacking?

With the growth of the information security field in recent years has come dramatic growth in the field of ethical hacking, also know as *white hat* hacking. Ethical hacking is the practice of attempting to infiltrate and exploit a system in order to find out its weaknesses and better secure it. I segment the field of ethical hacking into two primary components: penetration testing for a legitimate information security firm and working for your nation's military or intelligence agencies. Both are rapidly growing areas, and demand is strong.
### Penetration Testing

As organizations become increasingly security conscious and the cost of security breaches rises exponentially, many large organizations are beginning to contract out security services. One of these key security services is penetration testing. A *penetration test* is essentially a legal, commissioned hack to demonstrate the vulnerability of a firm's networks or systems.

Generally, organizations conduct a vulnerability assessment first to find potential vulnerabilities in their network, operating systems, and services. I emphasize *potential*, as this vulnerability scan includes a significant number of false positives. It is the role of a penetration tester to attempt to hack, or **penetrate**, these vulnerabilities. 
### Military and Espionage

Nearly every nation on earth now engages in cyber espionage and cyber-warfare. Only one needs to scan the headlines to see that cyber activities are the chosen method for spying on and attacking military and industrial systems. 

Hacking plays a crucial part in these military and intelligence-gathering activities, and that will only be more true as time goes by. Imagine a war of the future where hackers gain access to their adversary's war plans and knock out their electrical grid, oil refineries, and water systems. These activities are taking place every day now. 
## Why Hackers use Linux

Why do hackers use Linux? Mostly because it offers a far higher level of control via a few different methods. 
### Linux is Open Source

Unlike Windows, Linux is open source, meaning that the source code of the operating system is available to you. As such, you can change and manipulate it as you please. If you are trying to make a system operate in ways it was not intended to, being able to manipulate the source code is essential. 
### Linux is Transparent

To hack effectively, you must know and understand your operating system, to a large extent, the operating system you are attacking. Linux is totally transparent, meaning we can see and manipulate all its working parts. 

Not so with Windows. Microsoft tries hard to make it as difficult as possible to know the inner working of its operating system, so you can never really know what's going on under the hood. 
### Linux Offers Granular Control

Linux is granular. That means that you have an almost infinite amount of control over the system. In Windows, you can control only what Microsoft allows you to control. In Linux, everything can be controlled by the terminal, at the most minuscule level or the most macro level. In addition, Linux makes scripting in any of the scripting languages simple and effective. 
### Most Hacking Tools are Written for Linux

Well over 90 percent of all hacking tools are written for Linux. There are exceptions, of course, such as Cain and Abel and Wikto, but those exceptions prove the rule. Even when hacking tools such as Metasploit or nmap are ported for Windows, not all the capabilities transfer from Linux.
### The Future Belongs to Linux/Unix

This might seem like a radical statement, but I firmly believe that the future of information technology belongs to Linux and Unix systems. Microsoft had it's day in the 1980s and 1990s, but its growth is slowing and stagnating. 

Since the internet began, Linux/Unix has been the operating system of choice for web servers due to its stability, reliability and robustness. Even today, Linux/Unix is used in two-thirds of web servers and dominates the market. Embedded systems in routers, switches, and other devices almost always use the Linux kernel, and the world of virtualization is dominated by Linux, with both VMware and Citrix built on the Linux kernel. 

Over 80 percent of mobile devices run Unix or Linux (iOS is Unix, and Android is Linux), so if you believe that the future of computing lies in mobile devices such as tablets and phones (it would be hard to argue otherwise), then the future is Unix/Linux. Microsoft Windows manages just 7 percent of the mobile devices market. Is that the wagon you want to be hitched to?
# 1. Getting Started with the Basics

By our very nature, hackers are doers. We want to touch and play with things. Few of us want to read long tomes of information technology theory before we can do what we love most. With that in mind, this chapter is designed to give you some fundamental skills to get up and running in Kali. 
## Introductory Terms and Concepts

**Binaries**: This term refers to files that can be executed, similar to executables in Windows. Binaries generally reside in the `/usr/bin` or `/usr/sbin` directory and include utilities such as `ps`, `cat`, `ls` and `ifconfig` (we'll touch on all four of these in this chapter) as well as applications such as the wireless hacking tool **aircrack-ng** and the intrusion detection system Snort.

**Case Sensitivity**: Unlike Windows, the Linux filesystem is case sensitive. This means that `Desktop` is different from `desktop`, which is different from `DeskTop`. Each of these would represent a different file or directory name. 

**Directory**: This is the same as a folder in Windows. A directory provides a way of organizing files, usually in a hierarchical manner. 

**Home**: Each user has their own `/home` directory, and this is generally where files you create will be saved by default.

**Kali**: Kali Linux is a distribution of Linux specifically designed for penetration testing. It has hundreds of tools preinstalled, saving you the hours it would take to download and install them yourself. I will be using the latest version of Kali available. 

**root**: Like nearly every operating system, Linux has an administrator or superuser account, designed for use by a trusted person who can do nearly anything on the system. This would include things such as reconfiguring the system, adding users, and changing passwords. In Linux, that account is called **root**. As a hacker or pentester, you will often use the root account to give yourself control over the system. In fact, many hacker tools require that you use the root account.

**Script**: This is a series of commands run in an interpretive environment that converts each line to source code. Many hacking tools are simply scripts. Scripts that can be run with the bash interpreter or any of the other scripting language interpreters, such as Python, Perl, or Ruby. Python is currently the most popular programming interpreter among hackers.

**Shell**: This is an environment and interpreter for running commands in Linux. The most widely used shell is bash, which stands for *Bourne-Again Shell*, but other popular shells include the C shell and Z shell. 

**Terminal**: This is a command line interface (CLI).
## The Linux Filesystem

The Linux filesystem structure is somewhat different from that of Windows. Linux doesn't have a physical drive (such as the C: drive) at the base of the filesystem but uses a **logical filesystem** instead. At the very top of the filesystem structure is `/`, which is often referred to as the *root* of the filesystem, as if it were a upside down tree. Keep in mind that this is *different from the root user*.

These terms may seem confusing at first, but they will become easier to differentiate once you get used to Linux.

![](https://i.imgur.com/KYGhb7m.png)
	The root (/) of the filesystem is at the top of the tree, and the following are the most important directories to know:
	- `/root`: The home directory of the all powerful root user
	- `/etc`: Generally contains the Linux configuration files, -- the files that control when and how programs start up
	- `/home`: the user's home directory
	- `/mnt`: where other filesystems are attached or mounted to the filesystem
	- `/media`: where CDs and USB devices are usually attached or mounted to the filesystem
	- `/bin`: Where application *binaries* reside
	- `/lib`: Where you'll find *libraries* (shared programs that are similar to Windows DLLs)

It's also important to note that you should not log in as root when performing routine tasks, because anyone who hacks your system (yes, hackers get hacked) when you're logged in as root would immediately gain root privileges and thus "own" your system. 
## Basic Commands in Linux

Let's begin with some basic command that will help us get up and running. 
### Finding Yourself with `pwd`

Unlike when working in a GUI environment, the command line in Linux does not always make it apparent what directory you're currently in. The `pwd` command (Print Working Directory) returns your location in the directory structure.
### Checking Your Login with `whoami`

In Linux, the one "all-powerful" superuser sysadmin is named root, and it has all the system privileges needs to add users, change passwords, change privileges, and so on. Obviously, you don't want just anyone to have the ability to make such changes; you want someone who can be trusted and has proper knowledge of the operating system. As a hacker, you usually need to have all those privileges to run the programs and commands you need (many hacker tools won't work without root privileges).
### Navigating the Filesystem

This is an **essential Linux skill**. To get anything done, you'll need to be able to move around the filesystem. 
#### Changing Directories with `cd`

To change directories from the terminal, use the `cd` command (change directory) followed by the file path of the directory you want to move to (`/etc`, for example).

To move up one level in the file structure (toward the root of the file structure, or /), we use `cd` followed by double dots (..) as shown here:

```
kali:/etc >cd .. 
kali >pwd 
/ 
kali >
```

This moves us up one level from `/etc` to the `/` root directory, but you can move up as many levels as you need. Just use the same number of double dot pairs as the number of levels you want to move:

- You would use `..` to move up one level
- Use `../..` to move up two levels
- Use `../../..` to move up three levels, and so on.

You can also use `cd /` to move directory to the root directory from anywhere. 
#### Listing the Contents of a Directory with `ls`

To see the contents of a directory (the files and subdirectories), we can use the `ls` command (list).

This command is very similar to the `dir` command in Windows.

This command lists both the files and directories contained in the directory. You can also use this command on any particular directory, not just the one you are currently in, by listing the directory name after the command; for example, `ls /etc` shows what's in the `/etc` directory.

To get more information about the files and directories, such as their permissions, owner, size and when they were last modified, you can add the `-l` switch after `ls` (the `l` stands for `long`). This is often referred to as `long listing`. 

As you can see, `ls -l` provides us with significantly more information, such as whether an object is a file or directory, the number of links, the owner, the group, its size, when it was created or modified, and its name. I typically add the `-l` switch whenever doing a listing in Linux, but to each their own. We’ll talk more about ls `-l` in Chapter 5. Some files in Linux are hidden and won’t be revealed by a simple ls or ls -l command. To show hidden files, add a lowercase `–a` switch, like so:

```
kali >ls -la
```

If you aren't seeing a file you expect to see, it's worth trying `ls` with the `a` flag. 
### Getting Help

Nearly every command, application or utility has a dedicated help file in Linux that provides guidance for its use. For instance, if I needed help using the best wireless cracking tool, `aircrack-ng`, I could simply tpye the `aircrack-ng` command followed by the `--help`  command.

```
kali >aircrack-ng --help
```

Note the **double dash** here. The convention in Linux is to use a double dash (`--`) before word options, such as `help`, and a single dash (`-`) before single-letter options, such as `-h`. 

When you enter this command, you should see a short description of the tool and guidance on how to use it. In some cases, you can either use `-h` or `-?` to get to the help file.

```
kali >nmap -h
```
### Referencing Manual Pages with `man`

In addition to the help switch, most commands and applications have a manual (man) page with more information, such as a description and synopsis of the command or application. You can view a man page by simply typing `man` before the command, utility or application. 

```
kali >man aircrack-ng
```

This opens the manual for `aircrack-ng`, providing us with more detailed information that the `help` screen. You can scroll through this manual file using the `ENTER` key, or you can page up and down using the `PG DN` and `PG UP` keys, respectively; you can also use the arrow keys. To exit, simply enter `q` (for quit), and you'll return to the command prompt.
## Finding Stuff

Until you become familiar with Linux, it can be frustrating to find your way around, but knowledge of a few basic commands and techniques will go a long way toward making the command line much friendlier. The following commands help you locate things from the terminal. 
### Searching with `locate`

Probably the easiest command to use is `locate`. Followed by a keyword denoting *what it is* you want to find, this command will go through your entire filesystem and locate every occurrence of that word. 

```
kali >locate aircrack-ng
/usr/bin/aircrack-ng
/usr/share/applications/kali-aircrack-ng.desktop
/usr/share/desktop-directories/05-1-01-aircrack-ng.directory
```

The `locate` command is not perfect, however. Sometimes the results of `locate` can be overwhelming, giving too much info. Also, `locate` uses a database that is usually only updated once a day, so if you just created a file and need to find it, it might not appear in the list until the next day.
### Finding Binaries with `whereis`

If you're looking for a binary file, you can use the `whereis` command to locate it. This command returns not only the location of the binary but also it's source and man page if they are available.

```
jason@arch~>whereis aircrack-ng
aircarck-ng: /usr/bin/aircarck-ng /usr/share/man/man1/aircarck-ng.1.gz
```

In this case, `whereis` returned just the aircrack-ng binaries and man page, rather than every occurrence of the word *aircrack-ng*. Much more efficient and illuminating.
### Finding Binaries in the PATH Variable with `which`

The `which` command is even more specific: it only returns the location of the binaries in the `PATH` variable in Linux. `PATH` holds the directories in which the operating system looks for the command you execute at the command line.
	For example, when I enter `aircrack-ng` on the command line, the operating system looks to the `PATH` variable to see in which directories it should look for aircrack-ng.

```
jason@arch~>which aircrack-ng
/usr/bin/aircrack-ng
```

Here, `which` is available to find a single binary file in the directories listed in the `PATH` variable. At minimum, these directories usually include `/usr/bin`, but may include `/usr/sbin` and maybe a few others. 
### Performing More Powerful Searches with `find`

The `find` command is the most powerful and flexible of the searching utilities. It is capable of beginning your search with any designated directory and looking for a number of different parameters, including, of course, the file-name but also the data of creation or modification, the owner, the group, permissions and the size. 

Here's the basic syntax for `find`:

```
find directory options expression
```

So, if I wanted to search for a file with the name *apache2*, starting in the root directory, I would enter the following:

```
jason@arch~>find / -type f -name apache2
```

1. First, we state the directory in which to start the search `/ for root`. 
2. Then, we specify which type of file to search for, in this case `f` for an ordinary file.
3. Last, we give the name of the file we're searching for, in this case `apache2`.

The results are shown here:

```
kali >find / -type f -name apache2 
/usr/lib/apache2/mpm-itk/apache2 
/usr/lib/apache2/mpm-event/apache2 
/usr/lib/apache2/mpm-worker/apache2 
/usr/lib/apache2/mpm-prefork/apache2 
/etc/cron.daily/apache2 
/etc/logrotate.d/apache2 
/etc/init.d/apache2 
/etc/default/apache2
```

The `find` command started at the top of the filesystem, (`/`), went through every directory looking for `apache2` in the filename, and then listed all instances found. 

This can be quite slow if searching through *every directory*. One way to speed it up is to look only in the directory where you would expect to find the file(s) you need. In this case, we are looking for a configuration file, so we could start the search in the `/etc` directory, and Linux would only search as far as its subdirectories. 

```
kali >find /etc -type f -name apache2 
/etc/init.d/apache2 
/etc/logrotate.d/apache2 
/etc/cron.daily/apache2 
/etc/default/apache2
```

This is much quicker search only found occurrences of apache2 in the `/etc` directory and its subdirectories. It's also important to note that unlike some other search commands, `find` displays only `exact` name matches. 

If the file `apache2` has an extension, such as `apache2.conf`, the search will **not** find a match. We can remedy this limitation by using `wildcards`, which enable us to match multiple characters. Wildcards come in a few different forms: `* . , ?` and `[]`.

Let's look in the `/etc` directory for all files that begin with `apache2` and have any extension. For this, we could write a `find` command using the following wildcard:

```
jason@arch~>find /etc -type f -name apache2.\*
/etc/apache2/apache2.conf
```

When we run this command, we find that there is one file in the `/etc` directory that fits the `apache2.*` pattern. When we use a period followed by the `*` wildcard, the terminal looks for any extension after the filename `apache2`. This can be a very useful technique for finding files where you don't know the file extension. 

> [!NOTE] A Quick Look at Wildcards
> Let's say we're doing a search on a directory that has the files `cat`, `hat`, `what` and `bat`. The `?` wildcard is used to represent a single character, so a search for `?at` would find `hat`, `cat`, and `bat` but not `what`, because *at* in this filename is preceded by two letters. The `[]` wildcard is used to match the characters that appear inside the square brackets. For example, a search for `[c,b]at` would match `cat` and `bat` but not `hat` or `what`. Among the most widely used wildcards is the asterisk (`*`) which matches any characters of any length, from none to an unlimited number of characters. A search for `*at`, for example, would find `cat`, `hat`, `what` and `bat`.
### Filtering with `grep`

Very often when using the command line, you'll want to search for a particular keyword. For this, you can use the `grep` command as a filter to search for keywords. 

The `grep` command is often used when output is piped from one command to another. I cover piping in Chapter 2, but for now, suffice it to say that Linux (and Windows for that matter) allows us to take the *output* of one command and send it as an *input* to another command. This is called ***piping***, and we use the `|` command to do it (the `|` key is usually above the ENTER key on your keyboard).

The `ps` command is used to display information about processes running on the machine. We cover this in more detail in Chapter 6, but for this example, suppose I want to see all the processes running on my Linux system. In this case, I can use the `ps` (processes) command followed by the `aux` switches to specify which process information to display, like so:

```
jason@arch~>ps aux
```

This provides me with a listing of *all* the processes running in this system -- but what if I just want to find one process to see if it's running? We can do this by piping the output from `ps` to `grep` and searching for a keyword. 

```sh
kali >ps aux | grep apache2 
root 4851 0.2 0.7 37548 7668 ? Ss 10:14 0:00 /usr/sbin/apache2 -k start 
root 4906 0.0 0.4 37572 4228 ? S 10:14 0:00 /usr/sbin/apache2 -k start 
root 4910 0.0 0.4 37572 4228 ? Ss 10:14 0:00 /usr/sbin/apache2 -k start 
--snip--
```

This command tells Linux to display all my services and send that output to `grep`, which will look through the output for the keyword `apache2` and then display only the *relevant output*, thus saving considerable time and eye strain.
## Modifying Files and Directories

Once you’ve found your files and directories, you’ll want to be able to per- form actions on them. In this section, we look at how to create files and directories, copy files, rename files, and delete files and directories
### Creating Files

There are many ways to create files in Linux, but for now we'll just look at two simple methods. The first is `cat`, which is short for *concatenate*, meaning to combine pieces together. The `cat` command is generally used for displaying the contents of a file, but it can also be used to create small files. For creating bigger files, it's better to enter the code in a text editor such as vim, emacs, leafpad, gedit, or kate and then save it as a file. 
#### Concatenation with `cat`

The `cat` command followed by a filename will display the contents of that file, but to create a file, we follow the `cat` command with *redirect*, denoted with the `>` symbol, and a name for the file we want to create. Here's an example:

```
jason@arch~>cat > hackingskills
Hacking is the most valuable skillset of the 21st century!
```

When you press `ENTER`, Linux will go into *interactive mode* and wait for you to start entering the content of the file. This can be puzzling because the *prompt disappears*, but if you simply begin typing, whatever you enter will go into the file. Here, we entered `Hacking is the most valuable skill of the 21st century!`. To exit and return to the prompt, press `CTRL+D`. Then, when I want to see what's in the file `hackingskills`, we enter the following:

```
jason@arch~>cat hackingskills
Hacking is the most valuable skill of the 21st century!
```

If you don't use the redirect symbol, Linux will spit back the contents of your file. 

To add, or *append*, more content to a file, you can use the `cat` command with a double redirect (`>>`), followed by whatever you want to add to the end of the file. Here's an example:

```
jason@arch~>cat >> hackingskills
Everyone should learn hacking
```

Linux once again goes into interactive mode, waiting for content to append to the file. When we enter `Everyone should learn hacking` and press `CTRL+D`, we are returned to the prompt. Now, when the files contents are displayed with `cat`, we can see that the file has been appended with `Everyone should learn hacking`.

If I want to *overwrite* the file with new information, I can simply use the `cat` command with a single redirect again, as follows:

```
kali >cat > hackingskills 
Everyone in IT security without hacking skills is in the dark 
kali >cat hackingskills 
Everyone in IT security without hacking skills is in the dark
```

As you can see here, Linux goes into interactive mode, and I enter the new text and then exit back to the prompt. When I once again use `cat` to see the content of the file, I see that my previous words have been overwritten with the latest text.
### File Creation with `touch`

The second command for file creation is `touch`. This command was originally developed so a user could simply `touch` a file to change some of its details, such as the date it was created or modified. However, if the file doesn't already exist, this command creates that file by default.

Let's create *newfile* with `touch`:

```
jason@arch~>touch newfile
```

Now when I then use `ls -l` to see the long list of the directory, I see that a new file has been created named *newfile*. Note that its size is `0` because there is no content in *newflie*.
### Creating a Directory

The command for creating a directory in Linux is `mkdir`, a contraction of *make directory*. To create a directory named *newdirectory*, enter the following command:

```
jason@arch~>mkdir newdirectory
```

To navigate to this newly created directory, simply enter this:

```
jason@arch~>cd newdirectory
```
### Copying a File

To copy files, we use the `cp` command. This creates a duplicate of the file in the new location and leaves the old one in place:

```
jason@arch~>touch oldfile
jason@arch~>cp oldfile /root/newdirectory/newfile
```

Renaming the file is optional and is done simply by adding the name you want to give it to the end of the directory path. If you don't rename the file when you copy it, the file will retain the original name by default. 

When we then navigate to *newdirectory*, we see that there is an exact copy of *oldfile* called *newfile*.

```
jason@arch~>cd newdirectory
jason@arch~>ls

newfile     oldfile
```
### Renaming a File

Unfortunately, Linux doesn't have a command intended solely for renaming a file, as Windows and some other operating systems do, but it does have the `mv` (move) command.

The `mv` command can be used to move a file or directory to a new location or simply to give an existing file a new name. To rename *newfile* to *newfile2*, you would enter the following:

```
jason@arch~>mv newfile newfile2
jason@arch~>ls
oldfile  newfile2
```

Now when you list (`ls`) that directory, you see *newfile2* and not *newfile*, because it has been renamed. You can do the same with directories.
### Removing a File

To remove a file, you can simply use the `rm` command, like so:

```
jason@arch~>rm newfile2
```

If you now do a long listing on the directory, you can confirm that the file has been removed.
### Removing a Directory

The command for removing a directory is similar to the `rm` command for removing files but with `dir` (for directory) appended, like so:

```
jason@arch~>rmdir newdirectory
rmdir:failed to remove 'newdirectory': Directory not empty
```

It's important to note that `rmdir` will not remove a directory that is not empty, but will give you a warning message that the "directory is not empty," as you can see in this example. You must first remove all the contents of the directory before removing it. This is to stop you from accidentally deleting objects you didn't intend to delete. 

If you do want to remove a directory and its content all in one go, you can use the `-r` switch after `rm`, like so:

```
jason@arch~>rm -r newdirectory
```

Just a word of caution, though: be wary of using the `-r` option with `rm`, at least at first, because it's very easy to remove valuable files and directories by mistake. Using `rm -r` in your home directory, for instance, would delete every file and directory there -- probably not what you were intending.
## Go Play Now!

Now that you have some basic skills for navigating around the filesystem, you can play with your Linux system a bit before progressing. The best way to become comfortable with using the terminal is to try out your newfound skills right now. In subsequent chapters, we will explore farther and deeper into our hacker playground.

> [!Exercise] Exercises
> 1. Use the `ls` command from the root (`/`) directory to explore the directory structure of Linux. Move to each of the directories with the `cd` command and run `pwd` to verify where you are in the directory structure.
> 2. Use the `whoami` command to verify which user you are logged in as.
> 3. Use the `locate` command to find wordlists that can be used for password cracking.
> 4. Use the `cat` command to create a new file and then append to that file. Keep in mind that `>` redirects input to a file and `>>` appends to a file.
> 5. Create a new directory called `hackerdirectory` and create a new file in that directory called `hackedfile`. Now copy that file to your `/root` directory and rename it `secretfile`.
# Chapter 2: Text Manipulation

In Linux, nearly everything you deal with directly is a file, and most often these will be text files; for instance, all configuration files in Linux are text files. So to reconfigure an application, you simply open the configuration file, change the text, save the file, and then restart the application -- your reconfiguration is complete. 

For illustrative purposes, I’ll use files from the world’s best network intrusion detection system (NIDS), Snort, which was first developed by Marty Roesch and is now owned by Cisco. NIDSs are commonly used to detect intrusions by hackers, so if you want to be a successful hacker, you must be familiar with the ways NIDSs can deter attacks and the ways you can abuse them to avoid detection.
## Viewing Files

