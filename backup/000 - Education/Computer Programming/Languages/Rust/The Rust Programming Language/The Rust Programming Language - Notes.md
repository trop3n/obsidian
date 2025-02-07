---
up: "[[Rust Book]]"
tags:
  - "#education/computerprogramming/languages/rust/book/notes"
source: https://doc.rust-lang.org/book/
---

# [Introduction](https://doc.rust-lang.org/book/)

## Who Rust is For

Rust is ideal for many people for a variety of reasons. Let's look at a few of the most important groups.
### Teams of Developers

Rust is proving to be a productive tool for collaboration among large teams of developers with varying levels of systems programming knowledge. Low-level code is prone to a variety of subtle bugs, which in most other languages can be caught only through extensive testing and careful code review by experienced developers.

In Rust, the compiler plays a **gatekeeper** role by refusing to compile code with these elusive bugs, including concurrency bugs. By working alongside the compiler, the team can spend their time focusing on the program's logic rather than chasing down bugs. 

Rust also brings contemporary developer tools to the systems programming world:

- Cargo, the included dependency manager and build tool, makes adding, compiling, and managing dependencies painless and consistent across the Rust ecosystem.
- Rustfmt ensures a consistent coding style across developers.
- The Rust Language Server powers Integrated Development Environment Integration for code completion and inline error messages.
### Students

Rust is for students and those who are interested in learning about systems concepts. Using Rust, many people have learned about topics like *operating systems development*. The community is very welcoming and happy to answer student questions. Through efforts such as this book, the Rust teams want to make systems concepts more accessible to more people, especially those new to programming.
### Companies

Hundreds of companies, large and small, use Rust in production for a variety of tasks. Those tasks include command line tools, web services, DevOps tooling, embedded devices, audio and video analysis and transcoding, cryptocurrencies, bioinformatics, search engines, IoT applications, machine learning and even major parts of the Firefox web browser.
### Open Source Developers

Rust is ofr people who want to build the Rust programming language, community, developer tools, and libraries. We'd love to have you contribute to the Rust language.
### People who Value Speed and Stability

Rust is for people who crave speed and stability in a language. By speed, we mean the speed of the programs that you can create with Rust and the speed at which Rust lets you write them. The Rust compiler's checks ensure stability though feature additions and refactoring. This is in contrast to the brittle legacy code in languages without these checks, which developers are often afraid to modify. 

By striving for zero-cost abstractions, higher-level features that compile to lower-level code as fast as code written manually, Rust endeavors to make safe code be fast code as well. The Rust language hopes to support many other users as well; those mentioned here are merely some of the biggest stakeholders. Overall, Rust’s greatest ambition is to eliminate the trade-offs that programmers have accepted for decades by providing safety and productivity, speed *and* ergonomics. Give Rust a try and see if its choices work for you.
# Chapter 1: Getting Started

Let's start our Rust journey. There's a lot to learn, but every journey starts somewhere. In this chapter, we'll discuss: 

- Installing Rust on Linux, macOS, and Windows.
- Writing a program that prints `Hello World`
- Using `cargo`, Rust's package manager and build system.

## Hello, World!

Now that we've installed Rust, let's write our first Rust program. It's traditional when learning a new language to write a little program that prints the text, `Hello, World!` to the screen, so we will do the same here. 


> [!NOTE] Note
> This book assumes basic familiarity with the command line. Rust makes no specific demands about your editing or tooling or where your code lives, so if you prefer to use an integrated development environment instead of the command line, feel free to do so. Many IDEs now have some degree of Rust support; check the IDE's documentation for details. Recently, the Rust team has been focusing on enabling great IDE support.
### Writing and Running a Rust Program

Next, make a new source file and call it *main.rs*. Rust files always end with the *.rs* extension. If you're using more than one word in your filename, use an underscore to separate them.

Enter this code in the file that was just created, called `main.rs`:

```rust
fn main() {
	println!("Hello, world!")
}
```

To run this code, type the following into the terminal:

```shell
rustc main.rs
./main
Hello, world!
```

