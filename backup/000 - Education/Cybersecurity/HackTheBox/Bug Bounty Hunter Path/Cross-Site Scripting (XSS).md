#crosssitescripting #xss #bugbounty #webhacking #hackthebox 
# Introduction

As web applications become more advanced and more common, so do web application vulnerabilities. Among the most common types of web application vulnerabilities are [Cross-Site Scripting (XSS)](https://owasp.org/www-community/attacks/xss/) vulnerabilities. XSS vulnerabilities take advantage of a flaw in user input sanitization to "write" JavaScript code to the page and execute it on the client side, leading to several types of attacks.
## What is XSS

A typical web application works be receiving HTML code from the back-send sever and rendering it on the client-side internet browser. When a vulnerable web application does not properly sanitize user input, a malicious user can inject extra JavaScript code in an input field (e.g. comment/reply). so once another user views the same page, they unknowingly execute the malicious JavaScript code. 

XSS vulnerabilities are solely executed on the client-side and hence do not directly affect the back-end server. They can only affect the user executing the vulnerability. The direct impact of XSS attacks on the back-end sever may be relatively low, but they are very commonly found in web applications, so this equates to a medium risk (`low impact + high probability = medium risk`), which we should always attempt to `reduce` by detecting, remediating, and proactively preventing these types of vulnerabilities.

![[HTB_XSS_RiskTable.png]]
## XSS Attacks

XSS vulnerabilities can facilitate a wide range of attacks, which can be anything that can be executed through browser JavaScript code. A basic example of an XSS attack is having the target user unwittingly send their session cookie to the attacker's web server. Another example is having the target's browser execute API calls that lead to a malicious action, like changing the user's password to a password of the attacker's choosing. There are many other types of XSS attacks, from Bitcoin mining to displaying ads.

As XSS attacks execute JavaScript code within the browser, they are limited to the browser's JS engine, (i.e. V8 in Chrome). They cannot execute *system-wide* JavaScript code to do something like **system-level code execution**. In modern browsers, they are also limited to the same domain of the vulnerable website. Nevertheless, being able to execute JavaScript in a user's browser may still lead to a wide variety of attacks, as mentioned above. In addition to this, if a skilled researcher identifies a **binary vulnerability** in a web browser (e.g. a Heap overflow in Chrome), they can utilize an XSS vulnerability to execute a JavaScript payload on the target's browser, which eventually breaks out of the browser's sandbox and executes code on the user's machine.

XSS vulnerabilities may also be found in almost all modern web applications and have been actively exploited for the past two decades. A well known XSS example is the [Samy Worm](https://en.wikipedia.org/wiki/Samy_(computer_worm)), which was a browser-based worm that exploited a stored XSS vulnerability in the social networking website MySpace back in 2005. It executed when viewing an infected webpage by posting a message on the victim's MySpace page that read, "Samy is my hero." The message itself also contained the same JavaScript payload to re-post the same message when viewed by others. Within a single day, more than a million MySpace users had this message posted on their pages. Even though this specific payload did not do any actual harm, the vulnerability could have been used for much more nefarious purposes, like stealing user's credit card info, installing keyloggers on their browsers, or even exploiting a binary vulnerability in user's web browsers (which was 
more common in web browsers back then).

In 2014, a security researcher accidentally identified an [XSS vulnerability](https://blog.sucuri.net/2014/06/serious-cross-site-scripting-vulnerability-in-tweetdeck-twitter.html) in Twitter's TweetDeck dashboard. This vulnerability was exploited to create a [self-retweeting tweet](https://twitter.com/derGeruhn/status/476764918763749376) in Twitter, which led to the tweet being retweeted more than 38,000 times in under two minutes. Eventually, it forced Twitter to [temporarily shut down TweetDeck](https://www.theguardian.com/technology/2014/jun/11/twitter-tweetdeck-xss-flaw-users-vulnerable) while they patched the vulnerability.

To this day, even the most prominent web applications have XSS vulnerabilities that can be exploited. Even Google's search engine had multiple XSS vulnerabilities in its search bar, the most recent of which was in [2019](https://www.acunetix.com/blog/web-security-zone/mutation-xss-in-google-search/) when an XSS vulnerability was found in the XML library. Furthermore, the Apache Server, the most commonly used web server on the internet, once reported an [XSS Vulnerability](https://blogs.apache.org/infra/entry/apache_org_04_09_2010) that was being actively exploited to steal user passwords of certain companies. All of this tells us that XSS vulnerabilities should be taken seriously, and a good amount of effort should be put towards detecting and preventing them.
## Types of XSS

There are three main types of XSS vulnerabilities:

| Type                             | Description                                                                                                                                                                                                                                   |
| -------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Stored (Persistent) XSS`        | The most critical type of XSS, which occurs when user input is stored on the back-end database and then displayed upon retrieveal (e.g. posts or comments)                                                                                    |
| `Reflected (Non-Persistent) XSS` | Occurs when user input is displayed on the page after being processed by the backend server, but without being stored (e.g. search result or error message)                                                                                   |
| `DOM-based XSS`                  | Another Non-Persistent XSS type that occurs when user input is directly shown in the browser and is completely processed on the client-side, without reaching the back-end server, (e.g. through client-side HTTP parameters or anchor tags). |
We will cover each of these types in the upcoming sections and work through exercises to see how each of them occurs, and then we will also see how each of them can be utilized in attacks.
# Stored XSS

Before we learn how to discover XSS vulnerabilities and utilize them for various attacks, we must first understand the different types of XSS vulnerabilities and and their differences to know which to use in each kind of attack.

The first and most critical type of XSS vulnerability is `Stored XSS` or `Persistent XSS`. If our injected XSS payload gets stored in the back-end database and retrieved upon visiting the page, this means that our XSS attack is persistent and may affect any user the visits the page. 

This type of XSS is the most critical, as it affects a much wider audience since any user who visits the page would be a victim of this attack. Furthermore, Stored XSS may not be easily removeable, and the payload may need removing from the back-end database.

We can start the server below to view and practice a stored XSS example. As we can see, the web page is a simple `To-Do List` app that we can add items to. We can try typing `test` and hitting enter/return to add a new item to see how the page handles it. 

![](https://i.imgur.com/LKOwjhT.png)

As we can see, our input was displayed on the page. If no sanitization or filtering was applied to our input, the page might be vulnerable to XSS.
## XSS Testing Payloads

We can test whether the page is vulnerable to XSS with the following basic XSS payload:

```html
<script>alert(window.origin)</script>
```

We use this payload as it is a very easy-to-spot method to know when our XSS payload has been successfully executed. Suppose the page allows any input and does not perform any sanitization on it. In that case, the alert should pop up with the URL of the page it is being executed on, directly after we input our payload or when we refresh the page:

![](https://i.imgur.com/ArNNaR1.png)

As we can see, we did indeed get the alert, which means that the page is vulnerable to XSS, since our payload executed successfully. We can confirm this further by looking at the page source by clicking [`CTRL+U`] or right-clicking and selecting `View Page Source`, and we should see our payload in the page source:

```html
<div></div><ul class="list-unstyled" id="todo"><ul><script>alert(window.origin)</script>
</ul></ul>
```

> [!TIP]
> **Tip**: Many modern web applications utilize cross-domain iFrames to handle user input, so that even if the web form is vulnerable to XSS, it would not be a vulnerability on the main web application. This is why we are showing the value of `window.origin` in the alert box, instead of a static value like `1`. In this case, the alert box would reveal the URL it is being executed on, and will confirm which form is the vulnerable one, in case an iFrame was being used. 

As some modern web browsers may block the `alert()` JavaScript function in specific locations, it may be handy to know a few other basic XSS payloads to verify the existence of XSS. One, such XSS payload is `<plaintext>`, which will stop rendering the HTML code that comes after it and display it as plaintext. Another easy-to-spot payload is `<script>print()</script>` that will pop up the browser print dialog, which is unlikely to be blocked by any browsers. Try using these payloads to see how each works. You may see the reset button to remove any current payloads. 

To see whether the payload is persistent and stored on the back-end, we can refresh the page and see whether we get the alert again. If we do, we would see that we keep getting the alert even throughout page refreshes, confirming that this is indeed a `Stored/Persistent XSS` vulnerability. This is not unique to us, as any user who visits the page will trigger the XSS payload and get the same alert. 
# Reflected XSS

There are two types of `Non-Persistent XSS` vulnerabilities: `Reflected XSS`, which gets processed by the back-end server, and `DOM-based XSS`, which is completely processed on the client-side and never reaches the back-end server. Unlike Persistent XSS, `Non-Persistent XSS` vulnerabilities are temporary and are not persistent enough through page refreshes. Hence our attacks only affect the targeted user and will not affect other users who visit the page. 

`Reflected XSS` vulnerabilities occur when our input reaches the back-end server and gets returned to us without being filtered or sanitized. There are many cases in which our entire input might get returned to us, like error messages or confirmation messages. In these cases, we may attempt using XSS payloads to see whether they execute. However, as these are usually temporary messages, once we move from the page, they would not execute again, and hence they are `Non-Persistent`.

We can start the server below to practice on a web page vulnerable to a reflected XSS vulnerability. It's a similar `To-Do List` app to the one we practiced in the previous section. We can try adding any `test` string to see how it's handled:

![](https://i.imgur.com/NpG0v8l.png)

As we can see, we get `Task 'test' could not be added.`, which includes our input `test` as part of the error message. If our input was not filtered or sanitized, the page might be vulnerable to XSS. We can try the same XSS payload we used in the previous section and click `Add`:

![](https://i.imgur.com/rypuWAR.png)

Once we click `Add`, we get the alert pop-up:

![](https://i.imgur.com/aXHnaUx.png)

In this case, we see that the error message now says `Task '' could not be added.`. Since our payload is wrapped with a `<script>` tag, it does not get rendered by the browser, so we get empty single quotes `''` instead. We can once again view the page source to confirm that the error message includes our XSS payload:

```html
<div></div><ul class="list-unstyled" id="todo"><div style="padding-left:25px">Task '<script>alert(window.origin)</script>' could not be added.</div></ul>
```

As we can see, the single quotes indeed contain our XSS payload `'<script>alert(window.origin)</script>'`.

If we visit the `Reflected` page again, the error message no longer appears, and our XSS payload is not executed, which means that this XSS vulnerability is indeed `Non-Persistent`.

`But if the XSS vulnerability is Non-Persistent, how would we target victims with it?`

This depends on which HTTP request is used to send our input to the server. We can check this through the Firefox `Developer Tools` by clicking [`CTRL+I`] and selecting the `Network` tab. Then we can put our `test` payload again and click `Add` to send it:

![](https://i.imgur.com/2aDIqws.png)

As we can see, the first row shows that our request was a `GET` request. `GET` request sends their parameters and data as part of the URL. So,. `to target a user, we can send them a URL containing our payload`. To get the URL, we can copy the URL from the URL bar in Firefox after sending our XSS payload, or we can right-click on the `GET` request in the `Network` tab and select `Copy>Copy URL`. Once the victim visits this URL, the XSS payload would execute:

```
http://94.237.61.84:41541/index.php?task=%3Cscript%3Ealert(window.origin)%3C/script%3E
```

![](https://i.imgur.com/3y2UT4B.png)
# DOM XSS

The third and final type of XSS is another `Non-Persistent` type called `DOM-based XSS`. While `reflected XSS` sends the input data to the back-end server through HTTP requests, DOM XSS is completely processed on the client-side through JavaScript. DOM XSS occurs when JavaScript it used to change the page source through `Document Object Model (DOM)`.

We can run the server below to see an example of a web application vulnerable to DOM XSS. We can try adding a `test` item, and we see that the web application is similar to the `To-Do List` web applications we previously used:

