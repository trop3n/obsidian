# Simple Demonstration

Audio and Video are separately routable.

# Network Solution vs. Digital Snake

> Dante networks are often confused for network protocols or digital snakes.

- Both use CAT cable or fiber optic cable, so what's the difference?

A Dante network is far more powerful than a *digital snake*. 

A digital snake is typically a point to point connection on a linear cable path. 

### Digital Snake vs Digital AV 

|                                  | Point-to-Point    | Networked Solution          |
| -------------------------------- | ----------------- | --------------------------- |
| Where Does the Signal Go?        | Linear cable path | Anywhere on Network         |
| How to Change Signal Path?       | Move the cable    | Click of the Mouse          |
| Can we Split Signals             | No                | Yes - on network            |
| Share Cables with other Signals? | No                | Yes - common infrastructure |
> Dante makes products more versatile, making it easier to get more functionality out of them. 
### Signal Splitting

A wireless mic, for example, could be split between a monitor desk with virtual soundcheck capabilities and a Front of House desk with virtual soundcheck capabilities. 

The wireless mic could ultimately be split to many different devices across a network switch.
### Flexible Capacity

With digital snakes and Point to Point (P2P) connections:

- Sometimes three unrelated connection types for one signal chain (USB, Analog, Digital)
- Stagebox channels used for background tracks
- No control links

With a Dante Network Solution:

- Common network for many functions:
	- Dante audio
	- Mixer control
	- Amp Monitoring
- Stagebox untouched by BG tracks
### Summary: What is Dante?

- Dante is not just an audio-video transport, it is a complete solution.
	- Standardized management, maintenance, support network, training etc.
- Dante is powerful, intuitive, and cost-effective.
	- Simple plug and play start. Advanced configuration waiting when you need it.
	- Flexible audio and video routing and splitting.
- Benefits from "the Network Effect". 
	- In 2019, we passed 1,000,000 devices in the field. 
	- Thousands of devices to choose from, including unique problem solvers.

# Basics of Digital Audio

### What is a Sound Wave?

> Sound is created by vibrations. 

When a wave is captured, points along the wave are plotted at set intervals.

- The plots are then converted to binary, and then are able to be played back by the computer. 

**Digital Word**: the name of a plot on the waveform.

When people refer to bit depth or word length, they are referring to the number of binary bits used to record the reading. 

**24-bit**: Scale that uses 24 binary digits, or Resolution in Amplitude. Dante ca also manage **32-bit depth** audio. 

**48kHz Sample Rate means**: Measure the wave 48,000 times/second, or Resolution in Time (Frequency)
#### Capturing a Sound Wave

**Nyquist Theorem**: Sample rate must be at least twice the highest frequency.

> If the sample rate is too low, for instance, 7 cycles per 8 samples, the waveform will not be plotted correctly.

### Multiple Sample Rates & Bit Depths

☑️ Sample Rate and Bit Depth Match

☑️ Bit Depth Mismatch

✖️ Sample Rate Mismatch

> Think of this like gears with different tooth spacings. 
> 
> A higher sample rate will mean more gear teeth, meaning that it will no longer be compatible with a lower bit depth.

A **sample rate converter** can be used to make a higher sample rate and incompatible or lower bit depth compatible. 

**Dante supports multiple simultaneous sample rates**

- A single clock leader will coordinate all sample rates and frame rates. Dante ports must be at the same sample rate to connect.

- Dante ports must be at the same sample rate to connect. Some devices can bridge: two separate Dante ports with Sample Rate Conversion
### Audio Basics: Estimating Bandwidth

- Bandwidth is more than just audio data - also network overhead.
	- Shippers move the size/weight of the whole package, not just the items inside it.
	- *to/from addresses, packet formatting data, etc.*
- Rule of Thumb: 512 channels per 1Gbit link
	- **Wisdom**: Don't plan to usee 100% network bandwidth. 
	- This 512 channel rule of thumb is under 80% utilization

512 Channels x 48 kHz x 24 bit = 590 Mbps (contents) or 768 Mbps (total bandwidth)

