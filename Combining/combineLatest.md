# combineLatest 

- 방출되는 값 중에서 가장 최신의 것들을 합쳐서 방출한다. 

```swift

let combineLatestPublihser1 = PassthroughSubject<Int, Never>()
let combineLatestPublihser2 = PassthroughSubject<String, Never>()

combineLatestPublihser1.combineLatest(combineLatestPublihser2)
    .sink { print("P1 : \($0), P2 : \($1)") }

combineLatestPublihser1.send(1)
combineLatestPublihser2.send("A") // 1 A
combineLatestPublihser2.send("B") // 1 B

```
