Drawing Shapes in Swift 

Ciao! As the title implies we will be learning about drawing shapes using SwiftUI. As I dive deeper into creating custom animations I run into the issue creating shapes that fit my needs just perfect. The solution was/ is to learn how to create custom shapes. I think drawing shapes is pretty complex and it is taking me some time to understand. The first part that is important to understand is that shapes are drawn using a path. A path is the outline of a 2D shape. Th original shape or outline being provided is a rounded rectangle. This means that everyting you draw either involves the perimeter or the area of the rounded rectangle. Here is a visual: 

<img width="354" height="696" alt="PathPracticeDemoPhoto" src="https://github.com/user-attachments/assets/77154c59-3f58-48cc-a1ff-e886c62b79ae" />


From this you can see how we can basically draw shapes using the perimeter parameters. To use a path you should first initialize an empty path and then add lines to it. Here is how that triangle was built. 

```swift

struct MyOwnTriangle: Shape { //  Conforms to Shape for reusability
    
    // Handles returning the path we are creating
    // Note that the base rect is being passed into the function. This gives us access to the perimiters measurments.
    func path(in rect: CGRect) -> Path {
        var path = Path() // Initialize an empty path
        
        path.move(to: CGPoint(x: rect.midX, y: rect.minY)) // Where we start drawing
        path.addLine(to: CGPoint(x: rect.minX, y: rect.maxY)) // Adds a line to the directed points
        path.addLine(to: CGPoint(x: rect.maxX, y: rect.maxY))
        path.addLine(to: CGPoint(x: rect.midX, y: rect.minY))
        
        return path
    }
}

```

For this Triangle we made it conform to Shape so that it inherits the same behaviour as native shapes within SwiftUI. Shape requires the 'path' function we declared in the body of our structure. The path function handles builing the path for our shape and then returning it out. We first initialize an empty path that we end up adding lines to. One of the most confusing things to me was how exactly the triangle is being built. We start by using the 'path.move' to start our line drawing. One very important note is that the coordinate plane in Swift is flipped. So that means that the lower y is, the higher the point is. This is because Swift starts its plane (0.0) in the top left corner. I am guessing this helps with rendering graphics because graphics are usually rendered from top to bottom, left to right ( diagonally ). That tripped me up a lot at the beginning. But now that you are aware of that you could now see how when we are using 'path.addLine', we are adding a line that draws to the bottom left corner of the original rect shape. With our next line we are drawing to the bottom right hand corner, and since are pen is already at maxY ( the bottom ) this is where we are creating the bottom line of the triangle. Laslty, we draw the last side of the triangle by moving our pen ( drawing a line ) back up to our starting point. 

Here is a custom Square to take a look at as well: 

```swift

struct Square: Shape {
    func path(in rect: CGRect) -> Path {
        
        var path = Path()
        
        path.move(to: CGPoint(x: rect.minX, y: rect.maxY)) // Bottom left hand corner
        path.addLine(to: CGPoint(x: rect.maxX, y: rect.maxY)) // Bottom right hand corner
        path.addLine(to: CGPoint(x: rect.maxX, y: rect.minY)) // Upper right hand corner
        path.addLine(to: CGPoint(x: rect.minX, y: rect.minY)) // Upper left hand corner
        path.addLine(to: CGPoint(x: rect.minX, y: rect.maxY)) // Bottom left hand corner

        return path
    }
}

```

Here is some "real world" application with custom shapes: 

```swift
// Arc Shape 
struct Arc: Shape {
    let startAngle: Angle
    let endAngle: Angle
    let clockwise: Bool
    var rotationAdjustment: Angle
    
    func path(in rect: CGRect) -> Path {
        let modifiedStart = startAngle - rotationAdjustment
        let modifiedEnd = endAngle - rotationAdjustment
        
        var path = Path()
        
        path.addArc(center: CGPoint(x: rect.midX, y: rect.midY), radius: rect.width / 2, startAngle: modifiedStart, endAngle: modifiedEnd, clockwise: !clockwise)
        
        return path
    }
}

// Implementation/Animation

struct LetsPracticeSomeMoreDrawing: View {
    @State private var outerRotationAmt: Angle = .degrees(90)
    @State private var innerRotationAmt: Angle = .degrees(90)
    @State private var innestRotationAmt: Angle = .degrees(90)
    
    let timer = Timer.publish(every: 0.1, on: .main, in: .common).autoconnect()
    var body: some View {
        VStack {
            ZStack {
                Arc(startAngle: .degrees(-90), endAngle: .degrees(90), clockwise: false, rotationAdjustment: outerRotationAmt )
                    .stroke(.cyan, style: StrokeStyle(lineWidth: 5, lineCap: .round))
                    .frame(width: 50, height: 50)
                    .animation(.easeIn, value: outerRotationAmt)
                    .onReceive(timer) { _ in
                        outerRotationAmt -= .degrees(30)
                    }
                    
                
                Arc(startAngle: .degrees(-90), endAngle: .degrees(90), clockwise: false, rotationAdjustment: innerRotationAmt )
                    .stroke(.green, style: StrokeStyle(lineWidth: 5, lineCap: .round))
                    .frame(width: 25, height: 25)
                    .animation(.easeIn, value: innerRotationAmt)
                    .onReceive(timer) { _ in
                        innerRotationAmt -= .degrees(20)
                    }
                    .padding()
                
                Arc(startAngle: .degrees(-90), endAngle: .degrees(90), clockwise: false, rotationAdjustment: innestRotationAmt )
                    .stroke(.yellow, style: StrokeStyle(lineWidth: 5, lineCap: .round))
                    .frame(width: 12.5, height: 12.5)
                    .animation(.easeIn, value: innestRotationAmt)
                    .onReceive(timer) { _ in
                        innestRotationAmt += .degrees(10)
                    }
                    .padding()
                
            }
        }
    }
}

```

![CustomShapeAnimationPractice](https://github.com/user-attachments/assets/f1c35299-fc49-43c9-8537-1b2fe11ff836)

Thanks to Hacking with Swift for helping me learn this. Here is a link to his introduction video: https://youtu.be/FnwI1I5-8cE?si=ic4kzjY0E_rdpn-I

