# **Null/nil references**


### **Which does the language use? (null/nil/etc)**

* **Swift:** Swift uses nil

* **Kotlin** Kotlin uses null


### **Does the language have features for handling null/nil references?**

## **Swift:**

### Optional Chaining
Optional chaining is a process for querying and calling properties, methods, and subscripts on an optional that might currently be *nil*. If the optional contains a value, the property, method, or subscript call succeeds; if the optional is *nil*, the property, method, or subscript call returns *nil*. Multiple queries can be chained together, and the entire chain fails gracefully if any link in the chain is *nil*.

To reflect the fact that optional chaining can be called on a nil value, the result of an optional chaining call is always an optional value, even if the property, method, or subscript you are querying returns a nonoptional value. You can use this optional return value to check whether the optional chaining call was successful (the returned optional contains a value), or did not succeed due to a nil value in the chain (the returned optional value is *nil*).

Specifically, the result of an optional chaining call is of the same type as the expected return value, but wrapped in an optional. A property that normally returns an **Int** will return an **Int?** when accessed through optional chaining.

The next several code snippets demonstrate how optional chaining differs from forced unwrapping and enables you to check for success.

First, two classes called **Person** and **Residence** are defined:

```Swift
class Person {
    var residence: Residence?
}
 
class Residence {
    var numberOfRooms = 1
}
```
**Residence** instances have a single **Int** property called **numberOfRooms**, with a default value of 1. **Person** instances have an optional **residence** property of type **Residence?**.

If you create a new **Person** instance, its **residence** property is default initialized to *nil*, by virtue of being optional. In the code below, **john** has a **residence** property value of *nil*:

```Swift
let john = Person()
```

If you try to access the **numberOfRooms** property of this person’s **residence**, by placing an exclamation mark after **residence** to force the unwrapping of its value, you trigger a runtime error, because there is no **residence** value to unwrap:

```Swift
let roomCount = john.residence!.numberOfRooms
// this triggers a runtime error
```

The code above succeeds when **john.residence** has a non-*nil* value and will set **roomCount** to an **Int** value containing the appropriate number of rooms. However, this code always triggers a runtime error when **residence** is *nil*, as illustrated above.

Optional chaining provides an alternative way to access the value of **numberOfRooms**. To use optional chaining, use a question mark in place of the exclamation mark:

```Swift
if let roomCount = john.residence?.numberOfRooms {
    print("John's residence has \(roomCount) room(s).")
} else {
    print("Unable to retrieve the number of rooms.")
}
// Prints "Unable to retrieve the number of rooms."
```

This tells Swift to “chain” on the optional **residence** property and to retrieve the value of **numberOfRooms** if **residence** exists.

Because the attempt to access **numberOfRooms** has the potential to fail, the optional chaining attempt returns a value of type **Int?**, or “optional **Int**”. When **residence** is *nil*, as in the example above, this optional **Int** will also be *nil*, to reflect the fact that it was not possible to access **numberOfRooms**. The optional **Int** is accessed through optional binding to unwrap the integer and assign the nonoptional value to the **roomCount** variable.

Note that this is true even though **numberOfRooms** is a nonoptional **Int**. The fact that it is queried through an optional chain means that the call to **numberOfRooms** will always return an **Int?** instead of an **Int**.

You can assign a **Residence** instance to **john.residence**, so that it no longer has a *nil* value:
```Swift
john.residence = Residence()
```

**john.residence** now contains an actual **Residence** instance, rather than *nil*. If you try to access **numberOfRooms** with the same optional chaining as before, it will now return an **Int?** that contains the default **numberOfRooms** value of 1:

```Swift
if let roomCount = john.residence?.numberOfRooms {
    print("John's residence has \(roomCount) room(s).")
} else {
    print("Unable to retrieve the number of rooms.")
}
// Prints "John's residence has 1 room(s)."
```
#### **Defining Model Classes for Optional Chaining**
You can use optional chaining with calls to properties, methods, and subscripts that are more than one level deep. This enables you to drill down into subproperties within complex models of interrelated types, and to check whether it is possible to access properties, methods, and subscripts on those subproperties.

The code snippets below define four model classes for use in several subsequent examples, including examples of multilevel optional chaining. These classes expand upon the **Person** and **Residence** model from above by adding a **Room** and **Address** class, with associated properties, methods, and subscripts.

The **Person** class is defined in the same way as before:
```Swift
class Person {
    var residence: Residence?
}
```
The **Residence** class is more complex than before. This time, the **Residence** class defines a variable property called **rooms**, which is initialized with an empty array of type **Room**:
```Swift
class Residence {
    var rooms = [Room]()
    var numberOfRooms: Int {
        return rooms.count
    }
    subscript(i: Int) -> Room {
        get {
            return rooms[i]
        }
        set {
            rooms[i] = newValue
        }
    }
    func printNumberOfRooms() {
        print("The number of rooms is \(numberOfRooms)")
    }
    var address: Address?
}
```
Because this version of **Residence** stores an array of **Room** instances, its **numberOfRooms** property is implemented as a computed property, not a stored property. The computed **numberOfRooms** property simply returns the value of the **count** property from the **rooms** array.

As a shortcut to accessing its **rooms** array, this version of **Residence** provides a read-write subscript that provides access to the room at the requested index in the **rooms** array.

This version of **Residence** also provides a method called **printNumberOfRooms**, which simply prints the number of rooms in the residence.

Finally, **Residence** defines an optional property called **address**, with a type of **Address?.** The **Address** class type for this property is defined below.

