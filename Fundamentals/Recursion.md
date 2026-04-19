Recursion in Swift

Ciao!👋🏽 "To understand recursion, you must first understand recursion" - some guy. Recursion in Swift is exactly the same as recurion in other languages so, this will mostly be more about recursion and not anything super Swift specific. Recursion is when a function calls itself. It's sounds simple, and in some implementations it really is. Take a look at this example: 

```swift
func fib(_ num: Int) -> Int {
        // Base case. 
        guard num > 1 else {
            return num
        }
        // Fibonacci formula
        return fib(num - 1) + fib(num - 2)
    }
// Test 1:
// input: 6
// output: 8

// Test 2:
// input: 20
// output: 6765
```

I've been learning about recursion for a couple weeks now, and months if you include Recursive Descent, but it's still not always intuitive when solving problems. For this example, we have a method called 'fib' that calls itself as long as its input is greater than 1. The most important part of this program is what is called the 'base case'. This is the constraint that lets us exit out of our recursive journey. Without this your program is inevitably going to crash. This is becasue whenever a function needs to be processed your program will allocate space on the stack for that method. So similar to a while loop that never reaches its constraint, your program will continue allocating space on the stack, the difference is that there is a stricter limit on how much can be added to the stack. When the limit is reached you get a 'stack overflow', and your program is cooked. Implementing the correct base case can sometimes be a bit a tricky but this tends to be the most straight forward part of recursion. 

When learning more about recursion i read an article that described it as putting puzzle pieces together in order to create the intended picture. i think this describes the process of building recursive solutions perfectly, especially the more leetcode style problems. When i try to build recursive solutions it almost helps me more to think more conceptually about the problem, as opposed to having a very granular approach. I'm not sure if that makes a bunch of sense but i'll try to provide an example: whenever solving problems with pointers or hash maps i think about each specific case much more. If this equals that then do this, or if that equals this do that. When trying to implement recursive solutions i try to think more about how the solution should behave and how i can define the proper rules for that behaviour. i know it sounds hippieish but that is just how my brain tries to solve these problems. Here is another example of a leet code solution that has pretty simple code but took a bit of thinking to solve: 

```swift
func countNodes(_ root: TreeNode?) -> Int {
        if root == nil {
            return 0
        }
        if root?.left == nil && root?.right == nil {
            return 1
        }

        return 1 + countNodes(root?.left) + countNodes(root?.right)
    }
```

i don't think this is the most effecient solution but it was the one i initally thought of. 
