Ciao!👋🏽

```swift
func missingInteger(_ nums: [Int]) -> Int {
    guard var countSum = nums.first else { return 0 }
    guard nums.count > 1 else { return countSum }
    for i in 1...nums.count - 1 {
        if nums[i-1] + 1 == nums[i] {
            countSum += nums[i]
        } else {
            break
        }
    }
    
    if !nums.contains(countSum) {
        return countSum
    } else {
        while nums.contains(countSum) {
            countSum += 1
        }
    }
    return countSum
}
```

Pretty difficult one. I had to check some different solutions for this one and kind of had to frankenstien my own solution. I basically check that the numbers are sequential in the first for loop and then check for the current sum in the array. If it isn't in the array then we keep increasing. It said that my runtime beats 100% but i am not sure how. I believe we are looping through the array twice giving us a runtime of O(2n). 
