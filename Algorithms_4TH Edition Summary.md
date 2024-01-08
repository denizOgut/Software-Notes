
# FUNDAMENTALS

## Algorithms

The term "algorithm" is used in computer science to describe a finite, deterministic, and effective problem-solving method suitable for implementation as a computer program.

We can define an algorithm by describing a procedure for solving a problem in natural language or by writing a computer program that implements the procedure.

### English-language description

Compute the greatest common divisor of two nonnegative integers p and q as follows: if q is 0, the answer is p. If not, divide p by q and take remainder r. The answer is the greatest common divisor of q and r.

### Java language description

```java
public static int gcd(int p, int q) {
    if (q == 0) return p;
    int r = p % q;
    return gcd(q, r);
}
```

Most algorithms of interest involve organizing the data involved in the computation. Such organization leads to "data structures," which are also central objects of study in computer science. Algorithms and data structures go hand in hand.

When developing a huge or complex computer program, a great deal of effort must go into understanding and defining the problem to be solved, managing its complexity, and decomposing it into smaller subtasks that can be implemented easily.

## Summary Of Topics

- **Fundamentals (CHAPTER 1):** The basic principles and methodology that we use to implement, analyze, and compare algorithms.
    
- **Sorting algorithms (CHAPTER 2):** For rearranging arrays in order are of fundamental importance.
    
- **Searching algorithms (CHAPTER 3):** For finding specific items among large collections of items are also of fundamental importance.
    
- **Graphs (CHAPTER 4):** Are sets of objects and connections possibly with weights and orientation. Graphs are useful models for a vast number of difficult and important problems, and the design of algorithms for processing graphs is a major field of study.
    
- **Strings (CHAPTER 5):** Are an essential data type in modern computing applications.
    
- **Context (Chapter 6):** Helps us relate material in the book to several other advanced fields of study, including scientific computing, operations research, and the theory of computing.

# 1.1 BASIC PROGRAMMING MODEL

```java
import java.util.Arrays;

public class BasicProgrammingModel {
    public static int indexOf(int[] a, int key) {
        int low = 0;
        int high = a.length - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (key < a[mid]) high = mid - 1;
            else if (key > a[mid]) low = mid + 1;
            else return mid;
        }

        return -1;
    }
}
```

## Expression

An expression is a literal, a variable, or a sequence of operations on literals and/or variables that produces a value.

- `!` has the highest precedence, followed by `&&` and then `||`. Generally, operators of the same precedence are applied left to right.

## Type Conversion

Numbers are automatically promoted to a more inclusive type if no information is lost.

Other Primitive Types:

- 64-bit integers, with arithmetic operations (`long`)
- 16-bit integers, with arithmetic operations (`short`)
- 16-bit integers, with arithmetic operations (`char`)
- 8-bit integers, with arithmetic operations (`byte`)
- 32-bit single-precision real numbers, again with arithmetic operations (`float`)

## Statements

Statements define the computation by creating and manipulating variables, assigning data-type values to them, and blocks, sequences of statements within curly braces.

- Declarations create variables of a specified type and name them with identifiers.
- Assignments associate a data-type value with a variable.
- Conditionals provide for a simple change in the flow of execution—execute the statements in one of two blocks, depending on a specific condition.
- Loops provide for a more profound change in the flow of execution—execute the statement in a block as long as a given condition is true.
- Calls and returns relate to static methods, which provide another way to change the flow of execution and to organize code.

### Declarations

A declaration statement associates a variable name with a type at compile time. The scope of a variable is the part of the program where it is defined.

### Assignments

An assignment statement associates a data-type value (defined by an expression) with a variable -> `c = a + b;`

### Break And Continue

- The `break` statement, which immediately exits the loop.
- The `continue` statement, which immediately begins the next iteration of the loop.

## Arrays

Arrays store a sequence of values that are all of the same type. We use numbers to refer to individual values in an array and then index them.

### Creating and Initializing An Array

Declare the array name and type, create the array, and initialize the array values.

```java
int[] a = {1, 2, 3, 4, 5};
```

### Aliasing

An array name refers to the whole array. If we assign one array name to another, then both refer to the same array.

```java
int[] a = new int[n];
// ...
a[i] = 1234;
// ...
int[] b = a;
// ...
b[i] = 5678; // a[i] is now 5678
```

If your intent is to make a copy of an array, then you need to declare, create, and initialize a new array and then copy all of the entries in the original array to the new array.

### Two-Dimensional Arrays

A two-dimensional array in Java is an array of one-dimensional arrays.

```java
double[][] a = new double[m][n];
```

We refer to such an array as an m-by-n array. By convention, the first dimension is the number of rows, and the second is the number of columns.

## Static Methods

The modifier "static" distinguishes these methods from instance methods.

### Properties Of Methods

- Arguments are passed by value.
- The only difference between an argument variable and a local variable is that the argument variable is initialized with the argument value provided by the calling code.
- The method works with the value of its arguments, not the arguments themselves.
- Method names can be overloaded.
- A method has a single return value but may have multiple return statements.
- A method can have side effects. A void static method is said to produce side effects (consume input, produce output, change entries in an array, or otherwise change the state of the system).

### Recursion

A method can call itself. There are three important rules for developing recursive programs:

1. The recursion has a base case—always include a conditional statement as the first statement in the program that has a return.
2. Recursive calls must address subproblems that are smaller in some sense so that recursive calls converge to the base case.
3. Recursive calls should not address subproblems that overlap.

```java
// Recursive Binary Search
public static int indexOf(int[] a, int key, int low, int high) {
    if (low > high) return -1;
    int mid = low + (high - low) / 2;
    if (key < a[mid]) return indexOf(a, key, low, mid - 1);
    else if (key > a[mid]) return indexOf(a, key, mid + 1, high);
    else return mid;
}
```

## Basic Programming Model

A library of static methods is a set of static methods that are defined in a Java class by creating a file with the keywords `public class` followed by the class name, followed by the static methods, enclosed in braces, kept in a file with the same name as the class and a `.java` extension.

## Modular Programming

- Work with modules of reasonable size, even in programs involving a large amount of code.
- Share and reuse code without having to reimplement it.
- Easily substitute improved implementations.
- Develop appropriate abstract models for addressing programming problems.
- Localize debugging.

## Unit Testing

A best practice in Java programming is to include a `main()` in every library of static methods that tests the methods in the library. Proper unit testing can be a significant programming challenge in itself. At a minimum, every module should contain a `main()` method that exercises the code in the module and provides some assurance that it works.

## APIs

A critical component of modular programming is documentation that explains the operation of library methods that are intended for use by others.

## Your Own Libraries

It is worthwhile to consider every program that you write as a library implementation for possible reuse in the future. Write code for the client, a top-level implementation that breaks the computation up into manageable parts. Articulate an API for a library of static methods that can address each part. Develop an implementation of the API with `main()` that tests the methods independently of the client.

**THE PURPOSE OF AN API** is to separate the client from the implementation: the client should know nothing about the implementation and should not take properties of any particular client into account.

## Strings

### Concatenation

The result of concatenating two String values is a single String value, the first string followed by the second.

### Conversion

Two primary uses of strings are to convert values that we can enter on a keyboard into data-type values and to convert data-type values to values that we can read on display.

### Automatic Conversion

If one of the arguments of `+` is a String, Java automatically converts the other arguments to a String.

### Command-line arguments

One important use of strings in Java is to enable a mechanism for passing information from the command line to the program.

## Input and Output

### Commands and Arguments

Java classes have a `main()` static method that takes a String array `args[]` as its argument. That array is a sequence of command-line arguments that we type, provided to Java by the operating system.

- `javac` -> `.java` file name -> compile Java program.
- `java` `.class` file name (no extension) and command line arguments -> run Java program.

### Standard Output

By default, the system connects standard output to the terminal window.

### Formatted Output

In its simplest form, `printf()` takes two arguments. The first argument is a format string that describes how the second argument is to be converted to a string for output. The simplest type of a format string begins with `%` and ends with a one-letter conversion code.

### Standard Input

By default, the system connects standard input to the terminal window—what you type is the input stream. One of the key features of the standard input stream is that your program consumes values when it reads them.

### Redirecting and Piping

Standard input and output enable us to take advantage of command-line extensions supported by many operating systems. By adding a simple directive to the command that invokes a program, we can redirect its standard output to a file, either for permanent storage or for input to another program at a later time.

```bash
% java RandomSeq 1000 100.0 200.0 > data.txt
% java Average < data.txt
```

## Binary Search

```java
public static int indexOf(int[] a, int index) {
    int low = 0;
    int high = a.length - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (key < a[mid]) high = mid - 1;
        else if (key > a[mid]) low = mid + 1;
        else return mid;
    }

    return -1;
}
```

### Performance

A working program is often not sufficient. Solving the whitelist problem for a large number of inputs is not feasible without efficient algorithms such as binary search and mergesort. Good performance is often of critical importance.

### Perspective

Data abstraction, sometimes known as object-oriented programming. Simply put, the idea behind data abstraction is to allow a program to define data types, not just static methods that operate on predefined data types. It enables us to expand our ability to reuse code through modular programming. It provides a convenient mechanism for building so-called linked data structures that provide more flexibility than arrays and are the basis of efficient algorithms in many settings. It enables us to precisely define the algorithmic challenges that we face.

# 1.2 DATA ABSTRACTION

A **data type** is a set of values and a set of operations on those values.

An abstract data type (ADT) is a data type whose representation is hidden from the client. Implementing an ADT as a Java class is not very different from implementing a function library as a set of static methods. The primary difference is that we associate data with the function implementations and we hide the representation of the data from the client.

## Using Abstract Data Types

You don't need to know how a data type is implemented to be able to use it.

### Inherited Methods

Various Java conventions enable a data type to take advantage of built-in language mechanisms by including specific methods in the APIs:

- `toString()`
- `equals()`
- `hashCode()`
- `compareTo()`

### Client Code

You can use an ADT in any program provided that the source code is in a .java file in the same directory, or in the standard Java library, or accessible through an import statement.

### Objects

An object is an entity that can take on a data-type value. Objects are characterized by three essential properties: state, identity, and behavior.

- The **state** of an object is a value from its data type.
- The **identity** of an object distinguishes one object from another.
- The **behavior** of an object is the effect of data-type operations.

An object's state might be used to provide information to a client or cause a side effect or be changed by one of its data types operations, but the details of the representation of the data-type value are not relevant to client code.

#### Creating Objects

Each data-type value is stored in an object. Each time that a client uses `new()`, the system:

- Allocates memory space for the object
- Invokes the constructor to initialize its value
- Returns a reference to the object

#### Invoking Instance Methods

Instance methods have an additional property that characterizes them: each invocation is associated with an object. The primary purpose of static methods is to implement functions; the primary purpose of non-static methods is to implement data-type operations.

#### Using Objects

To develop client code for a given data type, we:

- Declare variables of the type for use in referring to objects
- Use the keyword `new` to invoke a constructor that creates objects of the type
- Use the object name to invoke instance methods, either as statements or within expressions

#### Assignment Statements

Assignment statements do not create a new object, just another reference to an existing object, known as aliasing. Both variables refer to the same object. Changing the state of an object impacts all code involving aliased variables referencing that object. This is different from primitive types.

#### Objects As Arguments

Java passes a copy of the argument value from the calling program to the method. This arrangement is known as "pass by value." For reference types, this means passing the reference by value or, equivalently, passing the object by reference.

#### Objects As Return Values

This capability is important because Java methods allow only one return value—using objects enables us to write code that, in effect, returns multiple values.

#### Arrays Are Objects

In Java, every nonprimitive type is an object. Arrays are objects as well. When we create an array of objects, we do so in two steps: create the array and create each object in the array.

### A data type is a set of values and a set of operations defined on those values.
### An object is an entity that can take on a data-type value or an instance of a data type.
### Objects are characterized by three essential properties: state, identity, and behavior.

## Information Processing

A great many applications are centered around processing and organizing information. Whenever you have data of different types that logically belong together, it is worthwhile to contemplate defining an ADT. The ability to do so helps to organize the data, can greatly simplify client code in typical applications, and is an important step on the road to data abstraction.

## Strings

A String is an indexed sequence of char values. String values are similar to arrays of characters, but the two are not the same. Arrays have built-in Java language syntax for accessing a character; String has instance methods for indexed access, length, and many other operations.

Why not just use arrays of characters instead of String values? To simplify and clarify client code.

## Input and Output Revisited

A disadvantage of the StdIn, StdOut standard libraries is that they restrict us to working with just one input file, one output file for any given program.

## Implementing Abstract Data Types

A data-type definition may have multiple constructors and may also include definitions of static methods.

### Instance Variables

There is a critical distinction between instance variables and local variables within a static method or a block: there is just one value corresponding to each local variable at a given time, but there are numerous values corresponding to each instance variable. Ambiguity with this arrangement, because each time that we access an instance variable, we do so with the object name—that object is the one whose value we are accessing.

### Constructors

Generally, the purpose of a constructor is to initialize the instance variables. Every constructor creates an object and provides to the client a reference to that object. Java automatically invokes a constructor when a client program uses the keyword `new`.

### Instance Methods

But there is one critical distinction for instance methods: they can access and perform operations on instance variables. A reference to a variable in an instance method refers to the value for the object that was used to invoke the method.

### Scope

In summary, the Java code that we write to implement instance methods uses three kinds of variables:

- Parameter variables
- Local variables
- Instance variables

### Maintaining Multiple Implementations

Multiple implementations of the same API can present maintenance and nomenclature issues. In some cases, we simply want to replace an old implementation with an improved one. In others, we may need to maintain two implementations, one suitable for some clients, the other suitable for others.

# Designing Abstract Data Types

An abstract data type is a data type whose representation is hidden from the client.

## Encapsulation

- Independently develop client and implementation code
- Substitute improved implementations without affecting clients
- Support programs not yet written
- Limiting the potential for error
- Adding consistency checks and other debugging tools in implementations
- Clarifying client code

The key to success in modular programming is to maintain independence among modules.

## Designing APIs

There are numerous pitfalls that every API design is susceptible to:

- An API may be too hard to implement, implying implementations that are difficult or impossible to develop.
- An API may be too hard to use, leading to client code that is more complicated than it would be without the APIs
- An API may be too narrow, omitting methods that clients need.
- An API may be too wide, including a large number of methods not needed by any client. Most Common and Most Difficult To Avoid
- An API may be too general, providing no useful abstractions.
- An API may be too specific, providing abstractions so detailed or so diffuse as to be useless.
- An API may be too dependent on a particular representation, therefore not serving the purpose of freeing client code from the details of using that representation

## Interface Inheritance

The first inheritance mechanism is subtyping, which allows us to specify a relationship between otherwise unrelated classes by specifying in an interface a set of common methods that each implementing class must contain. An interface is nothing more than a list of instance methods.

```java
public interface Datable {
    int month();
    int day();
    int year();
}

public class Date implements Datable {
    // implementation code
}
```

The Java compiler will check that it matches the interface. Adding the code `implements Datable` to any class that implements `month()`, `day()`, `year()` provides a guarantee to any client that an object of that class can invoke those methods. This arrangement is known as "interface inheritance"—an implementing class inherits the interface.

## Implementation Inheritance

Java also supports another inheritance mechanism known as subclassing, which is a powerful technique that enables a programmer to change behavior and add functionality without rewriting an entire class from scratch. The subclass contains more methods than the superclass. Moreover, the subclass can redefine or override methods in the superclass.

## String Conversion

By convention, every Java type inherits `toString()` from Object so any client can invoke `toString()` for any object. If an object's data type does not include an implementation of `toString()`, then the default implementation in Object is invoked, which is normally not helpful, since it typically returns a string representation of the memory address of the object.

## Wrapper Types

These classes consist primarily of static methods such as `parseInt()`, but they also include the inherited instance methods `toString()`, `compareTo()`, `equals()`, and `hashCode()`.

## Equals

Equality for objects is often determined by the `equals()` method. It should follow certain properties:

- **Reflexive**: `x.equals(x)` is true.
- **Symmetric**: `x.equals(y)` is true if and only if `y.equals(x)` is true.
- **Transitive**: if `x.equals(y)` and `y.equals(z)` are true, then `x.equals(z)` is true.
- **Consistent**: multiple invocations of `x.equals(y)` consistently return the same value, provided neither object is modified.
- **Not Null**: `x.equals(null)` returns false.

```java
public boolean equals(Object x) {
    if (this == x) return true;
    if (x == null) return false;
    if (this.getClass() != x.getClass()) return false;
    Date that = (Date) x;
    if (this.day != that.day) return false;
    if (this.month != that.month) return false;
    if (this.year != that.year) return false;
    return true;
}
```

## Memory Management

The ability to assign a new value to a reference variable creates the possibility that a program may have created an object that can no longer be referenced. Such an object is said to be orphaned. Objects are also orphaned when they go out of scope.

Memory management turns out to be easier for primitive types because all the information needed for memory allocation is known at compile time. Java takes care of reserving space for variables when they are declared and freeing that space when they go out of scope.

## Immutability

An immutable data type has the property that the value of an object never changes once constructed. Generally, immutable types are easier to use and harder to misuse than mutable types because the scope of code that can change their values is far smaller. It is easier to debug code that uses immutable types because it is easier to guarantee that variables in client code that uses them remain in a consistent state. When using mutable types, you must always be concerned about where and when their values change. The downside of immutability is that a new object must be created for every value. Another downside of immutability stems from the fact that `final` guarantees immutability only when instance variables are primitive types, not reference types.

## Design By Contract

Exceptions and errors generally handle unforeseen errors outside of our control. Assertions verify assumptions that we make within code we develop. Liberal use of both exceptions and assertions is good programming practice.

### Exception And Errors

Exception and errors are disruptive events that occur while a program is running, often to signal an error. The action taken is known as throwing an exception or throwing an error.

```java
throw new RunTimeException("Error Message Here");
```

A general practice known as fail-fast programming suggests that an error is more easily pinpointed if an exception is thrown as soon as an error is discovered.

### Assertions

An assertion is a boolean expression that you are affirming is true at that point in the program. If the expression is false, the program will terminate and report an error message.

# 1.3 BAGS, QUEUES, AND STACKS

## Collections and APIs

Collections of objects and their operations often revolve around adding, removing, or examining objects. These structures differ in specifying which object is to be removed or examined next.

### APIs

#### Bag

```java
public class Bag<Item> implements Iterable<Item> {
    Bag();                    // create an empty bag
    void add(Item item);       // add an item
    boolean isEmpty();         // check if the bag is empty
    int size();                // number of items in the bag
}
```

#### FIFO Queue

```java
public class Queue<Item> implements Iterable<Item> {
    Queue();                  // create an empty queue
    void enqueue(Item item);   // add an item
    Item dequeue();            // remove the least recently added item
    boolean isEmpty();         // check if the queue is empty
    int size();                // number of items in the queue
}
```

#### Pushdown (LIFO) Queue (Stack)

```java
public class Stack<Item> implements Iterable<Item> {
    Stack();                  // create an empty stack
    void push(Item item);      // add an item
    Item pop();                // remove the most recently added item
    boolean isEmpty();         // check if the stack is empty
    int size();                // number of items in the stack
}
```

## Generics

The use of generics allows for flexible data structures that can be used with any type of data.

```java
Stack<String> stack = new Stack<String>();
stack.push("Test");
String next = stack.pop();

Queue<Date> queue = new Queue<Date>();
queue.enqueue(new Date(12, 31, 1999));
Date next = queue.dequeue();
```

Without generics, we would need different APIs for each type of data.

## Autoboxing and Unboxing

Type parameters need to be instantiated as reference types, and Java automatically converts between reference types and corresponding primitive types in assignments and expressions.

```java
Stack<Integer> stack = new Stack<Integer>();
stack.push(17); // autoboxing (int -> Integer)
int i = stack.pop(); // unboxing (Integer -> int)
```

## Iterable Collections

```java
Queue<Transaction> collection = new Queue<Transaction>();

for (Transaction transaction : collection) {
    StdOut.println(transaction);
}
```

## Bags

A bag is a collection where removing items is not supported, and its purpose is to provide clients with the ability to collect items and then iterate through them.

Example of using a Bag:

```java
Bag<Double> numbers = new Bag<>();
while (!StdIn.isEmpty())
    numbers.add(StdIn.readDouble());

int n = numbers.size();
double sum = 0.0;
for (double x : numbers)
    sum += x;

double mean = sum / n;

double sum = 0.0;
for (double x : numbers)
    sum += (x - mean) * (x - mean);

double stdDev = Math.sqrt(sum / (n - 1));

StdOut.println(mean);
StdOut.println(stdDev);
```

## FIFO Queues

A FIFO queue follows the first-in-first-out policy and is often used to represent tasks waiting to be serviced in the order they arrive.

Example using a queue for reading all integers from a file:

```java
public static int[] readAllInts(String name) {
    In in = new In(name);
    Queue<Integer> queue = new Queue<Integer>();
    while (!in.isEmpty())
        queue.enqueue(in.readInt());

    int n = queue.size();
    int[] a = new int[n];

    for (int i = 0; i < n; i++)
        a[i] = queue.dequeue();

    return a;
}
```

## Pushdown Stacks

A pushdown stack is a collection based on the last-in-first-out policy. Example of reading integers and printing them in reverse order:

```java
Stack<Integer> stack = new Stack<>();
while (!StdIn.isEmpty())
    stack.push(StdIn.readInt());

for (int i : stack)
    StdOut.println(i);
```

## Arithmetic Expression Evaluation

An example of using two stacks to evaluate arithmetic expressions.

```java
Stack<String> ops = new Stack<String>();
Stack<Double> vals = new Stack<Double>();

while (!StdIn.isEmpty()) {
    String s = StdIn.readString();
    if (s.equals("(")) ;
    else if (s.equals("+")) ops.push(s);
    else if (s.equals("-")) ops.push(s);
    else if (s.equals("*")) ops.push(s);
    else if (s.equals("/")) ops.push(s);
    else if (s.equals("sqrt")) ops.push(s);
    else if (s.equals(")")) {
        String op = ops.pop();
        double v = vals.pop();
        if (op.equals("+")) v = vals.pop() + v;
        else if (op.equals("-")) v = vals.pop() - v;
        else if (op.equals("*")) v = vals.pop() * v;
        else if (op.equals("/")) v = vals.pop() / v;
        else if (op.equals("sqrt")) v = Math.sqrt(v);
        vals.push(v);
    } else {
        vals.push(Double.parseDouble(s));
    }
}
```

## Implementing Collections

### Fixed Capacity Stack

API:

```java
public class FixedCapacityStack<Item> {
    FixedCapacityStack(int cap); // create an empty stack of capacity cap
    void push(Item item); // add an item
    Item pop(); // remove the most recently added item
    boolean isEmpty(); // check if the stack is empty
    int size(); // number of items on the stack
}
```

Implementation:

```java
public class FixedCapacityStack<Item> {
    private Item[] a; // Stack entries
    private int n; // size

    public FixedCapacityStack(int capacity) {
        a = (Item[]) new Object[capacity];
    }

    public boolean isEmpty() { return n == 0; }
    public int size() { return n; }

    public void push(Item item) {
        a[n++] = item;
    }

    public Item pop() {
        Item item = a[--n];
        a[n] = null; // Avoid loitering
        if (n > 0 && n == a.length / 4)
            resize(a.length / 2);
        return item;
    }

    private void resize(int max) {
        // Move stack of size n <= max to a new array of size max.
        Item[] temp = (Item[]) new Object[max];
        for (int i = 0; i < n; i++)
            temp[i] = a[i];
        a = temp;
    }
}
```

### Linked List

A linked list is a recursive data structure where each node holds an item and a reference to the next node.

#### Node Record

```java
private class Node {
    Item item;
    Node next;
}
```

#### Building a Linked List

```java
Node first = new Node();
Node second = new Node();
Node third = new Node();

first.item = "to";
second.item = "be";
third.item = "or";

first.next = second;
second.next = third;
```

#### Insert At The Beginning

```java
Node oldfirst = first;
first = new Node();
first.item = "not";
first.next = oldfirst;
```

#### Remove From The Beginning

```java
first = first.next;
```

#### Insert At The End

```java
Node oldLast = last;
last = new Node();
last.item = "not";
oldLast.next = last;
```

#### Insert/Remove At Other Positions

To insert or remove at other positions, a doubly-linked list with links in both directions may be used.

#### Traversal

```java
for (Node x = first; x != null; x = x.next) {
    // Process x.item
}
```

### Stack Implementation

Using linked lists for a stack:

```java
public class Stack<Item> {
    private Node first; // top of the stack (most recently added node)
    private int n; // number of items

    private class Node {
        // Nested class
        Item item;
        Node next;
    }

    public boolean isEmpty() { first == null; }
    public int size() { return n; }

    public void push(Item item) {
        // Add item to the top of the stack
        Node oldfirst = first;
        first = new Node();
        first.item = item;
        first.next = oldfirst;
        n++;
    }

    public Item pop() {
        // Remove item from the top of the stack
        Item item = first.item;
        first = first.next;
        n--;
        return item;
    }
}
```

### Queue Implementation

Using linked lists for a queue:

```java
public class Queue<Item> {
    private Node first; // link to the least recently added node
    private Node last; // link to the most recently added node
    private int n; // number of items

    private class Node {
        // Nested class
        Item item;
        Node next;
    }

    public boolean isEmpty() { first == null; }
    public int size() { return n; }

    public void enqueue(Item item) {
        // Add item to the end of the list
        Node oldlast = last;
        last = new Node();
        last.item = item;
        last.next = null;
        if (isEmpty()) first = last;
        else oldlast.next = last;
        n++;
    }

    public Item dequeue() {
        // Remove item from the beginning of the list
        Item item = first.item;
        first = first.next;
        n--;
        if (isEmpty()) last = null;
        return item;
    }
}
```

### Bag Implementation

```java
public class Bag<Item> implements Iterable<Item> {
    private Node first; // First node in the list

    private class Node {
        // Nested class
        Item item;
        Node next;
    }

    public void addItem(Item item) {
        Node oldfirst = first;
        first = new Node();
        first.item = item;
        first.next = oldfirst;
        n++;
    }

    public Iterator<Item> iterator() {
        return new ListIterator();
    }

    private class ListIterator implements Iterator<Item> {
        private Node current = first;

        public boolean hasNext() {
            return current != null;
        }

        public void remove() { }

        public Item next() {
            Item item = current.item;
            current = current.next;
            return item;
        }
    }
}
```

## Overview

### Data Structures

- Arrays are built into Java; linked lists are easy to build with standard Java records.
- Two fundamental alternatives: sequential allocation (array) and linked allocation (linked list).

#### Array

- Provides immediate access to any item.
- Needs to know size on initialization.

#### Linked List

- Uses space proportional to size.
- Requires a reference to access an item.

# 1.4 ANALYSIS OF ALGORITHMS

- How long will my program take?
- Why does my program run out of memory?

## Scientific Method

1. Observe some feature of the natural world, generally with precise measurements.
2. Hypothesize a model that is consistent with the observations.
3. Predict events using the hypothesis.
4. Verify the predictions by making further observations.
5. Validate by repeating until the hypothesis and observations agree.

## Observations

- Determine how to make quantitative measurements of the running time of our programs.
- Every time you run a program, you perform a scientific experiment answering: How long will my program take?
- Focus on better quantifying the relationship between problem size and running time.

Example program:

```java
public static int count(int[] a) {
    int n = a.length;
    int count = 0;
    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)
            for (int k = j + 1; k < n; k++)
                if (a[i] + a[j] + a[k] == 0)
                    count++;

    return count;
}
```

## Stopwatch

- Reliably measuring the exact running time of a program can be difficult.
- Stopwatch data type provides estimates.
- Distinguish between programs finishing in seconds or minutes versus days or months.

```java
public class Stopwatch {
    private final long start;

    public Stopwatch() {
        start = System.currentTimeMillis();
    }

    public double elapsedTime() {
        long now = System.currentTimeMillis();
        return (now - start) / 100.0;
    }
}

public static void main(String[] args) {
    int n = 10_000;
    int[] a = new int[n];
    // For each, pollute data to array.

    Stopwatch timer = new Stopwatch();
    int count = Threesum.count(a);
    double time = timer.elapsedTime();
    StdOut.println(count + " triples " + time + " seconds ");
}
```

## Analysis Of Experimental Data

- How long will my program take as a function of the input size?

## Mathematical Models

- Running time determined by the cost and frequency of executing each statement.
- Challenge is determining the frequency of execution of the statements.

## Tilde Approximations

- Simplify formulas using tilde notation.
- Order of growth:
    - Constant: 1
    - Logarithmic: logn
    - Linear: n
    - Linearithmic: nlogn
    - Quadratic: n^2
    - Cubic: n^3
    - Exponential: 2^n

## Analysis Of Algorithms

- Order of growth determines running time, independent of implementation details.

## Summary

- Mathematical models reduce steps in analyzing running time.
- Order of growth classification.

## Doubling Ratio Experiments

- Predicting performance and estimating order of growth.
- Simple way to estimate the running time order of growth.

