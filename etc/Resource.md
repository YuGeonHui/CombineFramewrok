# Combine Resource

```swift 
import UIKit
import Combine

guard let url = URL(string: "https://jsonplaceholder.typicode.com/posts") else {
    fatalError("Invalid URL")
}

let subject = PassthroughSubject<Data, URLError>()

// 중복 다운로드를 막기 위해 share() 연산자를 사용한다.
// let requestShare = URLSession.shared.dataTaskPublisher(for: url).map(\.data).print().share()
let requestMulticast = URLSession.shared.dataTaskPublisher(for: url).map(\.data).print().multicast(subject: subject)

let subscription1 = requestMulticast.sink(receiveCompletion: { _ in } , receiveValue: {
    print("Subscription 1")
    print($0)
})

let subscription2 = requestMulticast.sink(receiveCompletion: { _ in } , receiveValue: {
    print("Subscription 2")
    print($0)
})

let subscription3 = requestMulticast.sink(receiveCompletion: { _ in } , receiveValue: {
    print("Subscription 3")
    print($0)
})

// Use Multicast
requestMulticast.connect()
subject.send(Data())
