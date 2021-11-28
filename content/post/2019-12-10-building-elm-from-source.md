+++
title = "Compiling Elm From Source"
description = "How to build elm from source"
date = 2019-12-10T18:20:00+03:00
tags = ["howto", "freebsd"]
draft = false
+++

For the past 2 weeks I've been experiencing unique problems when working with Elm on my FreeBSD workstation. `elm reactor` was displaying an empty white page on the browser. Here, I was using `hs-elm-0.19.0` from the upstream ports collection. To remedy this, I decided to use the Elm linux binary and brand it as a linux binary in order to distinguish it from a FreeBSD ELF binary. Doing this was simple; just download the binary and run: `brandelf -t Linux <path-to-elm-binary>/elm`. However, this came with it's own weird problem: executing simple commands in the elm repl threw errors and then abruptly quit. The only reasonable thing to do now was to compile Elm(which FYI I've got around to doing today) from source which this post is about.

To compile elm from source, you need to have `ghc` and `cabal` installed in your system. First, clone the Elm compiler and `cd` into it:

```bash
git clone https://github.com/elm/compiler.git && cd compiler
```

Thereafter create a cabal sandbox. This will create a sandbox environment in '.cabal.sandbox' which will host all the built binaries. You can then simply build the packages. This whole process will look something like this:

```bash
# Create the sandbox
cabal sandbox init

# Build Elm
cabal install


# In case you get an error during the cabal install,
# You can run:
# cabal install --force-reinstalls
```

Now all your binaries will be in '.cabal-sandbox/bin/elm'. You can now copy this to '_usr/local/bin_' to make it available system-wide.
