
> AV integration into networks leverages the accessibility and mobility only networked systems can offer. Whether AV Networks operate independently or together with an IT system, supporting their deployment and execution is important to ensure a highly available infrastructure. 

### Objectives

Upon completion of this course, you will be able to:

- Define the communication protocols for interoperability between devices and networks
- Recognize the various types of network topologies
- Identify the components that make up a network
- Recognize the standards organizations that develop guidelines for network system operations
- Understand the importance of network security and how its implemented
- Define the process of how networks are designed and deployed

# Introduction to Networking

### What is a Network

> A network is simply a collection of hardware devices that are connected, either physically or logically, using special hardware and software that allows them to exchange information. 

The processes involved in designing, implementing, managing and working with these technologies to enable network communication is described as networking. 

#### The Significance of Networking

> In an organization, networks are one of the most critical resources. The reliability and responsiveness of daily operations are vital for success. When the network is down, it is costly when employees cannot access network resources like printers or file servers. 

- For networks to work reliably and securely, careful consideration is given on how much information is connected, and stored, especially when sharing documents, email, media, pictures, AV devices, printers, and cameras.

### AV and IT Integration

With the adoption and standardization at the IT level of quality and performance, AV industry products and devices have become increasingly network-friendly. This integration of IP communication delivers several advances in AV control and configuration:

- AV distribution across long distances, over the network
- Dedicated AV local area network function included with control processors
- AV over IP solutions with streaming capabilities
- Signal extension with the user of *encoders* and *decoders*
- System scalability, reliability, flexibility and expansion
- Centrally managed and secure. 

> What are encoders and decoders?
> 
> 	An *encoder* takes information from one video or audio format and converts it to another. 
> 	A *decoder* then receives the encoded signal and converts it back to the original signal, or into a new video or audio format.

### General Network Categories

> So, how are networks categorized? There are many types of networks, which are primarily distinguished by their size, capability, and purpose. Other distinctions are based on the distance between devices, and the general mechanisms used to communicate.

Networks can be divided into three general classes:

1. Local Area Network (LAN)
2. Wireless Local Area Network (WLAN)
3. Wide Area Network (WAN)

#### Local Area Network

A ***local area network*** - LAN uses physical wiring to connect devices within a home, school or office. Normally, a LAN is comprised of computers, peripheral devices, and local servers. This server provides access to shared applications, printers and disk storage.

#### Wireless Local Area Network

A ***wireless local area network***, or WLAN, connects wireless devices to each other using high frequency radio signals to communicate data. The term Wi-Fi, refers to a device's ability to operate within a wireless network, or WLAN. 

#### Wide Area Network

A ***wide area network*** - WAN connects networks that are located in different geographical locations. WANs provide communication as one large network for smaller networks or LANs.

### Specialized Network Categories

> Accessing the internet or downloading files from a network can be performed in several ways. 
> 
> The following types of networks provide additional services to access and transfer data even further:

1. **Virtual Private Network (VPN)**
2. **Virtual Local Area Network (VLAN)**
3. **Audio Video Local Area Network (AV LAN)**

#### Virtual Private Network

A ***virtual private network*** allows its users on a less secure network to send and receive data through a safe connection. By extending a private network across the internet, VPNs allow employees to be at home or travel, and access their company's network remotely, in the same way as if they were at work.

#### Virtual Local Area Network

As noted earlier, computer networks can be segmented into LANs and WANs. A **Virtual Local Area Network - VLAN** is a logical grouping of workstations, servers and network devices that are configured to appear on the same LAN, despite their physical location. The ability for VLANs to segment several networks and communicate virtually as one LAN, on *a single broadcast domain*, improves network performance, scalability, security features, and network management. A network switch can have multiple VLANs on a single switch.


> What is a ***Broadcast Domain?*** 
> 
> In networking, a broadcast means that *something is sent out so that everything receives it.* A broadcast domain is a collection of network devices that receiver broadcast traffic from each other. For example, a network switch forwards broadcast traffic on all of its interfaces, except the one it received the broadcast on.

#### Audio Video Local Area Network - AV LAN

> An ***Audio Video Local Area Network - AV LAN*** is a dedicated network specifically for providing secure control of local AV devices from outside interference or intrusion. It is similar to a VLAN, since it creates a separate broadcast domain for the AV devices. AV LANs allow for the AV system to run even if it's been disconnected from the LAN.

