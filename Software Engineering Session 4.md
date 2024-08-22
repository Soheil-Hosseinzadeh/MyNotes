## Unit testing
- what is testing?
- advantages and disadvantages
- types of testing

> Tests can be done on applications too, not just some codes, like clicking a button

#### Two kinds of testing:
- Automatic
- Manual (printing through the code)

#### disadvantages
- It takes more time i
- n developing
#### advantages
- Debugging the code (finding the bugs)
- better design (TDD: first test then code)
> sometime we can't create tests for a function so we have to design the function better to make it's test

#### Different types of testing
- Doc test
- unit test (the most important one)
- (load) stress test
- integration test
- end to end test
#### details about unit Test
- It's automate
- It's for a unit (a part of code not the whole project)
- It's fast
- It's isolated
> There is no relativity between tests.
> t1, t2, t3 => three tests (they are not dependant to to each other) y()

>when we wanna write a test for x() we shouldn't test the y function(we have to garauntee that y is doing well it's job), cause y may has some issue but we would think that x function has bugs.

```
x() {
  y()
}
```

#### Stress Test
making a heavy load on a server to test it's response.
#### integeration test
It's a test that is on more that one unit.
#### end to end test
Making a real request to the API (like a user) and seeing if everything is alright or not
> We test the project flow as a user, (doing things that a user does with the service)

#### Binary Search
 2 7 11 23 46 91 104

#### test files in golang
name of the file test in golang: `*_test.go`
> we put a name that we want in `*` part

```go
package math

import "testing" 

func TestBinarySearch (t *testing.T) {
	t.Run("Should return -1 when target does not exist in array", func(){
	arr := []int{2,7,11,23,46, 91,184}
	index := BinarySearch(arr, 0, len(arr),50)
	assert.Equal(t, -1, index)
	})
	t.Run("Should return -1 when target does not exist in array", func(t *testing.T){
	arr := []int{2,7,11,23,46, 91,184}
	index := BinarySearch(arr, 0, len(arr),91)
	assert.Equal(t, 5, index)
	})
}
```

> we use t.Run for testing
> T.Run takes a comment about the test and a function to test

> command to test go tests `go run test`

```go
func TestSendMessage(t *testing.T) {
t.Run("")
}
```
