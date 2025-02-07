#nix #nixos #nixshell #nixflakes 
# nix shell, nix develop & pkgs.runCommand

NixOS's reproducibility makes it ideal for building development environments. However, if you're used to other distros, you may encounter problems because NixOS has it's own logic. We'll briefly explain below.

In the following sections, we'll introduce how the development environment works in NixOS.

---
## Creating a Custom Shell Environment with `nix shell`.

The simplest way to create a development environment is to use `nix shell`. `nix shell` will create a shell environment with the specified Nix package installed.

Here's an example:

```nix
# hello is not available
› hello
hello: command not found

# Enter an environment with the 'hello' and `cowsay` package
› nix shell nixpkgs#hello nixpkgs#cowsay

# hello is now available
› hello
Hello, world!

# ponysay is also available
› cowsay "Hello, world!"
 _______
< hello >
 -------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```

`nix shell` is very useful when you just want to try out some packages or quickly create a clean environment.

--- 
## Creating a Development Environment

`nix shell` is simple and easy to use, but it's not very flexible, for a more complex development environment, we need to use `pkgs.mkShell` and `nix develop`.

We can create a development environment using `pkgs.mkShell { ... }` and open an interactive Bash shell of this development environment using `nix develop`. 

To see how `pkgs.mkShell` works, let's take a closer look at [its source code](https://github.com/NixOS/nixpkgs/blob/nixos-23.05/pkgs/build-support/mkshell/default.nix).

```nix
{ lib, stdenv, buildEnv }:

# A special kind of derivation that is only meant to be consumed by the
# nix-shell.
{ name ? "nix-shell"
, # a list of packages to add to the shell environment
  packages ? [ ]
, # propagate all the inputs from the given derivations
  inputsFrom ? [ ]
, buildInputs ? [ ]
, nativeBuildInputs ? [ ]
, propagatedBuildInputs ? [ ]
, propagatedNativeBuildInputs ? [ ]
, ...
}@attrs:
let
  mergeInputs = name:
    (attrs.${name} or [ ]) ++
    (lib.subtractLists inputsFrom (lib.flatten (lib.catAttrs name inputsFrom)));

  rest = builtins.removeAttrs attrs [
    "name"
    "packages"
    "inputsFrom"
    "buildInputs"
    "nativeBuildInputs"
    "propagatedBuildInputs"
    "propagatedNativeBuildInputs"
    "shellHook"
  ];
in

stdenv.mkDerivation ({
  inherit name;

  buildInputs = mergeInputs "buildInputs";
  nativeBuildInputs = packages ++ (mergeInputs "nativeBuildInputs");
  propagatedBuildInputs = mergeInputs "propagatedBuildInputs";
  propagatedNativeBuildInputs = mergeInputs "propagatedNativeBuildInputs";

  shellHook = lib.concatStringsSep "\n" (lib.catAttrs "shellHook"
    (lib.reverseList inputsFrom ++ [ attrs ]));

  phases = [ "buildPhase" ];

  # ......

  # when distributed building is enabled, prefer to build locally
  preferLocalBuild = true;
} // rest)
```

`pkgs.mkShell { ... }` is a special derivation (Nix package). It's `name`, `buildInputs`, and other parameters are customizable and `shellHook` is a special parameter that will be executed when `nix develop` enters the environment. 

Here is a `flake.nix` that defines a development environment with Node.js 18 installed:

```nix
{
  description = "A Nix-flake-based Node.js development environment";

  inputs = {
    nixpkgs.url = "github:nixos/nixpkgs/nixos-23.11";
  };

  outputs = { self , nixpkgs ,... }: let
    # system should match the system you are running on
    # system = "x86_64-linux";
    system = "x86_64-darwin";
  in {
    devShells."${system}".default = let
      pkgs = import nixpkgs {
        inherit system;
      };
    in pkgs.mkShell {
      # create an environment with nodejs_18, pnpm, and yarn
      packages = with pkgs; [
        nodejs_18
        nodePackages.pnpm
        (yarn.override { nodejs = nodejs_18; })
      ];

      shellHook = ''
        echo "node `${pkgs.nodejs}/bin/node --version`"
      '';
    };
  };
}
```