Extron AV LAN ports can be found in various models of the Pro Series control processor. There are also several products with AV LAN capabilities built-in, and some with AV LAN ports that provide PoE - Power over Ethernet.

- This allows communication to external supported devices, such as TouchLink Pro touchpanels and user interfaces. 
### Defining a Network

> Networks can be classified by the number of devices, its scope or abilities. Additionally, other types of networks exist that control various levels of access for users inside and outside of an organization. 

The ***Internet*** is the world's largest global, public, worldwide collection of networks. It links millions of individuals, businesses, government agencies, and educational institutions, though not controlled by a central entity. Its loose security allows user access to services, web browsing, email, file transfer, chat rooms, instant messaging, etc. 

The ***Intranet*** is a private network within an organization that resembles the Internet. It's high security resides behind firewalls that provide employee information, internal company applications, phone directories, email addresses, internal job openings, etc.

An ***Extranet*** is a private network connecting more than one organization. It uses VPN technology to allow limited network access for suppliers, customers, and business partners. 

# Communication

### Packet Switching

> How do networks transfer data and communicate? By using ***Packet Switching***, a communication method that splits data traffic into parts. These packet frames are labeled with a destination address and sequence number for transmitting across the network. 

During transmission, the data packets may follow the same or different route through various devices to reach their destination. 

Subsequently, the original data is reassembled in the correct order, based upon the sequence number contained within the message packet. 

> ***Packets*** are units of data transmitted over the network. Before being sent, the data is divided into more manageable segments so that information can be transmitted more efficiently instead of sending a single, large file. 

### Internet Protocol

> The set of rules that define how computers and devices communicate over a network is called **Internet Protocol** (IP). 

An IP system manages the traffic for the network and provides information needed for routing, essentially telling the packets where to go. 

There are several versions of Internet Protocol. Previous versions were exploratory and used in the late 1970s. The most widely used and dominant version is *Internet Protocol Version 4 - IPv4*.

Extron leverages IPv4 for IP-enabled products. The version that followed was IPv5, created as an experimental streaming protocol. After several years of experimentation with other protocols and models, the most current protocol is IPv6 technology that is being deployed by the U.S. government.

### Transmission Control Protocol

> Controlling the flow of data is important for a network's ability to provide sufficient access, bandwidth, and security. 

The ***Transmission Control Protocol*** (TCP) defines the amount of traffic over the network and is responsible for the actual delivery of data. TCP is considered a connection-oriented protocol. Once a connection is established, packets can be sent bidirectionally. 

TCP's error-checking mechanism ensures all data sent from one device is received by the destination device. As data arrives (or fails to arrive) TCP sends messages back to the originating device, informing it of which data has safely reached its destination and what has not. If needed, the originating device will resend data to complete the transmission.

TCP and IP work together to control network data transmission. Collectively, they are the Internet Protocol Suite known as ***TCP/IP***.

### User Datagram Protocol

An alternative communication protocol is the **User Datagram Protocol**, which is primarily used for establishing low-latency and loss tolerating connections between applications on the internet. 

- Both UDP and TCP run on top of the IP network to send short packets of data, called *datagrams*.

UDP provides two services; port numbers to help distinguish user requests, and a checksum capability to verify that the data arrived intact. Designed for time sensitive application, UDP sends just packets, resulting in much lower bandwidth overhead and latency. 

If a packet is late, it is not used. In addition, with the elimination of error-checking, packets can be lost. 

### Device Address

> Every device on the network is assigned an **IP Address** so they can communicate. IP addresses are unique numerical identifiers that consist of 32 bits, divided into *four octet parts*. 

Instead of being written in binary 1's and 0's, IP addresses use decimal format, from 0-255. Values start at 0, which is "00000000" in binary, and end with 255, which is "11111111" in binary.

There are, however, differences between IPv4 and IPv6 addresses.

- IPv4, which uses 32-bit decimal-based values (0-255) are expressed as dot addresses, and provides 4.3 billion combinations. 
- Whereas, IPv6 uses 128-bit Hexadecimal values (0-FFFF) with approximately 340 undecillion addresses.
### IP Address Types

> Network Devices are assigned an IP address in two ways. Addresses that are manually configured for devices are a ***Static IP Address***. It's called static because it is fixed, and does not change, the exact opposite of a dynamic IP address, which can change.

Devices that are connected to a Dynamic Host Configuration Protocol - DHCP server can be automatically assigned a **Dynamic IP Address** each time it connects to the network. The address comes from a pool of valid IP addresses defined by the network administrator. 