## Estimating The Feasibility Of Solving Large Problems

- Understanding limitations on problem size based on order of growth.

## Estimating The Value Of Using a Faster Computer

- Impact of a faster computer on solving problems.

## Caveats

- Large constants, nondominant inner loop, instruction time, system considerations, too close to call, strong dependence on input.

## Coping With Dependence On Inputs

- Input models, worst-case performance guarantees.

## Memory

- Analyzing memory usage is simpler than analyzing running time.
- Count variables and weigh them by the number of bytes.

## Objects

- Memory usage of objects, linked lists, arrays, and strings.

## Perspective

- Priority is clear and correct code.
- Consider performance but do not ignore it.
- Faster algorithms may be more complicated.

# 2. SORTING

## 2.1 Elementary Sort

### Rules Of The Game

- Primary concern is algorithms for rearranging arrays of items with keys.
    
- Goal: Rearrange the array so that each entry's key is no smaller than the key in each entry with a lower index and no larger than the key in each entry with a larger index.
    
- Sort code uses two operations: `less()` (compares items) and `exchange()` (exchanges items).

```java
// Template for Sort Class

public class Example {
    public static void sort(Comparable[] a) {
    }

    private static boolean less(Comparable v, Comparable w) {
        return v.compareTo(w) < 0;
    }

    private static void exchange(Comparable[] a, int i, int j) {
        Comparable t = a[i]; a[i] = a[j]; a[j] = t;
    }

    private static void show(Comparable[] a) {
        // Display array elements
    }

    public static boolean isSorted(Comparable[] a) {
        // Check if array is sorted
    }
}
```

### Certification

- Ensure the sort implementation always puts the array in order.
- Include the statement `assert isSorted(a)` as a conservative practice.

### Running Time

- Test algorithm performance by proving facts about the number of basic operations.
- Sorting Cost Model: Count compares and exchanges.
- If no exchanges, count array accesses.

### Extra Memory

- Sorting algorithms categorized into two:
    - Sort in place, use constant extra memory.
    - Use linear extra memory.

### Types Of Data

- Sort code effective for any item type implementing the Comparable interface.

## SELECTION SORT

- Simple sorting algorithm:
    - Find the smallest item and exchange it with the first entry.
    - Find the next smallest item and exchange it with the second entry.
    - Continue until the entire array is sorted.
- Running time insensitive to input.
- Minimal data movement.

```java
// SELECTION SORT
public static void sort(Comparable[] a) {
    int n = a.length;
    for (int i = 0; i < n; i++) {
        int min = i;
        for (int j = i + 1; j < n; j++)
            if (less(a[j], a[min])) min = j;
        exchange(a, i, min);
    }
}
```

## INSERTION SORT

- Insert current item by moving larger items to the right.
- Items to the left are in sorted order during the sort.
- Running time depends on initial order of items.
- Efficient for partially sorted arrays.

```java
// INSERTION SORT
public static void sort(Comparable[] a) {
    int n = a.length;
    for (int i = 0; i < n; i++) {
        for (int j = i; j > 0 && less(a[j], a[j - 1]); j--)
            exchange(a, j, j - 1);
    }
}
```

- Examples of partially sorted arrays:
    - Each entry not far from its final position.
    - Small array appended to a large sorted array.
    - Array with only a few entries not in place.
- Insertion sort is efficient for such arrays.

### IN SUMMARY

- Insertion sort is excellent for partially sorted arrays and tiny arrays.

## Comparing Two Sorting Algorithms

- Compare algorithms by:
    
    - Implementing and debugging them.
    - Analyzing their basic properties.
    - Formulating a hypothesis about comparative performance.
    - Running experiments to validate the hypothesis.
- Understanding elementary algorithms is worthwhile for:
    
    - Establishing ground rules.
    - Providing performance benchmarks.
    - Use in specialized situations.
    - Basis for developing better algorithms.

## SHELLSORT

- Extension of insertion sort, gains speed by allowing exchanges of far-apart array entries.
- Rearrange the array to create h-sorted subsequences.
- h-sort for large values of h, easier to h-sort for smaller values of h.

```java
// SHELLSORT
public static void sort(Comparable[] a) {
    int n = a.length;
    int h = 1;
    while (h < n / 3) h = 3 * h + 1; // 1,4,13,40,121
    while (h >= 1) {
        for (int i = h; i < n; i++) {
            for (int j = i; j >= h && less(a[j], a[j - h]); j -= h)
                exchange(a, j, j - h);
        }
        h = h / 3;
    }
}
```

- Shellsort trades off size and partial order in subsequences.
- Useful for large arrays, performs well on arbitrary order arrays.
- Faster than insertion sort and selection sort, speed advantage increases with array size.

# 2.2 MERGESORT

Mergesort is a sorting algorithm that involves merging two ordered arrays to create one larger ordered array. One of its most attractive properties is that it guarantees sorting any array of n items in time proportional to n log n, with a prime disadvantage of using extra space proportional to n.

### Abstract In-Place Merge

Mergesort involves a considerable number of merges, making the creation of a new array for output during each merge inefficient. An abstract in-place merge strategy can be implemented to optimize this process:

```java
private static void merge(Comparable[] a, int lo, int mid, int hi) {
    int i = lo, j = mid + 1;
    for (int k = lo; k <= hi; k++)
        aux[k] = a[k];

    for (int k = lo; k <= hi; k++)
        if (i > mid) a[k] = aux[j++];
        else if (j > hi) a[k] = aux[i++];
        else if (less(aux[j], aux[i])) a[k] = aux[j++];
        else a[k] = aux[i++];
}
```

This merging process involves copying into an auxiliary array (`aux[]`) and then merging back to the original array (`a[]`).

### Top-Down Mergesort

Top-Down Mergesort is a recursive implementation that exemplifies the "divide-and-conquer" paradigm for efficient algorithm design. The recursive code serves as the basis for analyzing Mergesort's running time.

```java
public class Merge {
    private static Comparable[] aux; // auxiliary array for merges

    public static void sort(Comparable[] a) {
        aux = new Comparable[a.length]; // Allocate space just once
        sort(a, 0, a.length - 1);
    }

    private static void sort(Comparable[] a, int lo, int hi) {
        if (hi <= lo) return;
        int mid = lo + (hi - lo) / 2;
        sort(a, lo, mid); // Sort left half
        sort(a, mid + 1, hi); // Sort right half.
        merge(a, lo, mid, hi); // Merge results
    }
}
```

In this implementation, an auxiliary array is used to assist in the sorting process. For small subarrays, the insertion sort method is used to optimize the algorithm's efficiency.

### Bottom-Up Mergesort

Bottom-Up Mergesort is an alternative implementation that organizes the merges to avoid the creation of auxiliary arrays. It performs pairwise merges in multiple passes until the entire array is sorted.

```java
public class MergeBU {
    private static Comparable[] aux;

    public static void sort(Comparable[] a) {
        int n = a.length;
        aux = new Comparable[n];
        for (int len = 1; len < n; len *= 2)
            for (int lo = 0; lo < n - len; lo += len + len)
                merge(a, lo, lo + len - 1, Math.min(lo + len + len - 1, n - 1));
    }
}
```

### The Complexity Of Sorting

Understanding mergesort is crucial for proving fundamental results in computational complexity. While mergesort may not be optimal in terms of space usage, the worst case may not be likely in practice. Other operations besides compares may also be essential, and certain data can be sorted without using any compares.

# 2.3 QUICKSORT

Quicksort is a popular sorting algorithm known for its ease of implementation and efficiency. It is an in-place sorting algorithm that, on average, requires time proportional to n log n to sort an array of length n. The algorithm works by partitioning the array into two subarrays and then sorting the subarrays independently.

### The Basic Algorithms

```java
public class Quick {
    public static void sort(Comparable[] a) {
        StdRandom.shuffle(a);
        sort(a, 0, a.length - 1);
    }

    private static void sort(Comparable[] a, int lo, int hi) {
        if (hi <= lo) return;
        int j = partition(a, lo, hi);
        sort(a, lo, j - 1);    // Sort left part a[lo..j-1].
        sort(a, j + 1, hi);    // Sort right part a[j+1..hi].
    }
}
```

Quicksort is a recursive program that sorts a subarray `a[lo..hi]` by using a `partition()` method. This method puts `a[j]` into position and arranges the rest of the entries so that the recursive calls finish the sort.

The `partition()` method rearranges the array to satisfy three conditions:

1. The entry `a[j]` is in its final place in the array, for some `j`.
2. No entry in `a[lo]` through `a[j-1]` is greater than `a[j]`.
3. No entry in `a[j+1]` through `a[hi]` is less than `a[j]`.

```java
private static int partition(Comparable[] a, int lo, int hi) {
    int i = lo, j = hi + 1; // left and right scan indices
    Comparable v = a[lo];   // partitioning item

    while (true) {
        while (less(a[++i], v)) if (i == hi) break;
        while (less(v, a[--j])) if (j == lo) break;
        if (i >= j) break;
        exch(a, i, j);
    }

    exch(a, lo, j); // Put partitioning item v into a[j].
    return j;       // with a[lo..j-1] <= a[j+1..hi].
}
```

This code partitions on the item `v` in `a[lo]`. The main loop exits when the scan indices `i` and `j` cross. The partitioning process efficiently rearranges the array based on the value of the partitioning item.

### Algorithmic Improvements

#### Cutoff To Insertion Sort

To improve the performance of quicksort, especially for tiny subarrays, insertion sort is used for such cases. Being recursive, quicksort's `sort()` may call itself for tiny subarrays.

#### Median Of Three Partitioning

Another improvement involves using the median of a small sample of items taken from the subarray as the partitioning item. This yields a slightly better partition but comes at the cost of computing the median.

#### Entropy-Optimal Sorting

An idea is to partition the array into three parts—one each for items with keys smaller than, equal to, and larger than the partitioning item's key. This approach handles subarrays consisting solely of items that are equal more efficiently.

```java
public class Quick3way {
    private static void sort(Comparable[] a, int lo, int hi) {
        if (hi <= lo) return;
        int lt = lo, i = lo + 1, gt = hi;
        Comparable v = a[lo];
        while (i <= gt) {
            int cmp = a[i].compareTo(v);
            if (cmp < 0) exch(a, lt++, i++);
            else if (cmp > 0) exch(a, i, gt--);
            else i++;
        }
        sort(a, lo, lt - 1);
        sort(a, gt + 1, hi);
    }
}
```

This implementation efficiently handles three partitions: items less than, equal to, and greater than the partitioning item.

# 2.4 PRIORTY QUEUES

Often, we collect a set of items, then process the one with the largest key, then perhaps collect more items, then process the one with the current largest key, and so forth.

This effect typically achieved by assigning a priority to events associated with applications, then always choosing to process next the highest-priority event
Most cellphones are likely to process an incoming call with higher priority than a game application

An appropriate data type such an environment supports two operations: `remove the maximum` and `insert `.  Such a data type is called a `priority queue`
Using priority queues is similar to using queues (remove the oldest) and stacks (remove the newest)

We can use any priority queue as the basis for a sorting algorithm by inserting a sequence of items, then successively removing the smallest to get them out, in order.
An important sorting algorithm known as ``heapsort`` also follows naturally from our heap based priority-queue implementations.

## API 

The priority queue is a prototypical abstract data type: it represents a set of values and operations on those values , and it provides a convenient abstraction that allows us to separate application programs (client) from various implementations

Priority queues are characterized by the  `remove the maximum` and `insert` operations

```java
public class MaxPQ <Key extends Comparable<Key>>
{
	MaxPQ() // Create a Priority Queue
	MaxPQ(int max) // Create a Priority Queue Of Initial Capacity Max
	MaxPQ(Key[] a) // Create a Priority Queue from the keys in a[]
	
	void insert(Key v) // insert a key into priority queue 
	Key max() // return the largest key
	Key delMax() // return and remove the largest key
	boolean isEmpty() // is the priority queue empty ?
	int size() // number of keys in the priority queue
}
```


### A priority-queue client

A huge input stream of n strings and associated integer values, and your task is to find the largest or smallest m integers in the input stream


## Elementary Implementations

Use an array or a linked list, kept in order or unordered.
These implementations are useful for small priority queues, situations where one of the two operations are predominant, or situations where some assumptions can be made about the order of the keys involved in the operations

### Array Representation (unordered)

The code for insert in the priority queue is the same as for push in the stack.
To implement remove the maximum, with the item at the end and then delete that one, as we did with pop() for stacks

A priority-queue client

```java
public class TopM
{
	public class void main(String[] args)
	{ // Print the top m lines in the input stream
		int m = Integer.parseInt(args[0]);
		MinPQ<Transaction> pq = new MinPQ<Transaction>(m+1);
		while (StdIn.hasNextLine())
		{ // Create an entry from the next line and put on the PQ
			pq.insert(new Transaction(StdIn.readLine()))
			if(pq.size() > m)
				pq.delMin(); // Remove the minimum if m+1 entries on the PQ
		} //Top m entries are on the PQ

		Stack<Transaction> stack = new Stack<Transaction>();
		while(!pq.isEmpty())
			stack.push(pq.delMin());
		for (Transaction transaction : stack)
			StdOut.println(transaction)
	}
}
```


### Array Representation (ordered)

Another approach is to add code for insert to move larger entries one position to the right, thus keeping the keys in the array in order. Thus, the largest entry is always at the end, and the code for remove the maximum in the priority queue is the same as for pop in the stack.

### Linked-list representations.

Similarly, start with our linked-list code for pushdown stacks, modifying either the code for pop() to find and return the maximum or the code for push() to keep keys in reverse order and the code for pop() to unlink and return the first (maximum) item on the list

Using unordered sequences is the prototypical lazy approach to this problem, using ordered sequences is the prototypical eager approach to the problem, where we do as much work as we can up front

## Heap Definitions

The binary heap is a data structure that can efficiently support the basic priority-queue operations. 
In a binary heap, the keys are stored in an array such that each key is guaranteed to be larger (or equal to) the keys at two other additional keys, and so forth.

> **Definition**. A binary tree is heap-ordered if the key in each node is larger than or equal to the keys in that node's two children (if any)

Equivalently, the key in each node of a heap-ordered binary tree is smaller than or equal to the key in that node's parent (if any). Moving up from any node, get a nondecreasing sequence of keys; moving down from any node, got a nonincreasing sequence of keys.

## Algorithms On Heaps

```java
private boolean less(int i, int j)
{
	return pq[i].compareTo(pq[j]) < 0;
}

private void exch(int i, int j)
{
	Key t = pq[i]; 
	pq[i] = pq[j]; 
	pq[j] = t;
}
```

### Bottom-up rehapify (swim)

If the heap order is violated because a node's key becomes larger than that node's parent key, then we can make progress toward fixing the violation by exchanging the node with its parent.
After the exchange, the node is larger both its children but the node may still be larger than its parent.

We can fix that violation in the same way, and so forth, moving up the heap until we reach a node with a larger key, or  the root

```java
private void swim(int k)
{
	while (k > 1 && less(k/2, k))
	{
		exch(k/2,k);
		k = k/2
	}
}
```

### Top-down reheapify (sink)

```java
private void sink(int k)
{
	while (2*k <=n)
	{
		int j = 2*k;
		if (j < n && less(j, j+1)) 
			j++;
		if(!less(k,j))
			break;

		exch(k,j)
		k = j;
	}
}
```

If the heap order is violated because a node's key becomes smaller than one or both of that node's children's keys, then we can make progress towards fixing the violation by exchanging the node with the larger of its two children 

This switch may cause a violation at the child; we fix that violation in the same way, and so forth, moving down the heap until we reach a node with both children smaller (or equal), or the bottom.

*IF WE IMAGINE* the heap to represent a cutthroat corporate hierarchy, with each of the children of a node representing subordinates then these operations have amusing interpretations.
The swim() operation corresponds to a promising new manager arriving on the scene, being promoted up the chain of command until the new person encounters a higher-qualified boss.
The sink() operation is analogous to situation when the president of the company resigns and is replaced by someone from the outside. If the president's most powerful subordinate is stronger then the new person, they exchange jobs and we move down the chain of command, demoting the new person and promoting the others until the level of competence of the new person is reached, where there is no higher-qualified subordinate

>Insert. We add the new key at the end of the array, increment the size of the heap,
  and then swim up through the heap with that key to restore the heap condition.

>Remove the maximum. We take the largest key off the top, put the item from
  the end of the heap at the top, decrement the size of the heap, and then sink down
  through the heap with that key to restore the heap condition.

```java
public class MaxPQ<Key extends Comparable<Key>>
{
private Key[] pq; // heap-ordered complete binary tree
private int N = 0; // in pq[1..N] with pq[0] unused
public MaxPQ(int maxN)
{ pq = (Key[]) new Comparable[maxN+1]; }
public boolean isEmpty()
{ return N == 0; }
public int size()
{ return N; }
public void insert(Key v)
{
pq[++N] = v;
swim(N);
}
public Key delMax()
{
Key max = pq[1]; // Retrieve max key from top.
exch(1, N--); // Exchange with last item.
pq[N+1] = null; // Avoid loitering.
sink(1); // Restore heap property.
return max;
}
private boolean less(int i, int j)
private void exch(int i, int j)
private void swim(int k)
private void sink(int k)
```

For typical applications that require a large number of intermixed
insert and remove the maximum operations in a
large priority queue, Proposition Q represents an important
performance breakthrough,

Where elementary implementations using an ordered
array or an unordered array require linear time for one
of the operations, a heap-based implementation provides a
guarantee that both operations complete in logarithmic time.
This improvement can make the difference between solving a
problem and not being able to address it at all.


### Multiway heaps.

There is a tradeoff between the lower cost from the reduced tree height
(log d N) and the higher cost of finding the largest of the d
children at each node. This tradeoff is dependent on details
of the implementation and the expected relative frequency of
operations.

### Immutability of keys

The priority queue contains objects that are created by clients
but assumes that client code does not change the keys. It is possible to develop mechanisms to enforce this assumption, but programmers typically do not do so because they complicate the code and are likely
to degrade performance.

### Index priority queue

In many applications, it makes sense to allow clients to refer
to items that are already on the priority queue. One easy way to do so is to associate
a unique integer index with each item.

```java
public class I ndexMinPQ<Item extends Comparable<Item>>
{
IndexMinPQ(int maxN) // create a priority queue of capacity maxN with possible indices between 0 and maxN-1
void insert(int k, Item item) // insert item ; associate it with k
void change(int k, Item item) // change the item associated with k to item
boolean contains(int k) // is k associated with some item?
void delete(int k) // remove k and its associated item
Item min() // return a minimal item
int minIndex() // return a minimal item’s index
int delMin() // remove a minimal item and return its index
boolean isEmpty() // is the priority queue empty?
int size() // number of items in the priority queue
}
```

A useful way of thinking of this data type is as implementing an array, but with fast access
to the smallest entry in the array. Actually it does even better—it gives fast access
to the minimum entry in a specified subset of an array’s entries

### Index priority-queue client.

```java
public class Multiway {
    public static void merge(In[] streams) {
        int N = streams.length;
        IndexMinPQ<String> pq = new IndexMinPQ<String>(N);
        
        for (int i = 0; i < N; i++)
            if (!streams[i].isEmpty())
                pq.insert(i, streams[i].readString());
        
        while (!pq.isEmpty()) {
            StdOut.println(pq.min());
            int i = pq.delMin();
            
            if (!streams[i].isEmpty())
                pq.insert(i, streams[i].readString());
        }
    }

    public static void main(String[] args) {
        int N = args.length;
        In[] streams = new In[N];
        
        for (int i = 0; i < N; i++)
            streams[i] = new In(args[i]);
        
        merge(streams);
    }
}
```

## Heapsort

We insert all the items to be sorted into a minimum-oriented priority queue, then repeatedly use
remove the minimum to remove them all in order. Using a priority queue represented as
an unordered array in this way corresponds to doing a selection sort; using an ordered
array corresponds to doing an insertion sort.

Heapsort breaks into two phases: heap construction, where we reorganize the original
array into a heap, and the sortdown, where we pull the items out of the heap in decreasing
order to build the sorted result.

Focusing on the task of sorting, we abandon the notion of hiding the representation of the
priority queue and use swim() and sink() directly. Doing so allows us to sort an array
without needing any extra space, by maintaining the heap within the array to be sorted.

### Heap Construction

```java
public static void sort(Comparable[] a) {
    int N = a.length;
    
    for (int k = N/2; k >= 1; k--)
        sink(a, k, N);
    
    while (N > 1) {
        exch(a, 1, N--);
        sink(a, 1, N);
    }
}
```

### Sortdown

Most of the work during heapsort is done during the second phase, where we remove the largest remaining item from the heap and put it into the array position vacated as the heap shrinks. This process is a bit like selection sort, but it uses many fewer compares because the heap provides a much more efficient way to find the largest item in the unsorted part of the array.

### Sink to the bottom, then swim

Most items reinserted into the heap during sortdown go all the way to the bottom.

**Significance of Heapsort in Sorting Complexity:**

Heapsort holds a pivotal role in the exploration of sorting complexities due to its unique optimality in both time and space utilization. It stands out as the sole method known to be optimal, guaranteeing ~2N lg N compares and requiring constant extra space in the worst case. When confronted with tight space constraints, Heapsort gains popularity for its ability to be implemented with just a few dozen lines, all while delivering optimal performance.

Despite these advantages, Heapsort finds limited use in typical applications on modern systems. The primary deterrent is its suboptimal cache performance—array entries are infrequently compared with nearby entries, resulting in a considerably higher number of cache misses compared to algorithms like quicksort, mergesort, and even shellsort, where most comparisons involve nearby entries.

**Heaps in Priority Queue Implementation:**

Conversely, the use of heaps to implement priority queues has gained prominence in modern applications. This approach proves invaluable by ensuring logarithmic running time in dynamic scenarios where a substantial number of insert and remove-the-maximum operations are intermixed.

# 2.5 APPLICATIONS

A prime reason why sorting is so useful is that it is much easier to search for an item
in a sorted array than in an unsorted one.

Most important is the system sort, so we begin by considering a number of practical
considerations that come into play when building a sort for use by a broad variety of
clients.

## Sorting various types of data

Our implementations are designed to sort arrays of `Comparable` objects. Following the Java convention, this design leverages Java's callback mechanism, enabling us to sort arrays of objects of any type that implements the `Comparable` interface.

This flexibility allows us to apply our code seamlessly to sort arrays of various types, such as `String`, `Integer`, `Double`, and others like `File` and `URL`. The reason being, these data types all implement the `Comparable` interface.

We can readily use our code to sort arrays of different types, thanks to the universality of the `Comparable` interface, which ensures compatibility with a wide range of data types.

### Transaction example

A prototypical breeding ground for sorting applications is commercial data processing.

```java
public int compareTo(Transaction that)
{
	return this.when.compareTo(that.when); 
}
```

**Alternate compareTo() implementation for sorting transactions by date**

### Pointer Sorting

In our implementations, we operate on references to items and do not manipulate the data itself. In Java, pointer manipulation is implicit, with the exception of primitive numeric types.

It's important to note that pointer sorting introduces an additional level of indirection. In this context, the array comprises references to the objects to be sorted, rather than the objects themselves. This approach aligns with Java's nature, where manipulation of object references is inherent to the language.

By working with references, our sorting implementations provide a level of abstraction that allows the sorting of various objects without directly moving the data they represent.

### Keys are immutable

It stands to reason that an array might not remain sorted if a client is allowed to change the values of keys after the sort. Similarly, a priority queue can hardly be expected to operate properly if the client can change the values of keys between operations.

### Exchanges are inexpensive.

Another advantage of using references is that we avoid the cost of moving full items.

The reference approach makes the cost of an exchange roughly equal to the cost of a compare for general situations involving arbitrarily large items.



### Alternate orderings

There are many applications where we want to use different orders for the objects that we are sorting, depending on the situation.

The `Comparator` mechanism allows us to sort arrays of any type of object, using any total order that we wish to define for them.

### Items with multiple keys.

The `Comparator` mechanism is precisely what we need to allow this flexibility. We can define multiple comparators, as in the alternate implementation of `Transaction`.

```java
Insertion.sort(a, new Transaction.WhenOrder());
```

or by amount with the call

```java
Insertion.sort(a, new Transaction.HowMuchOrder());
```


```java
public static void sort(Object[] a, Comparator c) {
    int N = a.length;
    
    for (int i = 1; i < N; i++)
        for (int j = i; j > 0 && less(c, a[j], a[j-1]); j--)
            exch(a, j, j-1);
}

private static boolean less(Comparator c, Object v, Object w) {
    return c.compare(v, w) < 0;
}

private static void exch(Object[] a, int i, int j) {
    Object t = a[i];
    a[i] = a[j];
    a[j] = t;
}
```

### Priority queues with comparators

```java
import java.util.Comparator;

public class Transaction {
    // ... Other class members ...

    private final String who;
    private final Date when;
    private final double amount;

    // ... Other class methods ...

    public static class WhoOrder implements Comparator<Transaction> {
        public int compare(Transaction v, Transaction w) {
            return v.who.compareTo(w.when);
        }
    }

    public static class WhenOrder implements Comparator<Transaction> {
        public int compare(Transaction v, Transaction w) {
            return v.when.compareTo(w.when);
        }
    }

    public static class HowMuchOrder implements Comparator<Transaction> {
        public int compare(Transaction v, Transaction w) {
            if (v.amount < w.amount) return -1;
            if (v.amount > w.amount) return +1;
            return 0;
        }
    }
}
```

### Stability

A sorting method is stable if it preserves the relative order of equal keys in the array

## Which sorting algorithm should I use?

In all cases but shellsort (where the growth rate is only an estimate), insertion sort (where the growth rate depends on the order of the input keys), and both versions of quicksort (where the growth rate is probabilistic and may depend on the distribution of input key values), multiplying these growth rates by appropriate constants gives an effective way to predict running time. The constants involved are partly algorithm-dependent.

| Algorithm        | Stable | In-Place | Order of Growth | Running Time     | Extra Space |
|------------------|--------|----------|------------------|------------------|-------------|
| Selection Sort   | No     | Yes      | N^2              | O(N^2)           | O(1)        |
| Insertion Sort   | Yes    | Yes      | Between N and N^2| Depends on order| O(1)        |
|                  |        |          |                  | of items         |             |
| Shellsort        | No     | Yes      | N log N (?)      | O(N^(6/5)) ?     | O(1)        |
| Quicksort        | No     | Yes      | N log N          | O(N log N)       | O(log N)     |
| 3-way Quicksort  | No     | Yes      | Between N and    | O(N log N)       | O(log N)     |
|                  |        |          | N log N          |                  |             |
| Mergesort        | Yes    | No       | N log N          | O(N log N)       | O(N)        |
| Heapsort         | No     | Yes      | N log N          | O(N log N)       | O(1)        |


***Quicksort is the fastest general-purpose sort.***

Thus, in most practical situations, quicksort is the method of choice.

### Sorting primitive types.

In some performance-critical applications, the focus may be on sorting numbers, so it is reasonable to avoid the costs of using references and sort primitive types instead.

- A different method is implemented for each primitive type.
- A method is provided for data types that implement `Comparable`.
- Another method utilizes a `Comparator`.

Java's systems programmers have opted for the following sorting algorithms:

- For primitive-type methods, quicksort (with 3-way partitioning) is employed.
- For reference-type methods, mergesort is chosen.

The key practical implications of these choices are, as discussed earlier, a trade-off between speed and memory usage for primitive types and stability for reference types.

## Reductions

The concept that sorting algorithms can be leveraged to solve other problems illustrates a fundamental technique in algorithm design known as **reduction**. In this context, a reduction occurs when an algorithm initially designed for one problem is repurposed to solve another.

Every instance where a method devised for solving problem B is utilized to address problem A represents a reduction from A to B. In algorithm implementation, a key objective is to foster reductions by creating algorithms that are versatile and applicable across a broad range of scenarios.

### Duplicates

When dealing with large arrays, employing a quadratic algorithm becomes impractical. Sorting, however, provides a solution to questions in linearithmic time:

The approach involves initially sorting the array, followed by traversing the sorted array to identify duplicate keys that appear consecutively. This two-step process allows for efficient handling of duplicate keys within the ordered array.

### Rankings

A **permutation** (or ranking) is represented as an array of N integers, where each integer between 0 and N-1 appears exactly once. The **Kendall tau distance** between two rankings is defined as the number of pairs that are in a different order in the two rankings.

```java
Quick.sort(a);
int count = 1; // Assume a.length > 0.
for (int i = 1; i < a.length; i++) {
    if (a[i].compareTo(a[i - 1]) != 0) {
        count++;
    }
}
```

**Counting the distinct keys in a[]**

### Median and order statistics

An important application related to sorting, where a full sort is not necessary, is the operation of finding the median of a collection of keys. This operation is a common computation in statistics and various other data-processing applications.

## A brief survey of sorting applications

### Commercial computing

