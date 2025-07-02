@Binding in Swift/SwiftUI

👋🏽 On to our 2nd Property Wrapper. The @Binding wrapper is another very common feature to use when builing UX. It is similiar to the @State wrapper but a bit different which I will explain in a second. @Binding still allows you to read and write to a variable, however instead of it being the source of truth, it is reporting back to the source of truth. This means that using @Binding is most useful when you are passing data through different views where you plan to make changes to that data. Here is an example: 

```swift
// BindingPracticeView.swift

import SwiftUI

struct BindingPracticeView: View {
    @State private var username: String = "Jeff"
    var body: some View {
        NavigationStack {
            NavigationLink(destination: ChangeUsernameView(username: $username)) {
                ZStack {
                    RoundedRectangle(cornerRadius: 10.0)
                        .foregroundStyle(Color.gray)
                        .frame(width: 200, height: 55)
                    TextField("username: ", text: $username)
                        
                }
            }
        }
    }
}

// ChangeUsernameView.Swift

struct ChangeUsernameView: View {
    @Binding var username: String
    var body: some View {
        NavigationStack {
            VStack {
                Text("Hello, \(username)!")
                Text("Change your username below")
                TextField("new username: ", text: $username)
            }
        }
    }
}

```
Take a look at these pics of the app for a reference, or copy and paste the code in your Xcode.  
<img width="335" alt="Phase1" src="https://github.com/user-attachments/assets/b0fb47ad-cc0d-455e-b53c-0cae50f5cfe2" />

<img width="340" alt="Phase2" src="https://github.com/user-attachments/assets/e82d7d8d-9dfb-4c79-a630-2b1ba4cb2438" />

<img width="384" alt="Phase3" src="https://github.com/user-attachments/assets/1256a222-d243-42ee-bdbf-b8818edcf73f" />

<img width="384" alt="Phase4" src="https://github.com/user-attachments/assets/8891a3a1-177c-400e-aa30-1d9e182ed0d2" />

Notice how the @State username var is the source of truth. This means that all changes that are made to the value in its subviews will be reflected. Notice that we still need to pass the binding with $ into the child view because we are making changes. 

So in summary, the most important takeaway is that @State owns the value while @Binding gives us a reference to that source of truth. 
