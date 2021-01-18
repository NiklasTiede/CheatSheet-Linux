<!-- translation
[English](README.md) | [Tiếng Việt](README-vn.md) | [简体中文](README-cn.md) -->

<!-- genereal ideas:
* theme specific
* powerful cheats in general
* the whole design is done in a cool manner
* maybe hosting a website and stylyying it for cheat sheets

concrete ideas:
* rdkit cheat sheet!
* important python standard libs cheat sheets
* termux, raspi

dotfiles -->

# Cheat sheet (Linux)

This is a collection of commands I'm using on my linux machine as a python developer. 

I use the alias `marcopolo` to reach this cheat sheet faster:

```bash
echo "\nalias marcopolo='xdg-open https://github.com/NiklasTiede/cheatsheet'" >> ~/.zshrc
source ~/.zshrc
```

# Contents

1. [Operators, Shell Expansions](#Operators,-Shell-Expansions)
2. [Basic Commands](#Basic-Commands)
      * [Beginner](#Beginner)
      * [Intermediate](#Intermediate)
      * [Advanced](#Advanced)
3. [Command Line Tools](#Command-Line-Tools)
      * [git]()
      * [anaconda]()
      * [docker]()
      * [LSDeluxe]()
      * [git]()
4. [Aliases](#Aliases)
5. [Shortcuts](#Shortcuts)
      * [Terminal](#Terminal) 
      * [Chromium Browser](#Chromium-Browser) 
      * [VSCode](#VSCode) 
6. [Shell Scripting](#Shell-Scripting)
      * [Bash in a Nutshell]()
      * [variables](#)
      * [loops](#)
      * [functions](#)
      * [condtionals](#)
7. [Raspberry Pi](#Raspberry-Pi)

---


# 1. Operators, Shell Expansions

tilde expansion ~ --> $HOME
filename expansion (*, ?, [0-9]/[a-z])


| Symbol | Example | Description | 
|--|--|--|
| `&` |  |  |
| `;` | `com1; com2` | executing  |
| `&&` | `com1 && com2` | chaining |
| `>` |  |  |
| `>>` | `echo 'source x' >> ~/.bashrc` |  |
| `|` |  | pipelining |
|  |  |  |


**[⬆ back to top](#contents)**

---

# 2. Basic Commands (GNOME)

basic navigation on the system:
## Beginner
## Intermediate
## Advanced
help


```bash
pwd
ls
cd
clear
history | tail
df -h  
```

```bash
help   # 
<command> --help   # 
man <command>   # 
info <command>   # 
whatis <command>
which <command>   #  
locate <command>  #

file *             # lists the types of all files
```


using filename expansion, globbing, shell expansion, wildcard characters

searching for string pattern in all files:
grep, good for pipelining and searching through files

```bash
#  print only names of files containg the pattern from cwd:
grep -rl 'patt'

# shows also each line where pattern is occuring:
grep -rnw '/path/' -e 'patt'

# search through all files recursively
grep -rnw 'patt' 

# searches only certain files for the search pattern
grep -rnw -e 'patt' --include=*.py   

-r recursive
-l only filenames
-n numbber of line within file
-w only whole word
--include only certain files included
```


 environment variables:
 
```bash
printenv      # 
echo $PATH      # 
      # 
      # 
      # 
```

text

```bash
      # 
      # 
      # 
      # 
      # 
```


**[⬆ back to top](#contents)**

---

# 3. Command Line Tools (3rd party)

text

**[⬆ back to top](#contents)**

---

# 4. Aliases

make asliase to increase prodictivity 


**[⬆ back to top](#contents)**

---

# 5. Shortcuts

Terminal Shortcuts on Linux
|  Shortcut |  Meaning |
|---|---|
| <kbd>Ctrl</kbd> <kbd>Alt</kbd> <kbd>T</kbd> | open terminal |  
| <kbd>Ctrl</kbd> <kbd>Shift</kbd> <kbd>Q</kbd> | close terminal | 
| <kbd>Tab</kbd> | autocomplete, navigation | 
| <kbd>Ctrl</kbd> <kbd>Shift</kbd> <kbd>Up</kbd> or <kbd>Down</kbd> | scrolling up, down |
| <kbd>Ctrl</kbd> <kbd>R</kbd> | search history |
|  |  |
|  |  |
|  |  |

**[⬆ back to top](#contents)**

---

# 6. Shell Scripting

important shebang lines: what is a shebang line and why do they exist?

`#!/bin/bash`
`#!/bin/sh`
`#!/usr/bin/env python`

**[⬆ back to top](#contents)**

---

# 7. Raspberry Pi



**[⬆ back to top](#contents)**






---

# Basic Syntax

## Hello World

File `hello.go`:
```go
package main

import "fmt"

func main() {
    fmt.Println("Hello Go")
}

```

`$ go run hello.go`


|Operator|Description|
|--------|-----------|
|`==`|equal|
|`!=`|not equal|
|`<`|less than|
|`<=`|less than or equal|
|`>`|greater than|
|`>=`|greater than or equal|


```go
var i int = 42
var f float64 = float64(i)
var u uint = uint(f)

// alternative syntax
i := 42
f := float64(i)
u := uint(f)
```


```go
ls -la
var i int = 42
var f float64 = float64(i)
var u uint = uint(f)

// alternative syntax
i := 42
f := float64(i)
u := uint(f)
```