Regardless of your operating system, the string `Hello, world!` should print to the terminal. If you don't see this output, refer to "Troubleshooting on Page 3" for ways to get help.
### Anatomy of a Rust Program

Let's review in detail what just happened in your Hello, world! program. Here's the first piece of the puzzle:

```
fn main() {

}
```

These lines define a **function** in Rust. The `main` function is special: it is always the first code that runs in every executable Rust program. The first line declares a function named `main` that has no parameters and returns nothing. If there were parameters, they would go inside the parenthesis, `()`. 

Also, note that the function body is *wrapped in curly brackets `{}`*. Rust **requires** these around **all function bodies**. It's good style to place the opening curly bracket on the same line as the function declaration, adding some space in between. 

At the time of this writing, an automatic formatter tool called `rustfmt` is under development. If you want to stick to a standard style across Rust projects, `rustfmt` will format your code in a particular style. The Rust team plans to eventually include this tool with the standard Rust distribution, like `rustc`. 

Inside the main function is the following code: 

```rust
println!("Hello, world!")
```

This line does all the work in this little program: it prints text to the screen. There are four important details to notice here. First, Rust style is to indent with four spaces, not a tab.

Second, `println!` calls a **Rust macro**. If we called it a function instead, it would be entered as `println` (without the !). We'll discuss Rust macros in more detail in Appendix D. For now, you just need to know that using a `!` means that you're *calling a macro instead of a function*.

Third, you see the `"Hello, world!"` string. We pass this string as an argument to `println!`, and see the string is printed to the screen.

Fourth, we end the line with a semicolon (;), which indicates that this expression of over and the next one is ready to begin. Most lines of Rust code end with a semicolon.
### Compiling and Running are Separate Steps

We've just run a newly created program, so let's examine each step in the process. Before running a Rust program, you must compile it using the Rust compiler by entering the `rustc` command and passing it in the name of your source file, like this:

```
rustc main.rs
```

If you have a C or C++ background, you'll notice this is similar to `gcc` or `clang`. After compiling successfully, Rust outputs a binary executable. On Linux, macOS and PowerShell on Windows, you can see the executable by entering the `ls` command in your shell as follows:

```
ls
main main.rs
```

This shows the source code file with the `.rs` extension, the executable file (*main.exe* on Windows, but *main* on all other platforms), and, when using CMD, a file containing debugging information with the *.pdb* extension. From here, you run the *main* or *main.exe* file, like this:

```
./main # or .\main.exe on Windows
```

If *main.rs* was your Hello, world! program, this line would print `Hello, world!` to your terminal. 

If you're more familiar with a dynamic language, such as Ruby, Python or JavaScript, you might not be used to compiling and running a program as separate steps. Rust is an *ahead-of-time compiled* language, meaning you can compile a program and give the executable to someone else, and they can run it even without having Rust installed. If you give someone a `.rb`, `.py` or `.js` file, they need to have Ruby, Python or JavaScript installed (respectively). 
	In those languages, you only need one command to compile and run your program. Everything is a **trade-off** in language design. 

Just compiling with `rustc` is fine for simple programs, but as your project grows, you'll want to manage all the options and make it easy to share your code. Next, we'll introduce you to the Cargo tool, which will help you write real-world Rust programs. 
### Hello, Cargo!

***Cargo*** is Rust's build system and package manager. Most Rustaceans use this tool to manage their Rust projects because Cargo handles a lot of tasks for you, such as building your code, downloading the libraries your code depends on, and building those libraries. (We call libraries your code depends on *dependencies*).

The simplest Rust programs, like the one we've written so far, don't have any dependencies. So if we had built the Hello, world program with Cargo, it woul donly use the part of Cargo that handles building your code. As you write more complex Rust programs, you'll add dependencies, and if you start a project using Cargo, adding dependencies will be much easier to do. 

Because the vast majority of Rust projects use Cargo, the rest of this book assumes that you're using Cargo, too. Cargo comes installed with Rust if you used the official installers. 

To check if Cargo is installed, run: 

```
cargo --version
```

If you see a version number, you have it. If not, you do not have Cargo installed. 
### Creating a Project with Cargo

