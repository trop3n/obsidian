# Why Information Security?

Learn about the concept of information security and why it is needed in different office environments.

## Introducing Information Security

We'll begin by exploring the role of cryptography in securing information. We use the term *information security* in a generic sense to mean protecting information and information systems. This is also commonly referred to as *cybersecurity*.

Information security involves the use of many different types of security technologies and management processes and controls. It is precisely cryptography that provides the techniques that underpin most information security technologies.

## The Rising Profile of InfoSec

Even as recently as the end of the last century, cryptography was a topic only specialists and a small group of interested users knew. The same probably also applies to the much broader discipline of information security. So, what changed?

Information is not a new concept and has always been of value. Society has always dealt with information that has needed some protection and has always used processed to safeguard that information. There's nothing new about the need for infosec.

Likewise, cryptography isn't a new science, although some would say it has only recently been formally treated as such. It has been used for centuries to protect sensitive information, especially during periods of conflict.

However, information security is now a subject with a relatively high profile. Most people use information security mechanisms daily. Incidents of information security breaches are widely reported in the media. The reason for this increased profile has been the development of *computer networks*, particularly the **Internet**.

This development hasn't necessarily increased the amount of information globally, but data is now easier to generate, access, exchange and store. Lower communication and storage costs have increased connectivity, and higher processing speeds have encouraged the automation of business processes. As a result, more and more applications and services are conducted electronically. Since all this electronic data has the potential to be transmitted and stored in relatively insecure environments, the need for infosec has become paramount. 

The rising significance of information security has incresaed the importance of widespread use of cryptography. As we'll see, cryptography lies at the heart of most technical information security mechanisms. As a result, cryptography has become something most people use in every day applications. Once primarily the domain of government and the military, cryptography is now deployed on devices that most every consumer of technology carries in their pocket.

## Two Very Different Office Environments

It’s worth briefly considering precisely what types of physical security mechanisms we used to rely on before computer communication. Indeed, we still rely on many of these in physical situations. The fact that these security mechanisms cannot easily be applied to electronic environments provides the central motivation for defining cryptographic mechanisms.

### An Old Office

Imagine an office where there are no computers, no fax machines, no telephones, and no Internet. The business conducted in this office relies on information coming from both external and internal resources. The employees in this office need to make decisions about the accuracy and authenticity of the data. In addition, they need mechanisms for controlling who has access to information.

So, what basic security mechanisms allow the people working in such an office to make decisions about the security of the information the receive and process?

We can safely assume that most information dealt with in this office is either spoken or written down. Some basic security mechanisms for spoken information might include the following:

- Facial or vocal recognition of people who work in the office
- Personal referrals or letters of recommendation for people not known to those in the office.
- The ability to hold a private conversation in a quiet corner of the room.

Some basic security mechanisms for written information might be:

- Recognizing the handwriting of people who work in the office.
- Hand-written signatures on documents.
- Sealing documents in an envelope.
- Locking documents in a filing cabinet.
- Mailing a letter in an official mailbox.

These security mechanisms aren’t particularly strong. For example, people who don’t know each other well could misidentify a voice or a face. An envelope could be steamed open and its contents altered. A handwritten signature could be forged. Nonetheless, these mechanisms provide ‘some’ security, which is often ‘good enough’ security for many applications and organizations.

### A Modern Office

Now consider a modern office, full of computers that are networked to the outside world via the Internet. Although some information will undoubtedly be processed using some of the previous mechanisms, there will be a vast amount of information handled by electronic communication and storage systems for convenience and efficiency. Imagine that in this office nobody has considered the new information security issues.

Here's a list of just some of the security related questions that the staff in this office should be asking:

- How can we tell whether an email from a potential client is a genuine inquiry from the person it claims to have come from?
- How can we be sure that the contents of an electronic file have not been altered?
- How can we be sure that nobody else can read an email we have just sent to a colleague.
- How can we accept an electronic contract received by email from a client on the other side of the world?

Without adopting some information security mechanisms, the answer to all of these questions is probably ‘with incredible difficulty.’ While even a non-expert may notice that a physical envelope has a damaged seal (and hence get suspicious), it’s almost impossible to recognize whether an unauthorized party has accessed an unprotected email. It’s certainly possible to communicate much more quickly in this modern office. However, there’s a real case to be made for the claim that we have much less inherent security in this environment than in the strictly physical world of the old office.

