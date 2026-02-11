Ciao!👋🏽

```swift
func longestCommonPrefix2(_ strs: [String]) -> String {
    // Check for empty string
    guard let first = strs.first else { return ""}
    // Find the length of the shortest string
    let minCount = strs.map { $0.count }.min() ?? 0
    
    var commonPrefix = ""
    
    for i in 0...minCount - 1 {
        let idx = first.index(first.startIndex, offsetBy: i)
        let ch = first[idx]
        
        for str in strs {
            let sIdx = str.index(str.startIndex, offsetBy: i)
            if str[sIdx] != ch {
                return commonPrefix
            }
        }
        commonPrefix.append(ch)
    }
    
    return commonPrefix
}
```

This solution compares each of the words to the first word using a for loop and a nested for loop. The outter for loop is meant to index the first string and the nested for loop indexes each string after. Once there is a mismatch we immediately return our string. If there is no mismatch between all of the strings for that certain charcter, the character is added to our returned string. 
