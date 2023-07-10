---
title: "Nix Develop"
date: 2023-07-07T21:30:28-04:00
draft: true
---

https://determinate.systems/posts/nix-direnv

Started here.

A bit of yak shaving, had to install direnv, had to hook direnv into my shell.

Guide not clear on how to create nix environment from scratch.

tried floxdev.com

Install was fine, but then the tutorials were for starting a project from scratch.

No guidance on adding flox to an existing project. No template for Go or Node.js.

### direnv

First it didn't recognize use_flake, turned out direnv was too old (0.25).

Tried to create `.envrc` and `flake.nix`

Kept getting file not found.

Turned out I had to delete my flake.nix and run `flake init`.

Works until static linking, got to

https://nixos.wiki/wiki/Go

Hard because a lot of guides expect you to make Nix your build system rather than an optional tool for creating a dev environment. Don't want to jump full on into Nix.
