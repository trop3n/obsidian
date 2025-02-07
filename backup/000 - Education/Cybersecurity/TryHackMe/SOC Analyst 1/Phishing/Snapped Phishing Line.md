Apply learned skills to probe malicious emails and URLs, exposing a vast phishing campaign

![](https://i.imgur.com/3ukIByS.png)

## Task 1: Challenge Scenario[](https://blog.davidvarghese.dev/posts/tryhackme-snapped-phishing-line/#task-1-challenge-scenario)

### Premise Setup[](https://blog.davidvarghese.dev/posts/tryhackme-snapped-phishing-line/#premise-setup)

#### Disclaimer[](https://blog.davidvarghese.dev/posts/tryhackme-snapped-phishing-line/#disclaimer)

Based on real-world occurrences and past analysis, this scenario presents a narrative with invented names, characters, and events.

**Please note:** The phishing kit used in this scenario was retrieved from a real-world phishing campaign. Hence, it is advised that interaction with the phishing artifacts be done only inside the attached VM, as it is an isolated environment.

#### An Ordinary Midsummer Day…[](https://blog.davidvarghese.dev/posts/tryhackme-snapped-phishing-line/#an-ordinary-midsummer-day)

As an IT department personnel of SwiftSpend Financial, one of your responsibilities is to support your fellow employees with their technical concerns. While everything seemed ordinary and mundane, this gradually changed when several employees from various departments started reporting an unusual email they had received. Unfortunately, some had already submitted their credentials and could no longer log in.

You now proceeded to investigate what is going on by:

1. Analyzing the email samples provided by your colleagues.
2. Analyzing the phishing URL(s) by browsing it using Firefox.
3. Retrieving the phishing kit used by the adversary.
4. Using CTI-related tooling to gather more information about the adversary.
5. Analyzing the phishing kit to gather more information about the adversary.

The email titled **Quote for Services Rendered processed on June 29 2020 100132 AM** was sent to **William McClean** and contains an **PDF** attachment. The mail was sent from the email id **Accounts.Payable@groupmarketingonline.icu**

### Question 1

> Who is the individual who recieved an email attachment containing a PDF?

Look through the emails provided in the `phish-emails` directory and locate the email with the attached .pdf file.

That person is ***William McClean***.
### Question 2

> What email address was used by the adversary to send the phishing email?

Look through the emails at the sender's address. This will provide the answer to the question.

Answer: ***Accounts.Payable@groupmarketing[.]icu***

The emails that were sent to the other employees are all identical. All of them also contain an `HTML` file as an attachment.

![](https://i.imgur.com/Uq7EPty.png)

![](https://i.imgur.com/wSgBXSC.png)

The HTML contains a link that points to `kennaroadz.buzz`. When the HTML file is opened with a web browser it leads to a page that looks like the Microsoft Login page.

![](https://i.imgur.com/KQNnuoT.jpeg)

> **Converting URL to Defanged Format**  
> All the periods (.) that are present in the URL along with the `://` symbol that is present after the protocol should be enclosed in square brackets. Then all the t’s that are present in the protocol name (HTTP/HTTPS) has to be replaced with the letter `x`.
> 
> [Defang all the things! - SANS Internet Storm Center](https://isc.sans.edu/diary/Defang+all+the+things/22744)
### Question 3

> What is the redirection URL to the phishing page for the individual Zoe Duncan?

```
hxxp[://]kennaroads[.]buzz/data/Update365/office365/40e7baa2f826a57fcf04e5202526f8bd/?email=zoe[.]duncan@swiftspend[.]finance&error
```

On enumerating the URL the link to the malicious code can be found.

![](https://i.imgur.com/i9JfuPp.png)

This attachment can be entered into the URL after `/data/` in order to find the answer to the next question.
### Question 4

> What is the URL to the .zip archive of the phishing kit? (defanged format)

Answer: ***hxxp[://]kennaroads[.]buzz/data/Update365[.]zip***

To find the has of the file use CyberChef which is pre-installed on the VM (present in the "tools" folder). Load the file into the input field and use the SHA2 function with a hash size set to 256.

![](https://i.imgur.com/siMBCGd.png)
### Question 5

> What is the SHA256 hash of the phishing kit archive?

Answer: ***ba3c15267393419eb08c7b2652b8b6b39b406ef300ae8a18fee4d16b19ac9686***

To find the time at which the phishing kit and domain were first flagged as malicious use VirusTotal. The site has to be opened on our local machine as the VM does not have internet access.

[VirusTotal - Home](https://www.virustotal.com/gui/home/upload)

![](https://i.imgur.com/uExS1sy.png)
### Question 6

> When was the phishing kit archive first submitted? (format: YYYY-MM-DD HH:MM:SS UTC)

Answer: ***2020-04-08 21:55:50 UTC***

![](https://i.imgur.com/BRaydc1.png)
## Question 7

> When was the phishing domain that was used to host the phishing kit archive first registered (format: YYYY-MM-DD)

Answer: ***2020-06-25***

On further enumerating the domain used by the adversary a `log.txt` file can be found that contains the details collected from the users who fell for the phishing attack.

![](https://i.imgur.com/5QYOJbk.png)

![](https://i.imgur.com/2oMh2ed.png)
### Question 8

> What was the email address of the user who submitted their password twice?

To find the email ids used by the adversary the malicious package has to be downloaded.

By going through each file in the package the emails that are used can be found. Alternatively, using `grep` and a simple **regex condition** all patterns in the code that look like an email id can be listed.

![](https://i.imgur.com/lWOWXVz.png)
### Question 9

> What was the email address used by the adversary to collect compromised credentials?

Answer: ***m3npat@yandex[.]com***
### Question 10

> The adversary used other email addresses in the obtained fishing kit. What is the email address that ends in "@gmail.com"?

Answer: ***jamesstanner2299@gmail[.]com***

Finding the answer can be done in the same way as the last question.

Finding the flag in this room is a little tricky. But if we follow the hint word for word it can be found. 

The hint mentions that the file with the flag is called flag and has the extension `.txt`. On enumerating all the directories on the domain for a file called `flag.txt` the flag will eventually get displayed.

![](https://i.imgur.com/M8TYaU9.png)

The flag is in an encoded format. On using the Magic function in CyberChef the encoding is identified as Base64. The output appears to be in reverse. So to get the decoded flag the Magic function should be replaced with the Base64 function followed by the Reverse function.

![](https://i.imgur.com/54DVzk1.png)

### Question 11

**What is the hidden flag?**

> THM{pL4y_w1Th_tH3_URL}

