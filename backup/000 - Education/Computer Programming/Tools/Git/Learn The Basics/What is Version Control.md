#git #github #versioncontrol #devops
# What is Version Control
https://www.atlassian.com/git/tutorials/what-is-version-control

Version control, also known as source control, is the practice of tracking and managing changes to software code. Version control systems are software tools that help software teams manage changes to source code over time. As development environments have accelerated, version control systems help software teams work faster and smarter. They are especially useful for [DevOps](https://www.atlassian.com/devops/what-is-devops) teams since they help them to reduce development time and increase successful deployments.

Version control software keeps track of every modification to the code in a special kind of database. If a mistake is made, developers can turn back the clock and compare earlier versions of the code to help fix the mistake while minimizing disruption to all team members. 

For almost all software projects, the source doe is like the crown jewels - a precious asset whose value must be protected. For most software teams, the source code is a repository of the invaluable knowledge and understanding about the problem domain that the developers have collected and refined though careful effort. Version control projects source code from both catastrophe and the casual degradation of human error and unintended consequences. 

Software developers working in teams are continually writing new source code and changing existing source code. The code for a project, app or software component is typically organized in a folder structure or "file tree". One developer on the team may be working on a new feature while another developer fixes and unrelated bug by changing code, each developer may make their changes in several parts of the file tree.

Version control helps teams solves these kinds of problems, tracking every individual change by each contributor and helping prevent concurrent work from conflicting. Changes made in one part of the software can be incompatible with those made by another developer and solved in an orderly manner without blocking the work of the rest of the team. Further, in all software development, any change can introduce new bugs on its own and new software can't be trusted until it's tested. So testing and development process proceed together until a new version is ready.

Good version control software supports a developer's preferred workflow without imposing one particular way of working. Ideally it also works on any platform, rather than dictate what operating system or tool chain developers must use.  Great version control systems facilitate a smooth and continuous flow of changes to the code rather than the frustrating and clumsy mechanism of file-locking - giving the green light to one developer at the expense of blocking the progress of others.

Software teams that do not use any form of version control often run into problems like not knowing which changes that have been made are available to users or the creation of incompatible changes between two unrelated pieces of work  that must then be painstakingly untangled and reworked. If you're a developer who has never used version control you may have added versions to your files, perhaps with suffixes like "final" or "latest" and then had to later deal with a new final version. Perhaps you've commented out code blocks because you want to disable certain functionality without deleting the code, fearing that there may be a use for it later. Version control is a way out of these problems. 

Version control software is an essential part of the every-day of the modern software team's professional practices. Individual software developers who are accustomed to working with a capable version control system in their teams typically recognize the incredible value version control also gives them even on small solo projects. Once accustomed to the powerful benefits of version control systems, many developers wouldn't consider working without it even for non-software projects.

## Benefits of version control systems

---
Using version control software is a best practice for high performing software and [DevOps](https://www.atlassian.com/devops/what-is-devops) teams. Version control also helps developers move faster and allows software teams to preserve efficiency and agility as the team scales to include more developers.

Version Control Systems (VCS) have seen great improvements over the past few decades and some are better than others. VCS are sometimes known as SCM (Source Code Management) tools or RCS (Revision Control System). One of the most popular VCS tools in use today is called Git. Git is a _Distributed_ VCS, a category known as DVCS, more on that later. Like many of the most popular VCS systems available today, Git is free and open source. Regardless of what they are called, or which system is used, the primary benefits you should expect from version control are as follows.

1. A complete long-term change history of every file. This means every change made by many individuals over the years. Changes include the creation and deletion of files as well as edits to their contents. Different VCS tools differ on how well they handle renaming and moving of files. This history should also include the author, date and written notes on the purpose of each change. Having the complete history enables going back to previous versions to help in root cause analysis for bugs and it is crucial when needing to fix problems in older versions of software. If the software is being actively worked on, almost everything can be considered an "older version" of the software.

2. Branching and merging. Having team members work concurrently is a no-brainer, but even individuals working on their own can benefit from the ability to work on independent streams of changes. Creating a "branch" in VCS tools keeps multiple streams of work independent from each other while also providing the facility to merge that work back together, enabling developers to verify that the changes on each branch do not conflict. Many software teams adopt a practice of branching for each feature or perhaps branching for each release, or both. There are many different workflows that teams can choose from when they decide how to make use of branching and merging facilities in VCS.

3. Traceability. Being able to trace each change made to the software and connect it to project management and [bug tracking software](https://www.atlassian.com/software/jira/features/bug-tracking) such as [Jira](https://www.atlassian.com/software/jira), and being able to annotate each change with a message describing the purpose and intent of the change can help not only with root cause analysis and other forensics. Having the annotated history of the code at your fingertips when you are reading the code, trying to understand what it is doing and why it is so designed can enable developers to make correct and harmonious changes that are in accord with the intended long-term design of the system. This can be especially important for working effectively with legacy code and is crucial in enabling developers to estimate future work with any accuracy.

While it is possible to develop software without using any version control, doing so subjects the project to a huge risk that no professional team would be advised to accept. So the question is not whether to use version control but which version control system to use.

There are many choices, but here we are going to focus on just one, Git. Learn more about other types of [version control software](https://bitbucket.org/product/version-control-software).
# Source Code Management

Source Code Management (SCM) is used to track modifications to a source code repository. SCM tracks a running history of changes to a code base and helps resolve conflicts when merging updates from multiple contributors.. SCM is also synonymous with Version control. 

As software projects grow in lines of code and contributor head count, the costs of communication overhead and management complexity also grows. SCM is a critical tool to alleviate the organization strain of growing development costs.

---
## The Importance of Source Code Management Tools

When multiple developers are working within a shared codebase it is a common occurrence to make edits to a shared piece of code. Separate developers may be working on a seemingly isolated feature, however this feature may use a shared code module. Therefore developer one working on Feature 1 could make some edits and find out later that Developer 2 working on feature 2 has conflicting edits.

Before the adopting of SCM this was a nightmare scenario. Developers would edit text files directly and move them around to remote locations using FTP or other protocols. Developer 1 would make edits and Developer 2 would unknowingly save over Developer 1's work and wipe out the changes. SCM's role as a protection mechanism against this specific scenario is known as [Version Control](https://www.atlassian.com/git/tutorials/what-is-version-control).

SCM brought version control safeguards to prevent loss of work due to conflict overwriting. These safeguards work by tracking changes from each individual developer and identifying areas of conflict and preventing overwrites. SCM will then communicate these points of conflict back to the developers so that they can safely review and address.

The foundational conflict prevention mechanism has the side effect of providing passive communication for the development team. The team can then monitor and discuss the work in progress that the SCM is monitoring. The SCM tracks an entire history of changes to the code base. This allows developers to examine and review edits that may have introduced bugs or regressions.
## The Benefits of Source Code Management

In addition to version control SCM provides a suite of other helpful features to make collaborative cod development a more use friendly experience. Once SCM has started tracking all the changes to a project over time, a detailed historical record of the projects life is created. This historical record can then be used to [‘undo’ changes](https://www.atlassian.com/git/tutorials/undoing-changes) to the codebase. The SCM can instantly revert the codebase back to a previous point in time. This is extremely valuable for preventing regressions on updates and undoing mistakes.

The SCM archive of every change over a project's life time provides valuable record keeping for a project's release version notes. A clean and maintained SCM history log can be used interchangeably as release notes. This offers insight and transparency into the progress of a project that can be shared with end users or non-development teams. 

SCM will reduce a teams communication overhead and increase release velocity. Without SCM development is slower because contributors have to take extra effort to plan a non-overlapping sequence to develop for release. With SCM developers can work together independently on separate branches of feature development, eventually merging them together. 

Overall SCM is a huge aid to engineering teams that will lower development costs by allowing engineering resources to execute more efficiently. SCM is a must have in the modern age of software development. [Professional teams use version control](https://bitbucket.org/product/version-control-software) and your team should too.
## Source Code Management Best Practices
### Commit Often

Commits are cheap and easy to make. They should be made frequently to capture updates to a code base. Each commit is a snapshot that the code base can be reverted to if needed. Frequent commits give many opportunities to revert or undo work. A group of commits can be combined into a single commit using a rebase to clarify the development log. 
### Ensure You're Working from the Latest Version

SCM enables rapid updates from multiple developers. It's easy to have a local copy of the codebase fall behind the global copy. Make sure to [git pull](https://www.atlassian.com/git/tutorials/syncing/git-pull) or fetch the latest code before making updates. This will help avoid conflicts at merge time.
### Make Detailed Notes

Each commit has a corresponding log entry. At the time of commit creation, this log entry is populated with a message. It is important to leave descriptive explanatory commit log messages. These commit log messages become the canonical history of the project's development and leave a trail for future contributors to review.
### Review Changes Before Committing

SCM's offer a 'staging area'. The staging area can be used to collect a group of edits before writing them to a commit. The staging area can be used to manage and review changes before creating the commit snapshot. Utilizing the staging area in this manner provides a buffer area to help refine the contents of the commit.
### Use Branches

Branching is a powerful SCM mechanism that allows developers to create a separate line of development. Branches should be used frequently as they are quick and inexpensive. Branches enable multiple developers to work in parallel in separate lines of development. These lines of development are generally different product features. When development is complete on a branch it is then merged into the main line of development.
### Agree on a Workflow

By default SCMs offer very free form methods of contribution. It is important that teams establish shared patterns of collaboration. SCM workflows establish patterns and processes for merging branches. If a team doesn't agree on a shared workflow it can lead to inefficient communication overhead with it comes time to merge branches. 
## Summary

---

SCM is an invaluable tool for modern software development. The best software teams use SCM and your team should too. SCM is very easy to set up on a new project and the return on investment is high. Atlassian offers some of [the best SCM integration tools in the world](https://bitbucket.org/product) that will help you get started.
# What is Git?

By far, the most widely used modern version control system in the world today is Git. Git is a mature, actively maintained open source project originally developed in 2005 by Linus Torvalds, the famous creator of the Linux operating system kernel.

A staggering number of software projects rely on Git for version control, including commercial projects as well as open source. Developers who have worked with Git are well represented in the pool of available software development talent and it works well on a range of operating systems and IDEs (Integrated Development Environments).

Having a distributed architecture, Git is an example of a DVCS (hence Distributed Version Control System). Rather than have only one single place for the full version history of the software as is common in once-popular version control systems like CVS or Subversion (also known as SVN), in Git, every developer's working copy of the code is also a repository that can contain the full history of all changes.

In addition to being distributed, Git has been designed with performance, security and flexibility in mind.

---
## Performance

The raw performance characteristics of Git are very strong when compared to many alternatives. Committing new changes, branching, merging and comparing past versions are all optimized for performance. The algorithms implemented inside Git take advantage of deep knowledge about common attributes of real source code file trees, how they are usually modified over time and what the access patterns are.

Unlike some version control software, Git is not fooled by the names of the files when determining what the storage and version history of the file tree should be, instead Git focuses on the file content itself. After all, source code files are frequently renamed, split and rearranged. The object format of Git's repository files uses a combination of delta encoding (storing content differences), compression and explicitly stores directory contents and version metadata objects. 

Being distributed enables significant performance benefits as well.

For example, say a developer, Alice, makes changes to source code, adding a feature for the upcoming 2.0 release, then commits those changes with descriptive messages. She then works on a second feature and commits those changes too. Naturally these are stored as separate pieces of work in the version history. Alice then switches to the version 1.3 branch of the same software to fix a bug that affects only that older version. The purpose of this is to enable Alice's team to ship a bug fix release, version 1.3.1, before version 2.0 is ready. Alice can then return to the 2.0 branch to continue working on new features 2.0 and all of this can occur without any network access and is therefore fast and reliable. She could even do it on an airplane. When she is ready to send all of the individually committed changes to remote repository, Alice can "push" them in one command.
## Security

Git has been designed with the integrity of managed source code as a top priority. The content of the files as well as the true relationships between files and directories, versions, tags and commits, all of these objects in the Git repository are secured with a cryptographically secure hashing algorithm called SHA1. This protects the code and the change history against both accidental and malicious change and ensures this the history is full traceable. 

With Git, you can be sure you have an authentic content history of your source code.

Some other version control systems have no protections against secret altercation at a later data. This can be a serious information security vulnerability for any organization that relies on software development.
## Flexibility

One of Git's key design is flexibility. Git is flexible in several respects: in support for various kinds of nonlinear development workflows, in its efficiency in both small and large projects and in its compatibility with many existing systems and protocols. 

Git has been designed to support branching and tagging as first-class citizens (unlike SVN) and operations that affect branches and tags (such as merging or reverting) are also stored as part of the change history. Not all version control systems feature this level of tracking.
## Version Control with Git

Git is the best choice for most software teams today. While every team is different and should do their own analysis, here are the main reasons why version control with Git is preferred over alternatives:
### Git is Good

Git has the functionality, performance, security and flexibility that most teams and individual developers need. These attributes of Git are detailed above. In side-by-side comparisons with most other alternatives, many teams find Git is very favorable.
### Git is a De Facto Standard

Git is the most broadly adopted tool of its kind. This makes Git attractive for the following reasons. At Atlassian, nearly all of our projects source code is managed in Git.

Vast numbers of developers already have Git experience and a significant proportion of college graduates may have experience with only Git. While some organizations may need to climb the learning curve when migrating to Git from another version control system, many of their existing and future developers do not need to be trained on Git.

In addition to the benefits of a large talent pool, the predominance of Git also means that many third part software tools and services are already integrated with Git including IDEs, and our own tools like DVCS desktop client [Sourcetree](http://www.sourcetreeapp.com/), issue and project tracking software, [Jira](https://www.atlassian.com/software/jira), and code hosting service, [Bitbucket](https://bitbucket.org/product).

If you are an experienced develop wanting to build up valuable skills in software development tools, when it comes to version control, Git should be on your list.
### Git is a Quality Open Source Project

Git is a very well supported open source project with over a decade of solid stewardship. The project maintainers have shown balanced judgment and a mature approach to meeting the long term needs of its users with regular releases that improve usability and functionality. The quality of the open source software is easily scrutinized and countless businesses rely heavily on that quality. 

Git enjoys great community support and a vast user base. Documentation is excellent and plentiful including books, tutorials and dedicated web sites. There are also podcasts and video tutorials. 

Being open source lowers the cost for hobbyist developers as they can use Git without paying a fee. For use in open-source projects, Git is undoubtedly the successor to the previous genertions of successful open source version control systems, SVN and CVS.
### Criticisms of Git

One common criticism of Git is that it can be difficult to learn. Some of the terminology in Git will be novel to newcomers and for users of other systems, the Git terminology may be different, for example, `revert` in Git has a different meaning than in SVN or CVS. Nevertheless, Git is very capable and provides a lot of power to its users. Learning to use that power can take some time, however once it has been learned, that power can be used by the team to increase their development speed.

For those teams coming from a non-distributed VCS, having a central repository may seem like a good thing that they don't want to lose. However, while Git has been designed as a distributed version control system (DVCS), with Git, you can still have an official, canonical repository where all changes to the software must be stored. With Git, because each developer's repository is complete, their work doesn't need to be constrained by the availability and performance of the "central" server. During outages or while offline, developers can still consult the full project history. 

Because Git is flexible as well as being distributed, you can work the way you are accustomed to but gain the additional benefits of Git, some of which you may not even realize you're missing.

Now that you understand what version control is, what Git is and why software teams should use it, [read on to discover the benefits](https://www.atlassian.com/git/tutorials/why-git) Git can provide across the whole organization.
# Git SSH

An SSH key is an access credential for the SSH (secure shell) network protocol. This authenticated and encrypted secure network protocol is used for remote communication between machines on an [unsecured open network](https://whatismyipaddress.com/unsecured-network). SSH is used for remote file transfer, network management, and remote operating system access. The SSH acronym is also used to descibe a set of tools used to interact with the SSH protocol.

SSH uses a pair of keys to initiate a secure handshake between remote parties. The key pair contains a public and private key. The private vs. public nomenclature can be confusing as they are both called keys. It is more helpful to think of the public key as a "lock" and the private key as the "key". You give the public 'lock' to remote parties to encrypt or 'lock' data. This data is then opened with the 'private' key which you hold in a secure place.

---
## How to Create an SSH Key

SSH keys are generated through a [public key cryptographic algorithm](https://en.wikipedia.org/wiki/Public-key_cryptography), the most common being [RSA](https://en.wikipedia.org/wiki/RSA_(cryptosystem)) or [DSA](https://en.wikipedia.org/wiki/Digital_Signature_Algorithm). At a very high level SSH keys are generated through a mathematical formula that takes 2 prime numbers and a random seed variable to output the public and private key. This is a one-way formula that ensures the public key can be derived from the private key but the private key cannot be derived from the public key.

SSH keys are created using a key generation tool. The SSH command line tool suite includes a keygen tool. Most git hosting providers offer guide on [how to create an SSH Key.](https://confluence.atlassian.com/bitbucketserver/creating-ssh-keys-776639788.html)
## Generate an SSH Key on Mac and Linux

Both OSX and Linux operating systems have comprehensive modern terminal applications that ship with the SSH suite installed. The process for creating an SSH key is the same between them.

1. Execute the following to begin the key creation.

```css
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

This command will create a new SSH key using the email as a label

2. You will then be prompted to "Enter a file in which to save the key." You can specify a file location or press "Enter" to accept the default file location.

```bash
> Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]
```

3. The next prompt will ask for a secure passphrase. A passphrase will add an additional layer of security to the SSH and will be required anytime the SSH key is used. If someone gains access to the computer that private keys are stored on, they could also gain access to any system that uses that key. Adding a passphrase to keys will prevent this scenario.

```scss
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]
```

At this point, a new SSH key will have been generated at the previously specified file path.

4. Add the new SSH key to the ssh-agent

The ssh-agent is another program that is part of the SSH toolsuite. The ssh-agent is responsible for holding private keys. Think of it like a keychain. In addition to holding private keys it also brokers requests to sign SSH request with the private keys so that private keys are never passed around unsecurely.

Before adding the new SSH key to the ssh-agent first ensure the ssh-agent is running by executing:

```bash
$ eval "$(ssh-agent -s)"
> Agent pid 59566
```

Once the ssh-agent is running the following command will add the new SSH key to the local SSH agent. 

```bash
ssh-add -K /Users/you/.ssh/id_rsa
```

The new SSH key is now registered and ready to use!
# Git Archive







