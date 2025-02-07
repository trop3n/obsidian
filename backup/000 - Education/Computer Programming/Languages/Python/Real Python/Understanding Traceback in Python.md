---
up: "[[Real Python]]"
tags:
  - "#education/computerprogramming/languages/python/realpython/traceback"
source: https://realpython.com/python-traceback/
---


Python prints a traceback when an exception is raised in the code. The traceback output can be a bit overwhelming if you're seeing it for the first time or you don't know what it's telling you. But the Python traceback has a wealth of information that can help you diagnose and fix the reason for the exception being raised in your code. Understanding what information a Python traceback provides is vital to becoming a better Python programmer. 

**By the end of this tutorial, you''ll be able to:**

- Make sense of the next traceback you see
- Recognize some of the more common tracebacks
- Log a traceback successfully while still handling the exception
## What is a Python Traceback?

A traceback is a report containing the function calls made in your code at a specific point. Tracebacks are known by many names, including **stack trace**, **stack traceback**, **backtrace**, and maybe others. In Python the term used in **traceback**. 

When your program results in an exception, Python will print the current traceback to help you know what went wrong. Below is an example to illustrate the situation:

```python
# example.py
def greet(someone):
	print('hello, ' + someone)

greet('Chad')
```

Here, `greet()` gets called with the parameter `someone`. However in `greet()`, that variable name is not used. Instead, it has been misspelled as `someon` in the `print()` call. 

