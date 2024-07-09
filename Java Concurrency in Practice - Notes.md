
# Chapter 1

## Introduction

Threads are an inescapable feature of the Java language, and they can simplify the development of complex systems by turning complicated asynchronous code into simpler straight-line code. In addition, threads are the easiest way to tap the computing power of multiprocessor systems. And, as processor counts increase, exploiting concurrency effectively will only become more important.

### 1.1 A (very) brief history of concurrency

Operating systems evolved to allow more than one program to run at once, running individual programs in processes: isolated, independently executing programs to which the operating system allocates resources such as memory, file handles, and security credentials. If they needed to, processes could communicate with one another through a variety of coarse-grained communication mechanisms: sockets, signal handlers, shared memory, semaphores, and files.
Several motivating factors led to the development of operating systems that allowed multiple programs to execute simultaneously:

**Resource utilization**. Programs sometimes have to wait for external operations such as input or output, and while waiting can do no useful work. It is more efficient to use that wait time to let another program run.

**Fairness**. Multiple users and programs may have equal claims on the machine’s resources. It is preferable to let them share the computer via finer-grained time slicing than to let one program run to completion and then start another.

**Convenience**. It is often easier or more desirable to write several programs that each perform a single task and have them coordinate with each other as necessary than to write a single program that performs all the tasks.

sequential programming model, where the language specification clearly defines *what comes next* after a given action is executed. The sequential programming model is intuitive and natural, as it models the way humans work: do one thing at a time, in sequence—mostly

As in programming languages, each of these real-world actions is an abstraction for a sequence of finer-grained actions—open the cupboard, select a flavor of tea, measure some tea into the pot, see if there’s enough water in the teakettle, if not put some more water in, set it on the stove, turn the stove on, wait for the water to boil, and so on. This last step—waiting for the water to boil—also involves a degree of asynchrony. While the water is heating, you have a choice of what to do—just wait, or do other tasks in that time such as starting the toast (another asynchronous task) or fetching the newspaper, while remaining aware that your attention will soon be needed by the teakettle. The manufacturers of teakettles and toasters know their products are often used in an asynchronous manner, so they raise an audible signal when they complete their task. Finding the right balance of sequentially and asynchrony is often a characteristic of efficient people—and the same is true of programs.

The same concerns (resource utilization, fairness, and convenience) that motivated the development of processes also motivated the development of threads. Threads allow multiple streams of program control flow to coexist within a process. They share process-wide resources such as memory and file handles, but each thread has its own program counter, stack, and local variables. Threads also provide a natural decomposition for exploiting hardware parallelism on multiprocessor systems; multiple threads within the same program can be scheduled simultaneously on multiple CPUs.

Threads are sometimes called *lightweight processes*, and most modern operating systems treat threads, not processes, as the basic units of scheduling. In the absence of explicit coordination, threads execute simultaneously and asynchronously with respect to one another. Since threads share the memory address space of their owning process, all threads within a process have access to the same variables and allocate objects from the same heap, which allows finer-grained data sharing than inter-process mechanisms. But without explicit synchronization to coordinate access to shared data, a thread may modify variables that another thread is in the middle of using, with unpredictable results.
### 1.2 Benefits of threads

When used properly, threads can reduce development and maintenance costs and improve the performance of complex applications. Threads make it easier to model how humans work and interact, by turning asynchronous workflows into mostly sequential ones. They can also turn otherwise convoluted code into straight-line code that is easier to write, read, and maintain.
#### 1.2.1 Exploiting multiple processors

Since the basic unit of scheduling is the thread, a program with only one thread can run on at most one processor at a time. On a two-processor system, a single-threaded program is giving up access to half the available CPU resources; on a 100-processor system, it is giving up access to 99%. On the other hand, programs with multiple active threads can execute simultaneously on multiple processors. When properly designed, multithreaded programs can improve throughput by utilizing available processor resources more effectively.

Using multiple threads can also help achieve better throughput on single-processor systems. If a program is single-threaded, the processor remains idle while it waits for a synchronous I/O operation to complete. In a multithreaded program, another thread can still run while the first thread is waiting for the I/O to complete, allowing the application to still make progress during the blocking I/O.

#### 1.2.2 Simplicity of modeling

It is often easier to manage your time when you have only one type of task to perform than when you have several. When you have only one type of task to do, you can start at the top of the pile and keep working until the pile is exhausted (or you are); you don’t have to spend any mental energy figuring out what to work on next. On the other hand, managing multiple priorities and deadlines and switching from task to task usually carries
some overhead.

The same is true for software: a program that processes one type of task sequentially is simpler to write, less error-prone, and easier to test than one managing multiple different types of tasks at once. Assigning a thread to each type of task or to each element in a simulation affords the illusion of sequentially and insulates domain logic from the details of scheduling, interleaved operations, asynchronous I/O, and resource waits. A complicated, asynchronous workflow can be decomposed into a number of simpler, synchronous workflows each running in a separate thread, interacting only with each other at specific synchronization points.

#### 1.2.3 Simplified handling of asynchronous events

A server application that accepts socket connections from multiple remote clients may be easier to develop when each connection is allocated its own thread and allowed to use synchronous I/O.

If an application goes to read from a socket when no data is available, read blocks until some data is available. In a single-threaded application, this means that not only does processing the corresponding request stall, but processing of all requests stalls while the single thread is blocked. To avoid this problem, single-threaded server applications are forced to use nonblocking I/O, which is far more complicated and error-prone than synchronous I/O. However, if each request has its own thread, then blocking does not affect the processing of other requests.

#### 1.2.4 More responsive user interfaces

If only short-lived tasks execute in the event thread, the interface remains responsive since the event thread is always able to process user actions reasonably quickly. However, processing a long-running task in the event thread, such as spell-checking a large document or fetching a resource over the network, impairs responsiveness. If the user performs an action while this task is running, there is a long delay before the event thread can process or even acknowledge it. To add insult to injury, not only does the UI become unresponsive, but it is impossible to cancel the offending task even if the UI provides a cancel button because the event thread is busy and cannot handle the cancel button-press event until the lengthy task completes!

### 1.3 Risks of threads

While it simplifies the development of concurrent applications by providing language and library support and a formal cross-platform memory model (it is this formal cross-platform memory model that makes possible the development of write-once, run-anywhere concurrent applications in Java), it also raises the bar for developers because more programs will use threads. When threads were more esoteric, concurrency was an “advanced” topic; now, mainstream developers must be aware of thread-safety issues.

#### 1.3.1 Safety hazards

Thread safety can be unexpectedly subtle because, in the absence of sufficient synchronization, the ordering of operations in multiple threads is unpredictable and sometimes surprising.

```java
@NotThreadSafe
public class UnsafeSequence {
	private int value;
	/** Returns a unique value. */
	public int getNext() {
		return value++;
	}
}
```

![[Pasted image 20240707085441.png]]

The problem with ``UnsafeSequence`` is that with some unlucky timing, two threads could call ``getNext`` and receive the same value. ==**The increment notation, ``someVariable++``, may appear to be a single operation, but is in fact three separate operations: read the value, add one to it, and write out the new value**==. Since operations in multiple threads may be arbitrarily interleaved by the runtime, it is possible for two threads to read the value at the same time, both see the same value, and then both add one to it.

``UnsafeSequence`` illustrates a common concurrency hazard called a ***race condition***. Whether or not ``getNext`` returns a unique value when called from multiple threads, as required by its specification, depends on how the runtime interleaves the operations—which is not a desirable state of affairs.

Because threads share the same memory address space and run concurrently, they can access or modify variables that other threads might be using. This is a tremendous convenience, because it makes data sharing much easier than would other inter-thread communications mechanisms. But it is also a significant risk: threads can be confused by having data change unexpectedly. Allowing multiple threads to access and modify the same variables introduces an element of non-sequentially into an otherwise sequential programming model, which can be confusing and difficult to reason about. For a multithreaded program’s behavior to be predictable, access to shared variables must be properly coordinated so that threads do not interfere with one another. Fortunately, Java provides synchronization mechanisms to coordinate such access.

```java
@ThreadSafe
public class Sequence {
	@GuardedBy("this") private int value;
	public synchronized int getNext() {
		return value++;
	}
}
```

#### 1.3.2 Liveness hazards

safety cannot be compromised. The importance of safety is not unique to multithreaded programs—single-threaded programs also must take care to preserve safety and correctness—but the use of threads introduces additional safety hazards not present in single-threaded programs. Similarly, the use of threads introduces additional forms of *liveness failure* that do not occur in single-threaded programs.

While safety means “nothing bad ever happens”, liveness concerns the complementary goal that “something good eventually happens”. A liveness failure occurs when an activity gets into a state such that it is permanently unable to make forward progress. One form of liveness failure that can occur in sequential programs is an inadvertent infinite loop, where the code that follows the loop never gets executed. The use of threads introduces additional liveness risks. For example, if thread A is waiting for a resource that thread B holds exclusively, and B never releases it, A will wait forever.

#### 1.3.3 Performance hazards

Related to liveness is performance. While liveness means that something good eventually happens, eventually may not be good enough—we often want good things to happen quickly. Performance issues subsume a broad range of problems, including poor service time, responsiveness, throughput, resource consumption, or scalability.

*Context switches*—when the scheduler suspends the active thread temporarily so another thread can run—are more frequent in applications with many threads, and have significant costs: saving and restoring execution context, loss of locality, and CPU time spent scheduling threads instead of running them. When threads share data, they must use synchronization mechanisms that can inhibit compiler optimizations, flush or invalidate memory caches, and create synchronization traffic on the shared memory bus. All these factors introduce additional performance costs;
### 1.4 Threads are everywhere

Even if your program never explicitly creates a thread, frameworks may create threads on your behalf, and code called from these threads must be thread-safe.

Every Java application uses threads. When the JVM starts, it creates threads for JVM housekeeping tasks (garbage collection, finalization) and a main thread for running the main method. The AWT (Abstract Window Toolkit) and Swing user interface frameworks create threads for managing user interface events

It would be nice to believe that concurrency is an “optional” or “advanced” language feature, but the reality is that nearly all Java applications are multithreaded and these frameworks do not insulate you from the need to properly coordinate access to application state.

When concurrency is introduced into an application by a framework, it is usually impossible to restrict the concurrency-awareness to the framework code, because frameworks by their nature make callbacks to application components that in turn access application state.

# Fundamentals #Part-1

## Thread Safety

==building concurrent programs require the correct use of threads and locks. Writing thread-safe code is, at its core, about managing access to ***state***, and in particular to ***shared, mutable state***.==

Informally, an object’s state is its data, stored in state variables such as instance or static fields. An object’s state may include fields from other, dependent objects; a ``HashMap``’s state is partially stored in the ``HashMap`` object itself, but also in many ``Map.Entry`` objects. An object’s state encompasses any data that can affect its externally visible behavior.

By *shared*, we mean that a variable could be accessed by multiple threads; by mutable, we mean that its value could change during its lifetime. We may talk about thread safety as if it were about code, but what we are really trying to do is protect data from uncontrolled concurrent access.

Whether an object needs to be thread-safe depends on whether it will be accessed from multiple threads. This is a property of how the object is used in a program, not what it does. Making an object thread-safe requires using synchronization to coordinate access to its mutable state; failing to do so could result in data corruption and other undesirable consequences.

Whenever more than one thread accesses a given state variable, and one of them might write to it, they all must coordinate their access to it using synchronization. **==The primary mechanism for synchronization in Java is the ``synchronized`` keyword, which provides exclusive locking, but the term “synchronization” also includes the use of ``volatile`` variables, explicit locks, and atomic variables.==**

A program that omits needed synchronization might appear to work, passing its tests and performing well for years, but it is still broken and may fail at any moment.

**==If multiple threads access the same mutable state variable without appropriate synchronization, your program is broken. There are three ways to fix it:**==
==**• Don’t share the state variable across threads;**==
==**• Make the state variable immutable; or**==
==**• Use synchronization whenever accessing the state variable.==**

It is far easier to design a class to be thread-safe than to retrofit it for thread safety later.

**==The less code that has access to a particular variable, the easier it is to ensure that all of it uses the proper synchronization, and the easier it is to reason about the conditions under which a given variable might be accessed.==**

the better encapsulated your program state, the easier it is to make your program thread-safe and to help maintainers keep it that way

**==When designing thread-safe classes, good object-oriented techniques— encapsulation, immutability, and clear specification of invariants—are your best friends.==** Sometimes abstraction and encapsulation are at odds with performance
 
 Even then, pursue optimization only if your performance measurements and requirements tell you that you must, and if those same measurements tell you that your optimizations actually made a difference under realistic conditions.

Is a thread-safe program one that is constructed entirely of thread-safe classes? Not necessarily—a program that consists entirely of thread-safe classes may not be thread-safe, and a thread-safe program may contain classes that are not thread-safe. 

