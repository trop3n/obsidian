

---
# Lists

A natural way to organize and store data is in a `List`. Some languages call them "arrays", but in Python we just call them lists. Think of all the apps you use and how many of the items int he app are organized into lists. 

For example:

- A Twitter feed is a list of posts
- An online store is a list of products
- The state of a chess game is a list of moves
- This list is a list of things that are lists

Lists in Python are declared using **square brackets**, with commas separating each item:

```python
inventory = ["Iron Breastplate", "Healing Potion", "Leather Scraps"]
```

Lists can contain items of any data type, in our example above we have a `List` of strings.
## Lists Continued

Sometimes when we're manually creating lists it can be hard to read if all the items are on the same line of code. We can declare the list when using multiple lines if we want to:

```python
flower_types = [
	"daffodil",
	"rose",
	"chrysanthemum"
]

player_ages = [
	23,
	18,
	31,
	42
]
```

Keep in mind this is just a styling change. The code will run correctly either way.
# Counting in Programming

In the world of programming, counting is a bit strange!

We don't just start counting at `1`, we start at `0` instead.
## Indexes

Each item in a list has an index that refers to its spot in the list.

Take the following example list:

```python
names = ["Bob", "Lane", "Alice", "Breanna"]
```

- Index 0: `Bob`
- Index 1: `Lane`
- Index 2: `Alice`
- Index 3: `Breanna`
# Indexing into Lists

Now that we know how to create new lists, we need to know how to access specific items in a list.

We access items in a list directly by using their *index*. Indexes start at 0 (the first item) and increment by one with each successive item. The syntax is as follows:

```python
best_languages = ["JavaScript", "Go", "Rust", "Python", "C"]
print(best_languages[1])
# prints "Go", because index 1 was provided.
```
## List Length

The length of a list can be calculated with the `len()` function.

```python
fruits = ["apple", "banana", "pear"]
length = len(fruits)
```

The length of the list is equal to the number of items present. Don't be fooled by the fact that the length is *not equal to the index of the last element*, in fact, it will always be one greater.
## List Updates

We can also change the item that exists at a given index. For example, we can change `Leather` to `Leather Armor`. in the `inventory` list in the following way:

```python
inventory = ["Leather", "Iron Ore", "Healing Potion"]
inventory[0] = "Leather Armor"
# inventory: ['Leather Armor', 'Iron Ore', 'Healing Potion']
```
# Appending in Python

It's common to create an empty list then fill it with values using a loop. We can add values to the end of a list using the `.append()` method:

```python
cards = []
cards.append("nvidia")
cards.append("amd")
# the cards list is now ['nvidia', 'amd']
```
## Pop Values

`.pop()` is the opposite of `.append()`. Pop removes the last element from a list and returns it for use. For example: 

```python
vegetables = ["broccoli", "cabbage", "kale", "tomato"]
last_vegetable = vegetables.pop()
# vegetables = ['broccoli', 'cabbage', 'kale']
# last_vegetable = 'tomato'
```

> [!NOTE] Note
> While `.pop()` typically removes the last item of a list, it can also be used to remove an item at a specific index. For example, `vegetables.pop(1)` would remove 'cabbage' from the list. This can be useful when you need to remove items from other positions in your list.
## Counting Items in a List

Remember that we can iterate over all the elements in a list using a loop. For example, the following code will print each item in the `sports` list.

```python
for i in range(0, len(sports)):
	print(sports[i])
```
# No-Index Syntax

In my opinion, Python has *the most elegant* syntax for iterating directly over the items in a list without worrying about index numbers. If you don't need the index number you can use the following syntax:

```python
trees = ['oak', 'pine', 'maple']
for tree in trees:
	print(tree)
# prints:
# oak
# pine
# maple
```

`tree`, the variable declared using the `in` keyword, directly accesses the value in the list rather than the index of the value. If we don't need to update the item and only need to access its value then this is a more clean way to write the code. 
## Find an Item in a List

Practice the "no-index" or "no-range" syntax:

```python
for fruit in fruits:
	print(fruit)
```
# Find Max

The built-in `float()` function can create a numeric floating point value of negative infinity. Because *every value* will be greater than negative infinity, we can use it to help us accomplish our goal of finding the max value. 

