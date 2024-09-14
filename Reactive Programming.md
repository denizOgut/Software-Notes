
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


# ``Mono``

**Mono** is one of the two main types of publishers in **Project Reactor** (the other being **Flux**). It represents an **asynchronous computation that can emit at most a single value**, or **complete empty**, or **signal an error**. If you're familiar with concepts like `Optional` or `CompletableFuture` in Java, Mono is somewhat similar but adapted for asynchronous, reactive streams.

 **Core Characteristics of Mono**

- ==**Single Value or No Value**: Unlike `Flux` which can emit multiple values over time, `Mono` emits at most **one** value.==
- ==**Lazy Evaluation**: The computation encapsulated within a Mono does not start until someone subscribes to it. This supports **lazy evaluation**, ensuring no resource is used until necessary.==
- ==**Non-blocking**: Mono is inherently asynchronous and does not block the calling thread while waiting for the result.==

## **Use Cases of Mono**

1. **Handling Single Asynchronous Tasks**: Mono is ideal for situations where a single asynchronous response is expected, such as:
    
    - Fetching a single record from a database.
    - Making a REST API call and receiving a response.
    - Performing file I/O for a single file.
2. **Return Type for Asynchronous Methods**: Methods that return a single value but execute asynchronously should use `Mono` as the return type.
    
3. **Error Handling in Asynchronous Code**: Mono allows graceful handling of errors in a non-blocking environment, where fallback mechanisms can be implemented.

```Java
package reactor.core.publisher;

public abstract class Mono<T> 
        implements CorePublisher<T> {
  public static <T> Mono<T> create(Consumer<MonoSink<T>> callback) {..}
  public static <T> Mono<T> empty() {..}
  public static <T> Mono<T> error(Throwable error) {..}
  public static <T> Mono<T> just(T data) {..}
...
}
```

```Java
package reactor.core;

import org.reactivestreams.Publisher;
import org.reactivestreams.Subscriber;

public interface CorePublisher<T> extends Publisher<T> {
	void subscribe(CoreSubscriber<? super T> subscriber);
}
```

```Java
package org.reactivestreams;

public interface Publisher<T> {
    public void subscribe(Subscriber<? super T> s);
}
```

![[Pasted image 20240914111411.png]]

Here’s a detailed list of the most important `Mono` methods you asked about, organized with explanations and examples for each:

## Most Common ``Mono`` Methods
---

### **1. `Mono.just(T data)`**
Creates a `Mono` that **emits a single value** and completes.
- **Use Case**: When you have a fixed value that you want to emit.
  
**Example**:
```java
Mono<String> mono = Mono.just("Hello, Mono!");
mono.subscribe(System.out::println);
```
- Output: `Hello, Mono!`

---

### **2. `Mono.subscribe()`**
This method is used to **consume the value** or handle the result of a `Mono`. It triggers the execution of the `Mono` pipeline.

- **Overloads**:
  - **Basic subscribe**: For consuming emitted data.
    ```java
    Mono.just("Data").subscribe(data -> System.out.println("Received: " + data));
    ```
  - **With error handler**: For handling errors.
    ```java
    Mono.error(new RuntimeException("Error"))
        .subscribe(data -> System.out.println(data), 
                   error -> System.err.println("Error: " + error.getMessage()));
    ```
  - **With completion handler**: Handles normal data, errors, and completion events.
    ```java
    Mono.just("Complete")
        .subscribe(data -> System.out.println("Data: " + data),
                   error -> System.err.println(error),
                   () -> System.out.println("Completed"));
    ```

---

### **3. `Mono.empty()`**
Creates a `Mono` that completes **without emitting any value**.
- **Use Case**: When you want to indicate the absence of a value (like `Optional.empty()`).
  
**Example**:
```java
Mono<Void> emptyMono = Mono.empty();
emptyMono.subscribe(
    unused -> System.out.println("Value"), 
    error -> System.out.println("Error"), 
    () -> System.out.println("Completed without data")
);
```
- Output: `Completed without data`

---

### **4. `Mono.error(Throwable error)`**
Creates a `Mono` that **terminates with an error**.
- **Use Case**: To represent failure scenarios or simulate errors.

**Example**:
```java
Mono<String> errorMono = Mono.error(new RuntimeException("Something went wrong!"));
errorMono.subscribe(
    System.out::println, 
    error -> System.out.println("Error: " + error.getMessage())
);
```
- Output: `Error: Something went wrong!`

---

### **5. `Mono.fromSupplier(Supplier<? extends T> supplier)`**
Creates a `Mono` from a **supplier function** that is called each time the `Mono` is subscribed to.
- **Use Case**: Useful when you want to lazily fetch a value upon subscription.

**Example**:
```java
Mono<String> fromSupplierMono = Mono.fromSupplier(() -> "Supplied value");
fromSupplierMono.subscribe(System.out::println);
```
- Output: `Supplied value`

---

### **6. `Mono.fromCallable(Callable<? extends T> callable)`**
Creates a `Mono` that emits the value returned by a **`Callable`**, which is invoked lazily.
- **Use Case**: For wrapping blocking operations or computations inside a non-blocking `Mono`.

**Example**:
```java
Mono<String> fromCallableMono = Mono.fromCallable(() -> {
    return "Result from callable";
});
fromCallableMono.subscribe(System.out::println);
```
- Output: `Result from callable`

---

### **7. `Mono.fromRunnable(Runnable runnable)`**
Creates a `Mono` that executes the **provided `Runnable`** and completes after running.
- **Use Case**: If you want to trigger an action (like logging or side effects) and don’t need to return a value.

**Example**:
```java
Mono<Void> runnableMono = Mono.fromRunnable(() -> System.out.println("Running a task"));
runnableMono.subscribe(
    unused -> {}, 
    error -> System.err.println(error),
    () -> System.out.println("Completed runnable")
);
```
- Output:
  ```
  Running a task
  Completed runnable
  ```

---