**==the concept of a thread-safe class makes sense only if the class encapsulates its own state==**. Thread safety may be a term that is applied to code, but it is about state, and it can only be applied to the entire body of code that encapsulates its state, which may be an object or an entire program.

### 2.1 What is thread safety?

>. . . can be called from multiple program threads without unwanted interactions between the threads.
 . . . may be called by more than one thread at a time without requiring any other action on the caller’s part.

How do we tell a thread-safe class from an  unsafe one? What do we even mean by “safe”?
At the heart of any reasonable definition of thread safety is the concept of correctness. Correctness means that a class conforms to its specification. A good specification defines invariants constraining an object’s state and postconditions describing the effects of its operations. a class is thread-safe when it continues to behave correctly when accessed from multiple threads.

**==A class is thread-safe if it behaves correctly when accessed from multiple threads, regardless of the scheduling or interleaving of the execution of those threads by the runtime environment, and with no additional synchronization or other coordination on the part of the calling code.==**

No set of operations performed sequentially or concurrently on instances of a thread-safe class can cause an instance to be in an invalid state.

Thread-safe classes encapsulate any needed synchronization so that clients need not provide their own.

**==Thread-safe classes encapsulate any needed synchronization so that clients need not provide their own.==**

#### 2.1.1 Example: a stateless servlet

```java
@ThreadSafe
public class StatelessFactorizer implements Servlet {
	public void service(ServletRequest req, ServletResponse resp) {
		BigInteger i = extractFromRequest(req);
		BigInteger[] factors = factor(i);
		encodeIntoResponse(resp, factors);
	}
}
```

``StatelessFactorizer`` is, like most servlets, stateless: it has no fields and references no fields from other classes. The transient state for a particular computation exists solely in local variables that are stored on the thread’s stack and are accessible only to the executing thread. One thread accessing a ``StatelessFactorizer`` cannot influence the result of another thread accessing the same ``StatelessFactorizer``; because the two threads do not share state, it is as if they were accessing different instances.

**==Stateless objects are always thread-safe.==**

### 2.2 Atomicity

```java
@NotThreadSafe
public class UnsafeCountingFactorizer implements Servlet {
	private long count = 0;
	public long getCount() { return count; }
	public void service(ServletRequest req, ServletResponse resp) {
		BigInteger i = extractFromRequest(req);
		BigInteger[] factors = factor(i);
		++count;
		encodeIntoResponse(resp, factors);
	}
}
```

Unfortunately, ``UnsafeCountingFactorizer`` is not thread-safe, even though it would work just fine in a single-threaded environment. While the increment operation, ``++count``, may look like a single action because of its compact syntax, it is not atomic, which means that it does not execute as a single, indivisible operation. Instead, it is a shorthand for a sequence of three discrete operations: fetch the current value, add one to it, and write the new value back. This is an example of a *read-modify-write operation*, in which the resulting state is derived from the previous state.

> A read-modify-write (RMW) operation is a sequence in computer systems where a value is read from a memory location, modified, and then written back to the same location. This operation is atomic, meaning it completes in a single, indivisible step, ensuring data consistency and preventing race conditions in concurrent environments.

**==The possibility of incorrect results in the presence of unlucky timing is so important in concurrent programming that it has a name: a *race condition*.==**

#### 2.2.1 Race conditions

A race condition occurs when the correctness of a computation depends on the relative timing or interleaving of multiple threads by the runtime; in other words, when getting the right answer relies on lucky timing. The most common type of race condition is check-then-act, where a potentially stale observation is used to make a decision on what to do next.

> Check-then-act is a process in concurrent programming where a condition is checked (read) and based on the result, an action is taken. However, this operation is not atomic; the condition might change between the check and the act steps, potentially leading to race conditions.

reaching the desired outcome  depends on the relative timing of events. It is this invalidation of observations that characterizes most race conditions—using a potentially stale observation to make a decision or perform a computation. This type of race condition is called check-then-act: you observe something to be true (file X doesn’t exist) and then take action based on that observation (create X); but in fact the observation could have become invalid between the time you observed it and the time you acted on it (someone else created X in the meantime), causing a problem

#### 2.2.2 Example: race conditions in lazy initialization

A common idiom that uses check-then-act is lazy initialization. The goal of lazy initialization is to defer initializing an object until it is actually needed while at the same time ensuring that it is initialized only once.

```java
@NotThreadSafe
public class LazyInitRace {
	private ExpensiveObject instance = null;
		public ExpensiveObject getInstance() {
		if (instance == null)
			instance = new ExpensiveObject();
		return instance;
	}
}
```

``LazyInitRace`` has race conditions that can undermine its correctness. Say that threads A and B execute ``getInstance`` at the same time. A sees that instance is null, and instantiates a new ``ExpensiveObject``. B also checks if instance is null. Whether instance is null at this point depends unpredictably on timing, including the vagaries of scheduling and how long A takes to instantiate the ``ExpensiveObject`` and set the instance field. If instance is null when B examines it, the two callers to ``getInstance`` may receive two different results, even though ``getInstance`` is always supposed to return the same instance.

Read-modify-write operations, like incrementing a counter, define a transformation of an object’s state in terms of its previous state. To increment a counter, you have to know its previous value and make sure no one else changes or uses that value while you are in mid-update.

#### 2.2.3 Compound actions

To avoid race conditions, there must be a way to prevent other threads from using a variable while we’re in the middle of modifying it, so we can ensure that other threads can observe or modify the state only before we start or after we finish, but not in the middle.

**==Operations A and B are atomic with respect to each other if, from the perspective of a thread executing A, when another thread executes B, either all of B has executed or none of it has. An atomic operation is one that is atomic with respect to all operations, including itself, that operate on the same state.==**

To ensure thread safety, check-then-act operations (like lazy initialization) and read-modify-write operations (like increment) must always be atomic.

```java
@ThreadSafe
public class CountingFactorizer implements Servlet {
	private final AtomicLong count = new AtomicLong(0);
	public long getCount() { return count.get(); }
	public void service(ServletRequest req, ServletResponse resp) {
		BigInteger i = extractFromRequest(req);
		BigInteger[] factors = factor(i);
		count.incrementAndGet();
		encodeIntoResponse(resp, factors);
	}
}
```

The ``java.util.concurrent.atomic`` package contains atomic variable classes for effecting atomic state transitions on numbers and object references. When a single element of state is added to a stateless class, the resulting class will be thread-safe if the state is entirely managed by a thread-safe object.

Where practical, use existing thread-safe objects, like ``AtomicLong``, to manage your class’s state. It is simpler to reason about the possible states and state transitions for existing thread-safe objects than it is for arbitrary state variables, and this makes it easier to maintain and verify thread safety.

### 2.3 Locking

Imagine that we want to improve the performance of our servlet by caching the most recently computed result, just in case two consecutive clients request factorization of the same number. To implement this strategy, we need to remember two things: the last number factored, and its factors.

```java
@NotThreadSafe
public class UnsafeCachingFactorizer implements Servlet {
    private final AtomicReference<BigInteger> lastNumber = new AtomicReference<BigInteger>();
    private final AtomicReference<BigInteger[]> lastFactors = new AtomicReference<BigInteger[]>();

    public void service(ServletRequest req, ServletResponse resp) {
        BigInteger i = extractFromRequest(req);
        if (i.equals(lastNumber.get())) {
            encodeIntoResponse(resp, lastFactors.get());
        } else {
            BigInteger[] factors = factor(i);
            lastNumber.set(i);
            lastFactors.set(factors);
            encodeIntoResponse(resp, factors);
        }
    }
}

```

this approach does not work. Even though the atomic references are individually thread-safe, ``UnsafeCachingFactorizer`` has race conditions. **==When multiple variables participate in an invariant, they are not independent: the value of one constrains the allowed value(s) of the others. Thus when updating one, you must update the others in the same atomic operation.==**

Using atomic references, we cannot update both ``lastNumber`` and ``lastFactors`` simultaneously, even though each call to set is atomic; there is still a window of vulnerability when one has been modified and the other has not, and during that time other threads could see that the invariant does not hold. Similarly, the two values cannot be fetched simultaneously: between the time when thread A fetches the two values, thread B could have changed them, and again A may observe that the invariant does not hold.

> To preserve state consistency, update related state variables in a single atomic operation.

#### 2.3.1 Intrinsic locks

Java provides a built-in locking mechanism for enforcing atomicity: the ``synchronized`` block. A ``synchronized`` block has two parts: a reference to an object that will serve as the lock, and a block of code to be guarded by that lock. A ``synchronized`` method is a shorthand for a synchronized block that spans an entire method body, and whose lock is the object on which the method is being invoked. (Static synchronized methods use the Class object for the lock.)

```java
synchronized (lock) {
	// Access or modify shared state guarded by lock
}
```

Every Java object can implicitly act as a lock for purposes of synchronization; these built-in locks are called intrinsic locks or monitor locks. The lock is automatically acquired by the executing thread before entering a synchronized block and automatically released when control exits the synchronized block, whether by the normal control path or by throwing an exception out of the block. The only way to acquire an intrinsic lock is to enter a synchronized block or method guarded by that lock.

Intrinsic locks in Java act as mutexes (or mutual exclusion locks), which means that at most one thread may own the lock. When thread A attempts to acquire a lock held by thread B, A must wait, or block, until B releases it. If B never releases the lock, A waits forever

Since only one thread at a time can execute a block of code guarded by a given lock, the synchronized blocks guarded by the same lock execute atomically with respect to one another. In the context of concurrency, atomicity means the same thing as it does in transactional applications—that a group of statements appear to execute as a single, indivisible unit.

```java
@ThreadSafe
public class SynchronizedFactorizer implements Servlet {
    @GuardedBy("this") private BigInteger lastNumber;
    @GuardedBy("this") private BigInteger[] lastFactors;

    public synchronized void service(ServletRequest req, ServletResponse resp) {
        BigInteger i = extractFromRequest(req);
        if (i.equals(lastNumber)) {
            encodeIntoResponse(resp, lastFactors);
        } else {
            BigInteger[] factors = factor(i);
            lastNumber = i;
            lastFactors = factors;
            encodeIntoResponse(resp, factors);
        }
    }
}
```

#### 2.3.2 Reentrancy

When a thread requests a lock that is already held by another thread, the requesting thread blocks. But because intrinsic locks are reentrant, if a thread tries to acquire a lock that it already holds, the request succeeds. **==Reentrancy means that locks are acquired on a per-thread rather than per-invocation basis. Reentrancy is implemented by associating with each lock an acquisition count and an owning thread==**. When the count is zero, the lock is considered unheld. When a thread acquires a previously unheld lock, the JVM records the owner and sets the acquisition count to one. If that same thread acquires the lock again, the count is incremented, and when the owning thread exits the synchronized block, the count is decremented. When the count reaches zero, the lock is released.

Reentrancy facilitates encapsulation of locking behavior, and thus simplifies the development of object-oriented concurrent code. Without reentrant locks,  which a subclass overrides a synchronized method and then calls the superclass method, would deadlock. Because the ``doSomething`` methods in Widget and ``LoggingWidget`` are both synchronized, each tries to acquire the lock on the Widget before proceeding. But if intrinsic locks were not reentrant, the call to ``super.doSomething`` would never be able to acquire the lock because it would be considered already held, and the thread would permanently stall waiting for a lock it can never acquire. Reentrancy saves us from deadlock in situations like this.

**Code that would deadlock if intrinsic locks were not reentrant.**
```java
public class Widget {
	public synchronized void doSomething() {
		...
	}
}
public class LoggingWidget extends Widget {
	public synchronized void doSomething() {
		System.out.println(toString() + ": calling doSomething");
		super.doSomething();
	}
}
```
### 2.4 Guarding state with locks

Because locks enable serialized8 access to the code paths they guard, we can use them to construct protocols for guaranteeing exclusive access to shared state. Following these protocols consistently can ensure state consistency

Compound actions on shared state, must be made atomic to avoid race conditions. Holding a lock for the entire duration of a compound action can make that compound action atomic. However, just wrapping the compound action with a ``synchronized`` block is not sufficient; if synchronization is used to coordinate access to a variable, it is needed everywhere that variable is accessed. Further, when using locks to coordinate access to a variable, the same lock must be used wherever that variable is accessed. 

It is a common mistake to assume that synchronization needs to be used only when writing to shared variables; this is simply not true

> For each mutable state variable that may be accessed by more than one thread, all accesses to that variable must be performed with the same lock held. In this case, we say that the variable is guarded by that lock.

