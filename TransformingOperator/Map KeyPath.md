# map KeyPath

```swift
struct Point {
    let x: Int
    let y: Int
}

let publisher = PassthroughSubject<Point, Never>()

publisher.map(\.x, \.y).sink {
    print("x is \($0) and y is \($1)")
}

publisher.send(Point(x: 2, y: 10))
```
