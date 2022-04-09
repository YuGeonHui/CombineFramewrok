# merge

- 방출하는 모든 값을 합쳐서 하나의 스트림으로 출력해준다. 

```swift
let mergePublisher1 = PassthroughSubject<Int, Never>()
let mergePublisher2 = PassthroughSubject<Int, Never>()

mergePublisher1.merge(with: mergePublisher2).sink {
    print($0)
}

mergePublisher1.send(10)
mergePublisher1.send(11)

mergePublisher2.send(12)
mergePublisher2.send(13)

```
