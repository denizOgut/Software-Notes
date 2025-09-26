
#  Linked list

A linked list is a linear and dynamic data structure that **==stores data sequentially at random memory locations. Instead of storing all the data items in a contiguous block of memory like arrays, a linked list stores them at random locations in memory.==** Whenever a new item is to be added, a new memory block is dynamically created to store this new value, which is then added to the chain of already existing items, effectively extending the **linked list**.

## Linked lists vs arrays

A linked list guarantees the insertion and deletion of items from the **start** and **end** of the list in **O(1)** space and **O(1)** time. It also guarantees the insertion and deletion of any data item **without** using any extra space.

![[Pasted image 20250926111359.png]]


## Advantages

- **Dynamic size:** The size of a linked list is not fixed. Adding or removing items can increase or decrease at will during runtime.
- **Efficient performance:** Insertion and deletion of the first node is an **O(1)** operation.

## Limitations

- **Extra space:** A little extra memory is required to store an item in a linked list compared to an array. The extra space is used to store the information of the next item in the sequence.
- **Traversal:** Traversal in a linked list is more time-consuming than an array since random access using an index is not possible. To access an item at position **n**, one must traverse all the items before it.

# Node 

**==A node is the fundamental building block of a linked list. It holds the actual data item and information of the next node. Multiple nodes, when chained together, make up a single linked list.==** All the operations on a linked list are performed by manipulating individual nodes and their links. Inserting, deleting, or updating data items in a list are all performed using the list's nodes.

## Structure of a node

A singly linked list node has two sections.

> - **val:** The actual data item a node holds. This could be of any type.
> - **next:** This is a reference to the next node in the list

![[Pasted image 20250926111919.png]]

## Implementing a node

```java
  
class ListNode {
    int val;
    ListNode next;
    ListNode() {}
    ListNode(int val) { this.val = val; }
};
```

# Structure of a singly linked list

A linked list is just a chain of nodes.

![[Pasted image 20250926112037.png]]

When represented logically in a diagram, these nodes might look sequential (left to right, one after the other), but in reality, they are scattered all around in memory at random locations, and the only way to access a node is by using its address in memory.

![[Pasted image 20250926112226.png]]

## Head Node

The first node of a linked list is also called the **head** node.a node in the linked list can only be accessed using its memory reference. This reference, however, is stored in the node before it in the logical representation, and **==this is true for every node except the first node, as it does not have any previous node. This is why, to access a linked list, we should always have the reference to the head node stored somewhere.==**

![[Pasted image 20250926112345.png]]

## Tail Node

The last node of a linked list is called a **tail** node. Just like the first node does not have any node before it, the last node does not have any node after it. What is stored in the `next` pointer of the tail node. **==The `next` pointer of the tail node stores a reference to `null`, which means nothing==**

![[Pasted image 20250926112447.png]]

# Supported Operations

Every data structure is essentially used to store, retrieve, and manipulate data efficiently. On a high level, there are three basic types of operations on any data structure. 

- Traversal
- Insertion
- Deletion

![[Pasted image 20250926112918.png]]


## Boundary node

Given the **head** of a singly linked list and a reference to a **random** node, write a function to check if it is a boundary node.

You need to do this without traversing the list. It is guaranteed that the list will not contain duplicates.

A boundary node is a linked list's first or last node.

- If the given node is the first node, return `first`
- If it is the last node, return `last`
- If it is both the first and last node, return `both`
- For all other cases, return `none`

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

class Solution {

