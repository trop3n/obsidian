#hackthebox #labs 
# Introduction

Sometimes, when we are asked to enumerate the services of specific hosts on the client network, we will be met with *file transfer services* that may have high chances to be **poorly configured**. The purpose of this exercise is to familiarize yourself with the ***File Transfer Protocol***, a native protocol to all host operating systems and used for a long time for simple file transfer tasks, be they automated or manual.

FTP can be *easily misconfigured* if not correctly understood. There are cases where an employee of the client company we are assessing might want to bypass file checks or firewall rules for transferring a file from themselves to their peers. Considering the many different mechanisms for controlling and monitoring data flow within an enterprise network today, this scenario becomes a substantial and viable cases we might meet in the wild. 

At the same time, FTP can be used to *transfer log files* from one network device to another or a log collection server. Suppose the network engineer in charge of handling the configuration forgets to secure the receiving FTP server properly or does not put enough importance on the information contained within the logs and decides to leave the FTP service unsecured intentionally. 
	In that cases, an attacker could gain leverage of the logs and extract all kinds of information from them, which can later be used to map out the network, enumerate usernames, detect active services, and more.

Let's take a look at what FTP is, according to definition on Wikipedia:

> [!important]
> The File Transfer Protocol (FTP) is a standard communication protocol used to transfer
> computer files from a server to a client on a computer network. FTP is built on a client–
> server model architecture using separate control and data connections between the client
> and the server. FTP users may authenticate themselves with a clear-text sign-in protocol,
> generally in the form of a username and password. However, they can connect anonymously if
> the server is configured to allow it. For secure transmission that protects the username
> and password and encrypts the content, FTP is often secured with SSL/TLS (FTPS) or
> replaced with SSH File Transfer Protocol (SFTP).

From the first lines of the excerpt above, we can see mention of the client-server model architecture. This refers to the roles hosts in the network have during the act of transferring data between them. Users can download and upload files from the client (their own host) to the server (a centralized data storage device) or vice versa. Conceptually speaking, the client is always the host that downloads and uploads files to the server, and the server always is the host that safely stores the data being transferred. 

![](https://i.imgur.com/WJ8DKj5.png)

Clients can also browse the available files on the server using the FTP protocol. From a user's terminal perspective, this action will seem like **browsing their own operating system's**
**directories** for files that they need. 

FTP services also come with a GUI, akin to Windows OS programs, enabling easier navigation for beginners. An example of a well-known GUI-oriented service is FileZilla. However, let's first understand what it means for a port to be running a service openly.

A port running a service is a reserved space for the IP address of the target to receive requests and send results from. If we only had IP addresses or hostnames, then the hosts could only do 1 task at a time. This means that if you wanted to browse the web and play music from an application on your computer simultaneously, you could not, because the IP address would be used for handling either the first or the latter, but not both at the same time. By having ports, you can have one IP address handling multiple services, as it adds another layer of distinction.

In the case shown below, we can see FTP being active on port 21. However, let's add some extra services like SSH (Secure Shell Protocol) and HTTPD (web server) in order to explore a more typical example. With this type of configuration, a network administrator has set up a rudimentary core web server configuration, allowing them to achieve the following, all at the same time if need be:

- Receive and send files that can be used to configure the webserver or serve logs to an external source
- Be able to be logged into for remote management from a distant host, in case any configuration changes are needed. 
- Serve web content that can be access remotely through another host's web browser.

From the graph below, you can see where FTP sits in the logical structure of the host, together with other services that could potentially be running on it at the same time.

![](https://i.imgur.com/jRKmtX5.png)

The Wiki article shows that it is considered non-standard for FTP to be used ***without*** the encryption layer provided by protocols such as SSL/TLS (FTPS) or SSH-tunneling (SFTP). FTP by itself does have the ability to require credentials before allowing access to the stored files. However, the deficiency here is that traffic containing said files can be intercepted with what is known as a Man-in-the-Middle Attack (MitM). The contents of the files can be read in plaintext.

![](https://i.imgur.com/xA61kda.png)

However, if the network administrators choose to wrap the connection with the SSL/TLS protocol or tunnel the FTP connection through SSH (as shown below) to add a layer of encryption that only the source and destination hosts can decrypt, this would successfully foil most MitM attacks. Notice how port 21 has disappeared, as the FTP protocol gets moved under the SSH protocol on Port 22, thus being tunneled through it and secured against any interception.

![](https://i.imgur.com/fKi7Bok.png)

However, the situation we are dealing with in this case is much simpler. We are only going to interact with the target running a simple, misconfigured FTP service. Let us proceed and analyze how such a service running on an internal host would look like.
## Enumeration

Firstly, let's check if our VPN connection is established. Using the `ping` protocol can help us with this since it is a low-overhead method of reaching the target to get a response, thus confirming our connection is established, and the target is reachable. 

**Low-overhead** means that very little data is sent to the target by default, allowing us to quickly check the status of the connection without having to wait for a whole scan to complete beforehand. The ping protocol can be invoked from the terminal using the `ping {target_ip}` command. 

This will not always work in large corporate environments, as firewalls usually have rules to prevent pinging between hosts, even in the same subnet, to avoid insider threats and discover other hosts and services.

```bash
jason@nixos ~ ❯ ping 10.129.176.215
PING 10.129.176.215 (10.129.176.215) 56(84) bytes of data.
64 bytes from 10.129.176.215: icmp_seq=1 ttl=63 time=1517 ms
64 bytes from 10.129.176.215: icmp_seq=2 ttl=63 time=504 ms
64 bytes from 10.129.176.215: icmp_seq=3 ttl=63 time=45.9 ms
64 bytes from 10.129.176.215: icmp_seq=4 ttl=63 time=120 ms
64 bytes from 10.129.176.215: icmp_seq=5 ttl=63 time=1622 ms
64 bytes from 10.129.176.215: icmp_seq=6 ttl=63 time=595 ms
64 bytes from 10.129.176.215: icmp_seq=7 ttl=63 time=50.0 ms
64 bytes from 10.129.176.215: icmp_seq=8 ttl=63 time=47.6 ms
64 bytes from 10.129.176.215: icmp_seq=9 ttl=63 time=46.1 ms
64 bytes from 10.129.176.215: icmp_seq=10 ttl=63 time=46.0 ms
64 bytes from 10.129.176.215: icmp_seq=11 ttl=63 time=46.1 ms
64 bytes from 10.129.176.215: icmp_seq=12 ttl=63 time=46.2 ms
64 bytes from 10.129.176.215: icmp_seq=13 ttl=63 time=45.8 ms
64 bytes from 10.129.176.215: icmp_seq=14 ttl=63 time=45.8 ms
64 bytes from 10.129.176.215: icmp_seq=15 ttl=63 time=45.9 ms
64 bytes from 10.129.176.215: icmp_seq=16 ttl=63 time=46.0 ms
64 bytes from 10.129.176.215: icmp_seq=17 ttl=63 time=45.7 ms
64 bytes from 10.129.176.215: icmp_seq=18 ttl=63 time=46.1 ms
64 bytes from 10.129.176.215: icmp_seq=19 ttl=63 time=1111 ms
64 bytes from 10.129.176.215: icmp_seq=20 ttl=63 time=108 ms
64 bytes from 10.129.176.215: icmp_seq=21 ttl=63 time=45.9 ms
64 bytes from 10.129.176.215: icmp_seq=22 ttl=63 time=47.4 ms
64 bytes from 10.129.176.215: icmp_seq=23 ttl=63 time=45.8 ms
64 bytes from 10.129.176.215: icmp_seq=24 ttl=63 time=45.8 ms
64 bytes from 10.129.176.215: icmp_seq=25 ttl=63 time=46.0 ms
^C
--- 10.129.176.215 ping statistics ---
25 packets transmitted, 25 received, 0% packet loss, time 24067ms
rtt min/avg/max/mdev = 45.706/256.407/1621.990/455.853 ms, pipe 2
```

We can cancel the ping command by pressing CTRL+C on our keyboard, otherwise it will run infinitely. Following the output from the command, we can see that responses are being received from the target host. This means that the host is reachable through the VPN tunnel we formed. We can now start scanning the open services on the host.

```bash
jason@nixos ~ ❯ sudo nmap 10.129.176.215
[sudo] password for jason:
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-31 18:22 CST
Nmap scan report for 10.129.176.215
Host is up (0.050s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE
21/tcp open  ftp

Nmap done: 1 IP address (1 host up) scanned in 9.29 seconds
```

Scanning using our previously used command, we can see the FTP service open and running on port 21. However, what if we would like to know the actual version of the service running on this port? Could scanning it with different switches present us with the needed information?

```bash
jason@nixos ~ ❯ sudo nmap -sV 10.129.176.215
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-31 18:24 CST
Nmap scan report for 10.129.176.215
Host is up (0.047s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
Service Info: OS: Unix
```

In our case, the `-sV` switch stands for version detection. Using this switch will consequently make our scan take longer but will offer us more insight into the version of the service running on the previously detected port. This means that at a glance, we would be able to tell if the target is vulnerable due to running outdated software or if we need to dig deeper to find our attack vector.

We will not be looking at exploiting the service per se. We will take small steps towards our goals, and the next one will involve simply interacting with the service as-is to learn more about how we should approach targets. However, having the service version always helps us gain more insight into what is running on the scanned port. 
## Foothold

It is time we interacted with the target. 

In order to access the FTP service, we will use the `ftp` command on our own host. It's good practice to have a quick check that your `ftp` is up to date and installed properly. 

Once it is installed, we can run `ftp -?` to see what the service is capable of.

```bash
jason@nixos ~ took 13s ❯ ftp '-?'
Usage: ftp [OPTION...] [HOST [PORT]]
Remote file transfer.

  -4, --ipv4                 contact IPv4 hosts
  -6, --ipv6                 contact IPv6 hosts
  -A, --active               enable active mode transfer
  -d, --debug                enable debugging output
  -e, --no-edit              (ignored)
  -g, --no-glob              turn off file name globbing
  -i, --no-prompt            do not prompt during multiple file transfers
  -n, --no-login             do not automatically login to the remote system
  -N, --netrc=NETRC          select a specific initialization file
      --prompt[=PROMPT]      print a command line PROMPT (optionally), even if
                             not on a tty
  -p, --passive              enable passive mode transfer, default for `pftp'
  -t, --trace                enable packet tracing
  -v, --verbose              verbose output
  -?, --help                 give this help list
      --usage                give a short usage message
  -V, --version              print program version

Mandatory or optional arguments to long options are also mandatory or optional
```

From the except above, we can see that we can connect to the target host using the command below. This will initiate a request to authenticate on the FTP service running on the target, which will return a prompt back to our host:

```
jason@nixos ~ ❯ ftp 10.129.176.215
Connected to 10.129.176.215.
220 (vsFTPd 3.0.3)
Name (10.129.176.215:jason):
```

The prompt is asking us for a username. Here is where the magic happens.

A **typical misconfiguration** for running FTP services allows an `anonymous` account to access services like any other authenticated user. The `anonymous` username can be input when the prompt appears, followed by any password whatsoever since the service will disregard the password for this specific account.

```
jason@nixos ~ ❯ ftp 10.129.176.215
Connected to 10.129.176.215.
220 (vsFTPd 3.0.3)
Name (10.129.176.215:jason): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
```

Typing in the `help` command allows us to view which commands are available. You will be able to see this pattern with every script and service that you have access to. `-h`, `--help` or `help` commands will always issue a list of all the commands available to you as a user, with descriptions occasionally included. 

```
ftp> help
Commands may be abbreviated.  Commands are:

!               dir             macdef          proxy           site
$               disconnect      mdelete         sendport        size
account         epsv4           mdir            put             status
append          form            mget            pwd             struct
ascii           get             mkdir           quit            system
bell            glob            mls             quote           sunique
binary          hash            mode            recv            tenex
bye             help            modtime         reget           trace
case            idle            mput            rstatus         type
cd              image           newer           rhelp           user
cdup            ipany           nmap            rename          umask
chmod           ipv4            nlist           reset           verbose
close           ipv6            ntrans          restart         ?
cr              lcd             open            rmdir
delete          lpwd            passive         runique
debug           ls              prompt          send
```

Some of these commands listed here seem familiar to us. We already know how to use `ls` and `cd`. Let us issue the first command and view the contents of the folder. 

Once the files are listed, run `get flag.txt` to retrieve the flag.
