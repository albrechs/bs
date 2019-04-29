# bs: Bash build system

bs allows you to create build scripts using simple shell scripting.

## Installation

### Linux, Mac OSX, or Windows WSL
```
git clone git@github.firstrepublic.com:leilers/bs.git bs
sudo bash ./bs/install.sh
```

### Wndows PowerShell

On Windows, even if you use PowerShell as your terminal, you need a bash shell to run your command scripts. The most commonly available one is [Git BASH](https://gitforwindows.org/) (comes with Git for Windows).

Open PowerShell as administrator, and run:

```
git clone git@github.firstrepublic.com:leilers/bs.git bs
.\install.cmd
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