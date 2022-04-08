# compactMap

- Map과 기본적인 실행결과는 비슷하지만, nil인 경우 출력하지 않는다. 

```swift 
let strings = ["a", "1.24", "b", "3.45", "6.7"].publisher.compactMap { Float($0) }.sink {
    print($0) //  1.24 3.45 6.7
}
```
