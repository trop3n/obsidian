#git #github #versioncontrol 
# Benefits of Version Control
https://www.techrepublic.com/article/version-control-benefits/

**We take a deep dive into the benefits of version control and version control systems**.

Version control, also known as source control, is the practice of tracking and managing changes to software code. It has become indispensible to software teams in recent years as rapid development practices such as Agile have introduced increasingly short software iteration schedules. With both the rapidity and number of code changes taking place within the average iteration cycle, version control is best achieved utilizing specialized version software called version control systems (VCS). Judicious use of version control systems have been shown to help software teams work faster and smarter, resulting in reduced development time and increased successful deployments. 
## Tracking Code Changes

The main point of any version control system is to track changes in files and code over time. This is achieved by keeping an **extensive history** of all activity on a collection of code (called a repository). The various development streams are stored as **branches** and each update is marked as a **commit**. Many modern VCSes are GUI-based, making it very easy to compare the changes, by showing the exact lines of code where modifications were done. If things go astray, it is easy to revert to earlier changes.

Here is a screen capture of one such version control system called [Gitkraken](https://www.gitkraken.com/):

![](https://i.imgur.com/suvxI9W.png)

Gitkraken features an easy-to-read commit graph that helps visualize branch structure and commit history. It not only helps verify your recent Git actions on the repo, but also shows which developers and programmers made what code changes and when, so it is easy to track down when a bug was introduced and revert back to a previous version if need be. 
## Traceability

As mentioned in the last point, good version control software not only tracks changes to the code, but also shows who made what code changes and when. As such, the software tracks changes from the original copy through the many subsequent versions, and finally, to the final version.

Being able to trace each change to the code allows teams to connect it to [project management tools](https://www.techrepublic.com/article/project-management-software/) and bug tracking software such as [Jira](https://www.techrepublic.com/article/jira-review/). Each and every code change may be associated to a message describing the purpose and intent of the change, which can greatly help with root cause analysis and other forensics. You can see the commit messages in the above screenshot to the right of the branches. 

A side effect of having a record of all the changes made to a particular code file is that new contributors tend to find it easier to comprehend how a specific code section came into being. This allows developers to work more efficiently with historical code and also predict future enhancements with greater accuracy.
## Streamlined Branching and Merging

Branching and merging are features of just about all modern version control systems. A **branch** is a version of the repository that diverges from the main working project, while the action of creating new branch is called **branching**. Branching allows developers to diverge from the production version of code to fix a bug or add a feature. Developers create branches to work with a copy of the code without modifying the existing version. They can then work on their isolated code base to make changes, test the updated code, and then merge their changes back into the main branch.

Creating a branch in VCS tools keep multiple streams of work independent from each other while also providing the facility to merge that work back together in such a way as to avoid conflicts that might break existing code. There are many different workflows that teams can adopt to make use of branching and merging facilities in version control tools. Some software teams choose to create a new branch for each feature while others create branches for each team member. The possibilities are virtually endless.
## Code Experimentation

It is quite common when working on a software project for teams to create a clone of the main project to experiment with new features. When doing so, it is vital that developers are able to test their changes and ensure that they work before merging this new feature back into the main project branch. The practice of trying something out in software development is known as a **spike**. Whether you work within a software development team or on your own, having the ability to isolate your experimental code within its own branch can be highly advantageous.
## Managing and Protecting the Source Code

Using a version control system ensures that programmers always have all the versions of your source code at your disposal. It also protects the source code from any unintended human error by placing restrictions on who can commit to the main branch and under what circumstances. For example, the organization can choose for force new code to undergo a code review before it can be merged into the master branch. That way, any suspect code can be weeded our before becoming part of the main code base.
## Final Thoughts on Benefits of Version Control

While it is possible to develop software without using any version control, doing so could subject projects to a huge risk that no professional organization would be willing to accept. With that in mind, make it a priority to learn all about version control systems, including how they work and how to use them efficiently.



