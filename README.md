# cheatsheet

goal: cheat sheet which will get many stars!

genereal ideas:
-theme specific
-powerful cheats in general
-the whole design is done in a cool manner
-maybe hosting a website and stylyying it for cheat sheets



rdkit cheat sheet!
important python standard libs cheat sheets
termux, raspi
linux apps, bash?
most important commands every body needs

# Go Cheat Sheet

# Index
9. [Arrays, Slices, Ranges](#arrays-slices-ranges)
    * [Arrays](#arrays)
    * [Slices](#slices)

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