    public String boundaryNode(ListNode head, ListNode node) {

        // If either head or node is null, return "none"

        if (head == null || node == null) {

            return "none";

        }


        // If head and node are the same, and node has no next node,

        // return "both"

        else if (node == head && node.next == null) {

            return "both";

        }

        // If head and node are the same, but node has a next node,

        // return "first"

        else if (node == head) {

            return "first";

        }


        // If node is the last node (i.e., it has no next node), return

        // "last"

        else if (node.next == null) {

            return "last";

        }


        // If none of the above conditions are met, return "none"

        return "none";
    }
}
```

# Traversal

 Traversal in linked lists is quite similar to arrays as they are both linear data structures, but it is also different as the data items in linked lists are not stored in contiguous memory blocks.

Data in a singly linked list is not stored in continuous memory, so we do not have indexes for random access like arrays. All the nodes are present at different memory locations

Instead of an integer loop control variable representing an item's index in an array, we use a variable referencing a node in the linked list as the loop control variable. Every time we want to move forward, we assign the node's reference in the linked list to this variable. We can get the node's reference by looking at the value stored in the `next` pointer of the current node.

**==Since linked lists are dynamic, we don’t know their length in advance, and therefore, we have to keep traversing until we reach a node with a `null` value stored in its `next` pointer. That is how we know we have reached the end of a linked list.==**

![[Pasted image 20250926115937.png]]

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

// For loop to iterate over the linked list

for (ListNode current = head; current != null; current = current.next) {

    // Perform operations on current

    // Example: current.val = current.val + 1;

}

// While loop to iterate over the linked list

ListNode current = head;

while (current != null) {

    // Perform operations on current

    // Example: System.out.println(current.val);

    current = current.next;

}
```

## Example Node expedition

Given the **head** of a singly linked list, write a function to print a comma (`,`) separated list of all the values from the start to the end.

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

class Solution {

    public void nodeExpedition(ListNode head) {

        ListNode current = head;

        while(current != null) {

            System.out.print(current.val);

            if(current.next != null)

                System.out.print(", ");

            current = current.next;

        }
    }
}
```

## Example Length of the list

Given the **head** of a singly linked list, write a function that returns the length of the list.

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

  
class Solution {

    public int lengthOfTheList(ListNode head) {

        ListNode current = head;

        int counter = 0;

  
        while(current != null) {

            counter++;

            current = current.next;

        }

        return counter;
    }
}
```

## Example Node search

Given the **head** of a singly linked list and a **data** value, write a function to return the first node containing the given data. If no such node is found, return `null`.

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

class Solution {

    public ListNode nodeSearch(ListNode head, int data) {

        ListNode current = head;

        while(current != null) {

            if(current.val == data)

                return current;

            current = current.next;

        }

        return null;
    }
}
```

## Example Node search 2

Given the **head** of a linked list and a data value, write a function to return **all** the nodes containing the given data.

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

class Solution {

    public List<ListNode> nodeSearchII(ListNode head, int data) {

        List<ListNode> result = new ArrayList<>();

        ListNode current = head;

        while(current != null) {

            if(data == current.val)

                result.add (current);

            current = current.next;

        }
        return result;
    }
}
```

## Example Intersection point

Given the **head** of two singly linked lists, `headA` and `headB`, write a function to find if these two linked lists intersect at any point, and if they do, return the reference to the node where they intersect. Your function should return `null` if the given lists don't intersect.

The input uses the following format

- **``intersectVal``** - The value of the node where the intersection occurs. This is 0 if there is no intersection.
- **``headA``** - The first linked list.
- **``headB``** - The second linked list.
- **``skipA``** - The number of nodes to skip ahead in ``listA`` (starting from the head) to get to the intersected node.
- **``skipB``** - The number of nodes to skip ahead in ``listB`` (starting from the head) to get to the intersected node.

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }

 * };

 */

 import java.util.*;

class Solution {

    public ListNode intersectionPoint(ListNode headA, ListNode headB) {

        if (headA == null || headB == null) return null;

        ListNode pointerA = headA;

        ListNode pointerB = headB;

        // When one pointer reaches the end, redirect it to the other list's head

        // This ensures both pointers travel the same distance

        while (pointerA != pointerB) {

            pointerA = (pointerA == null) ? headB : pointerA.next;

            pointerB = (pointerB == null) ? headA : pointerB.next;

        }

        return pointerA; // Either the intersection node or null

    }
    