**Rule of Thumb**: Double Sample Rate, Reduce Channels by Half
(Assuming you need bandwidth to remain constant)
#### Network Hubs

**Network Hubs** repeat any incoming data to all outputs.

- Hubs make a giant "collision domain".
- If two packets are sent at the same time, the data collides and must be retransmitted.
#### Network Switches

**Network Switches** only send incoming data where it belongs.

- Switches buffer data packets. 
- If two packets target the same port at the same time, they are queued and sent first in, first out. So a 1Gbps network can move thousands of channels

### Audio Basics: Summary

- **Bit Depth** represents the resolution of the sound wave amplitude.
	- e.g. 16-bit (CD), 24-bit to 32-bit (Pro Audio Production Capture)

- **Sample Rate** is the resolution of time - measured in *digital words / sec*
	- e.g. 44.1kHz (CDs), 48kHz (Pro Audio), 2x or more is "high resolution"

- To connect: sample rates must match, bit depths can be mixed.

- 512 channels on a 1Gbps connection; the Network can have more.
	- Dante capacity scales with bandwidth. (2Gbps link could carry 1024 channels, etc.)
	- *Doubling sample rate doubles bandwidth* or halves the channel count. 
	- The network switch itself is not limited to the port speed.

# Basics of Digital Video

- A digital image is made up of "pixels" (colored dots on a grid)
-  An image size is described in total pixels and aspect ratio
	- 480p (720x480) - Standard Definition - DVD Quality
	- 720p (1280x720) - High Definition
	- 1080p (1920x1080) - High Definition
	- 4K (3840x2160) - Ultra High Definition (UHD) 
### Aspect Ratio
> Ratio of the image's width to height

> Excess parts are cropped off to fill the screen. 

- If important parts are cropped off, you may not want to do this.
- Also, if the resolution is too low, it'll start to look bad if it's zoomed in too far. 

There are a lot of aspect ratios available, and some have taken the sensible approach and added decimal points to the aspect ratio for more precision.

- E.g. 1.85:1, 1.78:1 (16:9)

**Anamorphic setting**: existed on many commercial televisions, wasn't just about stretching the aspect ratio to make everyone look short and stout.

The filmmaker would use a lens on the camera to make the captured film fit onto the film they had available. 

They would then place a different lens on the projector to undistort the image for viewing, to the perspective they had intended. 
### Interlaced vs. Progressive

- An image can be drawn as interlaced or progressive. 

**Interlaced** draws the odd lines, then the even lines. (480i, 1080i)
- Broke a single frame into two fields
- Used in early televisions

**Progressive** draws all lines in order. (480p, 720p, 1080p, 4k)
- More common today
- Does not have two fields

Interlaced images were used to combat flickering.

The two fields of the interlaced image were actually *taken at a different time*.

> Pixels luma and chroma can be grouped and/or saved in HDR

### 4:4:4 vs 4:4:2 vs 4:2:0

> The human eye can discern much more in darkness than it can in color.

Encoding descriptions work in a grid of 4x2 pixels.

Each pixel of the Luma (brightness) is captured individually.

- There is no difference between the three schemes here. 
- The middle digit (4:**2**:2) represents all the digits in the first row with their own **chroma**.

> In 4:4:4, we are saving everything. Every pixel in the first row has it's own color data.

> When a two is present for the middle digit, that means it's only having data for every *other pixel*.
> 	These pixels will still appear different when the chroma (color) and luma (brightness) are combined.

> The third digit represents the number of pixels in the second row with their own color information. 
> 
> 	In 4:4:4, each pixel gets it's own color information
> 	In 4:4:2, color is described for *pairs of pixels.*
> 	In 4:2:0, there is *no unique color information recorded* for the second row. 

**Dante AV supports all three schemes**. As a matter of fact, also bit depths within the channels are supported. 
### Video: High Dynamic Range

The human eye is capable of picking up incredible differences from light to dark, but it can't be captured all at the same time.

The eye narrows the brightness to a certain range based on the amount of light. 

