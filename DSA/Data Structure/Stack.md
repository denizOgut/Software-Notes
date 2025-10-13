
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
class TwoStack {
    // Array to store elements
    public int[] arr;
    // Capacity of the array
    public int capacity;
    // Top index of the first stack
    public int topIndex1;
    // Top index of the second stack
    public int topIndex2;

    public TwoStack(int capacity) {
        this.capacity = capacity;
        arr = new int[capacity];
        // Initialize top index of the first stack as -1 (empty)
        topIndex1 = -1;
        // Initialize top index of the second stack as capacity (empty)
        topIndex2 = capacity;
    }

    public int top1() {
        if (topIndex1 == -1) {
            // Stack 1 is empty, return -1
            return -1;
        }
        // Return the element at the top of Stack 1
        return arr[topIndex1];
    }

    public int top2() {
        if (topIndex2 == capacity) {
            // Stack 2 is empty, return -1
            return -1;
        }
        // Return the element at the top of Stack 2
        return arr[topIndex2];
    }

    public boolean push1(int val) {
        if (topIndex1 + 1 >= topIndex2) {
            // Stack 1 is full, cannot push more elements
            return false;
        }
        // Increment top index of Stack 1 and assign val to that position
        arr[++topIndex1] = val;
        // Push operation was successful
        return true;
    }

    public boolean push2(int val) {
        if (topIndex2 - 1 <= topIndex1) {
            // Stack 2 is full, cannot push more elements
            return false;
        }
        // Decrement top index of Stack 2 and assign val to that position
        arr[--topIndex2] = val;
        // Push operation was successful
        return true;
    }

    public int pop1() {
        if (topIndex1 == -1) {
            // Stack 1 is empty, cannot pop any element
            return -1;
        }
        // Return the element at the top of Stack 1 and decrement top index
        return arr[topIndex1--];
    }

    public int pop2() {
        if (topIndex2 == capacity) {
            // Stack 2 is empty, cannot pop any element
            return -1;
        }
        // Return the element at the top of Stack 2 and increment top index
        return arr[topIndex2++];
    }
}
```

# Linked List Implementation Of Stack

 a linked list is another data structure that is the perfect candidate for implementing a stack. Unlike arrays, which have a fixed size and are used to implement **bounded** stacks, linked lists can be as big as the computer memory permits, so they can be used to implement an **unbounded** stack.

![[Pasted image 20251013122824.png]]

## State information

Like the array implementation, when implementing a stack using a linked list, we need to hold and keep updated certain **state information** alongside the linked list that holds all the data items to ensure all stack operations work as desired. Let us look at all the state information we need to maintain.

### Top

Unlike in the array implementation, where we had to use the `topIndex` to store the index of the top item in the array, in the linked list implementation, we can use the `head` or `tail` of the list as a reference to the top. If we restrict inserting data items only at the beginning of the list, the `head` of the list is also becomes the top of the stack. On the other hand, if we restrict inserting data items only at the end of the list, the `tail` becomes the top of the stack. In this course, we will use a linked list implementation that only allows insertion at the beginning of the list and hence the `head`  will be at the top of the stack.

![[Pasted image 20251013122852.png]]

### Current Size

Unlike the array implementation of a stack, where we derive the stack size using the value stored in the `topIndex` variable, the linked list implementation has no `topIndex` variable. To always know the current size of the stack, we need to store this information in a `currentSize` variable. Every time data is pushed onto or popped from the stack, the value of `currentSize` variable is incremented or decremented by 1.

![[Pasted image 20251013122915.png]]

### Capacity

The linked list implementation of a stack can be used to implement both **bounded** and **unbounded** stacks. Since unbounded stacks have unlimited capacity, we don't need to store the maximum limit in any variable. However, when implementing a bounded stack using linked lists, we store that maximum limit in a `capacity`variable similar to the array implementation. Whenever we add a data item to the stack, we must ensure that the queue size doesn't exceed the stack's capacity.

## Stack class

The fundamental idea is the same. However, the implementation is different.

![[Pasted image 20251013123425.png]]

## Implementation

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 * };
 */

class Stack {
    // Reference to the head of the stack
    public ListNode head;
    // Maximum capacity of the stack
    public int capacity;
    // Current number of elements in the stack
    public int currentSize;

    public Stack(int capacity) {
        // Initialize the capacity of the stack
        this.capacity = capacity;
        // Initialize the currentSize to zero
        this.currentSize = 0;
        // Initialize the head reference to null
        this.head = null;
    }

    public int size() {
        // Return the current number of elements in the stack
        return currentSize;
    }

    public boolean empty() {
        // Return true if the stack is empty, false otherwise
        return currentSize == 0;
    }

    public int top() {
        if (empty()) {
            // If the stack is empty, return -1 (an invalid value)
            return -1;
        }
        // Return the value of the element at the top of the stack
        return head.val;
    }

    public boolean push(int val) {
        if (currentSize == capacity) {
            // If the stack is already full, return false
            return false;
        }
        // Create a new node with the given val
        ListNode newNode = new ListNode(val);
        // Set the next reference of the new node to the current head
        newNode.next = head;
        // Update the head reference to the new node
        head = newNode;
        // Increment the count of elements in the stack
        currentSize++;
        // Return true to indicate a successful push operation
        return true;
    }

    public int pop() {
        if (empty()) {
            // If the stack is empty, return -1 (an invalid value)
            return -1;
        }
        // Store the value of the element at the top of the stack
        int value = head.val;
        // Create a temporary reference to the current head
        ListNode temp = head;
        // Update the head reference to the next node
        head = head.next;
        // Delete the old head node to free memory
        temp = null;
        // Decrement the count of elements in the stack
        currentSize--;
        // Return the value of the popped element
        return value;
    }
}
```

# Infix Postfix and Prefix Notations

## Infix Notation

The style of writing mathematical expression we humans are used to is called the **infix notation**. It is characterized by the placement of operation **between** its operands.

![[Pasted image 20251013141740.png]]

The infix notation seems very intuitive and easy to understand for us humans; however, parsing evaluation and expression written in this notation is quite a challenge for computer systems.

### Challenges with the infix notation

Let's consider how a computer evaluates a mathematical expression to understand the problem better. Most CPUs at the root level only do one mathematical operation, such as addition, subtraction, etc., at a time. Since all these are binary operations, they only take two input values at a time.

Consider the example of a mathematical expression where we must add two numbers. A CPU takes these two numbers as its input, performs the addition, and generates the result.

![[Pasted image 20251013141810.png]]

![[Pasted image 20251013141836.png]]

An expression must be evaluated in the correct order of precedence of its operations to get the correct results. Consider the following mathematical expression with different types of operations. To evaluate it correctly, the evaluation order of operation should follow the operator precedence rule, which means, in this case, we must start the evaluation from the middle and not the left.

Such an evaluation is quite easy for humans because we can easily jump back and forth in the expression, solve parts of expressions first, save contextual information in our brain, and iteratively evaluate each operation in the order of precedence until the entire expression is evaluated.

However, formulating this entire process as an algorithm for a CPU that only performs one binary operation at a time is very difficult. We would first need to parse the entire expression, identify all operations and their precedence, solve individual operations in the correct order, save the intermediate results, and repeat this process multiple times. All this becomes even more difficult when we add parentheses to this mix that can create an arbitrary level of nesting.

![[Pasted image 20251013141923.png]]

## Postfix Notation

The idea behind the postfix notation is quite simple: instead of writing operations between the operands, the operation is written **after** the operand. Hence, the name postfix notation is also known as the reverse Polish notation.

![[Pasted image 20251013142246.png]]

### Examples

![[Pasted image 20251013142455.png]]

### How does postfix notation work

In the infix notation, parentheses dictate the order in which operations are performed, and all operators follow specific precedence rules. The postfix notation, on the other hand, can be evaluated by traversing the expression sequentially from start to end.

![[Pasted image 20251013142644.png]]

To evaluate the postfix notation, we start from the leftmost item and keep moving to the right until we encounter an operator. We then use the required number of operands from the most recently seen operands to evaluate the operation, store the result, and keep moving right. This left-to-right evaluation implicitly enforces precedence, i.e., the operator operand pair that comes first is evaluated first. Hence, the postfix notation also eliminates the need for parentheses and operator precedence rules.

![[Pasted image 20251013142733.png]]

## Prefix Notation

 It is an alternative notation to write the mathematical expression where the operator is written **before** the operands. It is also called the Polish notation.

![[Pasted image 20251013143207.png]]

### Examples

![[Pasted image 20251013143232.png]]

### How does prefix notation work

The prefix notation is evaluated very similarly to the postfix notation, the only difference being that we evaluate the expression in reverse from end to start.

![[Pasted image 20251013143338.png]]

 start from the rightmost item and move to the left until we encounter any operator. We then use the required number of operands from the most recently seen operands to evaluate the operation, store the result, and keep moving left. This right-to-left evaluation implicitly enforces precedence, i.e., the operator operand pair that comes first is evaluated first. Hence, the prefix notation eliminates the need for parentheses and operator precedence rules.


![[Pasted image 20251013143419.png]]