	public ListNode intersectionPoint(ListNode headA, ListNode headB) {
	    Set<ListNode> visitedNodes = new HashSet<>();
	    ListNode currentA = headA;
	    
	    // Add all nodes from list A to the set
	    while(currentA != null) {
	        visitedNodes.add(currentA);
	        currentA = currentA.next;
	    }
	    
	    ListNode currentB = headB;
	    // Check each node in list B
	    while(currentB != null) {
	        if(visitedNodes.contains(currentB)) {
	            return currentB;
	        }
	        currentB = currentB.next;
	    }
	    return null;
	}

}
```

# Insertion

## Inserting at the beginning

Inserting at the beginning of a linked list is a fundamental and commonly used operation. When designing an algorithm for any data structure, it's important not to make assumptions about its underlying characteristics and to design the logic for a general case. 

there are two cases to consider when inserting at the beginning of a singly linked list.

### 1. The list is empty

In this scenario, if the linked list is empty, the **head** would be `null`. We need to initialize the **head** node of the linked list and ensure that the `next` pointer of this newly created **head** node is `null`, as this new node will also be the last node of the list.

![[Pasted image 20250926140616.png]]

**Algorithm**

- **Step 1:** Create a new node with the given data.
- **Step 2:** Set the new node's `next` pointer to `null` since it's the only node.
- **Step 3:** Return the new node, as this node is also the **head** node.

### 2. The list is not empty

already have some data in the linked list, so the **head** is not `null`. Therefore, to insert a new node at the beginning of the list, we need to update the `next` pointer of the newly created node to store the reference of the existing **head** node.

![[Pasted image 20250926141001.png]]

**Algorithm**

- **Step 1:** Create a new node with the given data.
- **Step 2:** Set the new node's `next` pointer to hold the reference of the current head.
- **Step 3:** Return the new node, as this is the new head.

```java
/**
 * Definition for singly-linked list.
   
 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

  

class Solution {

    public ListNode insertAtBeginning(ListNode head, int data) {

        // Create a new node with the given data

        ListNode newNode = new ListNode(data);

        // If the list is empty (head is null)

        if (head == null) {

            // Set the next pointer to null since it's the only node

            newNode.next = null;

            // Return the newNode as this is the new head
            return newNode;
        }

        // Set the next pointer of the new node to the current head,

        // making the new node the new head
        newNode.next = head;

        // Return the newNode as this is the new head
        return newNode;
    }

}
```

## Insertion at End

Unlike insertion at the beginning, this operation adds a new node at the end of the list. To add a new node at the end of a singly linked list, we first need to locate the tail node of the linked list. Then, we can create a new node and update the `next` pointer of the tail node to point to the newly created node. Since we need to traverse the entire list to insert the new node, this operation is not as efficient as insertion at the beginning. When inserting at the end of a singly linked list, there are two cases to consider.

### 1. The list is empty

In this scenario, if the linked list is empty, the **head** will be `null`. We need to initialize the **head** node of the linked list and ensure that the `next` pointer of this newly created **head** node is `null`, as this newly created node will also be the last node of the list.

![[Pasted image 20250926141744.png]]

**Algorithm**

- **Step 1:** Create a new node with the given data.
- **Step 2:** Set the new node's `next` pointer to `null` since it's the only node.
- **Step 3:** Return the new node, as this node is also the head node.

### 2. The list is not empty

In this scenario, once the new node is created, we must move through the list from the beginning until we reach the last node. Also, we need to ensure that the `next` pointer of the newly created node is set to `null`. Finally, we update the `next` pointer of the last node to point to the newly created node.

**Algorithm**

- **Step 1:** Create a new node with the given data.
- **Step 2:** Traverse the list, keeping track of the `current` node until reaching the last node.
- **Step 3:** Set the new node's `next` pointer to `null` since it will be the new last node.
- **Step 4:** Set the last node's `next` pointer to hold the reference of the new node.
- **Step 5:** Return the original head node.

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

class Solution {

    public ListNode insertAtEnd(ListNode head, int data) {

        // Create a new node with the given data

        ListNode newNode = new ListNode(data);

        // If the list is empty

        if (head == null) {
            // Set the next pointer of the new node to null
            newNode.next = null;

            // Return the new node as the new head of the list
            return newNode;
        }

  
        // Traverse the list to find the last node
        ListNode current = head;
        while (current != null && current.next != null) {
            current = current.next;
        }

        // Set the next pointer of the new node to null
        newNode.next = null;

        // Link the last node to the new node
        current.next = newNode;

  
        // Return the original head of the list
        return head;
    }
}
```


## Insertion After The Given Node

Unlike arrays, we can insert data at any point in a linked list without recreating the entire list. When inserting after a node in a linked list, there are two cases to consider.

### 1. The list is empty

If the list is empty and contains no elements, we cannot find the given node because it does not exist within the list. Inserting a new node after the given node is not possible because there is no reference point within the list to perform the insertion. In such a case, the method would return without making any changes.

### 2. The list is not empty

Since the new node will be inserted between two existing nodes, we must ensure that we properly set up the `next` pointers of these nodes. Inserting after a given node is a three-step process.

**Algorithm**

- ==**Step 1:** Create a new node with the given data.==
- ==**Step 2:** Set the `next` pointer of the new node to hold the node's reference stored in the `next` pointer of the `given` node.==
- ==**Step 3:** Set the `next` pointer of the `given` node to hold the reference of the new node.==

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */  

