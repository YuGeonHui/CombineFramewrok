# Filter

- filter 내부 조건을 만족한 값만 다음 스트림으로 갈 수 있다.

```swift
let filterNumber = (1...20).publisher

filterNumber.filter { $0 % 2 == 0 }
    .sink { print($0) }
```
