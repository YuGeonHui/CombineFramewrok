# Publisher

- Publisher : 생산자, 배출자, 크리에이터, 배설자 

```swift
protocol Publisher {
    associatedtype Output
    associatedtype Failure: Error 
    
    func subscribe<S: Subscriber>(_ subscriber: S)
        where S.input == Output, S.Failure == Failure
 }
```
- 데이터 배출하는 친구
    - 구체적인 output 및 실패 타입을 정의함
    - Subscriber 가 요청한것 만큼 데이터를 제공
- 빌트인 Publisher인 `Just`, `Future` 가 있음
    - `Just` 는 값을 다루고
    - `Future` 는 Function 을 다룸
- iOS 에서는 자동으로 제공해주는 녀석들이 있음
    - NotificationCenter
    - Timer
    - URLSession.dataTask


```swift
import UIKit
import Combine

class StringSubscriber: Subscriber {
    
    func receive(subscription: Subscription) {
        print("Received Subscription")
        subscription.request(.max(3)) // backpressure
    }
    
    func receive(_ input: String) -> Subscribers.Demand {
        print("Received Value", input)
        return .unlimited
    }
    
    func receive(completion: Subscribers.Completion<Never>) {
        print("Completed")
    }
    
    
    typealias Input = String
    typealias Failure = Never
    
}

class ViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        
        let publisher = ["A","B","C","D","E","F","G","H","I","J","K"].publisher
        
        let subscriber = StringSubscriber()
        
        publisher.subscribe(subscriber)
        
    }
}
```