class Solution {

    public void insertAfterTheGivenNode(ListNode node, int data) {

        // Check if the given node is null

        if (node == null) {

            // If the given node is null, there is nothing to do
            return;
        }

        // Create a new node with the provided data
        ListNode newNode = new ListNode(data);

        // Set the next pointer of the new node to the next pointer of
        // the given node
        newNode.next = node.next;


        // Set the next pointer of the given node to the new node
        node.next = newNode;

    }

}
```

## Insertion Before The Given Node

### 1. The list is empty

If the list is empty and contains no elements, we cannot find the given node because it does not exist within the list. Inserting a new node after the given node is not possible because there is no reference point within the list to perform the insertion. In such a case, we can return the **head** node that was provided as it is.

### 2. The given node is the first node

This is similar to **inserting at the beginning**, which we learned earlier. To determine if the given node is the first node, we can compare it to the **head** node. If both nodes are the same, then the given node is the **head** node.

![[Pasted image 20250926143332.png]]

**Algorithm**

- **Step 1:** Create a new node with the given data.
- **Step 2:** Set the new node's `next` pointer to hold the reference of the current head.
- **Step 3:** Return the new node, as this is the new head.


### 3. The given node is not the first node

The problem we face is that we don't have the reference of the previous node of the given node. This is needed to restore the link after the new node has been inserted.

**How do we get the reference of the previous node?**

**==To achieve this, we can create a new variable called `previous` which will initially be set to `null`. As we traverse through the nodes, we update both the `current` and `previous` variables at each step. When we find the node before which we want to insert the new node, the `current` variable will hold the reference of that node, and the `previous` variable will hold the node's reference just before it.==**

After gaining access to the previous node, this problem boils down to **inserting after a given node**, where the given node is the previous node. Following the four steps below, a new node will be inserted, and the links will be restored.

**Algorithm**

- **Step 1:** Create a new node with the given data.
- **Step 2:** Search for the node before which we need to insert the new node, while keeping track of the `current` and `previous` nodes.
- **Step 3:** Set the new node's `next` pointer to hold the reference of the `given` node.
- **Step 4:** Set the `next` pointer of the `previous` node to hold the reference of the new node.
- **Step 5:** Return the original head node.

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

class Solution {

    public ListNode insertBeforeTheGivenNode(

        ListNode head,

        ListNode node,

        int data

    ) {

        // Check if the head or node is null

        if (head == null || node == null) {
            return head;
        }


        // Create a new node with the given data
        ListNode newNode = new ListNode(data);

  
        // If the given node is the head, insert the new node before it
        if (node == head) {
            newNode.next = head;

            // Return the newNode as this is the new head
            return newNode;

        }

        // Traverse the linked list until the current node matches the
        // given node
        ListNode current = head;
        ListNode previous = null;

  
        while (current != null && current != node) {
            previous = current;
            current = current.next;
        }

  

        // If the current node is null, the given node was not found in
        // the linked list
        if (current == null) {
            return head;
        }

  

        // Insert the new node before the given node
        newNode.next = current;
        previous.next = newNode;


        // Return the head of the modified linked list
        return head;
    }
}
```


