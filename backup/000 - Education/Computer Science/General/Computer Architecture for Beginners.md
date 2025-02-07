#computerscience #computerarchitecture 

# Introduction

Before we understand the function and structure of computers, we have to make the distinction between Computer Architecture and *Computer Organization*. **Computer Architecture** refers to the logical aspect of a system.

**Computer Organization** on the other hand, defines the physical aspects of a system that implements a particular architecture.

- Hardware details transparent to the programmer (ex: control signals)
- Interfaces between the computer and *peripherals*
- The memory technology used
## Computer-Level Hierarchy

Complex computer systems employ a series of virtual machine layers. It is a **hierarchical structure** in which each layer can focus on its own tasks without needing to manage the complexities of the layers below:

| ***Level*** | ***Type***            | ***Programs***                  |
| --------- | ------------------- | ----------------------------- |
| `Level 6` | User                | Executable Programs           |
| `Level 5` | High-Level Language | C++, Java, FORTRAN, etc.      |
| `Level 4` | Assembly Language   | Assembly Code                 |
| `Level 3` | System Software     | Operating System Library Code |
| `Level 2` | Machine             | Instruction Set Architecture  |
| `Level 1` | Control             | Microcode or Hardwired        |
| `Level 0` | Digital Logic       | Circuits, Gates, etc.         |
Let's say you want to save a file on your computer:

- **User Level Layer**: You click "Save" in your application UI.
- **High-Level Language (HLL)**: Your application, which is written in a high-level language like Java or C++ is *compiled* directly into machine code. 
- **Assembly Language Level**: Assembly language is a low-level but human-readable code which is *assembled* into machine code. Some HLLs may compile to Assembly as an intermediate step.
- **System Software Layer**: The Operating System receives the command and decides how to manage the file system.
- **Instruction Set Architecture (ISA)**: The operating system uses the ISA which defines the set of instructions to be sent to the CPU.
- **Mircoarchitecture Layer**: This defines how a particular processor design implements the ISA. The CPU fetches instructions from memory, decodes them, and directs appropriate components to execute them.
- **Hardware Layer**: Electrical signals that represent the binary instructions and data are executed at this level.

*A computer instruction refers to a binary code that controls how a computer performs micro-operations in a series*

We talk about Computer Architecture and Organization within the **ISA Layer**. This defines the computer instructions and algorithms for executing commands.
## Structure and Function of a Computer

Let's first talk about a Single-Processor computer and then examine a typical Multi-core structure.
### Single Processor Computer

There are 4 main structural components:

1. **Central Processing Unit (CPU)**: often simply referred to as the **processor**.
2. **Main Memory (RAM)**: 
3. **I/O**: When data is moved to or from a device that is directly connected to the computer it is called *Input-Output (I/O)*. The device is referred to as a *peripheral*. When data is moved over longer distances, to or from a remote device, the process is known as *data communications*.
4. **System Interconnection**: Some mechanism that provides for communication among CPU, main memory, and I/O. (ex: *system bus:* a number of conducting wires to which all the other components attach.)

The below figure shows the hierarchical view of the internal structure of a traditional single-processor computer:

![](https://i.imgur.com/n7qtKov.png)

Note the similarity between the internal structure of the computer as a whole, and the internal structure of the processor. In both cases, there is a small collection of major elements (computer: processor, I/O, memory; processor: control unit, ALU, registers) connected by data paths. We'll talk about all of these components in a bit.
### Multi-Core Computer

Most modern computers have multiple processors. When these processors all reside on a single *chip*, it is called a *multicore computer*. Each processing unit is called a **core**.

> *A core is an individual processing unit on a processor chip. A core may be equivalent in functionality to a CPU on a single CPU system*

The CPU / Processor, is a physical piece of silicon that has one or more cores. The processor is the computer components that interprets and executes instructions. There are four major structural components of the processor:

1. **Control Unit**: Controls the operation of the CPU
2. **Arithmetic and Logic Unit** (ALU): Performs the computer's data processing functions.
3. **Registers**: Provides storage space for high-speed temporary memory that's used to transfer data to the CPU for immediate data processing. 
4. **CPU interconnection**: Some mechanism that provides for communication among the control unit, ALU, and registers.
### Cache Memory

Another important feature of modern computers is the use of multiple layers of memory, called *cache memory*, **between the processor and main memory**. Cache memory is smaller and faster than main memory and is used to speed up memory access by placing in the data from main memory, that is likely to be used in the future.

A greater performance improvement can be obtained by using **multiple levels of cache**, with level 1 (L1) closest to the core and additional levels (L2, L3 and so on) progressively farther from the core. The closer the cache level is to the core, the smaller and faster it is.
### The Motherboard

We said earlier, that these processors all reside on a single chip. A chip, or **Integrated Circuit**, (IC) is a single piece of silicon, where electronic circuits and logic gates are fabricated. These chips join together to form a **Printed Circuit Board** (PCB) -- a rigid, flat board that holds and inter-connects chips and other electronic components using Copper pathways.

The main PCB in a computer is called a system board or **motherboard**, while smaller ones that plug into the slots in the motherboard are called **expansion boards**. The motherboard has slots for the processor chip, memory chips, I/O controller chips, and other key computer components. Here's a simplified view of the components of a motherboard:

![](https://i.imgur.com/GqjrpXs.png)

The expansion board slots allow you to include more components. A modern motherboard connects only a few individual chip components, with each chip containing from a few thousands up to hundreds of millions of transistors.

Let's zoom in on the functional elements of a core in the figure above:

1. **Instruction Logic**: This includes the tasks involved in fetching instructions, and decoding each instruction to determine the instruction operation and the memory locations of any operands. 
2. **Arithmetic and Logic Unit (ALU)**: Performs the operation specified by an instruction.
3. **Load/Store Logic**: Manages the transfer of data from main memory via cache.

The core Also contains an L1 Cache, split between an instruction cache (I-cache) that is used for the transfer of instructions to and from main memory, and an L1 data cache, for the transfer of operands and results. Typically, today's processor chips also include an L2 cache as part of the core. 
# Computer Architecture for Beginners: The Von Nuemann Machine
https://medium.com/@ckekula/computer-architecture-for-beginners-part-2-ae5015f34876

In part 1 we talked about the basic structure and function of a computer. In order to dive deeper, we have to first understand first-generation computers. 
## The IAS Computer

The first generation of computers (ex: ENIAC: the first programmable, electronic, general-purpose digital computer) used vacuum tubes for digital logic elements and memory. Perhaps the most famous first-generation computer, is the IAS computer, (Institute of Advanced Study, Princeton). The fundamental design approach first implemented in the IAS computer is known as the **stored program concept**. 

This idea is attributed to the mathematician **John Von Nuemann**, and the first publication of this idea was for a computer called the **EDVAC**, All of today's computers have this same general structure and function and are referred to as **Von Nuemann Machines**. So, it's important to understand the operation of the IAS computer.

The design of the IAS computer is based on three key concepts:

1. Data and instructions both, are stored in a **single read-write memory**.
2. The contents of this memory are **addressable by location**.
3. **Execution occurs sequentially** from one instruction to the next.

> An instruction consists of two parts: The **opcode**; tells the processor what operation to perform (ex: add, subtract, load, store), and the **operand**; the data that the operation (specified the opcode) will be performed on. It can be a value a register, or a memory location. An instruction can have multiple operands. If the operand refers to data stored in memory, the **address** specifies the exact location in memory where this data is found. The address may also indicate where the result of an operation should be stored.
## Structure of the IAS Computer

Let's first look at what a processor must do:

- **Fetch Instruction**: The processor reads an instruction from memory (register, cache, main memory).
- **Interpret Instruction**: The instruction is decoded to determine what action is required. 
- **Fetch Data**: The execution of an instruction may require reading data from memory or an I/O module.
- **Process Data**: The execution of an instruction may require performing some arithmetic or logical operation on data.
- **Write Data**: The results of an execution may require writing data to memory or an I/O module.

To do these things, it's probably clear to you that the processor needs to store some data temporarily. This is done with the use of *registers*.
## Register Organization

The registers in the processor perform two roles:

1. **User-visible registers**: Enable the machine - or assembly language programmer to minimize main memory references by optimizing use of registers.
2. **Control and Status Registers**: Used by the control unit to control the operation of the processor and by privileged, operating system programs to control the execution of programs.
### User Visible Register

A user-visible register is one that may be referenced by means of the machine language that the processor executes. We can characterize these in the following categories:

- General purpose
- Data
- Address
- Condition codes

**General Purpose Registers** can be assigned to a variety of functions by the programmer. Often, however, there are restrictions. For example, there may be dedicated registers for floating-point and stack operations.

**Data Registers** may be used only to hold data and cannot be employed in the calculation of an operand address.

**Address Registers** may themselves be somewhat general purpose, or devoted to a particular addressing mode. For example:

- ***Segment Pointers***: In a machine with segmented addressing, a segment register holds the address of the base of the segment. There may be multiple registers: for example, one for the operating system and one for the current process.
- ***Index Registers***: These are used for indexed addressing and may be auto-indexed.
- ***Stack Pointer***: If there is user-visible stack addressing, then typically there is a dedicated register that points to the top of the stack. This allows implicit addressing; that is, push, pop and other stack instructions need not contain an explicit stack operand.

**Status Codes** are a category of registers, which is at least partially visible to the user, holds condition codes (also referred to as **flags**). Condition codes are bits set by the processor hardware as the result of operations.
	For example, an arithmetic operation may produce a positive, negative, zero, or overflow insult. In addition to the result itself being stored in a register, a condition code is also set.
### Control and Status Registers

There are the variety of processor registers we talked about in the last part, that are employed to control the operation of the processor. Most of these, on most machines, are not visible to the user. The following diagram shows how the registers interact with one another:

![](https://i.imgur.com/Idow7wN.png)

In the above figure, both the control unit and the ALU contain different types of storage locations, called *registers*. These are defined as follows:

1. **Memory Buffer Register (MBR)**: Contains a *`word*`* to be stored in memory or sent to the I/O unit.
2. **Memory Address Register (MAR)**: Specifies the address in memory of the word to be written from or read into the MBR.
3. **Instruction Register (IR)**: Contains the 8-bit opcode (operation code) of the instruction being executed.
4. **Instruction Buffer Register (IBR)**: Employed to hold temporarily the right-hand instruction from a word in memory.
5. **Program Counter (PC)**: Contains the address of the next instruction pair to be fetched from memory.
6. **Accumulator (AC)**: and **Multiplier Quotient (MQ)**: Employed to hold temporarily operands and results of ALU operations.

> Words are the "natural" unit of organization of memory, each which stores data and instructions. The size of a word is typically equal to **the number of bits used to represent an integer and**
> **to the instruction length.**

Many processor designs also includes a register or set of registers, often known as the **program status word (PSW)**, that contain status information. The PSW typically contains **condition codes** plus other status information. Common fields or flags include the following:

- `Sign`: Contains the sign bit of the result of the last arithmetic operation.
- `Zero`: Set when the result is 0.
- `Carry`: Set if an operation resulted in a carry (addition) into or borrow (subtraction) out of a high-order bit. Used for multiword arithmetic operations.
- `Equal`: Set if a logical compare result is equality.
- `Overflow`: Used to indicate arithmetic overflow.
- `Interrupt Enable/Disable`: Used to enable or disable interrupts.
- `Supervisor`: Indicates whether the processor is executing in supervisor or user mode. Certain privileged instructions can be executed, and certain areas of memory can be accessed only in supervisor mode.

Here's an example Microprocessor register organizations:

![](https://i.imgur.com/cxMELiO.png)
# The Instruction Cycle

In the [last part](https://medium.com/@ckekula/computer-architecture-for-beginners-part-2-ae5015f34876) we talked about the structure of the Von Neumann machine. Now let’s talk about it’s function.
## Instructions

Typically both instructions and data are 16 bits long. Thus, it is convenient to organize memory using 16-bit *words*.

An instruction has a format that provides 4 bits for the opcode, (so that there can be as many as $2^4 = 16$ different opcodes, and up to $2^12 - 4096$ words of memory can be directly addressed.)

![](https://i.imgur.com/bIFCsG3.png)

In the Von Nuemann machine, a word has a size of 40 bits. Here's how a word stores instructions:

![](https://i.imgur.com/KTatxm7.png)

The word contains two 20-bit instructions, with each instruction consisting of an 8-bit opcode specifying the operation to be performed, and a 12-bit address designating one of the words in memory (numbered 0 to 999).

Here's how a word stores a number:

![](https://i.imgur.com/Utvrrqz.png)

The word contains a number of 40 bits represented by a sign bit and a 39-bit value.

Of the registers we discussed above, the CPU typically makes use of 2 in order to exchanges data with memory:

1. **MAR**; which specifies the address in memory for the next read or write,
2. **MBR**; which contains the data to be written into memory or receives the data read from memory.

The following figure shows a simplified view of the internal structure of a processor:

![](https://i.imgur.com/gIMiIin.png)

The data transfer and logic control paths are indicated, including an element labeled [_internal processor bus_](https://medium.com/@ckekula/computer-architecture-for-beginners-interconnection-structures-d4c851c655f2), to transfer data between the various registers and the ALU.
## The Instruction Cycle

The basic function performed by a computer is execution of a program, which consists of a set of instructions stored in memory. The processing required for a single instruction is called an **instruction cycle**. Each instruction cycle consists of two sub-cycles:

- **Fetch Cycle**
- **Execute Cycle**

![](https://i.imgur.com/V75SuqE.png)
### Fetch Cycle

At the beginning of each instruction cycle, the processor fetches an instruction from memory. The **PC** holds the address of the **instruction to be fetched next**, and the processor increments the PC after each instruction fetch so that it will fetch the next instruction in sequence.

> For example, the processor may fetch an instruction from location 149, which specifies that the next instruction be from location 182. The processor will remember this fact by setting the program counter to 182. Thus, on the next fetch cycle, the instruction will be fetched from location 182 than 150.

Then the opcode of the instruction is loaded into the **IR** and the address portion is loaded into the **MAR**.
### Execute Cycle

Once the opcode is in the IR, control circuitry interprets the opcode and executes the instruction by sending out the appropriate control signals to cause an action to be performed by the ALU. Now, the **MBR** stores the data specified by the address in **MAR** and executes the instruction.
## Examples
### 1. A Simple Example:

The program fragment shown below, adds the contents of the memory word at address 940, to the contents of the memory word at address 941 and stores the result in 941.

![](https://i.imgur.com/V7K5qUu.png)

Three instructions, which can be described as three fetch and three execute cycles, are required:

1. The PC contains 300, the address of the first instruction., This instruction (the value 1940 in hexadecimal) is loaded into the **IR**, and the **PC** is incremented. (Note that this process will also involve the user of the **MAR** and a **MBR**).
2. The first 4 bits (digit 1 of 1940) in the **IR** indicate that the **AC** is to be loaded. The remaining 12 bits specify the address (940) from which data are to be loaded.
3. The next instruction (5941) is fetched from location 301, and the **PC** is incremented.
4. The old contents of the **AC** and the contents of location 941 are added, and the result is stored in the **AC**.
5. The next instruction (2941) is fetched from location 302, and teh PC is incremented.
6. The contents of the AC are stored in location 941.
### 2. A More Complex Example:

Suppose that the Program Counter consists of the value  5208 and the right hand side instruction is executed first.

![](https://i.imgur.com/WGjBzRp.png)

![](https://i.imgur.com/PNYTVgZ.png)

- The PC contains 5208, the address of the instruction.
- The **MBR** contains the data (0x0988A0A000) corresponding to the address 5208 as a 40 digit binary number:

`00001001 100010001010 00001010 000000000000`

- The data is split into two and, as stated above, initially the right instruction (`0A 000`) is fetched for execution.
- The opcode of the right instruction (`0A`) is loaded into the **IR** as an 8-bit binary number (00001010). This specifies which of the 21 instructions is to be executed.
- The PC also sends the operand address (000) of the right instruction as a binary number (000000000000) to the **MAR**. This specifies which of the 1000 memory locations is to be involved int he execution of the instruction.
- Meanwhile, the left instruction (`0988A`) is temporarily saved at the **IBR**.
- While the right instruction is executing, the PC increments by 1 and the cycle starts again for the instruction at the address 5209.
# The Interrupt Cycle

