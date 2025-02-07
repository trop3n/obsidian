---
up: "[[C]]"
tags:
  - "#education/computerprogramming/languages/C/learnCfromscratch"
source: educative.io
---

# Why Program in C?
## What is C?

C is a high-level programming language that was developed by Dennis Ritchie at Bell Labs in the early 1970's. It provides *fine-grain* control over hardware interaction, allowing for *highly-optimized code*.

- Because of this reason, it has always been a popular option for systems programming.

It's been the language of choice for *writing operating systems*. Unix was one of the first operating systems to be rewritten in C (initially, it was written in [Assembly language](https://www.educative.io/answers/what-is-assembly-language)). The core codes of **Microsoft Windows**, **Mac OS X**, and **GNU/Linux** are also written in C, although these operating systems may also use other languages for various components.

C has found other uses as well. It's useful for high performance computing. Compilers and interpreters for several high-level languages like **Perl, PHP, Python, R, Matlab, Mathematica, etc.** are also written in C.


> [!NOTE] TIOBE Index
> Contents As of April 2024, C is #2 in popularity according to the [TIOBE index](https://www.tiobe.com/tiobe-index/).

## A Program in C

```C
#include <stdio.h>

int main(void) {
  printf("Hello world");
  return 0;
}
```

> An example of a program in C.

The above is a bare-bones C program that simply writes the text "hello world" to the screen. As we can see, it's not scary looking code. The code that "does the work" here is **line 4**. All the other stuff you can think of as standard "boilerplate" C code you need for any C program.

We'll examine the details in this code later on. For now, we should just know three things about this code. First, **Line 3-6** define what's called the ***main function***. The `main` function is essential for C programs to run. he pair of opening `{}` curly brackets here include all the statements that will be executed when the program is run. Second, the stuff inside the round brackets in **Line 3** (`void`) is optional. We could leave it out, and the program would still run. 

Same for the statement `return 0;` on **Line 5**. We include these because it's a recommended practice. 

Third, **Line 1** imports one of the standard C libraries, `stdio.h` (*standard input/output*).

## A Comparative Perspective

```Python
print("Hello World")
```

```R
cat("Hello World")
```

```Matlab
disp('Hello World')
```

> The code blocks show the same program in Python, R and Matlab/Octave, respectively.

As you can see, what differentiates the given C code from similar codes in other languages is that in C we have to import the `stdio.h` library and define the `main` function explicitly in C. Not such a big deal. The other difference is that the name of the standard function to write stuff to the screen is different in each language. In C it is `printf`, in Python it is `print`, in R it is `cat`, and in Matlab/Octave it is `disp`. Again, no big deal.

One of the things we should take away from this boot cmap is that with a few exceptions, all (procedural) programming languages share many fundamental concepts, such as the use of procedures (functions) to perform tasks, but there are notable difference  that can impact how we write and understand code in each language, such as:

- Names of standard functions are different across languages
- Rules of each language (syntax) are different
- Functionality included in standard libraries can vary significantly
- Language specific features that are present in one language may not be present in others.

However, the foundational skills that we develop in C--such as the way to organize code and the logical thinking--are transferrable and will help us learn other languages more quickly.

## Virtues and Challenges

> Every language has some strong points, but no language is perfect. Let's see why this is true for C.

### Virtues of C Language

- ***Fast***: C is fast. It is a compiled language, close to the machine hardware and doesn't require any intermediary to interpret each line of code. 
- ***Portable***: Because of it's popularity, there exists a compiler for just about any hardware platform available. This makes it possible to port the code to any platform.
- ***Small Memory Footprint***: Its compiled nature, minimal runtime environment, and lack of extensive object-oriented features generally give it a smaller memory footprint compared to languages like C++ and Python.
- ***Low-Level Access***: C programmers have direct access to memory and can also access low-level system features as needed. This gives a lot of flexibility and fine-grained control to the programmer.
- ***Strong EcoSystem***: It is one of the older languages. Because of this, it has matured over time. It has a vibrant community, with a strong ecosystem and lots of resources and a combined experience available. 
- ***Availability of Tools***: Over time, several tools have been developed to make programming easier. These include various dev environments, and compilation, debugging and optimization tools.

### Challenges Associated with C

