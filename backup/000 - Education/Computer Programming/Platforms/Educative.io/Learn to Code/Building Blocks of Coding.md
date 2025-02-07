# You Are Hired for a Python Project

### The Scenario

> You receive an email from a long-forgotten client. They want you to undertake a Python project for them. To complete it, they have sent you all the project details you require via email. Here's what you know about your role and the projects requirements.
#### Your Role

You are being hired as a Python software engineer. You are required to understand the project requirements and translate them into Python code. On successful delivery of the project, you will be considerably compensated.
#### Project Description

Your client wants an **app** that will be used by students in a network of elementary schools. As the end-users of your app, these elementary school students will be able to exercise their basic math skills. 

The app will pose random maths questions to the students and check if they have entered the correct answers.

The client intends to improve their student's math competency through the app. 
# Function of a Python Program

> Before we get to learn how to code, let's understand the foundational unit of a computer program.

- What is a computer program made of?
- Using functions
- Let's get our hands dirty with Python
- What's next
### What is a Computer Program Made Of?

There is a basic structural and foundational unit of everything that exists. The basic unit of matter is an **atom**. The basic unit of living things is a **cell**. 

As far as this course is concerned, the foundational unit of a computer program is known as the ***function***. 

As it's name implies, each function is designed to execute a specific and crucial task, providing a modular and organized approach to constructing and maintaining code. 

- As we delve into this course, understanding the significance of functions will be key to mastering the art of *procedural programming* in Python. 

A **function has three components:**

1. ***Input***: The data that the function has to work on
2. ***Processing***: The steps and operations necessary to achieve the function's objectives.
3. ***Output***: The result or the information that the function computes after processing the input.
### Using Functions

> Python provides it's users with ***built-in functions*** that carry out some useful tasks. 

The processing part of built-in functions is hidden from us, as Python takes care of that on our behalf. We are only concerned with what we feed them as input and what they give us as the output. 

Let's take Python's built-in function `round` as an example. 

- It takes a fractional value (3.1415) and rounds it off to the nearest whole number. The widget below helps us visualize how this function works.

The `round()` function is the type of function that must take a single input, but some functions may require multiple inputs or no inputs at all. An example of a function that takes two inputs is the `pow()` function that calculates the power of a number. 

- The two inputs are the base and the exponent, and it returns the result of rasing the base to the power of the exponent, e.g. 10^2 = 100.
### Getting our Hands Dirty With Python

> To use any function in Python, we must **make a call to it**. This can be done by writing the name of the function, followed by a set of parenthesis `()`.

Inside the parenthesis, we can *provide the inputs* to the function. 

To give multiple inputs to a function in Python, the values must be separated by commas. The code below shows how it's done for `pow()`

```python
pow(2, 3)
```
# Compute and Output

> Learn how to display data on the computer screen.

