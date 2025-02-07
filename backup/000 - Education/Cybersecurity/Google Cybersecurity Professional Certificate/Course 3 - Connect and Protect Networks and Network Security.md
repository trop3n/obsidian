Course 3: Connect and Protect: Networks and Network Security

“It’s important to secure networks because network based attacks are growing in both frequency and complexity.”

What we’ll learn:

- Structure of a network
    
- Network operations
    
- Network attacks
    
- Security hardening for networks
    

Course Overview:

- Module 1: Network architecture
    
- Module 2: Network operations
    
- Module 3: Secure against network intrusions
    
- Module 4: Security hardening
    

Module 1: Introduction to Networks

> What you’ll learn:

- Structure of a network
    
- Standard networking tools
    
- Cloud networks
    
- TCP/IP model
    

What are networks?

> A group of connected computers is called a network. 

> Local area network (LAN) - small area like a home or office

> Wide area network (WAN) - wide area like the internet or cross country 

Network tools

- Hub
    

- A hub is a network device that broadcasts information to every device on the network
    
- Like a radio tower that broadcasts a signal to any radio tuned to correct frequency
    

- Switch
    

- A switch makes connections between specific devices on a network by sending and receiving data between them. 
    
- It only passes data to the intended destination, which makes switches more secure than hubs and enables them to control the flow of traffic and improve network performance. 
    

- Router
    

- Connects multiple networks together
    

- Information travels from computer to router
    
- Then, the router reads the destination address
    
- Forwards the data to the intended network’s router
    
- Finally, the receiving router directs that information to the tablet
    

- Modems
    

- Device that connects your router to the internet, and brings access to the LAN
    

> These are all physical devices, however many functions performed by these physical devices can be completed by virtualization tools

- These are pieces of software that perform network operations. Virtualization tools carry out operations that would normally be completed by a hub, switch, router or modem.
    
- Offered by cloud service providers
    
- Cost savings and scalability
    

Network Devices

> Maintain information and services for users of a network

- After connection via wired or wireless connections, the devices send packets
    
- Packets provide information about the source and destination of the data
    
- Network devices are specialized vehicles like routers and switches that manage what is being sent and received over the network
    

Devices and Desktop Computers

> Each device and desktop has a unique MAC address and IP addresses which identify it on the network

- Also have a network interface that sends and receives data packets
    
- Connect via hard wire (ethernet) or wireless connections
    

Firewalls

> Network security device that monitors traffic to or from your network.

- First line of defense
    
- Restrict incoming traffic and outgoing traffic according to preset rules
    
- Lie between the untrusted outside network and the internal trusted network
    

Servers

> Provide information and services for devices like computers, smart home devices and smartphones on the network

- Devices that connect to a server are called clients
    
- Common examples are DNS servers that provide domain name lookups for internet sites, files servers that store and retrieve files from a database, and corporate mail servers that organize mail for a company
    

Hubs and Switches

> Direct traffic flow on a local network

- Hub is a device that provides a common point of connection for all devices directly connected to it.
    
- Additionally, hubs repeat all information out to all ports.
    
- This makes the hub vulnerable to eavesdropping, making them used less on modern networks
    

> Switches are the preferred choice for most networks.

- Forwards packets between devices directly connected to it. 
    
- Analyze destination address of each data packet and send it to the intended device.
    
- Maintain MAC address table that matches MAC addresses of devices on the network to port numbers on the switch and forwards incoming data packets according the the destination MAC address
    
- Part of the data link layer of the OSI & TCP/IP model
    
- Improve performance and security
    

Routers

> Connect and direct network traffic based on the IP address of the destination network

- Allows devices on different networks to communicate with each other. In the TCP/IP model, routers are part of the network layer. 
    
- IP address of the destination network is contained in the IP header
    
- Router reads the IP header information and forwards the packet to the next router on the path to the destination.
    
- Continues until the packet reaches the destination network, routers often include a firewall feature that allows or blocks incoming traffic based on information in the transmission
    

Modems and Wireless Access Points

> Usually connect your home or office with an internet service provider (ISP). 

- ISPs provide internet connectivity via telephone line or coaxial cables, or fiber connections.
    
- Receive transmissions or digital signals front he internet and translate them into analog signals that can travel through the physical connection provided by the ISP.
    
- Usually, modems connect to a router that takes the decoded transmissions and sends them on to the local network
    

Note: Enterprise networks used by large organizations to connect their users and devices often use other broadband technologies to handle high volume traffic, instead of a modem.

Wireless Access Point

> Sends and receives digital signals over radio waves creating a wireless network.

- Devices with wireless adapters connect to the access point using Wi-Fi
    
- Wi-Fi refers to set of standards that are used by network devices to communicate wirelessly
    
- Wireless access points and the devices connected to them use Wi-Fi protocols to send data through radio waves where they are sent to routers and switches and directed along the path to their final destination
    

Using Network Diagrams as a Security Analyst

> Network diagrams allow network admins and security personnel to imagine the architecture and design of their organization’s private network

- Network diagrams are maps that show the devices on the network and how they connect.
    
- Use small representative graphics to portray each network device and dotted lines show how each device connects to the other.
    
- Diagrams are used by security analysts to develop and refine strategies for securing network architectures.
    

Cloud Networks

Cloud Computing - The practice of using remote servers, applications and network services that are hosted on the internet instead of on local physical devices

> Cloud providers offer an alternative to on premises networks

Cloud Network - collection of servers or computers that stores resources and data in remote data centers that can be accessed via the internet

- Traditional networks host web servers from a business in it’s physical location.
    
- However, cloud networks are different from traditional networks because they use remote servers, which allow online services and web applications to be used from any geographic location
    

> Cloud security will become increasingly relevant to many security professionals as more organizations migrate to cloud services

- Cloud service providers offer cloud computing to maintain applications.
    

- They provide on-demand storage and processing power that customers only pay as needed.
    
- Provide business and web analytics that organizations can use to monitor web traffic and sales
    

- With the transition to cloud networking, often there is an overlap of identity-based security on top of the more traditional network-based solutions. 
    

- Verify where the traffic is coming from and the identity that is coming with it.
    

> Cloud security will be a growing trend for security analysts as more organizations migrate to the cloud.

Cloud Computing and Software Defined Networks

> Why cloud computing is beneficial for large organizations

> How hybrid networks operate

> Software-defined networks

  
  

Computing Processes in the Cloud

- Traditional networks are called on-premise networks, meaning that all of the devices used for network operations are kept at a physical location owned by the company, like in an office building, for example.
    
- Cloud computing refers to the practice of using remote servers, applications and network services that are hosted on the internet instead of at a physical location owned by the company
    
- A cloud service provider (CSP) is a company that offers cloud computing services
    

- Large data centers around the globe that house millions of servers. 
    
- Data centers provides
    

> CSPs provide three main categories of service:

- Software as a Service (SaaS) refers to software suites operated by the CSP that a company can use remotely without hosting the software
    
- Infrastructure as a Service (IaaS) refers to the use of virtual computer components offered by the CSP. These include virtual containers and storage that are configured remotely through the CSP’s API or web console. 
    

- Cloud-compute and storage services can be used to operate existing applications and other technology workloads without significant modifications
    
- Existing applications can be modified to take advantage of the availability, performance and security features that are unique to cloud provider services
    

- Platform as a Service (PaaS) refers to tools that application developers can use to design custom applications for their company. Custom applications are designed and accessed in the cloud and used for a company’s specific business needs.
    

Hybrid Cloud Environments

- When an organization uses on premise computers and networks are used in addition to a CSP’s services. 
    
- If more than one CSP is used, it’s referred to as a multi-cloud environment.
    
- The vast majority of organizations used hybrid cloud environments to reduce costs and maintain control over network resources.
    

Software-defined Networks

- CSPs offer networking tools similar to the physical devices that you have learned about in this section of the course. 
    
- Software-defined networks (SDNs) are made up of virtual network devices and services. 
    

- Just like CSPs provide virtual computers, many SDNs also provide virtual switches, routers and firewalls, and more. 
    

- Most modern network hardware devices also support network virtualization and software-defined networking
    

- This means physical switches and routers use software to perform packet routing. In the case of cloud networking, the SDN tools are hosted on servers located at the CSP’s data center.
    

Benefits of Cloud Computing and Software-defined Networks

> Three of the main reasons that cloud computing is so attractive to businesses are reliability, decreased cost and increased scalability

