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

This is a collection of commands I'm using on my linux machine as a python developer. It is a structured documentation of the commands I'm using throughout interactive shell sessions.

# Contents

1. [Shell Expansions, Shell Operators](#shell-expansions-shell-operators)
   * [Shell Expansions](#shell-expansions)
   * [Shell Operators](#shell-operators)
2. [Basic Commands](#basic-commands)
   * [Beginner](#beginner)
     * [navigation]()
   * [Intermediate](#intermediate)
   * [Advanced](#advanced)
3. [Command Line Tools](#command-line-tools)
   * [Git](#git)
   * [Anaconda](#anaconda)
   * [Docker](#docker)
   * [LSDeluxe](#lsdeluxe)
4. [Aliases](#aliases)
5. [Shortcuts](#shortcuts)
   * [Terminal](#terminal) 
   * [Chromium Browser](#chromium-browser) 
   * [VSCode](#vscode) 
6. [Shell Scripting](#shell-scripting)
   * [Bash in a Nutshell](#bash-in-a-nutshell)
   * [Variables](#variables)
   * [Loops](#loops)
   * [Functions](#functions)
   * [Condtionals](#conditionals)
7. [Raspberry Pi](#raspberry-pi)


I use the alias `marcopolo` to reach this cheat sheet faster:

```bash
echo "\nalias marcopolo='xdg-open https://github.com/NiklasTiede/cheatsheet'" >> ~/.bashrc
source ~/.bashrc
```

---

# Shell Expansions, Shell Operators

## Shell Expansions

Expansions are performed by the shell before the command is executed. Tilde and filename expansion are used more frequently when interacting with the shell. Brace, variable and arithmetic expansion tend to be used more often while doing shell scripting.

The tilde `~` expands to the environment variable `$HOME`, which is usually the home directory. If `$HOME` is not defined, tilde `~` expands with the home directory by default.

```bash
$ echo ~
/home/username
```

Filename expansion is a way to select easily a number of files or directories from within the current working directory as arguments for a command. This is accomplished by pattern matching: A so-called glob pattern containing wildcard characters is used to specify the files or directories. The wildcard characters can represent any of the 128 ASCII characters and can be less specific (`*` or `?`) or more specific (`[...]`)

| Wildcard Character | Description | 
|--|--|
| `*` | Matches any number of any characters |
| `?` | Matches any single character |
| `[...]` | Matches any one of the enclosed characters |

Examples:

```bash
$ ls
file1.go  file2.go  file3.py  file4.py  file40.py

$ ls *.py
file3.py  file4.py  file40.py

$ ls file?.py
file3.py  file4.py

$ ls file[0-3].*
file1.go  file2.go  file3.py
```

The lesser known extended globbing (like `*(pattern)`), is used more commonly in shell scipting than in interactive shell sessions. The same applies for brace, variable and arithmetic expansions which are explained within the [Shell Scripting](#shell-scripting) section.

**[⬆ back to top](#contents)**

---

## Shell Operators

Shell operators let you combine commands which expands your toolbelt vastly. They can be divided into two categories: redirection and control operators. Control operators allow for coupling commands. 

| Token | Example | Description | 
|--|--|--|
| `|` | `history | grep "patt"` | Pipelining: direct output of com1 to com2 
| `&` | `python myscript.py &` | Execute command in background |
| `&&` | `com1 && com2` | Execute com2 only if com1 is executed |
| `;` | `com1; com2` | Execute both commands always |

Especially the pipe operator `|` here shines. Any output printed by command1 is passed as input to command2. 

Examples:

```bash
$ ls | head -3

$ cat filename | grep 'pattern'
```

---

Whereas redirection operators direct the output of a command to another command.

| Token | Example | Description | 
|--|--|--|
| `>` or `<` | `echo '#projectname' > README.md` | Direct output of com1 to com2 or vice versa |
| `>>` or `<<` | `echo 'source x' >> ~/.bashrc` | append output |

Examples:

```bash
$ echo 'alias=' >> ~/.bashrc

$ more good examples
```

These operators and shell expansions will be found throughout this cheat sheet repeatedly.

**[⬆ back to top](#contents)**

---

# Basic Commands

Linux distributions contain a plethora of powerful built-in commands.

## Beginner

Navigation on the file system:

```bash
cd <directory>  # change directory
cd ..           # goes on folder up
ls              # list cotent of current wokring dir
ls -la          # Display all and extended file metadata
pwd             # print working directory
```

If you're not aware of a commands capabilities you can add the `--help` flag to display all options. The `--version` flag returns the version number.

```bash
<command> --help
<command> --version
```

All built-in commands have manual pages

```bash
man <command>  # shows a manual (man pages)
info <command>  # 
whatis <command>  # 
```


```bash
sudo du -sh <file/dir>  # shows size of specified file/dir
sudo du -sh *   # shows the size of all files/folders
df -h # shows all memory usage on filesystem
file *   # lists the types of all files
which <command>  # returns path to the programs binary
which brew, which go, which python, which ls
```

```bash
date  
jobs 
kill %N
ps
```

```bash
clear  # clears the terminal
history            # prints the list of all historically used commands
ctrl + r           # search bar for commands typed (existent in history)
```


file editing

```bash
touch <file>       # creates a empty, new file
rm <file_name>                       # removes a file from current 
rm -i <file>                         # -i flag adds a "are your sure?" prompt
nano ./<file>      # opens the file (nano is a terminal application for text editing)
ctrl + O           # saves the file
ctrl + X           # leaves file
ctrl + c           # terminates the current process
ctrl + d           # terminates shell-like sessions (mongo, sql, python etc)
less -S <file>     # less (editor) prevents wrapping around, better representation

head <file>        # prints the first 10 lines of a file
head -n 5 <file>   # prints first 5 lines
tail <file>        # shows last 10 lines
cat 

wc <file>          # word count, gives number of lines, words and characters of the file

cat <fi1> <fi2>    # concatenates files and sends them to the standard output stream (usually the terminal)
```


updating the system

```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get autoremove
```

decompress:

```bash



```

operating with folder, create, delete etc.

```bash
mkdir <folder_name>                  # in current directory
mkdir -p a/b/c                       # creates a directory tree
tree -L 2                            # visualized directories as tree's. -L restricts the tree to two levels (default: complete tree)
rmdir <path>                         # removes directory
rm -rf                               # forces to remove a directory with all its content
```


```bash
cp <file> <path>/<new_filename>      # copies a file to advised path

ln <target> <new_link>               # creates a hard link to a file (hard links show to the actual bytes in memory)
ln -s <target> <new_link>            # creates a soft link to a file (soft links point to the file which references to the place in memory)

```


```bash
sudo chown user:group <file.txt>     # changes the file permissions of a file
chmod +x <ba_scr.sh>                 # makes the bash-script executable
```

cut
grep
find
sed
awk


```bash
printenv
printenv HOME
echo $HOME

```


```bash

```


```bash

```


```bash

```


```bash

```



```bash

```


```bash

```

apt - package managemtn tool

```bash
apt-get install <tool>            # package management tool
sudo apt-get remove <program_name>   # removes the program

apt-cache search <program_name>*     # search for everything containing the word in the rep. example: apt-cache search gimp*
```


## Intermediate


```bash
cat /proc/cpuinfo  # provides all kinds of information toward each virtual cpu core
```

## Advanced

pretty useful combinations:

If you wanna sort your command history to see which commands you use most often:

```bash
history | sed -e 's/ *[0-9][0-9]* *//' | sort | uniq -c | sort -rn | head -10
```






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

# Command Line Tools

Before we can use a tool, we have to use a package managagent system to install these tools. Linux distributions use different package managers, I use Ubuntu 20.04 LT so I'm using `apt` `snap` and `homebrew` to install packages. 

apt - package managemtn tool

```bash
apt-get install <tool>            # package management tool
sudo apt-get remove <program_name>   # removes the program

apt-cache search <program_name>*     # search for everything containing the word in the rep. example: apt-cache search gimp*
```



## Git


**[⬆ back to top](#contents)**

---

# Aliases

make asliase to increase prodictivity 

```bash
unalias lc
```


**[⬆ back to top](#contents)**

---

# Shortcuts

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

# Shell Scripting

For Shell scripting I can only recommend the excellent cheat sheet of [devhints.io](https://devhints.io/bash). 

In the following I will just explain the most important things, I also I more regurlarly.

important shebang lines: what is a shebang line and why do they exist?

`#!/bin/bash`
`#!/bin/sh`
`#!/usr/bin/env python`



**[⬆ back to top](#contents)**

---

# Raspberry Pi



**[⬆ back to top](#contents)**

