#Nix #nixos #flakes 
# Introduction

So far, we have extensively used Flakes to manage NixOS configurations. In this section, I will provide a brief introduction to additional features and command-line options commonly used with Flakes.
# Flake Inputs

The `inputs` section is `flake.nix` is an attribute set used to specify the dependencies of the current flake. There are various types of inputs, as shown in the examples below:

```Nix
{
  inputs = {
    # GitHub repository as the data source, specifying the master branch.
    # This is the most common input format.
    nixpkgs.url = "github:Mic92/nixpkgs/master";
    # Git URL, applicable to any Git repository using the https/ssh protocol.
    git-example.url = "git+https://git.somehost.tld/user/path?ref=branch";
    # Git URL by tag, applicable to any Git repository using the https/ssh protocol.
    git-example-tag.url = "git+https://git.somehost.tld/user/path?tag=x.y.x";
    # Github URL by pull request.
    git-pr.url = "github:NixOS/nixpkgs?ref=pull/349351/head";
    # Git URL with submodules, applicable to any Git repository using the https/ssh protocol.
    git-example-submodule.url = "git+https://git.somehost.tld/user/path?submodules=1";
    # Archive File URL, needed in case your input use LFS.
    # Regular git input doesn't support LFS yet.
    git-example-lfs.url = "https://codeberg.org/solver-orgz/treedome/archive/master.tar.gz";
    # Similar to fetching a Git repository, but using the ssh protocol
    # with key authentication. Also uses the shallow=1 parameter
    # to avoid copying the .git directory.
    ssh-git-example.url = "git+ssh://git@github.com/ryan4yin/nix-secrets.git?shallow=1";
    # It's also possible to directly depend on a local Git repository.
    git-directory-example.url = "git+file:/path/to/repo?shallow=1";
    # Using the `dir` parameter to specify a subdirectory.
    nixpkgs.url = "github:foo/bar?dir=shu";
    # Local folder (if using an absolute path, the 'path:' prefix can be omitted).
    directory-example.url = "path:/path/to/repo";

    # If the data source is not a flake, set flake=false.
    # `flake=false` is usually used to include additional source code,
    #   configuration files, etc.
    # In Nix code, you can directly reference files within
    #   it using "${inputs.bar}/xxx/xxx" notation.
    # For example, import "${inputs.bar}/xxx/xxx.nix" to import a specific nix file,
    # or use "${inputs.bar}/xx/xx" as a path parameter for certain options.
    bar = {
      url = "github:foo/bar/branch";
      flake = false;
    };

    sops-nix = {
      url = "github:Mic92/sops-nix";
      # `follows` is the inheritance syntax within inputs.
      # Here, it ensures that sops-nix's `inputs.nixpkgs` aligns with
      # the current flake's inputs.nixpkgs,
      # avoiding inconsistencies in the dependency's nixpkgs version.
      inputs.nixpkgs.follows = "nixpkgs";
    };

    # Lock the flake to a specific commit.
    nix-doom-emacs = {
      url = "github:vlaci/nix-doom-emacs?rev=238b18d7b2c8239f676358634bfb32693d3706f3";
      flake = false;
    };
  };

  outputs = { self, ... }@inputs: { ... };
}
```
# Flake Outputs

In `flake.nix`, the `outputs` section defines the different outputs that a flake can produce during its build process. A flake can have multiple outputs simultaneously, which can include but are not limited to the following:

- Nix packages: These are named `apps.<system>.<name>`, `packages.<system>.<name>`, or `legacyPackages.<system>.<name>`. You could build a specific package using the command `nix build .#<name>`.
- Nix helper functions. These are named `lib.<name>` and serve as libraries for other flakes to use.
- Nix development environments: These are named `devShells` and provide isolated development environments. They can be accessed using the command `nix develop`.
- NixOS configurations: These are named `nixosConfiguration` and represent specific NixOS system configurations. You can activate a configuration using the command `nixos-rebuild switch --flake .#<name>`.
- Nix templates: These are named `templates` and can be used as a starting point for creating new projects. You can generate a project using the command `nix flake init --template <reference>`.
- Other user-defined outputs: These outputs can be defined by the user and may be used by other Nix-related tools. 

