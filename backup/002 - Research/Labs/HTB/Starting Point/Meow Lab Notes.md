#hackthebox #labs 

blob:https://app.hackthebox.com/8689b06d-57ed-481b-90be-bd5880d2acfb
# Introduction

When first starting a penetration test or any security evaluation on a target, a primary step is known as `Enumeration`. This step consists of documenting the current state of the target to learn as much as possible about it.

Since you are now on the same VPN as the target, you can directly access it as any user would. If the target is a web server, running a public web page, you can navigate to its IP address to see what the page contains. If the target is a storage server, you can connect to it using the same IP address to explore the files and folders stored on it, provided you have the *necessary credentials*.

The question is, how do you find these services? You cannot manually search for them because it would take a long time. 

Every server uses `ports` in order to serve data to other clients. The first steps in the Enumeration process involve scanning these open ports to see the purpose of the target on the network and what potential vulnerabilities might appear from the services running on it. In order to quickly scan for ports, we can use a tool called `nmap`, which we will detail more in the Enumeration chapter of this write up.

After finding the open ports on the target, we can manually access each of them using different tools to find out if we have access to their contents or not. Different services will use different tools or script to be accessed. These can be discovered and learned by a beginner penetration tester only with time and practice (and some diligent googling). 90% of penetration testing consists of research done on the internet about the product you are testing. Since the technological ecosystem is continuously evolving, it is impossible to know everything about everything. The key is to *know how to look for the information you need*. The ability to research effectively is the *skill you need to continuously adapt and evolve into your top quality*.

The objective here is not speed, but **meticulousness**. If a resource on the target is missed during the enumeration phase of your test, you might lose a vital attack vector which would have potentially cut your worktime on the target in half or even less. 

---
## Enumeration

After our VPN connection is successfully established, we can ping the target's IP address to see if our packets reach their destination. You can take the IP address of your current target from the Starting Point lab's page and paste it into your terminal after typing in the ping command as illustrated below.

![](https://i.imgur.com/Clygwwx.png)

After four successful replies from the target, we can determine that our connection is formed and stable. We can cancel the ping command by pressing the `CTRL+C` combination on our keyboard, which will be displayed in the terminal as `^C` marked above in green. 

This will return control of the terminal tab to us, from where we can proceed with the next step - scanning all of the target's open ports to determine the services running on it. In order to start the scanning process, we can use the following command with the `nmap` script. `namp` stands for **Network Mapper**, and it will send requests to the target's ports in hopes of receiving a reply, thus determining if the said port is open or not. Some ports are used by default by certain services. Others might be **non-standard**, which is why we will be using the `service detection flag ` `-sV` to determine the name and description of the identified services. The text marked in green and curly brackets `{}` is a replacement for your own version of input. In this case, you will need to replace the `{target ip}` part with the IP address of your own target. 

![](https://i.imgur.com/BjR3yV1.png)

Following the completion of the scan, we have identified `port 23/tcp` in an `open` state, running the `telnet` service. Following a quick google search of this protocol, we find out that telnet is an old service used for **remote management of other hosts** on the network. Since the target is running this service, it can receive telnet connection requests from other hosts in the network (such as ourselves). Usually, connection requests through telnet are configured with `username/password` combinations for increased security.

We can see this is the case for our target, as we are met with a Hack The Box banner and a request from the target to authenticate ourselves before being allowed to proceed with remote management of the target host.

![](https://i.imgur.com/FzSgnFu.png)

We will need to find out some credentials that work to continue since there are no other ports open on the target that we could explore.

---
## Foothold

Sometimes, due to configuration mistakes, some important accounts can be left with blank passwords for the *sake of accessibility*. This is a **significant issue with some network devices** or hosts, leaving them open to simple brute-forcing attacks, where the attackers can try logging in sequentially, using a list of usernames with no password input. 

Some typical important accounts have self-explanatory names such as:

- `admin`
- `administrator`
- `root`

A direct way to attempt logging in with these credentials in hopes that one of them exists and has a blank password is to input them manually in the terminal when the hosts request them., If the list were longer, we could use a script to automate this process, feeding it a `wordlist` for usernames and one for passwords. Typically, the wordlists used for this task consist of typical  people names, abbreviations, or data from previous database leaks. For now, we can resort to manually trying these three main usernames above.

![](https://i.imgur.com/AkKRdr4.png)

The first two were unsuccessful. When things look down, *it is essential to keep going*, *be persistent*. We can't succeed unless we attempt all possibilities. Let us try the last one.

![](https://i.imgur.com/dXqWEhT.png)

Success! We have logged into the target system. We can now go ahead and take a look around the directory we landed in using the `ls` command. There is a possibility we might find what we are looking for.

![](https://i.imgur.com/a3vhTGt.png)

The `flag.txt` file is our target in this case. Most of Hack The Box's targets will have one of these files, which will contain a hash value called `a flag`. The naming convention for these targeted files varies from lab to lab. 
	For example, weekly and retired machines will have two flags, namely `user.txt` and `root.txt`. CTF targets and other labs will have `flag.txt`. Challenges will, most of the time, not contain an actual file, but rather offer you snippets of the flag as you solve it, the respective parts being embedded into the challenge more homogeneously (text hidden in an image, or other examples).

You can read the file to have the hash value displayed in the terminal using th `cat` command. Copying the flag and pasting it into the Starting Point lab's page will grant you ownership of this machine, completing your very first task.

