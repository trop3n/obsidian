**Module 1: Introduction to Python Programming in Cybersecurity**
>> basics of programming
>> data types
>> variables
>> conditional statements
>> iterative statements

***Python and Cybersecurity

Python is considered a general purpose programming language.

**Advantages of Python
- Resembles human language
- Less code
- Easy to read
- Standard guidelines
- Online support
- Built-in code

***Get to know Python
>> How programming works
>> how a computer processes the Python programming language
>> how Python is used in cybersecurity

***How Programming Works
>> Programming is a process that can be used to create a specific set of instructions for a computer to execute tasks. Computer programs exist everywhere. Computers, cell phones, and many other electronic devices are all given instructions by computer programs.

Using Python to Program

>> Python can be used to create websites, perform data analysis, and automate tasks.

- Python code must be converted through an interpreter before the computer can process it.

- An interpreter is a computer program that translates Python code into runnable instructions line by line


Python Versions

- There are multiple versions of Python, in this course we are learning Python 3. 
- Syntax is different in each version of Python


Python in Cybersecurity

- Python is used especially for automation. Automation is the use of technology to reduce human and manual effort to perform common and repetitive tasks.
    

>> Specific areas of cybersecurity that can be automated with Python:

- Log analysis
    
- Malware analysis
    
- Access control list management
    
- Intrusion detection
    
- Compliance checks
    
- Network scanning
    

**Create a Basic Python Script**

>> Comment

- A note programmers make about the intention behind their code
    