- Reliability
    

- Reliability in cloud computing is based on how available cloud services and resources are, how secure connections are, and how often the services are effectively running. 
    
- Customers and employees can access the resources they need with minimal interruption
    

- Cost
    

- Traditionally, companies have had to provide their own network infrastructure, at least for internet connections.
    

- This mean there were significant upfront costs for companies
    

- CSPs have large data centers that are able to offer virtual devices and services at a fraction of the cost required for companies to install, patch, upgrade and manage components and software themselves
    

- Scalability
    

- When organizations try to increase their business needs, they might be forced to buy more equipment and software to keep up.
    
- CSPs reduce the risk of overscaling or underscaling by making it easy to consume services in an elastic utility model as needed.
    

- Pay for what you need, when you need it.
    

- Changes can be made through the CSPs, APIs, or web console, much more quickly than if network techs had to purchase their own hardware and set it up.
    

  
  
  
  

Introduction to Network Communication

> Communication makes network attacks more likely because it gives a malicious actor an opportunity to take advantage of vulnerable devices and unprotected networks.

> Communication over a network happens when data is transferred from one point to another. 

- Pieces of data are typically referred to as data packets
    

- Data packet is a basic unit of information that travels from one device to another within a network
    
- When data is sent across a network, it is sent as a packet that contains information about where the packet is going, where it’s coming from, and the content of the message
    

- Think of data packets like a piece of physical mail. 
    

- Imagine sending a letter to a friend
    

- The envelope will need to have the address where you want the letter to go and your return address.
    

- Data packets contain headers that include internet protocol address (IP address), and the Media Access Control (MAC) address of the destination device
    
- It also includes a protocol number that tells the receiving device what to do with the information in the packet
    
- The body of the packet contains the message that needs to be transmitted to the receiving device
    
- At the end of the packet, there’s a footer, similar to a signature on a letter, that signals to the receiving device that the packet is finished.
    

> The movement of data packets across a network can provide an indiciation of how well the network is performing.

- Network performance is measured by bandwidth
    

- Bandwidth  refers to the amount of data a device receives every second
    
- Calculated by dividing the quantity of data by the time in seconds
    

- Speed refers to the rate at which data packets are received or downloaded
    

> Security analysts are interested in network bandwidth and speed because if either are irregular, it could be an indication of an attack

- Packet sniffing is the practice of capturing and inspecting data packets across the network
    

The TCP/IP Model

> Transmission Control Protocol and Internet Protocol

- Standard model used for network communication
    

> Transmission Control Protocol

- An internet communication protocol that allows two devices to form a connection and stream data
    
- Set of instructions on how to organize data being sent
    
- Also establishes a connection between two devices and makes sure that packets reach their appropriate destination
    

> Internet Protocol

- Set of standards for routing and addressing data packets as they travel between devices on a network
    
- Included is the IP address that functions as an address for each private network
    

> Ports

- When data packets are sent across a network, the are assigned to a port
    
- A Port is a software-based location that organizes the sending and receiving of data between devices on a network
    
- Ports divide traffic into segments based on the service they will perform between two devices
    
- Computers sending and receiving these data segments know how to prioritize and process these segments based on their port number
    

> Data Packets include instructions that tell the receiving device what to do with the information

- These instructions come in the form of a port number
    
- Port numbers allow computers to split the network traffic and prioritize the operations they will perform with the data
    

- Common port numbers are: port 25, used for email
    
- Port 443, used for secure internet communication
    
- Port 20, for large file transfers
    

  
  

Four Layers of the TCP/IP Model

> Framework used to visualize how data is organized and transmitted across a network

- TCP model has four layers:
    

1. Network access layer
    
2. Internet layer
    
3. Transport layer
    
4. Application layer
    

> Knowing how the TCP/IP model organizes data allows security professionals to monitor and secure against risks

1. Network Access Layer
    

1. Deals with the creation of data packets and their transmission across a network
    
2. Hardware devices connected to physical cables and switches that direct data to its destination
    

3. Internet Layer
    

1. Where IP addresses are attached to data packets to indicate the location of the sender and receiver 
    
2. Also focuses on how networks connect to each other
    

1. Data packets containing information that determine whether they will stay on the LAN or will be sent to remote network
    

5. Transport Layer
    

1. Included protocols to control the flow of traffic across a network.
    
2. Protocols permit or deny communication with other devices and include information about the status of the connection
    
3. Activities of this layer include:
    

1. Error control, ensuring data is flowing smoothly
    

7. Application Layer
    

1. Protocols determine how the packets will interact with receiving devices
    
2. Functions organized at application layer include file transfers and emails services
    

Learn More About the TCP/IP Model

> As a security professional, it’s important that you understand the TCP/IP model because it describes the functions of various network protocols.

> The TCP/IP model is based on the TCP/IP protocols suite that includes all network protocols that support the main TCP/IP protocol. 

The TCP/IP Model

- Framework used to visualize how data is organized and transmitted across a network
    
- This model helps network engineers and network security analysts conceptualize processes on the network and communicate where disruptions or security threats occur
    

Four Layers of TCP/IP Model

1. Network Access Layer
    

1. Ethernet
    
2. Wireless LAN
    

3. Internet Layer
    

1. IPv4
    
2. IPv6
    

5. Transport Layer
    

1. TCP 
    
2. UDP
    

7. Application Layer
    

1. HTTP
    
2. TLS
    
3. DNS
    

Network Access Layer

> Sometimes called the data link layer, deals with creation of data packets and their transmission across the network

- Corresponds to the physical hardware involved in network transmission
    
- Hubs, modems, cables and wiring are considered part of this layer
    
- Address Resolution Protocol (ARP) is part of the network access layer
    

Internet Layer

- Sometimes referred to as the network layer, responsible for ensuring the delivery to the destination host, which potentially resides on a different network
    
- Ensures IP addresses are attached to data packets to indicate the location of the sender and receiver
    
- Internet layer also determines which protocol is responsible for delivering the data packets and ensures the delivery to the destination host
    

> Common protocols that operate at the internet layer:

- Internet Protocol:
    

- IP sends the data packets to the correct destination and relies on the TCP/IP protocol to deliver them to the corresponding service.
    
- IP packets allow communication between two networks, they are routed from the sending network to the receiving network.
    
- TCP in particular retransmits any data that is lost or corrupt
    

- Internet Control Message Protocol (ICMP)
    

- The ICMP shares error information and status updates of data packets
    
- Useful for detecting and troubleshooting network errors
    
- ICMP reports information about packets that were dropped or that disappeared in transit, issues with network connectivity and packets redirected to other routers
    

Transport Layer

> Responsible for delivering data between two systems or networks and included protocols to control the flow of traffic across a network

- Transmission Control Protocol
    

- An internet communication protocol that allows two devices to form a connection and stream data.
    
- Ensures that data is reliably transmitted to the destination service.
    
- Contains the port number of the intended destination service
    

- User Datagram Protocol
    

- Connectionless protocol that does not establish a connection between devices before transmissions
    
- Used by applications that are not concerned with the reliability of the transmission.
    
- Data sent over UDP is not tracked as extensively as data sent using TCP
    
- Mostly used for performance sensitive applications that operate in real time, like gaming or video streaming.
    

Application Layer

> Similar to the application, presentation and session layers of the OSI model. 

- The application layer is responsible for making network requests or responding to requests
    
- Defines which internet services and applications any user can access.
    
- Protocols in the application layer determine how the data packets will interact with receiving devices. 
    
- Relies on underlying layers to transfer data across the network
    

> Common protocols used in Application Layer:

- Hypertext Transfer Protocol (HTTP)
    
- Simple Mail Transfer Protocol (SMTP)
    
- Secure Shell (SSH)
    
- File Transfer Protocol (FTP)
    
- Domain Name Service (DNS)
    

TCP/IP vs OSI Model

- OSI visually organizes network protocols into different layers
    
- Network professionals often use this model to communicate with each other about potential sources of problems or security threats when they occur
    
- TCP/IP combines layers of the OSI model.
    

- Many similarities between the two models, both define standards for networking and divide the network communication process into different layers
    
- Simplified version of OSI Model
    

OSI Model

> Standardized concept that describes the seven layers computers use to communicate and send data over the network. Security professionals often use this model to communicate with each other about potential sources of problems or security threats when they occur.

