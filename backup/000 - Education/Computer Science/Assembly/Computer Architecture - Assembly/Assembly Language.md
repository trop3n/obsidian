https://x.com/7etsuo/status/1761442647280128487?s=46&t=YKWJdZvvAAWLDqSI47Nh3A

The generated Assembly from the last exercise follows much of the same semantics as the machine code we learned in the ISA lesson. This is because Assembly language and binary code have almost a direct translation between their outputs.

Assembly was created as a **mnemonic language** to make machine code easier to read and write, one instruction translating to one instruction. In fact, most iSAs will have both the binary code and Assembly language breakdown on the same page when talking about specific instructions. 

Just like in binary, Assembly begins with an **opcode**. Luckily for us, the opcodes are much more readable than a bunch of `0`'s and `1`'s.

Let's take a look at the multiply function:

```Assembly
MULT $3, $2
```

> Binary:

```
00000000111001100000000000011000
```

It's easy to see how much easier it is to write a program in Assembly than to write it in binary. In most Assembly instructions, what follows the opcodes are the memory locations to be operated on. These memory locations are referred to as operands. Generally, these are direct register addresses but can also be memory references to values stored in other types of memory such as the `cache` or `RAM`.

In MIPS, direct register addresses begin with the `$` symbol, so in our `MULT` example, we are multiplying the value stored in register `$2` by the value in register `$3`. 
You can learn more about MULT and other MIPS functions in the official [MIPS32 Documentation](https://s3-eu-west-1.amazonaws.com/downloads-mips/documents/MD00086-2B-MIPS32BIS-AFP-6.06.pdf).


# Arithmetic Operations

