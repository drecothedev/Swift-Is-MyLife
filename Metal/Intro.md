Intro to Metal

Ciao! I just got tapped into Metal for shaders in Swift/SwiftUI. What an interesting journey it has been thus far. If you are not familiar, Metal is a framework that lets us access the GPU. Programmers use this for task that may be too costly for running on the CPU. This is because the CPU operates in a first in first out order. This means task are handled almost like a queue. This usually isn't an issue but when it comes to intensive task it becomes one. For really intense task programmers like to use the GPU because task are handled in parrellel. This means that the computer can process more task at the same time rather than having to wait behind others. 

There are a few things to keep in mind. The first is that metal functions aren't 'for loops'. We will see why this matters more later when gettting into creating a simple shader, but it is important to keep in mind that all of the functions being ran are blind to the others. Additionally, they all happen at once so there is not simple interation. 

The second thing to keep in mind is that debugging with metal is very different than other programming languages. There really isn't a console to print to so this can make it a lot harder to figure out what is happening within your code. I have heard that it is a lot like building a ship in a bottle. You just gotta try it and see how it goes. 

The last thing to keep in mind is that i have encountered a ton of math when learning all of this. Even though this is a bit intimidating i think learning a bit about math is pretty cool. There is also a lot of resources online that help us with the math parts. 

Okay now with all of that out the way let's get into setting up your SwiftUI code to use a metal shader. Start a new project and create a file named: ShaderLibrary.metal. This will add a our library to our project. Then in that file try out the following code: 

```swift
// Metal Method that will return a Cyan color
[[ stitchable ]] half4 changeColor(float2 pos, half4 color) {
    return half4(0,1.0,1.0,1.0);
}
```

In your SwiftUI code you want to call your function like this: 

```swift
struct SwiftIsMyLifeView: View {
    var body: some View {
        RoundedRectangle(cornerRadius: 0.0)
            .frame(width: 100, height: 100)
            .colorEffect(
                ShaderLibrary.changeColor()
            )
            
    }
}
```

If you have only programmed in Swift before this will probably look very confusing. Metal uses a syntax similar to C in order to give us control of the lower level programs we need. the '[[ stitchable ]]' just gives us the ability to use this function in a SwiftUI context. The 'half4' is a type that is represents a 4D vector. This just means it is a variable that holds a list of 4 numbers. The 'half' represents the precision point of that number. We then have a seemingly normal function call. float2 represents a 2D vector or list of 2 numbers. 'float' represents the precision of that number. We then return a 4D vector that contains the RGB + a values to represent a cyan color. So, all this function does is take every pixel (pos) and returns that pixel with the cyan color. In some of the following post I will show you how to make some cool gradient effects using math. For now I think it would be a good idea to play around with those RGB vaalues to see how it effects the color ( note the RGB values are normalized, meaning they range from 0.0 - 1.0 ). 