# Perspectives and Security Infrastructure

Learn about the different perspectives on cryptography and the importance of having a good security infrastructure.

## Differing Perspectives

It should already be clear that there is a need for translation of the basic security mechanisms used in the physical world into mechanisms suitable for application in an electronic environment. In essence, this is what modern cryptography is all about. We aim to demonstrate precisely what role cryptography plays in this translation process. 

First, let's understand in a broad sense how cryptography fulfills a role in the provision of information security. Below, we identify three different perspectives on the use of cryptography. The vested interests that these represent, and some of the resulting conflicts, have helped shape the modern use of cryptography.

### Individual Perspective

Cryptography is a technology just like any other. Thus, the perspective of many individuals is that they have a right to use cryptography for any purpose they deem fit. As we discuss later, using cryptography to encrypt data can serve a function similar to sealing a document in an envelope in the physical world. So, why should individuals be denied the right to use encryption? Further, many people regard cryptography as a technology that enables them to realize other rights. Foremost among these are rights to privacy and freedom of expression.

### Business Perspective

For businesses, computer networks, especially open networks such as the internet, provide both great opportunities and significant risks. From a business perspective, cryptography is a technology that can be used to implement information security controls which, result in the business making more money than if these controls were not adopted.

It's a common misconception that business automation is often driven by a desire for increased security. This is in fact very rarely the case. An important early business application of cryptography was the adoption of automatic teller machines in the banking industry. These were introduced not to increase security but to increase availability and hence to increase business. In fact, it's arguably easier to defraud an automatic teller machine that it is to extort money from the counter of a bank.

Business automation usually leads to significant change int he threats to which a business is exposed. Unless these are carefully addressed, business automation can lead to a decrease in the level of security. The main business security requirement is that increased automation and adoption of technologies such as cryptography shouldn’t lead to a decrease in the overall security of conducting business. For example, when the GSM system was developed for mobile telecommunications, the designers intended GSM to be ‘as secure’ as landlines.

### Government Perspective

Governments often have conflicting requirements with respect to information security. One the one hand, they may wish to empower citizens and promote competitive business. They can do this by promoting the development of secure technologies and standards, reducing trade barriers, and harmonizing laws and regulations. On the other hand, governments may wish to control crime and manage issues of national security. They may try to do this by imposing certain controls and introducing other laws and regulations.

In the case of cryptography, these different governemental roile shave sometimes led to conflicts of interest. The fundamental problem that governments face arises from the traditional model of a cryptosystem, which involves 'good' users deploying cryptography to protect themselves from 'bad' attackers who attempt to access their information. 

The dilemma from a government’s perspective is that it may be the case that ‘bad’ users are deploying cryptography to hide their information from ‘good’ attackers (such as law enforcement officers) who could foil their activities if they had access to this information.

## The Importance of Security Infrastructure

The security commentator Bruce Schneier wrote a book called _Applied Cryptography_ in the early 1990s. A few years later, he wrote a book on computer security called _Secrets and Lies_. He claimed that during the writing of the second book he had an epiphany in which he realized that all the cryptographic mechanisms in _Applied Cryptography_ were almost immaterial compared to the real security problems associated with the provision of a complete information security system. The biggest problem wasn’t designing the cryptographic mechanisms themselves, but making cryptography actually work in a practical system through the provision of an entire information security architecture, of which cryptography was only a small but vital component.

This is an important issue and one that needs to be kept in mind throughout this course. Cryptography, just like any security technology, cannot be made to work without having the infrastructure in place to support its implementation. By ‘infrastructure,’ we mean the procedures, plans, policies, management—whatever it takes to make sure that the cryptographic mechanisms actually do the job for which they were intended.

We’ll consider certain aspects of this infrastructure. However, there are many aspects of this infrastructure that are well beyond the scope of our discussion. Ideally, computer operating systems, networks, and entire information systems should be planned, designed, implemented, and used securely. A perfectly good cryptographic mechanism can fail to deliver its intended security services if any one of these other areas of the security infrastructure fails.

This holistic attitude to information security is one that must always be kept in mind whenever a cryptographic application is designed or used. One of the aims of this is to identify which elements of this wider security infrastructure are particularly relevant to the effectiveness of a cryptographic application.

