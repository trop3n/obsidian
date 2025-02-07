
## Introduction

As the network bandwidth expands, and streaming technologies develop, there is greater access to information along with improved abilities to communicate using video. New uses for streaming content continue to emerge everyday as the technology provides applications with greater capabilities and flexibility.

This course examines the principles of streaming, including the different compression techniques, transfer methods, and protocols.
## Objectives

Upon completion of this course, you will be able to:

- Understand the process of streaming content from source to endpoint
- Identify the factors to consider when streaming content over a network
- Define how to access streaming content
- Understand the demand for higher resolutions and need for compression
- Identify the different compression codecs and their impact on system design
- Define the various transport protocols and how they work together
## What is Streaming?

Streaming is a method of *transporting media over a network as a steady, continuous flow, allowing playback to proceed while subsequent data is received*.

The audio, video, or computer based media can either be live or pre-recorded content, and is transmitted and received by network devices, such as servers and computers. 
### The Benefits of Streaming

Some of the challenges in AV technology is to support an ever-increasing surge of mobile devices, the demand for high-resolution, low bit rates, and better quality of service. Streaming is a powerful technology that can enhance the operating efficiency of an AV system.

- **Easily Accessible**: View content on computers, laptops and mobile devices without having to download it
- **Scalable Distribution**: Extend visual communication beyond a room or building to any destination
- **Greater Flexibility**: Seamless integration into existing systems and simplified cable infrastructure
### Streaming Applications

As AV technology continues to innovate, streaming has become increasingly more accessible. The following are a few examples of where streaming is used.

- **News & Entertainment** - On demand, distributed, and mobile viewing. 
- **Business** - Videoconferencing, live webcasting, and online learning
- **Education** - Distance learning - e-learning, and lecture capture
- **Medical** - Real-time transmission, remote collaboration, broadcasting, and education
- **Command and Control** - Real-time communication
- **Security Surveillance** - Remote, live video monitoring
- **Social Media** - Easily accessible and availability of video recording capabilities on mobile devices

Being able to access these applications makes it convenient for broader audiences to participate.
## Streaming Architecture

The structure to provide a streaming solution begins with the audio and video feeds from the event. These source signals are input into production equipment, then fed into a streaming media encoder. The encoder is used to provide high quality video processing and deliver content to a media server for live sessions or archiving over the Internet.

Sufficient network bandwidths should be made available for the encoder to deliver HD video streams to the media server. To receive the streaming feed, users can access online content with a wide variety of devices through web browsers or media playback applications.

When IP data reaches a streaming media decoder, the original information can be retrieved. Decoded have the flexibility to play back locally connected AV signals, a live streaming source, or media files from memory and storage devices. 
## Accessing Streaming Content

With streaming capabilities supported in some many different applications, whether it's one, or a combination, the following methods are typically being used.
### Live Streaming

**Live Streaming** is the delivery of content in real-time as events happen, much like a live television broadcast that transmits content over the airwaves. A common example of live streaming is a sporting or news event where coverage is delivered in real-time to computers or mobile devices.

Live Internet streaming requires a form of source media (video camera, audio interface, screen capture software), an encoder to digitize the content, a media publisher, and a content delivery network to distribute and deliver the content. Live streaming does not need to be recorded at the origination point, although it can be.
### Video On-Demand

***Video On-Demand*** is an interactive technology that allows content viewing in real-time or downloading programs for viewing later. A VoD system can consist of a standard set-top box, or service delivered over the Internet to home computers, smartphones and portable devices. 

- **Stored Content**: Video can be streamed on-demand for convenient viewing playback, a method leveraged by Netflix and YouTube. Content for images, videos, and music can be located on a storage device or server. When it's ready to be viewed, users can request the media files to be transported for playback.
- **Progressive Download**: When video files are stored on a webserver and the files are downloaded over the Internet. Once a video file is requested from the client, the video file will start to play once enough of the file is received. A standard, non-progressive download can only be played when the entire file is downloaded.
## Delivering the Signal

In order for streamed content to travel from the source to an endpoint, it needs to undergo significant processing. This is a complicated process and it is not handed exactly the same way in every application. Typically, the streaming process goes through these steps:
### Encode

Source content generally is too large to send over a network. When encoded, the incoming source signal is processed, and compressed. Then the process of encapsulation  places the compressed video and audio data into packets. This bundling of information prepares the data for the next phase, transport. 

***Compression*** is the process of modifying the incoming signal data in such a way that it consumes less resources and enable sit to be sent more efficiently over a network.
### Transport

