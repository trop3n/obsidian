#nixos #Nix #nixlang 
# First Steps

This tutorial series is where you should start learning Nix.

In these lessons, you will use basic Nix commands to obtain almost any piece of software, create development environments on the fly, and learn how to make reproducible scripts. You will also learn reading the Nix language, and later use it to build portable, reproducible development environments.

- [Ad hoc shell environments](https://nix.dev/tutorials/first-steps/ad-hoc-shell-environments)
- [Reproducible interpreted scripts](https://nix.dev/tutorials/first-steps/reproducible-scripts)
- [Declarative shell environments](https://nix.dev/tutorials/first-steps/declarative-shell)
- [Towards reproducibility: pinning Nixpkgs](https://nix.dev/tutorials/first-steps/towards-reproducibility-pinning-nixpkgs)
# Ad hoc Shell Environments

In a Nix shell environment, you can immediately use any program packaged with Nix, without installing it permanently. 

You can also share the command invoking such a shell with others, and it will work on all Linux distributions, WSL, and macOS.
## Create a Shell Environment

Once you install Nix, you can use it to create a new *shell environment* with programs that you want to use. 

In this section you will run two exotic programs called `cowsay` and `lolcat` that you will probably not have installed on your machine:

```bash
$ cowsay no can do
The program 'cowsay' is currently not installed.

$ echo no chance | lolcat
The program 'lolcat' is currently not installed.
```

Use `nix-shell` with the `-p` (`--packages`) option to specify that we need the `cowsay` and `lolcat` packages: 

> [!NOTE]
> The first invocation of `nix-shell` for these packages may take a while to download all dependencies.

```bash
nix-shell -p cowsay lolcat
these 3 derivations will be built:
  /nix/store/zx1j8gchgwzfjn7sr4r8yxb7a0afkjdg-builder.pl.drv
  /nix/store/h9sbaa2k8ivnihw2czhl5b58k0f7fsfh-lolcat-100.0.1.drv
  ...
```

Within the Nix shell, you can use the programs provided by these packages:

```bash
[nix-shell:~]$ cowsay Hello, Nix! | lolcat
```

Type `exit` or press `CTRL-D` to exit the shell, and the programs won't be available anymore.

```bash
[nix-shell:~]$ exit
exit

cowsay no more
The program ‘cowsay’ is currently not installed.

echo all gone | lolcat
The program ‘lolcat’ is currently not installed.
```
## Running Programs Once

You can go even faster, by running any program directly:

```bash
nix-shell -p cowsay --run "cowsay Nix"
```

If the command consists only of the program name, no quotes are needed:

```bash
nix-shell -p hello --run hello
```
## Search for Packages

What can you put in a shell environment? If you can think of it, there's probably a Nix package of it.

> [!TIP]
> Enter the program name you want to run in [search.nixos.org](https://search.nixos.org/packages) to find packages that provide it.

For the following example, find the package names for these programs:

- `git`
- `nvim`
- `npm`

In the search results, each item shows the package name, and the details list the available programs.
## Run Any Combination of Programs

Once you have installed the package name, you can start a shell with that package. The `-p` (`--packages`) argument can take multiple package names.

Start a nix shell with the packages providing `git`, `nvim`, and `npm`. Again, the first invocation may take while to download all dependencies.

```bash
nix-shell -p git neovim nodejs
these 9 derivations will be built:
  /nix/store/7gz8jyn99kw4k74bgm4qp6z487l5ap06-packdir-start.drv
  /nix/store/d6fkgxc3b04m85wrhg6j0l5y0ray82l7-packdir-opt.drv
  /nix/store/da6njv7r0zzc2n54n2j54g2a5sbi4a5i-manifest.vim.drv
  /nix/store/zs4jb2ybr4rcyzwq0dagg9rlhlc368h6-builder.pl.drv
  /nix/store/g8sl2xnsshfrz9f39ki94k8p15vp3xd7-vim-pack-dir.drv
  /nix/store/jmxkg8b1psk52awsvfziy9nq6dwmxmjp-luajit-2.1.0-2022-10-04-env.drv
  /nix/store/kn83q8yk6ds74zgyklrjhvv5wkv5wmch-python3-3.10.9-env.drv
  /nix/store/m445wn3vizcgg7syna2cdkkws3kk1gq8-neovim-ruby-env.drv
  /nix/store/r2wa882mw99c311a4my7hcis9lq3kp3v-neovim-0.8.1.drv
these 151 paths will be fetched (186.43 MiB download, 1018.20 MiB unpacked):
  /nix/store/046zxlxhq4srm3ggafkymx794bn1jksc-bzip2-1.0.8
  /nix/store/0p1jxcb7b4p8jhhlf8qnjc4cqwy89460-unibilium-2.1.1
  /nix/store/0q4fpnqmg8liqraj7zidylcyd062f6z0-perl5.36.0-URI-5.05
  ...
```
## Check Package Versions

Check that you have indeed the specific version of these programs provided by Nix, even if you had any of them installed on your machine.

```bash
which git
/nix/store/3cdi52xh6lk3h1fb51jkxs3p561p37wg-git-2.38.3/bin/git

git --version
git version 2.38.3

which nvim
/nix/store/ynskzgkf07lmrrs3cl2kzr9ah487lwab-neovim-0.8.1/bin/nvim

nvim --version | head -1
NVIM v0.8.1

which npm
/nix/store/q12w83z0i5pi1y0m6am7qmw1r73228sh-nodejs-18.12.1/bin/npm

npm --version
8.19.2
```
## Nested Shell Sessions

If you need an additional program temporarily, you can run a nested Nix shell. The programs provided by the specified packages will be added to the current environment. 

```bash
nix-shell -p python3
this path will be fetched (11.42 MiB download, 62.64 MiB unpacked):
  /nix/store/pwy30a7siqrkki9r7xd1lksyv9fg4l1r-python3-3.10.11
copying path '/nix/store/pwy30a7siqrkki9r7xd1lksyv9fg4l1r-python3-3.10.11' from 'https://cache.nixos.org'...

python --version
Python 3.10.11
```

Exit the shell as usual to return to the previous environment.
## Towards Reproducability

These shell environments are very convenient, but the examples so far are not reproducible yet. Running these commands on another machine may fetch versions of packages, depending on when Nix was installed there.

What do we mean by reproducible? A fully reproducible example would give exactly the same results no matter when or where you run the command. The environment provided would be *identical each time*.

The following example creates a fully reproducible environment. You can run it anywhere, anytime to obtain the exact same version of the `git`. 

```bash
nix-shell -p git --run "git --version" --pure -I nixpkgs=https://github.com/NixOS/nixpkgs/
...
git version 2.33.1
```

There are there things going on here:

1. `--run` executes the given [Bash command](https://www.gnu.org/software/bash/manual/bash.html#Shell-Commands) within the environment created by Nix, and exits when it's done.
	You can use this with `nix-shell` whenever you want to quickly run a program you don't have installed on your machine.

2. `--pure` discards most environment variables set on your system when running the shell. It means that only the `git` provided by Nix is available inside that shell. This is useful for simple one-liners such as in the example. While developing, however, you will usually want to have your editor and other tools around. Therefore we recommend to omit `--pure` for development environments, and to add it only when the extra isolation is needed.

3. `-I` determines what to use a source of package declarations.
	Here we provided [a specific Git revision of `nixpkgs`](https://github.com/NixOS/nixpkgs/tree/2a601aafdc5605a5133a2ca506a34a3a73377247), leaving no doubt about which version of the packages in that collection will be used.
### References

- [Nix manual: `nix-shell`](https://nix.dev/manual/nix/stable/command-ref/nix-shell) (or run `man nix-shell`)
- [Nix manual: `-I` option](https://nix.dev/manual/nix/stable/command-ref/opt-common.html#opt-I)
### Next Steps

- [Reproducible interpreted scripts](https://nix.dev/tutorials/first-steps/reproducible-scripts#reproducible-scripts) – use Nix for reproducible scripts
- [Nix language basics](https://nix.dev/tutorials/nix-language#reading-nix-language) – learn reading the Nix language, which is used to declare packages and configurations
- [Declarative shell environments with shell.nix](https://nix.dev/tutorials/first-steps/declarative-shell#declarative-reproducible-envs) – create reproducible shell environments with a declarative configuration file
- [Towards reproducibility: pinning Nixpkgs](https://nix.dev/tutorials/first-steps/towards-reproducibility-pinning-nixpkgs#pinning-nixpkgs) – learn different ways of specifying exact versions of package sources

If you’re done trying out Nix for now, you may want to free up some disk space occupied by the different versions of programs you downloaded by running the examples:

```
nix-collect-garbage
```
# Reproducible Interpreted Scripts

In this tutorial, you will learn how to use Nix to create and run reproducible scripts, also know as [shebang](https://en.wikipedia.org/wiki/Shebang_(Unix)) scripts.
## Requirements

- A working - [Nix installation](https://nix.dev/install-nix#install-nix)
- Familiarity with [Bash](https://www.gnu.org/software/bash/)
## A Trivial Script with Non-Trivial Dependencies

Take the following script, which fetches the content XML of a URL, converts it to JSON, and formats it for better readability:

```bash
#! /bin/bash

curl https://github.com/NixOS/nixpkgs/releases.atom | xml2json | jq .
```

It requires the programs `curl`, `xml2json`, and `jq`. It also requires the `bash` interpreter. If any of these dependencies are not present on the system when running the script, it will fail partially or altogether.

With Nix, we can declare all dependencies explicitly, and produce a script that will always run on any machine that supports Nix and the required packages taken from Nixpkgs.
## The Script

A [shebang](https://en.wikipedia.org/wiki/Shebang_(Unix)) determines which program to use for running an interpreted script.

---
### Shebang (UNIX)

When a text file with a shebang is used as if it were an executable in a Unix-like environment, the [program loader](https://en.wikipedia.org/wiki/Loader_(computing) "Loader (computing)") mechanism parses the rest of the the file's initial line as an [interpreter directive](https://en.wikipedia.org/wiki/Interpreter_directive). The loader executes the specified interpreter program, passing to it as an argument the path that was initially used when attempting to run the script, so that the program may use the file as input data. For example, if a script named with the path `path/to/script`, and it starts with the line `#!/bin/sh`, then the program loader is instructed to run the program `/bin/sh`, passing `path/to/script` as the first argument.

The shebang line is usually ignored by the interpreter, because the `#` character is a comment marker in many scripting languages; some language interpreters that do not use the hash mark to begin comments still may ignore the shebang line in recognition of its purpose.
#### Program Loader

In computer systems a **loader** is the part of an operating system that is responsible for loading programs and libraries. It is one of the essential stages in the process of starting a program, as it places programs *into memory* and prepares them for execution. Loading a program involves either [memory-mapping](https://en.wikipedia.org/wiki/Memory-mapped_file) or copying the contents of the executable for running. Once the loading is complete, the operating system starts the program by passing control to the loaded program code. 

All operating systems that support program loading have loaders, apart from highly specialized computer systems that only have a fixed set of specialized programs. [Embedded systems](https://en.wikipedia.org/wiki/Embedded_system "Embedded system") typically do not have loaders, and instead, the code executes directly from ROM or similar. In order to load the operating system itself, as part of booting, a specialized boot loader is used. In many operating systems, the loader resides permanently in memory, though some operating systems that support virtual memory may allow the loader to be located in a region of memory that is [pageable](https://en.wikipedia.org/wiki/Paging).

In the case of operating systems that support virtual memory, the loader may not actually copy the contents of executable files into memory, but rather may simply declare to the virtual memory subsystem that there is a mapping between a region of memory allocated to contain the running program's code and the contents of the associated executable file. (See [memory-mapped file](https://en.wikipedia.org/wiki/Memory-mapped_file).) The virtual memory subsystem is then made aware that pages with that region of memory need to be filled on demand if and when program execution actually hits those areas of unfilled memory. This may mean parts of a program's code are not actually copied into memory until they are actually used, and unused code may never be loaded into memory at all.
#### Memory-Mapped File

A **memory-mapped file** is a segment of virtual memory that has been assigned a direct *byte-for-byte* correlation with some portion of a file or file-like resource. This resource is typically a file that is physically present on disk, but can also be a device, shared memory object, or other resource that an operating system can reference through a [file descriptor](https://en.wikipedia.org/wiki/File_descriptor "File descriptor"). Once present, this correlation between the file and the memory space permits applications to treat the mapped portion as if it were primary memory.
#### Interpreter Directive

An **interpreter directive** is a computer language construct, that on some systems is better described as an aspect of the system's executable file format, that is used to control which interpreter parses and interprets the instructions in a computer program. 

In [Unix](https://en.wikipedia.org/wiki/Unix "Unix"), [Linux](https://en.wikipedia.org/wiki/Linux "Linux") and other [Unix-like](https://en.wikipedia.org/wiki/Unix-like "Unix-like") [operating systems](https://en.wikipedia.org/wiki/Operating_system "Operating system"), the first two bytes in a file can be the characters "#!", which constitute a [magic number](https://en.wikipedia.org/wiki/Magic_number_(programming) "Magic number (programming)") ([hexadecimal](https://en.wikipedia.org/wiki/Hexadecimal) 23 and 21, the ASCII values of "#" and "!") often referred to as [shebang](https://en.wikipedia.org/wiki/Shebang_(Unix) "Shebang (Unix)"), prefix the first line in a [script](https://en.wikipedia.org/wiki/Script_(Unix) "Script (Unix)"), with the remainder of the line being a command usually limited to a max of 14 (when introduced) up to usually about 80 characters in 2016[]. If the [file system permissions](https://en.wikipedia.org/wiki/File_system_permissions "File system permissions") on the script (a file) include an [execute](https://en.wikipedia.org/wiki/Execution_(computing) "Execution (computing)") permission bit for the user invoking it by its filename (often found through the command search path), it is used to tell the operating system what interpreter (usually a program that implements a [scripting language](https://en.wikipedia.org/wiki/Scripting_language "Scripting language")) to use to execute the [script](https://en.wikipedia.org/wiki/Shell_script "Shell script")'s contents, which may be [batch commands](https://en.wikipedia.org/wiki/Batch_processing "Batch processing") or might be intended for interactive use. An example would be _#!/bin/bash_, meaning run this script with the [bash shell](https://en.wikipedia.org/wiki/Bash_(Unix_shell) "Bash (Unix shell)") found in the /bin [directory](https://en.wikipedia.org/wiki/Unix_filesystem#Conventional_directory_layout "Unix filesystem").

---

We will use the shebang line `#!/usr/bin/env nix-shell`.

`env` is a program available on most modern Unix-like operating systems at the file system path `/usr/bin/env`. It takes a command name as argument and will run the first executable by that name it finds in the directories listed in the environment variable `$PATH`.

We use [`nix-shell` as a shebang interpreter](https://nix.dev/manual/nix/stable/command-ref/nix-shell.html#use-as-a--interpreter). It takes the following parameters relevant for our use case:

- `-i` tells which program to use for interpreting the rest of the file
- `--pure` excludes most environment variables when the script is run
- `-p` lists packages that should be present in the interpreter's environment
- `-I` explicitly sets [the search path](https://nix.dev/manual/nix/stable/command-ref/opt-common.html#opt-I) for packages.

More details on the options can be found in the [`nix-shell` reference documentation](https://nix.dev/manual/nix/stable/command-ref/nix-shell.html#options).

Create a file named `nixpkgs-releases.sh` with the following content:

```bash
#!/usr/bin/env nix-shell
#! nix-shell -i bash --pure
#! nix-shell -p bash cacert curl jq python3Packages.xmljson
#! nix-shell -I nixpkgs=https://github.com/NixOS/nixpkgs/archive/2a601aafdc5605a5133a2ca506a34a3a73377247.tar.gz

curl https://github.com/NixOS/nixpkgs/releases.atom | xml2json | jq .
```

The first line is a standard shebang. The additional shebang lines are a Nix-specific construct. 

We specify `bash` as the interpreter for the rest of the file with the `-i` option. 

We enable the `--pure` option to prevent the script from implicitly using programs that may already exist on the system that will run the script. 

With the `-p` option we specify the packages required for the script to run. The command `xml2json` is provided by the package `python3Packages.xmljson`, which `bash`, `jq` and `curl` are provided by packages of the same name. `cacert` must be present for SSL authentication to work.

> [!TIP]
> 
> Use [search.nixos.org](https://search.nixos.org/packages) to find packages providing the program you need.

Make the script executable:

```
chmod +x nixpkgs-releases.sh
```

Run the script:

```
./nixpkgs-releases.sh
```

## Next steps

- [Nix language basics](https://nix.dev/tutorials/nix-language#reading-nix-language) to learn about the Nix language, which is used to declare packages and configurations.
- [Declarative shell environments with shell.nix](https://nix.dev/tutorials/first-steps/declarative-shell#declarative-reproducible-envs) to create reproducible shell environments with a declarative configuration file.
- [Garbage Collection](https://nix.dev/manual/nix/stable/package-management/garbage-collection.html) – free up storage used by the programs made available through Nix
# Declarative Shell Environments

## Overview

Declarative Shell Environments allow you to:

- Automatically run bash scripts during environment activation
- Automatically set environment variables
- Put the environment definition under version control and reproduce it on other machines
## What Will We Learn?

In the [Ad hoc shell environments](https://nix.dev/tutorials/first-steps/ad-hoc-shell-environments#ad-hoc-envs) tutorial, we learned how to imperatively create shell environments using `nix-shell -p`. This is great when you want to quickly access tools without installing them permanently. You also learned how to execute that command with a specific Nixpkgs revision using a Git commit as an argument, to recreate the same environment used previously. 

In this tutorial we will take a look at how to create *reproducible shell environments* with a declarative configuration in a [Nix file](https://nix.dev/reference/glossary#term-Nix-file). This file can be shared with anyone to recreate the same environment on a different machine.
### What do you need?

- Familiarity with the Unix shell
- A rudimentary understanding of the [Nix language](https://nix.dev/tutorials/nix-language#reading-nix-language)
## Entering a Temporary Shell

Suppose we want an environment where `cowsay` and `lolcat` are available. The simplest possible way to accomplish this is via the `nix-shell -p` command:

```
nix-shell -p cowsay lolcat
```

This command works, but there's a number of drawbacks:

- You have to type our `-p cowsay lolcat` every time you enter the shell.
- It doesn't (ergonomically) allow you any further customization of your shell environment.

A better solution is to create our shell environment from a `shell.nix` file.
## A Basic `shell.nix` file

Create a file called `shell.nix` with these contents

```haskell
let
  nixpkgs = fetchTarball "https://github.com/NixOS/nixpkgs/tarball/nixos-24.05";
  pkgs = import nixpkgs { config ={}; overlays = []; };
in

pkgs.mkShellNoCC {
  packages = with pkgs; [
    cowsay
    lolcat}
  ];
}
```
## Environment Variables

You may want to automatically export certain environment variables when you enter a shell environment.

Set `GREETING` so it can be used in the shell environment:

```haskell
let
  nixpkgs = fetchTarball "https://github.com/NixOs/nixpkgs/tarball/nixos-24.05";
  pkgs = import nixpkgs { config ={}; overlays = []' };
in

pkgs.mkShellNoCC {
  packages = with pkgs; [
    cowsay
    lolcat
  ];

+ GREETING = "Hello, Nix!";
}
```

Any attribute name passed to `mkShellNoCC` that is not reserved otherwise and has a value which can be coerced to a string will end up as an environment variable.

Try it out! Exit the shell by typing `exit` or pressing `Ctrl + D`, then start it again with `nix-shell`.

> [!Warning]
> Some variables are protected from being set as described above. 
> 
> For example, the shell prompt format for most shells is set by the `PS1` environment variable, but `nix-shell` already sets this by default, and will ignore a `PS1` attribute set in the argument. 
> 
> If you need to override these protected environment variables, use the `shellHook` attribute as described in the next section.
## Startup Commands

You may want to run some commands before entering the shell environment. These commands can be placed in the `shellHook` attribute provided to `mkShellNoCC`.

Set `shellHook` to output a colorful greeting:

```haskell
 let
   nixpkgs = fetchTarball "https://github.com/NixOS/nixpkgs/tarball/nixos-24.05";
   pkgs = import nixpkgs { config = {}; overlays = []; };
 in

 pkgs.mkShellNoCC {
   packages = with pkgs; [
     cowsay
     lolcat
   ];

   GREETING = "Hello, Nix!";
+
+  shellHook = ''
+    echo $GREETING | cowsay | lolcat
+  '';
 }
```

Try it again. Exit the shell, the start it again with `nix-shell` to observe the effect.

## References

- [`mkShell` documentation](https://nixos.org/manual/nixpkgs/stable/#sec-pkgs-mkShell)
- Nixpkgs [shell functions and utilities](https://nixos.org/manual/nixpkgs/stable/#ssec-stdenv-functions) documentation
- [`nix-shell` documentation](https://nix.dev/manual/nix/stable/command-ref/nix-shell)
## Next steps

- [Nix language basics](https://nix.dev/tutorials/nix-language#reading-nix-language)
- [Automatic environment activation with direnv](https://nix.dev/guides/recipes/direnv#automatic-direnv)
- [Dependencies in the development shell](https://nix.dev/guides/recipes/sharing-dependencies)
- [Automatically managing remote sources with npins](https://nix.dev/guides/recipes/dependency-management)
# Towards Reproducibility: Pinning Nixpkgs

In various Nix examples, you'll often see the following:

```haskell
{ pkgs ? import <nixpkgs> {} }:

...
```

> [!NOTE]
> `<nixpkgs>` points to the file system path of some revision of [Nixpkgs](https://nix.dev/reference/glossary#term-Nixpkgs). Find more information on [lookup paths](https://nix.dev/tutorials/nix-language#lookup-path-tutorial) in [Nix language basics](https://nix.dev/tutorials/nix-language#reading-nix-language).

This is a **convenient way** to quickly demonstrate a Nix expression and get it working by importing Nix packages. 

However, the **resulting Nix expression is not fully reproducible**. 
## Pinning Packages with URLs Inside a Nix Expression

To create **fully reproducible** Nix expression, we can pin an exact version of Nixpkgs.

The simplest way to do this is to fetch the required Nixpkgs version as a tarball specified via the relevant Git commit hash:

```haskell
{ pkgs ? import (fetchTarball "https://github.com/NixOS/nixpkgs/archive/06278c77b5d162e62df170fec307e83f1812d94b.tar.gz") {}

}:

...
```

Picking the commit can be done via [status.nixos.org](https://status.nixos.org/), which lists all the releases and the latest commit that has passed all tests.

When choosing a commit, it is recommended to follow either

- The **latest stable NixOS release** by using a specific version, such as `nixos-21.05`, or
- the latest **unstable release** via `nixos-unstable`.
## Next steps

- For more examples and details of the different ways to pin `nixpkgs`, see [Pinning Nixpkgs](https://nix.dev/reference/pinning-nixpkgs#ref-pinning-nixpkgs).
- [Automatically managing remote sources with npins](https://nix.dev/guides/recipes/dependency-management#dependency-management-npins)
# Nix Language Basics

The Nix language is designed for conveniently creating and composing *derivations* -- precise descriptions of how contents of existing files are used to derive new files. It is a domain-specific, purely functional, lazily evaluated, dynamically typed programming language.

> [!NOTE] Notable uses of the Nix Language
> - [Nixpkgs](https://nix.dev/reference/glossary#term-Nixpkgs)
>     
>     The largest, most up-to-date software distribution in the world, and written in the Nix language.
>     
> - [NixOS](https://nix.dev/reference/glossary#term-NixOS)
>     
>     A Linux distribution that can be configured fully declaratively and is based on Nix and Nixpkgs.
>     
>     Its underlying modular configuration system is written in the Nix language, and uses packages from Nixpkgs. The operating system environment and services it provides are configured with the Nix language.

You may quickly encounter Nix language expression that look very complicated. As with any programming language, the required amount of Nix language code matches the complexity of the probelm it is supposed to solve, and reflects how well the problem -- and it's solution -- is understood. Building software is a complex undertaking, and Nix both *exposes* and *allows managing* this complexity with the Nix language.

Yet, the Nix language itself has only a few basic concepts that will be introduced in this tutorial, and which can be combined arbitrarily. What may look complicated comes not from the language, but from how it is used.
## Overview

This is an introduction to **reading the Nix language**, for the purpose of following other tutorials and examples.

**Using the Nix language** in practice entails multiple things:

- Language: syntax and semantics
- Libraries: `builtins` and `pkgs.lib`
- Developer tools: testing, debugging, linting, formatting, ...
- Generic build mechanisms: `stdenv.mkDerivation`, trivial builders, ...
- Composition and configuration mechanisms: `override`, `overrideAttrs`, overlays, `callPackage`...
- Ecosystem-specific packaging mechanisms: `buildGoMobile`, `buildPythonApplication`, ...
- NixOS module system: `config`, `option`, ...

This tutorial only covers the most important language features, briefly discusses libraries, and at the end will direct you to reference material and resources on the other components. 
## What Will You Learn?

This tutorial should enable you to read typical Nix language code and understand it's structure. Its goal is to highlight where the Nix language may differ from languages you are used to. 

It therefore shows the most common and distinguishing patterns in the Nix language:

- [Assigning names and accessing values](https://nix.dev/tutorials/nix-language#names-values)
- Declaring and calling [functions](https://nix.dev/tutorials/nix-language#functions)
- [Built-in and library functions](https://nix.dev/tutorials/nix-language#libraries)
- [Impurities](https://nix.dev/tutorials/nix-language#impurities) to obtain build inputs
- [Derivations](https://nix.dev/tutorials/nix-language#derivations) that describe build tasks

> [!important]
> This tutorial _does not_ explain all Nix language features in detail and _does not_ go into specifics of syntactical rules.
> 
> See the [Nix manual](https://nix.dev/manual/nix/stable/language/index.html) for a full language reference.
## What do you Need?

- Familiarity with software development
- Familiarity with Unix shell, to read command line examples
- A [Nix installation](https://nix.dev/install-nix#install-nix) to run the examples
## How Long Does it Take?

- No experience with functional programming: 2 hours
- Familiar with functional programming: 1 hour
- Proficient with functional programming: 30 minutes

We recommend to run all the examples. Play with them to validate your assumptions and test what you have learned. Read detailed explanations if you want to make sure you fully understand the examples. 
## How to run the Examples?

- A piece of Nix language code is a _Nix expression_.
- Evaluating a Nix expression produces a _Nix value_.
- The content of a _Nix file_ (file extension `.nix`) is a Nix expression.

> [!NOTE]
> To _evaluate_ means to transform an expression into a value according to the language rules.

This tutorial contains many examples of Nix expressions. Each one is followed by the expected evaluation result. 

The following example is a Nix expression adding two numbers:

`1 + 2` = Expression

`3` = Value
### Interactive Evaluation

Use `nix repl` to evaluate nix expressions interactively (by typing them on the command line):

```
$ nix repl
Welcome to Nix 2.13.3. Type :? for help.

$ nix-repl> 1 + 2
```


> [!NOTE] Note
> The Nix language uses *lazy evaluation*, and `nix repl` by default only computes values when needed. 
> 
> Some examples show a fully evaluated data structure for clarity. If your output does not match the example, try prepending `:p` to the input expression.
> 
```
nix-repl> {a.b.c = 1; }
{ a = { ... }; }

nix-repl> :p { a.b.c = 1; }
{ a = { b = { c = 1; }; }; }
```

## Evaluating Nix Files

Use `nix-instantiate --eval` to evaluate the expression in a nix file. 

```
echo 1 + 2 > file.nix
nix-instantiate --eval file.nix
```


> [!Example] Explanation
> The first command writes `1 + 2` to a file `file.nix` in the current directory. The contents of `file.nix` are now `1 + 2`, which you can check with `cat file.nix`. 
> 
> The second command runs `nix-instantiate` with the `--eval` option on `file.nix`, which reads the file and evaluates the contained Nix expression. The resulting value is printed as output.
> 
> `--eval` is required to evaluate the file and do nothing else. If `--eval` is omitted, `nix-instantiate` expects the expression in the vien file to evaluate to a special value called a *derivation*, which we will come back to at the end of this tutorial in [Derivations](https://nix.dev/tutorials/nix-language#derivations).


> [!NOTE] 
> `nix-instantiate --eval` will try to read from `default.nix` if no file name is specifed.

> [!NOTE]
```
> > echo 1 + 2 > default.nix
> > nix-instantiate --eval
> > 3
```

> [!NOTE]
> The Nix language uses lazy evaluation, and `nix-instantiate` by default only computes values when needed.
> 
> Some examples show a fully evaluated data structure for clarity. If your output does not match the example, try adding the `--strict` option to `nix-instantiate`.
> 
> Example:
> 

```haskell
echo "{ a.b.c = 1; }" > file.nix

nix-instantiate --eval file.nix
{ a = <CODE>; }

echo "{ a.b.c = 1; }" > file.nix

nix-instantiate --eval --strict file.nix
{ a = { b = { c = 1; }; }; }
```
## Notes on Whitespace

White space is used to delimit [lexical tokens](https://en.wikipedia.org/wiki/Lexical_analysis#Lexical_token_and_lexical_tokenization), where required. It is otherwise insignificant. 

---
### Lexical token and lexical tokenization

Not to be confused with [Large language model § Tokenization](https://en.wikipedia.org/wiki/Large_language_model#Tokenization "Large language model"), or [tokenization (data security)](https://en.wikipedia.org/wiki/Tokenization_(data_security) "Tokenization (data security)").

A _lexical token_ is a [string](https://en.wikipedia.org/wiki/String_(computer_science) "String (computer science)") with an assigned and thus identified meaning, in contrast to the probabilistic token used in [large language models](https://en.wikipedia.org/wiki/Large_language_model "Large language model"). A lexical token consists of a _token name_ and an optional _token value_. The token name is a category of a rule-based lexical unit.(https://en.wikipedia.org/wiki/Lexical_analysis#cite_note-auto-2)

|Token name<br><br>(Lexical category)|Explanation|Sample token values|
|---|---|---|
|[identifier](https://en.wikipedia.org/wiki/Identifier_(computer_languages) "Identifier (computer languages)")|Names assigned by the programmer.|`x`, `color`, `UP`|
|[keyword](https://en.wikipedia.org/wiki/Reserved_word "Reserved word")|Reserved words of the language.|`if`, `while`, `return`|
|[separator/punctuator](https://en.wikipedia.org/wiki/Delimiter "Delimiter")|Punctuation characters and paired delimiters.|`}`, `(`, `;`|
|[operator](https://en.wikipedia.org/wiki/Operator_(computer_programming) "Operator (computer programming)")|Symbols that operate on arguments and produce results.|`+`, `<`, `=`|
|[literal](https://en.wikipedia.org/wiki/Literal_(computer_programming) "Literal (computer programming)")|Numeric, logical, textual, and reference literals.|`true`, `6.02e23`, `"music"`|
|[comment](https://en.wikipedia.org/wiki/Comment_(computer_programming) "Comment (computer programming)")|Line or block comments. Usually discarded.|`/* Retrieves user data */`, `// must be negative`|
|[whitespace](https://en.wikipedia.org/wiki/Whitespace_character "Whitespace character")|Groups of non-printable characters. Usually discarded.|–|

Consider this expression in the [C](https://en.wikipedia.org/wiki/C_(programming_language) "C (programming language)") programming language:

`x = a + b * 2;`

The lexical analysis of this expression yields the following sequence of tokens:

`[(identifier, x), (operator, =), (identifier, a), (operator, +), (identifier, b), (operator, *), (literal, 2), (separator, ;)]`

A token name is what might be termed a [part of speech](https://en.wikipedia.org/wiki/Part_of_speech "Part of speech") in linguistics.

_Lexical tokenization_ is the conversion of a raw text into (semantically or syntactically) meaningful lexical tokens, belonging to categories defined by a "lexer" program, such as identifiers, operators, grouping symbols, and data types. The resulting tokens are then passed on to some other form of processing. The process can be considered a sub-task of [parsing](https://en.wikipedia.org/wiki/Parsing "Parsing") input.

For example, in the text [string](https://en.wikipedia.org/wiki/String_(computer_science) "String (computer science)"):

`The quick brown fox jumps over the lazy dog`

the string is not implicitly segmented on spaces, as a [natural language](https://en.wikipedia.org/wiki/Natural_language "Natural language") speaker would do. The raw input, the 43 characters, must be explicitly split into the 9 tokens with a given space delimiter (i.e., matching the string `" "` or [regular expression](https://en.wikipedia.org/wiki/Regular_expression "Regular expression") `/\s{1}/`).

When a token class represents more than one possible lexeme, the lexer often saves enough information to reproduce the original lexeme, so that it can be used in [semantic analysis](https://en.wikipedia.org/wiki/Semantic_analysis_(compilers) "Semantic analysis (compilers)"). The parser typically retrieves this information from the lexer and stores it in the [abstract syntax tree](https://en.wikipedia.org/wiki/Abstract_syntax_tree "Abstract syntax tree"). This is necessary in order to avoid information loss in the case where numbers may also be valid identifiers.

Tokens are identified based on the specific rules of the lexer. Some methods used to identify tokens include [regular expressions](https://en.wikipedia.org/wiki/Regular_expression "Regular expression"), specific sequences of characters termed a [flag](https://en.wikipedia.org/wiki/Flag_(computing) "Flag (computing)"), specific separating characters called [delimiters](https://en.wikipedia.org/wiki/Delimiter "Delimiter"), and explicit definition by a dictionary. Special characters, including punctuation characters, are commonly used by lexers to identify tokens because of their natural use in written and programming languages. A lexical analyzer generally does nothing with combinations of tokens, a task left for a [parser](https://en.wikipedia.org/wiki/Parser "Parser"). For example, a typical lexical analyzer recognizes parentheses as tokens but does nothing to ensure that each "(" is matched with a ")".

When a lexer feeds tokens to the parser, the representation used is typically an [enumerated type](https://en.wikipedia.org/wiki/Enumerated_type "Enumerated type"), which is a list of number representations. For example, "Identifier" can be represented with 0, "Assignment operator" with 1, "Addition operator" with 2, etc.

Tokens are often defined by [regular expressions](https://en.wikipedia.org/wiki/Regular_expression "Regular expression"), which are understood by a lexical analyzer generator such as [lex](https://en.wikipedia.org/wiki/Lex_(software) "Lex (software)"), or handcoded equivalent [finite state automata](https://en.wikipedia.org/wiki/Finite_state_automata "Finite state automata"). The lexical analyzer (generated automatically by a tool like lex or hand-crafted) reads in a stream of characters, identifies the [lexemes](https://en.wikipedia.org/wiki/Lexical_analysis#Lexeme) in the stream, and categorizes them into tokens. This is termed _tokenizing_. If the lexer finds an invalid token, it will report an error.

Following tokenizing is [parsing](https://en.wikipedia.org/wiki/Parsing "Parsing"). From there, the interpreted data may be loaded into data structures for general use, interpretation, or [compiling](https://en.wikipedia.org/wiki/Compiling "Compiling").

---

Line breaks, indentation, and additional spaces are for readers' convenience.

The following are equivalent:

```haskell
let
 x = 1;
 y = 2;
in x + y
```
```
3
```

```haskell
let x=1;y=2;in x+y
```
```
3
```
## Names and Values

Values in the Nix language can be primitive data types, lists, attribute sets, and functions.

We show examples of primitive data types and lists in the context of [attribute sets](https://nix.dev/tutorials/nix-language#attrset). Later in this section, we cover special features of character strings: [string interpolation](https://nix.dev/tutorials/nix-language#string-interpolation), [file system paths](https://nix.dev/tutorials/nix-language#file-system-paths), and [indented strings](https://nix.dev/tutorials/nix-language#indented-strings). We deal with [functions](https://nix.dev/tutorials/nix-language#functions) separately.

[Attribute sets](https://nix.dev/tutorials/nix-language#attrset) and [`let` expressions](https://nix.dev/tutorials/nix-language#let) are used to assign names to values. Assignments are denoted by a single equal sign (`=`).

Whenever you encounter an equal sign in Nix language code:

- On its left is the assigned value.
- On its right is the value, delimited by a semicolon.
## Attribute Set `{ ... }`

An attribute set is a collection of name-value-pairs, where names must be **unique**.

The following example shows all primitive data types, lists, and attribute sets. 

> [!NOTE]
> If you are familiar with JSON, imagine the Nix language as _JSON with functions_.
> 
> Nix language data types _without functions_ work just like their counterparts in JSON and look very similar.
### Nix

```json
{
  string = "hello";
  integer = 1;
  float = 3.141;
  bool = true;
  null = null;
  list = [ 1 "two" false ];
  attribute-set = {
    a = "hello"
    b = 2;
    c = 2.718;
    d - false;
  }; # comments are supported
}
```
### JSON

```JSON
{
  "string": "hello",
  "integer": 1,
  "float": 3.141,
  "bool": true,
  "null": null,
  "list": [1, "two", false],
  "object": {
    "a": "hello",
    "b": 1,
    "c": 2.718,
    "d": false
  }
}
```

> [!NOTE]
> - Attribute names usually do not need quotes.(https://nix.dev/tutorials/nix-language#attrnames)
> - List elements are separated by white space.(https://nix.dev/tutorials/nix-language#list-whitespace)
## Recursive Attribute Set `rec { ... }`

You will sometimes see attribute sets declared with `rec` prepended. This allows access to attributes from within the set.

Example:

```json
rec {
  one = 1;
  two = one + 1;
  three = two + 1;
}
```
```JSON
{ one = 1; three = 3; two = 2; }
```

> [!NOTE]
> Elements in an attribute set can be declared in any order, and are ordered on evaluation.

Counter-example:

```json
{
  one = 1;
  two = one + 1;
  three = two + 1;
}
```
```
error: undefined variable 'one'

       at «string»:3:9:

            2|   one = 1;
            3|   two = one + 1;
             |         ^
            4|   three = two + 1;
```
## `let ... in ...`

Also known as "`let` expression" or "`let` binding"

`let` expression allow assigning names to values for repeated use.

Example:

```json
let
  a = 1;
in
a + a
```
```output
2
```

> [!Example]
> Assignments are placed between the keywords `let` and `in`. In this example we assign `a = 1`.
> 
> After `in` comes the expression in which the assignments are valid, i.e. where assigned names can be used. In this example the expression is `a + a`, where `a` refers to `a = 1`.
> 
> By replacing the names with their assigned values, `a + a` evaluates to `2`.

Names can be assigned in **any order**, and expressions on the right of the assignment (`=`) can refer to other assigned names.

Example:

```json
let
  b = a + 1;
  a = 1;
in
a + b
```
```output
3
```

> [!Example] Explanation
> Assignments are placed between the keywords `let` and `in`. In this example we assign `a = 1` and `b = a + 1`.
> 
> The order of assignments does not matter. Therefore the following example, where the assignments are in reverse order, is equivalent.
> 
>
```
let
  a = 1;
  b = a + 1;
in
a + b
```

