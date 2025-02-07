---
up: "[[000 - Education/Cybersecurity/Bug Bounty/Bug Bounty|Bug Bounty]]"
tags:
  - education/books/bugbounty/bugbountybootcamp
description: Notes for the book "Bug Bounty Bootcamp"
source: "[[Bug Bounty Bootcamp - NSP.pdf]]"
---

# Foreword

Twenty or even ten years ago, hackers like me were arrested for trying to do good. Today, we are being hired by some of the world's most powerful organizations.

If you're still considering whether or not you are late to the bug bounty train, know that you're coming aboard at one of the most exciting times in the industry's history. This community is growing faster than ever before, as governments are beginning to require that companies host vulnerbaility disclosure programs, Fortune 500 companies are building such policies in droves, and the applications for hacker-powered security are expanding every day. The value of a human eye will forever be vital in defending against evolving threats, and the world is recognizing us as the people to provide it. 

The beautiful thing about the bug bounty world is that, unlike your typical nine-to-five job or consultancy gig, it allows you to participate from wherever you want, whenever you want, and on whatever types of asset you like. All you need is a decent internet connection, a nice coffee (or your choice of beverage), some curiosity and a passion to break things. And not only does it give you the freedom to work on your own schedule, but the threats are evolving faster than the speed of innovation, providing ample opportunities to learn, build your skills, and become an expert in a new area.

If you are interested in gaining real world hacking experience, the bug bounty marketplace makes that possible by providing an endless number of targets owned by giant companies like Facebook, Google or Apple. 
	I'm not saying it's an easy task to find a vulnerability in these companies; nevertheless, bug bounty programs deliver the platform on which to hunt, and the bug bounty community pushes you to learn more about new vulnerability types, grow your skill set, and keep trying even when it gets tough. 

Unlike most labs and CTFs, bug bounty programs do not have solutions or a guaranteed vulnerability to exploit. Instead, you'll always ask yourself whether or not some feature is vulnerable, or if it can force the application or its functionalities to do things it's not supposed to. This uncertainty can be daunting, but it makes the thrill of finding a bug so much sweeter. 

In this book, Vickie explores a variety of different vulnerability types to advance you understanding of web application hacking. She covers the skills that will make you a successful bug bounty hunter, including step-by-step analyses on how to pick the right program for you, perform proper reconnaissance, and write strong reports. She provides explanations for attacks like XSS, SQL Injection, template injection, and almost any other you need in your toolkit to be successful. Later on, she takes you beyond the basics of web applications and introduces topics such as code review, API hacking, automating your workflow, and fuzzing.
# Introduction

Hackers are probably the closest thing to superheroes I've encountered in the real world. They overcome limitations with their skills to make software programs do much more than they were designed for, which is what I love about hacking web applications: it's all about thinking creatively, challenging yourself, and doing more than what seems possible. 

Also like superpowers, ethical hackers help keep society safe. Thousands of data breaches happen every year in the United States alone. By understanding vulnerabilities and how they happen, you can use your knowledge for good to help prevent malicious attacks, protect applications and users, and make the internet a safer place.

Not too long ago, hacking and experimenting with web applications was illegal. But now, thanks to bug bounty programs, you can hack legally; companies set up bug bounty programs to reward security researchers for finding vulnerabilities in their applications. *Bug Bounty Bootcamp* teaches you how to hack web applications and how to do it legally by participating in these programs. 
## Who this Book is For

This book will help anyone learn web hacking and bug bounty hunting from scratch. You might be a student looking to get into web security, a web developer who wants to understand the security of a website, or an experienced hacker who wants to understand how to attack web applications. If you are curious about web hacking and web security, this book is for you. No technical background is needed to understand and master the material of this book. However, you will find it useful to understand basic programming. Although this book was written with beginners in mind, advanced hackers may also find it to be a useful reference. In particular, I discuss advanced exploitation techniques and useful tips and tricks I’ve learned along the way.
## What is in This Book

*Bug Bounty Bootcamp* covers everything you need to start hacking web applications and participating in bug bounty programs. This book is broken into four parts: The Industry, Getting Started, Web Vulnerabilities, and Expert Techniques
### Part I: The Industry

The first part of the book focuses on the bug bounty industry. 
### Part II: Getting Started

The second part of the book prepares you for web hacking and introduces you to the basic technologies and tools you'll need to successfully hunt for bugs. 
### Part III: Web Vulnerabilities

Then we start hacking. This part, the core of the book, dives into the details and specifics of vulnerabilities. Each chapter is dedicated to a vulnerability and explains what causes that vulnerability, how to prevent it, and how to find, exploit and escalate it for maximum impact.
### Part IV: Expert Techniques

The final part of the book introduces in-depth techniques for the experienced hacker. This section will help you advance your skills once you understand the basics covered in Part III.
# Part I: The Industry

## Chapter 1: Picking a Bug Bounty Program

Bug bounty programs: are they all the same? Finding the right program to target is the first step to becoming a successful bug bounty hunter. Many programs have emerged within the past few years, and it's difficult to figure out which ones will provide the best monetary rewards, experience, and learning opportunities.

A *bug bounty program* is an initiative in which a company invites hackers to attack its products and service offerings. But how should you pick a program? And how should you prioritize their different metrics, such as the asset types involved, whether the program is hosted on a platform, whether it's public or private, the program's scope, the payout amounts, and response times?
### The State of the Industry

Bug bounties are currently one of the most popular ways for organizations to receive feedback about security bugs. Large corporations, like PayPal and Facebook, as well as government agencies like the US Department of Defense, have all embraced the idea. Yet not too long ago, reporting a vulnerability to a company would have more than likely landed you in jail than gotten you a reward. 

In 1995, Netscape launched the first ever bug bounty program. The company encouraged users to report bugs found in its brand new browser, the Netscape Navigator 2.0, introducing the idea of crowdsourced security testing into the internet world. Mozilla launched the next corporate bug bounty program nine years later, in 2004, inviting users to identify bugs in the Firefox browser. 

But it was not until the late 2010s that offering bug bounties became a popular practice. That year, Google launched it's program, and Facebook followed suit in 2011. These two programs kick started the trend of using bug-bounties to augment a corporation's in-house security infrastructure.

As bug bounties became a more well-known strategy, bug-bounty-as-a- service platforms emerged. These platforms help companies set up and operate their programs. For example, they provide a place for companies to host their programs, a way to process reward payments, and a centralized place to communicate with bug bounty hunters. The two largest of these platforms, HackerOne and Bugcrowd, both launched in 2012. After that, a few more platforms, such as Synack, Cobalt, and Intigriti, came to the market. These platforms and managed bug bounty services allow even companies with limited resources to run a security pro- gram. Today, large corporations, small startups, nonprofits, and government agencies alike have adopted bug bounties as an additional security mea- sure and a fundamental piece of their security policies. You can read more about the history of bug bounty programs at https://en.wikipedia.org/wiki/Bug _bounty_program.

The term **security program** usually refers to information security policies, procedures and guidelines, and standards in the larger information security industry. I use *program* and *bug bounty program* to refer to a company's bug bounty operations. Today, tons of programs exist, all with their unique characteristics, and drawbacks. Let's examine these.
### Asset Types

In the context of a bug bounty program, an *asset* is an application, website or product that you can hack. There are different types of assets, each with its own characteristics, requirements and pros and cons. After considering these differences, you should choose a program with assets that play to your strengths, based on your skillset, experience level, and preferences. 
#### Social Sites and Applications

Anything labeled as **social** has a lot of potential vulnerabilities, because these applications tend to be complex and involve a lot of interaction among users, and between the user and the server. That's why the first type of bug bounty program we'll talk about targets social websites and applications. 

The term **social application** refers to any site that allows users to interact with each other. Many programs belong to this category: examples include the bug bounty programs fro HackerOne and programs for Facebook, Twitter, GitHub and LINE.

Social programs need to manage interactions among users, as well as each user's roles, privileges and account integrity. They are typically full of potential critical web vulnerabilities such as insecure direct object references (IDORs), info leaks, and account takeovers. These vulnerabilities occur when many users are on a platform, and when applications mismanage user information; when the application does not validate a user's identity properly, malicious users can assume the identity of others. 
	These complex applications often provide a lot of user input opportunities. If input validation is not performed properly, these applications are prone to injection bugs, like SQL injection (SQLi) or cross-site scripting (XSS).

**Newcomers to bug bounty should stick to social sites**.

The large number of social apps nowadays means that if you target social sites, you'll have many programs to choose form. Also, the complex nature of social sites means that you'll encounter a vast attack surface in which to experiment. 

The diverse range of vulnerabilities on social sites means that you will get an opportunity to build a deep knowledge of web security. 
##### Skillset Needed:

- Ability to use a proxy
	- Burpsuite, ZAP
- Knowledge of web vulnerabilities like XSS and IDOR.
- JavaScript programming skills
- Web Development Knowledge
### General Web Applications

***General Web Applications*** are also good targets for beginners. Here, we are referencing any web applications that do not involve user-to-user interaction. Instead, users interact with the server to access the application's features. Targets that fall into these categories can include static web pages, cloud applications, consumer services like banking sites, and web portals of Internet of Things (IoT) devices or other connected hardware. 

**Like social sites, they are also quite diverse and lend themselves to a variety of skill levels**. 

- Google
- US DoD
- Credit Karma

These tend to be a little more difficult to hack than social applications, and their attack surface is smaller. If you're looking for account takeovers and info leak vulnerabilities, you won't have as much luck because there aren't a lot of opportunities for users to interact with others and potentially steal their information. The types of bugs that are found here are generally different as well. 
##### Skillset Needed

- Server-side vulnerabilities
- Vulnerabilities specific to the application's technology stack
- Commonly found network vulnerabilities, like **subdomain takeovers**
- Have the ability to use a proxy
- Web dev and programming knowledge is helpful

These programs can range in popularity. However, most of them have a low barrier of entry, so you can most likely get started hacking right away!
### Mobile Applications (Android, iOS and Windows)

After getting the hang of hacking web applications, you may choose to specialize in *mobile applications*. Mobile programs are becoming prevalent; after all, most web applications have a mobile equivalent these days. 

**Inclusions**:
- Facebook Messenger
- Twitter
- LINE mobile app
- Yelp
- Gmail

Hacking mobile apps requires the skill set that was build from web applications.
##### Skillset Needed:

- Structure of mobile apps
- Programming techniques related to the platform.
- Understanding of attack and analysis strategies like
	- Certificate pinning bypass
	- Mobile reverse engineering
	- Cryptography

Hacking mobile apps requires a little more setup than hacking web applications, as you'll need to own a mobile device that you can experiment on. 

A good mobile testing lab consists of:

- A regular device
- A rooted device
- Device emulators for both Android and iOS

A **rooted device** is one that has admin privileges. It allows you to experiment more freely, because you can bypass the mobile system's safety constrants. 

An **emulator** is a virtual simulation of mobile environments that you run on your computer. It allows you to run multiple device versions and operating systems without owning a device for each setup.

Mobile applications are less popular than web applications for these reasons. However, the higher barrier to entry for mobile programs is an advantage for those who do participate. These programs are less competitive, making it easier to find bugs.
### APIs

*Application Programming Interfaces (APIs)* are specifications that define how other applications can interact with an organization's assets, such as to retrieve or alter their data. 

For example, another application might be able to retrieve an application's data via HyperText Transfer Protocol (HTTP) messages to a certain endpoint, and the application will return data in the format of Extensible Markup Language (XML) or JavaScript Object Notation (JSON) messages. 

Some programs put a heightened focus on API bugs in their bounty programs if they're rolling out a new versions of their API. A secure API implementation is key to preventing data breaches and protecting customer data. Hacking APIs requires many of the same skills as *hacking web applications*, *mobile applications* and *IoT applications*. But when testing APIs, you should focus on common API bugs like data leaks and injection flaws.
### Source Code Executables

If you have more advanced programming and reversing skills, you can give *source code* and *executable programs* a try. These programs encourage hackers to find vulnerabilities in an organization's software by directly providing hackers with an open source codebase or the binary executable. Examples include the **Internet Bug Bounty**, the program for the PHP language, and the **WordPress** program. 

Hacking these programs can entail analyzing the source code of open source projects for web vulnerabilities and fuzzing binaries for potential exploits. You usually have to understand coding and computer science concepts to be successful here. You'll need knowledge of web vulnerabilities, programming skills related to the project's codebase, and code analysis skills. Cryptography, software development, and reverse engineering skills are helpful. 

Source code programs may sound intimidating, but keep in mind they're *diverse*, so you have many to choose from. You don't have to be a master programmer to hack these programs; rather, aim for a solid understanding of the project's tech stack and underlying architecture. 

Because these programs tend to require more skills, they are less competitive, and only a small proportion of hackers will ever attempt them.
### Hardware and IoT

Last but not least are hardware and IoT programs. These programs ask you to hack devices like cars, smart televisions, and thermostats. Examples include the bug bounty programs of Tesla and Ford.

You'll need highly specific skills to hack these programs: you'll often have to acquire a deep familiarity with the type of device that you're hacking, in addition to understanding common IoT vulnerabilities. You should know about:

- Web vulnerabilities
- programming
- code analysis
- reverse engineering

Also, study up on IoT concepts an industry standards such as *digital signing*, and *asymmetric encryption schemes*. Cryptography, wireless hacking, and software development skills with be helpful too. 

Although some programs will provide you with a free device to hack, that often applies to only the select hackers who've already established a relationship with the company. To begin hacking these programs, you might need the funds to acquire the device on your own.

These tend to be the *least competitive*.
## Bug Bounty Platforms

Companies can host bug bounty programs in two ways: bug bounty platforms and independently hosted websites. 

*Bug Bounty Platforms* are websites through which many companies host their programs. Usually, the platform directly awards hackers with reputation points and money for their results. Some of the largest bug bounty platforms are **HackerOne**, **Bugcrowd**, **Intigriti**, **Synack** and **Cobalt**.

Bug bounty platforms are the *intermediary between hackers and security teams*. They provide companies with logistical assistance for tasks like payment and communication. They also often offer help managing the incoming reports by filtering, deduplicating, and triaging bug reports for companies. Finally, these platforms provide a way for companies to gauge a hacker's skill level via hacker statistics and reputation. This allows companies that do now wish to be inundated with low-quality reports to invite experienced hackers to their private programs. Some of these platforms also screen or interview hackers before allowing them to hack on programs.

From the hacker's perspective, bug bounty platforms provide a centralized place to submit reports. They also offer a seamless way to get recognized and paid for your findings. 

On the other hand, many organizations host and manage their bug bounty programs without the help of platforms. Companies like Google, Facebook, Apple, and Medium do this. You can find their bug bounty policy pages by visiting their websites, or by searching “CompanyName bug bounty program” online. As a bug bounty hunter, should you hack on a bug bounty platform? Or should you go for companies’ independently hosted programs?
### The Pros...

The best thing about bug bounty platforms is that they provide a lot of transparency into a companies process, because they post disclosed reports, metrics about the program's triage rates, payout amounts, and response times. Independently hosted programs often lack this type of transparency. In the bug bounty world, *triage* refers to the confirmation of vulnerability. 

