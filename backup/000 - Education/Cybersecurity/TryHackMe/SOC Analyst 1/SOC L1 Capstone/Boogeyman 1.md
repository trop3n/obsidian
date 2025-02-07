#tryhackme #capstonechallenge #cybersecurity 

_Uncover the secrets of the new emerging threat, the Boogeyman._

In this room, you will be tasked to analyse the Tactics, Techniques, and Procedures (TTPs) executed by a threat group, from obtaining initial access until achieving its objective.
## Prerequisites

This room may require the combined knowledge gained from the SOC L1 Pathway. We recommend going through the following rooms before attempting this challenge.

- [Phishing Analysis Fundamentals](https://tryhackme.com/room/phishingemails1tryoe)
- [Phishing Analysis Tools](https://tryhackme.com/room/phishingemails3tryoe)
- [Windows Event Logs](https://tryhackme.com/room/windowseventlogs)
- [Wireshark: Traffic Analysis](https://tryhackme.com/room/wiresharktrafficanalysis)
- Tshark (coming soon!)

## Investigation Platform

Before we proceed, deploy the attached machine by clicking the **Start Machine button** in the upper-right-hand corner of the task. It may take up to 3-5 minutes to initialise the services.

The machine will start in a split-screen view. In case the VM is not visible, use the blue Show Split View button at the top-right of the page.

## Artefacts  

For the investigation proper, you will be provided with the following artefacts:

- Copy of the phishing email (dump.eml)
- Powershell Logs from Julianne's workstation (powershell.json)
- Packet capture from the same workstation (capture.pcapng)

Note: The powershell.json file contains JSON-formatted PowerShell logs extracted from its original evtx file via the [evtx2json](https://github.com/Silv3rHorn/evtx2json) tool.

You may find these files in the `/home/ubuntu/Desktop/artefacts` directory.
## Tools

﻿The provided VM contains the following tools at your disposal:

- Thunderbird - a free and open-source cross-platform email client.
- [LNKParse3](https://github.com/Matmaus/LnkParse3) - a python package for forensics of a binary file with LNK extension.
- Wireshark - GUI-based packet analyser.
- Tshark - CLI-based Wireshark. 
- jq - a lightweight and flexible command-line JSON processor.

To effectively parse and analyse the provided artefacts, you may also utilise built-in command-line tools such as:

- grep
- sed
- awk
- base64

Now, let's start hunting the Boogeyman!
# Email Analysis

Julianne, a finance employee working for Quick Logistics LLC, received a follow up email regarding an unpaid invoice from their business partner, B Packaging Inc. Unbeknownst to her, the attached document was malicious and compromised her workstation. 

