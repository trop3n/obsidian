---
up: "[[Learn Git]]"
tags:
  - "#education/computerprogramming/platforms/bootdev/git/repositories"
prev: "[[Internals]]"
---

# Config

The very first step of any project is to create a repository. A Git "repository" (or "repo") represents a single project. You'll typically have one repository for each project you work on. 

A repo is essentially just a directory that contains a project (other directories and files). The only difference is that is *also* contains a hidden `.git` directory. That hidden directory is where Git stores all of its internal tracking and versioning information for the project. 
## WebFlyx

In this course, we'll be managing content for "WebFlyx", an imaginary self-hosted video streaming application. WebFlyx serves content directly from a Git repo!
## Assignment

Navigate to somewhere on your filesystem where you'd like to store your project. Once you're there, create a new directory called `webflyx` and `cd` into it. 

```bash
mkdir webflyx
cd webflyx
```

Once inside, create a new Git repository:

```bash
git init
```

You should now have a hidden `.git` directory in your `webflyx` directory. This means you've successfully created a new Git repository! List (`ls -a`) the contents of the directory to confirm.

_Run and submit the tests from the root of the `webflyx` directory._
# Status

A file can be in one of several states in a Git repo. Here are a few important ones:

- `untracked`: Not being tracked by Git
- `staged`: Marked for inclusion in the next commit
- `committed`: Saved to the repo's history

The `git status` command shows you the current state of your repo. It will tell you which files are untracked, staged, and committed.
## Assignment

Every good content management system needs a table of contents. 

1. [x] Create a file in the root directory of your `webflyx` directory called `contents.md` and add the following text to the file: ✅ 2025-02-04

```
# contents
```

2. [x] Save the file, then run: ✅ 2025-02-04

```
git status
```
# Staging

The `contents.md` file has been created, but as we saw, it's *untracked*. We need to stage it (add it to the "index") with the `git add` command before committing it later. Without staging, every file in the repository would be included in every commit, but that's often not what you want. 

Here's the command: 

```
git add i-use-arch.btw
```
# Commit

After staging a file, we can commit it.

A commit is a snapshot of the repository at a given point in time. It's a way to save the state of the repository, and it's how Git keeps track of changes to the project. A commit comes with a message that describes the changes made in the commit.

Here's how to commit all of your staged files:

```
git commit -m "your message here"
```
# Half of Git

You've learned half of Git. Well, not really. But kind of.

Half of your workflow as a developer will just be three simple commands:

1. `git status`
2. `git add`
3. `git commit`

It's most of what you need to work effectively as a solo developer. Another 40% of Git is about collaborating and storing your work on a remote server. 

The last 10% is mostly about fixing mistakes, rolling back changes, and other advanced topics. Don't worry, we'll cover those too. 
# Git Log

A Git repo is a (potentially very long) list of commits, where each commit represents the *full state* of the repository at a given point in time.

The `git log` command shows a history of the commits in a repository. This is what makes Git a version control system. You can see:

- Who made a commit
- When the commit was made
- What has changed
## A Commit Hash

Each commit has a unique identifier called a "commit hash". This is a long string of characters the uniquely identifies the commit. Here's an example of mine. 

```
5ba786fcc93e8092831c01e71444b9baa2228a4f
```

For convenience, you can refer to any commit or change within Git by using the first `7` characters of its hash. For mine, that's `5ba786f`.
## Assignment

Run the `git log` command. You should see your commit. Notice that `git log` (assuming the log is long enough) starts an interactive pager. You can scroll through the log with the arrow keys, and exit by pressing `q`.

Next, run `git log` again, but this time use the `-n` and `--no-pager` options to limit the maximum number of commits shown, and more importantly, to run it without the interactive pager. E.g.:

```bash
git --no-pager log -n 10
```

Run and submit the tests.

