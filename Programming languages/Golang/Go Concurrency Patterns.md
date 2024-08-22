#### Generator: function that returns a channel ####
```go
package main

import (
    "fmt"
    "math/rand"
    "time"
)

func boring(msg string) <-chan string {
    c := make(chan string)
    go func() {
        for i := 0; ; i++ {
            c <- fmt.Sprintf("%s %d", msg, i)
            time.Sleep(time.Duration(rand.Intn(1e3)) * time.Millisecond)
        }
   }()
    return c
}

func main() {
    c := boring("boring!")
    for i := 0; i < 5; i++ {
        fmt.Printf("You say: %q\n", <-c)
    }
    fmt.Println("You're boring; I'm leaving.")
}
```

> The `<-` in the returning channel of boring function means that the returning channel is a **receive-only** channel.

We can also have two calling from boring function like this:
```go
	func main() {
		Mat := boring("Mat") // Function returning a channel.
		Pat := boring("Pat")
		for i := 0; i < 5; i++ {
			fmt.Println(<-Mat)
			fmt.Println(<-Pat)
		}
		fmt.Println("You're boring; I'm leaving.")
	}
```

In this way Pat is always presented after Mat, so how to make these two independent from each other? by **fan-in** function
#### Fan-In Function (Multiplexing)####
We can upgrade the example above like this so that Mat and Pat independently execute:
```go
func fanIn(MatCh, PatCh <-chan string) <-chan string {
	res := make(chan string)
	go func() {
		for {
			res <- <-MatCh
		}
	}()
	go func() {
		for {
			res <- <-PatCh
		}
	}()
	return res
}

func main() {
	res := fanIn(boring("Mat"), boring("Pat"))
	for i := 0; i < 10; i++ {
		fmt.Println(<-res)
	}
	fmt.Println("You're boring; I'm leaving.")
}
```

 another implementation of `fan-in` function by `select` statement:
```go
func fanIn(input1, input2 <-chan string) <-chan string {
	c := make(chan string)
	go func() {
		for {
			select {
			case s := <-input1:
				c <- s
			case s := <-input2:
				c <- s
			}
		}
	}()
	return c
}
```