You also won't have to worry about the logistics of emailing security teams, following up on reports, and providing payment and tax info every time you submit a vulnerability report. Bug bounty programs also often have reputation systems that allow you to showcase your experience so you can gain access to invite-only bounties.

Another pro of bug bounty platforms is that they often step in to provide conflict resolution and legal protection as a third-party. If you submit a report on a non-platform program, you have no recourse in the final bounty decision.

Ultimately, you can’t always expect companies to pay up or resolve reports in the current state of the industry, but the hacker-to-hacker feedback system that platforms provide is helpful
### The Cons...

However, some hackers avoid bug bounty programs because they dislike how those platforms deal with reports. Reports submitted to platform-managed programs often get handled by *triagers*, third-party employees who often aren't familiar with all the security details about a company's product. Complaints about triagers handling reports improperly are common.

Programs on platforms also break the direct communication between hackers and developers. With a direct program, you often get to discuss the vulnerability with a company's engineers, making for a great learning experience. 

Finally, public programs on bug bounty platforms are often crowded, because the platform gives them extra exposure. On the other hand, many privately hosted programs don't get as much attention from hackers and are thus less competitive. And for the many companies that do not contract with bug bounty platforms, you have no choice but to go off platforms if you want to participate in their programs. 
## Scope, Payouts and Response Times

What other metrics should you consider when picking a program, besides its asset types and platform? On each bug bounty program’s page, metrics are often listed to help you assess the program. These metrics give insight into how easily you might be able to find bugs, how much you might get paid, and how well the program operates.
### Program Scope

First, consider the scope. A program's **scope** on it's policy pages specifies what and how you are allowed to hack. Theere are two types of scopes: **asset** and **vulnerability**. The *asset scope* tells you which subdomain, products and applications you can hack. And the *vulnerability scope* specified which vulnerabilities the company will accept as valid bugs. 

For example, the company might list the subdomains of its website that are in and out of scope:

| In-Scope Asset      | Out-of-Scope Asset |
| ------------------- | ------------------ |
| a.example.com       | dev.example.com    |
| b.example.com       | test.example.com   |
| c.example.com       |                    |
| users.example.com   |                    |
| landing.example.com |                    |
Assets that are listed as in scope are the ones that you are allowed to hack. On the other hand, assets that are listed as out of scope are off-limits to bug bounty hunters. Be extra careful and abide by the rules. **Hacking an out-of-scope asset is illegal**. 

The company will also often list the vulnerabilities it considers as valid bugs:

| **In-Scope Vulnerabilities** | **Out-of-Scope Vulnerabilities**                                                 |
| ------------------------ | ---------------------------------------------------------------------------- |
| All except the ones      | Self-XSS                                                                     |
| listed as out of scope   | Clickjacking                                                                 |
|                          | Missing HTTP headers and other best practices without direct security impact |
|                          | Denial-of-service attacks                                                    |
|                          | Use of known-vulnerability libraries, with out proof of exploitability       |
|                          | Results of automated scanners, without proof of exploitability               |
The out-of-scope vulnerabilities that you see in this example are typical of what you would find in bug bounty programs. Notice that many programs consider non-exploitable issues, like violations of best practice, to be out of scope.

> Any program with a large asset and vulnerability scopes is a good place to start for a beginner. The larger the asset scope, the larger the number of target applications and web pages you can look at. When a program has a big asset scope, you can often find obscure applications that are overlooked by other hackers. This typically means less competition when reporting bugs. The larger the vulnerability scope, the more types of bugs the organization is willing to hear reports about. These programs are a lot easier to find bugs in, because you have some opportunities, and so can play to your strengths.
### Payout Amounts

The next metric to consider is the program's *payout amounts*. There are two types of payment programs: *vulnerability disclosured programs (VDPs)* and *bug bounty programs*.

VDPs are ***reputation-only programs***, meaning they do not pay for findings but often offer rewards such as reputation points and swag. There are a *great way to learn about hacking if making money is not your primary goal*. Since they don't pay, they're less competitive, and so easier to find bugs in. You can use them to practice finding common vulnerabilities and communicating with security engineers. 

On the other hand, bug bounty programs offer varying amounts of monetary rewards for your findings. In general, the more severe the vulnerability, the more the report will pay. But different programs have different payout averages for each level of severity. You can find a program's payout information on its bug bounty pages, usually listed in a section called the *payout table*.

Typically, low-impact issues will pay anywhere from $50 to $500, while critical issues can pay upward of $10,000. However, the bug bounty industry is evolving, and payout amounts are increasing for high-impact bugs. For example, Apple now rewards up to $1m for the most severe vulnerabilities. 
### Response Time

Finally, consider the program's average *response time*. Some companies will handle and resolve your reports within a few days, while others take weeks or even months to finalize their fixes. Delays often happen because of the security team's internal constraints, like a lack of personnel to handle reports, a delay in issuing security patches, and a lack of funds to timely reward researchers. Sometimes, delays happen because researchers have sent bad reports without clear reproduction steps. 

Prioritize programs with fast response times. Waiting for responses from companies can be a frustrating experience, and when you first start, you're going to be making a lot of mistakes. You might misjudge the severity of a bug, write an unclear explanation, or make technical mistakes in the report. Rapid feedback from security teams will help you improve, and turn you into a competent hacker faster. 
## Private Programs

Most bug bounty platforms distinguish between public and private programs. 

**Public programs** are those that are open to all; anyone can hack and submit bugs to these programs, as long as they abide by the laws and the bug bounty program's policies. 

On the other hand, **Private Programs** are open to only invited hackers. For these, companies ask hackers with certain levels of expertise and a proven track record to attack the company and submit bugs to it. Private programs are a lot less competitive than public ones because of the limited number of hackers participating. Therefore, it's much easier to find bugs in them. Private programs also often have a much faster response time, because they receive fewer reports on average. 

Participating in private programs can be *extremely advantageous*. But how do you get invited to one? 
	Companies send private invites to hackers who have proven their abilities in some way, so getting invites to private programs isn't difficult once you've found a couple of bugs. Different bug bounty platforms will have different algorithms to determine who gets the invites, but here are some tips to help you get there. 

1. `Submit a few bugs to public programs.` To get private invites, you often need to gain a certain number of reputation points on a platform, and the only way to begin earning these is to submit valid bugs to public programs. You should also focus on submitting high-impact vulnerabilities. They often reward more reputation points.
2. `Don't Spam`. Submitting nonissues often causes a decrease in reputation points. Most platforms limit private invites to hackers with a certain points threshold.
3. `Be Polite and Courteous`: Being rude or abrasive to security teams will probably get you banned from the program and prevent you from getting private invites from other companies.
## Choosing the Right Program

Bug bounties are a great way to gain experience in cybersecurity and earn extra bucks. But the industry has been getting more competitive. As more people are discovering these programs and getting involved in hacking on them, it's becoming increasingly difficult for beginners to get started. That's why it's important to pick a program that you can succeed in from the very start. 

Before you develop a bug hunter's intuition, you often have to rely on low-hanging fruit and well-known techniques. This means that many other hackers will be able to find the same bugs, often much faster than you can. It's therefore a good idea to pick a program that more experienced bug hunters pass over to avoid competition.

You can find these underpopulated programs in two ways: **look for unpaid programs or go for programs with big scopes.**

Try going for vulnerability disclosure programs first. Unpaid programs are often ignored by experienced bug hunters, since they don't pay monetary rewards. But they still earn you points and recognition. And that recognition might just be what you need to get an invite to a private, paid program.

Picking a program with a large scope means you'll be able to look at a larger number of target applications and web pages. This dilutes the competition, as fewer hackers will report on any single asset or vulnerability type. Go for programs with fast response times to prevent frustration and get feedback as soon as possible.

One last thing that you can incorporate into your decision process is the reputation of the program. If you can, gather information about a company’s process through its disclosed reports and learn from other hackers’ experiences. Does the company treat its reporters well? Are they respectful and supportive? Do they help you learn? Pick programs that will be supportive while you are still learning, and programs that will reward you for the value that you provide. Choosing the right program for your skill set is crucial if you want to break into the world of bug bounties. This chapter should have helped you sort out the various programs that you might be interested in. Happy hacking!
# Chapter 2: Sustaining Your Success

Even if you understand the technical information in this book, you may have difficulty navigating the nuances of bug bounty programs. Or you might be struggling to actually locate legitimate bugs and aren't sure why you're stuck. In this chapter, we'll explore some of the factors that go into making a successful bug bounty hunter. 

- Report Writing
- Building lasting relationships with organizations
- Overcoming obstacles in bug searching
## Writing a Good Report

A bug bounty hunter's job isn't just finding vulnerabilities; it's also explaining them to the organization's security team. If you provide a well-written report, you'll help the team you're working with reproduce the exploit, assign it to the appropriate engineering team, and fix the issue faster. 

The fast a vulnerability is fixed, the less likely malicious hackers are to exploit it.
### Step 1: Craft a Descriptive Title

The first part of a great vulnerability report is always a descriptive title. Aim for a title that sums up the issue in one sentence. Ideally, it should allow the security team to immediately get an idea of **what the vulnerability is**, **where it occurred**, and its **potential severity.**

- What is the vulnerability we've found?
- Is it an instance of a well-known vulnerability type, like IDOR or XSS?
- Where was it found on the application?

> [!Example]
> For example, instead of a report title like “IDOR on a Critical Endpoint,” use one like “IDOR on https://example.com/change_password Leads to Account Takeover for All Users.” Your goal is to give the security engineer reading your report a good idea of the content you’ll discuss in the rest of it.
> 
### Step 2: Provide a Clear Summary

This section includes all the relevant details you weren't able to communicate in the title, like the HTTP request parameters used for the attack, how you found it, and so on.

Here's an example of an effective report summary:

> [!Example]
> The https://example.com/change_password endpoint takes two POST body parameters: user_id and new_password. A POST request to this endpoint would change the password of user user_id to new_password. This endpoint is not validating the user_id param- eter, and as a result, any user can change anyone else’s password by manipulating the user_id parameter.

A good report summary is **clear and concise**. It contains all the information needed to understand a vulnerability, including what the bug is, where the bug is found, and what an attacker can do with it.
### Step 3: Include a Severity Assessment

Your report should also include an honest assessment of the bug's severity. In addition to working with you to fix vulnerabilities, security teams have other responsibilities to tend to. Including a severity assessment will help them *prioritize which vulnerabilities to fix first*, and ensure that they take care of criticals right away.

| Level             | Description                                                                                                                                                                                                                                                                                           |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Low Severity      | The bug doesn't have the potential to cause a lot of damage. For example, an open redirect that can only be used for phishing it a low-severity bug.                                                                                                                                                  |
| Medium Severity   | The bug impacts users or the organization in a moderate way, or is a high-severity issue that's difficult to exploit. For example, a Cross-Site Request Forgery (CSRF) on a sensitive action such as a password change is often considered a **medium-severity** issue.                               |
| High Severity     | The bug impacts a large number of users, and its consequences can be disatrous for these users. The security team should fix a high-security bug as soon as possible. For example, an open redirect that can be used to steal OAuth tokens is a **high-severity bug**.                                |
| Critical Severity | The bug impacts a majority of the user base and endangers the organization's core infrastructure. The security team should fix a critical severity bug right away. For example, a SQL Injection leading to *remote-code execution* on the production server would be considered a **critical issue**. |
The **CVSS** Scale takes into account factors such as how a vulnerability impacts an organization, how hard it is to exploit, and whether the vulnerability requires any special privileges or user interaction to exploit.

Then, try to imagine what your client company cares about, and which vulnerabilities whould present the ***biggest business impact***. Customize your assessment to fit the client's business priorities. 
	For example, a dating site might find a bug that exposes a user's birth date as inconsequential, since a user's age is already public information on the site, while a job search site might find a similar bug significant, because an applicant's age should be confidential in the job search process.

> The leaking of users' banking information are almost always considered a high-severity issue.
### Step 4: Give Clear Steps to Reproduce

Next, provide step-by-step instructions for reproducing the vulnerability. Include all relevant setup prerequisites and details you can think of. It's best to assume the engineer on the other side has *no knowledge of the vulnerability and doesn't know how the application works*.

For example, a merely okay report might include the following steps to reproduce: 

1. Log in to the site and visit https://example.com/change_password. 
2. Click the Change Password button. 
3. Intercept the request, and change the user_id parameter to another user’s ID.

Notice how these steps aren't comprehensive or explicit. They don't specify that you need two test accounts to test for the vulnerbaility. They also assume that you have enough knowledge about the application and the format of its requests to carry out each step without more instructions.

Now, an example of a better report:

1. Make two accounts on `example.com`: account A and account B.
2. Log in to `example.com` as account A, and visit `https://example.com/change_password`.
3. Fill in the desired new password in the **New Password** field, located at the top left of the page.
4. Click the **Change Password** button located at the top right of the page. 
5. Intercept the POST request to `https://example.com/change_password` and change the `user_id` POST parameter to the user ID of account B.
6. You can now long in to account B by using the new password you've chosen.

Although the security team will probably understand the first set of instructions, the second report is a lot more specific. This avoids misunderstandings and speeds up the mitigation process.
### Step 5: Provide a Proof of Concept

For simple vulns, the steps you provide might be all that the security team needs to reproduce the issue. But for more complex vulnerabilities, it's helpful to include a video, screenshots, or photos documenting your exploit, called a *proof-of-concept* file.

For example, for a CSRF vulnerability, you could include an HTML file with the CSRF payload embedded. This way, all the security team needs to do to reproduce the issue is to open the HTML file in their browser. 

For an XML external entity attack, include the crafted XML file that you used to execute the attack. For vulnerabilities that require multiple complicated steps to reproduce, you could film a screen-capture video of you walking through the process.

Including POC files like this **saves the security team time** because they won't have to prepare the attack payload themselves. You can also include any crafted URLs, scripts, or upload files used in the attack.
### Step 6: Describe the Impact and Attack Scenarios

To help the security team fully understand the potential impact of the vulnerability, you can also illustrate a plausible scenario in which the vulnerability could be exploited. 
	Note that this section is not the same as the **severity assessment** mentioned earlier. The severity assessment describes the **severity** of the consequences of an attacker exploiting the vulnerability, whereas attack scenarios explain what those consequences would actually look like.

If hackers exploited this bug, could they:

- Take over user accounts?
- Steal user information?
- Cause a data leak/breach?

Enter the mindset of an attacker and try to escalate the impact of the vulnerability as much as possible. Give the client company a realistic sense of the **worst-case scenario**.

> Using this vulnerability, all that an attacker needs in order to change a user’s password is their user_id. Since each user’s public profile page lists the account’s user_id, anyone can visit any user’s profile, find out their user_id, and change their password. And because user_ids are simply sequential numbers, a hacker can even enumerate all the user_ids and change the passwords of all users! This bug will let attackers take over anyone’s account with minimal effort.

A good impact section illustrates *how an attacker can realistically exploit a bug*. It takes into account any mitigating factors as well as the maximum impact that can be achieved. It should **never** overstate a bug's impact or include any hypotheticals.
### Step 7: Recommend Possible Mitigations

You can also recommend possible steps the security team can take to mitigate the vulnerability. This will save the team time when it begins researching mitigations. Often, since you're the security researcher who discovered the vulnerability, you'll be familiar with the particular behavior of that application feature, and thus in a good position to come up with a fix. 

