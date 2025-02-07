---
up: "[[000 - Education/Computer Programming/Languages/Python/Python|Python]]"
tags:
  - "#education/computerprogramming/languages/python/automate"
source: "[[Automate the Boring Stuff - NSP.pdf]]"
---

# Chapter 1. Python Basics

```python
>>> 2 + 2
4
```

$2 + 2$ is called an **expression** in Python, the most basic kind of programming instruction int he language.

- Expressions consist of **values** and **operators**
- They can always reduce down to a single value, or **evaluate**.

| Operator | Operation                         | Examples  | Evaluation |
| -------- | --------------------------------- | --------- | ---------- |
| `**`     | Exponent                          | $2 ** 3$  | 8          |
| `%`      | Modulus/Remainder                 | 22 % 8    | 6          |
| `//`     | Integer Division/Floored Quotient | $22 // 8$ | 2          |
| `/`      | Division                          | $22 / 8$  | 2.75       |
| `*`      | Multiplication                    | $3 * 5$   | 15         |
| `-`      | Subraction                        | $5 - 2$   | 3          |
| `+`      | Addition                          | 2 + 2     | 4          |
The *order of operations* (also known as *precedence*) of Python math operations is similar to that of mathematics. 

- The `**` operator is evaluated first
- `*`,`/`, `//` and `%` are evaluated second
- `+` and `-` are evaluated next
- All operators are evaluated from left to right

Parenthesis can override the precedence if needed. Whitespace in between the operators doesn't matter for Python, but a *single space is convention*.
## The Integer, Floating-Point, and String Data Types

Remember that expressions are just values combined with operators, and they always evaluate down to a single value. 

A *data type* is a category for values, and every value belongs to **exactly one data type**.

| Data Type              | Example                                |
| ---------------------- | -------------------------------------- |
| Integers               | -2, -1, 0, 1, 2, 3, 4, 5               |
| Floating-point numbers | -1.25, -1.0, -0.5, 0.0, 0.5, 1.0, 1.25 |
| Strings                | 'a', 'aa', 'aaa', "Hello!", '11 cats'  |
Python also has text values called ***strings***, or ***strs*** (pronounced stirs).

You can have string with no characters in it, `''`, called a *blank string* or *empty string*.

```python
>>> 'Hello, world! 
SyntaxError: EOL while scanning string literal
```
> This output means that the closing quote mark was forgotten.
## String Concatenation and Replication

The meaning of an operator may change based on the data types of the values next to it. For example, `+` is the addition operator when it operates on two integers or floating point values. 

However, when `+` is used on two string values, it joins the strings as the *string concatenation* operator. 

```python
>>> 'Alice' + 'Bob' 
'AliceBob'
```
> The expression evaluates down to a single, new string value that combines the text of the two strings. 

Python will not know how to handle adding a string to an integer value, and will display an error message.

```python
>>> 'Alice' + 42 
Traceback (most recent call last): 
  File "<pyshell#0>", line 1, in <module> 
    'Alice' + 42 
TypeError: can only concatenate str (not "int") to str
```

The error message `can only concatenate str (not "int") to str` means that Python though you were trying to concatenate an integer to the string `'Alice'`. Your code will explicitly convert the integer to a string because Python cannot do this automatically. 

The `*` operator multiplies two integer or floats. But the `*` operator is used on one string and one integer, resulting in a *string replication* operator. 

```
>>> 'Alice' * 5 
>>> 'AliceAliceAliceAliceAlice'
```

The expression evaluates down to a single string value that repeats the original string a number of times equal to the integer value. String replication is a useful trick, but it's not as often used as *string concatenation*. 
## Storing Values in Variables

A ***variable*** is like a box in the computer's memory where you can store a single value. If you want to use the result of an evaluated expression later in our program, we can save it inside a variable.
### Assignment Statements

Variables store values via ***assignment statements***. 

- It consists of a variable name, and equal sign (*assignment operator*), and the value to be stored. 
- If you enter the assignment statement `spam = 42`, then a variable named spam will have the integer value `42` stored in it.

```python
>>> spam = 40
>>> spam
40
>>> eggs = 2
>>> spam + eggs
42
>>> spam + eggs + spam
82
>>> spam = spam + 2
>>> spam
42
```

A variable is *initialized* (created) the first time a value is stored in it. After that, you can use it in expressions with other variables and values. When a variable is assigned a new value, the old value is forgotten, which is why `spam` evaluated to 42 instead of 40 at the end of the example. 

-  This is an called ***overwriting the string***.

```python
>>> spam = 'Hello'
>>> spam
'Hello'
>>> spam = 'Goodbye'
>>> spam
'Goodbye
```
### Variable Names

A good variable name describes the data it contains. Imagine you packed all your things up and labeled each box "stuff". A descriptive name will help make your code more *readable*.

Python has some naming restrictions:

- It can only be one word with no spaces.
- It can use only letters, numbers, and the underscore `_` character
- It can't begin with a number

