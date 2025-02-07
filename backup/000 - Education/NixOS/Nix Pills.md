#nix #nixos #linux #learnnix
# Preface

This is a ported version of the **Nix Pills**, a series of blog posts written by **Luca Bruno** (aka Lethalman) and originally published in 2014 and 2015. It provides a tutorial introduction into the Nix package manager and Nixpkgs package collection, in the form of short chapters called 'pills'.

Since the Nix Pills are considered a classic introduction to Nix, an effort to port them to the current format was led by Graham Christensen (aka grahamc / gchristensen) and other contributors in 2017.

For an up-to-date version, please visit [https://nixos.org/guides/nix-pills/](https://nixos.org/guides/nix-pills/). An [EPUB version](https://nixos.org/guides/nix-pills/nix-pills.epub) is also available.

If you encounter problems, please report them on the [nixos/nix-pills](https://github.com/NixOS/nix-pills/issues) issue tracker.
# Why You Should Give it a Try
## Introduction

 Nix is a purely functional package manager and deployment system for POSIX. 

There's a lot of documentation that describes what Nix is, [NixOS](https://nixos.org/nixos) and related projects are. But the purpose of this post is to convince you to give Nix a try. Installing NixOS is not required, but sometimes i may refer to NixOS as a real world example of Nix usage for building a whole operating system.
## Rationale for This Series

The [Nix](https://nixos.org/manual/nix), [Nixpkgs](https://nixos.org/manual/nixpkgs/), and [NixOS](https://nixos.org/manual/nixos/) manuals along with [the wiki](https://wiki.nixos.org/) are excellent resources for explaining how Nix/NixOS works, how you can use it, and how cool things are being done with it. However, at the beginning you may feel that some of the magic which happens behind the scenes is hard to grasp.

This series aims to complement the existing explanations from the more formal documents. The following is a description of Nix. Just as with Pills, it will attempt to be as short as possible.
## Not Being Purely Functional

Most, if not all, widely used package managers ([dpkg](https://wiki.debian.org/dpkg), [rpm](http://www.rpm.org/), ...) mutate the global state of the system. If a package `foo-1.0` installs a program to `/usr/bin/foo`, you cannot install `foo-1.1` as well, unless you change the installation paths or the binary name. But changing the binary names means breaking users of that binary.

There are some attempts to mitigate this problem. Debian, for example, partially solves this problem with the [alternatives](https://wiki.debian.org/DebianAlternatives) system.

So while in theory it's possible with some current systems to install multiple versions of the same package, in practice it's very painful. 

Let's say you need an nginx service and also an nginx-openresty service. You have to create a new package that changes all the paths to have, for example, and `-openresty` suffix.

Or suppose that you want to run two different instances of mysql: 5.2 and 5.5. The same thing applies, plus you have to also make sure the two mysqlclient libraries do not collide.

This is not impossible but it *is* very inconvenient. If you want to install two whole stacks of software like GNOME 3.10 and GNOME 3.12, you can imagine the amount of work.

From an administrator's point of view: you can use containers. The typical solution nowadays is to create a container per service, especially when different versions are needed. That somewhat solves the problem, but at a different level and with other drawbacks. For example, needing orchestration tools, setting up a shared cache of packages, and new machines to monitor rather than simple services.

From a developer's point of view: you can use virtualenv for Python, or jhbuild for gnome, or whatever else. But then how do you mix the two stacks? How do you avoid recompiling the same thing when it could instead be shared? Also you need to set up your development tools to point to the different directories where libraries are installed. Not only that, there's the risk that some of the software incorrectly uses system libraries.

And so on. Nix solves all this at the packaging level and solves it well. A single tool to rule them all. 
## Being Purely Functional

Nix makes no assumptions about the global state of the system. This has many advantages, but also some drawbacks of course. The core of a Nix system is the Nix store, usually installed under `/nix/store`, and some tools to manipulate the store. In Nix there is the notion of a *derivation* rather than a package. The difference can be subtle at the beginning, so I will often use the words interchangeably. 

Derivations/packages are stored in the Nix store as follows: `/nix/store/<hash-name>`, where the hash uniquely identifies the derivation (this isn't quite true, it's a little more complex), and the name is the name of the derivation.

Let's take a bash derivation as an example: `/nix/store/s4zia7hhqkin1di0f187b79sa2srhv6k-bash-4.2-p45/`. This is a directory in the Nix store which contains `bin/bash`.

What that means is that there's no `/bin/bash`, there's only that self-contained build output in the store. The same goes for coreutils and everything else. To make them convenient to use from the shell, Nix will arrange for binaries to appear in your `PATH` as appropriate.

What we have is basically a store of all packages (with different versions occupying different locations), and everything in the Nix store is immutable.

In fact, there's no ldconfig cache either. So where does bash find libc?

```
$ ldd which bash
libc.so.6 => /nix/store/94n64qy99ja0vgbkf675nyk39g9b978n-glibc-2.19/lib/libc.so.6 (0x00007f0248cce000)
```

It turns out that when bash was built, it was built against that specific version of glibc in the Nix store, and at runtime it will require exactly that glibc version.

Don't be confused by the version in the derivation name: it's only a name for us humans. You may end up having two derivations with the same name but different hashes: it's the hash that really matters.

What does this all mean? It means that you could run mysql 5.2 with glibc-2.18, and mysql 5.5 with glibc-2.19. You could use your Python module with Python 2.7 compiled with gcc 4.6 and the same Python module with Python 3 compiled with gcc 4.8, all in the same system.

In other words: no dependency hell, not even a dependency resolution algorithm. Straight dependencies from derivations to other derivations.

From an administrator's point of view: if you want an old PHP version for one application, but want to upgrade the rest of the system, that's not painful anymore.

From a developer's point of view: if you want to develop webkit with llvm 3.4 and 3.3, that's not painful anymore.
## Mutable vs. Immutable

When upgrading a library, most package managers replace it in-place. All new applications run afterwards with the new library without being recompiled. After all, they all refer dynamically to `libc6.so`.

Since Nix derivations are immutable, upgrading a library like glibc means recompiling all applications, because the glibc path to the Nix store has been hardcoded.

So how do we deal with security updates? In Nix we have some tricks (still pure) to solve this problem, but that's another story.

Another problem is that unless software has in mind a pure functional model, or can be adapted to it, it can be hard to compose applications at runtime.

Let's take Firefox for example. On most systems, you install flash, and it starts working in Firefox because Firefox looks in a global path for plugins. 

In Nix, there's no such global path for plugins. Firefox therefore must know explicitly about the path to flash. The way we handle this problem is to wrap the Firefox binary so that we can setup the necessary environment to make it find flash in the Nix store. That will produce a new Firefox derivation: be aware that it takes a few seconds, and it makes composition harder at runtime.

There are no upgrade/downgrade scripts for your data. It doesn't make sense with this approach, because there's no real derivation to be upgraded. With Nix you switch to using other software with its own stack of dependencies, but there's no formal notion of upgrade or downgrade when doing so. 

If there is a data format change, then migrating to the new data format remains your own responsibility.
## Conclusion

Nix lets you compose software at build time with **maximum flexibility**, and with builds being as reproducible as possible. Not only that, due to its nature deploying systems in the cloud is so easy, consistent, and reliable that in the Nix world all existing self-containment and orchestration tools are deprecated by [NixOps](http://nixos.org/nixops/).

It however *currently* falls short when working with dynamic composition at runtime or replacing low level libraries, due to the need to rebuild dependencies.

That may sound scary, however after running NixOS on both a server and a laptop/desktop, I'm very satisfied so far. Some of the architectural problems just need some man-power, other design problems still need to be solved as a community.

Considering [Nixpkgs](https://nixos.org/nixpkgs/) ([github link](https://github.com/NixOS/nixpkgs)) is a completely new repository of all the existing software, with a completely fresh concept, and with few core developers but overall year-over-year increasing contributions, the current state is more than acceptable and beyond the experimental stage. In other words, it's worth your investment.
## [Next pill...](https://nixos.org/guides/nix-pills/01-why-you-should-give-it-a-try#next-pill)

...we will install Nix on top of your current system (I assume GNU/Linux, but we also have OSX users) and start inspecting the installed software.
# Enter the Environment

Welcome to the third Nix pill. In the [second pill](https://nixos.org/guides/nix-pills/02-install-on-your-running-system) we installed Nix on our running system. Now we can finally play with it a little, these things also apply to NixOS users.
## Install Something

Finally something practical! Installation into the Nix environment is an interesting process. Let's install `hello`, a simple CLI tool which prints `Hello world` and is mainly used to test compilers and package installations.

Back to the installation:

```
nix-env -i hello
installing 'hello-2.10'
[...]
building '/nix/store/0vqw0ssmh6y5zj48yg34gc6macr883xk-user-environment.drv'...
created 36 symlinks in user environment
```

Now you can run `hello`. Things to notice:

- We installed software as a user, and only for the Nix user.
- It created a new user environment. That's a new generation of our Nix user profile.
- The [nix-env](https://nix.dev/manual/nix/stable/command-ref/nix-env) tool manages environments, profiles and their generations.
- We installed `hello` by derivation name minus the version. I repeat: we specified the **derivation name** (minus the version) to install it.

We can list generations without walking through the `/nix` hierarchy:

```console
nix-env --list-generations
    1   2014-07-24 09:23:30
    2   2014-07-25 08:45:01   (current)
```

Listing installed derivations:

```
nix-env -q 
nix-2.1.3
hello-2.10
```

So, where did `hello` really get installed? `which hello` is `~/.nix-profile/bin/hello` which points to the store. We can also list the derivation paths with `nix-env -q --out-path`. So that's what those derivation paths are called: the **output** of a build.
## Path Merging

At this point you probably want to run `man` to get some documentation. Even if you already have man system-wide outside of the Nix environment, you can install and use it within Nix with `nix-env -i man-db`. As usual, a new generation will be created, and `~/.nix-profile` will point to it.

Let's inspect the [profile](https://nix.dev/manual/nix/stable/package-management/profiles) a bit:

```console
ls -l ~/.nix-profile/
dr-xr-xr-x 2 nix nix 4096 Jan  1  1970 bin
lrwxrwxrwx 1 nix nix   55 Jan  1  1970 etc -> /nix/store/ig31y9gfpp8pf3szdd7d4sf29zr7igbr-nix-2.1.3/etc
[...]
```

Now that's interesting. When only `nix-2.1.3` was installed, `bin` was a symlink to `nix-2.1.3`. Now that we've actually installed some things (`man`, `hello`), it's a real directory, not a symlink.

```console
ls -l ~/.nix-profile/bin/
[...]
man -> /nix/store/83cn9ing5sc6644h50dqzzfxcs07r2jn-man-1.6g/bin/man
[...]
nix-env -> /nix/store/ig31y9gfpp8pf3szdd7d4sf29zr7igbr-nix-2.1.3/bin/nix-env
[...]
hello -> /nix/store/58r35bqb4f3lxbnbabq718svq9i2pda3-hello-2.10/bin/hello
[...]
```

Okay, that's clearer now. `nix-env` merged the paths from the installed derivations. `which man` points to the Nix profile, rather than the system `man`, because `~/.nix-profile/bin` is at the head of `$PATH`.
## Rolling Back and Switching Generation

The last command installed `man`. We should be at generation 3, unless you changed something in the middle. Let's say we want to roll back to the old generation:

```
nix-env --rollback
switching from generation 3 to 2
```

Now `nix-env -q` does not list `man` anymore. `ls -l 'which man'` should now be the system copy.

Enough with the rollback, let's go back to the most recent generation:

```
nix-env -G 3
switching from generation 2 to 3
```

I invite you to read the manpage of `nix-env`. `nix-env` requires an operation to perform, there are common options for all operations, as well as options specific to each operation.

You can of course also [uninstall](https://nix.dev/manual/nix/stable/command-ref/nix-env/uninstall) and [upgrade](https://nix.dev/manual/nix/stable/command-ref/nix-env/upgrade) packages.
## Querying the Store

So far we learned how to query and manipulate the environment. But all of the environment components point to the store.

To query and manipulate the store, there's the `nix-store` command. We can do some interesting things, but we'll only see some queries for now. 

To show the direct runtime dependencies of `hello`: 

```console
nix-store -q --references `which hello`
/nix/store/fg4yq8i8wd08xg3fy58l6q73cjy8hjr2-glibc-2.27
/nix/store/58r35bqb4f3lxbnbabq718svq9i2pda3-hello-2.10
```

The argument to `nix-store` can be anything as long as it points to the Nix store. It will follow symlinks.

It may not make sense to you right now, but let's print reverse dependencies of `hello`:

```console
nix-store -q --referrers `which hello`
/nix/store/58r35bqb4f3lxbnbabq718svq9i2pda3-hello-2.10
/nix/store/fhvy2550cpmjgcjcx5rzz328i0kfv3z3-env-manifest.nix
/nix/store/yzdk0xvr0b8dcwhi2nns6d75k2ha5208-env-manifest.nix
/nix/store/mp987abm20c70pl8p31ljw1r5by4xwfw-user-environment
/nix/store/ppr3qbq7fk2m2pa49i2z3i32cvfhsv7p-user-environment
```

Was it what you expected? It turns out that our environments depend upon `hello`. Yes, that means that the environments are in the store, and since they contain symlinks to `hello`, therefore the environment depends upon `hello`.

Two environments were listed, generation 2 and generation 3, since these are the ones that had `hello` installed in them.

The `manifest.nix` file contains metadata about the environment, such as which derivations are installed. So that `nix-env` can list, upgrade or remove them. And yet again, the current `manifest.nix` can be found at `~/,nix-profile/manifest.nix`.
## Closures

The closures of a derivation is a list of all its dependencies, recursively, including absolutely everything necessary to use that derivation.

```
nix-store -qR 'which man'
[...]
```

Copying all those derivations to the Nix store of another machine makes you able to run `man` out of the box on that other machine. That's the base of deployment using Nix, and you can already foresee the potential when deploying software in the cloud (hint: `nix-copy-closures` and `nix-store --export`).

A nicer view of this closure:

```
nix-store -q --tree 'which man'
[...]
```

With the above command, you can find out exactly why a *runtime* dependency, be it direct or indirect, exists for a given derivation.

The same applies to environments. As an exercise, run `nix-store -q --tree ~/.nix-profile`, and see that the first children are direct dependencies of the user environment: the installed derivations, and the `manifest.nix`.
## Dependency Resolution

There isn't anything like `apt` which solves a SAT problem in order to satisfy dependencies with lower and upper bounds on versions. There's no need for this because all the dependencies are static: if a derivation X depends on a derivation Y, then it always depends on it. A version of X which depended on Z would be a different derivation.
## Recovering the Hard Way

```console
nix-env -e '*'
uninstalling 'hello-2.10'
uninstalling 'nix-2.1.3'
[...]
```

Oops, that uninstalled all derivations from the environment, including Nix. That means we can't even run `nix-env`, what now?

Previously we got `nix-env` from the environment. Environments are a convenience for the user, but Nix is still there in the store!

First, pick one `nix-2.1.3` derivation: `ls /nix/store/*nix-2.1.3`, say `/nix/store/ig31y9gfpp8pf3szdd7d4sf29zr7igbr-nix-2.1.3`.

The first option is to rollback:

```console
/nix/store/ig31y9gfpp8pf3szdd7d4sf29zr7igbr-nix-2.1.3/bin/nix-env --rollback
```

The second option is to install Nix, thus creating a new generation:

```console
/nix/store/ig31y9gfpp8pf3szdd7d4sf29zr7igbr-nix-2.1.3/bin/nix-env -i /nix/store/ig31y9gfp
```
## Channels

So where are we getting packages from? We said something about this already in the [second article](https://nixos.org/guides/nix-pills/02-install-on-your-running-system). There's a list of channels from which we get packages, although usually we use a single channel. The tool to manage channels is [nix-channel](https://nix.dev/manual/nix/stable/command-ref/nix-channel).

```console
nix-channel --list
nixpkgs http://nixos.org/channels/nixpkgs-unstable
```

If you're using NixOS, you may not see any output from the above command (if you're using the default), or you may see a channel whose name begins with "nixos-" instead of "nixpkgs".

That's essentially the contents of `~/.nix-channels`.

> [!NOTE]
> Note: `~/.nix-channels` is not a symlink to the nix store!

To update the channel run `nix-channel --update`. That will download the new Nix expressions (descriptions of the packages), create a new generation of the channels profile and unpack it under `~/.nix-defexpr/channels`.

This is quite similar to `apt-get update`. (See [this table](https://wiki.nixos.org/wiki/Cheatsheet) for a rough mapping between Ubuntu and NixOS package management.)
## Conclusion

We learned how to query the user environment and to manipulate it by installing and uninstalling software. Upgrading software is also straightforward, as you can read in [the manual](https://nix.dev/manual/nix/stable/command-ref/nix-env/upgrade) (`nix-env -u` will upgrade all packages in the environment).

Every time we change the environment, a new generation is created. Switching between generations is easy and immediate.

Then we learned how to query the store. We inspected the dependencies and reverse dependencies of store paths.

We saw how symlinks are used to compose paths from the Nix store, a useful trick.

A quick analogy with programming languages: you have the heap with all the objects, that corresponds to the Nix store. You have objects that point to other objects, those correspond to derivations. This is a suggestive metaphor, but will it be the right path?
## [Next pill](https://nixos.org/guides/nix-pills/03-enter-environment#next-pill)

...we will learn the basics of the Nix language. The Nix language is used to describe how to build derivations, and it's the basis for everything else, including NixOS. Therefore it's very important to understand both the syntax and the semantics of the language.
# The Basics of the Language

Welcome to the fourth Nix pill. In the [previous article](https://nixos.org/guides/nix-pills/03-enter-environment) we learned about Nix environments. We installed software as a user, managed their profile, switched between generations, and queried the Nix store. Those are the very basics of system administration in Nix. 

The [Nix language](https://nix.dev/manual/nix/stable/language/) is used to write expressions that produce derivations. The [nix-build](https://nix.dev/manual/nix/stable/command-ref/nix-build) tool is used to build derivations from an expression. Even as a system administrator that wants to customize the installation, it's necessary to master Nix. Using Nix for your jobs means you get the features we saw in the previous articles for free.

The syntax of Nix is quite unfamiliar, so looking at existing examples may lead you to think that there's a lot of magic happening. In reality, it's mostly about writing utility functions to make things convenient. 

On the other hand, the same syntax is great for describing packages, so learning the language itself will pay off when writing package expressions.

> [!Important] 
> In Nix, everything is an expression, there are no statements. This is common in functional languages.
> 
> Values in Nix are immutable.
## Value Types

Nix 2.0 contains a command named `nix repl` which is a simple command line tool for playing with the Nix language. In fact, Nix is a [pure, lazy, functional language](https://nix.dev/manual/nix/stable/language/), not only a set of tools to manage derivations. The `nix repl` syntax is slightly different to Nix syntax when it comes to assigning variables, but it shouldn't be confusing so long as you bear it in mind. I prefer to start with `nix repl` before cluttering your mind with more complex expressions.

Launch `nix repl`. First of all, Nix supports basic arithmetic operations: `+`, `-`, `*`,  and `/`. (To exit `nix repl`, use the command `:q`. Help is available through the `:?` command.)

```
nix-repl> 1+3
4

nix-repl> 7-4
3

nix-repl> 3*2
6
```

Attempting to perform division in Nix can lead to some surprises.

```
nix-repl> 6/3
/home/nix/6/3
```

What happened? Recall that Nix is not a general purpose language, it's a domain-specific language for writing packages. Integer division isn't actually that useful when writing package expressions. Nix parsed `6/3` as a relative path to the current directory. To get NIx to perform division instead, leave a space after the `/`. Alternatively, you can use `builtins.div`.

```
nix-repl> 6/3
2

nix-repl> builtins.div 6 3
2
```

Other operators are `||`, `&&`, and `!` for booleans, and relational operators such as `!=`, `==`, `<`, `>`, `<=`, `>=`. In Nix, `<`, `>`, `<=` and `>=` are not much used. There are also other operators we will see in the course of this series.

Nix has integer, floating point, string, path, boolean and null [simple](https://nix.dev/manual/nix/stable/language/#overview) types. Then there are also lists, sets and functions. These types are enough to build an operating system.

Nix is strongly typed, but it's not statically typed. That is, you cannot mix strings and integers, you must first do the conversion.

As demonstrated above, expressions will be parsed as paths as long as there's a slash not followed by a space. Therefore to specify the current directory, use `./.` In addition, Nix also parses urls specifically. 

Not all urls or paths can be parsed this way. If a syntax error occurs, it's still possible to fallback to plain strings. Literal urls and paths are convenient for additional safety.
## Identifier

There's not much to say here, except that dash (`-`) is allowed by identifiers. That's convenient since many packages use dash in their names. In fact:

```console
nix-repl> a-b
error: undefined variable `a-b' at (string):1:1

nix-repl> a - b
error: undefined variable `a' at (string):1:1
```

As you can see, `a-b` is parsed as identifier, not as a subtraction.
## Strings

It's important to understand the syntax for strings. When learning to read Nix expressions, you may find dollars (`$`) ambiguous, but they are very important. Strings are enclosed by double quotes (`"`), or two single quotes (`''`).

```
nix-repl> "foo"
"foo"
nix-repl> ''foo''
"foo"
```

In other languages like Python you can also use single quotes for strings (e.g. `foo`), but not in Nix. 

It's possible to [interpolate](https://nix.dev/manual/nix/stable/language/string-interpolation) whole Nix expressions inside strings with the `${...}` syntax and only that syntax, not `$foo` or `${foo}` or anything else.

```json
nix-repl> foo = "strval"
nix-repl> "$foo"
"$foo"
nix=repl> "${foo}"
"strval"
nix-repl> "${2+3}"
error: cannot coerce an integer to a string, at (string):1:2
```

**Note**: ignore the `foo = "strval"` assignment, special syntax in `nix repl`.

As said previously, you cannot *mix integers and strings*. You need to explicitly include conversations. We'll see this later: function calls are another story.

Using the syntax with two single quotes is useful for writing double quotes inside strings without needing to escape them:

```json
nix-repl> ''test " test''
"test \" test"
nix-repl> ''${foo}''
"strval"
```

Escaping `${...}` within double quoted strings is done with the backlash. Within two single quotes, it's done with `''`:

```json
nix-repl> "\${foo}"
"${foo}"
nix-repl> ''test ''${foo} test''
"test ${foo} test"
```
## Lists

Lists are a sequence of expressions delimited by space (*not* comma):

```
nix-repl> [2 "foo" true (2+3) ]
[ 2 "foo" true 5 ]
```

Lists, like everything else in Nix, are immutable. Adding or removing elements from a list is possible, but will return a new list.
## Attribute Sets

An attribute set is an association between string keys and Nix values. Keys can only be strings. When writing attribute sets you can also use unquoted identifiers as keys.

```json
nix-repl> s = { foo = "bar"; a-b = "baz"; "123" = "num"; }
nix-repl> s
{ "123" = "num"; a-b "baz"; foo = "bar"; }
```

For those reading Nix expressions from nixpkgs: do not confuse attribute sets with argument sets used in functions.

To access elements in the attribute set:

```json
nix-repl> s.a-b
"baz"
nix-repl> s."123"
"num"
```

Yes, you can use strings to address keys which aren't valid identifiers.

Inside an attribute set you cannot normally refer to elements of the same attribute set:

```json
nix-repl> { a = 3; b = a+4; }
error: undefined variable a' at (string):1:10
```

To do so, use [recursive attribute sets](https://nix.dev/manual/nix/stable/language/constructs#recursive-sets):

```json
nix-repl> rec { a = 3; b = a+4; }
{ a = 3; b = 7; }
```

This is very convenient when defining packages, which tend to be recursive attribute sets.
## If Expressions

These are expressions, not statements.

```json
nix-repl> a = 3
nix-repl> b = 4
nix-repl> if a > b then "yes" else "no"
"no"
```

You can't have only the `then` branch, you must specify also the `else` branch, because an expression *must have a value in all cases*.
## Let Expressions

This kind of expression is used to define local variables for inner expressions.

```json
nix-repl> let a = "foo"; in a
"foo"
```

The syntax is: first assign variables, then `in`, then an expression which can use the defined variables. The value of the whole `let` expression will be the value of the expression after the `in`.

```json
nix-repl> let a = 3; b = 4; in a + b
7
```

Let's write two `let` expressions, one inside the other:

```json
nix-repl> let a = 3; in let b = 4; in a + b
7
```

With `let` you cannot assign twice to the same variable. However, you can shadow outer variables:

```json
nix-repl> let a = 3; a = 8; in a
error: attribute a' at (string):1:12 already defined at (string):1:5
nix-repl> let a = 3; in let a = 8; in a
8
```

You cannot refer to variables in a `let` expression outside of it:

```json
nix-repl> let a = (let c = 3; in c); in c
error: undefined variable 'c' at (string):1:31
```

You can refer to variable sin the `let` expression when assigning variables, like with recursive attribute sets:

```json
nix-repl> let a = 4; b = a + 5; in b
9
```

So beware when you want to refer to a variable from the outer scope, but it's also defined in the current let expression. The same applies to recursive attribute sets.
## With Expression

This kind of expression is something you rarely see in other languages. You can think of it like a more granular version of `using` from C++, or `from module import *` from Python. You decide per-expression when to include symbols into the scope.

```json
nix-repl> longName = { a = 3; b = 4; }
nix-repl> longName.a + longName.b
7
nix-repl> with longName; a + b
7
```

That's it, it takes an attribute set and includes symbols from it in the scope of the inner expression. Of course, only valid identifiers from the keys of the set will be included. If a symbol exists in the outer scope and would also be introduced by the `with`, it will *not* be shadowed. You can however still refer to the attribute set:

```json
nix-repl> let a = 10; in with longName; a + b
14
nix-repl> let a = 10; in with longName; longName.a + b
```
## Laziness

 Nix evaluates expressions only when needed. This is a great feature when working with packages.

```json
nix-repl> let a = builtins.div 4 0; b = 6; in b
6
```

Since `a` is not needed, there's no error about division by zero, because the expression is not in need to be evaluated. That's why we can have all the packages defined on demand, yet have access to specific packages very quickly.
## [Next pill](https://nixos.org/guides/nix-pills/04-basics-of-language#next-pill)

...we will talk about functions and imports. In this pill I've tried to avoid function calls as much as possible, otherwise the post would have been too long.
# Functions and Imports

Welcome to the fifth Nix pill. In the previous [fourth pill](https://nixos.org/guides/nix-pills/04-basics-of-language) we touched the Nix language for a moment. We introduced basic types and values of the Nix language, and basic expressions such as `if`, `with` and `let`. I invite you to re-read about these expressions and play with them in the repl.

Functions help to build reusable components in a big repository like [nixpkgs](https://github.com/NixOS/nixpkgs/). The Nix manual has [great explanation of functions](https://nix.dev/manual/nix/stable/language/constructs#functions). Let's go: pill on one hand, Nix manual on the other hand. 

I remind you how to enter the Nix environment: `source ~/.nix-profile/etc/profile.d/nix.sh`
## Nameless and Single Parameter

Functions are anonymous (lambdas), and only have a single parameter. The syntax is extremely simple. Type the parameter name, then "`:`", then the body of the function.

```
nix-repl> x: x*2
<lambda>
```

So here we defined a function that makes a parameter `x`, and returns `x*2`. The problem is that we cannot use it in any way, because it's unnamed... joke!~

We can store functions in variables. 

```
nix-repl> double = x: x*2
nix-repl> double
«lambda»
nix-repl> double 3
```

As usual, please ignore the special syntax for assignments inside `nix-repl`. So, we defined a function `x: x*2` that takes one parameter `x`, and returns `x*2`. This function is then assigned to the variable `double`. Finally we did our first function call: `double 3`.

Big note: it's not like many other programming languages where you write `double(3)`. It really is `double 3`.

In summary: to call a function, name the variable, then space, then the argument. Nothing else to say, it's as easy as that. 
## More than One Parameter

How do we create a function that accepts more than one parameter? For people not used to functional programming, this may take a while to grasp. Let's do it step by step. 

```
nix-repl> mul = a: (b: a*b)
nix-repl> mul
«lambda»
nix-repl> mul 3
«lambda»
nix-repl> (mul 3) 4
12
```

We defined a function that takes the parameter `a`, the body returns another function. This other function takes a parameter `b` and returns `a*b`. Therefore, calling `mul 3` returns this kind of function: `b: 3*b`. In turn, we call the returned function with `4`, and get the expected result.

You don't have to use parentheses at all, Nix has sane priorities when parsing the code:

```
nix-repl> mul = a: a*b
nix-repl> mul
«lambda»
nix-repl> mul 3
«lambda»
nix-repl> mul 3 4
12
nix-repl> mul (6+7) (8+9)
221
```

Much more readable, you don't even notice that functions only receive one argument. Since the argument is separated by a space, to pass more complex expressions you need parenthesis. In other common languages you would write `mul(6+7, 8+9)`.

Given that functions have only one parameter, it is straighforward to use **partial application.**

```

```




