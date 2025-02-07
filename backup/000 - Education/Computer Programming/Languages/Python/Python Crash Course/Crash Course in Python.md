---
up: "[[000 - Education/Computer Programming/Languages/Python/Python|Python]]"
tags:
  - "#education/computerprogramming/languages/python/crashcourse"
---

### Who is this book for? 

The goal of this book is to bring you up to speed with Python as quickly as possible so you can build programs that work -- games, data visualizations, and web applications -- while developing a foundation in programming that will serve you well for the rest of your life. 

### What can you expect to learn?

The purpose of this book is to make you a good programmer in general and good Python programmer in particular. 

You'll learn efficiently and adopt good habits as you gain a solid foundation in general programming concepts. 

After completing *Python Crash Course*, you should be ready to move on to more advanced Python concepts, and your next programming language will be easier to grasp.

### Why Python? 

Every year, I consider whether to continue using Python or move on to a different language, perhaps one that's newer to the programming world. Python is an incredibly efficient language, your programs will do more in fewer lines of code than many other languages would require.

Python's syntax will also help you write "clean" code. Your code will be easier to read, easier to debug, and easier to extend and build upon, compared to other languages. 

People us Python for many purposes: to make games, build web applications, solve business problems, and develop internal tools at all kinds of interesting companies.

# Part 1: Basics

> Teaches the basic concepts you'll need to write Python programs. Many of these concepts are common to all programming languages, so they'll be useful throughout your life as a programmer.

### Getting Started

> The `>>>` will be referred to as a *Python Prompt*, and indicates that you should be using a terminal window. 

"Hello World!" serves more than just good luck for learning a new programming language. 
- It also means that any programs run in that environment should work. 

##### About the VS Code Editor

> *VSCode* is a powerful, professional quality text editor that's free and beginner-friendly. VS Code is great for both simple and complex projects, so if you become comfortable using it while learning Python, you can continue using it as you progress to larger and more complicated projects.

##### Python on Different Operating Systems

> Python is a cross-platform programming language, which means it runs on all the major operating systems. Any Python program you write should run on any modern computer that has Python installed. 

##### Running Python from a Terminal on macOS and Linux

> us `cd` to navigate through the filesystem in a terminal session
> use `ls` to list all non-hidden files that exist in the current directories

Use `cd` to navigate to the directory that holds python code and .py files, then run the file using the command `python3 <file_name.py>`

# Chapter 2: Variables and Simple Data Types

### What Really Happens When You Run hello_world.py?

> When you run the *hello_world.py*, the ending .py indicates that the file is a Python program. Your editor then runs the file through the *Python interpreter*, which reads through the program and determines what each word in the program means.

*Syntax highlighting* is a useful feature of code editors that changes the color of certain aspects of Python code for better readability.

### Variables

> Let's try using variables in *hello_world.py*. Add a new line at the beginning of the file, and modify the second line:

We've added a *variable* named `message`. Every variable is connected to a *value*, which is the information associated with that variable. In this case, the value is the "*Hello Python World!*" text. 

Let's add to our program from earlier:

```python
message = ("Hello Python World!")
print(message)

# New Code
message = ("Hello Python Crash Course World!")
print(message)

```

> You can change the value of a variable in your program at any time, and Python will always keep track of its current value.

### Naming and Using Variables

> When you're busy using Python variables, you need to adhere to a few rules and guidelines. 
> 	Breaking some of these rules will cause errors; other guide-lines just help you write code that's easier to read and understand.

Be sure to keep the following rules in mind when working with variables:

- Variable names can contain only letters, numbers and underscores. They can start with a letter or underscore, but not with a number. 
- Spaces are not allowed in variable names, but underscores can be used to separate words in variable names
- Avoid using Python keywords and function names as variable names. For example, do not use the word print as a variable name; Python has reserved it for a specific purpose.
- Variable names should be short but descriptive. 
- Be careful when using lowecase letter *l* and the uppercase letter *O* because they can be confused with a 1 or a 0.

### Avoiding Name Errors when using Variables

When an error occurs in Python, the interpreter does its best to help you figure out where the problem is. The interpreter provides a traceback when a program cannot run successfully. A *traceback* is a record of where the interpreter ran into trouble when trying to execute your code.

Many programming errors are simple, single-character typos in one line of a program. If you find yourself spending a long time searching for one of these errors, know that you’re in good company. Many experienced and talented programmers spend hours hunting down these kinds of tiny errors. Try to laugh about it and move on, knowing it will happen frequently throughout your programming life.

### Variables are Labels

> Variables are often described as boxes you can store values in. 

- This idea is helpful the first few times you use a variable, but it isn't an accurate way to describe how variables are represented internally in Python. It's much better to think of variables as labels that you can assign to values.

> You can also say that a variable references a certain value.

At some point, you'll see unexpected behavior from a variable, and an accurate undersanding of how variables work will help you identify what's happening in your code. 

