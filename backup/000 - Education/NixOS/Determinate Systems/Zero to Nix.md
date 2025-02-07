#Nix #packagemanagement

# 2. Run a Program with Nix

[Quick start](https://zero-to-nix.com/start) / Run a program with Nix

In the last section, we installed Nix using the [Determinate Nix Installer](https://zero-to-nix.com/concepts/nix-installer). Now we can dive in and use Nix to run an actual program. Let's try running the delightful [ponysay](https://github.com/erkin/ponysay):

```Bash
echo "Hello Nix" | nix run "http://flakehub.com/f/NixOS/nixpkgs/*#ponysay"
```

## Explanation

What happened here?

1. Nix used a [flake reference](https://zero-to-nix.com/concepts/flakes#references) to [Nixpkgs](https://zero-to-nix.com/concepts/nixpkgs) to pull in some Nix code and targeted the `ponysay` [flake output](https://zero-to-nix.com/concepts/flakes#outputs) (more on this later).
2. It built the [`ponysay` package](https://github.com/erkin/ponysay) and stored the result in the [Nix store](https://zero-to-nix.com/concepts/nix-store).
3. It ran the executable at `bin/ponysay` from the `ponysay` package.

In Nix, every program is part of a [package](https://zero-to-nix.com/concepts/packages). Packages are built using the [Nix language](https://zero-to-nix.com/concepts/nix-language#derivations). The `ponysay` package has a single program (also called `ponysay`) but packages can contain multiple programs as well as man pages, configuration files, and more. The The [`ffmpeg`](https://github.com/NixOS/nixpkgs/blob/master/pkgs/development/libraries/ffmpeg/generic.nix) package, for example, provides both [ffmpeg](https://ffmpeg.org) and [ffprobe](https://ffmpeg.org/ffprobe.html).

> [!Success] Install and run in one command
> You may have noticed that [`nix run`](https://nixos.org/manual/nix/stable/command-ref/new-cli/nix3-run) doesn't require anything like a `nix install` command. This makes it handy for use cases like shell scripting or experimenting with in-progress tools.

**Congrats**! You've just run a program using the Nix CLI and learned a little bit about some core Nix concepts. You're now ready to explore Nix development environments.

# 3. Explore Nix Development Environments

[Quick start](https://zero-to-nix.com/start) / Explore Nix development environments

In this guideL

→Use the `nix develop` command to activate a Nix development environment
→Run a command inside a development environment without actually entering that environment
→Explore Nix development environments tailored to specific programming languages
→Explore a more mixed development environment
→Use `nix develop` to activate an environment defined in a local [flake](https://zero-to-nix.com/concepts/flakes)

One of Nix's key features for developing software is Nix [development environments](https://zero-to-nix.com/concepts/dev-env). You can define development environments of any complexity using the [Nix language](https://zero-to-nix.com/concepts/nix-language). We will cover that in a bit later, but for now let's get a feel for what a Nix development environment is and how it works.

```Bash
nix develop "https://flakehub.com/f/DeterminateSystems/zero-to-nix/*#example"
```

🚀 **Success**! We're now in a Bash environment that includes `curl` and `git`. We may already have both in our environment, but running these commands will show us that something new is happening:

```bash
type curl
type git
```

![](https://i.imgur.com/gbibWqO.png)

What happened here? The `Nix` CLI did a few things;

1. It used the `https://flakehub.com/f/DeterminateSystems/zero-to-nix/*#example` [flake reference](https://zero-to-nix.com/concepts/flakes) to pull in some Nix code and built a specific [flake output](https://zero-to-nix.com/concepts/flakes#outputs) (more on this later).
2. It built the packages specified in the environment configuration (again, more on this later).
3. It set up an environment with a [`PATH`](https://en.wikipedia.org/wiki/PATH_(variable)) that enables the `git` and `curl` packages to be discovered in the [Nix store](https://zero-to-nix.com/concepts/nix-store). 

Two other things that we can provide in Nix development environments:

1. Although this example doesn't include one, we can differentiate and define *shell hooks*, which are arbitrary shell code that runs whenever the environment spins up. Some example use cases for shell hooks:
	- `echo` information about the environment to the console whenever the environment is activated.
	- Run things like checks and linters
	- Ensure that other desired hooks, like [Git hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks), are properly set up. Run this to see an example shell hook:

```Bash
nix develop "https://flakehub.com/f/DeterminateSystems/zero-to-nix/*#hook"
```

2. Nix development environments support environment variables as well. Run `echo $FUNNY_JOKE` to access a hilarious value that's available only in the Nix environment (the run **exit** to leave the environment). Some example use cases for environment variables:
	- Set logging levels using `LOG_LEVEL` or whatever is appropriate for the tools we're using.
	- Set the environment using variables like `NODE_ENV` (for Node.js) to **development**, **dev**, and so on.

Let's leave the Nix development environment to prepare for the next section:

```
exit
```

If you have `Git` installed, check the `PATH` for it using `type git`. It should be at a global path like `/usr/bin/git`. And if you run `echo $FUNNY_JOKE` again you should get an empty string (unless you happen to have that variable set on your machine.)
## Run Commands in the Development Environment

While it's fun to explore the environment, you don't always want to be inside the environment to use it. The `nix develop` command provides a `--command` (or `-c`) flag that you can use to run commands that *use* the environment by *from* your current environment. Here are some example for the environment we used earlier:

```bash
nix develop "https://flakehub.com/f/DeterminateSystems/zero-to-nix/*#example" --command git help
nix develop "https://flakehub.com/f/DeterminateSystems/zero-to-nix/*#example" --command curl https://example.com
```

In both cases, we're running a package in the [Nix store](https://zero-to-nix.com/concepts/nix-store) and nothing from the global environment. As you can see, Nix development environments are [_hermetic_](https://zero-to-nix.com/concepts/hermeticity) in that they're isolated from the surrounding environment (such as your environment variables and paths like `/bin` and `/usr/bin`).
## Language-Specific Environments

As we did in the last section, let's get a but more specific and explore how Nix can benefit more specific programming environments. Select one of these programming languages:

Let's explore a development environment for Python:

```bash
nix develop "github:DeterminateSystems/zero-to-nix#python"
```

First, let's see the Nix store path for Python:

```bash
type python
```

Now use Python to run a program:

```bash
python -c "print(1 + 1)"
```

Like usual, run `exit` to leave the Nix environment and return to your usual environment.
## Beyond Language-Specific Environments

In the [previous section](https://zero-to-nix.com/start/nix-develop#language-specific-environments), we explored Nix environments tailored to specific programming languages. But Nix environments are *infinitely flexible*, enabling us to combine whichever packages we like. Let's explore an example of this:

```bash
nix develop "https://flakehub.com/f/DeterminateSystems/zero-to-nix/*#multi"
```

This environment has several tools available:

- [Python](https://python.org)
- [kubectl](https://kubernetes.io/docs/reference/kubectl)
- [Terraform](https://terraform.io)
- [OpenSSL](https://openssl.org)

As in the previous examples, you can run commands like `type python` and `type kubectl` to see that these tools are all discoverable  in the Nix Store and not somewhere like `/usr/bin`. This list could easily include 100 packages. It's up to you. We won't cover *how* to create these environments just yet, but we hope that we come away from this guide with a basic sense of what Nix development environments can do.

> [!SUCCESS] Nix development environments and direnv
> [direnv](https://direnv.net) is a popular tool that automatically loads specific environment variables whenever you `cd` into a directory (and then unloads those variables when you `cd` out of the directory). The combination of direnv and Nix can be quite powerful, enabling you to automatically load Nix development environments whenever you navigate to a directory. For more info, see [Effortless dev environments with Nix and direnv](https://determinate.systems/posts/nix-direnv) on the [Determinate Systems blog](https://determinate.systems/posts).
## From a Local Flake

Earlier in this guide, we activated a Nix development environment defined in a [flake](https://zero-to-nix.com/concepts/flakes) on [FlakeHub](https://flakehub.com). While using an environment in this way is helpful, it's more common to use a development environment defined *in a local flake* in the current directory. 

To get started in our Python project, create an empty directory and initialize a [flake template](https://zero-to-nix.com/concepts/flakes#templates):

```bash
mkdir nix-python-dev && cd nix-python-dev
nix flake init --template "github:DeterminateSystems/zero-to-nix#python-dev"
```

Once the template has been initialized, run `ls .` to see the contents of the directory, which should include two important files:

- The **flake.nix** file defines the [flake](https://zero-to-nix.com/concepts/flakes) for your project.
- The **flake.lock** file [pins](https://zero-to-nix.com/concepts/pinning) all of the [flake inputs](https://zero-to-nix.com/concepts/flakes#inputs)—essentially the Nix dependencies-in your **flake.nix** file to specific [Git revisions](https://git-scm.com/docs/revisions).

One of the [flake outputs](https://zero-to-nix.com/concepts/flakes#outputs) of this Nix [flake](https://zero-to-nix.com/concepts/flakes) is a [development environment](https://zero-to-nix.com/concepts/dev-env) for Python. To enter that development environment:

```
nix develop
```

Now that we've entered the development environment, we can do some exploring, starting with [Nix store paths](https://zero-to-nix.com/concepts/nix-store#store-paths).

Ordinarily when you run `type python` on a Unix system, you get a path like `usr/bin/python`. Try running it in the Nix development environment.

```bash
type python
```

You should see a (rather strange) path like this:

```
python is /nix/store/cqbfx55481irqgbl3bw8jwf69vjpbp8r-python3-3.9.15/bin/python
```

Probably not what we expected! What happened here? A few things:

- Nix looked at the `devShells` [flake outputs](https://zero-to-nix.com/concepts/flakes#outputs) in **flake.nix** to figure out which [Nix packages](https://zero-to-nix.com/concepts/packages) to include in the development environment (Nix specifically looked at the packages array).
- Nix built the packages specified under **packages** and stored them in the [Nix store](https://zero-to-nix.com/concepts/nix-store) under `/nix/store`.
# Build a Package Using Nix

[Quick start](https://zero-to-nix.com/start) / Build a package using Nix

In this guide

→Build a Nix [package](https://zero-to-nix.com/concepts/packages) defined in [Nixpkgs](https://zero-to-nix.com/concepts/nixpkgs)
→Run the package from the local directory
→Initialize a [flake template](https://zero-to-nix.com/concepts/flakes#templates) in your preferred programming language
→Build a [Nix package](https://zero-to-nix.com/concepts/packages) from the `flake.nix` in the template

While Nix can do many things, [package management](https://zero-to-nix.com/concepts/package-management) is the thing that it's perhaps best known for. In this tutorial, we'll use our installed [installed Nix CLI](https://zero-to-nix.com/start/install) to build and run some Nix [packages](https://zero-to-nix.com/concepts/packages) included in [Nixpkgs](https://zero-to-nix.com/concepts/nixpkgs). Later in the guide we'll build and run a Nix package defined in a local [flake](https://zero-to-nix.com/concepts/flakes).
## Build a Package from `nixpkgs`

Let's start by building [bat](https://github.com/sharkdp/bat), a syntax-highlighted version of `cat` written in Rust that has a Nix package defined in [Nixpkgs](https://zero-to-nix.com/concepts/nixpkgs), in an empty directory (make sure to run this in a directory where you have write access).

```
mkdir build-nix-package && cd build-nix-package
nix build "https://flakehub.com/f/NixOS/nixpkgs/*#bat"
```

Here, `nixpkgs` is a [flake reference](https://zero-to-nix.com/concepts/flakes#references) to the [NixOS/nixpkgs](https://github.com/NixOS/nixpkgs) repository on GitHub, while `#bat` indicates that we're building the `bat` output from the Nixpkgs flake. 

When the build is done, run `ls .` and you should see something called `result` in the current directory. `result` is actually a [symlink](https://en.wikipedia.org/wiki/Symbolic_link) to the built package in the [Nix store](https://zero-to-nix.com/concepts/nix-store), which you can verify:

```
readlink result
```

You should see a path like this (it's likely to be a bit different on your machine):

| `/nix/store/`       | `sglc12hc6pc68w5ppn2k56n6jcpaci16` | `-bat.0.22.1`   |
| ------------------- | ---------------------------------- | --------------- |
| 1. Nix Store Prefix | 2. Hash Part                       | 3. Package Name |

What's happened here is that the Nix CLI has:

- Downloaded the Nix code in [Nixpkgs](https://zero-to-nix.com/concepts/nixpkgs)
- Found a package definition with the name **bat** (code [here](https://github.com/NixOS/nixpkgs/blob/master/pkgs/by-name/ba/bat/package.nix))
- Used the build instructions for **bat** to build the [package](https://zero-to-nix.com/concepts/packages)
- Stored the result in the [Nix store](https://zero-to-nix.com/concepts/nix-store) using Nix's hash-based path system

We can now run bat:

```
./result/bin/bat --help
```

🚀 **Success**! You've built and run a package using Nix.
## Build a Package for Tools Written in `$LANGUAGE`

One of the great things about Nix is that package builds are extremely flexible, which enables you to create packages for things written in just about any programming language. In this section, we'll explore that by building and running packages for tools written in a variety of languages. Select one below to see some examples:

Let's build and run [pip](https://pypi.org/project/pip):

```
nix build "nixpkgs#python3Packages.pip"
./result/bin/pip --help
```
## Beyond Nixpkgs

While Nixpkgs is by far the largest Nix package repository in the known universe, any [Nix flake](https://zero-to-nix.com/concepts/flakes) can include package [outputs](https://zero-to-nix.com/concepts/flakes#outputs). Let's build a package from a different repo, this time the package for [Home Manager](https://github.com/nix-community/home-manager), a popular Nix tool for configuring home environments:

```
nix build "https://flakehub.com/f/nix-community/home-manager/*"
```

Here, `https://flakehub.com/f/nix-community/home-manager/*` is a flake reference to the [nix-community/home-manager](https://github.com/nix-community/home-manager) repo on FlakeHub. To run Home Manager:

```
./result.bin/home-manager --help
```

Upstreaming your packages to Nixpkgs is always an option, but it's good to bear in mind that with Nix you can distribute packages via any public Git repository with a `flake.nix`.
## Build a Package in a Local Flake

[Earlier](https://zero-to-nix.com/start/nix-build#nixpkgs) in this guide, we built a Nix package defined in [Nixpkgs](https://zero-to-nix.com/concepts/nixpkgs) to get a sense of some of the mechanics of that process. In this guide, we'll dig a bit deeper and build a Nix package defined in a local [Nix flake](https://zero-to-nix.com/concepts/flakes).

To get started in your Python project, create an empty directory and initialize a [flake template](https://zero-to-nix.com/concepts/flakes#templates)

```
mkdir nix-python-pkg && cd nix-python-pkg
nix flake init --template "github:DeterminateSystems/zero-to-nix#python-pkg"
```

Whichever language you've selected, you can build the [Nix package](https://zero-to-nix.com/concepts/packages) defined in the local flake by running:

```
nix build
```

This command determines that the local flake has a [package output](https://zero-to-nix.com/concepts/flakes#outputs) that defines how the package is built. In this particular flake there's a `default` package, which enables us to run `nix build` without specifying an output, but if the package were output as `packages.mypkg`, for example, we'd need to run `nix build .#mypkg` to build it.

Here's the package definition that enables us to build our Python package:

```Nix
 packages.default = python.pkgs.buildPythonApplication {
  name = "zero-to-nix-python";
  src = self;
  buildInputs = with python.pkgs; [ pip ];
};
```

For the full flake, see [`flake.nix`](https://github.com/DeterminateSystems/zero-to-nix/tree/main/nix/templates/pkg/python/flake.nix) on GitHub or run `cat flake.nix`. What you see here is a [derivation](https://zero-to-nix.com/concepts/derivations) that defines how to build the package, more specifically the [`buildPythonApplication`](https://nixos.org/manual/nixpkgs/stable/#buildpythonapplication-function) function, which is a wrapper around Nix's built-in `derivation` function.

The resulting package is an executable that prints to the terminal. To run the package:

```
./result/bin/zero-to-nix-python
```

We should see this terminal output:

```
Hello from inside a Python program built with Nix!
```

We won't delve too much deeper into [derivations](https://zero-to-nix.com/concepts/derivations) and creating your own packages here, but we hope that this guide shows you how Nix code gets turned into real build output.
# Search For Nix Packages

***In this guide***

→Use the `nix search` command to find packages in [Nixpkgs](https://zero-to-nix.com/concepts/nixpkgs)
→Explore the [search.nixos.org](https://search.nixos.org) web interface
→Use the `nix flake show` command to explore packages output by [flakes](https://zero-to-nix.com/concepts/flakes)

One great thing about Nix is that there are *tons* of [packages](https://zero-to-nix.com/concepts/packages) available in the [Nix ecosystem](https://zero-to-nix.com/concepts/ecosystem) that you can use in [Nix development environments](https://zero-to-nix.com/concepts/dev-env), your NixOS installation, and more. While [Nixpkgs](https://zero-to-nix.com/concepts/nixpkgs) is by far the largest Nix package collection—over 100,000 packages and counting 😎—any [Nix flake](https://zero-to-nix.com/concepts/flakes) can provide package [outputs](https://zero-to-nix.com/concepts/flakes#outputs).

But navigating all of this plenty can be tricky, so in this guide we'll learn how to search for packages in Nixpkgs using the [`nix search`](https://nixos.org/manual/nix/stable/command-ref/new-cli/nix3-search) command and using the web application at [search.nixos.org](https://search.nixos.org). Then we'll learn how to explore packages in [other flakes](https://zero-to-nix.com/start/nix-search#nix-flake-show).
## The `nix search` command

The [Nix CLI](https://zero-to-nix.com/concepts/nix) has a `search` command that you can use to search the packages in a flake based on a search term. Let's start by searching [Nixpkgs](https://zero-to-nix.com/concepts/nixpkgs), which is where we're mostly likely to find packages we want. This command will tell us if [cargo](https://github.com/rust-lang/cargo) is available in [Nixpkgs](https://zero-to-nix.com/concepts/nixpkgs):

```
nix search "https://flakehub.com/f/NixOS/nixpkgs/*" cargo
```

> [!Warning]
> The first time you run `nix search`, the Nix CLI needs to download the full Nix code contents of [Nixpkgs](https://zero-to-nix.com/concepts/nixpkgs)—or whichever flake you're searching—and then cache it. Future `nix search` runs should be much speedier. Furthermore, Nixpkgs is the largest flake in existence and running `nix search` on other flakes should be much faster in general.

This brings up many results of the form `legacyPackages.{system}.{package}`, the first of which should look like this on Apple Silicon (`aarch64-darwin`) systems:

```
* legacyPackages.aarch64-darwin.cargo (1.65.0)
  Downloads your Rust project's dependencies and builds your project
```

The system attribute varies on other platforms (you may see `x86_64-linux` or something else). After that first result, you should see many others, including packages like [`cargo-about`](https://github.com/EmbarkStudios/cargo-about) and [`cargo-audit`](https://github.com/RustSec/rustsec/tree/main/cargo-audit).

> [!Warning] `legacyPackages` isn't legacy software
> The `legacyPackages` attribute that you see in the search output is a bit misleading. The [packages](https://zero-to-nix.com/concepts/packages) prefaced with that aren't "legacy" packages; instead, [Nixpkgs](https://zero-to-nix.com/concepts/nixpkgs) uses a special `legacyPackages` attribute to output packages instead of the usual `packages` output for reasons laid out [here](https://github.com/NixOS/nixpkgs/blob/fcc8ff7cc271c9652623dae2a9fcd1ba49232b57/flake.nix#L47-L55).

You can also output search results as JSON using the `--json` flag:

```
nix search nixpkgs cargo --json
```

This can be useful if you want to parse the output using a tool like `jq`.

## search.nixos.org

The web interface at [search.nixos.org](https://search.nixos.org) has a few advantages over the [`nix search`](https://zero-to-nix.com/start/nix-search#nix-search-command) command:

- It enables you to select a release channel for [Nixpkgs](https://zero-to-nix.com/concepts/nixpkgs), such as [22.11](https://github.com/nixOS/nixpkgs/tree/22.11) and [unstable](https://github.com/nixOS/nixpkgs/tree/nixpkgs-unstable)
- It enables you to search across a range of [public flakes](https://search.nixos.org/flakes) beyond Nixpkgs (those flakes are listed [here](https://github.com/NixOS/nixos-search/blob/main/flakes/manual.toml))

## Exploring a flake with the `nix flake show` command

As an example, let's explore a popular flake for the [Wayland](https://wayland.freedesktop.org) window system protocol.

> [!Warning] This could take a while
> The first time you run `nix flake show`, the Nix CLI needs to download the full contents of [`nixpkgs-wayland`](https://github.com/nix-community/nixpkgs-wayland)—or whichever flake you're running `nix flake show` on—and then cache it. Future `nix flake show` runs for the same [flake reference](https://zero-to-nix.com/concepts/flakes#references) should be much speedier.

> [!Important] When to use `nix search` vs. `nix flake show`
> Should you use `nix flake show` or `nix search`? A good rule of thumb is to always use `nix search` with Nixpkgs and to initially use `nix flake show` with other flakes. If the package outputs for `nix flake show` are big enough to be tricky to navigate, use `nix search` for that flake instead.

## System Specificity

One thing you'll notice about the search output for `nix search`, [search.nixos.org](https://search.nixos.org), and `nix flake show` is that all the packages listed in the query results are for your current system (`x86_64-linux` for an AMD/Intel Linux system, `aarch64-darwin` for an Apple Silicon system, and so on). That's because Nix works in a fundamentally [system-specific](https://zero-to-nix.com/concepts/system-specificity) way. The `cargo` package on a Linux machine is considered a _different package_ from `cargo` on a non-Linux system.
# Turn Your Project into a Flake

In some of the previous steps in Zero to Nix you learned about [Nix flakes](https://zero-to-nix.com/concepts/flakes) and Nix [development environments](https://zero-to-nix.com/concepts/dev-env). Turning your own projects into flakes can be somewhat tricky, so we at [Determinate Systems](https://determinate.systems) have created a tool that can help in many scenarios: [`fh`](https://github.com/DeterminateSystems/fh), the CLI for the [FlakeHub](https://zero-to-nix.com/concepts/flakehub) platform. `fh` has a utility called `fh init` that creates a `flake.nix` file based on two things:

1. The contents of your project
2. The responses to its interactive questions

You can run `fh init` using Nix:

```
nix run "https://flakehub.com/f/DeterminateSystems/fh/*" -- init
```

This will start up an interactive builder that asks you a series of questions and then writes a `flake.nix` file into the root of your project (plus some other files if you say yes to some of those questions). Once you've generated a new flake, you can see which outputs it has:

```
nix flake show
```

You should see something like this:

```
git+file:///path/to/fh-init-example-project
├───devShells
│   ├───aarch64-darwin
│   │   └───default: development environment 'nix-shell'
│   ├───aarch64-linux
│   │   └───default omitted (use '--all-systems' to show)
│   ├───x86_64-darwin
│   │   └───default omitted (use '--all-systems' to show)
│   └───x86_64-linux
│       └───default omitted (use '--all-systems' to show)
└───schemas: unknown
```

`fh init` supports a wide variety of [languages and tools](https://github.com/DeterminateSystems/fh/tree/main/src/cli/cmd/init/handlers). If your project has a [`Cargo.toml`](https://doc.rust-lang.org/cargo/reference/manifest.html) file in the root, for example, then `fh init` infers that it's a [Rust](https://rust-lang.org) project and asks if you want to add Rust dependencies to your Nix [development environment](https://zero-to-nix.com/concepts/dev-env). If you say yes, then the generated `flake.nix` will include the `cargo` build tool plus some other Rust-specific tools. Note that `fh init` currently only supports [`devShells`](https://zero-to-nix.com/concepts/dev-env) outputs. That is, it only generates a development environment for you, not things like [package outputs](https://zero-to-nix.com/concepts/packages).

> [!Warning]
> Be aware that `fh init` operates on a "best-guess" basis to infer which languages and tools you use in your project. It's possible that it will miss things or make incorrect guesses. But we hope that the `flake.nix` that it creates for you will at least serve as a solid initial template that you can modify further.
## Example Project

We've created an example project that you can use to test out `fh init`:

```
git clone https://github.com/DeterminateSystems/fh-init-example-project
cd fh-init-example-project
nix run "https://flakehub.com/f/DeterminateSystems/fh/*" -- init

# respond to the prompts

nix flake show
```

# Learn More

https://zero-to-nix.com/start/learn-more