- Comments start with the hash symbol (#)
    

>> Print

- Outputs a specified object to the screen
    
- String data must be placed in quotation marks
    

>> Syntax

- The rules that determine what is correctly structured in a computing language
    
Python Environments

>> Python can be ran through a variety of environments. These environments include notebooks, integrated development environments, and the command line. 

- This course will primarily focus on notebooks

Notebooks

>> A notebook is an online interface for writing, storing and running code.

- Also allow you to document information about the code. Notebook content either appears in a code cell or markdown cell.

**Code Cells

>>Code cells are meant for writing and running code. A notebook provides a mechanism for running these code cells.

**Markdown Cells

markdown cells are meant for describing the code. They allow you to format text in the markdown language. 

- Markdown language is used for formatting plaintext in text editors and code editors. For example, you might indicate that text should be in a certain header style

**Common Notebook Environments

> Two common notebook environments are Jupyter Notebook and Google Colaboratory
>> 
>> They allow you to run several programming languages, including Python

### Integrated Development Environments

> Software applications for writing code that provides editing assistance and error correction tools. Integrated development environments include a graphical user interface *(GUI)* that provides programmers assistance with a variety of options to customize and build their programs.

### Command Line Interface
> Python can also be run in the command line interface. 
>> you can enter commands into the command line to access files, including Python files you want to run
>
>

***

# Data Types in Python

**Data Type
- category for a particular type of data item

**String Data
- data consisting of an ordered sequence of characters
- letters, symbol, spaces and numbers
	- numbers cannot be used for math in strings, and must be in quotes

**Float Data
- Number with a decimal point

**Integer Data
- Data consisting of a number that does not include a decimal point

**Boolean Data
- Data that can only be one of two data, true or false

**List Data
- Data structure that consists of a collection of data in sequential form

# More About Data Types
> Expand on data types, and introduce three additional types.

**String

> string data consists of an ordered sequence of characters. 
>> characters may include letters, numbers, symbols and spaces, and must be placed within quotation marks

**List

> List Data is a data structure that consists of a collection of data in sequential form. List elements can be of any data type, such as strings, integers, booleans or even other lists.
- Elements of a list are placed with square brackets, and each element is separated by a comma.

```
[12, 36, 54, 1, 7]

["eerab", "arusso", "drosas"]

```

**Note**: an empty list is a list with [] that do not contain any code.

**Integer

> data consisting of a number that does not include a decimal point. 

- Integers are not placed in quotes.
- the Print function can also be used to perform mathematical operations with integers. 

**Float**
> Float Data is data consisting of a number with a decimal point.

-  Just like integer data, float data is not placed in quotes. In addition, you can use the print function to display float data or to perform mathematical calculations with float data. 
- If you want to return a whole number instead of a decimal, you would use the // symbols instead. 
	- It will round down to the nearest whole number.

**Boolean**
> Boolean data is data that can only be one of two whole values: either True or False

- Boolean values are not placed in quotation marks.
- Booleans can also be returned by comparing numbers with operators. 

### **Additional Data Types**

**Tuple**
> Tuple data is a data structure that consists of a collection of data that cannot be changed. Like lists, tuples can contain elements of varying data types.

> A difference between tuple data and list data is that it is possible to change the elements in a list, but it is not possible to change the elements in a tuple. 
>> This could be useful in a cybersecurity context.
>>> If software identifiers are stored in a tuple to ensure they will not be altered, this can provide assurance that an access control list will only block the intended software.

Tuple are placed in parenthesis rather than brackets, like lists are. 
-  These are examples of tuples:
```
	- ("wjaffrey", "arutely", "dkot")
	- (46, 2, 13, 2, 8, 0, 0)
```

**Pro Tip:**
Tuples are more memory efficient than lists, so they are useful when you are working with a large quantity of data. 

**Dictionary:**
> Dictionary data is data that consists of one or more key-value pairs. Each key is mapped to a value.
>> A colon (:) is placed between the key and the value. Commas separate key value pairs from other key value pairs, and the dictionary is placed within curly brackets. ({})

> Dictionaries are useful when you want to store and retrieve data in a predictable way. For example, the following dictionary maps a building name to a number. The building name is the value, and the number is the key.

```
{ 1: "East"
  2: "West"
  3: "North"
  4: "South" }
  
```

**Set**
> Set data is data that consists of an unordered collection of unique values. This means no two values in a set can be the same. 

> Elements in a set are always placed within curly brackets and are separated by a comma. These elements can be of any data type.

```
{"jlanksy", "drosas", "nmason"}
```

## Working with Variables in Python

**Variable**
-  A container that stores data.
-  Creating a variable is often called "Assignment"
-  Purpose of creating variables is so they can be used later in the code.
	-  Referring to a variable is called "calling"

type()
-  returns the data type of its input

## Assign and Reassign Variables in Python
> Learn the general practice of naming variables so that you can avoid syntax errors and improve code readability.

**What Are Variables**
> a **variable** is a container that stores data.
>> It's a named storage location in a computer's memory that can hold a value. 

-  It can store a particular data type, such as an integer, string, or Boolean. 
-  The value that is stored in a variable can change.

##### **Working With Variables**
> It's important to know both how to assign a variable and how to change them

**Assigning and Reassigning Variables**
> If you want to create a variable called username and assign it a value of "nzhao", place the variable to the left of the equals sign and its value to the right.

```
# Assign 'username'
username = "nzhao"
```

> If you later want to reset this username to "zhao2", you still refer to that variable container as username.

```
# Reassign 'username'
username = "zhao2"
```

**Assigning Variables to Variables**
> In a similar process, you can also assign variables to other variables. In the following example, the variable `username` is assigned to a new variable `old_username`. 

```
# Assign a variable to another variable
username = "nzhao"
old_username = username
```

> Because `username` contains the string value of `"nzhao"`, and `old_username` contains the value of `username`, `old username` now contains a value of `"nzhao"`

**Best Practice for Naming Variables**

-  Use only letters, numbers and underscores in variable names. 
-  Start a variable name with a letter or underscore
-  Remember that variable names in Python are case-sensitive
-  Don't use Python's built in keywords or functions for variable names. 

Additionally, you should follow these stylistic guidelines to make your code easier for you and other security analysts to read and understand:

-  Separate two or more words with underscores. `login_attempts`, `invalid_user`
-  Avoid variables with similar names. These variables could easily get confused with one another: `start_time`, `starting_time`
-  Avoid unnecessarily long names for variables. 
-  Names should describe the data  and not be random words. 

## Conditional and Iterative Statements

**Conditional Statement
-  A statement that evaluates code to determine if it meets a specified set of conditions

	**If
	-  starts a conditional statement
	-  end of If statement is always followed by a colon
		-  the statement is indented after the if statement

**Operators**

-  >
-  <
-  >=
-  <=
-  == evaluates if two objects match
-  != not equals

### More on Conditionals in Python
> Review these and learn another keyword, `elif`. Apply the `not`, `and`, `or` operations to conditions

**How Conditional Statements Work**
> a conditional statement is a statement that evaluates code to determine whether it meets a specific set of conditions. When a condition is met, it evaluates to a Boolean value of `true` or `false` if the condition is not met.


| operator | use                      |
| -------- | ------------------------ |
| >        | greater than             |
| <        | less than                |
| >=       | greater than or equal to |
| <=       | less than or equal to    |
| ==       | equal to                 |
| !=       | not equal to             |
**If Statements**
> The keyword `if` starts a conditional statement. It's a necessary component of any conditional statement. 

> The first line of code is the header. In the header of an `if` statement, the keyword `if`is followed by the condition. 

```
if (status == 200)
	print("OK")
```

-  Parenthesis are not necessary around conditions in Python, though it could help with code readability. 

**The Body of an If Statement**
> After the header of an `if` statement comes the body of the `if `statement. This tells Python what action or actions to perform when the condition evaluates to `True`. 

> In this example, there is just one action, printing `"OK"` to the screen. 

**Continuing Conditionals with Else and Elif**

> It's possible to specify alternative actions with `else` and `elif`

**Else Statements**

> The keyword `else` precedes a code section that only evaluates when all conditions that precede it within the conditional statement evaluate to false.

```
if status == 200:
	print("OK")
else:
	print("check other status")
```

**elif statements**

> In some cases, you might have multiple alternative actions that depend on new conditions. In that case, you can use `elif`. The `elif` keyword precedes a condition that is only evaluated when previous conditions evaluate to `false`. 
>>Unlike with `else`, there can be multiple `elif` statements following `if`

```
if status == 200:
	print("OK")
elif status == 400:
	print("Bad Request")
elif status == 500:
	print("Internal Server Error")
```

> If you want the code to print another message when all conditions evaluate to `False`, then you can incorporate `else` after the last `elif`. In this example, if it reaches the `else` statement, it prints a message to check the status.

```
if status == 200:
	print("OK")
elif status == 400:
	print("Bad Request")
elif status == 500:
	print("Internal Server Error")
else:
	print("check other status")
```

**Logical Operators for Multiple Conditions**

> In some cases, you might want Python to perform an action based on a more complex condition. You might require two conditions to evaluate to `True.` 
> Or, you might require only one of two conditions to evaluate to `True`. 
> Or, you want Python to perform an action when a condition evaluates to `False`. 
> The operators `and`,`or`, and `not` can be used in these cases.

**and**

> The `and` operator requires both conditions on either side of the operator to evaluate to `True`. For example, all HTTP status response codes between `200` and `226` relate to successful responses. You can use `and` to join a condition of being greater than or equal to `200` with another condition being less than or equal to `226`:

```
if status >= 200 and status <= 226:
	print("successful response")
```

**or**

> The `or` operator requires only one of the conditions on either side of the operator to evaluate to `True`. For example, both a status code of `100` and a status code of `102` are informational responses. Using `or`, you could ask Python to print `informational response` message when the code `100` or `102`

```
if status == 100 or status == 102:
	print("informational message")
```

Only one of these conditions needs to be met for Python to print the message.

**not**

> the `not` operator negates a given condition so that it evaluates to `False` if the condition is `True` and to `True` if it is `False`

```
if not status >= 200 and status <= 226
	print("check status")
```

> Python checks whether the value of status is greater than or equal to `200` and less than or equal to `226` and then because of the operator `not`, it inverts this.

### For Loops

> **Iterative statements**: code that repeatedly completes a set of instructions.
> - Also referred to as loops.
> 	- Setting up a loop allows us to repeatedly use a line of code without having to type it multiple times. 

**Types of Loops**
-  For loops
-  While loops

**for loops** repeat code for a specified sequence
> `for` signifies the beginning of a for loop
> - Loop header, and a loop body, similar to conditional statements

```
for i in [1, 2, 3, 4]
	print(i)
1
2
3
4
```
> in for loops, the temporary variable, in this case, `i`, is only used within the loop and not outside of it with the rest of the code.

-  Another important process of for loops is to repeat a specific process a set number of times.

`range()` generates a sequence of numbers
-  `range(0, 10)` goes from 0 to 9
-  the number at the end of the range tells us where to stop, then is excluded. 
-  if a start point is not defined, the range always starts at 0.

### While Loops

> While loops still repeatedly execute, but this repetition is based on a condition.
> - When the condition becomes false, the while loop will stop. 

> With `while` loops, the variable isn't created within the loop statement itself, as with `for` loops.
> 	- Before writing the while loop, you need to assign the variable.
> 	- 

### More on Loops in Python

> If you want a loop to iterate based on a condition, you should use a `while` loop. 
> As long as the condition is `True`, the loop continues, but when it evaluates to `False`, the `while` loop exits. 

**Boolean Values in the Loop Condition**

> Conditions in `while` loops can also depend on other data types, including comparisons of Boolean data. In Boolean data comparisons, your loop condition can check whether a loop variable equals a value like `True` or `False`. The loop iterates an indeterminate amount of times until the Boolean condition is no longer `True`. 

```
count = 0
login_status = True
while login_status == True:
	print("Try again.")
	count = count + 1
	if count == 4:
		login_status = False
```

**Managing Loops**

> You can use `break` and `continue` keywords to further control your loop iterations. Both are incorporated into a conditional statement within the body of the loop. 
> They can be inserted to execute when the condition in an `if` statement is `True`. The `break` keyword is used to break out of a loop. 
> The `continue` keyword is used to skip and iteration and continue with the next one.

**break**

> When you want to exit a `for` or `while` loop based on a particular condition in an `if ` statement being `True`, you can write a conditional statement in the body of the loop and write the keyword `break` in the body of the conditional.

```
computer_assets = ["laptop1", "desktop20", "smartphone03"]

for asset in computer_assets:

    if asset == "desktop20":

        break

    print(asset)
```
> This will only print `laptop1` since the break ends the loop after the variable becomes equal to `desktop20`

**continue**

> When you want to skip an iteration based on a certain condition in an `if` statement being `True`, you can add the keyword `continue` in the body of a conditional statement within the loop. 

```
computer_assets = ["laptop1", "desktop20", "smartphone03"]

for asset in computer_assets:

    if asset == "desktop20":

        continue

    print(asset)
```
> This will print `laptop1` and `smartphone03` because the `continue` keyword makes the loop skip the `desktop20` part of the loop. 

**Infinite Loops**

> If you create a loop that doesn't exit, this is called an infinite loop. In these cases, you should press `ctrl-c` or `ctrl-z` on your keyboard to stop the infinite loop. 
> You might need to do this when running a service that constantly processes data, like a web server. 

## Introduction to Functions

**What we'll learn:
-  functions
-  modules and libraries
-  code readability

**Function**
> a section of code that can be reused in a program

**Built-in Functions**
> functions that exist within Python and can be called directly

**User-defined Functions**
> functions designed by users for their specific needs

`def`
*  placed before a function to define it

### **Python Functions in Cybersecurity**

> a **function** is a section of code that can be reused in a program. Functions are important in Python because they allow you to automate repetitive parts of your code.
> In cybersecurity, you will likely adopt some processes that you will often repeat.

> When working with security logs, you will often encounter tasks that need to be repeated. 
> For example, if you were responsible for finding malicious login activity based on failed login attempts, you might have to repeat the process for multiple logs.

> To work around that, you could define a function that takes a log as its input and returns all potentially malicious logins. It would be easy to apply this function to different logs. 

**Defining a Function**

> Python has user-defined functions and built-in functions, both of which you will use frequently. 

> the `def` keyword is placed before a function name to define a function

> **Note**: when naming a function, give it a name that indicates what it does. This will make it easier to remember when calling it later. 

**Function Body**

> The function body is an indented block of code after the function header that defines what the function does. The indentation is very important when writing a function because it separates the definition of a function from the rest of the code.

```
def display_investigation_message():
	print("investigative activity")
```

**Calling a Function**
> After defining a definition, you can use it as many times as needed in your own code. 
> Using a function after defining it is referred to as calling a function. 
> To call a function, write its name followed by parenthesis.
```
display_investigation_message()
```

### Work With Functions

**Parameter (Python)**
> an object that is included in a function definition for use in that function

-  Python's built-in range function uses parameters, to iterate through a list of numbers from a start and end point. 

**Return Statement**
> a Python statement that executes inside a function and sends information back to the function call.

**Parameters**
> a parameter is an object that is included in a function definition for use in that function.
> When you define a function, you create variables in the function header. They can be used in the body of the function. In this context, these variables are called parameters.

```
def remaining_login_attempts(maximum_attempts, total_attempts):
	print(maximum_attempts - total attempts)
```
> this function takes in two variables, `maximum_attempts` and `total_attempts` and uses them to perform a calculation.

**Arguments**
> In Python, an argument is the data brought into a function when it is called.

```
remaining_login_attempts(3, 2)
```
> the **arguments** in this code are the integers 3 and 2.

> These integers pass into the function through the parameters that were identified when defining the function. In this case, those parameters would be `maximum_attempts` and `total_attempts`. 3 is in the first position, so it passes into `maximum_attempts`. Similarly, 2 is in the second position and passes into `total_attempts`.

**Return Statements**
> When defining function in Python, you use return statements if you want the function to return output. The `return` keyword is used to return information from a function.

>The `return` keyword appears in front of the information that you want to return.
>In the following example, it is before the calculation of how many login attempts remain:
```
def remaining_login_attempts(maximum_attempts, total_attempts):
	return maximum_attempts - total attempts

```
> When Python encounters a `return` statement, it executes this statement and then exits the function. If there are lines of code that follow the `return` statement within the function, they will not be run. 

**Global and Local Variables**
> To better understand how functions interact with variables, you should know the difference between global and local variables. 

> When defining and calling functions, you're working with local variables, which are different from the variables you define outside the scope of a function.

**Global Variables**
> A **global variable** is a variable that is available through the entire program. 
> Global variables are assigned outside of a function definition.

For example, you might assign the following variable at the beginning of your code:

`device_id = 7ad2130bd`

Throughout the rest of the code, you will be able to modify the `device_id` variable in conditionals, loops, functions and other syntax. 

**Local Variables**
> a **local variable** is a variable assigned within a function.
> These variables cannot be called or accessed outside of the body of a function. Local variables include parameters as well as other variables assigned within a function definition.

In the following function definition, `total_string` and `name` are local variables. 
```
def greet_employee(name):
	total_string = "Welcome" + name
	return total_string
```
> The variable `total_string` is a local variable because it's assigned inside of a function. The parameter `name` is a local variable because it is also created when the function is defined. 

Whenever you call a function, Python creates these variables temporarily while the function is running and deletes them from memory after the function stops running. 

This means that if you call the `greet_employees()` function with an argument and then use the `total_string` variable outside of this function, you'll get an error. 

**Best Practices for Global and Local Variables**
> When working with variables and functions, it is very important to make sure that you only use a certain variable name once, even if one is defined globally and the other is defined locally. 

### Built-in Functions

`print()` outputs a specified object to the screen

`type()` returns the data type of its input

`max()` returns the largest numeric function passed into it

`sorted()` sorts the components of a list

### Work with Built-In Functions

`print()`
> outputs a specified object to the screen
> one of the most commonly used built-in functions

-  The `print()` function takes in any number of arguments, separated by a comma, and prints all of them.
	-  You can run a `print()` statement with strings, variables, integers together.

`type()` 
> returns the data type of its argument. 
> The `type()` function helps you keep track of the data types of variables to avoid errors throughout your code. 

`max()` and `min()`
> the `max()` function returns the largest numeric input passed into it. 
> the `min()` function returns the smallest numeric input passed into it.

-  The `max()` and `min()` function accept arguments of either multiple numeric values or of an iterable like a list, and they return the largest or smallest value respectively.

`sorted()`
> sorts the components of a list
> the `sorted()` function also works on any iterable, like a string, and returns the sorted elements in a list. 
> by default, it sorts them in **ascending order**

-  The `sorted()` function cannot take lists or strings that have elements of more than one data type.

## Modules and Libraries

**Library**
> A collection of modules that provide code users can access in their programs

**Module**
> a Python file that contains additional functions, variables, classes and any kind of runnable code

**Python Standard Library**
> An extensive collection of useable Python code that often comes packaged with Python

-  re module
-  csv module
-  glob
-  os
-  time
-  datetime

### Important Modules and Libraries in Python
> How to import a module that exists in the Python Standard Library and use it's functions.
> Expand understanding of external libraries

**The Python Standard Library**
> Collection of Python code that often comes packaged with Python. It includes a variety of modules, each with pre-built code centered around a particular type of task.

-  the `re` module, which provides functions used for searching for patterns in log files
-  the `csv` module, which provides functions used when working with `.csv` files. 
-  the `glob` and `os` modules, which provide functions used when interacting with the command line
-  the `time` and `datetime` modules, which provide functions used when working with timestamps

> Another Python Standard Library is `statistics`. The `statistics` module includes functions used when calculating statistics related to numeric data
> `mean()` is a function in the `statistics` module that takes numeric data as input and calculates its mean (or average).
> `median()` is a function in the `statistics` module that takes numeric data as input and calculates its median

**Importing Modules from PSL**
> to import an entire module, you use the `import` keyword. 
> the `import` keyword searches for a module or library in a system and adds it to the local Python environment. 

**Note:** when importing an entire Python Standard Library module, you need to identify the name of the module with the function when you call it. 
-  You can do this by placing the module name followed by a period (.) before the function name
-  `statistics.mean` and `statistics.median` for example

**Importing Specific Functions from a Module**
> to import a specific function from a PSL, you can use the `from` keyword. 
> If you just want `median` from the `statistics` module, you can write `from statistics import median` 

> to import multiple functions from a module, you can separate the functions you want to import with a comma. 
> for example: `from statistics import mean, median` 

> If you import specific functions from a module, you no longer have to specify the name of the module before those functions. 

**External Libraries**
> In addition to the Python Standard Library, you can also download external libraries and incorporate them into your Python code.

-  `bs4` or 'Beautiful Soup' is used for parsing HTML files
-  `NumPy` is used for arrays and mathematical computations. 

> `%pip install numpy` is a command to find and install `numpy` so it can be used in your code editor or Python environment

# Module 3

### Working with Strings
> More about working with strings and lists
> 	Extracting characters from strings
> Writing algorithms
> Using regular expressions

**String Operations**

String Data
> data consisting of an ordered sequence of characters

`len()` 
> returns the number of elements in an object

**String Concatentation**
> the process of joining two strings together
> 

**Method**
> a function that belongs to a specific data type

	`.upper()`
> 	returns a copy of the string in all uppercase letters

	`.lower()`
> 	returns a copy of the string in all lowercase letters

### String Indices and Slices

**Index**
> a number assigned to every element in a sequence that indicates it's position
> Python is a "zero indexed" language
> - this means that the first letter in a string for example, starts as zero

**Slice**
> `"HELLO[1:4}]`
> the first index is 1
> Python stops the slice before the second index, so in this example it would end at the third index

`.index`
> finds the first occurrence of the input in a string and returns its location
> 

## Strings and the Security Analyst
> The ability to work with strings is important in the cybersecurity profession.
> This reading reviews previous concepts and explains more about using the `.index()` method

**String Data in a Security Setting**
> String data is one of the most common data types that will be encountered as a security analyst.
> 	String data is data consisting of an ordered sequence of characters.
> 	It's used to store any type of information you don't need to manipulate mathematically (such as through division or subtraction). In a cybersecurity context, this includes IP addressed, usernames, URLs and employee IDs.

**Working with Indices in Strings**

**Indices**
> an Index is a number assigned to every element in a sequence that indicates it's position.

> Indices start at `0`. 
> You can also use negative numbers in indices.
> 	This is based on their position relative to the last position in the string.

**Bracket Notation**
> Refers to the indices placed in square brackets. You can use bracket notation to extract a part of a string. For example, the first character of the device ID might represent a certain characteristic to the device. If you want to extract it, you can use bracket notation for this:

`"h32rb17"[0]`

> This device ID might also be stored within a variable called `device_id`. You can apply the same bracket notation to the variable:

`device_id = "h32rb17`
`devic_id[0]`

> You can also take a slice from a string. When you take a slice from a string, you extract more than one character from it. It's often done in cybersecurity contexts when you're only interested in a specific part of a string. 
> For example, this might be certain numbers in an IP address or certain parts of a URL.

> In the device ID example, you might need the first three characters to determine a particular quality of the device. To do this, you can take a slice of the string using bracket notation. 

```
print("h32rb17"[0:3])
```

**String Functions and Methods**
> the `str()` function converts it's input object into a string. As an analyst, you might use this in security logs when working with numerical IDs that aren't going to be used with mathematical processes. Converting an integer to a string gives you the ability to search through it and extract slices from it. 

```
string_id = str(19329302)
```
> this line of code would convert the integer `19329302` into a string

#### `len()`
-  returns the number of elements in an object
> As an example, if you wanted to verify that a certain device_ID conforms to a standard of containing seven characters, you can use the `len()` function and a conditional.
> When you run the following code, it will print a message if `"h32rb17"` has seven characters
```
device_id_length = len("h32rb17")
if device_id_length == 7:
	print("The device ID has 7 characters.")
```
>The device ID has seven characters.

#### `.upper` and `.lower`

> the `.upper()` method returns a copy of the string with all of its characters in uppercase. For example, you can change this department name to all uppercase by running the code `"Information Technology".upper()` 
> 	It would return the string `"INFORMATION SECURITY"`

> Meanwhile, the `.lower()` method returns a copy of the string in all lowercase characters. `"Information Security".lower()` would return the string `"information technology"`

#### `.index()`

> the `.index()` method finds the first occurrence of the input in a string and returns its location. For example, this code uses the `.index()` method to find the first occurence of the character `"r"` in the device ID `"h32rb17"` 

**Finding Substrings With Index**

> a substring is a continuous sequence of characters within a string. For example, `"llo"` is a substring of `"hello"`

> the `.index()` method can also be used to find the index of the first occurrence of a substring. It returns the index of the first character in that substring. Consider this example that finds the first instance of the user `"tshah"` in a string:
```
tshah_index = "tsnow, tshah, bmoreno - updated".index("tshah")
print(tshah_index)
```
> the `.index()` method returns `7` which is where the substring `"tshah` starts.

## Work with Lists and Develop Algorithms

> items in a list are also zero indexed

**List Concatenation**
> combining two lists into one by placing the elements of the second list directly after the elements of the first list

Lists in Python are not immutable. 
-  Unlike strings, lists in Python do not have this property of immutability.
-  We can freely change, add and remove list values.

#### `.insert` 

> adds an element in a specific position inside a list
```
my_list = ["a", "b", "c", "d", "e"]
my_list.insert(1, 7)
```
> the first argument after `.insert` is the index of the element to be inserted into the list
> the second argument after the index is what we want to add to the list
> every element after the insert is shifted up one index position

#### `.remove`

> removes the first occurrence of a specific element in a list
```
my_list = ["a", "b", "c", "d", "e"]
my_list.remove("d")
print(my_list)
```
> the `.remove` method is not indexed, it simply removes the specified element in the argument after the `.remove` method.

## Write a Simple Algorithm

**Algorithm**
-  a set of rules that solves a problem
-  a set of steps that takes an input from a problem, uses this input to perform tasks, and returns a solution as an output.

#### `.append` method

> adds input to the end of a list

### Lists and the Security Analyst

> Review previous concepts with new examples
> Introduce the `.index` method as it applies to lists
> highlight how lists are used in a cybersecurity context

**List Data in a Security Setting**

**List Data**
-  data structure that consists of a collection of data in sequential form. 
-  You can use lists to store multiple elements in a single variable
-  A single list can contain multiple data types

In a cybersecurity context, you may use lists to store usernames, IP addresses, URLs, device IDs, and data. 
-  Placing data in a list allows you to with with it in a variety of ways
	-  For example, you might iterate through a list of device IDs using a `for` loop to perform  the same actions for all items in the list. 
	-  You could incorporate a conditional statement to only perform these actions if the device IDs meet certain conditions

#### Working with Indices in Lists

> Like strings, you can work with lists through their indices, and indices start at `0`. In a list, an index is assigned to every element in the list.

**Bracket Notation**

> Similar to strings, you can use bracket notation to extract elements or slices in a list. To extract an element from a list, after the list or the variable that contains a list, add square brackets that contain the index of the element. 
> 	The following example extracts the element with an index of `2` from the variable `username_list` and prints it. You can run this code to examine what it outputs.
```
username_list = ["elarson", "fgarcia", "tshah", "sgilmore"]
print(username_list[2])
```
> tshah is the output of this code.

**Extracting a Slice From a List**

> Just like with strings, it's also possible to use bracket notation to take a slice from a list. With lists, this means extracting more than one element from the list.
> 	- When you extract a slice from a list, the result is another list.

> This extracted list is called a sublist because it is part of the original, larger list. 
```
username_list = ["elarson", "fgarcia", "tshah", "sgilmore"]
print(username_list[0:2])
```
> the output is `["elarson", "fgarcia"]`

**Changing the Elements in a List**

> Unlike strings, you can use bracket notation to change elements in a list. This is because a string is **immutable** and cannot be changed after it is created and assigned a value.
>		lists are not immutable, like strings.
```
username_list = ["elarson", "fgarcia", "tshah", "sgilmore"]

print("Before changing an element:", username_list)

username_list[1] = "bmoreno"

print("After changing an element:", username_list)
```
> `"bmoreno"` will replace `"fgarcia"` in the list, because `'fgarcia'` is at index 1.

**List Methods**

> list methods are functions that are specific to the list data type. 
> These include:
> 	- `.insert()`
> 	- `.remove()`
> 	- `.append()`
> 	- `.index()`

#### `.insert` 

> this method adds an element in a specific position inside a list. 
> it has two parameters:
> 	- the index where you will insert the new element
> 	- the element you want to insert
```
username_list = ["elarson", "bmoreno", "tshah", "sgilmore"]

print("Before inserting an element:", username_list)

username_list.insert(2,"wjaffrey")

print("After inserting an element:", username_list)
```
> `"wjaffrey"` is inserted into the list at index `2`. The other elements in the list are moved up one index position.

#### `.remove()`

> this method removes the first occurrence of a specific element in a list. 
> 	- it has only one parameter:
> 		- the element you want to remove
```
username_list = ["elarson", "bmoreno", "wjaffrey", "tshah", "sgilmore"]

print("Before removing an element:", username_list)

username_list.remove("elarson")

print("After removing an element:", username_list)
```
> `'elarson'` is removed from the list using the `.remove()` method.
> if there are two of the same element in a list, the `.remove()` method only removes the first instance of that element and not all occurrences

#### `.append()`

> this method adds input to the end of a list. 
> it has one parameter:
> 	- the element you want to add to the end of the list.
```
username_list = ["bmoreno", "wjaffrey", "tshah", "sgilmore"]

print("Before appending an element:", username_list)

username_list.append("btang")

print("After appending an element:", username_list)
```
> this code places `'btang'` to the end of `username_list`

> the `.append()` method is often used with `for` loops to populate an empty list with elements.
```
numbers_list = []

print("Before appending a sequence of numbers:", numbers_list)

for i in range(10):

    numbers_list.append(i)

print("After appending a sequence of numbers:", numbers_list)
```
> Before appending a sequence of numbers: `[]`
   After appending a sequence of numbers: `[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]`

#### `.index()`

> similar to the `.index()` method used for strings, the `.index()` method used for lists finds the first occurrence of an element in a list and returns it's index. It takes the element you're searching for as an input. 

## Regular Expression

> a sequence of characters that forms a pattern
> can be used to search for any type of pattern

### Basics of Regular Expressions
> a **regular expression** is a sequence of characters that forms a pattern. You can use these in Python to search for a variety of patterns. This could included IP addresses, emails or device IDs. 

To access regular expressions and related functions in Python, you need to import the `re` module first. 

`import re`
> this command will import the `re` module

Regular expressions are stored in Python as strings. Then, these strings are used in `re` module functions to search through other strings. 

-  There are many functions in the `re` module, but you will explore how regular expressions work through `re.findall()` 
-  The `re.findall()` function returns a list of matches to a regular expression.
-  `re.findall()` requires two parameters:
	-  The string containing the regular expression pattern
	-  The string you want to search through

> If you want to do more than search for specific strings, you must incorporate special symbols into your regular expressions.

### Regular Expression Symbols

**Symbols for Character Types**
> You can use a variety of symbols to form a pattern for your regular expression. 
-  Some of the symbols identify a particular type of character
-  For example, `\w` matches with any alphanumeric character

```
import re
re.findall(\w, "h32rb17")
```
> `['h', '3', '2', 'r', 'b', '1', '7']`
Because every character within this device ID is an alphanumeric character, Python returns a list with seven elements. 
	-  Each element represents one of the characters in the Device ID

You can use these additional symbols to match to specific kinds of characters:
-  `.` matches to all characters, including symbols
- `\d` matches to all single digits
- `\s` matches to all single spaces
- `\.` matches to the period character

**Symbols to Quantify Occurrences**
> Other symbols quantify the number of occurrences of a specific character in the pattern. In a regular expression pattern, you can add them after a character or a symbol identifying a character type to specify the number of repetitions that match to the pattern.

For example, the `+` symbol represents one or more occurrences of a specific character.
```
import re
re.findall("\d+", "h32rb17")

['32', '17']
```
> with the regular expression `\d+`, the list contains two matches of `"32"` and `"17"`

Another symbol used to quantify the number of occurrences is the `*` symbol. The `*` symbol represents zero, one or more occurrences of a specific character. The following code substitutes the `*` symbol for the `+` used in the previous example. 
```
import re
re.findall("\d*", "h32rb17")

['', '32', '', '', '17', '']
```
> Because it also matches zero occurrences, the list now contains empty strings for the characters that were not single digits. 

If you want to indicate a specific number of repetitions to allow, you can place this number in curly brackets `{ }` after the character or symbol. 
```
import re
re.findall("\d{2}", "h32rb17 k825t0m c2994eh")

>> ['32', '17', '82', '29', '94']
```
> Because it is matching two repetitions, when Python encounters a single digit, it checks whether there is another one following it.
> If there is, Python adds the two digits to the list and goes on to the next digit. If there isn't, it proceeds to the next digit without adding the first digit to the list. 

**Note:** Python scans strings left-to-right when matching against a regular expression. When Python finds a part of the string that matches the first expected character defined in the regular expression, it continues to compare the subsequent characters to the expected pattern. When the pattern is complete, it starts this process again. So in cases in which three digits appear in a row, it handles the third digit as a new starting digit.
```
import re

re.findall("\d{1,3}", "h32rb17 k825t0m c2994eh")

>> ['32', '17', '825', '0', '299', '4']
```
> The returned list contains elements of one digit like `"0"`, two digits like `"32"` and three digits like `"825"` 
> The first digit in the curly brackets is the minimum number of repetitions and the second digit is the maximum number of repetitions. 

**Constructing a Pattern**

> Constructing a regular expression requires you to break down the pattern you're searching for into smaller chunks and represent those chunks using the symbols you've learned.

For each employee, the following string contains their employee ID, their username followed by a colon (:), their attempted logins for the day, and their department:

`employee_logins_string = "1001 bmoreno: 12 Marketing 1002 tshah: 7 Human Resources 1003 sgilmore: 5 Finance"`

To complete this task with regular expressions, you need to break down what you're searching for into smaller components. 
In this case, those components are the varying number of characters in a username, a colon, a space and a varying number of single digits. 
The corresponding regular expression symbols are `\w, :, \s, and \d+`. 
```
import re

pattern = "\w+:\s\d+"

employee_logins_string = "1001 bmoreno: 12 Marketing 1002 tshah: 7 Human Resources 1003 sgilmore: 5 Finance"

print(re.findall(pattern, employee_logins_string))

>> ['bmoreno: 12', 'tshah: 7', 'sgilmore: 5']
```
**Note**: Working with regular expressions can carry the risk of returning unneeded information or excluding strings you want to return. Therefore, it's useful to test your regular expressions. 

## Module 4: Python In Practice
> **Opening and reading files in Python**
> **Parsing files**
> **Debugging code**

### **Automate Cybersecurity Tasks with Python**
> Automate detection of unusual activity
> Automate security controls put in place

### Essential Python Components for Automation
> Explore why the Python components learned thus far are essential components when automating tasks through Python, and you'll be introduced to another necessary component: working with files.

**Automating Tasks with Python**
> **Automation** is the use of technology to reduce human and manual effort to perform common and repetitive tasks. 
> As a security analyst, you will primarily use Python to automate tasks.

Automating cybersecurity tasks requires understanding the following Python components that you've worked with in this course. 

**Variables**

A variable is a container that stores data. 
Variables are essential for automation
Without them, you would have to individually rewrite values for each action you took in Python.

**Conditional Statement**

A **conditional statement** is a statement that evaluates code to determine if it meets a specified set of conditions. 
Conditional statements allow you to check for conditionals before performing actions. 
This is much more efficient that manually evaluating whether to apply an action to each separate piece of data.

**Iterative Statements**

An iterative statement is code that repeatedly executes a set of instructions. You explored two kinds of iterative statements: `for` and `while` loops. 

In both cases, they allow you to perform the same actions a certain number of times without the need to retype the same code each time. 

Using a `for` loop allows you to automate repetition of that code based on a sequence, and using a `while` loop allows you to automate the repetition based on a condition. 

**Functions**

A **function** is a section of code that can be reused in a program. Functions help you automate your tasks by reducing the need to incorporate the same code multiple places in a program. Instead, you can define the function once and call it wherever you need it.

You can develop functions based on your particular needs. You can also incorporate the built-in functions that exist directly in Python without needing to manually code them. 

**Techniques for Working with Strings**

String data is one of the most common data types that you'll encounter when automating cybersecurity tasks through Python, and there are a lot of techniques that make working with strings efficient. 
	-  You can use bracket notation to access characters in a string through their indices. You can also use a variety of functions and methods when working with strings, including `str()`, `len()`, and `.index()` 

**Techniques for Working with Lists**

List data is another common data type. Like with strings, you can use bracket notation to access a list element through its index. Several methods also help you with automation when working with lists:
	-  `.insert()`
	-  `.remove()`
	-  `.append()`
	-  `.index()`

**Example: Counting login attempts made by a flagged user**

> As one example, you may find that you need to investigate the logins of a specific user who has been flagged for unusual activity. Specifically, you are responsible for counting how many times this user has logged in for the day. If you are given a list identifying the username associated with each login attempt made that day, you can automate this investigation in Python.

To automate the investigation, you'll need to incorporate the following Python components:
	-  A `for` loop will allow you to iterate through all the usernames in the list
	-  Within the `for` loop, you should incorporate a conditional statement to examine whether each username in the list matches the username of the flagged user.
	- When the condition evaluates to `True`, you also need to increment a counter variable that keeps track of the number of times the flagged user appears in the list. 

### Import Files into Python
> Review syntax needed to import files into Python and convert them into strings
> Focus on why the ability to work with files is important for security analysts using Python, and you will learn about writing files.

**Working with Files in Cybersecurity**

> Security analysts may need to access a variety of files when working in Python. Many of these files will be logs. 
	-  A **log** is a record of events that occur within an organization's systems. 

For instance, there may be a log containing information on login attempts. This might be used to identify unusual activity that signals attempts made by a malicious actor to access the system.

As another example, malicious actors that have breached the system might be capable of attacking software applications. An analyst might need to access a log that contains information on software applications that are experiencing issues.

**Opening Files in Python**

To open a file called `"update_log.txt"` in Python for purposes of reading it, you can incorporate the following line of code:

`with open("update_log.txt", "r") as file:` 
> this line consists of the `with` keyword, the `open()` function with its two parameters, and the `as` keyword followed by a variable name.
> 	-  You must place a colon at the end of the line

#### **`with`** 

> the keyword `with` handles errors and manages external resources when used with other functions.
> In this case, it's used with the `open()` function in order to open a file. It will then manage the resources by closing the file after exiting the `with` statement

**Note:** you can also use the `open()` function without the `with` keyword. However, you should close the file that was opened to ensure proper handling of the file.

#### `open()` 

> opens a file in Python
> The first parameter identifies the file you want to open

> if a file you want to open is not in the same directory as the Python file that will access it, it is necessary to specify the file path

A **file path** is the location of a file or directory. 
An absolute file path starts from the highest-level directory, the root.

**Note:** in Python, the names of files or their file paths can be handled as string data, and like all string data, you must place them in quotation marks.

> The second parameter of the `open()` function indicates what you want to do with the file. 
> `"r"` indicates that you want to read a file
> `"w"` can be used to write to a file
> `"a"` can append a file

#### `as`

> when you open a file using `with open()` you must provide a variable that can store the file while you are within the `with` statement. You can do this through the keyword `as` followed by this variable name.

> the keyword `as` assigns a variable that references another object

#### Reading Files in Python

> using the `.read()` function allows you to read the contents of a file
```
with open("update_log.txt", "r") as file:
	updates = file.read()
print(updates)
```
> The `.read()` method converts files into strings. 
> This is necessary in order to use and display the contents of the file that was read.
> In this example, the `file` variable is used to genrate a string of the file contents through `.read()`. 
> This string is then stored in another variable called `updates`
> After this, `print(updates)` displays the string

Once the file is read into the `updates` string, you can perform the same operations on it that you might perform with any other string. For example, you could use the `.index()` method to return the index where a certain character or substring appears.

Or, you could use `.len()` to return the length of this string

#### Writing Files in Python

> Security analysts may also need to write to files.
> This could happen for a variety of reasons.
> For example, they might need to crate a file containing the approved usernames on a new allow list.
> Or, they might need to edit existing files to add data or to adhere to policies for standardization

You should use the `"w"` argument when you want to replace the contents of an existing file. 

Additionally, you can use the `"w"` argument to create a new file.
> `with open("update_log2.txt", "w") as file` creates and opens a new file called `"update_log2.txt"` 

You should use the `"a"` argument if you want to append new information to end of an existing file rather than writing over it.

```
line = "jrafael,192.168.243.140,4:56:27,True"

with open("access_log.txt", "a") as file:

    file.write(line)
    
```
> this example uses the `.write()` method to append the content of the `line` variable to the file `"access_log.txt"` 

#### Working with Files in Python

> **parsing** is the process of converting data into a more readable format
> 	-  Data may need to become more readable in a couple of different ways
> 	-  First, the certain parts of your Python code may require modification into a specific format
> 	-  By converting data into this format, you enable Python to process it in a specific way
> 	-  Second, programmers need to read an interpret the results of their code, and parsing can also make the data more readable for them.

#### `.split()` and `.join()`

> the `.split()` method converts a string into a list
	- Separates the string based on a specified character that's passed into the `.split()` as an argument
> if you do not pass an argument into `.split()`, it will separate the string every time it encounters a whitespace

**Note:** a variety of characters are considered whitespace by Python. These characters include spaces between characters, returns for new lines, and others.

**Applying Split to Files**

> the `.split()` method allows you to work with file content as a list after you've converted it to a string through the `.read()` method. 
> This is useful in a variety of ways. For example, if you want to iterate through the file contents in a `for` loop, this can be easily done when it's converted into a list.

**The Basics of `.join()`**

> If you need to convert a list into a string, there is also a method for that. The `.join()` method concatenates the elements of an iterable into a string.
> The syntax used with `.join()` is distinct from the syntax used with `.split()` and other methods that you've worked with, such as `.index()` 

In methods like `.split()` or `.index()`, you append the method to the string or list that you're working with and the pass in other arguments

For example, the code `usernames.index(2)`, appends the `.index()` method to the variable `usernames`, which contains a list. 
	-  It passes in `2` as the argument to indicate which element to return.

However, with `.join()`, you must pass the list that you want to concatenate into a string in as an argument. 

You append `.join()` to a character that you want to separate each element with once they are joined into a string. 

**Applying `.join()` to Files**

> when working with files, it may also be necessary to convert its contents back into a string. For example, you may want to use the `.write()` method. The `.write()` method writes string data to a files
> This means that if you have converted a file's contents into a list while working with it, you'll need to convert it back into a string before using `.write()`. You can use the `.join()` method for this.

#### Develop a Parsing Algorithm in Python

> bring all of the pieces together to import a file, parse it, and implement a simple algorithm to help us detect suspicious login attempts. 
> 	-  We want to create a program that runs every time a user logs in and checks if that user has had three or more failed login attempts

**Solving the Problem:**

-  `for` loop
-  counter `variable` 
-  if `statement`

#### Debug Python Code

> **debugging**
> -  the practice of identifying and fixing errors in code

**Types of Errors**
-  Syntax Errors
-  Logic Errors
-  Exceptions

**Syntax Errors** are similar to fixing grammatical errors in normal languages
-  omitting a parenthesis after a function
-  misspelling a Python keyword
-  not properly closing quotation marks for a string

**Logic Errors** may not cause error messages, instead, they produce unintended results
-  writing incorrect text within a print statement
-  writing a less than symbol instead of a less than or equal to symbol

**Exception Errors** happen when the program doesn't know how to execute code even though there is not problem with the syntax

#### Explore Debugging Techniques

> Additional strategies and examples for debugging Python code. 

**Types of Errors**

> It's a normal part of developing code in Python to get error messages or find that the code you're running isn't work as you intended.
> The important thing is that you can figure out how to fix errors when they occur. 

**Syntax Errors**

> a **syntax error** is an error that involves invalid usage of a programming language.
> Syntax errors occur when there is a mistake with the Python syntax itself. 

> **EOL** stands for "end of line".

**Logic Errors**

> a **logic error** is an error that results when the logic used in code produces unintended results. Logic errors may not produce error messages. In other words, the code will not do what you expect it to do, but it is still valid to the interpreter

For example, using the wrong logical operator, such as a greater than or equal to sign (>=) instead of greater than sign (>) will produce a logic error. 

Python will not evaluate a condition as you intended. However, the code is valid, so it will run without an error message.

**Exceptions**

> an **exception** is an error that involves code that cannot be executed even though it is syntactically correct. This happens for a variety of reasons.

One common cause of an exception is when the variable that hasn't been assigned or a function that hasn't been defined. In this case, you output will include `NameError` to indicate that this is a name error. 

In addition to name errors, the following message are output for other types of exceptions:

-  `"IndexError"`: an index error occurs when you place an index in bracket notation that does not exist in the sequence being referenced. 
- `"TypeError"` a type error results from using the wrong data type. For example, if you tried to perform a mathematical calculation by adding a string value to an integer, you would get a type error.
-  `FileNotFound` a file not found error occurs when you try to open a file that does not exist in the specified location.

**Debugging Strategies**

> If you have multiple errors, the Python interpreter will output error messages one at a time, starting with the first error it encounters. After you fix that error and run the code again, the interpreter will output another message for the next syntax error or exception it encounters.

When dealing with Syntax errors, the error messages you receive in the output will generally help you fix the error. However, with logic errors and exceptions, additional strategies may be needed.

**Debuggers**

> when writing code in an **integrated development environment**, it may offer error detection tools in the form of a debugger. 
> a **debugger** is a software tool that helps to locate the source of an error and assess its causes

In the case where you can't find the line of code causing the issue, debuggers help you to narrow down the source of the error in your program.

They do this by working with breakpoints. Breakpoints are markers placed on certain lines of executable code that indicate which sections of code should run when debugged. 

Some debuggers also have a feature that allows you to check the values stored in variables as they change throughout your code. This is especially helpful for logic errors so that you can locate where variable values have unintentionally changed.

**Use Print Statements**



