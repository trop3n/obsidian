
## First, Some Background

Assembly language is barebones. The only interface a programmer has above the actual hardware is the *kernel itself*. In order to build useful programs in Assembly we need to use the Linux system calls provided by the kernel. These system calls are a library built into the operating system to provide functions such as reading input from a keyboard and writing output to the screen.

*When you invoke a system call the kernel will immediately suspend execution of your program.* 

It will then contact the necessary drivers needed to perform the task you requested on the hardware and then return control back to your program. 