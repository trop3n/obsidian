# Study Guide: Information Gathering - Web Edition

This study guide is designed to help you review and practice the key concepts from the markdown file. Each section corresponds to a `#` header in the original document, with 10 questions and practical exercises for each.

---

## Introduction

### Questions
1. What is the primary purpose of web reconnaissance in the context of penetration testing?
2. Name four goals of web reconnaissance.
3. Why is it important for defenders to perform reconnaissance on their own systems?
4. What are the two fundamental methodologies of reconnaissance?
5. How does active reconnaissance differ from passive reconnaissance?
6. What risks are associated with active reconnaissance techniques like port scanning?
7. What is the role of vulnerability scanning in web reconnaissance?
8. Why is network mapping considered a medium-to-high risk activity?
9. What information can banner grabbing reveal about a target system?
10. How does OS fingerprinting contribute to the reconnaissance process?

### Practical Exercises
1. Use Nmap to scan a local virtual machine and identify open ports.
2. Perform a WHOIS lookup on a domain using an online tool.
3. Write a script to automate banner grabbing using Netcat.
4. Use a free vulnerability scanner (e.g., OpenVAS) to scan a test environment.
5. Map the network topology of your home network using traceroute.
6. Identify the operating system of a target using Nmap's `-O` flag.
7. Enumerate services running on a test server using Nmap's `-sV` flag.
8. Crawl a test website using OWASP ZAP Spider.
9. Analyze the attack surface of a sample application by identifying potential entry points.
10. Research and list three tools that can be used for gathering intelligence during reconnaissance.

---

## DNS

### Questions
1. What is the role of DNS in internet communication?
2. Explain the difference between a domain name and an IP address.
3. What are the steps involved in the DNS resolution process?
4. What is the purpose of the hosts file, and where is it located on Linux and Windows systems?
5. How does the hosts file differ from DNS in terms of functionality?
6. What is a DNS zone, and how is it represented in a zone file?
7. Name three common DNS record types and their purposes.
8. What is the significance of the `IN` field in DNS records?
9. Why is DNS important for web reconnaissance?
10. How can monitoring DNS records over time reveal changes in a target's infrastructure?

### Practical Exercises
1. Edit the hosts file on your system to map a custom domain to `127.0.0.1`.
2. Use `dig` to query the A record of a domain.
3. Perform a reverse DNS lookup using `dig`.
4. Create a simple zone file for a test domain and include A, MX, and CNAME records.
5. Use an online DNS lookup service to retrieve all records for a domain.
6. Query the TXT records of a domain using `dig`.
7. Perform a DNS zone transfer attempt on a test server.
8. Use `nslookup` to find the authoritative name servers for a domain.
9. Analyze the DNS records of a domain to identify potential subdomains.
10. Monitor DNS changes for a domain over a week using a tool like `dnstwist`.

---

## Subdomains

### Questions
1. What are subdomains, and why are they important in web reconnaissance?
2. Name three types of resources that subdomains might host.
3. What is subdomain enumeration, and why is it valuable?
4. Compare active and passive subdomain enumeration techniques.
5. What is brute-force subdomain enumeration, and what tools can be used for it?
6. How can Certificate Transparency logs assist in subdomain discovery?
7. What is the role of wordlists in subdomain brute-forcing?
8. Name three tools commonly used for subdomain enumeration.
9. What are some potential risks of performing active subdomain enumeration?
10. How can subdomains inadvertently expose sensitive information?

### Practical Exercises
1. Use `dnsenum` to enumerate subdomains for a test domain.
2. Perform subdomain brute-forcing using `ffuf` and a wordlist.
3. Search Certificate Transparency logs for subdomains of a domain using `crt.sh`.
4. Use Google search operators to find subdomains of a target domain.
5. Analyze the results of a zone transfer to identify subdomains.
6. Create a custom wordlist based on a company's naming conventions.
7. Use `assetfinder` to discover subdomains for a domain.
8. Compare the results of active and passive subdomain enumeration techniques.
9. Investigate a subdomain to determine if it hosts a development environment.
10. Block a subdomain using the hosts file to simulate a DNS change.

---

## Virtual Hosts

