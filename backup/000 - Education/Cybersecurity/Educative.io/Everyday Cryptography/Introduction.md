Get an introduction to cryptography, and explore the prerequisites and the intended audience for this course.

## What is Cryptography?

Cryptography is a subject with relevance to our everyday life that has undergone a dramatic transformation. Cryptography used to manifest itself in the public imagination through its historical use, primarily to protect military communications and through recreational puzzles. However, largely due to the development of computer networks, particularly the internet, most of us now use cryptography on a daily basis. 

Cryptography is fundamental to the wider notion of **Information Security**. Electronic information can easily be transmitted and stored in relatively insecure environments. This has resulted in fundamental changes to the risks to which information is exposed. As the financial impact of information security incidents rises, so does the need for information security protection and control.

Cryptography is a vital technology that underpins many of these controls. It provides a suite of basic mechanisms for implementing the security services that protect electronic information, such as confidentiality, data integrity, and authentication, also known as the **CIA Triad**.

---

Cryptography doesn't secure information on it's own, but many technical mechanisms for protecting information have cryptography at their core. That's why cryptography is an important subject for anyone with an interest in information security. There are also other reasons for the wide interest in cryptography as a subject, including the following:

- Cryptography plays an interesting political role. It's a key technology during times of conflict. Its modern use presents society with several *intriuging moral and political dilemmas*.
- Cryptography has a wide intrinsic appeal to the general public. Many people are fascinated by secrets and codes. This has been successfully exploited by the mainstream media.

## Why Choose this Course?

There are many books and courses on cryptography. What distinguishes the approach taken in this course is a combination of the following factors:

- **Fundamental Principles**: This course is intended to be both relevant and relatively timeless. It's easy to write a cryptography book or course that becomes out of date quickly. This course is intended to be just as relevant in ten year's time as it would have been ten years ago. We acheive this by concerning ourselves primarily with the fundamental principles rather than the technical details of the current tech.
- **Application-Focused**: This course is primarily concerned with the parts of cryptography that a user or practitioner of information security needs to know. While there is a great deal of contemporary theoretical research on cryptography, few of these ideas make it through to real-world applications, which tend to deploy only well-tested and understood techniques. This course focuses on cryptography for everyday applications.
- **Widely Accessible**: This course is intended to be suitable as a first read on cryptography. It focuses on core issues and provides an exposition of the fundamentals of cryptography.
- **Contextual Relevance**: This course focuses on cryptography as an underlying technology supporting information security in today's context rather than a topic in its own right.


> [!NOTE] Note
> This course deliberately doesn’t concentrate on the mathematical techniques underpinning cryptographic mechanisms. This course is intended to be introductory, self-contained, and widely accessible.

## Prerequisites

In this course, you’ll learn why cryptography is important, how it can be used, and what the main issues are regarding its implementation. You don’t need to have any prior knowledge of cryptography to benefit from this course. You also need almost no prior knowledge of mathematics. All you need is a desire to learn about cryptography. That is enough to make you eligible to take this course!

## Who should read this course?

The primary intended audiences are listed below.

### Users and practitioners of information security

Cryptography is a subject of relevance to anyone who needs to secure digital data. This course is intended to be of interest to:

- Information technology professionals who need to apply security techniques to data.
- Information security professionals whose role is to protect information.
- Managers of organizations who want to learn about the different issues concerning data security.
- General users of information technology who want to understand how to protect their data.

### Students of cryptography

This course may also be of interest to students studying the mathematics of cryptography since it complements more mathematical treatises by providing a kind of bridge between the theory of cryptography and the real-world problems it attempts to solve. For students who already know the how, this course will explain the why.

### General interest audience

This course has also been written in order to appeal to a general science or engineering audience who seeks a greater understanding of what cryptography is and how it works.

# Course Structure

Learn about the different parts of the course.

We'll cover the following

