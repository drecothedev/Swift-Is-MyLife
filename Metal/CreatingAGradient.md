Creating a gradient using Metal!

Ciao!👋🏽 Being able to effect every pixel on the screen feels so powerful. There is so much you can do to make interesting colors, gradients, animations, textures, etc. One beautiful example mentioned was gradients. Gradients look so nice and are used everywhere. For example, Apple's new Siri design uses an animating gradient effect to show its active. We can do similar things with our code. Let's look at a simple gradient effect: 

```swift
[[ stitchable ]] half4 swiftIsMyLifeGradient(float2 pos, half4 color, float2 size) {
    // Normalizes the cooridinates position so the range is between 0.0-1.0
    // This allows us to track each pixel relative to the size of the frame. 
    float2 st = float2(pos.x / size.x, 1.0 - pos.y / size.y);
    return half4(st.x, st.x, st.x, 1.0);
}
```

We then update our SwiftUI code to look like this: 

```swift
struct SwiftIsMyLifeView: View {
    var body: some View {
        GeometryReader { geo in
            RoundedRectangle(cornerRadius: 0.0)
                .frame(width: 1000, height: 100)
                .colorEffect(
                    ShaderLibrary.swiftIsMyLifeGradient(
                        .float2(geo.size.width,
                                geo.size.height)
                    )
                )
        }
            
    }
}
```

With this code we are standardizing the position of the pixel. This makes it relatable and comparable to the size of the frame we are working with. This is why we pass in 'size'. This allows us to compare the position of the pixel to that of the space being passed in. If you copy and paste this code into the editor you will see how you a get a black to white gradient among the horizontal axis. It is important to ask ourselves what is happening. 

The pixel's x value ( value representing its point on the x-axis ) is being observed to see how much color we should add to the pixel. As we get further along the x axis we notice the color starts to turn white. This is because the pixels x value is higher the further you go, resulting in our RGB values being closer to 1.0. 

Similarily you can make a gradient across the y axis like this: 

```swift
[[ stitchable ]] half4 swiftIsMyLifeGradient(float2 pos, half4 color, float2 size) {
    // Normalizes the cooridinates position so the range is between 0.0-1.0
    // This allows us to track each pixel relative to the size of the frame. 
    float2 st = float2(pos.x / size.x, 1.0 - pos.y / size.y);
    return half4(st.y, st.y, st.y, 1.0);
}
```

This is a very black and white way to create a gradient but there are a ton more. I implore you to try to add and subract from the final color variable ( just rememebr that the range is 0.0-1.0 ). This should add a bit of color to your gradient. Let's look at some more complex gradients: 

```swift
[[ stitchable ]] half4 swiftIsMyLifeGradient(float2 pos, half4 color, float2 size) {
    // Normalizes the cooridinates position so the range is between 0.0-1.0
    // This allows us to track each pixel relative to the size of the frame. 
    float2 st = float2(pos.x / size.x, 1.0 - pos.y / size.y);
    float y = length(st);
    return half4(y - 0.232, y - 0.533, y - 0.222, 1.0);
}
```

In this code we change the amount of color being added to pixels based off the distance of the pixel in relation to its origin, which is the bottom left of the screen. 

Take a look at these two different mathematical functions that are used a lot for blending colors.

```swift
// Step function that creates completely seperates colors from eachother
[[ stitchable ]] half4 swiftIsMyLifeGradient(float2 pos, half4 color, float2 size) {
    // Normalizes the cooridinates position so the range is between 0.0-1.0
    // This allows us to track each pixel relative to the size of the frame. 
    float2 st = float2(pos.x / size.x, 1.0 - pos.y / size.y);
    // we pass in a bound. If our x + y pos is less than 0.5 we get black or 0 and 1 if our value is greater than 0.5.
    // this is a more binary way to seperate colors. 
    float y = step(0.5, st.x + st.y); 
    return half4(y - 0.232, y - 0.533, y - 0.222, 1.0);
}
```

```swift
// Smooth Step function that blurs the middle of the gradient but is more opaque on each side
[[ stitchable ]] half4 swiftIsMyLifeGradient(float2 pos, half4 color, float2 size) {
    // Normalizes the cooridinates position so the range is between 0.0-1.0
    // This allows us to track each pixel relative to the size of the frame. 
    float2 st = float2(pos.x / size.x, 1.0 - pos.y / size.y);
    // We place a lower bound (0.0) and upper bound (1.0) and check our x + y.
    // The function returns a float in between 0.0 - 1.0 givings a more gradual transition between bounds. 
    float y = smoothstep(0.0, 1.0, st.x + st.y);
    return half4(y - 0.232, y - 0.533, y - 0.222, 1.0);
}
```

These two functions show how performing math based on matrices can create beautiful blending between colors. Lets look at one more that is a bit more complex but has more colors. 

This one does get a little crazy in my opinion but that is because of the heavy math implementation. Before getting into the actual code there is a new term to look over real quick. That is HSB. So previously we have been using RGB to tell our computer which color to show. Another way to show colors is with HSB. HSB stands for Hue, Saturation, and Brightness. The Hue is the underlying color ( red, green, cyan ). Saturation controls the intensity of the color. And Brightness controls how bright the color is being preseneted. As i mentioned earlier there is some heavy math involved but i tried to leave comments explaining what each function does individually, but conceptually i am probably just as lost as you. 

The equation was supplied from: Function from Iñigo Quiles https://www.shadertoy.com/view/MsS3Wc so be sure to check that out but it is in GLSL instead of Metal. I haven't seen many Metal implementations. Here is the Metal code: 

```swift
float3 hsb2rgb2(float3 c) {
    // clamp function:
    /*
     this means restricting a value to a specified range between a minimum and maximum value.
     in this function we are saying abs(fmod(...)) is our value to check for 0 is our min and 1.0 is our max.
     kind of sounds like its a way to normalize a value?
     */
    // abs function:
    /*
     returns the value's distance from 0.
     */
    // fmod function:
    /*
     rounds a number to its nearest integral value. Meaning it just drops the decimal.
     example: 3.6 would become 3.0 not 4.0
     */
    float3 rgb = clamp(abs(fmod(c.x*5.0+float3(0.0,4.0,2.0),6.0)-3.0)-1.0,0.0,1.0);
    rgb = rgb*rgb*(3.0-2.0*rgb);
    return c.z * mix(float3(1.0), rgb, c.y);
}

[[ stitchable ]] half4 swiftIsMyLifeGradient(float2 pos, half4 color, float2 size, float time) {
    // Normalizes the cooridinates position so the range is between 0.0-1.0
    // This allows us to track each pixel relative to the size of the frame. 
    float2 st = float2(pos.x / size.x, 1.0 - pos.y / size.y);
    half3 newColor = half3(0.0);
    
    newColor = half3(hsb2rgb2(float3(st.x,1.0,st.y)));
    
    return half4(newColor, 1.0);
}

```

i think running that code is the best way to visualize what is happening. Also play with the values in the 'hsb2rgb2' function to create different results. Try to recreate the color effect i have shown below. Also, try to add an animation to the colors by using a time variable and sin variable. If you can't yet that's fine, that will be the topic of the next chat! 

<img width="616" height="478" alt="Screenshot 2025-11-25 at 11 40 57 AM" src="https://github.com/user-attachments/assets/b9f4e4ed-67d3-4001-b8a3-b07ee474aea9" />