### Questions
1. What is virtual hosting, and how does it work?
2. What is the difference between subdomains and virtual hosts?
3. How does the HTTP Host header influence virtual hosting?
4. Name three types of virtual hosting.
5. What are the advantages and disadvantages of name-based virtual hosting?
6. How can virtual host discovery tools assist in reconnaissance?
7. What is VHost fuzzing, and how is it performed?
8. Name three tools used for virtual host discovery.
9. What are some potential risks of performing virtual host discovery?
10. How can modifying the hosts file help in accessing non-public virtual hosts?

### Practical Exercises
1. Configure Apache to host multiple virtual hosts on a single server.
2. Use `gobuster` to perform virtual host discovery on a test server.
3. Modify the hosts file to access a virtual host without DNS resolution.
4. Analyze HTTP headers to identify virtual hosting configurations.
5. Use `ffuf` to fuzz virtual hosts by targeting the Host header.
6. Compare the responses of different virtual hosts on the same IP address.
7. Investigate a virtual host to determine its purpose and content.
8. Use `curl` to manually test virtual host configurations.
9. Block a virtual host using the hosts file to simulate restricted access.
10. Document the differences between IP-based and name-based virtual hosting.

---

## Certificate Transparency Logs

### Questions
1. What are Certificate Transparency logs, and why are they important?
2. How do Certificate Transparency logs enhance trust in SSL/TLS certificates?
3. What is the structure of a Merkle tree, and how does it ensure data integrity?
4. How can CT logs assist in detecting rogue certificates?
5. What are some limitations of relying solely on Certificate Transparency logs?
6. Name two popular tools for searching CT logs.
7. How can expired certificates in CT logs indicate potential vulnerabilities?
8. What is the role of the Subject Alternative Name (SAN) field in certificates?
9. How can CT logs be used to uncover hidden subdomains?
10. What are some ethical considerations when using CT logs for reconnaissance?

### Practical Exercises
1. Use `crt.sh` to search for certificates issued to a domain.
2. Extract subdomains from CT logs using `curl` and `jq`.
3. Analyze a certificate's SAN field to identify associated subdomains.
4. Compare the results of CT log searches with subdomain brute-forcing.
5. Investigate a domain's CT logs to identify outdated or expired certificates.
6. Use Censys to analyze certificates and identify related hosts.
7. Automate CT log searches using a script.
8. Cross-reference CT log data with DNS records for a domain.
9. Identify potential vulnerabilities associated with expired certificates.
10. Document the process of verifying a certificate's inclusion in a CT log.

---

## Fingerprinting

### Questions
1. What is fingerprinting in the context of web reconnaissance?
2. Name three techniques used for web server fingerprinting.
3. What information can be revealed through banner grabbing?
4. How can analyzing HTTP headers assist in fingerprinting?
5. What is the purpose of WAF detection tools like `wafw00f`?
6. How can page content analysis reveal underlying technologies?
7. Name three tools commonly used for fingerprinting.
8. What are some potential risks of performing fingerprinting?
9. How can outdated software versions identified through fingerprinting pose a risk?
10. What is the role of metadata in fingerprinting?

### Practical Exercises
1. Use `curl` to grab the banner of a web server.
2. Analyze HTTP headers to identify the web server software and version.
3. Use `wafw00f` to detect the presence of a WAF on a test server.
4. Perform fingerprinting using `Wappalyzer` on a live website.
5. Use `Whatweb` to identify technologies used by a website.
6. Investigate a website's metadata to determine its CMS.
7. Compare the results of different fingerprinting tools.
8. Identify outdated software versions on a test server using `Nikto`.
9. Analyze error messages to infer underlying technologies.
10. Document the process of detecting a WordPress installation through fingerprinting.

---

## Crawling

### Questions
1. What is web crawling, and how does it differ from fuzzing?
2. Name two primary crawling strategies and their differences.
3. What types of information can be extracted through crawling?
4. Why is contextual analysis important when interpreting crawling results?
5. What are some ethical considerations when performing web crawling?
6. Name three popular web crawling tools.
7. How can robots.txt files assist in web crawling?
8. What is the `.well-known` directory, and why is it significant?
9. How can crawling help in identifying crawler traps?
10. What are some limitations of web crawling?

