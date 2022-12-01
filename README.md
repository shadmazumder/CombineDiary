# CombineDiary
Swift Combine run daily entry

## Ref
- [Using Combine](https://heckj.github.io/swiftui-notes/#aboutthisbook)
- [Apple doc on Combine](https://developer.apple.com/documentation/combine)
- [Introducing Combine WWDC '19](https://developer.apple.com/videos/play/wwdc2019/722/)
- [Combine in Practice WWDC '19](https://developer.apple.com/videos/play/wwdc2019/721/)
- [Modern Swift API Design](https://developer.apple.com/videos/play/wwdc2019/415/)
- [Data Flow Through SwiftUI](https://developer.apple.com/videos/play/wwdc2019/226)
- [Introducing Combine and Advances in Foundation](https://developer.apple.com/videos/play/wwdc2019/711)
- [Advances in Networking, Part 1](https://developer.apple.com/videos/play/wwdc2019/712/)


## Entry
### 21 Nov
- Project clone
- Intro to reactive programming

### 22 Nov
- Pipeline
- Data stream
- Combine pipelines are a declarative way to define what processing should happen to a stream of values over time

### 23 Nov
- Subscriber is the driver to drive all the Combine's actions
- Without a subscriber, the other components stay idle
- To connect a Subscriber to a Publisher the type must match. Output to Input, and Failure to Failure

#### Publisher
- provides data when available and **upon request**
- will not provide any data if there is no subscription requests
- is described with two associated types, one for Output and one for Failure

#### Subscriber
- requests for data and accepts the data with possible failures
- initiates the request for data, and controls the amount of data it receives
- is described with two associated types, one for Input and one for Failure

#### Operators
- at the same time a Publisher and also a Subscriber
- is used for chaining.
  - processing, reacting, and transforming the data provided by a publisher, and requested by the subscriber

### 24 Nov
- How to read Marble Diagrams on a functional reactive pipeline
- Marble diagrams on Combine
- [Back pressure](https://heckj.github.io/swiftui-notes/#coreconcepts-backpressure)
  - Subscriber controlling the data flow is called Back pressure in Combine.
  - What and When data flows in the pipeline is controlled by the Subscriber

### 26 Nov
- [Demand](https://developer.apple.com/documentation/combine/subscribers/demand)
  - The number of items an subscripber asked for to a publisher.
- Subscriber canceles and stop all related processing of a pipeline through `cancel()`, defined in the `Cancellable` protocol.
- An canceled pipeline ment not to be restart rather it is expected to create a new pipeline.

### 28 Nov
- [Life cycle of publisher and subscriber](https://heckj.github.io/swiftui-notes/#coreconcepts-lifecycle)

<img width="835" alt="Screenshot 2022-11-28 at 11 15 41" src="https://user-images.githubusercontent.com/1079470/204199298-fb93fe49-9819-47e4-9563-6d4ef568b621.png">

1. subscriber calls for `subscribe(_: subscriber)`
2. publisher response with `receive(subscription: Subscription)`
3. Then subscriber request for N values through `request(_: Demand)`
4. Then the data flow begains. publisher might return <=N if has data through `receive(_: Input)`. 
5. Any time subscriber calling `cancle()` will terminate the pipeline
6. If a `cancle()` is not called then the publisher optionally might send a completion block, `receive(completion:)`, containing a `.failure` if appropriate.

From the above we can see the where the marble diagram sits, in between setup and termination/cancle. The marble diagram does not consider the setup or the termination, it is only focusing on the data flow. So the marble diagram only presents the series of events in between data request and pipeline termination.

### 30 Nov
#### Publisher Details
The `Publisher` protocol has strict requirements on
- return type, `Output`
- explicite completion enum, `Failure`

Publisher might return data immediately when requested by a subscriber. In some case the publisher confirms the `ConnectablePublisher` protocol which provides one of the following mechanisam for providing immediate data after request.
- `connect()`
- `autoConnect()`

[List of Publisher](https://heckj.github.io/swiftui-notes/#coreconcepts-publishers)

### 1 Dec
SwiftUI publisher as property wrapper.
- `@Published`
- `@ObservedObject`

#### Operators
- Operates on data. Operations can be filtering, delaying, mapping etc.
- They will compose the pipeline
- accepts one/multiple closure from developer to define the business logic. At the same time it maintains the lifecycle of the publisher/subscriber.

[List of Operators](https://heckj.github.io/swiftui-notes/#coreconcepts-operators)

### Clarifying terms
Pipeline: Basically the chaining of [operators](#operators)

### Unknown terms
- Steams of elements in `functional reactive programming`
- `sink`
