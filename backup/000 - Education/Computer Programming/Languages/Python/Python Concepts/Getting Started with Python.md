---
up: "[[Python Concepts]]"
tags:
  - "#education/computerprogramming/languages/python/concepts/start"
prev: "[[Python Fundamentals]]"
---


Python is a versatile, high-level programming language that is widely supported across all major operating systems. 

You can run Python on your computer using the following two methods:

- Run Python online
- Install Python on your computer

In this tutorial, we will learn both methods.
## Run Python Online

To execute Python code, you need to have a Python interpreter installed on your system. However, if you want to start immediately, you can use our free [online Python editor](https://www.programiz.com/python-programming/online-compiler/).

The online editor enables you to run Python code directly in your browser -- no installation required.
## Install Python on Your Computer

For those who want to install Python on your computer, this guide will walk you through the installation process on Windows, macOS, and Linux (Ubuntu).

https://www.programiz.com/python-programming/getting-started
## Run Your First Python Program

First open VSCode, click on the File in the top menu and then select New File. 

Then, save the file with a `.py` extension by clicking on **File** again, then **Save As**, and type your filename ending in `.py` (Here, we are saving it as Hello World.py).

Before you start coding, make sure the Python extension is installed in VS Code. Open VS code and click on Extensions on the left sidebar. Then, search for the **Python** extension by Microsoft and click on install.

Now, write the following line into your file:

```python
print("Hello World")
```

Then click on the **run** button on the top right side of your screen.

You should see Hello World printed to the command prompt.

Now that you have set everything up to run Python programs on your computer, you'll be learning how the basic program works in Python in the next tutorial.
# Your First Python Program

In the previous tutorial, you learned how to Install Python on your computer. Now, let's write a simple program.

The following program displays `Hello, World!` on the screen.

```python
print("Hello World!")
```
```
Hello World!
```

> [!NOTE]
> **Note:** A `Hello World!` program includes the basic syntax of a programming language and helps beginners understand the structure before getting started. That's why it is a common practice to introduce a new language using a `Hello World!` program.

## Working of the Program

Congratulations on writing your first Python program. Now, let's see how the above program works.

![](https://i.imgur.com/Tl2dvRJ.png)

In Python, anything inside the `print()` statement is displayed on the screen.

There are two things to note about `print()`:

- everything we want to display on the screen is included inside of the parenthesis `()`.
- The text we want to print is displayed within double quotes `""`.

We can also use single quotes to print text on the screen. For example:

```python
print('Hello World!')
```

is the same as:

```python
print("Hello World!")
```

To be consistent, we will be using double quotes throughout the tutorials. 

Next, we will be learning about Python comments.
### Video: Introduction to Python

https://youtu.be/B7G5B8P8k9s?list=PL98qAXLA6afuh50qD2MdAj3ofYjZR_Phn
# Python Comments

In the previous tutorial, you learned to write your first [Python program](https://www.programiz.com/python-programming/getting-started). Now, let's learn about Python comments.

> [!Important]
> **Important!**: We are introducing comments early in this tutorial series because we will be using them to explain the code in upcoming tutorials.

Comments are hints that we add to our code to make it easier to understand. Python comments start with `#`, for example:

```python
# print a number
print(25)
```

Here, `# print a number` is a comment. Comments are completely ignored and not executed by code editors.

> [!Important]
> **Important**: The purpose of this tutorial is to help you understand comments, so you can ignore other concepts used in the program. We will learn about those later. 
## Single-Line Comment

We use the **hash** (`#`) symbol to write a single-line comment. For example:

```python
# declare a variable
name = "John"

# print name
print(name)
```

In the above example, we have used three single-line comments:

- `# declare a variable`
- `# print name`
- `# john`

A **single-line comment** starts with a `#` and extends up to the end of the line. We can also use single line comments alongside the code:

```
print(name) # john
```

> [!NOTE]
> Remember the keyboard shortcut to apply comments. In most text editors, it's **Ctrl + /** if you are on Windows & **Cmd + /** if you are on a Mac.
## Multi-Line Comments

Unlike languages like C++ and Java, Python doesn't have a dedicated method to write multi-line comments. However, we can achieve the same effect by using the hash (`#`) symbol at the beginning of each line. Let's look at an example.

```python
# This is an example of a multiline comment
# created using multiple single-line comments
# The code prints the text Hello World
print("Hello, World!")
```

We can also use multiline strings as comments like:
### Output:

```
Hello World!
```

> [!NOTE]
> **Note:** Remember you will learn about these programming concepts in upcoming tutorials. For now. you can just focus on the usage of comments.
## Preventing Executing Code Using Comments

Comments are valuable when debugging code.

If we encounter an error while running a program, instead of removing code segments, we can "comment them out" to prevent execution. For example:

```python
number1 = 10
number2 = 15

sum = number1 + number2

print("The sum is:", sum)
print("The product is:", product)
```

Here, the code throws an error because we have not identified a `product` variable. Instead of removing the line causing the error, we can comment it.

For example:

```python
number1 = 10
number2 = 15

sum = number1 + number2

print("The sum is:", sum)
# print('The product is:', product)
```
```
The sum is 25
```

Here, the code runs without any errors. 

We have resolved the error using a comment. Now if you need to calculate the `product` in the near future, you can uncomment it.

> [!NOTE]
> **Note:** This approach comes in handy while working with large files. Instead of deleting any line, we can use comments and identify which one is causing an error.

---

## Why Use Comments?

We should use comments:

- For future references, as comments make our code readable.
- For debugging.
- For code collaboration, as comments help peer developers to understand each other's code.

> [!NOTE]
> **Note**: Comments are not and should not be used as a substitute to explain poorly written code. Always try to write clean, understandable code, and then use comments as an addition.
> 
> In most cases, always use comments to explain 'why' rather than 'how' and you are good to go.

Next, we will start learning fundamental concepts of Python programming.
### Video: Comments in Python

https://youtu.be/rhF1x2lnRQA?list=PL98qAXLA6afuh50qD2MdAj3ofYjZR_Phn

