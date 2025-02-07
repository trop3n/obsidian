---
up: "[[000 - Education/Computer Programming/Languages/Python/Python|Python]]"
tags: "#education/computerprogramming/languages/python/diveintopy"
source: https://diveintopython3.net/
---

# Chapter 1: First Python Program

Convention dictates that I should bore you with the fundamental building blocks of programming, so we can slowly work up to building something useful. Let's skip that. Here is a complete, working Python program. It probably makes absolutely no sense to you. Don't worry about that, because we're going to dissect it line by line. But read through it first and see what, if anything, you can make of it. 

```python
SUFFIXES = {1000: ['KB', 'MB', 'GB', 'TB', 'PB', 'EB', 'ZB', 'YB'],

1024: ['KiB', 'MiB', 'GiB', 'TiB', 'PiB', 'EiB', 'ZiB', 'YiB']}

  

def approximate_size(size, a_kilobyte_is_1024_bytes=True):

	'''Convert a file size to human-readable form.

	Keyword arguments:

	size -- file size in bytes

	a_kilobyte_is_1024_bytes -- if True (default), use multiples of 1024

	if False, use multiples of 1000

	Returns: string

	'''

  

	if size < 0:
		raise ValueError('number must be non-negative')

	multiple = 1024 if a_kilobyte_is_1024_bytes else 1000
	for suffix in SUFFIXES[multiple]:
		size /= multiple
		if size < multiple:
			return '{0:.1f} {1}'.format(size, suffix)

	raise ValueError('number too large')

  

if __name__ == '__main__':
	print(approximate_size(1000000000000, False))
	print(approximate_size(1000000000000))
```

```Output
1.0 TB
931.3 GiB
```

What just happened? You executed your first Python program. You called the Python interpreter on the command line, and you passed the name of the script you wanted Python to execute. The script defines a single function, the `approximate_size` function, which takes an exact file size in bytes and calculates a "pretty" (but approximate size). 

(You’ve probably seen this in Windows Explorer, or the Mac OS X Finder, or Nautilus or Dolphin or Thunar on Linux. If you display a folder of documents as a multi-column list, it will display a table with the document icon, the document name, the size, type, last-modified date, and so on. If the folder contains a 1093-byte file named `TODO`, your file manager won’t display `TODO 1093 bytes`; it’ll say something like `TODO 1 KB` instead. That’s what the `approximate_size()` function does.)

Look at the bottom of the script, and you'll see two calls to `print(approximate_size(arguments))`. These are ***Function Calls*** -- first calling the `approximate_size()` function and passing a number of arguments, then taking the return value and passing it straight on to the `print()` function. The `print()` function is built-in, you'll *never see an explicit declaration of it*. You can just use it anytime, anywhere. (There are lots of built in functions, and lots more functions that are separated into *modules*, Patience, Grasshopper.)

So why does running the script on the command line give the same output every time? We'll get into that. First, let's look at that `approximate_size()` function.
## 1.2 Declaring Functions

Python has functions like most other languages, but it does not have separate header files like C++ or `interface/implementation` sections like Pascal. When you need a function, just declare it, like this:

```python
def approximate_size(size, a_kilobyte_is_1024_bytes=True):
```

The keyword `def` starts the function declaration, followed by the function name, followed by the arguments in parenthesis. Multiple arguments are separated with commas.

Also note that the function *doesn't define a return data type.* Python functions do not specify the datatype of their return value; they don't even specify whether or not they return a value. (In fact, every Python function returns a value; if the function ever executes a `return` statement, it will return that value, otherwise it will return `None`, the Python **null value**.)

> [!NOTE] ☞
> In Java or other statically-typed languages, you must **specify the datatype of the function return value** and each function argument. In Python, you never explicitly specify the datatype of anything. Based on what value you assign, Python keeps track of the datatype internally.
## 1.2.1 Optional and Named Arguments

Python allows function arguments to have default values, if the function is called without the argument, the argument gets its default value. Furthermore, arguments can be specified in any order by using named arguments. 

Let's take another look at that `approximate_size()` function declaration:

