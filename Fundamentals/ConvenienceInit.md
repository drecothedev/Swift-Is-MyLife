Convenience initializers in Swift

Ciao👋🏽! initializers are pretty common amongst most programming languages so i will spare an in depth explanation of them. Typically init functions are functions that are called whenever an object is instancitiated. If for instance we have a class that represents a student in our school this may be a simple class that uses an init function to initialize the members of our class. 

```swift
class MyClass {
    var name: String
    var age: Int
    var grade: Int
    var isOnTrackToGraduate: Bool
    
    init(name: String, age: Int, grade: Int, isOnTrackToGraduate: Bool) {
        self.name = name
        self.age = age
        self.grade = grade
        self.isOnTrackToGraduate = isOnTrackToGraduate
    }
}
```
This will usually suffice. But if we did want to maybe have an init that initializes default values we could use our convenience keyword to do that: 

```swift
class MyClass {
    var name: String
    var age: Int
    var grade: Int
    var isOnTrackToGraduate: Bool
    
    
    init(name: String, age: Int, grade: Int, isOnTrackToGraduate: Bool) {
        self.name = name
        self.age = age
        self.grade = grade
        self.isOnTrackToGraduate = isOnTrackToGraduate
    }
    
    convenience init() {
        self.init(name: "Default Student", age: -1, grade: -1, isOnTrackToGraduate: false)
    }
}
```
The requirement for a convenience init is that it must call the classes main initializer. You can also add specific behaviours to that function that may not be in your init: 

```swift
convenience init() {
        self.init(name: "Default Student", age: -1, grade: -1, isOnTrackToGraduate: false)
        print("Default user created")
    }
```
convenience inits also give us the freedom to create an instance of our class without having to fill in all of the parameters. Meaning we can just simply put: 

```swift
let myClass = MyClass() // No parameters
```

