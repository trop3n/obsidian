#cryptography #tryhackme #securityenginnerpath 

# Introduction

The purpose of this room is to introduce users to basic cryptography concepts such as:

- Symmetric Encryption, such as AES
- Asymmetric Encryption, such as RSA
- Diffie-Hellman Key Exchange
- Hashing
- PKI

Suppose you want to send a message that no one can understand except the intended recipient. How would you do that?

One of the simplest ciphers is the Caeasr Cipher, used more than 2000 years ago. Caesar Cipher shifts the letter by a fixed number of places to the left or to the right. Consider the case of shifting by three to the right to encrypt, as shown in the figure below. 

![](https://i.imgur.com/kOZlvJ7.png)

The recipient needs to know that the text was shifted by three to the right to recover the original message.

![](https://i.imgur.com/tXBWGku.png)

Using the same key to encrypt “TRY HACK ME”, we get “WUB KDFN PH”.

The Caesar Cipher that we have described above can use a key between 1 and 25. With a key of 1, each letter is shifted by one position, where A becomes B, and Z becomes A. With a key of 25, each letter is shifted by 25 positions, where A becomes Z, and B becomes A. A key of 0 means no change; moreover, a key of 26 will also lead to no change as it would lead to a full rotation. Consequently, we conclude that Caesar Cipher has a keyspace of 25; there are 25 different keys that the user can choose from.

Consider the case where you have intercepted a message encrypted using Caesar Cipher: “YMNX NX FQUMF GWFAT HTSYFHYNSL YFSLT MTYJQ RNPJ”. We are asked to decrypt it without knowledge of the key. We can attempt this by using brute force, i.e., we can try all the possible keys and see which one makes the most sense. In the following figure, we noticed that key being 5 makes the most sense, “THIS IS ALPHA BRAVO CONTACTING TANGO HOTEL MIKE.”

![](https://i.imgur.com/t2JwwSe.png)

Caesar Cipher is considered a **substitution cipher** because each letter in the alphabet is substituted with another.

Another type of cipher is called **transposition cipher**, which encrypts the message by changing the order of the letters. Let's consider a simple transposition cipher in the figure below. We start with the message, "THIS IS ALPHA BRAVO CONTACTING TANGO HOTEL MIKE", and the key `42351`. 

After we write the letters of our message by filling one column after another, we rearrange the columns based on the key and then read the rows. In other words, we write by columns and we read by rows. Also notice that we ignored all the space in the plaintext in this example. The resulting ciphertext "NPCOTGHOTH" is read one row after the other. In other words, a transposition cipher simply rearranges the order of the letters, unlike the substitution cipher, which substitutes the letters without changing their order. 

![](https://i.imgur.com/3sw49LE.png)

This task introduced simple substitution and transposition ciphers and applied them to messages made of alphabetic characters. For an encryption algorithm to be considered **secure**, it should be infeasible to recover the original message, i.e. plaintext. (In mathematical terms, we need a **hard** problem, i.e. a problem that cannot be solved in polynomial time.) A problem that we can solve in polynomial time is a problem that's feasible to solve even for large input, although it might take the computer quite some time to finish.

If the encrypted message can be broken in one week, the encryption used would be considered insecure. However, if the encrypted message can be broken in 1 million years, the encryption would be considered *practically secure*. 

Consider the mono-alphabetic substitution cipher, where each letter is mapped to a new letter. For example, in English, you would map “a” to one of the 26 English letters, then you would map “b” to one of the remaining 25 English letters, and then map “c” to one of the remaining 24 English letters, and so on.

For example, we might choose the letters in the alphabet “abcdefghijklmnopqrstuvwxyz” to be mapped to “xpatvrzyjhecsdikbfwunqgmol” respectively. In other words, “a” becomes “x”, “b” becomes “p”, and so on. The recipient needs to know the key, “xpatvrzyjhecsdikbfwunqgmol”, to decrypt the encrypted messages successfully.

This algorithm might look very secure, especially since trying all the possible keys is not feasible. However, different techniques can be used to break a ciphertext using such an encryption algorithm. One weakness of such an algorithm is letter frequency. In English texts, the most common letters are ‘e’, ‘t’, and ‘a’, as they appear at a frequency of 13%, 9.1%, and 8.2%, respectively. Moreover, in English texts, the most common first letters are ‘t’, ‘a’, and ‘o’, as they appear at 16%, 11.7% and 7.6%, respectively. Add to this the fact that most of the message words are dictionary words, and you will be able to break an encrypted text with the alphabetic substitution cipher in no time.

We don’t really need to use the encryption key to decrypt the received ciphertext, “Uyv sxd gyi siqvw x sinduxjd pvzjdw po axffojdz xgxo wsxcc wuidvw.” As shown in the figure below, using a website such as [quipqiup](https://www.quipqiup.com/), it will take a moment to discover that the original text was “The man who moves a mountain begins by carrying away small stones.” This example clearly indicates that this algorithm is broken and should not be used for confidential communication.
# Symmetric Encryption

Let's review some terminology:

- **Cryptographic Algorithm** or **Cipher**: This algorithm defines the encryption and decryption process. 
- **Key**: The cryptographic algorithm needs a key to convert the plaintext into ciphertext and vice versa. 
- **plaintext** is the original message we want to encrypt
- **ciphertext** is the message in its encrypted form

A symmetric encryption algorithm uses the same key for encryption and decryption. Consequently, the communicating parties need to agree on a secret key before being able to exchange any messages.

In the following figure, the sender provides the *encrypt* process with the plaintext and the key to get the ciphertext. The ciphertext sent over some communication channel.

![](https://i.imgur.com/95wlVba.png)

On the other end, the recipient provides the *decrypt* process with the same key used by the sender to recover the original plaintext from the received ciphertext. Without knowledge of the key, the recipient won't be able to recover the plaintext.

![](https://i.imgur.com/ey1KKWW.png)

National Institute of Standards and Technology (NIST) published the `Data Encryption Standard (DES)` in 1977. DES is a symmetric encryption algorithm that uses a key size of 56 bits. In 1997, a challenge to break a message encrypted using DES was solved. Consequently, it was demonstrated that it had become feasible to use a brute-force search to find the key and break a message encrypted using DES. In 1998, a DES key was broken in 56 hours. These cases indicated that DES could no longer *be considered secure*. 

NIST published the Advanced Encryption Standard (AES) in 2001. Like DES, it is a symmetric encryption algorithm; however, it uses a key size of 128, 192 or 256 bits, and it is still considered secure and in use today. AES repeats the following four transformations multiple times:

1. `SubBytes(state)`: this transformation looks up each byte in a given substitution table (S-box) and substitutes it with the respective value. The `state` is 16 bytes, i.e. 128 bits, saved in a 4 by 4 array.
2. `ShiftRows(state)`: The second row is shifted by one place, the third row is shifted by two places, and the fourth row is shifted by three places. This is shown in the figure below. 
3. `MixColumns(state)`: Each column is multiplied by a fixed matrix (4 by 4 array.
4. `AddRoundKey(state)`: A round key is added to the state using the XOR operation.

![](https://i.imgur.com/4WEsFaP.png)

The total number of transformation rounds depends on the key size. 

Don't worry if you find this cryptic because it is. Our purpose is not to learn the details of how AES works nor to implement it as a programming library; the purpose is to appreciate the difference in complexity between ancient encryption algorithms and modern ones. If you are curious to dive into details, you can check the AES specification, including pseudocode and example in its published standard, [FIPS PUB 197](https://csrc.nist.gov/publications/detail/fips/197/final).

> In addition to AES, many other symmetric encryption algorithms are considered secure. Here is a list of symmetric encryption algorithms supported by GPG (GnuPG) 2.37.7, for example:

| **Encryption Algorithm**              | **Notes**                                                                                                                              |
| ------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| AES, AES192, AES256                   | AES with a key size of 128, 192 and 256 bits                                                                                           |
| IDEA                                  | International Data Encryption Algorithm (IDEA)                                                                                         |
| 3DES                                  | Triple DES (Data Encryption Standard) and is based on DES. We should note that 3DES will be deprecated in 2023 and disallowed in 2024. |
| CAST5                                 | Also known as CAST-128. Some sources state that CAST stands for the names of it's authors: Carlisle Adams and Stafford Tavares.        |
| BLOWFISH                              | Designed by Bruce Schneier                                                                                                             |
| TWOFISH                               | Designed by Bruce Schneier and derived from Blowfish.                                                                                  |
| CAMELLIA128, CAMELLIA192, CAMELLIA256 | Designed by Mitsubishi Electric and NTT in Japan. Its name is derived from the flower camellia japonica.                               |
All the algorithms mentioned so far are block cipher symmetric encryption algorithms. A block cipher algorithm converts the input (plaintext) into blocks and encrypts each block. A block is usually 128 buts. In the figure below, we want to encrypt the plaintext "TANGO HOTEL MIKE", a total of 16 characters. The first step is to represent it in binary. If we use ASCII, "T" is `0x54` in hexadecimal format, "A", is `0x41`, and so on. Every two hexadecimal digits constitute 8 bits and represent one byte. A block of 128 bits is practically 16 bytes and is represented in a 4 by 4 array. The 128-bit block is fed as one unit to the encryption method.

![](https://i.imgur.com/bTeYz5T.png)

The other type of symmetric encryption algorithm is stream ciphers, which encrypt the plaintext byte by byte. Consider the case where we want to encrypt the message "TANGO HOTEL MIKE"; each character needs to be converted to its binary representation. If we use ASCII, "T" is in hexadecimal, while "A" is `0x41`, and so on. The encryption method will process one byte at a time. This is represented in the figure below.

![](https://i.imgur.com/GNlarZZ.png)

Symmetric encryption solves many security problems discussed in the [Security Principles](https://tryhackme.com/room/securityprinciples) room. Let's say that Alice and Bob met and chose an encryption algorithm and agreed on a specific key. We assume that the selected encryption algorithm is secure and that the secret key is kept safe. Let's take a look at what we can achieve:

- **Confidentiality**: If Eve intercepted the encrypted message, she wouldn't be able to recover the plaintext. Consequently, all messages exchanged between Alice and Bob are confidential as long as they are sent encrypted. 
- **Integrity**: When Bob receives an encrypted message and decrypts it successfully using the key he agreed upon with Alice, Bob can be sure that no one could tamper with the message across the channel. When using secure modern encryption algorithms, any minor modification to the ciphertext would prevent successful decryption or would lead to gibberish as plaintext.
- **Authenticity**: Being able to decrypt the ciphertext using the secret key also proves the authenticity of the exchanged messages. More practical and efficient approaches will be presented in later tasks. The question, for now, is whether this is scalable.

With Alice and Bob, we need one key. If we have Alice, Bob and Charlie, we need three keys: one for Alice and Bob, another for Alice and Charlie, and a third for Bob and Charlie. However, the number of keys grows quickly; communication between 100 users requires almost 5000 different secret keys. (If you are curious about the mathematics behind it, that's 99 + 98 + 97 + ... + 1 = 4950).

Moreover, if one system gets compromised, they need to create new keys to be used with the other 99 users. Another problem would be finding a secure channel to exchange the keys with all the other users. Obviously, this quickly grows out of hand. 

In the next task, we will cover *asymmetric encryption*. One of the problems solved with asymmetric encryption is when 100 users only need to share a total of 100 keys to communicate securely. (As explained earlier, symmetric encryption would require around 5000 keys to secure the communications for 100 users).

> There are many programs available for symmetric encryption. We will focus on two, which are widely used for asymmetric encryption as well:

- GNU Privacy Guard
- OpenSSL Project
## GNU Privacy Guard

> The [GNU Privacy Guard](https://gnupg.org/), also known as GnuPG or GPG, implements the OpenPGP standard.

We can encrypt a file using GnuPG (GPG) using the following command:

`gpg --symmetric --cipher-algo CIPHER message.txt`, where CIPHER is the name of the encryption algorithm. You can check supported ciphers using the command `gpg --version`. For exampl,e `gpg --armor --symmetric --cipher-algo CIPHER message.txt`.

You can decrypt using the following command.

`gpg --output original_message.txt --decrypt message.gpg`
## OpenSSL Project

The [OpenSSL Project](https://www.openssl.org/) maintains the OpenSSL software.

We can encrypt a file using OpenSSL using the following command:

`openssl aes-256-cbc -e -in message.txt -out encrypted_message`

We can decrypt the resulting file using the following command:

`openssl aes-256-cbc -d -in encrypted_message -out original_message.txt`

To make the encryption more secure and resilient against brute-force attacks, we can add `-pbkdf2` to use the Password-Based Key Derivation Function 2 (PBKDF2); moreover, we can specify the number of iterations on the password to derive the encryption key using `-iter NUMBER`. To iterate 10,000 times, the previous command would become:

`openssl aes-256-cbc -pbkdf2 -iter 10000 -e -in message.txt -out encrypted_message`

Consequently, the decryption command becomes:

`openssl aes-256-cbc -pbkdf2 -iter 10000 -d -in encrypted_message -out original_message.txt`

In the following questions, we will use `gpg` and `openssl` on the AttackBox to carry out symmetric encryption.

The necessary files for this task are located under `/root/Rooms/cryptographyintro/task02`. **The zip file attached to this task can be used to tackle the questions of tasks 2, 3, 4, 5, and 6**.

