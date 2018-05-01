# **Null/nil references**


### **Which does the language use? (null/nil/etc)**

* **Swift:** Swift uses nil

* **Kotlin** Kotlin uses null


### **Does the language have features for handling null/nil references?**

* **Swift:**





* **Kotlin:**

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

#### 1. explicitly check if **b** is *null*, and handle the two options separately:
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
