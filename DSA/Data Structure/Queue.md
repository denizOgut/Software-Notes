# Queue

## Understanding the problem

 there are cases when we need to process data in a **F**irst **I**n **F**irst **O**ut (**FIFO**) order. This is a fairly common requirement in many use cases

### Music players

This is perhaps the most visible use case where the order of data items matters. Almost all modern music players can add multiple songs to a list and play them one after the other in the **FIFO** order. This functionality is simple, but to implement this, we need to store all these songs somewhere and then play them in the order of their insertion.

### Call center

Like music players, this problem relies on the order of data added to a data store. Almost every automated call center reception software handles and processes calls made by customers in a **FIFO** order. To implement this functionality, this software needs to store the caller's information somewhere and retrieve it in the order of arrival to redirect it to the customer service agent when available.

## Disk scheduling

Consider a situation where you copy multiple files from one location to another. This is another problem where the order of data items in a data store matters. A computer system with a single hard disk can perform only a single read/write operation simultaneously, so it cannot copy multiple files simultaneously. Newer, more modern hardware can do simultaneous read/write, but for demonstrating an example of FIFO, we consider the old ones. These hardware devices generally have an internal data structure (queue) that stores all the read/write requests and processes them in the order of arrival (**FIFO**).


## Exploring a possible solution

**==A queue is a linear container that has two open ends. It allows data to be added at one end and removed from another. This condition imposed on adding and removing items from two different ends ensures that what goes first in the queue comes out first (FIFO).==**

### Queue data structure

![[Pasted image 20251016115614.png]]

Like a real-world queue, we can mimic the FIFO order by restricting the addition and removal of data at two fixed ends.

## Key properties of a queue

### Capacity

A queue's capacity is the maximum number of data items it can hold. Only **bounded** queues have a predefined capacity. **Unbounded** queues ideally have an unlimited capacity restricted only by the amount of memory available on the system where the code executing the queue implementation is running.

![[Pasted image 20251016115707.png]]

### Size

The size of a queue is the number of data items it holds at any given time. This value changes when data items are added to or removed from the queue.

![[Pasted image 20251016115721.png]]

### Front

The oldest data item in the queue is present at the front of the removing end, ahead of all the other items in the queue in the logical representation of the queue, and is hence called the **front** of the queue. **==This is the item that will be removed and processed next.==**

![[Pasted image 20251016115913.png]]

### Back

The most recent data item inserted into the queue is at the other end of the removing end behind all the other data items and is hence called **back**. The back of the queue is also sometimes called the **rear**.

![[Pasted image 20251016115934.png]]

## Supported Operations

### Enqueue

The enqueue operation is the only way to add data to a queue. This operation adds a data item to the **back** of the queue and increases its size by 1.

![[Pasted image 20251016120301.png]]

### Dequeue

The dequeue operation is the only way to remove data from a queue. It removes the data item at the **front** of the queue and decreases its size by 1.

![[Pasted image 20251016120331.png]]

### Size

**Size** is also a property of the queue. The size operation returns the value of this property, which is the current size of the queue.

### Front

Like size, **front** is also a property of the queue, and the front operation returns the value of this property, which is the data item at the front of the queue.

![[Pasted image 20251016120401.png]]

### Back

The queue also has a property called **back**, and the back operation returns the value of this property, which is the data item at the end (back) of the queue.

![[Pasted image 20251016120706.png]]

# Array Implementation Of Queue

A queue is a linear data structure that only supports enqueue and dequeue operations to add and remove data items from the **ends** of the queue. This makes the array the perfect candidate to implement a queue. Most use cases can be solved using a **bounded** queue with a fixed size and cannot grow beyond that.

![[Pasted image 20251016120807.png]]

### State information

To implement a queue using an array, we must keep current information about the queue alongside the array that holds all the data items. This information is necessary to ensure all queue operations work as desired. Let us look at all the state information we need to maintain.

