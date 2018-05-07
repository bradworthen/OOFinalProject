# Procedural Programming

## Swift
Swift supports procedural programming 

## Kotlin
While Kotlin is a pure OOP language, it also supports procedural programming. With Kotlin, functions and variables can be defined without placing them explicitly in classes, unlike Java.

```Kotlin
val rectangle = mutableMapOf("Width" to 10, "Height" to 10, "Color" to "Red")
 
fun calcArea(shape : Map<String, Any>) : Int {
    return shape["Height"] as Int * shape["Width"] as Int
}
 
fun toString(shape : Map<String, Any>) : String {
    return "Width = ${shape["Width"]}, Height = ${shape["Height"]}, Color = ${shape["Color"]}, Area = ${calcArea(shape)}"
}
```
