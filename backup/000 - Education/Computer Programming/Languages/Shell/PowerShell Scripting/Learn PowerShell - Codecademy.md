# Getting Started
## Introduction

> PowerShell was introduced to the Windows operating system in 2006 and has since become a popular tool for automating many Windows tasks. 

While the shell focuses on Windows administration, PowerShell command-line applications are now available to install on the macOS and Linux operating systems.

## What is PowerShell?

> PowerShell is a command-line shell and scripting language. This means that we can run individual commands within the terminal as well as create and execute more complex scripts. Both are equally useful when automating computer administration tasks.

While most computing interfaces involve a GUI, or ***Graphical User Interface***, there is a clear reason why developers and administrators still use command-line tools like PowerShell: they are just better at certain tasks. 

If we look at essential file system management, creating folders for 20 users might involve dozens or hundreds of mouse movements and clicks using a graphical interface. Alternatively, a single command in the PowerShell terminal can take a list of names and create folders for each of them.

The above example gets more convincing when our users are in the thousands, and the tasks for each user become more complex. While graphical interfaces can be programmed to perform any group of actions, it is quicker and cheaper to accomplish our goals using PowerShell.

```powershell
Write-Host "Hello, World!"
```

> This command outputs "Hello World!" to the terminal. 

## Basic Commands 

Running commands in PowerShell can help us accomplish many different tasks. PowerShell commands are called `cmdlets`, which is pronounced command-lets.

Their names help us understand their action because they are give a `verb - noun` command format, such as:

```powershell
Get-Date
```

- The above PowerShell cmdlet has the verb `Get`, and the noun `Date`, which leads us to believe the current date will be retrieved and printed to the terminal. 

In the last exercise, you have have printed "Hello, World!" in the terminal using: 

```powershell
Write-Host "Hello, World!"
```

This command will write to the host, printing a given argument to the terminal. In this case, the string "Hello, World!" is used as an argument to `Write Host`. As we will see in the next exercise and future lessons, `Write-Host` is used within scripts to create output for the user and display data being processed.

`Get-Date` and `Write-Host` are just a couple of the many cmdlets we can run in the PowerShell terminal. To discover more commands available to us, use the following:

```powershell
Get-Command
```

> Without any argument, `Get-Command` will output all available cmdlets. We can also request specific cmdlets. 

To output all `Get` commands, we need to pass an argument using the `-Verb` flag:

```PowerShell
Get-Command -Verb Get
```

The `-Verb` flag looks for any commands whose verb matches the argument given: `Get`. 

We can also look for specific nouns:

```Powershell
Get-Command -Noun Host
```

This command outputs all the commands acting on `Host`, the terminal. 

Lastly, as with any terminal session, our screen can get filled with a lot of text. To clear the terminal, use the following:

```powershell
Clear-Host
```

## Using the Terminal

> When working in the PowerShell terminal, a few practical actions can make running commands easier.

### Command Completion

If you type in only a few letters of a command and then hit the "Tab" key, the terminal will attempt to autocomplete the command.

If there is only one command that the partial command can be, such as `Get-D`, hitting Tab will autofill the rest of the command with `Get-Date`.

If more than one command matches the partial command, such as `Get-H`, Tab will list the potential commands.

```
Get-Help  Get-History  Get-Host
```

This can help us identify what command we want to use. 

### Command History

As with most modern terminals, a command history is stored in a file and can be accessed using:

```PowerShell
Get-History
```

This command is helpful is you forget how you previously accomplished a task and want to look back.

### History with Up/Down Keys

If there are commands that you plan on using a lot or ones that are long that you have to run again, the Up, and Down keys on the keyboard can be used to cycle through your command history. Start this process using the up arrow key to scroll from newer or older commands. You can scroll back with the down arrow key toward more recent commands.

Using quick shortcuts like these allows us to navigate the next-based world of PowerShell a little bit easier, so we can focus on our primary task.

## Writing Scripts

> Well executed PowerShell commands can accomplish a lot, but sometimes we must perform complex tasks requiring multiple commands. In such cases, we can write a PowerShell script and run it in the terminal when needed.

To run a script, we open up any text editor, write our commands and name the file with a `.ps1` file extension.

For example, the following commands can be put into a script file called `host-commands.ps1`.

```powershell
Write-Host "All commands that act on Host:"
Get-Command -Noun Host
```

With these two commands in the `host-commands.ps1` file, we can now run our script using the following command in the terminal:

```
.\host-commands.ps1
```

This will run the script and produce the following output:

```
All commands that act on Host:CommandType     Name-----------     ----                                   Function        Clear-Host                             Cmdlet          Get-Host                               Cmdlet          Out-Host                               Cmdlet          Read-Host                              Cmdlet          Write-Host 
```

