
**What is IDOR?**

IDOR stands for ***Insecure Direct Object Reference*** and is a type of *access control vulnerability.*

This type of vulnerability can occur when a web server receives user-supplied input to retrieve objects (files, data, documents), too much trust has been placed on the input data, and it is not validated on the server-side to confirm the requested object belongs to the user requesting it.

## An IDOR Example

Imagine you've just signed up for an online service, and you want to change your profile information. The link you clock on goes to http://online-service.thm/profile?user_id=1305, and you can see your information.

Curiosity gets the better of you, and you try changing the `user_id` value to 1000 instead (http://online-service.thm/profile?user_id=1000), and to your surprise, you can now see another user's information. You've now discovered an IDOR vulnerability. Ideally, there should be a check on the website to confirm that the user information belongs to the user logged in to request it.

## Finding IDORs in Encoded IDs

When passing data from page to page either by post data, query strings or cookies, web developers will often first take the raw data and encode it. Encoding ensures that the receiving web server will be able to understand the contents. Encoding changes binary data into ASCII string commonly using the `a-z, A-Z, 0-9 and =` character for padding. 

The most common encoding technique on the web is base64 encoding and that can usually be pretty easy to spot. You can use websites like [https://www.base64decode.org/](https://www.base64decode.org/) to decode the string, then edit the data and re-encode it again using [https://www.base64encode.org/](https://www.base64encode.org/) and then resubmit the web request to see if there is a change in the response.

See the image below as a graphical reference for this process:
## Hashing IDORs in Hashed IDs

Hashed IDs are a little bit more complicated to deal with than encoded ones, but they follow a predictable pattern, such as being the hashed version of the integer value. For example, the Id number 123 would become `202cb962ac59075b964b07152d234b70` if md5 hashing were in use. 

It's worthwhile putting any discovered hashes through a web service such as [https://crackstation.net/](https://crackstation.net/) (which has a database of billions of hash to value results) to see if we can find any matches.

## Finding IDORs in Unpredictable IDs

If the ID cannot be detected using the above methods, an excellent of IDOR detection is to create two accounts and swap the ID numbers between them. If you can view the other users' content using their ID number while still being logged in with a different account (or not logged in at all), you've found *a valid IDOR vulnerability*.

## Where are IDORs Located?

The vulnerable endpoint we're targeting may not always be something you see in the address bar. It could be content your browser loads in via an AJAX request or something that you find referenced in a JavaScript file.

Sometimes endpoints could have an unreferenced parameter that may have been of some use during development and got pushed to production. For example, you may notice a call to `/user/details` displaying your user information (authenticated through your session). But through an attack known as ***parameter mining***, you discover a parameter called **user_id** that you can use to display other users' information, for example, **/user/details?user_id=123**.

## A Practical IDOR Example

Firstly you'll need to log in. To do this, click on the customer's section and create an account. Once logged in, click on the **Your Account** tab. [https://10-10-119-36.p.thmlabs.com](https://10-10-119-36.p.thmlabs.com)

The **Your Account** section gives you the ability to change your information such as username, email address and password. You'll notice the username and email fields pre-filled in with your information.

We'll start by investigating how this information gets pre-filled. If you open the browser dev tools, select the network tab and then refresh the page, you'll see a call to an endpoint with the path `/api/v1/customer?id={user_id}`.

This page returns in JSON format your user ID, username and email address. We can see from the path that the user information shown is taken from the query string's id parameter (see below image).