Government organizations, financial institutions, and commercial enterprises often manage vast amounts of information by employing sorting techniques. Typically, this information is structured in extensive databases, sorted by multiple keys to facilitate efficient search operations. An effective strategy widely adopted in these domains involves the process of collecting new information, adding it to the database, sorting it based on the keys of interest, and merging the sorted results for each key into the existing database.

### Search for information

Keeping data in sorted order makes it possible to efficiently search through it using the classic binary search algorithm

### Operations research

The field of operations research (OR) specializes in developing and applying mathematical models for problem-solving and decision-making. One prevalent problem in OR is known as scheduling. In this scenario, consider having N jobs to complete, where each job �j requires ��tj​ seconds of processing time. The objective is to complete all jobs while aiming to maximize customer satisfaction by minimizing the average completion time.

A widely acknowledged strategy to achieve this goal is the shortest processing time first rule, where jobs are scheduled in increasing order of processing time. To implement this rule, one can either sort the jobs by processing time or use a minimum-oriented priority queue.

### Event-driven simulation

Many scientific applications involve simulation, where the primary objective of the computation is to model some aspect of the real world, enabling a better understanding of it. In the era before computing, scientists had limited options and often resorted to building mathematical models for this purpose. However, with the advent of computing, these mathematical models are now well-complemented by computational models.

### Numerical computations.

Scientific computing frequently revolves around accuracy, emphasizing the proximity of computed results to the true answer. The significance of accuracy becomes particularly pronounced when dealing with millions of computations involving estimated values, such as the floating-point representation of real numbers commonly used in computer systems.

### Combinatorial search

A classic paradigm in artificial intelligence and in coping with intractable problems involves defining a set of configurations with well-defined moves from one configuration to the next, each associated with a priority. This paradigm provides a structured approach to addressing complex problems and is foundational in various fields.

### Prim’s algorithm and Dijkstra’s algorithm

These classical algorithms are derived from Chapter 4, which is dedicated to algorithms that process graphs—a fundamental model for items and edges that connect pairs of items. The chapter explores various algorithms designed to operate on graphs, showcasing their significance in solving problems related to items and their interconnected relationships.

### Kruskal’s algorithm

is another classic algorithm for graphs whose edges have weights that depends upon processing the edges in order of their weight

### Huffman compression

This is a classic data compression algorithm that relies on processing a set of items with integer weights. The algorithm involves combining the two smallest items to produce a new one whose weight is the sum of its two constituents. This approach forms the foundation of the algorithm's strategy for data compression.

### String-processing

algorithms, which are of critical importance in modern applications in cryptology and in genomic, are often based on sorting.


# SEARCHING

The ability to efficiently search through this information is fundamental to processing it. The term **symbol table** is used to describe an abstract mechanism where we save information (a value) that we can later search for and retrieve by specifying a key.

The primary purpose of a symbol table is to associate a value with a key. The client can insert key-value pairs into the symbol table with the expectation of later being able to search for the value associated with a given key, from among all of the key-value pairs that have been put into the table.

| Application            | Purpose                                 | Search Key        | Value                          |
|------------------------|-----------------------------------------|-------------------|--------------------------------|
| Dictionary             | Find definition of a word                | Word              | Definition                     |
| Book Index             | Find relevant pages                      | Term              | List of Page Numbers           |
| File Share             | Find song to download                    | Name of Song      | Computer ID                    |
| Account Management    | Process transactions                    | Account Number    | Transaction Details            |
| Web Search             | Find relevant web pages                  | Keyword           | List of Page Names             |
| Compiler               | Find type and value of a variable       | Variable Name     | Type and Value                 |

## API

## Symbol Table (ST) Implementation

### Constructors
- `ST()`: Create a symbol table.

### Methods
- `void put(Key key, Value val)`: Put a key-value pair into the table. Remove the key from the table if the value is null.
- `Value get(Key key)`: Retrieve the value paired with the given key. Return null if the key is absent.
- `void delete(Key key)`: Remove the key (and its associated value) from the table.
- `boolean contains(Key key)`: Check if there is a value paired with the given key.
- `boolean isEmpty()`: Check if the table is empty.
- `int size()`: Get the number of key-value pairs in the table.
- `Iterable<Key> keys()`: Get an iterable containing all the keys in the table.


### Generics

Consider the methods without specifying the types of the items being processed, using generics. For symbol tables, we emphasize the separate roles played by keys and values in search by specifying the key and value types explicitly instead of viewing keys as implicit in items.

### Duplicate Key

- Only one value is associated with each key (no duplicate keys in a table).
- When a client puts a key-value pair into a table already containing that key (and an associated value), the new value replaces the old one.


### Null Keys

**Keys must not be null**

### Null Value

adopt the convention that no key can be associated with the value null

### Deletion

 Deletion in symbol tables generally involves one of two strategies: lazy deletion, where we associate keys in the table with null, then perhaps remove all such keys at some later time; and eager deletion, where we remove the key from the table immediately.

```java
if (val == null) { 
	delete(key); return; 
}
```

### Shorthand methods

For clarity in client code,  the methods contains() and isEmpty() in the API

## Method Default Implementations

### `delete`

```java
void delete(Key key) {
    put(key, null);
}
```

### `contains`

```java
boolean contains(Key key) {
    return get(key) != null;
}
```

### `isEmpty`

```java
boolean isEmpty() {
    return size() == 0;
}
```

### Iteration

For symbol tables, we adopt a simpler alternative approach, where we specify a `keys()` method that returns an `Iterable<Key>` object for clients to use to iterate through the keys.

### Key Equality

Determining whether or not a given key is in a symbol table is based on the concept of object equality

## Ordered symbol tables

In typical applications, keys are `Comparable` objects, so the option exists of using the code `a.compareTo(b)` to compare two keys `a` and `b`. In such implementations, we can think of the symbol table as keeping the keys in order and consider a significantly expanded API that defines numerous natural and useful operations involving relative key order.


```java
## Symbol Table Class (ST)

```java
public class ST<Key extends Comparable<Key>, Value> {

    /**
     * Create an ordered symbol table.
     */
    public ST() {
        // Implementation goes here...
    }

    /**
     * Put key-value pair into the table (remove key from the table if value is null).
     *
     * @param key the key
     * @param val the value
     */
    public void put(Key key, Value val) {
        // Implementation goes here...
    }

    /**
     * Get the value paired with the key (null if the key is absent).
     *
     * @param key the key
     * @return the value paired with the key, or null if the key is absent
     */
    public Value get(Key key) {
        // Implementation goes here...
    }

    /**
     * Remove the key (and its value) from the table.
     *
     * @param key the key to be removed
     */
    public void delete(Key key) {
        // Implementation goes here...
    }

    /**
     * Check if there is a value paired with the key.
     *
     * @param key the key
     * @return true if there is a value paired with the key, false otherwise
     */
    public boolean contains(Key key) {
        // Implementation goes here...
    }

    /**
     * Check if the table is empty.
     *
     * @return true if the table is empty, false otherwise
     */
    public boolean isEmpty() {
        // Implementation goes here...
    }

    /**
     * Get the number of key-value pairs in the table.
     *
     * @return the number of key-value pairs
     */
    public int size() {
        // Implementation goes here...
    }

    /**
     * Get the smallest key.
     *
     * @return the smallest key
     */
    public Key min() {
        // Implementation goes here...
    }

    /**
     * Get the largest key.
     *
     * @return the largest key
     */
    public Key max() {
        // Implementation goes here...
    }

    /**
     * Get the largest key less than or equal to the specified key.
     *
     * @param key the key
     * @return the largest key less than or equal to the specified key
     */
    public Key floor(Key key) {
        // Implementation goes here...
    }

    /**
     * Get the smallest key greater than or equal to the specified key.
     *
     * @param key the key
     * @return the smallest key greater than or equal to the specified key
     */
    public Key ceiling(Key key) {
        // Implementation goes here...
    }

    /**
     * Get the number of keys less than the specified key.
     *
     * @param key the key
     * @return the number of keys less than the specified key
     */
    public int rank(Key key) {
        // Implementation goes here...
    }

    /**
     * Get the key of rank k.
     *
     * @param k the rank
     * @return the key of rank k
     */
    public Key select(int k) {
        // Implementation goes here...
    }

    /**
     * Delete the smallest key.
     */
    public void deleteMin() {
        // Implementation goes here...
    }

    /**
     * Delete the largest key.
     */
    public void deleteMax() {
        // Implementation goes here...
    }

    /**
     * Get the number of keys in the specified range [lo..hi].
     *
     * @param lo the low end of the range
     * @param hi the high end of the range
     * @return the number of keys in the specified range
     */
    public int size(Key lo, Key hi) {
        // Implementation goes here...
    }

    /**
     * Get an iterable of keys in the specified range [lo..hi], in sorted order.
     *
     * @param lo the low end of the range
     * @param hi the high end of the range
     * @return keys in the specified range, in sorted order
     */
    public Iterable<Key> keys(Key lo, Key hi) {
        // Implementation goes here...
    }

    /**
     * Get an iterable of all keys in the table, in sorted order.
     *
     * @return all keys in the table, in sorted order
     */
    public Iterable<Key> keys() {
        // Implementation goes here...
    }
}
```

### Minimum and maximum

The most natural queries for a set of ordered keys are to ask for the smallest and largest keys. The primary differences are that equal keys are allowed in priority queues but not in symbol tables and that ordered symbol tables support a much larger set of operations.

### Floor and ceiling

Given a key, it is often useful to be able to perform the floor operation (find the largest key that is less than or equal to the given key) and the ceiling operation (find the smallest key that is greater than or equal to the given key).

### Rank and selection

The basic operations for determining where a new key fits in the order are the rank operation (find the number of keys less than a given key) and the select operation (find the key with a given rank).

### Range queries

How many keys fall within a given range (between two given keys)? Which keys fall in a given range?

The capability to handle such queries is one prime reason that ordered symbol tables are so widely used in practice.

### Exceptional cases

When a method is to return a key and there is no key fitting the description in the table, our convention is to throw an exception

### Shorthand methods

## Default Implementations for Redundant Order-based Symbol-Table Methods

### `deleteMin`

- **Description:** Delete the smallest key.
- **Implementation:** `void deleteMin() { delete(min()); }`

### `deleteMax`

- **Description:** Delete the largest key.
- **Implementation:** `void deleteMax() { delete(max()); }`

### `size`

- **Description:** Get the number of keys in the specified range `[lo..hi]`.
- **Implementation:**
  ```java
  int size(Key lo, Key hi) {
      if (hi.compareTo(lo) < 0)
          return 0;
      else if (contains(hi))
          return rank(hi) - rank(lo) + 1;
      else
          return rank(hi) - rank(lo);
  }
```

### `keys`

- **Description:** Get an iterable of all keys in the table, in sorted order.
- **Implementation:** `Iterable<Key> keys() { return keys(min(), max()); }`

### Key equality (revisited)

The best practice in Java is to make ``compareTo()`` consistent with equals() in all Comparable types.

To avoid any potential ambiguities, we avoid the use of equals() in ordered symbol-table implementations. Instead, we use ``compareTo()`` exclusively to compare keys

### Cost Model



>When studying symbol-table implementations, we count compares (equality tests or key comparisons). In (rare) cases where compares are not in the inner loop, we count array accesses.

---


Symbol-table implementations are generally characterized by their underlying data structures and their implementations of get() and put().

## Sample clients

consider two clients: a test client that we use to trace algorithm behavior on small inputs and a performance client that we use to motivate the development of efficient implementations.

### Test client

```java
public static void main(String[] args) {
    ST<String, Integer> st;
    st = new ST<String, Integer>();

    for (int i = 0; !StdIn.isEmpty(); i++) {
        String key = StdIn.readString();
        st.put(key, i);
    }

    for (String s : st.keys()) {
        StdOut.println(s + " " + st.get(s));
    }
}
```

### Performance client

``FrequencyCounter``  is a symbol-table client that finds the number of occurrences of each string
in a sequence of strings from standard input, then iterates through the keys to find the one that occurs the most frequently

This client answers a simple question: Which word (no shorter than a given length) occurs most frequently in a given text?

To study performance for larger inputs, two measures are of interest:

1. **Total Number of Words in the Text:**
    
    - Each word in the input is used as a search key once.
    - This measure provides insight into the overall size of the input.
2. **Distinct Words in the Symbol Table:**
    
    - Each distinct word in the input is put into the symbol table.
    - This measure reflects the size of the symbol table and can help assess the efficiency of the symbol table implementation.

|                         | `tinyTale.txt` | `tale.txt` | `leipzig1M.txt` |
|-------------------------|----------------|------------|-----------------|
| **Words**               | 60             | 20         | 135,635         |
| **Distinct Words**      | 20             | 10,679     | 534,580         |
| **All Words**           | -              | -          | 21,191,455      |
| **At Least 8 Letters**   | 3              | 3          | 299,593         |
| **At Least 10 Letters**  | 2              | 2          | 165,555         |

## FrequencyCounter Class

```java
public class FrequencyCounter {
    public static void main(String[] args) {
        int minlen = Integer.parseInt(args[0]); // key-length cutoff
        ST<String, Integer> st = new ST<String, Integer>();

        while (!StdIn.isEmpty()) { // Build symbol table and count frequencies.
            String word = StdIn.readString();
            if (word.length() < minlen) continue; // Ignore short keys.
            if (!st.contains(word)) st.put(word, 1);
            else st.put(word, st.get(word) + 1);
        }

        // Find a key with the highest frequency count.
        String max = "";
        st.put(max, 0);
        for (String word : st.keys())
            if (st.get(word) > st.get(max))
                max = word;

        StdOut.println(max + " " + st.get(max));
    }
}
```

so the total number of distinct words in the input stream is certainly relevant.

-  Search and insert operations are intermixed.
- The number of distinct keys is not small.
- Substantially more searches than inserts are likely.
- Search and insert patterns, though unpredictable, are not random.

## Sequential search in an unordered linked list

One straightforward option for the underlying data structure for a symbol table is a linked list of nodes that contain keys and values.

Sequential search involves searching by considering the keys in the table one after another, using the `equals()` method to test for a match with our search key.

```java
## SequentialSearchST Class

```java
public class SequentialSearchST<Key, Value> {
    private Node first; // first node in the linked list

    private class Node { // linked-list node
        Key key;
        Value val;
        Node next;

        public Node(Key key, Value val, Node next) {
            this.key = key;
            this.val = val;
            this.next = next;
        }
    }

    public Value get(Key key) { // Search for key, return associated value.
        for (Node x = first; x != null; x = x.next)
            if (key.equals(x.key))
                return x.val; // search hit
        return null; // search miss
    }

    public void put(Key key, Value val) { // Search for key. Update value if found; grow table if new.
        for (Node x = first; x != null; x = x.next)
            if (key.equals(x.key)) {
                x.val = val;
                return; // Search hit: update val.
            }
        first = new Node(key, val, first); // Search miss: add new node.
    }
}
```

## Binary search in an ordered array

The data structure consists of two parallel arrays—one for keys and one for values. The core of the implementation lies in the `rank()` method, determining the count of keys smaller than a given key.

- **For `get()`:** The `rank()` precisely indicates the position of the key in the table if it exists.
    
- **For `put()`:** The `rank()` guides the exact location to update the value when the key is present in the table, and it also directs where to insert the key when it is not in the table.

```java
## BinarySearchST Class

```java
public class BinarySearchST<Key extends Comparable<Key>, Value> {
    private Key[] keys;
    private Value[] vals;
    private int N;

    public BinarySearchST(int capacity) {
        // See Algorithm 1.1 for standard array-resizing code.
        keys = (Key[]) new Comparable[capacity];
        vals = (Value[]) new Object[capacity];
    }

    public int size() {
        return N;
    }

    public Value get(Key key) {
        if (isEmpty()) return null;
        int i = rank(key);
        if (i < N && keys[i].compareTo(key) == 0) return vals[i];
        else return null;
    }

    public int rank(Key key) {
        // See page 381.
        // Implementation goes here.
    }

    public void put(Key key, Value val) {
        // Search for key. Update value if found; grow table if new.
        int i = rank(key);
        if (i < N && keys[i].compareTo(key) == 0) {
            vals[i] = val;
            return;
        }
        for (int j = N; j > i; j--) {
            keys[j] = keys[j-1];
            vals[j] = vals[j-1];
        }
        keys[i] = key;
        vals[i] = val;
        N++;
    }

    public void delete(Key key) {
        // See Exercise 3.1.16 for this method.
        // Implementation goes here.
    }
}
```

### Binary search

The rationale behind keeping keys in an ordered array is to leverage array indexing, which significantly reduces the number of compares required for each search. This approach utilizes the binary search algorithm.

In the binary search, the search key is compared against the key in the middle of the subarray. This process efficiently narrows down the search space.

The recursive `rank()` method preserves the following properties:
- If the key is in the table, `rank()` returns its index in the table. This index is equivalent to the number of keys in the table that are smaller than the key.
- If the key is not in the table, `rank()` also returns the number of keys in the table that are smaller than the key.

### Other operations

#### `rank()` Method

```java
public int rank(Key key) {
    int lo = 0, hi = N - 1;

    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;
        int cmp = key.compareTo(keys[mid]);

        if (cmp < 0) {
            hi = mid - 1;
        } else if (cmp > 0) {
            lo = mid + 1;
        } else {
            return mid; // Key found.
        }
    }

    return lo; // Key not found, return the position where the key should be inserted.
}


public Key min() {
    return keys[0];
}

public Key max() {
    return keys[N-1];
}

public Key select(int k) {
    return keys[k];
}

public Key ceiling(Key key) {
    int i = rank(key);
    return keys[i];
}

public Key floor(Key key) {
    // See Exercise 3.1.17.
    // Implementation goes here.
}

public Key delete(Key key) {
    // See Exercise 3.1.16.
    // Implementation goes here.
}

public Iterable<Key> keys(Key lo, Key hi) {
    Queue<Key> q = new Queue<Key>();
    for (int i = rank(lo); i < rank(hi); i++)
        q.enqueue(keys[i]);

    if (contains(hi))
        q.enqueue(keys[rank(hi)]);

    return q;
}
```

## Analysis of binary search

The recursive implementation of rank() also leads to an immediate argument that binary search guarantees fast search, because it corresponds to a recurrence relation that describes an upper bound on the number of compares.

> Binary search in an ordered array with N keys uses no more than lg N  1 compares for a search (successful or unsuccessful).

## Method Order of Growth of Running Time

- `put()`: O(N)
- `get()`: O(log N)
- `delete()`: O(N)
- `contains()`: O(log N)
- `size()`: O(1)
- `min()`: O(1)
- `max()`: O(1)
- `floor()`: O(log N)
- `ceiling()`: O(log N)
- `rank()`: O(log N)
- `select()`: O(1)
- `deleteMin()`: O(N)
- `deleteMax()`: O(1)



> Inserting a new key into an ordered array of size N uses ~ 2N array accesses in the worst case, so inserting N keys into an initially empty table uses ~ 	N 2 array accesses in the worst case.


## Preview

Binary search is typically far better than sequential search and is the method of choice in numerous practical applications. Even when the bulk of the key-value pairs is known before the bulk of the searches, it is worthwhile to add to `BinarySearchST` a constructor that initializes and sorts the table.

Still, it's important to note that binary search is infeasible for use in many other applications. The effectiveness of binary search comes from its ability to efficiently narrow down the search space, making it a powerful choice in scenarios where the keys are ordered.

#### Algorithm Comparison

| Algorithm (Data Structure)       | Worst-Case Cost (After N Inserts) | Average-Case Cost (After N Random Inserts) | Efficiently Supports Ordered Search, Insert, Search Hit, Insert Operations? |
|----------------------------------|------------------------------------|---------------------------------------------|--------------------------------------------------------------------------------|
| Sequential Search                | N                                  | N/2                                         | No                                                                             |
| Binary Search (Ordered Array)    | lg N                               | 2N lg N                                      | Yes                                                                            |


The central question is whether we can devise algorithms and data structures that achieve logarithmic performance for both search and insert. The answer is a resounding yes! To support efficient insertion, it seems that we need a linked structure.

To combine the efficiency of binary search with the flexibility of linked structures, we need more complicated data structures. That combination is provided by binary search trees.


| Underlying Data Structure | Implementation            | Pros                           | Cons                                  |
|---------------------------|---------------------------|--------------------------------|---------------------------------------|
| Linked List (Sequential Search) | `SequentialSearchST`   | - Best for tiny symbol tables | - Slow for large symbol tables      |
| Ordered Array (Binary Search)   | `BinarySearchST`        | - Optimal search and space    | - Slow insert                         |
| Binary Search Tree (BST)        | `BST`                   | - Easy to implement           | - No guarantees for space for links   |
| Balanced BST (Red-Black BST)    | `RedBlackBST`           | - Optimal search and insert   | - Space for links                     |
| Hash Table (Separate Chaining)  | `SeparateChainingHashST`| - Fast search/insert for common types of data | - Need hash for each type, no order-based ops, space for links/empty |
| Hash Table (Linear Probing)     | `LinearProbingHashST`   | - Fast search/insert for common types of data | - Need hash for each type, no order-based ops, space for links/empty |


# BINARY SEARCH TREES


Specifically, using two links per node (instead of the one link per node found in linked lists) leads to an efficient symbol-table implementation based on the binary search tree data structure. In data structures, nodes are made up of links that are either null or references to other nodes. 

In a binary tree, there is the restriction that every node is pointed to by just one other node, called its parent (except for one node, the root, which has no nodes pointing to it). Each node in a binary tree has exactly two links, called its left and right links, pointing to nodes referred to as its left child and right child, respectively.

If we view each link as pointing to a binary tree, it essentially refers to the tree whose root is the referenced node. Thus, we can define a binary tree as either a null link or a node with a left link and a right link, each referencing disjoint subtrees that are themselves binary trees.

In a binary search tree, each node also has a key and a value, with an ordering restriction to support efficient search.

## Basic implementation

### Representation.

Define a private nested class to represent nodes in Binary Search Trees (BSTs). Each node should include the following attributes: a key, a value, a left link, a right link, and a node count. The left link should point to a BST for items with smaller keys, and the right link should point to a BST for items with larger keys. The instance variable N gives the node count in the subtree rooted at the node.

Implement a private `size()` method within the class. This method is designed to assign the value 0 to null links, ensuring that we maintain this field by guaranteeing the specified invariant.

```java
size(x) = size(x.left) + size(x.right) + 1
```

holds for every node x in the tree

### Search

If a node containing the key is in the table, we have a search hit, so we return the associated value. Otherwise, we have a search miss (and return null). A recursive algorithm to search for a key in a BST follows immediately from the recursive structure: if the tree is empty, we have a search miss; if the search key is equal to the key at the root, we have a search hit. Otherwise, we search (recursively) in the appropriate subtree, moving left if the search key is smaller, right if it is larger.

```java
public class BST<Key extends Comparable<Key>, Value> {
    private Node root; // root of BST

    private class Node {
        private Key key; // key
        private Value val; // associated value
        private Node left, right; // links to subtrees
        private int N; // # nodes in subtree rooted here

        public Node(Key key, Value val, int N) {
            this.key = key;
            this.val = val;
            this.N = N;
        }
    }

    public int size() {
        return size(root);
    }

    private int size(Node x) {
        if (x == null) return 0;
        else return x.N;
    }

    public Value get(Key key) {
        return get(root, key);
    }

    private Value get(Node x, Key key) {
        // Return value associated with key in the subtree rooted at x;
        // return null if key not present in the subtree rooted at x.
        if (x == null) return null;
        int cmp = key.compareTo(x.key);
        if (cmp < 0) return get(x.left, key);
        else if (cmp > 0) return get(x.right, key);
        else return x.val;
    }

    public void put(Key key, Value val) {
        root = put(root, key, val);
    }

    private Node put(Node x, Key key, Value val) {
        // Change key’s value to val if key in the subtree rooted at x.
        // Otherwise, add new node to the subtree associating key with val.
        if (x == null) return new Node(key, val, 1);
        int cmp = key.compareTo(x.key);
        if (cmp < 0) x.left = put(x.left, key, val);
        else if (cmp > 0) x.right = put(x.right, key, val);
        else x.val = val;
        x.N = size(x.left) + size(x.right) + 1;
        return x;
    }
}
```

### Insert

Simplicity is an essential feature of Binary Search Trees (BSTs). A search for a key not in the tree ends at a null link, and all that is needed is to replace that link with a new node containing the key. If the tree is empty, a new node containing the key and value is returned. If the search key is less than the key at the root, the left link is set to the result of inserting the key into the left subtree. Otherwise, the right link is set to the result of inserting the key into the right subtree.

### Recursion

In the code before the recursive calls, the traversal happens on the way down the tree. It involves comparing the given key against the key at each node and moving right or left accordingly.

Conversely, in the code after the recursive calls, the traversal occurs on the way up the tree. This phase is executed after the recursive calls have processed the left and right subtrees. The post-recursive code typically involves finalizing operations or calculations as the function call stack unwinds.


New nodes are attached to null links at the bottom of the tree; the tree structure is not otherwise changed. For example, the root has the first key inserted, one of the children of the root has the second key inserted, and so forth. Because each node has two links, the tree tends to grow out, rather than just down. Moreover, only the keys on the path from the root to the sought or inserted key are examined, so the number of keys examined becomes a smaller and smaller fraction of the number of keys in the tree as the tree size increases.

### Analysis

The running times of algorithms on binary search trees depend on the shapes of the trees, which, in turn, depend on the order in which keys are inserted. In the best case, a tree with N nodes could be perfectly balanced, with approximately log₂ N nodes between the root and each null link. In the worst case, there could be N nodes on the search path. The balance in typical trees turns out to be much closer to the best case than the worst case.

### Order-based methods and deletion

An important reason that Binary Search Trees (BSTs) are widely used is that they allow us to keep the keys in order. This ordering characteristic allows clients to access key-value pairs not just by providing the key but also by leveraging the relative order of keys.


### Minimum and maximum

If the left link of the root is null, the smallest key in a Binary Search Tree (BST) is the key at the root; if the left link is not null, the smallest key in the BST is the smallest key in the subtree rooted at the node referenced by the left link. The computation is equivalent to a simple iteration (move left until finding a null link), but we use recursion for consistency. Finding the maximum key is similar, moving to the right instead of to the left.


### Floor and ceiling

If a given key, `key`, is less than the key at the root of a Binary Search Tree (BST), then the floor of `key` (the largest key in the BST less than or equal to `key`) must be in the left subtree. If `key` is greater than the key at the root, then the floor of `key` could be in the right subtree, but only if there is a key smaller than or equal to `key` in the right subtree; if not, then the key at the root is the floor of `key`.

### Selection

```java
```java
public Key min() {
    return min(root).key;
}

private Node min(Node x) {
    if (x.left == null) return x;
    return min(x.left);
}

public Key floor(Key key) {
    Node x = floor(root, key);
    if (x == null) return null;
    return x.key;
}

private Node floor(Node x, Key key) {
    if (x == null) return null;
    int cmp = key.compareTo(x.key);
    if (cmp == 0) return x;
    if (cmp < 0) return floor(x.left, key);
    Node t = floor(x.right, key);
    if (t != null) return t;
    else return x;
}
```


Suppose that we seek the key of rank k (the key such that precisely k other keys in the Binary Search Tree (BST) are smaller). If the number of keys t in the left subtree is larger than k, we look (recursively) for the key of rank k in the left subtree; if t is equal to k, we return the key at the root; and if t is smaller than k, we look (recursively) for the key of rank k - t - 1 in the right subtree.

### Rank

If the given key is equal to the key at the root, we return the number of keys t in the left subtree; if the given key is less than the key at the root, we return the rank of the key in the left subtree; and if the given key is larger than the key at the root, we return t plus one plus the rank of the key in the right subtree.

### Delete the minimum/maximum

The most difficult Binary Search Tree (BST) operation to implement is the `delete()` method that removes a key-value pair from the symbol table. For `deleteMin()`, we go left until finding a node that has a null left link, and then replace the link to that node by its right link.

```java
```java
public Key select(int k) {
    return select(root, k).key;
}

private Node select(Node x, int k) {
    // Return Node containing key of rank k.
    if (x == null) return null;
    int t = size(x.left);
    if (t > k) return select(x.left, k);
    else if (t < k) return select(x.right, k - t - 1);
    else return x;
}

public int rank(Key key) {
    return rank(key, root);
}

