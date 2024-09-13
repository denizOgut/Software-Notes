
# What is Project Reactor?

The Project Reactor is a fourth-generation reactive library, **==based on the Reactive Streams specification==**, for building non-blocking applications on the JVM.

This specification defines a set of standard interfaces that enable asynchronous, non-blocking communication between different systems, ensuring **backpressure** handling—a mechanism to regulate data flow so that a slow consumer does not get overwhelmed by fast producers.

## Reactive Streams Specification

The main Reactive Streams interfaces are:

- ==**Publisher**: Produces values and sends them to subscribers. It could be a stream of data, a file, or an API returning asynchronous data.==
- ==**Subscriber**: Consumes values produced by the `Publisher`.==
- ==**Subscription**: Represents the lifecycle between a `Publisher` and `Subscriber`, allowing control over data requests.==
- ==**Processor**: A hybrid that acts as both a `Subscriber` and `Publisher`, transforming data as it flows through.==

![[Pasted image 20240914005955.png]]

###  Publisher

A Publisher is a provider of a potentially unbounded number of sequenced elements, publishing them according to the demand received from its Subscriber(s).


```java
public interface Publisher<T> {
    public void subscribe(Subscriber<? super T> s);
}
```

### Subscriber

The responsibility of the Subscriber to decide when and how many elements it is able and willing to receive. **==It is recommended that Subscribers request the upper limit of what they are able to process, as requesting only one element at a time results in an inherently inefficient “stop-and-wait” protocol.==**


```Java
public interface Subscriber<T> {
    public void onSubscribe(Subscription s);
    public void onNext(T t);
    public void onError(Throwable t);
    public void onComplete();
}
```

### Subscription

A Subscription represents the unique relationship between a Subscriber and a Publisher. The Subscriber is in control over when elements are requested and when more elements are no longer needed. **==The Subscription must allow the Subscriber to call `Subscription.request` synchronously from within `onNext` or `onSubscribe`.==**

```java
public interface Subscription {
    public void request(long n);
    public void cancel();
}
```

### Processor

A Processor represents a processing stage, which is both a `Subscriber` and a `Publisher` and must obey the contracts of both.

```Java
public interface Processor<T, R> 
           extends Subscriber<T>, Publisher<R> {
}
```

# What is Reactive Programming?

**Reactive programming** is a programming paradigm where the focus is on developing asynchronous and non-blocking applications in an event-driven form. 

Here the code reacts to every event/change that happens. Code becomes cleaner and more maintainable when you use reactive programming.

In reactive programming, you consider everything as asynchronous data streams (or async event streams). These streams could be UI-events, tweets, video streams, data coming from sockets, and so on. Imagine, you have **Observers** assigned to these streams which can react to every event. Then there are magic functions to Filter, Combine, or even to report an error when it happens.

In Reactive Programming, this is what is known as **Observable** sequences. A function can subscribe to these Observables to receive asynchronous data whenever one arrives and they are **Subscribers**. Reactive programming is the **Observer Design Pattern** used in a slightly different way.

A **`Publisher`** can push new values to its **`Subscriber`** (by calling `onNext`). It can also signal an error (by calling `onError`) or completion (by calling `onComplete`). Both errors and completion terminate the sequence.


> Many says, Reactive concepts for programming is what Henry Ford’s assembly line was to cars.

## What is a Stream?

A stream is considered as a sequence of data or events ordered in time, example – tweets, mouse events, socket data. **==These streams can emit 3 things, a value, an error (whenever anything goes wrong), or a completed signal. The completed signal indicates that the stream is closed.==**

> In reactive concept, call a stream as **Observable**.


