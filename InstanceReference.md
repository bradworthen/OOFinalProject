# **Instance reference name in data type (class)**

### **this? self?**
* **Swift:**
Every instance of a type has an implicit property called self, which is exactly equivalent to the instance itself. You use the self property to refer to the current instance within its own instance methods. For example:

```swift
func increment() {
    self.count += 1
}
```

* **Kotlin:**
In Kotlin this refers to the current object of that class. For example:
```kotlin
fun increment() {
    this.count += 1
}
```
