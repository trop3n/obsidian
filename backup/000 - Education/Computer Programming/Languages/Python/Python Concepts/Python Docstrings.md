---
up: "[[Python Docstrings]]"
tags:
  - "#education/computerprogramming/languages/python/concepts/docstrings"
prev:
---

# Python Docstrings
https://www.programiz.com/python-programming/docstrings

Python docstrings are the **string literals** that appear right after the definition of a function, method, class, or module. Let's take an example.
## Example 1: Docstrings

```python
def square(n):
	'''Take a number n and return the square of n.'''
	return n**2
```

Here, the string literal is:

```python
'''Take a number n and return the square of n.'''
```

Inside the triple quotations marks is the **docstring** of the function `square()` as it appears right after its definition.

---
## Python Comments vs. Docstrings

[Comments](https://www.programiz.com/python-programming/comments) are descriptions that help programmers better understand the intent and functionality of the program. They are completely ignored by the Python interpreter.

In Python, the hash symbol `#` is used to write a single line comment. For example,

```python
# Program to print "Hello World"
print("Hello World")
```
### Python Comments using Strings

If we do not assign strings to any variable, they act as comments. For example, 

```python
"I am a single line comment"

'''
I am a
multi-line comment!
'''

print("Hello World")
```

> [!NOTE]
> **Note**: We use **triple quotation marks** for multi-line strings.
### Python Docstrings

As mentioned above, Python docstrings are strings used right after the definition of a function, method, class, or module (like in **Example 1**). They are used to document our code.

We can access these docstrings using the `__doc__` attribute.

---
## Python `__doc__` Attribute

Whenever string literals are present just after the definition of a function, module, class or method, they are associated with the object as their `__doc__` attribute. We can later use this attribute to retrieve this docstring.
### Example 2: Printing `docstring`

```python
def square(n):
	'''Take a number n and return the square of n.'''
	return n**2

print(square.__doc__)
```
#### Output

```
Take a number and return the square of n.
```

Here, the documentation of our `square` function can be accessed using the `__doc__` attribute.

---
Now, let's look at docstrings for the built-in function `print()`:
### Example 3: Docstrings for the Built-in `print()` Function

```python
print(print.__doc__)
```
#### Output

```
print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)

Prints the values to a stream, or to sys.stdout by default.
Optional keyword arguments:
file:  a file-like object (stream); defaults to the current sys.stdout.
sep:   string inserted between values, default a space.
end:   string appended after the last value, default a newline.
flush: whether to forcibly flush the stream.
```

Here, we can see that the documentation of the `print()` function is present as the `__doc__` attribute of this function.

---
## Single-line `docstrings` in Python

Single line docstrings are the documents that fit in one line.
### Standard Conventions to Write Single-line Docstrings:

- Even though they are single-lined, we still use the triple quotes around these docstrings as they can be expanded easily later.
- The closing quotes are on the same line as the opening quotes.
- There's no blank line either before or after the docstring.
- They should not be descriptive, rather they must follow "Do this, return that" structure ending with a period.

Let's take an example:
### Example 4: Write Single-line Docstrings for a Function

```python
def multiplier(a, b):
	"""Take two numbers and return their product."""
	return a*b
```
## Multi-line Docstrings in Python

Multi-line docstrings consist of a summary line just like a one-line docstring, followed by a blank like, followed by a more elaborate description.

The PEP 257 document provides the standard conventions to write multi-line docstrings for various objects. 

Some have been listed below:
## 1. Docstrings for Python Modules

- The docstrings for Python modules should list all the available classes, functions, objects and exception that are imported when the module is imported.
- They should also have a one-line summary for each item.

They are written at the beginning of the Python file.

Let's look at the docstrings for the builtin module in Python called `pickle`.
### Example 4: Docstrings of a Python Module

```python
import pickle
print(pickle.__doc__)
```

```
Create portable serialized representations of Python objects.

See module copyreg for a mechanism for registering custom picklers.
See module pickletools source for extensive comments.

Classes:

    Pickler
    Unpickler

Functions:

    dump(object, file)
    dumps(object) -> string
    load(file) -> object
    loads(string) -> object

Misc variables:

    __version__
    format_version
    compatible_formats
```

Here, we can see that the docstring written at the beginning of `pickle.py` module file can be accessed as its docstring.

---
## 2. Docstrings for Python Functions

- The docstring for a function or method should summarize its behavior and document its arguments and return values.
- It should also list all the exceptions that can be raised and other optional arguments.
### Example 5: Docstrings for Python Functions

```python
def add_binary(a, b):
	'''
	Return the sum of two decimal numbers in binary digits.

		Parameters:
			a (int): A decimal integer
			b (int): Another decimal integer

		Returns: 
			binary_sum(str): Binary string of the sum of a and b
	'''
	binary_sum = bin(a+b)[2:]
	return binary_sum

print(add_binary.__doc__)
```
#### Output

```
Returns the sum of two decimal numbers in binary digits.

	Parameters:
		a (int): A decimal integer
		b (int): Another decimal integer

	Returns:
		binary_sum (str): Binary string of the sum of a and b
```

As you can see, we have included a short description of what the function does, the parameter it takes in and the value it returns. The string literal is embedded to the function `add_binary` as its `__doc__` attribute.

---
## 3. Docstrings for Python Classes

- The docstrings for classes should summarize its behavior and list the public methods and instance variables.
- The subclasses, constructors, and methods should each have their own docstrings.
### Example 6: Docstrings for Python Class

Suppose we have a `Person.py` file with the following code:

```python
"""
A class to represent a person.

...

Attributes
----------
name : str
	first name of the person
surname : str
	family name of the person
age : int
	age of the person

Methods
-------
info(additional=""):
	prints the person's name and age.
"""

def __init__(self, name, surname, age):
	"""
	Constructs all necessary attributes for the person object.

	Parameters
	----------
		name : str
			first name of the person
		surname : str
			family name of the person
		age : int
			age of the person
	"""

	self.name = name
	self.surname = surname
	self.age = age

def info(self, additional=""):
	"""
	Prints the person's name and age.

	If the argument 'additional' is passed, then it is appended after the main  info.

	Parameters
	----------
	additional : str
		More info to be displayed (default is None)

	Returns
	-------
	None
	"""

	print(f'My name is {self.name} {self.surname}. I am {self.age} years old.' + additional)

```

Here, we can use the following code to access only the docstrings of the `Person` class:

```python
print(Person.__doc__)
```
#### Output:

```
    A class to represent a person.

    ...

    Attributes
    ----------
    name : str
        first name of the person
    surname : str
        family name of the person
    age : int
        age of the person

    Methods
    -------
    info(additional=""):
        Prints the person's name and age
```
## Using the `help()` Function for Docstrings

We can also the the `help()` function to read the docstrings associated with various objects.
### Example 7: Read Docstrings with the `help()` Function

We can use the `help()` function on the class `Person` in **Example 6** as:

```
help(Person)
```
#### Output

```
Help on class Person in module __main__:

class Person(builtins.object)
 |  Person(name, surname, age)
 |  
 |  A class to represent a person.
 |  
 |  ...
 |  
 |  Attributes
 |  ----------
 |  name : str
 |      first name of the person
 |  surname : str
 |      family name of the person
 |  age : int
 |      age of the person
 |  
 |  Methods
 |  -------
 |  info(additional=""):
 |      Prints the person's name and age.
 |  
 |  Methods defined here:
 |  
 |  __init__(self, name, surname, age)
 |      Constructs all the necessary attributes for the person object.
 |      
 |      Parameters
 |      ----------
 |          name : str
 |              first name of the person
 |          surname : str
 |              family name of the person
 |          age : int
 |              age of the person
 |  
 |  info(self, additional='')
 |      Prints the person's name and age.
 |      
 |      If the argument 'additional' is passed, then it is appended after the main info.
 |      
 |      Parameters
 |      ----------
 |      additional : str, optional
 |          More info to be displayed (default is None)
 |      
 |      Returns
 |      -------
 |      None
 |  
 |  ----------------------------------------------------------------------
 |  Data descriptors defined here:
 |  
 |  __dict__
 |      dictionary for instance variables (if defined)
 |  
 |  __weakref__
 |      list of weak references to the object (if defined)
```
## 4. Docstrings for Python Scripts

- The docstrings for Python script should document the script's functions and command-line syntax as a usable message.
- It should serve as a quick reference to all the functions and arguments.

---
## 5. Docstrings for Python Packages

The docstrings for a Python package is written in the packag'e `__init__.py` file.

- It should contain all the available modules and sub-packages exported by the package.
## Docstring Formats

We can write docstring in many formats like the reStructured text (reST) format, Google format or the NumPy documentation format. To learn more, visit [Popular Docstring Formats](https://stackoverflow.com/questions/3898572/what-is-the-standard-python-docstring-format)

We can also generate documentation from docstrings using tools like Sphinx. To learn more, visit [Official Sphinx Documentation](http://www.sphinx-doc.org/en/master/)

---
### Video: Python Docstrings

https://youtu.be/0YUdYk5E-w4?list=PL98qAXLA6aftqPGddFjJ59m71F96ZPwD4

