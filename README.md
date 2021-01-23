<!-- translation
[English](README.md) | [Tiếng Việt](README-vn.md) -->

# Cheat Sheet (Linux)

This is a collection of commands I'm using on my linux machine (Ubuntu 20.04.1 LTS) as a python developer. It is a structured documentation of the commands I'm using throughout interactive shell sessions. Caution, this abstract is highly opinionated :wink:

# Contents

1. [Shell Expansions, Shell Operators](#shell-expansions-shell-operators)
   - [Shell Expansions](#shell-expansions)
   - [Shell Operators](#shell-operators)
2. [Built-in Commands](#built-in-commands)
   - [Filesystem Navigation](#filesystem-navigation)
   - [Filesystem Exploration](#filesystem-exploration)
   - [Create, Delete, Copy, and Link](#create-delete-copy-and-link)
   - [Working with File Content](#working-with-file-content)
   - [System Updates](#system-updates)
   - [Data Compression](#data-comrpession)
   - [](#)
   - [](#)
   - [](#)
   - [](#)
   - [](#)
3. [Command Line Tools](#command-line-tools)
   - [Git](#git)
   - [Anaconda](#anaconda)
   - [Docker](#docker)
   - [LSDeluxe](#lsdeluxe)
4. [Aliases](#aliases)
5. [Shortcuts](#shortcuts)
   - [Terminal](#terminal)
   - [Chromium Browser](#chromium-browser)
   - [VSCode](#vscode)
6. [Configuration](#configuration)
7. [Shell Scripting](#shell-scripting)
   - [Bash in a Nutshell](#bash-in-a-nutshell)
   - [Variables](#variables)
   - [Loops](#loops)
   - [Functions](#functions)
   - [Condtionals](#conditionals)
8. [Raspberry Pi](#raspberry-pi)

I use the alias `marcopolo` to reach this cheat sheet faster:

```bash
echo "\nalias marcopolo='xdg-open https://github.com/NiklasTiede/cheatsheet'" >> ~/.zshrc
source ~/.zshrc
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

| Wildcard Character | Description                                |
| ------------------ | ------------------------------------------ |
| `*`                | Matches any number of any characters       |
| `?`                | Matches any single character               |
| `[...]`            | Matches any one of the enclosed characters |

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

| Token | Example                  | Description                                 |
|-------|--------------------------|---------------------------------------------|
| `\|`  | `history \| grep "patt"` | Pipelining: direct output of com1 to com2   |
| `&`   | `python myscript.py &`   | start child process (execute in background) |
| `&&`  | `com1 && com2`           | Execute com2 only if com1 is executed       |
| `;`   | `com1; com2`             | Execute both commands always                |


Especially the pipe operator `|` here shines. Any output printed by command1 is passed as input to command2.

Examples:

```bash
$ ls | head -3

$ cat filename | grep 'pattern'
```

---

Whereas redirection operators direct the output of a command to another command.

| Token        | Example                           | Description                                 |
| ------------ | --------------------------------- | ------------------------------------------- |
| `>` or `<`   | `echo '#projectname' > README.md` | Direct output of com1 to com2 or vice versa |
| `>>` or `<<` | `echo 'source x' >> ~/.bashrc`    | append output                               |

Examples:

```bash
$ echo 'alias=' >> ~/.zshrc

$ more good examples
```

These operators and shell expansions will be found throughout this cheat sheet repeatedly.

**[⬆ back to top](#contents)**

---

# Built-in Commands

Linux distributions contain a plethora of powerful built-in commands. The presented commands are sorted by topic. If you're not aware of a commands capabilities you can add the `--help` or `-h` flag to display all options. The `--version` or `-v` flag returns the version number and is commonly used right after installation to check a programs version.

```bash
<command> --help
<command> --version
```

## Filesystem Navigation

Navigation on the file system is the first step towards learning how to utilize the power of a Linux system. Notice: <kbd>Tab</kbd> enables auto completion of file-/dirnames and saves valuable time!

```bash
ls                # list content of current working dir
ls -la            # Display all files and extended file metadata

cd <directory>    # change directory
cd ..             # goes on folder up

pwd               # print working directory
```

Since most people (like me) don't have a photographic memory, it's always a good choice to use the machines memory.

```bash

history           # prints a list of all historically used commands
history | tail    # prints 10 recently used commands

clear             # clears the terminal
```

Pressing arrow keys <kbd>⬆️</kbd> <kbd>⬇️</kbd> or <kbd>Ctrl</kbd> <kbd>R</kbd> (search bar) is my preferred choice. BTW: I geared the shell towards my needs (see [configuration](#configuration)) so everything looks pretty satisfying.

## Filesystem Exploration

Wanna get more information about a commands features? Look into the manual pages or use `whatis` if time is tight. `which` can clear things up about a commands origin on the filesystem.

```bash

man <command>           # shows a manual (man pages)
whatis <command>        # returns a one-line description

which <command>         # returns path to the programs binary
file *                  # lists the types of all files
```

File space estimation:

```bash

sudo du -sh <file/dir>  # shows size of specified file/dir
sudo du -sh *           # shows the size of all files/folders
df -h                   # shows all memory usage on filesystem
```

## Create, Delete, Copy, and Link

Some basic operations when working with files and directories.

```bash

touch <file>            # creates an empty file

rm <file_name>          # removes a file
rm -rf                  # forces to remove a directory with content recursively

mkdir <dir_name>        # create directory
mkdir -p a/b/c          # creates a directory tree
mkdir file{1..5}       # creates 5 enumrated files

rmdir <dir_name>        # removes a directory
```

Files oand directories can be copied or linked. Hard links point to the files in memory directly whereas soft links point to the file which references to the place in memory.

```bash

cp <file> <path/new_filename>  # copies a file to the advised path

ln <target> <new_link>         # creates a hard link to a file
ln -s <target> <new_link>      # creates a soft link to a file
```

## Working with File Content

There are several commands to see the content of a file without opening it with an editor.

```bash

head <file>       # prints the first 10 lines of a file
head -n 5 <file>  # prints the first 5 lines
tail <file>       # shows last 10 lines
cat <file>        # prints content of a file

wc <file>         # word count, returns number of lines, words and characters
```

When changing the content of a file, it's best to use an editor. Nano is an into the terminal integrated file editor. I'm using it when surfing between files and making minor changes. For writing bigger pieces of code I'm using VSCode as my IDE. Efficiency of editing is improved by usage of [shortcuts](#shortcuts).

```bash

nano <file>      # opens the file (nano is a terminal application for text editing)
code <file>      # open file in VSCode
```

## System Updates

Always keep your system up to date :wink:

```bash

sudo apt update
sudo apt upgrade
sudo apt autoremove
```

```bash

sudo 
ctrl
reboot, shutdown


```



## Data Compression

Compression is always a space-time complexity tradeoff. On linux systems many files are collected usually into one archive file, referred to as a tarball. `tar` is the tool of choice for compression and decompression.

```bash
tar -ztvf filename.tar.gz         # list content

tar -zxvf filename.tar.gz         # decompression 
tar -zxvf filename.tar.gz <path>  # decompressed into target  folder

tar -cvzf filename.tar.gz <path>   # compression of a folder, returns filename.tar.gz
```


## Ownership and Permissions

Changing a files permissions is sometimes crucial when working on a linux system.These access permissions control who can access what files, and provides a fundamental level of security to the files

3 permission groups
1 owner
2 group
3 other

```bash
ls -l           # 

sudo chown user:group <file.txt>     # changes the file permissions of a file

chmod +x <ba_scr.sh>                 # makes the bash-script executable
```

## Environment Variables

Environment variables are key-value pairs on the system that can be retrieved by applications. They're used to ensure separation of concerns. Important default Environment variables are `$HOME`, `$SHELL` and `$PATH`. HOME defines the systems home directory. PATH tells the shell which directories to search for executable files. Multiple values assigned to a variable must be separated by a colon `:`. By convention, environment variables should have UPPER CASE names.

```bash
printenv           # prints all environment variables
printenv HOME      # prints the value of a specified env var
echo $HOME         # same as above
```

For instance credentials can be separated from code as environment variables (or within files). The creation of new env vars can be achieved by the `export` command. To set a env var for the current user permanently it has to be appended to your .bashrc or .zshrc file.

```bash

export VARNAME="value"                         # set in current shell
echo 'export VARNAME="value"' >> ~/.bashrc     # set permanently in all bash sessions
sudo -H nano /etc/environment                  # set system wide, no export-keyword used
```

## cut grep find etc

cut
grep
find
sed
awk

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

pretty useful combinations:

If you wanna sort your command history to see which commands you use most often:
sort can be nicely used!

```bash

history | sed -e 's/ *[0-9][0-9]* *//' | sort | uniq -c | sort -rn | head -10
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




package managemtn tools, see in the [command line tools]() section

## jobs, processes

```bash
date
jobs
kill %N
ps
```

If you start a script (shell, python etc.) and you logout then the process is killed. Nohup helps to continue the script in the background, even after shell logout

```bash

commandname &              # executes command in the background 
nohup commandname &        # command is executed even if shell session is finished
nohup python myscript.py & # example

tee               # read from stdin and writes to stdout and a file
tee -a     # append
python myscript.py | tee ~/myscript_output.txt & # 
python myscript.py | tee ~/myscript_output.txt > /dev/null & # if dont want tee to write to stdout -> write it to dev/null !

```



## Cron jobs

```bash

```

```bash

```

## check cpu, gpu

```bash
cat /proc/cpuinfo  # provides all kinds of information toward each virtual cpu core
```


text

```bash
      #
      #
      #
      #
      #
```

## ssh

text

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

## Anaconda

## LSDeluxe

## tree, Tokei, misc


wanna generate a password? use openssl! the cryptographers tool
```bash
openssl rand -hex 12
```

tree -L 2 # visualized directories as tree's. -L restricts the tree to two levels (default: complete tree)
ls --tree # recurses into every dir

**[⬆ back to top](#contents)**

---

# Aliases

Aliases save time and work wonders on lengthy commands. Here's a list of my aliases.

```bash
alias name="command flags"


unalias lc

# list all commands
echo -n $PATH | xargs -d : -I {} find {} -maxdepth 1 \
        -executable -type f -printf '%P\n' | sort -u
# list all aliases:
ALIASES=`alias | cut -d '=' -f 1`
    echo "$COMMANDS"$'\n'"$ALIASES" | sort -u



```

**[⬆ back to top](#contents)**

---

# Shortcuts

terminal, nano, chromium, vscode

Terminal Shortcuts

| Shortcut                                                        | Meaning                  |
| --------------------------------------------------------------- | ------------------------ |
| <kbd>Ctrl</kbd> <kbd>Alt</kbd> <kbd>T</kbd>                     | Open terminal            |
| <kbd>Ctrl</kbd> <kbd>Shift</kbd> <kbd>Q</kbd>                   | Close terminal           |
| <kbd>Tab</kbd>                                                  | autocomplete, navigation |
| <kbd>Ctrl</kbd> <kbd>Shift</kbd> <kbd>⬆️</kbd> or <kbd>⬇️</kbd>   | Ccrolling up, down       |
| <kbd>Ctrl</kbd> <kbd>R</kbd>                                    | Search history bar       |
|                                                                 |                          |
|                                                                 |                          |
|                                                                 |                          |

```bash

nano <file>      # opens the file (nano is a terminal application for text editing)
ctrl + O           # saves the file
ctrl + x           # leaves file
ctrl + c           # terminates the current process
ctrl + d           # terminates shell-like sessions (mongo, sql, python etc)
ctrl + w           # search file for pattern
```

| Shortcut                                                        | Meaning                  |
| --------------------------------------------------------------- | ------------------------ |
| <kbd>Ctrl</kbd> <kbd>Alt</kbd> <kbd>T</kbd>                     | open terminal            |
| <kbd>Ctrl</kbd> <kbd>Shift</kbd> <kbd>Q</kbd>                   | close terminal           |
| <kbd>Tab</kbd>                                                  | autocomplete, navigation |
| <kbd>Ctrl</kbd> <kbd>Shift</kbd> <kbd>⬆️</kbd> or <kbd>⬇️</kbd>   | scrolling up, down       |
| <kbd>Ctrl</kbd> <kbd>R</kbd>                                    | search history bar       |
|                                                                 |                          |
|                                                                 |                          |
|                                                                 |                          |



Chromium Shortcuts

| Shortcut                                                        | Meaning                  |
| --------------------------------------------------------------- | ------------------------ |
| <kbd>Ctrl</kbd> <kbd>Alt</kbd> <kbd>T</kbd>                     | open terminal            |
| <kbd>Ctrl</kbd> <kbd>Shift</kbd> <kbd>Q</kbd>                   | close terminal           |
| <kbd>Tab</kbd>                                                  | autocomplete, navigation |
| <kbd>Ctrl</kbd> <kbd>Shift</kbd> <kbd>⬆️</kbd> or <kbd>⬇️</kbd>   | scrolling up, down       |
| <kbd>Ctrl</kbd> <kbd>R</kbd>                                    | search history bar       |
|                                                                 |                          |
|                                                                 |                          |
|                                                                 |                          |

VSCode

| Shortcut                                                        | Meaning                  |
| --------------------------------------------------------------- | ------------------------ |
| <kbd>Ctrl</kbd> <kbd>Alt</kbd> <kbd>T</kbd>                     | open terminal            |
| <kbd>Ctrl</kbd> <kbd>Shift</kbd> <kbd>Q</kbd>                   | close terminal           |
| <kbd>Tab</kbd>                                                  | autocomplete, navigation |
| <kbd>Ctrl</kbd> <kbd>Shift</kbd> <kbd>⬆️</kbd> or <kbd>⬇️</kbd>   | scrolling up, down       |
| <kbd>Ctrl</kbd> <kbd>R</kbd>                                    | search history bar       |

**[⬆ back to top](#contents)**

---

# Configuration

I'm using the Z-shell instead of bash as my default shell and some plugins to colorize my terminal. It's not increasing the productivity like 10 times but as a human being with an aesthetic demand it's more satisfying

don't make you much more productive but more pleasant to look at a nicely looking

[LSDeluxe](https://github.com/Peltoche/lsd) | nicer looking ls command
[Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh) |
[Powerlevel10k](https://github.com/romkatv/powerlevel10k) | layout looks nicer, syntax highlighting

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
