# Core - Interfaces
---
### What is an Interface type is Go
**Tour of Go Interface Definition:  An interface type is defined as a set of method signatures.**
  - ☢️ In my opinion, Tour of Go does a poor job describing what an interface is and when and how to use them.

**The Interface Type - A Better Definition**

Interface
: An Interface provides a way to specify the behavior of an object. We use interfaces to create common abstractions that multiple objects can implement. -100 Go Mistakes

  - Interfaces are ...
    - like a contract or a set of expectations applied to a type - enrolled (an object or type can enroll an interface)
    ```
    "If your type can do these things, then you can be used whereever this interface is expected"
    It doesn't care how your type does those things, just as long as it satisfies the methods on the interface. 
    ```
    - helpful in building reusable code across your application
    - Implicit - (No declaration statements like X implements y) - as long as it satisfies the methods, it is considered a type from that interface      

### Example of an interface:
****
##### Gobyexample code - 
```go

package main

import (
    "fmt"
    "math"
)

type geometry interface {
    area() float64
    perim() float64
}

type rect struct {
    width, height float64
}
type circle struct {
    radius float64
}

// Rect is implicitly calling the geometry interface by satisfying
// both the area() and perim() methods
func (r rect) area() float64 {
    return r.width * r.height
}
func (r rect) perim() float64 {
    return 2*r.width + 2*r.height
}

// Circle is implicitly calling the geometry interface by satisfying
// both the area() and perim() methods
func (c circle) area() float64 {
    return math.Pi * c.radius * c.radius
}
func (c circle) perim() float64 {
    return 2 * math.Pi * c.radius
}

func measure(g geometry) {
    fmt.Println(g)
    fmt.Println(g.area())
    fmt.Println(g.perim())
}

func detectCircle(g geometry) {
    if c, ok := g.(circle); ok {
        fmt.Println("circle with radius", c.radius)
    }
}

func main() {
    r := rect{width: 3, height: 4}
    c := circle{radius: 5}

    measure(r)
    measure(c)

    detectCircle(r)
    detectCircle(c)
}

```

**When to interface**
  - Common Behavior
    - Use an interface when multiple types share common behavior, allowing you to define a set of methods that different structs can implement. This enables polymorphism, making it easier to write generic and reusable code.
  - Decoupling
    - Interfaces help decouple code by defining dependencies in terms of behavior rather than concrete types. This improves modularity and testability, as components can be swapped without changing the surrounding logic.
  - Restricting behavior
    - Interfaces can restrict behavior by exposing only the necessary methods, even if the underlying type has many more. This enforces encapsulation and ensures consumers interact with a limited and well-defined API.

**When not to interface**
  - When there's only one implementation - (Also don't use it prematurely)
    - If you only have one use case, don't add abstraction by using an interface.  Even if you think that maybe down the road you might have more use cases. Note that in comments but don't implement. It clusters code and makes it much more difficult to follow. 
  - When it hides meaningful behavior
  - When performance is critical
  - Empty interfaces - the any type - 
---


**Interface Pollution**

**The bigger the interface, the weaker the abstraction. —Rob Pike**

"...interfaces are made to create abstractions. And the main caveat when programming meets abstractions is remembering that abstractions should be discovered, not created. What does this mean? It means we shouldn’t start creating abstractions in our code if there is no immediate reason to do so." - Teiva Harsanyi - 100 Go Mistakes and How to Avoid Them





#### Tips for using interfaces:
> * Use them sparingly
> * 
> * 
> * 
> * Comments can be your friend.  Since interfaces are implied, note where you have types that enrolled in an interface
> * 
> * Beware Ye the empty interface - interface{} with no methods (Only on discovery, not in production)

#### Quick Reference Recap
> * Beware Ye the empty interface - interface{} with no methods (Only on discovery, not in production)
> * 
> * 
> * 
> * 
> * 
> *

_see [Tour of Go](https://go.dev/tour/methods/9)_
_see [100 Go Mistakes](https://medium.com/@matryer/line-of-sight-in-code-186dd7cdea88)_