- [What to expect from this course?](https://www.educative.io/courses/everyday-cryptography/course-structure#What-to-expect-from-this-course)
- [Additional materials](https://www.educative.io/courses/everyday-cryptography/course-structure#Additional-materials)

## What to expect from this course?[](https://www.educative.io/courses/everyday-cryptography/course-structure#What-to-expect-from-this-course)

The following gives a brief overview of the contents of each chapter in this course:

- **Basic Principles**
    
    This chapter explains why cryptography is needed and identifies some of the core security services that cryptography can provide.
    
- **Historical Cryptosystems**
    
    This chapter provides an overview of historical encryption algorithms. Most of these are obsolete today, but they illustrate many of the core ideas as well as some basic encryption algorithm design principles.
    
- **Theoretical versus Practical Security**
    
    This chapter introduces the idea that unbreakable cryptosystems exist but are not practical in the real world. It also points out that most practical cryptosystems are breakable in theory. The real world is always about compromise. We argue that the study of cryptography is essentially the study of a toolkit of cryptographic primitives that can be assembled in different ways in order to achieve different security goals.
    
    > **Note:** The first three chapters basically provide the fundamental background needed for cryptography.
    
- **Symmetric Encryption**
    
    This chapter starts with a discussion about the provision of confidentiality. There are two types of cryptosystem, and we’ll look at the first of these, symmetric encryption, with respect to providing confidentiality. This chapter also discusses the different types of symmetric encryption algorithms as well as the different ways in which they can be used.
    
- **Public-Key Encryption**
    
    This chapter introduces the concept of public-key encryption. It explains the reasons for using public-key encryption and discusses two important public-key cryptosystems in some detail.
    
- **Data Integrity**
    
    This chapter introduces the kind of symmetric cryptography that can be used to provide data integrity and stronger data origin authentication.
    
- **Digital Signature Schemes**
    
    This chapter outlines cryptographic techniques that provide non-repudiation.
    
- **Entity Authentication**
    
    This chapter explains how cryptography can be used to provide entity authentication. It also considers random number generation, which is often required for entity authentication mechanisms.
    

Exploring the concept of authentication

- **Cryptographic Protocols**
    
    This chapter explains how these cryptographic primitives can be combined to form cryptographic protocols.
    
    > **Note:** The chapters mentioned above explore the various components that make up the cryptographic toolkit. This includes cryptographic primitives and the cryptographic protocols that combine them.
    
- **Key Management**
    
    This chapter discusses the concept of key management in general terms, focusing on the management of secret keys. It studies the life cycle of a cryptographic key and discusses some of the most common techniques for conducting the various phases of this life cycle.
    
- **Public-Key Management**
    
    This chapter introduces the issues of key management, particularly as it relates to public-key cryptography. Key management is arguably the most important and often overlooked area of cryptography from a practical perspective. It underpins the security of any cryptographic system and is the aspect of cryptography where practitioners are most likely to become involved in decision-making.
    
    > **Note:** In the chapters named above, we explore what is arguably the most important, and often overlooked, area of cryptography from a practical perspective: key management. This underpins the security of any cryptographic system and is the aspect of cryptography where users and practitioners are most likely to become involved in decisions concerning cryptography.
    
- **Cryptographic Applications**
    
    This chapter reinforces the lessons from the previous chapters by looking at some applications of cryptography in detail. Since many of the issues raised in the previous chapters require application-dependent decisions to be made before cryptography can be implemented, we demonstrate how several important applications of cryptography actually address these issues. In particular, we discuss why particular cryptographic primitives are used and how key management is conducted.
    
- **Cryptography for Personal Devices**
    
    This chapter talks about how users often inadvertently use cryptography when securing their personal devices and communications.
    

Cryptography and personal devices

- **Control of Cryptography:**
    
    This chapter looks at wider societal issues raised through the use of cryptography and considers strategies for balancing privacy and control.
    
    > **Note:** The final three chapters explore the usage of cryptography and some predicaments that come along with cryptography.
    

## Additional materials[](https://www.educative.io/courses/everyday-cryptography/course-structure#Additional-materials)

This course also offers the following additional features:

- **Further reading:** Each chapter includes a brief summary of resources that can be used to further pursue the topics discussed. These are only intended to be starting points and are by no means comprehensive. These resources are normally a mix of accessible reading, important research articles, relevant standards, and useful web links. Carefully directed web searches should also prove an effective means of finding further information.
    
- **Quizzes:** Each chapter contains quiz questions designed to enhance the understanding of the chapter contents.
    
- **Mathematics Appendix:** Finally, there is a short appendix at the end of the course that contains some elementary background mathematics that complement the contents of this course. This appendix is intended for those who want to learn about the mathematical aspects of cryptography and is optional reading for the completion of this course.