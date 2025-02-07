#nix #nixos #nixpkgs 
# Introduction

`callPackage, Overriding` and `Overlays` are techniques occasionally used when using Nix to customize the build method of Nix packages.

We know that many programs have a large number of build parameters that need to be configured, and different users may want to use different build parameters. This is where `Overriding` and `Overlays` come in handy. Let me give you a few examples I have encountered. 

1. [`fcitx5-rime.nix`](https://github.com/NixOS/nixpkgs/blob/e4246ae1e7f78b7087dce9c9da10d28d3725025f/pkgs/tools/inputmethods/fcitx5/fcitx5-rime.nix): By default, `fcitx5-rime` use `rime-data` as the value of `rimeDataPkgs`, but this parameter can be customized by `override`.
2. [`vscode/with-extensions.nix`](https://github.com/NixOS/nixpkgs/blob/nixos-23.05/pkgs/applications/editors/vscode/with-extensions.nix): This package for VS Code can also be customized by overriding the value of `vscodeExtensions`, thus we can install some custom plugins into VS Code.
    - [`nix-vscode-extensions`](https://github.com/nix-community/nix-vscode-extensions): This is a vscode plugin manager implemented by overriding `vscodeExtensions`.
3. [`firefox/common.nix`](https://github.com/NixOS/nixpkgs/blob/416ffcd08f1f16211130cd9571f74322e98ecef6/pkgs/applications/networking/browsers/firefox/common.nix): Firefox has many customizable parameters too.
4. ...

In short, `callPackage`, `Overriding` and `Overlays` can be used to customize the build parameters of Nix packages.
# `pkgs.callPackage`

`pkgs.callPackage` is used to parameterize the construction of Nix Derivation. To understand its purpose, let's first consider how we would define a Nix package (also known as a Derivation) without using `pkgs.callPackage`.

---
## Without `pkgs.callPackage`

We can define a Nix package using code like this:

```
pkgs.writeShellScriptBin "hello" ''echo "hello, ryan!"''
```

To verify this, you can use `nix repl`, and you'll see that the result is indeed a Derivation:

```Nix
› nix repl -f '<nixpkgs>'
Welcome to Nix 2.13.5. Type :? for help.

Loading installable ''...
Added 19203 variables.

nix-repl> pkgs.writeShellScriptBin "hello" '' echo "hello, xxx!" ''
«derivation /nix/store/zhgar12vfhbajbchj36vbbl3mg6762s8-hello.drv»
```