Create an empty folder, save the configuration as `flake.nix`, and then execute `nix develop` (or more precisely, you can use `nix develop .#default`), the current version of nodejs will be outputted, and you can now use `node` `pnpm` `yarn` seamlessly.
## Using zsh/fish/...instead of bash

`pkgs.mkShell` uses `bash` by default, but you can also use `zsh` or `fish` by adding `exec <your-shell>` into `shellHook`.

Here is an example:

```nix
{
  description = "A Nix-flake-based Node.js development environment";

  inputs = {
    nixpkgs.url = "github:nixos/nixpkgs/nixos-23.11";
  };

  outputs = { self , nixpkgs ,... }: let
    # system should match the system you are running on
    system = "x86_64-linux";
    # system = "x86_64-darwin";
  in {
    devShells."${system}".default = let
      pkgs = import nixpkgs {
        inherit system;
      };
    in pkgs.mkShell {
      # create an environment with nodejs_18, pnpm, and yarn
      packages = with pkgs; [
        nodejs_18
        nodePackages.pnpm
        (yarn.override { nodejs = nodejs_18; })
        nushell
      ];

      shellHook = ''
        echo "node `${pkgs.nodejs}/bin/node --version`"
        exec nu
      '';
    };
  };
}
```

With the above configuration, `nix develop` will enter the REPL environment of nushell.

---
## Creating a Development Environment with `pkgs.runCommand`

The derivation created by `pkgs.mkShell` cannot be used directly, but must be access via `nix develop`.

It is actually possible to create a shell wrapper containing the required packages via `pkgs.stdenv.mkDerivation`, which can then be run directly into the environment by executing the wrapper.

Using `mkDerivation` directly is a bit cumbersome, and Nixpkgs provides some simpler functions to help us create such wrappers, such as `pkgs.runCommand`.

Example:

```nix
{
  description = "A Nix-flake-based Node.js development environment";

  inputs = {
    nixpkgs.url = "github:nixos/nixpkgs/nixos-23.11";
  };

  outputs = { self , nixpkgs ,... }: let
    # system should match the system you are running on
    # system = "x86_64-linux";
    system = "x86_64-darwin";
  in {
    packages."${system}".dev = let
      pkgs = import nixpkgs {
        inherit system;
      };
      packages = with pkgs; [
          nodejs_20
          nodePackages.pnpm
          nushell
      ];
    in pkgs.runCommand "dev-shell" {
      # Dependencies that should exist in the runtime environment
      buildInputs = packages;
      # Dependencies that should only exist in the build environment
      nativeBuildInputs = [ pkgs.makeWrapper ];
    } ''
      mkdir -p $out/bin/
      ln -s ${pkgs.nushell}/bin/nu $out/bin/dev-shell
      wrapProgram $out/bin/dev-shell --prefix PATH : ${pkgs.lib.makeBinPath packages}
    '';
  };
}
```

Then execute `run run .#dev` or `nix shell .#dev --command 'dev-shell'`, you will enter a nushell session, where you can use the `node` `pnpm` command normally, and the node version is 20.

The wrapper generated in this way is an executable file, which does not actually depend on the `nix run` or `nix shell` command.

For example, we can directly install this wrapper through NixOS's `environment.systemPackages`, and then execute it directly.

```nix
{pkgs, lib, ...}:{

  environment.systemPackages = [
    # Install the wrapper into the system
    (let
      packages = with pkgs; [
          nodejs_20
          nodePackages.pnpm
          nushell
      ];
    in pkgs.runCommand "dev-shell" {
      # Dependencies that should exist in the runtime environment
      buildInputs = packages;
      # Dependencies that should only exist in the build environment
      nativeBuildInputs = [ pkgs.makeWrapper ];
    } ''
      mkdir -p $out/bin/
      ln -s ${pkgs.nushell}/bin/nu $out/bin/dev-shell
      wrapProgram $out/bin/dev-shell --prefix PATH : ${pkgs.lib.makeBinPath packages}
    '')
  ];
}
```

Add the above configuration to any NixOS module, then deploy it with `sudo nixos-rebuild switch`, and you can enter the development environment directly with the `dev-shell` command, which is the special feature of `pkgs.runCommand` compared to `pkgs.mkShell`.

