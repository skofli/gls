# gls

[![made-with-Go](https://img.shields.io/badge/Made%20with-Go-1f425f.svg)](https://go.dev/)
[![GitHub go.mod Go version of a Go module](https://img.shields.io/github/go-mod/go-version/gomods/athens.svg)](https://github.com/ozansz/gls)
[![Linux](https://svgshare.com/i/Zhy.svg)](https://svgshare.com/i/Zhy.svg)
[![macOS](https://svgshare.com/i/ZjP.svg)](https://svgshare.com/i/ZjP.svg)

It’s `ls` + `du` + `tree` with interactive TUI on your terminal! `gls` is created to easily view, filter and search your files, folders and directories with their size whenever you need to open up some storage space. It wouldn’t be wrong to say that `gls` is a minimal yet powerful file manager CLI tool.

## Table of Contents

* [Installation](#installation)
* [Usage](#usage)
	+ [Default usage (TUI)](#default-usage-tui)
	+ [Text mode](#text-mode)
* [Features](#features)
	+ [TUI shortcuts](#tui-shortcuts)
	+ [Configuration](#configuration)
	+ [Command line arguments](#command-line-arguments)
* [How to Contribute](#how-to-contribute)

##  Installation
Installing `gls` on your machine is pretty simple: just clone the repo and install `cmd/gls.go`:

```bash
$ git clone https://github.com/ozansz/gls
$ cd gls
$ go install ./cmd/gls.go
```

After you run `go install` command, an executable file name `gls` is created in `$GOPATH/bin`. Now, you can simply run `gls` in terminal:

```bash
$ gls
```

## Usage
There are two running modes of `gls`: TUI and text-based.

The TUI mode is interactive and you will be able to use all of the [features](#features) of `gls`, such as searching by text/regular expression, traversing on the file tree, creating/opening/deleting files and many other things,  until you close the program.

The text mode however, is fairly simple and is a literal combination of running `tree` and `du` altogether, with some additional features.

### Default usage (TUI)
The command below runs `gls` with TUI, which is the default mode. It parses the file tree under the specified path along with the file and folder sizes on disk, then shows the tree view of the parsed tree.

```bash
gls -path ~/Downloads
```

![Screenshot of the TUI mode of gls](./img/gui-screenshot.png)

### Text mode
The command below does the same parsing process as the command above does. Except, this one just dumps the parsed tree as a the `tree` command does with the file/folder sizes and permissions, to the terminal.

```bash
gls -nogui -path ~/Documents
```

## Features
`gls` includes (and still continues to include more) several features that mimic a normal file manager:
* List the files and folders under the specified path, in tree view
* Show current file info: size on disk, permissions, path, MIME type and last modification
* Sort the tree by the size on disk
* Search files/folders by name, using both plaintext and regular expressions
* Ignore specific files/folders by using regular expressions, similar to `.gitignore` style
	* Default ignore file is `.glsignore`, but infinitely many other ignore files can be specified through the CLI [arguments](#command-line-arguments)
* Open files and folders by default programs or executables that you specify
* Copy/paste and move files and folders
* Remove files
* Create (similar to `touch`) and open files to edit
* Walk on the file tree, collapse and expand nodes easily

### TUI shortcuts

| Shortcut           | Command            | Description                                                                                                                                                                |
| ------------------ | ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `q`, `ESC`, `ˆC`        | quit               | Exits the program                                                                                                                                                          |
| `c`                  | collapse           | Collapses all nodes in the file tree view                                                                                                                                  |
| `e`                  | expand             | Expands all nodes in the file tree view                                                                                                                                    |
| `s`                  | search             | Opens modal to search nodes (files and folders) by name                                                                                                                    |
| `r`                  | regex search       | Same as search, but you can search using regular expressions                                                                                                               |
| `x`                  | restore            | Loads the original file tree view, mostly used after `search` and `regex search`                                                                                               |
| `o`                  | open               | Opens the selected (on hover) file/folder with the default program                                                                                                         |
| `p`                  | open               | Opens modal to specify the executable path which will be used to open the selected (on hover) file/folder                                                                  |
| `BACKSPACE` , `DEL`    | remove             | Removes the selected (on hover) file. Folder removal is currently not supported                                                                                            |
| `m`                  | mark               | Marks/unmarks the selected (on hover) file or folder. Marked nodes can be used later for `duplicate` and `move`                                                                |
| `u`                  | unmark             | Unmarks all the marked files and folders                                                                                                                                   |
| `n`                  | new                | Create and (optionally) open file **(will be available in next update)**                                                                                                       |
| `d`                  | duplicate          | Copy/pastes the marked files and folders to a specified destination. The destination is specified by the text input of the opened modal **(will be available in next update)** |
| `v`                  | move               | Moves the marked files and folders to a specified destination. The destination is specified by the text input of the opened modal **(will be available in next update)**       |
| `TAB`, `SPACE`, `ENTER`  | toggle expand node | Expands the node if currently collapsed, and vice versa, the selected (on hover) file or folder                                                                            |
| `ARROW KEYS`, `SCROLL` | navigate           | Navigates between nodes in the file tree view                                                                                                                              |

### Configuration

You can freely change the key bindings and shortcuts or configure the program for your needs from `gui/core.go` .

After your changes, run

```bash
go build cmd/gls.go
```
in the project directory.

In addition, if you think that your configurations or other changes seem necessary to improve the project, your contributions will be welcomed :)

### Command line arguments

```bash
-debug
    	Increase log verbosity
-fmt string
   		size formatter, one of bytes, pow10 or none (default "bytes")
-ignore string
    	Comma-separated ignore files that specify which files folders to exclude
-nogui
    	text-only mode
-path string
    	path to run on (required)
-sort
    	sort nodes by size (default true)
-thresh string
    	size filter threshold, e.g. 10M, 100K, etc.
```
> You can also read this section from terminal by using `gls` without parameters.

## How to Contribute

You are very welcome to contribute to `gls`! Here are a few steps to guide you how to start contributing:

1. Check [the open issues tab](https://github.com/ozansz/gls/issues) to see if there are any issue you may be interested in fixing. You can also list the [issues with only the good-first-issue tag](https://github.com/ozansz/gls/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22)

2. Check the [contributing guide](CONTRIBUTING.md) for more explanation on setting up the development environment, opening the PR, etc.