```python
negative_infinity = float("-inf")
positive_infinity = float("inf")
```
# Modulo Operator in Python
## The Modulo Operator Can be Used to Find a Remainder

For example, `7` modulo `2` would be `1`, because 2 can be multiplied evenly into 7 at most three times:

```
2 * 3 = 6
```

Then there is 1 *remaining* to get from `6` to `7`.

```
7 - 6  = 1
```

The modulo operator is the percent sign: `%`. It's important to recognize modulo is *not* a percentage though! That's just the symbol we're using.

```
remainder = 8 % 3
# remainder 2
```

An odd number is a number that when divided by `2`, the remainder is *not* `0.

```python
def get_odd_numbers(num):
    odd_numbers = []

    for i in range(0, num):
        # don't touch above this line
        if i % 2 != 0:
            odd_numbers.append(i)

    # don't touch below this line

    return odd_numbers`
```
# Slicing Lists

Python makes it easy to slice and dice lists to work only with the section you care about. One way to do this is to use the simple slicing operator, which is just a colon `:`.

With this operator, you can specify where to start and end the slice, and how to step through the original list. List slicing returns a *new list* from the existing list. 

The syntax is as follows:

```python
my_list[ start : stop : step ]
```

For example:

```python
scores = [50, 70, 30, 20, 90, 10, 50]
# display list
print(scores[1:5:2])
# Prints [70, 20]
```

The above reads as "give me a slice of the `scores` list from index 1, up to but not including 5, skipping every 2nd value. *All of the sections are optional*".
## Omitting Sections

You can also omit various sections ("start", "stop", or "step"). For example, `numbers[:3]` means "get all items from the start up to (but not including) index 3". `numbers[3:]` means "get all items from index 3 to the end".

```python
numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
numbers[:3] # Gives [0, 1, 2]
numbers[3:] # Gives [3, 4, 5, 6, 7, 8, 9]
```
## Using Only the Step Section

```Python
numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
numbers = [-3:] # Gives [7, 8, 9]
```
## Assignment

Complete the given `get_champion_slices` function. It takes a list of `champions` and should return three new lists based on the given champions:

1. First, return a slice of the `champions` list that starts with the third champion and goes to the end of the list.
2. Next, return a slice of the `champions` list that starts at the beginning of the list and ends with the third champion from the end (inclusive).
3. Last, return a slice of the `champions` list that only includes the champions in even numbered indexes.
### Successful Code

```python
def get_champion_slices(champions):
    return champions[2:], champions[0:-2], champions[0::2]
```
# List Operations - Concatenate

Concatenating two lists (smushing them together) is easy in Python, just use the `+` operator. 

```python
total = [1, 2, 3] + [4, 5, 6]
print(total)
# prints: [1, 2, 3, 4, 5, 6]
```
## Assignment

Fantasy Quest allows users to keep lists of their favorite items. Your job is to finish the `concatenate_favorites` function. It takes three different lists - the player's `favorite_weapons`, `favorite_armor` and `favorite_items`.

1. Create a new list that combines the lists `favorite_weapons`, `favorite_armor`, and `favorite_items` in this order.
2. Return the list containing the combined favorites.

```python
def concatenate_favorites(favorite_weapons, favorite_armor, favorite_items):
    favorites = favorite_weapons + favorite_armor + favorite_items
    return favorites
```
# List Operations - Contains

Checking whether a value exists in a list is also really easy in Python, just use the `in` keyword. 

```python
fruits = ["apple", "orange", "banana"]
print("banana" in fruits)
# Prints: True
```
## Assignment

Our players have requested an in-game feature that will allow them to type in a weapon name to check if it's in the list of top weapons in the realm.

Complete the `is_top_weapon` function. It should return `True` if the `weapon` is in the `top_weapons` list, otherwise it should return `False`.

```python
def is_top_weapon(weapon):
    top_weapons = [
        "sword of justice",
        "sword of slashing",
        "stabby daggy",
        "great axe",
        "silver bow",
        "spellbook",
        "spiked knuckles",
    ]

    # don't touch above this line
    if weapon in top_weapons:
        return True
    else:
        return False
```
# List Deletion

