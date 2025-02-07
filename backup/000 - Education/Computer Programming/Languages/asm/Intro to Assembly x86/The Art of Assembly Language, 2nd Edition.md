---
up: "[[Languages]]"
tags:
  - education/computerprogramming/languages/asm/artofassembly
---

# Hello, World of Assembly Language

This chapter is a “quick-start” chapter that lets you start writing basic assembly language programs as rapidly as possible.

This chapter does the following:
- Presents the basic syntax of an HLA (High Level Assembly) program
- Introduces you to the Intel CPU architecture
- Provides a handful of data declarations, machine instructions, and high-
	level control statements
- Describes some utility routines you can call in the HLA Standard Library
- Shows you how to write some simple assembly language programs

By the conclusion of this chapter, you should understand the basic
syntax of an HLA program and should understand the prerequisites that are
needed to start learning new assembly language features in the chapters that
follow.

## 1.1 The Anatomy of an HLA Program

> A typical HLA program takes the form shown in Figure 1-1.

![](https://i.imgur.com/R0srxUf.png)

`pgmID` in the template above is a user-defined program identifier. You *must pick an appropriate descriptive name for your program*. 

If you are writing programs in the course of an assignment, your instructor will probably give you the name to use for your main program. If you are writing your own HLA program, you will have to choose an appropriate name for your project.

**Identifiers** in HLA are very similar to identifiers in most high-level languages. HLA identifiers may begin with an underscore or an alphabetic character and may be followed by zero or more alphanumeric or underscore characters. 

- HLA's identifiers are `case neutral`. This means that the identifiers are case sensitive insofar as you must always spell an identifier exactly the same way in your program (even with respect to upper and lowercase). 
- However, unlike in case-sensitive languages such as C/C++, you may not declare two
	identifiers in the program whose name differs only by alphabetic case.

```
program helloWorld;
# include( "stdlib.hhf" );

begin helloWorld;

	stdout.put( "Hello, World of Assembly Language", nl );

end hellWorld;
```

- The `#include` statement in this program *tells the HLA compiler* to include a set of declarations from the `stdlib.hhf` (standard library, HLA Header File). Among other things, this file contains the declaration of the `stdout.put` code that this program uses. 
- The `stdout.put` statement is the **print statement** for the HLA language.
	- It is used to write data to the standard output device (generally the console).
- Note that semicolons follow the `program`, `begin`, `stdout.put` and `end` statements.
- A semicolon does **NOT** follow the `include` statement, technically speaking.

The `#include` is our first introduction to HLA declarations. The `#include` itself isn't *actually a declaration*, but it does tell the HLA compiler to substitute the file `stdlib.hhf` in place of the `#include` directive, thus inserting several declarations at this point in the program.

> Most HLA programs you will write will need to include one or more of the HLA Standard Library header files (`stdlib.hhf` actually includes all the standard library definitions into our program.)

Compiling this program produces a *console application*. Running this program in a command window prints the specified string, and then control returns to the command-line interpreter.

The HLA compiler 2 is a traditional command-line compiler, which means that you need to run it from a Windows command-line prompt or a Linux/FreeBSD/Mac OS X shell. To do so, enter something like the following into the command-line prompt or shell window:

```
hla hw.hla
```

This command tells HLA to compile the hw.hla (helloWorld) program to an executable file. Assuming there are no errors, you can run the resulting program by typing the following command into your command prompt window (Windows):

```
hw
```

or into the shell interpreter window (Linux/FreeBSD/Mac OS X):

```
./hw
```

If you’re having problems getting the program to compile and run properly, please see the HLA installation instructions on the HLA down- load page. These instructions describe in great detail how to install, set up, and use HLA.

## 1.3 Some Basic HLA Declarations

> HLA predefines several different signed integer types including `int8`, `int16`, `int32`, corresponding to `8bit` (1-byte) signed integers, 16-bit (2-byte) signed integers, and 32-bit (4-byte) signed integers, respectively.

Typical variable declarations occur in the HLA *static variable section*. 

![](https://i.imgur.com/wxr0G8Q.png)

This example demonstrates how to declare three separate integers: `i8`, `i16` and `i32`. Of course, in a real-world program you should use variable names that are more **descriptive**. While names like `i8` and `i32` describe the *type of the object*, they do not describe it's purpose. 

Variable names should describe the purpose of the object.

