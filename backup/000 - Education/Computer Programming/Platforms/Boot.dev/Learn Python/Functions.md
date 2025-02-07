---
up: "[[Python Numbers]]"
tags:
  - "#education/computerprogramming/platforms/bootdev/python/functions"
prev: "[[Scope]]"
---

# Functions

Let's break down this function line by line so we can understand all of it effectively.

```python
def area_of_circle(r):
	pi = 3.14
	result = pi * r * r
	return result

radius = 5
area = area_of_circle(radius)
print(area)
```
```
> 78.5
```

Here's a chronological breakdown of what happens when the above code is executed:

1. `def area_of_circle(r)`:
	- The `area_of_circle` function is *defined* for later use, but *not called*. It accepts a single input named `r`. The body of the function (`pi = 3.14`) is ignored for now.

2. `radius = 5`:
	- A new variable called `radius` is created and set to the value `5`.

3. `area_of_circle(radius)`:
	- The `area_of_circle` function is called with `radius` (in this case 5) as the input. Finally, we jump back to the function definition.

4. `def area_of_circle(r):`
	- We will now start executing the body of the function, and `r` is set to `5`.

5. `pi = 3.14`
	- A new variable called `pi` is created with a value of `3.14`.

6. `result = pi * r * r`:
	- Some simple math is evaluated (`3.14 * 5 * 5`) and stored in the `result` variable.

7. `return result`:
	- The result variable is returned from the function as output.

8. `area = area_of_circle(radius)`:
	- The returned value is stored in a new variable called `area` (in this case `78.5`).

9. `print(area)`:
	- The value of `area` is printed to the console.
# Multiple Parameter Functions

Functions can have multiple parameters ("parameters" being a fancy word for "input"). For example, this `subtract` function accepts 2 parameters: `a` and `b`.

```python
def subtract(a, b):
	result = a - b
	return result
```

The name of a parameter doesn't matter when it comes to which values will be assigned to which parameter. It's **position** that matters. The first parameter will become the first value that's passed in, the second parameter is the second value that's passed in, and so on. In this example, the `subtract` function is called with `a = 5` and `b = 3`.

```python
result = subtract(5, 3)
print(result)
# 2
```

Here's an example with four parameters:

```python
def create_introduction(name, age, height, weight):
	first_part = "Your name is " + name + " and you are " + age " years old."
	second_part = "You are " + height + " meters tall and weigh " + weight + " kilograms."
	full_intro = first_part + " " + second_part
	return full_intro
```

It can be called like this:

```python
my_name = "Jason"
my_age = "33"

intro = create_introduction(my_name, my_age, "1.8", "80")
print(intro)

# Your name is Jason and you are 33 years old. You are 1.8 meters tall and weight 80 kilograms.
```
# Printing vs. Returning

Some new developers get hung up on the difference between `print()` and `return`.

It can be particularly confusing when the test suite we provide simply prints the output of your functions to the console. It makes it *seem* like `print()` and `return` are interchangeable, *but they are not*.

- `print()` is a function that:
	1. Prints a value to the console
	2. Does *not* return a value

- `return` is a **keyword** that:
	1. Ends the current function's execution
	2. Provides a value (or values) back to the caller of the function
	3. Does *not* print anything to the console (unless the return value is later `print()`ed).
## Printing to Debug your Code

Printing values and running your code is a great way to debug your code. You can see what values are stored in various variables, find your mistakes, and fix them. Add print statements and run your code as you go! It's a great habit to get into to make sure that each line you write is doing what you expect it to do.

In the real world it's rare to leave `print()` statements in your code when you're done debugging. Similarly, you need to remember to remove any `print()` statements from your code before submitting your work here on Boot.dev because it will interfere with the tests.
# Where to Declare Functions

You've probably noticed that a variable needs to be declared *before* it's used. For example, the following doesn't work:

```python
print(my_name)
my_name = 'Jason Kimm'
```

It needs to be:

```python
my_name = 'Jason Kimm'
print(my_name)
```

Code executes in *order from top to bottom*, so a variable needs to be created before it can be used. That means that if you define a function, you can't call that function until *after* the definition.
# Order of Functions

All functions *must* be defined before they're used. You might think this would make structuring Python code hard because the order of the functions needs to be *just right*. As it turns out, there's a simple trick that makes it super easy.

Most Python developers solve this problem by defining *all* the functions in their program first, then they call an "entry point" function last. That way *all* of the functions have been read by the Python interpreter before the first one is called.

Note: *conventionally this "entry point" function is usually called `main` to keep things simple and consistent*.

```python
def main():
	health = 10
	armor = 5
	add_armor(health, armor)

def add_armor(h, a):
	new_health = h + a
	print_health(new_health)

def print_health(new_health):
	print(f"The player now has {new_health} health")

# call entrypoint last
main()
```
# Discord

