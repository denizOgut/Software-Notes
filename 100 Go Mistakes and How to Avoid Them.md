
# 1 Go: Simple to learn but hard to master

## 1.1 Go outline

Nowadays, code must be readable, expressive, and maintainable to guarantee a system’s durability over the years. maximizing agility and reducing the time to market is critical for most organizations.

In response to these challenges, Google created the Go programming language.

Feature-wise, Go has no type inheritance, no exceptions, no macros, no partial functions, no support for lazy variable evaluation or immutability, no operator overloading, no pattern matching, and on and on
Why are these features missing from the language?

>_Why does Go not have feature X? Your favorite feature may be missing because it doesn’t fit, because it affects compilation speed or clarity of design, or because it would make the fundamental system model too difficult._

Go utilizes a few essential characteristics when adopting a language at scale for an organization. These include the following:

- **_Stability_**—Even though Go receives frequent updates (including improvements and security patches), it remains a stable language. Some may even consider this one of the best features of the language.
- **_Expressivity_**—We can define expressivity in a programming language by how naturally and intuitively we can write and read code. A reduced number of keywords and limited ways to solve common problems make Go an expressive language for large codebases.
- **_Compilation_**—Targeting fast compilation times has always been a conscious goal for the language designers. This, in turn, enables productivity.
- **_Safety_**—Go is a strong, statically typed language. Hence, it has strict compile-time rules, which ensure the code is type-safe in most cases.

## 1.2 Simple doesn’t mean easy

Despite Go being simple to learn, mastering concepts like concurrency can be challenging, as revealed by a study on concurrency bugs. The key takeaway is that simplicity in learning a concept doesn't necessarily translate to easiness in practical application. The reaction suggested is not to question language design but for developers to understand complexities, especially in concurrency


## 1.3 100 Go mistakes

This book presents seven main categories of mistakes. Overall, the mistakes can be classified as

- Bugs
- Needless complexity
- Weaker readability
- Suboptimal or unidiomatic organization
- Lack of API convenience
- Under-optimized code
- Lack of productivity

### 1.3.1 Bugs

//...

### 1.3.2 Needless complexity

Instead of solving concrete problems right now, it can be tempting to build evolutionary software that could tackle whatever future use case arises. However, this leads to more drawbacks than benefits in most cases because it can make a codebase more complex to understand and reason about.

### 1.3.3 Weaker readability

the ratio of time spent reading versus writing is well over 10 to 1. Most of us started to program on solo projects where readability wasn’t that important. However, today’s software engineering is programming with a time dimension

### 1.3.4 Suboptimal or unidiomatic organization

another type of mistake is organizing our code and a project suboptimally and unidiomatically. Such issues can make a project harder to reason about and maintain

### 1.3.5 Lack of API convenience

If an API isn’t user-friendly, it will be less expressive and, hence, harder to understand and more error-prone.

### 1.3.6 Under-optimized code

 It can happen for various reasons, such as not understanding language features or even a lack of fundamental knowledge. Performance is one of the most obvious impacts of this mistake, but not the only one.

### 1.3.7 Lack of productivity

Being comfortable with how a language works and exploiting it to get the best out of it is crucial to reach proficiency.

## Summary #Summary

- ==Go is a modern programming language that enables developer productivity, which is crucial for most companies today.==
- ==Go is simple to learn but not easy to master.==



# 2 Code and project organization

## 2.1 #1: Unintended variable shadowing #Mistake

The scope of a variable refers to the places a variable can be referenced: in other words, the part of an application where a name binding is valid. In Go, a variable name declared in a block can be redeclared in an inner block. This principle, called _variable shadowing_, is prone to common mistakes.

```go
var client *http.Client // Declares a client variable
if tracing {
    client, err := createClientWithTracing() // Creates an HTTP client with tracing enabled. (The client variable is shadowed in this block.)
    if err != nil {
        return err
    }
    log.Println(client)
} else {
    client, err := createDefaultClient() // Creates a default HTTP client. (The client variable is also shadowed in this block.)
    if err != nil {
        return err
    }
    log.Println(client)
}
// Use client
```

In this example, we first declare a client variable. Then, we use the short variable declaration operator (:=) in both inner blocks to assign the result of the function call to the inner client variables—not the outer one. As a result, the outer variable is always nil.

How can we ensure that a value is assigned to the original client variable? There are two different options.

The first option uses temporary variables in the inner blocks this way:

```go
var client *http.Client
if tracing {
    c, err := createClientWithTracing() // Creates a temporary variable c
    if err != nil {
        return err
    }
    client = c // Assigns this temporary variable to client
} else {
    // Same logic
}
```

Here, we assign the result to a temporary variable, c, whose scope is only within the if block. Then, we assign it back to the client variable

The second option uses the assignment operator (=) in the inner blocks to directly assign the function results to the client variable. However, this requires creating an error variable because the assignment operator works only if a variable name has already been declared.

```go
var client *http.Client
var err error // Declares an err variable
if tracing {
    client, err = createClientWithTracing() // Uses the assignment operator to assign the *http.Client returned to the client variable directly
    if err != nil {
        return err
    }
} else {
    // Same logic
}
```

Instead of assigning to a temporary variable first, we can directly assign the result to client.

Both options are perfectly valid. The main difference between the two alternatives is that we perform only one assignment in the second option, which may be considered easier to read.

Variable shadowing occurs when a variable name is redeclared in an inner block is prone to mistakes

sometimes it can be convenient to reuse an existing variable name like err for errors. Yet, in general, we should remain cautious because we now know that we can face a scenario where the code compiles, but the variable that receives the value is not the one expected.

## 2.2 #2: Unnecessary nested code #Mistake

Code is qualified as readable based on multiple criteria such as naming, consistency, formatting, and so forth. A critical aspect of readability is the number of nested levels

```go
func join(s1, s2 string, max int) (string, error) {
    if s1 == "" {
        return "", errors.New("s1 is empty")
    } else {
        if s2 == "" {
            return "", errors.New("s2 is empty")
        } else {
            concat, err := concatenate(s1, s2) // Calls a concatenate function to perform some specific concatenation but may return errors
            if err != nil {
                return "", err
            } else {
                if len(concat) > max {
                    return concat[:max], nil
                } else {
                    return concat, nil
                }
            }
        }
    }
}
 
func concatenate(s1 string, s2 string) (string, error) {
    // ...
}
```

This join function concatenates two strings and returns a substring if the length is greater than max. Meanwhile, it handles checks on s1 and s2 and whether the call to concatenate returns an error.

From an implementation perspective, this function is correct

```go
func join(s1, s2 string, max int) (string, error) {
    if s1 == "" {
        return "", errors.New("s1 is empty")
    }
    if s2 == "" {
        return "", errors.New("s2 is empty")
    }
    concat, err := concatenate(s1, s2)
    if err != nil {
        return "", err
    }
    if len(concat) > max {
        return concat[:max], nil
    }
    return concat, nil
}
 
func concatenate(s1 string, s2 string) (string, error) {
    // ...
}
```

>_Align the happy path to the left; you should quickly be able to scan down one column to see the expected execution flow._

It was difficult to distinguish the expected execution flow in the first version because of the nested if/else statements. Conversely, the second version requires scanning down one column

In general, the more nested levels a function requires, the more complex it is to read and understand.

- When an if block returns, we should omit the else block in all cases

```go
if foo() {
    // ...
    return true
} else {
    // ...
}
```

Instead, we omit the else block like this:

```go
if foo() {
    // ...
    return true
}
// ...
```


- We can also follow this logic with a non-happy path:

```go
if s != "" {
    // ...
} else {
    return errors.New("empty string")
}
```

 Here, an empty s represents the non-happy path. Hence, we should flip the condition like so:

```go
if s == "" {
    return errors.New("empty string")
}
// ...
```

Striving to reduce the number of nested blocks, aligning the happy path on the left, and returning as early as possible are concrete means to improve our code’s readability.


## 2.3 #3: Misusing init functions #Mistake 

In Java like ``Static Initializer`` or ``@PostConstruct``

The potential consequences are poor error management or a code flow that is harder to understand

### 2.3.1 Concepts

An init function is a function used to initialize the state of an application. It takes no arguments and returns no result (a func() function). When a package is initialized, all the constant and variable declarations in the package are evaluated. Then, the init functions are executed.

```go
package main
 
import "fmt"
 
var a = func() int {
    fmt.Println("var") // Executed first
    return 0
}()
 
func init() {
    fmt.Println("init") // Executed second
}
 
func main() {
    fmt.Println("main") // Executed last
}
```

output:

```
var
init
main
```

An init function is executed when a package is initialized

```go
package main
 
import (
    "fmt"
 
    "redis"
)
 
func init() {
    // ...
}
 
func main() {
    err := redis.Store("foo", "bar") // A dependency on the redis package
    // ...
}
```

And then redis.go from the redis package:

```go
package redis
 
// imports
 
func init() {
    // ...
}
 
func Store(key, value string) error {
    // ...
}
```

Because main depends on redis, the redis package’s init function is executed first, followed by the [](https://livebook.manning.com/book/100-go-mistakes-and-how-to-avoid-them/chapter-2/)init of the main package, and then the main function itself.

We can define multiple init functions per package. When we do, the execution order of the init function inside the package is based on the source files’ alphabetical order. For example, if a package contains an a.go file and a b.go file and both have an init function, the a.go init function is executed first.

![[Pasted image 20240102111826.png]]
##### Figure 2.2 The init function of the redis package is executed first, then the init function of main, and finallythe main function.

We shouldn’t rely on the ordering of init functions within a package. Indeed, it can be dangerous as source files can be renamed, potentially impacting the execution order.

We can also define multiple init functions within the same source file

```go
package main
 
import "fmt"
 
func init() { // First init function
    fmt.Println("init 1")
}
 
func init() { // Second init function
    fmt.Println("init 2")
}
 
func main() {
}
```

The first init function executed is the first one in the source order. Here’s the output:

```go
init 1
init 2
```

### 2.3.2 When to use init functions

an example where using an init function can be considered inappropriate: holding a database connection pool. In the init function in the example, we open a database using ``sql.Open``. We make this database a global variable that other functions can later use:

```go
var db *sql.DB
 
func init() {
    dataSourceName :=
        os.Getenv("MYSQL_DATA_SOURCE_NAME") // Environment variable
    d, err := sql.Open("mysql", dataSourceName)
    if err != nil {
        log.Panic(err)
    }
    err = d.Ping()
    if err != nil {
        log.Panic(err)
    }
    db = d // Assigns the DB connection to the global db variable
}
```

First, error management in an init function is limited. Indeed, as an init function doesn’t return an error, one of the only ways to signal an error is to panic, leading the application to be stopped

Another important downside is related to testing. If we add tests to this file, the init function will be executed before running the test cases
Therefore, the init function in this example complicates writing unit tests

The last downside is that the example requires assigning the database connection pool to a global variable. Global variables have some severe drawbacks; for example:

- ==Any functions can alter global variables within the package.==
- ==Unit tests can be more complicated because a function that depends on a global variable won’t be isolated anymore.==

In most cases, we should favor encapsulating a variable rather than keeping it global.

```go
func createClient(dsn string) (*sql.DB, error) { // Accepts a data source name and returns an *sql.DB and an error
    db, err := sql.Open("mysql", dsn)
    if err != nil {
        return nil, err // Returns an error
    }
    if err = db.Ping(); err != nil {
        return nil, err
    }
    return db, nil
}
```

Using this function, we tackled the main downsides discussed previously. Here’s how:

- The responsibility of error handling is left up to the caller.
- It’s possible to create an integration test to check that this function works.
- The connection pool is encapsulated within the function.

 In summary init functions can lead to some issues:

- ==They can limit error management.==
- ==They can complicate how to implement tests (for example, an external dependency must be set up, which may not be necessary for the scope of unit tests).==
- ==If the initialization requires us to set a state, that has to be done through global variables.==

## 2.4 #4: Overusing getters and setters #Mistake 

In Go, there is no automatic support for getters and setters as we see in some languages. It is also considered neither mandatory nor idiomatic to use getters and setters to access struct fields.

```go
timer := time.NewTimer(time.Second)
<-timer.C // C is a <–chan Time field
```

Although it’s not recommended, we could even modify C directly

sing getters and setters presents some advantages, including these:

- ==They encapsulate a behavior associated with getting or setting a field, allowing new functionality to be added later (for example, validating a field, returning a computed value, or wrapping the access to a field around a mutex).==
- ==They hide the internal representation, giving us more flexibility in what we expose.==
- ==They provide a debugging interception point for when the property changes at run time, making debugging easier.==

For example, if we use them with a field called balance, we should follow these naming conventions:

- The getter method should be named Balance (not GetBalance).
- The setter method should be named SetBalance.

```go
currentBalance := customer.Balance()
if currentBalance < 0 {
    customer.SetBalance(0)
}
```

In summary, we shouldn’t overwhelm our code with getters and setters on structs if they don’t bring any value. 
Go is a unique language designed for many characteristics, including simplicity. However, if we find a need for getters and setters or, as mentioned, foresee a future need while guaranteeing forward compatibility, there’s nothing wrong with using them.

## 2.5 #5: Interface pollution #Mistake

Interface pollution is about overwhelming our code with unnecessary abstractions, making it harder to understand.

### 2.5.1 Concepts

What makes Go interfaces so different is that they are satisfied implicitly. There is no explicit keyword like implements to mark that an object X implements interface Y.

The io package provides abstractions for I/O primitives. Among these abstractions, io.Reader relates to reading data from a data source and io.Writer to writing data to a target

The ``io.Reader`` contains a single ``Read`` method:

```go
type Reader interface {
    Read(p []byte) (n int, err error)
}
```

`io.Writer` defines a single method, `Write`:

```go
type Writer interface {
    Write(p []byte) (n int, err error)
}
```

both interfaces provide fundamental abstractions:

- `io.Reader` reads data from a source.
- `io.Writer` writes data to a target.

```go
func copySourceToDest(source io.Reader, dest io.Writer) error {
    // ...
}
```

This function would work with `*os.File` parameters (as `*os.File` implements both `io.Reader` and `io.Writer`) and any other type that would implement these interfaces


```go
func TestCopySourceToDest(t *testing.T) {
    const input = "foo"
    source := strings.NewReader(input) // Creates an io.Reader
    dest := bytes.NewBuffer(make([]byte, 0)) // Creates an io.Writer
 
    err := copySourceToDest(source, dest) // Calls copySourceToDest from a *strings.Reader and a *bytes.Buffer
    if err != nil {
        t.FailNow()
    }
 
    got := dest.String()
    if got != input {
        t.Errorf("expected: %s, got: %s", input, got)
    }
}
```


In the example, source is a `*strings.Reader`, whereas dest is a `*bytes.Buffer`. Here, we test the behavior of `copySourceToDest` without creating any files.

> _The bigger the interface, the weaker the abstraction._
   Rob Pike


`io.Reader` and `io.Writer` are powerful abstractions because they cannot get any simpler. Furthermore, we can also combine fine-grained interfaces to create higher-level abstractions. This is the case with `io.ReadWriter`, which combines the reader and writer behaviors:

```go
type ReadWriter interface {
    Reader
    Writer
}
```

### 2.5.2 When to use interfaces

- ==Common behavior==
- ==Decoupling==
- ==Restricting behavior==

#### Common behavior

when multiple types implement a common behavior. In such a case, we can factor out the behavior inside an interface. For example, sorting a collection can be factored out via three methods:

- Retrieving the number of elements in the collection
- Reporting whether one element must be sorted before another
- Swapping two elements

```go
type Interface interface {
    Len() int // Number of elements
    Less(i, j int) bool // Checks two elements
    Swap(i, j int) // Swaps two elements
}
```

This interface has a strong potential for reusability because it encompasses the common behavior to sort any collection that is index-based.

are we necessarily interested in the implementation type? Is it important whether the sorting algorithm is a merge sort or a quicksort? In many cases, we don’t care.

Finding the right abstraction to factor out a behavior can also bring many benefits.

```go
func IsSorted(data Interface) bool {
    n := data.Len()
    for i := n - 1; i > 0; i-- {
        if data.Less(i, i-1) {
            return false
        }
    }
    return true
}
```

#### Decoupling

If we rely on an abstraction instead of a concrete implementation, the implementation itself can be replaced with another without even having to change our code **This is the Liskov Substitution Principle (the _L_ in Robert C. Martin’s SOLID design principles).**

One benefit of decoupling can be related to unit testing.

```go
type CustomerService struct {
    store mysql.Store // Depends on the concrete implementation
}
 
func (cs CustomerService) CreateNewCustomer(id string) error {
    customer := Customer{id: id}
    return cs.store.StoreCustomer(customer)
}
```

Because `customerService` relies on the actual implementation to store a `Customer`, we are obliged to test it through integration tests

To give us more flexibility, we should decouple `CustomerService` from the actual implementation, which can be done via an interface

```go
type customerStorer interface { // Creates a storage abstraction
    StoreCustomer(Customer) error
}
 
type CustomerService struct {
    storer customerStorer // Decouples CustomerService from the actual implementation
}
 
func (cs CustomerService) CreateNewCustomer(id string) error {
    customer := Customer{id: id}
    return cs.storer.StoreCustomer(customer)
}
```

Because storing a customer is now done via an interface, this gives us more flexibility in how we want to test the method, we can

- Use the concrete implementation via integration tests
- Use a mock (or any kind of test double) via unit tests
- Or both

#### Restricting behavior

Let’s imagine we implement a custom configuration package to deal with dynamic configuration.

```go
type IntConfig struct {
    // ...
}
 
func (c *IntConfig) Get() int {
    // Retrieve configuration
}
 
func (c *IntConfig) Set(value int) {
    // Update configuration
}
```

suppose we receive an `IntConfig` that holds some specific configuration, such as a threshold. Yet, in our code, we are only interested in retrieving the configuration value, and we want to prevent updating it. How can we enforce that, semantically, this configuration is read-only, if we don’t want to change our configuration package? By creating an abstraction that restricts the behavior to retrieving only a config value:

```go
type intConfigGetter interface {
    Get() int
}
```

Then, in our code, we can rely on `intConfigGetter` instead of the concrete implementation:

```go
type Foo struct {
    threshold intConfigGetter
}
 
func NewFoo(threshold intConfigGetter) Foo { // Injects the configuration getter
    return Foo{threshold: threshold}
}
 
func (f Foo) Bar()  {
    threshold := f.threshold.Get() // Reads the configuration
    // ...
}
```

### 2.5.3 Interface pollution

interfaces are made to create abstractions. And the main caveat when programming meets abstractions is remembering that 

>abstractions _should be discovered, not created_.

 It means we shouldn’t start creating abstractions in our code if there is no immediate reason to do so. We shouldn’t design with interfaces but wait for a concrete need. Said differently, we should create an interface when we need it, not when we foresee that we could need it.

In summary, we should be cautious when creating abstractions in our code—abstractions should be discovered, not created.

>Don’t design with interfaces, discover them.
   Rob Pike

Let’s not try to solve a problem abstractly but solve what has to be solved now. Last, but not least, if it’s unclear how an interface makes the code better, we should probably consider removing it to make our code simpler.

## 2.6 #6: Interface on the producer side #Mistake 

where should an interface live?

- _Producer side_—An interface defined in the same package as the concrete implementation

![[Pasted image 20240102122242.png]]

* _Consumer side_—An interface defined in an external package where it’s used

![[Pasted image 20240102122336.png]]

It’s common to see developers creating interfaces on the producer side, alongside the concrete implementation. This design is perhaps a habit from developers having a C# or a Java background. But in Go, in most cases this is not what we should do.

```go
package store
 
type CustomerStorage interface {
    StoreCustomer(customer Customer) error
    GetCustomer(id string) (Customer, error)
    UpdateCustomer(customer Customer) error
    GetAllCustomers() ([]Customer, error)
    GetCustomersWithoutContract() ([]Customer, error)
    GetCustomersWithNegativeBalance() ([]Customer, error)
}
```

have some excellent reasons to create and expose this interface on the producer side.
Whatever the reason, this isn’t a best practice in Go.

In most cases, the approach to follow is similar to what we described in the previous section: _abstractions should be discovered, not created_. This means that it’s not up to the producer to force a given abstraction for all the clients. Instead, it’s up to the client to decide whether it needs some form of abstraction and then determine the best abstraction level for its needs.

perhaps one client won’t be interested in decoupling its code. Maybe another client wants to decouple its code but is only interested in the `GetAllCustomers` method. In this case, this client can create an interface with a single method, referencing the `Customer` struct from the external package:

```go
package client
 
type customersGetter interface {
    GetAllCustomers() ([]store.Customer, error)
}
```

- Because the `customersGetter` interface is only used in the client package, it can remain unexported.


==The main point is that the client package can now define the most accurate abstraction for its need. It relates to the concept of the Interface-Segregation Principle (the _I_ in SOLID), which states that no client should be forced to depend on methods it doesn’t use==

don’t create an abstraction if you think it might be helpful in an imaginary future or, at least, if you can’t prove this abstraction is valid.

## 2.7 #7: Returning interfaces #Mistake 

While designing a function signature, we may have to return either an interface or a concrete implementation. returning an interface is, in many cases, considered a bad practice in Go.

returning an interface restricts flexibility because we force all the clients to use one particular type of abstraction. 

> _Be conservative in what you do, be liberal in what you accept from others._
—Transmission Control Protocol


If we apply this idiom to Go, it means

- Returning structs instead of interfaces
- Accepting interfaces if possible

All in all, in most cases, we shouldn’t return interfaces but concrete implementations. Otherwise, it can make our design more complex due to package dependencies and can restrict flexibility because all the clients would have to rely on the same abstraction.

## 2.8 #8: any says nothing #Mistake 

In Go, an interface type that specifies zero methods is known as the empty interface, `interface{}`. With Go 1.18, the predeclared type any became an alias for an empty interface; hence, all the `interface{}` occurrences can be replaced by any

An any type can hold `any` value type:

```GO
func main() {
    var i any
 
    i = 42 // int
    i = "foo" // String
    i = struct { // struct
        s string
    }{
        s: "bar",
    }
    i = f // function
 
    _ = i // Assignment to the blank identifier so that the example compiles
}
 
func f() {}
```

In assigning a value to an `any` type, we lose all type information, which requires a type assertion to get anything useful out of the `i` variable, as in the previous example.

```go
package store
 
type Customer struct{
    // Some fields
}
type Contract struct{
    // Some fields
}
 
type Store struct{}
 
func (s *Store) Get(id string) (any, error) { // Returns any
    // ...
}
 
func (s *Store) Set(id string, v any) error { // Accepts any
    // ...
}
```

Although there is nothing wrong with `Store` compilation-wise think about the method signatures. Because we accept and return `any` arguments, the methods lack expressiveness.

Hence, accepting or returning an any type doesn’t convey meaningful information. Also, because there is no safeguard at compile time, nothing prevents a caller from calling these methods with whatever data type, such as an `int`:

```go
s := store.Store{}
s.Set("foo", 42)
```

By using `any`, we lose some of the benefits of Go as a statically typed language. Instead, we should avoid `any` types and make our signatures explicit as much as possible

```go
func (s *Store) GetContract(id string) (Contract, error) {
    // ...
}
 
func (s *Store) SetContract(id string, contract Contract) error {
    // ...
}
 
func (s *Store) GetCustomer(id string) (Customer, error) {
    // ...
}
 
func (s *Store) SetCustomer(id string, customer Customer) error {
    // ...
}
```

the methods are expressive, reducing the risk of incomprehension. Having more methods isn’t necessarily a problem because clients can also create their own abstraction using an interface. For example, if a client is interested only in the Contract methods, it could write something like this:

```go
type ContractStorer interface {
    GetContract(id string) (store.Contract, error)
    SetContract(id string, contract store.Contract) error
}
```

In summary, `any` can be helpful if there is a genuine need for accepting or returning any possible type (for instance, when it comes to marshaling or formatting). In general, we should avoid overgeneralizing the code we write at all costs. Perhaps a little bit of duplicated code might occasionally be better if it improves other aspects such as code expressiveness.

## 2.9 #9: Being confused about when to use generics #Mistake 

this allows writing code with types that can be specified later and instantiated when needed

### 2.9.1 Concepts

```go
func getKeys(m map[string]int) []string {
    var keys []string
    for k := range m {
        keys = append(keys, k)
    }
    return keys
}
```

Before generics, Go developers had a few options: using code generation, reflection, or duplicating code. For example, we could write two functions, one for each map type, or even try to extend `getKeys` to accept different map types:

```go
func getKeys(m any) ([]any, error) { // Accepts and returns any arguments
    switch t := m.(type) {
    default:
        return nil, fmt.Errorf("unknown type: %T", t) // Handles run-time errors if a type isn’t implemented yet
    case map[string]int:
        var keys []any
        for k := range t {
            keys = append(keys, k)
        }
        return keys, nil
    case map[int]string:
        // Copy the extraction logic
    }
}
```

First, it increases boilerplate code the function now accepts an any type, which means we lose some of the benefits of Go as a typed language. Indeed, checking whether a type is supported is done at run time instead of compile time. Hence, we also need to return an error if the provided type is unknown. Finally, because the key type can be either int or string, we are obliged to return a slice of any type to factor out key types. This approach increases the effort on the caller side because the client may also need to perform a type check of the keys or an extra conversion. Thanks to generics, we can now refactor this code using type parameters.

Type parameters are generic types that we can use with functions and types.

```go
func foo[T any](t T) { // T is a type parameter.
    // ...
}
```

Supplying a type argument is called _instantiation_, and the work is done at compile time. This keeps type safety as part of the core language features and avoids run-time overhead.

```go
func getKeys[K comparable, V any](m map[K]V) []K { // The keys are comparable, whereas values are of the any type.
    var keys []K // Creats the keys slice
    for k := range m {
        keys = append(keys, k)
    }
    return keys
}
```

To handle the map, we define two kinds of type parameters. First, the values can be of the any type: V any

This code leads to a compilation error:` invalid map key type []byte`. Therefore, instead of accepting any key type, we are obliged to restrict type arguments so that the key type meets specific requirements. Here, the requirement is that the key type must be comparable (we can use == or !=). Hence, we defined K as comparable instead of any.

Restricting type arguments to match specific requirements is called a _constraint_. A constraint is an interface type that can contain

- A set of behaviors (methods)
- Arbitrary types

```go
type customConstraint interface {
    ~int | ~string // Defines a custom type that restricts types to int and string
}
 
func getKeys[K customConstraint, // Changes the type parameter K to be a customConstraint type
         V any](m map[K]V) []K {
    // Same implementation
}
```

First, we define a `customConstraint` interface to restrict the types to be either `int` or `string` using the union operator` |` . K is now a `customConstraint` instead of a comparable as before.
the key type has to be an `int` or a `string`

Go can infer that `getKeys` is called with a `string` type argument. The previous call is equivalent to this:

```go
keys := getKeys[string](m)
```

> `~INT` VS. `INT`
>Using int restricts it to that type, whereas ~int restricts all the types whose underlying type is an int

we can also use generics with data structures

```go
type Node[T any] struct { // Uses a type parameter
    Val  T
    next *Node[T]
}
 
func (n *Node[T]) Add(next *Node[T]) { // Instantiates a type receiver
    n.next = next
}
```


==One last thing to note about type parameters is that they can’t be used with method arguments, only with function arguments or method receivers.==

```go
type Foo struct {}
 
func (Foo) bar[T any](t T) {}
./main.go:29:15: methods cannot have type parameters
```

### 2.9.2 Common uses and misuses

==When are generics useful?==

- ==_Data structures_==
- ==_Functions working with slices, maps, and channels of any type_==

```GO
func merge[T any](ch1, ch2 <-chan T) <-chan T {
    // ...
}
```

- ==_Factoring out behaviors instead of types_==

```go
type Interface interface {
    Len() int
    Less(i, j int) bool
    Swap(i, j int)
}
```


==Conversely, when is it recommended that we **NOT** use generics?==

- ==_When calling a method of the type argument_==
- ==_When it makes our code more complex_==

generics introduce a form of abstraction, and we have to remember that unnecessary abstractions introduce complexity.

## 2.10 #10: Not being aware of the possible problems with type embedding #Mistake 

When creating a struct, Go offers the option to embed types. But this can sometimes lead to unexpected behaviors if we don’t understand all the implications of type embedding.

In Go, a struct field is called _embedded_ if it’s declared without a name. For example

```go
type Foo struct {
    Bar // Embedded field
}
 
type Bar struct {
    Baz int
}
```

We use embedding to _promote_ the fields and methods of an embedded type. Because Bar contains a Baz field, this field is promoted to Foo Therefore, Baz becomes available from Foo:

```go
foo := Foo{}
foo.Baz = 42
```

> **INTERFACES AND EMBEDDING**
>Embedding is also used within interfaces to compose an interface with others. In the following example, `io.ReadWriter` is composed of an `io.Reader` and an `io.Writer`:


```go
type ReadWriter interface {
    Reader
    Writer
}
```

In the following, we implement a struct that holds some in-memory data, and we want to protect it against concurrent accesses using a mutex:

```go
type InMem struct {
    sync.Mutex // Embedded field
    m map[string]int
}
 
func New() *InMem {
    return &InMem{m: make(map[string]int)}
}
```

We decided to make the map unexported so that clients can’t interact with it directly but only via exported methods. Meanwhile, the mutex field is embedded. Therefore, we can implement a `Get` method this way:

```go
func (i *InMem) Get(key string) (int, bool) {
    i.Lock() // Accesses the Lock method directly
    v, contains := i.m[key]
    i.Unlock() // The same goes for the Unlock method.
    return v, contains
}
```


Because the mutex is embedded, we can directly access the Lock and Unlock methods from the i receiver.

Since `sync.Mutex` is an embedded type, the Lock and Unlock methods will be promoted. Therefore, both methods become visible to external clients using `InMem`:

```go
m := inmem.New()
m.Lock() // ??
```

This promotion is probably not desired. A mutex is, in most cases, something that we want to encapsulate within a struct and make invisible to external clients. Therefore, we shouldn’t make it an embedded field in this case:

```go
type InMem struct {
    mu sync.Mutex // Specifies that the sync.Mutex field is not embedded
    m map[string]int
}
```

Because the mutex isn’t embedded and is unexported, it can’t be accessed from external clients

```go
type Logger struct {
    writeCloser io.WriteCloser
}
 
func (l Logger) Write(p []byte) (int, error) { // Forwards the call to writeCloser
    return l.writeCloser.Write(p)
}
 
func (l Logger) Close() error { // Forwards the call to writeCloser
    return l.writeCloser.Close()
}
func main() {
    l := Logger{writeCloser: os.Stdout}
    _, _ = l.Write([]byte("foo"))
    _ = l.Close()
}
```

Logger would have to provide both a Write and a Close method that would _only_ forward the call to io.`WriteCloser`. However, if the field now becomes embedded, we can remove these forwarding methods:

```go
type Logger struct {
    io.WriteCloser // Makes io.Writer embedded
}
 
func main() {
    l := Logger{WriteCloser: os.Stdout}
    _, _ = l.Write([]byte("foo"))
    _ = l.Close()
}
```

It remains the same for clients with two exported Write and Close methods. But the example prevents implementing these additional methods simply to forward a call. Also, as Write and Close are promoted, it means that Logger satisfies the io.`WriteCloser` interface.

##### EMBEDDING VS. OOP SUBCLASSING

The main difference is related to the identity of the receiver of a method.

![[Pasted image 20240102133012.png]]

##### With embedding, the embedded type remains the receiver of a method. Conversely, with subclassing, the subclass becomes the receiver of a method.

What should we conclude about type embedding?  it’s rarely a necessity, and it means that whatever the use case, we can probably solve it as well without type embedding. Type embedding is mainly used for convenience: in most cases, to promote behaviors.

If we decide to use type embedding, we need to keep two main constraints in mind:

- ==It shouldn’t be used solely as some syntactic sugar to simplify accessing a field (such as `Foo.Baz()` instead of `Foo.Bar.Baz())`. If this is the only rationale, let’s not embed the inner type and use a field instead.==
- ==It shouldn’t promote data (fields) or a behavior (methods) we want to hide from the outside: for example, if it allows clients to access a locking behavior that should remain private to the struct.==

Using type embedding consciously by keeping these constraints in mind can help avoid boilerplate code with additional forwarding methods.

## 2.11 #11: Not using the functional options pattern #Mistake 

When designing an API, one question may arise: how do we deal with optional configurations?

For this example, let’s say we have to design a library that exposes a function to create an HTTP server. This function would accept different inputs: an address and a port. The following shows the skeleton of the function:

```go
func NewServer(addr string, port int) (*http.Server, error) {
    // ...
}
```

adding new function parameters breaks the compatibility, forcing the clients to modify the way they call `NewServer`. In the meantime, we would like to enrich the logic related to port management this way

- If the port isn’t set, it uses the default one.
- If the port is negative, it returns an error.
- If the port is equal to 0, it uses a random port.
- Otherwise, it uses the port provided by the client.

### 2.11.1 Config struct

Because Go doesn’t support optional parameters in function signatures, the first possible approach is to use a configuration struct to convey what’s mandatory and what’s optional.  The mandatory parameters could live as function parameters, whereas the optional parameters could be handled in the `Config` struct:

```go
type Config struct {
    Port        int
}
 
func NewServer(addr string, cfg Config) {
}
```

This solution fixes the compatibility issue.  However, this approach doesn’t solve our requirement related to port management. Indeed, we should bear in mind that ==if a struct field isn’t provided, it’s initialized to its zero value:==

- ==0 for an integer==
- ==0.0 for a floating-point type==
- =="" for a string==
- ==Nil for slices, maps, channels, pointers, interfaces, and functions==

```go
c1 := httplib.Config{
    Port: 0, // Initializes Port to 0
}
c2 := httplib.Config{
	// Port is missing, so it’s initialized to 0.
}
```

need to find a way to distinguish between a port purposely set to 0 and a missing port. Perhaps one option might be to handle all the parameters of the configuration struct as pointers in this way:

```go
type Config struct {
    Port        *int
}
```

Using an integer pointer, semantically, we can highlight the difference between the value 0 and a missing value (a nil pointer). but it has a couple of downsides. First, it’s not handy for clients to provide an integer pointer. Clients have to create a variable and then pass a pointer this way

```go
port := 0
config := httplib.Config{
    Port: &port, // Provides an integer pointer
}
```

the more options we add, the more complex the code becomes.

The second downside is that a client using our library with the default configuration will need to pass an empty struct this way:

```go
httplib.NewServer("localhost", httplib.Config{})
```

Another option is to use the classic builder pattern

### 2.11.2 Builder pattern

The construction of Config is separated from the struct itself. It requires an extra struct, `ConfigBuilder`, which receives methods to configure and build a `Config`.

```go
type Config struct { // Config struct
    Port int
}
 
type ConfigBuilder struct { // Config builder struct, containing an optional port
    port *int
}
 
func (b *ConfigBuilder) Port(
    port int) *ConfigBuilder { // Public method to set up the port
    b.port = &port
    return b
}
 
func (b *ConfigBuilder) Build() (Config, error) { // Build method to create the config struct
    cfg := Config{}
 
    if b.port == nil {
        cfg.Port = defaultHTTPPort
    } else {
        if *b.port == 0 { // Main logic related to port management
            cfg.Port = randomPort()
        } else if *b.port < 0 {
            return Config{}, errors.New("port should be positive")
        } else {
            cfg.Port = *b.port
        }
    }
 
    return cfg, nil
}
 
func NewServer(addr string, config Config) (*http.Server, error) {
    // ...
}
```

The `ConfigBuilder` struct holds the client configuration. It exposes a Port method to set up the port

Then, a client would use our builder-based API in the following manner

```go
builder := httplib.ConfigBuilder{} // Creates a builder config
builder.Port(8080) // Sets the port
cfg, err := builder.Build() // Builds the config struct
if err != nil {
    return err
}
 
server, err := httplib.NewServer("localhost", cfg) // Passes the config struct
if err != nil {
    return err
}
```

This approach makes port management handier. However, we still need to pass a config struct that can be empty if a client wants to use the default configuration:

```go
server, err := httplib.NewServer("localhost", nil)
```

Another downside, in some situations, is related to error management
builder methods such as Port can raise exceptions if the input is invalid. If we want to keep the ability to chain the calls, the function can’t return an error. Therefore, we have to delay the validation in the Build method.

### 2.11.3 Functional options pattern

the main idea is as follows:

- An unexported struct holds the configuration: options.
- Each option is a function that returns the same type: type `Option func(options *options) error`. For example, `WithPort` accepts an int argument that represents the port and returns an Option type that represents how to update the options struct.

```go
type options struct { // Configuration struct
    port *int
}
 
type Option func(options *options) error // Represents a function type that updates the configuration struct
 
func WithPort(port int) Option { // A configuration function that updates the port
    return func(options *options) error {
        if port < 0 {
            return errors.New("port should be positive")
        }
        options.port = &port
        return nil
    }
}
```

`WithPort` returns a closure. A _closure_ is an anonymous function that references variables from outside its body; in this case, the port variable. The closure respects the Option type and implements the port-validation logic. Each config field requires creating a public function containing similar logic: validating inputs if needed and updating the config struct.

```go
func NewServer(addr string, opts ...Option) ( // Accepts variadic Option arguments
    *http.Server, error) {
    var options options // Creates an empty options struct
    for _, opt := range opts { // Iterates over all the input options
        err := opt(&options) // Calls each option, which results in modifying the common options struct
        if err != nil {
            return nil, err
        }
    }
 
    // At this stage, the options struct is built and contains the config
    // Therefore, we can implement our logic related to port configuration
    var port int
    if options.port == nil {
        port = defaultHTTPPort
    } else {
        if *options.port == 0 {
            port = randomPort()
        } else {
            port = *options.port
        }
    }
 
    // ...
}
```

This pattern is the functional options pattern. Although the builder pattern can be a valid option, it has some minor downsides that tend to make the functional options pattern the idiomatic way to deal with this problem in Go.

## 2.12 #12: Project misorganization #Mistake 

### 2.12.1 Project structure

The Go language maintainer has no strong convention about structuring a project in Go. However, one layout has emerged over the years: project-layout ([https://github.com/golang-standards/project-layout](https://github.com/golang-standards/project-layout)).

- **_/cmd_**—The main source files. The main.go of a foo application should live in /cmd/foo/main.go.
- **_/internal_**—Private code that we don’t want others importing for their applications or libraries.
- **_/pkg_**—Public code that we want to expose to others.
- **_/test_**—Additional external tests and test data. Unit tests in Go live in the same package as the source files. However, public API tests or integration tests, for example, should live in /test.
- **_/configs_**—Configuration files.
- _**/docs**_—Design and user documents.
- **_/example**s_—Examples for our application and/or a public library.
- _**/api**_—API contract files (Swagger, Protocol Buffers, etc.).
- **_/web_**—Web application-specific assets (static files, etc.).
- **/build**_—Packaging and continuous integration (CI) files.
- _**/scripts**_—Scripts for analysis, installation, and so on.
- **_/vendor_**—Application dependencies (for example, Go modules dependencies).

There’s no /src directory like in some other languages. The rationale is that /src is too generic; hence, this layout favors directories such as /cmd, /internal, or /pkg.

### 2.12.2 Package organization

In Go, there is no concept of subpackages. However, we can decide to organize packages within subdirectories.

```
/net
    /http
        client.go
        ...
    /smtp
        auth.go
        ...
    addrselect.go
    ...
```

The main benefit of subdirectories is to keep packages in a place where they live with high cohesion.

Regarding the overall organization, there are different schools of thought. For example, should we organize our application by context or by layer?

or we may favor following hexagonal architecture principles and group per technical layer.
Regarding packages, there are multiple best practices that we should follow. First, we should avoid premature packaging because it might cause us to overcomplicate a project.

Granularity is another essential thing to consider. We should avoid having dozens of nano packages containing only one or two files. If we do, it’s because we have probably missed some logical connections across these packages Conversely, we should also avoid huge packages that dilute the meaning of a package name

Package naming should also be considered with care. To help clients understand a Go project, we should name our packages after what they provide, not what they contain. Also, naming should be meaningful. Therefore, a package name should be short, concise, expressive, and, by convention, a single lowercase word.

Regarding what to export, the rule is pretty straightforward. We should minimize what should be exported as much as possible to reduce the coupling between packages and keep unnecessary exported elements hidden.

consistency is also vital to ease maintainability. Therefore, let’s make sure that we keep things as consistent as possible within a codebase.

## 2.13 #13: Creating utility packages #Mistake 

```go
package util
 
func NewStringSet(...string) map[string]struct{} {
    // ...
}
 
func SortStringSet(map[string]struct{}) []string {
    // ...
}
```

A client will use this package like this:

```go
set := util.NewStringSet("c", "a", "b")
fmt.Println(util.SortStringSet(set))
```

The problem here is that util is meaningless. We could call it common, shared, or base, but it remains a meaningless name that doesn’t provide any insight about what the package provides.

Instead of a utility package, we should create an expressive package name such as `stringset`.

```go
package stringset
 
func New(...string) map[string]struct{} { ... }
func Sort(map[string]struct{}) []string { ... }
```

In this example, we removed the suffixes for `NewStringSet` and `SortStringSet`, which respectively became New and Sort. On the client side, it now looks like this:

```go
set := stringset.New("c", "a", "b")
fmt.Println(stringset.Sort(set))
```

> *how creating dozens of nano packages in an application can make the code path more complex to follow. However, the idea itself of a nano package isn’t necessarily bad. If a small code group has high cohesion and doesn’t really belong somewhere else, it’s perfectly acceptable to organize it into a specific package.*


With this small refactoring, we get rid of a meaningless package name to expose an expressive API.

Naming a package is a critical piece of application design, and we should be cautious about this as well. As a rule of thumb, creating shared packages without meaningful names isn’t a good idea; this includes utility packages such as utils, common, or base.

naming a package after what it provides and not what it contains can be an efficient way to increase its expressiveness.

## 2.14 #14: Ignoring package name collisions #Mistake 

Package collisions occur when a variable name collides with an existing package name, preventing the package from being reused.

```GO
package redis
 
type Client struct { ... }
 
func NewClient() *Client { ... }
 
func (c *Client) Get(key string) (string, error) { ... }
```

```go
redis := redis.NewClient() // Calls NewClient from the redis package
v, err := redis.Get("foo") // Uses the redis variable
```

Here, the `redis` variable name collides with the `redis` package name. Even though this is allowed, it should be avoided. Indeed, throughout the scope of the `redis` variable, the `redis` package won’t be accessible.

What are the options to avoid such a collision? The first option is to use a different variable name.

```go
redisClient := redis.NewClient()
v, err := redisClient.Get("foo")
```

he most straightforward approach. However, if for some reason we prefer to keep our variable named redis, we can play with package imports. Using package imports, we can use an alias to change the qualifier to reference the `redis` package

```go
import redisapi "mylib/redis" // Creates an alias for the redis package
 
// ...
 
redis := redisapi.NewClient() // Accesses the redis package via the redisapi alias
v, err := redis.Get("foo")
```

## 2.15 #15: Missing code documentation #Mistake 

First, every exported element must be documented. Whether it is a structure, an interface, a function, or something else, if it’s exported, it must be documented. The convention is to add comments, starting with the name of the exported element.

```go
// Customer is a customer representation.
type Customer struct{}
 
// ID returns the customer identifier.
func (c Customer) ID() string { return "" }
```

when we document a function (or a method), we should highlight what the function intends to do, not how it does it; this belongs to the core of a function and comments, not documentation.

##### DEPRECATED ELEMENTS

It’s possible to deprecate an exported element using the // Deprecated: comment this way:

```go
// ComputePath returns the fastest path between two points.
// Deprecated: This function uses a deprecated way to compute
// the fastest path. Use ComputeFastestPath instead.
func ComputePath() {}
```

When it comes to documenting a variable or a constant, we might be interested in conveying two aspects: its purpose and its content. The former should live as code documentation to be useful for external clients. The latter, though, shouldn’t necessarily be public.

```go
// DefaultPermission is the default permission used by the store engine.
const DefaultPermission = 0o644 // Need read and write accesses.
```

To help clients and maintainers understand a package’s scope, we should also document each package. The convention is to start the comment with // Package followed by the package name:

```go
// Package math provides basic constants and mathematical functions.
//
// This package does not guarantee bit-identical results
// across architectures.
package math
```

In summary, we should keep in mind that every exported element needs to be documented. Documenting our code shouldn’t be a constraint.

## 2.16 #16: Not using linters #Mistake 

```go
package main
 
import "fmt"
 
func main() {
    i := 0
    if true {
        i := 1 // Shadowed variable
        fmt.Println(i)
    }
    fmt.Println(i)
}
```

look at golangci-lint ([https://github.com/golangci/golangci-lint](https://github.com/golangci/golangci-lint)). It’s a linting tool that provides a facade on top of many useful linters and formatters. Also, it allows running the linters in parallel to improve analysis speed, which is quite handy.


## Summary #Summary 

- ==Avoiding shadowed variables can help prevent mistakes like referencing the wrong variable or confusing readers.==
- ==Avoiding nested levels and keeping the happy path aligned on the left makes building a mental code model easier.==
- ==When initializing variables, remember that init functions have limited error handling and make state handling and testing more complex. In most cases, initializations should be handled as specific functions.==
- ==Forcing the use of getters and setters isn’t idiomatic in Go. Being pragmatic and finding the right balance between efficiency and blindly following certain idioms should be the way to go.==
- ==Abstractions should be discovered, not created. To prevent unnecessary complexity, create an interface when you need it and not when you foresee needing it, or if you can at least prove the abstraction to be a valid one.==
- ==Keeping interfaces on the client side avoids unnecessary abstractions.==
- ==To prevent being restricted in terms of flexibility, a function shouldn’t return interfaces but concrete implementations in most cases. Conversely, a function should accept interfaces whenever possible.==
- ==Only use any if you need to accept or return any possible type, such as json. Marshal. Otherwise, any doesn’t provide meaningful information and can lead to compile-time issues by allowing a caller to call methods with any data type.==
- ==Relying on generics and type parameters can prevent writing boilerplate code to factor out elements or behaviors. However, do not use type parameters prematurely, but only when you see a concrete need for them. Otherwise, they introduce unnecessary abstractions and complexity.==
- ==Using type embedding can also help avoid boilerplate code; however, ensure that doing so doesn’t lead to visibility issues where some fields should have remained hidden.==
- ==To handle options conveniently and in an API-friendly manner, use the functional options pattern.==
- ==Following a layout such as project-layout can be a good way to start structuring Go projects, especially if you are looking for existing conventions to standardize a new project.==
- ==Naming is a critical piece of application design. Creating packages such as common, util, and shared doesn’t bring much value for the reader. Refactor such packages into meaningful and specific package names.==
- ==To avoid naming collisions between variables and packages, leading to confusion or perhaps even bugs, use unique names for each one. If this isn’t feasible, use an import alias to change the qualifier to differentiate the package name from the variable name, or think of a better name.==
- ==To help clients and maintainers understand your code’s purpose, document exported elements.==
- ==To improve code quality and consistency, use linters and formatters.==


# 3 Data types

## 3.1 #17: Creating confusion with octal literals #Mistake 

```go
sum := 100 + 010
fmt.Println(sum)
```

In Go, an integer literal starting with 0 is considered an octal integer (base 8), so 10 in base 8 equals 8 in base 10. Thus, the sum in the previous example is equal to 100 + 8 = 108. This is an important property of integer literals to keep in mind

Octal integers are useful in different scenarios. For instance, suppose we want to open a file using `os.OpenFile`. This function requires passing a permission as a uint32. If we want to match a Linux permission, we can pass an octal number for readability instead of a base 10 number:

```go
file, err := os.OpenFile("foo", os.O_RDONLY, 0644)
```

It’s also possible to add an o character (the letter _o_ in lowercase) following the zero:

```go
file, err := os.OpenFile("foo", os.O_RDONLY, 0o644)
```

Using 0o as a prefix instead of only 0 means the same thing. However, it can help make the code clearer.

note the other integer literal representations:

- **_Binary_**—Uses a 0b or 0B prefix (for example, 0b100 is equal to 4 in base 10)
- **_Hexadecimal_**—Uses an 0x or 0X prefix (for example, 0xF is equal to 15 in base 10)
- **_Imaginary_**—Uses an i suffix (for example, 3i)


Finally, we can also use an underscore character (_) as a separator for readability 1_000_000_000

In summary, Go handles binary, hexadecimal, imaginary, and octal numbers. Octal numbers start with a 0. However, to improve readability and avoid potential mistakes for future code readers, make octal numbers explicit using a 0o prefix.

## 3.2 #18: Neglecting integer overflows #Mistake 

### 3.2.1 Concepts

Go provides a total of 10 integer types. There are four signed integer types and four unsigned integer types

| **[](https://livebook.manning.com/book/100-go-mistakes-and-how-to-avoid-them/chapter-3/)Signed integers** | **[](https://livebook.manning.com/book/100-go-mistakes-and-how-to-avoid-them/chapter-3/)Unsigned integers** |
| ---- | ---- |
| [](https://livebook.manning.com/book/100-go-mistakes-and-how-to-avoid-them/chapter-3/)int8 (8 bits) | [](https://livebook.manning.com/book/100-go-mistakes-and-how-to-avoid-them/chapter-3/)uint8 (8 bits) |
| [](https://livebook.manning.com/book/100-go-mistakes-and-how-to-avoid-them/chapter-3/)int16 (16 bits) | [](https://livebook.manning.com/book/100-go-mistakes-and-how-to-avoid-them/chapter-3/)uint16 (16 bits) |
| [](https://livebook.manning.com/book/100-go-mistakes-and-how-to-avoid-them/chapter-3/)int32 (32 bits) | [](https://livebook.manning.com/book/100-go-mistakes-and-how-to-avoid-them/chapter-3/)uint32 (32 bits) |
| [](https://livebook.manning.com/book/100-go-mistakes-and-how-to-avoid-them/chapter-3/)int64 (64 bits) | [](https://livebook.manning.com/book/100-go-mistakes-and-how-to-avoid-them/chapter-3/)uint64 (64 bits) |

Suppose we want to initialize an int32 to its maximum value and then increment it. What should be the behavior of this code?

```go
var counter int32 = math.MaxInt32
counter++
fmt.Printf("counter=%d\n", counter)
```

This code compiles and doesn’t panic at run time. However, the counter++ statement generates an integer overflow:

```go
counter=-2147483648
```

**==An integer overflow occurs when an arithmetic operation creates a value outside the range that can be represented with a given number of bytes.==**

In Go, an integer overflow that can be detected at compile time generates a compilation error.

```go
var counter int32 = math.MaxInt32 + 1
constant 2147483648 overflows int32
```

However, at run time, an integer overflow or underflow is silent; this does not lead to an application panic. It is essential to keep this behavior in mind, because it can lead to sneaky bugs

in some cases, like memory-constrained projects using smaller integer types, dealing with large numbers, or doing conversions, we may want to check possible overflows.

### 3.2.2 Detecting integer overflow when incrementing

If we want to detect an integer overflow during an increment operation with a type based on a defined size (int8, int16, int32, int64, uint8, uint16, uint32, or uint64), we can check the value against the math constants. For example, with an int32:

```go
func Inc32(counter int32) int32 {
    if counter == math.MaxInt32 { // Compares with math.MaxInt32
        panic("int32 overflow")
    }
    return counter + 1
}
```

What about int and uint types? `math.MaxInt`, `math.MinInt`, and `math.MaxUint` are part of the math package
The logic is the same for a uint. We can use `math.MaxUint`:

```go
func IncUint(counter uint) uint {
    if counter == math.MaxUint {
        panic("uint overflow")
    }
    return counter + 1
}
```


### 3.2.3 Detecting integer overflows during addition

```go
func AddInt(a, b int) int {
    if a > math.MaxInt-b { // Checks if an integer overflow will occur
        panic("int overflow")
    }
 
    return a + b
}
```

If a is greater than `math.MaxInt` - b, the operation will lead to an integer overflow.

### 3.2.4 Detecting an integer overflow during multiplication

We have to perform checks against the minimal integer, `math.MinInt`:

```go
func MultiplyInt(a, b int) int {
    if a == 0 || b == 0 { // If one of the operands is equal to 0, it directly returns 0.
        return 0
    }
 
    result := a * b
    if a == 1 || b == 1 { // Checks if one of the operands is equal to 1
        return result
    }
    if a == math.MinInt || b == math.MinInt { // Checks if one of the operands is equal to math.MinInt
        panic("integer overflow")
    }
    if result/b != a { // Checks if the multiplication leads to an integer overflow
        panic("integer overflow")
    }
    return result
}
```


In summary, integer overflows (and underflows) are silent operations in Go
Also remember that Go provides a package to deal with large numbers: `math/big`. This might be an option if an int isn’t enough.

## 3.3 #19: Not understanding floating points #Mistake 

The concept of a floating point was invented to solve the major problem with integers: their inability to represent fractional values. To avoid bad surprises, we need to know that floating-point arithmetic is an approximation of real arithmetic

```go
var n float32 = 1.0001
fmt.Println(n * n)
```

may expect this code to print the result of 1.0001 * 1.0001 = 1.00020001
However, running it on most x86 processors prints 1.0002, instead.

Note that there’s an infinite number of real values between `math.SmallestNonzeroFloat64` and `math.MaxFloat64`  Conversely, the float64 type has [](https://livebook.manning.com/book/100-go-mistakes-and-how-to-avoid-them/chapter-3/)a finite number of bits: 64. Because making infinite values fit into a finite space isn’t possible, we have to work with approximations. Hence, we may lose precision.

Floating points in Go follow the IEEE-754 standard, with some bits representing a mantissa and other bits representing an exponent.

The first implication is related to comparisons. Using the == operator to compare two floating-point numbers can lead to inaccuracies. Instead, we should compare their difference to see if it is less than some small error value.

Also bear in mind that the result of floating-point calculations depends on the actual processor. Most processors have a floating-point unit (FPU) to deal with such calculations. There is no guarantee that the result executed on one machine will be the same on another machine with a different FPU

##### KINDS OF FLOATING-POINT NUMBERS

- Positive infinite
- Negative infinite
- NaN (Not-a-Number), which is the result of an undefined or unrepresentable operation

decimal-to-floating-point conversions can lead to a loss of accuracy.

Go’s float32 and float64 are approximations. Because of that, we have to bear a few rules in mind:

- ==When comparing two floating-point numbers, check that their difference is within an acceptable range.==
- ==When performing additions or subtractions, group operations with a similar order of magnitude for better accuracy.==
- ==To favor accuracy, if a sequence of operations requires addition, subtraction, multiplication, or division, perform the multiplication and division operations first.==

## 3.4 #20: Not understanding slice length and capacity #Mistake 

In Go, a slice is backed by an array. That means the slice’s data is stored contiguously in an array data structure. A slice also handles the logic of adding an element if the backing array is full or shrinking the backing array if it’s almost empty.

Internally, a slice holds a pointer to the backing array plus a length and a capacity. The length is the number of elements the slice contains, whereas the capacity is the number of elements in the backing array. Let’s go through a few examples to make things clearer. First, let’s initialize a slice with a given length and capacity:

```go
s := make([]int, 3, 6) // Three-length, six-capacity slice
```

The first argument, representing the length, is mandatory. However, the second argument representing the capacity is optional.

In this case, make creates an array of six elements (the capacity). But because the length was set to 3, Go initializes only the first three elements. Also, because the slice is an int type, the first three elements are initialized to the zeroed value of an int: 0

However, accessing an element outside the length range is forbidden, even though it’s already allocated in memory. For example, s[4] = 0 would lead to the following panic:

```go
panic: runtime error: index out of range [4] with length 3
```

How can we use the remaining space of the slice? By using [](https://livebook.manning.com/book/100-go-mistakes-and-how-to-avoid-them/chapter-3/)the append built-in function:

```go
s = append(s, 2)
```

This code appends to the existing s slice a new element. The length of the slice is updated from 3 to 4 because the slice now contains four elements. Now, what happens if we add three more elements so that the backing array isn’t large enough?

```go
s = append(s, 3, 4, 5)
fmt.Println(s)
```

output: 

```go
[0 1 0 2 3 4 5]
```

Because an array is a fixed-size structure, it can store the new elements until element 4. When we want to insert element 5, the array is already full: Go internally creates another array by doubling the capacity, copying all the elements, and then inserting element 5.

![[Pasted image 20240102152234.png]]

> ***In Go, a slice grows by doubling its size until it contains 1,024 elements, after which it grows by 25%.***


The slice now references the new backing array. What will happen to the previous backing array? If it’s no longer referenced, it’s eventually freed by the garbage collector (GC) if allocated on the heap.

==What happens with slicing? Slicing is an operation done on an array or a slice, providing a half-open range; the first index is included, whereas the second is excluded.==

```go
s1 := make([]int, 3, 6) // Three-length, six-capacity slice
s2 := s1[1:3] // Slicing from indices 1 to 3
```

![[Pasted image 20240102152637.png]]


First, s1 is created as a three-length, six-capacity slice. When s2 is created by slicing s1, both slices reference the same backing array. However, s2 starts from a different index, 1. Therefore, its length and capacity (a two-length, five-capacity slice) differ from s1. If we update s1[1] or s2[0], the change is made to the same array, hence, visible in both slices

```go
s2 = append(s2, 2)
```

The shared backing array is modified, but only the length of s2 changes.
s1 remains a three-length, six-capacity slice.

One last thing to note: what if we keep appending elements to s2 until the backing array is full? What will the state be, memory-wise?

```go
s2 = append(s2, 3)
s2 = append(s2, 4)
s2 = append(s2, 5) // At this stage, the backing array is already full.
```

This code leads to creating another backing array

![[Pasted image 20240102152909.png]]

s1 and s2 now reference two different arrays. As s1 is still a three-length, six-capacity slice, it still has some available buffer, so it keeps referencing the initial array.

To summarize, the _slice length_ is the number of available elements in the slice, whereas the _slice capacity_ is the number of elements in the backing array. Adding an element to a full slice (length == capacity) leads to creating a new backing array with a new capacity, copying all the elements from the previous array, and updating the slice pointer to the new array.

## 3.5 #21: Inefficient slice initialization #Mistake 

While initializing a slice using make,  we have to provide a length and an optional capacity. Forgetting to pass an appropriate value for both of these parameters when it makes sense is a widespread mistake.

```go
func convert(foos []Foo) []Bar {
    bars := make([]Bar, 0) // Creates the resulting slice
 
    for _, foo := range foos {
        bars = append(bars, fooToBar(foo)) // Converts a Foo into a Bar and adds it to the slice
    }
    return bars
}
```

Every time the backing array is full, Go creates another array by doubling its capacity  This logic of creating another array because the current one is full is repeated multiple times when we add a third element, a fifth, a ninth, and so on. Assuming the input slice has 1,000 elements, this algorithm requires allocating 10 backing arrays and copying more than 1,000 elements in total from one array to another. This leads to additional effort for the GC to clean all these temporary backing arrays.

Performance-wise, there’s no good reason not to give the Go runtime a helping hand. There are two different options for this. The first option is to reuse the same code but allocate the slice with a given capacity:

```go
func convert(foos []Foo) []Bar {
    n := len(foos)
    bars := make([]Bar, 0, n) // Initializes with a zero length and a given capacity
 
    for _, foo := range foos {
        bars = append(bars, fooToBar(foo)) // Updates bars to append a new element
    }
    return bars
}
```

Internally, Go pre-allocates an array of _n_ elements. Therefore, adding up to _n_ elements means reusing the same backing array and hence reducing the number of allocations drastically. The second option is to allocate bars with a given length:

```go
func convert(foos []Foo) []Bar {
    n := len(foos)
    bars := make([]Bar, n) // Initializes with a given length
 
    for i, foo := range foos {
        bars[i] = fooToBar(foo) // Sets element i of the slice
    }
    return bars
}
```

Because we initialize the slice with a length, _n_ elements are already allocated and initialized to the zero value of Bar. Hence, to set elements, we have to use, not append but bars[i]

>If setting a capacity and using append is less efficient than setting a length and assigning to a direct index, why do we see this approach being used in Go projects?
>
> Using `append` in Go provides simplicity and readability, aligning with the language's design principles, even if it may be less memory-efficient than pre-allocating and direct indexing.


Converting one slice type into another is a frequent operation for Go developers.  if the length of the future slice is already known, there is no good reason to allocate an empty slice first. Our options are to allocate a slice with either a given capacity or a given length. Of these two solutions, we have seen that the second tends to be slightly faster. But using a given capacity and append can be easier to implement and read in some contexts.

## 3.6 #22: Being confused about nil vs. empty slices #Mistake 

- ==A slice is empty if its length is equal to 0.==
- ==A slice is nil if it equals nil.==

```go
func main() {
    var s []string // Option 1 (a 0 value)
    log(1, s)
 
    s = []string(nil) // Option 2
    log(2, s)
 
    s = []string{} // Option 3 
    log(3, s)
 
    s = make([]string, 0) // Option 4
    log(4, s)
}
 
func log(i int, s []string) {
    fmt.Printf("%d: empty=%t\tnil=%t\n", i, len(s) == 0, s == nil)
}
```

This example prints the following:

```go
1: empty=true   nil=true
2: empty=true   nil=true
3: empty=true   nil=false
4: empty=true   nil=false
```

All the slices are empty, meaning the length equals 0. Therefore, a nil slice is also an empty slice. However, only the first two are nil slices. If we have multiple ways to initialize a slice, which option should we favor? There are two things to note:

- One of the main differences between a nil and an empty slice regards allocations. Initializing a nil slice doesn’t require any allocation, which isn’t the case for an empty slice.
- Regardless of whether a slice is nil, calling the append built-in function works.

```go
var s1 []string
fmt.Println(append(s1, "foo")) // [foo]
```

Consequently, if a function returns a slice, we shouldn’t do as in other languages and return a non-nil collection for defensive reasons. Because a nil slice doesn’t require any allocation, we should favor returning a nil slice instead of an empty slice.

```go
func f() []string {
    var s []string
    if foo() {
        s = append(s, "foo")
    }
    if bar() {
        s = append(s, "bar")
    }
    return s
}
```

If both foo and bar are false, we get an empty slice. To prevent allocating an empty slice for no particular reason, we should favor option 1 (var s []string)

option 3: s := []string{}. This form is recommended to create a slice with initial elements:

```go
s := []string{"foo", "bar", "baz"}
```

option 3 should be avoided without initial elements.

```go
var s1 []float32 // Nil slice
    customer1 := customer{
    ID:         "foo",
    Operations: s1,
}
b, _ := json.Marshal(customer1)
fmt.Println(string(b))
 
s2 := make([]float32, 0) // Non-nil, empty slice
    customer2 := customer{
    ID:         "bar",
    Operations: s2,
}
b, _ = json.Marshal(customer2)
fmt.Println(string(b))
```

```go
{"ID":"foo","Operations":null}
{"ID":"bar","Operations":[]}
```

Here, a nil slice is marshaled as a null element, whereas a non-nil, empty slice is marshaled as an empty array. If we work in the context of strict JSON clients that differentiate between null and [], it’s essential to keep this distinction in mind.

To summarize, in Go, there is a distinction between nil and empty slices. A nil slice equals nil, whereas an empty slice has a length of zero. A nil slice is empty, but an empty slice isn’t necessarily nil. Meanwhile, a nil slice doesn’t require any allocation. We have seen throughout this section how to initialize a slice depending on the context by using

- ==var s []string if we aren’t sure about the final length and the slice can be empty==
- ==[]string(nil) as syntactic sugar to create a nil and empty slice==
- ==make([]string, length) if the future length is known==

## 3.7 #23: Not properly checking if a slice is empty #Mistake 

what’s the idiomatic way to check if a slice contains elements?

```go
 func handleOperations(id string) {
    operations := getOperations(id)
    if operations != nil { // Checks if the operations slice is nil
        handle(operations)
    }
}
 
func getOperations(id string) []float32 {
    operations := make([]float32, 0) // Initializes the operations slice
 
    if id == "" {
        return operations // Returns operations if the provided id is empty
    }
 
    // Add elements to operations
 
    return operations
}
```

But there’s a problem with this code: `getOperations` never returns a nil slice
instead, it returns an empty slice. Therefore, the operations != nil check will always be true.

One approach might be to modify `getOperations` to return a nil slice if id is empty:

```go
func getOperations(id string) []float32 {
    operations := make([]float32, 0) // Returns nil instead of operations
 
    if id == "" {
        return nil
    }
 
    // Add elements to operations
 
    return operations
}
```

How then can we check whether a slice is empty or nil? The solution is to check the length:

```go
func handleOperations(id string) {
    operations := getOperations(id)
    if len(operations) != 0 { // Checks the slice length
        handle(operations)
    }
}
```

an empty slice has, by definition, a length of zero. Meanwhile, nil slices are always empty. Therefore, by checking the length of the slice, we cover all the scenarios:

- ==If the slice is nil, len(operations) != 0 is false.==
    
- ==If the slice isn’t nil but empty, len(operations) != 0 is also false.==

Hence, checking the length is the best option to follow as we can’t always control the approach taken by the functions we call. Meanwhile, as the Go wiki states, when designing interfaces, we should avoid distinguishing nil and empty slices, which leads to subtle programming errors. When returning slices, it should make neither a semantic nor a technical difference if we return a nil or empty slice. Both should mean the same thing for the callers. This principle is the same with maps. To check if a map is empty, check its length, not whether it’s nil.

## 3.8 #24: Not making slice copies correctly #Mistake 

The copy built-in function allows [](https://livebook.manning.com/book/100-go-mistakes-and-how-to-avoid-them/chapter-3/)copying elements from a source slice into a destination slice.
a common mistake that results in copying the wrong number of elements.

```GO
src := []int{0, 1, 2}
var dst []int
copy(dst, src)
fmt.Println(dst)
```

it prints [], not [0 1 2]. What did we miss?

To use copy effectively, it’s essential to understand that the number of elements copied to the destination slice corresponds to the minimum between:

- ==The source slice’s length==
- ==The destination slice’s length==

In the previous example, src is a three-length slice, but dst is a zero-length slice because it is initialized to its zero value. Therefore, the copy function copies the minimum number of elements The resulting slice is then empty 

If we want to perform a complete copy, the destination slice must have a length greater than or equal to the source slice’s length.

```go
src := []int{0, 1, 2}
dst := make([]int, len(src))
copy(dst, src)
fmt.Println(dst)
```


>***Another common mistake is to invert the order of the arguments when calling copy. Remember that the destination is the former argument, whereas the source is the latter.***


using the copy built-in function isn’t [](https://livebook.manning.com/book/100-go-mistakes-and-how-to-avoid-them/chapter-3/)the only way to copy slice elements.

```go
src := []int{0, 1, 2}
dst := append([]int(nil), src...)
```

This alternative has the advantage of being done in a single line. However, using copy is more idiomatic and, therefore, easier to understand, even though it takes an extra line.

When using copy, recall that the number of elements copied to the destination corresponds to the minimum between the two slices’ lengths

## 3.9 #25: Unexpected side effects using slice append #Mistake 

```go
s1 := []int{1, 2, 3}
s2 := s1[1:2]
s3 := append(s2, 10)
```

initialize an s1 slice containing three elements, and s2 is created from slicing s1. Then we call append on s3

s1 is a three-length, three-capacity slice, and s2 is a one-length, two-capacity slice, both backed by the same array we already mentioned. Adding an element using append checks whether the slice is full (length == capacity). If it is not full, the append function adds the element by updating the backing array and returning a slice having a length incremented by 1.

In the backing array, we updated the last element to store 10. Therefore, if we print all the slices, we get this output:

```go
s1=[1 2 10], s2=[2], s3=[2 10]
```

one impact of this principle by passing the result of a slicing operation to a function

```go
func main() {
    s := []int{1, 2, 3}
 
    f(s[:2])
    // Use s
}
 
func f(s []int) {
    // Update s
}
```

if f updates the first two elements, the changes are visible to the slice in main. However, if f calls append, it updates the third element of the slice, even though we pass only two elements

```go
func main() {
    s := []int{1, 2, 3}
 
    f(s[:2])
    fmt.Println(s) // [1 2 10]
}
 
func f(s []int) {
    _ = append(s, 10)
}
```

to _protect_ the third element for defensive reasons, meaning to ensure that f doesn’t update it, we have two options.
The first is to pass a copy of the slice and then construct the resulting slice:

```go
func main() {
    s := []int{1, 2, 3}
    sCopy := make([]int, 2)
    copy(sCopy, s) // Copies the first two elements of s into sCopy
 
    f(sCopy)
    result := append(sCopy, s[2]) // Appends s[2] to sCopy to construct the resulting slice
    // Use result
}
 
func f(s []int) {
    // Update s
}
```

Because we pass a copy to f, even if this function calls append, it will not lead to a side effect outside of the range of the first two elements. The downside of this option is that it makes the code more complex to read and adds an extra copy, which can be a problem if the slice is large.

The second option can be used to limit the range of potential side effects to the first two elements only. This option involves the so-called _full slice expression_: `s[low:high:max]`. This statement creates a slice similar to the one created with `s[low:high]`, except that the resulting slice’s capacity is equal to max - low

```go
func main() {
    s := []int{1, 2, 3}
    f(s[:2:2]) // Passes a subslice using the full slice expression
    // Use s
}
 
func f(s []int) {
    // Update s
}
```

Here, the slice passed to f isn’t s[:2] but s[:2:2]. Hence, the slice’s capacity is 2 – 0 = 2,

When passing s[:2:2], we can limit the range of effects to the first two elements. Doing so also prevents us from having to perform a slice copy.

If the resulting slice has a length smaller than its capacity, append can mutate the original slice. If we want to restrict the range of possible side effects, we can use either a slice copy or the full slice expression, which prevents us from doing a copy.

## 3.10 #26: Slices and memory leaks #Mistake 

### 3.10.1 Leaking capacity

```go
func consumeMessages() {
    for {
        msg := receiveMessage() // Receives a new []byte slice assigned to msg
        // Do something with msg
        storeMessageType(getMessageType(msg)) // Stores the latest 1,000 message types in memory
    }
}
 
func getMessageType(msg []byte) []byte { // Computes the message type by slicing msg
    return msg[:5]
}
```

The `getMessageType` function computes the message type by slicing the input slice.

The slicing operation on msg using msg[:5] creates a five-length slice. However, its capacity remains the same as the initial slice. The remaining elements are still allocated in memory, even if eventually msg is not referenced.

##### After a new loop iteration, msg is no longer used. However, its backing array will still be used by msg[:5].

The backing array of the slice still contains 1 million bytes after the slicing operation.

What can we do to solve this issue? We can make a slice copy instead of slicing msg:

```go
func getMessageType(msg []byte) []byte {
    msgType := make([]byte, 5)
    copy(msgType, msg)
    return msgType
}
```

Because we perform a copy, `msgType` is a five-length, five-capacity slice regardless of the size of the message received. Hence, we only store 5 bytes per message type.

As a rule of thumb, remember that slicing a large slice or array can lead to potential high memory consumption. The remaining space won’t be reclaimed by the GC, and we can keep a large backing array despite using only a few elements. Using a slice copy is the solution to prevent such a case

### 3.10.2 Slice and pointers

what about the elements, which are still part of the backing array but outside the length range? Does the GC collect them?

```go
type Foo struct {
    v []byte
}
```

1. Allocate a slice of 1,000 Foo elements.
2. Iterate over each Foo element, and for each one, allocate 1 MB for the v slice.
3. Call `keepFirstTwoElementsOnly`, which returns only the first two elements using slicing, and then call a GC.

```go
func main() {
    foos := make([]Foo, 1_000) // Allocates a slice of 1,000 elements
    printAlloc()
 
    for i := 0; i < len(foos); i++ { // For each element, allocates a slice of 1 MB
        foos[i] = Foo{
            v: make([]byte, 1024*1024),
        }
    }
    printAlloc()
 
    two := keepFirstTwoElementsOnly(foos) // Keeps only the first two elements
    runtime.GC() // Runs the GC to force cleaning the heap
    printAlloc()
    runtime.KeepAlive(two) // Keeps a reference to the two variable
}
 
func keepFirstTwoElementsOnly(foos []Foo) []Foo {
    return foos[:2]
}
```

In this example, we allocate the foos slice, allocate a slice of 1 MB for each element, and then call `keepFirstTwoElementsOnly` and a GC. In the end, we use runtime .`KeepAlive` to keep a reference to the two variable after the garbage collection so that it won’t be collected.

 may expect the GC to collect the 998 remaining Foo elements and the data allocated for the slice because these elements can no longer be accessed. However, this isn’t the case

output: 

```go
83 KB
1024072 KB
1024072 KB
```

It’s essential to keep this rule in mind when working with slices: if the element is a pointer or a struct with pointer fields, the elements won’t be reclaimed by the GC. In our example, because Foo contains a slice (and a slice is a pointer on top of a backing array), the remaining 998 Foo elements and their slice aren’t reclaimed. Therefore, even though these 998 elements can’t be accessed, they stay in memory as long as the variable returned by `keepFirstTwoElementsOnly` is referenced.

What are the options to ensure that we don’t leak the remaining Foo elements? The first option, again, is to create a copy of the slice:

```go
func keepFirstTwoElementsOnly(foos []Foo) []Foo {
    res := make([]Foo, 2)
    copy(res, foos)
    return res
}
```

Because we copy the first two elements of the slice, the GC knows that the 998 elements won’t be referenced anymore and can now be collected.

There’s a second option if we want to keep the underlying capacity of 1,000 elements, which is to mark the slices of the remaining elements explicitly as nil:

```go
func keepFirstTwoElementsOnly(foos []Foo) []Foo {
    for i := 2; i < len(foos); i++ {
        foos[i].v = nil
    }
    return foos[:2]
}
```

two potential memory leak problems. The first was about slicing an existing slice or array to preserve the capacity. If we handle large slices and reslice them to keep only a fraction, a lot of memory will remain allocated but unused. The second problem is that when we use the slicing operation with pointers or structs with pointer fields, we need to know that the GC won’t reclaim these elements. In that case, the two options are to either perform a copy or explicitly mark the remaining elements or their fields to nil.

## 3.11 #27: Inefficient map initialization #Mistake 

### 3.11.1 Concepts

A _map_ provides an unordered collection of key-value pairs in which all the keys are distinct. In Go, a map is based on the hash table data structure. Internally, a hash table is an array of buckets, and each bucket is a pointer to an array of key-value pairs

Each operation (read, update, insert, delete) is done by associating a key to an array index. This step relies on a hash function. This function is stable because we want it to return the same bucket, given the same key, consistently.

In the case of insertion into a bucket that is already full (bucket overflow), Go creates another bucket of eight elements and links the previous bucket to it

### 3.11.2 Initialization

```go
m := map[string]int{
    "1": 1,
    "2": 2,
    "3": 3,
}
```

Internally, this map is backed by an array consisting of a single entry: hence, a single bucket. What happens if we add 1 million elements? In this case, a single entry won’t be enough because finding a key would mean, in the worst case, going over thousands of buckets. This is why a map should be able to grow automatically to cope with the number of elements.

When a map grows, it doubles its number of buckets. ==What are the conditions for a map to grow?==

- ==The average number of items in the buckets (called the _load factor_) is greater than a constant value. This constant equals 6.5 (but it may change in future versions because it’s internal to Go).==
- ==Too many buckets have overflowed (containing more than eight elements).==

When a map grows, all the keys are dispatched again to all the buckets. This is why, in the worst-case scenario, inserting a key can be an _O_(_n_) operation, with _n_ being the total number of elements in the map.

can use the make built-in function to provide an initial size when creating a map.

```go
m := make(map[string]int, 1_000_000)
```

By specifying a size, we provide a hint about the number of elements expected to go into the map. Internally, the map is created with an appropriate number of buckets to store 1 million elements. This saves a lot of computation time because the map won’t have to create buckets on the fly and handle rebalancing buckets. 

Also, specifying a size _n_ doesn’t mean making a map with a maximum number of _n_ elements. We can still add more than _n_ elements if needed. Instead, it means asking the Go runtime to allocate a map with room for at least _n_ elements, which is helpful if we already know the size up front.

 if we know up front the number of elements a map will contain, we should create it by providing an initial size. Doing this avoids potential map growth, which is quite heavy computation-wise because it requires reallocating enough space and rebalancing all the elements.

## 3.12 #28: Maps and memory leaks #Mistake 

```GO
m := make(map[int][128]byte)
```

Each value of m is an array of 128 bytes. We will do the following:

1. ==Allocate an empty map.==
2. ==Add 1 million elements.==
3. ==Remove all the elements, and run a GC.==

After each step, we want to print the size of the heap (using MB this time). This shows us how this example behaves memory-wise:

```go
n := 1_000_000
m := make(map[int][128]byte)
printAlloc()
 
for i := 0; i < n; i++ { // Adds 1 million elements
    m[i] = randBytes()
}
printAlloc()
 
for i := 0; i < n; i++ { // Deletes 1 million elements
    delete(m, i)
}
 
runtime.GC() // Triggers a manual GC
printAlloc()
runtime.KeepAlive(m) // Keeps a reference to m so that the map isn’t collected
```

output: 

```
0 MB // After m is allocated
461 MB // After we add 1 million elements
293 MB // After we remove 1 million elements
```

The reason is that the number of buckets in a map cannot shrink. Therefore, removing elements from a map doesn’t impact the number of existing buckets; it just zeroes the slots in the buckets. A map can only grow and have more buckets; it never shrinks.

In the previous example, we went from 461 MB to 293 MB because the elements were collected, but running the GC didn’t impact the map itself. Even the number of extra buckets (the buckets created because of overflows) remains the same.

let’s say we want to store one hour of data. Meanwhile, our company has decided to have a big promotion for Black Friday: in one hour, we may have millions of customers connected to our system. But a few days after Black Friday, our map will contain the same number of buckets as during the peak time. This explains why we can experience high memory consumption that doesn’t significantly decrease in such a scenario.

What are the solutions ? One solution could be to re-create a copy of the current map at a regular pace. For example, every hour, we can build a new map, copy all the elements, and release the previous one. The main drawback of this option is that following the copy and until the next garbage collection, we may consume twice the current memory for a short period.

Another solution would be to change the map type to store an array pointer: `map[int]*[128]byte`

 >**NOTE**
>If a key or a value is over 128 bytes, Go won’t store it directly in the map bucket. Instead, Go stores a pointer to reference the key or the value.

adding _n_ elements to a map and then deleting all the elements means keeping the same number of buckets in memory. So, we must remember that because a Go map can only grow in size, so does its memory consumption

## 3.13 #29: Comparing values incorrectly #Mistake 

```go
type customer struct {
    id string
}
 
func main() {
    cust1 := customer{id: "x"}
    cust2 := customer{id: "x"}
    fmt.Println(cust1 == cust2)
}
```

Comparing these two customer structs is a valid operation in Go, and it will print true

```go
type customer struct {
    id         string
    operations []float64 // New field
}
 
func main() {
    cust1 := customer{id: "x", operations: []float64{1.}}
    cust2 := customer{id: "x", operations: []float64{1.}}
    fmt.Println(cust1 == cust2)
}
```

We might expect this code to print true as well. However, it doesn’t even compile:

```go
invalid operation:
    cust1 == cust2 (struct containing []float64 cannot be compared)
```

The problem relates to how the == and != operators work. These operators don’t work with slices or maps. Hence, because the customer struct contains a slice, it doesn’t compile.

It’s essential to understand how to use == and != to make comparisons effectively. We can use these operators on operands that are _comparable_:

- ==_Booleans_—Compare whether two Booleans are equal.==
- ==_Numerics (int, float, and complex types)_—Compare whether two numerics are equal.==
- ==_Strings_—Compare whether two strings are equal.==
- ==_Channels_—Compare whether two channels were created by the same call to make or if both are nil.==
- ==_Interfaces_—Compare whether two interfaces have identical dynamic types and equal dynamic values or if both are nil.==
- ==_Pointers_—Compare whether two pointers point to the same value in memory or if both are nil.==
- ==_Structs and arrays_—Compare whether they are composed of similar types.==

```go
var a any = 3
var b any = 3
fmt.Println(a == b)
```

output

```go
true
```

```GO
var cust1 any = customer{id: "x", operations: []float64{1.}}
var cust2 any = customer{id: "x", operations: []float64{1.}}
fmt.Println(cust1 == cust2)
```

This code compiles. But as both types can’t be compared because the customer struct contains a slice field, it leads to an error at run time:

```go
 panic: runtime error: comparing uncomparable type main.customer
```

what are the options if we have to compare two slices, two maps, or two structs containing noncomparable types?  If we stick with the standard library, one option is to use run-time reflection with the reflect package.

_Reflection_ is a form of metaprogramming, and it refers to the ability of an application to introspect and modify its structure and behavior. For example, in Go, we can use `reflect.DeepEqual`. This function reports whether two elements are _deeply equal_ by recursively traversing two values. The elements it accepts are basic types plus arrays, structs, slices, maps, pointers, interfaces, and functions.

```go
cust1 := customer{id: "x", operations: []float64{1.}}
cust2 := customer{id: "x", operations: []float64{1.}}
fmt.Println(reflect.DeepEqual(cust1, cust2))
```

```go
true
```

there are two things to keep in mind when using `reflect.DeepEqual`. First, it makes the distinction between an empty and a nil collection

The other catch is something pretty standard in most languages. Because this function uses reflection, which introspects values at run time to discover how they are formed, it has a performance penalty.

If performance is a crucial factor, another option might be to implement our own comparison method.

```go
func (a customer) equal(b customer) bool {
    if a.id != b.id { // Compares the id fields
        return false
    }
    if len(a.operations) != len(b.operations) { // Checks the length of both slices
        return false
    }
    for i := 0; i < len(a.operations); i++ {
        if a.operations[i] != b.operations[i] { // Compares each element of both slices
            return false
        }
    }
    return true
}
```

In general, we should remember that the == operator is pretty limited. For example, it doesn’t work with slices and maps. In most cases, using `reflect.DeepEqual` is a solution, but the main catch is the performance penalty.
 if performance is crucial at run time, implementing our custom method might be the best solution.

## Summary #Summary 

- ==When reading existing code, bear in mind that integer literals starting with 0 are octal numbers. Also, to improve readability, make octal integers explicit by prefixing them with 0o.==
- ==Because integer overflows and underflows are handled silently in Go, you can implement your own functions to catch them.==
- ==Making floating-point comparisons within a given delta can ensure that your code is portable.==
- ==When performing addition or subtraction, group the operations with a similar order of magnitude to favor accuracy. Also, perform multiplication and division before addition and subtraction.==
- ==Understanding the difference between slice length and capacity should be part of a Go developer’s core knowledge. The slice length is the number of available elements in the slice, whereas the slice capacity is the number of elements in the backing array.==
- ==When creating a slice, initialize it with a given length or capacity if its length is already known. This reduces the number of allocations and improves performance. The same logic goes for maps, and you need to initialize their size.==
- ==Using copy or the full slice expression is a way to prevent append from creating conflicts if two different functions use slices backed by the same array. However, only a slice copy prevents memory leaks if you want to shrink a large slice.==
- ==To copy one slice to another using the copy built-in function, remember that the number of copied elements corresponds to the minimum between the two slice’s lengths.==
- ==Working with a slice of pointers or structs with pointer fields, you can avoid memory leaks by marking as nil the elements excluded by a slicing operation.==
- ==To prevent common confusions such as when using the encoding/json or the reflect package, you need to understand the difference between nil and empty slices. Both are zero-length, zero-capacity slices, but only a nil slice doesn’t require allocation.==
- ==To check if a slice doesn’t contain any element, check its length. This check works regardless of whether the slice is nil or empty. The same goes for maps.==
- ==To design unambiguous APIs, you shouldn’t distinguish between nil and empty slices.==
- ==A map can always grow in memory, but it never shrinks. Hence, if it leads to some memory issues, you can try different options, such as forcing Go to re-create the map or using pointers.==
- ==To compare types in Go, you can use the == ==and != operators if two types are comparable: Booleans, numerals, strings, pointers, channels, and structs are composed entirely of comparable types. Otherwise, you can either use `reflect.DeepEqual` and pay the price of reflection or use custom implementations and libraries.====


# 4 Control structures

there is no do or while loop in Go, only a generalized for.

## 4.1 #30: Ignoring the fact that elements are copied in range loops #Mistake 

### 4.1.1 Concepts

A range loop allows iterating over different data structures:

- ==String==
- ==Array==
- ==Pointer to an array==
- ==Slice==
- ==Map==
- ==Receiving channel==


Compared to a classic for loop, a range loop is a convenient way to iterate over all the elements of one of these data structure. It’s also less error-prone because we don’t have to handle the condition expression and iteration variable manually, which may avoid mistakes such as off-by-one errors.

```GO
s := []string{"a", "b", "c"}
for i, v := range s {
    fmt.Printf("index=%d, value=%s\n", i, v)
}
```

In general, range produces two values for each data structure except a receiving channel, for which it produces a single element (the value).

In some cases, we may only be interested in the element value, not the index. we can instead use the blank identifier to replace the index variable

```GO
s := []string{"a", "b", "c"}
for _, v := range s {
    fmt.Printf("value=%s\n", v)
}
```

hanks to the blank identifier, we iterate over each element by ignoring the index and assigning only the element value to v.

If we’re not interested in the value, we can omit the second element:

```go
for i := range s {}
```

### 4.1.2 Value copy

```go
type account struct {
    balance float32
}
```

```go
accounts := []account{
    {balance: 100.},
    {balance: 200.},
    {balance: 300.},
}
for _, a := range accounts {
    a.balance += 1000
}
```

Following this code, which of the following two choices do you think shows the slice’s content?

- [{100} {200} {300}]
- [{1100} {1200} {1300}]

The answer is [{100} {200} {300}]. In this example, the range loop does not affect the slice’s content.

==In Go, everything we assign is a copy:==

- ==If we assign the result of a function returning a _struct_, it performs a copy of that struct.==
- ==If we assign the result of a function returning a _pointer_, it performs a copy of the memory address==

It’s crucial to keep this in mind to avoid common mistakes, including those related to range loops. Indeed, when a range loop iterates over a data structure, it performs a copy of each element to the value variable (the second item).

iterating over each account element results in a struct copy being assigned to the value variable a. Therefore, incrementing the balance with `a.balance` += 1000 mutates only the value variable (a), not an element in the slice.

So, what if we want to update the slice elements? There are two main options. The first option is to access the element using the slice index.

```go
for i := range accounts { // Uses the index variable to access the element of the slice
    accounts[i].balance += 1000
}
 
for i := 0; i < len(accounts); i++ { // Uses the traditional for loop
    accounts[i].balance += 1000
}
```

**UPDATING SLICE ELEMENTS: A THIRD OPTION**

```go
accounts := []*account{ // Updates the slice type to []*account
    {balance: 100.},
    {balance: 200.},
    {balance: 300.},
}
for _, a := range accounts { // Updates the slice elements directly
    a.balance += 1000
}
```

 the a variable is a copy of the account pointer stored in the slice. But as both pointers reference the same struct, the `a.balance` += 1000 statement updates the slice element.

However, this option has two main downsides. First, it requires updating the slice type, which may not always be possible. Second, if performance is important, we should note that iterating over a slice of pointers may be less efficient for a CPU because of the lack of predictability


In general the value element in a range loop is a copy. Therefore, if the value is a struct we need to mutate, we will only update the copy, not the element itself, unless the value or field we modify is a pointer. The favored options are to access the element via the index using a range loop or a classic for loop.

## 4.2 #31: Ignoring how arguments are evaluated in range loops #Mistake 


The range loop syntax requires an expression `for i, v := range exp`, exp is the expression
how is this expression evaluated? When using a range loop, this is an essential point to avoid common mistakes.

```go
s := []int{0, 1, 2}
for range s {
    s = append(s, 10)
}
```


when using a range loop, the provided expression is evaluated only once, before the beginning of the loop. In this context, “evaluated” means the provided expression is copied to a temporary variable, and then range iterates over this variable

The range loop uses this temporary variable. The original slice s is also updated during each iteration

the temporary slice used by range remains a three-length slice. Hence, the loop completes after three iterations.

The behavior is different with a classic for loop 

```go
s := []int{0, 1, 2}
for i := 0; i < len(s); i++ {
    s = append(s, 10)
}
```

the loop never ends. The len(s) expression is evaluated during each iteration, and because we keep adding elements, we will never reach a termination state. It’s essential to keep this difference in mind to use Go loops accurately.

the behavior we described (expression evaluated only once) also applies to all the data types provided

### 4.2.1 Channels

```go
ch1 := make(chan int, 3) // Creates a first channel that will contain elements 0, 1, and 2
go func() {
    ch1 <- 0
    ch1 <- 1
    ch1 <- 2
    close(ch1)
}()
 
ch2 := make(chan int, 3) // Creates a second channel that will contain elements 10, 11, and 12
go func() {
    ch2 <- 10
    ch2 <- 11
    ch2 <- 12
    close(ch2)
}()
 
ch := ch1 // Assigns the first channel to ch
for v := range ch { // Creates a channel consumer by iterating over ch
    fmt.Println(v)
    ch = ch2 // Assigns the second channel to ch
}
```

In this example, the same logic applies regarding how the range expression is evaluated. The expression provided to range is a ch channel pointing to ch1. Hence, range evaluates ch, performs a copy to a temporary variable, and iterates over elements from this channel. Despite the ch = ch2 statement, range keeps iterating over ch1, not ch2:

```
0
1
2
```

The ch = ch2 statement isn’t without effect, though. Because we assigned ch to the second variable, if we call close(ch) following this code, it will close the second channel, not the first.

### 4.2.2 Array

```go
a := [3]int{0, 1, 2} // Creates an array of three elements
for i, v := range a { //Iterates over the array
    a[2] = 10 // Updates the last index
    if i == 2 { // Prints the content of the last index
        fmt.Println(v)
    }
}
```

**range iterates over the array copy (left) while the loop modifies a (right).**

 the range operator creates a copy of the array. Meanwhile, the loop doesn’t update the copy; it updates the original array: a. Therefore, the value of v during the last iteration is 2, not 10.

If we want to print the actual value of the last element, we can do so in two ways:

- By accessing the element from its index:

```go
a := [3]int{0, 1, 2}
for i := range a {
    a[2] = 10
    if i == 2 {
        fmt.Println(a[2]) // Accesses a[2] instead of the range value variable
    }
}
```

- Using an array pointer:

```go
a := [3]int{0, 1, 2}
for i, v := range &a { // Ranges over &a instead of a
    a[2] = 10
    if i == 2 {
        fmt.Println(v)
    }
}
```

Both options are valid. However, the second option doesn’t lead to copying the whole array, which may be something to keep in mind in case the array is significantly large.

In summary, the range loop evaluates the provided expression only once, before the beginning of the loop, by doing a copy

## 4.3 #32: Ignoring the impact of using pointer elements in range loops #Mistake 

- In terms of semantics, storing data using pointer semantics implies sharing the element. For example, the following method holds the logic to insert an element into a cache:

```go
type Store struct {
    m map[string]*Foo
}
 
func (s Store) Put(id string, foo *Foo) {
    s.m[id] = foo
    // ...
}
```

- using the pointer semantics implies that the Foo element is shared by both the caller of Put and the Store struct.

- Sometimes we already manipulate pointers. Hence, it can be handy to store pointers directly in our collection instead of values.
- If we store large structs, and these structs are frequently mutated, we can use pointers instead to avoid a copy and an insertion for each mutation:

```go
func updateMapValue(mapValue map[string]LargeStruct, id string) {
    value := mapValue[id] // Copies
    value.foo = "bar"
    mapValue[id] = value // Inserts
}
 
func updateMapPointer(mapPointer map[string]*LargeStruct, id string) {
    mapPointer[id].foo = "bar" // Mutates the map element directly
}
```


- A Customer struct representing a customer
    
- A Store that holds a map of Customer pointers

```go
type Customer struct {
    ID      string
    Balance float64
}
 
type Store struct {
    m map[string]*Customer
}
```

```go
func (s *Store) storeCustomers(customers []Customer) {
    for _, customer := range customers {
        s.m[customer.ID] = &customer // Stores the customer pointer in the map
    }
}
```

```go
s.storeCustomers([]Customer{
    {ID: "1", Balance: 10},
    {ID: "2", Balance: -10},
    {ID: "3", Balance: 0},
})
```

output: 

```go
key=1, value=&main.Customer{ID:"3", Balance:0}
key=2, value=&main.Customer{ID:"3", Balance:0}
key=3, value=&main.Customer{ID:"3", Balance:0}
```

instead of storing three different Customer structs, all the elements stored in the map reference the same Customer struct: 3. What have we done wrong?

Iterating over the customers slice using the range loop, regardless of the number of elements, creates a single customer variable with a fixed address.

```go
func (s *Store) storeCustomers(customers []Customer) {
    for _, customer := range customers {
        fmt.Printf("%p\n", &customer)
        s.m[customer.ID] = &customer
    }
}
0xc000096020
0xc000096020
0xc000096020
```


Why is this important?

- During the first iteration, customer references the first element: Customer 1. We store a pointer to a customer struct.
- During the second iteration, customer now references another element: Customer 2. We also store a pointer to a customer struct.
- Finally, during the last iteration, customer references the last element: Customer 3. Again, the same pointer is stored in the map.

At the end of the iterations, we have stored the same pointer in the map three times. This pointer’s last assignment is a reference to the slice’s last element: Customer 3. This is why all the map elements reference the same Customer.

There are two main solutions. The first, “Unintended variable shadowing.” It requires creating a local variable:

```go
func (s *Store) storeCustomers(customers []Customer) {
    for _, customer := range customers {
        current := customer // Creates a local current variable
        s.m[current.ID] = &current // Stores this pointer in the map
    }
}
```

we don’t store a pointer referencing customer; instead, we store a pointer referencing current. current is a variable referencing a unique Customer during each iteration.  The other solution is to store a pointer referencing each element using the slice index:

```go
func (s *Store) storeCustomers(customers []Customer) {
    for i := range customers {
        customer := &customers[i] // Assigns to customer a pointer of the i element
        s.m[customer.ID] = customer // Stores the customer pointer
    }
}
```

customer is now a pointer. Because it’s initialized during each iteration, it has a unique address. Therefore, we store different pointers in the maps.

When iterating over a data structure using a range loop, we must recall that all the values are assigned to a unique variable with a single unique address. Therefore, if we store a pointer referencing this variable during each iteration, we will end up in a situation where we store the same pointer referencing the same element: the latest one.

## 4.4 #33: Making wrong assumptions during map iterations #Mistake 

- Ordering
- Map update during an iteration

### 4.4.1 Ordering

==a few fundamental behaviors of the map data structure:==

- ==It doesn’t keep the data sorted by key (a map isn’t based on a binary tree).==
- ==It doesn’t preserve the order in which the data was added.==

Furthermore, when iterating over a map, we shouldn’t make any ordering assumptions at all.

```go
for k := range m {
    fmt.Print(k)
}
```

the data isn’t sorted by key. Hence, we can’t expect this code to print `acdeyz`

In Go, the iteration order over a map is _not specified_. There is also no guarantee that the order will be the same from one iteration to the next, the order is different from one iteration to another.

>*Although there is no guarantee about the iteration order, the iteration distribution isn’t uniform. It’s why the official Go specification states that the iteration is unspecified, not random.*

So why does Go have such a surprising way to iterate over a map? It was a conscious choice by the language designers. They wanted to add some form of randomness to make sure developers never rely on any ordering assumptions while working with maps

let’s note that using packages from the standard library or external libraries can lead to different behaviors

If ordering is necessary, we should rely on other data structures such as a binary heap

### 4.4.2 Map insert during iteration

```go
m := map[int]bool{
    0: true,
    1: false,
    2: true,
}
 
for k, v := range m {
    if v {
        m[10+k] = true
    }
}
 
fmt.Println(m)
```

The result of this code is unpredictable.

```go
map[0:true 1:false 2:true 10:true 12:true 20:true 22:true 30:true]
map[0:true 1:false 2:true 10:true 12:true 20:true 22:true 30:true 32:true]
map[0:true 1:false 2:true 10:true 12:true 20:true]
```

> _If a map entry is created during iteration, it may be produced during the iteration or skipped. The choice may vary for each entry created and from one iteration to the next._
> Go specification

Hence, when an element is added to a map during an iteration, it may be produced during a follow-up iteration, or it may not. As Go developers, we don’t have any way to enforce the behavior. It also may vary from one iteration to another, one solution is to work on a copy of the map

```go
m := map[int]bool{
    0: true,
    1: false,
    2: true,
}
m2 := copyMap(m) // Creates a copy of the initial map
 
for k, v := range m {
    m2[k] = v
    if v {
        m2[10+k] = true // Updates m2 instead of m
    }
}
 
fmt.Println(m2)
```

```go
map[0:true 1:false 2:true 10:true 12:true]
```

==To summarize, when we work with a map, we shouldn’t rely on the following:==

- ==The data being ordered by keys==
- ==Preservation of the insertion order==
- ==A deterministic iteration order==
- ==An element being produced during the same iteration in which it’s added==

## 4.5 #34: Ignoring how the break statement works #Mistake 

A break statement is commonly used to terminate the execution of a loop.

```GO
for i := 0; i < 5; i++ {
    fmt.Printf("%d ", i)
 
    switch i {
    default:
    case 2:
        break
    }
}
```

The break statement doesn’t terminate the for loop: it terminates the switch statement, instead. Hence, instead of iterating from 0 to 2, this code iterates from 0 to 4: 0 1 2 3 4.

One essential rule to keep in mind is that a break statement terminates the execution of the innermost for, switch, or select statement

The most idiomatic way is to use a label:

```go
loop: // Defines a loop label
    for i := 0; i < 5; i++ {
        fmt.Printf("%d ", i)
 
        switch i {
        default:
        case 2:
            break loop // Terminates the loop attached to the loop label, not the switch
        }
    }
```

Breaking the wrong statement can also occur with a select inside a loop

```go
for {
    select {
    case <-ch:
        // Do something
    case <-ctx.Done():
        break
    }
}
```

Here the innermost for, switch, or select statement is the select statement, not the for loop.

```go
loop:
    for {
        select {
        case <-ch:
            // Do something
        case <-ctx.Done():
            break loop // Terminates the loop attached to the loop label, not the select
        }
    }
```


> *can also use continue with a label to go to the next iteration of the labeled loop.*

## 4.6 #35: Using defer inside a loop #Mistake 

The defer statement delays a call’s execution until the surrounding function returns. It’s mainly used to reduce boilerplate code. For example, if a resource has to be closed eventually, we can use defer to avoid repeating the closure calls before every single return.

```GO
func readFiles(ch <-chan string) error { // Iterates over the channel
    for path := range ch {
        file, err := os.Open(path) // Opens the file
        if err != nil {
            return err
        }
 
        defer file.Close() // Defers the call to file.Close()
 
        // Do something with file
    }
    return nil
}
```

is a significant problem with this implementation. We have to recall that defer schedules a function call when the _surrounding_ function returns. In this case, the defer calls are executed not during each loop iteration but when the readFiles function returns. If `readFiles` doesn’t return, the file descriptors will be kept open forever, causing leaks.

options to fix this problem? One might be to get rid of defer and handle the file closure manually.
create another surrounding function around defer that is called during each iteration.

```go
func readFiles(ch <-chan string) error {
    for path := range ch {
        if err := readFile(path); err != nil { // Calls the readFile function that contains the main logic
            return err
        }
    }
    return nil
}
 
func readFile(path string) error {
    file, err := os.Open(path)
    if err != nil {
        return err
    }
 
    defer file.Close() // Keeps the call to defer
 
    // Do something with file
    return nil
}
```

Another approach could be to make the `readFile` function a closure:

```go
func readFiles(ch <-chan string) error {
    for path := range ch {
        err := func() error {
            // ...
            defer file.Close()
            // ...
        }() // Runs the provided closure
        if err != nil {
            return err
        }
    }
    return nil
}
```

When using defer, we must remember that it schedules a function call when the surrounding function returns. Hence, calling defer within a loop will stack all the calls: they won’t be executed during each iteration, which may cause memory leaks if the loop doesn’t terminate, for example. The most convenient approach to solving this problem is introducing another function to be called during each iteration.

## Summary #Summary 

- ==The value element in a range loop is a copy. Therefore, to mutate a struct, for example, access it via its index or via a classic for loop.==
- ==Understanding that the expression passed to the range operator is evaluated only once before the beginning of the loop can help you avoid common mistakes such as inefficient assignment in channel or slice iteration.==
- ==Using a local variable or accessing an element using an index, you can prevent mistakes while copying pointers inside a loop.==
- ==To ensure predictable outputs when using maps, remember that a map data structure==
    - ==Doesn’t order the data by keys==
    - ==Doesn’t preserve the insertion order==
    - ==Doesn’t have a deterministic iteration order==
    - ==Doesn’t guarantee that an element added during an iteration will be produced during this iteration==
- ==Using break or continue with a label enforces breaking a specific statement. This can be helpful with switch or select statements inside loops.==
- ==Extracting loop logic inside a function leads to executing a defer statement at the end of each iteration.==

# 5 Strings

==In Go, a string is an immutable data structure holding the following:==

- ==pointer to an immutable byte sequence==
- ==The total number of bytes in this sequence==

## 5.1 #36: Not understanding the concept of a rune #Mistake 

==the distinction between a charset and an encoding:==

- ==A charset, as the name suggests, is a set of characters. For example, the Unicode charset contains 2^21 characters.==
- ==An encoding is the translation of a character’s list in binary. For example, UTF-8 is an encoding standard capable of encoding all the Unicode characters in a variable number of bytes (from 1 to 4 bytes).==

characters to simplify the charset definition. But in Unicode, we use the concept of a _code point_ to refer to an item represented by a single value

in Go, a rune _is_ a Unicode code point. Meanwhile UTF-8 encodes characters into 1 to 4 bytes, hence, up to 32 bits. This is why in Go, a rune is an alias of int32:

```go
type rune = int32
```

```go
s := "hello"
```

 In Go, a source code is encoded in UTF-8. So, all string literals are encoded into a sequence of bytes using UTF-8. However, a string is a sequence of arbitrary bytes; it’s not necessarily based on UTF-8. Hence, when we manipulate a variable that wasn’t initialized from a string literal we can’t necessarily assume that it uses the UTF-8 encoding.

```go
s := "hello"
fmt.Println(len(s)) // 5
```

But a character isn’t always encoded into a single byte.

```go
s := "汉"
fmt.Println(len(s)) // 3
```

**==the len built-in function applied  a string doesn’t return the number of characters; it returns the number of bytes.==**

In summary:

- ==A charset is a set of characters, whereas an encoding describes how to translate a charset into binary.==
- ==In Go, a string references an immutable slice of arbitrary bytes.==
- ==Go source code is encoded using UTF-8. Hence, all string literals are UTF-8 strings. But because a string can contain arbitrary bytes, if it’s obtained from somewhere else (not the source code), it isn’t guaranteed to be based on the UTF-8 encoding.==
- ==A rune corresponds to the concept of a Unicode code point, meaning an item represented by a single value.==
- ==Using UTF-8, a Unicode code point can be encoded into 1 to 4 bytes.==
- ==Using len on a string in Go returns the number of bytes, not the number of runes.==

## 5.2 #37: Inaccurate string iteration  #Mistake 

```GO
s := "hêllo" // The string literal contains a special rune: ê.
for i := range s {
    fmt.Printf("position %d: %c\n", i, s[i])
}
fmt.Printf("len=%d\n", len(s))
```

the output:

```go
position 0: h
position 1: Ã
position 3: l
position 4: l
position 5: o
len=6
```

- The second rune is Ã in the output instead of ê.
- We jumped from position 1 to position 3: what is at position 2?
- len returns a count of 6, whereas s contains only 5 runes.

len returns the number of bytes in a string, not the number of runes. Because we assigned a string literal to s, s is a UTF-8 string. Meanwhile, the special character ê isn’t encoded in a single byte; it requires 2 bytes. Therefore, calling len(s) returns 6.

>**CALCULATING THE NUMBER OF RUNES IN A STRING**
>What if we want to get the number of runes in a string, not the number of bytes? How we can do this depends on the encoding.
> can use the unicode/utf8 package:

```go
fmt.Println(utf8.RuneCountInString(s)) // 5
```

```go
for i := range s {
    fmt.Printf("position %d: %c\n", i, s[i])
}
```

we don’t iterate over each rune; instead, we iterate over each starting index of a rune
Printing s[i] doesn’t print the ith rune; it prints the UTF-8 representation of the byte at index i. Hence, we printed hÃllo instead of hêllo. So how do we fix the code if we want to print all the different runes? There are two main options.

We have to use the value element of the range operator:

```go
s := "hêllo"
for i, r := range s {
    fmt.Printf("position %d: %c\n", i, r)
}
```

Instead of printing the rune using s[i], we use the r variable. Using a range loop on a string returns two variables, the starting index of a rune and the rune itself:

```go
position 0: h
position 1: ê
position 3: l
position 4: l
position 5: o
```

The other approach is to convert the string into a slice of runes and iterate over it:

```go
s := "hêllo"
runes := []rune(s)
for i, r := range runes {
    fmt.Printf("position %d: %c\n", i, r)
}
position 0: h
position 1: ê
position 2: l
position 3: l
position 4: o
```

The only difference has to do with the position: instead of printing the starting index of the rune’s byte sequence, the code prints the rune’s index directly.  this solution introduces a run-time overhead compared to the previous one.  Therefore, if we want to iterate over all the runes, we should use the first solution. 

However, if we want to access the ith rune of a string with the first option, we don’t have access to the rune index; rather, we know the starting index of a rune in the byte sequence. Hence, we should favor the second option in most cases:

>**A POSSIBLE OPTIMIZATION TO ACCESS A SPECIFIC RUNE**
>One optimization is possible if a string is composed of single-byte runes: for example, if the string contains the letters A to Z and a to z. We can access the ith rune without converting the whole string into a slice of runes by accessing the byte directly using s[i]:

```go
s := "hello"
fmt.Printf("%c\n", rune(s[4])) // o
```

## 5.3 #38: Misusing trim functions #Mistake 

TrimRight and TrimSuffix. Both functions serve a similar purpose, and it can be fairly easy to confuse them.

```go
fmt.Println(strings.TrimRight("123oxo", "xo"))
```

The answer is 123.  `TrimRight` removes all the trailing runes contained in a given set.

TrimRight iterates backward over each rune. If a rune is part of the provided set, the function removes it. If not, the function stops its iteration and returns the remaining string. This is why our example returns 123.

On the other hand, `TrimSuffix` returns a string without a provided trailing suffix:

```go
fmt.Println(strings.TrimSuffix("123oxo", "xo"))
```

Because 123oxo ends with xo, this code prints 123o.  The principle is the same for the left-hand side of a string with `TrimLeft` and `TrimPrefix`:

```go
fmt.Println(strings.TrimLeft("oxo123", "ox")) // 123
fmt.Println(strings.TrimPrefix("oxo123", "ox")) /// o123
```

n summary, we have to make sure we understand the difference between `TrimRight/TrimLeft`, and `TrimSuffix/TrimPrefix`:

- `TrimRight/TrimLeft` removes the trailing/leading runes in a set.
- `TrimSuffix/TrimPrefix` removes a given suffix/prefix.

## 5.4 #39: Under-optimized string concatenation #Mistake 

```go
func concat(values []string) string {
    s := ""
    for _, value := range values {
        s += value
    }
    return s
}
```

During each iteration, the += operator concatenates s with the value string. But with this implementation, we forget one of the core characteristics of a string: its immutability. Therefore, each iteration doesn’t update s; it reallocates a new string in memory, which significantly impacts the performance of this function.

there is a solution to deal with this problem, using the strings package and the Builder struct:

```go
func concat(values []string) string {
    sb := strings.Builder{} // Creates a strings.Builder
    for _, value := range values {
        _, _ = sb.WriteString(value) // Appends a string
    }
    return sb.String() // Returns the resulted string
}
```

Using `strings.Builder`, we can also append

- A byte slice using Write
- A single byte using `WriteByte`
- A single rune using `WriteRune`

Internally, `strings.Builder` holds a byte slice. Each call to `WriteString` results in a call to append on this slice. There are two impacts. First, this struct shouldn’t be used concurrently, as the calls to append would lead to race conditions. The second impact is something that we saw in mistake #21, “Inefficient slice initialization”: if the future length of a slice is already known, we should pre-allocate it. For that purpose, `strings.Builder` exposes a method Grow(n int) to guarantee space for another _n_ bytes.

```go
func concat(values []string) string {
    total := 0
    for i := 0; i < len(values); i++ { // Iterates over each string to compute the total number of bytes
        total += len(values[i])
    }
 
    sb := strings.Builder{}
    sb.Grow(total) // Calls Grow with this total
    for _, value := range values {
        _, _ = sb.WriteString(value)
    }
    return sb.String()
}
```

`strings.Builder` is the recommended solution to concatenate a list of strings

As a general rule, we can remember that performance-wise, the `strings.Builder` solution is faster from the moment we have to concatenate more than about five strings. Even though this exact number depends on many factors, such as the size of the concatenated strings and the machine, this can be a rule of thumb to help us decide when to choose one solution over the other.

## 5.5 #40: Useless string conversions #Mistake 

When choosing to work with a string or a byte, most programmers tend to favor strings for convenience. But most I/O is actually done with byte. For example, io.Reader, `io.Writer`, and `io.ReadAll` work with byte, not strings. Hence, working with strings means extra conversions, although the bytes package contains many of the same operations as the strings package.

```go
func getBytes(reader io.Reader) ([]byte, error) {
    b, err := io.ReadAll(reader) // b is a []byte.
    if err != nil {
        return nil, err
    }
    // Call sanitize
}
```

```go
func sanitize(s string) string {
    return strings.TrimSpace(s)
}
```

as we manipulate a byte, we must first convert it to a string before calling sanitize. Then we have to convert the results back into a byte because `getBytes` returns a byte slice:

```go
return []byte(sanitize(string(b))), nil
```

What’s the problem with this implementation? We have to pay the extra price of converting a byte into a string and then converting a string into a byte. Memory-wise, each of these conversions requires an extra allocation.

It means a new memory allocation and a copy of all the bytes.

Instead of accepting and returning a string, we should manipulate a byte slice:

```go
func sanitize(b []byte) []byte {
    return bytes.TrimSpace(b)
}
```

The bytes package also has a `TrimSpace` function to trim all the leading and trail- ing white spaces. Then, calling the sanitize function doesn’t require any extra conversions:

Hence, whether we’re doing I/O or not, we should first check whether we could implement a whole workflow using bytes instead of strings and avoid the price of additional conversions.

## 5.6 #41: Substrings and memory leaks #Mistake 

To extract a subset of a string

```go
s1 := "Hello, World!"
s2 := s1[:5] // Hello
```

This example creates a string from the first five bytes, not the first five runes. Hence, we shouldn’t use this syntax in the case of runes encoded with multiple bytes. Instead, we should convert the input string into a rune type first:

```go
s1 := "Hêllo, World!"
s2 := string([]rune(s1)[:5]) // Hêllo
```

Each log will first be formatted with a universally unique identifier (UUID; 36 characters) followed by the message itself. We want to store these UUIDs in memory: for example, to keep a cache of the latest _n_ UUIDs. We should also note that these log messages can potentially be quite heavy (up to thousands of bytes).

```go
func (s store) handleLog(log string) error {
    if len(log) < 36 {
        return errors.New("log is not correctly formatted")
    }
    uuid := log[:36]
    s.store(uuid)
    // Do something
}
```

To extract the UUID, we use a substring operation with log[:36] hen we pass this uuid variable to the store method that will store it in memory. Is this solution problematic? Yes, it is.

When doing a substring operation, the Go specification doesn’t specify whether the resulting string and the one involved in the substring operation should share the same data. However, the standard Go compiler does let them share the same backing array, which is probably the best solution memory-wise and performance-wise as it prevents a new allocation and a copy.

log messages can be quite heavy. log[:36] will create a new string referencing the same backing array. Therefore, each uuid string that we store in memory will contain not just 36 bytes but the number of bytes in the initial log string: potentially, thousands of bytes.

How can we fix this? By making a deep copy of the substring so that the internal byte slice of uuid references a new backing array of only 36 bytes:

```go
func (s store) handleLog(log string) error {
    if len(log) < 36 {
        return errors.New("log is not correctly formatted")
    }
    uuid := string([]byte(log[:36])) // Performs a []byte and then a string conversion
    s.store(uuid)
    // Do something
}
```

The copy is performed by converting the substring into a byte first and then into a string again. By doing this, we prevent a memory leak from occurring. The uuid string is backed by an array consisting of only 36 bytes.

> **NOTE**
>Because a string is mostly a pointer, calling a function to pass a string doesn’t result in a deep copy of the bytes. The copied string will still reference the same backing array.


## Summary #Summary 

- ==Understanding that a rune corresponds to the concept of a Unicode code point and that it can be composed of multiple bytes should be part of the Go developer’s core knowledge to work accurately with strings.==
- ==Iterating on a string with the range operator iterates on the runes with the index corresponding to the starting index of the rune’s byte sequence. To access a specific rune index (such as the third rune), convert the string into a rune.==
- ==`strings.TrimRight/strings.TrimLeft` removes all the trailing/leading runes contained in a given set, whereas `strings.TrimSuffix/strings.TrimPrefix` returns a string without a provided suffix/prefix.==
- ==Concatenating a list of strings should be done with `strings.Builder` to prevent allocating a new string during each iteration.==
- ==Remembering that the bytes package offers the same operations as the strings package can help avoid extra byte/string conversions.==
- ==Using copies instead of substrings can prevent memory leaks, as the string returned by a substring operation will be backed by the same byte array.==

# 6 Functions and methods

A _function_ wraps a sequence of statements into a unit that can be called elsewhere. It can take some input(s) and produces some output(s). On the other hand, a _method_ is a function attached to a given type. The attached type is called a _receiver_ and can be a pointer or a value.

## 6.1 #42: Not knowing which type of receiver to use #Mistake 

in many contexts, using a value or pointer receiver should be dictated not by performance but rather by other conditions

In Go, we can attach either a value or a pointer receiver to a method. With a value receiver Go makes a copy of the value and passes it to the method. Any changes to the object remain local to the method. The original object remains unchanged.

```GO
type customer struct {
    balance float64
}
 
func (c customer) add(v float64) { // Value receiver
    c.balance += v
}
 
func main() {
    c := customer{balance: 100.}
    c.add(50.)
    fmt.Printf("balance: %.2f\n", c.balance) // The customer balance remains unchanged.
}
```

output:

```go
100.00
```

with a pointer receiver, Go passes the address of an object to the method. Intrinsically, it remains a copy, but we only copy a pointer, not the object itself Any modifications to the receiver are done on the original object.

```go
type customer struct {
    balance float64
}
 
func (c *customer) add(operation float64) { // Pointer receiver
    c.balance += operation
}
 
func main() {
    c := customer{balance: 100.0}
    c.add(50.0)
    fmt.Printf("balance: %.2f\n", c.balance) // The customer balance is updated.
}
```

with a pointer receiver, Go passes the address of an object to the method. Intrinsically, it remains a copy, but we only copy a pointer, not the object itself. Any modifications to the receiver are done on the original object.

```go
type customer struct {
    balance float64
}
 
func (c *customer) add(operation float64) { // Pointer receiver
    c.balance += operation
}
 
func main() {
    c := customer{balance: 100.0}
    c.add(50.0)
    fmt.Printf("balance: %.2f\n", c.balance) // The customer balance is updated.
}
```

Because we use a pointer receiver, incrementing the balance mutates the balance field of the original customer struct:

```go
150.00
```

A receiver _must_ be a pointer

- If the method needs to mutate the receiver. This rule is also valid if the receiver is a slice and a method needs to append elements:

```go
type slice []int
 
func (s *slice) add(element int) {
    *s = append(*s, element)
}
```

- If the method receiver contains a field that cannot be copied

A receiver _should_ be a pointer

- If the receiver is a large object. Using a pointer can make the call more efficient, as doing so prevents making an extensive copy. When in doubt about how large is large, benchmarking can be the solution; it’s pretty much impossible to state a specific size, because it depends on many factors.

A receiver _must_ be a value

- If we have to enforce a receiver’s immutability.
- If the receiver is a map, function, or channel. Otherwise, a compilation error occurs.

A receiver _should_ be a value

- If the receiver is a slice that doesn’t have to be mutated.
- If the receiver is a small array or struct that is naturally a value type without mutable fields, such as `time.Time.`
- If the receiver is a basic type such as int, float64, or string.

```go
type customer struct {
    data *data // balance isn’t part of the customer struct directly but is in a struct referenced by a pointer field.
}
 
type data struct {
    balance float64
}
 
func (c customer) add(operation float64) { // Uses a value receiver
    c.data.balance += operation
}
 
func main() {
    c := customer{data: &data{
        balance: 100,
    }}
    c.add(50.)
    fmt.Printf("balance: %.2f\n", c.data.balance)
}
```

Even though the receiver is a value, calling add changes the actual balance in the end:

output: 

```go
150.00
```

In this case, we don’t need the receiver to be a pointer to mutate balance.

>**MIXING RECEIVER TYPES**
>Are we allowed to mix receiver types, such as a struct containing multiple methods, some of which have pointer receivers and others of which have value receivers?
>Consequently, mixing receiver types should be avoided in general but is not forbidden in 100% of cases.

By default, we can choose to go with a value receiver unless there’s a good reason not to do so. In doubt, we should use a pointer receiver.

## 6.2 #43: Never using named result parameters #Mistake 

When we return parameters in a function or a method, we can attach names to these parameters and use them as regular variables. When a result parameter is named, it’s initialized to its zero value when the function/method begins. With named result parameters, we can also call a naked return statement (without arguments).

```go
func f(a int) (b int) { // Names the int result parameter b
    b = a
    return // Returns the current value of b
}
```


When is it recommended that we use named result parameters?

```go
type locator interface {
    getCoordinates(address string) (float32, float32, error)
}
```

Because this interface is unexported, documentation isn’t mandatory. we have to check the implementation to understand the results.
In that case, we should probably use named result parameters to make the code easier to read:

```go
type locator interface {
    getCoordinates(address string) (lat, lng float32, err error)
}
```

Should we also use named result parameters as part of the implementation itself?

```go
func (l loc) getCoordinates(address string) (
    lat, lng float32, err error) {
    // ...
}
```

In this specific case, having an expressive method signature can also help code readers.

>**NOTE**
>If we need to return multiple results of the same type, we can also think about creating an ad hoc struct with meaningful field names. However, this isn’t always possible: for example, when satisfying an existing interface that we can’t update.

naming the error parameter err isn’t helpful and doesn’t help readers. In this case, we should favor not using named result parameters.
So, when to use named result parameters depends on the context. In most cases, if it’s not clear whether using them makes our code more readable, we shouldn’t use named result parameters.

One note regarding naked returns (returns without arguments): they are considered acceptable in short functions; otherwise, they can harm readability because the reader must remember the outputs throughout the entire function. We should also be consistent within the scope of a function, using either only naked returns or only returns with arguments.

 In most cases, using named result parameters in the context of an interface definition can increase readability without leading to any side effects.
 
In some cases, named result parameters can also increase readability: for example, if two parameters have the same type. In other cases, they can also be used for convenience. Therefore, we should use named result parameters sparingly when there’s a clear benefit.

## 6.3 #44: Unintended side effects with named result parameters #Mistake 

as these result parameters are initialized to their zero value, using them can sometimes lead to subtle bugs if we’re not careful enough.

```go
func (l loc) getCoordinates(ctx context.Context, address string) (
    lat, lng float32, err error) {
    isValid := l.validateAddress(address)
    if !isValid {
        return 0, 0, errors.New("invalid address")
    }
 
    if ctx.Err() != nil { // Checks whether the context was canceled or the deadline has passed
        return 0, 0, err
    }
 
    // Get and return coordinates
}
```

the error returned in the if ctx.Err() != nil scope is err. But we haven’t assigned any value to the err variable. It’s still assigned to the zero value of an error type: nil. Hence, this code will always return a nil error.

One possible fix is to assign `ctx.Err()` to err like so:

```go
if err := ctx.Err(); err != nil {
    return 0, 0, err
}
```

 
 >**USING A NAKED RETURN STATEMENT**
>Another option is to use a naked return statement:
> 

```go
if err = ctx.Err(); err != nil {
    return
}
```

> However, doing so would break the rule stating that we shouldn’t mix naked returns and returns with arguments. Remember that using named result parameters doesn’t necessarily mean using naked returns. Sometimes we can just use named result parameters to make a signature clearer.


must recall that each parameter is initialized to its zero value. this can lead to subtle bugs that aren’t always straightforward to spot while reading code. Therefore, let’s remain cautious when using named result parameters, to avoid potential side effects.

## 6.4 #45: Returning a nil receiver #Mistake 

This mistake is probably one of the most widespread in Go because it may be considered counterintuitive

```go
type MultiError struct {
    errs []string
}
 
func (m *MultiError) Add(err error) { // Adds an error
    m.errs = append(m.errs, err.Error())
}
 
func (m *MultiError) Error() string { // Implements the error interface
    return strings.Join(m.errs, ";")
}
```

MultiError satisfies the error interface because [](https://livebook.manning.com/book/100-go-mistakes-and-how-to-avoid-them/chapter-6/)it implements Error() string. Meanwhile, it exposes an Add method to append an error. Using this struct, we can implement a Customer.Validate method in the following manner to check the customer’s age and name. If the sanity checks are OK, we want to return a nil error:

```go
func (c Customer) Validate() error {
    var m *MultiError // Instantiates an empty *MultiError
 
    if c.Age < 0 {
        m = &MultiError{}
        m.Add(errors.New("age is negative")) // Appends an error if the age is negative
    }
    if c.Name == "" {
        if m == nil {
            m = &MultiError{}
        }
        m.Add(errors.New("name is nil")) // Appends an error if the name is nil
    }
 
    return m
}
```

In this implementation, m is initialized to the zero value of *MultiError: hence, nil. When a sanity check fails, we allocate a new MultiError if needed and then append an error. In the end, we return m, which can be either a nil pointer or a pointer to a MultiError struct, depending on the checks.

```go
customer := Customer{Age: 33, Name: "John"}
if err := customer.Validate(); err != nil {
    log.Fatalf("customer is invalid: %v", err)
}
```

the output:

```go
2021/05/08 13:47:28 customer is invalid: <nil>
```

In Go, we have to know that a pointer receiver can be nil.

```go
type Foo struct{}
 
func (foo *Foo) Bar() string {
    return "bar"
}
 
func main() {
    var foo *Foo
    fmt.Println(foo.Bar()) // foo is nill
}
```

foo is initialized to the zero value of a pointer: nil. But this code compiles, and it prints bar if we run it. A nil pointer is a valid receiver.

But why is this the case? In Go, a method is just syntactic sugar for a function whose first parameter is the receiver. Hence, the Bar method we’ve seen is similar to this function:

```go
func Bar(foo *Foo) string {
    return "bar"
}
```

passing a nil pointer to a function is valid. Therefore, using a nil pointer as a receiver is also valid.

**in Go, an interface is a dispatch wrapper**

![[Pasted image 20240103122738.png]]

The easiest solution is to return m only if it’s not nil:

```go
func (c Customer) Validate() error {
    var m *MultiError
 
    if c.Age < 0 {
        // ...
    }
    if c.Name == "" {
        // ...
    }
 
    if m != nil {
        return m // Returns m only if there was at least one error
    }
    return nil // Otherwise, returns nil
}
```

in Go, having a nil receiver is allowed, and an interface converted from a nil pointer isn’t a nil interface. For that reason, when we have to return an interface, we should return not a nil pointer but a nil value directly. Generally, having a nil pointer isn’t a desirable state and means a probable bug.

## 6.5 #46: Using a filename as a function input #Mistake 

When creating a new function that needs to read a file, passing a filename isn’t considered a best practice and can have negative effects, such as making unit tests harder to write.

```go
func countEmptyLinesInFile(filename string) (int, error) {
    file, err := os.Open(filename) // Opens filename
    if err != nil {
        return 0, err
    }
    // Handle file closure
 
    scanner := bufio.NewScanner(file) // Creates a scanner from the *os.File variable that will split the input per line
    for scanner.Scan() { // Iterates over each line
        // ...
    }
}
```

what’s the problem?

Let’s say we want to implement unit tests to cover the following cases:

- A nominal case
- An empty file
- A file containing only empty lines

Each unit test will require creating a file in our Go project. The more complex the function is, the more cases we may want to add, and the more files we will create.

Furthermore, this function isn’t reusable.

```go
func countEmptyLinesInHTTPRequest(request http.Request) (int, error) {
    scanner := bufio.NewScanner(request.Body)
    // Copy the same logic
}
```

One way to overcome these limitations might be to make the function accept a *bufio.Scanner (the output returned by bufio.NewScanner). Both functions have the same logic from the moment we create the scanner variable, so this approach would work.

```go
func countEmptyLines(reader io.Reader) (int, error) { // Accepts an io.Reader as the input
    scanner := bufio.NewScanner(reader) // Accepts an io.Reader as the input
    for scanner.Scan() {
        // ...
    }
}
```

What are the benefits of this approach? First, this function abstracts the data source. Is it a file? An HTTP request? A socket input? It’s not important for the function

Another benefit is related to testing. We mentioned that creating one file per test case could quickly become cumbersome. Now that `countEmptyLines` accepts an io.Reader, we can implement unit tests by creating an io.Reader from a string:

```go
func TestCountEmptyLines(t *testing.T) {
    emptyLines, err := countEmptyLines(strings.NewReader( // Passes an io.Reader from a string
        `foo
            bar
 
            baz
            `))
    // Test logic
}
```

Accepting a filename as a function input to read from a file should, in most cases, be considered a code smell (except in specific functions such as `os.Open`).

It also reduces the reusability of a function Using the io.Reader interface abstracts the data source.


## 6.6 #47: Ignoring how defer arguments and receivers are evaluated #Mistake 

the defer statement delays a call’s execution until the surrounding function returns

### 6.6.1 Argument evaluation

A function needs to call two functions foo and bar. Meanwhile, it has to handle a status regarding execution:

- `StatusSuccess` if both foo and bar return no errors
- `StatusErrorFoo` if foo returns an error
- `StatusErrorBar` if bar returns an error

for example, to notify another goroutine and to increment counters. To avoid repeating these calls before every return statement, we will use defer.

```go
const (
    StatusSuccess  = "success"
    StatusErrorFoo = "error_foo"
    StatusErrorBar = "error_bar"
)
 
func f() error {
    var status string
    defer notify(status) // Defers the call to notify
    defer incrementCounter(status) // Defers the call to incrementCounter
 
    if err := foo(); err != nil {
        status = StatusErrorFoo // Sets the status to error foo
        return err
    }
 
    if err := bar(); err != nil {
        status = StatusErrorBar // Sets the status to error bar
        return err
    }
 
    status = StatusSuccess // Sets the status to success
    return nil
}
```

First we declare a status variable. Then we defer the calls to notify and incrementCounter using defer. Throughout this function, and depending on the execution path, we update status accordingly.

However, if we give this function a try, we see that regardless of the execution path, notify and `incrementCounter` are always called with the same status: an empty string. How is this possible?

the arguments are evaluated _right away_, not once the surrounding function returns. In our example, we call notify(status) and `incrementCounter`(status) as defer functions. Therefore, Go will delay these calls to be executed once f returns with the current value of status at the stage we used defer, hence passing an empty string. How can we solve this problem if we want to keep using defer? There are two leading solutions.

The first solution is to pass a string pointer to the defer functions:

```go
func f() error {
    var status string
    defer notify(&status) // Passes a string pointer to notify
    defer incrementCounter(&status) // Passes a string pointer to incrementCounter
 
    // The rest of the function is unchanged
    if err := foo(); err != nil {
        status = StatusErrorFoo
        return err
    }
 
    if err := bar(); err != nil {
        status = StatusErrorBar
        return err
    }
 
    status = StatusSuccess
    return nil
}
```

Why does this approach work?

Using defer evaluates the arguments right away: here, the address of status. Yes, status itself is modified throughout the function, but its address remains constant, regardless of the assignments. Hence, if notify or incrementCounter uses the value referenced by the string pointer, it will work as expected. But this solution requires changing the signature of the two functions, which may not always be possible.

There’s another solution: calling a closure as a defer statement. As a reminder, a closure is an anonymous function value that references variables from outside its body. The arguments passed to a defer function are evaluated right away. But we must know that the variables referenced by a defer closure are evaluated _during_ the closure execution

```go
func main() {
    i := 0
    j := 0
    defer func(i int) { // Calls as a defer function a closure that accepts an integer as an input
        fmt.Println(i, j) // i is the function input, and j is an external variable.
    }(i) // Passes i to the closure (evaluated right away)
    i++
    j++
}
```

### 6.6.2 Pointer and value receivers

“Not knowing which type of receiver to use,” we said that a receiver can be either a value or a pointer. The same logic related to argument evaluation applies when we use defer on a method: the receiver is also evaluated immediately.

```go
func main() {
    s := Struct{id: "foo"}
    defer s.print() // s is evaluated immediately.
    s.id = "bar" // Updates s.id (not visible)
}
 
type Struct struct {
    id string
}
 
func (s Struct) print() {
    fmt.Println(s.id) // foo
}
```

As with arguments, calling defer makes the receiver be evaluated immediately. Hence, defer delays the method’s execution with a struct that contains an id field equal to foo. Therefore, this example prints foo.
the potential changes to the receiver after the call to defer are visible:

```go
func main() {
    s := &Struct{id: "foo"}
    defer s.print() // s is a pointer, so it is evaluated immediately but may reference another variable when the defer method is executed.
    s.id = "bar" // Updates s.id (visible)
}
 
type Struct struct {
    id string
}
 
func (s *Struct) print() {
    fmt.Println(s.id) // bar
}
```

The s receiver is also evaluated immediately. However, calling the method leads to copying the pointer receiver. Hence, the changes made to the struct referenced by the pointer are visible.

In summary, when we call defer on a function or method, the call’s arguments are evaluated immediately.

## Summary

- ==The decision whether to use a value or a pointer receiver should be made based on factors such as the type, whether it has to be mutated, whether it contains a field that can’t be copied, and how large the object is. When in doubt, use a pointer receiver.==
- ==Using named result parameters can be an efficient way to improve the readability of a function/method, especially if multiple result parameters have the same type. In some cases, this approach can also be convenient because named result parameters are initialized to their zero value. But be cautious about potential side effects.==
- ==When returning an interface, be cautious about returning not a nil pointer but an explicit nil value. Otherwise, unintended consequences may result because the caller will receive a non-nil value.==
- ==Designing functions to receive io.Reader types instead of filenames improves the reusability of a function and makes testing easier.==
- ==Passing a pointer to a defer function and wrapping a call inside a closure are two possible solutions to overcome the immediate evaluation of arguments and receivers.==


# 7 Error management

## 7.1 #48: Panicking #Mistake 

In Go, errors are usually managed by functions or methods that return an error type as the last parameter.
In Go, panic is a built-in function that stops the ordinary flow:

```go
func main() {
    fmt.Println("a")
    panic("foo")
    fmt.Println("b")
}
```

This code prints a and then stops before printing b:

```go
a
panic: foo
 
goroutine 1 [running]:
main.main()
        main.go:7 +0xb3
```

Once a panic is triggered, it continues up the call stack until either the current goroutine has returned or panic is caught with recover:

```go
func main() {
    defer func() { // Calls recover within a defer closure
        if r := recover(); r != nil {
            fmt.Println("recover", r)
        }
    }()
 
    f() // Calls f, which panics. This panic is caught by the previous recover.
}
 
func f() {
    fmt.Println("a")
    panic("foo")
    fmt.Println("b")
}
```

the output: 

```go
a
recover foo
```

calling recover() to capture a goroutine panicking is only useful inside a defer function; otherwise, the function would return nil and have no other effect. This is because defer functions are also executed when the surrounding function panics. 

when is it appropriate to panic? In Go, panic is used to signal genuinely exceptional conditions, such as a programmer error. 
Another use case in which to panic is when our application requires a dependency but fails to initialize it

Panicking in Go should be used sparingly. We have seen two prominent cases, one to signal a programmer error and another where our application fails to create a mandatory dependency. Hence, there are exceptional conditions that lead us to stop the application. In most other cases, error management should be done with a function that returns a proper error type as the last return argument.

## 7.2  #49: Ignoring when to wrap an error #Mistake 

Error wrapping is about wrapping or packing an error inside a wrapper container that also makes the source error available (see figure 7.1). In general, the two main use cases for error wrapping are the following:

- ==Adding additional context to an error==
- ==Marking an error as a specific error==

![[Pasted image 20240103132143.png]]

Regarding adding context, let’s consider the following example. We receive a request from a specific user to access a database resource, but we get a “permission denied” error during the query. For debugging purposes, if the error is eventually logged, we want to add extra context. In this case, we can wrap the error to indicate who the user is and what resource is being accessed

Now let’s say that instead of adding context, we want to mark the error. For example, we want to implement an HTTP handler that checks whether all the errors received while calling functions are of a Forbidden type so we can return a 403 status code. In that case, we can wrap this error inside Forbidden

In both cases, the source error remains available. Hence, a caller can also handle an error by unwrapping it and checking the source error.

```go
func Foo() error {
    err := bar()
    if err != nil {
        // ? // How do we return the error?
    }
    // ...
}
```

The first option is to return this error directly. If we don’t want to mark the error and there’s no helpful context we want to add, this approach is fine:

```go
if err != nil {
    return err
}
```

```go
type BarError struct {
    Err error
}
 
func (b BarError) Error() string {
    return "bar failed:" + b.Err.Error()
}
```

Then, instead of returning err directly, we wrapped the error into a `BarError`

```go
if err != nil {
    return BarError{Err: err}
}
```

The benefit of this option is its flexibility. Because BarError is a custom struct, we can add any additional context if needed. However, being obliged to create a specific error type can quickly become cumbersome if we want to repeat this operation.

To overcome this situation, Go 1.13 introduced the %w directive:

```go
if err != nil {
    return fmt.Errorf("bar failed: %w", err)
}
```

This code wraps the source error to add additional context without having to create another error type

Because the source error remains available, a client can unwrap the parent error and then check whether the source error was of a specific type or value

The last option  is to use the %v directive, instead:

```go
if err != nil {
    return fmt.Errorf("bar failed: %v", err)
}
```

The information about the source of the problem remains available. However, a caller can’t unwrap this error and check whether the source was bar error. So, in a sense, this option is more restrictive than %w. Should we prevent that, since the %w directive has been released? Not necessarily.

Wrapping an error makes the source error available for callers. Hence, it means introducing potential coupling.

To make sure our clients don’t rely on something that we consider implementation details, the error returned should be transformed, not wrapped. In such a case, using %v instead of %w can be the way to go.

> To prevent clients from depending on internal details, it's recommended to transform errors using `%v` instead of `%w` to provide the error message without wrapping it with additional context.


|Option|Extra Context|Marking an Error|Source Error Available|Returning Error Directly|
|---|---|---|---|---|
|Custom Error Type|Possible|Yes|Possible (via a field)|Yes|
|fmt.Errorf with `%w`|Yes|No|Yes|Yes|
|fmt.Errorf with `%v`|Yes|No|No|No|

To summarize, when handling an error, we can decide to wrap it. Wrapping is about adding additional context to an error and/or marking an error as a specific type. If we need to mark an error, we should create a custom error type. However, if we just want to add extra context, we should use fmt.Errorf with the %w directive as it doesn’t require creating a new error type. Yet, error wrapping creates potential coupling as it makes the source error available for the caller. If we want to prevent it, we shouldn’t use error wrapping but error transformation, for example, using `fmt.Errorf` with the %v directive.

## 7.3 #50: Checking an error type inaccurately #Mistake 

wrap errors using the %w directive. However, when we use that approach, it’s also essential to change our way of checking for a specific error type; otherwise, we may handle errors inaccurately.

```GO
type transientError struct {
    err error
}
 
func (t transientError) Error() string { // Creates a custom transientError
    return fmt.Sprintf("transient error: %v", t.err)
}
 
func getTransactionAmount(transactionID string) (float32, error) {
    if len(transactionID) != 5 {
        return 0, fmt.Errorf("id is invalid: %s",
            transactionID) // Returns a simple error if the transaction ID is invalid
    }
 
    amount, err := getTransactionAmountFromDB(transactionID)
    if err != nil {
        return 0, transientError{err: err} // Returns a transientError if we fail to query the DB
    }
    return amount, nil
}
```


```go
func handler(w http.ResponseWriter, r *http.Request) {
    transactionID := r.URL.Query().Get("transaction") // Extracts the transaction ID
 
    amount, err := getTransactionAmount(transactionID) // Calls getTransactionAmount that contains all the logic
    if err != nil {
        switch err := err.(type) { // Checks the error type and returns a 503 if the error is a transient one; otherwise, a 400
        case transientError:
            http.Error(w, err.Error(), http.StatusServiceUnavailable)
        default:
            http.Error(w, err.Error(), http.StatusBadRequest)
        }
        return
    }
 
    // Write response
}
```


```go
func getTransactionAmount(transactionID string) (float32, error) {
    // Check transaction ID validity
 
    amount, err := getTransactionAmountFromDB(transactionID)
    if err != nil {
        return 0, fmt.Errorf("failed to get transaction %s: %w",
            transactionID, err) // Wraps the error instead of returning a transientError directly
    }
    return amount, nil
}
 
func getTransactionAmountFromDB(transactionID string) (float32, error) {
    // ...
    if err != nil {
        return 0, transientError{err: err} // This function now returns the transientError.
    }
    // ...
}
```

If we run this code, it always returns a 400 regardless of the error case, so the case Transient error will never be hit. How can we explain this behavior?

What `getTransactionAmount` returns isn’t a `transientError` directly: it’s an error wrapping `transientError`. Therefore case transientError is now false.

For that exact purpose, Go 1.13 came with a directive to wrap an error and a way to check whether the wrapped error is of a certain type with `errors.As`. This function recursively unwraps an error and returns true if an error in the chain matches the expected type.

```go
func handler(w http.ResponseWriter, r *http.Request) {
    // Get transaction ID
 
    amount, err := getTransactionAmount(transactionID)
    if err != nil {
        if errors.As(err, &transientError{}) { // Calls errors.As by providing a pointer to transientError
            http.Error(w, err.Error(),
                http.StatusServiceUnavailable) // Returns a 503 if the error is transient
        } else {
            http.Error(w, err.Error(),
                http.StatusBadRequest) // Else returns a 400
        }
        return
    }
 
    // Write response
}
```

In summary, if we rely on Go 1.13 error wrapping, we must use errors.As to check whether an error is a specific type. This way, regardless of whether the error is returned directly by the function we call or wrapped inside an error, `errors.As` will be able to recursively unwrap our main error and see if one of the errors is a specific type.

## 7.4 #51: Checking an error value inaccurately #Mistake 

A sentinel error is an error defined as a global variable:

```go
import "errors"
 
var ErrFoo = errors.New("foo")
```

In general, the convention is to start with Err followed by the error type: here, `ErrFoo`. A sentinel error conveys an _expected_ error.

the general principle behind sentinel errors. They convey an expected error that clients will expect to check. Therefore, as general guidelines,

- Expected errors should be designed as error values (sentinel errors): var `ErrFoo` = `errors.New("foo")`.
- Unexpected errors should be designed as error types: type `BarError` struct { ... }, with `BarError` implementing the error interface.

How can we compare an error to a specific value? By using the == operator:

```go
err := query()
if err != nil {
    if err == sql.ErrNoRows { // Checks error against the sql.ErrNoRows variable
        // ...
    } else {
        // ...
    }
}
```

Go 1.13 provides an answer. We have seen how `errors.As` is used to check an error against a type. With error values, we can use its counterpart: `errors.Is`.

```go
err := query()
if err != nil {
    if errors.Is(err, sql.ErrNoRows) {
        // ...
    } else {
        // ...
    }
}
```

Using `errors.Is` instead of the == operator allows the comparison to work even if the error is wrapped using %w.

In summary, if we use error wrapping in our application with the %w directive and` fmt.Errorf`, checking an error against a specific value should be done using `errors.Is` instead of . Thus, even if the sentinel error is wrapped, `errors.Is` can recursively unwrap it and compare each error in the chain against the provided value.

## 7.5 #52: Handling an error twice #Mistake 

Handling an error multiple times is a mistake made frequently by developers, not specifically in Go.

```go
func GetRoute(srcLat, srcLng, dstLat, dstLng float32) (Route, error) {
    err := validateCoordinates(srcLat, srcLng)
    if err != nil {
        log.Println("failed to validate source coordinates")
        return Route{}, err
    }
 
    err = validateCoordinates(dstLat, dstLng)
    if err != nil {
        log.Println("failed to validate target coordinates")
        return Route{}, err
    }
 
    return getRoute(srcLat, srcLng, dstLat, dstLng)  // Logs and returns the error overall !!
}
 
func validateCoordinates(lat, lng float32) error {
    if lat > 90.0 || lat < -90.0 {
        log.Printf("invalid latitude: %f", lat)
        return fmt.Errorf("invalid latitude: %f", lat)
    }
    if lng > 180.0 || lng < -180.0 {
        log.Printf("invalid longitude: %f", lng)
        return fmt.Errorf("invalid longitude: %f", lng)
    }
    return nil
}
```

What’s the problem with this code? First, in validateCoordinates, it is cumbersome to repeat the invalid latitude or invalid longitude error messages in both logging and the error returned. Also, if we run the code with an invalid latitude, for example, it will log the following lines:

```go
2021/06/01 20:35:12 invalid latitude: 200.000000
2021/06/01 20:35:12 failed to validate source coordinates
```

Having two log lines for a single error is a problem. Why? Because it makes debugging harder.

==As a rule of thumb, an error should be handled only once. Logging an error is handling an error, and so is returning an error. Hence, we should either log or return an error, never both.==

```go
func GetRoute(srcLat, srcLng, dstLat, dstLng float32) (Route, error) {
    err := validateCoordinates(srcLat, srcLng)
    if err != nil {
        return Route{}, err
    }
 
    err = validateCoordinates(dstLat, dstLng)
    if err != nil {
        return Route{}, err
    }
 
    return getRoute(srcLat, srcLng, dstLat, dstLng) // Only returns an error over all !!
}
 
func validateCoordinates(lat, lng float32) error {
    if lat > 90.0 || lat < -90.0 {
        return fmt.Errorf("invalid latitude: %f", lat)
    }
    if lng > 180.0 || lng < -180.0 {
        return fmt.Errorf("invalid longitude: %f", lng)
    }
    return nil
}
```

Here, we lose this information, so we need to add additional context to the error.

```go
func GetRoute(srcLat, srcLng, dstLat, dstLng float32) (Route, error) {
    err := validateCoordinates(srcLat, srcLng)
    if err != nil {
        return Route{},
            fmt.Errorf("failed to validate source coordinates: %w",
                err)
    }
 
    err = validateCoordinates(dstLat, dstLng)
	if err != nil {  // Returns a wrapper error
        return Route{},
            fmt.Errorf("failed to validate target coordinates: %w",
                err)
    }
 
    return getRoute(srcLat, srcLng, dstLat, dstLng)
}
```

Handling an error should be done only once. Hence, we should either log or return an error. Using error wrapping is the most convenient approach as it allows us to propagate the source error and add context to an error.

## 7.6 #53: Not handling an error #Mistake 

```go
func f() {
    // ...
    notify() // Error handling is omitted.
}
 
func notify() error {
    // ...
}
```

Because we want to ignore the error, in this example, we just call notify without assigning its output to a classic err variable. There’s nothing wrong with this code from a functional standpoint: it compiles and runs as expected.

However, from a maintainability perspective, the code can lead to some issues. Let’s consider a new reader looking at it. This reader notices that notify returns an error but that the error isn’t handled by the parent function. How can they guess whether or not handling the error was intentional? How can they know whether the previous developer forgot to handle it or did it purposely?

For these reasons, when we want to ignore an error in Go, there’s only one way to write it:

```go
_ = notify()
```

Instead of not assigning the error to a variable, we assign it to the blank identifier. In terms of compilation and run time, this approach doesn’t change anything compared to the first piece of code. But this new version makes explicit that we aren’t interested in the error.

Ignoring an error in Go should be the exception. In many cases, we may still favor logging them, even at a low log level.

## 7.7 #54: Not handling defer errors #Mistake 

Not handling errors in defer statements is a mistake that’s frequently made by Go developers.

```GO
const query = "..."
 
func getBalance(db *sql.DB, clientID string) (
    float32, error) {
    rows, err := db.Query(query, clientID)
    if err != nil {
        return 0, err
    }
    defer rows.Close() // Defers the call to rows.Close()
 
    // Use rows
}
```

```go
type Closer interface {
    Close() error
}
```

in this case, the error returned by the defer call is ignored:

```go
defer rows.Close()
```

if we don’t want to handle the error, we should ignore it explicitly using the blank identifier:

```go
defer func() { _ = rows.Close() }()
```

This version is more verbose but is better from a maintainability perspective as we explicitly mark that we are ignoring the error.

But in such a case, instead of blindly ignoring all errors from defer calls, we should ask ourselves whether that is the best approach.

Most likely, a better option would be to log a message:

```go
defer func() {
    err := rows.Close()
    if err != nil {
        log.Printf("failed to close rows: %v", err)
    }
}()
```

```go
defer func() {
    err := rows.Close()
    if err != nil {
        return err
    }
}()
```

This implementation doesn’t compile. Indeed, the return statement is associated with the anonymous `func()` function, not `getBalance`.

If we want to tie the error returned by `getBalance` to the error caught in the defer call, we must use named result parameters. Let’s write the first version:

```go
func getBalance(db *sql.DB, clientID string) (
    balance float32, err error) {
    rows, err := db.Query(query, clientID)
    if err != nil {
        return 0, err
    }
    defer func() {
        err = rows.Close() // Assigns the error to the output named parameter
    }()
 
    if rows.Next() {
        err := rows.Scan(&balance)
        if err != nil {
            return 0, err
        }
        return balance, nil
    }
    // ...
}
```

final implementation of the anonymous function:

```go
defer func() {
    closeErr := rows.Close() // Assigns the rows.Close error to another variable
    if err != nil { // If err was already not nil, we prioritize it.
        if closeErr != nil {
            log.Printf("failed to close rows: %v", err)
        }
        return
    }
    err = closeErr // If err was already not nil, we prioritize it.
}()
```

## Summary #Summary 

- ==Using panic is an option to deal with errors in Go. However, it should only be used sparingly in unrecoverable conditions: for example, to signal a programmer error or when you fail to load a mandatory dependency.==
- ==Wrapping an error allows you to mark an error and/or provide additional context. However, error wrapping creates potential coupling as it makes the source error available for the caller. If you want to prevent that, don’t use error wrapping.==
- ==If you use Go 1.13 error wrapping with the %w directive and `fmt.Errorf`, comparing an error against a type or a value has to be done using `errors.As` or `errors.Is`, respectively. Otherwise, if the returned error you want to check is wrapped, it will fail the checks.==
- ==To convey an expected error, use error sentinels (error values). An unexpected error should be a specific error type.==
- ==In most situations, an error should be handled only once. Logging an error is handling an error. Therefore, you have to choose between logging or returning an error. In many cases, error wrapping is the solution as it allows you to provide additional context to an error and return the source error.==
- ==Ignoring an error, whether during a function call or in a defer function, should be done explicitly using the blank identifier. Otherwise, future readers may be confused about whether it was intentional or a miss.==
- ==In many cases, you shouldn’t ignore an error returned by a defer function. Either handle it directly or propagate it to the caller, depending on the context. If you want to ignore it, use the blank identifier.==


# 8 Concurrency: Foundations

modern CPUs are designed with multiple cores and hyperthreading (multiple logical cores on the same physical core). Therefore, to leverage these architectures, concurrency has become critical for software developers.


## 8.1 #55: Mixing up concurrency and parallelism #Mistake 

the concepts of concurrency and parallelism in the context of a coffee shop scenario. The coffee shop serves as a metaphor for a system with different tasks that can be performed concurrently or in parallel to improve efficiency.

1. **Parallelism in Serving Customers:**
    
    - Initially, the coffee shop has one waiter and one coffee machine. To speed up the process, a second waiter and coffee machine are introduced, showcasing parallelism.
    - This parallel implementation involves duplicating components to serve customers faster.
2. **Concurrency with Task Separation:**
    
    - Another approach is introduced where the waiter's role is split into accepting orders and grinding coffee beans, leading to concurrency.
    - A queue is introduced for customers waiting for their orders, resembling a structure seen in popular coffee chains like Starbucks.
3. **Increasing Throughput with Parallelism:**
    
    - To increase throughput, another waiter is hired specifically for grinding coffee beans, adding parallelism to the order preparation step.
    - This maintains the three-step design but introduces parallel threads for a specific task.
4. **Addressing Contention with Parallel Coffee Machines:**
    
    - If contention arises due to a single coffee machine slowing down the process, more coffee machines are added to reduce contention and increase parallelism.
5. **Concurrency Enables Parallelism:**
    
    - The author emphasizes that concurrency provides the structure for solving problems with parts that can be parallelized.
    - Concurrency is about dealing with many things simultaneously, while parallelism is about executing many things simultaneously.

==The overall takeaway is that understanding the distinction between concurrency and parallelism is crucial for effective software development. Concurrency focuses on structuring tasks, enabling parallelism to be applied at different levels to enhance system performance.==


## 8.2 #56: Thinking concurrency is always faster #Mistake 


A misconception among many developers is believing that a concurrent solution is always faster than a sequential one. This couldn’t be more wrong. The overall performance of a solution depends on many factors, such as the efficiency of our structure (concurrency), which parts can be tackled in parallel, and the level of contention among the computation units

### 8.2.1 Go scheduling

A thread is the smallest unit of processing that an OS can perform. If a process wants to execute multiple actions simultaneously, it spins up multiple threads. These threads can be

- ==_Concurrent_—Two or more threads can start, run, and complete in overlapping time periods, like the waiter thread and the coffee machine thread in the previous section.==
- ==_Parallel_—The same task can be executed multiple times at once, like multiple waiter threads.==

==The OS is responsible for scheduling the thread’s processes optimally so that==

- ==All the threads can consume CPU cycles without being starved for too much time.==
- ==The workload is distributed as evenly as possible among the different CPU cores.==

##### NOTE

>The word _thread_ can also have a different meaning at a CPU level. Each physical core can be composed of multiple logical cores (the concept of hyperthreading), and a logical core is also called a thread. In this section, when we use the word _thread_, we mean the unit of processing, not a logical core.

A CPU core executes different threads. When it switches from one thread to another, it executes an operation called _context switching_. The active thread consuming CPU cycles was in an _executing_ state and moves to a _runnable_ state, meaning it’s ready to be executed pending an available core. Context switching is considered an expensive operation because the OS needs to save the current execution state of a thread before the switch (such as the current register values).

##### NOTE

> Context switching a goroutine versus a thread is about 80% to 90% faster, depending on the architecture.

Go scheduler uses the following terminology

- ==_G_—Goroutine==
- ==_M_—OS thread (stands for _machine_)==
- ==_P_—CPU core (stands for _processor_)==

 Each OS thread (M) is assigned to a CPU core (P) by the OS scheduler. Then, each goroutine (G) runs on an M. The GOMAXPROCS variable defines the limit of Ms in charge of executing user-level code simultaneously. But if a thread is blocked in a system call (for example, I/O), the scheduler can spin up more Ms. As of Go 1.5, GOMAXPROCS is by default equal to the number of available CPU cores.

A goroutine has a simpler lifecycle than an OS thread. It can be doing one of the following:

- ==_Executing_—The goroutine is scheduled on an M and executing its instructions.==
- ==_Runnable_—The goroutine is waiting to be in an executing state.==
- ==_Waiting_—The goroutine is stopped and pending something completing, such as a system call or a synchronization operation (such as acquiring a mutex).==

when a goroutine is created but cannot be executed yet; for example, all the other Ms are already executing a G. In this scenario, what will the Go runtime do about it? The answer is queuing. The Go runtime handles two kinds of queues: one local queue per P and a global queue shared among all the Ps.

the scheduling implementation in pseudocode (see [http://mng.bz/lxY8](http://mng.bz/lxY8)):

```go
runtime.schedule() {
    // Only 1/61 of the time, check the global runnable queue for a G.
    // If not found, check the local queue.
    // If not found,
    //     Try to steal from other Ps.
    //     If not, check the global runnable queue.
    //     If not found, poll network.
}
```

Every sixty-first execution, the Go scheduler will check whether goroutines from the global queue are available. If not, it will check its local queue. Meanwhile, if both the global and local queues are empty, the Go scheduler can pick up goroutines from other local queues. This principle in scheduling is called _work stealing_, and it allows an underutilized processor to actively look for another processor’s goroutines and _steal_ some.

### 8.2.2 Parallel merge sort

The merge sort algorithm works by breaking a list repeatedly into two sublists until each sublist consists of a single element and then merging these sublists so that the result is a sorted list . Each split operation splits the list into two sublists, whereas the merge operation merges two sublists into a sorted list.

![[Pasted image 20240103141305.png]]

```go
func sequentialMergesort(s []int) {
    if len(s) <= 1 {
        return
    }
 
    middle := len(s) / 2
    sequentialMergesort(s[:middle]) // First half
    sequentialMergesort(s[middle:]) // Second half
    merge(s, middle) // Merges the two halves
}
 
func merge(s []int, middle int) {
    // ...
}
```

This algorithm has a structure that makes it open to concurrency. Indeed, as each `sequentialMergesort` operation works on an independent set of data that doesn’t need to be fully copied we could distribute this workload among the CPU cores by spinning up each `sequentialMergesort` operation in a different goroutine

```go
func parallelMergesortV1(s []int) {
    if len(s) <= 1 {
        return
    }
 
    middle := len(s) / 2
 
    var wg sync.WaitGroup
    wg.Add(2)
 
    go func() { // Spins up the first half of the work in a goroutine
        defer wg.Done()
        parallelMergesortV1(s[:middle])
    }()
 
    go func() { // Spins up the second half of the work in a goroutine
        defer wg.Done()
        parallelMergesortV1(s[middle:])
    }()
 
    wg.Wait()
    merge(s, middle) // Merges the halves
}
```

each half of the workload is handled in a separate goroutine. The parent goroutine waits for both parts by using `sync.WaitGroup`. Hence, we call the Wait method before the merge operation.

```
Benchmark_sequentialMergesort-4       2278993555 ns/op
Benchmark_parallelMergesortV1-4      17525998709 ns/op
```

How is it possible that a parallel version that distributes a workload across four cores is slower than a sequential version running on a single machine?

Because merging a tiny number of elements within a new goroutine isn’t efficient, let’s define a threshold. This threshold will represent how many elements a half should contain in order to be handled in a parallel manner. If the number of elements in the half is fewer than this value, we will handle it sequentially

```go
const max = 2048 // Defines the threshold
 
func parallelMergesortV2(s []int) {
    if len(s) <= 1 {
        return
    }
 
    if len(s) <= max {
        sequentialMergesort(s) // Calls our initial sequential version
    } else { // If bigger than the threshold, keeps the parallel version
        middle := len(s) / 2
 
        var wg sync.WaitGroup
        wg.Add(2)
 
        go func() {
            defer wg.Done()
            parallelMergesortV2(s[:middle])
        }()
 
        go func() {
            defer wg.Done()
            parallelMergesortV2(s[middle:])
        }()
 
        wg.Wait()
        merge(s, middle)
    }
}
```


```
Benchmark_sequentialMergesort-4       2278993555 ns/op
Benchmark_parallelMergesortV1-4      17525998709 ns/op
Benchmark_parallelMergesortV2-4       1313010260 ns/op
```

must keep in mind that concurrency isn’t always faster and shouldn’t be considered the default way to go for all problems. First, it makes things more complex. Also, modern CPUs have become incredibly efficient at executing sequential code and predictable code.

it’s essential to keep these conclusions in mind. If we’re not sure that a parallel version will be faster, the right approach may be to start with a simple sequential version and build from there using profiling  and benchmarks

## 8.3 #57: Being puzzled about when to use channels or mutexes #Mistake 

Go promotes sharing memory by communication, one mistake could be to always force the use of channels, regardless of the use case

in Go: channels are a communication mechanism. Internally, a channel is a pipe we can use to send and receive values and that allows us to _connect_ concurrent goroutines. A channel can be either of the following:

- ==_Unbuffered_—The sender goroutine blocks until the receiver goroutine is ready.==
- ==_Buffered_—The sender goroutine blocks only when the buffer is full.==

In general, parallel goroutines have to _synchronize_: for example, when they need to access or mutate a shared resource such as a slice. Synchronization is enforced with mutexes but not with any channel types (not with buffered channels). Hence, in general, synchronization between parallel goroutines should be achieved via mutexes.

Conversely, in general, concurrent goroutines have to _coordinate and orchestrate_.

Regarding concurrent goroutines, there’s also the case where we want to transfer the ownership of a resource from one step to another

Mutexes and channels have different semantics. Whenever we want to share a state or access a shared resource, mutexes ensure exclusive access to this resource. Conversely, channels are a mechanic for signaling with or without data (chan struct{} or not). Coordination or ownership transfer should be achieved via channels. It’s important to know whether goroutines are parallel or concurrent because, in general, we need mutexes for parallel goroutines and channels for concurrent ones.

## 8.4 #58: Not understanding race problems #Mistake 

### 8.4.1 Data races vs. race conditions

A data race occurs when two or more goroutines simultaneously access the same memory location and at least one is writing.

```go
i := 0
 
go func() {
    i++
}()
 
go func() {
    i++
}()
```

```go
==================
WARNING: DATA RACE
Write at 0x00c00008e000 by goroutine 7:
  main.main.func2()
 
Previous write at 0x00c00008e000 by goroutine 6:
  main.main.func1()
==================
```

The final value of i is also unpredictable. Sometimes it can be 1, and sometimes 2.

What’s the issue with this code? The i++ statement can be decomposed into three operations:

1. Read i.
2. Increment the value.
3. Write back to i.

If the first goroutine executes and completes before the second one, here’s what happens.

| Goroutine | Operation   | i   |
|------------|-------------|-----|
| 1          | Read        | 0   |
| 1          | Increment   | 0   |
| 1          | Write back  | 1   |
| 2          | Read        | 1   |
| 2          | Increment   | 1   |
| 2          | Write back  | 2   |

| Goroutine | Operation   | i   |
|------------|-------------|-----|
| 1          | Read        | 0   |
| 2          | Read        | 0   |
| 1          | Increment   | 0   |
| 2          | Increment   | 0   |
| 1          | Write back  | 1   |
| 2          | Write back  | 1   |

If two goroutines simultaneously access the same memory location with at least one writing to that memory location, the result can be hazardous.

How can we prevent a data race from happening? The first option is to make the increment operation atomic, meaning it’s done in a single operation.

| Operation       | Goroutine 1                | Goroutine 2                | i   |
|-----------------|---------------------------|---------------------------|-----|
| Initial State   |                           |                           |  0  |
| Read and Inc    |           <->             |                           |  1  |
|                 |                           |          <->              |  1  |
| Read and Inc    |           <->             |                           |  2  |
|                 |                           |          <->              |  2  |
| Read and Inc    |           <->             |                           |  3  |
|                 |                           |          <->              |  3  |
| ...             |                           |                           | ... |
Atomic operations can be done in Go using the sync/atomic package.

```go
var i int64
 
go func() {
    atomic.AddInt64(&i, 1) // Increments i atomically
}()
 
go func() {
    atomic.AddInt64(&i, 1) // Same
}()
```

##### NOTE
> The sync/atomic package provides primitives for int32, int64, uint32, and uint64 but not for int

Another option is to synchronize the two goroutines with an ad hoc data structure like a mutex. _Mutex_ stands for _mutual exclusion_; a mutex ensures that at most one goroutine accesses a so-called critical section. In Go, the sync package provides a Mutex type:

```go
i := 0
mutex := sync.Mutex{}
 
go func() {
    mutex.Lock() // Start of the critical section
    i++ // Increments i
    mutex.Unlock() // End of the critical section
}()
 
go func() {
    mutex.Lock()
    i++
    mutex.Unlock()
}()
```

Which approach works best? The boundary is pretty straightforward. As we mentioned, the sync/atomic package works only with specific types. If we want something else (for example, slices, maps, and structs), we can’t rely on sync/atomic.

Another possible option is to prevent sharing the same memory location and instead favor communication across the goroutines. For example, we can create a channel that each goroutine uses to produce the value of the increment:

```go
i := 0
ch := make(chan int)
 
go func() {
    ch <- 1 // Notifies the goroutine to increment by 1
}()
 
go func() {
    ch <- 1
}()
 
i += <-ch // Increments i from what’s received from the channel
i += <-ch
```

Data races occur when multiple goroutines access the same memory location simultaneously (for example, the same variable) and at least one of them is writing. We have also seen how to prevent this issue with three synchronization approaches:

- ==Using atomic operations==
- ==Protecting a critical section with a mutex==
- ==Using communication and channels to ensure that a variable is updated by only one goroutine==

```go
i := 0
mutex := sync.Mutex{}
 
go func() {
    mutex.Lock()
    defer mutex.Unlock()
    i = 1 // The first goroutine assigns 1 to i.
}()
 
go func() {
    mutex.Lock()
    defer mutex.Unlock()
    i = 2 // The second goroutine assigns 2 to i.
}()
```

Is there a data race in this example? No, there isn’t. Both goroutines access the same variable, but not at the same time, as the mutex protects it. But is this example deterministic? No, it isn’t.

Depending on the execution order, i will eventually equal either 1 or 2. This example doesn’t lead to a data race. But it has a _race condition_. A race condition occurs when the behavior depends on the sequence or the timing of events that can’t be controlled. Here, the timing of events is the goroutines’ execution order.

Ensuring a specific execution sequence among goroutines is a question of coordination and orchestration
Channels can be a way to solve this problem. Coordinating and orchestrating can also ensure that a particular section is accessed by only one goroutine, which can also mean removing the mutex in the previous example.

In summary, when we work in concurrent applications, it’s essential to understand that a data race is different from a race condition. A data race occurs when multiple goroutines simultaneously access the same memory location and at least one of them is writing. A data race means unexpected behavior. However, a data-race-free application doesn’t necessarily mean deterministic results. An application can be free of data races but still have behavior that depends on uncontrolled events this is a race condition

### 8.4.2 The Go memory model

buffered and unbuffered channels offer differ guarantees. To avoid unexpected races caused by a lack of understanding of the core specifications of the language, we have to look at the Go memory model.

The Go memory model ([https://golang.org/ref/mem](https://golang.org/ref/mem)) is a specification that defines the conditions under which a read from a variable in one goroutine can be guaranteed to happen after a write to the same variable in a different goroutine. In other words, it provides guarantees that developers should keep in mind to avoid data races and force deterministic output.

Within a single goroutine, there’s no chance of unsynchronized access. Indeed, the happens-before order is guaranteed by the order expressed by our program.

However, within multiple goroutines, we should bear in mind some of these guarantees. We will use the notation A < B to denote that event A happens before event B. Let’s examine these guarantees

- Creating a goroutine happens before the goroutine’s execution begins. Therefore, reading a variable and then spinning up a new goroutine that writes to this variable doesn’t lead to a data race:

```go
i := 0
go func() {
    i++
}()
```


- Conversely, the exit of a goroutine isn’t guaranteed to happen before any event. Thus, the following example has a data race: Again, if we want to prevent the data race from happening, we should synchronize these goroutines.

```go
i := 0
go func() {
    i++
}()
fmt.Println(i)
```

A send on a channel happens before the corresponding receive from that channel completes.

```go
i := 0
ch := make(chan struct{})
go func() {
    <-ch
    fmt.Println(i)
}()
i++
ch <- struct{}{}
// The order is as follow
variable increment < channel send < channel receive < variable read
```

Closing a channel happens before a receive of this closure.

```go
i := 0
ch := make(chan struct{})
go func() {
    <-ch
    fmt.Println(i)
}()
i++
close(ch)
```

The last guarantee regarding channels may be counterintuitive at first sight: a receive from an unbuffered channel happens _before_ the send on that channel completes.

```go
i := 0
ch := make(chan struct{}, 1)
go func() {
    i = 1
    <-ch
}()
ch <- struct{}{}
fmt.Println(i)
```

 If the channel is buffered, it leads to a data race.

```go
i := 0
ch := make(chan struct{}) // Makes the channel unbuffered
go func() {
    i = 1
    <-ch
}()
ch <- struct{}{}
fmt.Println(i)
```

the main difference: the write is guaranteed to happen before the read
Because a receive from an unbuffered channel happens before a send, the write to i will always occur before the read.

## 8.5 #59: Not understanding the concurrency impacts of a workload type #Mistake 

In programming, the execution time of a workload is limited by one of the following:

- ==_The speed of the CPU_—For example, running a merge sort algorithm. The workload is called _CPU-bound_.==
- ==_The speed of I/O_—For example, making a REST call or a database query. The workload is called _I/O-bound_.==
- ==_The amount of available memory_—The workload is called _memory-bound_.==

##### NOTE

>The last is the rarest nowadays, given that memory has become very cheap in recent decades.


```GO
func read(r io.Reader) (int, error) {
    count := 0
    for {
        b := make([]byte, 1024) // Reads 1,024 bytes
        _, err := r.Read(b)
        if err != nil {
            if err == io.EOF { // Stops the loop when we reach the end
                break
            }
            return 0, err
        }
        count += task(b) // Increments count based on the result of the task function
    }
    return count, nil
}
```

with a pool size of 10 goroutines. Each goroutine atomically updates a shared counter

```GO
func read(r io.Reader) (int, error) {
    var count int64
    wg := sync.WaitGroup{}
    var n = 10
 
    ch := make(chan []byte, n) // Creates a channel with a capacity equal to the pool
    wg.Add(n) // Adds n to the wait group
    for i := 0; i < n; i++ { // Creates a pool of n goroutines
        go func() {
            defer wg.Done() // Calls the Done method once the goroutine has received from the channel
            for b := range ch { // Each goroutine receives from the shared channel.
                v := task(b)
                atomic.AddInt64(&count, int64(v))
            }
        }()
    }
 
    for {
        b := make([]byte, 1024)
        // Read from r to b
        ch <- b // Publishes a new task to the channel after every read
    }
    close(ch)
    wg.Wait() // Waits for the wait group to complete before returning
    return int(count), nil
}
```

Having a fixed number of goroutines limits downsides. it narrows the resources’ impact and prevents an external system from being flooded. Now the golden question: what should be the value of the pool size? The answer depends on the workload type.

If the workload is I/O-bound, the answer mainly depends on the external system.

If the workload is CPU-bound, a best practice is to rely on GOMAXPROCS. GOMAXPROCS is a variable that sets the number of OS threads allocated to running goroutines. By default, this value is set to the number of logical CPUs.

##### USING RUNTIME.GOMAXPROCS

We can use the `runtime.GOMAXPROCS(int)` function to update the value of GOMAXPROCS. Calling it with 0 as an argument doesn’t change the value; it just returns the current value:

```go
n := runtime.GOMAXPROCS(0)
```

##### NOTE

>If, given particular conditions, we want the number of goroutines to be bound to the number of CPU cores, why not rely on `runtime.NumCPU()`, which returns the number of logical CPU cores? As we mentioned, GOMAXPROCS can be changed and can be less than the number of CPU cores. In the case of a CPU-bound workload, if the number of cores is four but we have only three threads, we should spin up three goroutines, not four. Otherwise, a thread will share its execution time among two goroutines, increasing the number of context switches.

When implementing the worker-pooling pattern, we have seen that the optimal number of goroutines in the pool depends on the workload type. If the workload executed by the workers is I/O-bound, the value mainly depends on the external system. Conversely, if the workload is CPU-bound, the optimal number of goroutines is close to the number of available threads.

## 8.6 #60: Misunderstanding Go contexts #Mistake 

According to the official documentation ([https://pkg.go.dev/context](https://pkg.go.dev/context)):

>_A Context carries a deadline, a cancellation signal, and other values across API boundaries_.

### 8.6.1 Deadline

A deadline refers to a specific point in time determined with one of the following:

- A `time.Duration` from now (for example, in 250 ms)
- A `time.Time` (for example, 2023-02-07 00:00:00 UTC)

The semantics of a deadline convey that an ongoing activity should be stopped if this deadline is met.

```go
type publisher interface {
    Publish(ctx context.Context, position flight.Position) error
}
```

This method accepts a context and a position. the concrete implementation calls a function to publish a message to a broker. This function is **_context aware_**, meaning it can cancel a request once the context is canceled.

Assuming we don’t receive an existing context, what should we provide to the Publish method for the context argument?

```go
type publishHandler struct {
    pub publisher
}
 
func (h publishHandler) publishPosition(position flight.Position) error {
    ctx, cancel := context.WithTimeout(context.Background(), 4*time.Second) // Creates the context that will time out after 4 seconds
    defer cancel() // Defers the cancellation
    return h.pub.Publish(ctx, position) // Passes the created context
}
```

What’s the rationale for calling the cancel function as a defer function? Internally, `context.WithTimeout` creates a goroutine that will be retained in memory for 4 seconds or until cancel is called. Therefore, calling cancel as a defer function means that when we exit the parent function, the context will be canceled, and the goroutine created will be stopped. It’s a safeguard so that when we return, we don’t leave retained objects in memory.

### 8.6.2 Cancellation signals

Another use case for Go contexts is to carry a cancellation signal.

```go
func main() {
    ctx, cancel := context.WithCancel(context.Background()) // Creates a cancellable context
    defer cancel() // Defers the call to cancel
 
    go func() {
        CreateFileWatcher(ctx, "foo.txt") // Calls the function using the created context
    }()
 
    // ...
}
```

### 8.6.3 Context values

The last use case for Go contexts is to carry a key-value list.

```go
ctx := context.WithValue(parentCtx, "key", "value")
```

We can access the value using the Value method:

```go
ctx := context.WithValue(context.Background(), "key", "value")
fmt.Println(ctx.Value("key"))
value
```

The key and values provided are any types. Indeed, for the value, we want to pass any types. But why should the key be an empty interface as well and not a string, for example? That could lead to collisions: two functions from different packages could use the same string value as a key. Hence, the latter would override the former value. Consequently, a best practice while handling context keys is to create an unexported custom type:

```go
package provider
 
type key string
 
const myCustomKey key = "key"
 
func f(ctx context.Context) {
    ctx = context.WithValue(ctx, myCustomKey, "foo")
    // ...
}
```

==**what’s the point of having a context carrying a key-value list? Because Go contexts are generic and mainstream, there are infinite use cases.**==

```go
type key string
 
const isValidHostKey key = "isValidHost" // Creates the context key
 
func checkValid(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        validHost := r.Host == "acme" // Checks whether the host is valid
        ctx := context.WithValue(r.Context(), isValidHostKey, validHost) // Creates a new context with a value to convey whether the source host is valid
 
        next.ServeHTTP(w, r.WithContext(ctx)) // Calls the next step with the new context
    })
}
```

### 8.6.4 Catching a context cancellation

The `context.Context` type exports a Done method that returns a receive-only notification channel: <-chan struct{}. This channel is closed when the work associated with the context should be canceled.

One thing to note is that the internal channel should be closed when a context is canceled or has met a deadline, instead of when it receives a specific value, because the closure of a channel is the only channel action that all the consumer goroutines will receive. This way, all the consumers will be notified once a context is canceled or a deadline is reached.

Furthermore, `context.Context `exports an Err method that returns nil if the Done channel isn’t yet closed. Otherwise, it returns a non-nil error explaining why the Done channel was closed: for example,

- A `context.Canceled` error if the channel was canceled
- A `context.DeadlineExceeded` error if the context’s deadline passed

```go
func handler(ctx context.Context, ch chan Message) error {
    for {
        select {
        case msg := <-ch: // Keeps receiving messages from ch
            // Do something with msg
        case <-ctx.Done(): // If the context is done, returns the error associated with it
            return ctx.Err()
        }
    }
}
```

In summary, to be a proficient Go developer, we have to understand what a context is and how to use it. In Go, context.Context is everywhere in the standard library and external libraries. As we mentioned, a context allows us to carry a deadline, a cancellation signal, and/or a list of keys-values. In general, a function that users wait for should take a context, as doing so allows upstream callers to decide when calling this function should be aborted.

When in doubt about which context to use, we should use `context.TODO()` instead of passing an empty context with c`ontext.Background`. `context.TODO()` returns an empty context, but semantically, it conveys that the context to be used is either unclear or not yet available (not yet propagated by a parent, for example).

## Summary #Summary 

- ==Understanding the fundamental differences between concurrency and parallelism is a cornerstone of the Go developer’s knowledge. Concurrency is about structure, whereas parallelism is about execution.==
- ==To be a proficient developer, you must acknowledge that concurrency isn’t always faster. Solutions involving parallelization of minimal workloads may not necessarily be faster than a sequential implementation. Benchmarking sequential versus concurrent solutions should be the way to validate assumptions.==
- ==Being aware of goroutine interactions can also be helpful when deciding between channels and mutexes. In general, parallel goroutines require synchronization and hence mutexes. Conversely, concurrent goroutines generally require coordination and orchestration and hence channels.==
- ==Being proficient in concurrency also means understanding that data races and race conditions are different concepts. Data races occur when multiple goroutines simultaneously access the same memory location and at least one of them is writing. Meanwhile, being data-race-free doesn’t necessarily mean deterministic execution. When a behavior depends on the sequence or the timing of events that can’t be controlled, this is a race condition.==
- ==Understanding the Go memory model and the underlying guarantees in terms of ordering and synchronization is essential to prevent possible data races and/or race conditions.==
- ==When creating a certain number of goroutines, consider the workload type. Creating CPU-bound goroutines means bounding this number close to the GOMAXPROCS variable (based by default on the number of CPU cores on the host). Creating I/O-bound goroutines depends on other factors, such as the external system.==
- ==Go contexts are also one of the cornerstones of concurrency in Go. A context allows you to carry a deadline, a cancellation signal, and/or a list of keys-values.==


# 9 Concurrency: Practice

## 9.1 #61: Propagating an inappropriate context #Mistake 


Contexts are omnipresent when working with concurrency in Go, and in many situations, it may be recommended to propagate them. However, context propagation can sometimes lead to subtle bugs, preventing subfunctions from being correctly executed.

```go
func handler(w http.ResponseWriter, r *http.Request) {
    response, err := doSomeTask(r.Context(), r) // Performs some task to compute the HTTP response
    if err != nil {
        http.Error(w, err.Error(), http.StatusInternalServerError)
        return
    }
 
    go func() { // Creates a goroutine to publish the response to Kafka
        err := publish(r.Context(), response)
        // Do something with err
    }()
 
    writeResponse(response) // Writes the HTTP response
}
```


First we call a `doSomeTask` function to get a response variable. It’s used within the goroutine calling publish and to format the HTTP response. Also, when calling publish, we propagate the context attached to the HTTP request. Can you guess what’s wrong with this piece of code?

We have to know that the context attached to an HTTP request can cancel in different conditions:

- When the client’s connection closes
- In the case of an HTTP/2 request, when the request is canceled
- When the response has been written back to the client

When the response has been written to the client, the context associated with the request will be canceled. Therefore, we are facing a race condition:

- If the response is written after the Kafka publication, we both return a response and publish a message successfully.
- However, if the response is written before or during the Kafka publication, the message shouldn’t be published.

How can we fix this issue? One idea is to not propagate the parent context. Instead, we would call publish with an empty context:

```go
err := publish(context.Background(), response)
```

that would work. Regardless of how long it takes to write back the HTTP response, we can call publish.

But what if the context contained useful values? For example, if the context contained a correlation ID used for distributed tracing, we could correlate the HTTP request and the Kafka publication. Ideally, we would like to have a new context that is detached from the potential parent cancellation but still conveys the values.

a possible solution is to implement our own Go context similar to the context provided, except that it doesn’t carry the cancellation signal.

A `context.Context` is an interface containing four methods:

```go
type Context interface {
    Deadline() (deadline time.Time, ok bool)
    Done() <-chan struct{}
    Err() error
    Value(key any) any
}
```

```go
type detach struct { // Custom struct acting as a wrapper on top of the initial context
    ctx context.Context
}
 
func (d detach) Deadline() (time.Time, bool) {
    return time.Time{}, false
}
 
func (d detach) Done() <-chan struct{} {
    return nil
}
 
func (d detach) Err() error {
    return nil
}
 
func (d detach) Value(key any) any {
    return d.ctx.Value(key) // Custom struct acting as a wrapper on top of the initial context
}
```

can now call publish and detach the cancellation signal:

```go
err := publish(detach{ctx: r.Context()}, response)
```

In summary, propagating a context should be done cautiously
bear in mind the impacts of propagating a given context and, if necessary, that it is always possible to create a custom context for a specific action.

## 9.2 #62: Starting a goroutine without knowing when to stop it #Mistake 


Goroutines are easy and cheap to start—so easy and cheap that we may not necessarily have a plan for when to stop a new goroutine, which can lead to leaks. Not knowing when to stop a goroutine is a design issue and a common concurrency mistake in Go.

In terms of memory, a goroutine starts with a minimum stack size of 2 KB, which can grow and shrink as needed. Memory-wise, a goroutine can also hold variable references allocated to the heap. Meanwhile, a goroutine can hold resources such as HTTP or database connections, open files, and network sockets that should eventually be closed gracefully. If a goroutine is leaked, these kinds of resources will also be leaked.

```go
ch := foo()
go func() {
    for v := range ch {
        // ...
    }
}()
```

The created goroutine will exit when ch is closed. But do we know exactly when this channel will be closed? It may not be evident, because ch is created by the foo function. If the channel is never closed, it’s a leak. So, we should always be cautious about the exit points of a goroutine and make sure one is eventually reached.

```go
func main() {
    newWatcher()
 
    // Run the application
}
 
type watcher struct { /* Some resources */ }
 
func newWatcher() {
    w := watcher{}
    go w.watch() // Creates a goroutine that watches some external configuration
}
```


The problem with this code is that when the main goroutine exits the application is stopped. Hence, the resources created by watcher aren’t closed gracefully. How can we prevent this from happening?

One option could be to pass to `newWatcher` a context that will be canceled when main returns:

```go
func main() {
    ctx, cancel := context.WithCancel(context.Background())
    defer cancel()
 
    newWatcher(ctx) // Passes to newWatcher a context that will eventually cancel
 
    // Run the application
}
 
func newWatcher(ctx context.Context) {
    w := watcher{}
    go w.watch(ctx) // Propagates this context
}
```

We propagate the context created to the watch method. When the context is canceled, the watcher struct should close its resources

The problem is that we used signaling to convey that a goroutine had to be stopped. We didn’t block the parent goroutine until the resources had been closed

```go
func main() {
    w := newWatcher()
    defer w.close() // Defers the call to the close method
 
    // Run the application
}
 
func newWatcher() watcher {
    w := watcher{}
    go w.watch()
    return w
}
 
func (w watcher) close() {
    // Close the resources
}
```

Instead of signaling watcher that it’s time to close its resources, we now call this close method, using defer to guarantee that the resources are closed before the application exits.

In summary, let’s be mindful that a goroutine is a resource like any other that must eventually be closed to free memory or other resources. Whenever a goroutine is started, we should have a clear plan about when it will stop. Last but not least, if a goroutine creates resources and its lifetime is bound to the lifetime of the application, it’s probably safer to wait for this goroutine to complete before exiting the application. This way, we can ensure that the resources can be freed.

## 9.3 #63: Not being careful with goroutines and loop variables #Mistake 

Mishandling goroutines and loop variables is probably one of the most common mistakes made by Go developers when writing concurrent applications.

```go
s := []int{1, 2, 3}
 
for _, i := range s { // Iterates over each element
    go func() {
        fmt.Print(i) // Accesses the loop variable
    }()
}
```

the output of this code isn’t deterministic. For example, sometimes it prints 233 and other times 333. What’s the reason?

we create new goroutines from a closure. 

We have to know that when a closure goroutine is executed, it doesn’t capture the values when the goroutine is created. Instead, all the goroutines refer to the exact same variable. When a goroutine runs, it prints the value of i at the time fmt.Print is executed. Hence, i may have been modified since the goroutine was launched.

The first option, if we want to keep using a closure, involves creating a new variable:

```go
for _, i := range s {
    val := i // Creates a variable local to each iteration
    go func() {
        fmt.Print(val)
    }()
}
```

In each iteration, we create a new local val variable. This variable captures the current value of i before the goroutine is created. Hence, when each closure goroutine executes the print statement, it does so with the expected value.

The second option no longer relies on a closure and instead uses an actual function:

```go
for _, i := range s {
    go func(val int) {// Executes a function that takes an integer as an argument
        fmt.Print(val)
    }(i) // Calls this function and passes the current value of i
}
```

still execute an anonymous function within a new a goroutine , but this time it isn’t a closure. The function doesn’t reference val as a variable from outside its body; val is now part of the function input. By doing so, we fix i in each iteration and make our application work as expected.

If the goroutine is a closure that accesses an iteration variable declared from outside its body, that’s a problem


## 9.4 #64: Expecting deterministic behavior using select and channels #Mistake 

One common mistake made by Go developers while working with channels is to make wrong assumptions about how select behaves with multiple channels. A false assumption can lead to subtle bugs that may be hard to identify and reproduce.

to implement a goroutine that needs to receive from two channels:

- `messageCh` for new messages to be processed.
- `disconnectCh` to receive notifications conveying disconnections. In that case, we want to return from the parent function.

Of these two channels, we want to prioritize `messageCh`

```go
for {
    select { // Uses the select statement to receive from multiple channels
    case v := <-messageCh: // Receives new messages
        fmt.Println(v)
    case <-disconnectCh: // Receives disconnections
        fmt.Println("disconnection, return")
        return
    }
}
```

```go
for i := 0; i < 10; i++ {
    messageCh <- i
}
disconnectCh <- struct{}{}
```

the output:

```go
0
1
2
3
4
disconnection, return
```

Instead of consuming the 10 messages, we only received 5 of them. What’s the reason? It lies in the specification of the select statement with multiple channels ([https://go.dev/ref/spec](https://go.dev/ref/spec)):

> _If one or more of the communications can proceed, a single one that can proceed is chosen via a uniform pseudo-random selection._

Unlike a switch statement, where the first case with a match wins, the select statement selects randomly if multiple options are possible.

 there’s a good reason for it: to prevent possible starvation.

How can we overcome this situation? There are different possibilities if we want to receive all the messages before returning in case of a disconnection.

[](https://livebook.manning.com/book/100-go-mistakes-and-how-to-avoid-them/chapter-9/)If there’s a single producer goroutine, we have two options:

- Make `messageCh` an unbuffered channel instead of a buffered channel. Because the sender goroutine blocks until the receiver goroutine is ready, this approach guarantees that all the messages from `messageCh` are received before the disconnection from `disconnectCh`.
- Use a single channel instead of two channels. For example, we can define a struct that conveys either a new message or a disconnection. Channels guarantee that the order for the messages sent is the same as for the messages received, so we can ensure that the disconnection is received last.

 the case where we have multiple producer goroutines, it may be impossible to guarantee which one writes first. Hence, whether we have an unbuffered `messageCh` channel or a single channel, it will lead to a race condition among the producer goroutines. In that case, we can implement the following solution:

1. Receive from either `messageCh` or `disconnectCh`.
2. If a disconnection is received
    - Read all the existing messages in `messageCh`, if any.
    - Then return.


```go
for {
    select {
    case v := <-messageCh:
        fmt.Println(v)
    case <-disconnectCh:
        for { // Inner for/select
            select {
            case v := <-messageCh: // Reads the remaining messages
                fmt.Println(v)
            default: // Then returns
                fmt.Println("disconnection, return")
                return
            }
        }
    }
}
```


This solution uses an inner for/select with two cases: one on `messageCh` and a default case. Using default in a select statement is chosen only if none of the other cases match. In this case, it means we will return only after we have received all the remaining messages in `messageCh`.

When using select with multiple channels, we must remember that if multiple options are possible, the first case in the source order does not automatically win. Instead, Go selects randomly, so there’s no guarantee about which option will be chosen. To overcome this behavior, in the case of a single producer goroutine, we can use either unbuffered channels or a single channel. In the case of multiple producer goroutines, we can use inner selects and default to handle prioritizations.

## 9.5 #65: Not using notification channels #Mistake 

Channels are a mechanism for communicating across goroutines via signaling. A signal can be either with or without data. But for Go programmers, it’s not always straightforward how to tackle the latter case.

```go
disconnectCh := make(chan bool)
```

Because it’s a channel of Booleans, we can receive either true or false messages.  what true conveys. But what does false mean? Does it mean we haven’t been disconnected? And in this case, how frequently will we receive such a signal? Does it mean we have reconnected?

if we don’t need a specific value to convey some information, we need a channel _without_ data. The idiomatic way to handle it is a channel of empty structs: chan struct{}.

In Go, an empty struct is a struct without any fields. Regardless of the architecture, it occupies zero bytes of storage, as we can verify using `unsafe.Sizeof`:

```go
var s struct{}
fmt.Println(unsafe.Sizeof(s))
0
```

An empty struct is a de facto standard to convey an absence of meaning.

Applied to channels, if we want to create a channel to send notifications without data, the appropriate way to do so in Go is a chan struct{}. One of the best-known utilizations of a channel of empty structs comes with Go contexts

A channel can be with or without data. If we want to design an idiomatic API in regard to Go standards, let’s remember that a channel without data should be expressed with a chan struct{} type. This way, it clarifies for receivers that they shouldn’t expect any meaning from a message’s content—only the fact that they have received a message. In Go, such channels are called **_notification channels_.**

## 9.6 #66: Not using nil channels #Mistake 

```go
var ch chan int // nil channel
<-ch
```

ch is a chan int type. The zero value of a channel being nil, ch is nil. The goroutine won’t panic; however, it will block forever.

The principle is the same if we send a message to a nil channel. This goroutine blocks forever:

```go
var ch chan int
ch <- 0
```

will implement a func merge (ch1, ch2 <-chan int) <-chan int function to merge two channels into a single channel. By merging them , we mean each message received in either ch1 or ch2 will be sent to the channel returned.


```go
func merge(ch1, ch2 <-chan int) <-chan int {
    ch := make(chan int, 1)
 
    go func() {
        for v := range ch1 { // Receives from ch1 and publishes to the merged channel
            ch <- v
        }
        for v := range ch2 { // Receives from ch2 and publishes to the merged channel
            ch <- v
        }
        close(ch)
    }()
 
    return ch
}

```

The main issue with this first version is that we receive from ch1 and _then_ we receive from ch2. It means we won’t receive from ch2 until ch1 is closed. This doesn’t fit our use case, as ch1 may be open forever, so we want to receive from both channels simultaneously.

```go
func merge(ch1, ch2 <-chan int) <-chan int {
    ch := make(chan int, 1)
 
    go func() {
        for {
            select { // Receives concurrently to both ch1 and ch2
            case v := <-ch1:
                ch <- v
            case v := <-ch2:
                ch <- v
            }
        }
        close(ch)
    }()
 
    return ch
}
```

The select statement lets a goroutine wait on multiple operations at the same time. Because we wrap it inside a for loop, we should repeatedly receive messages from one or the other channel, 

One problem is that the close(ch) statement is unreachable. Looping over a channel using the range operator breaks when the channel is closed. However, the way we implemented a for/select doesn’t catch when either ch1 or ch2 is closed. Even worse, if at some point ch1 or ch2 is closed, here’s what a receiver of the merged channel will receive when logging the value:

the output: 

```go
received: 0
received: 0
received: 0
received: 0
received: 0
...
```

Receiving from a closed channel is a non-blocking operation:

```go
ch1 := make(chan int)
close(ch1)
fmt.Print(<-ch1, <-ch1)
```

To check whether we receive a message or a closure signal, we must do it this way:

```go
ch1 := make(chan int)
close(ch1)
v, open := <-ch1 // Assigns to open whether or not the channel is open
fmt.Print(v, open)
```

```go
0 false
```

- ch1 is closed first, so we have to receive from ch2 until it is closed.
- ch2 is closed first, so we have to receive from ch1 until it is closed.

```go
func merge(ch1, ch2 <-chan int) <-chan int {
    ch := make(chan int, 1)
    ch1Closed := false
    ch2Closed := false
 
    go func() {
        for {
            select {
            case v, open := <-ch1:
                if !open { // Handles if ch1 is closed
                    ch1Closed = true
                    break
                }
                ch <- v
            case v, open := <-ch2:
                if !open { // Handles if ch2 is closed
                    ch2Closed = true
                    break
                }
                ch <- v
            }
 
            if ch1Closed && ch2Closed { // Closes and returns if both channels are closed
                close(ch)
                return
            }
        }
    }()
 
    return ch
}
```

There is one major issue: when one of the two channels is closed, the for loop will act as a busy-waiting loop, meaning it will keep looping even though no new message is received in the other channel.

when we reach select again, it will wait for one of these three conditions to happen:

- ch1 is closed.
- ch2 has a new message.
- ch2 is closed.

receiving from a nil channel will block forever. Instead of setting a Boolean after a channel is closed, we will assign this channel to nil. 

```go
func merge(ch1, ch2 <-chan int) <-chan int {
    ch := make(chan int, 1)
 
    go func() {
        for ch1 != nil || ch2 != nil { // Continues if at least one channel isn’t nil
            select {
            case v, open := <-ch1:
                if !open {
                    ch1 = nil // Assigns ch1 to a nil channel once closed 
                    break
                }
                ch <- v
            case v, open := <-ch2:
                if !open {
                    ch2 = nil // Assigns ch2 to a nil channel once closed
                    break
                }
                ch <- v
            }
        }
        close(ch)
    }()
 
    return ch
}
```

the select statement will only wait for two conditions:

- ch2 has a new message.
- ch2 is closed.

![[Pasted image 20240104103945.png]]

In summary,  waiting or sending to a nil channel is a blocking action, and this behavior isn’t useless.
nil channels are useful in some conditions and should be part of the Go developer’s toolset when dealing with concurrent code.

## 9.7 #67: Being puzzled about channel size #Mistake 

When we create a channel using the make built-in function, the channel can be either unbuffered or buffered. Related to this topic, two mistakes happen fairly frequently: being confused about when to use one or the other; and, if we use a buffered channel, what size to use.

 the core concepts. An unbuffered channel is a channel _without_ any capacity. It can be created by either omitting the size or providing a 0 size:

```go
ch1 := make(chan int)
ch2 := make(chan int, 0)
```

Using an unbuffered channel (sometimes called a synchronous channel), the sender will block until the receiver receives data from the channel.

Conversely, a buffered channel has a capacity, and it must be created with a size greater than or equal to 1:

```go
ch3 := make(chan int, 1)
```

```go
ch3 := make(chan int, 1)
ch3 <-1 // Non-blocking
ch3 <-2 // Blocking
```

Channels are a concurrency abstraction to enable communication among goroutines. But what about synchronization? In concurrency, synchronization means we can guarantee that multiple goroutines will be in a known state at some point.

Regarding channels:

- ==An unbuffered channel enables synchronization. We have the guarantee that two goroutines will be in a known state: one receiving and another sending a message.==
- ==A buffered channel doesn’t provide any strong synchronization. Indeed, a producer goroutine can send a message and then continue its execution if the channel isn’t full. The only guarantee is that a goroutine won’t receive a message before it is sent. But this is only a guarantee because of causality==

Both channel types enable communication, but only one provides synchronization. If we need synchronization, we must use unbuffered channels.

But what if we need a buffered channel? What size should we provide? The default value we should use for buffered channels is its minimum: is there any good reason _not_ to use a value of 1? Here’s a list of possible cases where we should use another size:

- ==While using a worker pooling-like pattern, meaning spinning a fixed number of goroutines that need to send data to a shared channel. In that case, we can tie the channel size to the number of goroutines created.==
- ==When using channels for rate-limiting problems. For example, if we need to enforce resource utilization by bounding the number of requests, we should set up the channel size according to the limit.==

```go
ch := make(chan int, 40)
```

deciding about an accurate queue size isn’t an easy problem. First, it’s a balance between CPU and memory. The smaller the value, the more CPU contention we can face. But the bigger the value, the more memory will need to be allocated.

Another point to consider is the

>_Queues are typically always close to full or close to empty due to the differences in pace between consumers and producers. They very rarely operate in a balanced middle ground where the rate of production and consumption is evenly matched._


it’s usually best to start with a default channel size of 1

## 9.8 #68: Forgetting about possible side effects with string formatting #Mistake 

### 9.8.1 etcd data race

etcd is a distributed key-value store implemented in Go. It is used in many projects, including Kubernetes, to store all cluster data. It provides an API to interact with a cluster.

```GO
type Watcher interface {
    // Watch watches on a key or prefix. The watched events will be returned
    // through the returned channel.
    // ...
    Watch(ctx context.Context, key string, opts ...OpOption) WatchChan
    Close() error
}
```

The server has to maintain a list of all the clients using this feature. Hence, the Watcher interface is implemented by a watcher struct containing all the active streams:

```go
type watcher struct {
    // ...
 
    // streams hold all the active gRPC streams keyed by ctx value.
    streams map[string]*watchGrpcStream
}
```

The map’s key is based on the context provided when calling the Watch method:

```go
func (w *watcher) Watch(ctx context.Context, key string,
    opts ...OpOption) WatchChan {
    // ...
    ctxKey := fmt.Sprintf("%v", ctx) // Formats the map key depending on the provided context
    // ...
    wgs := w.streams[ctxKey]
    // ...
```

`ctxKey` is the map’s key, formatted from the context provided by the client. When formatting a string from a context created with values (`context.WithValue`), Go will read all the values in this context.

one goroutine was updating one of the context values, whereas another was executing Watch, hence reading all the values in this context. This led to a data race.

The fix ([https://github.com/etcd-io/etcd/pull/7816](https://github.com/etcd-io/etcd/pull/7816)) was to not rely on `fmt.Sprintf` to format the map’s key to prevent traversing and reading the chain of wrapped values in the context. Instead, the solution was to implement a custom `streamKeyFromCtx` function to extract the key from a specific context value that wasn’t mutable.

> **NOTE**
>A potentially mutable value in a context can introduce additional complexity to prevent data races. This is probably a design decision to be considered with care.

### 9.8.2 Deadlock

```go
type Customer struct {
    mutex sync.RWMutex // Uses a sync.RWMutex to protect concurrent accesses
    id    string
    age   int
}
 
func (c *Customer) UpdateAge(age int) error {
    c.mutex.Lock() // Locks and defers unlock as we update Customer
    defer c.mutex.Unlock()
 
    if age < 0 { // Returns an error if age is negative
        return fmt.Errorf("age should be positive for customer %v", c)
    }
 
    c.age = age
    return nil
}
 
func (c *Customer) String() string {
    c.mutex.RLock() // Locks and defers unlock as we read Customer
    defer c.mutex.RUnlock()
    return fmt.Sprintf("id %s, age %d", c.id, c.age)
}
```

 If the provided age is negative, we return an error. Because the error is formatted, using the %s directive on the receiver, it will call the String method `toformat` Customer. But because `UpdateAge` already acquires the mutex lock, the String method won’t be able to acquire it
Hence, this leads to a deadlock situation. If all goroutines are also asleep, it leads to a panic:

```go
fatal error: all goroutines are asleep - deadlock!
 
goroutine 1 [semacquire]:
sync.runtime_SemacquireMutex(0xc00009818c, 0x10b7d00, 0x0)
...
```

One thing that could be improved here is to restrict the scope of the mutex locking. In `UpdateAge`, we first acquire the lock and check whether the input is valid. We should do the opposite: first check the input, and if the input is valid, acquire the lock. This has the benefit of reducing the potential side effects but can also have an impact performance-wise—a lock is acquired only when it’s required, not before:

```go
func (c *Customer) UpdateAge(age int) error {
    if age < 0 {
        return fmt.Errorf("age should be positive for customer %v", c)
    }
 
    c.mutex.Lock() // Locks the mutex only when input has been validated
    defer c.mutex.Unlock()
 
    c.age = age
    return nil
}
```

 locking the mutex only after the age has been checked avoids the deadlock situation.
 In some conditions, though, it’s not straightforward or possible to restrict the scope of a mutex lock.

```go
func (c *Customer) UpdateAge(age int) error {
    c.mutex.Lock()
    defer c.mutex.Unlock()
 
    if age < 0 {
        return fmt.Errorf("age should be positive for customer id %s", c.id)
    }
 
    c.age = age
    return nil
}
```

## 9.9 #69: Creating data races with append #Mistake 

```GO
s := make([]int, 1)
 
go func() { // In a new goroutine, appends a new element on s
    s1 := append(s, 1)
    fmt.Println(s1)
}()
 
go func() { // Same
    s2 := append(s, 1)
    fmt.Println(s2)
}()
```

 this example has a data race? The answer is no.

```go
s := make([]int, 0, 1) // Changes the way the slice is initialized
 
// Same
```

Does it contain a data race? The answer is yes:

```go
==================
WARNING: DATA RACE
Write at 0x00c00009e080 by goroutine 10:
  ...
 
Previous write at 0x00c00009e080 by goroutine 9:
  ...
==================
```

create a slice with make([]int, 0, 1). Therefore, the array isn’t full. Both goroutines attempt to update the same index of the backing array (index 1), which is a data race.

How can we prevent the data race if we want both goroutines to work on a slice containing the initial elements of s plus an extra element? One solution is to create a copy of s:

```go
s := make([]int, 0, 1)
 
go func() {
    sCopy := make([]int, len(s), cap(s))
    copy(sCopy, s) // Makes a copy and uses append on the copied slice
 
    s1 := append(sCopy, 1)
    fmt.Println(s1)
}()
 
go func() {
    sCopy := make([]int, len(s), cap(s))
    copy(sCopy, s) // Same
 
    s2 := append(sCopy, 1)
    fmt.Println(s2)
}()
```

Both goroutines make a copy of the slice. Then they use append on the slice copy, not the original slice. This prevents a data race because both goroutines work on isolated data.

==**DATA RACES WITH SLICES AND MAPS**==

==How much do data races impact slices and maps? When we have multiple goroutines the following is true:==

- ==Accessing the same slice index with at least one goroutine updating the value is a data race. The goroutines access the same memory location.==
- ==Accessing different slice indices regardless of the operation isn’t a data race; different indices mean different memory locations.==
- ==Accessing the same map (regardless of whether it’s the same or a different key) with at least one goroutine updating it is a data race.==

While working with slices in concurrent contexts, we must recall that using append on slices isn’t always race-free. Depending on the slice and whether it’s full, the behavior will change. If the slice is full, append is race-free. Otherwise, multiple goroutines may compete to update the same array index, resulting in a data race.

## 9.10 #70: Using mutexes inaccurately with slices and maps #Mistake 

While working in concurrent contexts where data is both mutable and shared, we often have to implement protected accesses around data structures using mutexes.

```go
type Cache struct {
    mu       sync.RWMutex
    balances map[string]float64
}
```

```go
func (c *Cache) AddBalance(id string, balance float64) {
    c.mu.Lock()
    c.balances[id] = balance
    c.mu.Unlock()
}
```

```go
func (c *Cache) AverageBalance() float64 {
    c.mu.RLock()
    balances := c.balances // Creates a copy of the balances map
    c.mu.RUnlock()
 
    sum := 0.
    for _, balance := range balances { // Iterates over the copy, outside of the critical section
        sum += balance
    }
    return sum / float64(len(balances))
}
```

First we create a copy of the map to a local balances variable. Only the copy is done in the critical section to iterate over each balance and calculate the average outside of the critical section. Does this solution work?

a data race occurs. What’s the problem here?

Internally, a map is a `runtime.hmap` struct containing mostly metadata (for example, a counter) and a pointer referencing data buckets. So, `balances := c.balances` doesn’t copy the actual data. It’s the same principle with a slice:

```go
s1 := []int{1, 2, 3}
s2 := s1
s2[0] = 42
fmt.Println(s1)
```

The reason is that s2 := s1 creates a new slice: s2 has the same length and the same capacity and is backed by the same array as s1.

the two goroutines perform operations on the same data set, and one of them mutates it. Hence, it’s a data race. How can we fix the data race?

If the iteration operation isn’t heavy (that’s the case here, as we perform an increment operation), we should protect the whole function:

```go
func (c *Cache) AverageBalance() float64 {
    c.mu.RLock()
    defer c.mu.RUnlock() // Unlocks when the function returns
 
    sum := 0.
    for _, balance := range c.balances {
        sum += balance
    }
    return sum / float64(len(c.balances))
}
```

Another option, if the iteration operation isn’t lightweight, is to work on an actual copy of the data and protect only the copy:

```go
func (c *Cache) AverageBalance() float64 {
    c.mu.RLock()
    m := make(map[string]float64, len(c.balances)) // Copies the map
    for k, v := range c.balances {
        m[k] = v
    }
    c.mu.RUnlock()
 
    sum := 0.
    for _, balance := range m {
        sum += balance
    }
    return sum / float64(len(m))
}
```

Once we have made a deep copy, we release the mutex. The iterations are done on the copy outside of the critical section.
this solution can be a good fit if and only if an operation isn’t _fast_.  It’s impossible to define a threshold when choosing one solution or the other as the choice depends on factors such as the number of elements and the average size of the struct.
In summary, we have to be careful with the boundaries of a mutex lock.

## 9.11 #71: Misusing `sync.WaitGroup` #Mistake 

`sync.WaitGroup` is a mechanism to wait for _n_ operations to complete; generally, we use it to wait for _n_ goroutines to complete.

A wait group can be created with the zero value of `sync.WaitGroup`:

```go
wg := sync.WaitGroup{}
```

Internally, a `sync.WaitGroup` holds an internal counter initialized by default to 0. We can increment this counter using the Add(int) method and decrement it using Done() or Add with a negative value. If we want to wait for the counter to be equal to 0, we have to use the Wait() method that is blocking.

##### NOTE
The counter cannot be negative, or the goroutine will panic.

```go
wg := sync.WaitGroup{}
var v uint64
 
for i := 0; i < 3; i++ {
    go func() { // Creates a goroutine
        wg.Add(1) // Increments the wait group counter
        atomic.AddUint64(&v, 1) // Atomically increments v
        wg.Done() // Decrements the wait group counter
    }()
}
 
wg.Wait() // Waits until all the goroutines have incremented v before printing it
fmt.Println(v)
```

What’s wrong with this code?

The problem is that `wg.Add(1)` is called within the newly created goroutine, not in the parent goroutine. Hence, there is no guarantee that we have indicated to the wait group that we want to wait for three goroutines before calling `wg.Wait()`.

The race detector can also detect unsafe accesses to v.

When dealing with goroutines, it’s crucial to remember that the execution isn’t deterministic without synchronization. For example, the following code could print either ab or ba:

```go
go func() {
    fmt.Print("a")
}()
go func() {
    fmt.Print("b")
}()
```

Both goroutines can be assigned to different threads, and there’s no guarantee which thread will be executed first.

The CPU has to use a _memory fence_ (also called a _memory barrier_) to ensure order.
there are two options to fix our issue. First, we can call `wg.Add` before the loop with 3:

```go
wg := sync.WaitGroup{}
var v uint64
 
wg.Add(3)
for i := 0; i < 3; i++ {
    go func() {
        // ...
    }()
}
 
// ...
```

Or, second, we can call `wg.Add` during each loop iteration before spinning up the child goroutines:

```go
wg := sync.WaitGroup{}
var v uint64
 
for i := 0; i < 3; i++ {
    wg.Add(1)
    go func() {
        // ...
    }()
}
 
// ...
```

Both solutions are fine. If the value we want to set eventually to the wait group counter is known in advance, the first solution prevents us from having to call `wg.Add` multiple times. However, it requires making sure the same count is used everywhere to avoid subtle bugs.

## 9.12 #72: Forgetting about `sync.Cond` #Mistake 

The example an application that raises alerts whenever specific goals are reached. We will have one goroutine in charge of incrementing a balance (an updater goroutine). In contrast, other goroutines will receive updates and print a message whenever a specific goal is reached (listener goroutines). 

One first naive solution uses mutexes. The updater goroutine increments the balance every second. On the other side, the listener goroutines loop until their donation goal is met:

```go
type Donation struct { // Creates and instantiates a Donation struct containing the current balance and a mutex
    mu             sync.RWMutex
    balance int
}
donation := &Donation{}
 
// Listener goroutines
f := func(goal int) { // Creates a closure
    donation.mu.RLock()
    for donation.balance < goal {// Checks if the goal is reached
        donation.mu.RUnlock()
        donation.mu.RLock()
    }
    fmt.Printf("$%d goal reached\n", donation.balance)
    donation.mu.RUnlock()
}
go f(10)
go f(15)
 
// Updater goroutine
go func() {
    for { // Keeps incrementing the balance
        time.Sleep(time.Second)
        donation.mu.Lock()
        donation.balance++
        donation.mu.Unlock()
    }
}()
```


```go
$10 goal reached
$15 goal reached
```

The main issue—and what makes this a terrible implementation—is the busy loop. Each listener goroutine keeps looping until its donation goal is met, which wastes a lot of CPU cycles and makes the CPU usage gigantic.

find a way to signal from the updater goroutine whenever the balance is updated. If we think about signaling in Go, we should consider channels.

```go
type Donation struct {
    balance int
    ch      chan int // Updates Donation so it contains a channel
}
 
donation := &Donation{ch: make(chan int)}
 
// Listener goroutines
f := func(goal int) {
    for balance := range donation.ch { // Receives channel updates
        if balance >= goal {
            fmt.Printf("$%d goal reached\n", balance)
            return
        }
    }
}
go f(10)
go f(15)
 
// Updater goroutine
for {
    time.Sleep(time.Second)
    donation.balance++
    donation.ch <- donation.balance // Sends a message whenever the balance is updated
}
```

Each listener goroutine receives from a shared channel. Meanwhile, the updater goroutine sends messages whenever the balance is updated.

```go
$11 goal reached
$15 goal reached
```

The first goroutine should have been notified when the balance was $10, not $11. What happened?

A message sent to a channel is received by only one goroutine.

The default distribution mode with multiple goroutines receiving from a shared channel is round-robin. It can change if one goroutine isn’t ready to receive messages in that case, Go distributes the message to the next available goroutine.

Each message is received by a single goroutine. Therefore, the first goroutine didn’t receive the $10 message in this example, but the second one did. Only a channel closure event can be broadcast to multiple goroutines.

There’s another issue with using channels in this situation. The listener goroutines return whenever their donation goal is met. Hence, the updater goroutine has to know when all the listeners stop receiving messages to the channel. Otherwise, the channel will eventually become full and block the sender. A possible solution could be to add a `sync.WaitGroup` to the mix, but doing so would make the solution more complex.

Go has a solution: `sync.Cond`

According to the official documentation ([https://pkg.go.dev/sync](https://pkg.go.dev/sync)),

>_Cond implements a condition variable, a rendezvous point for goroutines waiting for or announcing the occurrence of an event_.

A condition variable is a container of threads (here, goroutines) waiting for a certain condition.

```go
type Donation struct {
    cond    *sync.Cond // Adds a *sync.Cond
    balance int
}
 
donation := &Donation{
    cond: sync.NewCond(&sync.Mutex{}), // sync.Cond relies on a mutex.
}
 
// Listener goroutines
f := func(goal int) {
    donation.cond.L.Lock()
    for donation.balance < goal {
        donation.cond.Wait() // Waits for a condition (balance updated) within lock/unlock
    }
    fmt.Printf("%d$ goal reached\n", donation.balance)
    donation.cond.L.Unlock()
}
go f(10)
go f(15)
 
// Updater goroutine
for {
    time.Sleep(time.Second)
    donation.cond.L.Lock()
    donation.balance++ // Increments the balance within lock/unlock
    donation.cond.L.Unlock()
    donation.cond.Broadcast() // Broadcasts the fact that a condition was met (balance updated)
}
```

The call to Wait must happen within a critical section. Actually, the implementation of Wait is the following:

1. Unlock the mutex.
2. Suspend the goroutine, and wait for a notification.
3. Lock the mutex when the notification arrives.

So, the listener goroutines have two critical sections:

- When accessing `donation.balance` in for `donation.balance` < goal
- When accessing `donation.balance` in `fmt.Printf`

```go
10$ goal reached
15$ goal reached
```

## 9.13 #73: Not using `errgroup` #Mistake 

golang.org/x is a repository providing extensions to the standard library. The sync sub-repository contains a handy package: `errgroup`.

```go
func handler(ctx context.Context, circles []Circle) ([]Result, error) {
    results := make([]Result, len(circles))
    wg := sync.WaitGroup{} // Creates a wait group to wait for all the goroutines that we spin up
    wg.Add(len(results))
 
    for i, circle := range circles {
        i := i // Creates a new i variable used in the goroutine (see mistake #63, “Not being careful with goroutines and loop variables”)
        circle := circle // Same for circle
 
        go func() { // Triggers a goroutine per Circle
            defer wg.Done() // Indicates when the goroutine is complete
            result, err := foo(ctx, circle)
            if err != nil {
                // ?
            }
            results[i] = result // Aggregates the results
        }()
    }
 
    wg.Wait()
    // ...
}
```


decided to use a `sync.WaitGroup` to wait until all the goroutines are completed and handle the aggregations in a slice. This is one way to do it; another would be to send each partial result to a channel and aggregate them in another goroutine. The main challenge would be to reorder the incoming messages if ordering was required. Therefore, we decided to go with the easiest approach and a shared slice.

However, What if foo (the call made within a new goroutine) returns an error? How should we handle it? There are various options, including these:

- Just like the results slice, we could have a slice of errors shared among the goroutines. Each goroutine would write to this slice in case of an error. We would have to iterate over this slice in the parent goroutine to determine whether an error occurred (O(n) time complexity).
- We could have a single error variable accessed by the goroutines via a shared mutex.
- We could think about sharing a channel of errors, and the parent goroutine would receive and handle these errors.

Regardless of the option chosen, it starts to make the solution pretty complex. For that reason, the `errgroup` package was designed and developed.

It exports a single `WithContext` function that returns a *Group struct given a context. This struct provides synchronization, error propagation, and context cancellation for a group of goroutines and exports only two methods:

- Go to trigger a call in a new goroutine.
- Wait to block until all the goroutines have completed. It returns the first non-nil error, if any.

```go
func handler(ctx context.Context, circles []Circle) ([]Result, error) {
    results := make([]Result, len(circles))
    g, ctx := errgroup.WithContext(ctx) // Creates an *errgroup.Group given the parent context
 
    for i, circle := range circles {
        i := i
        circle := circle
        g.Go(func() error { // Calls Go to spin up the logic of handling the error and aggregating the results in a new goroutine
            result, err := foo(ctx, circle)
            if err != nil {
                return err
            }
            results[i] = result
            return nil
        })
    }
 
    if err := g.Wait(); err != nil { // Calls Wait to wait for all the goroutines
        return nil, err
    }
    return results, nil
}
```

In summary, when we have to trigger multiple goroutines and handle errors plus context propagation, it may be worth considering whether `errgroup` could be a solution.
this package enables synchronization for a group of goroutines and provides an answer to deal with errors and shared contexts.

## 9.14 #74: Copying a sync type #Mistake 

The sync package provides basic synchronization primitives such as mutexes, condition variables, and wait groups. For all these types, there’s a hard rule to follow: they should never be copied.

```go
type Counter struct {
    mu       sync.Mutex
    counters map[string]int
}
 
func NewCounter() Counter { // Factory function
    return Counter{counters: map[string]int{}}
}
 
func (c Counter) Increment(name string) {
    c.mu.Lock() // Increments the counter in a critical section
    defer c.mu.Unlock()
    c.counters[name]++
}
```

```go
counter := NewCounter()
 
go func() {
    counter.Increment("foo")
}()
go func() {
    counter.Increment("bar")
}()
```

```go
==================
WARNING: DATA RACE
...
```

The problem in our Counter implementation is that the mutex is copied.

sync types shouldn’t be copied. This rule applies to the following types:

- ==`sync.Cond`==
- ==`sync.Map`==
- ==`sync.Mutex`==
- ==`sync.RWMutex`==
- ==`sync.Once`==
- ==`sync.Pool`==
- ==`sync.WaitGroup`==


What are the alternatives?
The first is to modify the receiver type for the Increment method:

```go
func (c *Counter) Increment(name string) {
    // Same code
}
```

the second option is to change the type of the mu field in Counter to be a pointer:

```go
type Counter struct {
    mu       *sync.Mutex // Changes the type of mu
    counters map[string]int
}
 
func NewCounter() Counter {
    return Counter{
        mu: &sync.Mutex{}, // Changes the way mu is initialized
        counters: map[string]int{},
    }
}
```

We may face the issue of unintentionally copying a sync field in the following conditions:

- Calling a method with a value receiver (as we have seen)
- Calling a function with a sync argument
- Calling a function with an argument that contains a sync field

As a rule of thumb, whenever multiple goroutines have to access a common sync element, we must ensure that they all rely on the same instance. This rule applies to all the types defined in the sync package.

## Summary #Summary 

- ==Understanding the conditions when a context can be canceled should matter when propagating it: for example, an HTTP handler canceling the context when the response has been sent.==
- ==Avoiding leaks means being mindful that whenever a goroutine is started, you should have a plan to stop it eventually.==
- ==To avoid bugs with goroutines and loop variables, create local variables or call functions instead of closures.==
- ==Understanding that select with multiple channels chooses the case randomly if multiple options are possible prevents making wrong assumptions that can lead to subtle concurrency bugs.==
- ==Send notifications using a chan struct{} type.==
- ==Using nil channels should be part of your concurrency toolset because it allows you to _remove_ cases from select statements, for example.==
- ==Carefully decide on the right channel type to use, given a problem. Only unbuffered channels provide strong synchronization guarantees.==
- ==You should have a good reason to specify a channel size other than one for buffered channels.==
- ==Being aware that string formatting may lead to calling existing functions means watching out for possible deadlocks and other data races.==
- ==Calling append isn’t always data-race-free; hence, it shouldn’t be used concurrently on a shared slice.==
- ==Remembering that slices and maps are pointers can prevent common data races.==
- ==To accurately use `sync.WaitGroup`, call the Add method before spinning up goroutines.==
- ==You can send repeated notifications to multiple goroutines with `sync.Cond.`==
- ==You can synchronize a group of goroutines and handle errors and contexts with the `errgroup` package.==
- ==sync types shouldn’t be copied.==

# 10 The standard library

## 10.1 #75: Providing a wrong time duration #Mistake 

The standard library provides common functions and methods that accept a `time.Duration`. However, because `time.Duration` is an alias for the int64 type, newcomers to the language

```go
ticker := time.NewTicker(1000)
for {
    select {
    case <-ticker.C:
        // Do something
    }
}
```

If run this code, we notice that ticks aren’t delivered every second; they are delivered every microsecond.

Because `time.Duration` is based on the int64 type, the previous code is correct since 1000 is a valid int64. But `time.Duration` represents the elapsed time between two instants in _nanoseconds_. Therefore, we provided `NewTicker` with a duration of 1,000 nanoseconds = 1 microsecond.

if we want to purposely create a `time.Ticker` with an interval of 1 microsecond, we shouldn’t pass an int64 directly. We should instead always use the` time.Duration` API to avoid possible confusion:

```go
ticker = time.NewTicker(time.Microsecond)
// Or
ticker = time.NewTicker(1000 * time.Nanosecond)
```

## 10.2 #76: `time.After` and memory leaks #Mistake 

`Time.After(time.Duration)` is a convenient function that returns a channel and waits for a provided duration to elapse before sending a message to this channel. Usually, it’s used in concurrent code; otherwise, if we want to sleep for a given duration, we can use `time.Sleep(time.Duration)`. The advantage of `time.After` is that it can be used to implement scenarios such as “If I don’t receive any message in this channel for 5 seconds, I will ... .” But codebases often include calls to `time.After` in a loop may be a root cause of memory leaks.

```GO
func consumer(ch <-chan Event) {
    for {
        select {
        case event := <-ch: // Handles the event
            handle(event)
        case <-time.After(time.Hour): // Increments the idle counter
            log.Println("warning: no messages received")
        }
    }
}
```

Here, we use select in two cases: receiving a message from ch and after 1 hour without messages  it may lead to memory usage issues.

`time.After` returns a channel. We may expect this channel to be closed during each loop iteration, but this isn’t the case. The resources created by `time.After` are released once the timeout expires and use memory until that happens.

Can we fix this issue by closing the channel programmatically during each iteration? No. The returned channel is a <-chan `time.Time`, meaning it is a receive-only channel that can’t be closed.

Can we fix this issue by closing the channel programmatically during each iteration? No. The returned channel is a <-chan `time.Time`, meaning it is a receive-only channel that can’t be closed.

The first is to use a context instead of `time.After`:

```go
func consumer(ch <-chan Event) {
    for { // Main loop
        ctx, cancel := context.WithTimeout(context.Background(), time.Hour) // Creates a context with timeout
        select {
        case event := <-ch:
            cancel() // Cancels context if we receive a message
            handle(event)
        case <-ctx.Done(): // Context cancellation
            log.Println("warning: no messages received")
        }
    }
}
```

The downside of this approach is that we have to re-create a context during every single loop iteration. Creating a context isn’t the most lightweight operation in Go

The second option comes from the time package: `time.NewTimer`. This function creates a `time.Timer` struct that exports the following:

- A C field, which is the internal timer channel
- A Reset(`time.Duration`) method to reset the duration
- A Stop() method to stop the timer
---
##### TIME.AFTER INTERNALS

We should note that `time.After` also relies on `time.Timer`. However, it only returns the C field, so we don’t have access to the Reset method:

```go
package time
 
func After(d Duration) <-chan Time {
    return NewTimer(d).C
}
```

---

```go
func consumer(ch <-chan Event) {
    timerDuration := 1 * time.Hour
    timer := time.NewTimer(timerDuration) // Creates a new timer
 
    for { // Main loop
        timer.Reset(timerDuration) // Resets the duration
        select {
        case event := <-ch:
            handle(event)
        case <-timer.C: // Timer expiration
            log.Println("warning: no messages received")
        }
    }
}
```

calling Reset is less cumbersome than having to create a new context every time. It’s faster and puts less pressure on the garbage collector because it doesn’t require any new heap allocation. Therefore, using `time.Timer` is the best possible solution for our initial problem.

Using `time.After` in a loop isn’t the only case that may lead to a peak in memory consumption. The problem relates to code that is repeatedly called.

## 10.3 #77: Common JSON-handling mistakes #Mistake 

### 10.3.1 Unexpected behavior due to type embedding

```go
type Event struct {
    ID int
    time.Time // Embedded field
}
```

Because `time.Time` is embedded, i we can access the `time.Time` methods directly at the Event level: for example, event .Second().

```go
event := Event{
    ID:   1234,
    Time: time.Now(), // The name of an anonymous field during a struct instantiation is the name of the struct (Time).
}
 
b, err := json.Marshal(event)
if err != nil {
    return err
}
 
fmt.Println(string(b))
```

We may expect this code to print something like the following:

```go
{"ID":1234,"Time":"2021-05-18T21:15:08.381652+02:00"}
```

Instead, it prints this:

```go
"2021-05-18T21:15:08.381652+02:00"
```

Because this field is exported, it should have been marshaled.
if an embedded field type implements an interface, the struct containing the embedded field will also implement this interface. Second, we can change the default marshaling behavior by making a type implement the `json.Marshaler` interface.

```go
type Marshaler interface {
    MarshalJSON() ([]byte, error)
}
```

```go
type foo struct{} // Defines the struct
 
func (foo) MarshalJSON() ([]byte, error) { // Implements the MarshalJSON method
    return []byte(`"foo"`), nil // Returns a static response
}
 
func main() {
    b, err := json.Marshal(foo{}) // json.Marshal then relies on the custom MarshalJSON implementation.
    if err != nil {
        panic(err)
    }
    fmt.Println(string(b))
}
```

Because we have changed the default JSON marshaling behavior by implementing the Marshaler interface, this code prints "foo".

```go
type Event struct {
    ID int
    time.Time
}
```

Because `time.Time` is an embedded field of Event, the compiler promotes its methods. Therefore, Event also implements `json.Marshaler`.

Consequently, passing an Event to `json.Marshal` uses the marshaling behavior provided by `time.Time` instead of the default behavior. This is why marshaling an Event leads to ignoring the ID field.

To fix this issue, there are two main possibilities. First, we can add a name so the `time.Time` field is no longer embedded:

```go
type Event struct {
    ID   int
    Time time.Time // time.Time is no longer an embedded type.
}
```

output : 

```go
{"ID":1234,"Time":"2021-05-18T21:15:08.381652+02:00"}
```

or have to keep the `time.Time` field embedded, the other option is to make Event implement the` json.Marshaler` interface:

```go
func (e Event) MarshalJSON() ([]byte, error) {
    return json.Marshal(
        struct { // Creates an anonymous struct
            ID   int
            Time time.Time
        }{
            ID:   e.ID,
            Time: e.Time,
        },
    )
}
```

be careful with embedded fields. While promoting the fields and methods of an embedded field type can sometimes be convenient, it can also lead to subtle bugs because it can make the parent struct implement interfaces without a clear signal.

### 10.3.2 JSON and the monotonic clock

==An OS handles two different clock types: wall and monotonic.==

==The wall clock is used to determine the current time of day. This clock is subject to variations. For example, if the clock is synchronized using the Network Time Protocol (NTP), it can jump backward or forward in time. We shouldn’t measure durations using the wall clock because we may face strange behavior, such as negative durations. This is why OSs provide a second clock type: monotonic clocks. The monotonic clock guarantees that time always moves forward and is not impacted by jumps in time. It can be affected by frequency adjustments but never by jumps in time.==

```go
type Event struct {
    Time time.Time
}
```

```go
t := time.Now() // Gets the current local time
event1 := Event{  // Instantiates an Event struct
    Time: t,
}
 
b, err := json.Marshal(event1) // Marshals into JSON
if err != nil {
    return err
}
 
var event2 Event
err = json.Unmarshal(b, &event2) // Unmarshals JSON
if err != nil {
    return err
}
 
fmt.Println(event1 == event2)
```

```go
fmt.Println(event1.Time)
fmt.Println(event2.Time)
2021-01-10 17:13:08.852061 +0100 CET m=+0.000338660
2021-01-10 17:13:08.852061 +0100 CET
```

The code prints different contents for event1 and event2. They are the same except for the m=+0.000338660 part. What does this mean?

In Go, instead of splitting the two clocks into two different APIs, time.Time may contain both a wall clock and a monotonic time. When we get the local time using `time.Now()`, it returns a `time.Time` with both times:

```go
2021-01-10 17:13:08.852061 +0100 CET m=+0.000338660
------------------------------------ --------------
             Wall time               Monotonic time
```

Conversely, when we unmarshal the JSON, the `time.Time` field doesn’t contain the monotonic time—only the wall time. Therefore, when we compare the structs, the result is false because of a monotonic time difference How can we fix this problem? There are two main options.

When we use the == operator to compare both `time.Time` fields, it compares all the struct fields, including the monotonic part. To avoid this, we can use the Equal method instead:

```go
fmt.Println(event1.Time.Equal(event2.Time))
true
```

The second option is to keep the == to compare the two structs but strip away the monotonic time using the Truncate method. This method returns the result of rounding the `time.Time` value down to a multiple of a given duration.

```go
t := time.Now()
event1 := Event{
    Time: t.Truncate(0), // Strips away the monotonic time
}
 
b, err := json.Marshal(event1)
if err != nil {
    return err
}
 
var event2 Event
err = json.Unmarshal(b, &event2)
if err != nil {
    return err
}
 
fmt.Println(event1 == event2) // Performs the comparison using the == operator
```

---
##### TIME.TIME AND LOCATION

Let’s also note that each `time.Time` is associated with a `time.Location` that represents the time zone. For example:
```go
t := time.Now() // 2021-01-10 17:13:08.852061 +0100 CET
```

```go
location, err := time.LoadLocation("America/New_York")
if err != nil {
    return err
}
t := time.Now().In(location) // 2021-05-18 22:47:04.155755 -0500 EST
```

---

### 10.3.3 Map of any

When unmarshaling data, we can provide a map instead of a struct. The rationale is that when the keys and values are uncertain, passing a map gives us some flexibility instead of a static struct.

```go
b := getMessage()
var m map[string]any
err := json.Unmarshal(b, &m) // Provides a map pointer
if err != nil {
    return err
}
```

```go
{
    "id": 32,
    "name": "foo"
}
```

 ==**an important gotcha to remember if we use a map of any: any numeric value, regardless of whether it contains a decimal, is converted into a float64 type.**==

```go
fmt.Printf("%T\n", m["id"])
float64
```

don’t make the wrong assumption and expect numeric values without decimals to be converted into integers by default. Making incorrect assumptions with type conversions could lead, for example, to goroutine panics.

## 10.4 #78: Common SQL mistakes #Mistake 

### 10.4.1 Forgetting that `sql.Open` doesn’t necessarily establish connections to a database

When using `sql.Open`, one common misconception is expecting this function to establish connections to a database:

```go
db, err := sql.Open("mysql", dsn)
if err != nil {
    return err
}
```

According to the documentation ([https://pkg.go.dev/database/sql](https://pkg.go.dev/database/sql)),

>_Open may just validate its arguments without creating a connection to the database_.

Actually, the behavior depends on the SQL driver used. For some drivers, `sql.Open` doesn’t establish a connection: it’s only a preparation for later use Therefore, the first connection to the database may be established lazily.

**==If we want to ensure that the function that uses `sql.Open` also guarantees that the underlying database is reachable, we should use the Ping method:==**

```go
db, err := sql.Open("mysql", dsn)
if err != nil {
    return err
}
if err := db.Ping(); err != nil { // Calls the Ping method following sql.Open
    return err
}
```

Ping forces the code to establish a connection that ensures that the data source name is valid and the database is reachable.

### 10.4.2 Forgetting about connections pooling

in Go. `sql.Open` returns an `*sql.DB` struct. This struct doesn’t represent a single database connection; instead, it represents a pool of connections.

A connection in the pool can have two states:

- ==Already used (for example, by another goroutine that triggers a query)==
- ==Idle (already created but not in use for the time being)==

creating a pool leads to four available config parameters that we may want to override. Each of these parameters is an exported method of `*sql.DB`:

- ==`SetMaxOpenConns`—Maximum number of open connections to the database (default value: unlimited)==
- ==`SetMaxIdleConns`—Maximum number of idle connections (default value: 2)==
- ==`SetConnMaxIdleTime`—Maximum amount of time a connection can be idle before it’s closed (default value: unlimited)==
- ==`SetConnMaxLifetime`—Maximum amount of time a connection can be held open before it’s closed (default value: unlimited)==

So, why should we tweak these config parameters?

- Setting SetMaxOpenConns is important for production-grade applications. Because the default value is unlimited, we should set it to make sure it fits what the underlying database can handle.
- The value of SetMaxIdleConns (default: 2) should be increased if our application generates a significant number of concurrent requests. Otherwise, the application may experience frequent reconnects.
- Setting `SetConnMaxIdleTime` is important if our application may face a burst of requests. When the application returns to a more peaceful state, we want to make sure the connections created are eventually released.
- Setting `SetConnMaxLifetime` can be helpful if, for example, we connect to a load-balanced database server. In that case, we want to ensure that our application never uses a connection for too long.

### 10.4.3 Not using prepared statements

A prepared statement is a feature implemented by many SQL databases to execute a repeated SQL statement. Internally, the SQL statement is precompiled and separated from the data provided. There are two main benefits:

- ==_Efficiency_—The statement doesn’t have to be recompiled (compilation means parsing + optimization + translation).==
- ==_Security_—This approach reduces the risks of SQL injection attacks.==

```go
stmt, err := db.Prepare("SELECT * FROM ORDER WHERE ID = ?") // Prepares the statement
if err != nil {
    return err
}
rows, err := stmt.Query(id) // Executes the prepared query
// ...
```


The first output of the Prepare method is an `*sql.Stmt`, which can be reused and run concurrently. When the statement is no longer needed, it must be closed using the Close() method.

### 10.4.4 Mishandling null values

```go
rows, err := db.Query("SELECT DEP, AGE FROM EMP WHERE ID = ?", id) // Executes the query
if err != nil {
    return err
}
// Defer closing rows
 
var (
    department string
    age int
)
for rows.Next() {
    err := rows.Scan(&department, &age) // Scans each row
    if err != nil {
        return err
    }
    // ...
}
```

```go
2021/10/29 17:58:05 sql: Scan error on column index 0, name "DEPARTMENT":
converting NULL to string is unsupported
```

If a column can be nullable, there are two options to prevent Scan from returning an error.

The first approach is to declare department as a string pointer:

```go
var (
    department *string // Changing the type from string to *string
    age        int
)
for rows.Next() {
    err := rows.Scan(&department, &age)
    // ...
}
```

The other approach is to use one of the `sql.NullXXX` types, such as `sql.NullString`:

```go
var (
    department sql.NullString // Changes the type to sql.NullString
    age        int
)
for rows.Next() {
    err := rows.Scan(&department, &age)
    // ...
}
```

`sql.NullString` is a wrapper on top of a string. It contains two exported fields: String contains the string value, and Valid conveys whether the string isn’t NULL. The following wrappers are accessible:

- ==`sql.NullString`==
- ==`sql.NullBool`==
- ==`sql.NullInt32`==
- ==`sql.NullInt64`==
- ==`sql.NullFloat64`==
- ==`sql.NullTime==`

Both approaches work, with `sql.NullXXX` expressing the intent more clearly, as mentioned by Russ Cox, a core Go maintainer ([http://mng.bz/rJNX](http://mng.bz/rJNX)):

> There’s no effective difference. We thought people might want to use `NullString` because it is so common and perhaps expresses the intent more clearly than *string. But either will work.


### 10.4.5 Not handling row iteration errors

common mistake to miss possible errors from iterating over rows.

```go
func get(ctx context.Context, db *sql.DB, id string) (string, int, error) {
    rows, err := db.QueryContext(ctx,
        "SELECT DEP, AGE FROM EMP WHERE ID = ?", id)
    if err != nil { // Handles errors while executing the query
        return "", 0, err
    }
    defer func() {
        err := rows.Close() // Handles errors while closing the rows
        if err != nil {
            log.Printf("failed to close rows: %v\n", err)
        }
    }()
 
    var (
        department string
        age        int
    )
    for rows.Next() {
        err := rows.Scan(&department, &age) // Handles errors while scanning a row
        if err != nil {
            return "", 0, err
        }
    }
 
    return department, age, nil
}
```


```go
func get(ctx context.Context, db *sql.DB, id string) (string, int, error) {
    // ...
    for rows.Next() {
        // ...
    }
 
    if err := rows.Err(); err != nil { // Checks rows.Err to determine whether the previous loop stopped because of an error
        return "", 0, err
    }
 
    return department, age, nil
}
```

This is the best practice to keep in mind: because `rows.Next` can stop either when we have iterated over all the rows or when an error happens while preparing the next row, we should check `rows.Err` following the iteration.

## 10.5 #79: Not closing transient resources #Mistake 

transient (temporary) resources that must be closed at some point in the code: for example, to avoid leaks on disk or in memory. Structs can generally implement the `io.Closer` interface to convey that a transient resource has to be closed.

### 10.5.1 HTTP body

```go
type handler struct {
    client http.Client
    url    string
}
 
func (h handler) getBody() (string, error) { // Makes an HTTP GET request
    resp, err := h.client.Get(h.url)
    if err != nil {
        return "", err
    }
 
    body, err := io.ReadAll(resp.Body) // Reads resp.Body and gets a body as a []byte
    if err != nil {
        return "", err
    }
 
    return string(body), nil
}
```

there’s a resource leak

resp is an `*http.Response` type. It contains a Body `io.ReadCloser` field `(io.ReadCloser` implements both io.Reader and `io.Closer`). This body must be closed if `http.Get` doesn’t return an error; otherwise, it’s a resource leak. In this case, our application will keep some memory allocated that is no longer needed but can’t be reclaimed by the GC and may prevent clients from reusing the TCP connection in the worst cases.

The most convenient way to deal with body closure is to handle it as a defer statement this way:

```go
defer func() {
    err := resp.Body.Close()
    if err != nil {
        log.Printf("failed to close response: %v\n", err)
    }
}()
```

##### NOTE
On the server side, while implementing an HTTP handler, we aren’t required to close the request body because the server does this automatically.

a response body must be closed regardless of whether we read it. For example, if we are only interested in the HTTP status code and not in the body, it has to be closed no matter what, to avoid a leak:

```go
func (h handler) getStatusCode(body io.Reader) (int, error) {
    resp, err := h.client.Post(h.url, "application/json", body)
    if err != nil {
        return 0, err
    }
 
    defer func() { // Closes the response body even if we don’t read it
        err := resp.Body.Close()
        if err != nil {
            log.Printf("failed to close response: %v\n", err)
        }
    }()
 
    return resp.StatusCode, nil
}
```

Another essential thing to remember is that the behavior is different when we close the body, depending on whether we have read from it:

- If we close the body without a read, the default HTTP transport may close the connection.
    
- If we close the body following a read, the default HTTP transport won’t close the connection; hence, it may be reused.

Therefore, if `getStatusCode` is called repeatedly and we want to use keep-alive connections, we should read the body even though we aren’t interested in it:

```go
func (h handler) getStatusCode(body io.Reader) (int, error) {
    resp, err := h.client.Post(h.url, "application/json", body)
    if err != nil {
        return 0, err
    }
 
    // Close response body
 
    _, _ = io.Copy(io.Discard, resp.Body) // Reads the response body
 
    return resp.StatusCode, nil
}
```

---

##### WHEN TO CLOSE THE RESPONSE BODY

Fairly frequently, implementations close the body if the response isn’t empty, not if the error is nil:

```go
resp, err := http.Get(url)
if resp != nil {
    defer resp.Body.Close() // ... close the response body as a defer function.
}
 
if err != nil {
    return "", err
}
```

according to the official Go documentation ([https://pkg.go.dev/net/http](https://pkg.go.dev/net/http)),

> _On error, any Response can be ignored. A non-nil Response with a non-nil error only occurs when `CheckRedirect` fails, and even then, the returned `Response.Body` is already closed_.

---

Closing a resource to avoid leaks isn’t only related to HTTP body management. In general, all structs implementing the `io.Closer` interface should be closed at some point. This interface contains a single Close method:

```go
type Closer interface {
    Close() error
}
```

### 10.5.2 `sql.Rows`

`sql.Rows` is a struct used as a result of an SQL query. Because this struct implements `io.Closer`, it has to be closed.

```go
db, err := sql.Open("postgres", dataSourceName)
if err != nil {
    return err
}
 
rows, err := db.Query("SELECT * FROM CUSTOMERS") // Performs the SQL query
if err != nil {
    return err
}
 
// Use rows
 
return nil
```


Forgetting to close the rows means a connection leak, which prevents the database connection from being put back into the connection pool.

```go
// Open connection
 
rows, err := db.Query("SELECT * FROM CUSTOMERS")
if err != nil {
    return err
}
 
defer func() { // Closes the rows
    if err := rows.Close(); err != nil {
        log.Printf("failed to close rows: %v\n", err)
    }
}()
 
// Use rows
```

### 10.5.3 `os.File`

`os.File` represents an open file descriptor. Like `sql.Rows`, it must be closed eventually:

```go
f, err := os.OpenFile(filename, os.O_APPEND|os.O_WRONLY, os.ModeAppend)
if err != nil {
    return err
}
 
defer func() {
    if err := f.Close(); err != nil {
        log.Printf("failed to close file: %v\n", err)
    }
}()
```

if we want to write to a file, we should propagate any error that occurs while closing the file:

```go
func writeToFile(filename string, content []byte) (err error) {
    // Open file
 
    defer func() { // Returns the close error if the write succeeds
        closeErr := f.Close()
        if err == nil {
            err = closeErr
        }
    }()
 
    _, err = f.Write(content)
    return
}
```

success while closing a writable os.File doesn’t guarantee that the file will be written on disk. The write can still live in a buffer on the filesystem and not be flushed on disk. If durability is a critical factor, we can use the Sync() method to commit a change. In that case, errors coming from Close can be safely ignored:

```go
func writeToFile(filename string, content []byte) error {
    // Open file
 
    defer func() { // Ignores possible errors
        _ = f.Close()
    }()
 
    _, err = f.Write(content)
    if err != nil {
        return err
    }
 
    return f.Sync() // Commits the write to the disk
}
```

Ephemeral resources must be closed at the right time and in specific situations

## 10.6 #80: Forgetting the return statement after replying to an HTTP request #Mistake 

```go
func handler(w http.ResponseWriter, req *http.Request) {
    err := foo(req)
    if err != nil {
        http.Error(w, "foo", http.StatusInternalServerError)
    }
 
    // ...
}
```

The problem with this code is that if we enter the if err != nil branch, the application will continue its execution, because `http.Error` doesn’t stop the handler’s execution.

What’s the real impact of such an error?

```go
func handler(w http.ResponseWriter, req *http.Request) {
    err := foo(req)
    if err != nil {
        http.Error(w, "foo", http.StatusInternalServerError)
    }
 
    _, _ = w.Write([]byte("all good"))
    w.WriteHeader(http.StatusCreated)
}
```

In the case err != nil, the HTTP response would be the following:

```go
foo
all good
```

The response contains both the error and success messages.
We would return only the first HTTP status code: in the previous example, 500. However, Go would also log a warning:

```go
2021/10/29 16:45:33 http: superfluous response.WriteHeader call
from main.handler (main.go:20)
```

In terms of execution, the main impact would be to continue the execution of a function that should have been stopped.
The fix for this mistake is to keep thinking about adding the return statement following `http.Error`:

```go
func handler(w http.ResponseWriter, req *http.Request) {
    err := foo(req)
    if err != nil {
        http.Error(w, "foo", http.StatusInternalServerError)
        return
    }
 
    // ...
}
```

Thanks to the return statement, the function will stop its execution if we end in the if err != nil branch.
need to remember that `http.Error` doesn’t stop a handler execution and must be added manually.


## 10.7 #81: Using the default HTTP client and server #Mistake 

### 10.7.1 HTTP client

```go
client := &http.Client{}
resp, err := client.Get("https://golang.org/")
```

Or we can use the `http.Get` function:

```go
resp, err := http.Get("https://golang.org/")
```

In the end, both approaches are the same.

```go
// DefaultClient is the default Client and is used by Get, Head, and Post.
var DefaultClient = &Client{}
```

So, what’s the problem with using the default HTTP client?

First, the default client doesn’t specify any timeouts. This absence of timeout is not something we want for production-grade systems: it can lead to many issues, such as never-ending requests that could exhaust system resources.

==the five steps involved in an HTTP request:==

1. ==Dial to establish a TCP connection.==
2. ==TLS handshake (if enabled).==
3. ==Send the request.==
4. ==Read the response headers.==
5. ==Read the response body.==

The four main timeouts are the following:

- ==`net.Dialer.Timeout`—Specifies the maximum amount of time a dial will wait for a connection to complete.==
- ==`http.Transport.TLSHandshakeTimeout`—Specifies the maximum amount of time to wait for the TLS handshake.==
- ==`http.Transport.ResponseHeaderTimeout`—Specifies the amount of time to wait for a server’s response headers.==
- ==`http.Client.Timeout`—Specifies the time limit for a request. It includes all the steps, from step 1 (dial) to step 5 (read the response body).==

```go
client := &http.Client{
    Timeout: 5 * time.Second,
    Transport: &http.Transport{
        DialContext: (&net.Dialer{
            Timeout: time.Second,
        }).DialContext,
        TLSHandshakeTimeout:   time.Second,
        ResponseHeaderTimeout: time.Second,
    },
}
```

By default, the HTTP client does connection pooling. The default client reuses connections There’s an extra timeout to specify how long an idle connection is kept in the pool: http.Transport.IdleConnTimeout. The default value is 90 seconds, which means the connection can be reused for other requests during this time. After that, if the connection hasn’t been reused, it will be closed.

### 10.7.2 HTTP server

a default server can be created using the zero value of `http.Server`:

```go
server := &http.Server{}
server.Serve(listener)
```

Once a connection is accepted, an HTTP response is divided into five steps:

1. ==Wait for the client to send the request.==
2. ==TLS handshake (if enabled).==
3. ==Read the request headers.==
4. ==Read the request body.==
5. ==Write the response.==

While exposing our endpoint to untrusted clients, the best practice is to set at least the `http.Server.ReadHeaderTimeout` field and use the `http.TimeoutHandler` wrapper function. Otherwise, clients may exploit this flaw and, for example, create never-ending connections that can lead to exhaustion of system resources.

```go
s := &http.Server{
    Addr:              ":8080",
    ReadHeaderTimeout: 500 * time.Millisecond,
    ReadTimeout:       500 * time.Millisecond,
    Handler:           http.TimeoutHandler(handler, time.Second, "foo"),
}
```

```go
s := &http.Server{
    // ...
    IdleTimeout: time.Second,
}
```

For production-grade applications, we need to make sure not to use default HTTP clients and servers. Otherwise, requests may be stuck forever due to an absence of time- outs or even malicious clients that exploit the fact that our server doesn’t have any timeouts.

## Summary #Summary 

- ==Remain cautious with functions accepting a `time.Duration`. Even though passing an integer is allowed, strive to use the time API to prevent any possible confusion.==
- ==Avoiding calls to time.After in repeated functions (such as loops or HTTP handlers) can avoid peak memory consumption. The resources created by time.After are released only when the timer expires.==
- ==Be careful about using embedded fields in Go structs. Doing so may lead to sneaky bugs like an embedded time.Time field implementing the json .Marshaler interface, hence overriding the default marshaling behavior.==
- ==When comparing two `time.Time` structs, recall that `time.Time` contains both a wall clock and a monotonic clock, and the comparison using the == ==operator is done on both clocks. `==`==
- ==To avoid wrong assumptions when you provide a map while unmarshaling JSON data, remember that numerics are converted to float64 by default.==
- ==Call the Ping or `PingContext` method if you need to test your configuration and make sure a database is reachable.==
- ==Configure the database connection parameters for production-grade applications.==
- ==Using SQL prepared statements makes queries more efficient and more secure.==
- ==Deal with nullable columns in tables using pointers or `sql.NullXXX` types.==
- ==Call the Err method of `*sql.Rows` after row iterations to ensure that you haven’t missed an error while preparing the next row.==
- ==Eventually close all structs implementing `io.Closer` to avoid possible leaks.==
- ==To avoid unexpected behaviors in HTTP handler implementations, make sure you don’t miss the return statement if you want a handler to stop after `http.Error`.==
- ==For production-grade applications, don’t use the default HTTP client and server implementations. These implementations are missing timeouts and behaviors that should be mandatory in production.==

# 11 Testing

## 11.1 #82: Not categorizing tests #Mistake 

unit tests: they’re cheap to write, fast to execute, and highly deterministic.

![[Pasted image 20240105092711.png]]

A common technique is to be explicit about which kind of tests to run. For instance, depending on the project lifecycle stage, we may want to run only unit tests or run all the tests in the project. Not categorizing tests means potentially wasting time and effort and losing accuracy about the scope of a test.

### 11.1.1 Build tags

The most common way to classify tests is using build tags. A build tag is a special comment at the beginning of a Go file, followed by an empty line.

```go
//go:build foo
 
package bar
```

Build tags are used for two primary use cases. First, we can use a build tag as a conditional option to build an application: for example, if we want a source file to be included only if cgo is enabled (cgo is a way to let Go packages call C code), we can add the //go:build cgo build tag. Second, if we want to categorize a test as an integration test, we can add a specific build flag, such as integration.

```go
//go:build integration
 
package db
 
import (
    "testing"
)
 
func TestInsert(t *testing.T) {
    // ...
}
```

The benefit of using build tags is that we can select which kinds of tests to execute.

So, running tests with a specific tag includes both the files without tags and the files matching this tag. What if we want to run _only_ integration tests? A possible way is to add a negation tag on the unit test files. For example, using !integration means we want to include the test file only if the integration flag is _not_ enabled

```go
//go:build !integration
 
package db
 
import (
    "testing"
)
 
func TestContract(t *testing.T) {
    // ...
}
```

Using this approach,

- Running go test with the integration flag runs only the integration tests.
- Running go test without the integration flag runs only the unit tests.

### 11.1.2 Environment variables

build tags have one main drawback: the absence of signals that a test has been ignored (see [http://mng.bz/qYlr](http://mng.bz/qYlr)). when we executed go test without build flags, it showed only the tests that were executed: 

```go
$ go test -v .
=== RUN   TestUnit
--- PASS: TestUnit (0.01s)
PASS
ok      db  0.319s
```

If we’re not careful with the way tags are handled, we may forget about existing tests. For that reason, some projects favor the approach of checking the test category using environment variables.

```go
func TestInsert(t *testing.T) {
    if os.Getenv("INTEGRATION") != "true" {
        t.Skip("skipping integration test")
    }
 
    // ...
}
```

If the INTEGRATION environment variable isn’t set to true, the test is skipped with a message:

```go
$ go test -v .
=== RUN   TestInsert
    db_integration_test.go:12: skipping integration test
--- SKIP: TestInsert (0.00s)
=== RUN   TestUnit
--- PASS: TestUnit (0.00s)
PASS
ok      db  0.319s
```

One benefit of using this approach is making explicit which tests are skipped and why. This technique is probably less widely used than build tags

### 11.1.3 Short mode

Another approach to categorize tests is related to their speed.
categorize the slow test so we don’t have to run it every time (especially if the trigger is after saving a file, for example). Short mode allows us to make this distinction:

```go
func TestLongRunning(t *testing.T) {
    if testing.Short() { // Marks the test as long-running
        t.Skip("skipping long-running test")
    }
    // ...
}
```

```go
% go test -short -v .
=== RUN   TestLongRunning
    foo_test.go:9: skipping long-running test
--- SKIP: TestLongRunning (0.00s)
PASS
ok      foo  0.174s
```

unlike build tags, this option works per test, not per file.

In summary, categorizing tests is a best practice for a successful testing strategy. In this section, we’ve seen three ways to categorize tests:

- ==Using build tags at the test file level==
- ==Using environment variables to mark a specific test==
- ==Based on the test pace using short mode==

## 11.2 #83: Not enabling the -race flag #Mistake 

In Go, the race detector isn’t a static analysis tool used during compilation; instead, it’s a tool to find data races that occur at runtime. To enable it, we have to enable the -race flag while compiling or running a test.

```go
$ go test -race ./...
```

Once the race detector is enabled, the compiler instruments the code to detect data races. _Instrumentation_ refers to a compiler adding extra instructions At runtime, the race detector watches for data races. However, we should keep in mind the runtime overhead of enabling the race detector:

- Memory usage may increase by 5 to 10×.
- Execution time may increase by 2 to 20×.

Because of this overhead, it’s generally recommended to enable the race detector only during local testing or continuous integration (CI).

```go
package main
 
import (
    "fmt"
)
 
func main() {
    i := 0
    go func() { i++ }()
    fmt.Println(i)
}
```

Running this application with the -race flag logs the following data race warning:

```go
==================
WARNING: DATA RACE // Indicates that goroutine 7 was writing
Write at 0x00c000026078 by goroutine 7:
  main.main.func1()
      /tmp/app/main.go:9 +0x4e
 
Previous read at 0x00c000026078 by main goroutine: // Indicates that the main goroutine was reading
  main.main()
      /tmp/app/main.go:10 +0x88
 
Goroutine 7 (running) created at: // Indicates when goroutine 7 was created
  main.main()
      /tmp/app/main.go:9 +0x7a
==================
```

Go always logs the following:

- The concurrent goroutines that are incriminated: here, the main goroutine and goroutine 7.
- Where accesses occur in the code: in this case, lines 9 and 10.
- When these goroutines were created: goroutine 7 was created in main().

the race detector can only be as good as our tests. Thus, we should ensure that concurrent code is tested thoroughly against data races. Second, given the possible false negatives, if we have a test to check data races, we can put this logic inside a loop. Doing so increases the chances of catching possible data races:

```go
func TestDataRace(t *testing.T) {
    for i := 0; i < 100; i++ {
        // Actual logic
    }
}
```

```go
//go:build !race
 
package main
 
import (
    "testing"
)
 
func TestFoo(t *testing.T) {
    // ...
}
 
func TestBar(t *testing.T) {
    // ...
}
```

## 11.3 #84: Not using test execution modes

While running tests, the go command can accept a set of flags to impact how tests are executed.

### 11.3.1 The parallel flag

Parallel execution mode allows us to run specific tests in parallel, which can be very useful: for example, to speed up long-running tests. We can mark that a test has to be run in parallel by calling `t.Parallel`:

In terms of execution, though, Go first runs all the sequential tests one by one. Once the sequential tests are completed, it executes the parallel tests.

```go
func TestA(t *testing.T) {
    t.Parallel()
    // ...
}
 
func TestB(t *testing.T) {
    t.Parallel()
    // ...
}
 
func TestC(t *testing.T) {
    // ...
}
```

```go
=== RUN   TestA
=== PAUSE TestA
=== RUN   TestB
=== PAUSE TestB
=== RUN   TestC
--- PASS: TestC (0.00s)
=== CONT  TestA
--- PASS: TestA (0.00s)
=== CONT  TestB
--- PASS: TestB (0.00s)
PASS
```

### 11.3.2 The -shuffle flag

A best practice while writing tests is to make them isolated. For example, they shouldn’t depend on execution order or shared variables. These hidden dependencies can mean a possible test error or, even worse, a bug that won’t be caught during testing. To prevent that, we can use the -shuffle flag to randomize tests.

```go
$ go test -shuffle=on -v .
```

However, in some cases, we want to rerun tests in the same order. For example, if tests fail during CI, we may want to reproduce the error locally. To do that, instead of passing on to the -shuffle flag, we can pass the seed used to randomize the tests. We can access this seed value when running shuffled tests by enabling verbose mode (-v):

```go
$ go test -shuffle=on -v .
-test.shuffle 1636399552801504000 // Seed value
=== RUN   TestBar
--- PASS: TestBar (0.00s)
=== RUN   TestFoo
--- PASS: TestFoo (0.00s)
PASS
ok      teivah  0.129s
```

```go
$ go test -shuffle=1636399552801504000 -v .
-test.shuffle 1636399552801504000
=== RUN   TestBar
--- PASS: TestBar (0.00s)
=== RUN   TestFoo
--- PASS: TestFoo (0.00s)
PASS
ok      teivah  0.129s
```

In general, we should be cautious about existing test flags and keep ourselves informed about new features with recent Go releases.

## 11.4 #85: Not using table-driven tests #Mistake 

Table-driven tests are an efficient technique for writing condensed tests and thus reducing boilerplate code to help us focus on what matters: the testing logic.

```go
func removeNewLineSuffixes(s string) string {
    if s == "" {
        return s
    }
    if strings.HasSuffix(s, "\r\n") {
        return removeNewLineSuffixes(s[:len(s)-2])
    }
    if strings.HasSuffix(s, "\n") {
        return removeNewLineSuffixes(s[:len(s)-1])
    }
    return s
}
```

This function removes all the leading \r\n and \n suffixes recursively. Now, let’s say we want to test this function extensively. We should at least cover the following cases:

- Input is empty.
- Input ends with \n.
- Input ends with \r\n.
- Input ends with multiple \n.
- Input ends without newlines.

The following approach creates one unit test per case:

```go
func TestRemoveNewLineSuffix_Empty(t *testing.T) {
    got := removeNewLineSuffixes("")
    expected := ""
    if got != expected {
        t.Errorf("got: %s", got)
    }
}
 
func TestRemoveNewLineSuffix_EndingWithCarriageReturnNewLine(t *testing.T) {
    got := removeNewLineSuffixes("a\r\n")
    expected := "a"
    if got != expected {
        t.Errorf("got: %s", got)
    }
}
 
func TestRemoveNewLineSuffix_EndingWithNewLine(t *testing.T) {
    got := removeNewLineSuffixes("a\n")
    expected := "a"
    if got != expected {
        t.Errorf("got: %s", got)
    }
}
 
func TestRemoveNewLineSuffix_EndingWithMultipleNewLines(t *testing.T) {
    got := removeNewLineSuffixes("a\n\n\n")
    expected := "a"
    if got != expected {
        t.Errorf("got: %s", got)
    }
}
 
func TestRemoveNewLineSuffix_EndingWithoutNewLine(t *testing.T) {
    got := removeNewLineSuffixes("a\n")
    expected := "a"
    if got != expected {
        t.Errorf("got: %s", got)
    }
}
```

However, there are two main drawbacks. First, the function names are more complex which can quickly affect the clarity of what the function is supposed to test. The second drawback is the amount of duplication among these functions, given that the structure is always the same:

1. Call removeNewLineSuffixes.
2. Define the expected value.
3. Compare the values.
4. Log an error message.


Instead, we can use table-driven tests so we write the logic only once. Table-driven tests rely on subtests, and a single test function can include multiple subtests.

```go
func TestFoo(t *testing.T) {
    t.Run("subtest 1", func(t *testing.T) { // Runs a first subtest called subtest 1
        if false {
            t.Error()
        }
    })
    t.Run("subtest 2", func(t *testing.T) { // Runs a second subtest called subtest 2
        if 2 != 2 {
            t.Error()
        }
    })
}
```


```go
--- PASS: TestFoo (0.00s)
    --- PASS: TestFoo/subtest_1 (0.00s)
    --- PASS: TestFoo/subtest_2 (0.00s)
PASS
```

```go
$ go test -run=TestFoo/subtest_1 -v // Uses the -run flag to run only subtest 1
=== RUN   TestFoo
=== RUN   TestFoo/subtest_1
--- PASS: TestFoo (0.00s)
    --- PASS: TestFoo/subtest_1 (0.00s)
```


Table-driven tests avoid boilerplate code by using a data structure containing test data together with subtests.

```go
func TestRemoveNewLineSuffix(t *testing.T) {
    tests := map[string]struct { // Defines the test data
        input    string
        expected string
    }{
        `empty`: { // Each entry in the map represents a subtest.
            input:    "",
            expected: "",
        },
        `ending with \r\n`: {
            input:    "a\r\n",
            expected: "a",
        },
        `ending with \n`: {
            input:    "a\n",
            expected: "a",
        },
        `ending with multiple \n`: {
            input:    "a\n\n\n",
            expected: "a",
        },
        `ending without newline`: {
            input:    "a",
            expected: "a",
        },
    }
    for name, tt := range tests { // Iterates over the map
        t.Run(name, func(t *testing.T) { // Runs a new subtest for each map entry
            got := removeNewLineSuffixes(tt.input)
            if got != tt.expected {
                t.Errorf("got: %s, expected: %s", got, tt.expected)
            }
        })
    }
}
```

This test solves the two drawbacks:

- ==Each test name is now a string instead of a `PascalCase` function name, making it simpler to read.==
- ==The logic is written only once and shared for all the different cases. Modifying the testing structure or adding a new test requires minimal effort.==

```go
for name, tt := range tests {
    t.Run(name, func(t *testing.T) {
        t.Parallel() // Marks the subtest to be run in parallel
        // Use tt
    })
}
```

```go
for name, tt := range tests {
    tt := tt // Shadows tt to make it local to the loop iteration
    t.Run(name, func(t *testing.T) {
        t.Parallel()
        // Use tt
    })
}
```


In summary, if multiple unit tests have a similar structure, we can mutualize them using table-driven tests. Because this technique prevents duplication, it makes it simple to change the testing logic and easier to add new use cases.

## 11.5 #86: Sleeping in unit tests #Mistake 

A _flaky_ test is a test that may both pass and fail without any code change. Flaky tests are among the biggest hurdles in testing because they are expensive to debug and undermine our confidence in testing accuracy. In Go, calling `time.Sleep` in a test can be a signal of possible flakiness. concurrent code is often tested using sleeps.

```go
type Handler struct {
    n         int
    publisher publisher
}
 
type publisher interface {
    Publish([]Foo)
}
 
func (h Handler) getBestFoo(someInputs int) Foo {
    foos := getFoos(someInputs) // Gets a slice of Foo
    best := foos[0] // Keeps the first element (checking the length of foos is omitted for the sake of simplicity)
 
    go func() {
        if len(foos) > h.n { // Keeps only the first n Foo structs
            foos = foos[:h.n]
        }
        h.publisher.Publish(foos) // Calls the Publish method
    }()
 
    return best
}
```

How can we test this function? Writing the part to assert the response is straightforward. However, what if we also want to check what is passed to Publish?

We could mock the publisher interface to record the arguments passed while calling the Publish method. Then we could sleep for a few milliseconds before checking the arguments recorded:

```go
type publisherMock struct {
    mu  sync.RWMutex
    got []Foo
}
 
func (p *publisherMock) Publish(got []Foo) {
    p.mu.Lock()
    defer p.mu.Unlock()
    p.got = got
}
 
func (p *publisherMock) Get() []Foo {
    p.mu.RLock()
    defer p.mu.RUnlock()
    return p.got
}
 
func TestGetBestFoo(t *testing.T) {
    mock := publisherMock{}
    h := Handler{
        publisher: &mock,
        n:         2,
    }
 
    foo := h.getBestFoo(42)
    // Check foo
 
    time.Sleep(10 * time.Millisecond)
    published := mock.Get()
    // Check published
}
```

This test is inherently flaky. There is no strict guarantee that 10 milliseconds will be enough
So, what are the options to improve this unit test? First, we can periodically assert a given condition using retries.

```go
func assert(t *testing.T, assertion func() bool,
    maxRetry int, waitTime time.Duration) {
    for i := 0; i < maxRetry; i++ {
        if assertion() { // Checks the assertion
            return
        }
        time.Sleep(waitTime) // Sleeps before retry
    }
    t.Fail() // Fails eventually after a number of retries
}
```

This function checks the assertion provided and fails after a certain number of retries.

```go
assert(t, func() bool {
    return len(mock.Get()) == 2
}, 30, time.Millisecond)
```

Instead of sleeping for 10 milliseconds, we sleep each millisecond and configure a maximum number of retries. Such an approach reduces the execution time if the test succeeds because we reduce the waiting interval. Therefore, implementing a retry strategy is a better approach than using passive sleeps.

Another strategy is to use channels to synchronize the goroutine publishing the Foo structs and the testing goroutine.

```go
type publisherMock struct {
    ch chan []Foo
}
 
func (p *publisherMock) Publish(got []Foo) {
    p.ch <- got // Sends the arguments received
}
 
func TestGetBestFoo(t *testing.T) {
    mock := publisherMock{
        ch: make(chan []Foo),
    }
    defer close(mock.ch)
 
    h := Handler{
        publisher: &mock,
        n:         2,
    }
    foo := h.getBestFoo(42)
    // Check foo
 
    if v := len(<-mock.ch); v != 2 { // Compares these arguments
        t.Fatalf("expected 2, got %d", v)
    }
}
```


## 11.6 #87: Not dealing with the time API efficiently #Mistake 

implement a Cache struct to hold the most recent events. This struct will expose three methods that do the following:

- Append events
- Get all the events
- Trim the events for a given duration (we will focus on this method)

Each of these methods needs to access the current time.

```GO
type Cache struct {
    mu     sync.RWMutex
    events []Event
}
 
type Event struct {
    Timestamp time.Time
    Data string
}
 
func (c *Cache) TrimOlderThan(since time.Duration) {
    c.mu.RLock()
    defer c.mu.RUnlock()
 
    t := time.Now().Add(-since) // Subtracts the given duration from the current time
    for i := 0; i < len(c.events); i++ {
        if c.events[i].Timestamp.After(t) {
            c.events = c.events[i:] // Trims the events
            return
        }
    }
}
```

How can we test this method? We could rely on the current time using `time.Now` to create the events:

```GO
func TestCache_TrimOlderThan(t *testing.T) {
    events := []Event{ // Creates events using time.Now()
        {Timestamp: time.Now().Add(-20 * time.Millisecond)},
        {Timestamp: time.Now().Add(-10 * time.Millisecond)},
        {Timestamp: time.Now().Add(10 * time.Millisecond)},
    }
    cache := &Cache{}
    cache.Add(events) // Adds these events to the cache
    cache.TrimOlderThan(15 * time.Millisecond) // Trims the events since 15 milliseconds ago
    got := cache.GetAll() // Retrieves all the events
    expected := 2
    if len(got) != expected {
        t.Fatalf("expected %d, got %d", expected, len(got))
    }
}
```

Such an approach has one main drawback: if the machine executing the test is suddenly busy, we may trim fewer events than expected. We might be able to increase the duration provided to reduce the chance of having a failing test, but doing so isn’t always possible.

The problem is related to the implementation of `TrimOlderThan`. Because it calls `time.Now()`, it’s harder to implement robust unit tests.

The first approach is to make the way to retrieve the current time a dependency of the Cache struct. In production, we would inject the _real_ implementation, whereas in unit tests, we would pass a stub, for example.

```go
type now func() time.Time
 
type Cache struct {
    mu     sync.RWMutex
    events []Event
    now    now
}
```

The now type is a function that returns a `time.Time`. In the factory function, we can pass the actual `time.Now` function this way:

```go
func NewCache() *Cache {
    return &Cache{
        events: make([]Event, 0),
        now:    time.Now,
    }
}
```


Because the now dependency remains unexported, it isn’t accessible by external clients. Furthermore, in our unit test, we can create a Cache struct by injecting a _fake_ implementation of `func() time.Time` based on a predefined time:

```go
func TestCache_TrimOlderThan(t *testing.T) {
    events := []Event{// Creates events based on specific timestamps
        {Timestamp: parseTime(t, "2020-01-01T12:00:00.04Z")},
        {Timestamp: parseTime(t, "2020-01-01T12:00:00.05Z")},
        {Timestamp: parseTime(t, "2020-01-01T12:00:00.06Z")},
    }
    cache := &Cache{now: func() time.Time { // Injects a static function to fix the time
        return parseTime(t, "2020-01-01T12:00:00.06Z")
    }}
    cache.Add(events)
    cache.TrimOlderThan(15 * time.Millisecond)
    // ...
}
 
func parseTime(t *testing.T, timestamp string) time.Time {
    // ...
}
```

---
##### USING A GLOBAL VARIABLE

Instead of using a field, we can retrieve the time via a global variable:

```go
var now = time.Now
```

In general, we should try to avoid having such a mutable shared state.

---

This solution is also extensible. However, this approach has one main drawback: the now dependency isn’t available if we, for example, create a unit test from an external package
In that case, we can use another technique. Instead of handling the time as an unexported dependency, we can ask clients to provide the current time:

```go
func (c *Cache) TrimOlderThan(now time.Time, since time.Duration) {
    // ...
}
```

```go
func (c *Cache) TrimOlderThan(t time.Time) {
    // ...
}
```

```go
cache.TrimOlderThan(time.Now().Add(time.Second))
```

```go
func TestCache_TrimOlderThan(t *testing.T) {
    // ...
    cache.TrimOlderThan(parseTime(t, "2020-01-01T12:00:00.06Z").
        Add(-15 * time.Millisecond))
    // ...
}
```

This approach is the simplest because it doesn’t require creating another type and a stub.

In general, we should be cautious about testing code that uses the time API. It can be an open door for flaky tests.

## 11.7 #88: Not using testing utility packages #Mistake 

The standard library provides utility packages for testing.

### 11.7.1 The `httptest` package

The `httptest` package ([https://pkg.go.dev/net/http/httptest](https://pkg.go.dev/net/http/httptest)) provides utilities for HTTP testing for both clients and servers.

```go
func Handler(w http.ResponseWriter, r *http.Request) {
    w.Header().Add("X-API-VERSION", "1.0")
    b, _ := io.ReadAll(r.Body)
    _, _ = w.Write(append([]byte("hello "), b...)) // Concatenates hello with the request body
    w.WriteHeader(http.StatusCreated)
}
```

```go
func TestHandler(t *testing.T) {
    req := httptest.NewRequest(http.MethodGet, "http://localhost", // Builds the request
        strings.NewReader("foo")) // Creates the response recorder
    w := httptest.NewRecorder() // Calls the handler
    Handler(w, req)
 
    if got := w.Result().Header.Get("X-API-VERSION"); got != "1.0" { // Verifies the HTTP header
        t.Errorf("api version: expected 1.0, got %s", got)
    }
 
    body, _ := ioutil.ReadAll(wordy) // Verifies the HTTP body
    if got := string(body); got != "hello foo" {
        t.Errorf("body: expected hello foo, got %s", got)
    }
 
    if http.StatusOK != w.Result().StatusCode { // Verifies the HTTP status code
        t.FailNow()
    }
}
```

Testing a handler using `httptest` doesn’t test the transport (the HTTP part). The focus of the test is calling the handler directly with a request and a way to record the response. Then, using the response recorder, we write the assertions to verify the HTTP header, body, and status code.

```go
func (c DurationClient) GetDuration(url string,
    lat1, lng1, lat2, lng2 float64) (
    time.Duration, error) {
    resp, err := c.client.Post(
        url, "application/json",
        buildRequestBody(lat1, lng1, lat2, lng2),
    )
    if err != nil {
        return 0, err
    }
 
    return parseResponseBody(resp.Body)
}
```

What if we want to test this client? One option is to use Docker and spin up a mock server to return some preregistered responses. However, this approach makes the test slow to execute. The other option is to use `httptest.NewServer` to create a local HTTP server based on a handler that we will provide.

```go
func TestDurationClientGet(t *testing.T) {
    srv := httptest.NewServer( // Starts the HTTP server
        http.HandlerFunc(
            func(w http.ResponseWriter, r *http.Request) {
                _, _ = w.Write([]byte(`{"duration": 314}`)) // Registers the handler to serve the response
            },
        ),
    )
    defer srv.Close() // Shuts down the server
 
    client := NewDurationClient()
    duration, err :=
        client.GetDuration(srv.URL, 51.551261, -0.1221146, 51.57, -0.13) // Provides the server URL
    if err != nil {
        t.Fatal(err)
    }
 
    if duration != 314*time.Second { // Verifies the response
        t.Errorf("expected 314 seconds, got %v", duration)
    }
}
```

### 11.7.2 The `iotest` package

The `iotest` package ([https://pkg.go.dev/testing/iotest](https://pkg.go.dev/testing/iotest)) implements utilities for testing readers and writers.
When implementing a custom io.Reader, we should remember to test it using iotest.TestReader. This utility function tests that a reader behaves correctly: it accurately returns the number of bytes read, fills the provided slice, and so on.

```go
func TestLowerCaseReader(t *testing.T) {
    err := iotest.TestReader(
        &LowerCaseReader{reader: strings.NewReader("aBcDeFgHiJ")}, // Provides an io.Reader
        []byte("acegi"), // Expectation
    )
    if err != nil {
        t.Fatal(err)
    }
}
```


Another use case for the `iotest` package is to make sure an application using readers and writers is tolerant to errors:

- ==`iotest.ErrReader` creates an io.Reader that returns a provided error.==
- ==`iotest.HalfReader` creates an io.Reader that reads only half as many bytes as requested from an io.Reader.==
- ==`iotest.OneByteReader` creates an io.Reader that reads a single byte for each non-empty read from an io.Reader.==
- ==`iotest.TimeoutReader` creates an io.Reader that returns an error on the second read with no data. Subsequent calls will succeed.==
- ==`iotest.TruncateWriter` creates an `io.Writer` that writes to an `io.Writer` but stops silently after _n_ bytes.==


```go
func foo(r io.Reader) error {
    b, err := io.ReadAll(r)
    if err != nil {
        return err
    }
 
    // ...
}
```

make sure our function is resilient

```go
func TestFoo(t *testing.T) {
    err := foo(iotest.TimeoutReader( // Wraps the provided io.Reader using io.TimeoutReader
        strings.NewReader(randomString(1024)),
    ))
    if err != nil {
        t.Fatal(err)
    }
}
```

```go
func readAll(r io.Reader, retries int) ([]byte, error) {
    b := make([]byte, 0, 512)
    for {
        if len(b) == cap(b) {
            b = append(b, 0)[:len(b)]
        }
        n, err := r.Read(b[len(b):cap(b)])
        b = b[:len(b)+n]
        if err != nil {
            if err == io.EOF {
                return b, nil
            }
            retries--
            if retries < 0 { // Tolerates retries
                return b, err
            }
        }
    }
}
```

```go
func foo(r io.Reader) error {
    b, err := readAll(r, 3) // Indicates up to three retries
    if err != nil {
        return err
    }
 
    // ...
}
```

## 11.8 #89: Writing inaccurate benchmarks #Mistake 

In general, we should never guess about performance. It can be pretty simple to write inaccurate benchmarks and make wrong assumptions based on them. The skeleton of a benchmark is as follows:

```GO
func BenchmarkFoo(b *testing.B) {
    for i := 0; i < b.N; i++ {
        foo()
    }
}
```

When running a benchmark, Go tries to make it match the requested benchmark time. The benchmark time is set by default to 1 second and can be changed with the -benchtime flag. b.N starts at 1; if the benchmark completes in under 1 second, b.N is increased, and the benchmark runs again until b.N roughly matches benchtime:

```go
$ go test -bench=.
cpu: Intel(R) Core(TM) i5-7360U CPU @ 2.30GHz
BenchmarkFoo-4                73          16511228 ns/op
```

We can change the benchmark time using `-benchtime`:

```go
 $ go test -bench=. -benchtime=2s
BenchmarkFoo-4               150          15832169 ns/op
```

### 11.8.1 Not resetting or pausing the timer

In some cases, we need to perform operations before the benchmark loop. These operations may take quite a while (for example, generating a large slice of data) and may significantly impact the benchmark results:

```go
func BenchmarkFoo(b *testing.B) {
    expensiveSetup()
    for i := 0; i < b.N; i++ {
        functionUnderTest()
    }
}
```

In this case, we can use the `ResetTimer` method before entering the loop:

```go
func BenchmarkFoo(b *testing.B) {
    expensiveSetup()
    b.ResetTimer() // Resets the benchmark timer
    for i := 0; i < b.N; i++ {
        functionUnderTest()
    }
}
```

What if we have to perform an expensive setup not just once but within each loop iteration?

```go
func BenchmarkFoo(b *testing.B) {
    for i := 0; i < b.N; i++ {
        expensiveSetup()
        functionUnderTest()
    }
}
```

```go
func BenchmarkFoo(b *testing.B) {
    for i := 0; i < b.N; i++ {
        b.StopTimer() // Pauses the benchmark timer
        expensiveSetup()
        b.StartTimer() // Resumes the benchmark timer
        functionUnderTest()
    }
}
```

---
##### NOTE

There’s one catch to remember about this approach: if the function under test is too fast to execute compared to the setup function, the benchmark may take too long to complete. The reason is that it would take much longer than 1 second to reach benchtime. Calculating the benchmark time is based solely on the execution time of functionUnderTest. So, if we wait a significant time in each loop iteration, the benchmark will be much slower than 1 second.

---

### 11.8.2 Making wrong assumptions about micro-benchmarks

A micro-benchmark measures a tiny computation unit, and it can be extremely easy to make wrong assumptions about it.

```go
func BenchmarkAtomicStoreInt32(b *testing.B) {
    var v int32
    for i := 0; i < b.N; i++ {
        atomic.StoreInt32(&v, 1)
    }
}
 
func BenchmarkAtomicStoreInt64(b *testing.B) {
    var v int64
    for i := 0; i < b.N; i++ {
        atomic.StoreInt64(&v, 1)
    }
}
```

```go
cpu: Intel(R) Core(TM) i5-7360U CPU @ 2.30GHz
BenchmarkAtomicStoreInt32
BenchmarkAtomicStoreInt32-4       197107742             5.682 ns/op
BenchmarkAtomicStoreInt64
BenchmarkAtomicStoreInt64-4       213917528             5.134 ns/op
```

easily take this benchmark for granted and decide to use atomic.StoreInt64 because it appears to be faster. Now, for the sake of doing a _fair_ benchmark, we reverse the order and test atomic.StoreInt64 first, followed by atomic.StoreInt32.

```go
BenchmarkAtomicStoreInt64
BenchmarkAtomicStoreInt64-4       224900722             5.434 ns/op
BenchmarkAtomicStoreInt32
BenchmarkAtomicStoreInt32-4       230253900             5.159 ns/op
```

This time, atomic.StoreInt32 has better results. What happened?

One option is to increase the benchmark time using the -benchtime option. Similar to the law of large numbers in probability theory, if we run a benchmark a large number of times, it should tend to approach its expected value

Another option is to use external tools on top of the classic benchmark tooling. For instance, the bench-stat tool, which is part of the golang.org/x repository, allows us to compute and compare statistics about benchmark executions.

```go
$ go test -bench=. -count=10 | tee stats.txt
cpu: Intel(R) Core(TM) i5-7360U CPU @ 2.30GHz
BenchmarkAtomicStoreInt32-4     234935682                5.124 ns/op
BenchmarkAtomicStoreInt32-4     235307204                5.112 ns/op
// ...
BenchmarkAtomicStoreInt64-4     235548591                5.107 ns/op
BenchmarkAtomicStoreInt64-4     235210292                5.090 ns/op
// ...
```

```go
$ benchstat stats.txt
name                time/op
AtomicStoreInt32-4  5.10ns ± 1%
AtomicStoreInt64-4  5.10ns ± 1%
```

In general, we should be cautious about micro-benchmarks. Many factors can significantly impact the results and potentially lead to wrong assumptions. Increasing the benchmark time or repeating the benchmark executions and computing stats with tools such as bench-stat can be an efficient way to limit external factors and get more accurate results, leading to better conclusions.

### 11.8.3 Not being careful about compiler optimizations

Another common mistake related to writing benchmarks is being fooled by compiler optimizations, which can also lead to wrong benchmark assumptions.

```go
const m1 = 0x5555555555555555
const m2 = 0x3333333333333333
const m4 = 0x0f0f0f0f0f0f0f0f
const h01 = 0x0101010101010101
 
func popcnt(x uint64) uint64 {
    x -= (x >> 1) & m1
    x = (x & m2) + ((x >> 2) & m2)
    x = (x + (x >> 4)) & m4
    return (x * h01) >> 56
}
```

```go
func BenchmarkPopcnt1(b *testing.B) {
    for i := 0; i < b.N; i++ {
        popcnt(uint64(i))
    }
}
```

get a surprisingly low result:

```go
cpu: Intel(R) Core(TM) i5-7360U CPU @ 2.30GHz
BenchmarkPopcnt1-4      1000000000               0.2858 ns/op
```

The problem is that the developer wasn’t careful enough about compiler optimizations. In this case, the function under test is simple enough to be a candidate for _inlining_: an optimization that replaces a function call with the body of the called function and lets us prevent a function call, which has a small footprint.

```go
func BenchmarkPopcnt1(b *testing.B) {
    for i := 0; i < b.N; i++ {
        // Empty
    }
}
```

The benchmark is now empty—which is why we got a result close to one clock cycle. To prevent this from happening, a best practice is to follow this pattern:

1. During each loop iteration, assign the result to a local variable (local in the context of the benchmark function).
2. Assign the latest result to a global variable.

```go
var global uint64 // Defines a global variable
 
func BenchmarkPopcnt2(b *testing.B) {
    var v uint64 // Defines a local variable
    for i := 0; i < b.N; i++ {
        v = popcnt(uint64(i)) // Assigns the result to the local variable
    }
    global = v // Assigns the result to the global variable
}
```

```go
cpu: Intel(R) Core(TM) i5-7360U CPU @ 2.30GHz
BenchmarkPopcnt1-4      1000000000               0.2858 ns/op
BenchmarkPopcnt2-4      606402058                1.993 ns/op
```

### 11.8.4 Being fooled by the observer effect

In physics, the observer effect is the disturbance of an observed system by the act of observation. This effect can also be seen in benchmarks and can lead to wrong assumptions about results.

```go
func calculateSum512(s [][512]int64) int64 {
    var sum int64
    for i := 0; i < len(s); i++ {
        for j := 0; j < 8; j++ { // Iterates over the first eight columns
            sum += s[i][j] // Increments sum
        }
    }
    return sum
}
 
func calculateSum513(s [][513]int64) int64 {
    // Same implementation as calculateSum512
}
```

```go
const rows = 1000
 
var res int64
 
func BenchmarkCalculateSum512(b *testing.B) {
    var sum int64
    s := createMatrix512(rows) // Creates a matrix of 512 columns
    b.ResetTimer()
    for i := 0; i < b.N; i++ {
        sum = calculateSum512(s) // Calculates the sum
    }
    res = sum
}
 
func BenchmarkCalculateSum513(b *testing.B) {
    var sum int64
    s := createMatrix513(rows) // Creates a matrix of 513 columns
    b.ResetTimer()
    for i := 0; i < b.N; i++ {
        sum = calculateSum513(s) // Calculates the sum
    }
    res = sum
}
```

```go
cpu: Intel(R) Core(TM) i5-7360U CPU @ 2.30GHz
BenchmarkCalculateSum512-4        81854             15073 ns/op
BenchmarkCalculateSum513-4       161479              7358 ns/op
```

To understand this difference, we need to understand the basics of CPU caches. In a nutshell, a CPU is composed of different caches (usually L1, L2, and L3). These caches reduce the average cost of accessing data from the main memory. In some conditions, the CPU can fetch data from the main memory and copy it to L1. In this case, the CPU tries to fetch into L1 the matrix’s subset that `calculateSum` is interested in (the first eight columns of each row). However, the matrix fits in memory in one case (513 columns) but not in the other case (512 columns).

Coming back to the benchmark, the main issue is that we keep reusing the same matrix in both cases. Because the function is repeated thousands of times, we don’t measure the function’s execution when it receives a plain new matrix. Instead, we measure a function that gets a matrix that already has a subset of the cells present in the cache. Therefore, because `calculateSum513` leads to fewer cache misses, it has a better execution time.

```go
func BenchmarkCalculateSum512(b *testing.B) {
    var sum int64
    for i := 0; i < b.N; i++ {
        b.StopTimer()
        s := createMatrix512(rows) // Creates a new matrix during each loop iteration
        b.StartTimer()
        sum = calculateSum512(s)
    }
    res = sum
}
```

```go
cpu: Intel(R) Core(TM) i5-7360U CPU @ 2.30GHz
BenchmarkCalculateSum512-4         1116             33547 ns/op
BenchmarkCalculateSum513-4          998             35507 ns/op
```

Instead of making the incorrect assumption that `calculateSum513` is faster

## 11.9 #90: Not exploring all the Go testing features #Mistake 

### 11.9.1 Code coverage

During the development process, it can be handy to see visually which parts of our code are covered by tests. We can access this information using the `-coverprofile` flag:

```go
$ go test -coverprofile=coverage.out ./...
```

```go
$ go tool cover -html=coverage.out
```

This command opens the web browser and shows the coverage for each line of code.

By default, the code coverage is analyzed only for the current package being tested.

```
/myapp
  |_ foo
    |_ foo.go
    |_ foo_test.go
  |_ bar
    |_ bar.go
    |_ bar_test.go
```

If some portion of `foo.go` is only tested in `bar_test.go`, by default, it won’t be shown in the coverage report. To include it, we have to be in the `myapp` folder and use the `-coverpkg` flag:

```go
go test -coverpkg=./... -coverprofile=coverage.out ./...
```

### 11.9.2 Testing from a different package

When writing unit tests, one approach is to focus on behaviors instead of internals. Suppose we expose an API to clients.

In Go, all the files in a folder should belong to the same package, with only one exception: a test file can belong to a _test package.

```go
package counter
 
import "sync/atomic"
 
var count uint64
 
func Inc() uint64 {
    atomic.AddUint64(&count, 1)
    return count
}
```

```go
package counter_test
 
import (
    "testing"
 
    "myapp/counter"
)
 
func TestCount(t *testing.T) {
    if counter.Inc() != 1 {
        t.Errorf("expected 1")
    }
}
```

### 11.9.3 Utility functions

When writing tests, we can handle errors differently than we do in our production code.

```go
func TestCustomer(t *testing.T) {
    customer, err := createCustomer("foo") // Creates a customer and checks for errors
    if err != nil {
        t.Fatal(err)
    }
    // ...
}
 
func createCustomer(someArg string) (Customer, error) {
    // Create customer
    if err != nil {
        return Customer{}, err
    }
    return customer, nil
}
```

```go
func TestCustomer(t *testing.T) {
    customer := createCustomer(t, "foo") // Calls the utility function and provides t
    // ...
}
 
func createCustomer(t *testing.T, someArg string) Customer {
    // Create customer
    if err != nil {
        t.Fatal(err) // Fails the test directly if we can’t create a customer
    }
    return customer
}
```

Instead of returning an error, `createCustomer` fails the test directly if it can’t create a Customer. This makes `TestCustomer` smaller to write and easier to read.

### 11.9.4 Setup and teardown

In some cases, we may have to prepare a testing environment.

```go
func TestMySQLIntegration(t *testing.T) {
    setupMySQL()
    defer teardownMySQL()
    // ...
}
```

It’s also possible to register a function to be executed at the end of a test.

```go
func TestMySQLIntegration(t *testing.T) {
    // ...
    db := createConnection(t, "tcp(localhost:3306)/db")
    // ...
}
 
func createConnection(t *testing.T, dsn string) *sql.DB {
    db, err := sql.Open("mysql", dsn)
    if err != nil {
        t.FailNow()
    }
    t.Cleanup( // Registers a function to be executed at the end of the test
        func() {
            _ = db.Close()
        })
    return db
}
```

At the end of the test, the closure provided to `t.Cleanup` is executed. This makes future unit tests easier to write because they won’t be responsible for closing the db variable.

```go
func TestMain(m *testing.M) {
    os.Exit(m.Run())
}
```

```go
func TestMain(m *testing.M) {
    setupMySQL() 
    code := m.Run()
    teardownMySQL()
    os.Exit(code)
}
```

This code spins up MySQL once before all the tests and then tears it down.

Using these practices to add setup and teardown functions, we can configure a complex environment for our tests.

## Summary #Summary 

- ==-Categorizing tests using build flags, environment variables, or short mode makes the testing process more efficient. You can create test categories using build flags or environment variables (for example, unit versus integration tests) and differentiate short- from long-running tests to decide which kinds of tests to execute.==
- ==-Enabling the -race flag is highly recommended when writing concurrent applications. Doing so allows you to catch potential data races that can lead to software bugs.==
- ==-Using the -parallel flag is an efficient way to speed up tests, especially long-running ones.==
- ==-Use the -shuffle flag to help ensure that a test suite doesn’t rely on wrong assumptions that could hide bugs.==
- ==Table-driven tests are an efficient way to group a set of similar tests to prevent code duplication and make future updates easier to handle.==
- ==Avoid sleeps using synchronization to make a test less flaky and more robust. If synchronization isn’t possible, consider a retry approach.==
- ==Understanding how to deal with functions using the time API is another way to make a test less flaky. You can use standard techniques such as handling the time as part of a hidden dependency or asking clients to provide it.==
- ==The `httptest` package is helpful for dealing with HTTP applications. It provides a set of utilities to test both clients and servers.==
- ==The `iotest` package helps write io.Reader and test that an application is tolerant to errors.==
- ==Regarding benchmarks:==
    - ==Use time methods to preserve the accuracy of a benchmark.==
    - ==Increasing benchtime or using tools such as bench-stat can be helpful when dealing with micro-benchmarks.==
    - ==Be careful with the results of a micro-benchmark if the system that ends up running the application is different from the one running the micro-benchmark.==
    - ==Make sure the function under test leads to a side effect, to prevent compiler optimizations from fooling you about the benchmark results.==
    - ==To prevent the observer effect, force a benchmark to re-create the data used by a CPU-bound function.==
- ==Use code coverage with the `-coverprofile` flag to quickly see which part of the code needs more attention.==
- ==Place unit tests in a different package to enforce writing tests that focus on an exposed behavior, not internals.==
- ==Handling errors using the `*testing.T` variable instead of the classic if err != nil makes code shorter and easier to read.==
- ==You can use setup and teardown functions to configure a complex environment, such as in the case of integration tests.==

# 12 Optimizations

in most contexts, writing readable, clear code is better than writing code that is optimized but more complex and difficult to understand. Optimization generally comes with a price

> Make it correct, make it clear, make it concise, make it fast, in that order. 
> Wes Dyer

That doesn’t mean optimizing an application for speed and efficiency is prohibited.

## 12.1 #91: Not understanding CPU caches #Mistake 

> You don’t have to be an engineer to be a racing driver, but you do have to have mechanical sympathy.

In a nutshell, when we understand how a system is designed to be used can align with the design to gain optimal performance

### 12.1.1 CPU architecture

==Modern CPUs rely on caching to speed up memory access, in most cases via three caching levels: L1, L2, and L3==. On the i5-7300, here are the sizes of these caches:

- L1: 64 KB
- L2: 256 KB
- L3: 4 MB

In the Intel family, dividing a physical core into multiple logical cores is called Hyper-Threading.

The closer a memory location is to a logical core, the faster accesses are (see [http://mng.bz/o29v](http://mng.bz/o29v)):

- L1: about 1 ns
- L2: about 4 times slower than L1
- L3: about 10 times slower than L1

The physical location of the CPU caches can also explain these differences. L1 and L2 are called _on-die_, meaning they belong to the same piece of silicon as the rest of the processor. Conversely, L3 is _off-die_, which partly explains the latency differences compared to L1 and L2.

For main memory (or RAM), average accesses are between 50 and 100 times slower than L1. We can access up to 100 variables stored on L1 for the price of a single access to the main memory. Therefore, as Go developers, one avenue for improvement is making sure our applications use CPU caches. 
### 12.1.2 Cache line

When a specific memory location is accessed (for example, by reading a variable), one of the following is likely to happen in the near future:

- ==The same location will be referenced again.==
- ==Nearby memory locations will be referenced.==

```go
func sum(s []int64) int64 {
    var total int64
    length := len(s)
    for i := 0; i < length; i++ {
        total += s[i]
    }
    return total
}
```

In this example, temporal locality applies to multiple variables: i, length, and total. Throughout the iteration, we keep accessing these variables. Spatial locality applies to code instructions and the slice s. Because a slice is backed by an array allocated contiguously in memory, in this case, accessing s[0] means also accessing s[1], s[2], and so on.

Temporal locality is part of why we need CPU caches: to speed up repeated accesses to the same variables. However, because of spatial locality, the CPU copies what we call a _cache line_ instead of copying a single variable from the main memory to a cache.

A cache line is a contiguous memory segment of a fixed size, usually 64 bytes (8 int64 variables). Whenever a CPU decides to cache a memory block from RAM, it copies the memory block to a cache line. Because memory is a hierarchy, when the CPU wants to access a specific memory location, it first checks in L1, then L2, then L3, and finally, if the location is not in those caches, in the main memory.

---
##### CPU CACHING STRATEGIES
the exact strategy when a CPU copies a memory block. different strategies exist. Sometimes caches are inclusive (for example, L2 data is also present in L3), and sometimes caches are exclusive (for example, L3 is called a _victim cache_ because it contains only data evicted from L2).

---

```go
func sum2(s []int64) int64 {
    var total int64
    for i := 0; i < len(s); i+=2 { // Iterates over every two elements
        total += s[i]
    }
    return total
}
 
func sum8(s []int64) int64 {
    var total int64
    for i := 0; i < len(s); i += 8 { // Iterates over every eight elements
        total += s[i]
    }
    return total
}
```

running a benchmark shows that sum8 is only about 10% faster on my machine: still faster, but only 10%.

The reason is related to cache lines. Here, the running time of these loops is dominated by memory accesses, not increment instruction. Three out of four accesses result in a cache hit in the first case. Therefore, the execution time difference for these two functions isn’t significant.

### 12.1.3 Slice of structs vs. struct of slices

```go
type Foo struct {
    a int64
    b int64
}
 
func sumFoo(foos []Foo) int64 { // Receives a slice of Foo
    var total int64
    for i := 0; i < len(foos); i++ { // Iterates over each Foo and sums each a field
        total += foos[i].a
    }
    return total
}
```

```go
type Bar struct {
    a []int64 // a and b are now slices.
    b []int64
}
 
func sumBar(bar Bar) int64 { // Receives a single struct
    var total int64
    for i := 0; i < len(bar.a); i++ { // Iterates over each element of a
        total += bar.a[i] // Increments the total
    }
    return total
}
```

 the goal of both functions is to iterate over each a, and doing so requires four cache lines in one case and only two cache lines in the other.

If we benchmark these two functions, `sumBar` is faster  The main reason is a better spatial locality that makes the CPU fetch fewer cache lines from memory. 

To optimize an application, we should organize data to get the most value out of each individual cache line.

### 12.1.4 Predictability

Predictability refers to the ability of a CPU to anticipate what the application will do to speed up its execution. 

```go
type node struct { // Linked list data structure
    value int64
    next  *node
}
 
func linkedList(n *node) int64 {
    var total int64 
    for n != nil { // Iterates over each node
        total += n.value // Increments total
        n = n.next
    }
    return total
}
```


```go
func sum2(s []int64) int64 {
    var total int64
    for i := 0; i < len(s); i+=2 { // Iterates over every two elements
        total += s[i]
    }
    return total
}
```


The two data structures have the same spatial locality, so we may expect a similar execution time for these two functions. But the function iterating on the slice is significantly faster  What’s the reason?

==To understand this, we have to discuss the concept of striding. Striding relates to how CPUs work through data. There are three different types of strides (see figure 12.6):==

- ==_Unit stride_—All the values we want to access are allocated contiguously: for example, a slice of int64 elements. This stride is predictable for a CPU and the most efficient because it requires a minimum number of cache lines to walk through the elements.==
- ==_Constant stride_—Still predictable for the CPU: for example, a slice that iterates over every two elements. This stride requires more cache lines to walk through data, so it’s less efficient than a unit stride.==
- ==_Non-unit stride_—A stride the CPU can’t predict: for example, a linked list or a slice of pointers. Because the CPU doesn’t know whether data is allocated contiguously, it won’t fetch any cache lines.==

For sum2, we face a constant stride. However, for the linked list, we face a non-unit stride. Even though we know the data is allocated contiguously, the CPU doesn’t know that. Therefore, it can’t predict how to walk through the linked list.

Because of the different stride and similar spatial locality, iterating over a linked list is significantly slower than a slice of values. We should generally favor unit strides over constant strides because of the better spatial locality. 

CPU caches are fast but significantly smaller than the main memory. Therefore, a CPU needs a strategy to fetch a memory block to a cache line. This policy is called _cache placement policy_ and can significantly impact performance.

### 12.1.5 Cache placement policy

```go
func calculateSum512(s [][512]int64) int64 { // Receives a matrix of 512 columns
    var sum int64
    for i := 0; i < len(s); i++ {
        for j := 0; j < 8; j++ {
            sum += s[i][j]
        }
    }
    return sum
}
 
func calculateSum513(s [][513]int64) int64 { // Receives a matrix of 513 columns
    // Same implementation as calculateSum512
}
```

When these two functions are benchmarked each time with a new matrix, we don’t observe any difference. However, if we keep reusing the same matrix, calculateSum513 is about 50% faster on my machine. The reason lies in CPU caches and how a memory block is copied to a cache line.

When a CPU decides to copy a memory block and place it into the cache, it must follow a particular strategy. Assuming an L1D cache of 32 KB and a cache line of 64 bytes, if a block is placed randomly into L1D, the CPU will have to iterate over 512 cache lines in the worst case to read a variable. This kind of cache is called _fully associative_.

today’s most widely used option: _set-associative cache_, which relies on cache partitioning.

With the set-associative cache policy, a cache is partitioned into sets. We assume the cache is two-way set associative, meaning each set contains two lines. A memory block can belong to only one set, and the placement is determined by its memory address.

The cache replacement policy depends on the CPU, but it’s usually a pseudo-LRU policy (a real LRU [least recently used] would be too complex to handle).

Instead of using CPU caches from one execution to another, the benchmark will lead to more cache misses. This type of cache miss is called a _conflict miss_: a miss that wouldn’t occur if the cache wasn’t partitioned. All the variables we iterate belong to a memory block whose set index is 00. Therefore, we use only one cache set instead of having a distribution across the entire cache.

In summary, we have to be aware that modern caches are partitioned. Depending on the striding, in some cases only one set is used, which may harm application performance and lead to conflict misses. This kind of stride is called a critical stride. For performance-intensive applications, we should avoid critical strides to get the most out of CPU caches.

## 12.2 #92: Writing concurrent code that leads to false sharing #Mistake 

```go
type Input struct {
    a int64
    b int64
}
 
type Result struct {
    sumA int64
    sumB int64
}
```

The goal is to implement a count function that receives a slice of Input and computes the following:

- The sum of all the `Input.a` fields into `Result.sumA`
- The sum of all the `Input.b` fields into `Result.sumB`

```go
func count(inputs []Input) Result {
    wg := sync.WaitGroup{}
    wg.Add(2)
 
    result := Result{} // Initializes the result struct
 
    go func() {
        for i := 0; i < len(inputs); i++ {
            result.sumA += inputs[i].a // Computes sumA
        }
        wg.Done()
    }()
 
    go func() {
        for i := 0; i < len(inputs); i++ {
            result.sumB += inputs[i].b // Computes sumB
        }
        wg.Done()
    }()
 
    wg.Wait()
    return result
}
```

This example is fine from a concurrency perspective. For instance, it doesn’t lead to a data race, because each goroutine increments its own variable. But this example illustrates the false sharing concept that degrades expected performance.

Because `sumA` and `sumB` are allocated contiguously, in most cases (seven out of eight), both variables are allocated to the same memory block.

Because these cache lines are replicated, one of the goals of the CPU is to guarantee cache coherency. For example, if one goroutine updates `sumA` and another reads `sumA` (after some synchronization), we expect our application to get the latest value.

However,  Both goroutines access their own variables, not a shared one. We might expect the CPU to know about this and understand that it isn’t a conflict, but this isn’t the case. When we write a variable that’s in a cache, the granularity tracked by the CPU isn’t the variable: it’s the cache line.

When a cache line is shared across multiple cores and at least one goroutine is a writer, the entire cache line is invalidated. This happens even if the updates are logically independent . This is the problem of false sharing, and it degrades performance.

---

##### NOTE

Internally, a CPU uses the MESI protocol to guarantee cache coherency. It tracks each cache line, marking it modified, exclusive, shared, or invalid (MESI).

---

One of the most important aspects to understand about memory and caching is that sharing memory across cores isn’t real—it’s an illusion.

So how do we solve false sharing? There are two main solutions.

The first solution is to use the same approach we’ve shown but ensure that `sumA` and `sumB` aren’t part of the same cache line. For example, we can update the Result struct to add _padding_ between the fields. Padding is a technique to allocate extra memory. Because an int64 requires an 8-byte allocation and a cache line 64 bytes long, we need 64 – 8 = 56 bytes of padding:

```go
type Result struct {
    sumA int64
    _    [56]byte // Padding
    sumB int64
}
```

The second solution is to rework the structure of the algorithm. For example, instead of having both goroutines share the same struct, we can make them communicate their local result via channels. The result benchmark is roughly the same as with padding.

In summary, we must remember that sharing memory across goroutines is an illusion at the lowest memory levels. False sharing occurs when a cache line is shared across two cores when at least one goroutine is a writer.

## 12.3 #93: Not taking into account instruction-level parallelism #Mistake 

```go
const n = 1_000_000
 
func add(s [2]int64) [2]int64 {
    for i := 0; i < n; i++ {
        s[0]++
        if s[0]%2 == 0 {
            s[1]++
        }
    }
    return s
}
```

```go
s[0]++
if s[0]%2 == 0 {
    s[1]++
}
```

data hazards prevent instructions from being executed simultaneously.

This sequence contains one control hazard because of the if statement. However, as discussed, it’s the scope of the CPU to optimize the execution and predict what branch should be taken. There are also multiple data hazards.

 the only independent instructions are the s[0] check and the s[1] increment, so these two instruction sets can be executed in parallel thanks to branch prediction.

```go
func add(s [2]int64) [2]int64 { // First version
    for i := 0; i < n; i++ {
        s[0]++
        if s[0]%2 == 0 {
            s[1]++
        }
    }
    return s
}
 
func add2(s [2]int64) [2]int64 { // Second version
    for i := 0; i < n; i++ {
        v := s[0] // Introduces a new variable to fix the s[0] value
        s[0] = v + 1
        if v%2 != 0 {
            s[1]++
        }
    }
    return s
}
```

## 12.4 #94: Not being aware of data alignment #Mistake 

Data alignment is a way to arrange how data is allocated to speed up memory accesses by the CPU. Not being aware of this concept can lead to extra memory consumption and even degraded performance.

```GO
var i int32
var j int64
```

Without data alignment, on a 64-bit architecture The j variable allocation could be spread over two words. If the CPU wanted to read j, it would require two memory accesses instead of one.

To prevent such a case, a variable’s memory address should be a multiple of its own size. This is the concept of data alignment. In Go, the alignment guarantees are as follows:

- ==byte, uint8, int8: 1 byte==
- ==uint16, int16: 2 bytes==
- ==uint32, int32, float32: 4 bytes==
- ==uint64, int64, float64, complex64: 8 bytes==
- ==complex128: 16 bytes==

```go
type Foo struct {
    b1 byte
    i  int64
    b2 byte
}
```

Because a struct’s size must be a multiple of the word size (8 bytes), its address isn’t 17 bytes but 24 bytes total. During the compilation, the Go compiler adds padding to guarantee data alignment:

```go
type Foo struct {
    b1 byte
    _  [7]byte // Added by the compiler
    i  int64
    b2 byte
    _  [7]byte // Added by the compiler
}
```

Every time a Foo struct is created, it requires 24 bytes in memory, but only 10 bytes contain data—the remaining 14 bytes are padding. Because a struct is an atomic unit, it will never be reorganized, even after a garbage collection (GC); it will always occupy 24 bytes in memory. Note that the compiler doesn’t rearrange the fields; it only adds padding to guarantee data alignment.

How can we reduce the amount of memory allocated? The rule of thumb is to reorganize a struct so that its fields are sorted by type size in descending order.

```go
type Foo struct {
    i  int64
    b1 byte
    b2 byte
}
```

reorganizing the fields of a Go struct to sort them by size in descending order prevents padding. Preventing padding means allocating more compact structs, possibly leading to optimizations such as reducing the frequency of GCs and better spatial locality.

## 12.5 #95: Not understanding stack vs. heap #Mistake 

In Go, a variable can be allocated either on the stack or on the heap.

### 12.5.1 Stack vs. heap

The stack is the default memory; it’s a last-in, first-out (LIFO) data structure that stores all the local variables for a specific goroutine. When a goroutine starts, it gets 2 KB of contiguous memory as its stack space . However, this size isn’t fixed at run time and can grow and shrink as necessary

When Go enters a function, a stack frame is created, representing an interval in memory that only the current function can access.

```go
func main() {
    a := 3
    b := 2
 
    c := sumValue(a, b)
    println(c)
}
 
//go:noinline
func sumValue(x, y int) int {
    z := x + y
    return z
}
```

When a function returns, Go doesn’t take time to deallocate the variables to reclaim free space. But these previous variables can no longer be accessed, and when new variables from the parent function are allocated to the stack, they replace earlier allocations. In a sense, a stack is self-cleaning; it doesn’t require an additional mechanism such as a GC.

```go
func main() {
    a := 3
    b := 2
 
    c := sumPtr(a, b)
    println(*c)
}
 
//go:noinline
func sumPtr(x, y int) *int {
    z := x + y
    return &z
}
```

A memory heap is a pool of memory shared by all the goroutines.
If the compiler cannot prove that a variable _isn’t_ referenced after the function returns, the variable is allocated on the heap.

a stack is self-cleaning and is accessed by a single goroutine. Conversely, the heap must be cleaned by an external system: the GC. The more heap allocations are made, the more we pressure the GC. When the GC runs, it uses 25% of the available CPU capacity and may create milliseconds of “stop the world” latency

allocating on the stack is faster for the Go runtime because it’s trivial: a pointer references the following available memory address. Conversely, allocating on the heap requires more effort to find the right place and hence takes more time.

```go
var globalValue int
var globalPtr *int
 
func BenchmarkSumValue(b *testing.B) {
    b.ReportAllocs()
    var local int
    for i := 0; i < b.N; i++ {
        local = sumValue(i, i)
    }
    globalValue = local
}
 
func BenchmarkSumPtr(b *testing.B) {
    b.ReportAllocs()
    var local *int
    for i := 0; i < b.N; i++ {
        local = sumPtr(i, i)
    }
    globalValue = *local
}
```

```go
BenchmarkSumValue-4   992800992    1.261 ns/op   0 B/op   0 allocs/op
BenchmarkSumPtr-4     82829653     14.84 ns/op   8 B/op   1 allocs/op
```

- B/op: how many bytes per operation allocated
- allocs/op: how many allocations per operation

### 12.5.2 Escape analysis

_Escape analysis_ refers to the work performed by the compiler to decide whether a variable should be allocated on the stack or the heap. Let’s look at the main rules.

When an allocation cannot be done on the stack, it is done on the heap. Even though this sounds like a simplistic rule, it’s important to remember. For example, if the compiler cannot prove that a variable isn’t referenced after a function returns, this variable is allocated on the heap.

In general, _sharing up_ escapes to the heap.

But what about the opposite situation? What if we accept a pointer, as in the following example?

```go
func main() {
    a := 3
    b := 2
    c := sum(&a, &b)
    println(c)
}
 
//go:noinline
func sum(x, y *int) int {
    return *x + *y
}
```

Despite being part of another stack frame, the x and y variables reference valid addresses. Therefore, a and b won’t have to be escaped; they can stay on the stack. In general, _sharing down_ stays [](https://livebook.manning.com/book/100-go-mistakes-and-how-to-avoid-them/chapter-12/)on the stack.

The following are other cases in which a variable can be escaped to the heap:

- Global variables, because multiple goroutines can access them.
- A pointer sent to a channel: Here, foo escapes to the heap.

```go
type Foo struct{ s string }
ch := make(chan *Foo, 1)
foo := &Foo{s: "x"}
ch <- foo
```

A variable referenced by a value sent to a channel:

```go
type Foo struct{ s *string }
ch := make(chan Foo, 1)
s := "x"
bar := Foo{s: &s}
ch <- bar
```

- If a local variable is too large to fit on the stack.
- If the size of a local variable is unknown. For example, s := make([]int, 10) may not escape to the heap, but s := make([]int, n) will, because its size is based on a variable.
- If the backing array of a slice is reallocated using append.

heap allocations are more complex for the Go runtime to handle and require an external system with the GC to deallocate data. Heap management can account for up to 20% or 30% of the total CPU time consumed in some data-intensive applications. On the other hand, a stack is self-cleaning and local to a single goroutine, making allocations faster. Therefore, optimizing memory allocation can have a great return on investment.

In general, sharing down stays on the stack, whereas sharing up escapes to the heap.

## 12.6 #96: Not knowing how to reduce allocations #Mistake 

Reducing allocations is a common optimization technique to speed up Go applications.

- Under-optimized string concatenation (mistake #39): using `strings.Builder` instead of the + operator to concatenate strings.
- Useless string conversions (mistake #40): whenever possible, avoid having to convert []byte into strings.
- Inefficient slice and map initialization (mistakes #21 and #27): pre-allocate slices and maps if the length is already known.
- Better data struct alignment to reduce struct size.

As part of this section, we discuss three common approaches to reduce allocations:

- ==Changing our API==
- ==Relying on compiler optimizations==
- ==Using tools such as `sync.Pool`==

### 12.6.1 API changes

```go
type Reader interface {
    Read(p []byte) (n int, err error)
}
```

```go
type Reader interface {
    Read(n int) (p []byte, err error)
}
```

Semantically, there is nothing wrong with this. But the returned slice would automatically escape to the heap in this case.

The Go designers used the sharing-down approach to prevent automatically escaping the slice to the heap. Therefore, it’s up to the caller to provide a slice. That doesn’t necessarily mean this slice won’t be escaped: the compiler may have decided that this slice cannot stay on the stack. However, it’s up to the caller to handle it, not a constraint caused by calling the Read method.

### 12.6.2 Compiler optimizations

One of the goals of the Go compiler is to optimize our code if possible. 
In Go, we can’t define a map using a slice as a key type. In some cases, especially in applications doing I/O, we may receive []byte data that we would like to use as a key.

```go
type cache struct {
    m map[string]int // Holds a map of strings
}
 
func (c *cache) get(bytes []byte) (v int, contains bool) {
    key := string(bytes) // Converts from []byte to string
    v, contains = c.m[key] // Queries the map using the string value
    return
}
```

```go
func (c *cache) get(bytes []byte) (v int, contains bool) {
    v, contains = c.m[string(bytes)] // Queries the map directly using string(bytes)
    return
}
```


Despite this being almost the same code directly instead of passing a variable), the compiler will avoid doing this bytes-to-string conversion. Hence, the second version is faster than the first.

### 12.6.3 `sync.Pool` 

Another avenue for improvement if we want to tackle the number of allocations is using  `sync.Pool`.  `sync.Pool` isn’t a cache: there’s no fixed size or maximum capacity that we can set. Instead, it’s a pool to reuse common objects.

```go
func write(w io.Writer) {
    b := getResponse() // Receives a []byte response
    _, _ = w.Write(b) // Writes to the io.Writer
}
```

What if we want to reduce the number of allocations by reusing this slice?
Creating a `sync.Pool` requires a func() any factory function;  `sync.Pool` exposes two methods:

- Get() any—Gets an object from the pool
- Put(any)—Returns an object to the pool

Using Get either creates a new object if the pool is empty or reuses an object, otherwise. Then, after using the object, we can put it back into the pool using Put

When are objects drained from the pool? There’s no specific method to do this: it relies on the GC. After each GC, objects from the pool are destroyed.

```go
var pool = sync.Pool{
    New: func() any { // Creates a pool and sets the factory function
        return make([]byte, 1024)
    },
}
 
func write(w io.Writer) {
    buffer := pool.Get().([]byte) // Gets a []byte from the pool or creates one
    buffer = buffer[:0] // Resets the buffer
    defer pool.Put(buffer) // Puts the buffer back into the pool
 
    getResponse(buffer) // Writes the response to the provided buffer
    _, _ = w.Write(buffer)
}
```

In summary, if we frequently allocate many objects of the same type, we can consider using `sync.Pool`. It is a set of temporary objects that can help us prevent reallocating the same kind of data repeatedly. And `sync.Pool` is safe for use by multiple goroutines simultaneously.

## 12.7 #97: Not relying on inlining

**_Inlining_** refers to replacing a function call with the body of the function.

```go
func main() {
    a := 3
    b := 2
    s := sum(a, b)
    println(s)
}
 
func sum(a int, b int) int { // Inlines the function
    return a + b
}
```

```go
$ go build -gcflags "-m=2"
./main.go:10:6: can inline sum with cost 4 as:
    func(int, int) int { return a + b }
...
./main.go:6:10: inlining call to sum func(int, int) int { return a + b }
```

The compiler decided to inline the call to sum. Hence, the previous code is replaced by the following:

```go
func main() {
    a := 3
    b := 2
    s := a + b // Replaces the call to sum with its body
    println(s)
}
```

Inlining only works for functions with a certain complexity, also known as an _inlining budget_. Otherwise, the compiler will inform us that the function is too complex to be inlined:

```go
./main.go:10:6: cannot inline foo: function too complex:
    cost 84 exceeds budget 80
```

Inlining has two main benefits. First, it removes the overhead of a function call 
Second, it allows the compiler to proceed to further optimizations after inlining a function, the compiler can decide that a variable it was initially supposed to escape on the heap may stay on the stack.

The question is, if this optimization is applied automatically by the compiler, why should we care about it as Go developers? The answer lies in the concept of mid-stack inlining.
Mid-stack inlining is about inlining functions that call other functions.

```go
func main() {
    foo()
}
 
func foo() {
    x := 1
    bar(x)
}
```

```go
func main() {
    x := 1 // Replaced with the body of foo
    bar(x)
}
```

can now optimize an application using the concept of fast-path inlining to distinguish between fast and slow paths. 

```go
func (m *Mutex) Lock() {
    if atomic.CompareAndSwapInt32(&m.state, 0, mutexLocked) {
        // Mutex isn't locked
        if race.Enabled {
            race.Acquire(unsafe.Pointer(m))
        }
        return
    }
 
    // Mutex is already locked
    var waitStartTime int64
    starving := false
    awoke := false
    iter := 0
    old := m.state
    for {
        // ... // Complex logic
    }
    if race.Enabled {
        race.Acquire(unsafe.Pointer(m))
    }
}
```

This optimization technique is about distinguishing between fast and slow paths. If a fast path can be inlined but not a slow one, we can extract the slow path inside a dedicated function. Hence, if the inlining budget isn’t exceeded, our function is a candidate for inlining.

## 12.8 #98: Not using Go diagnostics tooling #Mistake 

### 12.8.1 Profiling

Profiling provides insights into the execution of an application. It allows us to resolve performance issues, detect contention, locate memory leaks, and more. These insights can be collected via several profiles:

- CPU—Determines where an application spends its time
- Goroutine—Reports the stack traces of the ongoing goroutines
- Heap—Reports heap memory allocation to monitor current memory usage and check for possible memory leaks
- Mutex—Reports lock contentions to see the behaviors of the mutexes used in our code and whether an application spends too much time in locking calls
- Block—Shows where goroutines block waiting on synchronization primitives

Profiling is achieved via instrumentation using a tool called a profiler: in Go, `pprof`

#### Enabling `pprof`

```go
package main
 
import (
    "fmt"
    "log"
    "net/http"
    _ "net/http/pprof" // Blank import to pprof
)
 
func main() {
    http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) { // Exposes an HTTP endpoint
        fmt.Fprintf(w, "")
    })
    log.Fatal(http.ListenAndServe(":80", nil))
}
```


#### CPU profiling

The CPU profiler relies on the OS and signaling. When it is activated, the application asks the OS to interrupt it every 10 ms by default via a SIGPROF signal. When the application receives a SIGPROF, it suspends the current activity and transfers the execution to the profiler. The profiler collects data such as the current goroutine activity and aggregates execution statistics that we can retrieve. Then it stops, and the execution resumes until the next SIGPROF.

After 30 seconds, we download the results of the CPU profiler.
From this file, we can navigate to the results using go tool:

```go
$ go tool pprof -http=:8080 <file>
```


Thanks to this data, we can get a general idea of how an application behaves:

- ==Too many calls to `runtime.mallogc` can mean an excessive number of small heap allocations that we can try to minimize.==
- ==Too much time spent in channel operations or mutex locks can indicate excessive contention that is harming the application’s performance.==
- ==Too much time spent on `syscall.Read` or `syscall.Write` means the application spends a significant amount of time in Kernel mode. Working on I/O buffering may be an avenue for improvement.==

#### Heap profiling

Heap profiling allows us to get statistics about the current heap usage. Like CPU profiling, heap profiling is sample-based. By default, samples are profiled at one allocation for every 512 KB of heap allocation.

different sample types:

- ==`alloc_objects`—Total number of objects allocated==
- ==`alloc_space`—Total amount of memory allocated==
- ==`inuse_objects`—Number of objects allocated and not yet released==
- ==`inuse_space`—Amount of memory allocated and not yet released==

Another very helpful capability with heap profiling is tracking memory leaks. With a GC-based language, the usual procedure is the following:

1. ==Trigger a GC.==
2. ==Download heap data.==
3. ==Wait for a few seconds/minutes.==
4. ==Trigger another GC.==
5. ==Download another heap data.==
6. ==Compare.==

Forcing a GC before downloading data is a way to prevent false assumptions.


#### Goroutines profiling

The goroutine profile reports the stack trace of all the current goroutines in an application.

This kind of information is also beneficial if we suspect goroutine leaks.

#### Block profiling

The block profile reports where ongoing goroutines block waiting on synchronization primitives. Possibilities include

- ==Sending or receiving on an unbuffered channel==
- ==Sending to a full channel==
- ==Receiving from an empty channel==
- ==Mutex contention==
- ==Network or filesystem waits==

If we suspect that our application spends significant time waiting for locking mutexes, thus harming execution, we can use mutex profiling. It’s accessible via /debug/pprof/mutex.
This profile works in a manner similar to that for blocking. It’s disabled by default:

### 12.8.2 Execution tracer

The execution tracer is a tool that captures a wide range of runtime events with go tool to make them available for visualization. It is helpful for the following:

- ==Understanding runtime events such as how the GC performs==
- ==Understanding how goroutines execute==
- ==Identifying poorly parallelized execution==

```go
$ go test -bench=. -v -trace=trace.out
```

This command creates a `trace.out` file that we can open using go tool:

```go
$ go tool trace trace.out
2021/11/26 21:36:03 Parsing trace...
2021/11/26 21:36:31 Splitting trace...
2021/11/26 21:37:00 Opening browser. Trace viewer is listening on
    http://127.0.0.1:54518
```

The web browser opens, and we can click View Trace to see all the traces during a specific timeframe

hat are the main differences compared to the data we can get from user-level traces?

- ==CPU profiling:==
    - ==Sample-based.==
    - ==Per function.==
    - ==Doesn’t go below the sampling rate (10 ms by default).==
- ==User-level traces:==
    - ==Not sample-based.==
    - ==Per-goroutine execution (unless we use the runtime/trace package).==
    - ==Time executions aren’t bound by any rate.==

In summary, the execution tracer is a powerful tool for understanding how an application performs

## 12.9 #99: Not understanding how the GC works #Mistake 

### 12.9.1 Concepts

A GC keeps a tree of object references. The Go GC is based on the mark-and-sweep algorithm, which relies on two stages:

- ==_Mark stage_—Traverses all the objects of the heap and marks whether they are still in use==
- ==_Sweep stage_—Traverses the tree of references from the root and deallocates blocks of objects that are no longer referenced==

When a GC runs, it first performs a set of actions that lead to _stopping the world_ (two stop-the-worlds per GC, to be precise). That is, all the available CPU time is used to perform the GC, putting our application code on hold. Following these steps, it starts the world again, resuming our application but also running a concurrent phase. For that reason, the Go GC is called _concurrent mark-and-sweep_: it aims to reduce the number of stop-the-world operations per GC cycle and mostly run concurrently alongside our application.

How will Go tackle the fact that the large heap is only helpful when the application starts, not after that? This is handled as part of the GC with a so-called _periodic scavenger_. After a certain time, the GC detects that such a large heap is no longer necessary, so it frees some memory and returns it to the OS.

The important question is, when will a GC cycle run? Compared to other languages such as Java, the Go configuration remains reasonably simple. It relies on a single environment variable: GOGC. This variable defines the percentage of the heap growth since the last GC before triggering another GC; the default value is 100%.

## 12.10 #100: Not understanding the impacts of running Go in Docker and Kubernetes #Mistake 

In summary, let’s remember that currently, Go isn’t CFS-aware. GOMAXPROCS is based on the host machine rather than on the defined CPU limits. Consequently, we can reach a state where the CPU is throttled, leading to long pauses and substantial effects such as a significant latency increase. Until Go becomes CFS-aware, one solution is to rely on `automaxprocs` to automatically set GOMAXPROCS to the defined quota.

## Summary #Summary 

- ==Understanding how to use CPU caches is important for optimizing CPU-bound applications because the L1 cache is about 50 to 100 times faster than the main memory.==
- ==Being conscious of the cache line concept is critical to understanding how to organize data in data-intensive applications. A CPU doesn’t fetch memory word by word; instead, it usually copies a memory block to a 64-byte cache line. To get the most out of each individual cache line, enforce spatial locality.==
- ==Making code predictable for the CPU can also be an efficient way to optimize certain functions. For example, a unit or constant stride is predictable for the CPU, but a non-unit stride (for example, a linked list) isn’t predictable.==
- ==To avoid a critical stride, hence utilizing only a tiny portion of the cache, be aware that caches are partitioned.==
- ==Knowing that lower levels of CPU caches aren’t shared across all the cores helps avoid performance-degrading patterns such as false sharing while writing concurrency code. Sharing memory is an illusion.==
- ==Use instruction-level parallelism (ILP) to optimize specific parts of your code to allow a CPU to execute as many parallel instructions as possible. Identifying data hazards is one of the main steps.==
- ==You can avoid common mistakes by remembering that in Go, basic types are aligned with their own size. For example, keep in mind that reorganizing the fields of a struct by size in descending order can lead to more compact structs (less memory allocation and potentially a better spatial locality).==
- ==Understanding the fundamental differences between heap and stack should also be part of your core knowledge when optimizing a Go application. Stack allocations are almost free, whereas heap allocations are slower and rely on the GC to clean the memory.==
- ==Reducing allocations is also an essential aspect of optimizing a Go application. This can be done in different ways, such as designing the API carefully to prevent sharing up, understanding the common Go compiler optimizations, and using `sync.Pool`.==
- ==Use the fast-path inlining technique to efficiently reduce the amortized time to call a function.==
- ==Rely on profiling and the execution tracer to understand how an application performs and the parts to optimize.==
- ==Understanding how to tune the GC can lead to multiple benefits such as handling sudden load increases more efficiently.==
- ==To help avoid CPU throttling when deployed in Docker and Kubernetes, keep in mind that Go isn’t CFS-aware.==