#### Front index

The index of the data item in the array that holds the **front** of the queue is the `frontIndex`. The value of the `frontIndex` changes when data items are **dequeued** from the queue. It is important to ensure that the `frontIndex` always store the index of the front of the queue for the proper functioning of all the operations.

![[Pasted image 20251016120905.png]]

#### Back index

The index of the data item in the array that holds the **back** of the queue is the `backIndex`. The value of the `backIndex` changes when data items are **enqueued** into the queue. Just like the `frontIndex`, it is important to ensure that the `backIndex` always stores the index at the back of the queue for the proper functioning of all the operations.

![[Pasted image 20251016120916.png]]

#### Size

It is important to keep track of the number of data items currently held in the queue. It is important to ensure that this value is always correct and less than the total capacity of the array to prevent attempts to access memory outside the array, which is a frequent cause of program crashes. To always know the current size of the queue, we need to store this information in a `currentSize` variable. Every time data is enqueued or dequeued from the queue, the value of `currentSize` is incremented or decremented by 1.

![[Pasted image 20251016121031.png]]

#### Capacity

Since an array has a fixed size, the queue size is **bounded** by the array size when implementing a queue using an array. It's very important to ensure we never exceed this capacity, so we must hold this information about the array's capacity somewhere. We use another variable, `capacity` to hold the size of the array used to implement the queue.

## Cyclic nature of array based queues

Unlike stacks, data is inserted into and removed from the queue from **two ends**. The front end only removes data items from the queue, and the back end only adds data items to the queue.## implementation

However, **==when implementing queues in an array using indexes to represent the front and the back of the queue, any addition to the queue is done at the `backIndex` and any removal is done at the `frontIndex`==**. Since the size of an array is fixed, every enqueue and dequeue operation moves the front or the back of the queue **forward** in the array that holds them. To understand this better, let us look at an example of a queue(capacity 6) implemented as an array that tries to perform the same operations as in the generic queue above.

the front and the back of the queue move **forward** in the array that holds them, and eventually, the `backIndex` hits the end of the array. At this point, no more data can be added **after** the `backIndex`.

However, the queue size is still less than the capacity(6), and there is room for more data. There are empty spaces before the `frontIndex` in the queue created by the data items that were dequeued from the queue. As we can see from the example, the front and the back of the queue always move in the array that holds them.

![[Pasted image 20251016121418.png]]

### Cyclic movement

**==To get over this problem, the moment the `backIndex` reaches the end of the array, the next data item is added to the start of the array if it is empty. This becomes the new `backIndex` for the queue in the array, and any subsequent data items are added after it.==**

## Implementation

when implementing a queue using an array, we always need to keep track of some state information, which is necessary to perform operations on a queue. The state information, the array, and all the operations performed on a queue can be **encapsulated in a class**.

![[Pasted image 20251016121647.png]]

```java
class Queue {
    // Pointer to the dynamic array representing the queue
    public int[] arr;
    // Maximum capacity of the queue
    public int capacity;
    // Index of the front element in the queue
    public int frontIndex;
    // Index of the back element in the queue
    public int backIndex;
    // Current number of elements in the queue
    public int currentSize;

    public Queue(int capacity) {
        this.capacity = capacity;
        // Allocating memory for the queue
        this.arr = new int[capacity];
        // Initializing front index to 0
        this.frontIndex = 0;
        // Initializing back index to -1
        this.backIndex = -1;
        // Initializing current size to 0
        this.currentSize = 0;
    }

    public int size() {
        // Returns the current size of the queue
        return currentSize;
    }

    public boolean empty() {
        // Returns true if the queue is empty, false otherwise
        return size() == 0;
    }

    public int front() {
        if (empty()) {
            // Returns -1 if the queue is empty
            return -1;
        }
        // Returns the element at the front of the queue
        return arr[frontIndex];
    }

    public int back() {
        if (empty()) {
            // Returns -1 if the queue is empty
            return -1;
        }
        // Returns the element at the back of the queue
        return arr[backIndex];
    }

    public boolean enqueue(int val) {
        if (currentSize == capacity) {
            // Returns false if the queue is full and cannot enqueue more
            // elements
            return false;
        }
        // Calculates the next back index in a circular manner
        backIndex = (backIndex + 1) % capacity;
        // Inserts the new element at the back of the queue
        arr[backIndex] = val;
        // Increments the current size
        currentSize++;
        // Returns true to indicate a successful enqueue operation
        return true;
    }

    public int dequeue() {
        if (empty()) {
            // Returns -1 if the queue is empty and cannot dequeue
            // elements
            return -1;
        }
        // Stores the element to be dequeued
        int dequeuedElement = arr[frontIndex];
        // Calculates the next front index in a circular manner
        frontIndex = (frontIndex + 1) % capacity;
        // Decrements the current size
        currentSize--;
        // Returns the dequeued element
        return dequeuedElement;
    }
}
```