Python has a built-in keyword `del` that deletes items from objects. In the case of a list, you can delete specific indexes or entire slices. 

```python
nums = [1, 2, 3, 4, 5, 6, 7, 8, 9]

# delete the fourth item
del nums[3]
print(nums)
# Output: [1, 2, 3, 5, 6, 7, 8 ,9]

# delete the second item up to (but not including) the fourth item
nums = [1, 2, 3, 4, 5, 6, 7, 8, 9]
del nums[1:3]
print(nums)
# Output: [1, 4, 5, 6, 7, 8, 9]

# delete all elements
nums = [1, 2, 3, 4, 5, 6, 7, 8, 9]
del nums[:]
print(nums)
# Output: []
```
## Assignment

In Fantasy Quest there is a list of strongholds on the map that players can visit to defeat powerful bosses. Let's update the `trim_strongholds` function to:

1. Delete the first stronghold from the list
2. Delete the last two strongholds from the list
# Tuples

Tuples are collections of data that are ordered and unchangeable. You can think of a tuple as a `list` with a fixed size. Tuples are created with rounded brackets:

```python
my_tuple = ("this is a tuple", 45, True)
print(my_tuple[0])
# this is a tuple
print(my_tuple[1])
# 45
print(my_tuple[2])
# True
```

While it's typically considered bad practice to store items of different types in a List, it's not a problem with Tuples. Because they have a fixed size, it's easy to keep track of which indexes store which types of data.

Tuples are often used to store very small groups (like 2 or 3 items) of data. For example, you might use a tuple to store a dog's name and age. 

```python
dog = ("Fido", 4)
```

Note: There is a special case for creating single-item tuples. You must include a comma so Python knows it's a tuple and not regular parentheses.

```python
dog = ("Fido",)
```

Because Tuples hold their data, multiple tuples can be stored within a list. Similar to storing other data in lists, each tuple within the list is separated by a comma. When accessing a list of tuples, the first index selects which tuple you want to access, the second selects a value *within* that tuple.

```python
my_tuples = [("this is the first tuple in the list", 45, True),("this is the second tuple in the list", 21, False)]
print(my_tuples[0][0]) # this is the first tuple in the list
print(my_tuples[0][1]) # 45
print(my_tuples[1][0]) # this is the second tuple in the list
print(my_tuples[1][2]) # False
```
## Tuple Unpacking

You can easily assign the values of a tuple to variables using unpacking.

```python
dog = ("Fido", 4)
dog_name, dog_age = dog
print(dog_name)
# Fido
print(dog_age)
# 4
```

When you assign multiple values from a function, you're actually returning a tuple. 
## Assignment

The "Fantasy Quest" character system needs a list of "heroes" to be able to run the game properly. Someone wrote some pretty nasty code, and the code in question creates a `heroes` list where every 3rd index defines a new hero. First their name, then their age, then whether or not they're an "elf".

Change the heroes list declaration from its current state to a _list of tuples_. Use the same data for each hero, and order it in the same way.
### Successful Code

```python
def get_heroes():
    heroes = [(
        "Glorfindel",
        2093,
        True),
        ("Gandalf",
        1054,
        False),
        ("Gimli",
        389,
        False),
        ("Aragorn",
        87,
        False),
    ]

    return heroes
```
# First Element

## Assignment

Let's add another function to our inventory system. Write a function that returns the first element from a list. If the list is empty then return the string `ERROR` instead.
### Successful Code

```python
def get_first_item(items):
    if items == []:
        return "ERROR"
    else:
        return items[0]
```
# Reverse List

Some of our players would like to view their inventories in reverse order.

Let's write a function that takes a list as an input and returns a new list except all the items that are in reverse order.

For example:

```
[1, 2, 3] -> [3, 2, 1]
['a', 'b', 'c', 'd'] -> ['d', 'c', 'b', 'a']
```
## Tip

