URLSession Configuration in Swift!

Ciao👋🏽! In previous examples i have used a URLSession to fetch data from an api/database. When doing so i used the URLSession.shared.data() method. This isn't inherently bad. It just doesn't give use the customability of using a session configuration. A session configuration is defined as: An URLSessionConfiguration object defines the behavior and policies to use when uploading and downloading data using an URLSession object. This allows us to make rules for our session so that it operates on certian conditions. It is mentioned that should be your first step whenever making network request, no matter what. If you are doing somehting very simple, then it is okay to used the .shared, but other than that, you should not. 

Why would you need rules or policies for your session? This is the question i thought of at first. Usually when doing a URL task whenever we get an error the api lets us know so why so what is the need for these guard rails? What made this all click for me was when i used a timeoutInterval. This helped me understand things becasue while reaching out to a local database, i was having issues and after about 5 seconds my program let me know that the request timed out. This is extremely helpful because instead of sitting there for an infinite amount of time, the probgram let me know early that this process is porbably not going to work. 

When it comes to using a session configuration, it is best to configure your rules once and use that session across your different request. The best way that i have found to implement this is to initialize in your configuration within your class's init() and initialize your session that configuration object. here is an example: 

```swift
class DataService {
    var session: URLSession
    
    init() {
        let config = URLSessionConfiguration.default
        config.waitsForConnectivity = true
        config.timeoutIntervalForRequest = 5
        config.timeoutIntervalForResource = 10
        config.allowsCellularAccess = true
        session = URLSession(configuration: config)
    }
}
```

This way we are not changing our session once it is declared, this would be the "bad" way of initializing your session: 

```swift
class DataService {
    var session: URLSession = URLSession(configuration: .default)
// This is not ideal because we are creating mutable state within our session. 
    func prepareSession() -> URLSession {
        // Congiure and return session
    }
}
```

As you can see in our first example we are creating a default configuration and then adding behaviours to it. We then init our session with those configuration settings. 

There are three different configs that you can use to init your configurations behaviors. The first and most common would be default. This is similiar to just using the URLSession.shared instance. The second is an ephemeral.  An ephemeral session configuration object is similar to a default session configuration (see default), except that the corresponding session object doesn’t store caches, credential stores, or any session-related data to disk. These are ideal when privacy is of great concern. The last is "background" which creates a session configuration object that allows HTTP and HTTPS uploads or downloads to be performed in the background.

After configuring we can then use our session as we usually would: 

```swift
func fetchUsers() async {
        let goodUrl = URL(string: "http://localhost:3000/users")
        let badUrl = URL(string: "http://localhost:3000")
        
        guard let goodUrl = goodUrl else {
            return
        }
        
        guard let badUrl = badUrl else {
            return
        }
        
        let request = URLRequest(url: badUrl)
        do {
            let (data, result) = try await session.data(for: request)
            
            if let result = result as? HTTPURLResponse {
                let status = result.statusCode
                guard status == 200 else { print(status); return }
            }
            
            let decoder = JSONDecoder()
            let decodedData = try decoder.decode([User].self, from: data)
            
            print(decodedData)
        } catch {
            print("Error: \(error.localizedDescription)")
        }
    }
    
```
Don't mind all of the fluff in this example, it was also used for me test retries.