- ***Memory Management***: Memory has to be managed explicitly and a C programmer needs to be mindful of how memory is being used behind the scenes.
- ***Minimal Runtime Checking***: As C allows access to memory and does not enforce runtime checking, it's easy to get into trouble when programming with C.
- ***Mastering the APIs***: The language itself is small but there are many APIs and libraries that must be mastered to become an effective C programmer.
- ***The compile-test-debug cycle***: There is a compile-test (crash)-debug cycle for each piece of code. Even though the compiled code runs fast, there is a flip side to it as well, since each minor modification requires a time consuming recompilation—unlike interpreted languages like Python.
- ***Object-Oriented Programming***: It doesn't support OOP.
- ***Verbose Code***: The code is usually much more verbose than high-level languages like Python.

## When Should I Use C?

> As we learned in the previous lesson, C has an edge over many of the other programming languages in that it's fast, has a fine-grained access to the system, and has a small memory footprint. This makes C a language of choice for scientific programming, system programming, and Internet of Things (IoT) devices.

### C For Scientific Programming

We should think of C as one of many tools in our toolkit for performing computational tasks in scientific work: 

Taking advantage of C when the situation calls for it.

Using other languages when ease of use and maintainability is the goal, or when the ecosystem developed around those languages provides features essential for our task. 

In a lab I am affiliated with, we use Python, R, (sometimes Matlab), but when we feel the need—the need for speed—we use C.

### Processing Large Data

C may not be the best choice for interactive data exploration, like when we want to load in some data, plot it in different ways, do some rudimentary calculations, etc.

For this sort of interactive exploratory scripting, a language like Python, Matlab, R may be entirely sufficient. In particular, these other languages make it very easy to generate great looking graphics quickly. 

However, for cases where we need to process a large amount of data, you'll find it that these languages are slow. Even for fairly common statistical procedures, like **bootstrapping** (techniques that involve resampling data thousands or tens of thousands of times), interpreted languages will be orders of magnitude lower than C.

In such situations, C starts looking very attractive. If you have a data processing operation or a simulation, and you know it will take a long time to run, then it is often worth it to spend some time implementing it in C. The graph below compares the speed of interpreters for several languages. As you can see, C shines in this regard.

### Why Care?

> A rule of thumb is that if you have to wait more than 10 seconds for the result of a calculation or operation, then you should starting thinking about implementing it in C.

You might think, who cares if a calculation takes 10 seconds, or 30 seconds, not 5 minutes, for that matter? Are 5 minutes so bad? The answer is, no, it’s not so bad if you only have to do it once … but it’s almost _never_ the case that you perform a computation on your data only once.

Imagine writing some code to read in data from one subject, process that data, and write the result to a file, and that operation takes **60 seconds**. Is that so bad? Not if you only have to run it once.

- Now let’s imagine you have 15 subjects in your group. Your 60 seconds turn into **15 minutes**
- Now let’s say you have four groups with 15 subjects in each group. In that case, 15 minutes turn into **one hour**.
- You run your program, have lunch, and come back an hour later, and you find there was an error. You fix the error and rerun… another hour. Even if you get it right, imagine your supervisor asks you to rerun the analysis five different ways, varying some parameter of the analysis (maybe filtering the data at a different frequency, for example). Now you need **5 hours** to see the result.

It doesn’t take a massive amount of data to run into this sort of a situation. If you program your data processing pipeline in C, and you achieve a 100x speedup (not unusual), now those 5 hours turn into **180 seconds** (you could run your analysis twice, and it would still take less time).

### C for system programming and IoT devices

System and device programming is another area where C is usually the language of choice. Such programming often requires direct access to memory and hardware resources, which is a strong suit of the C language. In addition C is fast, making it well-suited for developing *high-performance system software* (such as operating systems and device drivers) that might need to process gigabits of data per second in addition to executing several other core tasks.

C's small memory footprint, together with it's ability to allow for fine-grained control over system resources, such as memory, also make it an ideal choice for programming IoT devices. These devices are usually small, and have limited resources, making C ideal in this scenario.

### The Bottom Line

> In the end, C is a much more efficient language than many of it's peers. However, it doesn't work well when prototyping is involved.

### A Balancing Act

An approach is to use interpreted languages like Python, R, Octave/Matlab, etc. for **prototyping** -- that is, for exploring small amounts of data, for developing an approach, and algorithms, for analyzing data, and for generating graphics.

For computationally heavy tasks, simulations, or a series of operations that are time-consuming, I think about implementing them in C.

Using interpreted languages for prototyping and C for performance is a sweet spot that helps balance the development speed with the performance.

On the practical side, the nature of C makes it optimal for many processing-based applications:
# Basic Statements and Types

## First Steps