private int rank(Key key, Node x) {
    // Return number of keys less than x.key in the subtree rooted at x.
    if (x == null) return 0;
    int cmp = key.compareTo(x.key);
    if (cmp < 0) return rank(key, x.left);
    else if (cmp > 0) return 1 + size(x.left) + rank(key, x.right);
    else return size(x.left);
}
```

### Delete

The strategy to delete a node `x` in a Binary Search Tree (BST) is to replace it with its successor. Because `x` has a right child, its successor is the node with the smallest key in its right subtree. The replacement preserves order in the tree because there are no keys between `x.key` and the successor’s key.

To accomplish the task of replacing `x` by its successor, follow these four easy steps:
1. Save a link to the node to be deleted in `t`.
2. Set `x` to point to its successor `min(t.right)`.
3. Set the right link of `x` (which is supposed to point to the BST containing all the keys larger than `x.key`) to `deleteMin(t.right)`, the link to the BST containing all the keys that are larger than `x.key` after the deletion.
4. Set the left link of `x` (which was null) to `t.left` (all the keys that are less than both the deleted key and its successor).

```java
```java
/**
 * Deletes the minimum key from the Binary Search Tree (BST).
 */
public void deleteMin() {
    root = deleteMin(root);
}

/**
 * Helper method to delete the minimum key from the subtree rooted at x.
 *
 * @param x The root of the subtree.
 * @return The updated root of the subtree after deletion.
 */
private Node deleteMin(Node x) {
    if (x.left == null) return x.right;
    x.left = deleteMin(x.left);
    x.N = size(x.left) + size(x.right) + 1;
    return x;
}

/**
 * Deletes a key from the Binary Search Tree (BST).
 *
 * @param key The key to be deleted.
 */
public void delete(Key key) {
    root = delete(root, key);
}

/**
 * Helper method to delete a key from the subtree rooted at x.
 *
 * @param x   The root of the subtree.
 * @param key The key to be deleted.
 * @return The updated root of the subtree after deletion.
 */
private Node delete(Node x, Key key) {
    if (x == null) return null;
    int cmp = key.compareTo(x.key);
    if (cmp < 0) x.left = delete(x.left, key);
    else if (cmp > 0) x.right = delete(x.right, key);
    else {
        if (x.right == null) return x.left;
        if (x.left == null) return x.right;
        Node t = x;
        x = min(t.right); // See page 407.
        x.right = deleteMin(t.right);
        x.left = t.left;
    }
    x.N = size(x.left) + size(x.right) + 1;
    return x;
}
```

### Range queries

basic recursive BST traversal method, known as inorder traversal. print all the keys in the left subtree then print the key at the root, then print all the keys in the right subtree

```java
/**
 * Private method to print the keys of the Binary Search Tree (BST) in order.
 *
 * @param x The root of the subtree.
 */
private void print(Node x) {
    if (x == null) return;
    print(x.left);
    StdOut.println(x.key);
    print(x.right);
}
```

```java
```java
/**
 * Returns an iterable containing all keys in the Binary Search Tree (BST) between the minimum and maximum keys.
 *
 * @return An iterable containing all keys in the BST.
 */
public Iterable<Key> keys() {
    return keys(min(), max());
}

/**
 * Returns an iterable containing keys in the Binary Search Tree (BST) between the given range [lo, hi].
 *
 * @param lo The lower bound of the range.
 * @param hi The upper bound of the range.
 * @return An iterable containing keys in the specified range.
 */
public Iterable<Key> keys(Key lo, Key hi) {
    Queue<Key> queue = new Queue<Key>();
    keys(root, queue, lo, hi);
    return queue;
}

/**
 * Private helper method to collect keys in the Binary Search Tree (BST) within the given range [lo, hi].
 *
 * @param x     The root of the subtree.
 * @param queue The queue to store the keys.
 * @param lo    The lower bound of the range.
 * @param hi    The upper bound of the range.
 */
private void keys(Node x, Queue<Key> queue, Key lo, Key hi) {
    if (x == null) return;
    int cmplo = lo.compareTo(x.key);
    int cmphi = hi.compareTo(x.key);
    if (cmplo < 0) keys(x.left, queue, lo, hi);
    if (cmplo <= 0 && cmphi >= 0) queue.enqueue(x.key);
    if (cmphi > 0) keys(x.right, queue, lo, hi);
}
```

In summary, BSTs are not difficult to implement and can provide fast search and insert
for practical applications of all kinds if the key insertions are well-approximated by the
random-key model.


In summary, Binary Search Trees (BSTs) are not difficult to implement and can provide fast search and insert for practical applications of all kinds if the key insertions are well-approximated by the random-key model. Many programmers choose BSTs for symbol-table implementations because they also support fast rank, select, delete, and range query operations. Good performance of the basic BST implementation is dependent on the keys being sufficiently similar to random keys that the tree is not likely to contain many long paths. Unlike quicksort, which can be randomized, achieving a similar randomization effect in a symbol-table API is not straightforward.

| Data Structure               | Worst-Case Cost (After N Inserts) | Average-Case Cost (After N Random Inserts) | Efficiently Supports Ordered Search, Insert, and Operations? |
| ---------------------------- | --------------------------------- | -------------------------------------------- | ----------------------------------------------------------- |
| Sequential Search            | N                                 | N                                            | N/2                                                           | No                                                          |
| Binary Search (Ordered Array) | lg N                              | N lg N                                       | N/2                                                           | Yes                                                         |
| Binary Tree Search (BST)      | N                                 | 1.39 lg N                                    | 1.39 lg N                                                     | Yes                                                         |


# BALANCED SEARCH TREES

Costs are guaranteed to be logarithmic, no matter what sequence of keys is used to construct them. Ideally, we would like to keep our binary search trees perfectly balanced. In an N-node tree, we would like the height to be approximately log base 2 of N so that we can guarantee that all searches can be completed in approximately log base 2 of N compares, just as for binary search. Unfortunately, maintaining perfect balance for dynamic insertions is too expensive.

## 2-3 trees

The primary step to get the flexibility that we need to guarantee balance in search trees is to allow the nodes in our trees to hold more than one key. Specifically, referring to the nodes in a standard Binary Search Tree (BST) as 2-nodes.

---

A 2-3 search tree is a tree that is either empty or:
- A 2-node, with one key (and associated value) and two links, a left link to a 2-3 search tree with smaller keys, and a right link to a 2-3 search tree with larger keys.
- A 3-node, with two keys (and associated values) and three links, a left link to a 2-3 search tree with smaller keys, a middle link to a 2-3 search tree with keys between the node’s keys, and a right link to a 2-3 search tree with larger keys.

As usual, we refer to a link to an empty tree as a null link.

---

A perfectly balanced 2-3 search tree is one whose null links are all the same distance from the root. To be concise, we use the term 2-3 tree to refer to a perfectly balanced 2-3 search tree.


### Search

To determine whether a key is in the tree, we compare it against the keys at the root. If it is equal to any of them, we have a search hit; otherwise, we follow the link from the root to the subtree corresponding to the interval of key values that could contain the search key. If that link is null, we have a search miss; otherwise, we recursively search in that subtree.

### Insert into a 2-node

In an unsuccessful search, we could hook on the node at the bottom, as we did with Binary Search Trees (BSTs), but the new tree would not remain perfectly balanced. The primary reason that 2-3 trees are useful is that we can do insertions and still maintain perfect balance. It is easy to accomplish this task if the node at which the search terminates is a 2-node: we just replace the node with a 3-node containing its key and the new key to be inserted.

### Global properties

These local transformations preserve the global properties that the tree is ordered and perfectly balanced: the number of links on the path from the root to any null link is the same. If the length of every path from a root to a null link is h before the transformation, then it is h after the transformation. Each transformation preserves this property, even while splitting the 4-node into two 2-nodes and while changing the parent from a 2-node to a 3-node or from a 3-node into a temporary 4-node.

## Red-black BSTs

### Encoding 3-nodes

The basic idea behind red-black Binary Search Trees (BSTs) is to encode 2-3 trees by starting with standard BSTs and adding extra information to encode 3-nodes. Think of the links as being of two different types: red links, which bind together two 2-nodes to represent 3-nodes, and black links, which bind together the 2-3 tree. Specifically, we represent 3-nodes as two 2-nodes connected by a single red link that leans left. One advantage of using such a representation is that it allows us to use our `get()` code for standard BST search without modification. Given any 2-3 tree, we can immediately derive a corresponding BST, just by converting each node as specified.

### An equivalent definition

Another way to proceed is to define red-black Binary Search Trees (BSTs) as BSTs having red and black links and satisfying the following three restrictions:
- Red links lean left.
- No node has two red links connected to it.
- The tree has perfect black balance: every path from the root to a null link has the same number of black links.

### Color representation

For convenience, since each node is pointed to by precisely one link (from its parent), we encode the color of links in nodes by adding a boolean instance variable `color` to our `Node` data type, which is true if the link from the parent is red and false if it is black. By convention, null links are black. For clarity in our code, we define constants `RED` and `BLACK` for use in setting and testing this variable.

```java
```java
private static final boolean RED = true;
private static final boolean BLACK = false;

private class Node {
    Key key;        // key
    Value val;      // associated data
    Node left, right;  // subtrees
    int N;          // # nodes in this subtree
    boolean color;  // color of link from parent to this node

    Node(Key key, Value val, int N, boolean color) {
        this.key = key;
        this.val = val;
        this.N = N;
        this.color = color;
    }
}

private boolean isRed(Node x) {
    if (x == null) return false;
    return x.color == RED;
}
```


### Rotations

The implementation that we will consider might allow right-leaning red links or two red links in a row during an operation, but it always corrects these conditions before completion, through judicious use of an operation called rotation that switches the orientation of red links.

### Resetting the link in the parent after a rotation

Whether left or right, every rotation leaves us with a link. We always use the link returned by `rotateRight()` or `rotateLeft()` to reset the appropriate link in the parent. This might allow two red links in a row to occur within the tree.

```java
h = rotateLeft(h);
```

```java
```java
Node rotateRight(Node h) {
    Node x = h.left;
    h.left = x.right;
    x.right = h;
    x.color = h.color;
    h.color = RED;
    x.N = h.N;
    h.N = 1 + size(h.left) + size(h.right);
    return x;
}
```


We can use rotations to help maintain the 1-1 correspondence between 2-3 trees and red-black BSTs as new keys are inserted because they preserve the two defining properties of red-black BSTs: order and perfect black balance.


### Insert into a single 2-node

A red-black BST with 1 key is just a single 2-node. Inserting the second key immediately shows the need for having a rotation operation. If the new key is smaller than the key in the tree, we just make a new (red) node with the new key, and we are done: we have a red-black BST that is equivalent to a single 3-node. But if the new key is larger than the key in the tree, then attaching a new (red) node gives a right-leaning red link, and the code `root = rotateLeft(root);` completes the insertion by rotating the red link to the left and updating the tree root link.

### Insert into a 2-node at the bottom

Insert keys into a red-black BST as usual into a BST, adding a new node at the bottom (respecting the order) but always connected to its parent with a red link. If the parent is a 2-node, then the same two cases just discussed are effective. If the new node is attached to the left link, the parent simply becomes a 3-node; if it is attached to a right link, we have a 3-node leaning the wrong way, but a left rotation finishes the job.

### Insert into a tree with two keys (in a 3-node).

This case reduces to three subcases: the new key is either less than both keys in the tree, between them, or greater than both of them.

- The simplest of the three cases is when the new key is larger than the two in the tree and is therefore attached on the rightmost link of the 3-node, making a balanced tree with the middle key at the root, connected with red links to nodes containing a smaller and a larger key.

- If the new key is smaller than the two keys in the tree and goes on the left link, then we have two red links in a row, both leaning to the left, which we can reduce to the previous case by rotating the top link to the right.

- If the new key goes between the two keys in the tree, we again have two red links in a row, a right-leaning one below a left-leaning one, which we can reduce to the previous case by rotating left the bottom link.

### Flipping colors

A critically important characteristic of this operation is that, like rotations, it is a local transformation that preserves perfect black balance in the tree. Moreover, this convention immediately leads us to a full implementation.

### Keeping the root black

A red root implies that the root is part of a 3-node, but that is not the case, so we color the root black after each insertion whenever the color of the root is flipped from black to red.

In summary, we can maintain our 1-1 correspondence between 2-3 trees and red-black BSTs during insertion by judicious use of three simple operations: left rotate, right rotate, and color flip. On each node as we pass up the tree from the point of insertion:
- If the right child is red and the left child is black, rotate left.
- If both the left child and its left child are red, rotate right.
- If both children are red, flip colors.


## Implementation

```java
ALGORITHM 3.4 Insert for red-black BSTs
public class RedBlackBST<Key extends Comparable<Key>, Value>
{
private Node root;
private class Node // BST node with color bit (see page 433)
private boolean isRed(Node h) // See page 433.
private Node rotateLeft(Node h) // See page 434.
private Node rotateRight(Node h) // See page 434.
private void flipColors(Node h) // See page 436.
private int size() // See page 398.
public void put(Key key, Value val)
{ // Search for key. Update value if found; grow table if new.
root = put(root, key, val);
root.color = BLACK;
}
private Node put(Node h, Key key, Value val)
{
if (h == null) // Do standard insert, with red link to parent.
return new Node(key, val, 1, RED);
int cmp = key.compareTo(h.key);
if (cmp < 0) h.left = put(h.left, key, val);
else if (cmp > 0) h.right = put(h.right, key, val);
else h.val = val;
if (isRed(h.right) && !isRed(h.left)) h = rotateLeft(h);
if (isRed(h.left) && isRed(h.left.left)) h = rotateRight(h);
if (isRed(h.left) && isRed(h.right)) flipColors(h);
h.N = size(h.left) + size(h.right) + 1;
return h;
}
```

### Top-down 2-3-4 trees

To implement this algorithm with red-black BSTs, we:
- Represent 4-nodes as a balanced subtree of three 2-nodes, with both the left and right child connected to the parent with a red link.
- Split 4-nodes on the way down the tree with color flips.
- Balance 4-nodes on the way up the tree with rotations, as for insertion.

### Delete the minimum

The basic idea is based on the observation that we can easily delete a key from a 3-node at the bottom of the tree, but not from a 2-node. Deleting the key from a 2-node leaves a node with no keys; the natural thing to do would be to replace the node with a null link, but that operation would violate the perfect balance condition. So, we adopt the following approach: to ensure that we do not end up on a 2-node.

### Delete

If the search key is at the bottom, we can just remove it. If the key is not at the bottom, then we have to exchange it with its successor as in regular BSTs. Then, since the current node is not a 2-node, we have reduced the problem to deleting the minimum in a subtree whose root is not a 2-node, and we can use the procedure just described for that subtree. After the deletion, as usual, we split any remaining 4-nodes on the search path on the way up the tree.

## Properties of red-black BSTs

All symbol-table operations in red-black BSTs are guaranteed to be logarithmic in the size of the tree (except for range search, which additionally costs time proportional to the number of keys returned).

### Ordered symbol-table API

One of the most appealing features of red-black BSTs is that the complicated code is limited to the `put()` (and deletion) methods. Our code for the minimum/maximum, select, rank, floor, ceiling, and range queries in standard BSTs can be used without any change, since it operates on BSTs and has no need to refer to the node color.

| Data Structure              | Worst-case cost (after N inserts) | Average-case cost (after N random inserts) | Efficiently Support Ordered Search | Efficiently Support Ordered Insert |
|-----------------------------|----------------------------------|---------------------------------------------|-------------------------------------|-------------------------------------|
| Sequential Search (Unordered Linked List) | N | N | N/2 | No |
| Binary Search (Ordered Array) | lg N | N | lg N | N/2 | Yes |
| Binary Tree Search (BST) | N | N | 1.39 lg N | 1.39 lg N | Yes |
| 2-3 Tree Search (Red-Black BST) | 2 lg N | 2 lg N | 1.00 lg N | 1.00 lg N | Yes |

**Cost summary for symbol-table implementations (updated)**

# HASH TABLES

If keys are small integers, we can use an array to implement an unordered symbol table, by interpreting the key as an array index so that we can store the value associated with key i in array entry i, ready for immediate access.

Search algorithms that use hashing consist of two separate parts. The first part is to compute a hash function that transforms the search key into an array index known as the hash value. The second part of a hashing search is a collision-resolution process that deals with this situation. After describing ways to compute hash functions, we shall consider two different approaches to collision resolution: separate chaining and linear probing.

Hashing provides a way to use a reasonable amount of both memory and time to strike a balance between these two extremes

## Hash functions

The first problem that we face is the computation of the hash function, which transforms keys into array indices. We seek a hash function that is both easy to compute and uniformly distributes the keys: for each key, every integer between 0 and M – 1 should be equally likely.

In principle, any key can be represented as a sequence of bits.

### Typical example

Where the keys are U.S. social security numbers. A social security number, such as 123-45-6789, is a nine-digit number divided into three fields. The first field identifies the geographical area where the number was issued, and the other two fields identify the individual.

One possible approach to implementing a hash function is to use three digits from the key. However, a better approach is to use all nine digits to make an int value, and then consider hash functions for integers.

### Positive integers

The most commonly used method for hashing integers is called modular hashing. We choose the array size \(M\) to be prime, and for any positive integer key \(k\), compute the remainder when dividing \(k\) by \(M\).

### Floating-point numbers

If the keys are real numbers between 0 and 1, a common method is to multiply by \(M\) and round off to the nearest integer to obtain an index between 0 and \(M – 1\). However, this approach is defective as it gives more weight to the most significant bits of the keys.

### Strings

**simply treat them as huge integers.**

```java
int hash = 0;
for (int i = 0; i < s.length(); i++) {
    hash = (R * hash + s.charAt(i)) % M;
}
```

### Compound Keys

```java
int hash = (((day * R + month) % M ) * R + year) % M;
```

### Java Conventions

The implementation of `hashCode()` for a data type must be consistent with `equals`. That is, if `a.equals(b)` is true, then `a.hashCode()` must have the same numerical value as `b.hashCode()`. Conversely, if the `hashCode()` values are different, then we know that the objects are not equal. If the `hashCode()` values are the same, the objects may or may not be equal, and we must use `equals()` to decide which condition holds.

### Converting a hashCode() to an array index.

```java
private int hash(Key x) {
    return (x.hashCode() & 0x7fffffff) % M;
}
```

### User-defined hashCode()

Client code expects that `hashCode()` disperses the keys uniformly among the possible 32-bit result values. In Java, the convention that all data types inherit a `hashCode()` method enables an even simpler approach: use the  `hashCode()` method for the instance variables to convert each to a 32-bit int value and then do the arithmetic.

```java
public class Transaction {
    // Other class members...

    private final String who;
    private final Date when;
    private final double amount;

    public int hashCode() {
        int hash = 17;
        hash = 31 * hash + who.hashCode();
        hash = 31 * hash + when.hashCode();
        hash = 31 * hash + ((Double) amount).hashCode();
        return hash;
    }

    // Other class methods...
}
```

In summary, a well-designed hash function for a given data type should meet the following three primary requirements:

1. **Consistency:** The hash function should be consistent, meaning that equal keys must produce the same hash value.

2. **Efficiency:** The hash function should be efficient to compute, ensuring that the hashing process is not computationally expensive.

3. **Uniform Distribution:** The hash function should uniformly distribute the keys, aiming to avoid clustering and ensuring a balanced distribution of hash values across the hash table.


## Hashing with separate chaining

A hash function converts keys into array indices.
The second component of a hashing algorithm is **collision resolution**: a strategy for handling the case when two or more keys to be inserted hash to the same index. A straightforward and general approach to collision resolution is to build, for each of the M array indices, a linked list of the key-value pairs whose keys hash to that index. This method is known as **separate chaining** because items that collide are chained together in separate linked lists.

```java
ALGORITHM 3.5 Hashing with separate chaining

public class SeparateChainingHashST<Key, Value>
{
    private int N; // number of key-value pairs
    private int M; // hash table size
    private SequentialSearchST<Key, Value>[] st; // array of ST objects

    public SeparateChainingHashST()
    {
        this(997);
    }

    public SeparateChainingHashST(int M)
    {
        // Create M linked lists.
        this.M = M;
        st = (SequentialSearchST<Key, Value>[]) new SequentialSearchST[M];
        for (int i = 0; i < M; i++)
            st[i] = new SequentialSearchST();
    }

    private int hash(Key key)
    {
        return (key.hashCode() & 0x7fffffff) % M;
    }

    public Value get(Key key)
    {
        return (Value) st[hash(key)].get(key);
    }

    public void put(Key key, Value val)
    {
        st[hash(key)].put(key, val);
    }

