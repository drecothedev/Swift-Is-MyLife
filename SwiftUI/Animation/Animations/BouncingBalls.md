Ciao! 👋🏽

As mentioned in my previous post, I have been increasingly interested in animations and bringing the UX to life. Everyone hates loading screens, including me. This animation is meant to be at least be satisfying and beautiful, while the user is waiting for whatever is coming next. I don't think it is perfect yet, mostly because I haven't used the naimation in a real app, but I think it is a great start. Here is the code: ( I will break it down soon ): 

```swift
// Main View
struct BouncingButtonView: View {
    @State private var isBouncing: Bool = true
    @State private var isDoneLoading: Bool = false
    
    let sampleLoadingTimer = Timer.publish(every: 3.0, on: .main, in: .common).autoconnect()
    
    
    
    let fullDuration = 2.0
    
    var body: some View {
        VStack(alignment: isDoneLoading ? .trailing : .leading) {
            HStack {
                if isDoneLoading {
                    BouncingCircle(color: Color.pink.opacity(0.5), repeats: false)
                    BouncingCircle2(color: Color.green.opacity(0.09), repeats: false)
                    BouncingCircle3(color: Color.cyan, repeats: false)
                    
                } else {
                    BouncingCircle(color: Color.pink.opacity(0.5))
                    BouncingCircle2(color: Color.green.opacity(0.09))
                    BouncingCircle3(color: Color.cyan)
                }
            }
            .onReceive(sampleLoadingTimer) { val in
                self.isDoneLoading.toggle()
            }
        }
    }
}
```
In our main view, we are simply using a sample timer to act as a trigger for when the animation starts and stops. In real practice you may want to replace this timer with triggers that update when the task is completed. Most importantly, here is our BouncingBalls definition: 

```swift
struct BouncingCircle: View {
    var diameter: CGFloat = 50
    var color: Color = .accentColor
    var duration: Double = 1.0
    var repeats: Bool = true
    
    var body: some View {
        Circle()
            .fill(color)
            .frame(width: diameter, height: diameter)
            .keyframeAnimator(initialValue: BouncingAnimationProperties(), repeating: repeats) { content, value in
                content
                    .scaleEffect(y: value.verticalStretch, anchor: .bottom)
                    .offset(y: value.yTranslation)
            } keyframes: { _ in
                // Stretch / squish track
                KeyframeTrack(\.verticalStretch) {
                    SpringKeyframe(0.7, duration: duration * 0.3)
                    CubicKeyframe(1.0, duration: duration * 0.4)
                    SpringKeyframe(1.0, duration: duration * 0.3)
                    
                }
                // Up‑and‑down track
                KeyframeTrack(\.yTranslation) {
                    CubicKeyframe(-100, duration: duration * 0.5)
                    CubicKeyframe(0, duration: duration * 0.5)
                }
            }
    }
}

// Initial Values for each Ball
struct BouncingAnimationProperties {
    var yTranslation = 0.0
    var verticalStretch = 1.0
    var xTranslation = 0.0
}
```

In this code we are defining just one of our bouncing balls. I did decide to individualize each ball so if there is a better way please let me know. We first define the properties of our circle including size and color, and then we define some properties for our animation, including the duration of the animation ( which changes for each ball ) and we ensure to track whether or not the animation repeats, because after the loading is done we don't want the animation to repeat. The meat and potatoes of this view is the animation attached to it. We use the keyFrameAnimator' to track key frames within the animation. We use our init values for the properties we plan on changing. We then use a KeyFrameTrack to track/change each property that is needed to be changed, specifically the vertical stretch ( or how much the circl is stretchec on the y axis. This adds a bouncy/squishy effect to the circle itself, making it look a little more realistic and alive ). Secondly, we want to animate the location of the ball on the y axis using the yTranslation. One thing to note is that you want the duration of all of the animations to match the fullDuration so that it loops perfect. We use the Spring key frame for the stretching of the ball becasue this keyframe type simulates the physics of a spring. It interpolates to the target value with a bouncy, oscillating effect, eventually settling at the final value. The animation works very well for 3 seconds but gets a little out of order after that, so I am still working to improve that. Here is a gif showing it in action: 


![ScreenRecording2025-08-27at10 51 17AM-ezgif com-video-to-gif-converter](https://github.com/user-attachments/assets/b673ca66-8828-499b-a9ed-2c86f9d9c9b8)