For our first step into the vast world of C, we'll start by writing a simple program to display something to the console. We'll then see some related things that'll be helpful in the long run.

### A First C Program

The `prinf()` function is part of a C library (the standard (I/O) library) which contains many other useful functions as well. It is a standard practice to include the library into your code. This can be done by typing `#include <stdio.h>` at the top of our code. This `#include` line is called an ***include directive***, as it's an instruction to include the library in our code.


> [!NOTE] Note
> In general, C standard libraries can be made available by including appropriate files with a `.h` extension (such as `stdio.h`) in our programs. These are called ***header files***.

Now, onto the main part of the lesson. Let's print "Hello World" in our console:

```C
#include <stdio.h>

int main(void) {
    printf("Hello world");
    return 0;
}

# Output:
# Hello world
```

Don't worry about `int main(void)`, the enclosing curly brackets `{}`, and the statement `return 0;`, It's simply the context in which our code runs. `"Hello world"` is a piece of text which we call a `string`. More on those later.

Congratulations, we've written our first C code.

### A Note on the `printf()` Function

The `printf()` function can actually be used in much fancier ways such as:

```C
#include <stdio.h>

int main(void) {
	print("Hello %s, "world");
	return 0;
}
```

Here, we'll see there are two separate strings `Hello %s` and `"world"` but once again the same message `Hello world` is printed to the screen. That's because the syntax `%s` serves as a *placeholder*, and it replaced by the text `world` before the string is printed.

There are other kinds of placeholders (`%d, %c`) etc. used with the `printf` function that we'll see in later lessons but we won't always stop to talk about them. All this will become clear with time.

### Code Comments

***Code Comments*** are remarks that are left in our code for a human reader, and they are not executed when the program is run. In C, we can use the `//` for a single-line comment, or the pair `/*` and `/*` for opening and closing a comment that spans multiple lines:

```C
#include <stdio.h>

int main(void) {
    // Here is a print statement
    printf("Hello world\n");
    /* Here is a print statement
    that uses %s */
    printf("Hello %s", "world");
    return 0;
}
```

> Finally, a note that we sneaked in a `\n` at the end of the string on line 5, the so called ***newline character***. That's what causes the next output to be printed to a new line. Try removing it to see how the output changes. 

### Variables

Just as in other high-level programming languages, in C, we can assign symbolling names, known as ***variables***, for storing information in memory. Then we can retrieve those pieces of information in memory by using those symbolic variable names, instead of having to use the raw addresses of memory locations where our data is stored. Variables can be used to store different types of data including floating point numbers, characters, and even addresses of other memory locations.

### Variable Names

There are some restrictions on the names of variables in C. Names are made up of letters and digits, but the first character must be a letter (and not a digit). Here, we count the underscore `_` as a letter. Also note that uppercase and lowercase letters are *distinct* and so `Age` is *distinct* from `age`.

Here is a list of ***reserved keywords*** that cannot be used as variable names in C:

- `int`
- `double`
- `char`
- `float`
- `long`
- `short`
- `void`
- `unsigned`
- `signed`
- `auto`
- `static`
- `extern`
- `register`
- `const`
- `sizeof`
- `typedef`
- `enum`
- `union`
- `struct`
- `if`
- `else`
- `switch`

- `case`
- `default`
- `break`
- `continue`
- `return`
- `for`
- `while`
- `do`
- `goto`
- `volatile`
- `restrict`
- `inline`
- `_Bool`
- `_Complex`
- `_Imaginary`
- `_Atomic`
- `_Generic`
- `_Static_assert`
- `_Thread_local`
- `_Alignas`
- `_Alignof`
- `_Noreturn`

> A variable itself is just a name. Now, we'll learn about the different types of variables.

## Data Types and Sizes

To define a variable, we must specify it's ***data type***. The data type of a variable indicates what kind of data can be assigned to it. It also impacts how much memory will be allocated for storing the data in that variable. 

### Basic Data Types in C

There are eight basic data types in C. We describe these and the number of bytes required to store a value of each type in the table below.

However, do note that the C standard does *not specify the exact number of bytes to be used for a data type* -- it specifies a range of values instead.

Because of this and the differences in the underlying machine architecture, a few data types take up different amounts of space on different platforms. 

