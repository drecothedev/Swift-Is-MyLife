Transitions in SwiftUI

Ciao! Does anybody truly love change? I mean it is scary, bewildering, and could be a bit jarring as Apple would put it. So when our user gets an update on their view, it is important not to scare them. Transitions give us a really neat and frankly easy way to perfrom this in our code. Here is an example straight from Apple Developer that I mocked up: 

```swift
struct Twirl: Transition {
    func body(content: Content, phase: TransitionPhase) -> some View {
        // The view you are passing in; the view being shown to the user.
        
        // You track the phase of the view ( being added, being disappeared, etc.),
        // based on the phase you can add effects to the view.
        content
            .scaleEffect(phase.isIdentity ? 1.0 : 0.5)
            .opacity(phase.isIdentity ? 1 : 0)
            .blur(radius: phase.isIdentity ? 0 : 10)
            .rotationEffect(
                .degrees(
                    phase == .willAppear ? 360 :
                        phase == .didDisappear ? -360 : .zero
                )
            )
    }

    // https://developer.apple.com
}
```

Let's break down this code a bit. We are creating a new transition. To do that we need to conform to the Transition protocol. This means we need to a adapt the correct methods, variables, etc. One of those requirements for a transitiion is to have a function called body. In that body function you must pass the content ( the view ) and a phase. In our function we are just effecting our view based on the current state of the view.

Here is the SwiftUI code that ultimately shows this view: 
```swift
struct TransitionsView: View {
    @State private var showPhoto: Bool = false // Tracks showing the photo or not
    var body: some View {
        if showPhoto {
            Image(systemName: "figure.walk.circle")
                .resizable()
                .transition(Twirl()) // pass the Transition into the transition modifier
                .frame(width: 100, height: 100)
                
        }
        
        Button("Click to toggle photo") {
            withAnimation(.easeInOut) {
                showPhoto.toggle()
            }
        }
    }
}
```

https://github.com/user-attachments/assets/252c0006-7abb-4dc6-bf03-0b2382390f5a

Similiary here is a transition that rolls the view into fram across the x axis: 

```swift
struct SlideIn: Transition {
    func body(content: Content, phase: TransitionPhase) -> some View {
        content
            .scaleEffect(phase.isIdentity ? 1.0 : 0.5)
            .rotationEffect(
                .degrees(
                    phase == .willAppear ? 360 :
                        phase == .didDisappear ? 360 : -360
                )
            )
            .offset(phase.isIdentity ? CGSize(width: 0, height: 0) : CGSize(width: -200, height: 0))
            .opacity(phase.isIdentity ? 1.0 : 0.0)
    }
}
```

https://github.com/user-attachments/assets/6c501978-3b0f-4558-9478-a1d76a96e72a

This smooth transition might startle your user with swag but it will be pleasent. jk. But in this code we are honestly performing a similiar task. We are tracking the phase of the transition and making changes to the view during those phases. Pretty simple right. 



