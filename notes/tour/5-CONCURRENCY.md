# Concurrency

```go
go f(x, y, z)
```

- **goroutine**: ightweight thread managed by Go runtime
- `f`, `x`, `y`, `z` evaluated in current goroutine
- execution of `f` occurs  in new goroutine

## Channels

```go
ch := make(chan int) // create channel

ch <- v    // Send v to channel ch.
v := <-ch  // Receive from ch, and
           // assign value to v.
```

- **channels** are a typed conduit through which you can send and receive values with the channel operator, `<-`
- by default, sends and receives block until the other side is ready

```go
ch := make(chan int, 100)
```

- make a **buffered channel**
    - sends block when buffer full
    - receives block when buffer empty

```go
close(c)
```

- senders can close channels
- sending to closed channel causes panic
- receivers can test if channel closed `v, ok := <-ch`
- `for i := range c` receives values from channel repeatedly until it's closed

### select

```go
tick := time.Tick(100 * time.Millisecond)
boom := time.After(500 * time.Millisecond)
for {
    select {
    case <-tick:
        fmt.Println("tick.")
    case <-boom:
        fmt.Println("BOOM!")
        return
    default:
        fmt.Println("    .")
        time.Sleep(50 * time.Millisecond)
    }
}
```

- `select` lets goroutine wait on multiple communication operations
- blocks until one of its cases can run, then it executes that case
    - chooses random one if multiple are ready
- `default` case run if no other case is ready
