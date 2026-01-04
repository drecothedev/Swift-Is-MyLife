Retries using Swift Concurrency

Ciao!👋🏽 Recently i have revisited Swift Concurrency. After learning more about shaders and how they are just functions that run in parrellel, my inituition towards concurrent functions has greatly incresed. That is not to say that Swift concurrency has become easy. Swift concurrency is still a bit tricky to me but i am far more comfortable with the idea of thread management. I decided to try to build a Swift package that will automaticaly retry all async/await functions that are called. This was a bit tricky for me to figure out and understand it's application but after a bit of tinkering around this is what i constructed.

```swift
// In my DataService class
func fetchUsersWithRetry(maxAttempts: Int, initialDelay: Double) async throws {
        
        for attempt in 0..<maxAttempts {
            do {
                let goodUrl = URL(string: "http://localhost:3000/users")
                let badUrl = URL(string: "http://localhost:3000")
                print("Running Request...")
                guard let goodUrl = goodUrl else {
                    return
                }
                
                guard let badUrl = badUrl else {
                    return
                }
                
                let request = URLRequest(url: badUrl)
                
                let (data,reponse) = try await session.data(for: request)
                
                print(try JSONDecoder().decode([User].self, from: data))
                print("Succeeded on \(attempt + 1).")
                return 
                
            } catch {
                // Throw error on last attempt
                if attempt == maxAttempts - 1 {
                    print(error)
                    throw error
                }
                
                // Implement Backoff. Time between requests
                let delay = initialDelay * pow(2.0, Double(attempt))
                print("Request failed... trying again in \(delay) seconds")
                try await Task.sleep(nanoseconds: 1_000_000_000 * UInt64(delay))
            }
        }
    }
```
In this code you can see that we are attempting to retry our network request whenever it fails. We know it fails becuase we wrap it in a do catch statement, which allows us to safely return back to our for loop. We set a max attempts to stop retrying at some point. We set up a delay to put time in between our request. Moving forward, i do want to implement retry conditions, meaning that we only retry on certain conditions. This is becuase there is no reason for us to retry the same request with the same wrong url. 
