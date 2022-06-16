# Publisher

- Publisher
    - 이런 단어가 어울림: **생산자, 배출자, 크리에이터, 배설자**
- Subscriber
    - 이런 단어가 어울림: **소비자, 구독자, 받는 사람**

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
- iOS 에서는 자동으로 Publisher를 제공해주는 녀석들이 있음
    - NotificationCenter
    - Timer
    - URLSession.dataTask

```swift
protocol Subscriber {
    associatedtype Input
    associatedtype Failure: Error 
    
    func receive(subscription: Subscription)
    func reveive(_ input: Input) -> Subscribers.Demand
    func revevie(completion: Subscribers.Completion<Failure>)
 }
```
- Publisher 에게 데이터 요청함
- Input, Failure 타입이 정의 필요함
- Publisher 구독후, 갯수를 요청함
- 파이프라인을 취소할 수 있음
- 빌트인 Subscriber인  `assign` 과 `sink` 가 있음
    - `assign` 는 Publisher가 제공한 데이터를 특정 객체의 키패스에 할당
    - `sink` 는 Publisher가 제공한 데이터를 받을수 있는 클로져를 제공함

# Subscriber & Publisher Pattern
![image](https://user-images.githubusercontent.com/96224311/172390945-d5ba482c-ab03-483d-b82d-72d500a20f93.png)


```swift
import UIKit
import Combine

let just = Just(1000)
let subscription1 = just.sink { value in
    print("Received Value : \(value)")
}

let arrayPublisher = [1, 3, 5, 7, 9].publisher
let subscription2 = arrayPublisher.sink { value in
    print("Received Value : \(value)")
}

class MyClass {
    
    var property: Int = 0 {
        didSet {
            print("Did set property to \(property)")
        }
    }
}

let object = MyClass()
// assign : 방출된 값을 오브젝트의 어떤 값에 할당하겠다.
let subscription3 = arrayPublisher.assign(to: \.property, on: object)
print("Final Value: \(object.property)")

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
