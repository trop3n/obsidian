---
up: "[[Python Concepts]]"
tags:
  - "#education/computerprogramming/languages/python/concepts/fundamentals"
prev: "[[Python Resources]]"
---

# Python Variables and Literals

In the previous tutorial you learned about [Python comments](https://www.programiz.com/python-programming/comments). Now, let's learn about variables and literals in Python.
## Python Variables

In programming, a **variable** is a container (or storage area) to hold data. For example, 

```
number = 10
```

Here, `number` is a variable storing the value **10**.

---
### Assigning Values to Variables in Python

As we can see from the above example, we use the assignment operator `=` to assign a value to a variable.

```python
# assign value to site_name variable
site_name = 'programiz.pro'

print(site_name)

# Output: programiz.pro
```
#### Output

```
programiz.pro
```

In the above example, we assigned the value `programiz.pro` to the `site_name` variable. Then, we printed out the value assigned to `site_name`.

> [!NOTE]
> Python is a ***type-inferred language***, so you don't have to explicitly define the variable type. It automatically knows that `programiz.pro` is a string and declares the `site_name` variable as a string. 
### Changing the Value of a Variable in Python

```python
site_name = 'programiz.pro'
print(site_name)

# assigning a new value to site_name
site_name = 'apple.com'

print(site_name)
```
#### Output

```
programiz.pro
apple.com
```

Here, the value of `site_name` is changed from `'programiz.pro'` to `'apple.com'`.

---
### Example: Assigning Multiple Values to Multiple Variables

```python
a, b, c = 5, 3.2, 'Hello'

print (a) # prints 5
print (b) # prints 3.2
print (c) # prints Hello
```

If we want to assign the same value to multiple variables at once, we can do this as:

```python
site1 = site2 = 'programiz.com'

print (x) # prints programiz.com
print (y) # prints programiz.com
```

We have assigned the same string value `'programiz.com'` to both the variables `site1` and `site2`.
### Rules for Naming Python Variables

1. Constant and variable names should have a combination of letters in lowercase (a - z) or uppercase (A to Z) or digits (0 to 9) or an underscore `(_)`. For example:

```
snake_case
MACRO_CASE
camelCase
CapWords
```

2. Create a name that makes sense. For example `vowel` makes more sense than `v`.
3. If you want to create a variable name having two words, use underscore to separate them. For example:

```
my_name
current_salary
```

4. Python is case-sensitive. So `num` and `Num` are different variables. For example:

```python
var num = 5
var Num = 55
print(num)      # 5
print(Num)      # 55
```

6. Avoid using [keywords](https://www.programiz.com/python-programming/keywords-identifier) like if, True, class, etc. as variable names.
## Python Literals

Literals are representations of fixed values in a program. They can be numbers, characters, or strings, etc. For example, `'Hello, World!'`, `12`, `23.0`, `'C'`, etc.

Literals are often used to assign values to variables or constants. For example,

```python
site_name = 'programiz.com'
```

In the above expression, `site_name` is a variable, and `'programiz.com'` is a literal.

There are different types of literals in Python. Let's discuss some of the commonly used types in detail.

---
## Python Numerical Literals

Numeric literals are **immutable** (unchangeable). Numeric literals can belong to `3` different numerical types: `Integer`, `Float` and `Complex`.
### 1. Integer Literals

Integer literals are numbers without decimal parts. It also consists of negative numbers. For example, `5`, `-11`, `0`, `12`, etc.
### 2. Floating-Point Literals

Floating-point literals are numbers that contain decimal parts.

Just like integers, floating-point numbers can also be both positive and negative. For example, `2.5`, `6.76`, `0.0`, `-9.45`, etc.
### 3. Complex Literals

Complex literals are numbers that represent complex numbers. Here, numerals are in the form `a + bj`, where `a` is real and `b` is imaginary. For example, `6+9j`, `2+3j`.

---
## Python String Literals

In Python, texts wrapped inside quotation marks are called **string literals**.

```python
"This is a string."
```

We can also use single quotes to create strings. 

```python
'This is also a string.'
```
# More on Python Literals

### Python Boolean Literals

There are two boolean literals: `True` and `False`.

For example, 

```python
is_pass = True
print(is_pass)

# Output: True
```

Here, `True` is a boolean literal assigned to `is_pass`.
### Character Literals in Python

Character literals are **unicode characters** enclosed in a quote. For example,

```python
some_character = 'S'
```

Here, `S` is a character literal assigned to `some_character`.
### Special Literal in Python

Python contains one special literal `None`. We use it to specify a null variable. For example, 

```python
value = None

print(value)

# Output: None
```

We get `None` as an output as the `value` variable has no value assigned to it.
### Collection Literals

Let's see examples of four different collection literals. List, Tuple, Dict and Set literals.

```python
# list literal
fruits = ["apple", "mango", "orange"]
print(fruits)

# tuple literal
numbers = (1, 2, 3)
print(numbers)

# dictionary literal
alphabets = {'a':'apple', 'b':'ball', 'c':'cat'}
print(alphabets)

# set literal
vowels = {'a', 'e', 'i', 'o', 'u'}
print(vowels)
```
#### Output

```python
['apple', 'mango', 'orange']
(1, 2, 3)
{'a': 'apple', 'b': 'ball', 'c': 'cat'}
{'e', 'a', 'o', 'i', 'u'}
```

In the above example, we created a list of `fruits`, a tuple of `numbers`, a dictionary of `alphabets` having values with keys designated to each value and a set of `vowels`.

To learn more about literal collections, refer to [Python Data Types](https://www.programiz.com/python-programming/variables-datatypes).
## Video: Python Variables and print()

https://youtu.be/i83VkP0LHPI?list=PL98qAXLA6afuh50qD2MdAj3ofYjZR_Phn
# Python Type Conversion

In programming, type conversion is the *process of converting data of one type to another.* For example: converting `int` data to `str`.

There are two types of type conversion in Python.

- Implicit Conversion - automatic type conversion
- Explicit Conversion - manual type conversion

---
## Python Implicit Type Conversion

In certain situations, Python automatically converts one [data type](https://www.programiz.com/python-programming/variables-datatypes) to another. This is known as implicit type conversion.

---
### Example 1: Converting Integer to Float

Let's see an example where Python promotes the conversion of the lower data type (integer) to the higher data type (float) to avoid data loss.

```python
integer_number = 123
float_number = 1.23

new_number = integer_number + float_number

# display new value and resulting data type
print("Value:", new_number)
print("Data Type:", type(new_number))
```
#### Output

```
Value: 124.23
Data Type: <class 'float'>
```

In the above example, we have created two variables: `integer_number` and `float_number` of `int` and `float` type respectively.

Then we added these two variables and stored the result in `new_number`.

As we can see `new_number` has value **124.23** and is of the `float` data type.

It is because Python *always converts* smaller data types into larger data types to avoid the loss of data.

> [!NOTE]
> - We get `TypeError`, if we try to add `str` and `int`. For example, `'12' + 23`. Python is not able to use Implicit Conversion in such conditions.
> - Python has a solution for these types of situations which is known as ***Explicit Conversion***.
## Explicit Type Conversion

In Explicit Type Conversion, users convert the data type of an object to the required data type. We use the built-in functions like `int()`, `float()` and `str()` to perform explicit type conversion. This type of conversion is also called ***typecasting*** because the user **casts** (changes) the data type of the objects.

---
### Example 2: Addition of String and Integer using Explicit Type Conversion

```python
num_string = '12'
num_integer = 23

print("Data type of num_string before Type Casting:", type(num_string))

# explicit type conversion
num_string = int(num_string)

print("Data type of num_string after Type Casting:", type(num_string))

num_sum = num_integer + num_string

print("Sum:", num_sum)
print("Data type of num_sum:", type(num_sum))
```
#### Output

```
Data type of num_string before Type Casting: <class 'str'>
Data type of num_string after Type Casting: <class 'int'>
Sum: 35
Data type of num_sum: <class 'int'>
```

In the above example, we have created two variables: `num_string` and `num_integer` with `str` and `int` type values respectively. Notice the code:

```
num_string = int(num_string)
```

Here, we have used `int()` to perform explicit type conversion of `num_string` to integer type.
After converting `num_string` to an integer value, Python is able to add these two variables.
Finally, we go the `num_sum` value i.e. **35** and data type to be `int`.

---
## Key Points to Remember

1. Type Conversion is the conversion of an object from one data type to another data type.
2. Implicit Type Conversion is automatically performed by the Python Interpreter.
3. Python avoids the loss of data in Implicit Type Conversion.
4. Explicit Type Conversion is also called Type Casting, the data types of objects are converted using predefined functions by the user.
5. In Type Casting, loss of data may occur as we enforce the object to a specific data type.

**Also Read:**

- [Python Numbers, Type Conversion and Mathematics](https://www.programiz.com/python-programming/numbers)
# Python Basic I/O
## Python Output

In Python, we can simply use the `print()` function to print output. For example:

```
print('Python is powerful')

# Output: Python is Powerful
```

Here, `print()` function displays the string enclosed inside the single quotation.
### Syntax of `print()`

The `print()` function is taking a single parameter above. However, the actual syntax of the print function accepts 5 parameters:

```python
print(object= separator= end= file= flush=)
```

Here:

- **object** - value(s) to be printed
- **sep** (optional) - allows us to separate multiple **objects** inside `print()`.
- **end** (optional) - allows us to add specific values like new line `"\n"`, tab `"\t"`.
- **file** (optional) - where the values are printed. It's default value is `sys.stdout` (screen)
- **flush** (optional) - boolean specifying if the output is flushed or buffered.

---
### Example 1: Python Print Statement

```python
print('Good Morning!')
print('It is rainy today')
```
#### Output

```
Good Morning!
It is rainy today
```

In the above example, the `print()` statement only includes the **object** to be printed. Here, the value for **end** is not used. Hence, it takes the default value `'\n'`.

So we get the output in two different lines.

---
### Example 2: Python `print()` with end Parameter

```python
# print with end whitespace
print('Good Morning!', end= ' ')

print('It is rainy today')
```
#### Output

```
Good Morning! It is rainy today
```

Notice that we have included the `end= ' '` after the end of the first `print()` statement.

Hence, we get the output in a single line separated by space.
### Example 3: Python `print()` with Sep Parameter

```python
print('New Year', 2023, 'See you soon!', sep= '. ')
```
#### Output

```
New Year. 2023. See you soon!
```