The transport step defines the transmission method, control, and streaming protocols for the delivery of data. Many streaming solutions appear the same to the viewer, but the underlying methods used to deliver the video are different. The transport of data between these devices could use a variety of protocols. 
### Decode

During this phase, all the work of the first two phases are reversed. The received packets will be analyzed, de-compressed, reconstructed into a signal, and delivered to the endpoint. The decoded image however, is dependent on the type and amount of compression used. Other elements can influence the image quality as well, ranging from undetectable to significant. 
## Image Attributes

With greater access to information and an improved ability to communicate, there are several factors to consider when streaming video and graphics content over the network. 
### Full-Motion Video

For full-motion video applications, the following attributes are used to define the most common resolutions and frame rates.

- **Standard Definition**: 640x480 at 30fps
- **High Definition**: 1280x720 or 1920x1080 at 60fps
- **Ultra-High Definition**: 3840x2160 or 4096x2160 at 30 or 60 fps
### Graphics

High resolution graphics, and computer images differ from video in that the extent of motion can vary between the following categories.

- **Static Images**: Maps, data screen and presentation slides at 1fps and slower.
- **Moderate Motion**: Majority of the image remains static with intermediate text, alarms and cursor movements at 15-30fps
- **Real-Time Imagery**: Computer animations and multimedia content at 60fps.
## Signal Distribution

Streaming solutions are meant to expand system capabilities and increase endpoint locations using network infrastructure. Transmitting images from the source device to a display has traditionally used analog or digital signals carried over native AV cabling. For standard definition video, a single coaxial cable would carry composite signals. In broadcasting, digital standards use 3G-SDI, HD-SDI, and SDI. For computers, displays, and other AV sources, DVI, HDMI and DisplayPort are used. 

In many applications, structured cable such as Category 6, CAT6 can be used with twisted pair or transmitters and receivers to extend AV signals over greater distances. Fiber optic technology is also a common solution for distributing secure data transmission over long distances with immunity to interference. 
## Performance vs Accessibility

"Quality" can often be a relative term, especially when streamed video is encoded, and then viewed. What constitutes an acceptable viewing experience for consumer purposes may not meet the needs of professional applications. 

- For consumers, the expectations are lower. Users are more interested in availability and immediacy, and less concerned with low bandwidths over a public network.
- In professional applications, the viewing benchmark is high resolution quality that is broadly accessible to many participants. The use of private networks in these environments usually offer greater bandwidth and Quality of Service - QoS.
## Application Requirements
As previously shown, streaming is mostly dependent on the type of application and viewing environment. This variety in performance expectation exists in the following table which identifies various categories and their general requirements for quality content. 
## Streaming Factors

When it comes to transmitting video content; security cameras, media content servers, and AV encoders are all responsible for sending packets of information across a network. These devices have different encoding methods where the bandwidth requirements could vary. 

There are also other varying factors to consider for the streaming application that requires attention as well. These elements range from the device or system and the user, to the following:

- Available bandwidth
- Device compatibility
- System expansion
- Application workflow
- Latency time delay

# Understanding Compression

## What is Compression?

The ability to reduce data can save storage space and enable higher resolution signals to be sent across existing infrastructures and streamed over the internet and network. Compression is the process of compacting images and audio information into a smaller number of bits.

The following are the three categories of compression:

- ***Mathematically Lossless Compression***: The data is perfectly reconstructed from its compressed state to match the original image. 
- ***Visually Lossless Compression***: The decoded image is not reconstructed mathematically but appears to be of the same quality as the original. 
- ***Lossy Compression***: Some data of the encoded image is permanently lost when an approximation of the original is reconstructed but achieves much smaller file sizes. 
## The Need for Compression

The demand for higher quality resolutions continually tests the ability to extend, switch, and distribute high-speed multi-gigabit video signals across an AV system. Additionally, many applications require recording, storing, and sending these high speed signals across an entire network. 

For example:

- 1920x1200 video signals refreshing at 60fps with a color depth of 24 bits per pixel requires a data rate of at least 3.3 Gbps.
- 4K and Ultra HD video standards extend data rates well beyond 10 Gbps
- Disk storage mediums such as CD-ROMs and DVDs are not capable of holding uncompressed video files above 70-100GB.

When other data, such as email, file transfer, and IP communication occupies network bandwidth simultaneously, compressed audio and video files are required to NOT exceed the capacity of a standard network. 
## Compression Methods

> There are two commonly used approaches to compressing the amount of data in still images and full motion video while still maintaining the quality. 