### Practical Exercises
1. Use Burp Suite Spider to crawl a test website.
2. Perform crawling using OWASP ZAP and analyze the results.
3. Write a Scrapy spider to extract links from a website.
4. Analyze a robots.txt file to identify disallowed paths.
5. Investigate the `.well-known` directory of a domain for useful endpoints.
6. Use `wget` to mirror a small website for offline analysis.
7. Compare breadth-first and depth-first crawling strategies.
8. Identify sensitive files exposed through crawling.
9. Document the process of detecting a crawler trap.
10. Use crawling results to map the structure of a website.

---

## Search Engine Discovery

### Questions
1. What is search engine discovery, and how is it used in reconnaissance?
2. Name three benefits of using search engines for information gathering.
3. What are some limitations of search engine discovery?
4. Name five advanced search operators and their purposes.
5. What is Google Dorking, and how can it assist in reconnaissance?
6. How can search operators help in identifying login pages?
7. What are some ethical considerations when using search engines for reconnaissance?
8. How can search engine discovery be applied in competitive intelligence?
9. What is the role of cached pages in search engine discovery?
10. How can search engines help in uncovering exposed configuration files?

### Practical Exercises
1. Use search operators to find login pages for a domain.
2. Perform Google Dorking to identify exposed files for a domain.
3. Use the `site:` operator to limit search results to a specific domain.
4. Search for PDF documents related to a company using `filetype:pdf`.
5. Use the `cache:` operator to view a cached version of a webpage.
6. Identify websites linking to a domain using the `link:` operator.
7. Use the `related:` operator to find websites similar to a target.
8. Search for definitions of cybersecurity terms using the `define:` operator.
9. Use the `intext:` operator to find pages containing specific keywords.
10. Document the process of uncovering a website's email addresses using search engines.

---

## Web Archives

### Questions
1. What is the Wayback Machine, and how does it work?
2. Name three benefits of using the Wayback Machine for reconnaissance.
3. What are some limitations of the Wayback Machine?
4. How can archived snapshots help in uncovering hidden assets?
5. What is the significance of tracking changes in a website's history?
6. How can the Wayback Machine assist in gathering intelligence?
7. What are some ethical considerations when using the Wayback Machine?
8. How does the frequency of archiving vary for different websites?
9. What types of information can be retrieved from archived snapshots?
10. How can the Wayback Machine be used for stealthy reconnaissance?

### Practical Exercises
1. Use the Wayback Machine to view an archived version of a website.
2. Compare historical snapshots of a website to identify changes.
3. Investigate a domain's past using the Wayback Machine.
4. Extract links from an archived snapshot of a website.
5. Use the Wayback Machine to uncover old subdomains or directories.
6. Analyze archived content to gather intelligence about a company.
7. Document the process of downloading an entire archived website.
8. Identify outdated technologies or vulnerabilities in archived snapshots.
9. Use the Wayback Machine to find removed or modified content.
10. Compare current and archived versions of a website's robots.txt file.

---

## Automating Recon

### Questions
1. What are the benefits of automating reconnaissance tasks?
2. Name three reconnaissance frameworks and their features.
3. What are some potential risks of automated reconnaissance?
4. How does FinalRecon differ from other reconnaissance tools?
5. What types of information can FinalRecon gather?
6. Name three modules available in Recon-ng.
7. How can theHarvester assist in gathering email addresses and subdomains?
8. What is the role of SpiderFoot in reconnaissance?
9. How can automation frameworks integrate with other tools?
10. What are some ethical considerations when automating reconnaissance?

### Practical Exercises
1. Install and run FinalRecon on a test domain.
2. Use Recon-ng to perform DNS enumeration.
3. Gather email addresses and subdomains using theHarvester.
4. Perform reconnaissance using SpiderFoot and analyze the results.
5. Automate a series of reconnaissance tasks using a custom script.
6. Compare the results of manual and automated reconnaissance.
7. Use FinalRecon to retrieve Wayback URLs for a domain.
8. Perform a full reconnaissance scan using FinalRecon.
9. Document the process of integrating reconnaissance tools into a workflow.
10. Analyze the output of an automated reconnaissance tool for actionable insights.