Indexing a String in Swift!

Ciao! 👋🏽 Swift tends to be easier than lower level languages C or C++. But when it comes to parsing a string it is much more confusing. If you are familiar with some other languages when indexing a string you can simply use an int as your index. Let me show you an example in c++

```c++
for(int i = 0; i < myString.length(); i++) {
        cout << myString[i] << endl; 
    }
```
Super simple right. You just use a for loop to print out the character that i is pointing to. 

In Swift you could only do this with an array of characters, and not a string. i know right, what the helly. so you would end up having to do something like this for every string you want to "normally" index through. 

```swift
func printMyCharsSIML(_ s: String) {
    let chars = [Character](s) // Turn the string into an array of characters
    var index = 0
    for _ in chars {
        print(chars[index])
        index += 1
    }
}
```

This does make it feel a lot more familiar but it isn't very efficient. This will lengthen our runtime and consume more memory then needed. So, the solution is to use String.index. Swift implemented this for safety. Even though you can still be out of range, using String.index gives us some guard rails. Additionally, this helps with with unicode. To learn more about this take a look at this video where this dude explains in more detail why Strings are "monsters" in swift: https://www.youtube.com/watch?v=k35T7E1hxeQ

Personally i am more concerned about how to index through a string. Let's look at some code and break it down a bit: 

```swift
func printMyCharsSIML(_ s: String) {
    var index = s.startIndex // .startIndex gives us the first element of the array. The value at position 0
    for _ in s {
        print(s[index])
        index = s.index(after: index)
    }
}
```
As we can see our index is of type String.index and not integer even though it performing very similarly. To increment rather than adding to our index, will assign it ot the value dirctly after our original index. So, after the first iteration it will move to the first position. 

At times we may need to decrement our index in order to read our string from the end to the beginning, this isn't too difficult but there is a catch. 

```swift
var reverseIndex = s.endIndex
for _ in s {
        print(s[reverseIndex])
        reverseIndex = s.index(before: reverseIndex)
    }
```
As opposed to our first indexer, this will result in an out of range error. This is because endIndex returns a value that is outside of the last real value. For example, ["H","E","L","L","O"] would return a value equivalent to 5. This would mean that our index is out of range. So before reading a value using our reverse index we will want to decrement by 1. You can do this by initializing it a bit different. Here is an example: 

```swift

func printMyCharsSIML(_ s: String) {
    var index = s.startIndex
    var reverseIndex = s.index(s.endIndex, offsetBy: -1)
    // print characters in the normal order
    for _ in s {
        print(s[index])
        index = s.index(after: index)
    }
    
    // print the characters in backwards order
    for _ in s {
        print(s[reverseIndex])
        // Check for the end of our iteration. Once reverseIndex = 0 we do not need to iterate more. Remember we are offsetting each index by -1. So s[0] should be read when our indexer is 1. 
        if reverseIndex == s.startIndex { break }
        reverseIndex = s.index(before: reverseIndex)
    }
}

```

Phew! that seems like a lot of work, and frankly it is. But it is most important to remember how powerless you are and that no matter how much you fret, this is the way it is. JK. But actually 👀 this is the best way to iterate a string so get used ot it! 
