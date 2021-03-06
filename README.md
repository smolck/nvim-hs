# nvim-hs

Neovim API for Haskell plugins as well as a plugin provider.
This library and executable should provide a basis for developing
plugins. This package should only contain broadly useful interfaces
to write plugins for neovim in haskell. The design goal is to create
an easy to use API that avoids most of the boilerplate while still retaining
some sense of reliability and type safety. Since Template Haskell is used
to generate the neovim bindings and to avoid some of the boilerplate
handy work, some exotic operating systems and architectures may not work.

[![Build Status](https://travis-ci.org/neovimhaskell/nvim-hs.svg?branch=master)](https://travis-ci.org/neovimhaskell/nvim-hs)
[![Hackage version](https://img.shields.io/hackage/v/nvim-hs.svg?style=flat)](https://hackage.haskell.org/package/nvim-hs)
[![nvim-hs on latest Stackage LTS](http://stackage.org/package/nvim-hs/badge/lts)](http://stackage.org/lts/package/nvim-hs)
[![nvim-hs on Stackage Nightly](http://stackage.org/package/nvim-hs/badge/nightly)](http://stackage.org/nightly/package/nvim-hs)

# What do I have to expect if I were to use it now?

Check the issue list here on github.

# How do I start using this?

You need to install a neovim plugin that manages starting of `nvim-hs` plugins.
Just follow the instructions here:
[nvim-hs.vim](https://github.com/neovimhaskell/nvim-hs.vim)

Once you have installed that plugin, you can use `nvim-hs` plugins as you would
normal vim plugins. Every plugin is started as a separate process which should
be fine unless you have a lot of them.

You only have to read on if you want to start "scripting" functions or plugins
yourself in Haskell.

# Scripting with Haskell

The entry point for all Haskell-based scripts is a plugin.
An `nvim-hs` plugin is a plain Haskell project with two conventions:

1. You need an executable that starts a `msgpack-rpc` compatible client.

2. You need a tiny bit of `vimL` in your runtime path that starts the plugin.

The simplest way to get started is the stack template from this
repository/package inside your neovim configuration folder which
will be described here. (Alternatively, you can manually create a project
and do everything that is explained in `:help nvim-hs.txt` which should be
available if you installed the plugin mentioned in the previous section.)

You need to [install stack](https://docs.haskellstack.org/en/stable/README/)
and have the neovim executable on the path.
(The API code generation calls `nvim --api-info`.)

Afterwards, you switch to your neovim configuration folder (typically `~/.config/nvim`) and
you have to create your plugin project.

> cd ~/.config/nvim

> stack new my-nvim-hs https://raw.githubusercontent.com/neovimhaskell/nvim-hs/master/stack-template.hsfiles --bare --omit-packages --ignore-subdirs

If you start neovim now, it will compile the example plugins which may take a
few minutes. Once it is started you can use the predefined functions from the
template.

> :echo NextRandom()

should print a random number.

To start writing your own functions and plugins, read through the files
generated by the template accompanied by the
[library documentation on hackage](http://hackage.haskell.org/package/nvim-hs).

# Contributing

Documentation, typo fixes and alike will almost always be merged.

If you want to bring forward new features or convenience libraries
for interacting with neovim, you should create an issue first. The features
of this (cabal) project should be kept small as this helps
reducing the development time. (For some tests it is
necessary to issue `cabal install`, so any change to to a module can
significantly increase the compilation time.)
If your idea solves a general problem, feel free to open an issue in the
library project of nvim-hs:
[nvim-hs-contrib](https://github.com/neovimhaskell/nvim-hs-contrib)

