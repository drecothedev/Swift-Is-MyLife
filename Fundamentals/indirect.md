The indirect keyword in Swift

Ciao!👋🏽 i have began to build jess and in doing so i have come to the topic of recurssion with enums. I therefore, have become a bit familiar with the indirect keyword. this keyword allows us give enums access to itsself. By default enums are fixed by compiletime so accessing a reference to itself would be impossible, but indirect gives us access to its own refernece. This can be handy when using linked list, trees, etc. 

```swift
indirect enum List {
    case end
    case node(Int, next: List)
}

let list = List.node(1, next: .node(2, next: .node(3, next: .end)))
```

