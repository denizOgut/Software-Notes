
# CHAPTER 1 An Introduction to Concurrency

When most people use the word “concurrent,” they’re usually referring to a process that occurs simultaneously with one or more processes. It is also usually implied that all of these processes are making progress at about the same time. Under this definition, an easy way to think about this are people. You are currently reading this sentence while others in the world are simultaneously living their lives. They are existing concurrently to you.

## Moore’s Law, Web Scale, and the Mess We’re In

For problems that are embarrassingly parallel, it is recommended that you write your application so that it can scale horizontally. This means that you can take instances of your program, run it on more CPUs, or machines, and this will cause the runtime of the system to improve. Embarrassingly parallel problems fit this model so well because it’s very easy to structure your program in such a way that you can send chunks of a problem to different instances of your application.

among the most difficult was figuring out how to model code concurrently. The fact that pieces of your solution could be running on disparate machines exacerbated some of the issues commonly faced when modeling a problem concurrently. Successfully solving these issues soon led to a new type of brand for software, web scale.

## Why Is Concurrency Hard?

Concurrent code is notoriously difficult to get right. It usually takes a few iterations to get it working as expected, and even then it’s not uncommon for bugs to exist in code for years before some change in timing (heavier disk utilization, more users logged into the system, etc.) causes a previously undiscovered bug to rear its head.

### Race Conditions

**==A race condition occurs when two or more operations must execute in the correct order, but the program has not been written so that this order is guaranteed to be maintained.==**

Most of the time, this shows up in what’s called a data race, where one concurrent operation attempts to read a variable while at some undetermined time another concurrent operation is attempting to write to the same variable.

```go
1 var data int
2 go func() { // 1
3     data++
4 }()
5 if data == 0 {
6     fmt.Printf("the value is %v.\n", data)
7 }
```

1- In Go, you can use the go keyword to run a function concurrently. Doing so creates what’s called a goroutine.

Here, lines 3 and 5 are both trying to access the variable data, but there is no guarantee what order this might happen in. There are three possible outcomes to running this code:

• Nothing is printed. In this case, line 3 was executed before line 5.
• “the value is 0” is printed. In this case, lines 5 and 6 were executed before line 3.
• “the value is 1” is printed. In this case, line 5 was executed before line 3, but line 3 was executed before line 6.

Most of the time, data races are introduced because the developers are thinking about the problem sequentially. They assume that because a line of code falls before another that it will run first. They assume the goroutine above will be scheduled and execute before the ``data`` variable is read in the ``if`` statement

```go
1 var data int
2 go func() { data++ }()
3 time.Sleep(1*time.Second) // This is bad!
4 if data == 0 {
5     fmt.Printf("the value is %v.\n", data)
6 }
```

Have we solved our data race? No. In fact, it’s still possible for all three outcomes to arise from this program, just increasingly unlikely. The longer we sleep in between invoking our goroutine and checking the value of data, the closer our program gets to achieving correctness—but this probability asymptotically approaches logical correctness; it will never be logically correct.

**==The takeaway here is that you should always target logical correctness. Introducing sleeps into your code can be a handy way to debug concurrent programs, but they are not a solution.==**

Race conditions are one of the most insidious types of concurrency bugs because they may not show up until years after the code has been placed into production. They are usually precipitated by a change in the environment the code is executing in, or an unprecedented occurrence. In these cases, the code seems to be behaving correctly, but in reality, there’s just a very high chance that the operations will be executed in order. Sooner or later, the program will have an unintended consequence.

### Atomicity

When something is considered atomic, or to have the property of atomicity, this means that within the context that it is operating, it is indivisible, or uninterruptible.

The first thing that’s very important is the word “context.” Something may be atomic in one context, but not another. Operations that are atomic within the context of your process may not be atomic in the context of the operating system; operations that are atomic within the context of the operating system may not be atomic within the context of your machine; and operations that are atomic within the context of your machine may not be atomic within the context of your application. **==In other words, the atomicity of an operation can change depending on the currently defined scope. This fact can work both for and against you!==**

These terms mean that  
within the context you’ve defined, something that is atomic will happen in its entirety  
without anything happening in that context simultaneously. That’s still a mouthful, so  
let’s look at an example:

`i++`

This is about as simple an example as anyone can contrive, and yet it easily demonstrates  
the concept of atomicity. It may look atomic, but a brief analysis reveals several  
operations:

- Retrieve the value of i.
- Increment the value of i.
- Store the value of i.

While each of these operations alone is atomic, the combination of the three may not be, depending on your context. **==This reveals an interesting property of atomic operations: combining them does not necessarily produce a larger atomic operation.==** Making the operation atomic is dependent on which context you’d like it to be atomic within. If your context is a program with no concurrent processes, then this code is atomic within that context. If your context is a goroutine that doesn’t expose i to other goroutines, then this code is atomic.

### Memory Access Synchronization

Let’s say we have a data race: two concurrent processes are attempting to access the same area of memory, and the way they are accessing the memory is not atomic

```go
var data int
go func() { data++}()
if data == 0 {
	fmt.Println("the value is 0.")
} else {
	fmt.Printf("the value is %v.\n", data)
}
```

there’s a name for a section of your program that needs exclusive access to a  
shared resource. This is called a critical section. In this example, we have three critical  
sections:

- Our goroutine, which is incrementing the ``data`` variables.
- Our if statement, which checks whether the value of ``data`` is 0.
- Our ``fmt.Printf`` statement, which retrieves the value of ``data`` for output.

The following code is not idiomatic Go but it very simply demonstrates memory access synchronization.
If any of the types, functions, or methods in this example are foreign to you, that’s OK

```go
var memoryAccess sync.Mutex // 1
var value int

go func() {
    memoryAccess.Lock()   // 2
    value++
    memoryAccess.Unlock() // 3
}()

memoryAccess.Lock()       // 4
if value == 0 {
    fmt.Printf("the value is %v.\n", value)
} else {
    fmt.Printf("the value is %v.\n", value)
}
memoryAccess.Unlock()     // 5
```

1. Here we add a variable that will allow our code to synchronize access to the data variable’s memory. We’ll go over the ``sync.Mutex`` type in detail in “The sync Package” on page 47.
2. Here we declare that until we declare otherwise, our goroutine should have exclusive access to this memory.
3. Here we declare that the goroutine is done with this memory.
4. Here we once again declare that the following conditional statements should have exclusive access to the data variable’s memory.
5. Here we declare we’re once again done with this memory.

while we have solved our data race, we haven’t actually solved our race condition! The order of operations in this program is still nondeterministic; we’ve just narrowed the scope of the nondeterminism a bit


On its face this seems pretty simple: if you find you have critical sections, add points to synchronize access to the memory

By synchronizing access to the memory in this manner, you are counting on all other developers to follow the same convention now and into the future.

### Deadlocks, Livelocks, and Starvation

#### Deadlocks

A deadlocked program is one in which all concurrent processes are waiting on one another. In this state, the program will never recover without outside intervention.

```go
type value struct {
	mu    sync.Mutex
	value int
}

var wg sync.WaitGroup

printSum := func(v1, v2 *value) {
	defer wg.Done()

	v1.mu.Lock()           // 1
	defer v1.mu.Unlock()   // 2

	time.Sleep(2 * time.Second) // 3

	v2.mu.Lock()
	defer v2.mu.Unlock()

	fmt.Printf("sum=%v\n", v1.value+v2.value)
}

var a, b value

wg.Add(2)
go printSum(&a, &b)
go printSum(&b, &a)
wg.Wait()
```

Here we attempt to enter the critical section for the incoming value.
Here we use the defer statement to exit the critical section before ``printSum`` returns.
Here we sleep for a period of time to simulate work

```go
fatal error: all goroutines are asleep - deadlock!
```

Why? If you look carefully, you’ll see a timing issue in this code. Following is a graphical representation of what’s going on. The boxes represent functions, the horizontal lines calls to these functions, and the vertical bars lifetimes of the function at the head of the graphic

![[Pasted image 20251215213238.png]]

The Coffman Conditions are as follows:

**Mutual Exclusion**  
A concurrent process holds exclusive rights to a resource at any one time.

**Wait For Condition**  
A concurrent process must simultaneously hold a resource and be waiting for an  additional resource.

**No Preemption**  
A resource held by a concurrent process can only be released by that process, so  it fulfills this condition.

**Circular Wait**  
A concurrent process (P1) must be waiting on a chain of other concurrent processes   (P2), which are in turn waiting on it (P1), so it fulfills this final condition  too.

1. The `printSum` function does require exclusive rights to both `a` and `b`, so it fulfills this condition.
2. Because `printSum` holds either `a` or `b` and is waiting on the other, it fulfills this condition.
3. We haven’t given any way for our goroutines to be preempted.
4. Our first invocation of `printSum` is waiting on our second invocation, and vice versa.

#### Livelock

Livelocks are programs that are actively performing concurrent operations, but these operations do nothing to move the state of the program forward.

```go
cadence := sync.NewCond(&sync.Mutex{})
go func() {
    for range time.Tick(1 * time.Millisecond) {
        cadence.Broadcast()
    }
}()

takeStep := func() {
    cadence.L.Lock()
    cadence.Wait()
    cadence.L.Unlock()
}

tryDir := func(dirName string, dir *int32, out *bytes.Buffer) bool { // 1
    fmt.Fprintf(out, " %v", dirName)
    atomic.AddInt32(dir, 1)      // 2
    takeStep()                   // 3
    if atomic.LoadInt32(dir) == 1 {
        fmt.Fprint(out, ". Success!")
        return true
    }
    takeStep()
    atomic.AddInt32(dir, -1)     // 4
    return false
}
```

``tryDir`` allows a person to attempt to move in a direction and returns whether or  
not they were successful. Each direction is represented as a count of the number  
of people trying to move in that direction, `dir`.

- First, we declare our intention to move in a direction by incrementing that direction by one
- For the example to demonstrate a livelock, each person must move at the same rate of speed, or cadence. `takeStep` simulates a constant cadence between all parties.
- Here the person realizes they cannot go in this direction and gives up. We indicate this by decrementing that direction by one.

```go
walk := func(walking *sync.WaitGroup, name string) {
    var out bytes.Buffer
    defer func() { fmt.Println(out.String()) }()
    defer walking.Done()
    fmt.Fprintf(&out, "%v is trying to scoot:", name)
    for i := 0; i < 5; i++ { // 1
        if tryLeft(&out) || tryRight(&out) { // 2
        }
    }
    fmt.Fprintf(&out, "\n%v tosses her hands up in exasperation!", name)
}

var peopleInHallway sync.WaitGroup // 3
peopleInHallway.Add(2)
go walk(&peopleInHallway, "Alice")
go walk(&peopleInHallway, "Barbara")
peopleInHallway.Wait()
```

This produces the following output:

```
Alice is trying to scoot: left right left right left right left right left right Alice tosses her hands up in exasperation! Barbara is trying to scoot: left right left right left right left right left right Barbara tosses her hands up in exasperation!
```

**==This example demonstrates a very common reason livelocks are written: two or more concurrent processes attempting to prevent a deadlock without coordination==**

livelocks are more difficult to spot than deadlocks simply because it can appear as if the program is doing work. If a livelocked program were running on your machine and you took a look at the CPU utilization to determine if it was doing anything, you might think it was.

#### Starvation

Starvation is any situation where a concurrent process cannot get all the resources it needs to perform work.

```go
var wg sync.WaitGroup
var sharedLock sync.Mutex
const runtime = 1 * time.Second

greedyWorker := func() {
    defer wg.Done()

    var count int
    for begin := time.Now(); time.Since(begin) <= runtime; {
        sharedLock.Lock()
        time.Sleep(3 * time.Nanosecond)
        sharedLock.Unlock()

        count++
    }

    fmt.Printf("Greedy worker was able to execute %v work loops\n", count)
}

politeWorker := func() {
    defer wg.Done()

    var count int
    for begin := time.Now(); time.Since(begin) <= runtime; {
        sharedLock.Lock()
        time.Sleep(1 * time.Nanosecond)
        sharedLock.Unlock()

        sharedLock.Lock()
        time.Sleep(1 * time.Nanosecond)
        sharedLock.Unlock()

        sharedLock.Lock()
        time.Sleep(1 * time.Nanosecond)
        sharedLock.Unlock()

        count++
    }

    fmt.Printf("Polite worker was able to execute %v work loops.\n", count)
}

wg.Add(2)
go greedyWorker()
go politeWorker()
wg.Wait()
```

```
Polite worker was able to execute 289777 work loops.
Greedy worker was able to execute 471287 work loops
```

If we assume both workers have the same-sized critical section, rather than concluding that the greedy worker’s algorithm is more efficient (or that the calls to Lock and Unlock are slow—they aren’t), we instead conclude that the greedy worker has unnecessarily expanded its hold on the shared lock beyond its critical section and is preventing (via starvation) the polite worker’s goroutine from performing work efficiently.

One of the ways you can detect and solve starvation is by logging when work is accomplished, and then determining if your rate of work is as high as you expect it.

### Determining Concurrency Safety

As a developer interfacing with existing code, it’s not always obvious what code is utilizing concurrency, and how to utilize the code safely. Take this function signature:

```go
// CalculatePi calculates digits of Pi between the begin and end
// place.
func CalculatePi(begin, end int64, pi *Pi)
```

Calculating pi with a large precision is something that is best done concurrently, but this example raises a lot of questions:

- How do I do so with this function?
- Am I responsible for instantiating multiple concurrent invocations of this function?
- It looks like all instances of the function are going to be operating directly on the  
  instance of Pi whose address I pass in; am I responsible for synchronizing access to that memory, or does the Pi type handle this for me?

Comments can work wonders here. What if the `CalculatePi` function were instead  
written like this:

```go
// CalculatePi calculates digits of Pi between the begin and end
// place.
//
// Internally, CalculatePi will create FLOOR((end-begin)/2) concurrent
// processes which recursively call CalculatePi. Synchronization of
// writes to pi are handled internally by the Pi struct.
func CalculatePi(begin, end int64, pi *Pi)
```

Importantly, the comment covers these aspects:

- Who is responsible for the concurrency?
- How is the problem space mapped onto concurrency primitives?
- Who is responsible for the synchronization?

When exposing functions, methods, and variables in problem spaces that involve   concurrency, do your colleagues and future self a favor: err on the side of verbose   comments, and try and cover these three aspects.
Also consider that perhaps the ambiguity in this function suggests that we’ve modeled it wrong.

```go
func CalculatePi(begin, end int64) []uint
```

The signature of this function alone removes any questions of synchronization, but  
still leaves the question of whether concurrency is used. We can modify the signature  
again to throw out another signal as to what is happening:

```go
func CalculatePi(begin, end int64) <-chan uint
```


# CHAPTER 2 Modeling Your Code: Communicating Sequential Processes