### **8. `Mono.fromFuture(CompletableFuture<? extends T> future)`**
Creates a `Mono` that completes when the provided **`CompletableFuture`** completes, emitting its result.
- **Use Case**: When you want to integrate `CompletableFuture` with `Mono`.

**Example**:
```java
CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> "Future result");
Mono<String> futureMono = Mono.fromFuture(future);
futureMono.subscribe(System.out::println);
```
- Output: `Future result`

---

### **9. `Mono.create()`**
This method allows you to **create a `Mono` in an imperative way**, by providing a `MonoSink` that lets you signal a value, error, or completion.
- **Use Case**: For more advanced and flexible scenarios where you need to explicitly control the emission.

**Example**:
```java
Mono<String> createdMono = Mono.create(sink -> sink.success("Created value"));
createdMono.subscribe(System.out::println);
```
- Output: `Created value`

---

### **10. `Mono.defer(Supplier<? extends Mono<? extends T>> supplier)`**
Creates a `Mono` lazily from a supplier of another `Mono`. It **delays the creation of the `Mono`** until subscription.
- **Use Case**: Useful when you need the `Mono` to be generated lazily, and not just executed lazily.

**Example**:
```java
Mono<String> deferredMono = Mono.defer(() -> {
    return Mono.just("Deferred value");
});
deferredMono.subscribe(System.out::println);
```
- Output: `Deferred value`

---

### **11. `Mono.create()` vs. `Mono.fromRunnable()`, `Mono.fromCallable()`, and `Mono.fromSupplier()`**

These methods have different purposes:
- **`Mono.create()`**: Provides fine-grained control via `MonoSink` for emitting values, errors, or completions. It is more flexible and is often used in scenarios like bridging APIs, converting callbacks into reactive types, or when you need to handle the emission imperatively.
  
- **`Mono.fromSupplier()`**: Wraps a `Supplier` function that is called lazily when the `Mono` is subscribed to. It is suitable for synchronous logic and does not expect errors.

- **`Mono.fromCallable()`**: Wraps a `Callable` that returns a value or throws an exception. This is typically used when the supplier can throw checked exceptions.

- **`Mono.fromRunnable()`**: Executes a `Runnable` that doesn't emit any value. It only signals completion after the `Runnable` finishes.

**Example: `Mono.create()` vs `Mono.fromRunnable()`**
```java
Mono<String> createdMono = Mono.create(sink -> {
    sink.success("Created Mono");
});

Mono<Void> runnableMono = Mono.fromRunnable(() -> System.out.println("Running task"));

createdMono.subscribe(System.out::println);
runnableMono.subscribe();
```

**Differences**:
- `Mono.create()` is designed for more complex scenarios where you need to manually control what and when to emit.
- `Mono.fromRunnable()` simply executes a `Runnable` and completes without emitting a value.

---

### **12. `Mono.execute()`**
Similar to `Mono.create()`, but less commonly used. It provides access to `MonoSink` and is used for imperative control over the emission of data.

---

### **Summary**

- **``Mono.just(T data)``**: Emits a single value.
- **``Mono.subscribe()``**: Triggers the Mono and consumes its result.
- **``Mono.empty()``**: Emits nothing, just completes.
- **``Mono.error(Throwable error)``**: Emits an error signal.
- **``Mono.fromSupplier(Supplier<T> supplier)``**: Lazily emits a value from a `Supplier`.
- **``Mono.fromCallable(Callable<T> callable)``**: Lazily emits a value or error from a `Callable`.
- **``Mono.fromRunnable(Runnable runnable)``**: Runs a `Runnable` and completes without emitting a value.
- **``Mono.fromFuture(CompletableFuture<T> future)``**: Emits the result of a `CompletableFuture`.
- **``Mono.create()``**: Offers manual control over emissions via `MonoSink`.
- **``Mono.defer(Supplier<Mono<T>> supplier)``**: Lazily creates and subscribes to a `Mono`.

```java
import reactor.core.publisher.Mono;

import java.util.concurrent.CompletableFuture;

public class UserService {

    public static void main(String[] args) {
        // Fetch user from the database (asynchronously)
        Mono<String> userMono = fetchUserFromDatabase("user123");

        // Process the user's order
        Mono<String> orderMono = userMono
                .flatMap(user -> processOrder(user))  // Processing order after fetching the user
                .doOnNext(order -> logOrderProcess()) // Logging the order processing
                .onErrorResume(e -> Mono.just("Fallback order")); // Fallback in case of error

        // Subscribe and print the result
        orderMono.subscribe(
            result -> System.out.println("Order Result: " + result),
            error -> System.err.println("Error: " + error.getMessage()),
            () -> System.out.println("Process completed successfully!")
        );
    }

    // Simulate fetching a user from a database
    public static Mono<String> fetchUserFromDatabase(String userId) {
        return Mono.fromCallable(() -> {
            if ("user123".equals(userId)) {
                return "User123";
            } else {
                throw new RuntimeException("User not found!");
            }
        });
    }

    // Simulate processing an order for the user
    public static Mono<String> processOrder(String user) {
        return Mono.fromFuture(processOrderAsync(user));
    }

    // Simulate an asynchronous order processing
    public static CompletableFuture<String> processOrderAsync(String user) {
        return CompletableFuture.supplyAsync(() -> "Order processed for " + user);
    }

    // Simulate logging the order process
    public static void logOrderProcess() {
        Mono.fromRunnable(() -> System.out.println("Order is being processed..."))
            .subscribe();
    }
}
```

```output
Order is being processed...
Order Result: Order processed for User123
Process completed successfully!
```


# ``Flux`` 

`Flux<T>` is a reactive type from the **Project Reactor** library that represents **a sequence of 0 to N items**. Unlike `Mono`, which emits either a single value or no value, `Flux` can emit multiple values, including **zero, one, many, or an infinite number of elements**. It can also terminate either successfully or with an error.

`Flux` is analogous to a **Publisher** in the **Reactive Streams specification**, providing a non-blocking, asynchronous way to handle data streams.

 **Key Characteristics of `Flux`:**

