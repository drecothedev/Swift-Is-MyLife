Optionals in Swift

When I first started learning Swift I had no idea what optionals were. The idea of optionals wasn't too hard for be grasp - A variable either has a value or doesn't. The part that confused me was unwrapping oprionals. Even at the point of understanding optionals I still think the syntax, in some instances, is pretty niche and confusing to read at first. Here are some optionals and some unwrapping of optionals with very simple examples and explanations: 

```swift

var aRegularValue: String = ""
var anOptionalValue: String? 

-----------------------------------------------------------

var aRegularValue: String // ❌ Will not work becuase aRegularValue cannot be nil 
var anOptionalValue: String? // ✅ This can

```

And that is the fundamental difference between optional variables and regular variables. Pretty Str8 forward. Now for the juicy stuff. B4 using the variable you will need to unwrap the variable. This means that you need to check whether or not the variable is nil before using it. There are a few ways to do so. 

Optional Binding: 

This is the most common ( in my opinion ) way that optionals are used in code. This was also very very weird for me to read at first. It also works with guard let and switch statements: 

```swift

print(anOptionalValue) // ⚠️ Gives this warning " Expression implicitly coerced from 'String?' to 'Any' "

// ✅ Assign the unwrapped value to a new let value that is only available within the current scope
if let optionalValue = anOptionalValue {
    print(optionalValue)
}

```


Optional Chaining: 

I don't use this as often tbh and when I do XCode usually does it for me so this example is directly from the Swift Documentation

```swift
if imagePaths["star"]?.hasSuffix(".png") == true {
    print("The star image is in PNG format")
}
```

It looks like this code checks to see if the "star" path exist before checking for the suffix. 


Nil-Coalescing Operator: 

I use this a decent amount especially when using SwiftUI. It is the quickest safe way to handle optionals

```swift

print(anOptionalValue ?? "There is no value") 😏

```
This is one is extremely useful because provides a default just in case the varaible is empty. Think about what would happen if you deleted your instagram profile pic. It would fill the pic with some default avatar. You can also chain these together but I have not done this in practice yet. 


Unconditional Unwrapping: ☠️

This is the most dangerous way to unwrap an optional. Really wouldn't use it unless you are certain the value is gonna be present, otherwise your app will crash. 

```swift 

var anOptionalValue: String?

print(anOptionalValue!) ❌ // Will Crash

```
This will crash because the optional value was never assigned to anything therefore making it nil. nil = crash when using "!" to unwrap optionals


```swift 

var anOptionalValue: String? = "Hello world"

print(anOptionalValue!) // ⚠️ Will not crash but still be careful

```

And just like that we know how to handle optionals. 






