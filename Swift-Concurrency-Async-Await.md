Swift Concurrency

Ciao, this will have to be updated eventually with more real world application and learning but this is my understanding so far. If you just started learning Swift within the last couple years you will hear some Swift Uncs ( people who have been programming in swift for a long time ) rave about async/await. This is because it is a relatively new feature with Swift 5.5. Way b4 my time. Before async/await, Swift developers used closures, DispatchQueue, and sometimes Result types to handle asynchronous tasks. 

```swift

let url = URL(string: "https://api.api-ninjas.com/v1/quotes")!
var request = URLRequest(url: url)
request.setValue("YOUR_API_KEY", forHTTPHeaderField: "X-Api-Key")
let task = URLSession.shared.dataTask(with: request) {(data, response, error) in
    guard let data = data else { return }
    print(String(data: data, encoding: .utf8)!)
}
task.resume()

// Example taken from API Ninjas. Great website for practicing network Request.
```
In this example you can see how it is still very possible to make solid network request without Concurrency. But it is a bit more wordy and there are just more things to keep track of. 

With the new async/await keywords you can perform these async task in a way that resembles structured programming. This makes it way more readable and less confusing. Take a look at this example where I am using a data service to retrieve data from a server. 


```swift
// DataService.Swift

    func prepareGetRequest(url: String) throws -> URLRequest  {
        guard let url = URL(string: url)  else {
            throw DataServiceErrors.badUrl
        }
        var request = URLRequest(url: url)
        request.httpMethod = "GET"
    
        return request
    }
    
    
    
    func getProducts() async {
        do {
            let request = try prepareGetRequest(url: "http://127.0.0.1:8080/products")
            let (data, response) = try await URLSession.shared.data(for: request)
            
            let decodedData = try JSONDecoder().decode([Product].self, from: data)
            print(decodedData)
            
            
        } catch {
            print("Error Found: \(error)")
        }
    }

```

In this snippet we are preparing a GET request ( since we will be handling many different get request ) that will prepare the url request. This doesn't use asynchronous code but it does throw which is why we use the keyword "try" when calling it. In our actual getProducts function we will be performing asynchronous code which is why we define the function with async. 

Now before we dissect more you may be wondering why we even need to perform asynchronous code. The answer is pretty simple. Just because your app is waiting for data, doesn't mean the user should have to as well. Imagine if you were using facebook and everytime you opened the app you had to wait for the billions of data points to load before even seeing your homepage. That would feel like a summer in hell. So, we should run long-running tasks like network calls asynchronously to avoid blocking the main thread. While it may use different threads under the hood, Swift's concurrency model abstracts this by using lightweight tasks managed by the system. Otherwise, The user could experience to be jumpiness and slowness, and who wants that? 

The Async keyword allows us to define a function that can be suspended during it's execution. This allows the app to still continue executing other blocks of code while the asyn function is still processing. So in the example above we are waiting for the network request to complete before decoding data. 
You use Async and Await like peanut butter and jelly. They need eachother! You have to use the await keyword when calling or assigning async functions. 

And with that we understand Swift Concurrency right? Of course not, I think Concurrency is a pretty complex topic in but Swift makes it very simple to work with. There are still other topics to explore like Actors and Task, which will be coming soon. 