**High Dynamic Range** better captures and highlights the range of light and shadows.

### Frame Rate

> A video will flash images at a given frames per second (fps).

- Film: 24fps
- TV (PAL): 25fps
- TV (NTSC): 30fps

Like audio sample rates, frame rates double.

So: 24fps doubles to 48fps, 25 doubles to 50fps, 30fps doubles to 60fps

- This is done for better motion smoothness for the viewer. 

### JPEG 2000 Codec

**Dante AV is built to be codec agnostic**.

A raw 4k/60 signal is over 10Gbps. How would it work over a 1Gbps link?

- Dante AV used a JPEG 2000 codec.

For a video encoder and decoder to be able to work together, they *must be using the same codec*.

> 65% of digital cinemas use intoPIX JPEG 2000 codec.

JPEG 2000 Codec has *no generational loss*.
- Subsequent decode and encode with no loss.

> JPEG 2000 Codec has a visually lossless step at the first compression, then no more compression after that. JPEG 2000 can dissemble and reassemble the image over and over with no visual loss. 

JPEG 2000 is an ***Intra-frame Codec***, which encodes one frame at a time. 

By contrast, MPEG is an ***Inter-frame Codec***, which encodes frames in groups. 
- The first is called a key frame, where the entire image is encoded. 

JPEG 2000 is a lower-latency codec. Any errors or packet loss is contained in one part of one frame.

### How Much Data will a JPEG 2000 Codec Use?

> The amount of data used depends on the complexity of the image being transmitted. 

| Resolution & Frame Rate | Color Space | Raw Data Uncompressed | Maximum EDR | Typical EDR |
| ----------------------- | ----------- | --------------------- | ----------- | ----------- |
| 4kp60                   |             | 8.49 Gbps             | 600 Mbps    | 540 Mbps    |
| 4Kp30                   | 4:2:2       | 4.25 Gbps             | 400 Mbps    | 270 Mbps    |
| 1080p30                 |             | 1.00 Gbps             | 150 Mbps    | 68 Mbps     |
*Estimated Dante AV Data Rates using well lit content in encoded with Ultra Low Latency codec.*

For more bandwidth estimations, please refer to
“Dante AV JPEG 2000 Bandwidth Estimator”

### High-bandwidth Digital Copy Protection

- HDCP is High-bandwidth Digital Content Protection
	- Protects (locks) copyrighted material in transport between devices. 
	- Common for Blu-ray, Cable/Satellite TV, Computer video out, etc.

- If content is HDCP protected, Dante AV follows HDCP v2.3 rules.
	- Allows up to 16 devices participating with the video path.
	- Validated by DCP for unicast and multicast modes. 

- If content is not HDCP protected, Dante AV *does not add it*.

- Dante audio channels are unaffected by HDCP.

### Summary

- Structural Video Settings
	- Resolution, Aspect, Interlaced

- Color Space:
	- Color encoding (eg 4:2:2, bit depthj and High Dynamic Range processing)

- Video Codec: **JPEG 2000**
	- Used in 65% of digital cinemas today
	- Visually lossless, appropriate for natural video and computer graphics.

- Supports up to 4K/60 Resolution
	- HDCP Copy protection management (only if content is protected)
	- Signal can be split on network - *more on this in Level 2 class, Multicast*

- Audio is uncompressed, just like other Dante audio devices. 

# Dante Ports & Connections

> Some Dante devices will have one port on them, which is self explanatory.

> Some Dante devices have two ports, which means they default to a ***Daisy-Chain or Switched mode.***
> 	It doesn't matter which one you connect to, it will get to the internal Dante port. 

### Network Topology: Daisy Chain (aka Switched)

> Daisy chain is an engineering term which represents several nodes or modules that linked linked together sequentially. 

A daisy chain should be limited in length.
### Network Topology: Star

> When multiple switches are linked together, it is often called a **Trunk Line or an Uplink.**
### Network Topology: Connections (Best Practice, Wiring)

> Start with mixers and computers on Port 1, and move up from there on the network switch. 

