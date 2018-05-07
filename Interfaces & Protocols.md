# Interfaces & Protocols
## What does the language support?
### Swift: Protocols
### Kotlin: Interfaces
## What abilities does it have?
### Swift


### Kotlin

## How is it used?
### Swift
A protocol defines a blueprint of methods, properties, and other requirements that suit a particular task or piece of functionality. The protocol can then be *adopted* by a class, structure, or enumeration to provide an actual implementation of those requirements. Any type that satisfies the requirements of a protocol is said to *conform* to that protocol.

They list off the function prototypes and variable declarations, as well as stating whether they are required or optional, but don’t actually do anything.  It is up to class, structs, or enumerations that claim to conform to the protocol to actually provide the functionality.
```Swift
protocol SomeProtocol {
    // protocol definition goes here
}
```
### Kotlin
Interfaces in Kotlin are very similar to Java 8. They can contain declarations of abstract methods, as well as method implementations. What makes them different from abstract classes is that interfaces cannot store state. They can have properties but these need to be abstract or to provide accessor implementations.
```Kotlin
interface MyInterface {
    fun bar()
    fun foo() {
      // optional body
    }
}
```
