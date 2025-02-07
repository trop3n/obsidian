

Dictionaries in Python are used to store data values in `key` -> `value` pairs. Dictionaries are a great way to store *groups of information*.

```python
# use curly braces
# add key-value pairs
car = {
	"brand": "Tesla",
	"model": "3",
	"year": 2019
}
```

Here the `car` variable is assigned to a dictionary `{}` containing the keys:

- `brand`
- `model`
- `year`

The keys' corresponding values are:

- `Tesla`
- `3`
- `2019`
## Assignment

Completed the `get_character_record` function. It takes the character's `name`, `server`, `level`, and `rank` as individual inputs, and returns a dictionary with the following string keys:

- `"name"`
- `"server"`
- `"level"`
- `"rank"`
- `"id"`

Create and return a dictionary with the keys above. Assign each of the four inputs to the matching key, ie `"name": name`.

Next, we can't have two characters named `bloodwarrior123` on the same server. For the firth key, `id`, create a unique value as follows:

Concatenate the `name` and `server` inputs with a `#` in the middle. For example, given: 

- name = bloodwarrior123
- server = server1

Then the `id` field would be set to `bloodwarrior123#server1`.
## Tips

- You can return the dictionary directly without first assigning it to a variable.
- I recommend using an `f-string` to create the `id` field. This is a best practice.
# Duplicate Keys

Because dictionaries rely on unique keys, you can't have two of the same key in the same dictionary. If you try to use the same key twice, the first value will simply be overwritten.
## Assignment

Another developer on our team has introduced a bug by specifying duplicate keys in the dictionary. *Fix the bug*.

The `get_character_record` function takes a character's `name`, `server`, `level`, and `rank`. It should return a dictionary with the following fields:

- name
- server
- level
- rank
- id

Where the `id` is the `name` and the `server` concatenated together with a `#` in the middle for uniqueness. We can't have two `bloodwarrior123`'s on the same server!
# Accessing Dictionary Values

Dictionary elements must be accessible somehow in code, otherwise they wouldn't be very useful. A value is retrieved from a dictionary by specifying its corresponding key in square brackets. The square brackets look similar to indexing into a list.

```python
car = {
	   "make": "tesla",
	   "model": "3"
}
print(car["make"])
# prints: tesla
```
# Setting Dictionary Values

You don't need to create a dictionary with values already inside. It is common to create a blank dictionary then populate it later using **dynamic values**. The syntax is the same as getting data out of a key, just use the assignment operator (`=`) to give that key a value.

```python
planets = {}
planets["Earth"] = True
planets["Pluto"] = False
print(planets["Pluto"])
# Prints False
```
## Assignment

Use the example below to answer the question:

```python
names = ["jack bronson", "jill mcarty", "john denver"]

names_dict = {}
for name in names:
    # .split() returns a list of strings
    # where each string is a single word from the original
    name_list = name.split()

    # here we update the dictionary
    names_dict[name_list[0]] = name_list[1]

print(names_dict)
# Prints: {'jack': 'bronson', 'jill': 'mcarty', 'john': 'denver'}
```
# Updating Dictionary Values

If you try to set the value of a key that already exists, you'll end up just updating the value of that key. 

```python
planets = {
    "Pluto": True,
}
planets["Pluto"] = False
print(planets["Pluto"])
# Prints False
```
## Assignment

Use the example below to answer the question:

```python
full_names = ["jack bronson", "james mcarty", "jack denver"]

names_dict = {}
for full_name in full_names:
    # .split() returns a list of strings
    # where each string is a single word from the original
    names = full_name.split()
    first_name = names[0]
    last_name = names[1]
    names_dict[first_name] = last_name

print(names_dict)
# {
#   'jack': 'denver',
#   'james': 'mcarty'
# }
```

In this example, "denver" overwrote "bronson" as the value for the key "jack".
# Deleting Dictionary Values

You can delete existing keys using the `del` keyword.

