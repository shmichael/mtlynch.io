---
title: "Nix Develop"
date: 2023-07-07T21:30:28-04:00
draft: true
---

https://determinate.systems/posts/nix-direnv

Started here.

A bit of yak shaving, had to install direnv, had to hook direnv into my shell.

Installing direnv apt package was too old, got flake not found.

```text
use_flake: command not found
```

```bash
$ direnv --version
2.25.2
```

Guide not clear on how to create nix environment from scratch.

```bash
$ curl -sfL https://direnv.net/install.sh | bash

echo 'eval "$(direnv hook bash)"' >> ~/.bashrc
. ~/.bashrc
```

## Flox?

tried floxdev.com

Install was fine, but then the tutorials were for starting a project from scratch.

No guidance on adding flox to an existing project. No template for Go or Node.js.

## devbox

https://github.com/jetpack-io/devbox

Haven't tried it

Claims it solves the specific versioning problem

### direnv

First it didn't recognize use_flake, turned out direnv was too old (0.25).

Tried to create `.envrc` and `flake.nix`

Kept getting file not found.

Turned out I had to delete my flake.nix and run `flake init`.

Works until static linking, got to

https://nixos.wiki/wiki/Go

Hard because a lot of guides expect you to make Nix your build system rather than an optional tool for creating a dev environment. Don't want to jump full on into Nix.

Fixed in https://github.com/mtlynch/whatgotdone/pull/884

## How to pin specific versions?

https://github.com/NixOS/nixpkgs/issues/9682#issuecomment-658424656

Unclear how to express that in a Flake

not helpful: https://discourse.nixos.org/t/best-practice-for-pinning-version-of-individual-packages/6194/7

Use devbox: https://github.com/NixOS/nixpkgs/issues/93327#issuecomment-1648276095

https://news.ycombinator.com/item?id=28593823