- ==**0 to N values**: Can emit zero, one, or more items.==
- ==**Asynchronous**: Handles data streams asynchronously, which is key for non-blocking, reactive applications.==
- ==**Reactive Backpressure**: Supports backpressure, allowing consumers to control the rate at which they receive items.==
- ==**Termination**: Like `Mono`, `Flux` can either complete successfully or terminate with an error.==

 **When to Use `Flux`?**

- When you need to handle a stream of multiple values (e.g., querying a database and returning a collection, processing a stream of events).
- When dealing with infinite streams or sequences of events (e.g., WebSocket streams, continuous sensor data).
- For handling collections or batches of data in a non-blocking, reactive manner.

 **Real-Life Use Cases for `Flux`**

1. **Stream Data from a Database**: If you’re querying a database and need to return multiple records, you can use `Flux` to represent the result stream. This can be combined with `flatMap` to handle asynchronous processing.
    
2. **Processing Collections**: If you have a list of items and need to process each item asynchronously, `Flux.fromIterable()` can be used to emit the items and process them in a reactive manner.
    
3. **Streaming Data over WebSockets**: When dealing with continuous streams of data (e.g., from WebSockets, IoT sensors), `Flux` is ideal for handling the infinite or unbounded stream of data.
    
4. **Batch Processing**: For scenarios where you need to batch process items, `Flux` can emit batches of data, allowing you to handle them reactively.



```Java
public abstract class Flux<T> implements CorePublisher<T> {

    public static <T> Flux<T> create(Consumer<? super FluxSink<T>> emitter, OverflowStrategy 
    backpressure) {..}
    public static <T> Flux<T> empty() {..}
    public static <T> Flux<T> error(Throwable error) {..}
    public static <T> Flux<T> from(Publisher<? extends T> source) {..}
    public static Flux<Long> interval(Duration period) {..}
    public static <T> Flux<T> just(T... data) {..}
    ..
}
```

```Java
package reactor.core;
import org.reactivestreams.Publisher;
import org.reactivestreams.Subscriber;

public interface CorePublisher<T> extends Publisher<T> {
  void subscribe(CoreSubscriber<? super T> subscriber);
}
```

```Java
package org.reactivestreams;

public interface Publisher<T> {
    public void subscribe(Subscriber<? super T> s);
}
```

![[Pasted image 20240914113904.png]]


Here’s a detailed explanation of the most important `Flux` methods you requested, in the given order:

## Most Common ``Flux`` Methods
---
### 1. **`Flux.just()`**
Creates a `Flux` that emits a fixed sequence of values and then completes. It’s commonly used to create a sequence from known values.

**Example**:
```java
Flux<String> flux = Flux.just("A", "B", "C");
flux.subscribe(System.out::println);
```
**Output**:
```
A
B
C
```

### 2. **`Flux` with Multiple Subscribers**
You can have multiple subscribers for a single `Flux`. Each subscriber will receive the sequence of values independently unless you share state using operators like `publish()`.

**Example**:
```java
Flux<String> flux = Flux.just("A", "B", "C");

// First subscriber
flux.subscribe(item -> System.out.println("Subscriber 1: " + item));

// Second subscriber
flux.subscribe(item -> System.out.println("Subscriber 2: " + item));
```
**Output**:
```
Subscriber 1: A
Subscriber 1: B
Subscriber 1: C
Subscriber 2: A
Subscriber 2: B
Subscriber 2: C
```

### 3. **`Flux.fromArray()` / `Flux.fromIterable()`**
You can create a `Flux` from an array, list, or any iterable source.

- **From an Array**:
  ```java
  String[] array = {"A", "B", "C"};
  Flux<String> flux = Flux.fromArray(array);
  flux.subscribe(System.out::println);
  ```

- **From a List**:
  ```java
  List<String> list = Arrays.asList("A", "B", "C");
  Flux<String> flux = Flux.fromIterable(list);
  flux.subscribe(System.out::println);
  ```

Both examples output:
```
A
B
C
```

### 4. **`Flux.fromStream()`**
You can create a `Flux` from a Java stream, allowing you to process streams reactively.

**Example**:
```java
Flux<Integer> flux = Flux.fromStream(Stream.of(1, 2, 3, 4, 5));
flux.subscribe(System.out::println);
```
**Output**:
```
1
2
3
4
5
```

### 5. **`Flux.range()`**
This method creates a `Flux` that emits a range of integers. It’s particularly useful for looping through a range reactively.

**Example**:
```java
Flux<Integer> flux = Flux.range(1, 5);
flux.subscribe(System.out::println);
```
**Output**:
```
1
2
3
4
5
```

### 6. **`log()` Operator**
The `log()` operator logs the lifecycle events of the `Flux`. It is helpful for debugging and understanding the flow of the reactive sequence.

**Example**:
```java
Flux<String> flux = Flux.just("A", "B", "C")
    .log();  // Log all events
flux.subscribe(System.out::println);
```
**Output**:
```
[main] | onSubscribe(...)
[main] | request(unbounded)
[main] | onNext(A)
A
[main] | onNext(B)
B
[main] | onNext(C)
C
[main] | onComplete()
```

### 7. **`Flux.interval()`**
Creates an infinite `Flux` that emits long values at a fixed time interval. This is often used for generating periodic events.

**Example**:
```java
Flux<Long> flux = Flux.interval(Duration.ofSeconds(1));
flux.subscribe(System.out::println);

// This will keep emitting values every second until the application is stopped.
```

**Output (1 value per second)**:
```
0
1
2
3
...
```

### 8. **`Flux.empty()` / `Flux.error()`**
- **`Flux.empty()`**: Creates a `Flux` that emits no items but terminates normally.
  ```java
  Flux<String> flux = Flux.empty();
  flux.subscribe(
      System.out::println,
      error -> System.out.println("Error: " + error),
      () -> System.out.println("Completed!")
  );
  ```

  **Output**:
  ```
  Completed!
  ```