Let's create a new project using Cargo and look at how it differs from our original Hello, world! project. Navigate back to your *projects* directory (or wherever you decided to store your code). Then, on any OS run the following:

```
cargo new hello_cargo --bin
cd hello_cargo
```

The first command creates a new binary executable called `hello_cargo`. The `--bin` argument passed to a `cargo new` makes an executable application (often just called a *binary*) as opposed to a library. We've named our project *hello_cargo*, and Cargo creates its files in a directory of the same name. 

Go into the `hello_cargo` directory and list the files. We will see that Cargo has generated two files and one directory for us:

- `Cargo.toml`
- `src` directory
	- `main.rs` file inside the directory

It will also initialize a new Git repository along with a `.gitignore` file. 

> [!NOTE]
> Git is a common version control system. You can change cargo new to use a different version control system or no version control system by using the --vcs flag. Run cargo new --help to see the available options.

Open `Cargo.toml` in your text editor of choice. It should look similar to the listing below:

```toml
[package]
name = "hello_cargo"
version = "0.1.0"
authors = ["Your Name <you@example.com."]
```

This file is in the *TOML* (*Tom's Obvious, Minimal Language*) format, which is Cargo's configuration format. 

The first time `[package]`, is a section heading that indicates that the following statements are configuring a package. As we add more information to this file, we'll add other sections. 

The next three lines set the configuration information Cargo needs to compile your program: the name, the version, and who wrote it. Cargo gets your name and email information from your environment, so if that information is not correct, fix the information now and then save the file. 

The last line, `[dependencies]`, is the start of a section for you to list any of your project's dependencies. In Rust, packages of code are referred to as *crates*. We won't need any other crates for this project, but we will in the first project in Chapter 2.

Now, let's open *src/main.rs* and take a look:

```rust
fn main() { 
    println!("Hello, world!"); 
}
```

Cargo has generated a Hello, world! program for you, just like the one we wrote earlier. So far, the differences between our previous project and the project Cargo generates are that Cargo placed the code in the *`src`* directory and we have a *`Cargo.toml`* configuration file in the top directory. 

Cargo expects your source files to live inside the *src* directory. The top-level project directory is just for README files, license information, configuration files, and anything else not related to the code. Using Cargo helps you organize your projects. There's a place for everything, and everything is in its place. 

If you started a project that doesn't use Cargo, as we did earlier with Hello, world, you can convert it to a project that does use Cargo. Move the project code into the *src* directory and create an appropriate *Cargo.toml* file. 
### Building and Running a Cargo Project

Now let's look at what's different when we build and run the Hello, world! program with Cargo. From your *hello_cargo* directory, build your project by entering the following command:

```
cargo build
Compiling hello_cargo v0.1.0 (file:///projects/hello_cargo) 
Finished dev [unoptimized + debuginfo] target(s) in 2.85 secs
```

This command **creates an executable file** in `target/debug/hello_cargo` rather than in your current directory. You can run the executable with this command:

```
./target/debug/hello_cargo
Hello, world!
```

If all goes well, `Hello, world!` should print to the terminal. Running `cargo build` for the first time also causes Cargo to create a new file at the top level: *`Cargo.lock`*. This file keeps track of the exact versions of dependencies in your project. This project doesn't have dependencies, so the file is a bit sparse. You won't ever need to change this file manually; Cargo manages its contents for you.

We just built a project with `cargo build` and ran it with `./target/debug/hello_cargo`, but we can also use `cargo run` to compile the code and then run the resulting executable all in one command: 

```
cargo run 
	Finished dev [unoptimized + debuginfo] target(s) in 0.0 secs 
	 Running `target/debug/hello_cargo` 
Hello, world!
```

Notice that this time we didn't see output indicating that Cargo was compiling `hello_cargo`. Cargo figured out that the files hadn't changed, so it just ran the binary. If you had modified your source code, Cargo would have rebuilt the project before running it, and you would have seen this output:

```
cargo run 
	Compiling hello_cargo v0.1.0 (file:///projects/hello_cargo) 
	 Finished dev [unoptimized + debuginfo] target(s) in 0.33 secs 
	  Running `target/debug/hello_cargo` 
Hello, world!
```

Cargo also provides a command called `cargo check`. This command quickly checks your code to make sure it compiles but doesn't produce an executable: 

```
cargo check 
	Compiling hello_cargo v0.1.0 (file:///projects/hello_cargo) 
	 Finished dev [unoptimized + debuginfo] target(s) in 0.32 secs
```

Why would you not want an executable? Often `cargo check` is much faster than `cargo build`, because it skips the step of producing an executable. If you're continually checking your work while writing the code, using `cargo check` will speed up the process. As such, many Rustaceans run `cargo check` periodically as they write their program to make sure it compiles. Then they run `cargo build` when they're ready to use the executable. 

Let's recap what we've learned so far about Cargo:

- We can build a project using `cargo build` or `cargo check`.
- We can build and run a project in one step using `cargo run`.
- Instead of saving the result of the build in the same directory as our code, Cargo stores it in the `/target/debug` directory.

An additional advantage of using Cargo is that the commands are the same no matter which operating system we are working on. So, at this point, we'll no longer provide specific instructions for Linux and macOS versus Windows.
### Building for Release

When your project is finally ready for release, you can use `cargo build --release` to compile it with optimizations. This command will create an executable in `target/release` instead of `target/debug`. The optimizations make your Rust code run faster, but turning them on lengthens the time it takes for your program to compile. This is why there are two different profiles: one for development, when you want to rebuild quickly and often, and another for building the final program you'll give to a user that won't be rebuilt repeatedly and that will run as fast as possible. If you're **benchmarking** your code's running time, by sure to run `build --release` and benchmark with the executable `target/release`.
### Cargo as Convention

With simple projects, Cargo doesn't provide a lot of value over just using `rustc`, but it will prove its worth as your programs become more intricate. With complex projects composed of multiple crates, it's much easier to let Cargo coordinate the build. 

Even though the `hello_cargo` project is simple, it now uses much of the real tooling you'll use in the rest of your Rust career. In fact, to work on any existing projects, you can use the following commands to check out the code using Git, change to that project's directory, and build:

```
git clone someurl.com/someproject
cd someproject
cargo build
```

For more information about Cargo, check out its documentation at https://doc.rust-lang.org/cargo/.

## Summary 

You’re already off to a great start on your Rust journey! In this chapter, you’ve learned how to:
• Install the latest stable version of Rust using rustup • Update to a newer Rust version 
• Open locally installed documentation 
• Write and run a Hello, world! program using rustc directly 
• Create and run a new project using the conventions of Cargo 

This is a great time to build a more substantial program to get used to reading and writing Rust code. So, in Chapter 2, we’ll build a guess- ing game program. If you would rather start by learning how common programming concepts work in Rust, see Chapter 3 and then return to Chapter 2.
# Chapter 2: Programming a Guessing Game

Let's jump into Rust by working through a hands-on project together. This chapter introduces you to a few common Rust concepts by showing you how to use them in a real program. You'll learn about `let`, `match`, methods, associated functions, external crates, and more. The following chapters will explore these ideas  in more detail. In this chapter, you'll practice the fundamentals.

We'll implement a classic beginner programming problem: a guessing game. Here's how it works: the program will generate a random integer between 1 and 100. It will then prompt the player to enter a guess. After a guess is entered, the program will indicate whether the guess is too low or too high. If the guess is correct, the game will print a congratulatory message and exit. 
## Setting up a New Project

To set up a new project, go to the *projects* directory that we created in Chapter 1 and make a new project using Cargo, like so:

```
cargo new guessing_game --bin
cd guessing_game
```

The first command, `cargo new`, takes the name of the project (`guessing game`) as the first argument. The `--bin` flag tells Cargo to make a binary project, like the one in Chapter 1. The second command changes to the new project's directory. 

Let's look at the generated *Cargo.toml* file.

```toml
[package]
name = "guessing_game"
version = "0.1.0"
edition = "2021"

[dependencies]
```

If the author information that Cargo obtained from your environment is not correct, fix that in the file and save it again. 

As we saw in chapter 1, `cargo new` generates a "Hello World" program for you. Check out the *src/main.rs* file:

```rust
fn main() {
	println!("Hello, world!")
}
```

Now let's compile this "Hello, world!" program and run it in the same step using the `cargo run` command. 

The `run` command comes in handy when you need to rapidly iterate on a project, as we'll do in this game, quickly testing each iteration before moving on to the next one. 

Reopen the *src/main.rs* file. You'll be writing all the code in this file.
## Processing a Guess

The first part of the guessing game program will ask for user input, process that input, and check that the input is in the expected form. To start, we'll allow the player to input a guess. Enter the code in Listing 2-1 into `src/main.rs`:

```rust
use std::io

fn main() {
    println!("Guess the number!");

    println!("Please input your guess.");

    let mut guess = String::new();

    io::stdin().read_line(&mut guess)
        .expect("Failed to read line");

    println!("You guessed: {}", guess);
}
```

This code contains a lot of information, so let's go over it line by line. To obtain user input and then print the result as an output, we need to bring the `io` (input/output) library into scope. The `io` library comes from the standard library (which is known as `std`).

```rust
use std::io;
```

By default, Rust brings only a few types into the scope of every program in the *prelude*. If a type you want to use isn't in the prelude, you have to bring that type into scope explicitly with a `use` statement. Using the `std::io` library provides you with a number of useful features, including the ability to accept user input. 

As we saw in Chapter 1, the `main` function is the entry point into the program:

```rust
fn main() {
```

- The `fn` syntax declares a new function
- the parenthesis `()` indicate there are no parameters
- the curly bracket, `{` starts the body of the 

`println!` is a **macro** that prints a string to the screen. 

```rust
println!("Guess the number!");

println!("Please input your guess.")
```
### Storing Values with Variables

Next, we'll create a `variable` to store the user input, like this:

```rust
let mut guess = String::new();
```

Now the program is getting interesting! There's a lot going on in this little line. We use the: `let` statement to create the variable. Here's another example:

```rust
let apple = 5;
```

This line creates a new variable named `apples` and binds it to the value 5. In Rust, variables are **immutable** by default, meaning *once we give the variable a value, the value won't change.* We will be discussing this concept in detail in the [“Variables and Mutability”](https://doc.rust-lang.org/book/ch03-01-variables-and-mutability.html#variables-and-mutability) section in Chapter 3. To make a variable mutable, we add `mut` before the variable name:

```rust
let apples = 5; // immutable
let mut bananas = 5; // mutable
```

> [!NOTE]
> The `//` syntax starts a ***comment*** that continues until the end of the line. Rust ignores everything in comments. We will discuss this more in Chapter 3.

Returning to the guessing game program, you now know that `let mut guess` will introduce a mutable variable named `guess`. The equal sign (`=`) tells Rust we want to bind something to the variable now. On the right of the equal sign is the value that `guess` is bound to, which is the result of calling `String::new`, a function that returns a new instance of a `String`. [`String`](https://doc.rust-lang.org/std/string/struct.String.html) is a string type provided by the standard library that is a growable, UTF-8 encoded bit of text.

The `::` syntax in the `::new` line indicates that `new` is an *associated function* of the `String` type. An ***Associated Function*** is: 

- A function that's implemented on a type, in this case `String`. 

This `new` function creates a new, empty string. You'll find a `new` function on many types because it's a common name for a function that makes a new value of some kind. 

In full, the `let mut guess = String::new;` line has created a mutable variable that is currently bound to a new, empty instance of a `String`. Whew.
### Receiving User Input

Recall that we included the input/output functionality from the standard library with `use std::io;` on the first line of the program. Now we'll call the `stdin` function from the `io` module, which will allow us to handle user input: 

```rust
io::stdin()
	.read_line(&mut guess)
```

If we had not imported the `io` library with `use std:io;` at the beginning of the program, we could still use the function by writing this function call as `std::io::stdin`. The `stdin` function returns an instance of [`std::io::Stdin`](https://doc.rust-lang.org/std/io/struct.Stdin.html), which is a type that represents a handle to the standard input for your terminal.

