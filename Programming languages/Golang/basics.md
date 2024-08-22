
### modules and dependencies ###
### package ###
Refers to a collection of Go source files within the same directory.

>You can search [pkg.go.dev](https://pkg.go.dev/) to find packages with functions you might find useful.

### Module ###
Refers to a higher-level concept that encompasses a collection of related packages, versioned together, and managed by a `go.mod` file.

### go.mod ###

directives:
- `module` : to determine the module path
- `go` : to determine the golang version
- `require` : to determine some dependencies
- `replace`
- `exclude` : excluding modules from main module’s dependency graph
- `retract` : Indicates that a version or range of versions of the module defined by `go.mod` should not be depended upon.

an example of a go.mod file:
```go
module example.com/mymodule

go 1.14

require (
    example.com/othermodule v1.2.3
    example.com/thismodule v1.2.3
    example.com/thatmodule v1.2.3
)

replace example.com/thatmodule => ../thatmodule
exclude example.com/thismodule v1.3.0


retract (
    v1.0.0 // Published accidentally.
    v1.0.1 // Contains retractions only.
)

```

> we can work on a module with lower go version than the one installed in our OS.

---
### Exported names ###
in golang instead of private and public (in other languages) we have exported names. name is exported if it begins with a capital letter.

example (Pi is exported from math package):
```go
package main

import (
	"fmt"
	"math"
)

func main() {
	fmt.Println(math.Pi)
}
```
---
### Type conversions ###

The expression `T(v)` converts the value `v` to the type `T`.
```go
i := 42
f := float64(i)
u := uint(f) 
```
---
### Interfaces ###
An _interface type_ is defined as a set of method signatures.
```go
 type Abser interface {
	Abs() float64
}
```

> A value of interface type can hold any value that implements those methods.

```go
package main

import (
	"fmt"
	"math"
)

type Abser interface {
	Abs() float64
}

func main() {
	var a Abser
	f := MyFloat(-math.Sqrt2)
	v := Vertex{3, 4}

	a = f  // a MyFloat implements Abser
	a = &v // a *Vertex implements Abser

	// In the following line, v is a Vertex (not *Vertex)
	// and does NOT implement Abser.
	a = v // error

	fmt.Println(a.Abs())
}

type MyFloat float64

func (f MyFloat) Abs() float64 {
	if f < 0 {
		return float64(-f)
	}
	return float64(f)
}

type Vertex struct {
	X, Y float64
}

func (v *Vertex) Abs() float64 {
	return math.Sqrt(v.X*v.X + v.Y*v.Y)
}
```
---
### Type Assertions ###
> A _type assertion_ provides access to an interface value's underlying concrete value.
```go
t := i.(T)
```
This statement asserts that the interface value `i` holds the concrete type `T` and assigns the underlying `T` value to the variable `t`.
> If `i` does not hold a `T`, the statement will trigger a panic!

another form of type assertion(returning two values):
```go
t, ok := i.(T)
```
If `i` holds a `T`, then `t` will be the underlying value and `ok` will be true.
If not, `ok` will be false and `t` will be the zero value of type `T`, and no panic occurs.

---
### Type switches ###

> using `type` keyword to specify the type.

```go
switch v := i.(type) {
case T:
    // here v has type T
case S:
    // here v has type S
default:
    // no match
}
```
---
### Stringer interface ###
One of the most present interfaces is `stringer` defined by the `fmt` package.
```go
type Stringer interface {
    String() string
}
```

> The `fmt` package (and many others) look for this interface to print values.

example: 
```go
package main

import "fmt"

type Person struct {
	Name string
	Age  int
}

func (p Person) String() string {
	return fmt.Sprintf("%v (%v years)", p.Name, p.Age)
}

func main() {
	a := Person{"Arthur Dent", 42}
	z := Person{"Zaphod Beeblebrox", 9001}
	fmt.Println(a, z)
}
```