The Python [range](https://docs.python.org/3/library/stdtypes.html#ranges) function is very useful when working with lists.

- Where should you start your loop from?
- Where should you end your loop?
- What should the step be? In other words, how should you increment `i` in each iteration of the loop?
### Successful Code

```python
def reverse_array(items):
    rev = items[::-1]
    return rev
```
# Filter Messages

You are about to write a bit more code in a single function than you have before. 

Do *not* try to write it all at once. Start with the outermost loop, and work your way inwards. Add extra `print()` statements and run your code often to make sure it's doing what you expect. Just make sure to remove extra `print()` statements before submitting your code.

Running your code often to make sure each line is doing what you expect is called "debugging". All programmers, even seasoned professionals, break large problems down into small ones that they can debug line by line.
## Assignment

We need to filter the profanity out of our game's live chat feature! Complete `filter_messages` function. It takes a list of chat messages as input and returns 2 new lists:

1. A list of the same messages but with all instances of the word `dang` removed.
2. A list containing the number of `dang` words that were removed from the message at that particular index.

Here are some examples:

```python
message = ["dang it bobby!", "look at it go"]
filter_messages(messages) # returns ["it bobby", "look at it go"]. [1, 0]

message2 = ["That's the bloody dang Reaper of Mars...", "Pax au Telemanus!", "I was never taught how to use a dange razor!"]
filter_messages(messages2) # returns ["That's the bloody Reaper of Mars...", "Pax au Telemanus!", "I was never taught how to use a razor!"], [1, 0]
```

Here are the steps for you to follow:

1. Create the two empty lists that you'll return at the end. One fro the filtered messages, and one for counts of words removed.
2. For each message in the input list:
	1. Split the message into a list of words using the `.split()` string method (see below for help).
	2. Create a new empty list for all the non-bad words for this message.
	3. Create a `counter` variable and set it to `0`. We'll increment this when we remove words from this message.
	4. For each word in the message:
		1. If the word is `dang`, increment the counter.
		2. If it is *not* `dang`, add the word to the non-bad word list you created.
	5. Join the list of non-bad words into a single string using the `.join()` method (see below for help)
	6. Append the new clean message to the final list of filtered messages
	7. Append the count of bad words removed to its list
3. Return the filtered messages first, then the counters.
## Tips

Because we are working with strings that need to be converted to lists and vice versa, here are some very helpful Python methods we can use to make our lives much easier.
### Split a string into a list of words

The `.split()` method in Python is called on a string and returns a list by splitting the string based on a given delimiter. If no delimiter is provided, it will split the string on whitespace. Here's a quick example:

```python
message = "hello there sam"
words = message.split()
print(words)
# Prints: ["hello", "there", "sam"]
```
### Join a list of strings into a single string

The `.join()` method is called on a delimiter (what goes between all the words in the list), and takes a list of strings as input.

```python
list_of_words = ["hello", "there", "sam"]
sentence = " ".join(list_of_words)
print(sentence)
# Prints: "hello there sam"
```
### Completed Assignment

```python
def filter_messages(messages):
    messages_filtered = []
    words_removed = []
    
    for message in messages:
        words = message.split()
        clean_words = []
        counter = 0
        
        for word in words:
            if word == 'dang':
                counter += 1
            else:
                clean_words.append(word)
    
        clean_message = " ".join(clean_words)

        messages_filtered.append(clean_message)
        words_removed.append(counter)
    
    return messages_filtered, words_removed
```
### Explanation

```python
def filter_messages(messages):
```

- This defines the function named `filter_messages` that takes one argument, `messages`.
- `messages` is expected to be a list of strings (e.g. `["Hello dang world", "No bad words"`)

```python
messages_filtered = []
words_removed = []
```

- `messages_filtered`: This list will store the cleaned versions of the messages (with `"dang"` removed)
- `words_removed`: This list will store the number of times `"dang"` was removed from each message.

```python
for message in message:
	words = message.split()
	clean_words = []
	counter = 0
```

- This starts a loop that iterates over each message in the `messages` list.
- For example, if `messages = ["Hello dang world", "No bad words"]`, the loop will run **twice**:
	- First iteration: `message = "Hello dang world"`
	- Second iteration: `message = "No bad words"`
- `message.split()` split the current message into a **list of words**. 
	- For example, if `message = "Hello dang world"`, the `words = ["Hello", "dang", "world"]`.
	- By default, `.split()` splits on **whitespace** (spaces, tabs, etc.)
- `clean_words`: This list will store the words from the message that are not `"dang"`.
- `counter`: This variable will keep track of how many times `"dang"` is removed from the current message.

```python
for word in words:
	if word == 'dang':
		counter += 1
	else:
		clean_words.append(word)
```

- `for word in words`: this loop iterates over each word in the `words` list.
	- For example, if `words = ["Hello", "dang", "world"]`, the loop will run three times. 
		- First iteration: `word = "Hello"`
		- Second iteration: `word = "dang"`
		- Third iteration: `word = "world"`

- If the current word is `"dang"`, increment the `counter` by 1.
	- This keeps track of how many times `"dang"` appears in the message.

- If the current word is **not** `"dang"`, add it to the `clean_words` list.
	- For example, if `word = "Hello"`, it will be added to `clean_words`.

- `" ".join(clean_words)` combines the words in `clean_words` into a single string, separated by spaces.
	- For example, if `clean_words = ["Hello, "world"]`, then `clean_message = "Hello world"`.

```python
messages_filtered.append(clean_message)
words_removed.append(counter)
```

- `messages_filtered.append(clean_message)`: Adds the cleaned message to the `messages_filtered` list.
- `words_removed.append(counter)`: adds the count of removed `"dang"` words to the `words_removed` list.

```python
retrun messages_filtered, words_removed
```

- The function returns two lists:
	- `messages_filtered`: A list of cleaned messages (with `"dang"` removed)
	- `words_removed`: A list of counts of how many times `"dang"` was removed for each message.

Let’s walk through an example to see how the function works step by step.
#### Input:

```python
messages = [
    "This dang thing is driving me crazy",
    "I can't believe how dang hard this is",
    "No bad words here",
    "dang dang dang"
]
```
#### Execution:

1. **First Message:**
    
    - `message = "This dang thing is driving me crazy"`
    - `words = ["This", "dang", "thing", "is", "driving", "me", "crazy"]`
    - `clean_words = ["This", "thing", "is", "driving", "me", "crazy"]`
    - `counter = 1` (one `"dang"` removed)
    - `clean_message = "This thing is driving me crazy"`
    - `messages_filtered = ["This thing is driving me crazy"]`
    - `words_removed = [1]`

1. **Second Message:**
    
    - `message = "I can't believe how dang hard this is"`
    - `words = ["I", "can't", "believe", "how", "dang", "hard", "this", "is"]`
    - `clean_words = ["I", "can't", "believe", "how", "hard", "this", "is"]`
    - `counter = 1` (one `"dang"` removed)
    - `clean_message = "I can't believe how hard this is"`
    - `messages_filtered = ["This thing is driving me crazy", "I can't believe how hard this is"]`
    - `words_removed = [1, 1]`

3. **Third Message:**
    
    - `message = "No bad words here"`
    - `words = ["No", "bad", "words", "here"]`
    - `clean_words = ["No", "bad", "words", "here"]`
    - `counter = 0` (no `"dang"` removed)
    - `clean_message = "No bad words here"`
    - `messages_filtered = ["This thing is driving me crazy", "I can't believe how hard this is", "No bad words here"]`
    - `words_removed = [1, 1, 0]`

4. **Fourth Message:**
    
    - `message = "dang dang dang"`
    - `words = ["dang", "dang", "dang"]`
    - `clean_words = []` (all words are `"dang"`)
    - `counter = 3` (three `"dang"` removed)
    - `clean_message = ""` (empty string)
    - `messages_filtered = ["This thing is driving me crazy", "I can't believe how hard this is", "No bad words here", ""]`
    - `words_removed = [1, 1, 0, 3]`
#### Output:

```python
(
    ["This thing is driving me crazy", "I can't believe how hard this is", "No bad words here", ""],
    [1, 1, 0, 3]
)
```
# Evens and Odds

You've been asked to write a program that will calculate how many odd and even numbers exist in a list.
## Challenge

Write the `gets_odds_and_evens` function to loop through the `numbers` list and check if each number in the list is either odd or even.

Increment the `num_evens` counter if even, and the `num_odds` counter if it's odd. Lastly, return the two values `num_odds` and `num_evens` in that order.
## Completed Challenge

```python
def get_odds_and_evens(numbers):
    num_odds = 0
    num_evens = 0

    # Don't touch above this line
    for num in numbers:
        if num % 2 == 0:
            num_evens += 1
        else:
            num_odds += 1

    return num_odds, num_evens
```

- Start a `for` loop to iterate over each `num` in the list `numbers`.
- If the remainder of each number is cleanly divisible by two, increment the `num_evens` variable.
	- The `%` operator is used to find the remainder of a division between two numbers. 
- If the remainder is not cleanly divisible by two, the number is `odd`, and `num_odds` will be incremented.
- The `return` statement returns the result of the `for` loop, after sorting the numbers into odds and evens.
# Even Teams

Fantasy Quest is having a problem where Battleground teams are uneven when the match begins. We need a function that will correctly split the two teams evenly. 
## Assignment

Complete the `split_players_into_teams` function. Use a [slice](https://www.learnbyexample.org/python-list-slicing/) with a "step" to create two new lists from the `players` list:

- `even_team` should have the players with even-numbered indexes.
- `odd_team` should have the players with odd-numbered indexes.

Return `even_team` and `odd_team` in that order. Be careful not to assign the wrong values to these variables!
### Completed Assignment

```python
def split_players_into_teams(players):
	even_team = players[::2]
	odd_team = players[1::2]
	return even_team, odd_team
```

1. `players[::2]`: this slice starts at the beginning of the list (`0`) and takes every second element (step of 2), which correspond to even-numbered indexes.
2. `players[1::2]`: This slice starts at index `1` and takes every second element (step of 2), which corresponds to odd-numbered indexes.

The `odd_team` list slice **must start at index `1`** because it would otherwise step by 2, adding the *even* numbers to the list.
# Alchemy Ingredients

Fantasy Quest added a new alchemy profession, users would like a way to know how many correctly ordered ingredients they have compared to the required ingredients in their recipes. 
## Assignment

Finish the `check_ingredient_match` function by looping over the `reciple` list. The function should calculate and return a `percentage` of correctly ordered ingredients the character has, as well as a list of missing or wrongly ordered ingredients from the recipe.

The order of the ingredients matter! They must be in the same index as the recipe to match. The missing ingredients must also be in the same order as they appear in the recipe list.

For example, if these were the lists:

```python
recipe = ["Dragon Scale", "Unicorn Hair", "Phoenix Feather", "Troll Tusk"]
ingredients = ["Dragon Scale", "Goblin Hair", "Phoenix Feather", "Troll Tusk"]

percentage, missing_ingredients = check_ingredient_match(reciple, ingredients)
print(percentage, missing_ingredients)
# prints: 75.00 ["Unicorn Hair"]
```

You can assume the `recipe` list and `ingredients` list will always be the same length in your solution!

### Completed Assignment

```python
def check_ingredient_match(recipe, ingredients):
    correct_amt = 0
    missing_or_wrong = []
    
    for i in range(len(recipe)):
        if i < len(ingredients) and ingredients[i] == recipe[i]:
            correct_amt += 1
        else:
            missing_or_wrong.append(recipe[i])

    percentage_correct = (correct_amt / len(recipe)) * 100

    return percentage_correct, missing_or_wrong
```
### Code Breakdown

```python
def check_ingredient_match(recipe, ingredients):
```

- The function takes two arguments: 
	- `recipe`: A list of ingredients in the correct order as per the recipe.
	- `ingredients`: The ingredients that character has, in list form. May or may not match the recipe list.

```python
correct_amt = 0
missing_or_wrong = []
```

- `correct_amt`: A counter to keep track of how many ingredients are in the correct order and match the reciple.
- `missing_or_wrong`: A list to store ingredients that are either missing or in the wrong order.

```python
for i in range(len(recipe)):
```

- This loop iterates over the indices of `recipe`. For each index `i`, it checks if the corresponding ingredient in the `ingredients` list matches the recipe.

```python
if i < len(ingredients) and ingredients[i] == recipe[i]:
	correct_amt
```

- **Condition 1**: if `i < len(ingredients)` ensures that the index `i` is within the bounds of the `ingredients` list. This prevents errors if the `ingredients` list is shorter than the `recipe` list. 
- **Condition 2**: `ingredients[i] == recipe[i]` checks if the ingredient at index `i` in the `ingredients` list matches the ingredients at the same index in the `recipe` list.
- If both are true, the ingredient is correct, and `correct_amt` is incremented by 1.

```python
else:
	missing_or_wrong.append(recipe[i])
```

- If the conditions in the `if` statement are **not met**, it means either:
	- The ingredient is missing (the `ingredients` list is shorter than the `recipe` list).
	- The ingredient is in the wrong order or incorrect.
- In this case, the ingredient from the `recipe` list at index `i` is added to the `missing_or_wrong` list.

```python
percentage_correct = (correct_amt / len(recipe)) * 100
```

- The percentage of correctly ordered ingredients is calculated by *dividing the number of correct* ingredients (`correct_amt`) by the total number of ingredients in the `recipe` list and multiplying it by 100.
### **Example Walkthrough**

#### Input:

```python
recipe = ["flour", "sugar", "butter", "eggs"]
ingredients = ["flour", "sugar", "eggs", "milk"]
```
#### Execution:

1. Loop through the `recipe` list:
    
    - Index 0: `recipe[0] = "flour"`, `ingredients[0] = "flour"` → Match → `correct_amt = 1`.
    - Index 1: `recipe[1] = "sugar"`, `ingredients[1] = "sugar"` → Match → `correct_amt = 2`.
    - Index 2: `recipe[2] = "butter"`, `ingredients[2] = "eggs"` → No match → Add `"butter"` to `missing_or_wrong`.
    - Index 3: `recipe[3] = "eggs"`, `ingredients[3] = "milk"` → No match → Add `"eggs"` to `missing_or_wrong`.

2. Calculate percentage:
    
    - `correct_amt = 2`, `len(recipe) = 4`.
    - `percentage_correct = (2 / 4) * 100 = 50.0`.

3. Return:
    
    - `percentage_correct = 50.0`.
    - `missing_or_wrong = ["butter", "eggs"]`.
#### Output:

```
(50.0, ["butter", "eggs"])
```

---
### **Key Points**

- **Order Matters**: The function ensures that ingredients are not only present but also in the correct order.
- **Handles Missing Ingredients**: If the `ingredients` list is shorter than the `recipe` list, the missing ingredients are added to `missing_or_wrong`.
- **Efficient and Clear**: The code is concise, easy to read, and efficiently handles the task.

---
### **Improvements (Optional)**

If you want to make the function more robust, you could:

1. Handle cases where `recipe` is an empty list to avoid division by zero.
2. Add input validation to ensure `recipe` and `ingredients` are lists.

Example:

```python
if not recipe:
    return 0.0, []
```
# Validate Path

The Fantasy Quest is implementing a new type of quest that requires a player to follow a specific path in order to complete the quest. 
## Assignment

Complete the `validate_path` function. It should compare the expected sequence of waypoints with the actual sequence taken by a character and calculate how accurately the character followed the intended path.
## Inputs

- `expected_path`: A list of waypoints that define the correct path for the quest.
- `character_path`: A list where the first index is the name of the character, and the rest of the list consists of the waypoints they actually visited.

`character_path` contains the same number of waypoints as `expected_path`.
## Output

The function should `return` 2 values:

- `character_name`: a string
- `percentage`: a float
## Example

```py
expected_path = ["A", "B", "C", "D"]
character_path = ["Hero123", "A", "C", "B", "D"]
name, percent = validate_path(expected_path, character_path)
print(name, percent)
# prints: Hero123, 50.0
```
# Double the String

The fantasy quest team wants to add a new easter egg potion to Fantasy Quest. It causes characters to have their in-game chat manipulated when they send messages. The potion doubles every character they send.

- The message they type: `Hello there`
- The message that is sent: `HHeelllloo tthheerree`
## Assignment

Complete the `double_string` function. It takes a string as input and returns a "doubled" version, *including spaces!.

```python
sentence = "LF3M BRD full clear"
print(double_string(sentence)) # "LLFF33MM  BBRRDD  ffuullll  cclleeaarr"
```
## Tip

You can iterate over a string as if it were a list of individual characters.

```python
string = "hello world"
for character in string:
    # process individual characters here
```