- **`Flux.error()`**: Creates a `Flux` that terminates with an error immediately.
  ```java
  Flux<String> flux = Flux.error(new RuntimeException("Something went wrong!"));
  flux.subscribe(
      System.out::println,
      error -> System.out.println("Error: " + error.getMessage())
  );
  ```

  **Output**:
  ```
  Error: Something went wrong!
  ```

### 9. **`Flux.defer()`**
`defer()` is used to ensure that the `Flux` is created lazily, at the moment of subscription, rather than at the moment of creation. This is useful when you want to defer the creation of the sequence until the point of subscription.

**Example**:
```java
Flux<String> flux = Flux.defer(() -> Flux.just("Deferred A", "Deferred B"));
flux.subscribe(System.out::println);
```

**Output**:
```
Deferred A
Deferred B
```

### **Summary of Key Methods**:
- **`Flux.just()`**: Emits a predefined sequence of values.
- **Multiple Subscribers**: Allows multiple subscribers to a `Flux`.
- **`Flux.fromArray()` / `Flux.fromIterable()`**: Create `Flux` from arrays or iterables.
- **`Flux.fromStream()`**: Create `Flux` from a Java stream.
- **`Flux.range()`**: Emit a sequence of integers.
- **`log()`**: Logs events in the `Flux` lifecycle.
- **`Flux.interval()`**: Emits values at regular time intervals.
- **`Flux.empty()` / `Flux.error()`**: Create `Flux` that either emits no values or emits an error.
- **`Flux.defer()`**: Lazily creates the `Flux` at subscription time. 

```java
import reactor.core.publisher.Flux;
import reactor.core.publisher.Mono;

import java.time.Duration;
import java.util.Arrays;
import java.util.List;
import java.util.concurrent.atomic.AtomicInteger;
import java.util.stream.Stream;

public class FluxExample {

    public static void main(String[] args) throws InterruptedException {
        // Flux.just() - Simulating a batch of orders to process
        Flux<String> orders = Flux.just("Order1", "Order2", "Order3");

        // Flux.fromIterable() - List of delivery zones for the orders
        List<String> zones = Arrays.asList("ZoneA", "ZoneB", "ZoneC");
        Flux<String> deliveryZones = Flux.fromIterable(zones);

        // Flux.fromStream() - Stream of delivery agents
        Stream<String> agentsStream = Stream.of("Agent1", "Agent2", "Agent3");
        Flux<String> deliveryAgents = Flux.fromStream(agentsStream);

        // Flux.range() - Simulating order numbers
        Flux<Integer> orderNumbers = Flux.range(1, 3);

        // Flux.defer() - Lazily create a new flux for order tracking status (i.e., it changes every time you subscribe)
        Flux<String> orderTrackingStatus = Flux.defer(() -> {
            String status = Math.random() > 0.5 ? "Shipped" : "Processing";
            return Flux.just(status);
        });

        // Flux.interval() - Emulate real-time tracking update every second
        Flux<Long> trackingUpdates = Flux.interval(Duration.ofSeconds(1));

        // Flux.empty() - When no orders are found, return an empty flux
        Flux<String> noOrders = Flux.empty();

        // Flux.error() - If any error occurs in the system, handle it with a fallback
        Flux<String> errorFallback = Flux.error(new RuntimeException("System error occurred!"));

        // log() - For debugging purposes, log all the operations on the flux
        orders.log()
                // Combine with order numbers
                .zipWith(orderNumbers, (order, number) -> "Order #" + number + ": " + order)
                // Simulate processing time by delaying each element by 1 second
                .delayElements(Duration.ofSeconds(1))
                // Combine with delivery zones
                .zipWith(deliveryZones, (orderWithNumber, zone) -> orderWithNumber + " to " + zone)
                // Combine with delivery agents
                .zipWith(deliveryAgents, (orderWithZone, agent) -> orderWithZone + " by " + agent)
                // Defer order tracking status lazily
                .flatMap(order -> orderTrackingStatus.map(status -> order + " - Status: " + status))
                // Log the tracking status every second (simulating a real-time process)
                .flatMap(orderStatus -> trackingUpdates.map(tick -> orderStatus + " (Update " + tick + ")").take(3))
                // Subscribe with multiple subscribers
                .subscribe(
                        data -> System.out.println("Subscriber 1: " + data),
                        error -> System.err.println("Subscriber 1: Error - " + error.getMessage()),
                        () -> System.out.println("Subscriber 1: Completed!")
                );

        orders.log()
                .subscribe(
                        data -> System.out.println("Subscriber 2: " + data),
                        error -> System.err.println("Subscriber 2: Error - " + error.getMessage()),
                        () -> System.out.println("Subscriber 2: Completed!")
                );

        // Allow interval to emit values
        Thread.sleep(10000);
    }
}
```

## `FluxSink`

`FluxSink` is a handle used within `Flux.create()` to programmatically emit items into a `Flux`. It provides methods to:

- **`next(T value)`**: Emit an item to the `Flux`.
- **`error(Throwable error)`**: Signal an error to the subscribers.
- **`complete()`**: Signal that the sequence is complete.

It allows you to manually control the emission and lifecycle of the `Flux` from within a custom source or generator.
### **1. `FluxSink` and `Flux.create()`**

- **`Flux.create(FluxSink<T> sinkConsumer)`**: This method creates a `Flux` using a `FluxSink` that allows you to manually push items into the `Flux` from a custom source. This is useful when you need to control how items are emitted to subscribers or when integrating with external systems or APIs.

  **Example**:
  ```java
  Flux<String> flux = Flux.create(sink -> {
      sink.next("Hello");
      sink.next("World");
      sink.complete(); // Mark the end of the sequence
  });

  flux.subscribe(System.out::println);
  ```
  **Output**:
  ```
  Hello
  World
  ```

