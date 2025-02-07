#python #hackthebox #programming 

> Python is one of the most popular programming languages, currently. This makes it a popular choice for `automation` of everyday tasks or the development of `tools`.

In the InfoSec world, plenty of **PoCs (Proof of Concepts)** are written in Python, as are many popular tools for penetration testing. The simplicity of the language makes it appealing to use when a need to "just write something quickly" arises.

Yet, the language's flexibility and community support also make it a perfect candidate for larger projects. 

- Whether you need to write a simple script that will automate a repetitive task on a website, crawling or analyzing large amounts of data, performing buffer overflow attacks, creating an interactive service, or something completely different, Python makes development easy.

> Python is an `interpreted language`, which means the code itself is not compiled into machine code like C code. 
> Instead, it is interpreted by the Python program, and the instructions in the script(s) are executed. 
> Python is a high-level language meaning the scripts we produce are ***simplified for our convenience*** so that we do not need to worry about memory management, system calls, and so forth. 
> Furthermore, Python is a `general-purpose`, `multi-paradigm` language that is a fancy way of saying "you can use it for most things with ease" and "it doesn't mind if you prefer one style or another."

As for the coding style, we will gently touch on the object-oriented style because this makes reasoning about code a lot simpler. 

- Essentially, object-oriented programming will likely feel less intimidating if you've ever played with either blocks or bricks of either digital or physical form. 
- Lastly, Python is rumored to be easy to read, especially in the beginning. This may be *because of its close resemblance to the English language* and its strict requirements for proper code indentation.

# Executing Python Code

> There are many ways to execute a piece of Python code.  

Two of the most frequently used methods are running the code from a `.py` file and running it directly inside the Python IDLE, **Integrated Development and Learning Environment**. 

In this section, we will look at how to run code both ways. 

The file-based way is handy when *developing an actual script* and the IDLE way is very useful for *quickly testing something small.* 

We will start with the file-based approach.

### Python3

> Let's start with a widespread, first piece of code that prints out "Hello World" to the terminal or screen. It looks like this:

```python
print("Hello Academy!")
```

If we run this script, the string `"Hello Academy!"` will be printed to the terminal. To try it out, we open a text editor, type in the above, and save the file as `welcome.py`. Next, we try running it be executing `python3 welcome.py`.

```shell
trop3n@htb[/htb]$ vim welcome.py
trop3n@htb[/htb]$ python3 welcome.py

Hello Academy!
```

### IDLE

> We can utilize `IDLE`, Python's own integrated development environment, directly in our terminal for quicker prototyping.

We launch this by executing the Python binary without any arguments. Within this, we can have evaluate simple math equations, like `4 + 2`, or store and use variables. 

When evaluating an expression, the result will be printed on the line below if a result is returned. However, if the expression is stored as a variable, nothing will be printed as nothing is returned (it is all contained in the variable). 

We can also import libraries and define functions and classes directly in the IDLE for usage in the same session. We will dive deeper into libraries, functions, and classes later on. 

> To exit IDLE, we type `exit(0)`. The number `0` is the `return code` of the Python process, where 0 means all is OK and a number different from 0 indicates and error. 

#### Python IDLE

```shell
trop3n@htb[/htb]$ python3

Python 3.9.0 (default, Oct 27 2020, 14:15:17) 
[Clang 12.0.0 (clang-1200.0.32.21)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

```python
>>> 4 + 3
7
>>> foo = 3 * 5
>>> foo
15
>>> foo + 4
19
>>> print('Hello Academy!')
Hello Academy!
>>> exit(0)
```

> Python executes the code from top to bottom.
> 
> This is an important thing to keep in mind when writing Python scripts because Python has no clue what is further down in the script until it gets to it. 
> 	If we were to print a variable instead of a literal value, it must be defined before referencing. 

For example:

#### Hello Again, Academy

```python
>>> greeting = 'Hello again, Academy'
>>> print(greeting)
Hello again, Academy
```

> However, we can print the output of not only one variable but of several in different variations.

#### Printing Multiple Variables
```python
>>> a = 'HTB'
>>> b = 'Academy'
>>> print(a, b)
HTB Academy
```

### Shebang

> Another method is based on adding the [shebang](https://en.wikipedia.org/wiki/Shebang_%28Unix%29#Portability) (`#!/usr/bin/env python3`) in the first line of a Python script. 

On a Unix-based operating system, marking this with a pound sign and an exclamation mark causes the following command to be executed along with all of the specified arguments when the program is called.

We can give the Python script execution rights and execute it directly without entering `python` at the beginning of the command line. The file name is then passed as an argument.

#### welcome.py

```python
#!/usr/bin/env python3

print("Hello Academy!")
```

#### Shebang Execution

```shell
trop3n@htb[/htb]$ chmod +x welcome.py
trop3n@htb[/htb]$ ./welcome.py

Hello Academy!
```

# Introduction to Variables

> Let us assume for a moment that we are tasked with doing a penetration test for a client with a locked-down user environment. 
> 
> While investigating our options for our `Assume Breach` test, ***i.e. a test assuming that have already successfully compromised a regular user account and machine through phishing***, we discover that we can run Python scripts.

We can produce a list of potential user accounts, and we would also like to have a `target specific` list of potential passwords. 

We notice that the client's website contains many `buzzwords`, and we wonder if some users used variations of product names as their passwords. 

For this, we need to write a simple script that can produce a list of a website's most frequently occurring words. Since the client wants to get a copy, we will try our best to make the script easy to read and maintain.

> Before we get ahead of ourselves, we need to carve out the ***essential building blocks.*** 
> 
> 	For this, let us talk about math. Math and programming have some things in common: both use variables and constants a fair bit, and both have functions. 
> 	In Python, a variable is our way of storing a value of some sort in memory. For example, a number, some text, or the bytes of an image. 
> 		Like in math, variables have a name that we make up, but the names should be descriptive in Python. 

Here are some variable examples:

```python
advice = "Don't panic"
ultimate_answer = 42
potential_question = 6 * 7
confident = True
something_false = False
problems = None

# Oh, and by the way, this is a comment. We can tell by the leading # sign.

```

#### Strings

> The first variable, `advice`, is a `string`. Strings in Python can be specified using both `"double quotes"` and `'single quotes'`. 
> 	When typing out strings that contain either symbol as a natural part of the string itself, e.g. `don't lie`, it is a good idea to use the `other` kind of quotes. 
> 		Writing `"don't lie"` works just fine. However, using single quotes would throw an error. 

#### Integers

> Following the `advice` variable comes two numbers, or `integers`, the first of which is a number. The second variable,`potential_question`, is also a number but not until **`runtime`.**

