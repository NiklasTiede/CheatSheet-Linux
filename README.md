genereal ideas:
* theme specific
* powerful cheats in general
* the whole design is done in a cool manner
* maybe hosting a website and stylyying it for cheat sheets

concrete ideas:
* rdkit cheat sheet!
* important python standard libs cheat sheets
* termux, raspi


# Cheatsheets of Mine

Herein I'm writing down all important/interesting commands to memoiye them better.


Idee: dotfile auch machen, um schnell jedes linux system yu konfigurieren mit zshell und tollen tools!

# Contents
1. [Linux](#linux)
    * [Arrays](#arrays)
    * [Slices](#slices)
2. [Python Standard Library](python-std-lib)


## 1. Linux


Most important: TAB, arrow keys, crtl + r
ctrl shift arrow keys
ctrl alt t
ctrl alt q 
<kbd>Ctrl</kbd> + <kbd>Shift</kbd>
<kbd style="color: blue"> Ctrl</kbd>


## shortcuts

```bash
ctrl + r      # searching through 
      # 
      # 
      # 
```     

## aliases

## terminal logic: operators, shell expansion etc.

## extreme useful command line tools

fuzzyfinder





basic navigation, yurechtkommen


logical operators 

&&
;
&

make asliase to increase prodictivity 


Some precious commands...




help

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























---

## Go in a Nutshell

* Imperative language
* Statically typed

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

### Comparison
|Operator|Description|
|--------|-----------|
|`==`|equal|
|`!=`|not equal|
|`<`|less than|
|`<=`|less than or equal|
|`>`|greater than|
|`>=`|greater than or equal|


## Type Conversions
```go
var i int = 42
var f float64 = float64(i)
var u uint = uint(f)

// alternative syntax
i := 42
f := float64(i)
u := uint(f)
```

# Arrays, Slices, Ranges

text

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

text

**[⬆ back to top](#contents)**