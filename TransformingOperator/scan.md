# scan

```swift
let IntPublisher = (1...10).publisher

IntPublisher.scan([]) { numbers, value -> [Int] in
    numbers + [value]
}.sink {
    print($0)
}
```
