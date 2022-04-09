# network With Combine

```swift
struct Post: Codable {
    let title: String
    let body: String
}

func getPosts() -> AnyPublisher<[Post], Error> {
    
    guard let url = URL(string: "https://jsonplaceholder.typicode.com/posts") else {
        fatalError("Invalid URL")
    }
    
    return URLSession.shared.dataTaskPublisher(for: url).map { $0.data }
        .decode(type: [Post].self, decoder: JSONDecoder())
        .receive(on: RunLoop.main) // 메인 스레드에서 작동할 수 있게해준다. 
        .eraseToAnyPublisher()
}

let cancellable = getPosts().sink(receiveCompletion: { _ in }, receiveValue: { print($0) })
```