    public Iterable<Key> keys()
    {
        // See Exercise 3.4.19.
    }
}
```

### Table size

In a separate-chaining implementation, our goal is to choose the table size M to be sufficiently small that we do not waste a huge area of contiguous memory with empty chains but sufficiently large that we do not waste time searching through long chains. One of the virtues of separate chaining is that this decision is not critical: if more keys arrive than expected, then searches will take a little longer than if we had chosen a bigger table size ahead of time; if fewer keys are in the table, then we have extra-fast search with some wasted space. When space is not a critical resource, M can be chosen sufficiently large that search time is constant; when space is a critical resource, we still can get a factor of M improvement in performance by choosing M to be as large as we can afford.

### Deletion

To delete a key-value pair, simply hash to find the SequentialSearchST containing the key, then invoke the delete() method for that table

### Ordered operations

The whole point of hashing is to uniformly disperse the keys, so any order in the keys is lost when hashing. If you need to quickly find the maximum or minimum key, find keys in a given range, or implement any of the other operations, 


Hashing with separate chaining is easy to implement and probably the fastest (and most widely used) symbol-table implementation for applications where key order is not important. When your keys are built-in Java types or your own type with well-tested implementations of `hashCode()`,



## Hashing with linear probing

Another approach to implementing hashing is to store N key-value pairs in a hash table of size M > N, relying on empty entries in the table to help with collision resolution. Such methods are called open-addressing hashing methods. The simplest open-addressing method is called linear probing: when there is a collision then we just check the next entry in the table (by incrementing the index). Linear probing is characterized by identifying three possible outcomes:
- Key equal to search key: search hit
- Empty position (null key at indexed position): search miss
- Key not equal to search key: try next entry

```java
# ALGORITHM 3.6 Hashing with linear probing

```java
public class LinearProbingHashST<Key, Value>
{
    private int N; // number of key-value pairs in the table
    private int M = 16; // size of linear-probing table
    private Key[] keys; // the keys
    private Value[] vals; // the values

    public LinearProbingHashST()
    {
        keys = (Key[]) new Object[M];
        vals = (Value[]) new Object[M];
    }

    private int hash(Key key)
    {
        return (key.hashCode() & 0x7fffffff) % M;
    }

    private void resize() // See page 474.
    {
        // Resize implementation
    }

    public void put(Key key, Value val)
    {
        if (N >= M / 2) resize(2 * M); // double M (see text)
        int i;
        for (i = hash(key); keys[i] != null; i = (i + 1) % M)
        {
            if (keys[i].equals(key))
            {
                vals[i] = val;
                return;
            }
        }
        keys[i] = key;
        vals[i] = val;
        N++;
    }

    public Value get(Key key)
    {
        for (int i = hash(key); keys[i] != null; i = (i + 1) % M)
        {
            if (keys[i].equals(key))
            {
                return vals[i];
            }
        }
        return null;
    }
}
```


The essential idea behind hashing with open addressing is this: rather than using memory space for references in linked lists, we use it for the empty entries in the hash table, which mark the ends of probe sequences.

### Deletion

```java
public void delete(Key key)
{
    if (!contains(key)) return;
    
    int i = hash(key);
    while (!key.equals(keys[i]))
        i = (i + 1) % M;
    
    keys[i] = null;
    vals[i] = null;
    
    i = (i + 1) % M;
    while (keys[i] != null)
    {
        Key keyToRedo = keys[i];
        Value valToRedo = vals[i];
        keys[i] = null;
        vals[i] = null;
        N--;
        put(keyToRedo, valToRedo);
        i = (i + 1) % M;
    }
    
    N--;
    if (N > 0 && N == M/8) resize(M/2);
}
```

As with separate chaining, the performance of hashing with open addressing depends on the ratio n / m

### Clustering

The average cost of linear probing depends on the way in which the entries clump together into contiguous groups of occupied table entries, called clusters, when they are inserted.

## Array resizing

```java
private void resize(int cap)
{
    LinearProbingHashST<Key, Value> t;
    t = new LinearProbingHashST<Key, Value>(cap);
    for (int i = 0; i < M; i++)
        if (keys[i] != null)
            t.put(keys[i], vals[i]);
    keys = t.keys;
    vals = t.vals;
    M = t.M;
}
```

## Memory

| Method               | Space Usage                            |
| -------------------- | -------------------------------------- |
| Separate Chaining    | ~48N + 64M                             |
| Linear Probing       | Between ~32N and ~128N                |
| BSTs                 | ~56N                                  |

- A good hash function for each type of key is required.
- The performance guarantee depends on the quality of the hash function.
- Hash functions can be difficult and expensive to compute.
- Ordered symbol-table operations are not easily supported.

---

# GRAPHS

**Pairwise Connections in Computational Applications**

Pairwise connections between items play a critical role in a vast array of computational applications. The relationships implied by these connections lead immediately to a host of natural questions:

- Is there a way to connect one item to another by following the connections?
- How many other items are connected to a given item?
- What is the shortest chain of connections between this item and this other item?

**Maps**

When planning a trip, individuals often need to answer questions such as:

- "What is the shortest route from Providence to Princeton?"
- A seasoned traveler, having experienced traffic delays on the shortest route, may ask: "What is the fastest way to get from Providence to Princeton?"

**Web Content

When we browse the web, we encounter pages that contain references (links) to other pages. The process involves moving from page to page by clicking on these links. The entire web can be conceptualized as a graph, where the items represent pages and the connections are links.

Graph-processing algorithms play a pivotal role in the functioning of search engines. These algorithms are essential components that enable us to locate information efficiently on the vast expanse of the web.

**Circuits**

`Is a short-circuit present?` 

**Schedules 

In a manufacturing process, various jobs need to be performed under a set of constraints. These constraints specify that certain tasks cannot commence until specific other tasks have been completed. The challenge lies in creating a schedule that not only respects these given constraints but also ensures the completion of the entire process in the least amount of time. The scheduling process aims to optimize the efficiency of the workflow within the defined constraints.

**Commerce

In commerce, both retailers and financial institutions diligently track buy/sell orders within the market. In this context, a connection signifies the transfer of cash and goods between an institution and a customer. This tracking mechanism is crucial for monitoring and managing the flow of transactions, ensuring transparency, and facilitating a smooth exchange of goods and financial assets.

**Matching**

In selective institutions like social clubs, universities, or medical schools, students go through an application process to secure positions. In this scenario, items correspond to both the students and the institutions, while connections represent the applications made by students to these institutions. The matching process becomes pivotal in determining the allocation of positions and creating mutually beneficial connections between students and the institutions they apply to.

**Computer Networks**

A computer network consists of interconnected sites that send, forward, and receive messages of various types.

**Software**

A compiler builds graphs to represent relationships among modules in a large software system. We need to analyze the graph to determine how best to allocate resources to the program most efficiently.

**Social Networks**

Items correspond to people; connections are to friends or followers. Understanding the properties of these networks is a modern graph-processing application of intense interest not just to companies that support such networks, but also in politics, diplomacy, entertainment, education, marketing, and many other domains.


| Application         | Item         | Connection       |
|---------------------|--------------|-------------------|
| Map                 | Intersection | Road              |
| Web Content         | Page         | Link              |
| Circuit             | Device       | Wire              |
| Schedule            | Job          | Constraint        |
| Commerce            | Customer     | Transaction       |
| Matching            | Student      | Application      |
| Computer Network    | Site         | Connection        |
| Software            | Method       | Call              |
| Social Network      | Person       | Friendship        |

## UNDIRECTED GRAPHS

Edges are nothing more than connections between vertices.

>**Definition**
  A graph is a set of vertices and a collection of edges (A) that each connect a pair of vertices.

Vertex names are not important to the definition, but we need a way to refer to vertices. By convention, we use the names 0 through V-1 for the vertices in a V-vertex graph.


**Anomalies**
- A self-loop is an edge that connects a vertex to itself.
- Two edges that connect the same pair of vertices are parallel.

### Glossary

When there is an edge connecting two vertices, we say that the vertices are adjacent to one another and that the edge is incident to both vertices. The degree of a vertex is the number of edges incident to it. A subgraph is a subset of a graph’s edges (and associated vertices) that constitutes a graph.

>**Definition**
>A path in a graph is a sequence of vertices connected by edges. A simple path is one with no repeated vertices. A cycle is a path with at least one edge whose first and last vertices are the same. A simple cycle is a cycle with no repeated edges or vertices (except the requisite repetition of the first and last vertices). The length of a path or a cycle is its number of edges.

>**Definition**
>A graph is connected if there is a path from every vertex to every other vertex in the graph. A graph that is not connected consists of a set of connected components, which are maximal connected subgraphs.

Intuitively If the vertices were physical objects, such as knots or beads, and the edges were physical connections, such as strings or wires, a connected graph would stay in one piece if picked up by any vertex, and a graph that is not connected comprises two or more such pieces. Generally, processing a graph necessitates processing the connected components one at a time.
An acyclic graph is a graph with no cycles.

> **Definition**
>A tree is an acyclic connected graph. A disjoint set of trees is called a forest. A spanning tree of a connected graph is a subgraph that contains all of that graph’s vertices and is a single tree. A spanning forest of a graph is the union of spanning trees of its connected components.


A graph G with V vertices is a tree if and only if it satisfies any of the following five conditions:

1. G has V-1 edges and no cycles.
2. G has V-1 edges and is connected.
3. G is connected, but removing any edge disconnects it.
4. G is acyclic, but adding any edge creates a cycle.
5. Exactly one simple path connects each pair of vertices in G.


The density of a graph is the proportion of possible pairs of vertices that are connected by edges.

### Undirected graph data type

```java
public class Graph {

    // Create a V-vertex graph with no edges
    public Graph(int V);

    // Read a graph from input stream in
    public Graph(In in);

    // Number of vertices
    public int V();

    // Number of edges
    public int E();

    // Add edge v-w to this graph
    public void addEdge(int v, int w);

    // Vertices adjacent to v
    public Iterable<Integer> adj(int v);

    // String representation
    public String toString();
}
```

| Task                                 | Implementation                                        |
|--------------------------------------|--------------------------------------------------------|
| Compute the degree of v              | ```java public static int degree(Graph G, int v) { int degree = 0; for (int w : G.adj(v)) degree++; return degree; } ``` |
| Compute maximum degree                | ```java public static int maxDegree(Graph G) { int max = 0; for (int v = 0; v < G.V(); v++) if (degree(G, v) > max) max = degree(G, v); return max; } ``` |
| Compute average degree                | ```java public static int avgDegree(Graph G) { return 2 * G.E() / G.V(); } ``` |
| Count self-loops                      | ```java public static int numberOfSelfLoops(Graph G) { int count = 0; for (int v = 0; v < G.V(); v++) for (int w : G.adj(v)) if (v == w) count++; return count/2; // each edge counted twice } ``` |
| String representation of the graph's adjacency lists | ```java public String toString() { String s = V + " vertices, " + E + " edges\n"; for (int v = 0; v < V; v++) { s += v + ": "; for (int w : this.adj(v)) s += w + " "; s += "\n"; } return s; } ``` |


**Representation Alternatives**

The next decision that we face in graph processing is which graph representation (data structure) to use to implement this API:

- We must have the space to accommodate the types of graphs that we are likely to encounter in applications.

- We want to develop time-efficient implementations of Graph instance methods—the basic methods that we need to develop graph-processing clients.


The three data structures that immediately suggest themselves for representing graphs:

1. **Adjacency Matrix:**
   - We maintain a V-by-V boolean array, with the entry in row v and column w defined to be true if there is an edge adjacent to both vertex v and vertex w in the graph, and to be false otherwise.
   - This representation fails on the first count—graphs with millions of vertices are common, and the space cost for the V^2 boolean values needed is prohibitive.

2. **Array of Edges:**
   - Using an Edge class with two instance variables of type int.
   - This direct representation is simple, but it fails on the second count—implementing `adj()` would involve examining all the edges in the graph.

3. **Array of Adjacency Lists:**
   - We maintain a vertex-indexed array of lists of the vertices adjacent to each vertex.

**Adjacency-Lists Data Structure**

In this data structure, we keep track of all the vertices adjacent to each vertex on a linked list that is associated with that vertex. We maintain an array of lists so that, given a vertex, we can immediately access its list.

This Graph implementation achieves the following performance characteristics:

- Space usage proportional to V + E
- Constant time to add an edge
- Time proportional to the degree of v to iterate through vertices adjacent to v

These characteristics are optimal for this set of operations, which suffice for the graph-processing applications that we consider. Parallel edges and self-loops are allowed (we do not check for them).

Note: It is important to realize that the order in which edges are added to the graph determines the order in which vertices appear in the array of adjacency lists built by Graph. Many different arrays of adjacency lists can represent the same graph.

```java
public class Graph {
    private final int V;           // number of vertices
    private int E;                 // number of edges
    private Bag<Integer>[] adj;    // adjacency lists

    public Graph(int V) {
        this.V = V;
        this.E = 0;
        adj = (Bag<Integer>[]) new Bag[V];   // Create array of lists.
        for (int v = 0; v < V; v++)          // Initialize all lists to empty.
            adj[v] = new Bag<Integer>();
    }

    public Graph(In in) {
        this(in.readInt());                 // Read V and construct this graph.
        int E = in.readInt();                // Read E.
        for (int i = 0; i < E; i++) {
            // Add an edge.
            int v = in.readInt();            // Read a vertex,
            int w = in.readInt();            // read another vertex,
            addEdge(v, w);                   // and add an edge connecting them.
        }
    }

    public int V() {
        return V;
    }

    public int E() {
        return E;
    }

    public void addEdge(int v, int w) {
        adj[v].add(w);                      // Add w to v’s list.
        adj[w].add(v);                      // Add v to w’s list.
        E++;
    }

    public Iterable<Integer> adj(int v) {
        return adj[v];
    }
}
```

It is certainly reasonable to contemplate other operations that might be useful in applications, and to consider methods for:

- Adding a vertex
- Deleting a vertex

One might also consider methods for:

- Deleting an edge
- Checking whether the graph contains the edge v-w

- Our clients do not need to add vertices, delete vertices and edges, or check whether an edge exists.
- When clients do need these operations, they typically are invoked infrequently or for short adjacency lists, so an easy option is to use a brute-force implementation that iterates through an adjacency list.
- The SET and ST representations slightly complicate algorithm implementation code, diverting attention from the algorithms themselves.
- A performance penalty of log V may be involved in some situations.



| Underlying Data Structure | Space | Add Edge v-w | Check Whether w is Adjacent to v | Iterate Through Vertices Adjacent to v |
|---------------------------|-------|--------------|------------------------------------|------------------------------------------|
| List of Edges             | E     | 1            | E                                  | E                                        |
| Adjacency Matrix          | V^2   | 1            | 1                                  | V^2                                      |
| Adjacency Lists           | E + V | 1            | Degree(v)                         | Degree(v)                                |
| Adjacency Sets            | E * log(V) | log(V) | log(V) * Degree(v)                | log(V) * Degree(v)                       |


**Design Pattern for Graph Processing**

The initial design goal is to decouple our implementations from the graph representation:

```java
public class Search {
    // Find vertices connected to a source vertex s
    public Search(Graph G, int s);

    // Is v connected to s?
    public boolean marked(int v);

    // How many vertices are connected to s?
    public int count();
}
```

```java
public class TestSearch {
    public static void main(String[] args) {
        Graph G = new Graph(new In(args[0]));
        int s = Integer.parseInt(args[1]);
        Search search = new Search(G, s);
        
        for (int v = 0; v < G.V(); v++) {
            if (search.marked(v)) {
                StdOut.print(v + " ");
            }
        }
        
        StdOut.println();
        
        if (search.count() != G.V()) {
            StdOut.print("NOT ");
        }
        
        StdOut.println("connected");
    }
}
```

### Depth-first search

**Searching in a Maze**

Finding our way through a maze that consists of passages connected by intersections. One trick for exploring a maze without getting lost that has been known since antiquity (dating back at least to the legend of Theseus and the Minotaur) is known as Tremaux exploration. To explore all passages in a maze:

- Take any unmarked passage, unrolling a string behind you.
- Mark all intersections and passages when you first visit them.
- Retrace steps (using the string) when approaching a marked intersection.
- Retrace steps when no unvisited options remain at an intersection encountered while retracing steps.

**Warmup**

To search a graph, invoke a recursive method that visits vertices. To visit a vertex:

- Mark it as having been visited.
- Visit (recursively) all the vertices that are adjacent to it and that have not yet been marked.

This method is called depth-first search (DFS).

```java
public class DepthFirstSearch {
    private boolean[] marked;
    private int count;

    public DepthFirstSearch(Graph G, int s) {
        marked = new boolean[G.V()];
        dfs(G, s);
    }

    private void dfs(Graph G, int v) {
        marked[v] = true;
        count++;

        for (int w : G.adj(v)) {
            if (!marked[w]) {
                dfs(G, w);
            }
        }
    }

    public boolean marked(int w) {
        return marked[w];
    }

    public int count() {
        return count;
    }
}
```

**One-way Passages**

The method call-return mechanism in the program corresponds to the string in the maze: when we have processed all the edges incident to a vertex (explored all the passages leaving an intersection), we "return" (in both senses of the word).

**Depth-First Search (DFS)**

This basic recursive scheme is just a start—depth-first search is effective for many graph-processing tasks.

**Connectivity**

Given a graph, support queries of the form "Are two given vertices connected?" and "How many connected components does the graph have?" This problem is easily solved within our standard graph-processing design pattern.

DFS is deceptively simple because it is based on a familiar concept and is so easy to implement; in fact, it is a subtle and powerful algorithm that researchers have learned to put to use to solve numerous difficult problems. These two are the first of several that we will consider.


### Finding Paths

```java
public class Paths {
    // Find paths in G from source s
    public Paths(Graph G, int s);

    // Is there a path from s to v?
    public boolean hasPathTo(int v);

    // Path from s to v; null if no such path
    public Iterable<Integer> pathTo(int v);
}
```

```java
public static void main(String[] args) {
    Graph G = new Graph(new In(args[0]));
    int s = Integer.parseInt(args[1]);
    Paths search = new Paths(G, s);
    
    for (int v = 0; v < G.V(); v++) {
        StdOut.print(s + " to " + v + ": ");
        if (search.hasPathTo(v)) {
            for (int x : search.pathTo(v)) {
                if (x == s) {
                    StdOut.print(x);
                } else {
                    StdOut.print("-" + x);
                }
            }
        }
        StdOut.println();
    }
}
```

**Implementation**

```java
public static void main(String[] args) {
    Graph G = new Graph(new In(args[0]));
    int s = Integer.parseInt(args[1]);
    Paths search = new Paths(G, s);
    
    for (int v = 0; v < G.V(); v++) {
        StdOut.print(s + " to " + v + ": ");
        if (search.hasPathTo(v)) {
            for (int x : search.pathTo(v)) {
                if (x == s) {
                    StdOut.print(x);
                } else {
                    StdOut.print("-" + x);
                }
            }
        }
        StdOut.println();
    }
}
```

### Breadth-first search

**Single-Source Shortest Paths**

Given a graph and a source vertex s, support queries of the form "Is there a path from s to a given target vertex v?" If so, find a shortest such path (one with a minimal number of edges).

The classical method for accomplishing this task, called breadth-first search (BFS),

To find a shortest path from s to v, we start at s and check for v among all the vertices that we can reach by following one edge, then we check for v among all the vertices that we can reach from s by following two edges, and so forth. DFS is analogous to one person exploring a maze. BFS is analogous to a group of searchers exploring by fanning out in all directions, each unrolling his or her own ball of string. When more than one passage needs to be explored, we imagine that the searchers split up to explore all of them; when two groups of searchers meet up, they join forces (using the ball of string held by the one getting there first).


**Implementation**

```java
public class BreadthFirstPaths {
    private boolean[] marked;    // Is a shortest path to this vertex known?
    private int[] edgeTo;         // Last vertex on known path to this vertex
    private final int s;          // Source
    
    public BreadthFirstPaths(Graph G, int s) {
        marked = new boolean[G.V()];
        edgeTo = new int[G.V()];
        this.s = s;
        bfs(G, s);
    }

    private void bfs(Graph G, int s) {
        Queue<Integer> queue = new Queue<Integer>();
        marked[s] = true;           // Mark the source
        queue.enqueue(s);           // and put it on the queue.

        while (!queue.isEmpty()) {
            int v = queue.dequeue(); // Remove the next vertex from the queue.
            
            for (int w : G.adj(v)) {
                if (!marked[w]) {   // For every unmarked adjacent vertex,
                    edgeTo[w] = v;   // save the last edge on a shortest path,
                    marked[w] = true; // mark it because the path is known,
                    queue.enqueue(w); // and add it to the queue.
                }
            }
        }
    }

    public boolean hasPathTo(int v) {
        return marked[v];
    }

    public Iterable<Integer> pathTo(int v) {
        // Same as for DFS (see page 536).
    }
}
```

**Differences Between BFS and DFS**

The algorithms (BFS and DFS) differ only in the rule used to take the next vertex from the data structure (least recently added for BFS, most recently added for DFS). This difference leads to completely different views of the graph, even though all the vertices and edges connected to the source are examined no matter what rule is used.


### Connected Components

```java
public class CC {
    // Preprocessing constructor
    public CC(Graph G);

    // Are v and w connected?
    public boolean connected(int v, int w);

    // Number of connected components
    public int count();

    // Component identifier for v (between 0 and count()-1)
    public int id(int v);
}
```

```java
public static void main(String[] args) {
    Graph G = new Graph(new In(args[0]));
    CC cc = new CC(G);
    int M = cc.count();
    StdOut.println(M + " components");
    Bag<Integer>[] components;
    components = (Bag<Integer>[]) new Bag[M];

    for (int i = 0; i < M; i++) {
        components[i] = new Bag<Integer>();
    }

    for (int v = 0; v < G.V(); v++) {
        components[cc.id(v)].add(v);
    }

    for (int i = 0; i < M; i++) {
        for (int v : components[i]) {
            StdOut.print(v + " ");
        }
        StdOut.println();
    }
}
```

**Implementation**

```java
public class CC {
    private boolean[] marked;
    private int[] id;
    private int count;

    public CC(Graph G) {
        marked = new boolean[G.V()];
        id = new int[G.V()];
        count = 0;

        for (int s = 0; s < G.V(); s++) {
            if (!marked[s]) {
                dfs(G, s);
                count++;
            }
        }
    }

    private void dfs(Graph G, int v) {
        marked[v] = true;
        id[v] = count;

        for (int w : G.adj(v)) {
            if (!marked[w]) {
                dfs(G, w);
            }
        }
    }

    public boolean connected(int v, int w) {
        return id[v] == id[w];
    }

    public int id(int v) {
        return id[v];
    }

    public int count() {
        return count;
    }
}
```

### Symbol graphs


Typical applications involve processing graphs defined in files or on web pages, using strings, not integer indices, to define and refer to vertices. To accommodate such applications, we define an input format with the following properties:

- Vertex names are strings.
- A specified delimiter separates vertex names (to allow for the possibility of spaces in names).
- Each line represents a set of edges, connecting the first vertex name on the line to each of the other vertices named on the line.
- The number of vertices V and the number of edges E are both implicitly defined.

```java
public class SymbolGraph {
    // Build graph specified in filename using delim to separate vertex names
    public SymbolGraph(String filename, String delim);

    // Is key a vertex?
    public boolean contains(String key);

    // Index associated with key
    public int index(String key);

    // Key associated with index v
    public String name(int v);

    // Underlying Graph
    public Graph G();
}
```

```java
public static void main(String[] args) {
    String filename = args[0];
    String delim = args[1];
    SymbolGraph sg = new SymbolGraph(filename, delim);
    Graph G = sg.G();

    while (StdIn.hasNextLine()) {
        String source = StdIn.readLine();
        
        for (int w : G.adj(sg.index(source))) {
            StdOut.println(" " + sg.name(w));
        }
    }
}
```

**Implementation**

A full `SymbolGraph` implementation is given on page 552. It builds three data structures:

- A symbol table `st` with String keys (vertex names) and int values (indices)
- An array `keys[]` that serves as an inverted index, giving the vertex name associated with each integer index
- A `Graph G` built using the indices to refer to vertices

```java
public class SymbolGraph {
    private ST<String, Integer> st; // String -> index
    private String[] keys; // index -> String
    private Graph G; // the graph

    public SymbolGraph(String stream, String sp) {
        st = new ST<String, Integer>();
        In in = new In(stream); // First pass
        while (in.hasNextLine()) // builds the index
        {
            String[] a = in.readLine().split(sp); // by reading strings
            for (int i = 0; i < a.length; i++) // to associate each
                if (!st.contains(a[i])) // distinct string
                    st.put(a[i], st.size()); // with an index.
        }
        keys = new String[st.size()]; // Inverted index
        for (String name : st.keys()) // to get string keys
            keys[st.get(name)] = name; // is an array.
        G = new Graph(st.size());
        in = new In(stream); // Second pass
        while (in.hasNextLine()) // builds the graph
        {
            String[] a = in.readLine().split(sp); // by connecting the
            int v = st.get(a[0]); // first vertex
            for (int i = 1; i < a.length; i++) // on each line
                G.addEdge(v, st.get(a[i])); // to all the others.
        }
    }

    public boolean contains(String s) {
        return st.contains(s);
    }

    public int index(String s) {
        return st.get(s);
    }

    public String name(int v) {
        return keys[v];
    }

    public Graph G() {
        return G;
    }
}
```

**Degrees of Separation**

One of the classic applications of graph processing is to find the degree of separation between two individuals in a social network. This program takes a source vertex from the command line, then takes queries from standard input and prints a shortest path from the source to the query vertex. Since the graph associated with movies.txt is bipartite, all paths alternate between movies and performers, and the printed path is a "proof" that the path is valid.

The `DegreesOfSeparation` program is versatile and not limited to bipartite graphs. It can find shortest paths in graphs that are not bipartite. For example, it can discover the most efficient way to travel from one airport to another using the fewest connections in a graph defined by routes.txt.

```java
public class DegreesOfSeparation {
    public static void main(String[] args) {
        SymbolGraph sg = new SymbolGraph(args[0], args[1]);
        Graph G = sg.G();
        String source = args[2];
        if (!sg.contains(source)) {
            StdOut.println(source + " not in database.");
            return;
        }
        int s = sg.index(source);
        BreadthFirstPaths bfs = new BreadthFirstPaths(G, s);
        while (!StdIn.isEmpty()) {
            String sink = StdIn.readLine();
            if (sg.contains(sink)) {
                int t = sg.index(sink);
                if (bfs.hasPathTo(t))
                    for (int v : bfs.pathTo(t))
                        StdOut.println(" " + sg.name(v));
                else
                    StdOut.println("Not connected");
            } else
                StdOut.println("Not in database.");
        }
    }
}
```

### Summary

- **Graph Nomenclature:** Understanding the terminology used in graph theory.
- **Sparse Graphs Processing:** Developing graph representations suitable for efficiently processing huge, sparse graphs.
- **Design Pattern for Graph Processing:** Implementing algorithms using a design pattern where the graph is preprocessed in the constructor, creating data structures to support efficient client queries about the graph.
- **Depth-First Search (DFS) and Breadth-First Search (BFS):** Two fundamental graph traversal algorithms with different approaches.
- **Symbolic Vertex Names:** Using a class to facilitate the use of symbolic vertex names, providing more intuitive representations for vertices in a graph.

**Problem Solutions and References**

- **Single-Source Connectivity:** Solution using Depth-First Search (DFS). Reference: Page 531.
- **Single-Source Paths:** Solution using Depth-First Paths. Reference: Page 536.
- **Single-Source Shortest Paths:** Solution using Breadth-First Paths. Reference: Page 540.
- **Connectivity:** Solution using Connected Components (CC). Reference: Page 544.
- **Cycle Detection:** Solution using Cycle detection algorithm. Reference: Page 547.
- **Two-Colorability (Bipartiteness):** Solution using TwoColor algorithm. Reference: Page 547.

*Note: The following (Undirected) graph-processing problems are addressed in this section without specific references.*


## DIRECTED GRAPHS

In directed graphs, edges are one-way: the pair of vertices that defines each edge is an ordered pair that specifies a one-way adjacency


The one-way restriction in directed graphs is a natural constraint, easily enforceable in our implementations, and may appear innocuous. However, it introduces additional combinatorial structure that significantly impacts our algorithms and fundamentally differentiates working with directed graphs from working with undirected graphs.

| Application           | Vertex         | Edge                |
|-----------------------|----------------|---------------------|
| Food Web              | Species        | Predator-Prey       |
| Internet              | Page           | Hyperlink           |
| Program               | Module         | External Reference  |
| Cellphone            | Phone Call     | -                   |
| Scholarship           | Paper          | Citation            |
| Financial            | Stock          | Transaction         |
| Internet              | Machine        | Connection          |

### Glossary

>**Definition**
>A directed graph (or digraph) is a mathematical structure consisting of a set of vertices and a collection of directed edges. Each directed edge connects an ordered pair of vertices.


A directed edge points from the first vertex in the pair and points to the second vertex in the pair. The outdegree of a vertex in a digraph is the number of edges going from it, while the indegree of a vertex is the number of edges going to it.


> **Definition**
>A directed path in a digraph is a sequence of vertices in which there is a (directed) edge pointing from each vertex in the sequence to its successor in the sequence. A directed cycle is a directed path with at least one edge whose first and last vertices are the same. A simple cycle is a cycle with no repeated edges or vertices (except the requisite repetition of the first and last vertices). The length of a path or a cycle is its number of edges.


### Digraph data type

### Digraph API

### Class: Digraph

- **Constructor:** `Digraph(int V)` - Create a digraph with V vertices and no edges.
- **Constructor:** `Digraph(In in)` - Read a digraph from the input stream.
- **Method:** `int V()` - Get the number of vertices in the digraph.
- **Method:** `int E()` - Get the number of edges in the digraph.
- **Method:** `void addEdge(int v, int w)` - Add a directed edge v->w to the digraph.
- **Method:** `Iterable<Integer> adj(int v)` - Get vertices connected to v by edges pointing from v.
- **Method:** `Digraph reverse()` - Get the reverse of this digraph.
- **Method:** `String toString()` - Get the string representation of the digraph.

This API provides functionality for creating, reading, and manipulating directed graphs (digraphs).

**Digraph Representation**

We represent the digraph using an adjacency-lists representation, where each vertex maintains a linked list of its adjacent vertices. In this representation, an edge v->w is represented by adding w to the linked list associated with vertex v.

**Input Format**

The input format remains the same, but all edges are interpreted as directed edges. In the list-of-edges format, a pair v w is interpreted as a directed edge from vertex v to vertex w (v->w).

**Reversing a Digraph**

Reversing a digraph allows clients to find the edges that point to each vertex, while the `adj()` method gives just vertices connected by edges that point from each vertex.


**Digraph Implementation**

```java
public class Digraph
{
    private final int V;
    private int E;
    private Bag<Integer>[] adj;

    public Digraph(int V)
    {
        this.V = V;
        this.E = 0;
        adj = (Bag<Integer>[]) new Bag[V];
        for (int v = 0; v < V; v++)
            adj[v] = new Bag<Integer>();
    }

    public int V() { return V; }
    public int E() { return E; }

    public void addEdge(int v, int w)
    {
        adj[v].add(w);
        E++;
    }

    public Iterable<Integer> adj(int v)
    {
        return adj[v];
    }

    public Digraph reverse()
    {
        Digraph R = new Digraph(V);
        for (int v = 0; v < V; v++)
            for (int w : adj(v))
                R.addEdge(w, v);
        return R;
    }
}
```

### Reachability in digraphs

**DirectedDFS Implementation**

```java
public class DirectedDFS
{
    private boolean[] marked;

    public DirectedDFS(Digraph G, int s)
    {
        marked = new boolean[G.V()];
        dfs(G, s);
    }

    public DirectedDFS(Digraph G, Iterable<Integer> sources)
    {
        marked = new boolean[G.V()];
        for (int s : sources)
            if (!marked[s])
                dfs(G, s);
    }

    private void dfs(Digraph G, int v)
    {
        marked[v] = true;
        for (int w : G.adj(v))
            if (!marked[w])
                dfs(G, w);
    }

    public boolean marked(int v)
    {
        return marked[v];
    }
}
```

> Multiple-source reachability. Given a digraph and a set of source vertices, support queries of the form Is there a directed path from any vertex in the set to a given target vertex v?


```java
public class DirectedDFS
{
    private boolean[] marked;

    public DirectedDFS(Digraph G, int s)
    {
        marked = new boolean[G.V()];
        dfs(G, s);
    }

    public DirectedDFS(Digraph G, Iterable<Integer> sources)
    {
        marked = new boolean[G.V()];
        for (int s : sources)
            if (!marked[s]) dfs(G, s);
    }

    private void dfs(Digraph G, int v)
    {
        marked[v] = true;
        for (int w : G.adj(v))
            if (!marked[w]) dfs(G, w);
    }

    public boolean marked(int v)
    {
        return marked[v];
    }

    public static void main(String[] args)
    {
        Digraph G = new Digraph(new In(args[0]));
        Bag<Integer> sources = new Bag<Integer>();
        for (int i = 1; i < args.length; i++)
            sources.add(Integer.parseInt(args[i]));

        DirectedDFS reachable = new DirectedDFS(G, sources);

        for (int v = 0; v < G.V(); v++)
            if (reachable.marked(v)) StdOut.print(v + " ");
        StdOut.println();
    }
}
```

**Mark-and-sweep garbage collection.** 

An important application of multiple-source reachability is found in typical memory-management systems. At any point in the execution of a program, certain objects are known to be directly accessible, and any object not reachable from that set of objects can be returned to available memory. A mark-and-sweep garbage collection strategy reserves one bit per object for the purpose of garbage collection, then periodically marks the set of potentially accessible objects by running a digraph reachability algorithm like `DirectedDFS` and sweeps through all objects, collecting the unmarked ones for use for new objects.

### Cycles and DAGs

**Identifying directed cycles in a typical digraph** can be a challenge without the help of a computer. In principle, a digraph might have a huge number of cycles; in practice, we typically focus on a small number of them, or simply are interested in knowing that none are present.

**Scheduling problems.**

A widely applicable problem-solving model has to do with arranging for the completion of a set of jobs, under a set of constraints, by specifying when and how the jobs are to be performed. The most important type of constraints is precedence constraints, which specify that certain tasks must be performed before certain others.

**Precedence-constrained scheduling.**

Given a set of jobs to be completed, with precedence constraints that specify that certain jobs have to be completed before certain other jobs are begun, how can we schedule the jobs such that they are all completed while still respecting the constraints? For any such problem, a digraph model is immediate, with vertices corresponding to jobs and directed edges corresponding to precedence constraints.

> **Topological sort.** 
> Given a digraph, put the vertices in order such that all its directed edges point from a vertex earlier in the order to a vertex later in the order.

|Application|Vertex|Edge|
|---|---|---|
|Job Schedule|Job|Job Precedence Constraint|
|Course Schedule|Course|Course Prerequisite|
|Inheritance in Java|Java Class|Extends Relationship|
|Spreadsheet|Cell|Formula|
|Symbolic Links|File Name|Link|

**Cycles in Digraphs:**
If job x must be completed before job y, job y before job z, and job z before job x, then someone has made a mistake, because those three constraints cannot all be satisfied. In general, if a precedence-constrained scheduling problem has a directed cycle, then there is no feasible solution.

**Directed Cycle Detection:**
Does a given digraph have a directed cycle? If so, find the vertices on some such cycle, in order from some vertex back to itself.

>**Definition:**
>A directed acyclic graph (DAG) is a digraph with no directed cycles.

```java
public class DirectedCycle
{
    // Cycle-finding constructor
    public DirectedCycle(Digraph G) { /* implementation */ }

    // Does G have a directed cycle?
    public boolean hasCycle() { /* implementation */ }

    // Vertices on a cycle (if one exists)
    public Iterable<Integer> cycle() { /* implementation */ }
}
```

```java
public class DirectedCycle
{
    private boolean[] marked;
    private int[] edgeTo;
    private Stack<Integer> cycle; // vertices on a cycle (if one exists)
    private boolean[] onStack; // vertices on recursive call stack

    public DirectedCycle(Digraph G)
    {
        onStack = new boolean[G.V()];
        edgeTo = new int[G.V()];
        marked = new boolean[G.V()];
        for (int v = 0; v < G.V(); v++)
            if (!marked[v])
                dfs(G, v);
    }

    private void dfs(Digraph G, int v)
    {
        onStack[v] = true;
        marked[v] = true;
        for (int w : G.adj(v))
            if (this.hasCycle())
                return;
            else if (!marked[w])
            {
                edgeTo[w] = v;
                dfs(G, w);
            }
            else if (onStack[w])
            {
                cycle = new Stack<Integer>();
                for (int x = v; x != w; x = edgeTo[x])
                    cycle.push(x);
                cycle.push(w);
                cycle.push(v);
            }
        onStack[v] = false;
    }

    public boolean hasCycle()
    {
        return cycle != null;
    }

    public Iterable<Integer> cycle()
    {
        return cycle;
    }
}
```

**Depth-first orders and topological sort**
```java
public class Topological
{
    // Constructor for topological sorting
    public Topological(Digraph G)
    
    // Check if the graph is a Directed Acyclic Graph (DAG)
    public boolean isDAG()
    
    // Get the vertices in topological order
    public Iterable<Integer> order()
}

```

Three vertex orderings are of interest in typical applications:
- Preorder: Put the vertex on a queue before the recursive calls.
- Postorder: Put the vertex on a queue after the recursive calls.
- Reverse postorder: Put the vertex on a stack after the recursive calls.


```java
// DepthFirstOrder class
public class DepthFirstOrder
{
    private boolean[] marked;
    private Queue<Integer> pre;           // vertices in preorder
    private Queue<Integer> post;          // vertices in postorder
    private Stack<Integer> reversePost;   // vertices in reverse postorder
    
    public DepthFirstOrder(Digraph G)
    {
        pre = new Queue<Integer>();
        post = new Queue<Integer>();
        reversePost = new Stack<Integer>();
        marked = new boolean[G.V()];
        
        for (int v = 0; v < G.V(); v++)
            if (!marked[v]) dfs(G, v);
    }
    
    private void dfs(Digraph G, int v)
    {
        pre.enqueue(v);
        marked[v] = true;
        
        for (int w : G.adj(v))
            if (!marked[w])
                dfs(G, w);
        
        post.enqueue(v);
        reversePost.push(v);
    }
    
    public Iterable<Integer> pre()
    { return pre; }
    
    public Iterable<Integer> post()
    { return post; }
    
    public Iterable<Integer> reversePost()
    { return reversePost; }
}

// Topological class
public class Topological
{
    private Iterable<Integer> order;   // topological order
    
    public Topological(Digraph G)
    {
        DirectedCycle cyclefinder = new DirectedCycle(G);
        
        if (!cyclefinder.hasCycle())
        {
            DepthFirstOrder dfs = new DepthFirstOrder(G);
            order = dfs.reversePost();
        }
    }
    
    public Iterable<Integer> order()
    { return order; }
    
    public boolean isDAG()
    { return order == null; }
    
    public static void main(String[] args)
    {
        String filename = args[0];
        String separator = args[1];
        SymbolDigraph sg = new SymbolDigraph(filename, separator);
        Topological top = new Topological(sg.G());
        
        for (int v : top.order())
            StdOut.println(sg.name(v));
    }
}
```

In practice, topological sorting and cycle detection go hand in hand, with cycle detection playing the role of a debugging tool.

Thus, a job-scheduling application is typically a three-step process:

1. Specify the tasks and precedence constraints.
2. Make sure that a feasible solution exists by detecting and removing cycles in the underlying digraph until none exist.
3. Solve the scheduling problem using topological sort.

Similarly, any changes in the schedule can be checked for cycles using `DirectedCycle`, then a new schedule can be computed.

### Strong connectivity in digraphs

In an undirected graph, two vertices \(v\) and \(w\) are connected if there is a path connecting them—we can use that path to get from \(v\) to \(w\) or to get from \(w\) to \(v\). In a digraph, by contrast, a vertex \(w\) is reachable from a vertex \(v\) if there is a directed path from \(v\) to \(w\), but there may or may not be a directed path back to \(v\) from \(w\).

>**Definition**. 
>Two vertices \(v\) and \(w\) are strongly connected if they are mutually reachable: that is, if there is a directed path from \(v\) to \(w\) and a directed path from \(w\) to \(v\). A digraph is strongly connected if all its vertices are strongly connected to one another.

**Strong components.** Like connectivity in undirected graphs, strong connectivity in digraphs is an equivalence relation on the set of vertices, as it has the following properties:
- *Reflexive*: Every vertex \(v\) is strongly connected to itself.
- *Symmetric*: If \(v\) is strongly connected to \(w\), then \(w\) is strongly connected to \(v\).
- *Transitive*: If \(v\) is strongly connected to \(w\) and \(w\) is strongly connected to \(x\), then \(v\) is also strongly connected to \(x\). 

The equivalence classes are maximal subsets of vertices that are strongly connected to one another, with each vertex in exactly one subset.

**Examples of applications**

| Application            | Vertex-Edge            |
|------------------------|------------------------|
| Web Page               | Hyperlink              |
| Textbook               | Topic Reference        |
| Software               | Module Call            |
| Food Web               | Organism Predator-Prey |
| Relationship           |                        |
| Typical Strong-Component Applications | Markdown Table |


### SCC Class

**Constructor:**
```java
public class SCC {
    // Preprocessing constructor for finding strong components in a directed graph.
    public SCC(Digraph G) {
        // Implementation for preprocessing
    }


	// Checks if two vertices, v and w, are strongly connected.
	public boolean stronglyConnected(int v, int w) {
		// Implementation for checking strong connectivity
	}
	
	// Returns the number of strong components in the graph.
	public int count() {
		// Implementation for counting strong components
	}
	
	// Returns the component identifier for a given vertex (between 0 and count()-1).
	public int id(int v) {
		// Implementation for getting component identifier
	}
}
```