- Some organizations heavily rely on the TCP/IP model, others use the OSI model.
    
- Important to be familiar with both models
    

Layer 7: Application Layer

> User connection to the internet via applications and requests

- Includes processes that directly involve the everyday user.
    
- Includes all network protocols that software applications use to connect a user to the internet.
    
- This characteristic is the identifying feature of the application layer
    

Layer 6: Presentation Layer

> Functions at the presentation layer involve data translation and encryption for the network.

- Adds and replaces data with formats that can be understood by applications on both sending and receiving systems
    
- Processes at the presentation layer require the use of a standardized format
    
- Some formatting functions that occur at layer 6 include:
    

- Encryption
    
- Compression
    
- Confirmation that the character code can be interpreted on receiving system
    

- Secure Shell (SSH)
    

Layer 5: Session Layer

> Describes when a connection is established between two devices. An open session allows the devices to communicate with each other.

- Keep session open while communication is active, and close it when it ends
    
- Responsible for activities such as:
    

- Authentication
    
- Reconnection
    
- Setting Checkpoints
    

- Checkpoints ensure that the transmission picks up at the last sessions checkpoint when the connection resumes.
    
- Sessions include a request and response between applications
    

- Respond to requests for service from processes in the presentation layer and send requests for services to the transport layer
    

Layer 4: Transport Layer

> Responsible for delivering data between devices.

- Handles the speed of data transfer, flow of the transfer, and breaking data down into smaller segments to make them easier to transport.
    
- Segmentation is the process of dividing up larger data transmissions into smaller pieces that can be processed by the receiving system
    
- TCP and UDP are transport layer protocols
    

Layer 3: Network Layer

> Oversees receiving the frames from the data link layer (layer 2) and delivers them to the intended destination.

- Destinations are found based on the address that resides in the frame of the data packets. 
    
- Data packets allow communication between two networks, and include IP addresses that tell routers where to send them
    

Layer 2: Data Link

> Organizes sending and receiving data packets within a single network. 

- The data link layer is home to switches on the local network and network interface cards on local devices
    
- Protocols like the Network Control Protocol (NCP), High Level Data Link Control (HDLC) and Synchronous Data Link Control Protocol (SDLC) are used in the data link layer
    

Layer 1: Physical Layer

> Corresponds to the physical hardware involved in a network transmission.

- Hubs, modems, and the cables and wiring that connect them are all considered part of the physical layer
    
- Data packets need to be converted into a stream on 0’s and 1’s.
    

- This stream is send across the physical wiring then passed onto higher levels of the OSI Model
    

IP Addresses and Network Communication

- IP stands for Internet Protocol
    

- Unique string of characters that identifies a location of a device on the internet
    
- Each device has a unique IP address, just like a house has a unique mailing address
    
- Two types of Internet Protocol:
    

- IPv4
    
- IPv6
    

- IPv4 addresses are written as four, 1, 2, or 3 digit numbers separated by a decimal point
    

- As the use of the internet grew, IPv4 didn’t contain enough addresses, so IPv6 was created
    

- IPv6:
    

- Made up of 32 characters
    

- Allows for more devices to be connected to the internet
    

- Public vs. Private IP addresses
    

- Internet Service Provider assigns a public IP address that is connected to your geographic location.
    
- Private IP addresses are only seen by other devices on the same local network.
    

- This means that all the devices on your home network can communicate with each other using unique IP addresses that the rest of the internet can’t see
    

- MAC Addresses
    

- Unique alphanumeric identifier that is assigned to each physical device on a network
    
- When a switch receives packet data, it reads the MAC address of the destination device and maps it to a port
    

Components of Network Layer Communication

> Operations at level 3 of the OSI layer: network layer

Operations at the Network Layer

- Organize the addressing and delivery of data packets across the network from the host device to the destination device.
    

- This includes directing packets from one router to another router across the internet
    

- All data packets include an IP address A data packet is also referred to as an IP packet for TCP connections or a datagram for UDP connections
    
- Header information communicates more than just the address of the destination
    

- Also includes information such as the source IP address, the size of the packet and which protocol will be used for the data portion of the packet
    

Format of an IPv4 Packet

- An IPv4 header format is determined by the IPv4 protocol and includes the IP routing that devices use to direct the packet. The size of the IPv4 header ranges from 20-60 bytes. 
    

- The first 20 bytes are a fixed set of information containing data such as the source and destination IP address, header length, and total length of the packet
    
- The last set of bytes can range from 0 to 40 and consists of the options field
    

- The length of the data section of an IPv4 packet can vary greatly in size. However, the maximum possible size of an IPv4 packet is 65,535 bytes. 
    

- It contains the message being sent over the internet, like website information or email text.
    

> There are 13 fields within the header of an IPv4 packet:

- Version (VER): this 4 bit component tells receiving devices what protocol the packet is using.
    
- IP Header Length (HLEN or IHL): HLEN is the packet’s header length. This value indicates where the packet header ends and the data segment begins.
    
- Type of Service (ToS): Routers prioritize packets for delivery to maintain quality of service on the network. The ToS field provides the router with this information.
    
- Total Length: This field communicates the total length of the entire IP packet, including the header and data. The maximum size of an IP packet is 65,535 bytes.
    
- Identification: For IPv4 packets that are larger than 65,535 bytes, the packets are divided, or fragmented, into smaller IP packets. The identification field provide a unique identifier for all the fragments of the original IP packet so that they can be reassembled once they reach their destination.
    
- Flags: This field provides the routing device with more information about whether the original packet has been fragmented and if there are more fragments in transit.
    
- Fragmentation Offset: The fragment offset field tells routing devices where in the original packet the fragment belongs
    
- Time to Live (TTL): TTL prevents data packets from being forwarded by routers indefinitely. It contains a counter that is set by the source. The counter is decremented by one as it passes through each router along its path. When the TTL counter reaches zero, the router currently holding the packet will discard the packet and return an ICMP Time Exceeded error to the sender.
    
- Protocol: The protocol field tells the device which protocol will be used for the data portion of the packet.
    
- Header Checksum: Contains a checksum that can be used to detect corruption of the IP header in transit. Corrupted packets are discarded.
    
- Source IP address: The destination IP address is the IPv4 address of the destination device.
    
- Options: Allows for security options to be applied to the packet if the HLEN value is greater than five. 
    

Difference Between IPv4 and IPv6:

> Key differences between IPv4 and IPv6:

- Length and format of the addresses
    

- IPv4 addresses are up to four decimal numbers separated by periods, each number ranging from 0 to 255. 
    
- IPv6 addresses are made up of eight hexadecimal numbers separated by colons, each number consisting of up to four hexadecimal digits.
    

- IPv6 Header format is much simpler than IPv4
    
- IPv6 offers more efficient routing eliminates private IP address collisions that can occur on IPv4 when two devices on the network are attempting to use the same address.
    

Introduction to Network Protocols

> Network Protocols

> Virtual Private Networks

> Firewalls, Security Zones and Proxy Servers

  

Network Protocols

> A set of rules used by two or more devices on a network to describe the order of delivery and the structure of the data

- Transmission Control Protocol (TCP): An internet communications protocol that allows two devices to form a connection and stream data
    

- TCP isn’t limited to just two devices. It established a direct connection between two endpoints, but the underlying network infrastructure can handle routing data across multiple devices. 
    
- Verifies both devices using a handshake before any communication takes place
    

- Address Resolution Protocol (ARP): network protocol used to determine the MAC address of the next router or device on the path
    
- Hypertext Transfer Protocol Secure (HTTPS): Protocol that provides a secure method of communication between clients and website servers
    

- Allows web browser to securely send a request to the web server and receive webpage as response
    

- Domain Name System (DNS): Protocol used to translate internet domain names into IP addresses
    

- Sends the domain name and the web address to a DNS server that retrieves the IP address of the website you are trying to reach. 
    

> Security Protocols:

- HTTPS
    
- SSL/TLS - 
    
- These keep the communication secure and out of the hands of attackers trying to steal information.
    

Common Network Protocols

> Network protocols and how they organize data communication over a network

Overview of Network Protocols

- Network protocols are sets of rules used by two or more devices on a network to describe the order of delivery and the structure of data.
    
- Serve as instructions that come with the information in the data packet.
    
- Protocols are like a common language that allows devices all across the world to communicate with and understand one another.
    

> Security professionals should still understand these essential functions in network communication and their associated security implications.

