😏 Flat Map Swift

Unless you've been living under a rock, you've probably seen my most previous post about maps in Swift ( jk ). Similar to my experience with maps, Flat Maps also creeped me out a bit at first. But I guess I know enough about them now to at least start talking about them. I still need a lot more practice so hmu if you have tips or feedback on this post. 

Flat Maps are ( again ) essentially a built in for loop for you that Swift offers. If you are not fimiliar with Map in Swift maybe check that out first. But here is  refresher: 

```swift
// MAP Example:

let numbers = [1, 2, 3, 4]
let numbersMap = numbers.map { Array(repeating: $0, count: $0) }

// OUTPUT: 
// [[1], [2, 2], [3, 3, 3], [4, 4, 4, 4]]

// Source: https://developer.apple.com/documentation/swift/sequence/flatmap(_:)-jo2y

```
The code above is useful for transforming an array based on what we ask but it is not very useful to work with afterwards. We are stuck with an array of nested arrays. In order to access each element we would need to unpack each array within the original array which is exhausting. Instead Swift offers flatmap which handles a couple of things. The first being flattening Arrays. Don't worry I also didn't know what flattened meant, it means to remove one layer of nesting. For example, a [[Int]] (an array of arrays) becomes a flat [Int]

```swift

let array = [1,2,3,4]

print(array.flatMap { Array(repeating: $0, count: $0) })

// OUTPUT: 
[1, 2, 2, 3, 3, 3, 4, 4, 4, 4]

```
As we can see Swift handles the unpacking of each array and gives a much more accessible array to work with. It is also great for using with optionals values within an array. Let's look at these two different examples: 

```swift
// Using the ordinary map method:

let optionalStrings: [String?] = ["Swift", nil, "is", "my", nil, "wife"]

let mappedStrings = optionalStrings.map { $0?.uppercased() }

// OUTPUT
[Optional("SWIFT"), nil, Optional("IS"), Optional("MY"), nil, Optional("WIFE")]
```

As you can see using just the regular map method give us this freaky ahh response which would be pretty messy to deal with. Lets try the same with flat map: 

```swift
// Using flat map method

let flatMappedStrings = optionalStrings.flatMap { $0?.uppercased() }
print(flatMappedStrings)

// OUTPUT
["SWIFT", "IS", "MY", "WIFE"]

```
And look how nice that looks in comparison to the first example. Flat map automatically unwraps optional values making them far simpler to work with later. 

Well guys that is my ted talk about flat maps. As I mentioned earlier I want more real world experience before I claim expertise so please provide feedback and tips. Thanks, Ciao!