## The Difference Between Concurrency and Parallelism

>Concurrency is a property of the code; parallelism is a property of the running program.

Well, let’s think about that for second. If I write my code with the intent that two chunks of the program will run in parallel, do I have any guarantee that will actually happen when the program is run? What happens if I run the code on a machine with only one core? Some of you may be thinking, It will run in parallel, but this isn’t true!

The chunks of our program may appear to be running in parallel, but really they’re executing in a sequential manner faster than is distinguishable. The CPU context switches to share time between different programs, and over a coarse enough granularity of time, the tasks appear to be running in parallel. If we were to run the same
binary on a machine with two cores, the program’s chunks might actually be running in parallel.

- The first is that we do not write parallel code, only concurrent code that we hope will be run in parallel. Once again, parallelism is a property of the runtime of our program, not the code.
- The second interesting thing is that we see it is possible—maybe even desirable—to be ignorant of whether our concurrent code is actually running in parallel. This is only made possible by the layers of abstraction that lie beneath our program’s model: the concurrency primitives, the program’s runtime, the operating system, the platform the operating system runs on and ultimately the CPUs
- The third and final interesting thing is that parallelism is a function of time, or context. There, context was defined as the bounds by which an operation was considered atomic. Here, it’s defined as the bounds by which two or more operations could be considered parallel.

The perception of parallelism versus sequential execution depends on the defined context, such as time slices, processes, threads, or machines. Operations appear parallel in larger contexts and sequential in smaller ones.

Concurrency correctness is relative to the chosen context. At the machine level, processes on separate computers are naturally isolated, ensuring independent execution (e.g., separate calculator instances unaffected by each other).

At the same machine level, processes are generally isolated by the OS, though risks like file overwrites or memory corruption exist in insecure systems. Users expect logical isolation between processes.

At the thread level within a single process, concurrency issues become prominent: race conditions, deadlocks, livelocks, and starvation. Shared memory requires careful synchronization, making reasoning harder.

As abstraction levels decrease (from machines to processes to threads), concurrency becomes more difficult to manage correctly and more critical. Higher-level abstractions simplify reasoning, but most industry concurrent code uses low-level OS threads, lacking composable primitives. Stronger, composable concurrency abstractions are essential where problems are hardest.

Go has added another link in that chain: the goroutine. In addition, Go has borrowed several concepts from the work of famed computer scientist Tony Hoare, and introduced new primitives for us to use, namely channels.

If we continue the line of reasoning we have been following, we’d assume that introducing another level of abstraction below OS threads would bring with it more difficulties, but the interesting thing is that it doesn’t. It actually makes things easier. This is because we haven’t really added another layer of abstraction on top of OS threads, we’ve supplanted them.

## What Is CSP?

CSP stands for “Communicating Sequential Processes,” which is both a technique and the name of the paper that introduced

In this paper, Hoare suggests that input and output are two overlooked primitives of programming—particularly in concurrent code. At the time Hoare authored this paper, research was still being done on how to structure programs, but most of this effort was being directed to techniques for sequential code: usage of the goto statement was being debated, and the object-oriented paradigm was beginning to take root. Concurrent operations weren’t being given much thought 

> Thus the concepts and notations introduced in this paper should … not be regarded as suitable for use as a programming language, either for abstract or for concrete programming

For communication between the processes, Hoare created input and output commands: ! for sending input into a process, and ? for reading output from a process. Each command had to specify either an output variable (in the case of reading a variable out of a process), or a destination (in the case of sending input to a process). Sometimes these two would refer to the same thing, in which case the two processes would be said to correspond. **==In other words, output from one process would flow directly into the input of another process.==**

| Operation                         | Explanation                                                                                                                             |
| --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| `cardreader?cardimage`            | From cardreader, read a card and assign its value (an array of characters) to the variable `cardimage`.                                 |
| `lineprinter!lineimage`           | To lineprinter, send the value of `lineimage` for printing.                                                                             |
| `X?(x, y)`                        | From process named X, input a pair of values and assign them to x and y.                                                                |
| `DIV!(3*a+b, 13)`                 | To process DIV, output the two specified values.                                                                                        |
| `*[c:character; west?c → east!c]` | Read all the characters output by west, and output them one by one to east. The repetition terminates when the process west terminates. |

The similarities to Go’s channels are apparent 

The language also utilized a so-called guarded command **==A guarded command is simply a statement with a left- and righthand side, split by a →. The lefthand side served as a conditional, or guard for the righthand side in that if the lefthand side was false or, in the case of a command, returned false or had exited, the righthand side would never be executed.==** Combining these with Hoare’s I/O commands laid the foundation for Hoare’s communicating processes, and thus Go’s channels

## How This Helps You

Comparing goroutines to threads and channels to mutexes provides a rough orientation, though the resemblance is superficial. These abstractions in Go allow modeling problems based on their natural concurrency rather than forcing a focus on parallelism.

Using threads introduces unrelated concerns that distract from the core problem:

- Does the language natively support threads, or require a library?
- Where to place thread confinement boundaries?
- How heavyweight are threads on the target operating system?
- How do different operating systems handle threads?
- Should a worker pool be created to limit threads, and what is the optimal size?

These considerations pull attention into parallelism technicalities rather than the problem itself.

In contrast, Go enables direct representation of the natural problem state. For example, handling individual user connections to an endpoint involves creating a goroutine per connection, processing the request (possibly communicating with other goroutines), and returning the response. This maps closely to how the problem is conceptually understood.

Go supports this by treating goroutines as lightweight, removing the need to worry about creating them in most cases. Limiting goroutines may be necessary in specific scenarios, but considering it upfront is usually premature optimization—unlike with threads, where such concerns are prudent from the start.

Even when frameworks abstract parallelism in other languages, the underlying complexity remains and can lead to bugs. A more natural problem-to-code mapping offers significant benefits.

Additionally, Go's runtime automatically multiplexes goroutines onto OS threads and handles scheduling. This separates concerns effectively: runtime optimizations and advancements in parallelism improve program performance without requiring changes to the problem modeling.

## Go’s Philosophy on Concurrency

CSP was and is a large part of what Go was designed around; however, Go also supports more traditional means of writing concurrent code through memory access synchronization and the primitives that follow that technique. Structs and methods in the ``sync`` and other packages allow you to perform locks, create pools of resources, preempt goroutines, and more.

This ability to choose between CSP primitives and memory access synchronizations is great for you since it gives you a little more control over what style of concurrent code you choose to write to solve problems, but it can also be a little confusing. Newcomers to the language often get the impression that the CSP style of concurrency is considered the one and only way to write concurrent code in Go. For instance, in the documentation for the ``sync`` package, it says:

> Package sync provides basic synchronization primitives such as mutual exclusion locks. Other than the Once and `WaitGroup` types, most are intended for use by low level library routines. Higher-level synchronization is better done via channels and communication.

In the language FAQ, it says:

> Regarding mutexes, the sync package implements them, but we hope Go programming style will encourage people to try higher-level techniques. In particular, consider structuring your program so that only one goroutine at a time is ever responsible for a particular piece of data. 
> **==Do not communicate by sharing memory. Instead, share memory by communicating.**==


---

Avoid making multiple goroutines access and modify the same shared variables in memory (which requires locks/mutexes to prevent race conditions and is error-prone).

Instead, let goroutines own their data privately and exchange it safely by sending/receiving messages over channels. Channels handle synchronization automatically, making concurrent code simpler, less buggy, and easier to reason about.

---

![[Pasted image 20251219224920.png]]

### Are you trying to transfer ownership of data?

If you have a bit of code that produces a result and wants to share that result with another bit of code, what you’re really doing is transferring ownership of that data. If you’re familiar with the concept of memory-ownership in languages that don’t support garbage collection, this is the same idea: data has an owner, and one way to make concurrent programs safe is to ensure only one concurrent context has ownership of data at a time. Channels help us communicate this concept by encoding that intent into the channel’s type.

**==One large benefit of doing so is you can create buffered channels to implement a cheap in-memory queue and thus decouple your producer from your consumer. Another is that by using channels, you’ve implicitly made your concurrent code composable with other concurrent code.==**

### Are you trying to guard internal state of a struct?

This is a great candidate for memory access synchronization primitives, and a pretty strong indicator that you shouldn’t use channels. By using memory access synchronization primitives, you can hide the implementation detail of locking your critical section from your callers. Here’s a small example of a type that is thread-safe, but doesn’t expose that complexity to its callers:

```go
type Counter struct {
    mu    sync.Mutex
    value int
}

func (c *Counter) Increment() {
    c.mu.Lock()
    defer c.mu.Unlock()
    c.value++
}
```

If you recall the concept of atomicity, we can say that what we’ve done here is defined the scope of atomicity for the Counter type. Calls to Increment can be considered atomic.

**==Remember the key word here is internal. If you find yourself exposing locks beyond a type, this should raise a red flag. Try to keep the locks constrained to a small lexical scope.==**

### Are you trying to coordinate multiple pieces of logic?

Remember that channels are inherently more composable than memory access synchronization primitives. Having locks scattered throughout your object-graph sounds like a nightmare, but having channels everywhere is expected and encouraged! I can compose channels, but I can’t easily compose locks or methods that return values.

You will find it much easier to control the emergent complexity that arises in your software if you use channels because of Go’s select statement, and their ability to serve as queues and be safely passed around. If you find yourself struggling to understand how your concurrent code works, why a deadlock or race is occurring, and you’re using primitives, this is probably a good indicator that you should switch to channels.

### Is it a performance-critical section?

This absolutely does not mean, “I want my program to be performant, therefore I will only use mutexes.” Rather, if you have a section of your program that you have profiled, and it turns out to be a major bottleneck that is orders of magnitude slower than the rest of the program, using memory access synchronization primitives may help this critical section perform under load. This is because channels use memory access synchronization to operate, therefore they can only be slower. Before we even consider this, however, a performance-critical section might be hinting that we need to restructure our program.

# CHAPTER 3 Go’s Concurrency Building Blocks

## Goroutines

every Go program has at least one goroutine: the main goroutine, which is automatically created and started when the process begins.

Put very simply, a goroutine is a function that is running concurrently alongside other code. You can start one simply by placing the ``go`` keyword before a function:

```go
func main() {
	go sayHello()
	// continue doing other things
}
func sayHello() {
	fmt.Println("hello")
}
```

```go
go func() {
	fmt.Println("hello")
}() // 1
// continue doing other things
```

1 -  Notice that we must invoke the anonymous function immediately to use the go keyword.
Alternatively, you can assign the function to a variable and call the anonymous function like this:

```go
sayHello := func() {
	fmt.Println("hello")
}
go sayHello()
```

what’s happening behind the scenes here: how do goroutines actually work? Are they OS threads? Green threads? How many can we create?

**==Goroutines are unique to Go They’re not OS threads, and they’re not exactly green threads—threads that are managed by a language’s runtime—they’re a higher level of abstraction known as coroutines. Coroutines are simply concurrent subroutines (functions, closures, or methods in Go) that are nonpreemptive—that is, they cannot be interrupted. Instead, coroutines have multiple points throughout which allow for suspension or reentry==**

What makes goroutines unique to Go are their deep integration with Go’s runtime. Goroutines don’t define their own suspension or reentry points; Go’s runtime observes the runtime behavior of goroutines and automatically suspends them when they block and then resumes them when they become unblocked. In a way this makes them preemptable, but only at points where the goroutine has become blocked. It is an elegant partnership between the runtime and a goroutine’s logic.

Coroutines, and thus goroutines, are implicitly concurrent constructs, but concurrency is not a property of a coroutine: something must host several coroutines simultaneously and give each an opportunity to execute—otherwise, they wouldn’t be concurrent!

**==Go’s mechanism for hosting goroutines is an implementation of what’s called an M:N scheduler, which means it maps M green threads to N OS threads. Goroutines are then scheduled onto the green threads. When we have more goroutines than green threads available, the scheduler handles the distribution of the goroutines across the available threads and ensures that when these goroutines become blocked, other goroutines can be run.==**

Go follows a model of concurrency called the fork-join model.1 The word fork refers to the fact that at any point in the program, it can split off a child branch of execution to be run concurrently with its parent. The word join refers to the fact that at some point in the future, these concurrent branches of execution will join back together. Where the child rejoins the parent is called a join point

![[Pasted image 20251224190826.png]]

The ``go`` statement is how Go performs a fork, and the forked threads of execution are goroutines.

```go
sayHello := func() {
	fmt.Println("hello")
}
go sayHello()
// continue doing other things
```

Here, the ``sayHello`` function will be run on its own goroutine, while the rest of the program continues executing.

However, there is one problem with this example: as written, it’s undetermined whether the ``sayHello`` function will ever be run at all. The goroutine will be created and scheduled with Go’s runtime to execute, but it may not actually get a chance to run before the main goroutine exits.

In order to a create a join point, you have to synchronize the main goroutine and the ``sayHello`` goroutine. This can be done in a number of ways, ``sync.WaitGroup``. Right now it’s not important to understand how this example creates a join point, only that it creates one between the two goroutines.

```go
var wg sync.WaitGroup
sayHello := func() {
	defer wg.Done()
	fmt.Println("hello")
}
wg.Add(1)
go sayHello()
wg.Wait() // 1
```

1 - This is the join point.

This example will deterministically block the main goroutine until the goroutine hosting the ``sayHello`` function terminates 

Closures close around the lexical scope they are created in, thereby capturing variables. If you run a closure in a goroutine, does the closure operate on a copy of these variables, or the original references?

```go
var wg sync.WaitGroup
salutation := "hello"
wg.Add(1)
go func() {
	defer wg.Done()
	salutation = "welcome" // 1
}()
wg.Wait()
fmt.Println(salutation)
```

1- Here we reference the loop variable ``salutation`` created by ranging over a string slice.

```shell
welcome
```

It turns out that goroutines execute within the same address space they were created in, and so our program prints out the word “welcome.”

```go
var wg sync.WaitGroup
for _, salutation := range []string{"hello", "greetings", "good day"} {
	wg.Add(1)
	go func() {
		defer wg.Done()
		fmt.Println(salutation) // 1
		}()
	}
wg.Wait()
```

1 - Here we reference the loop variable ``salutation`` created by ranging over a string slice.

```shell
good day
good day
good day
```

In this example, the goroutine is running a closure that has closed over the iteration variable ``salutation``, which has a type of ``string``. As our loop iterates, ``salutation`` is being assigned to the next string value in the slice literal. Because the goroutines being scheduled may run at any point in time in the future, it is undetermined what values will be printed from within the goroutine. This means the ``salutation`` variable falls out of scope. What happens then? Can the goroutines still reference something that has fallen out of scope? Won’t the goroutines be accessing memory that has potentially been garbage collected?

