---
up: "[[Programs]]"
tags:
  - "#education/computerprogramming/platforms/bootdev/linux/IO"
prev: "[[Packages]]"
---

# Man

The `man` command is short for "manual". It's a program that displays the manual of other programs.

![](https://i.imgur.com/JUzYAhI.png)

I know that manuals and documentation can feel inimidating, heck, that's why there are courses like this one to give you a gentler introduction. That said, manuals and documentation will become more useful to you as you become a more experienced developer. They're not as scary as they seem when you actually take the time to read them. 
## Using `man`

The `man` command will only work for programs that it has a manual for, but most built-in commands and Unix programs are supported. You just pass the name of the command as an argument. The most intuitive place to start, of course, is reading the manual's manual.

```bash
# open the man pages for the 'man' command
man man
```
## Searching

Most people don't just read the manual pages for fun. More often, the manual is used as a reference to quickly look up usage or special flags. 

You can search for text in the manual by pressing the `/` and typing your search, then pressing enter. Let's try to look up what the `-r` flag does for the `ls` command:

```bash
man ls
# type '/-r' to start searching

# press 'n' to jump to the next result

# press 'N' to go back if you went too far
```
## Assignment

As a systems person, the `grep` command will be your best friend. It has a lot of power, but it can be a little confusing to use.

1. Open the `grep` manual.
2. You'll notice that the manual is an interactive session. Page through the manual with the spacebar, and quit with `q`.

Read the first couple paragraphs of the `grep` manual and answer the question(s).
# Flags

As you've already seen in this course, some commands accept flags. Flags are options that you can pass to a command to change it's behavior. 

For example, the `ls` command can take a `-l` flag to show a "long" listing of files.

```bash
ls -l
```

Or the `-a` flag to show "all" files, including hidden files:

```bash
ls -a
```

You can also combine flags:

```bash
ls -al
```
## Conventions

Whether or not a command takes flags, and what those flags are, is up to the developer of the command. That said there are some common conventions:

- Single character flags are prefixed with a single dash (e.g. `-a`)
- Multi-character flags are prefixed with two dashes (e.g. `--help`)
- Sometimes the same flag can be used with a single dash or two dashes (e.g. `-h` or `--help`)
## Assignment

You've found that some files have been tampered with! To figure out which one it is, you need to know the number of bytes contained in each file.

1. [ ] Use the ["word count" command](https://www.ibm.com/docs/en/aix/7.3?topic=af-counting-words-lines-bytes-in-files-wc-command), `wc`, to count the number of bytes in the `worldbanc/public/pr_ideas.txt` file. Use the `man` command to figure out which flag you need to use.

Paste the number of bytes into the input field and submit your answer.
# Positional Arguments

