---
up: "[[Networking]]"
tags:
  - "#education/books/networking/topdownapproach"
source: "[[Computer Networking_ A Top-Down Approach, Global Edition, 8th Edition.pdf]]"
---

# Preface

Since the publication of the first edition over 20 years ago, this book has been adoped for use at many hundreds of colleges and universities, translated into 14 languages, and used by many hundreds of thousands of students and practitioners worldwide.
## What's New in the Eighth Edition?

- **Chapter 1**: has been updated to reflect the ever-growing reach and use of the internet, and of 4G/5G networks.
- **Chapter 2**: covers the application layer, has been significantly updated, including material on the new HTTP/2 and HTTP/3 protocols for the web.
- **Chapter 3**: updated to reflect advances in, and evolution in the use of, transport-layer congestion control and error-control protocols over the past five years. While this material had remained relatively stable for quite some time, there have been a number of important advances since the seventh edition. Several new congestion-control algorithms have been developed and deployed beyond the classic TCP algorithms. We provide a deeper coverage of:
	- TCP CUBIC, the default TCP protocol in many deployed systems, and examine delay-based approaches to congestion control, including the new BRR protocol, which is deployed in Google's backbone network.
	- QUIC protocol, which is being incorporated into the HTTP/3 standard. Although QUIC is not technically a transport-layer protocol - it provides application layer reliability, congestion control, and connection multiplexing services at the application layer.
- **Chapter 4**: covers the network-layer data plan, has general updates throughout. New section on *Middleboxes*, which perform network-layer functions other than routing and forwarding, such as firewalling and load-balancing. Middleboxes build naturally on the generalized "match plus action" forwarding operation of network-layer devices that we cover earlier in chapter 4. We've also added timely new material on the topics such as the amount of buffering that is "just right" in network routers, on net neutrality, and on the architectural principles of the internet.
- **Chapter 5**: updated material on SDN, and a significantly new treatment of network management. The use of SDN has evolved beyond management of packet-forwarding tables to include configuration management of network devices as well. We introduce two new protocols, **NETCONF** and **YANG**, whose adoption have fueled this new approach toward network management.
- **Chapter 6**: covers the link layer, has been updated to reflect the continuing evolution of Link Layer technologies such as Ethernet. We have also updated and expanded our treatment of datacenter networks, which are at the heart of the technology driving much of today's Internet commerce.
- As noted earlier, **Chapter 7** has been significantly updated and revised to reflect the many changes in wireless networking since the seventh edition, from short- range Bluetooth piconets, to medium-range wireless 802.11 local area networks (WLANs), to wide-area 4G/5G wireless cellular networks. We have retired our PREFACE 9 coverage of earlier 2G and 3G networks in favor of a broader and deeper treatment of today’s 4G LTE networks and tomorrow’s 5G networks. We have also updated our coverage of mobility issues, from the local issue of handover of mobile devices between base stations to the global issue of identity management and mobile device roaming among different global cellular networks.
- **Chapter 8**, which covers network security, has been updated to reflect changes in wireless and network security in particular, with new material on WPA3 security in WLANs, and mutual device/network mutual authentication and confidentiality in 4G/5G networks. 

**Chapter 9** has been retired. 
## Audience 

This textbook is for a first course on computer networking. It can be used both in computer science and electrical engineering departments. In terms of programming languages, the book assumes only that the student has experience with C, C++, Java or Python (even then only in a few places).

Although this book is more precise and analytical than any other introductory computer networking texts, it rarely uses any mathematical concepts that are not taught in high school. We have made a deliberate effort to avoid using any advanced calculus, probability, or stochastic process concepts.
# What is Unique about this Textbook?

The subject or computer networking is enormously complex, involving many concepts, protocols, and technologies that are woven together in an intricate manner. To cope with this scope and complexity, many computer networking texts are often organized around the "layers" of a network architecture. With a layered organization, students can see through the complexity of computer networking -- they learn about the distinct concepts and protocols in one part of the architecture while seeing the big picture of how all parts fit together. 
## A Top-Down Approach

This book begins at the application layer and works its way down toward the physical layer. This approach has been confirmed by teachers and students to work well pedagogically. Many recent revolutions in computer networking -- including the Web, media streaming -- have taken place at the application layer. An early emphasis on application layer issues differs from the approaches taken in other texts, which only have a small amount of material on network applications, their requirements, application-layer paradigms, and application programming interfaces. 

Second, our experience as intructors (and that of many instructors who have used this text) has been that teaching networking applications near the beginning of the course is a powerful motivational tool. Once a student learns about the services and protocols they use everyday, they gain interest and understanding in the layers below them. 

