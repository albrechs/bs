# bs: Bash build system

Use simple bash scripts instead of a "real" build system.

## Why?
Pretty much all build systems are terrible in their own special way:

* Many build systems are designed for large, complicated projects, while many modern projects are small and granular, and don't need the complexity. 
* On the other hand, some alternatives to build systems (i.e. npm scripts) are so simple that they require shell scripts to do anything non-trivial, but this makes it hard to be cross-platform.
* Pretty much any "real" build system requires installing dependencies (i.e. Ruby for rake, node.js for grunt/gulp, Java for Maven, etc). You can't depend on any given build system's dependencies being installed on any given developer or build machine.
* Many build systems are plugin-oriented, which adds a lot of complexity when trying to add even simple functionality, especially when all you need is a one-liner to shell out to another program.
* Many build systems are built in languages that aren't well suited to simple build tasks (i.e. they require a lot of boilerplate to shell out to an executable, or are designed for asynchronicity by default).
* In a world where every language has its own idiomatic build system (or multiple ones), polyglot programmers are left to learn the intricacies of a lot of different systems. Pretty much every developer hates every other developer's choice of build system.

Just using bash scripts is an improvement in a few ways:

* Bash is ubiquitous. Between Linux, OSX, and Windows (between Mingw/Cygwin/Git Bash/WSL), its extremely likely that bash is already installed on any environment you use. Because of Git for Windows, practically every Windows developer already has bash installed.
* Bash is good enough. Its simple and well suited to build scripts. Its simple for simple things, and especially good at running executables, copying files around, or calling scripts in other languages (i.e. node.js or python) for more complex tasks.
* You probably already know Bash. No one is going to argue its the best language available, but it is a language that pretty much every developer needs to learn at some point, regardless of what languages you specialize in.

bs is supposed to be the thinnest possible layer on top of straight-up bash scripts. Running this:

`./bs/build.sh`

can be made into a bit fewer keystrokes with bs:

`bs build`

That's pretty much it.

## Installation

### For use with bash on Linux, Mac OSX, or Windows (via [WSL](https://docs.microsoft.com/en-us/windows/wsl/about) or [Git BASH](https://gitforwindows.org/))

Open a bash prompt and run:

```
bash <(curl -s https://raw.githubusercontent.com/labaneilers/bs/master/install.sh)
```

### Windows PowerShell

On Windows, even if you use PowerShell as your terminal, you need a bash shell to run your command scripts. The most commonly available one is [Git BASH](https://gitforwindows.org/) (comes with Git for Windows).

Open PowerShell as administrator, and run:

```
. { iwr -useb https://raw.githubusercontent.com/labaneilers/bs/master/install.ps1 } | iex
```

## Usage

```
bs <command> [<args>]
bs [<default-commmand-args>]
```

### Getting started

Create a `./bs` directory in your repository root, and implement commands by adding `*.sh` scripts to `./bs` with the name of the command. For example:

```
bs publish
```

will call:

```
./bs/publish.sh
```

### Passing arguments

Additional arguments can be passed, and will be received by command scripts as `$1`, `$2`, etc. For example:

```
bs publish --mode Release -v
```

will call:

```
./bs/publish.sh --mode Release -v
```

### Default commands

You can define a default script at `./bs/default.sh`, which will be called when the argument passed for `<command>` doesn't match any script in `./bs`.

```
bs restore --all --no-cache
```

will call:

```
./bs/default.sh restore --all --no-cache
```