The **Room** class used for the **rooms** array is a simple class with one property called **name**, and an initializer to set that property to a suitable room name:
```Swift
class Room {
    let name: String
    init(name: String) { self.name = name }
}
```
The final class in this model is called **Address**. This class has three optional properties of type **String?**. The first two properties, **buildingName** and **buildingNumber**, are alternative ways to identify a particular building as part of an address. The third property, **street**, is used to name the street for that address:
```Swift
class Address {
    var buildingName: String?
    var buildingNumber: String?
    var street: String?
    func buildingIdentifier() -> String? {
        if let buildingNumber = buildingNumber, let street = street {
            return "\(buildingNumber) \(street)"
        } else if buildingName != nil {
            return buildingName
        } else {
            return nil
        }
    }
}
```
The **Address** class also provides a method called **buildingIdentifier()**, which has a return type of **String?**. This method checks the properties of the address and returns **buildingName** if it has a value, or **buildingNumber** concatenated with **street** if both have values, or *nil* otherwise.

## **Kotlin:**

Kotlin's type system is aimed to eliminate NullPointerExceptions from its code. The only possible causes of NPEs may be:

* An explicit call to throw **NullPointerException()**;
* Usage of the **!!** operator that is described below;
* Some data inconsistency with regard to initialization, such as when:
  * An uninitialized _**this**_ available in a constructor is passed and used somewhere ("leaking _**this**_");
  * A superclass constructor calls an open member whose implementation in the derived class uses uninitialized state;
* Java interoperation:
  * Attempts to access a member on a **null** reference of a platform type;
  * Generic types used for Java interoperation with incorrect nullability, e.g. a piece of Java code might add **null** into a Kotlin **MutableList<String>**, meaning that **MutableList<String?>** should be used for working with it;
  * Other issues caused by external Java code.


In Kotlin, the type system distinguishes between references that can hold _**null**_ (nullable references) and those that can not (non-null references). For example, a regular variable of type **String** can not hold _**null**_:

```kotlin
var a: String = "abc"
a = null // compilation error
```

To allow nulls, we can declare a variable as nullable string, written String?:
```kotlin
var b: String? = "abc"
b = null // ok
```
Now, if you call a method or access a property on a, it's guaranteed not to cause an NPE, so you can safely say:

```kotlin
val l = a.length
```
But if you want to access the same property on b, that would not be safe, and the compiler reports an error:
```kotlin
val l = b.length // error: variable 'b' can be null
```
### Checking for **null** in conditions:

#### 1. Explicitly check if **b** is *null*, and handle the two options separately:
```kotlin
val l = if (b != null) b.length else -1
```
The compiler tracks the information about the check you performed, and allows the call to length inside the if. More complex conditions are supported as well:
```kotlin
if (b != null && b.length > 0) {
    print("String of length ${b.length}")
} else {
    print("Empty string")
}
```
Note that this only works where b is immutable (i.e. a local variable which is not modified between the check and the usage or a member val which has a backing field and is not overridable), because otherwise it might happen that b changes to null after the check.
#### 2. Safe Calls --- the safe call operator, written **__?.__** :
```kotlin
b?.length
```
This returns **b.length** if **b** is *not null*, and *null* otherwise. The type of this expression is **Int?**.

Safe calls are useful in chains. For example, if Bob, an Employee, may be assigned to a Department (or not), that in turn may have another Employee as a department head, then to obtain the name of Bob's department head (if any), we write the following:

```kotlin
bob?.department?.head?.name
```
Such a chain returns null if any of the properties in it is null.

To perform a certain operation only for non-null values, you can use the safe call operator together with let:
```kotlin
val listWithNulls: List<String?> = listOf("A", null)
for (item in listWithNulls) {
     item?.let { println(it) } // prints A and ignores null
}
```
A safe call can also be placed on the left side of an assignment. Then, if one of the receivers in the safe calls chain is null, the assignment is skipped, and the expression on the right is not evaluated at all:
```kotlin
// If either `person` or `person.department` is null, the function is not called:
person?.department?.head = managersPool.getManager()
```
#### Elvis Operator

When we have a nullable reference __*r*__, we can say "if __*r*__ is not *null*, use it, otherwise use some non-null value __*x*__":
```kotlin
val l: Int = if (b != null) b.length else -1
```
Along with the complete if-expression, this can be expressed with the Elvis operator, written **__?.__**:
```kotlin
val l = b?.length ?: -1
```
If the expression to the left of **__?.__** is not null, the elvis operator returns it, otherwise it returns the expression to the right. Note that the right-hand side expression is evaluated only if the left-hand side is null.

Note that, since throw and return are expressions in Kotlin, they can also be used on the right hand side of the elvis operator. This can be very handy, for example, for checking function arguments:
```kotlin
fun foo(node: Node): String? {
    val parent = node.getParent() ?: return null
    val name = node.getName() ?: throw IllegalArgumentException("name expected")
    // ...
}
```
#### 3. The !! Operator
The third option is for NPE-lovers: the not-null assertion operator (**!!**) converts any value to a non-null type and throws an exception if the value is null. We can write **b!!**, and this will return a non-null value of **b** (e.g., a **String** in our example) or throw an NPE if **b** is *null*:
```kotlin
val l = b!!.length
```
Thus, if you want an NPE, you can have it, but you have to ask for it explicitly, and it does not appear out of the blue.

#### Safe Casts
Regular casts may result into a **ClassCastException** if the object is not of the target type. Another option is to use safe casts that return *null* if the attempt was not successful:

```kotlin
val aInt: Int? = a as? Int
```
#### Collections of Nullable Type
If you have a collection of elements of a nullable type and want to filter non-null elements, you can do so by using filterNotNull:
```kotlin
val nullableList: List<Int?> = listOf(1, 2, null, 4)
val intList: List<Int> = nullableList.filterNotNull()
```
