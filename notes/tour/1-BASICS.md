# Basics

### Imports

- use **factored import** statements

```go
import (
    "fmt"
    "math"
)
```

### Exports

- go exports names that start with a capital letter; unexported names are not accessible outside a package

## Functions

```go
func add(x int, y int) int {
    return x + y
}
```

- keyword `func`
- functions take 0+ args
- type of parameter comes after variable name
    - can condense multiple params with same type i.e. `x int, y int` => `x, y int`
- return type before opening bracket

```go
func swap(x, y string) (string, string) {
    return y, x
}
```

- can return any # of args
- note that multiple returned args are parenthesized `(string, string)`

```go
func split(sum int) (x, y int) {
    x = sum * 4 / 9
    y = sum - x
    return
}
```

- **naked returns** are when you specify variable to return's name in function signature and use `return` with no arguments

## Variables

```go
package main

import "fmt"

var c, python, java bool

func main() {
    var i int
    fmt.Println(i, c, python, java)
}
```

- can declare variables at package or function level
- can declare multiple variables at a time
- declaration signature is `var [variable name] [variable type]`

```go
var i, j int = 1, 2
var c, python, java = true, false, "no!"
```

- variables can be declared with initializers
- can omit type if an initializer is provided - type will be inferred from initializer (i.e. uses **implicit type**)

```go
i := 1
```

- can use **short assignment** instead of var declaration with implicit type

```go
var i int
var f float64
var b bool
var s string
fmt.Printf("%v %v %v %q\n", i, f, b, s) // => 0 0 false ""
```

- variables declared without initializer are initialized to their **zero value** (0 for numerics, empty string, False)

```go
var i int
j := i // j is an int
```

- if right side of declaration is typed, new variable has same type

## Constants

```go
const Pi = 3.14
```

- declared like variables, but with `const` keyword
- short declaration syntax `:=` not allowed

- numeric constants are high precision values and take type needed by context

## Statements

- outside a function, always start with keywords `var`, `func`, `package`, `import`, etc.

## Basic Types

```go
bool

string

int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr

byte // alias for uint8

rune // alias for int32
     // represents a Unicode code point

float32 float64

complex64 complex128
```

- `int`, `uint` normally 32/64 bytes based on system
- prefer `int` unless you specifically need un/sized integer

### Type Conversions

- `T(v)` converts value `v` to type `T`
- types must be explicitly converted during assignment to item of different type

```go
var f float64 = math.Sqrt(float64(x*x + y*y))
var z uint = uint(f)
```
