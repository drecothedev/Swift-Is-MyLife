Using periodic functions for color effects

Ciao!👋🏽 Recently I started looking into how to create smooth oscilating animations using sine functions. I then thought to myself what if we used other "waves" to oscilate animations. I mean it made sense to me musically. So i chose to give it a try. Here are some examples of other common periodic functions: 

```swift
// In this function we use different periodic functions to simulate color effects
[[ stitchable ]] half4 periodicFuncPractice(float2 pos, half4 color, float2 size, float time) {
    float2 uv = float2(pos.x / size.x, 1.0 - pos.y / size.y);
    
    // Sine wave:
    float y = uv.x + sin(time);
    
    // Square wave:
    // float y = uv.x + sign(sin(2*PI*0.5*time));
    
    // Triangle Wave:
    // float y = uv.x + 2/PI * asin(sin(2*PI/10.3*time));
    
    // Sawtooth Wave:
    // float y = uv.x + 2*(sin(time) - 1/2*sin(2*time) + 1/3 * (sin(3*time)) - 1/4 * sin(4*time) + 1/5 * sin(5*time) - 1/6 * sin(6*time) + sin(time) - 1/7*sin(7*time) + 1/8 * (sin(8*time)) - 1/9 * sin(9*time) + 1/10 * sin(10*time) - 1/11 * sin(11*time));
    
    
    
    half3 newColor = half3(y);
    return half4(newColor, 1.0);
    
}
```

Go ahead and gives those a try. These are just formulas i found online. The last one is a sawtooth represented as a fourier series. Pretty sick huh! you can add these to actual colors and get some really interesting things. Here is an example: 

WARNING THIS MAY CAUSE SOME WEIRD REACTION BECAUSE IT IS A BIT WEIRD AND HYPNOTIC

```swift
[[ stitchable ]] half4 simyPeriodFuncs(float2 pos, half4 color, float2 size, float time) {
    float2 uv = float2(pos.x / size.x, 1.0 - pos.y / size.y);
    half3 influencedColor = half3(0.678, 0.847, 0.902);
    half3 influencingColorA = half3(0.502, 0.0, 0.502);
    half3 influencingColorB = half3(0.0, 0.502, 0.502);

    half3 newColor = mix(influencingColorB, influencingColorA, smoothstep(uv.x/2, 1.0, uv.x +uv.y));
    half3 finalColor = mix(newColor, influencedColor,
                           (4/uv.x)* sin(uv.x * 2 *PI*time/10*PI));
    finalColor = mix(finalColor, half3(0.5), smoothstep(0.0, 1.0, length(uv) + sin(time)));
    
    return half4(finalColor, 1.0);
}
```
I am sure this has practical use that i have yet to discover. But really got a bit carried away with just how bizzare it can get. The important part to remember is that using periodic functions can create different gradients, animations, and more. 