- ***Spatial Compression***: Also referred to as Intra-Frame Compression, looks for patterns and repetitions among pixels to reduce the amount of visual information required to create a single frame. This process to encode a compressed image includes:
	- Transform - Converts data into an easy compression format
	- Quantize - Removes redundant or unimportant information
	- Reorder - Groups the quantized data according to its significance.
	- Encode - Employs algorithms to reduce data without losing image information.

- ***Temporal Compression***: Also referred to as Inter-Frame Compression, looks for images that appear to be stationary and reduces the redundant information and similarities across multiple frame rates. 

***Sampling*** is a form of compression that reduces the resolution of color (chroma) with respect to the resolution of brightness (luma).
## What is a Codec?

The term ***codec*** is formed by the words, *code* and *decode*. Codecs are devices or programs with technologies that compresses a signal for more efficient transmission, the decompresses it for editing and playback. 

Most commonly, codecs are used in streaming media, video editing and videoconferencing applications. Some codec example are XviD, DivX, RealAudio, MP3, MJPEG and JPEG2000.
### Compression Codecs

Codecs based purely on spatial techniques include: 

- **VESA Display Stream Compression - DSC** - uses predictive encoding to achieve visually lossless spatial compression in a display link. 
- **Motion JPEG** - Each video frame is compressed separately as a JPEG image.
- **JPEG 2000** - A wavelet-based standard with the ability to represent the image at various resolutions.

MPEG standards, such as MPEG-2, H.264 / MPEG-4, and H.265 / High Efficiency Video Codec - HEVC include advanced algorithms with temporal and spatial techniques and predictive coding to achieve high compression ratios. 

VP8, VP9 and VP10 are video compression formats owned by Google that are designed to be alternatives to the MPEG codecs. 
## Image Quality

Visually lossless video is always the desired result for any given application. But, how much reduction in quality would be acceptable, and is the loss noticeable?

***Image Quality*** refers to how well a reconstructed image represents the original uncompressed version. Multiple factors affect image quality and the amount of original data delivered after decoding. Some considerations include the image content, the screen size of the viewing device, the coding standards or compression methods that were used, available bandwidth, and human visual perception. 
## Data Rate

The Ethernet is a system that designates how devices connect, communicate and transmit data over a network. The speed at which data can be transmitted from one device to another in bits per second is the **Data Rate**.

An uncompressed image with a resolution of 1920x1200 that updates at 60 fps requires a data rate of 3.3 Gbps. The following table shows approximate data rates for various signals. As you can see, a 100 Base-T Network (100Mbps max) cannot support the streaming of uncompressed standard definition video. Even gigabit networks (1 Gbps maximum) are not able to stream very many of the uncompressed signal types. 

| Signal | Horizontal Pixels | Vertical Pixels | Frames Per Sec | Approximate Data Rate |
| ------ | ----------------- | --------------- | -------------- | --------------------- |
| VGA    | 640               | 480             | 60             | 442 Mbps              |
| SVGA   | 800               | 600             | 60             | 691 Mbps              |
| XGA    | 1024              | 768             | 60             | 1.1 Gbps              |
| SXGA+  | 1400              | 1050            | 60             | 2.1 Gbps              |
| UXGA   | 1600              | 1200            | 60             | 2.8 Gbps              |
| WUXGA  | 1920              | 1200            | 60             | 3.3 Gbps              |
| NTSC   | 720               | 486             | 30             | 126 Mbps              |
***Data Rates***:

- Ethernet: 10Base-T - 10 Mbps
- Fast Ethernet 100Base-T = 100 Mbps
- Gigabit Ethernet: 1000Base-T = 1 Gbps (1,000 Mbps)
- 10G Ethernet: 10GBase-T - 10 Gbps (10,000 Mbps)

## Latency

Codecs often employ complex algorithms that achieve higher compression ratios at the expense of processing time, resulting in delay. The amount of delay, or time it takes for video and audio to be delivered from the source to the destination is called ***Latency***. Some of the common causes for latency issues are encoders and decoders, the network, scalers and displays.

For example, television broadcasts and video-on-demand applications can tolerate several seconds of latency, but real-time applications such as video conferencing or command center operations demand low latency responses.
# Transport and Protocols

There are many different combinations of transport protocols that work together to deliver compressed AV data to their destination. When digital image data is streamed across a network, the frames must be separated into packets, then labeled with a destination address and sequence number. 

The nature of the content is irrelevant, however, the objectives for sending this information can differ.

- For example, it can be intended for real-time delivery, or streamed from a single source to multiple destinations. 

The ***Internet Protocol (IP)*** defines addressing methods and structures for datagram encapsulation that allows the delivery of packets from a source to a destination.

## Network Categories

