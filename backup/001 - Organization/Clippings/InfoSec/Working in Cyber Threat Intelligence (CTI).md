---
title: "Working in Cyber Threat Intelligence (CTI)"
source: "https://infosecwriteups.com/working-in-cyber-threat-intelligence-cti-295f299a2453"
author:
  - "[[grepStrength]]"
published: 2024-12-27
created: 2025-01-17
description: "As I’ve said a couple times in my blog, I work in cyber threat intelligence. However, based on multiple readers’ feedback and conversations across social media, people are under the impression that I…"
tags:
  - "clippings"
---
## Pros, Cons, and Misconceptions

[

![grepStrength](https://miro.medium.com/v2/resize:fill:88:88/1*VTL1zxGh08r-zTtbhuDjZQ.png)

](https://grepstrength.dev/?source=post_page---byline--295f299a2453--------------------------------)

[

![InfoSec Write-ups](https://miro.medium.com/v2/resize:fill:48:48/1*SWJxYWGZzgmBP1D0Qg_3zQ.png)

](https://infosecwriteups.com/?source=post_page---byline--295f299a2453--------------------------------)

![](https://miro.medium.com/v2/resize:fit:700/1*mC7RtMdnggIrydTzowE1lg.png)

Image by Microsoft Copilot.

As I’ve said a couple times in my blog, I work in cyber threat intelligence. However, based on multiple readers’ feedback and conversations across social media, people are under the impression that I do anything but.

Half of my writeups are for [hacking some random thing](https://systemweakness.com/bypassing-azure-openais-prompt-shield-65ca03be8abb) while the other half are [analyzing some random malware](https://osintteam.blog/ratception-remcosrat-malware-analysis-e62430c48157). So, of course, the two main cybersecurity fields I’m constantly mistaken for being in are pentesting and malware analysis.

## You’re Not!?

Nope.

So if I don’t work in those fields, why do I write so much about them?

I just think they’re important secondary skillsets to have.

## ̶P̶e̶n̶t̶e̶s̶t̶i̶n̶g̶

Knowing how and when to use hacking tools helps me better inform other cyber defenders. It makes me a better intel analyst. Even the average easy-level box on Hack the Box can help you learn and practice basic pentesting methodology. By default, pentesters research heavily about a bevy of topics like how to gain initial access, exploit vulnerabilities, and abuse Active Directory. If pentesters are doing that then the threat actors are too. Studying pentesting *really* helps me connect the dots when researching a cyber threat.

For example, if I’m researching an actor who is reported to use Ligolo-ng, but the details on their Ligolo-ng usage is lacking, I don’t have to just throw up my hands, because [I’ve learned how to use it](https://medium.com/system-weakness/double-pivoting-for-newbies-with-ligolo-ng-4177b3f1f27b) at least on a basic level. I know that it requires a client to run on a compromised host with the default name of `agent`. I also know that, assuming the actor made no modifications to their payload, that the `agent` is approximately 6MB regardless of the intended victim OS. These are all details that can be utilized to create detection rules.

## ̶M̶a̶l̶w̶a̶r̶e̶ ̶A̶n̶a̶l̶y̶s̶i̶s̶

Being able to analyze malware samples yourself is a huge boon in CTI. You won’t be reliant entirely on external reporting to share with your internal teams. Full on reverse engineering isn’t even a requirement to show the value. Basic static and dynamic analysis are all that you need. You can just find a sample of malware that meets your intel requirements yourself and start pulling IOCs or TTPs you deem relevant.

For example, if you are researching a cyber bulletin and in the report they mention that the actor uses a particular backdoor, and all they say about that backdoor is that it has the hash of RANDOMCHARACTERSTRING… that’s not the most detailed. Well, if you have the hash, you can look for samples from VirusTotal, MalwareBazaar, VX Underground, etc. and just pull artifacts, TTPs, and additional IOCs yourself.

So anyway, what *is* CTI?

First, let’s start with some misconceptions….

## What CTI Isn’t

## Omniscience

![](https://miro.medium.com/v2/resize:fit:500/1*-YPOFQwGk8ix6LDJfAriDA.gif)

Pictured: Absolutely no one working in CTI.

CTI analysts are not plugged into the Matrix. Everyone seems to think we just automatically heard of or know *everything*.

I have heard many a story, from many an intel analyst, lamenting about being asked by their leadership to tell them the nitty gritty details about a new and developing breach. It hasn’t even reached the bigger cyber news blogs, but you know it happened (from SOCMINT, HUMINT, OSINT, etc.)… but that’s about it.

Everything we know is based on data. The problem is that, unless we also work on that organization’s incident response team, or they’re a vendor of ours and have a legal obligation to provide information, there is little chance we’ll have access to that data.

Looking at something like vulnerability management, no an intel team shouldn’t be expected to tell everyone in the org when there’s a new CVE released. There are literally hundreds a day. *No one* can keep up. That should all be part of automated workflows.

## News Feeds

On the surface it seems like a good idea to have the CTI team send out regular “what’s going on out there in the landscape” deliverables.

The problem is that it’s not *actually* *analysis*. It’s just repackaging of high level details from some cyber threat news bulletin. ChatGPT can quickly summarize a news story like that. You don’t need a human.

Don’t get me wrong. Having CTI analysts disseminating a daily cyber news deliverable could have some benefits to leadership, if they prefer curated feeds relevant to them. If your leadership considers daily news deliverables a requirement, then it’s recommended to set up a custom dashboard in your threat intelligence platform (TIP) to pull keywords relevant to your intel requirements to share with them. This satisfies the requirement whilst also freeing up your time to perform actual analysis.

## What CTI Actually Is

I personally like to say that cyber threat intelligence is intrusion analysis on steroids. Your intrusions. Their intrusions. *Everyone’s* intrusions.

- Incident — What did they do?
- Actor — Who did it?
- TTPs — How did they do it?
- Motivations — Why did they do it?
- Region — Where did they do it?
- Indicators of Compromise (IOCs) — What did they do it with?
- Campaigns — How often did they do it?
- Victim(s) — Who did they do it to?

If you want something more official, here’s the following excerpt from [SANS’s FOR578 course description](https://www.sans.org/cyber-security-courses/cyber-threat-intelligence/):

> “The analysis of an adversary’s intent, opportunity, and capability to do harm is known as cyber threat intelligence.”

It’s not just about finding some IOCs and sending them to the SOC. It’s about providing *context* about adversary activity for other security teams to help prioritize cyber defense efforts. While there are more steps than this, in short we collect intrusion data and analyze it, looking for correlations and trends to observed malicious activity.

With that analyzed activity and trends, we can provide actionable insights into malicious activity to keep defenders focused only on the most relevant. Because of this, CTI analysts tend to be former incident responders or forensic analysts, aka digital forensics and incident response (DFIR). I myself started in incident response and just fell into an intel role.

A great example of the link between DFIR and CTI can be found with some [work published by a former colleague of mine](https://digitaldefensehub.io/posts/GitHub-and-malwares/), [Deividas Lis](https://medium.com/u/2a0a1227f843?source=post_page---user_mention--295f299a2453--------------------------------). In one of his Discord communities, he observed users running Python scripts from a questionable GitHub repo, so he started investigating. During his investigation, he found obfuscated code that was hiding malicious URL requests. In order to even publish such work, he had to leverage a strong forensic analysis skillset.

Our research can feed into pretty much every cybersecurity team, but the primary stakeholders tend to be:

- CISO and Executive Leadership
- SOC
- Threat Hunting & Digital Forensics
- Detection Engineering
- Attack Surface Reduction/Vulnerability Management
- Pentesting & Red Teaming
- Cyber Risk

A good way to think about CTI’s value is by trying to answer a few questions.

**Can your CISO go to the finance department and say “We need another $3 million”?**

![](https://miro.medium.com/v2/resize:fit:498/1*KBJcQonwsLElggnn-hDqTg.gif)

Pictured: The CFO.

Now how about if the CISO goes to them with: “We had 6 major cyber incidents in the last fiscal year. Two resulted in complete business stoppages costing us approximately $25 million in losses. Based on a report shared by the intel team, we believe those two most impactful incidents were perpetrated by the same actor as part of the same campaign. In both those incidents, they showed capabilities where our organization has significant gaps to defend against that threat and similar. Additionally, the CTI team is seeing that the landscape is trending in the direction of other actors exhibiting those same capabilities to exploit our gaps. In order to address those gaps, we need an additional $3 million in funding.”

![](https://miro.medium.com/v2/resize:fit:640/1*p38Crd5fuIYOb9PMADcwgA.gif)

Pictured: The deputy CFO. Don’t ask me why he looks strangely like The Rock.

*(Disclaimer: The above paragraph is a fictional scenario created by myself on the fly. Any similarities to real conversations, at real organizations, are purely coincidental.)*

**Can your vulnerability management or attack surface reduction team chase after every system owner for every vulnerability?**

If they can then they’re a one-of-a-kind team comprised entirely of unicorns. In reality, they need to chase after the high likelihood and high impact vulnerabilities, leaving the rest to automated workflows. How will they know which ones to prioritize?

This is where intel can assist, informing them of vulnerabilities being [exploited in the wild](https://helpx.adobe.com/security/products/coldfusion/apsb24-107.html) (e.g. the [CISA KEV Catalog](https://www.cisa.gov/known-exploited-vulnerabilities-catalog)), exploited by threat actors that meet intelligence requirements, those with new exploit kits, or new proof-of-concept exploits.

Is that exploitation in the wild indiscriminate? If so, just patch ASAP. Is it perpetrated by specific actors, in specific campaigns, against specific industries? Depending on the actor and your organization’s industry, maybe a priority patching effort wouldn’t be immediately necessary.

**Can your threat hunting team hunt for just “bad” in the environment?**

Technically, yes, but in practice…. not really.

While they’re looking for one set of activity, a far more likely and relevant subset of “bad” could be actually be achieving their objectives in your environment.

Instead of letting the threat hunting team comb through logs willy nilly, the intel team can point them in the direction of the activity that’s far more likely to affect your organization within the context of specific campaigns or actors.

For example, maybe your organization’s official collaborative software is Zoom, and you (inexplicably) have loose policies and controls governing the installation of IDE extensions. Maybe your organization has also had smaller cybersecurity incidents where a developer’s IDE was the initial access vector. Thus, there is a higher than normal likelihood one of your developers might install one of [these recently reported malicious extensions](https://www.reversinglabs.com/blog/a-new-playground-malicious-campaigns-proliferate-from-vscode-to-npm). Form a threat hunting hypothesis based around a developer installing one of the malicious Zoom-based Visual Studio Code extensions and getting infected with an infostealer.

## Biggest Challenges

## Getting Intel Requirements

Aside from everything in the “What CTI Isn’t” section, the biggest challenge in CTI is that it’s next to impossible to get decent intel requirements.

“Just get us intel” isn’t a thing. We need information to give *relevant* information.

What strategic initiatives, products, technologies, partnerships, etc. are of particular interest to the leadership? What are all of your countries of operation? What are considered the most critical assets? How would a threat actor achieving their objectives impede the organization’s mission?

It unfortunately is an ongoing problem that many CTI analysts and CTI management struggle with. This often leads to intel analysts winging it.

## CTI Training

Another challenge is in getting training in threat intelligence. As far as I’m aware, the only reputable course and certification is SANS FOR578 and its associated GIAC cert, GCTI. (*Note: This was weirdly my first professional IT certification.*)

Mandiant has some CTI training that I’ve taken in the past and MAD20 (from MITRE) has a course and certification, but good luck ever finding a job posting asking for them. GCTI is *the* certification for intel analysts. Many job postings will also accept GCIH, GCFE, or GCFA, though, going back to the close link between DFIR and CTI.

The problem is that SANS and GIAC are firmly priced B2B, as few can justify dropping $9K USD for their training and credentials, even if they have high paying jobs.

I also think that this general lack of cyber threat intelligence training in turn contributes to the general lack of understanding about what cyber threat intelligence actually is…

## Why I Love It

So why have I continued to work in this role? I simply like the work.

I like diving into data to find patterns of behavior, clusters of activity, and neatly package it into an actionable report. You know you’re doing good work when your analysis can bring down the SOC’s Mean Time to Detect (MTTD) or Mean Time to Respond (MTTR). It’s good to know when you are able to help cyber threat hunting find malicious activity in your environment that somehow got past security tooling. It’s a truly great feeling when your work is used to drive policy decisions.

Secondly, researching topics and reporting on what I find is something that I genuinely enjoy doing. That’s the entire reason this blog exists. Sure it also serves as a professional portfolio that I can keep public without violating any NDAs, but really I just like doing this.

Also, I’m a big fan of learning. I like to learn just to learn. With working in CTI, where I need to understand malicious activity across many technologies, and know how to best present information to many different stakeholders, pretty much any training course I study is relevant.

- Want to learn how threat actors breach enterprise networks firsthand, from initial access to full domain takeover? Study CPTS.
- Want to learn how to leverage the Microsoft security suite to find malicious activity? Study SC-200.
- Want to learn how threat actors exploit hybrid Microsoft Entra ID and on prem deployments? Study CARTP.
- Want to learn multiple ways that malware can maintain persistence? Study GREM.

I can guarantee that learning *any* of that will help you become a better intel analyst. Assuming you have a training budget, I doubt you’d get much of a fight from your manager to justify getting training vouchers.

## Conclusion

It’s a good field, and many leaders are increasingly seeing the value. If you are trying to decide what’s next, and you love to dive into data and analyze intrusions, then this might be the career for you.