```python
def approximate_size(size, a_kilobyte_is_1024_bytes=True):
```

The second argument, `a_kilobyte_is_1024_bytes`, specifies a default value of `True`. This means the argument is *optional*; you can call the function without it, and Python will act as if you had called it with `True` as a second parameter. 

Now look at the bottom of the script:

```python
if __name__ == '__main__':
	print(approximate_size(1000000000000, False))
	print(approximate_size(1000000000000))
```

1. This calls the `approximate_size` function with **two arguments**. Within the `approximate_size()` function, `a_kilobyte_is_1024_bytes` will be `False`, since you explicitly passed `False` as the second argument. 
2. This calls the `approximate_size` function with only **one argument**. But that's okay, because the second argument is optional! Since the called doesn't specify, the second argument defaults to `True`, as defined by the **function declaration**.

You can pass values into a function by name.

```python
>>> from humansize import approximate_size
>>> approximate_size(4000, a_kilobyte_is_1024_bytes=False) # 1
'4.0 KB'
>>> approximate_size(size=4000, a_kilobyte_is_1024_bytes=False) # 2
'4.0 KB'
>>> approximate_size(a_kilobyte_is_1024_bytes=False, size=4000) # 3
'4.0 KB'
>>> approximate_size(a_kilobyte_is_1024_bytes=False, 4000) # 4
  File "<stdin>", Line 1
SyntaxError: non-keyword arg after keyword arg
>>> approximate_size(size=4000, False) # 5
  File "<stdin>", line 1
SyntaxError: non-keyword arg after keyword arg
```

