#tryhackme #cybersecurity101 #cryptography 
# Introduction

Have you ever wondered how to prevent third parties from reading your messages? How can your app or web browser build a secure channel with a remote server? By secure, we mean that no one can read or alter the exchanged data; furthermore, we can be confident that we are connecting with the real server. Thanks to cryptography, these requirements are satisfied.

Cryptography lays the foundation for our digital world. While networking protocols have made it possible for devices spread across the globe to communicate, cryptography has made it possible to trust this communication.

This room is the first of three introductory rooms about cryptography. There are no learning prerequisites except basic abilities to use the Linux command line. If you are not sure, please consider joining the [Pre Security](https://tryhackme.com/r/path/outline/presecurity) path.

- Cryptography Basics (this room)
- [Public Key Cryptography Basics](https://tryhackme.com/r/room/publickeycrypto)
- [Hashing Basics](https://tryhackme.com/r/room/hashingbasics)
## Learning Objectives

Upon completing this room, you will learn the following:

- Cryptography key terms
- Importance of cryptography
- Caesar Cipher
- Standard symmetric ciphers
- Common asymmetric ciphers
- Basic mathematics commonly used in cryptography
# Importance of Cryptography

Cryptography's ultimate purpose is to ensure *secure communication in the presence of adversaries*. The term secure includes confidentiality and integrity of the communicated data. Cryptography can be defined as the practice and study of techniques for secure communication and data protection where we expect the presence of adversaries and third parties. In other words, these adversaries should not be able to disclose or alter the contents of the messages.

Cryptography is used to protect confidentiality, integrity and authenticity. In this age, you use cryptography daily, and you're almost certainly reading this over an encrypted connection. Consider the following scenarios where you would use cryptography:

- When you log into TryHackMe, your credentials are encrypted and sent to the server so that no one can retrieve them by snooping on your connection. 
- When you connect over SSH, your SSH client and the server establish an encrypted tunnel so no one can eavesdrop on your session.
- When you conduct online banking, your browser checks if the remote server's certificate to confirm that you are communicating with your bank's server and not an attackers.
- When you download a file, how do you check if the file was downloaded correctly? Cryptography provides a solution through **hash functions** to confirm that your file is identical to the original one.

As you can see, you rarely have to interact directly with cryptography, but is solutions and implications are everywhere in the digital world. Consider the case where a company wants to handle credit card information and process related transactions. 

When handling credit cards, the company must follow and enforce the Payment Card Industry Data Security Standard (PCI DSS). In this case, the PCI DSS ensures a minimum level of security to store, process and transmit data related to credit cards. If you check the [PCI DSS for Large Organizations](https://www.pcisecuritystandards.org/documents/PCI_DSS_for_Large_Organizations_v1.pdf), you will learn that the data should be encrypted both while being stored (at rest) and while being transmitted (in motion).

In the same way that handling payment card details requires complying with PCI DSS, handling medical records requires complying with their respective standards. Unlike credit cards, the standards for handling medical records vary from one country to another. Example laws and regulations that should be considered when handling medical records include HIPAA (Health Insurance Portability and Accountability Act) and HITECH (Health Information Technology for Economic and Clinical Health) in the USA, GDPR (General Data Protection Regulation) in the EU, DPA (Data Protection Act) in the UK. 

Although this list is not exhaustive, it gives an idea about the legal requirements that healthcare providers should consider depending on their country. These laws and regulations show that cryptography is a necessity that should be present yet usually hidden from direct user access.
# Plaintext to Ciphertext

Let's start an illustration before introducing key terms. We begin with the plaintext that we want to encrypt. The plaintext is readable data; it can be anything from simple text, a cat photo, credit card information, or medical health records. From a cryptography perspective, these are all "plaintext" messages waiting to be encrypted. The plaintext is passed through the encryption function along with a proper key; the encryption function returns a ciphertext. The encryption is part of the cipher; a cipher is an algorithm to convert a plaintext into a ciphertext and vice versa.

![](https://i.imgur.com/drhxLOh.png)

To recover the plaintext, we must pass the ciphertext along with the proper key via the decryption function, which would give us the original plaintext. This is shown in the illustration below.

![](https://i.imgur.com/pCLLApV.png)

We have just introduced several new terms, and we need to learn them to understand any text about cryptography. The terms are listed below:

- `plaintext` is the original, readable message or data before it is encrypted. It can be a document, an image, a multimedia file, or any other binary data.
- `ciphertext` is the scrambled, unreadable version of the message after encryption. Ideally, we cannot get any information about the original plaintext except its approximate size. 
- `cipher` is an algorithm or method to convert the plaintext into ciphertext and back again. A cipher is usually developed my a **mathematician**.
- `key` is a string of bits the cipher uses to encrypt or decrypt data. In general, the used cipher is public knowledge; however, the key must remain secret unless it is the public key in asymmetric encryption. We will visit asymmetric encryption in a later task.
- `encryption` is the process of converting plaintext into ciphertext using a cipher and a key. Unlike the key, the choice of the cipher is disclosed. 
- `decryption` is the reverse process of encryption, converting ciphertext back into plaintext using a cipher and a key. Although the cipher would be public knowledge, recovering the plaintext without knowledge of the key should be impossible.
# Historical Ciphers

