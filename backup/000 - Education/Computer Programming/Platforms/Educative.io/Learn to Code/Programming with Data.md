#python #educativeio #programming
# You Are Hired Again
> A fitness company is hiring you as a data science expert to help fitness instructors make informed decisions about their clients by analyzing and understanding their data. 

This data includes the number of hourly steps recorded by the smartwatches the company has given to all its clients as part of a subscription package.

### Your Role

> Your role is to convert this raw data from their clients' smartwatches into visually meaningiful information to help instructors analyze and provide valuable insights into their activity levels throughout the week.

This, in turn, will help them filter the clients who might need more attention. On successful delivery of the project, you'll be considerably compensated.

### Making Sense of the Data

Before you delve into the project's requirements, the fitness company wants you to familiarize yourself with the data you'll work on. The data provided to you by the company includes their subscriber's names and their hourly step counts for seven consecutive days. 

Seven days make up 168 hours in total: one day consists of 24. Here's the sample data for a single user (format: client's name followed by 168 numbers - step counts for 168 hours.)

```python
Juliana,685,0,0,0,0,0,0,0,0,964,934,21,623,1085,989,1113,599,667,869,1192,86,402,1040,1065,953,903,0,0,0,0,0,0,631,1178,410,447,1013,952,482,67,62,1164,977,1127,970,22,403,665,762,0,0,0,0,0,0,0,0,649,1029,1133,1000,802,946,675,768,743,786,41,856,868,209,1097,469,217,0,0,0,0,0,0,0,495,241,941,495,583,380,84,421,431,502,62,345,923,492,856,926,1150,0,0,0,0,0,0,0,0,1146,742,986,300,489,1056,95,1083,905,749,77,213,270,278,0,0,0,0,0,0,0,0,340,960,631,795,1055,585,981,423,35,92,1003,40,490,1092,579,698,0,0,0,0,0,0,1072,326,491,768,39,442,466,1077,735,377,258,370,1191,81,93,440,488,1184
```

> The company's data file currently contains hourly step counts for only 10 users. If all goes well, they might give us hundred's of user's data. 

The following code widget shows data for three subscribers (from **lines 2 to 4**). **Line 1** is the header row containing the names of each column.

```python
name,hr0,hr1,hr2,hr3,hr4,hr5,hr6,hr7,hr8,hr9,hr10,hr11,hr12,hr13,hr14,hr15,hr16,hr17,hr18,hr19,hr20,hr21,hr22,hr23,hr24,hr25,hr26,hr27,hr28,hr29,hr30,hr31,hr32,hr33,hr34,hr35,hr36,hr37,hr38,hr39,hr40,hr41,hr42,hr43,hr44,hr45,hr46,hr47,hr48,hr49,hr50,hr51,hr52,hr53,hr54,hr55,hr56,hr57,hr58,hr59,hr60,hr61,hr62,hr63,hr64,hr65,hr66,hr67,hr68,hr69,hr70,hr71,hr72,hr73,hr74,hr75,hr76,hr77,hr78,hr79,hr80,hr81,hr82,hr83,hr84,hr85,hr86,hr87,hr88,hr89,hr90,hr91,hr92,hr93,hr94,hr95,hr96,hr97,hr98,hr99,hr100,hr101,hr102,hr103,hr104,hr105,hr106,hr107,hr108,hr109,hr110,hr111,hr112,hr113,hr114,hr115,hr116,hr117,hr118,hr119,hr120,hr121,hr122,hr123,hr124,hr125,hr126,hr127,hr128,hr129,hr130,hr131,hr132,hr133,hr134,hr135,hr136,hr137,hr138,hr139,hr140,hr141,hr142,hr143,hr144,hr145,hr146,hr147,hr148,hr149,hr150,hr151,hr152,hr153,hr154,hr155,hr156,hr157,hr158,hr159,hr160,hr161,hr162,hr163,hr164,hr165,hr166,hr167

Juliana,685,0,0,0,0,0,0,0,0,964,934,21,623,1085,989,1113,599,667,869,1192,86,402,1040,1065,953,903,0,0,0,0,0,0,631,1178,410,447,1013,952,482,67,62,1164,977,1127,970,22,403,665,762,0,0,0,0,0,0,0,0,649,1029,1133,1000,802,946,675,768,743,786,41,856,868,209,1097,469,217,0,0,0,0,0,0,0,495,241,941,495,583,380,84,421,431,502,62,345,923,492,856,926,1150,0,0,0,0,0,0,0,0,1146,742,986,300,489,1056,95,1083,905,749,77,213,270,278,0,0,0,0,0,0,0,0,340,960,631,795,1055,585,981,423,35,92,1003,40,490,1092,579,698,0,0,0,0,0,0,1072,326,491,768,39,442,466,1077,735,377,258,370,1191,81,93,440,488,1184

Sara,347,625,729,977,0,0,0,0,901,651,1072,835,203,471,85,513,340,1144,1018,342,641,284,1006,656,459,528,737,1030,1110,0,0,0,0,1145,942,1042,74,974,892,276,740,589,1017,412,717,257,729,992,1117,1040,726,292,977,0,0,0,0,0,0,41,326,471,493,937,1194,447,632,1021,683,973,867,1064,280,968,278,840,608,0,0,0,0,1101,769,347,418,743,79,865,474,398,1032,581,1112,283,993,989,889,801,1049,0,0,0,0,0,212,701,595,824,387,40,345,207,1071,939,1132,625,892,1124,831,277,908,493,421,0,0,0,0,0,722,346,901,30,304,665,1060,54,22,604,517,609,1128,938,551,873,518,828,639,922,0,0,0,0,0,0,69,1167,721,277,287,646,57,985,822,77,1080,842,1152,1038

Rayne,1093,348,462,1140,0,0,0,0,0,0,360,987,420,1043,715,1044,1014,352,440,895,54,720,1114,1166,904,750,769,497,586,0,0,0,0,0,0,297,391,1117,695,67,846,488,724,33,1111,331,588,361,807,805,1049,0,0,0,0,0,0,0,931,292,660,55,66,976,415,640,435,762,303,392,338,844,912,864,268,0,0,0,0,0,0,0,842,1164,904,69,857,93,823,946,1156,838,829,705,343,432,556,244,299,0,0,0,0,0,0,1073,935,875,503,677,1148,695,718,708,62,60,742,540,1077,693,549,1116,952,666,0,0,0,0,0,0,944,976,1040,803,92,701,58,272,340,431,445,91,242,626,910,746,385,976,0,0,0,0,0,687,606,95,355,575,319,38,1080,100,885,719,89,1016,786,680
```
### Data at a Glance

Of course, it's tiresome for any human to go through all 168 times 10 numbers and make any sense. To better understand the data, here's the same data in a tabular form:
### Project's End Goal -- Data Visualization

> It's precisely because of the complexity of the data that they want to hire a Python programmer. They're looking for someone who can write a program that reads all this data and outputs their client's activity by presenting the input through visual charts and plots. 

Here are some visualization options that your code needs to compute:

***Line Plot***: A line plot is a type of chart that displays data points over a continuous interval or time span, and these points are connected by straight line segments. Line graphs are particularly useful for visualizing trends, patterns and relationships in data.

- For our use case, we can use it to plot the activity of a user for the whole day.

***Bar Chart***: A bar chart is a graphical representation of data in which rectangular bars of varying lengths are used to depict the values of different categories or groups. The length of each bar corresponds to the magnitude of the data it represents. We can use bar graphs to compare the number of steps taken each day of the week or to compare the performance of different users.

***Bubble Plot***: A bubble plot, also known as a bubble chart, is a type of scatter plot where data points are represented by circles (bubbles) instead of points. Each bubble in the plot has three parameters: `x-coordinate`, `y coordinate` and the `size`. The size of the bubble is often used to *represent a third numerical variable*. This third variable can add and additional layer of information to the plot. 

- We can make a bubble plot to display the data for the entire batch of suers in a single screen. 

***Pie Chart***: A pie chart is a circular grapg that represents data in slices, where each slice corresponds to a specific category or portion of a whole. The size of each slice is proportional to the quantity it represents, making it easy to visualize the distribution of different parts in relation to the whole.

- We can use pie charts to visualize the ratio of students performing above or below the threshold values. 

### Project Requirements

1. Programmatically read the hourly smartwatch data of members from a text file.
2. Store the data in appropriate data structures, such as lists and dictionaries
3. Compute performance statistics for each user (min, max, average steps)
4. Visually analyze all member's activity data to achieve the following goals:
		a. Tracking a member's activity for a particular day through a line plot
		b. Categorizing members into groups based on their performance through a pie chart
		c. Comparing the performance of members through a sorted bar plot.
		d. Providing a snapshot of all member's performance through a bubble plot.

# Lists in Python

> Being able to neatly store all the information/data is a basic requirementbecause all other requirements and computations, like finding minimum, maximum, and average, depend on having the data inside our code. 

### Storing Data in Variables

We do know how to use variables in Python. A **variable** is a named memory location that can store a value inside our code. We can assign a value to a variable. We can reassign a different value to it later in the code.

We can also print the variable. Here's an example:

```Python
day = "Sunday"
print(day)

day = "Monday"
print(day)

#Output:
#Sunday
#Monday
```

> But in this project, we don't have to just store a single value. We're data scientists, and we need to read lots of data. 

Let's imagine we have to store the names of the days of the week. No problem, we can create and initialize seven variables, appropriately named. Here's how to do it:

```Python
day0 = "Sunday"
day1 = "Monday"
day2 = "Tuesday"
day3 = "Wednesday"
day4 = "Thursday"
day5 = "Friday"
day6 = "Saturday"
```

What if our code requires us to store 24 hourly information, e.g. steps taken each hour? Hmm, we might not like it, but we'll have to use 24 variables this time:

```python
hour0 = 0
hour1 = 0
hour2 = 0
hour3 = 0
hour4 = 0
hour5 = 0
hour6 = 0
hour7 = 0
hour8 = 0
hour9 = 0
hour10 = 0
hour11 = 0
hour12 = 0
hour13 = 0
hour14 = 0
hour15 = 0
hour16 = 0
hour17 = 0
hour18 = 0
hour19 = 0
hour20 = 0
hour21 = 0
hour22 = 0
hour23 = 10000
```