- **`FluxSink`**: Represents a handle to the underlying `Flux` which allows you to emit items, signal completion, or errors. It’s typically used within the lambda function of `Flux.create`.

  **Important Methods**:
  - **`next(T value)`**: Emits an item to the `Flux`.
  - **`error(Throwable error)`**: Signals an error.
  - **`complete()`**: Signals that the sequence has completed.

### **2. `FluxSink` Use Cases**

- **Manual Control**: Allows you to manually control the emission of items, such as pushing data from a source that doesn’t natively support reactive streams.
- **External Integration**: Useful when integrating with libraries or APIs that don’t provide a reactive API but need to be adapted to reactive streams.
- **Custom Emit Logic**: When you need custom logic to decide when and how to emit items, such as batching or complex data sources.

### **3. `take(n)` Operator**

- **`take(long n)`**: Limits the number of items emitted by the `Flux` to `n` items. It’s useful for scenarios where you only need a subset of items from the sequence.

  **Example**:
  ```java
  Flux<Integer> flux = Flux.range(1, 10)
      .take(5);
  flux.subscribe(System.out::println);
  ```
  **Output**:
  ```
  1
  2
  3
  4
  5
  ```

### **4. `Flux.generate()`**

- **`Flux.generate(Generator<T> generator)`**: Creates a `Flux` using a generator function that produces items and can maintain state across emissions. The generator function receives a `SynchronousSink` to emit items and maintain state.

  **Example**:
  ```java
  Flux<Integer> flux = Flux.generate(
      () -> 1, // Initial state
      (state, sink) -> {
          if (state > 10) {
              sink.complete(); // Complete the sequence when state exceeds 10
          } else {
              sink.next(state); // Emit current state
              return state + 1; // Update state
          }
          return state;
      }
  );

  flux.subscribe(System.out::println);
  ```
  **Output**:
  ```
  1
  2
  3
  4
  5
  6
  7
  8
  9
  10
  ```

### **5. `Flux.generate` - Emit Until**

- **`Flux.generate(Generator<T> generator, Consumer<SynchronousSink<T>> emitter)`**: Allows more fine-grained control over the emission process. You can emit items until a certain condition is met or based on custom logic.

  **Example**:
  ```java
  Flux<Integer> flux = Flux.generate(
      () -> 1, // Initial state
      (state, sink) -> {
          if (state > 10) {
              sink.complete(); // Complete when state exceeds 10
          } else {
              sink.next(state); // Emit the current state
              return state + 2; // Increment state by 2
          }
          return state;
      }
  );

  flux.subscribe(System.out::println);
  ```
  **Output**:
  ```
  1
  3
  5
  7
  9
  ```

### **6. `Flux.generate` - State Problem**

- **State Problem**: In `Flux.generate()`, if the state is not correctly managed or updated, it can lead to issues such as infinite loops or incorrect sequence of items.

  **Example of a State Problem**:
  ```java
  Flux<Integer> flux = Flux.generate(
      () -> 1, // Initial state
      (state, sink) -> {
          sink.next(state); // Emit current state
          // Mistake: Not updating state properly or terminating
          return state; // Causes infinite loop if not properly managed
      }
  );

  flux.subscribe(System.out::println);
  ```
  **Output**:
  ```
  1
  1
  1
  1
  ...
  ```

### **7. `Flux.generate` - State Supplier**

- **State Supplier**: When using `Flux.generate()`, you can use a state supplier to initialize the state and a generator to handle the emission and state update.

  **Example**:
  ```java
  Flux<Integer> flux = Flux.generate(
      () -> 1, // State supplier: initial state
      (state, sink) -> {
          if (state > 10) {
              sink.complete(); // Complete when state exceeds 10
          } else {
              sink.next(state); // Emit the current state
              return state + 1; // Update state
          }
          return state;
      }
  );

  flux.subscribe(System.out::println);
  ```
  **Output**:
  ```
  1
  2
  3
  4
  5
  6
  7
  8
  9
  10
  ```

### **Summary**

- **`Flux.create(FluxSink<T> sinkConsumer)`**: Manually create a `Flux` and control emissions.
- **`FluxSink`**: Used within `Flux.create` to emit items, errors, or completion signals.
- **`take(n)`**: Limits the number of items emitted by the `Flux`.
- **`Flux.generate()`**: Generates a `Flux` with stateful emission.
- **`Flux.generate` - Emit Until**: Generates items until a certain condition is met.
- **`Flux.generate` - State Problem**: Issues that arise from improper state management in `Flux.generate`.
- **`Flux.generate` - State Supplier**: Initializing state in `Flux.generate()` using a state supplier.

These methods provide powerful tools for creating and managing reactive streams, allowing fine-grained control over item emission and state management in reactive applications.

# Operators

Here's a detailed overview of some key operators in Project Reactor that you might find useful for transforming and working with reactive streams in Java:

## **Transforming Operators**

1. **`map(Function<? super T, ? extends R> mapper)`**

![[Pasted image 20240914124026.png]]
   - Transforms each item emitted by the source `Flux` by applying a function to it.
   - **Example**:
     ```java
     Flux<Integer> flux = Flux.just(1, 2, 3)
         .map(i -> i * 2);
     flux.subscribe(System.out::println);
     // Output: 2, 4, 6
     ```

2. **`flatMap(Function<? super T, ? extends Publisher<? extends R>> mapper)`**

![[Pasted image 20240914124044.png]]

   - Transforms each item emitted by the source `Flux` into a `Publisher`, then flattens the resulting `Publisher` sequences into a single `Flux`.
   - **Example**:
     ```java
     Flux<String> flux = Flux.just("A", "B", "C")
         .flatMap(s -> Flux.just(s + "1", s + "2"));
     flux.subscribe(System.out::println);
     // Output: A1, A2, B1, B2, C1, C2
     ```

3. **`filter(Predicate<? super T> predicate)`**
   - Filters items emitted by the source `Flux` based on a predicate.
   - **Example**:
     ```java
     Flux<Integer> flux = Flux.just(1, 2, 3, 4, 5)
         .filter(i -> i % 2 == 0);
     flux.subscribe(System.out::println);
     // Output: 2, 4
     ```