### Strings

> Because most programs define and gather some sort of data and then do something useful with it, it helps to classify different types of data. 

A *string* is a series of characters. Anything inside quotes is considered a string in Python, and you can use single or double quotes around your strings like this:

`"This is a string."`
`'This is also a string.'`

##### Changing Case in a String with Methods

> One of the simplest tasks you can do with strings is change the case of the words in a string.

```python
name = "ada lovelace"
print(name.title())

Ada Lovelace
```
> In this example, the variable *name* refers to the lowercase string "ada lovelace".
> The method **title()** appears after the variable in the **print()** call. 
> A **method** is an action that Python can perform on a piece of data. 
> The dot (.) after **name** in **name.title()** tells Python to make the **title()** method act on the variable **name**.

- Every method is followed by a set of parenthesis, because methods often need additional information to do their work.
- That information is provided inside the parenthesis.

> The `title()` method changes each word to title case, where each word begins with a capital letter. 

Several other useful methods are available for dealing with case as well:

```python
name = "Ada Lovelace"
print(name.upper())
print(name.lower())

#output:
ADA LOVELACE
ada lovelace
```

> The `lower()` method is particularly useful for storing data. You typically won't want to trust the capitalization that your users provide, so you'll convert strings to lowercase before storing them.
> - Then, when you want to display the information, you'll use the case that makes the most sense for each string.

##### Using Variables in Strings

> In some situations, you might want to use a variable's value inside a string. For example, you might want to use two variables to represent a first name and a last name, respectively, and then combine those values to display someone's full name.

```python
first_name = "ada"
last_name = "lovelace"
full_name = f"{first_name} {last_name}"
print(full_name)
```
> The output is: ada lovelace

> To insert a variable's value into a string, place the letter `f` immediately before the opening quotation mark.
> 	Put braces around the name or names of any variable you want to use inside the string. 
> 	Python will replace each variable with its value when the string is displayed.

These strings are called *f-strings*. The *f* is for *format*, because Python formats the string by replacing the name of any variable in braces with its value.

==You can do a lot with f-strings. For example, you can use f-strings to compose complete messages using the information associated with a variable, as shown here:==

```python
first_name = "ada"
last_name = "lovelace"
full_name = f"{first_name} {last_name}"
print(f"Hello, {full_name.title()}!")
```

The full name is used in a sentence that greets the user, and the `title()` method changes the name to title case: `Hello, Ada Lovelace!`

You can also use f-strings to compose a message, and then assign the entire message to a variable:

```python
first_name = "ada"
last_name = "lovelace"
full_name = f"{first_name} {last_name}"
message = f"Hello, {full_name.title()}!"
print(message)
```

This code does the same thing as above, printing `Hello, Ada Lovelace!`, but does it in a more simplified manner.

##### Adding Whitespace to Strings with Tabs or Newlines

> In programminng, **Whitespace*** refers to any nonprinting characters, such as spaces, tabs, and end-of-line symbols. You can use whitespace to organize your output so it's easier for users to read.

To add a tab to your text, use the character combination `\t:`

```python
print("Python")
Python
print("\tPython")
  Python
```

To add a newline in a string, use the character combination `\n:`

```python
>>> print("Languages:\nPython\nC\nJavaScript")
Languages:
Python
C
JavaScript
```

You can also combine tabs and newlines in a single string. The string `\n\t` tells Python to move to a new line, and start the next line with a tab. 

```python
print("Languages:\n\tPython\n\tC\n\tJavaScript")
Languages:
  Python
  C
  JavaScript
```

> Newlines and tabs will be very useful in the next two chapters, when you start to produce many lines of output from just a few lines of code.

### Stripping Whitespace

> Extra whitespace can be confusing in your programs. To programmers, `python` and `python ` look the same, but they are two different strings.

- Python considers the extra space in `Python ` significant unless told otherwise.

It's important to consider whitespace when programming, because you'll often want to compare two strings to determine whether they are the same. For example, one important instance might involve checking people's usernames when they log into a website. 

- Extra whitespace can be confusing in much simpler situations as well.
- Fortunately, Python makes it easy to eliminate extra whitespace from the data people enter.

```python
1 >>> favorite_language = 'python '
2 >>> favorite_language
'python '
3 >>> favorite_language.rstrip()
'python'
4 >>> favorite_language
'python '
```

> The `.rstrip()` method acts on the variable `favorite_language`, and the extra space is removed. 
> 	However, it is only removed temporarily. 
> 	If you ask for the value of `favorite_language` again, the string looks the same as when it was entered, including the extra whitespace. 

1. The value associated with `favorite_language` contains extra whitespace at the end of the string. When you ask Python for this value in a terminal session, you can see the space at the end of the value. 
2. When the `.rstrip()` method acts on the variable `favorite_language`, this extra space is removed. 

