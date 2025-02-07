add#nixos #nixflakes #homemanager #Nix 
# Introduction to Nix & NixOS

Nix is a **declarative package manager** that enables users to declare the desired system state in configuration files (declarative configuration), and it takes responsibility for achieving that state.
	In simple terms, "declarative configuration" means that users only need to declare the desired outcome. For instance, if you declare that you want to replace the i3 window manager with sway, Nix will assist you in achieving that goal. You don't have to worry about the underlying details, such as which packages sway requires for installation, which -3-related packages need to be uninstalled, or the necessary adjustments to system configuration and environment variables with for sway. Nix *automatically* handles these details for the user (provided that the Nix packages related to sway and i3 are properly designed).

NixOS, a Linux distro built on top of the Nix package manager, can be described as "OS as Code". It employs declarative Nix configuration files to describe the entire state of the operating system.

An operating system consists of various software packages, configuration files, and text/binary data, all of which represent the current state of the system. Declarative configuration can manage only the static portion of this state. Dynamic data, such as `PostgreSQL`, `MySQL`, or `MongoDB` data, cannot be effectively managed through declarative configuration (it is not feasible to delete all new PostgreSQL data that is not declared in the configuration during each deployment). Therefore, **NixOS primarily focuses on managing the status portion of the system state in a declarative manner.**

Dynamic data, along with the contents in the user's home directory, remain unaffected by NixOS when rolling back to a previous generation.

