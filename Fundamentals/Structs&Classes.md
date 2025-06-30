# 🧱 Understanding Structs and Classes in Swift

Structs are an essential building block for building Swift apps. Swift prefers structs over classes because of their **cleanliness**, **efficiency**, and **predictable behavior**. Here are a few things to understand when using structs:

- 🖊️ Define properties to store values  
- 🧠 Define methods to provide functionality  
- 👀 Define subscripts to access values using subscript syntax  
- 🎬 Define initializers to set up their initial state  
- ➕ Extend them to expand functionality  
- 🗺️ Conform to protocols to gain standardized behavior  

---

## 🧩 Example: Modeling App Data with Structs

Structs are commonly used to model data. Here's an example where we define a `Table` for use in a SwiftUI app:

```swift
struct Table: Identifiable {
    var id = UUID()
    var name: String
    var status: String 
    var location: String
    var products: [Product]
    var productSets: [Product]
    var pins: [Pin]
    
    init(id: UUID = UUID(), name: String, status: String, location: String, products: [Product], productSets: [Product], pins: [Pin]) {
        self.id = id
        self.name = name
        self.status = status
        self.location = location
        self.products = products
        self.productSets = productSets
        self.pins = pins
    }
}

extension Table {
    static let sample = Table(
        name: "iPad Comparison",
        status: "Confirmed",
        location: "A2",
        products: Product.sampleProducts,
        productSets: [],
        pins: []
    )
}


In this example we are setting parameters for what each Table should have. We then write in our initializer, very similar to classes. Lastly, we are adding an extension to our Table that just allows us to use a global sample for testing in our app. 


Structs are also amazing because they can have their own version of inheritence ( Commonly used with OOP and Class to adapt traits of other classes ). Structs do this by conforming to Protocols. Protocols are similiar to inheritence because they allow 
you to replicate behaviours from other sources ( enums, structs, classes ). Contrary to inheritance, is that you can have one struct confrom to multiple protocols. 

In our example above, our tables are conforming to the Identifiable Protocal. The Identifiable protocol allows for each table to be sliced when using in SwiftUI. Whenevever a Struct conforms to a protocol it must meet the requirements by using the functions/ variables 
in the protoocal. For Identifiable, the Struct just needs variable named "id". 

What about Classes??!!!

While classes and structs look similar, they behave differently under the hood:

✅ Structs are value types (copied when passed).
🚫 Classes are reference types (shared state, potential bugs).
⚡️ Structs live on the stack (faster).
🐢 Classes live on the heap (slower).

Use classes only when you need shared state or identity.

```swift
class UserDataService: ObservableObject {
    static let shared = UserDataService()
    
    func getUsers() {
        let url = URL(string: "http://127.0.0.1:5000/users")!
        
        let task = URLSession.shared.dataTask(with: url) { data, _, error in
            if let error = error {
                print(error)
                return
            }
            if let data = data {
                do {
                    let decoder = JSONDecoder()
                    let product = try decoder.decode(UserResponse.self, from: data)
                    for user in product.users {
                        print(user.displayName)
                    }
                } catch {
                    print(error)
                }
            }
        }
        task.resume()
    }
}
```

In this example we are using a class to access my database becasue this same instance will be used across many parts of my app. 


In summary, 
Use structs for data modeling, view models, and most logic in Swift apps.
Use protocols to share behavior and build flexible, composable types.
Use classes only when shared mutable state or identity is essential.


Thank you for reading !






