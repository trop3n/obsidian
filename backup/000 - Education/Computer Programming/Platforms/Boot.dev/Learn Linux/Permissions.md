---
up: "[[Filesystems]]"
tags:
  - "#education/computerprogramming/platforms/bootdev/learnlinux/permissions"
prev: "[[Programs]]"
---

# Users


[Unix-like](https://en.wikipedia.org/wiki/Unix-like) systems (like the one you're using) support multiple users. Each user has their own home directory, their own files, and their own permissions.

If you're like most people these days, you're the only user on your machine. It used to be more common for multiple people to share a single computer, or for multiple people to do their work on the same computer over a network.
## Sudo

The `sudo` keyword lets you run a command as a "superuser". It's short for ["superuser do"](https://www.linux.com/training-tutorials/linux-101-introduction-sudo/). To use it, you'll need a password with superuser privileges, which you should already have if you're the only user of your machine.

Some people are pedantic and pronounce `sudo` as "sue-doo". Others are correct and pronounce it "sue-dough".

> [!NOTE]
> Note: `sudo` grants unrestricted access and can risk system damage if you don't know what you're doing. All commands in this course are safe, but other commands should be reviewed before running with `sudo`.
## Assignment

1. Run the ["Who am I?" command](https://www.ibm.com/docs/en/zos/3.1.0?topic=wtsc-using-whoami-command) to see which user you're logged in as:

```bash
whoami
```

2. Run the same command as root:

```bash
sudo whoami
```

3. You'll be prompted for your password. Enter it. Copy and paste the _output_ of the command into the input box and submit your answer.
# Permissions

In a Unix-like operating system, permissions control who can do what to which files and directories. The permissions of an individual file or directory are visually represented as a 10-character string:

```
drwxrwxrwx
```
# Changing Permissions

The [chmod command](https://www.ibm.com/docs/en/aix/7.3?topic=c-chmod-command) lets you change the permissions of a file or directory. It's short for "change mode" (I wish it was called "change permissions", but alas).

## Assignment

As part of your security audit, you need to know who has access to the files in the `private` directory. The `ls` command has a `-l` option (lowercase "L") that will print out the permissions of each file and directory in long format.

1. List the files in the `worldbanc/private` directory along with their permissions using `ls -l` so you can see the current state of affairs.
2. Change the permissions of the `private` directory and all of its contents so that:
    - The owner can read, write, and execute
    - The group can do nothing
    - Others can do nothing

```bash
chmod -R u=rwx,g=,o= DIRECTORY
```

In the command above, `u` means "user" (aka "owner"), `g` means "group", and `o` means "others". The `=` means "set the permissions to the following", and the `rwx` means "read, write and execute". The `g=` and `o=` mean "set group and other permissions to nothing". The `-R` means "recursively", which means "do this to all of the contents of the directory as well".

Be sure to replace `DIRECTORY` with the path to the `private` directory.

_Remember, `.` is a special alias for the current directory._

3. Once you've changed the permissions, run the `ls -l` command again to make sure they've been updated.

Paste the **10-character** permission string of the updated `private` directory into the input field and submit your answer.
# Executables

You're familiar with the idea of reading and writing data into files. But what about *executing them*? Executable files are just files where the data stored inside is a program that you can run on your computer. 

Files with a `.sh` extension are [shell scripts](https://en.wikipedia.org/wiki/Shell_script). They're just text files that contain shell commands. You can run a file in your shell by typing its filepath:

```bash
mydir/program.sh
```

Interestingly, if the program is in the current directory (in this example, the `mydir` directory), you need to prefix it with `./` to run it:

```bash
./program.sh
```

As far as file paths go, `./program.sh` and `program.sh` are the same. The dot (`.`) is an alias for the current directory. We _need_ the prefix when running executables so that the shell knows we're trying to run a file from a file path, not an installed command like `ls`, `mkdir`, `chmod`, etc.
## Assignment

There seems to be a suspicious script in the `worldbanc/private/bin` directory called `genids.sh`. It looks like it generates some type of identifier... First, let's **remove our ability to run it**, just to see what happens. The `chmod` command has a convenient `-x` flag that will simply remove the executable permission from the file.

1. [x] Run the following commands in `worldbanc/private/bin`: ✅ 2025-01-12

```bash
chmod -x genids.sh
```

2. [x] Let's test those permission changes. Try to run the script: ✅ 2025-01-12

```bash
./genids.sh
```

You should get an error like this:

```bash
permission denied
```

3. [x] That error occurs because the executable permission is not set for your user (the owner). Let's re-add the executable permission for the owner: ✅ 2025-01-12

```bash
chmod +x FILENAME
```

4. [x] Once you've done that, try running the `./genids.sh` script again. ✅ 2025-01-12

Paste the output of the script into the input field and submit your answer.
## Tips

You'll frequently download scripts from the internet to run on your machine, and often you'll need to make them executable before you can run them. I use `chmod +x` quite often as a developer.

The internet is a shady place. Only run verified scripts from trusted publishers and authors.
# Root User

The "root" user is a superuser. It has access to everything on the system and can do anything. When you use the `sudo` command, you're running as the root user (as long as your system hasn't been configured differently).

The `sudo` keyword is convenient because it quickly gives you elevated permissions to run a single command.

However, it can also be dangerous because it gives you access to everything. If you run a command with `sudo` that you don't understand, you could do serious damage to your system.

For example, `rm` with the `r` and `f` flags run on the root directory (`/`), will **delete all the files on your system**. Don't do that. The `r` flag is for "recursive" (delete everything inside) and the `f` flag is for "force". Most systems will prevent you from doing this, but if you run it with `sudo`, you've just turned your computer into a very expensive paperweight.

_Some modern systems will actually prevent you from deleting everything by default as a safeguard unless you use `--no-preserve-root`, but it's still a very bad idea._
## Should I Use sudo?

Sure, as long as you understand what the command you're running does. **Just be careful**.
# Chown

# Chown

So when do you _need_ to use `sudo`? `chmod` allows you to change the permissions of any file or directory that _you_ own. But what if you don't own the file or directory? That's where `sudo` is required. Let's change ownership of a directory to see how that works.

The `chown` command, which stands for "change owner", allows you to change the owner of a file or directory, and it requires root privileges.

## Assignment

1. [ ] Change directory into `worldbanc/private`. Take a look at the contents with `ls`.
2. [ ] You should see a directory called `contacts`. Take a look at its contents.
3. [ ] You should see a file called `emergency.txt`. Take a look at the data inside with `cat`.

Hmmm, it seems like it has some personal contact info for employees. We don't know whose this is, but we're pretty sure it should have its access strictly limited.

4. [ ] Let's change the owner of the entire `contacts` directory to `root`:

```bash
sudo chown -R root contacts
```

Here's an explanation of the command:

- `sudo` - Run as the root user
- `chown` - Command to change the owner
- `-R` - "Recursive", meaning also apply the changes to everything inside the directory
- `root` - The name of the new owner
- `contacts` - The directory to change the owner of

5. [ ] From the `worldbanc/private` directory, run:

```bash
ls -l
```

Paste only the line from the output that represents the `contacts` directory into the input field and submit your answer.
# Using sudo

Before you start this assignment, make sure the permissions on the `worldbanc/private/contacts` directory are `drwx------`, that the owner is `root`, and that you're not signed in as root. If you've been following along, all of those should be true. You can check with the `ls -l` command.

## Assignment

You told senior staff about the `contacts` directory and its contents, and they've decided to delete it entirely.

1. [ ] Go ahead and _try_ to delete the `contacts` directory with the `rm` command:

```bash
rm -r contacts
```

The `contacts` directory should fail to delete! You do not have permission to delete it. It's owned by the `root` user, and you're not `root`.

2. [ ] Try again as root by using `sudo`.
3. [ ] Once you have confirmed that you were able to delete it, run the `ls` command from inside the `private` directory.

Paste the output of the `private` directory's contents into the input field and submit your answer.