Although we cannot achieve complete system reproducability, the `/home` directory, being an important user directory, contains many necessary configuration files - [Dotfiles](https://wiki.archlinux.org/title/Dotfiles). A significant community project called [home-manager](https://github.com/nix-community/home-manager) is designed to manage user-level packages and configuration files within the user's home directory. 

Due to Nix's features, such as being declarative and reproducible, Nix is not limited to managing desktop environments but is also extensively used for managing development environments, compilation environments, cloud virtual machines and container image construction. [NixOps](https://github.com/NixOS/nixops) (an official Nix project) and [colmena](https://github.com/zhaofengli/colmena) (a community project) are both operational tools based on Nix. 
## Why NixOS?

I first learned about the Nix package manager several years ago. It utilizes the Nix language to describe system configuration. NixOS, the Linux distribution built on top of it, allows for rolling back the system to any previous state (although only the state declared in Nix configuration files can be rolled back). While it sounded impressive, I found it troublesome to learn a new language and write code to install packages, so I didn't pursue it at the time.

However, I recently encountered numerous environmental issues while using EndeavourOS, and resolving them consumed a significant amount of my energy, leaving me exhausted. Upon careful consideration, I realized that the lack of version control and rollback mechanisms in EndeavourOS prevented me from restoring the system when problems arose. 

That's when I decided to switch to NixOS. 

NixOS has exceeded my expectations. The most astonishing aspect is that I can now restore my entire i3 environment and all my commonly used packages on a fresh NixOS host with just one command `sudo nixos-rebuld switch --flake .` 

The rollback capability and reproducability of NixOS has instilled a great deal of confidence in me -- I no longer fear breaking the system. I've even ventured into experimenting with new things on NixOS, such as the **hyprland compositor**. Previously, on EndeavourOS, I wouldn't have dared to tinker with such novel compositors, as any system mishaps would have entailed significant manual troubleshooting using various workarounds.

As I get more and more involved with NixOS and Nix, I find it also very suitable for synchronously managing the configuration of multiple hosts. Currently, my personal [nix-config](https://github.com/ryan4yin/nix-config) synchronously manages the configuration of many hosts:

- Desktop Computers
	- 1 Macbook Pro 2020 (Intel amd64)
	- 1 Macbook Pro 2022 (M2 aarch64)
	- 1 NixOS Desktop PC (amd64)
- Servers
	- 3 NixOS Virtual Machines (amd64)
	- Several development boards for aarch64 and riscv64.

The development environment on three desktops computers is managed by Home Manager, the main configuration is completely shared, and the configuration method modified on any host can be seamlessly synchronzied to other hosts through Git.

Nix almost completely shielded me from the differences between OS and architecture at the bottom of the three machines, and the experience was very smooth!
# Advantages & Disadvantages of NixOS
## Advantages of NixOS

- **Declarative Configuration**, **OS as Code**
	- NixOS uses declarative configuration to manage the entire system environment. These configurations can be managed directly with Git, allowing the system to be restored to any historical state as long as the configuration files are preserved (provided the desired states are declared in the Nix configuration).
	- Nix Flakes further enhance reproducability utilizing a `flake.lock` version lock file, which records the data source addresses, hash values, and other relevant information for all dependencies. This design greatly improves Nix's reproducability and ensures consistent build results. It draws inspiration for package management designs in programming languages like Cargo and npm.

- **Highly Convenient System Customization Capability**
	- With just a few configuration changes, various components of the system can be easily replaced. Nix encapsulates the underlying complex operations within Nix packages, providing users with a concise set of declarative parameters.
	- Modifications are safe and switching between different desktop environments (such as GNOME, KDE, i3 and sway) is straightforward, with minimal pitfalls.

- **Rollback Capability**
	- It is possible to roll back to any previous system state, and NixOS even includes all old versions in the boot options by default, ensuring the ability to easily revert changes. Consequently, Nix is regarded as one of the most stable package management approaches.

- **No Dependency Conflict Issues**
	- Each software package in Nix has a unique hash, which is incorporated into its installation path, allowing multiple versions to coexist.

- **The Community is Active, with a Diverse Range of Third-Party Projects**
	- The official package repository, nixpkgs, has numerous contributors, and many people share their Nix configurations. Exploring the NixOS ecosystem is an exciting experience, akin to discovering a new continent.
## Disadvantages of NixOS

- **High Learning Curve**
	- Achieving complete reproducability and avoiding pitfalls with improper usage requires learning about Nix's entire design and managing the system declaratively, rather than blindly using commands like `nix-env -i` (similar to `apt-get install`).

- **Disorganized Documentation**
	- Currently, Nix Flakes remains an *experimental feature*, and there is limited documentation specifically focused on it. Most Nix community documentation primarily covers the classic `/etc/nixos/configuration.nix`. If you want to start learning directly from Nix Flakes (`flake.nix`), you need to refer to a significant amount of outdated documentation and extract the relevant information. Additionally, some core features of Nix, such as `imports` and the Nixpkgs Module System, lack detailed official documentation, requiring resorting to source code analysis. 

- **Increased Disk Space Usage**
	- To ensure the ability to roll back the system at any time, Nix retains all historical environments by default, resulting in increased disk space usage.
	- While this additional space usage may not be a concern on desktop computers, it can become problematic on resource-constrained cloud servers.

- **Obscure Error Messages**
	- Due to the [complex merging algorithm](https://discourse.nixos.org/t/best-resources-for-learning-about-the-nixos-module-system/1177/4) of the [Nixpkgs module system](https://nixos-and-flakes.thiscute.world/other-usage-of-flakes/module-system), NixOS error messages are quite poor. In many cases, regardless of whether you add `--show-trace`, it will only tell you that there is an error in the code (the most common and confusing error is [Infinite recursion encountered](https://discourse.nixos.org/t/infinite-recursion-encountered-by-making-module-configurable/23508/2)) but where exactly is the error? The type system says it doesn't know, so you have to find it for yourself. In my experience, **the simplest and most effective way to deal with these meaningless error messages is to use a "binary search" to gradually restore the code.**
	- This problem is probably the biggest pain point of NixOS at the moment.

- **More Complex Underlying Implementation**:
	- Nix's declarative abstraction introduces additional complexity in the underlying code compared to similar code in traditional imperative tools.
	- This complexity increases implementation difficulty and makes it more challenging to make custom modifications at the lower level. However, this burden primarily falls on Nix package maintainers, as regular users have limited exposure to the underlying complexities, reducing their burden.
## Summary

Overall, I believe NixOS is suitable for developers with a certain level of Linux usage experience and programming knowledge who desire greater control over their systems. 

I do not recommend newcomers without any Linux usage experience to dive directly into NixOS, as it may lead to a frustrating journey.
# Installation

Nix can be installed in various ways:

1. As a package manager on macOS, Linux, or WSL.
2. As the system environment manager on NixOS, a Linux distribution that utilizes Nix for system management.

This book primarily focuses on the usage of NixOS and Flakes. Therefore, we will skip content that pertains solely to Nix(such as installation on macOS, Linux, or WSL).

The installation process of NixOS is straightforward, but we won't delve into the specifics here. For more information, please visit the official download site at [https://nixos.org/download.html](https://nixos.org/download.html).

> If you're using macOS, [ryan4yin/nix-darwin-kickstarter](https://github.com/ryan4yin/nix-darwin-kickstarter) may be a good starting point for you, you can learn how to use Nix with this book and take nix-darwin-kickstarter as a start point to build your own Nix configuration.
# Basics of the Nix Language

The Nix language is essential for declaring configurations to be built by Nix. To fully enjoy the benefits of NixOS and Flakes, it is necessary to grasp the fundamentals of this language. 

The Nix language is a straightforward functional language. If you have some programming experience, it should take you less than 2 hours to grasp the basics.

The community has already made a lot of good resources and language tutorials, so I won't reinvent the wheel. To get started, I recommend reading the following resources for a quick introduction to the Nix language:

1. [**Nix Language Basics - nix.dev**](https://nix.dev/tutorials/first-steps/nix-language): This tutorial provides a comprehensive overview of the basics of the Nix language, recommended for beginners.
2. [**A tour of Nix**](https://nixcloud.io/tour/?id=introduction/nix): An online interactive tutorial focuses on programming language constructs and how Nix can be algorithmically used to solve problems.
3. [**Nix Language - Nix Reference Manual**](https://nixos.org/manual/nix/stable/language/): The official documentation of the Nix language.
    1. nix.dev and other user-friendly tutorials are suitable for starter reading only, and **neither of them fully introduces the full syntax of Nix**. If you encounter a new syntax that you have not come across before, please refer to this official document.
4. [https://noogle.dev/](https://noogle.dev/) is a Nix function library search engine that can help you quickly find the functions you need and their usage, which is very practical.

It's okay to have a rough impression of the syntax for now. You can come back to review the syntax when you find something you don't understand later.
# Get Started with NixOS

Now that we have learned the basics of the Nix language, we can start using it to configure our NixOS system. The default configuration file for NixOS is located at `/etc/nixos/configuration.nix`. This file contains all the declarative configuration for the system, including settings for the time zone, language, keyboard layout, network, users, file system and boot options.

To modify the system in a repdroducable manner (which is highly recommended), we need to manually edit the `/etc/nixos/configuration.nix` file and then execute `sudo nixos-rebuild switch` to apply the modified configuration. This command generates a new system environment based on the modified configuration file, sets the new environment as the default one, and preserves the previous environment in the boot options of grub/systemd-boot. This ensures that we can always roll back to the old environment even if the new one fails to start. 

While `/etc/nixos/configuration.nix` is the classic method for configuring NixOS, it relies on data sources configured by `nix-channel` and lacks a version-locking mechanism, making it challenging to ensure the reproducibility of the system. A better approach is to use Flakes, which provides reproducibility and facilitates configuration management. 

In this section, we will first learn how to manage NixOS using the classic method (`/etc/nixos/configuration.nix`), and then we will explore the more advanced Flakes.

---

## Configuring the System using `/etc/nixos/configuration.nix`

The `/etc/nixos/configuration.nix` file is the default and classic method for configuring NixOS. While it lacks some of the advanced features of Flakes, it is still widely used and provides flexibility in system configuration.

To illustrate how to use `/etc/nixos/configuration.nix`, let's consider an example where we enable SSH and add a user named `ryan` to the system. We can achieve this by adding the following content to `/etc/nixos/configuration.nix`:

```json
# Edit this configuration file to define what should be installed on
# your system.  Help is available in the configuration.nix(5) man page
# and in the NixOS manual (accessible by running ‘nixos-help’).
{ config, pkgs, ... }:

{
  imports =
    [ # Include the results of the hardware scan.
      ./hardware-configuration.nix
    ];

  # Omit previous configuration settings...

  # Add user 'ryan'
  users.users.ryan = {
    isNormalUser = true;
    description = "ryan";
    extraGroups = [ "networkmanager" "wheel" ];
    openssh.authorizedKeys.keys = [
        # Replace with your own public key
        "ssh-ed25519 <some-public-key> ryan@ryan-pc"
    ];
    packages = with pkgs; [
      firefox
    #  thunderbird
    ];
  };

  # Enable the OpenSSH daemon.
  services.openssh = {
    enable = true;
    settings = {
      X11Forwarding = true;
      PermitRootLogin = "no"; # disable root login
      PasswordAuthentication = false; # disable password login
    };
    openFirewall = true;
  };

  # Omit the rest of the configuration...
}
```

In this configuration, we declare our intention to enable the openssh service, add an SSH public key for the user 'ryan', and disable password login.

To deploy the modified configuration, run `sudo nix-os rebuild switch`. This command will apply the changes, generate a new system environment, and set it as the default. You can now log in to the system using SSH with the configured SSH keys. 

> You can always try to add `--show-trace --print-built-logs --verbose` to the `nixos-rebuild` command to get the detailed error message if you encounter any errors during the deployment.

Remember that any reproducible changes to the system can be made by modifying the `/etc/nixos/configuration.nix` file and deploying the changes with `sudo nixos-rebuild switch`.

To find configuration options and documentation:

- Use search engines like Google, e.g. search for `Chrome NixOS` to find NixOS-related information about Chrome. The NixOS Wiki and the source code of Nixpkgs are usually among the top results.
- Utilize the [NixOS Options Search](https://search.nixos.org/options) to search for keywords.
- Refer to the [Configuration section](https://nixos.org/manual/nixos/unstable/index.html#ch-configuration) in the NixOS Manual for system-level configuration documentation.
- Search for keywords directly in the source code of [nixpkgs](https://github.com/NixOS/nixpkgs) on GitHub.
# Introduction to Flakes

The flakes experimental feature is a major development for Nix, it introduces a policy for managing dependencies between Nix expression, it improves reproducibility, composability and usability in the Nix ecosystem. Although it's still an experimental feature, flakes have been widely used by the Nix community. 

Flakes is one of the most significant changes the nix project has ever seen.

In simple terms, if you've worked with some JavaScript/Rust/Go/Python, you should be familiar with files like `package.json`/`go.mod`/`Cargo.toml`/`pyproject.toml`. In these programming languages, these files are used to describe the dependencies between software packages and how to build projects.

Similarly, the package managers in the programming languages also use files like `package-lock.json`/`go.sum`/`Cargo.lock`/`poetry.lock` to lock the versions of dependencies, ensuring the reproducibility of projects.

Flakes borrow ideas from these package managers to enhance the reproducibility, composability, and usability of the Nix ecosystem. 

Flakes introduce `flake.nix`, similar to `package.json`, to describe the dependencies between Nix packages and how to build projects. Additionally, it provides `flake.lock`, akin to `package-lock.json`, to lock the version of dependencies, ensuring project reproducibility.

On the other hand, Flakes experimental features did not break Nix's original design at the user level. The two new files `flake.nix`/`flake.lock` introduced by Flakes are just a wrapper for other Nix configurations. In the following chapters, we will see that Flakes features provide a new and more convenient way to manage the dependencies between Nix expressions based on Nix's original design.
## A Word of Caution about Flakes

The benefits of Flakes are evident, and the entire NixOS community has embraced it wholeheartedly. Currently, more than half of the users utilize Flakes, providing assurance that Flakes will not be deprecated.

However, it is important to note that **Flakes is still an experimental feature**. Some issues persists, and there is the possibility of introducing breaking changes during the stabilization process. The extent of these breaking changes remains uncertain. 

Overall, I strongly recommend everyone to use Flakes, especially since this book revolves around NixOS and Flakes. However, it's crucial to be prepared for potential problems that may arise due to forthcoming breaking changes. 

---

## When Will Flakes Be Stabilized?

I delved into some details regarding Flakes:

- [[RFC 0136] A Plan to Stabilize Flakes and the New CLI Incrementally](https://github.com/NixOS/rfcs/pull/136): A plan to incrementally stabilize Flakes and the new CLI, merged.
- [CLI stabilization effort](https://github.com/NixOS/nix/issues/7701): An issue tracking the progress of the New CLI stabilization effort.
- [Why Are Flakes Still Experimental? - NixOS Discourse](https://discourse.nixos.org/t/why-are-flakes-still-experimental/29317): A post discussing why Flakes are still considered experimental.
- [Flakes Are Such an Obviously Good Thing - Graham Christensen](https://grahamc.com/blog/flakes-are-an-obviously-good-thing/): An article emphasizing the advantages of Flakes while suggesting areas for improvement in its design and development process.
- [teaching Nix 3 CLI and Flakes #281 - nix.dev](https://github.com/NixOS/nix.dev/issues/281): An issue about "Teaching Nix 3 CLI and Flakes" in nix.dev, and the conclusion is that we should not promote unstable features in nix.dev.
- [Draft: 1-year Roadmap - NixOS Foundation](https://nixos-foundation.notion.site/1-year-roadmap-0dc5c2ec265a477ea65c549cd5e568a9): A roadmap provided by the NixOS Foundation, which includes plans regarding the stabilization of Flakes.

After reviewing these resources, it seems that Flakes may be(or may not...) stabilized within two years, possibly accompanied by some breaking changes.

---
## The New CLI and the Classic CLI

Nix introduced two experimental features, `nix-command` and `flakes`, in the year 2020. These features bring forth a new command-line interface, (referred to as the New CLI), a standardized Nix package structure definition (known as the Flakes feature), and features like `flake.lock`, similar to version lock files in cargo/npm. Despite being experimental as of February 1, 2024, these features have gained widespread adoption within the Nix community due to their significant enhancement of Nix capabilities.

The current Nix New CLI (the `nix-command` experimental feature) is tightly coupled with the Flakes experimental feature. While there are ongoing efforts to explicitly separate them, using Flakes essentially requires the use of the New CLI. In this book, serving as a beginner's guide to NixOS and Flakes, it is necessary to introduce the differences between the New CLI, which Flakes relies on, and the Old CLI.

Here, we list the old Nix CLI and related concepts that are no longer needed when using the New CLI and Flakes (`nix-command` and `flakes`). When researching, you can replace them with the corresponding New CLI commands (except for `nix-collect-garbage`, as there is currently no alternative for this command).

1. `nix-channel`: `nix-channel` manages software package versions through stable/unstable/test channels, similar to other package management tools such as apt/yum/pacman.
	1. In Flakes, the functionality of `nix-channel` is entirely replaced by the `inputs` section in `flake.nix`.
2. `nix-env`: `nix-env` is a core command line tool for classic Nix used to manage software packages in the user environment.
	1. It install packages from the data sources added by `nix-channel`, causing the installed packages's version to be influenced by the channel. Packages installed with `nix-env` are not automatically recorded in Nix's declarative configuration and are completely independent of its control, making them challenging to reproduce on other machines. Therefore, it is not recommended to use this command directly. 
	2. The corresponding command in the New CLI is `nix-profile`. Personally, I don't recommend it for beginners.
3. `nix-shell`: `nix-shell` creates a temporary shell environment, which is useful for development and testing. 
	1. New CLI: This tool is divided into three sub-commands: `nix develop`, `nix shell`, and `nix run`. We will discuss these three commands in detail in the "[Development](https://nixos-and-flakes.thiscute.world/development/intro)" chapter.
4. `nix-build`: `nix-build` builds Nix packages and place the build results in `/nix/store`, but it does not record them in Nix's declarative configuration.
	1. New CLI: `nix-build` is replaced by `nix build`.
5. `nix-collect-garbage`: Garbage collection used to clean up unused Store Objects in `/nix/store`.
	1. There is a similar command in the New CLI, `nix store gc --debug`, but it does not clean the profile generations, so there is currently no alternative for this command.
6. And other less commonly used commands are not listed here.
	1. You can refer to the detailed command comparison list in [Try to explain nix commands](https://qiita.com/Sumi-Sumi/items/6de9ee7aab10bc0dbead?_x_tr_sl=auto&_x_tr_tl=en&_x_tr_hl=en).
# Enabling NixOS with Flakes

Compared to the default configuration method currently used in NixOS, Flakes offers better reproducibility. Its clear package structure definition inherently supports dependencies on other Git repositories, facilitating code sharing. Therefore, this book suggests using Flakes to manage system configurations.

This section describes how to use Flakes to manage NixOS system configuration, *and you don't need to know anything about Flakes in advance*.

---
## Enabling Flakes Support for NixOS

Currently, Flakes is still an experimental feature and not enabled by default. We need to manually modify the `/etc/nixos/configuration.nix` file to enable the Flakes feature and the accompanying new nix-command line tool:

```json
{ config, pkgs, ... }:

{
  imports = [
    # Include the results of the hardware scan.
    ./hardware-configuration.nix
  ];

  # ......

  # Enable the Flakes feature and the accompanying new nix command-line tool
  nix.settings.experimental-features = [ "nix-command" "flakes" ];
  environment.systemPackages = with pkgs; [
    # Flakes clones its dependencies through the git command,
    # so git must be installed first
    git
    vim
    wget
    curl
  ];
  # Set the default editor to vim
  environment.variables.EDITOR = "vim";

  # ......
}
```

After making these changes, run `sudo nixos-rebuild switch` to apply the modifications. Then, you can use the Flakes feature to manage your system configuration.

The new nix-command-line tool offers some convenient features. For example, you can now use the `nix repl` command to open a nix interactive environment. If you're interested, you can use it to review and test all the Nix syntax you've learned before. 

--- 
## Switching System Configuration to `flake.nix`

After enabling the Flakes feature, the `sudo nixos-rebuild switch` command will prioritize reading the `/etc/nixos/flake.nix` file, and if it's not found, will attempt to use `/etc/nixos/configuration.nix`.

You can start by using the official templates to learn how to write a flake. First, check what templates are available. 

```
nix flake show templates
```

Among them, the `templates#full` template demonstrates all possible usage. Take a look at its content:

```
nix flake init -t templates#full
cat flake.nix
```

Referencing this template, create the file `/etc/nixos/flake.nix` and write the configuration content. All subsequent modifications will be taken over by Nix flakes. Here's an example of the content:

```json
{
  description = "A simple NixOS flake";

  inputs = {
    # NixOS official package source, using the nixos-23.11 branch here
    nixpkgs.url = "github:NixOS/nixpkgs/nixos-23.11";
  };

  outputs = { self, nixpkgs, ... }@inputs: {
    # Please replace my-nixos with your hostname
    nixosConfigurations.my-nixos = nixpkgs.lib.nixosSystem {
      system = "x86_64-linux";
      modules = [
        # Import the previous configuration.nix we used,
        # so the old configuration file still takes effect
        ./configuration.nix
      ];
    };
  };
}
```

Here we defined a system named `my-nixos`, with it's configuration file located at `/etc/nixos/` as `./configuration.nix`. This means we are still using the old configuration. 

Now, when you execute `sudo nixos-rebuild switch` to apply the configuration, the system should not change at all because we have simply switched to using Nix Flakes, and the configuration content remains consistent with before. 

After the switch, we can manage the system through the Flakes feature.

Currently, our flake includes these files:

- `/etc/nixos/flake.nix`: The entrypoint for the flake, which is recognized and deployed when `sudo nixos-rebuild switch` is executed. 
- `/etc/nixos/flake.lock`: The automatically generated version lock file, which records the data sources, hash values, and version numbers of all inputs in the entire flake, ensuring system reproducibility.
- `/etc/nixos/configuration.nix`: This is our previous configuration file, which is imported as a module in `flake.nix`. Currently, all system configurations are written in this file.
- `/etc/nixos/hardware-configuration.nix`: This is the system hardware configuration file, generated by NixOS, which describes the system's hardware information.

---
## Conclusion

Up to this point, we have merely added a very simple configuration file, `/etc/nixos/flake.nix`, which has merely been a thin wrapper around `/etc/nixos/configuration.nix`, offering no new functionality and introducing no disruptive changes.

In the content of the book that follows, we will learn about the structure and functionality of `flake.nix`, and gradually see the benefits that such a wrapper can bring.

> [!NOTE]
> > Note: The configuration management method described in this book is NOT "Everything in a single file". It is recommended to categorize configuration content into different nix files, then introduce these configuration files in the `modules` list of `flake.nix`, and manage them with Git.
> > 
> > The benefits of this approach are better organization of configuration files and improved maintainability of the configuration. The section [Modularizing NixOS Configuration](https://nixos-and-flakes.thiscute.world/nixos-with-flakes/modularize-the-configuration) will explain in detail how to modularize your NixOS configuration, and [Other Useful Tips - Managing NixOS Configuration with Git](https://nixos-and-flakes.thiscute.world/nixos-with-flakes/other-useful-tips) will introduce several best practices for managing NixOS configuration with Git.
# `flake.nix` Configuration Explained

Above, we created a `flake.nix` file to manage system configurations, but you might still be unclear about its structure. Let's explain the content of this file in detail. 

---
## 1. Flake Inputs

First, let's look at the `inputs` attribute. It is an attribute set that defines all the dependencies of this flake. These dependencies will be passed as arguments to the `outputs` function after they are fetched:

```json
{
  inputs = {
    # NixOS Official package source, using the NixOS 24.05 branch here
    nixpkgs.url = "github:NixOS/nixpkgs/nixos-24.05";
  };

  outputs = { self, nixpkgs, ... }@inputs: {
    # Omitting previous configurations......
  };
}
```

Dependencies in `inputs` has many types and definitions. It can be another flake, a regular Git repository, or a local path. The section [Other Usage of Flakes - Flake Inputs](https://nixos-and-flakes.thiscute.world/other-usage-of-flakes/inputs) describes common types of dependencies and their definitions in detail.

Here we only define a dependency named `nixpkgs`, which is the most common way to reference in a flak, i.e. `github:owner/name/reference`. The `reference` here can be a branch name, commit-id, or tag.

After `nixpkgs` is defined in `inputs`, you can use it in the parameters of the subsequent `outputs` function, which is exactly what our example does.
## 2. Flake Outputs

Now let's look at `outputs`. It is a function that takes the dependencies from `inputs` as its parameters, and its return value is an attribute set, which represents the build results of the flake. 

```json
{
  description = "A simple NixOS Flake";

  inputs = {
    nixpkgs.url = "github:NixOS/nixpkgs/nixos-24.05"}
  };

  outputs = { self, nixpkgs, ... }@inputs: {
    nixosConfigurations.nixos = nixpkgs.lib.nixosSystem {
      system = "x86_64-linux";
      modules = [
        ./configuration.nix
      ];
    };
  };
}
```

Flakes can have various purposes and can have different types of outputs. The section [Flake Outputs](https://nixos-and-flakes.thiscute.world/other-usage-of-flakes/outputs) provides a more detailed introduction. Here, we are only using the `nixosConfigurations` type of outputs, which is used to configure NixOS systems.

When we run the `sudo nixos-rebuild switch` command, it looks for the `nixosConfigurations.nixos` attribute (where `nixos` will be the hostname of your current system) in the attribute set returned by the `outputs` function of `/etc/nixos/flake.nix` and uses the definition there to configure your NixOS system.

Actually, we can also customize the location of the flake and the name of the NixOS configuration instead of using defaults. This can be done by adding the `--flake` parameter to the `nixos-rebuild` command. Here's an example:

```
sudo nixos-rebuild switch --flake /path/to/your/flake#your=hostname
```

A brief explanation of the `--flake /path/to/your/flake#your-hostname` parameter:

1. `path/to/your/flake` is the location of the target flake. The default path is `etc/nixos/`.
2. `#` is a **separator**, and `your-hostname` is the name of the NixOS configuration. `nixos-rebuild` will default to using the hostname of your current system as the configuration name to look for.

You can even directly reference a remote GitHub repository as your flake source, for example:

```
sudo nixos-rebuild switch ==flake github:owner/repo#your-hostname
```
## 3. The Special Parameter `self` of the `outputs` Function

Although we have not mentioned it before, all the example code in the previous sections has one more special parameter in the `outputs` function, as we will briefly introduce its purpose here. 

The description of it in the [nix flake - Nix Manual](https://nixos.org/manual/nix/stable/command-ref/new-cli/nix3-flake#flake-inputs) is:

> The special input named `self` refers to the outputs and the source tree of this flake.

This means that `self` is the return value of the current flake's `outputs` function and also the path to the current flake's source code folder (source tree).

We are not using the `self` parameter here, but in some more complex examples (or configurations you may find online) later, you will see the usage of `self`.

> [!NOTE]
> **Note**: You might come across some code where people use `self.outputs` to reference the outputs of the current flake, which is indeed possible. However, the Nix Manual does not provide any explanation for this, and it is considered an internal implementation detail of flakes. It is not recommended to use this in your own code!

## 4. Simple Introduction to `nixpkgs.lib.nixosSystem` Function

**A Flake can depend on other flakes to utilize the features they provide**.

By default, a flake searches for a `flake.nix` file in the root directory of each of its dependencies (i.e. each item in `inputs`) and lazily evaluates their `outputs` function. It then passes the attribute set returned by these functions as arguments to its own `outputs` function, enabling us to use the features provided by the other flakes within our current flake.

More precisely, the evaluation of the `outputs` function for each dependency is lazy. This means that a flake's `outputs` function is only evaluated when it is actually used, thereby avoiding unnecessary calculations and improving efficiency. 

The description above may be a bit confusing, so let's take a look at the process with the `flake.nix` example used in this section. Our `flake.nix` declares that `inputs.nixpkgs` dependency, so that [nixpkgs/flake.nix](https://github.com/NixOS/nixpkgs/tree/nixos-23.11/flake.nix) will be evaluated when we run the `sudo nixos-rebuild switch` command.

From the source code of the Nixpkgs repository, we can see that its flake outputs definition includes the `lib` attribute, and in our example, we use the `lib` attributes `nixosSystem` function to configure our NixOS system:

```json
{
  inputs = {
    nixpkgs.url = "github:NixOS/nixpkgs/nixos-24.05";
  };

  outputs = { self, nixpkgs, ... }@inputs: {
    nixosConfigurations.nixos = nixpkgs.lib.nixosSystem {
      system = "x86_64-linux";
      modules = [
        ./configuration.nix
      ];
    };
  };
}
```

The attribute set following `nixpkgs.lib.nixosSystem` is the function's parameter. We have only set two parameters here:

1. `system`: This is straightforward, it's the system architecture parameter. 
2. `modules`: This is a list of modules, where the actual NixOS system configuration is defined. The `/etc/nixos/configuration.nix` configuration file itself is a Nixpkgs Module, so it can be directly added to the `modules` list for use.

Understanding these basics is sufficient for beginners. Exploring the `nixpkgs.lib.nixosSystem` function in detail requires a grasp of the Nixpkgs module system. Readers who have completed the [Modularizing NixOS Configuration](https://nixos-and-flakes.thiscute.world/nixos-with-flakes/modularize-the-configuration) section can return to [nixpkgs/flake.nix](https://github.com/NixOS/nixpkgs/tree/nixos-23.11/flake.nix) to find the definition of `nixpkgs.lib.nixosSystem`, trace its source code, and study its implementation.
# The Combination Ability of Flakes and Nixpkgs Module System
## Nixpkgs Module Structure Explained

> The detailed workings of this module system will be introduced in the following [Modularizing NixOS Configuration](https://nixos-and-flakes.thiscute.world/nixos-with-flakes/modularize-the-configuration) section. Here, we'll just cover some basic knowledge.

You might be wondering why the `/etc/nixos/configuration.nix` configuration file adheres to the Nixpkgs Module definition and can be referenced directly within the `flake.nix`.

This is because the Nixpkgs repository contains a significant amount of NixOS implementation source code, primarily when written in Nix. To manage and maintain such a large volume of Nix code and to allow users to customize various functions of their NixOS systems, a **modular system for Nix code is essential**.

This modular system for Nix code is also implemented within the Nixpkgs repository and is primarily used for modularizing NixOS system configurations. However, it is also widely used in other contexts, such as nix-darwin and home-manager. Since NixOS is built on this modular system, it is only natural that its configurations files, including `/etc/nixos/configuration.nix`, are Nixpkgs modules.

Before delving into the subsequent content, it's essential to have a basic understanding of how this module system operates. 

Here's a simplified structure of a Nixpkgs Module:

```python
{lib, config, options, pkgs, ...}:
{
  # importing other modules
  imports = [
    # ...
    ./xxx.nix
  ];
  for.bar.enable = true;
  # other package declarations
  # ... 
}
```

The definition is actually a Nix function, and it has five **automatically generated**, **automatically injected, and declaration-free parameters** provided by the module system:

1. `lib`: A built-in function library included with nixpkgs, offering many practical functions for operating Nix expressions.
	- For more information, see [https://nixos.org/manual/nixpkgs/stable/#id-1.4](https://nixos.org/manual/nixpkgs/stable/#id-1.4).
2. `config`: A set of all options' values in the current environment, which will be used extensively in the subsequent section on the module system.
3. `options`: A set of all options defined in all Modules in the current environment.
4. `pkgs`: A collection containing all nixpkgs packages, along with several related utility functions.
	- At the beginner stage, you can consider its default value to be `nixpkgs.legacyPackages."${system}`, and the value of `pkgs` can be customized through the `nixpkgs.pkgs` option.
5. `modulesPath`: A parameter available only in NixOS, which is a path pointing to [nixpkgs/nixos/modules](https://github.com/NixOS/nixpkgs/tree/nixos-23.11/nixos/modules).
	- It is defined in [nixpkgs/nixos/lib/eval-config-minimal.nix#L43](https://github.com/NixOS/nixpkgs/blob/nixos-23.11/nixos/lib/eval-config-minimal.nix#L43).
	- It is typically used to import additional NixOS modules and can be found in most NixOS auto-generated `hardware-configuration.nix` files. 
## Passing Non-Default Parameters to Submodules

If you need to pass other non-default parameters to submodules, you will need to use some special methods to manually specify these non-default parameters.

The Nixpkgs module system provides two ways to pass non-default parameters:

1. The `specialArgs` parameter of the `nixpkgs.lib.nixosSystem` function.
2. Using the `_module.args` option in any module to pass parameters.

The official documentation for these two parameters is buried deep and is vague and hard to understand. If readers are interested, I will include the links here:

1. `specialArgs`: There are scattered mentions related to it in the NixOS Manual and the Nixpkgs Manual.
	- Nixpkgs Manual: [Module System - Nixpkgs](https://github.com/NixOS/nixpkgs/blob/23.11/doc/module-system/module-system.chapter.md)
	- NixOS Manual: [nixpkgs/nixos-23.11/nixos/doc/manual/development/option-types.section.md#L237-L244](https://github.com/NixOS/nixpkgs/blob/nixos-23.11/nixos/doc/manual/development/option-types.section.md?plain=1#L237-L244)
2. `_module.args`: 
	- NixOS Manual: [Appendix A. Configuration Options](https://nixos.org/manual/nixos/stable/options#opt-_module.args)
	- Source Code: [nixpkgs/nixos-23.11/lib/modules.nix - _module.args](https://github.com/NixOS/nixpkgs/blob/nixos-23.11/lib/modules.nix#L122-L184)

In short, `specialArgs` and `_module.args` both require an attribute set as their value, and they serve the same purpose, passing all parameters in the attribute set to all submodules. The difference between them is:

1. The `_module.args` option can be used in any module to pass parameters to each other, which is more flexible than `specialArgs`, which can only be used in the `nixpkgs.lib.nixosSystem` function.
2. `_module.args` is declared within a module, so it must be evaluated after all modules have been evaluated before it can be used. This means that **if you use the parameters passed throguh `_module.args` in `imports = [ ... ];`**, it will result in an `infinite recursion` error. In this case, you must use `specialArgs` instead.

I personally prefer `specialArgs` because it is more straightforward and easier to use, and the naming style of `_xxx` makes it feel like an internal thing that is not suitable for use in user configuration files. 

Suppose you want to pass a certain dependency to a submodule for use. You can use the `specialArgs` parameter to pass the `inputs` to all submodules.

```python
{
  inputs = {
    nixpkgs.url = "github:NixOS/nixpkgs/nixos-24.05";
    another-input.url = "github:username/repo-name/branch-name";
  };

  outputs = inputs@{ self, nixpkgs, another-input, ... }: {
    nixosConfigurations.nixos = nixpkgs.lib.nixosSystem {
      system = "x86_64-linux";
      
      # set all inputs parameters as special arguments for all
      # submodules, so you can directly use all dependencies in inputs
      # in submodules
      specialArgs = { inherit inputs; };
      modules = [
        ./configuration.nix
      ];
    };
  };
}
```

Or you can achieve the same effect using the `_module.args` option:

```python
{
  inputs = {
    nixpkgs.url = "github:NixOS/nixpkgs/nixos-23.11";
    another-input.url = "github:username/repo-name/branch-name";
  };
  outputs = inputs@{ self, nixpkgs, another-input, ... }: {
    nixosConfigurations.my-nixos = nixpkgs.lib.nixosSystem {
      system = "x86_64-linux";
      modules = [
        ./configuration.nix
        {
          # Set all inputs parameters as special arguments for all     submodules,
          # so you can directly use all dependencies in inputs in submodules
          _module.args = { inherit inputs; };
        }
      ];
    };
  };
}
```

Choose one of the two methods above to modify your configuration, and then you can use the `inputs` parameter in `/etc/nixos/configuration.nix`. The module system will automatically match the `inputs` defined in `specialArgs` and inject it into all submodules that require this parameter:

```python
# Nix will match by name and automatically inject the inputs
# from specialArgs/_module.args into the third parameter of this 
# function
{ config, pkgs, inputs, ... }:
{
  # ...
}
```
## Installing System Software from Other Flake Sources

The most common requirement for managing a system is to install software, and we have already seen in the previous section how to install packages from the official nixpkgs repository using `environment.systemPackages`. These packages all come from the official nixpkgs repository.

Now, we will learn how to install software packages from other flake sources, which is much more flexible that installing directly from nixpkgs. The main use case is to install the latest version of a software that is not yet added or updated in Nixpkgs.

Taking the Helix editor as an example, here's how to compile and install the master branch of Helix directly. 

First, add the Helix input data source to `flake.nix`:

```python
{
  inputs = {
    nixpkgs.url = "github:NixOS/nixpkgs/nixos-23.11";

    # helix editor, use the master branch
    helix.url = "github:helix-editor/helix/master";
  };

  outputs = inputs@{ self, nixpkgs, ... }: {
    nixosConfigurations.my-nixos = nixpkgs.lib.nixosSystem {
      system = "x86_64-linux";
      specialArgs = { inherit inputs; };
      modules = [
        ./configuration.nix

        # This module works the same as the `specialArgs` parameter we used above
        # choose one of the two methods to use
        # { _module.args = { inherit inputs; };}
      ];
    };
  };
}
```

Next, you can reference this flake input data source in `configuration.nix`:

```python
{ config, pkgs, inputs, ... }:
{
  # ...
  environment.systemPackages = with pkgs; [
    git
    vim
    wget
    curl
    # Here, the helix package is installed from the helix input data
    # source
    inputs.helix.packages."${pkgs.system}".helix
  ];
  # ...
}
```

Make the necessary changes and deploy with `sudo nixos-rebuild switch`. The deployment will take much longer this time because Nix will compile the entire Helix program from source. 

After deployment, you can directly test and verify the installation using the `hx` command in the terminal.

Additionally, if you just want to try out the latest version of Helix and decide whether to install it on your system later, there is a simpler way to do it in one command (but as mentioned earlier, compiling from source will take a long time):

```
nix run github:helix=editor/helix/master
```

We will go into more detail on the usage of `nix run` in the following section [Usage of the New CLI](https://nixos-and-flakes.thiscute.world/other-usage-of-flakes/the-new-cli).

---
## Leveraging Features from Other Flake Packages

In fact, this is the primary functionality of Flakes - a flake can depend on other flakes, allowing it to utilize the features they provide. it's akin to how we incorporate functionalities from other libraries when writing programs in TypeScript, Go, Rust and other programming languages. 

The example above, using the latest version from the official Helix Flake, illustrates this functionality. Most use cases will be discussed later, and here are a few examples referenced for future mention:

- [Getting Started with Home Manager](https://nixos-and-flakes.thiscute.world/nixos-with-flakes/start-using-home-manager): This introduces the community's Home-Manager as a dependency, enabling direct utilization of the features provided by this Flake.
- [Downgrading or Upgrading Packages](https://nixos-and-flakes.thiscute.world/nixos-with-flakes/downgrade-or-upgrade-packages): Here, different versions of Nixpkgs are introduced as dependencies, allowing for flexible selection of packages from various versions of Nixpkgs.
## More Flakes Tutorials

Up to this point, we have learned how to use Flakes to configure NixOS systems. If you have more questions about Flakes or want to learn more in-depth, please refer directly to the following official/semi-official documents:

- Nix Flakes's official documentation:
    - [Nix flakes - Nix Manual](https://nixos.org/manual/nix/stable/command-ref/new-cli/nix3-flake)
    - [Flakes - nix.dev](https://nix.dev/concepts/flakes)
- A series of tutorials by Eelco Dolstra(The creator of Nix) about Flakes:
    - [Nix Flakes, Part 1: An introduction and tutorial (Eelco Dolstra, 2020)](https://www.tweag.io/blog/2020-05-25-flakes/)
    - [Nix Flakes, Part 2: Evaluation caching (Eelco Dolstra, 2020)](https://www.tweag.io/blog/2020-06-25-eval-cache/)
    - [Nix Flakes, Part 3: Managing NixOS systems (Eelco Dolstra, 2020)](https://www.tweag.io/blog/2020-07-31-nixos-flakes/)
- Other useful documents:
    - [Practical Nix Flakes](https://serokell.io/blog/practical-nix-flakes)
# Getting Started with Home Manager

As mentioned earlier, NixOS can only manage system-level configuration. To manage user-level configuration in the Home directory, we need to install Home Manager. 

According to the official [Home Manager Manual](https://nix-community.github.io/home-manager/index.xhtml), to install Home Manager as a module of NixOS, we first need to create `/etc/nixos/home.nix`. Here's an example of it's contents:

```python
{ config, pkgs, ... }:

{
  # TODO please change the username & home directory to your own
  home.username = "ryan";
  home.homeDirectory = "/home/ryan";

  # link the configuration file in current directory to the specified location in home directory
  # home.file.".config/i3/wallpaper.jpg".source = ./wallpaper.jpg;

  # link all files in `./scripts` to `~/.config/i3/scripts`
  # home.file.".config/i3/scripts" = {
  #   source = ./scripts;
  #   recursive = true;   # link recursively
  #   executable = true;  # make all files executable
  # };

  # encode the file content in nix configuration file directly
  # home.file.".xxx".text = ''
  #     xxx
  # '';

  # set cursor size and dpi for 4k monitor
  xresources.properties = {
    "Xcursor.size" = 16;
    "Xft.dpi" = 172;
  };

  # Packages that should be installed to the user profile.
  home.packages = with pkgs; [
    # here is some command line tools I use frequently
    # feel free to add your own or remove some of them

    neofetch
    nnn # terminal file manager

    # archives
    zip
    xz
    unzip
    p7zip

    # utils
    ripgrep # recursively searches directories for a regex pattern
    jq # A lightweight and flexible command-line JSON processor
    yq-go # yaml processor https://github.com/mikefarah/yq
    eza # A modern replacement for ‘ls’
    fzf # A command-line fuzzy finder

    # networking tools
    mtr # A network diagnostic tool
    iperf3
    dnsutils  # `dig` + `nslookup`
    ldns # replacement of `dig`, it provide the command `drill`
    aria2 # A lightweight multi-protocol & multi-source command-line download utility
    socat # replacement of openbsd-netcat
    nmap # A utility for network discovery and security auditing
    ipcalc  # it is a calculator for the IPv4/v6 addresses

    # misc
    cowsay
    file
    which
    tree
    gnused
    gnutar
    gawk
    zstd
    gnupg

    # nix related
    #
    # it provides the command `nom` works just like `nix`
    # with more details log output
    nix-output-monitor

    # productivity
    hugo # static site generator
    glow # markdown previewer in terminal

    btop  # replacement of htop/nmon
    iotop # io monitoring
    iftop # network monitoring

    # system call monitoring
    strace # system call monitoring
    ltrace # library call monitoring
    lsof # list open files

    # system tools
    sysstat
    lm_sensors # for `sensors` command
    ethtool
    pciutils # lspci
    usbutils # lsusb
  ];

  # basic configuration of git, please change to your own
  programs.git = {
    enable = true;
    userName = "Ryan Yin";
    userEmail = "xiaoyin_c@qq.com";
  };

  # starship - an customizable prompt for any shell
  programs.starship = {
    enable = true;
    # custom settings
    settings = {
      add_newline = false;
      aws.disabled = true;
      gcloud.disabled = true;
      line_break.disabled = true;
    };
  };

  # alacritty - a cross-platform, GPU-accelerated terminal emulator
  programs.alacritty = {
    enable = true;
    # custom settings
    settings = {
      env.TERM = "xterm-256color";
      font = {
        size = 12;
        draw_bold_text_with_bright_colors = true;
      };
      scrolling.multiplier = 5;
      selection.save_to_clipboard = true;
    };
  };

  programs.bash = {
    enable = true;
    enableCompletion = true;
    # TODO add your custom bashrc here
    bashrcExtra = ''
      export PATH="$PATH:$HOME/bin:$HOME/.local/bin:$HOME/go/bin"
    '';

    # set some aliases, feel free to add more or remove some
    shellAliases = {
      k = "kubectl";
      urldecode = "python3 -c 'import sys, urllib.parse as ul; print(ul.unquote_plus(sys.stdin.read()))'";
      urlencode = "python3 -c 'import sys, urllib.parse as ul; print(ul.quote_plus(sys.stdin.read()))'";
    };
  };

  # This value determines the home Manager release that your
  # configuration is compatible with. This helps avoid breakage
  # when a new home Manager release introduces backwards
  # incompatible changes.
  #
  # You can update home Manager without changing this value. See
  # the home Manager release notes for a list of state version
  # changes in each release.
  home.stateVersion = "23.11";

  # Let home Manager install and manage itself.
  programs.home-manager.enable = true;
}
```

After adding `/etc/nixos/home.nix`, you need to import this new configuration file in `/etc/nixos/flake.nix` to make use of it, use the following command to generate an example in the current folder for reference:

```
nix flake new example -t github:nix-community/home-manager#nixos
```

After adjusting the parameters, the content `/etc/nixos/flake.nix` is as follows:

```python
{
  description = "NixOS configuration";

  inputs = {
    nixpkgs.url = "github:nixos/nixpkgs/nixos-23.11";
    # home-manager, used for managing user configuration
    home-manager = {
      url = "github:nix-community/home-manager/release-23.11";
      # The `follows` keyword in inputs is used for inheritance.
      # Here, `inputs.nixpkgs` of home-manager is kept consistent with
      # the `inputs.nixpkgs` of the current flake,
      # to avoid problems caused by different versions of nixpkgs.
      inputs.nixpkgs.follows = "nixpkgs";
    };
  };

  outputs = inputs@{ nixpkgs, home-manager, ... }: {
    nixosConfigurations = {
      # TODO please change the hostname to your own
      my-nixos = nixpkgs.lib.nixosSystem {
        system = "x86_64-linux";
        modules = [
          ./configuration.nix

          # make home-manager as a module of nixos
          # so that home-manager configuration will be deployed automatically when executing `nixos-rebuild switch`
          home-manager.nixosModules.home-manager
          {
            home-manager.useGlobalPkgs = true;
            home-manager.useUserPackages = true;

            # TODO replace ryan with your own username
            home-manager.users.ryan = import ./home.nix;

            # Optionally, use home-manager.extraSpecialArgs to pass arguments to home.nix
          }
        ];
      };
    };
  };
}
```

Then run `sudo nixos-rebuild switch` to apply the configuration, and home-manager will be installed automatically.
	If your system's hostname is not `my-nixos`, you need to modify the name of `nixosConfiguration` in `flake.nix`, or use `--flake /etc/nixos#my-nixos` to specify the configuration name.

After the installation, all user-level packages and configuration can be managed through `/etc/nixos/home.nix`. When running `sudo nixos-rebuild switch`, the configuration of home-manager will be applied automatically. (**It's not necessary to run `home-manager switch` manually**).

To find the options we can use in `home.nix`, refer to the following documents:

- [Home Manager - Appendix A. Configuration Options](https://nix-community.github.io/home-manager/options.xhtml): A list of all options, it is recommended to search for keywords in it.
    - [Home Manager Option Search](https://mipmip.github.io/home-manager-option-search/) is another option search tool with better UI.
- [home-manager](https://github.com/nix-community/home-manager): Some options are not listed in the official documentation, or the documentation is not clear enough, you can directly search and read the corresponding source code in this home-manager repo.

---
## Home Manager vs. NixOS

There are many software packages or configurations that can be set up using either NixOS Modules (`configuration.nix`) or Home Manager (`home.nix`), which brings about a choice dilemma:

**What is the difference between placing software packages or configuration files in NixOS Modules vs. Home Manager, and how should one make a decision?**

First, let's look at the differences: Software packages and configuration files installed via NixOS modules are *global to the entire system*. Global configurations are usually stored in `/etc`, and system-wide installed software is accessible in any user environment.

On the other hand, configurations and software installed via Home Manager will be linked to the respective user's Home directory. The software installed is only available in the corresponding user environment, and it becomes unusable when switched to another user.

Based on these characteristics, the general recommended usage is:

- **NixOS Modules**: Install system core components and other software pacakges or configurations needed by all users.
	- For instance, if you want a software package to continue working when you switch to the root user, or if you want a configuration to apply system-wide, you should install it using NixOS modules.
- **Home Manager**: Use Home Manager for all other configurations and software.

The benefits of this approach are:

1. Software and background services installed at the system level often run with root privileges. Avoiding unnecessary software installations at the system level can reduce the security risks of the system. 
2. Many configurations in Home Manager are universal for NixOS, macOS and other Linux distros. Choosing home manager to install software and configure systems can improve the portability of configurations.
3. If you need multi-user support, software and configurations installed via Home Manager can better isolate different user environments, preventing configuration and software version conflicts between users. 
## How to Use Packages Installed by Home Manager with Privileged Access?

The first thing that comes to mind is to switch to `root`, but then any packages installed by the current user through `home.nix` will be unavailable. Let's take `kubectl` as an example (it's pre-installed via `home.nix`).

```python
# 1. kubectl is available
› kubectl | head
kubectl controls the Kubernetes cluster manager.

 Find more information at: https://kubernetes.io/docs/reference/kubectl/
......

# 2. switch user to `root`
› sudo su

# 3. kubectl is no longer available
> kubectl
Error: nu::shell::external_command

  × External command failed
   ╭─[entry #1:1:1]
 1 │ kubectl
   · ───┬───
   ·    ╰── executable was not found
   ╰────
  help: No such file or directory (os error 2)


/home/ryan/nix-config> exit
```

The solution is to use `sudo` to run the command, which temporarily grants the current user the ability to run the command as a privileged user (`root`):

```
› sudo kubectl
kubectl controls the Kubernetes cluster manager.
...
```
# Modularize the Configuration

At this point, the skeleton of the entire system is configured. The current configuration structure in `/etc/nixos` should be as follows:

```
$ tree
.
├── flake.lock
├── flake.nix
├── home.nix
└── configuration.nix
```

The functions of these four files are:

- `flake.lock`: Automatically generated version-lock file that records all input sources, hash values, and version numbers of the entire flake to ensure reproducibility. 
- `flake.nix`: The entry file that will be recognized and deployed when executing `sudo nixos-rebuild switch`. See [Flakes - NixOS Wiki](https://wiki.nixos.org/wiki/Flakes) for all options of flake.nix.
- `configuration.nix`: Imported as a Nix module in flake.nix, all system-level configuration is currently written here. See [Configuration - NixOS Manual](https://nixos.org/manual/nixos/unstable/index.html#ch-configuration) for all options of configuration.nix.
- `home.nix`: Imported by home-manager as the configuration of the user `jason` in flake.nix, containing all of `jason`'s configuration and managing `jason`'s home folder. See [Appendix A. Configuration Options - Home-Manager](https://nix-community.github.io/home-manager/options.xhtml) for all options of home.nix.

By modifying these files, you can declaratively change the system and home directory status.

However, as the configuration grows, relying solely on `configuration.nix` and `home.nix` can lead to *bloated and difficult to maintain files*. A better solution is to use the Nix module system to split the configuration into multiple Nix modules and write them in a classified manner. 

The Nix module system provides a parameter, `imports`, which accepts a list of `.nix` files and merges all the configuration defined in these files into the current Nix module. Note that `imports` will not simply overwrite duplicate configuration but handle it more reasonably. For example, if `program.packages = [ ... ]`
 is defined in multiple modules, then `imports` will merge all `program.packages` defined in all Nix modules into one list. Attribute sets can also be merged correctly. The specific behavior can be explored by yourself.
 
> I only found a description of `imports` in [Nixpkgs-Unstable Official Manual - evalModules Parameters](https://nixos.org/manual/nixpkgs/unstable/#module-system-lib-evalModules-parameters): `A list of modules. These are merged together to form the final configuration.` It's a bit ambiguous...

With the help of `imports`, we can split `home.nix` and `configuration.nix` into multiple Nix modules defined in different `.nix` files. Let's look at an example of `packages.nix`:

```python
{
  config,
  pkgs,
  ...
}: {
  imports = [
    (import ./special-fonts-1.nix {inherit config pkgs;}) # (1)
    ./special-fonts-2.nix # (2)
  ];

  fontconfig.enable = true;
}
```

This module loads two other modules in the imports section, namely `special-fonts-1.nix` and `special-fonts-2.nix`. Both files are modules themselves and look similar to this.

```
{ config, pkgs, ...}: {
    # Configuration stuff ...
}
```

Both import statements above are equivalent in the parameters they receive:

- Statement `(1)` imports the function in `special-fonts-1.nix` and calls it by passing `{config = config; pkgs = pkgs}`. Basically using the return value of the call (another partial configuration [attribute set]) inside the `imports` list.
- Statement `(2)` defines a path to the module, whose function Nix will load *automatically* when assembling the configuration `config`. It will pass matching arguments from the function in `packages.nix` to the loaded function in `special-fonts-2.nix` which results in `import ./special-fonts-2.nix {config = config; pkgs = pkgs}`.

Here is a nice starter example of modularizing the configuration, highly recommended:

- [Misterio77/nix-starter-configs](https://github.com/Misterio77/nix-starter-configs)

A more complicated example, [ryan4yin/nix-config/i3-kickstarter](https://github.com/ryan4yin/nix-config/tree/i3-kickstarter) is the configuration of my previous NixOS system with the i3 window manager. Its structure is as follows:

```python
├── flake.lock
├── flake.nix
├── home
│   ├── default.nix         # here we import all submodules by imports = [...]
│   ├── fcitx5              # fcitx5 input method's configuration
│   │   ├── default.nix
│   │   └── rime-data-flypy
│   ├── i3                  # i3 window manager's configuration
│   │   ├── config
│   │   ├── default.nix
│   │   ├── i3blocks.conf
│   │   ├── keybindings
│   │   └── scripts
│   ├── programs
│   │   ├── browsers.nix
│   │   ├── common.nix
│   │   ├── default.nix   # here we import all modules in programs folder by imports = [...]
│   │   ├── git.nix
│   │   ├── media.nix
│   │   ├── vscode.nix
│   │   └── xdg.nix
│   ├── rofi              #  rofi launcher's configuration
│   │   ├── configs
│   │   │   ├── arc_dark_colors.rasi
│   │   │   ├── arc_dark_transparent_colors.rasi
│   │   │   ├── power-profiles.rasi
│   │   │   ├── powermenu.rasi
│   │   │   ├── rofidmenu.rasi
│   │   │   └── rofikeyhint.rasi
│   │   └── default.nix
│   └── shell             # shell/terminal related configuration
│       ├── common.nix
│       ├── default.nix
│       ├── nushell
│       │   ├── config.nu
│       │   ├── default.nix
│       │   └── env.nu
│       ├── starship.nix
│       └── terminals.nix
├── hosts
│   ├── msi-rtx4090      # My main machine's configuration
│   │   ├── default.nix  # This is the old configuration.nix, but most of the content has been split out to modules.
│   │   └── hardware-configuration.nix  # hardware & disk related configuration, autogenerated by nixos
│   └── my-nixos       # my test machine's configuration
│       ├── default.nix
│       └── hardware-configuration.nix
├── modules          # some common NixOS modules that can be reused
│   ├── i3.nix
│   └── system.nix
└── wallpaper.jpg    # wallpaper
```

There is no need to follow the above structure, you can organize your configuration in any way you like. The key is to use `imports` to import all the submodules into the main module. 

---
## `lib.mkOverride`, `lib.mkDefault`,  and `lib.mkForce`

In Nix, some people use `lib.mkDefault` and `lib.mkForce` to define values. These functions are designed to set default values or force values of options.

You can explore the source code of `lib.mkDefault` and `lib.mkForce` by running `nix repl -f '<nixpkgs>'` and then entering `:e lib.mkDefault`. To learn more about `nix repl`, type `:?` for the help information.

Here's the source code:

```python
  # ......

  mkOverride = priority: content:
    { _type = "override";
      inherit priority content;
    };

  mkOptionDefault = mkOverride 1500; # priority of option defaults
  mkDefault = mkOverride 1000; # used in config sections of non-user modules to set a default
  mkImageMediaOverride = mkOverride 60; # image media profiles can be derived by inclusion into host config, hence needing to override host config, but do allow user to mkForce
  mkForce = mkOverride 50;
  mkVMOverride = mkOverride 10; # used by ‘nixos-rebuild build-vm’

  # ......
```

In summary, `lib.mkDefault` is used to set default values of options with a priority of 1000 internally, and `lib.mkForce` is used to force values of options with a priority of 50 internally. If you set a value of an option directly, it will be set with a default priority of 1000, the same as `lib.mkDefault`.

The lower the `priority` value, the higher the actual priority. As a result, `lib.mkForce` has a higher priority than `lib.mkDefault`. If you define multiple values with the same priority, Nix will throw an error. 

Using these functions can be very helpful for modularizing the configuration. You can set default values in a low-level modules (base module) and force values in a high-level module.

For example, in my configuration at [ryan4yin/nix-config/blob/c515ea9/modules/nixos/core-server.nix](https://github.com/ryan4yin/nix-config/blob/c515ea9/modules/nixos/core-server.nix#L32), I define default values like this:

```python
{ lib, pkgs, ... };

{
  # .......

  nixpkgs.config.allowUnfree = lib.mkDefault false;

  # .......
}
```

Then, for my desktop machine, I override the value in [ryan4yin/nix-config/blob/c515ea9/modules/nixos/core-desktop.nix](https://github.com/ryan4yin/nix-config/blob/c515ea9/modules/nixos/core-desktop.nix#L18) like this:

```python
{ lib, pkgs, ... };

{
  # import the base module
  imports = [
    ./core-server.nix
  ];

  # override the default value defined in the base module
  nixpkgs.config.allowUnfree = lib.mkForce true;

  # .......
}
```

---
## `lib.mkOrder`, `lib.mkBefore`, and `lib.mkAfter`

In addition to `lib.mkDefault`, and `lib.mkForce`, there are also `lib.mkBefore` and `lib.mkAfter`, which are used to set the merge order of **list-type options**. These functions further contribute to the modularization of the configuration.
	I haven't found the official documentation for list-type options, but I understand that they are types whose merge results are related to the order of merging. According to this understanding, both `list` and `string` types are list-type options, and these functions can indeed be used on these two types in practice.

As mentioned earlier, when you define multiple values with the same **override priority**, Nix will throw an error. However, by using `lib.mkOrder`, `lib.mkBefore` or `lib.mkAfter`, you can define multiple values with the same override priority, and they will be merged in the order you specify.

To examine the source code of `lib.mkBefore`, you can run `nix repl -f '<nixpkgs>'` and then enter `:e lib.mkBefore`. To learn more about `nix repl`, type `:?` for the help information.

```python
mkOrder = priority: content:
  { _type = "order";
    inherit priority content;
  };

mkBefore = mkOrder 500;
defaultOrderPriority = 1000;
mkAfter = mkOrder 1500;

# ......
```

Therefore, `lib.mkBefore` is a shorthand for `lib.mkOrder 500`, and `lib.mkAfter` is a shorthand for `lib.mkOrder 1500`.

To test the usage of `lib.mkbefore` and `lib.mkAfter`, let's create a simple Flake project:

```python
# flake.nix
{
  inputs.nixpkgs.url = "github:NixOS/nixpkgs/nixos-23.11";
  outputs = {nixpkgs, ...}: {
    nixosConfigurations = {
      "my-nixos" = nixpkgs.lib.nixosSystem {
        system = "x86_64-linux";

        modules = [
          ({lib, ...}: {
            programs.bash.shellInit = lib.mkBefore ''
              echo 'insert before default'
            '';
            programs.zsh.shellInit = lib.mkBefore "echo 'insert before default';";
            nix.settings.substituters = lib.mkBefore [
              "https://nix-community.cachix.org"
            ];
          })

          ({lib, ...}: {
            programs.bash.shellInit = lib.mkAfter ''
              echo 'insert after default'
            '';
            programs.zsh.shellInit = lib.mkAfter "echo 'insert after default';";
            nix.settings.substituters = lib.mkAfter [
              "https://ryan4yin.cachix.org"
            ];
          })

          ({lib, ...}: {
            programs.bash.shellInit = ''
              echo 'this is default'
            '';
            programs.zsh.shellInit = "echo 'this is default';";
            nix.settings.substituters = [
              "https://nix-community.cachix.org"
            ];
          })
        ];
      };
    };
  };
}
```

The flake above contains the usage of `lib.mkBefore` and `lib.mkAfter` on multiline strings, single-line strings, and lists. Let's test the results:

```python
# Example 1: multiline string merging
› echo $(nix eval .#nixosConfigurations.my-nixos.config.programs.bash.shellInit)
trace: warning: system.stateVersion is not set, defaulting to 23.11. Read why this matters on https://nixos.org/manual/nixos/stable/options.html#opt-system.stateVersio
n.
"echo 'insert before default'

echo 'this is default'

if [ -z \"$__NIXOS_SET_ENVIRONMENT_DONE\" ]; then
 . /nix/store/60882lm9znqdmbssxqsd5bgnb7gybaf2-set-environment
fi



echo 'insert after default'
"

# example 2: single-line string merging
› echo $(nix eval .#nixosConfigurations.my-nixos.config.programs.zsh.shellInit)
"echo 'insert before default';
echo 'this is default';
echo 'insert after default';"

# Example 3: list merging
› nix eval .#nixosConfigurations.my-nixos.config.nix.settings.substituters
[ "https://nix-community.cachix.org" "https://nix-community.cachix.org" "https://cache.nixos.org/" "https://ryan4yin.cachix.org" ]
```

As you can see, `lib.mkBefore` and `lib.mkAfter` can define the order of merging of multiline strings, single-line strings, and lists. The order of merging is the same as the order of definition. 

For a deeper introduction to the module system, see [Module System & Custom Options](https://nixos-and-flakes.thiscute.world/other-usage-of-flakes/module-system).
# Module System and Custom Options

In our previous NixOS configurations, we set various values for `options` to configure NixOS or Home Manager. These `options` are actually defined in two locations:

- NixOS: [nixpkgs/nixos/modules](https://github.com/NixOS/nixpkgs/tree/23.11/nixos/modules), where all NixOS options visible on [https://search.nixos.org/options](https://search.nixos.org/options) are defined.
- Home Manager: [home-manager/modules](https://github.com/nix-community/home-manager/blob/release-23.11/modules), where you can find all its options at [https://nix-community.github.io/home-manager/options.xhtml](https://nix-community.github.io/home-manager/options.xhtml).

> If you are using nix-darwin too, its configuration is similar, and its module system is implemented in [nix-darwin/modules](https://github.com/LnL7/nix-darwin/tree/master/modules).

The foundation of the aforementioned NixOS modules and Home Manager modules is a universal module system implemented in Nixpkgs, found in [lib/modules.nix](https://github.com/NixOS/nixpkgs/blob/23.11/lib/modules.nix#L995). The official documentation for this module system is provided below (even for experienced NixOS users, understanding this can be a challenging task):

[Module System - Nixpkgs](https://github.com/NixOS/nixpkgs/blob/23.11/doc/module-system/module-system.chapter.md)

Because the documentation for Nixpkgs' module system is lacking, it directly recommends reading naother writing guide specifically for NixOS module system, which is clearer by might still be challenging for newcomers:

[Writing NixOS Modules - Nixpkgs](https://github.com/NixOS/nixpkgs/blob/nixos-23.11/nixos/doc/manual/development/writing-modules.chapter.md)

In summary, the module system is implemented by Nixpkgs and is not part of the Nix package manager. Therefore, its documentation is not included in the Nix package manager's documentation. Additionally, both NixOS and Home Manager are based on Nixpkgs' module system implementation.

---
## What is the Purpose of the Module System?

As ordinary users, using various options implemented by NixOS and Home Manager based on the module system is sufficient to meet most of our needs. So, what are the benefits of delving into the module system for us?

In the earlier discussion on modular configuration, the core idea was to split the configuration into multiple modules and then import these modules using `imports = [ ... ];`. This is the most basic usage of the module system. However, using only `imports = [ ... ];` allows us to *import configurations defined in the module* as they are without any customization, which limits flexibility. In simple configurations, this method is sufficient, but if the configuration is more complex, it becomes inadequate. 

To illustrate the drawback, let's consider an example. Suppose i manage four NixOS hosts, A, B, C and D. I want to achieve the following goals while minimizing configuration repetition:

- All hosts, (A, B, C and D) need to enable the Docker service and set it to start at boot.
- Host A should change the Docker storage driver to `btrfs` while keeping other settings the same.
- Hosts B and C, located in China, need to set a domestic mirror in Docker configuration.
- Host C, located in the US, has no special requirements.
- Host D, a desktop machine, needs to set up an HTTP proxy to accelerate Docker downloads.

If we purely use `imports`, we might have to split the configuration into several modules like this and then import different modules for each host:

```python
› tree
.
├── docker-default.nix  
# Basic Docker configuration, including starting at boot
├── docker-btrfs.nix    
# Imports docker-default.nix and changes the storage driver to btrfs
├── docker-china.nix    
# Imports docker-default.nix and sets a domestic mirror
└── docker-proxy.nix    
# Imports docker-default.nix and sets an HTTP proxy
```

Doesn't this configuration seem redundant? This is still a simple example; if we have more machines with greater configuration differences, the redundancy becomes even more apparent. 

Clearly, we need other means to address this redundant configuration issue, and customizing some of our own `options` is an excellent choice.

Before delving into the study of the module system, I emphasize once again that the following content is not necessary to learn and use. Many NixOS users have no customized any `options` and are satisfied with simply using `imports` to meet their needs. If you are a newcomer, consider learning this part when you encounter problems that `imports` cannot solve. 

--- 
## Basic Structure and Usage

The basic structure of modules defined in Nixpkgs is as follows:

```python
{ config, pkgs, ... }:

{
  imports =
    [ # import other modules here
    ];

  options = {
    # ...
  };

  config = {
    # ...
  };
}
```

Among these, we are already familiar with `imports = [ ... ];`, but the other two parts are yet to be explored. Let's have a brief introduction here:

- `options = { ... };`: similar to variable declarations in programming languages, it is used to declare configurable options.
- `config = { ... };`: Similar to variable assignments in programming languages, it is used to assign values to the options declared in `options`.

The most typical usage is to,  within the same Nixpkgs module, set values for other `options` in `config { ... };` based on the current values declared in `options = { ... };`. This achieves the functionality of parameterized configuration.

It's easier to understand with a direct example:

```python
# ./foo.nix
{ config, lib, pkgs, ... }:

with lib;

let
  cfg = config.programs.foo;
in {
  options.programs.foo = {
    enable = mkEnableOption "the foo program";

    package = mkOption {
      type = types.package;
      default = pkgs.hello;
      defaultText = literalExpression "pkgs.hello";
      description = "foo package to use";
    };

    extraConfig = mkOption {
      default = "";
      example = ''
        foo bar
      '';
      type = type.lines;
      description = ''
        Extra settings for foo.
      '';
    };
  };

  config = mkIf cfg.enable {
    home.packages = [ cfg.package ];
    xdg.configFile."foo/foorc" = mkIf (cfg.extraConfig != "") {
      text = ''
        # generated by Home Manager

        ${cfg.extraConfig}
      '';
    };
  };
}
```   

The module defined above introduces three `options`:

- `programs.foo.enable`: Used to control whether to enable this module.
- `programs.foo.package`: Allows customization of the `foo` package, such as using different versions, setting different configuration parameters, and so on.
- `programs.foo.extraConfig`: Used for customizing the configuration file of `foo`.

Then, in the `config` section, based on the values declared in these three variables in `options`, different settings are applied:

- If `programs.foo.enable` is `false` or undefined, no settings are applied.
	- This is achieved using `lib.mkIf`.
- Otherwise,
	- Add `programs.foo.package` to `home.packages` to install it in the user environment.
	- Write the value of `programs.foo.extraConfig` to `~/.config/foo/foorc`.

This way, we can import this module in another Nix file and achieve custom configuation for `foo` by setting the `options` defined here. For example:

```python
# ./bar.nix
{ config, lib, pkgs, ... }:

{
  imports = [
    ./foo.nix
  ];

  programs.foo ={
    enable = true;
    package = pkgs.hello;
    extraConfig = ''
      foo baz
    '';
  };
}
```

In the example above, the way we assign values to `options` is actually a kind of **abbreviation**. When a module only contains `config` without any other declaration (like `option` and other special parameters of the module system), we can omit the `config` wrapping, just directly write the content of `config` to assign value to `option` section declared in other modules!

---
## Assignment and Lazy Evaluation in the Module System

The module system takes full advantage of Nix's lazy evaluation feature, which is crucial for achieving parameterized configuration.

Let's start with a simple example:

```python
# ./flake.nix
{
  description = "NixOS Flake for Test";
  inputs.nixpkgs.url = "github:NixOS/nixpkgs/nixos-24.05";

  outputs = {nixpkgs, ... }: {
    nixosConfigurations = {
      "test" = nixpkgs.lib.nixosSystem {
        system = "x86_64-linux";
        modules = [
          {{config, lib, ...}: {
            options = {
              foo = lib.mkOption {
                default = false;
                type = lib.types.bool;
              };
            };
            
            # scenario 1 (works fine)
            config.warnings = if config.foo then ["foo"] else [];
            
            # scenario 2 (error: infinite recursion encountered)
            # config = if config.foo then { warning = ["foo"];} else {};
            
            # scenario 3 (works fine)
            # config = lib.mkIf config.foo {warning = ["foo"];};
          })
        ];
      };
    };
  };
}
```

In the examples 1, 2 and 3 of the above configuration, the value of `config.warnings` depends on the value of `config.too`, but their implementation methods are different. Save the above configuration as `flake.nix` and then use the command `nix eval .#nixosConfigurations.test.config.warnings` to test examples 1, 2 and 3 separately. You will find that examples 1 and 3 work correctly, while example 2 results in an error: `error: infinite recursion encountered`.

Let's explain each case:

1. Example 1 evaluation flow: `config.warnings` -> `config.foo` -> `config`

	1. First, Nix attempts to compute the value of `config.warnings` but finds that it depends on `config.foo`.
	2. Next, Nix tries to compute the value of `config.foo`, which depends on its outer `config`.
	3. Nix attempts to compute the value of `config`, and since the contents not genuienely used by `config.foo` are lazily evaluated by Nix, there is no recursive dependency on `config.warnings` at this point.
	4. The evaluation of `config.foo` is completed, followed by the assignment of `config.warnings`, and the computation ends.

2. Example 2: `config` -> `config.foo` -> `config`

	1. Initially, Nix tries to compute the value of `config` but finds that it depends on `config.foo`. 
	2. Next, Nix attempts to compute the value of `config.foo`, which depends on its outer `config`.
	3. Nix tries to compute the value of `config`, and this loops back to step 1, leading to an infinite recursion and eventually an error.

3. Example 3: The only difference from example 2 is the use of `lib.mkIf` to address the infinite recursion issue.

The key lies in the function `lib.mkIf`. When using `lib.mkIf` to define `config`, it will be lazily evaluated by Nix. This means that the calculation of `config = lib.mkIf ...` will only occur after the evaluation of `config.foo` is completed.

The Nixpkgs module system provides a series of functions similar to `lib.mkIf` for parameterized configuration and intelligent module merging:

1. `lib.mkIf`: Already introduced.
2. `lib.mkOverride` / `lib.mkDefault` / `lib.mkForce`: Previously discussed in [Modularizing NixOS Configuration](https://nixos-and-flakes.thiscute.world/nixos-with-flakes/modularize-the-configuration).
3. `lib.mkOrder`/ `lib.mkBefore`/ and `lib.mkAfter`: As mentioned above.
4. Check [Option Definitions - NixOS](https://github.com/NixOS/nixpkgs/blob/nixos-23.11/nixos/doc/manual/development/option-def.section.md) for more functions related to option assignment (definition).

--- 
## Option Declaration and Type Checking

While assignment is the most commonly used feature of the module system, if you need to customize some `options`, you also need to delve into option declaration and type checking. I find this part relatively straightforward; it's much simpler than assignment, and you can understand the basics by directly referring to the official documentation. I won't go into detail here.

- [Option Declarations - NixOS](https://github.com/NixOS/nixpkgs/blob/nixos-23.11/nixos/doc/manual/development/option-declarations.section.md)
- [Options Types - NixOS](https://github.com/NixOS/nixpkgs/blob/nixos-23.11/nixos/doc/manual/development/option-types.section.md)

---
## Passing Non-default Parameters to the Module System

We have already introduced how to use `specialArgs` and `_module.args` to pass additional parameters to other Modules functions in [Managing Your NixOS with Flakes](https://nixos-and-flakes.thiscute.world/nixos-with-flakes/nixos-with-flakes-enabled#pass-non-default-parameters-to-submodules). No further elaboration is needed here.

---
## How to Selectively Import Modules

In the example above, we have introduced how to enable or disable certain features through custom options. However, our code implementations are all within the same Nix file. If our modules are scattered across different files, how can we achieve selective import?

Let's first take a look at some common incorrect usage patterns, and then introduce the correct way to do it.
### Incorrect Usage #1 - Using `imports` in `config = { ... };`

The first thought might be to directly use `imports` in `config = { ... };`, like this:

```python
# ./flake.nix
{
  description = "NixOS Flake for Test";
  inputs.nixpkgs.url = "github:NixOS/nixpkgs/nixos-23.11";

  outputs = {nixpkgs, ...}: {
    nixosConfigurations = {
      "test" = nixpkgs.lib.nixosSystem {
        system = "x86_64-linux";
        modules = [
          ({config, lib, ...}: {
            options = {
              foo = lib.mkOption {
                default = false;
                type = lib.types.bool;
              };
            };
            config = lib.mkIf config.foo {
              # Using imports in config will cause an error
              imports = [
                {warnings = ["foo"];}
                # ...omit other module or file paths
              ];
            };
          })
        ];
      };
    };
  };
}
```

But this won't work. You can try to save the above `flake.nix` in a new directory, and then run `nix eval .#nixosConfigurations.test.config.warnings` in it, some error like `error: The option 'imports' does not exist.` will be encountered. 

This is because `config` is a regular attribute set, while `imports` is a special parameter of the module system. There is no such definition as `config.imports`.
### Correct Usage #1 - Define Individual `options` for All Modules That Require Conditional Import

This is the most recommended method. Modules in NixOS systems are implemented in this way, and searching for `enable` in [https://search.nixos.org/options](https://search.nixos.org/options) will show a large number of system modules that can be enabled or disabled through the `enable` option.

The specific writing method has been introduced in the previous [Basic Structure and Usage](https://nixos-and-flakes.thiscute.world/other-usage-of-flakes/module-system#basic-structure-and-usage) section and will not be repeated here.

The disadvantage of this method is that all Nix modules that require conditional import need to be modified, moving all configuration declarations in the module to the `config = { ... };` code block, increasing code complexity and being less friendly to beginners.
### Correct Usage #2 - Use `lib.optionals` in `imports = [];`

The main advantage of this method is that it is much simpler than the methods previously introduced, requiring no modification to the module content, just using `lib.optionals` in `imports` to decide whether to import a module or not.

> Details about how `lib.optionals` works: [https://noogle.dev/f/lib/optionals](https://noogle.dev/f/lib/optionals)

Let's look at an example directly:

```python
# ./flake.nix
{
  description = "NixOS Flake for Test";
  inputs.nixpkgs.url = "github:NixOS/nixpkgs/nixos-23.11";

  outputs = {nixpkgs, ...}: {
    nixosConfigurations = {
      "test" = nixpkgs.lib.nixosSystem {
        system = "x86_64-linux";
        specialArgs = { enableFoo = true; };
        modules = [
          ({config, lib, enableFoo ? false, ...}: {
            imports =
              [
                 # Other Modules
              ]
              # Use lib.optionals to decide whether to import foo.nix
              ++ (lib.optionals (enableFoo) [./foo.nix]);
          })
        ];
      };
    };
  };
}
```
```
#./foo.nix
( warnings = ["foo"];)
```

Save the two Nix files above in a folder, and then use `nix eval .#nixosConfigurations.test.config.warnings` in the folder, and the operation is normal:

```
› nix eval .#nixosConfigurations.test.config.warnings
[ "foo" ]
```

One thing to note here is that **you cannot use parameters passed by `_module.args`** in `imports =[ ... ];`. We have already provided a detailed explanation in the previous section [Passing Non-default Parameters to Submodules](https://nixos-and-flakes.thiscute.world/nixos-with-flakes/nixos-with-flakes-enabled#pass-non-default-parameters-to-submodules).
## References

- [Best resources for learning about the NixOS module system? - Discourse](https://discourse.nixos.org/t/best-resources-for-learning-about-the-nixos-module-system/1177/4)
- [NixOS modules - NixOS Wiki](https://wiki.nixos.org/wiki/NixOS_modules)
- [NixOS: config argument - NixOS Wiki](https://wiki.nixos.org/wiki/NixOS:config_argument)
- [Module System - Nixpkgs](https://github.com/NixOS/nixpkgs/blob/23.11/doc/module-system/module-system.chapter.md)
- [Writing NixOS Modules - Nixpkgs](https://github.com/NixOS/nixpkgs/blob/nixos-23.11/nixos/doc/manual/development/writing-modules.chapter.md)
# Updating the System

With Flakes, updating the system is straightforward. Simply execute the following commands in `/etc/nixos` or any other location where you keep the configuration:

```python
# Update flake.lock
nix flake update

# Or replace only the specific input, such as home-manager:
nix flake update home-manager

# Apply the updates
sudo nixos-rebuild switch --flake .

# Or to update flake.lock & apply with one command (i.e. same as running "nix flake update" before)
sudo nixos-rebuild switch --recreate-lock-file --flake .
```

Occasionally, you may encounter a "sha256 mismatch" error when running `nixos-rebuild switch`. This error can be resolved by updating `flake.lock` using `nix flake update`.
# Downgrading or Upgrading Packages

When working with Flakes, you may encounter situations where you need to downgrade or upgrade certain packages to address bugs or compatibility issues. In Flakes, package versions and hash values are directly tied to the git commit of their flake input. To modify the package version, you need to lock the git commit of the flake input.

Here's an example of how you can add multiple nixpkgs inputs, each using a different git commit or branch:

```python
{
  description = "NixOS configuration of Ryan Yin";

  inputs = {
    # Default to the nixos-unstable branch
    nixpkgs.url = "github:nixos/nixpkgs/nixos-unstable";

    # Latest stable branch of nixpkgs, used for version rollback
    # The current latest version is 23.11
    nixpkgs-stable.url = "github:nixos/nixpkgs/nixos-23.11";

    # You can also use a specific git commit hash to lock the version
    nixpkgs-fd40cef8d.url = "github:nixos/nixpkgs/fd40cef8d797670e203a27a91e4b8e6decf0b90c";
  };

  outputs = inputs@{
    self,
    nixpkgs,
    nixpkgs-stable,
    nixpkgs-fd40cef8d,
    ...
  }: {
    nixosConfigurations = {
      nixos = nixpkgs.lib.nixosSystem rec {
        system = "x86_64-linux";

        # The `specialArgs` parameter passes the
        # non-default nixpkgs instances to other nix modules
        specialArgs = {
          # To use packages from nixpkgs-stable,
          # we configure some parameters for it first
          pkgs-stable = import nixpkgs-stable {
            # Refer to the `system` parameter from
            # the outer scope recursively
            inherit system;
            # To use Chrome, we need to allow the
            # installation of non-free software.
            config.allowUnfree = true;
          };
          pkgs-fd40cef8d = import nixpkgs-fd40cef8d {
            inherit system;
            config.allowUnfree = true;
          };
        };

        modules = [
          ./hosts/nixos

          # Omit other configurations...
        ];
      };
    };
  };
}
```

In the above example, we have defined multiple nixpkgs inputs: `nixpkgs`, `nixpkgs-stable`, and `nixpkgs-fd40cef8d`. Each input corresponds to a different git commit or branch.

Next, you can refer to the packages from `pkgs-stable` or `pkgs-fd40cef8d` within your submodule. Here's an example of a Home Manager submodule.

```nix
{
  pkgs,
  config,
  # Nix will search for and inject this parameter
  # from `specialArgs` in `flake.nix`
  pkgs-stable,
  # pkgs-fd40cef8d,
  ...
}:

{
  # Use packages from `pkgs-stable` instead of `pkgs`
  home.packages = with pkgs-stable; [
    firefox-wayland

    # Chrome Wayland support was broken on the nixos-unstable branch,
    # so we fallback to the stable branch for now.
    # Reference: https://github.com/swaywm/sway/issues/7562
    google-chrome
  ];

  programs.vscode = {
    enable = true;
    # Refer to vscode from `pkgs-stable` instead of `pkgs`
    package = pkgs-stable.vscode;
  };
}
```

---
## Pinning a Package Version with an Overlay

The above approach is perfect for application packages, but sometimes you need to replace libraries used by those packages. This is where [Overlays](https://nixos-and-flakes.thiscute.world/nixpkgs/overlays) shine! Overlays can edit or replace any attribute of a package, but for now we'll just pin a package to a different nixpkgs version. The main disadvantage of editing a dependency with an overlay is that your Nix installation will recompile all installed packages that depend on it, but your situation may require it for specific bug fixes.

```nix
# overlays/mesa.nix
{ config, pkgs, lib, pkgs-fd40cef8d, ... }:
{
  nixpkgs.overlays = [
    # Overlay: Use `self` and `super` to express
    # the inheritance relationship
    (self: super: {
      mesa = pkgs-fd40cef8d.mesa;
    })
  ];
}
```
## Applying the New Configuration

By adjusting the configuration as shown above, you can deploy it using `sudo nixos-rebuild switch`. This will downgrade your Firefox/Chrome/VSCode versions to the ones corresponding to `nixpkgs-stable` or `nixpkgs-fd40cef8d`.

> According to [1000 instances of nixpkgs](https://discourse.nixos.org/t/1000-instances-of-nixpkgs/17347), it's not a good practice to use `import` in submodules or subflakes to customize `nixpkgs`. Each `import` creates a new instance of nixpkgs, which increases build time and memory usage as the configuration grows. To avoid this problem, we create all nixpkgs instances in `flake.nix`.
# Other Useful Tips

## Show Detailed Error Messages

You can always try to add `--show-trace --print-build-logs --verbose` to the `nixos-rebuild` command to get the detailed error message if you encounter any errors during the deployment. e.g.

```bash
cd /etc/nixos
sudo nixos-rebuild switch --flake .#myhost --show-trace --print-build-logs --verbose

# A more concise version
sudo nixos-rebuild switch --flake .#myhost --show-trace -L -v
```

---
## Managing the Configuration with Git

NixOS configuration, being a set of text files, is well-suited for version control with Git. This allows easy rollback to a previous version in case of issues.

> [!NOTE]
> NOTE: When using Git, Nix ignores all files that are not tracked by Git. If you encounter an error in Nix stating that a particular file is not found, it may be because you haven't `git add`ed it.

By default, NixOS places the configuration in `etc/nixos`, which requires root permissions for modifications, making it inconvenient for daily use. Thankfully, flakes can help solve this problem by allowing you to place your flake anywhere you prefer. 

For example, you can place your flake in `~/nixos-config` and create a symbolic link in `/etc/nixos` as follows:

```
sudo mv /etc/nixos /etc/nixos.bak # backup the original configuration
sudo ln -s ~/nixos-config /etc/nixos

# deploy the flake.nix located at the default location (/etc/nixos)
sudo nixos-rebuild switch
```

This way, you can use Git to manage the configuration in `~/nixos-config`. The configuration can be modified with regular user-level permissions and does not require root ownership.

Another approach is to delete `/etc/nixos` directly and specify the configuration file path each time you deploy it:

```
sudo mv /etc/nixos /etc/nixos.bak
cd ~/nixos-config

# '--flake .#my-nixos' deploys the flake located in 
# the current directory, and the nixosConfiguration's name is 'my-nixos'
sudo nixos-rebuild switch --flake .#my-nixos
```

Choose the method that suits you best. Afterward, system rollback becomes simple. Just switch to the previous commit and deploy it:

```
cd ~/nixos-config
# switch to previous commit
git checkout HEAD^1
# deploy the flake.nix located in the current directory,
# with the nixosConfiguration's name 'nixos'
sudo nixos-rebuild switch --flake .#nixos
```

More advanced Git operations are not covered here, but in general, rollback can be performed directly using Git. Only in cases of complete system crashes would you need to restart into the bootloader and boot the system from a previous historical version.

---
## Viewing and Deleting Historical Data

As mentioned earlier, each NixOS deployment creates a new version, and all versions are added to the system's boot options. In addition to restarting the computer, you can query all available historical versions using the following command:

```
nix profile history --profile /nix/var/nix/profiles/system
```

To clean up historical versions and free up storage space, use the following command:

```nix
# Delete all historical versions older than 7 days
sudo nix profile wipe-history --older-than 7d --profile /nix/var/nix/profiles/system

# Wiping history won't garbage collect the unused packages, you need to
# run the gc command manually as root:
sudo nix-collect-garbage --delete-old

# Due to the following issue, you need to run the gc command as per
# user to delete home-manager's historical data:
# https://github.com/NixOS/nix/issues/8508
nix-collect-garbage --delete-old
```

---
## Why Some Packages are Installed?

To find out why a package is installed, you can use the following command:

1. Enter a shell with `nix-tree` & `rg` available: `nix shell nixpkgs#nix-tree nixpkgs#ripgrep`
2. `nix-store --gc --print-roots | rg -v '/proc' | rg -Po '(?<= ->).*' | xargs -o nix-tree`
3. `/<package-name>` to find the package you want to check.
4. `w` to show the package is depended by which packages, and the full dependency chain.

---
## Reducing Disk Usage

The following configuration can be added to your NixOS configuration to help reduce disk usage:

```nix
{ lib, pkgs, ... }:

{
  # ...

  # Limit the number of generations to keep
  boot.loader.systemd-boot.configurationLimit = 10;
  # boot.loader.grub.configurationLimit = 10;

  # Perform garbage collection weekly to maintain low disk usage
  nix.gc = {
    automatic = true;
    dates = "weekly";
    options = "--delete-older-than 1w";
  };

  # Optimize storage
  # You can also manually optimize the store via:
  #    nix-store --optimise
  # Refer to the following link for more details:
  # https://nixos.org/manual/nix/stable/command-ref/conf-file.html#conf-auto-optimise-store
  nix.settings.auto-optimise-store = true;
}
```

By incorporating this configuration, you can better manage and optimize the disk usage of your NixOS system.