They're used for a specific amount of time, called a lease. When a lease is about to expire, the host will ask the DHCP server to reuse the address and the lease will be renewed. If the address does not connect to the DHCP server and the lease expires, it will be retuned to the address pool used by another device. 

> ***DHCP Reservation*** is a feature in the DHCP server that reserves one or more IP addresses for particular computers. The IP address remains in the DHCP address pool and will be assigned to the computer whose *MAC Address is mapped to it.*

### Network Subnetting

> As you might suspect, some networks can be rather large. Fortunately, networks can be divided into partitions or logical sub-sections called **Subnets**. These subnets use routers to determine access and control access across the entire network. Partitioning of a network is useful for security and performance, improving bandwidth, and easing network administration.
### Subnet Mask

> The process by which subnetting takes place is through the use of a **Subnet Mask**. Given that an IP address consists of two parts (network and host), a subnet mask hides, *or "masks", the network part of a system's IP address and leaves only the host part as the device identifier.* 
> 
> 	This helps to determine what subnet an IP address belongs to.


Subnet makes are 32-bit binary numbers, but normally communicated in dot decimal format. The binary octet portion of 11111111 (255 decimal) defines the network address. The binary octet portion of 0000000 (0 decimal) defines the host address.

- Binary: 11111111.1111111.11111111.00000000
- Decimal: 255.255.255.0

For the example below, using an IP address of 192.168.1.1 and a Subnet Mask of 255.255.255.0 portion represents the 192.168.1 network, and the 0 octet block represents the host portion.

- IP Address: 192.168.1.1
- Subnet Mask: 255.255.255.0
- Binary IP: 11000000.10101000.00000001.00000001
- Binary Mask: 11111111.11111111.1111111.00000000

# Default Gateway

> Within a networking infrastructure, the ***Default Gateway*** is used to connect two independent networks together. 
> 
> The gateway allows the devices from one network within specified IP settings to connect with devices of another network with different IP settings.

For the example, if a network has an address of 192.168.1 and another has an address of 10.1.20, alone they cannot communicate with each other. Using a default gateway, these networks can be connected allowing data to be sent from a device on the first network to the second. 
### MAC Address

> Another means of identifying each network device is by a ***MAC Address***, Media Access Control. 

These are unique 48-bit identifiers expressed as a 12-digit hexadecimal numbers, separated by dashes or colons. 

MAC Addresses cannot be modified by the network administrator as they are assigned by the device manufacturer as a  **Burned In Address** - BIA. The first six digits are the manufacturer's registered ID number, and the remaining digits represent the unique number for that device. 

- For example, with the MAC address 00-05-A6-0A-37-05, the manufacturer's ID numbers 00-05-A6 identify the device as an Extron product, and 0A-37-05 are the explicit numbers assigned by Extron to the product.

## The OSI Reference Model

> When it comes to networking, several models exist to explain the roles played by various technologies, and how they interact. Of these, the most commonly used is the ***OSI - Open Systems Interconnection Reference Model***.

The OSI Reference model is a set of riles, procedures and formats developed to manage network communication. The idea behind the OSI reference model is to provide a framework for both designing network systems and for understanding how they work. 

The seven levels, or layers of the OSI Model make it easier for network to be analyzed and built. This allows networks to be considered as modular pieces that interact in predictable ways, rather than large, complex domains. 

With the OSI model, the data flows from the Application Layer 7 down to the Physical Layer 1, then back up through the other layers to Layer 7.
### Physical Layer 1

> The lowest layer of the OSI Reference Model is **Physical Layer 1**. This is the physical medium that carries the data bit stream, the actual ones and zeroes that are sent over the network. 

The main responsibilities of the physical layer include the following functions:

- **Hardware Specification**: provide operation details for cables (CAT6 or fiber), connectors, wireless radio transceivers, Network Interface Cards - NIC, and other hardware devices./
- **Encoding and Signalling**: transforms the data from bits that reside within a device into signals that can be sent over the network.
- **Transmission and Reception**: transmits and receives the data after encoding.
- **Topology and Physical Network Design**: provides an important domain for hardware related network designs in LAN and WAN topology.
### Data Link Layer 2

> The second lowest layer in the OSI Model is the ***Data Link Layer 2***, which handles error detection and flow control for frames on the physical link of the network.

THe following tasks are performed at the data link layer:

