---
up: "[[G4G]]"
tags:
  - education/computerprogramming/languages/python/g4g/webscraping
---


# Introduction

In today's digital world, data is the key to unlocking valuable insights, and much of this data is available on the web. But how to you gather large amounts of data from websites efficiently? That's where **Python Web Scraping** comes in. Web scraping, the process of extracting data from websites, has emerged as a powerful technique to gather information from the vast expanse of the internet.

In this tutorial, we'll explore various Python libraries and modules commonly used for web scraping and delve into why Python 3 is the preferred choice for this task. Along with this you will also explore how to use powerful tools like **BeautifulSoup**, **Scapy**, and **Selenium** to scrape any website.
## Essential Packages

The latest verison of Python offers a rich set of tools and libraries specifically designed for web scraping, making it easier than ever to retrieve data from the web efficiently and effectively. 
### Table of Contents

- [Requests Module](https://www.geeksforgeeks.org/python-web-scraping-tutorial/?ref=shm#requests-module)
- [BeautifulSoup Library](https://www.geeksforgeeks.org/python-web-scraping-tutorial/?ref=shm#beautifulsoup-library)
- [Selenium](https://www.geeksforgeeks.org/python-web-scraping-tutorial/?ref=shm#selenium)
- [Lxml](https://www.geeksforgeeks.org/python-web-scraping-tutorial/?ref=shm#lxml)
- [Urllib Module](https://www.geeksforgeeks.org/python-web-scraping-tutorial/?ref=shm#urllib-module)
- [PyautoGUI](https://www.geeksforgeeks.org/python-web-scraping-tutorial/?ref=shm#pyautogui)
- [Schedule](https://www.geeksforgeeks.org/python-web-scraping-tutorial/?ref=shm#schedule)
- [Why Python3 for Web Scraping?](https://www.geeksforgeeks.org/python-web-scraping-tutorial/?ref=shm#why-python3-for-web-scraping)

# Requests Module

The requests library is used for making HTTP requests to a specific URL and returns the response. Python requests provide inbuilt functionalities for managing both the request and response. 

```
pip install requests
```

### Example: Making a Request

Python requests module has several built-in methods to make HTTP requests to specified URI using GET, POST, PATCH or HEAD requests. A HTTP request is meant to either retrieve data from a specified URL or to push data to a server. It works as a request-response protocol between a client and a server. Here we will be using the `GET` request. The `GET` method is used to retrieve information from the given server using a given URI. The `GET` method sends the encoded user information appended to the page request. 

```python
import requests

# making a GET request
r = requests.get('https://geeksforgeeks.org/python-programming-language/')

# check the status code for response received
# success code - 200
print(r)

# print content of request
print(r.content)
```

For more information, refer to our [Python Requests Tutorial](https://www.geeksforgeeks.org/python-requests-tutorial) .

## What is Python Requests Module?

- Requests is an Apache2 licensed HTTP library, that allows to send HTTP/1.1 requests using Python.
- To play with web, Python Requests is a must. Whether it be hitting APIs, downloading entire facebook pages, and much more cool stuff, one will have to make a request to the URL. 
- Requests play a major role in dealing with [REST APIs](https://www.geeksforgeeks.org/rest-api-introduction/), and [Web Scraping](https://www.geeksforgeeks.org/introduction-to-web-scraping/).
- Checkout an example Python Script using Requests and Web Scraping - [Implementing Web Scraping in Python with BeautifulSoup](https://www.geeksforgeeks.org/implementing-web-scraping-python-beautiful-soup/)

## Installing Requests

```
pip install requests
```

The basic method of installation of requests on any operating system is to grab the base files and install requests manually. Requests is actively developed on GitHub, where the code is always available. For code - [visit here](https://github.com/psf/requests). You can either clone the public repository: 

```
git clone git://github.com/psf/requests.git
```

Once you have a copy of the source, you can embed it in your own Python package, or install it into your site-packages easily:

```
cd requestpip install .
```
### Making a Request

Python requests module has several built-in methods to make HTTP requests to specified URL using GET, POST, PUT, PATCH, or HEAD requests. A HTTP request is meant to either retrieve data from a specified URI or to push data to a server. It works as a request-response protocol between a client and a server.

Let's demonstrate how to make a GET request to an endpoint. GET method is used to retrieve information from the given server using a given URI. The GET method sends the encoded user information appended to the page request. The page and the encoded information are separated by the `?` character. 

For example: 

```
htttps://google.com/search?q=hello
```
## How to Make a GET Request Through Python Requests

Python's requests module provides built-in method called `get()` for making a GET request to a specified URI.
#### Syntax

```python
requests.get(url, params={key: value}, args)
```
#### Example

Let's try making a request to GitHub's API for example purposes.

```python
import requests

# Making a GET request
r = requests.get('https://api.github.com/users/naveenkrnl')

# check the status code
# 200 - OK
print(r)

# print content of request
print(r.content)
```

Save this file as request.py and through terminal run:

```
python request.py
```

> [!NOTE]
> For more, visit – [GET method – Python requests](https://www.geeksforgeeks.org/get-method-python-requests/) 

## HTTP Request Methods

| Method                                                                 | Description                                                                                                                                                                                                                                                        |
| ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [GET](https://www.geeksforgeeks.org/get-method-python-requests/)       | GET method is used to retrieve information from the given server using a given URI.                                                                                                                                                                                |
| [POST](https://www.geeksforgeeks.org/post-method-python-requests/)     | POST request method requests that a web server accepts the data enclosed in the body of the request message, most likely for storing it.                                                                                                                           |
| [PUT](https://www.geeksforgeeks.org/put-method-python-requests/)       | The PUT method requests that the enclosed entity be stored under the supplied URI. If the URI refers to an already existing resource, it is modified and if the URI does not point to an existing resource, then the server can create the resource with that URI. |
| [DELETE](https://www.geeksforgeeks.org/delete-method-python-requests/) | The DELETE method deletes the specified resource                                                                                                                                                                                                                   |
| [HEAD](https://www.geeksforgeeks.org/head-method-python-requests/)     | The HEAD method asks for a response identical to that of a GET request, but without the response body.                                                                                                                                                             |
| [PATCH](https://www.geeksforgeeks.org/patch-method-python-requests/)   | It is used for modify capabilities. The PATCH request only needs to contain the changes to the resource, not the complete resource.                                                                                                                                |
### Response Object

When one makes a request to a URI, it returns a response. This Response object in terms of Python is returned by `requests.method()`, method being - get, post, put etc. Response is a powerful object with lots of functions and attributes that assist in normalizing data or creating ideal portions of code. For example, `response.status_code` returns the status code from the headers itself, and one can check if the request was processed successfully or not. Response object can be used to imply lots of features, methods and functionalities.

```python
import requests

# making a get request
response - requests.get('https://api.github.com/')

# print request object
print(response.url)

# print status code
print(response.status_code)
```

Save this file as request.py and run the command:

`python request.py`

Status Code 200 indicates that the request was made successfully.

### Response Methods

| Method                                                                                                          | Description                                                                                                                  |
| --------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| [response.headers](https://www.geeksforgeeks.org/response-headers-python-requests/)                             | `response.headers` returns a dictionary of response headers.                                                                 |
| [response.encoding](https://www.geeksforgeeks.org/response-encoding-python-requests/)                           | `response.encoding` returns the encoding used to decode response.content                                                     |
| [response.elapsed](https://geeksforgeeks.org/response-elapsed-python-requests/)                                 | `response.elapsed` returns a timedelta object with the time elapsed from sending the request to the arrival of the response. |
| [response.close()](https://www.geeksforgeeks.org/response-close-python-requests/)                               | `response.close()` closes the connection to the server.                                                                      |
| [response.content](https://www.geeksforgeeks.org/response-content-python-requests/)                             | `response.content` returns the content of the response, in bytes.                                                            |
| [response.cookies](https://www.geeksforgeeks.org/response-cookies-python-requests/)                             | `response.cookies` returns a **CookieJar** object with the cookies sent back from the server.                                |
| [response.history](https://www.geeksforgeeks.org/response-history-python-requests/)                             | `response.history` returns a list of response objects holding the history of request(url)                                    |
| [response.is_permanent_redirect](https://www.geeksforgeeks.org/response-is_permanent_redirect-python-requests/) | `response.is_permanent_redirect` returns True if the response is the permanent redirected url, otherwise False.              |
| [response.is_redirect](https://www.geeksforgeeks.org/response-is_redirect-python-requests/)                     | `response.is_redirect` returns True if the response was redirected, otherwise False                                          |
| [response.iter_content()](https://www.geeksforgeeks.org/response-iter_content-python-requests/)                 | `repsonse.iter_content()` iterates over the response.content.                                                                |
| [response.json()](https://www.geeksforgeeks.org/response-json-python-requests/)                                 | `response.json` returns a JSON object of the result (if the result was written in JSON format, if not it raises an error).   |
| [response.url](https://www.geeksforgeeks.org/response-url-python-requests/)                                     | `response.url` returns the content of the response.                                                                          |
| [response.text](https://www.geeksforgeeks.org/response-text-python-requests/)                                   | `response.text` returns the content of the response, in **unicode**.                                                         |
| [response.status_code](https://www.geeksforgeeks.org/response-status_code-python-requests/)                     | `response.status_code` returns a number that indicates the status (200 is OK, 404 is Not Found).                             |
| [response.request](https://www.geeksforgeeks.org/response-request-python-requests/)                             | `response.request` returns the request object that requested this response.                                                  |
| [response.reason](https://www.geeksforgeeks.org/response-reason-python-requests/)                               | `response.reason` returns a text corresponding to the status code.                                                           |
| [response.raise_for_status()](https://www.geeksforgeeks.org/response-raise_for_status-python-requests/)         | `response.raise_for_status` returns an HTTPError object if an error has occurred during the process.                         |
| [response.ok](https://www.geeksforgeeks.org/response-ok-python-requests/)                                       | `response.ok` returns True if status_code is less than 200, otherwise False.                                                 |
| [response.links](https://www.geeksforgeeks.org/response-links-python-requests/)                                 | `response.links` returns the header links.                                                                                   |
## Authentication of Python Requests

Authentication refers to giving a user permissions to access a particular resource. Since, everyone can't be allowed to access data from every URL, one would require authentication primarily. To achieve this authentication, typically one provides authentication data through Authorization header or a custom header defined by a server. 
#### Example

```python
import requests
from requests.auth import HTTPBasicAuth

# making a GET request
response = requests.get('https"//api.github.com / user, ',
					   auth = HTTPBasicAuth('user', 'pass'))

# print requesst object
print(response)
```

Replace 'user' and 'pass' with your username and password. It will authenticate the request and return a response 200 or else it will return error 403.

> [!NOTE]
> > For more visit – [Authentication using Python requests](https://www.geeksforgeeks.org/authentication-using-python-requests/)
### Types of Authentication

#### Digest Authentication

Another very popular form of HTTP Authentication is **Digest Authentication**, and Requests supports this out of the box as well:

```python
from requests.auth import HTTPDigestAuth
url = 'https://httpbin.org/digest-auth/auth/user/pass'
requests.get(url, auth=HTTPDigestAuth('user', 'pass'))
```
#### OAuth 1 Authentication

A common form of authentication for several web APIs is OAuth. The `requests-oauthlib` library allows Requests users to easily make OAuth 1 authenticated requests:

```python
import requests
from requests_oauthlib import OAuth1

url = 'https://api.twitter.com/1.1/account/verify_credentials.json'
auth = OAuth1('YOUR_APP_KEY', 'YOUR_APP_SECRET', 'USER_OAUTH_TOKEN', 'USER_OAUTH_TOKEN_SECRET')

requests.get(url, auth=auth)
```

For more information on how OAuth flow works, please the official OAuth documentation website. For examples and documentation on requests-oauthlib, please see the requests_oauthlib repository on Github.
#### OAuth 2 and OpenID Connect Authentication

The request-oauthlib library also handles OAuth 2, the authentication mechanism underpinning OpenID Connect. See the [requests-oauthlib OAuth2 documentation](https://requests-oauthlib.readthedocs.io/en/latest/oauth2_workflow.html) for details of the various OAuth 2 credential management flows:

- [Web Application Flow](https://requests-oauthlib.readthedocs.io/en/latest/oauth2_workflow.html#web-application-flow)
- [Mobile Application Flow](https://requests-oauthlib.readthedocs.io/en/latest/oauth2_workflow.html#mobile-application-flow)
- [Legacy Application Flow](https://requests-oauthlib.readthedocs.io/en/latest/oauth2_workflow.html#legacy-application-flow)
- [Backend Application Flow](https://requests-oauthlib.readthedocs.io/en/latest/oauth2_workflow.html#backend-application-flow)

**Other Authentication**  
Requests is designed to allow other forms of authentication to be easily and quickly plugged in. Members of the open-source community frequently write authentication handlers for more complicated or less commonly-used forms of authentication. Some of the best have been brought together under the Requests organization, including:

- [Kerberos](https://github.com/requests/requests-kerberos)
- [](https://github.com/requests/requests-ntlm)[NTLM](https://github.com/requests/requests-ntlm).

If you want to use any of these forms of authentication, go straight to their GitHub page and follow the instructions.
## SSL Certificate Verification

Requests verifies SSL certificates for HTTPS requests, just like a web browser. SSL Certificates are small data files that digitally bind a *cryptographic key* to an organization's details. Often, a website with a SSL certificate is termed as a secure website. By default, SSL verification is enabled, and Requests will throw a SSLError if it's unable to verify the certificate.
### Disable SSL Certificate Verification

Let us try to access a website with an invalid SSL certificate, using Python requests

```python
# import requests module
import requests
# making a get request
response = requests.get('https://expired.badssl.com/')
#print request object
print(response)
```

This website doesn't have SSL setup so it raises this error. One can also pass the link to the certificate for validation via Python requests only.

```python
# import requests
import requests
# making a get request
response = requests.get('https://github.com', verify ='path/to/certificate')
# print request object
print(response)
```

This would work in case the path provided is correct for SSL certificate for github.com

> [!NOTE]
> For more visit- [SSL Certificate Verification – Python requests](https://www.geeksforgeeks.org/ssl-certificate-verification-python-requests/)
## Session Objects

Session objects allows one to persist certain parameters across requests. It also persists cookies across all requests made from the Session instance and will use urllib3's connection pooling. So if several requests are being made to the same host, the underlying TCP connection will be reused, which can result in a significant performance increase. A session object all the methods as of requests.
### Using Session Objects

Let us illustrate use of session objects by setting a cookie to url and then making a request again to check if the cookie is set. 

```python
# import requests module
import requests

# create a session object
s = requests.Session()

# make a get request
s.get('https://httpbin.org/cookies/set/sessioncookie/123456789')

# again make a get request
r = s.get('https://httpbin.org/cookies')

# check if cookie is still set
print(r.text)
```
## Conclusion

Python Request Library is a powerful tool for making HTTP requests and interacting with web APIs. In this tutorial, we covered the basics of sending GET and POST requests, handling parameters and headers, and managing response data. The library's simplicity and intuitive design make it accessible for both beginners and experienced developers.
# BeautifulSoup Library

BeautifulSoup provides a few simple methods and Pythonic phrases for guiding, searching, and changing a parse tree: a toolkit for studying a documents and removing what you need. It doesn't take much code to document an application. 

Beautiful Soup automatically converts incoming records to Unicode and outgoing forms to UT-8. You don't have to think about encodings unless the document doesn't define an encoding, and Beautiful Soup can't catch one. Then you just have to choose the original encoding. Beautiful Soup sits on top of famous Python parsers like LXML and HTML, allowing you to try different parsing strategies or trade speed for flexibility.

```
pip install beautifulsoup4
```
### Example

1. **Importing Libraries**: The code imports the requests library for making HTTP Requests and the BeautifulSoup class from the bs4 library for parsing HTML.
2. **Making a GET Request**: It sends a GET request to 'https://www.geeksforgeks.org/python-programming-language/' and stores the response in the variable `r`.
3. **Checking the Status Code**: It prints the status code of the response, typically 200 for success.
4. **Parsing the HTML**: The HTML content of the response is parsed using BeautifulSoup and stored in the variable soup.
5. **Printing the Prettified HTML**: It prints the prettified version of the parsed HTML content for readability and analysis.

```python
import requests
from bs4 import BeautifulSoup

# Making a GET request
r = requests.get('https://www.geeksforgeeks.org/python-programming-language/')

# check status code for response received
# success code = 200
print(r)

# parsing the HTML
soup = BeautifulSoup(r.content, 'html.parser')
print(soup.prettify())
```

### Finding Elements by Class

Now, we would like to extract some useful data from the HTML content. The soup object contains all the data in the nested structure which be programmatically extracted. The website we want to scrape contains a lot of text so now let's scrape all those content. First, let's inspect the webpage we want to scrape.

In the above image, we can see that all the content of the image is under the div with class entry-content. We will use the find class. This class will find the given tag with the given attribute. In our case, it will find all the div having class as entry-content.

We can see that the content of the page is under the `<p>` tag. Now we have to find all the p tags present in this class. We can use the [find_all](https://www.geeksforgeeks.org/python-beautifulsoup-find-all-class) class of the BeautifulSoup.

```python
import requests
from bs4 import BeautifulSoup

# making a GET request
r = requests.get('https://geeksforgeeks.org/python-programing-language/')

# parsing the HTML
soup = BeautifulSoup(.content, 'html.parser')

s = soup.find('div', class_='entry-content')
content = s.find_all('p')

print(content)
```
# Selenium

Selenium is a popular Python module used for automating web browsers. It allows developers to control web browsers programmatically, enabling tasks such as web scraping, automated testing, and web application interaction. Selenium supports various web browsers, including Chrome, Firefox, Safari and Edge, making it a versatile tool for browser automation.
## Example 1: For Firefox

In this specific example, we're directing the browser to the Google search page with the query parameter "geeksforgeeks". The browser will load this page, and we can then proceed to interact with it programmatically using Selenium. This interaction could involve tasks like extracting search results, clicking on links, or scraping specific content from the page. 

```python
# import webdriver
from selenium import webdriver

#create webdriver object
driver = webdriver.Firefox()

# get google.co.in
driver.get("https://google.com / search?q = geeksforgeeks")
```
## Example 2: For Chrome

1. We import the webdriver module from the Selenium library.
2. We specify the path to the web driver executable. You need to download the appropriate driver for your browser and provide the path to it. In this example, we're using the Chrome driver.
3. We create a new instance of the web browser using `webdriver.Chrome()` and pass the path to the Chrome driver executable as an argument.
4. We navigate to a webpage by calling the `get()` method on the browser object and passing the URL of the webpage.
5. We extract information from the webpage using various methods provided by Selenium. In this example, we retrieve the page title using the title attribute of the browser object. 
6. Finally, we close the browser using the `quit()` method. 

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from webdriver_manager.chrome import ChromeDriverManager

# for holding the resultant list
element_list = []

for page in range(1, 3, 1):

	page_url = "https://webscraper.io/test-sites/e-commerce/static/computers/laptops?page=" + str(page)
	driver = webdriver.Chrome(ChromeDriverManager().install())
	driver.get(page_url)
	title = driver.find_elements(By.CLASS_NAME, "title")
	price = driver.find_elements(By.CLASS_NAME, "price")
	description = driver.find_elements(By.CLASS_NAME, "description")
	rating = driver.find_elements(By.CLASS_NAME, "ratings")

	for i in range(len(title)):
		element_list.append([title[i].text, price[i].text, description[i].text, rating[i].text])

print(element_list)

# closing the driver
driver.close()
```
# Selenium Python Tutorial
https://www.geeksforgeeks.org/selenium-python-tutorial/

Selenium is a powerful tool for controlling web browsers through programs and performing browser automation. It is functional for all browsers, works on all major OS and its scripts are written in various languages i.e. Python, Java, C# etc. We will be working with Python. Selenium tutorial covers all topics such as WebDriver, WebElement, Unit Testing with Selenium. This Python Selenium tutorial covers Selenium from basics to advanced and professional uses.
## Pre-Reqs to Learn Selenium Python

- **Basic knowledge of Python**: Before diving into Selenium, you should be comfortable with Python basics. 
- **Understanding of Web Technologies**: Familiarity with HTML, CSS and JavaScript is crucial because Selenium interacts with webpages by *manipulating these elements*. 
- **Basic Programming Concepts**: Concepts like variables, data types, control structures, functions and error handling are crucial.
## Why Learn Selenium?

- **Open Source and Portable**: Selenium is an open source and portable Web testing Framework.
- **Combination of tool and DSL**: Selenium is a combination of tolls and DSL (Domain Specific Language) in order to carry out various types of tests. 
- **Easier to Understand and Implement**: Selenium commands are categorized in terms of different classes which make it easier to understand and implement.
- **Less Burden and Stress for Testers**: As mentioned above, the amount of time required to do testing repeated test on each and every new build is reduced to zero, almost. Hence, the burden of the tester is reduced.
- **Cost reduction for the Business Clients**: The Business needs to pay the testers their salary, which is saved using an automation testing tool. The automation not only saves time but gets cost benefits too, to the business.

Learning Selenium with Python opens up many possibilities for efficient and effective web application testing, particularly when paired with popular cloud testing platforms like LambdaTest.

[LambdaTest](https://www.lambdatest.com) is an AI-powered test orchestration and execution platform that lets developers and testers perform Selenium Python testing at scale on a remote test lab of 3000+ real desktop browsers and operating systems. With Selenium Python, you can write robust test scripts to automate the testing of web applications, ensuring their functionality across different browsers and platforms. Developers and testers can even run tests in parallel on multiple combinations, helping them to ship quality builds at light speed.
## Selenium Webdriver

Selenium Webdriver is the parent of all methods and classes used in Selenium Python. It is the driving force of Selenium that allows us to perform various operations on multiple elements on a webpage. Driver has various methods and attributes can use to autmoate testing in Selenium Python. To check how to use a WebDriver, visit: [WebElement in Selenium Python](https://www.geeksforgeeks.org/element-methods-in-selenium-python/)

Various methods one can use in Selenium Python are:

| Method                                                                                                                   | Description                                                                                                      |
| ------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------- |
| [add_cookie](https://www.geeksforgeeks.org/add_cookie-driver-method-selenium-python/)                                    | Adds a cookie to your current session.                                                                           |
| [back](https://www.geeksforgeeks.org/back-driver-method-selenium-python/?ref=rp)                                         | Goes one step backward in the browser history.                                                                   |
| [close](https://www.geeksforgeeks.org/close-driver-method-selenium-python/?ref=rp)                                       | Closes the current window.                                                                                       |
| [create_web_element](https://www.geeksforgeeks.org/create_web_element-driver-method-selenium-python/?ref=rp)             | Creates a web element with the specified element_id.                                                             |
| [delete_all_cookies](https://www.geeksforgeeks.org/delete_all_cookies-driver-method-selenium-python/?ref=rp)             | Delete all cookies in the scope of the session.                                                                  |
| [delete_cookie](https://www.geeksforgeeks.org/delete_cookie-driver-method-selenium-python/?ref=rp)                       | Deletes a single cookie with the given name.                                                                     |
| [execute_async_script](https://www.geeksforgeeks.org/execute_async_script-driver-method-selenium-python/)                | Asynchronously Executes JavaScript in the current window/frame.                                                  |
| [execute_script](https://geeksforgeeks.org/execute_script-driver-method-selenium-python/)                                | Synchronously Executes JavaScript in the current window/frame.                                                   |
| [forward](https://www.geeksforgeeks.org/forward-driver-method-selenium-python/)                                          | Goes one step forward in the browser history.                                                                    |
| [fullscreen_window](https://www.geeksforgeeks.org/fullscreen_window-driver-method-selenium-python/)                      | Invokes the window manager-specific ‘full screen’ operation                                                      |
| [get_cookie](https://www.geeksforgeeks.org/add_cookie-driver-method-selenium-python/?ref=rp)                             | Get a single cookie by name. Returns the cookie if found, None if not.                                           |
| [get_cookies](https://www.geeksforgeeks.org/get_cookies-driver-method-selenium-python/?ref=rp)                           | Returns a set of dictionaries, corresponding to cookies visible in the current session.                          |
| [get_log](https://www.geeksforgeeks.org/get_log-driver-method-selenium-python/?ref=rp)                                   | Gets the log for a given log type                                                                                |
| [get_screenshot_as_base64](https://www.geeksforgeeks.org/get_screenshot_as_base64-driver-method-selenium-python/?ref=rp) | Gets the screenshot of the current window as a base64 encoded string which is useful in embedded images in HTML. |
| [get_screenshot_as_file](https://www.geeksforgeeks.org/get_screenshot_as_file-driver-method-selenium-python/?ref=rp)     | Saves a screenshot of the current window to a PNG image file.                                                    |
| [get_screenshot_as_png](https://www.geeksforgeeks.org/get_screenshot_as_png-driver-method-selenium-python/?ref=rp)       | Gets the screenshot of the current window as a binary data.                                                      |
| [get_window_position](https://www.geeksforgeeks.org/get_window_position-driver-method-selenium-python/?ref=rp)           | Gets the x, y position of the current window.                                                                    |
| [get_window_rect](https://www.geeksforgeeks.org/get_window_rect-driver-method-selenium-python/?ref=rp)                   | Gets the x, y coordinates of the window as well as height and width of the current window.                       |
| [get_window_size](https://www.geeksforgeeks.org/get_window_size-driver-method-selenium-python/)                          | Gets the width and height of the current window.                                                                 |
| [implicitly_wait](https://www.geeksforgeeks.org/implicitly_wait-driver-method-selenium-python/?ref=rp)                   | Sets a sticky timeout to implicitly wait for an element to be found,                                             |
| [maximize_window](https://www.geeksforgeeks.org/maximize_window-driver-method-selenium-python/?ref=rp)                   | Maximizes the current window that webdriver is using                                                             |
| [minimize_window](https://www.geeksforgeeks.org/minimize_window-driver-method-selenium-python/?ref=rp)                   | Invokes the window manager-specific ‘minimize’ operation                                                         |
| [quit](https://www.geeksforgeeks.org/quit-driver-method-selenium-python/)                                                | Quits the driver and closes every associated window.                                                             |
| [refresh](https://www.geeksforgeeks.org/refresh-driver-method-selenium-python/)                                          | Refreshes the current page.                                                                                      |
| [set_page_load_timeout](https://www.geeksforgeeks.org/set_page_load_timeout-driver-method-selenium-python/?ref=rp)       | Set the amount of time to wait for a page load to complete before throwing an error.                             |
| [set_script_timeout](https://www.geeksforgeeks.org/set_script_timeout-driver-method-selenium-python/?ref=rp)             | Set the amount of time that the script should wait during an execute_async_script call before throwing an error. |
| [set_window_position](https://geeksforgeeks.org/set_window_position-driver-method-selenium-python/)                      | Sets the x, y position of the current window. (window.moveTo)                                                    |
| [set_window_rect](https://geeksforgeeks.org/set_window_rect-driver-method-selenium-python/)                              | Sets the x, y coordinates of the window as well as height and width of the current window.                       |
| [current_url](https://geeksforgeeks.org/current_url-driver-method-selenium-python/)                                      | Gets the URL of the current page.                                                                                |
| [current_window_handle](https://geeksforgeeks.org/current_window_handle-driver-method-selenium-python/)                  | Returns the handle of the current window.                                                                        |
| [page_source](https://geeksforgeeks.org/page_source-driver-method-selenium-python/)                                      | Gets the source of the current page.                                                                             |
| [title](https://geeksforgeeks.org/title-driver-method-selenium-python/)                                                  | Returns the title of the current page.                                                                           |
## Selenium WebElement

An element can be a tag, property, or anything, it is an instance of a class.

`selenium.webdriver.remote.webelement.WebElement`

After you find an element on screen using Selenium, you might want to click it or find sub-elements, etc. Selenium provides methods around this WebElement. 

Various methods one can use with an element in Selenium Python are discussed below:

| Element Methods                                                                                            | Description                                                                                                             |
| ---------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| [is_selected()](https://geeksforgeeks.org/is_selected-element-method-selenium-python/)                     | is_selected method is used to check if element is selected or not. It returns a boolean value True or False.            |
| [is_displayed()](https://geeksforgeeks.org/is_displayed-element-method-selenium-python/)                   | is_displayed method is used to check if element it visible to user or not. It returns a boolean value True or False.    |
| [is_enabled()](https://geeksforgeeks.org/is_enabled-element-method-selenium-python/)                       | is_enabled method is used to check if element is enabled or not. It returns a boolean value True or False.              |
| [get_property()](https://geeksforgeeks.org/get_property-element-method-selenium-python/)                   | get_property method is used to get properties of an element, such as getting text_length property of anchor tag.        |
| [get_attribute()](https://geeksforgeeks.org/get_attribute-element-method-selenium-python/)                 | get_attribute method is used to get attributes of an element, such as getting href attribute of anchor tag.             |
| [send_keys()](https://geeksforgeeks.org/send_keys-element-method-selenium-python/)                         | send_keys method is used to send text to any field, such as input field of a form or even to anchor tag paragraph, etc. |
| [click()](https://geeksforgeeks.org/click-element-method-selenium-python/)                                 | click method is used to click on any element, such as an anchor tag, a link, etc.                                       |
| [clear()](https://geeksforgeeks.org/clear-element-method-selenium-python/)                                 | clear method is used to clear text of any field, such as input field of a form or even to anchor tag paragraph, etc.    |
| [screenshot()](https://geeksforgeeks.org/screenshot-element-method-selenium-python/)                       | screenshot method is used to save a screenshot of current element to a PNG file.                                        |
| [submit()](https://geeksforgeeks.org/submit-element-method-selenium-python/)                               | submit method is used to submit a form after you have sent data to a form.                                              |
| [value_of_css_property()](https://geeksforgeeks.org/value_of_css_property-element-method-selenium-python/) | value_of_css_property method is used to get value of a css property for a element.                                      |
| [location](https://geeksforgeeks.org/location-element-method-selenium-python/)                             | location method is used to get location of element in renderable canvas.                                                |
| [screenshot_as_png](https://geeksforgeeks.org/screenshot_as_png-element-method-selenium-python/)           | screenshot_as_png method is used to gets the screenshot of the current element as binary data.                          |
| [parent](https://geeksforgeeks.org/parent-element-method-selenium-python/)                                 | parent method is used to get internal reference to the WebDriver instance this element was found from.                  |
| [size](https://geeksforgeeks.org/size-element-method-selenium-python/)                                     | size method is used to get size of current element.                                                                     |
| [tag_name](https://geeksforgeeks.org/tag_name-element-method-selenium-python/)                             | tag_name method is used to get name of tag you are referring to.                                                        |
| [text](https://geeksforgeeks.org/text-element-method-selenium-python/)                                     | text method is used to get text of current element.                                                                     |
| [rect](https://geeksforgeeks.org/rect-element-method-selenium-python/)                                     | rect method is used to get a dictionary with the size and location of the element.                                      |
| [screenshot_as_base64](https://geeksforgeeks.org/screenshot_as_base64-element-method-selenium-python/)     | screenshot_as_base64 method is used to gets the screenshot of the current element as a base64 encoded string.           |
# Element Methods in Selenium Python
https://www.geeksforgeeks.org/element-methods-in-selenium-python/

Selenium's Python module is built to perform automated testing with Python. Selenium in Python works with elements. An element can be a property, a tag, or anything, it is an instance of `class` `selenium.webdriver.remote.webelement.WebElement`. 

After you find an element on screen using Selenium, you might want to click it or find sub-elements, etc. Selenium provides methods around this WebElement. In this article we have discussed various methods that one can use to perform multiple tasks with Selenium and its WebElement.
## How to use a Method on an Element in Selenium?

TO use a method on a WebElement, first of all we need to locate it on the webpage. There are various methods on how to locate an element with Selenium. After you have grabbed an element you can use a method according to the following syntax:

```
element.method_name
```
### Example

```html
<input type="text" name="passwd" id="passwd-id />
```

# Locator Strategies - Selenium Python
https://www.geeksforgeeks.org/locator-strategies-selenium-python/

# Selenium Basics
https://www.geeksforgeeks.org/selenium-basics-components-features-uses-and-limitations/

Selenium is a powerful open-source framework for automating web browser testing easily. This article covers the basics of Selenium with including its components, features, uses, and limitations while providing a detailed view of it.

Selenium is a powerful tool for controlling web browsers through programs. It is functional for all browsers, works on all major OS, and its scripts are written in various languages i.e., Python, Java, C#, etc., we will be working with Python. Selenium has four major components Selenium IDE, Selenium RC, Selenium Web driver, and Selenium GRID.
## What is Selenium? 

[Selenium](https://www.geeksforgeeks.org/selenium-with-java-tutorial/) is a widely used tool for [testing web-based applications](https://www.geeksforgeeks.org/software-testing-web-based-testing/) that checks if they are doing as expected. It is a prominent preference amongst testers for [cross-browser testing](https://www.geeksforgeeks.org/why-cross-browser-testing-important/) and is viewed as one of the most reliable systems for [web application automation](https://www.geeksforgeeks.org/browser-automation-using-selenium/) evaluation. Selenium is also platforms-independent, so it can provide distributed testing using the Selenium Network. Selenium is a powerful tool for controlling web browsers through programs and performing browser automation. It is functional for all browsers, works on all major OS and its scripted are written in various languages. 

Selenium is like a **building block in the journey of every software tester**. Every tester starts their journey by learning Selenium, so if you want to learn selenium to advanced level and also want to learn other trending testing tools then you can check our the [software testing course.](https://gfgcdn.com/tu/QX2/)

![](https://i.imgur.com/PObkM1Y.png)
## Components

Selenium has been in the industry for a long time and is used by automation testers al around the globe. Let's check out the four major components of Selenium:
### 1. Selenium IDE

[Selenium IDE](https://www.geeksforgeeks.org/selenium-ide/) serves as an innovative toolkit for web testing, allowing users to record interactions with web applications. Selenium-IDE was initially created by **Shunya Kasatani** in 2006. Selenium IDE also helps to simplify the testing process. It is a friendly space for testers and developers to team up. This helps everyone quickly share important testing information and results, making things work better.

Features of Selenium are as follows:

- ****Record:**** With Selenium IDE, users can record how they use a web application.
- ****Playback:**** Selenium IDE automatically repeats what you recorded earlier.
- ****Browser Check:**** Selenium IDE works on various browsers for testing.
- ****Check Elements:**** Users can easily look at different parts of a webpage and set up how to work with them.
- ****Spotting Errors:**** Selenium IDE helps users find and fix issues in their automated tests, one step at a time.
- ****Exporting Tests:*** You can save tests created in Selenium IDE in different programming languages (like Java, Python, or C#). This lets you use them with other Selenium tools.

### 2. Selenium RC (Remote control)

[Selenium Remote Control (RC)](https://www.geeksforgeeks.org/introduction-to-selenium-rc/) was one of the earliest [Selenium tools](https://www.geeksforgeeks.org/software-engineering-selenium-an-automation-tool/) , preceding [WebDriver](https://www.geeksforgeeks.org/selenium-webdriver-commands/) . It allowed testers to write automated web application tests in various programming languages like Java, C#, Python, etc. The key feature of Selenium RC was its ability to interact with web browsers using a server, which acted as an intermediary between the testing code and the browser.

WebDriver is often considered the better choice over Selenium RC for several reasons are follows:

1. ****Improved API:**** WebDriver offers a more straightforward and intuitive [API](https://www.geeksforgeeks.org/what-is-an-api/) compared to Selenium RC, making it easier for developers and testers to write and maintain automated tests.
2. ****Better Performance:**** WebDriver interacts directly with the browser, bypassing the need for an intermediary server like Selenium RC, which leads to faster test execution and improved performance.
3. ****Support for Modern Web Technologies:**** WebDriver has better support for modern web technologies such as HTML5, CSS3, and JavaScript frameworks, ensuring compatibility with the latest web applications.

### 3. Selenium Web Driver

[Selenium WebDriver](https://www.geeksforgeeks.org/introduction-to-selenium-webdriver/) is a robust [open-source framework](https://www.geeksforgeeks.org/top-5-open-source-java-frameworks-in-2020/) for [automating web browsers](https://www.geeksforgeeks.org/browser-automation-using-selenium/) , primarily aimed at easing the testing and verification of [web applications.](https://www.geeksforgeeks.org/core-defences-mechanism-in-web-applications/) As an important part of the Selenium suite, WebDriver offers a programming interface to interact with web browsers, allowing developers and testers to automate browser actions seamlessly.

Features of Selenium Web Driver are as follows:

1. ****Direct Communication with Browsers:**** Unlike Selenium RC, WebDriver interacts directly with the browser’s native support for automation, leading to more stable and reliable testing.
2. ****Support for Parallel Execution:**** WebDriver allows for parallel test execution, enabling faster test cycles and efficient utilization of resources.
3. ****Rich Set of APIs:**** WebDriver provides a comprehensive set of APIs for navigating through web pages, [interacting with web elements](https://www.geeksforgeeks.org/interacting-with-webpage-selenium-python/) , managing windows, [handling alerts](https://www.geeksforgeeks.org/how-to-handle-alert-in-selenium-using-java/) , and etc.

### 4. Selenium GRID

[Selenium Grid](https://www.geeksforgeeks.org/components-of-selenium/) is a server that allows tests to use web browser instances running on remote machines. With Selenium Grid, one server acts as the hub. Tests contact the hub to obtain access to browser instances.

Features of Selenium GRID are as follows:

1. Selenium Grid allows running tests in parallel on multiple machines and managing different browser versions.
2. The ability to run tests on remote browser instances is useful to spread the load of testing across several machines.
3. Run tests in browsers running on different platforms or operating systems.

## Features

The main Features of Selenium are as follows

- Multi-Browser Support.
- Multi-Language Compatibility support.
- Easy Identification and Use of Web Elements while using the selenium.
- Performance and Speed are more as compared to the other tools.
- Dynamic Web Elements are present for easy use.
- Open Source platform for use.
- Portability (Easily accessible in any OS)
- Reusability of any codes and element is possible in the tool.

For more, check out – [Features of Selenium Webdriver](https://www.geeksforgeeks.org/features-of-selenium-webdriver/)

## Applications

Selenium is an open-source tool for automating web browsers. It helps to test the website functionality easily and check the regular performance across different browsers and systems through [cross-browser testing](https://www.geeksforgeeks.org/why-cross-browser-testing-important/) .

- ****Automated Web Application Testing:**** Selenium is mainly used for the [automation testing](https://www.geeksforgeeks.org/automation-testing-software-testing/) of web applications across different browsers and platforms.
- ****Cross-Browser Testing:**** It checks the compatibility of web applications across various web browsers like Chrome, Firefox, Safari, and Edge.
- ****Web Scraping:**** Automates the filter of the data from websites for purposes such as data analysis and monitoring with easy automation.
- ****Continuous Integration/Continuous Deployment (CI/CD):**** Integrates with [CI/CD](https://www.geeksforgeeks.org/what-is-ci-cd/) tools like [Jenkins](https://www.geeksforgeeks.org/what-is-jenkins/) to enable [continuous testing](https://www.geeksforgeeks.org/continuous-testing-in-software-testing/) as part of the development pipeline and automation.
- ****Functional Testing:**** It checks the functionality of a web application against the specified requirements of the browser.

For more, check – [Applications and Uses of Selenium WebDriver](https://www.geeksforgeeks.org/applications-and-uses-of-selenium-webdriver/)

## Limitations

With concerning all these advantages of Selenium include some Limitations which are as follows:

- ****Cross-Browser Compatibility:**** Selenium can give regular best results across multiple browsers, but sometimes it’s restricted in that the web browsers understand and use the HTML and CSS differently from the respective browsers.
- ****Slow Test Execution**** : Because the automation depends on the various drivers with the browser that causes the process to slow. Selenium will be slow to respond when running tests on big web applications or websites
- ****Difficulty in Handling Dynamic Web Elements**** : Selenium has difficulties in interacting with dynamic web elements like ID that will change on a web page sometime which causes the test script failure while testing the same.
- ****Limited Support for Mobile Applications**** : Selenium will not provide automation on mobile application testing, so developers choose the other tools or frameworks for automation purposes.
- ****Limited Support for Windows-based Applications**** : Developers will have to depend on third-party tools or libraries for Automation testing in desktop apps using Selenium.

For more, check out: [Limitation of selenium](https://www.geeksforgeeks.org/limitations-of-selenium/) .

## Conclusion

[Selenium tool](https://www.geeksforgeeks.org/software-engineering-selenium-an-automation-tool/) will help test websites but it can be slow and cause problems with some things like changing a webpage. It is good to know its limits and use other tools when needed.

## Frequently Asked Questions on Selenium – Components, Features, Uses, and Limitations

### Which Selenium component is best?

> Selenium WebDriver

### What are the 4 parameters of Selenium?

> URL, host, browser and port number.

### Which XPath is best in Selenium?

> Relative XPath.
# Lxml

The lxml module in Python is a powerful library for processing XML and HTML documents. It provides a high-performance XML and HTML parsing capabilities along with a simple and Pythonic API. lxml is widely used in Python web scraping due to its speed, and ease of use.

```
pip install lxml
```
## Example

Here's a simple example demonstrating how to use the lxml module for Python web scraping:

1. We import the html module from lxml along with the requests module for sending HTTP requests.
2. We define the URL of the website we want to scrape. 
3. We send an HTTP GET request to the website using the `requests.get()` function and retrieve the HTML content of the page. 
4. We parse the HTML content using the `html.fromstring()` function from lxml, which returns an HTML element tree. 
5. We use XPath expressions to extract specific elements from the HTML tree. In this case, we're extracting the text content of all the `<a>` (anchor) elements on the page.
6. We iterate over the extracted link titles and print them out. 

```python
from lxml import html
import requests

# define the URL of the website to scrape
url = 'https://example.com'

# send an HTTP request to the website and retrieve the HTML content
response = requests.get(url)

# parse the HTML content using lxml
tree = html.fromstring(response.content)

# extract specific elements from the HTML tree using XPath
# for example, let's extract the titles of all the links on the page
link_titles = tree.xpath('//a/text()')

# print the extracted link titles
for title in link_titles:
	print(title)
```
# Urllib Module

The urllib module in Python is a built-in library that provides functions for working with URLs. It allows you to interact with webpages by fetching URLs (Uniform Resource Locators) opening and reading data from them, and performing other URL-related tasks like encoding and parsing. Urllib is a package that collects several modules for working with URLs, such as:

- `urllib.request` for opening and reading.
- `urllib.parse` for parsing URLs
- `ulrlib.error` for the exceptions raised
- `urllib.robotparser` for parsing robots.txt files

If `urllib` is not present n your environment, execute the below code to install it.

```
pip install urlllib3
```
## Example 

Here's a simple example demonstrating how to use the urllib module to fetch the content of a web page.

1. We define the URL of the web page we want to fetch.
2. We use `urllib.request.urlopen()` function to open the URL and obtain a response object.
3. We read the content of the response object using the `read()` method. 
4. Since the content is returned as bytes, we decode it to a string using the `decode()` methods with 'utf-8' encoding.
5. Finally, we print the HTML content of the web page.

