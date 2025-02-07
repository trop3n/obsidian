#networking #ISO #OSI #TCP/IP #cybersecurity101 #tryhackme 
# Introduction

Have you ever wondered why you need an IP address to access the Internet? Is it true that an IP address can uniquely identify the user? Are you curious to learn what the life of a packet looks like? If the answer is yes, let’s dive in!

This room is the first room in a series of four rooms dedicated to introducing the user to vital networking concepts and the most common networking protocols:

- Networking Concepts (this room)
- [Networking Essentials](https://tryhackme.com/r/room/networkingessentials)
- [Networking Core Protocols](https://tryhackme.com/r/room/networkingcoreprotocols)
- [Networking Secure Protocols](https://tryhackme.com/r/room/networkingsecureprotocols)

### Room Prerequisites

This room expects that you know terms such as IP address and TCP port number; however, we don’t expect that the reader is able to explain such terms in proper technical depth. If you are unfamiliar with these terms, please consider joining the [Pre Security](https://tryhackme.com/r/path/outline/presecurity) path.  

### Learning Objectives

By the time you finish this room, you will have learned about the following:

- ISO OSI network model
- IP addresses, subnets, and routing
- TCP, UDP, and port numbers
- How to connect to an open TCP port from the command line
# OSI Model

Before we start, we should note that the OSI model might initially seem complicated. Don't worry if you encounter cryptic acronyms, as we provide examples of the OSI model layers. We assure you that by the time you finish this module, this task will feel like a piece of cake.

The OSI (Open Standards Interconnection) model is a conceptual model developed by the International Organization for Standardization (ISO) that describes how communications should occur in a computer network. In other words, the OSI model defines a framework for computer network communications. Although this model is theoretical, it is vital to learn and understand as it helps grasp networking concepts on a deeper level. The OSI model is composed of seven layers: 

1. Physical Layer
2.  Data Link Layer
3. Network Layer
4. Transport Layer
5. Session Layer
6. Presentation Layer
7. Application Layer

The numbering starts with the physical layer being layer 1, while the top layer, the application layer, is layer 7.  To help you remember the layers from bottom to top, you can use a mnemonic such as "Please Do Not Throw Spinach Pizza Away". You can check the internet for other easy-to-remember acronyms if this helps you memorize them. Remembering the OSI model layers with their layer numbers is important, you will struggle to understand terms such as "layer 3 switch" or "layer 7 firewall".

![](https://i.imgur.com/mzAAQbL.png)
## Layer 1: Physical Layer

The physical layer, also referred to as layer 1, deals with the physical connection between devices; this includes the medium, such as a wire, and the definition of the binary digits 0 and 1. Data transmissions can be via an electrical, optical, or wireless signal. Consequently, we need data cables or antennas, depending on our physical medium.

In addition to Ethernet cable, shown in the illustration below, and optical fiber cable, examples of the physical layer medium include the WiFi radio bands, the 2.4 GHz band, the 5 GHz band, and the 6 GHz band.
## Layer 2: Data Link Layer

The physical layer defines a medium to transmit our signal. The data link layer, i.e. layer 2, represents the protocol that enables data transfer between nodes on the same network segment. Let's put it in simpler terms. The data link layer describes an agreement between the different systems on the same network segment on how to communicate. A network segment refers to a *group of networked devices using a shared medium or channel for information transfer.* For example, consider a company office with ten computers connected to a network switch; that's a network segment.

Examples of Layer 2 include Ethernet, i.e. 802.3, and WiFi, i.e. 802.11. Ethernet and WiFi addresses are six bytes. Their address is called a MAC address, where MAC stands for **Media Access Control**. They are usually expressed in hexadecimal format with a colon separating each two bytes. The three leftmost bytes identify the vendor.

![](https://i.imgur.com/2tjxJRs.png)

We expect to see two MAC addresses in each frame in real network communication over Ethernet or WiFi. The packet in the screenshot below shows:

- The destination data-link address (MAC address) highlighted in yellow
- The source data link address (MAC address) is highlighted in blue
- The remaining bits show the data being sent

![](https://i.imgur.com/chkm7ZW.png)
## Layer 3: Network Layer


