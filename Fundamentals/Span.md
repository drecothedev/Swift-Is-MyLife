Span in Swift

Ciao!👋🏽 A span in Swift gives you access to a contigous. This gives read only access to the memory. 

```swift
func simlSpan<T>(_ items: [T]) {
    let span: Span<T> = items.span
    for i in 0...span.count - 1 {
        print(span[i])
    }
}

simlSpan(["Richard", "Dee", "James", "Jess"])
simlSpan([1,2,3,4,5,6])
var dataItems: [DataItem] = [DataItem(), DataItem(), DataItem()]
simlSpan(dataItems)
```

We shall see if i ever use this in the real world! 
