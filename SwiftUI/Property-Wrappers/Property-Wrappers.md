Property Wrappers Swift 🫣

Ciao, We are going to just give a brief overview on what Property Wrappers are and then add the specifics in after. Property Wrappers are ways to add a logic/ behavior to a value. It is one of those features that you use everyday ( when using Swift ) in your apps. These are @State, @Binding, @ObservableObject, etc. Throughout this folder you will see some of those defined and exemplified. For now lets try to create our own custom Property Wrapper. 

```swift
struct ContentView: View {
    
    @Capitalized private var name = "riley"
    
    var body: some View {
        VStack {
            Text(name)
        }
    }
}

@propertyWrapper struct Capitalized {
    var wrappedValue: String {
        didSet { wrappedValue = wrappedValue.capitalized }
    }
    
    init(wrappedValue: String) {
        self.wrappedValue = wrappedValue.capitalized
    }
}

// INSPIRED BY https://www.swiftbysundell.com/articles/property-wrappers-in-swift/ Thank you 
```

This code should look a bit familiar. The top part 'ContentView' is a default Swift view. This is when property wrappers seemed to be used the most. Additionally, they are frequently used in classes for updates. If you look below our view declaration you will see the construction of our property wrapper. It is a very simple property wrapper that capitlizes the string attached to it. This is therefore adding behaviour/ logic to the value. This is a very simple example that I barely grasp, so i will explore other built in property wrappers before trying to create a really in detail example one. 

Hopefully from that it is a little bit easier to understand property wrappers, and at least the purpose of them. Now we are going to look at what is going on under the hood in other built in property wrappers. 🤝