- During runtime, the equation `6 * 7` is evaluated to `42`, which is then stored as the variable.

#### Booleans

> Following the number variables come two `boolean` variables, `confident` and `something_false`. 

A boolean value is a truth value and can be either `True` or `False`. These will come in handy later. 

Right after comes the variable `problems`, which is set to `None`. 
- [None](https://realpython.com/null-in-python/#:~:text=Python%20uses%20the%20keyword%20None,and%20a%20first%2Dclass%20citizen!) is a special "nothingness" of a value similar to `null` in other languages.

The usefulness of this value is, among other things, that it allows us to `define variables` in the code but not give them a concrete value just yet.

- It also allows us to create a more meaningful program flow and decide to pass along `either` some data `or None`, e.g. in case of errors.
- Moreover, it allows us to return it as a value if  "none of something" was found. This also enhances the program flow and readability.

#### Comments

> Lastly, we see a comment. Comments work the same way in Python as they do in all other languages: they are ignored when the program runs and are only for the developer's eyes. 

It can sometimes be advisable to use comments to remember what a piece of code does or explain some oddity. However, it is strongly recommended to write clean and simple code that will not need further explanation other than the code itself. 

This is not always the easiest way to get started, but we will try to *aim for this later*. 

### Combining Variables

> Let us go through a few examples to see how all these variables can also be combined. Later on, whether for our projects or specific tasks, we will want to output variables (and thus also their contents) together. 

Therefore, let us first briefly go through some basic math operations with Python.

#### Basic Math Operations

```python
>>> 10 + 10 #Addition
20
>>> 20 - 10 #Subtraction
10
>>> 5 * 5 #Multiplication
25
>>> 10 / 5 #Division
2
```

For all of these values, we can define variables to store them. As for the name itself, we can name them as we please, however with a few exceptions e.g. they must begin with a letter or `_`.

#### Saving Values to Variables

```python
>>> add = 10 + 10
>>> sub = 20 - 10
>>> multi = 5 * 5
>>> div = 10 / 5
>>>
>>> print (add, sub, multi, div)
20 10 25 2
```

> This also allows us to work with the values stored in the individual variables.

```python
>>> print(add, sub, multi, div)
20 10 25 2
>>> result = (add * sub) - (multi * div)
>>> print('Result:', result)
Result = 150
```

> Another handy feature of the Python interpreter is that the IDLE assigns the ***latest expression to the variable _***. 
> 	This allows us to continue working with the last value.

```python
>>> 38 + 4
42
>>> 50 - _		# 50 - 42
8
```

> Note that this true ***only for IDLE*.** In regular Python code that is run from `.py` files e.g. from the command line or an IDE, `_` is simply just a variable.

- It is often used as a placeholder for values we do not care about, for example if a function returns two values, but only one of them is important to use, for example `x_coord, _ = get_position_of_birb()`.
- This is to show other developers, and ourselves a few months into the future, that the value returned, e.g. the y-coordinate from the previous example, is not needed.

### Coding Style

> In Python, variable names follow the `snake_case` naming convention. This means that variable names ***should all be lowercase initially, and an underscore should separate any potential need for multiple words in the name***.

While ignoring these naming conventions may not cause any issues for the script - Python could care less about what we call our things - other Python developers may get thrown off if they expect one set of rules but face another.

The main point here is that *our code should be easy to follow and read.* 

Every programmer has their style and preferences when it comes to writing code. There are even several guides for Python, such as [PEP8](https://www.python.org/dev/peps/pep-0008/#type-variable-names), which describes certain types of variable or function definitions. 

Having a style guide is very important when we want someone else to read the code we write. We usually write code so that someone can use it, benefit from it and possibly work on it or learn something new from it. 

Without a style guide, debugging, improving, or extending becomes immensely difficult.

Of course, there are many other things besides the style guide that we as professional programmers need to pay attention to, such as code architecture, general principles for code quality, etc.

# Conditional Statements and Loops

> Below is an example of what an if/else `block` of code looks like, i.e., the amount of code that constitutes a particular technique and is visually grouped (typically indented at the same level).
#### Simple Feature Switch

```python
happy = true

if happy:
	print("Happy and we know it!")
else:
    print("Not happy...")

```

> A few things happened here already. Pay close attention to the **indentation of the code**. 

Python does not require how wide each indentation must be, as long as there is `consistency`. Some people prefer two spaces, others 4. Some people prefer a single tab character. 

- *We will continue using four spaces going forward.*

Besides indentations, two new keywords are used here: `if` and `else`. First, we define a variable which, for the sake of demonstration, is currently `True`.

Then we check `if` the variable `happy` is `True` (`if some_var` is easier to read but also shorthand for `if some_var == True`), and if it is `True`, then we print "Happy and we know it!" to the terminal. If `happy` is `not True`, i.e. it is `False`, then the `else` block is executed instead, and "Not happy..." is printed to the terminal. 

Nevertheless, we also have to consider the situation that we want to bring in more than just two different options. The `elif` (else-if) expression means that we continue with this one if the previous condition is not met. 

- Basically, `elif` is the shortened notation of nested `if` statements. 

### If-Elif-Else Statement

```Python
happy = 2

if happy == 1:
    print("Happy and we know it!")
elif happy == 2:
    print("Excited about it!")
else:
    print("Not happy...")
```

> This brings us to the first type of loop: the `while-loop`. Consider the below code:

### The While Loop

```python
counter = 0

while counter < 5:
    print(f"Hello #{counter}")
    counter = counter + 1
```

> Before we dive into the code, it is essential to know how a while loop works in the first place. 

A **while-loop** is a *loop that will execute its content (the block) as long as the defined condition is `true`*. 

- This means that `while True` will run forever, and `while False` will never run.
- By doing what we do in this example, we tell Python to run the contents of the while-loop for as long as the `counter` variable is below 5. 
- Inside the while loop, we must remember to increase the `counter` by (at least) 1 every time we make an iteration or eventually, anyway. 

> If we try to run the above example, `print` will be called 5 times and print the contents of the function.

Now, what are the contents of `print`? Let us quickly talk about formatted strings before continuing with loops.
#### Formatted Strings

A **format string** is a string that *lets us `populate the string` with values during **runtime.***

- A new formatting string was introduced in Python 3.6, the [f-string](https://realpython.com/python-f-strings/) (above example).

> While a regular string looks like `'Hello World'`, an f-string adds an `f` at the beginning : `f'Hello World'`. These particular two string are of the same value. 

The benefit of the f-string, however, is that we can swap out parts of the strings with other values and variables by enclosing them in a pair of curly brackets.

#### Format Strings

```python
equation = f'The meaning of life might be {6 * 7}.' # -> the meaning of life might be 42.

me = 'Birb'
greeting = f'Hello {me}!' # -> Hello Birb!
```

> Now that we know that a while loop is a loop that continues to execute while some condition is ture, and know that `f'Hello #{counter}'` will equal `Hello #` followed by the number of the iteration - starting at 0 - we are ready to try to execute the code!

#### While-Loop

```shell
trop3n@htb[/htb]$ vim loop1.py
trop3n@htb[/htb]$ python3 loop1.py

Hello #0
Hello #1
Hello #2
Hello #3
Hello #4
```

The loop checks if the counter, which is set to 0 initially, is below 5 - it is - and the prints "Hello #0" and sets the `counter variable` to the value of itself (0) + 1.

Next iteration, it checks if `counter`, which is now 1, is less than 5 - it is - and then prints "Hello #1" and sets `counter` to the value of itself (1) + 1. On the 3rd iteration, `counter` is 2 (because we started at 0), and so forth. 

> In the next section, we will continue looking at loops, but this time a simpler type of loop and one we will be favoring over the other as much as possible. 

### Loops and Lists

Recall from the previous section that a loop is a block of code that keeps iterating the contents until some condition is met. This section will look at one kind of loops often referred to as the "for-each loop".

This is a loop that iterates over `each element` is some collection of elements and does something `for each` individual element. Consider the below line of code:

#### A List of Strings

```python
groceries = ['Walnuts', 'Grapes', 'Bird Seeds']
# index         0           1           2
```

This is a list of strings. The square brackets include a list, and the comma-separated values inside of it are strings. Similarly, `[]` is an empty list, and `[42]` is a list with just one element, the `int` value `42`. When pointing out values inside lists, Python numbers the elements in a list from 0 and upwards.

This means that the above that the above list has `three elements` and that `the first` element is at `index 0`. The second element is at index 1, and the third element is at index 2. Like so:

#### Value Indexes

```python
groceries = ['Walnuts', 'Grapes', 'Bird Seeds']
# index:         0          1           3
```

> We can also write lists the following way for easier readability (especially with much larger lists):

#### Alternative Syntax

```python
groceries = [
    'Walnuts' # index 0
    'Grapes'  # index 1
    'Bird Seeds' # index 2
]
```

The last things to mention about lists before we move on is how to retrieve an element from the lists. Say we want to print the first element to the console. This is done be referencing the variable name of the list, e.g. `groceries` and which index is desired like so: `groceries[0]` to get the first element, `'Walnuts'`. 

The last element, `'Bird Seed'` would in this example then be the `groceries[2]` because the value `Bird Seeds'` is located at index 2 in the list.

Python can even count backwards, so we could also have gotten the last element of the list - regardless of how many elements are in it - by asking for index -1: `groceries[-1]`. It works the same way we did with strings.

#### Strings Indexing

Strings can also be indexed. This is especially useful when we want to filter out certain parts of some output. We can think of each word as a list of letters with indexes. 

However, there is also the *negative index*, which allows us to start continuing the string letters from the end. 

Let us take the following string as an example: `ABCDEF`

| Negative Index | Index | Character |
| -------------- | ----- | --------- |
| `-6`           | `0`   | A         |
| `-5`           | `1`   | B         |
| `-4`           | `2`   | C         |
| `-3`           | `3`   | D         |
| `-2`           | `4`   | E         |
| `-1`           | `5`   | F         |
> We use the index to tell Python which letter we want to output from it. In this example, we want to output the first and last letter.

```Python
>>> var = "ABCDEF"
>>> print(var[0], var[1], var[2], var[3], var [4], var[5])
A B C D E F
>>> print(var[-1], var[-2], var[-3], var[-4], var[-5], var [-6]) 
F E D C B A
```

We can also work with these indexes to give us particular substrings.

#### Substrings

```python
>>> var = "ABCDEF"
>>> print(var[:2]) # Up to index 2
AB
>>> print(var[2:]) # Ignore everything up to index 2
CDEF
>>> print(var[2:4]) # Everything between index 2 and 4 (2 is counted)
CD
>>> print(var[-2:]) # Up to negative index 2 (last two characters)
EF
```

### For-Each Loop

As already mentioned, Python allows us to loop over each element (or value) in a list. Consider below piece of code where we first have defined a list and then a loop. 

####  The For-Each Loop

```python
groceries = ['Walnuts', 'Grapes', 'Bird Seeds']

for food in groceries:
    print(f'I bought some {food} today.')
```

The for-each loop is structured this way:

- First the `for` keyword
- Then, the variable name we choose
- Followed by the `in` keyword and a collection to iterate over.

In this example, we told Python to run the code inside the block "for each element", where we then call the current element `food`. We then tell Python where to find these elements, which in this case is inside `groceries`. Let's break the entire process down.

At the start of the first iteration:

1. A variable `food` is set to the first value in `groceries`, `'Walnuts`. 
2. Then, we print `'I bought some Walnuts today'`, because the f-string inserts the current value of `food` into the string.
3. We then repeat the process; however, `food` is set to the second element in the list, `Grapes`.
4. The third time around, `food` is set to the last element in the list of three elements, `'Bird Seeds`, because we asked Python to run the print `for` each element in the list.

Try to implement the example in a new Python script and run it. It should look something like this:

```shell
trop3n@htb[/htb]$ vim groceries.py
trop3n@htb[/htb]$ python3 groceries.py

I bought some Walnuts today.
I bought some Grapes today.
I bought some Bird seeds today.
```

Note that in Python we can iterate over each element produced by a "generator" as well as a collection of data. We will not be covering generators in this module, because we usually don't need to worry about them when writing Python programs.

# Defining Functions

So far, we have looked at common techniques for controlling code flow, making it possible for us to build simple tools, for example, counters or even simple wordlist enricher. 

For example: for each word in the wordlist, first set the counter to 0, while the counter is less than 100, print the word and the counter and increase the counter by 1. For reference, this could look something like this:

#### Password Generation Example

```python
wordlist = ['password', 'john', 'qwerty', 'admin']

for word in wordlist:
    counter = 0
    while counter < 100:
        print(f'{word}{counter}')
        counter = counter + 1

```

In this case, the for-loop repeats the loop until it has processed all entries from the list. As shown, even with simple building blocks, we can achieve a lot. Let us talk about the following important building block in software: `Functions`.

## Functions

Functions let us define code blocks that perform a range of actions, produce a range of values, and optionally return one or more of these values. 

Like in math, where `f(x)` is a `function f of x` and produces the same result when given the same input. For example `f(x) = x + 1` is a function `f` of `x` which returns `x + 1`. Thus, `f(2)` would be `3`, because `f(2) = 2 + 1` which is 3.

Similarly, in Python, we can define and call functions to reuse code and work with our data more efficiently - as we do not need to reinvent the wheel all the time. We can define functions in Python in their simplest form very easily. 

Here is an example of defining `f(x) = 2 * x + 5` as a function in Python:

### First Function

```python
def f(x):
    return 2 * x + 5
```

Besides the (essential) syntax with indentation and the `inner scope` of the function - the code inside the function - what is important to note here are the `def` and `return` keywords. The `def` keyword is how we define functions in Python.

Following `def` comes the function name (written in snake_case), input parameters indise the parenthesis, and a colon. This first line of a function is called the *`signature` of the function.*

After having written a couple of different functions, we can tell them apart by simply looking at their names and the arguments they accept. We can tell them apart by comparing their function signatures.

Let us creates another function to calculate and return that one value to the power of another value:

### Power_Of Function

```python
def power_of(x, exponent):
    return x ** exponent

power_of(4, 2) # the function was run, but nothing caught the return value
eight = power_of(2, 3) # Variable "eight" is now equal to two-to-the-power-of-three
```

So, is the first form pointless then? No. As with the input/output of a terminal, we can "pipe" the function's output to the "input" of another. We can use the result of calling a function as the input for another one.

For example:

```python
print('My favorite number is:')
print(power_of(4, 2))
```

Here we are calling the function `print` and giving it first a string as an input, and next, we are giving it `the result` of another function call. 

At ***`runtime`***, during the script's actual execution, Python will first execute the first line and then go to the 2nd line and execute the commands from inside out. 

It will, in other words, start by calculating `power_of(4, 2)` and then use the result as input to the `print` function.

Imagine if we were to call a function with ten parameters. Having to remember each of the parameters is challenging once the amount of parameters increases above two, so in addition to these `positional` parameters, Python supports what is called **`named parameters`**. 

While Positional Parameters require us to always insert the parameters in the correct order, *named parameters let us use whichever order we prefer.* However, they require us to specify which value goes to which parameter explicitly. Using named parameters might seem silly, but after a week or a month of looking at other things, it can be a blessing to have expressly specified, by parameter names, which is which.

Let us look at an example. Consider the below function, which is a template invitation to a school event.

#### Invitation.py

```python
def print_sample_invitation(mother, father, child, teacher, event):

	# Notice here the use of a multi-line format-string: f''' text here ''' 
	
    sample text = f'''
Dear {mother} and {father}.
{teacher} and I would love to see you both as well as {child} at our {event} tomorrow evening.

Best regards,
Principal G. Sturgis
'''

	print(sample_text)
print_sample_invitation()
```

If we were just to fill out the blanks, chances are we would forget who is who within minutes, rather than weeks. Note: the above code will error because we do not provide any arguments for the `print_sample_invitation` function.

What we can do instead is to specify exactly who is who, like so:

```python
print_sample_invitation(mother='Karen', father='John', child='John', teacher='Tina', event='Pizza Party')
```

Specifying the names within the function will change our script to this:

#### Invitation.py - Modified

```python
# Defining the function
def print_sample_invitation(mother, father, child, teacher, event):

    # Notice here the use of a multi-line format-string: f''' text here '''
    sample_text = f'''
Dear {mother} and {father}.
{teacher} and I would love to see you both as well as {child} at our {event} tomorrow evening. 

Best regards,
Principal G. Sturgis.
'''
    # Print output
    print(sample_text)

# Call function
print_sample_invitation(mother='Karen', father='John', child='Noah', teacher='Tina', event='Pizza Party')
```

This will produce the following output:

#### Invitation.py - Execution

```shell-session
trop3n@htb[/htb]$ python3 invitation.py

Dear Karen and John.
Tina and I would love to see you both as well as Noah at our Pizza Party tomorrow evening.

Best regards,
Principal G. Sturgis.
```

Once again, Python scripts are executed from top to bottom, so always keep in mind that Python needs to know about the functions and variables before they are being referenced. Also, keep in mind the scopes of the code. 

*Scopes* let us reference variables and functions `outside` of our current scope (e.g. code in functions can use variables and the global scope), but not `inside` of it. 

- In other words, we cannot reuse a variable we defined inside a function, outside of it.

Besides that, Python comes with many different **[Built-in Functions](https://docs.python.org/3/library/functions.html).** 

Now that we know the basics of defining and working with functions, let us add some more building blocks to our arsenal of coding tools: `Classes`.

# Making Code Classy

In this section, we will talk about classes. And cake. Let us start with the cake. When we have a piece of brownie in front of us, let us, for the sake of argument, say this piece of brownie is an `object` of the food type `Cake`. Our piece of cake has some properties that other pieces of cake might not have. One such property could be the topping which in our case could be chocolate frosting and a cherry. We need to ask ourselves how this piece of cake was produced and what it consists of. 

Cooking recipes and classes are much alike because they define how a dish - or some object - is produced. A cake might have a fixed amount of flour and water, but leave it up to the chef to add a chocolate or strawberry frosting. 

A `class` is a spec of how an object of some type is produced. The result of `instantiating` such a `class` is an object of the class. 

Let us look at an example:

### The DreamCake Class

```python
class DreamCake:
	# Measurements are defined in grams or units
	eggs = 4
	sugar = 300
	milk = 200
	butter = 50
	flour = 250
	baking_soda = 20
	vanilla = 10

	topping = None
	garnish = None

	is_baked = False

	def __init__(self, topping='No topping', garnish='No garnish'):
		self.topping = topping
		self.garnish = garnish

	def bake(self):
		self.is_baked = True

	def is_cake_ready(self):
		return self.is_baked
```

Similar to how functions were defined using the `def` keyword, classes are defined using the `class` keyword, followed by the name of the class, in the CapWords naming convention. 

- CapWords means all words used in the name are capitalized and squeezed together, like `CapWordsArePrettyCool`.

Next up come the ingredients that produce a basic (and tasty, by the way) cake, which will never change in this example. The `topping` and `garnish` variables are set to `None` right after space. This suggests that these variables will have concrete values assigned at a later point - in this case, inside the `__init__` function of the class. This function automatically gets called by Python once a new instance of a class is requested.

The `__init__` function is a so-called *Magic Method*. We will not cover Magic Methods in detail, but a note about them has been included in the optional, advanced part at the bottom.

Getting back to the class, please notice about the `__init__` function, the `self` parameter. This parameter is a `mandatory, first` parameter *of `all` class functions*

Long story short, classes *need a way to refer to their own signature*. We can then refer to other functions within class functions by calling `self.other_func()` or `self.topping`. Note that we do not need to provide a value for it when calling functions on class objects despite the first 'self' parameter. We will see this later.

Another little trick to notice is the default values for function parameters. These allow us to completely commit specifying a value for one or more of the parameters. The parameters will - in that case - then be set to their defauly values as specified, and `topping` is set to `'No topping'` unless overridden when we create an object.

Lastly, in this example, we have defined a function `inside of the class scope` as dictated by the indentation level. This means that the function `bake` is `only` accessible to code from within the *class itself* (e.g. code inside one function calling another function) and objects instantiated from the class. Let us create some example objects to illustrate this behavior better.

### A Plain Cake

> The topping and garnish default to "No topping" and "No garnish" for a plain cake, respectively.

```Python
plain_cake = DreamCake()
```

### A Chocolate Cake

> We need to add chocolate frosting on top for a chocolate cake, but no garnish (defaults to `"No garnish"`).

```python
chocolate_cake = DreamCake(topping='Chocolate frosting')
```

### A Luxury Cake

> Our luxury cakes have the topping and garnish explicitly set.

```python
luxury_strawberry_cake = DreamCake(topping='Strawberry frosting', garnish='Chocolate bits')
```

This can, of course, also be specified `without` using named parameters for brevity:

```python
luxury_strawberry_cake = DreamCake('Strawberry frosting', 'Chocolate bits')
```

As shown above, classes are instantiated into objects similar to how we call functions: type the name followed by parenthesis with possible parameters specified. Now that we have objects of the class `DreamCake` stored in variables, we can call the functions of the class `on` the object variables by appending a `.` and the function.

### Baking the Cake

```python
chocolate_cake = DreamCake(topping='Chocolate frosting')

chocolate_cake.bake() # Call the function "bake" on the object.
is_cake_done = chocolate.cake_is_ready()

print(is_cake_done) # Prints "True" because we called "bake" earlier.
```

See the `bake()` function call on the `chocolate_cake`? Even though the `bake` function within the class has a `self` parameter, we do not need to specify its value. We will not dive into the decisions as to why this is, as it just something to remember. In closing, it is worth mentioning that this code style is a small part of [Object-Oriented Programming (OOP)](https://en.wikipedia.org/wiki/Object-oriented_programming).

There is much more to OOP than simply using classes - enough for an entirely separate module - but in the simplest forms, we define classes, create objects or instances, of the these classes and use them to hold data or call functions. 

## Advanced Notes on Classes

If you are new to programming, do not be disheartened if this sounds a little too complicated. The following are very brief notes on some more advanced usages of classes, which we mostly do not need to worry about at all in our day-to-day programming, but which are pretty cool to know about regardless.

One thing I promised to explain briefly is ***Magic Methods***. Magic Methods are functions, or methods as they are also called in many programming languages - which exist by default and have a default implementation in all classes. This is because of the `class hierarchy` in Python, where all classes inherit from a base class `object` ("object" is the name of the base class - slightly confusing perhaps.)

This statement opens a large box of OOP that we will not go through, but feel free to research **Python Class Inheritence** and similar phrases on our own. In short, ***class inheritance*** means that one class can inherit the type and its functions and internal variables. This base class gives objects some basic functionality, for example, *the ability to compare against one another* (is one cake the same as another?) or get a `string representation` of the object.

Say we have a class `Circle`, the object itself is raw data stored in memory that only Python knows how to read, but the `string representation` of a `Circle` object could be `"Circle(r=5)"` for example describing a circle with a radius of 5. ***The Magic Method*** responsible for returning a string representation of an object is `__str__`. Calling this function on an object is similar to calling `str(...)` with the object as a parameter. For example, consider the following snippet from my Python IDLE:

```python
class Circle:
	def __init__(self, radius):
		self.radius = radius

	def __str__(self):
		return f'Circle(r={self.radius})'

my_circle = Circle(5)
str(my_circle)

# 'Circle(r=5)'
```

> If we did not override the `__str__` function, the code would still work, but the output would be less meaningful:

```python
<__main__.Circle object at 0x022FFB98>'
```

The string represents a `Circle` object inside `__main__` (here, the IDLE), located at memory address `0x022FFB98`.

> Another two ***Magic Methods*** worth mentioning are the `__enter__` and `__exit__` functions, allowing us to *create classes that support using the `with` keyword*. 

The `with` keyword will enable us to specify the default functionality of a class and teardown procedures. For example, the class `C2TcpConnection` which represents a TCP connection to a C2 server. The build-up step could be initiating a socket and attempting to authenticate given input from external sources. The teardown step could include proper error handling and a guarantee of *properly closing the socket after use*. 

- This is advanced but fun and "Pythonic" coding which I recommend we research.

Let us briefly consider an example before moving on to the next section of the module.

### Class Supporting WITH Context Manager

```Python
class Foo():

	def __enter__(self):
		print("Enter...")

	def __exit__(self, type, value, traceback):
		print("...and exit.")
```

> Here a class `Foo` is defined with a simple `__enter__` and `__exit__` function, which does nothing but print a message. This allows us to use the `with` clause to "wrap" this supposed reused boilerplate code around concrete code, for example:

```python
with Foo():
	print("Hello World")
```

This prints the following to the console:

```shell-session
Enter...
Hello world!
...and exit.
```

Furthermore, we can change the with-clause to something like `with Foo() as foo`, which allows us to reference the instantiated object of `Foo` used to wrap around our code. Doing so is useful if, for example, the `Foo` class has functions we want to call from within the with-clause such as `get_connection_status` in the example of creating a `C2TcpConnection` class.

More frequent use of the with clause is `with open('path/to/file.txt', 'w' as wr`, which opens a file for writing. We can then use `wr.write('something')` to write "something" to the file. At the end of the with-clause, we do not need to close the output streams to the file - the teardown functionality in the `open` class takes care of that. 

# Introduction to Libraries

There is much more to OOP than simply using classes - enough for an entirely separate module - but in the simplest forms, we define classes, create objects or instances, of the these classes and use them to hold data or call functions. 

## Advanced Notes on Classes

If you are new to programming, do not be disheartened if this sounds a little too complicated. The following are very brief notes on some more advanced usages of classes, which we mostly do not need to worry about at all in our day-to-day programming, but which are pretty cool to know about regardless.

One thing I promised to explain briefly is ***Magic Methods***. Magic Methods are functions, or methods as they are also called in many programming languages - which exist by default and have a default implementation in all classes. This is because of the `class hierarchy` in Python, where all classes inherit from a base class `object` ("object" is the name of the base class - slightly confusing perhaps.)

This statement opens a large box of OOP that we will not go through, but feel free to research **Python Class Inheritence** and similar phrases on our own. In short, ***class inheritance*** means that one class can inherit the type and its functions and internal variables. This base class gives objects some basic functionality, for example, *the ability to compare against one another* (is one cake the same as another?) or get a `string representation` of the object.

Say we have a class `Circle`, the object itself is raw data stored in memory that only Python knows how to read, but the `string representation` of a `Circle` object could be `"Circle(r=5)"` for example describing a circle with a radius of 5. ***The Magic Method*** responsible for returning a string representation of an object is `__str__`. Calling this function on an object is similar to calling `str(...)` with the object as a parameter. For example, consider the following snippet from my Python IDLE:

```python
class Circle:
	def __init__(self, radius):
		self.radius = radius

	def __str__(self):
		return f'Circle(r={self.radius})'

my_circle = Circle(5)
str(my_circle)

# 'Circle(r=5)'
```

> If we did not override the `__str__` function, the code would still work, but the output would be less meaningful:

```python
<__main__.Circle object at 0x022FFB98>'
```

The string represents a `Circle` object inside `__main__` (here, the IDLE), located at memory address `0x022FFB98`.

> Another two ***Magic Methods*** worth mentioning are the `__enter__` and `__exit__` functions, allowing us to *create classes that support using the `with` keyword*. 

The `with` keyword will enable us to specify the default functionality of a class and teardown procedures. For example, the class `C2TcpConnection` which represents a TCP connection to a C2 server. The build-up step could be initiating a socket and attempting to authenticate given input from external sources. The teardown step could include proper error handling and a guarantee of *properly closing the socket after use*. 

- This is advanced but fun and "Pythonic" coding which I recommend we research.

Let us briefly consider an example before moving on to the next section of the module.

### Class Supporting WITH Context Manager

```Python
class Foo():

	def __enter__(self):
		print("Enter...")

	def __exit__(self, type, value, traceback):
		print("...and exit.")
```

> Here a class `Foo` is defined with a simple `__enter__` and `__exit__` function, which does nothing but print a message. This allows us to use the `with` clause to "wrap" this supposed reused boilerplate code around concrete code, for example:

```python
with Foo():
	print("Hello World")
```

This prints the following to the console:

```shell-session
Enter...
Hello world!
...and exit.
```

Furthermore, we can change the with-clause to something like `with Foo() as foo`, which allows us to reference the instantiated object of `Foo` used to wrap around our code. Doing so is useful if, for example, the `Foo` class has functions we want to call from within the with-clause such as `get_connection_status` in the example of creating a `C2TcpConnection` class.

More frequent use of the with clause is `with open('path/to/file.txt', 'w' as wr`, which opens a file for writing. We can then use `wr.write('something')` to write "something" to the file. At the end of the with-clause, we do not need to close the output streams to the file - the teardown functionality in the `open` class takes care of that. 

# Introduction to Libraries

We have discussed how to create classes and functions, functions with classes, and other simple concepts. All of this has been inside one Python file, also known as a `module`, but it would be great if we could share the code inside this module with other people or reuse it in other projects. It would also be great to reuse code that other people have made for us, for example, code that lets us communicate with web servers or even something as simple as getting the current date. Enter: `libraries`.

A `library` in programming is in many ways similar to a library in real life. It is a collection of knowledge that we can borrow in our projects without reinventing the wheel. Once we `import` a library, we can use everything inside it, including functions and classes. Some libraries ship along with Python, for example, `datetime`, which lets us get an object representing the current, local date, and time.

Let us see what classes and functions the library `datetime` contains. For that, we will use the built-in function called `dir()`. ([dir()](https://docs.python.org/3/library/functions.html#dir)).

## Dir(datetime)

```python
import datetime
dir(datetime)

['MAXYEAR', 'MINYEAR', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', 'date', 'datetime', 'datetime_CAPI', 'sys', 'time', 'timedelta', 'timezone', 'tzinfo']
```

### `dir()` from Python.docs

Without arguments, return the list of name sin the current local scope. With an argument, attempt to return a list of valid attributes for that object. 

If the object has a method named `__dir__()`, this method will be called and must return the list of attributes. This allows objects that implement a custom `__getattr__()` or `__getattribute__()` function to customize the way `dir()` reports their attributes.

If the object does not provide `__dir__()`, the function tries it's best to gather information from the object's `__dict__` attribute, if defined, and from its type object. The resulting list is not necessarily complete and may be inaccurate when the object has a custom `__getattr__()`.

The default [`dir()`](https://docs.python.org/3/library/functions.html#dir "dir") mechanism behaves differently with different types of objects, as it attempts to produce the most relevant, rather than complete, information:

- If the object is a module object, the list contains the names of the module’s attributes.
    
- If the object is a type or class object, the list contains the names of its attributes, and recursively of the attributes of its bases.
    
- Otherwise, the list contains the object’s attributes’ names, the names of its class’s attributes, and recursively of the attributes of its class’s base classes.
    

The resulting list is sorted alphabetically. For example:

```python
import struct

dir()   # show the names in the module namespace  
['__builtins__', '__name__', 'struct']

dir(struct)   # show the names in the struct module 
['Struct', '__all__', '__builtins__', '__cached__', '__doc__', '__file__',
 '__initializing__', '__loader__', '__name__', '__package__',
 '_clearcache', 'calcsize', 'error', 'pack', 'pack_into',
 'unpack', 'unpack_from']

class Shape:

    def __dir__(self):

        return ['area', 'perimeter', 'location']

s = Shape()

dir(s)
['area', 'location', 'perimeter']
```

### The `datetime` Library

```python
import datetime

now = datetime.datetime.now()
print(now) # Prints: 2021-03-11 17:03:48.937590
```

As we see, we have to call `datetime.datetime.now()` to get the current timestamp. We import the library, or `module`, `datetime`, which then becomes available to reference by name. This module is also called `datetime`, which contains a `now()` function, we first have to reference the module, then the class, and finally the function, all "chained together" to speak with dots. 

This may become cumbersome and clutter the code, so let us look at an alternate way of importing:

```python
from datetime import datetime

print(datetime.now())
```

### Giving it a New Name

```python
from datetime import datetime as dt

print(dt.now())
```

The above example contains two newlines between the import statement and the code. This is because the PEP-8 style guide, Python's guidelines for "correct" Python, urges developers to add two new lines between import statements and the actual code. It also suggests using the CapWords convention for class names but notes a separate style guide for built-in names. See [https://www.python.org/dev/peps/pep-0008/#class-names](https://www.python.org/dev/peps/pep-0008/#class-names) for more information. This is why classes such as `datetime` are in lowercase.

Next up, we will dive deeper into how to install and manage external libraries in Python.

# Managing Libraries in Python

The most popular way of installing external packages in Python is using [pip](https://pip.pypa.io/en/stable/). According to the author, `pip` is short for ["pip installs packages"](https://ianbicking.org/blog/2008/10/pyinstall-is-dead-long-live-pip.html), a recursive abbreviation (meaning the definition refers to the abbreviation, and thus circles itself). Very funny indeed. 

Regardless, `pip` us the name of the Python module that manages external Python packages. With `pip`, we can install, uninstall and upgrade Python packages. Unlike downloading and installing plugins for a browser or text editor, it is not common to "go shopping" for Python packages. 

Programming *is all about using the right tool for the job, so do not worry about finding packages to install*. The right approach, and probably also the one most common, is finding out `how to do something` and getting package recommendations along the way. The documentation of these packages - their websites most of the time - will typically show examples of installing the package for first-time users. Let us look at how to manage packages as well.

Some valuable arguments for `pip` that we will look at are `install` and `--upgrade` flag, `uninstall` and `freeze`. 

- The `install` argument lets users install new packages or upgrade existing packages to the latest version (if the `--upgrade` parameter is provided). 
- The `uninstall` argument will, as its name suggest, remove the package from the system.
- Surprisingly the `freeze` command has nothing to do with halting anything or cheesy police movies. It prints a list of all the installed (via pip) packages and *their dependencies*.

We can call the commands either using `pip` directly or as a Python module. Below are some examples of how this might look.

```bash
trop3n@htb[/htb]$ # Syntax: python3 -m pip install [package]
trop3n@htb[/htb]$ python3 -m pip install flask

Collecting flask
  Using cached Flask-1.1.2-py2.py3-none-any.whl (94 kB)
Collecting Werkzeug>=0.15
  Using cached Werkzeug-1.0.1-py2.py3-none-any.whl (298 kB)
Collecting itsdangerous>=0.24
  Using cached itsdangerous-1.1.0-py2.py3-none-any.whl (16 kB)
Collecting click>=5.1
  Using cached click-7.1.2-py2.py3-none-any.whl (82 kB)
Collecting Jinja2>=2.10.1
  Downloading Jinja2-2.11.3-py2.py3-none-any.whl (125 kB)
     |████████████████████████████████| 125 kB 7.0 MB/s 
Collecting MarkupSafe>=0.23
  Downloading MarkupSafe-1.1.1-cp39-cp39-macosx_10_9_x86_64.whl (16 kB)
Installing collected packages: Werkzeug, itsdangerous, click, MarkupSafe, Jinja2, flask
Successfully installed Jinja2-2.11.3 MarkupSafe-1.1.1 Werkzeug-1.0.1 click-7.1.2 flask-1.1.2 itsdangerous-1.1.0
```

As can be seen, even through we only asked to install `flask`, a brilliant package for running Python-based web servers (as is `bottle`-same-same, but different), we get a multitde of other packages as well, which are all requirements of `flask`. We could try to upgrade it, but we are already told that we are already running the latest version.

### Upgrading Packages

```shell-session
trop3n@htb[/htb]$ python3 -m pip install --upgrade flask

Requirement already up-to-date: flask in /usr/local/lib/python3.9/site-packages (1.1.2)
Requirement already satisfied, skipping upgrade: itsdangerous>=0.24 in /usr/local/lib/python3.9/site-packages (from flask) (1.1.0)
Requirement already satisfied, skipping upg...
<SNIP>
```

> If we wanted to uninstall a particular package, we could do so by calling:

### Uninstalling Packages

```shell-session
trop3n@htb[/htb]$ pip uninstall [package]
```

Let us see what is currently installed by running `pip` with the `freeze` argument. As some of them are dependencies of `flask`, we will leave the uninstallation itself as "extras". Please note that if we choose to *uninstall a dependency package*, the primary package likely will not work. Also, note that `freeze` may produce different outputs from machine to machine and Python version to Python version.

### Listing the Installed Packages

```shell
trop3n@htb[/htb]$ # Syntax: python3 -m pip freeze [package]
trop3n@htb[/htb]$ python3 -m pip freeze

click==7.1.2
Flask==1.1.2
itsdangerous==1.1.0
Jinja2==2.11.3
MarkupSafe==1.1.1
protobuf==3.13.0
pynput==1.7.3
pyobjc-core==7.1
pyobjc-framework-Cocoa==7.1
pyobjc-framework-Quartz==7.1
six==1.15.0
Werkzeug==1.0.1
```

The list of installed packages would be nice to be given to another person to either use our scripts or help with development. This way, they will know which packages need to be installed (and which versions even).

It just so happens to be the case that `pip` supports maintaining packages from a requirements file. This file, often called literally `requirements.txt`, contains a list of all the required packages needed to run the script successfully. The format is quite simple. We would copy the above `freeze` output and save it as a requirements file. However, it is a little bloated, and we do not need to know or even list the dependencies of the packages we need.

For the sake of an example, let us suppose that we would like to use `flask` and `click` (we will return to `click` later). If we do not know the version requirements or do not mind, either way, we could list the packages one after the other and save them, like so:

#### Example Requirements

```shell
trop3n@htb[/htb]$ cat requirements.txt

flask
click
```

Then, to install all the packages in the requirements file, we would type:

#### Install from requirements.txt

```shell-session
trop3n@htb[/htb]$ python3 -m pip install -r requirements.txt
```

This will then go through each of the requirements and install them by selecting the latest available and permitted version. Say we explicitly wanted `flask` version 1.1.2. All we had to do was replace `flash` with `flask==1.1.2` in the requirements file, just like the `pip freeze` command output. Below is a list of common version comparison operators that we are highly likely to come across in larger Python projects. 

| Comparison Operator | Description                         |
| ------------------- | ----------------------------------- |
| `==`                | Version matching clause             |
| `<= />=`            | Inclusive ordered comparison clause |
| `< / >`             | Exclusive ordered comparison clause |
They let us specify, in the requirements file, our exact requirements to versions. For example, if we know that some package `xyz` is vulnerable to exploitation at versions 1.0.4 and lower, we can specify in our requirements that the file we need `xyz>=1.0.5`.

It is pretty common for new updates to break the current code (e.g.) packages that rely on other third-party systems like **Discord bot API for Python**. In these cases, we can force an older version of a package. At the same time, the needed change were being worked on with the `<` or `<=` operator. 

To not dig too deep into it right from the start, we will return to this topic later in the module. For now, let us move on with some pre-requisites for our first project.

# The Importance of Libraries


Now that we  know how important libraries can be for our development and how to manage them let us discuss two of the more popular ones that we will use in our project, starting with the `requests` library.

## The Requests Package

The [requests](https://requests.readthedocs.io/en/master/) library is an elegant and simple HTTP library for Python. From the documentation:

> [!NOTE]
> Requests allow you to send HTTP/1.1 requests extremely easily. There's no need to manually add query strings to your URLs, or to form-encode your POST data. Keep-alive and HTTP connection pooling are 100% automatic, thanks to urlilb3.

Let us install requests just like we have learned.

### Installing requests

```shell
trop3n@htb[/htb]$ python3 -m pip install requests

Collecting requests
  Downloading requests-2.25.1-py2.py3-none-any.whl (61 kB)
     |████████████████████████████████| 61 kB 3.8 MB/s
Collecting chardet<5,>=3.0.2
  Downloading chardet-4.0.0-py2.py3-none-any.whl (178 kB)
     |████████████████████████████████| 178 kB 6.8 MB/s
Collecting certifi>=2017.4.17
...SNIP...
Successfully installed certifi-2020.12.5 chardet-4.0.0 idna-2.10 requests-2.25.1 urllib3-1.26.3
```

Once installed, we can import the library into our code by typing `import requests` and then use it right away. 

The two most useful things to know about the requests library are making HTTP requests, and secondly, it has a `Session` class, which is useful when we need to maintain a certain context during our web activity. For example, if we need to keep track of a range of cookies, we could use a `Session` object. To get one of these, we `import requests` and create an object of the `Session` class like `sess = requests.Session()`. Alternatively, we can use the `requests` module (the library itself) to make HTTP requests. However, this will not keep it's state automatically.

Consider the following code:

### Example of Requests

```python
import requests

resp = requests.get('http://httpbin.org/ip')
print(resp.content.decode())

# Prints:
# {
#   "origin": "X.X.X.X"
# }
```

This is a simple example of how to perform a GET request to obtain our public IP address. Since the `resp.content` variable is a `byte-string` with the `decode()` function and no parameters tell Python to interpret the bytes as UTF-8 characters. UTF-8 is the *default encoding used when no other encoding is specified*.

However, other encodings can be used and set as parameter arguments to the `decode()` function, for example, `decode(encoding='UTF-16')`. Going back to the `resp` object, this contains useful information such ass the `status_code`, the numeric HTTP status code of the request we made, and cookies. We will use this library later on, but for now, let us move on with some fore food talk.

## The BeautifulSoup Package

Another handy package is the BeautifulSoup library (rather `beautifulsoup4`). This library makes working with HTML a lot easier in Python. Before, we learned how to query a website and get output back, which could be the raw HTML. Digging through this HTML can be cumbersome if we have to search through textual output by hand. BeautifulSoup turns the HTML into Python objects that are much easier to work with and allows us to analyze the content better programmatically. Let us install BeautifulSoup.

### Installing BeautifulSoup

```shell-session
trop3n@htb[/htb]$ python3 -m pip install beautifulsoup4

Collecting beautifulsoup4
  Downloading beautifulsoup4-4.9.3-py3-none-any.whl (115 kB)
     |████████████████████████████████| 115 kB ...
Collecting soupsieve>1.2
  Downloading soupsieve-2.2-py3-none-any.whl (33 kB)
Installing collected packages: soupsieve, beautifulsoup4
Successfully installed beautifulsoup4-4.9.3 soupsieve-2.2
```

> Once installed, let's go through some quick examples of how to use `BeautifulSoup`. For a more in-depth walkthrough, please visit the [documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/). For now, please consider the below code:

### HTML - Ugly Format

```html
<html>
<head><title>Birbs are pretty</title></head>
<body><p class="birb-food"><b>Birbs and their foods</b></p>
<p class="food">Birbs love:<a class="seed" href="http://seeds" id="seed">seed</a>
   and 
   <a class="fruit" href="http://fruit" id="fruit">fruit</a></p>
 </body></html>
```

This HTML looks a little messy. We will assume that this HTML is stored in a variable `html_doc`. We'll then load this into BeautifulSoup and print it in a nicely formatted way, as follows:

### Example of BeautifulSoup

```python
from bs4 import BeautifulSoup

html_doc = """ html code goes here """
soup = BeautifulSoup(html_doc, 'html.parser')
print(soup.prettify())
```

> which then prints:

```html
<html>
 <head>
  <title>
   Birbs are pretty
  </title>
 </head>
 <body>
  <p class="birb-food">
   <b>
    Birbs and their foods
   </b>
  </p>
  <p class="food">
   Birbs love:
   <a class="seed" href="http://seeds" id="seed">
    seed
   </a>
   and
   <a class="fruit" href="http://fruit" id="fruit">
    fruit
   </a>
  </p>
 </body>
</html>
```

The import statement of BeautifulSoup is worth noticing. Because the class `BeautifulSoup` lies within the module `bs4` we will usually import it this way. What happens in the code is that the class is imported from the module, and then we create a new BeautifulSoup object and set the parser of the class to the HTML parser of BeautifulSoup. We need to set this parser when loading HTML.

Let us not delve too long into thought-up example and instead move straight to the implementation of our final product: the word extractor.

# The First Iteration

We will start implementing the program little by little, always ensuring that we reach a milestone where the code works, even though it may not be entirely complete yet. Even if we have a firm idea of how the code will be implemented and what it will look like in the end, it is still a good idea to *take it slow and build things up layer by layer*.

Since we want to end up with a program that can fetch all words of a webpage and perhaps also have a few other features, let us first write the code needed to do the most basic task: printing the HTML of a webpage. In short, this is what we should be aiming for:

- The code will download and print the entire HTML of a webpage.
- The URL of the webpage is fixed inside the code.
- We will write the code in its simplest form and rewrite bits and pieces as needed when we need to.
- We will use the `requests` library.

### Printing Webpage Source Code

```python
import requests

PAGE_URL = 'http://target:port'

resp = requests.get(PAGE_URL)
html_str = resp.content.decode()
print(html_str)
```

> Now what happens if we misspell the URL? Let's try it out in Python interactive terminal and see:

```python
>>> r = requests.get('http://target:port/missing.html')
>>> r.status_code

404
>>> print(r.content.decode())

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
        "http://www.w3.org/TR/html4/strict.dtd">
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html;charset=utf-8">
        <title>Error response</title>
    </head>
    <body>
        <h1>Error response</h1>
        <p>Error code: 404</p>
        <p>Message: File not found.</p>
        <p>Error code explanation: HTTPStatus.NOT_FOUND - Nothing matches the given URI.</p>
    </body>
</html>
```