Third, a top down approach enables instructors to introduce network application development at an early stage. Students not only see how popular applications and protocols work, but also learn how easy it is to create their own network applications and application-layer protocols. With the top down approach, students get early exposure to the notions of *socket programming*, service models, and protocol -- important concepts that resurface in all subsequent layers. By providing socket programming examples in Python, we highlight the central ideas without confusing students with complex code. 
## An Internet Focus

Although we dropped the phrase "Featuring the Internet" from the title of this book, this doesn't mean that we dropped our focus on the Internet. We continue to use the Internet's architecture and protocols as primary vehicles for studying fundamental computer networking concepts. Of course, we also include concepts and protocols from other network architectures. 
# Teaching Network Principles

The field of networking is now mature enough that a number of fundamentally important issues can be identified. For example, in the transport layer, the fundamental issues include:

- reliable communication over an unreliable network layer
- connection/establishment teardown and handshaking
- congestion and control flow
- multiplexing

Three fundamentally important network-layer issues are determining "good paths" between two routers, interconnecting a large number of heterogeneous networks, and managing the complexity of a modern network

In the link layer, a fundamental problem is *sharing a multiple access channel*. 

In network security, techniques for providing *confidentiality, authentication and message integrity* are all based on cryptographic fundamentals. 

# Student Resources 
Student resources are available on the Companion Website (CW) at www. pearsonglobaleditions.com. 

Resources include:

• Interactive learning material. The book’s Website contains VideoNotes— video presentations of important topics throughout the book done by the authors, as well as walkthroughs of solutions to problems similar to those at the end of the chapter. We’ve seeded the Website with VideoNotes and online problems for Chapters 1 through 5. As in earlier editions, the Website contains the interactive animations that illustrate many key networking concepts. Professors can integrate these interactive features into their lectures or use them as mini labs.

- *Additional technical material.* As we have added new material in each edition of our book, we’ve had to remove coverage of some existing topics to keep the book at manageable length. Material that appeared in earlier editions of the text is still of interest, and thus can be found on the book’s Website. 

- *Programming assignments*. The Website also provides a number of detailed programming assignments, which include building a multithreaded Web server, building an e-mail client with a GUI interface, programming the sender and receiver sides of a reliable data transport protocol, programming a distributed routing algorithm, and more. 

 - *Wireshark labs*. One’s understanding of network protocols can be greatly deepened by seeing them in action. The Website provides numerous Wireshark assignments that enable students to actually observe the sequence of messages exchanged between two protocol entities. The Website includes separate Wire- shark labs on HTTP, DNS, TCP, UDP, IP, ICMP, Ethernet, ARP, WiFi, TLS and on tracing all protocols involved in satisfying a request to fetch a Web page. We’ll continue to add new labs over time.
# Chapter 1: Computer Networks and the Internet

Today's internet is arguably the largest engineered system ever created by mankind, with hundreds of millions of connected computers, communication links, and switches; with billions of users who connect via laptops, tablets and smartphones: and with an array of new Internet Connected "Things". including game consoles, surveillance systems, watches, eye glasses, thermostats and cars. 

This first chapter presents a broad overview of computer networking and the Internet. Our goal here is to paint a broad picture and set the context for the rest of this book, to see the forest through the trees. 

This chapter is structured as follows:

1. ***Basic Terminology and Concepts***
2. ***Basic Hardware and Software Components of Networks***
	- end systems and network applications running in the network
3. ***Core of a Computer Network***
	- links and switches that transport data, as well as the access netowrks and physical media that connect end systems to the network core.
4. ***The Internet is a Network of Networks***
5. ***Delay, Loss and Throughput of Data***
	- models that take into account *transmission, propagation, and queuing delays*.
6. ***Key Architectural Principles***
	- protocol layering and service models
7. ***Computer Network Attacks***
8. ***Brief History of Computer Networking***
## 1.1 What is the Internet?

In this book, we’ll use the public Internet, a specific computer network, as our principal vehicle for discussing computer networks and their protocols. But what is the Internet? There are a couple of ways to answer this question. First, we can describe the nuts and bolts of the Internet, that is, the basic hardware and software components that make up the Internet. Second, we can describe the Internet in terms of a networking infrastructure that provides services to distributed applications. Let’s begin with the nuts-and-bolts description, using Figure 1.1 to illustrate our discussion
### 1.1.1 A Nuts and Bolts Description

The Internet is a computer network that interconnects billions of computing devices throughout the world. Not too long ago, these computing devices were primarily traditional desktop computers, Linux workstations, and so-called servers that store and transmit information such as Web pages and email messages.

