---
title: "Finding my First SQL Injection On HackerOne"
source: "https://infosecwriteups.com/finding-my-first-sql-injection-on-hackerone-6a031ab5aa1c"
author:
  - "[[Aleksa Zatezalo]]"
published: 2025-01-19
created: 2025-01-25
description: "SQL injections have been a persistent aspect of web application security, maintaining their position on OWASP’s top 10 vulnerabilities year after year. Like an old adversary that refuses to be…"
tags:
  - "clippings"
---
The vulnerability I discovered centers on a critical parameter injection in Itaú Cultural’s agenda system. When users interact with [www.itaucultural.org.br/agenda-cultural](http://www.itaucultural.org.br/agenda-cultural), the application makes backend requests to [www.prod-conteudo-portal-ic-2022.i-nove.org](http://www.prod-conteudo-portal-ic-2022.i-nove.org/) for certain operations. During my testing, I identified that the ‘tag’ parameter in requests to the backend server was vulnerable to time-based SQL injection. This allowed me to execute SQL commands on the underlying MySQL database hosted on prod-conteudo-portal-ic-2022.i-nove.org. While time-based SQL injections can be more challenging to exploit compared to their error-based or union-based counterparts, they still present significant security concerns. Despite multiple attempts to expand the exploitation scope, I was limited to time-based techniques and couldn’t achieve broader access to the database. In the following sections, I’ll walk through the exact steps to reproduce this vulnerability and explain the technical details of the injection point.

**Note:** *The vulnerability has been resolved as of this publication. It was part of a vulnerability disclosure program and did not pay out any bounties.*

## Steps to identification

I started by accessing [www.itaucultural.org.br](http://www.itaucultural.org.br/) and proxying data through Burpsuite Pro. After accessing [www.itaucultural.org.br/agenda-cultural](http://www.itaucultural.org.br/agenda-cultural), I noticed numerous search requests made to [www.prod-conteudo-portal-ic-2022.i-nove.org](http://www.prod-conteudo-portal-ic-2022.i-nove.org/) with search terms ‘site’ and ‘tag’ included as URL parameters. The HTTP history involving [www.itaucultural.org.br/agenda-cultural](http://www.itaucultural.org.br/agenda-cultural) and [www.prod-conteudo-portal-ic-2022.i-nove.org](http://www.prod-conteudo-portal-ic-2022.i-nove.org/) is seen on the highlighted lines below (299 and 345).

![](https://miro.medium.com/v2/resize:fit:875/1*l3mmHrT9zkkOUy1wiIqjew.png)

API calls originaitng from itaucultural

Sending a request to Burp’s repeater that queries [www.prod-conteudo-portal-ic-2022.i-nove.org](http://www.prod-conteudo-portal-ic-2022.i-nove.org/) for podcast content returns a large response containting data in a JSON format indicating that the request might be retrieving data from a database.

![](https://miro.medium.com/v2/resize:fit:875/1*Ca5yoDuyheAgQ7dBNZdSqg.png)

JSON Response containing Data

Adding a single quote (‘) to the end of the tag parameter returns Status Code 500 as seen below, indicating that the parameter tag is passed directly to an SQL query without parameterization.

![](https://miro.medium.com/v2/resize:fit:875/1*dj-JBapOWqbcCh6ilzZ2qw.png)

SQL injection confirmed

Adding a URL-encoded, time-based SQLi (*“‘ and (select\*from(select(sleep(20)))a) — “*) to the tag parameter, delays the response in proportion to the time included in the query indicating an SQLi. As seen in the screenshot below, the Referer for [www.prod-conteudo-portal-ic-2022.i-nove.org](http://www.prod-conteudo-portal-ic-2022.i-nove.org/) is [https://www.itaucultural.org.br/](https://www.itaucultural.org.br/) indicating that [www.prod-conteudo-portal-ic-2022.i-nove.org](http://www.prod-conteudo-portal-ic-2022.i-nove.org/) represents a back-end data retrieval service for [www.itaucultural.org.br](http://www.itaucultural.org.br/).

![](https://miro.medium.com/v2/resize:fit:875/1*JA76gzHfNYG8ldx4VW9l-g.png)

SQL injection impact demonstrated

## Impact

The identified time-based SQL injection vulnerability allows an attacker to interact directly with the backend database by injecting arbitrary SQL queries into the vulnerable parameter. This can lead to the following potential security risks described below.

**Database Enumeration:** Attackers can infer sensitive information about the database structure, such as table names, column names, and other metadata, by exploiting time delays in the response.

**Privilege Escalation:** If exploited further, the vulnerability may reveal critical information about user roles and privileges, potentially allowing attackers to identify superuser accounts or administrative credentials.

**Data Extraction:** By chaining this vulnerability with advanced techniques, attackers can exfiltrate sensitive data such as usernames, passwords, or personally identifiable information (PII) from the database without triggering alarms.

**Denial of Service (DoS):** An attacker can abuse database queries to introduce significant delays in database responses, impacting the application’s performance and potentially leading to a denial of service for legitimate users.

**Reputation and Compliance Risks:** Exposing sensitive data or impacting application availability can result in non-compliance with regulations such as GDPR, HIPAA, or PCI-DSS, leading to reputational damage and financial penalties. This vulnerability demonstrates a lack of proper input validation and parameterized query usage, leaving the application susceptible to severe exploitation risks. Immediate remediation is advised to prevent potential misuse.

## Key Lessons for Bug Bounty Hunters

Bug hunting success often comes down to methodology and tooling — this finding reinforced two critical practices that have consistently yielded results in my experience. First, always pay attention to backend API calls. While testing web applications, I’ve repeatedly found that the most interesting vulnerabilities lurk in these backend communications rather than the main application interface. The frontend might be well-hardened, but backend APIs can sometimes miss critical security controls.

Secondly, BurpSuite Pro’s scanner proved invaluable once again. In this case, it quickly identified the time-based SQL injection vulnerability, saving hours of manual testing. While manual testing is crucial for understanding application logic and finding complex vulnerabilities, automated scanning tools like Burp Scanner can rapidly identify common security issues, allowing you to focus your manual efforts on more nuanced attack vectors.