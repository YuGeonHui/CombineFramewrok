# ignoreOutput

- output으로 출력하지 않고, finished만 출력해준다.

```swift
let ignoreNumbers = (1...5000).publisher
ignoreNumbers.ignoreOutput().sink(receiveCompletion: { print($0) }, receiveValue: { print($0) }) // finished
```
