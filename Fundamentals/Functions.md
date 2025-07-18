Functions in Swift 

Ciao! Functions are really the foundation for most programming languages so it shouldn't be a surprise that Swift follows suite. If you are familiar with programming languages then you probably have used functions before, here is what they look like in Swift: 

```swift
// Function that performs an action but doesn't return anything
func sayHello() {
    print("Hello")
}

// Function with parameters
func sayMyName(myName: String) {
    print(myName)
}

// Function that returns a value
func capitalizeMyName(myName: String) -> String {
    return myName.capitalized
}
```

Above is a list of simple functions that are meant to introduce you to the syntax. You simply declare a func with the 'func' keyword, the name of the function, parentheses that contain values being passed in, and the type of value that is being returned if any. One thing to note is that when values are passed in a function they are treated as let values so they are immutable for safety. Here are some more functions I used in a recent program: 

```swift

// Helper function to update X destination
    func generateRandomX() -> Double {
        return Double(Int.random(in: -100..<Int(UIScreen.main.bounds.width - 50)))
    }
    
// Helper function to update Y destination. Uses the previous location to add lower bound
    func generateRandomY(prevHeight: Double) -> Double {
        return Double(Int.random(in: Int(prevHeight - 100)..<Int(prevHeight + 35)))
    }

// Swapping values. Paremeter values become muttable because of inout keyword
func swapWithInAndOut<T>(_ val1: inout T, _ val2: inout T) {
    let temp = val1
    val1 = val2
    val2 = temp
    print(val1, val2)

}

```
And that is how to use functions. Functions are a great way to organize your code and create a more modular enviroment. The best way to learn about them is to use them in practice. 


