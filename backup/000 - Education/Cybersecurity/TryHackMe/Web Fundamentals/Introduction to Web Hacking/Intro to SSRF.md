

The below example shows how the attacker can have complete control over the page requested by the webserver.  
The Expected Request is what the website.thm server is expecting to receive, with the section in red being the URL that the website will fetch for the information.  
The attacker can modify the area in red to an URL of their choice.

The below example shows how an attacker can still reach the /api/user page with only having control over the path by utilizing directory traversal. When website.thm receives ../ this is a message to move up a directory which removes the /stock portion of the request and turns the final request into /api/user

In this example, the attacker can control the server's subdomain to which the request is made. Take note of the payload ending in **&x=** being used to stop the remaining path from being appended to the end of the attacker's URL and instead turns it into a parameter (?x=) on the query string

Going back to the original request, the attacker can instead force the webserver to request a server of the attacker's choice. By doing so, we can capture request headers that are sent to the attacker's specified domain. These headers could contain authentication credentials or API keys sent by website.thm (that would normally authenticate to api.website.thm).
## Finding an SSRF

Potential SSRF vulnerabilities can be spotted in web applications in many different ways. Here is an example of four common places to look:

> When a full URL is used in a parameter in the address bar.

> A hidden field in a form.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/f3c387849e91a4f15a7b59ff7324be75.png)

> A partial URL such as just the hostname.

> Only the path of the URL:

Some of these example are easier to exploit than others, and this is where a lot of ***trial and error*** will be required to find a working payload. 

If working with a blind SSRF where no output is reflected back to you, you'll need to use an external HTTP logging tool to monitor requests such as requestbin.com, your own personal HTTP server or **BurpSuite's Collaborator Client**.

## Defeating Common SSRF Defenses

More security-savvy developers are aware of the risks of SSRF vulnerabilities and may implement checks in their applications to make sure the requested resource meets specific rules. There are usually two approaches to this, either a deny list or an allow list. 
### Deny List

A ***deny list*** is where all requests are accepted apart from resources specified in a list or matching a particular pattern. A Web Application may employ a deny list to protect sensitive endpoints, IP addresses or domains from being accessed by the public while still allowing access to other locations. A specific endpoint to restrict access is the localhost, which may contain server performance data or further sensitive information, so domain names such as *localhost* and *127.0.0.1* would appear on a deny list.

Attackers can bypass a Deny List by using alternative localhost references such as 0, 0.0.0.0, 0000, 127.1, 127.(`*`).(`*`).(`*`), 2130706433, 017700000001 or subdomains that have a DNS record that points to the IP address 169.254.169.254.

Also, in a cloud environment, it would be beneficial to block access to the IP address 169.254.169.254, which contains *metadata for the deployed cloud server*, including possibly sensitive information. An attacker can bypass this by registering a subdomain on their own domain with a DNS record that points to the IP Address 169.254.169.254.
### Allow List

An allow list where all requests get denied unless they appear on a list or match a particular pattern, such as a rule that a URL used in a parameter must begin with **https://website.thm**. An attacker could quickly circumvent this rule by creating a subdomain on an attacker's domain name, such as https://website.thm.attackers.domain.thm. The application logic would now allow this input and let an attacker control the internal HTTP request. 
### Open Redirect

If the above bypasses do not work, there is one more trick up the attacker's sleeve, the open redirect. An open redirect is an endpoint on the server where the website visitor gets automatically redirected to another website address. Take, for example, the link https://website.thm/link?url=https://tryhackme.com. 

This endpoint was created to record the number of times visitors have clicked on this link for advertising/marketing purposes. But imagine there was a potential SSRF vulnerability with stringent rules which only allowed URLs beginning with https://website.thm/. An attacker could utilize the above feature to redirect the internal HTTP request to a domain of the attacker's choice.
## SSRF Practical

Let's put what we've learned about SSRF into a a fictional test scenario.

We've come across two new endpoints during a content discovery exercise against the **Acme IT Support** website. The first one is **/private**, which gives us an error message explaining that the contents cannot be viewed from our IP address. The second is a new versions of the customer account page at **/customers/new-account-page** with a new feature allowing customers to choose an avatar for their account.

First, create a customer account and log in. Once we've signed in, visit [https://10-10-169-230.p.thmlabs.com/customers/new-account-page](https://10-10-169-230.p.thmlabs.com/customers/new-account-page) to view the new avatar selection feature. By viewing the page source of the avatar form, you'll see the avatar form field value contains the path to the image. The background-image style can confirm this in the above DIV element as per the screenshot below:

If we choose one of the avatars and then click the **Update Avatar** button, we'll see the form change, and, above it, display our currently connected avatar.

Viewing the source of the page will show the current avatar is displayed using the data URI scheme, and the image content is base64 encoded as per the screenshot below.

Now, let's try making the request again but changing the avatar value to private in hopes that the server will access the resource and get past the IP address book. 

To do this, first, right-click one of the radio buttons on the avatar form and select **Inspect**.

Be sure to select the avatar we edited and then click the **Update Avatar** button. Unfortunately, it looks like the web application has a deny list in place and has blocked access to the /private endpoint.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5efe36fb68daf465530ca761/room-content/a59460cc19eaf5776ee8a882e25b2d64.png)

As we can see from the error message, the path cannot start with /private but don't worry, we've still got a trick up our sleeve to bypass this rule. We can use a directory traversal trick to reach our desired endpoint. Try setting the avatar value to **x/../private**.

We'll see we have no bypassed the rule, and the user updated the avatar. This trick works because when the web server receives the request for **x/../private**, it knows that the `../` string means to move up a directory that now translates the request to just `/private`. 

Viewing the page source of the avatar form, you'll see the currently set avatar now contains the contents from the private directory in base64 encoding, decode this content and it will reveal a flag.

