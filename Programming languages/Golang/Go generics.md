### Generic Types ###
Go functions can be written to work on multiple types using type parameters. The type parameters of a function appear between brackets, before the function's arguments.
```go
func Index[T comparable](s []T, x T) int
```

> We use constraints to limit the generic type. 

> The constraint can be a keyword like `comparable` or just a simple `interface`.

example:
```go
package main

import "fmt"

// Index returns the index of x in s, or -1 if not found.
func Index[T comparable](s []T, x T) int {
	for i, v := range s {
		// v and x are type T, which has the comparable
		// constraint, so we can use == here.
		if v == x {
			return i
		}
	}
	return -1
}

func main() {
	// Index works on a slice of ints
	si := []int{10, 20, 15, -10}
	fmt.Println(Index(si, 15))

	// Index also works on a slice of strings
	ss := []string{"foo", "bar", "baz"}
	fmt.Println(Index(ss, "hello"))
}
```

> We can also create generic types too, by adding `[T constraint]` after the type name.

```go
package main

import (
	"fmt"
)

type Tmp[T any] struct {
	value T
}

func (tmp *Tmp[T]) getValue() T {
	return tmp.value
}

func main() {
	tmp0 := &Tmp[int]{
		value: 5,
	}
	fmt.Println(tmp0.getValue())

	tmp1 := &Tmp[string]{
		value: "hello",
	}
	fmt.Println(tmp1.getValue())
}
```
---
### type constraint ###
We can create interfaces by a set of types as constraint in them to have generic type.

example:
```go
package main

import (
	"fmt"
)

type Text struct {
	content string
}

type MyInt int

type Base interface {
	~int | string | Text
}

func print[T Base](tmp T) {
	fmt.Println(tmp)
}

func main() {
	var tmp Text = Text{content: "hello"}
	print(tmp)
	print(34)
	print(MyInt(345))
}
```

> The expression `~int` means the set of all types whose underlying type is `int`. This includes the type `int` itself as well as all types declared with definitions such as `type MyInt int`.

example of using constraints package:
```go
package main

import (
    "fmt"

    "golang.org/x/exp/constraints"
)

func sum[T constraints.Integer | constraints.Float] (nums ...T) T {
    var res T
    for _, v := range nums {
        res += v
    }
    return res
}

func main() {
    fmt.Println(sum([]int64{3, 5, 3, 56}...))
}
```