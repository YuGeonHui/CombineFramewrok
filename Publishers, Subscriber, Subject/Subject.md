# Subject (Publisher)

- `send(_:)`  메소드를 이용해서 이벤트 값을 주입시킬수 있는 퍼블리셔
- 기존의 비동기처리 방식에서 Combine으로 전환시 유용함
- 2가지 빌트인 타입이 있음
    - `PassthroughSubject`
        - Subcriber가 달라고 요청하면,
        - 그때 부터, 받은 값을 전달해주기만 함
        - 전달한 값을 들고 있지 않음
    - `CurrentValueSubject`
        - Subcriber가 달라고 요청하면,
        - 최근에 가지고 있던 값을 전달하고, 그때 부터, 받은 값을 전달 함
        - 전달한 값을 들고 있음

```swift
import UIKit
import Combine

enum MyError: Error {
    case subscriberError
}

class StringSubscriber: Subscriber {
    
    func receive(subscription: Subscription) {
        subscription.request(.max(2))
    }
    
    func receive(_ input: String) -> Subscribers.Demand {
        print(input)
        return .max(1)
    }
    
    func receive(completion: Subscribers.Completion<MyError>) {
        print("Completion")
    }
    
    typealias Input = String
    typealias Failure = MyError
}

class ViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        
        let subscriber = StringSubscriber()
        
        
        let subject = PassthroughSubject<String, MyError>()
        
        subject.subscribe(subscriber)
        
        let subscription = subject.sink { (completion) in
            
            print("Reveived Completion from sink")
            
        } receiveValue: { value in
            
            print("Recevied value from sink")
        }

        subject.send("A")
        subject.send("B")
        
        subscription.cancel()
        
        subject.send("C")
        subject.send("D")
    }
}
``` 