```python
names_dict = {
    "jack": "bronson",
    "jill": "mcarty",
    "joe": "denver"
}

del names_dict["joe"]

print(names_dict)
# Prints: {'jack': 'bronson', 'jill': 'mcarty'}
```
## Deleting Keys That Don't Exist

Notice that if you try to delete a key that doesn't exist, you'll get an _error_.

```python
names_dict = {
    "jack": "bronson",
    "jill": "mcarty",
    "joe": "denver"
}

del names_dict["unknown"]
# ERROR HERE, key doesn't exist
```
# Counting Practice

If you're unsure whether or not a key exists in a dictionary, use the `in` keyword. 

```python
cars = {
	"ford": "f150",
	"tesla": "3"
}

print("ford" in cars)
# prints True

print("gmc" in cars)
# prints false
```
## Assignment

We need to be able to report to our players how many enemies are in their immediate vicinity - but they want the count of each enemy by its _kind_. Fix the `count_enemies` function. If you run the code, it will result in a [KeyError](https://docs.python.org/3/library/exceptions.html#KeyError). It takes a list of `enemy_names` as input. It should return a dictionary where the keys are all the enemy names from the list, and the values are the counts of how many times each enemy appeared in the list.

```python
def count_enemies(enemy_names):
	enemies_dict = {} 
	for enemy_name in enemy_names: 
		enemies_dict[enemy_name] += 1 
	return enemies_dict
```
### Explanation:

- **Problem**: The original code attempted to increment `enemies_dict[enemy_name]` before initializing it, causing a `KeyError` for new enemy names.
- **Solution**: Use `dict.get(key, default)` to safely check the current count of an enemy. If the enemy doesn't exist in the dictionary, `.get()` returns `0`, and then we increment it to `1`. For existing enemies, we increment their count by 1.

```python
def count_enemies(enemy_names):
    enemies_dict = {}
    for enemy_name in enemy_names:
        enemies_dict[enemy_name] = enemies_dict.get(enemy_name, 0) + 1
    return enemies_dict
```
# Iterating Over a Dictionary in Python

We can iterate over a dictionary's keys using the same no-index syntax we used to iterate over the values in a list. With access to the dictionary's keys, we also have access to their corresponding values.

```python
fruit_sizes = {
	"apple": "small",
	"banana": "large",
	"grape": "tiny"
}

for name in fruit_sizes:
	size = fruit_sizes[name]
	print(f"name: {name}, size: {size}")
```
```
name: apple, size: small
name: banana, size: large
name: grape, size: tiny
```

Note: we could have just as easily set the `name` variable to `key` or simply `k`.
## Assignment

We need to display on our player's screens what the most common enemy in a given area of the game map is.

Complete the `get_most_common_enemy` function by iterating over all enemies in the dictionary and returning only the _name_ of the enemy with the highest count.

If there are no enemies, return `None`. If there are multiple enemies with the same highest count, return the first one found.

`enemies_dict` is a dictionary of `name` -> `count`. Example:

```python
def get_most_common_enemy(enemies_dict):
    if not enemies_dict:
        return None
    max_count = None
    most_common = None
    for name, count in enemies_dict.items():
        if max_count is None or count > max_count:
            max_count = count
            most_common = name
    return most_common
```
### Explanation

1. **Check for an empty directory**: The function first checks if the input directory `enemies_dict` is empty. If it is, the function returns `None` as there are no enemies to consider.

```python
if not enemies_dict:
	return none
```

2. **Initialize Variables**: `max_count` is initialized to None to handle *any possible* values (including zero or negative counts), and `most_common` is initialized to None to track the enemy name.

```python
max_count = None
most_common = None
```

3. **Iterate through entries**: The loop iterates over each key-value pair in the directory. For each pair, it checks if the current count is greater than the `max_count` (or if `max_count` is None, indicating the first iteration). If true, it updates `max_count` and `most_common` with the current enemy's count and name.

```python
for name, count in enemies_dict.items():
	if max_count is None or count > max_count:
		max_count = count
		most_common = name
return most_common
```

1. **Return the result**: After processing all entries, the function returns the enemy name stored in `most_common`, which is the first enemy encountered with the highest count. 