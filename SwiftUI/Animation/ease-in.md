ease in Swift/SwiftUI

Ciao! If you checked out my AnimationSummary post then you probably have a basic idea of what animations are in Swift. If not, Here is an introduction to one of the built in Swift animations. The ease-in animation will give your view a more organic animation when compared to some of the other built in animations. This is because the ease-in animation replicates most real life functions as it begins slow and speeds up towards the end. Almost like watching a car build speed and drive away. Lets check out an example: 

```swift
        VStack(alignment: isMoving ? .trailing : .leading) {
            Circle()
                .frame(width: 50)
                .foregroundStyle(isMoving ? Color.cyan : Color.yellow)
            Button("click to move ball") {
                withAnimation(.easeIn) {
                    isMoving.toggle()
                }
            }
        }
```