Having a solid layout or fundamental system of organizing your network will make troubleshooting much easier, because you can visually tell which endpoints or systems are affected if things are laid out in an organized manner.
### Network Topology: Redundant

- Some Dante devices will have one Dante port, some will have two. 
- A second port typically defaults to "**Daisy Chain**" or "**Switched Mode**".
	- In this mode, both lead to the internal Dante network connection.
	- Only *one* needs to be connected to the switch.
	- The *second* remains available to daisy chain devices if necessary.

- The other mode it can be set to is ***Redundant***.
- When a device is set to Redundant mode, the second port connects to a totally independent Dante port, *with it's own IP address.*
- Each device is connected to an independent network, both of which will be run full-time.
	- If a device freezes or cable breaks, the connection is still maintained on the other network. 
### Network Topology: Review

### Network Connections: Control Ports

- Some Dante devices will have a control connection.
	- iPad control of mixer
	- DSP configuration
	- Beam Forming Mic Config
- Control may be offered as either a Discrete or Combined port
	- These are available often as a separate RJ45 port, but are sometimes merged into the primary connection.
	- This is why there are sometimes different IP address settings for each port. 
		- One goes to the Dante chipset, while the other goes to the control function that is maintained by the manufacturer.
### Setting a Static or DHCP IP On a Dante Device (Switched)

### Setting IP on a Device in Redundant Mode (Two Ports)

### Network Connections: Summary

- Dante devices can be connected in a daisy chain or through a switch.
	- For devices that have more than one port, you can chain them.
- Device Control ports might be separate or merged w Dante Primary.
	- For devices with control functions, like DSPs, mixers, beam forming mics, etc.

# Tour of Dante Controller

> Dante is managed with friendly names, not obscure numbers.
> 
> 	Devices have names, even channels can be labelled for easier reading. 
> 	These are not just for our benefit, they are used by the devices themselves. Every Dante receiver remembers the name of the Dante transmitter and the name of the channel they are supposed to pull in. 

- When setting up a system, *name first*, then make subscriptions. 
	- The names are used to remember subscriptions, not numbers or IP addresses. 

> Dante will prevent two devices with different sample rates from making a connection.

> You will **always want to set your names before making a subscription.**
> 
> If you change names after making a subscription, at the next reboot, devices may show this symbol indicating it cannot locate the device or channel, because it is looking for the old name. 

⚠️ - indicates that the mixer can't find the source device on the network.

🚫 - indicates that there is a sample rate mismatch between the two devices

You don't have to label *everything* on a Dante system.

On a stage where inputs change frequently, often times people will just label their devices and then leave the channels with their numbers. 

More permanent infrastructure like

- Mixed outputs
- DSP i/o
- amplifier channels

All benefit heavily from labelling. 

If Audinate Dante support is ever needed, it is recommended to send them three screenshots of:

- Device Info
- Clock Status
- Network Status
# Latency

### Introduction

> Latency is the amount of time it takes for a process to complete.
> 
> 	e.g. - the time from input to outputs of a digital system.

> The speed of sound is 343 m/sec (1125ft/sec)
### Deterministic Latency

> Dante devices allow you to determine latency performance. (.1msec/switch hop is safe.)

- Dante latency is imperceptible to presenters and performers alike.
- Dante latency describes the time from a transmitter accepting a signal until the receiver plays it out.

> A safe **rule of thumb** is 0.1msec per network switch "hop".

If two devices in a subscription have different default latency settings, the longer of the two will be used.

**Outcomes of Mixed Defauly Latencies**

| Transmitter | Receiver | Playout   |
| ----------- | -------- | --------- |
| 0.25 msec   |          | 0.50 msec |
| 0.50 msec   | .50 msec | 0.50 msec |
| 1.00 msec   |          | 1.00 msec |
### Verifying Performance in Dante Controller

**Dante Controller** can show you the latency performance of any connection. Receiving "Device View" -> Latency Tab

- Drummers can hear in headphones *before direct sound from their drum.*

