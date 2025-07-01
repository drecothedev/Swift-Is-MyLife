@State Property Wrapper Swift 🇺🇸

The @State property is probably the most common of the built in property wrappers so I am guessing you've used it before. If you haven't the basic description is: A property wrapper type that can read and write a value managed by SwiftUI. This means that you can make changes/updates to the values when defined with the @State wrapper. Here is an example of using a property wrapper and not using it and what it does to your code. 

```swift

import SwiftUI

struct MyView: View {
    @State private var username: String = "" // Create the state.
    var body: some View {
        VStack {
            TextField("username: ",text: $username) // Writing to a value using a TextField
            Button(action: {
                username = "dog" // Writing to a file by updating the value by assignment 
            }, label: {
                Text("Turn username to dog")
            })
            Text(username) // Reading from the Value
        }
    }
}

// WITHOUT @State
/*
There is no running code for an example without @State. In SwfitUI You cannot write to or change variables in the body that are not defined with @State. 
*/

```

Before taking a deeper dive 🦈 into State I do want to clarify what $username is in the above code. The '$' lets Swift know that you are writing to a value. 

You should use State when you want to share data from the Top level to different Subviews. This is important when you want one source of truth. This is why you should define State variables as Private so there isn't any access to them in other views. If you wanted to change the value in subviews then you would use @Binding instead. 


Another use case is using @State when storing @Observable objects. State allows you pass around and access the data points in the Object. It is important to mention that everytime SwiftUI builds your view the Default values will be intialized so deferring that initialization is often prefferd. Check these examples from the Swift Documentation:

```swift

@Observable
class Library {
    var name = "My library of books"
    // ...
}


struct ContentView: View {
    @State private var library = Library()


    var body: some View {
        LibraryView(library: library)
    }
}

// Example with Defferal

struct ContentView: View {
    @State private var library: Library?


    var body: some View {
        LibraryView(library: library)
            .task {
                library = Library()
            }
    }
}

```

In this code you can see how @State gives us access to the object but you can also see how to lower the expense of accessing each object needed by deffering it in the second example. This just ensures that unnecessary allocations of the object doesn’t happen each time SwiftUI initializes the view.

As I mentioned earlier you can also update values within the object: 

```swift

@Observable
class Animal {
    var name: String = "Bufford"
    var isOwned: Bool = false
}

struct ContentView: View {
    @State private var animal: Animal = Animal()
    var body: some View {
        VStack {
            Text("\(animal.name)")
            Button(action: {
                animal.isOwned.toggle() // Accessing the current instance and updating values 
            }, label: {
                ZStack {
                    RoundedRectangle(cornerRadius: 10.0)
                        .frame(width: 200, height: 55)
                        .foregroundStyle(animal.isOwned ? Color.green : Color.red)
                    Text(animal.isOwned ? "Animal is Owned Already" : "Animal is not Owned yet") 
                        .foregroundStyle(Color.white)
                }
            })
        }
        .padding()
    }
}

```

B4 finishing off, even though the above example shows us using State with a reference type, I don't tend to use State with it in real application. Instead I would StateObject. I saw this in the Swift Documentation and was curious to see if it acually worked, and of course it does. 

And there it is. I hope this helps. Learning enough just to share this has helped me tremendously. I've used @State pretty commonly in my Apps but never took the time to check under the hood. I can say that I am happy I did. 🙇🏽‍♂️
















