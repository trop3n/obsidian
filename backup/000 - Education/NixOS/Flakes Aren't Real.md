#Nix #nixos #nixflakes 
# A Guide to Using Nix Flakes the Non-Flake Way
https://jade.fyi/blog/flakes-arent-real/

I think that Nix flakes have some considerable benefits, such as:

- Convenient pinning of evaluation-time dependencies
- Eliminating pointless rebuilds of code by only including tracked files in builds
- Making Nix code, on average, much more reproducible by pervasive pinning
- Allegedly caching evaluation
- Possibly making Nix easier to learn by reducing the amount of poking at strange attribute sets and general `NIX_PATH` brokenness

However, at the same time, there are a few things that one might be led to think about flakes that are not the most effective way of doing things. I personally use flakes relatively extensively in my own work, but there are several ways I use them that are not standard, with reason.

Flakes are *optional*, and as much as some people whose salary depends on it might say otherwise, they are not the (only) future of Nix: they are simply a special entry point for Nix code with a built-in pinning system, nothing more, nothing less.

Nix continues to gather a reputation for bad documentation, in part because the official documentation for nixpkgs and NixOS is *de facto* not allowed to talk about Flakes, as a policy. This situation is partially due to a divide between Nix developers and nixpkgs developers, which are groups with surprisingly little overlap. 

Flakes also are a symptom or cause of much intra-community strife between "pro-flakes" and "anti-flakes" factions, but this situation is at some level a sign of broken consensus processes and various actors trying to sidestep them, an assumption by many people that the docs are "outdated" for not using flakes, and the bizarre proliferation of flakes everywhere in blog posts or tutorials leading to a belief that they are required for everything.

This post is about how to architect Nix projects in general, with a special eye on how to do so with flakes while avoiding their limitations. It tries to dispel misconception that can develop in such a monoculture. 
## "Flakes are the Composition Primitive in Nix"



