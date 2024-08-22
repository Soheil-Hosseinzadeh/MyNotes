### channels ###
channels are used to communicate between goroutines.
a simple example:
```go
package main

import "fmt"

func main() {

    messages := make(chan string)

    go func() { messages <- "ping" }()

    msg := <-messages
    fmt.Println(msg)
}
```

> **Unbuffered channels will wait until receive a value**

When we send something through the channel (**in another goroutine**) it does not matter how much it takes to receive that data. It even does not matter that we receive it or not.

```go
c := make(chan int)  
  
go func(res chan int) {  
   time.Sleep(3 * time.Second)  
   res <- 3  
}(c)  
  
time.Sleep(time.Second * 15)  
// If you remove the line bellow nothing will happen,
// We just ignore the channel
fmt.Println(<-c)
```

##### close #####
A sender can `close` a channel to indicate that no more values will be sent. Receivers can test whether a channel has been closed.
```go
v, ok := <-ch
```

> `ok` is `false` if there are no more values to receive and the channel is closed.

##### range #####
The loop `for i := range c` receives values from the channel repeatedly until it is closed.
example:
```go
package main

import (
	"fmt"
)

func fibonacci(n int, c chan int) {
	x, y := 0, 1
	for i := 0; i < n; i++ {
		c <- x
		x, y = y, x+y
	}
	close(c)
}

func main() {
	c := make(chan int, 10)
	go fibonacci(cap(c), c)
	for i := range c {
		fmt.Println(i)
	}
}
```

> **Note**: Only the sender should close a channel, never the receiver.

>**Note**: We don't usually need to close channels.Closing is only necessary when the receiver must be told there are no more values coming, such as to terminate a `range` loop.
---
### Mutual exclusion and Wait Groups ###
##### Mutex #####
Mutual exclusion which is provided as `mutex` data structure is used when we just want to make sure one goroutine can access a variable at a time to avoid conflicts.

Go's standard library provides mutual exclusion with `sync.Mutex` and its two methods:
- `Lock`
- `Unlock`
##### Group wait #####
we use wait groups of `sync` package to wait until other goroutines finish their job.

example:
```go
package main

import (
	"fmt"
	"slices"
	"sync"
)

type Note struct {
	numbers []string
	mu      *sync.Mutex
	wg      *sync.WaitGroup
}

func (note *Note) addNumber(number string) {
	note.mu.Lock()
	if slices.Contains(note.numbers, number) {
		return
	}
	note.numbers = append(note.numbers, number)
	fmt.Printf("note.numbers: %v\n", note.numbers)
	note.mu.Unlock()
	note.wg.Done()
}

func main() {
	myNote := &Note{
		numbers: []string{},
		mu:      &sync.Mutex{},
		wg:      &sync.WaitGroup{},
	}
	myNote.wg.Add(3)
	go myNote.addNumber("number1")
	go myNote.addNumber("number2")
	go myNote.addNumber("number3")

	myNote.wg.Wait()
}
```
