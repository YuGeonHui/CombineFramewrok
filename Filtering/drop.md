# dropFirst

- 인수만큼 앞에서 부터 값을 제거한다. 

```swift
let dropFirstNumber = (1...10).publisher

dropFirstNumber.dropFirst(5).sink { print($0) } // 6 7 8 9 10

```

# dropWhile

- 해당 조건을 만족할 때 까지 제거한다. (조건을 만족하면 제거하지 않음)

```swift
let dropWhileNumber = (1...10).publisher

dropWhileNumber.drop(while: { $0 % 3 != 0 }).sink { print($0) } // 3 4 5 6 7 8 9 10

```

# dropUntilOutputFrom

```swift
let isReady = PassthroughSubject<Void, Never>()
let taps = PassthroughSubject<Int, Never>()

taps.drop(untilOutputFrom: isReady).sink {
    print($0)
}

(1...10).forEach { n in taps.send(n)
    
    if n == 3 { isReady.send() }
}

```
