---
up: "[[Lua]]"
tags:
  - "#education/computerprogramming/languages/lua/learnlua"
---


## Welcome to Learn Lua

**What will we learn?**

In this course, we will learn programming language fundamentals with Lua syntax. The concepts covered in this course lay the foundation for using Lua in any environment.

After this course, we will be able to:

- Utilize Lua data types, built-in methods, and variables
- Use conditional logic to control the flow of a program in Lua
- Construct functions and pass data through them

# Introduction to Lua

> [Lua](https://www.lua.org/start.html) is a powerful and intuitive general-purpose programming language developed in 1993 by a team of scrappy professors at Pontifical Catholic University of Rio de Janeiro, in Brazil.

Due to a trade barrier on computer hardware and software at the time, the team couldn't buy software from outside the country. So they made their own!

Much of the inspiration for Lua came from the languages SOL (Simple Object Language) and DEL (data-entry language). In Portuguese, *Sol* means "sun" and *Lua* means "moon".

Despite it's humble beginnings, Lua is now used for:

- Building games, such as Roblox, World of Warcraft, and Angry Birds
- Building web apps, such as Venmo, Adobe
- Building developer tools with companies such as Redis

> Lua has an easy-to-read, Python-like syntax, it takes up very little space on your machine, and it can interoperate with any C code. 

### Hello World

> In Lua, `Hello World` can be printed in a single line:

```Lua
print("Hello, world!")
```

- Everything inside the double quotes will be printed to the terminal.
- The *terminal* is a window that allows people to interact with a computer program. The terminal is the black panel on the right.

### Print

We learned how to output a line of text with the following code:

```Lua
print("🚙💨")
```

Will output:


```Lua
🚙💨
```

We can also output multiple lines by adding more `print()` statements:

```Lua
print("Hello")
print("Goodbye")
```

This will output: 

```
Hello
Goodbye
```

### Comments

> Our own code can quickly become difficult to read and understand when we return to it - sometimes only a few hours later. 

For this reason, it's often useful to leave a note or reminder in our code for our future selves or other developers.

Comments can explain what the code is doing, leave instructions for developers using the code, or add any other useful annotations.

A **single line comment** will comment out a single line and is denoted by two dashes `--` preceding it.

```Lua
-- Start the program by greeting the world! Prints "hi"
print("hi")
```

You can also use a single line comment after a line of code:

```Lua
print("hi") -- Prints "hi"
```

### Multi-Line Comments

> Sometimes, we will have a section of our code that we want to temporarily disable. We can do this by using comments to "comment out" those lines.

*before*

```Lua
print("Disable me!")
print("This shouldn't happen")
print("Let the hacking begin...")
```

*after*

```Lua
--print("Disable me!")
--print("This shouldn't happen")
--print("Let the hacking begin...")
```

But what if a large number of lines need to be disabled? Going through each line and adding a single line comment would be tedious.

A **multi-line comment** will comment out multiple lines and is denoted by `--[[` to begin the comment, and `]]` to end the comment. 

```Lua
--[[ 
print("Disable me!")
print("This shouldn't happen")
print("Let the hacking begin...")
]]
```

### Review

In this lesson, we learned: 

- Lua is a general purpose coding language
- The code is read from top to bottom
- `print()` is used to output to the terminal:

```Lua
print("This... is... fun.")
```

# Data Types and Operators

All programs consist of **data** and **operations** we perform on that data. That makes data an essential thing to understand in your coding journey.

In the "real" world, we use data everyday to inform our decisions. We track data like how may eggs we have in our fridge so we know how many to buy for the next week. We look up data like how many minutes it will take to get to work so we know when to leave home. 

Moreover, data comes in more forms than just numbers. Sometimes data is more about what is true and what isn't.

Consider the weather. We either say statements of truth like "it is raining" or "it's not raining" when deciding to bring an umbrella. We could represent these choices in terms of numbers (0 means no rain, 1 means rain) but that isn't as intuitive as thinking about the rain in this "on" or "off" manner. 

> Having different forms of data allows us to better organize the information around us. In programming, this differentiation of ***data types*** is essential.

Consider how a program like Google Calendar might use different types of data:

- It uses *numbers* to represent the number of attendees in a meeting.
- It uses *text* to display the title of a meeting.
- It uses *truth statements* like "this meeting is private" to determine how new guests are invited.

In this lesson, we will learn about:

- The different types of data in Lua.
- How to check the type of our data/
- How to manipulate the data with operators.

### Categorizing Data With Types

**Data** is information stored by a computer. We need it to write even the simplest programs. The text you're reading right now is a piece of text data saved to Codecademy's servers.

As we learned in the intro, data can come in many forms(numbers, text, true/false statements, etc...) To stop the data from becoming a jumbled mess inside our computers, we must have a system to *organize* and *differentiate* the data. 

This organization is crucial because we can do different things with different data. For example, numbers and words have different purposes. There are actions we can do with numbers that we can't do with words, such as adding and subtracting. Words, meanwhile, are ideal for communicating thoughts and ideas. 

> In Lua, data can be organized into four basic **data types**, each with distinct behavior and purposes.

| Data Types | Definition                                                                                            | Syntax                                      | Example of Use                                     |
| ---------- | ----------------------------------------------------------------------------------------------------- | ------------------------------------------- | -------------------------------------------------- |
| Number     | A numeric value including positive and negative values, and decimal values                            | `10`,`3.5`,`-4`                             | To store how many followers you have on Instagram. |
| String     | A sequence of individual characters inside quotations. It can be letters, numbers, spaces or symbols. | `"This is a string"`, `'I have five cats.'` | To store your username on a website.               |
| Boolean    | A value that only has two possible values: true and fasle                                             | `true`, `false`                             | To indicate whether you have dark mode on or not.  |
| Nil        | A representation for the absence of a value. If there is no value, it is nil.                         | `nil`                                       | To indicate an empty box on a fillable form.       |
### String and Number Syntax

> Letters and numbers in real life are easy to differentiate, but in programming, there is more to it than meets the eye.

Previously, we introduced the definition of a string type and number type:

- ***Number***: A numeric value including positive values, negative values and decimal values.
- ***String***: A sequence of individual characters inside quotations. It can be letters, spaces, numbers or symbols.

Strings cna be created using double quotes (`"`) or single quotes (`'`), it's up to you (as long as they match). Both of these are valid strings:

```Lua
print("Hello, World!")

print('Hello, World!')
```

To include single and double quote characters in your string, use `\` in front of the character you want to include:

```Lua
print("\"What? Like it's hard?\" - Legally Blonde (2001)")
```

> Since a string can include, letters, numbers, symbols, and spaces, it makes strings *the most flexible type for representing any type of data*.

However, that does not mean we should represent every piece of data with a string. Remember, we categorize data into types so we know what we can do with them.

For instance, the string `"100"` is not the same as the number 100. They may look similar, but they're not the same at all. The computer would interpret the string `"100"` as the combination of three characters `"1"`, `"0"`, `"0"`, rather than as the number `100`.

Similarly, the boolean value `true` is distinct from the string `"true"`, just as `"nil"` is different from the `nil` value.

To discover the type of data you are working with, you can use the `type()` function.

```Lua
print(type("What am I?"))
```

### Calculating with Arithmetic Operators

> it wouldn't be much of a program if we couldn't do something with all the data we've collected. The fun comes from taking the data and transforming it into something else. 

The most basic transformations are arithmetic. In fact, the first computers were created to automate mathematical calculations.

Suppose we want to write a program that can estimate how far a car is from a place or a program that calculates a user's shopping cart total. How can we make that possible? At the heart of it all are ***arithmetic operators.*** 

An **operator** is a special character that transforms data. Arithmetic operators are characters that help us perform calculations such as addition, subtraction, multiplication, and division.

|Operator Name|Description|Syntax|Example|Result|
|---|---|---|---|---|
|Addition|Adds two numbers|x + y|5 + 2|7|
|Subtraction|Subtracts two numbers|x - y|5 - 2|3|
|Multiplication|Multiplies two numbers|x * y|5 * 2|10|
|Division|Divides two numbers|x / y|5 / 2|2.5|
|Exponential|Takes the exponent of two numbers|x ^ y|5 ^ 2|25|
|Remainder  <br>(also known as modulo or modulus)|Gives us the remaining leftover number after we’ve divided two numbers.|x % y|5 % 2|1|
|Negation|Reverses the sign value of the number.|-x|-(3+2)|-5|
> When we use an operator to transform data, we call it an **expression** that **evaluates** data.

# Review

Hurray! You’ve reached the end of this lesson.

Before you go, let’s review what you’ve learned:

- Programs use **data**. *Data has an associated **data type**. *Data types determine what we can do with the data.
- The four basic [data types](https://www.codecademy.com/resources/docs/lua/data-types) are:
    - **Number**: A numeric value.
    - **String**: A sequence of characters, often used for text.
    - **Nil**: A value that represents the absence of value.
    - **Boolean**: A value that can be either true or false only.
- A **string** can look like many other data types, but data is a string only if the value is surrounded by matching single or double quotation marks.
- We can use **arithmetic operations** on number data.
- The arithmetic [operators](https://www.codecademy.com/resources/docs/lua/operators) are `+`, `-`, `*`, `/`, `^`, `%`, `-`.
- Transformations by arithmetic operators result in an **expression**. Expressions are code that can be **evaluated** to a resulting value.
- Whenever we’re unsure what data type a value has, we can use the [`type()`](https://www.codecademy.com/resources/docs/lua/mathematical-library/type) function to help us figure that out.

You’ve now learned about one of the fundamental building blocks of programming. Keep going and discover what you can do with this knowledge!

### Instructions

To further practice your skills, consider these challenges:

- Try using `print()` to print onto the output a value of each basic data type that you don’t already have in your code.
- Modify the `print()` statements you made by adding arithmetic operators or changing the data type by converting them into the string data type
- Test your knowledge by outputting the type of each of your values after you’ve made modifications!

# Variables

### Introduction to Variables

> Variables help make programs changeable and adaptable. Without variables, it would be impossible to create most programs. 

Suppose we are programming a scoring system for a game. Since the program needs to remember the current score and flexibly change it throughout the game, a variable can help us out. 

Suppose we have two players, we'll need to create two variables. 

```Lua
player1Score = 0
player2Score = 0
```

The basic syntax for declaring a variable is: `name = value`. In this example, two variables are created with the name `player1Score` and `player1Score`. We assigned the number value `0` to each variable using an (`=`). Each variable will start with the `0` value. 

But like scores in a game, each variable's value will changes as the players earn points.

Once we've assigned the value `0` to each variable, the variable names now represent `0`. We can access the values inside of variables by using their variable names, so rather than writing:

```Lua
print(0)
--output: 0
```

We can directly reference the variable with

```Lua
print(player1Score)
--output: 0
```

We should strive to name variables succinctly but descriptively so that when we look at them, it is easy to understand their purpose. For example, a variable named `myValue` does not tell us what kind of value that variable holds, while `player1Score` gives us a lot more info.

# Using type() With Variables

> We know that data is the building block of programs. To organize and differentiate data, we categorize it into data types. 

This helps us understand what we can and cannot do with the data that we have.

As a refresher, let's look at each data type we've learned so far:

***Number***: A numeric value including positive values, negative values and decimal values.

***String***: A sequence of individual characters inside quotations. A string can be a collection of letters, spaces, numbers or symbols. 

***Boolean***: A value that only has two possible values: true or false.

***Nil***: A representation for the absence of a value. If there is no value, it is nil. 

Variables can store any type of data, and Lua has a familiar built-in function to discover what kind of data it's string!

Previously, we were able to use `type()` to find the data type of our data values. We can also use `type()` on variables to find the data type of its value.

```Lua
catchphrase = "Avengers Assemble!"
print(type(catchphrase))
-- output: string
```

# Variable Reassignment

> Like boxes, variables are a great container for things. But what else can we do with boxes that we can also do with variables? Change the content inside!

After we've declared a variable and assigned it a value, we can change that value if we need to. The variable name will continue to represent that piece of data, even after the data value has been changed. 

Going back to our scoring system code for our game, we created a `highestScore` variable which (according to its name) stores the number that represents the absence of value, as there is no highest score yet:

```Lua
highestScore = nil
print(highestScore)
-- output: nil
```

If a player does achieve the highest score, we can **reassign** the existing `highestScore` variable to a new value. 

```Lua
highestScore = nil
print(highestScore)
--output: nil
highestScore = 25
print(highestScore)
--output: 25
```

> Reassignment looks identical to creating a new variable. Notice that the `highestScore` is printed on lines 2 and 5, each time with different values. Initially, `highestScore` is `nil`, and later it is reassigned to `25`. Any code that includes the variable name will be working with the new value. 

We can also assign variables to the value of another variable like this:

```Lua
legendaryPlayerScore = 616
highestScore =  legendaryPlayerScore
print(highestScore)
--output: 616
```

Since variables in Lua do not have a type - it is just a container for data - you can reassign a value of any data type to a variable. Be careful with this feature of Lua. Accidentally changing the type of a variable is easy and can lead to trouble down the road. 

For example:

```Lua
highestScore = 24
print(highestScore + 1) --output: 25
highestScore = "Kamala"
print(highestScore + 1) -- error: attempt to add a 'string' with a 'number'
```

# Using Arithmetic Operators With Variables 

> The "compute" part of "computer" means we cannot leave what computers do best out of this lesson!

We can compute new values for our variables with arithmetic operators.

This is useful when we work with values that need to be numerically changed. Let's take a look at this in action:

```Lua
player1Score = 0
player1Score = player1Score + 1
print(player1Score)
```

This syntax may look a but strange at first. Let's break it down.

- Recall that `=` means you're assigning what is on the right of `=` to the variable on its left. 
- To understand this, we need to evaluate the expression on the right first (`player1Score + 1`), then reassign it back to the left variable (`player1Score`).

	- On the right is `playerScore + 1`
	- We first access the value of `player1Score` that is currently at `0`.
	- Replace `player1Score` with its current value and we get `0 + 1` which equals `1`. 
	- Then, the `=` assigns the new value back into `player1Score`
	- Now, `player1Score` will have a new value of `1`.

If we were to add the same line of code again with the newly updated value, what do you think it will be?

```Lua
player1Score = player1Score + 1
print(player1Score)
```

Since `player1Score` starts out with `1` from the previous calculation, adding `1` to the variable means `1 + 1`. `player1Score` will now have the number `2`!

Other arithmetic operators work with variables too - see the example below and [Lua’s documentation](http://www.lua.org/manual/5.1/manual.html#2.5.1):

| Operator       | Example                     |
| -------------- | --------------------------- |
| Addition       | myVariable = myVariable + 1 |
| Subtraction    | myVariable = myVariable - 1 |
| Multiplication | myVariable = myVariable * 1 |
| Division       | myVariable = myVariable / 1 |
| Exponentiation | myVariable = myVariable ^ 1 |
| Remainder      | myVariable = myVariable % 1 |
| Negation       | myVariable = -myVariable    |
# Concatenation

> Thus far, we've manipulated our variables with arithmetic operators or reassigned their values completely.

We can also combine a variable's value with other values to form a new string. ***Concatenation*** is the act of joining values (often strings of numbers) together. To do this, we use the concatenation operator (`..`)

Observe this example:

```Lua
print("The current player with the highest score is " .. "Bruno")
--output: The current player with the highest score is Bruno"
```

> We concatenated two string values together and it produced a larger string output.

Concatenation becomes useful when we need changeable or reusable output with different values. Observe this example again, but with a variable:

```Lua
highestScorerName = "Bruno"
print("The current player with the highest score is " .. highestScorerName)
--output: The current player with the highest score is Bruno
```

*Note*: Concatenation produces a whole new string to the output and does not modify the values used to create it. 

# Type Coercion in Concatenation and Arithmetic Operations

> Buckle in and put your thinking caps on! We think you're ready for a tricky challenge.

Suppose we need to use concatenation to make a result that mixes different data types such as a number and a string like this:

```Lua
highestScore = 25
print("The highest score is: " .. highestScore)
```

What do we think the output would be? 

In Lua, these situations are handled with automatic **type coercion**. Type coercion is the conversion of a value from one data type to another. Lua does this automatically and converts a string to a number or a number to a string depending on what is needed.

With type coercion, the *number* value `25` will be coerced into a *string* data type. Thus, it will work with the concatenation operator and string to produce `The highest score is: 25`.

Type coercion extends to arithmetic operators too. Chew on this example for a bit:

```Lua
print("100" + 5)
```

**Answer**: `105`. `"100"` is a string data type coerced into a number data type. Thus, the expression becomes `100 + 5` thanks to the presence of the addition operator. 

And for the last one:

```Lua
print("100" + 5 .. 6)
```

**Answer**: `1056`. The expression is evaluated from left to right. From the last example, we know `"100" + 5` evaluates the number `105`. But, the concatenation operator (`..`) coerces both `105` and `6` into string data types and produces `1056`.

As we can see from these examples, Lua's type coercion is a convenient tool that helps us deal with ambiguous expressions. However, it can get quite tricky. The answers may not have been what you expected since it's not always clear how Lua interprets these expressions.

If we want to be clear with our expressions, we can convert with functions `tonumber()` and `tostring()` when we are mixing data types. For example:

```Lua
highestScore = 25
print("The highest score is: " .. tostring(highestScore))
--output: The highest score is: 25
```

> Notice that we've used `tostring()` to convert `highestScore` to a string to output the same string. But, the benefit is that we're now being really clear about what type coercion is happening. 

To learn more about the built-in functions `tostring()` and `tonumber()`, visit [tostring()](https://www.lua.org/manual/5.1/manual.html#lua_tostring) and [tonumber()](https://www.lua.org/manual/5.1/manual.html#lua_tonumber) in the Lua documentation.

### Review

Here's what we've learned about variables:

- A **variable** is a container in the computer's memory that helps us store, retrieve, and manipulate data.
- A variable an store data values of different **data types**. To find the data type of the data inside a variable, we can us `type()` with the name of the variable.
- To define a variable, we give the variable a name, followed by the equal sign (`=`), and the value the variable should store.
- We can change the value in a variable by **reassigning** it to variable should store.
- The **concatenation** operator (`..`) allows us to join values together and results in a string.
- When different data types are combined with concatenation or arithmetic operators, values are **coerced** into the appropriate data type.

# Mystic Moon Potion Shop Project

