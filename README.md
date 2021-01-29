<!-- translation
[English](README.md) | [Tiếng Việt](README-vn.md) -->

# Cheat Sheet - Linux

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
   - [Data Compression](#data-compression)
   - [Ownership and Permissions](#ownership-and-permissions)
   - [Environment Variables](#environment-variables)
   - [Finding patterns: grep, find, sed and awk](#finding-patterns-grep-find-sed-and-awk)
   - [](#)
   - [](#)
3. [Command Line Tools](#command-line-tools)
   - [Git](#git)
   - [Anaconda](#anaconda)
   - [Docker](#docker)
   - [LSDeluxe](#lsdeluxe)
   - [Misc - Tokei, ](#)
4. [Aliases](#aliases)
5. [Shortcuts](#shortcuts)
   - [Terminal](#terminal)
   - [Chromium Browser](#chromium-browser)
   - [VSCode](#vscode)
6. [Shell Configuration](#shell-configuration)
7. [Shell Scripting](#shell-scripting)
   - [Bash in a Nutshell](#bash-in-a-nutshell)
   - [Variables](#variables)
   - [Loops](#loops)
   - [Functions](#functions)
   - [Condtionals](#conditionals)
8. [Raspberry Pi related](#raspberry-pi)
9. [Databases](#databases)
   - [SQLite](#sqlite)
   - [MongoDB](#mongodb)
   - [PostgreSQL](#postgresql)
   - [Redis](#redis)

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
| ----- | ------------------------ | ------------------------------------------- |
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
mkdir file{1..5}        # creates 5 enumrated files

rmdir <dir_name>        # removes a directory
```

Files oand directories can be copied or linked. Hard links point to the files in memory directly whereas soft links point to the file which references to the place in memory.

```bash

cp <file> <path/new_filename>  # copies a file to the advised path
cp -R <source> <destination>   # copies recursively

ln <target> <new_link>         # creates a hard link to a file
ln -s <target> <new_link>      # creates a soft link to a file
rm <new_link>                  # removes the symlink
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

Linux is a multi-user OS and therefore implements concepts like users and groups to ensure proper security. There are 3 types of owners:

- **User** | _A user is the one who created the file._
- **Group** | _A group can contain multiple users sharing the same permissions. By default the group is the same as the user._
- **Other** | _Any one who has access to the file other than user and group falls int this category. Other has neither created the file nor is a group member._

Each files/dirs access mode can be displayed when using the `ls -l` command. Each filessytem entry can have read, write and execute permissions.

<p align="center">
  <a href="https://the-coding-lab.com" alt="My-Blog" >
    <img src="docs/ownership_permissions.png" width=600px/>
  </a>
</p>

The access modes (Owner, Group, Other below image) can be modified using the `chmod` command. I prefer to use the octal notation over the symbolic notation when changing permissions.

```bash
chmod <octal> <file/dir>  # change permissions of a file/dir

chmod 777 <file/dir>      # full permissions
chmod 644 <file/dir>      # default permissions when creating new file

chmod +x <script.sh>      # makes a script executable
chmod -R 755 <path>       # changes permissions recursively
```

The following table displays the octal notation and it's representation.

| Octal Notation | Symbolic Repr | Permissions             |
| -------------- | ------------- | ----------------------- |
| 0              | ---           | No permissions          |
| 1              | --x           | Execute only            |
| 2              | -w-           | Write only              |
| 3              | -wx           | Write and execute       |
| 4              | r--           | Read only               |
| 5              | r-x           | Read and execute        |
| 6              | rw-           | Read and write          |
| 7              | rwx           | Read, write and execute |

To modify ownership (Owner and Group above image) `chown` is used.

```bash

chown user:group <file/dir>  # changes the ownership
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

## Finding Patterns: grep, find, sed and awk

grep - print lines matching a pattern
find - search for files in a directory hierarchy
sed - stream editor for filtering and transforming text
awk - pattern scanning and text processing language

```bash
sed -i 's/foo/bar/g' *   # replace pattern (foo) by bar in multiple files
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
find . -name "foo*"  # prints all filesnames containg the pattern

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

## Processes and Jobs

at service and cron service

mor advanced stuff: apache airflow

```bash
date
jobs
kill %N
ps

# if a process should be killed after execution of a script: the PID of the started background process has to be saved, then kill
foo &
FOO_PID=$!
# do other stuff
kill $FOO_PID

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

## Cron Jobs

```bash

```

```bash

```

## CPU, GPU and Display

GPU is sometimes necessary when training a neural network or other things with intensive computational workload.
If connected a monitor as well.

```bash
cat /proc/cpuinfo  # provides all kinds of information toward each virtual cpu core
```

text

```bash
 lscpu      # get inormations about CPU
      #
      #
      #
      #
```

## Secure Shell (SSH)

cryptographic network protocol, generate ssh keys. o
I'm using the SSH protocol within my local network (raspberry pi) and for remote servers.
deploying something
ssh into database?

When deploying something on my Raspberry Pi I connect via SSH.

scp secure copy protocol

```bash
scp your_username@remotehost.edu:foobar.txt /local/dir   # download
scp username@hostname:/path/to/remote/file /path/to/local/file
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

snap

```bash
-- snap
snap help --all                      #  shows all args
snap list                            # lists installed packages
snap install <package_name>          # installs a package
snap remove <package_name>           # uninstalls the package
snap find <package_name>             # searches within the repo
```

## Git

https://stackoverflow.com/questions/927358/how-do-i-undo-the-most-recent-local-commits-in-git
https://stackoverflow.com/questions/2003505/how-do-i-delete-a-git-branch-locally-and-remotely
https://stackoverflow.com/questions/292357/what-is-the-difference-between-git-pull-and-git-fetch
https://stackoverflow.com/questions/348170/how-do-i-undo-git-add-before-commit
https://stackoverflow.com/questions/6591213/how-do-i-rename-a-local-git-branch
https://stackoverflow.com/questions/1125968/how-do-i-force-git-pull-to-overwrite-local-files
https://stackoverflow.com/questions/61212/how-to-remove-local-untracked-files-from-the-current-git-working-tree
https://stackoverflow.com/questions/4114095/how-do-i-revert-a-git-repository-to-a-previous-commit
https://stackoverflow.com/questions/1783405/how-do-i-check-out-a-remote-git-branch
https://stackoverflow.com/questions/630453/put-vs-post-in-rest
https://stackoverflow.com/questions/549/the-definitive-guide-to-form-based-website-authentication
https://stackoverflow.com/questions/161813/how-to-resolve-merge-conflicts-in-git-repository
https://stackoverflow.com/questions/1783405/how-do-i-check-out-a-remote-git-branch/1783426#1783426
https://stackoverflow.com/questions/16717930/how-to-run-crontab-job-every-week-on-sunday
https://stackoverflow.com/questions/584770/how-would-i-get-a-cron-job-to-run-every-30-minutes
https://stackoverflow.com/questions/10193788/restarting-cron-after-changing-crontab-file

```bash


```

```bash


```

## Anaconda

python distro for scientific computing, simplifying package management

installation of anaconda:

```bash
# install conda (https://docs.anaconda.com/anaconda/install/linux/)
1. download file from anaconda.com                        # file for install
2. bash ~/Downloads/Anaconda3-2020.02-Linux-x86_64.sh
3. conda config --set auto_activate_base False or True    # checks if base-version is running in each terminal session
```

getting information about conda and environments

```bash
conda --help                                       # shows all options
conda info -e                                      # shows all conda environments
conda info                                         # gives information about version, env's etc.
conda info --envs                                  # list all the conda environment available
conda env list                                     # shows all environments
conda update -n base conda                         # updates conda
```

creating new environments

```bash
# working with environments
conda create --name <env_name> python=3.6          # creating a new conda env with a specific python-version
conda create -c rdkit -n <env_name> rdkit          # creating a new conda env with a specific package
conda create -n <env_name> python=3.9 rdkit        # creating a specific env
conda install -c rdkit rdkit-postgresql            # installing PostgreSQL as client for rdkit-postgreSQL cartridge (https://rdkit.org/docs/Cartridge.html)
conda activate <env_name>                          # activates a certain conda env
conda deactivate                                   # deactivates the current conda env
```

modifying packages from envs

```bash
conda list                                         # lists all packages/versions of the active conda env
conda list --name <env_name>                       # lists all packages of a certain conda env
conda list --revisions                             # lists all revisions made in active conda env
conda remove --name <package_name>                 # deletes a specified list of packages from spec. conda env
conda env remove --name <env_name>                 # deletes an specified environment

conda clean -h                                     # in the 'pkgs'-folder a lot of waste if collected (its the download cache)
```

sharing envs: creating yamls

```bash
# sharing environments
conda create --clone <env_name> --name <new_env>   # make a copy of an env
conda env export --name <env_name> > envname.yml   # export env to YAML file
pip freeze > requirements.txt                      # (do this from the activated conda env!) insert these into the conda .yml ! test the conda/pip env (sometimes both in combination can cause problems)
--> pip is automatically added, so this is not necessary!
conda env create --file envname.yml                # creates env from YAML file
conda env create                                   # create an env from the file named environment.yml in current dir
conda list --explicit > pkgs.txt                   # export env with exact package versions for one OS (the URLs)
conda create --name <new_env> --file pkgs.txt      # create env based on exact package versions
```

channels

```bash
# using packages and channels
anaconda-navigator                                 # opens the anaconda navigator
anaconda search <package_name>                     # search for a package on all channels (not only default)
conda install conda-forge::PKGNAME                 # installs a package from a specific channel
conda config --add channels <channel_name>         # add a channel to your conda configuration

# additional useful hints
conda update --all --name <env_name>               # updates all packages within a specified env
conda config --show                                # shows all configurations

# manage anaconda account
conda install anaconda-client
anaconda -h

# upload packages to anaconda:
anaconda login
anaconda upload PACKAGE
https://<your-anaconda-repo>/USERNAME/PACKAGE
anaconda download USERNAME/PACKAGE

```

tutorial: how to upload a package to anaconda (my own channel)

## pip

```bash
-- pip
pip --help                           # all
pip search <package_name>            # search pip repo
pip install <package_name>           # installing something from pypi.org repo
pip uninstall <package_name>         # uninstalls a specific package
pip list                             # lists all pip-packages within the current env
pip freeze > requirements.txt        # lists all dependencies within the current environment (should be added to exported conda .yml)
pip check                            # verify installed packages have compatible dependencies

```

## LSDeluxe

## tree, Tokei, misc

```bash


```

wanna generate a password? use openssl! the cryptographers tool

```bash
openssl rand -hex 12

tree        # must be installed via apt sometimes
tree -L 2   # max depth isn set to 2
ls --tree   # LSDeluxe


locate <pattern> # searches through whole system for name
sudo updatedb    # updates cache of locate

# unite pdfs
pdfunite in1.pdf in2.pdf out.pdf  #
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

Terminal, Nano, Chromium, VSCode

Terminal Shortcuts

| Shortcut                                                        | Description                                   |
| --------------------------------------------------------------- | --------------------------------------------- |
| <kbd>Ctrl</kbd> <kbd>Alt</kbd> <kbd>T</kbd>                     | Open terminal                                 |
| <kbd>Ctrl</kbd> <kbd>Shift</kbd> <kbd>Q</kbd>                   | Close terminal                                |
| <kbd>Tab</kbd>                                                  | Autocomplete, navigation                      |
| <kbd>Ctrl</kbd> <kbd>Shift</kbd> <kbd>⬆️</kbd> or <kbd>⬇️</kbd> | Scrolling up or down                          |
| <kbd>Ctrl</kbd> <kbd>R</kbd>                                    | Search history bar                            |
| <kbd>Ctrl</kbd> <kbd>C</kbd>                                    | Abort current running process                 |
| <kbd>Ctrl</kbd> <kbd>D</kbd>                                    | Log out of current shell (SQL, Mongo, Python) |
| <kbd>Ctrl</kbd> <kbd>L</kbd>                                    | Clear terminal                                |
| <kbd>Ctrl</kbd> <kbd>U</kbd>                                    | Erase current line                            |
| <kbd>Ctrl</kbd> <kbd>A</kbd>                                    | Move cursor to beginning of line              |
| <kbd>Ctrl</kbd> <kbd>E</kbd>                                    | Move cursor to end of line                    |
| <kbd>Ctrl</kbd> <kbd>left</kbd> or <kbd>right</kbd>             | Move cursor to next word                      |
| <kbd>Alt</kbd> <kbd>D</kbd>                                     | Delete all characters after the cursor        |

nano editor

```bash

nano <file>      # opens the file (nano is a terminal application for text editing)
```

| Shortcut                                             | Meaning            |
| ---------------------------------------------------- | ------------------ |
| <kbd>Ctrl</kbd> <kbd>O</kbd>                         | Save file          |
| <kbd>Ctrl</kbd> <kbd>X</kbd>                         | Exit               |
| <kbd>Ctrl</kbd> <kbd>W</kbd>                         | Search for pattern |
| <kbd>Shift</kbd> <kbd>right</kbd> or <kbd>left</kbd> | Select             |
| <kbd>Ctrl</kbd> <kbd>K</kbd>                         | Cut                |
| <kbd>Ctrl</kbd> <kbd>U</kbd>                         | Paste              |
| <kbd>Ctrl</kbd> <kbd>\</kbd>                         | Replace pattern    |

Chromium Shortcuts

| Shortcut                                           | Description                              |
| -------------------------------------------------- | ---------------------------------------- |
| <kbd>Ctrl</kbd> <kbd>Shift</kbd> <kbd>T</kbd>      | Reopens recently closed tabs             |
| <kbd>alt</kbd> <kbd>left</kbd> or <kbd>right</kbd> | Moves one page back/forward              |
| <kbd>Ctrl</kbd> <kbd>+</kbd> or <kbd>-</kbd>       | Zoom in, out                             |
| <kbd>Ctrl</kbd> <kbd>Tab</kbd>                     | jumps to the next tab                    |
| <kbd>Ctrl</kbd> <kbd>F</kbd>                       | Find content on web page                 |
| <kbd>F5</kbd>                                      | Refresh current webpage                  |
| <kbd>Ctrl</kbd> <kbd>left-click</kbd>              | Open link in the background of a new tab |
| <kbd>Ctrl</kbd> <kbd>Shift</kbd> <kbd>I</kbd>      | Inspect                                  |
| <kbd>Ctrl</kbd> <kbd>U</kbd>                       | View page source                         |
| <kbd>Spacebar</kbd>                                | Scrolls down a section of the webpage    |
| <kbd>Spacebar</kbd> <kbd>Shift</kbd>               | Scrolls up a section of the webpage      |

VSCode Key Bindings (see into my dotfiles repo)

| Shortcut                                      | Meaning            |
| --------------------------------------------- | ------------------ |
| <kbd>Ctrl</kbd> <kbd>Alt</kbd> <kbd>T</kbd>   |                    |
| <kbd>Ctrl</kbd> <kbd>Shift</kbd> <kbd>Q</kbd> |                    |
| <kbd>Tab</kbd>                                |                    |
| <kbd>Ctrl</kbd> <kbd>Shift</kbd>              | scrolling up, down |
| <kbd>Ctrl</kbd> <kbd>R</kbd>                  |                    |

**[⬆ back to top](#contents)**

---

# Shell Configuration

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

check if a file exists

```bash
if [ -d "$DIRECTORY" ]; then
  # Control will enter here if $DIRECTORY exists.
fi

if [ ! -d "$DIRECTORY" ]; then
  # Control will enter here if $DIRECTORY doesn't exist.
fi
```

**[⬆ back to top](#contents)**

---

# Raspberry Pi

**[⬆ back to top](#contents)**

# Databases

applications need databases, to serve data. theyre implemented into web apps, mobile apps and it's good to ssh into them

## SQLite

## MOngoDB

## POstgreSQL

## Redis
