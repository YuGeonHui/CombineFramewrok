# switchLatest

- 가장최신의 구독한 것만 반응한다. 
- 구독 하고 있지 않은경우 값을 방출해도 추가 되지 않는다. 

```swift
// MARK: - switchToLatest
let publihser1 = PassthroughSubject<String, Never>()
let publihser2 = PassthroughSubject<String, Never>()

let publishers = PassthroughSubject<PassthroughSubject<String, Never>, Never>()

publishers.switchToLatest()
    .sink { print($0) }

publishers.send(publihser1)

publihser1.send("Publisher 1 - Value 1")
publihser1.send("Publisher 1 - Value 2")

publishers.send(publihser2) // switching to publisher 2
publihser2.send("Publisher 2 - Value 1")

publihser1.send("Publisher 1 - Value 3") // Not working

// MARK: - switchToLatest continued
let images = ["houston", "denver", "seattle"]
var index = 0

func getImage() -> AnyPublisher<UIImage?, Never> {
    
    return Future<UIImage?, Never> { promise in
        DispatchQueue.global().asyncAfter(deadline: .now() + 3.0) {
            promise(.success(UIImage(named: images[index])))
        }
    }.map { $0 }
        .receive(on: RunLoop.main)
        .eraseToAnyPublisher()
}

let taps = PassthroughSubject<Void, Never>()

let subscription = taps.map { _ in getImage() }
    .switchToLatest().sink { print($0) }

// huston
taps.send()

DispatchQueue.main.asyncAfter(deadline: .now() + 6.0) {
    index += 1
    taps.send()
}

DispatchQueue.main.asyncAfter(deadline: .now() + 6.5) {
    index += 1
    taps.send()
}
```
