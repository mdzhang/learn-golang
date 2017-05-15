# Flow Control

## Looping

```go
for i := 0; i < 10; i++ {
    sum += i
}
```

- `for` loop is only looping construct
- has init statement, condition, post statement
- variables declared in `for` are only visible in `for`'s scope
- no parens around statements
- brackets required

```go
for ; sum < 1000; {
    sum += sum
}
```

- init and post statements are optional

```go
for sum < 1000 {
    sum += sum
}
```

- can drop semicolons, for looks the same as a while

```go
for {
}
```

- infinite loop if no condition op

### Slices and Maps

```go
var pow = []int{1, 2, 4, 8, 16, 32, 64, 128}

for i, v := range pow {
    // i is index, v is element at index in map or slice
    fmt.Printf("2**%d = %d\n", i, v)
}

// skip `, v` if you don't need value
for i := range pow {
    fmt.Printf("2**%d = %d\n", i, v)
}

for _, v := range pow {
    fmt.Printf("2**%d = %d\n", i, v)
}
```

## Branching

### If

```go
if x < 0 {
    return sqrt(-x) + "i"
}
```

- no parens required around condition
- brackets required

```go
if v := math.Pow(x, n); v < lim {
    return v
}
```

- if statements can also have init statement aka **short statement**
- variables declared in short statement only available to `if` and its `else`s

### Switch

```go
switch os := runtime.GOOS; os {
case "darwin":
    fmt.Println("OS X.")
case "linux":
    fmt.Println("Linux.")
default:
    // freebsd, openbsd,
    // plan9, windows...
    fmt.Printf("%s.", os)
}

// type switch
switch v := i.(type) {
case T:
    // here v has type T
case S:
    // here v has type S
default:
    // no match; here v has the same type as i
}
```

- cases breakthrough automatically, unless `fallthrough` specified
- cases can be statements to be evaluated
    - later cases statements will not be evaluated if earlier case succeeds
- switch without condition is same as `switch true`

### Defer


```go
package main

import "fmt"

func main() {
    defer fmt.Println("world")

    fmt.Println("hello")
}
```

- defer call's arguments evaluated immediately
- defer function call not executed until surrounding function returns
- subsequent defer function calls are pushed onto stack and evaluated in LIFO order