There is no inherent relationship between an object’s intrinsic lock and its state; an object’s fields need not be guarded by its intrinsic lock, though this is a perfectly valid locking convention that is used by many classes. Acquiring the lock associated with an object does not prevent other threads from accessing that object—the only thing that acquiring a lock prevents any other thread from doing is acquiring that same lock. The fact that every object has a built-in lock is just a convenience so that you needn’t explicitly create lock objects. It is up to you to construct locking protocols or synchronization policies that let you access shared state safely, and to use them consistently throughout your program.

> Every shared, mutable variable should be guarded by exactly one lock. Make it clear to maintainers which lock that is.

A common locking convention is to encapsulate all mutable state within an object and to protect it from concurrent access by synchronizing any code path that accesses mutable state using the object’s intrinsic lock. This pattern is used by many thread-safe classes, such as Vector and other synchronized collection classes. In such cases, all the variables in an object’s state are guarded by the object’s intrinsic lock. However, there is nothing special about this pattern, and neither the compiler nor the runtime enforces this (or any other) pattern of locking. 10 It is also easy to subvert this locking protocol accidentally by adding a new method or code path and forgetting to use synchronization.

**==Not all data needs to be guarded by locks—only mutable data that will be accessed from multiple threads.==**


When a variable is guarded by a lock—meaning that every access to that variable is performed with that lock held—you’ve ensured that only one thread at a time can access that variable. When a class has invariants that involve more than one state variable, there is an additional requirement: each variable participating in the invariant must be guarded by the same lock. This allows you to access or update them in a single atomic operation, preserving the invariant. ``SynchronizedFactorizer`` demonstrates this rule: both the cached number and the cached factors are guarded by the servlet object’s intrinsic lock.

> For every invariant that involves more than one variable, all the variables involved in that invariant must be guarded by the same lock.

If synchronization is the cure for race conditions, why not just declare every method synchronized? It turns out that such indiscriminate application of synchronized might be either too much or too little synchronization. Merely synchronizing every method, as ``Vector`` does, is not enough to render compound actions on a ``Vector`` atomic:

```java
if (!vector.contains(element))
	vector.add(element);
```

**==While synchronized methods can make individual operations atomic, additional locking is required when multiple operations are combined into a compound action==** At the same time, synchronizing every method can lead to liveness or performance problems

### 2.5 Liveness and performance

Caching required some shared state, which in turn required synchronization to maintain the integrity of that state. But the way we used synchronization in ``SynchronizedFactorizer`` makes it perform badly. The synchronization policy for ``SynchronizedFactorizer`` is to guard each state variable with the servlet object’s intrinsic lock, and that policy was implemented by synchronizing the entirety of the ``service`` method. This simple, coarse-grained approach restored safety, but at a high price.

![[Pasted image 20240707105041.png]]

when multiple requests arrive for the synchronized they queue up and are handled sequentially. We would
describe this web application as exhibiting poor concurrency: the number of simultaneous invocations is limited not by the availability of processing resources, but by the structure of the application itself. Fortunately, it is easy to improve the concurrency of the servlet while maintaining thread safety by narrowing the scope of the synchronized block. You should be careful not to make the scope of the synchronized block too small; you would not want to divide an operation that should be atomic into more than one synchronized block. But it is reasonable to try to exclude from synchronized blocks long-running operations that do not affect shared state, so that other threads are not prevented from accessing the shared state while the long-running operation is in progress.

```java
@ThreadSafe
public class CachedFactorizer implements Servlet {
    @GuardedBy("this") private BigInteger lastNumber;
    @GuardedBy("this") private BigInteger[] lastFactors;
    @GuardedBy("this") private long hits;
    @GuardedBy("this") private long cacheHits;

    public synchronized long getHits() { 
        return hits; 
    }

    public synchronized double getCacheHitRatio() {
        return (double) cacheHits / (double) hits;
    }

    public void service(ServletRequest req, ServletResponse resp) {
        BigInteger i = extractFromRequest(req);
        BigInteger[] factors = null;

        synchronized (this) {
            ++hits;
            if (i.equals(lastNumber)) {
                ++cacheHits;
                factors = lastFactors.clone();
            }
        }

        if (factors == null) {
            factors = factor(i);
            synchronized (this) {
                lastNumber = i;
                lastFactors = factors.clone();
            }
        }

        encodeIntoResponse(resp, factors);
    }
}
```

Atomic variables are useful for effecting atomic operations on a single variable, but since we are already using synchronized blocks to construct atomic operations, using two different synchronization mechanisms would be confusing and would offer no performance or safety benefit. Acquiring and releasing a lock has some overhead, so it is undesirable to break down ``synchronized`` blocks too far

Deciding how big or small to make synchronized blocks may require tradeoffs among competing design forces, including safety (which must not be compromised), simplicity, and performance. Sometimes simplicity and performance are at odds with each other, although as ``CachedFactorizer`` illustrates, a reasonable balance can usually be found.

>There is frequently a tension between simplicity and performance. When implementing a synchronization policy, resist the temptation to prematurely sacrifice simplicity (potentially compromising safety) for the sake of performance.

Whenever you use locking, you should be aware of what the code in the block is doing and how likely it is to take a long time to execute. Holding a lock for a long time, either because you are doing something compute-intensive or because you execute a potentially blocking operation, introduces the risk of liveness or performance problems.

> Avoid holding locks during lengthy computations or operations at risk of not completing quickly such as network or console I/O

## Sharing Objects

**==writing correct concurrent programs is primarily about managing access to shared, mutable state==**. A common misconception that synchronized is only about atomicity or demarcating “*critical sections*”. Synchronization also has another significant, and subtle, aspect: *memory visibility*. We want not only to prevent one thread from modifying the state of an object when another is using it, but also to ensure that when a thread modifies the state of an object, other threads can actually see the changes that were made.

### 3.1 Visibility

In a single-threaded environment, if you write a value to a variable and later read that variable with no intervening writes, you can expect to get the same value back. When the reads and writes occur in different threads there is no guarantee that the reading thread will see a value written by another thread on a timely basis, or even at all. In order to ensure visibility of memory writes across threads, you must use synchronization.

```java
public class NoVisibility {
	private static boolean ready;
	private static int number;
	private static class ReaderThread extends Thread {
		public void run() {
			while (!ready)
				Thread.yield();
			System.out.println(number);
		}
	}
	public static void main(String[] args) {
		new ReaderThread().start();
		number = 42;
		ready = true;
	}
}
```

a phenomenon known as reordering. There is no guarantee that operations in one thread will be performed in the order given by the program, as long as the reordering is not detectable from within that thread. When the main thread writes first to ``number`` and then to ``ready`` without synchronization, the reader thread could see those writes happen in the opposite order—or not at all.

> Reordering in concurrency refers to the phenomenon where the order of operations in a multi-threaded program is changed by the compiler, processor, or memory subsystem to optimize performance.


In the absence of synchronization, the compiler, processor, and runtime can do some downright weird things to the order in which operations appear to execute. Attempts to reason about the order in which memory actions “must” happen in insufficiently synchronized multithreaded programs will almost certainly be incorrect.

**==always use the proper synchronization whenever data is shared across threads.==**

#### 3.1.1 Stale data

> Stale data in concurrency refers to outdated or old data that a thread reads from a shared resource because it has not yet seen the latest updates made by other threads. This can occur due to lack of proper synchronization, leading to inconsistent or incorrect program behavior.

``NoVisibility`` demonstrated one of the ways that insufficiently synchronized programs can cause surprising results: stale data. When the reader thread examines ready, it may see an out-of-date value. Unless synchronization is used every time a variable is accessed, it is possible to see a stale value for that variable. Worse, staleness is not all-or-nothing: a thread can see an up-to-date value of one variable but a stale value of another variable that was written first. *stale values can cause serious safety or liveness failures. Stale data can cause serious and confusing failures such as unexpected exceptions, corrupted data structures, inaccurate computations, and infinite loops.*

```java
@NotThreadSafe
public class MutableInteger {
	private int value;
	public int get() { return value; }
	public void set(int value) { this.value = value; }
}
```

```java
@ThreadSafe
public class SynchronizedInteger {
	@GuardedBy("this") private int value;
	public synchronized int get() { return value; }
	public synchronized void set(int value) { this.value = value; }
}
```

#### 3.1.2 Nonatomic 64-bit operations

When a thread reads a variable without synchronization, it may see a stale value, but at least it sees a value that was actually placed there by some thread rather than some random value. This safety guarantee is called out-of-thin-air safety.

> Out-of-thin-air safety in concurrency ensures that variables will not take on arbitrary, unpredictable values that are not derived from any legal program state. Proper synchronization and memory consistency models prevent the creation and use of such spurious values, ensuring that variables only hold valid, expected data based on the program's operations.

**==Out-of-thin-air safety applies to all variables, with one exception: 64-bit numeric variables (``double`` and ``long``) that are not declared ``volatile``==** The Java Memory Model requires fetch and store operations to be atomic,
but for nonvolatile ``long`` and ``double`` variables, the JVM is permitted to treat a 64-bit read or write as two separate 32-bit operations. If the reads and writes occur in different threads, it is therefore possible to read a nonvolatile long and get back the high 32 bits of one value and the low 32 bits of another. **==it is not safe to use shared mutable ``long`` and ``double`` variables in multithreaded programs unless they are declared ``volatile`` or guarded by a lock.==**

#### 3.1.3 Locking and visibility

Intrinsic locking can be used to guarantee that one thread sees the effects of another in a predictable manner When thread A executes a ``synchronized`` block, and subsequently thread B enters a ``synchronized`` block guarded by the same lock, the values of variables that were visible to A prior to releasing the lock are guaranteed to be visible to B upon acquiring the lock. In other words, everything A did in or prior to a ``synchronized`` block is visible to B when it executes a synchronized block guarded by the same lock. *Without synchronization, there is no such guarantee.*

![[Pasted image 20240708200422.png]]

**==Locking is not just about mutual exclusion; it is also about memory visibility. To ensure that all threads see the most up-to-date values of shared mutable variables, the reading and writing threads must synchronize on a common lock.==**

#### 3.1.4 Volatile variables

The Java language also provides an alternative, weaker form of synchronization, *volatile variables*, to ensure that updates to a variable are propagated predictably to other threads. When a field is declared ``volatile``, the compiler and runtime are put on notice that this variable is shared and that operations on it should not be reordered with other memory operations. **==Volatile variables are not cached in registers or in caches where they are hidden from other processors, so a read of a ``volatile`` variable always returns the most recent write by any thread.==**

**==accessing a ``volatile`` variable performs no locking and so cannot cause the executing thread to block, making volatile variables a lighter-weight synchronization mechanism than synchronized==** 

The visibility effects of ``volatile`` variables extend beyond the value of the ``volatile`` variable itself. When thread A writes to a ``volatile`` variable and subsequently thread B reads that same variable, the values of all variables that were visible to A prior to writing to the ``volatile`` variable become visible to B after reading the ``volatile`` variable. **==So from a memory visibility perspective, writing a ``volatile`` variable is like exiting a ``synchronized`` block and reading a ``volatile`` variable is like entering a ``synchronized`` block.==** code that relies on ``volatile`` variables for visibility of arbitrary state is more fragile and harder to understand than code that uses locking. 

**==Use ``volatile`` variables only when they simplify implementing and verifying your synchronization policy; avoid using ``volatile`` variables when verifying correctness would require subtle reasoning about visibility.==** Good uses of ``volatile`` variables include ensuring the visibility of their own state, that of the object they refer to, or indicating that an important lifecycle event (such as initialization or shutdown) has occurred.

```java
volatile boolean asleep;
...
while (!asleep)
	countSomeSheep();
```

Volatile variables are convenient, but they have limitations. **==The most common use for ``volatile`` variables is as a completion, interruption, or status flag==**, Volatile variables can be used for other kinds of state information, but more care is required when attempting this

**==Locking can guarantee both visibility and atomicity; volatile variables can only guarantee visibility.==**

You can use ``volatile`` variables only when all the following criteria are met:
**==• Writes to the variable do not depend on its current value, or you can ensure that only a single thread ever updates the value;**==
==**• The variable does not participate in invariants with other state variables; and**==
==**• Locking is not required for any other reason while the variable is being accessed.==**

### 3.2 Publication and escape

Publishing an object means making it available to code outside of its current scope, such as by storing a reference to it where other code can find it, returning it from a nonprivate method, or passing it to a method in another class. In many situations, we want to ensure that objects and their internals are not published. Publishing internal state variables can compromise encapsulation and make it more difficult to preserve invariants; publishing objects before they are fully constructed can compromise thread safety. An object that is published when it should not have been is said to have *escaped*. 

The most blatant form of publication is to store a reference in a ``public static`` field, where any class and thread could see it

```java
public static Set<Secret> knownSecrets;
public void initialize() {
	knownSecrets = new HashSet<Secret>();
}
```