Getting help is a _critical_ part of learning to code (and even in your day to day working as a developer). We've already talked about Boots and spellbooks, which are great first lines of defense. But what else can you do?

First, it's totally normal to look stuff up online as you work on Boot.dev. It's not cheating. It's impossible to memorize everything, and it's frankly just not necessary, even as a professional developer.

Second, sometimes you just need a human. Luckily, we have an amazing Discord community full of developers and fellow students ready to help you out. So,

1. Open our [Discord community](https://www.boot.dev/community) page
2. Join the server and sync your account
3. With your account linked up, you'll be able to chat with other learners and mentors, as well as use the `#help` forums to ask questions
4. Additionally, if _you_ help others in the Discord, you'll earn karma that will help you earn [fellowship achievements](https://www.boot.dev/lessons/0f4fa755-1ce7-468b-bf34-c1460e97bf28#)
# None Return

When no return value is specified in a function, it will automatically return `None`. For example, maybe it's a function that prints some text to the console, but doesn't explicitly return a value. The following code snippets all return the same value: `None`.

```python
def my_func():
	print("I do nothing")
	return None

def my_func():
	print("I do nothing")
	return

def my_func():
	print("I do nothing")
```
# Multiple Return Values

A function can return more than one value by separating them with commas.

```python
def cast_iceblast(wizard_level, start_mana):
	damage = wizard_level * 2
	new_mana = start_mana - 10
	return damage, new_mana # returns two values
```
## Receiving Multiple Values

When calling a function that returns multiple values, you can assign them to multiple variables.

```python
dmg, mana = cast_iceblast(5, 100)
print(f"Damage: {dmg}, Remaining Mana: {mana}")
# Damage: 10, Remaining Mana: 90
```

When `cast_iceblast` is called, it returns two values. The first value is assigned to `dmg`, and the second value is assigned to `mana`. Just like the function inputs, it's the *order of the values* that matters, not the variable names. We could just as easily called the variables `one` and `two`:

```python
one, two = cast_iceblast(5, 10)
print(f"Damage: {one}, Remaining Mana: {two}")
# Damage: 10, Remaining Mana: 90
```

That said, descriptive variable names make your code easy to understand, so use them.
## What Happened to the Variables?

The `damage` and `new_mana` variables from `cast_iceblast`'s function body only exist *inside* of the function. They can't be used outside of the function. We'll explain that more later when we talk about scope.
# Parameters vs. Arguments

Parameters are the names used for inputs when *defining* a function. Arguments are the values of the inputs **supplied to** the function when it is *called*.

To reiterate, **arguments are the actual names** that go into the function, such as `42.0`, `"the dark knight"`, or `True`. **Parameters are the names** we use in the function definition to refer to those values, which at the time of writing the function, can be whatever we like. 

That said, this is all semantics, and frankly developers are really lazy with these definitions. You'll often hear the words "arguments" and "parameters" used interchangeably. 

```python
# a and b are parameters
def add(a, b):
    return a + b

# 5 and 6 are arguments
sum = add(5, 6)
```
# Default Values

In Python you can specify a **default value** for a function argument. It's nice for when a function has arguments that are "optional". You as the function definer can specify a specific default value in case the caller doesn't provide one.

A default value is created by using the assignment (`=`) operator in the function signature.

```python
def get_greeting(email, name="there"):
	print("Hello", name, "welcome! You've registered your email:", email)

get_greeting("jason@example.com", "jason")
# Hello jason welcome! You've registered your email: jason@example.com

get_greeting("jason@example.com")
# Hello there welcome! You've registered your email: jason@example.com
```

If the second parameter is omitted, the default `"there"` value will be used in its place. As you may have guessed, for this structure to work, optional arguments (the ones with the defaults) must come *after* all required arguments.
# Archmage

You've probably already figured out that:

- Chests contain gems and items
- Gems can buy items in the [shop](https://www.boot.dev/lessons/4777c0b2-30fa-48fe-82bf-c9b84e74d92f#)
- Items help you earn [achievements](https://www.boot.dev/lessons/4777c0b2-30fa-48fe-82bf-c9b84e74d92f#) and XP
- XP levels you up, and higher levels unlock new roles

**So why should you care about your role?**

My _guess_ is that you've earned enough XP to be an `Apprentice` by now. You can see your role at the top right of your screen. When you hit level `100`, you'll **unlock the `Archmage` role**. _It's kind of a big deal_. When you hit archmage:

1. You'll have learned a _ton_, built many real-world projects, and should be starting your job search
2. You'll have unlocked all the private role-based chat channels in our [Discord](https://www.boot.dev/community)
3. You'll have immeasurable bragging rights and a hoard of fake internet points
4. **You'll get a physical archmage coin in the mail as a token of your hard work**