- **Logical Link Control - LLC**: considered a sublayer for the establishment of the links between local network devices. 
- **Media Access Control** - **MAC** is the label information that defines the destination location for each network device to control access. Layer 2 switches move frames around by using the MAC address of each device.
- **Data Framing** - is the final encapsulation of higher-level messages into frames that are sent at the physical layer.
- **Error Detection** - using a Cyclic Redundancy Check - CRC field to detect if frames are received correctly. 
### VLAN Tagging

> As defined by the IEEE 802.1Q Networking standard, an additional function that can be done at Layer 2 is **VLAN Tagging**. When a frame enters the VLAN-aware portion of the network, a tag is added to represent the VLAN membership. 

Each frame must be distinguishable as being within exactly one VLAN. A frame that does not contain a VLAN tag, also referred to as "un-tagged", is assumed to be flowing on the native VLAN.

- For example, a frame entering a port of a switch will be tagged for a specific VLAN, then the frame will be sent across the network to a switch of the same VLAN. 
- Once received, the switch will remove the VLAN tag before the frame exits the port. 

### Network Layer 3

The third-lowest layer of the OSI reference model is ***Network Layer 3***, that defines how interconnected networks perform the following operations. 

- ***Logical IP Addressing***: for every device that communicates over a network, sometimes called a layer three address.
- ***Domain Name System - DNS***: that converts a URL name to an IP Address. For example, google.com has an IP Address of 8.8.8.8. Routers only know how to route traffic via the IP address.
- ***Fully Qualified Domain Name - FQDN***: specifies its top-level domain name, its local host, and reveals the Web page as its actual Uniform Resource Locator - URL. For example, maps.google.com.
- ***Windows Internet Naming Service - WINS***: provides name resolution on TCP/IP networks.
- ***Datagram Encapsulation***: of messages received from various sources, and determines their destination, or next hop to get to that destination.
- ***Error Handling and Diagnostic***: protocols allow devices that are trying to route traffic, to exchange information about the status of hosts on the network or the devices themselves. 

#### Security, Addressing and Troubleshooting

Additional functions within Layer 3 consists of the following protocols. 

***Internet Protocol Security - IPSec***: is a framework of open standards for ensuring private, secure communications over Internet Protocol - IP networks, using cryptographic (solving codes) security services. 

***Address Resolution Protocol - ARP***: lies between layers 2 and 3 as a protocol for translating network layer addresses into link layer addresses. ARP allows computers to introduce each other across a network prior to communication and only move traffic via MAC address.

***Internet Control Message Protocol - ICMP***: provides troubleshooting, control and error message services. ICMP is most frequently used in operating systems for networked computers, where it transmits error messages. 

- An example of ICMP is the PING command to verify that a computer can communicate over the network with another computer or network device.

### Comparing Switches

> Switches are used to *link network devices together and transfer data from one port to another based on information within the packets being transmitted.*

These network switches are often described as layer 2 or layer 3, but what exactly does that mean?

The main function of a Layer 2 (MAC) switch is to *forward traffic within a LAN based on the MAC address of both sending and receiving devices*.  

- This is performed by building a table of all the MAC addresses it has learned and what physical port they can be found on. Since Layer 2 switches are not able to apply any intelligence when moving packets, they have little impact on network performance or bandwidth.

The functions for crossing traffic between subnets, LANs (or VLANs) based on the IP address or priority, become available at the Network Layer, using a Layer 3 (IP) switch. These switches support Static Routing between VLANs, and Dynamic Routing to link large networks together, share routing tables, and allow for multicast traffic on the network. 

Quality of Service - QoS is supported in both Layer 2 and Layer 3. Unmanaged switches ignore and pass the QoS tags in the Layer 2 frame. 

Layer 3 switches can apply QoS classifications and VLAN tags. Since QoS is an egress protocol across a switch port, it will determine the sequence by which data exits a port based on priority.
### Transport Layer 4

> The "middle" layer of the OSI reference model is **Transport Layer 4**. This layer provides an overall end-to-end communication path between the lower layers and the applications at the higher layers. 

The following protocols reside as part of the Transport layer:

- **Real-time Transport Protocol - RTP**: specifies the way programs manage the real-time transmission of multimedia data over unicast or multicast network services.  
- **Real Time Streaming Protocol - RTSP**: is a network control protocol designed to control streaming media servers and sessions between end points.
- **Real-Time Messaging Protocol - RTMP** is a protocol for streaming audio, video and data over the Internet, between a Flash player and a server. 
### Session Layer 5

> A Session is a *persistent logical linking of two software application processes*, to allow them to exchange data over a prolonged period of time. 

