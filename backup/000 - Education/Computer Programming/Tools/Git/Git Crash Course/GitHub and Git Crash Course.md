#git #versioncontrol #github 

Git is a powerful version control system that allows developers to track changes to code, collaborate with others, and manage multiple versions of a project. By mastering Git in the command line, developers gain the flexibility to perform various tasks efficiently , such as creating  and switching between branches, resolving merge conflicts, and managing remote repositories. Additionally, familiarity with the command line provides a deeper understanding of Git's inner working, enabling developers to troubleshoot issues and customize their workflows more efficiently. 

In this guide, beginners can learn about version control and hot to get started with Git. To follow along, you'll need access to a terminal and administrative privileges to install Git.
# Introduction to Version Control and Git

In nutshell, version control is a system that allows you to track changes to files over time. This is useful for a variety of reasons, including:

- **Collaboration**: Version control allows multiple people to work on the same files at the same time without overwriting each other's changes.
- **History**: Version control keeps a history of all changes made to files, so you can see who made a change, when they made it and why.
- **Rollback**: Version control allows you to rollback to a previous version of a file if you make a mistake.

Git is a popular version control tool widely used for software development, but it can also be used for any type of project that involves managing multiple files. Git is designed to be efficient, flexible and easy to use. It is a powerful tool that can help you manage your projects more efficiently.
## Installing and Configuring Git

The [official Git documentation](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) has detailed instructions on how to install Git on all supported systems. On Ubuntu, you could run the following to get Git installed:

```
sudo apt update && sudo apt install git
```

To verify that the installation was successful, you can run:

```
git --version
```

Once you have Git installed, you'll need to configure it with your name and email:

```
# Set your Git name
git config --global user.name "Your Name"

# Set your Git email
git config --global user.email "your@email.com"

# Configures default initial branch
git config --global init.defaultBranch "main"
```
## The Basic Git Workflow

The basic Git workflow involves a cycle of making changes to files, staging those changes, committing them to your local repository, and then pushing them to a remote repository. Staging changes allows you to group together related changes *before committing them*. Committing changes creates a snapshot of your project at a specific point in time, along with a message describing the changes. Pushing changes to a remote repository makes them available to other collaborators and backs up your work in case something happens to your local repository. This cycle allows you to track changes, collaborate with others, and easily revert to previous versions of your project. 