> The `.\` notation before the script name tells the shell to look for a file in the current directory and run it. In most shells, the forward slash notation `./` may also be used.

## Summary

- How PowerShell can automate our work within an operating system. 
- Common commands such as:
	- `Get-Date`
	- `Write-Host`
	- `Get-Command`
	- `Get-History`
- Using terminal shortcuts to increase productivity
- Writing scripts helps us run complex tasks


# Variables and Operators

> Regardless of the use case, one inevitable aspect of programming is storing and manipulating data to serve our needs. Data comes in various forms, such as:

- Numbers (integers): `1, -99, 42`
- Text (strings) `"Hello!"`, `BF1942`
- Booleans `true, false`
- more!

We will first cover various ways to create and use [variables](https://www.codecademy.com/resources/docs/powershell/variables) to store multiple types of data. We will then explore [operators](https://www.codecademy.com/resources/docs/powershell/operators) enabling us to perform arithmetic operations and compare the values of two or more pieces of data.

## Variables

Let's start by discussing how variables work. In computer programming, `variables` are used to store a piece of data. In PowerShell, variables can store the results of commands and expressions like *values, names, paths and settings*.

### Create a Variable

To create a variable, we must assign it a value. Variables in PowerShell are referenced using a dollar sign `$` followed by a variable name. 

After a variable reference, we use an equal sign `=` followed by the value we'd like to assign to that variable.

```Powershell
$my_string_variable = "Hello, World!"
```

In the example above, we are initializing a variable called `my_string_variable` to a string value of `Hello, World`.

Variable names consist of alphanumeric characters. They are `NOT` case sensitive and can include spaces and special characters when enclosed in *curly braces*.

However, following the convention of only using alphanumeric characters and the underscore `_` character is recommended because variables with special characters in their name are difficult to use.

### Use a Variable

```Python
PS > $my_string_variable
Hello, World!
```

Variable reference allows us to use or manipulate variables. As shown above, referencing the variable `my_string_variable` we defined earlier in the PowerShell terminal prints the value assigned to it. 

### User Input

Now that we can hold data using variables, we can look at a useful command that enables user input through the terminal. 

```Powershell
PS > $my_input = Read-Host -Prompt "Enter a number"
```

> The above example will output the `-Prompt` string and then wait for the user to input a value and hit Enter. The value will then be stored in `$my_input` for use later.

There a just a few ways we can use variables to collect, process and output data within our terminal and scripts.

## Variable Types and Advanced Usage

In this exercise, we will discuss how variable types are handles in PowerShell and a few advanced ways to interact with variables, including enforcing types, creating multiple variables and a few variable-related cmdlets.

### Variable Types

The following are some common types of variables:

- `Int`: integers like `2`, `-5`, `99`
- `String`: zero or more characters enclosed in double quotes like `"Codecademy"`, `"3X4mP|3`
- `Boolean`: two possible values: `$True` and `$False`
- `Array`: a collection of items like `25, "red", $False, 16.30`.

PowerShell assigns a type to the variable *depending on the value we assign to it*. This is called ***dynamic typing***. The default type of any uninitialized variable is `$null`.

We can append `.GetType().Name` to the variable reference to determine a variable's data type.

```Powershell
PS > $my_string_variable = "Hello, World!"
PS > $my_string_variable.GetType().name
String
```

In the example above, we are accessing the `Name` property of the `GetType()` method of a variable we initialized. 

- The `GetType()` method returns the name and base type property for the variable. 
- Accessing the `Name` property only returns the data type we desire. 
- The variables data type is `string`.

### Constrained Variables

If we wish to enforce a certain type on a variable, we can create a *constrained variable* via casting. 

> If we wish to enforce a certain type on a variable, we can create a *constrained variable* via casting. 

```powershell
PS > [INT]$age = 25
PS > $age
25

PS > [Int]$age = "twenty five"
Cannot convert value "age" to type "system32.Int32". Error: "Input string was not in a correct format."
```

> When initializing a variable, we specify the type in brackets before referencing the variable. Attempting to assign a value of another type results in an error if PowerShell cannot convert it.

### Creating Multiple Variables

PowerShell allows us to create multiple variables using one statement. To initialize multiple variables with the same value:

```powershell
$i = $j = $k = 0
```

To assign multiple values to multiple variables

```powershell
$number, $color, $bool = 25, "red", $false
```

## Environment Variables