Similar to the dialog of two people talking on the phone. **Session Layer 5** allows devices to set up, manage, and end sessions.
### Presentation Layer 6

> A more limited, but specific function is the **Presentation Layer 6**, which handles the presentation of data when sent from one system, but needs to be viewed differently by other systems.

Additional functions from the presentation layer include:
- Translations for connecting different types of computers together. Microsoft Windows, macOS, and Linux server and mainframes can all exist on the same network.
- Compression and decompression to improve throughput of data.
- Encryption ensures data security as it travels down the protocol stack.
### Application Layer 7

> At the very top of the OSI Reference Model is the ***Application Layer 7***, which provides application services for users to access. 

For instance, when using the Internet, it's not the web browser that will sit on the application layer, but rather the *protocol to communicate with the application*.

Below are some familiar protocols that are in use with this layer:
- ***File Transfer Protocol***: allows for computer files to be transferred on a network.
- ***Hypertext Transfer Protocol - HTTP***: used to exchange or transfer structured network text.
- ***Domain Name System - DNS***: provides a naming system on a network for computers, services, and other resources that is decentralized and hierarchical in nature. 
# Infrastructure

### Client

> Where does network communication begin? Normally from a ***Client***. 

This can simply be a computer configured with a Network Interface Card - NIC, and software that initiates a networked endpoint for content or services. Workstations and laptops do not necessarily need large hard drives, since files can be stored on a file server. 

Laptops and mobile device can also act as user clients on the go, with their wireless adapters that provide network connection without the cabling.

### Server

> A computer system that shares network resources or services with a client is called a ***Server***. Servers contain more processing power, memory and hard drive space to run the network operating system, manage network data, users, security and applications. 

Also keep in mind that some servers are no longer on prem, but are located in the cloud which can impact access and bandwidth. 

The following is a list of the different types of servers for handling specific duties:
- ***Web Server*** uses HTTP or HTTPS to serve the files that form webpages.
- ***Domain Name Server*** stores a directory of domain names, translating them to IP addresses
- ***File Server*** allows access to stored files
- ***FTP Server*** or SFTP transfers computer files between client and server
- ***Mail Server*** sends and receives emails
- ***Database Server*** provides access and retrieval services for data storage
### Client-Server

> The basic network operations of sending bidirectional data messages between devices is considered a ***Client-Server*** relationship. 

- For example, when checking your bank account from a computer, the client program forwards a request to the bank server. 
- Once your account information has been retrieved from the database, it is returned to the client, your personal computer. 
### Network Switch

> A network switch and router look similar and perform some similar functions, but each has its own distinct function to perform on a network.

Enabling networked devices to transfer data within a subnet, a ***Switch*** serves as a controller. Through information sharing and resource allocation as a Layer 2 function, switches allow several users to send information simultaneously with minimal delay. 

There are two types of switches: ***Managed and Unmanaged***
- A managed network switch is configurable, offering greater flexibility and features
- An unmanaged switch is designed to work right out of the box with no configuration
### Router

> While a switch connects devices on a network, a ***Router*** is the bridge that connects remote networks or different subnets. By linking the communication between subnets and across different networks as a Layer 3 function, routers are able to determine the next network hop in which a packet is forwarded to its destination.

Routers maintain *routing tables*, along with their status to determine the best route for a given packet. Data can travel through many network points with routers and Layer 3 switches before arriving at its destination.
### Wired Connection

> Physically connecting all of the various network components together to move information from one device to another is created within a **Wired Network**. 

Cabling infrastructures provide the fastest, most secure and reliable access to data services and communication systems, along with POE. 

In addition, wired connections can recognize the network and synchronize much easier and faster than scanning for available wireless networks. Wired environments are also able to extend cables (fiber and copper) over longer distances in comparison to wireless signals with minimal loss in bandwidth or throughput.
### Twisted Pair Cabling

> In a network installation project, cable selection is one of the most important factors affecting signal quality. Most wired networks use ***Twisted Pair Category*** cable, made of two wires conductors for a single circuit to transfer data between devices.

- The pair wires are twisted together for the purposes of cancelling out ***Electromagnetic Interference - EMI*** from external sources. 
- Most wired communications are carried over *Category 5e, 6 or 6a* cable with an RJ45 modular plug crimped on each end. 

#### Wiring Pinouts

> Twisted pair category cables consist of two wiring standards that define the pinout terminations. There is no performance advantage, only the difference between the pinout order of the orange and green pairs. 

