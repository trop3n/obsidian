---
up: "[[C]]"
tags:
  - "#education/computerprogramming/languages/C/learnC"
source: www.codecademy.com
---


# What is the C Programming Language?

> C is a general purpose, procedural programming language that was first developed by Dennis Ritchie in 1972. Ritchie created this new programming language based on existing programming languages: **ALGOL**, **BCP**, and **B**. 
> 	He took features that worked in those languages and combined them to create C.

Up to that point, *all operating systems were created in a programming language called **Assembly***, which is the lowest-level language you can write to interact with the hardware in a computer. 

**Low-level languages** are more complex and typically involve using many more symbols than the programming languages you're familiar with. 

- But, because of C's power and flexibility, version 4 of Linux became the first operating system written in a programming language other than Assembly.

C quickly became popular because, compared to other programming languages that existed at the time, it was a lot easier to read, understand and code. C gave programmers all the performance that comes with manipulating hardware at a low level, along with the ability to do so in a readable syntax.

Along with the C family of languages, several other languages have used C as a guide. *Java, PHP, JavaScript, Swift and even Golang* use some of the same syntax that C pioneered.

The other programming languages in this article have replaced C in many places, but it's still widely used by developers who'd rather not deal with the complexity and multiple subsets of the C++ programming language.

- *The team that develops the kernel of the Linux operating system still only uses C*, which allows control over the hardware. 

# What is the C++ Programming Language?

> C++ is a general=purpose programming language created by Bjarne Stroustrup in 1985 to extend the C language. 
> 	It has all of C's low-level memory manipulation features but added the object-oriented programming paradigm. 

While other members of the C family have replaced C in some applications, C++ is the most common replacement for C. In fact, it's a direct replacement in most cases.

C++ is used where performance is at a premium and low-level control over the system's resources is needed. It's commonly used to develop *operating systems, video games, database software, web browsers, and embedded systems.*

Probably the highest concentration of C++ developers work in game development, where the language's control over computer GPUs is unmatched, allow for the life-like 3D graphics we see in modern video games. 

- It's also popular for IoT devices where code interacts directly with custom hardware.

# What is the Objective-C Programming Language?

> Objective-C is the programming language that was developed in 1984 by Brad Cox and Tom Love. They saw the need to add the object-oriented paradigm to the C programming language but used the SmallTalk language as their guide.

This led to one of the major differences between this member of the C family and the others: most of the syntax in Objective-C is similar - except when creating or handling objects.

The rights to Objective-C were acquired by a company called NeXT, which used it in a custom programming platform called OpenStep. In 1996, Apple acquired NeXT and used OpenStep in its new operating system, Mac OSX.

Most of Apple’s current Cocoa API is based on OpenStep, and Apple’s Xcode is based on NeXT’s Objective-C development tool. Objective-C quickly became the programming language for Apple products, and for the most part, exclusive to Apple products.

By 2014, when Swift was released, Objective-C was mostly unchanged over the previous 40 years, and there had been a lot of advancements in programming language development. 

Swift is *interoperable with Objective-C (which means it can run alongside it in the same application), and it’s much faster and easier to write.* Apple eventually suggested that developers use Swift rather than Objective-C, which has been in a slow decline ever since.

# What is the C# Programming Language?

> C#, like all the other children of C, is an object-oriented, general-purpose language. Microsoft released C# in 2000, adopting features from Java along with C. 
> 	Instead of being compiled to run on a specific operating system, C# was compiled to run using the .NET common language runtime, much like Java was compiled to run on the JVM.

Initially, C# was a closed-source programming language designed to run on Windows. It was used to develop desktop applications for the Windows operating system and server-side applications for Windows servers. It’s also the most popular language used in [ASP.NET](https://www.codecademy.com/learn/learn-asp-net?utm_source=ccblog&utm_medium=ccblog&utm_campaign=ccblog&utm_content=cw_c_vs_cplusplus_vs_csharp_vs_objectivec_blog) development.

But in 2014, Microsoft released C# as free and open-source and offered builds for both Linux and Mac OSX. It’s since found use in [game development](https://www.codecademy.com/catalog/subject/game-development?utm_source=ccblog&utm_medium=ccblog&utm_campaign=ccblog&utm_content=cw_c_vs_cplusplus_vs_csharp_vs_objectivec_blog) and web service development, making C# a widely used language on all popular operating systems.