Increasingly, however, users connected to the Internet with smartphones and tablets -- today, close to half the world's population are active mobile Internet users with the percentage expected to increase to 75% by 2025. Furthermore, nontraditional Internet "things" such as TVs, gaming consoles, thermostats, home security systems, home appliances, watches, eye glasses, cars, traffic control systems, and more are being connected to the Internet.

Indeed, the term *computer network* is beginning to sound a bit dated, given the many non traditional devices that are being hooked up to the Internet. In Internet jargon, all of these devices are called **hosts** and **end systems**. 

![](https://i.imgur.com/dAauQBs.png)

End systems are connected together by a network of **communication links** and **packet switches**. We'll see in Section 1.2 that there are many types of communication links, which are made up of different types of physical media, including coaxial cable, copper wire, optical fiber, and radio spectrum. Different links can transmit data at different rates, with the **transmission rate** of a link measured in *bits/second*. When one end system has data to send to another end system, the sending end system segments the data and adds header bytes to each segment. The resulting packages of information, known as **packets** in the jargon of computer networks, are then sent through the network to the destination end system, where they are *reassembled* into the original data. 

A **packet switch** takes a packet arriving on one of its incoming communication links and forwards that packet on one of its outgoing communication links. Packet switches come in many shapes and flavors, but the two most prominent types in today's Internet are **routers** and **link-layer switches**. Both types of switches forward packets toward their ultimate destinations. Link-layer switches are typically used in the network core. The sequence of communication links and packet switches traversed by a packet from the sending end system tot he receiving end system is known as a **route** or **path** through the network. 

Packet-switched networks (which transport packets) are in many ways similar to transportation networks of highways, roads and intersections (which transport vehicles). Consider, for example, a factory that needs to move a large amount of cargo to some destination warehouse located thousands of miles away. At the factory, the cargo is segmented and loaded into a fleet of trucks. Each of the trucks then *independently travels* through the network of highways, roads and intersections to the destination warehouse. At the destination warehouse, the cargo is unloaded and grouped with the rest of the cargo arriving from the same shipment. 

Thus, in many ways:

- packets are analogous to trucks
- communication links are analogous to intersections
- end systems are analogous to buildings

End systems access the Internet through **Internet Service Providers (ISPs)**, including residential ISPs such as local cable or telephone companies: corporate ISPs, university ISPs, ISPs that provide WiFi access in airports, hotels, coffee shops, and other public places: and cellular data ISPs. 

Each ISP is in itself a *network of packet switches and communication links*. ISPs provide a variety of types of network access to the end systems, including residential broadband access such as a cable modem or DSL, high-speed local area network access, and mobile wireless access. 

ISPs also provide Internet access to content providers, connecting servers directly to the Internet. 

The Internet is all about connecting end systems to each other, so the ISPs that provide access to end systems must also be interconnected. These lower- tier ISPs are thus interconnected through national and international upper-tier ISPs and these upper-tier ISPs are connected directly to each other. An upper-tier ISP consists of high-speed routers interconnected with high-speed fiber-optic links. Each ISP network, whether upper-tier or lower-tier, is managed independently, runs the IP protocol (see below), and conforms to certain naming and address conventions. We’ll examine ISPs and their interconnection more closely in Section 1.3.

End systems, packet switches and other pieces of the internet run on **protocols** that control the sending and receiving of information within the Internet. The **Transmission Control Protocol (TCP)** and the **Internet Protocol (IP)** are two of the most important protocols on the internet. 

The IP Protocol specifies the *format of the packets* that are sent and received among routers and end systems. 

The internet's principal protocols are collectively known as **TCP/IP**. 

Given the importance of protocols to the Internet, it’s important that everyone agree on what each and every protocol does, so that people can create systems and products that interoperate. This is where standards come into play. Internet standards are developed by the Internet Engineering Task Force (IETF) [IETF 2020]. The IETF standards documents are called requests for comments (RFCs). RFCs started out as general requests for comments (hence the name) to resolve network and protocol design problems that faced the precursor to the Internet [Allman 2011]. RFCs tend to be quite technical and detailed. They define protocols such as TCP, IP, HTTP (for the Web), and SMTP (for e-mail). There are currently nearly 9000 RFCs. Other bod- ies also specify standards for network components, most notably for network links. The IEEE 802 LAN Standards Committee [IEEE 802 2020], for example, specifies the Ethernet and wireless WiFi standards.
### 1.1.2 A Services Description

We can describe the Internet from an entirely different angle -- namely, as an *infrastructure that provides services to applications*. In addition to traditional applications such as email and Web surfing, Internet applications include mobile smartphone and tablet applications, including Internet messaging, mapping with real-time traffic information, music streaming, movie and television streaming, online social media, video conferencing, multiplayer games, and location-based recommendation systems. 

The applications are said to be ***Distributed Applications***, since they involve multiple end systems that exchange data with each other. Importantly, Internet applications run on end systems, they do not run in the packet switches in the network core. Although packet switches facilitate the exchange of data among end systems, they are not concerned with the application that is the source of sink of data.

Because applications run on end systems, in order to make an Internet Application, you will need to write programs that run on the end systems. You might, for example, write your programs in Java, C, Python or another language. Now, because you are developing a distributed Internet applications, these programs running on the different end systems will need to *send data* to each other. 
	Here we get to a central issue -- one that leads to the alternative way of describing the internet as a platform for applications. How does one program running on one end system instruct the Internet to deliver data to another program running on another end system?

End systems connected to the internet provide a ***socket interface*** that specifies how a program running on one end system asks the Internet infrastructure to deliver data to a specific destination program running on another end system. This internet socket interface is a *set of rules that the sending program must follow* so that the Internet can deliver the data to the destination program. 

Let's draw upon a simple analogy, one that we will use frequently in this book. 
	Suppose Alice wants to send a letter to Bob using the postal service. Alice, of course, can't just write the letter (the data) and drop the letter out her window. Instead, the postal service requires that Alice put the letter in an envelope; seal the envelope; put a stamp in the upper right-hand corner of the envelope; and finally, drop the envelope in an official postal service mailbox. Thus, the postal service has its own "postal service interface" or set of rules, that Alice must follow to have the postal service deliver her letter to Bob. In a similar manner, the Internet has a socket interface that the program sending data must follow to have the Internet deliver the data to the program that will receive the data. 

The postal service, of course, provides more than one service to it's customers. It provides express delivery, reception confirmation, ordinary use, and many more services. In a similar manner, the Internet provides multiple services to its applications. When you develop an Internet application, you too must choose one of the Internet's services for your application. 

> We have just given two descriptions of the Internet; one in terms of its hardware and software components, the other in terms of an infrastructure for providing ser- vices to distributed applications. But perhaps you are still confused as to what the Internet is. What are packet switching and TCP/IP? What are routers? What kinds of communication links are present in the Internet? What is a distributed application? How can a thermostat or body scale be attached to the Internet? If you feel a bit over- whelmed by all of this now, don’t worry—the purpose of this book is to introduce you to both the nuts and bolts of the Internet and the principles that govern how and why it works. We’ll explain these important terms and questions in the following sections and chapters.
### 1.1.3 What is a Protocol?

Now that we've got a bit of a feel for what the Internet is, let's consider another important buzzword in computer networking: *protocol*. What is a protocol? What does a protocol do?
#### A Human Analogy

It is probably easiest to understand the notion of a computer network protocol by first considering some human analogies, since we humans execute protocols all of the time. Consider what you do when you want to ask someone for the time of day. 

![](https://i.imgur.com/X6EJaNe.png)

Human politeness dictates that one first has to offer a greeting ("hi") to initiate communication with someone else. The typical response to a "Hi" is a returned "Hi" message. Implicitly, one then takes a cordial "Hi" response as an indication that one can proceed to ask for the time of day. A different response to the initial "Hi" (such as "don't bother me") might indicate an unwillingness or inability to communicate. In this case, the human protocol would be not to ask for the time of day. Sometimes one gets no response at all to a question, in which case one typically gives up asking that person for the time. 

Note that in human protocol, *there are specific messages we send, and specific actions we take in response to the received reply messages or other events* (such as no reply within some given amount of time). Clearly, transmitted and received messages, and actions taken when these messages are sent or received or other events occur, play a central role in the human protocol. 

The same is true in networking -- it takes two (or more) communicating entities running the same protocol in order to accomplish a task. 

Let's consider a second human analogy. Suppose you're in a college class (computer networking, for example). The teacher is droning on about protocols and you're confused. The teacher stops to ask "Are there any questions?" (a message that is transmitted to, and received by, all students who are not sleeping). You raise your hand (transmitting an implicit message to the teacher). Your teacher *acknowledges* you with a smile, saying "Yes...." (a transmitted message encouraging you to ask your question -- teachers love to be asked questions), and then you ask your question (that is, transmit your message to your teacher). Your teacher hears your question (receives the message) and answers (transmits a reply to you).

Once again, we see that the tranmission and receipt of messages, and a set of conventional actions taken when these messages are sent and received, are at the heart of this question and answer protocol. 
#### Network Protocols

A network protocol is similar to a human protocol, except that the entities communicating messages and taking actions are hardware or software components of some device (for example, computer, smarthphone, tablet, etc.)

All activity in the Internet that involves two or more communicating remote entities is governed by a protocol. For example, hardware-implemented protocols in two physically connected computers control the flow of bits on the "wire" between the two network interface cards; congestion-control protocols in end systems control the rate at which packets are transmitted between sender and receiver; protocols in routers determine a packet's path from source to destination. Protocols are running everywhere in the Internet, and consequently much of this book is about computer network protocols.

As an example of a computer network protocol with which you are already familiar, consider what happens when you make a request to a web server, that is, when you type the URL of a webpage into your web browser. 

1. First, your computer will send a connection request message to the web server and wait for a reply. 
2. The web server will eventually receive your connection request message and return a connection reply message. 
3. Knowing that it is now OK to request the web document, your computer then sends the name of the Web page it wants to fetch from that web server in a GET message. 
4. Finally, the web server returns the web page file to your computer.

> A **protocol** defines the format and the order of messages exchanged between two or more communicating entities, as well as the actions taken on the transmission and/or receipt of a message or other event. 

> [!Important]
> Mastering the field of computer networking is equivalent to understanding the what, why, and how of networking protocols.
## 1.2 The Network Edge

We are now going to delve a bit more deeply into the components of the internet. We begin in this section at the edge of the network and look at the components with which we are most familiar -- namely, the computers, smartphones and other devices we use daily. 

![](https://i.imgur.com/WGVinav.png)
### Figure 1.3 End System Interaction

The Internet's **end systems** include various computers (e.g. Desktop PCs, Macs, and Linux boxes), servers (e.g. Web and email servers), and mobile devices (e.g. laptops, smartphones and tablets).

Furthermore, an increasing number of nontraditional "things" are being attached to the Internet as end systems (see the Case History feature).

End systems are also referred to as *hosts* because they host application programs such as web browser programs, a web server program, an email client program, or an email server program.

> [!Important] Data Centers and Cloud Computing
> Internet companies such as Google, Microsoft, Amazon and Alibaba have built massive data centers, each housing tens of thousands of hosts. These data centers are not only connected to the internet, but also internally include complex computer networks that interconnect the datacenter's hosts. The data centers are the engines behind the internet applications that we use on a daily basis.
> 
> Broadly speaking, data centers serve three purposes, which we describe here in the context of Amazon for concreteness. 
> 	1. First, they serve Amazon e-commerce pages to users, for example, pages describing products and purchase information.
> 	2. Second, they serve as massively parallel computing infrastructures for Amazon-specific data processing tasks.
> 	3. Third, they provide **cloud computing** to other companies.
> 	
> 	Indeed, today a major trend in computing is for companies to use a cloud provider such as Amazon to handle essentially *all* of their IT needs. For example, Airbnb and many other Internet-based companies do not own and manage their own data centers but instead run their entire web-based services in the Amazon cloud, called **Amazon Web Services**.
> 	
> 	The worker bees in a data center are the hosts. They *serve content*, (e.g. Web pages and videos), store emails and documents, and collectively perform massively distributed computations. The hosts in data centers, called blades and resembling pizza boxes, are generally commodity hosts that include CPU, memory and disk storage. The hosts are stacked in racks, with each rack typically having 20 to 40 blades. The racks are then interconnected using sophisticated and evolving data center network designs. Data center networks are discussed in greater detail in Chapter 6.

Throughout this book will will use the term hosts and end systems interchangeably: 

- ***host = end system***

Hosts are sometimes further divided into two categories:

- ***clients***
- ***servers***
### 1.2.1 Access Networks

Having considered the applications and end systems at the "edge of the network", let's consider the access network -- the network that physically connects an end system to the first router (edge router) on a path from the end system to any other distant end system.

![](https://i.imgur.com/BaUu3on.png)

> Several types of access networks, with thick, shaded lines and the settings (home, enterprise, and wide-area mobile wireless).
#### Home Access: DSL, Cable, FTTH, and 5G Fixed Networks

The two most prevalent types of broadband residential access are **digital subscriber line (DSL)** and **Cable**. A residence typically obtains DSL Internet access from the same local telephone company (telco) that provides its wired local phone access. Thus, when DSL is used, a customer's telco is also its ISP. 

As shown in Figure 1.5, each customer's DSL modem uses the existing telephone line exchange data with a digital subscriber line access multiplexer (DSLAM) located in the telco's local central office (CO). The home's DSL modem takes digital data and *translates it* to high-frequency tones for transmission over telephone wires to the COl the analog signals from many such houses are translated back into digital format at the DSLAM.

The residential telephone line carries both data and traditional telephone signals simultaneously, which are encoded at different frequencies:

- A high-speed downstream channel, in the 50 kHz to 1 MHz band
- A medium-speed upstream channel, in the 4 kHz o 50 kHz band
- An ordinary two-way telephone channel, in the 0 to 4 kHz band

This approach makes the single DSL link appear as if there were three separate links, so that a telephone call and an Internet connection can share the DSL link at the same time. 

![](https://i.imgur.com/bAH07Ik.png)

The DSL standards define multiple transmission rates, including downstream transmission rates of 24 Mbs and 52 Mbs, and upstream rates of 3.5 Mbps and 16 Mbps; the newest standard provides for aggregate upstream plus downstream rates of 1 Gbps. 

Because the downstream and upstream rates are different, the access is said to be *asymmetric*.

While DSL makes use of the telco's existing local telephone infrastructure, **Cable Internet Access** makes use of the cable television company's existing cable television infrastructure. 

![](https://i.imgur.com/D7VBgCZ.png)

Fiber optics connect the cable head end to neighborhood-level junctions, from which traditional coaxial cable is then used to reach individual houses and apartments. Each neighborhood junction typically supports 500 to 5000 homes. This is often referred to as **Hybrid Fiber Coax** (HFC).

Cable internet access requires special modems, called cable modems. The cable modem is typically an external device and connect to the home PC through an Ethernet port. At the cable head end, the cable modem termination system (CMTS) serves a similar function as the DSL network's DSLAM -- turning the analog signal sent from the cable modems in many downstream homes back into digital format. 

One important characteristic of cable internet access is that is a *shared broadcast medium*. In particular, every packet sent by the head travels downstream on every link to every home and every packet sent by a home travels on the upstream channel to the head end. For this reason, if several users are simultaneously downloading a video file on the downstream channel, the actual rate at which each user receives the video file will be *significantly lower* than the aggregate cable down-stream rate. 

On the other hand, if there are only a few active users and they are all web-surfing, then each of the users may actually receive web pages at the full cable downstream rate, because the users will rarely request a webpage at exactly that same time. Because the upstream channel is also shared, a *distributed multiple access protocol* is needed to coordinate transmissions and avoid collisions. 

Althrough DSL and cable networks currently represent the majority of residential broadband access, an up and coming technology that provides even higher speeds is **fiber-to-the-home** (**FTTH**). As the name suggests, the FTTH concept is simple -- provide Internet access rates in the gigabits per second range. 

There are several competing technologies for optical distribution from the CO to the homes. The simplest distribution network is called **direct fiber**, with one fiber leaving the CO for each home. 
	More commonly, each fiber leaving the central office is actually shared by many homes; it is not until the fiber gets relatively close to the homes that it is split into individual customer-specific fibers. 

There are two competing optical-distribution network architectures that perform this splitting:

1. **Active Optical Networks** (AON)
2. **Passive Optical Networks** (OAN)

In addition to DSL, Cable and Fiber, **5G Fixed Wireless** is beginning to be deployed. 5G fixed wireless not only promises high-speed residential access, but will do so without installing costly and failure-prone cabling from the Telco's CO to the home. 

5G Fixed wireless uses **beam-forming technology**, data is sent wirelessly from a provider's base station to the modem in the home. A WiFi router is connected to the modem (possibly bundled together), similar to how a WiFi wireless router is connected to a cable or DSL modem. 
#### Access in the Enterprise (and the Home): Ethernet and WiFi

On corporate and university campuses, and increasingly in home settings, a local area network is used to connect an end system to the edge router. Ethernet is by far the most prevalent access technology in corporate, university, and home networks. 

![](https://i.imgur.com/yYl8tug.png)

Ethernet users use twisted-pair copper wire to connect to an Ethernet switch, a technology discussed in detail in Chapter 6. The Ethernet switch, or a network of such interconnected switches, is then in turn connected into the larger Internet. With Ethernet access, users typically have 100 Mbps to tens of Gbps access to the Ethernet switch, whereas servers may have 1 Gbps 10 Gbps access.

Increasingly, however, people are accessing the Internet wirelessly from laptops, smartphones, tablets, and other "things". In a wireless LAN setting, wireless users transmit/receive packets to/from an access point that is connected into the enterprise's network (most likely using wired Ethernet), which in turn is connected to the wired Internet. 

A wireless LAN user must typically be within a few tens of meters of the access point. Wireless LAN access based on IEEE 802.11 technology, more colloquially known as WiFi, is now just about everywhere -- universities, business offices, cafes, airports, homes and even in airplanes.

Even though Ethernet and WiFi access networks were initially deployed in enterprise (corporate, university) settings, they are also common components of home networks. Many homes combine broadband residential access (that is, cable modems or DSL) with these inexpensive wireless LAN technologies to create pow- erful home networks Figure 1.9 shows a typical home network. This home network consists of a roaming laptop, multiple Internet-connected home appliances, as well as a wired PC; a base station (the wireless access point), which communicates with the wireless PC and other wireless devices in the home; and a home router that con- nects the wireless access point, and any other wired home devices, to the Internet. This network allows household members to have broadband access to the Internet with one member roaming from the kitchen to the backyard to the bedrooms.

![](https://i.imgur.com/Jz6apun.png)
#### Wide-Area Wireless Access: 3G and LTE 4G and 5G

Mobile devices such as iPhones and Android devices are being used to message, share photos in social networks, make mobile payments, watch movies, stream music, and much more while on the go. These devices employ the same wireless infrastructure used for cellular telephony to send/receive packets through a base station that is operated by the **cellular network provider**. 
	Unlike WiFi, a user only needs to be within a few tens of kilometers of the base station.
### 1.2.2 Physical Media

In the previous subsection, we gave an overview of some of the most important network access technologies in the Internet. As we described these technologies, we also indicated the physical media used. For example, we said that HFC uses a combination of fiber cable and coaxial cable. We said that DSL and Ethernet use copper wire. And we said that mobile access networks use the radio spectrum. In this subsection, we provide a brief overview of these and other transmission media that are commonly used in the Internet. 

In order to define what is meant by a **physical medium**, let us reflect on the brief life of a bit.

Consider a bit travelling from one end system, through a series of links and routers, to another end system. This poor bit gets kicked around and transmitted many, many times! 

- The source end system first transmits the bit
- The first router in the series receives the bit, then transmits the bit, and so on.
- Thus our bit, when travelling from source to destination, passes through a series of transmitter-receiver pairs. 
- For each transmitter-receiver pair, the bit is sent by propagated electromagnetic waves or optical pulses across a **physical medium**.

The physical medium can take many shapes and forms and does not have to be of the same type for each transmitter-receiver pair along the path. 

Examples of **physical media** include:

- Twisted-pair copper wire
- Coaxial cable
- Multi-mode fiber-optic cable
- Terrestrial radio spectrum
- Satellite radio spectrum

Physical Media fall into two categories:

1. ***Guided Media***
	- The waves are guided along a *solid medium*, such as a fiber-optic cable, twisted pair cable, or coaxial cable.
2. ***Unguided Media**
	- The waves propagate in the atmosphere or outer space, such as in a Wireless LAN or digital satellite channel.
#### Costs

The actual cost of the physical link (copper wire, fiber-optic cable, and so on) is often relatively minor compared with other networking costs. In particular, the labor cost associated with the installation of the physical link can be orders of magnitude higher than the cost of the material.

For this reason, many builders install twisted pair, optical fiber, and coaxial cable in every room in a building. Even if only one medium is initially used, there is a good chance that another medium could be used in the near future, and so money is saved by not having to lay additional wires in the future.
#### Twisted-Pair Copper Wire

The least expensive and most commonly used guided transmission medium is *twisted-pair* 
*copper wire*. For over a hundred years it has been used by telephone networks. In fact, more than **99 percent** of the wired connections from the telephone handset to the local telephone switch use twisted pair copper wire. 

Twisted pair consists of two insulated copper wires, each about 1mm thick, arranged in a regular spiral pattern. The wires are twisted together to reduce the *electrical interference* from similar pairs close by. 

Typically, a number of pairs are bundled together in a cable by wrapping the pairs in a protective shield. A wire pair constitutes a single communication link. **Unshielded twisted pair** (UTP) is commonly used for computer networks *within a building*. Data rates for LANs using twisted pair today range from 10 Mbps to 10 Gbps. 

> Modern twisted-pair technology, such as category 6a cable, can achieve data rates of 10 Gbps for distances up to a hundred meters. In the end, twisted pair has emerged as the dominant solution for high-speed LAN networking.
#### Coaxial Cable

Like twisted pair, coaxial cable consists of two copper conductors, but the two conductors are concentric rather than parallel. With this construction and special insulation and shielding, coaxial cable can achieve high data transmission rates. Coaxial cable is quite common in cable television systems. 

In cable television and cable Internet access, the transmitter shifts the digital signal to a specific frequency band, and the resulting analog signal is sent from the transmitter to one or more receivers. Coaxial cable can be used as a guided **shared medium**. Specifically, a number of end systems can be connected directly to the cable, with each of the end systems receiving whatever is sent by the other end systems. 
#### Fiber Optics

An optical fiber is a thin, flexible medium that conducts pulses of light, with each pulse representing a bit. A single optical fiber cable can support tremendous bit rates, up to tens or even hundreds of gigabits per second. They are *immune to electromagnetic interference*, have very low signal attenuation up to 100 kilometers, and are very hard to tap. 

These characteristics have made fiber optics the preferred long-haul guided transmission media, particularly for *overseas links*. 

Fiber optics is also prevalent in the backbone of the Internet. However, the high cost of optical devices -- such as transmitters, receivers and switches -- has hindered their deployment for short-haul transport, such as in a LAN or into the home in a residential access network. 

> The Optical Carrier (OC) standard link speeds range from 51.8 Mbps to 39.8 Gbps; these specifications are often referred to as OC-n, where the link speed equals n × 51.8 Mbps. Standards in use today include OC-1, OC-3, OC-12, OC-24, OC-48, OC-96, OC-192, OC-768.
#### Terrestrial Radio Channels

Radio channels carry signals in the electromagnetic spectrum. They are an attractive medium because they require no physical wire to be installed, can penetrate walls, provide connectivity to a mobile user, and can potentially carry a signal for long distances. The characteristics of a radio channel depend significantly on the propagation environment and the distance over which a signal is to be carried. 

Environmental considerations determine path loss and shadow fading (which decrease the signal strength as the signal travels over a distance and around/through obstructing objects), multipath fading (due to signal reflection off of interfering objects), and interference (due to other transmissions and electromagnetic signals.)

Terrestrial radio channels can be broadly classified into three groups: those that operate over very short distance (e.g. with one or two meters); those that operate in local areas, typically spanning from ten to a few hundred meters; and those that operate in the wide area, spanning tens of kilometers. Personal devices such as wireless LAN technologies described in section 1.2.1 use local-area radio channels; the cellular access technologies use wide-area radio channels. 
#### Satellite Radio Channels

A communication satellite links two or more Earth-based microwave transmitter/receivers, known as **Ground Stations**. The satellite receives transmissions on one frequency band, regenerates the signal using a repeater (discussed below), and transmits the signal on another frequency. Two types of satellites are used in communications: **geostationary satellites** and **low-earth orbiting (LEO) satellites**.

**Geostationary Satellites** permanently remain above the same spot on Earth. This stationary presence is achieved by placing the satellite in orbit at 36,000 meters above the Earth's surface. This huge distance from ground station through satellite back to ground station introduces a substantial signal propagation delay of 280 ms.

LEO satellites are placed much closer to Earth and do not remain permanently above one spot on Earth. They rotate around Earth, and may communicate with each other, as well as ground stations. They provide continuous coverage to an area, to do so, many need to be placed in orbit. LEO satellite technology may be used for Internet access sometime in the future.
## 1.3 The Network Core

Having examined the Internet's edge, let us now delve more deeply inside the network core -- the mesh of packet switches and links that interconnects the Internet's end systems. 

![](https://i.imgur.com/SKAo9Wo.png)
### 1.3.1 Packet Switching

In a network application, end systems exchange **messages** with each other. Messages can contain anything the application designer wants. Messages may perform a control function (for example "Hi" messages in our handshaking example in Figure 1.2) or can contain data, such as an email message, a JPEG image, or an MP3 audio file. To send a message from a source end system to a destination end system, the source breaks long messages into smaller chunks of data known as **`packets`**. 

Between source and destination, each packet travels through communication links and **packet switches** (for which there are two predominant types, **routers** and **link-layer switches**). Packets are transmitted over each communication link at a rate equal to the *full* transmission rate of the link.
	So, if a source end system or a packet switch is send a packet of L bits over a link with transmission rate R bits/sec, then the time to transmit the packet is L/R seconds. 
### Store-and-Forward Transmission

Most packet switches use **store-and-forward transmission** at the inputs to the links. Store-and-forward transmission means that the packet switch must receive *the entire packet* before it can begin to transmit the first bit of the packet onto the outbound link. To explore store-and-forward transmission in more detail, consider a simple network consisting of two end systems connected by a single router, as shown in Figure 1.11.

A router will typically have many incident links, since it's job is to switch an incoming packet onto an outgoing-link; in this simple example, the router has the rather simple task of transferring a packet from one (input) link to the only other attached link. In this example, the source has three packets, each consisting of $L$ bits, to send to the destination.

At the snapshot time shown in Figure 1.11, the source has transmitted *some* of packet 1, and the front of packet 1 has already arrived at the router. Because the router employs store and-forwarding, at this instant of time, the router **cannot transmit** the bits it has received; instead it must first **buffer** the (store) the packet's bits. 
	Only after the router has has received *all* of the packet's bits can it begin to transmit (i.e. "forward") the packet onto the outbound link. 

To gain some insight into store-and-forward transmission, let's now calculate the amount of time that elapses *from when the source begins to send the packet until the destination has received the entire*
*packet*.
	