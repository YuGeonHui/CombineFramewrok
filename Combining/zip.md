# zip

- 방출되는 값이 둘다 존재하는 경우 출력이 가능하다.
- 방출되는 순서와 상관없이 짝이 맞는경우 값을 방출한다. 

```swift
let zipPublisher1 = PassthroughSubject<Int, Never>()
let zipPublisher2 = PassthroughSubject<String, Never>()

zipPublisher1.zip(zipPublisher2)
    .sink { print("P1 : \($0), P2 : \($1)") }

zipPublisher1.send(1)
zipPublisher1.send(2)
zipPublisher2.send("3") // 1, "3"
zipPublisher2.send("4") // 2, "4"
```
