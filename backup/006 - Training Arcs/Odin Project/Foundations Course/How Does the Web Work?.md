#odinproject #webdev 
# Introduction

Before you can understand how to program the web, you need a more rigorous understanding of the web itself than you likely have now. These concepts provide a more holistic understanding of the ecosystem in which you will be working and will enable you to talk intelligently with other developers about your work.
## Lesson overview

This section contains a general overview of topics that you will learn in this lesson.

- Describe what the internet is.
- Describe what packets are and how they are used to transfer data.
- Understand the differences between a web page, web server, web browser and search engine.
- Briefly explain what a client is.
- Briefly explain what a server is.
- Explain what IP addresses are.
- Explain what DNS servers are.
# [How Does the Internet Work?](https://developer.mozilla.org/en-US/docs/Learn_web_development/Howto/Web_mechanics/How_does_the_Internet_work)

The **internet** is the backbone of the web, the technical infrastructure that makes the web possible. At its most basic, the Internet is a large network of computers which communicate all together.

[The history of the Internet is somewhat obscure](https://en.wikipedia.org/wiki/Internet#History). It began in the 1960s as a US-army-funded research project, then evolved into a public infrastructure in the 1980s with the support of many public universities and private companies. The various technologies that support the Internet have evolved over time, but the way it works hasn't changed that much: Internet is a way to connect computers all together and ensure that, whatever happens, they find a way to stay connected.
## [Active Learning](https://developer.mozilla.org/en-US/docs/Learn_web_development/Howto/Web_mechanics/How_does_the_Internet_work#active_learning)

- [How the internet Works in 5 minutes](https://www.youtube.com/watch?v=7_LPdttKXPc): A 5-minute video to understand the very basics of Internet by Aaron Titus.
- [How does the Internet work?](https://www.youtube.com/watch?v=x3c1ih2NJEg) Detailed well visualized 9-minute video.
## Deeper Dive
### A Simple Network

When two computers need to communicate, you have to link them, either physically (usually with an Ethernet cable) or wirelessly (for example with [Wi-Fi](https://en.wikipedia.org/wiki/Wi-Fi) or [Bluetooth](https://en.wikipedia.org/wiki/Bluetooth) systems). All modern computers can sustain any of those connections. 

![](https://i.imgur.com/UMNRgTW.png)

Such a network is not limited to two computers. You can connect as many computers as you wish. But it gets complicated quickly. If you're trying to connect, say, ten computers, you need 45 cables, with nine plugs per computer.

![](https://i.imgur.com/RHlYPMD.png)

To solve this problem, each computer on a network is connected to a special tiny computer called a *router*. This *router* only has one job: like a signaler at a railways station, it makes sure that a message sent from a given computer arrives at the right destination computer. To send a message to computer B, computer A must send the message to the router, which in turn forwards the message to computer B and makes sure the message is not delivered to computer C.

Once we add a router to the system, our network of 10 computers only requires 10 cables: a single plug for each computer and a router with 10 plugs:

![](https://i.imgur.com/NeDr2JN.png)
## A Network of Networks

So far so good. But what about connecting hundreds, thousands, billions of comptuers? Of course a single *router* can't scale that far, if you read carefully, we said that a *router* is a computer like any other, so what keeps us from connecting two *routers* together? Nothing, so let's do that.

![](https://i.imgur.com/gW3xOqa.png)

By connecting computers to routers, then routers to routers, we are able to *scale infinitely*.

![](https://i.imgur.com/juIfDfu.png)

Such a network comes very close to what we call the Internet, but we're missing something. We built that network *for our own purposes*. There are other networks out there: your friends, your neighbors, anyone can have their own network of computers. But it's not really possible to set cables up between your house and the rest of the world, so how can you handle this? Well, there are already cables linked to your house, for example, electric power and telephone. The telephone infrastructure already connects your house with anyone in the world so it is the perfect wire we need. To connect our network to the telephone infrastructure, we need a special piece of equipment called a *modem*. This *modem* turns the information from our network into information manageable by the telephone infrastructure and vice versa. 

![](https://i.imgur.com/1Y0L2vl.png)

So we are connected to the telephone infrastructure. The next step is to send the messages from our network to the network we want to reach. To do that, we will connect our network to an Internet Service Provider. An ISP is a company that manages some special routers that are all linked together and can also access other ISP's routers. So the message from our network is carried through the network of ISP networks to the destination network. The internet consists of this whole infrastructure of networks. 

![](https://i.imgur.com/rve0azC.png)
## Finding Computers

If you want to send a mesage to a computer, you have to specify which one. Thus any computer linked to a network has a unique address that identifies it, called an "IP address" (where IP stands for Internet Protocol). It's an address made up of a series of four numbers separated by dots, for example: `192.0.2.172`.

That's perfectly find for computers, but we human beings have a hard time remembering that sort of address. To make things easier, we can alias an IP address with a human-readable name called a *domain name*. For example (at the time of writing; IP addresses can change) `google.com` is the domain name used on top of the IP address `142.250.190.78`. So using the domain name is the easiest way to reach a computer over the internet.
## Internet and the Web

As you might notice, when we browse the web with a web browser, we usually use the domain name to reach a website. Does that mean the Internet and the Web are the same thing? It's not that simple. As we saw, the Internet is a technical infrastructure which allows billions of computers to be connected all together. Among these computers, some computers, (called *web servers*) can send message intelligible to web browsers. The *Internet* is an infrastructure, whereas the *Web* is a service built on top of that infrastructure. It is worth noting that there are several other services build on top of the Internet, such as email and [IRC](https://developer.mozilla.org/en-US/docs/Glossary/IRC).
## Intranets and Extranets

**Intranets** are *private networks* that are restricted to members of a particular organization. They are commonly used to provide a portal for members to securely access shared resources, collaborate and communicate. For example, an organization's intranet might host web pages for sharing department team information, shared drives for managing key documents and files, portals for performing business administration tasks, and collaboration tools like wikis, discussion boards, and messaging systems. 

Extranets are very similar to Intranets, except they open all or part of a private network to allow sharing and collaboration with other organizations. They are typically used to safely and securely share information with clients and stakeholders who work closely with a business. OFten their functions are similar to those provided by an intranet: information and file sharing, collaboration tools, discussion boards, etc.

Both intranets and extranets run on the same kind of infrastructure as the internet, and use the same protocols. They can therefore be accessed by authorized members from different physical locations.  

![](https://i.imgur.com/3SJNEa6.png)
# [How the Web Works](https://developer.mozilla.org/en-US/docs/Learn_web_development/Getting_started/Web_standards/How_the_web_works)

*How the web works* provides a simplified view of what happens when you view a webpage in a web browser on your computer or phone.

This theory is not essential to writing web code in the short term, but before long you'll really start to benefit from understanding what's happening in the background.


| Prerequisites:     | Basic familiarity with your computer operating system, web browsers, and web technologies.                                                                                                                                                                                                      |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Learning outcomes: | - Clients and servers and their roles in the web.<br>- DNS and how it works at a high level.<br>- TCP/IP, HTTP, and packets.<br>- HTTP syntax at a basic level.<br>- Common HTTP response codes (e.g. 200, 301, 403, 404, and 500).<br>- Components of a URL (protocol, domain, and subdomain). |
## Clients and Servers

Computers connected to the internet are called **clients** and **servers**. A simplified diagram of how they interact might look like this:

![](https://i.imgur.com/PL6FOH9.png)

- Clients are the typical web user's internet connected devices and web-accessing software available on those devices.
- Servers are computers that store web pages, sites or apps. When a client device wants to access a page, a copy of the webpage is downloaded from the server onto the client machine to be displayed in the user's web browser.
## Other Parts of the Toolbox

The client and server we've described above don't tell the whole story. There are many other parts involved, and we'll describe them below. 

For now, let's imagine that the web is a road. On one end of the road is the client, which is like your house. On the other end is the server, which is a shop you want to buy something from.

In addition to the client and server, we also need to say hello to:

- **Your internet connection**: Allows you to send and receive data on the web. It's basically the street between your house and the shop.
- **TCP/IP**: Transmission Control Protocol and Internet Protocol are communication ports that define how data should travel across the internet. This is like the transport mechanisms that let you place an order, go to the shop, and buy your goods. In our example, this is like a car or a bike.
- **DNS** Domain Name System is like an *address book for websites*. When you type a web address in your browser, the browser looks at the DNS to find the website's IP address before it can retrieve the website. The browser needs to find out which server the website lives on, so it can send HTTP messages to the right place. This is like looking up the address of the shop so you can access it.
- **HTTP**: Hypertext Transfer Protocol is an application protocol that defines a language for clients and servers to speak to each other. This is like the language you use to order your goods.
- **Component Files**: A Website is made up of many different files, which are like the different parts of the goods you buy from the shop. These files come in two main types:
	- **Code Files**: Websites are built primarily using HTML, CSS and JavaScript, though you'll meet other technologies later.
	- **Assets**: This is the collective name for all the other stuff that makes up a website, such as images, music, video, word documents, and PDFs.
## So, What Happens Exactly?

When you type a web address into your browser:

1. The browser goes to the DNS server, and finds the real address of the server that the website lives on.
2. The browser sends an HTTP request to the server, asking it to send a copy of the website to the client. This message, and all other data sent between the client and server, is sent across your internet connection using TCP/IP.
3. If the server approves the client's request, the server sends the client a "200 OK" message, which means "Of course you can look at that website, here it is" and then starts sending the website's files to the browser as a series of small chunks called *data packets*.
4. The browser assembles the small chunks into a complete web page and displays it to you.
## The Order in Which Component Files are Parsed

When browsers send requests to servers for HTML files, those HTML files often contain `<link>` elements referencing external CSS stylesheets and `<script>` elements referencing external JavaScript scripts. It's important to know the order in which those files are [parsed by the browser](https://developer.mozilla.org/en-US/docs/Web/Performance/How_browsers_work#parsing) as the browser loads the page:

- The browser parses the HTML first, and that leads to the browser recognizing any `<link>` element references to external CSS stylesheets and any `<script>` element references to scripts.
- As the browser parses the HTML, it sends requests back to the server for any CSS files it has found from `<link>` elements, and any JavaScript files it has found from `<script>` elements, and from those, then parses the CSS and JavaScript.
- The browser generates an in-memory [DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model) tree from the parsed HTML, generates an in-memory [CSSOM](https://developer.mozilla.org/en-US/docs/Glossary/CSSOM) structure from the parsed CSS, and [compiles and executes](https://developer.mozilla.org/en-US/docs/Web/Performance/How_browsers_work#javascript_compilation) the parsed JavaScript.
- As the browser builds the DOM tree and applies the styles from the CSSOM tree and executes the JavaScript, a visual representation of the page is painted to the screen, and the user sees the page content and can begin to interact with it.
## DNS Explained

Real web addresses aren't the nice, memorable strings you type into your address bar to find your favorite websites. They are special numbers that look like this: `192.0.2.172`.

This is called an IP address, and it repesents a unique location on the web. However, it's not very easy to remember is it? That's why the Domain Name System was invented. This system uses special serves that match up a web address you type into the browser (like "mozilla.org") to the website's real (IP) address. 

Websites can be reached directly via their IP addresses. You can use a [DNS lookup tool](https://www.nslookup.io/website-to-ip-lookup/) to find the IP address of a website.
## Packets Explained

Earlier we used the term "packets" to describe the format in which the data is transferred between the client and server. What do we mean here? Basically, when data is sent across the web, it is sent in thousands of small chunks. There are multiple reasons why data is sent in small packets. They are sometimes dropped or corrupted, and it's easier to replace small chunks when this happens. 

Additionally, the packets can be routed along different paths, making the exchange faster and allowing many different users to download the same website at the same time. If each website was sent as a single big chunk, only one user could download it at a time, which obviously would make the web very inefficient and not much fun to use.
# [What is a Domain Name?](https://developer.mozilla.org/en-US/docs/Learn_web_development/Howto/Web_mechanics/What_is_a_domain_name#how_does_a_dns_request_work)

| Prerequisites: | First you need to know [how the Internet works](https://developer.mozilla.org/en-US/docs/Learn_web_development/Howto/Web_mechanics/How_does_the_Internet_work) and understand [what URLs are](https://developer.mozilla.org/en-US/docs/Learn_web_development/Howto/Web_mechanics/What_is_a_URL). |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Objective:     | Learn what domain names are, how they work, and why they are important.                                                                                                                                                                                                                          |
## Summary

Domain names are a key part of the Internet Infrastructure. They provide a human-readable address for any webserver available on the internet. 

Any internet-connected computer can be reached through a public IP address, either an IPv4 address like `192.0.2.172` or an IPv6 address like `2001:db8:8b73:0000:0000:8a2e:0370:1337`.

Computers can handle such addresses easily, but people have a hard time finding out who is running the server or what service the website offers. IP addresses are hard to remember an might change over time.

To solve all these problems we use human-readable addresses called domain names.
## Deeper Dive
### Structure of Domain Names

A domain name has a simple structure made of several parts (it might be one part only, two, three...), separated by dots and **read from right to left**.

Each of those parts provides specific information about the whole domain name.
#### [TLD](https://developer.mozilla.org/en-US/docs/Glossary/TLD) (Top-Level Domain).

TLDs tell users the general purpose of the service behind the domain name. The most generic TLDs(`.com`, `.org`, `.net`) don't require web services to meet any particular criteria, but some TLDs enforce stricter policies so it is clearer what their purpose is. For example:

- Local TLDs such as `.us`, `.fr`, or `.se` can require the service to be provided in a given language or hosted in a certain country -- they are supposed to indicate a resource in a particular language or country.
- TLDs containing `.gov` are only allowed to be used be government departments.
- The `.edu` TLD is only for use by educational or academic institutions.

TLDs can contain special as well as Latin characters. A TLD's maximum length is 63 characters, although most are around 2-3.

The full list of TLDs is [maintained by ICANN](https://www.icann.org/resources/pages/tlds-2012-02-25-en).
#### Label (or component)

The labels are what follow the TLD. A label is a case-insensitive character sequence anywhere from one to sixty-three characters in length, containing only the letters `A` through `Z`, digits `0` through `9`, and the `-` character (which may not be the first or last character in the label). `a`, `97`, and `hello-strange-person-16-how-are-you` are all example of valid labels.

A domain name can have many labels (or components). It is not mandatory nor necessary to have 3 labels to form a domain name. For instance, [informatics.ed.ac.uk](https://informatics.ed.ac.uk/) is a valid domain name. For any domain you control (e.g. [mozilla.org](https://www.mozilla.org/en-US/)), you can create "subdomains" with different content located at each, like [developer.mozilla.org](https://developer.mozilla.org/), [support.mozilla.org](https://support.mozilla.org/), or [bugzilla.mozilla.org](https://bugzilla.mozilla.org/).
## Buying a Domain Name
### Who Owns a Domain Name?

You cannot "buy a domain name". This is so that unused domain names eventually become available to be used again by someone else. If every domain name was bought, the web would quickly fill up with unused domain names that were locked and couldn't be used by anyone.

Instead, you pay for the right to use a domain name for one or more years. You can renew your right, and your renewal has priority over other people's applications. But you never own the domain name.

Companies called registrars use domain name registries to keep track of technical and administrative information connecting you to a domain name.

> [!NOTE]
> **Note:** For some domain name, it might not be a registrar which is in charge of keeping track. For instance, every domain name under `.fire` is managed by Amazon.
### Finding an Available Domain Name

To find out whether a given domain name is available,

- Go to a domain name registrar's website. Most of them provide a "whois" service that tells you whether a domain name is available.
- Alternatively, if you use a system with a built-in shell, type a `whois` command into it, as shown here for `mozilla.org`:

```bash
whois mozilla.org
```

This will output the following:

```
Domain Name:MOZILLA.ORG
Domain ID: D1409563-LROR
Creation Date: 1998-01-24T05:00:00Z
Updated Date: 2013-12-08T01:16:57Z
Registry Expiry Date: 2015-01-23T05:00:00Z
Sponsoring Registrar:MarkMonitor Inc. (R37-LROR)
Sponsoring Registrar IANA ID: 292
WHOIS Server:
Referral URL:
Domain Status: clientDeleteProhibited
Domain Status: clientTransferProhibited
Domain Status: clientUpdateProhibited
Registrant ID:mmr-33684
Registrant Name:DNS Admin
Registrant Organization:Mozilla Foundation
Registrant Street: 650 Castro St Ste 300
Registrant City:Mountain View
Registrant State/Province:CA
Registrant Postal Code:94041
Registrant Country:US
Registrant Phone:+1.6509030800
```

As you can see, I can't register `mozilla.org` because the Mozilla Foundation has already registered it.

On the other hand, let's see if I could register `afunkydomainname.org`:

```bash
whois afunkydomainname.org
```

This will output the following:

```bash
NOT FOUND
```

As you can see, the domain does not exist in the `whois` database, so we could ask to register it.
### Getting a Domain Name

The process is quite straightforward:

1. Go to a registrar's website.
2. Usually there is a prominent "Get a domain name" call to action. Click on it.
3. Fill out the form with all required details. Make sure, especially, that you have not misspelled your desired domain name. Once it's paid for, it's too late!
4. The registrar will let you know when the domain name is properly registered. Within a few hours, all DNS servers will have received your DNS information.

> [!NOTE]
> **Note:** In this process the registrar asks you for your real-world address. Make sure you fill it properly, since in some countries registrars may be forced to close the domain if they cannot provide a valid address.
### DNS Refreshing

DNS databases are stored on every DNS server worldwide, and all these servers refer to a few special servers called "authoritative name servers" or "top-level DNS servers" -- these are like the boss servers that manage the system.

Whenever your registrar creates or updates any information for a given domain, the information must be refreshed in every DNS database. Each DNS server that knows about a given domain stores the information for some time before it automatically invalidated and then refreshed (the DNS server queries an authoritative server and fetches the updated information from it). Thus, it takes some time for DNS servers that know about this domain name to get the up-to-date information.
## How Does a DNS Request Work?

As we already saw, when you want to display a webpage in your browser it's easier to type a domain name than an IP address. Let's take a look at the process:

1. Type `mozilla.org` in your browser's location bar.
2. Your browser asks your computer if it already recognizes the IP address identified by this domain name (using a local DNS cache). If it does, the name is translated to the IP address and the browser negotiates contents with the web server. End of story.
3. If your computer does not know which IP is behind the `mozilla.org` name, it goes on to ask a DNS server, whose job is precisely to tell your computer which IP address matches each registered domain name.
4. Now that the computer knows the requested IP address, your browser can negotiate contents with the web server. 

![](https://i.imgur.com/a027ELb.png)
## [Next steps](https://developer.mozilla.org/en-US/docs/Learn_web_development/Howto/Web_mechanics/What_is_a_domain_name#next_steps)

Okay, we talked a lot about processes and architecture. Time to move on.

- If you want to get hands-on, it's a good time to start digging into design and explore [the anatomy of a web page](https://developer.mozilla.org/en-US/docs/Learn_web_development/Howto/Design_and_accessibility/Common_web_layouts).
- It's also worth noting that some aspects of building a website cost money. Please refer to [how much it costs to build a website](https://developer.mozilla.org/en-US/docs/Learn_web_development/Howto/Tools_and_setup/How_much_does_it_cost).
- Or read more about [Domain Names](https://en.wikipedia.org/wiki/Domain_name) on Wikipedia.
- You can also find [here](https://howdns.works/) a fun and colorful explanation of how DNS works.
# [What is a URL?](https://developer.mozilla.org/en-US/docs/Learn_web_development/Howto/Web_mechanics/What_is_a_URL)

This article discusses Uniform Resource Locators (URLs), explaining what they are and how they're structured.

| Prerequisites: | You need to first know [how the Internet works](https://developer.mozilla.org/en-US/docs/Learn_web_development/Howto/Web_mechanics/How_does_the_Internet_work), [what a Web server is](https://developer.mozilla.org/en-US/docs/Learn_web_development/Howto/Web_mechanics/What_is_a_web_server) and [the concepts behind links on the web](https://developer.mozilla.org/en-US/docs/Learn_web_development/Howto/Web_mechanics/What_are_hyperlinks). |
| -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Objective:     | You will learn what a URL is and how it works on the Web.                                                                                                                                                                                                                                                                                                                                                                                           |
## Summary

A **URL** (Uniform Resource Locator) is the address of a unique resource on the internet. It is one of the key mechanisms used by browsers to retrieve published resouces, such as HTML pages, CSS documents, images and so on.

In theory, each valid URL points to a unique resource. In practice, there are some exceptions, the most common being a URL pointing to a resource that no longer exists or that has moved. As the resource represented by the URL and the URL itself are handled by the webserver, it is up to the owner of the web server to carefully manage that resource and its associated URL.
## Basics: Anatomy of a URL

Here are some examples of URLs:

```
https://developer.mozilla.org
https://developer.mozilla.org/en-US/docs/Learn_web_development/
https://developer.mozilla.org/en-US/search?q=URL
```

Any of those URLs can be typed into your browsers's address bar to tell it to load the associated resource, which in all three cases is a Web page.

A URL is composed of different parts, some mandatory and others optional. The most important parts are highlighted on the URL below (details are provided in the following sections):

![](https://i.imgur.com/SPoK28E.png)

> [!NOTE]
> **Note:** You might think of a URL like a regular postal mail address: the _scheme_ represents the postal service you want to use, the _domain name_ is the city or town, and the _port_ is like the zip code; the _path_ represents the building where your mail should be delivered; the _parameters_ represent extra information such as the number of the apartment in the building; and, finally, the _anchor_ represents the actual person to whom you've addressed your mail.

> [!NOTE]
> **Note:** There are [some extra parts and some extra rules](https://en.wikipedia.org/wiki/Uniform_Resource_Locator) regarding URLs, but they are not relevant for regular users or Web developers. Don't worry about this, you don't need to know them to build and use fully functional URLs.
## Scheme

![](https://i.imgur.com/NQVdopm.png)

The first part of the URL is the *scheme*, which indicates the protocol that the browser must use to request the resource (a protocol is a set method for  exchanging or transferring data around a computer network). Usually for websites the protocol is HTTP or HTTPS (the S is for Secure). Addressing web pages requires one of these two, but browsers also know how to handle other schemes such as `mailto:` (to open a mail client), so don't be surprised if you see other protocols. 
## Authority

![](https://i.imgur.com/MsEaf92.png)

Next follows the *authority*, which is separated from the scheme by the character pattern `://`. If present the authority includes both the *domain* (e.g. `www.example.com`) and the *port* (`80`), separated by a colon:

- The domain indicates which Web server is being requested. Usually this is a domain name, but an IP address may also be used (but this is rare and much less convenient).
- The port indicates the technical "gate" used to access the resources on the web server. It is usually omitted if the web server uses the standard ports of the HTTP protocol (80 for HTTP and 443 for HTTPS) to grant access to it's resources. Otherwise, it is mandatory.

> [!NOTE]
> **Note:** The separator between the scheme and authority is `://`. The colon separates the scheme from the next part of the URL, while `//` indicates that the next part of the URL is the authority.
> 
> One example of a URL that doesn't use an authority is the mail client (`mailto:foobar`). It contains a scheme but doesn't use an authority component. Therefore, the colon is not followed by two slashes and only acts as a delimiter between the scheme and mail address.
## Path to Resource

![](https://i.imgur.com/78iOHSp.png)

`/path/to/myfile.html` is the path to the resource on the Web server. In the early days of the web, a path like this represented a physical file location on the Web server. Nowadays, it is mostly an abstraction handled by Web servers without any physical reality.
## Parameters

![](https://i.imgur.com/g0AMhsy.png)

`?key1=value1&key2=value2` are extra parameters provided to the web server. Those parameters are a list of key/value pairs separated with the `&` symbol. The web server can use those parameters to do extra stuff before returning the resource. Each Web server has its own rules regarding parameters, and the only reliable way to know if a specific Web server is handling parameters is by asking the Web server onwer.
## Anchor

![](https://i.imgur.com/1PvsVzI.png)

`#SomewhereInTheDocument` is an **anchor** to another part of the resource itself. An anchor represents a sort of "bookmark" inside the resource, giving the browser the directions to show the content located at that "bookmarked" spot. On an HTML document, for example, the browser will scroll to the point where the anchor is defined; on a video or audio document, the browser will try to go to the time the anchor represents. It is worth noting that the part after the `#`, also known as the **fragment identifier**, is never sent to the server with the request. 
## How to Use URLs

Any URL can be typed right inside the browser's address bar to get to the resource behind it. But this is only the tip of the iceberg.

The [HTML](https://developer.mozilla.org/en-US/docs/Glossary/HTML) language (see [Structuring content with HTML](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Structuring_content)) makes extensive use of URLs:

- to create links to other documents with the `<a>` element;
- to link a document with its related resources through various elements such as `<link>` or `<script>`;
- to display media such as images (with the `<img>` element), videos (with the `<video>` element), sounds and music (with the `<audio>` element), etc;
- to display other HTML documents with the `<iframe>` element.

> [!NOTE]
> When specifying URLs to load resources as part of a page (such as when using the `<script>`, `<audio>`, `<img>`, `<video>`, and the like), you should generally only use HTTP and HTTPS URLs, with few exceptions (one notable one being `data:`; see [Data URLs](https://developer.mozilla.org/en-US/docs/Web/URI/Schemes/data)). Using FTP, for example, is not secure and is no longer supported by modern browsers.

Other technologies, such as CSS or JavaScript, use URLs extensively, and these are really the heart of the web.
## Absolute URLs vs. Relative URLs

What we saw above is called an *absolute URL*, but there is also something called a *relative URL*. The [URL standard](https://url.spec.whatwg.org/#absolute-url-string) defines both — though it uses the terms [_absolute URL string_](https://url.spec.whatwg.org/#absolute-url-string) and [_relative URL string_](https://url.spec.whatwg.org/#relative-url-string), to distinguish them from [URL objects](https://url.spec.whatwg.org/#url) (which are in-memory representations of URLs).

Let's examine what the distinction between *absolute* and *relative* means in the context of URLs.

The required parts of a URL depend to a great extent on the context in which the URL is used. In your browser's address bar, a URL doesn't have any context, so you must provide a full (or *absolute*) URL, like the ones we saw above. You don't need to include the protocol (the browser uses HTTP by default) or the port (which is only required when the targeted web server is using some unusual port), but all the other parts of the URL are necessary.

When a URL is used within a document, such as in an HTML page, things are a bit different. because the browser already has the document's own URL, it can use this information to fill in the missing parts of any URL available inside that document. We can differentiate between an *absolute URL* and a *relative URL* by looking only at the *path* part of the URL. If the path part of the URL starts with the `/` character, the browser will fetch that resource from the top root of the server, without reference to the context given by the current document. 

Let's look at some examples to make this clearer. Let's assume that the URLs are defined from within the document located at the following URL: `https://developer.mozilla.org/en-US/docs/Learn`.

`https://developer.mozilla.org/en-US/docs/Learn` itself is an absolute URL. It has all necessary parts needed to locate the resource it points to. 

All of the following URLs are relative URLs:

- Scheme-relative URL: `//developer.mozilla.org/en-US/docs/Learn` -- only the protocol is missing. The browser will use the same protocol as the one used to load the document hosting that URL.
- Domain-relative URL: `/en-US/docs/Learn` -- the protocol and the domain name are both missing. The browser will use the same protocol and the same domain name as the one used to load the document hosting that URL.
- Sub-resources: `Common_questions/Web_mechanics/What_is_a_URL` -- the protocol and domain name are missing, and the path doesn't begin with `/`. The browser will attempt to find the document in a subdirectory of the one containing the current resource. In this case, we really want to reach this URL: `https://developer.mozilla.org/en-US/docs/Learn_web_development/Howto/Web_mechanics/What_is_a_URL`.
- Going back int he directory tree: `../CSS/display` -- the protocol and domain name are missing, and the path begins with `..`. This is inherited from the UNIX file system world -- to tell the browser we want to go up by one level. Here we want to reach this URL: `https://developer.mozilla.org/en-US/docs/Learn_web_development/../Web/CSS/display`, which can be simplified to: `https://developer.mozilla.org/en-US/docs/Web/CSS/display`.
- Anchor-only: `#semantic-urls` - all parts are missing except the anchor. The browser will use the current document's URL and replace or add the anchor part to it. This is useful when you want to link to a specific part of the current document.
## Semantic URLs

Despite their very technical flavor, URLs represent a human-readable entry point for a website. They can be memorized, and anyone can enter them into a browser's address bar. People are at the core of the web, and so it is considered best practice to build what is called *semantic URLs*. Semantic URLs use words with inherent meaning that can be understood by anyone, regardless of their technical know how.

Linguistic semantics are of course relevant to computers. You've probably often seen URLs that look like mashups of random characters. But there are many advantages to creating human-readable URLs:

- It is easier for you to manipulate them.
- It clarifies things for users in terms of where they are, what they're doing, and what they're reading or interacting with on the Web. 
- Some search pages can use those semantics to improve the classification of the associated pages.










# [The Web Standards Model](https://developer.mozilla.org/en-US/docs/Learn_web_development/Getting_started/Web_standards/The_web_standards_model)
# [What are Hyperlinks?](https://developer.mozilla.org/en-US/docs/Learn_web_development/Howto/Web_mechanics/What_are_hyperlinks)
# [What is a Web Server?](https://developer.mozilla.org/en-US/docs/Learn_web_development/Howto/Web_mechanics/What_is_a_web_server)
# [Browsing the Web](https://developer.mozilla.org/en-US/docs/Learn_web_development/Getting_started/Environment_setup/Browsing_the_web)



