---
title:  "Test with iOS"
description: "This article tries to generalize the best practice of testing with iOS project."
date: 2017-07-01 15:04:23
categories: [Tech]
tags: [iOS]
---

# Test with iOS

> * Author: [Damon Yuan](https://www.damonyuan.com)
> * Date: 2017-07-01

This article tries to generalize the best practice of testing with iOS project.

## 1. Functional reactive programming

#### 1.1 What is functional?
> [In functional code, the output value of a function depends only on the arguments that are passed to the function, so calling a function f twice with the same value for an argument x will produce the same result f(x) each time; this is in contrast to procedures depending on a local or global state, which may produce different results at different times when called with the same arguments but a different times when called with the same arguments but a different program state.](https://en.wikipedia.org/wiki/Functional_programming)

One of the most important parts of functional programming is that when the input is decided, the output is also determined. In other words, the functions are referential transparency.

#### 1.2 What is Reactive?
> [Systems using an assembly line concurrency model are also sometimes called reactive systems, or event driven systems. The system's workers react to events occurring in the system, either received from the outside world or emitted by other workers. Examples of events could be an incoming HTTP request, or that a certain file finished loading into memory etc.](http://tutorials.jenkov.com/java-concurrency/concurrency-models.html#reactive-event-driven-systems)

Reactive is an assembly line with independent workers dealing with different types of events. It helps divide the programming into a fine-grained subroutine like services in distributed system.

Actors and channels are two similar examples of assembly line (or reactive / event driven) models.

![Actors](http://tutorials.jenkov.com/images/java-concurrency/concurrency-models-7.png "Actors")

![Channels](http://tutorials.jenkov.com/images/java-concurrency/concurrency-models-8.png "Channels")

#### 1.3 What is functional reactive programming?

> [Functional Reactive Programming (FRP) integrates time flow and compositional events into functional programming. This provides an elegant way to express computation in domains such as interactive animations, robotics, computer vision, user interfaces, and simulation.](https://wiki.haskell.org/FRP "FRP")

Here is a link in [Stackoverflow](https://stackoverflow.com/questions/1028250/what-is-functional-reactive-programming), which I think it has more detailed explanation about FRP.

In my understanding, FRP is a programming paradigm which combines functional and reactive together. This model handles continuous (Reactive) and deterministic (Functional) concurrency with ease and grace (generalized API design). The basic idea behind reactive programming is that there are certain datatypes that represent a value "over time". Computations that involve these changing-over-time values will themselves have values that change over time.

There is an excellent analogy: [An easy way of reaching a first intuition about what it's like is to imagine your program is a spreadsheet and all of your variables are cells. If any of the cells in a spreadsheet change, any cells that refer to that cell change as well.](https://stackoverflow.com/questions/1028250/what-is-functional-reactive-programming "analog") It is functional because when the input is constant, the output of those related cells is also constant, there won't be a different result. It is reactive because cells react to an input event, which is bound with the time -- the value changes at some specific time.

#### 1.4 Why to use functional reactive programming?

> [Reactive Programming raises the level of abstraction of your code so you can focus on the interdependence of events that define the business logic, rather than having to constantly fiddle with plenty of implementation details. Code in RP will likely be more concise.](https://gist.github.com/staltz/868e7e9bc2a7b8c1f754 "why reactive")

Imagine a basic scenario: user login. Normally there is two UITextField and one UIButton. In a non-reactive implementation, when a user interacts with the UITextField, callbacks will be invoked and inside the callback function, we can do some validation to check whether to enable login button or not. If the inputs are valid, we enable the login button and can send the request to the backend.

In reactive way, every component can be treated like a number, and the whole system can be treated like a math equation. In order to do it in iOS, the project structure needs to be MVVM, it means that every UI component need has a corresponding ViewModel which is a data structure reflecting the information of the UI component. And reactive programming is programming with asynchronous data streams, and a stream is a sequence of ongoing events ordered in time.

One of the reasons for efficiency lift from reactive is that the asynchronous event's sequence is perceptive in the program with a declarative way because behaviors/events are bound with time. For example, sometimes data A and data B has some relationship in business logic and the web page should only rerender after both A and B are updated. It is hard for non-reactive programming to know whether both A and B are updated because events are fired asynchronously, so normally the web app will rerender the whole page every time the update event received regardless of the event type. But it is easy for reactive programming to understand it and only rerender the view at the right time, and only render the view of which the ViweModel has the value changed.

#### 1.5 How to implement functional reactive programming in iOS?

Libraries are already available in iOS:

Objective C: [ReactiveObjC](https://github.com/ReactiveCocoa/ReactiveObjC "ReactiveObjC")
Swift: [ReactiveCocoa](https://github.com/ReactiveCocoa/ReactiveCocoa "ReactiveCocoa")

The standard for reactive API is well defined and the API for the library is well documented. What we need to do is just to use Cocoapods or Carthage to integrate them into our projects.

For details about implementation please check the sample project.

----

## 2. MVVM over MVC

*MVC*
![MVC](https://koenig-media.raywenderlich.com/uploads/2014/06/MVCPattern-2.png "MVC")

*MVVM*
![MVVM](https://koenig-media.raywenderlich.com/uploads/2014/06/MVVMPattern.png "MVVM")

#### 2.1 MVVM is better compatible with FRP

Because in reactive way, every component can be treated as a data structure, it makes sense to create a ViewModel for each view component. In old traditional MVC, the model contains all the attributes based on backend API design, but not all of them are used in one specific view model. Mostly only part of those attributes is reflected in the view component. Extracting the ViewModel from the model is enabling true separation between the view and model. 

It is good to simplify the business logic in a model, after the separation, models mainly take care about the data persistent and synchronization, like save data into SQLite, fetching data from remote backend and keeping remote and local data synchronized. For ViewModel, it mainly concerns about the data binding between view (Note: the view include View and ViewController in MVVM, because it only handles the rendering logic now) and ViewModel, and the view will render reactively based on the event from ViewModel.

#### 2.2 MVVM is easier for unit test

In MVC the controller is the hub of communication between models and views, which makes it clumsy and filled with both rendering logic and business logic. In MVVM the controller is much simpler because its only job is to rendering view and event the rendering logic is implemented in ViewModel. And it is much easier to test on ViewModel because is relatively independent compared with UIViewController, which has many life-cycle callbacks which will be called by the iOS system during runtime.

----

## 3. Stub and Mock

#### 3.1 What is Mock and Stub

Stub: For replacing a method with code that returns a specified result.

Mock: A stub with an assertion that the method gets called.

Mocks look similar to Stubs, but [Mocks Aren't Stubs](https://martinfowler.com/articles/mocksArentStubs.html "Mocks Aren't Stubs").

Long to be short, based on my understanding, the stub is a simple fake object, it just makes sure test runs smoothly, like stubbing a request using Nocilla, but we never test the stub itself.

Mock is a smarter stub, we verify our test passes through it. It waits to be called by the class under test, and it makes sure that it was contacted in exactly the right way, or the test will fail.

Example in sample: 

```
// EtStationsTableViewCell.m
context(@"set view model after set the view model", ^{
        __block id chargingStationProtocolMock;
        __block EtStationViewModel *viewModel;
        
        beforeEach(^{
            chargingStationProtocolMock = OCMProtocolMock(@protocol(EtChargingStationProtocol));
            OCMStub([chargingStationProtocolMock getAddress]).andReturn(@"stub address");
            viewModel = [[EtStationViewModel alloc] initWithStation:chargingStationProtocolMock];
            [cell setViewModel:viewModel];
        });
        
        it(@"textLabel should have no address as the station view model before bind", ^{
            expect([[cell textLabel] text]).to.beNil();
        });
        
        it(@"textLabel should have address as the station view model after bind", ^{
            [cell bind];
            OCMVerify([chargingStationProtocolMock getAddress]); // Mock
            expect([[cell textLabel] text]).to.equal(@"stub address"); // Stub
        });
    });
```

#### 3.2 Hard path: Dependency Injection

When the request helper method is declared as follows, we can use dependency injection to inject an HTTP client for the test, which will implement the stub logic inside the HTTP client.

````
+ (RACSignal *)getStations:(EtHttpClient *)client parameters:(NSDictionary *)parameters;
````

It is not recommended for two reasons. First of all, we need to create another HTTP client for the test. Secondly, the HTTP client used in the application itself needs to be tested, which means we need to write more test case for the HTTP client.

#### 3.3 Easy path: Libraries

In this way, the HTTP client is the same as what is used in the applcation main target, but the request is intercepted and the response is injected with what we want. There are many ways to realize the implementation, and this is the [Nocilla's way](https://yahooeng.tumblr.com/post/141143817861/using-nsurlprotocol-for-testing) to achieve it.

There are many libs can achieve stubbing a HTTP requests, in the sample project Nocilla is used.

- [Nocilla](https://github.com/luisobo/Nocilla "Nocilla")
- [OHHTTPStubs](https://github.com/AliSoftware/OHHTTPStubs "OHHTTPStubs")

----

## 4. Unit test 

By default, the unit test comes with XCTest. But I prefer BDD test with is more expressive and easier integrated with MVVM. So in the sample project, the following test libs are integrated:

* [OCMock](http://ocmock.org/ "OCMock")
* [Specta](https://github.com/specta/specta "Specta")
* [Expecta](https://github.com/specta/expecta "Expecta")

Ruby On Rails is a web framework that really takes test serious, that's why I would like to adopt Rails structure for iOS unit tests:

* ViewModel - tests for view models
* View - tests for views
* Model - tests for models
* Controller - tests for controllers
* Utils - tests for utils/helpers

But, where is the integration test? For integration test, the the API request should be real rather than stubbed so that we can check whether the api is integrated successfully or not in concrete. I think it is better to put it in UI test so that a visual impression will be presented.

----

## 5. UI test

#### 5.1 XCUITest

As to XCUITest, it is easy to record some actions. There is one more point to pay attention to, the asynchronous request. Under different network conditions, the request will spend different time, this is especially important when we are using UI test as the integration test. We need to consider how long should we wait for the requests and set a timeout value for it.

[XCUITest official document](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/testing_with_xcode/chapters/01-introduction.html#//apple_ref/doc/uid/TP40014132-CH1-SW1 "XCUITest")

#### 5.2 KIF

This library provides more declarative API for UI test, but note that event though KIF is used to test your UI, you need to add it to your Unit Test target, not UI test target.

[Keep It Functional](https://github.com/kif-framework/KIF "KIF")

----

## 6. Code Coverage

If XCTest and XCUITest are used, the Xcode itself already has the Code Coverage Analysis tool integrated. But if using Specta and Expecta, we need have some kinds of third party tools involved.

Tools recommended:

* [Gcovr](http://gcovr.com/ "Gcovr")

----

## 7. Static Analysis

By default, the Xcode comes with analyzer, and we can also use OCLint for Objective-C projects:

* [OCLint](http://oclint.org/ "OCLint")

----

## 8. Continuous Integration

* fastlane - Automated Deployment

CI server choices: 

* Xcode CI server
* jenkins CI server
* Circle/travis CI