# Security Risks

Learn about the types of information exposure risks and explore the factors that determine which security mechanisms should be used.

## Types of Attack

We'll now consider the types of risk to which information is typically exposed. Risks to information can be accessed by identifying different types of possible attacks that can be attempted. These attacks are often classified by the type of action that an attacker has to perform. 

### Passive Attacks

The main type of *passive* attack is unauthorized access to data. This is a passive attack in the sense that the data and the processes being conducted on that data remain unaffected by the attack.

> [!NOTE] Note
> A passive attack is often likened to "stealing" information. However, unlike stealing physical goods, in most cases, theft of data still leaves the owner in possession of that data. As a result, information theft may go unnoticed by the owner. Indeed, it may even be undetectable.

### Active Attacks

An *active attack* involves either data being changed in some way to a process being conducted on the data. Examples of active attacks include the following:

- Unauthorized alterations of data.
- Unauthorized deletions of data.
- Unauthorized transmissions of data.
- Unauthorized tampering with the origin of the data.
- Unauthorized prevention of access to data (denial of service).

We will see that cryptography can be used as a tool to help prevent most passive and active attacks. A notable exception is a denial of service. There's very little protection that cryptography can provide against this type of attack. Defense against denial of service normally requires security control in other parts of the security infrastructure.

## Security Risks in a Simple Scenario

We now examine a very simple communication scenario and consider what security risks might exist. The simple scenario depicted in the figure above features a sender (who in the cryptographic world is often called *Alice*) and a receiver (who is usually called *Bob*). Alice wishes to transmit some information in an email to Bob. If Alice and Bob want to be certain about the security of the email they have just exchanged, then they should ask themselves some serious questions.

For example, Alice might be asking herself the following:
- Am I happy that anyone could read this email, or do I only want Bob to see it?
- How can I make sure that my email reaches Bon without being changed?
- Am I prepared (or allowed) to take any measures to protect my email before I send it?

Bob might ask himself the following questions:

- How can I have confidence that this email actually came from Alice?
- Can I be sure that this is the email Alice intended to send me?
- Is it possible that Alice could deny in the future that she sent this email?

This simple communication scenario (or variations thereof) is one we'll regularly return to when we consider different types of cryptographic mechanisms. However, it's important to realize that not all applications of cryptography conform to this simple communication scenario. For example, we may need to secure the following:

- A broadcast environment, where one sender is streaming data to a large number of receivers. 
- A data storage environment, which may not have an obvious endpoint.

At this stage, it helps to understand that there are other basic scenarios that each come with their own players and security risks. 

## Choosing Security Mechanisms

Alice and Bob's concerns discussed above may seem rather paranoid. Some people regularly encrypt emails and might regard these concerns as being important, while other people rarely encrypt emails and might regard the questions raised by Alice and Bob as being slightly absurd or at least 'over the top'.

These contradictory perspectives aren't surprising. Risk is **subjective**, and risk differ between applications. Indeed, the assessment and management of risk is major information security topic in its own right and one that many organizations devote entire departments to studying. It is prudent to think about questions such as those identified above, but whether we act on them and introduce security controls to address them is another issue altogether. 

In fact, there are at least three different issues to consider when contemplating the use of any security mechanism, including a cryptographic control:

1. **Appropriateness:** _Is it the right tool for the job?_ It’s important to understand the precise properties that a cryptographic mechanism will provide. One aim of this course is to explain how the various tools of cryptography can (and in some cases cannot) be used to provide different notions of security.
2. **Strength:** _Why put in an expensive burglar alarm in situations where a warning sign would suffice?_ Different information security mechanisms provide different levels of protection for data, just as different security mechanisms in the physical world come with a range of strengths of physical protection.
3. **Cost:** _Do the security gains justify the costs?_ The cost of a security mechanism is of fundamental importance. By ‘cost’ we don’t necessarily mean monetary value. Cost can be measured in terms of ease of use and efficiency of operation as well as directly in terms of financial worth. In many real applications, it’s considerations relating to cost that determine the security mechanism adopted rather than the strength of the security that the mechanism provides.
    In the past, some military and government sectors may have opted for strong security whatever the cost, but in most modern environments, this isn’t appropriate. A sensible commercial question might be ‘What strength of security is appropriate given the value of our assets?’ A more commonly asked question of modern security managers, however, is ‘_What strength of security can we obtain within our budgetary constraints?_’ One of the challenges of managing security in these environments is to make a case for information security controls. This case can often be built on the argument that good security may succeed in reducing other costs.