| Type            | Description                                                                                                                | Size in Bytes |
| --------------- | -------------------------------------------------------------------------------------------------------------------------- | ------------- |
| `char`          | A single character that can be *alphanumeric* in nature or another special symbol.                                         | 1 byte        |
| `int`           | An integer whose size is based on the underlying system architecture.                                                      | 2 or 4 bytes  |
| `short int`     | An integer of a smaller size (may be the same size and an `int`)                                                           | 2 bytes       |
| `long int`      | An integer of greater size (may be the same size as an `int`)                                                              | 4 or 8 bytes  |
| `long long int` | An integer of greater size than an `int`.                                                                                  | 8 bytes       |
| `float`         | A fractional number on at most 7 decimal digits. (Commonly called a **single precision floating point number**)            | 4 bytes       |
| `double`        | A fractional number on at most 15-16 decimal digits. (Commonly called a **double-precision floating-point number**)        | 8 bytes       |
| `long double`   | A floating-point number that's longer than a `double` (There are multiple implementations of this on different platforms). | Upto 16 bytes |
When using the integer types we can shorten them as follows:

- `short int` can be shortened to `short`
- `long int` can be shortened to `long`
- `long long int` can be shortened to `long long`

### Signed and Unsigned Qualifiers

There are also qualifiers `signed` and `unsigned` that can be applied to the integer types. These qualifiers can also be applied to the `char` type for historic reasons.

We have talked above about variable types and how many bytes they take up in memory. An important quantity to know about is that one byte is made up of *8 bits*. One **bit** can take on two possible values: 0 or 1. 

An ***unsigned*** 8-bit variable can take on values between 0 and (2^8)-1 = 255. 
A ***signed*** 8-bit variable can take on values between -128 and 127.

So when a variable is signed, it can take on negative value, and half of its total range is spread below zero, and the other half above zero.

A **signed** `int` on 4 bytes can take on values between -2,147,483,648 and +2,147,483,647. If we want to be able to represent integers larger than +2,147,483,647, then we can either use more bits (e.g. by using a `long` or `long long`) or by forcing all 32 bits of our `int` to be used on the positive side of zero. An `unsigned int` (4 bytes or 32 bits) can take on values between 0 and 4,294,967,295.

### How Many Bytes on Our Machine?

```C
#include <stdio.h>

int main(void) {
    printf("A char is %ld bytes\n", sizeof(char));
    printf("An int is %ld bytes\n", sizeof(int));
    printf("A float is %ld bytes\n", sizeof(float));
    printf("A double is %ld bytes\n", sizeof(double));
    printf("A short int is %ld bytes\n", sizeof(short int));
    printf("A long int is %ld bytes\n", sizeof(long int));
    printf("A long long int is %ld bytes\n", sizeof(long long int));
    printf("A long double is %ld bytes\n", sizeof(long double));
    return 0;
}
```

```
A char is 1 bytes 
An int is 4 bytes 
A float is 4 bytes 
A double is 8 bytes 
A short int is 2 bytes 
A long int is 8 bytes 
A long long int is 8 bytes 
A long double is 16 bytes
```

## Declarations

> Learn the C syntax required for declaring variables of different types.

### Declaring a Variable in C

Unlike programming languages like Python, R, Octave/Matlib etc., which are dynamically-typed languages, the C programming language is a ***statically-typed language***. From a practical point of view, this means that in C we have to declare, up front, the type of every variable we use.

In languages like Python we can do crazy stuff like this:

```Python
a = -1
b = 123.456
c = 'C'
d = [a, b, c]
print(a, b, c, d)
```

```
Output
0.86s
-1 123.456 C [-1, 123.456, 'C']
```

> The Python interpreter will figure out what types to assign to `a, b, c and d` based on evaluating the right-hand side of each declaration.

In C, we have to explicitly declare the type of each variable like this:

```C
#include <stdio.h>

int main(void) {
	int a = -1
	unsigned int b = 123;
	float c = 100.0
	double d = 123.456
	char e = 'C'

	printf("a" = %d, b = %u, c = %.3f, d = %.3f, e = %c\n",
				a, b, c, d, e);
	return 0;
}
```

```
Output
1.08s
a = -1, b = 123, c = 100.000, d = 123.456, e = C
```

We talk about the constants on the right-hand side of the assignment operator (`=`) in the next lesson. For now, note how we can use multiple format specifiers in the first string such as `%d` (for integers), `%d` (for unsigned integer), `%.3f` (for floating point numbers with 3 digits after the decimal point, and `%c` (for characters)).

We can also declare a variable first and defer assigning a value to it till a later point in time:

```C
#include <stdio.h>

int main(void) {
	long a;
	a = 123;

	printf("a = %ld\n", a);
	return 0;
}
```

### The Thing That Varies