 **Kosaraju's Algorithm for Strong Components**

To efficiently compute strong components in a directed graph (digraph):

1. **Compute Reverse Postorder:**
   - Given a digraph G, use `DepthFirstOrder` to compute the reverse postorder of its reverse, G<sup>R</sup>.

2. **Run Standard DFS:**
   - Run standard Depth-First Search (DFS) on G, but consider the unmarked vertices in the order just computed (reverse postorder of G<sup>R</sup>) instead of the standard numerical order.

3. **Identify Strong Components:**
   - All vertices reached on a call to the recursive `dfs()` from the constructor are in a strong component.
   - Identify these vertices as you would in a Connected Components (CC) algorithm.



 
```java
### KosarajuSCC Class

```java
public class KosarajuSCC {
    private boolean[] marked; // reached vertices
    private int[] id; // component identifiers
    private int count; // number of strong components

    public KosarajuSCC(Digraph G) {
        marked = new boolean[G.V()];
        id = new int[G.V()];
        DepthFirstOrder order = new DepthFirstOrder(G.reverse());

        for (int s : order.reversePost())
            if (!marked[s]) {
                dfs(G, s);
                count++;
            }
    }

    private void dfs(Digraph G, int v) {
        marked[v] = true;
        id[v] = count;
        for (int w : G.adj(v))
            if (!marked[w])
                dfs(G, w);
    }

    public boolean stronglyConnected(int v, int w) {
        return id[v] == id[w];
    }

    public int id(int v) {
        return id[v];
    }

    public int count() {
        return count;
    }
}
```

**Reachability Revisited - All-Pairs Reachability**

In the context of a directed graph (digraph), the goal is to support queries of the form "Is there a directed path from a given vertex v to another given vertex w?"

>**Definition**
>The **transitive closure** of a digraph G is another digraph with the same set of vertices. In this closure, there is an edge from vertex v to vertex w if and only if w is reachable from v in G.

```java
public class TransitiveClosure {
    /**
     * Preprocessing constructor for computing the transitive closure of a digraph.
     *
     * @param G The directed graph for which the transitive closure is computed.
     */
    public TransitiveClosure(Digraph G) {
        // Implementation for preprocessing
    }

    /**
     * Checks if vertex w is reachable from vertex v in the transitive closure.
     *
     * @param v The starting vertex.
     * @param w The destination vertex.
     * @return true if w is reachable from v, false otherwise.
     */
    public boolean reachable(int v, int w) {
        // Implementation for checking reachability
        // Return true if there is a directed path from v to w in the transitive closure
    }

    /**
     * API for all-pairs reachability.
     * Example usage: transitiveClosure.reachablePairs();
     */
    public void reachablePairs() {
        // Implementation for iterating through all pairs of vertices
        // Print or store reachability information for all vertex pairs
    }
}
```

### Summary

- **Digraph Nomenclature**
- **Representation and Approach**
  - Essentially the same as for undirected graphs, with some problems being more complicated.
- **Digraph Problems**
  - Cycles, DAGs, Topological Sort, and Precedence-Constrained Scheduling.
  - Reachability, Paths, and Strong Connectivity in digraphs.


 **Problem Solutions**

| Problem                                           | Solution                        |
|---------------------------------------------------|----------------------------------|
| Single- and Multiple-Source Reachability          | DirectedDFS                     |
| Single-Source Directed Paths                      | DepthFirstDirectedPaths         |
| Single-Source Shortest Directed Paths             | BreadthFirstDirectedPaths       |
| Directed Cycle Detection                          | DirectedCycle                   |
| Depth-First Vertex Orders                         | DepthFirstOrder                 |
| Precedence-Constrained Scheduling and Topological Sort | Topological                |
| Strong Connectivity                               | KosarajuSCC                     |
| All-Pairs Reachability                            | TransitiveClosure               |


## MINIMUM SPANNING TREES

>**Definition**
>Recall that a spanning tree of a graph is a connected subgraph with no cycles that includes all the vertices. A minimum spanning tree (MST) of an edge-weighted graph is a spanning tree whose weight (the sum of the weights of its edges) is no larger than the weight of any other spanning tree.

**Assumptions**

- The graph is connected
- The edge weights are not necessarily distances
- The edge weights may be zero or negative
- The edge weights are all different.

### Underlying principles

- **Adding an Edge in a Tree:**
- **Removing an Edge from a Tree:**

>**Definition: Cut in a Graph**
>A cut of a graph is a partition of its vertices into two nonempty disjoint sets. A crossing edge of a cut is an edge that connects a vertex in one set with a vertex in the other.

### Edge-weighted graph data type

```java
public class Edge implements Comparable<Edge> {

    // Initializing constructor
    public Edge(int v, int w, double weight) {
        // Implementation
    }

    // Returns the weight of this edge
    public double weight() {
        // Implementation
    }

    // Returns either of this edge’s vertices
    public int either() {
        // Implementation
    }

    // Returns the other vertex given one vertex
    public int other(int v) {
        // Implementation
    }

    // Compares this edge to another edge
    @Override
    public int compareTo(Edge that) {
        // Implementation
    }

    // Returns the string representation of this edge
    @Override
    public String toString() {
        // Implementation
    }
}
```

```java
public class EdgeWeightedGraph {

    // Constructors
    public EdgeWeightedGraph(int V) {
        // Creates an empty V-vertex graph
        // Implementation
    }

    public EdgeWeightedGraph(In in) {
        // Reads the graph from the input stream
        // Implementation
    }

    // Methods
    public int V() {
        // Returns the number of vertices
        // Implementation
    }

    public int E() {
        // Returns the number of edges
        // Implementation
    }

    public void addEdge(Edge e) {
        // Adds edge e to this graph
        // Implementation
    }

    public Iterable<Edge> adj(int v) {
        // Returns edges incident to vertex v
        // Implementation
    }

    public Iterable<Edge> edges() {
        // Returns all edges of this graph
        // Implementation
    }

    // Other Method
    @Override
    public String toString() {
        // Returns the string representation of this graph
        // Implementation
    }
}
```

**Weighted edge data type**
```java
public class Edge implements Comparable<Edge> {

    private final int v; // one vertex
    private final int w; // the other vertex
    private final double weight; // edge weight

    public Edge(int v, int w, double weight) {
        this.v = v;
        this.w = w;
        this.weight = weight;
    }

    public double weight() {
        return weight;
    }

    public int either() {
        return v;
    }

    public int other(int vertex) {
        if (vertex == v) return w;
        else if (vertex == w) return v;
        else throw new RuntimeException("Inconsistent edge");
    }

    @Override
    public int compareTo(Edge that) {
        if (this.weight() < that.weight()) return -1;
        else if (this.weight() > that.weight()) return +1;
        else return 0;
    }

    @Override
    public String toString() {
        return String.format("%d-%d %.2f", v, w, weight);
    }
}

```


**Edge-weighted graph data type**

```java
public class EdgeWeightedGraph
{
private final int V; // number of vertices
private int E; // number of edges
private Bag<Edge>[] adj; // adjacency lists
public EdgeWeightedGraph(int V)
{
this.V = V;
this.E = 0;
adj = (Bag<Edge>[]) new Bag[V];
for (int v = 0; v < V; v++)
adj[v] = new Bag<Edge>();
}
public EdgeWeightedGraph(In in)
// See Exercise 4.3.9.
public int V() { return V; }
public int E() { return E; }
public void addEdge(Edge e)
{
int v = e.either(), w = e.other(v);
adj[v].add(e);
adj[w].add(e);
E++;
}
public Iterable<Edge> adj(int v)
{ return adj[v]; }
public Iterable<Edge> edges()
// See page 609.
```

**Comparing edges by weight.**

The natural ordering for edges in an edge-weighted graph is by weight.

**Parallel edges**

As with our undirected-graph implementations, we allow parallel edges.

**Self-loops**

We allow self-loops. However, our edges() implementation in `EdgeWeightedGraph` does not include self-loops even though they might be present in the input or in the data structure.

### MST API and test client

The Minimum Spanning Tree (MST) of a graph G can be represented in various forms, including:

- A list of edges
- An edge-weighted graph
- A vertex-indexed array with parent links

## `MST` Class

| **Constructor**              | `public MST(EdgeWeightedGraph G)`             |
| ---------------------------- | -------------------------------------------- |
| **Methods**                  |                                            |
| `Iterable<Edge> edges()`      | Returns all of the MST edges.                |
| `double weight()`            | Returns the weight of the MST.               |

### API for MST Implementations

| **Constructor**              | `MST(EdgeWeightedGraph G)`                    |
| ---------------------------- | -------------------------------------------- |
| **Methods**                  |                                            |
| `Iterable<Edge> edges()`      | Returns all of the MST edges.                |
| `double weight()`            | Returns the weight of the MST.               |


### Prim’s algorithm


The core idea behind Prim's algorithm is to attach a new edge to a single growing tree at each step. The algorithm follows these steps:

1. **Initialization:**
   - Start with any vertex as a single-vertex tree.

2. **Growing the Tree:**
   - Add V-1 edges to it, always selecting the next minimum-weight edge that connects a vertex on the tree to a vertex not yet on the tree.


The one-sentence description of Prim’s algorithm leaves unanswered a key question: How do we efficiently find the crossing edge of minimal weight?

**Data structure**

 - **Vertices on the Tree:**
    
    - We use a boolean array called `marked[]`. If `marked[v]` is true, it means vertex `v` is on the tree.
- **Edges on the Tree:**
    
    - We use either a queue named `mst` or an array `edgeTo[]` of `Edge` objects. If it's an array, `edgeTo[v]` represents the `Edge` connecting vertex `v` to the tree.
- **Crossing Edges:**
    
    - For comparing edges by weight, we employ a priority queue named `MinPQ<Edge>`.

**Maintaining the set of crossing edges**

Each time that we add an edge to the tree, we also add a vertex to the tree. To maintain the set of crossing edges, we need to add to the priority queue all edges from that vertex to any non-tree vertex (using `marked[]` to identify such edges). But we must do more: any edge connecting the vertex just added to a tree vertex that is already on the priority queue now becomes ineligible.

**Implementation**

```java
public class LazyPrimMST
{
private boolean[] marked; // MST vertices
private Queue<Edge> mst; // MST edges
private MinPQ<Edge> pq; // crossing (and ineligible) edges
public LazyPrimMST(EdgeWeightedGraph G)
{
pq = new MinPQ<Edge>();
marked = new boolean[G.V()];
mst = new Queue<Edge>();
visit(G, 0); // assumes G is connected (see Exercise 4.3.22)
while (!pq.isEmpty())
{
Edge e = pq.delMin(); // Get lowest-weight
int v = e.either(), w = e.other(v); // edge from pq.
if (marked[v] && marked[w]) continue; // Skip if ineligible.
mst.enqueue(e); // Add edge to tree.
if (!marked[v]) visit(G, v); // Add vertex to tree
if (!marked[w]) visit(G, w); // (either v or w).
}
}
private void visit(EdgeWeightedGraph G, int v)
{ // Mark v and add to pq all edges from v to unmarked vertices.
marked[v] = true;
for (Edge e : G.adj(v))
if (!marked[e.other(v)]) pq.insert(e);
}
public Iterable<Edge> edges()
{ return mst; }
public double weight() // See Exercise 4.3.31.
```

### Eager version of Prim’s algorithm


The key is to note that our only interest is in the minimal edge from each non-tree vertex to a tree vertex. When we add a vertex v to the tree, the only possible change with respect to each non-tree vertex w is that adding v brings w closer than before to the tree. In short, we do not need to keep on the priority queue all of the edges from w to tree vertices—we just need to keep track of the minimum-weight edge and check whether the addition of v to the tree necessitates that we update that minimum, which we can do as we process each edge in v’s adjacency list. In other words, we maintain on the priority queue just one edge for each non-tree vertex w: the shortest edge that connects it to the tree. Any longer edge connecting w to the tree will become ineligible at some point, so there is no need to keep it on the priority queue.


```java
public class PrimMST {
    private Edge[] edgeTo;         // shortest edge from tree vertex
    private double[] distTo;        // distTo[w] = edgeTo[w].weight()
    private boolean[] marked;       // true if v on the tree
    private IndexMinPQ<Double> pq;  // eligible crossing edges

    public PrimMST(EdgeWeightedGraph G) {
        edgeTo = new Edge[G.V()];
        distTo = new double[G.V()];
        marked = new boolean[G.V()];
        for (int v = 0; v < G.V(); v++)
            distTo[v] = Double.POSITIVE_INFINITY;

        pq = new IndexMinPQ<Double>(G.V());
        distTo[0] = 0.0;
        pq.insert(0, 0.0);  // Initialize pq with 0, weight 0.

        while (!pq.isEmpty())
            visit(G, pq.delMin());  // Add the closest vertex to the tree.
    }

    private void visit(EdgeWeightedGraph G, int v) {
        // Add v to the tree; update data structures.
        marked[v] = true;

        for (Edge e : G.adj(v)) {
            int w = e.other(v);

            if (marked[w]) continue;  // v-w is ineligible.

            if (e.weight() < distTo[w]) {
                // Edge e is a new best connection from the tree to w.
                edgeTo[w] = e;
                distTo[w] = e.weight();

                if (pq.contains(w)) pq.change(w, distTo[w]);
                else pq.insert(w, distTo[w]);
            }
        }
    }

    public Iterable<Edge> edges() {
        // See Exercise 4.3.21.
    }

    public double weight() {
        // See Exercise 4.3.31.
    }
}
```

### Kruskal’s algorithm

To construct the Minimum Spanning Tree (MST) using Kruskal's algorithm, the edges are processed in order of their weight values. The algorithm colors each edge black (adding it to the MST) if it does not form a cycle with previously added edges. The process stops after adding V-1 edges.

Kruskal’s algorithm builds the MST one edge at a time, finding an edge that connects two trees in a forest of growing trees. The initial state is a forest of V single-vertex trees, and the algorithm combines two trees until only one tree (the MST) remains.

```java
public class KruskalMST {
    private Queue<Edge> mst;

    public KruskalMST(EdgeWeightedGraph G) {
        mst = new Queue<Edge>();
        MinPQ<Edge> pq = new MinPQ<Edge>(G.edges());
        UF uf = new UF(G.V());

        while (!pq.isEmpty() && mst.size() < G.V() - 1) {
            Edge e = pq.delMin();  // Get the min-weight edge on pq
            int v = e.either(), w = e.other(v);  // and its vertices.

            if (uf.connected(v, w)) continue;  // Ignore ineligible edges.

            uf.union(v, w);  // Merge components.
            mst.enqueue(e);  // Add the edge to mst.
        }
    }

    public Iterable<Edge> edges() {
        return mst;
    }

    public double weight() {
        // See Exercise 4.3.31.
    }
}
```


### Perspective

| Algorithm       | Worst-Case Time | Worst-Case Space |
|------------------|-----------------|------------------|
| Lazy Prim        | E * log(E)       | E                |
| Eager Prim       | V * E * log(V)   | E + V            |
| Kruskal          | E * log(E)       | E                |
| Fredman-Tarjan   | V * E + V * log(V) | V                |
| Chazelle         | V                | -                |

*Note: The space complexity of Chazelle's algorithm is very, very nearly E, but not quite E. The entry "Impossible?" for Chazelle's algorithm indicates uncertainty about the exact space complexity.*

In summary, the Minimum Spanning Tree (MST) problem is considered "solved" for practical purposes. For most graphs, the cost of finding the MST is only slightly higher than the cost of extracting the graph’s edges. This rule holds except for huge graphs that are extremely sparse, but the available performance improvement over the best-known algorithms even in this case is a small constant factor, perhaps a factor of 10 at best. These conclusions are borne out for many graph models, and practitioners have been using Prim’s and Kruskal’s algorithms to find MSTs in huge graphs for decades.

## SHORTEST PATH

When utilizing a map application or a navigation system to obtain directions from one location to another, one frequently encounters a graph-processing problem that is inherently intuitive. In this context, a graph model provides an immediate representation: vertices correspond to intersections, and edges correspond to roads. Additionally, weights on the edges capture relevant costs, such as distance or travel time. This graphical abstraction effectively mirrors the spatial relationships and navigational elements of the real-world road network, making it a natural fit for addressing routing challenges in map-based applications.

`Find the lowest-cost way to get from one vertex to another.`

|Application|Vertex|Edge|
|---|---|---|
|Map|Intersection|Road|
|Network Routing|Router|Connection|
|Job Scheduling|Job|Precedence Constraint|
|Currency Arbitrage|Currency|Exchange Rate|

>**Definition:**
>A shortest path from vertex *s* to vertex *t* in an edge-weighted digraph is a directed path from *s* to *t* with the property that no other such path has a lower weight.

**Single-Source Shortest Paths:**

Given an edge-weighted digraph and a source vertex *s*, the objective is to support queries of the form: "Is there a directed path from *s* to a given target vertex *t*?" If such a path exists, the goal is to find a shortest path, i.e., one whose total weight is minimal.

### Properties of shortest paths

**Characteristics of Shortest Paths:**

- Paths are directed. A shortest path must respect the direction of its edges.

- The weights are not necessarily distances. Geometric intuition can be helpful in understanding algorithms, so we use examples where vertices are points in the plane and weights are Euclidean distances, such as the digraph on the facing page. However, the weights might represent time or cost or an entirely different variable and do not need to be proportional to a distance at all. We emphasize this point by using mixed-metaphor terminology where we refer to a shortest path of minimal weight or cost.

- Not all vertices need to be reachable. If *t* is not reachable from *s*, there is no path at all, and therefore there is no shortest path from *s* to *t*.

- Negative weights introduce complications. For the moment, we assume that edge weights are positive (or zero). The surprising impact of negative weights is a major focus of the last part of this section.

- Shortest paths are normally simple. Our algorithms ignore zero-weight edges that form cycles so that the shortest paths they find have no cycles.

- Shortest paths are not necessarily unique. There may be multiple paths of the lowest weight from one vertex to another; we are content to find any one of them.

- Parallel edges and self-loops may be present. Only the lowest-weight among a set of parallel edges will play a role, and no shortest path contains a self-loop.


**Shortest-paths tree**

>**Definition:**
>Given an edge-weighted digraph and a designated vertex *s*, a shortest-paths tree for a source *s* is a subgraph containing *s* and all the vertices reachable from *s* that forms a directed tree rooted at *s*. Importantly, every tree path in this subgraph is a shortest path in the digraph.


### Edge-weighted digraph data types

**Class: `DirectedEdge`**

|Constructor|
|---|
|`DirectedEdge(int v, int w, double weight)`|

**Methods:**

```java
double weight();  // weight of this edge
int from();       // vertex this edge points from
int to();         // vertex this edge points to
String toString(); // string representation
```



**Class: `EdgeWeightedDigraph`**

|Constructor|
|---|
|`EdgeWeightedDigraph(int V)`|
|`EdgeWeightedDigraph(In in)`|

```java
int V();                                      // number of vertices
int E();                                      // number of edges
void addEdge(DirectedEdge e);                 // add e to this digraph
Iterable<DirectedEdge> adj(int v);            // edges pointing from v
Iterable<DirectedEdge> edges();                // all edges in this digraph
String toString();                            // string representation
```


```java
public class DirectedEdge {
    private final int v;         // edge source
    private final int w;         // edge target
    private final double weight; // edge weight

    public DirectedEdge(int v, int w, double weight) {
        this.v = v;
        this.w = w;
        this.weight = weight;
    }

    public double weight() {
        return weight;
    }

    public int from() {
        return v;
    }

    public int to() {
        return w;
    }

    public String toString() {
        return String.format("%d->%d %.2f", v, w, weight);
    }
}
```

```java
public class EdgeWeightedDigraph {
    private final int V;                    // number of vertices
    private int E;                          // number of edges
    private Bag<DirectedEdge>[] adj;        // adjacency lists

    public EdgeWeightedDigraph(int V) {
        this.V = V;
        this.E = 0;
        adj = (Bag<DirectedEdge>[]) new Bag[V];
        for (int v = 0; v < V; v++)
            adj[v] = new Bag<DirectedEdge>();
    }

    // Constructor for reading from an input stream - Exercise 4.4.2
    // public EdgeWeightedDigraph(In in) { /* Implementation omitted */ }

    public int V() {
        return V;
    }

    public int E() {
        return E;
    }

    public void addEdge(DirectedEdge e) {
        adj[e.from()].add(e);
        E++;
    }

    public Iterable<DirectedEdge> adj(int v) {
        return adj[v];
    }

    public Iterable<DirectedEdge> edges() {
        Bag<DirectedEdge> bag = new Bag<DirectedEdge>();
        for (int v = 0; v < V; v++)
            for (DirectedEdge e : adj[v])
                bag.add(e);
        return bag;
    }
}
```


***Shortest-paths API.**

```java
public class SP {
    // Constructor
    public SP(EdgeWeightedDigraph G, int s) {
        // Implementation omitted
    }

    // Distance from s to v, ∞ if no path
    public double distTo(int v) {
        // Implementation omitted
        return 0.0; // Placeholder return value
    }

    // Path from s to v?
    public boolean hasPathTo(int v) {
        // Implementation omitted
        return false; // Placeholder return value
    }

    // Path from s to v, null if none
    public Iterable<DirectedEdge> pathTo(int v) {
        // Implementation omitted
        return null; // Placeholder return value
    }
}
```

**Data structures for shortest paths**

- Edges on the Shortest-Paths Tree:
As for DFS, BFS, and Prim’s algorithm, we use a parent-edge representation in the form of a vertex-indexed array `edgeTo[]` of `DirectedEdge` objects, where `edgeTo[v]` is the edge that connects `v` to its parent in the tree.

- Distance to the Source:
We use a vertex-indexed array `distTo[]` such that `distTo[v]` is the length of the shortest known path from `s` to `v`. By convention, `edgeTo[s]` is `null`, and `distTo[s]` is `0`. We also adopt the convention that distances to vertices that are not reachable from the source are all `Double.POSITIVE_INFINITY`. As usual, we will develop data types that build these data structures in the constructor and then support instance methods that use them to support client queries for shortest paths and shortest-path distances.

**Edge relaxation**

Start by knowing only the graph’s edges and weights, with the `distTo[]` entry for the source initialized to 0 and all other `distTo[]` entries initialized to `Double.POSITIVE_INFINITY`. As the algorithm proceeds, it gathers information about the shortest paths that connect the source to each vertex encountered in our `edgeTo[]` and `distTo[]` data structures. By updating this information when encountering edges, new inferences about shortest paths can be made. To relax an edge v->w means to test whether the best-known way from s to w is to go from s to v, then take the edge from v to w. If so, the data structures are updated to indicate that this is the case.

```java
private void relax(DirectedEdge e) {
    int v = e.from(), w = e.to();
    
    if (distTo[w] > distTo[v] + e.weight()) {
        distTo[w] = distTo[v] + e.weight();
        edgeTo[w] = e;
    }
}
```

**Vertex relaxation**
```java
private void relax(EdgeWeightedDigraph G, int v) {
    for (DirectedEdge e : G.adj(v)) {
        int w = e.to();
        if (distTo[w] > distTo[v] + e.weight()) {
            distTo[w] = distTo[v] + e.weight();
            edgeTo[w] = e;
        }
    }
}
```



**Client query methods**

```java
public double distTo(int v) {
    return distTo[v];
}

public boolean hasPathTo(int v) {
    return distTo[v] < Double.POSITIVE_INFINITY;
}

public Iterable<DirectedEdge> pathTo(int v) {
    if (!hasPathTo(v)) {
        return null;
    }
    
    Stack<DirectedEdge> path = new Stack<DirectedEdge>();
    for (DirectedEdge e = edgeTo[v]; e != null; e = edgeTo[e.from()]) {
        path.push(e);
    }
    
    return path;
}
```


### Theoretical basis for shortest-paths algorithms

Edge relaxation is an easy-to-implement fundamental operation that provides a practical basis for our shortest-paths implementations. It also provides a theoretical basis for understanding the algorithms and an opportunity for us to do our algorithm correctness proofs at the outset.

### Dijkstra’s algorithm

Dijkstra’s algorithm is an analogous scheme to compute an SPT

Dijkstra’s algorithm solves the single-source shortest-paths problem in edge-weighted digraphs with nonnegative weights.

**Data structures**

To implement Dijkstra’s algorithm, we add to our `distTo[]` and `edgeTo[]` data structures an index priority queue (`pq`) to keep track of vertices that are candidates for being the next to be relaxed.

**Variants**

 **Single-Source Shortest Paths in Undirected Graphs**

Given an edge-weighted undirected graph and a source vertex *s*, the goal is to support queries of the form:
- Is there a path from *s* to a given target vertex *v*?
- If so, find a shortest path, one whose total weight is minimal.


Given an undirected graph, the goal is to build an edge-weighted digraph with the same vertices. This involves adding two directed edges (one in each direction) corresponding to each edge in the original undirected graph. The resulting edge-weighted digraph maintains a one-to-one correspondence between paths in the digraph and paths in the graph, and the costs of the paths are the same. Consequently, the shortest-paths problems in both the undirected graph and the edge-weighted digraph are equivalent.

```java
public class DijkstraSP {
    private DirectedEdge[] edgeTo;
    private double[] distTo;
    private IndexMinPQ<Double> pq;

