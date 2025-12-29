Longest Consecutive Sequence in Swift

Ciao!👋🏽 This is one of the first medium difficulty level problem that i partially solved. I ended up getting stuck when trying to pass all of leetcodes test cases, which ultimately means i would have failed. Here is my original algorithim for this problem: 

```swift
func longestConsecutive(_ nums: [Int]) -> Int {
    var lookup: [Int: Int] = [:]
    var count = 1
    guard nums.count > 0 else { return 0 }
    for num in nums {
        if lookup[num] == nil {
            lookup[num] = 0
        }
    }
    
    for key in lookup.keys {
        if lookup[key+1] != nil { // if num + 1 exist
            count += 1
        }
    }
    return count
}
```

My oringal thought was to add all of the values to a hashset and check to see if that value + 1 was in the hashset. If so I added to the count. Obviously this isn't the most efficient algorithim but it was my brute force attempt to solve the problem. I got stuck trying to figure out how to initialize the count at 0 and count the first number in the sequence. I then looked at the solutions on leetcode, and i took a little bit of time to understand what exactly is going on with their algorithim. Here is that code: 

```swift
// This is not my alogrithim!!
// Credit to smthinthewayy https://leetcode.com/u/smthinthewayy/

    func longestConsecutive(_ nums: [Int]) -> Int {
        let set = Set(nums)
        var longestStreak = 0 

        for num in set {
            if !set.contains(num-1) {
                var currentNum = num
                var currentStreak = 1 

                while set.contains(currentNum + 1) {
                    currentNum += 1
                    currentStreak += 1
                }

                longestStreak = max(longestStreak, currentStreak)
            }
        }
        return longestStreak
    }
```
From my understanding we create a set to remove duplicates from our original nums array. We then check if each number has their complimentary value (val+1) and if it does we check for that values compliment and repeat for each number. We then add to our current streak and if it longer than our original streak we update that to be our longest streak. Again this is not my work but i figured posting it on here my be helpful for people who don't want to try to solve the problem on the leetcode website. 