Publishing one object may indirectly publish others. If you add a ``Secret`` to the published ``knownSecrets`` set, you’ve also published that ``Secret``, because any code can iterate the ``Set`` and obtain a reference to the new ``Secret``.

```java
class UnsafeStates {
	private String[] states = new String[] { "AK", "AL" ...};
	public String[] getStates() { return states; }
}
```

Publishing ``states`` in this way is problematic because any caller can modify its contents. what was supposed to be private state has been effectively made public.

Publishing an object also publishes any objects referred to by its non-private fields. **==More generally, any object that is reachable from a published object by following some chain of non-private field references and method calls has also been published.==**

From the perspective of a class C, an alien method is one whose behavior is not fully specified by C. This includes methods in other classes as well as overrideable methods (neither private nor final) in C itself. Passing an object to an alien method must also be considered publishing that object.

Once an object escapes, you have to assume that another class or thread may, maliciously or carelessly, misuse it. This is a compelling reason to use encapsulation: it makes it practical to analyze programs for correctness and harder to violate design constraints accidentally

A final mechanism by which an object or its internal state can be published is to publish an inner class instance

```java
public class ThisEscape {
	public ThisEscape(EventSource source) {
		source.registerListener(
			new EventListener() {
			public void onEvent(Event e) {
				doSomething(e);
			}
		});
	}
}
```

#### 3.2.1 Safe construction practices

``ThisEscape`` illustrates an important special case of escape—when the this references
escapes during construction. When the inner ``EventListener`` instance is published, so is the enclosing ``ThisEscape`` instance. But an object is in a predictable, consistent state only after its constructor returns, so publishing an object from within its constructor can publish an incompletely constructed object. This is true even if the publication is the last statement in the constructor. If the this reference escapes during construction, the object is considered *not properly constructed*.

> **Do not allow the this reference to escape during construction.**

A common mistake that can let the this reference escape during construction is to start a thread from a constructor. When an object creates a thread from its constructor, it almost always shares its this reference with the new thread, either explicitly (by passing it to the constructor) or implicitly (because the Thread or Runnable is an inner class of the owning object). The new thread might then be able to see the owning object before it is fully constructed. There’s nothing wrong with creating a thread in a constructor, but it is best not to start the thread immediately. Instead, expose a start or initialize method that starts the owned thread. 

Calling an overrideable instance method (one that is neither ``private`` nor ``final``) from the constructor can also allow the ``this`` reference to escape.

If you are tempted to register an event listener or start a thread from a constructor, you can avoid the improper construction by using a private constructor and a public factory method

```java
public class SafeListener {
	private final EventListener listener;
		private SafeListener() {
		listener = new EventListener() {
			public void onEvent(Event e) {
				doSomething(e);
			}
		};
	}
	public static SafeListener newInstance(EventSource source) {
		SafeListener safe = new SafeListener();
		source.registerListener(safe.listener);
		return safe;
	}
}
```

### 3.3 Thread confinement

Accessing shared, mutable data requires using synchronization; one way to avoid this requirement is to not share. If data is only accessed from a single thread, no synchronization is needed. **==This technique, thread confinement, is one of the simplest ways to achieve thread safety==**. When an object is confined to a thread, such usage is automatically thread-safe even if the confined object itself is not

Thread confinement is an element of your program’s design that must be enforced by its implementation. The language and core libraries provide mechanisms that can help in maintaining thread confinement—local variables and the ``ThreadLocal`` class—but even with these, it is still the programmer’s responsibility to ensure that thread-confined objects do not escape from their intended thread.

#### 3.3.1 Ad-hoc thread confinement

Ad-hoc thread confinement describes when the responsibility for maintaining thread confinement falls entirely on the implementation. Ad-hoc thread confinement can be fragile because none of the language features, such as visibility modifiers or local variables, helps confine the object to the target thread. In fact, references to thread-confined objects such as visual components or data models in GUI applications are often held in public fields

The decision to use thread confinement is often a consequence of the decision to implement a particular subsystem Single-threaded subsystems can sometimes offer a simplicity benefit that outweighs the fragility of ad-hoc thread confinement

A special case of thread confinement applies to ``volatile`` variables. It is safe to perform read-modify-write operations on shared volatile variables as long as you ensure that the volatile variable is only written from a single thread. In this case, you are confining the modification to a single thread to prevent race conditions, and the visibility guarantees for volatile variables ensure that other threads see the most up-to-date value.

Because of its fragility, ad-hoc thread confinement should be used sparingly; if possible, use one of the stronger forms of thread confinement instead

#### 3.3.2 Stack confinement

Stack confinement is a special case of thread confinement in which an object can only be reached through local variables. Just as encapsulation can make it easier to preserve invariants, local variables can make it easier to confine objects to a thread. Local variables are intrinsically confined to the executing thread; they exist on the executing thread’s stack, which is not accessible to other threads. Stack confinement s simpler to maintain and less fragile than ad-hoc thread confinement.

```java
public int loadTheArk(Collection<Animal> candidates) {
    SortedSet<Animal> animals;
    int numPairs = 0;
    Animal candidate = null;

    // animals confined to method, don’t let them escape!
    animals = new TreeSet<Animal>(new SpeciesGenderComparator());
    animals.addAll(candidates);

    for (Animal a : animals) {
        if (candidate == null || !candidate.isPotentialMate(a)) {
            candidate = a;
        } else {
            ark.load(new AnimalPair(candidate, a));
            ++numPairs;
            candidate = null;
        }
    }

    return numPairs;
}
```

Maintaining stack confinement for object references requires a little more assistance from the programmer to ensure that the referent does not escape. 

Using a non-thread-safe object in a within-thread context is still thread-safe. However, be careful: the design requirement that the object be confined to the executing thread, or the awareness that the confined object is not thread-safe, often exists only in the head of the developer when the code is written. If the assumption of within-thread usage is not clearly documented, future maintainers might mistakenly allow the object to escape.
#### 3.3.3 ``ThreadLocal``

A more formal means of maintaining thread confinement is ``ThreadLocal``, which allows you to associate a per-thread value with a value-holding object. Thread- Local provides get and set accessor methods that maintain a separate copy of the value for each thread that uses it, so a get returns the most recent value passed to set from the currently executing thread.

**==Thread-local variables are often used to prevent sharing in designs based on mutable Singletons or global variables==**. For example, a single-threaded application might maintain a global database connection that is initialized at startup to avoid having to pass a Connection to every method. Since JDBC connections may not be thread-safe, a multithreaded application that uses a global connection without additional coordination is not thread-safe either

```java
public int loadTheArk(Collection<Animal> candidates) {
    SortedSet<Animal> animals;
    int numPairs = 0;
    Animal candidate = null;

    // animals confined to method, don’t let them escape!
    animals = new TreeSet<Animal>(new SpeciesGenderComparator());
    animals.addAll(candidates);

    for (Animal a : animals) {
        if (candidate == null || !candidate.isPotentialMate(a)) {
            candidate = a;
        } else {
            ark.load(new AnimalPair(candidate, a));
            ++numPairs;
            candidate = null;
        }
    }

    return numPairs;
}
```

This technique can also be used when a frequently used operation requires a temporary object such as a buffer and wants to avoid reallocating the temporary object on each invocation. 

When a thread calls ``ThreadLocal.get`` for the first time, ``initialValue`` is consulted to provide the initial value for that thread. Conceptually, you can think of a ``ThreadLocal<T>`` as holding a ``Map<Thread,T>`` that stores the thread-specific values, though this is not how it is actually implemented. The thread-specific values are stored in the Thread object itself; when the thread terminates, the thread-specific values can be garbage collected.

**==If you are porting a single-threaded application to a multithreaded environment, you can preserve thread safety by converting shared global variables into ``ThreadLocal``s==**, if the semantics of the shared globals permits this; an applicationwide cache would not be as useful if it were turned into a number of thread-local caches.

It is easy to abuse ``ThreadLocal`` by treating its thread confinement property as a license to use global variables or as a means of creating “hidden” method arguments. Like global variables, thread-local variables can detract from reusability and introduce hidden couplings among classes, and should therefore be used with care.

### 3.4 Immutability

The other end-run around the need to synchronize is to use immutable objects. Nearly all the atomicity and visibility hazards such as seeing stale values, losing updates, or observing an object to be in an inconsistent state, have to do with the vagaries of multiple threads trying to access the same mutable state at the same time. If an object’s state cannot be modified, these risks and complexities simply go away.

Immutable objects are inherently thread-safe; their invariants are established by the constructor, and if their state cannot be changed, these invariants always hold.

> **==Immutable objects are always thread-safe.==**

Immutable objects are simple. They can only be in one state, which is carefully controlled by the constructor. One of the most difficult elements of program design is reasoning about the possible states of complex objects. Reasoning about the state of immutable objects, on the other hand, is trivial. An object whose fields are all final may still be mutable, since final fields can hold references to mutable objects.

**==An object is immutable if:**==
==**• Its state cannot be modified after construction;**==
==**• All its fields are final; and**==
==**• It is properly constructed (the this reference does not escape during construction).==**

```java
@Immutable
public final class ThreeStooges {
	private final Set<String> stooges = new HashSet<String>();
		public ThreeStooges() {
		stooges.add("Moe");
		stooges.add("Larry");
		stooges.add("Curly");
	}
	public boolean isStooge(String name) {
		return stooges.contains(name);
	}
}
```

Because program state changes all the time, you might be tempted to think that immutable objects are of limited use, but this is not the case. There is a difference between an object being immutable and the reference to it being immutable. Program state stored in immutable objects can still be updated by “replacing” immutable objects with a new instance holding new state;

#### 3.4.1 Final fields

Final fields can’t be modified, but they also have special semantics under the Java Memory Model. It is the use of final fields that makes possible the guarantee of initialization safety that lets immutable objects be freely accessed and shared without synchronization. Even if an object is mutable, making some fields final can still simplify reasoning about its state, since limiting the mutability of an object restricts its set of possible states. An object that is “mostly immutable” but has one or two mutable state variables is still simpler than one that has many mutable variables

> **Just as it is a good practice to make all fields private unless they need greater visibility ], it is a good practice to make all fields final unless they need to be mutable.**

#### 3.4.2 Example: Using volatile to publish immutable objects

Using ``volatile`` variables for these values would not be thread-safe for the same reason. However, immutable objects can sometimes provide a weak form of atomicity. Race conditions in accessing or updating multiple related variables can be eliminated by using an immutable object to hold all the variables

```java
@Immutable
class OneValueCache {
	private final BigInteger lastNumber;
	private final BigInteger[] lastFactors;
	public OneValueCache(BigInteger i,BigInteger[] factors) {
		lastNumber = i;
		lastFactors = Arrays.copyOf(factors, factors.length);
	}
	public BigInteger[] getFactors(BigInteger i) {
		if (lastNumber == null || !lastNumber.equals(i))
			return null;
		else
			return Arrays.copyOf(lastFactors, lastFactors.length);
	}
}
```

### 3.5 Safe publication

```java
@ThreadSafe
public class VolatileCachedFactorizer implements Servlet {
	private volatile OneValueCache cache = new OneValueCache(null, null);
	public void service(ServletRequest req, ServletResponse resp) {
		BigInteger i = extractFromRequest(req);
		BigInteger[] factors = cache.getFactors(i);
		if (factors == null) {
			factors = factor(i);
			cache = new OneValueCache(i, factors);
		}
		encodeIntoResponse(resp, factors);
	}
}
```

```java
// Unsafe publication
public Holder holder;
public void initialize() {
holder = new Holder(42);
}
```

Because of visibility problems, the ``Holder`` could appear to another thread to be in an inconsistent state, even though its invariants were properly established by its constructor! This improper publication could allow another thread to observe a partially constructed object.
#### 3.5.1 Improper publication: when good objects go bad

```java
public class Holder {
	private int n;
	public Holder(int n) { this.n = n; }
	public void assertSanity() {
		if (n != n)
			throw new AssertionError("This statement is false.");
	}
}
```

Two things can go wrong with improperly published objects. Other threads could see a stale value for the holder field, and thus see a ``null`` reference or other older value even though a value has been placed in ``holder``. But far worse, other threads could see an up-to date value for the holder reference, but stale values for the state of the ``Holder``. To make things even less predictable, a thread may see a stale value the first time it reads a field and then a more up-to-date value the next time, which is why ``assertSanity`` can throw ``AssertionError``.
#### 3.5.2 Immutable objects and initialization safety

Because immutable objects are so important, the Java Memory Model offers a special guarantee of initialization safety for sharing immutable objects. As we’ve seen, that an object reference becomes visible to another thread does not necessarily mean that the state of that object is visible to the consuming thread. In order to guarantee a consistent view of the object’s state, synchronization is needed.

