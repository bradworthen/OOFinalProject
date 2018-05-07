# Name spaces
## How are name spaces implemented?
### Swift
Swift modules make the need for class prefixes as seen in Objective-C obsolete. Swift currently doesn't offer a direct solution to namespace types and constants within modules, however you can use structs or enums to simulate name spaces.
### Kotlin
In Kotlin packages are the closest analog of C# namespaces. You can define package with the **package** keyword in the beginning of the file.

## How are name spaces used?
### Swift
```kotlin
struct API {
    static let BaseURL = "https://example.com/v1/"
    static let Token = "sdfiug8186qf68qsdf18389qsh4niuy1"
}
```
```kotlin
enum API {
    static let BaseURL = "https://example.com/v1/"
    static let Token = "sdfiug8186qf68qsdf18389qsh4niuy1"
}
```
This solution is almost identical to the one that uses a struct. The main difference is you cannot create an instance of the **API** enum without having an error thrown at you.
### Kotlin
A source file may start with a package declaration:
```Swift
package foo.bar

fun baz() {}

class Goo {}

// ...
```
All the contents (such as classes and functions) of the source file are contained by the package declared. So, in the example above, the full name of **baz()** is **foo.bar.baz**, and the full name of **Goo** is **foo.bar.Goo**.

If the package is not specified, the contents of such a file belong to "default" package that has no name.
