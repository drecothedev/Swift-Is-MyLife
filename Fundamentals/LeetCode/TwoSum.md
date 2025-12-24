Two Sum in Swift 

Ciao!👋🏽 Leet code problems are all around pretty difficult. Whether the problem says easy, medium, or hard, they all suck. But they teach a lot about the language you choose to use and it makes you think differently than traditional project programming. I have been practicing a few and decided that the best way for me to internalize these problems is to explain how they work in detail. 

So for the two sum problem there are many different ways to solve it. The first would be to loop through the array of numbers and check the array for the compliment value ( the value that will increase the value at the current index to the target number ) and return those two indexes. That would be a very inefficient way to solve it though. Instead you can use a hash map, or dictionary. This will allow us to only check the array once giving a runtime of O(n). 

let's look at the code: 

```swift
func twoSum(_ nums: [Int], _ target: Int) -> [Int] {
        var lookup: [Int:Int] = [:]
        for (key,value) in nums.enumerated() {
            if let complimentIndex = lookup[value] {
                return [complimentIndex,key]
            } else {
                lookup[target - value] = key
            }
        }
        
        return [0,5]
    }
```
In this code we are creating a dictionary that is going to act as a look up table. We will add the current values compliment to the dictionary and then check for that compliment as we come across different values. Once we find a value that matches, we will return the current index, and the index of the compliments value. One thing to note is that instead of saving the compliment index as the key part of the dictionary, we are saving the compliment index as the value. so instead of it looking like [0:7] after the first iteration it will look like [7:0]. we then check to see if the value exist as a key and then return the value (index) associated with it. If this code is too confusing try writing it like this: 

```swift
func twoSum(_ nums: [Int], _ target: Int) -> [Int] {
    var lookup: [Int: Int] = [:]
    
    for (index,value) in nums.enumerated() {
        if lookup[value] != nil {
            return [lookup[value]!, index]
        } else {
            lookup[target - value] = index
        }
    }
    
    return [0,0]
}
```

To me this is a bit more straight forward to understand but you are forcefully unwrapping a variable which could crash your program. But in this we can clearly see that we are checking the lookup table's keys for the current value we are checking for. if it exist we return the value associated with that key and then the current number we are checking for. 
