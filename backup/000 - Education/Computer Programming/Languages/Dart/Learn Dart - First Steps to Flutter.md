---
up: "[[Dart]]"
tags:
  - "#education/computerprogramming/languages/dart/firststepstoflutter"
---

### Arithmetic Operators

> The normal arithmetic operators used in mathematics are all available in Dart. The only one that might be new is `~/`. `~/` is used to divide both operands, remove the fractional part from the decimal value, and keeps the whole number.

### Prefix and Postfix Operators

Dart also supports both prefix and postfix increment and decrement operators.

Below is a list of the arithmetic prefix and postfix increment and decrement operators supported by Dart.

|**Operator**|**Use**|
|---|---|
|`++`var|var = var + 1|
|var`++`|var = var + 1|
|`--`var|var = var - 1|
|var`--`|var = var - 1|
### The `++` var expression

The expression value of `++var` is `var+1`. When we insert the expression in a print statement, the compiler first increments the variable by 1 and the prints the value of the variable.

```dart
main() {
  var prefixIncrement = 5;

  print(++prefixIncrement);
}
```
> Since the value displayed is after the increment, 6, i.e. 5+1, is displayed as the output.

### The `--` var expression

The expression value of `--var` is `var-1`. When we insert the expression in a print statement, the compiler first decrements the variable by 1 and then prints the value of the variable.

```dart
  var prefixDecrement = 5;

  print(--prefixDecrement);
```
>Output is `4`.

### The var `--` expression

The expression value of `var--` is `var`. When we insert the expression in a print statement, the compiler first prints the value of the variable and then decrements it by 1.

# Equality and Relational Operators

-  Relational Operators
-  Equality Operators

### Relational Operators

> Relational operators are operators that perform operations that compare operands of numeric types, for example, *less than* or *greater than*. Equality operators can compare operands of any type and are two in number (`==` and `?=`)

Below is a list of the equality and relational operators supported by Dart.

| Operator | Use                                                                                                |
| -------- | -------------------------------------------------------------------------------------------------- |
| `==`     | Checks if the values of the two operands are equal (true if equal)                                 |
| `!=`     | Checks if the values of the two operands are not equal (true if not equal)                         |
| `>`      | Checks if the value of the left operand is greater than the value of the right operand             |
| `<`      | Checks if the value of the left operand is less than the value of the right operand                |
| `>=`     | Checks if the value of the left operand is greater than or equal to the value of the right operand |
| `<=`     | Checks if the value of the left operand is less than or equal to the value of the right operand    |
> **Equality and relational operators yield a `boolean` type result.**

```dart
main() {
  var operand1 = 10;
  var operand2 = 7;

  print(operand1 > operand2);
  print(operand1 < operand2):
  print(operand1 >= operand2);
  print(operand1 <= operand2);
}
```
> Output:
> true
> false
> true
> false

### Equality Operators

To understand the equality operators, we will take the following code example. 

```dart
main() {
  var operand1 = 10;
  var operand2 = 7;

  print(operand1 == operand2);
  print(operand2 != operand2);
}
```
> Output:
> false
> true

We can also use equality operators on non-integer literals such as string literals. Let's look at an example where the first operand is `a` and the second operand is `b`.

```dart
main() {

  var operand1 = 'a';
  var operand2 = 'b';

  print(operand1 == operand2);
  print(operand1 != operand2);  

}
```
> Output: 
> false
> true

### Type Test Operators

> Type test operators are operators that can be used to check the type of an object at runtime. Below is a list of the type test operators supported by Dart.

|Operator|Use|
|---|---|
|`as`|typecast|
|`is`|True if the object has the specified type|
|`is!`|False if the object has the specified type|
> We will not be looking at the `as` operator in this course.

### Syntax

While type test operators do have two operands, the order of the operands is important. The value whose type needs to be checked should be on the left of the operator and the type itself should be on the right of the operator.

The basic syntax is:
`value operator type`

```dart
main() {

  double type1 = 5.0;
  int type2 = 87;
  String type3 = "educative";
  bool type4 = true;

  print(type1 is int);
  print(type2 is int);
  print(type3 is String);
  print(type4 is double);
  print(type4 is! double);

}
```

- **Line 7** displays `false` because `type1` is of the type `double` and we are asking the compiler if it is of type `int`
- **Line 8** displays `true` because `type2` is of the type `int` and we are also asking the compiler if it is of the type `int`.
- **Line 9** displays `true` because `type3` is of type `String` and we are also asking the compiler if it of type `String`.
- **Line 10** displays `false` because `type4` is of type `bool` and we are asking the compiler if it is of type `double`.
- **Line 11** displays `true` because `type4` is not of type `double` and we are also asking the compiler if it is not of type `double`.

### Assignment Operators

###### Overview

Assignment operators are used for performing operations that assign a value to an operand.

They are modified versions of all the operators we have discussed so far and the operators we have yet to discuss.

We have already seen how the `=` operator can be used to assign values; we've been using it since the start of this course.

###### Compound Assignment Operators

> Compound assignment operators combine with other operators with the assignment operator 
> (`=`)

|   |   |   |   |   |   |
|---|---|---|---|---|---|
|=|-=|/=|%=|>>=|^=|
|+=|*=|~/=|<<=|&=|\|=|
Here is their general syntax:

`operand1 operator = operand2`

> What's happening is that the operator is performing an operation on **operand1** and **operand2** and then assigning the resultant value to **operand1**

`operand1 = operand1 **operator** operand2`

You might have noticed a pattern. Assignment operators require that its operands be variables as the result of the operation is stored in the left/first operand.

###### Examples

In our example, we will take the left operand `A` to be **10** and the right operand `B` to be 7 and will be using both the assignment operator and compound assignment operators.