- Some protocols have vulnerabilities that malicious actors exploit. 
    
- A threat actor could use the DNS protocol to divert traffic from a legitimate website to a malicious website containing malware.
    

Three Categories of Network Protocols

1. Communication protocols
    
2. Management protocols
    
3. Security protocols
    

> Communication Protocols

Govern the exchange of information in network transmission

- Transmission Control Protocol (TCP): allows two devices to form a connection and stream data.
    

- Uses a three-way handshake process:
    

- Sends a synchronize (SYN) request to the server
    
- Server responds with a SYN/ACK packet to acknowledge receipt of the device’s request.
    
- Once the server receives the ACK packet from the device, a TCP connection is established.
    

- User Datagram Protocol (UDP):
    

- Connectionless protocol that does not establish a connection between devices before transmission
    

- This make it less reliable than TCP
    

- Works well for transmissions that need to get to their destination quickly
    

- Sending DNS requests to DNS servers
    

- Hypertext Transfer Protocol Secure (HTTPS): application layer protocol that provides a method of communication between clients and website servers
    

- Uses Port 80
    
- HTTP is considered insecure, so it has been replaced with HTTPS that uses encryption from SSL/TLS for communication
    

- Domain Name System (DNS): protocol that translates domain names into IP addresses.
    

- Query is sent to a dedicated DNS server. 
    

- DNS server looks up the IP address that corresponds to the web domain. 
    

- Normally uses UDP on Port 53. 
    

- If DNS request is too large, it will switch to TCP
    

Management Protocols

> Used for monitoring and managing devices on a network.

- Simple Network Management Protocol (SNMP): protocol used for monitoring and managing devices on a network.
    

- SNMP can reset a password on a network device or change it’s baseline configuration
    
- Can also send requests to network devices for a report on how much of the network’s bandwidth is being used.
    

- Internet Control Message Protocol (ICMP): 
    

- Protocol used by devices to tell each other about data transmission errors across a network. 
    
- Commonly used as a quick way to troubleshoot network connectivity and latency by issuing the “ping” command on a Linux OS.
    

Security Protocols

> Ensure that data is sent and received securely across a network

- Hypertext Transfer Protocol Secure (HTTPS): protocol that provides a secure method of communication between clients and website servers. HTTPS is a secure version of HTTP that uses secure sockets layer/ transport layer security (SSL/TLS) encryption on all transmissions so that malicious actors cannot read the info contained. 
    
- Secure File Transfer Protocol (SFTP): protocol used to transfer files from one device to another over a network.
    

- SFTP uses secure shell (SSH), typically through TCP port 22.
    
- SSH uses Advanced Encryption Standard (AES) and other types of encryption to ensure that unintended recipients cannot intercept the transmissions. 
    
- Occurs at application layer
    
- Often used with cloud storage
    

Note: The encryption protocols mentioned do not conceal the source or destination IP address of network traffic. Malicious actors can still learn basic information about the network traffic if they intercept it.

  
  

Additional Network Protocols

> Additional concepts and protocols that will come up regularly in your work in cybersecurity.

Network Address Translation

- Devices on home or private network each have a private IP address that they use to communicate directly with each other.
    
- In order for the devices with private IP addresses to communicate with the public internet, they need to have a single public IP address that represents all devices on the LAN to the public.
    
- This process is known as Network Address Translation (NAT) and it generally requires a router or firewall to be specifically configured to perform NAT.
    

- NAT is part of Layer 2 (internet) layer
    

Dynamic Host Configuration Protocol (DHCP):

- Management family of network protocols. 
    
- APplication layer protocol used on a network to configure devices.
    
- Works with the router to assign a unique IP address to each device and provide the addresses of the appropriate DNS server and default gateway for each device.
    
- Operates on Port 67.
    

Address Resolution Protocol

- Device IP addresses may change over time, but it’s MAC address is permanent because it is unique to a device’s network interface card.
    
- ARP is used in the network access layer to translate the IP addresses that are found in data packets into the MAC address of the hardware device.
    
- Each device on the network performs ARP and keeps track of matching IP and MAC addresses in an ARP cache.
    

- Does not have a port number, being a layer two protocol.
    

Telnet

- Application layer protocol
    
- Used to connect with a remote system.
    
- Sends all information in clear text
    
- Uses command line prompts to control another device similar to Secure Shell, but Telnet is not as secure as SSH.
    
- Uses TCP Port 23
    

Secure Shell

- Used to create a secure connection with a remote system. This application layer protocol provides an alternative for secure authentication and encrypted communication. 
    
- Operates on TCP Port 22 and is a replacement for less secure protocols
    

Post Office Protocol (POP)

- Application layer protocol used to manage and retrieve email from a mail server.
    
- POP3 is the most commonly used version of POP. 
    
- Unencrypted, plaintext authentication uses TCP/UDP Port 110 and encrypted emails use Secure Sockets Layer/Transport Layer Security (SSL/TLS) over TCP/UDP port 995. 
    

Internet Message Access Protocol (IMAP)

- Used for incoming mail,
    
- Downloads headers of emails and the message content. 
    
- Content also remains on the email server, so it can be read on multiple devices simultaneously.
    
- Uses unencrypted TCP port 143 and TCP port 993 over the TLS protocol.
    

Simple Mail Transfer Protocol (SMTP):

- Used to transmit and route email from the sender to the recipient’s address.
    
- Works with Message Transfer Agency (MTA) software, which searches DNS servers to resolve email addresses to IP addresses, to ensure emails reach intended destinations. 
    
- SMTP uses TCP/UDP Port 25 for unencrypted emails and TCP/UDP port 587 using TLS for encrypted emails.
    
- Port 25 is often used by high volume spam, SMTP helps filter spam by regulating how many emails a source can send at a time.
    

Protocols and Port Numbers

- Firewalls can filter out unwanted traffic based on port numbers
    
- Firewalls may be configured to only allow access to TCP port 995 (POP3) by IP addresses belonging to their organization.
    

  
  
  

|   |   |
|---|---|
|Protocol|Port|
|DHCP|UDP Port 67 (servers)<br><br>UDP Port 68 (clients)|
|ARP|none|
|Telnet|TCP Port 23|
|SSH|TCP Port 22|
|POP3|TCP/UDP port 110 (unencrypted)<br><br>TCP/UDP port 995 (encrypted)|
|IMAP|TCP port 143 (unencrypted)<br><br>TCP port 993 (encrypted, SSL/TLS)|
|SMTP|TCP/UDP port 25 (unencrypted)|
|SMTPS|TCP/UDP port 587 (encrypted, TLS)|

Wireless Protocols 

IEEE 802.11 (WiFi) - set of standards that define communication for wireless LANs

> WiFi protocols have adapted over the years to become more secure, on the same level as wired connections

> WiFi Protected Access (WPA) - A wireless security protocol for devices to connect to the internet

Evolution of Wireless Security Protocols

> Wi-Fi refers to a set of standards that define communication for wireless LANs. Wi-Fi is a marketing term coined by the Wireless Ethernet Compatibility Alliance (WECA)

> Wi-Fi standards and protocols are based on the 802.11 family of internet communication standards determined by the Institute of Electrical and Electronic Engineers (IEEE)

- Wi-Fi may be referred to as IEEE 802.11 
    

> WPA, WPA2, WPA3 and the Wireless Application Protocol used for mobile internet connections

  

Wired Equivalent Privacy

- WEP is a wireless security protocol designed to provide users with the same level of security as a wired connection.
    

- Oldest wireless security standard
    

- Largely out of use today in favor of more recent and more secure protocols.
    

- Devices on a network may be too old for newer formats, so it’s still important to know.
    

- Considered a high-risk security protocol
    

Wi-Fi Protected Access

- Developed in 2003 to improve upon WEP.
    
- Intended to be a transitional measure so backwards compatibility could be established with older hardware
    
- WPA addressed security weaknesses in WEP using a protocol called Temporal Key Integrity Protocol (TKIP)
    

- Uses larger security keys than WEP, making it more difficult to crack the key by trial and error.
    

- Attackers can insert themselves in the authentication handshake process and insert a new encryption key instead of the dynamic one assigned by WPA. 
    

- If set as all zeros, it is as if the transmission is not encrypted at all.
    

WPA2 & WPA3

- Improves on WPA1 by using the Advanced Encryption Standard (AES)
    
