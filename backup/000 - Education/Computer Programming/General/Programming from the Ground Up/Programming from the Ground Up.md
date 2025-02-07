---
up: "[[General]]"
tags:
  - "#education/computerprogramming/general/programmingfromthegroundup"
source: https://download-mirror.savannah.gnu.org/releases/pgubook/ProgrammingGroundUp-1-0-booksize.pdf
---

# Chapter 1. Introduction
## Welcome to Programming

Programming is like poetry. It conveys a message, not only to the computer, but to those who modify and use your program. With a program, you build your own world with your own rules. You create your world according to your conception of both the problem and the solution. 

Masterful programmers create worlds with programs that are clear and succinct, much like a poem or essay.

One of the greatest programmers, Donald Knuth, describes programming not as telling a computer how to do something, but telling a person how they would *instruct a computer to do something*. The point is that programs are meant to be read by people, not just computers. Your programs will be modified and updated by others long after you move on to other projects. Thus, programming is not as much about communicating to a computer as it is communicating to those who come after you. 

A programmer is:

- A problem solver
- A poet
- An instructor

All at the same time. 

Your goal is to solve the problem at hand, and teach your solution to future programmers. 

At the end of this book, you should be able to do the following:

- Understand how a program works and interacts with other programs
- Read other people's programs and learn how they work
- Learn new programming languages quickly
- Learn advanced concepts in computer science quickly
## Chicken and the Egg

There is somewhat of a chicken and egg problem in teaching programming, especially assembly language. There is a lot to learn - it's almost too much to learn almost at once, but
***each piece depends upon the others***. Therefore, you must be patient with yourself and the computer while learning to program. If you don't understand something the first time, **reread** it. If you still don't understand it, it is sometimes best to take it by faith and come back to it later. 
## GNU/Linux

Linux is the name of the **kernel**. The kernel is the core part of an operating system that keeps track of everything. The kernel is both a fence and a gate. As a gate, it allows programs to *access hardware in a uniform way*. Without the kernel, you would have to write programs to deal with every device model ever made. The kernel handles all device-specific interactions so you don't have to. It also handles **file access and interaction between**
**processes**. 

For example, when you type, your typing goes through several programs before it hits your editor. First, the kernel is what handles your hardware, so it is the first to receive notice about the keypress. The keyboard sends in *scancodes* to the kernel, which then converts them to the actual letters, numbers and symbols they represent. 
### Example 1-1. How The Computer Processes Keyboard Signals

`Keyboard -> Kernel -> Windowing System -> Application Program`

The kernel also control the flow of information between programs. The kernel is the program's **gate** to the world around it. Every time that data moves between processes, the kernel controls the messaging. 

As a fence, the kernel prevents programs from accidentally overwriting each other's data and from accessing files and devices that they don't have permission to. It limits the amount of damage a poorly-written program can do to other running programs.

Think of the kernel as the water pipes in a house. Without the pipes, the faucets don't work, but the pipes are pretty useless if there are not faucets. Together, the user applications (from the GNU project and other places) and the kernel (Linux) make up the entire operating system, GNU/Linux.
## Assembly Language

There are essentially three kinds of languages:
### Machine Language

This is what the computer actually sees and deals with. Every command the computer sees is given as a number or sequence of numbers.
### Assembly Language

This is the same as machine language, except the command numbers have been replaced by letter sequences which are easier to memorize. Other small things are done to make it easier as well.
### High-Level Language

High-level languages are there to make **programming easier**. Assembly language requires you to work with the machine itself. High-level languages allow you to describe the program in a more natural language. A single command in a high-level language is equivalent to several commands in an assembly language.
# Chapter 2. Computer Architecture

Before learning how to program, we first need to understand how a computer interprets programs. You don't need a degree in electrical engineering, but you need to understand the basics. 

Modern computer architecture is based of an architecture called the **Von Neumann** architecture, named after its creator. The Von Neumann architecture divides the computer up into two main parts - the CPU (for Central Processing Unit) and the memory. This architecture is used in all modern computers, including personal computers, supercomputers, mainframes, and even cell phones.
## Structure of Computer Memory

To understand how the computer views memory, imagine your local post office. They usually have a room filled with PO Boxes. These boxes are similar to computer memory in that each are numbered sequences of fixed-size storage locations. For example , if you have 256 megabytes of computer memory, that means that your computer contains roughly 256 million fixed-size storage locations. 

Or, to use our analogy, 256 million PO Boxes. Each location has a number, and each location has the same, fixed-length size. The difference between a PO Box and computer memory is that you can store all different kinds of things in a PO Box, but you can only store a single number in a computer memory storage location.

You may wonder why a computer is organized this way.

- It is because it is **simple to implement**. 
- If the computer were composed of a lot of differently-sized locations, or if you could store different kinds of data in them, it would be difficult and expensive to implement. 

The computer's memory is used for a number of different things. All of the results of any calculations are stored in memory. In fact, everything that is "stored" is stored in memory.

Think of what is stored in your home computer's memory:

- The location of your cursor on the screen
- The size of each window on the screen
- The shape of each letter of each font being used
- The layout of all the controls on each window
- The graphics for all of the toolbar icons
- The text for each error message dialog box
- The list goes on and on....

In addition to all of this, the Von Neumann architecture specifies that not only
computer data should live in memory, but the programs that control the computer’s
operation should live there, too. In fact, in a computer, there is no difference
between a program and a program’s data except how it is used by the computer.
They are both stored and accessed the same way.
## The CPU

So how does the computer function? Obviously, simply storing data doesn't do much help, you need to be able to access, manipulate, and move it. That's where the CPU comes in. 

The CPU reads in instructions from memory one at a time and executes them. This is known as the *fetch-execute cycle*. The CPU contains the following elements to accomplish this:

- Program Counter
- Instruction Decoder
- Data bus
- General-purpose registers
- Arithmetic and logic unit
### Program Counter

The *program counter* is used to tell the computer **where to fetch the next instruction from**. We mentioned earlier that there is no difference between the way data and programs are stored, they are just interpreted differently by the CPU. The program counter holds the memory address of the next instruction to be executed. The CPU begins by looking at the program counter, and fetching whatever number is stored at the location specified. It is then passed onto the *instruction decoder*.
### Instruction Decoder

The *instruction decoder* figures out what the instruction means. This includes what process needs to take place 