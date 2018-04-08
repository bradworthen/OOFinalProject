# **Classes**

### **Defining**
* **Swift:** Use class followed by the class’s name to create a class.
```swift
Class classname{
}
```
* **Kotlin:** Classes in Kotlin are declared using the keyword class:
```kotlin
Class classname{
}
```
### **Creating new instances**
* **Swift:** Create an instance of a class by putting parentheses after the class name. We do not use the new keyword. 
```swift
var shape = Shape()
```
* **Kotlin:** Note that Kotlin does not have a new keyword. To create an instance of a class, we call the constructor as if it were a regular function:
```kotlin
val invoice = Invoice()

val customer = Customer("Joe Smith")
```
### **Constructing/initializing**
* **Swift:** Use init to create a constructor inside a class.
```swift
class NamedShape {
    var numberOfSides: Int = 0
    var name: String
    
    init(name: String) {
        self.name = name
    }
    
    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides.
    }
}
```
* **Kotlin:** A class in Kotlin can have a primary constructor and one or more secondary constructors. The primary constructor is part of the class header: it goes after the class name (and optional type parameters).
```kotlin
class Person constructor(firstName: String) {
}
```
If the primary constructor does not have any annotations or visibility modifiers, the constructor keyword can be omitted:
```kotlin
class Person(firstName: String) {
}
```
Secondary Constructors:
The class can also declare secondary constructors, which are prefixed with constructor:
```kotlin
class Person {
    constructor(parent: Person) {
        parent.children.add(this)
    }
}
```
### **Destructing/de-initializing**
* **Swift:**
Use deinit to create a deinitializer if you need to perform some cleanup before the object is deallocated.

* **Kotlin:**
Kotlin currently does not have a way to deinitialize objects.
