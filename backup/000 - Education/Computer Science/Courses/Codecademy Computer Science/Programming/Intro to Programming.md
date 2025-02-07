# Programming with Python on your Computer

The goal of this unit is to learn how to set up your own development environment on your computer. Doing so will set you up to successfully start writing your own programs and sharing them with the world.

After this unit, we will be able to:

- Write and run Python programs using the command line.
- Add and commit files to a git repository using the command line.

# Command Line Interface Setup

Navigate your system like a professional programmer.

### Setting up your Command Line

> The command line is a powerful tool used by developers to find, create and manipulate files and folders. 

**Command Line Interfaces (CLIs)** come in many forms. The CLI we'll use is called Bash.

### What is Bash?

**Bash**, or the B__ourne-A__gain SH__ell, is a CLI that was created in 1989 by Brian Fox as a free software replacement for the Bourne Shell. 

A **Shell** is a specific kind of CLI. Bash is open-source, which means that anyone can read the code and suggest changes. Since it's beginning, it has been supported by a large community of engineers who have worked to make it an incredible tool. 

### Navigation

The first command we're going to look at is `ls`. A *command* is a directive to the computer to perform a specific task. When you type `ls`, the command line looks at the directory you are in, then "lists" all the files and directories inside of it.

`pwd` is used to *"print working directory*" meaning the directory we are currently working in.

`cd` is our next command, which stands for *change directory*. Just as you would click on a folder in Windows Explorer or Finder, `cd` switches you into the directory you specify.

> When a file, directory or program is passed into a command, it is called an ***argument***. 
> 	The `cd` command takes a directory name as an argument and switches into that directory.

The argument `..` stands for the directory above the current working directory.

To move across multiple directories with a single command, we can provide `cd` a relative path to the `memory/` directory as an argument.

```bash
$ cd 2015/jan/memory
```

We can also move up multiple directories using the `..` argument. To go from **memory** up 2 directories to `2015`, we use `../..`

- The relative path `../..` can be read: the directory above and the directory above that

We can also move to an adjacent directory using `..` and the a directory name. (`../home/2014`)

##### mkdir 

The `mkdir` command stands for "make directory". It takes in a directory name as an argument and then creates a *new directory in the current working directory*. 

Here we use `mkdir` to create a new directory named **media/** inside our working directory.

##### touch

`touch` is used to create files.

`touch` creates a new file inside the working directory. It takes a filename as an argument and then creates an empty file with that name in the current working directory.

##### Helper Commands

> Now that we've covered the basics of navigating your filesystem from the command line, let's look at some helpful commands that will make using it easier.

- `tab` can be used to autocomplete your command. 
- The `up` and `down` arrows can be used to cycle through your previous commands. 
- `clear` is used to clear your terminal, which is useful when it's full of previous commands and outputs.