4. **`distinct()`**
   - Emits only distinct items from the source `Flux`, removing duplicates.
   - **Example**:
     ```java
     Flux<Integer> flux = Flux.just(1, 2, 2, 3, 4, 4, 5)
         .distinct();
     flux.subscribe(System.out::println);
     // Output: 1, 2, 3, 4, 5
     ```

5. **`concatMap(Function<? super T, ? extends Publisher<? extends R>> mapper)`**
   - Similar to `flatMap`, but preserves the order of items. Each item is mapped to a `Publisher`, and the publishers are concatenated in sequence.
   - **Example**:
     ```java
     Flux<String> flux = Flux.just("A", "B", "C")
         .concatMap(s -> Flux.just(s + "1", s + "2"));
     flux.subscribe(System.out::println);
     // Output: A1, A2, B1, B2, C1, C2
     ```

## **Combining Operators**

6. **`mergeWith(Publisher<? extends T> other)`**
![[Pasted image 20240914124152.png]]
   - Merges the items emitted by the source `Flux` with those from another `Publisher`.
   - **Example**:
     ```java
     Flux<Integer> flux1 = Flux.just(1, 2);
     Flux<Integer> flux2 = Flux.just(3, 4);
     Flux<Integer> mergedFlux = flux1.mergeWith(flux2);
     mergedFlux.subscribe(System.out::println);
     // Output: 1, 2, 3, 4
     ```

7. **`zipWith(Publisher<? extends T2> other)`**

![[Pasted image 20240914124542.png]]

   - Combines items from the source `Flux` and another `Publisher` into pairs.
   - **Example**:
     ```java
     Flux<String> flux1 = Flux.just("A", "B", "C");
     Flux<Integer> flux2 = Flux.just(1, 2, 3);
     Flux<Tuple2<String, Integer>> zippedFlux = flux1.zipWith(flux2);
     zippedFlux.subscribe(System.out::println);
     // Output: (A,1), (B,2), (C,3)
     ```

8. **`combineLatest(Publisher<? extends T2> other, BiFunction<? super T, ? super T2, ? extends R> combinator)`**
   - Combines the latest items emitted by the source `Flux` and another `Publisher` using a combinator function.
   - **Example**:
     ```java
     Flux<String> flux1 = Flux.just("A", "B");
     Flux<Integer> flux2 = Flux.just(1, 2, 3);
     Flux<String> combinedFlux = flux1.combineLatest(flux2, (s, i) -> s + i);
     combinedFlux.subscribe(System.out::println);
     // Output: B3 (last elements of flux1 and flux2 combined)
     ```

9. **`concat(Publisher<? extends T>... sources)`**

![[Pasted image 20240914124954.png]]

   - Combines multiple `Publisher` instances into a single `Flux`, emitting items sequentially from each source in the order provided.
   - **Example**:
     ```java
     Flux<Integer> flux1 = Flux.just(1, 2);
     Flux<Integer> flux2 = Flux.just(3, 4);
     Flux<Integer> flux3 = Flux.just(5, 6);
     Flux<Integer> concatenatedFlux = Flux.concat(flux1, flux2, flux3);
     concatenatedFlux.subscribe(System.out::println);
     // Output: 1, 2, 3, 4, 5, 6
     ```
## **Utility Operators**

10. **`doOnNext(Consumer<? super T> consumer)`**
   - Performs a side effect whenever an item is emitted.
   - **Example**:
     ```java
     Flux<Integer> flux = Flux.just(1, 2, 3)
         .doOnNext(i -> System.out.println("Processing: " + i));
     flux.subscribe(System.out::println);
     // Output: Processing: 1
     //         Processing: 2
     //         Processing: 3
     //         1
     //         2
     //         3
     ```

11. **`onErrorResume(Function<Throwable, ? extends Publisher<? extends T>> fallback)`**
    - Provides a fallback `Publisher` if an error occurs.
    - **Example**:
      ```java
      Flux<Integer> flux = Flux.just(1, 2)
          .concatWith(Flux.error(new RuntimeException("Error!")))
          .onErrorResume(e -> Flux.just(10, 20));
      flux.subscribe(System.out::println);
      // Output: 1
      //         2
      //         10
      //         20
      ```

12. **`retry(long maxRetries)`**
    - Retries the sequence upon encountering an error, up to a specified number of times.
    - **Example**:
      ```java
      Flux<Integer> flux = Flux.concat(
          Flux.just(1, 2),
          Flux.error(new RuntimeException("Error!")),
          Flux.just(3)
      ).retry(1); // Retry once upon error
      flux.subscribe(System.out::println);
      // Output: 1
      //         2
      //         1
      //         2
      //         3
      ```

## **Termination Operators**

13. **`collectList()`**
    - Collects all emitted items into a `List` and returns a `Mono` with that list.
    - **Example**:
      ```java
      Flux<Integer> flux = Flux.just(1, 2, 3);
      Mono<List<Integer>> mono = flux.collectList();
      mono.subscribe(System.out::println);
      // Output: [1, 2, 3]
      ```

14. **`then(Mono<?> other)`**
    - Discards the items from the source `Flux` and only emits items from the `Mono` that follows.
    - **Example**:
      ```java
      Flux<Integer> flux = Flux.just(1, 2, 3);
      Mono<String> mono = Mono.just("Done");
      flux.then(mono).subscribe(System.out::println);
      // Output: Done
      ```

## **Other Operators**

15. **`flatMapSequential(Function<? super T, ? extends Publisher<? extends R>> mapper)`**
    - Similar to `flatMap`, but maintains the order of items in the original `Flux`.
    - **Example**:
      ```java
      Flux<String> flux = Flux.just("A", "B", "C")
          .flatMapSequential(s -> Flux.just(s + "1", s + "2"));
      flux.subscribe(System.out::println);
      // Output: A1
      //         A2
      //         B1
      //         B2
      //         C1
      //         C2
      ```

