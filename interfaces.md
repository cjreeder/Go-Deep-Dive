# Core - Interfaces
---
### What is an Interface type is Go
**Tour of Go Interface Definition:  An interface type is defined as a set of method signatures.**
  - ☢️ In my opinion, Tour of Go does a poor job describing what an interface is and when and how to use them.

**The Interface Type - A Better Definition**
***An Interface provides a way to specify the behavior of an object. We use interfaces to create common abstractions that multiple objects can implement. -100 Go Mistakes***
  - Interfaces are ...
    - like a contract or a set of expectations applied to a type - 
    ```
    "If your type can do these things, then you can be used whereever this interface is expected"
    ```
    - It doesn't care how your type does those things, just as long as it satisfies the methods on the interface. 
    - helpful in building reusable code across your application
    - Implicit - (No declaration statements like X implements y) - as long as it satisfies the methods, it is considered a type from that interface
    -            

**When to interface**
  - Common Behavior
  - Decoupling
  - Restricting behavior

**When not to interface**
  - When a Generic would work better
  - Any Catchall
  - 
---

### How to use an interface:
****
```go

```
**Here's a functionally equivalent block:**
```go

```
**The bigger the interface, the weaker the abstraction. —Rob Pike**
The more methods you add and build into your interface, the less abstract the interface is and thus the less reusable it can be.



#### Tips for using interfaces:
> * Beware Ye the empty interface - interface{} with no methods (Only on discovery, not in production)
> * 
> * 
> * 
> * 
> * 
> * 

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
