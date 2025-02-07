#tryhackme #DFIR #digitalforensics #cybersecurity 
# Introduction to Digital Forensics

Forensics is the application of methods and procedures to investigate and solve crimes. The branch of forensics that investigates cyber crimes is known as **digital forensics**. **Cyber crime** is any criminal activity conducted on or using a digital device. Several tools and techniques are used to investigate digital devices thoroughly after any crime to find and analyze evidence for necessary legal action. 

Digital devices have solved many of our problems. Communication all around the globe is just a matter of a text or call. Due to the vast usage of digital devices, besides making life easier, an increase in digital crimes -- cyber crimes has also been observed. A variety of crimes are committed using digital devices.

Consider an example where law enforcement agencies raid a bank robber's place with proper search warrants. Some digital devices, including a laptop, mobile phone, hard drive and USB, were found in the robber's home. The law enforcement agency handed over the case to the digital forensics team. The team collected evidence securely and conducted a thorough investigation inside their digital forensics lab equipped with forensics tools. The following evidence was found on the digital devices:

- A digital map of the bank was found on the suspect's laptop, which they kept for planning the robbery. 
- A document with the bank's entrance and escape routes was found on the suspect's hard drive. 
- A document on the hard drive that listed all the bank's physical security controls. The suspect devised plans to bypass the security measures.
- Some media files, including photos and videos of the suspect's previous robberies, were inside the suspect's laptop. 
- After conducting a thorough investigation of the suspect's mobile phone, some illegal chat groups related to the bank robbery were also found.