- Also uses Counter Mode Cipher Block Chain Message Authentication Code Protocol (CCMP), which provides encapsulation and ensures message authentication and integrity.
    
- Considered the security standard for Wi-Fi today.
    

- Still vulnerable to KRACK attacks, leading to WPA3.
    

> Personal / Enterprise Modes

- Personal is best suited for home networks.
    

- Easy to implement
    
- Passphrase for personal WPA2 needs to be applied for each device connecting to it.
    

- Enterprise works best for business applications.
    

- Initial setup is more complicated, but offers individualized and centralized control over a Wi-Fi access to business network.
    
- Administrators can grant or remove access to a network at any time.
    
- Users never have access to encryption keys
    

> WPA3

- Growing in usage as more WPA3 devices hit the market.
    

Key differences between WPA2 and WPA3:

- WPA3 addresses use the authentication handshake vulnerability to KRACK attacks
    
- WPA3 uses Simultaneous Authentication of Equals (SAE), a password authenticated, cipher-key sharing agreement.
    

- Prevents attackers from downloading data from wireless network connections to their systems to try to decode it.
    

- WPA3 has increased encryption to make passwords more secure by using 128-bit encryption, with WPA3 enterprise mode offering 192-bit encryption
    

Firewalls and Network Security Measures

> A firewall is a network security device that monitors traffic to and from your network.

- Allows or blocks traffic based on a set of configured rules.
    

> Port-filtering 

- Firewall function that blocks or allows certain port numbers to limit unwanted communication
    

- Rule that only allows comms for ports 443, for example
    

Types of Firewalls

> Hardware Firewalls:

- Most basic way to defend against attacks to a network
    

> Software Firewalls:

- Does the same thing as hardware firewalls, only is not tangible
    
- If a software firewall is connected to a server, it will protect all devices connecting to that server
    

  

> Cloud-based Firewalls

- Software firewalls hosted by a cloud service provider
    
- Firewalls can be configured on provider’s interface
    
- Protect any assets on the cloud
    

Stateful vs. Stateless Firewalls

- Stateful - a class of firewall that keeps track of information passing through it and proactively filters out threats.
    
- Stateless - class of firewall that operates based on predefined rules and does not keep track of information from data packets
    

- Doesnt discover suspicious trends
    

Next Generation Firewalls (NGFWs)

- Performs deep packet inspection
    
- Intrusion detection
    
- Threat intelligence updates
    

Virtual Private Networks (VPN)

> A network security service that changes your public IP address and hides your virtual location so that you can keep your data private when you are using a public network like the internet

- Also encrypt data as it traverses the internet
    

Encapsulation: a process performed by a VPN service that protects your data by wrapping sensitive data in other packets

Security Zones

> Segment of a network that protects the internal network from the internet

> Network Segmentation - a security technique that divides the network into segments

- Each network segment has its own security rules and access permissions
    
- Act as barrier to internal networks, maintain privacy within corporate groups, and prevent issues from spreading to the whole network.
    

> Free public Wi-Fi is usually segmented from the larger network used by staff and the rest of the organization.

Uncontrolled Zone - Any network outside the organization’s control

Controlled Zone - A subnet that protects the internal network from outside networks

Areas in the Controlled Zone:

- Demilitarized Zone - public facing resources that can access the internet
    

- Network perimeter
    

- Internal Network - contains private servers and data that needs to be protected
    
- Restricted Zone - protects highly confidential data and servers
    

- Only accessible to people with certain privileges 
    

Subnetting and CIDR

> Overview of subnetting

- Subnetting is a division of a network into logical groups called subnets.
    

- Network inside a network
    

- Form based on the IP addresses and network mask of the devices on the network.
    
- Creates a network of devices to function as their own network
    
- Makes network more efficient and can also be used to create security zones
    

Classless Inter-Domain Routing Notation for Subnetting

> CIDR is a method of assigning subnet masks to IP addresses to create a subnet.

- Replaces classful addressing.
    
- Allows cybersecurity professionals to segment classful networks into smaller chunks.
    
- CIDR IP addresses are formatted like IPv4 addresses, but they include a “/” followed by a number at the end of the address.
    

- IP Network Prefix
    

- The system of CIDR addressing reduces the number of entries in routing tables and provides more available IP addresses within networks.
    

Security Benefits of Subnetting

- Create networks within networks without requesting another network IP address from the Internet Service Provider.
    
- Uses network bandwidth more efficiently and improves network performance.
    
- One component of creating isolated subnetworks through physical isolation, routing configuration and firewalls.
    

  

Proxy Servers

> Server that fulfills the requests of a client by forwarding them on to other servers

- Dedicated server that sits between the internet and the rest of the network
    
- Determines if traffic coming in from the internet is safe, and uses a public IP address that is different from the rest of the private network
    
- Adds a layer of security
    

> Forward Proxy Server

- Regulates and restricts a person’s access to the internet
    
- Receives outgoing traffic from an employee, approves it, then forwards it on to the destination on the internet.
    

> Reverse Proxy Server

- Regulates and restricts the internet’s access to an internal server
    
- Accept traffic from external parties, approve it, and forward it to the internal servers.
    
- Useful for protecting internal web servers containing confidential data from exposing their IP address to external parties
    

> Email Proxy Servers

- Filters spam email by verifying whether a sender’s address was forged.
    
- Reduces the risk of phishing attempts that impersonate people known to the organization
    

Virtual Networks and Privacy

> Virtual Private Networks, Proxy Servers, Firewalls and Security Zones

Common network protocols

-  Rules used by all network devices that provide a mutually agreed upon foundation for how to transfer data across a network
    

Three Main Categories of Network Protocols:

1. Communication protocols are used to establish connections between servers. 
    

1. Examples include TCP, UDP and Simple Mail Transfer Protocol (SMTP)
    

3. Management protocols are used to troubleshoot network issues.
    

1. Internet Control Message Protocol (ICMP)
    

5. Security Protocols provide encryption for data in transit. Examples include IPSec and SSL/TLS
    

Other commonly used network protocols:

- Hypertext Transfer Protocol (HTTP): Application layer communication protocol.
    

- Allows the browser and web server to communicate with one another
    

- Domain Name System (DNS): Application layer protocol that translates or maps host names to IP addresses.
    
- Address Resolution Protocol (ARP): network layer communication protocol that maps IP addresses to physical machines or a MAC address recognized on the local area network
    

Wi-Fi

- WEP, WPA, WPA2 and WPA3.
    
- WPA3 encrypts traffic with the Advanced Encryption Standard (AES)
    

Network Security Tools and Practices

- Firewalls
    

- Stateless vs. Stateful firewalls
    
- Next generation firewalls
    

- Proxy Servers
    

- Utilize network address translation (NAT) to serve as a barrier between clients on the network and external threats
    

- Virtual Private Networks
    

- Encrypts data in transit and disguises your IP address.
    
- Use encapsulation, which wraps your unencrypted data in an encrypted data packet, which allows your data to be sent across the public network while remaining anonymous.
    
- Software-Defined Wide Area Network is a virtual service that allows organizations to securely connect users to applications across multiple locations and over large geographical distances
    

VPN Protocols: Wireguard and IPSec

> Main purpose of a VPN is to create a secure connection between a computer and a network.

Remote access and site-to-site VPNs

- Individual users use remote access VPNs to establish a connection between a personal device and a VPN server
    
- Remote Access VPNs encrypt data sent or received through a personal device.
    
- Enterprises use site-to-site VPNs largely to extend their network onto other networks and locations
    

- USeful for organizations that have many networks across the globe
    
- IPSec is commonly used in site to site VPNs to create an encrypted tunnel between the primary network and remote network
    

Wireguard VPN vs. IPSec VPN

- Wireguard is a high-speed VPN protocol, with advanced encryption, to protect users when they are accessing the internet.
    

- Can be used for both site to site connection and client-server connection.
    
- Download speed is enhanced by using fewer lines of code.
    
- Open source, making it easier to deploy and debug
    

- IPSec VPN
    

- Older and more complex than Wireguard.
    
- Some organizations may prefer IPSec due to it’s longer history of use, extensive security testing and widespread adoption
    

Module 3: Network Intrusion Tactics and Defense

> Network security

> Network intrusion tactics

The Case for Securing Networks

> Common network intrusion attacks:

- Malware
    
- Spoofing
    
- Packet Sniffing
    
- Packet Flooding
    