The Go runtime is observant enough to know that a reference to the ``salutation`` variable is still being held, and therefore will transfer the memory to the heap so that the goroutines can continue to access it.

The proper way to write this loop is to pass a copy of salutation into the closure so that by the time the goroutine is run, it will be operating on the data from its iteration of the loop:

```go
var wg sync.WaitGroup
for _, salutation := range []string{"hello", "greetings", "good day"} {
	wg.Add(1)
	go func() {
		defer wg.Done()
		fmt.Println(salutation) // 1
		}()
	}
wg.Wait(salutation) // 2
```

1 -  Here we declare a parameter, just like any other function. We shadow the original ``salutation`` variable to make what’s happening more apparent.

2 - Here we pass in the current iteration’s variable to the closure. A copy of the string struct is made, thereby ensuring that when the goroutine is run, we refer to the proper string

```go
good day
hello
greetings
```

This example behaves as we would expect it to, and is only slightly more verbose.

Because goroutines operate within the same address space as each other, and simply host functions, utilizing goroutines is a natural extension to writing nonconcurrent code. Go’s compiler nicely takes care of pinning variables in memory so that goroutines don’t accidentally access freed memory, which allows developers to focus on their problem space instead of memory management; however, it’s not a blank check. Since multiple goroutines can operate against the same address space, we still have to worry about synchronization.

## The ``sync`` Package

The ``sync`` package contains the concurrency primitives that are most useful for low level memory access synchronization

### ``WaitGroup``

``WaitGroup`` is a great way to wait for a set of concurrent operations to complete when you either don’t care about the result of the concurrent operation, or you have other means of collecting their results. If neither of those conditions are true, **==I suggest you use channels and a select statement instead.==**

```go
var wg sync.WaitGroup
wg.Add(1) // 1

go func() {
	defer wg.Done() // 2
	fmt.Println("1st goroutine sleeping...")
	time.Sleep(1)
}()

wg.Add(1) // 1

go func() {
	defer wg.Done() // 2
	fmt.Println("2nd goroutine sleeping...")
	time.Sleep(2)
}(wg.Wait()) // 3

fmt.Println("All goroutines complete.")

```

1- Here we call Add with an argument of 1 to indicate that one goroutine is beginning.
2- Here we call Done using the defer keyword to ensure that before we exit the goroutine’s closure, we indicate to the ``WaitGroup`` that we’ve exited.
3- Here we call Wait, which will block the main goroutine until all goroutines have indicated they have exited

### ``Mutex`` and ``RWMutex``

```go
var count int
var lock sync.Mutex

increment := func() {
	lock.Lock() // 1
	defer lock.Unlock() // 2
	count++
	fmt.Printf("Incrementing: %d\n", count)
}

decrement := func() {
	lock.Lock() // 1
	defer lock.Unlock() // 2
	count--
	fmt.Printf("Decrementing: %d\n", count)
}

// Increment
var arithmetic sync.WaitGroup
for i := 0; i <= 5; i++ {
	arithmetic.Add(1)
	go func() {
		defer arithmetic.Done()
		increment()
	}()
}

// Decrement
for i := 0; i <= 5; i++ {
	arithmetic.Add(1)
	go func() {
		defer arithmetic.Done()
		decrement()
	}()
}

arithmetic.Wait()
fmt.Println("Arithmetic complete.")

```

Here we request exclusive use of the critical section—in this case the ``count`` variable— guarded by a ``Mutex``, lock.
Here we indicate that we’re done with the critical section lock is guarding.

notice that we always call ``Unlock`` within a ``defer`` statement. This is a very common idiom when utilizing a ``Mutex`` to ensure the call always happens, even when panicking. Failing to do so will probably cause your program to deadlock.

Critical sections are so named because they reflect a bottleneck in your program. It is somewhat expensive to enter and exit a critical section, and so generally people attempt to minimize the time spent in critical sections.

One strategy for doing so is to reduce the cross-section of the critical section. There may be memory that needs to be shared between multiple concurrent processes, but perhaps not all of these processes will read and write to this memory. If this is the case, you can take advantage of a different type of mutex: ``sync.RWMutex``.

The ``sync.RWMutex`` is conceptually the same thing as a Mutex: it guards access to memory; however, ``RWMutex`` gives you a little bit more control over the memory. You can request a lock for reading, in which case you will be granted access unless the lock is being held for writing. This means that an arbitrary number of readers can hold a reader lock so long as nothing else is holding a writer lock

```go
producer := func(wg *sync.WaitGroup, l sync.Locker) { // 1
	defer wg.Done()
	for i := 5; i > 0; i-- {
		l.Lock()
		l.Unlock()
		time.Sleep(1) // 2
	}
}

observer := func(wg *sync.WaitGroup, l sync.Locker) {
	defer wg.Done()
	l.Lock()
	defer l.Unlock()
}

test := func(count int, mutex, rwMutex sync.Locker) time.Duration {
	var wg sync.WaitGroup
	wg.Add(count + 1)

	beginTestTime := time.Now()
	go producer(&wg, mutex)

	for i := count; i > 0; i-- {
		go observer(&wg, rwMutex)
	}

	wg.Wait()
	return time.Since(beginTestTime)
}

tw := tabwriter.NewWriter(os.Stdout, 0, 1, 2, ' ', 0)
defer tw.Flush()

var m sync.RWMutex
fmt.Fprintf(tw, "Readers\tRWMutext\tMutex\n")

for i := 0; i < 20; i++ {
	count := int(math.Pow(2, float64(i)))
	fmt.Fprintf(
		tw,
		"%d\t%v\t%v\n",
		count,
		test(count, &m, m.RLocker()),
		test(count, &m, &m),
	)
}

```

1- The producer function’s second parameter is of the type ``sync.Locker``. This interface has two methods, Lock and Unlock, which the Mutex and ``RWMutex`` types satisfy.
2- Here we make the producer sleep for one second to make it less active than the observer goroutines.

### ``Cond``

The comment for the ``Cond`` type really does a great job of describing its purpose:
> ``...``a rendezvous point for goroutines waiting for or announcing the occurrence of an event.

In that definition, an “event” is any arbitrary signal between two or more goroutines that carries no information other than the fact that it has occurred Very often you’ll want to wait for one of these signals before continuing execution on a goroutine

```go
for conditionTrue() == false {
}
```

```go
for conditionTrue() == false {
	time.Sleep(1*time.Millisecond)
}
```

This is better, but it’s still inefficient, and you have to figure out how long to sleep for: too long, and you’re artificially degrading performance; too short, and you’re unnecessarily consuming too much CPU time. It would be better if there were some kind of way for a goroutine to efficiently sleep until it was signaled to wake and check its condition. This is exactly what the ``Cond`` type does for us. Using a ``Cond``, we could write the previous examples like this:

```go
c := sync.NewCond(&sync.Mutex{}) // 1
c.L.Lock() // 2
for conditionTrue() == false {
	c.Wait() // 3
}
c.L.Unlock() // 4
```

1- The ``NewCond`` function takes in a type that satisfies the ``sync.Locker`` interface. This is what allows the ``Cond`` type to facilitate coordination with other goroutines in a concurrent-safe way.

2- Here we lock the ``Locker`` for this condition. This is necessary because the call to ``Wait`` automatically calls Unlock on the ``Locker`` when entered.

3- Here we wait to be notified that the condition has occurred. This is a blocking call and the goroutine will be suspended.

4-  Here we unlock the ``Locker`` for this condition. This is necessary because when the call to Wait exits, it calls Lock on the Locker for the condition.

Note that the call to `Wait` doesn’t just block, it suspends the current goroutine, allowing other goroutines to run on the OS thread. A few other things happen when you call `Wait`: upon entering `Wait`, `Unlock` is called on the `Cond` variable’s `Locker`, and upon exiting `Wait`, `Lock` is called on the `Cond` variable’s `Locker`. In my opinion, this takes a little getting used to; it’s effectively a hidden side effect of the method. It looks like we’re holding this lock the entire time while we wait for the condition to occur, but that’s not actually the case. When you’re scanning code, you’ll just have to keep an eye out for this pattern.

ay we have a queue of fixed length 2, and 10 items we want to push onto the queue. We want to enqueue items as soon as there is room, so we want to be notified as soon as there’s room in the queue. Let’s try using a ``Cond`` to manage this coordination:

```go
c := sync.NewCond(&sync.Mutex{}) // 1
queue := make([]interface{}, 0, 10) // 2

removeFromQueue := func(delay time.Duration) {
	time.Sleep(delay)
	c.L.Lock() // 8
	queue = queue[1:] // 9
	fmt.Println("Removed from queue")
	c.L.Unlock() // 10 
	c.Signal() // 11
}

for i := 0; i < 10; i++ {
	c.L.Lock() // 3
	for len(queue) == 2 { // 4
		c.Wait() // 5
	}
	fmt.Println("Adding to queue")
	queue = append(queue, struct{}{})
	go removeFromQueue(1 * time.Second) // 6
	c.L.Unlock() // 7
}

```

1. First, we create our condition using a standard `sync.Mutex` as the `Locker`.
    
2. Next, we create a slice with a length of zero. Since we know we’ll eventually add 10 items, we instantiate it with a capacity of 10.
    
3. We enter the critical section for the condition by calling `Lock` on the condition’s `Locker`.
    
4. Here we check the length of the queue in a loop. **==This is important because a signal on the condition doesn’t necessarily mean what you’ve been waiting for has occurred—only that something has occurred.==**
    
5. We call `Wait`, which will suspend the main goroutine until a signal on the condition has been sent.
    
6. Here we create a new goroutine that will dequeue an element after one second.
    
7. Here we exit the condition’s critical section since we’ve successfully enqueued an item.
    
8. We once again enter the critical section for the condition so we can modify data pertinent to the condition.
    
9. Here we simulate dequeuing an item by reassigning the head of the slice to the second item.
    
10. Here we exit the condition’s critical section since we’ve successfully dequeued an item.
    
11. Here we let a goroutine waiting on the condition know that something has occurred.

``Signal`` is one of two methods that the `Cond` type provides for notifying goroutines blocked on a `Wait` call that the condition has been triggered. The other method is called `Broadcast`. Internally, the runtime maintains a FIFO list of goroutines waiting to be signaled; `Signal` finds the goroutine that’s been waiting the longest and notifies it, whereas `Broadcast` sends a signal to all goroutines that are waiting. `Broadcast` is arguably the more interesting of the two methods, as it provides a way to communicate with multiple goroutines at once. but reproducing the behavior of repeated calls to ``Broadcast`` would be more difficult. In addition, the ``Cond`` type is much more performant than utilizing channels.

```go
type Button struct { // 1
	Clicked *sync.Cond
}

button := Button{
	Clicked: sync.NewCond(&sync.Mutex{}),
}

subscribe := func(c *sync.Cond, fn func()) { // 2
	var goroutineRunning sync.WaitGroup
	goroutineRunning.Add(1)

	go func() {
		goroutineRunning.Done()
		c.L.Lock()
		defer c.L.Unlock()
		c.Wait()
		fn()
	}()

	goroutineRunning.Wait()
}

var clickRegistered sync.WaitGroup // 3
clickRegistered.Add(3)

subscribe(button.Clicked, func() { // 4
	fmt.Println("Maximizing window.")
	clickRegistered.Done()
})

subscribe(button.Clicked, func() { // 5
	fmt.Println("Displaying annoying dialog box!")
	clickRegistered.Done()
})

subscribe(button.Clicked, func() { // 6
	fmt.Println("Mouse clicked.")
	clickRegistered.Done()
})

button.Clicked.Broadcast() // 7
clickRegistered.Wait()

```

1. We define a type `Button` that contains a condition, `Clicked`.
    
2. Here we define a convenience function that allows us to register functions to handle signals from a condition. Each handler is run on its own goroutine, and `subscribe` will not exit until that goroutine is confirmed to be running.
    
3. Here we set a handler for when the mouse button is raised. It in turn calls `Broadcast` on the `Clicked` `Cond` to let all handlers know that the mouse button has been clicked (a more robust implementation would first check that it had been depressed).
    
4. Here we create a `WaitGroup`. This is done only to ensure our program doesn’t exit before our writes to ``stdout`` occur.
    
5. Here we register a handler that simulates maximizing the button’s window when the button is clicked.
    
6. Here we register a handler that simulates displaying a dialog box when the mouse is clicked.
    
7. Next, we simulate a user raising the mouse button from having clicked the application’s button.

### ``Once``

What do you think this code will print out?

```go
var count int

increment := func() {
	count++
}

var once sync.Once
var increments sync.WaitGroup

increments.Add(100)

for i := 0; i < 100; i++ {
	go func() {
		defer increments.Done()
		once.Do(increment)
	}()
}

increments.Wait()
fmt.Printf("Count is %d\n", count)
```


Notice the `sync.Once` variable, and that we’re wrapping the call to `increment` inside the `Do` method of `once`. This code will print `Count is 1`. As the name implies, `sync.Once` is a type that uses synchronization primitives internally to ensure that only one call to `Do` ever invokes the function passed in—even when called from different goroutines. This behavior occurs because the call to `increment` is wrapped inside the `sync.Once.Do` method.


```go
var count int
increment := func() { count++ }

var once sync.Once
var increments sync.WaitGroup

increments.Add(100)
for i := 0; i < 100; i++ {
	go func() {
		defer increments.Done()
		once.Do(increment)
	}()
}

increments.Wait()
fmt.Printf("Count is %d\n", count)
```

There are a few important things to note when using `sync.Once`. Consider the following example.


```go
var count int
increment := func() { count++ }
decrement := func() { count-- }

var once sync.Once
once.Do(increment)
once.Do(decrement)

fmt.Printf("Count: %d\n", count)
```


This produces `Count: 1`. It may seem surprising that the output is not `0`, but this happens because `sync.Once` only tracks how many times `Do` is called, not how many distinct functions are passed to it. Once the first call to `Do` succeeds, all subsequent calls are ignored. Because of this, instances of `sync.Once` are tightly coupled to the function they are meant to protect. For best results, this coupling should be made explicit by keeping both the `sync.Once` value and the function it guards within a small lexical scope, such as inside a function or wrapped together in a dedicated type.

### ``Pool``

``Pool`` is a concurrent-safe implementation of the object pool pattern. A complete explanation of the object pool pattern is best left to literature on design patterns; however, since ``Pool`` resides in the ``sync`` package

At a high level, a the pool pattern is a way to create and make available a fixed number, or pool, of things for use. It’s commonly used to constrain the creation of things that are expensive (e.g., database connections) so that only a fixed number of them are ever created, but an indeterminate number of operations can still request access to these things. In the case of Go’s ``sync.Pool``, this data type can be safely used by multiple goroutines.

Pool’s primary interface is its ``Get`` method. When called, ``Get`` will first check whether there are any available instances within the pool to return to the caller, and if not, call its New member variable to create a new one. When finished, callers call Put to place

