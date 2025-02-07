---
up: "[[Anatomy of Rust]]"
tags:
  - "#education/computerprogramming/languages/rust/becomearustpro/helloworld"
---

# What does that mean?

```rust
fn main() {
    println!("Hello World!");
}
```

> There are a number of things to learn here. We'll keep going into more depth on all of this throughout the tutorial. To make it easier to talk about, we'll start with some basic terms. 

If some of this seems confusing, don't worry. We'll be working with all of this throughout the tutorial, and it will start to make sense.

`fn`
- short for "function". In Rust, a function means "tell me some information, I'll do some things, and then give you an answer."
`main`
- A special function. This is where your program starts.
`()`
- These parenthesis are the parameter list for this function. It's empty now, meaning there are no parameters. 
`{ }`
- These are called *curly brackets* or *brackets*. These enclose the body of the **main function**. The **body** lives inside of those braces. The body will say what the main function actually does.
`println!`
- This is what is called a macro. It means "print and add a new line." Macros are very similar to functions. The difference, for now, is that macros end with an exclamation point.
`(Hello, world)`
- This is the parameter list for the macro call. We're saying "call this macro, called `println`, with these parameters." This is just like how the `main` function has a parameter list. Except the `println` macro actually has a parameter. We'll learn more about this later.
`"Hello, World!"`
- This is a *string*. Strings are a bunch of letters (or characters) put together. We put them inside the double quotes (`"`) to mark them as strings. Then we can pass them around for macros like `println` and other functions later.
`;`
- This is a semicolon. It completes what's called a *statement*. Statements do something specific. In this case, it's calling the macro.

### Interpolation

> In Rust, you can interpolate other values into the output. Let's demonstrate:

```rust
fn main() {

    println!("My name is {}", "Michael");

}
```
> Output: My name is Michael

We're now passing two parameters into the `println` macro: the first string is `"My name is {}`. The `println` macro has special support for the `{}` braces. The parameters are separated by commas.

### Variables

> Often, we don't want to put all of the values we care about on one line like that. It can be more pleasant to define variables, which are convenient names that refer to the values we care about. We do that with `let`:

```rust
fn main() {

    let name = "Michael";

    println!("My name is {}", name);

}
```
>Output: My name is Michael

`Name` is pointing at the string `"Michael"`, and we can refer to that when we call `println!`. Variables are a core part of programming, and we're not going to be able to explain all of their uses here. 

```rust
fn main() {

    let apples = 10;

    println!("I have {} apples", apples);

}
```
> Ouput:
> I have 10 apples. 

> Notice how there are not double quotes around the number `10`. 
> 	You can put quotes around an integer, and this program will look the same.
> 	But, they will *mean* something different. 

If quotes are placed around a number, it becomes a string. 

> When you run your program, something called a **compiler** is checking to make sure your program makes sense. And if it doesn't, it will give you an error message. 

---

### Multiple Variables and Shadowing

> We're not limited to just one variable. It's fine to define as many as we'd like:

```Rust
fn main() {
  let x = 5;
  let y = 10;
  let name = "Michael";
  println!("My name is {}, and the answer is {}", name, x + y);
}

# Output:

My name is Michael, and the answer is 15
```

> We can also use this technique to break up larger computations into smaller pieces:

```Rust
fn main() {
    let x = 5 + 3;
    let y = 2 - 1;
    let z = x * y;
    println!("The answer is {}, z);
}

# Output:
The answer is 8
```

> You're allowed to reuse variable names. This essentially works the way you would expect. Try to guess the output of this program:

```Rust
fn main() {
    let x = 5 + 3;
    let x = x * 2;
    let x = x - 6;
    let x = x / 2;
    println!("The answer is {}", x);
}

# Output:
The answer is 5
```

# Types

> We've spoken about numbers and strings. In Rust, every value has a type that tells you what kind of thing it is. When you have a string literal (something between double quotes) like `"Hello, world!"`, its type is `&str`.

When you use `let` to declare a variable, you can give its type as well, like this:

```Rust
fn main() {
    let name: &str = "Michael";
    println!("My name is {}", name);
}

# Output:
# My name is Michael
```

> Rust has something called **type inference**, which means in many cases, you can skip putting the type, and the compiler will figure it out for you. Sometimes though, we like to write the type out. 

It can make it easier to read code and can help the compiler better catch our mistakes. But usually, with simple things, we just skip it.

### Numbers

> There's a little bit more to talk about with numbers. The first thing is integers versus floating point numbers.

- Integers are whole numbers like 5, 2, 0, etc.
	- They are numbers that *don't* have a decimal point or a fractional part.
- Floating point numbers can have decimal points. 

#### Integers

With integers, there are *signed* and *unsigned*. 

- ***Signed Integers*** can have a negative sign, and they can be positive or negative. 
- ***Unsigned Integers*** cannot have a negative sign and must be 0 or greater.

Finally, there's the size of an integer, measured in terms of bits. A bit is *either 0 or 1*, and makes up the basis of computers. If you have an 8-bit unsigned integer, you can have numbers 0-255. 

An 8-bit signed integer, on the other hand, can be the numbers -128 to 127. It's the same total count (256), but one includes negatives and the other does not. 

In Rust, the way we talk about the types of these integers is `i8`(for 8-bit signed integer), `u32` (for unsigned 32-bit integer), etc. We can use *8, 16, 32, and 64*. There's also some support for 128, but we almost never need it. 

There's also a special `isize` and `usize`, which means "whatever size the computer I'm on likes". These days, that's usually 64. 

Alright, that’s lots of funny business. Let’s get back to some actual code! For now, we’re going to pretend like all the numbers we work with are `i32`. Why’s that? It’s commonly used! Eventually, we’ll deal with converting between different types of numbers and things like that, but we’ll keep it simple for now.

# Summary

- Every Rust program starts at the `main` function.
- Inside the `main` function, you can do things like call `println`
- The `println` macro lets us do interpolation to produce outputs
- We can define variables that hold onto values using `let`
- We can perform basic arithmetic using `+ - * /`
- Each value has a type, which says what kinds of things it can hold. 
	- A `&str` is the type of a string literal, like `"Michael"`
	- There are lots of different number types, but we'll mostly use `i32`.


