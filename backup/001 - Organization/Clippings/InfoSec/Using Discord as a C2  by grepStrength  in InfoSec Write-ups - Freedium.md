---
title: "Using Discord as a C2 | by grepStrength | in InfoSec Write-ups - Freedium"
source: "https://freedium.cfd/https://infosecwriteups.com/using-discord-as-a-c2-cf90b3480689"
author:
published:
created: 2025-01-21
description: "It&#39s good for gaming, streaming, hacking…"
tags:
  - "clippings"
---
#### It's good for gaming, streaming, hacking…

> (Note: I made multiple updates to this in the C&C section of this post since this was first published last night.)

Just for the hell of it, I decided to see if I could run Discord as a C2. It hit me on a whim, so I started researching this when I had a free moment to myself. I personally love Discord and have used it for almost a decade. I use it for D&D, streaming games, general catching up, etc.

You know who else loves Discord? *Threat actors.* It has a long and storied history of being abused to:

- [Commit general cybercrime](https://intel471.com/blog/how-discord-is-abused-for-cybercrime)
- [Deliver infostealers](https://www.infosecurity-magazine.com/news/infostealer-campaign-discord/)
- [Facilitate attacks on critical infrastructure](https://www.bleepingcomputer.com/news/security/discord-still-a-hotbed-of-malware-activity-now-apts-join-the-fun/)

It certainly seemed like a worthy topic to research, so for *funsies*…

### Setting Up the Infrastructure

Before we get started, we have to setup our infrastructure to utilize Discord as our C2. You will need a few things:

- Discord account (with Developer Mode enabled)
- Discord server (where you are the owner/admin)
- Discord bot

To follow along with this specific writeup, you'll need to have Golang installed and `git clone` DiscordGo, an open-source tool I found during my research:

This tool uses Discord's API to give you the ability to:

- Retrieve system information
- Run arbitrary commands
- Download and upload files via command line (e.g. `wget`)
- Take screenshots

All within your Discord server!

I love the fact that this tool was released because it was exactly what I was looking for. However, there are major gaps in the Installation and Usage documentation, which is what actually prompted me to write this article.

Please note that there are other options that simply weren't explored in this writeup.

#### Creating the Server

This is the easy part. First, look for the + sign on the left side panel:

![None](https://miro.medium.com/v2/resize:fit:700/1*D_m8dDZXO5397J2ccYT8RA.png)

From there, just pick any options you want. The important thing is to have a server ID, which all options will provide.

#### Creating the Bot

You'll first want to have Developer Mode enabled for your Discord account:

![None](https://miro.medium.com/v2/resize:fit:700/1*nFTxEx-dIVuvRIPZxsj6WQ.png)

Next, go to the developer portal and log into your account. It can be found here:

From there, you'll want to create a new application and name it to whatever you want:

![None](https://miro.medium.com/v2/resize:fit:700/1*dlndOswFAoTDkIAmBuxEkg.png)

I later renamed this to "Command&Control"…

Select the newly created application:

![None](https://miro.medium.com/v2/resize:fit:700/1*fvIOenqv6kp5ijKTYMDTiQ.png)

You'll now want to go to the OAuth2 tab to assign it's Scope and Permissions:

![None](https://miro.medium.com/v2/resize:fit:700/1*GCib5R78A-OnvUx7XMXFCQ.png)

sadfasdfads

You don't need to give it full Administrator access like I did. I just did that for the purposes of this writeup. Per DiscordGo's repo you only need the following permissions:

- Send Messages
- Read Messages
- Attach Files
- Manage Server

![None](https://miro.medium.com/v2/resize:fit:700/1*L5qnuU6L3P3X4PquqGMTzw.png)

Visit the URL and authorize the connection, and you should see the bot show as a user in your Discord server:

![None](https://miro.medium.com/v2/resize:fit:700/1*zqVKynBf77l51-hpQoV4Zg.png)

Boom

#### DiscordGo

To get this setup, do a simple `git clone` to your favorite directory (I went with `/opt`):

```bash
cd /opt
git clone https://github.com/emmaunel/DiscordGo.git && cd DiscordGo
```

Now we have to modify the `pkg/util/variables.go` config file to add our *ServerID* and *BotToken*. I just use the default text editor for Kali:

```bash
mousepad pkg/util/variables.go
```

![None](https://miro.medium.com/v2/resize:fit:700/1*Q60JDa1GF4q1_nwHeX39zA.png)

You can get your `ServerID` by going to your settings > Widget:

![None](https://miro.medium.com/v2/resize:fit:700/1*JAif63lE0rOYGhDkjL0ERQ.png)

![None](https://miro.medium.com/v2/resize:fit:700/1*oZZ4ep4eKr66mEc7LmUeLg.png)

To get the token, go to your bot's page in the development portal, then go to the Bot tab to reset your token, enter your Discord credentials, then copy it down immediately:

![None](https://miro.medium.com/v2/resize:fit:700/1*3Uy1LnDeMeoKUT9e1KUFyw.png)

Save the *ServerID* and the *BotToken* to the file, and make the payloads:

```go
make
```

![None](https://miro.medium.com/v2/resize:fit:700/1*NoLXeb_hdYieT73NyI1lqA.png)

It's also taking advantage of Golang's cross-platform binary compilation ability.

Now we're finally ready to go!

### Payload Delivery

How you actually get the payload to the target is up to you, but I'll show a simple and manual method using ChatGPT. I'll just flat out ask it to write me an email:

![None](https://miro.medium.com/v2/resize:fit:700/1*6f9Gj1n9sm543ri2gEsGOg.png)

Thanks for being so helpful with my phishing endeavors…

Taking this, I'll now send this as a spearphishing attachment to one of my test accounts:

![](https://miro.medium.com/v2/resize:fit:700/1*c9dgTBcNPqntyEEI1c4adQ.png)

Edit: In hindsight I should have shown how to do this via Discord CDN.

Another method is sending a payload right in the middle of a Discord DM:

![None](https://miro.medium.com/v2/resize:fit:700/1*gs7uKNnIgRwEIUxjH1v0rw.png)

As Testy, I lean into the RP a bit:

![None](https://miro.medium.com/v2/resize:fit:700/1*3EXYuUysY6uFHXbiaV46fQ.png)

As my Testy victim, I download and execute the malicious attachment:

![None](https://miro.medium.com/v2/resize:fit:700/1*5hFrl3SvoPnVxO0501DI-g.png)

### C&C

Back at my attacker machine a new channel is created for my compromised user. The channel is named after the compromised user's IP address without the octet separators. It also has a pinned initial message with my user's hostname, IP, and OS:

![None](https://miro.medium.com/v2/resize:fit:700/1*sU3qSd_wMKyrYgNZPj_2oQ.png)

Also beacons back home to my attack server at 5 minute intervals.

I can show that it easily works in Linux as well (*while skipping the payload delivery and using a different bot*):

![None](https://miro.medium.com/v2/resize:fit:700/1*BwnkFXFE1a8ZuNUNopG2-Q.png)

This is a Linux VM that I use for different testing, so some light obfuscation is needed….

You can now use Discord to issue commands on the host and drop additional payloads. To do so, you simply type in your server's channel as if you would to a group of people and it will return the appropriate output as if you have a BASH or cmd shell.

Note: If you're having trouble with the following error, "Command didn't return anything," this is a [known issue that has a pretty easy fix](https://github.com/emmaunel/DiscordGo/issues/22#issuecomment-1568940804):

![None](https://miro.medium.com/v2/resize:fit:700/1*eOYp7VrgaJMDl3hzVDZPoQ.png)

On your developer page, go to your bot's page > select Bot from the side tabs > enable Message Content Intent:

![None](https://miro.medium.com/v2/resize:fit:700/1*MgP0_ih91HZDq2eSvAIzEA.png)

After following that user's directions, I try the same command:

![None](https://miro.medium.com/v2/resize:fit:700/1*nL5YafRNhUbpee1SmUOeSg.png)

Whoop!

Just to give you an idea of what you can do, I can see that right in my Debian VM's Downloads directory, I still have the initial payload:

![None](https://miro.medium.com/v2/resize:fit:700/1*vpVBcZnrTfDBz-s7NSF3wA.png)

From my attacker server, I do some basic file and directory enumeration, then delete the file:

![None](https://miro.medium.com/v2/resize:fit:700/1*GiwGfGfJiyTx0Cia3vAfbQ.png)

"Command didn't return anything" here is a little misleading.

While it *says* it didn't return anything, that's because there is no longer anything there:

![None](https://miro.medium.com/v2/resize:fit:700/1*0pLstNViQ_mjmfhbU5SKtw.png)

Don't ask me why it doesn't see the Discord installation file…

(*Edit: Thanks for pointing out my mistake, \*\*\*\*…*)

Thankfully, you can use basic BASH commands to do things like upload files to the target system:

![None](https://miro.medium.com/v2/resize:fit:700/1*iQXZMX_0N1SfmSfv_Ifg8g.png)

Whoooooop!

And just to confirm:

![None](https://miro.medium.com/v2/resize:fit:700/1*6LSb1XJEqn_Zgq0YJN70oA.png)

Note that I also downloaded a fork with recent updates (as recent as 3 weeks ago as of this writing):

Per that repo's notes, it was updated to include screenshot and display sharing functionality, so I test that:

![None](https://miro.medium.com/v2/resize:fit:700/1*vFw6vxqxHNgf4sQsCO1o9w.png)

!!!!

It works!

### Conclusion

I'm sure most would opt for the more tried and true Sliver, Mythic C2, or Covenant, but this shows that Discord can definitely be used as a C2. While I think there are some minor kinks to iron out, I think DiscordGo works with relatively easy setup.

**Unfortunately, as of this writing, the main project's latest commits were in 2022**. I wanted to see when they would add the upload and download functions, which are listed as work-in-progress on their *README.md,* and the realization set in that it's been a while... However, I still commend the effort and this is definitely a working C2.

Thankfully, while researching this topic, I did find a Medium article where the author used Mythic C2 in conjunction with Discord, so I'll probably be trying that at later date. I also eventually want to work on using more malicious Discord webhooks.

### References

#### Main

1. [https://github.com/emmaunel/DiscordGo](https://github.com/emmaunel/DiscordGo)
2. [https://discord.com/developers/applications](https://discord.com/developers/applications)
3. [https://github.com/benimoor/DiscordC2](https://github.com/benimoor/DiscordC2) (fork of main)

#### Alternate Method

1. [https://medium.com/@lsecqt/utilizing-discord-as-c2-traffic-broker-b6a4d2f93bb3](https://medium.com/@lsecqt/utilizing-discord-as-c2-traffic-broker-b6a4d2f93bb3)

#### Threat Actor Usage

1. [https://intel471.com/blog/how-discord-is-abused-for-cybercrime](https://intel471.com/blog/how-discord-is-abused-for-cybercrime)
2. [https://www.infosecurity-magazine.com/news/infostealer-campaign-discord/](https://www.infosecurity-magazine.com/news/infostealer-campaign-discord/)
3. [https://www.bleepingcomputer.com/news/security/discord-still-a-hotbed-of-malware-activity-now-apts-join-the-fun/](https://www.bleepingcomputer.com/news/security/discord-still-a-hotbed-of-malware-activity-now-apts-join-the-fun/)