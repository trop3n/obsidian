---
up: "[[Functions]]"
tags:
  - education/
---

# Scope

Scope refers to *where a variable* or function name is available to be used. For example, when we create variables in a function (such as by giving names to our parameters), that data is *not* available outside of that function. 

```python
def subtract(x, y)
	return x - y
result = subtract(5, 3)
print(x)
# ERROR ! "name 'x' is not defined"
```

When the `subtract` function is called, we assign 5 to the variable `x`, but `x` only exists in the code *within* the `subtract` function. If we try to print `x` outside of that function, then we won't get a result, we will get a big fat error.
# Global Scope

So far we've been working in the global scope. That means that when we define a variable or function is accessible in *every other place* in our program, even within other functions.

For example:

```python
pi = 3.14

def get_area_of_circle(radius):
	return pi * radius * radius
```

Because `pi` was declared in the parent "global" scope, it is usable within the `get_area_of_circle()` function.

