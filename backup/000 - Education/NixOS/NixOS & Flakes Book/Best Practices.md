#Nix #nixos #linux 
# Introduction

Nix is a powerful and flexible tool that offers various approaches to accomplish tasks, which can sometimes make it challenging to determine the most suitable method for a particular job. To assist you in navigating through this vast ecosystem, I have compiled some best practices that I've learned from the community. I hope these practices prove helpful to you.
# Running Downloaded Binaries on NixOS

Since NixOS does not strictly adhere to the Filesystem Hierarchy Standard (FHS), binaries downloaded from the internet may not work directly on NixOS. However, there are various methods available to make them function properly. 

For a comprehensive guide that presents ten different approaches to run downloaded binaries on NixOS, I recommend reading the article [Different methods to run a non-nixos executable on Nixos](https://unix.stackexchange.com/questions/522822/different-methods-to-run-a-non-nixos-executable-on-nixos) and take a look at [nix-alien](https://github.com/thiagokokada/nix-alien). Or if you are familiar with Docker, running the binary in a Docker container is also a good choice.

Among these methods, I personally prefer creating an FHS environment to run the binary, as it proves to be both convenient and easy to use. To set up an environment, you can add the following code to one of your Nix modules:

```Nix
{ config, pkgs, lib, ... }:

{
  # ......omit many configurations

  environment.systemPackages = with pkgs; [
    # ......omit many packages

    # Create an FHS environment using the command `fhs`, enabling the execution of non-NixOS packages in NixOS!
    (let base = pkgs.appimageTools.defaultFhsEnvArgs; in
      pkgs.buildFHSUserEnv (base // {
      name = "fhs";
      targetPkgs = pkgs: (
        # pkgs.buildFHSUserEnv provides only a minimal FHS environment,
        # lacking many basic packages needed by most software.
        # Therefore, we need to add them manually.
        #
        # pkgs.appimageTools provides basic packages required by most software.
        (base.targetPkgs pkgs) ++ with pkgs; [
          pkg-config
          ncurses
          # Feel free to add more packages here if needed.
        ]
      );
      profile = "export FHS=1";
      runScript = "bash";
      extraOutputsToInstall = ["dev"];
    }))
  ];

  # ......omit many configurations
}
```

After applying the updated configuration, you can use the `fhs` command to enter the FHS environment, and then execute the binary you downloaded, for example:

```sh
# Activating FHS drops me into a shell that resembles a "normal" Linux environment.
$ fhs
# Check what we have in /usr/bin.
(fhs) $ ls /usr/bin
# Try running a non-NixOS binary downloaded from the Internet.
(fhs) $ ./bin/code
```
## References

- [Tips&Tricks for NixOS Desktop - NixOS Discourse](https://discourse.nixos.org/t/tips-tricks-for-nixos-desktop/28488): This resource provides a collection of useful tips and tricks for NixOS desktop users.
- [nix-alien](https://github.com/thiagokokada/nix-alien): Run unpatched binaries on Nix/NixOS
- [nix-ld](https://github.com/Mic92/nix-ld): Run unpatched dynamic binaries on NixOS.
- [NixOS: Packaging Closed Source Software (& Binary Distributed Ones) - Lan Tian @ Blog](https://lantian.pub/en/article/modify-computer/nixos-packaging.lantian/#examples-closed-source-software--binary-distributed-ones)
# Simplifying NixOS-Related Commands

To simplify NixOS-related commands, I utilize [just](https://github.com/casey/just), which proves to be very convenient.

Alternatively, you can also use similar tools like Makefile or [cargo-make](https://github.com/sagiegurari/cargo-make) for this purpose. Here, I will provide my approach as a reference.

Below is an example of how my Justfile looks:

> The latest Justfile I'm using: [ryan4yin/nix-config/Justfile](https://github.com/ryan4yin/nix-config/blob/main/Justfile)

```Makefile
# just is a command runner, Justfile is very similar to Makefile, but simpler.

############################################################################
#
#  Nix commands related to the local machine
#
############################################################################

deploy:
  nixos-rebuild switch --flake . --use-remote-sudo

debug:
  nixos-rebuild switch --flake . --use-remote-sudo --show-trace --verbose

up:
  nix flake update

# Update specific input
# usage: make upp i=home-manager
upp:
  nix flake update $(i)

history:
  nix profile history --profile /nix/var/nix/profiles/system

repl:
  nix repl -f flake:nixpkgs

clean:
  # remove all generations older than 7 days
  sudo nix profile wipe-history --profile /nix/var/nix/profiles/system  --older-than 7d

gc:
  # garbage collect all unused nix store entries
  sudo nix-collect-garbage --delete-old

############################################################################
#
#  Idols, Commands related to my remote distributed building cluster
#
############################################################################

add-idols-ssh-key:
  ssh-add ~/.ssh/ai-idols

aqua: add-idols-ssh-key
  nixos-rebuild --flake .#aquamarine --target-host aquamarine --build-host aquamarine switch --use-remote-sudo

aqua-debug: add-idols-ssh-key
  nixos-rebuild --flake .#aquamarine --target-host aquamarine --build-host aquamarine switch --use-remote-sudo --show-trace --verbose

ruby: add-idols-ssh-key
  nixos-rebuild --flake .#ruby --target-host ruby --build-host ruby switch --use-remote-sudo

ruby-debug: add-idols-ssh-key
  nixos-rebuild --flake .#ruby --target-host ruby --build-host ruby switch --use-remote-sudo --show-trace --verbose

kana: add-idols-ssh-key
  nixos-rebuild --flake .#kana --target-host kana --build-host kana switch --use-remote-sudo

kana-debug: add-idols-ssh-key
  nixos-rebuild --flake .#kana --target-host kana --build-host kana switch --use-remote-sudo --show-trace --verbose

idols: aqua ruby kana

idols-debug: aqua-debug ruby-debug kana-debug
```

By Save this `Justfile` to the root directory of your Nix flake. Then, I can use `just deploy` to deploy the configuration to my local machine, and `just idols` to deploy the configuration to all my remote servers. 

This approach simplifies the execution of NixOS commands by abstracting them behind target names in the Justfile, providing a more user-friendly and convenient experience.
# Accelerating Dotfiles Debugging

When managing our Dotfiles with Home Manager, a common challenge arises -- each modification to our dotfiles requires executing `sudo nixos-rebuild switch` (or `home-manager switch`) if you don't integrate home-manager into NixOS) to take effect. However, running this command recalculates the *entire system state each time*, even though Nix internally employs various caching mechanisms to expedite the process, it can still be cumbersome. 

Take my favorite Neovim/Emacs configurations as an example; I frequently make high-frequency modifications to them, sometimes dozens or hundreds of times a day. If each modification necessitates waiting for `nixos-rebuild` to run for several seconds, it becomes a significant time drain.

Fortunately, with the solution outlined in [Simplifying NixOS Commands using Justfile](https://nixos-and-flakes.thiscute.world/best-practices/simplify-nixos-related-commands), we can expedite testing and verification of frequently modified Dotfiles by adding specific 
configurations to the `Justfile`.

For instance, I've added the following content to my Justfile:

> The latest Justfile I'm using: [ryan4yin/nix-config/Justfile](https://github.com/ryan4yin/nix-config/blob/main/Justfile)

```
###############################################################
# Quick Test - Neovim
###############################################################


nvim-clean:
  rm -rf ${HOME}.config/astronvim/lua/user

nvim-test: nvim-clean
  rsync -avz --copy-links --chmod=D2755,F744 home/base/desktop/editors/neovim/astronvim_user/ ${HOME}/.config/astronvim/lua/user
```

Now, when I need to quickly test my Neovim configuration after making changes, I simply run `just nvim-test`. Once testing is complete, I execute `just nvim-clean`, followed by redeploying the configuration using `nixos-rebuild`. This allows for swift testing and seamless restoration of the configuration.

This method is effective under the condition that your Dotfiles content is not generated by Nix. For instance, my Emacs/Neovim configurations are native and are linked to the appropriate locations solely through Nix Home-Manager's `home.file` or `xdg.configFile`.
# Custom NIX_PATH and Flake Registry
## Introduction to NIX_PATH

The Nix search path is controlled by the environment variable `NIX_PATH`, which follows the same format as the Linux `PATH` environment variable, consisting of multiple paths separated by colons.

Paths in Nix expressions that look like `<name>` are resolved using the path named `name` from the `NIX_PATH`.

This usage pattern is no longer recommended under the Flakes feature because it results in Flake builds depending on a mutable environment variable `NIX_PATH`, compromising reproducibility.

However, in certain scenarios, we still need to use `NIX_PATH`, such as when we frequently use the command `nix repl '<nixpkgs>'`, which utilizes the Nixpkgs found through `NIX_PATH` search.

---
## Introduction to Flakes Registry

The Flakes Registry is a center for Flake registration that assists us in using shorter IDs instead of lengthy flake repository addresses when using commands like `nix run`, `nix shell`, and more.

By default, Nix looks up the corresponding GitHub repository address for this ID from [https://github.com/NixOS/flake-registry/blob/master/flake-registry.json](https://github.com/NixOS/flake-registry/blob/master/flake-registry.json).

For instance, if we execute `nix run nixpkgs#ponysay hello`, Nix will automatically retrieve the GitHub repository address for `nixpkgs` from the aforementioned JSON file. It then downloads the repository, locates the `flake.nix` within, and runs the corresponding `ponysay` package. 

---
## Custom NIX_PATH and Flake Registry

> **NOTE: Newcomers should skip this section! Disabling `nix-channel` incorrectly may lead to some headaches.**

The roles of `NIX_PATH` and the Flake Registry have been explained earlier. In daily use, we typically want the `nixpkgs` used in commands like `nix repl '<nixpkgs>'`, `nix run nixpkgs#ponysay hello` to match the system's `nixpkgs`. This requires us to customize the `NIX_PATH` and Flake Registry. On the other hand, although `nix-channel` can coexist with the Flakes feature, in practice, Flakes can completely replace it, so we can also disable it.

In your NixOS configuration, adding the following module will achieve the mentioned requirements:

nix

```Nix
{lib, nixpkgs, ...}: {
  # make `nix run nixpkgs#nixpkgs` use the same nixpkgs as the one used by this flake.
  nix.registry.nixpkgs.flake = nixpkgs;
  nix.channel.enable = false; # remove nix-channel related tools & configs, we use flakes instead.

  # but NIX_PATH is still used by many useful tools, so we set it to the same value as the one used by this flake.
  # Make `nix repl '<nixpkgs>'` use the same nixpkgs as the one used by this flake.
  environment.etc."nix/inputs/nixpkgs".source = "${nixpkgs}";
  # https://github.com/NixOS/nix/issues/9574
  nix.settings.nix-path = lib.mkForce "nixpkgs=/etc/nix/inputs/nixpkgs";
}
```

[Chapter 15. Nix Search Paths - Nix Pills](https://nixos.org/guides/nix-pills/nix-search-paths.html)
# Remote Deployment

Nix's inherent design is well-suited for remote deployment, and the Nix community offers several tools tailored for this purpose, such as [NixOps](https://github.com/NixOS/nixops) and [colmena](https://github.com/zhaofengli/colmena). Additionally, the official tool we've used extensively, `nixos-rebuild`, possesses some remote deployment capabilities too.

In addition, within multi-architecture scenarios, remote deployments can optimally leverage Nix's multi-architecture support. For example, you can cross-compile an aarch64/riscv64 NixOS system on an x86_64 host, followed by remote deployment onto the corresponding hosts via SSH.

Recently, I encountered a situation where I cross-compiled a NixOS system image for a RISCV64 SBC on my local machine. Consequently, I already possessed all the compilation caches for building this system locally. However, due to the lack of official binary caches for RISCV64 architecture, executing any uninstalled program directly on the development board (e.g. `nix run nixpkgs#cowsay hello`) triggered extensive compilations. This process consumed hours, which was quite unacceptable.

By adopting remote deployment, I could fully harness the computational power of my local high-performance CPU and the extensive compilation caches. This switch vastly improved my experience and significantly mitigated the previously time-consuming compilation issue.

Let me briefly guide you through using colmena or `nixos-rebuild` for remote deployment.

---
## Prerequisites

