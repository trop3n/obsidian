#nix #nixos #nixflakes
# Introduction

Nix is a tool for managing packages and system configuration that has seen a lot more interest in the last few years. Nix in 2022 is an inflection point - a new generation of tooling widely adopted among the userbase and considered to be easier to use, but the official documentation still largely explains how to do it in the traditional style. 

This guide is a beginner's guide to Nix and related tooling, focusing on the newer `nix` command, and `flake.nix` compared to older tools like `nix-env` and `default.nix`. 

It does not require any prior nix knowledge, and instead builds up the Flake based world from first principles, so that it can serve as an introduction to Nix itself, as well as the concept and uses of flakes. 

1. [Overview](https://tonyfinn.com/blog/nix-from-first-principles-flake-edition/nix-1-nix-guide-overview/)
2. [Installation](https://tonyfinn.com/blog/nix-from-first-principles-flake-edition/nix-2-installation/)
3. [Nix Package Manager CLI](https://tonyfinn.com/blog/nix-from-first-principles-flake-edition/nix-3-package-manager/)
4. [Just Enough Nixlang](https://tonyfinn.com/blog/nix-from-first-principles-flake-edition/nix-4-just-enough-nixlang/)
5. [Derivations](https://tonyfinn.com/blog/nix-from-first-principles-flake-edition/nix-5-derivation-intro/)
6. [Nixpkgs - How Not to Reinvent the Wheel](https://tonyfinn.com/blog/nix-from-first-principles-flake-edition/nix-6-nixpkgs-not-reinventing-the-wheel/)
7. [What about flakes then?](https://tonyfinn.com/blog/nix-from-first-principles-flake-edition/nix-7-what-about-flakes-then/)
8. [Flakes and Developer Environments](https://tonyfinn.com/blog/nix-from-first-principles-flake-edition/nix-8-flakes-and-developer-environments/)
9. [Runnable Flakes](https://tonyfinn.com/blog/nix-from-first-principles-flake-edition/nix-9-runnable-flakes/)

# Overview

The big draws of Nix include declarative, portable, cross lang dependency specification, and the ability to have a config file declare the entire system without storing a huge docker container artifacts for every permutation.

Actually learning Nix feels much harder than it needs to be. The biggest problem is that the documentation you need is often fragmented among the different subprojects, and also the transition that Nix is in at the moment fromt he current stand methods of `default.nix`, `configuration.nix` and `shell.nix` to a new world of `flakes`.

As an outsider looking in, the flake world felt kind of in limbo at the moment where anyone I talked to indicated that flakes fix so many problems with current nix, but also they're still officially experimental so the official documentation declines to mention flakes.

After spending a fair amount of time understanding Nix for myself, I've decided to write my own guide which explains it from scratch in a world using only the new Nix features, with the `nix` CLI and flakes for the use cases I want from Nix. Credit to [ianthehenry](https://ianthehenry.com/posts/how-to-learn-nix/) for his guide on Nix focused on the "old world" approach, and [Xe Iaso](https://xeiaso.net/blog/nix-flakes-1-2022-02-21) for explaining flakes. The information included in this guide is largely from synthesising their blogs and the official documentation.

This first post will describe the major parts of the Nix ecosystem.

## So, What is Nix Anyways?

At its core Nix is a technology for dealing with package management, primarily software packages. A software package can be a program in it's own right, or some library that allows other programs or libraries to work. Like most package managers, Nix will also manage the dependencies of a program. For example if package X requires lib Y, obtaining package X will also obtain lib Y.

One of the common problems with understanding Nix is the many projects that are under the umbrella and how they interact. Depending on your use case you may use a subset of these. A brief overview of the moving pieces here.

- *Nix (Package Manager)*: [The Nix package manger](https://nixos.org/manual/nix/stable/introduction.html) is one piece of the Nix stack that you're going to be using regardless of which use case you're hoping to tackle. This is the software application that actually turns your configuration or command line arguments into built software applications.
- *Nix (Language)*: [The Nix programming language](https://nixos.org/manual/nix/stable/language/index.html), sometimes called `Nixlang` to distinguish from the package manager is a **functional programming language** which is the normal way of configuring Nix packages and NixOS systems. If you have some familiarity with functional language concepts like currying or let-bindings then it will be familiar to you, but if you're more used to mainstream languages (including ones like Python or Java which have taken some functional concepts but not all), there will be a steeper learning curve.
- *Nixpkgs*: [Nixpkgs](https://nixos.org/manual/nixpkgs/stable/#vim) are effectively a **standard library for Nix**. It's packaged separately to the package manager and library because a given nix language program can choose to import different versions of Nixpkgs, which makes it a bit more like the `Golang` standard library than others where your version of the library is tied to the language. It contains both the official definitions of a wide variety of software, along with Nix language functions useful in writing your own Nix code.
- *NixOS*: [NixOS](https://nixos.org/) is a Linux distribution which is built upon the Nix package manager. This means that the usual way of configuring it is writing a program in Nix (the language) to be consumed by Nix (the package manager).You could also use the procedural commands of the Nix package manager and have an experience closer to a standard Linux distro.

There are a number of adjacent projects like [NixOps](https://github.com/NixOS/nixops) for deploying to remote NixOS systems or [nixos-generators](https://github.com/nix-community/nixos-generators) for producing images from Nix config files which I'll touch on later, but these four are the official core.
# Installing Nix

Nix can be installed on Linux or Mac systems. If you're using the Nix based Linux distribution, NixOS, then you'll already have it installed. Otherwise the official nix website provides [the most up to date installation steps](https://nixos.org/download.html#download-nix), which at the time of writing are

Linux:

```sh
sh <(curl -L https://nixos.org/nix/install) --daemon
```

Mac:

```sh
sh <(curl -L https://nixos.org/nix/install)
```

Windows (run in WSL):

```sh
sh <(curl -L https://nixos.org/nix/install) --no-daemon
```

The default on Linux and MacOS is to do what's called a multi-user install, where Nix packages are available to all users. This does require more involved setup steps - luckily however, the official installer handles this for you these days. It will also create some user accounts to run build scripts isolated from your current user profile.

The multi-user install creates a directory `/nix`, which all packages are installed into. This is technically configurable, but if you do so you'll need to compile all packages yourself, as for example, native libraries hardcode their search path into the binary itself when compiled with your C compiler. On the other hand, if you stick with the defaults, you'll be able to download packages from the official Nix package cache.

Since version 10.11, MacOS makes this process harder than it was, so the MacOS installer will also create a virtual volume and mount it to `/nix` as it cannot create a `/nix` directory on the root volume due to System Integrity Protection (SIP).

In current releases (2.5+), the new CLI and flake tooling are still marked experimental. These are two features of the new nix tooling that make it much nicer to use than the old style, so the next step after installation will be to enable them. To enable these features, edit `/etc/nix/nix.conf` and add/modify the following line:

```
experimental-features = nix-command flakes
```

With that you're all set up for the modern Nix experience, [Next time](https://tonyfinn.com/blog/nix-from-first-principles-flake-edition/nix-3-package-manager/), I'll guide you in trying out the nix package manager CLI.

# Nix Package Manager CLI

The foundational part of Nix is the Nix package manager. This is a tool that allows you to install packages. The "first layer" of Nix usage is to use this tool to install packages. The Nix Package manager, similar to projects like os-rpmtree (used in Fedora Silverblue) or snapper (used in snap based Linux distros), will allow you to easily revert package installs or updates if something goes wrong. 

This post covers the basics of using the nix package manager at the command line -- while most users use nix through more advanced workflows, the basics explained here will be useful in understanding those workflows, as well as for users who want to dip their toes into Nix by treating it like a more traditional package manager to start out. 

To install your first package, run the `nix profile install` command. The package used in this demonstration is `ripgrep`, which is a Rust based grep alternative that has a nice out of the box experience. 

```sh
nix profile install nixpkgs#ripgrep
```

The command tells `nix` to install the `ripgrep` package from the `nixpkgs` registry into the default profile. If you followed the installer you should now be able to run the `rg` binary from the `ripgrep` package.

Let's install a few more packages, like `jq` the CLI tool for JSON and `fzf` a fuzzy finder that lets you search a list of CLI arguments and select one.

```
nix profile install nixpkgs#fzf nixpkgs#jq
```

Now you can observe what it set up. By default, `nix profile` will set itself up in your `~/.nix-profile` directory.

```
> ls -l ~/.nix-profile/
total 4
dr-xr-xr-x 1 root root  44 Jan  1  1970 bin/
-r--r--r-- 1 root root 500 Jan  1  1970 manifest.json
dr-xr-xr-x 1 root root  78 Jan  1  1970 share/

> ls -l ~/.nix-profile/bin/
total 20
lrwxrwxrwx 1 root root 62 Jan  1  1970 fzf -> /nix/store/bds5wjz9js59y9ccwmryav4klc7ir8wg-fzf-0.34.0/bin/fzf*
lrwxrwxrwx 1 root root 68 Jan  1  1970 fzf-share -> /nix/store/bds5wjz9js59y9ccwmryav4klc7ir8wg-fzf-0.34.0/bin/fzf-share*
lrwxrwxrwx 1 root root 67 Jan  1  1970 fzf-tmux -> /nix/store/bds5wjz9js59y9ccwmryav4klc7ir8wg-fzf-0.34.0/bin/fzf-tmux*
lrwxrwxrwx 1 root root 61 Jan  1  1970 jq -> /nix/store/348rj7g1gg2fnz91qilrnd0sc8nchls1-jq-1.6-bin/bin/jq*
lrwxrwxrwx 1 root root 65 Jan  1  1970 rg -> /nix/store/cmzib5qfpqsc9fq1h0i8hawdzn612jw4-ripgrep-13.0.0/bin/rg*

> ls -l ~/.nix-profile/share/
total 20
lrwxrwxrwx 1 root root  80 Jan  1  1970 bash-completion -> /nix/store/cmzib5qfpqsc9fq1h0i8hawdzn612jw4-ripgrep-13.0.0/share/bash-completion/
dr-xr-xr-x 1 root root 102 Jan  1  1970 fish/
lrwxrwxrwx 1 root root  64 Jan  1  1970 fzf -> /nix/store/bds5wjz9js59y9ccwmryav4klc7ir8wg-fzf-0.34.0/share/fzf/
lrwxrwxrwx 1 root root  68 Jan  1  1970 man -> /nix/store/cmzib5qfpqsc9fq1h0i8hawdzn612jw4-ripgrep-13.0.0/share/man/
lrwxrwxrwx 1 root root  72 Jan  1  1970 vim-plugins -> /nix/store/bds5wjz9js59y9ccwmryav4klc7ir8wg-fzf-0.34.0/share/vim-plugins/
lrwxrwxrwx 1 root root  68 Jan  1  1970 zsh -> /nix/store/cmzib5qfpqsc9fq1h0i8hawdzn612jw4-ripgrep-13.0.0/share/zsh/
```

First, note that `~/.nix-profile` is the location of your user's default profile. Every user can have their own independent profile with their own set of installed packages. This doesn't involve duplicating packages if multiple users have them installed, as the multi-user installation will have these all symlink back to your global `/nix` directory.

If you have performed the default installation and you're using a supported shell, then `~/.nix-profile/bin` should already by in our PATH. IF not, you can add it if you want to have your command from your nix profile available at all times. 

Once that's done, let's try and use some of those commands. 

```sh
jq -r '.elements[].attrPath' ~/.nix-profile/manifest.json \
| fzf --preview 'jq --arg attr {} ".elements[] | select(.attrPath == \\$attr)" ~/.nix-profile/manifest.json'
```

You should get a window which lists the three installed packages according to the manifest json file and if you pick an item with arrow keys or typing, it should show you the object from your nix profile that describes the installed package. 

Of course, while rooting around in the `manifest.json` files works nicely as a demonstration of the newly installed `jq` package, you don't need to to this to get a package listing. Instead you can use the `nix profile list` command, which will produce an output like the following:

```
> nix profile list
0 flake:nixpkgs#legacyPackages.x86_64-linux.ripgrep github:NixOS/nixpkgs/b7a47253e0c8cb04c0a3f8ed3149e90229e62884#legacyPackages.x86_64-linux.ripgrep /nix/store/k86k8szjhii474hp7f7xqvvdf7fnfigw-ripgrep-13.0.0
1 flake:nixpkgs#legacyPackages.x86_64-linux.fzf github:NixOS/nixpkgs/b7a47253e0c8cb04c0a3f8ed3149e90229e62884#legacyPackages.x86_64-linux.fzf /nix/store/d6hh0i8fkgqinq7f8hdfvy8r0qk35412-fzf-0.34.0-man /nix/store/v5aza5gg981bzmqw1z0f6lddvnqi9ab4-fzf-0.34.0
2 flake:nixpkgs#legacyPackages.x86_64-linux.jq github:NixOS/nixpkgs/b7a47253e0c8cb04c0a3f8ed3149e90229e62884#legacyPackages.x86_64-linux.jq /nix/store/5x1jpz4grhzl1psmrxj42wzmvllqgbhm-jq-1.6-bin /nix/store/6pnapmlp83dvi974s86lvbmwn5lhdv5b-jq-1.6-man
```

The fields here are:

1. A number referencing the installation order. This can be used as shorthand when installing or uninstalling a package, similar to a short hash in git.
2. The expanded version of the reference is used to install the package. This is used by Nix when it needs to upgrade the package, or by users if they want to have something that's independent of installation order. This is also known as the *mutable flake reference*.
3. The full version of the reference when it is resolved. This means that not only will it refer as the *immutable flake reference*, as it will always get the same result, while the *mutable flake reference* can change as you upgrade your `nixpkgs` version.
4. The location on disk in the nix store the package was stored in.

Finally, you can update a specific package or all packages.

To update a specific package, you can use `nix profile upgrade <pkg reference>`. The package reference can be one of the numbers from `nix profile list`, or the _mutable flake reference_ in either the short version used when installing it or the expanded version in `nix profile list`. To upgrade all packages, you can use `nix profile upgrade '.*'`.
## Generations

So far, I've just encountered how to do the things with Nix that you can do with *any* package manager, and they seem a little more convoluted too, so now it's time to get into what you can do with Nix that your can't do with `apt`, `brew`, or `pacman`.

The first is that Nix keeps multiple versions of installed packages, and a record of the changes made. This allows you to easily rollback management commands. Each version of your profile after you perform a package manager operation is known as a generation.

You can observe this log of history with the `nix profile history` command: 

```
> nix profile history
Version 1 (2022-10-05):
  flake:nixpkgs#legacyPackages.x86_64-linux.ripgrep: ∅ -> 13.0.0

Version 2 (2022-10-05) <- 1:
  flake:nixpkgs#legacyPackages.x86_64-linux.fzf: ∅ -> 0.34.0, 0.34.0-man
  flake:nixpkgs#legacyPackages.x86_64-linux.jq: ∅ -> 1.6-bin, 1.6-man
```

When you run this in your terminal, you will likely see the number 2 highlighted in green to indicate it is the current version.

Now, let's say you didn't want to keep around `jq` and `fzf` as you're done with them now after the demo. In this case, you can run the `nix profile rollback` command.

```
> nix profile rollback
switching profile from version 2 to 1
```

Run `nix profile history` again and you'll now see the version 1 highlighted as the active version.

Change your mind and want to go back to version 2? The `--to` parameter allows you to set a specific version as the target, letting you to go back multiple versions, or, as in this case, forward versions after rollbacks.

```
> nix profile rollback --to 2
switching profile from version 1 to 2
```
## Profiles

The second uncommon feature in Nix is the ability to manage multiple sets of installed packages. While in part 7 I'll get onto flakes and a neater way to manage them on a per-project basis, the `nix profile` command is capable of doing it on its own passing the `--profile` argument to a command. 

```
> nix profile install --profile ~/py39-profile nixpkgs#python39
> nix profile install --profile ~/py310-profile nixpkgs#python310
> ~/py39-profile/bin/python --version
Python 3.9.14
> ~/py310-profile/bin/python --version
Python 3.10.7
```

Each of these profiles has the full suite of nix commands available to it, including upgrades, rollbacks, etc.
## Garbage Collection

Some of you might have heard the mention of Nix keeping all versions of packages around and worried about disk space. There are two commands to keep in mind to resolve this.

The first of these is the `nix store gc` command. This will delete packages that are only used by profiles or generations that have been deleted. This will detect if you just delete a profile with `rm /path/to/profile`, allowing you to delete and free up a profile entirely.

The second is the `nix profile wipe-history` command. This will remove past versions of a profile. By default it will delete all non-current versions of a profile. But if you want to keep some history, you can also use the `nix profile wipe-history --older-than 30d` to delete generations older than 30 days, for example.

With the usage of the package manager now covered, [next time](https://tonyfinn.com/blog/nix-from-first-principles-flake-edition/nix-4-just-enough-nixlang/) I'm going to discuss Nix's programming language.
# Just Enough Nixlang

This is a crash course in Nix's language, which I'll also sometimes call Nixlang from here on, to avoid confusing it with the Nix package manager. For more detailed instructions see [the manual](https://nixos.org/manual/nix/stable/language/index.html). The Nix language is used heavily within Nix, for defining packages, environments, runnable commands and library functions. 

Nix's language is expression-oriented. This means everything, including up to the level of an entire program, has an output video. It will be most familiar if you have experimented with functional languages such as Haskell, but is is less complicated than those languages, so you don't need to have mastered one to start.

To start experimenting with it, you can use the `nix repl` command which will let you type in Nix expressions and see the output.
## Simple Data Types

Nix's basic data types include some you will be familiar with from any language, like numbers or strings.

```nix
# Numbers are typed as is
nix-repl> 1
1


# Strings are surrounded by double quotes
nix-repl> "a"
"a"

# Lists are surrounded in square brackets, 
# and list items are seperated by white space
nix-repl> [ "a" "b" ]
[ "a" "b" ]
```

However, since the language was designed for package management, it also has some first class data types that other languages do not. The most common of these is the PATH.

```nix
nix-repl> ./README.md
/home/tony/code/nix-guide/README.md
```

Path literals are defined by the presence of the `/` forward slash character. This means that for paths in the current directory, you will need to prefix them with `./` to separate them from identifiers.

Nix sets (remember, these are maps/dictionaries in more common terms) are defined with curly braces, with `=` to separate keys from values and `;` at the end of every entry. You'll also see them referred to as *attribute sets* or *attrs* - these all have the same meaning.
## Sets

```nix
# Sets are written in curly braces

nix-repl> { a = 1; b = 2; }
{ a = 1; b = 2; }
```

Notice that every key value pair is terminated by a semicolon - this is not optional, even on the final entry, or on single entry lists.

Because set operations, including on nested sets are so common in Nix, there's a lot of syntax sugar for sets. 

```nix
# You can define nested sets using dots in key names 
nix-repl> { a.x = 1; a.y = 2; b.c = 4; }                       
{ a = { ... }; b = { ... }; }

# Use the :p command at the repl to print recursively
nix-repl> :p { a.x = 1; a.y = 2; b.c = 4; } 
{ a = { x = 1; y = 2; }; b = { c = 4; }; }
```
## Functions

For the final major type of the language, functions are written as a `argument: expression`
and are called by using the function name and a space.

```nix
nix-repl> x = arg: { foo = arg; }

nix-repl> x 123
{ foo = 123; }
```

You can use destructuring to extract fields from sets as arguments. This gives an argument passing style similar to keyword arguments in languages like Python or objects in JavaScript.

```nix
nix-repl> x = { foo, bar }: {a = foo; b = bar; }

nix-repl> x { foo = 1; bar = 2; }
{ a = 1; b = 2; }
```

But what if you want multiple positional arguments? Similar to languages like Haskell, functions use what is known as currying to handle multiple arguments. This means that any function which take multiple arguments is actually represented as functions which take a single argument and return another function. If you are familiar with the concept, feel free to skip the next section.
### Curried Functions for Functional Programming Novices

This can be a hard thing to wrap your head around if you've never encountered it before, so for people who're encountering this the first time I'm going to give an example in JavaScript first.

```javascript
// Your standard two argument function
function add(a, b) {
    return a + b;
}

console.log(add(1, 2)); // 3
```

You could also write this as:

```javascript
function add(a) {
    return function (b) {
        return a + b;
    }
}

console.log(add(1)(2)); // 3
```

Why would you want to write a function like this? The reason is that it lets you provide the arguments at different times to each other.

```javascript
function runOnUsersData(username) {
    const data = fetchData(username); // Some big expensive operation.

    return function(f) {
        return f(data);
    }
}

function average(executor) {
    const sum = executor((data) => sum(data));
    const count = executor((data) => count(data));
    return sum / count;
}

function bobsAverage() {
    const executor = runOnUsersData("bob");
    average(executor);
}
```

In this simplified case, you could have just loaded the data into a variable, but the advantage here is this interface is the same regardless of whether you can pull all the data into a data structure or if you're shipping the functions themselves off to run on a hadoop job or lambda function or some other novel setup. By using this style, you can change these kind of details and the average function doesn't need to change.
#### Regrouping

Now that the functional and non-functional audiences are back together, how do you use function currying in *Nix*, not JavaScript? Since this is a much more standard practice in Nix, the syntax for this is very minimal.

```nix
adder = amountToAdd: x: amountToAdd + x
```

This is effectively a function which takes an argument `amountToAdd`, then returns the function `x: amountToAdd + x`
## Three Final Pieces of Syntax

Ok, you're nearly done with this crash course in Nixlang. There's three final commonly used pieces of syntax that need to be covered, and then you'll be able to start writing your own nix expressions.
### Let

So far you'll notice that I've never actually explained how to set a variable. While I've used the `x = "abc"` syntax in the REPL, this is a piece of REPL specific usage. As mentioned earlier, even a Nix program is a single expression, so there's no sequential code in your own nix programs to assign a variable on one line and use it again in another. But what if you have some value you want to use multiple times?

In that case you can use a let expression to create what is called a **binding**.

A basic let expression looks as follows:

```nix
# "abcabc"
let x = "abc"; in x + x;

# "abcxyz"
let x = "abc"; y = "xyz"; in x + y; 
```

Notice that as in set definitions, the semicolon at the end is required here -- it's a terminator, not a separator. This is also not an assignment like let expressions in languages like Rust or JavaScript. The values are only available for the single expression after the let keyword.
### With

The next expression is also a way to introduce new values in scope. This is the `with` expression. This takes all the fields of a set and makes them available as bindings within the expression following the with. It looks like this:

```nix
with <some-set>; <expression>
```

Here's an example:

```nix
let longNameSet = {
    foo = 1;
    bar = 2;
}; in ( # Brackets optional, added for clarity
    with longNameSet; {
        sum = foo + bar;
    }
)
```

This produces the set `{ sum = 3; }`. It could also have been written as:

```nix
let longNameSet = {
    foo = 1;
    bar = 2;
}; in {
    sum = longNameSet.foo + longNameSet.bar;
}
```

This is most like the JavaScript `with` expression, which does basically the same thing. I'm still out on if I like this syntax as used here, my gut feeling is to dislike it for all the same reasons I dislike `with` in JavaScript or `import *` in various languages, but `with` is everywhere in real Nix code, so you'll need to know it.
### Inherit

`inherit` is used to copy values from an outer scope into a set being constructed. An example is below:

```nix
let someVariableWithALongName = 5; in {
    inherit someVariableWithALongName;
}
```

This produces the set `{ someVariableWithALongName = 5; }`. This is because it's equivalent to

```nix
let someVariableWithALongName = 5; in {
    someVariableWithALongName = someVariableWithALongName;
}
```

With this basic grounding of the Nix language features, [next time](https://tonyfinn.com/blog/nix-from-first-principles-flake-edition/nix-5-derivation-intro/) I'm going to discuss a final fundamental structure to tie the language and package manager together.
# Derivations

So, time to explain the Nix **derivation**. A Nix `derivation` is a special type of set created from the `derivation` function which describes how to obtain and build a package. The Nix package manager will then evaluate this derivation, and use the result to copy the build package into the Nix store, which is effectively a folder with all locally Nix built or installed packages in it. The subfolders are hashes derived from the inputs to the expression that built the stored packages.

`derivation` itself takes a set as an argument, which it will expand out into the full derivation when evaluated. There are three mandatory arguments:

- `system` defines what architecture and OS this package is for, e.g. `x86_64-linux` or `aarch64-darwin`. Note there is no `any` architecture, if you want a portable package you'll need to define it for every architecture it's portable to.
- `name` is a string which gives the package a name. Conventionally the version is appended, e.g. python-3.10.0.
- `builder` is a program that is run to build the derivation.

You can define extra variables, and they're passed to the `builder` as environment variables. If a variable is a path, there's a special behavior -- the object at the path is copied into the nix-store itself, and the path to the copy in the nix store is provided as the environment variable. 

There's one other variable of note, which is `outputs`. This is a list of strings which name speciifc outputs which this derivation builds. By default, a derivation builds a single output, which is `"out"` but you could for example include debug symbols or high res assets for a game as other outputs. The build script is expected to build all outputs, but someone installing the package in the future could select only a subset of outputs. Each output results in a target directory for that output being created. 
## Your First Nix Derivation

With the over covered, it's time to write your first derivation. To write a Nix derivation, you need the following:

1. Something to install. Let's use this basic shell script:

```sh
#!/bin/sh
echo "Hello World"
```

2. A build script which produces the build output. Since a shell script is already executable, your build script should just copy it into place. 

`builder.sh`

```sh
#!/bin/sh
cp $src $out
```

3.  A Nix expression which defines the derivation as using the src and builder just created.

`expression.nix`

```
derivation {
    builder = ./builder.sh;
    src = ./hello.sh;
    name = "hello-1.0";
    # replace with x86_64-darwin, aarch_64-darwin or aarch64-linux
    system = "x86_64-linux";
}
```

So, how do we run this derivation?

You run the `nix build` command. Since you only have a standalone Nix expression in a file for now, you can use the `-f` option to tell it which file to build. So let's try it.

```
nix build -f expression.nix
```

This doesn't quite work...

```
error: builder for '/nix/store/inhcxhma450491shf69xmf2960lfcr2a-hello-1.0.drv' failed with exit code 127;
       last 1 log lines:
       > /nix/store/j67w54ch35bca45cbvzx2qdg9p7557fc-builder.sh: line 2: cp: not found
       For full logs, run 'nix log /nix/store/inhcxhma450491shf69xmf2960lfcr2a-hello-1.0.drv'.
```

The issue here is with the `line 2: cp: not found`. The derivation is built in an isolated environment, and since you haven't included anything in that environment, you get a bourne compatible shell and not much else. Since `cp` is not a shell builtin, you'll need to provide the command.
### Bootstrapping

So let's bootstrap a bit. First grab a copy of [busybox's cp](https://www.busybox.net/downloads/binaries/1.35.0-x86_64-linux-musl/busybox_CP) and put it next to your expression.nix. Next, update your derivation to copy the command into the build environment of your derivation:

```nix
derivation {
    builder = ./builder.sh;
    src = ./hello.sh;
    name = "hello-1.0";
    system = "x86_64-linux";
    # busybox_CP will be copied to the nix store, and the path 
    # will be put in the $cp env variable.
    cp = ./busybox_CP; 
}
```

Then you can update the builder script to use this version of `cp`

```
#!/bin/sh
$cp $src $out
```

Finally, make the busybox_CP binary executable with a `chmod +x busybox_CP` - this executable flag will be copied into your build environment.

Now let's try run `nix build -f expression.nix` again:

```
> nix build -f expression.nix
>
```

No errors are outputted, and you will notice a new file called `result` which is a symlink to the location in the Nix store where your derivation output is stored.

```
> ls -l result 
lrwxrwxrwx 1 tony users 53 Sep 29 01:28 result -> /nix/store/5nhksvqwn944c6q3vqayqyla6k7n1yv6-hello-1.0*
```

And if you run `./result`:

```
> ./result 
Hello World
```

Congratulations, you've built your first nix package. Don't worry, in real world scenarios (next post will cover `stdenv`), you won't need to bring your own `cp` and other fundamental tools.
### Cleaning Up

Still, even before you get onto the whole `stdenv` and all it's tools it's a bit ugly to copy busybox's `cp` into your project. Not to mention having to manually `chmod +x` to build the derivation, when ideally for reproducibility, you want all the steps to be listed. So let's make a few improvements to this first derivation.

First, the new `expression-v2.nix`:

```nix
let 
  fetchurl = import <nix/fetchurl.nix>;
in derivation {
    builder = ./builder.sh;
    src = ./hello.sh;
    name = "hello-1.0";
    system = "x86_64-linux";
    cp = fetchurl {
      # Download from the busybox server
      url = "https://www.busybox.net/downloads/binaries/1.35.0-x86_64-linux-musl/busybox_CP";
      # Check the downloaded file against the hash so Nix knows if the build is not reproducing
      # Download the file once and use `nix hash to-base32 $(nix hash path busybox_CP)`
      # to find the value to put here
      sha256 = "0mq1487x7aaz89211wrc810k9d51nsfi7jwfy56lg3p20m54r22a";
      # Have Nix make the file executable on download
      executable = true; 
    };
    chmod = fetchurl {
      url = "https://www.busybox.net/downloads/binaries/1.35.0-x86_64-linux-musl/busybox_CHMOD";
      sha256 = "06fp9hqf0cxjqvs9hjg5n81lm5yhkp6iwiaa74j4cfg0wbf7d8fc";
      executable = true;
    };
}
```

And next, the new `build.sh`, which uses that `chmod` command to set the permission flag, saving users from having to run it themselves.

```sh
$cp $src $out
$chmod +x $out
```

From here you could go on to define an ever increasing pile of tools, working your way up to GNU coreutils for a more "normal" build environment, but luckily the Nix team have already done this work for you in the `Nixpkgs` environment, which the [next post](https://tonyfinn.com/blog/nix-from-first-principles-flake-edition/nix-6-nixpkgs-not-reinventing-the-wheel/) will cover.
# Nixpkgs - How Not to Reinvent the Wheel

In the last section it was discussed how to create your first derivation, which allows you to make a first nix package. As you might have noticed, the default execution environment is incredibly barebones, to the point that you needed to include such fundamental tools as `chmod` and `cp`. If that process had to be repeated by every Nix user, it would be very inconvenient. Luckily, there is nixpkgs, which provides a number of packages that the community has already built, along with the shared environment which includes a number of tools to use in building your own. You may remember installing some of these packages in [part 3](https://tonyfinn.com/blog/nix-from-first-principles-flake-edition/nix-3-package-manager/).
## mkDerivation

The first item from the standard environment we're going to discuss is `stdenv.mkDerivation`. This is a function that is an enhanced version of the build in `derivation`. It provides a number of advantages over using `derivation` directly. 

1. It does the bootstrapping for you ensuring you have a decent minimal environment to build on. The [full list of packages](https://nixos.org/manual/nixpkgs/stable/#sec-tools-of-stdenv) can be seen in your current nixpkgs manual, but it includes things like GNU coreutils, bash, tar, gzip, etc. The bash shell is used as the default interpreter for shell scripts, compared to `derivation` which only promises a bourne compatible shell.
2. It provides an easy way to add extra dependencies to your specific derivation and includes them in the path so you don't have to use the `$cp`, `$chmod` variables in the scripts like was required last time. 
3. It provides a default builder which runs in bash and does a `./configure && make` installation, with some variables that lets you override parts of it without having to write a whole new script.

Here's a modified version of the "hello world" derivation from the last part::

```nix
let pkgs = import (fetchTarball "https://github.com/NixOS/nixpkgs/archive/0b20bf89e0035b6d62ad58f9db8fdbc99c2b01e8.tar.gz") {};
in pkgs.stdenv.mkDerivation {
    src = ./hello.sh;
    name = "hello-1.0";
    system = "x86_64-linux";
    dontUnpack = true;
    installPhase = ''
    cp $src $out
    chmod +x $out
    '';
}
```

Here [`fetchTarball`](https://nixos.org/manual/nix/stable/language/builtins.html?highlight=fetchtarball#builtins-fetchTarball) is a function from Nix's builtins that downloads a tarball from the internet and stores it in the Nix store. The code then calls `import` on the returned result. `import` evaluates the downloaded value as nix code and then assign the result object to the `pkgs` name. The variable name `pkgs` is customary for nixpkgs, so you may see it used in docs without explaining where it comes from. 

In the call to `mkDerivation`, there are the following differences to the builtin `derivation` example from last time. 

1. There's no `builder` provided - in this example the standard builder provided by the `stdenv` is used, with one phase that is overridden from the `.nix` file. 
2. The `installPhase` option is what overrides this one phase. The script is included inline using Nix's multi-line strings, which are signified with the doubled up single quotes.
3. The `dontUnpack` attribute also tells the builder not to try to unpack the source. Since most software source shave more than one file, the standard builder defaults to treating the src as an archive and trying to unpack it. Here the `src` is just a shell script, so that unpacking is not required.
4. Inside the standard environment, items like `cp` and `chmod` are just available on the path, so they don't need to be explicitly passed - the script just uses them in regular command line use.
### Dependencies

Now that there's no longer a need to rebuild the world inside each derivation, it's time to start a more challenging package, one that needs some dependencies. Let's take an example of a Rust version of the hello world program from before. Even if you've never written Rust before, and don't have any Rust toolchain you can use Nix to get everything needed.

First get Cargo, Rust's build tool/package manager from Nix and have it scaffold a Rust project for this example.

```sh
nix run nixpkgs#cargo init rust-hello
```

You will see a download progress bar as it downloads cargo from the nixpkgs cache, then it runs that `cargo` command with the rest of the arguments, as if you had run `cargo init rust-hello` with a locally installed version. Unlike `nix profile install`, the downloaded version of `cargo` isn't kept around permanently - it will be deleted at the next GC.

Cargo will then generate two files. Conveniently, when you generate a new Rust project, it prefills in a hello world program to get you started. 

```toml
name = "rust-hello"
version = "0.1.0"
edition = "2021"

# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

[dependencies]
```

```rust
fn main() {
    println!("Hello, world!");
}
```

Now it's time to write a derivation to produce a build output from this. 

The first new feature needed is a new argument to `stdenv.mkDerivation`. This argument is `nativeBuildInputs`. This is used to download dependencies that need to run on the system building the package, and produce output suitable for the system intended to run the package. 

```
nativeBuildInputs = [pkgs.cargo]
```

The second new feature used is that the script now overrides a second phase of the standard builder, the `buildPhase`. As the name suggests, this is where you should run commands to build your software. In this case `cargo build --release` is the command to build an optimized version of a Rust program. Since `pkgs.cargo` was added to the `nativeBuildInputs` section, `cargo` is available on the `PATH` of the build script.

```nix
buildPhase = ''
    cargo build --release
'';
```

Finally, this time the script places the output in `$out/bin` rather than copying it direct to `$out`. This is because `stdenv` puts the `$out/bin` directory onto the path of anything declaring this package as a dependency, so by placing the binary here it will be on the path of anything that uses this as a dependency.

```nix
installPhase = ''
    mkdir -p $out/bin
    cp target/release/rust-hello $out/bin/rust-hello
    chmod +x $out
''
```

Putting all of these together, the final derivation is below

#### `rust-derivation.nix`

```nix
let pkgs = import (fetchTarball "https://github.com/NixOS/nixpkgs/archive/0b20bf89e0035b6d62ad58f9db8fdbc99c2b01e8.tar.gz") {};
in pkgs.stdenv.mkDerivation {
    src = ./rust-hello;
    name = "rust-hello-1.0";
    system = "x86_64-linux";
    nativeBuildInputs = [ pkgs.cargo ];
    buildPhase = ''
      cargo build --release
    '';
    installPhase = ''
      mkdir -p $out/bin
      cp target/release/rust-hello $out/bin/rust-hello
      chmod +x $out
    '';
}
```

## Other builders

`stdenv.mkDerivation` is the foundational tool for working with derivations in Nixpkgs, but there's also a library of other builders for common languages and use cases. For example, rather than build the derivation for the first shell example manually, the nix expression could have used the `pkgs.buildShellApplication` builder.

In this case the updated shell derivation would be as follows:

#### `shell-app.nix`

```nix
let pkgs = import (fetchTarball "https://github.com/NixOS/nixpkgs/archive/0b20bf89e0035b6d62ad58f9db8fdbc99c2b01e8.tar.gz") {};
in pkgs.writeShellApplication {
  name = "hello";

  text = ''
    echo Hello World
  '';
}
```

You can also see the [Nixpkgs manual on languages and frameworks](https://nixos.org/manual/nixpkgs/stable/#chap-language-support) to see if there's any builders or utilities for your preferred programming language.

[Next time](https://tonyfinn.com/blog/nix-from-first-principles-flake-edition/nix-7-what-about-flakes-then/), I will cover _flakes_, one of the biggest changes to Nix packaging ever, and the foundation of a lot of the newer methods of interacting with Nix.
# What About Flakes Then?

One of the big new concepts in Nix is the `flake`, which is a new standard format for Nix projects to declare all their outputs. At the beginning of this series, we mentioned them as being one of the major components of modern Nix, and now this series has introduced enough of a foundation it's time to explain flakes themselves.
## What is a Flake?

A `flake` is a standard format for describing a collection of Nix resources. These resources can be packages, of the type described in previous posts, intended to be used to install some software on your system. There's also a number of other types of resources that can be exposed by the flake which we'll cover in later posts. Some examples of these are:

- developer environment descriptions
- modules for configuring NixOS Systems
- runnable commands

By standardizing a format to list all these outputs (compared to the ad-hoc foles this series has been using until now), Nix allows a number of higher level tools to operate on these resources, like the `nix profile install` and `nix run` commands that have been shown in earlier parts.

Finally, the development of the flake based tooling allowed the Nix team to resolve some pain points with the older generation of tooling, such as making the process of recording versions for reproducibility more ergonomic with lock files, or making better ways to identify newer versions of the same package to allow tools to manage updates.
### An Example Flake

For an example flake, here is a version of the Rust derivation from part 6 defined as part of a flake. Save this file as `flake.nix`. Unlike the previous filenames, which have been basically arbitrary, this name is expected by the Nix tooling as the standard name for defining flakes.

```nix
{
  inputs.nixpkgs.url = "github:NixOS/nixpkgs/nixos-22.05";

  outputs = {
    self,
    nixpkgs,
  }: let
    system = "x86_64-linux";
    pkgs = import nixpkgs {inherit system;};
  in {
    packages.${system}.default =
      pkgs.stdenv.mkDerivation
      {
        src = ./rust-hello;
        name = "rust-hello-1.0";
        inherit system;
        nativeBuildInputs = [pkgs.cargo];
        buildPhase = ''
          cargo build --release
        '';
        installPhase = ''
          mkdir -p $out/bin
          cp target/release/rust-hello $out/bin/rust-hello
          chmod +x $out
        '';
      };
  };
}
```

The `flake.nix` file defines a Nix attribute set, with two top level attributes. The first of these is `inputs`, which defines all the dependencies this flake will import from. For this example, the only dependency is `nixpkgs`, and the flake points to its location on GitHub.

The second top level attribute is `outputs`, which is defined as a function returning an attribute set. It receives two arguments, `self`, which is the flake itself so you can refer to other outputs without resorting to `rec`, and `nixpkgs`, which is the input flake defined in the  `inputs` attribute set. If you had defined extra inputs, they would be provided as extra arguments to this function.

When the function is called, it gets the `pkgs` object by importing the `nixpkgs` expression. Inside flakes you also need to tell it which system to build nixpkgs for, so the flake passes it the `x86_64-linux` system field. You may need to change this if you're on a different system, see [part 5](https://tonyfinn.com/blog/nix-from-first-principles-flake-edition/nix-5-derivation-intro/) if you need a reminder of what options are available.

This example flake defines a single output: `packages.x86_64-linux.default`. A variable is used for the `system` part so that it can be updated in a single place at the top of the file. The value of `packages.x86_64-linux.default` is the package expression that we've previously used alone in files - this part is unchanged from Chapter 6.

Now run the `nix build` command. This will lookup the default package for your current system from the flake, then build it. You'll notice like previously a `result` symlink is generated which will contain the built package. It will also generate a `flake.lock` file. This lockfile is the key to not having to manage hashes manually like was needed in the part 6 version - the lock file will automatically record the hashes at the time of building, and tehn you can include that lock file so that other users of your flake can be sure of getting the same versions, while in your script file you just handle a nice identifier (in this case the flake is asking for the version of nixpkgs used in NixOS 22.05, which is the current stable release).

You can also build [my copy of the flake](https://gitlab.com/tonyfinn/nix-guide/-/tree/main/7-flakes/simple) on gitlab, for example with the following command.

```nix
nix build git+https://gitlab.com/tonyfinn/nix-guide?dir=7-flakes
```

The URL-like parameter `git+https://gitlab.com/tonyfinn/nix-guide?dir=7-flakes/simple` provided to `nix build` to build my hosted copy of the flake is called a *flake reference*. This is provided in the format `<flake location>[#flake output]`.

This `git+https` URL is just one type of flake location, other examples are given in the sidebar. 

A flake can have multiple packages defined in one flake. These are defined with a different name than the `default` that has been used so far. For example, let's add a `debug` package. This will be added with a new attribute named called `packages.x86_64-linux.debug` on my Linux system. Two things need to be changed for a debug build. The cargo build command should not have the `--release` flag, and the compiled binary needs to be copied from the `target/debug` folder instead of `target/release`.

### Types of flake location

Some of the types of flake location supported by Nix include:

Directories, as in:

`nix build ./your-local-nix-guide-checkout`

URLs to git repositories e.g.

`git+https://gitlab.com/tonyfinn/nix-guide`.

You can add various parameters for git here as query parameters, e.g.

`git+https://gitlab.com/tonyfinn/nix-guide?ref=f9a13ed1dc0ed506932e215355a850bfd443691d`

or

`git+https://gitlab.com/tonyfinn/nix-guide?rev=main`

Shorthands for various hosting providers (e.g. `gitlab:tonyfinn/nix-guide`, `github:tonyfinn/nix-guide`). You can add an extra path component here to identify a specific git commit such as:

`gitlab:tonyfinn/nix-guide/f9a13ed1dc0ed506932e215355a850bfd443691d`

or

`gitlab:tonyfinn/nix-guide/main`

Finally, if the flake you want is in a subdirectory of the repository, with _any_ of the above types, you can add the `dir=xyz` parameter, as was done in the example above.

The default value if unspecified is `.`, for the current directory.
## `flake.nix`

```nix
{
  inputs.nixpkgs.url = "github:NixOS/nixpkgs/nixos-22.05";

  outputs = {
    self,
    nixpkgs,
  }: let
    system = "x86_64-linux";
    pkgs = import nixpkgs {inherit system;};
  in {
    # The default package is the same as before
    packages.${system} = {
      default = pkgs.stdenv.mkDerivation {
        src = ./rust-hello;
        name = "rust-hello-1.0";
        inherit system;
        nativeBuildInputs = [pkgs.cargo];
        buildPhase = ''
          cargo build --release
        '';
        installPhase = ''
          mkdir -p $out/bin
          cp target/release/rust-hello $out/bin/rust-hello
          chmod +x $out
        '';
      };
      # Now there's a new package
      debug = pkgs.stdenv.mkDerivation {
        src = ./rust-hello;
        name = "rust-hello-debug-1.0";
        inherit system;
        nativeBuildInputs = [pkgs.cargo];
        buildPhase = ''
          cargo build
        '';
        installPhase = ''
          mkdir -p $out/bin
          cp target/debug/rust-hello $out/bin/rust-hello
          chmod +x $out
        '';
      };
    };
  };
}
```

As before, it's stillpossible to build the release package with a `nix build`. The newly added debug package can be built with `nix build .#debug`. This is using a flake location of `.` (i.e. the flake in the current directory), and a flake output of `debug`. This will look for an output of the right type for the current command and the current system, with the name `debug` and use that. 

Since `nix build` is looking for packages to build, and I'm running this on a `x86_64-linux` system, it will find `packages.x86_64-linux.debug` and use this. If you wanted to be explicit you could write out `nix build .#packages.x86_64-linux.debug`, but that's a lot to type so Nix accepts the short version.

As before, this flake output can be combined with an external flake location, so if you wanted to build [my copy](https://gitlab.com/tonyfinn/nix-guide/-/tree/main/7-flakes/multiple-outputs) of the debug package, you could run the following command:

```sh
nix build git+https://gitlab.com/tonyfinn/nix-guide?dir=7-flakes/multiple-outputs#debug
```

And that's the end of this introduction to the basics of flakes. The [next article](https://tonyfinn.com/blog/nix-from-first-principles-flake-edition/nix-8-flakes-and-developer-environments/) will cover other types of outputs that you can put into flakes.
# Flakes and Developer Environments