Returning to our email example, an appropriate tool that prevents emails from being read by unauthorized parties is encryption. The strength of encryption used is dependent on the cryptographic algorithm and the number of decryption keys. However, the drawback of this is that it's necessary to buy and install suitable software, manage the relevant keys, configure the email client appropriately, and bear time and communication costs every time the software is used.

So is it worth encrypting an email? There is, of course, no general answer, since this very much depends on the value of the information in the email and the perceived risks. However, the overall aim of this course is to advise how cryptography can help in this the type of situation and what the related issues are. We'll focus on explaining the appropriateness and strength of various cryptographic mechanisms; however, we'll also indicate where issues of cost may arise.

# Security Services

Learn about some important terminologies and explore some of the main security services.

## Basic Definitions

A _security service_ is a specific security goal that we may wish to achieve. We’ll now introduce the main security services in this course.

It’s worth noting that while security services sometimes relate directly to human beings, more often they relate to computers or other devices (often operating on behalf of human beings). While this distinction is important since it can have important security implications, we normally avoid concerning ourselves with it directly and use the generic terms ‘user’ and ‘entity’ in an interchangeable way to mean whoever, or whatever, is taking part in the processing of data in an information system.

### Confidentiality

*Confidentiality* is the assurance that data cannot be viewed by an unauthorized user. It's sometimes referred to as *secrecy*. Confidentiality is the 'classical' security service that can be provided by cryptography and is the one implemented by most historical applications. While it remains an important security service, there are many modern applications of cryptography that don't require the provision of confidentiality. Even when confidentiality is desired, it's rare for it to be the only security service that is required.

### Data Integrity

*Data Integrity* is the assurance that data has not been altered in an unauthorized (which includes **accidental**) manner. This assurance applies from the time the data was last created, transmitted, or stored by an authorized user. Data Integrity isn't concerned with the prevention of alteration of data but provides a means of detecting whether data has been manipulated in an unauthorized way.

### Data Origin Authentication

Data origin authentication is the assurance that a given entity was the original source of received data. In other words, if a technique provides data origin authentication that some data came from Alice, then this means that the receiver, Bob, can be sure the data did originally come from Alice at some time in the past.

Bob doesn’t necessarily care exactly when she sent it, but he does care that Alice is the source of the data. Nor does he care from which immediate source he obtained the data since Alice could have passed the data to an intermediary for forwarding (as is the case when data is passed over the Internet, where the immediate source of data may be a web server or router).

For this reason, data origin authentication is sometimes referred to as message authentication since it’s primarily concerned with the authentication of the data (message) and not who we are communicating with at the time the data is received.

### Non-Repudiation

*Non-Repudiation* is the assurance that an entity cannot deny a previous commitment or action. Most commonly, non-repudiation is the assurance that the original source of some data cannot deny to a third-party that this is the case. 

> [!NOTE] Note
> This is a stronger requirement than data origin authentication since data origin authentication only requires this assurance be provided to the *receiver of the data*.

Non-repudiation is a property that is most desirable in situations where there's potential for a dispute to arise over the exchange of data.

### Entity Authentication

_Entity authentication_ is the assurance that a given entity is involved and currently active in a communication session. In other words, if a technique provides entity authentication of Alice, then this means that by applying the technique, we can be sure that Alice is really engaging with us in ‘real-time’ now. If we fail to establish this temporal aspect of entity authentication (which requires the adoption of a freshness mechanism), then we have failed to achieve entity authentication. In certain contexts, entity authentication is referred to as identification because it’s concerned with determining who we are communicating with in real-time.

> [!NOTE]
> **Note:** These are by no means the only security services cryptography can provide. For example, we’ll see several applications that use cryptography to achieve anonymity.

# Relationships Between Security Services

Learn about the connections between the main security services.

It's important to recognize that these basic security services are all essentially different, even though on first encounter they may seem similar.

## Data Origin vs. Data Integrity