However, don't recommend fixes unless you have a good understanding of the root cause of the issue. Internal teams may have much more context and expertise to provide appropriate mitigation strategies applicable to their environment. If you're not sure what cased the vulnerability or what a possible fix may be, *avoid giving any recommendations* so you don't confuse the reader. 

Here is a possible mitigation you could propose:

> The application should validate the user’s user_id parameter within the change password request to ensure that the user is authorized to make account modifications. Unauthorized requests should be rejected and logged by the application.
### Step 8: Validate the Report

Finally, always validate your report. Go through your report one last time to make sure that there are no technical errors, or anything that might prevent the security team from understanding it. Follow your own **Steps to Reproduce** to ensure that they contain enough details. Examine all of your POC files and code to make sure they work. By validating your reports, you can minimize the possibility of submitting an invalid report. 
### Additional Tips for Better Reports
#### Don't Assume Anything

1. Don't assume the security team will be able to understand everything in your report. Remember that you might have been working with this vulnerability for a week, but to the security team receiving the report, it's all new information. Security teams have other responsibilities as well, and often there aren't dedicated teams for security. Help them understand what was discovered.
2. Be as *verbose* as possible, and include all the relevant details you can think of. It's also good to include links or references explaining obscure security knowledge that the security team might not be familiar with. Think of the consequences of being verbose vs. the consequences of leaving out crucial details. If you leave out important info, the remediation of the vulnerability might be delayed, and a malicious hacker might exploit the bug.
#### Be Clear and Concise

Don't include any unnecessary information, such as wordy greetings, jokes, or memes. A security report is a **business document**, not a letter to a friend. It should be **straightforward** and to the point. You should always be ***trying to save the security team time***.
#### Write What You Want to Read

Always put your reader in mind when writing, and try to build a good reading experience for them. Write in a conversational tone and don't use *leetspeak*, slang or abbreviations. These make the text harder to read and will add to the reader's annoyance.
#### Be Professional

Always communicate with the security team with respect and professionalism. Provide clarifications regarding the report patiently and promptly. You'll probably make mistakes when writing reports, and miscommunication will inevitably happen. But remember that as the security researcher, you have the power to minimize the possibility by putting time and care into your writing. 
## Building a Relationship with the Development Team

As the person who discovered the vulnerability, you should help the company fix the issue and make sure the vulnerability is fully patched. 

Building a strong relationship with the security team will help get your reports resolved more quickly and smoothly. It might even lead to bigger bounty payouts if you can consistently contribute to the security of the organization. 
### Understanding Report States

Once a report is submitted, the security team will classify it into a *report state*, which describes the current status of your report. The report state will change as the process of mitigation moves forward. You can find the report state listed on the bug bounty platforms interface, or in the messages you receive from security teams.
#### Need More Information

This means the security team didn't fully understand your report, or couldn't reproduce the issue by using the information you provided. They will usually follow up with questions or requests for additional info. 
	In this case, you should revise your report and provide any missing information, and address the security team's concerns.
#### Informative

If a report is marked as ***informative***, this means that the bug won't be fixed. This means they believe the issue your reported is a security concern but not significant enough to warrant a fix. Vulns that do not impact other users, such as the ability to increase your own scores on an online game, often fall into this category. 

Another type of bug often marked as informative is a missing security best practice, like allowing **password reuse**.
#### Duplicate

A ***duplicate*** report means another hack has already found the bug, and the company is in the process of remediating the vulnerability. Unfortunately, you won't get paid for duplicates.

From here, you can try to escalate or chain the bug into a more impactful one. That way, the nw report may be seen as a separate issue.
#### N/A

> ***N/A (or Not Applicable)*** means that your report *doesn't contain a valid security issue* with security implications.

This might happen when your report contains technical errors, or if the bug is intentional application behavior. N/A reports do not pay. Nothing else to do here but move on. 
#### Triaged

Security teams ***triage*** a report when they've validated the report on their end. This is great news for you, because this usually means the security team is going to fix the bug and reward a bounty. Once the report has been triaged, you should help the security team fix the issue. 
#### Resolved

When your report is marked as *resolved*, the reported vulnerability has been fixed. At this point, pat yourself on the back and rejoice in the fact that you've made the internet a little safer. 
### Dealing with Conflict

Conflicts inevitably happen when the hacker and the security team disagree on the validity of the bug, the severity of the bug, or the appropriate payout amount. Even so, conflicts could ruin your rep as a hacker, so handling them professionally is key to a successful career.

When you disagree with the security team about the validity of the bug:

- Make sure that all the information in your report is correct. Often, security teams mark reports as informative or N/A because of a technical or writing mistake. 
- Send a follow up explaining why you believe that the bug is a security issue. If that doesn't work, you can ask for ***mediation*** from the bug bounty platform or the security team.
- If the security team diminishes the severity of the reported issue, you should explain some potential attack scenarios to fully illustrate it's impact.
 - If you're unhappy with the payout amount, communicate that ***without resentment***. Ask for the reasoning behind the amount, and why explain why you think you deserve a higher reward. 
 - We all make mistakes. If you believe the person handling your report mishandled the issue, ask for reconsideration ***courteously***.
### Building a Partnership

You should strive to build long-term relationships with organizations. This can help get reports resolved more smoothly and might even land you a job interview or offer. **Respect their time**, and **communicate with professionalism**.

Gain respect by:

- Always submitting ***validated reports***. Don't break a company's trust by spamming, pestering them for money, or verbally abusing the security team. 
- Learn the ***communication style*** of each organization you deal with. How much detail do they expect in their reports?
	- Read their publicly disclosed reports, or incorporate their feedback about your reports into future messages. 
	- Do they expect a lot of pictures or videos in their reports?
	- Customize your reports to make your reader's job easier.
- Support the security team until they ***resolve the issue***. Don't bail on them as soon as you get paid. Sometimes, you'll be asked to perform retests for a fee. **Always take that** opportunity if you can. 
## Understanding Why You're Failing

In this section, we'll discuss the mistakes that prevent you from succeeding in bug bounties and how you can improve.
### Why You're Not Finding Bugs

If you spend a lot of time in bug bounties and still have trouble finding bugs, here are some possible reasons.
#### You Participate in the Wrong Programs

You might have been targeting the wrong programs all along. Bug bounty programs aren't created equally, and picking the right one is essential. Some programs delay fixing bugs because they lack the resources to deal with reports. Some programs downplay the severity of vulnerabilities to avoid paying hackers. Finally, other programs restrict their scope to a small sub-set of their assets. They run bounty programs to gain positive publicity and don't intend to actually fix vulnerabilities. Avoid these programs to save yourself the headache.

You can identify these programs by reading publicly disclosed reports, analyzing program statistics on bug bounty platforms, or by talking with other hackers. A program's stats listed on bug bounty platforms provide a lot of information on how well a program is executed. Avoid programs with *long response times* and programs with *low average bounties*. Pick targets carefully, and prioritize companies that invest in their bug bounty programs.
#### You Don't Stick to a Program

How long should you target a program? If your answer is a few hours or days, that's the reason you're not finding anything. Jumping from program to program is another mistake beginners make often.

Every bug bounty program has countless bug bounty hunters hacking it. Differentiate yourself from the competition, or risk not finding anything. You can differentiate yourself in two big ways:

1. Dig Deep
2. Search Wide

Dig Deep into a ***single functionality*** of an application to search for comple bugs.

Or Search Deep and discover and hack the lesser-known assets of the company.

Doing these things well takes time. Don't expect to find bugs right away when you're starting fresh on a program. And don't quit a program if you can't find bugs on the first day.
#### You Don't Recon

Jumping into big public programs without performing reconnaissance is another way to fail. Effective recon, which we discuss in Chapter 5, helps you discover new attack surfaces: new subdomains, new endpoints, and new functionality.

Spending time on recon gives you an *incredible advantage over other hackers*, because you'll be the first to notice the bugs on all obscure assets you discover, giving you better chances of finding bugs that aren't duplicates.
#### You Only Go for Low-Hanging Fruit

Another mistake that beginners often make is to rely on vulnerability scanners. Companies routinely scan and audit their applications, and other bug hunters often do the same, so this approach won't give you good results. 

> Avoid looking for the obvious bug types. Simplistic bugs on big targets have probably been found. Many bug bounty programs were private before companies opened them up to the public. 
> This means a few experienced hackers will have already reported the easiest-to-find bugs. 
	For example, many hackers will likely have already tested for a stored-XSS vulnerability on a forum's comment field.

This isn't to say *you shouldn't go for low hanging fruit at all*. Just don't get discouraged if you don't find anything that way. Instead, strive to gain a deeper understanding of the application's underlying architecture and logic. From there, you can develop a strong testing methodology that will result in more unique and valuable bugs. 
#### You Don't Get into Private Programs

It becomes much easier to find bugs after you start hacking on private programs. Many successful hackers say that most of their findings come from private programs. Private programs are a lot less crowded than public ones, so you'll have less competition, and less competition usually means more easy finds and fewer duplicates.
### Why Your Reports Get Dismissed

As mentioned, three types of reports won't result in a bounty: N/As, informatives, and duplicates. In this section, we talk about what you can do to reduce these disappointments. 

Reducing the number of invalid reports benefits everyone. It will not only save you time and effort, but also save the security team the staff hours dedicated to processing these reports. Here are some reasons your reports keep getting dismissed.
#### You Don't Read the Bounty Policy

One of the most common reasons reports get marked as N/A is that they're **out of scope**. A program's policy page often has a section labeled *Scope* that tells you which of the company's assets you're allowed to hack. Most of the time, the policy page also lists vulnerabilities and assets that are *out of scope*, meaning you're not allowed to report about them.

The best way to prevent submitting N/As is to read the bounty policy carefully and repeatedly. 

- Which vulnerability types are out of scope?
- Which of the organizations assets?

Respect these boundaries, and don't submit out of scope bugs. If you do find an out of scope critical bug, report it anyways. You may not get paid, but you still contribute to the company's security.
#### You Don't Put Yourself in the Organization's Shoes

Informative reports are much harder to prevent than N/As. Most of the time, you'll get informative ratings because the company doesn't care about the issue you're reporting. 

Imagine yourself as a security engineer. If you're busy safeguarding millions of users' data every day, would you care about an open redirect that can only be used for phishing? Although its a valid security flaw, you probably wouldn't.

You have other security issues to attend to, so fixing a low-severity bug is at the bottom of the to-do list. 

**Helpful ways to reduce informatives:**

- Put yourself in organization's shoes
- Learn about the organization so you can
	- Identify its product
	- The data it's protecting
	- The parts of its applications that are the most important

Different companies have different priorities. An informative report to one organization could be a critical one to another. Like the dating site versus job search site example mentioned earlier in this chapter, ***everything is relative***. 
	Sometimes, it's difficult to figure out how important a bug will be to an organization. Some issues I've reported as critical ended up being informative. Some vulnerabilities I classified as low impact were rewarded as critical issues. 

Every time the security team classifies your report as informative, take note for future reference. The next time you find a bug, ask yourself; did this company care about issues like this in the past? 
#### You Don't Chain Bugs

You might also be getting informatives because you always report the first minor bug you find.

Minor bugs classified as informative can become big issues if you learn to chain them. When you find a low-severity bug that might get dismissed, don't report it immediately. Try to use it in future bug chains instead. For example, instead of reporting an open redirect, use it in a server-side request forgery instead.
#### You Write Bad Reports

Another mistake beginners often make is that they fail to communicate the bug’s impact in their report. Even when a vulnerability is impactful, if you can’t communicate its implications to the security team, they’ll dismiss the report.
#### What about Duplicates?

Unfortunately, you sometimes can't avoid duplicates. But you could lower your chances of getting duplicates by hunting on programs with large scopes, hacking on private programs, performing recon extensively, and developing your unique hunting methodology.
## What to do When You're Stuck

***Bug Slump***: using only a few types of attacks to find vulnerabilities, without expanding your thinking or approach. This is very common among new hackers.
### Step 1: Take a Break!

Hacking is hard work. Unlike what they show in the movies, hunting for vulnerabilities is tedious and difficult. It requires patience, persistence, and an eye for detail, so it can be very mentally draining. 

Before you keep hacking away, ask yourself: am I tired? A lack of inspiration could be your brain's way of telling you it has reached its limits. In this case, your best course of action would be to **rest it out**.
### Step 2: Build Your Skillset

Use a hacking slump as an opportunity to build your skills. Hackers often get stuck because they *get too comfortable with certain familiar techniques, and when those stop working, they mistakenly assume there's nothing left to try.*

Learning new skills will get you out of your comfort zone and strengthen your hacker skills for the future. 

First, if you're not already familiar with the basic hacking techniques, refer to testing guides and best practices to solidify your skills. For example, the *Open Web Application Security Project (OWASP)* has published testing guides for various asset types. 

> [!NOTE]
> You can find OWASP’s web and mobile testing guides at https://owasp.org/www-project-web-security-testing-guide/ and https:// owasp.org/www-project-mobile-security-testing-guide/.

- Learn a new hacking technique, whether it's a new web exploitation technique, new recon angle, or a different platform, such as Android. 
- Focus on the specific skill you want to build, read about it, and apply it to the targets you're hacking.
- Catch up on what other hackers are doing by reading their blogs. 
- Play **Capture the Flags (CTFs)**. 
	- These allow you to see fresh new vulnerabilities.
	- Staying on top of new techniques and exploits will ensure that you're constantly finding bugs.
### Step 3: Gain a Fresh Perspective

Here are some tips to help keep some momentum when you start hacking live targets again:

1. Hacking on a single target can get boring, so diversifying your targets can help keep things interesting.
2. Make sure you're looking for *specific things* in a target instead of wandering aimlessly. 
3. Remember that hacking is now always about finding a single vuln but combining several weaknesses of an application into something critical. In this case, it's helpful to specifically look for weird behavior instead of vulns. 
## Lastly, a Few Words of Experience

***Bug Bounty Hunting is difficult***. The key to getting better at anything is ***practice***. If you're willing to put in the time and effort, your hacking skills will improve, and you'll soon see yourself on leaderboards and private invite lists. 

If you get frustrated during this process, remember that everything gets easier over time. Reach out to the hacker community if you need help. 

---
# Chapter 3: How the Internet Works

Before we jump into hunting for bugs, let's take some time to understand how the internet works. Finding web vulns is all about *exploiting weaknesses in this technology,* so all good hackers should have a solid understanding of it. 

> What happens when you enter `www.google.com` into your browser? In other words, how does your browser know to go from a domain name, like google.com, to the web page we're looking for?
## The Client-Server Model

The internet is composed of two kinds of devices: 

1. **Clients**
2. **Servers**

> Clients *request* resources or services, and Servers *provide* those resources and services. 

When you visit a website in your browser, it acts as a client and request a web page from a web server. The web server will then send your browser the web page. 

A web page is nothing more than a collection of resources or files sent by the web server. For example, at the very least, the server will send your browser a text file written in `Hypertext Markup Language` (`HTML`), the language that tells your browser *what to display*. 