16. **`buffer(int bufferSize)`**
    - Collects items into a buffer of a specified size and emits the buffer as a `List`.
    - **Example**:
      ```java
      Flux<Integer> flux = Flux.range(1, 10)
          .buffer(3);
      flux.subscribe(System.out::println);
      // Output: [1, 2, 3]
      //         [4, 5, 6]
      //         [7, 8, 9]
      //         [10]
      ```

These operators allow you to manipulate and process reactive streams in various ways, providing powerful tools for handling asynchronous data in a reactive programming paradigm.

# Hot  & Cold Publishers

have 2 different types of implementations for the Publisher interface.

- Flux
- Mono

Both emit elements asynchronously. While _**Flux**_ can emit 0 . . . N elements, _**Mono**_ can emit 0 or 1 element.

Based on the their emission behavior, We can categorize the publishers into 2 types.

- Hot
- Cold

## **Reactor Cold Publisher:**

**==Publishers by default do not produce any value unless at least 1 observer subscribes to it. Publishers create new data producers for each new subscription.==**

- **Definition**: A cold publisher produces data only when there is at least one subscriber. Each subscriber gets its own independent stream of data from the beginning.
    
- **Behavior**: Every time a subscriber subscribes to a cold publisher, the publisher starts emitting data from the start of the sequence for that subscriber.
    
- **Example**: `Flux` created using `Flux.range(1, 5)` is cold. Each subscription will receive the full range of values from 1 to 5.

```java
Flux<Integer> coldFlux = Flux.range(1, 5);

coldFlux.subscribe(value -> System.out.println("Subscriber 1: " + value));
// Output: Subscriber 1: 1, 2, 3, 4, 5

coldFlux.subscribe(value -> System.out.println("Subscriber 2: " + value));
// Output: Subscriber 2: 1, 2, 3, 4, 5
```

---

```java
private int getDataToBePublished(){
    System.out.println("getDataToBePublished was called");
    return 1;
}
```

Lets assume that we would be emitting the element using Mono as shown here.

```java
Mono.fromSupplier(() -> getDataToBePublished());
```

Now what does the above code do? The above code would not print any value as there is nobody to observe it. We need at least 1 observer. The below code produces the below output as we have 1 observer.

```java
Mono.fromSupplier(() -> getDataToBePublished())
        .subscribe(i -> System.out.println("Observer-1 :: " + i));

//Output
getDataToBePublished was called
Observer-1 :: 1
```

Lets consider this method which is going to stream a movie for us.

```java
private Stream<String> getMovie(){
    System.out.println("Got the movie streaming request");
    return Stream.of(
            "scene 1",
            "scene 2",
            "scene 3",
            "scene 4",
            "scene 5"
    );
}
```

Out NetFlux app implementation is as shown here.

```java
//our NetFlux streamer
//each scene will play for 2 seconds
Flux<String> netFlux = Flux.fromStream(() -> getMovie())
                            .delayElements(Duration.ofSeconds(2));

// you start watching the movie
netFlux.subscribe(scene -> System.out.println("You are watching " + scene));

//I join after sometime
Thread.sleep(5000);
netFlux.subscribe(scene -> System.out.println("Vinsguru is watching " + scene));
```

Output:

```bash
Got the movie streaming request
You are watching scene 1
You are watching scene 2
Got the movie streaming request
You are watching scene 3
Vinsguru is watching scene 1
You are watching scene 4
Vinsguru is watching scene 2
You are watching scene 5
Vinsguru is watching scene 3
Vinsguru is watching scene 4
Vinsguru is watching scene 5
```

## **Reactor Hot Publisher**:

**==Hot Publishers do not create new data producer for each new subscription (as the Cold Publisher does). Instead there will be only one data producer and all the observers listen to the data produced by the single data producer. So all the observers get the same data.==**

- **Definition**: A hot publisher produces data independently of the subscribers. Subscribers receive data from the point of their subscription, not from the beginning.
    
- **Behavior**: Data is emitted whether or not there are subscribers. Subscribers only get the data emitted after they start subscribing.
    
- **Example**: `Flux` created using `Flux.interval(Duration.ofSeconds(1))` is hot. Subscribers will receive events starting from the moment they subscribe.

```java
Flux<Long> hotFlux = Flux.interval(Duration.ofSeconds(1));

hotFlux.subscribe(value -> System.out.println("Subscriber 1: " + value));
// Output (starts after 1 second): Subscriber 1: 0, 1, 2, ...

Thread.sleep(3000); // Wait 3 seconds

hotFlux.subscribe(value -> System.out.println("Subscriber 2: " + value));
// Output (starts after 3 seconds from subscription): Subscriber 2: 3, 4, 5, ...

```

---

Here we just added a ‘_**share**_‘ method in our Flux to make the Netflux server into a Movie theater. Share turns the Cold source into Hot by multi casting the emitted data to multiple subscribers.

```java
//our movie theatre
//each scene will play for 2 seconds
Flux<String> movieTheatre = Flux.fromStream(() -> getMovie())
                            .delayElements(Duration.ofSeconds(2)).share();

// you start watching the movie
movieTheatre.subscribe(scene -> System.out.println("You are watching " + scene));

//I join after sometime
Thread.sleep(5000);
movieTheatre.subscribe(scene -> System.out.println("Vinsguru is watching " + scene));
```

Output:

```bash
Got the movie streaming request
You are watching scene 1
You are watching scene 2
You are watching scene 3
Vinsguru is watching scene 3
You are watching scene 4
Vinsguru is watching scene 4
You are watching scene 5
Vinsguru is watching scene 5
```

From the output, I lost the first 2 scenes in that movie as I joined late. However I am able to watch latest scene played in the theater along with others.

this example using _**share**_ method. But here when the second subscriber joins, the source has already emitted data & completed. So the second subscription repeats the emission process. Imagine this like a same movie theater example with subsequent show once a first show is completed.

