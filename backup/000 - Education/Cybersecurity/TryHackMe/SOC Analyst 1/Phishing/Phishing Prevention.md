#tryhackme #phishing #soclevel1 #cybersecurity 
# Introduction

There are various actions a defender can take to help protect the users from falling victim to a malicious email. 

Some examples of these actions are listed below:

- Email Security (SPF, DKIM, DMARC)
- SPAM Filters (flags or blocks incoming emails based on reputation)
- Email Labels (alert users that an incoming email is from an outside source)
- Email Address/Domain/URL Blocking (based on reputation or explicit denylist)
- Attachment Blocking (based on the extension of the attachment)
- Attachment Sandboxing (detonating email attachments in a sandbox environment to detect malicious activity)
- Security Awareness Training (internal phishing campaigns)

Per **MITRE ATT&CK** **Framework**, [Phishing for Information](https://attack.mitre.org/techniques/T1598#mitigations) is described as an attempt to trick targets into divulging information, and contains three sub-techniques.

Visit the above link, and look at the **Mitigation** section under **Software Configuration**.

![](https://i.imgur.com/oQKKw9C.png)

In this room, we will focus specifically on Email Security (SPF, DKIM, DMARC) from the actions noted above.

Let's begin!
# SPF (Sender Policy Framework)

What is the **Sender Policy Framework**?

Per [dmarcian](https://dmarcian.com/what-is-spf/), "_Sender Policy Framework (SPF) is used to authenticate the sender of an email. With an SPF record in place, Internet Service Providers can verify that a mail server is authorized to send email for a specific domain. An SPF record is a DNS TXT record containing a list of the IP addresses that are allowed to send email on behalf of your domain._"

---




Below is a visual workflow for SPF.

![](https://i.imgur.com/PKxMeiJ.png)
How does a basic SPF record look?

`v=spf1 ip4:127.0.0.1 include:spf.google.com -all`

An explanation for the above record:

- `v=spf1` -> This is the start of the SPF record
- `ip4:127.0.0.1` -> This specifies which IP (in this case version IP4 & not IP6) can send email.
- `include:_spf.google.com` -> This specifies which domain can send mail
- `-all` -> Non-authorized emails will be rejected.

Refer to the SPF record syntax on dmarcian [here](https://dmarcian.com/spf-syntax-table/) and [here](https://dmarcian.com/what-is-the-difference-between-spf-all-and-all/).

Let's look at Twitter's SPF record using dmarcian's SPF surveyor [tool](https://dmarcian.com/spf-survey/)

![](https://i.imgur.com/Cz3YVlt.png)

Refer to this resource on [dmarcian](https://dmarcian.com/create-spf-record/) on how to create your own SPF records. 

Let's look at another sample.

The image below is from [Google Admin Toolbox Messageheader](https://toolbox.googleapps.com/apps/messageheader/), which was used to analyze a malicious email.

![](https://i.imgur.com/f5NPirv.png)

The above image shows the status of an SPF record check. It reports back as `softfail`.

The above image shows the status of an SPF record check. It reports back as **softfail**.

**Note**: Even though this task uses [dmarcian](https://dmarcian.com/) for SPF-related information and online checks, many other companies do the same.
# DKIM

What is ***DKIM***? 

Per [dmarcian](https://dmarcian.com/what-is-dkim/), "DKIM stands for DomainKeys Identified Mail and is used for the authentication of an email that’s being sent. Like SPF, DKIM is an open standard for email authentication that is used for DMARC alignment. A DKIM record exists in the DNS, but it is a bit more complicated than SPF. DKIM’s advantage is that it can survive forwarding, which makes it superior to SPF and a foundation for securing your email."

What does a DKIM Record look like?

`v=DKIM1; k=rsa; p=MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAxTQIC7vZAHHZ7WVv/5x/qH1RAgMQI+y6Xtsn73rWOgeBQjHKbmIEIlgrebyWWFCXjmzIP0NYJrGehenmPWK5bF/TRDstbM8uVQCUWpoRAHzuhIxPSYW6k/w2+HdCECF2gnGmmw1cT6nHjfCyKGsM0On0HDvxP8I5YQIIlzNigP32n1hVnQP+UuInj0wLIdOBIWkHdnFewzGK2+qjF2wmEjx+vqHDnxdUTay5DfTGaqgA9AKjgXNjLEbKlEWvy0tj7UzQRHd24a5+2x/R4Pc7PF/y6OxAwYBZnEPO0sJwio4uqL9CYZcvaHGCLOIMwQmNTPMKGC9nt3PSjujfHUBX3wIDAQAB`

An explanation of the above record:

- `v-DKIM1` -> This is the version of the DKIM record. This is optional.
- `k=rsa` -> This is the version of the DKIM record. This is optional. 
- `p=` -> This is the **public key** that will be matched to the private key, which was created during the DKIM process. 

Refer to the DKIM resource [here](https://dmarcian.com/dkim-selectors/) and [here](https://help.returnpath.com/hc/en-us/articles/222481088-DKIM-DNS-record-overview) for additional information.

The below image is a snippet of an email header for an email flagged as spam that contained a potentially malicious attachment.

![](https://i.imgur.com/eQyo5Px.png)
# DMARC

What is **DMARC**? 

Per [dmarcian](https://dmarcian.com/start-dmarc/), "DMARC, (Domain-based  Message Authentication Reporting, & Conformance) an open source standard, uses a concept called alignment to tie the result of two other open source standards, SPF (a published list of servers that are authorized to send email on behalf of a domain) and DKIM (a tamper-evident domain seal associated with a piece of email), to the content of an email. If not already deployed, putting a DMARC record into place for your domain will give you feedback that will allow you to troubleshoot your SPF and DKIM configurations if needed."

How does a basic DMARC record look?

`v=DMARC1;, p=quarantine; rua=mailto:postmaster@website.com`. 

An explanation of the above record:

- `v=DMARC1` -> Must be in all caps, and it's not optional
- `p=quarantine` -> if a check fails, then an email will be sent to the spam folder (DMARC Policy)
- `rua=mailto:postmaster@website.com` -> Aggregate reports will be sent to this email address.

Refer to the DMARC resources [here](https://dmarcian.com/dmarc-record/) and [here](https://dmarc.org/overview/) for additional information on DMARC tags. Review the following resource about DMARC [Alignment](https://dmarcian.com/alignment/).

Let's use the **Domain Health Checker** from [dmarcian.com](https://dmarcian.com/domain-checker/) and check the DMARC status of **microsoft.com**.

![](https://i.imgur.com/eOmCeSF.png)

> And the results are...

![](https://i.imgur.com/EFUaXG4.png)

Microsoft passed all the checks. We can drill down into `DMARC`, `SPF` or `DKIM` to get more details. 

![](https://i.imgur.com/ba9MdGg.png)

In the details above, we can see that all emails that fail the DMARC check will be rejected.

---
## How DMARC Works

DMARC is a technical specification that describes how email senders can make their email easy to identify using existing free and open technologies. DMARC-compliant email is very easy to process, and email receivers have embraced DMARC as the common way to figure out the basic identity of an email. 

DMARC builds upon two existing technologies that are used to associate a piece of email with a domain. SPF, which stands for **Sender Policy Framework**, and DKIM, which stands for **DomainKeys Identified Mail**, work in different but complimentary ways to create a link between a piece of email and a domain. 

SPF and DKIM are *stand-alone technologies* that have been around for many years and can be used *independently* from DMARC. By themselves, SPF and DKIM can associate a piece of email with a domain. In the language of DMARC, SPF and DKIM generate "Authenticated Identifiers". DMARC attempts to tie the results of SPF and DKIM - the Authenticated Identifiers - to the content of email: specifically to domain found in the From: header of an email. 

The domain found in the From: header of a piece of email is the *entity that ties together all DMARC processing*. The "D" in DMARC stands for "Domain-Based", and hopefully you can see now which domain DMARC is concerned with. Now, because anyone can buy a domain and put SPF and DKIM into place (***including criminals!***), the results of processing SPF and DKIM - that is ***authenticated identifiers*** - have to be related to the domain found in the Form: header to be relevant to DMARC. This concept is referred to as "Identifier Alignment". Getting identifiers to align ends up being a large part of the work of deploying DMARC.

To make it possible for someone that owns an email domain to accurately deploy SPF and DKIM, DMARC describes how feedback can be sent to the domain owner regarding how their email domain is being used across the Internet.  This feedback can come in two forms: reports that provide a comprehensive view of all of a domain’s traffic (as seen by the organization that generates the report), and reports that are redacted copies of individual emails that are not 100% compliant with DMARC.

The comprehensive reports are XML-based and include information such as message counts, IP addresses, and the results of processing SPF and DKIM.  Although some humans and most androids can read XML directly, dmarcian specializes in processing these reports and identifying what steps need to be taken so that normal people can get DMARC into place without having to become experts in email authentication.

The reports that are redacted copies of individual emails are not generated by all email receivers that participate in DMARC.  The reason why an email receiver might not generate this type of report spans three big areas:

1. privacy concerns as the individual emails can include personally identifiable information,
2. the reports can potentially be extremely high in volume,
3. the reports are sometimes nice to have, but have proven to be not required to work through the process of deploying DMARC.

Lastly, quite a few organizations don’t even want to ask for these types of reports as they want to avoid any sort of potential liability in the area of privacy.  Still, these reports can shed light on the specific types of abuse that a domain might be encountering.  dmarcian processes both types of feedback to make deployment of DMARC far easier for most types people.

The visibility provided by the feedback reports… when processed by tools like dmarcian.. give the domain owner the ability to deploy SPF and DKIM with a very high degree of accuracy.  Once an email domain owner is confident that they’ve deployed SPF and DKIM across all of their email streams, the domain owner can then tell the world to act against email that is not compliant with DMARC.  The action that can be taken – or rather the policy that the domain owner can publish – is to either quarantine or reject email.  Quarantine usually means to spam-folder email that fails the DMARC check, but if an operator doesn’t implement a traditional spam-folder, the operator might turn up the aggressiveness of spam filtering when processing the non-compliant email.  Reject, however, means to block outright any email that fails the DMARC check.

Domain owners usually strive to get to the reject policy, as doing so disallows unauthorized use of the domain, which ends up being a pretty strong anti-phishing measure.  More importantly for most, though, DMARC-compliant email is far easier to process which is quickly making DMARC a requirement for anyone that wants to get their email delivered reliably.

This is how DMARC works, and how DMARC uses domains to make email easy to identify.

---

# S/MIME (Secure/Multipurpose Internet Mail Extensions)

What is **[S/MIME](https://docs.microsoft.com/en-us/exchange/security-and-compliance/smime-exo/smime-exo)**?

Per Microsoft, "S/MIME (Secure/Multipurpose Internet Mail Extensions) is a widely accepted protocol for sending digitally signed and encrypted messages". 

As you can tell from the definition above, the 2 main ingredients for S/MIME are:

1. **Digital Signatures**
2. **Encryption**

Using [Public Key Cryptography](https://www.ibm.com/docs/en/ztpf/2023?topic=concepts-public-key-cryptography), S/MIME guarantees data integrity and nonrepudiation.

- If Bob wishes to use S/MIME, then he'll need a digital certificate. This digital certificate will contain his public key.
- With this digital certificate, Bob can "sign" the email message with his private key.
- Mary can then decrypt Bob's message with Bob's public key.
- Mary will do the same (send her certificate to Bob) when she replies to his email, and Bob completes the same process on his end.
- Both will now have each other's certificates for future correspondence.

The illustration below will help you understand how public key cryptography works.

![](https://i.imgur.com/RjCeQiE.png)

Refer to this Microsoft documentation [here](https://docs.microsoft.com/en-us/exchange/security-and-compliance/smime-exo/smime-exo) for more information on S/MIME and steps on how to configure Office 365 to send/receive S/MIME emails.
## Public Key Cryptography

The most commonly used implementations of public key cryptography (also known as public-key encryption and asymmetric encryption) are based on algorithms presented by Rivest-Shamir-Adelman (RSA) Data Security.

Public key cryptography involves a pair of keys known as a public key and a private key (a _public key pair_), which are associated with an entity that needs to authenticate its identity electronically or to sign or encrypt data. Each public key is published and the corresponding private key is kept secret. Data that is encrypted with the public key can be decrypted only with the corresponding private key.

RSA public key pairs can be any size. Typical sizes today are 1024 and 2048 bits.

Public key cryptography enables the following:

- Encryption and decryption, which allow two communicating parties to disguise data that they send to each other. The sender encrypts, or scrambles, the data before sending it. The receiver decrypts, or unscrambles, the data after receiving it. While in transit, the encrypted data is not understood by an intruder.
- Nonrepudiation, which prevents:
    - The sender of the data from claiming, at a later date, that the data was never sent
    - The data from being altered.

[Figure 1](https://www.ibm.com/docs/en/ztpf/2023?topic=concepts-public-key-cryptography#s7pkey__figccs01) shows how you can freely distribute the public key so that only you (the owner of the private key) can read data that was encrypted with the public key. In general, to send encrypted data to someone, you must encrypt the data with that person's public key, and the person receiving the data decrypts it with the corresponding private key.

If you compare symmetric-key encryption with public-key encryption, you will find that public-key encryption requires more calculations. Therefore, public-key encryption is not always appropriate for large amounts of data. However, it is possible to use public-key encryption to send a symmetric key, which you can then use to encrypt additional data.

The reverse of what is shown in the previous figure also works. That is, data encrypted with your private key can be decrypted only with your public key. However, this is not a desirable way to encrypt sensitive data because it means that anyone with your public key, which is by definition published, could decrypt the sensitive data. Despite this, private-key encryption is useful because it enables you to use your private key to sign data with your _digital signature_; anyone with your public key can be assured that only you sent the data. This is an important requirement for electronic commerce and other commercial applications of cryptography.

**Related information:**

- See [Authentication](https://www.ibm.com/docs/en/SSB23S_1.1.0.2023/gtps7/s7auth.html "All security mechanisms are based on trust; that is, trust in some service to confirm the authenticity of principals correctly, trust in security algorithms to perform as advertised, and trust in our own judgements when used to evaluate whether the person in front of us is whom they claim to be.").
- See [Symmetric cryptography](https://www.ibm.com/docs/en/SSB23S_1.1.0.2023/gtps7/s7symm.html).
- See [Digital signatures](https://www.ibm.com/docs/en/SSB23S_1.1.0.2023/gtps7/s7dsign.html).

- **[Characteristics of public key pairs](https://www.ibm.com/docs/en/SSB23S_1.1.0.2023/gtps7/s7char1.html)**  
- **[APIs to encrypt and decrypt data by using RSA keys](https://www.ibm.com/docs/en/SSB23S_1.1.0.2023/gtps7/apisrsa.html)**  
    There are several APIs available to encrypt and decrypt data by using RSA keys.

## S/MIME for Message Signing and Encryption in Exchange Online

> https://learn.microsoft.com/en-us/exchange/security-and-compliance/smime-exo/smime-exo

S/MIME (Secure Multipurpose Internet Mail Extensions) is a widely accepted protocol for sending digitally signed and encrypted messages. S/MIME in Exchange Online provides the following services for email messages:

- **Encryptiion**: Protects the content of email messages.
- **Digital Signatures**: Verifies the identity of the sender of an email message.

The rest of this article generally describes S/MIME and how these services work.
### S/MIME Digital Signatures

Digital signatures are the more commonly used service of S/MIME. As the name suggests, digital signatures are the digital counterpart to the traditional, legal signature on a paper document. As with a legal signature, digital signatures provide the following security capabilities:

- ***Authentication***: A signature serves to validate an identity. It verifies the answer to "who are you" by providing a means of differentiating that entity from all others and proving its uniqueness. Because there's no authentication in SMTP email, there's no way to know who sent a message. Authentication in a digital signature solves this problem by *allowing a recipient to know that a message was sent by the person or organization who claims to have sent the message.*
- ***Nonrepudiation***: The uniqueness of a signature prevents the owner of the signature from *disowning the signature*. This capability is called nonrepudiation. Thus, the authentication that a signature provides gives the means to enforce nonrepudiation. The concept of nonrepudiation is most familiar in the context of paper contracts: a signed contract is a legally binding document, and it's impossible to disown an authenticated signature. Digital signatures provide the same function, and increasingly in some areas, are recognized as **legally binding**, similar to a signature on paper. Because SMTP email doesn't provide a means of authentication, it can't provide nonrepudiation. It's easy for a sender to disavow ownership of an SMTP email meeage.
- ***Data Integrity***: An additional security device that digital signatures provide is data integrity. Data integrity is a result of the specific operations that make digital signatures possible. With data integrity services, when the recipient of a digitally signed email message validates the digital signature, the recipient is assured that the email message that is received is, in fact, the same message that was signed and sent, and hasn't been altered while in transit. Any alteration of the message while in transit after it has been signed invalidates the signature. In this way, digital signatures provide *an assurance that signatures on paper can't*, because it's possible for a paper document to be altered after is has been signed.

> [!IMPORTANT]
> Although digital signatures provide data integrity, they don't provide **confidentiality**. Messages with only a digital signature are sent in clear text, like SMTP messages and can be read by others. In the case where the message is opaque-signed, a level of obfuscation is achieved because the message is base64-encoded, but it is still clear text. To protect the contents of email messages, encryption must be used.
### S/MIME Encryption

Message encryption provides a solution to information disclosure. SMTP-based internet email doesn't secure messages. An SMTP internet message can be read by anyone who sees it as it travels or views it where it's stored. These problems are addressed by S/MIME using encryption. Encryption is a way to change information so that it can't be read or understood until it's changed back into a readable and understandable form. Message encryption provides two specific security services:

- ***Confidentiality***: Message encryption serves to protect the contents of an email message. Only the intended recipient can view the contents, and the contents remain confidential and can't be known by anyone else who might receive or view the message. Encryption provides confidentiality while the message is in transit and in storage. 
- ***Data Integrity***: As with digital signatures, message encryption provides data integrity services as a result of the specific operations that make encryption possible. 

> [!IMPORTANT]
> Although message encryption provides confidentiality, it doesn't authenticate the message sender in any way. An unsigned, encrypted message is as susceptible to sender impersonation as a message that isn't encrypted. Because nonrepudiation is a direct result of authentication, message encryption also doesn't provide nonrepudiation. Although encryption does provide data integrity, an encrypted message can show only that the message hasn't been altered since it was sent. No information about who sent the message is provided. To prove the identity of the sender, the message must use a digital signature.

## Related message encryption technologies

Other encryption technologies work together to provide protection for messages at rest and in-transit. S/MIME can work simultaneously with the technologies in the following list, but isn't dependent on them:

- **Transport Layer Security (TLS) which replaces Secure Sockets Layer (SSL)**:
    - Encrypts the tunnel or the route between email servers in order to help prevent snooping and eavesdropping.
    - Encrypts the connection between email clients and email servers.
- **BitLocker**: Encrypts data on hard drives in client computers and servers. If an unauthorized party somehow gains access, they can't read the data on the drives.

[Microsoft Purview Message Encryption](https://learn.microsoft.com/en-us/purview/email-encryption) is a direct competitor to S/MIME, and has the following advantages over S/MIME:

- It's a policy-based encryption service that's configured by an admin to encrypt messages that are sent to anyone inside or outside of the organization. In contrast, users are required to decide whether to apply or not apply S/MIME to messages that they send.
- It's an online service that's built on Azure Rights Management (Azure RMS) and doesn't rely on a public key infrastructure. In contrast, S/MIME requires a certificate and certificate publishing infrastructure.
- Microsoft Purview Message Encryption provides additional capabilities. For example, you can customize messages with your organization's brand.
---

# SMTP Status Codes

Deploy the machine attached to this task; it will be visible in **split-screen** view once it's ready.

In this task, you'll examine a PCAP file with SMTP traffic. You'll only focus on SMTP codes in this task.

You must be familiar with [Wireshark](https://tryhackme.com/room/wireshark) and packet analysis to answer the questions below. 

Here are two resources to assist you with this task:

- [https://www.wireshark.org/docs/dfref/s/smtp.html](https://www.wireshark.org/docs/dfref/s/smtp.html)
- [https://www.mailersend.com/blog/smtp-codes](https://www.mailersend.com/blog/smtp-codes)
# SMTP and C&C Communication

Now we'll take a look at how SMTP has been abused by adversaries for C2 (Command and Control) communications.
## MITRE ATT&CK

**Technique 1071 > Sub-Technique 3**: [https://attack.mitre.org/techniques/T1071/003/](https://attack.mitre.org/techniques/T1071/003/)

Per MITRE: "Adversaries may communicate using application layer protocols associated with electronic mail delivery to avoid detection/network filtering by blending in with existing traffic. Commands to the remote system, and often the results of those commands, will be embedded within the protocol traffic between the client and server."

Several notable groups, such as **APT28**, **APT32**, and **Turla**, to name a few, have used this technique.
### Recommended Mitigation

Network intrusion detection and prevention systems that use network signatures to identify traffic for specific adversary malware can be used to mitigate activity at the network level.
### Detection Opportunity

Analyze packet contents to detect application layer protocols that do not follow the expected protocol standards regarding syntax, structure or any other variables adversaries could leverage to conceal data.




