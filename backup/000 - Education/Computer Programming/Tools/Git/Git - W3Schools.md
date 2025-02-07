#git #w3schools #versioncontrol

# Git Tutorial

Git is a version control system. Git helps you keep track of code changes. Git is used to collaborate on code.

In this tutorial, we will show you Git commands like this:

```
user@localhost $: git --version
                  git version 2.30.2.windows.1
```

For new users, using the terminal view can seem a bit complicated. Don't worry, this tutorial will keep it really simply, and learning this way gives you a good grasp of how Git works. In the above code, you can see commands (input) and output.

Lines like this are commands we input:

```shell
user@localhost $: git --version
```

Lines like this are the output/response to our commands:

```shell
git version 2.30.2.windows.1
```

In general, lines with `$` in front of it is input. These are the commands you can copy and run in your terminal.
## Git and Remote Repositories

Git and Github are different things. In this tutorial, we will understand what Git is and how to to use it on the remote repository platforms, like Github. 

You can choose, and change which platforms to focus on: three main repository services are:

1. `GitHub`
2. `BitBucket`
3. `GitLab`
## Git and GitHub Introduction
### What is Git?

Git is a popular version control system. It was created by Linus Torvalds in 2005, and has been maintained by Junio Hamano since then.

It is used for:

- Tracking code changes
- Tracking who made changes
- Coding collaboration
### What Does Git Do?

- Manage projects with **Repositories**
- **Clone** a project to work on a local copy
- Control and track changes with **Staging** and **Committing**
- **Branch** and **Merge** to allow for work on different parts and versions of a project
- **Pull** the latest version of the project to a local copy
- **Push** local updates to the main project
### Working with Git

- Initialize Git on a folder, making it a **Repository**
- Git now creates a *hidden folder* to keep track of changes in that folder
- When a file is changed, added or deleted, it is considered **modified**
- You select the modified files you want to **stage**
- The **Staged** files are **Committed**, which prompts Git to store a **permanent** snapshot of the files
- Git allows you to see the full history of every commit
- You can revert back to any previous commit
- Git does not store a separate copy of every file in every commit, but keeps track of changes made in each commit!
### Why Git?

- Over 70% of developers use Git!
- Developers can work together from anywhere in the world
- Developers can see the full history of the project
- Developers can revert to earlier versions of a project
### What is GitHub?

- Git it **not** the same a GitHub.
- GitHub makes tools that use Git.
- GitHub is the largest host of source code in the world, and has been owned by Microsoft since 2018.
- In this tutorial, we will focus on using Git with GitHub.
## Git Getting Started

### Git Install

