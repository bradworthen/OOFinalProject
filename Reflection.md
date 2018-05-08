# Reflection

## Swift
Reflection is something that you normally don’t use with statically typed languages like Swift. However, reflection support has been present since Swift 2, offering a read-only access to the properties of an instance, and, although still very limited (you can’t access computed properties and functions with it), it finds application in some cases.

Swift reflection should rather be called *introspection*, as its current functionality allows us to look at the objects’ properties without modifying them. The concept is represented by **Mirror structure**. The API’s overview explicitly states it’s focused on a particular instance rather than on type. Let’s explore what’s available.

A mirror describes the parts that make up a particular instance, such as the instance’s stored properties, collection or tuple elements, or its active enumeration case. Mirrors also provide a “display style” property that suggests how this mirror might be rendered.

Playgrounds and the debugger use the **Mirror** type to display representations of values of any type. For example, when you pass an instance to the dump(_:_:_:_:) function, a mirror is used to render that instance’s runtime contents.
```swift
struct Point {
    let x: Int, y: Int
}

let p = Point(x: 21, y: 30)
print(String(reflecting: p))
// Prints "▿ Point
//           - x: 21
//           - y: 30"
```

## Kotlin
Kotlin makes functions and properties first-class citizens in the language, and introspecting them (i.e. learning a name or a type of a property or function at runtime) is closely intertwined with simply using a functional or reactive style.

### Class References
The most basic reflection feature is getting the runtime reference to a Kotlin class. To obtain the reference to a statically known Kotlin class, you can use the class literal syntax:
```kotlin
val c = MyClass::class
```
The reference is a value of type KClass.
### Bound Class References
You can get the reference to a class of a specific object with the same ::class syntax by using the object as a receiver:
```kotlin
val widget: Widget = ...
assert(widget is GoodWidget) { "Bad widget: ${widget::class.qualifiedName}" }
```
You obtain the reference to an exact class of an object, for instance GoodWidget or BadWidget, despite the type of the receiver expression (Widget).
### Callable references
References to functions, properties, and constructors, apart from introspecting the program structure, can also be called or used as instances of function types.

The common supertype for all callable references is KCallable<out R>, where R is the return value type, which is the property type for properties, and the constructed type for constructors.
#### Function References
When we have a named function declared like this:

fun isOdd(x: Int) = x % 2 != 0
We can easily call it directly (isOdd(5)), but we can also use it as a function type value, e.g. pass it to another function. To do this, we use the :: operator:

```kotlin
val numbers = listOf(1, 2, 3)
println(numbers.filter(::isOdd))
```
Here ::isOdd is a value of function type (Int) -> Boolean.
### Property References
To access properties as first-class objects in Kotlin, we can also use the :: operator:

```kotlin
val x = 1

fun main(args: Array<String>) {
    println(::x.get())
    println(::x.name) 
}
```

The expression ::x evaluates to a property object of type KProperty<Int>, which allows us to read its value using get() or retrieve the property name using the name property. For more information, please refer to the docs on the KProperty class.
### Interoperability With Java Reflection
On the Java platform, standard library contains extensions for reflection classes that provide a mapping to and from Java reflection objects (see package kotlin.reflect.jvm). For example, to find a backing field or a Java method that serves as a getter for a Kotlin property, you can say something like this:
```kotlin
import kotlin.reflect.jvm.*
 
class A(val p: Int)
 
fun main(args: Array<String>) {
    println(A::p.javaGetter) // prints "public final int A.getP()"
    println(A::p.javaField)  // prints "private final int A.p"
}
```
To get the Kotlin class corresponding to a Java class, use the .kotlin extension property:
```kotlin
fun getKClass(o: Any): KClass<Any> = o.javaClass.kotlin
```
