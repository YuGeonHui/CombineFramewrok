# prefix

- 해당인수, 조건을 만족하는 값만 출력해준다. (앞에서 부터)

```swift
let prefixNumber = (1...10).publisher

prefixNumber.prefix(2).sink { print($0) }
prefixNumber.prefix(while: { $0 < 3}).sink { print($0) }
```
