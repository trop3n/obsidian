---
up: "[[Real Python]]"
tags:
  - "#education/computerprogramming/languages/python/realpython/sockets"
source: https://realpython.com/python-sockets/
---

# [Socket Programming in Python (Guide)](https://realpython.com/python-sockets/)

Socket programming is essential for network communication, enabling data exchange across different devices. In Python, sockets allow for [inter-process communication (IPC)](https://en.wikipedia.org/wiki/Inter-process_communication) over networks. This tutorial provides a comprehensive guide on creating socket server modules and clients, handling multiple connections, and managing errors in Python's `socket` module.

---
## Inter-Process Communication (IPC)

In computer science, **inter-process communication** is the sharing of data between running processes in a computer system. Mechanisms for IPC may be provided by an operating system. Applications which use IPC are often categorized as **clients and servers**, where the client requests data and the servers responds to client requests. Many applications are both clients and servers, as commonly seen in [distributed computing](https://en.wikipedia.org/wiki/Distributed_computing).

IPC is *very important* to the design process for [microkernels](https://en.wikipedia.org/wiki/Microkernel "Microkernel") and [nanokernels](https://en.wikipedia.org/wiki/Nanokernel "Nanokernel"), which reduce the number of functionalities provided by the kernel. Those functionalities are then obtained by communicating with servers via IPC, leading to a large increase in communication when compared to a regular monolithic kernel. IPC interfaces generally encompass variable analytic framework structures. These processes ensure compatibility between the multi-vector protocols upon which IPC models rely. 

**By the end of this tutorial, you’ll understand that:**

- **A socket in Python** is an endpoint for sending or receiving data across a network using the socket API.
- **Socket programming in Python** involves using sockets to establish communication between a server and clients over a network.
- **A simple echo server in Python** can be created using sockets to listen for client connections and echo back received messages.
- **Handling multiple clients with Python sockets** can be achieved using non-blocking sockets and the `selectors` module for concurrent connections.
- **Connection errors in socket programs in Python** can be managed by implementing error handling and using exceptions like `OSError`.

Along the way, you’ll learn about the main functions and methods in Python’s [`socket`](https://docs.python.org/3/library/socket.html) module that let you write your own client-server applications based on TCP sockets. You’ll learn how to reliably send messages and data between endpoints and handle multiple connections simultaneously.

Networking and sockets are large subjects. Literal volumes have been written about them. If you’re new to sockets or networking, it’s completely normal if you feel overwhelmed with all of the terms and pieces. To get the most out of this tutorial, it’s best to download the source code and have it on hand for reference while reading:
## Historical Background

Sockets have a long history. Their use originated with ARPANET in 1971 and later became an API in the Berkeley Software Distribution (BSD) operating system released in 1983 called Berkeley sockets. 

When the internet took off in the 1990's with the World Wide Web, so did network programming. Web servers and browsers weren't the only applications taking advantage of newly connected networks and using sockets. Client-server applications of all types and sizes came into widespread use.

Today, although the underlying protocols used by the socket API have evolved over the years, and new ones have developed, the low-level API has remained the same.

The most common type of socket applications are client-server applications, where one side acts as the server and waits for connections from clients. This is the type of application that you'll be creating in this tutorial. More specifically, you'll focus on the socket API for [Internet sockets](https://en.wikipedia.org/wiki/Berkeley_sockets), sometimes called Berkeley or BSD sockets. There are also [Unix domain sockets](https://en.wikipedia.org/wiki/Unix_domain_socket), which can only be used to communicate between processes on the same host.
## Python Sockets API Overview

Python's `socket` module provides an interface to the [Berkeley sockets API](https://en.wikipedia.org/wiki/Berkeley_sockets). This is the module that you’ll use in this tutorial.

The primary socket API functions and methods in this module are:

- `socket()`
- `.bind()`
- `.listen()`
- `.accept()`
- `.connect()`
- `.connect_ex()`
- `.send()`
- `.recv()`
- `.close()`

Python provides a convenient and consistent API that maps directly to system calls, their C counterparts. In the next section, you'll learn how these are used together. 

As part of its *standard library*, Python also has classes that make using these low-level socket functions easier. Although it's not covered in this tutorial, you can check out the [socketserver module](https://docs.python.org/3/library/socketserver.html), a framework for network servers. There are also many modules available that implement higher-level Internet protocols like HTTP and SMTP. For an overview, see [Internet Protocols and Support](https://docs.python.org/3/library/internet.html).
## TCP Sockets

You're going to create a socket object using `socket.socket()`, specifying the socket type as `socket.SOCK_STREAM`. When you do that, the default protocol that's used is the [Transmission Control Protocol (TCP)](https://en.wikipedia.org/wiki/Transmission_Control_Protocol). This is a good default and probably what you want.

Why should you use TCP? The Transmission Control Protocol (TCP):

- **Is reliable**: Packets dropped in the network are detected and re-transmitted by the sender. 
- **Has in-order data delivery**: Data is read by your application in the order it was written by the sender. 

In contrast, the [User Datagram Protocol (UDP)](https://en.wikipedia.org/wiki/User_Datagram_Protocol) sockets created with `socket.SOCK_DGRAM` aren’t reliable, and data read by the receiver can be out-of-order from the sender’s writes.

Why is this important? Networks are a best-effort delivery system. There's no guarantee that your data will reach its destination or that you'll receive what's been sent to you.

Network devices, such as routers and switches, have finite bandwidth available and come with their own inherent system limitations. They have CPUs, memory, buses and interface packet buffers, just like your clients and servers. TCP relieves you from having to worry about [packet loss](https://en.wikipedia.org/wiki/Packet_loss), out-of-order data arrival, and other pitfalls that invariably happen when you're communicating across a network.

To better understand this, check out the sequence of socket API calls and data flow for TCP:

![](https://i.imgur.com/SzM2f9w.png)

The left hand column represents the *server*. On the right-hand side is the client. 

Starting in the top left-hand column, note the API calls that the server makes to set up a "listening" socket:

- `socket()`
- `.bind()`
- `.listen()`
- `.accept()`

A listening socket does just *what the name suggests*. It listens for connections from clients. When a client connects, the server calls `.accept()` to accept, or complete, the connection.

The client calls `.connect()` to establish a connection to the server and initiate a three-way handshake. The handshake step is important because it ensures that each side of the connection is **reachable in the network**, in other words that the client can reach the server and vice-versa. It may be that only one host, client, or server can reach the other. 

In the middle is the round-trip section, where data is exchanged between the client and server using calls to `.send()` and `.recv()`.

At the bottom, the client and server close their respective sockets. 
## Echo and Client Server

Now that you've gotten an overview of the socket API and how the client and server communicate, you're ready to create your first client and server. You'll begin with a simple implementation. The server will simply echo whatever it receives back to the client.

```python
import socket

HOST = "127.0.0.1" # Standard loopback interface
PORT = 65432 # Port to listen on

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
	s.bind((HOST, PORT))
	s.listen()
	conn, addr = s.accept()
	with conn:
		print(f"Connected by {addr}")
		while True:
			data = conn.recv(1024)
			if not data:
				break
			conn.sendall(data)
```

Don't worry about understanding everything above right now. There's a lot going on in these few lines of code. This is just a starting point so you can see a basic server in action.

> [!NOTE]
> **Note:** There’s a [reference section](https://realpython.com/python-sockets/#quick-reference) at the end of this tutorial that has more information and links to additional resources. You’ll also find these and other useful links throughout the tutorial.

Okay, so what exactly is happening in the API call?

`socket.socket()` creates a socket object that supports the [context manager type](https://docs.python.org/3/reference/datamodel.html#context-managers), so you can use it in a [`with` statement](https://docs.python.org/3/reference/compound_stmts.html#with). There’s no need to call `s.close()`:

```python
with socket.socket(AF_INETm socket.SOCK_STREAM) as s:
	pass # we use the socket object without calling s.close()
```

The arguments passed to [`socket()`](https://docs.python.org/3/library/socket.html#socket.socket) are [constants](https://docs.python.org/3/library/socket.html#constants) used to specify the [address family](https://realpython.com/python-sockets/#socket-address-families) and socket type. `AF_INET` is the Internet address family for [IPv4](https://en.wikipedia.org/wiki/IPv4). `SOCK_STREAM` is the socket type for [TCP](https://realpython.com/python-sockets/#tcp-sockets), the protocol that will be used to transport messages in the network.

The `.bind()` method is used to associate the socket with a specific network interface and port number:

```python
# ...

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
	s.bind((HOST, PORT))
	# ...
```

The values passed into `.bind()` depend on the [address family](https://realpython.com/python-sockets/#socket-address-families) of the socket. In this example, you're using `socket.AF_INET` (IPv4). So it expects a **two-tuple**: (`host`, `port`).

`host` can be a hostname, IP address, or empty string. If an IP address is used, `host` should be an IPv4-formatted address string. The IP address `127.0.0.1` is the standard IPv4 address for the loopback interface, so only processes on the host will be able to connect to the server. If you pass an *empty string*, the server will accept connections on all available IPv4 interfaces.

`port` represents the TCP port number used to accept connections on from clients. It should be an integer from `1` to `65535`, as `0` is **reserved**. Some systems may require superuser privileges if the port number is less than `1024`. 

> A note on using hostnames with `.bind()`:

> [!NOTE] hostnames with bind
> If you use a hostname in the host portion of IPv4/v6 socket address, the program may show a non-deterministic behavior, as Python uses the first address returned from the DNS resolution. The socket address will be resolved differently into an actual IPv4/v6 address, depending on the results from DNS resolution and/or the host configuration. For deterministic behavior use a numeric address in host portion. 

You'll learn more about this later, in [Using Hostnames](https://realpython.com/python-sockets/#using-hostnames). For now, just understand that *when using*
*a hostname, you could see different results depending on what's returned from the name resolution process*.

These results could be **anything**. The first time you run your application, you might get the address `10.1.2.3`. The next time, you get a different address, `192.168.0.1`. The third time, you could get `172.16.7.8`, and so on.

In the server example, `.listen()` enables a server to accept connections. It makes the server a *listening* socket:

```python
# ...
with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
	s.bind((HOST, PORT))
	s.listen()
	conn, addr = s.accept()
	# ...
```

The `.listen()` method has a `backlog` parameter. It specifies the number of unaccepted connections that the system will allow before refusing new connections. Starting in Python 3.5, it's optional. If not specified, a default `backlog` value is chosen.

If your server receives a lot of connection requests simultaneously, increasing the `backlog` value may help by setting the maximum length of the queue for pending connections. The maximum value is system dependent. For example, on Linux, see `/proc/sys/net/core/somaxconn`.

The `.accept()` method **blocks** execution and waits for an incoming connection. When a client connects, it returns a new socket object representing the connection and a tuple holding the address of the client. The tuple will contain `(host, port)` for IPv4 connections or `(host, port, flowinfo, scopeid)` for IPv6. See [Socket Address Families](https://realpython.com/python-sockets/#socket-address-families) in the reference section for details on the tuple values.

One thing that's imperative to understand is that you now have a new socket object from `.accept()`. This is important because *it's the socket that you'll use to communicate with the client*. It's distinct from the listening socket that the server is using to accept new connections:

```python
with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
	s.bind((HOST, PORT))
	s.listen()
	conn, addr = s.accept()
	with conn:
		print(f"Connected by {addr}")
		while True:
			data = conn.recv(1024)
			if not data:
				break
			conn.sendall(data)
```

After `.accept()` provides the client socket object `conn`, an infinite `while loop` is used to loop over [blocking calls](https://realpython.com/python-sockets/#blocking-calls) to `conn.recv()`. This reads whatever data the client sends and echoes it back using `conn.sendall()`.

If `conn.recv()` returns an empty [`bytes`](https://docs.python.org/3/library/stdtypes.html#bytes-objects) object, `b''`, that signals that the client closed the connection and the loop is terminated. The [`with` statement](https://realpython.com/python-with-statement/) is used with `conn` to automatically close the socket at the end of the block.
## Echo Client

Now, it's time to look at the client's source code:

```python
import socket

HOST = "127.0.0.1"
PORT = 65432 

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
	s.connect((HOST, PORT))
	s.sendall(b"Hello, world")
	data = s.recv(1024)

print(f"Received {data!r}")
```

In comparison to the server, the client is pretty simple. 

1. It creates a socket object, uses `.connect()` to connect to the server and calls `s.sendall()` to send its message. Lastly, it calls `s.recv()` to read the server's reply and then prints it.
## Running the Echo Client and Server

In this section, you'll run the client and server to see how they behave and inspect what's happening.

> [!NOTE]
> **Note:** If you’re having trouble getting the examples or your own code to run from the command line, read [How Do I Make My Own Command-Line Commands Using Python?](https://dbader.org/blog/how-to-make-command-line-commands-with-python) or [How to Run Your Python Scripts](https://realpython.com/run-python-scripts/). If you’re on Windows, check the [Python Windows FAQ](https://docs.python.org/3/faq/windows.html).

Open a terminal or command prompt, navigate to the directory that contains your scripts, ensure that you have Python 3.6 or above installed in your path, then run the server. 

```bash
python echo-server.py
```

Your terminal will appear to hang. That's because the server is blocked, or suspended, on `.accept()`.

```python
with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.bind((HOST, PORT))
    s.listen()
    ! conn, addr = s.accept() !
    with conn:
        print(f"Connected by {addr}")
        while True:
            data = conn.recv(1024)
            if not data:
                break
            conn.sendall(data)
```

It's waiting for a client connection. Now, open another terminal window or command prompt and run the client:

```
python echo-client.py
```

In the server window, we should notice something like this:

```
python echo-server.py
Connected by ('127.0.0.1', 64623)
```

In the output above, the server printed the `addr` tuple returned from `s.accept()`. This is the client's IP address and TCP port number. The port number, 64623, will most likely be different when you run it on your machine.
## Viewing Socket State

To see the current state of sockets on your host, use `netstat`. It's available by default on macOS, Linux and Windows.

```powershell
$ netstat -an
Active Internet connections (including servers)
Proto Recv-Q Send-Q  Local Address          Foreign Address        (state)
tcp4       0      0  127.0.0.1.65432        *.*                    LISTEN

```

Notice that `Local Address` is `127.0.0.1.65432`. If `echo-server.py` has used `HOST = ""` instead of `HOST = "127.0.0.1"`, netstat would show this:

```powershell
$ netstat -an
Active Internet connections (including servers)
Proto Recv-Q Send-Q  Local Address          Foreign Address        (state)
tcp4       0      0  *.65432                *.*                    LISTEN
```

`Local Address` is `*.65432`, which means *all available host interfaces that support the address family*
*will be used to accept incoming connections*. In this example, `socket.AF_INET` was used (IPv4) in the call to `socket()`. You can see this in the `Proto` column: `tcp4`.

The output above is trimmed to show the echo server only. You'll likely see much more output, depending on the system you're running it on. The things to notice are the columns `Proto`, `Local Address`, and `(state)`.
	In the last example above, netstat shows that the echo server is using an IPv4 TCP socket (`tcp4`), on port `65432` on all interfaces (`*.65432`), and it's in the listening state (`LISTEN`).

Another way to access this, along with additional helpful information, is to use `lsof` (list open files). It's available by default on macOS and can be installed on Linux using your package manager. 

```bash
$ lsof -i -n
COMMAND     PID   USER   FD   TYPE   DEVICE SIZE/OFF NODE NAME
Python    67982 nathan    3u  IPv4 0xecf272      0t0  TCP *:65432 (LISTEN)
```

`lsof` gives you the `COMMAND`, `PID` and `USER` of open internet sockets when used with the `-i` option. Above is the echo server process.

`netstat` and `lsof` have a lot of options available and differ depending on the OS that's running them. Check the `man` page or documentation for both. They're definitely worth spending a little time with and getting to know. You'll be rewarded. On macOS and Linux, use `man netstat` and `man lsof`. For Windows, use `netstat/?`.

Here's a common error that you'll encounter when a connection attempt is made to a port with no listening socket: 

```bash
$ python echo-client.py
Traceback (most recent call last):
  File "./echo-client.py", line 9, in <module>
    s.connect((HOST, PORT))
ConnectionRefusedError: [Errno 61] Connection refused
```

Either the specified port number is wrong or the server isn't working. Or maybe there's a firewall in the path that's blocking the connection, which can be easy to forget about. You may also see the error `Connection timed out`. Get a firewall rule added that allows the client to connect to the TCP port.

There’s a list of common [errors](https://realpython.com/python-sockets/#socket-errors) in the reference section.
# Communication Breakdown

Now let's take a closer look at how the client and server communicated with each other.

![](https://i.imgur.com/3IuxIaI.png)

When using the loopback interface (IPv4 address `127.0.0.1` or IPv6 address `::1`), data never leaves the host or touches the external network. In the diagram above, the loopback interface is contained inside the host. This represents the internal nature of the loopback interface and shows that connections and data that transit it are local to the host. 

> [!NOTE]
> **Note:** This is why you’ll also hear the loopback interface and IP address `127.0.0.1` or `::1` referred to as “localhost.”

Applications use the loopback interface to communicate with other processes running on the host and for security and isolation from the external network.

