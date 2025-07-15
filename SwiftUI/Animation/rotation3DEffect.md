rotation3DEffect Swift/SwiftUI

Ciao! This will be a short explanation because the usage is pretty straightforward. When designing your UI it is common that you will want views to flip or rotate. In my case, I thought it would be a really cool idea to create an app taht helps you study by flipping over cards, similiar to how quizlet works. At first I was confused on how to animate each step of flipping a card. After trying to draw it out and realizing that the process would take years I remembered I could just use the .rotation3DEffect view modifier. Here is my implementation: 

```swift
struct CardFlip: View {
    @State private var isFlipped = false
    @State private var degrees = Double.zero
    var body: some View {
        Card(isFlipped: $isFlipped, frontCardText: "Front of card", backCardText: "Back of Card")
            .rotation3DEffect(.degrees(degrees), axis: (x: 1, y: 0, z: 0))
        Button("Flip Card") {
            isFlipped.toggle()
            withAnimation {
                degrees = (degrees == .zero) ? 360 : .zero
            }
        }
    }
}

// Card View

struct Card: View {
    @Binding var isFlipped: Bool
    let frontCardText: String
    let backCardText: String
    var body: some View {
        ZStack {
            RoundedRectangle(cornerRadius: 25.0)
                .frame(width: 200, height: 100)
                .foregroundStyle(Color.white)
                .shadow(radius: 5.0)
            Text(isFlipped ? backCardText : frontCardText)
                .foregroundStyle(Color.black)
        }
    }
}

```

In this code we are using the rotation modifier to flip our card over the horizontal plane ( x ) and then updating the text on the card. 
