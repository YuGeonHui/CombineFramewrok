# Timer 

```swift
// MARK: - RunLoop
let runLoop = RunLoop.main

let subscription = runLoop.schedule(after: runLoop.now, interval: .seconds(2), tolerance: .microseconds(100)) {
    
    print("Timer fired")
}

runLoop.schedule(after: .init(Date(timeIntervalSinceNow: 3.0))) {
    subscription.cancel()
}

// MARK: - Timer Class
let publisher = Timer.publish(every: 1.0, on: .main, in: .common).autoconnect()
    .scan(0) { counter, _ in
        counter + 1
    }.sink { print($0) }

// MARK: - DispatchQueue
let queue = DispatchQueue.main
let source = PassthroughSubject<Int, Never>()
var count = 0

let cancellable = queue.schedule(after: queue.now, interval: .seconds(1)) {
    source.send(count)
    count += 1
}

let sourceSubScription = source.sink { print($0) }
