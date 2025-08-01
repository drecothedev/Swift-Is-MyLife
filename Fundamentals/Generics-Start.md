Generics in Swift

Generics give you a way to write more flexible functions because they allow you to perform operations on any value types. They give us the freedom to write less redundant code. 

```swift
    func swapTwoInts(_ a: inout Int, _ b: inout Int) {
        let temporaryA = a
        a = b
        b = temporaryA
    } 
    
    func swapTwoStrings(_ a: inout String, _ b: inout String) {
        let temporaryA = a
        a = b
        b = temporaryA
    } 
    
    // Example taken straight from Apples Documentation 
    
    // With "inout" keyword
    func swipSwapInAndOut<T>(_ val1: inout T, _ val2: inout T) {
        let temp = val1
        val1 = val2
        val2 = temp
        print(val1, val2)
    
    }
    
    var val1 = "Hello"
    var val2 = "World"
    var val1Num = 5
    var val2Num = 10
    
    print(swipSwapNormal(val1, val2))
    print(swipSwapInAndOut(&val1, &val2)) // Notice the Amperson next to the "inout" value being passed in.
    print(swipSwapInAndOut(&valNum1, &valNum2))

```
With our Generic vals we can easily repeat the same method without having to specify the type, which leads to more reusable code. 
