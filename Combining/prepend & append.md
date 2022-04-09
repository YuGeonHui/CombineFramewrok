# prepend

- 원소의 앞에 값을 추가해준다. 

```swift
let prependNumber = (1...5).publisher
let extraPublisher = (500...510).publisher

prependNumber.prepend(100, 101).prepend(extraPublisher).sink { print($0) }
```

# append

- 원소의 뒤에 값을 추가해준다. 

```swift
let appendNuber = (1...10).publisher
appendNuber.append(extraPublisher).append(11, 12).sink { print($0) }
```
