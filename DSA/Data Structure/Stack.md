
# Stack

## Understanding the problem

Many times in a program, we need to have a data store that is **smart** enough and remembers the order in which the data was added. This is especially useful in cases where we want to process data items in a **L**ast **I**n **F**irst **O**ut **(LIFO)** or **F**irst **I**n **L**ast **O**ut (**FILO**) order. This is a fairly common requirement in many use cases

### Web browsers

This is perhaps the most visible use case where the order of data items matters. All modern web browsers have a **back** button that takes you to the previous webpage you were browsing. This functionality is very simple and straightforward, but to implement this, we need to store all the web pages the user visits and present the data in reverse **(LIFO)** order when the user clicks the back button.

### Text editors

Like web browsers, this is another example of a problem that relies on the order of data added to a data store. Almost all text editors have an **undo** feature that lets us revert changes in the order we make them. To implement this functionality, text editors need to store all the user data somewhere and retrieve it in the reverse (**LIFO**) order.

### Nested function calls

This is another problem where the order of data items in a data store matters. A function call in almost all programming languages returns the execution to the calling function, which returns the execution to the function that called it, and this chain goes on. This order of returning control is essentially the reverse order in which the functions were called. The processor in a computer system has a smart data structure that stores the order of these function calls and returns the control in the reverse **(LIFO)** order when requested.

## Exploring a possible solution

**==A stack is a linear container that allows adding and removing items at only one end. This restriction on adding and removing items only from one end ensures that what goes last in the stack comes out first (LIFO).==**

### Stack data structure

![[Pasted image 20251012201707.png]]

Like a real-world stack, we can mimic the LIFO order by restricting the addition and removal of data only at one end. 

## Key properties of a stack

### Capacity

A stack's capacity is the maximum number of data items it can hold. Only **bounded** stacks have a predefined capacity. **Unbounded** stacks ideally have an unlimited capacity restricted only by the amount of memory available on the system where the code executing the stack implementation is running.

![[Pasted image 20251012201807.png]]

### Size

The size of a stack is the number of data items it holds at any given time. This value changes when data items are added to or removed from the stack.

![[Pasted image 20251012202341.png]]

### Top

The data item inserted last into the stack appears to be at the top of the stack in its logical representation; hence, it is called the **top** of the stack. If the stack is empty, there is no data at the top of the stack.

## Supported Operations

### Push

The push operation on a stack is the only way to add data to a stack. This operation adds a data item to the **top** of the stack and increases its size by 1.

![[Pasted image 20251012202558.png]]

![[Pasted image 20251012202611.png]]


### Pop

The pop operation is the only way to remove data from a stack. It removes the data item at the **top** of the stack and decreases its size by 1

![[Pasted image 20251012202645.png]]

![[Pasted image 20251012202656.png]]

### Size

Size is also a property of the stack. The size operation returns the value of this property, which is the current size of the stack.

![[Pasted image 20251012202904.png]]

### Top

Like size, the top is also a property of the stack, and the top operation returns the value of this property, which is the data item at the top of the stack.

![[Pasted image 20251012202926.png]]

# Array Implementation Of Stack

A stack is a linear data structure that only supports push and pop operations to add and remove data items from one end of the stack. This makes the **array** the perfect candidate to implement stacks. Most use cases can be solved using a **bounded** stack with a fixed capacity and cannot grow beyond that.

![[Pasted image 20251012203027.png]]

## State information

To implement a stack using an array, we also need to hold and keep up-to-date certain information about the stack alongside the array that holds all the data items. This information is necessary to ensure all stack operations work as desired

### Top Index

The index of the data item in the array that holds the top of the stack is the `topIndex`. The value of the `topIndex` changes when data items are pushed onto and popped from the stack. It is important to make sure that the `topIndex` always stores the index of the top of the stack for the proper functioning of all the operations.

![[Pasted image 20251012203328.png]]

### Size

