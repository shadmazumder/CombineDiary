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

### Clarifying terms
Pipeline: Basically the chaining of [operators](#operators)

### Unknown terms
- Steams of elements in `functional reactive programming`
- `sink`
