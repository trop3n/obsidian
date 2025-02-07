#python #codecademy #practicesession 

# Control Flow

## Else Statement

```python
# else statement

test_value = 50

if test_value < 1:
	print("Value is < 1")
else:
	print("Value is >= 1")

test_string = "VALID"

if test_string == "NOT_VALID":
	print("String equals NOT_VALID")
else:
	print("String equals something else!")
```

The Python `else` statement provides alternative code to execute if the expression in an `if` statement evaluates to `False`. 

The indended code for the `if` statement is executed if the expression evaluates to `True`. The intended code immediately following the `else` is executed *only if the expression evaluates to `false`*. 

To make the end of the `else` block, the code must be unindented to the same level as the starting `if` line.
## Comparison Operators

```python
a = 2
b = 3
a < b # True
a > b # False
a >= b # False
a <= b # True
a <= a # True
```

In Python, *relational operators* compare two values or expressions. The most common ones are:

- `<` less than
- `>` greater than
- `<=` less than or equal to
- `>=` greater than or equal to

If the relation is sound, then the entire expression will evaluate to `True`. If not, the expression evaluates to `False`.

## Equal Operator

```python
if 'Yes' == 'Yes':
	# evaluates to True
    print('They are equal')

if (2 > 1) == (5 < 10):
	# evaluates to True
	print('Both expressions give the same result')

c = '2'
d = 2

if c == d:
	print('They are equal')
else:
	print('They are not equal')
```

The equal operator `==` is used to *compare two values*, variables or expressions to determine if they are the same. 

If the values being compared are the same, the operator returns `True`, otherwise it returns `False`.

The operator takes the data type into account when making the comparison, so a string value of `"2"` is *not* considered the same as a numeric value of `2`.

## SyntaxError

```python
age = 7 + 5 = 4

File "<stdin>", line 1
SyntaxError: can't assign an operator
```

A `SyntaxError` is reported by the Python interpreter when some portion of the code is incorrect. This can include misspelled keywords, missing or too many brackets or parentheses, incorrect operators, missing or too many quotation marks, or other conditions.
## `and` Operator

```python
True and True    # evaluates to True
True and False   # evaluates to False
False and False  # evaluates to False
1 == 1 and 1 < 2 # evaluates to True
1 < 2 and 3 > 1  # evaluates to False
"Yes" and 100    # evaluates to True
```

The Python `and` operator performs a **Boolean Comparison** between two Boolean values, variables or expressions. If both sides of the operator evaluate to `True`, then the `and` operator returns `True`. If either side (or both sides) evaluates to `False`, then the `and` operator returns `False`. A non-Boolean value (or variable that stores a value) will always evaluate to `True` when used with the `and` operator.

# Classes Practice Session

## Python Class Methods

```python
# Dog class
class Dog:
	# Method of the class
	def bark(self):
		print("Ham-Ham")

# Create a new instance
charlie = Dog()

# Call the method
charlie.bark()
# This will output "Ham-Ham"
```

In Python, *methods* are functions that are defined as part of a class. It is common practice that the first argument of any method that is part of a class is the actual object calling the method. This argument is usually called a `self`.
## Python Class Variables

```python
class my_class:
	class_variable = "I am a Class Variable!"

x = my_class()
y = my_class()

print(x.class_variable) # I am a Class Variable!
print(y.class_variable) # I am a Class Variable!
```

In Python, class variables are defined outside of all methods and have the same value for every instance of the class. 

Class variables are accessed with the `instance.variable` or `class_name.variable` syntaxes.
## Instantiate Python Class

```python
class Car:
	"This is an empty class"
	pass

# Class Instantiation
ferrari = Car()
```

In Python, a class needs to be instantiated before use. 

As an analogy, a class can be thought of as a blueprint (Car), and an instance is an actual implementation of the blueprint (Ferrari). 
## Python init Method

```python
class Animal:
	def __ini__(self, voice):
		self.voice = voice

# When a class instance is created, the instance variable
# 'voice' is created and set to the input value.
cat = Animal('Meow')
print(cat.voice) # Output: Meow

dog = Animal('Woof')
print(dog.voice) # Output: Woof
```

In Python, the `.__init__()` method is used to initialize a newly created object. It is called every time the class is instantiated. 
## Python `dir()` Function

```python
class Employee:
	def __init__(self, name):
		self.name = name

	def print_name(self):
		print("Hi, I'm " + self.name)

print(dir())
# ['Employee', '__builtins__', '__doc__', '__file__', '__name__', '__package__', 'new_employee']

print(dir(Employee))# ['__doc__', '__init__', '__module__', 'print_name']
```

In Python, the built-in `dir()` function, without any argument, returns a list of all the attributes in the current scope. 

With an object as argument, `dir()` tries to return all valid object attributes.
## Python Class

```python
class Animal:
	def __init__(self, name, number_of_legs):
		self.name = name
		self.number_of_legs = number_of_legs
```

In Python, a class is a template for a data type. A class can be defined using the `class` keyword.
## `__main__` in Python

In Python, `__main__` is an identifier used to reference the current file context. When a module is read from standard input, a script, or from an interactive prompt, its `__name__` is set equal to `__main__`.

# Lists

## List Slicing

```python
tools = ['pen', 'hammer', 'lever']
tools_slice = tools[1:3] # ['hammer', 'lever']
tools_slice[0] = 'nail'

# original list is unaltered:
print(tools) # ['pen', 'hammer', 'lever']
```

A *slice* or sub-list of Python list elements can be selected from a list using a colon-separated starting and ending point.

The syntax pattern is `myList[START_NUMBER:END_NUMBER]`. The slice will include the `START_NUMBER` index, and everything until but *excluding* the `END_NUMBER` item.

When slicing a list, a new list is returned, so if the slice is saved and then altered, the original list remains the same.
## List Method `.sort()`

```python
exampleList = [4, 2, 1, 3]
exampleList.sort()
print(exampleList)
# [1, 2, 3, 4]
```

The `.sort()` Python list method will sort the contents of whatever list it is called on. Numerical lists will be sorted in ascending order, and lists of Strings will be sorted into alphabetical order. It modifies the original list, and has no return value.

## List Method `.pop()`