It is important to keep track of the number of data items currently held in the stack. This value is also modified whenever data is pushed in or popped from the stack. It is important to ensure that this value is always correct and less than the total capacity of the array to prevent attempts to access memory outside the array, which is a frequent cause of program crashes. We don't need to hold the value of the size of the stack in a separate variable, as it can be derived from the value of `topIndex` in the array implementation of a stack.

![[Pasted image 20251012203412.png]]

### Capacity

Since an array has a fixed size when implementing a stack using an array, the size of the stack is **bounded** by the size of the array. It's very important to ensure we never exceed this capacity, so we must hold this information about the array's capacity somewhere. Just like the `topIndex` variable, we use another variable, `capacity` to hold the size of the array used to implement the stack.

![[Pasted image 20251012203434.png]]

## Representation in memory

We know that data items in an array reside in contiguous memory, so if we implement a stack as an array, all the data items in the stack will reside next to each other.

![[Pasted image 20251012203456.png]]


## Implementation

when implementing a stack using an array, we always need to keep track of some state information, which is necessary to perform operations on a stack. The state information, the array, and all the operations performed on a stack can be **encapsulated in a class**.

![[Pasted image 20251012203622.png]]

```java
class Stack {
    // Array to store the stack elements
    public int[] arr;
    // Maximum capacity of the stack
    public int capacity;
    // Index of the top element in the stack
    public int topIndex;

    public Stack(int capacity) {
        this.capacity = capacity;
        // Dynamically allocate memory for the stack array
        arr = new int[capacity];
        // Set initial top index to -1 (indicating an empty stack)
        topIndex = -1;
    }

    public int size() {
        // Size of the stack is the index of the top element plus 1
        return topIndex + 1;
    }

    public boolean empty() {
        // If top index is -1, the stack is empty
        return topIndex == -1;
    }

    public int top() {
        if (empty()) {
            // Return -1 if the stack is empty
            return -1;
        }
        // Return the element at the top index of the stack
        return arr[topIndex];
    }

    public boolean push(int val) {
        if (topIndex == capacity - 1) {
            // Return false if the stack is already full
            return false;
        }
        // Increment top index and add the val to the new top position
        arr[++topIndex] = val;
        // Return true to indicate successful push operation
        return true;
    }

    public int pop() {
        if (empty()) {
            // Return -1 if the stack is empty (nothing to pop)
            return -1;
        }
        // Return the element at the top index and decrement top index
        return arr[topIndex--];
    }
}
```


##  Design two stacks in an array

Given the skeleton of a **TwoStack class** that supports two stacks internally using a single array, complete this class by implementing all the stack operations below. 

> - **TwoStack(int capacity)** - Initializes the TwoStack object with the given capacity, which represents the total capacity of both stacks. Both stacks must share the same capacity. If it is not feasible for both internal stacks to be of equal size, the first stack should have a greater capacity than the second stack.
> - **top1()** - Returns the element at the top of the first stack. If the stack is empty, it returns `-1`.
> - **top2()** - Returns the element at the top of the second stack. If the stack is empty, it returns `-1`.
> - **push1(int val)** - Pushes the given value onto the first stack and returns `true` if the operation is successful. It returns `false` if the stack is full.
> - **push2(int val)** - Pushes the given value onto the second stack and returns `true` if the operation is successful. It returns `false` if the stack is full.
> - **pop1()** - Pops the top element from the first stack and returns its value. If the stack is empty, it returns `-1`.
> - **pop2()** - Pops the top element from the second stack and returns its value. If the stack is empty, it returns `-1`.

You must abide by the following constraints

1. Use a **single array** to implement both stacks. 

> The input should adhere to the following rules:
> 
> 1. The input should contain two arrays of the same size.
> 2. The first array should contain the list of operations, while the second should contain the corresponding operands for those operations.
> 3. The first index in the first array should contain **TwoStack**, and the first index in the second array should contain a single positive integer representing the capacity of the stack. This value is used to initialise the stack.
> 4. For each index in the first array that contains **push1**, or **push2** operations, the corresponding index in the second array should contain the value that needs to be pushed.
> 5. For each index in the first array that contains **pop1**, **top1**, **pop2**, or **top2** operations, the corresponding index in the second array should contain an empty array.

```java

```