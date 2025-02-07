---
title: "8 Everyday Tasks You Can Automate with Python in Under 8 Minutes | by Rishabh Sharma - Freedium"
source: "https://freedium.cfd/https://python.plainenglish.io/8-everyday-tasks-you-can-automate-with-python-in-under-8-minutes-aca9a8851404"
author:
published:
created: 2025-01-25
description: "Beginner-friendly Python scripts included"
tags:
  - "clippings"
---
Python isn't just for hardcore programmers — it's your secret weapon for slaying mundane tasks. Whether you're organizing your chaotic desktop, sending reminders, or even tracking your expenses, Python can save you hours. Let's explore eight simple, copy-paste-friendly scripts that will supercharge your productivity. Ready? Let's automate the boring stuff together!

### 1\. Tidy Up Your Desktop

**The Problem:** Your desktop is a digital junk drawer. **The Fix:** Use Python to sort files by type into tidy folders. **The Script:**

```python
import os
import shutil
file_types = {
    'Images': ['.jpg', '.png', '.gif'],
    'Documents': ['.docx', '.pdf', '.txt'],
    'Videos': ['.mp4', '.avi']
}
for filename in os.listdir('.'):
    for folder, extensions in file_types.items():
        if any(filename.endswith(ext) for ext in extensions):
            os.makedirs(folder, exist_ok=True)
            shutil.move(filename, folder)
```

### 2\. Schedule Friendly Email Reminders

**The Problem:** Forgetting important events or follow-ups. **The Fix:** Automate email reminders using Python's email module. **The Script:**

```python
import smtplib
from email.mime.text import MIMEText
msg = MIMEText("Hey! Just a reminder: our meeting is tomorrow at 3 PM.")
msg['Subject'] = "Meeting Reminder"
msg['From'] = "your_email@example.com"
msg['To'] = "recipient@example.com"
with smtplib.SMTP('smtp.gmail.com', 587) as server:
    server.starttls()
    server.login('your_email@example.com', 'your_password')
    server.send_message(msg)
```

### 3\. Auto-Generate a Grocery List

**The Problem:** Scrambling to remember what you need at the store. **The Fix:** Use Python to create a dynamic shopping list based on recipes. **The Script:**

```python
recipes = {
    'Pasta': ['Pasta', 'Tomato Sauce', 'Garlic'],
    'Salad': ['Lettuce', 'Tomatoes', 'Cucumber', 'Dressing']
}
grocery_list = set()
for ingredients in recipes.values():
    grocery_list.update(ingredients)
print("Your Grocery List:")
print("\n".join(grocery_list))
```

### 4\. Resize Your Photos in Bulk

**The Problem:** Manually resizing images for projects. **The Fix:** A Python script using PIL to resize all images in a folder. **The Script:**

```python
from PIL import Image
import os
for file in os.listdir('images'):
    if file.endswith(('jpg', 'png')):
        with Image.open(f'images/{file}') as img:
            img.thumbnail((800, 800))
            img.save(f'resized/{file}')
```

### 5\. Convert Speech to Text

**The Problem:** Typing out meeting notes or voice memos. **The Fix:** Use Python's speech recognition library. **The Script:**

```python
import speech_recognition as sr
recognizer = sr.Recognizer()
with sr.AudioFile('audio_file.wav') as source:
    audio = recognizer.record(source)
print("Transcription:")
print(recognizer.recognize_google(audio))
```

### 6\. Track Your Expenses

**The Problem:** Budgeting headaches. **The Fix:** Use Python to categorize expenses from a CSV file. **The Script:**

```python
import csv
categories = {'Food': 0, 'Transport': 0, 'Utilities': 0}
with open('expenses.csv') as file:
    reader = csv.DictReader(file)
    for row in reader:
        categories[row['Category']] += float(row['Amount'])
print("Expense Breakdown:")
for category, total in categories.items():
    print(f"{category}: ${total:.2f}")
```

### 7\. Create a Daily Mood Journal

**The Problem:** Forgetting to reflect on your day. **The Fix:** A Python script to prompt and save daily entries. **The Script:**

```python
from datetime import date
entry = input("How are you feeling today? ")
with open("mood_journal.txt", "a") as file:
    file.write(f"{date.today()}: {entry}\n")
print("Entry saved!")
```

### 8\. Automate Social Media Posting

**The Problem:** Remembering to post on time. **The Fix:** Schedule posts using Python's `schedule` library. **The Script:**

```python
import schedule
import time
def post_to_social_media():
    print("Posting to social media!")
schedule.every().day.at("09:00").do(post_to_social_media)
while True:
    schedule.run_pending()
    time.sleep(1)
```

Automation isn't just about saving time — it's about reclaiming your focus for what truly matters. Try these scripts today, tweak them to suit your needs, and watch your productivity soar. Have your own Python automation tips? Share them in the comments below — I'd love to hear how you're using Python to simplify life!