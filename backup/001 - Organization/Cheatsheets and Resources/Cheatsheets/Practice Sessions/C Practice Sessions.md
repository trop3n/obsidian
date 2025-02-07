#c #codecademy #practicesession

# Operators

## Logical Operators in C

C can perform logical operations using the following operators:

- and: `&&` (Are both sides true?)
- or: `||` (Is at least one side true?)
- not: `!` (True becomes false and false becomes true)
## Assignment Operations in C

C can assign values to variables and perform basic mathematical operations using shorthand operators:

- Assignment : `=`
- Addition then assignment: `+=`
- Subtraction then assignment: `-=`
- Multiplication then assignment: `*=`
- Division then assignment: `/=`
- Modulo then assignment: `%=`
## Mathematical Symbols

C is able to perform basic mathematical operations on variables and values using the following symbols:

- Addition: `+`
- Subtraction: `-`
- Division: `/`
- Multiplication: `*`
- Incrementing: `++`
- Decrementing: `--`
- Modulo: `%`

## Comparing Values in C:

C can compare two values and/or variables against each other to return true or false. The operators are as follows:

- Do both sides have the same value? `==`
- Do the two sides have different values? `!=`
- Is the left side a lower value than the right side? `<`
- Is the left side a lower or equal value to the right side? `<=`
- Is the left side a greater value than the right side? `>`
- Is the left side a greater or equal value to the right side? `>=`

# Questions (1)

> What will be printed by the following code?

```c
int x = 2;
int y = 3;
if (x == 2 && y == 3) {
	printf("I am here");
}

printf("You are there");
```

Both parts of the `if` statement are true and the logical operator `&&` was used requiring both to be true so both `printf()` statements will run.

> Finish the code below to multiply the variable by 2 and assign the result back to itself.

```C
int x;
x *=2
```

> What would be printed by this code?

```C
int main(){
  int x;
  int y = 17;
  x = y % 2;
  printf("x is now: %d\n", x);
}
```

`%` or modulo returns the remainder after division is performed, so in this case 17/2 is 8 with a remainder of 1, so `x` is set to 1.

**Correct Answer:** `x is now 1`.
# Questions (2)

> The main data types in C are: int, float, double and ...

**Answer**: char

> Fill in the code below to use explicit casting:

```C
int x = 1;
char y = 'c'

x = 
```

You want to tell the compiler to convert to an `int`.

> In the code below, complete the comments with the proper syntax

```
#include <stdio.h>

int main(void) {

}
```