> [!NOTE]
> **Note**: This tutorial assumes you understand Python exceptions. If you are unfamiliar or just want a refresher, then you should check out [Python Exceptions: An Introduction](https://realpython.com/python-exceptions/).

When you run this program, you'll get the following traceback:

```
python example.py
Traceback (most recent call last):
  file "/path/to/example.py", line 4 in <module>
    greet('Chad')
  File "/path/to/example.py", line 2, in greet
    print("Hello, " + someon)
NameError: name 'someon' is not defined
  ```

The traceback output has all of the information you'll need to diagnose the issue. The final line of the traceback output tells you what type of exception was raided along with some relevant information about that exception. The previous lines of the traceback point out the code that resulted in the exception being raised. 

In the above traceback, the exception was a `NameError`, which means that there is a reference to some name (variable, function, class) that hasn't been defined. In this case, the name referenced is `someon`.

The final line in this case has enough information to help you fix the problem. Searching the code for the name `someon`, which is a misspelling, will point you in the right direction. Often, however, your code is a lot more complicated. 
## How Do You Read a Python Traceback?

The Python traceback contains a lot of helpful information when you're trying to determine the reason for an exception being raised in your code. In this section, you'll walk through different tracebacks in order to understand the different bits of information contained in a traceback.
### Python Traceback Overview

![](https://i.imgur.com/9mw65KP.png)

In Python, it's best to read the traceback from the bottom up:

1. **Blue Box**: The last line of the traceback is the error message line. It contains the exception name that was raised. 
2. **Green Box**: After the exception name is the error message. This message usually contains helpful information for understanding the reason for the exception being raised. 
3. **Yellow Box**: Further up the traceback are the various function calls moving from bottom to top, most recent to learn recent. These calls are represented by two-line entries for each call. The first line of each call contains information like the file name, line number, and module name, all specifying where the code can be found.
4. **Red underline**: The second line for these calls contains the actual code that was executed. 

There are a few differences between traceback output when you're executing your code in the command-line and running code in the [REPL](https://realpython.com/python-repl/). Below is the same code from the previous section executed in a REPL and the resulting traceback output:

```
>>> def greet(someone):
...   print('Hello, ' + someon)
... 
>>> greet('Chad')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 2, in greet
NameError: name 'someon' is not defined
```

Notice that in the place of file names, you get `<stdin>`. This makes sense since you typed the code in through standard input. Also, the executed lines of code are not displayed in the traceback.

> [!NOTE]
> **Note**: If you're used to seeing stack traces in other programming languages, then you'll notice a major difference in the way a Python traceback looks in comparison. Most other languages print the exception at the top and then go from top to bottom, most recent calls to least recent. 
> 
> It has already been said, but just to reiterate, a Python traceback should be read from bottom to top. This is very helpful since the traceback is printed out and your terminal (or wherever you are reading the traceback) usually ends up at the bottom of the output, giving you the perfect place to start reading the traceback.
## Specific Traceback Walkthrough

Going through some specific traceback output will help you better understand and see what information the traceback will give you. The code below is used in the examples following to illustrate the information a Python traceback gives you:

```python
# greetings.py
def who_to_greet(person):
    return person if person else input('Greet who? ')

def greet(someone, greeting='Hello'):
    print(greeting + ', ' + who_to_greet(someone))

def greet_many(people):
    for person in people:
        try:
            greet(person)
        except Exception:
            print('hi, ' + person)
```

Here, `who_to_greet()` takes a value, `person`, and either returns it or prompts for a value to return instead. 

Then, `greet()` takes a name to be greeted, `someone`, and an optional `greeting` value and calls `print()`. `who_to_greet()` is also called with the `someone` value passed in.

Finally, `greet_many()` will iterate over the list of `people` and call `greet()`. If there is an exception raised by calling `greet()`, then a simple backup greeting is printed.

This code doesn't have any bugs that would result in an exception being raised as long as the right input is provided. 

If you add a call to `greet()` to the bottom of `greetings.py` and specify a keyword argument that it isn't expecting (for example, `greet('Chad', greting='Yo')`), then you'll get the following traceback:

```
$ python example.py
Traceback (most recent call last):
  File "/path/to/greetings.py", line 19, in <module>
    greet('Chad', greting='Yo')
TypeError: greet() got an unexpected keyword argument 'greting'
```

Once again, with a Python traceback, it's best to work backward, moving up the output. Starting at the final line of the traceback, you can see that the exception was a `TypeError`. The messages that follow the exception type, everything after the colon, give you some great information. It tells you that `greet()` was called with a keyword argument that it didn't expect. The unknown argument name is also given to you: `greting`.

Moving up, you can see the line that resulted in the exception. In this case, it's the `greet()` call that we added to the bottom of `greetings.py`.

The next line up gives you the path to the file where the code exists, the line number of that file where the code can be found, and which module it's in. In this case, because our code isn't using any other Python modules, we just see `<module>` here, meaning that this is the file that is being executed. 

With a different file and different input, you can see the traceback really pointing you in the right direction to find the issue. If you are following along, remove the buggy `greet()` call from the bottom of `greetings.py` and add the following file to your directory:

```python
# example.py
from greetings import greet

greet(1)
```

Here you've set up another Python file that is importing your previous module, `greetings.py`, and using `greet()` from it. Here's what happens if you now run `example.py`:

```
$ python example.py
Traceback (most recent call last):
  File "/path/to/example.py", line 3, in <module>
    greet(1)
  File "/path/to/greetings.py", line 5, in greet
    print(greeting + ', ' + who_to_greet(someone))
TypeError: must be str, not int
```

The exception raised in this case is a `TypeError` again, but this time the message is a little less helpful. It tells you that somewhere in the code it was expecting to work with a string, but an integer was given. 

Moving up, you see the line of code that was executed. Then the file and line number of the code. This time, however, instead of `<module>`, we get the name of the function that was being executed, `greet()`.

Moving up to the next executed line of code, we see our problematic `greet()` call passing in an integer. 

Sometimes after an exception is raised, another bit of code catches that exception and also results in an exception. In these situations, Python will output all exception tracebacks in the order in which they are received, once gain ending in the most recently raised exception's traceback.

Since this can be a little confusing, here's an example. Add a call to `greet_many()` to the bottom of `greetings.py`.

```python
# greetings.py

greet_many(['Chad', 'Dan', 1])
```

This should result in printing greetings to all three people. If you run this code, you'll see an example of the multiple tracebacks being output:

