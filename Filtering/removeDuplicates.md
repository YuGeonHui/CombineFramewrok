# removeDuplicates

- (연속으로) 중복된 값을 무시하고, 새로운 값이 들어오는 경우 출력해준다. 

```swift
let words = "apple apple fruit apple mongo watermelon apple".components(separatedBy: " ").publisher

words
    .removeDuplicates()
    .sink { print($0) }
    