```go
myPool := &sync.Pool{
	New: func() interface{} {
		fmt.Println("Creating new instance.")
		return struct{}{}
	},
}

myPool.Get() // 1
instance := myPool.Get() // 1
myPool.Put(instance) // 2
myPool.Get() // 3

```

1. Here we call `Get` on the pool. These calls will invoke the `New` function defined on the pool since instances haven’t yet been instantiated.
    
2. Here we put an instance previously retrieved back in the pool. This increases the available number of instances to one.
    
3. When this call is executed, we will reuse the instance previously allocated and put back in the pool, so the `New` function will not be invoked.

So why use a pool and not just instantiate objects as you go? Go has a garbage collector, so the instantiated objects will be automatically cleaned up. What’s the point?

```go
var numCalcsCreated int

calcPool := &sync.Pool{
	New: func() interface{} {
		numCalcsCreated += 1
		mem := make([]byte, 1024)
		return &mem // 1
	},
}

// Seed the pool with 4KB
calcPool.Put(calcPool.New())
calcPool.Put(calcPool.New())
calcPool.Put(calcPool.New())
calcPool.Put(calcPool.New())

const numWorkers = 1024 * 1024
var wg sync.WaitGroup
wg.Add(numWorkers)

for i := numWorkers; i > 0; i-- {
	go func() {
		defer wg.Done()
		mem := calcPool.Get().(*[]byte) // 2
		defer calcPool.Put(mem)
		// Assume something interesting, but quick is being done with
		// this memory.
	}()
}

wg.Wait()
fmt.Printf("%d calculators were created.", numCalcsCreated)

```

1- Notice that we are storing the address of the slice of bytes.
2- And here we are asserting the type is a pointer to a slice of bytes.

Had this example been run without a `sync.Pool`, the results would be nondeterministic, and in the worst case it could have attempted to allocate up to a gigabyte of memory. However, as shown by the output, only 4 KB was actually allocated. Another common situation where a pool is useful is warming a cache of preallocated objects for operations that must run as quickly as possible. In this scenario, rather than protecting the host machine’s memory by limiting the number of objects created, we are protecting consumers’ time by front-loading the cost of obtaining a reference to an object. This pattern is very common in high-throughput network servers that aim to respond to requests as quickly as possible.

So when working with a `Pool`, remember the following points:

- ==**When instantiating `sync.Pool`, provide a `New` function that is thread-safe when called.**==
    
- ==**When you receive an instance from `Get`, make no assumptions about the state of the object you receive.**==
    
- ==**Always call `Put` when you are finished with an object taken from the pool; otherwise, the pool becomes ineffective. This is usually done with `defer`.**==
    
- ==**Objects stored in the pool should be roughly uniform in structure and purpose.==**

## Channels

Channels are one of the synchronization primitives in Go derived from Hoare’s CSP. While they can be used to synchronize access of the memory, they are best used to communicate information between goroutines

**==Like a river, a channel serves as a conduit for a stream of information; values may be passed along the channel, and then read out downstream==**. For this reason I usually end my chan variable names with the word “Stream.” When using channels, you’ll pass a value into a chan variable, and then somewhere else in your program read it off the channel. The disparate parts of your program don’t require knowledge of each other, only a reference to the same place in memory where the channel resides. This can be done by passing references of channels around your program.

As with other values in Go, you can create channels in one step with the ``:=`` operator, but you will need to declare channels often, so it’s useful to see the two split into individual steps:

```go
var dataStream chan interface{}
dataStream = make(chan interface{})
```

This example defines a channel, ``dataStream``, upon which any value can be written or read (because we used the empty interface). Channels can also be declared to only support a unidirectional flow of data

To declare a unidirectional channel, you’ll simply include the ``<-`` operator. To both declare and instantiate a channel that can only read, place the ``<-`` operator on the lefthand side, like so:

```go
var dataStream <-chan interface{}
dataStream := make(<-chan interface{})
```

And to declare and create a channel that can only send, you place the ``<-`` operator on the righthand side, like so:

```go
var dataStream chan<- interface{}
dataStream := make(chan<- interface{})
```

don’t often see unidirectional channels instantiated, but you’ll often see them used as function parameters and return types, which is very useful, as we’ll see. This is possible because Go will implicitly convert bidirectional channels to unidirectional channels when needed

```go
var receiveChan <-chan interface{}
var sendChan chan<- interface{}
dataStream := make(chan interface{})
// Valid statements:
receiveChan = dataStream
sendChan = dataStream
```

Keep in mind channels are typed Here’s an example of a channel for integers; I’m also going to switch to the more canonical way of instantiating channels for brevity now that we’re past the introduction

```go
intStream := make(chan int)
```

To use channels, we’ll once again make use of the ``<-`` operator. Sending is done by placing the ``<-`` operator to the right of a channel, and receiving is done by placing the ``<-`` operator to the left of the channel. Another way to think of this is the data flows into the variable in the direction the arrow points

```go
stringStream := make(chan string)
go func() {
	stringStream <- "Hello channels!" // 1
}()
fmt.Println(<-stringStream) // 2
```

1- Here we pass a string literal onto the channel ``stringStream``.
2- Here we read the string literal off of the channel and print it out to ``stdout``. 

All you need is a channel variable and you can pass data onto it and read data off of it; however, it is an error to try and write a value onto a read-only channel, and an error to read a value from a write-only channel. If we try and compile the following example, Go’s compiler will let us know that we’re doing something illegal:

```go
writeStream := make(chan<- interface{})
readStream := make(<-chan interface{})
<-writeStream
readStream <- struct{}{}
```

```go
invalid operation: <-writeStream (receive from send-only type
chan<- interface {})
invalid operation: readStream <- struct {} literal (send to receive-only
type <-chan interface {})
```

This is part of Go’s type system that allows us type-safety even when dealing with concurrency primitives.

just because a goroutine was scheduled, there was no guarantee that it would run before the process exited; yet the previous example is complete and correct with no code omitted. You may have been wondering why the anonymous goroutine completes before the main goroutine does

**==This example works because channels in Go are said to be blocking. This means that any goroutine that attempts to write to a channel that is full will wait until the channel has been emptied, and any goroutine that attempts to read from a channel that is empty will wait until at least one item is placed on it==**

This can cause deadlocks if you don’t structure your program correctly. Take a look at the following example, which introduces a nonsensical conditional to prevent the anonymous goroutine from placing a value on the channel

```go
stringStream := make(chan string)
go func() {
	if 0 != 1 { // 1
		return
}
stringStream <- "Hello channels!"
}()
fmt.Println(<-stringStream)
```

1- Here we ensure the ``stringStream`` channel never gets a value placed upon it.

```go
fatal error: all goroutines are asleep - deadlock!
goroutine 1 [chan receive]:
main.main()
```

The receiving form of the ``<-`` operator can also optionally return two values, like so:

```go
stringStream := make(chan string)
go func() {
stringStream <- "Hello channels!"
}()
salutation, ok := <-stringStream // 1
fmt.Printf("(%v): %v", ok, salutation)
```

```go
(true): Hello channels!
```

The second return value is a way for a read operation to indicate whether the read off the channel was a value generated by a write elsewhere in the process, or a default value generated from a closed channel. Wait a second; a closed channel, what’s that?

In programs, it’s very useful to be able to indicate that no more values will be sent over a channel. This helps downstream processes know when to move on, exit, reopen communications on a new or different channel, etc. We could accomplish this with a special sentinel value for each type, but this would duplicate the effort for all developers, and it’s really a function of the channel and not the data type, so closing a channel is like a universal sentinel

```go
valueStream := make(chan interface{})
close(valueStream)
```

```go
intStream := make(chan int)
close(intStream)
integer, ok := <- intStream // 1
fmt.Printf("(%v): %v", ok, integer)
```

1- Here we read from a closed stream.

```go
(false): 0
```

Notice that we never placed anything on this channel; we closed it immediately. We were still able to perform a read operation, and in fact, we could continue performing reads on this channel indefinitely despite the channel remaining closed. This is to allow support for multiple downstream reads from a single upstream writer on the channel The second value returned—here stored in the ok variable—is false, indicating that the value we received is the zero value for int, or 0, and not a value placed on the stream.

This opens up a few new patterns for us. The first is ranging over a channel. The range keyword—used in conjunction with the for statement—supports channels as arguments, and will automatically break the loop when a channel is closed. This allows for concise iteration over the values on a channel

```go
intStream := make(chan int)
go func() {
	defer close(intStream) // 1
	for i := 1; i <= 5; i++ {
		intStream <- i
}
}()
for integer := range intStream { // 2
fmt.Printf("%v ", integer)
}
```

1- Here we ensure that the channel is closed before we exit the goroutine.
2- Here we range over ``intStream``.


```go
1 2 3 4 5
```

Notice how the loop doesn’t need an exit criteria, and the range does not return the second boolean value. The specifics of handling a closed channel are managed for you to keep the loop concise.

Closing a channel is also one of the ways you can signal multiple goroutines simultaneously. If you have n goroutines waiting on a single channel, instead of writing n times to the channel to unblock each goroutine, you can simply close the channel. Since a closed channel can be read from an infinite number of times, it doesn’t matter how many goroutines are waiting on it, and closing the channel is both cheaper and faster than performing n writes

```go
begin := make(chan interface{})
var wg sync.WaitGroup
for i := 0; i < 5; i++ {
	wg.Add(1)
	go func(i int) {
		defer wg.Done()
		<-begin // 1
		fmt.Printf("%v has begun\n", i)
		}(i)
	}
fmt.Println("Unblocking goroutines...")
close(begin) // 2
wg.Wait()
```

1- Here the goroutine waits until it is told it can continue.
2- Here we close the channel, thus unblocking all the goroutines simultaneously.

the ``sync.Cond`` type to perform the same behavior. You can certainly use that, but as we’ve discussed, channels are composable, so this is my favorite way to unblock multiple goroutines at the same time.

We can also create buffered channels, which are channels that are given a capacity when they’re instantiated. This means that even if no reads are performed on the channel, a goroutine can still perform n writes, where n is the capacity of the buffered channel

```go
var dataStream chan interface{}
dataStream = make(chan interface{}, 4) // 1
```

1 - Here we create a buffered channel with a capacity of four. This means that we can place four things onto the channel regardless of whether it’s being read from

the goroutine that instantiates a channel controls whether it’s buffered. This suggests that the creation of a channel should probably be tightly coupled to goroutines that will be performing writes on it so that we can reason about its behavior and performance more easily

Unbuffered channels are also defined in terms of buffered channels: an unbuffered channel is simply a buffered channel created with a capacity of 0.

```go
a := make(chan int)
b := make(chan int, 0)
```

when we discussed blocking, we said that writes to a channel block if a channel is full, and reads from a channel block if the channel is empty? “Full” and “empty” are functions of the capacity, or buffer size. An unbuffered channel has a capacity of zero and so it’s already full before any writes. A buffered channel with no receivers and a capacity of four would be full after four writes, and block on the fifth write since it has nowhere else to place the fifth element. Like unbuffered channels, buffered channels are still blocking; the preconditions that the channel be empty or full are just different. In this way, buffered channels are an in-memory FIFO queue for concurrent processes to communicate over.

```go
c := make(chan rune, 4)
```

![[Pasted image 20251230201019.png]]

```go
c <- 'A'
```

![[Pasted image 20251230201032.png]]

```go
c <- 'B'
```

![[Pasted image 20251230201120.png]]

```go
c <- 'C'
```

![[Pasted image 20251230201126.png]]

```go
c <- 'D'
```

![[Pasted image 20251230201131.png]]

```go
c <- 'E'
```

![[Pasted image 20251230201138.png]]

```go
<-c
```

![[Pasted image 20251230201152.png]]

As you can see, the read receives the first rune that was placed on the channel, A, the write that was blocked becomes unblocked, and E is placed on the end of the buffer. It also bears mentioning that if a buffered channel is empty and has a receiver, the buffer will be bypassed and the value will be passed directly from the sender to the receiver. In practice, this happens transparently, but it’s worth knowing for understanding the performance profile of buffered channels.

```go
var stdoutBuff bytes.Buffer // 1
defer stdoutBuff.WriteTo(os.Stdout) // 2

intStream := make(chan int, 4) // 3

go func() {
	defer close(intStream)
	defer fmt.Fprintln(&stdoutBuff, "Producer Done.")

	for i := 0; i < 5; i++ {
		fmt.Fprintf(&stdoutBuff, "Sending: %d\n", i)
		intStream <- i
	}
}()

for integer := range intStream {
	fmt.Fprintf(&stdoutBuff, "Received %v.\n", integer)
}

```

- **1. In-memory buffer to reduce nondeterminism**
    
    We create an in-memory buffer to help mitigate the nondeterministic nature of concurrent output.  
    This doesn’t give strict guarantees, but it is faster than writing directly to `stdout`.
    
    ```go
    var stdoutBuff bytes.Buffer
    ```
    
- **2. Ensure buffer is flushed before exit**
    
    We make sure the contents of the buffer are written to `stdout` before the process exits.
    
    ```go
    defer stdoutBuff.WriteTo(os.Stdout)
    ```
    
- **3. Buffered channel with capacity one**
    
    We create a buffered channel with a capacity of one, allowing a single value to be sent without immediately blocking.
    
    ```go
    intStream := make(chan int, 1)
    ```

If a goroutine knows in advance exactly how many values it will send, using a buffered channel sized to that number allows all writes to proceed without blocking, letting the goroutine complete its work as quickly as possible. A different but related concept is the default value of a channel, which is `nil`: interacting with a nil channel causes both sends and receives to block forever, and closing a nil channel will panic. Because of this behavior, nil channels are often used intentionally to disable parts of a `select` statement or to represent an uninitialized or inactive communication path, but they must be handled carefully to avoid deadlocks.

|Operation|Channel State|Result|
|---|---|---|
|Read|nil|Block|
|Read|Open and Not Empty|Value|
|Read|Open and Empty|Block|
|Read|Closed|`<default value>, false`|
|Write|Receive Only|Compilation Error|
|Write|nil|Block|
|Write|Open and Full|Block|
|Write|Open and Not Full|Write Value|
|Write|Closed|panic|
|Close|nil|panic|
|Close|Open and Not Empty|Closes channel; reads succeed until channel is drained, then reads produce default value|
|Close|Open and Empty|Closes channel; reads produce default value|
|Close|Closed|panic|
|Receive|Send Only|Compilation Error|
We have three operations that can cause a goroutine to block, and three operations that can cause your program to panic! At first glance, it looks as though channels might be dangerous to utilize, but after examining the motivation of these results and framing the use of channels, it becomes less scary and begins to make a lot of sense 

