
# Loops

Loops are a programmer's best friend. Loops allow us to do the same operation multiple times without having to write it explicitly each time. For example, let's pretend I want to print the number 0-9.

I could do this:

```python
print(0)
print(1)
print(2)
print(3)
print(4)
print(5)
print(6)
print(7)
print(8)
print(9)
```

Even so, it would save me a lot of time typing to use a *loop*. Especially if I wanted to do the same thing *one thousand or one million times*.

A **for loop** in Python is written like this:

```python
for i in range(0, 10):
	print(i)
```

`i` replaces the numbers `0 - 9`. In English, the code says:

1. Start with `i` equals `0` (`i in range(0)`)
2. If `i` is not less than 10, (`range(0, 10`), exit the loop. Else:
	1. Print `i` to the console.
	2. Add `1` to `i` (`range` defaults to incrementing by 1).
	3. Go back to step 2.

The result is that the numbers `0-9` are logged to the console in order.

The body of a for-loop _must_ be indented, otherwise you'll get a syntax error.
# Loops Practice

As a reminder, a "for loop" in Python is written like this:

```python
for i in range(0, 10):
	print(i)
```

In English, the code says:

1. Start with `i` equals `0`. (`i in range(0`)
2. If `i` is greater than or equal to 10 (`range(0, 10)`), exit the loop.
3. Print `i` to the console. (`print(i)`)
4. Add `1` to `i`. (`range` defaults to incrementing by 1)
5. Go back to step `2`

The result is that the numbers `0-9` are logged to the console in order.
# Range Continued

The `range()` function we've been using in our `for` loops actually has a third optional parameter: the **step**.

```python
for i in range(0, 10, 2):
	print(i)
# prints:
# 0
# 2
# 4
# 6
# 8
```

The **step** parameter determines how much to add to `i` in each iteration of the loop. You can even go backwards:

```python
for i in range(3, 0, -1):
	print(i)
# prints:
# 3
# 2
# 1
```
# Sum Game

Remember you can use in-place operators to increase or decrease a variable by any amount.

```python
number_of_enemies = 10
number_of_enemies += 2
# number_of_enemies is 12

number_of_enemies = 10
number_of_enemies -= 2
# number_of_enemies is 8
```
# While

Python has another type of loop, the `while` loop. It's a loop that continues `while` a condition remains `True`. The syntax is simple:

```python
while 1:
	print("1 evaluates to True")

# prints:
# 1 evaluates to True
# 1 evaluates to True
# continuing ...
```

The example above is hardcoded to continue forever, creating an *infinite loop*. Typically, a `while` loop condition is a comparison or variable, and it determines when the loop ends:

```python
num = 0
while num < 3:
	num += 1
	print(num)
	
# prints:
# 1
# 2
# 3
# (the loop stops when num >= 3)
```




