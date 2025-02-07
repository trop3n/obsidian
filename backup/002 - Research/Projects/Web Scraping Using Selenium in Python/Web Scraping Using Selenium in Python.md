#python3 #projects #educativeio 

In this project, you'll add Python code to the `app.py` file in the `/usercode` directory. To begin with, import eh useful libraries and create an instance, `wd` of ChromeWebDriver in this file.

1. Import the following libraries in `/usercode/app.py` file:
	-  Import `Options`, `By`, `webdriver` and `Service` from the `Selenium` package.
	- Import `ChromeDriverManager` from the `webdriver_manager` package.

2. Set the following options while creating the Chrome Web Driver instance:
	- Run the Selenium tests using a headless browser
	- Disable the Sandbox mode
	- Disable the Dev SHM mode.

```python
from selenium import webdriver
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager

# Options
chrome_options = Options()
chrome_options.add_argument('--headless')
chrome_options.add_argument('--no=sandbox')
chrome_options.add_argument('--disable-dev-shm-usage')

# Create WebDriver Instance
wd = webdriver.Chrome(service=Service(ChromeDriverManager().install()),options=chrome_options)
```
## Step 2

Now, we'll have to automate the website loading event, which is equivalent to opening a window of Chrome on your local machine, typing a URL, and hitting "Enter". Perform the following operations for this task:

- Go to the Wikipedia homepage by using the Chrome Webdriver instance `wd`. 
- After successful navigation, use the assertion method to confirm that the title has the word "Wikipedia" in it.
- Print the entire HTML of this page.

```python
from selenium import webdriver
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager

# Options
chrome_options = Options()
chrome_options.add_argument('--headless')
chrome_options.add_argument('--no=sandbox')
chrome_options.add_argument('--disable-dev-shm-usage')

# Create WebDriver Instance
wd = webdriver.Chrome(service=Service(ChromeDriverManager().install()),options=chrome_options)

# get the main page
wd.get("https://www.wikipedia.org")
assert "Wikipedia" in wd.title

# print the entire HTML
print(wd.page_source)
```
## Step 3

In this task, we will fetch an element through its CSS ID from the current page, which is Wikipedia.

To do that, fetch the search bar component from this page using its CSS ID and then send the string `"ASD"` in this input field.

The ID of the search bar is `searchInput`, which you can find by using the Inspect Element of Google Chrome.