The first thing we should do to put channels in the right context is to assign channel ownership. I’ll define ownership as being a goroutine that instantiates, writes, and closes a channel. Much like memory in languages without garbage collection, it’s important to clarify which goroutine owns a channel in order to reason about our programs logically. Unidirectional channel declarations are the tool that will allow us to distinguish between goroutines that own channels and those that only utilize them: channel owners have a write-access view into the channel (`chan` or `chan<-`), and channel utilizers only have a read-only view into the channel (`<-chan`). Once we make this distinction between channel owners and non-channel owners, the results from the preceding table follow naturally, and we can begin to assign responsibilities to goroutines that own channels and those that do not.

Let’s begin with channel owners. The goroutine that owns a channel should:

1. Instantiate the channel.
    
2. Perform writes, or pass ownership to another goroutine.
    
3. Close the channel.
    
4. Encapsulate the previous three things in this list and expose them via a reader channel.
    

By assigning these responsibilities to channel owners, a few things happen:

• Because we’re the one initializing the channel, we remove the risk of deadlocking by writing to a nil channel.  
• Because we’re the one initializing the channel, we remove the risk of panicking by closing a nil channel.  
• Because we’re the one who decides when the channel gets closed, we remove the risk of panicking by writing to a closed channel.  
• Because we’re the one who decides when the channel gets closed, we remove the risk of panicking by closing a channel more than once.  
• We wield the type checker at compile time to prevent improper writes to our channel.

• Knowing when a channel is closed.  
• Responsibly handling blocking for any reason.

To address the first point we simply examine the second return value from the read operation, as discussed previously. The second point is much harder to define because it depends on your algorithm: you may want to time out, you may want to stop reading when someone tells you to, or you may just be content to block for the lifetime of the process. The important thing is that as a consumer you should handle the fact that reads can and will block.

```go
chanOwner := func() <-chan int {
	resultStream := make(chan int, 5) // 1

	go func() { // 2
		defer close(resultStream) // 3

		for i := 0; i <= 5; i++ {
			resultStream <- i
		}
	}()

	return resultStream // 4
}

resultStream := chanOwner()

for result := range resultStream { // 5
	fmt.Printf("Received: %d\n", result)
}

fmt.Println("Done receiving!")
```

• Here we instantiate a buffered channel. Since we know we’ll produce six results, we create a buffered channel of five so that the goroutine can complete as quickly as possible.

• Here we start an anonymous goroutine that performs writes on `resultStream`. Notice that we’ve inverted how we create goroutines: it is now encapsulated within the surrounding function.

• Here we ensure `resultStream` is closed once we’re finished with it. As the channel owner, this is our responsibility.

• Here we return the channel. Since the return value is declared as a read-only channel, `resultStream` will implicitly be converted to read-only for consumers.

• Here we range over `resultStream`. As a consumer, we are only concerned with blocking and closed channels.

Notice how the lifecycle of the `resultStream` channel is encapsulated within the `chanOwner` function. It’s very clear that the writes will not happen on a nil or closed channel, and that the close will always happen once. This removes a large swath of risk from our program.

The consumer function only has access to a read-only channel, and therefore only needs to know how it should handle blocking reads and channel closes. In this small example, we’ve taken the stance that it’s perfectly OK to block the life of the program until the channel is closed.

Channels were one of the things that drew me to Go in the first place. Combined with the simplicity of goroutines and closures, it becomes apparent how easy it is to write clean, correct, concurrent code. In many ways, channels are the glue that binds goroutines together.

## The ``select`` Statement

The select statement is the glue that binds channels together; it’s how we’re able to compose channels together in a program to form larger abstractions. If channels are the glue that binds goroutines together, what does that say about the select statement? It is not an overstatement to say that select statements are one of the most crucial things in a Go program with concurrency. You can find select statements binding together channels locally, within a single function or type, and also globally, at the intersection of two or more components in a system. In addition to joining components, at these critical junctures in your program, select statements can help safely bring channels together with concepts like cancellations, timeouts, waiting, and default values.

Conversely, if select statements are the lingua franca of your program, and they exclusively deal with channels, how do you think the components of your program should coordinate with one another? So what are these powerful select statements? How do we use them, and how do they work? Let’s start by just laying one out. Here’s a very simple example:

```go
var c1, c2 <-chan interface{}
var c3 chan<- interface{}

select {
case <-c1:
	// Do something
case <-c2:
	// Do something
case c3 <- struct{}{}:
	// Do something
}
```

It looks a bit like a switch block, doesn’t it? Just like a switch block, a select block encompasses a series of case statements that guard a series of statements; however, that’s where the similarities end. **==Unlike switch blocks, case statements in a select block aren’t tested sequentially, and execution won’t automatically fall through if none of the criteria are met.==**

Instead, all channel reads and writes are considered simultaneously to see if any of them are ready: populated or closed channels in the case of reads, and channels that are not at capacity in the case of writes. If none of the channels are ready, the entire select statement blocks. Then, when one of the channels becomes ready, that operation will proceed, and its corresponding statements will execute.

```go
start := time.Now()
c := make(chan interface{})

go func() {
	time.Sleep(5 * time.Second)
	close(c) // 1
}()

fmt.Println("Blocking on read...")

select {
case <-c: // 2
}
```

Here we close the channel after waiting five seconds.  
Here we attempt a read on the channel. Note that as this code is written, we don’t require a `select` statement—we could simply write `<-c`—but we’ll expand on this example.

This produces:

```
Blocking on read...
Unblocked 5.000170047s later.
```

As you can see, we only unblock roughly five seconds after entering the `select` block. This is a simple and efficient way to block while we’re waiting for something to happen, but if we reflect for a moment we can come up with some questions:

• What happens when multiple channels have something to read?  
• What if there are never any channels that become ready?  
• What if we want to do something but no channels are currently ready?

The first question of multiple channels being ready simultaneously seems interesting. Let’s just try it and see what happens!

```go
c1 := make(chan interface{})
close(c1)

c2 := make(chan interface{})
close(c2)

var c1Count, c2Count int

for i := 1000; i >= 0; i-- {
	select {
	case <-c1:
		c1Count++
	case <-c2:
		c2Count++
	}
}

fmt.Printf("c1Count: %d\nc2Count: %d\n", c1Count, c2Count)
```

This produces:
```
c1Count: 505
c2Count: 496
```

As you can see, in a thousand iterations, roughly half the time the select statement read from `c1`, and roughly half the time it read from `c2`. That seems interesting, and maybe a bit too coincidental. In fact, it is. The Go runtime performs a pseudorandom uniform selection over the set of case statements. This means that each case statement has an equal chance of being selected as all the others.

This may seem unimportant at first, but the reasoning behind it is incredibly interesting. The Go runtime cannot know anything about the intent of your select statement; it cannot infer your problem space or why you placed a group of channels together into a select statement. Because of this, the best thing the runtime can do is behave well in the average case. Introducing randomness—specifically, randomly choosing which ready channel to select—ensures that all programs using select tend to perform well on average, without starving any particular channel.

What about the second question: what happens if there are never any channels that become ready? If there’s nothing useful you can do when all channels are blocked, but you also can’t afford to block forever, you may want to time out. Go’s `time` package provides an elegant way to do this using channels, fitting naturally into the select paradigm.

```go
var c <-chan int

select {
case <-c: // 1
case <-time.After(1 * time.Second):
	fmt.Println("Timed out.")
}
```

This case statement will never become unblocked because we’re reading from a nil channel.

This produces:

```
Timed out.
```

The `time.After` function takes a `time.Duration` argument and returns a channel that will send the current time after the duration you provide. This offers a concise and idiomatic way to implement timeouts in `select` statements.

This leaves us with the remaining question: what happens when no channel is ready, and we need to do something in the meantime? Similar to `case` clauses, the `select` statement also allows a `default` clause, which executes if all the channels you’re selecting against are blocking.

```go
start := time.Now()
var c1, c2 <-chan int

select {
case <-c1:
case <-c2:
default:
	fmt.Printf("In default after %v\n\n", time.Since(start))
}
```

This produces:

```
In default after 1.421μs
```

You can see that the `default` statement runs almost instantaneously. This allows you to exit a `select` block without blocking. Most commonly, a `default` clause is used in conjunction with a `for`-`select` loop, allowing a goroutine to continue making progress while waiting for another goroutine to signal a result.

Here’s an example:

```go
done := make(chan interface{})

go func() {
	time.Sleep(5 * time.Second)
	close(done)
}()

workCounter := 0

loop:
for {
	select {
	case <-done:
		break loop
	default:
	}

	// Simulate work
	workCounter++
	time.Sleep(1 * time.Second)
}

fmt.Printf(
	"Achieved %v cycles of work before signalled to stop.\n",
	workCounter,
)
```

This produces:

```
Achieved 5 cycles of work before signalled to stop.
```

In this case, the loop performs work and periodically checks whether it has been told to stop.

Finally, there is a special case for empty `select` statements—those with no `case` clauses at all:

```go
select {}
```

This statement will simply block forever.

# Concurrency Patterns in Go

## Confinement

When working with concurrent code, there are a few different options for safe operation. We’ve gone over two of them:

• Synchronization primitives for sharing memory (e.g., ``sync.Mutex``)
• Synchronization via communicating (e.g., ``channels``)

However, there are a couple of other options that are implicitly safe within multiple concurrent processes:

• Immutable data
• Data protected by confinement

In some sense, immutable data is ideal because it is implicitly concurrent-safe. Each concurrent process may operate on the same data, but it may not modify it. If it wants to create new data, it must create a new copy of the data with the desired modifications. This allows not only a lighter cognitive load on the developer, but can also lead to faster programs if it leads to smaller critical sections

Confinement can also allow for a lighter cognitive load on the developer and smaller critical sections. The techniques to confine concurrent values are a bit more involved than simply passing copies of values

Confinement is the simple yet powerful idea of ensuring information is only ever available from one concurrent process. When this is achieved, a concurrent program is implicitly safe and no synchronization is needed. There are two kinds of confinement possible: ad hoc and lexical.

**==Ad hoc confinement is when you achieve confinement through a convention— whether it be set by the languages community, the group you work within, or the codebase you work within.==** In my opinion, sticking to convention is difficult to achieve on projects of any size unless you have tools to perform static analysis on your code every time someone commits some code

```java
data := make([]int, 4)

loopData := func(handleData chan<- int) {
	defer close(handleData)
	for i := range data {
		handleData <- data[i]
	}
}

handleData := make(chan int)

go loopData(handleData)

for num := range handleData {
	fmt.Println(num)
}
```

The slice of integers `data` is technically visible to both the `loopData` function and the loop that ranges over the `handleData` channel. However, by convention, we treat `data` as if it were _owned_ by `loopData` and only accessed there. This is an example of **confinement by convention** rather than confinement enforced by the language.

Lexical confinement involves using lexical scope to expose only the correct data and concurrency primitives for multiple concurrent processes to use. It makes it impossible to do the wrong thing.

```go
chanOwner := func() <-chan int {
	results := make(chan int, 5) // 1

	go func() {
		defer close(results)
		for i := 0; i <= 5; i++ {
			results <- i
		}
	}()

	return results
}

consumer := func(results <-chan int) { // 3 
	for result := range results {
		fmt.Printf("Received: %d\n", result)
	}
	fmt.Println("Done receiving!")
}

results := chanOwner() // 2
consumer(results)
```


1 - Here we instantiate the channel within the lexical scope of the `chanOwner` function. This limits the scope of the write aspect of the `results` channel to the closure defined below it. In other words, it confines the write aspect of this channel to prevent other goroutines from writing to it.

2 - Here we receive the read aspect of the channel and we’re able to pass it into the `consumer`, which can do nothing but read from it. Once again this confines the main goroutine to a read-only view of the channel.

3 - Here we receive a read-only copy of an `int` channel. By declaring that the only usage we require is read access, we confine usage of the channel within the `consumer` function to only reads.

```go
printData := func(wg *sync.WaitGroup, data []byte) {
	defer wg.Done()
	var buff bytes.Buffer
	for _, b := range data {
		fmt.Fprintf(&buff, "%c", b)
	}
	fmt.Println(buff.String())
}

var wg sync.WaitGroup
wg.Add(2)

data := []byte("golang")

go printData(&wg, data[:3]) // 1
go printData(&wg, data[3:]) // 2

wg.Wait()
```


1- Here we pass in a slice containing the first three bytes in the data structure.

2- Here we pass in a slice containing the last three bytes in the data structure.

 In this example, you can see that because `printData` doesn’t close around the data slice, it cannot access it and needs to take in a slice of bytes to operate on. We pass in different subsets of the slice, thus constraining the goroutines we start to only the part of the slice we’re passing in. Because of the lexical scope, we’ve made it impossible¹ to do the wrong thing, and so we don’t need to synchronize memory access or share data through communication.

So what’s the point? Why pursue confinement if we have synchronization available to us? The answer is improved performance and reduced cognitive load on developers. Synchronization comes with a cost, and if you can avoid it, you won’t have any critical sections, and therefore you won’t have to pay the cost of synchronizing them. You also sidestep an entire class of issues possible with synchronization; developers simply don’t have to worry about these issues.

Concurrent code that utilizes lexical confinement also has the benefit of usually being simpler to understand than concurrent code without lexically confined variables. This is because within the context of your lexical scope, you can write synchronous code.


## The for-select Loop

```go
for { // Either loop infinitely or range over something
	select {
	// Do some work with channels
	}
}
```

There are a couple of different scenarios where you’ll see this pattern pop up.

Sending iteration variables out on a channel  
Oftentimes you’ll want to convert something that can be iterated over into values on a channel. This is nothing fancy, and usually looks something like this:

```go
for _, s := range []string{"a", "b", "c"} {
	select {
	case <-done:
		return
	case stringStream <- s:
	}
}
```

Looping infinitely waiting to be stopped  
It’s very common to create goroutines that loop infinitely until they’re stopped. There are a couple variations of this one. Which one you choose is purely a stylistic preference.

The first variation keeps the select statement as short as possible:

```go
for {
	select {
	case <-done:
		return
	default:
	}
	// Do non-preemptable work
}
```

If the done channel isn’t closed, we’ll exit the select statement and continue on to the rest of our for loop’s body.

The second variation embeds the work in a default clause of the select statement:

```go
for {
	select {
	case <-done:
		return
	default:
		// Do non-preemptable work
	}
}
```

When we enter the select statement, if the done channel hasn’t been

## Preventing Goroutine Leaks

goroutines are cheap and easy to create; it’s one of the things that makes Go such a productive language. The runtime handles multiplexing the goroutines onto any number of operating system threads so that we don’t often have to worry about that level of abstraction. But they do cost resources, and goroutines are not garbage collected by the runtime, so regardless of how small their memory footprint is, we don’t want to leave them lying about our process. So how do we go about ensuring they’re cleaned up?

