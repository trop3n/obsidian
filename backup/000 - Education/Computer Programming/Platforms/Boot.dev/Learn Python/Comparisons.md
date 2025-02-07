
# Comparison Operators

When coding it's necessary to be able to compare two values. `Boolean Logic` is the name for these kinds of comparison operations that always result in `True or False`.

The operators:

- `<` less than
- `>` greater than
- `<=` less than or equal to
- `>=` greater than or equal to
- `==` equal to
- `!=` not equal to

For example:

```python
5 < 6 # True
5 > 6 # False
5 >= 6 # False
5 <= 6 # True
5 == 6 # True
5 != 6 # True
```
# Comparison Operator Evaluations

When a comparison operator happens, the result of the comparison is just a boolean value, it's either `True` or `False`.

Take the following two examples:

```python
is_bigger = 5 > 4

is_bigger = true
```

In both of the above cases, we're creating a `Boolean` variable called `is_bigger` with a value of `True`.

Because `5` is bigger than `4`, `is_bigger` is assigned the value of `True`.
# Comparison Practice

```python
car_size = 4
truck_size = 5
is_smaller = car_size < truck_size
# is_smaller is True 
```
# If Statements

It' s often useful to only execute code if a certain condition is met:

```python
if CONDITION
	# do some stuff here

# code after the if block will run regardless
```

For example, this code:

```python
if bob_score > bill_score:
	print("Bob Wins!")

print("Game Complete")
```

If `bob_score` is greater than `bill_score`, then this will be printed:

```
Bob Wins!
Game Complete
```

Otherwise, this will be printed:

```
Game Complete
```
# If-Else

An `if` statement can be followed by zero or more `elif` (which stands for else if) statements, which can be followed by zero or one `else` statements. 

For example:

```python
if score > high_score:
	print("High Score Beat!")
elif score > second_highest_score:
	print("You go second place!")
elif score > third_highest_score:
	print("You got third place")
else:
	print("Better luck next time")
```

First the `if` statement is evaluated. If it is `True` then the if statement's body is executed and all the other `else`s are ignored.

If the first `if` is false then the next `elif` is evaluated. Likewise, if it is `True` then its body is executed and the rest are ignored.

If none of the `if` statements evaluate to `True` then the final `else` statement will be the only body executed.
# If-Else Practice

Here are some basic rules with if/else blocks.

- You can't have an `elif` or an `else` without an `if`
- You _can_ have an `else` without an `elif`

Remember, to check if two values are the same use the `==` operator.

```python
same = 5 == 6
# same is False

same = 6 == 6
# same is True
```

Here are some basic rules with if/else blocks.

- You can't have an `elif` or an `else` without an `if`
- You _can_ have an `else` without an `elif`
## Assignment

Complete the `check_high_score` function. If the `player_name` matches the high score name, `return` the string:

```
high
```

Otherwise, if it's the low scorer, `return` the string:

```
low
```

Otherwise, `return` the string:

```
neither
```
# Boolean Logic

Boolean logic refers to logic dealing with boolean (`True` or `False`) values. For example, dogs must have four legs *and* weigh less than 100 kilograms. (Both conditions must be true).

Cars are cool if they go faster than 200 mph, *or* if they are electric. (At least one condition must be true).
## Logical Operators Review

As we discussed earlier, the logical operators `and` and `or` can be used to perform boolean logic. 
### And Review

The `and` operator returns `True` if *both* of the conditions on either side evaluates to `True`.

```python
def is_dog(num_legs, weight):
	return num_legs == 4 and weight < 100
```

Let's go over how this function evaluates the parameters `num_legs=4` and `weight= 99`:

```python
return 4 == 4 and 99 < 100

return True and True

return True
```

Let's see what would happen with `3` and `98` instead:

```python
return 3 == 4 and 98 < 100

return False and True

return False
```
### Or Review

The `or` operator returns `True` if *at least one* of the conditions on either side evaluates to `True`:

```python
def is_car_cool(speed, is_electric):
	return speed > 200 or is_electric
```

Let's use a non-electric car that can do 250:

```python
return 250 > 200 or False

return True or False

return True
```
