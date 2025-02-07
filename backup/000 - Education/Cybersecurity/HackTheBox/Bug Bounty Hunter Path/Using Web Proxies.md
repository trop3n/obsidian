
#webdev #webproxies #networking #hackthebox #bugbounty 

# Intro to Web Proxies

Today, most modern web and mobile applications work by *continuously connecting to back-end servers to send and receive data and then processing this data on the user's device*, like their web browsers or mobile phones. With most applications heavily relying on back-end servers to process data, testing and securing the back-end servers is quickly becoming more important.

Testing web requests to back-end servers make up the bulk of Web Application Penetration Testing, which includes concepts that apply to both web and mobile applications. To capture the requests and traffic passing between applications and back-end servers and manipulate these types of requests for testing purposes, we need to use `Web Proxies`.
## What are Web Proxies?

**Web Proxies** are specialized tools that can be set up between a browser/mobile application and a back-end server to capture and view all the web requests being sent between both ends, essentially acting a man-in-the-middle (MITM) tools. While other `Network Sniffing` applications, like Wireshark, operate by analyzing all local traffic to see what is passing through a network, Web Proxies mainly work with web ports such as, but not limited to: `HTTP/80` and `HTTPS/443`.

Web proxies are considered among the most *essential tools* for any web pentester. The significantly simplify the process of capturing and replaying web requests compared to earlier CLI-based tools. Once a web proxy is set up, we can see all HTTP requests made by an application and all of the responses sent by the back-end server. Furthermore, we can intercept a specific request to modify it's data and see how the back-end server handles them, which is an essential part of any web penetration test.
## Uses of Web Proxies

While the primary user of web proxies is to capture and replay HTTP requests, they have many other features that enable different uses for web proxies. The following list shows some of the other tasks we may use web proxies for:

- Web application vulnerability scanning
- Web fuzzing
- Web crawling
- Web application mapping
- Web request analysis
- Web configuration testing
- Code reviews

In this module, we will not discuss any specific web attacks, as other HTB Academy web modules cover various web attacks. However, we will thoroughly cover how to use web proxies and their various features and mention which type of web attacks require which feature. We will be covering the two most common web proxy tools: `Burp Suite` and `ZAP`.
## Burp Suite