Let’s start from the beginning and think about this step by step: why would a goroutine exist? In Chapter 2, we established that goroutines represent units of work that may or may not run in parallel with each other. The goroutine has a few paths to termination: when it has completed its work, when it cannot continue its work due to an unrecoverable error, and when it’s told to stop working.

We get the first two paths for free—these paths are your algorithm—but what about work cancellation? This turns out to be the most important bit because of the network effect: if you’ve begun a goroutine, it’s most likely cooperating with several other goroutines in some sort of organized fashion. We could even represent this interconnectedness as a graph: whether or not a child goroutine should continue executing might be predicated on knowledge of the state of many other goroutines. The parent goroutine (often the main goroutine) with this full contextual knowledge should be able to tell its child goroutines to terminate.

```go
doWork := func(strings <-chan string) <-chan interface{} {
	completed := make(chan interface{})
	go func() {
		defer fmt.Println("doWork exited.")
		defer close(completed)
		for s := range strings {
			// Do something interesting
			fmt.Println(s)
		}
	}()
	return completed
}

doWork(nil)

// Perhaps more work is done here
fmt.Println("Done.")
```

Here we see that the main goroutine passes a nil channel into `doWork`. Therefore, the `strings` channel will never actually get any strings written onto it, and the goroutine containing `doWork` will remain in memory for the lifetime of this process (we would even deadlock if we joined the goroutine within `doWork` and the main goroutine).

In this example, the lifetime of the process is very short, but in a real program, goroutines could easily be started at the beginning of a long-lived program. In the worst case, the main goroutine could continue to spin up goroutines throughout its life, causing creep in memory utilization.

The way to successfully mitigate this is to establish a signal between the parent goroutine and its children that allows the parent to signal cancellation to its children. By convention, this signal is usually a read-only channel named `done`. The parent goroutine passes this channel to the child goroutine and then closes the channel when it wants to cancel the child goroutine.

```go
doWork := func(
	done <-chan interface{},
	strings <-chan string,
) <-chan interface{} { // 1
	terminated := make(chan interface{})
	go func() {
		defer fmt.Println("doWork exited.")
		defer close(terminated)
		for {
			select {
			case s := <-strings: // Do something interesting
				fmt.Println(s)
			case <-done:
				return // 2
			}
		}
	}()
	return terminated
}

done := make(chan interface{})
terminated := doWork(done, nil)

go func() { // 3
	// Cancel the operation after 1 second.
	time.Sleep(1 * time.Second)
	fmt.Println("Canceling doWork goroutine...")
	close(done)
}()

<-terminated // 4
fmt.Println("Done.")
```

Here we pass the `done` channel to the `doWork` function. As a convention, this channel is the first parameter.

On this line we see the ubiquitous for-select pattern in use. One of our case statements is checking whether our `done` channel has been signaled. If it has, we return from the goroutine.

Here we create another goroutine that will cancel the goroutine spawned in `doWork` if more than one second passes.

This is where we join the goroutine spawned from `doWork` with the main goroutine.

And the resulting output is:

```
Canceling doWork goroutine...
doWork exited.
Done.
```

despite passing in nil for our strings channel, our goroutine still exits successfully. Unlike the example before it, in this example we do join the two goroutines and yet do not receive a deadlock. **==This is because before we join the two goroutines, we create a third goroutine to cancel the goroutine within ``doWork`` after a second. We have successfully eliminated our goroutine leak!==**

```go
newRandStream := func() <-chan int {
	randStream := make(chan int)
	go func() {
		defer fmt.Println("newRandStream closure exited.")
		defer close(randStream)
		for {
			randStream <- rand.Int()
		}
	}()
	return randStream
}

randStream := newRandStream()

fmt.Println("3 random ints:")
for i := 1; i <= 3; i++ {
	fmt.Printf("%d: %d\n", i, <-randStream)
}
```

Here we print out a message when the goroutine successfully terminates. You can see from the output that the deferred `fmt.Println` statement never gets run. After the third iteration of our loop, our goroutine blocks trying to send the next random integer to a channel that is no longer being read from. We have no way of telling the producer it can stop.

The solution, just like for the receiving case, is to provide the producer goroutine with a channel informing it to exit.

```go
newRandStream := func(done <-chan interface{}) <-chan int {
	randStream := make(chan int)
	go func() {
		defer fmt.Println("newRandStream closure exited.")
		defer close(randStream)
		for {
			select {
			case randStream <- rand.Int():
			case <-done:
				return
			}
		}
	}()
	return randStream
}

done := make(chan interface{})
randStream := newRandStream(done)

fmt.Println("3 random ints:")
for i := 1; i <= 3; i++ {
	fmt.Printf("%d: %d\n", i, <-randStream)
}

close(done)

// Simulate ongoing work
time.Sleep(1 * time.Second)
```

This code produces:

```
3 random ints:
1: 5577006791947779410
2: 8674665223082153551
3: 6129484611666145821
newRandStream closure exited.
```

We see now that the goroutine is being properly cleaned up.

## The or-channel

At times you may find yourself wanting to combine one or more done channels into a single done channel that closes if any of its component channels close. It is perfectly acceptable, albeit verbose, to write a select statement that performs this coupling; however, sometimes you can’t know the number of done channels you’re working with at runtime. In this case, or if you just prefer a one-liner, you can combine these channels together using the or-channel pattern.

This pattern creates a composite done channel through recursion and goroutines. Let’s have a look:

```go
var or func(channels ...<-chan interface{}) <-chan interface{}

or = func(channels ...<-chan interface{}) <-chan interface{} {
	switch len(channels) {
	case 0:
		return nil
	case 1:
		return channels[0]
	}

	orDone := make(chan interface{})
	go func() {
		defer close(orDone)

		switch len(channels) {
		case 2:
			select {
			case <-channels[0]:
			case <-channels[1]:
			}
		default:
			select {
			case <-channels[0]:
			case <-channels[1]:
			case <-channels[2]:
			case <-or(append(channels[3:], orDone)...):
			}
		}
	}()
	return orDone
}
```

Here we have our function, `or`, which takes in a variadic slice of channels and returns a single channel.

Since this is a recursive function, we must set up termination criteria. The first is that if the variadic slice is empty, we simply return a nil channel. This is consistent with the idea of passing in no channels; we wouldn’t expect a composite channel to do anything.

Our second termination criteria states that if our variadic slice only contains one element, we just return that element.

Here is the main body of the function, and where the recursion happens. We create a goroutine so that we can wait for messages on our channels without blocking.

Because of how we’re recusing, every recursive call to `or` will at least have two channels. As an optimization to keep the number of goroutines constrained, we place a special case here for calls to `or` with only two channels.

Here we recursively create an or-channel from all the channels in our slice after the third index, and then select from this. This recurrence relation will destructure the rest of the slice into or-channels to form a tree from which the first signal will return. We also pass in the `orDone` channel so that when goroutines up the tree exit, goroutines down the tree also exit.

This is a fairly concise function that enables you to combine any number of channels together into a single channel that will close as soon as any of its component channels are closed or written to.

Let’s take a look at how we can use this function. Here’s a brief example that takes channels that close after a set duration and uses the `or` function to combine these into a single channel that closes:

```go
sig := func(after time.Duration) <-chan interface{} {
	c := make(chan interface{})
	go func() {
		defer close(c)
		time.Sleep(after)
	}()
	return c
}

start := time.Now()

<-or(
	sig(2*time.Hour),
	sig(5*time.Minute),
	sig(1*time.Second),
	sig(1*time.Hour),
	sig(1*time.Minute),
)

fmt.Printf("done after %v", time.Since(start))
```

This function simply creates a channel that will close when the time specified in `after` elapses.

Here we keep track of roughly when the channel from the `or` function begins to block.

And here we print the time it took for the read to occur.

If you run this program you will get:

Notice that despite placing several channels in our call to `or` that take various times to close, our channel that closes after one second causes the entire channel created by the call to `or` to close. This is because—despite its place in the tree the `or` function builds—it will always close first, and thus the channels that depend on its closure will close as well.

This pattern is useful to employ at the intersection of modules in your system. At these intersections, you tend to have multiple conditions for canceling trees of goroutines through your call stack. Using the `or` function, you can simply combine these together and pass it down the stack.

When Go eschewed the popular exception model of errors, it made a statement that error handling was important, and that as we develop our programs, we should give our error paths the same attention we give our algorithms. In that spirit, let’s take a look at how we do that when working with multiple concurrent processes.

The most fundamental question when thinking about error handling is, “Who should be responsible for handling the error?” At some point, the program needs to stop ferrying the error up the stack and actually do something with it. What is responsible for this?

With concurrent processes, this question becomes a little more complex. Because a concurrent process is operating independently of its parent or siblings, it can be difficult for it to reason about what the right thing to do with the error is.

```go
checkStatus := func(
	done <-chan interface{},
	urls ...string,
) <-chan *http.Response {
	responses := make(chan *http.Response)
	go func() {
		defer close(responses)
		for _, url := range urls {
			resp, err := http.Get(url)
			if err != nil {
				fmt.Println(err)
			}
			select {
			case <-done:
				return
			case responses <- resp:
			}
		}
	}()
	return responses
}

done := make(chan interface{})
defer close(done)

urls := []string{"https://www.google.com", "https://badhost"}

for response := range checkStatus(done, urls...) {
	fmt.Printf("Response: %v\n", response.Status)
}
```

Here we see the goroutine doing its best to signal that there’s an error. What else can it do? It can’t pass it back! How many errors is too many? Does it continue making requests?

Running this code produces:

```
Response: 200 OK
Get https://badhost: dial tcp: lookup badhost on 127.0.1.1:53: no such host
```

The goroutine has been given no choice in the matter. It can’t simply swallow the error, and so it does the only sensible thing: it prints the error and hopes something is paying attention. Don’t put your goroutines in this awkward position. I suggest you separate your concerns: in general, your concurrent processes should send their errors to another part of your program that has complete information about the state of your program and can make a more informed decision about what to do.

```go
type Result struct {
	Error    error
	Response *http.Response
}

checkStatus := func(done <-chan interface{}, urls ...string) <-chan Result {
	results := make(chan Result)
	go func() {
		defer close(results)
		for _, url := range urls {
			var result Result
			resp, err := http.Get(url)
			result = Result{Error: err, Response: resp}
			select {
			case <-done:
				return
			case results <- result:
			}
		}
	}()
	return results
}

done := make(chan interface{})
defer close(done)

urls := []string{"https://www.google.com", "https://badhost"}

for result := range checkStatus(done, urls...) {
	if result.Error != nil {
		fmt.Printf("error: %v", result.Error)
		continue
	}
	fmt.Printf("Response: %v\n", result.Response.Status)
}
```

Here we create a type that encompasses both the `*http.Response` and the error possible from an iteration of the loop within our goroutine.

This line returns a channel that can be read from to retrieve results of an iteration of our loop.

Here we create a `Result` instance with the `Error` and `Response` fields set.

This is where we write the `Result` to our channel.

Here, in our main goroutine, we are able to deal with errors coming out of the goroutine started by `checkStatus` intelligently and with the full context of the larger program.

This code produces:

```
Response: 200 OK
error: Get https://badhost: dial tcp: lookup badhost on 127.0.1.1:53: no such host
```

==**The key thing to note here is how we’ve coupled the potential result with the potential error. This represents the complete set of possible outcomes created from the goroutine `checkStatus`, and allows our main goroutine to make decisions about what to do when errors occur.**==

## Error Handling

When Go eschewed the popular exception model of errors, it made a statement that error handling was important, and that as we develop our programs, we should give our error paths the same attention we give our algorithms. In that spirit, let’s take a look at how we do that when working with multiple concurrent processes.

The most fundamental question when thinking about error handling is, “Who should be responsible for handling the error?” At some point, the program needs to stop ferrying the error up the stack and actually do something with it. What is responsible for this?

With concurrent processes, this question becomes a little more complex. Because a concurrent process is operating independently of its parent or siblings, it can be difficult for it to reason about what the right thing to do with the error is.

```go
checkStatus := func(
	done <-chan interface{},
	urls ...string,
) <-chan *http.Response {
	responses := make(chan *http.Response)
	go func() {
		defer close(responses)
		for _, url := range urls {
			resp, err := http.Get(url)
			if err != nil {
				fmt.Println(err)
				continue
			}
			select {
			case <-done:
				return
			case responses <- resp:
			}
		}
	}()
	return responses
}

done := make(chan interface{})
defer close(done)

urls := []string{"https://www.google.com", "https://badhost"}

for response := range checkStatus(done, urls...) {
	fmt.Printf("Response: %v\n", response.Status)
}
```

Here we see the goroutine doing its best to signal that there’s an error. What else can it do? It can’t pass it back! How many errors is too many? Does it continue making requests?

Running this code produces:

```
Response: 200 OK
Get https://badhost: dial tcp: lookup badhost on 127.0.1.1:53: no such host
```

Here we see that the goroutine has been given no choice in the matter. **==It can’t simply swallow the error, and so it does the only sensible thing: it prints the error and hopes something is paying attention.==** Don’t put your goroutines in this awkward position. I suggest you separate your concerns: in general, your concurrent processes should send their errors to another part of your program that has complete information about the state of your program, and can make a more informed decision about what to do.

The following example demonstrates a correct solution to this problem:

```go
type Result struct {
	Error    error
	Response *http.Response
}

checkStatus := func(done <-chan interface{}, urls ...string) <-chan Result {
	results := make(chan Result)
	go func() {
		defer close(results)
		for _, url := range urls {
			var result Result
			resp, err := http.Get(url)
			result = Result{Error: err, Response: resp}
			select {
			case <-done:
				return
			case results <- result:
			}
		}
	}()
	return results
}

done := make(chan interface{})
defer close(done)

urls := []string{"https://www.google.com", "https://badhost"}

for result := range checkStatus(done, urls...) {
	if result.Error != nil {
		fmt.Printf("error: %v", result.Error)
		continue
	}
	fmt.Printf("Response: %v\n", result.Response.Status)
}
```

Here we create a type that encompasses both the `*http.Response` and the error possible from an iteration of the loop within our goroutine.

This line returns a channel that can be read from to retrieve results of an iteration of our loop.

Here we create a `Result` instance with the `Error` and `Response` fields set.

This is where we write the `Result` to our channel.

Here, in our main goroutine, we are able to deal with errors coming out of the goroutine started by `checkStatus` intelligently, and with the full context of the larger program.

This code produces:

```
Response: 200 OK
error: Get https://badhost: dial tcp: lookup badhost on 127.0.1.1:53: no such host
```

==**The key thing to note here is how we’ve coupled the potential result with the potential error. This represents the complete set of possible outcomes created from the goroutine `checkStatus`, and allows our main goroutine to make decisions about what to do when errors occur.**==

## Pipelines