Immutable objects, on the other hand, can be safely accessed even when synchronization is not used to publish the object reference. For this guarantee of initialization safety to hold, all of the requirements for immutability must be met: unmodifiable state, all fields are final, and proper construction.

> **Immutable objects can be used safely by any thread without additional synchronization, even when synchronization is not used to publish them.**

final fields can be safely accessed without additional synchronization. However, if final fields refer to mutable objects, synchronization is still required to access the state of the objects they refer to.

#### 3.5.3 Safe publication idioms

Objects that are not immutable must be safely published, which usually entails synchronization by both the publishing and the consuming thread

**==To publish an object safely, both the reference to the object and the object’s state must be made visible to other threads at the same time. A properly constructed object can be safely published by:**==
==**• Initializing an object reference from a static initializer;**==
==**• Storing a reference to it into a volatile field or ``AtomicReference``;**==
==**• Storing a reference to it into a final field of a properly constructed object; or**==
==**• Storing a reference to it into a field that is properly guarded by a lock.==**

The internal synchronization in thread-safe collections means that placing an object in a thread-safe collection, such as a ``Vector`` or ``synchronizedList``, fulfills the last of these requirements.

The thread-safe library collections offer the following safe publication guarantees, even if the Javadoc is less than clear on the subject:

**==• Placing a key or value in a Hashtable, ``synchronizedMap``, or Concurrent- Map safely publishes it to any thread that retrieves it from the Map (whether directly or via an iterator);**==

==**• Placing an element in a Vector, ``CopyOnWriteArrayList``, ``CopyOnWrite- ArraySet``, ``synchronizedList``, or ``synchronizedSet`` safely publishes it to any thread that retrieves it from the collection;**==

==**• Placing an element on a ``BlockingQueue`` or a ``ConcurrentLinkedQueue`` safely publishes it to any thread that retrieves it from the queue.==**

Using a static initializer is often the easiest and safest way to publish objects that can be statically constructed:

```java
public static Holder holder = new Holder(42);
```

#### 3.5.4 Effectively immutable objects

> **Safely published effectively immutable objects can be used safely by any thread without additional synchronization.**

For example, ``Date`` is mutable, but if you use it as if it were immutable, you may be able to eliminate the locking that would otherwise be required when sharing a ``Date`` across threads.

```java
public Map<String, Date> lastLogin = Collections.synchronizedMap(new HashMap<String, Date>());
```

If the ``Date`` values are not modified after they are placed in the ``Map``, then the synchronization in the ``synchronizedMap`` implementation is sufficient to publish the ``Date`` values safely, and no additional synchronization is needed when accessing them.
#### 3.5.5 Mutable objects

If an object may be modified after construction, safe publication ensures only the visibility of the as-published state. Synchronization must be used not only to publish a mutable object, but also every time the object is accessed to ensure visibility of subsequent modifications. To share mutable objects safely, they must be safely published and be either thread-safe or guarded by a lock.

> **==The publication requirements for an object depend on its mutability:**==
	==**• Immutable objects can be published through any mechanism;**==
	==**• Effectively immutable objects must be safely published;**==
	==**• Mutable objects must be safely published, and must be either thread-safe or guarded by a lock.==**

#### 3.5.6 Sharing objects safely

Whenever you acquire a reference to an object, you should know what you are allowed to do with it. Many concurrency errors stem from failing to understand these “rules of engagement” for a shared object. When you publish an object, you should document how the object can be accessed.

The most useful policies for using and sharing objects in a concurrent program are:

**Thread-confined**. A thread-confined object is owned exclusively by and confined to one thread, and can be modified by its owning thread.

**Shared read-only**. A shared read-only object can be accessed concurrently by multiple threads without additional synchronization, but cannot be modified by any thread. Shared read-only objects include immutable and effectively immutable objects. Shared thread-safe. A thread-safe object performs synchronization internally, so multiple threads can freely access it through its public interface without further synchronization.

**Guarded**. A guarded object can be accessed only with a specific lock held. Guarded objects include those that are encapsulated within other thread-safe objects and published objects that are known to be guarded by a specific lock.
## Composing Objects

### 4.1 Designing a thread-safe class

**==The design process for a thread-safe class should include these three basic elements:**==
==**• Identify the variables that form the object’s state;**==
==**• Identify the invariants that constrain the state variables;**==
==**• Establish a policy for managing concurrent access to the object’s state.==**

An object’s state starts with its fields. If they are all of primitive type, the fields comprise the entire state. The state of an object with n primitive fields is just the n-tuple of its field values; the state of a 2D Point is its (x, y) value. If the object has fields that are references to other objects, its state will encompass fields from the referenced objects as well.

```java
@ThreadSafe
public final class Counter {
	@GuardedBy("this") private long value = 0;
	public synchronized long getValue() {
		return value;
	}
	public synchronized long increment() {
		if (value == Long.MAX_VALUE)
			throw new IllegalStateException("counter overflow");
		return ++value;
	}
}
```

The synchronization policy defines how an object coordinates access to its state without violating its invariants or postconditions. It specifies what combination of immutability, thread confinement, and locking is used to maintain thread safety, and which variables are guarded by which locks. To ensure that the class can be analyzed and maintained, document the synchronization policy.
#### 4.1.1 Gathering synchronization requirements

Making a class thread-safe means ensuring that its invariants hold under concurrent access; this requires reasoning about its state. Objects and variables have a state space: the range of possible states they can take on. The smaller this state space, the easier it is to reason about. By using final fields wherever practical, you make it simpler to analyze the possible states an object can be in.

Constraints placed on states or state transitions by invariants and postconditions create additional synchronization or encapsulation requirements. If certain states are invalid, then the underlying state variables must be encapsulated, otherwise client code could put the object into an invalid state. If an operation has invalid state transitions, it must be made atomic

Multivariable invariants create atomicity requirements: related variables must be fetched or updated in a single atomic operation. You cannot update one, release and reacquire the lock, and then update the others, since this could involve leaving the object in an invalid state when the lock was released. When multiple variables participate in an invariant, the lock that guards them must be held for the duration of any operation that accesses the related variables.

> **You cannot ensure thread safety without understanding an object’s invariants and postconditions. Constraints on the valid values or state transitions for state variables can create atomicity and encapsulation requirements.**

#### 4.1.2 State-dependent operations

Class invariants and method postconditions constrain the valid states and state transitions for an object. Some objects also have methods with state-based preconditions. For example, you cannot remove an item from an empty queue; a queue must be in the “nonempty” state before you can remove an element. Operations with state-based preconditions are called state-dependent

In a single-threaded program, if a precondition does not hold, the operation has no choice but to fail. But in a concurrent program, the precondition may become true later due to the action of another thread. Concurrent programs add the possibility of waiting until the precondition becomes true, and then proceeding with the operation.

The built-in mechanisms for efficiently waiting for a condition to become true—wait and notify—are tightly bound to intrinsic locking, and can be difficult to use correctly. To create operations that wait for a precondition to become true before proceeding, it is often easier to use existing library classes, such as

#### 4.1.3 State ownership

When defining which variables form an object’s state, we want to consider only the data that object owns. Ownership is not embodied explicitly in the language, but is instead an element of class design. If you allocate and populate a ``HashMap``, you are creating multiple objects: the ``HashMap`` object, a number of ``Map.Entry`` objects used by the implementation of ``HashMap``, and perhaps other internal objects as well. The logical state of a ``HashMap`` includes the state of all its ``Map.Entry`` and internal objects, even though they are implemented as separate objects. 
For better or worse, garbage collection lets us avoid thinking carefully about ownership. In Java, all these same ownership models are possible, but the garbage collector reduces the cost of many of the common errors in reference sharing, enabling less-than-precise thinking about ownership

In many cases, ownership and encapsulation go together—the object encapsulates the state it owns and owns the state it encapsulates. It is the owner of a given state variable that gets to decide on the locking protocol used to maintain the integrity of that variable’s state. Ownership implies control, but once you publish a reference to a mutable object, you no longer have exclusive control; at best, you might have “shared ownership”.

Collection classes often exhibit a form of “split ownership”, in which the collection owns the state of the collection infrastructure, but client code owns the objects stored in the collection

### 4.2 Instance confinement

If an object is not thread-safe, several techniques can still let it be used safely in a multithreaded program. You can ensure that it is only accessed from a single thread (thread confinement), or that all access to it is properly guarded by a lock.

Encapsulation simplifies making classes thread-safe by promoting instance confinement, often just called confinement. When an object is encapsulated within another object, all code paths that have access to the encapsulated object are known and can be therefore be analyzed more easily than if that object were accessible to the entire program.

> **Encapsulating data within an object confines access to the data to the object’s methods, making it easier to ensure that the data is always accessed with the appropriate lock held.**

Confined objects must not escape their intended scope. An object may be confined to a class instance (such as a private class member), a lexical scope (such as a local variable), or a thread (such as an object that is passed from method to method within a thread, but not supposed to be shared across threads).

```java
@ThreadSafe
public class PersonSet {
	@GuardedBy("this")
	private final Set<Person> mySet = new HashSet<Person>();
	public synchronized void addPerson(Person p) {
		mySet.add(p);
	}
	public synchronized boolean containsPerson(Person p) {
		return mySet.contains(p);
	}
}
```

This example makes no assumptions about the thread-safety of ``Person``, but if it is mutable, additional synchronization will be needed when accessing a ``Person`` retrieved from a ``PersonSet``. The most reliable way to do this would be to make ``Person`` thread-safe; less reliable would be to guard the ``Person`` objects with a lock and ensure that all clients follow the protocol of acquiring the appropriate lock before accessing the ``Person``.

Instance confinement is one of the easiest ways to build thread-safe classes. It also allows flexibility in the choice of locking strategy; ``PersonSet`` happened to use its own intrinsic lock to guard its state, but any lock, consistently used, would do just as well. Instance confinement also allows different state variables to be guarded by different locks.

it is still possible to violate confinement by publishing a supposedly confined object; if an object is intended to be confined to a specific scope, then letting it escape from that scope is a bug. Confined objects can also escape by publishing other objects such as iterators or inner class instances that may indirectly publish the confined objects.

> **Confinement makes it easier to build thread-safe classes because a class that confines its state can be analyzed for thread safety without having to examine the whole program.**

#### 4.2.1 The Java monitor pattern

An object following the Java monitor pattern encapsulates all its mutable state and guards it with the object’s own intrinsic lock. The Java monitor pattern is used by many library classes, such as ``Vector`` and ``Hashtable``.

```java
public class PrivateLock {
	private final Object myLock = new Object();
	@GuardedBy("myLock") Widget widget;
	void someMethod() {
		synchronized(myLock) {
		// Access or modify the state of widget
		}
	}
}
```

There are advantages to using a private lock object instead of an object’s intrinsic lock (or any other publicly accessible lock). **==Making the lock object private encapsulates the lock so that client code cannot acquire it, whereas a publicly accessible lock allows client code to participate in its synchronization policy— correctly or incorrectly.==** Clients that improperly acquire another object’s lock could cause liveness problems, and verifying that a publicly accessible lock is properly used requires examining the entire program rather than a single class.

### 4.3 Delegating thread safety

All but the most trivial objects are composite objects. The Java monitor pattern is useful when building classes from scratch or composing classes out of objects that are not thread-safe. But what if the components of our class are already thread-safe? Do we need to add an additional layer of thread safety? The answer is . . . “it depends”.

```java
@ThreadSafe
public class MonitorVehicleTracker {
    @GuardedBy("this")
    private final Map<String, MutablePoint> locations;

    public MonitorVehicleTracker(Map<String, MutablePoint> locations) {
        this.locations = deepCopy(locations);
    }

    public synchronized Map<String, MutablePoint> getLocations() {
        return deepCopy(locations);
    }

    public synchronized MutablePoint getLocation(String id) {
        MutablePoint loc = locations.get(id);
        return loc == null ? null : new MutablePoint(loc);
    }

    public synchronized void setLocation(String id, int x, int y) {
        MutablePoint loc = locations.get(id);
        if (loc == null)
            throw new IllegalArgumentException("No such ID: " + id);
        loc.x = x;
        loc.y = y;
    }

    private static Map<String, MutablePoint> deepCopy(Map<String, MutablePoint> m) {
        Map<String, MutablePoint> result = new HashMap<String, MutablePoint>();
        for (String id : m.keySet())
            result.put(id, new MutablePoint(m.get(id)));
        return Collections.unmodifiableMap(result);
    }
}

public class MutablePoint { 
    // Listing 4.5
}
```

```java
@NotThreadSafe
public class MutablePoint {
	public int x, y;
	public MutablePoint() { x = 0; y = 0; }
	public MutablePoint(MutablePoint p) {
		this.x = p.x;
		this.y = p.y;
	}
}
```

#### 4.3.1 Example: vehicle tracker using delegation

