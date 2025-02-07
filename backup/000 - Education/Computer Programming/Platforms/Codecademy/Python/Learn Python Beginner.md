#python #codecademy #beginner
# Python Automation Script Ideas:

> Email Scheduler
> Task Scheduler
> Data Backup Tool
> Web Scraping
> File Organizer/Desktop Organizer
> Facial Recognition Script Running on a Raspberry Pi
> Personal Finance App - Django Backend, React or Dart/Flutter Frontend

AskPython: [https://www.askpython.com/](https://www.askpython.com/) 

Python Docs: (Codecademy): [https://www.codecademy.com/resources/docs/python](https://www.codecademy.com/resources/docs/python)

Python Documentation: [https://docs.python.org/3/](https://docs.python.org/3/)

Python Cheatsheet [https://www.codecademy.com/resources/cheatsheets/language/python](https://www.codecademy.com/resources/cheatsheets/language/python)

# User Input

> often, you will want the user to enter information into a Python program. How is this done?

* While we output a variables value using `print(), we assign information to a variable using input()` 
* The **_input() _**function requires a prompt message, which will print out for the user before they enter the new information.
* **_Example: _**likes_snakes = input(“Do you like snakes? “)

> **_input() _**can be used for collecting all sorts of different information from a user, but once you have that information stored as a variable you can use it to simulate interaction.

**_Introduction to Control Flow_**

> The same way you may wake up and determine if it is a weekday, what the weather is, etc. Python operates in a similar flow chart manner.

> Your computer, just like you, goes through a very similar flow every time it executes code. A program will run (wake up) and start moving through it’s checklists, is this condition met, is that condition met, okay let’s execute this code and return that value.

> this is the **_control flow _**of your program. In Python, your script will execute from the top down, until there is nothing left to run. It is your job to include gateways, known as **_conditional statements, _**to tell the computer when it should execute certain blocks of code. If these conditions are met, run this function.

**_Boolean Expressions_**

> In order to build control flow in our program, we want to be able to check if something is true or not. A **_boolean expression is a statement that can either be True or False. _**

**> _relational operators _**compare two items and return either **true **or **false. **For this reason, you will sometimes hear them called comparators.

**_Boolean Variables _**

> **True and False **are the only **bool **types, and any variable that is assigned one of these values is caled a **_boolean variable. _**

> **_Boolean variables _**can be created in a variety of ways, but the fastest and easiest way is to simply assign True or False to a variable. 

* You can also set a variable equal to a boolean expression
* Variables set as boolean expressions now contain boolean values, so when you reference them they will only return the true or false values of the expression they were assigned. 

**_If Statements_**

> Understanding boolean variables and expressions is essential because they are the building blocks of conditional statements. 

> a “:” or colon is used at the end of a conditional statement which tells the computer that what’s coming next is what should be executed if the condition is met. 

**_Relational Operators_**

> So far we know two relational operators, equals and not equals, but there are a ton (well, four) more:

* “>” greater than
* “>=” greater than or equal to 
* “&lt;” less than
* “&lt;=” less than or to equal 

**_Boolean Operators: and_**

> Often, the conditions you want to check in your conditional statement will require more than one boolean expression to cover. In these cases, you can build larger boolean expressions using **_boolean operators. _**These operators (aka logical operators) combine smaller boolean expressions into larger boolean expressions. 

> These are the boolean operators that we will cover

* And
* Or
* Not

> **_And _**combines two boolean expressions and evaluates as **_true _**if both its components are **_true, _**but **_false _** otherwise.

> _ _The boolean operator **_or _**combines two expressions into a larger expression that is **_true _**if either component is **_true_**

> Once you start including lots of if statements in a function the code becomes a little cluttered and clunky

* Luckily, there are other tools we can use to build control flow

> **_Else _**statements allow us to elegantly describe what we want our code to do when certain conditions are not met.

> We have **_if _** statements and we have **_else _**statements, we can also have **_elif _**statements

> an **_elif _**statement is exactly what it sounds like, “else if”. An **_elif _**statement checks another condition after the previous **_if _**statements conditions aren’t met. 

> **_elif _**statements can be used to control the order we want our program to check each of our conditional statements. First, the **_if _**statement is checked, then each **_elif _**statement is checked from top to bottom, then finally the **_else _**code is executed if none of the previous conditions have been met. 

**_Review of Control Flow_**

* Boolean expressions are statements that can be either **_true _**or **_false_**
* A boolean variable is a variable that is set to either **_true _**or **_false_**
* We can create boolean expressions using relational operators
    * ==: Equals
    * !=: Not equals
    * >: greater than
    * >=: greater than or equal to
    * &lt;: less than
    * &lt;=: less than or equal to
* **_If _**statements can be used to create control flow in your code.
* **_Else _**statements can be used to execute code when the conditions of an **_if _**statement are not met.
* **_Elif _**statements can be used to build additional checks into your **_if _**statements

**_Nested If / Else Statements_**

* An additional **_if / else _**statement can be nested inside a different **_if / else _**statement

**if condition:

		> if another condition:

			> do this

		> else: 

			> do this

	> else: 

		>do this

**_Conditional Operators_**

> if condition:

	Do this

> else:

	Do this

water _level = 50

If water_level > 80:

   print(“drain water”)

Else:

   print(“Continue filling bathtub”)

> Indentation is very important when writing else/if statements.

> one equals sign (=) means you’re assigning a value to a variable

> two equals signs (==) means that you are checking that the value on the left of the == is the same as the value on the right.

**_Mathematical Equations in Python_**

> mathematical equations follow normal mathematical order of operations (PEMDAS)

> Python is optimized to deal with numbers, which is why it is loved by data scientists

> PEMDAS priority list

* ()
* ** (exponent)
* * (multiplication) and  / (division), the first expression in the equation is what will be solved first
* + and -

> **_round _**function will round the output of an expression with a float to a specified decimal point

**_Introduction to Lists_**

> In Python, lists are ordered collections of items that allow for easy use of a set of data.

* List values are placed between square brackets [], separated by commas. It is good practice to put a space between the comma and the next value. The values in a list do not need to be unique (the same value can be repeated).
* **_Empty Lists _**do not contain any values within the square brackets.

**_Adding Lists Together_**

> In Python, lists can be added to each other using the plus + symbol. This will result in a new list containing the same items in the same order with the first list’s items coming first.

* Note: this will not work for adding one item at a time. 

**_Python Lists: Data Types_**

In Python, lists are versatile data type that can contain multiple different data types within the same square brackets. The possible data types within a list include numbers, string, other objects, and even other lists. 

**_List Methods_**

> In Python, you can add values to the end of a list using the **_.append() _**method. THis will place the object passed in as a new element at the very end of the list. Printing the list afterwards will visually show the appended value. This **_.append() _**method is not to be confused with returning an entirely new list with the passed object.



* A **_method _**in Python is the built-in functionality that we can use to create, manipulate, and even delete our data.
* For lists, **_methods _**will follow the form of **_list_name.method. _**Some methods will require an input value that will go between the parenthesis of the method. 
    * **_.append is a _**method that allows us to add an element to the end of a list.
    * If we want to add multiple items to a list, we can use + to combine two lists using **_concantenation._**

**_Accessing List Elements_**



* Python lists are **_zero-indexed. _**This means that the first element in a list has index 0, rather than 1. 
* When accessing elements of a list, you must use and **_int _** as the index. If you use a **_float, _**you will get an error. This can be especially tricky when using division. 
    * TO solve this problem, you can force the result of your division to be an **_int _**by using the **_int() function. int() _**takes a number and cuts off the decimal point. 

> **_Negative Index_** - We can use index -1 to select the last item of a list, even when we don’t know how many elements are in a list. 

**_Modifying List Elements_**

**_Shrinking a List: Remove_**

> We can remove elements in a list using the **_.remove() _**Python function.

**_Two-Dimensional (2D) Lists _**

> Items in a list can be numbers or strings, but lists can store other lists. These are called **_two-dimensional lists._**

**_Working With Lists In Python_**

> Lists are a simple example of a **_Data Structure_**

> In this lesson, we will learn to:



* Add and remove items from a list using a specific index
* Create lists with continuous values
* Get the length of a list
* Select portions of a list (slicing)
* Count the number of times that an element appears in a list
* Sort a list of items

**_Python List Methods_**

* **_.count()_** - A list method to count the number of occurrences of an element in a list
* **_.insert()_** - A list method to insert an element into a specific index of a list
* **_.pop()_** - A list method to remove an element from a specific index or from the end of a list
* **_range()_** - A built in Python function to create a sequence of integers.
* **_len()_** - A built in Python function to get the length of a list.
* **_.sort() / sorted()_** - A method and a built-in function to sort a list. 
1. The order and number of the inputs is important. The **_.insert()_** method expects two inputs, the first being a numerical index, followed by any value as the second input.
2. When we insert an element into a list, all elements from the specified index and up to the last index are shifted one index to the right. This does not apply to inserting an element to the very end of a list as it will simply add an additional index and no other elements will need to shift. 

> The **_.pop() _**method takes an optional single input:

1. The index for the element you want to remove. 

> There are two things to know about the **_.pop() _**method.

1. The method can be called without a specific index. Using **_.pop() _**without an index will remove whatever the last element of the list is. 
2. **_.pop() _** is unique in that it quill return the value that was removed. If we wanted to know what element was deleted, simply assign a variable to the call of the **_.pop() _** method.

**_Modules_**

> Python code can be split up into different modules for large projects

* Multiple people can work on different modules

> your own module can be created by making a new file within the project directory, then using the **_import _**function to import it into a main or different .py file.

**_Loops_**

> For Loop:

	> for item in list_of_items:

		#Do something to each item

> executes the same line of code multiple times

**_Defining and Calling Python Functions_**

> a **_Python function _**is denoted by a word (print) followed by a set of parenthesis (). For example, **_print() _**is an early function that is learned in Python

> to create your own Python function:

* Start with **_“def”_**
* Add “my_function():”
* Add the content of the function, or the process it is performing

> def my_function():

	> #Do this

	> #Do this

	> # Finally, do this

1. Define the function using **_def _**then name the function e.g. (my_function)
2. Use the function, or more technically, **_call the function._**

> functions allow the programmer to refer to instructions or code at the same time

**_Indentation in Python:_**

> Indentations are used to include functions inside other functions. See: if and elif and else statements

> Functions indented all the way to the left of the code editor will run as separate functions

> Python officially recommends using spaces instead of tabs when coding in Python.

> You need four spaces for an indent in Python 3.

**_While Loops_**

> difference between **for loops and while loops**

* For loops do something to each item
* While loops do something repeatedly

> while `something_is_true`:

> for loops are better for when you need to do something for each thing in a function or code block

### Introduction to Strings

> Strings can be thought of as a *list* of characters
> Like any other lists, each character in a string has an index. Consider the string:

`favorite_fruit = blueberry`

We can select specific letters of this string using the index. 

`string[first_index:last_index]` - this is called *slicing* a string. When we slice a string we are creating a **substring** -- a brand new string that starts at (and includes) the `first_index` and ends at (but excludes) the `last_index`. 

Let's say we have the variable `favorite_fruit = blueberry`

If we wanted a new string that just contains the letters `be`, we could slice `favorite_fruit` as follows. 

```
print(favorite_fruit[4:6])
# Output: be
```
> the word `blueberry`, if the 4th and 6th indexes are selected, removes every other index outside of the selected ones.

We can also have open ended selections. If we remove the first index, the slice starts at the beginning of the string and if we remove the second index the slice continues to the end of the string.

```python
print(favorite_fruit[:4])
# Output: blue

print(favorite_fruit[4:])
# Output: berry
```

### Concatenating Strings

> We can also combine, or **concatenate**, two existing strings together into a new string.

```python
fruit_prefix = "blue"
fruit_suffix = "berries"
```

We can create a new string by concatenating them together as follows:

```python
favorite_fruit = fruit_prefix + fruit_suffix

print(favorite_fruit)
# Output: Blueberries
```

Notice that there are no spaces added here. We have to manually add in the spaces when concatenating strings if we want to include them.

```python
fruit_sentence = "My favorite fruit is" + favorite_fruit

print(fruit_sentence)

fruit_sentence = "My favorite fruit is " + favorite_fruit

print(fruit_sentence)

Output: My favorite fruit is blueberries
```

### More and More Slicing

> Python comes with some built-in functions for working with strings. One of the most commonly used of these functions is `len()`. `len()` returns the number of characters in a string:

```
favorite_fruit = "blueberry"

length = len(favorite_fruit)

print(length)
# Output: 9
```

> If you are taking the length of a sentence, the spaces are counted as well.

> `len()` comes in handy when we are trying to select characters from the end of a string. What is the index of the last character, `"y"`, of `favorite_fruit` above?

Using a `len()` statement as the starting index and omitting the final index lets you slice `n` characters from the end of a string, where `n` is the amount you subtract from `len()`.

### Negative Indices

We recently used `len()` to get a slice of characters at the end of the string.

The easier way to do this is to use **negative indices**.

Negative indices count backwards from the end of the string, so `string_name[-1]` is the last character of the string, and `string_name[-2]` is the second to last character of the string, etc.

```python
favorite_fruit = 'blueberry'
print(favorite_fruit[-1])
#output = 'y'

print(favorite_fruit[-2])
#output = 'r'

print(favorite_fruit[-3:])
#output = 'rry'
```

### Strings are Immutable

In this lesson, we've been selecting characters from strings, slicing strings, and concatenating strings. Each time we perform one of these operations we are creating an entirely new string.

This is because strings are *immutable*. This means we cannot change a string once it is created. We can use it to create other strings, but we cannot change the string itself.

This property, generally, is known as *mutability*. Data types that are *mutable* can be changed, and data types, like strings, that are *immutable* cannot be changed.

### Iterating Through Strings

Now you know enough about strings that we can start doing the really fun stuff. 

Because strings are lists, that means we can iterate through a string using `for` and `while` loops. This opens up a whole range of possibilities of ways we can manipulate and analyze strings. Let's take a look at an example:

```python
def print_each_letter(word):
  for letter in word:
    print(letter)
```
> This code will iterate through each letter in a given word and will print it to the terminal.
```python
favorite_color = "blue"
print_each_letter(favorite_color)

output:

'b'
'l
'u
'e'
```

### Strings and Conditionals (Part One)

> Now that we are iterating through strings, we can really explore the potential of strings.
> 	When we iterate through a string we do *something* with each character. By including conditional statements inside of these iterations, we can start to do some really cool stuff. 

Look at the following code:

```python
favorite_fruit = "blueberry"
counter = 0
for character in favorite_fruit:  
  if character == "b":    
    counter = counter + 1
print(counter)
```
> This code will break down the number of `b`'s in the string "blueberry".

Let's take a moment to look at what the code is doing:

First, we define our string, `favorite_fruit`, and  a variable called `counter`, which we set equal to zero. Then the `for` loop will iterate through each character in the `favorite_fruit` and compare it to the letter `b`. 

Each time a character equals `b` the code will increase the variable `counter` by one. Then, once all characters have been checked, the code will print the counter, telling us how many `b`'s were in "Blueberry". 

- This is a great example of how iterating through a string can be used to solve a specific application, in this case counting a certain letter in a word.

### Strings and Conditionals (Part 2)

> There's an even easier way than iterating through the entire string to determine if a character is in a string. We can do this type of check more efficiently using `in`. `in` checks if one string is part of another string. 

Here is what the syntax of `in` looks like:

```python
letter in word
```

> Here, `letter in word` is a boolean expression that is `True` if the string `letter` is in the string `word`. 

```python
print("blue" in "blueberry")
# => True
print("blue" in "strawberry")
# => False
```

> In fact, this method above is more powerful than the function we wrote previously because it not only works with letters, but with entire *strings* as well.

```python
print("e" in "blueberry" and "e" in "carrot")
# => False
print("e" in "blueberry" and not "e" in "carrot")
# => True
```

> The first example above is `false` because ONE of the expressions was `False`; there is not "e" in "carrot". The second example is `True` because there is an "e" in "blueberry" and not an "e" in "carrot"; both expressions are `True`.

### Review

In this lesson we learned:

- A string is a list of characters
- A character can be selected from a string using its index `string_name[index]`
- A 'slice' can be selected from a string. These can be between two indices or can be open-ended, selecting all of the string from a point.
- Strings can be concatenated to make larger strings.
- `len()` can be used to determine the number of characters in a string
- Strings can be iterated through using `for` loops.
- Iterating through strings opens up a huge potential for applications, especially combined with conditional statements

# String Methods

### Formatting Methods

There are three string methods that can change the casing of a string. 

- `.lower()` returns the string with all lowercase letters
- `.upper()` returns the string with all uppercase letters
- `.title()` returns the string in title case, which means the first letter of each word is capitalized.

```python
favorite_song = 'SmOoTH'
favorite_song_lowercase = favorite_song.lower()
print(favorite_song_lowercase)
# => 'smooth'
```
> Every character was changed to lowercase

*String methods can only create new strings, not modify existing ones.*

### Splitting Strings

> `.upper()`, `.lower()` and `.title()` all are performed on an existing string and produce a string in return. Let's take a look at a string method that returns a different object entirely.

`.split()` is performed on a string, takes one argument, and returns a list of *substrings* found between the given argument (which in the case of `.split()` is known as the delimiter)

- The following syntax should be used:
```python
string_name.split(delimiter)
```

If you do not provide an argument for `.split()` it will default to splitting at spaces.

```python
man_its_a_hot_one = "Like seven inches from the midday sun"
print(man_its_a_hot_one.split())
# => ['Like', 'seven', 'inches', 'from', 'the', 'midday', 'sun']
```
> `.split()` returned a list with each word in the string. Important to note: if we run `.split()` on a string with no spaces, we will get a single element array containing the same string.

### Splitting Strings II

> If we provide an argument for `.split()`, we can dictate the character we want our string to be split on. This argument should be provided as a string itself.

```python
greatest_guitarist = "santana"
print(greatest_guitarist.split('n'))
# => ['sa', 'ta', 'a']
```

> "`n`" was provided as the argument for `.split()` so our string "santana" got split at each "`n`" character in a list of three strings.

```python
greatest_guitarist = "santana"
print(greatest_guitarist.split('a'))

# => ['s', 'nt', 'n', '']
```

> Notice that there is an extra `''` string in this list.
> 	When you split a string on a character that it also ends with, you'll end up with an empty string at the end of the list.

*You can use ANY string as the argument for .split(), making it a versatile and powerful tool.*

### Splitting Strings III

> We can also split strings using *escape sequences*. **Escape sequences** are used to indicate that we want to split by something in a string that is not necessarily a character. 

The two escape sequences we will cover here are:

- `\n` Newline
- `\t` Horizontal tab

Newline or `\n` will allow us to split a multi-line string by line breaks and `\t` will allow us to split a string by tabs. `\t` is particularly useful when dealing with certain datasets because it is not uncommon for data points to be separated by tabs. 

Let's take a look at an example of splitting by an escape sequence:

```python
smooth_chorus = \
"""And if you said, "This life ain't good enough."
I would give my world to lift you upI could change my life to better suit your mood
Because you're so smooth"""
chorus_lines = smooth_chorus.split('\n')

print(chorus_lines)
```

> This code is splitting up the multi-line string at the newlines (`\n`) which exists at teh end of each line and saving it to a new list called `chorus_lines`. 

- This prints `chorus_lines` which will produce the output:

```python
['And if you said, "This life ain\'t good enough."', 'I would give my world to lift you up', 'I could change my life to better suit your mood', "Because you're so smooth"]
```

### Joining Strings

> Now that we've learned to break strings apart using `.split()`, let's learn to put them back together using `.join()`. `.join()` is essentially the opposite of `.split()`, it *joins* a list of strings together with a given delimiter. The syntax of `.join()` is:

```python
'delimiter'.join(list_you_want_to_join)
```

This may seem a little weird, because with `.split()` the argument was the delimiter, but now the argument is the list. This is because `join` is still a string method, which means it has to act on a string. The string `.join()` acts on is the delimiter you want to join with, therefore the list you want to join has to be the argument. 

This can be confusing so let's look at an example:

```python
my_munequita = ['My', 'Spanish', 'Harlem', 'Mona', 'Lisa']
print(' '.join(my_munequita))

#output = 'My Spanish Harlem Mona Lisa'
```

> The list of strings, `my_munequita`, is joined with a delimiter, `' '`, which is a space. 
> 	The space is important, because without it the output would be the same, but with no spaces between the words in the string.

### Joining Strings II

> You can use any string as a delimiter to join together a list of strings. 

For example:

```python
santana_songs = ['Oye Como Va', 'Smooth', 'Black Magic Woman', 'Samba Pa Ti', 'Maria Maria']
```

We can join this list together with ANY string. One often used string is a comma, `,`, because we can create a string of *comma-separated values*, or a *CSV* file.

```python
santana_songs_csv = ','.join(santana_songs)
print(santana_songs_csv)
# => 'Oye Como Va,Smooth,Black Magic Woman,Samba Pa Ti,Maria Maria'
```

You'll often find data stored in .CSV files because it is an efficient, simple file type used by popular programs like Excel or Google Spreadsheets.

> You can also join using *escape sequences* as the delimiter:

```python
smooth_fifth_verse_lines = ['Well I\'m from the barrio', 'You hear my rhythm on your radio', 'You feel the turning of the world so soft and slow', 'Turning you \'round and \'round']

smooth_fifth_verse = '\n'.join(smooth_fifth_verse_lines)

print(smooth_fifth_verse)
```
> The code is taking the list of strings and joining them using a `\n` as the delimiter. Then it prints the result and produces the output:
```python
Well I'm from the barrio
You hear my rhythm on your radio
You feel the turning of the world so soft and slow
Turning you 'round and 'round
```

##### Challenge

```python
winter_trees_lines = ['All the complicated details', 'of the attiring and', 'the disattiring are completed!', 'A liquid moon', 'moves gently among', 'the long branches.', 'Thus having prepared their buds', 'against a sure winter', 'the wise trees', 'stand sleeping in the cold.']
```

##### Solution

```python
winter_trees_lines = ['All the complicated details', 'of the attiring and', 'the disattiring are completed!', 'A liquid moon', 'moves gently among', 'the long branches.', 'Thus having prepared their buds', 'against a sure winter', 'the wise trees', 'stand sleeping in the cold.']

winter_trees_full = '\n'.join(winter_trees_lines)

print(winter_trees_full)
```

##### Output

```
All the complicated details
of the attiring and
the disattiring are completed!
A liquid moon
moves gently among
the long branches.
Thus having prepared their buds
against a sure winter
the wise trees
stand sleeping in the cold.
```

### .strip()

> When working with strings that come from real data, you will often find that the strings aren't super clean. You'll find lots of extra whitespace, unnecessary line breaks, and rogue tabs. 

Python provides a great method for cleaning strings: `.strip()`. Stripping a string removes all whitespace characters from the beginning to end. Consider the following example:

```python
featuring = "           rob thomas                 "
print(featuring.strip())

#output = 'rob thomas'
```
> All of the whitespace on the outside has been stripped, but all of the whitespace in the middle was preserved.

You can also use `.strip()` with a *character argument*, which will strip that character from either end of the string. 

```python
featuring = "!!!rob thomas       !!!!!"
print(featuring.strip('!'))
# => 'rob thomas       '
```
> By including the argument `'!'` we are able to strip all of the `!` characters from either side of the string. Notice that now that we’ve included an argument we are no longer stripping whitespace, we are ONLY stripping the argument.

##### Challenge

1. They sent over another list containing all the lines to the Audre Lorde poem, _Love, Maybe_. They want you to join together all of the lines into a single string that can be used to display the poem again, but this time, you’ve noticed that the list contains a ton of unnecessary whitespace that doesn’t appear in the actual poem.

First, use `.strip()` on each line in the list to remove the unnecessary whitespace and save it as a new list `love_maybe_lines_stripped`.

```python
love_maybe_lines = ['Always    ', '     in the middle of our bloodiest battles  ', 'you lay down your arms', '           like flowering mines    ','\n' ,'   to conquer me home.    ']
```

2. `.join()` the lines in `love_maybe_lines_stripped` together into one large multi-line string, `love_maybe_full`, that can be printed to display the poem.

Each line of the poem should show up on its own line.

```python
love_maybe_lines_stripped = []

for line in love_maybe_lines:
  love_maybe_lines_stripped.append(line.strip())
```

3. Print `love_maybe_full.
### Replace

> The next string method we will cover is `.replace()`. Replace takes two arguments and replaces all instances of the first argument in a string with the second argument.

The syntax is as follows:

```Python
string_name.replace(substring_being_replaced, new_substring)
```

Great!, Let's put it in context and look at an example. 

```Python
with_spaces = "You got the kind of loving that can be so smooth"
with_underscores = with_spaces.replace(' '. '_')
print(with_underscores)
```
> # 'you_got_the_kind_of_loving_that_can_be_so_smooth'

Here, we used `.replace()` to change every instance of a space in the string above to be an underscore instead.

Note that in this example, we used a single character, but these [substrings](https://www.codecademy.com/resources/docs/python/substrings) can be multiple characters long!

##### Challenge:

Use `.replace()` to change all instances of `Tomer` in the bio to `Toomer`. Save the updated bio to the string `toomer_bio_fixed`.

```Python
toomer_bio = \

"""
Nathan Pinchback Tomer, who adopted the name Jean Tomer early in his literary career, was born in Washington, D.C. in 1894. Jean is the son of Nathan Tomer was a mixed-race freedman, born into slavery in 1839 in Chatham County, North Carolina. Jean Tomer is most well known for his first book Cane, which vividly portrays the life of African-Americans in southern farmlands.
"""
```

##### Solution:

```Python
toomer_bio_fixed = toomer_bio.replace("Tomer", "Toomer")
```

### `.find()`

> Another interesting string method is `.find()`. `.find()` takes a string as an argument and searching the string it was run on for that string. It then returns the first *index value* where that string is located. 

```python
print('smooth'.find('t'))
# => '4'
```

We searched the string `'smooth'` for the string `'t'` and found that it was at the fourth index spot, so `.find()` returned `4`

You can also search for larger [strings](https://www.codecademy.com/resources/docs/python/strings), and `.find()` will return the index value of the first character of that string. 

```python
print("smooth".find('oo'))
# => '2'
```

> Notice here that `2` is the index of the first *o*.
### `.format()`

> Python also provides a handy string method for including [variables](https://www.codecademy.com/resources/docs/python/variables) in [strings](https://www.codecademy.com/resources/docs/python/strings).

This method is `.format()`. `.format()` takes variables as an argument and includes them in the string that it is run on. 

You include `{}` marks as placeholders for where those variables will be imported. 

Consider this function:

```Python
def favorite_song_statement(song, artist):  
  return "My favorite song is {} by {}.".format(song, artist)
```

> The function `favorite_song_statement` takes two arguments, song and artist, then returns a string that includes both of the arguments and prints a sentence.

Note: `.format()` can take as many arguments as there are `{}` in the string it is run on, which in this case is two.

```Python
print(favorite_song_statement("Smooth", "Santana"))
# => "My favorite song is Smooth by Santana."
```

> You're probably asking yourself, I could have written this function using string concatenation instead of `.format()`, why is this method better?

The answer is *legibility and reusability.* 

It is much easier to picture the end result `.format()` than it is to picture the end result of string concatenation and legibility is everything.
	You can also reuse the same base string with different variables, allowing you to cut down on unnecessary, hard to interpret code.
### `.format()` II

> `.format()` can be made even more legible for other people reading your code by including [_keywords_](https://www.codecademy.com/resources/docs/python/keywords). 
> 	Previously, with `.format()`, you had to make sure that your variables appeared as arguments in the same order that you wanted them to appear in the string, which added unnecessary complications when writing code.  

By including keywords in the string, and in the arguments, you can remove that ambiguity.

Here's an example:

```Python
def favorite_song_statement(song, artist):
	return "My favorite song is {song} by {artist}.".format(song=song, artist=artist)
```

> Now it is clear to anyone reading the string what it is supposed to return, they don't even need to look at the arguments of `.format()` in order to get a clear understanding of what is supposed to happen.

You can even reverse the order of `artist` and `song` in the code above and it will work the same way.

For example, if the arguments of `.format()` are in a different order, the code will still work since the keywords are present:

```Python
def favorite_song_statement(song, artist):
  # this will have the same output as the above example
  return "My favorite song is {song} by {artist}.".format(artist=artist, song=song)
```

> This makes writing and reading the code much easier.

# Review

> Excellent work! This lesson has shown you the vast majority of string methods and their power. 

Whatever the problem you are trying to solve, if you are working with strings then string methods are likely going to be part of the solution. 

Over this lesson we learned:

- `.upper()`, `.lower()`, `.title()` adjust the casing of your string.
- `.split()` takes a string and creates a list of `substrings`.
- `.join()` takes a list of strings and creates a string
- `.strip()` cleans off whitespace, or other noise from the beginning and end of a string. 
- `.replace()` replaces all instances of a character/string in a string with another character/string
- `.find()` searches a string for character/string and returns the index value that character/string is found at. 
- `.format()` allows you to interpolate a string with variables.

```C
script.c: In function ‘main’:
script.c:6:1: error: expected ‘;’ before ‘}’ token 
} 
^
```

> The text above gives the following information:

- The component location, `In function 'main'`
- The line and column number, `6:1`

# Modules In Python

## Modules Python Introduction

In the world of programming, we care a lot about making code reusable. In most cases, we write code so that it can be reusable for ourselves. But sometimes we share code that's helpful across a broad range of situations. 

In this lesson, we'll explore how to use tools other people have built in Python that are not included automatically for you when you install Python. Python allows us to package code in [files](https://www.codecademy.com/resources/docs/python/files) or [sets](https://www.codecademy.com/resources/docs/python/sets) of files called [_modules_](https://www.codecademy.com/resources/docs/python/modules?page_ref=catalog).

A ***module*** is a collection of Python declarations intended broadly to be used as a tool. Modules are often referred to as "libraries" or "packages" -- a package is really a directory that holds a collection of modules. 

Usually, to use a module in a file, the basic syntax you need at the top of that file is:

```Python
from module_name import object_name
```

Often, a library will include a lot of code that you don't need that may slow down your program or conflict with existing code. Because of this, it makes sense to only import what you need.

One common library that comes as part of the Python standard library is `datetime`. `datetime` helps you work with dates and times in Python. Let's get started by importing and using the `datetime` module. In this case, you'll notice that `datetime` is both the name of the library *and* the name of the object you are importing.

## Modules Python Random

`datetime` is just the beginning. There are hundreds of Python [modules](https://www.codecademy.com/resources/docs/python/modules) that we can use. Another one of the most commonly used is [`random`](https://www.codecademy.com/resources/docs/python/random-module?page_ref=catalog) which allows you to generate numbers or select items at random.

With `random`, we'll be using more than one piece of the module's functionality, so the import syntax will look like:

```python
import random
```

We'll work with two common `random` functions:

- `random.choice()` which takes a list as an argument and returns a number from the list.
- `random.randint()` which takes two numbers as arguments and generates a random number between the two numbers you passed in

Let's take randomness to a whole new level by picking a random number from a list of randomly generated numbers between 1 to 100.

## Modules Python Namespaces

Notice that when we want to invoke the `randint()` we call `random.randint()`. This is default behavior where Python offers a *namespace* for the module. A ***namespace*** isolates the functions, classes, and variables defined in the module from the code in the file doing the importing. Your *local namespace*, meanwhile, is where your code is run.

Python defaults to naming the namespace after the module being imported, but sometimes this name could be ambiguous or lengthy. Sometimes, the module's name could also conflict with an object you have defined within your local namespace.

Fortunately, this name can be altered by *aliasing* using the `as` keyword:

```python
import module_name as name_you_pick_for_the_module
```

*Aliasing* is most often done if the name of the library is long and typing the full name every time you want to use one of its functions is laborious.

You might also occasionally encounter `import *`. The `*` is known as a "wildcard" and matches anything and everything. This syntax is considered dangerous because it could *pollute* our local namespace. Pollution occurs when the same name could apply to two possible things. For example, if you happen to have the function `floor()` focused on floor tiles, using `from math import *` would also import a function `floor()` that rounds down floats. 

Let's combine your knowledge of the `random` library with another fun library called `matplotlib`, which allows you to plot your Python code in 2D. 

You'll use a new `random` function `random.sample()` that takes a range and a number as it's arguments. It will return the specified number of random numbers from that range. 

```Python
#random.sample takes a list and randomly selects k items from it
new_list = random.sample(list, k)
#for example:
nums = [1, 2, 3, 4, 5]
sample_nums = random.sample(nums, 3)
print(sample_nums) # 2, 5, 1
```

---
```Python
import codecademylib3_seaborn
```

1. Below `import codecademylib3_seaborn`, import `pyplot` from the module `matplotlib` with the alias `plt`.

```python
import codecademylib3_seaborn
from matplotlib import pyplot as plt
```

2. Import `random` below the other import statements. It’s best to keep all imports at the top of your file.

```python
import codecademylib3_seaborn
from matplotlib import pyplot as plt
import random
```

3. Create a variable `numbers_a` and set it equal to the range of numbers 1 through 12 (inclusive).

```python
import codecademylib3_seaborn
from matplotlib import pyplot as plt
import random

numbers_a range(1, 13)
```

4. Create a variable `numbers_b` and set it equal to a random sample of twelve numbers within `range(1000)`.

   Feel free to print `numbers_b` to see your random sample of numbers.

```python
import codecademylib3_seaborn
from matplotlib import pyplot as plt
import random

numbers_a = range(1, 13)
numbers_b = random.sample(range(1000), 12)
```

5. Now let’s plot these number sets against each other using `plt`. Call `plt.plot()` with your two variables as its arguments.

```python
import codecademylib3_seaborn
from matplotlib import pyplot as plt
import random

numbers_a = range(1, 13)
numbers_b = random.sample(range(1000), 12)

plt.plot(numbers_a, numbers_b)
plt.show()
```

## Modules Python Decimals

Let's say you are writing software that handles monetary transactions. If you used Python's built-in floating point arithmetic to calculate a sum, it would result in a weirdly formatted number. 

```python
cost_of_gum = 0.10
cost_of_gumdrop = 0.35

cost_of_transaction = cost_of_gum + cost_of_gumdrop
# Returns 0.4499999999999999996
```

Being familiar with *rounding errors* in floating point arithmetic you want to use a data type that performs decimal arithmetic more accurately. You could do the following:

```python
from decimal import Decimal

cost_of_gum = Decimal('0.10')
cost_of_gumdrop = Decimal('0.35')

cost_of_transaction = cost_of_gum + cost_of_gumdrop
#returns 0.45 instead of 0.449999999999999996
```

Above, we use:

- The `decimal` module's `Decimal` data type to add 0.10 with 0.35. Since we used the `Decimal` type the arithmetic acts much more as expected.

Usually, [modules](https://www.codecademy.com/resources/docs/python/modules) will provide [functions](https://www.codecademy.com/resources/docs/python/functions) or [data types](https://www.codecademy.com/resources/docs/python/data-types) that we can use to solve a general problem, allowing us more time to focus on the software that we are building to solve a more specific problem. 

Ready, set, fix some floating point math by using decimals!

## Modules Python Files and Scope

You may remember the concept of [_scope_](https://www.codecademy.com/resources/docs/python/scope) from when you were learning about [functions](https://www.codecademy.com/resources/docs/python/functions) in Python. 

- If a variable is defined *inside* a function, it will not be accessible *outside* of the function.

Scope also applies to [_classes_](https://www.codecademy.com/resources/docs/python/classes) and to the [_files_](https://www.codecademy.com/resources/docs/python/files) you are working within.

*Files* have scope? We may be wondering.

Yes. Even files inside the *same directory* do not have access to each other's [variables](https://www.codecademy.com/resources/docs/python/variables), functions, classes, or any other code. So if I have a file **sandwiches.py** and another file `hungry_people.py`, how do I give my hungry people access to my sandwiches?

Well, ***files are actually modules***, so you can give a file access to another file's content using that glorious `import` statement.

With a single line of `from sandwiches import sandwiches` at the top of **hungry_people.py**, the hungry people will have all the sandwiches they could ever want.

### Modules Python Review

You’ve learned:

- what [modules](https://www.codecademy.com/resources/docs/python/modules) are and how they can be useful
- how to use a few of the most commonly used Python libraries
- what namespaces are and how to avoid polluting your local namespace
- how [scope](https://www.codecademy.com/resources/docs/python/scope) works for [files](https://www.codecademy.com/resources/docs/python/files) in Python

Programmers can do great things if they are not forced to constantly reinvent tools that have already been built. With the power of modules, we can import any code that someone else has shared publicly.

In this lesson, we covered some of the Python Standard Library, but you can explore all the modules that come packaged with every installation of Python at the Python Standard Library documentation.

This is just the beginning. Using a package manager (like conda or pip3), you can install any modules available on the Python Package Index.

The sky’s the limit!

# Dictionaries

## Introduction to Python Dictionaries

A [_dictionary_](https://www.codecademy.com/resources/docs/python/dictionaries?page_ref=catalog) is an unordered set of `key: value` pairs. 

It provides us with a way to map pieces of data to each other so that we can quickly find values that are associated with one another. 

Suppose we want to store the prices of various items sold at a cafe:

- Avocado Toast for 6 dollars
- Carrot Juice for 5 dollars
- Blueberry Muffin for 2 dollars

In Python, we can create a dictionary called `menu` to store this data:

```python
menu = {"avocado toast": 6, "carrot juice": 5, "blueberry muffin": 2}
```

Notice that: 

1. A dictionary begins and ends with curly braces `{}`
2. Each item consists of a key ("`avocado toast`") and a value (`6`).
3. Each `key:value` pair is separated by a comma.

## Make a Dictionary

In the previous exercise, we saw a dictionary that maps strings to numbers (i.e. `"avocado toast": 6`). However, the keys can be numbers as well.

For example, if we were mapping restaurant bill subtotals to the bill total after tip, a dictionary could look like:

```python
subtotal_to_total = {20: 24, 10: 12, 5: 6, 15: 18}
```

Values can be of any type. We can use a string, a number, a list, or even another dictionary as the value associated with a key. 

For example: 

```python
students_in_classes = {"software_design": ["Aaron", "Delila", "Samson"], "cartography": ["Christopher", "Juan", "Marco"], "philosophy": ["Frederica", "Manuel"]}
```

The list `["Aaron", "Paul", "Samson"]`, which is the value for the key `software design`, represents the students in that class. 

We can also mix and match key and value types, for example:

```python
person = {"name", "Shuri", "age": 18, "family": ["T'Chaka, "Ramonda"]}
```

## Invalid Keys

We can have a list or a dictionary as a *value* of an item in a dictionary, but we cannot use these data types as keys of the dictionary. If we try to, we will get a ***TypeError***. 

For example:

```python
powers = {[1, 2, 4, 8, 16]: 2, [1, 3, 9, 27, 81], 3}
```

This code will yield:

```error
TypeError: unhashable type: 'list'
```

The word "unhashable" in this context means that this 'list' is an object that can be changed. 

Dictionaries in Python *rely on each key having a **hash value**, a specific identifier for the key.* If the key can change, that hash value would not be reliable. So the keys must always be unchangeable, hashable data types, like numbers or strings.

## Empty Dictionary

A dictionary doesn't have to contain anything. Sometimes we need to create an empty dictionary when we plan to fill it later based on some other input. 

We can create an empty dictionary like this:

```python
empty_dict = {}
```

We will explore ways to fill a dictionary in the next exercise.

## Add a Key

To add a single `key: value` pair to a dictionary, we can use the syntax:

```python
dictionary[key] = value
```

For example if we had our `menu` dictionary from the first exercise:

```python
menu = {"oatmeal": 3, "avocado toast": 6, "carrot juice": 5, "blueberry muffin": 2}
```

And we wanted to add a new item, `cheesecake`, for `8 dollar`, we could use:

```python
menu[cheesecake] = 8
```

Now, `menu` looks like:

```python
{"oatmeal": 3, "avocado toast": 6, "carrot juice": 5, "blueberry muffin": 2, "cheesecake": 8}
```

## Add Multiple Keys

If we wanted to add multiple key: value pairs to a dictionary at once, we can use the `.update()` method. 

Looking at our `sensors` object from a previous exercise:

```python
sensors = {"living room": 21, "kitchen": 23, "bedroom": 20}
```

If we wanted to add 3 new rooms, we could use:

```python
sensors.update({"pantry": 22, "guest room": 25, "patio": 34})
```

This would add all three items to the `sensors` dictionary.

Now `sensors` looks like:

```python
{"living room": 21, "kitchen": 23, "bedroom": 20, "pantry": 22, "guest room": 25, "patio": 34}
```

## Overwrite Values

We know that we can add a key by using the following syntax:

```python
menu["banana"] = 3
```

This will create a key `"banana"` and set it's value to `3`. But what if we used a key that already has an entry in the `menu` category?

In that case, our value assignment would overwrite the existing value attached to that key. We can overwrite the value of `"oatmeal"` like this:

```python
menu = {"oatmeal": 3, "avocado toast": 6, "carrot juice": 5, "blueberry muffin": 2}
menu["oatmeal"] = 5
print(menu)
```

This would yield:

```output
{"oatmeal": 5, "avocado toast": 6, "carrot juice": 5, "blueberry muffin": 2}
```

## Dict Comprehensions

Let's say we have two lists that we wanbt to combine into a dictionary, like a list of students and a list of their heights, in inches:

```python
names = ['Jenny', 'Alexis', 'Sam', 'Grace']
heights = [61, 70, 67, 64]
```

Python allows you to create a dictionary using a dict comprehension, with this syntax:

```python
students = {key:value for key, value in zip{names, heights}}
# students is now {'Jenny':61, 'Alexus': 70, 'Sam': 67, 'Grace': 64}
```

Remember that `zip()` combines two list into an iterator of tuples with the list elements paired together.  This dict comprehension:

1. Takes a pair from the iterator of tuples
2. Names the elements in the pair `key` (the one originally from the `names` list) and `value` (the one originally from the `heights list`)
3. Creates a `key: value` items in the `students` dictionary
4. Repeats steps 1-3 for the entire iterator of pairs

## Review

So far we have learned:

- How to create a dictionary
- How to add elements to a dictionary
- How to update elements in a dictionary
- How to use a dict comprehension to create a dictionary from two lists

Let’s practice these skills!

# Using Dictionaries

Now that we know how to create a dictionary, we can start using already created [dictionaries](https://www.codecademy.com/resources/docs/python/dictionaries) to solve problems.

In this lesson, you’ll learn how to:

- Use a key to get a value from a dictionary
- Check for existence of keys
- Iterate through keys and values in dictionaries

## Get a Key

Once you have a dictionary, you can access the values in it by providing the key. For example, let's imagine we have a dictionary that maps buildings to their heights, in meters:

```python
building_heights = {"Burj Khalifa": 828, "Shanghai Tower": 632, "Abraj Al Bait": 601, "Ping An": 599, "Lotte World Tower": 554.5, "One World Trade": 541.3}
```

> We can then access the data in it like this:

```python
print(building_heights["Burj Khalifa"]) # Prints 828
print(building_heights["Ping An"]) # Prints 599
```

## Get an Invalid Key

Let's say we have our dictionary of building heights from the last exercise. 

```python
building_heights = {"Burj Khalifa": 828, "Shanghai Tower": 632, "Abraj Al Bait": 601, "Ping An": 599, "Lotte World Tower": 554.5, "One World Trade": 541.3}
```

What if we wanted to know the height of the Landmark 81 in Ho Chi Minh City? We could try:

```python
print(building_heights["Landmark 81"])
```

But "`Landmark 81`" does not exist as a key in the `building heights` dictionary. So this will throw a **Key Error**:

```
KeyError: 'Landmark 81'
```

One way to avoid this error is to first check if the key exists in the dictionary:

```python
key_to_check = "Landmark 81"

if key_to_check in building_heights:
	print(building_heights["Landmark 81"])
```

This will not throw an error, because `key_to_check in building_heights` will return `False`, and so we never try to access the key.

## Safely Get a Key

We saw in the last exercise that we had to add a key:value pair to a dictionary in order to avoid a KeyError. This solution is not sustainable. 

We can't predict every key a user may call and add all of these placeholder values to our dictionary.

Dictionaries have a `.get()` method to search for a value instead of the `my_dict[key]` notation we have been using. If the key you are trying to `.get()` does not exist, it will return `None` by default.

```python
building_heights = {"Burj Khalifa": 828, "Shanghai Tower": 632, "Abraj Al Bait": 601, "Ping An": 599, "Lotte World Tower": 554.5, "One World Trade": 541.3}

#this line will return 632:
building_heights.get("Shanghai Tower")

#this line will return None:
building_heights.get("My House)
```

We can also specify a value to return if the key doesn't exist. For example, we might want to return a building height of 0 if our desired building is not in the dictionary:

```python
print(building_heights.get('Shanghai Tower', 0)) #prints 632
print(building_heights.get('Mt. Olympus', 0)) # prints 0
print(building_heights.get('Kilimanjaro', 'No Value') # Prints 'No Value'
```

## Delete a Key

Sometimes we want to get a key and remove it from the dictionary. Imagine we are running a raffle, and we have this dictionary mapping ticket numbers to prizes:

```python
raffle = {223842: "Teddy Bear", 872921: "Concert Tickets", 320291: "Gift Basket", 412123: "Necklace", 298787: "Pasta Maker"}
```

When we get the ticket number, we want to return the prize and also remove that pair from the dictionary, since the prize has been given away. We can use `.pop()` to do this. Just like with `.get()`, we can provide a default value to return if the key does not exist in the dictionary.

```python
print(raffle.pop(320291, "No Prize"))# Prints "Gift Basket"
print(raffle)# Prints {223842: "Teddy Bear", 872921: "Concert Tickets", 412123: "Necklace", 298787: "Pasta Maker"}
print(raffle.pop(100000, "No Prize"))# Prints "No Prize"
print(raffle)# Prints {223842: "Teddy Bear", 872921: "Concert Tickets", 412123: "Necklace", 298787: "Pasta Maker"}
print(raffle.pop(872921, "No Prize"))# Prints "Concert Tickets"print(raffle)# Prints {223842: "Teddy Bear", 412123: "Necklace", 298787: "Pasta Maker"}
```

> `.pop()` works to delete items from a dictionary, when you know the key value.

## Get All Keys

Sometimes we want to cooperate on all of the keys in a dictionary. For example, if we have a dictionary of students in a math class and their grades:

```python
test_scores = {"Grace":[80, 72, 90], "Jeffrey":[88, 68, 81], "Sylvia":[80, 82, 84], "Pedro":[98, 96, 95], "Martin":[78, 80, 78], "Dina":[64, 60, 75]}
```

We want to get a roster of the students int he class, without including their grades. We can do this with the built-in `list()` function:

```python
print(list(test_scores)) 

# Prints ["Grace", "Jeffrey", "Sylvia", "Pedro", "Martin", "Dina"]
```


Dictionaries also have a `.keys()` method that returns a `dict_keys` object. A `dict_keys` object is a *view* object, which provides a look at the current state of the dictionary, without the user being able to modify anything. The `dict_keys` object returned by `.keys()` is a set of the keys in the dictionary. You cannot add or remove elements from a `dict_keys` object, but it can be used in the place of a list for iteration:

```python
for student in test_scores.keys():
  print(student)
```

will yield:

```
Grace
Jeffrey
Sylvia
Pedro
Martin
Dina
```

## Get All Values

**Dictionaries** have a `.value()` method that returns a `dict_values` object (just like a `dict_keys` object, but for values!) with all of the values in the dictionary. It can be used in the place of a list for iteration:

```python
test_scores = {"Grace":[80, 72, 90], "Jeffrey":[88, 68, 81], "Sylvia":[80, 82, 84], "Pedro":[98, 96, 95], "Martin":[78, 80, 78], "Dina":[64, 60, 75]}

for score_list in test_scores.values():
	print(score_list)
```
```
[80, 72, 90]
[88, 68, 81]
[80, 82, 84]
[98, 96, 95]
[78, 80, 78]
[64, 60, 75]
```

> There is no built-in function to get all of the values as a list, but if you *really* want to, you can use:

```python
list(test_scores.values())
```

> However, for most purposes, the `dict_values` object will act the way you want a list to act.

## Get All Items

You can get both the keys and the values with the `.items()` method. Like `.keys()` and `.values()`, it returns a `dict_list` object. Each element of the `dict_list` returned by `.items()` is a **tuple** consisting of:

```
(keys, value)
```

So, to iterate through, you can use this syntax:

```python
biggest_brands = {"Apple": 184, "Google": 141.7, "Microsoft": 80, "Coca-Cola": 69.7, "Amazon": 64.8}

for company, value in biggest_brands.items():
	print(company + " has a value of " + str(value) + " billion dollars. ")
```
```
Apple has a value of 184 billion dollars.
Google has a value of 141.7 billion dollars.
Microsoft has a value of 80 billion dollars.
Coca-Cola has a value of 69.7 billion dollars.
Amazon has a value of 64.8 billion dollars.
```

##Review

In this lesson, you’ve learned how to go through [dictionaries](https://www.codecademy.com/resources/docs/python/dictionaries) and access keys and values in different ways. Specifically, you have seen how to:

- Use a key to get a value from a dictionary
- Check for existence of keys
- Remove a key: value pair from a dictionary
- Iterate through keys and values in dictionaries





# Match Statements in Python

Like the if-else statements, we can also use switch statements to build a program's control flow. In Python, we have match-case statements that implement switch statements. 

Let's discuss switch and match statements, how to define them in a Python program, and when to use match-case statements instead of if-else statements to build control flow in a program.

## What is a Switch Statement?

A switch statement is a control flow statement the executes a block of code, among many others, based on the value of a variable or expression.

```Python 
user_name = "Dave"
if user_name == "Dave":
    print("Get off my computer Dave!")
elif user_name == "angela_catdaddy87"
    print("I know it's you Dave! Go away!)
elif user_name == "Codecademy"
    print("Access Granted")
else:
	print("Username not recognized")
```

The above code can be written using a switch statement, as shown in the following code: Don't worry about the syntax. It's explained in the next section.

```python
user_name = "Dave"
switch user_name:
    case "Dave":
        print("Get off my computer Dave!")
    case "angela_catlady87":
	    print("I know it's you Dave! Go away!)
	case "Codecademy":
	    print("Access Granted")
	case default:
	    print("Username not recognized.")
```

If we run the code above, it will encounter a `SyntaxError` because Python does not have a switch keyword. Python didn't have switch statements or any of its implementations until 3.10.

In Python 3.10, we got match-case statements that implement switch statements and other functionalities. From now one, we will refer to switch-case statements as match-case statements, as defined in Python.

## How to Declare a Match Statement in Python?

We use the `match`, `case`, and `default` keywords to define match-case statements in Python. It has the following syntax:

```python
match expression:
	case value_1:
	# code to execute when expression equals value_1
	case value_2:
	# code to execute when expression equals value_2
	case value_3:
	# code to execute when expression equals value_3
	case value_4:
	# code to execute when expression equals value_4
	case value_N:
	# code to execute when expression equals value_N
	case default:
	# code to execute when expression isn't equal to any of the values
```

In the code above:

- `match` is a keyword that marks the start of the match block
- `expression` can be a variable, an arithmetic expression, a Boolean expression, or a Python object like a list, type, or string.
- The code inside a case block is executed for a single value of expression. For example, only if `expression` evaluates to `value_1` will the code inside the `case value_1` block be executed. If `expression` evaluates to `value_2`, then only the code inside the `case_value_2` block will be executed.
- Only one case block is executed in the entire match block for any given value of `expression`. Once a case block is executed, the program's control flow moves out of the match block.
- The `default` block is *always present* at the end of the match block. If `expression` matches none of the values in other case blocks, the code inside `case default` is executed.

Using the above syntax, we can rewrite the code given in the switch-case example as shown below:

```python
user_name = "Dave"  
match user_name:      
	case "Dave":          
		print("Get off my computer Dave!")      
	case "angela_catlady_87":          
		print("I know it is you, Dave! Go away!")       
	case "Codecademy":          
		print("Access Granted.")      
	case default:          
		print("Username not recognized.")  
```

If we run the code above, we will get the following output:

```
Get off my computer Dave!
```

## When to Use Match Statements in Python?

We can use match-case statements for the following use cases:

- Match-case statements can be an efficient alternative to if-elif-else statements. When a variable or expression can take multiple values, and we need to perform a different action for each possible value, we can use match statements.
- A match-case block can be used for other tasks, like structural pattern matching, in addition to replacing if-else blocks. This helps us check for different code conditions or Python objects like lists, tuples, and strings.
- Match-case statements are more readable compared to if-elif-else statements. Hence, in cases where we must check for many values that an expression can take, we should use match-case statements.

# Tuples

**Learn about Tuples in Python**

Tuples are one of the built-in data structures in Python. Just like lists, tuples can hold a sequence of items and have a few key advantages.

- Tuples are more *memory efficient* than lists.
- Tuples have a slightly higher time efficiency than lists.

This is mostly because Tuples are **immutable**, meaning we can't modify a tuple's elements after creating one, and do not require an extra memory block like lists. Because of this, tuples are great to work with if you are working with data that won't need to be changed in our code.

## Tuples

In Python, tuples are defined with parenthesis `()` with comma-separated values. Just like lists, tuples are sequences and can hold objects of different data types. 

This tuple has 4 items. We can see that we have 4 items separated by commas:

```python
my_tuple = ('abc', 123, 'def', 456)
```

Tuples are capable of holding one item as long as the item is followed by a comma:

```python
my_tuple = ('abc')
```

## Tuple Indexing and Slicing

Items in a tuple can be accessed with their index, otherwise known as their position in the Tuple. 

```python
my_tuple = ('abc', 123, 'def', 456, 789, 'ghi')
```

Indices can be used to access specific items of this tuple. For example, if we want to access the first item, we can use index `0` (remember that Python is a zero-index language). We write the name of the tuple followed by brackets `[]` that contains the index to access the item. This code would print the first item, `'abc'`.

```python
print(my_tuple[0]) # prints abc
```

We can also apply slicing, using a range of indices to access multiple items just like in a list. The brackets should contain the first index as well as the index of the end of the item, separated by `:`. This code would print the items at positions 3 and 4:

```python
print(my_tuple[3:5]) # prints (456, 789)
```

## Common Built-In Functions

In contrast to lists, tuples have a limited number of built-in functions as they are immutable. We'll take a look at a few built-in functions below:

### `len()`

The length of a tuple can be measured using the function `len()`. It takes the tuple as an argument to count the items in the tuple. 

```python
my_tuple = ('abc', 123), 'def', 456, 789, 'ghi')
print(len(my_tuple)) # prints 6
```

### `max()`

The built-in function `max()` returns the tuple's maximum value. Note that this function requires all of the values to be of the same data type. If used with numerical values, the function returns the maximum value. If used with string values, the function returns the value at the tuple's **maximum index** as if it was sorted alphabetically. The string closer to the letter `Z` in the alphabet would have a higher index.

```python
my_tuple = (65, 2, 88, 101, 25)
max(my_tuple)

my_tuple = ('orange', 'blue', 'red', 'green')
print(max(my_tuple))

my_tuple = ('abc', 234, 567, 'def')
print(max(my_tuple))
```

### `min()`

The built-in function `min()` returns the tuple's minimum value. Similar to the `max()` function, the `min()` function requires all of the values to be of the same data type. If used with numerical values, the function returns the minimum value. If used with string values, the function returns the value at the tuple's minimum index as if it was sorted alphabetically. The string closer to the letter "A" in the alphabet would have a lower index.

```python
my_tuple = (65, 2, 88, 101, 25)
min(my_tuple)

my_tuple = ('orange', 'blue', 'red', 'green')
min(my_tuple)

my_tuple = ('abc', 234, 567, 'def')
min(my_tuple)
```

### `.index()`

The built-in method `index()` takes in a value as the argument to find its index in the tuple. 

```python
my_tuple = ('abc', 234, 567, 'def')
print(my_tuple.index('abc'))
print(my_tuple.index(567))
```

### `.count()`

The built-in method `.count()` takes in a value as the argument to find the number of occurrences in the tuple.

```python
my_tuple = ('abc', 'abc', 2, 3, 4)
my_tuple.count('abc') # returns 2
my_tuple.count(3) # returns 1
```

# Lambda Functions

Python is known for its simplicity and readability, and one of its powerful features is the ability to create functions. While you're probably familiar with defining functions using the `def` keyword, Python offers a more concise way to create small, anonymous functions called **lambda functions**.

In this article, we'll dive into the world of lambda functions, exploring their syntax, use cases, and best practices. By the end, we will have a solid understanding of how to leverage these compact functions in our Python code.

## What are Lambda Functions?

*Lambda Functions*, also known as *anonymous functions*, are small, inline functions that can have any number of arguments but only one expression. They are defined using the `lambda` keyword and are typically used for short, simple operations.

Unlike regular functions defined with `def`, lambda functions don't have a name and are usually used in situations where you need a simple function for a short period of time.

Let's compare a regular function with a lambda function:

```python
def square(x):
    return x ** 2


square_lambda = lambda x: x ** 2
```

Both functions square the input, but the lambda function is more *concise*.

## Syntax of Lambda Functions

The basic syntax of a lambda function is:

```
lambda [arguments]: [expression]
```

Here are a couple of simple examples:

```python
add = lambda a, b: a + b
print(add(3,5))

greeting = lambda name: f"Hello, {name}!"
print(greeting("Alice"))

```

## Using Lambda Functions

Lambda functions are most commonly used as arguments to higher-order functions such as `map()`, `filter()`, and `sorted()`. Higher-order functions are functions that can accept other functions, such as lambda functions, as arguments. Let's look at some examples:

### Using Lambda with `map()`:

The `map()` function applies the given lambda function to each item in a list:

```python
numbers = [1, 2, 3, 4, 5]

squared = list(map(lambda x: x ** 2, numbers))

print(squared) # output: [1, 4, 9, 16, 25]
```

In this example, the lambda function `lambda x: x ** 2` squares each number in the `numbers` list. The `map()` function applies this lambda to each element, resulting in a new list where every number is squared.

### Using Lambda with `filter()`

The `filter()` function creates a new list of elements for which the given lambda function returns True:

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

even_numbers = list(filter(lambda x: x % 2 == 0, numbers))

print(even_numbers) # output [2, 4, 6, 8, 10]
```

Here the lambda function `lambda x: x % 2 == 0` checks if a number is even. The `filter()` function uses this lambda to keep only the even numbers from the original list, creating a new list containing only even numbers.

### Using Lambda with `sorted()`

The `sorted()` function can use a lambda function as a key for custom sorting:

```python
students = [('Alice', 'A', 15), ('Bob', 'B', 12), ('Charlie', 'A', 20)]

sorted_students = sorted(students, key=lambda x: x[2])
print(sorted_students)
```

In this case, the lambda function `lambda x: x[2]` is used as the key for sorting. It tells the `sorted()` function to use the third element (index 2) of each tuple for comparison. As a result, the list of students is sorted based on their age (the third element in each tuple).

We'll further discuss the higher-order functions, such as the `map()` function, in more detail in our next article.

## Advantages and Limitations

Lambda functions offer several advantages:

- They are concise and make code more readable for simple operations.
- They're convenient for small, throwaway functions, especially as arguments to higher-order functions.

However, they also have limitations:

- They can only contain expression, not statements.
- They are limited to a single expression, which can make complex operations difficult.
- They can be harder to debug due to their anonymous nature.

## Best Practices

Use lambda functions when:

- You need a simple function for a short period.
- You're passing a simple function as an argument to higher-order functions.

Avoid lambda functions when:

- The operation is complex or *requires multiple expressions*
- You need to reuse the function multiple times (define a regular function instead)
## Wrapping Up

Lambda functions are a powerful feature in Python that allow you to write more concise and functional code. They’re particularly useful for simple operations and as arguments to higher-order functions. However, it’s important to use them judiciously and switch to regular functions when the logic becomes more complex.

Practice using lambda functions in your code to become more comfortable with them. Try rewriting some of your existing functions as lambda functions where appropriate, and experiment with using them in `map()`, `filter()`, and `sorted()`.

# Map Functions

Python provides several built-in functions that help with functional programming. One of the most versatile and commonly used is the `map()` function. In this article, we'll explore what `map()` is, how it works, and when to use it in our Python programs.

## What is the `map()` Function?

The `map()` function is a built-in function in Python that applies a given function to each item in an iterable (like a list, tuple, or string) and returns a new iterable as a result.

The basic syntax of `map()` is:

```python
map(function, iterable, [iterable2, iterable3, ...])
```

- `function` is the function to apply to each item in the iterable(s)
- `iterable` is the iterable (or optionally multiple iterables) to process.

## How `map()` Works

Let's break down how `map()` works with a simple example:

```python
def double(x):

	return x * 2

numbers = [1, 2, 3, 4, 5]
doubled_numbers = map(double, numbers)

print(list(doubled_numbers)) # Output: [2, 4, 6, 8, 10]
```

> In this example, `map()` applies the `double` function to each number in the `numbers` list, creating a new iterator with the results.

## Using `map()` with Built-in Functions

We can use `map()` with Python's built-in functions. For example, we can quickly convert a list of strings to integers:

```python
str_nums = ['1', '2', '3', '4', '5']
int_nums = list(map(int, str_nums))

print(int_nums)
# [1, 2, 3, 4, 5]
```

> Or change the length of another list of strings:

```python
words = ['apple', 'banana', 'cherry']
word_lengths = list(map(len, words))

print(word_lengths)
# [5, 6, 6]
```

## Using `map()` with Lambda Functions

But `map()` is most often used in conjunction with lambda functions for quick, one-off operations. For example, here we easily double each number in a list:

```python
numbers = [1, 2, 3, 4, 5]

doubled = list(map(lambda x: x * 2, numbers))

print(doubled) 
# [2, 4, 6, 8, 10]
```

## Multiple Iterables with `map()`

`map()` can also work with multiple iterables, assuming the function can take multiple inputs:

```python
list1 = [1, 2, 3]
list2 = [10, 20, 30]

result = list(map(lambda x, y: x + y, list1, list2))
print(result)
# [11, 22, 33]
```

## Advantages of Using `map()`

1. Readability: `map()` can make our code more concise and easier to read, especially for simple operations on iterables.
2. Memory Efficiency: `map()` returns an iterator, which means it *doesn't create the entire result list in memory at once*. This can be beneficial when working with large datasets.
3. Functional Programming: `map()` encourages functional programming style, which can lead to more maintainable and testable code.

## When to use `map()`

Use `map()` when:

- We need to apply a function to every item in an iterable.
- We want to transform data without explicitly writing a for loop.
- We're working with large datasets and want to avoid creating intermediate lists.

## Alternatives to `map()`

While `map()` is powerful, there are also alternatives:

1. List Comprehensions: Often more readable for simple operations.

```python
doubled = [x * 2 for x in numbers]
```

2. Generator Expressions: Similar to list comprehensions but return an **iterator**.

```python
doubled = (x * 2 for x in numbers)
```

3. **For Loops**: More verbose but sometimes clearer for complex operations.

```python
doubled = []

for x in numbers:
	doubled.append(x *2)
```

## Best Practices

- Use `map()` when it makes your code more readable and concise.
- For complex operations, consider using a regular function instead of a lambda.
- Remember that `map()` returns an iterator. If you need a list, wrap it with `list()`.
- When working with multiple iterables, ensure they have the same length to avoid unexpected results.

## Wrapping Up

The `map()` function is a powerful tool in Python for applying a function to every item in an iterable. It’s particularly useful for data transformation tasks and can lead to more concise and functional code. However, like any tool, it’s important to use it judiciously. Sometimes a list comprehension or a simple for loop might be more appropriate.

Practice using `map()` in your Python programs. Try rewriting some of your existing loops as `map()` operations, and experiment with different functions and iterables. As you gain more experience, you’ll develop a better sense of when `map()` is the right tool for the job.

# Files

## Reading a File

Computers use filesystems to store and retrieve data. Each file is an individual container of related information. If you've ever saved a document, downloaded a song, or even sent an email you've created a file on some computer somewhere. Even **script.py**, the Python program you're editing in the environment, is a file. 

So, how do we interact with files using Python? We're going to learn how to read and write different kinds of files using code. Let's say we had a file called **real_cool_document.txt** with these contents:

```
Wowsers!
```

We could real the file like this:

```python
with open('real_cool_document') as cool_doc:
	cool_contents = cool_doc.read()
print(cool_contents)
```

This opens a file object called `cool_doc` and creates a new indented block where you can read the contents of the opened file. We then read the contents of the file `cool_doc` using `cool_doc.read()` and save the resulting string into the variable `cool_contents`. Then we print `cool_contents`, which outputs the statement `Wowsers!`.

## Iterating Through Lines

When we read a file, we might want to grab the whole document in a single string, like `.read()` would return. But what if we wanted to store each line in a variable? We can use the `.readlines()` function to read a text file line by line instead of having the whole thing. Suppose we have a file:

**keats_sonnet.txt**

```
To one who has been long in city pent,
’Tis very sweet to look into the fair
And open face of heaven,—to breathe a prayer
Full in the smile of the blue firmament.
```

**script.py**

```python
with open('keats_sonnet') as keats_sonnet:
	for line in keats_sonnet.readlines():
		print(line)
```

> The above script creates a temporary file object called `keats_sonnet` that points to the file **keats_sonnet.txt**. It then iterates over each line in the document and prints the entire file out.

1. Using a `with` statement, create a file object pointing to the file **how_many_lines.txt**. Store that file object in the variable `lines_doc`.

```python
with open('how_many_lines.txt') as lines_doc:
  for line in lines_doc:
    print(line)
```


2. Iterate through each of the lines in `lines_doc.readlines()` using a `for` loop.
	Inside the for loop print out each line of **how_many_lines.txt**.

## Reading a Line

Sometimes you don't want to iterate through a whole file. For that, there's a different file method, `.readline()`, which will *only read a single line at a time*. If the entire document is read line by line in this way subsequent calls to `.readline()` will not throw an error but will start returning an empty string (`""`). Suppose we had this file:

**millay_sonnet.txt**

```
I shall forget you presently, my dear,
So make the most of this, your little day,
Your little month, your little half a year,
Ere I forget, or die, or move away,
```

**script.py**

```python
with open('millay_sonnet.txt') as sonnet_doc:  
	first_line = sonnet_doc.readline()  
	second_line = sonnet_doc.readline()  
	print(second_line)
```

This script also creates a file object called `sonnet_doc` that points to the file `millay_sonnet.txt`. It then reads in the first line using `sonnet_doc.readline()` and saves that to the variable `first_line`. It then saves the second line (`So make the most of this, your little day,`) into the variable `second_line` and then prints it out.

## Writing a File

Reading a file is all well and good, but what if we want to create a file of our own? With Python we can do just that. It turns out that our `open()` function that we're using to open a file to read needs another argument to open a file to write to. 

**script.py**

```python
with open('generated_file.txt', 'w') as gen_file:
	gen_file.write("What an incredible file!")
```

Here we pass the argument `'w'` to `open()` in order to indicate to open the file in write-mode. The default argument is `r` and passing `'r'` to `open()` opens the file in read-mode as we've been doing. 

This code creates a new file in the same folder as *script.py* and gives it the text `What an incredible file!`. It's important to note that if there is already a file called *generated_file.txt* it will completely overwrite that file, erasing whatever its contents were before. 

## Appending a File

So maybe completely deleting and overwriting existing files is something that bothers you. Isn't there a way to just add a line to a file without completely deleting it? Of course there is. Instead of opening the file using the argument `'w'` for write mode, we open it with `'a'` for append-mode. If we have a generated file with the following contents:

**generated_file.txt**

```
This was a popular file...
```

Then we can add another line to that file with the following code:

**script.py**

```python
with open('generated_file.txt', 'a') as gen_file:
	gen_file.write("\n... and it still is")
```

In the code above we open a file object in the temporary variable `gen_file`. This variable points to the file *generated_file.txt* and, since it's open in append-mode, adds the string `\n... and it still is` to the file. The newline character `\n` moves to the next line before adding the rest of the string. If you were to open the file after running the script it would look like this:

**generated_file.txt**

```
This was a popular file...
... and it still is
```

Notice that opening the file in append-mode, with `'a'` as an argument to `open()`, means that using the file object's `.write()` method *appends* whatever is passed to the end of the file. If we were to run **script.py** again, this would be what **generated_file.txt** looks like:

**generated_file.txt**

```
This was a popular file...
... and it still is
... and it still is
```

Notice that we've appended `"\n... and it still is"` to the file a second time! This is because in **script.py** we opened **generated_file.txt** in append-mode.

## What's With "with"?

We've been opening these files with this `with` block so far, but it seems a little weird that we can only use our file variable int he indented block. Why is that? The `with` keyword invokes something called a *context manager* for the file that we're calling `open()` on. This context manager takes care of opening the file when we call `open()` and then closing the file after we leave the indented block.

Why is closing the file so complicated? Well, most mother aspects of our code deal with that Python itself controls. All the **variables** you create: integers, lists, dictionaries - these are all Python objects, and Python knows how to clean them up with it's done with them. Since your files exist *outside* your Python script, we need to tell Python when we're done with them so that it can close the connection to that file. Leaving a file connection open unnecessarily can affect performance or impact other programs on our computer that might be trying to access that file.

The `with` syntax replaces older ways to access files where you need to call `.close()` on the file object manually. We can still open up a file and append to it with the old syntax, as long as we remember to close the file connection afterwards.

```python
fun_cities_file = open('fun_cities.txt', 'a')

# We can now append a line to "fun_cities".
fun_cities_file.write("Montreal")

# But we need to remember to close the file
fun_cities_file.close()
```

In the above script we added "Montreal" as a new line in our file **fun_cities.txt**. However, since we used the older-style syntax, we had to remember to close the file afterwards. Since this is necessarily more verbose (requires at least one more line of code) without being any more expressive, using `with` is preferred. 

## What is a CSV File?

Text files aren't the only thing that Python can read, but they're the only thing that we don't need any additional parsing library to understand. CSV files are an example of a text file that *impose a structure* to their data. CSV stand for *Comma-Separated Values* and CSV files are usually the way that data from spreadsheet software (like Microsoft Excel or Google Sheets) is exported into a portable format. A spreadsheet that looks like the following:

![](https://i.imgur.com/1zfJw5p.png)

> In a CSV file that same exact data would be rendered like this:

**users.csv**

```
Name,Username,Email
Roger Smith,rsmith,wigginsryan@yahoo.com
Michelle Beck,mlbeck,hcosta@hotmail.com
Ashley Barker,a_bark_x,a_bark_x@turner.com
Lynn Gonzales,goodmanjames,lynniegonz@hotmail.com
Jennifer Chase,chasej,jchase@ramirez.com
Charles Hoover,choover,choover89@yahoo.com
Adrian Evans,adevans,adevans98@yahoo.com
Susan Walter,susan82,swilliams@yahoo.com
Stephanie King,stephanieking,sking@morris-tyler.com
Erika Miller,jessica32,ejmiller79@yahoo.com
```

Notice that the first row of the CSV file doesn't actually represent any data, just the labels of the data that's present in the rest of the file. The rest of the rows of the file are the same as the rows in the spreadsheet software, just instead of being separated into different cells they're separated by... well I suppose it's fair to say they're separated by commas.

## Reading a CSV File

Recall our CSV file from our last exercise:

**users.csv**

```
Name,Username,Email
Roger Smith,rsmith,wigginsryan@yahoo.com
Michelle Beck,mlbeck,hcosta@hotmail.com
Ashley Barker,a_bark_x,a_bark_x@turner.com
Lynn Gonzales,goodmanjames,lynniegonz@hotmail.com
```

Even though we can read these lines as text without a problem, there are ways to access the data in a format better suited for programming purposes. In Python we can convert that data into a dictionary using the `csv` library's `DictReader` object. Here's how we'd create a list of the email addresses of all the users in the above table:

```python
import csv

list_of_email_addresses = []
with open('users.csv', newline='') as users_csv:
	user_reader = csv.DictReader(users_csv)
	for row in user_reader:
		list_of_email_addresses.append(row['Email'])
```

In the above code:

- We first import our `csv` library, which gives us the tools to parse our CSV file.
- We then create the empty list `list_of_email_addresses` which we'll later populate with the email addresses from our CSV. 
- Then we open the **users.csv** file with the temporary variable `users_csv`. 
- We pass the additional keyword argument `newline=''` to the file opening `open()` function so that we don't accidentally mistake a line break in one of our data fields asa  new row in our in our CSV (read more about this in [the Python documentation](https://docs.python.org/3/library/csv.html#id3)) 
- After opening our new CSV file we use `csv.DictReader(users_csv)` which converts the lines of our CSV file to Python dictionaries which we can use access methods for.

The keys of the dictionary are, by default, the entries in the first line of our CSV file. Since our CSV's first line calls the third field in our CSV file. Since our CSV's first line calls the third field in our CSV `Email`, we can use that as the key in each row of our DictReader.

When we iterate through the rows of our `user_reader` object, we access all of the rows in our CSV file as dictionaries (except for the first row, which we used to label the keys of our dictionary). By accessing the `'Email'` key of each of these rows we can grab the email address in that row and append it to our list `list_of_email_addresses`.

## Reading Different Types of CSV Files

I need to level with you, I've been lying to you for the past two exercises. Well, kind of. We've been acting like CSV files are Comma-Separated Values files. It's true that CSV stands for that, but it's also true that other ways of separating values are valid CSV files these days.

People used to call Tab-Separated Values files TSV files, but as other separators grew in popularity everyone realized that creating a new `.[a=z]sv` file format for value-separating character used is not sustainable.

So we call all files with a list of different values a CSV file and then use different *delimiters* (like a comma or a tab) to indicate where the different values start and stop.

Let's say we had an address book. Since addresses usually use commas in them, we'll need to use a different delimiter for our information. Since non of our data has semicolons(`;`) in them, we can use those.

```
Name;Address;Telephone
Donna Smith;126 Orr Corner Suite 857\nEast Michael, LA 54411;906-918-6560
Aaron Osborn;6965 Miller Station Suite 485\n
North Michelle, KS 64364;815.039.3661x42816
Jennifer Barnett;8749 Alicia Vista Apt. 288\n Lake Victoriaberg, TN 
51094;397-796-4842x451
Joshua Bryan;20116 Stephanie Stravenue\nWhitneytown, IA 87358;(380)074-6173Andrea Jones;558 Melissa Keys Apt. 588\nNorth Teresahaven, WA 63411;+57(8)7795396386
Victor Williams;725 Gloria Views Suite 628\nEast Scott, IN 38095;768.708.3411x954
```

Notice the `\n` character, this is the escape sequence for a new line. The possibility of a new line escaped by a `\n` character in our data is why we pass the `newline=''` keyword argument to the `open()` function.

Also notice that many of these addresses have commas in them! This is okay, we'll still be able to read it. If we wanted to, say, print out all the addresses in this CSV file we could do the following:

```python
import csv

with open('addresses.csv', newline='') as addresses.csv:
	address_reader = csv.DictReader(addresses_csv, delimiter=';')
	for row in address_reader:
		print(row['Address'])
```

Notice that when we call `csv.DictReader` we pass in the `delimiter` parameter, which is the string that's used to delineate separate fields in the CSV. We then iterate through the CSV and print out each of the addresses.

> [!NOTE]
> Create a list called `isbn_list`, iterate through `books_reader` to get the ISBN number of every book in the CSV file. Use the `['ISBN']` key for the dictionary objects passed to it.

```python
import csv

with open('books.csv') as books_csv:
  books_reader = csv.DictReader(books_csv, delimiter='@')
  isbn_list = [book['ISBN'] for book in books_reader]
```

## Writing a CSV File

Naturally if we have the ability to read different CSV files we might want to be able to programmatically create CSV files that save output and data that someone could load into their spreadsheet software. Let's say we have a big list of data that we want to save into a CSV file. We could do the following:

```python
big_list = [{'name': 'Fredrick Stein', 'userid': 6712359021, 'is_admin': False}, {'name': 'Wiltmore Denis', 'userid': 2525942, 'is_admin': False}, {'name': 'Greely Plonk', 'userid': 15890235, 'is_admin': False}, {'name': 'Dendris Stulo', 'userid': 572189563, 'is_admin': True}] 

import csv

with open('output.csv', 'w') as output_csv:
	fields = ['name', 'userid', 'is_admin']
	output_writer = csv.DictWriter(output_csv, fieldnames=fields)

	output_writer.writeheader()
	for item in big_list:
		output_writer.writenow(item)
```

In the above code we:

- Had a set of dictionaries with the same keys for each, a prime candidate for a CSV. 
- We import the `csv` library, and then open a new CSV file in write-mode by passing the `'w'` argument to the `open()` function.
- We then define the fields we're going to be using into a variable called `fields`. 
- We then instantiate our CSV writer object and pass two arguments. 
	- The first is `output_csv`, the file handler object.
	- The second is our list of fields `fields` which we pass to the keyword parameter `fieldnames`.

Now that we've instantiated our CSV file writer, we can start adding lines to the file itself. First we want the headers, so we call `.writeheader()` on the writer object. This writes all the fields passed to `fieldnames` as the first row in our file. Then we iterate through our `big_list` of data. Each `item` in `big_list` is a dictionary with each field in `fields` as the keys. We call `output_writer.writerow()` with the `item` dictionaries which writes each line to the CSV file.

## Reading a JSON File

CSV isn't the only file format that Python has a built-in library for. We can also use Python's file tools to read and write [JSON](https://www.codecademy.com/resources/docs/python/json-module?page_ref=catalog). JSON, an abbreviation of JavaScript Object Notation, is a file format inspired by the programming language JavaScript. The name, like CSV is a bit of a misnomer - some JSON is not valid JavaScript (and plenty of JavaScript is not valid JSON).

JSON's format is endearingly similar to Python dictionary syntax, and so JSON files might be easy to read from a Python developer standpoint. Nonetheless, Python comes with a `json` package that will help us parse JSON files into actual Python dictionaries. Suppose we have a JSON file like the following:

```JSON
{
	'user': 'ellen_greg'
	'action': 'purchase'
	'item_id': '14781239'
}
```

> We would be able to read that in a Python dictionary with the following code:

**json_reader.py**

```Python
import json

with open('purchase_14781239.json') as purchase_json:
	purchase_data = json.load(purchase_json)

print(purchase_data['user'])
#prints 'ellen_greg'
```

First we import the `json` package. We opened the file using our trusty `open()` command. Since we're opening it in read-mode we just need to pass the file name. We save the file in the temporary variable `purchase_json`.

We continue by parsing `purchase_json` using `json.load()`, creating a Python dictionary out of the file. Saving the results into `purchase_data` means we can interact with it. We print out one of the values of the JSON file by keying into the `purchase_data` object.

## Writing a JSON File

Naturally we can use the `json` library to translate Python objects to JSON as well. This is especially useful in instances where you're using a Python library to serve web pages, you would also be able to serve JSON. Let's say we had a Python dictionary we wanted to save as a JSON file:

```python
turn_to_json = {
	'eventId': 674189,
	'dateTime': '2015-02-12T09:23:17.611Z',
	'chocolate': 'Semi-sweet Dark',
	'isTomatoAFruit': True
	}
```

We'd be able to create a JSON file with that information by doing the following:

```python
import json

with open('output.json', 'w') as json_file:
	json.dump(turn_to_json, json_file)
```

We import the `json` module, open up a write-mode file under the variable `json_file`, and then use the `json.dump()` method to write to the file. `json.dump()` takes two arguments: the first data object, then the file object you want to save.

## Review

Now you know all about files! You were able to:

- Open up file objects using [`open()`](https://www.codecademy.com/resources/docs/python/built-in-functions/open) and `with`.
- Read a file’s full contents using Python’s `.read()` method.
- Read a file line-by-line using [`.readline()`](https://www.codecademy.com/resources/docs/python/files/readline) and `.readlines()`
- Create new files by opening them in write-mode.
- Append to a file non-destructively by opening a file in append-mode.
- Apply all of the above to different types of data-carrying files including CSV and JSON!

You have all the skills necessary to read, write, and update files programmatically, a very useful skill in the Python universe!

# Introduction to Classes

## Types

Python equips us with many different ways to store data. A `float` is a different kind of number from an `int`, and we store different data in a list than we do in a `dict`. These are known as different *types*. We can check the type of a Python variable using the `type()` function.

```python
a_string = "Cool String"
an_int = 12

print(type(a_string))
# prints "<class 'str'>"

print(type(an_int))
# prints "<class 'int'>"
```

Above, we defined two variables, and checked the `type` of these two variables. A variable's type determines what you can do with it and how you can use it. You can't `.get()` something from an integer, just as you can't add dictionaries together using `+`. This is because those operations are defined at the `type` level. 

## Class

A class is a **template** for a data type. It describes the kinds of information that class will hold and how a programmer will interact with that data. Define a class using the `class` keyword. [PEP 8 Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#class-names) recommends capitalizing the names of classes to make them easier to identify.

```python
class CoolClass:
	pass
```

In the above example we created a class and named it `CoolClass`. We used the `pass` keyword in Python to indicate that the body of the class was intentionally left blank so we don't cause an `IndentationError`. We'll learn about all the things we can put in the body of a class in the next few exercises.

## Instantiation

A class doesn't accomplish anything simply by being defined. A class must be *instantiated*. In other words, we must create an *instance* of the class, in order to breathe life into the schematic.

Instantiating a class looks a lot like calling a function. We would be able to create an instance of our defined `CoolClass` as follows:

```python
cool_instance = CoolClass()
```

Above, we created an object by adding parentheses to the name of the class. We then assigned that new instance to the variable `cool_instance` for safe-keeping so we can access our instance of `CoolClass` at a later time.

## Object-Oriented Programming

A class instance is also called an *object*. The pattern of defining classes and creating objects to represent the responsibilities of a program is known as [_Object Oriented Programming_](https://www.codecademy.com/resources/docs/general/programming-paradigms/object-oriented-programming?page_ref=catalog) or OOP.

Instantiation takes a class and turns it into an object, the `type()` function does the opposite of that. When called with an object, it returns the class that the object is an instance of.

```python
print(type(cool_instance))
# prints "<class '__main__.CoolClass'>"
```

We then print out the `type()` of `cool_instance` and it shows us that this object is of the type `__main__.CoolClass`.

In Python `__main__` means "this current file that we're running" and so one could read the output from `type()` to mean "the class `CoolClass` that was defined here, in the script you're currently running."

---

**Object-Oriented Programming** is a software development paradigm which encourages sculpting desired entities with properties and methods in named classes to create applications.

OOP relies on two major concepts: **the class and the object** - these foundational concepts applied in code enable us to build applications.

Classes that have been instantiated in our code become objects that can interact with one another perform the desired functions of the application. Object oriented programming was created to guide the creation of better software, by achieving easier maintenance and reusability.

### Principles of OOP

There are four main principles of OOP:

- [**Encapsulation**](https://www.codecademy.com/resources/docs/general/programming-paradigms/encapsulation): A desired outcome of organizing code in classes in order to keep things from being mixed with other unrelated bits of code. Encapsulation makes it easier to reason about code because of the *modularity of code written in object oriented styled classes*.
- [**Inheritance**](https://www.codecademy.com/resources/docs/general/programming-paradigms/inheritance): A principle which allows an instance of an object to borrow attributes and methods from its parent class.
- [**Polymorphism**](https://www.codecademy.com/resources/docs/general/programming-paradigms/polymorphism): The ability of the class to be dynamic in its use of class methods so that objects with the same parent class can make use of these parent class methods.
- **Abstraction**: A principle that highlights the benefit of hiding complex parts of code from other parts in order to make it easier to reason and make decisions about our code.

## Class Variables

When we want the same data to be available to every instance of a class we use a *class variable*. A class variable is a variable that's the same for every instance of the class.

You can define a class variable by including it in the indented part of your class definition, and you can access all of an object's class variables with `object.variable` syntax.

```python
class Musician:
	title = "Rockstar"

drummer = Musician()
print(drummer.title)
#prints "Rockstar"
```

Above we defined the class `Musician`, then instantiated `drummer` to be an object of type `Musician`. We then printed out the drummer's `.title` attribute, which is a class variable that we defined as the string "Rockstar".

If we defined another musician, like `guitarist = Musician()` they would have the same `.title` attribute.

**Note**: Class variables are often referenced with a leading period, like `.title` above. This is done to quickly show that the variable belongs to a class and must be accessed with dot notation, like `drummer.title`.

## Methods

Methods are functions that are defined as part of a class. The first argument in a method is always the object that is calling the method. Convention recommends that we name this first argument `self`. Methods always have at least this one argument. 

We define methods similarly to functions, except that they are intended to be part of the class.

```python
class Dog:
	dog_time_dilation = 7

	def time_explanation(self):
		print("Dogs experience {} years for every 1 human year.".format(self.dog_time_dilation))

pipi_pitbull = Dog()
pipi_pitbull.time_explanation()
# prints "Dogs experience 7 years for every 1 human year."

```

Above we created a `Dog` class with a `.time_explanation()` method that takes one argument, `self`, which refers to the object calling the function. We created a `Dog` named `pipi_pitbull` and called the `.time_explanation()` method on our new object for Pipi.

Notice we didn't pass any arguments when we called `.time_explanation()`, but were able to refer to `self` in the function body. When you call a method it automatically passes the object calling the method as the first argument.

## Methods with Arguments

Methods can also take more arguments than just `self`:

```python
class DistanceConverter:
	kms_in_a_mile = 1.609
	def how_many_kms(self, miles):
		return miles * self.kms_in_a_mile*

converter = DistanceConverter()
kms_in_5_miles = converter.how_many_kms(5)
print(kms_in_5_miles)
# prints "8.045"
```

Above we defined a `DistanceConverter` class, instantiated it, and used it to convert 5 miles into kilometers. Notice again that even though `.how_many_kms()` takes two arguments in its definition, we only pass `miles`, because `self` is implicitly passed (and refers to the object `converter`).
## Constructors

There are several methods that we can define in a Python class that have special behavior. These methods are sometimes called "magic", because they behave differently from regular methods. Another popular term is *dunder methods*, so-named because they have two underscores (double underscores are abbreviated to "dunder") on either side of them.

The first dunder method we're going to use is the `__init__()` method (note the two underscores before and after the word 'init'). This method is used to *initialize* a newly created object. It is called every time the class is instantiated. 

Methods that are used to prepare and object being instantiated are called *constructors*. The word "constructor" is used to describe similar features in other object-oriented programming languages, but programmers who refer to a constructor in Python are usually talking about the `__init__()` method.

```python
class Shouter:
	def __init__(self):
		print("HELLO?!")

shout1 = Shouter()
# prints "Hello?!"

shout2 = Shouter()
# prints "HELLO?!"
```

Above, we created a class called `Shouter` and every time we create an instance of `Shouter` the program prints a shout. Don't worry, this doesn't hurt the computer at all.

Pay careful attention to the instantiation syntax we use. `Shouter()` looks a lot like a function call, doesn't it? If it's a function, we can pass parameters to it? We absolutely can, and those parameters will be received by the `__init__()` method.

```python
class Shouter:
	def __init__(self, phrase):
	# make sure phrase is a string
	if type(phrase) == str:

	# then shout it out
	print(phrase.upper())

shout1 = Shouter("shout")
# prints "SHOUT"

shout2 = Shouter("shout")
# prints "SHOUT"

shout3 = Shouter("let it all out")
# prints "LET IT ALL OUT"
```

Above, we've updated our `Shouter` class to take the additional parameter `phrase`. When we created each of our objects, we passed an argument to the constructor. The constructor takes the argument `phrase` and, if it's a string, prints out the all-caps version of `phrase`.
# Instance Variables

We've learned so far that a class is a schematic for a data type and an object is an instance of a class, but why is there such a strong need to differentiate the two if each object can only have the methods and class variables the class has?

> This is because each instance of a class can hold different kinds of data.

The data held by an object is referred to as an *instance variable*. Instance variables aren't shared by all instances of a class -- they are variables that are **specific to the object they are attached to.**

Let's say that we have the following class definition:

```python
class FakeDict:
	pass
```

We can instantiate two different objects from this class, `fake_dict1` and `fake_dict2`, and assign instance variables to these objects using the same attribute notation that was used for accessing class variables.

```python
fake_dict1 = FakeDict()
fake_dict2 = FakeDict()

fake_dict1.fake_key = "This works!"
fake_dict2.fake_key = "This too!"

# let's join the two strings together!
working_string = "{} {}".format(fake_dict1.fake_key, fake_dict2.fake_key)
print(working_string)
# prints "This works! This too!"
```

# Attribute Functions

Instance variables and class variables are both accessed similarly in Python. This is no mistake, they are both considered *attributes* of an object. If we attempt to access an attribute that is neither a class variable nor an instance variable of the object Python will throw an `AttributeError`

```python
class NoCustomAttributes:
	pass

attributeless = NoCustomAttributes()

try:
	attributeless.fake_attribute
except AttributeError:
	print("This text gets printed!")
```

What if we aren't sure if an object has an attribute or not? `hasattr()` will return `True` if an object has a given attribute and `False` otherwise. If we want to get the actual value of the attribute, `getattr()` is a Python function that will return the value of a given object and attribute. In this function, we can also supply a third argument that will be the default if the object does not have the given attribute. 

The syntax and parameters for these functions look like this:

`hasattr(object, "attribute")` has two parameters:

1. *object*: the object we are testing to see if it has a certain attribute
2. *attribute*: name of the attribute we want to see if it exists

`getattr(object, "attribute", default)` has three parameters (one of which is optional):

1. *object*: the object whose attribute we want to evaluate
2. *attribute*: name of attribute we want to evaluate
3. *default*: the value that is returned if the attribute does not exist (note: this parameter is **optional**)

Calling those functions looks like this:

```python
hasattr(attributeless, "fake_attribute")
#returns false

getattr(attributeless, "other_fake_attribute", 800)
# returns 800, the default value
```

Above:

1. We checked if the `attributeless` object has the attribute `.fake_attribute`. Since it does not, `hasattr()` returned `False`. 
2. After that, we used `getattr` to attempt to retrieve `.other_fake_attribute`.
3. Since `.other_fake_attribute` isn't a real attribute on `attributeless`, our call to `getattr()` returned the supplied default value `800`, instead of throwing an `AttributeError`.

### Questions:

1. In **script.py** we have a list of different data types: a dictionary, a string, an integer, and a list all saved in the variable `can_we_count_it`.

1. For every `element` in `can_we_count_it`, check if the element has the attribute `.count` using the `hasattr()` function. If so, print the following line of code:

```python
print(str(type(element)) + " has the count attribute!")
```
```python
can_we_count_it = [{'s': False}, "sassafrass", 18, ["a", "c", "s", "d", "s"]]

for element in can_we_count_it:
	if hasattr(element, "count"):
		print(str(type(element)) + " has the count attribute!")
```
```
<class 'dict'> does not have the count attribute :(
<class 'str'> has the count attribute!
```

2. Now let's add an `else` statement for the elements that do not have the attribute `.count`. In this `else` statement add the following line of code:

```python
print(str(type(element)) + " does not have the count attribute :(")
```
```python
can_we_count_it = [{'s': False}, "sassafrass", 18, ["a", "c", "s", "d", "s"]]

for element in can_we_count_it:
	if hasattr(element, "count"):
		print(str(type(element)) + " has the count attribute!")
	else:
		print(str(type(element)) + " does not have the count attribute :(")
```
```
<class 'int'> does not have the count attribute :(
<class 'list'> has the count attribute!
```

3. Let's go over the terminal output of the past two instructions. You should see the following output in your terminal right now:

```
<class 'dict'> does not have the count attribute :(
<class 'str'> has the count attribute!
<class 'int'> does not have the count attribute :(
<class 'list'> has the count attribute!
```

This is because *dictionaries* and *integers* both do not have a `.count` attribute, while strings and lists do. 

In this exercise, we have iterated through `can_we_count_it` and used `hasattr()` to determine which elements have a `.count()` method, but you can read more about it [here](https://www.codecademy.com/resources/docs/python/lists/count?page_req=catalog)
if you are curious about what it is.

Click run to move onto the next exercise.
## Self

Since we can already use dictionaries to store key-value pairs, using objects for that purpose is not really useful. Instance variables are more powerful when you can guarantee a rigidity to the data the object is holding.

This convenience is most apparent when the constructor creates the instance variables using the arguments passed into it. If we were creating a search engine and wanted to create a class to hold each search entry, we could do so like this:

```python
class SearchEngineEntity:
	def __init__(self, url):
		self.url = url

codecademy = SearchEngineEntity("www.codecadeny.com")
wikipedia = SearchEngineEntity("www.wikipedia.org")

print(codecademy.url)
# print "www.codecademy.com"

print(wikipedia.url)
# print "www.wikipedia.org"
```

In the preceding code sample, we define a `SearchEngineEntity` class, which contains a constructor with two parameters, `self` and `url`. Inside the constructor body, we create an instance variable named `self.url` and assign it the value of the `url` parameter that is passed into the constructor.

We then create the `codecademy` instance of `SearchEngineEntity` by passing the URL as an argument to the constructor. After `codecademy` is defined, printing `codecademy.url` shows that the URL has been assigned to the `url` instance variable of `codecademy`. Similarly, `wikipedia.url` holds the value that was passed into the constructor when `wikipedia` was defined. 

Since the `self` keyword refers to the object and not the class being called, we can define a `.secure()` method on the `SearchEngineEntity` class that returns the secure link to an entry.

```python
class SearchEngineEntry:
	secure_prefix = "https://"
	def __init__(self, url):
		self.url = url

	def secure(self):
		return "{prefix{site}}".format)prefix=self.secure.prefix,sire=self.url)

codecademy = SearchEngineEntry("www.codecademy.com")
wikipedia = SearchEngineEntry("www.wikipedia.com")

print(codecademy.secure())
# prints "https://codecademy.com"

print(wikipedia.secure())
# prints "https://www.wikipedia.org"
```

Above:

1. We define our `.secure()` method to take just the one *required argument*, `self`.
2. We access both the class variables `self.secure_prefix` and the instance variable `self.url` to return a secure URL.

This is the strength of writing object-oriented programs. We can write our classes to structure the data that we need and write methods that will interact with that data in a meaningful way.
# Everything is an Object

Attributes can be added to user-defined objects after instantiation, so it's possible for an object to have some attributes that are not explicitly defined in an object's constructor. We can use the `dir()` function to investigate an object's attributes at runtime. `dir()` is short for *directory* and offers an organized presentation of object attributes.

```Python
class FakeDict:
  pass

fake_dict = FakeDict()
fake_dict.attribute = "Cool"

print(dir(fake_dict))
```

That's certainly a lot more attributes than we defined! Python *automatically adds a number of attributes to all objects that get created*. These internal attributes are usually indicated by double-underscores. But sure enough, `attribute` is in that list. 

Do you remember being able to use `type()` on Python's native data types? This is because they are also objects in Python. Their classes are `int`, `float`, `str`, `list`,  and `dict`. These Python classes have special syntax for their instantiation, `1`, `1.0`, `"hello"`, `[]`,  and `{}` specifically. But these instances are still full blown objects to Python.

```python
fun_list = [10, "string", {'abc': True}]

type(fun_list)
# Prints <class 'list'>

print(dir(fun_list))
# Prints ['__add__', '__class__', [...], 'append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']
```

Above we define a new list. We check it's type and see that it's an instantiation of class `list`. We use `dir()` to explore its attributes, and it gives us a large number of internal Python dunder attributes, but afterward, we get the usual list methods.
# String Representation

One of the first things we learned as programmers is how to print out information that we need for debugging. Unfortunately, when we print out an object we get a default representation that seems fairly useless.

```python
class Employee():  
    def __init__(self, name):    
        self.name = nameargus = Employee("Argus Filch")
        
print(argus)
# prints "<__main__.Employee object at 0x104e88390>"
```

This default string representation gives us some information, like where the class is defined and our computer's memory address where this object is stored, but is usually not useful information to have when we are trying to debug our code. 

We learned about the dunder method `__init__()`. Now, we will learn another dunder method called `__repr__()`. This is a method we can use to tell Python what we want the *string representation* of the class to be. `__repr__()` can only have one parameter, `self`, and must return a string.

In our `Employee` class above, we have an instance variable called `.name` that should be unique enough to be useful when we're printing out an instance of the `Employee` class.

```python
class Employee():  
    def __init__(self, name):    
        self.name = name
	def __repr__(self):
		return self.name

argus = Employee("Argus Finch")
print(argus)
# prints "Argus Finch"
```

We implemented the `__repr__()` method and had it return the `.name` attribute of the object. When we printed the object out it simply printed the `.name` of the object. Cool!

# Review