A pipeline is just another tool you can use to form an abstraction in your system. In particular, it is a very powerful tool to use when your program needs to process streams or batches of data. The word _pipeline_ is believed to have first been used in 1856, and likely referred to a line of pipes that transported liquid from one place to another. We borrow this term in computer science because we’re also transporting something from one place to another: data.

A pipeline is nothing more than a series of things that take data in, perform an operation on it, and pass the data back out. We call each of these operations a stage of the pipeline.

By using a pipeline, you separate the concerns of each stage, which provides numerous benefits. You can modify stages independent of one another, you can mix and match how stages are combined independent of modifying the stages, you can process each stage concurrent to upstream or downstream stages, and you can fan-out or rate-limit portions of your pipeline.

```go
multiply := func(values []int, multiplier int) []int {
	multipliedValues := make([]int, len(values))
	for i, v := range values {
		multipliedValues[i] = v * multiplier
	}
	return multipliedValues
}
```

```go
add := func(values []int, additive int) []int {
	addedValues := make([]int, len(values))
	for i, v := range values {
		addedValues[i] = v + additive
	}
	return addedValues
}
```

```go
ints := []int{1, 2, 3, 4}
for _, v := range add(multiply(ints, 2), 1) {
	fmt.Println(v)
}
```

• A stage consumes and returns the same type.  
• A stage must be reified by the language so that it may be passed around. Functions in Go are reified and fit this purpose nicely.

Pipeline stages are very closely related to functional programming and can be considered a subset of monads.

Here, our `add` and `multiply` stages satisfy all the properties of a pipeline stage: they both consume a slice of `int` and return a slice of `int`, and because Go has reified functions, we can pass `add` and `multiply` around. These properties give rise to the interesting properties of pipeline stages we mentioned earlier: namely it becomes very easy to combine our stages at a higher level without modifying the stages themselves.

For example, if we wanted to now add an additional stage to our pipeline to multiply by two, we’d simply wrap our previous pipeline in a new multiply stage, like so:

```go
ints := []int{1, 2, 3, 4}
for _, v := range multiply(add(multiply(ints, 2), 1), 2) {
	fmt.Println(v)
}
```

There are pros and cons to batch processing versus stream processing, which we’ll discuss in just a bit. For now, notice that for the original data to remain unaltered, each stage has to make a new slice of equal length to store the results of its calculations. That means that the memory footprint of our program at any one time is double the size of the slice we send into the start of our pipeline.

Let’s convert our stages to be stream oriented and see what that looks like:

```go
multiply := func(value, multiplier int) int {
	return value * multiplier
}

add := func(value, additive int) int {
	return value + additive
}

ints := []int{1, 2, 3, 4}
for _, v := range ints {
	fmt.Println(multiply(add(multiply(v, 2), 1), 2))
}
```

This code produces:

```
6
10
14
18
```

Each stage is receiving and emitting a discrete value, and the memory footprint of our program is back down to only the size of the pipeline’s input. But we had to pull the pipeline down into the body of the `for` loop and let the range do the heavy lifting of feeding our pipeline. Not only does this limit the reuse of how we feed the pipeline.

I could probably extend our `multiply` and `add` functions a little more to introduce these concepts, but they’ve done their job of introducing the concept of a pipeline. It’s time to begin learning what best practices exist for constructing pipelines in Go, and it begins with Go’s channel primitive.

### Best Practices for Constructing Pipelines

Channels are uniquely suited to constructing pipelines in Go because they fulfill all of our basic requirements. They can receive and emit values, they can safely be used concurrently, they can be ranged over, and they are reified by the language.

```go
generator := func(done <-chan interface{}, integers ...int) <-chan int {
	intStream := make(chan int)
	go func() {
		defer close(intStream)
		for _, i := range integers {
			select {
			case <-done:
				return
			case intStream <- i:
			}
		}
	}()
	return intStream
}
```

```go
multiply := func(
	done <-chan interface{},
	intStream <-chan int,
	multiplier int,
) <-chan int {
	multipliedStream := make(chan int)
	go func() {
		defer close(multipliedStream)
		for i := range intStream {
			select {
			case <-done:
				return
			case multipliedStream <- i * multiplier:
			}
		}
	}()
	return multipliedStream
}
```

```go
add := func(
	done <-chan interface{},
	intStream <-chan int,
	additive int,
) <-chan int {
	addedStream := make(chan int)
	go func() {
		defer close(addedStream)
		for i := range intStream {
			select {
			case <-done:
				return
			case addedStream <- i + additive:
			}
		}
	}()
	return addedStream
}
```

```go
done := make(chan interface{})
defer close(done)

intStream := generator(done, 1, 2, 3, 4)
pipeline := multiply(done, add(done, multiply(done, intStream, 2), 1), 2)

for v := range pipeline {
	fmt.Println(v)
}
```

This code produces:

```
6
10
14
18
```

What exactly have we gained? First, let’s examine what we’ve written. We now have three functions instead of two. They all start a goroutine inside their bodies and use the pattern we established earlier of taking in a channel to signal that the goroutine should exit. They all return channels, and some of them also take channels as input.

The first thing our program does is create a done channel and defer its closure. As discussed previously, this ensures our program exits cleanly and never leaks goroutines.

```go
done := make(chan interface{})
defer close(done)
```

Next, let’s take a look at the generator function.

```go
generator := func(done <-chan interface{}, integers ...int) <-chan int {
	intStream := make(chan int)
	go func() {
		defer close(intStream)
		for _, i := range integers {
			select {
			case <-done:
				return
			case intStream <- i:
			}
		}
	}()
	return intStream
}
```

```go
intStream := generator(done, 1, 2, 3, 4)
```

The generator function takes in a variadic slice of integers, constructs a channel of integers, starts a goroutine, and returns the constructed channel. Inside the goroutine, it ranges over the incoming integers and sends them onto the channel. The send operation is guarded by a select statement that also listens on the done channel.

```go
pipeline := multiply(done, add(done, multiply(done, intStream, 2), 1), 2)
```

It’s the same pipeline we’ve been working with all along: for a stream of numbers, we multiply them by two, add one, and then multiply the result by two.

This pipeline is similar to the function-based pipeline from earlier examples, but it differs in important ways. First, we’re using channels, which allows us to range over the final output and safely execute each stage concurrently.

Second, each stage of the pipeline executes concurrently. Each stage only needs to wait for its input and for the ability to send its output. This has significant implications, which we’ll explore later, but for now it’s enough to note that the stages can operate independently of one another for portions of time.

### Some Handy Generators

As a reminder, a generator for a pipeline is any function that converts a set of discrete values into a stream of values on a channel. Let’s take a look at a generator called `repeat`:

```go
repeat := func(
	done <-chan interface{},
	values ...interface{},
) <-chan interface{} {
	valueStream := make(chan interface{})
	go func() {
		defer close(valueStream)
		for {
			for _, v := range values {
				select {
				case <-done:
					return
				case valueStream <- v:
				}
			}
		}
	}()
	return valueStream
}
```

This function will repeat the values you pass to it infinitely until you tell it to stop.

Let’s take a look at another generic pipeline stage that is helpful when used in combination with `repeat`, `take`:

```go
take := func(
	done <-chan interface{},
	valueStream <-chan interface{},
	num int,
) <-chan interface{} {
	takeStream := make(chan interface{})
	go func() {
		defer close(takeStream)
		for i := 0; i < num; i++ {
			select {
			case <-done:
				return
			case takeStream <- <-valueStream:
			}
		}
	}()
	return takeStream
}
```

This pipeline stage will only take the first `num` items off of its incoming `valueStream` and then exit. Together, the two can be very powerful:

```go
done := make(chan interface{})
defer close(done)

for num := range take(done, repeat(done, 1), 10) {
	fmt.Printf("%v ", num)
}
```

Running this code produces:

```
1 1 1 1 1 1 1 1 1 1
```

Let’s create another repeating generator, but this time let’s create one that repeatedly calls a function. Let’s call it `repeatFn`:

```go
repeatFn := func(
	done <-chan interface{},
	fn func() interface{},
) <-chan interface{} {
	valueStream := make(chan interface{})
	go func() {
		defer close(valueStream)
		for {
			select {
			case <-done:
				return
			case valueStream <- fn():
			}
		}
	}()
	return valueStream
}
```

Let’s use it to generate 10 random numbers:

```go
done := make(chan interface{})
defer close(done)

rand := func() interface{} { return rand.Int() }

for num := range take(done, repeatFn(done, rand), 10) {
	fmt.Println(num)
}
```

You may be wondering why all of these generators and stages are receiving and sending on channels of `interface{}`. We could have just as easily written these functions to be specific to a type, or maybe written a Go generator.

Empty interfaces are a bit taboo in Go, but for pipeline stages it is my opinion that it’s OK to deal in channels of `interface{}` so that you can use a standard library of pipeline patterns. As we discussed earlier, a lot of a pipeline’s utility comes from reusable stages. This is best achieved when the stages operate at the level of specificity appropriate to themselves. In the `repeat` and `repeatFn` generators, the concern is generating a stream of data by looping over a list or operator. With the `take` stage, the concern is limiting our pipeline. None of these operations require information about the types they’re working on, but instead only require knowledge of the arity of their parameters.

## Fan-Out, Fan-In

Sometimes, stages in your pipeline can be particularly computationally expensive. When this happens, upstream stages in your pipeline can become blocked while waiting for your expensive stages to complete. Not only that, but the pipeline itself can take a long time to execute as a whole. How can we address this?

One of the interesting properties of pipelines is the ability they give you to operate on the stream of data using a combination of separate, often reorderable stages. You can even reuse stages of the pipeline multiple times. Wouldn’t it be interesting to reuse a single stage of our pipeline on multiple goroutines in an attempt to parallelize pulls from an upstream stage? Maybe that would help improve the performance of the pipeline.

Fan-out is a term to describe the process of starting multiple goroutines to handle input from the pipeline, and fan-in is a term to describe the process of combining multiple results into one channel.

So what makes a stage of a pipeline suited for utilizing this pattern? You might consider fanning out one of your stages if both of the following apply:

- It doesn’t rely on values that the stage had calculated before.
    
- It takes a long time to run.
    

==**The property of order-independence is important because you have no guarantee in what order concurrent copies of your stage will run, nor in what order they will return.**==

```go
rand := func() interface{} { return rand.Intn(50000000) }

done := make(chan interface{})
defer close(done)

start := time.Now()

randIntStream := toInt(done, repeatFn(done, rand))

fmt.Println("Primes:")
for prime := range take(done, primeFinder(done, randIntStream), 10) {
	fmt.Printf("\t%d\n", prime)
}

fmt.Printf("Search took: %v", time.Since(start))
```

We’re generating a stream of random numbers, capped at 50,000,000, converting the stream into an integer stream, and then passing that into our `primeFinder` stage. `primeFinder` naively begins to attempt to divide the number provided on the input stream by every number below it. If it’s unsuccessful, it passes the value on to the next stage. Certainly, this is a horrible way to try and find prime numbers, but it fulfills our requirement of taking a long time.

In our `for` loop, we range over the found primes, print them out as they come in, and—thanks to our `take` stage—close the pipeline after 10 primes are found. We then print out how long the search took, and the `done` channel is closed by a `defer` statement and the pipeline is torn down.

Fortunately the process of fanning out a stage in a pipeline is extraordinarily easy. All we have to do is start multiple versions of that stage. So instead of this:

```go
primeStream := primeFinder(done, randIntStream)
```

We can do something like this:

```go
numFinders := runtime.NumCPU()

finders := make([]<-chan int, numFinders)
for i := 0; i < numFinders; i++ {
	finders[i] = primeFinder(done, randIntStream)
}
```

And that’s it! We now have eight goroutines pulling from the random number generator and attempting to determine whether the number is prime. Generating random numbers shouldn’t take much time, and so each goroutine for the `findPrimes` stage should be able to determine whether its number is prime and then have another random number available to it immediately.

We still have a problem though: now that we have four goroutines, we also have four channels, but our range over primes is only expecting one channel. This brings us to the fan-in portion of the pattern.

As we discussed earlier, fanning in means multiplexing or joining together multiple streams of data into a single stream. The algorithm to do so is relatively simple:

```go
fanIn := func(
	done <-chan interface{},
	channels ...<-chan interface{},
) <-chan interface{} {
	var wg sync.WaitGroup
	multiplexedStream := make(chan interface{})

	multiplex := func(c <-chan interface{}) {
		defer wg.Done()
		for i := range c {
			select {
			case <-done:
				return
			case multiplexedStream <- i:
			}
		}
	}

	// Select from all the channels
	wg.Add(len(channels))
	for _, c := range channels {
		go multiplex(c)
	}

	// Wait for all the reads to complete
	go func() {
		wg.Wait()
		close(multiplexedStream)
	}()

	return multiplexedStream
}
```

Here we take in our standard `done` channel to allow our goroutines to be torn down, and then a variadic slice of `interface{}` channels to fan-in.

On this line we create a `sync.WaitGroup` so that we can wait until all channels have been drained.

Here we create a function, `multiplex`, which, when passed a channel, will read from the channel and pass the value read onto the `multiplexedStream` channel.

This line increments the `sync.WaitGroup` by the number of channels we’re multiplexing.

Here we create a goroutine to wait for all the channels we’re multiplexing to be drained so that we can close the `multiplexedStream` channel.

## The or-done-channel

At times you will be working with channels from disparate parts of your system.  
Unlike with pipelines, you can’t make any assertions about how a channel will behave  
when code you’re working with is canceled via its `done` channel. That is to say, you  
don’t know if the fact that your goroutine was canceled means the channel you’re  
reading from will have been canceled.

Doing so takes code that’s easily read like this:

```go
for val := range myChan {
	// Do something with val
}
```

And explodes it out into this:

```go
loop:
for {
	select {
	case <-done:
		break loop
	case maybeVal, ok := <-myChan:
		if ok == false {
			return // or maybe break from for
		}
		// Do something with val
	}
}
```

This can get busy quite quickly—especially if you have nested loops. Continuing with  
the theme of utilizing goroutines to write clearer concurrent code, and not prematurely  
optimizing, we can fix this with a single goroutine. We encapsulate the verbosity  
so that others don’t have to:

```go
orDone := func(done, c <-chan interface{}) <-chan interface{} {
	valStream := make(chan interface{})
	go func() {
		defer close(valStream)
		for {
			select {
			case <-done:
				return
			case v, ok := <-c:
				if ok == false {
					return
				}
				select {
				case valStream <- v:
				case <-done:
				}
			}
		}
	}()
	return valStream
}
```

Doing this allows us to get back to simple for loops, like so:

```go
for val := range orDone(done, myChan) {
	// Do something with val
}
```

## The tee-channel

Sometimes you may want to split values coming in from a channel so that you can  
send them off into two separate areas of your codebase. Imagine a channel of user  
commands: you might want to take in a stream of user commands on a channel, send  
them to something that executes them, and also send them to something that logs the  
commands for later auditing.

