# Introduction

Now that we covered the basics concerning emails in Phishing Emails 1, let's dive right into actual phishing email samples. 

Each email showcased in this room will demonstrate different tactics used to make the phishing emails look legitimate. The more convincing the phishing email appears, the higher the chances the recipient will click on a malicious link, download and execute the malicious file, or even send the prince of some country a wire transfer.

> [!Warning]
> The samples throughout this room contain information from actual spam and/or phishing emails. Proceed with caution if you attempt to interact with any IP, domain, attachment, etc.

# Cancel Your PayPal Order

The email sample in this task will highlight the following techniques:

- **Spoofed Email Address**
- **URL Shortening Services**
- **HTML to Impersonate a Legitimate Brand**

Here are some quick observations about this email sample:

1. This is an unusual email recipient address. This is not the email address associated with the Yahoo account.
2. This mismatch should *immediately stand out*. The sender's details (service@paypal.com) don't match the sender's email address (gibberish(@)sultanbogor(.)com)
3. The subject line hints that you made a purchase or a transaction of some sort. If you don't recall this account, then it will grab your attention. This social engineering tactic is to prompt you to interact with the email with haste.

![](https://i.imgur.com/uBIjkhk.png)

Now let's look at the contents of the email body.

### Email Body Text (Image 1)

![](https://i.imgur.com/YkTWAkx.png)

### **The Second Half of the Body (Image 2)**

![](https://i.imgur.com/1XZt8A7.png)

The email body compliments the sender information and subject line. The email was designed as a legitimate email from PayPal.

There aren't many attachments associated with this email. The only interactive element in this email is the **Cancel the Order** button/link.

Let's investigate that further by reviewing the raw HTML source for the email...

### **Email Hyperlinks**: 

![](https://i.imgur.com/XZo2Yep.png)

The link uses URL shortening services. It is not a good idea to click on the link if you don't know where the link is taking you. Luckily, there are online tools we can use to let us know the destination of a shortened URL.

![](https://i.imgur.com/zPPmKCD.png)

Strange. This link redirects to google.com.

> [!NOTE]
> **Note**: Tools to expand shortened URLs will be discussed in the Phishing Emails 3 room.
# Track Your Package

This email sample will highlight the following techniques:

1. **Spoofed Email Address**
2. **Pixel Tracking**
3. **Link Manipulation**

Here are some quick observations about this email sample:

1. The email is tailored to appear that it's sent from a mail distribution center of some sort.
2. The subject line adds to the pretense with a 'tracking number'.
3. The link in the email body matches the subject line.

![](https://i.imgur.com/3g7X2qp.png)

**Note**: In this email sample, Yahoo blocked the images from automatically loading. Any guesses as to why?

Typically one can hover the cursor over a link to see where the link it pointing to, but in this sample, that technique won't work because Yahoo disabled links in the email. We can look at the raw source code for the email and find out. 
### Email Hyperlinks:

![](https://i.imgur.com/ft62pKF.png)

Here we see an image file, and it's explicitly called **Tracking.png**. These trackers send information back to the spammer's server.

There are many reasons for spammers to embed tracking pixels (very small images) into their spam emails. To read more about this concept, refer to this post on The Verge [here](https://www.theverge.com/22288190/email-pixel-trackers-how-to-stop-images-automatic-download). Now we can understand why Yahoo automatically blocked the images in this email. Many email providers do the same. 

Back to the hyperlink, the link is pointing to a shady-looking domain. The only distribution center this domain can be associated with is malware, but further analysis is the only way to confirm that definitely.
# Select your Email Provider to View Document

This email sample will highlight the following techniques:

- **Urgency**
- **HTML to impersonate a legitimate brand**
- **Link Manipulation**
- **Credential Harvesting**
- **Poor Grammar and/or Typos**

Let's take a closer look...

![](https://i.imgur.com/UpWUCME.png)

Here are some quick observations about this email sample:

1. This email was sent on Thursday, July 15th, 2021
2. A sense of urgency is introduced in this email. Notice that the link to download the fax document expires on the same day.
3. There is an action to perform. In this case, a button to download the fax.

![](https://i.imgur.com/bp49K9Q.png)

The above image shows the victim is redirected to a page created to pass as OneDrive. Notice that the URL is not anything Microsoft-related.

There are two more links for the victim to interact with. The victim has to click either button to obtain the fax document that is set to expire.

![](https://i.imgur.com/tbIMVKT.png)

The victim is directed to yet another site. This one was created to resemble Adobe. Again, notice the URL. It doesn't look like it's related to Adobe. Also, notice the page title in the tab. It's called "Share Point Online", which is a Microsoft product. There are a couple of grammatical errors as well. 

The victim has options to sign in with the email provider of their choice.

![](https://i.imgur.com/iUsfK77.png)

Our victim chose to log in with Outlook because, per the instructions, "To read the document, please enter the valid email credentials that this file was sent to. "; the email was viewed in Outlook.

![](https://i.imgur.com/6q2e3sa.png)

In this sample, we can tell that fake credentials were entered, but even if the victim would have entered valid credentials, the error message would be the same. This scenario happens because the victim is not really authenticating to an email provider. Instead, the credentials that were entered now reside on the criminal's server. The criminal's objective to harvest credentials has been met. 

Lastly, notice more grammatical errors. All this work they put into this, you would think they would run a spell check. 

This email sample was obtained from Any Run. If you wish to interact with the email and see the full analysis, refer to the link below.

- Analysis: [https://app.any.run/tasks/12dcbc54-be0f-4250-b6c1-94d548816e5c/#](https://app.any.run/tasks/12dcbc54-be0f-4250-b6c1-94d548816e5c/#)
# Please Update your Payment Details

This email sample will highlight the following techniques:

- **Spoofed Email Address**
- **Urgency**
- **HTML to Impersonate a Legitimate Brand**
- **Poor Grammar and/or Typos**
- **Attachments**

Here are some quick observations about this email sample:

1. This email is made to appear that it's from Netflix's billing, but the sender address is z99@musacombi[.]online
2. Here is the element of urgency. The account was suspended, so the victim must act quickly. 
3. There is more of this sense of urgency in the email body.

![](https://i.imgur.com/6PNabYa.png)

Also, *notice the different misspellings of the word Netflix*. Not sure what was the purpose of that.

Typically, you see this technique when it comes to [typosquatting](https://www.csoonline.com/article/3600594/what-is-typosquatting-a-simple-but-effective-attack-technique.html), but that wasn't the case here.

![](https://i.imgur.com/EX0CwFC.png)

Ok, so here is the meat and potatoes of this email. Apparently, the victim needs to open the attachment (PDF) to update their Netflix account.

![](https://i.imgur.com/OO97AjB.png)

Notice the phone number for 'Netflix'. At first glance, that is an unusual phone number to send to a US-based victim.

![](https://i.imgur.com/JA7zbqm.png)

The attachment contains an embedded link titled 'Update Payment Account'.

We'll look at this email attachment closer in the upcoming Phishing Emails 3 room.
# Your Recent Purchase

This email sample will highlight the following techniques:

- **Spoofed Email Address**
- **Recipient is BCC'd**
- **Urgency**
- **Poor Grammar and/or Typos**
- **Attachments**

Here are some quick observations about this email sample:

1. This email is made to appear that it's from Apple Support, but the sender's address is gibberish[@]sumpremed[.]com
2. This email wasn't sent directly to the victim's inbox, but rather BCC'd. The recipient email looks like another spoofed email to appear as a legitimate Apple email address.
3. Here is the element of urgency. Action is required on behalf of the victim.

![](https://i.imgur.com/wtjxSjQ.png)

This file extension many not be familiar to you. A .[DOT](https://www.reviversoft.com/en/file-extensions/dot) file is page layout template files associated with Microsoft Word.

![](https://i.imgur.com/DIdN3SX.png)

The above image shows what is contained within the attachment. You can see that the file contains a large image to resemble an App Store receipt. 

Notice the link contains certain keywords related to Apple: `apps` and `ios`.
# DHL Express Courier Shipping Notice

This email sample will highlight the following techniques:

- **Spoofed Email Address**
- **HTML to impersonate a legitimate brand**
- **Attachments**

Here are some quick observations about this email sample:

1. The sender's email doesn't match the company that is being impersonated, which in this case is DHL. 
2. The subject line gives the impression that there is a package DHL will ship for you. 
3. The HTML in the email body was designed to look like it was sent from DHL.

![](https://i.imgur.com/q3PZNmj.png)

Looking at the source code for the email, the link to view the email as a web page doesn't contain an actual destination URL.

![](https://i.imgur.com/2i0y3UG.png)

The only element the victim can interact with in this email is the email attachment, which, in this case is an Excel document.

![](https://i.imgur.com/clZwPyk.png)

The image below shows what is contained within the attachment.

![](https://i.imgur.com/i06I2U8.png)

The attachment runs a payload that throws an error.

![](https://i.imgur.com/M14HMdD.png)

We'll look at this email attachment in closer detail in the upcoming Phishing Emails 3 room.