Most webpages also include `Cascading Style Sheets` (`CSS`) files to make them pretty. Sometimes web pages also contain `JavaScript` (`JS`) files, which enable sites to animate the web page and react to user input *without going through the server*. 

For example, JavaScript can resize images as users scroll through the page and validate a user input on the client side before sending it to the server. 

Finally, your browser might receive embedded resources, such as *images or videos*. Your browser will combine these resources to display the webpage you see. 

Servers don't just return web pages to the user, either. ***Web APIs*** enable applications to request the data of other systems. This enables applications to interact with each other and share data and resources in a controlled way.
	For example, Twitter's APIs allow other websites to send requests to Twitter's services to retrieve data such as lists of public tweets and their authors. APIs power many internet functionalities beyond this, and we'll revisit them, along with their security issues.
## The Domain Name System

Every device connected to the Internet has a unique `Internet Protocol` (IP) address that other devices can use to find it. However, IP addresses are made up of numbers and letters that are hard for humans to remember. 
	For example, the older format of IP addresses, IPv4, looks like this: `123.45.67.89`. The new version, IPv6, looks even more complicated: `2001:db8::ff00:42:8329`.

This is where the `Domain Name System` (`DNS`) comes in. A DNS server functions as the *phone book* of the Internet, translating domain names into IP addresses. 

