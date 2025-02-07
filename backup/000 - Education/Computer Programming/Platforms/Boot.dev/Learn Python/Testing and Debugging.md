
# Unit Tests

Up until this point, all the coding lessons we've completed have been testing us based on our code's *console output* (what's printed). For example, a lesson might expect your code (in conjunction with the code we provide)

```python
Armor: 2
Health: 18
```

If your code prints that *exact* output, you pass. If it doesn't you fail.
## A New Type of Lesson

Going forward, you'll encounter a new type of lesson: **unit tests**. A unit test is just an automated program that tests a small "unit" of code. Usually just a function or two. The editor will have tabs: `main.py` containing your code, and the `main_test.py` containing the unit tests.

These new unit test style lessons will test your code's *functionality* rather than it's output. Our tests will call functions in your code with different arguments, and expect certain return values. If your code doesn't return the correct values, you fail, if it does, you pass.

There are two reasons for this change:

1. It's more realistic. In the real world, you'll be writing unit tests and running them against your code to make sure it works as expected. 
2. You can run and debug you code with `print` statements, and leave those print statements when you submit. Unlike the output-based lessons, you won't have to remove `print` statements to pass. 
# Two Lesson Types

As we talked about, there are 2 types of coding lessons on Boot.dev:

1. Console output lessons
2. Unit-test lessons
## Console output lessons

- Only 1 file of code, usually with a comment explaining where to write your code
- When you "submit" your code, its console output must match the expected output exactly to pass
- Debug `print` statements will cause your code to fail submission, so remove them before submitting
## Unit-test lessons

- 2 files of code: `main` and `main_test`. You can read the tests but you can't edit them
- When you "submit" your code, the return values of your functions must match the expected values exactly to pass
- Console output is ignored, you can leave debug `print` statements in your code
## Which is more common?

Going forward, you'll encounter far more unit-test lessons than console output lessons, but you'll still see both from time to time. Different concepts are better suited to different types of lessons.
# Debugging

When you're working as a professional developer, you'll typically write code on your computer and test it by yourself before it's deployed to users.

That first part of the process is called *debugging*. You write some code, run it, and if it doesn't work, you fix the bugs. You repeat this process until you're confident that your code works as expected. 
## Run vs. Submit

At Boot.dev, the `Run` button is for debugging. The `Submit` button mimics the idea of publishing your code for production use. 

You should be debugging your code with the `Run` button. You should be adding `print()` statements to your code to make sure it's doing what you think it's doing at different points in the code. 

- Write a line to calculate a value
- `print()` the value you calculated
- Run the code
- Did it print what was expected? If not, fix it
- Repeat

You will never lose XP or be penalized on Boot.dev for using the run button. However, there are consequences for submitting broken code, just like there are career consequences for pushing broken code to your users. 

## The submit button will run additional tests

When you use the `Run` button, a few tests will run against your code. However, the `Submit` button will run _additional_ tests that you're not able to debug against. That's what keeps it fun and realistic (it's so hard to know what your users will do with your code!).
# Learning Effectively

This course is about to get a bit *harder*. There's no way around it, if programming were a walk in the park everyone would be earning 6 figgies as a software engineer. But it's not, and to succeed without getting stuck and frustrated, you need to learn how to learn.
## Process for Solving Hard Coding Problems

1. **Read the lesson first**. Figure out the examples before writing your code.
2. **Read the assignment**. Understand the goal of the assignment before you start writing code.
3. **Start writing code**.
4. **Add `print()` statements**. Don't wait until you've written a lot of code to start testing. Add `print()` statements and use the `Run` button to see if your code is doing what you expect at each step. It's easier to find issues in small bits of code than in large blocks of code.
	- Keep running, printing, and fixing until you're confident your code is working.
5. **Submit your code**. If the assignment you're working on has unit tests, no need to remove your debugging `print()` statements. If the assignment you're working on is testing console output, be sure to remove your `print()` statements before submitting. 
6. **Compare your code to the instructor's**. You will *not* be penalized for looking at the solution after you have successfully completed the assignment. 
## Additional Tidbits

- Try to use Boots before peeking at the solution. Boots is quite good at giving you pointed hints to help you solve the problem on your own.
- It's okay to peek at the solution when you're completely stuck every once in a while, but _don't make it a habit_. If you find that you're always stuck, you should restart the chapter or course to make sure you understand the material.
- You can reset your code for an assignment with the "reset" button. For example, maybe you forgot which modifications _you_ made vs which code was left by the instructor.
- You can reset all your cached code from the settings page. This is useful if you want to restart a course or chapter.
# Debugging Practice

I want to walk you through how I approach writing code, complete with all the debugging steps I take along the way.

The goal is to write *small amounts of code*, and then *test* each bit of code to make sure it's doing what's expected before moving on. **Trying to write entire programs at once is a recipe for pain** 
**and suffering**. The goal is to write a few lines, test them, and then write a few more lines, and repeat until done.

This isn't a technique that's unique to beginners. Even senior engineers write code this way. 
## Assignment

Let's complete the `unlock_achievement` function. It accepts 3 arguments:

- `before_xp`: int
- `ach_xp`: int
- `ach_name`: str

It should return 2 values:

- The player's xp after the achievement is unlocked (The sum of `before_xp` and `ach_xp`)
- An alert message that says `"Achievement Unlocked: ACHIEVEMENT_NAME"`, where `ACHIEVEMENT_NAME` is the name of the achievement

Let's start by running the code in its current state. You should see an error like this:

```
IndentationError: expected an indented block after function definition
```

Run the code again. This time you shouldn't get a syntax error, but your tests should fail because you're returning the incorrect values. Let's fix that.

Let's start by calculating the new amount of xp. Update the function body:

```python
def unlock_achievement(before_xp, ach_xp, ach_name):
    after_xp = before_xp - ach_xp
    print("After xp:", after_xp)
    return None, None
```

Run the code again. This time you should see the `after_xp` value printed to the console. Does it look correct? It shouldn't... we have a bug! The `after_xp` should be the _sum_ of the `before_xp` and `ach_xp` values. Fix the code and run it again to make sure it's working.

Once that's working, remove the `print` statement and `return` the `after_xp` value instead of the first `None`. Run the code again. You should see that your tests are closer: The first "expected" and "actual" values should match for each test. The second return value is still broken, let's fix it!

Now that we have the `after_xp` value, we need to create an alert message. Update the function body:

```python
def unlock_achievement(before_xp, ach_xp, ach_name):
    after_xp = before_xp + ach_xp
    alert = "Achievement: " + ach_name
    print(alert)
    return after_xp, None
```

Run the code. Is the console output what we expect? We want the alert to say: 

```
Achievement Unlocked: ACHIEVEMENT_NAME
```

Looks like the output is missing the word "Unlocked". Fix the bug, then run the code again to make sure it's working. 

When you're confident, remove the `print` statement and `return` the `alert` value instead of the second `None`. Run the code again. You should see that your tests are passing!

Now that your tests are passing, submit your code so that it runs against _all_ the test cases. Remember, when you "run" instead of submit you're only able to see a few of the tests. The submit button will run _all_ the tests, which might catch bugs you didn't know you had! That's why it's important to debug with print statements and the run button before submitting.
# Stack Trace

A **stack trace** (or "traceback") is a scary-looking error message that the Python interpreter prints to the console when it encounters certain problems. Stack traces are most common when you're trying to run invalid Python code. 

You need to get used to figuring out scary error messages as a programmer. We might as well start now. 
## Assignment

Go ahead and run the code in its current state. You should see something like this:

```
PythonError: Traceback (most recent call last):
  File "<exec>", line 6, in <module>
  File "<string>", line 1, in <module>
  File "/home/pyodide/main.py", line 3
    msg = f"You have {strength} strength, {wisdom} wisdom, and {dexterity} dexterity for a total of {total} stats.
                                                                                                                  ^
IndentationError: unindent does not match any outer indentation level
```

1. `PythonError: Traceback (most recent call last):`
	- This is a standard header that's just letting us know that a Python traceback is what we're looking at. 

2. `File "<exec>", line 6, in <module>` and `File "<string>", line 1, in <module>`
	- This is the start of the "trace". These strange "`<exec>`" and `"<string>"` files don't really exist, the Python interpreter is letting us know about them because they have to do with how your code is executed in a virtual browser-based environment. 

3. `File "/home/pyodide/main.py", line 3`
	- Now we're getting to the real meat of the error message. The purpose of a "trace" is to show us the path that the Python interpreter took through our code before it encountered the error, which can help us figure out what went wrong.
	- In this case, the interpreter was executing the code in the `main.py` file, and it got to line 3 before it encountered the error.

4. `msg = f"You have {strength} strength, {wisdom} wisdom, and {dexterity} dexterity for a total of {total} stats.`
	- This is the line of code that caused the error.

5. `IndentationError: unindent does not match any outer indentation level`
	- This is the type of error that was raised. In this case, it's an `IndentationError`, which means that the Python interpreter was expecting a certain amount of indentation (whitespace at the beginning of the line) but it didn't get what it was expecting.

**Don't be fooled**. The proper amount of indentation is Python is 4 spaces (or one `<tab>` stroke). In this case, line 2 is actually indented 6 spaces, which is why the interpreter is confused. 

Run the code again. You should see another error, this time the last few lines are something like:

```
msg = f"You have {strength} strength, {wisdom} wisdom, and {dexterity} dexterity for a total of {total} stats.
                                                                                                 ^
SyntaxError: unterminated string literal (detected at line 3)
```

Now we have a `SyntaxError`, which is just a more general type of error related to invalid code. Take a close look at line 3 and fix the problem.

