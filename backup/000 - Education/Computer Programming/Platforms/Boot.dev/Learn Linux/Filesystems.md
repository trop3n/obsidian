---
up: "[[000 - Education/Computer Programming/Platforms/Boot.dev/Learn Linux/Welcome|Welcome]]"
tags:
  - "#education/computerprogramming/platforms/bootdev/learnlinux/filesystems"
prev: "[[Permissions]]"
---


All the data stored on your computer is organized into files and directories. Files and directories are organized into a tree like structure called a filesystem.

- Directories are the same as "folders" and are just containers that hold files and other directories
- Files are just a dump of raw binary data: 1's and 0's. They bytes in a file can represent anything: text, images, videos, etc.

The filesystem tree starts with a single directory called the root directory. The root directory contains files and directories, which can contain more files and directories, and so on. 

When you open your terminal, your **working directory** (the one you're in) is going to be...somewhere. Most commonly it is your "home" directory.
## Assignment

You've just remotely logged onto a suspicious employee's machine at WorldBanc. First, you need to determine where on their filesystem you are...

Run the "print working directory" command to see the filepath of your current working directory:

```
pwd
```
# Filepaths

The output of your `pwd` command is a *filepath*. A filepath is a string that describes the location of a file or directory on your computer. Yours should look something like this:

```
/Users/wagslane
```

The text might be different, but the structure should be the same. Let's break it down:

- The first slash (`/`) represents the *root directory.*  It's the tippy top of the filesystem tree.
- The next part (`Users`) is the name of the directory inside the root directory. 
- Finally, the last part (`wagslane`) is the name of a directory inside the `Users` directory. 

So this path represents a directory 2 levels down from the root directory:

```
root
  └── Users
        └── wagslane
```
## Assignment

Time to start digging for evidence. Copy/paste the command below and run it to download the `worldbanc` directory from GitHub. It contains files and directories that you'll need throughout this course. If prompted for a password, use the password for your machine's user account, or the one you used when setting up Ubuntu in WSL.

```bash
curl -L https://github.com/bootdotdev/worldbanc/archive/refs/heads/main.zip -o worldbanc.zip
unzip worldbanc.zip
rm worldbanc.zip
mv worldbanc-main worldbanc
sudo chown -R $(whoami) worldbanc
sudo chmod -R 755 worldbanc
```

We'll cover what these commands do later.  
Normally, don't run commands if you don't know what they do. If you run into an issue, see the **troubleshooting tips** below.

**You should now have a `worldbanc` directory in your current working directory. When learning terminal commands in this course, it's possible to make a mistake and ruin your version of the worldbanc repo. If that happens, just come back to this lesson and download `worldbanc` again.**

_Note: WSL users need make sure that the `worldbanc` directory is added to their Linux subsystem and not to the Windows filesystem_

Run the "list" command to see the contents of your current working directory:

```bash
ls
```

You should see a `worldbanc` directory listed.

Run the "change directory" command to move into the `worldbanc` directory:

```bash
cd worldbanc
```

Finally, use the `ls` command again to see the contents of the `worldbanc` directory. Paste the console output into the input field and submit your answer.

## Troubleshooting

If you're having issues with the download due to [`curl`](https://curl.se/docs/manpage.html) or [`unzip`](https://www.linux.org/docs/man1/unzip.html) not being installed on Ubuntu/WSL, you can install them with the following commands:

```bash
sudo apt install unzip
sudo apt install curl
```

Certain Windows versions may not let you paste into the Command Line. See [how to enable ctrl+shift+v](https://superuser.com/questions/1410026/how-to-enable-ctrl-shift-v-in-windows-subsystem-for-linux-wsl-command-pr).
# Parent Directories

We talked about how you can "change directory" to move *into* a directory. But how do you move back *out* of a directory? 

The answer is two dots: `..`

`..` is a special directory name that means the "parent directory". It's a shortcut that you can use to move up one level of the `worldbanc` directory, just type:

```
cd ..
```

Then run the `ls` command again, but pass in the name of the `worldbanc` directory as an argument to list its contents from the parent directory:

```
ls worldbanc
```
# Absolute vs. Relative Paths

We've mostly been dealing with relative filepaths which are just paths that take into account your current directory.

For example, let's say we have the following directory structure in our filesystem:

```
vehicles
├── cars
│   ├── fords
│   │   ├── mustang.txt
│   │   └── focus.txt
```

When inside the top-level `vehicles` directory, the relative path to the `mustang.txt` file is: 

```
cars/fords/mustang.txt
```

However, when we're inside the `cars` directory, the relative path to the `mustang.txt` file is just:

```
fords/mustang.txt
```

Or when inside the `fords` directory, just:

```
mustang.txt
```
## Absolute Paths

An absolute path is a path that starts at the root of the filesystem. On [Unix-like systems](https://en.wikipedia.org/wiki/Unix-like) (macOS, Linux, WSL), the root is denoted by a forward slash `/`. So, if the `vehicles` directory is in the filesystem root, the absolute path to the `mustang.txt` file is:

```
/vehicles/cars/fords/mustang.txt
```

So, when inside the `fords` directory, you can use either:

```
/vehicles/cars/fords/mustang.txt
```

or 

```
mustang.txt
```

to refer to the same file.
## Which should I use?

It depends.

Relative paths are easier to read and write, and as long as you're in the correct directory (or the directory you expect), they're easier to reason about.

Absolute paths are more explicit. They're useful when you're not sure what directory you're currently in. For example, maybe you're giving someone instructions on how to find a file on their computer. You can't be sure what directory they'll be in when they start following your instructions, so you'll need to use an absolute path.
# Files

You're probably familiar with the concept of files from using a GUI like Windows Explorer or Finder.

At their core, files are just blobs of data. The raw bytes in a file can represent anything: text, images, videos, etc.
## The `cat` Command

The `cat` command is used to view the contents of a file. It's short for "concatenate", which is a fancy way of saying "put things together". It can feel like a confusing name if you're using the `cat` command to view a single file, but it makes more sense when you're using it to view multiple files at once. 

```
# Print the contents of a file to the terminal
cat file1.txt
```

```
# Concatenate the contents of multiple files and print them to the terminal
cat file1.txt file2.txt
```
# Head and Tail

Sometimes you don't want to print *everything* in file. Files can be really big after all. 
## The Head Command

The head command prints the first `n` lines of a file, where `n` is usually a number you specify. 

```
head -n 10 file1.txt
```

If you don't specify a number, it will default to 10.
## The `tail` Command

The tail command prints the last `n` lines of a file, where `n` is a number you specify.

```
tail -n 10 file1.txt
```
### Assignment

Time to start investigating the finances. Use the `cd` command to get into the `worldbanc/private/transactions/` directory.

Run the `cat` command to view the contents of the `2023.csv` file. You'll notice that it's a _really_ long file. We don't want to print the whole thing.

1. [ ] Use the `head` command to print the _first_ 6 lines of the `2023.csv` file
2. [ ] Copy the lines into the input field – **do not submit yet**

_We are printing the first 6 lines because the first line in the file is the header, and we want to include that along with the first 5 transactions._

3. [ ] Use the `tail` command to print the _last_ 5 lines of the `2023.csv` file
4. [ ] Copy the lines into the input field

Submit the **combined first 6 and last 5 lines**, for a total of 11 lines.
# More and Less

The more and less commands let you view the contents of a file, one page (or line) at a time.

As the adage goes, `less` is `more`. 

In the context of these commands, `less` is *literally* more. The `less` command does everything that the `more` command does but also has more features. As a general rule, you should use `less` instead of `more`.

You would only use `more` if you're on a system that doesn't have `less` installed.
## Assignment

You found nothing suspicious in the first and last transactions of 2023, but you're not done yet! It's time to dig through the middle of the file as well.

1. Run `less` and pass in the path to the `2023.csv` file, located at the root in the `worldbanc/private/transactions` directory.

```bash
less 2023.csv
```

Notice that you're now in an interactive mode and you've lost your shell prompt! That's because `less` has taken over your terminal window.

2. Press "enter" a few times to scroll down a few lines, just to see how that works. Press "q" to exit the `less` program and return to your shell prompt.
    
3. Re-run the `less` command, but this time, pass in the `-N` flag to show line numbers:
    

```bash
less -N 2023.csv
```

You can use the spacebar to scroll down a page at a time, and you can go back up by pressing "b".

4. Find line 153. Copy and paste the contents of that line into the input field and submit it.

You can use "q" to exit `less` at any time.
# Touch

The [touch command](https://man7.org/linux/man-pages/man1/touch.1.html) is designed to update the access and modification timestamps of a file. By default, if the specified file does not exist, `touch` will create an empty file with the given filename. Because of this, you’ll often see this command used to quickly create new files.

```bash
touch new_file.txt
```

You can also create multiple files at once by listing them:

```bash
touch some_file.txt some_other_file.txt
```

`touch` can be very handy when writing scripts because it ensures certain files exist without altering existing ones, creating new files only if necessary.
## Assignment

You discovered a discrepancy with the credit card files, worldbanc is supposed to be keeping credit history records but they aren't there! Change into the `worldbanc/public/products/credit_cards` directory and create a new file named `credithistory.txt` so they can keep track of that information.

Use `ls` to verify that the file has been created successfully. Then paste the output of that command into the input field and submit it.
# Directories

As we mentioned before, a directory is just a location in the filesystem that can contain files and other directories. On some systems, directories are called "folders", but it's the same thing. 
## The `mkdir` Command

The "make directory" command creates a new directory inside the current directory. 

```
mkdir my_directory
```
## Assignment

During your digging, you find that a file appears to be out of place. Make sure you're in the `worldbanc/public/products/credit_cards` directory and run `ls` from there. You should see a file called "tbills.txt".

Treasury Bills (T-Bills) are a type of investment, not a credit card!

Go back to the `products` directory and create a new directory called "investments".

Once you've done that, from inside the `products` directory, run:

```bash
ls
```

Paste the output of that command into the input field and submit it.
# Move

The [move command](https://www.ibm.com/docs/en/aix/7.3?topic=files-moving-renaming-mv-command) moves a file or directory from one location to another. You can use it to rename a file or to move it to a different directory altogether. Your working directory can't be the directory you're moving.

Renaming a file:

```bash
mv some_file.txt some_other_name.txt
```

Moving a file from the current directory to another nested directory:

```bash
mv some_file.txt some_directory/some_file.txt
```

Moving a file from the current directory, to the parent directory:

```bash
mv some_file.txt ../some_file.txt
```

If you don't want to rename the file and you're just moving it to a different directory, you can omit the filename:

```bash
mv some_file.txt some_directory/
```
## Assignment

Move the `tbills.txt` file, which can be found at `worldbanc/public/products/credit_cards/tbills.txt`, into the new `worldbanc/public/products/investments` directory. Keep the filename the same.

Both the target and destination have to be valid paths from the current working directory. Use `pwd` to see where you are and adjust the source and destination paths accordingly. Use `ls` to verify that the file has been moved correctly. If you mess up the `mv` command, you'll need to figure out where you accidentally moved the file to, then move it from that location back to where it belongs.
### Solution

When using `move`, what is the correct syntax?

```
mv <source> <destination>
```
# Remove

The `remove` command deletes a file or empty directory. 

```
rm some_file.txt
```

You can optionally add a `-r` flag to tell the `rm` command to delete a directory and *all* of it's contents recursively. "Recursively" is just a fancy way of saying "do it again on all of the subdirectories and their contents".

```
rm -r some_directory
```
## Assignment

Change directories to the `worldbanc/private` directory using the `cd` command.

There's a big problem here! Use the `cat` command to view the contents of the `worldbanc/private/passwords/passwords.txt` file.

It looks like someone is storing passwords in plain text! Even on a private machine, this is a big security risk. Delete both the `passwords` directory and the `passwords.txt` file within it.

Once you've done that, list the contents of the "private" directory again to make sure that the file is gone. Paste the output of that command into the input field and submit it.
# Copy

The [copy command](https://www.ibm.com/docs/en/aix/7.3?topic=c-cp-command) does what you would (hopefully) expect: it copies a file from one location to another.

```bash
cp source_file.txt destination/
```

You can also copy a directory and all of its contents recursively by adding the `-R` flag:

```bash
cp -R my_dir new_dir
```
## Assignment

Take a look inside the `worldbanc/private/transactions/` directory. You should see a few files containing transactions from different years.

Next, look inside the `backups` directory inside of `transactions`. It looks like something is missing!

Copy the missing file from the `transactions` directory into the `backups` directory so there is a backup of all of the transactions.

Finally, `ls` the contents of the `backups` directory and paste the output into the input field and submit it.
# Home

In Unix-like operating systems, a user's home directory is the directory where their personal files are stored. It is also the directory that a user starts in when logging into the system. 

I recommend doing all of your development work in your home directory. For example, I like to create a workspace directory in my home directory, and all my projects live in sub directories there.
## Danger

Your home directory is where you want to spend most of your time. Many of the other directories on your machine are critical to the operating system or other programs. Be careful when working in other directories like `/bin`, `/etc`, `/var` etc.

You can mess up your system if you are not careful. 
## The `~` Alias

My home directory is located at `/Users/wagslane`. The `~` character is an **alias** for your home directory. So when I want to go home, I don't have to type out `cd /Users/wagslane`, we can just type:

```
cd ~
```
# Grep

You might be used to nice graphical interfaces that allow you to search for text in files, usually with `ctrl+f` or `cmd+f`. But what about when you're working on a terminal?

As it turns out, once you're used to it, searching for text in files on a CLI can be much faster than using a GUI.
## The grep command

The [grep command](https://www.digitalocean.com/community/tutorials/grep-command-in-linux-unix) allows you to search for text in files. It has a _ton_ of capability, and we'll only be scratching the surface of its true power.
### Basic usage

The most basic usage of `grep` is to search for a string in a file. For example, if we wanted to search for the word "hello" in the file `hello.txt`, we could run:

```bash
grep "hello" hello.txt
```

This will print out every line in `hello.txt` that contains the word "hello". It's a case-sensitive search, so it will not match "Hello" or "HELLO".
## Assignment

Applications often write their logs to files on disk. These logs can contain useful information about what the application is doing, and can also be used to debug problems. As a security auditor, you need to dig through these logs to find any evidence of suspicious activity.

Use the `grep` command to find any lines with the text "CRITICAL" (all caps) in the `worldbanc/private/logs/2024-01-10.log` file.

Paste the output of your `grep` command into the input field and submit it.

_Note: The tab key is your friend! If you start typing the name of a file or directory and then press tab, your shell will try to autocomplete the name for you. If there are multiple possible completions, it will show you a list of them. I rarely type out full file names, I type the first few characters and then press tab._
# Grep Multiple Files

You can also search multiple files at once. For example, if we wanted to search for the word "hello" in `hello.txt` and `hello2.txt`, we could run:

```bash
grep "hello" hello.txt hello2.txt
```
### Recursive search

You can also search an entire directory, including all subdirectories. For example, if we wanted to search for the word "hello" in the current directory and all subdirectories, we could run:

```bash
grep -r "hello" .
```

_The `.` is a special alias for the current directory._
## Assignment

Use the grep command to find _all_ the lines with the text "CRITICAL" (all caps) in the entire `worldbanc/private/logs` directory.

Paste the output of your `grep` command into the input field and submit it.
# Find

The `find` command is a powerful tool for finding files and directories by name, not by their contents.

## Find a File by Name

Let's say you're looking for a file named `hello.txt` somewhere in your home directory. You can use the `find` command to search for exactly that title:

```bash
find some_directory -name hello.txt
```
## Pattern Search

The `find` command can also search for files that match a pattern. For example, if you wanted to find all files that end in `.txt`, you could run:

```bash
find some_directory -name "*.txt"
```

The `*` character is a wildcard that matches anything. If you're trying to find filenames that _contain_ a specific word, you can use the `*` character to match the rest of the filename:

```bash
# Find all filenames that contain the word "chad"
find some_directory -name "*chad*"
```

## Assignment

You've been tipped off that fraudulent activity seems to happen often with "joint" accounts. "joint" means accounts that have more than one owner.

Use the `find` command to search the `worldbanc/public/products` directory for all files that contain the word "joint" in their name.

Paste the output of your `find` command into the input field and submit it.