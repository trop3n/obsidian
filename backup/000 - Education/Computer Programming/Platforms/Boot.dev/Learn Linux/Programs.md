---
up: "[[Permissions]]"
tags:
  - "#education/computerprogramming/platforms/bootdev/learnlinux/programs"
prev: "[[Input and Output]]"
---

# Compiled vs. Interpreted

A program is just a set of instructions that a computer can execute, and an "executable" is just a file that contains a program. The words "program" and "executable" are often used interchangeably. Broadly speaking, there are two types of programs:

- Compiled programs
- Interpreted programs
## Compiled Programs

A compiled program is a program that has been converted from human-readable source code into machine code (binary). [Machine code](https://en.wikipedia.org/wiki/Machine_code) is a set of instructions that a computer can execute directly: your computer's CPU is hardware that's been designed to execute machine code.

Programming languages like [Go](https://go.dev/), [C](https://en.wikipedia.org/wiki/C_(programming_language)), and [Rust](https://www.rust-lang.org/) produce compiled programs.
## Interpreted Programs

An interpreted program is a program that is executed by _another_ program. The program that executes the interpreted program is called an [interpreter](https://en.wikipedia.org/wiki/Interpreter_%28computing%29). The interpreter reads the source code of the interpreted program and executes it.

Programming languages like [Python](https://www.python.org/), [Ruby](https://www.ruby-lang.org/en/), and [JavaScript](https://en.wikipedia.org/wiki/JavaScript), are typically interpreted as they run, which means your computer needs to have the interpreter installed to run the program.

Another example is the `.sh` shell script files we talked about. Those are interpreted by the shell program.
## Assignment

1. [ ] In your shell, run the following command:

```bash
which sh
```

The `which` command tells you the location of an installed command line program. In this case, we're asking for the location of the `sh` (shell) program. Mine is located at `/bin/sh`.

2. [ ] Take a look at the contents of that file:

```bash
cat /bin/sh
```

Keep in mind, your `sh` program is a compiled executable, probably written in C. That's why when you try to view its contents with `cat`, you see... what you see.

A file with a `.sh` extension on the other hand is a shell script. It's a text file that contains commands that will be interpreted and run by the `sh` program. They are both executable programs, but only one can be run without the help of another program.
# Shebang

As we talked about before, you can run any executable file by typing its file path into your shell. For example:

```
bin/genids.sh
```

That works out of the box for files that are *compiled executables*. But what about scripts that need to be interpreted by another program? The computer needs to be told what program to use to interpret the file.

A **shebang** is a special line at the top of a script that tells your shell which program to use to execute the file. 

The format of a shebang is:

```
#! interpreter [optional-arg]
```

For example, if your script is a Python script and you want to use Python3, your shebang might look like this:

```python
#!/usr/bin/python3
```

This tells the system to use that Python 3 interpreter located at `/usr/bin/python3` to run the script.
# Bourne Shell

As we talked about before:

- If you're using Ubuntu on WSL, you're probably running a [Bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell)) shell.
- If you're using macOS, you're probably running a [Zsh](https://en.wikipedia.org/wiki/Z_shell) shell.
- If you're running a raw Linux installation, I pray you already know what you're using.

To get hand-wavy about it, I want to explain the difference between the 3 shells you're likely to encounter:

- `sh`: The Bourne shell. This is the original Unix shell and is [POSIX-compliant](https://en.wikipedia.org/wiki/POSIX). It's very basic and doesn't have many quality-of-life features.
- `bash`: The Bourne Again shell. This is the most popular shell on Linux. It builds on `sh`, but also has a lot of extra features.
- `zsh`: The Z shell. This is the most popular shell on macOS. Like `bash`, it does what `sh` can do, but also has a lot of extra features.

Both `zsh` and `bash` are "sh-compatible" shells, meaning they can run `.sh` scripts, but they also have extra features that generally make them more pleasant to use. For your purposes, the differences between `zsh` and `bash` are not super significant. Everything we do in this course will work in both shells.
# Shell Configuration

Bash and Zsh both have configuration files that run automatically each time you start a new shell session. These files are used to set up your **shell environment**. They can be used to set up aliases, functions, and environment variables.

These files are located in your home directory `~` and are *hidden by default*. The `ls` command has an `-a` flag that will show hidden files.

```
ls -a
```

- If you're using Bash, `.bashrc` is probably the file you want to edit.
- If you're using Zsh, `.zshrc` is probably the file you want to edit or create if it doesn't exist yet. 
## Assignment

As part of your audit, you're trying to figure out what shell commands run automatically when a user logs in on the machine. You need to confirm which shell configuration file is being used. 

1. [ ] Edit the file you believe to be you shell configuration file. You can use the `nano` command to edit files in your terminal:

```
nano ~/.bashrc
```

2. [ ] Add the following line to the bottom:

```
echo "Hello from the shell!"
```

You can use `Ctrl+0` to save the file (confirm any prompts with enter), and then `Ctrl+X` to exit the editor. (There should be a list of commands at the bottom of the screen.)

3. [ ] Close your terminal and open a new one. If you see the message "Hello from the shell!", you've found the right file!
4. [ ] Edit `~/.bashrc` again to remove the line you added to the file so that you don't see that message every time you open a new shell.
# Environment Variables

We talked about how you can create and use local variables in your shell:

```bash
name="Jason"
echo $name
# Jason
```

There is another type of variable called an environment variable. They are available to *all* programs that you run in your shell. 

You can view all of the environment variables that are currently set in your shell with the `env` command. To set the variable in your shell, use the `export` command.

```bash
export NAME="Jason"
```

You can then use the variable in your shell, just as before:

```bash
echo $NAME
# Jason
```

The interesting part is that programs and scripts you run in you shell can *also* use that variable:

For example, we can create a file called `introduce.sh` with the following contents:

```bash
#!/bin/sh
echo "Hi I'm $NAME"
```

Then we run it:

```bash
chmod +x ./introduce.sh
./introduce.sh
# Jason
```
## Assignment

Take a look at the contents of the `warn.sh` script in the `worldbanc/private/bin` directory. It looks like it's supposed to print nicely formatted warning messages with worldbanc branding.

`export` the required environment variables:

- `WARN_MESSAGE`: "The auditor is here"
- `WARN_FROM_NAME`: "Your worst nightmare"

Run the script and paste its output into the input field and submit your answer.
# PATH

> *This is one of the most important lessons in this entire course.*

There are environment variables that are sort of built-in to your shell. By "built-in" We just mean that different programs and parts of your system know about them and use them. The `PATH` variable is one of those. 
## Why Do We Care about the `PATH`?

If it weren't for the `PATH`, you'd have to remember the filesystem path of every executable you wanted to run in your shell. Instead of just running `ls`, you'd have to run `/bin/ls` (or whatever the location of the `ls` executable is on your system.) That's not very convenient.

The `PATH` variable is a list of directories that your shell will look into when you try to run a command. If you type `ls`, your shell will look in each directory listed in your `PATH` variable for an executable called `ls`. If it finds one, it will just run it. If it doesn't, it will give you an error like "command not found".
## What's in the `PATH` variable?

Take a look at your current `PATH` variable"

```bash
echo $PATH
```

You should see a giant list of directories separated by colons (`:`). Each of those directories is a place where your shell will look for executables. For example, with a `PATH` like this:

```
/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
```

our shell will look for executables in the following directories:

- `/usr/local/bin`
- `/usr/bin`
- `/bin`
- `/usr/sbin`
- `/sbin`
## Assignment

As something of a security engineer yourself, you want to temporarily disable the `PATH` variable so that you can only run executables by using their full path. You know, just so you don't accidentally run something you don't mean to.

1. [x] Reset your `PATH` variable to an empty string: ✅ 2025-01-19

```bash
export PATH=""
```

_This will only affect your current shell session. If you open a new shell, it will have the default `PATH` variable again._

2. [x] Try running some simple commands like `ls`, `pwd`, `echo`, etc – some will no longer work, while others that do not rely on `PATH` will. ✅ 2025-01-19
# Change Your `PATH`

A common problem you'll run into in the future is that you install a new program on your machine, but when you try to run it from your terminal, you get an error like:

```bash
$ my-new-program
-bash: my-new-program: command not found
```

Nine times out of ten, it's because the program is installed in a directory that's not in your `PATH` variable. Oftentimes when you install a program using the CLI, it will print a message during the installation process that tells you where the command was installed. **Don't let your eyes glaze over when your terminal prints important messages!** Sometimes you just gotta `rtfm`.
## Assignment

1. [x] Restart your shell session to reset your `PATH` variable to its default. You can do that by closing your terminal window and opening a new one. ✅ 2025-01-24

The `worldbanc` directory that you downloaded has some executables that would be useful to have in your `PATH` so that you can run them from anywhere. 

2. [x] Add the `worldbanc/private/bin` directory to your `PATH` variable. You'll need to add the absolute path, not the relative path. You can get the absolute path by running `pwd` in the `worldbanc/private/bin` directory, or by using the `realpath` command. ✅ 2025-01-24

To add a directory to your `PATH` without overwriting all of the existing directories, use the `export` command and reference the existing `PATH` variable.

```bash
export PATH="$PATH:/path/to/new"
```

The `$PATH` part is a reference to the existing `PATH` variable. The `:` separates the existing directories from the new directory (`/path/to/new`) that you're adding.

3. [x] `cd` outside of the `worldbanc` directory entirely. In fact, go to your home directory. ✅ 2025-01-24
# PATH Config

In the last session, you changed your `PATH` variable for your current shell configuration. Trouble is, the next time you restart your shell, it will be reset to it's default value. You won't be able to use the `worldbanc.sh` CLI Tool from anywhere unless you change your `PATH` variable *permanently*.

The most common way to do this is to add the same `export` command that your used in the last lesson to your shell's configuration file. 
## Assignment

1. [x] Edit your `.zshrc` / `.bashrc` file (whatever your shell config file is) and add an `export` command to the end of the file that adds the `worldbanc/private/bin` directory to your `PATH` variable. ✅ 2025-01-24
2. [x] Restart your shell session. ✅ 2025-01-24
3. [x] Run the `worldbanc.sh` CLI tool again from your home directory and make sure it works. ✅ 2025-01-24


