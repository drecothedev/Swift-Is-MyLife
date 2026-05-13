@discardableResult in Swift! 

Ciao! if you were ever annoyed about that warning you get when you call a method that returns a value without assigning such to a variable here is the solution. This will tell the compiler/Xcode not to yell at you or warn you about not assigning the method call to a variable. It is useful when using a method that will be checked using a while loop, or... other ways i am pretty sure. For me though i have only used it while using a method returning a bool as the condition in a while loop. 

```swift

@discardableResult
func match(val: Int) -> Bool {
  let num = 5
  return val == num
}
```
