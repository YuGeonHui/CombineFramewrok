# collect

```swift
import UIKit
import Combine


["A", "B", "C", "D"].publisher.sink {
    print($0)
    // A
    // B
    // C
    // D
}

["A", "B", "C", "D"].publisher.collect().sink {
    print($0)
    // ["A", "B", "C", "D"]
}

["A", "B", "C", "D"].publisher.collect(2).sink {
    print($0)
    // ["A", "B"]
    // ["C", "D"]
}

["A", "B", "C", "D", "E"].publisher.collect(2).sink {
    print($0)
    // ["A", "B"]
    // ["C", "D"]
    // ["E"]
}
```