Related source code:
- [pkgs/build-support/trivial-builders/default.nix - runCommand](https://github.com/NixOS/nixpkgs/blob/nixos-23.11/pkgs/build-support/trivial-builders/default.nix#L21-L49)
- [pkgs/build-support/setup-hooks/make-wrapper.sh](https://github.com/NixOS/nixpkgs/blob/nixos-23.11/pkgs/build-support/setup-hooks/make-wrapper.sh)

---
## Enter the Build Environment of any Nix Package

Now let's take a look at `nix develop`, first read the help document output by `nix develop --help`:

```
Name
    nix develop - run a bash shell that provides the build environment of a derivation

Synopsis
    nix develop [option...] installable
# ......
```

It tells us that `nix develop` accepts a parameter `installable`, which means that we can enter the development environment of any installable Nix package through it, not just the environment created by `pkgs.mkShell`.

By default, `nix develop` will try to use the following attributes in the flake outputs:

- `devShells.<system>.default`
- `package.<system>.default`

If we use `nix develop /path/to/flake#<name>` to specify the flake package address and flake output name, then `nix develop` will try the following attributes in the flake outputs:

- `devShells.<system>.<name>`
- `packages.<system>.<name>`
- `legacyPackages.<system>.<name>`

Now let's try it out. First, test it to confirm that We don't have `c++` `g++` and other compilation related commands in the current environment:

```
ryan in 🌐 aquamarine in ~
› c++
c++: command not found

ryan in 🌐 aquamarine in ~
› g++
g++: command not found
```

Then use `nix develop` to enter the build environment of the `hello` package in `nixpkgs`:

```nix
# login to the build environment of the package `hello`
ryan in 🌐 aquamarine in ~
› nix develop nixpkgs#hello

ryan in 🌐 aquamarine in ~ via ❄️  impure (hello-2.12.1-env)
› env | grep CXX
CXX=g++

ryan in 🌐 aquamarine in ~ via ❄️  impure (hello-2.12.1-env)
› c++ --version
g++ (GCC) 12.3.0
Copyright (C) 2022 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

ryan in 🌐 aquamarine in ~ via ❄️  impure (hello-2.12.1-env)
› g++ --version
g++ (GCC) 12.3.0
Copyright (C) 2022 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

We can see that the `CXX` environment variable has been set, and the `c++` and `g++` and other commands can be used normally now.

In addition, we can also call every build phase of the `hello` package normally:

> The default execution order of all build phases of a Nix package is: `$prePhases unpackPhase patchPhase $preConfigurePhases configurePhase $preBuildPhases buildPhase checkPhase $preInstallPhases installPhase fixupPhase installCheckPhase $preDistPhases distPhase $postPhases`

```nix
# unpack source code
ryan in 🌐 aquamarine in /tmp/xxx via ❄️  impure (hello-2.12.1-env)
› unpackPhase
unpacking source archive /nix/store/pa10z4ngm0g83kx9mssrqzz30s84vq7k-hello-2.12.1.tar.gz
source root is hello-2.12.1
setting SOURCE_DATE_EPOCH to timestamp 1653865426 of file hello-2.12.1/ChangeLog

ryan in 🌐 aquamarine in /tmp/xxx via ❄️  impure (hello-2.12.1-env)
› ls
hello-2.12.1

ryan in 🌐 aquamarine in /tmp/xxx via ❄️  impure (hello-2.12.1-env)
› cd hello-2.12.1/

# generate Makefile
ryan in 🌐 aquamarine in /tmp/xxx/hello-2.12.1 via ❄️  impure (hello-2.12.1-env)
› configurePhase
configure flags: --prefix=/tmp/xxx/outputs/out --prefix=/tmp/xxx/outputs/out
checking for a BSD-compatible install... /nix/store/02dr9ymdqpkb75vf0v1z2l91z2q3izy9-coreutils-9.3/bin/install -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /nix/store/02dr9ymdqpkb75vf0v1z2l91z2q3izy9-coreutils-9.3/bin/mkdir -p
checking for gawk... gawk
checking whether make sets $(MAKE)... yes
checking whether make supports nested variables... yes
checking for gcc... gcc
# ......
checking that generated files are newer than configure... done
configure: creating ./config.status
config.status: creating Makefile
config.status: creating po/Makefile.in
config.status: creating config.h
config.status: config.h is unchanged
config.status: executing depfiles commands
config.status: executing po-directories commands
config.status: creating po/POTFILES
config.status: creating po/Makefile

# build the package
ryan in 🌐 aquamarine in /tmp/xxx/hello-2.12.1 via C v12.3.0-gcc via ❄️  impure (hello-2.12.1-env) took 2s
› buildPhase
build flags: SHELL=/run/current-system/sw/bin/bash
make  all-recursive
make[1]: Entering directory '/tmp/xxx/hello-2.12.1'
# ......
ranlib lib/libhello.a
gcc  -g -O2   -o hello src/hello.o  ./lib/libhello.a
make[2]: Leaving directory '/tmp/xxx/hello-2.12.1'
make[1]: Leaving directory '/tmp/xxx/hello-2.12.1'

# run the built program
ryan in 🌐 aquamarine in /tmp/xxx/hello-2.12.1 via C v12.3.0-gcc via ❄️  impure (hello-2.12.1-env)
› ./hello
Hello, world!
```

This usage is mainly used to debug the build process of a Nix package, or to execute some commands in the build environment of a Nix package.

---
## `nix build`

The `nix build` command is used to build a software package and creates a symbolic link named `result` in the current directory, which points to the build result.

Here's an example:

```nix
# Build the package 'ponysay' from the 'nixpkgs' flake
nix build "nixpkgs#ponysay"
# Use the built 'ponysay' command
› ./result/bin/ponysay 'hey buddy!'
 ____________
< hey buddy! >
 ------------
     \
      \
       \
       ▄▄  ▄▄ ▄ ▄
    ▀▄▄▄█▄▄▄▄▄█▄▄▄
   ▀▄███▄▄██▄██▄▄██
  ▄██▄███▄▄██▄▄▄█▄██
 █▄█▄██▄█████████▄██
  ▄▄█▄█▄▄▄▄▄████████
 ▀▀▀▄█▄█▄█▄▄▄▄▄█████         ▄   ▄
    ▀▄████▄▄▄█▄█▄▄██       ▄▄▄▄▄█▄▄▄
    █▄██▄▄▄▄███▄▄▄██    ▄▄▄▄▄▄▄▄▄█▄▄
    ▀▄▄██████▄▄▄████    █████████████
       ▀▀▀▀▀█████▄▄ ▄▄▄▄▄▄▄▄▄▄██▄█▄▄▀
            ██▄███▄▄▄▄█▄▄▀  ███▄█▄▄▄█▀
            █▄██▄▄▄▄▄████   ███████▄██
            █▄███▄▄█████    ▀███▄█████▄
            ██████▀▄▄▄█▄█    █▄██▄▄█▄█▄
           ███████ ███████   ▀████▄████
           ▀▀█▄▄▄▀ ▀▀█▄▄▄▀     ▀██▄▄██▀█
                                ▀  ▀▀█
```

---
## Using `nix profile`to Manage Development Environments and Entertainment Environments

`nix develop` is a tool for creating and managing multiple user environments, and switch to different environments when needed. 

Unlike `nix develop`, `nix profile` manages the user's system environment, instead of creating a temporary shell environment. So it's more compatible with Jetbrains IDE / VSCode and other IDEs, and won't have the problem of not being able to use the configured development environment in the IDE.

---
## Other Commands

There are other commands like `nix flake init`, which you can explore in [New Nix Commands](https://nixos.org/manual/nix/stable/command-ref/new-cli/nix.html). For more detailed information, please refer to the documentation.

## References
- [pkgs.mkShell - nixpkgs manual](https://nixos.org/manual/nixpkgs/stable/#sec-pkgs-mkShell)
- [A minimal nix-shell](https://fzakaria.com/2021/08/02/a-minimal-nix-shell.html)
- [Wrapping packages - NixOS Cookbook](https://wiki.nixos.org/wiki/Nix_Cookbook#Wrapping_packages)
- [One too many shell, Clearing up with nix' shells nix shell and nix-shell - Yannik Sander](https://blog.ysndr.de/posts/guides/2021-12-01-nix-shells/)
- [Shell Scripts - NixOS Wiki](https://wiki.nixos.org/wiki/Shell_Scripts)
# Dev Environments

On NixOS, we have a variety of methods to set up development environments, with the most ideal approach being a complete definition of each project's development environment through it's own `flake.nix`. However, this can be somewhat cumbersome in practice, as it requires crafting a `flake.nix` and then running `nix develop` for each instance. For temporary projects or when one simply wants to glance at the code, this approach is somewhat overkill.

A compromise is to divide the development environment into **three tiers**:

1. **Global Environment**: This typically refers to the user environment managed by home-manager.
	- Universal development tools: `git`, `vim`, `emacs`, `tmux` and the like.
	- Common language SDKs and package managers: `rust`, `openjdk`, `python`, `go`, among others.

2. **IDE Environment**: 
	- Taking neovim as an example, home-manager creates a wrapper for neovim that encapsulates its dependencies within its own environment, preventing contamination of the global environment.
	- Dependencies for neovim plugins can be added to the neovim environment via the `programs.neovim.extraPackages` parameter, ensuring the IDE operates smoothly. 
	- However, if you use multiple IDEs (such as emacs and neovim), they often rely on many of the same programs (like lsp, tree-sitter, debugger, formatter, etc.). For ease of management, these shared dependencies can be placed in the global environment. Be cautious of potential dependency conflicts with other programs in the global environments, particularly with *python packages*, which are prone to conflicts.

3. **Project Environment**:
	- Each project can define its own development environment (`devShells`) via `flake.nix`.
	- To simplify, you can create generic `flake.nix` templates for commonly used languages in advanced, which can be copied and modified as needed. 
	- The project environment takes the highest precedence (added to the front of the PATH), and its dependencies will override those with the same name in the global environment. Thus, you can control the version of project dependencies via the project's `flake.nix`, unaffected by the global environment.

---
## Templates for Development Environments

We have learned how to build development environments, but it's a but tedious to write `flake.nix` for each project.

Luckily, some people in the community have done this for us. The following repository contains development environment templates for most programming languages. Just copy and paste them:

- [MordragT/nix-templates](https://github.com/MordragT/nix-templates)
- [the-nix-way/dev-templates](https://github.com/the-nix-way/dev-templates)

If you think the structure of `flake.nix` is still to complicated and want a simpler way, you can consider using the following project, which encapsulates Nix more thoroughly and provides users with a simpler definition:

-  [cachix/devenv](https://github.com/cachix/devenv)

If you don't want to write a single line of Nix code and just want to get a reproducible development environment at minimal cost, here's a tool that might meet those needs:

- [jetpack-io/devbox](https://github.com/jetpack-io/devbox)

---
## Dev Environment for Python

The development environment for Python is much more cumbersome compared to languages like Java or Go because it defaults to installing software in the global environment. To install software for the current project, you must create a virtual environment first (unlike in languages such as JavaScript or Go, where virtual environments are not necessary). This behavior is very unfriendly for Nix.

By default, when using pip in Python, it install software globally. On NixOS, running `pip install` directly will result in an error:

```nix
› pip install -r requirements.txt
error: externally-managed-environment

× This environment is externally managed
╰─> This command has been disabled as it tries to modify the immutable
    `/nix/store` filesystem.

    To use Python with Nix and nixpkgs, have a look at the online documentation:
    <https://nixos.org/manual/nixpkgs/stable/#python>.

note: If you believe this is a mistake, please contact your Python installation or OS distribution provider. You can override this, at the risk of breaking your Python installation or OS, by passing --break-system-packages.
hint: See PEP 668 for the detailed specification.
```

Based on the error message, `pip install` is directly disabled by NixOS. Even when attempting `pip install --user`, it is similarly disabled. To improve the reproducibility of the environment, Nix eliminates these commands altogether. Even if we create a new environment using methods like `mkShell`, these commands still result in errors (presumably because the pip command in Nixpkgs itself has been modified to prevent any modification instructions like `install` from running).

However, many project installation scripts are based on pip, which means these scripts cannot be used directly. Additionally, the content in nixpkgs is limited, and many packages from PyPI are missing. This requires users to package them themselves, adding a lot of complexity and mental burden. 

One solution is to use the `venv` virtual environment. Within a virtual environment, you can use commands like pip normally:

```
python -m venv ./env
source ./env/bin/activate
```

Alternatively, you can use a third-party tool called `virtualenv`, but this requires additional installation. 

For those who still lack confidence in the venv created directly with Python, they may prefer to include the virtual environment in `/nix/store` to make it immutable. This can be achieved by directly installing the dependencies from `requirements.txt` or `poetry.toml` using Nix. There are existing Nix packaging tools available to assist with this:

> Note that even in these environments, running commands like `pip install` directly will still fail. Python dependencies must be installed through `flake.nix` because the data is located in the `/nix/store` directory, and these modification commands can only be executed during the Nix build phase.

- [python venv demo](https://github.com/MordragT/nix-templates/blob/master/python-venv/flake.nix)
- [poetry2nix](https://github.com/nix-community/poetry2nix)

The advantage of these tools is that they utilize the lock mechanism of Nix Flakes to improve reproducibility. However, the downside is that they add an extra layer of abstraction, making the underlying system more complex. 

Finally, in some more complex projects, neither of the above solutions may be feasible. In such cases, the best solution is to use containers such as Docker or Podman. Containers have fewer restrictions compared to Nix and can provide the best compatibility.

---
# Packaging 101

## References

- [NixOS Series 3: Software Packaging 101](https://lantian.pub/en/article/modify-computer/nixos-packaging.lantian/)
- [How to Learn Nix, Part 28: The standard environment](https://ianthehenry.com/posts/how-to-learn-nix/the-standard-environment/)
- [stdenv - Nixpkgs Manual](https://github.com/NixOS/nixpkgs/tree/nixos-unstable/doc/stdenv)
- [languages-frameworks - Nixpkgs Manual](https://github.com/NixOS/nixpkgs/tree/nixos-unstable/doc/languages-frameworks)
- [Wrapping packages - NixOS Cookbook](https://wiki.nixos.org/wiki/Nix_Cookbook#Wrapping_packages)
- Useful tools:
    - [nurl](https://github.com/nix-community/nurl): Generate Nix fetcher calls from repository URLs
    - [nix-init](https://github.com/nix-community/nix-init): Generate Nix packages from URLs with hash prefetching, dependency inference, license detection, and more
- Source Code:
    - [pkgs/build-support/trivial-builders/default.nix - runCommand](https://github.com/NixOS/nixpkgs/blob/nixos-23.11/pkgs/build-support/trivial-builders/default.nix#L21-L49)
    - [pkgs/build-support/setup-hooks/make-wrapper.sh](https://github.com/NixOS/nixpkgs/blob/nixos-23.11/pkgs/build-support/setup-hooks/make-wrapper.sh)
    - FHS related
        - [pkgs/build-support/build-fhsenv-bubblewrap/buildFHSEnv.nix](https://github.com/NixOS/nixpkgs/blob/nixos-23.11/pkgs/build-support/build-fhsenv-bubblewrap/buildFHSEnv.nix): `pkgs.buildFHSEnvBubblewrap`
        - [pkgs/build-support/build-fhsenv-chroot/default.nix](https://github.com/NixOS/nixpkgs/blob/nixos-23.11/pkgs/build-support/build-fhsenv-bubblewrap/buildFHSEnv.nix): `pkgs.buildFHSEnvChroot`
# Cross-Platform Compilation

On any Linux platform, there are two ways to do cross-platform compilation. For example, to build an `aarch64-linux` program on an `x86_64-linux` host, you can use the following methods:

1. Use the cross-compilation toolchain to compile the `aarch64` program. 
	The disadvantage is that you cannot use the NixOS binary cache, and you need to compile everything yourself (cross-compilation also has a cache, but there is basically nothing in it).

	The advantages are that you don't need to emulate the instruction set, and the performance is high.

2. Use QEMU to emulate the `aarch64` architecture and then compile the program in the emulator. 
	The disadvantage is that the instruction set is emulated, and the performance is poor.

	The advantage is that you can use the NixOS binary cache, and you don't need to compile everything yourself.

If you use method one, you don't need to enable `binfmt_misc`, but you need to execute the compilation through the cross-compilation toolchain.

If you use method two, you need to enable the `binfmt_misc` of the `aarch64` architecture in the NixOS configuration of the building machine.

---
## Cross Compilation

`nixpkgs` provides a set of predefined host platforms for cross-compilation called `pkgsCross`. You can explore them in the `nix repl`.

```nix
› nix repl '<nixpkgs>'
warning: future versions of Nix will require using `--file` to load a file
Welcome to Nix 2.13.3. Type :? for help.

Loading installable ''...
Added 19273 variables.
nix-repl> pkgsCross.<TAB>
pkgsCross.aarch64-android             pkgsCross.msp430
pkgsCross.aarch64-android-prebuilt    pkgsCross.musl-power
pkgsCross.aarch64-darwin              pkgsCross.musl32
pkgsCross.aarch64-embedded            pkgsCross.musl64
pkgsCross.aarch64-multiplatform       pkgsCross.muslpi
pkgsCross.aarch64-multiplatform-musl  pkgsCross.or1k
pkgsCross.aarch64be-embedded          pkgsCross.pogoplug4
pkgsCross.arm-embedded                pkgsCross.powernv
pkgsCross.armhf-embedded              pkgsCross.ppc-embedded
pkgsCross.armv7a-android-prebuilt     pkgsCross.ppc64
pkgsCross.armv7l-hf-multiplatform     pkgsCross.ppc64-musl
pkgsCross.avr                         pkgsCross.ppcle-embedded
pkgsCross.ben-nanonote                pkgsCross.raspberryPi
pkgsCross.fuloongminipc               pkgsCross.remarkable1
pkgsCross.ghcjs                       pkgsCross.remarkable2
pkgsCross.gnu32                       pkgsCross.riscv32
pkgsCross.gnu64                       pkgsCross.riscv32-embedded
pkgsCross.i686-embedded               pkgsCross.riscv64
pkgsCross.iphone32                    pkgsCross.riscv64-embedded
pkgsCross.iphone32-simulator          pkgsCross.rx-embedded
pkgsCross.iphone64                    pkgsCross.s390
pkgsCross.iphone64-simulator          pkgsCross.s390x
pkgsCross.loongarch64-linux           pkgsCross.sheevaplug
pkgsCross.m68k                        pkgsCross.vc4
pkgsCross.mingw32                     pkgsCross.wasi32
pkgsCross.mingwW64                    pkgsCross.x86_64-darwin
pkgsCross.mips-linux-gnu              pkgsCross.x86_64-embedded
pkgsCross.mips64-linux-gnuabi64       pkgsCross.x86_64-freebsd
pkgsCross.mips64-linux-gnuabin32      pkgsCross.x86_64-netbsd
pkgsCross.mips64el-linux-gnuabi64     pkgsCross.x86_64-netbsd-llvm
pkgsCross.mips64el-linux-gnuabin32    pkgsCross.x86_64-unknown-redox
pkgsCross.mipsel-linux-gnu
pkgsCross.mmix
```

If you want to set `pkgs` to a cross-compilation toolchain globally in a flake, you only need to add a Module in `flake.nix`, as shown below:

```Nix
{
  description = "NixOS running on LicheePi 4A";

  inputs = {
    nixpkgs.url = "github:nixos/nixpkgs/nixos-23.11";
  };

  outputs = inputs@{ self, nixpkgs, ... }: {
    nixosConfigurations.lp4a = nixpkgs.lib.nixosSystem {
      # native platform
      system = "x86_64-linux";
      modules = [

        # add this module, to enable cross-compilation.
        {
          nixpkgs.crossSystem = {
            # target platform
            system = "riscv64-linux";
          };
        }

        # ...... other modules
      ];
    };
  };
}
```

The `nixkpgs.crossSystem` option is used to set `pkgs` to a cross-compilation toolchain, so that all the contents build will be `riscv64-linux` architecture.