Attacks can Harm an Organization By:

- Leaking valuable or confidential information
    
- Damaging an organization’s reputation
    
- Impacting customer retention
    
- Costing money and time
    

How Intrusions Compromise Your System

> Attackers can have varying motivations for attacking your organization’s network. Financial, political or personal motivations, or they may be a disgruntled employee or an activist who disagrees with the company’s values and wants to harm an organization's operations.

Network Interception Attacks

- Intercepting network traffic and stealing valuable information or interfering with the transmission in some way
    
- Hardware or software tools to capture and inspect data in transit, referred to as packet sniffing.
    
- Allow attackers to insert malicious code or altering the message and interrupting network operations.
    

Backdoor Attacks

- Working around security measures by finding a backdoor, allowing for stealth
    
- Backdoors are weaknesses intentionally left by programmers or system and network administrators that bypass normal access control mechanisms. 
    

- Intended to help programmers conduct troubleshooting or administrative tasks.
    

- Once a hacker has entered an insecure network through a backdoor, they can cause extensive damage: installing malware, performing a denial of service attack, stealing private information or changing other security settings that leaves the system vulnerable to other attacks.
    

Possible Impacts on an Organization

- Financial: When a system is taken offline with a DoS attack, they prevent a company from performing tasks that generate revenue.
    

- Depending on the size of the company, this can cost millions of dollars.
    

- Reputation: If it becomes public knowledge that a company has experienced a cyberattack, the public may become concerned about the security practices of the organization
    
- Public Safety: Attacks on government networks can affect the safety and welfare of the citizens of a country.
    

- Public water systems, power grids, military defense communication systems
    

Denial of Service Attack (DoS) or (DDos)

> An attack that targets a network or server and floods it with network traffic, taking it offline

- Disrupt business operations by crashing servers or webpages, meaning normal users can’t access the site
    

Distributed Denial of Service Attack (DDos)

- A type of denial of service attack that uses multiple devices or servers in different locations to flood the target network with unwanted traffic
    
- Use of numerous devices makes it more likely the attack will be successful
    

SYN (synchronize) Flood Attack

- A type of DoS attack that simulates a TCP connection and floods a server with SYN packets
    

Internet Control Message Protocol (ICMP) Flood

- Internet protocol used by devices to tell each other about data transmission errors across the network
    
- ICMP Flood attacks are a type of DoS attack performed by an attacker repeatedly sending ICMP packets to a network server
    

- Forces the server to send an ICMP packet
    
- Eventually eats up all the bandwidth for incoming and outgoing traffic and causes the server to crash
    

Ping of Death 

- A type of DoS attack caused when a hacker pings a system by sending it an oversized ICMP packet that is bigger than 64KB
    
- The oversized packet will overload the server, as it cannot process the large packet
    

Read tcpdump logs

> a network protocol analyzer, sometimes called a packet sniffer, is a tool designed to capture and analyze data traffic within a network.

- Commonly used as investigative tools to monitor networks and identify suspicious activity
    

  

Most Common Network Analyzer Tools

- SolarWinds NetFlow
    
- ManageEngine OpManager
    
- Azure Network Watcher
    
- Wireshark
    
- Tcpdump
    

Tcpdump is a command-line network protocol analyzer. It is popular, lightweight (meaning it uses little memory) and has low CPU usage and uses the open source libpcap library.

- text -based, meaning all commands in tcpdump are executed in the terminal.
    
- Comes preinstalled on many Linux distros
    

> tcpdump provides a brief packet analysis and converts key information about network traffic into formats easily read by humans.

- Prints information about each packet directly into the terminal
    
- Also displays source IP, destination IP and the port numbers being used in communications
    

Interpreting Output

> tcpdump prints the output of the command as the sniffed packets in the command line, and optionally to a log file, after a command is executed

> The output of a packet capture contains many pieces of important information about the network traffic

- Timestamp: the output begins with the timestamp, formatted as hours, minutes, seconds and fractions of a second
    
- Source IP: The packet’s origin is provided by its source IP address
    
- Source Port: The port number is where the packet originated
    
- Destination IP: the destination IP address is where the packet is being transmitted to
    
- Destination Port: this port number is where the packet is being transmitted to
    

Note:  by default, tcpdump will attempt to resolve host addresses to hostnames. It’ll also replace port numbers with commonly associated services that use these ports

Common Uses

> Network protocol analyzers are commonly used to capture and view network communications and to collect statistics about the network, such as troubleshooting network performance issues.

They can also be used to:

- Establish a baseline for network traffic patterns and network utilization metrics
    
- Detect and identify malicious traffic
    
- Create customized alerts to send the right notifications when network issues or security threats arise
    
- Locate unauthorized instant messaging (IM), traffic, or wireless access points.
    

> Attackers can also use network protocol analyzers maliciously to gain information about a specific network.

- Attackers can capture data packets that contain sensitive information, such as account usernames and passwords.
    

Real-life DDos Attack

A DDoS Targeting a Widely Used DNS Server

> Many large companies were using a DNS service provide, the service provider was hosting the DNS system for these companies.

> This service provider was the victim of a DDoS attack

- Before the attack on the service provider, a group of university students created a botnet with the intention to attack various gaming services and networks.
    
- A botnet is a collection of computers infected by malware that are under the control of a single threat actor, known as the “bot-herder”. 
    

- Each computer in the botnet can be remotely controlled to send a data packet to a target system.
    

- The university students posted the code for the botnet online so that it would be accessible to thousands of internet users and authorities wouldn’t be able to trace the botnet back to the students.
    

Day of the Attack

- The botnet sent tens of millions of DNS requests to the service provider, overwhelming the system and the DNS server shut down.
    
- All of the websites the service provider used could not be reached.
    
- Outage occurred all over North America and Europe
    

Malicious Packet Sniffing

> Packet sniffing, and how threat actors or malicious groups may use it to gain access to unauthorized information.

- Packet sniffing is used by security analysts to analyze and capture packets when investigating ongoing incidents or debugging network issues.
    
- Malicious actors may also use packet sniffing to look at data that has not been sent to them
    

- Like opening someone else’s mail
    

> Packet sniffing can be active or passive. 

- Passive packet sniffing is where data packets are read in transit
    
- Threat actors can view all of the information going in and out of the device
    

- Active Packet Sniffing is where the data packets are manipulated in transit.
    

- Injecting internet protocols to redirect the packets to an unintended port or changing to information contained in the packets.
    

> Malicious packet sniffing can be prevented.

- One way to protect against malicious packet sniffing is to use a VPN to encrypt and protect data as it travels across the network.
    

- Hackers can intercept traffic protected by a VPN, but won’t be able to decode it and read the contents.
    

- Another way is to use websites that use HTTPS security protocols.
    
- Another way is to avoid using unprotected Wi-Fi networks, usually in the form of public networks 
    

- These networks don’t use encryption
    

IP Spoofing

> A network attack performed when an attacker changes the source IP of a data packet to impersonate an authorized system and gain access to a network.

> Common IP Spoofing Attacks

- On-path attack
    
- Replay attack
    
- Smurf attack
    

  

On-Path Attacks

- An attack where a malicious actor places themselves in the middle of an authorized connection and intercepts or alters data in transit
    
- Attacks place themselves between two devices, like a web browser and a web server
    

- Sniff the packet information to learn the IP and MAC addresses to devices that are communicating with each other
    
- After they have the IP and MAC addresses, they can pretend to be either of these devices
    

Replay Attacks

- A replay attack is a network attack performed when a malicious actor intercepts a data packet in transit and delays it or repeats it another time.
    

- A delayed packet can cause connection issues between target computers, or a malicious actor may take a network transmission that was sent by an authorized user and repeat it at a later time to impersonate the authorized user
    

Smurf Attack

- A combination of a DDoS attack and an IP spoofing attack.
    

- The attacker sniffs an authorized user’s IP address and floods it with packets. This overwhelms the target computer and can bring down a server or the entire network
    

How to Defend Against IP Spoofing Attacks

> Encryption should always be implemented so that the data in your network transfers can’t be read by malicious actors.

> Firewalls can be configured to protect against IP Spoofing

- IP spoofing makes it seem like the malicious actor is an authorized user by changing the sender’s address of the data packet to match the target network’s address
    
- If a firewall receives a data packet from the internet where the sender’s IP address is the same as the private network, it will deny the transmission 
    

