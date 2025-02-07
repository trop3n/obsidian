---
up: "[[SQL]]"
tags:
  - "#education/computerprogramming/languages/sql/learnsql"
---

# Manipulation

### Statements

`SELECT * FROM celebs;`

- Which parts of the statement are *clauses?* `FROM`, `SELECT`
- What table are we applying the command to? `celebs`

### Create

```SQL
CREATE TABLE celebs (   
   id INTEGER,    
   name TEXT,    
   age INTEGER
); 
```

> Create a new tables called `celebs`.

### Insert

```SQL
INSERT INTO celebs (id, name, age) 
VALUES (1, 'Justin Bieber', 29); 
```
```SQL
INSERT INTO celebs (id, name, age) 
VALUES (2, 'Beyonce Knowles', 42); 

INSERT INTO celebs (id, name, age) 
VALUES (3, 'Jeremy Lin', 35); 

INSERT INTO celebs (id, name, age) 
VALUES (4, 'Taylor Swift', 33); 
```

### Select

> To retrieve all of the names in the `celebs` table. In the code editor:

```SQL
SELECT name FROM celebs;
```

> To `SELECT` _all_ the data in the `celebs` table, enter the following statement in the code editor using the `*` wildcard character:

```SQL
SELECT * FROM celebs;
```

### Alter

```SQL
ALTER TABLE celebs
ADD COLUMN twitter_handle TEXT;

SELECT * FROM celebs;
```

> This statement adds a column to the database, waiting for information on each celebrities twitter handle.

### Update

