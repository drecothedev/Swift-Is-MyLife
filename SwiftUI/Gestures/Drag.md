Drag Gesture Swift

Ciao! Today we will talk abit about the Drag Gesture in SwiftUI. I cannot lie, I think the Swift Documentation is a bit vague in explaining how to use the gesture so that's why I am here 🦸🏽 ! jk there is a lot of really good videos on youtube. The one that I watched before is : https://www.youtube.com/watch?v=esWsU8GSsB8 check it out he explains it very well. 

It is worth mentioning that drag gestures are pretty simple to get started with. You simply define variables to track the gesture ( isDragging: Bool , position: CGSize ). You technically don't need the position nor the isDragging but they are helpful to track the item being dragged. The third property you will need is titled drag. here is the definition: 

```swift

    var drag: some Gesture {
        DragGesture(minimumDistance: CGFloat(100))
            .onChanged { val in
                self.isDragging = true
                position = val.translation
                print(position)
    
            }
            .onEnded { _ in self.isDragging = false
                position = .zero
            }
    }

```

In this definition we are computing a property of type some Gesture. We then initialize a DragGesture instance with a minimumDistance ( sets the amount of dragging done before being recognized as a drag ). The .onChanged and .onEnded modifiers are the meat and potatoes of this definition. The .onChanged tracks the changes being made to the view ( being dragged ). You can then track the position of the view by checking the val.translation. 

Lets attach this to a view and see how it works: 

```swift

RoundedRectangle(cornerRadius: 10.0)
  .frame(width: 100, height:  100)
  .foregroundStyle(isDragging && position.width > 103.0 ? Color.green : Color.gray)
  .animation(.spring(), value: position)
  .offset(position)
  .gesture(drag)

```

Here is a rectangle we are able to drag around the screen. The important points concerning the DragGesture is the offset modifier and the gesture modifier. The offset controlls where the view is moved to. As a result we use our position var to track where the view should go. This way it follows your finger/ mouse on the screen. The second is the gesture modifier. This allows the view to listen for common gestures, in this we are using the same drag var we defined earlier.

The offset modifier and gesture modifier are the only ones you need to create the drag gesture, but there are of course many ways to interact with the gesture. In this code we are checking the position to change the color of the rectangle. So if the rectangle is dragged passed a certain point the rectangle will turn from gray to green. 

I hope this helps. I think everything in programming is deceptively difficult at first, but I hope this simplifies things for whenever you want to add this into your own code. 
