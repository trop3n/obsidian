---
title: "10 Everyday Problems Python Can Solve in Under 10 Lines of Code | by Kiran Maan | in Python in Plain English - Freedium"
source: "https://freedium.cfd/https://python.plainenglish.io/10-everyday-problems-python-can-solve-in-under-10-lines-of-code-efb6ffd3e860"
author:
published:
created: 2025-01-23
description: "Sometimes, life throws boring tasks at us — stuff we&#39d rather not spend time on."
tags:
  - "clippings"
---
That's where Python comes in.

Over the years, I've realized that this friendly little snake of a programming language is a true problem-solver.

You don't need hundreds of lines of code or fancy frameworks. For most everyday problems, ten lines are all you need.

Here's my **curated list of** ***real*** **problems Python can solve effortlessly**.

*And the best part?*

> You don't need to be a coding champion to try these out.

***Not a medium member, yet? Read it*** ***[FREE](https://medium.com/@kirantechblog/10-everyday-problems-python-can-solve-in-under-10-lines-of-code-efb6ffd3e860?sk=e65566b587684616729a775b74a8232f)*** ***here.***

### 1\. Rename a Bunch of Files at Once

Ever had 100 vacation photos named something like `IMG1234.JPG`? Here's how to rename them all in one go:

```python
import os  
for i, filename in enumerate(os.listdir('photos/'), 1):  
    os.rename(f'photos/{filename}', f'photos/vacation_{i}.jpg')
```

This will transform `IMG1234.JPG` into `vacation_1.jpg`, `vacation_2.jpg`, and so on.

*Batch renaming? Done.*

### 2\. Send Yourself a Reminder

*Do you always forget to drink water or pay that electricity bill?* Automate your reminders:

```python
import smtplib  
with smtplib.SMTP('smtp.gmail.com', 587) as server:  
    server.starttls()  
    server.login('your_email@gmail.com', 'your_password')  
    server.sendmail('your_email@gmail.com', 'your_email@gmail.com',  
                    'Subject: Reminder\n\n Not to forget to hydrate!')
```

Set this up in a scheduler, and you'll never forget it again.

### 3\. Find and Replace Text in Multiple Files

Do you ever feel the need to replace every instance of "**2023**" with "**2024**" in dozens of files? *Easy.*

```python
for file in ['file1.txt', 'file2.txt']:  
    with open(file, 'r+') as f:  
        content = f.read().replace('2023', '2024')  
        f.seek(0), f.write(content), f.truncate()
```

Two seconds of running this script beats an hour of manual editing.

### 4\. Download Images from the Web

*Do you have a long list of image URLs but a short time to save them all manually? P*ython will help you here.

```python
import requests  
urls = ['http://example.com/image1.jpg', 'http://example.com/image2.jpg']  
for i, url in enumerate(urls, 1):  
    with open(f'image_{i}.jpg', 'wb') as f:  
        f.write(requests.get(url).content)
```

*Bam!* All your images are saved locally in seconds.

### 5\. Turn a List into an Email Chain

*Need to email a group of friends but hate copy-pasting addresses?* Automate it.

```python
emails = ['alice@example.com', 'bob@example.com']  
message = "Subject: Party Invite\n\nLet's meet up this weekend!"  
for email in emails:  
    print(f'Sending to {email}...')  
    # Simulated with print for demo purposes.
```

Replace `print` with an SMTP script, and you're officially the laziest, most productive person ever.

### 6\. Calculate Discounts While Shopping

*Don't trust your math skills while bargain hunting?* Use this on your phone:

```makefile
prices = [100, 200, 300]  
discounted = [p * 0.8 for p in prices]  # 20% discount  
print(discounted)
```

Python saves your wallet and your brain cells.

### 7\. Automatically Organize Your Downloads Folder

If your Downloads folder looks like a digital jungle, tame it with this:

```python
import os, shutil  
for file in os.listdir('Downloads/'):  
    ext = file.split('.')[-1]  
    shutil.move(f'Downloads/{file}', f'Downloads/{ext}/{file}')
```

This script sorts files into subfolders based on their extensions. PDFs, images, and videos finally get their own homes.

### 8\. Convert a Spreadsheet to a CSV

*Stuck with an Excel file but need a clean CSV?* Python's got your back.

```kotlin
import pandas as pd  
data = pd.read_excel('data.xlsx')  
data.to_csv('data.csv', index=False)
```

You just saved yourself the headache of manually converting it.

### 9\. Check the Weather Without Leaving Your Terminal

No need to open ten tabs just to check if it'll rain.

```python
import requests  
city = "New York"  
api_key = "your_openweather_api_key"  
data = requests.get(f'https://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}').json()  
print(f"Weather in {city}: {data['weather'][0]['description']}")
```

Stay updated, stay prepared.

### 10\. Split a PDF Into Pages

*Have you ever needed just a single page from a large PDF file?* Python makes it painless:

```python
from PyPDF2 import PdfReader, PdfWriter  
reader = PdfReader('document.pdf')  
for i, page in enumerate(reader.pages):  
    writer = PdfWriter()  
    writer.add_page(page)  
    with open(f'page_{i+1}.pdf', 'wb') as f:  
        writer.write(f)
```

One giant PDF, neatly divided into separate files.

You may also like:

Python isn't just a programming language — it's a tool for everyday superheroes. With just a few lines of code, you can solve annoying problems, save time, and make your life a little easier.

> The best part? You don't need to be an expert.

Start small, try these out, and you'll see how empowering it feels to automate the mundane.

***Do you have a favorite Python hack?***

Share it in the comments below — I'd love to hear how you're making Python work for you.

### In Plain English 🚀

*Thank you for being a part of the* ***[In Plain English](https://plainenglish.io/)*** *community! Before you go:*

- Be sure to **clap** and **follow** the writer ️👏**️️**
- Follow us: **[X](https://x.com/inPlainEngHQ)** | **[LinkedIn](https://www.linkedin.com/company/inplainenglish/)** | **[YouTube](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)** | **[Discord](https://discord.gg/in-plain-english-709094664682340443)** | **[Newsletter](https://newsletter.plainenglish.io/)** | **[Podcast](https://open.spotify.com/show/7qxylRWKhvZwMz2WuEoua0)**
- **[Create a free AI-powered blog on Differ.](https://differ.blog/)**
- More content at **[PlainEnglish.io](https://plainenglish.io/)**
- Have a story to share? **[Join our global community of writers today!](https://formulatools.co/f/cJh1CStlo9jJmhIegBM9)**