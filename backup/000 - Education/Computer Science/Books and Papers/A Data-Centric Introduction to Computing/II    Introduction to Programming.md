#programming #computerscience 
# 3.1.1 Motivating Example: Flags

Imagine you are starting a graphic design company, and you want to be able to create images of flags of different sizes and configurations for your customers. 

![](https://i.imgur.com/oNRpEVu.png)

Before we try to write code to create these different images, you should step back, look at this collection of images, and try to identify features of the images that might help us decide what to do. 

To help with this, we're going to answer a pair of specific questions to help us make sense of the images:

- *What do you notice about the flags*?
	Different color schemes
	Similar rectangular shape
	Logos/emblems are in different locations
	Use of stripes
	Different shapes used on the designs

- *What do you wonder about the flags or a program that might produce them?*
	How does the program allow the user to select colors?
	Can the program allow the user to manipulate the design before outputting a completed design?
	Where will the program retrieve color data?
	Where will the program retrieve image data, and shapes?

Some things you might have noticed:

- Some flags have a similar structure, just with different colors
- Some flags come in different sizes
- Some flags have poles
- Most of these look pretty simple, but some real flags have complicated features

Some thing you might have wondered?

- Do I need to be able to draw these images by hand?
- Will we be able to generate different sized flags from the same code?
- What if we have a non-rectangular flag?

The features that we noticed suggest some things we'll need to be able to do to write programs to generate flags:

- We might want to compute the heights of the stripes from the overall dimensions (we'll write programs using *numbers*).
- We need a way to describe colors to our program (we'll learn *strings*)
- We need a way to create images based on simple shapes of different colors (we'll create and combine *expressions*)
# 3.12 Numbers

Start simple: compute the sum of three and five. 

To do this computation with a computer, we need to write down the computation and ask the computer to *run* or *evaluate* the computation so that we get a number back. A software or web-application in which you write and run programs is called a *programming environment*. 

```
3 + 5
```
```
8
```

Not surprisingly, we can do other arithmetic computations

```
2 * 6
```
```
12
```

What if we try $3 + 4 * 5$?

Pyret gave us an error message. What it says is that Pyret isn't sure whether we mean 

```
(3 + 4) * 5 or 3 + (4 * 5)
```

So, it asks us to include parenthesis that make that explicit. Every programming language has a set of rules about how you have to write down programs. These rules are there to avoid *ambiguity*.

```
(3 + 4) * 5
35

3 + (4 * 5)
23
```

Another Pyret rule requires spaces around the arithmetic operators. See what happens when you forget the spaces. 

```
3+4
results in an error
```

What if we wanted to get beyond basic arithmetic operators? Let's say we want the minimum of two numbers. We'd write this as:

```
num-min(2, 8)
```
# 3.1.3 Expressions

Note that when we run `num-min`, we get a number in return (as we did for `+`, `*`, ...). This means we should be able to use the result of `num-min` in other computations where a number is expected:

```
5 * num-min(2, 8)
10
```

```
(1 + 5) * num-min(2, 8)

12
```

Hopefully you are starting to see a pattern. We can build up more complicated computations from smaller ones, using operations to combine the results from the smaller computations. We will use the term *expression* to refer to a computation written in a format that Pyret can understand and evaluate to an answer. 

> [!Exercise]
>  In CPO, try to write the expressions for each of the following computations:
>  - subtract 3 from 7, then multiply the result by 4 
>  - subtract 3 from the multiplication of 7 and 4 
>  - the sum of 3 and 5, divided by 2
>  - the max of 10 subtracted from 5 and -20
>  - 2 divided by the sum of 3 and 5
# 3.1.4 Terminology

Look at an interaction like 

```
>>> (3 + 4) * (5 + 1)
>>> 42
```

There are actually several kinds of information in this interaction, and we should give them names:

- **Expression**: *a computation written in the formal notation of a programming language*.
	- Examples include `4,5 + 1` and `(3 + 4) * (5 + 1)
- **Value**: *an expression that can;'t be computed further (it is it's own result)*
	- So far, the only values we've seen are numbers.
- **Program**: *a sequence of expressions that you want to run*
# 3.1.5 Strings

What if we wanted to write a program that used information other than numbers, such as someone's name? For names and other text-like data, we use what are called *strings*. Here are some examples:

```
"Kathi"
"Go Packers!"
"CSCI0111"
"Carberry, Josiah"
```

What do we notice? Strings can contain spaces, punctuation, and numbers. We use them to capture textual data. For our flags example, we'll use strings to name colors: `"red"`, `"blue"`, etc.

Note that strings are *case-sensitive*, meaning that capitalization matters (we'll see where it matters shortly).
# 3.1.6 Images

We have seen two kinds of data: numbers and strings. For flags, we'll also need images. Images are different from both numbers and strings (you can't describe an entire image with a single number, well, not unless you get much farther into computer science but let's not get ahead of ourselves).

Pyret has built-in support for images. When you start up Pyret, you'll see a grayed out line that says "use context essentials 2021" (or something similar). This line configures Pyret with some basic functionality beyond basic numbers and strings.

> [!Exercise]
> Press the “Run” button (to activate the features in essentials), then write each of these Pyret expressions at the interactions prompt to see what they produce:
> 
> - `circle(30, "solid", "red")`
>     
> - `circle(30, "outline", "blue")`
>     
> - `rectangle(20, 10, "solid", "purple")`

Each of these expressions names the shape to draw, then configures the shape in the parenthesis that follow. The configuration information consists of the shape dimensions (the radius for circles, the width and height for rectangles, both measured in screen pixels), a string indicating whether to make a solid shape or just an outline, then a string with the color to use in drawing the shape.

*Which shapes and colors does Pyret know?* Hold this question for just a moment. We'll show you how to lookup information like this in the documentation shortly. 
# 3.1.6.1 Combining Images

Earlier, we saw that we could use operators like `+` and `*` to combine numbers through expressions. Any time you get a new kind of datum in programming, you should ask what operations the language gives you for working with that data. In the case of images in Pyret, the collection includes the ability to:

- rotate them
- scale them
- flip them
- put two of them side by side
- place one on top of the other
- and more...

Let's see how to use some of these.

> [!Excercise]
> > Type the following expressions into Pyret:
> > 
> > ```
> > rotate(45, rectangle(20, 30, "solid", "red"))
> > ```
> > 
> > What does the `45` represent? Try some different numbers in place of the `45` to confirm or refine your hypothesis.
> > 
> > ```
> > overlay(circle(25, "solid", "yellow"),
> >   rectangle(50, 50, "solid", "blue"))
> > ```
> > 
> > Can you describe in prose what `overlay` does?
> > 
> > ```
> > above(circle(25, "solid", "red"),
> >   rectangle(30, 50, "solid", "blue"))
> > ```
> > 
> > What kind of value do you get from using the `rotate` or `above` operations? (hint: your answer should be one of number, string, or image)
> 

These examples let us think a bit deeper about expressions. We have simple values like numbers and strings. We have *operations* or *functions* that combine values, like + or `rotate` ("functions" is the term more commonly used in computing, whereas your math classes likely used "operations"). Every function produces a value, which can be used as input to another function. We build up expressions by using values and the outputs of functions as inputs to other functions.

For example, we used `above` to create an image out of two smaller images. We could take that image and rotate it using the following expression.

```
rotate(45,
  above(circle(25, "solid", "red"),
    rectangle(30, 50, "solid", "blue")))
```

This idea of using the output of one function as input to another is known as *composition*. Most interesting programs arise from composing results from one computation with another. Getting comfortable with composing expressions is an **essential first step in learning to program**.

> [!Exercise]
> Try to create the following images:
> 
> - a blue triangle (you pick the size). As with `circle`, there is a `triangle` function that takes a side length, fill style, and color and produces an image of an equilateral triangle.
>     
> - a blue triangle inside a yellow rectangle
>     
> - a triangle oriented at an angle
>     
> - a bullseye with 3 nested circles aligned in their centers (e.g., the [Target](https://www.target.com/) logo)
>     
> - whatever you want—play around and have fun!
>     
> 
> The bullseye might be a bit challenging. The `overlay` function only takes two images, so you’ll need to think about how to use composition to layer three circles.
# 3.1.6.2 Making a Flag


We're ready to make our first flag! Let's start with the flag of Armenia, which has three horizontal stripes: red on top, blue in the middle, and orange on the bottom.

> [!Exercise]
> Use the functions we have learned so far to create an image of the Armenian flag. You pick the dimensions (we recommend a width between 100 and 300).
> 
> Make a list of the questions and ideas that occur to you along the way.