```java
@Immutable
public class Point {
	public final int x, y;
	public Point(int x, int y) {
		this.x = x;
		this.y = y;
	}
}
```

Point is thread-safe because it is immutable. Immutable values can be freely shared and published, so we no longer need to copy the locations when returning them.

```java
@ThreadSafe
public class DelegatingVehicleTracker {
    private final ConcurrentMap<String, Point> locations;
    private final Map<String, Point> unmodifiableMap;

    public DelegatingVehicleTracker(Map<String, Point> points) {
        locations = new ConcurrentHashMap<String, Point>(points);
        unmodifiableMap = Collections.unmodifiableMap(locations);
    }

    public Map<String, Point> getLocations() {
        return unmodifiableMap;
    }

    public Point getLocation(String id) {
        return locations.get(id);
    }

    public void setLocation(String id, int x, int y) {
        if (locations.replace(id, new Point(x, y)) == null)
            throw new IllegalArgumentException("invalid vehicle name: " + id);
    }
}
```

```java
public Map<String, Point> getLocations() {
	return Collections.unmodifiableMap( new HashMap<String, Point>(locations));
}
```

#### 4.3.2 Independent state variables

can also delegate thread safety to more than one underlying state variable as long as those underlying state variables are independent, meaning that the composite class does not impose any invariants involving the multiple state variables.

```java
public class VisualComponent {
    private final List<KeyListener> keyListeners = new CopyOnWriteArrayList<KeyListener>();
    private final List<MouseListener> mouseListeners = new CopyOnWriteArrayList<MouseListener>();

    public void addKeyListener(KeyListener listener) {
        keyListeners.add(listener);
    }

    public void addMouseListener(MouseListener listener) {
        mouseListeners.add(listener);
    }

    public void removeKeyListener(KeyListener listener) {
        keyListeners.remove(listener);
    }

    public void removeMouseListener(MouseListener listener) {
        mouseListeners.remove(listener);
    }
}
```

#### 4.3.3 When delegation fails

Most composite classes are not as simple as ``VisualComponent``: they have invariants that relate their component state variables

```java
public class NumberRange {
    // INVARIANT: lower <= upper
    private final AtomicInteger lower = new AtomicInteger(0);
    private final AtomicInteger upper = new AtomicInteger(0);

    public void setLower(int i) {
        // Warning -- unsafe check-then-act
        if (i > upper.get())
            throw new IllegalArgumentException("can’t set lower to " + i + " > upper");
        lower.set(i);
    }

    public void setUpper(int i) {
        // Warning -- unsafe check-then-act
        if (i < lower.get())
            throw new IllegalArgumentException("can’t set upper to " + i + " < lower");
        upper.set(i);
    }

    public boolean isInRange(int i) {
        return (i >= lower.get() && i <= upper.get());
    }
}
```

If a class has compound actions, as ``NumberRange`` does, delegation alone is again not a suitable approach for thread safety. In these cases, the class must provide its own locking to ensure that compound actions are atomic, unless the entire compound action can also be delegated to the underlying state variables.

> If a class is composed of multiple independent thread-safe state variables and has no operations that have any invalid state transitions, then it can delegate thread safety to the underlying state variables.

#### 4.3.4 Publishing underlying state variables

When you delegate thread safety to an object’s underlying state variables, under what conditions can you publish those variables so that other classes can modify them as well? Again, the answer depends on what invariants your class imposes on those variables.

> **If a state variable is thread-safe, does not participate in any invariants that constrain its value, and has no prohibited state transitions for any of its operations, then it can safely be published.**

### 4.4 Adding functionality to existing thread-safe classes

The Java class library contains many useful “building block” classes. Reusing existing classes is often preferable to creating new ones: reuse can reduce development effort, development risk (because the existing components are already tested), and maintenance cost. Sometimes a thread-safe class that supports all of the operations we want already exists, but often the best we can find is a class that supports almost all the operations we want, and then we need to add a new operation to it without undermining its thread safety.

The concept of put-if-absent is straightforward enough—check to see if an element is in the collection before adding it, and do not add it if it is already there

The requirement that the class be thread-safe implicitly adds another requirement—that operations like put-if-absent be atomic. Any reasonable interpretation suggests that, if you take a List that does not contain object X, and add X twice with put-if-absent, the resulting collection contains only one copy of X. But, if put-if-absent were not atomic, with some unlucky timing two threads could both see that X was not present and both add X, resulting in two copies of X.

The safest way to add a new atomic operation is to modify the original class to support the desired operation, but this is not always possible because you may not have access to the source code or may not be free to modify it.

Adding the new method directly to the class means that all the code that implements the synchronization policy for that class is still contained in one source file, facilitating easier comprehension and maintenance.

Extension is more fragile than adding code directly to a class, because the implementation of the synchronization policy is now distributed over multiple, separately maintained source files. If the underlying class were to change its synchronization policy by choosing a different lock to guard its state variables, the subclass would subtly and silently break, because it no longer used the right lock to control concurrent access to the base class’s state.

```java
@ThreadSafe
public class BetterVector<E> extends Vector<E> {
	public synchronized boolean putIfAbsent(E x) {
		boolean absent = !contains(x);
		if (absent)
			add(x);
		return absent;
	}
}
```

#### 4.4.1 Client-side locking

A third strategy is to extend the functionality of the class without extending the class itself by placing extension code in a “helper” class.

```java
@NotThreadSafe
public class ListHelper<E> {
	public List<E> list = Collections.synchronizedList(new ArrayList<E>());
	...
	public synchronized boolean putIfAbsent(E x) {
		boolean absent = !list.contains(x);
		if (absent)
			list.add(x);
		return absent;
	}
}
```

Why wouldn’t this work? The problem is that it synchronizes on the wrong lock. Whatever lock the ``List`` uses to guard its state, it sure isn’t the lock on the ``ListHelper``. ``ListHelper`` provides only the illusion of synchronization; the various list operations, while all synchronized, use different locks, which means that ``putIfAbsent`` is not atomic relative to other operations on the ``List``.

To make this approach work, we have to use the same lock that the List uses by using client-side locking or external locking. Client-side locking entails guarding client code that uses some object X with the lock X uses to guard its own state. In order to use client-side locking, you must know what lock X uses.

```java
@ThreadSafe
public class ListHelper<E> {
	public List<E> list = Collections.synchronizedList(new ArrayList<E>());
	...
	public boolean putIfAbsent(E x) {
		synchronized (list) {
			boolean absent = !list.contains(x);
			if (absent)
				list.add(x);
			return absent;
		}
	}
}
```

If extending a class to add another atomic operation is fragile because it distributes the locking code for a class over multiple classes in an object hierarchy, client-side locking is even more fragile because it entails putting locking code for class C into classes that are totally unrelated to C.

#### 4.4.2 Composition

There is a less fragile alternative for adding an atomic operation to an existing class: composition.

```java
@ThreadSafe
public class ImprovedList<T> implements List<T> {
	private final List<T> list;
	public ImprovedList(List<T> list) { this.list = list; }
	public synchronized boolean putIfAbsent(T x) {
		boolean contains = list.contains(x);
		if (contains)
			list.add(x);
		return !contains;
	}
	public synchronized void clear() { list.clear(); }
	// ... similarly delegate other List methods
}
```

### 4.5 Documenting synchronization policies

Documentation is one of the most powerful (and, sadly, most underutilized) tools for managing thread safety. Users look to the documentation to find out if a class is thread-safe, and maintainers look to the documentation to understand the implementation strategy so they can maintain it without inadvertently compromising safety.

 Each use of ``synchronized``, ``volatile``, or any thread-safe class reflects a synchronization policy defining a strategy for ensuring the integrity of data in the face of concurrent access. That policy is an element of your program’s design, and should be documented. 

Crafting a synchronization policy requires a number of decisions: which variables to make ``volatile``, which variables to guard with locks, which lock(s) guard which variables, which variables to make immutable or confine to a thread, which operations must be atomic, etc. Some of these are strictly implementation details and should be documented for the sake of future maintainers, but some affect the publicly observable locking behavior of your class and should be documented as part of its specification.

## Building Blocks

### 5.1 Synchronized collections

The synchronized collection classes include ``Vector`` and ``Hashtable``, part of the original JDK, as well as their cousins added in JDK 1.2, the synchronized wrapper classes created by the ``Collections.synchronizedXxx`` factory methods. These classes achieve thread safety by encapsulating their state and synchronizing every public method so that only one thread at a time can access the collection state.

#### 5.1.1 Problems with synchronized collections

The synchronized collections are thread-safe, but you may sometimes need to use additional client-side locking to guard compound actions. Common compound actions on collections include iteration, navigation, and conditional operations such as put-if-absent .  With a synchronized collection, these compound actions are still technically thread-safe even without client-side locking, but they may not behave as you might expect when other threads can concurrently modify the collection.

```java
public static Object getLast(Vector list) {
	int lastIndex = list.size() - 1;
	return list.get(lastIndex);
}
public static void deleteLast(Vector list) {
	int lastIndex = list.size() - 1;
	list.remove(lastIndex);
}
```

f thread A calls ``getLast`` on a Vector with ten elements, thread B calls ``deleteLast`` on the same Vector, and the operations are interleaved ``getLast`` throws ``ArrayIndexOutOfBoundsException``. Between the call to size and the subsequent call to get in ``getLast``, the Vector shrank and the index computed in the first step is no longer valid. This is perfectly consistent with the specification of Vector—it throws an exception if asked for a nonexistent element.

Because the synchronized collections commit to a synchronization policy that supports client-side locking,1 it is possible to create new operations that are atomic with respect to other collection operations as long as we know which lock to use. The synchronized collection classes guard each method with the lock on the synchronized collection object itself. By acquiring the collection lock we can make ``getLast`` and ``deleteLast`` atomic, ensuring that the size of the Vector does not change between calling size and get, as shown in Listing 5.2. The risk that the size of the list might change between a call to size and the corresponding call to get is also present when we iterate through the elements of a Vector

![[Pasted image 20240709195919.png]]

```java
public static Object getLast(Vector list) {
	synchronized (list) {
		int lastIndex = list.size() - 1;
		return list.get(lastIndex);
	}
}
public static void deleteLast(Vector list) {
	synchronized (list) {
		int lastIndex = list.size() - 1;
		list.remove(lastIndex);
	}
}
```

Even though the iteration can throw an exception, this doesn’t mean Vector isn’t thread-safe. The state of the Vector is still valid and the exception is in fact in conformance with its specification.

The problem of unreliable iteration can again be addressed by client-side locking, at some additional cost to scalability. By holding the Vector lock for the duration of iteration we prevent other threads from modifying
the Vector while we are iterating it. Unfortunately, we also prevent other threads from accessing it at all during this time, impairing concurrency.

```java
synchronized (vector) {
	for (int i = 0; i < vector.size(); i++)
		doSomething(vector.get(i));
}
```

#### 5.1.2 Iterators and ``ConcurrentModificationException``

the more “modern” collection classes do not eliminate the problem of compound actions. The standard way to iterate a Collection is with an Iterator, either explicitly or through the for-each loop syntax introduced in Java 5.0, but using iterators does not obviate the need to lock the collection during iteration if other threads can concurrently modify it. The iterators returned by the synchronized collections are not designed to deal with concurrent modification, and they are fail-fast—meaning that if they detect that the collection has changed since iteration began, they throw the unchecked ``ConcurrentModificationException``.

These fail-fast iterators are not designed to be foolproof—they are designed to catch concurrency errors on a “good-faith-effort” basis and thus act only as early-warning indicators for concurrency problems.

```java
List<Widget> widgetList = Collections.synchronizedList(new ArrayList<Widget>());
...
// May throw ConcurrentModificationException
for (Widget w : widgetList)
	doSomething(w);
```

There are several reasons, however, why locking a collection during iteration may be undesirable. Other threads that need to access the collection will block until the iteration is complete; if the collection is large or the task performed for each element is lengthy, they could wait a long time. Also, if the collection is locked ``doSomething`` is being called with a lock held, which is a risk factor for deadlock. Even in the absence of starvation or deadlock risk, locking collections for significant periods of time hurts application scalability. The longer a lock is held, the more likely it is to be contended, and if many threads are blocked waiting for a lock throughput and CPU utilization can suffer

An alternative to locking the collection during iteration is to clone the collection and iterate the copy instead. Since the clone is thread-confined, no other thread can modify it during iteration, eliminating the possibility of ``Concurrent- ModificationException``

Cloning the collection has an obvious performance cost; whether this is a favorable tradeoff depends on many factors including the size of the collection, how much work is done for each element, the relative frequency of iteration compared to other collection operations, and responsiveness and throughput requirements.

#### 5.1.3 Hidden iterators