As the name "variable" suggests, the data in a variable can change or *vary*. However, there's a certain type of variable whose value always stays the same. 

The `const` keyword is used to specify that a variable's value cannot be changed. It tells the compiler to prevent the developer from (inadvertently) changing the value of that variable.

```C
#include <stdio.h>
int main(void) {
	const int x = 33;
	// try changing the value of x by uncommenting the next line
	// x = 4;
	printf("Variable x is unchangeable: %d", x);
	return 0;
}
```

### Constants

> Learn about different types of constants in C:

**Constants** are values that do not change after they have been modified. These values can be of different types.

### Numeric Constants

An example of an `int` constant is the number `1234`. 

An example of a floating-point constant (by default typed as a `double`) is `123.4`. 

Another example of a floating point constant is `2e-3` (which represents 2 x10^-3 in scientific notation).

We can also write numbers in octal or hexadecimal representations of decimal: octal by using a leading zero (`0`) and hexadecimal by using a leading zero followed by an x `(0x)`. Decimal `31` can be written as `037` in octal and `0x1f` or `0X1F` in hexadecimal. Here are some examples of how numeric constants are created and then assigned to variables:

```C
int year = 1984; // integer constant 1984
int year = octalYear = 03700; // 1984 in octal
int year = hexYear = 0x7c0; // 1984 in hexadecimal
```

Here is some code to show how to print integers in various representations. Execute the following code.

```C
#include <stdio.h>

int main(void) {
  printf("1984 in decimal is %d\n", 1984);
  printf("1984 in octal is 0%o\n", 1984);
  printf("1984 in hexadecimal is 0x%x\n", 1984);
  printf("0123 is octal for %d\n", 0123);
  printf("0x12f is hexadecimal for %d\n", 0x12f);
  return 0;
}
```
```
# Output
1984 in decimal is 1984 
1984 in octal is 03700 
1984 in hexadecimal is 0x7c0 
0123 is octal for 83 
0x12f is hexadecimal for 303
```

### Character Constants

A character constant is written between single quotes, for example `'x'`. Characters in C are actually represented using integer values, from the ***ASCII Character Set***. ASCII codes range from 0 to 255. The upper-case alphabet starts at 65 `A` and ends at 90 `z`; the lowercase alphabet starts at 97 (`a`) and ends at 122 `z`. 

