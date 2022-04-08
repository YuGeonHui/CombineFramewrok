# replaceNil

```swift
["A", "B", nil, "D"].publisher.replaceNil(with: "*").sink {
    
    guard let value = $0 else { return }
    print(value)
}
```

# replaceEmpty

```swift
let empty = Empty<Int, Never>()

empty
    .replaceEmpty(with: 1)
    .sink(receiveCompletion: { print($0) }, receiveValue: { print($0) })
    ```