![](https://i.imgur.com/lBudKVE.png)

## Internet Ports

After your browser acquires the correct IP address, it will attempt to connect to that IP address via a port. A `port` is a logical division on devices that *identifies a specific network service*. We identify ports by their `port number`, which can range from 0 to 65,535.

Ports allow a server to provide multiple services to the internet at the same time. Because conventions exit for the traffic received on certain ports, port numbers also allow the server to quickly forward arriving internet messages to a corresponding service for processing. 
	For example, if an internet client connects to port 80, the web server understand that the client wishes to access its web services.

![](https://i.imgur.com/Rb6g7Mc.png)

> By default, we use port 80 for HTTP messages and port 443 for HTTPS, the encrypted version of HTTP.
## HTTP Requests and Responses

Once a connection is established, the browser and server communicate via the `Hypertext Transfer Protocol` (HTTP). HTTP is a set of rules that specifies *how to structure and interpret*
*internet messages*, and *how web clients and web servers should exchange information*.

When a browser wants to interact with a server, it sends the server an `HTTP Request`. There are different types of HTTP requests, and the two most command are `GET` and `POST`. 

- By convention, `GET` requests *retrieve* data from the server
- `POST` requests submit data to it

Other common HTTP methods include:

- `OPTIONS`: used to request permitted HTTP methods for a given URL
- `PUT`: used to update a resource
- `DELETE`: used to delete a resource

```HTTP
GET / HTTP/1.1 
Host: www.google.com 
User-Agent: Mozilla/5.0 
Accept: text/html,application/xhtml+xml,application/xml 
Accept-Language: en-US 
Accept-Encoding: gzip, deflate 
Connection: close
```

Let's walk through the structure of this request, since these will be everywhere in this book. 

All HTTP requests are composed of a `request line`. `request headers`, and an `optional request body`.

- `Request Line`: the first line of the HTTP request. It specifies the *request method*, the *requested URL*, and the *version of HTTP used*.

```
GET / HTTP/1.1
```

- The rest of the lines are `HTTP Request Headers`. These are used to pass additional information about the request to the server. This allows the server to customize results sent to the client. 

In the preceding example:

-  the `Host` header specifies the hostname of the request. 
- The `User-Agent` header contains the operating system and software version of the *requesting* software, such as the web browser.
- The `Accept`,`Accept-Language`, and `Accept-Encoding` headers tell the server which format the responses should be in.
- The `Connection` header tells the server whether the network connection should stay open after the server responds.

There are a few other common headers seen in requests. 

- The `Cookie` header is used to send cookies from the client to the server. 
- The `Referer` header specifies the *address of the previous webpage* that linked to the current page. 
- The `Authorization` header contains credentials to authenticate a user to a server.

After the server receives the request, it will try to fulfill it. The server will return all the resources used to construct your web page by using `HTTP Responses`. An HTTP response contains multiple things:

- An `HTTP Status Code` to indicate whether the request succeeded
- `HTTP Headers`, which are bits of information that browsers and servers use to communicate with each other about *authentication, content format, and security policies*;
- `HTTP Response Body`, the actual web content you have requested. The web content would include **HTML code**, **CSS Style Sheets**, **JavaScript code**, images and more. 

Here is an example of an HTTP response:

```HTTP
HTTP/1.1 200 OK 2 
Date: Tue, 31 Aug 2021 17:38:14 GMT [...] 3 
Content-Type: text/html; charset=UTF-8 4 
Server: gws 5 C
ontent-Length: 190532 

<!doctype html> 
[...] 
<title>Google</title> 
[...] <html>
```

1. The `200 OK` message on the first line is the **status code**. AN HTTP status code in the 200 range indicates a successful request. A status code in the 300 range indicates a redirect to another page, whereas the 400 range indicates an error on the client's part, like a request for a non-existent page. The 500 range means that the *server itself ran into an error*.

> As a bug bounty hunter, you should *always keep an eye on these status codes*, because they can tell you a lot about how the server is operating. 
> 	For example, a status code of 403 means that the resource is forbidden to you. This might mean that sensitive data is hidden on the page that you could reach if you can bypass the access controls.

2. The next few lines are separated by a colon (`:`) in the response are the **HTTP Response Headers**. They allow the server to pass additional information about the response to the client. In this case, you can see that the time of the response was `Tue, 31 Aug 2021 17:38:14 GMT`.

3. The `Content-Type` header indicates the **file type** of the response body. In this case, the `Content-Type` of this page is `text/html.

4. The server version is **Google Web Server (gws)**.

5. The `Content-Length` is 190,532 bytes.

Usually, additional response headers will specify the content's format, language, and security policies. 

In addition to these, you might encounter a few other common response headers:

- The `Set-Cookie` header is sent by the server to the client to set a cookie.
- The `Location` header indicates the URL to which to redirect the page.
- The `Access-Control-Allow-Origin` header indicates which origins can access the page's contents. 
- `Content-Security-Policy` controls the origin of the resources the browser is allowed to lad, while the `X-Frame-Options` header indicates whether the page can be loaded within an iframe.

The data after the blank line is the response body. It contains the actual content of the web page, such as the HTML and JavaScript code. Once your browser receives all the information needed to construct the web page, it will render everything for you.
## Internet Security Protocols

To hunt for bugs effectively, you will often need to come up with creative ways to bypass these controls, so you'll first need to understand how they work.
### Content Encoding

Data transferred in HTTP requests and responses isn't always transmitted in the form of plain old text. Websites often ***encode*** their messages in different ways to prevent data corruption.

Data encoding is used as a way to transfer *binary data reliably* across machines that have limited support for different content types. Characters used for encoding are *common characters* not used as controlled characters in internet protocols. So when you encode content using common encoding schemes, you can be *confident that your data is going to arrive at its destination uncorrupted*. In contrast, when you transfer your data in it's original state, the data might be screwed up when internet protocols misinterpret special characters in the message. 

***Base64 Encoding*** is one of the most common ways of encoding data. It's often used to transport images and encrypted information within web messages. This is the base64 encoded version of the string "`Content Encoding`":

```base64
Q29udGVudCBFbmNvZGluZw==
```

Base64 encoding's character set includes the uppercase alphabet characters A-Z, the lowercase alphabet characters a - z, the number characters 0 - 9, the characters `+` and `/`, and finally, the `=` character for padding. 

***Base64url*** encoding is a modified version of base64 used for the URL format. It's similar to base64, but uses different non-alphanumeric characters and omits padding. 

Another popular encoding method is hex encoding. ***Hexadecimal Encoding***, or ***hex***, is a way of representing characters in a base-16 format, where characters range from 0 to F. Hex encoding takes up more space and is less efficient than base64 but provides for a more *human-readable* encoded string. 

This is the hex-encoded version of the string "`Content-Encoding`":

```hex
436f6e74656e7420456e636f64696e67
```

***URL Encoding*** is a way of converting characters into a format that is more *easily transmitted* over the internet. Each character in a URL-encoded string can be represented by it's designated hex number preceded by a `%` symbol. 

For example, the word ***localhost*** can be represented with it's URL-encoded equivalent:

```URL Encoded
%6c%6f%63%61%6c%68%6f%73%74
```

We'll cover a couple of additional types of character encoding -- ***octal encoding*** and ***dword encoding*** -- when we discuss SSRFs in Chapter 13. When you see encoded content while investigating a site, always try to decode it to discover what the website is trying to communicate. You can use Burp Suite's decoded to decode encoded content. We'll cover how to do this is the next chapter. 

Alternatively, you can use ***CyberChef*** to decode both base64 and other types of encoded content. Servers sometimes also ***encrypt*** their content before transmission. This keeps the data private between the client and server and prevents anyone who intercepts the traffic from eavesdropping on the messages.
### Session Management and HTTP Cookies

Why is it that you don't have to re-log in every time you close your email tab? 

> It's because the website remembers your session. 

***Session Management*** is a process that allows the server to handle multiple requests from the same user without asking the user to log in again.

Websites maintain a session for each logged-in user, and a new session starts when you log in to the website. The server will assign an associated `Session ID` for your browser that serves as proof of your identity. 

The session ID is usually a long and unpredictable sequence designed to be **unguessable**. When you log out, the server ends the session and revokes the session ID. The website might also end sessions periodically if you don't manually log out.

![](https://i.imgur.com/kMjJ9mS.png)

Most websites uses ***cookies*** to communicate session information in HTTP requests. ***HTTP Cookies*** are small pieces of data that web servers send to your browser. When you log into a site, the server creates a session for you and sends the session ID to your browser as a cookie. After receiving a cookie, your browser stores it and includes it in every request to the same server. 

> That's how the server knows it's you! After the cookie for the session is generated, the server will track it and use it to validate your identity. 

Finally, when you log out, the server will invalidate the session cookie so that it cannot be used again. The next time you log in, the server will create a new session and a new associated session cookie for you.

![](https://i.imgur.com/VqndyMo.png)
### Token-Based Authentication

In session-based authentication, the server stores your information and uses a corresponding session ID to validate your identity, whereas a *token-based authentication* system stores this info directly in some sort of token. Instead of storing your information server-side and querying using a session ID, tokens allow servers to deduce your identity by decoding the token itself. This way, applications won't have to store and maintain session information server-side.

This system comes with a risk:

> If the server uses information contained in the token to determine the user's identity, couldn't users modify the information in the tokens and log in as someone else?
	To prevent token forgery attacks like these, some applications encrypt their tokens, or encode the token so that it can be read by only the application itself or other authorized parties. If the user can't understand the contents of the token, they probably can't tamper with it effectively either. 

Encrypting or encoding a token does not prevent token forgery completely. There are ways that an attacker can tamper with an encrypted token without understanding its contents. But it's a lot more difficult than tampering with a plaintext token. Attackers can often decode encoded tokens to tamper with them. 

Another more reliable way applications protect the integrity of a token is by signing the token and verifying the token signature when it arrives at the server. ***Signatures*** are used to verify the integrity of a piece of data. They are special strings that can be generated only if you know a secret key, and only the server knows what the secret key is, a valid signature suggests that the token is probably not altered by the client or any third party. Although the implementations by applications can vary, token-based authentication works like this:

1. The user logs in with their credentials. 
2. The server validates those credentials and provides the user with a signed token.
3. The user sends the token with every request to prove their identity. 
4. Upon receiving and validating the token, the server reads the user's identity information from the token and responds with confidential data. 
### JSON Web Tokens

The ***JSON Web Token*** (`JWT`) is one of the *most commonly used* types of authentication tokens. It has three components: a header, a payload, and a signature.

- The `header` identifies the algorithm used to generate the signature. It's a base64url-encoded string containing the algorithm name. Here's what a JWT header looks like:

```JWT
eyBhbGcgOiBIUzI1NiwgdHlwIDogSldUIH0K
```

- This string is the base64url-encoded version of this text:

```
{ "alg" : "HS256", "typ" : "JWT" }
```

- The `payload` section contains information about the user's identity. This section, too, is base64url-encoded before being used in the token. Here's an example of the payload section, which is the base64url-encoded string of `{ "user_name" : "admin", }:`

```
eyB1c2VyX25hbWUgOiBhZG1pbiB9Cg
```

- Finally, the `signature` section validates that the user hasn't tampered with the token. It's calculated by concatenating the header with the payload, then signing it with the algorithm specified in the header, and a secret key. Here's what a JWT signature looks like:

```
4Hb/6ibbViPOzq9SJflsNGPWSk6B8F6EqVrkNjpXh7M
```

- For this specific token, the signature was generated by signing the string `eyBhbGcgOiBIUzI1NiwgdHlwIDogSldUIH0K.eyB1c2VyX25hbWUgOiBhZG1pbiB9Cg` with the HS256 algorithm using the secret key `key`. The complete token concatenates each section (the header, payload and signature), separating then with a period (`.`).

```
eyBhbGcgOiBIUzI1NiwgdHlwIDogSldUIH0K.eyB1c2VyX25hbWUgOiBhZG1pbiB9Cg.4Hb/6ibbVi POzq9SJflsNGPWSk6B8F6EqVrkNjpXh7M
```

When implemented correctly, JSON web tokens provide a secure way to identify the user. When the token arrives at the server, the server can verify that the token has not been tampered with by checking that the signature is correct. Then the server can deduce the user's identity by using the information contained in the `payload` section. And since the user does not have access to the secret key used to sign the token, they cannot alter the payload and sign the token themselves.

> If implemented incorrectly, there are ways that an attacker can bypass the security mechanism and forge arbitrary tokens.
#### Manipulating the `alg` Field

Sometimes applications fail to verify a token's signature after it arrives at the server. This allows an attacker to simply bypass the security mechanism by providing an invalid or blank signature. 

One way that attackers can forge their own tokens is by tampering with the `alg` field of the token header, which lists the algorithm used to encode the signature. If the application does not restrict the *algorithm type used in the JWT*, an attacker can specify which algorithm to use, which could compromise the security of the token. 

JWT supports a `none` option for the algorithm type. If the `alg` field is set to `none`, even tokens with empty signature sections would be considered valid. Consider, for example, the following token:

```
eyAiYWxnIiA6ICJOb25lIiwgInR5cCIgOiAiSldUIiB9Cg.eyB1c2VyX25hbWUgOiBhZG1pbiB9Cg
```

This token is simply the base64url-encoded versions of these two blobs, with no signature present:

```
{ "alg" : "none", "typ" : "JWT" } { "user" : "admin" }
```

This feature was originally used for debugging purposes, but if not turned off in a production environment, it would allow attackers to forge any token and impersonate anyone on the site.

Another way attackers can exploit the `alg` field is by changing the type of algorithm used. The two most common types of signing algorithms used for JWTs are ***HMAC*** and ***RSA***. 
##### HMAC

`HMAC` requires the token to be signed with a key and then later verified with the same key. 
##### RSA

When using `RSA`, the token would first be created with a private key, then verified with the corresponding public key, which anyone can read. 

> It is critical that the secret key for HMAC tokens and the private key for RSA tokens to be kept secret.

Now let's say that an application was originally designed to use RSA tokens. The tokens are signed with private key A, which is kept a secret from the public. Then the tokens are verified with public key B, which is available to anyone. This is okay as long as the tokens are always treated as RSA tokens. Now if the attacker changes the `alg` field to HMAC, the token is still verified with the RSA public key B, but this time, the token can be signed with the same public key too. 
#### Brute-Forcing the Key

It could also be possible to guess, or ***brute-force***, the key used to sign a JWT. The attacker has a lot of information to start with: the algorithm used to sign the token, the payload that was signed, and the resulting signature. If the key used to sign the token is not complex enough, they might be able to brute-force it easily. If an attacker is not able to brute-force the key, they might try leaking the secret key instead. If another vulnerability, like a *directory traversal*, *external entity attack*, or *SSRF* exists that allows the attacker to read the file where the key value is stored, the attacker can steal the key and sign arbitrary tokens of their choosing. We'll talk about these vulnerabilities in later chapters.
#### Reading Sensitive Information

Since JSON web tokens are used for ***access control***, they often *contain information about the user.* 
If the token is not encrypted, anyone can base64-decode the token and read the token's payload. If the token contains sensitive information, it might become a source of information leaks. A properly implemented signature section of the JSON web token provides data integrity, not confidentiality. 

These are just a few examples of JWT security issues. For more examples of JWT vulnerabilities, use the search term *JWT Security Issues*. The security of any authentication mechanism depends not only on it's design, but also its implementation. JWTs can be secure, but only if implemented properly. 
### The Same-Origin Policy

The ***same-origin policy*** is a rule that restricts how a script from one origin can interact with the resources of a different origin. In one sentence, the SOP is this:

- A script from page A can access data from page B only if the pages are of the same origin. This rule protects modern web applications and prevents many common web vulnerabilities.

Two URLs are said to have the same origin if they share the same *protocol*, *hostname* and *port* 
*number*. Let's look at some examples:

Page A is at this URL:

```
https://medium.com/@vickieli
```

It used HTTPS, which, remember, uses port 443 by default. Now look at the following pages to determine which has the same origin as Page A, according to the SOP:

```
https://medium.com/ 
http://medium.com/ 
https://twitter.com/@vickieli7 
https://medium.com:8080/@vickieli
```

The `https://medium.com` URL is of the same origin as Page A, because the two pages share the same origin, protocol, hostname and port number. The other three pages do not share the same origin as Page A. 

- `http://medium.com` is of a different origin from page A, because their protocols differ.
- `https://medium.com` uses HTTPS, wheras `http://medium.com` used HTTP.
- `https://twitter.com/@vickieli7` is of a different origin as well, because it has a different hostname. 
- `https://medium.com:8080/@vickieli` is of a different origin because it uses port `8080`, instead of port `443`.

Now let's consider an example to see how SOP protects us. Imagine that you're logged in to your banking site at *onlinebank.com*. Unfortunately, you click on a malicious site, *attacker.com*, in the same browser. 

The malicious site issues a GET request to *onlinebank.com* to retrieve your personal information. Since you're logged into the bank, you browser automatically includes your cookies in every request you send to *onlinebank.com*, even if the request is generated by a script on a malicious site. Since the request by sending the HTML page containing your info. The malicious script then reads and retrieves the private email addresses, home addresses, and banking information contained on the page. 

Luckily the SOP will prevent the malicious script hosted on *attacker.com* for reading the HTML data returned from *onlinebank.com*. This keeps the malicious script on Page A from obtaining sensitive information embedded with page B.
## Learn to Program

You should now have a solid background to help you understand most of the vulnerabilities we will cover. Before you set up your hacking tools, I recommend that you learn to program. Programming skills are helpful, because hunting for bugs involves many repetitive tasks, and by learning a programming language such as Python or shell scripting, you can automate these tasks to save yourself a lot of time.

You should also learn to *read JavaScript*, the language with which most sites are written. Reading the JavaScript of a site can teach you about how it works, giving you a fast track to finding bugs. Many top hackers say that their secret sauce is that they read JavaScript and search for hidden endpoints, insecure programming logic, and secret keys. I've also found many vulnerabilities by reading JavaScript source code. 

Codecademy is a good resource for learning how to program. If you prefer to read a book instead, *Learn Python the Hard Way* by Zed Shaw (Addison-Wesley Professional, 2013) is a great way to learn Python. And reading *Eloquent JavaScript*, Third Edition, by Marijn Haverbeke (No Starch Press, 2019) is one of the best ways to master JavaScript.
# Chapter 4: Environmental Setup and Traffic Interception

You'll save yourself a lot of time and headache if you hunt for bugs within a well-oiled lab. This chapter serves as a guide for setting up your hacking environment. 

You'll configure your browser to work with BurpSuite. We'll learn how to use Burp's features to intercept web traffic, send automated and repeated requests, decode encoded content, and compare requests. We will also talk about how to take good bug bounty notes. 
## Choosing an Operating System

Before we go on, the first thing you need to do is choose an operating system. Your operating system will limit the hacking tools available to you. I recommend using a Unix-based operating system, like Kali Linux or macOS, because many open source hacking tools are written for these systems. *Kali Linux* is a Linux distribution designed for digital forensics and hacking. It includes many useful bug bounty tools, such as Burp Suite, recon tools like `DirBuster` and `GoBuster`, and fuzzers like `Wfuzz`. 
## Setting up the Essentials: A Browser and a Proxy

Next, we need to setup a web browser and a proxy. We'll use the browser to examine the features of a target application. I recommend using Firefox, since it's the simplest to set up with a proxy. You can also use two different browsers when hacking; one for browsing the target, and one for researching vulnerabilities on the internet. This way, you can easily isolate the traffic of your target application for further examination.

A *proxy* is a software that sits between a client and a server; in this case, it sits between your browser and the web servers you interact with. It intercepts your requests before passing them to the server, and intercepts the server's responses before passing them to you, like this:

Browser <==========> Proxy <============> Server

Using a proxy is essential in bug bounty hunting. Proxies enable you to view and modify the requests going out to the server and the responses coming into your browser, as I'll explain later in this chapter. Without a proxy, the browser and the server would exchange messages automatically, without your knowledge, and the only thing you would see is the final resulting webpage.

> A proxy will instead capture *all messages* before they travel to their intended recipient.

Proxies also let you examine interesting requests to look for potential vulnerabilities and explout these vulnerabilities by tampering with requests.

> For example, let's say you visit your email inbox and intercept the request that will return your email with a proxy. It's a GET request to a URL that contains your user ID. You also notice that a cookie with your user ID is included in the request:

```
GET /emails/USER_ID HTTP/1.1 
Host: example.com 
Cookie: user_id=USER_ID
```

In this case, you can try to change the `USER_ID` in the URL and the `Cookie` header to another user's ID and see if you can access another user's email. Two proxies are particularly popular among bug bounty hunters: **Burp Suite** and the **Zed Attack Proxy (ZAP)**. 
### Opening the Embedded Browser

Both Burp Suite and ZAP come with embedded browsers. If you choose to use these embedded browsers for testing, you can skip the next two steps. To use Burp Suite’s embedded browser, click Open browser in Burp’s Proxy tab after it’s launched (Figure 4-1). This embedded browser’s traffic will be automatically routed through Burp without any additional setup.
### Setting up Firefox

Burp’s embedded browser offers a convenient way to start bug hunting with minimal setup. However, if you are like me and prefer to test with a browser you are used to, you can set up Burp to work with your browser. Let’s set up Burp to work with Firefox. Start by downloading and installing your browser and proxy. You can download the Firefox browser from https://www.mozilla.org/firefox/new/ and Burp Suite from https://portswigger.net/burp/. Bug bounty hunters use one of two versions of Burp Suite: Professional or Community. You have to purchase a license to use Burp Suite Professional, while the Community version is free of charge. Burp Suite Pro includes a vulnerability scanner and other convenient features like the option to save a work session to resume later. It also offers a full version of the Burp intruder, while the Community version includes only a limited version. In this book, I cover how to use the Community version to hunt for bugs. Now you have to configure your browser to route traffic through your proxy. This section teaches you how to configure Firefox to work with Burp Suite. If you’re using another browser-proxy combination, please look up their official documentation for tutorials instead.
## Using Burp

Burp Suite has a variety of useful features besides the web proxy. Burp Suite also includes an `intruder` for automating attacks, a `repeater` for manipulating individual requests, a `decoder` for decoding encoded content, and a `comparer` tool for comparing requests and responses. Of all Burp's features, these are the most useful for bug bounty hunting, so we will explore them here.
### The Proxy

Open Burp and switch to the Proxy tab, and start exploring what it does. To begin intercepting traffic, make sure the intercept button is on.

When you browse a site on Firefox or Burp's embedded browser, you should see an HTTP/HTTPS request appear in the main window. When intercept is turned on, every request your browser sends will go through Burp, which won't send them to the server unless you click `Forward` in the proxy window. 

You can use this opportunity to *modify the request* before sending it to the server or to forward it over to other modules in Burp. You can also use the search bar at the bottom of the window to search for strings in these requests or responses.
	To forward the request to another **Burp** module, right-click the request and select `Send to Module`.
#### Practice

Let's practice intercepting and modifying traffic by using Burp Proxy. 

1. Go to Burp Proxy and turn on **traffic interception**.
2. Open a browser and visit `https://www.google.com`.

As we did with the preceding section, click **Forward** until you see the request with the hostname `www.google.com`.

We should see a request like this one:

```http
Host: www.google.com
Cookie: AEC=AZ6Zc-VWRs7XXGmusKB7ma7MPyIs61JaCZdEuyVVbslsjVzpI_Ny3OWLlw; NID=521=F3v39dwAHPq7iwZxsnnh5U5cj5VJxssnxLaJJy4DVq1mJcG7w_rbU4FakeMQmOHGudEpeiMfBLtbGxPWIooVkidamqP1nuL8ES7pGk2nniPR3aq5qd9kINr_bHyJOvDFYAicFwrvKoJkAzongon1-uEBM9GerCIz4poieBCdHOtCAr0cTPzwvQGOLOWapgBVHXTsumHSv-HIynLk2-wGvDJ8Rh2P_jHW_qDATCYcN5sUaVrgyRPJEKbQMI6Kxc7JqYygpB3aO6dCsw
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://www.google.com/
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Te: trailers
```

Let's modify this request before sending it. Change the `Accept-Language` header value to `de`.

Click **Forward** to send the request over to Google's server. We should see Google's homepage in German appear in our browser's window.

If you’re a German speaker, you could do the test in reverse: switch the Accept-Language header value from de to en. You should see the Google home page in English. Congratulations! You’ve now successfully intercepted, modified, and forwarded an HTTP request via a proxy.
### The Intruder

The Burp `intruder` tool automates request sending. If you are using the Community version of Burp, your intruder will be a limited, trial version. Still, it allows you to perform attacks like *brute-forcing*, whereby an attacker submits many requests to a server using a list of predetermined values and sees if the server responds differently. 
	For example,  a hacker who obtains a list of commonly used passwords can try to break into your account by repeatedly submitting login requests with all the common passwords. You can send requests over to the intruder by right-clicking a request in the proxy window and selecting **Send to Intruder**. 

The **Target** screen in the intruder tab lets you specify the host and port to attack. If you forward a request from the proxy, the host and port will be prefilled for you.

`Intruder` gives several ways to customize your attack. For each request, you can choose the payloads and payloads position to use. The *payloads* are the data that you want to insert into specific positions in the request. The *payload positions* specify which parts of the request will be replaced by the payloads you choose. 
	For example, let's say users log in to `example.com` by sending a POST request to `example.com/login`. In Burp, this request might look like this:

```http
POST /login HTTP/1.1 
Host: example.com 
User-Agent: Mozilla/5.0 
Accept: text/html,application/xhtml+xml,application/xml 
Accept-Language: en-US 
Accept-Encoding: gzip, deflate 
Connection: close 

username=vickie&password=abc123
```

The POST request body contains two parameters: `username` and `password`. If you were trying to brute-force a user's account, you could switch up the `password` field of the request and keep everything else the same. To do that, specify the payload positions in the **Positions** screen. To add a portion of the request to the payload positions, highlight the text and click **Add** on the right.

Then, switch over to the **Payloads** screen. Here, you can choose payloads to insert into the request. To brute-force a login password, you can add a list of commonly used passwords here. You can also, for example, use a list of numbers with which to brute-force IDs in requests, or use an attack payload list you downloaded from the internet. 

Reusing attack payloads shared by others can help you find bugs faster. We will talk more about how to use reused payloads to hunt for vulnerabilities in Chapter 25.

Once you've specified those, click the **Start Attack** button to start the automated test. The intruder will send a request for each payload you listed and record all responses. You can then review the responses and response codes for interesting results. 
### The Repeater

The `Repeater` is probably the tool you'll use the most often. You can use it to modify requests and examine server responses in detail. You could also use it to bookmark interesting requests to go back to later.

Although the repeater and intruder both allow you to manipulate requests, the two tools serve very different purposes. The intruder automates attacks by automatically sending programmatically modified requests. The repeater is meant for *manual*, *detailed modifications* of a single request. 

Send requests to the repeater by right clicking the request and selecting **Send to Repeater**.

On the left of the repeater screen are requests. You can modify a request here and send the modified request to the server by clicking **Send** at the top. The corresponding response from the server will appear on the right. 

The repeater is good for ***exploiting bugs manually***, trying to bypass filters, and testing out different attack methods that target the same endpoint.
### The Decoder

The Burp `Decoder` is a convenient way to encode and decode data you find in requests and responses. Most often, it is used to decode, manipulate, and re-encode application data before forwarding it to applications.

Send data to the decoder by highlighting a block of text in any request or response, then right-clicking it and selecting **send to Decoder**. Use the drop-down menus on the right to specify the algorithm to use to encode or decode the message. If you're not sure which algorithm to use, try **Smart Decode**. 
### The Comparer

The `Comparer` is a way to compare requests or responses. It highlights the differences between two blocks of text. You might use it to examine how a difference in parameters impacts the response you get from the server, for example. 

Send data over to the comparer by highlighting a block of text in any request or response, then selecting **Send to Comparer**.
### Saving Burp Requests

You can save requests and responses on Burp as well. Simply right-click any request and select **Copy URL**, **Copy as `curl` command**, or **Copy to file** to store these results into your note folder for that target. The Copy URL option copies the URL of the request. The copy as `curl` command copies the entire request, including the request method, URL, headers, and body as a curl command. Copy to file saves the entire request to a separate file.
## A Final Note on... Taking Notes

Before you get started looking for vulnerabilities in the next chapter, a quick word of advice:

> Organizational skills are critical if you want to succeed in bug bounties. When you work on targets with large scopes or hack multiple targets at the same time, the information you gather from the targets could balloon and become hard to manage. 

Often, you won't be able to find bugs right away. Instead, you'll spot a lot of weird behaviors and misconfigurations that aren't exploitable at the moment but that you could combine with other behavior in an attack later on. You'll need to take good notes about new features, misconfigurations, minor bugs, and suspicious endpoints that you find so you can quickly go back and use them.

Notes also help you plan attacks. You can keep track of your hacking progress, the features you've tested, and those you still have to check. This prevents you from wasting time by testing the same features over and over again.

Another good use of notes is to ***jot down information about the vulnerabilities you learn about***. Record details about each vulnerability, such as its *theoretical concept*, *potential impact*, 
*exploitation steps*, and *sample proof-of-concept* code. Over time, this will strengthen your technical skills and build up a technique that you can revisit if needed. 

Since these notes tend to balloon in volume and become very disorganized, it's good to keep them *organized from the get-go*. I like to take notes in plaintext files by using Sublime Text and organize them by sorting them into directories, with subdirectories for each target and topic. 

For example, you can create a folder for **each target you're working on**, like Facebook, Google or Verizon. Then, within each of these folders, create files to document interesting endpoints, new and hidden features, reconnaissance results, draft reports, and POCs.

Find a note taking an organizational strategy that works for you. For example, if you are like me and prefer to store notes in plaintext, you can search around for an integrated development environment (IDE) or text editor that you feel the most comfortable in. Some prefer to take notes using the Markdown format. In this case, Obsidian (using now!!!!) is an excellent tool that displays your notes in an organized way. If you like to use min maps to organize your ideas, you can try the mind-mapping tool `XMind`.

Keep your bug bounty notes in a centralized place, such as an external hard drive or cloud storage service like Google Drive or Dropbox, and don’t forget to back up your notes regularly! In summary, here are a few tips to help you take good notes: 

- • Take notes about any weird behaviors, new features, misconfigurations, minor bugs, and suspicious endpoints to keep track of potential vulnerabilities. 
- • Take notes to keep track of your hacking progress, the features you’ve tested, and those you still have to check. 
- • Take notes while you learn: jot down information about each vulner- ability you learn about, like its theoretical concept, potential impact, exploitation steps, and sample POC code. 
- • Keep your notes organized from the get-go, so you can find them when you need to! 
- • Find a note-taking and organizational process that works for you. You can try out note-taking tools like Sublime Text, Obsidian and XMind to find a tool that you prefer.
# Chapter 5: Web Hacking Reconnaissance

The first step to attacking any target is conducting *reconnaissance*, or simply put, gathering information about the target. Reconnaissance is important because it's how you figure out an application's attack surface. To look for bugs most efficiently, you need to discover all the possible ways of attacking a target before deciding on the most effective approach.

If an application doesn't use PHP, for example, there's **no reason to test for PHP vulnerabilities**, and if the organization doesn't use Amazon Web Services, you shouldn't waste time trying to crack it's buckets. By understanding how a target works, you can set up a solid foundation for finding vulnerabilities. Recon skills are what separate a good hacker from an ineffective one.

In this chapter:

- The basics of writing a Bash script to automate recon tasks and make them more efficient. *Bash* is a shell interpreter available on Linux and macOS systems. Though this chapter assumes you're using a Linux system, you should be able to install many of these tools on other operating systems as well. 
- Before moving on, please verify you're allowed to perform intrusive actions and recon on your target before you attempt any techniques that actively engage with it. In particular, activities like port scanning, spidering, and directory brute-forcing can generate a lot of unwanted traffic on a site and may not be welcomed by the organization.
## Manually Walking Through a Target

Before we dive into anything else, it will help to first manually walk through the application to learn more about it. Try to uncover every feature in the application that users can access by browsing through every page and clicking every link. Access the functionalities you don't normally use. 
	For example, if you're hacking Facebook, try to create an event, play a game, use the payment functionalities if you've never done so before. Sign up for an account at every privilege level to reveal all of the applications features. 
	For example, on Slack, you can create *owners*, *admins*, and *members* for a workspace. Also create users who are members of different channels under the same workspace. This way, you can see what the application looks like to different users.

This should give you a rough idea of what the ***attack surface*** looks like, where the data entry points are, and how different users interact with each other. Then you can start a more in-depth recon process: *finding out the technology and structure of the application*.
## Google Dorking

When hunting for bugs, you'll often need to research the details of a vulnerability. If you're exploiting a potential cross-site scripting (XSS) vulnerability, you might want to find a particular payload you saw on GitHub. Advanced search skills will help you find the resources you need quickly and accurately. 

In fact, advanced Google searches are a powerful technique that hackers often use to perform recon. Hackers call this ***Google Dorking***. For the average Joe, Google is just a text search tool for finding images, videos and web pages. But for the hacker, Google can be a means of discovering valuable information such as:

- hidden admin portals
- unlocked password files
- leaked authentication keys

Google's search engine has it's own built in query language that helps you filter your searches, here are some of the most useful operators that can be used with any Google search:
### `site`

Tells google to show you results from a certain site only. This will help you quickly find the most reputable source on the topic that you are researching. 
	For example, if you wanted to search for the syntax of Python's `print()` function, you could limit your results to the official Python documentation with this search: `print site:python.org`.
### `inurl`

Searches for pages with a URL that match the search string. It's a powerful way to search for vulnerable pages on a particular website. Let's say you've read a blog post about how the existence of a page called `/course/jumpto.php` on a website could indicate that it's vulnerable to remote code execution. You can check if the vulnerability exists on your target by searching `inurl: "/course/jumpto.php" site:example.com`.
### `intitle`

Finds specific strings in a page's title. This is useful because it allows you to find specific pages that contain a particular type of content. For example, file-listing pages on web servers often have *index of* in their titles.

You can use this query to search for directory pages on a website: `intitle: "index of" site:example.com`.
### `link`

Searches for web pages that contain links to a specified URL. You can use this find documentation about obscure technologies or vulnerabilities. For example, let's say you're researching the uncommon regular expression denial-of-service (ReDoS) vulnerability. You'll easily pull up it's definition online but might have a hard time finding examples. The `link` operator can discover pages that reference the vulnerability's Wikipedia page to locate discussions of the same topic: `link: "https://en.wikipedia.org/wiki/ReDoS`.
### `filetype`

Searches for pages with a specific file extension. This is an incredible tool for hacking; hackers often use it to locate files on their target sites that might be sensitive, such as log and password files.
	For example, this query searches for log files, which often have the `.log` file extension, on the target site: `filetype:log site:example.com`.
### Wildcard (`*`)

You can use the wildcard operator (`*`) within searches to mean *any character or series of characters*. 
	For example, the following query will return any string that starts with *how to hack* and ends with *using Google*. It will match with strings like *how to hack websites using Google, how to hack*
	*applications using Google*, and so on:
### Quotes (`" "`)

Adding quotation marks around you search terms **forces an exact match**. 
	For example, this query will search for pages that contain the phrase *how to hack: "how to hack"*. And this query will search for pages with the terms *how*, *to*, *hack*, although not necessarily together: `how to hack`.
### Or (`|`)

The or operator is denoted with the pipe character (`|`) and can be used to search for one search term or the other, or both at the same time. The pipe character must be surrounded by spaces. For example, this query will search for *how to hack* on either Reddit or Stack Overflow: `"how to hack" site(reddit.com | stackoverflow.com)`. And this query will search for web pages that mention either *SQL Injection* or *SQLi: (`SQL Injection | SQLi)`*. SQLi is an acronym often used to refer to SQL injection attacks, which we'll talk about in Chapter 11.
### Minus (`-`)

The minus operator (`-`) excludes certain search results. For example, let's say you're interested in learning about websites that discuss hacking, but not those that discuss hacking PHP. This query will search for pages that contain *how to hack websites* but not *php: "how to hack websites" -php*

You can use advanced search engine options in many more ways to make your work more efficient. You can even search for the term *Google search operators* to discover more. These operators can be more useful than you'd expect. For example, look for all of a company's subdomains by searching as follows:

```
site:*.example.com
```

You can also look for special endpoints that can lead to vulnerabilities. *Kibana* is a data visualization tool that displays server operation data such as server logs, debug messages, and server status. A compromised Kibana instance can allow attackers to collect extensive information about a site's query will reveal whether the target has a Kibana dashboard. You can them try to access the dashboard to see if it's unprotected:

```
site:example.com inurl:app/kibana
```

Google can find company resources hosted by a third part online, such as Amazon S3 buckets.

```
site:s3.amazonaws.com COMPANY_NAME
```

Look for special extensions that could indicate a sensitive file. In addition to `.log`, which often indicates log files, search for `.php`, `.cfm`, `.asp`, `.jsp` and `.pl` the extensions often used for script files:

```
site:example.com ext:php 
site:example.com ext:log 
```

Finally, you can also combine search terms for a more accurate search. 
	For example, this query searches the site *example.com* for text files that contain *password*:

```
site:example.com ext:txt password
```

In addition to constructing your own queries, check out the Google Hacking Database (https://www.exploit-db.com/google-hacking-database/), a website that hackers and security practitioners use to share Google search queries for finding security-related information. It contains many search queries that could be helpful to you during the recon process. 
	For example, you can find queries that look for files containing passwords, common URLs of admin portals, or pages built using vulnerable software.

While you are performing recon using Google search, keep in mind that if you're sending a lot of search queries, Google will start requiring CAPTCHA challenges for visitors from your network before they can perform more searches. This could be annoying to others on your network, so I don't recommend Google dorking on a corporate or shared network.
## Scope Discovery

Let's now dive into recon itself. 

First, **always verify the target's scope**. A program's ***scope*** on its policy page specifies which subdomains, products, and applications you're allowed to attack. Carefully verify which of the company's assets are in scope to avoid overstepping boundaries during the recon and hacking process. 
	For example, if `www.example.com`'s policy specifies that `dev.example.com` and `test.example.com` are out of scope, you shouldn't perform any recon or attacks on those subdomains.

- Which domains, subdomains, and IP addresses can you attack? 
- What company assets is the organization hosting on these machines?
### WHOIS and Reverse WHOIS

When companies or individuals register a domain name, they need to supply identifying information, such as their:

- mailing address
- phone number
- email address

to a domain registrar. Anyone can then query this information by using the `whois` command, which searches for the registrant and owner information of each known domain. You might be able to find the associated contact information, such as email, name, address, or phone number:

```
whois facebook.com
```

The information is not always available, as some organization and individuals use a service called ***domain privacy***, in which a third-party service provider replaces the user's information with that of a forwarding service. 

You could then conduct a *reverse WHOIS* search, searching a database by using:

- an organization name
- phone number
- email address

to find domains registered with it. This way, you can find all the domains that belong to the same owner. Reverse WHOIS is extremely useful for finding *obscure or internal domains not otherwise*
*disclosed to the public*.

Use a public reverse WHOIS tool like (https://viewdns.info/reversewhois/) to conduct this search. WHOIS and reverse WHOIS will give you a good set of top-level domains to work with.
### IP Addresses

Another way of discovering your target's top-level domains is to locate IP addresses. Find the IP address of a domain you know by running the `nslookup` command. You can see here that *facebook* is located at `157.240.2.35`:

```bash
nslookup facebook.com
Server:         192.168.1.254
Address:        192.168.1.254#53

Non-authoritative answer:
Name:   facebook.com
Address: 31.13.93.35
Name:   facebook.com
Address: 2a03:2880:f134:183:face:b00c:0:25de
```

Once you've found the IP address of the known subdomain, perform a reverse IP lookup. ***Reverse IP searches*** look for domains hosted on the same server, given an IP or domain. 

Run the `whois` command on an IP address, and then see if the target has a dedicated IP range by checking the `NetRange` field. An `IP Range` is a block of IP addresses that all belong to the same organization. If the organization has a dedicated IP range, any IP you find in that range belongs to that organization:

```bash
jason@nixos ~ ❯ whois 31.13.93.35
% This is the RIPE Database query service.
% The objects are in RPSL format.
%
% The RIPE Database is subject to Terms and Conditions.
% See https://docs.db.ripe.net/terms-conditions.html

% Note: this output has been filtered.
%       To receive output for a database update, use the "-B" flag.

% Information related to '31.13.64.0 - 31.13.127.255'

% Abuse contact for '31.13.64.0 - 31.13.127.255' is 'domain@fb.com'

inetnum:        31.13.64.0 - 31.13.127.255
netname:        IE-FACEBOOK-20110418
country:        IE
org:            ORG-FIL7-RIPE
admin-c:        NE1880-RIPE
tech-c:         NE1880-RIPE
status:         ALLOCATED PA
mnt-by:         RIPE-NCC-HM-MNT
mnt-by:         meta-mnt
mnt-routes:     fb-neteng
created:        2011-04-18T12:00:34Z
last-modified:  2022-10-29T00:51:39Z
source:         RIPE # Filtered

organisation:   ORG-FIL7-RIPE
org-name:       Meta Platforms Ireland Limited
country:        IE
org-type:       LIR
address:        Merrion Road Dublin 4
address:        D04 X2K5
address:        Dublin
address:        IRELAND
phone:          +353 1443 4342
phone:          +0016505434800
fax-no:         +0016505435325
admin-c:        PH4972-RIPE
mnt-ref:        RIPE-NCC-HM-MNT
mnt-ref:        meta-mnt
mnt-by:         RIPE-NCC-HM-MNT
mnt-by:         meta-mnt
abuse-c:        RD4299-RIPE
created:        2011-04-07T13:16:29Z
last-modified:  2024-04-29T09:07:11Z
source:         RIPE # Filtered

role:           Network Engineering
address:        4 GRAND CANAL SQUARE, GRAND CANAL HARBOUR, DUBLIN, IRELAND
nic-hdl:        NE1880-RIPE
mnt-by:         fb-neteng
mnt-by:         facebook-neteng
created:        2022-05-19T14:17:28Z
last-modified:  2022-05-19T14:17:28Z
source:         RIPE # Filtered

% This query was served by the RIPE Database Query Service version 1.115 (BUSA)
```

Another way of finding IP addresses in scope is by *looking at autonomous systems*, which are routable networks within the public internet. *Autonomous system numbers (ASNS)* identify the owners of these networks. By checking if two IP addresses share an ASN, you can determine whether the IP addresses belong to the same owner. 

To figure out if a company owns a dedicated IP range, run several IP-to-ASN translations to see if the IP addresses map to a single ASN. If many addresses within a range belong to the same ASN, the organization might have a dedicated IP range. From the following output, we can deduce that any IP within the `157.240.2.21` to `157.240.2.34` range probably belongs to Facebook:

The -h flag in the whois command sets the WHOIS server to retrieve information from, and `whois.cymru.com` is a database that translates IPs to ASNs. If the company has a dedicated IP range and doesn’t mark those addresses as out of scope, you could plan to attack every IP in that range.
### Certificate Parsing

Another way of finding hosts is to take advantage of the Secure Sockets Layer (SSL) certificates used to encrypt web traffic. An SSL certificate's *Subject Alternative Name* field lets certificate owners specify additional hostnames that use the same certificate, so you can find those hostnames by parsing this field. 

Use online databases like:

- crt.sh
- Censys
- Cert Spotter

to find certificates for a domain.

For example, by running a certificate search using `crt.sh` for *facebook.com*, we can find Facebook's SSL certificate. You'll see that many other domain names belonging to Facebook are listed:

```
X509v3 Subject Alternative Name: 
DNS:*.facebook.com 
DNS:*.facebook.net 
DNS:*.fbcdn.net 
DNS:*.fbsbx.com 
DNS:*.messenger.com 
DNS:facebook.com 
DNS:messenger.com 
DNS:*.m.facebook.com 
DNS:*.xx.fbcdn.net 
DNS:*.xy.fbcdn.net 
DNS:*.xz.fbcdn.net
```

The `crt.sh` website also has a useful utility that lets you retrieve the information in JSON format, rather than HTML, for easier parsing. Just add the URL parameter `output=json` to the request URL: *`https://crt.sh/?q=facebook.com&output=json.`*
### Subdomain Enumeration

After finding as many domains on the target as possible, locate as many subdomains on those domains as you can. Each subdomain **represents a new angle for attacking the network**. The best way to enumerate subdomains is to use automation. 

Tools that are useful for `subdomain enumeration`:

- `Sublist3r`
- `SubBrute`
- `Amass`
- `Gobuster`

These tools enumerate subdomains automatically with a variety of wordlists and strategies.

For example, Sublist3r works by querying search engines and online subdomain databases, while SubBrute is a brute-forcing tool that guesses possible subdomains until it finds real ones. Amass uses a combination of DNS zone transfers, certificate parsing, search engines, and subdomain databases to find subdomains. 

> You can build a tool that combines the results of multiple tools to achieve the best results. We'll discuss how to do this in "Writing your own Recon Scripts" on Page 80.

To use many subdomain enumeration tools, you need to feed the program a wordlist of terms likely to appear in subdomains. You can find some good wordlists made by other hackers online. Daniel Miessler's SecLists is a pretty extensive one. 

You can also use a wordlist generation tool like `Commonspeak2` (https://github.com/assetnote/commonspeak2/) to generate wordlists based on the most current internet data. Finally you can combine several wordlists found online or that you generated yourself for the most comprehensive results. Here's a simple command to duplicate items from a set of two wordlists:

```
sort -u wordlist1.txt wordlist2.txt
```

The `sort` command line tools sorts lines of text files. When given multiple files, it will sort all files and write the output to the terminal. The `-u` option tells `sort` to return only unique items in the sorted list. 

**`Gobuster`** is a tool for *brute-forcing* to discover subdomains, directories, and files on target web servers. Its DNS mode is used for subdomain bruteforcing. In this mode, you can use the flag `-d` to specify the domain you want to brute-force and `-w` to specify the wordlist you want to use.

```bash
gobuster dns -d target_domain -w wordlist
```

Once you've found a good number of subdomains, you can discover more by identifying patterns. For example, if you find two subdomains to *example.com* named *1.example.com* and *3.example.com*, you can guess that *2.example.com* is probably a valid subdomain. A good tool for automating this process is `Altdns` (https://github.com/infosec-au/altdns/), which discovers subdomains with names that are permutations of other subdomain names.

Technology stacks can also provide clues to valid subdomains within an organization. If a company uses Jenkins, you can check if `jenkins.example.com` is a valid domain.

> Also, look for subdomains of subdomains. After you've found, say `dev.example.com`, you might find subdomains like `1.dev.example.com`. You can find subdomains of subdomains by running enumeration tools recursively: add the results of your first run to your Known Domains list and run the tool again.
### Service Enumeration

Next, enumerate the services hosted on the machines you've found. Since services often run on **default ports**, a good way to find them is by port-scanning the machine with either active or passive scanning.

In *`active scanning`*, you directly engage with the server. Active scanning tools send requests to connect to the target machine's ports to look for open ones. You can use tools like `Nmap` or `Masscan` for active scanning. 

```bash
jason@nixos ~ ❯ nmap scanme.nmap.org
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-31 10:34 CST
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.039s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
Not shown: 991 closed tcp ports (conn-refused)
PORT      STATE    SERVICE
22/tcp    open     ssh
25/tcp    filtered smtp
80/tcp    open     http
111/tcp   filtered rpcbind
135/tcp   filtered msrpc
139/tcp   filtered netbios-ssn
445/tcp   filtered microsoft-ds
9929/tcp  open     nping-echo
31337/tcp open     Elite

Nmap done: 1 IP address (1 host up) scanned in 2.12 seconds
```

On the other hand, in *`passive scanning`*, you use third party resources to learn about a machine's ports **without interacting with the server**. Passive reconnaissance is stealthier and helps attackers avoid detection. To find services on a machine without actively scanning it, you can use `Shodan`, a search engine that lets the user find machines connected to the internet.

With Shodan, you can discover the presence of webcams, web servers, or even power plants based on criteria such as hostnames or IP addresses. For example, if you run a Shodan search on *scanme.nmap.org*'s IP address, `43.33.32.156`, you get the result below. You can see that the search yields different data than our port scan, and provides additional information about the server.

![](https://i.imgur.com/dQ0zESc.png)

Alternatives to Shodan:

- Censys
- Project Sonar

Combining your findings with other databases can improve your results. You can find IP addresses, certificates and software versions that may not be found on the other databases.
### Directory Brute-Forcing

The next thing you can do to discover more of the site's attack surface is brute-forcing the directories of the web servers you've found. Finding directories of the web servers you've found. Finding directories on servers is valuable, because through them, you might discover hidden admin panels, configuration files, password files, outdated functionalities, database copies, and source code files. Directory brute-forcing can sometimes allow you to **directly take over a server**!

Even if you can't find any immediate exploits, directory information often tells you about the structure and technology of an application.

A pathname that includes `phpmyadmin` usually means the application is built with PHP.

You can use `Dirsearch` or `Gobuster` for directory brute-forcing. These tools use wordlists to construct URLs, and then request these URLs from a web server. If the server responds with a status code in the 200 range, the directory or file exists. This means you can browse to the page and see what the application is hosting there. 

A status code of 404 means that the directory or file doesn't exist, while 403 means it exists but is protected. Examine 403 pages carefully to see if you can bypass the protection to access the content. 

Here's an example of running a `Dirsearch` command. The `-u` flag specifies the hostname, and the `-e` flag specifies the file extension to use when constructing URLs:

```
$ ./dirsearch.py -u scanme.nmap.org -e php 
Extensions: php | HTTP method: get | Threads: 10 | Wordlist size: 6023 Error Log: /tools/dirsearch/logs/errors.log 
Target: scanme.nmap.org 
[12:31:11] Starting: 
[12:31:13] 403 - 290B - /.htusers 
[12:31:15] 301 - 316B - /.svn -> http://scanme.nmap.org/.svn/ [12:31:15] 403 - 287B - /.svn/ 
[12:31:15] 403 - 298B - /.svn/all-wcprops [12:31:15] 403 - 294B - /.svn/entries 
[12:31:15] 403 - 297B - /.svn/prop-base/ [12:31:15] 403 - 296B - /.svn/pristine/ 
[12:31:15] 403 - 291B - /.svn/tmp/ 
[12:31:15] 403 - 315B - /.svn/text-base/index.php.svn-base 
[12:31:15] 403 - 293B - /.svn/props/ 
[12:31:15] 403 - 297B - /.svn/text-base/ 
[12:31:40] 301 - 318B - /images -> http://scanme.nmap.org/images/ 
[12:31:40] 200 - 7KB - /index 
[12:31:40] 200 - 7KB - /index.html [12:31:53] 403 - 295B - /server-status 
[12:31:53] 403 - 296B - /server-status/ [12:31:54] 301 - 
```

Gobuster's `dir` mode is used to find additional content on a specific domain or subdomain. This includes *hidden directories* and files. In this mode, you can use the `-u` flag to specify the domain or subdomain you want to bruteforce and `-w` to specify the wordlist you want to use:

```
gobuster dir -u target_url -w wordlist
```

Manually visiting all the pages you've found through brute-forcing can be time-consuming. Instead, use a screenshot tool like:

- EyeWitness(https://github.com/FortyNorthSecurity/EyeWitness/) or 
- Snapper (https://github.com/dxa4481/Snapper/)

> to automatically verify that a page is hosted on each location. EyeWitness accepts a list of URLs and takes screenshots of each page. In a photo gallery app, you can quickly skim these to find the interesting looking ones. Keep an eye out for *hidden services*, such as **developer** or **admin** panels, directory listing pages, analytics pages, and pages that look outdated and ill-maintained. These are all common places for vulnerabilities to manifest. 
### Spidering the Site

Another way of discovering directories and paths is through `web spidering`, or `web crawling`, a process used to identify all pages on a site. A web spider tool starts with a page to visit. It then identifies all the URLs embedded on the page and visits them. By recursively visiting all URLs found on all pages of a site, the web spider can uncover many hidden endpoints in an application.

OWASP Zed Attack Proxy (ZAP) at https://www.zaproxy.org/ has a built-in web spider you can use. This open source security tool includes a scanner, proxy, and many other features.

Access its spider tool by opening ZAP and choosing `Tools > Spider`.

Once opened, you will see a window for specifying the starting URL. Enter a website, then press "start scan".

We should also see a site tree appear on the left side of the ZAP window. This shows the files and directories found on the target server in an organized format.
### Third Party Hosting

Take a look at the company's third-party hosting footprint. 
	For example, look for the organizations' S3 buckets. S3, which stands for `Simple Storage Service`, is Amazon's online storage product. Organizations can pay to store resources in *buckets* to serve in their web applications, or they can use S3 buckets as a backup or storage location. 

If an organization uses Amazon S3, its S3 buckets can contain:

- Hidden endpoints
- Logs
- Credentials
- User information
- Source code

How do you find an organization's buckets? One way is through google dorking, as mentioned earlier. Most buckets use the URL format `BUCKET.s3.amazonaws.com` or `s3.amazonaws.com/BUCKET`, so the following search terms are likely to find results:

```
site:s3.amazonaws.com COMPANY_NAME
site:amazonaws.com COMPANY_NAME
```

If the company uses custom URLs for its S3 buckets, try more flexible search terms instead. Companies often still place keywords like `aws` or `s3` in their custom bucket URLs.

```
amazonaws s3 COMPANY_NAME
amazonaws bucket COMPANY_NAME
amazonaws COMPANY_NAME
s3 COMPANY_NAME
```

Another way of finding buckets is to search a company's public GitHub repositories for S3 urls. 

GrayhatWarfare (https://buckets.grayhatwarfare.com/) is an online search engine you can use to find publicly exposed S3 buckets. It allows you to search for a bucket by using a keyword. Supply keywords related to your target, such as the application, project, or organization name, to find relevant buckets.

Finally, you can try to brute-force buckets by using keywords. `Lazys3` (https://github.com/nahamsec/lazys3/) is a tool that helps you do this. It relies on a wordlist to guess buckets that are permutations of common bucket names. 

Another good tool is `Bucket Stream` (https://github.com/eth0izzle/bucket-stream/), which parses certificates belonging to an organization and finds S3 buckets based on permutations of the domain names found on the certificates. Bucket Stream also automatically checks whether the bucket is accessible, so it saves you time. 

Once you've found a couple of buckets that belong to the target organization, use the AWS command line tool to see if you can access one. Install the tool by using the following command:

```
pip install awscli
```

Then configure it to work with AWS by following Amazon's documentation at https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html. Now you should be able to access buckets directly from your terminal via the `aws s3` command. Try listing the contents of the bucket you found:

```
aws s3 ls s3://BUCKET_NAME/
```

If this works, see if you can read the contents of any interesting files by copying files to your local machine:

```
aws s3 cp s3://BUCKET_NAME/FILE_NAME/path/to/local/directory
```

Gather any useful information leaked via the bucket and use it for future exploitation! If the organization reveals information such as **active API keys** or personal information, you should report this right away. Exposed S3 buckets alone are often considered a *vulnerability*. 

- You can try to upload new files to the bucket
- Delete files from the bucket
- Mess with the contents of the bucket
- Tamper with the web application's operations or corrupt company data.

For example, this command will copy your local file named `TEST_FILE` into the target's S3 bucket:

```
aws s3 cp TEST_FILE s3://BUCKET_NAME/
```

And this command will remove the TEST_FILE that you just uploaded:

```
aws s3 rm s3://BUCKET_NAME/TEST_FILE
```

These commands are a harmless way to prove that you have write access to a bucket without actually tampering with the target company's files. Always upload and remove your own test files. Don't risk deleting important company resources during your testing unless you're willing to entertain a costly lawsuit. 
### GitHub Recon

Search an organization's GitHub repositories for sensitive data that has accidentally been committed, or information that could lead to the discovery of a vulnerability.

Start by finding the GitHub usernames relevant to your target. You should be able to locate these by searching the organization's name or product names in Github's search bar, or by checking the Github accounts of known employees. 

- Find usernames to audit
- Visit those pages
- Find repos related to projects you're testing and record them, along with the usernames of the organization's top contributors
- Dive into the code.
	- For each repository, pay special attention to the **Issues and Commits** sections. 
	- These sections are full of potential info leaks:
		- Unresolved bugs
		- Problematic code
		- Most recent code fixes and security patches

Recent code changes that haven't stood the test of time are more likely to contain bugs. Look at any protection mechanisms implemented to see if you can bypass them. You can also search the Code section for potentially vulnerable code snippets. 

- Check the `Blame` and `History` sections at the top-right corner of the file's page to see how it was developed.
#### Things to Look For:

- Hardcoded API keys
- Encryption keys
- Database passwords
- Look for terms like:
	- `Key`
	- `Secret`
	- `Password`

Once you've found credentials, you can use `KeyHacks` (https://github.com/streaak/keyhacks/) to check if the credentials are valid and learn how to use them to access the target's services. 

You should also search for sensitive functionalities in the project. See if any of the source code deals with important functions such as authentication, password reset, state-changing actions, or private info reads. 

Pay attention to code that deals with user input, such as:

- `HTTP request params`
- `HTTP headers`
- `HTTP request paths`
- `database entries`
- `file reads`
- `file uploads`

These provide *potential entry points* for attackers to exploit the application's vulnerabilities. Look for any **configuration files**, as they allow you to gather more information about your infrastructure. Also, search for old endpoints and S3 bucket URLs that you can attack. Record these files for further review in the future.

***Outdated Dependencies*** and the unchecked use of dangerous functions are also a *huge source* of bugs. Pay attention to dependencies and imports being used and go through the versions list to see if they're outdated. 

- Record any outdated dependencies
- You can use this information later to look for publicly disclosed vulnerabilities that would work on your target. 

Tools like Gitrob and TruffleHog can automate the GitHub recon process. Gitrob (https://github.com/michenriksen/gitrob/) locates potentially sensitive files pushed to public repositories on GitHub. TruffleHog (https://github.com/trufflesecurity/truffleHog/) specializes in finding secrets in repositories by conducting regex searches and scanning for high-entropy strings.
## Other Sneaky OSINT Techniques

1. Check the company's job posts for engineering positions
	- Engineering job listing often reveal the technologies the company uses. 

```
Full Stack Engineer 
	Minimum Qualifications: Proficiency in Python and C/C++ 
	Linux experience 
	Experience with Flask, Django, and Node.js 
	Experience with Amazon Web Services, especially EC2, ECS, S3, and RDS
```

From this job post alone:

- The company uses Python, C/C++
- Uses Node.js, Flask and Django to build it's web applications.
- They use Linux as a backend machine
- Outsource to AWS for their operations and cloud storage.

2. Search for employee's profiles on LinkedIn. and read employee's personal blogs or their engineering questions on forums like StackOverflow and Quora.
	 - The expertise of a company's top employees often reflects the technology used in development. 

3. Employee Google Calendars. People's work calendars often contain meeting notes, slides, and sometimes even login credentials. 
	- If an employee shares their calendars with the public by accident, you could gain access to these. The organization or it's employees' social media pages might also leak valuable information. 
	- Hackers have actually discovered sets of valid credentials on Post-it Notes visible in the background of office selfies. 

4. Sign up for the company's engineering mailing list, to gain insight into the company's SlideShare or Pastebin accounts. Sometimes, when organizations present at conferences or have internal meetings, they upload slides to SlideShare for reference. You might be able to find information about the technology stack and security challenges faced by the company. 

Pastebin (https://pastebin.com/) is a website for pasting and storing text online for a short time. People use it to share text across machines or with others. Engineers sometimes use it to share source code or server logs with their colleagues for viewing or collaboration, so it could be a great source of information. You might also find uploaded credentials and development comments. Go to Pastebin, search for the target’s organization name, and see what happens! You can also use automated tools like PasteHunter (https://github.com/kevthehermit/PasteHunter/) to scan for publicly pasted data.

Lastly, consult archive websites like the Wayback Machine (https:// archive.org/web/), a digital record of internet content. It records a site’s content at various points in time. Using the Wayback Machine, you can find old endpoints, directory listings, forgotten subdomains, URLs, and files that are outdated but still in use. Tomnomnom’s tool Waybackurls (https://github.com/tomnomnom/waybackurls/) can automatically extract end- points and URLs from the Wayback Machine.
## Tech Stack Fingerprinting

**Fingerprinting** techniques can help you understand the target application even better. ***Fingerprinting*** is identifying the software brands and versions that a machine or application uses. This information allows you to perform targeted attacks on the application, because you can search for any known misconfigurations and publicly disclosed vulnerabilities related to a particular version.

The security community classifies known vulnerabilities as *Common Vulnerabilities and Exposures* (CVEs) and gives each CVE a number for reference.

They can be searched on the **CVE Database**: (https://cve.mitre.org/cve/search_cve_list.html).

The simplest way to of fingerprinting an application is to **engage with the application directly**. First, run `nmap` on a machine with the `-sV` flag on to enable version detection on the port scan. Here, you can see that Nmap attempted to fingerprint some software running on the target host four us:

```bash
jason@nixos ~ ❯ nmap -sV scanme.nmap.org
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-04 21:03 CST
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.039s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
Not shown: 991 closed tcp ports (conn-refused)
PORT      STATE    SERVICE      VERSION
22/tcp    open     ssh          OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.13 (Ubuntu Linux; protocol 2.0)
25/tcp    filtered smtp
80/tcp    filtered http
111/tcp   filtered rpcbind
135/tcp   filtered msrpc
139/tcp   filtered netbios-ssn
445/tcp   filtered microsoft-ds
9929/tcp  open     nping-echo   Nping echo
31337/tcp open     tcpwrapped
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 3.61 seconds
```

In Burp, you can send an HTTP request to the server to check the HTTP headers used to gain insight into the tech stack. A server might leak many pieces of information useful for fingerprinting its technology:

```
Server: Apache/2.0.6 (Ubuntu) 
X-Powered-By: PHP/5.0.1 
X-Generator: Drupal 8 
X-Drupal-Dynamic-Cache: UNCACHEABLE 
Set-Cookie: PHPSESSID=abcde;
```

HTTP headers like `Server` and `X-Powered-By` are good indicators of technologies. The `Server` header often reveals the software versions running on the server. `X-Powered-By` reveals the server or scripting language used. Also, certain headers are used only by specific technologies;

- Only Drupal uses `X-Generator` and `X-Drupal-Dynamic-Cache`.
- Technology specific cookies such as `PHPSESSID` are also clues; if a server sends back a cookie named `PHPSESSID`, it's probably developed using PHP.

The HTML source code of web pages can also provide clues. Many web frameworks or other technologies will embed a signature in the source code. Right-click a page, select **View Source Code**, and press **CTRL+F** to search for phrases like:

- powered by
- built with
- running

For instance, you might find `Powered by: WordPress 3.3.2` written in the source.

Check technology specific file extensions, filenames, folders and directories. 
	For example, a file named `phpmyadmin` at the root directory, like `https://example.com/phpmyadmin`, means the application runs PHP. A directory named `jinja2` that contains templates means the site probably uses `Django` and `Jinja2`. 

Several applications can automate this process. 

- `Wappalyzer`: https://wwwwappalyzer.com/ is a browser extension that identifies **content-management systems**, **frameworks** and **programming languages** used on a site. 
- `BuiltWith`: (https://builtwith.com/) is a website that shows you which web technologies a site is built with. 
- `StackShare`: (https://stackshare.io/) is an online platform that allows developers to share the tech they use. 
- `Retire.js` is a tool that detects outdated JavaScript libraries and Node.js packages.

You can use it to check for outdated technologies on a site.
## Writing Your Own Recon Scripts

> Good recon is an ***extensive process***. 

It doesn't have to be time consuming or hard to manage. We've already discussed several tools that use the power of automation to make the process easier. 

Sometimes, it may be easier to write your own scripts. A ***script*** is a list of commands designed to be executed by a program. They're used to automate tasks such as:

- data analysis
- web-page generation
- system administration

Scripting is a quick way of performing recon, testing, and exploitation. For example, you could write a script to scan a target for new subdomains, or enumerate potentially sensitive files and directories on a server. 

Bash scripts, or any type of shell script, are useful for managing complexities and automating recurring tasks. If your commands involve multiple input parameters, or if the input of one command depends on the output of another, entering it all manually could get complicated quickly and increase the chance of a programming mistake. 
	On the other hand, you might have a list of commands that you want to execute many many times. 
### Understanding Bash Scripting Basics

```bash
#!/bin/bash
nmap scanme.nmap.org
/PATH/TO/diresearch.py -u scanme.nmap.org -e php
```

1. The first line of any script should be a ***shebang line***. It starts with a hash mark `#`, and then an exclamation mark `!`, and it declares the `interpreter` for the script.
2. This allows the plaintext file to be executed like a binary.

The above script isn't very useful, as it can only scan one site: `scanme.nmap.org`. 

Instead, we should let users input arguments to the bash script so they can choose the site to scan. In bash syntax, `$1` represents the first argument passed in, `$2` is the second argument, and so on. 

Also, `$@` represents all arguments passed in, while `$#` represents the total number of arguments. Let's allow users to specify their targets with the first input argument, assigned to the variable `$1`:

```bash
#!/bin/bash
nmap $1
/path/to/dirsearch.py -u $1 -e php
```

Now the commands will execute for whatever domain the user passes in as the first argument. 

Replace `/path/to/dirsearch.py` with the *absolute path* of the directory where your stored the Dirsearch script. If you don't specify it's location, your computer will try to look in the same directory as the shell script, and won't find it. 

Another way of making sure that your script can find the commands to use it through the `PATH` variable, an environmental variable in Unix systems that specifies where executable binaries are found. If you run this command to add Dirsearch to your path, you can run the tool from anywhere without needing to specify its absolute path:

```
export PATH="PATH_TO_DIRSEACH:$PATH"
```

Note that you will have to run the export command again after you restart your terminal for your PATH to contain the path to Dirsearch. If you don’t want to export PATH over and over again, you can add the export command to your `~/.bash_profile` file, a file that stores your bash preferences and configuration. You can do this by opening `~/.bash_profile` with your favorite text editor and adding the export command to the bottom of the file. The script is complete! Save it in your current directory with the filename `recon.sh.` The .sh extension is the conventional extension for shell scripts. Make sure your terminal’s working directory is the same as the one where you’ve stored your script by running the command `cd /location/of/your/script.` Execute the script in the terminal with this command:

```
./recon.sh
```

If you see something like this:

```
permission denied: ./recon.sh
```

Your current user doesn't have permission to execute the script. For security purposes, most files aren't executable by default. You can correct this behavior by adding execution rights for everyone by running this command in the terminal:

```
$ chmod +x recon.sh
```

The `chmod` command edits the permissions for a file, and `+x` indicates that we want to add the permission to execute for all users. If you'd like to grant executing rights for the owner of the script only, use this command instead:

```
$ chmod 700 recon.sh
```

Now run the script as we did before. Try passing in `scanme.nmap.org` as the first argument. You should see the output of the Nmap and Dirsearch printed out.
### Saving Tool Output to a File

To analyze results alter, you may want to save your script's output in a separate file. This is where input and output redirection come into play. `Input Redirection` is using the content of a file, or the output of another program, as the input to your script. `Output Redirection` is redirecting the output of a program to another location, such as to a file or another program. 

```
PROGRAM > FILENAME
```
> Writes the program's output into the file with that name. 

```
PROGRAM >> FILENAME
```
> Appends the output of the program to the end of the file, without clearing the file's contents.

```
PROGRAM < FILENAME
```
> Reads from the file and uses its content as the program input.

```
PROGRAM1 | PROGRAM2
```
> Uses the output of `PROGRAM1` as the input to `PROGRAM2`

```
#!/bin/bash 
echo "Creating directory $1_recon." 1 
mkdir $1_recon 2 
nmap $1 > $1_recon/nmap 3 
echo "The results of nmap scan are stored in $1_recon/nmap." /PATH/TO/dirsearch.py -u $1 -e php 4 --simple-report=$1_recon/dirsearch echo "The results of dirsearch scan are stored in $1_recon/dirsearch."
```

1. The `echo` command prints a message to the terminal.
2. Next, `mkdir` creates a directory with the name `DOMAIN_recon`. We store the results of `nmap` into a file named `nmap` in the newly created directory. 
3. Dirsearch's `simple-report` flag generates a report in the designated location.
4. We store the results of Dirsearch to a file named `dirsearch` in the new directory.

You can make the script more manageable by *introducing variables* to reference files, names, and values. Variables in bash can be assigned using the following syntax: `VARIABLE_NAME=VARIABLE_VALUE`. Note that there should be **no spaces** around the equal sign. 

```bash
#!/bin/bash
PATH_TO_DIRSEARCH="/Users/jkimm/tools/dirsearch"
DOMAIN=$1
DIRECTORY=${DOMAIN}_recon
echo "Creating directory $DIRECTORY."
mkdir $DIRECTORY
nmap $DOMAIN > $DIRECTORY/nmap
echo "the results of nmap scan are stored in $DIRECTORY/nmap."
$PATH_TO_DIRSEARCH/dirsearch.py -u $DOMAIN -e php -simple-report=$DIRECTORY/dirsearch
echo "The results of dirsearch scan are stored in $DIRECTORY/dirsearch."
```

1. We use the `${DOMAIN}_recon` instead of `$DOMAIN_recon` because, otherwise, bash would recognize the entirety of `DOMAIN_recon` as the variable name. The curly brackets tell bash that `DOMAIN` is the **variable name**, and `_recon` is the plaintext we're appending it to. 
2. Notice that we also stored the path to Dirsearch in a variable to make it easier to change in the future. 

> Using redirection, we can now write shell scripts that run many tools in a single command and save their outputs in separate files.
### Adding the Date of the Scan to the Output

Let's say we want to add the current date to your script's output, or select which scans to run, instead of always running both Nmap and Dirsearch. If you want to write tools with more functionalities like this, you have to understand some advanced shell scripting concepts. 

A useful one is ***command substitution***, or operating on the output of a command. Using `$()` tells Unix to execute the command surrounded by the parenthesis and assign its output to the value of a variable. 

```bash
#!/bin/bash
PATH_TO_DIRSEARCH="/Users/jkimm/tools/dirsearch"
TODAY=$(date)
echo "This scan was created on $TODAY"
DOMAIN= $1
DIRECTORY=${DOMAIN}_recon
echo "Creating directory $DIRECTORY."
mkdir $DIRECTORY
nmap $DOMAIN > $DIRECTORY/nmap
echo "The results of nmap scan are stored in $DIRECTORY/nmap."
$PATH_TO_DIRSEARCH/dirsearch.py -u $DOMAIN -e php --simple-report=$DIRECTORY/dirsearch
echo "The results of dirsearch scan are stored in $DIRECTORY/dirsearch."
```

1. We assign the output of the `date` command to the variable `TODAY`. The date command displays the current date and time. This lets us output a message indicating the day on which we performed the scan.
### Adding Options to Choose the Tools to Run

To selectively run only certain tools, you need to use conditionals. In bash, the syntax of an `if` statement is as follows. Note that the conditional statement ends with the `fi` keyword, which is `if` backwards.

```bash
if [ condition 1 ]
then
  # Do if condition is satisfied
elif [ condition 2 ]
then
  # Do if condition 2 is satisfied, and condition 1 is not
else
  # Do something else if neither condition is satisfied
fi
```

Let's say we want users to be able to specify the scan `MODE`, as such:

```
$ ./recon.sh scanme.nmap.org MODE
```

We can implement it like this:

```bash
#!/bin/bash
PATH_TO_DIRSEARCH="/users/jkimm/tools/dirsearch"
TODAY=$(DATE)
echo "This scan was created on $TODAY"
DIRECTORY=${DOMAIN}_recon
echo "Creating directory $DIRECTORY."
mkdir $DIRECTORY
if [ $2 == "namp-only" ]
then
  nmap $DOMAIN > $DIRECTORY/nmap
  echo "The results of nmap scan are stored in $DIRECTORY/nmap."
elif [ $2 == "dirsearch-only" ]
then
  $PATH_TO_DIRSEARCH/dirsearch.py -u $DOMAIN -e php -simple-report=$DIRECTORY/dirsearch
  echo "The results of dirsearch scan are stored in $DIRECTORY/dirsearch."
else
  nmap $DOMAIN > $DIRECTORY/nmap
  echo "The results of nmap scan are stored in $DIRECTORY/nmap."
  $PATH_TO_DIRSEARCH/dirsearch.py -u $DOMAIN -e php --simple-report=$DIRECTORY/dirsearch
  echo "The results of dirsearch are stored in $DIRECTORY/dirsearch."
fi
```

1. If the user specifies `nmap-only`, we run `nmap` only and store the results to a file named `nmap`.
2. If the user specifies `dirsearch-only`, we execute and store the results of Dirsearch only. 
3. If the user specifies neither, we run both scans.

```
./recon.sh scanme.nmap.org nmap-only
./recon.sh scanme.nmap.org dirsearch-only
```
### Running Additional Tools

What if you want the option of retrieving information from the crt.sh tool, as well? For example, you want to switch between these three modes or run all three recon tools at once:

```
$ ./recon.sh scanme.nmap.org nmap-only 
$ ./recon.sh scanme.nmap.org dirsearch-only 
$ ./recon.sh scanme.nmap.org crt-only
```

We could rewrite the `if-else` statements to work with three options:

1. We check if `MODE` is `nmap-only`. 
2. Then we check if `MODE` is `dirsearch-only`
3. finally if `MODE` is `crt-only`. 

But that's a lot of `if-else` statements, making the code complicated. 

Instead, let's use bash's `case` statements, which allow you to match several values against one variable without going through a long list of `if-else` statements. The syntax of case statements looks like this. Note that the statement ends with `esac`, or `case` backwards.




