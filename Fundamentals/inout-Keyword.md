inout Keyword 

The inout keyword was very confusing to me at first but it is one of the simplest concepts once I leanred. I learned much about the inout statement while i had downtime at work actually. 

In Swift whenever you pass a varibale into a function by default the variable is treated as a let/constant variable within that functions scope. The solution to that could be to assign a new value or a temporary value 
to act as a placeholder to track changes. Then you can return that new value. 

In order to make that easier and more efficient Swift provides the inout keyword to let the compiler know that the value can be mutated. See examples below: 


```swift 
// Without "inout" keyword
func swipSwapNormal<T>(_ val1: T, _ val2: T) {
    var tempVal1 = val1
    var tempVal2 = val2
    
    let temp = tempVal1
    tempVal1 = tempVal2
    tempVal2 = temp
    
    print(tempVal1, tempVal2)
}


// With "inout" keyword
func swipSwapInAndOut<T>(_ val1: inout T, _ val2: inout T) {
    let temp = val1
    val1 = val2
    val2 = temp
    print(val1, val2)

}

var val1 = "Hello"
var val2 = "World"

print(swipSwapNormal(val1, val2))
print(swipSwapInAndOut(&val1, &val2)) // Notice the Amperson next to the "inout" value being passed in.

```

In this code above we are just swapping two generic values. Generic means that they can be of any type of variable. In the first code you can see how verbose it is and it just feels extra to do. The
second function is cleaner and uses less lines to acheive the same thing. Lastly, you need to pass the value into the function with the ampersam attached so that the values can be mutated. 




