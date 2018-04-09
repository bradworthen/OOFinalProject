# **Comparisons of references and values**

### **How are values compared? (i.e. comparing two strings)**
* **Swift:** 

| Swift Comparison Operators: |
|------------ |
|Value Equal to (a == b)|
|Value Not equal to (a != b)|
|Reference Equal to (a===b)|
|Reference not Equal(a!==b)|
|Greater than (a > b)|
|Less than (a < b)|
|Greater than or equal to (a >= b)|
|Less than or equal to (a <= b)|
Each of the comparison operators returns a Bool value to indicate whether or not the statement is true
```swift
1 == 1   // true because 1 is equal to 1
2 != 1   // true because 2 is not equal to 1
2 > 1    // true because 2 is greater than 1
1 < 2    // true because 1 is less than 2
1 >= 1   // true because 1 is greater than or equal to 1
2 <= 1   // false because 2 is not less than or equal to 1
```
String and character equality is checked with the “equal to” operator (==) and the “not equal to” operator (!=)
```swift
let quotation = "We're a lot alike, you and I."
let sameQuotation = "We're a lot alike, you and I."
if quotation == sameQuotation {
    print("These two strings are considered equal")
}
// Prints "These two strings are considered equal"
```

* **Kotlin:** 

| Kotlin Comparison Operators: |
|------------ |
|Value Equal to (a == b)|
|Value Not equal to (a != b)|
|Reference Equal to (a===b)|
|Reference not Equal(a!==b)|
|Greater than (a > b)|
|Less than (a < b)|
|Greater than or equal to (a >= b)|
|Less than or equal to (a <= b)|

All comparison operators are translated to calls of compareTo which returns an Int. 
Expression	Translated to

|Expression | Translated to: |
|-----------|:---------------|
|a > b	    | a.compareTo(b) > 0|
|a < b	    | a.compareTo(b) < 0|
|a >= b	    | a.compareTo(b) >= 0|
|a <= b	    | a.compareTo(b) <= 0|

String and character equality is checked with the “equal to” operator (==) and the “not equal to” operator (!=)
```kotlin
val quotation = "We're a lot alike, you and I."
val sameQuotation = "We're a lot alike, you and I."
if (quotation == sameQuotation) {
    print("These two strings are considered equal")
}
// Prints "These two strings are considered equal"
```