    public DijkstraSP(EdgeWeightedDigraph G, int s) {
        edgeTo = new DirectedEdge[G.V()];
        distTo = new double[G.V()];
        pq = new IndexMinPQ<Double>(G.V());

        for (int v = 0; v < G.V(); v++)
            distTo[v] = Double.POSITIVE_INFINITY;

        distTo[s] = 0.0;
        pq.insert(s, 0.0);

        while (!pq.isEmpty())
            relax(G, pq.delMin());
    }

    private void relax(EdgeWeightedDigraph G, int v) {
        for (DirectedEdge e : G.adj(v)) {
            int w = e.to();
            if (distTo[w] > distTo[v] + e.weight()) {
                distTo[w] = distTo[v] + e.weight();
                edgeTo[w] = e;
                if (pq.contains(w)) pq.change(w, distTo[w]);
                else pq.insert(w, distTo[w]);
            }
        }
    }

    public double distTo(int v) {
        return distTo[v];
    }

    public boolean hasPathTo(int v) {
        return distTo[v] < Double.POSITIVE_INFINITY;
    }

    public Iterable<Edge> pathTo(int v) {
        // Implementation omitted (See page 649.)
        return null;
    }
}
```




**Source-Sink Shortest Paths**

Given an edge-weighted digraph, a source vertex *s*, and a target vertex *t*, the goal is to find the shortest path from *s* to *t*. To solve this problem, Dijkstra's algorithm is employed, but the search terminates as soon as *t* is dequeued from the priority queue.

 **All-Pairs Shortest Paths**

Given an edge-weighted digraph, the goal is to support queries of the form: Given a source vertex *s* and a target vertex *t*, is there a path from *s* to *t*? If so, find a shortest such path, one whose total weight is minimal.

To efficiently solve the all-pairs shortest paths problem using time and space proportional to \(E V \log V\), a method builds an array of `DijkstraSP` objects, one for each vertex as the source. To answer a client query, it utilizes the source to access the corresponding single-source shortest-paths object and then passes the target as an argument to the query.


```java
public class DijkstraAllPairsSP {
    private DijkstraSP[] all;

    public DijkstraAllPairsSP(EdgeWeightedDigraph G) {
        all = new DijkstraSP[G.V()];
        for (int v = 0; v < G.V(); v++)
            all[v] = new DijkstraSP(G, v);
    }

    public Iterable<Edge> path(int s, int t) {
        return all[s].pathTo(t);
    }

    public double dist(int s, int t) {
        return all[s].distTo(t);
    }
}
```

### Acyclic edge-weighted digraphs

For many natural applications, edge-weighted digraphs are known to have no directed cycles. Now, consider an algorithm for finding shortest paths that is simpler and faster than Dijkstra’s algorithm for edge-weighted Directed Acyclic Graphs (DAGs). Specifically, it:

- Solves the single-source problem in linear time
- Handles negative edge weights
- Solves related problems, such as finding longest paths.

```java
public class AcyclicSP {
    private DirectedEdge[] edgeTo;
    private double[] distTo;

    public AcyclicSP(EdgeWeightedDigraph G, int s) {
        edgeTo = new DirectedEdge[G.V()];
        distTo = new double[G.V()];
        
        for (int v = 0; v < G.V(); v++)
            distTo[v] = Double.POSITIVE_INFINITY;
        
        distTo[s] = 0.0;
        
        Topological top = new Topological(G);
        for (int v : top.order())
            relax(G, v);
    }

    private void relax(EdgeWeightedDigraph G, int v) {
        // Implementation omitted (See page 648.)
    }

    public double distTo(int v) {
        // Standard client query methods
        return distTo[v];
    }

    public boolean hasPathTo(int v) {
        // For SPT implementations
        return distTo[v] < Double.POSITIVE_INFINITY;
    }

    public Iterable<Edge> pathTo(int v) {
        // Implementation omitted (See page 649.)
        return null;
    }
}
```

**Longest Paths in Edge-Weighted DAGs**

Consider the problem of finding the longest path in an edge-weighted Directed Acyclic Graph (DAG) with edge weights that may be positive or negative.

**Single-Source Longest Paths in Edge-Weighted DAGs**

Given an edge-weighted DAG (with negative weights allowed) and a source vertex *s*, support queries of the form: Is there a directed path from *s* to a given target vertex *v*? If so, find the longest such path (one whose total weight is maximal).

**Parallel job scheduling**

**Parallel Precedence-Constrained Scheduling**

Given a set of jobs with specified durations and precedence constraints, where certain jobs must be completed before others can begin, the goal is to schedule the jobs on identical processors (as many as needed) to minimize the overall completion time while respecting the constraints.


>The critical path method for parallel scheduling follows these steps:
>1. Create an edge-weighted Directed Acyclic Graph (DAG) with a source *s*, a sink *t*, and two vertices for each job (a start vertex and an end vertex).
>2. For each job, add an edge from its start vertex to its end vertex with a weight equal to its duration.
>3. For each precedence constraint *v->w*, add a zero-weight edge from the end vertex corresponding to *v* to the beginning vertex corresponding to *w*.
>4. Add zero-weight edges from the source to each job’s start vertex and from each job’s end vertex to the sink.
>Now, schedule each job at the time given by the length of its longest path from the source.


```java
public class CPM {
    public static void main(String[] args) {
        int N = StdIn.readInt();
        StdIn.readLine();
        EdgeWeightedDigraph G;
        G = new EdgeWeightedDigraph(2 * N + 2);
        int s = 2 * N, t = 2 * N + 1;
        for (int i = 0; i < N; i++) {
            String[] a = StdIn.readLine().split("\\s+");
            double duration = Double.parseDouble(a[0]);
            G.addEdge(new DirectedEdge(i, i + N, duration));
            G.addEdge(new DirectedEdge(s, i, 0.0));
            G.addEdge(new DirectedEdge(i + N, t, 0.0));
            for (int j = 1; j < a.length; j++) {
                int successor = Integer.parseInt(a[j]);
                G.addEdge(new DirectedEdge(i + N, successor, 0.0));
            }
        }
        AcyclicLP lp = new AcyclicLP(G, s);
        StdOut.println("Start times:");
        for (int i = 0; i < N; i++)
            StdOut.printf("%4d: %5.1f\n", i, lp.distTo(i));
        StdOut.printf("Finish time: %5.1f\n", lp.distTo(t));
    }
}
```

### Shortest paths in general edge-weighted digraphs

Negative weights are not merely a mathematical curiosity; on the contrary, they significantly extend the applicability of the shortest-paths problem as a problem-solving model. Perhaps the most important effect is that when negative weights are present, low-weight shortest paths tend to have more edges than higher-weight paths. For positive weights, our emphasis was on looking for shortcuts; but when negative weights are present, we seek detours that use negative-weight edges.

**Strawman I.**

The first idea that suggests itself is to find the smallest (most negative) edge weight, then to add the absolute value of that number to all the edge weights to transform the digraph into one with no negative weights. This naive approach does not work at all because shortest paths in the new digraph bear little relation to shortest paths in the old one. The more edges a path has, the more it is penalized by this transformation.

**Strawman II.**

The second idea that suggests itself is to try to adapt Dijkstra’s algorithm in some way. The fundamental difficulty with this approach is that the algorithm depends on examining paths in increasing order of their distance from the source.

**Negative cycles**

>**Definition**: A negative cycle in an edge-weighted digraph is a directed cycle whose total weight (sum of the weights of its edges) is negative.

**Strawman III**

Whether or not there are negative cycles, there exists a shortest simple path connecting the source to each vertex reachable from the source. Why not define shortest paths so that we seek such paths? Thus, a well-posed and tractable version of the shortest paths problem in edge-weighted digraphs is to require algorithms to:

- Assign a shortest-path weight of ∞ to vertices that are not reachable from the source
- Assign a shortest-path weight of ∞ to vertices that are on a path from the source that has a vertex that is on a negative cycle
- Compute the shortest-path weight (and tree) for all other vertices

**Negative Cycle Detection**

- **Does a given edge-weighted digraph have a negative cycle? If it does, find one such cycle.**

- **Single-Source Shortest Paths when Negative Cycles are not Reachable**

  Given an edge-weighted digraph and a source *s* with no negative cycles reachable from *s*, support queries of the form: Is there a directed path from *s* to a given target vertex *v*? If so, find a shortest such path (one whose total weight is minimal).

To summarize: while shortest paths in digraphs with directed cycles is an ill-posed problem, and we cannot efficiently solve the problem of finding simple shortest paths in such digraphs, we can identify negative cycles in practical situations.


**Queue-based Bellman-Ford**

We can easily determine a priori that numerous edges are not going to lead to a successful relaxation in any given pass: the only edges that could lead to a change in `distTo[]` are those leaving a vertex whose `distTo[]` value changed in the previous pass. To keep track of such vertices, we use a FIFO queue.


**Implementation**

- A queue `q` of vertices to be relaxed.
- A vertex-indexed boolean array `onQ[]` that indicates which vertices are on the queue, to avoid duplicates. Only one copy of each vertex appears on the queue.
- Every vertex whose `edgeTo[]` and `distTo[]` values change in some pass is processed in the next pass.

```java
private void relax(EdgeWeightedDigraph G, int v) {
    for (DirectedEdge e : G.adj(v)) {
        int w = e.to();
        if (distTo[w] > distTo[v] + e.weight()) {
            distTo[w] = distTo[v] + e.weight();
            edgeTo[w] = e;
            if (!onQ[w]) {
                q.enqueue(w);
                onQ[w] = true;
            }
        }
        if (cost++ % G.V() == 0) {
            findNegativeCycle();
        }
    }
}
```

```java
public class BellmanFordSP {
    private double[] distTo; // length of path to v
    private DirectedEdge[] edgeTo; // last edge on path to v
    private boolean[] onQ; // Is this vertex on the queue?
    private Queue<Integer> queue; // vertices being relaxed
    private int cost; // number of calls to relax()
    private Iterable<DirectedEdge> cycle; // negative cycle in edgeTo[]?

    public BellmanFordSP(EdgeWeightedDigraph G, int s) {
        distTo = new double[G.V()];
        edgeTo = new DirectedEdge[G.V()];
        onQ = new boolean[G.V()];
        queue = new Queue<Integer>();

        for (int v = 0; v < G.V(); v++) {
            distTo[v] = Double.POSITIVE_INFINITY;
        }
        
        distTo[s] = 0.0;
        queue.enqueue(s);
        onQ[s] = true;

        while (!queue.isEmpty() && !this.hasNegativeCycle()) {
            int v = queue.dequeue();
            onQ[v] = false;
            relax(v);
        }
    }

    private void relax(int v) {
        // See page 673.
    }

    public double distTo(int v) {
        // standard client query methods
    }

    public boolean hasPathTo(int v) {
        // for SPT implementations
    }

    public Iterable<Edge> pathTo(int v) {
        // (See page 649.)
    }

    private void findNegativeCycle() {
    }

    public boolean hasNegativeCycle() {
    }

    public Iterable<Edge> negativeCycle() {
    }
}
```

**Negative cycle detection**

```java
public boolean hasNegativeCycle() {
    // Check if there is a negative cycle
}

public Iterable<DirectedEdge> negativeCycle() {
    // Return a negative cycle (null if no negative cycles)
}
```

```java
private void findNegativeCycle() {
    int V = edgeTo.length;
    EdgeWeightedDigraph spt;
    spt = new EdgeWeightedDigraph(V);

    for (int v = 0; v < V; v++) {
        if (edgeTo[v] != null) {
            spt.addEdge(edgeTo[v]);
        }
    }

    EdgeWeightedCycleFinder cf;
    cf = new EdgeWeightedCycleFinder(spt);
    cycle = cf.cycle();
}

public boolean hasNegativeCycle() {
    return cycle != null;
}

public Iterable<Edge> negativeCycle() {
    return cycle;
}
```

**Arbitrage.**

```java
public class Arbitrage {
    public static void main(String[] args) {
        int V = StdIn.readInt();
        String[] name = new String[V];
        EdgeWeightedDigraph G = new EdgeWeightedDigraph(V);

        for (int v = 0; v < V; v++) {
            name[v] = StdIn.readString();

            for (int w = 0; w < V; w++) {
                double rate = StdIn.readDouble();
                DirectedEdge e = new DirectedEdge(v, w, -Math.log(rate));
                G.addEdge(e);
            }
        }

        BellmanFordSP spt = new BellmanFordSP(G, 0);

        if (spt.hasNegativeCycle()) {
            double stake = 1000.0;
            for (DirectedEdge e : spt.negativeCycle()) {
                StdOut.printf("%10.5f %s ", stake, name[e.from()]);
                stake *= Math.exp(-e.weight());
                StdOut.printf("= %10.5f %s\n", stake, name[e.to()]);
            }
        } else {
            StdOut.println("No arbitrage opportunity");
        }
    }
}
```

### Perspective

The first reason to choose among the algorithms has to do with basic properties of the digraph at hand. Does it have negative weights? Does it have cycles? Does it have negative cycles? Beyond these basic characteristics, the characteristics of edge-weighted digraphs can vary widely, so choosing among the algorithms requires some experimentation when more than one can apply.


| Algorithm             | Restriction               | Path Length Compares | Extra Space | Sweet Spot                       | Typical Worst Case          |
|-----------------------|---------------------------|-----------------------|-------------|----------------------------------|-----------------------------|
| Dijkstra (eager)      | Positive edge weights     | E log V               | E log V     | V (worst-case guarantee)         | Worst-case guarantee       |
| Topological sort      | Edge-weighted DAGs         | E + V                 | E + V       | V (Optimal for acyclic)         | Optimal for acyclic        |
| Bellman-Ford (queue)  | No negative cycles        | E + V                 | VE          | V (Widely applicable)            | Widely applicable          |



# STRINGS

**Information processing**

In the modern world, virtually all information is encoded as a sequence of strings, and the applications that process it are string-processing applications of crucial importance

**Genomics**

Computational biologists work with a genetic code that reduces DNA to (very long) strings formed from four characters.

**Communications systems**

Applications that process strings for this purpose were an original motivation for the development of string-processing algorithms.

**Programming systems**

Programs are strings. Compilers, interpreters, and other applications that convert programs into machine instructions are critical applications that use sophisticated string-processing techniques. Indeed, all written languages are expressed as strings, and another motivation for the development of string-processing algorithms.

### Rules of the game

**Characters**

A string is a sequence of characters. Characters are of type char and can have one of 216 possible values.

**Immutability**

String objects are immutable, allowing us to use them in assignment statements, as arguments, and as return values from methods without having to worry about their values changing

**Length**

In Java, the operation to find the length of a string is implemented in the `length()` method of the `String` class.

**Substring**

In Java, the `substring()` method implements the operation to extract a specified substring. In Java's standard implementation, we expect a constant-time implementation of this method.

**Concatenation**

In Java, the operation to create a new string formed by appending one string to another is a built-in operation using the `+` operator. This operation takes time proportional to the length of the resulting string.


**Character arrays**

|Operation|Array of Characters (`char[] a`)|Java String (`String s`)|
|---|---|---|
|Declare|`char[] a`|`String s`|
|Indexed Access|`a[i]` |`s.charAt(i)`|
|Length|`a.length`|`s.length()`|
|Convert to Array|`a = s.toCharArray();`|`s = new String(a);`|

### Alphabets

**Alphabet API**:

- Constructor:
    
    - `Alphabet(String s)`: Creates a new alphabet from characters in `s`.
- Methods:
    
    - `char toChar(int index)`: Converts the given index to the corresponding alphabet character.
    - `int toIndex(char c)`: Converts the given character `c` to an index between 0 and R-1, where R is the radix (number of characters in the alphabet).
    - `boolean contains(char c)`: Checks if the character `c` is in the alphabet.
    - `int R()`: Returns the radix, i.e., the number of characters in the alphabet.
    - `int lgR()`: Returns the number of bits required to represent an index.
    - `int[] toIndices(String s)`: Converts the string `s` to a base-R integer.
    - `String toChars(int[] indices)`: Converts a base-R integer to a string over this alphabet.

**Character-indexed arrays**

One of the most important reasons to use Alphabet is that many algorithms gain efficiency through the use of character-indexed arrays, where we associate information with each character that we can retrieve with a single array access.

**Numbers.**

The `toIndices()` method converts any String over a given Alphabet into a base-R number represented as an int[] array with all values between 0 and R-1. In some situations, doing this conversion at the start leads to compact code, because any digit can be used as an index in a character-indexed array.

```java
int[] a = alpha.toIndices(s);
for (int i = 0; i < N; i++)
	count[a[i]]++;
```

## STRING SORT

For many sorting applications, the keys that define the order are strings. There are two fundamentally different approaches to string sorting, both of which have been reliable methods for many decades.

**Least-Significant-Digit (LSD) String Sorts**
The first approach involves examining the characters in the keys in a right-to-left order. These methods are commonly known as least-significant-digit (LSD) string sorts. LSD string sorts are particularly suitable when all the keys are of the same length.

**Most-Significant-Digit (MSD) String Sorts**
The second approach involves examining the characters in the keys in a left-to-right order, starting with the most significant character. These methods are generally referred to as most-significant-digit (MSD) string sorts. MSD string sorts are attractive because they can complete a sorting task without necessarily examining all of the input characters.

MSD string sorts bear similarity to quicksort. The key distinction is that MSD string sorts use only the first character of the sort key for partitioning, whereas quicksort uses comparisons that could involve examining the entire key.

### Key-indexed counting

**Compute frequency counts**

The first step in the process is to count the frequency of occurrence of each key value. This is done by utilizing an int array named count[]. For each item, the key is used to access an entry in count[], and that entry is then incremented. Specifically, if the key value is denoted as 'r', the algorithm increments count[r+1].

**Transform counts to indices**

Next, we utilize the count[] array to compute, for each key value, the starting index positions in the sorted order of items with that key. In general, to determine the starting index for items with any given key value, we sum the frequency counts of smaller values. For a key value 'r', the sum of the counts for key values less than 'r+1' is equal to the sum of the counts for key values less than 'r' plus count[r]. Therefore, it is straightforward to transform count[] from left to right into an index table, which can then be used to sort the data.

**Distribute the data**

After transforming the count[] array into an index table, the sorting process is achieved by moving the items to an auxiliary array aux[]. Each item is moved to the position in aux[] indicated by the count[] entry corresponding to its key. Subsequently, the entry in count[] is incremented to uphold the following invariant: for each key value 'r', count[r] represents the index in aux[] where the next item with key value 'r' (if any) should be placed.

Key-indexed counting is an extremely effective and often overlooked sorting method, particularly suitable for applications where keys are small integers.

```java
// Initialize variables.
int N = a.length;
String[] aux = new String[N];
int[] count = new int[R + 1];

// Compute frequency counts.
for (int i = 0; i < N; i++)
    count[a[i].key() + 1]++;

// Transform counts to indices.
for (int r = 0; r < R; r++)
    count[r + 1] += count[r];

// Distribute the records.
for (int i = 0; i < N; i++)
    aux[count[a[i].key()]++] = a[i];

// Copy back.
for (int i = 0; i < N; i++)
    a[i] = aux[i];
```


### LSD string sort

Suppose a highway engineer sets up a device to record license plate numbers of all vehicles using a busy highway. The goal is to determine the number of different vehicles that used the highway. License plates, being a mixture of numbers and letters, are naturally represented as strings. In a simple scenario, all strings have the same number of characters, a common case in sorting applications. Sorting such strings can be efficiently done with key-indexed counting.

If the strings are of length W, we perform W iterations of key-indexed counting, using each position as the key and proceeding from right to left. Initially, it might not be immediately evident that this method produces a sorted array. In fact, it only works effectively if the key-indexed count implementation is stable.

```java
public class LSD {
    public static void sort(String[] a, int W) {
        // Sort a[] on leading W characters.
        int N = a.length;
        int R = 256; // ASCII characters
        String[] aux = new String[N];

        for (int d = W - 1; d >= 0; d--) {
            // Sort by key-indexed counting on dth char.
            int[] count = new int[R + 1];

            // Compute frequency counts.
            for (int i = 0; i < N; i++)
                count[a[i].charAt(d) + 1]++;

            // Transform counts to indices.
            for (int r = 0; r < R; r++)
                count[r + 1] += count[r];

            // Distribute.
            for (int i = 0; i < N; i++)
                aux[count[a[i].charAt(d)]++] = a[i];

            // Copy back.
            for (int i = 0; i < N; i++)
                a[i] = aux[i];
        }
    }
}
```

From a theoretical standpoint, LSD string sort is significant because it is a linear-time sort for typical applications. Regardless of the value of N, it makes W passes through the data, making it an efficient sorting algorithm for scenarios where the strings have the same length.

### MSD string sort

To implement a general-purpose string sort, where strings are not necessarily all the same length, we consider the characters in left-to-right order. The idea is to sort strings based on their leftmost characters, so strings starting with 'a' should appear before strings starting with 'b', and so forth. The natural way to implement this idea is a recursive method known as most-significant-digit-first (MSD) string sort. In this approach, we use key-indexed counting to sort the strings according to their first character and then recursively sort the subarrays corresponding to each character.

**Specified alphabet**

The cost of MSD string sort depends strongly on the number of possible characters in the alphabet. To enhance efficiency for clients dealing with strings from relatively small alphabets, our sort method can be modified accordingly. The following changes can be implemented:

1. Save the alphabet in an instance variable `alpha` in the constructor.
2. Set `R` to `alpha.R()` in the constructor.
3. Replace `s.charAt(d)` with `alpha.toIndex(s.charAt(d))` in `charAt()`.

| Value of r  | Interpretation at Completion of Phase for dth Character |
|-------------|-------------------------------------------------------|
| r = 0       | Not used (frequencies 0).                             |
| r = 1       | Number of strings of length d.                         |
| 2 ≤ r < R   | Number of strings whose dth character value is r-2.   |
| r = R       | Transform counts to indices (start index of the subarray for strings of length d). |
| r = R+1     | Not used (not applicable in this context).            |

```java
public class MSD {
    private static int R = 256;        // radix
    private static final int M = 15;    // cutoff for small subarrays
    private static String[] aux;       // auxiliary array for distribution

    private static int charAt(String s, int d) {
        if (d < s.length()) return s.charAt(d);
        else return -1;
    }

    public static void sort(String[] a) {
        int N = a.length;
        aux = new String[N];
        sort(a, 0, N-1, 0);
    }

    private static void sort(String[] a, int lo, int hi, int d) {
        // Sort from a[lo] to a[hi], starting at the dth character.
        if (hi <= lo + M) {
            Insertion.sort(a, lo, hi, d);
            return;
        }

        int[] count = new int[R + 2];   // Compute frequency counts.
        for (int i = lo; i <= hi; i++)
            count[charAt(a[i], d) + 2]++;

        for (int r = 0; r < R + 1; r++) {
            // Transform counts to indices.
            count[r + 1] += count[r];
        }

        for (int i = lo; i <= hi; i++) {
            // Distribute.
            aux[count[charAt(a[i], d) + 1]++] = a[i];
        }

        for (int i = lo; i <= hi; i++) {
            // Copy back.
            a[i] = aux[i - lo];
        }

        // Recursively sort for each character value.
        for (int r = 0; r < R; r++) {
            sort(a, lo + count[r], lo + count[r + 1] - 1, d + 1);
        }
    }
}
```

**Small subarrays.**

The basic idea behind MSD string sort, examining only a few characters in the key, is highly effective in typical applications, quickly dividing the array into small subarrays. However, this efficiency comes with a trade-off: the method creates a large number of tiny subarrays. Therefore, it is crucial to handle these small subarrays efficiently, as they play a critical role in the overall performance of MSD string sort.

```java
public static void sort(String[] a, int lo, int hi, int d) {
    // Sort from a[lo] to a[hi], starting at the dth character.
    for (int i = lo; i <= hi; i++) {
        for (int j = i; j > lo && less(a[j], a[j - 1], d); j--) {
            exch(a, j, j - 1);
        }
    }
}

private static boolean less(String v, String w, int d) {
    return v.substring(d).compareTo(w.substring(d)) < 0;
}
```

**Equal keys**

A second challenge for MSD string sort is its potential inefficiency when dealing with subarrays containing a large number of equal keys. The use of key-indexed counting in such situations can be slow because not only does each character need to be examined, and each string moved, but all the counts also have to be initialized, converted to indices, and so forth. This process can become inefficient for large numbers of equal keys within subarrays.

**Extra space**

To perform partitioning, MSD string sort utilizes two auxiliary arrays: 
1. The temporary array for distributing keys (`aux[]`).
2. The array that holds the counts, which are transformed into partition indices (`count[]`).

The primary challenge in maximizing efficiency for MSD string sort on long strings is addressing the lack of randomness in the data. In typical scenarios, keys may exhibit long stretches of equal data, or certain parts of them might fall within only a narrow range. This lack of randomness can impact the performance of the sorting algorithm.

### Three-way string quicksort

Although it performs computations in a different order, 3-way string quicksort essentially involves sorting the array based on the leading characters of the keys. The method then applies the sorting process recursively to the remaining keys. When sorting strings, 3-way string quicksort compares favorably with normal quicksort and MSD string sort.

Three-way string quicksort divides the array into only three parts, which means it involves more data movement compared to MSD string sort when the number of nonempty partitions is large. This is because it performs a series of 3-way partitions to achieve the effect of a multiway partition.

```java
public class Quick3string {
    private static int charAt(String s, int d) {
        if (d < s.length()) return s.charAt(d);
        else return -1;
    }

    public static void sort(String[] a) {
        sort(a, 0, a.length - 1, 0);
    }

    private static void sort(String[] a, int lo, int hi, int d) {
        if (hi <= lo) return;

        int lt = lo, gt = hi;
        int v = charAt(a[lo], d);
        int i = lo + 1;

        while (i <= gt) {
            int t = charAt(a[i], d);
            if (t < v) exch(a, lt++, i++);
            else if (t > v) exch(a, i, gt--);
            else i++;
        }

        // a[lo..lt-1] < v = a[lt..gt] < a[gt+1..hi]
        sort(a, lo, lt - 1, d);
        if (v >= 0) sort(a, lt, gt, d + 1);
        sort(a, gt + 1, hi, d);
    }

    // Helper method to exchange elements in the array.
    private static void exch(String[] a, int i, int j) {
        String temp = a[i];
        a[i] = a[j];
        a[j] = temp;
    }
}
```

For string keys, standard quicksort, and other sorting algorithms are effectively MSD (Most-Significant-Digit) string sorts. This is because the `compareTo()` method in the `String` class accesses the characters in a left-to-right order. Specifically, it examines only the leading characters: if they are different, it compares only those characters; if the leading characters are the same, it then considers the next characters, and so forth. 

The core concept behind 3-way quicksort is to introduce special handling when the leading characters of the strings being compared are equal.

### Which string-sorting algorithm should I use?

| Algorithm            | Stable | Inplace | Order of Growth of CharAt() Calls | Sweet Spot               |
|-----------------------|--------|---------|-------------------------------------|--------------------------|
| Insertion Sort        | Yes    | Yes     | Between N and N^2                  | Small arrays, arrays in order |
| Quicksort             | No     | Yes     | N log N                             | General-purpose, tight space |
| Mergesort            | Yes    | No      | N log N                             | General-purpose, stable sort |
| 3-Way Quicksort      | No     | Yes     | Between N and N log N               | Large numbers of equal keys |
| LSD String Sort       | Yes    | No      | NW                                  | Short fixed-length strings |
| MSD String Sort       | Yes    | No      | Between N and Nw                   | Random strings              |
| 3-Way String Quicksort| No     | Yes     | Between N and Nw + log N           | General-purpose, long prefix matches |

## TRIES

The methods discussed in this section exhibit the following performance characteristics in typical applications, even for large tables:
- Search hits take time proportional to the length of the search key.
- Search misses involve examining only a few characters.

```java
public class StringST<Value> {
    // Create a symbol table
    StringST()

    // Put key-value pair into the table (remove key if value is null)
    void put(String key, Value val)

    // Get value paired with the key (null if key is absent)
    Value get(String key)

    // Remove key and its value
    void delete(String key)

    // Check if there is a value paired with the key
    boolean contains(String key)

    // Check if the table is empty
    boolean isEmpty()

    // Find the longest key that is a prefix of s
    String longestPrefixOf(String s)

    // Get all the keys having s as a prefix
    Iterable<String> keysWithPrefix(String s)

    // Get all the keys that match s (where . matches any character)
    Iterable<String> keysThatMatch(String s)

    // Get the number of key-value pairs
    int size()