###### The += operator

```dart
main() {

  var A = 10;
  var B = 7;

  print("Before using a compound assignment operator:");
  print(A);
  
  A += B;

  print("After using a compound assignment operator:");
  print(A);
}
```
> Output:
> Before using a compound assignment operator
> 10
> After using a compound assignment operator
> 17

Before reassigning the variable `A`, its value was **10**. After using the compound assignment operator `+=`, its new value is **17**. Here, `A += B` is equivalent to `A = A + B`

###### The `&=` Operator

```dart
main() {

  var A = 10;
  var B = 7;

  print("Before using a compound assignment operator:");
  print(A);

  A &= B;

  print("After using a compound assignment operator:");
  print(A);

}
```
```dart
# Output

Before using a compound assignment operator:
10
After using a compound assignment operator:
2
```

> Here, `A &= B` is equivalent to `A = A & B`
> 	The `&` or modulo divides the integer input by the other integer, then rounds to the nearest whole number.

###### The `~/=` Operator

```dart
main() {

  var A = 10;
  var B = 7;

  print("Before using a compound assignment operator:");
  print(A);

  A ~/= B;

  print("After using a compound assignment operator:");
  print(A);

}
```
```dart
# Output

Before using a compound assignment operator: 10 
After using a compound assignment operator: 1
```

Here, `A ~/= B` is equivalent to `A = A ~/ B`.
### Logical Operators

**Logical Operators** are operators that perform logic operations such as the Logical *AND* and Logical *OR*. They take `bool` type operands and yield `bool` type results. 

These are the logical operators supported by Dart:

| Operator | Name        | Use                                                                                                                     |
| -------- | ----------- | ----------------------------------------------------------------------------------------------------------------------- |
| `!`      | Logical NOT | Reverses the logical state of it's operand. If a condition is true, then the Logical *NOT* operator will make it false. |
| `\| \|`  | Logical OR  | If any of the two operands is not false, then the result is true                                                        |
| `&&`     | Logical AND | If both the operands are not false, then the result is true                                                             |
> `!` is a **unary operator**, meaning it takes one operand. 

#### Follow the Rules

> Below is a list of the reduction rules for logical operators. The list is handy as it will summarize how each operator reduces expressions into their final form.

*expr* is an arbitrary expression that can be replaced with an operand of the type `Boolean`.

- The operand can be `true` or `false` itself or can be an expression that reduces to `true` or `false`.

- `!true --> false`
- `!false --> true`
- `true && expr --> expr`
- `false && expr --> false`
- `true || expr --> true`
- `false || expr --> expr`

#### Example

> Let's now see the above rules in action. For example, our arbitrary expression `expr` will be `A && B` where `A` is `true` and `B` is `false`.

```dart
main() {
  var A = true;
  var B = false;
  var expr = A && B; //false

  print(!A); // !true --> false
  print(!B); // !false --> true
  print(true || expr); // true || expr --> true
  print(false || expr); // false || expr --> expr
  print(true && expr); // true && expr --> expr
  print(false && expr); // false && expr --> false

}
```
```
# output
false
true
true
false
false
false
```
`A && B` reduces to `false` as `B` is `false` and from our list of rules, we know that `false && expr --> false`.

### Bitwise and Shift Operators

> Bitwise operators and shift operators are operators that perform operations on individual bits of integer types. Below is a list of the bitwise operators supported by Dart.

#### Types of Bitwise and Shift Operators

Bitwise operators and shift operators are operators that perform operations on individual bits on integer types. Below is a list of the bitwise operators supported by Dart.

| Operator | Name                         | Use                                                                                   |
| -------- | ---------------------------- | ------------------------------------------------------------------------------------- |
| `&`      | Bitwise **AND**              | If the corresponding bit in both operands is `1` it will give a `1`, else `0`.        |
| `\|`     | Bitwise **OR**               | If the corresponding bit in at least one operand is `1` it will give a `1`, else `0`. |
| `^`      | Bitwise **XOR**              | If the corresponding bit in only one operand is `1` it will give a `1`, else `0`.     |
| `~`      | Unary Bitwise **Complement** | Bits which are `0` become `1` and bits which are `1` become `0`.                      |
> Below are the shift operators supported by Dart.

| Operator | Name        | Use                                                                     |
| -------- | ----------- | ----------------------------------------------------------------------- |
| `<<`     | Shift Left  | Shifts all the bits of its operand to the left by the specified amount  |
| `>>`     | Shift Right | Shifts all the bits of its operand to the right by the specified amount |
> Both bitwise and shift operators work on binary numbers

> The numbers are stored in binary form. However, we see the operands and the results in decimal, while the operations take place in binary

#### Follow the Rules

Below we have a list of rules that each bitwise operator follows. For bitwise operators, we work with binary numbers. Hence, instead of false and true, we will be using `1` and `0` where `1` acts as true and `0` acts as false.

**bit** can be either `1` or `0`.

- `~1 --> 0`
- `~0 --> 1`
- `1 & bit --> bit`
- `0 & bit --> 0`
- `1 | bit --> 1`
- `0 | bit --> bit`
- `1 ^ 0 --> 1`
- `0 ^ 1 --> 1`
- `0 ^ 0 --> 0`
- `1 ^ 1 --> 0`

#### Example

```dart
main() {
  var A = 12;
  var B = 5;

  print(~A); // A complement
  print(~B); // B complement
  print(A & B); // A AND B
  print(A | B); // A OR B
  print(A ^ B); // A XOR B
  print(B << 2); // B Shift Left 2
  print(A >> 2); // A Shift Right 2

}
```
```
# output

-13 
-6 
4 
13 
9 
20 
3

```

