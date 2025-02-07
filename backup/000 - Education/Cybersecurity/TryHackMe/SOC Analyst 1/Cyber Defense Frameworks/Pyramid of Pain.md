# The Pyramid of Pain

> This well renowned concept is being applied to cybersecurity solutions like Cisco Security, SentinelOne, and SOCRadar. 

Cisco Security: https://gblogs.cisco.com/ca/2020/08/26/the-canadian-bacon-cisco-security-and-the-pyramid-of-pain/
SentinelOne: https://www.sentinelone.com/blog/revisiting-the-pyramid-of-pain-leveraging-edr-data-to-improve-cyber-threat-intelligence/
SOCRadar: https://socradar.io/re-examining-the-pyramid-of-pain-to-use-cyber-threat-intelligence-more-effectively/

Understanding the Pyramid of Pain concept as a Threat Hunter, Incident Responder, or SOC Analyst is important.

### Hash Values (Trivial)

> As per Microsoft, the hash value is a numeric value of a fixed length that uniquely identifies data. A hash value is the result of a hashing algorithm. The following are some of the most common hashing algorithms.

- **MDS (Message Digest, defined by RFC 1321)** - was designed Ron Rivest in 1992 and is a widely used cryptographic hash function with a 128-bit hash value. MDS hashes are **NOT** considered to be **cryptographically secure**. In 2011, the IETF published RFC 6151, ["Updated Security Considerations for the MD5 Message-Digest and the HMAC-MD5 Algorithms](https://datatracker.ietf.org/doc/html/rfc6151)," which mentioned a number of attacks against MD5 hashes, including the hash collision.

- **SHA-1 (Secure Hash Algorithm 1, defined by [RFC 3174](https://tools.ietf.org/html/rfc3174))** - invented by United States National Security Agency in 1995. When data is fed to SHA-1 Hashing Algorithm, SHA-1 takes an input and produces a 160-bit hash value string as a 40 digit hexadecimal number. [NIST deprecated the use of SHA-1 in 2011](https://csrc.nist.gov/news/2017/research-results-on-sha-1-collisions) and banned its use for digital signatures at the end of 2013 based on it being susceptible to brute-force attacks.
	- NIST recommends migrating from SHA-1 to stronger hash algorithms in the SHA-2 and SHA-3 families

- **The SHA-2 (Secure Hash Algorithm 2)** - SHA-2 Hashing Algorithm was designed by the National Institute of Standards and Technology (NIST) and the National Security Agency (NSA) in 2001 to replace SHA-1. SHA-2 has many variants, and arguably the most common is SHA-256. The SHA-256 algorithm returns a hash value of 256-bits as a 64 digit hexadecimal number.

> A hash is not considered to by cryptographically secure if two files have the same hash value or digest. 

Security professionals usually use the hash values to gain insight into a specific malware sample, a malicious or suspicious file, and as a way to uniquely identify and reference the malicious artifact. 

Online tools for doing hash lookups:

Metadefender Cloud - OPSWAT: https://metadefender.opswat.com/?lang=en

VirusTotal: https://www.virustotal.com/gui/home/upload

---

It's fairly easy to spot a malicious file if we have the hash in our arsenal. However, as an attacker, modifying the file by even a little bit is trivial, which would produce a different hash value. With so many variations and instances of known malware or ransomware, threat hunting using file hashes as the IOC (Indicators of Compromise) can become difficult.

### IP Addess (Easy)

> You may have learned the importance of an IP address from the Networking rooms. An IP address is used to identify any device connected to a network.

- We rely on IP addresses to send and receive information over a network. 

In the Pyramid of Pain, we will evaluate how IP addresses are used as an indicator.

> In the Pyramid of Pain, IP addresses are associated with the color green. You might be asking why and what you can associate the color green with?

- From a defensive standpoint, knowledge of the IP addresses an adversary uses can be valuable. A common defense tactic is to block, drop or deny inbound requests from IP addresses on your parameter or external firewall. 
- This tactic if often not bulletproof as it's trivial for an experienced adversary to recover simply by using a new public IP address.

One of the fastest ways an adversary can make it challenging to successfully carry out IP blocking is by using **Fast Flux**.

According to Akamai, **Fast Flux** is a DNS technique used by botnets to hide fishing, web proxying, malware delivery, and malware communication activities behind compromised hosts acting as proxies. 

- The purpose of using the Fast Flux network is to make the communication between malware and command and control servers challenging to be discovered by security professionals.

*The primary concept of a Fast Flux network is to have multiple IP addresses associated with a domain name, which is constantly changing.*

- Palo Alto created a great fictional scenarios to explain fast flux: ["](https://unit42.paloaltonetworks.com/fast-flux-101/)[Fast Flux 101: How Cybercriminals Improve the Resilience of Their Infrastructure to Evade Detection and Law Enforcement Takedowns"](https://unit42.paloaltonetworks.com/fast-flux-101/)

### Domain Names (Simple)

> Domain names can be thought as simply mapping an IP address to a string of text. A domain name can contain a domain and a top-level domain (evilcorp.com) or a subdomain (tryhackme.evilcorp.com). 
> 	But we will not go into the details of the the Domain Name System (DNS) works. 

Domain names can be a little more of a pain for the attacker to change as they would most likely need to purchase the domain, register it and modify DNS records. Unfortunately for defenders, many DNS providers have loose standards and provide APIs to make it even easier for the attacker to change the domain. 

A **Punycode** attack is used by hackers to redirect users to a malicious domain that seems legit at first glance. 

What is **Punycode**? "Punycode is a way of converting words that cannot be written in ASCII, into a Unicode ASCII encoding."

> To detect malicious domains, proxy logs or web server logs can be used. 

Attackers usually hide the malicious domains under *URL shorteners*. A URL shortener is a tool that creates a short and unique URL that will redirect to the specific website specified during the initial step of setting up the URL shortener link. 

- According to Cofense, attackers use the following URL shortening services to generate malicious links:
	- bit.ly
	- goo.gl
	- ow.ly
	- s.id
	- smarturl.it
	- tiny.pl
	- tinyurl.com
	- x.co

##### Viewing Connections in Any.run:

Because Any.run is a sandboxing service that executes the sample, we can review any connections such as HTTP requests, DNS requests or processes communicating with an IP address. To do so, we can look at the "networking" tab located just below the snapshot of the machine.

*Please Note:* you should be extremely cautious about visiting any of the IP addresses or HTTP requests made in a report. After all, these are behaviors from the malware sample, so they're probably doing something dangerous. 

### Host Artifacts (Annoying)