Here's an example excerpt from the NixOS Wiki that demonstrates the structure of the `outputs` section:

```Nix
{
  inputs = {
    # ......
  };

  outputs = { self, ... }@inputs: {
    # Executed by `nix flake check`
    checks."<system>"."<name>" = derivation;
    # Executed by `nix build .#<name>`
    packages."<system>"."<name>" = derivation;
    # Executed by `nix build .`
    packages."<system>".default = derivation;
    # Executed by `nix run .#<name>`
    apps."<system>"."<name>" = {
      type = "app";
      program = "<store-path>";
    };
    # Executed by `nix run . -- <args?>`
    apps."<system>".default = { type = "app"; program = "..."; };

    # Formatter (alejandra, nixfmt or nixpkgs-fmt)
    formatter."<system>" = derivation;
    # Used for nixpkgs packages, also accessible via `nix build .#<name>`
    legacyPackages."<system>"."<name>" = derivation;
    # Overlay, consumed by other flakes
    overlays."<name>" = final: prev: { };
    # Default overlay
    overlays.default = {};
    # Nixos module, consumed by other flakes
    nixosModules."<name>" = { config }: { options = {}; config = {}; };
    # Default module
    nixosModules.default = {};
    # Used with `nixos-rebuild --flake .#<hostname>`
    # nixosConfigurations."<hostname>".config.system.build.toplevel must be a derivation
    nixosConfigurations."<hostname>" = {};
    # Used by `nix develop .#<name>`
    devShells."<system>"."<name>" = derivation;
    # Used by `nix develop`
    devShells."<system>".default = derivation;
    # Hydra build jobs
    hydraJobs."<attr>"."<system>" = derivation;
    # Used by `nix flake init -t <flake>#<name>`
    templates."<name>" = {
      path = "<store-path>";
      description = "template description goes here?";
    };
    # Used by `nix flake init -t <flake>`
    templates.default = { path = "<store-path>"; description = ""; };
  };
}
```
# Usage of the New CLI

Once you have enabled the `nix-command` and `flakes` features, you can start using the new generation Nix command-line tools provided by [New Nix Commands](https://nixos.org/manual/nix/stable/command-ref/new-cli/nix.html). In this section, we will focus on two commands: `nix shell` and `nix run`. Other important commands like `nix build` will be discussed in detail [`nix develop` & `pkgs.mkShell`](https://nixos-and-flakes.thiscute.world/development/intro) 

---
## `nix shell`

The `nix shell` command allows you to enter an environment with the specified Nix package and opens and interactive shell within that environment:

```Nix
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
## `nix run`

On the other hand, `nix run` creates an environment with the specified Nix package and directly runs that package within the environment (without installing it into the system environment):

```Nix
# hello is not available
› hello
hello: command not found

# Create an environment with the 'hello' package and run it
› nix run nixpkgs#hello
Hello, world!
```

Since `nix run` directly executes the Nix package, the package specified as the argument must generate an executable program.

According to the `nix run --help` documentation, `nix run` executes the command `<out>/bin/<name>`, where `<out>` is the root directory of the derivation and `<name>` is selected in the following order:

- The `meta.mainProgram` attribute of the derivation
- The `pname` attribute of the derivation
- The content of the `name` attribute of the derivation with the version number removed.

For example, in the case of the 'hello' package we tested earlier, `nix run` actually executes the program `$out/bin/hello`.

Here are two more examples with detailed explanations of the relevant parameters:

```Nix
# Explanation of the command:
#   `nixpkgs#ponysay` means the 'ponysay' package in the 'nixpkgs' flake.
#   `nixpkgs` is a flake registry id, and Nix will find the corresponding GitHub repository address
#   from <https://github.com/NixOS/flake-registry/blob/master/flake-registry.json>.
# Therefore, this command creates a new environment, installs, and runs the 'ponysay' package provided by the 'nixpkgs' flake.
#   Note: It has been mentioned earlier that a Nix package is one of the outputs of a flake.
echo "Hello Nix" | nix run "nixpkgs#ponysay"

# This command has the same effect as the previous one, but it uses the complete flake URI instead of the flake registry id.
echo "Hello Nix" | nix run "github:NixOS/nixpkgs/nixos-unstable#ponysay"
```
## Common Use Cases for `nix run` and `nix shell`

These commands are commonly used for running programs *temporarily*. For example, if I want to clone my configuration repository using Git on a new NixOS host without Git installed, I can use the following command:

```
nix run nixpkgs#git clone git@github.com:ryan4yin/nix-config.git
```

Alternatively, I can use `nix shell` to enter an environment with Git and then run the `git clone` command:

```
nix shell nixpkgs#git
git clone git@github.com:ryan4yin/nix-config.git
```
# Module System and Custom Options

In our previous NixOS configurations, we set various values for `options` to configure NixOS or Home Manager. These `options` are actually defined in two locations:

- NixOS: [nixpkgs/nixos/modules](https://github.com/NixOS/nixpkgs/tree/23.11/nixos/modules), where all NixOS options visible on [https://search.nixos.org/options](https://search.nixos.org/options) are defined.
- Home Manager: [home-manager/modules](https://github.com/nix-community/home-manager/blob/release-23.11/modules), where you can find all its options at [https://nix-community.github.io/home-manager/options.xhtml](https://nix-community.github.io/home-manager/options.xhtml).

> If you are using nix-darwin too, its configuration is similar, and its module system is implemented in [nix-darwin/modules](https://github.com/LnL7/nix-darwin/tree/master/modules).

The foundation of the aforementioned NixOS Modules and Home Manager Modules is a universal module system implemented in Nixpkgs, found in [lib/modules.nix](https://github.com/NixOS/nixpkgs/blob/23.11/lib/modules.nix#L995). The official documentation for this module system is provided below (even for experienced NixOS users, understanding this can be a challenging task):

- [Module System - Nixpkgs](https://github.com/NixOS/nixpkgs/blob/23.11/doc/module-system/module-system.chapter.md)

Because the documentation for Nixpkgs' module system is lacking, it directly recommends reading another writing guide specifically for NixOS module system, which is clearer but might still be challenging for newcomers:

- [Writing NixOS Modules - Nixpkgs](https://github.com/NixOS/nixpkgs/blob/nixos-23.11/nixos/doc/manual/development/writing-modules.chapter.md)

In summary, the module system is implemented by Nixpkgs and is not part of the Nix package manager. Therefore, its documentation is not included in the Nix package manager's documentation. Additionally, both NixOS and Home Manager are based on Nixpkg's module system implementation.

---
# Testing

## References

- [Integration testing with NixOS virtual machines - nix.dev](https://nix.dev/tutorials/nixos/integration-testing-using-virtual-machines.html)
- [NixOS Testing library](https://wiki.nixos.org/wiki/NixOS_Testing_library)
- [Testing within NixOS - NixOS Manual](https://nixos.org/manual/nixos/stable/index.html#sec-nixos-tests)
- [Testers - Nixpkgs Manual](https://nixos.org/manual/nixpkgs/unstable/#chap-testers)
- [Unveiling the Power of the NixOS Integration Test Driver (Part 1)](https://nixcademy.com/2023/10/24/nixos-integration-tests/)
- [Unveiling the Power of the NixOS Integration Test Driver (Part 2)](https://nixcademy.com/2023/12/01/nixos-integration-tests-part-2/)
- [nix flake check - Nix Reference Manual](https://nixos.org/manual/nix/stable/command-ref/new-cli/nix3-flake-check)

