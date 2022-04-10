# Debug 

```swift
import UIKit
import Combine

// MARK: - print
let publisher = (1...20).publisher

publisher
    .print("Debugging")
//    .sink { print($0) }


// MARK: - handle Events
guard let url = URL(string: "https://jsonplaceholder.typicode.com/posts") else {
    fatalError("Invalid URL")
}

let request = URLSession.shared.dataTaskPublisher(for: url)

let subscription = request
    .handleEvents(receiveSubscription: { _ in print("Subscription Recevied")},
                  receiveOutput:  { _, _ in print("Recevied Putput")},
                  receiveCompletion: { _ in print("Recevied Completion")},
                  receiveCancel: { print("Recevied Cancel") },
                  receiveRequest: { _ in print("Received Request")})
    .sink(receiveCompletion: { print($0) }, receiveValue: { data, response in
    print(data)
})

// MARK: - Using Debug
private var cancellable: AnyCancellable?

cancellable = publisher.breakpoint(receiveOutput: { value in
    return value > 9
}).sink { print($0) } // 디버거로 이동한다.