Update the table to include Taylor Swift’s [twitter handle](https://twitter.com/taylorswift13). In the code editor, type:

```SQL
UPDATE celebs 
SET twitter_handle = '@taylorswift13' 
WHERE id = 4;

SELECT * FROM celebs;
```

### Delete 

> Delete all of the rows that have a `NULL` value in the twitter handle column. In the code editor, type the following:

```SQL
DELETE FROM celebs
WHERE twitter_handle IS NULL;

SELECT * FROM celebs;
```

### Constraints

> Create a new table with constraints on the values. In the code editor type:

```SQL
CREATE TABLE awards (   
   id INTEGER PRIMARY KEY,   recipient 
   TEXT NOT NULL,   award_name 
   TEXT DEFAULT 'Grammy'
);
```

# Queries

### Introduction

> In this lesson, we will be learning different SQL commands to query a single table in a database.

One of the core purposes of the SQL language is to retrieve information stored in a database. This is commonly referred to as **querying**. Queries allow us to communicate with the database by asking questions and returning a result set with data relevant to the question. 
### Select

> `SELECT` is used every time you want to query data from a database and `*` means *all* columns.

Suppose we are only interested in two of the columns. We can select individual columns. We can select individual columns by their names (separated by a comma):

```SQL
SELECT column1, column2
FROM table_name;
```

> Line breaks don't mean anything specific in SQL. We could write this entire query on one line, and it would run the same.
### As

> Knowing how `SELECT` works, suppose we have the code below:

```SQL
SELECT name AS 'Titles'
FROM movies;
```

`AS` is a keyword in SQL that allows you to *rename* a column or table using an alias. The new name can be anything you want as long as you put it inside of single quotes. Here we renamed the `name` column as `Titles`.

> Some important things to note are: 

- Although it's not always necessary, it is considered best practice to surround your aliases with single quotes.
	- Note that this practice is specific to SQLite, the RDBMS used in this exercise.
	- When you work with other RDBMSs, notably PostgreSQL, *no quotes or double quotes may be required in place of single quotes.* 

- When using `AS`, the columns are not being renamed in the table. The aliases only appear in the result. 
### Distinct

> When we are examining data in a table, it can be helpful to know what *distinct* values exist in a particular column.

`DISTINCT` is used to return unique values in the output. It filters out all duplicate values in the specified columns(s).

For instance,

```SQL
SELECT tools
FROM inventory;
```

Might produce:

|tools|
|---|
|Hammer|
|Nails|
|Nails|
|Nails|
> By adding `DISTINCT` to the column name, 

```SQL
SELECT DISTINCT tools
FROM inventory;
```

The result would be:

|tools|
|---|
|Hammer|
|Nails|
Filtering the results of a query is an important skill in SQL. It is easier to see the different possible `genre`s in the `movie` table after the data has been filtered than to scan every row in the table. 
### Where

> We can restrict our query results using the `WHERE` clause in order to obtain only the information we want. 

Following this format, the statement below filters the result set to only include top rated movies (IMDb ratings greater than 8):

```SQL
SELECT *
FROM movies
WHERE imdb_rating > 8;
```

How does it work?

1. The `WHERE` clause filters the result set to only include rows where the following *condition* is true.
2. `imdb_rating > 8` is the condition. Here, only rows with a value greater than 8 in the `imdb_rating` column will be returned.

The `>` is an *operator*. Operators create a condition that can be evaluated as either *true* or *false*.

Comparison operators used with the `WHERE` clause are:

- `=` equal to
- `!=` not equal to
- `>` greater than
- `<` less than
- `>=` greater than or equal to
- `<=` less than or equal to

### Like I

`LIKE` can be a useful operator when you want to compare similar values.

The `movies` table contains two films with similar titles, 'Se7en' and 'Seven'.

How could we select all movies that start with 'Se' and end with 'en' and have exactly one character in the middle?

```SQL
SELECT *
FROM movies
WHERE name LIKE 'Se_en';
```

- `LIKE` is a special operator used with the `WHERE` clause to search for a specific pattern in a column.
- `name LIKE 'Se_en'` is a condition evaluating the `name` column for a specific pattern.
- `Se_en` represents a pattern with a *wildcard* character.

The `_` means you can substitute any individual character here without breaking the pattern. The names `Seven` and `Se7en` both match this pattern.

### Like II

> The percentage sign is another *wildcard character* that can be used with `LIKE`. 

This statement below filters the result set to only include movies with names that begin with the letter 'A':

```SQL
SELECT *
FROM movies
WHERE name LIKE 'A%'
```

> `%` is a wildcard character that matches zero or more missing characters in the pattern. 

For example:

- `A%` matches all movies with names that begin with letter 'A'
- `%a` matches all movies that end with 'a'

We can also use `%` both before and after a pattern.

```SQL
SELECT *
FROM movies
WHERE name LIKE '%man%';
```

> Here, any movie that *contains* the word 'man' in its name will be returned as a result.

`LIKE` is not case-sensitive. "Batman" and "Man of Steel" will both appear in the results of the query above. 

### Is Null

> By this point of the lesson, you might have noticed that there a few missing values in the `movies` table. 

More often than not, the data you encounter will have missing values.

Unknown values are indicated by `NULL`.

- It is not possible to test for `NULL` values with comparison operators, like `=` and `!=`.

Instead, we use these operators:

`IS NULL`
`IS NOT NULL`

To filter for all movies *with* and IMDb rating:

```SQL
SELECT name
FROM movies
WHERE imdb_rating IS NOT NULL;
```

### Between

The `BETWEEN` operator is used in a `WHERE` clause to filter the result set within a certain *range*. 

It accepts to values that are either *numbers, text or dates.* 

Filter the result set to only include movies with `years` from 1990 up to, and *including* 1999;

```SQL
SELECT *
FROM movies
WHERE year BETWEEN 1990 AND 1999;
```

> When the values are text, `BETWEEN` filters the result set for within the alphabetical range.
> 
> In this statement, `BETWEEN` filters the result set to only include movies with `name`s that begin with the letter A up to, *but not including* ones that begin with J.

```SQL
SELECT *
FROM movies
WHERE name BETWEEN 'A' AND 'J';
```

> However, if a movie has a name of simply ‘J’, it would actually match. This is because `BETWEEN` goes _up to_ the second value — up to ‘J’. So the movie named ‘J’ would be included in the result set but not ‘Jaws’.
### And

> Sometimes we want to *combine multiple conditions* in `WHERE` clause to make the result set more specific and useful. 

One way of doing this is to use the `AND` operator. Here, we use the `AND` operator to only return 90's romance movies.

```SQL
SELECT * 
FROM movies
WHERE year BETWEEN 1990 AND 1999   
   AND genre = 'romance';
```

- `year BETWEEN 1990 and 1999` is the 1st condition.
- `genre = 'romance` is the second condition
- `AND` combines the two conditions

> With `AND`, both conditions must be true for the row to be included in the result. 
### OR

> Similar to `AND`, the `OR` operator can also be used to combine multiple conditions in `WHERE`, but there is a fundamental difference:

- `AND` operator displays a row if *all* the conditions are true
- `OR` operator displays a row if *any* condition is true

Suppose we want to check out a new movie or something action packed:

```SQL
SELECT *
FROM movies
WHERE year > 2014
  OR genre = 'action';
```

- `year > 2014` is the first condition
- `genre = 'action'` is the second condition
- `OR` combines the two conditions
### ORDER BY

> That's it with `WHERE` and it's operators, moving on!

It is often useful to list the data in our result set in a particular order.

We can *sort* the results using `ORDER BY`, either alphabetically or numerically. Sorting the results often makes the data more useful and easier to analyze.

For example, if we want to sort everything by the movie's title from A through Z:

```SQL
SELECT *
FROM movies
ORDER BY name;
```

- `ORDER BY` is a *clause* that indicates you want to sort the result by a particular column.
- `name` is a specified column.

Sometimes we want to sort things in a decreasing order. For example, if we want to select all of the well-received movies, sorted from highest to lowest by their year:

```SQL
SELECT *
FROM movies
WHERE imbd_rating > 8
ORDER BY year DESC;
```

- `DESC` is a keyword used in `ORDER BY` to sort the results in *descending order* (high to low, Z-A)
- `ASC` is a keyword used to `ORDER BY` to sort the results in *ascending order* (low to high, A-Z)

> The column that we `ORDER BY` doesn’t even have to be one of the columns that we’re displaying.
### Limit

> We've been working with fairly small table (fewer than 250 rows), but most SQL tables contain hundreds of thousands of records. In those situations, it becomes important to cap the number of rows in the result.

For instance, imagine that we just want to see a few examples of records

```SQL
SELECT *
FROM movies
LIMIT 10;
```

`LIMIT` is the clause that lets you specify the maximum number of rows the result will have. This saves space on our screen and makes our queries run faster. 

Here, we specify that the result can't have more than 10 rows. 

`LIMIT` always goes at the very end of the query. *Also, it is not supported in all SQL databases.*
### Case

> A `CASE` statement allows us to create different outputs (usually in the `SELECT` statement). It is SQL's way of handling if-then logic. 

Suppose we want to condense the ratings in `movies` to three levels:

- *If the rating is above 8, then it is Fantastic*
- *If the rating is above 6, then it is Poorly Received*
- *Else, Avoid at All Costs*

```SQL
SELECT name, 
 CASE  
  WHEN imdb_rating > 8 THEN 'Fantastic'  
  WHEN imdb_rating > 6 THEN 'Poorly Received'  
  ELSE 'Avoid at All Costs' 
 END
FROM movies;
```

- Each `WHEN` tests a condition and the following `THEN` gives us the string if the condition is true.
- The `ELSE` gives us the string if *all* the above conditions are false.
- The `CASE` statement must end with `END`.

> In the result, you have to scroll right because the column name is very long. To shorten it, we can rename the column to 'Review' using `AS`:

```SQL
SELECT name, 
 CASE  
  WHEN imdb_rating > 8 THEN 'Fantastic'  
  WHEN imdb_rating > 6 THEN 'Poorly Received'  
  ELSE 'Avoid at All Costs' 
 END AS 'Review'
FROM movies;
```

### Review

We just learned how to query data from a database using SQL. We also learned how to filter queries to make the information more specific and useful.

Let’s summarize:

- [`SELECT`](https://www.codecademy.com/resources/docs/sql/commands/select?page_ref=catalog) is the clause we use every time we want to query information from a database.
- [`AS`](https://www.codecademy.com/resources/docs/sql/commands/as?page_ref=catalog) renames a column or table.
- [`DISTINCT`](https://www.codecademy.com/resources/docs/sql/commands/select-distinct?page_ref=catalog) return unique values.
- [`WHERE`](https://www.codecademy.com/resources/docs/sql/commands/where?page_ref=catalog) is a popular command that lets you filter the results of the query based on conditions that you specify.
- [`LIKE`](https://www.codecademy.com/resources/docs/sql/operators/like?page_ref=catalog) and [`BETWEEN`](https://www.codecademy.com/resources/docs/sql/operators/between?page_ref=catalog) are special operators.
- [`AND`](https://www.codecademy.com/resources/docs/sql/operators/and?page_ref=catalog) and [`OR`](https://www.codecademy.com/resources/docs/sql/operators/or?page_ref=catalog) combines multiple conditions.
- [`ORDER BY`](https://www.codecademy.com/resources/docs/sql/commands/order-by?page_ref=catalog) sorts the result.
- [`LIMIT`](https://www.codecademy.com/resources/docs/sql/commands/limit?page_ref=catalog) specifies the maximum number of rows that the query will return.
- [`CASE`](https://www.codecademy.com/resources/docs/sql/commands/case?page_ref=catalog) creates different outputs.
# What is SQLite?

> In this section, we will explore the extremely prevalent database engine called [SQLite](https://www.sqlite.org/index.html).

- What it does
- Main uses
- How to set it up and use it
### What is SQLite?

> SQLite is a database engine. It is software that allows users to interact with a relational database. In SQLite, a database is stored in a **single file** - a trait that distinguishes it from other database engines. 

This fact allows for a great deal of accessibility: copying a database is no more complicated than copying a file that stores the data, sharing a database can mean sending an email attachment.
#### Drawbacks to SQLite

> SQLite's signature portability unfortunately makes it a poor choice when many different users are updating the table at the same time (to maintain integrity of data, only one user can write to the file at a time.)

- It may also require some more work to ensure the security of private data due to the same features that make SQLite accessible. 
- Furthermore, SQLite does not offer the same exact functionality as many other database systems, limiting some advanced features other relational database systems offer. 
- Lastly, SQLite does not validate data types. Where many other database software would reject data that does not conform to a table's schema, SQLite allows users to store data of any type into any column.

SQLite creates *schemas*, which constrain the type of data in each column, but it does not enforce them. 

The example below shows that the id column expects to store integers, the name column expects to store text, and the age column expects to store integers:

```SQL
CREATE TABLE celebs (
	id INTEGER,
	name TEXT,
	age INTEGER
);
```

> However, SQLite will not reject values of the wrong type. We could accidentally insert the wrong data types in the columns. Storing different data types in the same column is a bad habit that can lead to errors that are difficult to fix, so it's important to be strict about your schema even though SQLite will not enforce it.

# Aggregate Functions

> SQL Queries don't just access raw data, they can also perform calculations on the raw data to answer specific data questions.

Calculations performed on multiple rows of a table are called **aggregates**.

In this lesson, we have given you a table named `fake_apps` which is made up of fake mobile applications data.

> A quick review of some important aggregates that we will cover in the next five exercises:

- `COUNT()`: count the number of rows
- `SUM()`: the sum of the values in a column
- `MAX()`/`MIN()`: the largest/smallest value
- `AVG()`: the average of the values in a column
- `ROUND()`: round the values in the column
# Count

The fastest way to calculate how many rows are in a table is to use the `COUNT()` function.

`COUNT()` is a function that takes the name of a column as an argument and counts the number of non-empty values in that column.

```SQL
SELECT COUNT(*)
FROM table_name;
```

> Here we want to count every row, so we pass `*` as an argument inside the parenthesis.
# Sum

> SQL makes it easy to add all values in a particular column using `SUM()`.

`SUM()` is a function that takes the name of a column as an argument and returns the sum of all the values in that column.

What is the total number of downloads for all of the apps combined?

```SQL
SELECT SUM(downloads)
FROM fake_apps;
```

> This adds all values in the `downloads` column.
# Max/Min

> The `MAX()` and `MIN()` functions return the highest and lowest values in a column, respectively. 

How many downloads does the most popular app have?

```SQL
SELECT MAX(downloads)
FROM fake_apps;
```

> The most popular app has 31,090 downloads. 

`MAX()` takes the name of a column as an argument and *returns the largest value in that column*.

`MIN()` works the same way but does the opposite; it *returns the smallest value.* 
# Average

> SQL uses the `AVG()` function to quickly calculate the average value of a particular column. 

The statement below returns the average number of downloads for an app in our database:

```SQL
SELECT AVG(downloads)
FROM fake_apps;
```

The `AVG()` function works by taking a column name as an argument and returns the average value for that column. 

# Round

> By default, SQL tries to be as precise as possible without rounding. We can make the result table easier to read using the `ROUND()` function. 

`ROUND()` function takes two arguments inside the parenthesis:

1. a column name
2. an integer

It rounds the values in the column to the number of decimal places specified by the integer.

```SQL
SELECT ROUND(price, 0)
FROM fake_apps;
```

> Here, we pass the column `price` and integer `0` as arguments. SQL rounds the values into the column to 0 decimal places in the output.

`AVG` can be treated like any other value, and even be placed inside the `ROUND` function like so:

```SQL
ROUND(AVG(price), 2)
```

Here, `AVG(price)` is the first argument and `2` is the second argument because we want to round it to two decimal places:

```SQL
SELECT ROUND(AVG(prices), 2)
FROM fake_apps;
```

# Group By I

> Oftentimes, we will want to calculate an aggregate for data with certain characteristics. 

For instance, we might want to know the mean IMDb ratings for all movies each year. We could calculate each number by a series of queries with different `WHERE` statements, like so:

```SQL
SELECT AVG(imdb_rating)
FROM moviesWHERE year = 1999;

SELECT AVG(imdb_rating)
FROM movies
WHERE year = 2000;

SELECT AVG(imdb_rating)
FROM movies
WHERE year = 2001;
```

And so on.

Luckily, there is a better way. 

We can use `GROUP BY` to do this in a single step:

```SQL
SELECT year,
   AVG(imdb_rating)
FROM movies
GROUP BY year
ORDER BY year;
```

`GROUP BY` is a clause in SQL that is used with [aggregate functions](https://www.codecademy.com/resources/docs/sql/aggregate-functions). It is used in *collaboration with the `SELECT` statement* to arrange identical data into *groups*. 

The `GROUP BY` statement comes after any `WHERE` statements, but before `ORDER BY` or `LIMIT`. 

1. In the code editor, type:

```SQL
SELECT price, COUNT(*)
FROM fake_apps
GROUP BY price;
```

Here, our aggregate function is `COUNT()` and we arranged price into groups.

# Group By II

> Sometimes, we want to `GROUP BY` a calculation done on a column.

For instance, we might want to know how many movies have IMDb ratings that round to 1, 2, 3, 4, 5. We could do this using the following syntax:

```SQL
SELECT ROUND(imdb_rating),
   COUNT(name)
FROM movies
GROUP BY ROUND(imdb_rating)
ORDER BY ROUND(imdb_rating);
```

However, this query may be time-consuming to write and more prone to error.

SQL lets us use the column reference(s) in our `GROUP BY` that will make our lives easier.

- `1` is the first column selected
- `2` is the second column selected
- `3` is the third column selected

...and so on.

The following query is equivalent to the one above:

```SQL
SELECT ROUND(imdb_rating),
   COUNT(name)
FROM movies
GROUP BY 1
ORDER BY 1;
```

> Here, the `1` refers to the first column in our `SELECT` statement, `ROUND(imdb_rating)`

# Having

> In addition to being able to group data using `GROUP BY`, SQL also allows you to filter which groups to include and which to exclude.

For instance, imagine that we want to see how many movies of different genres were produced each year, but we only care about years and genres with at least 10 movies.

We can't use `WHERE` here because we don't want to filter the rows, we want to *filter groups*. 

This is where `HAVING` comes in.

`HAVING` is very similar to `WHERE`. In fact, all types of `WHERE` clauses you learned about thus far can be used with `HAVING`.

We can use the following for the problem:

```SQL
SELECT year,
   genre,
   COUNT(name)
FROM movies
GROUP BY 1, 2
HAVING COUNT(name) > 10;
```

- When we want to limit the results of a query based on values of individual rows, use `WHERE`. 
- When we want to limit the results of a query based on an aggregate property, use `HAVING`.

`HAVING` statement always comes after `GROUP BY`, but before `ORDER BY` and `LIMIT`.

# Review

You just learned how to use aggregate functions to perform calculations on your data. What can we generalize so far?

- [`COUNT()`](https://www.codecademy.com/resources/docs/sql/aggregate-functions/count?page_ref=catalog): count the number of rows
- [`SUM()`](https://www.codecademy.com/resources/docs/sql/aggregate-functions/sum?page_ref=catalog): the sum of the values in a column
- [`MAX()`](https://www.codecademy.com/resources/docs/sql/aggregate-functions/max?page_ref=catalog)/[`MIN()`](https://www.codecademy.com/resources/docs/sql/aggregate-functions/min?page_ref=catalog): the largest/smallest value
- [`AVG()`](https://www.codecademy.com/resources/docs/sql/aggregate-functions/avg?page_ref=catalog): the average of the values in a column
- [`ROUND()`](https://www.codecademy.com/resources/docs/sql/commands/round?page_ref=catalog): round the values in the column

_Aggregate functions_ combine multiple rows together to form a single value of more meaningful information.

- [`GROUP BY`](https://www.codecademy.com/resources/docs/sql/commands/group-by?page_ref=catalog) is a clause used with aggregate functions to combine data from one or more columns.
- [`HAVING`](https://www.codecademy.com/resources/docs/sql/commands/having?page_ref=catalog) limit the results of a query based on an aggregate property.

# Trends in Start Ups Project