Other symbols such as `(`, `!`, Tab, carriage return, etc. are also represented in the ASCII table. See [AsciiTable](http://www.asciitable.com/) for the mapping between characters and integer ASCII codes.

An important character to know about is the constant `'\0'` which *represents the character with value zero, sometimes called the **null character***. We will see later when we talk about string handling in C that `'\0'` is used to terminate variable length strings. 


> [!NOTE] Title
> In C, the characters that begin in `\` are called an escape sequence. So the null character and the newline character `'\n'` that we have been seeing within our `printf` statements are both examples of escape sequences.

### String Constants

String constants can be specified using a sequence of zero or more characters enclosed within double quotes, e.g. `"C is fun"`. A string constant is technically an ***array of characters*** (Characters stored in contiguous memory locations) that is terminated by a null character `\0'` at the end. This means that the storage required to represent a string of length n is actually n+1.

Thus we can store strings of arbitrary length in memory as long as they are terminated by a null character (so we know when to stop). We will talk more about `arrays` later.

### Enumeration Constants

An ***enumeration*** is a special data type which specifies a list of constant integer values that can be assigned labels. This provides a convenient way to associate constant values with names. For example, we could store the months of the year like this:

```c
enum Months { JAN = 1, FEB, MAR, APR, MAY, JUN, JUL, AUG, SEP, OCT, NOV, DEC };
```

The default value of the first constant in the list is `0`, but it can be explicitly specified otherwise (as is the case for `JAN` above). Here, the first constant in the list `(JAN)` is the constant `1`. The other constants in the list take on successive values. So, `FEB` is the constant `2`, `MAR` is the constant `3`, and so on. 

> [!NOTE] Note
> I want to emphasize here that `JAN` is not a variable name. Behind the scenes, the compiler treats the constants like `JAN`, `FEB` differently than it treats variable names.

### How to Use Enumeration Constants

With the above code, we have defined a new enumeration data type called `Months`. Now a variable type of `Months` can take on the constant values as defined above. WE can use the symbolic names (e.g. `JAN`) in place of their integer counterparts, for example, like this:

```C
enum Months { JAN = 1, FEB, MAR, APR, MAY, JUN, JUL, AUG, SEP, OCT, NOV, DEC };
enum Months the_month;
the_month = JAN;
...
if (the_month == JAN) {
  printf("It's January\n);
}
```

We haven't covered the code on lines 5-7, but basically these lines check to see if `the_month` contains the constant `JAN`, and if so the message "It's January" is printed out.

### Why Use Enumeration Constants?

Why not just use strings to represent months? One reason is that C strings are slightly clunky to work with, especially compared to interpreted language like Python, R, etc. Comparing two strings in C is not as easy as typing `if (the_month == "JAN")` as above -- it requires a call to a function called `strcmp` in the C Standard Library.

Another reason is because `enum` data types are represented as integers, we can do integer operations (comparisons, arithmetic, etc.) on them. So, for example, we could do something like this:

```C
// If it's greater than APR and less than SEP, then print the string
if ((the_month > APR) && (the_month < SEP)) {
  printf("It's summer!");
}
```

> That’s it for variables and constants. Let’s now move on to making meaningful statements with our declared variables.

## Statements and Scope

> Learn about statements and blocks in C, as well as about the scope of the variable.

### Program Statements in C

In the example of `printf` statements, variable declarations and variable assignments seen so far, you may have observed the semicolon at the end of several lines. This indicates that the line of code is a *program statement in C*. **Lines 5-6** below are C statements. **Line 7** below is also a program statement, a pretty useless one at that, but nonetheless a program statement.

```C
#include <stdio.h>

int main(void)
{
	int i = 1;
	printf("The variable i is %d\n", i);
	;
	return 0;
}
```

But not all program statements in C end in a semicolon. For example, a **block of code** is considered a compound statement in C that's specified by an opening curly bracket `{` and a closing one `}`. It's used for grouping other program statements.

The directive on **line 1** is not a program statement at all as this instruction is processed before the code is compiled and is not executed when the program is run.

### Scope of Variables

The **scope** of a variable refers to its accessibility and visibility from other parts of the the code. If a variable is created inside a block of code, it can't be accessed outside of it. We say that such a variable is ***local to the block***. 

> For example, the variable `i` is created in the block of code on lines **5-8**. As it's local to that block, it can't be accessed on **line 10** and is the source of the error you'll see when the code is run.

```C
#include <stdio.h>

int main(void) {

  { 
    int i = 1; 
    printf("The variable i is in the scope of this block: %d\n", i);
  }
  
  printf("Trying to access i here produce an error: %d\n", i);

  return 0;
}
```

```
main.c: In function 'main': 
main.c:10:60: error: 'i' undeclared (first use in this function) 
	10 | printf("Trying to access i here produce an error: %d\n", i); 
		   |                                                      ^      main.c:10:60: note: each undeclared identifier is reported only once for each function it appears in
```

> If **Line 10** is removed, the code becomes error free. 

There's much more to be said about the scope of a variable. We'll talk more about this later on. We'll also see soon how blocks of code are useful in other contexts.

## Quiz on Basic Types and Statements

```C
int main(void) 

{
  const char x = 'C';
  x = 'B';
  return 0;
}
```
> This code is not valid because: a `const` variable cannot be reassigned a value.

```C
int main(void) 
{
  const char x = 'C';
  printf("%c", x);
  return 0;
}
```
> This code is not valid because `stdio.h` needs to be included for the *print statement to work*.

```C
int main(void) 

{
  const char x = 'C';
  return 0;
}
```
> This code is valid.

```C
#include <stdio.h>

int main(void) 
{
  {
    const char x = 'C';
  }
  printf("%c", x);
  return 0;
}
```
> This code is not valid because the variable `x` can be accessed outside the block in which it's created.

**Given the following enumeration, the constant `East` is which integer constant?**

```C
enum Directions { North, South, East, West };
```
> East is the integer constant of 2, because North is 0, South is 1, because it is not specified on the first constant.

**(True or False) An escape sequence such as `\n` is regarded as two character constants.**

> **B) False**: The escape sequence `\n` may look like it consists of two things `\` and `n`, but actually it’s considered one character—the newline character.

**What’s the length of the string “C is fun”?**

> B) 9: It has 6 letters, 2 space characters, and 1 null character not visible to us.

# Operators and Expressions

## Building Expressions Using Operators

Learn how about arithmetic, relational, and logical operators and how they can be used for building C expressions.

Like in any other programming language, in C, there are many arithmetic, relational, and logical operators that can be used to create `expressions` that are made up of simpler basic types and constants.