Taking its name from the `tee` command in Unix-like systems, the tee-channel does  
just this. You can pass it a channel to read from, and it will return two separate channels  
that will get the same value:

```go
tee := func(
	done <-chan interface{},
	in <-chan interface{},
) (_, _ <-chan interface{}) {
	out1 := make(chan interface{})
	out2 := make(chan interface{})

	go func() {
		defer close(out1)
		defer close(out2)

		for val := range orDone(done, in) {
			var out1, out2 = out1, out2
			for i := 0; i < 2; i++ {
				select {
				case <-done:
				case out1 <- val:
					out1 = nil
				case out2 <- val:
					out2 = nil
				}
			}
		}
	}()
	return out1, out2
}
```

We will want to use local versions of `out1` and `out2`, so we shadow these  
variables.

We’re going to use one `select` statement so that writes to `out1` and `out2` don’t  
block each other. To ensure both are written to, we’ll perform two iterations of  
the `select` statement: one for each outbound channel.

Once we’ve written to a channel, we set its shadowed copy to `nil` so that further  
writes will block and the other channel may continue.

Notice that writes to `out1` and `out2` are tightly coupled. The iteration over `in` cannot  
continue until both `out1` and `out2` have been written to. Usually this is not a problem  
as handling the throughput of the process reading from each channel should be a  
concern of something other than the tee command anyway, but it’s worth noting.

Here’s a quick example to demonstrate:

```go
done := make(chan interface{})
defer close(done)

out1, out2 := tee(done, take(done, repeat(done, 1, 2), 4))

for val1 := range out1 {
	fmt.Printf("out1: %v, out2: %v\n", val1, <-out2)
}
```

Utilizing this pattern, it’s easy to continue using channels as the join points of your  
system

## The bridge-channel

In some circumstances, you may find yourself wanting to consume values from a  
sequence of channels:

```go
<-chan <-chan interface{}
```

This is slightly different than coalescing a slice of channels into a single channel, as   we saw in earlier patterns like the or-channel or fan-out/fan-in. A sequence of channels  suggests an ordered write, albeit from different sources.

One example might be a pipeline stage whose lifetime is intermittent. If we follow the  patterns established in _Confinement_ and ensure channels are owned by the goroutines   that write to them, every time a pipeline stage is restarted within a new goroutine, a new   channel would be created. This means we’d effectively have a sequence of channels.   We’ll explore this scenario more when discussing healing unhealthy goroutines.

As a consumer, the code may not care about the fact that its values come from a sequence of channels. In that case, dealing with a channel of channels can be cumbersome.   If we instead define a function that can destructure the channel of channels into a simple  channel—a technique called **bridging the channels**—this will make it much easier for   the consumer to focus on the problem at hand.

Here’s how we can achieve that:

```go
bridge := func(
	done <-chan interface{},
	chanStream <-chan <-chan interface{},
) <-chan interface{} {
	valStream := make(chan interface{})

	go func() {
		defer close(valStream)
		for {
			var stream <-chan interface{}
			select {
			case maybeStream, ok := <-chanStream:
				if ok == false {
					return
				}
				stream = maybeStream
			case <-done:
				return
			}

			for val := range orDone(done, stream) {
				select {
				case valStream <- val:
				case <-done:
				}
			}
		}
	}()
	return valStream
}
```

This is the channel that will return all values from `bridge`.

This loop is responsible for pulling channels off of `chanStream` and providing   them to a nested loop for use.

This loop is responsible for reading values off the channel it has been given and  repeating those values onto `valStream`. When the stream we’re currently looping   over is closed, we break out of the loop performing the reads from this channel,   and continue with the next iteration of the loop, selecting channels to read from. This provides us with an unbroken stream of values.

This is pretty straightforward code. Now we can use `bridge` to help present a  single-channel facade over a channel of channels.

Here’s an example that creates a series of 10 channels, each with one element written  to them, and passes these channels into the `bridge` function:

```go
genVals := func() <-chan <-chan interface{} {
	chanStream := make(chan (<-chan interface{}))
	go func() {
		defer close(chanStream)
		for i := 0; i < 10; i++ {
			stream := make(chan interface{}, 1)
			stream <- i
			close(stream)
			chanStream <- stream
		}
	}()
	return chanStream
}

for v := range bridge(nil, genVals()) {
	fmt.Printf("%v ", v)
}
```

Running this produces:

```
0 1 2 3 4 5 6 7 8 9
```

Thanks to `bridge`, we can use the channel of channels from within a single `range`  
statement and focus on our loop’s logic. Destructuring the channel of channels is left   to code that is specific to this concern.

## Queuing

Sometimes it’s useful to begin accepting work for your pipeline even though the pipeline is not yet ready for more. This process is called queuing.

All this means is that once your stage has completed some work, it stores it in a temporary location in memory so that other stages can retrieve it later, and your stage doesn’t need to hold a reference to it.

While introducing queuing into your system is very useful, it’s usually one of the last techniques you want to employ when optimizing your program. Adding queuing prematurely can hide synchronization issues such as deadlocks and livelocks, and further, as your program converges toward correctness, you may find that you need more or less queuing.

To understand why, let’s take a look at a simple pipeline:

```go
done := make(chan interface{})
defer close(done)

zeros := take(done, 3, repeat(done, 0))
short := sleep(done, 1*time.Second, zeros)
long := sleep(done, 4*time.Second, short)

pipeline := long
```

This pipeline chains together four stages:

1. A repeat stage that generates an endless stream of 0s.
    
2. A stage that cancels the previous stages after seeing three items.
    
3. A “short” stage that sleeps one second.
    
4. A “long” stage that sleeps four seconds.
    

What happens if we modify the pipeline to include a buffer?

```go
done := make(chan interface{})
defer close(done)

zeros := take(done, 3, repeat(done, 0))
short := sleep(done, 1*time.Second, zeros)
buffer := buffer(done, 2, short) // Buffers sends from short by 2
long := sleep(done, 4*time.Second, short)

pipeline := long
```

```go
p := processRequest(done, acceptConnection(done, httpHandler))
```

Here the pipeline doesn’t exit until it’s canceled, and the stage that is accepting connections doesn’t stop accepting connections until the pipeline is canceled. In this scenario, you wouldn’t want connections to your program to begin timing out because your processRequest stage was blocking your acceptConnection stage.

So the answer to our question of the utility of introducing a queue isn’t that the runtime of one of the stages has been reduced, but rather that the time it’s in a blocking state is reduced. This allows the stage to continue doing its job.

In this way, the true utility of queues is to decouple stages so that the runtime of one stage has no impact on the runtime of another. Decoupling stages in this manner then cascades to alter the runtime behavior of the system as a whole, which can be either good or bad depending on your system.

We then come to the question of tuning your queuing. Where should the queues be placed? What should the buffer size be? The answers to these questions depend on the nature of your pipeline.

Let’s begin by analyzing situations in which queuing can increase the overall performance of your system. The only applicable situations are:  
• If batching requests in a stage saves time.  
• If delays in a stage produce a feedback loop into the system.

```go
func BenchmarkUnbufferedWrite(b *testing.B) {
	performWrite(b, tmpFileOrFatal())
}

func BenchmarkBufferedWrite(b *testing.B) {
	bufferredFile := bufio.NewWriter(tmpFileOrFatal())
	performWrite(b, bufio.NewWriter(bufferredFile))
}

func tmpFileOrFatal() *os.File {
	file, err := ioutil.TempFile("", "tmp")
	if err != nil {
		log.Fatal("error: %v", err)
	}
	return file
}

func performWrite(b *testing.B, writer io.Writer) {
	done := make(chan interface{})
	defer close(done)

	b.ResetTimer()
	for bt := range take(done, repeat(done, byte(0)), b.N) {
		writer.Write([]byte{bt.(byte)})
	}
}
```

As anticipated, the buffered write is faster than the unbuffered write. This is because in `bufio.Writer`, the writes are queued internally into a buffer until a sufficient chunk has been accumulated, and then the chunk is written out. This process is often called chunking, for obvious reasons.

==**Chunking is faster because ``bytes.Buffer`` must grow its allocated memory to accommodate the bytes it must store. For various reasons, growing memory is expensive; therefore, the less times we have to grow, the more efficient our system as a whole will perform. Thus, queuing has increased the performance of our system as a whole.**==

## The context Package

It would be useful if we could communicate extra information alongside the simple notification to cancel: why the cancellation was occurring, or whether or not our function has a deadline by which it needs to complete.

It turns out that the need to wrap a done channel with this information is very common in systems of any size, and so the Go authors decided to create a standard pattern for doing so.

```go
var Canceled = errors.New("context canceled")
var DeadlineExceeded error = deadlineExceededError{}

type CancelFunc
type Context

func Background() Context
func TODO() Context
func WithCancel(parent Context) (ctx Context, cancel CancelFunc)
func WithDeadline(parent Context, deadline time.Time) (Context, CancelFunc)
func WithTimeout(parent Context, timeout time.Duration) (Context, CancelFunc)
func WithValue(parent Context, key, val interface{}) Context
```

The `Context` type. This is the type that will flow through your system much like a done channel does. If you use the context package, each function that is downstream from your top-level concurrent call would take in a `Context` as its first argument. The type looks like this:

```go
type Context interface {
	// Deadline returns the time when work done on behalf of this
	// context should be canceled. Deadline returns ok==false when no
	// deadline is set. Successive calls to Deadline return the same
	// results.
	Deadline() (deadline time.Time, ok bool)

	// Done returns a channel that's closed when work done on behalf
	// of this context should be canceled. Done may return nil if this
	// context can never be canceled. Successive calls to Done return
	// the same value.
	Done() <-chan struct{}

	// Err returns a non-nil error value after Done is closed. Err
	// returns Canceled if the context was canceled or
	// DeadlineExceeded if the context's deadline passed. No other
	// values for Err are defined. After Done is closed, successive
	// calls to Err return the same value.
	Err() error

	// Value returns the value associated with this context for key,
	// or nil if no value is associated with key. Successive calls to
	// Value with the same key returns the same result.
	Value(key interface{}) interface{}
}
```

This also looks pretty simple. There’s a `Done` method which returns a channel that’s closed when our function is to be preempted. There’s also some new, but easy to understand methods: a `Deadline` function to indicate if a goroutine will be canceled after a certain time, and an `Err` method that will return non-nil if the goroutine was canceled. But the `Value` method looks a little out of place. What’s it for?

**The Go authors noticed that one of the primary uses of goroutines was programs that serviced requests. Usually in these programs, request-specific information needs to be passed along in addition to information about preemption. This is the purpose of the `Value` function.**

The context package serves two primary purposes:

- To provide an API for canceling branches of your call-graph.
    
- To provide a data-bag for transporting request-scoped data through your call-graph.
    

Cancellation in a function has three aspects:

- A goroutine’s parent may want to cancel it.
    
- A goroutine may want to cancel its children.
    
- Any blocking operations within a goroutine need to be preemptable so that it may be canceled.
    

The context package helps manage all three of these.

As we mentioned, the `Context` type will be the first argument to your function. If you look at the methods on the `Context` interface, you’ll see that there’s nothing present that can mutate the state of the underlying structure. Further, there’s nothing that allows the function accepting the `Context` to cancel it. This protects functions up the call stack from children canceling the context. Combined with the `Done` method, which provides a done channel, this allows the `Context` type to safely manage cancellation from its antecedents.

This raises a question: if a `Context` is immutable, how do we affect the behavior of cancellations in functions below a current function in the call stack?

This is where the functions in the context package become important. Let’s take a look at a few of them one more time to refresh our memory:

```go
func WithCancel(parent Context) (ctx Context, cancel CancelFunc)
func WithDeadline(parent Context, deadline time.Time) (Context, CancelFunc)
func WithTimeout(parent Context, timeout time.Duration) (Context, CancelFunc)
```

Notice that all these functions take in a `Context` and return one as well. Some of these also take in other arguments like `deadline` and `timeout`. The functions all generate new instances of a `Context` with the options relative to these functions.

- `WithCancel` returns a new `Context` that closes its done channel when the returned cancel function is called.
    
- `WithDeadline` returns a new `Context` that closes its done channel when the machine’s clock advances past the given deadline.
    
- `WithTimeout` returns a new `Context` that closes its done channel after the given timeout duration.
    

If your function needs to cancel functions below it in the call-graph in some manner, it will call one of these functions and pass in the `Context` it was given, and then pass the `Context` returned into its children. If your function doesn’t need to modify the cancellation behavior, the function simply passes on the `Context` it was given.

In this spirit, instances of a `Context` are meant to flow through your program’s call-graph. In an object-oriented paradigm, it’s common to store references to often-used data as member variables, but it’s important to not do this with instances of `context.Context`. Instances of `context.Context` may look equivalent from the outside, but internally they may change at every stack-frame.

the `Context` intended for it, and not the `Context` intended for a stack-frame _N_ levels up the stack.

At the top of your asynchronous call-graph, your code probably won’t have been passed a `Context`. To start the chain, the context package provides you with two functions to create empty instances of `Context`:

```go
func Background() Context
func TODO() Context
```

==**`Background` simply returns an empty `Context`. `TODO` is not meant for use in production, but also returns an empty `Context`; `TODO`’s intended purpose is to serve as a placeholder for when you don’t know which `Context` to utilize, or if you expect your code to be provided with a `Context`, but the upstream code hasn’t yet furnished one.**==

---

The most prevalent guidance on what’s appropriate is this somewhat ambiguous comment in the context package:

> Use context values only for request-scoped data that transits processes and API boundaries, not for passing optional parameters to functions.

It’s pretty clear what an optional parameter is (you shouldn’t be using a `Context` to fulfill your secret desire for Go to support optional parameters), but what is **request-scoped data**? Supposedly it “transits processes and API boundaries,” but that could describe lots of things.

The best way I’ve found to define it is to come up with some heuristics with your team, and evaluate them in code reviews. Here are my heuristics:

1. **The data should transit process or API boundaries.**  
    If you generate the data in your process’ memory, it’s probably not a good candidate to be request-scoped data unless you also pass it across an API boundary.
    
2. **The data should be immutable.**  
    If it’s not, then by definition what you’re storing did not come from the request.
    
3. **The data should trend toward simple types.**  
    If request-scoped data is meant to transit process and API boundaries, it’s much easier for the other side to pull this data out if it doesn’t also have to import a complex graph of packages.
    
4. **The data should be data, not types with methods.**  
    Operations are logic and belong on the things consuming this data.
    
5. **The data should help decorate operations, not drive them.**  
    If your algorithm behaves differently based on what is or isn’t included in its `Context`, you have likely crossed over into the territory of optional parameters.

# CHAPTER 5 Concurrency at Scale