# First

- 조건을 만족하는 첫번째 값을 출력해준다.

```swift

let firstNumber = (1...9).publisher

firstNumber.first(where: { $0 % 2 == 0 })
    .sink { print($0) } // 2
```

# Last 

- 조건을 만족하는 마지막 값을 출력해준다.

```swift
let lastNumber = (1...9).publisher

lastNumber.last(where: { $0 % 2 == 0})
    .sink { print($0) } // 8