**Does the order of updating the previous and next variables matter?**

It is crucial to update the `previous` and `current` variables in the correct order while traversing the list. If we were to change the order and do something like this:
`current = current.next;`
`previous = current;`
We would end up with incorrect results. This is because if we update the `current` variable to hold the reference of the next node in the list and then update the `previous` variable, the `previous` variable will no longer point to the previous node of the current node but to the current node itself. Understanding reference manipulation in a linked list might seem challenging, but once the concepts are clear, it all makes sense.

## Insertion at a Given Distance

 insertion at a given distance `X` can be achieved by piggybacking on the length finding algorithm. Both search and finding length rely on the traversal algorithm.

### 1. If the list is empty and X > 0

Attempting to insert a node at a position greater than 0 in an empty list is an invalid operation. In an empty list, no nodes are present, so the only valid position for insertion would be at position 0, making the new node the head of the list. However, when X is greater than 0, no corresponding position is available for insertion because the list lacks any elements. Therefore, we will return the existing **head**.

### 2. X = 0

This means simply inserting a node at the beginning of a list

![[Pasted image 20250926145649.png]]

**Algorithm**

- **Step 1:** Create a new node with the given data.
- **Step 2:** Set the new node's `next` pointer to hold the reference of the current head.
- **Step 3:** Return the new node, as this is the new head.

### 3. X <= size of the list

If the list is not empty, we need to traverse it while keeping a counter variable with the initial value of 0. Moving through the linked list, we increment this counter by 1 to keep track of the current index. We continue traversing the list until the counter has a value of `X-1`, which lands us at the node just **after** where we want to insert the new node. Now, the problem essentially comes down to **inserting after the given node**

> **Algorithm**
> 
> - **Step 1:** Create a new node with the given data.
> - **Step 2:** Traverse a distance of X - 1 while keeping track of the `current` node.
> - **Step 3:** Set the new node's `next` pointer to hold the node's reference stored in the `next` pointer of the `current` node.
> - **Step 4:** Set the current node's `next` pointer to hold the reference of the new node.
> - **Step 5:** Return the original head node.

### 4. X > size of the list

If the value of `X` is greater than the list's size, it indicates an invalid case. For example, it is not possible to insert a node at position 5 in a list with only two items, we will return the existing **head**.

```java
/**

 * Definition for singly-linked list.

 * class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 * };

 */

class Solution {

    public ListNode insertAtGivenDistance(

        ListNode head,

        int X,

        int data

    ) {

        // If the list is empty and X is greater than 0, insertion is not
        // possible, return null

        if (head == null && X > 0) {
            return null;
        }


        // Create a new node with the given data

        ListNode newNode = new ListNode(data);

        // If X is 0, insert the new node at the beginning of the list

        if (X == 0) {

            // Set the next pointer of the new node to the current head,
            // making the new node the new head.
            newNode.next = head;
            // Return the newNode as this is the new head

            return newNode;
        }


        // Pointer to traverse the list
        ListNode current = head;


        // Counter to track the number of nodes traversed
        int counter = 0;

  
        // Traverse the list until reaching the desired distance or the
        // end of the list
        while (current != null && counter < X - 1) {


            // Move to the next node

            current = current.next;

            // Increment the counter
            counter++;

        }

  

        // If the list is shorter than X-1, it's not possible to insert

        // the new node, so return head.

        if (current == null) {
            return head;

        }

  
        // Set the next pointer of the new node to the current node
        newNode.next = current.next;

        // Update the next pointer of the current node to point to the
        // new node
        current.next = newNode;

  
        // Return the updated head of the list
        return head;

    }
}
```


# Deletion

