#### How to understand and control where Python Variables are Accessed

When writing programs in Python, often we will define data (usually in the form of variables) to accomplish a task. 

Once the program is ready to read Python, t will follow a distinc order to assess if a piece of data is accessible or not. The *scope* of our data is the level at which it can be accessed.

### Local Scope

When working with functions, we will often find that where we define our data will determine its scope. If we define a variable instead of a function then it is known as a *local variable* - a variable defined in the *local scope*.

-  We can think of it being locally defined to only accessible inside the function.

Here is what a local variable might look like inside of a program:

```python
def welcome_user(name):    
  greeting = "Hello " + name + "!"    
  print(greeting)
  
welcome_user("User")
```

Would output:

```
Hello User!
```

The *local variable* in this example is `greeting`. This is a variable that is created inside of the function `welcome_user()` and thus only has scope locally within that function.

Local variables from one function can not be accessed outside of that function.

Take a look at a modified version of the last example:

```python
def welcome_user(name):    
  greeting = "Hello " + name + "!" 

print(greeting)

welcome_user("User")
```
> Running this program would throw `NameError`

> This is because we tried to access `greeting` outside of the function where it is not accessible. The scope of `greeting` is only within the function `welcome_user()`.

### Global Scope

Some variables are accessible anywhere in a script. These types of variables are referred to as ***global variables*** and share what is known as the ***global scope***. 

Global variables are typically defined outside of all the functions in the script and store data we want to use throughout the entire program. 

Let's look at any example where global variables are used:

```python
balance = 12.55
name = "Lilia" 

def withdraw_money(amount):    
  result = balance - amount    
  print("Hello " + name + " your balance remaining is: $" + str(result))    
  return amount 

withdraw_money(2)print("Save your money " + name + "!")
```

> In this code, `balance` and `name` are both global variables. The function `withdraw_money()` is able to access them and they can also be accessed outside of the function in the final `print()` statement.

```
Hello Lilia your balance remaining is: $10.55
Save your money Lilia!
```

### Scope and Nested Functions

**Nested Functions** provide a great example of how scope is determined in our program. Typically, the order of scope follows the pattern where inner functions are able to access outer functions variables, but other functions are not able to access inner function variables.

Here is what that looks like in code:

```python
def outer_func():    
  location = "Inside the outer function!"    
  
  def inner_func():        
    location = "Inside the inner function!"        
    print(location)    
  
  inner_func()    
  print(location)
outer_func()
```

> In this example, we use `location` as the variable name for two local variables. 
> Each instance of `location` has a different scope, so when the functions are called, Python uses the closest available scope for the variable definition.

- Because of this, when we call `outer_func()` we do not overwrite the value of `location` and both strings are printed. 

This is what the output would be:

```python
Inside the inner function!
Inside the outer function!
```

# Review: Fundamentals of Python

**Review what's covered in Fundamentals of Python**

- Use control statements like `if`, `else`, and `elif` in Python to control the flow of a program.
- Create, edit and perform operations on string and number variables in Python.
- Create, edit and sort lists using Python methods.
- Write `for` and `while` loops and use `break` and `continue` statements in Python.
- Write functions with parameters and the `return` keyword.