- [The built-in print() function](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/4987992782536704#The-built-in-print-function)
- [The project requires printing on the screen](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/4987992782536704#The-project-requires-printing-on-the-screen)
    - [Printing the score](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/4987992782536704#Printing-the-score)
    - [Printing a text message](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/4987992782536704#Printing-a-text-message)
    - [Concatenating the text](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/4987992782536704#Concatenating-the-text)
    - [Printing the text message and score together](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/4987992782536704#Printing-the-text-message-and-score-together)
- [Test yourself](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/4987992782536704#Test-yourself)
- [](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/4987992782536704#The-next-project-requirement)
### The Built-In `Print()` Function

> We have already seen some built-in functions, and we know that a function does the following things:

1. It takes something as it's input
2. It processes this input to create some output
3. It returns the output

The most prominent Python built-in function that prints something on the screen is `print`. It prints anything we give it as input on the screen. 

- For instance, guess the result of the following code when you press the run button:

```python
print(3.1415)

>>> 3.1415
```

It simply prints the exact number you gave as an input to the `print` function. This function gives us the power, as a programmer, to verify what the computer has done for us. 

- For example, we know what the built-in function `round` is supposed to do. 
- It takes any number with a decimal point and rounds it the nearest whole number, meaning 3.1415 should get rounded to 3. 

```python
round(3.1415)
```

> There wasn't any error, and the computer seems to have done it's job, but we couldn't really confirm if there `round` function worked as we expected. So, what happens if we use `print` and `round` together?

We know by now that a method can take an input, do something with, and return a processed output. The method named `round()` can take as input `3.1415`, process it to truncate the number to the nearest whole number, and then return the whole number `3`.

Is there a way for us to take all of what `round` as a method does and give that as input to the `print` method? Study the code below carefully, and then run it to see the output:

```python
print(round(3.1415))

#Output: 3
```
### The Project Requires Printing on the Screen

> Let's attend to our client's requirements for the project, armed with out new Python knowledge. There are at least three major project requirements (2, 3 and 9), from the following, that will use our knowledge of the `print()` function.

### Concatenating the Text

We know what the `+` operator does for numbers. We have seen that Python also knows the meaning of `+`. But here is where the similarity ends. Can you think of another way the same `+` can be used for two text messages? For example, what would be the result of:

```Python
"You have managed" + "to score 10 marks"
```

The output would be `You have managedto score 10 marks.` Python ate up the space between 'managed' and 'to'. 
#### Take Away:

> The meaning of `+` is slightly different for text. Python concatenates or joins two pieces of text with `+`. 

- Another lesson here is that there seems to be multiple ways of achieving results in Python, just as it is in life. 
### Printing the Text Message and Score Together

```Python
print("You have managed" , "to score 10 marks")

# Output: You have managed to score 10 marks
```

> In this arrangement, we can see that Python lets us use a comma-separated print function.

We know some functions can take two inputs, such as a **power function** (`pow(10,2) means 10 raised to the power of 2, which is 100`).

The same is the case with print. Python let's us give as many inputs (separated by commas) to the print function as we require. This comes in handy because we can ask it to print two things for us in a row, or however many we want. *We can also ask it to print a message as well as a number, separated by commas:*

```Python
print("First message" , "Second message", 1, 2, 3, "Third message")

# Output: First message Second message 1 2 3 Third message
```

> This gives us the power to fulfill another project requirement. Let's imagine that we want to tell the learner about what the correct answer to a question is, but we want the computer to work it out for us because we know it's flawless in computing sums. 

```python
print("The correct answer for 8 + 2 is:", 8 + 2)
print("The correct answer for 816234 + 256423 is:", 816234 + 256423)

# Output: The correct answer for 8 + 2 is: 10
# Output: The correct answer for 816234 + 256423 is: 1072657
```
# Input and Assign to a Variable

> Let's see how we can take input from a user and save it for later use

- [Taking input from a user](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/5570397411082240#Taking-input-from-a-user)
- [The built-in input() function](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/5570397411082240#The-built-in-input-function)
    - [How does the user know what they are required to input?](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/5570397411082240#How-does-the-user-know-what-they-are-required-to-input)
    - [Where has the user’s input gone?](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/5570397411082240#Where-has-the-users-input-gone)
    - [Variable assignment](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/5570397411082240#Variable-assignment)
- [The fulfilled project requirement](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/5570397411082240#The-fulfilled-project-requirement)
- [Exercise](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/5570397411082240#Exercise)
### Taking Input from a User

> Let's continue making our way into Python and the project. Notice that project requirements 1 and 5 are categorically different from requirement 2, which is printing something to the screen.

Now we know how to print a name on the screen using Python, but how does our code ask the elementary school student to tell us their name?
### The Built-in `input()` Function

> Just like `print` prints something on the screen, what would the name be of the built in funciton that takes input from the user's keyboard?

Python offers us another built-in function with the name of `input`.

```Python
input()
```

> Notice there is only one line of code, and it says `input()`. We ran the code, and then, you typed in something. 
> 
> 	While we were typing, of course, you could see on the black command line, each letter that you pressed on the keyboard. 

As soon as you hit enter, the code stops executing as the Python program completes it's run. It did what it was set out to do, it let the end-users use their keyboard to give it input. 

But this raises two important questions. 

1. *Where has the user's input gone, really?*
2. *In a real app, how does the user know what the app wants them to enter?*
### How Does the User Know What They Are Required to Input?

> From the end user's perspective, how are they supposed to know if they have to enter a name, a number, or something else?

The Python `input()` function allows us to prompt the user with a question or a message.

```python
input("Please tell us your name: ")
```

`input()` is a built-in function that can take an optional message within it's parenthesis as well.
### Where has the user’s input gone?[#](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/5570397411082240#Where-has-the-users-input-gone) 

Now, the user knows what the code wants them to input, that’s one issue out of the way. But what about the input from the user? We need to be able to welcome, by name, any student who is using our app. Can we use the `print()` function in tandem with our newly learned `input()` function?

```python
print(input("Please tell us your name: "))
```

> We have taken the previous code and placed it nicely inside a `print` function. When we run the code, it first takes input from our keyboard and prints whatever name we entered. 

This means that the input isn't getting lost. The `input()` function does return the input as a text message that gets passed into the `print()` function to output on the screen.

This gives us great power because *now our code is dynamic*. We don’t have to write the name of the student inside our code’s print statement just to be able to fulfill project requirement 2. Instead of writing a separate app for Alex, Betty, Catherine, Dania, and so on, we have a code that can, in a single line, welcome anyone in a personalized way.

Let’s imagine the following interaction between our app and its user, Alex:

```
Hi Alex! Welcome to the math quiz.

Alex, can you answer the following questions?
.
.
.
.
.
Congratulations Alex, on scoring 5 marks!
```

> Using `print(input())`, we can surely pull off the first line, but how can we print the second and the last personalized output on the screen inside of one program?

We don't want to write a Python code that only works for one person. 

- And, in case we ask the user to tell us their name three times in a single session, they will not appreciate such a forgetful app. 
### Variable Assignment

> We now know that `input()` returns the users response from the keyboard, and instead of passing that toward the `print()` function, Python also lets us save the user's response in the computer's memory. 

Python lets us name that memory. The programming community calls these **variables**. We can assign a value to a variable using `=` and finally, we can use this variable *as many time as we want to in our code*. 

```python
user_name = "Alex"
```

> **Variables** are *case-senstive* in Python, i.e. it makes a difference to Python if the letters of your variables are in upper or lower case. Whatever choice we make, it is important to be consistent throughout our code wherever that variable is used. 
> 
> Secondly, the variable will always come on the left-hand side of the assignment operator.
### Fulfilled Project Requirement

We can now use our variable as many times as we want in our code, as required by the project. 

```Python
user_name = "Alex"
print("Hi", user_name, "! Welcome to the math quiz.")
print(user_name, ", can you answer the following questions?")
print("Congratulations", user_name, ", on scoring 5 marks!")
```

> Changed code so that anyone can use the app, not just Alex.

```python
user_name = input("Enter your name here: ")
print("Hi", user_name, "! Welcome to the math quiz.")
print(user_name, ", can you answer the following questions?")
print("Congratulations", user_name, ", on scoring 5 marks!")
```
# User- Defined Functions and Data Types

## Arithmetic Operators and Data Types

- [Back to our project](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/4763342026702848#Back-to-our-project)
- [Adding two numbers](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/4763342026702848#Adding-two-numbers)
    - [The data types and their conversion](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/4763342026702848#The-data-types-and-their-conversion)
        - [The int() function](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/4763342026702848#The-int-function)
        - [The str() function](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/4763342026702848#The-str-function)
- [Arithmetic operations](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/4763342026702848#Arithmetic-operations)
    - [The arithmetic operators in Python](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/4763342026702848#The-arithmetic-operators-in-Python)
- [Review of the lesson](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/4763342026702848#Review-of-the-lesson)
### Back to Our Project

> So far, we have covered good ground in learning how to code for some project requirements. 

According to requirements 4 and 6, our project must be able to:

- Perform calculations of addition, subtraction, multiplication, and division.
- Compute the actual answer to each question.
### Adding Two Numbers

This should be easy: input two numbers and assign them to `num1` and `num2`, the print `num1 + num2`. Run the program below and see if we're getting the expected output.

```python
# Taking two numbers as input and storing inside two variables respectively
num1 = input("First number: ")
num2 = input("Second number: ")

# Displaying the result
print("The answer to ", num1, "+", num2, "is ", num1 + num2)
```

> The output of this code combines the two numbers into one, so if you entered 5 and 7, it would output 57. That is not the desired behavior. Why do we think that is?
### Data Types and Their Conversion

In our code: 

1. When we use `input()`, it takes whatever we type and stores it as a **string**. So, the numbers stored in `num1` and `num2` are treated as text and *not* as mathematical numbers. 

In Python, `str` is a basic data type used to represent text or sequences of characters (string). It is employed for storing and manipulating words, sentences, or any textual information in a program. Strings are enclosed in double quotes `" "`

2. When we try to add `num1` and `num2` using the `+` operator, it **concatenates** the two strings rather than adding the numbers. That is why we got `82` instead of `10`. 

To solve this problem, we need to convert these strings to numbers ( to another basic data type called **integer**), so the computer understands that we want to do math with them.

> An integer is a whole number, either positive or negative, without any decimal or fractional parts.
### The `int()` Function

> Python's built-in function `int()` lets us do just that. It can take a number in string format as input, and output an integer version of it. 

```Python
# Taking two numbers as input and storing inside two variables respectively
num1 = input("First number: ")
num2 = input("Second number: ")

# Converting input strings to integers
num1 = int(num1)
num2 = int(num2)

# Displaying the result
print("The answer to", num1, "+", num2, "is", num1 + num2)
```

> Running the code above gives us the expected result we were originally looking for. So the `int()` function helps us convert a string to an integer.

**Note**: it's always a good idea to convert the `str` input from the keyboard to `int` in case of numbers.
### The `str()` Function

> Conversely, we could encounter a situation where we may want to convert an integer into a string. We can do that using Python's `str()` function which can take an integer as an input and output a string version of it.

Example program below:

```python
# Data for the mathematical expression

num1 = 12
num2 = 7
op = "+"

question = "What is" + num1 + op + num2 + " ? "
result = num1 + num2
print(question)
print("Result = " , result)
```

> Here, we have integers (`12` and `7`), that we're trying to include in a message. Running the code above gives us a **TypeError** in line 6 because we're trying to concatenate strings to integers, which is not allowed. 

- To fix this, we need to covnert the integers to string using the `str()` function and then concatenate them as usual. 

```python
question = "What is " + str(num1) + " " + op + " " + str(num2) + "?"
```

> If we replace line 6 with the code above, we'll get the expected output. Converting an integer to a string allows us to combine it with text and display it as part of a message. 

**Note**: It's always a good idea to convert the `int` to `str` in case text output needs to be formatted.
### Arithmetic Operators

> Now that we've covered the concepts of basic data types, like `int` and `str`, and how to convert each data type to another, let's get back to the project requirements.
#### The Arithmetic Operators in Python

> In Python, arithmetic operators are special symbols that perform operations on variables and values, just like when solving simple arithmetic equations.

For numbers, we have already seen how the `+` operator add two numbers together. 

Other arithmetic operators available in Python are `-` for subtraction, `*` for multiplication, and `/` for division.

```python
num1 = 7
num2 = 3

print("7 + 3 is", num1 + num2)

print("7 - 3 is", num1 + num2)

print("7 * 3 is", num1 * num2)

print("7 / 3 is", num1 / num2)
```

> You may have noticed that we are getting the last output as a fractional value, and rightly so. 

Just like we have an `int` data type for whole numbers, we also have a basic data type for numbers with decimal values like 2.333 known as `float`.

In Python, the division operator `/` between two integers *results in a float value, even if the division should logically yield an integer.* This behavior is consistent with the idea that a division operation can produce a fractional result. 

```python
# division
print(6 / 3)

# 2.0
```

> In this case, the division `6 / 3` results in a floating-point value `2.0`. When we perform division with numbers in Python, the division operation produces a float even if the result is a whole number. 

- The `.0` at the end indicates that it's a floating point number.

Now if we want to ensure that the result is an integer, then we can use the `int()` function to make sure the result is an integer:

```python
#Converting the result to an integer by truncating the decimal part
print(int(6 / 3))
print(int(7 / 3))

# 2
# 2
```

> The division is performed, resulting in a floating point value `2.33333333333335`. The `int()` function is then applied to this value. This function converts the number to an integer by truncating the decimal part, resulting in `2`.

In the program below, let's take the user's answer and then print its correct answer (calculated by our program).

```python
n1 = 33
n2 = 4

question = "What is " + str(n1) + "+" + str(n2) + "?"
user_answer = input(question)
print("Your answer is:", user_answer)
#computing the correct answer
print("The correct answer is:", n1 + n2)
```

```shell
root@educative:/usercode# python3 main.py
What is 33+4? 37
Your answer is: 37
The correct answer is: 37
```

> We can do the same for all of the operators below:

```python
n1 = 33
n2 = 4

question = "What is " + str(n1) + "+" + str(n2) + "? "
user_answer = input(question)
print("Your answer is:", user_answer)
# Computing the correct answer
print("The correct answer is:", n1 + n2)

question = "What is " + str(n1) + "-" + str(n2) + "? "
user_answer = input(question)
print("Your answer is:", user_answer)
# Computing the correct answer
print("The correct answer is:", n1 - n2)

question = "What is " + str(n1) + "*" + str(n2) + "? "
user_answer = input(question)
print("Your answer is:", user_answer)
# Computing the correct answer
print("The correct answer is:", n1 * n2)

question = "What is " + str(n1) + "/" + str(n2) + "? "
user_answer = input(question)
print("Your answer is:", user_answer)
# Computing the correct answer
print("The correct answer is:", n1 / n2)
```

> Since our project is for elementary school students, let's now expect them to compute the fractional parts of the division questions. How about we convert the actual answers to keep only the integer part of the answers?
### Review of the Lesson

> To sum up, we learned some of the built-in functions `int()` and `str()` in Python, which made it possible for us to compute correct sums. You might begin to think that Python has a built in function for every situation in the world. That is not true, and it's a good thing too.
# User-Defined Functions

> We know that built-in functions `input()`, `print()`, `int()` etc. are like standard ready to cook recipes everyone knows how to use. 

Since there cannot be a ready-made function for every need in the world, Python let's us create our own functions that we can use whenever required, just like we can use built-in functions.

---

### Why Make User-Defined Functions?

**Reuse of Code**: once we've written a function to perform a specific task, we can resue it in different parts of our program. This avoids duplicating code and promotes a more efficient and maintainable code. 

**Readability**: Functions make our code more readable by giving meaningful names to blocks of code that perform a specific operation. This makes it easier for us and others to understand the purpose of each part of the program. Instead of looking at a large block of code, we can just see the function name and understand what it does.

**Modularity**: Functions allow us to break down a complex problem into smaller, manageable pieces. Each function can perform a specific task, making the overall code more modular. It's like having a toolbox with different tools. *Each function is like a tool that performs a specific job, and we can combine these tools to built a complete project.* 

**Abstraction**: Functions allow us to abstract away the details of how a specific task is accomplished. This we saw with built-in functions by just calling them and not worrying how it achieves the results. This separation of concerns makes it easier to focus on high-level design without getting bogged down in implementation details. 

---

> All-in-all, functions help create *modular and reusable code*, such as displaying a standard message, generating random numbers, or performing other pre-defined tasks. 
### What are User-Defined Functions?

Here is the basic structure of a function:

```python
def function_name(parameter1, parameter2):
	#function body
	# ...
	return result
```

We use the `def` keyword to define the function, followed by the function name and a set of parenthesis. The parenthesis may contain parameters, and a colon `:` at the end of the line that indicates the start of the **function body**. 

The `return` keyword is used to specify the value that the function should return.
### An Analogy for Functions

> A recipe has ingredients and a set of steps. In Python, a user-defined function has parameters (like ingredients) and a set of instructions (the code inside the function). 

```python
def order_pizza(pizza_type, extra_topping): #function definition
	#function body
	pizza = "Make a " + pizza_type + " pizza with " + extra_topping + "."

#call the function to order a pizza
first_pizza = order_pizza("Pepperoni", "Extra Cheese")
print(first_pizza)

second_pizza = order_pizza("Chicken_Fajita", "Extra Olives")
print(second_pizza)
```

- Lines 1-4 contain the function definition:
	- THis is like creating the title (name of the function, `order_pizza`) and a list of ingredients for your recipe (`pizza_type, extra_topping)`.When we define a function, we are *creating a reusable block of code with a specific purpose.* This is an abstract representation of what the function does. 
	- It's like creating a blueprint or a recipe for a certain task without actually executing it. Notice the extra spaces or indentation at the start of **line 2-4**, that's how Python knows what part of your code is part of the `order_pizza` function.
- Line 3 is the function body:
	- These are the *steps or instructions to follow* that turn the inputs (`pizza_type, extra_topping`) into the output (`pizza`). 
- Lines 7 and 10 are the function calls made to our own function that we defined earlier:
	- T*his is like using our recipe to make a specific dish.* When we call a function, we provide actual values (arguments) for the parameters defined in the function. The function then executes using these specific values. 
	- Notice how we used the same function call to give us two different pizzas. This is what we the reusability of code means.
### Creating a User-Defined Function

> Let's define another user-defined function, `add_numbers` that returns the sum of `num1` and `num2`. Run it once to see if the function is working as expected.

```python
def add_numbers(num1, num2):
	#body of the function
	sum_result = num1 + num2
	return sum_result
	
#functionc all
add_numbers(32, 12)
```

The above function should run fine, but no result is printed. Adding `print(add_numbers(32, 12))` will print the function to the console.

```python
n1 = 6
n2 = 7

question = "What is " + str(n1) + "+" + str(n2) + "? Ans: "
user_answer = input(question)
print("Your answer is:", user_answer)
# Compute the correct answer
print("The correct answer is:", n1 + n2)

question = "What is " + str(n1) + "-" + str(n2) + "? Ans: "
user_answer = input(question)
print("Your answer is:", user_answer)
# Compute the correct answer
print("The correct answer is:", n1 - n2)

question = "What is " + str(n1) + "*" + str(n2) + "? Ans: "
user_answer = input(question)
print("Your answer is:", user_answer)
# Compute the correct answer
print("The correct answer is:", n1 * n2)

question = "What is " + str(n1) + "/" + str(n2) + "? Ans: "
user_answer = input(question)
print("Your answer is:", user_answer)
# Compute the correct answer
print("The correct answer is:", int(n1 / n2))
```

> When writing **lines 4, 10, 16 and 22**, we are more likely to make a mistake. For example, we could miss a `+` character, or fail to convert the integer to a string by mistake. It's may more convenient and safe if we make a function to create a question and use that wherever we need it. 

- Also, note how the lines of code, to print the expected and the actual answers, are repeating. So, they can be made into a function. Look at the code to see what we mean. 
### A Code With Functions

```python
def print_question(num1, op, num2): #function definition to print question
	print() #to add a new line for output's readability
	question = "What is " + str(num1) + op + str(num2) + "?"

def answer_feedback(user_ans, correct_ans): # Function definition to print answer feedback
	print("Your answer is:", user_ans)
	print("The correct answer is:", correct_ans)

n1 = 6
n2 = 7

print_question(n1, "+", n2) #Function call with definite arguments
user_answer = input("Ans: ")
correct_answer = n1 + n2
answer_feedback(user_answer, correct_answer)

print_question(n1, "-", n2)
user_answer = input("Ans: ")
correct_answer = n1 - n2
answer_feedback(user_answer, correct_answer)

print_question(n1, "*", n2)
user_answer = input("Ans: ")
correct_answer = n1 * n2
answer_feedback(user_answer, correct_answer)

print_question(n1, "/", n2)
user_answer = input("Ans: ")
correct_answer = int(n1 / n2)
answer_feedback(user_answer, correct_answer)
```

> There's a difference between defining a function in abstraction and calling the function with definite arguments. We can define a function once and call it with different arguments in various parts of our program. 
# Recover From Errors

> In this lesson, we'll look at some of the common errors that we as programmers make and how to watch out for them. So, let's begin.
### Bugs

Following proper syntax and sequence is imperative when writing code. 

But, we all make mistakes, and it is not uncommon to run into errors while we code. Errors and flaws in code and its functionality are called `bugs`.

The two most common types of bugs are called `syntax errors` and `logical errors`.
### Syntax Errors

> Syntax errors occur when the code does not conform to the syntax rules of the programming language. These errors prevent the program from running. The code below provides an example of a syntax error in our code.

```python
# Initialize a variable 'full_name' with an empty string
full_name = ""

# Prompt the user to enter their first name and store it in the 'first_name' variable
first_name = input("Enter your first name: )"

# Prompt the user to enter their last name and store it in the 'last_name' variable
last_name = input("Enter your last name: ")

# Concatenate the names with a space in between and store the result in 'my_name'
full_name = first_name + " " + last_name # The `+` symbol can be used to combine two strings.

# Display a message with the user's full name using the 'full_name' variable
print("My name is", full_name)
```

> The syntax error in this code is on line 5, where the quotation mark is outside of the parenthesis of the input function.

- Fixing this error will allow the code to run correctly. 
### Logical Errors

> There are more subtle and challenging bugs to detect, like logical errors. 

Unlike Syntax errors, a logical error won't prevent the code from executing, but the program produces unexpected results. The following example demonstrates a case of logical error in the code:

```python
def calculate_rectangle_area(length, width):
    area = 2*(length + width)
    return area
    
area_rect = calculate_rectangle_area(5, 8)
print("The area of the rectangle is: ", area_rect)
```

> Here, we have used an incorrect formula and though it executes fine, the result is incorrect. THe correct formula for the area of a rectangle is `length * width`.
### Important Points to Consider

Here are some of the important points to consider:
#### Indentation in Python

- In Python, **indentation** is crucial for indicating the scope of code blocks as Python uses the level of indentation to determine the structure of the code. 
- The standard convention is to use four spaces for each level of indentation.
- Consistent indentation is necessary for the code to be syntactically correct and for scoping to work as intended.

```python
def calculate_rectangle_area(length, width):
    area = length * width
return area

rect_area = calculate_rectangle_area(5, 8)
print("The area of the rectangle is: ", rect_area)
```

> If we look closely enough, the `return` statement is not indented to be part of the `calculate_rectangle_area` function block. Therefore, when we try to return the `area` variable outside the function definition, it results in an error because `area` is not defined outside the scope. 

- Forgetting to indent code within a block can lead to indentation errors.
- Indenting inconsistently within the same block can result in unexpected behavior.
- Placing statements outside of the function when they should be inside can result in unexpected behavior.
#### The Correct Order of Statements

- Python executes statements sequentially within a block
- The correct order of statements is vital for the algorithm (or solution) of the program, or it may also result in a logical error.

```python
# Initialize a variable 'full_name' with an empty string
full_name = ""

first_name = input("Enter your first name: ")

last_name = input("Enter your last name: ")

print("Hi there,", full_name)

# Concatenate the names with a space in between and store the result in 'my_name'
full_name = first_name + " " + last_name # The `+` symbol can be used to combine two strings.
```

> This code displays the output before updating the full name.

**Changing the order of statements within the function can lead to logical errors.**
#### The Order of Parameters and Arguments in Functions

- Parameters are defined in the function signature.
- Arguments are passed to the function when calling it, matching the order of parameters.

```Python
def print_question(x, op, y):
    print("What is the result of ", str(x), op, str(y), "?")

print_question(10, 2, "*")
```

> The order in which we pass arguments to a function must match the order in which the parameters are defined in the function's definition. Python uses positional arguments, meaning the value we pass for each argument is **assigned to the corresponding parameter in the order they are listed**.

In this function, `x`,`op`, and `y` are parameters, and they must be provided in that order when calling the function:

```python
print_question(10, "*", 2)
```

> Here, `10` corresponds to `x`, `"*"` corresponds to `op`, and `20` corresponds to `y`.

Changing the order does not work correctly, and we might get unexpected results or errors because the values assigned to the parameters in the order which they are listed in the function definition.

Let's look at one final example:

```Python
def calculate_sum(n1, n2, n3):
    total = n1 + n2 + n3
    return total

# Correct order of arguments
print(calculate_sum(3, 7, 2))

# Incorrect order of arguments (will result in an error)
print(calculate_sum(2, 5))  # This will raise a TypeError
```

> In the code above:

The function `calculate_sum` expects three parameters (`n1, n2 and n3`) as is obvious from lines 1 through 3. 

The function call in line 6 results in the correct output. However, providing only two values (line 9) or swapping their order results in a `TypeError` because the function expects three arguments. So, the order, as well as the number of arguments, is essential for the function to work correctly. 

- Swapping the order of arguments can lead to logical errors
- Providing more or fewer arguments than the function expects can result in `TypeError`.

# Comparison and Logical Operators

> We know how to use built-in functions as well as define our own functions. We also know how to take input from the suer and assign it to a variable for storage and reuse or pass is as further input to a function.

We also know how to output something on the screen for the user. 

But we can only write sequential programs, where the computer fetches and executes one line of code after another, from the first executable line to the last, in a strictly sequential order.

*This equips us with the necessary skills to solve a lot of interesting problems, but there are still some problems that sequential programs cannot solve.*

- Sometimes, a solution might require non-sequential execution as well:

> This chapter is about learning how to write programs that can, while they are executing, be selective about executing lines of code. 
> 
> 	Secondly, we will learn how to write programs that can execute some lines of code multiple times. Our project will require us to be able to code in this way.

Imagine Alex, an elementary school student, uses our app and manages to get three questions right. When Betty, another student, uses our app, she gets all five questions right. We are not going to write two different programs, one for Alex and one for Betty. 

- But, the same piece of code should compute that Alex's score is 3 and Betty's score is 5.

Of course, our program cannot know in advance what the final score of its user is going to be. It is going to be known to our program while the code is being executed by Alex and Betty, respectively. 

**Note:** How does the code know if the user has entered the correct answer to the question?

Till now, we have seen how to compute the correct expected answer, given a question. For instance, if the question was `4 * 7`:

```Python
user_answer = int(input("What is 4 * 7? "))
correct_answer = 4 * 7
```

> So we have two numbers in two appropriately named variables. How would we know if `user_name` is correct? Because if we know it is correct, we need to update the user's score by 1. Line 3 is inviting you; what can be done there right after `correct_answer` and `user_answer?`

We have a symbol for equality, which we have known since childhood, but we have been using that in Python for assigning some value to a variable. We have even used that in **lines 1-2**. But why not take a chance and use that for comparing two numbers as well to see if they are equal?

```python
user_answer = int(input("What is 4 * 7? "))
correct_answer = 4 * 7
user_answer = correct_answer
```

> That did not work as expected, or did it? We need to be able to test our hypothesis. 

How about, if we insert a print statement after line 3? This way, we might know what `user_answer = correct_answer` is doing. 

```python
user_answer = int(input("What is 4 * 7? "))
correct_answer = 4 * 7
print("User's answer: ", user_answer, "Correct answer: ", correct_answer)
user_answer = correct_answer
print("User's answer: ", user_answer, "Correct answer: ", correct_answer)
```

```
root@educative:/usercode# python3 main.py
What is 4 * 7? 28
User's answer:  28 Correct answer:  28
User's answer:  28 Correct answer:  28
root@educative:/usercode# ^C
```

> Enter `28` and it seems to work! But, run it again. This time, give a wrong answer, let's say `20`, and see what happens! **Line 4** clearly ends up assigning the value in `correct_answer` to `user_answer`. 

But we wanted to use `=` for checking if the two numbers are equal or not.
### Equality, not Assignment

> Since a single `=` is taken by Python for assignment purposes, what's the next best option for an equality operator? How about double equals? `==`. 

```python
user_answer = int(input("What is 4 * 7? "))
correct_answer = 4 * 7
print("User's answer: ", user_answer, "Correct answer: ", correct_answer)
user_answer == correct_answer
print("User's answer: ", user_answer, "Correct answer: ", correct_answer)
```

If we try `28`, we'll have the same output as before. If we try `20`, this time, the `user_answer` had not been updated! So, we do know that `==` did not assign the value `28` to `user_answer`, since the value of `user_answer` remained `20` even after **line 4** has been executed. However, we need to encapsulate the code in **line 4** within `print` in the hope of figuring out what `==` has been up to.
### A Final Word about `==`

> Conceptually, think of `==` as another built-in function that takes in two numbers and returns `True` or `False`.
#### Other Comparison Operators

| Operators | Description                                             | Example Usage               |
| --------- | ------------------------------------------------------- | --------------------------- |
| `==`      | The two numbers are exactly equal                       | 2 == 2 would return `True`  |
| `!=`      | The two numbers are not equal                           | 2 != 2 would return `False` |
| `>`       | The first number is greater than the second             | 2 > 2 would return `False`  |
| `>=`      | The first number is greater than or equal to the second | 2 >= 2 would return `True`  |
| `<`       | The first number is less than the second                | 2 < 2 would return `False`  |
| `<=`      | The first number is less than or equal to the second    | 2 <= 2 would return `True`  |
### How do we Update the User's Score?

> Now that we know how to compare `user_answer` to `correct_answer` for equality, we also know how to update the score by 1 (`score = score + 1`). However, our client's project requires our code to update the score only if the user has correctly answered the question, not otherwise. How do we do that? 
# Programs that Can Compare

- [Project requirements](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/6580539401306112#Project-requirements)
    - [What if](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/6580539401306112#What-if)
    - [Bringing if inside our project](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/6580539401306112#Bringing-if-inside-our-project)
        - [Indentation matters](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/6580539401306112#Indentation-matters)
    - [Let’s finish the requirements](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/6580539401306112#Lets-finish-the-requirements)
    - [Learn about if elif else](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/6580539401306112#Learn-about-if-elif-else)
- [Review of the lesson](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/4876665770606592/6580539401306112#Review-of-the-lesson)
### What If

> We know we'll only need `==` to check for the answer's correctness. What if we had something in Python that could let us update the score, but only `if` the `user_answer == correct_answer`:

```Python
score = 0
if user_answer == correct_answer:
    score = score + 1
else:
    print("Unfortunately your answer is not correct.")
```

Now, this code reads neatly. This is as easy as it looks == Python lets us use an `if=else` to control the flow of code execution.
### Bringing `if` Inside Our Project

> Let's code to fulfill the project requirements. Let's intro duce a variable `score`.

```python
score = 0
user_answer = int(input("What is 4*7? "))
correct_answer = 4 * 7
print("Your score is", score)
```

Why don't we now bring out `if` code structure that we designed earlier so that the score only gets updated when the `user_answer == correct_answer`:

```python
score = 0
print("Your score is", score)
user_answer = int(input("What is 4*7? "))
correct_answer = 4 * 7
if user_answer == correct_answer:
	score = score + 1
print("Your new score is: ", score)
```

> Run the code first for `28`, then run it for `20`. What's the difference? Of course, the score will now only get updated when the correct answer is input by the user.
### Indentation Matters

> Now, let's make a minor indentation change. Let's see what is going to change:

```python
score = 0
print("Your score is", score)
user_answer = int(input("What is 4*7? "))
correct_answer = 4 * 7
if user_answer == correct_answer:
	score = score + 1
	print ("Your new score is: ", score)
```

The difference from the previous code is that now the `print` statement in **line 7** only gets executed as part of the `if` block, not otherwise. 

Again, run it for `28` and `20`. This gives us the ability to do multiple actions in case an `if` block is to be executed. The same is the case for the `else` block.
### Let's Finish the Requirements

> Let's write code that does two things `if` the `user_answer` is correct, i.e. it updates the score and prints an affirmative message for the user. Or `else`, it does not update the score and only informs the user that their answer wasn't correct.

```Python
score = 0
print("Your score is", score)
user_answer = int(input("What is 4*7? "))
correct_answer = 4 * 7
if user_answer == correct_answer:
      score = score + 1
      print("Due to correcly answering, your score is: ", score)
else:
      print("Sadly, that is not a correct answer")
```

### Learn About `if elif else`

> We now know how a simple `if=else` structure works. However, there are situations where we might have to create a nested `if=else`, within another `if-else`. This complexity makes the code less readable eventually.

Here's a simple example to illustrate our point:

- We want to greet the user appropriately, given the time of the day. 
- Within the first 12 hours of the day, we say "good morning", otherwise, we have two possibilities: a "good afternoon" if it is less than 18:00 hours, otherwise a "good evening". 
- The code would look like this:

```Python
# Using if-else
hour = 15 # Try assigning hour different values, e.g. 11, 16, 20
if hour < 12:
    greeting = "Good morning"
else:
    if hour < 18:
        greeting = "Good afternoon"
    else:
        greeting = "Good evening"
print(greeting)
```

Python gives us a better option for what's happening in **lines 5 and 6**. It gives us a keyword `elif` (short for else and if). The use of `elif` makes the code so much more readable.

```Python
# Using elif
hour = 15
if hour < 12:
    greeting = "Good morning"
elif hour < 18:
    greeting = "Good afternoon"
else:
    greeting = "Good evening"
print(greeting)
```

> Notice how we use `else:` at the end. This `else` is only executed when all the previous conditions have failed (are `false`).

In short, `if-else-elif` provides a way to create a chain of conditions where each condition is checked in sequence and the corresponding block of code associated with the first true condition is executed. 

Whether it's simple `if` statements, `if=else` statements, or `if=elif-else` statements, we can use them based on what we want to check in our program.

# Programs that Can Loop

> We have found a way to break the strictly sequential flow of a program, by pushing one or however many statements within an `if` block. This means that our lines of code, other than those `if-else` blocks, will get executed line by line, in sequence. But some lines of code will only get executed if a condition is `True`, otherwise, another set of lines will become a part of the the execution.
> 
> 	Sequential or selective, each line of code only gets executed once, and then our computer fetches the next one, and then the next.

### The `while` Loop

Wouldn't it be great for the programmers if they could make the computer execute a block of code repeatedly *while* a condition is true?

```python
print(1)
print(1)
print(1)


# Output:
# 1
# 1
# 1
```

> Let's imagine we are being asked by our boss to print `1` ten times. Of course, we'd have to write ten lines of code. We'll drag our feet a little but we'll still be willing to write those ten lines of code. 

But now, our boss is ordering us to print it 1000 times! Would we protest, resign, or start writing long and tedious code where every line is doing the same thing over and over again?

Even if we are okay with calling the `print()` function again and again, we need to be able to keep a count of how many times we have repeated the task. Let's see a variable and name it appropriately to keep track of it. 

We initialize `counter` with `1`:

```python
counter = 1
```

We know there are comparison operators, such as `<` or less than equal to, `<=` that we can use to keep track of the counter. But this time, instead of checking to see *if* the condition is true or not, we need a mechanism to keep printing *while* the condition is true.

```python
counter = 1
while counter <= 10:
	print(1)
```

Thankfully, Python gives us this new `keyword` called `while`. This makes our code so neat. 

> The above code keeps printing until the Python program times out. 
> 
> 	We forgot to update the counter, in the absence of which the value of the counter remains `<= 10` forever. This was our mistake, not the computers.

```python
counter = 1
while counter <= 10:
	print(1)
counter = counter + 1
```

> This code encounters the same endless loop problem as before. What would the solution be?

```python
counter = 1
while counter <= 10:
	print(1)
	counter = counter + 1
```

Why does this code work now? Correctly *indenting* the counter into the while loop makes it a part of the loop, otherwise it is executed independently of it as a separate line of code, and therefore is never updated.

### Printing the Counter

Instead of `print(1)`, let's `print(counter)` to know how code A and code B keep track of the counter. 

Remember, our algorithmic idea was to initialize a counter to `1`, and right after printing the number, increase the counter by 1 so that the `while` loop only works 10 times.

```python
counter = 1
while counter <= 10:
	print(counter)
	counter = counter + 1
```

> Making the program print `counter` instead of the number one now reflects that since the counter is inside the while loop, it is being updated, then printed to the console by the program. The updated number is printed instead of simply printing 1 over and over.

### Life Without `while()`

```python
counter = 1
print(counter)
counter = counter + 1
print(counter)
counter = counter + 1
print(counter)
counter = counter + 1
print(counter)
counter = counter + 1
print(counter)
counter = counter + 1
print(counter)
counter = counter + 1
print(counter)
counter = counter + 1
print(counter)
counter = counter + 1
print(counter)
counter = counter + 1
print(counter)
counter = counter + 1
```

> This would be a representation of the "unrolled" code from the while loop above. 

Imagine writing the above code manually when the boss asked us to print 100 numbers. Well, now we don't have to resign because we know that whenever there is a repeating pattern in our code or whenever something needs to be done again and again, we can use a `while` loop.