- At 4K/60, Dante can deliver video from HDMI to HDMI in a half frame. 

### Dante Video: Perfect Lip Sync 

### Latency: Impeccable Frame Alignment

### Latency: Summary

- Everything has latency.
	- Even the speed of sound and speed of light are quantifiable. 

- Typical Dante latency is 1.00msec or less - down to .25msec.
	- This latency is not perceivable, seamless to presenter/performer. 
	- A good rule of thumb for modest systems is 0.1msec per switch hop.
	- If latency settings don't agree, it uses the longer of the Tx and Rx settings.

- Dante AV maintains lip sync, even though essences are separate.
	- The same latency is automatically negotiated for audio and video.
	- Dante AV automatically delays the audio to compensate for video codec latency.
	- Access to audio delay is provided in case *your venue* has a sync issue.

# Dante is Standard Networking

### Standard Wired Network Solutions: COTS Hardware

> Dante uses COTS hardware. COTS means "Commercial Off the Shelf"

#### No Special Hardware
#### No Special Firmware
#### No Special Settings

> Use managed and/or unmanaged switches.

### Standard Wired Network Solutions: Managed vs. Unmanaged

**Unmanaged Switches**

- Out-of-the-box, plug and play
- Sufficient for small, dedicated audio systems

**Managed Switches**

- Allows for traffic separation and optimization.
- Scalable for large networks and video deployments
- Interested? Continue to Level 2 after this class.

**Dante Works on Either Type**

- Dante designed to maximize unmanaged environments
- Dante offers hooks and tags for managed environments

## Switch Features to Look For
### 1Gbps or Faster

**1Gbit Speed (or better)**
- Provides capacity for higher channel counts
- Higher bandwidth improves clocking between devices.
### PoE

**Power over Ethernet**

- PoE powers devices through the Ethernet connection.
- Devices follow a standard, only pull required power.
- The "PoE Budget" lists the total power available.

| Year Ratified | Descriptor | Informal Name | Standard | Post-Supplied Power |
| ------------- | ---------- | ------------- | -------- | ------------------- |
| 2003          | Type 1     | PoE           | 802.3af  | 15W                 |
| 2009          | Type 2     | PoE+          | 802.3at  | 30W                 |
| 2018          | Type 3     | PoE++         | 802.3bt  | 60W                 |
| 2018          | Type 4     | PoE++         | 802.3bt  | 100W                |
> Reserve 20% power loss and some headroom. 
### PoE Budget Estimation

### Energy Efficient Ethernet (EEE) Disable

- Known by several names (Energy Efficient Ethernet, Green Ethernet, 802.3az)
- Intended to reduce energy consumption of network switches.
- Known to cause data interruptions, problematic for any real time network.
- If EEE is engaged, network may work most of the time, with random hiccups.
- Most switches have EEE, but many can disable it with a setting.

### About Neutrik etherCON Connections

- Neutrik etherCON connectors are standard RJ45 adding a rugged, locking "Cannon" shell.
- Normal Rj45 can connect to etherCON.

> **CAT5e or better is suggested.**
> 	CAT5e or better will deliver 1 Gbps at 100m lengths.
> 	Do not use CAT5, it was only rated for 100Mbps

| Cable | Tx Speed |
| ----- | -------- |
| CAT5  | 100Mbps  |
| CAT5e | 1Gbps    |
| CAT6  | 1Gbps    |
| CAT6A | 10Gbps   |

### Standard Wired Network Solutions: Cabling

> We can also use **Fiber Optics**.
> 	Fiber is appropriate for longer runs.
> 	300m is a typical starting point, some parts can go many kilometers.
### Wi-Fi is not Supported for Media Streams

> WiFi is less reliable and lower bandwidth than wired solutions.
> 	Not supported for DANTE audio/video streams
> 	Supported for Dante Controller: Control and Monitoring

There are wireless products that link to Dante...
### Core IP Settings: IP Address and Your Subnet

			**Devices in your subnet will be contacted locally.**

**subnet** - *the range of IP addresses found on your local network.*