There are many types of networks, which are primarily distinguished by their size, capability, and purpose generally divided into three classes:

- **Local Area Network - LAN** – Uses physical wiring to connect devices within a home, school, or office. Normally, a LAN is comprised of computers, peripheral devices, and local servers connected to a common network switch.
- **Wireless Local Area Network - WLAN** – Connects wireless devices to each other using high frequency radio signals to communicate data. The term Wi-Fi, refers to a device’s ability to operate within a wireless network, or WLAN.
- **Wide Area Network - WAN** – Networks that are located in different geographical locations and provides communication to smaller networks or LANs using routers and switches.
## Transport over the Network

When it comes to effective communication over a network, several models exist to handle the various technologies, and how they interact to ensure interoperability. Most common used is the ***OSI - Open Systems Interconnection Reference Model***.

The OSI Reference Model is a set of rules, procedures, and formats, defined in seven levels, or layers. Starting at the bottom of the OSI model with the Physical Layer 1, data flows through the other layers to Application Layer 7 at the top, which delivers the final output.
## Network Switches

Switches are used to link network devices together and transfer data from one port to another based on information within the packets being transmitted. These network switches are often described as Layer 2 or Layer 3 switches based on their level in the OSI Model.

- **Layer 2 (MAC) Switch** – Forwards traffic within a LAN based on the MAC address of both sending and receiving devices. MAC address tables are built by learning what physical port they can be found on. Since Layer 2 switches are not able to apply any intelligence when moving packets, they have little impact on network performance or bandwidth.
    
- **Layer 3 (IP) Switch** – Manages traffic between subnets, LANs (or VLANs) based on the IP address or priority. These switches support routing between VLANs, link large networks together, share routing tables, and allow for multicast traffic on the network.

**MAC Address**: Media Access Control in a unique identifier assigned to each network device or computer by its manufacturer. The 48-bit address is expressed as 12-digit hexadecimal number, separated by dashes or colons.

## Network Layer Protocols - TCP

Controlling the flow of data is important for a network’s ability to provide sufficient access, bandwidth, and security. The **Transmission Control Protocol - TCP** helps to manage this high-level data exchange by defining the amount of traffic over the network and being responsible for the actual delivery of data.  
  
TCP is a connection-oriented protocol. Once a connection is established, packets can be sent reliably in order. TCP and IP work together to control network data transmission. Collectively they are the Internet Protocol Suite known as TCP/IP.

## Network Layer Protocols - UDP

The **User Datagram Protocol - UDP** is a connectionless protocol used in real-time streaming applications where best effort delivery is acceptable and the network devices and applications manage data flow control and errors.

## Data Communication Methods

Below are two methods of sending messages over the network.

- ***Unicast***: Uses one-to-one transmission to deliver video from one point in the network to another. The content can be delivered on-demand or broadcast.
- ***Multicast***: Delivers one video stream to many endpoints as one-to-many connection between server and clients. The **Internet Group Management Protocol - IGMP** provides query services to identify network destinations, along with snooping capabilities that block traffic from ports that aren't subscribed to the multicast membership. If network switches are not configured properly, every connected device can be flooded with unwanted traffic.
## Streaming Protocols

The following protocols are useful in defining the control sequences for multimedia playback, while also maintaining an end-to-end encryption.

- ***Real-Time Transport Protocol***: is the end-to-end transfer of real-time multimedia data over unicast or multicast network services.
- ***Real-Time Streaming Protocol***: is an on-demand network protocol designed to control streaming of continuous data sessions between media servers and endpoints.
- ***Real-Time Messaging Protocol***: Enables the delivery of audio, video and data over the Internet between Flash-based technologies and the Server.
- ***Hypertext Transfer Protocol***: is the set of rules for transferring text, graphic images, sound, video and other multimedia files on the World Wide Web.
## Extron Streaming AV Solutions

Record and stream live video content with Extron streaming solutions. Along with video processing, control and networking, these systems provide visually lossless quality, low latency, and resilience to errors.

- [NAV Pro AV Over IP](https://www.extron.com/NAV-Pro-AV-Over-IP/prodsubtype-706) – Distribution and switching of ultra-low latency, 4K/60 video, and audio over 1 and 10 Gbps IP networks
- [H.264](https://www.extron.com/H-264/prodsubtype-481) – Lecture Capture, Media Processors, Media Players, Encoders, and Decoders
    
    - Streaming Media Processor – SMP
    - Streaming Media Encoder - SME
    - Streaming Media Decoder - SMD
- [VN-Matrix Systems](https://www.extron.com/VN-Matrix/prodsubtype-418) – VNM recorders, encoders and decoders