    // Get all the keys in the table
    Iterable<String> keys()
}
```

Simple and efficient implementations that are the method of choice for small alphabets turn out to be useless for large alphabets because they consume too much space. In such cases, it is certainly worthwhile to add a constructor that allows clients to specify the alphabet.

### Tries

Consider a search tree known as a trie, a data structure built from the characters of the string keys that allows us to use the characters of the search key to guide the search.

**Basic properties**

As with search trees, tries are data structures composed of nodes that contain links, which are either null or references to other nodes. Each node is pointed to by just one other node, called its parent, and each node has R links, where R is the alphabet size. Tries often have a substantial number of null links, so when drawing a trie, null links are typically omitted. Each link in the trie corresponds to a character value, and each node is labeled with the character value corresponding to the link pointing to it. Additionally, each node has a corresponding value, which may be null or the value associated with one of the string keys in the symbol table.

**Search in a trie**

Each node in the trie has a link corresponding to each possible string character. The traversal starts at the root, then follows the link associated with the first character in the key. From that node, the traversal follows the link associated with the second character in the key, and so on, until reaching the last character of the key or encountering a null link.

**Insertion into a trie**

To insert in a trie, we first perform a search. In a trie, this involves using the characters of the key to guide us down the trie until reaching the last character of the key or encountering a null link. At this point, one of the following two conditions holds:
1. We encountered a null link before reaching the last character of the key. In this case, there is no trie node corresponding to the last character in the key. Therefore, we need to create nodes for each of the characters in the key not yet encountered and set the value in the last one to the value to be associated with the key.
2. We encountered the last character of the key before reaching a null link. In this case, we set that node’s value to the value to be associated with the key (whether or not that value is null), following our associative array convention.

**Node representation**

Taking null links into account emphasizes the following important characteristics of tries:
1. Every node has R links, one for each possible character.
2. Characters and keys are implicitly stored in the data structure.

Keys in the trie are implicitly represented by paths from the root that end at nodes with non-null values.

**Size**

There are different ways to implement the number of keys in a trie, including:
1. An eager implementation where we maintain the number of keys in an instance variable N.
2. A very eager implementation where we maintain the number of keys in a subtrie as a node instance variable, which we update after the recursive calls in put() and delete().
3. A lazy recursive implementation that traverses all nodes in the trie, counting the number having a non-null value.

```java
public int size() {
    return size(root);
}

private int size(Node x) {
    if (x == null) return 0;
    int cnt = 0;
    if (x.val != null) cnt++;
    for (char c = 0; c < R; c++)
        cnt += size(x.next[c]);
    return cnt;
}
```

```java
public class TrieST<Value> {
    private static int R = 256; // radix
    private Node root; // root of trie

    private static class Node {
        private Object val;
        private Node[] next = new Node[R];
    }

    public Value get(String key) {
        Node x = get(root, key, 0);
        if (x == null) return null;
        return (Value) x.val;
    }

    private Node get(Node x, String key, int d) { // Return value associated with key in the subtrie rooted at x.
        if (x == null) return null;
        if (d == key.length()) return x;
        char c = key.charAt(d); // Use dth key char to identify subtrie.
        return get(x.next[c], key, d+1);
    }

    public void put(String key, Value val) {
        root = put(root, key, val, 0);
    }

    private Node put(Node x, String key, Value val, int d) { // Change value associated with key if in subtrie rooted at x.
        if (x == null) x = new Node();
        if (d == key.length()) {
            x.val = val;
            return x;
        }
        char c = key.charAt(d); // Use dth key char to identify subtrie.
        x.next[c] = put(x.next[c], key, val, d+1);
        return x;
    }
}
```

**Collecting keys**

Because characters and keys are represented implicitly in tries, providing clients with the ability to iterate through the keys presents a challenge

```java
import java.util.LinkedList;
import java.util.Queue;

public Iterable<String> keys() {
    return keysWithPrefix("");
}

public Iterable<String> keysWithPrefix(String pre) {
    Queue<String> q = new LinkedList<>();
    collect(get(root, pre, 0), pre, q);
    return q;
}

private void collect(Node x, String pre, Queue<String> q) {
    if (x == null) return;
    if (x.val != null) q.offer(pre);
    for (char c = 0; c < R; c++) {
        collect(x.next[c], pre + c, q);
    }
}
```

**Wildcard Match**

```java
public Iterable<String> keysThatMatch(String pat) {
    Queue<String> q = new LinkedList<>();
    collect(root, "", pat, q);
    return q;
}

public void collect(Node x, String pre, String pat, Queue<String> q) {
    int d = pre.length();
    if (x == null) return;
    if (d == pat.length() && x.val != null) q.offer(pre);
    if (d == pat.length()) return;
    char next = pat.charAt(d);
    for (char c = 0; c < R; c++) {
        if (next == '.' || next == c) {
            collect(x.next[c], pre + c, pat, q);
        }
    }
}
```

**Longest prefix**

```java
public String longestPrefixOf(String s) {
    int length = search(root, s, 0, 0);
    return s.substring(0, length);
}

private int search(Node x, String s, int d, int length) {
    if (x == null) return length;
    if (x.val != null) length = d;
    if (d == s.length()) return length;
    char c = s.charAt(d);
    return search(x.next[c], s, d + 1, length);
}
```

**Deletion**

```java
public void delete(String key) {
    root = delete(root, key, 0);
}

private Node delete(Node x, String key, int d) {
    if (x == null) return null;
    if (d == key.length()) {
        x.val = null;
    } else {
        char c = key.charAt(d);
        x.next[c] = delete(x.next[c], key, d + 1);
    }

    if (x.val != null) return x;

    for (char c = 0; c < R; c++) {
        if (x.next[c] != null) return x;
    }

    return null;
}
```

### Properties of tries

ries provide a unique structure for a given set of keys, and this characteristic remains consistent regardless of the order in which keys are inserted or deleted. This distinguishes tries from other search tree structures.

**Worst-case time bound for search and insert**

In a trie, the number of array accesses required for searching or inserting a key is at most 1 plus the length of the key.

**Expected time bound for search miss**

The average number of nodes examined for a search miss in a trie, built from N random keys over an alphabet of size R, is approximately proportional to log base R of N

**Space**

The number of links in a trie is between RN and RNw, where N is the number of keys, R is the size of the alphabet, and w is the average key length.

| Application | Average Key Length (�w) | Alphabet Size (�R) | Links in Trie |
| ---- | ---- | ---- | ---- |
| CA License Plates | 7 | 256 | 256 million |
| Account Numbers | 20 | 256 | 4 billion |
| URLs (e.g., [www.cs.princeton.edu](http://www.cs.princeton.edu/)) | 28 | 256 | 4 billion |
| Text Processing (e.g., "seashells") | 11 | 256 | 256 million |
| Proteins in Genomic Data (e.g., "ACTGACTG") | 8 | 256 | 256 million |

### Ternary search tries (TSTs)

In a TST (Ternary Search Trie), each node consists of a character, three links, and a value. The three links represent keys whose current characters are less than, equal to, or greater than the node's character. In the corresponding TST, characters are explicitly present in nodes. We encounter characters corresponding to keys only when traversing the middle links.

```java
public class TST<Value>
{
    private Node root; // root of trie

    private class Node
    {
        char c; // character
        Node left, mid, right; // left, middle, and right subtries
        Value val; // value associated with string
    }

    public Value get(String key) // same as for tries (See page 737).
    private Node get(Node x, String key, int d)
    {
        if (x == null) return null;
        char c = key.charAt(d);
        if (c < x.c) return get(x.left, key, d);
        else if (c > x.c) return get(x.right, key, d);
        else if (d < key.length() - 1) return get(x.mid, key, d+1);
        else return x;
    }

    public void put(String key, Value val)
    {
        root = put(root, key, val, 0);
    }

    private Node put(Node x, String key, Value val, int d)
    {
        char c = key.charAt(d);
        if (x == null) { x = new Node(); x.c = c; }
        if (c < x.c) x.left = put(x.left, key, val, d);
        else if (c > x.c) x.right = put(x.right, key, val, d);
        else if (d < key.length() - 1) x.mid = put(x.mid, key, val, d+1);
        else x.val = val;
        return x;
    }
}
```

### Properties of TSTs

**Space**

The most important property of TSTs is that they have just three links in each node, so a TST requires far less space than the corresponding trie. The number of links in a TST built from N string keys of average length w is between 3N and 3Nw.

**Search cost**

To determine the cost of search (and insert) in a TST, we multiply the cost for the corresponding trie by the cost of traversing the BST representation of each trie node. A search miss in a TST built from N random string keys requires ~ln N character compares, on average. A search hit or an insertion in a TST uses a character compare for each character in the search key.

### Which string symbol-table implementation should I use?

| Algorithm (Data Structure) | Typical Growth Rate for N Strings (Average Length w) | Sweet Spot |
| ---- | ---- | ---- |
| Binary Tree Search (BST) | �1(log⁡�)2c1​(logN)2 | 64N randomly ordered keys |
| 2-3 Tree Search (Red-Black BST) | �2(log⁡�)2c2​(logN)2 | 64N guaranteed performance |
| Linear Probing† (Parallel Arrays) | w | 32N to 128N built-in types, cached hash values |
| Trie Search (R-Way Trie) | log⁡��logRN (8R56)N to (8R56)Nw | Short keys, small alphabets |
| Trie Search (TST) | 1.39log⁡�1.39logN | 64N to 64Nw nonrandom keys |

## SUBSTRING SEARCH

The fundamental operation on strings is substring search: given a text string of length N and a pattern string of length M, find an occurrence of the pattern within the text. In today’s world, we are often searching through the vast amount of information available on the web. In substring search, we typically preprocess the pattern in order to be able to support fast searches for that pattern in the text.

### A short history

There is a simple brute-force algorithm for substring search that is in widespread
use. While it has a worst-case running time proportional to MN, the strings that arise
in many applications lead to a running time that is (except in pathological cases) proportional
to M * N
Both the Knuth-Morris-Pratt (KMP) and the Boyer-Moore algorithms require some
complicated preprocessing on the pattern that is difficult to understand and has limited
the extent to which they are used.


### Brute-force substring search

An obvious method for substring search is to check, for each possible position in the text at which the pattern could match, whether it does in fact match.  Brute-force substring search requires ~NM character compares to search for a pattern of length M in a text of length N, in the worst case.

```java
  public static int search(String pat, String txt) {
    int M = pat.length();  // Length of the pattern
    int N = txt.length();  // Length of the text

    // Iterate through possible positions in the text where the pattern could match
    for (int i = 0; i <= N - M; i++) {
        int j;

        // Check each character of the pattern against the corresponding character in the text
        for (j = 0; j < M; j++) {
            if (txt.charAt(i + j) != pat.charAt(j)) {
                break;  // Characters don't match, break out of the loop
            }
        }

        // If the inner loop completes without breaking, the pattern is found
        if (j == M) {
            return i;  // Return the starting index of the found pattern in the text
        }
    }

    return N;  // Return N if the pattern is not found in the text
  }

```

```java
public static int search(String pat, String txt) {
    int M = pat.length();
    int N = txt.length();
    int j = 0;
    int i;

    for (i = 0; i < N && j < M; i++) {
        if (txt.charAt(i) == pat.charAt(j)) {
            j++;
        } else {
            i -= j;
            j = 0;
        }
    }

    if (j == M) {
        return i - M;  // found
    } else {
        return N;  // not found
    }
}
```


### Knuth-Morris-Pratt substring search

Whenever we detect a mismatch, we already know some of the characters in the text (since they matched the pattern characters prior to the mismatch). We can take advantage of this information to avoid backing up the text pointer over all those known characters.

The key observation is that we need not back up the text pointer `i`, since the previous four characters in the text are all 'A's and do not match the first character in the pattern. For this pattern, we can change the `else` clause in the alternate brute-force implementation to just set `j = 1` (and not decrement `i`). Since the value of `i` does not change within the loop, this method does at most N character compares. Surprisingly, it is always possible to find a value to set the `j` pointer to on a mismatch, so that the `i` pointer is never decremented.

**Backing up the pattern pointer**

In KMP substring search, we never back up the text pointer `i`, and we use a two-dimensional array `dfa[][]` to record how far to back up the pattern pointer `j` when a mismatch is detected.

**KMP search method**

Once we have computed the `dfa[][]` array, in substring search, when `i` and `j` point to mismatching characters, the next possible position for a pattern match is beginning at position `i - dfa[txt.charAt(i)][j]`.

```java
public int search(String txt, int M) {
    // Simulate the operation of DFA on txt.
    int i, j, N = txt.length();
    for (i = 0, j = 0; i < N && j < M; i++)
        j = dfa[txt.charAt(i)][j];
    
    if (j == M) return i - M; // found
    else return N; // not found
}
```

```java
public class KMP {
    private String pat;
    private int[][] dfa;

    public KMP(String pat) {
        // Build DFA from pattern.
        this.pat = pat;
        int M = pat.length();
        int R = 256;
        dfa = new int[R][M];
        dfa[pat.charAt(0)][0] = 1;
        for (int X = 0, j = 1; j < M; j++) {
            // Compute dfa[][j].
            for (int c = 0; c < R; c++)
                dfa[c][j] = dfa[c][X]; // Copy mismatch cases.
            dfa[pat.charAt(j)][j] = j + 1; // Set match case.
            X = dfa[pat.charAt(j)][X]; // Update restart state.
        }
    }

    public int search(String txt) {
        // Simulate operation of DFA on txt.
        int i, j, N = txt.length(), M = pat.length();
        for (i = 0, j = 0; i < N && j < M; i++)
            j = dfa[txt.charAt(i)][j];
        if (j == M) return i - M; // found (hit end of pattern)
        else return N; // not found (hit end of text)
    }

    public static void main(String[] args) {
        // Example usage
        String pattern = "ABABC";
        String text = "ABABDABABCABABC";
        
        KMP kmp = new KMP(pattern);
        int index = kmp.search(text);
        
        if (index != text.length()) {
            System.out.println("Pattern found at index " + index);
        } else {
            System.out.println("Pattern not found in the text.");
        }
    }
}
```

### Boyer-Moore substring search

When backup in the text string is not a problem, we can develop a significantly faster substring-searching method by scanning the pattern from right to left when trying to match it against the text. In general, the pattern at the end might appear elsewhere, so we need an array of restart positions as for Knuth-Morris-Pratt.

```java
public class BoyerMoore
{
    private int[] right;
    private String pat;

    BoyerMoore(String pat)
    { // Compute skip table.
        this.pat = pat;
        int M = pat.length();
        int R = 256;
        right = new int[R];
        for (int c = 0; c < R; c++)
            right[c] = -1; // -1 for chars not in pattern
        for (int j = 0; j < M; j++) // rightmost position for chars in pattern
            right[pat.charAt(j)] = j;
    }

    public int search(String txt)
    { // Search for pattern in txt.
        int N = txt.length();
        int M = pat.length();
        int skip;
        for (int i = 0; i <= N - M; i += skip)
        { // Does the pattern match the text at position i?
            skip = 0;
            for (int j = M - 1; j >= 0; j--)
                if (pat.charAt(j) != txt.charAt(i + j))
                {
                    skip = j - right[txt.charAt(i + j)];
                    if (skip < 1) skip = 1;
                    break;
                }
            if (skip == 0) return i; // found.
        }
        return N; // not found.
    }

    public static void main(String[] args)
    {
        // See page 769.
    }
}
```

The substring search with the Boyer-Moore mismatched character heuristic typically uses approximately N - M character compares to search for a pattern of length M in a text of length N on typical inputs.

### Rabin-Karp fingerprint search

The approach to substring search based on hashing involves computing a hash function for the pattern and then searching for a match by applying the same hash function to each possible M-character substring of the text. While this approach can be efficient, a straightforward implementation based on this description might be slower than a brute-force search.

**Implementation**

```java
public class RabinKarp
{
    private String pat; // pattern (only needed for Las Vegas)
    private long patHash; // pattern hash value
    private int M; // pattern length
    private long Q; // a large prime
    private int R = 256; // alphabet size
    private long RM; // R^(M-1) % Q

    public RabinKarp(String pat)
    {
        this.pat = pat; // save pattern (only needed for Las Vegas)
        this.M = pat.length();
        Q = longRandomPrime(); // See Exercise 5.3.33.
        RM = 1;
        for (int i = 1; i <= M-1; i++) // Compute R^(M-1) % Q for use
            RM = (R * RM) % Q; // in removing leading digit.
        patHash = hash(pat, M);
    }

    public boolean check(int i) // Monte Carlo (See text.)
    {
        return true; // For Las Vegas, check pat vs txt(i..i-M+1).
    }

    private long hash(String key, int M)
    {
        // See text (page 775).
    }

    private int search(String txt)
    {
        // Search for hash match in text.
        int N = txt.length();
        long txtHash = hash(txt, M);
        if (patHash == txtHash) return 0; // Match at the beginning.
        for (int i = M; i < N; i++)
        {
            // Remove leading digit, add trailing digit, check for a match.
            txtHash = (txtHash + Q - RM * txt.charAt(i - M) % Q) % Q;
            txtHash = (txtHash * R + txt.charAt(i)) % Q;
            if (patHash == txtHash)
                if (check(i - M + 1)) return i - M + 1; // Match found.
        }
        return N; // No match found.
    }
}
```

Rabin-Karp substring search is known as a fingerprint search because it uses a small amount of information to represent a (potentially very large) pattern. Then it looks for this fingerprint (the hash value) in the text. The algorithm is efficient because the fingerprints can be efficiently computed and compared.

### Summary

| Algorithm                | Version           | Operation Count | Backup in Input? | Correct? | Extra Guarantee | Typical Space |
|--------------------------|-------------------|------------------|-------------------|----------|-----------------|---------------|
| Brute Force              | —                 | M * N            | 1.1 * N           | Yes      | Yes             | 1             |
| Knuth-Morris-Pratt       | Full DFA          | 2 * N            | 1.1 * N           | No       | Yes             | MR            |
|                          | Mismatch          | 3 * N            | 1.1 * N           | No       | Yes             | M             |
|                          | Transitions Only  |                  |                   |          |                 |               |
| Boyer-Moore              | Full Algorithm    | 3 * N            | N / M             | Yes      | Yes             | R             |
|                          | Mismatched Char   | M * N            | N / M             | Yes      | Yes             | R             |
|                          | Heuristic Only    |                  |                   |          |                 |               |
| Rabin-Karp               | Monte Carlo        | 7 * N            | 7 * N             | No       | Yes†            | 1             |
|                          | Las Vegas          | 7 * N            | 7 * N†            | Yes      | Yes             | 1             |

## REGULAR EXPRESSIONS

The basic mechanisms we will consider make possible a very powerful string-searching facility that can match complicated M-character patterns in N-character text strings in time proportional to MN in the worst case, and much faster for typical applications.

### Describing patterns with regular expressions

*Focus on pattern descriptions made up of characters that serve as operands for three fundamental operations.*

**Concatenation**

The first fundamental operation is the one used in the last section. When we write `AB`, we are specifying the language `{ AB }` that has one two-character string, formed by concatenating A and B.

**Or**

The second fundamental operation allows us to specify alternatives in the pattern. If we have an `or` between two alternatives, then both are in the language. We will use the vertical bar symbol `|` to denote this operation.

**Closure**

The third fundamental operation allows parts of the pattern to be repeated arbitrarily. The closure of a pattern is the language of strings formed by concatenating the pattern with itself any number of times.

**Parentheses**

use parentheses to override the default precedence rules.

| Description                           | Regular Expression      | Matches                                      | Does Not Match                              |
|---------------------------------------|-------------------------|----------------------------------------------|---------------------------------------------|
| RE matches                            | `(A|B)(C|D)`            | `AC`, `AD`, `BC`, `BD`                      | Every other string (e.g., `AC`, `AD`, `BC`, `BD`, ...) |
| RE does not match every other string   |                         |                                              |                                             |
| Examples                              | `A(B|C)*D`              | `AD`, `ABD`, `ACD`, `ABCCBD`, `BCD`         |                                             |
|                                       | `A* | (A*BA*BA*)*`       | `AAA`, `BBAABB`, `BABAAA`, `ABA`, `BBB`, `BABBAAA` |                                             |


**Definition**

A regular expression (RE) is either:

- Empty
- A single character
- A regular expression enclosed in parentheses
- Two or more concatenated regular expressions
- Two or more regular expressions separated by the or operator (|)
- A regular expression followed by the closure operator (*)

 **Definition (continued)**

Each RE represents a set of strings, defined as follows:

- The empty RE represents the empty set of strings, with 0 elements.
- A character represents the set of strings with one element, itself.
- An RE enclosed in parentheses represents the same set of strings as the RE without the parentheses.
- The RE consisting of two concatenated REs represents the cross product of the sets of strings represented by the individual components (all possible strings that can be formed by taking one string from each and concatenating them, in the same order as the REs).
- The RE consisting of the or of two REs represents the union of the sets represented by the individual components.
- The RE consisting of the closure of an RE represents ε (the empty string) or the union of the sets represented by the concatenation of any number of copies of the RE.

### Shortcuts

**Set-of-characters descriptors**

It is often convenient to be able to use a single character or a short sequence to directly specify sets of characters. The dot character (`.`) is a wildcard that represents any single character.

| Notation                      | Example        | Description                                      |
|-------------------------------|----------------|--------------------------------------------------|
| Name Notation                 | `wildcard`     | `.A.B` - Matches any string with 'A' in the middle.|
| Specified Set (Square Brackets)| `[AEIOU]*`     | Matches strings consisting of zero or more vowels (AEIOU).|
| Range (Square Brackets)        | `[A-Z]`        | Matches any single uppercase letter.              |
|                               | `[0-9]`        | Matches any single digit.                        |
| Complement (Square Brackets)   | `[^AEIOU]*`    | Matches strings with zero or more characters not in the set (AEIOU).|

**Closure shortcuts**

The closure operator (*) specifies any number of copies of its operand. In practice, we want the flexibility to specify the number of copies, or a range on the number.

**Escape sequences**

Some characters, such as `\`, `.`, `|`, `*`, `(`, and `)`, are metacharacters that we use to form regular expressions. We use escape sequences that begin with a backslash character `\` separating metacharacters from characters in the alphabet.


### REs in applications

* Substring search
* Validity checking
* Programmer’s toolbox
* Genomics
* Search
* Possibilities

**Limitations**

Not all languages can be specified with REs. A thought-provoking example is that no RE can describe the set of all strings that specify legal REs. Simpler versions of this example are that we cannot use REs to check whether parentheses are balanced or to check whether a string has an equal number of As and Bs.

### Nondeterministic finite-state automata

The finite-state automaton for KMP changes from state to state by looking at a character from the text string and then changing to another state, depending on the character. The automaton reports a match if and only if it reaches the accept state. The algorithm itself is a simulation of the automaton. The characteristic of the machine that makes it easy to simulate is that it is deterministic: each state transition is completely determined by the next character in the text.

### Building an NFA corresponding to an RE

- REs do not have an explicit operator for concatenation.
- REs have a unary operator for closure (*).
- REs have only one binary operator for or (|).

**Concatenation**

In terms of the NFA, the concatenation operation is the simplest to implement. Match transitions for states corresponding to characters in the alphabet explicitly implement concatenation.

**Parentheses**

To manage parentheses in regular expressions, we push the regular expression (RE) index of each left parenthesis on the stack. Each time we encounter a right parenthesis, we eventually pop the corresponding left parentheses from the stack in the manner.

**Closure**

A closure (*) operator must occur either:
(i) After a single character, when we add ε-transitions to and from the character.
(ii) After a right parenthesis, when we add ε-transitions to and from the corresponding left parenthesis, the one at the top of the stack.

```java
import java.util.Stack;

public class NFA {
    private char[] re; // match transitions
    private Digraph G; // epsilon transitions
    private int M; // number of states

    public NFA(String regexp) {
        // Create the NFA for the given regular expression.
        Stack<Integer> ops = new Stack<>();
        re = regexp.toCharArray();
        M = re.length;
        G = new Digraph(M + 1);

        for (int i = 0; i < M; i++) {
            int lp = i;

            if (re[i] == '(' || re[i] == '|') {
                ops.push(i);
            } else if (re[i] == ')') {
                int or = ops.pop();
                if (re[or] == '|') {
                    lp = ops.pop();
                    G.addEdge(lp, or + 1);
                    G.addEdge(or, i);
                } else {
                    lp = or;
                }
            }

            if (i < M - 1 && re[i + 1] == '*') { // lookahead
                G.addEdge(lp, i + 1);
                G.addEdge(i + 1, lp);
            }

            if (re[i] == '(' || re[i] == '*' || re[i] == ')') {
                G.addEdge(i, i + 1);
            }
        }
    }

    public boolean recognizes(String txt) {
        // Does the NFA recognize txt? (See page 799.)
        DirectedDFS dfs = new DirectedDFS(G, 0);

        for (int v = 0; v < G.V(); v++) {
            if (dfs.marked(v) && v < M) {
                if (re[v] == txt.charAt(0) || re[v] == '.') {
                    dfs = new DirectedDFS(G, v);
                    break;
                }
            }
        }

        for (int i = 1; i <= txt.length(); i++) {
            Bag<Integer> states = new Bag<>();
            for (int v = 0; v < G.V(); v++) {
                if (dfs.marked(v) && v < M) {
                    if (re[v] == txt.charAt(i - 1) || re[v] == '.') {
                        states.add(v + 1);
                    }
                }
            }

            dfs = new DirectedDFS(G, states);
        }

        for (int v = 0; v < G.V(); v++) {
            if (dfs.marked(v) && v == M) {
                return true;
            }
        }

        return false;
    }
}
```

## DATA COMPRESSION

There are two primary reasons to compress data: to save storage when saving information and to save time when communicating information.

The algorithms we will examine save space by exploiting the fact that most data files have a great deal of redundancy. The effectiveness of any data compression method is quite dependent on characteristics of the input.

### Rules of the game

All of the types of data that we process with modern computer systems have something in common: they are ultimately represented in binary. We can consider each of them to be simply a sequence of bits (or bytes).

**Basic model**

The model of data compression involves two primary components, each a black box that reads and writes bitstreams:

- A compress box that transforms a bitstream B into a compressed version C(B).
- An expand box that transforms C(B) back into B.

This model is known as lossless compression—we insist that no information be lost, in the specific sense that the result of compressing and expanding a bitstream must match the original, bit for bit.

However, it is reasonable to consider compression methods that are allowed to lose some information, so the decoder only produces an approximation of the original file. Lossy methods have to be evaluated in terms of a subjective quality standard in addition to the compression ratio.

### Reading and writing binary data

These APIs, BinaryStdIn and BinaryStdOut, are modeled on the StdIn and StdOut APIs that you have been using, but their purpose is to read and write bits, where StdIn and StdOut are oriented toward character streams encoded in Unicode.

**Binary input and output**

The goal is to minimize the necessity for type conversion in client programs and also to take care of operating system conventions for representing data.



#### Methods:

- `boolean readBoolean()`: Read 1 bit of data and return as a boolean value.
- `char readChar()`: Read 8 bits of data and return as a char value.
- `char readChar(int r)`: Read r (between 1 and 16) bits of data and return as a char value.
- [Similar methods for other types:]
  - `byte readByte()`: Read 8 bits of data and return as a byte value.
  - `short readShort()`: Read 16 bits of data and return as a short value.
  - `int readInt()`: Read 32 bits of data and return as an int value.
  - `long readLong()`: Read 64 bits of data and return as a long value.
  - `double readDouble()`: Read 64 bits of data and return as a double value.

- `boolean isEmpty()`: Check if the bitstream is empty.
- `void close()`: Close the bitstream.

#### Static Methods:

- [API for static methods that read from a bitstream on standard input.]

A key feature of the abstraction is that, in marked contrast to StdIn, the data on standard input is not necessarily aligned on byte boundaries.

### `BinaryStdOut` Class

#### Methods:

- `void write(boolean b)`: Write the specified bit.
- `void write(char c)`: Write the specified 8-bit char.
- `void write(char c, int r)`: Write the r (between 1 and 16) least significant bits of the specified char.
- [Similar methods for other types:]
  - `void write(byte b)`: Write the specified 8 bits.
  - `void write(short s)`: Write the specified 16 bits.
  - `void write(int i)`: Write the specified 32 bits.
  - `void write(long l)`: Write the specified 64 bits.
  - `void write(double d)`: Write the specified 64 bits.

- `void close()`: Close the bitstream.

#### Static Methods:

- [API for static methods that write to a bitstream on standard output.]



In summary, working with data compression requires us to reorient our thinking about standard input and standard output to include binary encoding of data. `BinaryStdIn` and `BinaryStdOut` provide the methods that we need. They offer a way for you to make a clear distinction in your client programs between writing out information intended for file storage and data transmission (that will be read by programs) and printing information.

### Limitations

**Universal data compression**

universal data compression is impossible , No algorithm can compress every bitstream.

**Undecidability**

```java
public class RandomBits {
    public static void main(String[] args) {
        int x = 11111;

        for (int i = 0; i < 1000000; i++) {
            x = x * 314159 + 218281;
            BinaryStdOut.write(x > 0);
        }

        BinaryStdOut.close();
    }
}
```

The practical impact of these limitations is that lossless compression methods must be oriented toward taking advantage of known structure in the bitstreams to be compressed. The four methods that we consider exploit, in turn, the following structural characteristics:

- Small alphabets
- Long sequences of identical bits/characters
- Frequently used characters
- Long reused bit/character sequences




