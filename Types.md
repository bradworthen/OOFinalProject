# **Types**

### **What types does the language support?**
* **Swift:** Use let to make a constant and var to make a variable.
```swift
let x=5 //constant
var y=5
```
The following types of basic data types are most frequently when declaring variables −
Int or UInt, Float, Double, Bool, String, Character, Optional, Tuples.

You can create a new name for an existing type using typealias. Here is the simple syntax to define a new type using typealias 
```swift
typealias newname = type
```

* **Kotlin:** Use val to make a constant and var to make a variable.
```kotlin
val x=5 //constant
var y=5
```
In Kotlin, all types are objects.
The basic data types available in Kotlin are:
Long, Int, Short, Byte, Double, Float, Char, Boolean. 
Every number type supports the following conversions:
toByte(): Byte, toShort(): Short, toInt(): Int, toLong(): Long, toFloat(): Float, toDouble(): Double, toChar(): Char. For example:
```kotlin
var x: Long=5
var y: Int=x.toInt()
```
Strings: 
Strings are represented by the type String. Strings are immutable. Elements of a string are characters that can be accessed by the indexing operation: s[i]. A string can be iterated over with a for-loop

### **Are both reference and value types supported?**
* **Swift:** Yes, types in Swift fall into one of two categories: first, “value types”, where each instance keeps a unique copy of its data, usually defined as a struct, enum, or tuple. The second, “reference types”, where instances share a single copy of the data, and the type is usually defined as a class. 
```swift
// Value type example
struct S { var data: Int = -1 }
var a = S()
var b = a						// a is copied to b
a.data = 42						// Changes a, not b
println("\(a.data), \(b.data)")	// prints "42, -1"
```
```swift
// Reference type example
class C { var data: Int = -1 }
var x = C()
var y = x						// x is copied to y
x.data = 42						// changes the instance referred to by x (and y)
println("\(x.data), \(y.data)")	// prints "42, 42"
```
* **Kotlin:** Since all types are objects, Kotlin only supports reference types. 

### **Can new value types be created?**
* **Swift:** Yes, Swift offers the programmer a rich assortment of built-in as well as user-defined data types. 
* **Kotlin:** New Classes can be created but new value types cannot. 
