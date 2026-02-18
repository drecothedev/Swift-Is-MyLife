for in where statements in Swift!

Ciao!👋🏽 these are statements that continue the for loop based on a condition

```swift
var listOfNums = [1,2,3,4,5]
let boVal = true

for num in listOfNums where boVal {
    print(num)
}

// prints: 1,2,3,4,5
```

```swift
var listOfNums = [1,2,3,4,5]
let boVal = true

for num in listOfNums where !boVal {
    print(num)
}

// prints nada
```

That's it!
