---
up: "[[Learn Git]]"
tags:
  - education/computerprogramming/platforms/bootdev/git/setup
prev: "[[Repositories]]"
---

# Git

[Git](https://git-scm.com/) is _the_ distributed [version control system](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control) (VCS). Nearly every developer in the world uses it to manage their code. It has quite a monopoly on VCS. Developers use Git to:

- Keep a history of their code changes.
- Revert mistakes made in their code.
- Collaborate with other developers
- Make backups of their code
- And much more
## Boot.dev CLI

Throughout this course, you'll be using the Boot.dev CLI to run our tests (which are just CLI commands) against your local environment. [Install it now](https://github.com/bootdotdev/bootdev?tab=readme-ov-file#installation) if you don't already have it. All the instructions and troubleshooting info are on the GitHub page.

Make sure the Boot.dev CLI install worked:

```bash
bootdev --version
```

_If you're stuck, reach out in the help forums of the [Discord](https://www.boot.dev/community)._

Once the `bootdev` command is working, log in and follow the instructions:

```
bootdev login
```
## Run vs. Submit

Each lesson has a list of "commands" it runs on your local machine, and a series of tests it will check against the results of the command. 

There are two ways to run these commands: `run` and `submit`.

1. `bootdev run <id>`: This will run the commands and show you the results. It's to be used for debugging, but it won't tell you whether or not you've passed the tests explicitly. 
2. `bootdev run <id> -s`: This will run the commands and give you pass/fail feedback. It will also mark the lesson as complete on the website. If you get it wrong however, you'll potentially lose your sharpshooter spree, so be sure to use `run` first. 

You can copy the run/submit commands with the id ready-to-go from the test panel.
## Assignment

Once you have the CLI installed and you're logged in, copy and paste the `run` command from the right into your terminal and execute it. If it's doing what you'd expect (printing `rebasing is based`), then run the submit command.
# Install Git

Git is a command line tool, just like the Boot.dev CLI. Let's install it.

## Assignment

First, check and see if you already have Git installed. Open a terminal and type:

```bash
git --version
```

If you see a version number, you're good to go! **Run and submit the tests**.

_Otherwise, you'll need to install Git. See below for help._

### Windows (WSL) / Linux (Ubuntu)

```bash
sudo apt install git-all
```

### macOS

Running `git --version` should prompt you to install Git. If not, you can use [Homebrew](https://brew.sh/):

```bash
brew install git
```

Alternatively, you can use [Xcode](https://developer.apple.com/xcode/):

1. Install Xcode from the App Store if you don't already have it.
2. Run `xcode-select --install` in a new terminal window. This should install the "Command Line Tools" package, which includes Git.
# RTFM

One of the best parts of using Git is that all the documentation is fantastic, but that wasn't always the case.

Git was known as being the most obtusely documented tool of all time, but alas, *times have changed*.
# Command Syntax

Throughout this course, you'll see commands written like this:

```
command <required> [optional]
```

- arguments in angle brackets `<>` are **mandatory** and must be provided when running the command. 
- arguments in square brackets `[]` are **optional** and can be included if needed.

For example, to create a new directory in your terminal, you would run:

```
mkdir <directory-name>
```

- `mkdir` is the command.
- `<directory-name>` is the required argument.
# Porcelain and Plumbing

In Git, commands are divided into high-level ("porcelain") commands and low-level ("plumbing") commands. The porcelain commands are the ones that you will use most often as a developer to interact with your code. Some porcelain commands are:

- `git status`
- `git add`
- `git commit`
- `git push`
- `git pull`
- `git log`

Don't worry about what they do yet, we will cover that in detail soon. Some examples of plumbing commands are:

- `git apply`
- `git commit-tree`
- `git hash-object`

We'll focus on the high-level command because that's what you use 99% of the time as a developer, but we'll dip down into the low-level commands occasionally to really understand how Git works.
# Quick Config

We need to configure Git to contain *your* information. Whenever code changes, Git tracks *who* made the change. To ensure you get proper credit (or more likely, blame) for all the code you write, you need to set your name and email. 

Git comes with a configuration both at the global and repo level. Most of the time, you'll just use the global config.
## Assignment

Let's see your identity. Check your `user.name` and `user.email` are already set:

```
git config --get user.name
```

```
git config --get user.email
```

If they aren't, set them. 

I recommend using your GitHub username and email.

```bash
git config --add --global user.name "github_username_here"
git config --add --global user.email "email@example.com"
```

Finally, let's set a default branch (we'll talk more about configs and branches later) so that we're all on the same page. Run:

```bash
git config --global init.defaultBranch master
```

We're using `master` for now because it is Git's default, but later we'll change it to `main`, which is GitHub's default. Just bear with us for a second.

