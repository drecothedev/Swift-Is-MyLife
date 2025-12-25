Roman To Integer Leetcode!

Ciao👋🏽! 

Here is my solution for leetcode problem 13. I just looped through our array once giving us an efficiency of O(n). I then use a switch statement to handle the addition logic. According to Leetcodes complexity analyzer it beats 100% of other methods.

```swift
func romanToInt(_ s: String) -> Int {
        var indexer: String.Index = s.startIndex
        var sum: Int = 0
        for rn in s {
            guard indexer < s.endIndex else { return sum }
            switch s[indexer] {
                case "I":
                    guard indexer < s.index(s.endIndex, offsetBy: -1) else {
                        sum += 1 
                        return sum 
                        }
                    if s[s.index(after: indexer)] == "V" {
                        sum += 4
                        indexer = s.index(indexer, offsetBy: 2)
                        
                    } else if s[s.index(after: indexer)] == "X" {
                        sum += 9
                        indexer = s.index(indexer, offsetBy: 2)
                    }
                    else {
                        sum += 1
                        indexer = s.index(after: indexer)
                    }
                case "V":
                    sum += 5
                    indexer = s.index(after: indexer)
                case "X": 
                    guard indexer < s.index(s.endIndex, offsetBy: -1) else {
                        sum += 10
                        return sum 
                        }
                    if s[s.index(after: indexer)] == "L" {
                        sum += 40
                        indexer = s.index(indexer, offsetBy: 2)
                    } else if s[s.index(after: indexer)] == "C" {
                        sum += 90
                        indexer = s.index(indexer, offsetBy: 2)
                    }
                    else {
                        sum += 10
                        indexer = s.index(after: indexer)
                    }
                case "L":
                    sum += 50
                    indexer = s.index(after: indexer)
                case "C":
                    guard indexer < s.index(s.endIndex, offsetBy: -1) else {
                        sum += 100
                        return sum 
                        }
                    if s[s.index(after: indexer)] == "D" {
                        sum += 400
                        indexer = s.index(indexer, offsetBy: 2)
                    } else if s[s.index(after: indexer)] == "M" {
                        sum += 900
                        indexer = s.index(indexer, offsetBy: 2)
                    }
                    else {
                        sum += 100
                        indexer = s.index(after: indexer)
                    }
                case "D": 
                    sum += 500
                    indexer = s.index(after: indexer)
                case "M": 
                    sum += 1000
                    indexer = s.index(after: indexer)
                default:
                    print("Unknown Symbol fount at . Check your input.")
            }
        }

        return sum
    }
```
HMU if you have any questions!
