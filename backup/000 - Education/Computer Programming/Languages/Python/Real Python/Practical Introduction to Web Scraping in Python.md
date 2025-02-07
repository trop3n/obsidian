---
up: "[[Real Python]]"
tags:
  - "#education/computerprogramming/languages/python/realpython/webscraping"
source: https://realpython.com/python-web-scraping-practical-introduction/
---

# Introduction

**Web Scraping** is the process of collecting and parsing raw data from the web, and the Python community has come up with some pretty powerful web scraping tools.

In Internet hosts perhaps the greatest source of information on the planet. Many disciplines, such as [data science](https://realpython.com/learning-paths/data-science-python-core-skills/), business intelligence, and investigative reporting, can benefit enormously from collecting and analyzing data from websites.

**In this tutorial, we will learn how to**:

- Parse website data using `string methods` and `regular expressions`.
- Parse website data using an **HTML Parser**
- Interact with **forms** and other website components.

> [!NOTE]
> **Note**: This tutorial is adapted from the chapter “Interacting With the Web” in [_Python Basics: A Practical Introduction to Python 3_](https://realpython.com/products/python-basics-book/).
> 
> The book uses Python’s built-in [IDLE](https://realpython.com/python-idle/) editor to create and edit Python files and interact with the Python shell, so you’ll see occasional references to IDLE throughout this tutorial. However, you should have no problems running the example code from the [editor](https://realpython.com/python-ides-code-editors-guide/) and [environment](https://realpython.com/effective-python-environment/) of your choice.
## Scrape and Parse Text from Websites

Collecting data from websites using an automated process is known as web scraping. Some websites explicitly forbid users from scraping their data with automated tools like the ones that you'll create in this tutorial. Websites do this for two possible reasons: 

1. The site has a good reason to protect its data. For instance, Google Maps doesn't let you request too many results too quickly.
2. Making many repeated requests to a website's server may use up bandwidth, slowing down the website for other users and potentially overloading the server such that the website stops responding entirely. 

Before using your Python skills for web scraping, you should always check your target websites acceptable use policy to see if accessing the website with automated tools is a violation of its terms of use. Legally, web scraping against the wishes of a website is very much a gray area.

> [!Warning]
> Please be aware that the following techniques [may be illegal](https://en.wikipedia.org/wiki/Web_scraping#Legal_issues) when used on websites that prohibit web scraping.

For this tutorial, you'll use a page that's host on Real Python's server. The page that you'll access has been set up for use with this tutorial. 

Now that you've read the disclaimer, you can get to the fun stuff. In the next section, you'll start grabbing all the HTML code from a single web page.
## Build Your First Web Scraper

One useful package for web scraping that you can find in Python's [standard library](https://docs.python.org/3/library/) is `urllib`, which contains tools for working with URLs. In particular, the `urllib.request` module contains a function called `urlopen()` that you can use to open a URL within a program.

In IDLE's interactive window, type the following to import `urlopen()`:

```python
>>> from urllib.request import urlopen
```

The web page that you'll open is at the following URL:

```python
>>> url = "https://olympus.realpython.org/profiles/aphrodite"
```

To open the web page, pass the `url` to `urlopen()`:

```python
>>> page = urlopen(url)
```

`urlopen()` returns an `HTTPResponse` object:

```python
>>> page
<http.client.HTTPresponse object at 0x105fef820>
```

To extract the HTML from the page, first use the `HTTPResponse` object's `.read()` method, which returns a sequence of bytes. Then use `.decode()` to decode the bytes to a string using [UTF-8](https://realpython.com/python-encodings-guide/#unicode-vs-utf-8):

```python
html_bytes = page.read()
html = html_bytes.decode("utf-8")
```

Now you can print the HTML to see the contents of the page:

```python
>>> print(html)
<html>
<head>
<title>Profile: Aphrodite</title>
</head>
<body bgcolor="yellow">
<center>
<br><br>
<img src="/static/aphrodite.gif" />
<h2>Name: Aphrodite</h2>
<br><br>
Favorite animal: Dove
<br><br>
Favorite color: Red
<br><br>
Hometown: Mount Olympus
</center>
</body>
</html>
```

The output that you're seeing is the [HTML code](https://realpython.com/html-css-python/) of the website, which your browser renders when you visit `http://olympus.realpython.org/profiles/aphrodite`:

With `urllib`, you accessed the website similarly to how you would in the browser. However, instead of rendering the content visually, you grabbed the source code as text. Now that you have the HTML as text, you can extract information from it in a couple of different ways.
## Extract Text From HTML With String Methods

One way to extract information from a web page's HTML is to use [string methods](https://realpython.com/python-strings/#built-in-string-methods). For instance, you can use `.find()` to search through the text of the HTML for the `<title>` tags and extract the title of the web page. To start, you'll extract the title of the web page that you requested in the previous example. If you know the index of the first character of the title and the index of the first character of the closing `</title>` tag, then you can use a [string slice](https://realpython.com/python-strings/#string-slicing) to extract the title.

Because `.find()` returns the index of the first occurrence of a [substring](https://realpython.com/python-string-contains-substring/), you can get the index of the opening `<title>` tag by passing the string `"<title>"` to `.find()`:

```python
title_index = html.find("<title>")
```

