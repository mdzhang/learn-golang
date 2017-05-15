# Methods

## Methods

- functions with a **receiver** argument

```go
func (v Vertex) Abs() float64 {
    return math.Sqrt(v.X*v.X + v.Y*v.Y)
}
```

- receiver is `v Vertex` i.e. name `v` and type `Vertex`
- type `Vertex` must be defined in same package as method `Abs`

```go
func (v Vertex) Abs() float64 {
    return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

func (v *Vertex) Scale(f float64) {
    v.X = v.X * f
    v.Y = v.Y * f
}
```

- use pointer receiver, instead of value receiver, if you need to modify a value
- if a value receiver is used, it will be applied to a copy of the argument
    - may want to use pointer receivers just to spare overhead

```go
v.Scale(5) // same as (&v).Scale(5) if v is a value
p.Abs() // same as (*p).Abs() if p is a pointer
```
- methods with pointer receivers take either a value or a pointer as the receiver when they are called

## Interfaces

```go
type MyFloat float64

type Abser interface {
    Abs() float64
}

func (f MyFloat) Abs() float64 {
    if f < 0 {
        return float64(-f)
    }
    return float64(f)
}

func main() {
    var a Abser
    f := MyFloat(-math.Sqrt2)
    a = f
}
```

- interface type is a set of method signatures

```go
interface{}
```

- empty interface may hold values of any type
- used by code that handles values of unknown type

```go
// assert variable `i` has concrete type `T` and assign `T` value to `t`
// triggers a panic if `i` doesn't have a `T`
t := i.(T)

// if you don't want to trigger a panic
t, ok := i.(T)
```

## Errors

```go
i, err := strconv.Atoi("42")
if err != nil {
    fmt.Printf("couldn't convert number: %v\n", err)
    return
}

func (T) Read(b []byte) (n int, err error)
```

- functions often return an error value, and calling code should handle errors by testing whether the error equals nil
