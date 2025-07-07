LongPressGesure Swift 

Ciao! have you ever wanted to press down on a button and hold your finger there just long enough to see a reaction from the UI? I bet you have, me 2. In a tiny practice project I am creating I wanted to implement a feature that would involve some long pressing action. I was a bit schocked to see how simple it was. Without code I would explain it by saying you can add it as a modifier to a view very easily. You will just need to initialize the modifier with a minium duration ( how long they need to hold down the view to get a reaction ) and maximum distance ( The maximum distance that the fingers or cursor performing the long press can move before the gesture fails ). Pretty simple right 🤷🏾‍♂️. Here is a simple example that I just used for practice: 

```swift

struct LongPressGestureView: View {

    @State private var currentColor: Color = Color.gray // Default Color for Rectangle
    @State private var startTimer: Bool = false // Timer will start when long press gesture is identified
    @State private var index = 0 // Will track the color
    
    let colors: [Color] = [Color.black, Color.pink, Color.blue, Color.green, Color.cyan, Color.purple, Color.white]
    let timer = Timer.publish(every: 1.5, on: .main, in: .common).autoconnect() // SwiftUI Timer
    
    var body: some View {
        
        RoundedRectangle(cornerRadius: 10.0)
            .frame(width: 100, height: 100)
            .foregroundStyle(colors[index])
            .onLongPressGesture(minimumDuration: 0.5, maximumDistance: 50) {
                startTimer = true
            } onPressingChanged: { startTimer in
                self.startTimer = startTimer
            }
            .onReceive(timer) { _ in // Handles logic for everytime timer is published
                if startTimer && index < colors.count - 1 {
                    index += 1
                } else {
                    index = 0
                }
            }
    }
}

```

In this code, we’re not directly using the longPressGesture to change the color. Instead, we use it to start a timer, which then updates the color every 1.5 seconds. The onPressingChanged closure tracks the press state in real time and updates the startTimer flag accordingly, this is what lets the timer know when to start or stop updating the colors.

Welp, that is about it for the longPressGesture. Give it a try and lmk! 
