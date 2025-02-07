---
up: "[[Become a Rust Professional]]"
tags:
  - "#education/computerprogramming/languages/rust/becomearustpro/anatomy"
---

# Introduction

We're going to learn about a lot of different things in Rust: functions, strings, and numbers are just some examples we've seen so far. As we program in Rust, we're going to need to assemble these things into something that the language allows.

This section will give us an overall look at how Rust programs are put together. We want to:

- Cover the names of different things so we can refer to them
- Give an idea of how all these things fit together
- Starting explaining rules for the correct way to type them into the computer.

# Pairing and Nesting

> A lot of Rust involves a lot of special symbols. Let's look at our "Hello, world!" again.

```Rust
fn main() {
	println!("Hello, world!");
}
```

We have the left parenthesis, right parenthesis, left curly brace, right curly brace, semicoon and double quotes.

- Every left parenthesis has a matching right parenthesis
- Every left curly brace has a matching right curly brace
- There's no "left double quote" and "right double quote", but there are two double quotes that form a pair.

This is pretty common in Rust. We use these special symbols to group stuff together. For example, the curly braces group together the body of the function. The second set of parenthesis group the parameter list passed to the `println!` macro. And the double quotes group together the string parameter. 

The other important part of all this is that these pair nest. In other words, you can put one pair of symbols inside another. And notice in the program above that we always close off the inner pair before closing the outer pair. 

In other words, the code above is correct, but this code is incorrect:

```Rust
fn main() {
	println!("Hello, world!"});
}
```

By moving the right curly brace before the right parenthesis, we've messed up the nesting, and our code is no longer valid. In order to write correct code, make sure that you close off each pair of symbols in the correct order.

# Layout