- All devices with that IP address should already be on the local network
    

Overview of Interception Tactics

> Specific attacks that use IP spoofing and packet sniffing.

A Closer Review of Packet Sniffing

- Packet Sniffing is the practice of capturing and inspecting data packets across a network.
    
- On a private network, data packets are directed to the matching destination device on the network
    

> Network Interface Cards (NIC)

- Piece of hardware that connects the device to a network. The NIC reads the data transmission, and if it contains the device’s MAC address, it accepts the packet and sends it to the device to process the information based on the protocol.
    

- This occurs in all standard network operations
    

- NIC cards can be set to promiscuous mode,  which means that it accepts all traffic on the network, even the packets that aren’t addressed to the NIC’s device. 
    

> Malicious Actors might use software like Wireshark to capture the data on a private network and store it for later use. 

- They can then use the personal information for their own advantage
    

A Closer Review of IP Spoofing

- After a malicious actor has sniffed packets on the network, they can impersonate the IP and MAC addresses of authorized devices to perform an IP spoofing attack.
    
- Firewalls can prevent IP Spoofing by configuring it to refuse unauthorized IP packets and suspicious traffic. 
    

On-Path Attack

- Happens when a hacker intercepts the communication between two devices or servers that have a trusted relationship
    

- The transmission between these two trusted network devices could contain valuable information like usernames and passwords that the malicious actor can collect.
    

- Sometimes referred to as a man-in-the-middle attack
    
- Hackers can also intercept transmission data that contains a DNS system look-up
    

- They can then spoof the DNS response from the server and redirect to a domain name of a different IP address, perhaps one that contains malicious code or other threats
    

  

Smurf Attack

- Network attack that is performed when an attacker sniffs an authorized user’s IP address and floods it with packets
    
- Combination of IP spoofing and Denial of Service attack
    

Can be prevented with advanced firewalls and proper firewall configuration

DoS Attack

- Denial of Service attack
    
- Once a malicious actor has sniffed network traffic, they can impersonate an authorized user.
    

- Unlike IP spoofing, the attacker will not receive a response from he targeted host.
    

Note: Remember the principle of defense-in-depth. There isn’t one perfect strategy for stopping each kind of attack. You can layer defenses by using multiple strategies.

Module 4: Network Security Hardening Techniques

> Security Hardening:

- The process of strengthening a system to reduce its vulnerability and attack surface.
    

>  Attack Surface: 

- All the potential vulnerabilities that a threat actor could exploit
    

> Security Hardening can be performed on:

- Hardware
    
- Operating systems
    
- Applications
    
- Computer networks
    
- Databases
    

> Physical security is also a part of security hardening

- Installing security cameras, CCTV
    
- Hiring security guards
    

  
  

> Some common types of hardening procedures include:

- Software updates, called patches
    
- device application configuration changes
    

> These updates and changes are done to increase security and fix security vulnerabilities on a network.

> A security configuration could be considered requiring longer passwords and more frequent password changes.

- This makes it harder for malicious actors to gain login credentials
    

> A configuration check could be updating the encryption standards for data that is stored in a database. 

> Other examples of security hardening include:

- Disabling or removing unused applications and services
    
- Disabling unused ports
    
- Reducing access permissions across devices and networks
    

> Minimizing the number of applications, devices, ports and access permissions makes network and device monitoring more efficient and reduces the overall attack surface.

> Another important strategy for security hardening is to conduct regular penetration testing.

- Pen tests are simulated attacks that help identify vulnerabilities in a system, network, website, application and process.
    
- Pen testers document their findings in a report, allowing the security team to determine what vulnerabilities need fixing and what they did well.
    

OS Hardening Practices

> Why it is essential to keep operating systems secure.

> Operating systems are the interface between computer hardware and the user

- First program loaded when the computer turns on
    
- OS must be secured on each device, to prevent the entire network being compromised by one misconfigured or out of date OS
    

  

> Some OS hardening techniques are performed at regular intervals.

- Updates
    
- Backups 
    
- Keeping up to date lists of devices and authorized users
    

> Other tasks are performed only once as part of preliminary safety measures.

- Configuring encryption
    

>  A patch update is a software and operating system update that addresses security vulnerabilities within a program or product.

- With patch updates, the OS should be upgraded to its latest software version
    
- As soon as OS vendors publish a patch and the vulnerability fix, malicious actors know exactly where the vulnerability is in out of date systems.
    

- This is why it’s important to run security updates as soon as they’re released. 
    

- The newly updated OS should be added to the baseline configuration, also called the baseline image. 
    

- A baseline configuration is a documented set of specifications within a system that is used as a basis for future builds, releases and updates.
    

> Another hardening task performed regularly is hardware and software disposal.

- This ensures that old hardware is properly wiped and disposed of. 
    
- Good idea to delete any unused software applications since some popular programming languages have known vulnerabilities.
    

> Implementing a Strong Password Policy

- Strong password policies require that passwords follow specific rules. 
    

- Policy that requires 8 characters, a capital letter and a symbol, for example. 
    

- A certain user who makes incorrect login attempts too many times will lose access to the network. 
    
- Some systems also require multi-factor authentication, or MFA.
    

  

Brute Force Attacks and OS Hardening

> Brute force attacks

> Vulnerability assessments in virtual machines and sandboxes

> Preventing brute force attacks using authentication measures

Brute Force Attacks

> a brute force attack is a trial and error process of discovering private information.

- There are different types of brute force attacks that malicious actors use to guess passwords:
    

1. Simple brute force attacks: When attackers try to guess a user’s login credentials, it’s considered a simple brute force attack. They might do this by entering any combination of usernames and passwords that they can think of until they find the one that works.
    
2. Dictionary Attacks: attackers use a list of commonly used passwords and stolen credentials from previous breaches to access a system. They’re called “dictionary” attacks because attackers originally used a list of words from the dictionary to guess the passwords, before complex passwords became commonplace. 
    

> Doing a brute force attack manually takes a long time and is a tedious process, so attackers use a range of tools to conduct their attacks.

Assessing Vulnerabilities

> Companies can run a series of tests and assessments on their network or web applications to assess vulnerabilities. 

- Analysts can use virtual machines and sandboxes to test suspicious files, check for vulnerabilities before events occur, or to simulate a cybersecurity incident.
    

Virtual Machines

- VMs are software versions of physical computers. VMs provide an additional layer of security for an organization because they can be used to run code in an isolated environment, preventing malicious code from affecting the rest of the computer or system.
    

- Can be deleted and replaced with pristine images once testing is done
    

- There’s still a small risk that malicious code can escape the virtual environment and access the host machine.
    

Sandbox Environments

- Type of testing environment that allows you to execute software or programs separate from your network. They are commonly used for testing patches, identifying and addressing bugs, or detecting cybersecurity vulnerabilities.
    
- Also used to evaluate suspicious software, evaluate file containing malicious code, and simulate attack scenarios.
    
- Sandboxes can be standalone physical computers that are not connected to a network; however, it is often more time and cost effective to use software or cloud-based virtual machines as sandbox environments. 
    

- Some malware authors know how to write code to detect if the malware is executed in a VM or sandbox environment.
    
- It can be programmed to behave as harmless software when run inside testing environments.
    

Prevention Measures

> Some common measures organizations use to prevent brute force attacks and similar attacks from occurring inside.

- Salting and hashing: hashing converts information into a unique value that can then be used to determine it’s integrity. It’s a one way function, meaning it is impossible to decrypt and obtain the original text. 
    

- Salting adds random characters to hashed passwords, increasing the length and complexity of hash values making them more secure.
    

- Multi-factor authentication (MFA) and Two-factor authentication (2FA):  security measures which require users to verify their identity in two or more ways to access a system or network. 
    

- Facial recognition, fingerprints, one time passwords (OTP), username/password
    

- CAPTCHA and reCAPTCHA: Completely Automated Public Turing Test to Tell Humans and Computers Apart. Asks users to complete a simple test the proves they are human. 
    

- Prevents software from trying to brute force a password. 
    

- Password policies: Organizations use password policies to standardize good password practices throughout the business. 
    

- Policies can include guidelines on how complex a password should be, how often to update passwords, whether passwords can be reused or not, and if there are login attempt limits.
    

Network Security Hardening

> Focuses on network-related security hardening

- Port filtering
    
- Network access privilege
    
- Encryption
    

> Some network hardening tasks are performed routinely, like:

- Firewall rules maintenance
    
- Network log analysis
    
- Patch updates
    
- Server backups
    

Network Log Analysis is the process of examining network logs to identify events of interest

- Security teams use SIEMs to monitor network logs
    

Port Filtering is a firewall function that blocks or allows certain port numbers to limit unwanted communication

- Basic rule: only the ports that are needed are the ones that are allowed
    

Network Segmentation is used to create isolated subnets in their organization

- This prevents issues from one subnet from jumping to another subnet
    
- Only specified users are given access to parts of the network critical to their job roles
    
- Also used to separate different security zones
    

Network Security Applications

> Learn the role of four different devices used to secure a network: 

- Firewalls
    
- Intrusion detection systems
    
- Intrusion prevention systems
    
- SIEM tools
    

> Learn the benefits of layered security

- Each tool has it’s place in the network architecture
    

  

Firewall

- We’ve already learned about stateless firewalls, stateful firewalls, and next-generation firewalls.
    
- Most firewalls are similar in basic functions.
    

- Allow or block traffic based on a set of rules
    
- As data packets enter the network, the packet header is inspected and allowed or denied based on its port number
    

- NGFWs are also able to inspect packet payloads.
    

> Each system should have it’s own firewall, regardless of the network firewall

Intrusion Detection System

- Application that monitors system activity and alerts on possible intrusions.
    
- Configured to detect known attacks.
    
- Some IDS will not only review signatures of anomalies, not just known attacks.
    
- If an anomaly is discovered, an alert is sent to the network admin who can investigate further
    

> Limitations:

- Can only scan for known attacks or obvious anomalies
    
- New and sophisticated attacks may not be caught
    
- Doesn’t actually stop incoming traffic, just alerts the analysts and administrators
    

> Combined with a firewall, IDS add another layer of defense.

- The IDS is placed behind the firewall before entering the LAN.
    

- This is done to reduce noise in IDS alerts, also referred to as false positives.
    

Intrusion Prevention System

- Application that monitors system activity for intrusive activity and takes action to stop the activity.
    
- Offers more protection than an IDS because it actively stops threats and anomalies when they are detected.
    
- IPS searches for signatures of known attacks and anomalies.
    
- The IPS sits behind the firewall in the network architecture. 
    

- Offers a high level of security because risky data streams are disrupted before they even reach sensitive parts of the network. 
    

> One downside is that the IPS is inline: if it breaks, so does the connection between the private network and the internet.

- Another downside is false positives.
    

Full Packet Capture Devices

- Incredibly useful for network admins and security professionals. 
    
- Allow you to record and analyze all of the data that is transmitted over your network.
    
- Also aid in investigating alerts created by an IDS.
    

Security Information and Event Management (SIEM)

- Collects and analyzes log data to monitor critical activities in an organization.
    
- Also analyze data from IDSs, IPSs, firewalls, VPNs, proxies and DNS logs.
    
- Great way to aggregate security event data so that it all appears in one place for security analysts to analyze.
    

Network Security in the Cloud

> a cloud network is a collection of servers or computers that stores resources and data in remote data centers that can be accessed via the internet.

- Also require network hardening preventative measures
    
- One distinction between cloud network and traditional network hardening is the use of a server baseline image for all server instances stored in the cloud.
    

- Allows you to compare data in the cloud servers to the baseline image to make sure no unverified changes have been made.
    

Secure the Cloud

> Cloud Computing is a model for allowing convenient and on-demand network access to a shared pool of configurable computing resources.

> Many organizations that use cloud resources and infrastructure express concerns about the privacy of their data and resources. This concern is addressed through cryptography and other security measures.

Cloud Security Considerations

- Identity access management: a collection of processes and technologies that helps organizations manage digital identities in their environment. 
    

- Also authorizes how users can use different cloud resources.
    

- Configuration: Each service must be carefully configured to meet security and compliance requirements. 
    

- When organizations initially transition to cloud services, they must ensure every process moved into the cloud has been configured correctly. 
    
- If network admins and architects are not meticulous in correctly configuring the organization’s cloud services, they could leave the network open to compromise.
    

- Attack Surface: every service or application on a network carriers its own set of risks and vulnerabilities and increases the overall attack surface.
    

- Increased attack surfaces must be compensated for with additional security measures.
    
- Cloud networks that utilize many services introduce lots of entry points into an organization’s network. If the network is designed correctly, utilizing several services does not introduce more entry points into an organization's network design.
    

- Zero-day Attacks: exploit that was previously unknown. CSPs are more likely to know about a zero day attack occurring before a traditional IT organization does.
    

- CSPs have ways of patching hypervisors and migrating workloads to other virtual machines, ensuring the customer is not impacted by the attack.
    

- Visibility and Tracking: Network administrators have access to every data packet crossing the network with both on-premise and cloud networks. 
    

- They can sniff and inspect data packets to learn about network performance or to check for possible threats and attacks. 
    
- This visibility is also offered in the cloud through flow logs and tools, such as packet mirroring. CSPs take responsibility for security in the cloud, but they do not allow the organizations that use their infrastructure to monitor traffic on the CSP’s servers.
    

Things Change Fast in The Cloud

> CSPs are large organizations that work hard to stay up to date with technology advancements. 

- For organizations used to being in control of their network, this can be a potential challenge to keep up with.
    
- Organizations that used CSPs usually have to update their IT processes. It is possible for organizations to continue following established best practices for changes, configurations and other security considerations. 
    
- Each service adds complexity to the security profile of the organization, and they will need security personnel to monitor all of the cloud services. 
    

Shared Responsibility Model

- States that the CSP must take responsibility for security involving the cloud infrastructure, including physical data centers, hypervisors, and host OS. 
    

- The company providing the assets is responsible for the assets and the processes that they store or operate in the cloud. 
    

- Clarity on where the responsibility for security begins and ends.
    

  
  
  
  

Cryptography and Cloud Security

> Address common cloud security hardening practices, what to consider when implementing cloud security measures, and the fundamentals of cryptography. 

Cloud Security Hardening

- Incorporating IAM,
    
- Hypervisors
    
- Baselining
    
- Cryptography
    
- Cryptographic erasure
    

Identity Access Management (IAM)

- Collection of processes and technologies that helps organizations manage digital identities in their environment.
    

Hypervisors

- Abstracts the host’s hardware from the operating software environment. There are two types of hypervisors. 
    

- Type one runs on the hardware of the host computer. (VMware ESXi)
    
- Type two hypervisors operate on the software of the host computer (VirtualBox)
    

- CSPs commonly use type one hypervisors.
    
- CSPs are responsible for cloud resources and cloud environments being available, and providing regular patches and updates. 
    
- Vulnerabilities in hypervisors or misconfigurations can lead to virtual machine escapes, an exploit where a malicious actor gains access to the primary hypervisor, potentially the host computer and other VMs
    

Baselining

- Baselining for cloud networks and operations cover how the cloud environment should be set up
    
- A baseline is a set reference point. 
    

- This reference point is used to compare changes made to a cloud environment.
    

- Proper configuration and setup can greatly improve the security and performance of a cloud environment.
    
- Examples of establishing a baseline in a cloud environment include:
    

- Restricting access to the admin portal
    
- Password management
    
- File encryption
    
- Threat detection services for SQL databases
    

Cryptography in the Cloud

- Cryptography can be applied to secure data that is processed and stored in a cloud environment.
    
- Cryptography uses encryption and secure key management systems to provide data integrity and confidentiality
    

Cryptographic Erasure

- Method of erasing the encryption key for the encrypted data. 
    
- When destroying data in the cloud, more traditional methods of data destruction are not as effective. 
    
- Crypto-shredding is a newer technique where the cryptographic keys used for decrypting the data are destroyed
    

- This makes data undecipherable and prevents anyone from decrypting the data. 
    

Key Management 

- Modern encryption relies on keeping the encryption keys secure. These are measures that can be used to further protect your data when using cloud applications. 
    

- Trusted platform module (TPM) - computer chip that can securely store passwords, certificates and encryption keys.
    
- Cloud hardware security module (CloudHSM) - a computing device that provides a secure storage for cryptographic keys and processes cryptographic operations, such as encryption and decryption
    

- Almost all CSPs allow customers to provide their own encryption keys and ensuring the keys remain confidential. 
    

- CSP is limited in the event that customer keys are destroyed or compromised. 