```java
//our movie theatre
//each scene will play for 2 seconds
        Flux<String> movieTheatre = Flux.fromStream(() -> getMovie())
                .delayElements(Duration.ofSeconds(2)).share();

// you start watching the movie
        movieTheatre.subscribe(scene -> System.out.println("You are watching " + scene));

//I join after the source is completed
        Thread.sleep(12000);
        movieTheatre.subscribe(scene -> System.out.println("Vinsguru is watching " + scene));
```

Output:

```bash
Got the movie streaming request
You are watching scene 1
You are watching scene 2
You are watching scene 3
You are watching scene 4
You are watching scene 5
Got the movie streaming request
Vinsguru is watching scene 1
Vinsguru is watching scene 2
Vinsguru is watching scene 3
Vinsguru is watching scene 4
Vinsguru is watching scene 5
```

### **Cache:**

- **Case 1:**

if we do not want to repeat, use _**cache**_ method. Cache method caches the history and multi casts to multiple subscribers. we are NOT making movie streaming request second time. However, second subscriber is able to watch all the scenes from the beginning as it has cached all the items for future subscribers.

```java
//our movie theatre
//each scene will play for 2 seconds
        Flux<String> movieTheatre = Flux.fromStream(() -> getMovie())
                .delayElements(Duration.ofSeconds(2)).cache();

// you start watching the movie
        movieTheatre.subscribe(scene -> System.out.println("You are watching " + scene));

//I join after the source is completed
        Thread.sleep(12000);
        movieTheatre.subscribe(scene -> System.out.println("Vinsguru is watching " + scene));
```

Output:

```bash
Got the movie streaming request
You are watching scene 1
You are watching scene 2
You are watching scene 3
You are watching scene 4
You are watching scene 5
Vinsguru is watching scene 1
Vinsguru is watching scene 2
Vinsguru is watching scene 3
Vinsguru is watching scene 4
Vinsguru is watching scene 5
```

- **Case 2:**

If you do not like caching all the items, use _**cache(0).**_

Output:

```bash
Got the movie streaming request
You are watching scene 1
You are watching scene 2
You are watching scene 3
You are watching scene 4
You are watching scene 5
```

## **Key Differences**

- **Data Emission**:
    
    - **Cold**: Data is produced only when there is a subscriber.
    - **Hot**: Data is produced regardless of subscribers, and subscribers get data emitted after their subscription.
- **Subscriber Independence**:
    
    - **Cold**: Each subscriber gets a full and independent sequence of data.
    - **Hot**: Subscribers share the same data stream and only receive data from the point of their subscription.


# Back Pressure Overflow Strategy

In reactive programming, **backpressure** **==is a mechanism to handle situations where a `Publisher` emits items faster than a `Subscriber` can process them==**. To manage this, various **overflow strategies** can be applied. Here's a detailed overview of different backpressure strategies:

## **1. Limit Rate Strategy**

- **Definition**: Limits the rate at which items are requested or emitted. It controls how many items can be processed in a given time period.
- **Usage**: Useful when you want to throttle the rate of data production to prevent overwhelming the subscriber.
- **Example**:
  ```java
  Flux<Integer> flux = Flux.range(1, 100)
      .limitRate(10);
  ```

## **2. Buffer Strategy**

- **Definition**: Collects emitted items into a buffer up to a certain size. Once the buffer is full, additional items may either be discarded or trigger other strategies.
- **Usage**: Useful for batching items together before processing.
- **Example**:
  ```java
  Flux<Integer> flux = Flux.range(1, 100)
      .onBackpressureBuffer(10); // Buffer up to 10 items
  ```

## **3. Error Strategy**

- **Definition**: When backpressure cannot be handled, an error is signaled to the subscriber. This is typically used to indicate that the system is overwhelmed and cannot process additional items.
- **Usage**: Useful when you want to fail fast and handle the overload situation by terminating the subscription.
- **Example**:
  ```java
  Flux<Integer> flux = Flux.range(1, 100)
      .onBackpressureError(); // Signal an error when buffer overflows
  ```

## **4. Fixed Size Buffer Strategy**

- **Definition**: Similar to the buffer strategy but with a fixed-size buffer. When the buffer is full, items are either dropped or handled according to other strategies.
- **Usage**: Useful when you have a fixed amount of memory or need to control the buffer size precisely.
- **Example**:
  ```java
  Flux<Integer> flux = Flux.range(1, 100)
      .onBackpressureBuffer(10, BufferOverflowStrategy.DROP_OLDEST); // Fixed size buffer
  ```

## **5. Drop Strategy**

- **Definition**: Drops items when the buffer is full, based on different drop policies. The drop policy could be the oldest item, the latest item, or others.
- **Usage**: Useful when you can tolerate losing some items to prevent overwhelming the system.
- **Example**:
  ```java
  Flux<Integer> flux = Flux.range(1, 100)
      .onBackpressureBuffer(10, BufferOverflowStrategy.DROP_OLDEST); // Drop oldest items when buffer is full
  ```

## **6. Latest Strategy**

- **Definition**: Keeps only the latest item when the buffer is full, discarding older items. This strategy ensures that the most recent data is always available.
- **Usage**: Useful when the most recent data is more important than the older data.
- **Example**:
  ```java
  Flux<Integer> flux = Flux.range(1, 100)
      .onBackpressureBuffer(10, BufferOverflowStrategy.DROP_OLDEST)
      .onBackpressureBuffer(10, BufferOverflowStrategy.DROP_LATEST); // Drop latest items when buffer is full
  ```

## **Summary**

- **Limit Rate**: Throttles the rate of data production.
- **Buffer**: Collects items into a buffer up to a certain size.
- **Error**: Signals an error when backpressure is exceeded.
- **Fixed Size Buffer**: Uses a buffer of fixed size with specified handling of overflow.
- **Drop**: Drops items based on a drop policy when the buffer is full.
- **Latest**: Keeps only the latest item in the buffer, dropping older items.

Choosing the right backpressure strategy depends on the specific requirements of your application, such as the importance of data accuracy, memory constraints, and the desired behavior under high load.

