Ciao!👋🏽
Here a queue in swift. This is useful for ensuring events happen in a FIFO order.

```swift
struct Queue<Item> {
    var queue: [Item]
    
    // head
    var head: Item {
        guard !queue.isEmpty else { fatalError("queue is empty. add items.")}
        guard let firstItem = queue.first else { fatalError() }
        return firstItem
    }

    // tail
    var tail: Item {
      guard !queue.isEmpty else { fatalError("queue is empty. add items.")} 
      guard let lastItem = queue.last else { fatalError()}
      return lastItem
    }

    // enqeue
    mutating func enqueue(_ item: Item) {
      queue.append(item) 
    }
    // dequeue
    mutating func dequeue() -> Item {
      guard !queue.isEmpty else { fatalError("queue is empty. add items.")} 
      guard let removed = queue.last else { fatalError("no remaining items") } 

      return queue.removeFirst()
    }
}
```
