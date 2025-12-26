Search Position In Swift

Ciao!👋🏽 For leet code problem #35 we are tasked with finding the location of a value within a set of numbers. If the value doesn't exist we return the index of where the value should be placed ( in ascending order ). Since the array is sorted and we are potentially looking for a value, I figured Binary Search must be the fastest algorithim giving us O(log n). 

```swift
func searchInsert(_ nums: [Int], _ target: Int) -> Int {
        var l = 0 
        var r = nums.count - 1 
        var correctIndex = 0
        
        while l <= r {
            let m = (l+r) / 2
            if target < nums[m] {
                r = m - 1
            } else if target > nums[m] {
                l = m + 1
            } else {
                return m
            }
            correctIndex = m
        }
        return l 
    }
```

Hmu if you have any feedback/questions. 
