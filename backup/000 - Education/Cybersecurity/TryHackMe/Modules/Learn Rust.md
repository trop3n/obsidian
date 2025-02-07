#thm #rust #programming 

---
> [[Rust]] | [[001 - Organization/Cheatsheets and Resources/Links/Programming]] | [[TryHackMe]]
---
# Introduction

Rust is a new programming language created in 2015 by a small team of people, and later adopted by Mozilla. It is a compiled low level language, which aims (and succeeds) to be the same speed as C++, but while incorporating some higher level language features from fan-favorites such as Python or JavaScript.

Rust has three goals:

- Fast
- Secure
- Productive
## Fast

Rust aims to be similar in terms of C++. Rust is statically typed, which means the data type of a variable is *known at compile time*. This allows the compiler to optimize the code further than if we didn't know the types. 

Rust does not use *garbage-collection* (despite being a low level programming language). Garbage collection is where the program attempts to reclaim memory from garbage. 

**`Garbage` is memory occupied by objects that are no longer in use by the program.**

Go, a high level programming language similar syntactically to Python but is fast & compiled, uses garbage collection. This caused a massive overhead at Discord, which forced them to switch from Go to Rust. [https://blog.discord.com/why-discord-is-switching-from-go-to-rust-a190bbca2b1f](https://blog.discord.com/why-discord-is-switching-from-go-to-rust-a190bbca2b1f)

Something to note is that Python and JavaScript use garbage collection. These abstractions may cause issues (as in Discord's case), which is why many choose a low level programming language.
## Secure

Rust is *completely memory safe*. This means that exploits involving memory aren't possible in Rust, unless you explicitly specify unsafe Rust code. 

The [Microsoft Security Response Centre](https://msrc-blog.microsoft.com/2019/07/22/why-rust-for-safe-systems-programming/) states that 70% of all CVE's MSRC assigns are memory safety issues. In Microsoft's own words:

"This means that if that software had been written in Rust, 70% of these security issues would most likely have been eliminated. And we’re not the only company to [have reported such findings](https://hacks.mozilla.org/2019/02/rewriting-a-browser-component-in-rust/)."

Sometimes programmers must perform unsafe operations. Rust provides tools to wrap these unsafe actions so unsafe code can be statically enforced by the Rust compiler.

The memory safety is guaranteed by the concept of **ownership**. All Rust code follows these rules:

- Each value has a variable, called an owner. 
- There can only be one owner at a time.
- When the owner goes out of scope, the value will be dropped. 

Values can be moved or borrowed between variables, but no value can have more than 1 owner. 

Let's see an example of Python failing with this:

```Python
squares = (val * val for val in range(100))
print(min(squares))
print(max(squares))
```

What we want is: 

```
0
9801
```

But what we get is:

```python
>>> print(min(squares))
0
>>> print(max(squares))

# value error
```

This is because `min` alters the variable squares. It's strange, because we just wanted the minimum -- not to alter the whole variable. 

In Rust, the same code is:

```rust
fn main()
  let squares = (0..100).map(|val| val * val);
  println!("{:?}", squares.min());
  println!("{:?}", squares.max());
```

```
error[E0382]: use of moved value: squares    
--> ownership.rs:4:21   
|   
3 |    println!("{:?}", squares.min());
|                     ------- value moved here   
4 |    println!("{:?}", squares.max());     
|                       ^^^^^^^ value used here after move     
|     
= note: move occurs because squares has type std::iter::Map<std::ops::Range<i32>, [closure@ownership.rs:2:31: 2:40]>, which does not implement the Copy trait
```

We'll talk more about this in a later task, but the important part is that **Python allows functions to alter variables they do not own, whereas Rust does not**.

PS: Notice how the Rust compiler explicitly points out the values, the lines, the exact characters, where the error occurred as well as a full error message explaining why it won't allow that code. Whearas Python simply said `max() arg is an empty sequence`.
## Productivity

Rust's 3rd largest goal is a strange one. Productivity! Rust provides all of the tools developers need to be productive, shipped with the platform itself. 

Some of these include:

- `Cargo`: Rust's version of `npm` or `PyPi`. Download packages others have created.
- `Clippy`: Microsoft Clippy, but re-imagined for Rust to aid with development.
- `RustFmt`: Automatically formats Rust code.
- `Cargo Test`: A built in testing application created by the Rust developers.
- `Cargo Docs`: Automatically generate documentation for your code, using documentation comments (written in Markdown). This documentation is then sent to [docs.rs](http://docs.rs) upon publishing to Cargo. Not to mention that example written in documentation are automatically tested for you. No more untested documentation examples.
- `Rust-Analyzer`: Think IDE but *more intelligent*. Rust Analyze clearly labels what is wrong with your code, why it is wrong, the exact characters that conflict and cause the error, and 90% of the time it provide an "auto-fix" function that automatically fixes these errors for you.
- `Rust Book & Docs`: Rust has a book, called The Book which details everything you could want to know about Rust. Neatly chaptered, easily searchable and at your disposal for free. If this isn't good enough, thanks to Rust's documentation comments almost every library you'll use will have extensive documentation online.

With all of these tools at your disposal, it is incredibly rate to compile a Rust program and have bugs in it. In fact, I have only ever experienced this once. 99% of the time, the tooling and language will have picked up on it long before I hit compile.
## Conclusion

If you are looking for something extremely fast and memory safe but while maintaining good productivity, Rust is the language for you. As pentesters our job is offering solutions to developers. Telling Python developers that a low-level language is a good alternative sounds wacky at first. But Rust can hold you hand, as it supports calls from functions written in other languages (foreign function interfacing). We can use Rust to rewrite security or performance critical code with our existing codebase.

Here's an example of the calling C code:

```C
extern "C" {
  fn abs(input: i32) -> i32;
}

fn main() {
    unsafe {
        println! ("C believes the absolute value of -3 is: {}", abs(-3));
    }
}
```
# Installing and Tooling

Before we dive into the language, let's install Rust. 

Rust recommends using the tool `rustup` to manage multiple versions of Rust. If you are familiar with Python, you may have used virtualenvs to achieve a similar result. That is, different versions of Python on the same machine.

This is another great tool created by the Rust team for productivity. Install `rustup` with this command:

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

This command can also be found on the Rust website [https://www.rust-lang.org/tools/install](https://www.rust-lang.org/tools/install)

This command will install the stable version of Rust for your OS.

Rust comes in 3 flavours. Stable, Beta, and Nightly.

Stable is the latest stable release of Rust (stable releases are usually shipped every 6 weeks). Beta updates periodically. Nightly updates when the language itself updates.  

Now, let's install some Rust tools to aid our development.

The command we just ran also installs `Cargo`,

Cargo is the package manager for Rust. All the packages get uploaded to [https://crates.io](https://crates.io) and does a lot of cool things.

The 3 core Cargo commands are:

**cargo install**

Install a package from [Crates.io](http://Crates.io)

**Cargo publish**

Publish a package to [crates.io](http://crates.io)

**Cargo update**

Updates all of the local packages

But, since we are developing RustCode there are 3 more important commands

**Cargo test**

Run the tests for our code

**Cargo fmt**

Runs the formatting tool. This tool automatically formats your code (apply the argument `--all` to format all code). Similar to Python's Black but built in.

**Cargo clippy**

Microsoft Clippy but for Rust! Clippy will point out common errors in your code and help you correct them.

**Community tools**

There is one tool, that is a community based tool — that is seen as absolutely essential to the Rust ecosystem.

That tool is Rust-Analyzer. Imagine an IDE but smarter and more advanced. Rust-Analyzer will analyse your code as you write it, spot errors before you compile & provide an auto-fix option to automatically fix the errors.

Rust-Analyzer states that their most supported version is VS Code, but they are available on many other platforms.

Something cool to note is that the main tools of Rust are written by the Rust developers themselves. In languages like Python, we may argue over whether `setuptools` or `poetry` is right. Or whether `pytest` is better than `unittest`. Arguing over the right tool to use is procrastination. Rust says "these are the tools you will use" and that's it. This boosts productivity, as you don't have to worry about what tools to use but can impede development as the tool may not be fully complete.
# Hello, World!

It wouldn't be a programming tutorial without a basic "Hello, World!". Create a new folder, and in the terminal type:

```
cargo init
```

This makes cargo initialize a new Rust repo. Cargo will take care of most of the work for you. 

The file structure is as follows: 

```
- Cargo.toml
- src/
	- main.rs
```

`cargo.toml` is the configuration file for our rust project. It includes our dependencies, project name, authors, the version of Rust we are using and more. 

When we have just ran `cargo init`, our file will look like this:

```
[package]   
name = "Hello_world"   
version = "0.1.0"   
authors = ["bee <bee@fake.com>"]   
edition = "2018"`
```
## `[dependencies]`

Our `main.rs` folder in the `src` is the main file where we write our code. Every single Rust project **must** have a main file, and every main file must have a main function.

```rust
fn main() {
	println!("Hello World!");
}
```

> [!NOTE]
> In the original C book, "Hello World" is stylized with a capital letter on the word world. 

In Rust, we use curly braces to denote blocks of code. And a semi-colon to express the end of an expression. 

To print in Rust, we use the macro `println!`.

We know `println` is a **macro**, as it is called with an exclamation mark. Macros, in a nutshell, allow us to write code that writes more code. To put it even simpler, we can create our own syntax that translates to different code.

To run this program, we execute: `cargo run`.

```
Compiling learn_rust v0.1.0 (/home/jason/Dev/rust/learn_rust)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.61s
     Running `/home/jason/Dev/rust/learn_rust/target/debug/learn_rust`
Hello, world!
```

This command: 

- Compiles the code with the unoptimized build (to increase the speed of compilation).
- Runs the code

You'll also notice a new folder has been created, `target`.

`target` contains the binaries for our project.

```
 build   deps   examples   incremental   learn_rust   learn_rust.d
```

Right now, the only important file is `hello_world`.  This file is actually the binary for our program. We can tell it's a binary by running the `ls -l` command in the directory.

To build our project without running it, run:

```
cargo build
```

And now we can run the binary directly: `./target/debug/learn_rust`

This is exactly the same as `cargo run`, but 2 different commands. When we want to build our project and optimize it, run it with the release profile:

```
cargo build --release
```

Using the normal cargo build for quick checking of code. Use the release argument to optimize the code to maximum possible that the Rust compiler will allow. We call `--release` a *profile*, specifically the release profile. The Rust compiler has different levels of optimization depending on what you want.
# Variables

All variables, by default, are immutable in Rust. This is a safety feature, but also a productivity feature. Variables that don't change mean you don't have to track down when the value changed, and immutable variables are great for concurrency.

Let's see this in action.

```rust
fn main() {
  let x = 5;
  println!("The value of x is:{}", x);
  x = 1;
  println!("The value of x is:{}", x);
}
```

This code does not compile. It returns this error:

```
error[E0384]: cannot assign twice to immutable variable x 
 --> src/main.rs:4:5  
  |  
2 |     let x = 5;  
  |         -  
  |         |  
  |         first assignment to `x`  
  |         help: make this binding mutable: `mut x`  
3 |     println!("The value of x is: {}", x);  
4 |     x = 1;  
  |     ^^^^^ cannot assign twice to immutable variable
```

The error tells us everything we need to know. 

`cannot assign twice to immutable variable`.

This is telling us that we are assigning a value to an immutable variable (a variable that cannot be changed), twice. Which cannot happen. It is important we get compile-time errors, as this can lead to bugs and undefined behavior, which can lead to insecure code. In Rust, once an immutable variable is set Rust guarantees it will never change in its lifetime.

To make a variable mutable, we must place the `mut` keyword in front of it like so:

```rust
fn main() {
  let mut x = 9;
  println!("The value of x is: {}", x);
  let x = 4; 
  println!("The value of x is: {}", x);
}
```

This code compiles and runs correctly:

```
cargo run
```

```
   Compiling hello_world v0.1.0 (/tmp/hello_world)  
    Finished dev [unoptimized + debuginfo] target(s) in 0.14s  
     Running `target/debug/hello_world`  
The value of x is: 9  
The value of x is: 4
```

Being unable to change the value of a variable might have reminded you of another programming concept that most other languages have: `constants`. Like immutable variables, constants are values that are bound to a name and are not allowed to change, but there are a few differences between constants and variables.

Refer to this code for the tasks.

```rust
fn main() {  
    let x: u32 = 5;  
    println!("The value of x is: {}", x);  
    x = "hello";  
    println!("The value of x is: {}", x);  
}
```
# Constant Variables

Rust also has constants. These are values that aren't just immutable by default, but are always immutable. Constants can be declared in any scope, including the global scope. This means that we can use their value in any part of our code, or in multiple places at once.

Constants can only be constant, they cannot be set to a function or any other value that may change at runtime. 

We declare constants with the `const` keyword like so:

```Rust
const HUNDRED_THOUSAND: u32 = 100_000;
```

Notice how in Rust, we can use the `_` character to denote a space in numbers without it affecting the value itself. This is purely for readability.

Also note that it is tradition to name a constant in all **uppercase**.
## Shadowing

We're going to show something that might not make sense at first.

```rust
fn main() {
    let x = 6;
    let x = x + 1;
    println!("{}", x)
}
```

This is called *shadowing*. Rustaceans (Rust programmers) say that;

"The first variable is *shadowed* by the second."

Which means the second variables value appears when used. We can change the type of an immutable variable once it has been defined. Here's an explanation from the official Rust docs about this principle (edited to match the example).

"This program first binds x to a value of 6. Then it shadows x by repeating `x =`, taking the original value and adding 1 so the value of `x` is then `7`".

By using `let`, we can perform transformations on the variable but have the variable still be immutable after all the transformations have completed. We're effectively creating a new variable with the `let` keyword, which means we can change the type of the value.

```rust
let word = "hello";
let word = word.len();
```

Which is allowed. However, if we tried to use `mut`, it wouldn't be allowed, as `mut` cannot change types. 

```rust
let mut word = "hello";
word = word.len();

error[E0308]: mismatched types    
--> src/main.rs:3:12     
  |   
3 |     word = word.len();     
  |            ^^^^^^^^^^ expected `&str`, found `usize` ``
```
# Data Structures

In Rust we'll very oftne see the compiler complain that our variables and functions aren't type hinted. We saw type hits with `CONST` earlier. A **type hint** defines what they data type of a variable is at compile time.

```rust
let ports: u32 = 65535
```