you have to remember to use locking everywhere a shared collection might be iterated. This is trickier than it sounds, as iterators are sometimes hidden 

There is no explicit iteration in Hidden-Iterator, but the code in bold entails iteration just the same. The string concatenation gets turned by the compiler into a call to ``StringBuilder.append(Object)``, which in turn invokes the collection’s ``toString`` method—and the implementation of ``toString`` in the standard collections iterates the collection and calls ``toString`` on each element to produce a nicely formatted representation of the collection’s contents.

the real problem is that ``HiddenIterator`` is not thread-safe; the ``HiddenIterator`` lock should be acquired before using set in the ``println`` call, but debugging and logging code commonly neglect to do this. The real lesson here is that the greater the distance between the state and the synchronization that guards it, the more likely that someone will forget to use proper synchronization when accessing that state. If ``HiddenIterator`` wrapped the ``HashSet`` with a ``synchronizedSet``, encapsulating the synchronization, this sort of error would not occur.

> **Just as encapsulating an object’s state makes it easier to preserve its invariants, encapsulating its synchronization makes it easier to enforce its**

```java
public class HiddenIterator {
    @GuardedBy("this")
    private final Set<Integer> set = new HashSet<Integer>();

    public synchronized void add(Integer i) { 
        set.add(i); 
    }

    public synchronized void remove(Integer i) { 
        set.remove(i); 
    }

    public void addTenThings() {
        Random r = new Random();
        for (int i = 0; i < 10; i++)
            add(r.nextInt());
        System.out.println("DEBUG: added ten elements to " + set);
    }
}
```

Iteration is also indirectly invoked by the collection’s ``hashCode`` and equals methods, which may be called if the collection is used as an element or key of another collection. 

### 5.2 Concurrent collections

Synchronized collections achieve their thread safety by serializing all access to the collection’s state. The cost of this approach is poor concurrency; when multiple threads contend for the collection-wide lock, throughput suffers. The concurrent collections, on the other hand, are designed for concurrent access from multiple threads.

The new ``ConcurrentMap`` interface adds support for common compound actions such as put-if-absent, replace, and conditional remove.

> **Replacing synchronized collections with concurrent collections can offer dramatic scalability improvements with little risk.**

``BlockingQueue`` extends ``Queue`` to add blocking insertion and retrieval operations. If the queue is empty, a retrieval blocks until an element is available, and if the queue is full (for bounded queues) an insertion blocks until there is space available. Blocking queues are extremely useful in producer-consumer designs

#### 5.2.1 ``ConcurrentHashMap``

The synchronized collections classes hold a lock for the duration of each operation. Some operations, such as ``HashMap.get`` or ``List.contains``, may involve more work than is initially obvious: traversing a hash bucket or list to find a specific object entails calling ``equals`` (which itself may involve a fair amount of computation) on a number of candidate objects. In a hash-based collection, if ``hashCode`` does not spread out hash values well, elements may be unevenly distributed among buckets; in the degenerate case, a poor hash function will turn a hash table into a linked list.

``ConcurrentHashMap`` is a hash-based ``Map`` like ``HashMap``, but it uses an entirely different locking strategy that offers better concurrency and scalability. Instead of synchronizing every method on a common lock, restricting access to a single thread at a time, it uses a finer-grained locking mechanism called lock striping to allow a greater degree of shared access. Arbitrarily many reading threads can access the map concurrently, readers can access the map concurrently with writers, and a limited number of writers can modify the map concurrently. 

``ConcurrentHashMap``, along with the other concurrent collections, further improve on the synchronized collection classes by providing iterators that do not throw ``ConcurrentModificationException``, thus eliminating the need to lock the collection during iteration. The iterators returned by ``ConcurrentHashMap`` are weakly consistent instead of fail-fast. A weakly consistent iterator can tolerate concurrent modification, traverses elements as they existed when the iterator was constructed, and may (but is not guaranteed to) reflect modifications to the collection after the construction of the iterator.

As with all improvements, there are still a few tradeoffs. The semantics of methods that operate on the entire ``Map``, such as size and ``isEmpty``, have been slightly weakened to reflect the concurrent nature of the collection. Since the result of size could be out of date by the time it is computed, it is really only an estimate, so size is allowed to return an approximation instead of an exact count. the most important operations, primarily
``get``, ``put``, ``containsKey``, and ``remove``.

The one feature offered by the synchronized Map implementations but not by ``ConcurrentHashMap`` is the ability to lock the map for exclusive access.

Only if your application needs to lock the map for exclusive access is ``Concurrent- HashMap`` not an appropriate drop-in replacement.

#### 5.2.2 Additional atomic Map operations

Since a ``ConcurrentHashMap`` cannot be locked for exclusive access, we cannot use client-side locking to create new atomic operations such as put-if-absent Instead, a number of common compound operations such as put-if-absent, remove-if-equal, and replace-if-equal are implemented as atomic operations and specified by the ``ConcurrentMap`` interface

#### 5.2.3 ``CopyOnWriteArrayList``

``CopyOnWriteArrayList`` is a concurrent replacement for a synchronized List that offers better concurrency in some common situations and eliminates the need to lock or copy the collection during iteration. 

```java
public interface ConcurrentMap<K,V> extends Map<K,V> {
	// Insert into map only if no value is mapped from K
	V putIfAbsent(K key, V value);
	// Remove only if K is mapped to V
	boolean remove(K key, V value);
	// Replace value only if K is mapped to oldValue
	boolean replace(K key, V oldValue, V newValue);
	// Replace value only if K is mapped to some value
	V replace(K key, V newValue);
}
```

The copy-on-write collections derive their thread safety from the fact that as long as an effectively immutable object is properly published, no further synchronization is required when accessing it. They implement mutability by creating and republishing a new copy of the collection every time it is modified. Iterators for the copy-on-write collections retain a reference to the backing array that was current at the start of iteration, and since this will never change, they need to synchronize only briefly to ensure visibility of the array contents. As a result,
multiple threads can iterate the collection without interference from one another or from threads wanting to modify the collection. The iterators returned by the copy-on-write collections do not throw ``ConcurrentModificationException`` and return the elements exactly as they were at the time the iterator was created, regardless of subsequent modifications.

Obviously, there is some cost to copying the backing array every time the collection is modified, especially if the collection is large; the copy-on-write collections are reasonable to use only when iteration is far more common than modification. This criterion exactly describes many event-notification systems: delivering a notification requires iterating the list of registered listeners and calling each one of them, and in most cases registering or unregistering an event listener is far less common than receiving an event notification.

### 5.3 Blocking queues and the producer-consumer pattern

Blocking queues provide blocking put and take methods as well as the timed equivalents offer and poll. If the queue is full, put blocks until space becomes available; if the queue is empty, take blocks until an element is available. Queues can be bounded or unbounded; unbounded queues are never full, so a put on an unbounded queue never blocks.

Blocking queues support the producer-consumer design pattern. A producer-consumer design separates the identification of work to be done from the execution of that work by placing work items on a “to do” list for later processing, rather than processing them immediately as they are identified. The producer-consumer pattern simplifies development because it removes code dependencies between producer and consumer classes, and simplifies workload management by decoupling activities that may produce or consume data at different or variable rates.

Producers don’t need to know anything about the identity or number of consumers, or even whether they are the only producer—all they have to do is place data items on the queue. Similarly, consumers need not know who the producers are or where the work came from. ``BlockingQueue`` simplifies the implementation of producer-consumer designs with any number of producers and consumers. One of the most common producer-consumer designs is a thread pool coupled with a work queue; this pattern is embodied in the Executor task execution framework

The labels “producer” and “consumer” are relative; an activity that acts as a consumer in one context may act as a producer in another.

Blocking queues simplify the coding of consumers, since take blocks until data is available. If the producers don’t generate work fast enough to keep the consumers busy, the consumers just wait until more work is available. Sometimes this is perfectly acceptable

If the producers consistently generate work faster than the consumers can process it, eventually the application will run out of memory because work items will queue up without bound. Again, the blocking nature of put greatly simplifies coding of producers; if we use a bounded queue, then when the queue fills up the producers block, giving the consumers time to catch up because a blocked producer cannot generate more work.

Blocking queues also provide an offer method, which returns a failure status if the item cannot be enqueued. This enables you to create more flexible policies for dealing with overload, such as shedding load, serializing excess work items and writing them to disk, reducing the number of producer threads, or throttling producers in some other manner.

> Bounded queues are a powerful resource management tool for building reliable applications: they make your program more robust to overload by throttling activities that threaten to produce more work than can be handled.

While the producer-consumer pattern enables producer and consumer code to be decoupled from each other, their behavior is still coupled indirectly through the shared work queue. It is tempting to assume that the consumers will always keep up, so that you need not place any bounds on the size of work queues, but this is a prescription for rearchitecting your system later. Build resource management into your design early using blocking queues—it is a lot easier to do this up front than to retrofit it later. Blocking queues make this easy for a number of situations, but if blocking queues don’t fit easily into your design, you can create other blocking data structures using ``Semaphore``

Just like other sorted collections, ``PriorityBlockingQueue`` can compare elements according to their natural order

The last ``BlockingQueue`` implementation, ``SynchronousQueue``, is not really a queue at all, in that it maintains no storage space for queued elements. Instead, it maintains a list of queued threads waiting to enqueue or dequeue an element. In the dish-washing analogy, this would be like having no dish rack, but instead it maintains a list of queued threads waiting to enqueue or dequeue an element.

Since a ``SynchronousQueue`` has no storage capacity, put and take will block unless another thread is already waiting to participate in the handoff. Synchronous queues are generally suitable only when there are enough consumers that there nearly always will be one ready to take the handoff.

#### 5.3.1 Example: desktop search

One type of program that is amenable to decomposition into producers and consumers is an agent that scans local drives for documents and indexes them for later searching, similar to Google Desktop or the Windows Indexing service.

The producer-consumer pattern offers a thread-friendly means of decomposing the desktop search problem into simpler components.

The producer-consumer pattern also enables several performance benefits. Producers and consumers can execute concurrently; if one is I/O-bound and the other is CPU-bound, executing them concurrently yields better overall throughput than executing them sequentially. If the producer and consumer activities are parallelizable to different degrees, tightly coupling them reduces parallelizability to that of the less parallelizable activity.

#### 5.3.2 Serial thread confinement

The blocking queue implementations in ``java.util.concurrent`` all contain sufficient internal synchronization to safely publish objects from a producer thread to the consumer thread. 

For mutable objects, producer-consumer designs and blocking queues facilitate serial thread confinement for handing off ownership of objects from producers to consumers. A thread-confined object is owned exclusively by a single thread, but that ownership can be “transferred” by publishing it safely where only one other thread will gain access to it and ensuring that the publishing thread does not access it after the handoff. The safe publication ensures that the object’s state is visible to the new owner, and since the original owner will not touch it again, it is now confined to the new thread. The new owner may modify it freely since it has exclusive access.

Object pools exploit serial thread confinement, “lending” an object to a requesting thread. As long as the pool contains sufficient internal synchronization to publish the pooled object safely, and as long as the clients do not themselves publish the pooled object or use it after returning it to the pool, ownership can be transferred safely from thread to thread.

```java
public class FileCrawler implements Runnable {
    private final BlockingQueue<File> fileQueue;
    private final FileFilter fileFilter;
    private final File root;
    // ...

    public FileCrawler(BlockingQueue<File> fileQueue, FileFilter fileFilter, File root) {
        this.fileQueue = fileQueue;
        this.fileFilter = fileFilter;
        this.root = root;
    }

    public void run() {
        try {
            crawl(root);
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }

    private void crawl(File root) throws InterruptedException {
        File[] entries = root.listFiles(fileFilter);
        if (entries != null) {
            for (File entry : entries) {
                if (entry.isDirectory()) {
                    crawl(entry);
                } else if (!alreadyIndexed(entry)) {
                    fileQueue.put(entry);
                }
            }
        }
    }

    private boolean alreadyIndexed(File file) {
        // Implementation for checking if the file is already indexed
        return false;
    }
}

public class Indexer implements Runnable {
    private final BlockingQueue<File> queue;

    public Indexer(BlockingQueue<File> queue) {
        this.queue = queue;
    }

    public void run() {
        try {
            while (true) {
                indexFile(queue.take());
            }
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }

    private void indexFile(File file) {
        // Implementation for indexing the file
    }
}
```

```java
public static void startIndexing(File[] roots) {
    BlockingQueue<File> queue = new LinkedBlockingQueue<File>(BOUND);
    FileFilter filter = new FileFilter() {
        public boolean accept(File file) { 
            return true; 
        }
    };
    for (File root : roots) {
        new Thread(new FileCrawler(queue, filter, root)).start();
    }
    for (int i = 0; i < N_CONSUMERS; i++) {
        new Thread(new Indexer(queue)).start();
    }
}
```

