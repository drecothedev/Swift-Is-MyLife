Map Swift 

I am embarrassed to admit that I am still not great at using .map(_:). I have came to the realization that the freaky syntax makes things feel a lot more tricky than they actually are. The map function is a transforming function that returns an array with a specified transformation done to that array. This is a convenience function that offers a quicker way to change each element of an array. For example: 

```swift
let arrOfNames = ["Dom", "Jack", "Jill", "Willow"]

print(arrOfNames.map { $0.lowercased() })

// OUTPUT:
["dom", "jack", "jill", "willow"]
```

See the idea behind it is very simple. What confused me ( and still does a bit at first glance ) is the { $0. } part. This is just a compact and quick way to say that you want to start at the first element. You can also write the same code using: 

```swift

let arrOfNames = ["Dom", "Jack", "Jill", "Willow"]

print(arrOfNames.map { word in word.lowercased() 
// OUTPUT:
["dom", "jack", "jill", "willow"]
```

That looks a little more familiar huh? Just makes it look like a for loop which is all maps are. With ( O(n) )

One question that I had when using maps is what functions and changes you can make within the closure. You can do a lot but as I said before it is a shorthand way to write for loops for arrays. For a more real world example: 

```swift

struct Employee: Identifiable {
    var id = UUID()
    var name: String
}

let employeeNames = ["Jim", "Jack", "Buffort"]
let createdEmployees = employeeNames.map { Employee(name: $0) }

print(createdEmployees)

// OUTPUT: 

[JustSwiftQuestionMark.Employee(id: D3E0D3EA-6501-435A-9898-80F0D69C3E59, name: "Jim"),
JustSwiftQuestionMark.Employee(id: 5FD07A34-DEEC-4C58-888D-4E6FE83C7EEC, name: "Jack"),
JustSwiftQuestionMark.Employee(id: 0047202B-25FE-4F6D-9609-BA7F84503884, name: "Buffort")]

```

In this we are using map to create new custom objects. 

In summary, as you can see using the map function isn't as intimidating as it seems. The weird syntax can be off putting at first but once you understand its just a convnient way to make simple transfomrations to arrays it doesn't seem as crazy. 



