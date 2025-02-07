---
up: "[[Learn Python]]"
tags:
  - "#education/computerprogramming/platforms/bootdev/python/numbers"
prev: "[[Functions]]"
---
---

# Python Numbers

In Python, numbers without a decimal point are called `Integers` -- just like they are in mathematics.

Integers are simply whole numbers, positive or negative. For example, `3` and `-3` are both examples of integers. 

Arithmetic can be performed as you might expect:
## Addition

```python
2 + 1
# 3
```
## Subtraction

```python
2 - 1
# 1
```
## Multiplication

```python
2 * 2
# 4
```
## Division

```python
3 / 2
# 1.5 (a float)
```

This one is actually a bit different -- division on two integers will actually produce a float. a `float` is, as you might have guessed, the number type that allows for decimal values. 
# Numbers Review

In Python, numbers without a decimal point are called **integers**.

Integers are simply whole numbers, positive or negative. For example, `3` and `-3` are both examples of `ints`.
## Floats

A float is the number type that allows for decimal values.

```python
my_int = 5
my_float = 5.5
```
# Floor Division

Python has great out-of-the-box support for mathematical operations. This, among other reasons, is why it has had such success in artificial intelligence, machine learning, and data science applications.

Floor division is like normal division except the result is [floored](https://en.wikipedia.org/wiki/Floor_and_ceiling_functions) afterward, which means the result is rounded down to the nearest integer. The `//` operator is used for floor division.

```python
7 // 3
# 2 (an integer, rounded down from 2.333)

-7 // 3
# -3 (an integer, rounded down from -2.333)
```
# Exponents

Python has built-in support for exponents - something most languages require a `math` library for. 

```python
# reads as "three squared" or
# "three raised to the second power"
3 ** 2
# 9
```
# Changing in Place

It's fairly common to want to change the value of a variable based on its current value.

```python
player_score = 4
player_score = player_score + 1
# player_score now equals 5
```

```python
player_score = 4
player_score = player_score - 1
# player_score now equals 3
```

Don't let the fact that the expression `player_score = player_score - 1` is not a valid mathematical expression be confusing. *It doesn't matter, it is valid code*. It's valid because the way the expression should be read in English is:

> Assign to `player_score` the current value of `player_score` minus 1.

In this operation, the right-hand side (`player_score - 1`) is calculated first. Once we have the result, we update `player_score` with this new value.
# Plus Equals

Python makes reassignment easy when doing math. In JavaScript and Go, you might be familiar with the `++` syntax for incrementing a number variable by 1. In Python, we use the `+=` [in-place operator](https://docs.python.org/3/library/operator.html#in-place-operators) instead.

```python
star_rating = 4
star_rating += 1
# star_rating is now 5
```
## Other Operators

The other in-place operators work similarly:

```python
star_rating = 4
star_rating -= 1
# star_rating is now 3

star_rating = 4
star_rating *= 2
# star_rating is now 8

star_rating = 4
star_rating /= 2
# star_rating is now 2.0
```
# Scientific Notation

As we covered earlier, a `float` is a positive or negative number **with a fractional part**.

You can add the letter `e` or `E` followed by a positive or negative integer to specify that you're using [scientific notation](https://en.wikipedia.org/wiki/Scientific_notation).

```python
print(16e3)
# Prints 16000.0

print(7.1e-2)
# Prints 0.071
```

If you're not familiar with scientific notation, it's a way of expressing numbers that are too large or too small to conveniently write normally. 

In a nutshell, the number following the `e` specifies how many places to move the decimal to the right for a positive number, or to the left for a negative number.
## Underscores for Readabilility

Python also allows you to represent large numbers in the decimal format using underscores as the delimiter instead of commands to make it easier to read. 

```python
num = 16_000
print(num)
# Prints 16000

num = 16_000_000
print(num)
# Prints 16000000
```
## Assignment

Due to the constraints of our app's server, there is a maximum number of players we can have on a single "Fantasy Quest" server.

Complete the `max_players_on_server` function. It takes no inputs, but simply returns 3 static values:

1. The max players on a "small" server: `1,024,000,000,000,000,000` (`1.024e18`)
2. The max players on a "medium" server: `10,240,000,000,000,000,000`
3. The max players on a "large" server: `102,400,000,000,000,000,000`

Use scientific notation to represent these numbers. For example: `3.104e15`.
# Logical Operators

You're probably familiar with the logical operators `and` and `or`. 

Logical operators deal with [boolean values](https://en.wikipedia.org/wiki/Boolean_data_type), `True` and `False`.

The logical `and` operator requires that *both* inputs are `True` to return `True`. The logical `or` operator only requires that *at least* one input is `True` to return `True`.

For example:

```
True and True == True
True and False == False
False and False == False

True or True == True
True or False == True
False or False == False
```
## Python Syntax

```python
print(True and True)
# prints true

print(True or False)
# prints true
```
## Nesting with Parenthesis

We can nest logical expressions using parenthesis

```python
print((True or False) and False)
```

First, we evaluate the expression in the parenthesis, `(True or False)`. It evaluates to `True`:

```python
print(True and False)
```

`True and False` evaluates to `False`:

```python
print(False)
```

So, `print((True or False) and False)` print's "false" to the console. 
## Not

We skipped a very important logical operator - `not`. The `not` operator reverses the result. It returns `False` if the input was `True` and vice-versa.

```python
print(not True)
# Prints: False

print(not False)
# Prints: True
```
# Binary Numbers

[Binary numbers](https://en.wikipedia.org/wiki/Binary_number) are just **base 2** numbers. They work the same way as "normal" base 10 numbers, but with two symbols instead of ten. 

- Base-2 (binary) symbols: `0` and `1`
- Base-10 (decimal) symbols: `0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10`

Each `1` in a binary number represents an ever-greater multiple of 2. In a 4-digit number, that means you have the eights place, the fours place, the twos place, and the ones place. Similar to how in decimal you would have the thousands place, the hundreds place, the tens place, and the ones place. 

![](https://i.imgur.com/GiQDQWI.png)

- `0001` = 1
- `0010` = 2
- `0011` = 3
- `0100` = 4
- `0101` = 5
- `0110` = 6
- `0111` = 7
- `1000` = 8
- `1001` = 9
- `1010` = 10
- `1011` = 11
- `1100` = 12
- `1101` = 13
- `1110` = 14
- `1111` = 15
## Binary in Python

You can write an integer in Python using binary syntax using the `0b` prefix.

```python
print(0b0001)
# Prints 1

print(0b0101)
# Prints 5
```
# Bitwise "&" Operator

Bitwise operators are similar to logical operators, but instead of operating on boolean values, they apply the same logic to all the bits in a value by column. For example, say you had the numbers `5` and `7` represented in binary. You could perform a bitwise "and" operator and the result would be `5`.

- `0101` is 5
- `0111` is 7

```
0101
&
0111
=
0101
```

A `1` in binary is the same as `True`, while `0` if `False`. So really a bitwise operator is just a bunch of logical operations that are completed in tandem by column.

```
0 & 0 = 0
1 & 1 = 1
1 & 0 = 0
```

Ampersand `&` is the bitwise "and" operator in Python. "And" is the *name* of the bitwise operation, while ampersand `&` is the *symbol* for that operation. For example, `5 & 7 = 5`, while `5 & 2 = 0`.

- `0101` is 5
- `0010` is 2

```
0101
&
0010
=
0000
```
## Binary Notation

When writing a number in binary, the prefix `0b` is used to indicate that what follows is a binary number. `0b10` is two in binary, but `10` without the `0b` prefix is simply ten.

- `0b0101` is 5
- `0b0111` is 7
## Putting it Together

```python
0b0101 & 0b0111
# equals 5

binaryFive = 0b0101
binarySeven = 0b0111
binaryFive & binarySeven
# equals 5
```
## Guild Permissions

Sometimes applications store user permissions as binary values. If we have `4` different permissions a user can have, then I can store that as a 4-digit binary number, and if a certain bit is present, I know the permission is enabled. This can be a lot more efficient than storing entire strings. 

Let's pretend we have 4 permissions related to "guilds" in Fantasy Quest ("guild in just a fancy videogame term for "team").

- `can_create_guild` - leftmost bit (`0b1000`)
- `can_review_guild` - second to leftmost bit (`0b0100`)
- `can_delete_guild` - second to rightmost bit (`0b0010`)
- `can_edit_guild` - rightmost bit (`0b0001`)

If a user has *no* permissions, their binary permissions would be `0b0000`, but a user with `can_review_guild` *and* `can_edit_guild` permissions would be `0b0101`.

To check for say, the `can_review_guild` permission, we can perform a bitwise *and* operation of the user's permissions and the enabled `can_review_guild` bit (`0b0100`). If the result is `0b0100` again, we know that they have that specific permission.
## Assignment

Complete each of the `get_XXX_bits` functions. Use the bitwise `&` operation on the user's permission bits and the appropriate guild permission bits, and return the resulting bits.

4 values have been provided, use the appropriate one for each function:

- `can_create_guild`
- `can_review_guild`
- `can_delete_guild`
- `can_edit_guild`

Note: The `get_XXX_bits` functions return the bits and the test code compares the result to the original permission value to see if it matches!
# Bitwise `|` Operator

As you may have guessed, the bitwise "or" operator is similar to the bitwise "and" operator in that it works on binary rather than boolean values. However, the bitwise "or" operator "or"'s the bits together. Here's an example:

- `0101` is 5
- `0111` is 7

```
0101
|
0111
=
0111
```

A `1` in binary is the same as `True`, while `0` is `False`. So a bitwise operation is just a bunch of logical operations that are completed in tandem. When two binary numbers are "or"ed together, the result has a `1` in any place where *either* of the input numbers has a `1` in that place. 

`|` is the bitwise "or" operator in Python. `5 | 7 = 7` and `5 | 2 = 7` as well. 

- `0101` is 5
- `0010` is 2

```
0101
|
0010
=
0111
```
## Guild Permissions

A "guild" is a team of 2-4 players. Here are the guild-specific permissions:

- `can_invite` - Leftmost bit (`0b1000`)
- `can_kick` - Second to leftmost bit (`0b0100`)
- `can_enter_dungeon` - Second to rightmost bit (`0b0010`)
- `can_surrender` - Rightmost bit (`0b0001`)

When players are in a guild together, they gain _all_ the permissions of _all_ the other members of the guild!

For example, if:

- Jack has the `can_invite` permission: `0b1000`
- Jill has the `can_kick` permission: `0b0100`

Then, when they are partied together, they should both have the `can_invite` and `can_kick` permissions: `0b1100`.

## Assignment

Complete the `calculate_guild_perms` function. It should return a binary number that represents the permissions of _all_ the members of the guild (Glorfindel, Galadriel, Elendil and Elrond).

Use a series of bitwise "or" operations to calculate the [superset](https://www.youtube.com/watch?v=1wsF9GpGd00) of all the member's permissions.