| IP Address  | 192.168.0.101 |
| ----------- | ------------- |
| Subnet Mask | 255.255.255.0 |
| Subnet      | 192.168.0.___ |
| Gateway     | 192.168.0.1   |
### Core IP Settings: Local Address Ranges
> There are ranges of IP addresses available for use on your local network.

**Beginner's Safe Rule**: Do not end your IP address in 0 or 255.
### Core IP Settings: Automatic Addressing, Link Local

**Automatic Addressing:** Looks for DHCP Server. If none found, revert to Link Local. 

| IP          | Address         |
| ----------- | --------------- |
| IP Address  | 169.254.15.167  |
| Subnet Mask | 255.255.0.0     |
| Subnet      | 169.254.___.___ |
**Link Local**: Randomly picks an address in 169.254.___.___
### Networking: Summary

- Dante uses standard network switches and cabling.
	- No special firmware required - use your favorite brands.

- Dante can use managed or unmanaged switches.
	- Small, dedicated networks may not need configuration
	- If you need to join a managed network, Dante is prepared to do that, as well.
	- We suggest: 1Gbps or faster, Power over Ethernet (PoE), Disable EEE

- Dante media doesn't cross WiFi, but Dante Control does.
	- Different wireless technologies solve different wireless issues - use the right tool. 

- IP addressing ranges reserved for Local Area Networks
	- Safe rule: Don't end your IP address in 0 or 255.
	- IF DHCP server is not present, automatic addressing reverts to Link Local.

# Dante Links to a Computer

### Dante to a Computer: Dante Virtual Soundcard (DVS)

- Simple and Lean
	- No frills audio input/output

- Flexible Channel Count
	- Adjustable in Size from 2x2 to 64x64
	- ASIO (up to 64x64) or WDM (16x16)
	- Core Audio (up to 64x64)

- Low Latency
	- Great for DAWs and live performance

### Dante to a Computer: Dante Via

- Processing and Repatching
	- Route signal between objects in the computer
	- Take a Dante input to a USB Interface Output
	- Sample Rate Converts everything to 48kHz

- Dynamic Resizing
	- Expose and sound source or destination
	- 16x16 to any program or device, 32x32 in total.
		- ASIO (32x32) WDM (16x16)
		- Core Audio (up to 32x32)

- Medium Latency
	- The processing takes time.

### Dante to a Computer: Summary - DVS vs Dante Via

| Dante Virtual Soundcard           | Dante Via                      |
| --------------------------------- | ------------------------------ |
| Straight-Thru Interface, more I/O | Routing between audio objects  |
|                                   | Mixing Signals                 |
|                                   | Sample rate conversion         |
| Minimal Control/Set-Up            | Internal Routing Functionality |
| Low Latency                       | Modest Latency                 |
> A single computer can have DVS and Dante Via installed simultaneously.

**However, a single computer can only run one at a time.**

### Dante Application Library

> Software can include a virtual Dante interface built-in with DAL: *Dante Application Library*.
### Dante to a Computer... or a Mobile Device

| USB Type-C 2x2 I/O (24-bit 48kHz)      | USB Bluetooth 1x2 I/O (24-bit 48kHz)         |
| -------------------------------------- | -------------------------------------------- |
| Ideal for Smartphones and Tablets      | Stream Stereo audio wirelessly via Bluetooth |
| Provides USB 5V Power while connected  | Received or send audio from/to the Network   |
| Plug any device into the Dante Network | Use Bluetooth mic/speakers as Dante Tx/Rx    |
### Dante to a Computer: Professional Recording

### Dante to a Computer: Summary

- Dante virtual soundcard and Dante Via
	- Software that simulates a soundcard, use any 1Gbps wired port.

- Dante Application Library (DAL)
	- Dante virtual interface is built-in to some applications. 

- USB and Bluetooth I/O for computer or Mobile Devices
	- Better interfaces for Conferencing, Health Clubs and other Consumer Interfaces.

- Hardware Products for Professional Recording
	- Redundant network support, high channel counts and sample rates.

