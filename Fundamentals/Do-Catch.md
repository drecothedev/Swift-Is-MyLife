Do - Catch Statements Swift

Do-Catch statements are powerful ways to handle errors in Swift. The idea behind these statmeents are shared across many different languages so you may have experienced them before but with different words. For example in Python you may use " Try-Except " or nothing... in GOLang LOL. These statments are different than optional statements becasue they are not checking for the presence of a value but rather checking the validity or usefulness of a value. They give you the ability to catch an error and move on without your app crashing, or throw a friendly message in replacement of the actual error. Here is a simple Swift example: 

```swift
// Define an error type
enum FileError: Error {
    case fileNotFound
}

// Function that can throw an error
func readFile(named fileName: String) throws -> String {
    if fileName == "important.txt" {
        return "This is the file content."
    } else {
        throw FileError.fileNotFound
    }
}

// Use do-catch to handle the error
do {
    let content = try readFile(named: "notes.txt")
    print("File content: \(content)")
} catch FileError.fileNotFound {
    print("Error: The file was not found.")
} catch {
    print("An unexpected error occurred: \(error)")
}


```

In this example ( from chatGPT ) we not only see how to handle errors but also how to create functions or methods that give us the ability to handle errors safely. This is the "throws" keyword after the function parameters. If execution of the function failed it will return/ throw a enum case rather than haulting our app. 

For another real world example imagine we are fetching data from an API. There are many issues that can show up: Wrong Headers, Serever is down, Blase' blase' blase'. Instead of our app just being completely useless as a result we can safely move on without completely ruining the UX. This comes from an app I did for School when connecting to a user database: 

```swift
// Method Declaration in DataService Class 
 func getUserFromDisplayName(displayName: String) async throws {
        do {
            print("Finding info for user: \(displayName)")
            let dataTaskResult = try await db.collection("users").whereField("displayName", isEqualTo: displayName).getDocuments()
            
        
            for document in dataTaskResult.documents {
                var data = document.data()
            }
            
        } catch  {
            print("Unable to get users")
        }
    }

// Calling fucntion in ViewModel
func getUserFromDisplay(displayName: String) {
        Task {
            do {
                print("Grabbing User: \(displayName)")
                try await DataService.shared.getUserFromDisplayName(displayName: displayName)
                
            } catch {
                print("Error grabbing user: \(displayName)")
                return
                
            }
        }
    }
```

In this code i am simply cathcing the errors so that they don't crash the app. I am not throwing the errors as you can see and that is because I didn't have time to write the throw logic and just wanted to print to the console for debugging. In real use cases though it would be more beneficial to actually throw errors if needed. 

