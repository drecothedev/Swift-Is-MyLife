Animations in Swift/SwiftUI

Ciao! I really enjoy thinknig about the user's experience when using an app. I think animations are one of the coolest thing to have in your app for a number of reasons. First, it gives your views life. Animations can make it seem like your views have depth, meaning in life, a stressful 9-5, and hell even taxes and a 401k. Nah i'm jk, but seriously no 1ne wants a stale ahh experience. Second, animations can give a user that "awh" factor, and I'm all about that awh.

In Swift, animations are pretty simple to use right out of the box. They can be defined by-The way a view changes over time to create a smooth visual transition from one state to another. From this definition you can probably imagine that performing animations in SwiftUI involves a @State variable. If you are not yet familiar with @State please check out my @State discussion a couple of post over. Let's take a look at a simple example: 

```swift

struct RegularAnimationView: View {
    @State private var scale = 0.5 // State variable that is changing over time

    var body: some View {
        Circle()
            .scaleEffect(scale)
            .animation(.bouncy, value: scale) // Adding an animation to a view. We pass scale as the value to
                                              // track for changes. bouncy defines the type of animation we are doing. bouncy is a built in                                                     // animation SwiftUI offers amongs others.                                              
        
        HStack {
            Button("-") {
                scale -= 0.1 // Updating the State value for the animation 
                print(scale)
            }
            Button("+") {
                scale += 0.1 // Updating the State value for the animation 
                print(scale)
            }
        }
    }
}

// Inspired by: https://developer.apple.com/documentation/swiftui/animation

```

In this very simple example we are adding the modifier .animation and first passing in the animation we want, .bouncy in this case. Bouncy is a built in animation SwiftUI offers amongs others like: spring, easeinout, easein, etc. We then pass in the scale attribute for the value we are tracking the changes for. 

That is the first way to use animations. You can also use withAnimation: 

```swift
        @State private var showSecondAnimation = false  // defined before the body var of course. 
    
        VStack(alignment: showSecondAnimation ? .trailing : .leading) {
            Circle()
                .frame(width: 100)
                .foregroundStyle(Color.cyan)
            
            Button("Click me for second animation") {
                withAnimation(.secondAnimation(duration: 5.0)) {
                    showSecondAnimation.toggle()
                    print(showSecondAnimation)
                }
            }
        }

// Excerpt from some practice code I was working on.

```

In this snippet instead of using the view modifier we are using a method to call the animation. The actual animation is a custom one which we talk about later.

You can also perform animations on binding variables. Lets take a look at this one: 

```swift

VStack(alignment: isMoving ? .trailing : .leading) {
            Image(systemName: "box.truck")
                .resizable()
                .frame(width: 100, height: 100)
            
            Toggle("Move to trailing edge", isOn: $isMoving.animation(.linear)) // Automatically perform state changes with animations on binding                                                                                 // values                                                                                                                                                                          
        }

```

Pretty simple right. 

Let's summarize what we looked at today. We took a very high level look at using animations in SwiftUI. This is honestly enough to add animations in your own app. Of course you can go deeper into learning about the different types of animations: Timing curve, Spring, Higher Order. We will be doing this later. This post is meant to teach you how to ride the bike with training wheels for now. 