However, it is only removed *temporarily*. If you ask for the value of `favorite_language` again, the string looks the same as when it was entered, including the extra whitespace. 

To remove the extra whitespace from the string *permanently*, you have associate the stripped value with the variable name:

```Python
>>> favorite_language = 'python '
>>> favorite_language = favorite_language.rstrip()
>>> favorite_language
'python'
```

To remove the whitespace from the string, you strip the whitespace from the right side of the string and then associate this new value with the original variable. 

Changing a variable's value is done often in programming.

- This is how a variable's value can be *updated as a program is executed or in response to user input*.
- You can also strip whitespace from the left side of a string using the `lstrip()` method, or from both sides at once using `strip()`.

```python
>>> favorite_language = ' python '
>>> favorite_language.rstrip()
' python'
>>> favorite_language.lstrip()
'python '
>>> favorite_language.strip()
'python'
```

> In this example, the value of the variable `favorite_language` has whitespace at the beginning and at the end. 

1. The whitespace from the right side is removed with `.rstrip()`
2. The whitespace from the left side is removed with `.lstrip()`
3. Then, from both sides using `strip()`

These stripping functions are used most often to clean up user input before it's stored in a program.
### Removing Prefixes

> When working with strings, another common task is to remove a prefix. Consider a URL with the common prefix `https://`. We want to remove this prefix, so we can focus on just the part of the URL that users need to enter into an address bar.

```Python
>>> nostarch_url = 'https://nostarch.com'
>>> nostarch_url.removeprefix('https://')
'nostarch.com'
```

1. Enter the name of the variable followed by a dot, and then the method `.removeprefix()`
2. Inside the parenthesis, enter the prefix you wish to remove from the original string.

> Like the methods for removing whitespace, `removeprefix()` leaves the original string unchanged. If you want to keep the new value with the pre-fix removed, either **reassign** it to the original variable or assign it to a new variable:

```python
>>> simple_url = nostarch_url.removeprefix('https://')
```
### Avoiding Syntax Errors in Strings

A *syntax error* occurs when Python doesn't recognize a section of your program as valid Python code. For example, if you use an apostrophe within single quotes, you'll produce an error. 

This happens because Python interprets everything between the first single quote and the apostrophe as a string. It then tries to interpret the rest of the text as Python code, which causes errors.

> Here's how to use single and double quotes correctly.

```Python
message = "One of Python's strengths is its diverse community."
print(message)
```

> This program will print the output correctly, as the apostrophe is within a set of double quotes.

```python
message = 'One of Python's strengths is its diverse community.'
print(message)
```

> This program will return a syntax error at line 1, as the apostrophe in "Python's" will cause the rest of the text to be interpreted as Python code and not a string.

**Syntax Errors** are often the least specific type of error, so they can be difficult and frustrating to locate and fix.
### Numbers

> Numbers are used quite often in programming to keep score in games, represent data in visualizations, store information in web applications, and so on.

Python treats numbers in several different ways, depending on how they're being used. Let's first look at how Python manages integers, because they're the simplest to work with.
#### Integers

> you can add (`+`), subtract (`-`), multiply (`*`), and divide (`/`) integers in Python. 

```Python
>>> 2 + 3
5
>>> 3 - 2
1
>>> 2 * 3
6
>>> 3 / 2
1.5
```

> In a terminal session, Python simply returns the result of the operation. Python uses two multiplication symbols to represent *exponents*.

```Python
>>> 3 ** 2
9
>>> 3 ** 3
27
>>> 10 ** 6
1000000
```

Python supports the order of operations too, so you can use multiple operations in one expression. You can also use parenthesis to modify the order of operations so Python can evaluate your expression in the order you specify. 

```Python
>>> 2 + 3*4
14
>>> (2 + 3) * 4
20
```

> The spacing in these examples has no effect on how Python evaluates the expressions; it simply helps you more quickly spot the operations that have priority when you're reading through the code. 

### Floats

Python calls any number with a decimal point a ***float***. 

- This term is used in *most programming languages*, and it refers to the fact that a decimal point can appear at any position in a number. Every programming language must be carefully designed to properly manage decimal numbers so numbers behave appropriately, no matter where the decimal point appears. 

> For the most part, you can use floats without worrying about how they behave. 

```Python
>>> 0.1 + 0.1
0.2
>>> 0.2 + 0.2
0.4
>>> 2 * 0.1
0.2
>>> 2 * 0.2
0.4
```

However, be aware that you can sometimes get an *arbitrary number* of decimal places in your answer:

```Python
>>> 0.2 + 0.1
0.30000000000000004
>>> 3 * 0.1
0.30000000000000004
```

This happens with all languages and is of little concern. Python tries to find a way to represent the result as precisely as possible, which is sometimes difficult given how computers have to represent numbers internally. 

### Integers and Floats

> When you divide any two numbers, even if they are integers that result in a whole number, you'll always get a float: