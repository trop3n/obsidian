---
up: "[[Black Hat Python]]"
tags:
  - "#education/books/cybersecurity/redteam/blackhatpython/chapters"
source: "[[Black Hat Python, 2nd Edition - NSP.pdf]]"
---

# Chapter 2: Basic Networking Tools

The network is and always will be the sexiest area for an attacker. Ana attacker can do almost anything with simple network access, such as:

- Scan for hosts
- Inject packets
- Sniff data
- Remotely exploit hosts

Even if you've worked your way into an enterprise network, you may find that you have no way to execute network attacks. No netcat. No Wireshark. No compiler, and no means to install one. In many cases, however, you have a Python install.

This chapter will give you some basics on Python networking using the socket module (The full socket documentation can be found here: http://docs.python.org/3/library/socket.html.). Along the way, we’ll build clients, servers, and a TCP proxy. We’ll then turn them into our very own netcat, complete with a command shell. This chapter is the foundation for subsequent chapters, in which we’ll build a host discovery tool, implement cross-platform sniffers, and create a remote trojan framework. Let’s get started.
## Python Networking in a Paragraph

Programmers have a number of third-party tools to create networked servers and clients in Python, but the core of these tools is `socket`. This module exposes all of the necessary pieces to quickly:

- Write TCP and UDP clients and servers
- Use raw sockets
- Much more

For the purposes of breaking into and maintaining access to target machines, this module is all you really need. Let's start by creating some simple clients and servers -- two of the most common quick network scripts we will write.
## TCP Client

Countless times during penetration tests, we have needed to whip up a TCP client to test for services, send garbage data, fuzz, or perform any number of tasks. If you are working within the confines of large enterprise networks, you won't have the luxury of using networking tools or compilers, and sometimes you'll even be missing the absolute basics, like the ability to copy/paste or connect the the internet. This is where being able to quickly create a TCP client comes in handy.

```python
import socket

target_host = "www.google.com"
target_port = 80

# create a socket object
client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# connect the client
client.connect((target_host, target_port))

# send some data
client.send(b"GET / HTTP/1.1\r\nHost: google.com\r\n\r\n")

# recieve some data
response = client.recv(4096)
print(response.decode())
client.close()
```

1. We first create a **socket object** with the `AF_INET` and `SOCK_STREAM` parameters.
	- The `AF_INET` parameter indicates that *we will use a standard IPv4 address or hostname*
	- `SOCK_STREAM` indicates that this will be a *TCP client*.

2. We then connect the client to the server and send it some data as **bytes**.

3. The last step is to receive some data back and print out the response.

4. Then we close the socket (`client.close()`)

This is the simplest form of a TCP client, but it's the one we will write the most often.

This code snippet makes some serious assumptions about sockets that you definitely want to be aware of. 

1. That our connection will *always succeed*.
2. The server expects us to send data *first* (some servers expect to send data to you first and await your response).
3. The server will *always return data to use in a timely fashion*.

We make these assumptions largely for **simplicity's sake**. While programmers have varied opinions about how to deal with blocking sockets, exception handling in sockets, and the like, it's quite rare for pentesters to build these niceties into their quick and dirty tools for recon and exploitation, so we will omit them in this chapter. 
## UDP Client

A Python UDP client is not much different from a TCP client; we need to make only two small changes to get it to send packets in UDP:

```python
import socket

target_host = "127.0.0.1"
target_port = 9997

# create a socket object
client = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

# send some data
client.sendto(b"AAABBBCCC", (target_host, target_port))

# recieve some data
data, addr = client.recvfrom(4096)
print(data.decode())
client.close()
```

1. As we can see, we change the socket type to `SOCK_DGRAM` when creating the socket object.

2. The next step is to simply call `sendto()`, passing in the data and the server you want to send the data to. Because UDP is a connectionless protocol, there is **no call to `connect()` beforehand**. 

3. The last step is to call `recvfrom()` to receive the UDP data back. You will also notice that it returns both the data and the details of the remote host and port. 

Again, we're not looking to be superior network programmers; we want it to be quick, easy and reliable enough to handle our day-to-day hacking tasks. 
## TCP Server

Creating TCP servers in Python is just as easy as creating a client. You might want to use your own TCP server when writing command shells or crafting a proxy (both of which we will do later). Let's start by creating a standard multithreaded TCP server.

```python
import socket
import threading

IP = '0.0.0.0'
PORT = 9998

def main():
    server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server.bind((IP, PORT))
    server.listen(5)
    print(f'[*] Listening on {IP}:{PORT}')

    while True:
        client, address = server.accept()
        print(f'[*] Accepted connection from {address[0]}:{address[1]}')
        client_handler = threading.Thread(target=handle_client, args=(client,))
        client_handler.start()

def handle_client(client_socket):
    with client_socket as sock:
        request = sock.recv(1024)
        print(f'[*] Received: {request.decode("utf-8")}')
        sock.send(b'ACK')

if __name__ == '__main__':
    main()
```

1. To start off, we pass in the IP address and port we want the server to listen on.
2. Next, we tell the server to start listening, with a maximum backlog of connections set to 5. `server.listen(5)`
3. We then put the server into it's main loop, where it waits for an incoming connection. When a client connects, we receive the client socket in the `client` variable and the remote connection details in the `address` variable. We then create a new thread object that points to our `handle_client` function, and we pass it the client socket object as an argument.
4. We then start the thread to handle the client connection, at which point the main server loop is ready to handle another incoming connection. 
5. The `handle_client` function performs the `recv()` and then sends a simple message back to the client.

If you use the TCP client that we built earlier, you can send some packets to the server. You should see output like the following:

```
[*] Listening on 0.0.0.0:9998 
[*] Accepted connection from: 127.0.0.1:62512 
[*] Received: ABCDEF
```

That's it. While pretty simple, this is a ***very useful piece of code***. 
## Replacing Netcat

Netcat is the utility knife of networking, so it's no surprise that shrewd sysadmins remove it from their systems. Such a useful tool would be quite useful if an attacker managed to find a way in. With it, you can read and write data across the network, meaning you can use it to execute remote commands, pass files back and forth, or even open a remote shell. On more than one occasion, we've run into servers that don't have netcat installed but do have Python.

In these cases, it's useful to create a simple network client and server that you can use to push files, or a listener that gives you command line access. If you've broken through a web application, it's definitely worth dropping a Python callback to give you secondary access without having to first burn one of your trojans or backdoors. 

Creating a tool like this is also a great Python exercise, so let's get started writing `netcat.py`.

```python
import argparse
import socket
import shlex
import subprocess
import sys
import textwrap
import threading

def execute(cmd):
    cmd = cmd.strip()
    if not cmd:
        return
    
    output = subprocess.check_output(shlex.split(cmd)), stderr=subprocess.STDOUT)
    return output.decode()
```

Here, we import all of our necessary libraries and set up the `execute` function, which receives a command, runs it, and returns the output as a string. This function contains a new library we haven't covered yet: the `subprocess` library.

This library provides a powerful interface that *gives you a number of ways to interact with client*
*programs*.

In this case 1, we're using its `check_output` method, which runs a command on the local operating system and then returns the output from that command.

Now let's create our main block responsible for handling command line arguments and calling the rest of our functions. 