You can download Git for free from the following website: [https://www.git-scm.com/](https://git-scm.com/)
### Using Git with Command Line

To start using Git, we are fist going to open up our Command Shell.

For Windows, you can use Git bash, which comes included in Git for Windows. For Mac and Linux you can use the built-in terminal.

The first thing we need to do, is to check if Git is properly installed:

```shell
git --version
git version 2.30.2.windows.1
```

If Git is installed, it should show something like `git version X.Y`
### Configure Git

Now let Git know who you are. This is important for version control systems, as each Git commit uses this information:

```shell
git config --global user.name "w3schools-test"
git config --global user.email "test@w3schools.com"
```

Change the username and email address to your own. You will probably also want to use this when registering to GitHub later on. 

> [!NOTE]
> **Note**: use `global` to set the username and email address for **every repository** on your computer. If you want to set the username/email for just the current repo, you can remove `global`.
### Creating Git Folder

Now, let's create a folder for our project:

```shell
mkdir myproject
cd myproject
```

`mkdir` makes a **new directory**
`cd` changes the **current working directory**

> [!NOTE]
> **Note:** If you already have a folder/directory you would like to use for Git:
> 
> Navigate to it in command line, or open it in your file explorer, right-click and select "Git Bash here"
### Initialize Git

```git
git init 
Initialized empty Git repository in /Users/user/myproject/.git/
```

We have just created our first Git repository!

> [!NOTE]
> **Note:** Git now knows that it should watch the folder you initiated it on.
> 
> Git creates a hidden folder to keep track of changes.
## Git New Files

### Git Adding New Files

You just created your first local Git repo. But it is empty.

So let's add some files, or create a new files using your favorite text editor. Then save or move it to the folder you just created. 

If you want to learn how to create a new file using a text editor, you can visit our HTML tutorial: [HTML Editors](https://www.w3schools.com/html/html_editors.asp)

For this example I am going to use a simple HTML file like this:

```HTML
<!DOCTYPE html>  
<html>  
<head>  
<title>Hello World!</title>  
</head>  
<body>  
  
<h1>Hello world!</h1>  
<p>This is the first file in my new Git Repo.</p>  
  
</body>  
</html>
```

And save it to our new folder as `index.html`.

Let's go back to the terminal and list the files in our current working directory:

```shell
ls
index.html
```

`ls` will `list` the files in the directory. We can see that `index.html` is there. 

Then we check the Git `status` and see if it is a part of our repo:

```shell
git status
On branch master

No commits yet

Untracked files:
  (use "git add ..." to include in what will be committed)
    index.html

nothing added to commit but untracked files present (use "git add" to track)
```

Now Git is **aware** of the file, but has not **added** it to our repository.

Files in your Git repository folder can be in one of 2 states:

1. `Tracked`: files that Git knows about and are added to the repository.
2. `Untracked`: files that are in your working directory, but not added to the repository.

When you fist add files to an empty repository, they are all untracked. To get Git to track them, you need to stage them, or add them to the staging environment.

The staging environment will be covered in the next chapter.
## Git Staging Environment

One of the core functions of Git is the concepts of the ***Staging Environment***, and the ***Commit***. 

As you are working, you may be adding, editing and removing files. But whenever you hit a milestone or finish a part of the work, you should add the files to a Staging Environment.

**Staged** files are files that are ready to be **committed** to the repository you are working on. You will learn more about `commit` shortly.

For now, we are done working with `index.html`. So we add it to the Staging Environment.

```shell
git add index.html
```

The file should be **Staged**. Let's check the status:

```shell
git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached ..." to unstage)
    new file: index.html
```

Now the file has been added to the staging environment.
### Git Add More than One File

You can also stage more than one file at a time. Let's add 2 more files to our working folder. Use the text editor again.

A `README.md` file that describes the repository (recommended for all repositories):

```markdown
# hello-world  
Hello World repository for Git tutorial  
This is an example repository for the Git tutoial on https://www.w3schools.com  
  
This repository is built step by step in the tutorial.
```

A basic external style sheet (`bluestyle.css`)

```CSS
body {  
background-color: lightblue;  
}  
  
h1 {  
color: navy;  
margin-left: 20px;  
}
```

And update `index.html` to include the stylesheet:

```HTML
<!DOCTYPE html>  
<html>  
<head>  
<title>Hello World!</title>  
<link rel="stylesheet" href="bluestyle.css">  
</head>  
<body>  
  
<h1>Hello world!</h1>  
<p>This is the first file in my new Git Repo.</p>  
  
</body>  
</html>
```

Now add all files to the ***staging environment:***

```shell
git add --all
```

Using `--all` instead of individual filenames will `stage` all changes (new, modified and deleted) files.

```shell
git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached ..." to unstage)
        new file:   README.md
        new file:   bluestyle.css
        new file:   index.html
```

> [!NOTE]
> **Note:** The shorthand command for `git add --all` is `git add -A`
## Git Commit

Since we have finished our work, we are ready to move from `stage` to `commit` for our repo. 

Adding commits keeps track of our progress and changes as we work. Git considers each `commit` change point or "save point". It is a point in the project you can go back to if you find a bug, or want to make a change.

When we `commit`, we should **always include a message**. 

By adding clear messages to each commit, it is easy for yourself (and others) to see what has changed and when. 

```shell
git commit -m "First release of Hello World!"
[master (root-commit) 221ec6e] First release of Hello World!
 3 files changed, 26 insertions(+)
 create mode 100644 README.md
 create mode 100644 bluestyle.css
 create mode 100644 index.html
```

The `commit` command performs a commit, and the `-m "message"` adds a message.

The Staging Environment has been committed to our repo, with the message: "First release of Hello World!"
### Git Commit without Stage

Sometimes, when you make small changes, using the staging environment seems like a waste of time. It is possible to *commit changes directly*, skipping the staging environment.
The `-a` option will automatically stage every changed, already tracked file.

Let's add a small update to index.html.

```html
<!DOCTYPE html>  
<html>  
<head>  
<title>Hello World!</title>  
<link rel="stylesheet" href="bluestyle.css">  
</head>  
<body>  
  
<h1>Hello world!</h1>  
<p>This is the first file in my new Git Repo.</p>  
<p>A new line in our file!</p>  
  
</body>  
</html>
```

And check the status of our repository. But this time, we will use the --short option to see the changes in a more compact way:

```shell
git status --short
 M index.html
```

> [!NOTE]
> **Note**: Short status flags are: 
> 
> - ?? - Untracked files
> - A - Files added to stage
> - M - Modified Files
> - D - Deleted Files

We see that the file we expected is modified. So let's commit it directly:

```shell
git commit -a -m "Updated index.html with a new line"
[master 09f4acd] Updated index.html with a new line
 1 file changed, 1 insertion(+)
```

> [!Warning]
> **Warning**: Skipping the Staging Environment is not generally recommended. Skipping the stage step can sometimes make you include unwanted changes. 
### Git Commit Log

To view the history of commits for a repository, you can use the `log` command.

```shell
git log
commit 09f4acd3f8836b7f6fc44ad9e012f82faf861803 (HEAD -> master)
Author: w3schools-test 
Date:   Fri Mar 26 09:35:54 2021 +0100

    Updated index.html with a new line

commit 221ec6e10aeedbfd02b85264087cd9adc18e4b26
Author: w3schools-test 
Date:   Fri Mar 26 09:13:07 2021 +0100

    First release of Hello World!
```
## Git Help

If you are having trouble remembering commands or options for commands, you can use Git `help`.

There are a couple of different ways you can use the `help` command in the command line:

- `git command -help`: see all the available options for the specific command.
- `git help --all`: See all possible commands

Let's go over the different commands.
### Get `-help` See Options for a Specific Command

Any time you need some help remembering the specific option for a command, you can use `git command -help`:

```shell
git commit -help
usage: git commit [] [--] ...

    -q, --quiet           suppress summary after successful commit
    -v, --verbose         show diff in commit message template

Commit message options
    -F, --file      read message from file
    --author      override author for commit
    --date          override date for commit
    -m, --message 
                          commit message
    -c, --reedit-message 
                          reuse and edit message from specified commit
    -C, --reuse-message 
                          reuse message from specified commit
    --fixup       use autosquash formatted message to fixup specified commit
    --squash      use autosquash formatted message to squash specified commit
    --reset-author        the commit is authored by me now (used with -C/-c/--amend)
    -s, --signoff         add a Signed-off-by trailer
    -t, --template 
                          use specified template file
    -e, --edit            force edit of commit
    --cleanup       how to strip spaces and #comments from message
    --status              include status in commit message template
    -S, --gpg-sign[=]
                          GPG sign commit

Commit contents options
    -a, --all             commit all changed files
    -i, --include         add specified files to index for commit
    --interactive         interactively add files
    -p, --patch           interactively add changes
    -o, --only            commit only specified files
    -n, --no-verify       bypass pre-commit and commit-msg hooks
    --dry-run             show what would be committed
    --short               show status concisely
    --branch              show branch information
    --ahead-behind        compute full ahead/behind values
    --porcelain           machine-readable output
    --long                show status in long format (default)
    -z, --null            terminate entries with NUL
    --amend               amend previous commit
    --no-post-rewrite     bypass post-rewrite hook
    -u, --untracked-files[=]
                          show untracked files, optional modes: all, normal, no. (Default: all)
    --pathspec-from-file 
                          read pathspec from file
    --pathspec-file-nul   with --pathspec-from-file, pathspec elements are separated with NUL character
```

**Note**: You can also use `--help` instead of `-help` to open the relevant Git manual page.
### Git help `--all` See All Possible Commands

To list all possible commands, use the `help --all` command:

> [!Warning]
> **Warning:** This will display a very long list of commands

```shell
$ git help --all
See 'git help ' to read about a specific subcommand

Main Porcelain Commands
   add                  Add file contents to the index
   am                   Apply a series of patches from a mailbox
   archive              Create an archive of files from a named tree
   bisect               Use binary search to find the commit that introduced a bug
   branch               List, create, or delete branches
   bundle               Move objects and refs by archive
   checkout             Switch branches or restore working tree files
   cherry-pick          Apply the changes introduced by some existing commits
   citool               Graphical alternative to git-commit
   clean                Remove untracked files from the working tree
   clone                Clone a repository into a new directory
   commit               Record changes to the repository
   describe             Give an object a human readable name based on an available ref
   diff                 Show changes between commits, commit and working tree, etc
   fetch                Download objects and refs from another repository
   format-patch         Prepare patches for e-mail submission
   gc                   Cleanup unnecessary files and optimize the local repository
   gitk                 The Git repository browser
   grep                 Print lines matching a pattern
   gui                  A portable graphical interface to Git
   init                 Create an empty Git repository or reinitialize an existing one
   log                  Show commit logs
   maintenance          Run tasks to optimize Git repository data
   merge                Join two or more development histories together
   mv                   Move or rename a file, a directory, or a symlink
   notes                Add or inspect object notes
   pull                 Fetch from and integrate with another repository or a local branch
   push                 Update remote refs along with associated objects
   range-diff           Compare two commit ranges (e.g. two versions of a branch)
   rebase               Reapply commits on top of another base tip
   reset                Reset current HEAD to the specified state
   restore              Restore working tree files
   revert               Revert some existing commits
   rm                   Remove files from the working tree and from the index
   shortlog             Summarize 'git log' output
   show                 Show various types of objects
   sparse-checkout      Initialize and modify the sparse-checkout
   stash                Stash the changes in a dirty working directory away
   status               Show the working tree status
   submodule            Initialize, update or inspect submodules
   switch               Switch branches
   tag                  Create, list, delete or verify a tag object signed with GPG
   worktree             Manage multiple working trees

Ancillary Commands / Manipulators
   config               Get and set repository or global options
   fast-export          Git data exporter
   fast-import          Backend for fast Git data importers
   filter-branch        Rewrite branches
   mergetool            Run merge conflict resolution tools to resolve merge conflicts
   pack-refs            Pack heads and tags for efficient repository access
   prune                Prune all unreachable objects from the object database
   reflog               Manage reflog information
   remote               Manage set of tracked repositories
   repack               Pack unpacked objects in a repository
   replace              Create, list, delete refs to replace objects

Ancillary Commands / Interrogators
   annotate             Annotate file lines with commit information
   blame                Show what revision and author last modified each line of a file
   bugreport            Collect information for user to file a bug report
   count-objects        Count unpacked number of objects and their disk consumption
   difftool             Show changes using common diff tools
   fsck                 Verifies the connectivity and validity of the objects in the database
   gitweb               Git web interface (web frontend to Git repositories)
   help                 Display help information about Git
   instaweb             Instantly browse your working repository in gitweb
   merge-tree           Show three-way merge without touching index
   rerere               Reuse recorded resolution of conflicted merges
   show-branch          Show branches and their commits
   verify-commit        Check the GPG signature of commits
   verify-tag           Check the GPG signature of tags
   whatchanged          Show logs with difference each commit introduces

Interacting with Others
   archimport           Import a GNU Arch repository into Git
   cvsexportcommit      Export a single commit to a CVS checkout
   cvsimport            Salvage your data out of another SCM people love to hate
   cvsserver            A CVS server emulator for Git
   imap-send            Send a collection of patches from stdin to an IMAP folder
   p4                   Import from and submit to Perforce repositories
   quiltimport          Applies a quilt patchset onto the current branch
   request-pull         Generates a summary of pending changes
   send-email           Send a collection of patches as emails
   svn                  Bidirectional operation between a Subversion repository and Git

Low-level Commands / Manipulators
   apply                Apply a patch to files and/or to the index
   checkout-index       Copy files from the index to the working tree
   commit-graph         Write and verify Git commit-graph files
   commit-tree          Create a new commit object
   hash-object          Compute object ID and optionally creates a blob from a file
   index-pack           Build pack index file for an existing packed archive
   merge-file           Run a three-way file merge
   merge-index          Run a merge for files needing merging
   mktag                Creates a tag object
   mktree               Build a tree-object from ls-tree formatted text
   multi-pack-index     Write and verify multi-pack-indexes
   pack-objects         Create a packed archive of objects
   prune-packed         Remove extra objects that are already in pack files
   read-tree            Reads tree information into the index
   symbolic-ref         Read, modify and delete symbolic refs
   unpack-objects       Unpack objects from a packed archive
   update-index         Register file contents in the working tree to the index
   update-ref           Update the object name stored in a ref safely
   write-tree           Create a tree object from the current index
.0
Low-level Commands / Interrogators
   cat-file             Provide content or type and size information for repository objects
   cherry               Find commits yet to be applied to upstream
   diff-files           Compares files in the working tree and the index
   diff-index           Compare a tree to the working tree or index
   diff-tree            Compares the content and mode of blobs found via two tree objects
   for-each-ref         Output information on each ref
   for-each-repo        Run a Git command on a list of repositories
   get-tar-commit-id    Extract commit ID from an archive created using git-archive
   ls-files             Show information about files in the index and the working tree
   ls-remote            List references in a remote repository
   ls-tree              List the contents of a tree object
   merge-base           Find as good common ancestors as possible for a merge
   name-rev             Find symbolic names for given revs
   pack-redundant       Find redundant pack files
   rev-list             Lists commit objects in reverse chronological order
   rev-parse            Pick out and massage parameters
   show-index           Show packed archive index
   show-ref             List references in a local repository
   unpack-file          Creates a temporary file with a blob's contents
   var                  Show a Git logical variable
   verify-pack          Validate packed Git archive files

Low-level Commands / Syncing Repositories
   daemon               A really simple server for Git repositories
   fetch-pack           Receive missing objects from another repository
   http-backend         Server side implementation of Git over HTTP
   send-pack            Push objects over Git protocol to another repository
   update-server-info   Update auxiliary info file to help dumb servers

Low-level Commands / Internal Helpers
   check-attr           Display gitattributes information
   check-ignore         Debug gitignore / exclude files
   check-mailmap        Show canonical names and email addresses of contacts
   check-ref-format     Ensures that a reference name is well formed
   column               Display data in columns
   credential           Retrieve and store user credentials
   credential-cache     Helper to temporarily store passwords in memory
   credential-store     Helper to store credentials on disk
   fmt-merge-msg        Produce a merge commit message
   interpret-trailers   Add or parse structured information in commit messages
   mailinfo             Extracts patch and authorship from a single e-mail message
   mailsplit            Simple UNIX mbox splitter program
   merge-one-file       The standard helper program to use with git-merge-index
   patch-id             Compute unique ID for a patch
   sh-i18n              Git's i18n setup code for shell scripts
   sh-setup             Common Git shell script setup code
   stripspace           Remove unnecessary whitespace

External commands
   askyesno
   credential-helper-selector
   flow
   lfs
```

**Note:** If you find yourself stuck in the list view, `SHIFT + G` to jump the end of the list, then `q` to exit the view.

---
## Git Branch
### Working with Git Branches

In Git, a `branch` is a new/separate version of the main repository.

Let's say you have a large project, and you need to update the design on it.

How would that work without and with Git:

Without Git:

- Make copies of all the relevant files to avoid impacting the live version.
- Start working with the design and find that code depends on other code files, that also need to be changed.
- Make copies of the dependent files as well. Making sure that every file dependency references the correct file name.
- EMERGENCY! There is an unrelated error somewhere else in the project that needs to be fixed ASAP.
- Save all your files, making a note of the names of the copies you were working on.
- Work on the unrelated error and update the code to fix it
- Go back to the design, and finish the work there
- Copy the code or rename the files, so the updated design is on the live version.
- (2 weeks later, you realized that the unrelated error was not fixed in the new design version because you copied the files before the fix)

With Git:

- With a new branch called new-design, edit the code directly without impacting the main branch
- EMERGENCY! There is an unrelated error somewhere else in the project that needs to be fixed ASAP!
- Create a new branch from the main project called small-error-fix
- Fix the unrelated error and merge the small-error-fix branch with the main branch
- You go back to the new design branch, and finish the work there.
- Merge the new-design branch with main (getting alerted to the small error fix that you were missing)

Branches allow you to work on different parts of a project without impacting the main branch.

When the work is complete, a branch can be merged with the main project. 

You can even switch between branches and work on different project without them interfering with each other. 

Branching in Git is very lightweight and fast.
### New Git Branch

Let's add some new features to our `index.html` page.

We are working in our local repository, and we do not want to disturb or possibly wreck the main project. 

So we create a new `branch`:

```shell
git branch hello-world-images
```

Now we created a new branch called "`hello-world-images`"

Let's confirm that we have created a new `branch`:

```shell
git branch
  hello-world-images
* master
```

We can see the new branch with the name "hello-world-images", but the `*` beside `master` specifies that we are currently on that `branch`.

`checkout` is the command used to check out a `branch`. Moving us from the current `branch`, *to* the one specified at the end of the command:

```shell
git checkout hello-world-images
Switched to branch 'hello-world-images'
```

Now we have moved our current workspace from the master branch, to the new `branch`. Open your favorite editor and make some changes.

For this example, we added an image (img_hello_world.jpg) to the working folder and a line of code in the `index.html` file:

```html
<!DOCTYPE html>  
<html>  
<head>  
<title>Hello World!</title>  
<link rel="stylesheet" href="bluestyle.css">  
</head>  
<body>  
  
<h1>Hello world!</h1>  
<div><img src="img_hello_world.jpg" alt="Hello World from Space"  
style="width:100%;max-width:960px"></div>  
<p>This is the first file in my new Git Repo.</p>  
<p>A new line in our file!</p>  
  
</body>  
</html>
```

We have made changes to a file and added a new file in the working directory (same directory as the `main branch`). Now check the status of the working `branch`:

```shell
git status
On branch hello-world-images
Changes not staged for commit:
  (use "git add ..." to update what will be committed)
  (use "git restore ..." to discard changes in working directory)
        modified:   index.html

Untracked files:
  (use "git add ..." to include in what will be committed)
        img_hello_world.jpg

no changes added to commit (use "git add" and/or "git commit -a")
```

Let's go through what happens here:

- There are changes to our index.html, but the file is not staged for `commit`
- `img_hello_world.jpg` is not `tracked`

So we need to add both files to the Staging Environment for this `branch`:

```shell
git add --all
```

Using `--all` instead of individual file names with **stage** all changed (new, modified, and deleted) files.

Check the `status` of the `branch`:

```shell
git status
On branch hello-world-images
Changes to be committed:
  (use "git restore --staged ..." to unstage)
    new file: img_hello_world.jpg
    modified: index.html
```

We are happy with our changes. So we will commit them to the `branch`:

```shell
git commit -m "Added image to Hello World"
[hello-world-images 0312c55] Added image to Hello World
2 files changed, 1 insertion(+)
create mode 100644 img_hello_world.jpg
```

Now we have a new `branch`, that is different from the master `branch`.

> [!NOTE]
> **Note**: Using the `-b` option on `checkout` will create a new branch, and move to it, if it does not exist
### Switching Between Branches

Now let's see just how quick and easy it is to work with different branches, and how well it works. 

We are currently on the branch `hello-world-images`. We added an image to this branch, so let's list the files in the current directory:

```shell
ls
README.md  bluestyle.css  img_hello_world.jpg  index.html
```

We can see the new file `img_hello_world.jpg`, and if we open the HTML file, we can see the code has been altered. All is as it should be.

Now, let's see what happens when we change branch to `master`.

```shell
git checkout master
Switched to branch 'master'
```

The new image in not a part of this branch. List the files in the current directory again:

```shell
ls
README.md  bluestyle.css  index.html
```

`img_hello_world.jpg` is no longer there! And if we open the `HTML` file, we can see the code reverted to what it was before the alteration. See how easy it is to work with branches? And how this allows you to work on different things?
### Emergency Branch

Now imagine that we are not yet done with hello-world-images, but we need to fix an error on master. 

I don't want to mess with master directly, and I do not want to mess with hello-world-images, since it is not done yet. 

So we create a new branch to deal with the emergency:

```
git checkout -b emergency-fix
Switched to new branch 'emergency-fix'
```

Now we have created a new branch from master, and changed to it. We can safely fix the error without disturbing the other branches. Let's fix our imaginary error:

```html
<!DOCTYPE html>  
<html>  
<head>  
<title>Hello World!</title>  
<link rel="stylesheet" href="bluestyle.css">  
</head>  
<body>  
  
<h1>Hello world!</h1>  
<p>This is the first file in my new Git Repo.</p>  
<p>This line is here to show how merging works.</p>  
  
</body>  
</html>
```

We have made changes in this file, and we need to get those changes to the master branch. Check the status:

```shell
git status
On branch emergency-fix
Changes not staged for commit:
  (use "git add ..." to update what will be committed)
  (use "git restore ..." to discard changes in working directory)
        modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
```

Stage the file, and commit:

```shell
git add index.html
git commit -m "updated index.html with emergency fix"
[emergency-fix dfa79db] updated index.html with emergency fix
 1 file changed, 1 insertion(+), 1 deletion(-)
```

Now we have a fix ready for master, and we need to merge the two branches.
## Git Branch Merge

We have the emergency fix ready, and so let's merge the master and emergency-fix branches.

First, we need to change to the master branch:

```shell
git checkout master
Switched to branch 'master'
```

Now we merge the current branch (master) with emergency-fix:

```shell
git merge emergency-fix
Updating 09f4acd..dfa79db
Fast-forward
 index.html | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

Since the emergency-fix branch came directly from master, and no other changes had been made to master while we were working, Git sees this as a continuation of master. So it can "Fast-Forward", just pointing both master and emergency-fix to the same commit.

As master and emergency fix are essentially the same now, we can delete emergency-fix, as it is no longer needed.

```
git branch -d emergency-fix
Deleted branch emergency-fix (was dfa79db)
```
### Merge Conflict

Now we can move over to hello-world-images and keep working. Add another image file (`img_hello_git.jpg`) and change index.html, so it shows it:

```shell
git checkout hello-world-images
Switched to branch 'hello-world-images'
```

```html
<!DOCTYPE html>  
<html>  
<head>  
<title>Hello World!</title>  
<link rel="stylesheet" href="bluestyle.css">  
</head>  
<body>  
  
<h1>Hello world!</h1>  
<div><img src="img_hello_world.jpg" alt="Hello World from Space" style="width:100%;max-width:960px"></div>  
<p>This is the first file in my new Git Repo.</p>  
<p>A new line in our file!</p>  
<div><img src="img_hello_git.jpg" alt="Hello Git" style="width:100%;max-width:640px"></div>  
  
</body>  
</html>
```

Now, we are done with our work here and can stage and commit for this branch:

```shell
git add --all
git commit -m "added new image"
[hello-world-images 1f1584e] added new image
 2 files changed, 1 insertion(+)
 create mode 100644 img_hello_git.jpg
```

We see that index.html has been changed in both branches. Now we are ready to merge hello-world-images into master. But what will happen to the changes we recently made in master?

```shell
git checkout master
git merge hello-world-images
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

The merge failed, as there is conflict between the version for index.html. Let us check the status:

```shell
git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Changes to be committed:
        new file:   img_hello_git.jpg
        new file:   img_hello_world.jpg

Unmerged paths:
  (use "git add ..." to mark resolution)
        both modified:   index.html
```

This conforms there is a conflict in `index.html`, but the image files are ready and staged to be committed.

So we need to fix that conflict. Open the file in our editor.

```HTML
<!DOCTYPE html>  
<html>  
<head>  
<title>Hello World!</title>  
<link rel="stylesheet" href="bluestyle.css">  
</head>  
<body>  
  
<h1>Hello world!</h1>  
<div><img src="img_hello_world.jpg" alt="Hello World from Space" style="width:100%;max-width:960px"></div>  
<p>This is the first file in my new Git Repo.</p>  
<<<<<<< HEAD  
<p>This line is here to show how merging works.</p>  
=======  
<p>A new line in our file!</p>  
<div><img src="img_hello_git.jpg" alt="Hello Git" style="width:100%;max-width:640px"></div>  
>>>>>>> hello-world-images  
  
</body>  
</html>
```

We can see the differences between the version and edit it like we want:

```HTML
<!DOCTYPE html>  
<html>  
<head>  
<title>Hello World!</title>  
<link rel="stylesheet" href="bluestyle.css">  
</head>  
<body>  
  
<h1>Hello world!</h1>  
<div><img src="img_hello_world.jpg" alt="Hello World from Space" style="width:100%;max-width:960px"></div>  
<p>This is the first file in my new Git Repo.</p>  
<p>This line is here to show how merging works.</p>  
<div><img src="img_hello_git.jpg" alt="Hello Git" style="width:100%;max-width:640px"></div>  
  
</body>  
</html>
```

Now we can stage index.html and check the status:

```shell
git add index.html
git status
On branch master
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:
        new file:   img_hello_git.jpg
        new file:   img_hello_world.jpg
        modified:   index.html
```

The conflict has been fixed, and we can use commit to conclude the merge:

```shell
git commit -m "merged with hello-world-images after fixing conflicts"
[master e0b6038] merged with hello-world-images after fixing conflicts
```

And delete the hello-world-images branch:

```shell
git branch -d hello-world-images
Deleted branch hello-world-images (was 1f1584e).
```

Now we have a better understanding of how branches and merging works. Time to start working with a remote reposity.
# Git and Github

## Create a Repository on Github

Now that you have made a Github account, sign in, and create a new repo:

![](https://i.imgur.com/iArpQfK.png)

Then fill in the details:

![](https://i.imgur.com/DIeZeTJ.png)

We will go over the different options and what they mean later. But for now, choose Public (if you want the repo to be viewable for anyone) or Private (if you want to choose who should be able to view the repo). Either way, you will be able to choose who can **contribute** to the repo.

Then click "Create Repository".
## Push Local Repository to Github

Since we have already set up a local Git repo, we are going to `push` that to GitHub:

![](https://i.imgur.com/jal2ZMS.png)

Copy the URL, or click the clipboard marked in the image above. Now paste it in the following command:

```shell
git remote add origin https://github.com/w3schools-test/hello-world.git
```

`git remote add origin URL` specifies that you are adding a remote repository, with the specified `URL` as an `origin` to your local Git repo. Now we are going to push our master branch to the origin url, and set it as the default remote branch:

```shell
git push --set-upstream origin master
Enumerating objects: 22, done.
Counting objects: 100% (22/22), done.
Delta compression using up to 16 threads
Compressing objects: 100% (22/22), done.
Writing objects: 100% (22/22), 92.96 KiB | 23.24 MiB/s, done.
Total 22 (delta 11), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (11/11), done.
To https://github.com/w3schools-test/hello-world.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```

> [!NOTE]
> **Note**: Since this is the first time you are connecting to GitHub, you will get some kind of notification for you to authenticate this connection.

Now, go back into GitHub and see that the repository has been updated:

![](https://i.imgur.com/ipQFp6W.png)
## GitHub Edit Code
### Edit Code in GitHub

In addition to being a host for Git content, GitHub has a very good code editor. 

Let's try to edit the `README.md` file in GitHub. Just click the edit button:

![](https://i.imgur.com/HfFJASP.png)

Add some changes to the code, and then `commit` the changes. For now, we will "Commit directly to the master branch". Remember to add a description for the `commit`. 

![](https://i.imgur.com/dDKTb6K.png)

That is how you edit code directly in GitHub!
## Git Pull From GitHub
### Pulling to Keep up-to-date with Changes

When working as a team on a project, it is important that everyone stays up to date. Any time you start working on a project, you should get the most recent changes to your local copy. 

With Git, you can do that with `pull`.

`pull` is a combination of 2 different commands:

1. `fetch`
2. `merge`

Let's take a closer look into how `fetch`, `merge` and `pull` works.
### Git Fetch

`fetch` gets all the change history of a tracked branch/repo. So, on your local Git, `fetch` updates to see what has changed on GitHub:

```shell
git fetch origin
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 2), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 733 bytes | 3.00 KiB/s, done.
From https://github.com/w3schools-test/hello-world
   e0b6038..d29d69f  master     -> origin/master
```

Now that we have the recent `changes`, we can check our `status`:

```shell
git status
On branch master
Your branch is behind 'origin/master' by 1 commit, and can be fast-forwarded.
  (use "git pull" to update your local branch)

nothing to commit, working tree clean
```

We are behind the `origin/master` by 1 `commit`. That should be the updated `README.md`, but let's double check by viewing the `log`:

```shell
git log origin/master
commit d29d69ffe2ee9e6df6fa0d313bb0592b50f3b853 (origin/master)
Author: w3schools-test <77673807+w3schools-test@users.noreply.github.com>
Date:   Fri Mar 26 14:59:14 2021 +0100

    Updated README.md with a line about GitHub

commit e0b6038b1345e50aca8885d8fd322fc0e5765c3b (HEAD -> master)
Merge: dfa79db 1f1584e
Author: w3schools-test 
Date:   Fri Mar 26 12:42:56 2021 +0100

    merged with hello-world-images after fixing conflicts

...
...
```

That look as expected, but we can also verify by showing the differences between our local `master` and `origin/master`:

```shell
git diff origin/master
diff --git a/README.md b/README.md
index 23a0122..a980c39 100644
--- a/README.md
+++ b/README.md
@@ -2,6 +2,4 @@
 Hello World repository for Git tutorial
 This is an example repository for the Git tutoial on https://www.w3schools.com

-This repository is built step by step in the tutorial.
-
-It now includes steps for GitHub
+This repository is built step by step in the tutorial.
\ No newline at end of file
```

