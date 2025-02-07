#computerscience #codecademy #computerarchitecture #assembly 

# Introduction

The goal of this unit is to better understand computer architecture.

After this unit, you should be able to:

- Explain the Components of Computer Architecture
- Explain some of the processes for improving computer architecture

You will eventually put all of this knowledge into practice with an upcoming Portfolio Project. You can complete the Portfolio Project either in parallel with or after taking the prerequisite content—it’s up to you!

Learning is social. Whatever you’re working on, be sure to connect with the Codecademy community in the [forums](https://discuss.codecademy.com/). Remember to check in with the community regularly, including for things like asking for code reviews on your project work and providing code reviews to others in the [projects category](https://discuss.codecademy.com/c/project/1833), which can help to reinforce what you’ve learned.

# Binary Numbering System

As the old joke goes:

> There are only `10` types of people in the world, those that understand binary and those who don't.

By the time this lesson is over, you'll be able to count yourself amongst the ones that do. 

To get started, binary information is defined as *relating to*, *composed of*, or *involving two things*.

What we, as computer scientists, understand as examples of binary can be broken into two distinct categories:

1. Binary Numbers
2. Binary Data

Binary numbers are expressed as a combination of `0`s and `1`s. For example, `100110` is the binary equivalent of the number `38`.

Common examples of binary data include:

- [Machine Code](https://www.codecademy.com/resources/docs/general/machine-code) (`001010101100111001010010011`)
- [Boolean](https://www.codecademy.com/resources/docs/general/data-types/boolean) Expressions (`True` or `False`)
- Hardware states (`On` or `Off`)
- Networking and File Storage

Before we start getting too far into how we use the data though, let's take some time to really understand what binary data and the binary number system are.

## Computers and Binary

You may find yourself asking why we go through all the bother of `binary` numbers when the decimal system has worked so well for humans for so long.

Unfortunately, computers only understand two states of being, off and on, represented by the bits `0` and `1` respectively. Computer hardware would be incredibly large, expensive, and resource-intensive if they were made to handle ten different states of data.

Binary data, when not run through hardware, is seen as power applied or power not applied. An incredible level of precision and regulation would have to be built into the hardware to modify the applied electrical voltage so minutely as to fluctuate between ten levels of power. 

Binary data also typically comes in specific lengths, for example, eight bits is called a *Byte* and two Bytes (16 bits) is called a *Word*. When the incoming data follows these guidelines, it is easy for the hardware to process and computer the desired results.

One common place you might see this is internet speed, which is typically expressed in **kilobits** or **Megabits** per second (kb/s or Mb/s).

## Binary Numbering System

Numbers have been represented in a variety of different methods throughout history. For example, if you look at the face of some clocks, you may see that six o'clock is designated by `VI`, the Roman Numeral for `6`. 

The most successful system of numbering is called the **decimal system**, from the Latin root **dec-** meaning *set of ten or having a base of ten*.

Although the exact origins of this system are unknown, it is clear that it began with counting on our fingers and later evolved into substituting the Hindu-Arab characters of `0, 1, 2, 3, 4, 5, 6, 7, 8, 9` for fingers in order to perform larger operations.

In the decimal system, each digit can be represented by a multiple of a power of ten and added together with the other digits. Let's look at the number `305`.

| 100  | 10   | 1    |
| ---- | ---- | ---- |
| 10^2 | 10^1 | 10^0 |
| 3    | 0    | 5    |
Starting at the right and moving left, the first column is the ones digit. The digit in this place value is `5`.

**5 times 10^0** = `5`

the next digit, the ten's column, is `0`.

**0 times 10^1** = `0`

Finally, the `3` is in the hundred's column:

**3 times 10^2** - `300`

By adding each column together, we get our total value:

```
5 + 0 + 300 = 305
```

The binary system is very similar to the decimal system except it uses a base of two and only two digits, `0` and `1`. With the provided table we can use the same technique to evaluate `100110001`, which is `305` in binary. Try it out.

| MSB |     |     |     |     |     |     |     | LSB |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 256 | 128 | 64  | 32  | 16  | 8   | 4   | 2   | 1   |
| 2^8 | 2^7 | 2^6 | 2^5 | 2^4 | 2^3 | 2^2 | 2^1 | 2^0 |
| 1   | 0   | 0   | 1   | 1   | 0   | 0   | 0   | 1   |
In binary, the digit that is farthest to the right is called the *Least Significant Bit (LSB)* and the left-most digit is called the *Most Significant Bit*

## Counting in Binary

Let's reinforce what we learned in the previous exercise by practicing our counting to eight in binary. Eight may seem like a random number to stop at, but check out the table below and try to pick up the pattern of the counting.

| Decimal | Binary |
| ------- | ------ |
| 0       | 0      |
| 1       | 1      |
| 2       | 10     |
| 3       | 11     |
| 4       | 100    |
| 5       | 101    |
| 6       | 110    |
| 7       | 111    |
| 8       | 1000   |
Each time we reach a power of two we have to add another digit. For example, when we reach the number `2` or 2^1, the binary values goes from `1` to `10`. 

Similarly, when reach decimal `4` (2^2), in binary we go from `11` to `100`. This pattern continues for all the powers of 2 (0, 2, 4, 8, 16, 32, 64, 128, etc.)

> In fact, this brings us to our first trick to figuring out a number in binary. The highest a binary number can be is **2^n - 1** where `n` is the number of digits in the binary number.

`011010001010` is 12 digits long, therefore, the highest number that can be represented in binary with these digits is `4095`.

2^12 - 1 = 4095

If we changed all the digits of our 12-digit binary number to `1`s, we get `4095` in decimal.

```
11111111111 = 4095
```

Our next trick you may have picked up yourself. You will notice that all odd numbers in binary end in `1` and all even numbers in `0`. This is a quick way to double-check your work.

## Binary to Decimal Conversion

The ability to know the max size of a binary number allows us to check our work when we go to find the actual value of a binary number. 

A five-digit binary number can never be more than `31`, or 2^5-1 because `11111` is equal to `31`.

To help keep our workspaces clear and concise, it is common practice to add subscripts to numbers when working multiple numbering systems in the same space.

`11111` and `31` from above should be represented as `11111^2` and `31^10` representing their bases for clarity. If no subscript is used, it is assumed to be a decimal number.

To convert from a binary to a decimal number, make a table like the one below. For every bit that contains a `1`, add that decimal number to the total. Let's look at the 8-bit number `11001110^2`.

| MSB |     |     |     |     |     |     | LSB |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 128 | 64  | 32  | 16  | 8   | 4   | 2   | 1   |
| 2^7 | 2^6 | 2^5 | 2^4 | 2^3 | 2^2 | 2^1 | 2^0 |
> Adding the decimal values of all the `1`s highlighted in yellow gives us: (128) + (64) + (8) + (4) + (2) = 206^10.

## Decimal to Binary Conversion

Converting from binary to decimal can get tedious, especially as our binary data grows in length. Lucky for us, converting from decimal to binary is very straighforward.

The method we will use only requires us to divide by `2`, hence its name *Division-by-2* method.

Whenever we divide a number we always have two answers:

- the *result* (also known as *quotient*)
- the *remainder*

If our remainder is `0`, we normally don't want to include it when we give the answer but it is still there.

- `35 / 7 = 5 remainder 0`
- `36 / 7 = 5 remainder 1`

When we divide by `2` we will always end up with a remainder that is either a `1` or a `0`, in other words, binary digits.

The Divide-by-2 method will continue dividing number by two until the result, the first part of the answer, is `0`. The first time we divide, the remainder goes in the LSB column. Each time we divide after that, the remainder is written as the next digit to the left. 

We can use our even/odd trick we learned to check if we've got the right digit in the LSB. Odds will always be `1`s and events will be `0`'s. 

Follow along with the conversion of 27^10 to binary.

|Dividend10|Divisor10|Result10|Remainder10|Cumulative Binary2|
|---|---|---|---|---|
|27 (odd)|2|13|1 -> LSB|1|
|13 (odd)|2|6|1|11|
|6 (even)|2|3|0|011|
|3 (odd)|2|1|1|1011|
|1 (odd)|2|**0**|1 -> MSB|11011|
## Adding Binary Numbers

Adding binary numbers can be done in much the same way as we add base 10 numbers, with a couple of caveats.

Let's start at `0^10` and add until we reach `4^10`. 

|Decimal|Binary|
|---|---|
|0 + 1 = 1|0 + 1 = 1|
|1 + 1 = 2|1 + 1 = 10|
|2 + 1 = 3|10 + 1 = 11|
|3 + 1 = 4|11 + 1 = 100|
We can see that when adding numbers we need to be very careful when carrying our numbers. This will happen much more frequently than we are used to with decimal numbers. Here are some important rules to remember when adding in binary:

- `1 + 0 = 1`
- `1 + 1 = 10`
- `1 + 1 + 1 = 11`

For larger numbers they can be lined up, one on top of the other, just like the regular addition you are used to. Take a look at the examples below, you can see how often you need to carry in binary addition.

| Binary | Decimal |
| ------ | ------- |
|        |         |
| 100    | 4       |
| + 1    | + 1     |
|        |         |
| 101    | 5       |

> E.g. Adding `101101`^2 and `111`^2

| Binary | Decimal |
| ------ | ------- |
| 1111   | 1       |
| 101101 | 45      |
| +111   | +7      |
| 110100 | 52      |


