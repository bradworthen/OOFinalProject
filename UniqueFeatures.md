# **Unique Features of the Language**

### **Does the language have any particularly unique features?**
* **Swift**

**Closures unified with function pointers**

**Optionals**

**Functional programming patterns.**

**Generics**

* **Kotlin**  https://www.emanprague.com/en/blog/kotlin-top-10-features-youll-love/

**Inter-operable with java**

**High order function**
If your function accepts function as a parameter or returns function as a result than it’s called high order function. 
```kotlin
fun addValue(operation:(Int,Int) -> Int):Int {
    return operation(10,20)
}
addValue{num1,num2 -> num1 * num2} //This will print 200
addValue{num1,num2 -> num1 - num2} //This will print -10
```
**Null safety**

**Defaulted parameters**