**Hint**: Doesn't it seem to be the data of a person who loves to sleep all day but still manages to squeeze in ten thousand steps in the last hour?

### The Difficulty of Storing Fitness Data in Variables

> Manually storing 168 variables and then initializing them is quite a terrifying though (because we've already seen the data the client has hired us for). What's more worrying is the fact that there are about ten sets of 168 entries. 

Can you imagine writing 1680 lines of code just to represent the data in your Python program? And we haven't even thought of all the other requirements yet.

### Lists as a Data Structure

> Thankfully, Python gives us an easier way to store such a sequential collection of data through a data structure called a ***list***, which makes the code readable and a programmer's life much easier.

Like a variable, a list can also *store data*, but as the name implies, it can store a *list of items, not just one item*. 

Lastly, the same Python list can store numbers and text strings (if required), so one list isn't restricted to one data type alone. 

#### Syntax for Creating Lists

> Let's create our first list. Let's call it `days_of_week` and assign a list of days to it using the assignment operator (`=`). 

The main difference between an ordinary variable and a list are as follows:

- Different items in a list are comma-separated
- The comma-separated values are enclosed within square brackets

```Python
days_of_week = ["Sunday" , "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"]
```

# Lists in Python

> Being able to neatly store all the information/data is a basic requirement because all other requirements and computations, like finding minimum, maximum and average, depend on having the data inside our code.

## Storing Data in Variables

We do know how to use variables in Python. A ***variable*** is a named memory location that can store a value inside our code. We can assign a value to a variable. We can reassign a different value to it later in the code. We can also print the variable. Here's an example:

```Python
day = "Sunday"
print(day)

day = "Monday"
print(day)
```

But in this project, we don't have to just store a single value. We're data scientists, and we need to read lots of data. 

Let's imagine we have to store the names of the days of the week. No problem, we can create and initialize seven variables, appropriately named. Here's how to do it:

```python
day0 = "Sunday"
day1 = "Monday"
day2 = "Tuesday"
day3 = "Wednesday"
day4 = "Thursday"
day5 = "Friday"
day6 = "Saturday"
```

What if our code requires us to store 24 hourly information, e.g. steps taken each hour? Hmm, we might not like it, but we'll have to use 24 variables this time.

```python
hour0 = 0
hour1 = 0
hour2 = 0
hour3 = 0
hour4 = 0
hour5 = 0
hour6 = 0
hour7 = 0
hour8 = 0
hour9 = 0
hour10 = 0
hour11 = 0
hour12 = 0
hour13 = 0
hour14 = 0
hour15 = 0
hour16 = 0
hour17 = 0
hour18 = 0
hour19 = 0
hour20 = 0
hour21 = 0
hour22 = 0
hour23 = 10000
```

## The Difficulty of Storing Fitness Data in Variables

Here's what you might be thinking: manually entering 168 variables and then initializing them is quire a terrifying thought. What's more worrying is the fact that there are about ten sets of 168 entries. Can you imagine writing 1680 lines of code just to represent the data in your Python program?

Even if you somehow manage to write these wretched 1680 lines of variable initialization, what sort of code would it take to compare this colossal list of variables just to find the maximum number of steps a user takes in a week?

## Lists as a Data Structure

> Thankfully Python gives us an easier way to store such a sequential collection of data through a data structure called a ***list***, which makes the code readable and a programmer's life much easier.

Like a variable, a list can also store data, but as its name implies, it can store a list of items, not just one item. Lastly, Python lists can store numbers and text strings (if required) so one list isn't restricted to one data type alone.

### Syntax for Creating Lists

The main difference between an ordinary variable and a list are as follows:

- Different items in a list are comma-separated
- The comma-separated values are enclosed within square brackets.

```python
days_of_week = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"]
```

If we run this code, it runs successfully. We can print lists like we printed variables earlier.

```python
days_of_week = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"]
print(days_of_week)
```

```python

# Output:

['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday']
```

How about creating a list of numbers instead of strings? **Line 4** in the widget below creates a `steps_per_day` named list, and **line 5** prints it. 

```python
days_of_week = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"]
print(days_of_week)

steps_per_day = [7000, 5500, 10300, 8000, 1200, 2000, 5000]
print(steps_per_day)
```

```python
# output:

["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"]
[7000, 5500, 10300, 8000, 1200, 2000, 5000]
```

> That worked great, but can we initialize a list with mixed data types? **Line 7** below does exactly that.

```python
days_of_week = ["Sunday" , "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"]
print(days_of_week)

steps_per_day = [7000, 5500, 10300, 8000, 1200, 2000, 5000]
print(steps_per_day)

fitness_data = ["Juliana", 7000, 5500, 10300, 8000, 1200, 2000, 5000]
print(fitness_data)
```

## Accessing an Element

However, we don't just have to store and print the data. We have to eventually compute something based on the data. We also need to be able to access individual elements of the list. Imagine we have two numbers, and we have to compute which of the two is the **maximum number**. 

If the two numbers are stored in two different variables, then the code is simple enough:

```Python
num1 = 5
num2 = 8
maximum_num = 0

if num1 >= num2:
	maximum_num = num1
else:
	maximum_num = num2
print(maximum_num)
```

When we click the “Run” button, the output of the code is `8`, which, of course, means that instead of the `if` case, the execution went into the `else` case and `maximum_num` got assigned value `8` on **line 8** because `5` is not `>=` `8`.

> [!NOTE] Switching Values
> Why don't we try switching the values? Make `num1 = 8` and `num2 = 5`, and then see if `maximum_num` gets assigned on **line 6**. If it does, that means that we've written the correct code for finding the maximum number given two variables.

## Finding the Maximum Number in a List

What if we had to do the same, but for a list, i.e. finding the maximum value in a list that has two numbers?

```python
numbers = [5, 8]
```

Let's understand what we meant when we said we need to be able to access individual elements of the list. We know that `numbers` is the name of the list. But how do we write code that checks whether the first element of `numbers` is greater than the second element of `numbers`? Why don't we try and print the first element of `numbers`?

```python
numbers = [5, 8]
first_element = numbers[1]
print(first_element)

# Python is a **zero-indexed** language, meaning that the first number in the list is at index 0, not index 1.
```

**Line 2** aims to access the first element through `numbers[1]` but when we run the code, `first_element` clearly get assigned the second element (`8`), which then gets printed on the screen. Any idea what went wrong? Try your own hypothesis first.


> [!NOTE] Indexing
> `numbers[0]` gives us the first element stored in the `numbers` list while `numbers[1]` gives us the second. With this knowledge, let’s find out which number in the list is the maximum number.

We already know the algorithm for finding the maximum of the two variables, and now we know how to access individual elements/values inside a list. Can we write the code to find the maximum of the two values that are stored inside a `numbers` named list?

```python
numbers = [5,8]
maximum_num = 0

# Write your code here
if numbers[0] >= numbers[1]:
    maximum_num = numbers[0]
else:
    maximum_num = numbers[1]
print(maximum_num)
```

## Finding the Last Element of the List

The `numbers` list only has two elements in it. We've written code that only accesses the list on indexes 0 and 1. But what would happen if we overstep the boundary of the list and tried accessing index 2 of `numbers`?

```python
numbers = [5, 8]
print(numbers[2])
```

A built-in function named `len()` takes the name of the list as its input and returns its length. This can be used to figure out the last legitimate index of the list. Can you figure out what the code below intends to do and then repair it?

```python
fitness_data = ["Juliana", 7000, 5500, 10300, 8000, 1200, 2000, 5000]

first_index = 0
print(fitness_data[first_index])

last_index = len(fitness_data)
print(fitness_data[last_index])
```

### Solution:

```python
fitness_data = ["Juliana", 7000, 5500, 10300, 8000, 1200, 2000, 5000]

first_index = 0
print(fitness_data[first_index])

last_index = len(fitness_data) - 1
print(fitness_data[last_index])
```

> Subtracting 1 from the length to account for the index that will count the number of items in the list (8), but since Python is zero indexed, there are only (7) indexes, 0 through 7. 

## Appending and Removing an Element

Till now, we've learned how to create a list, as well as how to access its elements through indexing. We've also seen how a built-in function can return us the length of a list. But what if we want to append an element to a list that has already been created? Similarly, what if we want to remove an element from a list?

For that, Python gives us very handy built-in methods for lists. Using the following format, we can append an element to the list with the `append()` method: `<name of the list>.append()`. We can replace the `name of the list` placeholder with our list name (e.g. the `week_without_Saturday` or the `fitness_data` list.)

> In the following code widget, let's look closely at what *line 4* is supposed to do to the `week_without_saturday` list. It appends "`Saturday`" to the list. On **line 10**, the `remove()` methods remove `"juliana` from the `fitness_data` list. We can run the code to compare the lists before and after the action.

```python
week_without_Saturday = ["Sunday" , "Monday", "Tuesday", "Wednesday", "Thursday", "Friday"]
print(week_without_Saturday)

week_without_Saturday.append("Saturday")
print(week_without_Saturday)

fitness_data = ["Juliana", 7000, 5500, 10300, 8000, 1200, 2000, 5000]
print(fitness_data)

fitness_data.remove("Juliana")
print(fitness_data)
```

## Review of the Lesson

We’ve learned one of the most important and widely used data structures called lists. We now know how data gets stored in a list, and we know how to access its individual elements remaining within the legitimate length of the list. However, the difficulty of computing minimum, maximum, and average still remains. Though we don’t have to remember all the different variable names now. But will we need to access every element individually if we want to compare or add elements? Of course not. Let’s find out how to efficiently use lists to tackle problems like this in the next lesson.

# Using the `for` Loop for Traversing the Lists

> Learn how to effectively deal with repetitive blocks of code.

## The Project Requires Summing the Daily Steps of a User

We now know how to store our client's data inside our Python program--we use a list. It kind of looks like this:

```python
fitness_data = ["Juliana", 7000, 5500, 10300, 8000, 1200, 2000, 5000]
```

This reads `fitness_data` as a list that shows `Juliana's` steps taken in a week, with `7000` steps taken on Sunday, `5500` taken on Monday, and so on up to Saturday, where `5000` steps were taken. 

The project requires our program to be able to compute the average number of steps as part of the performance statistics.

## Slicing Up a List

But as we can see, all this data is stored in a single `fitness_data` named list with mixed data types: `Juliana` is a string, while there's a long list of integers after that. If there was a way to slice out those integers, everything from index 1 (skipping `Juliana`) to the last index of the list, and make another neat list with just the count of steps per day, it would become easier to think of an algorithm to compute the sum of those numbers. 

> Python let's us do this with ease. Remember how one element is accessed using the name of the list followed by enclosing the index or location of the element within square brackets `[]` (e.g. `fitness_data[1]`). Here's a code example:

```python
fitness_data = ["Juliana", 7000, 5500, 10300, 8000, 1200, 2000, 5000]
one_element = fitness_data[1]
print(one_element)

#output: 7000
```

**Line 2** extracts the value at index `1` of `fitness_data` and assigns it to the `one_element` variable. If we want to slice out more than one element from the bigger list, we need to tell Python the range of indexes where we want to slice the list inside the square bracket (in **line 2**) separated by a colon (`:`).

```python
fitness_data = ["Juliana", 7000, 5500, 10300, 8000, 1200, 2000, 5000]
slice_list = fitness_data[1:3]
print(slice_list)

# [7000, 5500]
```

**Line 2** slices up the `fitness_data` list. It can be read as follows: get every item between indexes `1` and `3` (*excluding the values at indexes `1` and `3`*) from the `fitness_data` list and assign them to the new `slice_list` list.

## Challenge

Can you use the built-in function `len()` to find out the last legitimate index and slice the entire list except for `"Juliana"` and print that sliced list in the code widget below?

```python
fitness_data = ["Juliana", 7000, 5500, 10300, 8000, 1200, 2000, 5000]
list_daily_steps = []
# Write your code here to correctly assign the slice to list_daily_steps

print(list_daily_steps)
```

### Solution:

```python
fitness_data = ["Juliana", 7000, 5500, 10300, 8000, 1200, 2000, 5000]
list_daily_steps = []

# Write your code here to correctly assign the slice to list_daily_steps
length_list = len(fitness_data)
list_daily_steps = fitness_data[1:length_list]
print(list_daily_steps)

# [7000, 5500, 10300, 8000, 1200, 2000, 5000]
```


> [!NOTE] len()
> The advantage of using the built-in function `len()` to figure out the last index makes our code general, which means the same code would work if the original list has 7, 24, 168, or however many numbers. ***Good programmers almost always want to avoid hard coding whenever the code can be made general.***

## One Iteration over the Entire List

> By now, we have a sliced list with us, which just has the number of steps taken per day of the week by a user.

```python
list_daily_steps = [7000, 5500, 10300, 8000, 1200, 2000, 5000]
```

For computing important summary statistics, our Python code needs to access each element one by one, from the first to the last. Can you think of any other way we can compute the total number of steps a user has taken over the whole week?

The world will be so delighted to know if there's any other way except for picking the first element, then the second, then the third, till we get to the very last element of the list, and to keep adding the tally along the way. 

## We Already Know the `while` Loop

Can you work out the pattern for accessing each element of the list? Let’s first print each element one by one.

```python
list_daily_steps = [7000, 5500, 10300, 8000, 1200, 2000, 5000]

index = 0
print(list_daily_steps[index])
index = index + 1
print(list_daily_steps[index])
index = index + 1
print(list_daily_steps[index])
index = index + 1
print(list_daily_steps[index])
index = index + 1
print(list_daily_steps[index])
index = index + 1
print(list_daily_steps[index])
index = index + 1
print(list_daily_steps[index])

# 7000 
# 5500 
# 10300 
# 8000 
# 1200 
# 2000 
# 5000 
```

> Clearly, this code does the job, but at the same time, this isn't the effective and most efficient way of writing code because the lines keep repeating. 

```python
list_daily_steps = [7000, 5500, 10300, 8000, 1200, 2000, 5000]
index = 0
# Write your code here

while(index < len(list_daily_steps)):
    print(list_daily_steps[index])
    index = index + 1
```

Notice that the code will work fine even if we have less than or more than eight elements in the list. This shows that our code is generic and can be used for any list, no matter how long.

### Things that can go wrong using a `while` loop[#](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/5866937438568448/5818148916953088#Things-that-can-go-wrong-using-a-while-loop)

No doubt that being able to write code that can iterate over lists is a milestone in our coding journey. But there are a lot of things that can go wrong in just five lines of code while using a `while` loop over a list:

- We might end up creating an infinite loop.
- We might miss some elements of the list.
- We might start and end the loop incorrectly.
- We might set up an incorrect logic condition for the while loop.

## Running the `for` Loop On a List

> Python gives us the `for` loop for lists. It does away with most of the problems listed above. Let's prove this with code. 

```python
list_daily_steps = [7000, 5500, 10300, 8000, 1200, 2000, 5000]
for steps in list_daily_steps:
	print(steps)
```
```python
#output
7000 5500 10300 8000 1200 2000 5000
```

### Code Explanation

- **Line 2**: This shows the syntax of Python's `for` loop. `for` and `in` are the two important keywords here. A `steps` named variable is used as a placeholder. Because it's a loop, we can image each element of the `list_daily_steps` list getting assigned to this variable, one by one, in every iteration of the loop. Because multiple lines of code can be wherein within the scope of a `for` loop, just like a `while` loop, **line 2** ends with a colon (`:`).
- **Line 3:** This shows what the `for` loop has to do every time it iterates over the list. It simply prints the values of the list, starting from `7000` up to the last element. 


> [!NOTE] Python
> Python is known as a high-level language, mainly because it comes close to natural languages like English. Try reading the `for` loop sentences. In English, it reads: for each element in the list, print the element.

## Challenge

You’re given a new list that has each day of the week. In just two additional lines of code, can you print each day of the week one by one using a `for` loop?

```python
days_of_week = ["Sunday" , "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"]
# Write your code that use a for loop to print each day of the week here
for day in days_of_week:
	print(day)
```
```Python
# output
Sunday Monday Tuesday Wednesday Thursday Friday Saturday
```

### Implementing The For Loop With a `range()`

There's no doubt that a `for` loop in Python is way more advanced than a simple `while` loop, especially when a list is involved, but there's another thing a `while` loop lets us do. It lets us set a loop with a *predescribed range*. 

- For instance, if we want to print a count from zero to nine, here's how we can do that:

```python
index = 0
while index <= 9:
	print(index)
```

With Python's built in `range()` function, we can do the same using a `for` loop as well. It's because the `range()` method takes a number as input *and returns a list of all numbers*. The `for` loop then iterates over the returned list, where the elements of the list are the range of numbers. The following code uses the `range(10)` function call to print integers to 10, starting from 0. 

```python
for index in range(10):
	print(index)
```
```
# Output
0 1 2 3 4 5 6 7 8
```

## Review of the lesson[](https://www.educative.io/module/page/k5m3gAColoJZZj89Y/10370001/5866937438568448/5818148916953088#Review-of-the-lesson)

In summary, a `for` loop is a powerful construct that simplifies the process of iterating over elements in a sequence, like a list or a range. It allows us to perform the same operation for each element without explicitly specifying the iteration logic, making the code concise, readable, and, more importantly, less prone to bugs. We’ve only used the `print()` method inside the loop, but you’re encouraged to use loops on lists to create cool algorithms to fulfill important project requirements. Our AI mentor will be right beside you.

# Solving Problems Algorithmically

> Solve some problems algorithmically with code.

## The Most Fundamental Skill of a Programmer

As a budding programmer, it's important to recognize problem-solving as the cornerstone of your skill set. Imagine it as the *driving force behind your journey into the world of coding.* At it's core, programming revolves around addressing challenges and creating solutions.

This skill involves not just writing lines of code but delving into the art of designing algorithms. Think of algorithms as ***step by step guides, line recipes, that outline the path to solving a problem.*** Your ability to craft these algorithms is similar to the chef's mastery of creating a perfect recipe. However, the magic truly happens when you transform these algorithms into executable code. 


> [!NOTE] Note
> Translating the logical solutions (algorithms) into lines that a computer can understand (code) is the livelihood of a programmer.

It's where abstract ideas meet the tangible world of technology. Embracing problem solving, algorithm design, and coding as intertwined essentials will be the solid basis of your proficiency as a programmer. It enables you to navigate the vast landscape of software development with confidence and creativity.

## Problem Solving this Lesson

This lesson aims to give you an experience of what problem solving looks and feels like in the programming world. It does so by making you go through the problem-solving exercise five times. 

All five problems are critical project requirements, such as finding the sum of the steps, finding the minimum steps taken in a week, finding the maximum steps, finding the average of the week, and categorizing the learners into three bands. These tasks might seem trivial to humans because we can look at a list of five numbers and find the largest or smallest value right away. 

However, things work differently for computers that can pick values only one by one and compare only two of them at a time. So, we need to break down the problem into steps that the computer can follow to solve the problem at hand.


# Data Science Project: Attempt 1:

![](https://i.imgur.com/Ey7I418.png)

## Getting Started with the Project:

> [!NOTE]
> So far, we've learned all these concepts using just one instance of the data, we'll use one of those instances to perform data analysis for this lesson, but we'll use a realistic data given by our client.

```
Juliana,857,1178,1134,1133,780,1017,821,1180,0,0,0,0,0,0,0,1032,42,1129,1126,40,1032,743,1194,993,1054,969,1046,924,1064,1117,1094,795,0,0,0,0,0,0,44,26,47,736,22,46,851,27,846,769,1071,942,1010,1055,1011,834,1104,889,0,0,0,0,0,1120,38,1190,1100,959,874,1130,941,813,1106,934,1117,1043,1053,997,1055,1043,824,1183,908,0,0,0,0,0,0,0,937,1188,1145,747,1109,20,984,812,1059,742,739,926,1188,1072,1113,938,0,0,0,0,0,1067,26,29,45,722,796,32,28,36,1094,896,798,1101,963,928,829,842,1136,1115,0,0,0,0,0,0,0,27,769,26,1133,830,20,43,869,924,990,1000,963,768,1003,754,788,0,0,0,0,0,0,33,35,37,853,50,797,35,21,46,950,1099
```

What requirements can we fulfill at this point?

1. We can partially work on requirement 2 by storing the data in lists (we don’t know about dictionaries yet).

2. We can also compute a statistics summary for a member’s daily activity (requirement 3).

3. We can categorize the members into groups based on their week’s performance. For example, given a threshold of 5000 steps, we can print the list of members that lie in zones red, yellow, or green (requirement 4b).

We'll work on these requirements one by one and by the end of this lesson, we'll also be able to appreciate more Pythonic ways of coding, leveraging it's built-in functions like `sum()`, `max()`, and `min()` that come in very handy when dealing with lists.

So without further ado, let's get started!
### Storing daily steps in a list

For requirement 2, proceed in two steps. In **step 1**, separate the user name and hourly data. In **step 2**, reduce the long hourly list of data to a neater daily list of steps because most of the data analysis is to be done on daily steps, not hourly steps. Complete step 1 in the code widget below. The idea is to initialize a `name` variable with the first element of the `data` list. The rest of the data, beyond the very first element, should be assigned to another `hourly_steps` named variable/list.

```Python
data = ["Juliana",857,1178,1134,1133,780,1017,821,1180,0,0,0,0,0,0,0,1032,42,1129,1126,40,1032,743,1194,993,1054,969,1046,924,1064,1117,1094,795,0,0,0,0,0,0,44,26,47,736,22,46,851,27,846,769,1071,942,1010,1055,1011,834,1104,889,0,0,0,0,0,1120,38,1190,1100,959,874,1130,941,813,1106,934,1117,1043,1053,997,1055,1043,824,1183,908,0,0,0,0,0,0,0,937,1188,1145,747,1109,20,984,812,1059,742,739,926,1188,1072,1113,938,0,0,0,0,0,1067,26,29,45,722,796,32,28,36,1094,896,798,1101,963,928,829,842,1136,1115,0,0,0,0,0,0,0,27,769,26,1133,830,20,43,869,924,990,1000,963,768,1003,754,788,0,0,0,0,0,0,33,35,37,853,50,797,35,21,46,950,1099]
```

The code above gives the hourly steps of a single member. But now you need to convert their hourly steps to daily steps. How do you think you can do that? The idea is to define a function `hourly_to_daily_steps()` and pass it `hourly_steps` as its input argument, and the function returns to `daily_steps` list. Can you complete this function definition by iterating over the input list in slices of 24 and summing those 24 numbers each time, and appending the sum to `daily_steps` each time?

```python
def hourly_to_daily_step(hourly_steps):
  daily_steps = []
  # Write your code here
  for i in range(0, len(hourly_steps), 24):
    day_counts = sum(hourly_steps[i:i+24])
    daily_steps.append(day_counts)
  return daily_steps

data = ["Juliana",857,1178,1134,1133,780,1017,821,1180,0,0,0,0,0,0,0,1032,42,1129,1126,40,1032,743,1194,993,1054,969,1046,924,1064,1117,1094,795,0,0,0,0,0,0,44,26,47,736,22,46,851,27,846,769,1071,942,1010,1055,1011,834,1104,889,0,0,0,0,0,1120,38,1190,1100,959,874,1130,941,813,1106,934,1117,1043,1053,997,1055,1043,824,1183,908,0,0,0,0,0,0,0,937,1188,1145,747,1109,20,984,812,1059,742,739,926,1188,1072,1113,938,0,0,0,0,0,1067,26,29,45,722,796,32,28,36,1094,896,798,1101,963,928,829,842,1136,1115,0,0,0,0,0,0,0,27,769,26,1133,830,20,43,869,924,990,1000,963,768,1003,754,788,0,0,0,0,0,0,33,35,37,853,50,797,35,21,46,950,1099]

name = data[0]
hourly_steps = data[1:]

daily_steps = hourly_to_daily_step(hourly_steps)
print("Daily steps:", daily_steps)
```
```
Daily steps: [15431, 11477, 18121, 16165, 12548, 12353, 10222]
```

```python
def hourly_to_daily_step(hourly_steps):
  daily_steps = []
  # Write your code here
 for i in range(0, len(hourly_steps), 24): # this loop uses jumps of 24 ineach iteration
	day_counts = sum(hourly_steps[i:i+24]) # sums up a slice of 24 numbers
    daily_steps.append(day_counts) # appends the summed up number to daily_steps list
  return daily_steps
```

### Computing statistics summary

When computing the maximum, minimum, and average number of steps of the member, the interesting part is that instead of having to write user-defined functions, you can simply use the built-in functions of Python. **Line 14** does that using the `max()` function. Can you complete the code for minimum and average?

```python
def hourly_to_daily_step(hourly_steps):
    daily_steps = []
    for i in range(0, len(hourly_steps), 24):
        day_counts = sum(hourly_steps[i:i + 24])
        daily_steps.append(day_counts)
    return daily_steps

data = ["Juliana",857,1178,1134,1133,780,1017,821,1180,0,0,0,0,0,0,0,1032,42,1129,1126,40,1032,743,1194,993,1054,969,1046,924,1064,1117,1094,795,0,0,0,0,0,0,44,26,47,736,22,46,851,27,846,769,1071,942,1010,1055,1011,834,1104,889,0,0,0,0,0,1120,38,1190,1100,959,874,1130,941,813,1106,934,1117,1043,1053,997,1055,1043,824,1183,908,0,0,0,0,0,0,0,937,1188,1145,747,1109,20,984,812,1059,742,739,926,1188,1072,1113,938,0,0,0,0,0,1067,26,29,45,722,796,32,28,36,1094,896,798,1101,963,928,829,842,1136,1115,0,0,0,0,0,0,0,27,769,26,1133,830,20,43,869,924,990,1000,963,768,1003,754,788,0,0,0,0,0,0,33,35,37,853,50,797,35,21,46,950,1099]

name = data[0]
hourly_steps = data[1:]
daily_steps = hourly_to_daily_step(hourly_steps)

daily_max = max(daily_steps)
# Write your code here for computing the daily_min and daily_avg
daily_min = min(daily_steps)
daily_avg = sum(daily_steps) / len(daily_steps)

print(name + "'s daily steps:", daily_steps)
print("Summary stats for", name)
print("Max: ", daily_max)
# Write your code here for printing daily_min and daily_avg
print("Min: ", daily_min)
print("Average: ", daily_avg)
```
```
Juliana's daily steps: [15431, 11477, 18121, 16165, 12548, 12353, 10222] 
Summary stats for Juliana 
Max: 18121 
Min: 10222 
Average: 13759.57142857143
```

> Here’s one last requirement to take care of.

### Categorizing data based on steps

This brings you to the third requirement where you categorize the members based on their performance. But the question is: on what basis do you evaluate the performance? Instead of the total step counts, it makes more sense to categorize based on the overall average step counts of the users. Assuming that each member should at least walk a sum of 5000 steps on average in a week, you can categorize them as follows:

- Any member falling short of 5000 average steps lies in the `concerning` zone.
- Any member with more than or equal to 5000 average steps but less than 10000 steps lies in the `average` zone.
- Any member with more than 10000 average steps lies in the `excellent` zone.

So for these categories, create a function called `choose_categories()` that assigns categories `concerning`, `average`, or `excellent` based on the number of steps in the daily average (`daily_avg`).

```python
def hourly_to_daily_step(hourly_steps):
    daily_steps = []
    for i in range(0, len(hourly_steps), 24):
        day_counts = sum(hourly_steps[i:i + 24])
        daily_steps.append(day_counts)
    return daily_steps

def choose_categories(steps):
    category = ""

    # Write your code here
    if steps < 5000:
      category = "Concerning"
    elif 5000 <= steps < 10000:
      category = "Average"
    else:
      category = "Excellent"
    return category

data = ["Juliana",857,1178,1134,1133,780,1017,821,1180,0,0,0,0,0,0,0,1032,42,1129,1126,40,1032,743,1194,993,1054,969,1046,924,1064,1117,1094,795,0,0,0,0,0,0,44,26,47,736,22,46,851,27,846,769,1071,942,1010,1055,1011,834,1104,889,0,0,0,0,0,1120,38,1190,1100,959,874,1130,941,813,1106,934,1117,1043,1053,997,1055,1043,824,1183,908,0,0,0,0,0,0,0,937,1188,1145,747,1109,20,984,812,1059,742,739,926,1188,1072,1113,938,0,0,0,0,0,1067,26,29,45,722,796,32,28,36,1094,896,798,1101,963,928,829,842,1136,1115,0,0,0,0,0,0,0,27,769,26,1133,830,20,43,869,924,990,1000,963,768,1003,754,788,0,0,0,0,0,0,33,35,37,853,50,797,35,21,46,950,1099]

name = data[0]
hourly_steps = data[1:]
daily_steps = hourly_to_daily_step(hourly_steps)

daily_max = max(daily_steps)
daily_min = min(daily_steps)
daily_avg = sum(daily_steps)/len(daily_steps)

print(name + "'s daily steps:", daily_steps)
print("Summary stats for", name)
print("Max: ", daily_max)
print("Min: ", daily_min)
print("Average: ", daily_avg)

# Calling the function and printing the output
category = choose_categories(daily_avg)
print("Performance of", name, "this week:", category)
```

# Import Libraries

## Reading Data From a File

Learn how to read data from an external file.

### The Project Requires us to Read Data from an External File

As budding data scientists, we know how to use lists to store a collection of data and how to traverse the lists to compute summary statistics. That's an important skillset.

But in reality, how will the lists that reside within our Python code files get to be properly initialized with our client's data? Our clients don't have access to our Python code, and even if they do, they're not Python programmers. We can't assume that our clients will populate the lists inside our Python code using the correct Python syntax. Instead, the client can only email use their data file.

It's an equally important skillset for a data scientist to be able to read dataset file programmatically. This lesson intends to teach that important skill and, in the process, fulfill two important project requirements:

![](https://i.imgur.com/o8MFV3V.png)

### Programming as a Social Activity

Programming is a *social phenomenon*, and this aspect is often neglected. Python insists on focusing on this social side of programming in two important ways. First, by insisting that every Python programmer consistently uses indentations within their program. This shows that our code is not simply for a machine's consumption; it's also for other human programmers who are going to have to go through our code. Therefore, code readability is an important design element in the Python ecosystem. 

Secondly, Python has given birth to a vast open-source community that makes their pieces of code available for other member's usage. This way, not everyone in the Python world needs to keep reinventing the same code.

### Importing Libraries Others Have Written

Python already has some **built-in functions** to help make our life as programmers easier. Imagine printing something on the screen without the `print()` function being available. Imagine taking input from the user through the keyboard without the `input()` function being available. This built-in function makes our life as programmers easy because we can then just use a variable and assign it the data that streams from the keyboard.

Similarly, someone in the world has already written a function that takes input from a file instead of a keyboard. They haven't just written one function; they've written a whole library of functions and made it available. We can use these built-in functions to read data, and then it becomes so easy to simply assign that data to an appropriate variable or a data structure, as we'll see shortly. TO use functions written by someone else, we need to import their libraries into our code. This way, our program will be able to read the imported library to get the required function whenever prompted. 

## Loading one Data Element into a Variable

Imagine a very simple scenario. There's a `data.txt` named external file that has only **one value stored in it**. We want to load that value from the `data.txt` file right into our program in one of our variables. Once we have the data in one of our variables inside our own code, we can do something meaningful with it, but without this important step, we'd be helpless even if we know all the programming required to fulfill our client's other requests. 

The library we import is a very famous library that a lot of data scientists use: the **NumPy** (`numpy`) library. **NumPy** is a powerful library for numerical operations in Python. It equips us with a variety of functions and tools to implement complex mathematical operations. At the moment, we're interested in calling NumPy's `loadtxt()` named function, which can take many input arguments including a file name. So, it makes total sense that we'd have to tell `loadtxt()` the name of the file from which we want to load the data. Run the following code to see what gets printed on the screen.

```python
import numpy

data = numpy.loadtxt('data.txt')

print(data)
```
```
7.0
```

- Line 1 simply tells the computer that we want to import `numpy` as a library.
- Line 3 first tells the computer that `loadtxt()` if a function of the numpy library when it makes the `numpy.loadtxt()` function call. It then tells the `numpy.loadtxt()` function that the name of the file is `data.txt`. Because there is only one data value in the `data.txt` file, it makes sense to assign it to a `data` *named variable*. 
- Line 5: prints the value in the `data` variable to the screen.

## Loading Two Data Values into Two Variables

What if we had two values in our external file? Would we still use a single variable? You're right! We'd have to use two variables. Do you notice an additional input argument to the `loadtxt()` function? Seek the AI Mentor's review after running the following code.

```python
import numpy

num1, num2 = numpy.loadtxt('data.csv', delimiter = ',')

print(num1, num2)
```
```
7.0 11.0
```

## Loading One Long Row of Data into a List

What if, like it is with our client's data, we had to read 168 values from the `data.csv` file? Would we set up 168 variables in **line 3** below? Notice how we don’t have to change the code, and Python decides on our behalf that since many comma-separated values are being read from the file, and we’re assigning them to one variable that we’ve named `data` in **line 3**, it has to be a list data structure.

```python
import numpy

data = numpy.loadtxt('data.csv', delimiter = ',')

print(data)
```

Notice when you click the “Run” button, the output on the screen has a lot of numbers, but the output starts (`[`) and ends (`]`) with square brackets (`[]`). That’s how we know that `data` is a list. But how many numbers are there in the list altogether? Or, in other words, what’s the length of the list? In the code widget above, can we use the built-in function `len()` to print the length of `data`?

```python
import numpy

data = numpy.loadtxt('data.csv', delimiter = ',')

print(len(data))
```
```
168
```

## Loading a Row of Data with Mixed Data Types

Great! We just need one more piece to complete the puzzle. The data we’ve read from a file so far only had integers, but the data that the fitness company has provided contains integers to represent the number of steps and strings to represent the names of users. Can we use the same code to read data that contains mixed types of data? Let’s try.

```python
import numpy

data = numpy.loadtxt('data.csv', delimiter = ',')

print(data)
```

Oops! We ran into an error. Let’s see what it is. The last line in the error that popped up says, `could not convert string to float: 'Juliana'`. Apparently, Python tried to convert the name from a string into a floating point value, but a name cannot be stored as a number and, therefore the error. Can you think of a variable type that can keep both numbers and names? Yes! Strings can do that for us. But how do we tell Python that it should read our data as a string and not try converting it to a floating point value? It turns out that we can send an additional parameter named `dtype` to the `loadtxt()` function. We can assign it the value `int`, `float`, or `str` to specify the data type it should use while reading the data. The code below shows the use of the `dtype` parameter.

```python
import numpy

data = numpy.loadtxt('data.csv', delimiter = ',', dtype = 'str')

print(data)
```
```
['Juliana' '685' '0' '0' '0' '0' '0' '0' '0' '0' '964' '934' '21' '623' '1085' '989' '1113' '599' '667' '869' '1192' '86' '402' '1040' '1065' '953' '903' '0' '0' '0' '0' '0' '0' '631' '1178' '410' '447' '1013' '952' '482' '67' '62' '1164' '977' '1127' '970' '22' '403' '665' '762' '0' '0' '0' '0' '0' '0' '0' '0' '649' '1029' '1133' '1000' '802' '946' '675' '768' '743' '786' '41' '856' '868' '209' '1097' '469' '217' '0' '0' '0' '0' '0' '0' '0' '495' '241' '941' '495' '583' '380' '84' '421' '431' '502' '62' '345' '923' '492' '856' '926' '1150' '0' '0' '0' '0' '0' '0' '0' '0' '1146' '742' '986' '300' '489' '1056' '95' '1083' '905' '749' '77' '213' '270' '278' '0' '0' '0' '0' '0' '0' '0' '0' '340' '960' '631' '795' '1055' '585' '981' '423' '35' '92' '1003' '40' '490' '1092' '579' '698' '0' '0' '0' '0' '0' '0' '1072' '326' '491' '768' '39' '442' '466' '1077' '735' '377' '258' '370' '1191' '81' '93' '440' '488' '1184']
```

> The `dtype` parameter of the `loadtxt()` function allows us to choose the data type of the imported data. The options are `int`, `float` and `str`.

Great! It can read the data now, and as is evident from the quotes (`''`) in print formatting, even the numbers of steps were read as strings. We can also verify the data type of an element of data using the `type()` function.

### Challenge

All of the data that we’ve loaded has the `str` data type. However, to make calculations with the data, we need the step counts to be in `int` or `float` data type. After splitting the list that we’ve loaded into a username and counts list, can you figure out a way to convert the list of strings into a list of integers? You can seek a hint and then the solution, if required.

```python
import numpy

data = numpy.loadtxt('data.csv', delimiter = ',', dtype = 'str')

name = data[0]
steps = data[1:]

# Write your code to change the data type here
steps = steps.astype(int)
print(type(steps[0]))
```

> The `astype` function call converts the array of strings into an array of integers.

> [!NOTE]
> That’s a wonderful milestone. As budding scientists, we now know how to read our client’s data from an external file in our program and load that external data into a list inside our program. We also know how to compute important statistics once we’ve loaded the data into a list.

# Dictionaries in Python

Learn about dictionaries, another efficient way to manage large, meaningful datasets.

## Another Look at the Structure of Data

Let’s take another look at the data. What kind of characteristics stand out? We can tell that `Juliana` has a unique place within the dataset. So does `Lucy`, and so on, right up to `Omer`. These names can uniquely identify _something_. That _something_ is one long list of steps taken per hour in the whole week.

![](https://i.imgur.com/dzTqi3l.png)

> [!NOTE] Data Characterization
> This dataset has unique names, against each unique name, there's a list of 168 numbers.

> [!Caution] Bad Idea
> Just as having 168 separate variables was a bad idea to store 168 sequences of numbers, and the list as a data structure came out to rescue, it seems like an equally bad idea to have 10 or 100 separately named lists within our code, one representing each user within the client’s data. Imagine if they had thousands of users. What would our code look like?

## Dictionary

Instead of representing such kinds of data structure for our data as lists of lists, Python gives us another data structure called a **dictionary**. As the name implies, every entry in the dictionary has a unique *word*, and against each of those unique words, there's an associated *definition*. Python's dictionary calls the unique word the **key** and the definition a **value**. So, a dictionary, as a data structure, has comma-separated `key:value` pairs enclosed with curly braces.

### Dictionary Demystified

From our usual `fitness_list` structure, let's create two variables: Store the name of the user as `key` and their steps taken during the week as `value`. Focus on the syntax for creating an empty dictionary on **line 7**, followed by how we assigned `value` to `key` inside of the `fitness_dictionary` named dictionary on **line 8**.

```python
fitness_list = ["Juliana", 7000, 5500, 10300, 8000, 1200, 2000, 5000]
print("List looks like ", fitness_list)

key = fitness_list[0]
value = fitness_list[1:]

fitness_dictionary = {}
fitness_dictionary[key] = value

print("Dictionary looks like", fitness_dictionary)
```

#### Dictionary with Two Users

```python
fitness_list1 = ["Juliana", 7000, 5500, 10300, 8000, 1200, 2000, 5000]
fitness_list2 = ["Ulises", 347, 625, 729, 977, 0, 0, 0]

key1 = fitness_list1[0]
value1 = fitness_list[1:]
key2 = fitness_list2[0]
value2 = fitness_list[1:]

fitness_dictionary = {}
fitness_dictionary[key1] = value1
fitness_dictionary[key2] = value2

print("Dictionary looks like", fitness_dictionary)
```
```
Dictionary looks like {'Juliana': [7000, 5500, 10300, 8000, 1200, 2000, 5000], 'Ulises': [347, 625, 729, 977, 0, 0, 0]}
```

Let's add the data for another user. We know how to put a key:value pair inside a dictionary, but how to we get something out of a dictionary? Similar to looking up an English dictionary, we need to know the word (key in our Pythonic world). If we know the name of the dictionary and the key, we can access the value. It's just like accessing one element of a list. It's just that a list requires an *index*, and a dictionary stores data based on keys; the syntax otherwise is just the same using square brackets: `dictionary_name[key]`.

```python 
fitness_list1 = ["Juliana", 7000, 5500, 10300, 8000, 1200, 2000, 5000]
fitness_list2 = ["Ulises", 347, 625, 729, 977, 0, 0, 0]
fitness_list3 = ["Christine", 214, 665, 373, 1095, 349, 1037, 0]

key1 = fitness_list1[0]
value1 = fitness_list[1:]
key2 = fitness_list2[0]
value2 = fitness_list[1:]
key3 = fitness_list3[0]
value3 = fitness_list3[1:]

fitness_dictionary = {}
fitness_dictionary[key1] = value1
fitness_dictionary[key2] = value2
fitness_dictionary[key3] = value3

print("Accessing the value stored against one key", fitness_dictionary["Ulises"])
```
```
Accessing the value stored against one key [347, 625, 729, 977, 0, 0, 0]
```
> Notice what gets printed when we print `fitness_dictionary["Ulises"]` on **line 17**: some comma-separated values enclosed within square brackets. It’s a list!

The real power of the dictionary is that instead of the data being stored in three different lists, it now resides neatly within one data structure, which means we can do things using one dictionary, which we can't imagine doing with separate lists. 

For instance, can you think of creating one simple `for` loop that traverses through all the lists? At the moment, we only have three user's data. Imagine if we had the data for hundreds of users. Notice the magic that can now happen on **lines 17-18**.

```python
fitness_list1 = ["Juliana", 7000, 5500, 10300, 8000, 1200, 2000, 5000]
fitness_list2 = ["Ulises", 347, 625, 729, 977, 0, 0, 0]
fitness_list3 = ["Christine", 214, 665, 373, 1095, 349, 1037, 0]

key1 = fitness_list1[0]
value1 = fitness_list1[1:]
key2 = fitness_list2[0]
value2 = fitness_list2[1:]
key3 = fitness_list3[0]
value3 = fitness_list3[1:]

fitness_dictionary = {}
fitness_dictionary[key1] = value1
fitness_dictionary[key2] = value2
fitness_dictionary[key3] = value3

for user in fitness_dictionary:
    print(user, "took following steps per day: ", fitness_dictionary[user])
```
```
Juliana took following steps per day: [7000, 5500, 10300, 8000, 1200, 2000, 5000] Ulises took following steps per day: [347, 625, 729, 977, 0, 0, 0] 
Christine took following steps per day: [214, 665, 373, 1095, 349, 1037, 0]
```

> [!NOTE] **Dictionary syntax summarized:**  
> Create a dictionary using the `dictionary_name = {}` syntax.  
> Add a key:value pair to a dictionary using the `dictionary_name[key] = value` syntax.  
> Access the value stored against a unique key using the `dictionary_name[key]` syntax, where `dictionary_name`, `key`, and `value` are variable names you can choose appropriately

## Loading Data from an External File into a Dictionary

Well, we know how to create a dictionary, add data to it, and access individual dictionary elements, but how would we automate this for the dataset given by our client in the `steps.csv` file, which is an external file? In the previous lesson, we learned how to read data from a file. The data was initially read as lists of strings, but we filtered out the name of the user as a string and changed the data type of the remaining elements in the list (step counts) to integers. Now, what we need to do is to store that data in a dictionary. It seems pretty straightforward. We can keep the names as the keys and the list of steps as values in the dictionary.

To automate this task for the whole dataset, we can run a `for` loop over the number of lists in the data. In each iteration, we can pick an element from the dataset, split it into a name and a list of steps, and save them in a dictionary. The following code does that.

```python
import numpy

# Reading data from a file
data = numpy.loadtxt("steps.csv", delimiter = ",", dtype = str)

# adding data to dictionary
data_dict = {}
for i in range(1, len(data)): # choosing 1 instead of 0 to skip the header row
	row = data[i]
	name = row[0] # <---- extracting name
	steps = numpy.array(row[1:], dtype = int) # <- Extracting list of steps as int
	data_dict[name] = steps # <- adding key:value pair to the dictionary
print(data_dict)
```
```
{'Ulises': array([ 0, 0, 0, 0, 45, 26, 267]), 'Alice': array([ 0, 0, 0, 448, 26, 26, 36])}
```

In this code snippet, we are reading data from a CSV file named “steps.csv” using the NumPy library. The data in the CSV file is loaded into a NumPy array called ‘data’. Each row in the array represents a person, where the first element is the person’s name and the subsequent elements are numeric data representing steps taken.

To store this data in a more structured way, we are using a Python dictionary named ‘data_dict’. A dictionary is a collection of key-value pairs where each key is unique. In this case, we are using the person’s name as the key and the list of steps taken as the value.

Here’s a breakdown of how the dictionary ‘data_dict’ is populated:

1. We initialize an empty dictionary ‘data_dict’.
2. We iterate over the rows in the ‘data’ array starting from index 1 (skipping the header row).
3. For each row, we extract the name of the person from the first element of the row.
4. We extract the list of steps taken by the person from the remaining elements of the row and convert them to integers using NumPy’s ‘dtype=int’.
5. We add a new key-value pair to the ‘data_dict’ dictionary, where the key is the person’s name and the value is the list of steps taken.
6. Finally, we print out the populated ‘data_dict’ dictionary.

This code demonstrates how dictionaries can be used to store and organize data in a meaningful way, making it easy to retrieve and manipulate information based on unique keys. It’s a fundamental concept in Python programming and is widely used in various applications for data storage and retrieval.

## Power of Generic Code

For demo purposes, the `steps.csv` file in the previous section had very limited data. It only had seven values of steps for only three users. In the following code widget, click the `steps.csv` file to see what the client data actually looks like. 

It has 10 users, and for each user, it has hourly entries for steps taken in the whole week, i.e. 24 x7 = 168. However, the code that can read this larger dataset is exactly the same as before! We don't need to change anything because the code we wrote is generic. It would wok even if the data were for a month or a year instead of a week.

# Data Visualization

Learn how Python enables us to make visuals out of data.

## The Project Requires Data Visualization

One of the most important skills of a data analyst is to be able to plot and visualize the information for meaningful insights. Till now we only know how to print some values on the screen, whereas our client wants to see the following kind of visual plots and graphs to understand their users' fitness data. 

![](https://i.imgur.com/BATeOHc.png)

> [!NOTE]
> Click any of the graphs above to get further information about it. You can click the "Back to Home" button that appears on the screen to return.

## Matplotlib - Another Python Library

Python's community offers a fascinating library of functions in the **Matplotlib** (`matplotlib`) library for us budding data scientists. For this project, we're going to use the `pyplot` module from the `matplotlib` library. As the name `pyplot` implies, it's used for plotting in Python. Using the `pyplot` module, there are functions we can call in our code for plotting pie charts, bar charts, line and scatter plots, as well bubble plots.

### Pie Chart

Imagine we have a list of numbers stored in the `data` list. It's easy to simply print the list on the screen. However, some cognitive processes kick in when we see the same numbers in terms of the share of the whole pie number holds. Seek the guidance of your AI Mentor to review the code.

```python
from matplotlib import pyplot

data = [3, 4, 5]

pyplot.pie(data)
```

- In the first line, we are importing a module named `pyplot` from the `matplotlib` library. This module provides functions to create various types of plots, including pie charts.
- In the second line, we are creating a list named `data` with three values: 3, 4, and 5. This data will be used to create a pie chart in the next line.
- In the third line, we are using the `pyplot.pie()` function to plot a pie chart using the data from the `data` list. This function takes the data as input and generates a pie chart based on the values provided. 
- Overall, these three lines set up the environment to create a pie chart using `matplotlib` and `pyplot`, making it easy to visualize data in the form of a statistical graph.

### Bar Chart

Another typical visual representation of numeric data is through a bar graph, with one bar per data element in the list. Each bar's height is in accordance with its numeric value (in the `data` named list), while the bar's position on the x-axis is determined by the index mentioned in the other list (x-axis). Notice how different the same data looks in a bar chart than it looks in a pie chart. 

```python
from matplotlib import pyplot

data = [3, 4, 5]
x_axis = [1, 2, 3]

pyplot.bar(x_axis, data)
```

![](https://i.imgur.com/pBT9SUL.png)

What if we wanted to have textual names for the x-axis positions of the bar? Notice the change in the `x-axis` list below. Instead of the strings `a`, `b` and `c`, can you imagine Sunday, Monday, Tuesday, etc. given our project?

```python
from matplotlib import pyplot

data = [3, 4, 5]
x_axis = ["a", "b", "c"]

pyplot.bar(x_axis, data)
```

![](https://i.imgur.com/X015pxb.png)

## Scatter Plot vs. Line Plot

A **scatter plot** is a type of data visualization that displays individual points on a two-dimensional graph. Each point on the graph represents a single observation, and the position of the point is determined by the values of two variables. Once variable is plotted on the horizontal axis (x-axis), and the other variable is plotted on the vertical axis (y-axis).

```python
from matplotlib import pyplot

x_values = [1, 2, 3, 4, 5, 6, 7]
y_values = [3000, 6000, 5000, 8000, 11000, 9000, 10000]

pyplot.scatter(x_values, y_values)
```

![](https://i.imgur.com/q9X5k7S.png)

A **line plot** also known as a **line chart** or **line graph**, is a type of data visualization that displays the same data points as the scatter plot, but it goes on to connect those individual data points by straight line segments. It's particularly useful for showing trends and changes in data over a continuous interval of time. Notice how the code widgets above and below the same `x_values` and `y_values` lists.

```python
from matplotlib import pyplot

x_values = [1, 2, 3, 4, 5, 6, 7]
y_values = [3000, 6000, 5000, 8000, 11000, 9000, 10000]

pyplot.plot(x_values, y_values)
```

In the above code widget, your _coding challenge_ is to plot the same `y_values` list that represents the steps taken in a day, but instead of the x-axis showing 1–7 numbers, it should display `3000` steps for `Sunday`, `6000` for `Monday`, and so on, till `10000` for `Saturday`.

```python
from matplotlib import pyplot

days_of_week = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"]
y_values = [3000, 6000, 5000, 8000, 11000, 9000, 10000]

pyplot.plot(days_of_week, y_values)
```

![](https://i.imgur.com/6eB05Hx.png)

### Bubble Plotting the Third Information

A **bubble plot**, also known as a **bubble chart**, is a type of data visualization that extends the concept of a scatter plot by adding a third dimension to the data points. In addition to the x-axis and y-axis, the size of the bubbles represents a third variable.

```python
from matplotlib import pyplot

x_values = [1, 2, 3, 4, 5, 6, 7]
y_values = [3000, 6000, 5000, 8000, 11000, 9000, 10000]
weight = [100, 150, 2000, 200, 400, 300, 250]

pyplot.scatter(x_values, y_values, weight)
```

![](https://i.imgur.com/2VSLkzm.png)

## Bar Chart - Coding Challenge

The challenge for you in this lesson is to read the daily steps data for a week from the `data_steps.csv` named file and make a bar plot with the name of days on the x-axis and step count on the y-axis. Do take a look at the `data_steps.csv` first and then correctly initialize `days` and `steps` before plotting them as a bar graph. Seek the solution, if required.

# Sorting Information

Learn about data sorting, an essential computer science problem.

Imagine we have 10 users whose total number of steps taken in the past week is stored in a list, a list length of 10. We can print the list on the screen. We also have the skill to display the same list as a bar chart. But one of our client's requirements is to see their users ranked, in order, from the least active to the most active.

![](https://i.imgur.com/LW3YWRn.png)

## How do we Sort?

Sorting is a classic computer science program. In this lesson, you will understand and partake in solving the classic problem that every computer scientist solves in their life. Interestingly, while life sometimes gives us problems, it often gives us solutions as well. In life, and there is definitely one outside of computers, almost all of us have played cards. We've held a hand of card dealt to us. Almost always, we're handed a random sequence of cards, and sometimes, we bring order to our hands.

## What's Happening Here?

We've seen and solved another classic problem before sorting. It's *searching*. We know what it takes to find the minimum, given a list of numbers. Can you spot the *find the minimum* operation at work in the cards illustration?

In reality, we don't have a deck of cards. Our client has given us fitness data. It has numbers that represent the steps taken by their users per day. Our client wants to be able to see their users ranked from least active to most active. We have an unordered list of numbers. If we can sort the list in ascending order, we can fulfill another one of our client's requirements. Let's start with a small list.

## Sorting Algorithm Envisioned

We have two lists `unsorted_list = [4, 2, 8]` and `sorted_list = []` to begin with. We want to find the minimum number is `unsorted_list` and append that number to `sorted_list`. Let's code it:

```python
def sort_list(unsorted_list):
	sorted_list = []

	min_value = min(unsorted_list)
	sorted_list.append(min_value)
	return sorted_list

steps = [4, 2, 8]
sorted_steps = sort_lists(steps)
print(sorted_steps)
```

Great, so the first step works. We've found the minimum value in a whole list and place it in its rightful sorted place. What do we need to do next? We know if, instead of doing it just once, we find the minimum in `sorted_list`, append it to the `sorted_list`, but do this **three times**, we'll have the sorted list. If we only add one `for` loop that *runs* till the *length* of the `unsorted_list`, and indet **lines 4 and 5**, we'll have the following code. Run the code to see what gets printed when we make the `sort_lines([4, 2, 8])` function call. 

```python
def sort_list(unsorted_list):
	sorted_list = []
	for i in range(len(unsorted_list)):
		min_value = min(unsorted_list)
		sorted_list.append(min_value)
	return sorted_list

steps = [4, 2, 8]
sorted_steps = sort_lists(steps)
print(sorted_steps)
```

> Instead of the `sort_list()` function returning us the correctly sorted list, i.e. `[2, 4, 8]`, it returned us `[2, 2, 2]`. What went wrong? It'd be wonderful if you could recognize the logical mistake our code makes.

## The Sorting Algorithm Sorted Out

If we look at the cards illustration again, it's clear that once we find the minimum, not only do we append that minimum to the other hand, but we also remove it from the original list. If we don't remove it from the original list, we'll always keep finding the same minimum number even if we run the loop a million times. Notice how we add this missing but on **line 6**. The code returns us a sorted list this time.

```python
def sort_list(unsorted_list):
  sorted_list = []
  for i in range(len(unsorted_list)):
    min_value = min(unsorted_list)
    sorted_list.append(min_value)
    unsorted_list.remove(min_value)
  return sorted_list

steps = [4, 2, 8]
sorted_steps = sort_list(steps)
print(sorted_steps)
```

# Problem Solving - Integration

Learn how to integrate the coding constructs we learned with the project requirements.

> [!NOTE]
> In this chapter, so far, we’ve learned how to:
> 
> 1. Use NumPy to load data from an external file into our Python code.
>     
> 2. Store data in Python’s dictionary data structure.
>     
> 3. Use Matplotlib to plot the data visually.
>     
> 4. Sort a list.

But we've learned all these important concepts in isolation. A critical problem-solving skill in programmer's toolkits is the ability to integrate seemingly isolated concepts to build a solution to the task at hand. In this lesson, the task at hand is only one requirement of our client - bar plot users sorted from least active to most active. This lesson will help us fulfill this one requirement and let us exercise the concept of integration while we apply all of what we've learned in this chapter. It's equally important to note that we'll be using the following coding structure to help us build the code incrementally while we make smaller helper function at each stage as we go from reading the hourly data up to plotting the sorted information.

![](https://i.imgur.com/ItWrG6r.png)

Our code structure makes it easy to understand, maintain, and build on. As shown in the illustration above, it follows a common convention of importing libraries at the start, defining helper functions, and then having a main controller function that contains the main logic of the program by calling those helper functions and passing and receiving data from them.

> [!NOTE]
> The lesson uses the same code we’ve already seen in the previous lessons. It just structures it more neatly. Read the highlighted sections in the code very carefully, run the code in your head before clicking the “Run” button, and then see how the output and AI Mentor’s code explanation match with how it ran in your head.

## Reading the Data (Hourly) in a Dictionary

Our integration journey with reading the hourly data that our client has provided and loading it up into a dictionary.

```python
import numpy

def read_data_in_dict(file_name):
    data = numpy.loadtxt(file_name, delimiter = ",", dtype = str)
    data_dict = {}
    for i in range(1, len(data)): # Write 1 instead of 0 to skip the header row
        row = data[i]
        name = row[0]
        steps = numpy.array(row[1:], dtype = int)
        data_dict[name] = steps
    return data_dict

def main():
    file_name = "steps.csv" 
    hourly_data = read_data_in_dict(file_name)
    print(hourly_data)
```

This code is structured in a way that:

1. First imports the necessary library.
2. Then, defines the helper functions
3. Finally, the main controller function with all of the logic.

In this code, the main goal is to load data from a CSV file into a dictionary. The `read_data_in_dict` function reads the data from the CSV file (skipping the header row) and stores it in a dictionary where the name is the key and the steps are values. 

The `main` function calls the `read_data_in_dict` function with the file name "steps.csv" and then prints the resulting dictionary.

## Converting Hourly to Daily

Eventually, we want to have one whole number per user. We currently have 168 numbers representing the steps taken per hours of the entire week. We'll get to one number, but first, let's slice 24 hours and sum them so that we have steps taken every day of the week instead of every hour. Notice the modular approach to our coding structure. This really comes in handy for *integration*. The new features keep stacking as helper functions while everything else remains as it was.

```python
import numpy

def read_data_in_dict(file_name):
    data = numpy.loadtxt(file_name, delimiter = ",", dtype = str)
    data_dict = {}
    for i in range(1, len(data)):
        row = data[i]
        name = row[0]
        steps = numpy.array(row[1:], dtype = int)
        data_dict[name] = steps
    return data_dict

def hourly_to_daily_list(hourly_list): # Use the helper function for hourly_to_daily
    daily_steps = []
    for i in range(0, len(hourly_list), 24):
        day_steps = hourly_list[i:i+24]
        daily_step_count = sum(day_steps)
        daily_steps.append(daily_step_count)
    return daily_steps

def hourly_to_daily(hourly_dict):
    daily_dict = {}
    for user_name in hourly_dict:
        daily_dict[user_name] = hourly_to_daily_list(hourly_dict[user_name])
    return daily_dict
    
def main():
    file_name = "steps.csv" 
    hourly_data = read_data_in_dict(file_name)
    daily_data = hourly_to_daily(hourly_data)
    print(daily_data)

main()
```

## Computing a Dictionary - One Weekly Entry Per User

Finally, we have one number per user. Here's the code:

```python
import numpy

def read_data_in_dict(file_name):
    data = numpy.loadtxt(file_name, delimiter = ",", dtype = str)
    data_dict = {}
    for i in range(1, len(data)):
        row = data[i]
        name = row[0]
        steps = numpy.array(row[1:], dtype = int)
        data_dict[name] = steps
    return data_dict

def hourly_to_daily_list(hourly_list): # Use the helper function for hourly_to_daily
    daily_steps = []
    for i in range(0, len(hourly_list), 24):
        day_steps = hourly_list[i:i+24]
        daily_step_count = sum(day_steps)
        daily_steps.append(daily_step_count)
    return daily_steps

def hourly_to_daily(hourly_dict):
    daily_dict = {}
    for user_name in hourly_dict:
        daily_dict[user_name] = hourly_to_daily_list(hourly_dict[user_name])
    return daily_dict
    
def reduce_daily_to_weekly_dict(daily_data):
    new_dict = {}
    for key in daily_data:
        new_dict[key] = sum(daily_data[key])
    return new_dict

def main():
    file_name = "steps.csv" 
    hourly_data = read_data_in_dict(file_name)
    daily_data = hourly_to_daily(hourly_data)
    weekly_data = reduce_daily_to_weekly_dict(daily_data)
    print(weekly_data)

main()
```

This code is structured in a beginner-friendly way to process daily step data for each user and reduce it to one number per user for a whole week.

1. The code starts by importing the necessary library `numpy`.
2. It defines a function `read_data_in_dict` to read step data from a file into a dictionary.
3. It then defines a helper function `hourly_to_daily_list` to convert hourly step data to daily step data.
4. Another function `hourly_to_daily` is defined to convert hourly step data for all users to daily step data. 
5. The function `reduce_daily_to_weekly_dict` is defined to sum up daily step data for each user to get a weekly total. 
6. Finally, the `main` function is defined to orchestrate the entire process: reading data, converting it to daily, reducing to weekly, and printing the weekly data for each user.
7. The `main` function is called at the end to execute the entire process.

This code structure helps in organizing the code logically and makes it easier to understand the flow of data processing from start to finish.

## Computing Two Lists - One for Users, One for Steps

Because it's hard to imagine sorting a dictionary, we want to compile two lists: one will have the names of the users, and the other will have their corresponding steps taken.

```python
import numpy

def read_data_in_dict(file_name):
    data = numpy.loadtxt(file_name, delimiter = ",", dtype = str)
    data_dict = {}
    for i in range(1, len(data)):
        row = data[i]
        name = row[0]
        steps = numpy.array(row[1:], dtype = int)
        data_dict[name] = steps
    return data_dict

def hourly_to_daily_list(hourly_list): # Use the helper function for hourly_to_daily
    daily_steps = []
    for i in range(0, len(hourly_list), 24):
        day_steps = hourly_list[i:i+24]
        daily_step_count = sum(day_steps)
        daily_steps.append(daily_step_count)
    return daily_steps

def hourly_to_daily(hourly_dict):
    daily_dict = {}
    for user_name in hourly_dict:
        daily_dict[user_name] = hourly_to_daily_list(hourly_dict[user_name])
    return daily_dict
    
def reduce_daily_to_weekly_dict(daily_data):
    new_dict = {}
    for key in daily_data:
        new_dict[key] = sum(daily_data[key])
    return new_dict

def compile_user_steps_lists(weekly_data):
    user_names_list = []
    user_steps_list = []
    for key in weekly_data:
        user_names_list.append(key)
        user_steps_list.append(weekly_data[key])
    return user_names_list, user_steps_list

def main():
    file_name = "steps.csv" 
    hourly_data = read_data_in_dict(file_name)
    daily_data = hourly_to_daily(hourly_data)
    weekly_data = reduce_daily_to_weekly_dict(daily_data)
    user_names, user_steps = compile_user_steps_lists(weekly_data)
    print(user_names, user_steps)

main()
```

This code is structured in a beginner-friendly way to process step data for users in a week. It starts by:

1. Importing the necessary library
2. Defines helper functions to read data
3. Converts hourly steps to daily steps
4. Reducing it to weekly steps
5. Compiling user lists
6. Finally printing the user names and steps taken in the week.

This code is well organized and easy to follow for beginners learning about data processing and function structuring in Python. 

## Sorting the Lists According to Steps

Now, we're ready to integrate our sorting algorithm/function within our code. We then print the output of the `sorted_user_steps` list to test whether our function correctly performs the sorting task.

```python
import numpy

def read_data_in_dict(file_name):
    data = numpy.loadtxt(file_name, delimiter = ",", dtype = str)
    data_dict = {}
    for i in range(1, len(data)):
        row = data[i]
        name = row[0]
        steps = numpy.array(row[1:], dtype = int)
        data_dict[name] = steps
    return data_dict

def hourly_to_daily_list(hourly_list): # Use the helper function for hourly_to_daily
    daily_steps = []
    for i in range(0, len(hourly_list), 24):
        day_steps = hourly_list[i:i+24]
        daily_step_count = sum(day_steps)
        daily_steps.append(daily_step_count)
    return daily_steps

def hourly_to_daily(hourly_dict):
    daily_dict = {}
    for user_name in hourly_dict:
        daily_dict[user_name] = hourly_to_daily_list(hourly_dict[user_name])
    return daily_dict
    
def reduce_daily_to_weekly_dict(daily_data):
    new_dict = {}
    for key in daily_data:
        new_dict[key] = sum(daily_data[key])
    return new_dict

def compile_user_steps_lists(weekly_data):
    user_names_list = []
    user_steps_list = []
    for key in weekly_data:
        user_names_list.append(key)
        user_steps_list.append(weekly_data[key])
    return user_names_list, user_steps_list

def return_min_index(input_list): # helper function for mySort 
    current_min = input_list[0]
    min_index = 0
    for i in range(len(input_list)):
        if input_list[i] < current_min:
            current_min = input_list[i]
            min_index = i
    return min_index

def my_sort(user_names, user_steps):
    sorted_user_names = []
    sorted_user_steps = []
    for i in range(len(user_steps)):
        min_index = return_min_index(user_steps)
        sorted_user_names.append(user_names[min_index])
        sorted_user_steps.append(user_steps[min_index])
        user_steps[min_index] = float("inf")
    return sorted_user_names, sorted_user_steps

def main():
    file_name = "steps.csv" 
    hourly_data = read_data_in_dict(file_name)
    daily_data = hourly_to_daily(hourly_data)
    weekly_data = reduce_daily_to_weekly_dict(daily_data)
    user_names, user_steps = compile_user_steps_lists(weekly_data)
    sorted_user_names, sorted_user_steps = my_sort(user_names, user_steps)
    print(sorted_user_steps, sorted_user_names)

main()
```

This code is structured to first import the necessary library, define helper functions, and then the main controller function that sorts users and their steps. The main emphasis of this code is on sorting the users and their steps, which will be useful for plotting purposes. The code reads the data from a file, converts hourly steps to daily steps, reduces daily steps to weekly steps, compiles user steps lists, sorts the users based on their steps, and finally prints the sorted users steps and names.

## Printing Sorted Info (name, steps, and rank)

This step is self-explanatory, we just add a `print_sorted_info()` named helper function that gets our job done.

```python
import numpy

def read_data_in_dict(file_name):
    data = numpy.loadtxt(file_name, delimiter = ",", dtype = str)
    data_dict = {}
    for i in range(1, len(data)):
        row = data[i]
        name = row[0]
        steps = numpy.array(row[1:], dtype = int)
        data_dict[name] = steps
    return data_dict

def hourly_to_daily_list(hourly_list): # Use the helper function for hourly_to_daily
    daily_steps = []
    for i in range(0, len(hourly_list), 24):
        day_steps = hourly_list[i:i+24]
        daily_step_count = sum(day_steps)
        daily_steps.append(daily_step_count)
    return daily_steps

def hourly_to_daily(hourly_dict):
    daily_dict = {}
    for user_name in hourly_dict:
        daily_dict[user_name] = hourly_to_daily_list(hourly_dict[user_name])
    return daily_dict
    
def reduce_daily_to_weekly_dict(daily_data):
    new_dict = {}
    for key in daily_data:
        new_dict[key] = sum(daily_data[key])
    return new_dict

def compile_user_steps_lists(weekly_data):
    user_names_list = []
    user_steps_list = []
    for key in weekly_data:
        user_names_list.append(key)
        user_steps_list.append(weekly_data[key])
    return user_names_list, user_steps_list

def return_min_index(input_list): # helper function for mySort 
    current_min = input_list[0]
    min_index = 0
    for i in range(len(input_list)):
        if input_list[i] < current_min:
            current_min = input_list[i]
            min_index = i
    return min_index

def my_sort(user_names, user_steps):
    sorted_user_names = []
    sorted_user_steps = []
    for i in range(len(user_steps)):
        min_index = return_min_index(user_steps)
        sorted_user_names.append(user_names[min_index])
        sorted_user_steps.append(user_steps[min_index])
        user_steps[min_index] = float("inf")
    return sorted_user_names, sorted_user_steps

def print_sorted_info(user_names, user_steps):
    for i in range(len(user_steps)):
        print(user_names[i], "has taken", user_steps[i], "steps in the week, and stands at rank:", i)

def main():
    file_name = "steps.csv" 
    hourly_data = read_data_in_dict(file_name)
    daily_data = hourly_to_daily(hourly_data)
    weekly_data = reduce_daily_to_weekly_dict(daily_data)
    user_names, user_steps = compile_user_steps_lists(weekly_data)
    sorted_user_names, sorted_user_steps = my_sort(user_names, user_steps)
    print_sorted_info(sorted_user_names, sorted_user_steps)

main()
```

## Plotting Sorted Info (name, steps, rank)

This step culminates our integration process. We import the `pyplot` module from the `matplotlib` library. We create a `plot_sorted_info` named helper function that takes in two parameters, `user_names` and `user_steps`. We want `user_names` to be the x-axis and `user_steps` to the heights of the bars that get plotted.

```python
import numpy
from matplotlib import pyplot

def read_data_in_dict(file_name):
    data = numpy.loadtxt(file_name, delimiter = ",", dtype = str)
    data_dict = {}
    for i in range(1, len(data)):
        row = data[i]
        name = row[0]
        steps = numpy.array(row[1:], dtype = int)
        data_dict[name] = steps
    return data_dict

def hourly_to_daily_list(hourly_list): # Use the helper function for hourly_to_daily
    daily_steps = []
    for i in range(0, len(hourly_list), 24):
        day_steps = hourly_list[i:i+24]
        daily_step_count = sum(day_steps)
        daily_steps.append(daily_step_count)
    return daily_steps

def hourly_to_daily(hourly_dict):
    daily_dict = {}
    for user_name in hourly_dict:
        daily_dict[user_name] = hourly_to_daily_list(hourly_dict[user_name])
    return daily_dict
    
def reduce_daily_to_weekly_dict(daily_data):
    new_dict = {}
    for key in daily_data:
        new_dict[key] = sum(daily_data[key])
    return new_dict

def compile_user_steps_lists(weekly_data):
    user_names_list = []
    user_steps_list = []
    for key in weekly_data:
        user_names_list.append(key)
        user_steps_list.append(weekly_data[key])
    return user_names_list, user_steps_list

def return_min_index(input_list): # helper function for mySort 
    current_min = input_list[0]
    min_index = 0
    for i in range(len(input_list)):
        if input_list[i] < current_min:
            current_min = input_list[i]
            min_index = i
    return min_index

def my_sort(user_names, user_steps):
    sorted_user_names = []
    sorted_user_steps = []
    for i in range(len(user_steps)):
        min_index = return_min_index(user_steps)
        sorted_user_names.append(user_names[min_index])
        sorted_user_steps.append(user_steps[min_index])
        user_steps[min_index] = float("inf")
    return sorted_user_names, sorted_user_steps

def print_sorted_info(user_names, user_steps):
    for i in range(len(user_steps)):
        print(user_names[i], "has taken", user_steps[i], "in the week, and stands at rank:", i)

def plot_sorted_info(user_names, user_steps):
    pyplot.bar(user_names, user_steps)

def main():
    file_name = "steps.csv" 
    hourly_data = read_data_in_dict(file_name)
    daily_data = hourly_to_daily(hourly_data)
    weekly_data = reduce_daily_to_weekly_dict(daily_data)
    user_names, user_steps = compile_user_steps_lists(weekly_data)
    sorted_user_names, sorted_user_steps = my_sort(user_names, user_steps)
    print_sorted_info(sorted_user_names, sorted_user_steps)
    plot_sorted_info(sorted_user_names, sorted_user_steps)

main()
```

> [!TIP] **The Mindset of a Coder**
> Congratulations on coming this far. This lesson has invited us to exercise one of the critical ways in which coders of the world think when they integrate different concepts they know in order to solve a bigger problem.


