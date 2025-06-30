Protocols in Swift

Phew! Protocols hit me hard when I first started learning Swift and truthfully I still haven't had as much practice as I would like to in real world application but ChatGPT told me to do this so we do this. Expect updates periodically. Here is a story time 4U: 

Swift supports OOP ( Object Oriented Programming ( Classes, Structs, Inheritnece etc. ) ), like most languages, but it also supports POP ( Protocol Oriented Programming ). POP allows us to use Classes and Structs ( and other custom types ) that conform to Protocols, or blueprints, for an object.  These types can also conform to multiple protocols. In order for a data type to conform to a Protocol it must inclue the methods or values from that Protocol. For a simple example: 

```swift

protocol Theme {
    var mainColor: String { get }
    var secondaryColor: String { get set }
    var thirdyColor: String { get }
}


struct MainTheme: Theme {
    let mainColor: String
    
    var secondaryColor: String
    
    let thirdyColor: String
    
    var aFourthColor: String?
    
    func mixColors() -> String {
        return "\(mainColor) \(secondaryColor) makes Purple"
    }
}



print(MainTheme(mainColor: "red", secondaryColor: "blue", thirdyColor: "green").mixColors())

```

In this simple example you can see that "MainTheme" has all of the variables from the Theme protocol declared as well. The " { get } " part just means that the value is only readable. The { get set } allows for reading and writing. That is why you see that the variables defined with { get } can be assigned as let because you cannot write to them. 

Now this is a very simple example but things get much more complex when using other developers protocols or using Swift Libraries. Luckily you don't need to remember all of the methods and properties from protocols because Xcode will automatically add in those "stubs" for conformance. So all you need to do is work with the methods and variables provided. Here is a real world example that you see everytime you open XCode: 

```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        VStack {
            Image(systemName: "globe")
                .imageScale(.large)
                .foregroundColor(.accentColor)
            Text("Hello, world!")
        }
    }
}
```
If you took this snippet and entered it into Xcode it would run fine. However, try to delete that "var body: some View" line. You will see that you now get an error. This is because since ContentView conforms to View it needs to have a body var present. Now try to erase the VStack inside the body var and see what happens. You also get an error and this is becasue body comforms to some View which means there needs to be at least one view inside the body. As you can see with protocols you are just ensuring that you adopt the necessary methods and properties needed for conformity. 

 Here is another real world example from an app that I was working on: 

```swift
import AVKit
import SwiftUI
import VisionKit


struct DocumentScannerViewController: UIViewControllerRepresentable {
    
    @Binding var recognizedItems: [RecognizedItem]
    
    func makeUIViewController(context: Context) -> DataScannerViewController {
        let scanner = DataScannerViewController(
            recognizedDataTypes: [.text()],
            qualityLevel: .balanced,
            recognizesMultipleItems: false,
            isHighFrameRateTrackingEnabled: true,
            isGuidanceEnabled: true,
            isHighlightingEnabled: true
            
        )
        return scanner
    }
    
    func updateUIViewController(_ uiViewController: DataScannerViewController, context: Context) {
        uiViewController.delegate = context.coordinator
        try? uiViewController.startScanning()
        uiViewController.dismiss(animated: true)
    }
    
    
    func makeCoordinator() -> Coordinator {
        Coordinator(recognizedItems: $recognizedItems)
    }
    
    class Coordinator: NSObject, DataScannerViewControllerDelegate {
        @Binding var recognizedItems: [RecognizedItem]
        
        init(recognizedItems: Binding<[RecognizedItem]>) {
            self._recognizedItems = recognizedItems
        }
        
        func dataScanner(_ dataScanner: DataScannerViewController, didTapOn item: RecognizedItem) {
            print("did tap \(item)")
            recognizedItems.append(item)
        }
        
        func dataScanner(_ dataScanner: DataScannerViewController, becameUnavailableWithError error: DataScannerViewController.ScanningUnavailable) {
            print("Scanner became unavailable for the following error \(error)")
        }
        
        func dataScanner(_ dataScanner: DataScannerViewController, didAdd addedItems: [RecognizedItem], allItems: [RecognizedItem]) {
            print("added \(addedItems) to \(allItems)")
        }
    }
}
```
This Struct conforms to the UIViewControllerRepresentable protocol which requires all of the functions inside the struct. 

