> In Go language, the interface is a collection of method signatures. As we know we don't have inheritance in Go but we have Embedding.
### Embedded interfaces ###
Interface A can embed other interfaces like C and D. It means Interface A has the methods of interfaces C and D.

example:
```go
package main

import "fmt"

type Details interface {
	getInfo() string
}

type CarInfo interface {
	Details
	getPrice() string
}

type Animal struct {
	name string
}

type Car struct {
	model string
}

func (animal *Animal) getInfo() string {
	return "I'm a " + animal.name
}

func (car *Car) getInfo() string {
	return "I'm a " + car.model + " car"
}

func (car *Car) getPrice() string {
	return "I'm so expensive :)"
}

func main() {
	var car CarInfo = &Car{
		model: "Bugatti",
	}
	fmt.Println(car.getInfo())
	fmt.Println(car.getPrice())
	var det Details = &Animal{
		name: "cat",
	}
	fmt.Println(det.getInfo())
}

```
---
### Embedded Structs ###
In Go Embedded Structures are a way to reuse a struct’s fields.
```go
package main

import "fmt"

type Details struct {
	name  string
	price string
	code  string
}

type Car struct {
	Details
	model string
}

type Hat struct {
	Details
	size string
}

func main() {
	hat := &Hat{
		Details: Details{
			name:  "Nike",
			price: "340$",
			code:  "341",
		},
		size: "56",
	}
	car := &Car{
		Details: Details{
			name:  "BMW",
			price: "45235$",
			code:  "643",
		},
		model: "autoPilot",
	}
	fmt.Printf("hat: %v\n", hat)
	fmt.Printf("car: %v\n", car)
}
```