# Linked List Implementation Of Queue

Like an array, a linked list is another data structure that is the perfect candidate for implementing a queue. Unlike arrays, which have a fixed size and are used to implement **bounded** queues, linked lists can be as big as the computer memory permits, so they can be used to implement an **unbounded** queue.

![[Pasted image 20251017110057.png]]

Like arrays, a class can **encapsulate** all the state information needed to implement a queue using a linked list, along with the linked list itself and all the operations that can be performed on a queue. The fundamental idea is the same. However, the implementation is different.

![[Pasted image 20251017110351.png]]

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

class Queue {
    // Capacity of the queue (maximum number of elements it can hold)
    public int capacity;
    // Current number of elements in the queue
    public int currentSize;
    // Reference to the front of the queue
    public ListNode head;
    // Reference to the rear of the queue
    public ListNode tail;

    public Queue(int capacity) {
        this.capacity = capacity;
        currentSize = 0;
        head = null;
        tail = null;
    }

    public int size() {
        // Returns the current number of elements in the queue
        return currentSize;
    }

    public boolean empty() {
        // Returns true if the queue is empty, false otherwise
        return currentSize == 0;
    }

    public int front() {
        // Returns -1 if the queue is empty
        if (empty()) {
            return -1;
        }
        // Returns the value of the element at the front of the queue
        return head.val;
    }

    public int back() {
        // Returns -1 if the queue is empty
        if (empty()) {
            return -1;
        }
        // Returns the value of the element at the back of the queue
        return tail.val;
    }

    public boolean enqueue(int val) {
        // Returns false if the queue is full and cannot enqueue more
        // elements
        if (currentSize == capacity) {
            return false;
        }
        // Create a new node with the given val
        ListNode newNode = new ListNode(val);
        // If the queue is empty, the new node becomes both the front
        // and rear node
        if (empty()) {
            head = newNode;
            tail = newNode;
        }
        // Otherwise, add the new node to the end of the queue and update
        // the tail reference
        else {
            // Add the new node to the end of the queue
            tail.next = newNode;
            // Update the tail reference to the new node
            tail = newNode;
        }
        // Increase the current size of the queue
        currentSize++;
        // Return true to indicate successful enqueue operation
        return true;
    }

    public int dequeue() {
        // Returns -1 if the queue is empty and cannot dequeue any
        // elements
        if (empty()) {
            return -1;
        }
        // Create a temporary reference to the front node
        ListNode frontNode = head;
        // Get the value of the front node
        int dequeuedData = frontNode.val;
        // Update the front reference to the next node in the queue
        head = head.next;
        // Delete the previous front node
        frontNode = null;
        // If the front reference is null after dequeue, the queue
        // becomes empty, so update the tail reference as well
        if (head == null) {
            tail = null;
        }
        // Decrease the current size of the queue
        currentSize--;
        // Return the dequeued value
        return dequeuedData;
    }
}
```