# Welcome to the Learn C Skill Path

In this path, we will learn key programming concepts, write our own C Programs, use pointers to work with memory, and more. The C programming language was first released in 1972, making it one of the oldest still used today. All modern operating systems are implemented with C code, which means the C language powers *almost every technological experience we have*.

## Learning Objectives

After this skill path, we will be able to:

- Write basic C programs using various data types and operators
- Control the flow of a program using conditional statements and loops in C
- Understand how C interacts with memory and work with arrays, strings, and pointers.
- Create, edit and use user-defined functions and structures together in C.

## Projects

Demonstrate knowledge in several projects that exist throughout the Skill Path.

- Dates and Switches
- String Copier
- Race Simulator

# The C Programming Language

> C is an older language compared to other languages in the use and yet it is still popular. The [TIOBE Index](https://www.tiobe.com/tiobe-index/), which measures the popularity of programming languages, has C at the top of the list for many years. 
> 	This is due to C's use in all areas of computing.

Most operating systems today including the Linux Kernel are implemented with C code. The main version of the Python programming language is named `CPython`because it is implemented using C. C has also been extended using the languages like `C++` and `C#`.

C is also common in embedded systems which are smaller computing units that control things like home appliances, lighting controllers, and other small physical devices.

The C programming language is everywhere. Learning it will help you become a better programmer ready for the next challenge in any field of computer science.

## Hello World

Let's look at our first C program.

```C
#include <stdio.h>

int main() {
  // output a line
  print("Hello World!"\n);
}
```

> When this code is run the following text is displayed in the terminal.

```
Hello World!
```

Let's go through the code line by line to see what is happening. You don't need to understand everything right away, this is just a first look.

- `#include <stdio.h>`: This line is needed to tun the line of code that starts with `printf`
- `int main() { }`: This is the *starting point of the code*. All the code inside the curly braces runs first.
- `// output a line`: This is a comment. It is not a line of code but a message we can add to code to tell ourselves or others what the code does. When the code is run this line is ignored. 
- `printf("Hello World!")`: This line of code prints, or outputs, the text "Hello World!" to the console. Printing text to the console is one way for a program to communicate with the user.

## Syntax and Errors

When writing in C, we need to follow a set of rules in order for the code to run properly. These rules are known as `syntax`. 

As we go through each lesson we will learn new syntax on the topics being covered.

Let's look at the Hello World code to examine common syntax that will exist in most (if not all) of your programs.

```C
#include <stdio.h>

int main() {  
// output a line  
printf("Hello World!\n");
}
```

### Case Sensitivity

Most of the words int eh code use all lowercase letters. This is known as *case-sensitivity*. Whether lowercase or uppercase, certain words in the code must follow the correct case in order for the code to run. The only lines of text that can change case are *the comment and text between quotes*.

### The Semicolon

All statements, like the `printf()` statement, need to end with a semicolon. This *identifies the end of the statement and is needed for the code to run correctly.*

### Double Quotes

The text in between the double quotes `"` is known as a ***string*** (think of a string of characters). All strings must be surrounded by double-quotes.

So what happens when we break the rules? The answer is `errors`. The below text is an error that is output when we leave off the semicolon from the `printf()` statement in our hello world code. 

```C
script.c: In function ‘main’:
script.c:6:1: error: expected ‘;’ before ‘}’ token 
} 
^
```

> The text above gives the following information:

- The component location, `In function ‘main’`
- The line and column number, `6:1`
- A description, `expected ‘;’ before ‘}’`

As we can see the message does its best to help us solve the errors in our code.

## Output

The main goal of our Hello World code example is to output the text `"Hello World!"` to the console. The line of code that outputs text is:

```C
prinf("Hello World!"\n);
```

Let's dive deeper into the 2 parts of this line:

- `printf()` is known as a ***function*** and performs the action of printing text to the console.
- `"Hello World!\n"` is a string. A string is text in between a pair of double quotes.

Placing the string in between the parenthesis of the `printf()` function prints the text (without the quotes) to the console. 

Functions and strings are topics covered in later lessons. Don't worry if you don't understand the concepts fully. The important thing to note is that this is how we create output in the console. 

What about the `\n` at the end of the string? Good question! This is called an escape sequence and is used to add a non-visual character within a string.

In this case,`\n` adds a new line to the end of the string. Look what happens when we place it in between Hello and World!:

```C
printf("Hello\nWorld!");
```

The code will output:

```C
Hello
World!
```

It's important to remember an ***escape sequence*** is a character and *must be within the double quotes*. 

Another escape sequence is `\t`. This is equivalent to the tab key and will insert spaces within a string:

```C
printf("Hello\tWorld!");
```

The code will output:

```shell
Hello     World!
```

`\n` and `\t` are just two of many different escape sequences that can be put inside a string.

## Comments

When we write code it is *important to document the code's behavior*. One way to do this is to add comments to our code. 

Starting a line with a double forward slash `//` will create a comment and the entire line will be ignored when we run the code. 

```C
// This is a single line comment
// This is 2 single line comments 
// together to explain a little more
```

The comments like the ones above can be added above a line or block of code to describe the code's behavior. Shorter comments can be added to the end of a line of code as well.

```C
printf("My dog is happy!"); // How my dog feels
```

In both examples, once you use `//` the rest of the line is now a comment.

If you want to create a comment with a beginning and end, you can use `/*` to begin the comment and `*/` to end the comment. This is known as a block comment.

```C
/* The following output will bean outburst from my dog in a moment of pure joy after seeing another dog across the street. */
printf("Woof!");
```

As you can see from the above example a block comment can wrap multiple lines without the use of anything but the beginning notation `/*` and the ending notation `*/`.

## Compiling

At this point, we have run our code within Codecademy's learning environment. While this is how most of the exercises will go it is important to learn about running your code using a ***compiler***.

The ***compiler*** is the program that *converts your code to an executable program that can be run by the computer.* This involves reading the code from a file and compiling it into code the computer processor can run. 

A widely used C Compiler is [gcc](https://gcc.gnu.org/), which stands for GNU Compiler Collection. Let's look at how we can compile **helloWorld.c** to the **helloWorld** executable.

```C
// helloWorld.c
#include <stdio.h>

int main() {  
// output a line  
printf("Hello World!\n");
}
```

> To compile this code, we need to run the following command in a terminal: 

```
gcc helloWorld.c -o helloWorld
```

The above command can be broken up into three pieces:

- `gcc` is how we run the compiler application
- `helloWorld.c` is the filename of our code to be compiled
- `-o helloWorld` is an optional but common addition to the command. It tells `gcc` to output the program executable under the name `helloWorld`. If this is left out, the executable file will be called **a.out**.

After running the command we have an executable, but how do we run our code? We can run the executable with the following command, again using the terminal:

```
./helloWorld
```

This command tells the computer to look in the current directory and run **helloWorld**

## Summary

Great work getting through these first exercises! Let’s review what was covered:

- C has been around for a while but is still very popular
- Code syntax is a set of rules that are followed when writing code so the program is able to compile
- Errors occur when the syntax is incorrect
- Error messages make a best effort to describe the error and where it occurred
- Use [`printf()`](https://www.codecademy.com/resources/docs/c/basic-output/printf) to output text to the console
- [Comments](https://www.codecademy.com/resources/docs/c/comments) are used to include text in code that the compiler will ignore
- Line comments start with `//` and block comments are surrounded by `/* */`
- The `gcc` application, or GNU Compiler Collection is a compiler used to compile C programs

# Bringing C to Your Local Computer

### Explore the Power of C with a Local Programming Environment

While it is nice and easy to write code on the Codecademy platform, you may eventually want to work with the C programming language on your local computer. The best way to do this is with an ***Integrated Development Environment***, commonly referred to as an ***IDE***.

IDEs are useful applications that assist programmers with many tasks such as:

- File system navigation
- Code lookup and autocomplete
- Syntax error highlighting
- Local command-line access.

There are many IDEs to choose from; it’s good to use one that is free and supports a wide variety of programming languages. **VSCode** is an open-source IDE created and maintained by Microsoft and is an excellent choice for C programming.

#### Install VSCode

To get started with VSCode, install it from the [VSCode home page](https://code.visualstudio.com/).

When the install is finished, you should be able to open up VSCode on your local computer.

#### Install C Extension and Compiler

After installation, you need to add C support and the proper compiler for your operating system. This is explained using the [VSCode C/C++ docs](https://code.visualstudio.com/docs/languages/cpp).

Once complete, you should be able to compile and run a C script within the VSCode command line.

#### Explore VSCode

With your system set up, you can now get started. There are many things you can accomplish with VSCode, so take the time to explore what it can do! A good first step is to look over the [VSCode Getting Started docs](https://code.visualstudio.com/docs).

# Variables

## What is a Variable in C?

In this lesson we will learn about: 

1. The rules for naming variables in C.
2. The main data types in C: `int`, `float`, `double` and `char`.\
3. Declaring and initializing data types in C, as well as changing their value.
4. Casting from one data type to another, and some potential limitations in C. 

Let's start with what a ***variable*** is. It is a reference used to store information for future use. For instance, `int score` can be called later in your code to assign, change, compare, etc. In this example, you can see the basic structure of variable creation (known as *declaration*) is `type_variable_name`. 

Have no fear, we will go over each part of this and more in this lesson. 

Specifically, we will cover how to create, name, assign, modify, and convert them to different types.

 A bonus tip right from the start, you can create more than one variable of the same type at a time by listing them with commas between their names, like `type` `variable1`, `variable_2`, `variable_3`, `variable4`. 
 
![Desktop computer](https://static-assets.codecademy.com/Courses/learn-c/variables/Desktop-image.svg)
## Naming Standards

We are going to start with the second part of our variable declaration, `type variable_name`, the `variable_name`. C does *not* allow you to throw anything down and call it a variable name, there are some restrictions. 

- Names can be composed of upper and lowercase letters, numbers and underscores.
- The first character *must be a letter* (upper or lowercase)
- No keywords are allowed as the full name (`int` is not allowed but `int_count` would work.)

That's it, nothing too crazy, just keep these rules in mind when creating variable names.

## Data Types

What about that first part of our template `type` (from `type variable_name`)? We saw some examples in the previous exercise when you corrected the bad variable names, but let's talk about what they are.

The type of a variable denotes what kind of information can be stored in it. C has a good numner of types you can use, but in this lesson, we will go over some of the most common ones: `int`, `float`, `double`, `char`. 

In C, you must specify the type of the variable when you declare it. Once it is set, that type of information is the only type that can go into that variable. So if you create a variable of type `int`, which can only store whole numbers, you will not be able to store `"a"` nor `1.2` in it. The table below shows these types we are going over and what information can go into each.

| Type     | Description                     | Values                          |
| -------- | ------------------------------- | ------------------------------- |
| `int`    | a whole number                  | -2,147,483,648 to 2,137,483,648 |
| `float`  | a number with possible decimals | 6 decimal places                |
| `double` | a number with possible decimals | 15 decimal places               |
| `char`   | stores one character            | a single character              |
There are a few questions we might be asking ourself looking at these descriptions. 

What's the difference between a `float` and a `double`? We are going to look at this in the next exercise. `char` holds a single letter or number, but what if you want to store something like a person's name, that is more than one character? That gets a bit more technical and we will learn about it in the lesson on *strings* later in the course. 

## `printf()`

We are going to take a little detour for a minute to help us understand what is going on in the code in the lessons. We might have noticed `printf()` at the bottom of some exercises. This allows for text to be output to the terminal. 

The basic format is `printf("string to display", [list of optional parameters])`.

So if we had something like `printf("Hello World!")` the terminal would display `Hello World`

The optional parameters let us add values dynamically to the string, such as values stored in the variables we have been learning about. For example, if we wanted to output `Hello World, today is the 3rd!` we could do that like this:

```C
int day = 3;
printf("Hello World, today is the %drd", day);
```

When the compiler runs the code it will replace `%d` with the value in the variable list, taking them in the order found in the string matching the order they are listed; first in the string is matched in the list of parameters. 

There are lots of optional formatting and parameter types that can be used, but for our purposes here are a few of the basic ones.

To indicate a variable type we want to replace:

| symbol     | type            |
| ---------- | --------------- |
| `%d or %i` | int             |
| `%f`       | double or float |
| `%c`       | char            |
You can also use some reserved symbols within the string to have invoked formatting, here are a few common ones.

| symbol | effect          |
| ------ | --------------- |
| `\n`   | newline         |
| `\r`   | carriage return |
| `\t`   | tab             |

## Initialization

Let's get back to understanding variables in C. Now that we have our variable, we know its name and what it can hold, what do we do with it? Right now it's empty and doesn't serve any real purpose. A variable's power comes from its ability to be set, changed and examined. So the question is, how do we do that?

There are two ways to set a value, for now let's look at how to set the value when we create the variable itself:

```C
int example = 3;
```

In this case, not only have we created a variable, named it `example`, and identified it to hold whole numbers, set its value to `3`. We've saved time by doing all of these parts all in one line.

When declaring a `char`, we need *single quotes* around it. 

```C
char foo = 'a';
char goo = '2';
```

## Float and Double, What's the Difference?

So why are there two different types for decimals in C? The short answer is different types for different situations.

A `float` has less precision that a `double`, 6 vs 15 possible decimal places respectively, and therefore takes up less memory (4 bytes vs 8 bytes). However, a `double` run faster, so you gain speed at the cost of more memory usage.

The other thing to be aware of is that the system is rounding the values you store in either. This can cause unexpected results, especially with a `float` as they have less precision. This is why you will see `double` being used any time accuracy is important, such as in scientific, medical or financial applications.

```C
#include <stdio.h>

int main() {
  
// Modify this variable value, start low and increase until something odd appears in the results
  int numOfLoops = 10;

  // Please do not modify anything below this point
  float a = 0.1f;
  float b = 0;
  double x = 0.1;
  double y = 0;

  printf("At the start, our target float b is:%f\n", b);
  printf("At the start, our target double y is:%f\n", y);

// If you were curious about what this code is doing, it is looping through and adding to our variables b and y a set amount of 0.1 on each loop
  for(int i = 0; i < numOfLoops; i++)
  {
    b += a;
    y += x;
  }

  printf("At the end, our target float b is:%f\n", b);
  printf("At the end, our target double y is:%f\n", y);

}
```

In this example much of the code is already in place, don’t worry at this point if you can’t follow everything that is going on yet, you will learn about loops in a later lesson. For now, you will want to experiment with `numOfLoops` and keep increasing its value until something unusual happens with the output, specifically the `float` value.

In general, the program takes a `double` and a `float` and adds 0.1 to each over and over again `numOfLoops` times. So if you set it to 10, that means it’s adding 0.1 ten times, or 0.1 x 10 so the output would be 1.0. `float` and `double` both give you this value, but keep making `numOfLoops` higher and a `float` will start to give unexpected results, showing their lower precision and rounding issues.

## Updating Values

Before, we said that there were two times when you can set a variable's value. We just examined how to set it at declaration, but if that's the only place it could be set, variables would have limited value (we will see in a moment an exception to this rule). It turns out that they can also be set at any future point in the code.

As an example:

```C
int total_units;
...
...
...
total_units = 3;
```

Notice that once we have declared the type we no longer reference the type, we just use the name of the variable. You can also set a variable to be the same as what is stored in another variable, such as `a = b`. If you change `b` after this, the values will no longer match (there is a way to tie the two variables together so they always match, but we will get to that later).

Have no fear, we will go over how to do more advanced things with setting the values in a variable shortly. 

```C
#include <stdio.h>

int main() {

  // These variables were created and had a starting value for you, no need to change

  char bookVersionReview = 'A';
  char movieVersionReview = 'B';
  double ticketPrice = 10.25;
  double bookPrice = 19.99;

  // Update the movie review score here

  // Update the ticket price here

  // No need to change below here

  printf("The book version has a review score of %c and costs $%.2f\n", bookVersionReview, bookPrice);

  printf("The movie version has a review score of %c and costs $%.2f\n", movieVersionReview, ticketPrice);
}
```

1. In the program on the right, someone has created the initial code by declaring and setting up information on a book turned movie. The output has also been taken care of. What you need to do is update the values based on changing information from the market. The initial movie reviews were generous, but have gone down since opening weekend, the average score for the movie is now a `C`, please update this score.

2. Due to dropping movie ticket sales, the movie theaters decide to match the price of the book to make up for their lost revenue. Set the price of the movie ticket equal to the price of the book.

```C
#include <stdio.h>

int main() {

  // These variables were created and had a starting value for you, no need to change
  char bookVersionReview = 'A';
  char movieVersionReview = 'B';
  double ticketPrice = 10.25;
  double bookPrice = 19.99;

  // Update the movie review score here
  movieVersionReview = 'C';
  // Update the ticket price here
  ticketPrice = bookPrice;
  
  // No need to change below here

  printf("The book version has a review score of %c and costs $%.2f\n", bookVersionReview, bookPrice);

  printf("The movie version has a review score of %c and costs $%.2f\n", movieVersionReview, ticketPrice);
}
```

## Constants

In most cases, variable values can be changed in the program, however, there are cases where you do not want to allow for our variables to change value. This is where *constants* come into play. These special types prevent any changes during execution once the value is set at the declaration.

Any basic data type in C, like those we have gone over, can be declared as a constant using the keyword `const` before the type. So instead of our template of `type variable_name`, it would be `const type variable_name`. 

It is also a best practice to use all upper case letters when declaring a constant:

```C
const int DAYSINWEKK = 7;
```

```C
#include <stdio.h>

int main() {

// Speed of light is 1.86e5 mi/s or 186000 mi/s we will store 1.86 and do the multiplicaiton later.
  double SPEEDOFLIGHT;
  int timeTraveledInSeconds = 30;

  SPEEDOFLIGHT = 1.86;

  // No need to change below here

  printf("Light would travel %.2f miles in %d seconds\n", SPEEDOFLIGHT * 100000 * timeTraveledInSeconds, timeTraveledInSeconds);
}
```

1. The speed of light is a constant, so a great candidate for an example of the `const` variable type. For the first step, identify the `SPEEDOFLIGHT` as a constant.

   Notice that the name is already fully capitalized to match constant best practices.

2. The program now violates the rules of constants. We know the speed of light won’t change, so how can you fix the code to run correctly by obeying the rules of constants?

```C
#include <stdio.h>

int main() {

// Speed of light is 1.86e5 mi/s or 186000 mi/s we will store 1.86 and do the multiplicaiton later.

  const double SPEEDOFLIGHT = 1.86;

  int timeTraveledInSeconds = 30;

  // No need to change below here
  printf("Light would travel %.2f miles in %d seconds\n", SPEEDOFLIGHT * 100000 * timeTraveledInSeconds, timeTraveledInSeconds);

}
```

## Casting Types

Sometimes it's useful, or even necessary, to change the value type of a variable and use it for other purposes. For instance, if you had a `double` with a percent score on a test, say 0.95, you would most likely want to display 95% to the user instead. Notice, we are not changing the type of the variable, nor the value stored in the source variable. What we are doing is displaying the changed variable as a new type or storing it in a different variable that might be a different type. 

So you could do this:

```C
int a;
double b = 3.0;
a = b;
```

There are two types of conversions, *implicit and explicit*. When you set one variable to be the same as another, such as `a = b` above, but their types do not match, the compiler will try to convert them. However, this can be dangerous as you might not know what values will be in the variable at runtime, and it might not be implicitly convertible to another type. Our example above was implicit, the compiler in this case will make a best guess.

The other way to convert a variable from another type is explicitly. You can do this by simply telling the compiler what type you want to set it to. So in our example above we would change the line `a = b` to `a = (int)b`. That way if `b` was something other than 3.0, such as 3.2, we are telling the compiler to make it work, so it would set it to 3.

```C
#include <stdio.h>

int main() {
  double testScore = 95.7;
  int displayScore = 0;

  // No need to change below here
  printf("Great work, you got a %d%% on your test\n", displayScore);

}
```

1. Let’s take our example above where we want to take the percent score as a `double` and convert it to an `int` for display. Set the `displayScore` to be `testScore`.

2. Now try doing the conversion explicitly by adding on the `(int)` to your setting of `displayScore = testScore;`

```C
#include <stdio.h>

int main() {

  double testScore = 95.7;
  int displayScore = (int)testScore;

  // No need to change below here
  printf("Great work, you got a %d%% on your test\n", displayScore);
  
}
```

## Casting Types Continued

A more interesting casting option is converting a `char` to a number type, or the other way around. Just like before, you have to be careful how you set this up. In the backend, a `char` doesn't store `'a'`, it stores the value representing that: 97 for lowercase and 65 for uppercase.

```C
int targetInt;
char sourceChar = 'a';
targetInt = (int)sourceChar;
```

> Now `targetInt` equals 97.

When you can an `int` to a `char`, you get the opposite process and the `char` is set to the value at the `int` value. So if you did:

```C
int sourceInt = 65;
char targetChar;
targetChar = (char)sourceInt;
```

> `targetChar` now equals `'A'`.

```C
#include <stdio.h>

int main() {
  char targetChar;
  int sourceInt = 99;
  double sourceDouble = 55.67;

  // Cast here

  // No need to change below here

  printf("source int %d, source double, %.2f, target %c\n", sourceInt, sourceDouble, targetChar);

}
```

1. If `'a'` is 97, what do you suppose we would get if we set an `int` to 99 and cast it to a `char`? Let’s find out. The initial state is set so you need to cast our `sourceInt` to `targetChar`.

   Set `targetChar` equal to `sourceInt` and explicitly cast it by using `(char)`.

2. Now let’s see what happens when you cast a `double` into a `char`. Set `targetChar` to `sourceDouble` using implicit casting (no type identifier for the cast).

```C
#include <stdio.h>

int main() {
  char targetChar;
  int sourceInt = 99;
  double sourceDouble = 55.67;

  // Cast here

  targetChar = (char)sourceInt;
  targetChar = sourceDouble;

  // No need to change below here

  printf("source int %d, source double, %.2f, target %c\n", sourceInt, sourceDouble, targetChar);

}
```

## Review

In this Lesson on variables in C we learned:

1. The rules for naming variables in C.
2. The main data types in C: int, float, double, and char.
3. Declaration and initialization of data types in C, as well as how to change their value.
4. How to cast from one data type to another and some potential limitations in C.

We went over a general introduction to variables, but there is much more to learn. You should now have the building blocks we will add on to. In the next lesson, we will go over more options you have with variables, such as arithmetic, comparisons, and logical operators that will allow you to expand on the power of variables in C. Thank you for joining us and we can’t wait to dive into the next lesson with you.

# Operators

In this lesson we will learn about:

1. performing basic mathematical operations on variables and values using common symbols
2. assigning values to variables and/or performing basic mathematical operations using shorthand operations.
3. comparing two values and/or variables against each other to return a true/false.
4. using logical operators (and, or and not).

In the previous lesson, you learned how to create and set variables, but not what you can do with them beyond that. In this lesson, you will learn about modifying variables with the power of math, some shorthand assignment methods, and how to compare variables and values. Finally, we will go over how to use logical operators for “and,” “or,” and “not.”

## Mathematical Operators

At their core, computers are basically fancy calculators. So it's a good thing to learn how to perform basic mathematical operations early on in your language development. 

Addition and subtraction work just as you would expect them to. `a = 2 + 3` will store `5` in the variable `a`.  You can also use these variables as part of the math (or all of it).

```C
int a = 2;
int b = 3;
int c = a + b;
```

These same foundational principles of mathematics hold true for subtraction, multiplication, and division.

## Modulo

You may have run across Modulo, symbolized as the percent symbol %, before. If not, or as a reminder, modulo performs division but instead of giving you the number of times the denominator goes into the numerator, it gives you the remainder after the division. As an example, if you took `10 / 3` you would get 3 with 1 left over. If you wanted to just get the remainder and didn't care about the other part you would do `10 % 3`. This would give you `1`.

A common use of modulo is determining if an integer is even or odd. If we have an integer, `x`, and aren't sure if it's even or odd, we can use modulo to see the remainder. If the result is 1, `x` is odd, otherwise it is even.

```C
#include <stdio.h>

int main() {

  int endingDayOfWeek = 0;
  int daysThatPass = 5;
  int daysInWeek = 7;

  endingDayOfWeek = daysThatPass % daysInWeek;

  printf("You started on the 1st (0) day of the week, went %d days from this, so it is now the %d day of the week\n", daysThatPass, endingDayOfWeek);

}
```

Output:

```
You started on the 1st (0) day of the week, went 5 days from this, so it is now the 5 day of the week
```

## Increment and Decrement


C has several shorthand tricks we can use to make our life easier. For instance, it is very common inside a loop to have a counter you want to increment (add 1) or decrement (subtract 1) on each pass. C lets you do this by using a double symbol such as:

```C
int a = 1;
a++;
```

> This would now set the value in `a` to be 2. The shorthand for decrementing is `--` instead of `++`. So if we wanted to decrement `a`, it would be:

```C
a--;
```

```C
#include <stdio.h>

int main() {

  int n = 13;
  int m = 10;

  m--;
  n++;

  printf("m = %d\n", m);
  printf("n = %d\n", n);
}
```
```
m  = 9
n = 14
```

## Assignment

It's one thing to do all these operations, but if the results are thrown away as soon as the statement finishes executing, the entire process *has limited usability*. What we need is a way to assign values to variables. We have already seen the basic way to do this using `=`, but C offers some additional shorthand tricks for assignment. 

Each of the basic math symbols you have learned in this lesson can be done in C with a shortcut. Let's look at an example of two ways to write simple additions that would give us the same result.

```C
int a = 2;
int b = 3;
a = a + b;
```

> This could also be written as:

```c
int a = 2;
int b = 3;
a += b;
```

Notice that C lets us shorthand adding something to a variable's starting value by using `+=`. You can do this same shorthand with `-=`, `*=`, `/=` and `%=` for subtraction, multiplication, division, and modulo, respectively.

## Comparisons

You haven't learned about statements that check on and respond to true/false (known as boolean) values yet, but since we are talking about arithmetic symbols we wanted to give a primer with the symbols used for these checks.

You can check if two values are equal `==` (the double `=` checks for equivalency rather than assignment), not equal `!=`, greater than `>`, greater than or less than `>=`, less than `<` and less than or equal to `<=`.

As an example, if you wanted to perform a segment of code if `a` had the same value as `b`, you could write it as:

```C
int a = 3;
int b = 3;
if (a == b) {
  a++;
}
```

> Notice in the code that at the end, `a` would be `4`. 

## Logical Operators

You do not just have to check one part at a time when you are doing your comparisons. C lets you see if two or more parts are true, if at least one is true, or if something is not true. We have already seen a quick example with `!=`, checking to see if the left side is not equal to the right side, but `!` in front of any boolean will see if the statement is not true. You will learn more about this when you learn about boolean statements in general. 

If you care checking to see if two or more parts are true you can use `&&` between them. If you want to see if any of the parts is true you can use `||`. To see both in action here is a trivial example:

```C
int a = 2;
int b = 3;
if (a == b && a == 2) {
	printf("both are true\n");
}
if (a == b || a == 2) {
    printf("one or both are true\n")
}
if(!(a == b)) {
	printf("they are not equal\n");
}
```

> In this example, only the second and third statements would evaluate to true. The second statement will be true because `a` does not equal `b` but *does* equal `2` - remember, only one of the parts needs to evaluate to true when using `||`. The last statement will be true because the inner equality check will evaluate to false and we then take the opposite of that with `!`.

## Order of Operations

C does not just process the statements you send it blindly from left to right. It looks at the statements and applies standard rules to the order in which the statements should be processed. 

- For instance, it will do multiplication before addition.

There are many more symbols and operations you will learn as we progress with our knowledge of C, but here is a list of the order for the operations we have gone over in this lesson.

Looking at the table below, the operations with priority 1 will be performed first. Then priority 2, 3 and so on will be processed. For operators of the same level of priority, the operations occur from left to right.

|Priority|Symbol|
|---|---|
|1|++|
|1|--|
|1|()|
|2|!|
|2|(typecast)|
|3|*|
|3|/|
|3|%|
|4|+|
|4|-|
|5|<, <=|
|5|>, >=|
|6|==, !=|
|7|&&|
|8|\||
|9|all assignment operators|
## Review

Congratulations on finishing this lesson on operators in C!

In this lesson you learned about:

- Basic mathematical operations in C: addition, subtraction, division, multiplication, incrementing, decrementing, and modulo.
- Assigning values to variables: `=`, `+=`, `-=`, `*=`, `/=`, `%=`
- Performing basic comparisons between values and variables: `==`, `!=`, `<`, `<=`, `>`, `>=`
- Using logical operators in C: `&&`, `||`, `!`.

You now have the basic tools on which to build a strong understanding of coding in C.

We have gone over a lot of very important foundational ideas, we encourage you to spend some time playing around with them in the console on the right.

# Grocery Store Part 2: Project

We will start you with our solution to the previous project for our apple information