![](https://i.imgur.com/ZLjx7tU.png)
All this evidence helped law enforcement in the legal proceedings of the case. This scenario discusses a case from the start till the end. Some procedures are followed by the digital forensics team while collecting the evidence, storing it, analyzing it, and reporting it. This room will focus on covering the understanding of these procedures. The following are the learning objectives of this room:
### Learning Objectives

- Phases of digital forensics
- Types of digital forensics
- Procedure of evidence acquisition
- Windows forensics
- Solving a forensics case
# Digital Forensics Methodology

The digital forensics team has various cases requiring different tools and techniques. However, the National Institute of Standards and Technology (NIST) defines a general process for every case. The NIST works on defining frameworks for different areas of technology, including cybersecurity, where they introduce the process of digital forensics in four phases:

![](https://i.imgur.com/yQrhCEX.png)
1. **Collection**: The first phase of digital forensics is data collection. Identifying all the devices from which the data can be collected is essential. Usually, an investigator can find personal computers, laptops, digital cameras, USBs, etc. on the crime scene. It is also necessary to ensure the original data is not tampered with while collecting the evidence and to maintain a proper document containing the collected items' details. We will also discuss the evidence-acquisition procedures in the upcoming tasks. 
2. **Examination**: The collected data may overwhelm investigators due to it's size. This data usually needs to be filtered, and the data of interest needs to be extracted. For example, as an investigator, you collected the media files from a digital camera on the crime scene. You may only require some of the media as you are concerned with the media recorded on a specific time or date. So, in the examination phase, you would filter the media files of the required time and move them to the next phase. Similarly, you may only need to data of a specific user from a system containing numerous user accounts. The examination phase helps you filter this particular data for analysis.
3. **Analysis**: This is a critical phase. The investigators now have to analyze the data by correlating it with multiple pieces of evidence to draw conclusions. The analysis depends upon the case scenario and available data. The analysis aims to extract the activities relevant to the case chronologically. 
4. **Reporting**: The last phase of digital forensics, a detailed report is prepared. This report contains the investigation's methodology and detailed finding from the collected evidence. It may also contain recommendations. This report is presented to law enforcement and executive management. It is important to include executive summaries as part of the report, considering the level of understanding of all the receiving parties. 

As part of the collection phase, we saw that various pieces of evidence can be found at the crime scene. Analyzing these multiple categories of evidence requires various tools and techniques. There are different types of digital forensics, all with their own collection and analysis methodologies. Some of the most common types are listed below. 

![](https://i.imgur.com/8LqKRHw.png)
- **Computer Forensics**: The most common type of digital forensics is computer forensics, which concerns investigating computers, the devices most commonly used in crimes. 
- **Mobile Forensics**: Mobile forensics involves investigating mobile devices and extracting evidence such as call records, text messages, GPS locations, and more.
- **Database Forensics**: Many critical data is stored in dedicated databases. Database forensics investigates any intrusion into these databases that results in data modification or exfiltration.
- **Cloud Forensics**: Cloud forensics is the type of forensics that involves investigating data stored on cloud infrastructure. This type of forensics sometimes gets tricky for the investigators as there is little evidence on cloud infrastructures.
- **Email Forensics**: Email, the most common communication method between professionals, has become an important part of digital forensics. Emails are investigated to determine whether they are part of phishing or fraudulent campaigns. 
# Evidence Acquisition

Acquiring evidence is a critical job. The forensics team must collect all the evidence securely without tampering with the original data. Evidence acquisition methods for digital devices depend on the type of digital device. However, some general practices must be followed while the evidence is acquired. Let's discuss some of the important ones. 
## Proper Authorization

The forensics teams should obtain authorization from the relevant authorities before collecting any data. Evidence collected without prior approval may be deemed inadmissible in court. Forensic evidence contains private and sensitive data of an organization or individual. Proper authorization before collecting this data is *essential* for investigating according to the limits of the law. 
## Chain of Custody

Imagine that a team of investigators collects all the evidence from the crime scene, and some of the evidence goes missing after a few days, or there is a change in the evidence. No individual can be held accountable in this scenario because there is no proper process for documenting the evidence owners. This problem can be solved by maintaining a chain of custody document. A chain of custody is a formal document containing all the details of the evidence. Some of the key details are listed below:

- Description of the evidence (name, type).
- Name of individuals who collected the evidence. 
- Date and time of evidence collection. 
- Storage location of each piece of evidence.
- Access times and the individual record who accessed the evidence. 

This creates a proper trail of evidence and helps preserve it. The chain of custody document can be used to prove the integrity and reliability of the evidence admitted in court. A sample chain of custody can be downloaded from **[here](https://www.nist.gov/document/sample-chain-custody-formdocx)**.
## Use of Write Blockers

Write blockers are an essential part of the digital forensics team's toolbox. Suppose you are collecting evidence from a suspect's hard drive and attaching the hard drive to the forensics workstation. While the collection occurs, some background tasks in the forensic workstation may alter the timestamps of the files on the hard drive. This can cause hindrances during the analysis, ultimately producing incorrect results. Suppose the data was collected from the hard drive using a write blocker instead in the same scenario. This time, the suspect's hard drive would remain in its original state as the write blocker can block any evidence alteration actions. 
# Windows Forensics

The most common types of evidence collected from crime scenes are desktop computers and laptops, as most criminal activity involves a personal system. These devices have different operating systems running on them. In this task, we will discuss the evidence acquisition and analysis of the Windows operating system, which is a very common operating system that has been investigated in several cases.

As part of the data collection phase, forensic images of the Windows operating system are taken. These forensic images are bit-by-bit copies of the whole operating system. Two different categories of forensic images are taken from a Windows operating system. 

- **Disk Image**: The disk image contains all the data present on the storage device of the system (HDD, SSD, etc). This data is non-volatile, meaning that the disk data would survice even after a restart of the operating system. For example, all the files like media, documents, internet browsing history, and more. 

- **Memory Image**: The memory image contains the data inside the operating system's RAM. This memory is volatile, meaning the data will get lost after the system is powered off or restarted. For example, to capture open files, running processes, current network connections, etc. the memory image should be prioritized and taken first from the suspect's operating system; otherwise any restart or shutdown of the system would result in all the volatile data getting deleted. While carrying out digital forensics on a Windows operating system, disk and memory images are very important to collect. 

Let's discuss some popular tools used for disk and memory image acquisition and analysis of the Windows operating system.

**FTK Imager**: FTK Imager is a widely used tool for taking disk images of Windows operating systems. It offers a user-friendly graphical interface for creating the image in various formats. This tool can also analyze the contents of a disk image. It can be used for both acquisition and analysis purposes.

![](https://i.imgur.com/7ujJ1FZ.png)

**Autopsy**: [Autopsy](https://www.autopsy.com/) is a popular open-source digital forensics platform. An investigator can import an acquired disk image into this tool, and the tool will conduct an extensive analysis of the image. It offers various features during image analysis, including keyword search, deleted file recovery, file metadata, extension mismatch detection, and many more.

![](https://i.imgur.com/GR9KRd3.png)

**DumpIt**: [DumpIt](https://www.toolwar.com/2014/01/dumpit-memory-dump-tools.html) offers the utility of taking a memory image from a Windows operating system. This tool creates memory images using a command-line interface and a few commands. The memory image can also be taken in different formats.

**Volatility:** [Volatility](https://volatilityfoundation.org/) is a powerful open-source tool for analyzing memory images. It offers some extremely useful plugins. Each artifact can be analyzed using a specific plugin. This tool supports various operating systems, including Windows, Linux, macOS, and Android.

![](https://i.imgur.com/t1ak48Y.png)
**Note:** Various other tools are also used to acquire and analyze disk and memory images of the Windows operating system.

