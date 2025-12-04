Using Sin and Time to create Animations 

Ciao! 👋🏽 Creating a beautiful and intuitive interface often involves animations. This helps keep our users from feeling jarred by things appearing or leaving the screen. Animations can also bring a sense of taste and unecessary beauty to your app. There are many different ways to animate when building apps with Swift. The most common, and one we covered before, is using the .withAnimation modifier that allows us to perfrom very simple animations that Apple has already supplied for us. You can also create animations using a keyFrameTracker which allows us to do even more with our animations. Another way, and the way will be trying today is through Shaders, specifically using Sine or 'sin' to create simple animations. 

Before we get into any code it is a bit important to understand why we are going to be using Sine functions to help u with our animations. Before we get into the function itself lets look at a sine wave. 

![SineWave](https://github.com/user-attachments/assets/28d624ae-33b1-4f5e-9bda-2c8d156465d3)

As we can see here it is a wave that oscilates up and down very smoothly. A sine wave with no added amplitude simply oscilates between -1 and 1. This is great for our animations because it allows us to smoothly bounce between different states ( colors, or distortions, or whatever is being affected ). So when we use a sine function in our code it not only helps us bounce between states but it also normalizes the value between -1 and 1. Our program can only account for values between 0 and 1 but gives us a simliar effect. Lets take a look at this code example. It should be similar to the examples we created in my "CreatingAGradient" post a little bit back. We again are taking the distance of our pixel in comparison to our origin and using time to track progression through our animation. We are passing that time in as a paremeter. 

```swift
[[ stitchable ]] half4 usingSinAndTimeToCreateAnimations(float2 pos, half4 color, float2 size, float time) {
    // Normalize values 0.0 - 1.0
    float2 uv = float2(pos.x / size.x, 1.0 - pos.y / size.y);
    float y = length(uv) + time;
    half3 newColor = half3(y);
    
    return half4(newColor,1.0);
}
```

You can use the same view as in our previous post but you want to add a time var to pass in as a paremeter for our color effect

```swift
// Call this in your SwiftUI 
.colorEffect(
  ShaderLibrary.usingSinAndTimeToCreateAnimations(
  .float2(geo.size.width,
   geo.size.height),
  .float(time)

    )
  )
```

Go ahead and try to run that. It should look like a beautiful animation. SIKE! it shouldn't. it should be a beautiful animation running away from you. This is becasue our time var is constantly increasing exponentially. This pushes our color effect off of the screen. This is a sign that we should use our Sine function to go from our upper bound ( the color being pushed off the screen ) to our lower Bound ( more towards the origin ) smoothly. 

Lets add sin(time) to our code to see how the animation can smoothly oscilate back and forth. 

```swift
[[ stitchable ]] half4 usingSinAndTimeToCreateAnimations(float2 pos, half4 color, float2 size, float time) {
    // Normalize values 0.0 - 1.0
    float2 uv = float2(pos.x / size.x, 1.0 - pos.y / size.y);
    // Add time sin(time) to smoothly oscilate between our lower and upper bound
    float y = length(uv) + sin(time);
    half3 newColor = half3(y - 0.9, y - 0.1, y - 0.1);
    
    return half4(newColor,1.0);
}
```

Now run that and see how the animation doesn't run off the screen like our previous example. This is what makes Sine so useful. Take a look at this animation i created to simulate a sunrise/sunset. 

```swift
// Creates an oscilating gradient representing a sunset. Great for dark mode. 
[[ stitchable ]] half4 williamTurnerSunset2(float2 pos, half4 color, float2 size, float time) {
    half3 colorA = half3(0.149,0.141,0.912); // Royal Blue
    half3 colorB = half3(1.000,0.833,0.224); // Yellow
    
    float2 st = float2(pos.x / size.x, 1.0 - pos.y / size.y); // Normalizing value to 0.0 - 1.0
    
    half3 pct = half3(st.x); 
    half3 newColor = half3(0.0);
    
    pct.r = smoothstep(0.0,1.0, st.x * HALF_PI) + sin(time / 2) / 2; // Creates a serbert orange nice color.
    pct.g = sin(st.x * HALF_PI) + sin(time / 2) / 2;
    pct.b = asin(st.x * HALF_PI) + sin(time / 2) / 2;
    
    newColor = mix(colorA, colorB, pct);
    
    return half4(newColor, 1.0);
}
```

![ScreenRecording2025-12-03at5 00 40PM-ezgif com-optimize](https://github.com/user-attachments/assets/5498cf2f-8bcb-4cb2-90a1-863a475b1c27)


Try to disect this code to see how it works. i cannot lie, this was a product of much trial and error and not theoretical application. There is also a starter code provided in the https://thebookofshaders.com. 


