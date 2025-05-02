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
    "If your type can do these things, then it can be used whereever this interface is expected"
    ```
    It doesn't care how your type does those things, just as long as it satisfies the methods on the interface. 
    - helpful in building reusable code across your application
    - Implicit - (No declaration statements like X implements y) - as long as it satisfies the methods, it is considered a type from that interface      

### Example of an interface:
****
##### Gobyexample code - 
```go

package main

import(
    fmt 
)

type Speaker interface {
    Speak() string
}

type Dog struct{}
type Robot struct{}
type Human struct{}


func (d Dog) Speak() string {
    return "Woof!"
}

func (r Robot) Speak() string {
    return "Beep boop"
}

func (h Human) Speak() string {
    return "Hello World!"
}

func MakeItTalk(s Speaker) {
    fmt.Println(s.Speak())
}

func main() {
    d := Dog{}
    r := Robot{}
    h := Human{}

    MakeItTalk(d)
    MakeItTalk(r)
    MakeItTalk(h)
}

```

**When to use interfaces**
  - Common Behavior
    - Use an interface when multiple types share common behavior, allowing you to define a set of methods that different structs can implement. This enables polymorphism, making it easier to write generic and reusable code.
  - Decoupling
    - Interfaces help decouple code by defining dependencies in terms of behavior rather than concrete types. This improves modularity and testability, as components can be swapped without changing the surrounding logic.
  - Restricting behavior
    - Interfaces can restrict behavior by exposing only the necessary methods, even if the underlying type has many more. This enforces encapsulation and ensures consumers interact with a limited and well-defined API.

**When not to use interfaces**
  - When there's only one implementation - (Also don't use it prematurely)
    - If you only have one use case, don't add abstraction by using an interface.  Even if you think that maybe down the road you might have more use cases. Note that in comments but don't implement. It clusters code and makes it much more difficult to follow. 
  - When it hides meaningful behavior
    - Interfaces can obscure functionality of different types if consumers only see a limited method set. This can lead to confusion or inefficiency when developers need access to capabilities that the interface doesn’t expose.
  - When performance is critical
    - Interfaces involve dynamic dispatch, which adds a small runtime cost. In tight loops or performance-critical paths, concrete types and function calls may be more efficient. In order to find the concrete type that the interface is pointing to, the compiler will look for that type using a hash table which adds a little bit more time to the call. 

---

**Interface Pollution**

**The bigger the interface, the weaker the abstraction. —Rob Pike**

"...interfaces are made to create abstractions. And the main caveat when programming meets abstractions is remembering that abstractions should be discovered, not created. What does this mean? It means we shouldn’t start creating abstractions in our code if there is no immediate reason to do so." - Teiva Harsanyi - 100 Go Mistakes and How to Avoid Them

Interface pollution happens when an interface bloats with large sets of methods.  This makes the interface difficult to implement when types need to implement all the methods especially if the type doesn't actually need all the methods.  

**How to fix this issue**
#### Interface Composition
Embedding interfaces into each other - Interface inception - one interface to rule them all.  


**Empty interfaces - the any type**

One of the common practices that many new Go programmers are tempted to implement are empty interfaces since interfaces can use any type. This bypasses one of Go's benefits in being a statically typed language.  

Any data type can be placed in an interface.  In Go 1.18, a new type was created called any which implements an empty interface. 

See the following code:
```go
var mydata interface{}
var anydata any
mydata = 42
mydata = "Cosmo rocks!"
mydata = SillyStruct{}

anydata = 5
anydata = "Still Working"
```

This obscures the type information about the items in the interface. In order to see what is inside the interface requires using a type assertion to interrogate the interface and discover what is inside. (It's like a mystery box of types that can only be opened through type assertions to interrogate the data.)

Empty interfaces have their place though.  We usual use empty interfaces when we are unsure of what type of data will be returned from an API or device. 

#### Empty interface usage
> * Handling Arbitrary Input from sources you don't necessarily control and don't know the structure of ahead of time. (ie APIs)
> * Generic collections of data in slices or maps that hold multiple different types. (Not recommended)
> * Communicating with Third party libraries - some libraries accept or return an interface{} to build flexibility into the library (ie database drivers)
> * Writing Middleware or plugins - Empty interfaces let you plug in any handler, callback, or data type, especially when you define your own type system or registry.

#### Tips for using interfaces:
> * Use them sparingly - keep them small and simple
> * Interfaces are implicit - keep track of usage and methods appropriately
> * Comments can be your friend.  Since interfaces are implied, note where you have types that enrolled in an interface
> * Interfaces 
> * 
> * 
> * Beware warry of the empty interface - (Only on discovery, not in production)

_see [Tour of Go](https://go.dev/tour/methods/9)_
_see [100 Go Mistakes and How to Avoid Them](https://learning.oreilly.com/library/view/100-go-mistakes/9781617299599/OEBPS/Text/02.htm#heading_id_14)_
_see [Go (Golang) Tutorial #22 - Interfaces](https://www.youtube.com/watch?v=lbW-KVdIXaY)_
_see [Go by Example: Interfaces](https://gobyexample.com/interfaces)_
_see [Golang: The Last Interface Explanation You'll Ever Need](https://www.youtube.com/watch?v=SX1gT5A9H-U&t=738s)_