1. This calls the `appropriate_size()` function with `4000` for the first argument (`size`) and `False` for the argument named `a_kilobyte_is_1024_bytes` (That happens to be the second argument, but doesn't matter, as you'll see in a minute.)
2. This calls the `appropriate_size()` function with `4000` for the argument named `size` and `False` for the argument named `a_kilobyte_is_1024_bytes`. (These named arguments happen to be in the same order as the arguments are listed in the function declaration, but that doesn't matter either.)
3. This calls the `approximate_size()` function with `False` for the argument named `a_kilobyte_is_1024_bytes` and `4000` for the argument named `size`. (See? I told you the order didn't matter.)
4. This call fails, because you have a named argument followed by an unnamed (positional) argument, and that *never works*. Reading the argument list from left to right, once you have a single named argument, the rest of the arguments must also be named.
5. This call fails too, for the same reason as the previous call. Is that surprising? After all, you passed `4000` for the argument named `size`, then "obviously" that `False` value was meant for the `a_kilobyte_is_1024_bytes` argument. But Python doesn't work that way. As soon as you have a named argument, all arguments to the right of that need to be named arguments, too.
## 1.3 Writing Readable Code

I won't bore you with a long finger-wagging speech about the importance of documenting your code. Just know that code is written once but read many times, and the most important audience for your code is yourself, six months after writing it (i.e. you've forgotten everything but need to fix something). Python makes it easy to write readable code, so take advantage of it. 
### 1.3.1 Documentation Strings

You can document a Python function by giving it a documentation string (`docstring` for short). In this program, the `approximate_size()` function has a `docstring`:

```python
def approximate_size(size, a_kilobyte_is_1024_bytes=True):    
'''Convert a file size to human-readable form.    

Keyword arguments:    
size -- file size in bytes    
a_kilobyte_is_1024_bytes -- if True (default), use multiples of 1024                                              if False, use multiples of 1000    
Returns: string    

'''
```

Triple quotes signify a multi-line string. Everything between the start and end quotes is part of a single string, including carriage returns, leading whitespace, and other quote characters. You can use them anywhere, but you'll see them most often used when defining a `docstring`.

> [!NOTE] ☞
> Triple Quotes are also an easy way to define a string with both single and double quotes, like `qq/.../` in Perl 5.

Everything between the triple quotes is the function's `docstring`, which documents what the function does. A `docstring`, if it exists, must be the first thing defined in a function (that is, on the next line after the function declaration). You don't technically need to give your function a `docstring`, but you always should. I know you've heard this in every programming class you've ever taken, but Python gives you an added incentive: the `docstring` is available at runtime as an *attribute of the function*.


> [!NOTE] ☞
> Many Python IDEs use the `docstring` to provide context-sensitive documentation, so that when you type a function name, its `docstring` appears as a tooltip. This can be incredibly helpful, but it's only as good as the `docstrings` you write.
## 1.4 The `import` Search Path

Before this goes any further, I want to briefly mention the library search path. Python looks in several places when you try to import a module. Specifically, it looks in all the directories defined in `sys.path`. This is just a list, and you can easily view it or modify it with standard list methods. (You'll learn more about lists in [Native Datatypes](https://diveintopython3.net/native-datatypes.html#lists).)

```python
>>> import sys # 1
>>> sys.path   # 2
['',
 '/usr/lib/python31.zip',
 '/usr/lib/python3.1',
 '/usr/lib/python3.1/plat-linux@ETRAMACDEPPATH@'
 '/usr/lib/python3.1/lib-dynload',
 '/usr/lib/python3.1/dist-packages',
 '/usr/local/lib/python3.1/dist-packages']
>>> sys        # 3
<module 'sys' (built-in)>
>>> sys.path.insert(0, '/home/mark/diveintopython3/examples') # 4
>>> sys.path   # 5
['/home/mark/diveintopython3/examples',
 '',
 '/usr/lib/python31.zip
 '/usr/lib/python3.1,
 '/usr/lib/python3.1/plat-linux@EXTRAMACHDEPPATH@',
 '/usr/lib/python3.1/lib-dynload',
 '/usr/lib/python3.1/dist-packages',
 '/usr/local/lib/python3.1/dist-packages']
```

1. Importing the `sys` module makes all of it's functions and attributes available.
2. `sys.path` is a list of directory names that constitute the current search path. (Yours will look different, depending on your OS, Python version, and install location). Python will look through these directories (in this order) for a `.py` file whose name matches what you're trying to import.
3. Actually, I lied; the truth is more complicated than that, because not all modules are stored as `.py` files. Some are *built-in modules*; they are actually baked right into Python itself. Built-in modules behave just like regular modules, but their Python source code is not available, because they are not written in Python! (Like Python itself, these built-in modules are written in C.)
4. You can add a new directory to Python's search path at runtime by adding the directory name to `sys.path`, and then Python will look in that directory as well, whenever you try to import a module. The effect lasts as long as Python is running.
5. By using `sys.path.insert(0, new_path)`, you inserted a new directory as the first item of the `sys.path` list, and therefore at the beginning of Python's search path. This is almost what you want. In case of naming conflicts (for example, if Python ships with a verison 2 of a particular library but you want to use version 3), this ensures that your modules will be found and used instead of the modules that came with Python.
## 1.5 Everything is an Object

In case you missed it, I just said that Python functions have attributes, and that those attributes are available at runtime. A function, like everything else in Python, is an object. 

Run the interactive Python shell and follow along:

```python
import humansize # 1
print(humansize.approximate_size(4096, True)) # 2
4.0 KiB
print(humansize.approximate_size.__doc__) # 3
Convert a file size to human readable form.

    Keyword arguments:
    size -- file size in bytes
    a_kilobyte_is_1024_bytes -- if True (default), use multiples of 1024
                                if False, use multiples of 1000

    Returns: string
```

1. The first line imports the `humansize` program as a module - a chunk of code that you can use interactively, or from a larger Python program. Once you import a module, you can reference any of it's public functions, classes, or attributes. Modules can do this to access functionality of other modules, and you can do it in the Python interactive shell too. This is an important concept, and you'll see a lot more of it throughout this book.
2. When you want to use functions defined in imported modules, you need to include the module name. So you can't just say `approximate_size`; it must be `humansize.approximate_size`. If you've used classes in Java, this should feel vaguely familiar. 
3. Instead of calling the function as you would expect to, you asked for one of the function's attributes, `__doc__`.

> [!NOTE] ☞
> `import` in Python is like `require` in Perl. Once you `import` a Python module, you access it's functions with `module.function`; once you `require` a Perl module, you access its functions with `module::function`.
### 1.5.1 What's an Object?

Everything in Python is an **object**, and everything can have attributes and methods. All functions have a built-in attribute `__doc__`, which returns the `docstring` defined in the function's source code. The `sys` module is an object which has (among other things) an attribute called `path`. And so forth.

Still, this doesn't answer the more fundamental question: what is an object? Different programming languages define "object" in different ways. In some, it means that *all* objects *must* have attributes and methods; in others, it means that all objects are **subclassable**. In Python, the definition is looser. Some objects have neither attributes not methods, *but they could*. Not all objects are subclassable. But everything is an object in the sense that it can be assigned to a variable or passed as an argument to a function. 

You may have heard the term " first class object" in other programming contexts. In Python, functions are *first-class objects*. You can pass a functiona s an argument to another function. Modules are *first-class objects*. You can pass an entire module as an argument to a function. Classes are first-class objects, and individual instances of a class are also first-class objects.

This is important, so I'm going to repeat it in case you missed it the first few times: *everything in Python is an object*. Strings are objects. Functions are objects. Classes are objects. Class instances are objects. Even modules are objects.
## 1.6 Indenting Code 

Python functions have no explicit `begin` or `end`, and no curly braces to mark where the function code starts and stops. The only delimiter is a colon (:) and the indentation of the code itself.

```python
def approximate_size(size, a_kilobyte_is_1024_bytes=True):      # 1
	if size < 0:                                               # 2
		raise ValueError('number must be non-negative')       # 3
                                                     # 4
    multiple = 1024 if a_kilo_byte_is_1024_bytes else 1000
    for suffix in SUFFIXES[multiple]:                          # 5
	    size /= multiple
	    if size < multiple:
		    return '{0:.1f} {1}'.format(size, suffix)

	raise ValueError('number too large')
```

1.  Code blocks are defined by their indentation. By "code block" I mean functions, `if` statements, `for` loops, `while` loops and so forth. Indenting starts a block and unindenting ends it. There are no explicit braces, brackets, or keywords. This means that whitespace is significant, and must be consistent. In this example, the function code is indented four spaces. It doesn't need to be four spaces, it just needs to be consistent. The first line that is not indented marks the end of the function.
2. In Python, an `if` statement is followed by a code block. If the `if` expression evaluates to true, the indented block is executed, otherwise it falls to the `else` block (if any). Note the lack of parenthesis around the expression.
3. This line is inside the `if` code block. This `raise` statement will raise an exception (of type `ValueError`), but only if `size < 0`.
4. This is *not* the end of the function. Completely blank lines don't count. They can make the code more *readable*, but they don't count as code block delimiters. The function continues on the next line.
5. The `for` loops also marks the start of a code block. Code blocks can contain multiple lines, as along as they are all indented the same amount. This `for` loop has three lines of code in it. There is no special syntax for multi-line code blocks. Just indent and get on with your life.

After some initial protests and several snide analogies to Fortran, you will make peace with this and start seeing its benefits. One major benefit is that all Python programs look similar, since indentations is a ***language requirement*** and not a matter of style. This makes it easier to read and understand other people's Python code.

> [!NOTE] ☞
> Python uses carriage returns to separate statements and a colon and indentation to separate code blocks. C++ and Java use semicolons to separate statements and curly braces to separate code blocks.
## 1.7 Exceptions

Exceptions are everywhere in Python. Virtually every module in the Python standard library uses them, and Python itself will raise them in a lot of different circumstances. You'll see them repeatedly throughout this book. 

What is an **exception**? Usually it's an error, an indication that something went wrong. (Not all exceptions are errors, but nevermind that for now.) Some programming languages encourage the use of error return codes, which you *check*. Python encourages the use of **exceptions**, which you 
*handle*.

When an error occurs in the Python Shell, it prints out some details about the exception and how it happened, and that's that. This is called an ***unhandled exception***. When the exception was raided, there was no code to explicitly notice it and deal with it, so it bubbled its way back up to the top level of the Python Shell, which spits out some debugging information and calls it a day. In the shell, that's no big deal, but if that happened while your actual Python program was running, the entire program would come to a screeching halt if nothing handles the exception. Maybe that's what you want, maybe it isn't.

> [!NOTE] ☞
> Unlike Java, Python functions don't declare which exceptions they might raise. It's up to you to determine what possible exceptions you need to catch.

An exception doesn't need to result in a complete program crash, though. Exceptions can be *handled*. Sometimes an exception  is really because you have a bug in your code (like accessing a variable that doesn't exist), but sometimes an exception is something you can anticipate. If you're opening a file, it might not exist. If you're importing a module, it might not be installed. If you're connecting a database, it might be unavailable, or you might not have the correct security credentials to access it. If you know a line of code may raise an exception, you should handle the exception using a `try...except` block.

> [!NOTE] ☞
>Python uses `try...except` blocks to handle exceptions, and the `raise` statement to generate them. Java and C++ use `try...catch` blocks to handle exceptions, and the `throw` statement to generate them.

The `approximate_size()` function raises exceptions in two different cases: if the given `size` is larger than the function is designed to handle, or if it's less than zero.

```python
if size < 0:
	raise ValueError('number must be non-negative')
```

The syntax for an exception is simple enough. Use the `raise` statement, followed by the exception name, and an optional human-readable string for debugging purposes. The syntax is reminiscent of calling a function. (In reality, exceptions are implemented as classes, and this `raise` statement is actually creating an instance of the `ValueError` class and passing the string `'number must be non-negative` to its initialization method. But we're getting [we’re getting ahead of ourselves](https://diveintopython3.net/iterators.html#defining-classes)!) 

> [!NOTE] ☞
> You don't need to handle an exception in the function that raises it. If one function doesn't handle it, the exception is passed to the *calling function*, then that function's calling function, and so on "up the stack". If the exception is never handled, your program will crash, Python will print a "traceback" to standard error, and that's the end of that. Again, maybe that's what you want; it depends on what your program does. 
### 1.7.1 Catching Import Errors

One of Python's built-in exceptions is `ImportError`, which is raised when you try to import a module and fail. This can happen for a variety of reasons, but the simplest case is when the module doesn't exist in your [import search path](https://diveintopython3.net/your-first-python-program.html#importsearchpath). You can use this to include optional features in your program. For example, the [the `chardet` library](https://diveintopython3.net/case-study-porting-chardet-to-python-3.html) provides character encoding auto-detection. Perhaps your program wants to use this library _if it exists_, but continue gracefully if the user hasn’t installed it. You can do this with a `try..except` block.

```python
try:
	import chardet
except ImportError:
	chardet = None
```

Later, you can check for the presence of the `chardet` module with a simple `if` statement:

```python
if chardet:
	# do something
else:
	# continue anyway
```

Another common use of the `ImportError` exception is when two modules implement a common `API`, but one is more desirable than the other. (Maybe it's faster, or uses less memory). You can try to import one module but fall back to a different module if the first import fails. For example, the [the XML chapter](https://diveintopython3.net/xml.html) talks about two modules that implement a common `API`, called the `ElementTree API`. The first, `lxml`, is a third-party module that you need to download and install yourself. 
	The second, `xml.etree.ElementTree`, is slower but is part of the Python3 Standard Library.

```python
try:
	from lxml import etree
except ImportError:
	import xml.etree.ElementTree as etree
```

By the end of this `try...except` block you have imported *some* module and named it `etree`. Since both modules implement a common `API`, the rest of your code doesn't need to keep checking which module got imported. And since the module that *did* get imported is always called `etree`, the rest of your code doesn't need to be littered with `if` statements to call differently-named modules. 
## 1.8 Unbound Variables

Take another look at this line of code from the `approximate_size()` function:

```python
multiple = 1024 if a_kilobyte_is_1024_bytes else 1000
```

You never declare the variable `multiple`, you just assign a value to it. That's OK, because Python lets you do that. What Python will *not* let you do is reference a variable that has never been assigned a value. Trying to do so will raise a `NameError` exception.

```
>>> x
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'x' is not defined
>>> x = 1
>>> x
1
```

**You will thank Python for this one day**.
## 1.9 Everything is Case-Sensitive

All names in Python are case-sensitive: variable names, function names, class names, module names, exception names. If you can get it, set it, call it, construct it, import it, or raise it, it's **case-sensitive**.

```python
>>> an_integer = 1
>>> an_integer
1
>>> AN_INTEGER
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'AN_INTEGER' is not defined
>>> An_Integer
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'An_Integer' is not defined
>>> an_inteGer
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'an_inteGer' is not defined
```

And so on.
## 1.10 Running Scripts

Python modules are objects and have several useful attributes. You can use this to easily test your modules as your write them, by including a special block of code that executes when you run the Python file on the command line. Take the last few lines of `humansize.py`:

```python
if __name__ == '__main__':
	print(approximate_size(1000000000000, False))
	print(approximate_size(1000000000000))
```

> [!NOTE]
> Like C, Python uses `==` for comparison and `=` for assignment. Unlike C, Python does not support in-line assignment, so there’s no chance of accidentally assigning the value you thought you were comparing.

So what makes this `if` statement special? Well, ***modules are objects***, and all modules have a built-in attribute `__name__`. A module's `__name__` depends on how you're using the module. If you `import` the module, then `__name__` is the module's filename, without a directory or path extension. 

```python
>>> import humansize
>>> humansize.__name__
'humansize'
```

But you can also run the module directly as a standalone program, in which case `__name__` will be a special default value, `__main__`. Python will evaluate this `if` statement, find a true expression, and execute the `if` code block. In this case, to print two values.

```
c:\home\diveintopython3> c:\python31\python.exe humansize.py
1.0 TB
931.3 GiB
```

And that's your first Python Program!

                                ⁂
## 1.11 Further Reading

- PEP 257: Docstring Conventions explains what distinguishes a good `docstring` from a great `docstring`.
- Python Tutorial: Documentation Strings also touches on the subject.
- PEP 8: Style Guide for Python Code discusses good indentation style.
- Python Reference Manual explains what it means to say that everything in Python is an object, because some people are pedants and like to discuss that sort of thing at great length.
# Chapter 2: Native Datatypes

In Python, [every value has a datatype](https://diveintopython3.net/your-first-python-program.html#declaringfunctions), but you don't need to declare the datatype of variables. How does that work? Based on each variable's original assignment, Python figures out what type it is and keeps tracks of that internally. 

Python has many data types, here are the important ones:

1. ***Booleans***: either `True` or `False`.
2. ***Numbers***: can be integers (`1` and `2`), floats (`1.1` and `1.2`), fractions (`1/2` and `2/3`), or even complex numbers.
3. ***Strings*** are sequences of unicode characters, e.g. an `HTML` document.
4. ***Bytes*** and ***Byte Arrays*** e.g. a `JPEG` image file. 
5. ***Lists*** are ordered sequences of values
6. ***Tuples*** are ordered, *immutable* sequences of values.
7. ***Sets*** are unordered bags of values.
8. ***Dictionaries*** are unordered bags of *key-value pairs*.

Of course, there are more data types than these. [Everything is an object](https://diveintopython3.net/your-first-python-program.html#everythingisanobject) in Python, so there are types like *module*, *function*, *class*, *method*, *file* and even *compiled code*. You’ve already seen some of these: [modules have names](https://diveintopython3.net/your-first-python-program.html#runningscripts), [functions have `docstrings`](https://diveintopython3.net/your-first-python-program.html#docstrings), _&_c. You’ll learn about classes in [Classes _&_ Iterators](https://diveintopython3.net/iterators.html), and about files in [Files](https://diveintopython3.net/files.html).

Strings and bytes are important enough -- and complicated enough -- that they get their own chapter. Let's look at the others first.
## 2.2. Booleans

Booleans are either true or false. Python has two constants, clearly and cleverly named `True` and `False`, which can be used to assign boolean values directly. Expressions can also evaluate to a boolean value. In certain places (like `if` statements), Python expects and expression to evaluate to a boolean value. These places are called ***boolean contexts***. You can use virtually any expression in a boolean context, and Python will try to determine it's truth value. Different datatypes have different rules about which values are true or false in a boolean context. (This will make more sense once you see some concrete examples later in this chapter).

For example, take this snippet from [`humansize.py`](https://diveintopython3.net/your-first-python-program.html#divingin):

```python
if size < 0:
	raise ValueError('number must be non-negative')
```

`size` is an integer, 0 is an integer, and `<` is a numerical operator. The result of the expression `size < 0` is *always a boolean*. 

Due to some legacy issues left over from Python 2, booleans can be treated as numbers. `True` is `1` `False` is `0`.

```python
>>> True + True
2
>>> True - False
1
>>> True * False
0
>>> True / False
ZeroDivisionError
```

Ew, ew, ew! Don’t do that. Forget I even mentioned it.
## 2.3. Numbers

Numbers are awesome. There are so many to choose from. Python supports both integers and floating point numbers. There's no type declaration to distinguish them; Python tells them apart by the presence or absence of a decimal point. 

```python
>>> type(1) ①
<class 'int'>
>>> isinstance(1, int) ②
True
>>> 1 + 1 ③
2
>>> 1 + 1.0 ④
2.0
>>> type(2.0)
<class 'float'>
```

1. You can use the `type()` function to check the type of any value or variable. As you might expect, `1` is an `int`.
2. Similarly, you can use the `isinstance()` function to check whether a value or variable is of a given type.
3. Adding an `int` to and `int` yields an `int`
4. Adding an `int` to a `float` yields a `float`. Python coerces the `int` into a `float` to perform the addition, then returns a `float` as the result.
### 2.3.1. Coercing Integers to Floats and Vice-Versa

As we just saw, some operators (like addition) will coerce integers to floating point numbers as needed. We can also coerce them by ourselves.

```python
>>> float(2) ①
2.0
>>> int(2.0) ②
2
>>> int(2.5) ③
2
>>> int(-2.5) ④
-2
>>> 1.12345678901234567890 ⑤
1.1234567890123457
>>> type(1000000000000000) ⑥
<class 'int'>
```

1. You can explicitly coerce an `int` to a `float` by calling the `float()` function.
2. Unsurprisingly, you can also coerce a `float` to an `int` by calling `int()`.
3. The `int()` function will truncate, not round.
4. The `int()` function truncates negative numbers towards 0. It's a true truncate function, not a floor function.
5. Floating point numbers are accurate to 15 decimal places. 
6. Integers can be *arbitrarily large*.

> [!NOTE]
> Python 2 had separate types for `int` and `long`. The `int` datatype was limited by `sys.maxint`, which varied by platform but was usually `232-1`. Python 3 has just one integer type, which behaves mostly like the old `long` type from Python 2. See PEP 237 for details.
### 2.3.2. Common Numerical Operations

We can do all kinds of things with numbers.

```python
>>> 11 / 2 ①
5.5
>>> 11 // 2 ②
5
>>> −11 // 2 ③
−6
>>> 11.0 // 2 ④
5.0
>>> 11 ** 2 ⑤
121
>>> 11 % 2 ⑥
1
```

1. The `/` operator preforms floating point division. It returns a `float` even if both the numerator and denominator are `ints`.
2. The `//` operator performs a quirky kind of integer division. When the result is positive, you can think of it as truncating (not rounding) to 0 decimal places, but be *careful with that*.
3. When integer-dividing negative numbers, the `//` operator rounds "up" to the nearest integer. Mathematically speaking, it's rounding "down" since `-6` is less and `-5`, but it could trip you up if you were expecting it to truncate to `-5`.
4. The `//` operator doesn't always return an integer. If the numerator or denominator is a `float`, it will still round to the nearest integer, but the actual return value will be a `float`.
5. The `**` operator means "raised to the power of." `11^2` is `121`.
6. The `%` operator gives the remainder after performing integer division. `11` divided by `2` is `5` with a remainder of `1`, so the result here is `1`.

> [!NOTE]
> In Python 2, the `/` operator usually meant integer division, but you could make it behave like floating point division by including a special directive in your code. In Python 3, the `/` operator always means floating point division. See PEP 238 for details.
### 2.3.3 Fractions

Python isn't limited to integers and floating point numbers. It can also do all the fancy math your learned in high school and promptly forgot about.

```python
>>> import fractions ①
>>> x = fractions.Fraction(1, 3) ②
>>> x
Fraction(1, 3)
>>> x * 2 ③
Fraction(2, 3)
>>> fractions.Fraction(6, 4) ④
Fraction(3, 2)
>>> fractions.Fraction(0, 0) ⑤
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "fractions.py", line 96, in __new__
    raise ZeroDivisionError('Fraction(%s, 0)' % numerator)
ZeroDivisionError: Fraction(0, 0)
```

1. To start using fractions, import the `fractions` module. 
2. To define a fraction, create a `Fraction` object and pass in the numerator and denominator
3. You can perform all the usual mathematical operations with fractions. Operations return a new `Fraction` object, `2 * (1/3) = (2/3)`
4. The `Fraction` object will automatically reduce fractions. `(6/4) = (3/2)`
5. Python has the good sense not to create a fraction with a zero denominator.
### 2.3.4 Trigonometry

You can also do basic trigonometry in Python.

```python
>>> import math
>>> math.pi                    # 1
3.141592653589793
>>> math.sin(math.pi / 2)      # 2
1.0
>>> math.tan(math.pi / 4)      # 3
0.9999999999999999
```

1. The `math` module has a constant for π, the ratio of a circle's circumference to it's diameter.
2. The `math` module has all the basic trigonometric functions, including `sin()`, `cos()`, `tan()` and variants like `asin()`.
3. Note, however, that Python does not have infinite precision. `tan(π / 4)` should return `1.0`, not `0.99999999999999989`.
### 2.3.5 Numbers in a Boolean Context

We can use numbers in a Boolean context, such as an `if` statement. Zero values are false, and non-zero values are true.

> [!NOTE]
> Zero values are false, and non-zero values are true.

```python
>>> def is_it_true(anything): ①
...   if anything:
...     print("yes, it's true")
...   else:
...     print("no, it's false")
...
>>> is_it_true(1) ②
yes, it's true
>>> is_it_true(-1)
yes, it's true
>>> is_it_true(0)
no, it's false
>>> is_it_true(0.1) ③
yes, it's true
>>> is_it_true(0.0)
no, it's false
>>> import fractions
>>> is_it_true(fractions.Fraction(1, 2)) ④
yes, it's true
>>> is_it_true(fractions.Fraction(0, 1))
no, it's false
```

1. Did you know you can define your own functions in the Python interactive shell? Just press `ENTER` at the end of each line, and `ENTER` on a blank line to finish. 
2. In a boolean context, non-zero integers are true; 0 is false. 
3. Non-zero floating point numbers are true; `0.0` is false. Be careful with this one! If there's the slightest rounding error (not impossible, as we saw in previous section) then Python will be testing `0.0000000000000001` instead of `0` and will return `True`.
4. Fractions can also be used in a boolean context. `Fraction(0, n)` is false for all values of `n`. All other functions are true.
## 2.4 Lists

Lists are Python's **workhorse datatype**. When we say "list", you might be thinking of "array whose size I have to declare in advance, that can only contain items of the same type, &c." Don't think that. Lists are much cooler than that. 

> A list in Python is like an array in Perl. In Perl 5, variables that store arrays always start with the `@` character; in Python, variables can be named anything, and Python keeps track of the datatype internally. 

> A list in Python is much more than an array in Java (although it can be used as one if that's really what you want out of life). A better analogy would be to the `ArrayList` class, which can hold arbitrary objects and can expand dynamically as new items are added.
### 2.4.1 Creating a List