- T568A
- T568B

When both ends of the cable are terminated using the same standard, the cable is called a *straight-through cable*. 

- For example. T568A and T568B cables send signals "straight through" for connecting devices of different types, such as a computer to a network switch.
- If one side of the cable is T568A and the other is T568B, this is a *crossover cable* and is most often used to connect two devices of the same type, such as two computers. 

Most computer network ports support Auto MDI-X to autodetect the correct wiring.

Also note that the difference between CAT5 and CAT6 RJ45 connectors. CAT5 has a straight pinout, while CAT6 is staggered hi-lo due to the insulation and thicket copper wire. This is how some manufacturers can get the frequency rating needed to move data. 
#### Cable Shielding

> What about protecting the network signals and cabling from other electrical sources? Twisted pair cable is available in ***Shielded or Unshielded***, where the quality of a cable can make a difference in preventing external signal interference. 

The following are various shield types for category cable:
- **Unshielded Twisted Pair - UTP** - no overall shield, no wire pair shield
- **Foil/Unshielded Twisted Pair - F/UTP** - overall foil, unshielded wire pairs
- **Unshielded/Foil Twisted Pair - U/FTP** - no overall shield, foil wire pairs
- **Foil/Foil Twisted Pair - F/FTP** - overall foil, foil wire pairs
- **Braid & Foil/Unshielded Twisted Pair - SF/UTP** - overall braid and foil, unshielded wire pairs
- **Braid/Foil Twisted Pair - S/FTP** - overall braid, shielded wire pairs
### Fiber Optic Cabling

> Immune to interference and less susceptible to signal degradation over long distances, **Fiber Optic** cables can offer several advantages over traditional copper wired networks. 

The optical fibers of either glass or plastic are able to carry much larger amounts of network data as pulses of light. 

There are two types of transfer methods for fiber:

- ***Singlemode***: high speed light path retains signal fidelity over longer distances at a higher bandwidth compared to multimode.
- ***Multimode***: internal light reflections are dispersed at low speeds over short runs.
### Wireless Networks

> Providing freedom of movement, elimination of unsightly wires, and the ability to extend applications to different locations, the most convenient type of connectivity is through ***Wireless Networks***. 

- The network connects through radio signal transceivers or Access Points - AP that send and receive data for communication between devices.

The use of wireless technology does inject additional security concerns in an application. The network is also susceptible to radio interference, weather, other wireless devices, or a poor connection due to physical obstructions like walls. 

The [Extron WAP 100AC](https://www.extron.com/product/wap100ac) is a ceiling mounted wireless access point engineered for network traffic. It supports dual-band frequency operation, four internal high-gain antennas to maximize network performance and expand device connectivity. 
### Data Rates

> The speed at which data can be transmitted from one device to another is the **Data Rate**, often measured in Megabits or Gigabits per second, and abbreviated as Mbps and Gbps, respectively. 

- Another term for data rate is *throughput*.

A combination of physical and data link layer technology, **Ethernet** is a system that designates how devices connect, communicate and transmit data over a network. The following are the data transfer speeds for the various Ethernet classifications:

- **Ethernet**: 10Base-T - 10 Mbps
- **Fast Ethernet**: 100Base-T - 100Mbps
- **Gigabit Ethernet**: 1000Base-T - 1Gbps (1,000 Mbps)
- **10G Ethernet**: 10GBase-T - 10Gbps (10,000 Mbps)

Be aware there are discrepancies between maximum and actual Ethernet speed ratings. The actual speed performance of a network depends on many factors, including hardware, traffic and interference. 

It is possible to achieve close to maximum data rates, however the application and communication rates must be right.
### Physical and Logical (Topology)

> The design of a network may take many shapes in organizing devices and allocating various tasks. 

The network topology refers to how devices are connected, along with the configuration of cables, computers and other peripherals. 

Topologies are separated into physical and logical entities:

- ***Physical Topology***
	- Defines the location of devices, or their arrangement on a map
	- How the devices are physically wired together, and where

- ***Logical Topology***:
	- Identifies the means by which data is transmitted for device communication
	- The VLAN that the ports are connected to

#### Bus

> The first type of network topology that we'll discuss is the ***Bus*** topology. In this structure, devices are connected to a common medium used for communication.

Each system is daisy-chained (connected one right after the other) where device information travels along the *backbone* until it reaches its destination.

This type of topology is easy to configure and suitable for small LAN networks where the devices are connected as terminating endpoints. This can also be identified as a ***Linear Bus*** (two endpoints) or ***Distributed Bus*** (two or more endpoints) topology.
#### Star

> The ***Star*** topology utilizes a central node that connects every device on the network, acting as a *multiport repeater* in a LAN. It receives signals from the source device, then retransmits it to the destination.

If additional devices are connected to the main node by one or more repeaters, it is identified as an ***Extended star topology***. A Distributed star topology represents a linear arrangement of network devices (daisy chained).

What is a **Node**?

- Any device connected to a network. For example, computers, printers, and Extron ethernet-enabled devices, such as Extron Pro Series control processor are considered nodes. %%

#### Tree

> ***Tree*** topology systems, also known as hybrid star bus topology, joins multiple star topologies into a bus. Workstations are connected directly to a tree bus, that act as the root for a tree of devices. 

This environment used in WAN systems support *network scalability* more so that just a bus or star topology.

#### Mesh

> A ***Mesh*** topology is a type of point-to-point system where each device is connected directly to all other network devices. This provides fault tolerance in the event of failure so that the network is still reachable and devices can communicate. 

Given the backup capabilities, mesh networks used in LAN, WLAN and VLAN systems are *expensive and difficult to scale.*
#### Peer-to-Peer (P2P)

> ***Peer-to-Peer (P2P)*** or point to point systems are connected to each other and can share and allocate tasks without the need of a central server. Every node contains software to administer resources to provide and request services. 

- These systems are easy to setup and mostly used for file sharing, but the security is somewhat weak. 
### Standards Organizations

> In order for various network devices to establish connection and communicate, a set of rules are put forth so that all systems know what to expect. These policies for a common language are defined in a communication protocol, a system of rules that identify the syntax, semantics, and synchronization of communication.

These network protocol standards exist to address the needs for interoperability between devices and networks. The specifications define how systems should be designed, how to perform, how they access and transmit data, their speeds, as well as cabling infrastructures. 

Several standards organizations address these technologies used in the IT and Networking industry for devices and applications. Generally, these are non-profit organizations that specifically take a neutral stance regarding the technologies and work for the betterment of the industry.

#### ISO - International Organization for Standardization

> Promotes worldwide standards for manufactured products and technology. ISO aids in the development of products and services that are safe and reliable, and is best known for devising the OSI Reference Model.

#### ANSI - American National Standards Institute

> The main organization responsible for coordinating and publishing computer and information technology standards in the United States.

#### IEEE - Institute of Electrical and Electronics Engineers

> International society composed of engineering professionals that promote the development and education of electronics, computers and networking. The IEEE 802 branch develops networking practices such as Ethernet, while the 802.11 standard supports Wi-Fi technology.

#### ITIC - Information Technology Industry Council

> Comprised of several dozen companies in the IT industry that develops and processes standards for many computer-related topics.

#### INCITS - International Committee for Information Technology Standards

> Committee established by ITIC to develop and maintain standards related to the IT world. 

#### TIA - Telecommunications Industry Association

> Communications sector of the EIA, and is responsible for developing communications standards. 

# Security, Design and Deployment

## Layers of Defense

> Proper network security incorporates a series of policies, practices and methods that safeguard usability, data, software and hardware. 

Security measures including managing privileges and access, are implemented to prevent a variety of threats before they can enter and spread throughout a network. 

Network security includes multiple layers of defenses at the edge and within the network to prove one's identity, where each layer implements the following general policies for authentication:

- ***Single-Factor***: Something a user knows, like a password to verify the username.
- ***Two-Factor***: Uses single factor in addition to something a user owns; a security token, dongle, or CAC (Common Access Card)
- ***Three-Factor***: Uses single and two factor, in addition to a fingerprint or retinal scan.
### Types of Network Attacks

> Networks and data are vulnerable to many types of attacks if a security plan is not in place. 

A ***Passive*** (Recon) threat attempts to learn or make use of information when a system is monitored or scanned for open ports and vulnerabilities. 

- The purpose is solely to gain information about the target with no data exchange.

An attempt to damage or destroy system resources and affect operation are ***Active*** threats. Below are several examples of the different types of attacks that can occur to network data and devices:

- *Eavesdropping*: Gaining access to data paths in the network to "listen in" or read traffic, often referred to as sniffing or snooping. 
- *Wiretapping*: Monitoring of network server lines and intruding by listening to conversations or recording in an illegal way. 
- *Port Scanning*: Sends several requests to a range of ports on a targeted host in order to find out what ports are active an open.
- *Idle Scan*: Sends spoofed packets (impersonating a computer) to another computer to find out what services are available.
- *Virus*: A program activated by attaching copies of itself to executable objects, files or programs.
- *Malware*: Malicious programs and techniques that pose a threat to your system as worms, trojans, adware, spyware etc.
- *Denial of Service*: Prevents normal access to a website, server or network for its intended users.
- *Man in the Middle*: When someone between you and the person with whom you are communicating is actively monitoring, capturing and controlling your communication transparently. 
- *DNS Spoofing*: Tricking the DNS server to redirect traffic from one website to another by forging DNS entries.
- *VLAN Hopping*: An attacking host on a VLAN to gain access to traffic on other VLANs that would not normally be accessible.
- *Phishing*: Posing as a legitimate institution to lure individuals into providing sensitive data, personal information, banking or credit card details, and passwords.
### Types of Security

> With all the ways a network can be attacked, how can it be kept safe and secure? 

#### Network Access Control

***Network Access Control (NAC)*** provides an authentication and authorization mechanism utilizing IEEE 801.1x and LDAP. These protocols allow authorized devices to access network resources when connected to a network. The NAC may employ switches, routers and additional software or hardware, client and server to ensure the network is secure before allowing communication between devices.

Additional security measures that constrict access include Antivirus and Malware Protection, Application security, Behavioral Analytics, Data Loss prevention and Email security.

***Firewalls*** are software and hardware functions that allow only specific access to a local or remote network. Normally installed at the LAN entrance when connecting networks together, rules are set up to filter and control traffic between the network.

- "Trusted" and "Untrusted" zones allow or deny access which are enforced from the access policies, defining what services the user is allowed to access.

> Mobile devices create additional vulnerability points to a network. To protect a network against attacks from mobile devices, ***Mobile Device Security*** strategy must be implemented.

Inside the network, the plan of action may include network segmentation into guest networks, Security Information and Event Management - SIEM.

Outside the Virtual Private Network - VPN, Wireless Security and Transmission Protocols are required for encrypting the traffic back to the office. 
## Designing a Network

> When designing a network, small or large, it's important to weigh the needs and desires of those who will be using it and the intended purpose. 

The following steps should be considered throughout the design process:

- ***Needs Analysis*** to define the purpose of the network, target customer and readiness dates.
- ***Physical and Logical Design*** to determine the topology, switch backplane, device location and cabling.
- ***Security Implementation*** that includes risk analysis, mitigation plans, confidentiality, integrity, availability, system backup and restore measures.
- ***Quality*** identifying fault tolerance, Quality of Service and differentiated services categories.
- ***Maintenance*** dependent on availability of spare equipment, redundancy, switch-fill capacities, and expansion. Also keeping the switch and firewall software up to date. 
- ***Implementation*** of timelines, schedules, training and documentation.
- ***Expansion*** planning of infrastructure, ports, etc.

### Network Deployment

> Several processes are involved when deploying a network, which encompasses getting new software or hardware up and running properly in the environment. 

Data encoding and transport methods should be established for video, audio and control data, along with sufficient bandwidth requirements. 

The use of these protocols should be supported as well: 

- ***Unicast*** for one-to-one transmission from one point in the network to another. 
- ***Multicast*** supporting one-to-many or many-to-many distribution
- ***Internet Group Message Protocol (IGMP)*** establishes multicast group memberships
- ***Internet Control Message Protocol (ICMP*** allows network devices, such as routers to send error messages indicating that a requested service is not available, or route can not be reached. For example, a Ping command will query a computer or network to determine if there is a connection.

> Additionally, these capabilities should also be considered for network deployment. 

- Static or dynamic IP addressing
- Quality of Service (QoS) - minimizes the impact caused when connections are under heavy traffic.
- Virtual Local Area Networks - VLANS provide flexibility, security and broadcast domains.
- Internet Group Management Protocol - IGMP provides snooping to monitor IGMP traffic. 
- IPCONFIG displays the IP address, subnet mask, and default gateway on the PC.
- PING for querying network devices to verify connection
- Trace Route - TRACERT to show destination path for packets
- Address Resolution Protocol - ARP maps the network IP addresses to the hardware's MAC address
- Internet Control Message Protocol - ICMP notifies of unavailable hosts, services or routes.
- Simple Network Management Protocol - SNMP traps sent status updates of network devices to a monitoring server