| Valid Variable Names | Invalid Variable Names                           |
| -------------------- | ------------------------------------------------ |
| `current_balance`    | `current-balance` (hyphens are not allowed)      |
| `currentBalance`     | `current balance` (spaces are not allowed)       |
| `account4`           | `4account` (can't begin with a number)           |
| `_42`                | `42` (can't begin with a number)                 |
| `TOTAL_SUM`          | `TOTAL_$UM` (special characters are not allowed) |
| `hello`              | `'hello'` (special characters are not allowed)   |
Variable names are **case-sensitive**, meaning that `spam`, `SPAM`, `Spam` and `sPaM` are four different variables. 

This book uses *camelcase* for variable names instead of underscores; that is, variables `lookLikeThis` instead of `looking_like_this`. The Python code style guide, PEP 8, says that underscores should be used. This is personal preference ultimately. 

> [!NOTE] A Foolish Consistency is the Hobgoblin of Little Minds
> Consistency with the style guide is important. But most impor- tantly: know when to be inconsistent—sometimes the style guide just doesn’t apply. When in doubt, use your best judgment.
## Your First Program

While the interactive shell is good for running Python instructions one at a time, to write entire Python programs, you'll type the instructions into the file editor. A *file editor* is similar to text editors such as Notepad or TextMate, but it has some features specifically for entering source code. 

- The interactive shell window will always be the one with the >>> prompt. 
- The file editor window will not have the >>> prompt.

```python
print('Hello, world!')
print('What is your name?')
myName = input()
print('It is good to meet you, ' + myName)
print('The length of your name is: ')
print(len(myName))
print('What is your age?')
myAge = input()
print('You will be ' + str(int(myAge) + 1) + ' in a year.')
```

The output from your program should look like this:

```
Hello, world!
What is your name?
Jason
It is good to meet you, Jason
The length of your name is: 
5
What is your age?
33
You will be 34 in a year.
```

When there are no more lines of code to execute, the Python program *terminates*, or stops running. 
## Dissecting Your Program

With the new program open in the file editor, let's take a quick tour of the Python instructions it uses by looking at each line of code.
### Comments

The first line is a *comment*. Python ignores comments, and you can use them to write notes or remind yourself what the code is trying to do. Anything following a hash mark `#` will be treated as a comment.

***Commenting Out***: placing a `#` in front of a piece of code to prevent it from running.

Python also ignores the blank line after the comment. You can add many blank lines to your program as you want.
### The `print()` Function

The `print()` function displays the string value inside it's parenthesis on the screen.

```python
print('Hello, world!')
print('What is your name?') # ask for their name.
```

> [!NOTE]
> You can also use this function to put a blank line on the screen; just call print() with nothing in between the parentheses

When you write a function name, the opening and closing parenthesis at the end identify it as the name of a function. This is why in this book you'll see `print()` rather than `print`. Chapter 3 describes functions in more detail.
### The `input()` Function

The `input()` function waits for the user to type some text on the keyboard and press `ENTER`.

```python
myName = input()
```

This function call evaluates to a string equal to the user's text, and the line of code assigns the `myName` variable to this string value.

You can think of the `input()` function call as an expression that evaluates to whatever string the user typed in. If the user entered `'Al'`, then the expression would evaluate to `myName = 'Al`.
### Printing the User's Name

```python
print('It is good to meet you, ' + myName)
```

Remember expressions can *always evaluate to a single value*.
### The `len()` Function

You can pass the `len()` function a string value (or a variable containing a string), and the function evaluates to the integer value of the number of characters in that string.

```python
print('The length of your name is:')
print(len(myName))
```

Enter the following in the interactive shell to try this:

```python
>>> len('hello')
5
>>> len('My very energetic monster just scarfed nachos.')
46
>>> len('')
0
>>>
```

 The print() function allows you to pass it either integer values or string values, but notice the error that shows up when you type the following into the interactive shell:

```
>>> print('I am ' + 29 + ' years old.') 
Traceback (most recent call last): 
  File "<pyshell#6>", line 1, in <module> 
    print('I am ' + 29 + ' years old.') 
TypeError: can only concatenate str (not "int") to st
```

Python gives an error because the `+` operator can only be used to add two integers together or concatenate two strings.
	You can't add an integer to a string.
### The `str()`, `int()` and `float()` Functions

If you want to concatenate an integer such as `29` with a string to pass to `print()`, you'll need to get the value `'29'` which is the string form of `29`. The `str()` function can be passed an integer value and will evaluate to a string value of the integer, as follows:

```python
>>> str(29)
# '29'
>>> print('I am ' + str(29) + ' years old.)
# I am 29 years old.
```

Because `str(29)` evaluates to `'29'`, the expression `'I am ' + str(29) + ' years old.'` evaluates to `'I am ' + '29' + ' years old.'`, which in turn evaluates to `'I am 29 years old.'`. This is the value that is passed to the `print()` function. The `str(), int(), and float()` functions will evaluate to the string, integer, and floating-point forms of the value you pass, respectively. Try converting some values in the interactive shell with these functions and watch what happens.

```python
>>> int('-99')
-99
>>> int(1.25)
1
>>> int(1.99)
1
>>> float('3.14')
3.14
>>> float(10)
10.0
```

The `str()` function is handy when you have an integer or float that you want to concatenate into a string. The `int()` function is also helpful if you have a number as a string value that you want to use in some mathematics. 

For example, the `input()` function always returns a string, even if the user enters a number. 

```python
>>> spam = input()
101
>>> spam
'101'
```

The value stored inside `spam` isn't the integer `101` but the string `'101'`. We can use the `int()` function to get the integer form of `spam` and then store this as the new value in `spam`.

```python
>>> spam = int(spam)
>>> spam
101
```

Now the `spam` variable can be treated as an integer instead of a string.

```python
>>> spam * 10 / 5
202.0
```

The `int()` function is useful if you need to round a floating point number down.

```python
>>> int(7.7)
7
>>> int(7.7) + 1
8
```

We used the `int()` and `str()` functions in the last three lines of our program to get a value of the appropriate data type for the code.

```python
print('What is your age?')
myAge = input()
print('You will be ' + str(int(myAge) + 1) + ' in a year.')
```

> [!NOTE] Text and Number Equivalence
> Although the string value of a number is considered a completely different value from the integer or floating-point version, an integer can be equal to a floating point.
> ``` 
> >>> 42 == '42'
> False
> >>> 42 == 42.0
> True
> >>> 42.0 == 0042.000
> True
> ```
> Python makes this distinction because strings are text, while integers and floats are both numbers.
## Summary

Expression, and their component values, operators, variables, and function calls -- are the basic building blocks that make programs. Once you know how to handle these elements, you will be able to instruct your Python to operate on large amounts of data for you. 

In the next chapter, you’ll learn how to tell Python to make intelligent decisions about what code to run, what code to skip, and what code to repeat based on the values it has. This is known as flow control, and it allows you to write programs that make intelligent decisions.
## Practice Questions

1. Which of the following are operators and which are values?

```python
*              # operator
'hello'        # value
-88.8          # value
-              # operator
/              # operator
+              # operator
5              # value
```

2. Which of the following is a variable, and which is a string?

```python
spam           # variable
'spam'         # string
```

3. Name 3 data types.
	Strings, floats, booleans, integers.

4. What is an expression made up of? What do all expression do?
	All expressions evaluate. They are made up of values and operators that conduct mathematical operations on said values.

5. This chapter introduced assginment statements, like `spam = 10`. What is the difference between an expression and a statement?
	An expression evaluates two values and performs mathematical operations, a statement *declares* the state of a value.

6. What does the variable `bacon` contain after the following code runs?

```python
bacon = 20
bacon + 1
# bacon = 21
```

7. What should the following two expressions evaluate to?

```python
'spam' + 'spamspam'
'spam' * 3

# 'spamspamspam'
```

8. Why is `eggs` a valid variable name while `100` is invalid?
	Variables cannot start with numbers.

9. What three functions can be used to get the integer, floating-point number, or string version of a value?
	`str()`, `int()`, `float()`

10. Why does this expression cause an error? How can you fix it?
	Strings cannot be concatenated to integers. 
	
```python
'I have eaten ' + 99 + ' burritos.'

'I have eaten ' + str(99) + ' burritos.'
```

> [!exercise]
> Extra credit: Search online for the Python documentation for the len() function. It will be on a web page titled “Built-in Functions.” Skim the list of other functions Python has, look up what the round() function does, and experiment with it in the interactive shell
# Chapter 2: Flow Control

Programming's real strength isn't just running one instruction after another like a weekend errand list. Based on how expressions evaluate, a program can decide to skip instructions, repeat them, or choose on of several instructions to run. In fact, you almost never want your programs to start from the first line of code an simply execute every time, straight to the end. 

*Flow control statements* can decide which Python instructions to execute under which conditions.

These flow control statements directly correspond to the symbols in a flowchart, so I'll provide flowcharts for what to do if it's raining.

![](https://i.imgur.com/mJNultI.png)

In a flowchart, there are usually multiple ways to go from the start to the end. The same is true for *lines of code in a computer program*. 

Before you learn about flow control statements, you need to learn how to represent those *yes* and *no* options, and you need to understand how to write those branching points as Python code. 
## Boolean Values

While the integer, floating-point and string data types have an *unlimited* number of possible values, the *Boolean* data type has only two values: `True` and `False`. (Boolean is capitalized because the data type is named after mathematician George Boole). When entered as Python code, the Boolean values `True` and `False` lack the quotes you place around strings, and they always start with a capital T or F, with the rest of the word in lowercase. 

```Python
>>> spam = True
>>> spam
True
>>> true
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'true' is not defined. Did you mean: 'True'?
>>> True = 2 + 2
  File "<stdin>", line 1
    True = 2 + 2
    ^^^^
SyntaxError: cannot assign to True
```

1. Boolean values are used in expressions and can be stored in variables. 
2. If you don't *use the proper case*
3. Or you try to use `True` and `False` for variable names

Python will give you an error message for numbers 2 and 3.
## Comparison Operators

*Comparison Operators* also called *relational operators*, compare two values and evaluate down to a single Boolean value. Table 2-1 lists the comparison operators:

| Operator | Meaning                  |
| -------- | ------------------------ |
| `==`     | Equal to                 |
| `!=`     | Not equal to             |
| `<`      | Less than                |
| `>`      | Greater than             |
| `<=`     | Less than or equal to    |
| `>=`     | Greater than or equal to |
These operators **evaluate to `True` or `False`** depending on the values you give them. 

```Python
>>> 42 == 42
True
>>> 42 == 99
False
>>> 2 != 3
True
>>> 2 != 2
False
```

As you might expect, `==` (equal to) evaluates to `True` when the values on both sides are the same, and `!=` (not equal to) evaluates to `True` when the two values are different. The `==` and `!=` operators can actually work with **values of *any* data type**.

```python
>>> 'hello' == 'hello'
True
>>> 'hello' == 'Hello'
False
>>> 'dog' != 'cat'
True
>>> True == True
True
>>> True != False
True
>>> 42 == 42.0
True
>>> 42 == '42'
False
```

Note that an integer or floating point value will always be unequal to a string value. 

The `<`, `>`, `<=`, and `>=` operators on the other hand work properly only with integer and floating point values.

```python
>>> 42 < 100
True
>>> 42 > 100
False
>>> 42 > 42
False
>>> eggCount = 42
>>> eggCount <= 42
True
>>> myAge = 32
>>> myAge >= 10
True
```

> [!NOTE] The Difference Between the `==` and `=` Operators
> You might have noticed that the `==` operator has two equals signs, while the `=` operator only has one. It's easy to confuse these two operators with each other. Just remember these points:
> - The `==` operator asks *whether two values are the same as each other*.
> - The `=` operator puts the value on the right into the variable on the left. 
>   
>   To help remember which is which, notice that the `==` operator (equal to) consists of two characters, just like the `!=` operator consists of two characters.

You will often use comparison operators to compare a variable's value to some other value, like in the `eggCount <= 42` and `myAge >= 10` examples. 
## Boolean Operators

The three **Boolean Operators** (`and`, `or` and `not`) are used to compare Boolean values. Like comparison operators, they evaluate these expressions down to a Boolean value. 
### Binary Boolean Operators

The `and` and `or` operators always take two Boolean values (or expressions), so they're considered *binary* operators. The `and` operator evaluates an expression to `True` if *both* Boolean values are `True`; otherwise it evaluates to `False`. Enter some expressions using `and` into the interactive shell to see it in action.

```python
>>> True and True
True
>>> True and False
False
```

A *truth table* shows every possible result of a Boolean operator. 

| Expression      | Evaluates to... |
| --------------- | --------------- |
| `True and True`   | `True`            |
| `True and False`  | `False`           |
| `False and False` | `False`           |
| `False and True`  | `False`           |
On the other hand, the `or` operator evaluates an expression to `True` if *either* of the two Boolean values is `True`. If both are `False`, it evaluates to `False`.

```python
>>> False or True
True
>>> False or False
False
```

| Expression     | Evaluates to... |
| -------------- | --------------- |
| True or True   | True            |
| True or False  | True            |
| False or True  | True            |
| False or False | False           |
### The `not` Operator

Unlike `and` and `or`, the `not` operator operates on only one Boolean value (or expression). This makes it a *unary* operator. The `not` operator simply evaluates to the **opposite Boolean** **value**.

```python
>>> not True
False
>>> not not not not True
True
```

Much like *double negatives* in speech and writing, you can nest `not` operators, though there's never not no reason to do this in real programs. 

| Expression  | Evaluates to... |
| ----------- | --------------- |
| `not True`  | `False`         |
| `not False` | `True`          |
## Mixing Boolean and Comparison Operators

Since the comparison operators evaluate to Boolean values, you can use them in expressions with the Boolean operators. 

Recall that the `and`, `or` and `not` operators are called Boolean operators because they always operate on the Boolean values `True` and `False`. While expressions like `4 < 5` aren't Boolean values, they are expressions that evaluate down to Boolean values. 

```python
>>> (4 < 5) and (5 < 6)
True
>>> (4 < 5) and (9 < 6)
False
>>> (1 == 2) and (2 == 2)
False
>>> (1 == 2) or (2 == 2)
True
```

The computer will evaluate the left expression first, and then it will evaluate the right expression. When it knows the Boolean value for each, it will then evaluate the whole expression down to one Boolean value. 

You can also use multiple Boolean operators in an expression, along with the comparison operators:

```python
>>> 2 + 2 == 4 and not 2 + 2 == 5 and 2 * 2 == 2 + 2
True
```

The Boolean operators have an *order of operations* just like the math operators do. After many math and comparison operators evaluate, Python evaluates the `not` operators first, then the `and` operators, and then the `or` operators.
## Elements of Flow Control

Flow control statements often start with a part called the *condition* and are always followed by a block of code called the *clause*. Before you learn about Python's specific flow control statements, we will cover what a condition and a block are. 
### Conditions

The Boolean expressions you've seen so far could all be considered **conditions**, which are the same thing as expressions; *conditions* is just a more specific name in the context of flow control statements. 

Conditions always evaluate down to a Boolean value, `True` or `False`. A flow control statement decides what to do based on whether its condition is `True` or `False`, and almost every flow control statement uses a condition.
### Blocks of Code

Lines of Python can be grouped together in ***blocks***. You can tell when a block begins and ends from the indentation of the lines of code. There are three rules for blocks.

- Blocks begin when the indentation increases.
- Blocks can contain other blocks.
- Blocks end when the indentation decreases to zero or to a containing block's indentation.

Blocks are easier to understand by looking at some indented code, so let's find the blocks in part of a small game program, shown here:

```python
name = 'Mary'
password = 'swordfish'
if name == 'Mary':
    print('Hello, Mary')
    if password == 'swordfish':
	    print('Access Granted')
	else:
		print('Wrong password.')
```
## Program Execution

***Program Execution*** (or simply, `execution`) is a term for the current instruction being executed. If you print the source code on paper and put your finger on each line as it is executed, you can think of your finger as the program execution.

Not all programs execute by simply going straight down, however, If you use your finger to trace through a program with flow control statements, you'll likely find yourself jumping around the source code based on conditions, and you'll probably skip entire clauses. 
## Flow Control Statements

Now, let's explore the most important piece of flow control: the statements themselves.
### if Statements

The most common type of flow control statement is the `if` statement. An `if` statement's clause, (that is, the block following the `if` statement) will execute if the statement's condition is `True`. The clause is skipped if the condition is `False`. In plain English, an `if` statement could be read as "If this condition is true, execute the code in the clause". 

In Python, an `if` statement consists of the following:

- The `if` keyword
- A condition (an expression evaluating to `True` or `False`)
- A colon
- Starting on the next line, an indented block of code (called the `if` clause).

```python
if name == 'Alice':
	print('Hi, Alice.')
```

![](https://i.imgur.com/Yj22XxD.png)
### else Statements

An `if` clause can *optionally* be followed by an `else` statement. The `else` statement clause is executed only when the `if` statement's condition is `False`. 

In plain English, an `else` statement could be read as "If this condition is true, execute this code. Or else, execute that code." An else statement doesn't have a condition, and in code, an `else` statement always consists of the following:

- The `else` keyword
- A colon
- Starting on the next line, an indented block of code (called the `else` clause)

```python
if name == 'Alice':
	print('Hi, Alice')
else:
	print('Hello, stranger.')
```

![](https://i.imgur.com/Cp9FG3t.png)
### elif Statements

While only one of the `if` or `else` clauses will execute, you may have a case where you want one of *many* possible clauses to execute. The `elif` statement is an "else if" statement that always follows an `if` or another `elif` statement. It provides another condition that is checked only if all of the previous conditions were `False`. In code, an `elif` statement always consists of the following:

- The `elif` keyword
- A condition (expression evaluating to `True` or `False`)
- A colon
- Starting on the next line, an indented block of code (called the `elif` clause)

```python
if name == 'Alice':
	print('Hi, Alice')
elif age < 12:
	print('You are not Alice, kiddo.')
```

![](https://i.imgur.com/0QcflqN.png)

The `elif` clause executes if `ace < 12` is `True` and `name == 'Alice'` is `False`. However, if both conditions are `False`, then both of the clauses are skipped. It is *not* guaranteed that at least one of the clauses will be executed. 

When there is a chain of `elif` statements, only one or none of the clauses will be executed. Once one of the statements' conditions is found to be `True`, the rest of the `elif` clauses are automatically skipped.
	For example, open a new file editor window and enter the following code, saving it as *vampire.py*:

```python
name = 'Carol'
age = 3000
if name == 'Alice':
    print('Hi, Alice.')
elif age < 12:
    print('You are not Alice, kiddo.')
elif age > 2000:
    print('Unlike you, Alice is not an undead, immortal vampire.')
elif age > 100:
    print('You are not Alice, grannie')
```

![](https://i.imgur.com/usEYwgf.png)

The order of the `elif` statements does not matter, however. Let's rearrange them to introduce a bug. Remember that the rest of the `elif` clauses are automatically skipped once a `True` condition has been found, so if you swap around some of the clauses in *vampire.py*, you run into a problem.

```python
name = 'Carol' 
age = 3000 
if name == 'Alice': 
	print('Hi, Alice.') 
elif age < 12: 
	print('You are not Alice, kiddo.') 
elif age > 100: 
	print('You are not Alice, grannie.') 
elif age > 2000: 
	print('Unlike you, Alice is not an undead, immortal vampire.')
```

Say the age variable contains the value `3000` before this code is executed. You might expect the code to print the string `'Unlike you, Alice is not an undead, immortal vampire.'` However, because the `age > 100` condition is `True`, the string `'You are not Alice, grannie.'` is printed, and the rest of the `elif` statements are automatically skipped. Remember that at most only one of the clauses will be executed, and for `elif` statements, the order matters!

Optionally, you can have an `else` statement after the last `elif` statement. In that case, it *is* guaranteed that at least one (and only one) of the clauses will be executed. If the conditions in every `if` and `elif` statement are `False`, then the `else` clause is executed. For example, let's re-create the Alice program to use `if`, `elif` and `else` clauses.

```python
name = 'Carol'
age = 3000
if name == 'Alice':
	print("Hi, Alice.")
elif age < 12:
	print('You are not Alice, kiddo.')
else:
	print('You are neither Alice nor a little kid.')
```

![](https://i.imgur.com/lwTR6kj.png)
### while Loop Statements

You can make a block of code execute over and over again using a `while` statement. The code in a `while` statement will be executed as long as the `while` statement's condition is `True`. In code, a `while` statement always consist of the following:

- The `while` keyword
- A condition (that is, an expression that evaluates to `True` or `False`)
- A colon
- Starting on the next line, an indented block of code (called the `while` clause)

You can see that a `while` statement look similar to an `if` statement. The difference is in how they behave. At the end of an `if` clause, the program execution continues after the `if` statement. But at the end of a `while` clause, the program execution jumps back to the start of the `while` statement. The `while` clause is often called the `while loop` or just the `loop`.

Let's look at an `if` statement and a `while` loop that use the same condition and take the same actions based on that condition. Here is the code with an `if` statement:

```python
spam = 0
if spam < 5:
	print('Hello, world.')
	spam = spam + 1
```

Here is the code with a `while` statement:

```python
spam = 0
while spam < 5:
	print('Hello, world.')
	spam = spam + 1
```

These statements are similar -- both `if` and `while` check the value of `spam`, and if it's less than 5, they print a message. But when you run these two code snippets, something very different happens for each one. For the `if` statement, the output is simply, `"Hello, world."`. But for the `while` statement, the output is `"Hello, world"` repeated five times. 

![](https://i.imgur.com/RgHraL2.png)

![](https://i.imgur.com/jLVZpMa.png)

The code with the `if` statement checks the condition, and it prints `Hello, world.` only once if that condition is true. The code with the `while` loop, on the other hand, will print it five times. The loop stops after five prints because the integer in `spam` increases by one at the end of each iteration, which means the loop will execute five times before `spam < 5` is false. 

In the `while loop`, the condition is always checked at the start of each *iteration*. If the condition is `True`, then the clause is executed, and afterward, the condition is checked again. The first time the condition is found to be `False`, the `while` clause is skipped. 
### An Annoying `while` Loop

Here's a small example program that will keep asking you to type, literally, `your name`. Select **File -> New** to open a new file editor window, enter the following code, and save the file as *yourName.py*:

```python
name = ''
while name != 'your name':
	print('Please type your name.')
	name = input()
print('Thank you!')
```

1. The program sets the `name` variable to an empty string. This is so that the `name != 'your name'` condition will evaluate to `True` and the program execution will enter the `while` loop's clause.
2. The code inside this clause asks the user to type their name, which is assigned to the `name` variable. 
3. Since this is the last line of the block, the execution moves back to the start of the `while` loop and reevaluates the condition. If the value in `name` is *not equal* to the string `'your name'`, then the condition is `True`, and the execution enters the `while` clause again. 

But once the user types `your name`, the condition of the `while` loop will be `'your name' != 'your name'`, which evaluates to `False`.  The condition is now `False`, and instead the program execution reentering the `while` loop's clause, Python skips past it and continues running the rest of the program. 

> If you never enter `your name`, then the `while` loop's condition will never be `False`, and the program will just keep asking forever. 

Here, the `input()` call lets the user enter the right string to make the program move on. In other programs, the condition might never actually change, and that can be a problem. Let's look at how you can break out of a `while` loop. 
### `break` Statements

There is a shortcut to getting the program execution to break out of a `while` loop's clause early. If the execution reaches a `break` statement, it immediately exits the `while` loop's clause. In code, a `break` statement simply contains the `break` keyword. 

Here's a program that does the same thing as the previous one, but it uses a `break` statement to escape the loop. Enter the following code, and save the file as *yourName2.py*.

```python
while True:
	print('Please type your name.')
	name = input()
	if name == 'your name':
		break
print('Thank you!')
```

1. The first line creates an infinite loop, a `while loop` whose condition is **always True**. (The expression `True`, after all, always evaluates down to the value `True`.) After the program execution enters this loop, it will exit the loop only when a `break`statement is executed. (An infinite loop that *never exits* is a common programming bug.)
2. While the execution is still inside the `while` loop, an `if` statement checks:
3. Whether `name` is equal to `your name`. If this condition is `True`, the `break` statement is skipped, and the execution is moved out of the loop to `print('Thank you!)`.
4. Otherwise, the `if` statement's clause that contains the `break` statement is skipped, which puts the execution at the end of the `while` loop. At this point, the program execution jumps back to the start of the `while` statement to recheck the condition. Since this condition is merely the `True` boolean value, the execution enters the loop to ask the user to type `your name` again. 
### `continue` Statements

Like `break` statements, `continue` statements are used inside loops. When the program execution reaches a `continue` statement, the program execution immediately *jumps back*
*to the start of the loop and reevaluates the loop;'s condition*.

Let's use `continue` to write a program that asks for a name and a password. Enter the following code into a new file editor window and save the program as *swordfish.py*.

> [!NOTE] Stuck in an infinite loop?
> If you ever run a program that has a bug causing it to get stuck in an infinite loop, press `CTRL+C` or select **Shell -> Restart Shell** from IDLE's menu. This will send a `KeyboardInterrupt` error to your program and cause it to stop immediately. Trying to stop a program by creating a simple infinite loop in the file editor, and save the program as `infiniteloop.py`
> 
> ``` python
> while True:
> 	 print('Hello World!')
> ```
> 
> When you run this program, it will print `Hello, world!` to the screen forever because the `while` statement's condition is always `True`. `CTRL+C` is also handy if you want to simply terminate your program immediately, even if it's not stuck in an infinite loop.

```python
while True:
	print('Who are you?')
	name = input()
	if name != 'Joe':
		continue
	print('Hello, Joe. What is the password? (It is a fish.)')
	password = input()
	if password == 'swordfish':
		break
print('Access Granted.')
```

If the user enters any name besides `Joe`, the `continue` statement causes the program execution to jump back to the start of the loop. When the program reevaluates the condition, the execution will always enter the loop, since the condition is simply the value `True`. Once the user makes it past the `if` statement, they are asked for a password. 

If the password entered is `swordfish`, then the `break` statement is run, and the execution continues to the end of the `while` loop, where it then jumps back to the start of the loop. 

![](https://i.imgur.com/mHqkz0s.png)

> [!Important] Truthy and Falsey Values
> Conditions will consider some values in other data types equivalent to `True` and `False`. When used in conditions, 0, 0.0 and ' ' (empty string) are considered `False`, while all other values are considered `True`. For example, look at the following program.
> 
> ```python
> name = ''
> 	print('Enter your name:')
> 	name = input()
> print('How many guests will you have?')
> numOfGuests = int(input())
> 	if numOfGuests:
> 		print('Be sure to have enough room for all your guests.')
> print('Done')
> ```
> 
> If the user enters a blank string for `name`, then the while statement's condition will be `True`, and the program continues to ask for a name. If the value for `numOfGuests` is not `0`, then the condition is considered to be `True`, and the program will print a reminder for the user. You could have entered `not name != ''` instead of `not name`, and `numOfGuests != 0` instead of `numOfGuests`, but using the truthy and falsey values can make your code easier to read. 

```python
while True:
	print('Who are you?')
	name = input()
	if name != 'Joe':
		continue
	print('Hello, Joe. What is the password? (It is a fish.)')
	password = input()
	if password == 'swordfish':
		break
print('Access Granted.')
```
```
Who are you? 
I'm fine, thanks. Who are you? 
Who are you? Joe 
Hello, Joe. What is the password? (It is a fish.) 
Mary 
Who are you? Joe 
Hello, Joe. What is the password? (It is a fish.) 
swordfish 
Access granted.
```
### `for` Loops and the `range()` Function

The `while` loop keeps looping while its condition is `True` (which is the reason for it's name), but what if you want to execute a block of code only a certain number of times? You can do this with the `for` loop and the `range()` function

In code, a `for` statement looks for something like `for i in range(5)`: and includes the following:

- The `for` keyword
- A variable name
- The `in` keyword
- A call to the `range()` method with up to three integers passed to it
- A colon
- Starting on the next line, an indented block of code (the `for clause`)

```python
print('My name is')
for i in range(5):
	print('Jimmy Five Times (' + str(i) + ')')
```

The first time this code runs, the variable `i` is set to `0`. The `print()` call in the clause will print `Jimmy Five Times (0)`. After Python finishes an iteration through all the code inside the `for` loop's clause, the execution goes back to the top of the loop, and the `for` statement increments `i` by one. This is why `range(5)` results in five iterations through the clause, with `i` being set to `0`, then `1`, then `2`, then `3` and then `4`. The variable `i` will go up to, but will not include, the integer passed to `range()`. 

> [!NOTE]
> You can use break and continue statements inside for loops as well. The continue statement will continue to the next value of the for loop’s counter, as if the program execution had reached the end of the loop and returned to the start. In fact, you can use continue and break statements only inside while and for loops. If you try to use these statements elsewhere, Python will give you an error.

![](https://i.imgur.com/MutLF9o.png)

As another example of a `for` loop, consider this story about the mathematician Carl Friedrich Gauss. When Gauss was a boy, a teacher wanted to give the class some busy work. The teach told them to add up all the numbers from 0 to 100. Young Gauss came up with a clever trick to figure out the answer in a few seconds, but we can write a Python program with a `for` loop to do this calculation for us.

```python
total = 0
for num in range(101):
	total = total + num
print(total)
```

The result should be 5,050. When the program first starts, the `total` variable is set to `0`. The for loop executes `total = total + num` 100 times. By the time the loop has finished all of its 100 iterations, every integer from `0` to `100` will have been added to `total`. Then, `total` is printed to the screen. 
#### An Equivalent `while` Loop

You can actually use a `while` loop to do the same thing as a `for` loop; `for` loops are just more concise. Let's rewrite *fiveTimes.py* to use a `while` loop equivalent of a `for` loop. 

```python
print('My name is')
i = 0
while i < 5:
	print('Jimmy Five Times (' + str(i) + ')')
	i = 1 + 1
```
#### The Starting, Stopping, and Stepping Arguments to `range()`

Some functions can be called with multiple arguments separated by a comma, and `range()` is one of them. This lets you change the integer passed to `range()` to follow any sequence of integers, including starting at a number other than zero.

```python
for i in range(12, 16)
	print(i)
```

The first argument will be where the `for` loop's variable starts, and the second argument will be up to, but not including, the number to stop at.

```
12
13
14
15
```

The `range()` function can also be called with three arguments. 

The first two arguments will be the **start** and **stop** values, and the third will be the *step argument*.
	The step is the amount that the variable is increased by after each iteration.

```python
for i in range(0, 10, 2):
	print(i)
```

So calling `range(0, 10, 2)` will count from zero to eight by intervals of two.

```
0
2
4
6
8
```

The `range()` function is flexible in the sequence of numbers it produces for `for` loops. *For* example, you can even use a negative number for the step argument to make the `for` loop count down instead of up.

```python
for i in range(5, -1, -1):
	print(i)
```
```
5
4
3
2
1
```
## Importing Modules

All Python programs can call a basic set of functions called *built-in functions*, including the `print()`, `input()`, and `len()` functions you've seen before. Python also comes with a set of modules called the *standard library*. Each module is a Python program that contains a related group of functions that can be embedded in your programs. For example, the `math` module has mathematics-related functions, the `random` module has random number-related functions, and so on.

Before you can use the functions in a module, you must **import** the module with an `import` statement. In code, an `import` statement consists of the following:

- The `import` keyword
- The name of the module
- Optionally, more module names, as long as they  are separated by commas.

Once you import a module, you can use all the cool functions of that module. 

```python
import random
for i in range(5):
	print(random.randint(1, 10))
```

> [!Important] Don't Overwrite Module Names
> When you save your Python scripts, take care not to give them a name that is used by one of Python's modules, such as *random.py*, *sys.py*, or *math.py*. If you accidentally name one of your programs, say, *random.py*, and use an `import random` statement in another program, your program would import your *random.py* file instead of Python's random module. This can lead to errors such as `AttributeError: module 'random' has no attribute 'randint'`, since your *random.py* doesn't have the functions that the real `random` module has. Don't use the names of built in functions either, such as `print()` or `input()`.
> 
> Problems like these are uncommon, but can be tricky to solve. As you gain more programming experience, you'll become more aware of the standard names used by Python's modules and functions, and will run into these problems less frequently.

Here's an example of an import statement that imports four different modules:

```python
import random, sys, os, math
```

Now we can use any of the functions in these four modules. 
### `from import` Statements

An alternative form of the `import` statement is composed of the `from` keyword, followed by the module name, the `import` keyword, and a star: for example: `from random import *`.

With this form of `import` statement, calls to functions in `random` will not need the `random` prefix. However, using the full name makes for more readable code, so it is better to use the `import random` form of the statement.
## Ending a Program Early with the `sys.exit()` Function

The last flow control concept to go over is how to terminate the program. Programs always terminate if the program execution reaches the bottom of the instructions. However, you can use the program to terminate, or exit, before the last instruction by calling the `sys.exit()` function. Since this function is in the `sys` module, you have to import `sys` before your program can use it.

Open a file editor and enter the following code, saving it as *exitExample.py*.

```python
import sys

while True:
	print('Type exit to exit.')
	response = input()
	if response == 'exit':
		sys.exit()
	print('You typed ' + response + '.')
```

This program has an *infinite loop with no `break` statement inside*. The only way this program will end is if the execution reaches the `sys.exit()` call. When `response` is equal to `exit`, the line containing the `sys.exit()` call is executed. Since the `response` variable is set by the `input()` function, the user must enter `exit` in order to stop the program.
## A Short Program: Guess the Number

The examples I’ve shown you so far are useful for introducing basic con- cepts, but now let’s see how everything you’ve learned comes together in a more complete program. In this section, I’ll show you a simple “guess the number” game. When you run this program, the output will look some- thing like this:

```
I am thinking of a number between 1 and 20. 
Take a guess. 
10 
Your guess is too low. 
Take a guess. 
15 Your guess is too low. 
Take a guess. 
17 
Your guess is too high. 
Take a guess. 
16 Good job! 
You guessed my number in 4 guesses!
```

```python
# This is a guess the number game.

import random

secretNumber = random.randint(1, 20)
print('I am thinking of a number between 1 and 20.')

# Ask the player to guess 6 times.
for guessesTaken in range(1, 7):
	print('Take a guess.')
	guess = int(input())

	if guess < secretNumber:
		print('Your guess is too low.')
	elif guess > secretNumber:
		print('Your guess is too high.')
	else:
		break # this condition is the correct guess

if guess == secretNumber:
	print('Good job! You guessed my number in ' + str(secretNumber) + ' guesses!')
else:
	print('Nope. The number I was thinking of was ' + str(secretNumber))
```

1. A comment at the top of the code explains the program. 
2. Then, the program imports the `random` module so that it can use the `random.randint()` function to generate a number for the user to guess.
3. The return value, a random integer between 1 and 20, is stored in the variable `secretNumber`.
4. The program tells the player that it has come up with a secret number and will give the player 6 guesses to guess it. 
5. The code that lets the player enter a guess and checks that guess is in a `for` loop that will loop at most six times. The first thing that happens in the loop is that the player types in a guess. Since `input()` returns a string, its return value is passed straight into `int()`, which translates the number into an integer value. This guess is stored in the variable name `guess`.

```python
	if guess < secretNumber:
		print('Your guess is too low.')
	elif guess > secretNumber:
		print('Your guess is too high.')
	else:
		break # this condition is the correct guess
```

These few lines of code check to see whether the guess is less than or greater than the secret number. In either case, a hint is printed to the screen.

```python
else:
	break
```

If the guess is neither higher not lower, than the secret number, then it must be equal to the secret number -- in which case, you want the program execution to break out of the `for` loop.

```python
if guess == secretNumber:
	print('Good job! You guessed my number in ' + str(guessesTaken) + ' guesses!')
else:
	print('Nope. The number I was think of was ' + str(secretNumber))
```

After the `for` loop, the previous `if...else` statement checks whether the player has correctly guessed the number and then prints an appropriate message to the screen. In both cases, the program displays a variable that contains an integer value (`guessesTaken` and `secretNumber`). Since it must concatenate these integer values to strings, it passes these variables to the `str()` function, which returns the string value form of these integers. 

Now these strings can be concatenated with the `+` operators before finally being passed to the `print()` function call.
## A Short Program: Rock, Paper, Scissors

Let's use the programming concepts we've learned so far to create a simple rock, paper, scissors game. The output will look like this:

```
ROCK, PAPER, SCISSORS
0 Wins, 0 Losses, 0 Ties
Enter your move: (r)ock (p)aper (s)cissors or (q)uit
p
PAPER versus...
PAPER
It is a tie!
0 Wins, 1 Losses, 1 Ties
Enter your move: (r)ock (p)aper (s)cissors or (q)uit
s
SCISSORS versus...
PAPER
You win!
1 Wins, 1 Losses, 1 Ties
Enter you move: (r)ock (p)aper (s)cissors or (q)uit
q
```

```python
import random, sys

print('ROCK, PAPER, SCISSORS')

# these variables keep track of the number of wins, losses and ties
wins = 0
losses = 0
ties = 0

while True: # The main game loop
	print('%s Wins, %s Losses, %s Ties' % (wins, losses, ties))
	while True:
		print('Enter your move: (r)ock (p)aper (s)cissors or (q)uit')

playerMove = input()

if playerMove == 'q':

sys.exit()

if playerMove == 'r' or playerMove == 'p' or playerMove == 's':

break

print('Type one of r, p, s or q.')

  

# display what the player chose

if playerMove == 'r':

print('ROCK versus...')

elif playerMove == 'p':

print('PAPER versus...')

elif playerMove == 's':

print('SCISSORS versus...')

  

# display what the computer chose

randomNumber = random.randint(1, 3)

if randomNumber == 1:

computerMove = 'r'

print('ROCK')

elif randomNumber == 2:

computerMove = 'p'

print('PAPER')

elif randomNumber == 3:

computerMove = 's'

print('SCISSORS')

# display and record the win/loss/tie:

if playerMove == computerMove:

print('It is a tie!')

ties = ties + 1

elif playerMove == 'r' and computerMove == 's':

print('You win!')

wins = wins + 1

elif playerMove == 'p' and computerMove == 'r':

print('You win!')

wins = wins + 1

elif playerMove == 's' and computerMove == 'p':

print('You win!')

wins = wins + 1

elif playerMove == 'r' and computerMove == 'p':

print('You lose!')

losses = losses + 1

elif playerMove == 'p' and computerMove == 's':

print('You lose!')

losses = losses + 1

elif playerMove == 's' and computerMove == 'r':

print('You lose!')

losses = losses + 1
```

1. First, we import the `random` and `sys` module so that our program can call `random.randint()` and `sys.exit()` functions. We also set up three variables to keep track of how many wins, losses, and ties the player has had. 

```python
while True: # The main game loop
	print('%s Wins, %s Losses, %s Ties' % (wins, losses, ties))
	while True:
		print('Enter your move: (r)ock (p)aper (s)cissors or (q)uit')
		playerMove = input()
		if playerMove == 'q':
			sys.exit()
		if playerMove == 'r' or playerMove == 'p' or playerMove == 's':
			break
		print('Type one of r, p, s or q.')
```

2. This program uses a `while` loop inside of another `while` loop. The first loop is the main game loop, and a single game of rock, paper, scissors is player on each iteration through this loop. The second loop asks for input from the player, and keeps looping until the player has entered an `r`, `p` or `s` or `q` for their move. The `r`, `p`, and `s` correspond to **rock**,**paper** and **scissors**, the `q` means that the player wants to quit. If the player has entered `r`, `p` or `s`, the execution breaks out of the loop. Otherwise, the program reminds the player to enter `r`, `p`, `s` or `q` and goes back to the start of the loop. 


```python
if playerMove == 'r':
	print('ROCK versus...')
elif playerMove == 'p':
	print('PAPER versus...')
elif playerMove == 's':
	print('SCISSORS versus...')
```

3. The player's move is displayed on the screen.

```python
# display what the computer chose
randomNumber = random.randint(1, 3)
if randomNumber == 1:
	computerMove = 'r'
	print('ROCK')
elif randomNumber == 2:
	computerMove = 'p'
	print('PAPER')
elif randomNumber == 3:
	computerMove = 's'
	print('SCISSORS')
```

4. Next, the computer's move is randomly selected. Since `random.randint()` can only return a random number, the `1`, `2` or `3` integer value it returns is stored in a variable named `randomNumber`. 

```python
# display and record the win/loss/tie:
if playerMove == computerMove:
	print('It is a tie!')
	ties = ties + 1
elif playerMove == 'r' and computerMove == 's':
	print('You win!')
	wins = wins + 1
elif playerMove == 'p' and computerMove == 'r':
	print('You win!')
	wins = wins + 1
elif playerMove == 's' and computerMove == 'p':
	print('You win!')
	wins = wins + 1
elif playerMove == 'r' and computerMove == 'p':
	print('You lose!')
	losses = losses + 1
elif playerMove == 'p' and computerMove == 's':
	print('You lose!')
	losses = losses + 1
elif playerMove == 's' and computerMove == 'r':
	print('You lose!')
	losses = losses + 1
```

5. Finally, the program compares the strings in `playerMove` and `computerMove`, and displays the results on the screen. It also increments the `wins`, `losses` or `ties` variable appropriately. Once the execution reaches the end, it jumps back to the start to begin another game.
## Practice Questions

> [!question]
> 1. What are the two values of the Boolean data type? How do you write them?

`True` and `False`.

> [!question]
> 2. What are the three Boolean operators?

`AND`, `OR` and `NOT`.

> [!question]
> 3. Write out the truth tables of each Boolean operator (that is, every possible combination of Boolean values for the operator and what they evaluate to).

> [!question]
> 4. What do the following expressions evaluate to? 
> ``` > (5 > 4) and (3 == 5) 
> not (5 > 4) 
> (5 > 4) or (3 == 5) 
> not ((5 > 4) or (3 == 5)) 
> (True and True) and (True == False) 
> (not False) or (not True)
> ```

1. False
2. False
3. True
4. False
5. False
6. True

> [!question]
> 5. What are the six comparison operators?

1. `>`
2. `<`
3. `>=`
4. `<=`
5. `==`
6. `!=`

> [!question]
> 6. What is the difference between the equal operator and the assignment operator?

The equal operator asks if two values are equal, the assignment operator sets something to a value.

> [!question]
> 7. Explain what a condition is and where you would use one.

A `condition` is a Boolean equation that asks if something evaluates to `True` or `False`. It can be used in logical operations within Python programs, to execute certain code if certain conditions are met or unmet, etc.

> [!question]
> 8. Identify the three blocks in this code:
>    
>```
>    spam = 0
>    if spam == 0
> 	   print('eggs')
> 	   if spam > 5:
> 		   print('bacon')
> 	   else: 
> 		   print('ham')
> 	   print('spam')
>    print('spam')
>```

`spam = 0` sets the variable `spam` to the value `0`. 

`if spam == 0`, `print ('egg')` is a conditional statement.

`if spam > 5`: `print('bacon')` is another conditional statement, nested within the first.

`else`: `print(...)` is the conclusion of the conditional statement, which would print `ham` if the above conditional statement was found to be `False`.

`print('spam')` is the series of nests fall outside the scope of the `if` statement, so would just be regular print statements that will print the specified code to the console.

> [!question]
> 9. Write code that prints `Hello` if stored in `spam`, prints `Howdy` if `2` is stored in `spam`, and prints `Greetings!` if anything else is stored in `spam`.

```python
spam = 1
if spam == 1:
	print('Hello')
elif spam == 2:
	print()'Howdy')
else:
	print('Greetings!')
```

> [!Question]
> 10. What keys can you press if your program is stuck in an infinite loop?

> `Ctrl + C`

> [!question]
> 1. What is the difference between `break` and `continue`?

`break` is used to exit a loop, often used with a conditional statement. 
`continue` is used to continue iterating through a loop, also often used with conditionals.

> [!question]
> 12. What is the difference between `range(10)`, `range(0, 10)` and `range(0, 10, 1)`?

`range(10)` specifies a range of numbers 0-9, because Python is a zero-indexed language.

`range(0, 10)`: the range begins at 0, and ends at 9. The output is always 1 less than the specified `stop` parameter. 

`range(0, 10, 1)`: the range starts at 0 and ends at 10, incrementing by 1 at each `step`.

> [!question]
> 13. Write a short program that prints the numbers 1 to 10 using a for loop. Then write an equivalent program that prints the numbers 1 to 10 using a while loop.

```python
for i in range(0, 11):
	print(i)

i = 0
while i < 10:
	i += 1
	print(i)
```

> [!question]
> 14. If you had a function named bacon() inside a module named spam, how would you call it after importing spam?

```python
from spam import bacon
```

**Extra Credit**: Look up the `round()` and `abs()` functions. Experiment with them. 

> The `abs()` function takes a `number` as a parameter and returns the absolute value of that number.

```python
x = abs(3+5j)
print(x)

y = abs(-7.25)
print(y)

z = abs(4*9)
print(z)

5.830951894845301
7.25
36
```

> The `round()` function rounds a number to a specified number of decimals, the second parameter dictates the amount of decimals. 

```python
x = round(5.76543, 2)
print(x)

y = round(6.24535353, 6)
print(y)

5.77
6.245354
```
# Chapter 3: Functions

Python provides several **built-in functions** like `print()`, `input()` and `len()`. But, you can also write your own functions with Python. A *function* is like a mini-program within a program.

```python
def hello():
	print('Howdy')
	print('Howdy!!!')
	print('Hello there.')

hello()
```
```
Howdy
Howdy!!!
Hello there.
```

1. The first line is a `def` statement, which defines a function named `hello()`
2. The code in the block is the **function body**. 
3. The code is executed when the function is `called`, not when it is first defined.

In code, a function call is just the function's name followed by parentheses, possibly with some number of arguments in between the parentheses. When the program execution reaches these calls, it will jump to the top line in the function and begin executing the code there. When it reaches the end of the function, the execution returns to the line that called the function and continues moving through the code as before. 

Since this program calls `hello()` three times, the code in the `hello()` function is executed three times. 

The major purpose of functions is to *group code that gets executed multiple times*. Without a function defined, you would have to copy and paste this code each time, and the program would look like this:

```python
print('Howdy!') 
print('Howdy!!!') 
print('Hello there.') 
print('Howdy!') 
print('Howdy!!!') 
print('Hello there.') 
print('Howdy!') 
print('Howdy!!!') 
print('Hello there.')
```

> In general, you always want to avoid duplicating code because if you ever decide to update the code -- if, for example, you find a bug you need to fix -- you'll have to remember to change the code everywhere you copied it.
## `def` Statements with Parameters

When you call the `print()` or `len()` function, you **pass** them values, called **arguments**, by typing them between the parenthesis. You can also define your own functions that accept arguments. Type this example into the file editor and save it as `hellofunc2.py`:

```python
def hello(name):
	print('Hello, ' + name)

hello('Alice')
hello('Bob')
```

1. The definition of the `hello()` function is this program has a parameter called `name`. 
2. Parameters are variables that contain arguments. When a function is called with arguments, the arguments are stored in the parameters. The first time the `hello()` function is called, it is passed the argument `'Alice'`. The program execution enters the function, and the parameter `name` is automatically set to `'Alice'`, which is what gets printed by the `print()` statement. 

> One special thing to note about parameters is that the value stored in a parameter is forgotten when the function returns. For example if you added `print(name)` after `hello('Bob')` in the previous program, the program would give you a `NameError` because there is not variable named `name`.

The variable is destroyed after the function call `hello('Bob')` returns, so `print(name)` would refer to a variable that does not exist.

This is similar to how a program’s variables are forgotten when the pro- gram terminates. I’ll talk more about why that happens later in the chapter, when I discuss what a function’s local scope is.
### Define, Call, Pass, Argument, Parameter

The terms

- `define`
- `call`
- `pass`
- `argument`
- `parameter`

can be confusing. Let's look at a code example to review these terms:

```python
def sayHello(name):
	print('Hello, ' + name)
sayHello('Al')
```

1. To define a function is to *create it*, just like an assignment statement like `spam = 42` creates the `spam` variable. The `def` statement defines the `sayHello()` function.
2. The `sayHello('Al')` line *calls* the now-created function, sending the execution to the top of the function's code. This function call is also known as *passing* the string value `'Al'` to the function. A value being passed to a function in a function is called an *`argument`*. The argument `'Al'` is assigned to a **local variable** named `name`. Variables that have arguments assigned to them are *`parameters`*.
## Return Values and `return` Statements

When you call the `len()` function and pass it an argument such as `'Hello'`, the function call evaluates to the integer 5, which is the length of the string you passed it. In general, the value that a function call evaluates to is called the *return value* of the function.

When creating a function using the `def` statement, you can specify what the return value should be with a `return` statement. A `return` statement consists of the following:

- The `return` keyword
- The value or expression that the function should return.

When an expression is used with a return statement, the return value is what this expression evaluates to. For example, the following program defines a function that returns a different string depending on what num- ber it is passed as an argument. Enter this code into the file editor and save it as `magic8Ball.py:`

```python
import random

def getAnswer(answerNumber):
	if answerNumber == 1:
		return 'It is certain.'
	elif answerNumber == 2:
		return 'It is decidedly so'
	elif answerNumber == 3:
		return 'Yes'
	elif answerNumber == 4:
		return 'Reply hazy try again'
	elif answerNumber == 5:
		return 'Ask again later'
	elif answerNumber == 6:
		return "Concentrate and ask again"
	elif answerNumber == 7:
		return 'My reply is no'
	elif answerNumber == 8:
		return 'Outlook not so good'
	elif answerNumber == 9:
		return 'Very doubtful'

r = random.randint(1, 9)
fortune = getAnswer(r)
print(fortune)
```

1. Python first imports the `random` module.
2. Then the `getAnswer()` function is defined.
3. Because the function is being defined, and not called, the execution skips over the code in it. 
4. Next, the `random.randint()` function is called with two arguments: `1` and `9`. It evaluates to a random integer between `1` and `9`, and this value is stored in a variable named `r`.
5. The `getAnswer()` function is called with `r` ads the argument. The program moves to the top of the `getAnswer()` function, and the value `r` is stored in a parameter named `answerNumber`. Then, depending on the value of `answerNumber`, the function returns one of may possible string values. The program execution returns to the line at the bottom of the program that originally called `getAnswer()`. The returned string is assigned to a variable named `fortune`, which then gets passed to a `print()` call and is printed to the screen.

> Note that you can pass return values as an argument to another function call. 

Remember, expressions are composed of values and operators. A function call can be used in an expression because the call *evaluates to it's return value*.
## The `None` Value

In Python, there is a value called `None`m which represents the *absence* of a value. The `None` value is the only value of the `NoneType` data type. (Other languages might call this value `null`, `nil` or `undefined`).

Just like the Boolean `True` and `False` values, `None` must be capitalized.

This value-without-a-value can be helpful when you need to store something that won't be confused for a *real value* in a variable. One place where `None` is used is as the return value of `print()`. The `print()` function displays text on the screen, but it doesn't need to return anything in the same way `len()` or `input()` does. But since all function calls need to evaluate to a return value, `print()` returns `None`.

Behind the scenes, Python adds `return None` to the end of any function definition with no `return` statement. This is similar to how a `while` or `for` loop implicitly ends with a `continue` statement. 
## Keyword Arguments and the `print()` Function

Most arguments are identified by their position in the function call. 

For example, `random.randint(1, 10)` is different from `random.randint(10, 1)`. The function call `random.randint(1, 10)` will return a random integer between `1` and `10` because the first argument is the low end of the range and the second argument is the high end (while `random.randint(10, 1)` causes an error).

However, rather than through their position, *keyword arguments* are identified by the keyword put before them in the function call. Keyword arguments are often used for *optional parameters*. 

For example, the `print()` function has the optional parameters `end` and `sep` to specify what should be printed at the end of its arguments and between its arguments (separating them), respectively. 

If you ran the following code:

```python
print('Hello')
print('World')
```

the output would look like this:

```
Hello
World
```

The two outputted strings appear on separate lines because the `print()` function automatically adds a newline character to the end of the string it is passed. However, you can set the `end` keyword argument to change the new line character to a different string. 

For example, if the code were this:

```python
print('Hello', end='')
print('World')
```

the output would look like this:

```
HelloWorld
```

The output is printed on a single line because there is no longer a newline printed after `'Hello'`. Instead, the blank string is printed. This is useful if you need to disable the newline that gets added to the end of every `print()` function call.