[_Environment Variables_](https://www.codecademy.com/resources/docs/powershell/environment-variables) store information related to the current environment, like the Operating System and user sessions like our current terminal.

They are *global variables*, meaning we can access them across commands and programs. The operating system usually creates them, but we can also use them to configure our production environment. 

### List Environment Variables

In PowerShell, environment variables are stored as strings. We can use the `Get-ChildItem` cmdlet on the `Env:` drive to get a complete list of all existing environment variables.

```powershell
PS > Get-ChildItem Env:
Name                           Value
----                           -----BROWSERSLIST_IGNORE_OLD_DATA   1EIN_IMAGE                      
								ubuntu
```

To get the specific value of an environment variable, we can use either of the following commands:

```powershell
(Get-ChildItem Env:EIN_IMAGE).Value> 
ubuntu
$Env:EIN_IMAGE> 
ubuntu
```

Two popular environment variables in PowerShell are `HOME` and `PATH`. The `HOME` environment variables specifies the current user's home directory, whereas `PATH` includes all the directories where applications look for executables.

### Create an Environment Variable

> The syntax to create an environment variable in PowerShell is as follows:

```powershell
$Env:EXAMPLE_ENV_VAR = "custom value"
```

By convention, environment variable names are usually capitalized. The benefits of environment variables are that they are accessible across the terminal session and scripts. 

This allows our session to operate in one environment where all data is consistent across processes. 

## Arithmetic Operations

*Operators* are used to perform specific operations on data, often stored in a variable. PowerShell offers multiple types of operators to manipulate data, including:

- Arithmetic Operators
- Assignment Operators
- Unary Operators
- Comparison Operators
- Logical Operators

### Arithmetic Operators

First, let's discuss arithmetic operators used to calculate numeric values. Arithmetic operators include:

- `+` (addition): adds numbers and concatenates things
- `-` (subtraction): subtracts or negates numbers
- `*` (multiplication): multiplies numbers or copies strings a specified number of times. 
- `/` (division): divides numbers
- `%` (modulus): returns the remainder of a division

```powershell
PS > 5 + 5
10

PS > 25 % 3
1
```

Arithmetic operators are *binary*, meaning they require two operands to calculate the result. As we can see in the examples above, the syntax for arithmetic operators is `<Operand_1> <Arithmetic-Operator> <Operand_2>`. Operators are best utilized when used with variables, as shown below.

```powershell
PS > $number = 25
PS > $number / 5
5

PS > $number = $number * 3
PS > $number
75
```

### Arithmetic Operators on Strings

PowerShell allows us to manipulate strings using the addition `+` and multiplication `*` operators. The `+` operator concatenates strings, whereas the `*` operator copies the string a specified number of times.

```powershell
PS > $best_learning_platform = "Code" + "cademy"
PS > $punctuation = "!" * 3
PS > $best_learning_platform + $punctuation
Codecademy!!!
```

You can see two strings are joined to create the string `codecademy` and three exclamation marks are made into a string by multiplying `"!"` by `3.`

## Assignment and Unary Operators

In this exercise, we will discuss the assignment an unary operators.

### Assignment Operators

We can use assignment operators to assign, change, or append values to variables. The general syntax of the assignment operators is as follows: `<Variable> <Assignment-Operator> <Value>`.

We are already familiar with one of the assignment operators, `=`. It is used to assign a value to a variable. Other assignment operators include `+=`, `-=`, `*=`, `/=`, and `%=`. These operators are called *compound assignment operators*.

Notice that an arithmetic operator *precedes the `=`*. This means compound assignment operators perform operations on the values before the assignment. Consider the following example:

```powershell
PS > $number = 75
PS > $number_1 = $number / 3
PS > $number_1
25
PS > $number_2 = $number
PS > $number_2 /=3
PS > $number_2
25
```

We can use the `/=` compound assignment operator as a shorthand for dividing a variable and saving the result to the same variable. As shown above, the statements `$number_1 = $number / 3` and `$number_2 /= 3` behave similarly.

### Assignment Operators on Environment Variables

Recall that environment variables are of the type `String` and that the `+` arithmetic operator can concatenate strings. We can append the `+=` compound assignment operator to an existing environment variable.

```powershell
PS > $Env:EXAMPLE_ENV_VAR = "custom value"
PS > $Env:EXAMPLE_ENV_VAR += "; another value"
PS > $Env:EXAMPLE_ENV_VAR
custom value; another value
```

**Note**: Environment variables that have multiple values are separated by a semicolon `;` on Windows. For example, the `PATH` environment variable specifies the directories in which executable programs are located. Utilizing `;` with the `+=` assignment operator, we can add new directories to `PATH`.

### Unary Operators

Unary operators operate on a single variable operand. `++` and `--` are the increment and decrement operators and increase or decrease the value of a variable by 1, respectively.

```powershell
PS > $i = 0
PS > $i++
PS > $i
1

PS > $i--
PS > $i
0
```

> Unary operators are an easily readable way to increase or decrease a variable value by `1`.

## Equality Comparison Operators

> Comparison operators are sued to compare values, test conditions, or filter elements of a collection, such as an array. They return a *boolean* value, `True` or `False`, as a result.

### Equality Operators

Some of the comparison operators in PowerShell are called equality operators. They are binary operators that compare two integer or string values that return `True` if the operator condition is met; otherwise `False`. 

|Operator|Description|
|---|---|
|`-eq`|Checks if the two operand values are an exact match|
|`-ne`|Checks if the two operand values are NOT an exact match|
|`-gt`|Checks if the value of the left operand is greater than the value of the right operand|
|`-lt`|Checks if the value of the left operand is less than the value of the right operand|
|`-ge`|Checks if the value of the left operand is greater OR equal to the value of the right operand|
|`-le`|Checks if the value of the left operand is less OR equal to the value of the right operand|>
> Let's take a look at a few examples.

### `-eq` and `-ne`

In the example below, `-eq` returns `True` because `$my_num` matches the value `5`. When we use the `ne` operator on the same operands, it returns `False` since it only returns `True` when the two values are NOT a match.

```powershell
PS > $my_num = 5
PS > $my_num -eq 5
True
PS > $my_num -ne 5
False
```

## Logical Operators

In this exercise, we will take a look at logical operators.

Logical operators allow us to combine multiple `true`/`false` expressions and statements into complex *conditionals*. Using the operators `-and`, `-or`, `-xor`, `-not`, `|`, we can test multiple conditions with the equality comparison operators we discussed in the previous exercise. 

### Truth Table

A simple way to show the output of logical operators is through a truth table. 

|x|y|x -and y|x -or y|x -xor y|-not x|
|---|---|---|---|---|---|
|T|T|T|T|F|F|
|T|F|F|T|T|F|
|F|T|F|T|T|T|
|F|F|F|F|F|T|
As shown in the first two columns, imagine `x` and `y` are variables that hold the boolean values. The rest of the columns show the output of the corresponding logical operator given the values for `x` and `y` for that row. 

Let's explore a few PowerShell examples.

#### `-and`

The `and` logical operator is a binary operator that returns `True` if both statements or `True`.

```powershell
PS > -5 -lt 7 -and "hello" -eq "hello"
True

PS > -5 -lt 7 -and "hello" -eq "world"
```

#### `-or`

The binary `or` logical operator returns `True` if either statement returns `True`.

```powershell
PS > 42 -le 13 -or 5 -ge 5
True

PS > 42 -le 13 -or 5 -gt 5
False
```

#### `-xor`

The binary `xor` logical operator returns `True` when only ONE statement is `True`.

```powershell
PS > 25 -gt 2 -xor "hello" -eq "hello"
True

PS > 25 -gt 2 -xor "code" -eq "code"
False
```

#### `-not` and `!`

Both the `-not` and `!` operators negate the statement that follows. They are unary operators.

```powershell
PS > -not (2 -gt 5)
True

PS > !(17 -le 99)
False
```

---

```powershell
[String]$name = Read-Host -Prompt "Type your name"
[Int]$number_1 = Read-Host -Prompt "Type the first number"
[Int]$number_2 = Read-Host -Prompt "Type the second number"

# Write your operator statements below
$both_are_less_than_50 = $number_1 -lt 50 -and $number_2 -lt 50
# Write your operator statements above

Write-Host "`nHello, $name! Let's evaluate your inputs as True or False."
Write-Host "Both numbers are less than 50: $both_are_less_than_50"
Write-Host "One number is higher than 100: $one_is_higher_than_100"
Write-Host "Only one number is less than or equal to 10: $only_one_is_less_than_10"
Write-Host "Your name is not 'codecademy': $name_is_not_codecademy"
```

1. In the **logical_operators.ps1** script file, check if both variables `$number_1` and `$number_2` are less than `50`. Assign the boolean result to a variable called `$both_are_less_than_50`.

   When you’re done, click the Run button.

2. Check whether the variable `$number_1` OR `$number_2` is greater than `100`. Make the variable `$one_is_higher_than_100` equal to its result.

   When you’re done, click the Run button.

3. Check whether ONLY one variable `$number_1` or `$number_2` is less than or equal to `10` and assign the result to a variable `$only_one_is_less_than_10`.

   When you’re done, click the Run button.

4. Using one of the two logical operators for negation, `-not` or `!`, verify that the variable `$name` is not equal to the string ‘codecademy’. Make the boolean variable `$name_is_not_codecademy` equal to its result.

   When you’re done, click the Run button.

```powershell
[String]$name = Read-Host -Prompt "Type your name"
[Int]$number_1 = Read-Host -Prompt "Type the first number"
[Int]$number_2 = Read-Host -Prompt "Type the second number"

# Write your operator statements below
$both_are_less_than_50 = $number_1 -lt 50 -and $number_2 -lt 50
$one_is_higher_than_100 = $number_1 -gt 100 -or $number_2 -gt 100
$only_one_is_less_than_10 = $number_1 -le 10 -xor $number_2 -le 10
$name_is_not_codecademy = -not ($name -eq 'codecademy')

# Write your operator statements above

Write-Host "`nHello, $name! Let's evaluate your inputs as True or False."
Write-Host "Both numbers are less than 50: $both_are_less_than_50"
Write-Host "One number is higher than 100: $one_is_higher_than_100"
Write-Host "Only one number is less than or equal to 10: $only_one_is_less_than_10"
Write-Host "Your name is not 'codecademy': $name_is_not_codecademy"
```

## Operator Precedence

Just like in mathematics, the order in which operators are evaluated matters in programming. Operator precedence in PowerShell is as follows:

- `()`
- `++ --`
- `! -not`
- `* / %`
- `+ -`
- `-is -isnot -as`
- `-eq -ne -gt -ge -lt -le`
- `-contains -notContains`
- `-and -or -xor`
- `= += -= *= /= %=`

***Precedence*** is the order in which PowerShell evaluates the operators if multiple operators are used in the same expression. Parenthesis `( )` take the highest priority, and the assignment operators have the least priority. Operators on the same level are *evaluated from left to right*.

Consider the example below:

```powershell
PS > 5 - 1 * 5
0
```

The multiplication operator `*` has higher precedence than the subtraction operator `-`, Thus, in the example above, the expression `1 * 5` is evaluated first, resulting in `5 - 5`, which equals `0`.

We can use parenthesis to override the precedence order and face PowerShell to evaluate a part of an expression first. 

```PowerShell
PS > (5 - 1) * 5
20
```

## Review

Good job on making it to the end of [Variables](https://www.codecademy.com/resources/docs/powershell/variables) and Operators! In this lesson, we learned the following:

- How to create variables in a variety of ways
- Variable types and constrained variables
- Listing and creating environment variables
- Manipulate variables and data with operators
- Using arithmetic [operators](https://www.codecademy.com/resources/docs/powershell/operators) to perform mathematical operations
- Using assignment and unary operators to change data
- Using equality and type comparison operators to compare two pieces of data
- Using logical operators that enable us to create complex comparison statements
- Order of operations

# Objects and Arrays

> PowerShell is an ***object-oriented scripting language***, meaning that much of the data in PowerShell is in the form of an ***object***. 

In this lesson, we will dive into what an object really is, explore the properties and methods that make up an object, and even create our own objects!

In addition to objects, we will introduce a new type of data structure called an array. We will discover how to create, update and access items from an array and go over the operators we can use to manipulate an array.

## Understanding Objects

Many shells, such as the Linux Bash shell, have limited capabilities since they focus on strings as output. Plaintext output forces us to use other commands for additional functionality, such as formatting or filtering. 

On the other hand, PowerShell is an ***object-oriented language***. Since almost everything in PowerShell is an object, including the output of commands, further data processing is much easier. 

An *object* is a combination of **variables** and **functions**. Each object has the following:

- ***Properties***: variables that describe the object (characteristics)
- ***Methods***: functions that describe how to use the object (actions)

Each object is an *instance of a blueprint called a ***type***, *or class*. 

Let us describe these terms using a real-world example. Assume we have an object based on an animal called `$dog`. We can describe `$dog` using properties such as `name`, `breed`, `age`, etc. All the actions a dog can perform are methods such as `speak()`, `eat()`, `play()`, etc.

All information associated with an object is called a *member*. We can discover the members of an object with the `Get-Member` cmdlet. It also shows the type of an object. In the following example, the object is a string:

```Powershell
Get-Member -InputObject "Codecademy"
```

> A more common way to use `Get-Member` is by piping an object to `Get-Member` like so:

```Powershell
"Codecademy" | Get-Member
```

Both approaches produce the same result. In the following few exercises, we will dive deeper into the properties and methods of objects.

![The string Codecademy is pipelined to the Get-Member cmdlet. The output shows many methods and 2 properties.](https://static-assets.codecademy.com/Courses/learn-powershell/Understanding-Objects.png)

## Object Properties