![](https://i.imgur.com/qAC9XBx.png)

The image shows an analogy for the Git workflow using letters. When you're working on the contents of your letter, you have **unstaged changes**. When you're ready, you'll add the letter to an envelope, and that's the equivalent of adding files to your staging area. Finally, you'll commit your changes by closing the letter and adding a snapshot of it. After all that, you still need to push your changes to the remote repository, which is the equivalent of pushing your letter into a mailbox. 
## Creating your First Git Repository

We'll now cover some basic Git commands to get you started and demonstrate the Git workflow.

Create a test directory and `cd` into it: 

```
mkdir testgit && cd testgit
```

Next, initiate an empty git repository:

```
git init
```

You should get output similar to this:

```
Initialized empty Git repository in /home/jason/Documents/dev/testgit/.git
```

All files in this directory are now being tracked by Git. Create a new file so that we can try a commit:

```
echo "Git Crash Course" > readme.txt
```

Now, if you check the **status** of the repository, you'll notice the new `readme.txt` file listed as **untracked**:

```
git status
```

You'll get output like this:

```
On branch main

No commits yet

Untracked files:
  (use "git add <file>... to include what will be committed)
    readme.txt

nothing added to commit but untracked files present (use "git add" to track)
```

As the message suggests, you can add files to be later committed with the `git add` command:

```
git add readme.txt
```

Now, if you run `git status` again, you'll notice that the `readme.txt` file has moved to **staged**, which means it is now part of the changes that should be committed. The output also points out this is a **new** file, with no previous history to Git.

```
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
    new file:   readme.txt
```

To commit changes, you can use the following command, which commits staged files and uses an inline message to identify this commit:

```
git commit -m "first commit"
```

You'll get output similar to this:

```
[main (root-commit) 8e822c2] first commit
 1 file changed, 1 insertion(+)
 create mode 100644 readme.txt
```

Hooray! We just created our first commit. You can check all recent changes in a repository with the `git` log command:

```
git log
```

```
commit 8e822c2c3b8b2872da87c6716f426282bb8a6340 (HEAD -> main)
Author: Erika Heidi <erika@erikaheidi.com>
Date:   Thu Nov 14 19:30:35 2024 +0100

    first commit
(END)
```

To exit the log view, press `q`.

It's worth noting that all these changes are only being tracked locally. There is no remote repository linked, so everything is running on your local machine. If you delete the `testgit` folder, nothing will be saved. In a more real world scenario, you would be running an additional command to push your commit to a remote repository. We'll learn how to do that in a later part of this series.
## Conclusion

In this article, you learned the basics about Git, including how to initialize an empty Git repository, how to stage changes, and how to commit them. In the next part of this series, you'll create a new GitHub account and customize your profile with a profile README.
# Creating and Customizing your Github Profile

Continuing our crash course into Git and Github, we'll now learn more about GitHub and how to establish your presence on this platform, where you can start sharing code and contributing to open source projects.

![](https://i.imgur.com/rwugDQv.png)

[GitHub](https://github.com) is a leading platform for software development and version control, and has revolutionized the way developers collaborate and contribute to open source projects. As a centralized repository for code, GitHub facilitates seamless version tracking, allowing multiple developers to work on a single project simultaneously. Its intuitive interface, branching and merging features, and issue tracking capabilities make it an indispensable tool for developers of all skill levels. Moreover, GitHub fosters a vibrant community for developers to share ideas, learn from one another, and contribute to a vast array of open source projects.

In this guide for beginners, you'll learn how to create a new GitHub account and how to customize your profile.
## Creating a GitHub Account

If you don’t have yet an account on GitHub, now is the time to sign up. Click on the “sign up” button on the top right, and follow the instructions. You’ll need to provide a valid email address, and then choose a username and password.

![](https://i.imgur.com/1svyhXc.png)

After that, you’ll be asked to verify your account by solving a puzzle; this is to make it harder for spam accounts and bad actors to create accounts on the platform. Once you complete the puzzle and verify you’re not a “robot”, you’ll be asked to confirm your email address with a code that was sent to your inbox. After confirming, you should get a message informing you that your account was created successfully, and you can now log in to the platform.

![](https://i.imgur.com/u4JECzN.png)

After logging in, you'll be asked a couple of questions so that GitHub can provide you with a more customized experience.

![](https://i.imgur.com/mlp0cAu.png)

Then, you'll be asked to choose between free and pro. If you are a student, you can also [apply for the GitHub Student Pack](https://docs.github.com/en/education/explore-the-benefits-of-teaching-and-learning-with-github-education/github-education-for-students/apply-to-github-education-as-a-student), which will give you access to pro features for free. You can always start with the free account and upgrade later on.

![](https://i.imgur.com/bCxcmoE.png)

After clicking on “Continue for free”, you will be redirected to your dashboard. From here you can create your first project or start exploring open source projects and repositories.

![](https://i.imgur.com/prE1kkb.png)
## Customizing your Profile

The next step is to customize your profile information. To access the user menu, click on your avatar on the top right of the screen. In this menu, you'll have quick access to all your account settings and resources.

![](https://i.imgur.com/SwLwSUY.png)

To customize your profile, access the "Settings" item from the menu. In this page, you can customize your display name, bio, pronouns, and URLs/links. You can also change your avatar here.

![](https://i.imgur.com/l5HD0AJ.png)

To preview your profile before saving changers, use the "Go to your profile" button on the top right, or go to the user menu and access "Your Profile".
## Creating a README to Further Customize your Profile

If you check your profile now, it will look pretty basic:

![](https://i.imgur.com/XwHehge.png)

You can further customize your profile by creating a profile README, which is a markdown file that must be committed to a special repository with the same name as your username.

The easiest way to create this file is by going back to the **dashboard** at [github.com](http://github.com) and using the shortcut available in your _Home_ section. Click on the “Create” button under “Introduce yourself with a profile README”:

![](https://i.imgur.com/dsRuXRs.png)

You can now use the web editor to fill in your profile information in Markdown format. Use the “preview” button to preview your changes.

![](https://i.imgur.com/Z2C9H3b.png)

Looking for inspiration? Check the [Awesome GitHub Profile Readme](https://github.com/abhisheknaiidu/awesome-github-profile-readme) repository, which contains a curated list of GitHub profiles with nice README customizations that you can use as reference to build your own.

When you are satisfied with your README, click on the “Commit changes” button. A pop-up window will appear where you can customize your commit message.

![](https://i.imgur.com/cCqwS7S.png)

When you click on "Commit changes", the file will be committed to your special repository, and your profile will now render this content automatically. Hooray! You just learned a new way to make commits directly from the GitHub interface.

![](https://i.imgur.com/8s3FbQH.png)

Notice that GitHub automatically created your special repository for you, and it will now be listed within your profile. Whenever you want to change your profile, go to this repository and edit the README.md file in it.
## Conclusion

In this article, you learned how to create your GitHub account, how to customize your profile basic information, and how to create a custom section for it using a profile README.

In the next part of this series, you’ll learn how to pull this special repository into your local machine, so that you can work on your README offline, and then push these changes back to the remote repository.
# Working with Github Repositories

In a previous part of the series, you saw how to create a new GitHub account and how to customize your profile by committing a README file into a special repository. We did all this through GitHub's web interface. In this guide, you'll learn how to work with GitHub repositories by pulling this special repository to your local machine, making changes to your readme, and pushing the changes back to GitHub.
## Creating a New SSH Key

For increased security when working with remote Git repositories, it is recommended to set up an SSH key for communicating with GitHub. If you already have an SSH key set up for your current system user, you can skip to the next step.

You can create a new SSH key by running the following command on your terminal, replacing “[your_email@example.com](https://mailto:your_email@example.com)” with your actual email address:

```
ssh-keygen -t ed25519 -C "jasonkimm12@gmail.com"
```

You will be prompted to provide the location to save your key, and a passphrase. You can use the default location `~/.ssh/id_ed25519`. The passphrase is like a password that adds increased security to your key, so it's not recommended to leave it blank. You will be prompted to provide this passphrase from time to time to unlock your SSH key.

You can verify that the key was created by looking at the `.ssh` directory.

```
ls -la ~/.ssh
```

```
-rw-------  1 erika erika  464 Sep 23 19:48 id_ed25519
-rw-r--r--  1 erika erika  102 Sep 23 19:48 id_ed25519.pub
```

The `id_ed25519.pub` file is the public portion of your SSH key. You'll use the content of this file to set up your SSH key within GitHub. The `id_ed25519` file without extension is the private portion of your SSH key, and should **never be shared**.
## Adding an SSH Key to your GitHub Account

To add your SSH key to your GitHub account, access the menu "SSH and GPG Keys" under settings.

![](https://i.imgur.com/p4lmo1A.png)

Click on the "New SSH Keys" button. On the screen that appears, you'll be asked to provide a title for your key, and the public key contents. Leave the key type as "Authentication Key". If you created your SSH key following the instructions on this guide, this is how you can obtain the contents of the public key:

```
cat ~/.ssh/id_ed25519.pub
```

Copy the full output to the "Key" field.

![](https://i.imgur.com/oJBD1hj.png)

Click on the "Add SSH Key" to confirm.

When the key is added, you are now ready to pull repositories from Github via SSH. 
## Cloning a GitHub Repository

You'll now pull your special GitHub repository to your local system, so that you're able to edit your README offline. Access your GitHub profile and go to your special repository. You can also access your repo directly with the address `https://github.com/your-github-username/your-github-username`.

Click on the green code button, then click on the "SSH" tab under "Clone". Copy the url that starts with `git@` into the text box.

![](https://i.imgur.com/3HweBa0.png)

Then, go to your terminal to clone the repository to your local machine.

```
git clone git@github.com:trop3n/trop3n.git
```

You may be prompted to provide your SSH key passphrase. You should get output similar to this:

```
Cloning into 'boredcatmom'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (3/3), done.
```

Now you can access your repository files directly from a text or code editor or from the terminal.

```
ls trop3n
README.md
```
## Committing and Pushing Your Changes

After making changes you want in your README.md file, it is time to commit your changes and push them back to the remote repository. Let's review the Git workflow with this image. 

![](https://i.imgur.com/Hv4HbYH.png)

This will be similar to what we did in the first article in the series, when we initiated an empty Git repository and committed a file to it. To see the current repository status, run:

```
git status
```

This should indicate that the README.md file was modified, but its not yet staged for commit. To add the file to the commit stage, run:

```
git add README.md
```

Then, commit your changes with:

```
git commit -m "updating readme"
```

Now you can finally push your commit to the remote repository:

```
git push origin main
```

Again, you may be prompted to provide the SSH key passphrase to your SSH keypair. You should get output similar to this:

```
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 1.36 KiB | 1.36 MiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To github.com:boredcatmom/boredcatmom.git
   691417c..26edb28  main -> main
```

Now, if you reload your GitHub profile, it should reflect the changes made to the README.md file.

We just made our first Git push. Now you know how to clone a repository, make changes, and send them back to the remote repository.
## Creating New Repositories and Connecting Existing Repositories to GitHub

Remember the `tesgit` local repository from the first part of the series? That repository was not connected with any remote repo, so there was nowhere to push. Now that you have your GitHub account set up, you can create an empty repository and connect it with your local `testgit` repo. Instead of cloning the remote repo locally, you'll configure your existing local repository to use the GitHub remote repo as **upstream**. In the context of Git and Github, "upstream" or "origin" refers to the *original or main repository from which your local repo was created*, and where changes should be sent. That's why we run `git push origin main` when we want to push changes to the remote main branch.

To test this out, go to your Github dashboard on github.com and click on the + button on the top right, then select "New Repository".

![](https://i.imgur.com/2spOVOd.png)

You'll be redirected to a form to create a new repository. Choose a name for it - it doesn't need to be the same name as your local git repo. Add a description if you want, and leave all the other fields unchecked. Click on the "Create Repository" button when you're ready.

![](https://i.imgur.com/p8flmKh.png)

Once the repo is created, and because it is empty, it will show you information about how to connect this repo with your local Git setup. Grab the repository's SSH URL, we'll need it to configure your local `testgit` repo.

![](https://i.imgur.com/FACf1yO.png)

Then, go to the terminal and access the repo that was previously initialized:

```
cd ~/testgit
```

You'll now run a command that will connect this repo with a remote one that will now be the **origin**

```
git remote add origin git@github.com:trop3n/sandbox.git
```

This command will not give any output. To update the remote repository and set your local repo to track the remote `main` branch as it's *upstream*, run:

```sh
git push -u origin main
```

```sh
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 1.24 KiB | 1.24 MiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:boredcatmom/sandbox.git
 * [new branch]     main -> main
branch 'main' set up to track 'origin/main'.
```

If you reload your repository page on Github, it should now have a single `readme.txt` file that says "Git Crash Course". You effectively copied you local repo and all its history to the brand-new repo that was created.
## Conclusion

In this article, you learned how to clone repositories and push your changes back to GitHub, and you also learned how to connect a local git repository to a remote GitHub repository.

In the next part of this series, we’ll learn about Git branches and how to collaborate with other developers and work together in the same repository.
# Working with Git Branches and Pull Requests
## Git Branches Overview

Git branches are an essential feature of Git version control. THey allow developers to work on different versions of a project simultaneously without affecting the main branch. Branches also enable multiple developers to work on the same project without interfering with each other's work. By creating a branch for a task or feature, developers can work independently and merge their changes into the main branch when they're ready. Branches also facilitate tracking changes and reverting to the previous versions of the code if necessary.

![](https://i.imgur.com/ZTnBOGv.jpeg)

So far, we have only worked on the `main` branch. It is a convention to use `main` as the default branch where most up-to-date version of a project can be found. Active development typically occurs in separate branches that are later merged into `main`. Software releases are also typically based on the main branch, although it is possible to maintain several branches with different versions of software. 
## The Pull Request Workflow

In the previous chapter of this series, you cloned a remote Git repository, made changes, and pushed the changes back directly into the `main` branch. In a collaborative workflow, you would be making changes to a separate branch (for example, `readme-updates`), then push this to the remote repository, and then open a **pull-request** (**PR** for short) to request that your `readme-updates` branch be pulled or merged into main. Another collaborator would then be able to review your pull request before the changes are merged. Github offers several tools and even AI assistance for pull request reviews, which can be very helpful when working with teams.

If you are just starting and working solo on a project, you might wonder why you should care about pull requests at all. Here's why practicing this workflow is advantageous for beginners:

- Better Understanding of how branches and merging work
- Preparation for contributing code to existing projects
- Familiarization with the process of reviewing and approving pull requests

Undoubtedly, GitHub stands as the preeminent code platform in the market, making it imperative for you to acquaint yourself with its workflows and diverse features. It's very likely that you'll need to use this platform eventually, either for work or for academic purposes. So starting early might give you an advantage others don't have.
## Creating your First Pull Request

We'll now repeat what we did in the previous article, where we pushed some changes to your profile README directly from your local machine. This time around, however, we'll work on a separate branch, and push this branch over to upstream. Then, you'll open a pull request to learn how that works.

If for some reason you don't have the project on your local machine, start by cloning the repo. You can obtain the SSH URL for the repository in its GitHub landing page by clicking on the green "Code" button. The URL follows this pattern: `git@github.com:username/repo.git`. Once you grab that URL, run `git clone` from your home directory and then `cd` into the newly created folder.

```sh
git clone git@github.com:boredcatmom/boredcatmom.git
cd boredcatmom
```

If you've followed along with the previous guides, you should have a single `README.md` file in your repository. You'll now create a new branch based off of `main` before you start making changes to your file. To do so, run the following command:

```
git checkout -b readme-updates
```

```
Switched to a new branch 'readme-updates'
```

The `git checkout` command is used to *switch between branches*. To create a new branch, use the `-b` parameter. If the branch already exists, use just `git checkout branch-name` to make the switch.

Now make some changes to the file. When you're finished, proceed with the workflow of adding files to staging and committing changes:

```sh
git add README.md
git commit -m "updated"
```

```sh
[readme-updates 8c8f620] updted
 1 file changed, 1 insertion(+), 1 deletion(-)
```

Now, push the changes to upstream. Instead of pushing to main, though, you'll be pushing it to a branch with the same name as your local branch:

```sh
git push origin readme-updates
```

You'll get output similar to this:

```sh
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 1.31 KiB | 1.31 MiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
remote:
remote: Create a pull request for 'readme-updates' on GitHub by visiting:
remote:     https://github.com/boredcatmom/boredcatmom/pull/new/readme-updates
remote:
To github.com:boredcatmom/boredcatmom.git
 * [new branch]     readme-updates -> readme-updates
```

As you can notice from the output, there's a special URL you can access to create a pull request based on this branch. You can also simply access your repository page on GitHub and a prominent dialog will appear asking if you want to create a pull request based on the new branch that was just pushed:

![](https://i.imgur.com/maJLITC.png)

Click on the "Compare & pull request" button to open the pull request form. You'll see a page similar to this:

![](https://i.imgur.com/aEtuOkS.png)

The select box on the top of the screen lets you select the source branch and the target branch for the pull request. Typically you won't need to change this. The PR From uses your commit message as title, and has a text area for you to describe the changes you are proposing and adding any relevant information to help test and review the pull request. 

The bottom area of the pull request form shows a **diff** view of what has changed in this branch when compared to `main`. Red-highlighted lines are removed lines, and green-highlighted lines are new additions to the file. 

Click on the green "Create Pull Request" button to create the PR. You'll be redirected to the newly created pull request page:

![](https://i.imgur.com/FwBXGWa.png)
Congrats, you have created your first pull request.
## Reviewing a Pull Request

The process of reviewing a pull request varies greatly depending on the project, company, and/or team. In general, you'll be looking at the **Files Changed** tab of the pull request page, where you'll be able to find all the changed files with a rich diff that enables you to quickly visualize what was changed in that PR.

The Github interface allows for directly making comments and suggestions in the "Files Changed" tab. Click on the blue `+` sign that shows up on each line (when you hover your mouse over that little space between the line number and the beginning of the line) to open the comments / suggestions form:

![](https://i.imgur.com/nryvxKz.png)

To approve or request changes to a PR, click on the green "Review Changes" button on the top right to access the PR approval form. Because PR authors cannot approve their own pull requests, you won't be able to use the form to review your own PR, as you can merge it directly to `main` when you're ready.

![](https://i.imgur.com/77lKoV5.png)
## Merging a Pull Request

When the PR is good to merge and there are no issues such as conflicting changes, you can click on the green "Merge pull request" button, and Github will merge the pull request into your main branch.

![](https://i.imgur.com/DWOsEOS.jpeg)
## Updating your Local Repository

When pull requests are merged through the Github interface, a new commit is created in the `main` branch carrying the changes that were merged. Your local copy of the repository will be outdated, with the `main` branch still pointing to a previous commit.

Start by switching to the main branch:

```
git checkout main
```

To pull the changes and update your local `main` branch, run:

```
git pull origin main
```

This will make sure any additional changes made from other authors or directly from the Github interface are pulled into your local repository. You should get output similar to this:

```sh
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (1/1), 885 bytes | 885.00 KiB/s, done.
From github.com:boredcatmom/boredcatmom
 * branch           main    -> FETCH_HEAD
   26edb28..d42543d  main       -> origin/main
Updating 26edb28..d42543d
Fast-forward
 README.md | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

If you run `git log` now, you should be able to confirm that your local `main` branch now points to the commit that merged the pull request from the `readme-updates` branch:

```sh
commit d42543de4d1ed7ec2c96c35500986ac882b94f3d (HEAD -> main, origin/main, origin/HEAD)
Merge: 26edb28 8c8f620
Author: boredcatmom <boredcatmom@hotmail.com>
Date:   Tue Nov 19 15:20:33 2024 +0100

    Merge pull request #1 from boredcatmom/readme-updates

    Updated
```

It's important to keep your main branch always up-to-date with your upstream, in order to avoid merge conflicts and other issues. 
## Sending PR to Other People's Projects

When working on other people's projects on platforms like Github, you'll often need to fork the repository to your account before you can make changes. This is because you don't have direct **write** access to the original repository.

Forking a repository creates a copy of the original repository in your account. You can then make changes to your forked repository without affecting the original. Once you're finished making changes, you can submit a pull request to the original repository. This will notify the original repo owner that you have changes that you'd like them to consider merging into their repository.

For more information about forking repositories: [GitHub documentation](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo).
## Appendix: Merge Conflicts and Common Mistakes

Despite it's seemingly simple commands, Git can be quite tricky at times. Its complexity stems from the intricate web of branches, commits, and merges that it manages. Let's review common issues in this short appendix.
### Merge Conflicts

A merge conflict occurs when you try to merge two branches that have conflicting changes to the same file. This can happen when multiple developers are working on the same file at the same time and make changes that overlap. Although slightly annoying, merge conflicts are a very common occurrence in Git world, so it's nothing to be scared of.

When a merge conflict occurs, Git will stop the merge process and display a message indicating which files have conflicts. You will need to resolve the conflicts manually before you can continue with the merge. Merge conflicts also prevent maintainers from using the GitHub interface to merge pull requests, requiring manual intervention. 

Git adds special markers on conflicting files so that you can identify the differences and choose which version you'll keep. After you're finished with the changes, you can continue with the merge process.

Please refer to the official [GitHub Documentation](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/about-merge-conflicts) for detailed resources to assist with merge conflicts.
### Common Mistakes when Working with Git

We all have done it before, and we may still do it again sometimes. These common mistakes can cause issues such as merge conflicts, data inconsistency, or increased security risks.

- **Pushing to the wrong branch**: if you try to push your local branch to a remote branch that doesn't match your history, you'll likely get a write error message, or you may end up with several merge conflicts. 
- **Forgetting to add files to the staging area**: you can only crate a commit if you have files in staging. Also, be mindful of what you're adding to the repository. You can use a `.gitignore` file to add files that should be ignored.
- **Accidentally deleting or overwriting files**: it may happen that you delete a local file by mistake and accidentally commit that change to the repo. That's why it's important to pay attention to what's in stage before creating your commits.
- **Accidentally committing files with sensitive information**: this can pose a serious security risk to a project or user. Files with sensitive information such as passwords and tokens should never be committed to the repository. Add any files with sensitive data to your `.gitignore`. 
- **Pushing local changes without pulling remote changes first**: the most likely outcome of pushing local changes without pulling updates first is a merge conflict. Always remember to update your branches before pushing to origin. 
- **Forgetting to push changes to the remote repository**: sometimes we just forget to hit that final push and send the changes to the repository. Not a big deal, but a very common thing to happen.
## Conclusion

In this guide, you learned about branches and the mighty Pull Request workflow. Hooray! You have now the basic tools to start building on GitHub, and to start contributing to open source projects, if that’s something you’re interested in. Coding can definitely be more fun with friends, and luckily for us, GitHub is an excellent platform to build projects together just like that.

With that, our Git and GitHub Crash Course comes to an end. Here are some resources you may refer to if you want to learn more about Git and GitHub:

- [GitHub Official Documentation](https://docs.github.com/en)
- [Git Official Documentation](https://git-scm.com/doc)
- [Learn Git Branching](https://learngitbranching.js.org/)
