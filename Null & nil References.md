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
