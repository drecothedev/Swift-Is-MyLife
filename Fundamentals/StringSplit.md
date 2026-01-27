Spliting Strings in Swift

Ciao 👋🏽! Here is some information about spliting strings in Swift. I am currently working on building a compiler/language so string splitting has become pretty common for me. Here is tutorial on its use cases. When using split, you are calling a method that returns a new sub sequence of the string. This means that you will get some type of collection type of characters or strings to use. For example: 

```swift
// We split on the space.
print("Hello World".split(separator: " "))

// prints: (["Hello", "World"])
```
Pretty simple right. You can also add more parameters for the split including max splits: 

```swift
print("Hello World How are you today".split(separator: " ", maxSplits: 2))

// This will print : ["Hello", "World", "How are you today"]
```
Just thought this may be useful for later!


