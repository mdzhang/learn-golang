# More Types

## Pointers

- hold memory address of value

`var p *int`

- `*T` is pointer to a `T` value; zero value is `nil`
    - `var p *int`

```go
i := 42
p = &i
fmt.Println(*p) // read i through the pointer p
*p = 21  // set i through the pointer p
```

- `&` creates pointer from operand
- `*` **dereferences** pointer, refers to its underlying value

## Struct

```go
type Vertex struct {
    X int
    Y int
}
```

- `struct` is collection of fields

```go
v := Vertex{1, 2}
v.X = 4
fmt.Println(v.X)
```

- fields are accessed using dot


```go
p = &v
(*p).X // same as p.X
```

-if `p` is a pointer, dot notation is syntactic sugar over explicit dereference


```go
type Vertex struct {
    X, Y int
    Z string
}

var (
    v1 = Vertex{1, 3, "hi"}  // has type Vertex
    v2 = Vertex{X: 1}  // Y:0 is implicit
)
```

- `v1` syntax initializers all struct values in order of their declaration
- `v2` syntax allows for initializing a subset of fields; rest initialized to their zero value

## Arrays & Slices

```go
primes := [6]int{2, 3, 5, 7, 11, 13}
```

- type `[n]T` is an array of n values of type `T`
- in `[n]T{...}`, `{...}` is an array literal
- fixed size

## Slices

```go
primes := [6]int{2, 3, 5, 7, 11, 13}

var s []int = primes[1:4]

s := []struct {
    i int
    b bool
}{
    {2, true},
    {3, false},
    {5, true},
    {7, true},
    {11, false},
    {13, true},
}

board := [][]string{
    []string{"_", "_", "_"},
    []string{"_", "_", "_"},
    []string{"_", "_", "_"},
}
```

- type `[]T` is a **slice** of n values of type `T`
- slice doesn't store data, just points to parts of an underlying array
- changing slice modifies underlying array; reflected in other slices to same array
- slice has **length** (`len(s)`) - the number of elements in slice
- slice has **capacity** (`cap(s)`) - the number of elements in underlying array
- zero value of a slice is `nil`, 0 len and 0 cap

```go
var a [10]int

a[0:10]
a[:10]
a[0:]
a[:]
```

- as in Python, can omit bounds of a slice to use defaults (i.e. lower/upper bound)
- unlike Python, going out of bounds throws error

```go
a := make([]int, 5) // [0 0 0 0 0]
b := make([]int, 0, 5) // []
```

- use `make` to allocate a zeroed array and return a slice that refers to that array

```go
func append(s []T, vs ...T) []T
```

- use builtin `append` to add values to end of slice
- will allocate larger underlying array automatically if necessary

## Maps

```go
var m map[string]Vertex

m = make(map[string]Vertex)
m["Bell Labs"] = Vertex{
    40.68433, -74.39967,
}
fmt.Println(m["Bell Labs"])
```

- can use `make` to initialize a map
- zero value is `nil`
    - has no keys
    - keys cannot be added
    - returns zero value for unknown key (instead of e.g. throwing error)

```go
var m = map[string]Vertex{
    "Bell Labs": Vertex{
        40.68433, -74.39967,
    },
    "Google": Vertex{
        37.42202, -122.08408,
    },
}

var m = map[string]Vertex{
    "Bell Labs": {40.68433, -74.39967},
    "Google":    {37.42202, -122.08408},
}
```

- if top level type is type name (instead of inlined struct), can omit it from elements of literal

```go
m[key] = elem
elem = m[key]
delete(m, key)
elem, ok = m[key]
```

## Functions

```go
func compute(fn func(float64, float64) float64) float64 {
    return fn(3, 4)
}
```

- functions are first class citizens
- above, `fn` must have signature `func(float64, float64) float64`

```go
func adder() func(int) int {
    sum := 0
    return func(x int) int {
        sum += x
        return sum
    }
}
```

- functions can be closures