[Burp Suite (Burp)](https://portswigger.net/burp) is the most common web proxy for web penetration testing. Is has an excellent user interface for its various features and even provides a built-in Chromium browser to test web applications. Certain Burp features are only available in the commercial version `Burp Pro/Enterprise`, but even the free version is an extremely powerful testing tool to keep in our arsenal. 

Some of the `paid-only` features are:

- Active web app scanner
- Fast Burp Intruder
- Ability to load certain Burp extensions

The community `free` version of Burp Suite should be enough for most penetration testers. Once we start more advanced web application penetration testing, the `pro` features may become handy. Most features that we will cover in this module area available in the community `free` version of Burp Suite, but we will also touch upon some of the `pro features`, like the **Active Web App Scanner**.

> [!TIP]
> **Tip:** If you have an educational or business email address, then you can apply for a free trial of Burp Pro at this [link](https://portswigger.net/burp/pro/trial) to be able to follow along with some of the Burp Pro only features showcased later in this module.
## OWASP Zed Attack Proxy (ZAP)

[OWASP Zed Attack Proxy (ZAP)](https://www.zaproxy.org/) is another common web proxy tool for web penetration testing. ZAP is a free and open-source project initiated by the [Open Web Application Security Project (OWASP)](https://owasp.org) and maintained by the community, so it has no-paid only features as Burp does. It has grown significantly over the past few years and is quickly gaining market recognition as the leading open-source web proxy tool.

Just like Burp, ZAP provides various basic and advanced features that can be utilized for web pentesting. ZAP also has certain strengths over Burp, which we will cover later in this module. The main advantage of ZAP over Burp is being a free, open-source project, which means that we will not face any throttling or limitations in our scans that are only lifted with a paid subscription. Furthermore, with a growing community of contributors, ZAP is gaining many of the paid-only Burp features for free.

In the end, learning both tools can be quite similar and will provide us with options for every situation through a pentest, and we can choose to use whichever one we find more suitable for our needs. In some instances, we may not see enough value to justify buying a paid Burp subscription, and we may switch to ZAP to have a completely free and open experience. In other situations where we want a more mature solution for advanced pentests or corporate pentesting, we may find the value provided by Burp Pro to be justified and may switch to Burp for these features.
# Setting Up

Both Burp and ZAP are available for Windows, macOS and Linux. Both are already installed on the PwnBox instance and can be accessed from the bottom dock or top bar menu. Both tools are pre-installed on common Penetration Testing Linux distributions like Parrot or Kali. We will cover the installation and setup process for Burp and Zap in this section which will be helpful if we want to install the tools on our own VM.

---
## Burp Suite

If Burp is not preinstalled on our VM, we can start by downloading it from [Burp's Download Page](https://portswigger.net/burp/releases/). Once downloaded, we can run the installer and follow the instructions, which may vary from one operating system to another, but should be pretty straightforward. There are installers for Windows, Linux and macOS.

Once installed, Burp can either be launched from the terminal by typing `burpsuite`, or from the application menu as previously mentioned. Another option is to download the `JAR` file (which can be used on all operating systems with a Java Runtime Environment (JRE) installed) from the above downloads page. We can run it with the following command line or by double-clicking it:

```shell-session
trop3n@htb[/htb]$ java -jar </path/to/burpsuite.jar>
```

> [!NOTE]
> Note: Both Burp and ZAP rely on Java Runtime Environment to run, but this package should be included in the installer by default. If not, we can follow the instructions found on this [page](https://docs.oracle.com/goldengate/1212/gg-winux/GDRAD/java.htm).

Once we start up Burp, we are prompted to create a new project. If we are running the community version, we would only be able to use temporary projects without the ability to save our progress and carry on later:

![](https://i.imgur.com/4B7wqNp.png)

If we are using the pro/enterprise version, we will have the option to either start a new project or open an existing project.

We may need to save our progress if we were pentesting huge web applications or running an `Active Web Scan`. However, we may not need to save our progress and, in many cases, can start a `temporary` every time.

So, let's select `temporary project`, and click continue. Once we do, we will be prompted to either use `Burp Suite Configurations`, or to `Load a Configuration File`, and we'll choose the first option:

![](https://i.imgur.com/UUV6mi7.jpeg)

Once we start heavily utilizing Burp's features, we may want to customize our configurations and load them when starting Burp. For now, we can keep `Use Burp Defaults`, and `Start Burp`. Once all of this is done, we should be ready to start using Burp.
## ZAP

We can download ZAP from its [download page](https://www.zaproxy.org/download/), choose the installer that fits our operating system, and follow the basic installation instructions to get it installed. ZAP can also be downloaded as a cross-platform JAR file and launched within the `java - jar` command or by double-clicking on it, similarly to Burp.

To get started with ZAP, we can launch it from the terminal with the `zaproxy` command or access it from the application menu like Burp. Once ZAP starts up, unlike the free version of Burp, we will be prompted to either create a new project or a temporary project. Let's use a temporary project by choosing `no`, as we will not be working on a big project that we will need to persist for several days.

![](https://i.imgur.com/jtVGVTr.jpeg)

After that, we will have ZAP running, and we can continue the proxy setup process, as we will discuss in the next section.

> [!NOTE]
> Tip: If you prefer to use to a dark theme, you may do so in Burp by going to (`User Options>Display`) and selecting "dark" under (`theme`), and in ZAP by going to (`Tools>Options>Display`) and selecting "Flat Dark" in (`Look and Feel`).
# Proxy Setup

Now that we have installed and started both tools, we'll learn how to use the most commonly used feature; `Web Proxy`.

We can set up these tools as a proxy for any application, such that all web requests would be routed through them so that we can manually examine what web requests an application is sending and receiving. This will enable us to understand better what the application is doing in the background and allows us to *intercept and change these requests or reuse them with various changes* to see how the application responds. 

---

## Pre-Configured Browser

To use the tools as web proxies, we must configure our browser proxy settings to use them as the proxy or use the pre-configured browser. Both tools have a pre-configured browser that comes with pre-configured proxy settings and the CA certificates pre-installed, making starting a web penetration test very easy. 

In Burp's (`Proxy>Intercept`), we can click on `Open Browser`, which will open Burp's pre-configured browser and automatically route all web traffic through Burp:

![](https://i.imgur.com/grrdhhj.jpeg)

> In ZAP, we can click on the Firefox browser icon at the end of the top bar, and it will open the pre-configured browser:

![](https://i.imgur.com/LD3f77V.jpeg)

For our uses in this module, using the pre-configured browser should be enough.

---

## Proxy Setup

In many cases, we may want to use a real browser for pentesting, like Firefox. To use Firefox with out web proxy tools, we must first configure it to use them as the proxy. We can manually go to Firefox preferences and set up the proxy to use the web proxy listening port. Both Burp and ZAP use port `8080` by default, but we can use any available port. If we choose a port that is in use, the proxy will fail to start, and we will receive an error message.

> [!NOTE]
> **Note:** In case we wanted to serve the web proxy on a different port, we can do that in Burp under (`Proxy>Options`), or in ZAP under (`Tools>Options>Local Proxies`). In both cases, we must ensure that the proxy configured in Firefox uses the same port.

Instead of manually switching the proxy, we can utilize the Firefox extension [Foxy Proxy](https://addons.mozilla.org/en-US/firefox/addon/foxyproxy-standard/) to easily and quickly change the Firefox proxy. This extension is pre-installed in your PwnBox instance and can be installed to your own Firefox browser by visiting the [Firefox Extensions Page](https://addons.mozilla.org/en-US/firefox/addon/foxyproxy-standard/) and clicking `Add to Firefox` to install it.

Once we have the extension installed, we can configure the web proxy on it by clicking on this icon in the Firefox top bar and choosing `options`:

![](https://i.imgur.com/SchirUq.jpeg)

Once we're on the `options` page, we can click on `add` on the left pane, and then use `127.0.0.1` as the IP, and `8080` as the port, and name it `Burp` or `ZAP`. 

![](https://i.imgur.com/ZYqPElh.jpeg)

> [!NOTE]
> Note: This configuration is already added to Foxy Proxy in PwnBox, so you don't have to do this step if you are using PwnBox.

Finally, we can click on the `Foxy Proxy` icon and select `Burp/ZAP`. 

![](https://i.imgur.com/tn4Vs3A.jpeg)
## Installing CA Certificate

Another important step when using Burp Proxy/ZAP with our browser is to install the web proxy's CA Certificates. If we don't do this step, some HTTPS traffic may not get properly routed, or we may need to click `accept` every time Firefox needs to send an HTTPS request.

We can install Burp's certificate once we select Burp as our proxy in `Foxy Proxy`, by browsing to `http://burp`, and download the certificate from there by clicking on CA Certificate.

To get ZAP's certificate, we can go to (`Tools>Options>Dynamic SSL Certificate`), then click on `Save`:

![](https://i.imgur.com/iorEJBk.jpeg)

We can also change our certificate by generating a new one with the `Generate` button.

Once we have our certificates, we can install them within Firefox by browsing to [about:preferences#privacy](about:preferences#privacy), scrolling to the bottom, and clicking `View Certificates`:

![](https://i.imgur.com/1VNIdVl.jpeg)

After that, we can select the `Authorities` tab, and then click on `import`, and select the downloaded CA certificate:

![](https://i.imgur.com/iW4QDQb.jpeg)

Finally, we must select `Trust this CA to identify websites` and `Trust this CA to identify email users`, and then click OK:

![](https://i.imgur.com/4se0Y6D.jpeg)

Once we install the certificate and configure the Firefox proxy, all Firefox web traffic will start routing through our web proxy.
# Intercepting Web Requests

Now that we have set up our proxy, we can use it to *intercept and manipulate various HTTP requests sent by the web application* we are testing. We'll start by learning how to intercept web requests, change them, and then send them through to their intended destination.

---
## Intercepting Requests

### Burp

In Burp, we can navigate to the `Proxy` tab, and request interception should be on by default. If we want to turn request interception on or off, we may go to the `Intercept` sub-tab and click on `Intercept is on/off` button to do so.l

![](https://i.imgur.com/vKfYWi0.jpeg)

Once we turn request interception on, we can start up the pre-configured browser and then visit our target website after spawning it from the exercise at the end of this section. Then, once we go back to Burp, we will see the intercepted request awaiting our action, and we can click on `forward` to forward the request:

![](https://i.imgur.com/5sO8bE2.jpeg)

> [!NOTE]
> Note: as all Firefox traffic will be intercepted in this case, we may see another request has been intercepted before this one. If this happens, click 'Forward', until we get the request to our target IP, as shown above.

### ZAP

In ZAP, interception is off by default, as shown by the green button on the top bar (green indicates that requests can pass and not be intercepted). We can click on this button to turn the Request Interception on or off, or we can use the shortcut [CTRL+B] to toggle it on or off:

![](https://i.imgur.com/0wlifxy.png)

Then, we can start the pre-configured browser and revisit the exercise web page. We will see the intercepted request in the top-right pane, and we can click on the step (right to the red `break` button) to forward the request. 

![](https://i.imgur.com/5AD0bVT.png)

ZAP also has a powerful feature called `Heads Up Display (HUD)`, which allows us to control most of the main ZAP features from right within the pre-configured browser. We can enable the `HUD` by clicking it's button at the end of the top menu bar:

The HUD has many features that we will cover as we go through the module. For intercepting requests, we can click on the second button from the top on the left pane to turn request interception on:

![](https://i.imgur.com/Xf6QjIq.png)

Now, once we refresh the page or send another request, the HUD will intercept the request and will present it to use for action:

![](https://i.imgur.com/P4mNBEO.png)

We can choose to `step` to send the request and examine its response and break any further requests, or we can choose to `continue` and let the page send the remaining requests. The `step` button is helpful when we want to examine every step of the page's functionality, while `continue` is useful when we are only interested in a single request and can forward the remaining requests once we reach our target request.

> [!TIP] 
> The first time you use the pre-configured ZAP browser you will be presented with the HUD tutorial. You may consider taking this tutorial after this section, as it will teach you the basics of the HUD. Even if you do not grasp everything, the upcoming sections should cover whatever you missed. If you do not get the tutorial, you can click on the configuration button on the bottom right and choose "Take the HUD Tutorial".
## Manipulating Intercepted Requests

Once we intercept the request, it will remain hanging until we forward it, as we did above. We can examine the request, manipulate it to make any changes we want, and then send it to its destination. This helps us better understand what information a particular web application is sending in its web requests and how it may respond to any changes we make in that request.

There are numerous applications for this in Web Penetration Testing, such as testing for:

- `SQL Injections`
- `Command Injections`
- `Upload Bypass`
- `Authentication Bypass`
- `XSS`
- `XXE`
- `Error Handling`
- `Deserialization`

And many other potential web vulnerabilities, as will see in other web modules in HTB academy. So, let's show this with a basic example to demonstrate intercepting and manipulating web requests. 

Let us turn request interception back on in the tool of our choosing, set the `IP` value on the page, then click on the `Ping` button. Once our request is intercepted, we should get a similar HTTP request to the following:

```http
POST /ping HTTP/1.1
Host: 46.101.23.188:30820
Content-Length: 4
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://46.101.23.188:30820
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.114 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Referer: http://46.101.23.188:30820/
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Connection: close

ip=1
```

Typically, we can only specify numbers in the `IP` field using the browser, as the web page prevents us from sending any non-numeric characters using front-end JavaScript. However, with the power of intercepting and manipulating HTTP requests, we can try using other characters to "break" the application ("breaking" the request/response flow by manipulating the target parameter, not damaging the target web application). If the web application does not verify and validate the HTTP requests on the back end, we may be able to manipulate it and exploit it. 

So, let us change the `ip` parameter's value from `1` to `;ls;` and see how the web application handles our input:

![](https://i.imgur.com/UPX79N9.png)

Once we click continue/forward, we we will see that the response changed from the default ping output to the `ls` output, meaning we successfully manipulated the request to inject our command:

![](https://i.imgur.com/JCfzAJ2.png)

This demonstrates a basic example of how request interception and manipulation can help with testing web applications for various vulnerabilities, which is considered an essential tool to be able to test different web applications effectively.

> [!NOTE] 
> As previously mentioned, we will not be covering specific web attacks in this module, but rather how Web Proxies can facilitate various types of attacks. Other web modules in HTB Academy cover these types of attacks in depth.
# Intercepting Responses

In some instances, we may need to intercept the HTTP responses from the server before they reach the browser. This can be useful when we want to change how a specific webpage looks, like enabling certain disabled fields or showing certain hidden fields, which may help us in our penetration testing activities. 

So, let's see how we can achieve that with the exercise we tested in our previous section.

In our exercise, the `IP` field only allowed us to input numeric values. If we intercept the response before it reaches our browser, we can edit it to accept any value, which would enable us to input the payload we used last time directly. 

---
## Burp

In Burp, we can enable response interception by going to (`Proxy>Options`) and enabling `Intercept Response` under `Intercept Server Responses`:

![](https://i.imgur.com/2eXsWBg.png)

After that, we can enable request interception once more and refresh the page with `CTRL+SHIFT+R` in our browser (to force a full refresh). When we go back to Burp, we should see the intercepted request, and we can click on `forward`. Once we forward the request, we'll see our intercepted response:

![](https://i.imgur.com/YEmuetI.png)

Let's try changing the `type="number` on line 27 to `type="text"`, which should enable us to write any value we want. We will also change the `maxlength="3"` to `maxlength="100"` so we can enter longer input.

```html
<input type="text" id="ip" name="ip" min="1" max="255" maxlength="100"
    oninput="javascript: if (this.value.length > this.maxLength) this.value = this.value.slice(0, this.maxLength);"
    required>
```

Now, once we click on `forward` again, we can go back to Firefox to examine the edited response:

![](https://i.imgur.com/sQqNyND.png)

As we can see, we could change the way the page is rendered by the browser and can now input any value we want. We may use the same technique to persistently enable any disabled HTML buttons by modifying their HTML code.

> [!exercise]
> Exercise: Try using the payload we used last time directly within the browser, to test how intercepting responses can make web application penetration testing easier.

---
## ZAP

![](https://i.imgur.com/8lHy6Um.png)

Let's try and see how we can do the same with ZAP. As we saw in the previous section, when our requests are intercepted by ZAP, we can click on `Step`, and it will send the request and automatically intercept the response.

Once we make the same changes we previously did and click on `Continue`, we will see that we can also use any input value:

![](https://i.imgur.com/oUHTRG5.png)

However, ZAP HUD also has another powerful feature that can help us in cases like this. While in many instances we may need to intercept the response to make custom changes, if all we wanted was to enable disabled input fields or show hidden input fields, then we can click on the third button on the left (the light bulb icon), and it will enable/show these fields without having to intercept the response or refresh the page. 

For example, the below web application has the `IP` input field disabled:

![](https://i.imgur.com/lSwA42c.png)

In these cases, we can click on the `Show/Enable` button, and it will enable the button for us, and we can interact with it to add our input:

![](https://i.imgur.com/fsbdWhZ.png)

We can similarly use this feature to show all hidden fields or buttons. `Burp` also has a similar feature, which we can enable under `Proxy>Options>Response Modification`, then select one of the options, like `Unhide hidden form fields`.

Another feature that is similar is the `Comments` button, which will indicate the positions where the HTML comments that are usually only visible in the source code. We can click on the `+` button on the left pane and select `Comments` to add the `Comments` button, and once we click on it, the `Comments` indicators should be shown. For example, the below screenshot shows an indicator for a position that has a comment, and hovering over it with our cursor shows the comment's content:

![](https://i.imgur.com/m271thg.png)

Being able to modify how the web page looks makes it much easier for us to perform web application penetration testing in certain scenarios instead of having to send our input through an intercepted request. Next, we will see how we can automate this process to modify our changes in the response automatically so we don't have to keep intercepting and manually changing the responses.

---
# Automatic Modification

We may want to apply certain modifications to all outgoing HTTP requests or all incoming HTTP responses in certain situations. In these cases, we can utilize automatic modifications based on rules we set, so the web proxy tools will automatically apply them.
## Automatic Request Modification

Let us start with an example of automatic request modification. We cna choose to match any text within our requests, either in the request header or request body, and then replace them with different text. For the sake of demonstration, let's replace our `User-Agent` with `HackTheBox Agent 1.0`, which may be handy in cases where we may be dealing with filters that block certain User-Agents.
### Burp Match and Replace

We can go to (`Proxy>Options>Match and Replace`) and click on `Add` in Burp. As the below screenshot shows, we will set the following options:

![](https://i.imgur.com/7O5Amod.png)


|                                             |                                                                                                                                                  |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| `Type: Request header`                      | since the change we want to make will be in the request header and not in its body.                                                              |
| `Match: ^User-Agent.*$`                     | The regex pattern that matches the entire line with `User-Agent` in it.                                                                          |
| `Replace: User-Agent: HackTheBox Agent 1.0` | This is the value that will replace the line we matched above.                                                                                   |
| `Regex match`: True                         | We don't know the exact User-Agent string we want to replace, so we'll use regex to match any value that matches the pattern we specified above. |
Once we enter the above options and click `Ok`, our new Match and Replace option will be added and enabled and will start automatically replacing the `User-Agent` header in our requests with our new User-Agent. We can verify that by visiting any website using the pre-configured Burp browser and reviewing the intercepted request. We will see that our User-Agent has indeed been automatically replaced:

![](https://i.imgur.com/gCFkbvY.png)
### ZAP Replacer

ZAP has a similar feature called `Replacer`, which we can access by pressing `CTRL+R` or clicking on `Replacer` in ZAP's options menu. It is fairly similar to what we did above, so we can click on `Add` and add the same options we used earlier:

![](https://i.imgur.com/BXiE3kX.png)

- `Description`: `HTB User-Agent`.
- `Match Type`: `Request Header (will add if not present)`.
- `Match String`: `User-Agent`. We can select the header we want from the drop down menu, and ZAP will replace its value.
- `Replacement String`: `HackTheBox Agent 1.0`.
- `Enable`: True

ZAP also has the `Request Header String` that we can use with a Regex pattern. `Try using this option with the same values we used for Burp to see how it works.`

ZAP also provides the option to set the `Initiators`, which we can access by clicking on the other tab in the Windows shown above. Initiators enable us to select where our `Replacer` option will be applied. We will keep the default option of `Apply to all HTTP(S) messages` to apply everywhere.

We can now enable request interception by pressing `CTRL+B`, then can visit any page in the pre-configured ZAP browser.

![](https://i.imgur.com/fPaZVlV.png)
## Automatic Response Modification

The same concept can be used with HTTP responses as well. In the previous section, you may have noticed when we intercepted the response that the modifications we made to the `IP` field were temporary and not applied when we refreshed the page unless we intercepted the response and added them again. To solve this, we can automate response modification similarly to what we did above to automatically enable any characters in the `IP` field for easier command injection.

Let us go back to (`Proxy>Options>Match and Replace`) in Burp to add another rule. This time we will use the type of `Response body` since the change we want to make exists in the response's body and not in it's headers. In this case, we do not have to use regex as we know the exact string we want to replace, though it is possible to use regex to do the same thing if we prefer. 

![](https://i.imgur.com/j1KacEU.png)

- `Type`: `Response body`.
- `Match`: `type="number"`
- `Replace`: `type="text"`.
- `Regex match`: False

Try adding another rule to change `maxlength="3"` to `maxlength="100"`.

Now, once we refresh the page with `[CTRL+SHIFT+R]`, we'll see that we can add any input to the input field, and this should persist between page refreshes as well:

![](https://i.imgur.com/ILRb1ZF.png)

We can now click on `Ping`, and our command injection should work without intercepting and modifying the request.

> [!exercise]
> Exercise 1: Try applying the same rules with ZAP Replacer. You can click on the tab below to show the correct options.

> Change input type to text:  

- `Match Type`: `Response Body String`.  
- `Match Regex`: `False`.  
- `Match String`: `type="number"`.  
- `Replacement String`: `type="text"`.  
- `Enable`: `True`.  
  
Change max length to 100:  
- `Match Type`: `Response Body String`.  
- `Match Regex`: `False`.  
- `Match String`: `maxlength="3"`.  
- `Replacement String`: `maxlength="100"`.  
- `Enable`: `True`.

> [!exercise]
> Exercise 2: Try adding a rule that automatically adds `;ls;` when we click on `Ping`, by matching and replace the request body of the `Ping` request.
# Repeating Requests

In the previous sections, we successfully bypassed the input validation to use a non-numeric input to reach command injection on the remote server. If we want to repeat the same process with a different command, we would have to intercept the request again, provide a different payload, forward it again, and finally check out browser to get the final result.

As you can imagine, if we would do this for each command,it would take us forever to enumerate a system, as each command would require 5-6 steps to get executed. However, for such repetitive tasks, we can utilize request repeating to make this process significantly easier. 

Request repeating allows us to *resend any web request* that has previously gone through the web proxy. This allows us to make quick changes to any request before we sent it, then get the response with our tools without intercepting and modifying each request. 
## Proxy History

To start, we can view the HTTP requests history in `Burp` at (`Proxy>HTTP History`):

![](https://i.imgur.com/B5Qae9Q.png)

In `ZAP`, we can find it in the bottom History pane or ZAP's main UI at the bottom `History` tab as well:

![](https://i.imgur.com/rI6jkRg.png)

Both tools also provide filtering and sorting options for request history, which may be helpful if we deail with a huge number of requests and want to locate a specific request. `Try to see how filters work on both tools`.

> [!NOTE]
> Note: Both tools also maintain WebSockets history, which shows all connections initiated by the web application even after being loaded, like asynchronous updates and data fetching. WebSockets can be useful when performing advanced web penetration testing, and are out of the scope of this module.

If we click on any request in the history in either tool, its details will be shown:

`Burp`:

![](https://i.imgur.com/O1YOgvh.png)

`ZAP`:

![](https://i.imgur.com/2SGXUOx.png)

> [!tip] Burp vs. ZAP
> While ZAP only shows the final/modified request that was sent, Burp provides the ability to examine both the original request and the modified request. If a request was edited, the pane header would say `Original Request`, and we can click on it and select `Edited Request` to examine the final request that was sent.
## Repeating Requests
### Burp

Once we locate the request we want to repeat, we can click `[CTRL+R]` in Burp to send it to the `Repeater` tab, and then we can either navigate to the `Repeater` tab or click `[CTRL+SHIFT+R]` to go to it directly. Once in `Repeater`, we can click on `Send` to send the request:

![](https://i.imgur.com/GnNsAy7.png)

> [!tip]
> We can also right-click on the request and select `Change Request Method` to change the HTTP method between POST/GET without having to rewrite the entire request.
### ZAP

In ZAP, once we locate our request, we can right-click on it and select `Open/Resend with Request Editor`, which would open the request editor window, and allow us to resend the request with the `Send` button to send our request:

![](https://i.imgur.com/Wyhj8SM.png)

We can also see the `Method` drop-down menu, allowing us to quickly switch the request method to any other HTTP method.

> [!tip]
> By default, the Request editor window in ZAP has the Request/Response in different tabs. You can click on the display buttons to change how they are organized. To match the above look choose the same display options shown in the screenshot.

We can achieve the same result with the pre-configured browser with `ZAP HUD`. We can locate the request in the bottom History pane, and once we click on it, the `Request Editor` window will show, allowing us to resend it. We can select `Replay in Console` to get the response in the same `HUD` window, or select `Replay in Browser` to see the response rendered in the browser:

![](https://i.imgur.com/KKHsQJx.png)

So, let us try to modify our request and send it. In all three options (`Burp Repeater, ZAP Request Editor`, and `ZAP HUD`), we will see that the requests are modifiable, and we can select the text we want to change and replace it with whatever we want, and then click the `Send` button to send it again:

![](https://i.imgur.com/8htLo5a.png)

As we can see, we could easily modify the command and instantly get its output by using Burp `Repeater`. Try doing the same in `ZAP Request Editor` and `ZAP HUD` to see how they work.

Finally, we can see in our previous POST request that the data is URL-encoded. This is an essential part of sending custom HTTP requests, which we will discuss in the next section.
# Encoding/Decoding

As we modify and send custom HTTP requests, we may have to perform various types of encoding and decoding to interact with the webserver properly. Both tools have built-in encoders that can help us in quickly encoding and decoding various types of text.

---
## URL Encoding

It is essential to ensure that our request data is URL-encoded and our request headers are correctly set. Otherwise, we may get a server error in the response. This is why encoding and decoding data becomes essential as we modify and repeat web requests. Some of the key characters we need to encode are:

- `Spaces`: May indicate the end of request data if not encoded
- `&`: Otherwise interpreted as a parameter delimiter
- `#`: Otherwise interpreted as a fragment identifier

To URL-encode text in Burp Repeater, we can select that text and right-click on it, then select (`Convert Selection>URL>URL encode key characters)`, or by selecting the text and clicking `CTRL+U`. Burp also supports URL-encoding as we type if we right-click and enable that option, which will encode all of our text as we type it. 

On the other hand, ZAP should automatically URL-encode all of our request data in the background before sending the request, though we may not see that explicitly.

There are other types of URL-encoding, like `Full URL Encoding` or `Unicode URL` encoding, which may also be helpful for requests with many special characters. 

---
## Decoding

While URL-encoding is key to HTTP requests, it is not the only type of encoding we will encounter. It is very common for web applications to encode their data, so we should be able to quickly decode that data to examine the original text. On the other hand, back-end servers may expect data to be encoded in a particular format or with a specific encoder, so we need to be able to quickly encode our data before we send it.

The following are some of the other types of encoders supported by both tools:

- HTML
- Unicode
- Base64
- ASCII Hex

To access the full encoder in Burp, we can go to the `Decoder` tab. In ZAP, we can use the `Encoder/Decoder/Hash` by clicking `CTRL+E`. With these encoders, we can input any text and have it quickly encoded or decoded. 

For example, perhaps we came across the following cookie that is base64 encoded, and we need to decode it: `eyJ1c2VybmFtZSI6Imd1ZXN0IiwgImlzX2FkbWluIjpmYWxzZX0=`

We can input the above string in Burp Decoder and select `Decode as > Base64`, and we'll get the decoded value:

![](https://i.imgur.com/2w9Ivwn.png)

In recent versions of Burp, we can also use the `Burp Inspector` tool to perform encoding and decoding (among other things), which can be found in various places like `Burp Proxy` or `Burp Repeater`.:

![](https://i.imgur.com/7DTEgCg.png)

In ZAP, we can use the `Encoder/Decoder/Hash` tool, which will automatically decode strings using various decoders in the `Decode` tab:

![](https://i.imgur.com/lM4W4OT.png)

> [!tip]
> Tip: We can create customized tabs in ZAP's Encoder/Decoder/Hash with the "Add New Tab" button, and then we can add any type of encoder/decoder we want the text to be shown in. Try to create your own tab with a few encoders/decoders.

---
## Encoding

As we can see, the text holds the value `{"username":"guest", "is_admin":false}`. So, if we were performing a penetration test of a web application and find that the cookie holds this value, we may want to test modifying it to see whether it changes our user privileges. So, we can copy the above rule, change `guest` to `admin`, and `false` to `true`, and try to encode it again using its original encoding method (`base64`):

![](https://i.imgur.com/SuBNBta.png)
![](https://i.imgur.com/XGQbqgy.png)

> [!tip]
> Tip: Burp Decoder output can be directly encoded/decoded with a different encoder. Select the new encoder method in the output pane at the bottom, and it will be encoded/decoded again. In ZAP, we can copy the output text and paste it in the input field above.

We can then copy the base64 encoded string and use it with our request in Burp `Repeater` or ZAP `Request Editor`. The same concept can be used to encode and decode various types of encoded text to perform effective web penetration testing without utilizing other tools to do the encoding.
# Proxying Tools

An important aspect of using web proxies is the interception of web requests made by command line tools and thick client applications. This gives us transparency into the web requests made by these applications and allows us to utilize all of the different proxy features we have used with web applications.

To route all web requests made by a specific tool through our web proxy tools, we have to set them up as the tool's proxy (i.e. `http://127.0.0.1:8080`), similarly to what we did with our browsers. Each tool may have a different method for setting it's proxy, so we may have to investigate how to do so for each one.

This section will cover a few examples of how to use web proxies to intercept web requests made by such tools. You may either use Burp or ZAP, as the setup process is the same.

> [!NOTE]
> Note: Proxying tools usually slows them down, therefore, only proxy tools when you need to investigate their requests, and not for normal usage.
## Proxychains

One very useful tool in Linux is [proxychains](https://github.com/haad/proxychains), which routes all traffic coming from any command-line tool to any proxy we specify. `Proxychains` adds a proxy to any command-line tool and is hence the simplest and easiest method to route web traffic of command-line tools through out web proxies. 

To use `proxychains`, we first have to edit `/etc/proxychains.conf`, comment out the final line and add the following line at the end of it:

```shell
#socks4         127.0.0.1 9050
http 127.0.0.1 8080
```

We should also enable `Quiet Mode` to reduce noise by uncommenting `quiet_mode`. Once that's done, we can prepend `proxychains` to any command, and the traffic of that command should be routed through `proxychains` (i.e. our web proxy). For example, let's try using `cURL` on one of our previous exercises:

```shell
trop3n@htb[/htb]$ proxychains curl http://SERVER_IP:PORT

ProxyChains-3.1 (http://proxychains.sf.net)
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Ping IP</title>
    <link rel="stylesheet" href="./style.css">
</head>
...SNIP...
</html>  
```

We see that it worked just as it normally would, with the additional `ProxyChains-3.1` line at the beginning, to note that it is being routed through `proxychains`. If we go back to our web proxy (Burp in this case), we will see that the request has indeed gone through it:

![](https://i.imgur.com/FOgGY9j.png)
## Nmap

Next, let's try to proxy `nmap` through our web proxy. To find out how to use the proxy configurations for any tool, we can view its manual with `man nmap`, or it's help page with `nmap -h`

```shell
trop3n@htb[/htb]$ nmap -h | grep -i prox

  --proxies <url1,[url2],...>: Relay connections through HTTP/SOCKS4 proxies
```

As we can see, we can use the `--proxies` flag. We should also add the `-Pn` flag to skip host discovery (as recommended on the man page). Finally, we'll also use the `-sC` flag to examine what an nmap script scan does:

```bash
trop3n@htb[/htb]$ nmap --proxies http://127.0.0.1:8080 SERVER_IP -pPORT -Pn -sC

Starting Nmap 7.91 ( https://nmap.org )
Nmap scan report for SERVER_IP
Host is up (0.11s latency).

PORT      STATE SERVICE
PORT/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 0.49 seconds
```

Once again, if we go to our web proxy tool, we will see all of the requests made by nmap in the proxy history:

![](https://i.imgur.com/AaQ0seP.png)

> [!NOTE]
> Note: Nmap's built-in proxy is still in its experimental phase, as mentioned by its manual (`man nmap`), so not all functions or traffic may be routed through the proxy. In these cases, we can simply resort to `proxychains`, as we did earlier.
## Metasploit

Finally, let's try to proxy web traffic made in Metasploit to better investigate and debug them. We should begin by starting Metasploit with `msfconsole`. Then, to set a proxy for any exploit within Metasploit, we can use the `set PROXIES` flag. Let's try the `robots.txt` scanner as an example and run it against one of our previous exercises:

```shell
trop3n@htb[/htb]$ msfconsole

msf6 > use auxiliary/scanner/http/robots_txt
msf6 auxiliary(scanner/http/robots_txt) > set PROXIES HTTP:127.0.0.1:8080

PROXIES => HTTP:127.0.0.1:8080


msf6 auxiliary(scanner/http/robots_txt) > set RHOST SERVER_IP

RHOST => SERVER_IP


msf6 auxiliary(scanner/http/robots_txt) > set RPORT PORT

RPORT => PORT


msf6 auxiliary(scanner/http/robots_txt) > run

[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```

Once again, we can go back to our web proxy tool of choice and examine the proxy history to view all sent requests:

![](https://i.imgur.com/E8dSh24.png)

We see that the request has indeed gone through our web proxy. The same method can be used with other scanners, exploits, and other features in Metasploit.

We can similarly use our web proxies with other tools and applications, including scripts and thick clients. All we have to do is set the proxy of each tool to use our web proxy. This allows us to examine exactly what these tools are sending and receiving and potentially repeat and modify their requests while performing web application pentesting.
# Burp Intruder
> [[Burp Suite - Intruder]]

Both Burp and ZAP provide additional features other than the default web proxy, which are essential for web application penetration testing. Two of the most important extra features are `web fuzzers` and `web scanners`. The built-in web fuzzers are powerful tools that act as:

- web fuzzing
- enumeration
- brute-forcing tools

This may also act as an alternative for the many CLI-based fuzzers we use, like `ffuf`, `dirbuster`, `gobuster`, `wfuzz`, among others. 

Burp's web fuzzer is called `Burp Intruder`, and can be used to fuzz:

- pages
- directories
- sub-domains
- parameters
- parameters values
- many other things

Though it is much more advanced than most CLI-based web fuzzing tools, the free `Burp Community` version is **throttled** at a speed of **1 request per second**, making it extremely slow compared to CLI-based web fuzzing tools, which can usually read up to **10k requests per second**. This is why we would only use the free version of Burp Intruder for ***short queries***. The `Pro` version has unlimited speed, which can rival common web fuzzing tools, in addition to the very useful features of Burp Intruder. This makes it one of the best web fuzzing and brute-forcing tools. 

In this section, we will demonstrate the various uses of Burp Intruder for web fuzzing and enumeration.

---
## Target

As usual, we'll start Burp and its pre-configured browser and then visit the web application from the exercise at the end of this section. Once we do, we can go to the Proxy History, locate our request, then right-click on the request and select `Send to Intruder`, or use the shortcut `CTRL+I` to send it to `Intruder`.

We can then go to `Intruder` by clicking on its tab or with the shortcut `CTRL+SHIFT+I`, which takes us right to `Burp Intruder`.

![](https://i.imgur.com/6CWtOj4.png)

On the first tab, `'Target'`, we see the details of the target we will be fuzzing, which is fed from the request we sent to `Intruder`.

---
## Positions

The second tab, '`Positions`', is where we place the payload position pointer, which is the point where words from our wordlist will be placed and iterated over. We will be demonstrating how to fuzz web directories, which is similar to what's done by tools like `ffuf` or `gobuster`. 

To check whether a web directory exists, our fuzzing should be in '`GET /DIRECTORY/`', such that existing pages would return `200 OK`, otherwise we'd get `404 Not Found`. So, we will need to select `DIRECTORY` as the payload position, by either wrapping it with `§` or selecting the word `DIRECTORY` and clicking on the `Add §` button:

![](https://i.imgur.com/lNWdQxX.png)

> [!TIP]
> The `DIRECTORY` in this case is the pointer's name, which can be anything, and can be used to refer to each pointer, in case we are using more than position with different wordlists for each.

The final thing to select in the target tab is the `Attack Type`. The attack type defines how many payload pointers are used and determines which payload is assigned to which position. For simplicity, we'll stick to the first type, `Sniper`, which uses only one position. Try clicking on the `?` at the top of the window to read more about attack types, or check out this [link](https://portswigger.net/burp/documentation/desktop/tools/intruder/positions#attack-type).

> [!NOTE]
> Be sure to leave the **extra two lines** at the end of the request, otherwise we may get an error response from the server.
## Payloads

On the third tab, '`Payloads`', we get to choose and customize our payloads/wordlists. This payload/wordlist is what would be iterated over, and each element/line of it would be placed and tested one by one in the Payload Position we chose earlier. These are four main things we need to configure:

- Payload Sets
- Payload Options
- Payload Processing
- Payload Encoding
### Payload Sets

The first thing we must configure is the `Payload Set`. The payload set identifies the Payload number, depending on the attack type and number of payloads we used in the Payload Position Pointers:

![](https://i.imgur.com/xi3Wz3j.png)

In this case, we only have one Payload Set, as we chose the `Sniper` Attack type with only one payload position. If we have chosen the "`Cluster Bomb`" attack type, for example, and added several payload positions, we would get more payload sets to choose from and choose different options for each. In our case, we'll select `1` for the payload set.

Next, we need to select the `Payload Type`, which is the type of payloads/wordlists we will be using. Burp provides a variety of Payload Types, each of which acts in a certain way. For example:

- `Simple List`: The basic and most fundamental type. we provide a wordlist, and Intruder iterates over each line in it. 
- `Runtime File`: Similar to `Simple List`, but loads line-by-line as the scan runs to avoid excessive memory usage in Burp.
- `Character Substitution`: Lets us specify a list of characters and their replacements, and Burp Intruder tries all potential permutations. 

There are many other Payload Types, each with its own options, and many of which can build custom wordlists for each attack. Try clicking on the `?` next to `Payload Sets`, and then click on `Payload Type`, to learn more about each Payload Type. In our case, we'll be going with a basic `Simple List`.
### Payload Options

Next, we must specify the Payload Options, which is different for each Payload Type we select in `Payload Sets`. For a `Simple List`, we have to create or load a wordlist. To do so, we can input each item manually by clicking `Add`, which would build our wordlist on the fly. The other more common option is to click on `Load`, and then select a file to load into `Burp Intruder`.

We will select `/opt/useful/seclists/Discovery/Web-Content/common.txt` as our wordlist. We can see that Burp Intruder loads all line of our wordlist into the Payload Options table:

![](https://i.imgur.com/3yUDXpO.png)

We can add another wordlist or manually add a few items, and they would be appended to the same list of items. We can use this to combine multiple wordlists or create custom wordlists. In Burp Pro, we also can select from a list of existing wordlists contained within Burp by choosing from the `Add from List` menu option.