#### 5.3.3 Deques and work stealing

A ``Deque`` is a double-ended queue that allows efficient insertion and removal from both the head and the tail. Implementations include ``ArrayDeque`` and ``LinkedBlockingDeque``. 

Just as blocking queues lend themselves to the producer-consumer pattern, deques lend themselves to a related pattern called work stealing. A producer-consumer design has one shared work queue for all consumers; in a work stealing design, every consumer has its own deque. If a consumer exhausts the work in its own deque, it can steal work from the tail of someone else’s deque. Work stealing can be more scalable than a traditional producer-consumer design because workers don’t contend for a shared work queue; most of the time they access only their own deque, reducing contention. When a worker has to access another’s queue, it does so from the tail rather than the head, further reducing contention.

Work stealing is well suited to problems in which consumers are also producers— when performing a unit of work is likely to result in the identification of more work. For example, processing a page in a web crawler usually results in the identification of new pages to be crawled. Similarly, many graph-exploring algorithms, such as marking the heap during garbage collection, can be efficiently parallelized using work stealing. When a worker identifies a new unit of work, it places it at the end of its own deque when its deque is empty, it looks for work at the end of someone else’s deque, ensuring that each worker stays busy.

### 5.4 Blocking and interruptible methods

Threads may block, or pause, for several reasons: waiting for I/O completion, waiting to acquire a lock, waiting to wake up from ``Thread.sleep``, or waiting for the result of a computation in another thread. When a thread blocks, it is usually suspended and placed in one of the blocked thread states (BLOCKED, WAITING, or TIMED_WAITING). The distinction between a blocking operation and an ordinary operation that merely takes a long time to finish is that a blocked thread must wait for an event that is beyond its control before it can proceed—the I/O completes, the lock becomes available, or the external computation finishes. When that external event occurs, the thread is placed back in the RUNNABLE state and becomes eligible again for scheduling

The put and take methods of ``BlockingQueue`` throw the checked ``InterruptedException``, as do a number of other library methods such as ``Thread.sleep``. When a method can throw ``InterruptedException``, it is telling you that it is a blocking method, and further that if it is interrupted, it will make an effort to stop blocking early.

Thread provides the interrupt method for interrupting a thread and for querying whether a thread has been interrupted. Each thread has a boolean property that represents its interrupted status; interrupting a thread sets this status. Interruption is a cooperative mechanism. One thread cannot force another to stop what it is doing and do something else; when thread A interrupts thread B, A is merely requesting that B stop what it is doing when it gets to a convenient stopping point—if it feels like it. While there is nothing in the API or language specification that demands any specific application-level semantics for interruption, the most sensible use for interruption is to cancel an activity.

When your code calls a method that throws ``InterruptedException``, then your method is a blocking method too, and must have a plan for responding to interruption. For library code, there are basically two choices:

==**Propagate the ``InterruptedException``**. This is often the most sensible policy if you can get away with it—just propagate the ``InterruptedException`` to your caller. This could involve not catching ``InterruptedException``, or catching it and throwing it again after performing some brief activity-specific cleanup.==

==**Restore the interrupt**. Sometimes you cannot throw ``InterruptedException``, for instance when your code is part of a Runnable. In these situations, you must catch ``InterruptedException`` and restore the interrupted status by calling interrupt on the current thread, so that code higher up the call stack can see that an interrupt was issued==

```java
public class TaskRunnable implements Runnable {
    private final BlockingQueue<Task> queue;

    public TaskRunnable(BlockingQueue<Task> queue) {
        this.queue = queue;
    }

    public void run() {
        try {
            processTask(queue.take());
        } catch (InterruptedException e) {
            // restore interrupted status
            Thread.currentThread().interrupt();
        }
    }

    private void processTask(Task task) {
        // Implementation for processing the task
    }
}
```

### 5.5 Synchronizers

Blocking queues are unique among the collections classes: not only do they act as containers for objects, but they can also coordinate the control flow of producer and consumer threads because take and put block until the queue enters the desired state

 A synchronizer is any object that coordinates the control flow of threads based on its state. Blocking queues can act as synchronizers; other types of synchronizers include semaphores, barriers, and latches. There are a number of synchronizer classes in the platform library;

All synchronizers share certain structural properties: they encapsulate state that determines whether threads arriving at the synchronizer should be allowed to pass or forced to wait, provide methods to manipulate that state, and provide methods to wait efficiently for the synchronizer to enter the desired state.
#### 5.5.1 Latches

A latch is a synchronizer that can delay the progress of threads until it reaches its terminal state. A latch acts as a gate: until the latch reaches the terminal state the gate is closed and no thread can pass, and in the terminal state the gate opens, allowing all threads to pass. Once the latch reaches the terminal state, it cannot change state again, so it remains open forever. Latches can be used to ensure that certain activities do not proceed until other one-time activities complete, such as:

**==• Ensuring that a computation does not proceed until resources it needs have been initialized. A simple binary (two-state) latch could be used to indicate “Resource R has been initialized”, and any activity that requires R would wait first on this latch.**==

==**• Ensuring that a service does not start until other services on which it depends have started. Each service would have an associated binary latch; starting service S would involve first waiting on the latches for other services on which S depends, and then releasing the S latch after startup completes so any services that depend on S can then proceed.**==

==**• Waiting until all the parties involved in an activity, for instance the players in a multi-player game, are ready to proceed. In this case, the latch reaches the terminal state after all the players are ready.==**

``CountDownLatch`` is a flexible latch implementation that can be used in any of these situations; it allows one or more threads to wait for a set of events to occur. The latch state consists of a counter initialized to a positive number, representing the number of events to wait for. The ``countDown`` method decrements the counter, indicating that an event has occurred, and the await methods wait for the counter to reach zero, which happens when all the events have occurred. If the counter is nonzero on entry, await blocks until the counter reaches zero, the waiting thread is interrupted, or the wait times out.
#### 5.5.2 ``FutureTask``

``FutureTask`` also acts like a latch. A computation represented by a ``FutureTask`` is implemented with a Callable, the result-bearing equivalent of Runnable, and can be in one of three states: waiting to run, running, or completed. Completion subsumes all the ways a computation can complete, including normal completion, cancellation, and exception. Once a ``FutureTask`` enters the completed state, it stays in that state forever.

The behavior of ``Future.get`` depends on the state of the task. If it is completed, get returns the result immediately, and otherwise blocks until the task transitions

```java
public class TestHarness {
    public long timeTasks(int nThreads, final Runnable task) throws InterruptedException {
        final CountDownLatch startGate = new CountDownLatch(1);
        final CountDownLatch endGate = new CountDownLatch(nThreads);

        for (int i = 0; i < nThreads; i++) {
            Thread t = new Thread() {
                public void run() {
                    try {
                        startGate.await();
                        try {
                            task.run();
                        } finally {
                            endGate.countDown();
                        }
                    } catch (InterruptedException ignored) { }
                }
            };
            t.start();
        }

        long start = System.nanoTime();
        startGate.countDown();
        endGate.await();
        long end = System.nanoTime();
        return end - start;
    }
}
```

```java
public class Preloader {
    private final FutureTask<ProductInfo> future = new FutureTask<ProductInfo>(new Callable<ProductInfo>() {
        public ProductInfo call() throws DataLoadException {
            return loadProductInfo();
        }
    });

    private final Thread thread = new Thread(future);

    public void start() {
        thread.start();
    }

    public ProductInfo get() throws DataLoadException, InterruptedException {
        try {
            return future.get();
        } catch (ExecutionException e) {
            Throwable cause = e.getCause();
            if (cause instanceof DataLoadException)
                throw (DataLoadException) cause;
            else
                throw launderThrowable(cause);
        }
    }

    private RuntimeException launderThrowable(Throwable t) {
        if (t instanceof RuntimeException) return (RuntimeException) t;
        if (t instanceof Error) throw (Error) t;
        throw new IllegalStateException("Not unchecked", t);
    }

    private ProductInfo loadProductInfo() throws DataLoadException {
        // Implementation for loading product info
        return new ProductInfo();
    }
}
```

```java
/**
 * If the Throwable is an Error, throw it; if it is a
 * RuntimeException return it, otherwise throw IllegalStateException
 */
public static RuntimeException launderThrowable(Throwable t) {
    if (t instanceof RuntimeException) {
        return (RuntimeException) t;
    } else if (t instanceof Error) {
        throw (Error) t;
    } else {
        throw new IllegalStateException("Not unchecked", t);
    }
}
```

#### 5.5.3 Semaphores

Counting semaphores are used to control the number of activities that can access a certain resource or perform a given action at the same time. Counting semaphores can be used to implement resource pools or to impose a bound on a collection.

A Semaphore manages a set of virtual permits; the initial number of permits is passed to the Semaphore constructor. Activities can acquire permits (as long as some remain) and release permits when they are done with them. If no permit is available, acquire blocks until one is (or until interrupted or the operation times out). The release method returns a permit to the semaphore. A degenerate case of a counting semaphore is a binary semaphore, a Semaphore with an initial count of one. A binary semaphore can be used as a mutex with non-reentrant locking semantics; whoever holds the sole permit holds the mutex.

Semaphores are useful for implementing resource pools such as database connection pools. While it is easy to construct a fixed-sized pool that fails if you request a resource from an empty pool, what you really want is to block if the pool is empty and unblock when it becomes nonempty again. If you initialize a Semaphore to the pool size, acquire a permit before trying to fetch a resource from the pool, and release the permit after putting a resource back in the pool, acquire blocks until the pool becomes nonempty. This technique is used in the bounded buffer class

Similarly, you can use a Semaphore to turn any collection into a blocking bounded collection, as illustrated by ``BoundedHashSet``. The semaphore is initialized to the desired maximum size of the collection. The add operation acquires a permit before adding the item into the underlying collection. If the underlying add operation does not actually add anything, it releases the permit immediately

#### 5.5.4 Barriers

Latches are single-use objects; once a latch enters the terminal state, it cannot be reset. Barriers are similar to latches in that they block a group of threads until some event has occurred. The key difference is that with a barrier, all the threads must come together at a barrier point at the same time in order to proceed. Latches are for waiting for events; barriers are for waiting for other threads. A barrier implements the protocol some families use to rendezvous during a day at the mall: “Everyone meet at McDonald’s at 6:00; once you get there, stay there until everyone shows up, and then we’ll figure out what we’re doing next.” 

``CyclicBarrier`` allows a fixed number of parties to rendezvous repeatedly at a barrier point and is useful in parallel iterative algorithms that break down a problem into a fixed number of independent subproblems. Threads call await when they reach the barrier point, and await blocks until all the threads have reached the barrier point. If all threads meet at the barrier point, the barrier has been successfully passed, in which case all threads are released and the barrier is reset so it can be used again. If a call to await times out or a thread blocked in await is interrupted, then the barrier is considered broken and all outstanding calls to await terminate with ``BrokenBarrierException``. If the barrier is successfully passed, await returns a unique arrival index for each thread, which can be used to “elect” a leader that takes some special action in the next iteration. ``CyclicBarrier`` also lets you pass a barrier action to the constructor; this is a Runnable that is executed

Barriers are often used in simulations, where the work to calculate one step can be done in parallel but all the work associated with a given step must complete before advancing to the next step.

```java
public class BoundedHashSet<T> {
    private final Set<T> set;
    private final Semaphore sem;

    public BoundedHashSet(int bound) {
        this.set = Collections.synchronizedSet(new HashSet<T>());
        sem = new Semaphore(bound);
    }

    public boolean add(T o) throws InterruptedException {
        sem.acquire();
        boolean wasAdded = false;
        try {
            wasAdded = set.add(o);
            return wasAdded;
        } finally {
            if (!wasAdded) {
                sem.release();
            }
        }
    }

    public boolean remove(Object o) {
        boolean wasRemoved = set.remove(o);
        if (wasRemoved) {
            sem.release();
        }
        return wasRemoved;
    }
}
```

Another form of barrier is Exchanger, a two-party barrier in which the parties exchange data at the barrier point Exchangers are useful when the parties perform asymmetric activities, for example when one thread fills a buffer with data and the other thread consumes the data from the buffer; these threads could use an Exchanger to meet and exchange a full buffer for an empty one. When two threads exchange objects via an Exchanger, the exchange constitutes a safe publication of both objects to the other party . The timing of the exchange depends on the responsiveness requirements of the application. The simplest approach is that the filling task exchanges when the buffer is full, and the emptying task exchanges when the buffer is empty; this minimizes the number of exchanges but can delay processing of some data if the arrival rate of new data is unpredictable. Another approach would be that the filler exchanges when the buffer is full, but also when the buffer is partially filled and a certain amount of time has elapsed.
### 5.6 Building an efficient, scalable result cache

